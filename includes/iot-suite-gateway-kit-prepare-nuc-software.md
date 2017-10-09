## <a name="build-iot-edge"></a><span data-ttu-id="55ebf-101">IoT-rand bouwen</span><span class="sxs-lookup"><span data-stu-id="55ebf-101">Build IoT Edge</span></span>

<span data-ttu-id="55ebf-102">Deze zelfstudie maakt gebruik van aangepaste IoT rand modules toocommunicate Hello vooraf geconfigureerde oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="55ebf-102">This tutorial uses custom IoT Edge modules toocommunicate with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="55ebf-103">Daarom moet u toobuild Hallo IoT Edge-modules uit aangepaste broncode.</span><span class="sxs-lookup"><span data-stu-id="55ebf-103">Therefore, you need toobuild hello IoT Edge modules from custom source code.</span></span> <span data-ttu-id="55ebf-104">Hallo uit te voeren wordt beschreven hoe tooinstall IoT rand en build Hallo aangepaste module voor IoT rand.</span><span class="sxs-lookup"><span data-stu-id="55ebf-104">hello following sections describe how tooinstall IoT Edge and build hello custom IoT Edge module.</span></span>

### <a name="install-iot-edge"></a><span data-ttu-id="55ebf-105">IoT-rand installeren</span><span class="sxs-lookup"><span data-stu-id="55ebf-105">Install IoT Edge</span></span>

<span data-ttu-id="55ebf-106">Hallo volgende stappen wordt beschreven hoe tooinstall Hallo IoT rand software op Hallo Intel NUC vooraf gecompileerd:</span><span class="sxs-lookup"><span data-stu-id="55ebf-106">hello following steps describe how tooinstall hello pre-compiled IoT Edge software on hello Intel NUC:</span></span>

1. <span data-ttu-id="55ebf-107">Hallo vereist smart pakket opslagplaatsen door het uitvoeren van de volgende opdrachten op Hallo Intel NUC Hallo configureren:</span><span class="sxs-lookup"><span data-stu-id="55ebf-107">Configure hello required smart package repositories by running hello following commands on hello Intel NUC:</span></span>

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    <span data-ttu-id="55ebf-108">Voer `y` wanneer Hallo-opdracht wordt u gevraagd te**dit kanaal opnemen?**.</span><span class="sxs-lookup"><span data-stu-id="55ebf-108">Enter `y` when hello command prompts you too**Include this channel?**.</span></span>

1. <span data-ttu-id="55ebf-109">Hallo smart Pakketbeheer bijwerken door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="55ebf-109">Update hello smart package manager by running hello following command:</span></span>

    ```bash
    smart update
    ```

1. <span data-ttu-id="55ebf-110">Hello Azure IoT rand pakket installeren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="55ebf-110">Install hello Azure IoT Edge package by running hello following command:</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. <span data-ttu-id="55ebf-111">Hallo installatie controleren door actieve Hallo "Hallo wereld" voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="55ebf-111">Verify hello installation by running hello "Hello world" sample.</span></span> <span data-ttu-id="55ebf-112">Dit voorbeeld schrijft een hello world toohello log.txT berichtbestand elke vijf seconden.</span><span class="sxs-lookup"><span data-stu-id="55ebf-112">This sample writes a hello world message toohello log.txT file every five seconds.</span></span> <span data-ttu-id="55ebf-113">Hallo volgende opdrachten uitgevoerd Hallo "Hallo wereld" voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="55ebf-113">hello following commands run hello "Hello world" sample:</span></span>

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    <span data-ttu-id="55ebf-114">Alle **ongeldig argument** wanneer u stopt met het voorbeeld Hallo-berichten.</span><span class="sxs-lookup"><span data-stu-id="55ebf-114">Ignore any **invalid argument** messages when you stop hello sample.</span></span>

    <span data-ttu-id="55ebf-115">Hallo opdracht tooview Hallo inhoud van het logboekbestand Hallo volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="55ebf-115">Use hello following command tooview hello contents of hello log file:</span></span>

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a><span data-ttu-id="55ebf-116">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="55ebf-116">Troubleshooting</span></span>

<span data-ttu-id="55ebf-117">Als u de foutmelding Hallo 'geen pakket biedt util-linux-dev', Hallo Intel NUC opnieuw op te starten.</span><span class="sxs-lookup"><span data-stu-id="55ebf-117">If you receive hello error "No package provides util-linux-dev", try rebooting hello Intel NUC.</span></span>
