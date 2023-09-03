# CoreBookX-14-Hackintosh
EFI for Chuwi CoreBookX 14 (i5-8259U) By @weachy & @王刚 & [@maguag](https://github.com/maguag) .

**⚠️** 注意！！注意！！2022 年上架的 CoreBook X 14 16GB 版本主板大改，不能与之通用，本 EFI 仅适用于旧款（2021 款）！！

## 当前版本（Version）
**OpenCore-CoreBookX14-221008** （OpenCore 0.8.5）


如果你想了解更多关于 CoreBookX14 黑果玩机技巧，请查阅我的 [知乎专栏](https://www.zhihu.com/column/c_1419721568574013440) （
If you want to learn more about hackintosh with CoreBookX14. Please visit: My [Zhihu Column](https://www.zhihu.com/column/c_1419721568574013440) ）

## 配置（Specification）
- **Processor**: Intel Core i5-8259U @ 2.3GHz (Coffee Lake)
- **Graphic**: Intel® Iris® Plus Graphics 655 (共享显存 1536MB)
- **Wi-Fi**: 
   - （自带）Intel 7265 (不完美) / Realtek 8821CE (无解) 
   - （硬改）Broadcom BCM94360CS2 from Macbook（完美工作)
- **Ethernet**: No
- **Bluetooth**: 
   - （自带）Intel 7265 (与Wi-Fi共用一根天线，干扰严重) / Realtek 8821CE (无解) 
   - （硬改）Broadcom BCM94360CS2 from Macbook（完美工作)
- **Audio**: Realtek ALC897 
- **Touchpad**: SYNA3602
- **Storage**: 512GB Kingston RBUSNS8154P3512GJ M.2 NVME SSD
- **TF Card Reader**: Genesys Mass Storage Device (from Genesys Logic, Inc.)
- **WebCam**: USB 2.0 Camera (from Sonix Technology Co., Ltd.)
- **USB-C**: USB Gen1 5GB/s, DP output with 4k 60hz, 45w+ PD Charging
- **Battery**: 46.2 Wh Battery

## 前言（Preface）
8月份看到国光大佬的视频兴奋不已，遂产生了一起完善 CoreBookX 引导的想法，无奈大佬去意已决，挽留未果，目前我和 @王刚 [@maguag](https://github.com/maguag) 在继续维护和完善 CoreBookX 14 的引导。同时也感谢 [@rboldini](https://github.com/rboldini/CoreBook_X_OC) 为 CHUWI 相关机型黑苹果作出的辛苦贡献。

另外，我们设计出了一套“硬改方案”，使用 PCB 电路板将板载网卡改装成白果网卡，以解决 Apple 生态互联互通功能（airdrop隔空投送、接力、随航、共享剪切板等）以及在此笔记本上 Intel 蓝牙信号奇差等问题，使得它成为更为完美的黑果选择。
我们创建了QQ交流群 631070738（已满）917681794（请加此新群），欢迎大家加入共同交流完善。

## BIOS 设置（BIOS Settings）
- 「Advanced」-「CPU Configuration」-「Software Guard Extensions（SGX）」-「Disabled」
- 「Advanced」-「Power Management Control」-「CPU Lock Configuration」-「CFG Lock」-「Disabled」
- 「Advanced」-「AMI Graphic output Protocol Policy」-「Output Select」-「EDP1」  
   * For external display users only / 此选项仅限外接显示器的用户：外接显示器进入BIOS，切将此选项切到外接屏再切回 EDP1，可以解决外接显示器开机进桌面内屏黑屏的问题。
- 「Chipset」-「System Agent (SA) Configuration」-「Above 4GB MMID BIOS assignment」-「Enabled」
- 「Chipset」-「Graphics Configuration」-「DVMT Pre-Allocated」-「64MB」
- 「Boot」-「Fast Boot」-「Disabled」

## 更新日志（Change Log）

### 2022-10-08，本次更新内容：
1. 升级 OpenCore 0.9.4 正式版，例行升级 Kexts，支持 macOS Sonoma Beta

### 2022-10-08，本次更新内容：
1. 升级 OpenCore 0.8.5 正式版，例行升级 Kexts，支持 macOS Ventura

### 2022-03-17，本次更新内容：
1. 升级 OpenCore 0.7.9 正式版，例行升级 Kexts
2. 修改触摸板补丁与 ACPI 轮询的实现

### 2022-01-12，本次更新内容：
1. 升级 OpenCore 0.7.7 正式版，例行升级 Kexts
2. 解决盒盖休眠问题

### 2021-12-17，本次更新内容：
1. 升级 OpenCore 0.7.6 正式版，例行升级 Kexts
2. 处理无法检测到 macOS 12.1 更新的问题
3. 简化电池补丁、解决 Windows 系统下丢失电池的 BUG

### 2021-11-08，本次更新内容：
1. 升级 OpenCore 0.7.5，支持 macOS Monterey
2. 添加开机音效（duang）
3. 优化 kext 顺序，删除 NoTouchID.kext
4. 更新适配 Intel 网卡蓝牙驱动
5. 驱动 TF 读卡器
6. 亮度快捷键默认设置为 Fn+F11、Fn+F12
7. 新增电池补丁、触摸板补丁、以及各种 ACPI 缺失部件（感谢 [@maguag](https://github.com/maguag) @王刚 两位大佬的辛苦付出）

### 2021-09-10，本次更新内容：
1. 上一个版本中合盖睡眠在唤醒时偶发内核崩溃的问题
2. 修复充电状态延迟问题
3. 修复键盘波浪键（~）被映射为（±）的问题
4. 修正 Fn+F10 对应的播放暂停功能
5. 插入/移除耳机自动切换输出源（耳机->扬声器）
6. 重新整理 EFI 中，各项不规范的地方，增加稳定性：重新梳理 USB 定制、SSDT方式修改按键映射、完善触摸板相关（SSDT-GPI0.aml）、更正操作系统补丁（SSDT-OC-XOSI.aml）、添加 PNLF 重命名等等

#### 之前所做修复已提交给国光兄弟（详见 [CHUWI-COREBOOK-X-I5-8259U GitHub](https://github.com/sqlsec/CHUWI-COREBOOK-X-I5-8259U) ）
1. 实现合盖睡眠、开盖自动唤醒（由于 ACPI 不完整，会造成唤醒偶发内核崩溃）
2. 功能键调节亮度暂时无解，建议手动修改“系统偏好设置--键盘--快捷键--显示器”中的亮度快捷键，例如改为 F6、F7。
3. 提高触控板三指触控的稳定性
4. 对调 Command、Option 按键映射，遵循白苹果的按键布局
5. 显示器设置中新增自动调节亮度选项（没有实际效果），接通电源屏幕亮度会提高

