---
title: aaaConnect een apparaat met C op mbed | Microsoft Docs
description: Hierin wordt beschreven hoe tooconnect een apparaat toohello Azure IoT Suite vooraf geconfigureerde oplossing voor externe controle met behulp van een toepassing die is geschreven in C uitvoering op een apparaat mbed.
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 9551075e-dcf9-488f-943e-d0eb0e6260be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ROBOTS: NOINDEX
ms.openlocfilehash: dcd1e74635e8dec678a59bff060a73f7cfabd124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-mbed"></a>Verbinding maken met uw apparaat toohello vooraf geconfigureerde oplossing (mbed) voor externe controle

## <a name="scenario-overview"></a>Overzicht van scenario's
In dit scenario die u maakt een apparaat dat verzendt telemetrie toohello externe controle te volgen Hallo [vooraf geconfigureerde oplossing][lnk-what-are-preconfig-solutions]:

* Externe temperatuur
* Interne temperatuur
* Vochtigheid

Eenvoud, Hallo-code op Hallo apparaat genereert voorbeeldwaarden, maar we raden u tooextend Hallo voorbeeld door de echte sensoren tooyour apparaat verbinding te maken en verzenden van telemetrie echte.

Hallo-apparaat is ook kunnen toorespond toomethods aangeroepen vanuit het dashboard van de oplossing Hallo en eigenschapswaarden ingesteld in het dashboard van de oplossing Hallo gewenst.

toocomplete in deze zelfstudie, moet u een actief Azure-account. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure][lnk-free-trial] voor meer informatie.

## <a name="before-you-start"></a>Voordat u begint
Voordat u code voor het apparaat gaat schrijven, moet u de vooraf geconfigureerde oplossing voor externe controle inrichten en een nieuw aangepast apparaat in die oplossing inrichten.

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a>De vooraf geconfigureerde oplossing voor externe controle inrichten
Hallo-apparaat in deze zelfstudie hebt u verzendt gegevens tooan exemplaar van Hallo [externe controle] [ lnk-remote-monitoring] vooraf geconfigureerde oplossing. Als u al vooraf geconfigureerde oplossing in uw Azure-account voor externe controle Hallo nog niet hebt ingericht, gebruikt u Hallo stappen te volgen:

1. Op Hallo <https://www.azureiotsuite.com/> pagina, klikt u op  **+**  toocreate een oplossing.
2. Klik op **Selecteer** op Hallo **externe controle** toocreate van uw oplossing het deelvenster.
3. Op Hallo **maken oplossing voor externe controle** pagina, voert u een **oplossingsnaam** van uw keuze, selecteer Hallo **regio** u wilt toodeploy naar en selecteer hello Azure abonnement toowant toouse. Klik vervolgens op **Oplossing maken**.
4. Wacht totdat het Hallo inrichtingsproces is voltooid.

> [!WARNING]
> Hallo vooraf geconfigureerde oplossingen gebruiken factureerbare Azure-services. Zorg ervoor dat tooremove Hallo vooraf geconfigureerde oplossing van uw abonnement wanneer u klaar bent met het tooavoid eventuele onnodige kosten. U kunt een vooraf geconfigureerde oplossing volledig verwijderen uit uw abonnement via Hallo <https://www.azureiotsuite.com/> pagina.
> 
> 

Wanneer Hallo proces voor het Hallo-oplossing voor externe controle inrichten is voltooid, klikt u op **starten** tooopen Hallo dashboard van de oplossing in uw browser.

