# 卸载 Edge 后链接打不开修复

中文 | [English](README.en.md)

测试环境：**Windows 11 25H2**

强制卸载 Microsoft Edge 后，点击网页链接会弹出“你需要使用新应用打开此 https 链接”，链接打不开。原因是卸载过程把 Windows 自带的 `http` / `https` 协议定义也一起删掉了。导入本仓库的注册表文件即可恢复。

> 按手柄 Xbox 键弹出 ms-gamebar 窗口？那是另一个问题，见 [xbox-popup-fix](https://github.com/AINLZE/xbox-popup-fix)。

## 用文件修复

1. 下载 `fix-https-popup.reg`。
2. 双击并在 UAC 提示中确认导入。**需要管理员权限**，因为要写入 `HKEY_LOCAL_MACHINE`。

导入后如果链接仍然打不开，到“设置 › 应用 › 默认应用”里重新选择一次你的浏览器。

## 修复做了什么

- 在 `HKEY_LOCAL_MACHINE\SOFTWARE\Classes` 下重建 `http` 和 `https` 的协议定义。
- 如果当前用户下也有 `http` / `https` 键，它们会覆盖系统定义，所以同样给它们标记 `URL Protocol`。

## 不下载，手动修改

打开 `regedit`（注册表编辑器），以管理员身份运行：

1. 新建 `HKEY_LOCAL_MACHINE\SOFTWARE\Classes\https`，添加一个空的字符串值 `URL Protocol`。
2. 对 `http` 做同样的操作。
3. 如果 `HKEY_CURRENT_USER\Software\Classes\https`（或 `http`）已经存在，也给它添加 `URL Protocol`。

> 本修复会修改注册表，请自行承担风险。
