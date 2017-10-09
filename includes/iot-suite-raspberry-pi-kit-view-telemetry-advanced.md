## <a name="view-hello-telemetry"></a>Hallo telemetrie van paginaweergaven

Hallo frambozen Pi verzendt nu telemetrie toohello oplossing voor externe controle. U kunt Hallo telemetrie weergeven op Hallo oplossing dashboard. Ook kunt u berichten tooyour frambozen Pi verzenden vanuit Hallo oplossing dashboard.

- Navigeer toohello oplossing dashboard.
- Selecteer het apparaat in Hallo **apparaat tooView** vervolgkeuzelijst.
- Hallo telemetrie van Hallo frambozen Pi wordt weergegeven op Hallo-dashboard.

![Telemetrie weergegeven van Hallo frambozen Pi][img-telemetry-display]

## <a name="initiate-hello-firmware-update"></a>Hallo-firmware-update starten op

procedure Hallo firmware-update downloadt en installeert een bijgewerkte versie van Hallo device-clienttoepassing op Hallo frambozen Pi. Zie voor meer informatie over Hallo firmware updateproces Hallo beschrijving van Hallo firmware-update-patroon in [overzicht van Apparaatbeheer met IoT Hub][lnk-update-pattern].

U start Hallo firmware bijwerken door het aanroepen van een methode op Hallo-apparaat. Deze methode is asynchroon en retourneert zodra het updateproces Hallo begint. Eigenschappen toonotify Hallo oplossing Hallo apparaat gebruikt gerapporteerd over de voortgang van de update Hallo Hallo.

U kunt methoden aanroepen op uw Pi frambozen vanuit Hallo oplossing dashboard. Wanneer Hallo frambozen Pi toohello oplossing voor externe controle de eerst verbinding maakt, wordt informatie over Hallo methoden ondersteunt verzonden. 

[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-advanced/telemetry.png
[lnk-update-pattern]: ../articles/iot-hub/iot-hub-device-management-overview.md
