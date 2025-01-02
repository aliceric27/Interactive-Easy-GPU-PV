
[English](README_en.md) | [中文](README.md)

# 專案來源
一個正在進行中的 [jamesstringerparse Easy-GPU-PV repository](https://github.com/jamesstringerparsec/Easy-GPU-PV) 分支。該項目的目標是盡可能簡化整個過程。主要腳本是互動式的，因此用戶不必提前定義任何參數。相反，可以在腳本運行時選擇參數，使過程變得更加簡單。

![Administrator_-PowerShell-2023-03-21-16-38-00](https://github.com/aliceric27/picx-images-hosting/raw/master/GIF-2025-1-2-下午-07-44-59.99tfgndo79.gif)

***以下文字主要取自原始的 Easy-GPU-PV 項目。我做了一些修改和改進，以確保它準確反映項目的當前狀態並提供相關信息。***

GPU-PV 允許您將系統的專用或集成 GPU 分區，並將其分配給多個 Hyper-V 虛擬機。這是 WSL2 和 Windows Sandbox 中使用的相同技術。

Interactive-Easy-GPU-PV 的目標是通過自動化啟動 GPU-PV 虛擬機所需的步驟來簡化此過程。
此專案提供以下功能...
1) 創建您選擇的虛擬機
2) 自動將 Windows 安裝到虛擬機
3) 分區您選擇的 GPU 並將所需的驅動程式文件複製到虛擬機
4) 將 [Parsec](https://parsec.app) 安裝到虛擬機，Parsec 是一款超低延遲的遠端桌面應用程式，使用此應用程式連接到虛擬機。您可以免費非商業使用 Parsec。若要商業使用 Parsec，請註冊 [Parsec For Teams](https://parsec.app/teams) 帳戶
5) 配置 Microsoft 遠端桌面以提供 3D 加速的遠端會話。請注意，Microsoft RDP 遠端會話中的 3D 加速性能不如 Parsec 遠端桌面會話。

### 先決條件：
* 一台運行 Windows 10 20H1+ 專業版、企業版或教育版，或 Windows 11 專業版、企業版或教育版，或 Windows Server 2022 的桌面電腦。為了更好的兼容性，建議使用 Windows 11 或 Windows Server 2022。主機和虛擬機必須使用相同版本的 Windows，因為版本不匹配可能會導致兼容性問題、藍屏或其他問題。例如，Win10 21H1 + Win10 21H1 或 Win11 21H2 + Win11 21H2。
* 配備專用 NVIDIA/AMD GPU 或集成 Intel GPU 的電腦。目前不支持配備 NVIDIA GPU 的筆記型電腦，但集成 Intel GPU 的筆記型電腦可以使用。GPU 必須支持硬體視頻編碼（NVIDIA NVENC、Intel Quicksync 或 AMD AMF）。
* 從 [Intel.com](https://www.intel.com/content/www/us/en/search.html#sort=relevancy&f:@tabfilter=[Downloads]&f:@stm_10385_en=[Graphics]) 或 [AMD.com](https://www.amd.com/en/support) 或 [NVIDIA.com](https://www.nvidia.com/download/index.aspx) 下載的最新 GPU 驅動程式（對於桌面 NVIDIA GPU，僅支持 GameReady 驅動程式）。不要依賴設備管理器或 Windows 更新來安裝驅動程式。確保安裝最新的驅動程式以避免兼容性問題並確保最佳性能。
* 從[這裡下載](https://www.microsoft.com/en-gb/software-download/windows10ISO)的最新 Windows 10 ISO / 從[這裡下載](https://www.microsoft.com/en-us/software-download/windows11)的 Windows 11 ISO - 不要使用媒體創建工具，如果沒有直接的 ISO 下載鏈接，請遵循[此指南](https://www.nextofwindows.com/downloading-windows-10-iso-images-using-rufus)。
* 主板上啟用虛擬化並在 Windows 10/11 操作系統上[完全啟用 Hyper-V](https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)（需要重啟）。
* 允許在系統上運行 Powershell 腳本 - 通常通過以管理員身份運行 Powershell 並執行 "Set-ExecutionPolicy unrestricted"。

### 使用說明
要開始使用 Interactive-Easy-GPU-PV，請按照以下步驟操作：
1) 確保您的系統符合文檔中提到的所有先決條件。
2) 下載 [Interactive-Easy-GPU-PV repository](https://github.com/jamesstringerparsec/Easy-GPU-PV/archive/refs/heads/main.zip) 並將其解壓縮到電腦上的一個文件夾中。您可以從項目的 GitHub 頁面下載。
3) 在電腦上搜索 Powershell ISE 並以管理員身份運行。
4) 導航到您下載的解壓縮文件夾並運行名為 "GPUP-management.ps1" 的互動式腳本。在提示時選擇 "Create new VM with GPU acceleration" 並設置任何所需的參數。腳本將開始創建虛擬機，這可能需要 5-10 分鐘，具體取決於您的系統。
5) 虛擬機創建完成後，在虛擬機上打開並登錄 Parsec。您可以使用 Parsec 以高達 4K60FPS 的速度連接到虛擬機。
6) 一切就緒，享受吧！

