---
title: aaaAzure IoT Suite en Logic Apps | Microsoft Docs
description: Een zelfstudie over het toohook van Logic Apps tooAzure IoT Suite voor bedrijfsproces.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4629a7af-56ca-4b21-a769-5fa18bc3ab07
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: corywink
ms.openlocfilehash: 6ef7311ac38f4e2ddb032cff0fb73591da5f76c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-connect-logic-app-tooyour-azure-iot-suite-remote-monitoring-preconfigured-solution"></a>Zelfstudie: Logische App tooyour Azure IoT Suite Remote Monitoring vooraf geconfigureerde oplossing verbinden
Hallo [Microsoft Azure IoT Suite] [ lnk-internetofthings] vooraf geconfigureerde oplossing voor externe controle is een uitstekende manier tooget snel de slag met een end-to-end-functieset die verklaart de IoT-oplossing. Deze zelfstudie leert u hoe tooadd logische App tooyour Microsoft Azure IoT Suite remote monitoring vooraf oplossing geconfigureerde. Deze stappen laten zien hoe u uw IoT-oplossing nog verder door verbinding te maken dit bedrijfsproces tooa kunt nemen.

*Als u een overzicht over hoe een externe controle tooprovision vooraf oplossing geconfigureerde zoekt, Zie [zelfstudie: aan de slag met vooraf geconfigureerde IoT-oplossingen Hallo][lnk-getstarted].*

Voordat u deze zelfstudie begint, moet u het volgende doen:

