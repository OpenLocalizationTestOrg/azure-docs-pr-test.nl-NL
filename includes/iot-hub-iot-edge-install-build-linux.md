## <a name="install-hello-prerequisites"></a>Hallo vereisten installeren

Hallo stappen in deze zelfstudie wordt ervan uitgegaan dat u Ubuntu Linux wordt uitgevoerd.

Open van een shell en Voer Hallo opdrachten tooinstall Hallo vereiste pakketten te volgen:

```bash
sudo apt-get update
sudo apt-get install curl build-essential libcurl4-openssl-dev git cmake libssl-dev uuid-dev valgrind libglib2.0-dev libtool autoconf
```

Hallo-shell, start Hallo opdracht tooclone hello Azure IoT rand GitHub-opslagplaats tooyour lokale computer te volgen:

```bash
git clone https://github.com/Azure/iot-edge.git
```

## <a name="how-toobuild-hello-sample"></a>Hoe toobuild voorbeeld Hallo

U kunt nu opbouwen Hallo IoT rand runtime en voorbeelden op uw lokale machine:

1. Open een shell.

1. Navigeer toohello hoofdmap in de lokale kopie van Hallo **iot-edge** opslagplaats.

1. Voer het build-script als volgt:

    ```sh
    tools/build.sh --disable-native-remote-modules
    ```

Dit script maakt gebruik van de **cmake** hulpprogramma toocreate een map met de naam **bouwen** Hallo hoofdmap van het lokale exemplaar van de **iot-edge** opslagplaats en een make-bestand te genereren. Hallo script maakt vervolgens Hallo-oplossing, eenheidstests en end tooend tests overslaan. Als u wilt dat toobuild en Hallo eenheidstests uitvoeren, toevoegen Hallo `--run-unittests` parameter. Als u wilt dat toobuild en Hallo end tooend tests uitvoeren, toevoegen Hallo `--run-e2e-tests`.

> [!NOTE]
> Telkens wanneer u Hallo uitvoert **build.sh** -script wordt verwijderd en vervolgens opnieuw gemaakt Hallo **bouwen** map in de hoofdmap Hallo van uw lokale exemplaar van Hallo **iot-edge** opslagplaats.