### 更新主機 GPU 驅動程式後升級虛擬機 GPU 驅動程式
為了確保虛擬機的正常運行，在更新主機上的驅動程式後，必須更新虛擬機內的 GPU 驅動程式。要做到這一點，請按照以下步驟操作：
1) 在主機上更新 GPU 驅動程式後，重新啟動。
2) 以管理員身份打開 Powershell，導航到 Interactive-Easy-GPU-PV repo 的解壓縮文件夾並運行互動式腳本 GPUP-management.ps1。
3) 選擇操作 3：從主機複製 GPU 驅動程式到虛擬機。這將把更新的 GPU 驅動程式從主機複製到虛擬機。



### 注意事項：
- 如果您安裝了 Parsec 虛擬顯示驅動程式 (Parsec VDD)，在虛擬機上登入 Parsec 後，請始終使用 Parsec 連接到虛擬機。保持 Microsoft Hyper-V 視訊適配器禁用。使用 RDP 和 Hyper-V 增強會話模式將導致 Parsec 中的行為異常和黑屏。使用 Parsec 可以讓您使用高達 4k60 FPS 的解析度。
- 如果您收到 "ERROR : Cannot bind argument to parameter 'Path' because it is null." 這可能意味著您使用了媒體創建工具下載 ISO。不幸的是，您不能使用該工具，如果在 Microsoft 頁面上看不到直接的 ISO 下載鏈接，請遵循[此指南](https://www.nextofwindows.com/downloading-windows-10-iso-images-using-rufus)。
- 您主機上的 GPU 在設備管理器中將顯示為 Microsoft 驅動程式，而不是 nvidia/intel/amd 驅動程式。只要在設備管理器中沒有黃色三角形，它就能正常工作。
- 必須將顯示器或 HDMI 虛擬插頭插入 GPU，以允許 Parsec 捕捉螢幕。無論有多少虛擬機，每台主機只需要一個。
- 如果您的電腦速度非常快，可能會在音訊驅動程式 (VB Cable) 和 Parsec 顯示驅動程式安裝之前到達登入畫面，但不用擔心！它們應該很快就會安裝。
- 當 UAC 提示出現、應用程式進入和退出全螢幕以及在 Parsec 中切換視頻編解碼器時，螢幕可能會黑屏長達 10 秒，不確定為什麼會發生這種情況，這是 GPU-P 機器特有的，並且在 1280x720 時似乎恢復得更快。
- Vulkan 渲染器不可用，GL 遊戲可能會或可能不會運行。[這個](https://www.microsoft.com/en-us/p/opencl-and-opengl-compatibility-pack/9nqpsl29bfff?SilentAuth=1&wa=wsignin1.0#activetab=pivot:overviewtab) 可能對某些 OpenGL 應用程式有幫助。
- 如果您在機器上沒有管理員權限，這意味著您將用戶名和虛擬機名稱設置為相同，這些需要不同。
- AMD Polaris GPU，例如 RX 580，目前不支持通過 GPU 虛擬化進行硬體視頻編碼。
- 要使用 Rufus 下載 Windows ISO，必須啟用 "檢查更新"。


### 感謝：
- [jamesstringerparsec](https://github.com/jamesstringerparsec/Easy-GPU-PV) 創建了 EASY-GPU-PV 項目，該項目作為本 readme 的基礎和主要部分
- [Hyper-ConvertImage](https://github.com/tabs-not-spaces/Hyper-ConvertImage) 創建了更新版本的 [Convert-WindowsImage](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/master/hyperv-tools/Convert-WindowsImage)，該版本與 Windows 10 和 11 兼容。
- [gawainXX](https://github.com/gawainXX) 幫助 [jamesstringerparsec](https://github.com/jamesstringerparsec/Easy-GPU-PV) 測試並指出錯誤和功能改進。
- [KharchenkoPM](https://github.com/KharchenkoPM/Interactive-Easy-GPU-PV) 建立了原始 EASY-GPU-PV 版本修改後的專案