![Dashboard van de oplossing][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a>Uw apparaat bij Hallo oplossing voor externe controle inrichten
> [!NOTE]
> Als u al een apparaat in uw oplossing hebt ingericht, kunt u deze stap overslaan. Bij het maken van de client-toepassing hello moet u tooknow Hallo apparaat referenties.
> 
> 

Voor een apparaat tooconnect toohello vooraf geconfigureerde oplossing, deze moet zelfidentificatie tooIoT Hub met geldige referenties. U kunt Hallo apparaat referenties ophalen uit Hallo oplossing dashboard. Hallo apparaat referenties in uw clienttoepassing verderop in deze zelfstudie te nemen.

de oplossing voor externe controle van een apparaat-tooyour tooadd, volledige hello te volgen stappen in Hallo oplossing dashboard:

1. In Hallo linkerbenedenhoek van Hallo dashboard, klikt u op **een apparaat toevoegt**.
   
   ![Een apparaat toevoegen][1]
2. In Hallo **aangepast apparaat** -scherm, klikt u op **nieuwe toevoegen**.
   
   ![Een aangepast apparaat toevoegen][2]
3. Kies **Laat mij mijn eigen apparaat-id definiëren**. Voer een apparaat-ID zoals **mydevice**, klikt u op **cheque-ID** tooverify die naam niet al in gebruik en klik vervolgens op **maken** tooprovision Hallo apparaat.
   
   ![Apparaat-id toevoegen][3]
4. Een opmerking Hallo-apparaat referenties (apparaat-ID, hostnaam van de IoT-Hub en apparaatsleutel) maken. De clienttoepassing moet deze waarden tooconnect toohello oplossing voor externe controle. Klik vervolgens op **Gereed**.
   
    ![Apparaatreferenties weergeven][4]
5. Selecteer uw apparaat in de lijst met apparaten in het dashboard van de oplossing Hallo Hallo. Klik op Hallo **Apparaatdetails** -scherm, klikt u op **apparaat inschakelen**. Hallo-status van uw apparaat is nu **met**. Hallo-oplossing voor externe controle kan nu telemetrie van uw apparaat wordt ontvangen en methoden niet aanroepen voor het Hallo-apparaat.

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-hello-c-sample-solution"></a>Bouwen en uitvoeren van Voorbeeldoplossing Hallo C

Hallo volgende instructies beschrijven Hallo stappen voor het verbinden van een [mbed ingeschakeld Freescale FRDM-K64F] [ lnk-mbed-home] apparaat toohello oplossing voor externe controle.

### <a name="connect-hello-mbed-device-tooyour-network-and-desktop-machine"></a>Verbinding maken met de Hallo mbed apparaat tooyour netwerk- en computer

1. Hallo mbed apparaat tooyour netwerk met behulp van een Ethernet-kabel verbinden. Deze stap is nodig omdat de voorbeeldtoepassing Hallo hiervoor is internettoegang vereist.

1. Zie [aan de slag met mbed] [ lnk-mbed-getstarted] tooconnect uw mbed apparaat tooyour bureaublad PC.

1. Als uw PC kan Windows wordt uitgevoerd, Zie [configuratie PC] [ lnk-mbed-pcconnect] tooconfigure seriële poort toegang tooyour mbed apparaat.

### <a name="create-an-mbed-project-and-import-hello-sample-code"></a>Maken van een project mbed en voorbeeldcode Hallo importeren

Volg deze stappen tooadd sommige voorbeeldproject code tooan mbed. U Hallo externe controle starter project importeren en wijzig vervolgens Hallo project toouse hello MQTT protocol in plaats van Hallo AMQP-protocol. Op dit moment moet u toouse hello MQTT protocol toouse Hallo beheerfuncties voor apparaten van IoT Hub.

1. Ga in uw webbrowser toohello mbed.org [developer site](https://developer.mbed.org/). Als u dit nog niet hebt aangemeld, ziet u een optie toocreate een account (het is gratis). Anders kunt u aanmelden met referenties van uw account. Klik vervolgens op **Compiler** in Hallo rechterbovenhoek van Hallo pagina. Deze actie biedt u toohello *werkruimte* interface.

1. Zorg ervoor dat Hallo hardwareplatform dat u gebruikt in Hallo rechterbovenhoek van Hallo-venster wordt weergegeven of klik op Hallo-pictogram in Hallo rechterhoek tooselect uw hardwareplatform.

1. Klik op **importeren** in het hoofdmenu Hallo. Klik vervolgens op **Klik hier tooimport van URL**.
   
    ![Start importeren toombed werkruimte][6]

1. Voer in het pop-upvenster hello, Hallo-koppeling voor Hallo voorbeeld code https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ en klik vervolgens op **importeren**.
   
    ![Voorbeeld code toombed werkruimte importeren][7]

1. U kunt zien in Hallo mbed compiler venster dat dit project importeren ook verschillende bibliotheken invoer. Sommige worden geleverd en beheerd door hello Azure IoT-team ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), terwijl andere derden beschikbare bibliotheken in Hallo mbed bibliotheken catalogus.
   
    ![Weergave mbed project][8]

1. In Hallo **programma werkruimte**, klik met de rechtermuisknop Hallo **iothub\_amqp\_transport** bibliotheek, klikt u op **verwijderen**, en klik vervolgens op **OK** tooconfirm.

1. In Hallo **programma werkruimte**, klik met de rechtermuisknop Hallo **azure\_amqp\_c** bibliotheek, klikt u op **verwijderen**, en klik vervolgens op **OK**  tooconfirm.

1. Met de rechtermuisknop op Hallo **remote_monitoring** -project in Hallo **programma werkruimte**, selecteer **bibliotheek importeren**, selecteer daarna **van URL**.
   
    ![Starten van de werkruimte bibliotheek import-toombed][6]

1. Voer in het pop-upvenster hello, Hallo-koppeling voor Hallo MQTT transport bibliotheek https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport / klikt u vervolgens op **importeren**.
   
    ![De werkruimte toombed bibliotheek importeren][12]

1. Herhaal Hallo vorige stap tooadd hello MQTT-bibliotheek van https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c /.

1. Uw werkruimte is nu ziet eruit als Hallo volgende:

    ![Mbed-werkruimte weergeven][13]

1. Open Hallo externe\_monitoring\remote_monitoring.c bestands- en vervang Hallo bestaande `#include` instructies met Hallo code te volgen:

    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"

    #ifdef MBED_BUILD_TIMESTAMP
    #include "certs.h"
    #endif // MBED_BUILD_TIMESTAMP
    ```
1. Verwijderen van alle Hallo resterende code in externe Hallo\_monitoring\remote\_monitoring.c-bestand.

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a>Bouwen en uitvoeren van Hallo-voorbeeld

Toevoegen van code tooinvoke Hallo **externe\_bewaking\_uitvoeren** werken en vervolgens toepassing bouwen en uitvoeren Hallo apparaat.

1. Toevoegen een **belangrijkste** functie met de volgende code achter Hallo Hallo externe\_monitoring.c bestand tooinvoke hello **externe\_bewaking\_uitvoeren** functie:
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. Klik op **compileren** toobuild Hallo programma. U kunt veilig negeren van waarschuwingen, maar als Hallo build fouten genereert corrigeren voordat u doorgaat.

1. Als Hallo build geslaagd is, wordt Hallo mbed compiler website genereert u een .bin-bestand met de naam van uw project Hallo en downloadt u de lokale computer tooyour. Hallo .bin-bestand toohello apparaat kopiëren. Hallo .bin-bestand toohello apparaat opslaan Hallo apparaat toorestart veroorzaakt en opgenomen in het .bin-bestand Hallo Hallo-programma uitvoeren. U kunt handmatig opnieuw opstarten Hallo programma op elk gewenst moment Hallo opnieuw instellen door knop te drukken op Hallo mbed apparaat.

1. Verbinding maken met behulp van een SSH-client-toepassing, zoals PuTTY toohello-apparaat. U kunt de seriële poort Hallo die uw apparaat wordt gebruikt door het controleren van Windows-Apparaatbeheer bepalen.
   
    ![][11]

1. Klik in de PuTTY, op Hallo **seriële** verbindingstype. Hallo-apparaat is doorgaans verbinding maakt met 9600 baud, dus voer 9600 in Hallo **snelheid** vak. Klik vervolgens op **Open**.

1. Hallo-programma wordt uitgevoerd. Mogelijk hebt u tooreset Hallo Mededelingenbord (druk op CTRL + Break of druk op Hallo mededelingenbord herstelknop) als Hallo programma niet automatisch wordt gestart wanneer u verbinding maakt.
   
    ![][10]

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[6]: ./media/iot-suite-connecting-devices-mbed/mbed1.png
[7]: ./media/iot-suite-connecting-devices-mbed/mbed2a.png
[8]: ./media/iot-suite-connecting-devices-mbed/mbed3a.png
[10]: ./media/iot-suite-connecting-devices-mbed/putty.png
[11]: ./media/iot-suite-connecting-devices-mbed/mbed6.png
[12]: ./media/iot-suite-connecting-devices-mbed/mbed7.png
[13]: ./media/iot-suite-connecting-devices-mbed/mbed8.png

[lnk-mbed-home]: https://developer.mbed.org/platforms/FRDM-K64F/
[lnk-mbed-getstarted]: https://developer.mbed.org/platforms/FRDM-K64F/#getting-started-with-mbed
[lnk-mbed-pcconnect]: https://developer.mbed.org/platforms/FRDM-K64F/#pc-configuration
