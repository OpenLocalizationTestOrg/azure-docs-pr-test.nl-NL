## <a name="build-iot-edge"></a>IoT-rand bouwen

Deze zelfstudie maakt gebruik van aangepaste IoT rand modules toocommunicate Hello vooraf geconfigureerde oplossing voor externe controle. Daarom moet u toobuild Hallo IoT Edge-modules uit aangepaste broncode. Hallo uit te voeren wordt beschreven hoe tooinstall IoT rand en build Hallo aangepaste module voor IoT rand.

### <a name="install-iot-edge"></a>IoT-rand installeren

Hallo volgende stappen wordt beschreven hoe tooinstall Hallo IoT rand software op Hallo Intel NUC vooraf gecompileerd:

1. Hallo vereist smart pakket opslagplaatsen door het uitvoeren van de volgende opdrachten op Hallo Intel NUC Hallo configureren:

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    Voer `y` wanneer Hallo-opdracht wordt u gevraagd te**dit kanaal opnemen?**.

1. Hallo smart Pakketbeheer bijwerken door het uitvoeren van de volgende opdracht Hallo:

    ```bash
    smart update
    ```

1. Hello Azure IoT rand pakket installeren door het uitvoeren van de volgende opdracht Hallo:

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. Hallo installatie controleren door actieve Hallo "Hallo wereld" voorbeeld. Dit voorbeeld schrijft een hello world toohello log.txT berichtbestand elke vijf seconden. Hallo volgende opdrachten uitgevoerd Hallo "Hallo wereld" voorbeeld:

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    Alle **ongeldig argument** wanneer u stopt met het voorbeeld Hallo-berichten.

    Hallo opdracht tooview Hallo inhoud van het logboekbestand Hallo volgende gebruiken:

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a>Problemen oplossen

Als u de foutmelding Hallo 'geen pakket biedt util-linux-dev', Hallo Intel NUC opnieuw op te starten.
