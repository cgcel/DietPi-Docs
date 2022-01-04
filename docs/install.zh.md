---
description: 安装 & 初始化 DietPi 的简易教程
title: 如何安装 DietPi
---

# 如何安装 DietPi

DietPi 的安装包括几个步骤：

- 提供安装介质（如适用于单板计算机的SD卡或PC的U盘）
- 获取 DietPi 镜像文件（并将其安装在安装介质上）
- 启动 DietPi 设备并完成初始化配置

按照这些步骤，您将能够使用 [`dietpi-software`](../dietpi_tools/#dietpi-software) 初步设置 DietPi 并安装您想要使用的其他软件包。

请点击以下标签获取您的设备的安装说明。

=== "Raspberry Pi and derivatives (SBC)"

    ## 介绍

    得益于众所周知的基于ARM架构的Raspberry PI的SBC在过去几年中获得了越来越多的朋友。低成本与功率和硬件的灵活性相结合，使这些SBC成为嵌入式系统的最佳选择，例如家庭自动化或云应用。
    
    ![Raspberry Pi 1 Model B photo](assets/images/raspberry-pi-1b.jpg){: width="400" height="200" loading="lazy"}

    ## 硬件准备

    要学习本教程，您需要以下的硬件清单。
    
    - 一个Raspberry Pi、Odroid或其他SBC - 具体请查询[所有支持的SBC列表](.../hardware/)
    - 一张至少4GB的SD卡，并通过您的电脑写入（集成插槽或外部SD卡读卡器）。
    - 可选项：以太网（网络）电缆

    _注意_：按照本指南，您可以直接（从控制台）或通过网络运行安装。如果您选择通过网络安装，您将不需要显示器或键盘连接到您的SBC或虚拟环境。
    
    ## 1. 下载并提取 DietPi 磁盘镜像

    打开[`dietpi.com`](https://dietpi.com/#download)并选择 "Download"。所有支持的设备将在页面中显示。选择您的SBC并点击**Download**。磁盘镜像将被下载到本地。

    _例子：_
    ![DietPi for Raspberry Pi download page](assets/images/DietPi-RaspberryPi-image.jpg){: width="1186" height="561" loading="lazy"}

    **将下载的文件解压缩到本地文件夹中。**

    它是一种_7z_档案格式，所以您需要安装[7zip for Windows](https://www.7-zip.org/)或[The Unarchiver (Macintosh)](https://wakaba.c3.cx/s/apps/unarchiver.html)。两者都是免费的，并且经过测试可以正确地解压缩镜像文件。

    Linux用户需要下载并安装`p7zip`（终端版本的`7zip`）。

    ??? hint "如何在Linux系统中提取 DietPi 镜像文件"
        在基于Debian或Ubuntu的系统中，在命令行中输入：

        ```sh
        sudo apt install p7zip
        ```

        当p7zip安装完毕，在命令行中输入以下指令提取文件：

        ```sh
        7zr e DietPi-Image.7z
        ```

        将**DietPi-Image.7z**重命名为所下载文件的正确名称，e.g. **DietPi_RPi-ARMv6-Bullseye.7z**。这将提取DietPi的镜像文件供您使用。

    ## 2. 刷写 DietPi 镜像

    首先，下载并安装 [balenaEtcher](https://etcher.io/)。此应用程序可以在Windows、macOS、Linux上安全、轻松地将操作系统镜像文件刷入SD卡和U盘。  

    !!! note "在Windows系统中您亦可使用 [Rufus](https://rufus.ie/) 来刷写镜像文件。"
        点击上方的**在本机上安装**标签，内含使用Rufus的例子。如果是刷写SBC镜像，所有选项都是灰色的，这是正常现象，所以在选择镜像和目标驱动器后，您只需要点击START。

    启动balenaEtcher，确保你的U盘或SD卡插入你的电脑。找到并选择DietPi镜像。

    ![DietPi-Etcher-install-01](assets/images/DietPi-Etcher-install-01.jpg){: width="795" height="529" loading="lazy"}

    下一步，确保所选设备是正确的。

    !!! warning "设备的所有数据将被擦除！"
        刷写过程将擦除硬盘数据，所以如果你选择了设备，你可能有丢失数据的风险。

    ![DietPi-Etcher-install-02](assets/images/DietPi-Etcher-install-02.jpg){: width="796" height="478" loading="lazy"}

    确认所有的步骤都正确后，点击继续，即可开始写入SD卡。这个过程可能需要一些时间。

    ![DietPi-Etcher-install-03](assets/images/DietPi-Etcher-install-03.jpg){: width="796" height="478" loading="lazy"}

    ??? info "如果你想使用WiFi连接，请点击这里"
        如要设置WiFi，先打开SD卡文件夹，用文本编辑器更新下面两个文件。

        1.  打开名为`dietpi.txt`的文件。找到`AUTO_SETUP_NET_WIFI_ENABLED`并设置为数值1。
        2.  打开`dietpi-wifi.txt`文件，将`aWIFI_SSID[0]`设为你的WiFi网络名称。
        3. 在同一文件`dietpi-wifi.txt`中，将`aWIFI_KEY[0]`设置为您的WiFi网络密码。
        4. 保存并关闭这些文件

    ## 3. 准备第一次开机

    从PC上取下U盘或SD卡，并将其插入你的SBC设备，准备首次启动。 
    打开SBC的电源，登录并执行第一次启动程序。  

    ??? info "可选项：在第一次启动时自动进行基础安装（运行一次 _静默安装_ ）。"

        DietPi提供自动的首次启动安装的选项。细节请参见章节 ["How to do an automatic base installation at first boot"](../usage/#how-to-do-an-automatic-base-installation-at-first-boot)

    ???+ hint "初始启动时间"
        由于自动调整root文件系统的大小和基本的设置步骤，这个初始启动比进一步的系统启动序列需要更长的时间。它可能会持续几分钟，这取决于系统驱动器和硬件的情况。

=== "VirtualBox"

    <font size="+2">介绍</font>

    虚拟机镜像对于快速安装DietPi系统并进行测试的场合是非常好的。它也可以作为一个基于Debian的Linux系统，用于开发目的，例如使用X11窗口系统。占用空间小使得它可以小内存的PC上使用。同时，也可以为不同的应用程序运行几个虚拟机。

    这样的虚拟机的一大优势是它只需要几分钟就能运行DietPi系统。

    安装虚拟机的选择之一是 [__Oracle VirtualBox__](https://www.oracle.com/virtualization/virtualbox/).

    ![DietPi-VirtualBox-program](assets/images/dietpi-VirtualBox-program.png){: width="1593" height="814" loading="lazy"}

    <font size="+2">硬件准备</font>

    开始前，你需要一台 **运行VirtualBox软件的PC**，DietPi系统将在上面运行。 
    在这台PC上需要有以下硬盘空间： 

    - 1.2GiB用于运行最小运行系统  
    - 5 - 10 GiB用于运行X11的典型系统  

    建议至少有10GiB的可用空间。

    ??? important "安装带有VirtualBox扩展包的VirtualBox（"用户添加"）。"
        如果你打算安装VirtualBox扩展包，通常需要考虑以下方面以实现时间同步：

        - VirtualBox扩展包包含一个自己的时间同步功能，它可以使虚拟机系统时间与主机系统时间保持同步。
          因此，`dietpi-config` 中的时间同步模式应切换为 **Custom**，以避免启动过程中的冲突或超时。
        - 没有扩展包的VirtualBox需要一个网络时间同步解决方案，例如 `dietpi-config` 中的一个可配置的时间同步模式（它基于`systemd-timesyncd`）。

        所需的额外安装步骤（使用扩展包）在这里（在主机系统上的安装步骤）和下面（在DietPi用户系统内的安装步骤）描述。 
        在主机系统上的安装包括基本的VirtualBox安装和扩展包的安装。在基于Linux的主机系统的情况下，描述了VirtualBox主机的安装（该描述假设有root用户，否则最好添加 `sudo`）。

        1. 在Linux主机系统上安装VirtualBox  
           以下是手动安装的描述（你需要根据实际的VirtualBox版本来改变个别参数）。

             ```sh
             mkdir ~/Downloads
             cd ~/Downloads
             wget https://download.virtualbox.org/virtualbox/6.1.30/virtualbox-6.1_6.1.30-148432~Debian~bullseye_amd64.deb
             apt install ./virtualbox-6.1_6.1.30-148432~Debian~bullseye_amd64.deb
             ```

        2. 在Linux主机系统上安装VirtualBox扩展包  
           以下是手动安装的描述（你需要根据实际的VirtualBox版本来改变个别参数）。

             ```sh
             cd ~/Downloads
             wget https://download.virtualbox.org/virtualbox/6.1.18/Oracle_VM_VirtualBox_Extension_Pack-6.1.18.vbox-extpack
             VBoxManage extpack install Oracle_VM_VirtualBox_Extension_Pack-6.1.18.vbox-extpack
             ```

        完成这两个步骤之后，VirtualBox扩展包的主机安装就完成了。下面介绍在guest系统上的进一步安装步骤。

    <font size="+2">1. 下载并解压DietPi磁盘镜像</font>

    从 [`dietpi.com`](https://dietpi.com/#download) 下载 **DietPi VirtualBox** 镜像并将文件解压至本地文件夹中。它是一种_7z_档案格式，所以你需要安装[7zip for Windows](https://www.7-zip.org/)或其他替代工具。

    ![DietPi-VirtualBox-download-image](assets/images/dietpi-VirtualBox-Download.png){: width="1152" height="733" loading="lazy"}

    该压缩文件包含几个文件，其中重要的是必须导入VirtualBox的.ova文件。

    ![DietPi VirtualBox 7zip archive content](assets/images/dietpi-VirtualBox-7zip-file.png){: width="533" height="83" loading="lazy"}

    <font size="+2">2. 在VirtualBox中导入.ova文件</font>

    接下来，VirtualBox虚拟机必须通过导入.ova文件（通过\File\Import Appliance）进行设置。

    ![VirtualBox appliance import screenshot](assets/images/dietpi-VirtualBox-import1.png){: width="483" height="308" loading="lazy"}

    在下面的对话框中，用户必须选择要导入的".ova "文件。

    ![VirtualBox appliance import selection screenshot](assets/images/dietpi-VirtualBox-import2.png){: width="971" height="775" loading="lazy"}

    在下一个对话框中保持设置并点击 "Import"。

    导入完成后，DietPi VirtualBox虚拟机就创建好了。

    ![VirtualBox virtual machine list screenshot](assets/images/dietpi-VirtualBox-VB-Machine.png){: width="245" height="55" loading="lazy"}

    <font size="+2">3. 新VirtualBox镜像的初启动</font>

    按下启动按钮（绿色箭头），根据DietPi镜像“启动”你的系统。

    ??? attention "当主机使用WiFi时，你必须禁用IPv6"
        有时，虚拟机难以连接到互联网。在网络桥接模式下以及主机通过 WiFi 连接到互联网时，会报告这种情况：在这些情况下，虚拟机和互联网之间的 IPv6 路由失败（例如，见 [there](https://communities.vmware.com/t5/VMware-Fusion-Discussions/IPv6-Bridged-Wireless/td-p/2038235)）。 
        一个例子是，系统没有找到更新服务器（例如，在第一次更新运行时）。在第一次启动时的 "apt update "程序中会提示。 
        为解决这个问题，可打开一个子shell（或一个额外的ssh窗口），启动 `dietpi-config` 并在网络选项中禁用**IPv6**。

        ![IPv6 deactivate screenshot](assets/images/dietpi-VirtualBox-IPv6.png){: width="500" height="225" loading="lazy"}

        然后退出 `dietpi-config`。在这之后，第一次安装程序应该从头开始运行。

    ??? important "使用VirtualBox扩展包时在DietPi客户系统中的安装步骤"
        如果你使用VirtualBox扩展包，在DietPi基础安装后（在DietPi系统首次启动时完成），必须在DietPi客户系统内完成进一步的安装步骤以实现工作时间同步。一般来说，你必须使用以下 **Time sync mode** 选项，通过 `dietpi-config` 命令（在 **Advanced Options** 中）设置。

        - 没有扩展包的VirtualBox。时间同步必须使用选项1...4（"Boot only", "Boot + Daily", "Boot + Hourly", "Daemon + Drift"）。不需要进一步的安装步骤。
        - 带有扩展包的VirtualBox。时间同步必须使用选项0（"Custom"）。需要进一步的安装步骤，见下文。

            ![DietPi-config time synchronization](assets/images/dietpi-config-timesync.png){: width="600" height="328" loading="lazy"}

        在使用扩展包的情况下的额外安装步骤（描述中假设有一个root用户，否则添加 `sudo` 合适）。

        1. 检查是否存在带有VirtualBox扩展名（`.iso`）的光盘：

            ```sh
            lsblk
            ```

            如果你没有看到 `/dev/sr0` 光驱，你需要在虚拟机设置中（在虚拟机的关闭状态下） `/Machine->Settings->Storage` 中添加：添加一个链接到Guest添加的光存储（`.iso`）。

        2. 安装内核头文件和扩展包：

            ```sh
            apt -y install build-essential dkms linux-headers-amd64
            mkdir /root/mnt
            mount /dev/sr0 /root/mnt
            cd /root/mnt
            ./VBoxLinuxAdditions.run
            ```

            如果你看到一个错误信息 ***"VirtualBox Guest Additions: Kernel headers not found for target kernel"***，那么内核头文件就没有正确安装（执行 `apt -y install linux-headers-amd64`，然后再次尝试 `./VBoxLinuxAdditions.run`）。

        3. 重新启动并检查服务  
           用以下方法检查正在运行的VirtualBox扩展包服务：

             ```sh
             systemctl status vboxadd-service
             ```

             `vboxadd-service` 应该处于 *active* 状态。

        4. 在主机系统中的设置  
            为了确保guest虚拟机在启动时和从保存状态恢复时与主机同步时间，请在 **host system** （不是DietPi客户系统）上运行以下三个命令。

            ```sh
            VBoxManage guestproperty set "<vm_name>" --timesync-set-start
            VBoxManage guestproperty set "<vm_name>" --timesync-set-on-restore 1
            VBoxManage guestproperty set "<vm_name>" "/VirtualBox/GuestAdd/VBoxService/--timesync-set-threshold" 10000
            ```

            将 `<vm_name>` 替换为虚拟机VirtualBox Manager用户界面中显示的虚拟机名称，例如：如果你导入虚拟机时没有改变其名称则用 `DietPi_VirtualBox-x86_64-Bullseye`，。

        通过所有这些设置步骤，使用扩展包的时间同步应该可以工作。有时需要几分钟才能实现时间同步，所以要有一定的耐心。

=== "VMware"

    <font size="+2">介绍</font>

    Virtual machine images are great for those occasions where you want to set up a DietPi system very quickly and test things. Also it may be used as a Debian based Linux system with a small footprint for development purposes, e.g. with the X11 window system. The small footprint makes it optimally usable on PCs without a huge built in RAM. Also several VMs may be run for different applications.

    One big advantage of such a VM is that it needs only a couple of minutes coming to a running DietPi system.

    One of the options of a virtual machine is [__VMware Workstation Player__](https://www.vmware.com/de/products/workstation-player/workstation-player-evaluation.html) resp. [__VMware Fusion__](https://www.vmware.com/de/products/fusion/fusion-evaluation.html) (macOS).

    ![DietPi-VMware-program](assets/images/dietpi-VMware-program.png){: width="769" height="588" loading="lazy"}

    !!! info "Tested with Windows 10"
        This description relates to VMware Workstation 16 Player on a Microsoft Windows system.  
        ***VMware Workstation Pro*** as well as ***VMware Fusion for MAC*** were not tested but should work also.

    <font size="+2">硬件准备</font>

    As a starting point you need a **PC with a running VMware Workstation Player software** on which the DietPi system will run.

    On this PC a free harddisk space of about  

    - 3 GiB for a minimal running system (1.5 GiB in switched off state)
    - 5 - 10 GiB for a typical running system with X11  

    is needed. A recommended size is at least a free space of 10 GiB.

    <font size="+2">1. 下载并解压DietPi磁盘镜像</font>

    Download the **DietPi VMware** image from [`dietpi.com`](https://dietpi.com/#download) and unzip the downloaded file to a local folder. It is a _7z_ archive format so you will need to install either [7zip for Windows](https://www.7-zip.org/) or other alternative tools.

    ![DietPi VMware download image](assets/images/dietpi-VMware-Download.png){: width="1223" height="749" loading="lazy"}

    The zip file contains a couple of files, the important two are the `.vmx` and `.vmdk` file which have to be copied to a VMware machine folder (The folder can be located anywhere on the PCs harddisk).

    ![DietPi VMware 7zip archive content](assets/images/dietpi-VMware-7zip-file.png){: width="525" height="104" loading="lazy"}

    <font size="+2">2. 在VMware中添加文件</font>

    As next, the VMware virtual machine is setup by just opening the `.vmx` file (via ***Open a Virtual Machine***):

    ![VMware file open screenshot](assets/images/dietpi-VMware-import1.png){: width="715" height="585" loading="lazy"}

    In the following dialog the user has to navigate to the directory where the `.vmx` and `.vmdk` file were stored. Choose the `.vmx` file to open.  
    After this the DietPi VMware virtual machine is present and can be started:

    ![VMware virtual machine list screenshot](assets/images/dietpi-VMware-VM-Machine.png){: width="714" height="588" loading="lazy"}

    <font size="+2">3. VMware镜像初启动</font>

    Press the ***Play virtual machine*** (green arrow) to 'boot up' your system based on the DietPi image. Possibly you have to acknowledge in an appearing dialog "I Copied it" and go on.
    If you want to use a WiFi connection you have to change the network settings matching your environment (files `\boot\dietpi.txt` and `\boot\dietpi-wifi.txt`).

    ??? attention "You must disable IPv6 when the host uses WiFi"
        Sometimes the VM has difficulties to connect to the internet. This is reported in a network bridged mode and when the host connects to the internet via WiFi: In these cases the IPv6 routing between the VM and the internet fails (e.g. see [there](https://communities.vmware.com/t5/VMware-Fusion-Discussions/IPv6-Bridged-Wireless/td-p/2038235)).  
        A typical result is, that the system does not find the update server (e.g. at the very first update run). This is then signaled during the "apt update" procedure of the first boot startup.  
        To overcome this, open a subshell (or an additional ssh window), start `dietpi-config` and disable **IPv6** within the Network options.

        ![IPv6 deactivate screenshot](assets/images/dietpi-VirtualBox-IPv6.png){: width="500" height="225" loading="lazy"}

        Then exit `dietpi-config`. After this the first time installer procedure should run again from the start.

    <font size="+2">补充信息</font>

    For information about running DietPi in an VMware ESXi environment, you can read this article: [Running the DietPi VMware image on ESXi 6.7](https://ccie.tv/running-dietpi-vmware-image-on-esxi-6-7).

=== "Parallels (macOS)"

    <font size="+2">介绍</font>

    Virtual machine images are great for those occasions where you want to set up a DietPi system very quickly and test things. Also it may be used as a Debian based Linux system with a small footprint for development purposes, e.g. with the X11 window system. The small footprint makes it optimally usable on PCs without a huge built in RAM. Also several VMs may be run for different applications.

    One big advantage of such a VM is that it needs only a couple of minutes coming to a running DietPi system.

    One of the options of a virtual machine is [__Parallels Desktop__](https://www.parallels.com/products/desktop/) for macOS.

    ![Parallels Desktop DietPi machine](assets/images/dietpi-Parallels10.png){: width="720" height="405" loading="lazy"}

    <font size="+2">硬件准备</font>

    As a starting point you need an **Apple Mac with a running Parallels Desktop software** on which the DietPi system will run (x86 system, e.g. Mac mini 2011/2012/2014/2018).  
    On this MAC a free harddisk space of about  

    - 1.2 GiB for a minimal running system  
    - 5 - 10 GiB for a typical running system with X11  

    is needed. A recommended size is at least a free space of 10 GiB.

    <font size="+2">1. 下载并解压DietPi磁盘镜像</font>

    Download the **BIOS installer** image from [`dietpi.com`](https://dietpi.com/#download).

    ![DietPi download BIOS installer image](assets/images/dietpi-download-nativepc-bios.jpg){: width="722" height="218" loading="lazy"}

    Klick on the downloaded file to extract it. Move the contained `.iso` file e.g. on your desktop.

    ![DietPi ISO image on MAC desktop](assets/images/dietpi-Parallels00.png){: width="120" height="123" loading="lazy"}

    <font size="+2">2. 在 Parallels Desktop 中创建虚拟机</font>

    As next, the Parallels virtual machine has to be created using the `.iso` file:

    ![Parallels Desktop VM creation screenshot](assets/images/dietpi-Parallels01.png){: width="620" height="417" loading="lazy"}

    In the following dialog the user has to choose the `.iso` file as the installation image which shall be used.

    ![Parallels Desktop ISO file selection screenshot](assets/images/dietpi-Parallels02.png){: width="400" height="197" loading="lazy"}

    Set the machine name in the next dialog and klick “Create”.

    ![Parallels Desktop VM name screenshot](assets/images/dietpi-Parallels03.png){: width="620" height="417" loading="lazy"}

    After the creation has finished the DietPi Parallels Desktop virtual machine starts automatically.

    <font size="+2">3. Parallels Desktop新镜像的初启动</font>

    After booting the graphics selection dialog appears:

    ![Parallels Desktop Clonezilla main menu screenshot](assets/images/dietpi-Parallels04.png){: width="500" height="404" loading="lazy"}

    You can select the default settings. In case of problems, please select "Safe graphic settings".

    Once this step is completed, the installation process begins with the help of the wonderful Clonezilla tool.

    Select the harddisk of your virtual machine where your DietPi shall be installed. Normally, there is only one harddisk present.
    After this, the installation process starts with several steps, e.g. showing the process of the image copying:

    ![Clonezilla processing screenshot](assets/images/dietpi-boot-partclone.jpg){: width="500" height="350" loading="lazy"}

    These steps take some time, be patient! Otherwise buy an SSD. :-)  
    At the end the system executes a shutdown.

    For the first boot up of your Parallels Desktop virtual machine start the virtual machine to login and execute the first boot procedure:

    ![Parallels Desktop start virtual machine screenshot](assets/images/dietpi-Parallels06.png){: width="500" height="368" loading="lazy"}

    ??? note "Temperature value not shown correctly within the Parallels Desktop DietPi virtual machine"
        The temperature value shown in the login dialog or given by the command `cpu` or `G_OBTAIN_CPU_TEMP` is not valid. You have to ignore the shown warning.

        ![Parallels Desktop dialog after login screenshot](assets/images/dietpi-Parallels09.png){: width="693" height="347" loading="lazy"}

    ??? note "Network settings in case of networking problems"
        The settings of the network may lead to a failure of network access. This can e.g. be determined via a network timeout message (e.g. the given message `curl: (28) Resolving timed out after 3005 milliseconds`).

        ![Parallels Desktop dialog after login screenshot](assets/images/dietpi-Parallels09.png){: width="693" height="347" loading="lazy"}

        In this case open the network configuration from the machine's "Configuration" dialog:

        ![Parallels Desktop network configuration screenshot](assets/images/dietpi-Parallels20.png){: width="693" height="521" loading="lazy"}

        In the "Advanced" selection open the network preferences:

        ![Parallels Desktop network preferences screenshot](assets/images/dietpi-Parallels21.png){: width="420" height="243" loading="lazy"}

        Disable the DHCP:

        ![Parallels Desktop uncheck DHCP screenshot](assets/images/dietpi-Parallels22.png){: width="550" height="519" loading="lazy"}

        Then, go back to your virtual machine. The network connection should then run fine.

=== "Hyper-V"

    <font size="+2">介绍</font>

    Virtual machine images are great for those occasions where you want to set up a DietPi system very quickly and test things. Also it may be used as a Debian based Linux system with a small footprint for development purposes, e.g. with the X11 window system. The small footprint makes it optimally usable on PCs without a huge built in RAM. Also several VMs may be run for different applications.

    One big advantage of such a VM is that it needs only a couple of minutes coming to a running DietPi system.

    One of the options of a virtual machine is [__Microsoft Hyper-V__](https://docs.microsoft.com/en-us/windows-server/virtualization/hyper-v/hyper-v-technology-overview).

    ![Hyper-V-Manager screenshot](assets/images/dietpi-HyperV-program.png){: width="722" height="450" loading="lazy"}

    !!! info "Tested with Windows 10"
        This description relates to Hyper-V on a Microsoft Windows system.

    <font size="+2">硬件准备</font>

    As a starting point you need a **PC with a activated Hyper-V** on which the DietPi system will run.

    ??? info "Hyper-V activation within Windows"
        Hyper-V needs to be activated within Windows (e.g. [see there](https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)). The activation is done by enabling all Hyper-V features in the ***Turn Windows features on or off*** within the ***Apps and Features*** area in the Windows settings.

        ![Hyper-V activation](assets/images/dietpi-HyperV-activation.png){: width="367" height="328" loading="lazy"}

    On this PC a free harddisk space of about  

    - 3 GiB for a minimal running system (1.5 GiB in switched off state)
    - 8 - 10 GiB for a typical running system with X11  

    is needed. A recommended size is at least a free space of 10 GiB.

    <font size="+2">1. Download and extract the DietPi disk image</font>

    Download the **DietPi Hyper-V** image from [`dietpi.com`](https://dietpi.com/#download) and unzip the downloaded file to a local folder. It is a _7z_ archive format so you will need to install either [7zip for Windows](https://www.7-zip.org/) or other alternative tools.

    ![DietPi Hyper-V image download](assets/images/dietpi-HyperV-Download.jpg){: width="722" height="463" loading="lazy"}

    The archive contains the DietPi `README.md`, the `.vhdx` virtual disk image and a `hash.txt`, which contains hashes to check the integrity of the virtual disk image. Move the `.vhdx` file to the desired virtual machine folder on your harddisk.

    <font size="+2">2. 添加一个Hyper-V虚拟机</font>

    Next, a Hyper-V machine needs to be created. Start the Hyper-V-Manager, right click on your PCs node in the left tree and open the dialog wizard for the machine generation ("New" -> "Virtual Machine"):

    ![Hyper-V machine generation](assets/images/dietpi-HyperV-VM-generation.png){: width="450" height="364" loading="lazy"}

    In the following wizard you have to set the following:

    1. Give your machine a name ("Specify Name and Location")
    2. Select the Hyper-V Generation: Select **Generation 1** ("Specify Generation")
    3. Choose your RAM size (e.g. 2048 MB)
    4. If you have already configured a network, select your network. Otherwise let it "Not connected" and change it afterwards
    5. Choose to use the extracted `.vhdx` Hyper-V disc file (see above)

    If you have not set up any network connection, go on with the **Virtual Switch Manager** and add a network. Select that network in your virtual machine settings afterwards.  

    ![Hyper-V network management](assets/images/dietpi-HyperV-manage-network.png){: width="250" height="284" loading="lazy"}

    <font size="+2">3. Hyper-V新机器的初启动</font>

    First, click on ***Connect*** to open a window of the virtual machine:

    ![Hyper-V machine connection](assets/images/dietpi-HyperV-connect-machine.png){: width="450" height="205" loading="lazy"}

    Then press ***Start*** to boot up the machine:

    ![Hyper-V machine start](assets/images/dietpi-HyperV-start-machine.png){: width="550" height="420" loading="lazy"}

    After this, your machine should boot up.

    ??? attention "You must disable IPv6 when the host uses WiFi"
        Sometimes the VM has difficulties to connect to the internet. This is reported in a network bridged mode and when the host connects to the internet via WiFi: In these cases the IPv6 routing between the VM and the internet fails (e.g. see [there](https://communities.vmware.com/t5/VMware-Fusion-Discussions/IPv6-Bridged-Wireless/td-p/2038235)).  
        A typical result is, that the system does not find the update server (e.g. at the very first update run). This is then signaled during the "apt update" procedure of the first boot startup.  
        To overcome this, open a subshell (or an additional ssh window), start `dietpi-config` and disable **IPv6** within the Network options.

        ![IPv6 deactivate screenshot](assets/images/dietpi-VirtualBox-IPv6.png){: width="500" height="225" loading="lazy"}

        Then exit `dietpi-config`. After this the first time installer procedure should run again from the start.

    <font size="+2">其他信息/故障排除</font>

    <font size="+1">**Network connection not found**</font>  
    In the case that you did not setup your network configuration properly, the booting procedure will not find a network connection and may respond with this boot console output:

    ![Hyper-V boot without network](assets/images/dietpi-HyperV-boot-wo-network.jpg){: width="722" height="164" loading="lazy"}

    Then you have to check and repair your network configuration within the **Virtual Switch Manager**.

    <font size="+1">**生成一个Hyper-V第二代机器**</font>  
    An option to get a Hyper-V Generation 2 machine is to generate your own Hyper-V image via a **Debian network installation** (booting the Hyper-V machine from a Debian `netinst.iso` installer like you would do it on a PC). Install a minimal Debian machine (i.e. no X11 desktops, etc.). Afterwards run the procedure described in section ["Make your own distribution"](../hardware/#make-your-own-distribution). Generation 2 machines support (and require) to boot in UEFI mode, support [Secure Boot](https://en.wikipedia.org/wiki/Unified_Extensible_Firmware_Interface#Secure_Boot), [TPM](https://en.wikipedia.org/wiki/Trusted_Platform_Module), use modern SCSI controllers and have higher hardware limits. For use as a home server, however, you will not need any of these functions.

=== "Native PC"

    <font size="+2">介绍</font>

    The Native PC images are great for those occasions where SBC performance is just not enough. One example could be [Intel NUC Kit](https://www.intel.com/content/www/us/en/products/boards-kits/nuc/kits.html?page=2). It is a small, versatile, upgradable, and affordable desktop PC with the same basic feature set as that of a much larger machine.

    ![DietPi-Intel-NUC](assets/images/dietpi-nuc8.jpg){: width="300" height="200" loading="lazy"}

    It could be also a great way to make use of an old computer that’s not capable of running the latest version of Windows or macOS.

    !!! question "**UEFI** or **BIOS**?"
        First, you have to find out whether your PC contains **UEFI** ([Unified Extensible Firmware Interface](https://wikipedia.org/wiki/Unified_Extensible_Firmware_Interface)) or **BIOS** ([Basic Input/Output System](https://wikipedia.org/wiki/BIOS)):

        - In case of an UEFI based PC see the "**UEFI Installer image**" tab.
        - In case of a BIOS based PC see the "**BIOS Installer image**" tab or "**BIOS direct write image**" tab.

    !!! question ""**BIOS Installer image**" or "**BIOS direct write image**"?"
        The "**BIOS installer image**" is used to boot from and install the DietPi system on a different target boot drive (storage medium). In contrary to that the "**BIOS direct write image**" is used to be write the image directly to the target DietPi boot drive.

    === "UEFI installer image"

        <font size="+2">硬件准备</font>

        You would need the next:

        - one **working PC with internet access**, helping to write the boot media
        - one **bootable USB drive** (e.g. flash disk, at least 2 GiB), to hold the DietPi installer image and to boot the target PC
        - **target PC** to be installed

        <font size="+2">1. 下载并解压DietPi磁盘镜像</font>

        Download the **Native PC for UEFI** > **Installer Image** from [`dietpi.com`](https://dietpi.com/#download) and
        extract the downloaded file to a local folder. It is a _7z_ archive format so you will need to install either [7zip for Windows](https://www.7-zip.org/) or other alternative tools.

        ![DietPi download UEFI installer image](assets/images/dietpi-download-nativepc-uefi.jpg){: width="722" height="211" loading="lazy"}

        Download [Rufus](https://rufus.ie/) and run the application. There is a portable version of Rufus available which doesn't require any local installation.

        !!! warning "Be careful if you run alternative applications!"
            While [Balena Etcher](https://www.balena.io/etcher/) is recommended for installing DietPi on SBCs, it does not provide good results for UEFI images. The same also with win32diskimager, which does not work as an alternative.

        <font size="+2">2. 写入镜像至USB驱动</font>

        Start [Rufus](https://rufus.ie/) application and make sure you have your USB drive inserted into your computer. Follow the next steps:

        1. Select the USB device
        2. Select the downloaded **DietPi** image
        3. Select **GPT** as partition scheme
        4. Select **UEFI** as target system
        5. Click on **Start** button

        Ensure that the selected USB medium is the correct one.

        !!! warning "All data on the USB medium and later on the target PCs harddisk will be erased!"
            Before starting the installation first make a backup of the data available on the target PC and USB drive if you need it later again!

        ![Rufus UEFI installer image selections screenshot](assets/images/dietpi-rufus-uefi-installer.png){: width="473" height="579" loading="lazy"}

        <font size="+2">3. 启动目标电脑并在本地磁盘上安装镜像</font>

        Boot the **target PC** from the USB image and install the image on the local disk / harddisk. Put the USB stick into the target PC and boot from this USB stick.  

        !!! note "BIOS settings"
            It may be necessary to change BIOS settings to enable the UEFI boot. This action is not described here.

        During the initial boot, the following dialog may appear to boot from the USB stick:

        ![Bootloader menu screenshot](assets/images/dietpi-uefi-boot.jpg){: width="483" height="230" loading="lazy"}

        After booting the graphics selection dialog appears:

        ![Clonezilla main menu screenshot](assets/images/dietpi-uefi-boot-graphic.jpg){: width="834" height="394" loading="lazy"}

        You can select the default settings. In case of problems, please select "Safe graphic settings".

        Once this step is completed, you will able to select a different keyboard. If necessary, change your keyboard settings and go through the appropriate dialogues.

        Then the installation process begins with the help of the wonderful Clonezilla tool.

        Select the image file to be installed on the target PCs harddisk. Normally you should only see one single option:

        ![Clonezilla source image selection screenshot](assets/images/dietpi-boot-clonezilla.jpg){: width="656" height="198" loading="lazy"}

        After this, you have to select the target PCs harddisk where your DietPi shall be installed. In this example there is only one harddisk present:

        ![Clonezilla target drive selection screenshot](assets/images/dietpi-boot-clonezilla-run.jpg){: width="853" height="181" loading="lazy"}

        After this, the installation process starts with several steps, e.g. showing the process of the image copying:

        ![Clonezilla processing screenshot](assets/images/dietpi-boot-partclone.jpg){: width="500" height="350" loading="lazy"}

        These steps take some time, be patient! Otherwise buy an SSD. :-)  
        At the end the system executes a shutdown.

        ??? info "Click here if you want to use a WiFi connection"
            To setup the WiFi, you have to change the network settings matching to your environment:

            1.  Open the file `dietpi-wifi.txt` and set `aWIFI_SSID[0]` to the name of your WiFi network.
            2.  In the same file `dietpi-wifi.txt`, set `aWIFI_KEY[0]` to the password of your WiFi network.
            3.  Save and close the files

            You need to set these values before you boot up the PC for the first time (initial boot).

        For the first boot up of your PC disconnect your USB stick from the target PC and power on the PC to login and execute the first boot procedure.

    === "BIOS installer image"

        <font size="+2">硬件准备</font>

        You would need the next:

        - one **working PC with internet access**, helping to write the boot media
        - one **bootable USB drive** (e.g. flash disk, at least 2 GiB), to hold the DietPi installer image and to boot the target PC
        - **target PC** to be installed

        Remark: If your PC is not able to boot from a USB drive you can do a similar installation by burning the installer image onto a DVD and boot from the DVD. The same installation procedure will take place. Do not forget to eject your DVD before the installed DietPi shall boot from the hard disc for the first time.

        <font size="+2">1. 下载并解压DietPi安装程序镜像</font>

        Download the **Native PC for BIOS/CSM** > **Installer Image** from [`dietpi.com`](https://dietpi.com/#download) and
        extract the downloaded file to a local folder. It is a _7z_ archive format so you will need to install either [7zip for Windows](https://www.7-zip.org/) or other alternative tools.

        ![DietPi download BIOS installer image](assets/images/dietpi-download-nativepc-bios.jpg){: width="722" height="218" loading="lazy"}

        Download [Rufus](https://rufus.ie/) and run the application. There is a portable version of Rufus available which doesn't require any local installation.

        <font size="+2">2. 写入镜像至USB驱动</font>

        Start [Rufus](https://rufus.ie/) application and make sure you have your USB drive inserted into your computer. Follow the next steps:

        1. Select the USB device
        2. Select the downloaded **DietPi** image
        3. Select **MBR** as partition scheme and **BIOS or UEFI** as target system
        4. Click on **Start** button

        Ensure that the selected USB medium is the correct one.

        !!! warning "All data on the USB medium and later on the target PCs harddisk will be erased!"
            Before starting the installation first make a backup of the data available on the target PC and USB drive if you need it later again!

        ![Rufus BIOS installer image selections screenshot](assets/images/dietpi-rufus-bios-installer.png){: width="474" height="580" loading="lazy"}

        <font size="+2">3. 启动目标电脑并在本地磁盘上安装镜像</font>

        Boot the **target PC** from the USB image and install the image on the local disk / harddisk. Put the USB stick into the target PC and boot from this USB stick.  

        !!! note "BIOS settings"
            It may be necessary to change BIOS settings to enable the boot from the USB stick. This action is not described here.

        After booting the graphics selection dialog appears:

        ![Clonezilla main menu screenshot](assets/images/dietpi-uefi-boot-graphic.jpg){: width="834" height="394" loading="lazy"}

        You can select the default settings. In case of problems, please select "Safe graphic settings".

        Once this step is completed, you will able to select a different keyboard. If necessary, change your keyboard settings and go through the appropriate dialogues.

        Then the installation process begins with the help of the wonderful Clonezilla tool.

        Select the image file to be installed on the target PCs harddisk. Normally you should only see one single option:

        ![Clonezilla source image selection screenshot](assets/images/dietpi-boot-clonezilla.jpg){: width="656" height="198" loading="lazy"}

        After this, you have to select the target PCs harddisk where your DietPi shall be installed. In this example there is only one harddisk present:

        ![Clonezilla target drive selection screenshot](assets/images/dietpi-boot-clonezilla-run.jpg){: width="853" height="181" loading="lazy"}

        After this, the installation process starts with several steps, e.g. showing the process of the image copying:

        ![Clonezilla processing screenshot](assets/images/dietpi-boot-partclone.jpg){: width="500" height="350" loading="lazy"}

        These steps take some time, be patient! Otherwise buy an SSD. :-)  
        At the end the system executes a shutdown.

        ??? info "Click here if you want to use a WiFi connection"
            To setup the WiFi, you have to change the network settings matching to your environment:

            1.  Open the file `dietpi-wifi.txt` and set `aWIFI_SSID[0]` to the name of your WiFi network.
            2.  In the same file `dietpi-wifi.txt`, set `aWIFI_KEY[0]` to the password of your WiFi network.
            3.  Save and close the files

            You need to set these values before you boot up the PC for the first time (initial boot).

        For the first boot up of your PC disconnect your USB stick from the target PC and power on the PC to login and execute the first boot procedure.

    === "BIOS direct write image"

        <font size="+2">硬件准备</font>

        You would need the next:

        - one **working PC with internet access**, helping to write the boot media
        - one **disc drive**, to hold the DietPi system. It is written with the direct write image and will be the disk drive in the DietPi system.
        - **target PC** to be installed

        <font size="+2">1. 下载并解压DietPi直写镜像</font>

        Download the **Native PC for BIOS/CSM** > **Direct write Image** from [`dietpi.com`](https://dietpi.com/#download) and
        extract the downloaded file to a local folder. It is a _7z_ archive format so you will need to install either [7zip for Windows](https://www.7-zip.org/) or other alternative tools.

        ![DietPi download BIOS direct write image](assets/images/dietpi-download-nativepc-bios.jpg){: width="722" height="218" loading="lazy"}

        Download [Rufus](https://rufus.ie/) and run the application. There is a portable version of Rufus available which doesn't require any local installation.

        <font size="+2">2. 写入镜像至光盘驱动器</font>

        Start [Rufus](https://rufus.ie/) application and make sure you have your disc drive connected into your computer. This may e.g. be done using an USB to SATA controller if you use a SATA disc drive. Follow the next steps:

        1. Show advanced drive properties and select **List USB hard drives**  
          (in case that you have connected your disc drive via a USB adapter)
        2. Select the disc drive device
        3. Select the downloaded **DietPi** image
        4. Click on **Start** button

        Ensure that the selected disc drive is the correct one.

        !!! warning "All data on the disc drive will be erased!"
            Before starting the installation first make a backup of the data available on the disc drive if you need it later again!

        ![Rufus BIOS direct write image selections screenshot](assets/images/dietpi-rufus-bios-direct-write-image.png){: width="474" height="607" loading="lazy"}

        <font size="+2">3. 启动目标PC </font>

        ??? info "Click here if you want to use a WiFi connection"
            To setup the WiFi, you have to change the network settings matching to your environment:

            1.  Open the file `dietpi-wifi.txt` and set `aWIFI_SSID[0]` to the name of your WiFi network.
            2.  In the same file `dietpi-wifi.txt`, set `aWIFI_KEY[0]` to the password of your WiFi network.
            3.  Save and close the files

            You need to set these values before you boot up the PC for the first time (initial boot).

        For the first boot up of your PC disconnect your disc drive from your working PC and connect it to the target PC. Then power on the target PC to login and execute the first boot procedure.

        ??? info "Option: Automatic base installation at first boot (running an _unattended base installation_)"

            DietPi offers the option for an automatic first boot installation. See section ["How to do an automatic base installation at first boot"](../usage/#how-to-do-an-automatic-base-installation-at-first-boot) for details.

## 4. 首次登录DietPi

系统的默认hostname为：**DietPi**.  
你可以在第一次启动前在配置文件 `dietpi.txt` 中改变名称。

系统启动后，你可以继续按照屏幕上的指示，或通过网络连接：

- 如果你有一个键盘和显示器连接到你的系统，你可以通过这个控制台登录。
- 如果你有一个没有连接键盘和显示器的无头系统，你可以使用像[PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)这样的**SSH**客户端来从远程系统连接。SSH服务器[Dropbear](../software/ssh/#dropbear)在DietPi上默认安装并启用。
- 大多数SBC允许通过**UART**连接串行控制台，DietPi也默认启用该功能。

此时将出现一个登录提示。请使用初始的登录凭证。

- 登录：`root'.
- 密码：`dietpi` (即你通过`dietpi.txt`设置的密码)

??? hint "如果你想通过SSH连接，请点击这里（运行一个 _无头安装_）。"

    !!! warning "第一次登录时DietPi将立即升级系统和软件包。如果你的网络连接不稳定，建议在本地执行这一步骤。"

    **IP扫描工具**

    在以下步骤中，我们需要一个IP扫描工具来确定Raspberry Pi的IP地址。

    - 对于Windows，你可以试试 "Advanced IP Scanner"。从[这里](https://www.advanced-ip-scanner.com)下载该工具。
    - 对于Linux，你可以使用`nmap`命令。

        ```sh
        sudo apt-get install nmap # for installing Nmap
        sudo nmap -sn 192.168.1.0/24 # for scanning IP address in the eange 192.168.1.0 - 192.168.1.255
        ```

    另外，你也可以在你的DHCP服务器（通常包含在路由器中）的DHCP状态页面中确定IP地址。搜索主机名**DietPi**并获得IP地址。

    **通过SSH连接到DietPi**。

    PuTTY是一个流行的Windows的SSH客户端。你可以从[这里](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)下载PuTTY。在 `主机名` 栏中输入扫描时发现的IP地址，选择 `SSH`，然后点击_Open_按钮。 
    根据你的DHCP配置，只输入 `dietpi` 就可以作为主机名。 
    有时需要在后面加上你的路由器的域名（例如：`dietpi.fritz.box`）。

    ![DietPi-SSH](assets/images/dietpi-ssh.jpg)

    大多数Linux发行版都有一个ssh客户端的包装。在你的终端中输入下一条命令（将样本IP地址 `192.168.1.20` 替换为通过扫描网络找到的IP地址）。

    ```sh
    ssh root@192.168.1.20
    ```

    或将IP地址替换为主机名

    ```sh
    ssh root@dietpi
    ```

为了进一步配置，你需要接受DietPi GPL许可证。点击键盘上的++enter++键来完成这个操作。

![dietpi-login01](assets/images/dietpi-login01.jpg){: width="640" height="371" loading="lazy"}

然后DietPi将立即开始搜索和安装更新的软件包，这将需要一些时间来完成。

软件包更新完毕后，DietPi将提示您确认是否要启用用户分析功能。

!!! info "DietPi 调查"
    DietPi调查是**可选的，默认不启用**。它是匿名的，安全的，只需极小的数据传输。所有共享的细节将在[`dietpi.com/survey`](https://dietpi.com/survey/)页面上公布。查看并了解DietPi是如何被使用的!

![dietpi-data](assets/images/dietpi-data-policy.jpg){: width="642" height="385" loading="lazy"}

默认的DietPi密码是public，所以在下一阶段会要求你为 `root` 和 `dietpi` 用户账户更改密码。选择 `OK` 并点击 ++enter++，然后重新设置你的密码（两次）。

后续您可通过在终端输入`passwd` 或者通过命令行脚本 `dietpi-config`（在“安全选项”中）再次修改密码。

![dietpi-password](assets/images/dietpi-password-01.jpg){: width="643" height="386" loading="lazy"}

## 5. 进一步设置

DietPi的基本安装是最小的**设计，允许你选择你要安装和使用的软件。只需运行 `dietpi-software` 并安装 [**DietPi优化软件**](./software/)。

你可以随时返回 **DietPi-Software** 工具，通过在终端输入 `dietpi-software` 来做进一步的修改，或者输入 `dietpi-launcher` 并选择 **DietPi-Software** 工具。

如果你想进一步改变你的DietPi配置，你可以在终端运行`dietpi-launcher`查看所有可用的DietPi工具，包括**DietPi-Update**来更新你的设备和**DietPi-Backup**来备份你的设备。

更多细节，请查看[DietPi Tools](./dietpi_tools/)部分。

## YouTube 教程 (made by community)

由Roberto Jorge制作的关于 _如何安装和初步配置DietPi_ 的视频教程。

<iframe src="https://www.youtube-nocookie.com/embed/Me0PfuNLl-Q?rel=0" frameborder="0" allow="fullscreen" width="560" height="315" loading="lazy"></iframe>

更多参考视频：

- YouTube video #1: [`Installing DietPi : Fast Linux For Any Raspberry Pi!!!`](https://www.youtube.com/watch?v=U-UXenzA2m8)
- YouTube video #2: [`How Install Diet Pi Raspberry Pi 4 Or Any SBC - Install Set Up Configure`](https://www.youtube.com/watch?v=qH0YsFNIyFo)
- YouTube video #3: [`Headless install of Dietpi | No Monitor, No LAN, No router login | Pre Configure WiFi`](https://www.youtube.com/watch?v=vlMpn9u0Y4o)
- YouTube video #4: [`Installing DietPi on Raspberry Pi, First Boot and Configuration`](https://www.youtube.com/watch?v=LzJpAUufyy0)
- YouTube video #5 (German language): [`Raspberry Pi 4 & DietPi - die schnelle Alternative - Grundinstallation einfach erklärt`](https://www.youtube.com/watch?v=J5yPeJFLSO0&list=PLQIL7cyHMGboXtOzwAcX4hGPW6ECbVinp&index=7)
