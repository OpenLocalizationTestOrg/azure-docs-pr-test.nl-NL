## <a name="overview"></a><span data-ttu-id="f4a0d-101">Overzicht</span><span class="sxs-lookup"><span data-stu-id="f4a0d-101">Overview</span></span>

<span data-ttu-id="f4a0d-102">In deze zelfstudie maakt uitvoeren u Hallo stappen:</span><span class="sxs-lookup"><span data-stu-id="f4a0d-102">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="f4a0d-103">Implementeer een exemplaar van Hallo externe controle vooraf geconfigureerde oplossing tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f4a0d-103">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="f4a0d-104">Deze stap implementeert automatisch en meerdere Azure-services configureert.</span><span class="sxs-lookup"><span data-stu-id="f4a0d-104">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="f4a0d-105">Uw apparaat toocommunicate met uw computer en het Hallo-oplossing voor externe controle instellen.</span><span class="sxs-lookup"><span data-stu-id="f4a0d-105">Set up your device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="f4a0d-106">Bijwerken van Hallo voorbeeld apparaat code tooconnect toohello oplossing voor externe controle en gesimuleerde telemetrie die u op het dashboard van de oplossing Hallo weergeven kunt verzenden.</span><span class="sxs-lookup"><span data-stu-id="f4a0d-106">Update hello sample device code tooconnect toohello remote monitoring solution, and send simulated telemetry that you can view on hello solution dashboard.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4a0d-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f4a0d-107">Prerequisites</span></span>

<span data-ttu-id="f4a0d-108">toocomplete in deze zelfstudie, moet u een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f4a0d-108">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="f4a0d-109">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="f4a0d-109">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f4a0d-110">Zie [Gratis proefversie van Azure][lnk-free-trial] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f4a0d-110">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="f4a0d-111">Vereiste software</span><span class="sxs-lookup"><span data-stu-id="f4a0d-111">Required software</span></span>

<span data-ttu-id="f4a0d-112">SSH-client moet u op uw computer tooenable u tooremotely access Hallo-opdracht regel op Hallo frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="f4a0d-112">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="f4a0d-113">Windows bevat geen een SSH-client.</span><span class="sxs-lookup"><span data-stu-id="f4a0d-113">Windows does not include an SSH client.</span></span> <span data-ttu-id="f4a0d-114">Wordt u aangeraden [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="f4a0d-114">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="f4a0d-115">De meeste Linux-distributies en Mac OS bevatten Hallo SSH-opdrachtregelprogramma.</span><span class="sxs-lookup"><span data-stu-id="f4a0d-115">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="f4a0d-116">Zie voor meer informatie [SSH met behulp van Linux- of Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span><span class="sxs-lookup"><span data-stu-id="f4a0d-116">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="f4a0d-117">Vereiste hardware</span><span class="sxs-lookup"><span data-stu-id="f4a0d-117">Required hardware</span></span>

<span data-ttu-id="f4a0d-118">Een desktopcomputer tooenable u tooconnect op afstand toohello opdracht regel op Hallo frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="f4a0d-118">A desktop computer tooenable you tooconnect remotely toohello command line on hello Raspberry Pi.</span></span>

<span data-ttu-id="f4a0d-119">[Microsoft IoT Starter Kit voor frambozen Pi 3] [ lnk-starter-kits] of gelijkwaardige onderdelen.</span><span class="sxs-lookup"><span data-stu-id="f4a0d-119">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="f4a0d-120">In deze zelfstudie wordt de volgende items uit de Hallo kit Hallo:</span><span class="sxs-lookup"><span data-stu-id="f4a0d-120">This tutorial uses hello following items from hello kit:</span></span>

- <span data-ttu-id="f4a0d-121">Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="f4a0d-121">Raspberry Pi 3</span></span>
- <span data-ttu-id="f4a0d-122">MicroSD-kaart (met NOOBS)</span><span class="sxs-lookup"><span data-stu-id="f4a0d-122">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="f4a0d-123">Een Mini USB-kabel</span><span class="sxs-lookup"><span data-stu-id="f4a0d-123">A USB Mini cable</span></span>
- <span data-ttu-id="f4a0d-124">Een Ethernet-kabel</span><span class="sxs-lookup"><span data-stu-id="f4a0d-124">An Ethernet cable</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/