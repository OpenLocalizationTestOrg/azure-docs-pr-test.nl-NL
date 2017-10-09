## <a name="install-hello-prerequisites"></a>Hallo vereisten installeren

1. Installeer [Visual Studio 2015 of 2017](https://www.visualstudio.com). U kunt Hallo Community Edition gratis als u voldoen aan de licentievereisten Hallo. Worden ervoor tooinclude Visual C++ en NuGet Package Manager.

1. Installeer [git](http://www.git-scm.com) en zorg ervoor dat u kunt git.exe uitvoeren vanaf de opdrachtregel Hallo.

1. Installeer [CMake](https://cmake.org/download/) en zorg ervoor dat u kunt cmake.exe uitvoeren vanaf de opdrachtregel Hallo. CMake versie 3.7.2 of later wordt aanbevolen. Hallo **.msi** installatieprogramma is de eenvoudigste optie Hallo in Windows. Toevoegen van CMake toohello pad voor de huidige gebruiker ten minste Hallo wanneer u vraagt Hallo-installatieprogramma.

1. Installeer [Python 2.7](https://www.python.org/downloads/release/python-27). Zorg ervoor dat u toevoegt Python tooyour `PATH` omgevingsvariabele in **Configuratiescherm -> systeem -> Advanced systeeminstellingen -> omgevingsvariabelen**.

1. Voer bij een opdrachtprompt Hallo opdracht tooclone hello Azure IoT rand GitHub-opslagplaats tooyour lokale computer te volgen:

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-toobuild-hello-sample"></a>Hoe toobuild voorbeeld Hallo

U kunt nu opbouwen Hallo IoT rand runtime en voorbeelden op uw lokale machine:

1. Open een **opdrachtprompt voor ontwikkelaars voor VS 2015** of **opdrachtprompt voor ontwikkelaars voor VS 2017** opdrachtprompt.

1. Navigeer toohello hoofdmap in de lokale kopie van Hallo **iot-edge** opslagplaats.

1. Voer het build-script als volgt:

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

Dit script maakt een bestand van Visual Studio-oplossing en bouwt Hallo-oplossing. U vindt Hallo Visual Studio-oplossing in Hallo **bouwen** map in het lokale exemplaar van Hallo **iot-edge** opslagplaats. Als u wilt dat toobuild en Hallo eenheidstests uitvoeren, toevoegen Hallo `--run-unittests` parameter. Als u wilt dat toobuild en Hallo end tooend tests uitvoeren, toevoegen Hallo `--run-e2e-tests`.

> [!NOTE]
> Telkens wanneer u Hallo uitvoert **build.cmd** -script wordt verwijderd en vervolgens opnieuw gemaakt Hallo **bouwen** map in de hoofdmap Hallo van uw lokale exemplaar van Hallo **iot-edge** opslagplaats.
