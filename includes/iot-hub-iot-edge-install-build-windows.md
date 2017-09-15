## <a name="install-the-prerequisites"></a><span data-ttu-id="1b9c8-101">De vereiste software installeren</span><span class="sxs-lookup"><span data-stu-id="1b9c8-101">Install the prerequisites</span></span>

1. <span data-ttu-id="1b9c8-102">Installeer [Visual Studio 2015 of 2017](https://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="1b9c8-102">Install [Visual Studio 2015 or 2017](https://www.visualstudio.com).</span></span> <span data-ttu-id="1b9c8-103">U kunt de editie free-Community gebruiken als u voldoet aan de licentievereisten.</span><span class="sxs-lookup"><span data-stu-id="1b9c8-103">You can use the free Community Edition if you meet the licensing requirements.</span></span> <span data-ttu-id="1b9c8-104">Zorg dat u Visual C++ en NuGet Package Manager bevatten.</span><span class="sxs-lookup"><span data-stu-id="1b9c8-104">Be sure to include Visual C++ and NuGet Package Manager.</span></span>

1. <span data-ttu-id="1b9c8-105">Installeer [git](http://www.git-scm.com) en zorg ervoor dat u kunt git.exe uitvoeren vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="1b9c8-105">Install [git](http://www.git-scm.com) and make sure you can run git.exe from the command line.</span></span>

1. <span data-ttu-id="1b9c8-106">Installeer [CMake](https://cmake.org/download/) en zorg ervoor dat u kunt cmake.exe uitvoeren vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="1b9c8-106">Install [CMake](https://cmake.org/download/) and make sure you can run cmake.exe from the command line.</span></span> <span data-ttu-id="1b9c8-107">CMake versie 3.7.2 of later wordt aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="1b9c8-107">CMake version 3.7.2 or later is recommended.</span></span> <span data-ttu-id="1b9c8-108">De **.msi** installatieprogramma is de eenvoudigste optie in Windows.</span><span class="sxs-lookup"><span data-stu-id="1b9c8-108">The **.msi** installer is the easiest option on Windows.</span></span> <span data-ttu-id="1b9c8-109">Voeg ten minste CMake toe aan het pad voor de huidige gebruiker wanneer het installatieprogramma wordt u gevraagd.</span><span class="sxs-lookup"><span data-stu-id="1b9c8-109">Add CMake to the PATH for at least the current user when the installer prompts you.</span></span>

1. <span data-ttu-id="1b9c8-110">Installeer [Python 2.7](https://www.python.org/downloads/release/python-27).</span><span class="sxs-lookup"><span data-stu-id="1b9c8-110">Install [Python 2.7](https://www.python.org/downloads/release/python-27).</span></span> <span data-ttu-id="1b9c8-111">Zorg ervoor dat u bij het toevoegen van Python die moet worden uw `PATH` omgevingsvariabele in **Configuratiescherm -> systeem -> Advanced systeeminstellingen -> omgevingsvariabelen**.</span><span class="sxs-lookup"><span data-stu-id="1b9c8-111">Make sure you add Python to your `PATH` environment variable in **Control Panel -> System -> Advanced system settings -> Environment Variables**.</span></span>

1. <span data-ttu-id="1b9c8-112">Voer bij een opdrachtprompt de volgende opdracht voor het klonen van de Azure IoT rand GitHub-opslagplaats met uw lokale machine:</span><span class="sxs-lookup"><span data-stu-id="1b9c8-112">At a command prompt, run the following command to clone the Azure IoT Edge GitHub repository to your local machine:</span></span>

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-to-build-the-sample"></a><span data-ttu-id="1b9c8-113">Het voorbeeld maken</span><span class="sxs-lookup"><span data-stu-id="1b9c8-113">How to build the sample</span></span>

<span data-ttu-id="1b9c8-114">Nu kunt u de rand van de IoT-runtime en voorbeelden bouwen op uw lokale machine:</span><span class="sxs-lookup"><span data-stu-id="1b9c8-114">You can now build the IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="1b9c8-115">Open een **opdrachtprompt voor ontwikkelaars voor VS 2015** of **opdrachtprompt voor ontwikkelaars voor VS 2017** opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="1b9c8-115">Open a **Developer Command Prompt for VS 2015** or **Developer Command Prompt for VS 2017** command prompt.</span></span>

1. <span data-ttu-id="1b9c8-116">Navigeer naar de hoofdmap van uw lokale exemplaar van de **iot-edge**-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="1b9c8-116">Navigate to the root folder in your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="1b9c8-117">Voer het build-script als volgt:</span><span class="sxs-lookup"><span data-stu-id="1b9c8-117">Run the build script as follows:</span></span>

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

<span data-ttu-id="1b9c8-118">Dit script maakt een bestand van Visual Studio-oplossing en de oplossing is gebaseerd.</span><span class="sxs-lookup"><span data-stu-id="1b9c8-118">This script creates a Visual Studio solution file and builds the solution.</span></span> <span data-ttu-id="1b9c8-119">U vindt de Visual Studio-oplossing in de **bouwen** map in de lokale kopie van de **iot-edge** opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="1b9c8-119">You can find the Visual Studio solution in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="1b9c8-120">Als u wilt bouwen en de eenheidstests uitvoeren, voegt de `--run-unittests` parameter.</span><span class="sxs-lookup"><span data-stu-id="1b9c8-120">If you want to build and run the unit tests, add the `--run-unittests` parameter.</span></span> <span data-ttu-id="1b9c8-121">Als u wilt bouwen en de end-to-end-tests uitvoeren, voegt de `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="1b9c8-121">If you want to build and run the end to end tests, add the `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="1b9c8-122">Telkens wanneer u uitvoert het **build.cmd** script, op het worden verwijderd en vervolgens opnieuw de **bouwen** map in de hoofdmap van uw lokale exemplaar van de **iot-edge** opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="1b9c8-122">Every time you run the **build.cmd** script, it deletes and then recreates the **build** folder in the root folder of your local copy of the **iot-edge** repository.</span></span>