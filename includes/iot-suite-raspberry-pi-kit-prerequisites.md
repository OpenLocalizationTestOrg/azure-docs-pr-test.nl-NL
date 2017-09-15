## <a name="prerequisites"></a><span data-ttu-id="e79f9-101">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e79f9-101">Prerequisites</span></span>

<span data-ttu-id="e79f9-102">U hebt een actief Azure-abonnement nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="e79f9-102">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="e79f9-103">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="e79f9-103">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e79f9-104">Zie [Gratis proefversie van Azure][lnk-free-trial] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e79f9-104">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="e79f9-105">Vereiste software</span><span class="sxs-lookup"><span data-stu-id="e79f9-105">Required software</span></span>

<span data-ttu-id="e79f9-106">SSH-client moet u op de computer waarmee u kunt extern toegang tot de opdrachtregel op de frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="e79f9-106">You need SSH client on your desktop machine to enable you to remotely access the command line on the Raspberry Pi.</span></span>

- <span data-ttu-id="e79f9-107">Windows bevat geen een SSH-client.</span><span class="sxs-lookup"><span data-stu-id="e79f9-107">Windows does not include an SSH client.</span></span> <span data-ttu-id="e79f9-108">Wordt u aangeraden [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="e79f9-108">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="e79f9-109">De meeste Linux-distributies en Mac OS omvatten het SSH-opdrachtregelprogramma.</span><span class="sxs-lookup"><span data-stu-id="e79f9-109">Most Linux distributions and Mac OS include the command-line SSH utility.</span></span> <span data-ttu-id="e79f9-110">Zie voor meer informatie [SSH met behulp van Linux- of Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span><span class="sxs-lookup"><span data-stu-id="e79f9-110">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="e79f9-111">Vereiste hardware</span><span class="sxs-lookup"><span data-stu-id="e79f9-111">Required hardware</span></span>

<span data-ttu-id="e79f9-112">Een desktopcomputer zodat u kunt extern verbinding maken met de opdrachtregel op de frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="e79f9-112">A desktop computer to enable you to connect remotely to the command line on the Raspberry Pi.</span></span>

<span data-ttu-id="e79f9-113">[Microsoft IoT Starter Kit voor frambozen Pi 3] [ lnk-starter-kits] of gelijkwaardige onderdelen.</span><span class="sxs-lookup"><span data-stu-id="e79f9-113">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="e79f9-114">Deze zelfstudie maakt gebruik van de volgende items van de kit:</span><span class="sxs-lookup"><span data-stu-id="e79f9-114">This tutorial uses the following items from the kit:</span></span>

- <span data-ttu-id="e79f9-115">Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="e79f9-115">Raspberry Pi 3</span></span>
- <span data-ttu-id="e79f9-116">MicroSD-kaart (met NOOBS)</span><span class="sxs-lookup"><span data-stu-id="e79f9-116">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="e79f9-117">Een Mini USB-kabel</span><span class="sxs-lookup"><span data-stu-id="e79f9-117">A USB Mini cable</span></span>
- <span data-ttu-id="e79f9-118">Een Ethernet-kabel</span><span class="sxs-lookup"><span data-stu-id="e79f9-118">An Ethernet cable</span></span>
- <span data-ttu-id="e79f9-119">BME280-temperatuursensor</span><span class="sxs-lookup"><span data-stu-id="e79f9-119">BME280 sensor</span></span>
- <span data-ttu-id="e79f9-120">Breadboard</span><span class="sxs-lookup"><span data-stu-id="e79f9-120">Breadboard</span></span>
- <span data-ttu-id="e79f9-121">Meestal kabels</span><span class="sxs-lookup"><span data-stu-id="e79f9-121">Jumper wires</span></span>
- <span data-ttu-id="e79f9-122">Weerstand</span><span class="sxs-lookup"><span data-stu-id="e79f9-122">Resistors</span></span>
- <span data-ttu-id="e79f9-123">LED 's</span><span class="sxs-lookup"><span data-stu-id="e79f9-123">LEDs</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/