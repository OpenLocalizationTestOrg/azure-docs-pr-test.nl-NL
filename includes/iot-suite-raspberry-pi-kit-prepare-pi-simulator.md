## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="3685d-101">Uw Raspberry Pi voorbereiden</span><span class="sxs-lookup"><span data-stu-id="3685d-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="3685d-102">Raspbian installeren</span><span class="sxs-lookup"><span data-stu-id="3685d-102">Install Raspbian</span></span>

<span data-ttu-id="3685d-103">Als dit de eerste keer dat u uw Pi frambozen gebruikt, moet u het Raspbian-besturingssysteem met behulp van NOOBS op de SD-kaart die is opgenomen in de kit installeren.</span><span class="sxs-lookup"><span data-stu-id="3685d-103">If this is the first time you are using your Raspberry Pi, you need to install the Raspbian operating system using NOOBS on the SD card included in the kit.</span></span> <span data-ttu-id="3685d-104">De [frambozen Pi Software handleiding] [ lnk-install-raspbian] wordt beschreven hoe u een besturingssysteem installeren op uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="3685d-104">The [Raspberry Pi Software Guide][lnk-install-raspbian] describes how to install an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="3685d-105">Deze zelfstudie wordt ervan uitgegaan dat u het besturingssysteem Raspbian op uw Pi frambozen hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3685d-105">This tutorial assumes you have installed the Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="3685d-106">De SD-kaart die is opgenomen in de [Microsoft Azure IoT Starter Kit voor frambozen Pi 3] [ lnk-starter-kits] al NOOBS geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3685d-106">The SD card included in the [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="3685d-107">U kunt de Pi frambozen van deze kaart opstart en installeren van het besturingssysteem Raspbian.</span><span class="sxs-lookup"><span data-stu-id="3685d-107">You can boot the Raspberry Pi from this card and choose to install the Raspbian OS.</span></span>

<span data-ttu-id="3685d-108">U voltooit de installatie van de hardware, moet u:</span><span class="sxs-lookup"><span data-stu-id="3685d-108">To complete the hardware setup, you need to:</span></span>

- <span data-ttu-id="3685d-109">Verbinding maken met uw frambozen-Pi de voeding die is opgenomen in het pakket.</span><span class="sxs-lookup"><span data-stu-id="3685d-109">Connect your Raspberry Pi to the power supply included in the kit.</span></span>
- <span data-ttu-id="3685d-110">Verbinding maken met uw Pi frambozen via de Ethernet-kabel in uw kit opgenomen met het netwerk.</span><span class="sxs-lookup"><span data-stu-id="3685d-110">Connect your Raspberry Pi to your network using the Ethernet cable included in your kit.</span></span> <span data-ttu-id="3685d-111">U kunt ook kunt u instellen [draadloze netwerkverbinding] [ lnk-pi-wireless] voor uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="3685d-111">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="3685d-112">U hebt nu de hardware-instellingen van uw Pi frambozen voltooid.</span><span class="sxs-lookup"><span data-stu-id="3685d-112">You have now completed the hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="3685d-113">Aanmelden en toegang tot de terminal</span><span class="sxs-lookup"><span data-stu-id="3685d-113">Sign in and access the terminal</span></span>

<span data-ttu-id="3685d-114">U hebt twee opties voor toegang tot een terminal omgeving op uw Pi frambozen:</span><span class="sxs-lookup"><span data-stu-id="3685d-114">You have two options to access a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="3685d-115">Als u een toetsenbord en de monitor die zijn verbonden met uw Pi frambozen hebt, kunt u de gebruikersinterface van Raspbian voor toegang tot een terminalvenster.</span><span class="sxs-lookup"><span data-stu-id="3685d-115">If you have a keyboard and monitor connected to your Raspberry Pi, you can use the Raspbian GUI to access a terminal window.</span></span>

- <span data-ttu-id="3685d-116">Toegang tot de opdrachtregel op uw frambozen Pi gebruik van SSH op uw computer.</span><span class="sxs-lookup"><span data-stu-id="3685d-116">Access the command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-the-gui"></a><span data-ttu-id="3685d-117">Gebruik een terminalvenster in de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="3685d-117">Use a terminal Window in the GUI</span></span>

<span data-ttu-id="3685d-118">De standaardreferenties voor Raspbian zijn gebruikersnaam **pi** en het wachtwoord **frambozen**.</span><span class="sxs-lookup"><span data-stu-id="3685d-118">The default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="3685d-119">U kunt starten in de taakbalk in de gebruikersinterface van de **Terminal** hulpprogramma met het pictogram dat op een monitor lijkt.</span><span class="sxs-lookup"><span data-stu-id="3685d-119">In the task bar in the GUI, you can launch the **Terminal** utility using the icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="3685d-120">Meld u aan met SSH</span><span class="sxs-lookup"><span data-stu-id="3685d-120">Sign in with SSH</span></span>

<span data-ttu-id="3685d-121">U kunt SSH gebruiken voor vanaf de opdrachtregel toegang tot uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="3685d-121">You can use SSH for command-line access to your Raspberry Pi.</span></span> <span data-ttu-id="3685d-122">Het artikel [SSH (Secure Shell)] [ lnk-pi-ssh] wordt beschreven hoe SSH configureren op uw Pi frambozen en verbinding maken van [Windows] [ lnk-ssh-windows] of [Linux en Mac OS][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="3685d-122">The article [SSH (Secure Shell)][lnk-pi-ssh] describes how to configure SSH on your Raspberry Pi, and how to connect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="3685d-123">Aanmelden met gebruikersnaam **pi** en het wachtwoord **frambozen**.</span><span class="sxs-lookup"><span data-stu-id="3685d-123">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="3685d-124">Optioneel: Een map op uw Pi frambozen delen</span><span class="sxs-lookup"><span data-stu-id="3685d-124">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="3685d-125">U kunt desgewenst een map op uw Pi frambozen delen met uw bureaublad omgeving.</span><span class="sxs-lookup"><span data-stu-id="3685d-125">Optionally, you may want to share a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="3685d-126">Delen van een map, kunt u gebruikmaken van uw voorkeur bureaublad teksteditor (zoals [Visual Studio Code](https://code.visualstudio.com/) of [Sublime Text](http://www.sublimetext.com/)) voor het bewerken van bestanden op uw Pi frambozen in plaats van `nano` of `vi`.</span><span class="sxs-lookup"><span data-stu-id="3685d-126">Sharing a folder enables you to use your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) to edit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="3685d-127">Als u wilt delen een map met Windows, configureert u een Samba-server op de frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="3685d-127">To share a folder with Windows, configure a Samba server on the Raspberry Pi.</span></span> <span data-ttu-id="3685d-128">U kunt ook gebruik van de ingebouwde [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server met een SFTP-client op het bureaublad.</span><span class="sxs-lookup"><span data-stu-id="3685d-128">Alternatively, use the built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/