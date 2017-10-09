## <a name="overview"></a>Overzicht

In deze zelfstudie maakt uitvoeren u Hallo stappen:

- Implementeer een exemplaar van Hallo externe controle vooraf geconfigureerde oplossing tooyour Azure-abonnement. Deze stap implementeert automatisch en meerdere Azure-services configureert.
- Uw apparaat toocommunicate met uw computer en het Hallo-oplossing voor externe controle instellen.
- Bijwerken van Hallo voorbeeld apparaat code tooconnect toohello oplossing voor externe controle en gesimuleerde telemetrie die u op het dashboard van de oplossing Hallo weergeven kunt verzenden.

## <a name="prerequisites"></a>Vereisten

toocomplete in deze zelfstudie, moet u een actief Azure-abonnement.

> [!NOTE]
> Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure][lnk-free-trial] voor meer informatie.

### <a name="required-software"></a>Vereiste software

SSH-client moet u op uw computer tooenable u tooremotely access Hallo-opdracht regel op Hallo frambozen Pi.

- Windows bevat geen een SSH-client. Wordt u aangeraden [PuTTY](http://www.putty.org/).
- De meeste Linux-distributies en Mac OS bevatten Hallo SSH-opdrachtregelprogramma. Zie voor meer informatie [SSH met behulp van Linux- of Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).

### <a name="required-hardware"></a>Vereiste hardware

Een desktopcomputer tooenable u tooconnect op afstand toohello opdracht regel op Hallo frambozen Pi.

[Microsoft IoT Starter Kit voor frambozen Pi 3] [ lnk-starter-kits] of gelijkwaardige onderdelen. In deze zelfstudie wordt de volgende items uit de Hallo kit Hallo:

- Raspberry Pi 3
- MicroSD-kaart (met NOOBS)
- Een Mini USB-kabel
- Een Ethernet-kabel

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/