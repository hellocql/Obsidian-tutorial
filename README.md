# Obsidian，宇宙最强个人笔记软件

之前看过挺多人说Obsidian的，自己也下过这软件，但当时尝试一下就放弃了。大概因为一开始没意识到Obsidian万丈高楼平地起的插件逻辑，以为它功能就那么简单。而且我本来一直用Notion，那个时候感觉Notion天下无敌，Obsidian看起来不可能实现Notion那些丰富的功能

直到最近，误打误撞发现Obsidian强大的插件生态，这才意识到Obsidian需要靠插件支棱起来。大多数我原以为Obsidian无法实现的Notion功能，实际可以通过插件实现。相较于Notion这种商业软件，Obsidian的插件逻辑给到用户很大自由度。不仅可以选择添加、删除哪些功能，更好地适配个人需求。大多数插件内部也有包括功能、外观等自定义选项，进一步提高用户对笔记整体的细粒度控制

如果有一定编程基础，或者会用AI氛围编程，你可以在Obsidian实现几乎任何别家笔记软件的功能，甚至创造新功能。这种自由度使得Obsidian非常适合作为个人笔记平台

有一个有意思的比喻：如果说Notion是一把瑞士军刀，Obsidian就是乐高积木。你可以用积木搭建任何武器，比如剑，长矛，锤子，还能在这些武器中随意切换。这可以让你的笔记适应更多需求场景

但如果你用积木做一个和Notion一样的瑞士军刀，积木的质量怎么和钢抗衡呢？这也确实反映了Notion作为一个体系完备的商业软件，相同的功能，维护和实现上普遍来讲都会比Obsidian更好用的状况

两个软件面向群体不同。Notion适合小白，团队协作场景；Obsidian则适合有一定笔记软件以及编程基础，笔记主要用于个人业务的用户

我用了大概一个星期了解、添加Obsidian第三方社区插件中最热门，实用的插件，并把Obsidian主题、布局等调整成我习惯的样子。一些功能较多的复杂插件还在学习，如Excalidraw

虽然我本身用Notion比较久，对Markdown笔记软件相对熟悉，也有一定编程基础，但Obsidian一开始用起来还是有些费劲。时间上有很多花在问AI这些插件分别用来做什么，截图插件设置项给AI让AI解释，以及让AI写具体例子向我展示插件作用，帮助我更好地理解插件应用场景

由此我想到做一个GitHub仓库，以Obsidian Vault（Obsidian笔记库）的形式呈现，专门用于介绍Obsidian基础设置，最热门第三方插件的用法（包含每个插件后台设置选项介绍）。对于Dataview，Meta Bind，Kanban，Projects这种复杂插件，配上案例以帮助读者真正体验、理解插件。这样新入坑Obsidian的小伙伴就不用自己一个个问AI，让AI想案例啥的，直接从Obsidian Vault中统一查看可以节省大家很多时间

如前所述，仓库将以Obsidian Vault的形式呈现，这个Vault和我平时使用的Obsidian Vault设置上一模一样，大多数Obsidian实用插件都已安装，界面也很简洁。好处是大家不用在自己安装，我写教程时也趁手一点

写这个教程还有一个目的，就是希望能在过程中加深我对Obsidian插件的理解，帮助自己更好地利用这个软件，因为感觉它的潜力比较大。一起加油吧少年

---

## 🚀 如何使用本教程

### 📋 使用前准备

#### 1. 安装 Obsidian
- 访问 [Obsidian 官网](https://obsidian.md/) 下载并安装最新版本
- 支持 Windows、macOS、Linux、iOS、Android 等多平台
- **推荐版本**：v1.4.0 或更高版本

#### 2. 安装 Git（推荐）
如果您希望使用Git方式下载和同步本教程，需要先安装Git：

**Windows 用户：**
- 访问 [Git官网](https://git-scm.com/download/win) 下载安装包
- 运行安装程序，建议使用默认设置
- 安装完成后可以在命令提示符或Git Bash中使用

**macOS 用户：**
```bash
# 方法1：使用Homebrew（推荐）
brew install git

# 方法2：从官网下载
# 访问 https://git-scm.com/download/mac
```

**Linux 用户：**
```bash
# Ubuntu/Debian
sudo apt update
sudo apt install git

# CentOS/RHEL
sudo yum install git
# 或 sudo dnf install git

# Arch Linux
sudo pacman -S git
```

**验证安装：**
```bash
git --version
```
如果显示版本信息，说明安装成功。

#### 3. 下载本教程 Vault
有两种方式获取本教程：

**方法一：Git Clone（推荐）**
> ⚠️ **前提条件**：需要先完成步骤2的Git安装

```bash
git clone https://github.com/your-username/Obsidian-tutorial.git
```

**Git Clone 的优势：**
- 可以轻松获取最新更新：`git pull`
- 可以参与项目贡献
- 支持版本控制和冲突解决

**方法二：直接下载（简单快速）**
如果您不熟悉Git或只是想快速体验：
- 点击 GitHub 页面右上角的绿色 **Code** 按钮
- 选择 **Download ZIP**
- 解压到您希望存放的位置

> 💡 **建议**：如果您计划长期使用本教程或希望获取最新更新，推荐使用Git Clone方式。

### 注意事项

#### Git 同步冲突解决
在大家看教程并且尝试各种插件的过程中，Git同步时势必会发生各种冲突。如果您使用的是Git Clone方式下载的教程，遇到冲突时可以：

**方法1：通过Obsidian Git插件解决**
1. 按 `Ctrl + P`（Mac: `Cmd + P`）调出命令面板
2. 输入 "git: discard"
3. 在下拉框中选择 "Discard all changes"，丢弃所有更改
4. 按 `Ctrl + M`（Mac: `Cmd + M`），重新进行同步

![](https://img.aiexplorernote.com/obsidian-how-good/git-discrad.jpg)

**方法2：通过命令行解决**
```bash
# 进入项目目录
cd Obsidian-tutorial

# 丢弃所有本地更改
git reset --hard HEAD

# 获取最新更新
git pull
```

**方法3：重新下载**
如果遇到复杂冲突，最简单的方法是删除当前文件夹，重新执行Git Clone。

> 📝 **说明**：教程文件的更新不会影响您个人的笔记内容，只是插件配置和示例文件的更新。

如果有其他问题，可以在项目 [Issues](https://github.com/your-username/Obsidian-tutorial/issues) 中提出。

