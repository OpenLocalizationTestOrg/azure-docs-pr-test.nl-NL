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
# <a name="create-a-custom-rule-in-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="1bc15-103">Maak een aangepaste regel in Hallo vooraf geconfigureerde oplossing voor externe controle</span><span class="sxs-lookup"><span data-stu-id="1bc15-103">Create a custom rule in hello remote monitoring preconfigured solution</span></span>

## <a name="introduction"></a><span data-ttu-id="1bc15-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="1bc15-104">Introduction</span></span>

<span data-ttu-id="1bc15-105">In Hallo vooraf geconfigureerde oplossingen, configureert u [regels waarmee wordt geactiveerd wanneer een telemetrie waarde voor een apparaat een specifieke drempel bereikt][lnk-builtin-rule].</span><span class="sxs-lookup"><span data-stu-id="1bc15-105">In hello preconfigured solutions, you can configure [rules that trigger when a telemetry value for a device reaches a specific threshold][lnk-builtin-rule].</span></span> <span data-ttu-id="1bc15-106">[Gebruik dynamische telemetrie met vooraf geconfigureerde oplossing voor externe controle Hallo] [ lnk-dynamic-telemetry] wordt beschreven hoe u kunt aangepaste telemetrie waarden toevoegen, zoals *ExternalTemperature* tooyour oplossing.</span><span class="sxs-lookup"><span data-stu-id="1bc15-106">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic-telemetry] describes how you can add custom telemetry values, such as *ExternalTemperature* tooyour solution.</span></span> <span data-ttu-id="1bc15-107">Dit artikel laat zien hoe de aangepaste regel toocreate voor dynamische telemetrie typen in uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="1bc15-107">This article shows you how toocreate custom rule for dynamic telemetry types in your solution.</span></span>

<span data-ttu-id="1bc15-108">Deze zelfstudie wordt een eenvoudige Node.js gesimuleerd apparaat toogenerate dynamische telemetrie toosend toohello vooraf geconfigureerde oplossing voor back-end.</span><span class="sxs-lookup"><span data-stu-id="1bc15-108">This tutorial uses a simple Node.js simulated device toogenerate dynamic telemetry toosend toohello preconfigured solution back end.</span></span> <span data-ttu-id="1bc15-109">U voegt u aangepaste regels in Hallo **RemoteMonitoring** Visual Studio-oplossing en implementeren van deze tooyour aangepaste back-end van Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="1bc15-109">You then add custom rules in hello **RemoteMonitoring** Visual Studio solution and deploy this customized back end tooyour Azure subscription.</span></span>

<span data-ttu-id="1bc15-110">toocomplete deze zelfstudie hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="1bc15-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="1bc15-111">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="1bc15-111">An active Azure subscription.</span></span> <span data-ttu-id="1bc15-112">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="1bc15-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1bc15-113">Zie [Gratis proefversie van Azure][lnk_free_trial] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1bc15-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="1bc15-114">[Node.js] [ lnk-node] versie 0.12.x of hoger toocreate een gesimuleerd apparaat.</span><span class="sxs-lookup"><span data-stu-id="1bc15-114">[Node.js][lnk-node] version 0.12.x or later toocreate a simulated device.</span></span>
* <span data-ttu-id="1bc15-115">Visual Studio 2015 of Visual Studio 2017 toomodify Hallo vooraf geconfigureerde back-end oplossing met uw nieuwe regels.</span><span class="sxs-lookup"><span data-stu-id="1bc15-115">Visual Studio 2015 or Visual Studio 2017 toomodify hello preconfigured solution back end with your new rules.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

<span data-ttu-id="1bc15-116">Noteer Hallo oplossing die u hebt gekozen voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="1bc15-116">Make a note of hello solution name you chose for your deployment.</span></span> <span data-ttu-id="1bc15-117">Verderop in deze zelfstudie moet u de naam van deze oplossing.</span><span class="sxs-lookup"><span data-stu-id="1bc15-117">You need this solution name later in this tutorial.</span></span>

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