* Inrichten Hallo externe controle vooraf geconfigureerde oplossing in uw Azure-abonnement.
* Maken van een account SendGrid tooenable toosend een e-mailbericht uw bedrijfsproces activeert. U kunt zich aanmelden voor een gratis proefaccount op [SendGrid](https://sendgrid.com/) door te klikken op **Probeer gratis**. Nadat u hebt geregistreerd voor een gratis proefversie account, moet u toocreate een [API-sleutel](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) in SendGrid die machtigingen toosend mail verleent. Deze API-sleutel moet u later in de zelfstudie Hallo.

toocomplete in deze zelfstudie, moet u Visual Studio 2015 of Visual Studio 2017 toomodify Hallo-acties in Hallo vooraf geconfigureerde oplossing voor back-end.

Ervan uitgaande dat u al hebt ingericht uw externe controle vooraf geconfigureerde oplossing, gaat u de resourcegroep toohello voor deze oplossing in Hallo [Azure-portal][lnk-azureportal]. Hallo resourcegroep heeft Hallo dezelfde naam als hello oplossing servernaam die u hebt gekozen wanneer u uw oplossing voor externe controle ingericht. In de resourcegroep hello ziet u alle hello Azure-resources voor uw oplossing, met uitzondering van Azure Active Directory-toepassing die u in de klassieke Azure-Portal Hallo vinden kunt Hallo ingericht. Hallo volgende schermafbeelding ziet u een voorbeeld **resourcegroep** blade voor een externe controle vooraf geconfigureerde oplossing:

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

toobegin, instellen van de Hallo logic app toouse Hello vooraf geconfigureerde oplossing.

## <a name="set-up-hello-logic-app"></a>Hallo logische App instellen
1. Klik op **toevoegen** Hallo boven aan de blade met resourcegroepen in hello Azure-portal.
2. Zoeken naar **logische App**, selecteert u deze en klik vervolgens op **maken**.
3. Hallo invullen **naam** en gebruik dezelfde Hallo **abonnement** en **resourcegroep** die u hebt gebruikt bij het inrichten van uw oplossing voor externe controle. Klik op **Create**.
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. Wanneer uw implementatie is voltooid, ziet u Hallo die logische App wordt vermeld als een resource in de resourcegroep.
5. Klik op Hallo logische App toonavigate toohello logische App blade Selecteer Hallo **lege logische App** sjabloon tooopen hello **Logic Apps Designer**.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. Selecteer **aanvragen**. Deze actie geeft aan dat een inkomende HTTP-aanvraag met een specifieke JSON nettolading handelingen als een trigger opgemaakt.
7. Plak de volgende code in de aanvraag hoofdtekst JSON-Schema Hallo Hallo:
   
    ```json
    {
      "$schema": "http://json-schema.org/draft-04/schema#",
      "id": "/",
      "properties": {
        "DeviceId": {
          "id": "DeviceId",
          "type": "string"
        },
        "measuredValue": {
          "id": "measuredValue",
          "type": "integer"
        },
        "measurementName": {
          "id": "measurementName",
          "type": "string"
        }
      },
      "required": [
        "DeviceId",
        "measurementName",
        "measuredValue"
      ],
      "type": "object"
    }
    ```
   
   > [!NOTE]
   > Nadat u opslaan Hallo logische app, maar u moet eerst een actie toevoegen, kunt u Hallo-URL voor Hallo HTTP post kopiëren.
   > 
   > 
8. Klik op **+ een nieuwe stap** onder de handmatige trigger. Klik vervolgens op **een actie toevoegen**.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. Zoeken naar **SendGrid - e-mailbericht verzenden** en klik erop.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. Voer een naam voor de verbinding hello, zoals **SendGridConnection**, Voer Hallo **SendGrid-API-sleutel** u gemaakt wanneer u uw SendGrid-account instellen en klik op **maken**.
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. Toevoegen van e-mailadressen u eigen tooboth hello **van** en **naar** velden. Voeg **externe controle waarschuwing [DeviceId]** toohello **onderwerp** veld. In Hallo **hoofdtekst van de E-mail** veld, het toevoegen van **apparaat [DeviceId] [measurementName] met de waarde [measuredValue] heeft gerapporteerd.** U kunt toevoegen **[DeviceId]**, **[measurementName]**, en **[measuredValue]** door te klikken in Hallo **kunt u gegevens uit de vorige stappen**sectie.
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. Klik op **opslaan** in het bovenste menu Hallo.
13. Klik op Hallo **aanvragen** trigger en kopieer Hallo **Http Post toothis URL** waarde. U moet deze URL verderop in deze zelfstudie.

> [!NOTE]
> Logic Apps kunnen u toorun [veel verschillende soorten actie] [ lnk-logic-apps-actions] met inbegrip van acties in Office 365. 
> 
> 

## <a name="set-up-hello-eventprocessor-web-job"></a>Hallo EventProcessor Web Project instellen
In deze sectie maakt u verbinding maken uw vooraf geconfigureerde oplossing toohello logische App die u hebt gemaakt. toocomplete deze taak u Hallo URL tootrigger Hallo logische App toohello actie toevoegen die wordt geactiveerd wanneer de waarde van een apparaat sensor een drempelwaarde overschrijdt.

1. Gebruik uw git tooclone Hallo meest recente clientversie van Hallo [azure-iot-remote-monitoring github-opslagplaats][lnk-rmgithub]. Bijvoorbeeld:
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. Open in Visual Studio Hallo **RemoteMonitoring.sln** van een lokale kopie van de Hallo van Hallo-opslagplaats.
3. Open Hallo **ActionRepository.cs** bestand in Hallo **infrastructuur\\opslagplaats** map.
4. Update Hallo **actionIds** woordenlijst met de Hallo **Http Post toothis URL** hebt genoteerd uit uw logische App als volgt:
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post toothis URL>" },
        { "Raise Alarm", "<Http Post toothis URL>" }
    };
    ```
5. Hallo wijzigingen opslaan in de oplossing en Visual Studio af te sluiten.

## <a name="deploy-from-hello-command-line"></a>Implementeren vanaf de opdrachtregel Hallo
In deze sectie kunt u de bijgewerkte versie van Hallo externe controle oplossing tooreplace Hallo versie die momenteel worden uitgevoerd in Azure implementeren.

1. Volgende Hallo [dev set-up] [ lnk-devsetup] instructies tooset van uw omgeving voor implementatie.
2. toodeploy lokaal, volg Hallo [lokale implementatie] [ lnk-localdeploy] instructies.
3. toodeploy toohello cloud en bijwerken van uw bestaande cloudimplementatie, volgt u Hallo [cloud implementatie] [ lnk-clouddeploy] instructies. Hallo-naam van uw oorspronkelijke implementatie als de naam van de implementatie hello gebruiken. Bijvoorbeeld als de oorspronkelijke implementatie Hallo is aangeroepen **demologicapp**, Hallo volgende opdracht gebruiken:
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   Wanneer Hallo bouwen script wordt uitgevoerd, moet u toouse Hallo dezelfde Azure-account, abonnement, regio en Active Directory-exemplaar die u hebt gebruikt toen u Hallo oplossing hebt ingericht.

## <a name="see-your-logic-app-in-action"></a>Zie uw logische App in actie
Hallo vooraf geconfigureerde oplossing voor externe controle heeft twee regels standaard ingesteld wanneer u een oplossing inricht. Beide regels zijn op Hallo **SampleDevice001** apparaat:

* Temperatuur > 38.00
* Vochtigheid > 48,00

Hallo temperatuur regel activeert Hallo **verhogen Alarm** actie en Hallo vochtigheid regel activeert Hallo **SendMessage** in te grijpen. Ervan uitgaande dat u gebruikt dezelfde URL voor beide acties Hallo Hallo **ActionRepository** klasse, uw logische app-triggers voor de regel. Beide regels gebruiken SendGrid toosend een e-toohello **naar** adres met details van Hallo waarschuwing.

> [!NOTE]
> Hallo logische App blijft tootrigger telkens Hallo drempelwaarde wordt voldaan. tooavoid onnodige e-mailberichten, kunt u ofwel Hallo regels uitschakelen in uw oplossing portal- of uitschakelen Hallo logische App in Hallo [Azure-portal][lnk-azureportal].
> 
> 

Bovendien tooreceiving e-mailberichten, kunt u ook zien wanneer Hallo logische App in Hallo portal wordt uitgevoerd:

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a>Volgende stappen
Nu dat u een bedrijfsproces logische App tooconnect Hallo vooraf geconfigureerde oplossing tooa gebruikt hebt, kunt u meer informatie over opties voor het aanpassen van Hallo vooraf geconfigureerde oplossingen Hallo:

* [Gebruik dynamische telemetrie Hello vooraf geconfigureerde oplossing voor externe controle][lnk-dynamic]
* [Metagegevens van apparaten informatie in Hallo vooraf geconfigureerde oplossing voor externe controle][lnk-devinfo]

[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk-internetofthings]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-getstarted]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-azureportal]: https://portal.azure.com
[lnk-logic-apps-actions]: ../connectors/apis-list.md
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-devsetup]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/dev-setup.md
[lnk-localdeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/local-deployment.md
[lnk-clouddeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
