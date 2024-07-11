# windows docker 安装

* 步骤1：启用Hyper-V和容器特性

右键点击Windows徽标，选择“应用和功能”。

点击“程序和功能”。

点击“启用或关闭Windows功能”。

在弹出的窗口中勾选“Hyper-V”和“容器”相关选项（确保包括“容器”和“Hyper-V平台”等），然后点击“确定”。

根据提示重启操作系统。


* 步骤2：下载安装Docker Desktop

访问Docker官网（Docker Desktop | Docker），下载对应Windows版本的Docker Desktop安装包。
双击下载的安装包（通常是Docker Desktop Installer.exe），按照提示完成安装。
注意：在安装过程中，你可以选择是否使用WSL 2作为后端（如果你的系统支持并希望使用WSL 2，可以勾选此选项）。但如果你已经启用了Hyper-V，通常建议直接使用Hyper-V作为后端。
安装完成后，根据提示注销并重新登录Windows，以完成安装过程。
步骤3：运行Docker Desktop并验证安装

安装成功后，Docker Desktop通常会自动启动。如果没有自动启动，你可以手动从开始菜单中启动它。
启动后，你会在桌面右下角看到一个Docker的小鲸鱼图标。
打开PowerShell或命令提示符，运行docker run hello-world命令来验证Docker是否安装成功。如果一切正常，你会看到一条消息，表明Docker已经成功下载并运行了一个简单的容器。


# 启动遇到的问题  running Hyper-V engine: starting Hyper-V VM: status code not OK but 500: Unhandled exception: job failed with message: “DockerDesktopVM”无法启动。(虚拟机 ID A69512D8-CC31-4D81-B45F-1A5DB1C3E6EC)


1、首先需要登录docker

2、
1. 检查Hyper-V状态
首先，确保Hyper-V在Windows上已正确启用并且没有遇到任何配置问题。

打开或关闭Windows功能：
右键点击Windows徽标，选择“应用和功能”。
点击“程序和功能”。
点击“启用或关闭Windows功能”。
确保“Hyper-V”及其所有子功能（如“Hyper-V平台”、“Hyper-V管理工具”等）都已勾选。
点击“确定”并重启计算机。
2. 禁用并重新启用Hyper-V
如果Hyper-V已经启用但Docker Desktop仍然无法启动，尝试禁用并重新启用Hyper-V。

通过命令提示符禁用Hyper-V：
以管理员身份打开命令提示符（CMD）。
输入bcdedit /set hypervisorlaunchtype off并回车。
重启计算机。
重新启用Hyper-V：
再次以管理员身份打开命令提示符。
输入bcdedit /set hypervisorlaunchtype auto并回车。
然后使用dism.exe /Online /Enable-Feature:Microsoft-Hyper-V /All命令来重新启用Hyper-V。
重启计算机。