<span data-ttu-id="1bc15-118">U kunt Hallo Node.js-consoletoepassing stoppen wanneer u hebt geverifieerd dat het verzendt **ExternalTemperature** telemetrie toohello vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="1bc15-118">You can stop hello Node.js console app when you have verified that it is sending **ExternalTemperature** telemetry toohello preconfigured solution.</span></span> <span data-ttu-id="1bc15-119">Houd Hallo-consolevenster open omdat u deze Node.js-consoletoepassing opnieuw uitvoeren nadat u Hallo aangepaste regel toohello oplossing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1bc15-119">Keep hello console window open because you run this Node.js console app again after you add hello custom rule toohello solution.</span></span>

## <a name="rule-storage-locations"></a><span data-ttu-id="1bc15-120">Opslaglocaties voor regel</span><span class="sxs-lookup"><span data-stu-id="1bc15-120">Rule storage locations</span></span>

<span data-ttu-id="1bc15-121">Informatie over de regels worden bewaard op twee locaties:</span><span class="sxs-lookup"><span data-stu-id="1bc15-121">Information about rules is persisted in two locations:</span></span>

* <span data-ttu-id="1bc15-122">**DeviceRulesNormalizedTable** tabel – deze tabel bevat een genormaliseerde toohello regels die zijn gedefinieerd door de oplossingsportal Hallo verwijzen.</span><span class="sxs-lookup"><span data-stu-id="1bc15-122">**DeviceRulesNormalizedTable** table – This table stores a normalized reference toohello rules defined by hello solution portal.</span></span> <span data-ttu-id="1bc15-123">Wanneer apparaat regels wordt weergegeven in de oplossingsportal hello, hiervoor wordt deze tabel voor Hallo regeldefinities.</span><span class="sxs-lookup"><span data-stu-id="1bc15-123">When hello solution portal displays device rules, it queries this table for hello rule definitions.</span></span>
* <span data-ttu-id="1bc15-124">**DeviceRules** blob – deze blob slaat alle Hallo regels gedefinieerd voor alle apparaten geregistreerd en is gedefinieerd als een verwijzing invoer toohello Azure Stream Analytics-taken.</span><span class="sxs-lookup"><span data-stu-id="1bc15-124">**DeviceRules** blob – This blob stores all hello rules defined for all registered devices and is defined as a reference input toohello Azure Stream Analytics jobs.</span></span>
 
<span data-ttu-id="1bc15-125">Wanneer u een bestaande regel bijwerken of een nieuwe regel in de oplossingsportal Hallo definiëren, zijn Hallo tabel als de blob bijgewerkte tooreflect Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="1bc15-125">When you update an existing rule or define a new rule in hello solution portal, both hello table and blob are updated tooreflect hello changes.</span></span> <span data-ttu-id="1bc15-126">Hallo regel definitie weergegeven in de portal Hallo afkomstig van Hallo tabel store en Hallo regel definitie waarnaar wordt verwezen door de Stream Analytics-taken Hallo afkomstig is van Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="1bc15-126">hello rule definition displayed in hello portal comes from hello table store, and hello rule definition referenced by hello Stream Analytics jobs comes from hello blob.</span></span> 

## <a name="update-hello-remotemonitoring-visual-studio-solution"></a><span data-ttu-id="1bc15-127">Hallo RemoteMonitoring Visual Studio-oplossing bijwerken</span><span class="sxs-lookup"><span data-stu-id="1bc15-127">Update hello RemoteMonitoring Visual Studio solution</span></span>

<span data-ttu-id="1bc15-128">Hallo volgende stappen ziet u hoe toomodify Hallo RemoteMonitoring Visual Studio-oplossing tooinclude een nieuwe regel die gebruikmaakt van Hallo **ExternalTemperature** telemetrie vanaf het gesimuleerde apparaat Hallo verzonden:</span><span class="sxs-lookup"><span data-stu-id="1bc15-128">hello following steps show you how toomodify hello RemoteMonitoring Visual Studio solution tooinclude a new rule that uses hello **ExternalTemperature** telemetry sent from hello simulated device:</span></span>

