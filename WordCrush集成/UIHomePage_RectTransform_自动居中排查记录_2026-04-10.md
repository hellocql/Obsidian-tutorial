# UIHomePage RectTransform 自动居中排查记录（2026-04-10）

## 问题现象

- 文件：`Assets/Bundles/UI/HomePage/UIHomePage.prefab`
- 预期：`RectTransform` 为拉伸锚点时，`Left/Top/Right/Bottom` 初始都为 `0`
- 实际：页面加载后被“自动居中”，`Left/Right`、`Top/Bottom` 变成非 0，导致布局错乱
- 临时处理：手动改回 `0` 后显示正常

## 排查范围

- 业务页脚本：`Assets/Scripts/UI/HomePage/UIHomePage.cs`
- 页面框架：`Assets/Scripts/UI/UIFramework/PageManager.cs`
- 挂载工具：`Assets/Scripts/Game/Core/Utility/UGUIUtility.cs`
- 适配器（排除项）：`IPhoneXAdapter`、`IPhoneXFillAdapter`
- 资源实例化链路（辅助分析）：`MockResourceService`

## 关键证据

### 1) `UIHomePage.cs` 未直接改 RectTransform

在 `UIHomePage.cs` 未发现对以下字段的直接写入：

- `anchorMin/anchorMax`
- `offsetMin/offsetMax`
- `anchoredPosition`
- `sizeDelta`

### 2) 页面打开时会重挂父节点

`PageManager.DoOpenPage()` 中执行：

- `pPage.transform.SetCusParent(pageRoot);`

### 3) 旧实现会保留世界坐标

`UGUIUtility.SetCusParent(...)` 旧代码使用：

- `InTrans.SetParent(InParent);`（等价于 `worldPositionStays = true`）

这会导致 UI 在重挂父节点时，为保持世界位置而重新计算 offset。  
当锚点是全拉伸时，常见结果就是 `Left/Right`、`Top/Bottom` 变成类似父节点半尺寸的大值（例如 540/960）。

### 4) 运行信息辅助排除

- 运行环境：`Unity Editor (Windows)`
- `UIHomePage` 根/Panel：未挂 `IPhoneXAdapter/IPhoneXFillAdapter/Layout*`

因此 iPhoneX 适配器/布局组件自动重排不是本次主因。

## 根因结论

主因是：**UI 页面在打开流程中重挂父节点时，使用了 `SetParent(parent)`（默认保留世界坐标），导致拉伸型 RectTransform 的 offset 在运行时被重算，表现为“自动居中”和边距非 0。**

## 实际修复

修改文件：

- `Assets/Scripts/Game/Core/Utility/UGUIUtility.cs`

修复方式：

- 将 `SetCusParent(...)` 的所有重载内  
  `InTrans.SetParent(InParent);`  
  改为  
  `InTrans.SetParent(InParent, false);`

目的：

- 重挂父节点时以**本地坐标系**为准，不保留世界坐标，避免拉伸 offset 异常重算。

说明：

- `AddChild(...)` 中的 `SetParent(InParent)` 本次未改，避免扩大影响面（该路径与页面重挂逻辑不同）。

## 修复后预期

在 HomePage 正常打开链路下：

- `UIHomePage` 根节点保持 stretch 锚点
- `Left/Top/Right/Bottom` 不再跳成 540/960 一类值
- 页面不再“自动居中”导致错位

## 建议回归清单

- 打开 `UIHomePage`，确认根节点四边距保持 0
- 从其他全屏页面切回 Home，确认无跳动
- 检查 2~3 个依赖 `SetCusParent` 的页面（如结算页/活动页）确认无位置回归
- 若个别特效节点此前依赖保留世界坐标，改用显式 `SetParent(parent, true)`（按需点修）

## 本次结论摘要

- Prefab 初值本身不是核心问题
- 问题发生在“运行时重挂父节点”的默认行为
- 已通过统一改为 `SetParent(..., false)` 修复主路径

