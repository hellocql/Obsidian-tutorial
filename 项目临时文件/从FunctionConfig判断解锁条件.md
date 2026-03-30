
GetFunctionIsOpen

```CSharp
public static bool GetFunctionIsOpen(E_FunctionConfig limitEnum)
{
	return ConstantData.Instance.IsFunctionOpen(limitEnum) && 
		ConstantData.Instance.GetFunctionUnlockLevel(limitEnum) < DataManager.Player.CurrentLevel 
		&& ConstantData.Instance.IsFunctionOpen(E_FunctionConfig.E_LightLimitSystem);
}
```