1. <span data-ttu-id="1bc15-129">Als u nog niet hebt gedaan, kloon Hallo **azure-iot-remote-monitoring** opslagplaats tooa geschikte locatie op uw lokale machine Hallo volgende Git-opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="1bc15-129">If you have not already done so, clone hello **azure-iot-remote-monitoring** repository tooa suitable location on your local machine using hello following Git command:</span></span>

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. <span data-ttu-id="1bc15-130">Open in Visual Studio Hallo RemoteMonitoring.sln bestand in uw lokale exemplaar van Hallo **azure-iot-remote-monitoring** opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="1bc15-130">In Visual Studio, open hello RemoteMonitoring.sln file from your local copy of hello **azure-iot-remote-monitoring** repository.</span></span>

3. <span data-ttu-id="1bc15-131">Open Hallo bestand Infrastructure\Models\DeviceRuleBlobEntity.cs en voeg een **ExternalTemperature** eigenschap als volgt:</span><span class="sxs-lookup"><span data-stu-id="1bc15-131">Open hello file Infrastructure\Models\DeviceRuleBlobEntity.cs and add an **ExternalTemperature** property as follows:</span></span>

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. <span data-ttu-id="1bc15-132">In hetzelfde bestand hello, het toevoegen van een **ExternalTemperatureRuleOutput** eigenschap als volgt:</span><span class="sxs-lookup"><span data-stu-id="1bc15-132">In hello same file, add an **ExternalTemperatureRuleOutput** property as follows:</span></span>

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. <span data-ttu-id="1bc15-133">Open Hallo bestand Infrastructure\Models\DeviceRuleDataFields.cs en voeg de volgende Hallo **ExternalTemperature** eigenschap na Hallo bestaande **vochtigheid** eigenschap:</span><span class="sxs-lookup"><span data-stu-id="1bc15-133">Open hello file Infrastructure\Models\DeviceRuleDataFields.cs and add hello following **ExternalTemperature** property after hello existing **Humidity** property:</span></span>

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. <span data-ttu-id="1bc15-134">In hetzelfde bestand hello, Hallo bijwerken **_availableDataFields** methode tooinclude **ExternalTemperature** als volgt:</span><span class="sxs-lookup"><span data-stu-id="1bc15-134">In hello same file, update hello **_availableDataFields** method tooinclude **ExternalTemperature** as follows:</span></span>

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. <span data-ttu-id="1bc15-135">Hallo-bestand Infrastructure\Repository\DeviceRulesRepository.cs opent en wijzigt Hallo **BuildBlobEntityListFromTableRows** methode als volgt:</span><span class="sxs-lookup"><span data-stu-id="1bc15-135">Open hello file Infrastructure\Repository\DeviceRulesRepository.cs and modify hello **BuildBlobEntityListFromTableRows** method as follows:</span></span>

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

## <a name="rebuild-and-redeploy-hello-solution"></a><span data-ttu-id="1bc15-136">Opnieuw maken en implementeren van Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="1bc15-136">Rebuild and redeploy hello solution.</span></span>

<span data-ttu-id="1bc15-137">U kunt nu implementeren Hallo bijgewerkt oplossing tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="1bc15-137">You can now deploy hello updated solution tooyour Azure subscription.</span></span>

1. <span data-ttu-id="1bc15-138">Open een opdrachtprompt met verhoogde bevoegdheid en navigeer toohello hoofdmap van het lokale exemplaar van azure-iot-remote-monitoring Hallo-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="1bc15-138">Open an elevated command prompt and navigate toohello root of your local copy of hello azure-iot-remote-monitoring repository.</span></span>

