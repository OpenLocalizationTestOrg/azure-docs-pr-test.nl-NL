## <a name="install-hello-prerequisites"></a><span data-ttu-id="22a27-101">Hallo vereisten installeren</span><span class="sxs-lookup"><span data-stu-id="22a27-101">Install hello prerequisites</span></span>

<span data-ttu-id="22a27-102">Hallo stappen in deze zelfstudie wordt ervan uitgegaan dat u Ubuntu Linux wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="22a27-102">hello steps in this tutorial assume you are running Ubuntu Linux.</span></span>

<span data-ttu-id="22a27-103">Open van een shell en Voer Hallo opdrachten tooinstall Hallo vereiste pakketten te volgen:</span><span class="sxs-lookup"><span data-stu-id="22a27-103">Open a shell and run hello following commands tooinstall hello prerequisite packages:</span></span>

```bash
sudo apt-get update
sudo apt-get install curl build-essential libcurl4-openssl-dev git cmake libssl-dev uuid-dev valgrind libglib2.0-dev libtool autoconf
```

<span data-ttu-id="22a27-104">Hallo-shell, start Hallo opdracht tooclone hello Azure IoT rand GitHub-opslagplaats tooyour lokale computer te volgen:</span><span class="sxs-lookup"><span data-stu-id="22a27-104">In hello shell, run hello following command tooclone hello Azure IoT Edge GitHub repository tooyour local machine:</span></span>

```bash
git clone https://github.com/Azure/iot-edge.git
```

## <a name="how-toobuild-hello-sample"></a><span data-ttu-id="22a27-105">Hoe toobuild voorbeeld Hallo</span><span class="sxs-lookup"><span data-stu-id="22a27-105">How toobuild hello sample</span></span>

<span data-ttu-id="22a27-106">U kunt nu opbouwen Hallo IoT rand runtime en voorbeelden op uw lokale machine:</span><span class="sxs-lookup"><span data-stu-id="22a27-106">You can now build hello IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="22a27-107">Open een shell.</span><span class="sxs-lookup"><span data-stu-id="22a27-107">Open a shell.</span></span>

1. <span data-ttu-id="22a27-108">Navigeer toohello hoofdmap in de lokale kopie van Hallo **iot-edge** opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="22a27-108">Navigate toohello root folder in your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="22a27-109">Voer het build-script als volgt:</span><span class="sxs-lookup"><span data-stu-id="22a27-109">Run the build script as follows:</span></span>

    ```sh
    tools/build.sh --disable-native-remote-modules
    ```

<span data-ttu-id="22a27-110">Dit script maakt gebruik van de **cmake** hulpprogramma toocreate een map met de naam **bouwen** Hallo hoofdmap van het lokale exemplaar van de **iot-edge** opslagplaats en een make-bestand te genereren.</span><span class="sxs-lookup"><span data-stu-id="22a27-110">This script uses the **cmake** utility toocreate a folder called **build** in hello root folder of your local copy of the **iot-edge** repository and generate a makefile.</span></span> <span data-ttu-id="22a27-111">Hallo script maakt vervolgens Hallo-oplossing, eenheidstests en end tooend tests overslaan.</span><span class="sxs-lookup"><span data-stu-id="22a27-111">hello script then builds hello solution, skipping unit tests and end tooend tests.</span></span> <span data-ttu-id="22a27-112">Als u wilt dat toobuild en Hallo eenheidstests uitvoeren, toevoegen Hallo `--run-unittests` parameter.</span><span class="sxs-lookup"><span data-stu-id="22a27-112">If you want toobuild and run hello unit tests, add hello `--run-unittests` parameter.</span></span> <span data-ttu-id="22a27-113">Als u wilt dat toobuild en Hallo end tooend tests uitvoeren, toevoegen Hallo `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="22a27-113">If you want toobuild and run hello end tooend tests, add hello `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="22a27-114">Telkens wanneer u Hallo uitvoert **build.sh** -script wordt verwijderd en vervolgens opnieuw gemaakt Hallo **bouwen** map in de hoofdmap Hallo van uw lokale exemplaar van Hallo **iot-edge** opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="22a27-114">Every time you run hello **build.sh** script, it deletes and then recreates hello **build** folder in hello root folder of your local copy of hello **iot-edge** repository.</span></span>
