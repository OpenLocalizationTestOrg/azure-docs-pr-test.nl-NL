## <a name="configure-hello-nodejs-simulated-device"></a>Hallo Node.js gesimuleerde apparaat configureren
1. Klik op Hallo dashboard externe controle, **+ een apparaat toevoegt** en voeg vervolgens een *aangepast apparaat*. Noteer Hallo IoT Hub hostnaam, apparaat-id en apparaatsleutel. U moet deze verderop in deze zelfstudie als u Hallo remote_monitoring.js device-clienttoepassing voorbereiden.
2. Zorg dat Node.js-versie 0.12.x of hoger is geïnstalleerd op uw ontwikkelcomputer. Voer `node --version` achter de opdrachtprompt of in een shell toocheck Hallo-versie. Zie voor meer informatie over het gebruik van een pakket manager tooinstall Node.js op Linux [Node.js installeren via Pakketbeheer][node-linux].
3. Wanneer u Node.js hebt geïnstalleerd, de meest recente versie Hallo Hallo klonen [azure-iot-sdk-knooppunt] [ lnk-github-repo] opslagplaats tooyour ontwikkelcomputer. Gebruik altijd Hallo **master** vertakking voor de meest recente versie Hallo Hallo-bibliotheken en voorbeelden.
4. In uw lokale exemplaar van Hallo [azure-iot-sdk-knooppunt] [ lnk-github-repo] opslagplaats, kopie Hallo volgende twee bestanden uit Hallo apparaat-knooppunt-voorbeelden tooan lege map op uw ontwikkelcomputer:
   
   * Packages.JSON
   * remote_monitoring.js
5. Hallo remote_monitoring.js bestand openen en zoekt u Hallo variabeledefinitie volgt:
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. Vervang **[IoT Hub apparaat-verbindingsreeks]** met de verbindingsreeks van uw apparaat. Hallo waarden gebruiken voor uw IoT-Hub hostnaam, het apparaat-id en de apparaatsleutel die u een genoteerd in stap 1 hebt. Een verbindingsreeks apparaat heeft Hallo volgende indeling:
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    Als uw IoT Hub-hostnaam **contoso** en uw apparaat-id is **mydevice**, de verbindingsreeks ziet eruit als Hallo codefragment te volgen:
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. Hallo-bestand opslaan. Hallo volgende opdrachten in een shell of opdrachtprompt in Hallo-map met deze bestanden tooinstall hello-pakketten voor nodig zijn uitgevoerd en voer vervolgens de voorbeeldtoepassing Hallo:
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a>Houd rekening met dynamische telemetrie in actie
Hallo-dashboard ziet Hallo temperatuur en vochtigheid telemetrie van Hallo bestaande gesimuleerde apparaten:

![Hallo standaarddashboard][image1]

Als u Hallo Node.js gesimuleerd apparaat die hebt uitgevoerd in de vorige sectie Hallo selecteert, ziet u temperatuur en vochtigheid externe temperatuur telemetrie:

![Externe temperatuur toohello dashboard toevoegen][image2]

Hallo-oplossing voor externe controle Hallo aanvullende externe temperatuur telemetrie type detecteert automatisch en wordt toohello grafiek op Hallo dashboard toegevoegd.

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: media/iot-suite-send-external-temperature/image1.png
[image2]: media/iot-suite-send-external-temperature/image2.png