2. <span data-ttu-id="1bc15-139">toodeploy uw bijgewerkte-oplossing, Voer Hallo na opdracht vervangen door **{implementatienaam}** met Hallo-naam van de implementatie van uw vooraf geconfigureerde oplossing die u eerder hebt genoteerd:</span><span class="sxs-lookup"><span data-stu-id="1bc15-139">toodeploy your updated solution, run hello following command substituting **{deployment name}** with hello name of your preconfigured solution deployment that you noted previously:</span></span>

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-hello-stream-analytics-job"></a><span data-ttu-id="1bc15-140">Update Hallo Stream Analytics-taak</span><span class="sxs-lookup"><span data-stu-id="1bc15-140">Update hello Stream Analytics job</span></span>

<span data-ttu-id="1bc15-141">Wanneer het Hallo-implementatie is voltooid, kunt u Hallo Stream Analytics-taak toouse Hallo nieuwe regeldefinities bijwerken.</span><span class="sxs-lookup"><span data-stu-id="1bc15-141">When hello deployment is complete, you can update hello Stream Analytics job toouse hello new rule definitions.</span></span>

1. <span data-ttu-id="1bc15-142">Navigeer in hello Azure-portal, toohello resourcegroep die uw resources vooraf geconfigureerde oplossing bevat.</span><span class="sxs-lookup"><span data-stu-id="1bc15-142">In hello Azure portal, navigate toohello resource group that contains your preconfigured solution resources.</span></span> <span data-ttu-id="1bc15-143">Deze resourcegroep heeft Hallo dezelfde servernaam die u hebt opgegeven voor de oplossing tijdens de implementatie van Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="1bc15-143">This resource group has hello same name you specified for hello solution during hello deployment.</span></span>

2. <span data-ttu-id="1bc15-144">Navigeer toohello {implementatienaam}-regels Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="1bc15-144">Navigate toohello {deployment name}-Rules Stream Analytics job.</span></span> 

3. <span data-ttu-id="1bc15-145">Klik op **stoppen** toostop Hallo Stream Analytics-taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1bc15-145">Click **Stop** toostop hello Stream Analytics job from running.</span></span> <span data-ttu-id="1bc15-146">(U moet wachten Hallo streaming-taak toostop voordat u kunt Hallo query bewerken).</span><span class="sxs-lookup"><span data-stu-id="1bc15-146">(You must wait for hello streaming job toostop before you can edit hello query).</span></span>

4. <span data-ttu-id="1bc15-147">Klik op **Query**.</span><span class="sxs-lookup"><span data-stu-id="1bc15-147">Click **Query**.</span></span> <span data-ttu-id="1bc15-148">Hallo query tooinclude Hallo bewerken **Selecteer** -instructie voor **ExternalTemperature**.</span><span class="sxs-lookup"><span data-stu-id="1bc15-148">Edit hello query tooinclude hello **SELECT** statement for **ExternalTemperature**.</span></span> <span data-ttu-id="1bc15-149">Hallo volgende voorbeeld ziet u de volledige query Hallo Hello nieuwe **Selecteer** instructie:</span><span class="sxs-lookup"><span data-stu-id="1bc15-149">hello following sample shows hello complete query with hello new **SELECT** statement:</span></span>

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

5. <span data-ttu-id="1bc15-150">Klik op **opslaan** toochange Hallo regel query bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="1bc15-150">Click **Save** toochange hello updated rule query.</span></span>

6. <span data-ttu-id="1bc15-151">Klik op **Start** toostart Hallo Stream Analytics-taak opnieuw uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="1bc15-151">Click **Start** toostart hello Stream Analytics job running again.</span></span>

## <a name="add-your-new-rule-in-hello-dashboard"></a><span data-ttu-id="1bc15-152">De nieuwe regel toevoegen in Hallo-dashboard</span><span class="sxs-lookup"><span data-stu-id="1bc15-152">Add your new rule in hello dashboard</span></span>

<span data-ttu-id="1bc15-153">U kunt nu Hallo toevoegen **ExternalTemperature** regel tooa apparaat in Hallo oplossing dashboard.</span><span class="sxs-lookup"><span data-stu-id="1bc15-153">You can now add hello **ExternalTemperature** rule tooa device in hello solution dashboard.</span></span>

1. <span data-ttu-id="1bc15-154">Toohello oplossingsportal navigeert.</span><span class="sxs-lookup"><span data-stu-id="1bc15-154">Navigate toohello solution portal.</span></span>

