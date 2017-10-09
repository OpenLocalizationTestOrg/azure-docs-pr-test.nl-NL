## <a name="customize-and-extend-hello-device-management-actions"></a>Aanpassen en uitbreiden van beheeracties Hallo-apparaat

Uw IoT-oplossingen kunnen Breid Hallo gedefinieerd set apparaat management patronen of aangepaste patronen inschakelen met behulp van Hallo apparaat twin en cloud-naar-apparaat methode primitieven. Andere voorbeelden van acties voor apparaat zijn fabrieksinstellingen, firmware-update, software-update, energiebeheer, netwerk-en connectiviteit en versleuteling van gegevens.

## <a name="device-maintenance-windows"></a>Onderhoudsvensters voor apparaat

Normaal gesproken configureert u apparaten tooperform acties op een tijdstip dat onderbrekingen en uitvaltijd minimaliseert. Apparaat onderhoudsvensters zijn een veelgebruikte patroon toodefine Hallo tijd wanneer de configuratie moet worden bijgewerkt door een apparaat. Uw back-end-oplossingen kunnen Hallo gewenst eigenschappen van Hallo apparaat twin toodefine gebruiken en activeren van een beleid op uw apparaat waarmee een onderhoudsvenster. Wanneer een apparaat Hallo onderhoud-venster beleid ontvangt, kunt het Hallo-eigenschap van Hallo twin tooreport Hallo Apparaatstatus Hallo beleid gerapporteerd. Hallo back-endserver voor apps kunt vervolgens apparaat twin query's tooattest toocompliance van apparaten en elk beleid gebruiken.

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie maakt u een directe methode tootrigger extern opnieuw opstarten op een apparaat gebruikt. U gebruikte Hallo gemelde eigenschappen tooreport Hallo laatste tijd van het Hallo-apparaat opnieuw opstarten en opgevraagde Hallo apparaat twin toodiscover Hallo laatste tijd van het apparaat uit de cloud Hallo Hallo opnieuw opstarten.

toocontinue aan de slag met IoT Hub en device management patronen, zoals extern via Hallo lucht firmware-update, Zie:

[Zelfstudie: Hoe toodo een firmware bijwerken][lnk-fwupdate]

toolearn hoe tooextend uw IoT-oplossing en schema-methode aanroepen op meerdere apparaten, raadpleegt u Hallo [planning en broadcast taken] [ lnk-tutorial-jobs] zelfstudie.

aan de slag met IoT Hub toocontinue Zie [aan de slag met IoT rand][lnk-iot-edge].

[lnk-fwupdate]: ../articles/iot-hub/iot-hub-node-node-firmware-update.md
[lnk-tutorial-jobs]: ../articles/iot-hub/iot-hub-node-node-schedule-jobs.md
[lnk-iot-edge]: ../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md