## <a name="install-hello-prerequisites"></a><span data-ttu-id="88361-101">Hallo vereisten installeren</span><span class="sxs-lookup"><span data-stu-id="88361-101">Install hello prerequisites</span></span>

1. <span data-ttu-id="88361-102">Installeer [Visual Studio 2015 of 2017](https://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="88361-102">Install [Visual Studio 2015 or 2017](https://www.visualstudio.com).</span></span> <span data-ttu-id="88361-103">U kunt Hallo Community Edition gratis als u voldoen aan de licentievereisten Hallo.</span><span class="sxs-lookup"><span data-stu-id="88361-103">You can use hello free Community Edition if you meet hello licensing requirements.</span></span> <span data-ttu-id="88361-104">Worden ervoor tooinclude Visual C++ en NuGet Package Manager.</span><span class="sxs-lookup"><span data-stu-id="88361-104">Be sure tooinclude Visual C++ and NuGet Package Manager.</span></span>

1. <span data-ttu-id="88361-105">Installeer [git](http://www.git-scm.com) en zorg ervoor dat u kunt git.exe uitvoeren vanaf de opdrachtregel Hallo.</span><span class="sxs-lookup"><span data-stu-id="88361-105">Install [git](http://www.git-scm.com) and make sure you can run git.exe from hello command line.</span></span>

1. <span data-ttu-id="88361-106">Installeer [CMake](https://cmake.org/download/) en zorg ervoor dat u kunt cmake.exe uitvoeren vanaf de opdrachtregel Hallo.</span><span class="sxs-lookup"><span data-stu-id="88361-106">Install [CMake](https://cmake.org/download/) and make sure you can run cmake.exe from hello command line.</span></span> <span data-ttu-id="88361-107">CMake versie 3.7.2 of later wordt aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="88361-107">CMake version 3.7.2 or later is recommended.</span></span> <span data-ttu-id="88361-108">Hallo **.msi** installatieprogramma is de eenvoudigste optie Hallo in Windows.</span><span class="sxs-lookup"><span data-stu-id="88361-108">hello **.msi** installer is hello easiest option on Windows.</span></span> <span data-ttu-id="88361-109">Toevoegen van CMake toohello pad voor de huidige gebruiker ten minste Hallo wanneer u vraagt Hallo-installatieprogramma.</span><span class="sxs-lookup"><span data-stu-id="88361-109">Add CMake toohello PATH for at least hello current user when hello installer prompts you.</span></span>

1. <span data-ttu-id="88361-110">Installeer [Python 2.7](https://www.python.org/downloads/release/python-27).</span><span class="sxs-lookup"><span data-stu-id="88361-110">Install [Python 2.7](https://www.python.org/downloads/release/python-27).</span></span> <span data-ttu-id="88361-111">Zorg ervoor dat u toevoegt Python tooyour `PATH` omgevingsvariabele in **Configuratiescherm -> systeem -> Advanced systeeminstellingen -> omgevingsvariabelen**.</span><span class="sxs-lookup"><span data-stu-id="88361-111">Make sure you add Python tooyour `PATH` environment variable in **Control Panel -> System -> Advanced system settings -> Environment Variables**.</span></span>

1. <span data-ttu-id="88361-112">Voer bij een opdrachtprompt Hallo opdracht tooclone hello Azure IoT rand GitHub-opslagplaats tooyour lokale computer te volgen:</span><span class="sxs-lookup"><span data-stu-id="88361-112">At a command prompt, run hello following command tooclone hello Azure IoT Edge GitHub repository tooyour local machine:</span></span>

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-toobuild-hello-sample"></a><span data-ttu-id="88361-113">Hoe toobuild voorbeeld Hallo</span><span class="sxs-lookup"><span data-stu-id="88361-113">How toobuild hello sample</span></span>

<span data-ttu-id="88361-114">U kunt nu opbouwen Hallo IoT rand runtime en voorbeelden op uw lokale machine:</span><span class="sxs-lookup"><span data-stu-id="88361-114">You can now build hello IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="88361-115">Open een **opdrachtprompt voor ontwikkelaars voor VS 2015** of **opdrachtprompt voor ontwikkelaars voor VS 2017** opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="88361-115">Open a **Developer Command Prompt for VS 2015** or **Developer Command Prompt for VS 2017** command prompt.</span></span>

1. <span data-ttu-id="88361-116">Navigeer toohello hoofdmap in de lokale kopie van Hallo **iot-edge** opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="88361-116">Navigate toohello root folder in your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="88361-117">Voer het build-script als volgt:</span><span class="sxs-lookup"><span data-stu-id="88361-117">Run the build script as follows:</span></span>

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

<span data-ttu-id="88361-118">Dit script maakt een bestand van Visual Studio-oplossing en bouwt Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="88361-118">This script creates a Visual Studio solution file and builds hello solution.</span></span> <span data-ttu-id="88361-119">U vindt Hallo Visual Studio-oplossing in Hallo **bouwen** map in het lokale exemplaar van Hallo **iot-edge** opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="88361-119">You can find hello Visual Studio solution in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="88361-120">Als u wilt dat toobuild en Hallo eenheidstests uitvoeren, toevoegen Hallo `--run-unittests` parameter.</span><span class="sxs-lookup"><span data-stu-id="88361-120">If you want toobuild and run hello unit tests, add hello `--run-unittests` parameter.</span></span> <span data-ttu-id="88361-121">Als u wilt dat toobuild en Hallo end tooend tests uitvoeren, toevoegen Hallo `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="88361-121">If you want toobuild and run hello end tooend tests, add hello `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="88361-122">Telkens wanneer u Hallo uitvoert **build.cmd** -script wordt verwijderd en vervolgens opnieuw gemaakt Hallo **bouwen** map in de hoofdmap Hallo van uw lokale exemplaar van Hallo **iot-edge** opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="88361-122">Every time you run hello **build.cmd** script, it deletes and then recreates hello **build** folder in hello root folder of your local copy of hello **iot-edge** repository.</span></span>