2. <span data-ttu-id="1bc15-155">Navigeer toohello **apparaten** Configuratiescherm.</span><span class="sxs-lookup"><span data-stu-id="1bc15-155">Navigate toohello **Devices** panel.</span></span>

3. <span data-ttu-id="1bc15-156">Zoek Hallo aangepaste apparaat u hebt gemaakt die verzendt **ExternalTemperature** Telemetrie en op Hallo **Apparaatdetails** -scherm, klikt u op **regel toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1bc15-156">Locate hello custom device you created that sends **ExternalTemperature** telemetry and on hello **Device Details** panel, click **Add Rule**.</span></span>

4. <span data-ttu-id="1bc15-157">Selecteer **ExternalTemperature** in **gegevensveld**.</span><span class="sxs-lookup"><span data-stu-id="1bc15-157">Select **ExternalTemperature** in **Data Field**.</span></span>

5. <span data-ttu-id="1bc15-158">Stel **drempelwaarde** too56.</span><span class="sxs-lookup"><span data-stu-id="1bc15-158">Set **Threshold** too56.</span></span> <span data-ttu-id="1bc15-159">Klik vervolgens op **regels opslaan en weergeven**.</span><span class="sxs-lookup"><span data-stu-id="1bc15-159">Then click **Save and view rules**.</span></span>

6. <span data-ttu-id="1bc15-160">Geschiedenis van toohello dashboard tooview Hallo waarschuwingen retourneren.</span><span class="sxs-lookup"><span data-stu-id="1bc15-160">Return toohello dashboard tooview hello alarm history.</span></span>

7. <span data-ttu-id="1bc15-161">In Hallo consolevenster u opengelaten beginnen met het Hallo Node.js console app toobegin verzenden **ExternalTemperature** telemetrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="1bc15-161">In hello console window you left open, start hello Node.js console app toobegin sending **ExternalTemperature** telemetry data.</span></span>

8. <span data-ttu-id="1bc15-162">U ziet dat Hallo **geschiedenis van waarschuwingen** tabel ziet u nieuwe alarmen wanneer de nieuwe regel hello wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="1bc15-162">Notice that hello **Alarm History** table shows new alarms when hello new rule is triggered.</span></span>
 
## <a name="additional-information"></a><span data-ttu-id="1bc15-163">Aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="1bc15-163">Additional information</span></span>

<span data-ttu-id="1bc15-164">Veranderende Hallo operator  **>**  complexer en zich verder uitstrekt dan Hallo stappen in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="1bc15-164">Changing hello operator **>** is more complex and goes beyond hello steps outlined in this tutorial.</span></span> <span data-ttu-id="1bc15-165">U kunt Hallo Stream Analytics-taak toouse ongeacht operator die u wilt wijzigen, opgetreden bij het weergeven die operator in de oplossingsportal Hallo is een complexere taak.</span><span class="sxs-lookup"><span data-stu-id="1bc15-165">While you can change hello Stream Analytics job toouse whatever operator you like, reflecting that operator in hello solution portal is a more complex task.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1bc15-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1bc15-166">Next steps</span></span>
<span data-ttu-id="1bc15-167">Nu dat u hebt gezien hoe toocreate aangepaste regels, kunt u meer informatie over Hallo vooraf geconfigureerde oplossingen:</span><span class="sxs-lookup"><span data-stu-id="1bc15-167">Now that you've seen how toocreate custom rules, you can learn more about hello preconfigured solutions:</span></span>

- <span data-ttu-id="1bc15-168">[Logische App tooyour Azure IoT Suite Remote Monitoring vooraf geconfigureerde oplossing verbinden][lnk-logic-app]</span><span class="sxs-lookup"><span data-stu-id="1bc15-168">[Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logic-app]</span></span>
- <span data-ttu-id="1bc15-169">[Metagegevens van apparaten informatie in het Hallo externe controle vooraf geconfigureerde oplossing][lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="1bc15-169">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md