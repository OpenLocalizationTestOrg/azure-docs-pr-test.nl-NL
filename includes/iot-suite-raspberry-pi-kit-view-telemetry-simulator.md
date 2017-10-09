## <a name="view-hello-telemetry"></a>Hallo telemetrie van paginaweergaven

Hallo frambozen Pi verzendt nu telemetrie toohello oplossing voor externe controle. U kunt Hallo telemetrie weergeven op Hallo oplossing dashboard. Ook kunt u berichten tooyour frambozen Pi verzenden vanuit Hallo oplossing dashboard.

- Navigeer toohello oplossing dashboard.
- Selecteer het apparaat in Hallo **apparaat tooView** vervolgkeuzelijst.
- Hallo telemetrie van Hallo frambozen Pi wordt weergegeven op Hallo-dashboard.

![Telemetrie weergegeven van Hallo frambozen Pi][img-telemetry-display]

## <a name="act-on-hello-device"></a>Reageren op Hallo-apparaat

U kunt vanuit Hallo oplossing dashboard, methoden aanroepen op uw frambozen Pi. Wanneer Hallo frambozen Pi verbinding toohello oplossing voor externe controle, stuurt informatie over deze ondersteuning biedt voor Hallo-methoden.

- Klik in het dashboard van de oplossing hello, **apparaten** toovisit hello **apparaten** pagina. Selecteer uw Pi frambozen in Hallo **lijst met apparaten**. Kies vervolgens **methoden**:

    ![Lijst met apparaten in het dashboard][img-list-devices]

- Op Hallo **methode Invoke** pagina **LightBlink** in Hallo **methode** vervolgkeuzelijst.

- Kies **InvokeMethod**. Hallo simulator een bericht in de console Hallo op Hallo frambozen Pi afgedrukt. Hallo-app op Hallo frambozen Pi verzendt een dashboard van de bevestiging terug toohello oplossing:

    ![Overzicht van de methode weergeven][img-method-history]

- Kunt u schakelen Hallo LED in- en uitschakelen met behulp van Hallo **ChangeLightStatus** methode met een **LightStatusValue** instellen te**1** voor op of **0** voor uitschakelen.

> [!WARNING]
> Als u Hallo oplossing uitgevoerd in uw Azure-account voor externe controle laat, wordt u gefactureerd voor Hallo keer die wordt uitgevoerd. Zie voor meer informatie over het verminderen van verbruik tijdens het Hallo voor externe controle van de oplossing wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config]. Hallo vooraf geconfigureerde oplossing uit uw Azure-account verwijderen wanneer u klaar bent met het gebruik van maken.


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md