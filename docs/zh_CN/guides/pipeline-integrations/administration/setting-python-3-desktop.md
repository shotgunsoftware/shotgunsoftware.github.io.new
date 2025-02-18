---
layout: default
title: 为 Desktop 设置 Python 3
pagename: setting-python-3-desktop
lang: zh_CN
---

# 将 {% include product %} Desktop 中的默认 Python 版本设置为 Python 3

{% include info title="警告" content="**本主题仅在使用 ShotGrid Desktop 版本 1.7.3 时有效**，使用较新版本的 ShotGrid Desktop 时不再需要这些步骤。由于安全原因，ShotGrid Desktop 1.8.0 于 2023 年 1 月 26 日发布后，Python 2 随即遭到删除。[单击此处了解更多信息](https://community.shotgridsoftware.com/t/important-notice-upcoming-removal-of-python-2-7-and-3-7-interpreter-in-shotgrid-desktop/15166)。" %}

- [Windows](#windows)
- [MacOS](#macos)
- [CentOS 7](#centos-7)

## Windows

### 在 Windows 上手动将 `SHOTGUN_PYTHON_VERSION` 环境设置为 2

- 在 Windows 任务栏上，右键单击 Windows 图标，然后选择**“系统”**，导航到**“控制面板”/“系统和安全”/“系统”**。 

![](images/setting-python-3-desktop/01-setting-python-3-desktop.png)

- 在此位置，选择**“高级系统设置”**。

![](images/setting-python-3-desktop/02-setting-python-3-desktop.png)

- 接下来，在“系统属性”中选择**“环境变量”**。

![](images/setting-python-3-desktop/03-setting-python-3-desktop.jpg)

- 在**“环境变量”**窗口中，可以通过选择**“新建…”**来添加/编辑路径。 

![](images/setting-python-3-desktop/04-setting-python-3-desktop.jpg)

- 对于**“变量名”**，添加 `SHOTGUN_PYTHON_VERSION`，并将**“变量值”**设置为 `2`。 

![](images/setting-python-3-desktop/05-setting-python-3-desktop.jpg)

- 重新启动 {% include product %} Desktop 应用程序。现在，您应该会看到 Python 版本已更新为运行 Python 2。 

![](images/setting-python-3-desktop/06-setting-python-3-desktop.jpg)


## MacOS

### 在 MacOS 上将 `SHOTGUN_PYTHON_VERSION` 环境设置为 2

- 在 `~/Library/LaunchAgents/` 下创建名为 `my.startup.plist` 的属性文件  

```
$ vi my.startup.plist
```

- 将以下内容添加到 `my.startup.plist` 并**保存**：

```
<?xml version="1.0" encoding="UTF-8"?> 
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "https://www.apple.com/DTDs/PropertyList-1.0.dtd"> 
<plist version="1.0"> 
<dict> 
  <key>Label</key> 
  <string>my.startup</string> 
  <key>ProgramArguments</key> 
  <array> 
    <string>sh</string> 
    <string>-c</string> 
    <string>launchctl setenv SHOTGUN_PYTHON_VERSION 2</string> 
  </array> 
  <key>RunAtLoad</key> 
  <true/> 
</dict> 
</plist>
```

- 重新启动 Mac 后，新环境变量将保持活动状态。

- 重新启动 {% include product %} Desktop 应用程序。现在，您应该会看到 Python 版本已更新为运行 Python 2。 

![](images/setting-python-3-desktop/07-setting-python-3-desktop.jpg)

## CentOS 7

### 在 CentOS 7 上将 `SHOTGUN_PYTHON_VERSION` 环境设置为 2

- 将以下内容添加到 `~/.bashrc` 文件： 

```
export SHOTGUN_PYTHON_VERSION="2"
```

- 通过运行以下命令重新启动操作系统：  

```
$ sudo reboot 
```

- 重新启动 {% include product %} Desktop 应用程序。现在，您应该会看到 Python 版本已更新为运行 Python 2。 

![](images/setting-python-3-desktop/08-setting-python-3-desktop.jpg)
