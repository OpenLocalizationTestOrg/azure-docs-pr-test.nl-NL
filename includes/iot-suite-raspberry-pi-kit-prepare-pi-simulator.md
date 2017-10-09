## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="adc0f-101">Uw Raspberry Pi voorbereiden</span><span class="sxs-lookup"><span data-stu-id="adc0f-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="adc0f-102">Raspbian installeren</span><span class="sxs-lookup"><span data-stu-id="adc0f-102">Install Raspbian</span></span>

<span data-ttu-id="adc0f-103">Als dit Hallo eerste keer dat u uw Pi frambozen gebruikt, moet u tooinstall hello Raspbian besturingssysteem via NOOBS op Hallo SD-kaart is opgenomen in het Hallo-pakket.</span><span class="sxs-lookup"><span data-stu-id="adc0f-103">If this is hello first time you are using your Raspberry Pi, you need tooinstall hello Raspbian operating system using NOOBS on hello SD card included in hello kit.</span></span> <span data-ttu-id="adc0f-104">Hallo [frambozen Pi Software handleiding] [ lnk-install-raspbian] beschrijft hoe een besturingssysteem op uw Pi frambozen tooinstall.</span><span class="sxs-lookup"><span data-stu-id="adc0f-104">hello [Raspberry Pi Software Guide][lnk-install-raspbian] describes how tooinstall an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="adc0f-105">Deze zelfstudie wordt ervan uitgegaan dat u hebt Hallo Raspbian-besturingssysteem geïnstalleerd op uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="adc0f-105">This tutorial assumes you have installed hello Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="adc0f-106">Hallo SD-kaart is opgenomen in Hallo [Microsoft Azure IoT Starter Kit voor frambozen Pi 3] [ lnk-starter-kits] al NOOBS geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="adc0f-106">hello SD card included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="adc0f-107">U kunt opstarten Hallo frambozen Pi van deze kaart en tooinstall hello Raspbian OS kiezen.</span><span class="sxs-lookup"><span data-stu-id="adc0f-107">You can boot hello Raspberry Pi from this card and choose tooinstall hello Raspbian OS.</span></span>

<span data-ttu-id="adc0f-108">toocomplete hello hardware-installatie, moet u:</span><span class="sxs-lookup"><span data-stu-id="adc0f-108">toocomplete hello hardware setup, you need to:</span></span>

- <span data-ttu-id="adc0f-109">Verbinding maken met uw frambozen Pi toohello voeding opgenomen in het Hallo-pakket.</span><span class="sxs-lookup"><span data-stu-id="adc0f-109">Connect your Raspberry Pi toohello power supply included in hello kit.</span></span>
- <span data-ttu-id="adc0f-110">Verbinding maken met uw frambozen Pi tooyour netwerk met Hallo Ethernet-kabel is opgenomen in de kit.</span><span class="sxs-lookup"><span data-stu-id="adc0f-110">Connect your Raspberry Pi tooyour network using hello Ethernet cable included in your kit.</span></span> <span data-ttu-id="adc0f-111">U kunt ook kunt u instellen [draadloze netwerkverbinding] [ lnk-pi-wireless] voor uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="adc0f-111">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="adc0f-112">U hebt nu Hallo hardware-instellingen van uw Pi frambozen voltooid.</span><span class="sxs-lookup"><span data-stu-id="adc0f-112">You have now completed hello hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="adc0f-113">Aanmelden en Hallo terminal</span><span class="sxs-lookup"><span data-stu-id="adc0f-113">Sign in and access hello terminal</span></span>

<span data-ttu-id="adc0f-114">U hebt twee opties tooaccess een terminal-omgeving op uw Pi frambozen:</span><span class="sxs-lookup"><span data-stu-id="adc0f-114">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="adc0f-115">Als u een toetsenbord hebt en verbonden tooyour frambozen Pi bewaken, kunt u Hallo Raspbian GUI tooaccess een terminalvenster gebruiken.</span><span class="sxs-lookup"><span data-stu-id="adc0f-115">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

- <span data-ttu-id="adc0f-116">Hallo opdrachtregel toegang op uw frambozen Pi gebruik van SSH op uw computer.</span><span class="sxs-lookup"><span data-stu-id="adc0f-116">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="adc0f-117">Een terminalvenster in Hallo GUI gebruiken</span><span class="sxs-lookup"><span data-stu-id="adc0f-117">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="adc0f-118">Hallo standaardreferenties voor Raspbian zijn gebruikersnaam **pi** en het wachtwoord **frambozen**.</span><span class="sxs-lookup"><span data-stu-id="adc0f-118">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="adc0f-119">In de taakbalk Hallo in Hallo GUI, kunt u Hallo starten **Terminal** hulpprogramma Hallo-pictogram dat op een monitor lijkt.</span><span class="sxs-lookup"><span data-stu-id="adc0f-119">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="adc0f-120">Meld u aan met SSH</span><span class="sxs-lookup"><span data-stu-id="adc0f-120">Sign in with SSH</span></span>

<span data-ttu-id="adc0f-121">U kunt SSH gebruiken voor toegang tot opdrachtregel tooyour frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="adc0f-121">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="adc0f-122">Hallo artikel [SSH (Secure Shell)] [ lnk-pi-ssh] wordt beschreven hoe tooconfigure SSH op uw Pi frambozen en hoe tooconnect van [Windows] [ lnk-ssh-windows] of [Linux en Mac OS][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="adc0f-122">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="adc0f-123">Aanmelden met gebruikersnaam **pi** en het wachtwoord **frambozen**.</span><span class="sxs-lookup"><span data-stu-id="adc0f-123">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="adc0f-124">Optioneel: Een map op uw Pi frambozen delen</span><span class="sxs-lookup"><span data-stu-id="adc0f-124">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="adc0f-125">Desgewenst kunt u tooshare een map op uw frambozen Pi met uw bureaublad omgeving.</span><span class="sxs-lookup"><span data-stu-id="adc0f-125">Optionally, you may want tooshare a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="adc0f-126">U toouse uw voorkeur bureaublad teksteditor delen van een map kunt (zoals [Visual Studio Code](https://code.visualstudio.com/) of [Sublime Text](http://www.sublimetext.com/)) tooedit bestanden op uw Pi frambozen in plaats van `nano` of `vi`.</span><span class="sxs-lookup"><span data-stu-id="adc0f-126">Sharing a folder enables you toouse your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) tooedit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="adc0f-127">tooshare een map met Windows, configureert een Samba-server op Hallo frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="adc0f-127">tooshare a folder with Windows, configure a Samba server on hello Raspberry Pi.</span></span> <span data-ttu-id="adc0f-128">Ook gebruiken Hallo ingebouwde [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server met een SFTP-client op het bureaublad.</span><span class="sxs-lookup"><span data-stu-id="adc0f-128">Alternatively, use hello built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/