---
title: aaaCreate een aangepaste regel in Azure IoT Suite | Microsoft Docs
description: Hoe toocreate een aangepaste regel in een IoT-Suite vooraf geconfigureerde oplossing voor.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 562799dc-06ea-4cdd-b822-80d1f70d2f09
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 6c5bb2ca54f3f17b99ad482e727c8e9fa28d7fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-rule-in-hello-remote-monitoring-preconfigured-solution"></a>Maak een aangepaste regel in Hallo vooraf geconfigureerde oplossing voor externe controle

## <a name="introduction"></a>Inleiding

In Hallo vooraf geconfigureerde oplossingen, configureert u [regels waarmee wordt geactiveerd wanneer een telemetrie waarde voor een apparaat een specifieke drempel bereikt][lnk-builtin-rule]. [Gebruik dynamische telemetrie met vooraf geconfigureerde oplossing voor externe controle Hallo] [ lnk-dynamic-telemetry] wordt beschreven hoe u kunt aangepaste telemetrie waarden toevoegen, zoals *ExternalTemperature* tooyour oplossing. Dit artikel laat zien hoe de aangepaste regel toocreate voor dynamische telemetrie typen in uw oplossing.

Deze zelfstudie wordt een eenvoudige Node.js gesimuleerd apparaat toogenerate dynamische telemetrie toosend toohello vooraf geconfigureerde oplossing voor back-end. U voegt u aangepaste regels in Hallo **RemoteMonitoring** Visual Studio-oplossing en implementeren van deze tooyour aangepaste back-end van Azure-abonnement.

toocomplete deze zelfstudie hebt u nodig:

* Een actief Azure-abonnement. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure][lnk_free_trial] voor meer informatie.
* [Node.js] [ lnk-node] versie 0.12.x of hoger toocreate een gesimuleerd apparaat.
* Visual Studio 2015 of Visual Studio 2017 toomodify Hallo vooraf geconfigureerde back-end oplossing met uw nieuwe regels.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

Noteer Hallo oplossing die u hebt gekozen voor uw implementatie. Verderop in deze zelfstudie moet u de naam van deze oplossing.

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

U kunt Hallo Node.js-consoletoepassing stoppen wanneer u hebt geverifieerd dat het verzendt **ExternalTemperature** telemetrie toohello vooraf geconfigureerde oplossing. Houd Hallo-consolevenster open omdat u deze Node.js-consoletoepassing opnieuw uitvoeren nadat u Hallo aangepaste regel toohello oplossing toevoegen.

## <a name="rule-storage-locations"></a>Opslaglocaties voor regel

Informatie over de regels worden bewaard op twee locaties:

* **DeviceRulesNormalizedTable** tabel – deze tabel bevat een genormaliseerde toohello regels die zijn gedefinieerd door de oplossingsportal Hallo verwijzen. Wanneer apparaat regels wordt weergegeven in de oplossingsportal hello, hiervoor wordt deze tabel voor Hallo regeldefinities.
* **DeviceRules** blob – deze blob slaat alle Hallo regels gedefinieerd voor alle apparaten geregistreerd en is gedefinieerd als een verwijzing invoer toohello Azure Stream Analytics-taken.
 
Wanneer u een bestaande regel bijwerken of een nieuwe regel in de oplossingsportal Hallo definiëren, zijn Hallo tabel als de blob bijgewerkte tooreflect Hallo wijzigingen. Hallo regel definitie weergegeven in de portal Hallo afkomstig van Hallo tabel store en Hallo regel definitie waarnaar wordt verwezen door de Stream Analytics-taken Hallo afkomstig is van Hallo blob. 

## <a name="update-hello-remotemonitoring-visual-studio-solution"></a>Hallo RemoteMonitoring Visual Studio-oplossing bijwerken

Hallo volgende stappen ziet u hoe toomodify Hallo RemoteMonitoring Visual Studio-oplossing tooinclude een nieuwe regel die gebruikmaakt van Hallo **ExternalTemperature** telemetrie vanaf het gesimuleerde apparaat Hallo verzonden:

1. Als u nog niet hebt gedaan, kloon Hallo **azure-iot-remote-monitoring** opslagplaats tooa geschikte locatie op uw lokale machine Hallo volgende Git-opdracht gebruiken:

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. Open in Visual Studio Hallo RemoteMonitoring.sln bestand in uw lokale exemplaar van Hallo **azure-iot-remote-monitoring** opslagplaats.

3. Open Hallo bestand Infrastructure\Models\DeviceRuleBlobEntity.cs en voeg een **ExternalTemperature** eigenschap als volgt:

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. In hetzelfde bestand hello, het toevoegen van een **ExternalTemperatureRuleOutput** eigenschap als volgt:

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. Open Hallo bestand Infrastructure\Models\DeviceRuleDataFields.cs en voeg de volgende Hallo **ExternalTemperature** eigenschap na Hallo bestaande **vochtigheid** eigenschap:

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. In hetzelfde bestand hello, Hallo bijwerken **_availableDataFields** methode tooinclude **ExternalTemperature** als volgt:

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. Hallo-bestand Infrastructure\Repository\DeviceRulesRepository.cs opent en wijzigt Hallo **BuildBlobEntityListFromTableRows** methode als volgt:

    ```csharp
    else if (rule.DataField == DeviceRuleDataFields.Humidity)
    {
        entity.Humidity = rule.Threshold;
        entity.HumidityRuleOutput = rule.RuleOutput;
    }
    else if (rule.DataField == DeviceRuleDataFields.ExternalTemperature)
    {
      entity.ExternalTemperature = rule.Threshold;
      entity.ExternalTemperatureRuleOutput = rule.RuleOutput;
    }
    ```

