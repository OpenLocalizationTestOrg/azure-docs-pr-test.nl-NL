---
title: aaaCustomizing vooraf geconfigureerde oplossingen | Microsoft Docs
description: Biedt richtlijnen voor hoe toocustomize hello Azure IoT Suite vooraf oplossingen geconfigureerde.
services: 
suite: iot-suite
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4653ae53-4110-4a10-bd6c-7dc034c293a8
ms.service: iot-suite
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: 1a8573f5ac6ed944c44459df495446f15174d513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-a-preconfigured-solution"></a>Een vooraf geconfigureerde oplossing aanpassen

Hallo vooraf geconfigureerde oplossingen Hello Azure IoT Suite demonstreren Hallo services binnen Hallo suite werken samen toodeliver een end-to-end-oplossing. Vanaf deze beginpunt zijn er verschillende plaatsen waarin u kunt uitbreiden en aanpassen Hallo-oplossing voor specifieke scenario's. Hallo volgende secties beschrijven deze common aanpassing punten.

## <a name="find-hello-source-code"></a>Hallo broncode vinden

de broncode Hallo voor Hallo vooraf geconfigureerde oplossingen is beschikbaar op GitHub in Hallo opslagplaatsen te volgen:

* Externe controle: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)
* Voorspeld onderhoud: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)
* Verbonden factory: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)

de broncode Hallo voor Hallo vooraf geconfigureerde oplossingen wordt verstrekt toodemonstrate Hallo patterns and practice tooimplement Hallo end-to-end-functionaliteit van een IoT-oplossing met behulp van Azure IoT Suite gebruikt. U vindt meer informatie over het toobuild en oplossingen in de GitHub-opslagplaatsen Hallo Hallo implementeren.

## <a name="change-hello-preconfigured-rules"></a>Hallo vooraf geconfigureerde regels wijzigen

Hallo oplossing voor externe controle omvat drie [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) taken toohandle apparaatgegevens, Telemetrie en regellogica in Hallo-oplossing.

Hallo drie stream analytics-taken en hun syntaxis worden beschreven in de diepte in Hallo [externe controle oplossing walkthrough over vooraf geconfigureerde](iot-suite-remote-monitoring-sample-walkthrough.md). 

U kunt deze taken bewerken direct tooalter Hallo logica of Voeg logica specifieke tooyour scenario. U vindt Hallo Stream Analytics-taken als volgt:

1. Ga te[Azure-portal](https://portal.azure.com).
2. De resourcegroep toohello met dezelfde naam als uw IoT-oplossing Hallo navigeren. 
3. Selecteer hello Azure Stream Analytics-taak gewenst toomodify. 
4. Hallo-taak stoppen als u selecteert **stoppen** in Hallo reeks opdrachten. 
5. Hallo-in-, query- en uitgangen bewerken.
   
    Een eenvoudige wijziging is toochange Hallo-query voor Hallo **regels** taak toouse een **' < '** in plaats van een **' > '**. nog steeds weergegeven in de oplossingsportal Hello **' > '** wanneer u een regel voor het bewerken, maar u ziet hoe Hallo gedrag vanwege toohello wijziging in de onderliggende taak hello wordt gespiegeld.
6. Hallo taak starten

> [!NOTE]
> Hallo-dashboard voor externe controle, is afhankelijk van wat u specifieke gegevens dus Hallo dashboard toofail wijzigen Hallo taken kan veroorzaken.

## <a name="add-your-own-rules"></a>Uw eigen regels toevoegen

Bovendien toochanging Hallo vooraf geconfigureerde Azure Stream Analytics-taken, kunt u hello Azure portal tooadd nieuwe taken gebruiken of nieuwe query's tooexisting taken toevoegen.

## <a name="customize-devices"></a>Apparaten aanpassen

Een van de meest voorkomende extensie activiteiten Hallo werkt met apparaten specifieke tooyour scenario. Er zijn verschillende methoden voor het werken met apparaten. Deze methoden omvatten een gesimuleerd apparaat toomatch uw scenario wijzigen of met behulp van Hallo [IoT Device SDK] [ IoT Device SDK] tooconnect uw fysieke apparaat toohello oplossing.

Zie voor een stapsgewijze handleiding tooadding apparaten, Hallo [Iot Suite-verbinding maken met apparaten](iot-suite-connecting-devices.md) artikel en Hallo [van een remote monitoring C SDK voorbeeld](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring). Dit voorbeeld is ontworpen toowork Hello vooraf geconfigureerde oplossing voor externe controle.

### <a name="create-your-own-simulated-device"></a>Uw eigen gesimuleerd apparaat kunt maken

Opgenomen in Hallo [voor externe controle oplossing broncode](https://github.com/Azure/azure-iot-remote-monitoring), is een .NET-simulator. Deze simulator is Hallo een ingericht als onderdeel van het Hallo-oplossing en u kunt wijzigen toosend andere metagegevens telemetrie, reageren toodifferent opdrachten en -methoden.

de vooraf geconfigureerde simulator Hallo in Hallo vooraf geconfigureerde oplossing voor externe controle een koelervoorbeeld apparaat simuleert dat temperatuur en vochtigheid telemetrie verzendt. U kunt wijzigen Hallo simulator in Hallo [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) wanneer u hebt de GitHub-opslagplaats Hallo forked project.

### <a name="available-locations-for-simulated-devices"></a>Beschikbare locaties voor de gesimuleerde apparaten

Er is een Hallo standaardset locaties in Seattle/Redmond, Washington, Verenigde Staten van Amerika. U kunt deze locaties in wijzigen [SampleDeviceFactory.cs][lnk-sample-device-factory].

### <a name="add-a-desired-property-update-handler-toohello-simulator"></a>Een gewenste eigenschap update handler toohello simulator toevoegen

U kunt een waarde voor een gewenste eigenschap voor een apparaat in de oplossingsportal Hallo instellen. Het is Hallo verantwoordelijkheid van Hallo apparaat toohandle Hallo eigenschap wijzigingsaanvraag Hallo apparaat ophalen van eigenschapswaarde Hallo gewenst. tooadd ondersteuning voor een wijziging in de eigenschap waarde via een gewenste eigenschap, moet u een handler toohello simulator tooadd.

Hallo simulator bevat handlers voor Hallo **SetPointTemp** en **TelemetryInterval** eigenschappen die u bijwerken door het instellen van kunt de gewenste waarden in de oplossingsportal Hallo.

Hallo volgende voorbeeld ziet u Hallo-handler voor Hallo **SetPointTemp** gewenst eigenschap in Hallo **CoolerDevice** klasse:

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

Deze methode werkt Hallo telemetrie punt temperatuur- en vervolgens rapporten Hallo back tooIoT Hub wijzigen door een eigenschap gemeld.

U kunt uw eigen handlers voor uw eigen eigenschappen toevoegen door de volgende Hallo patroon in het voorgaande voorbeeld Hallo.

U moet ook Hallo gewenste eigenschap toohello handler binden zoals weergegeven in het volgende voorbeeld uit Hallo Hallo **CoolerDevice** constructor:

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

Houd er rekening mee dat **SetPointTempPropertyName** een constante is gedefinieerd als 'Config.SetPointTemp'.

### <a name="add-support-for-a-new-method-toohello-simulator"></a>Ondersteuning voor een nieuwe methode toohello simulator toevoegen

U kunt aanpassen Hallo simulator tooadd ondersteuning voor een nieuwe [methode (directe methode)][lnk-direct-methods]. Er zijn twee belangrijke stappen vereist:

- Hallo simulator verwittigt Hallo IoT-hub in Hallo vooraf geconfigureerde oplossing met details van Hallo-methode.
- Hallo simulator moet code toohandle Hallo methodeaanroep bevatten wanneer u het aanroepen van Hallo **Apparaatdetails** deelvenster in Hallo solution explorer of via een taak.

Hallo externe controle vooraf geconfigureerde oplossing maakt gebruik van *gerapporteerd eigenschappen* toosend details van de ondersteunde methoden tooIoT hub. Hallo back-end oplossing houdt een lijst van alle Hallo methoden die worden ondersteund door elk apparaat samen met een geschiedenis van methode aanroepen. U kunt deze informatie weergeven over apparaten en methoden aanroepen in de oplossingsportal Hallo.

Hallo toonotify IoT-hub of een apparaat een methode ondersteunt, Hallo apparaat moet toevoegen details van Hallo methode toohello **SupportedMethods** knooppunt in Hallo gerapporteerd eigenschappen:

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

Hallo Methodehandtekening heeft Hallo volgende indeling: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`. Bijvoorbeeld: toospecify hello **InitiateFirmwareUpdate** methode verwacht een tekenreeksparameter met de naam **FwPackageURI**, Hallo methodehandtekening volgende gebruiken:

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

Zie voor een lijst van ondersteunde parametertypen Hallo **CommandTypes** klasse in Hallo infrastructuurproject.

toodelete een methode instellen Hallo methodehandtekening te`null` in Hallo gerapporteerd eigenschappen.

> [!NOTE]
> Hallo back-end oplossing werkt alleen informatie over ondersteunde methoden wanneer dit ontvangt een *apparaatgegevens* bericht van het Hallo-apparaat.

Hallo volgende codevoorbeeld van Hallo **SampleDeviceFactory** klasse in Hallo gemeenschappelijke project toont hoe tooadd een methode toohello lijst van **SupportedMethods** Hallo eigenschappen is verzonden door Hallo gerapporteerd apparaat:

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' toospecifiy hello URI of hello firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

Dit codefragment voegt details van Hallo **InitiateFirmwareUpdate** methode, met inbegrip van tekst toodisplay in de oplossingsportal hello en details van Hallo methodeparameters vereist.

Hallo simulator verzendt gemelde eigenschappen, waaronder Hallo lijst van ondersteunde methoden tooIoT Hub wanneer Hallo simulator wordt gestart.

Voeg een handler toohello simulator code voor elke methode ondersteund. U kunt bestaande handlers in Hallo Hallo zien **CoolerDevice** klasse in Hallo Simulator.WebJob project. Hallo volgende voorbeeld ziet u Hallo-handler voor **InitiateFirmwareUpdate** methode:

```csharp
public async Task<MethodResponse> OnInitiateFirmwareUpdate(MethodRequest methodRequest, object userContext)
{
    if (_deviceManagementTask != null && !_deviceManagementTask.IsCompleted)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "Device is busy"
        }, 409));
    }

    try
    {
        var operation = new FirmwareUpdate(methodRequest);
        _deviceManagementTask = operation.Run(Transport).ContinueWith(async task =>
        {
            // after firmware completed, we reset telemetry
            var telemetry = _telemetryController as ITelemetryWithTemperatureMeanValue;
            if (telemetry != null)
            {
                telemetry.TemperatureMeanValue = 34.5;
            }

            await UpdateReportedTemperatureMeanValue();
        });

        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "FirmwareUpdate accepted",
            Uri = operation.Uri
        }));
    }
    catch (Exception ex)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = ex.Message
        }, 400));
    }
}
```

Methode handler namen moeten beginnen met `On` gevolgd door Hallo-naam van het Hallo-methode. Hallo **methodRequest** parameter met de methodeaanroep Hallo van Hallo back-end oplossing doorgegeven parameters bevat. Hallo retourwaarde moet van het type **taak&lt;MethodResponse&gt;**. Hallo **BuildMethodResponse** hulpprogramma methode kunt u de retourwaarde Hallo maken.

Binnen Hallo methode handler, kunt u het volgende doen:

- Een asynchrone taak gestart.
- Eigenschappen van de gewenste ophalen van Hallo *apparaat twin* in IoT-Hub.
- Bijwerken van één gemelde eigenschap Hallo met **SetReportedPropertyAsync** methode in Hallo **CoolerDevice** klasse.
- De eigenschappen van meerdere gemelde bijwerken door het maken van een **TwinCollection** exemplaar en aanroepen Hallo **Transport.UpdateReportedPropertiesAsync** methode.

Hallo voert voorgaande voorbeeld voor firmware-update Hallo stappen te volgen:

- Controles Hallo apparaat is een aanvraag kunnen tooaccept Hallo firmware-update.
- Asynchroon Hallo firmware-update-bewerking initieert en herstelt u de Hallo telemetrie wanneer Hallo voltooid is.
- Onmiddellijk retourneert 'FirmwareUpdate geaccepteerd' Hallo worden bericht tooindicate Hallo-aanvraag is geaccepteerd door Hallo-apparaat.

### <a name="build-and-use-your-own-physical-device"></a>Opbouwen en uw eigen (fysiek) apparaat gebruiken

Hallo [Azure IoT SDK's](https://github.com/Azure/azure-iot-sdks) bibliotheken voor het verbinden van verschillende typen apparaten (talen en besturingssystemen) in IoT-oplossingen bieden.

## <a name="modify-dashboard-limits"></a>Limieten van dashboard wijzigen

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a>Aantal apparaten weergegeven in de vervolgkeuzelijst dashboard

Hallo standaardwaarde is 200. U kunt dit nummer in wijzigen [DashboardController.cs][lnk-dashboard-controller].

### <a name="number-of-pins-toodisplay-in-bing-map-control"></a>Het aantal pincodes toodisplay in besturingselement Bing-kaart

Hallo standaardwaarde is 200. U kunt dit nummer in wijzigen [TelemetryApiController.cs][lnk-telemetry-api-controller-01].

### <a name="time-period-of-telemetry-graph"></a>De periode van telemetrie-grafiek

Hallo standaardwaarde is 10 minuten. U kunt deze waarde in wijzigen [TelmetryApiController.cs][lnk-telemetry-api-controller-02].

## <a name="manually-set-up-application-roles"></a>Toepassingsrollen handmatig instellen

Hallo volgende procedure wordt beschreven hoe tooadd **Admin** en **ReadOnly** toepassing rollen tooa vooraf geconfigureerde oplossing. Houd er rekening mee dat vooraf geconfigureerde oplossingen al ingericht van Hallo azureiotsuite.com site Hallo **Admin** en **ReadOnly** rollen.

Leden van Hallo **ReadOnly** rol Hallo dashboard en de lijst met apparaten Hallo kunt zien, maar zijn niet toegestaan tooadd apparaten, apparaatkenmerken wijzigen of de opdrachten voor verzenden.  Leden van Hallo **Admin** rol hebben volledige toegang tooall Hallo functionaliteit in Hallo-oplossing.

1. Ga toohello [klassieke Azure-portal][lnk-classic-portal].
2. Selecteer **Active Directory**.
3. Klik op de naam Hallo van Hallo AAD-tenant die u hebt gebruikt toen u uw oplossing hebt ingericht.
4. Klik op **toepassingen**.
5. Klik op Hallo-naam van de toepassing hello die overeenkomt met de naam van uw vooraf geconfigureerde oplossing. Als u uw toepassing in de lijst Hallo niet ziet, selecteert u **toepassingen mijn bedrijf eigenaar is van** in Hallo **weergeven** vervolgkeuzelijst en klik op Hallo selectievakje is ingeschakeld.
6. Klik onder aan de pagina Hallo Hallo op **beheren Manifest** en vervolgens **downloaden Manifest**.
7. Deze procedure downloadt een .json-bestand tooyour lokale machine. Open dit bestand bewerken in een teksteditor van uw keuze.
8. Op de derde regel Hallo van Hallo .json-bestand, kunt u het volgende zien:

   ```json
   "appRoles" : [],
   ```
   Deze regel vervangen door Hallo code te volgen:

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access toohello application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access toodevice information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. Sla Hallo bijgewerkte .json-bestand (u kunt Hallo bestaand bestand overschrijven).
10. Selecteer in de klassieke Azure-portal onderaan Hallo Hallo pagina Hallo **beheren Manifest** vervolgens **uploaden Manifest** tooupload hello .json-bestand die u in de vorige stap Hallo opgeslagen.
11. U hebt nu toegevoegd Hallo **Admin** en **ReadOnly** rollen tooyour toepassing.
12. Zie tooassign een van deze rollen tooa gebruiker in uw directory [machtigingen op Hallo azureiotsuite.com site][lnk-permissions].

## <a name="feedback"></a>Feedback

Hebt u het gewenste toosee in dit document behandeld aanpassen? Suggesties voor functies te toevoegen[User Voice](https://feedback.azure.com/forums/321918-azure-iot), of de opmerking bij dit artikel. 

## <a name="next-steps"></a>Volgende stappen

toolearn meer informatie over het Hallo-opties voor het aanpassen van Hallo vooraf geconfigureerde oplossingen, Zie:

* [Logische App tooyour Azure IoT Suite Remote Monitoring vooraf geconfigureerde oplossing verbinden][lnk-logicapp]
* [Gebruik dynamische telemetrie Hello vooraf geconfigureerde oplossing voor externe controle][lnk-dynamic]
* [Metagegevens van apparaten informatie in Hallo vooraf geconfigureerde oplossing voor externe controle][lnk-devinfo]
* [Aanpassen hoe Hallo factory oplossing geeft gegevens van uw servers OPC UA verbonden][lnk-cf-customize]

[lnk-logicapp]: iot-suite-logic-apps-tutorial.md
[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[IoT Device SDK]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-permissions]: iot-suite-permissions.md
[lnk-dashboard-controller]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/Controllers/DashboardController.cs#L27
[lnk-telemetry-api-controller-01]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L27
[lnk-telemetry-api-controller-02]: https://github.com/Azure/azure-iot-remote-monitoring/blob/e7003339f73e21d3930f71ceba1e74fb5c0d9ea0/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L25 
[lnk-sample-device-factory]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Common/Factory/SampleDeviceFactory.cs#L40
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-cf-customize]: iot-suite-connected-factory-customize.md