## <a name="rebuild-and-redeploy-hello-solution"></a>Opnieuw maken en implementeren van Hallo-oplossing.

U kunt nu implementeren Hallo bijgewerkt oplossing tooyour Azure-abonnement.

1. Open een opdrachtprompt met verhoogde bevoegdheid en navigeer toohello hoofdmap van het lokale exemplaar van azure-iot-remote-monitoring Hallo-opslagplaats.

2. toodeploy uw bijgewerkte-oplossing, Voer Hallo na opdracht vervangen door **{implementatienaam}** met Hallo-naam van de implementatie van uw vooraf geconfigureerde oplossing die u eerder hebt genoteerd:

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-hello-stream-analytics-job"></a>Update Hallo Stream Analytics-taak

Wanneer het Hallo-implementatie is voltooid, kunt u Hallo Stream Analytics-taak toouse Hallo nieuwe regeldefinities bijwerken.

1. Navigeer in hello Azure-portal, toohello resourcegroep die uw resources vooraf geconfigureerde oplossing bevat. Deze resourcegroep heeft Hallo dezelfde servernaam die u hebt opgegeven voor de oplossing tijdens de implementatie van Hallo Hallo.

2. Navigeer toohello {implementatienaam}-regels Stream Analytics-taak. 

3. Klik op **stoppen** toostop Hallo Stream Analytics-taak wordt uitgevoerd. (U moet wachten Hallo streaming-taak toostop voordat u kunt Hallo query bewerken).

4. Klik op **Query**. Hallo query tooinclude Hallo bewerken **Selecteer** -instructie voor **ExternalTemperature**. Hallo volgende voorbeeld ziet u de volledige query Hallo Hello nieuwe **Selecteer** instructie:

    ```
    WITH AlarmsData AS 
    (
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'Temperature' as ReadingType,
         Stream.Temperature as Reading,
         Ref.Temperature as Threshold,
         Ref.TemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'Humidity' as ReadingType,
         Stream.Humidity as Reading,
         Ref.Humidity as Threshold,
         Ref.HumidityRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'ExternalTemperature' as ReadingType,
         Stream.ExternalTemperature as Reading,
         Ref.ExternalTemperature as Threshold,
         Ref.ExternalTemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.ExternalTemperature IS NOT null AND Stream.ExternalTemperature > Ref.ExternalTemperature
    )
     
    SELECT *
    INTO DeviceRulesMonitoring
    FROM AlarmsData
     
    SELECT *
    INTO DeviceRulesHub
    FROM AlarmsData
    ```

5. Klik op **opslaan** toochange Hallo regel query bijgewerkt.

6. Klik op **Start** toostart Hallo Stream Analytics-taak opnieuw uit te voeren.

## <a name="add-your-new-rule-in-hello-dashboard"></a>De nieuwe regel toevoegen in Hallo-dashboard

U kunt nu Hallo toevoegen **ExternalTemperature** regel tooa apparaat in Hallo oplossing dashboard.

1. Toohello oplossingsportal navigeert.

2. Navigeer toohello **apparaten** Configuratiescherm.

3. Zoek Hallo aangepaste apparaat u hebt gemaakt die verzendt **ExternalTemperature** Telemetrie en op Hallo **Apparaatdetails** -scherm, klikt u op **regel toevoegen**.

4. Selecteer **ExternalTemperature** in **gegevensveld**.

5. Stel **drempelwaarde** too56. Klik vervolgens op **regels opslaan en weergeven**.

6. Geschiedenis van toohello dashboard tooview Hallo waarschuwingen retourneren.

7. In Hallo consolevenster u opengelaten beginnen met het Hallo Node.js console app toobegin verzenden **ExternalTemperature** telemetrische gegevens.

8. U ziet dat Hallo **geschiedenis van waarschuwingen** tabel ziet u nieuwe alarmen wanneer de nieuwe regel hello wordt geactiveerd.
 
## <a name="additional-information"></a>Aanvullende informatie

Veranderende Hallo operator  **>**  complexer en zich verder uitstrekt dan Hallo stappen in deze zelfstudie. U kunt Hallo Stream Analytics-taak toouse ongeacht operator die u wilt wijzigen, opgetreden bij het weergeven die operator in de oplossingsportal Hallo is een complexere taak. 

## <a name="next-steps"></a>Volgende stappen
Nu dat u hebt gezien hoe toocreate aangepaste regels, kunt u meer informatie over Hallo vooraf geconfigureerde oplossingen:

- [Logische App tooyour Azure IoT Suite Remote Monitoring vooraf geconfigureerde oplossing verbinden][lnk-logic-app]
- [Metagegevens van apparaten informatie in het Hallo externe controle vooraf geconfigureerde oplossing][lnk-devinfo].

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md