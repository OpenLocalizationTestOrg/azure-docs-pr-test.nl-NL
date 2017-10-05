---
title: Een aangepaste regel maken in Azure IoT Suite | Microsoft Docs
description: Het maken van een aangepaste regel in een vooraf geconfigureerde IoT Suite-oplossing.
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
ms.openlocfilehash: d58c27234ea05a82aaa3e8d72f70c1449980df09
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-custom-rule-in-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="c3403-103">Een aangepaste regel maken in de vooraf geconfigureerde oplossing voor externe controle</span><span class="sxs-lookup"><span data-stu-id="c3403-103">Create a custom rule in the remote monitoring preconfigured solution</span></span>

## <a name="introduction"></a><span data-ttu-id="c3403-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="c3403-104">Introduction</span></span>

<span data-ttu-id="c3403-105">In de vooraf geconfigureerde oplossingen, configureert u [regels waarmee wordt geactiveerd wanneer een telemetrie waarde voor een apparaat een specifieke drempel bereikt][lnk-builtin-rule].</span><span class="sxs-lookup"><span data-stu-id="c3403-105">In the preconfigured solutions, you can configure [rules that trigger when a telemetry value for a device reaches a specific threshold][lnk-builtin-rule].</span></span> <span data-ttu-id="c3403-106">[Gebruik dynamische telemetrie met externe controle vooraf geconfigureerde oplossing] [ lnk-dynamic-telemetry] wordt beschreven hoe u kunt aangepaste telemetrie waarden toevoegen, zoals *ExternalTemperature* aan uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="c3403-106">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic-telemetry] describes how you can add custom telemetry values, such as *ExternalTemperature* to your solution.</span></span> <span data-ttu-id="c3403-107">In dit artikel laat zien hoe aangepaste regel maken voor dynamische telemetrie typen in uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="c3403-107">This article shows you how to create custom rule for dynamic telemetry types in your solution.</span></span>

<span data-ttu-id="c3403-108">Deze zelfstudie wordt een eenvoudige Node.js gesimuleerd apparaat om dynamische telemetrie verzendt naar de back-end van de vooraf geconfigureerde oplossing te genereren.</span><span class="sxs-lookup"><span data-stu-id="c3403-108">This tutorial uses a simple Node.js simulated device to generate dynamic telemetry to send to the preconfigured solution back end.</span></span> <span data-ttu-id="c3403-109">U voegt u aangepaste regels in de **RemoteMonitoring** Visual Studio-oplossing en implementeren van deze aangepaste back-end voor uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="c3403-109">You then add custom rules in the **RemoteMonitoring** Visual Studio solution and deploy this customized back end to your Azure subscription.</span></span>

<span data-ttu-id="c3403-110">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="c3403-110">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="c3403-111">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="c3403-111">An active Azure subscription.</span></span> <span data-ttu-id="c3403-112">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="c3403-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c3403-113">Zie [Gratis proefversie van Azure][lnk_free_trial] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c3403-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="c3403-114">[Node.js] [ lnk-node] versie 0.12.x of hoger naar een gesimuleerd apparaat maakt.</span><span class="sxs-lookup"><span data-stu-id="c3403-114">[Node.js][lnk-node] version 0.12.x or later to create a simulated device.</span></span>
* <span data-ttu-id="c3403-115">Visual Studio 2015 of Visual Studio 2017 te wijzigen van de vooraf geconfigureerde oplossing terug eindigen met uw nieuwe regels.</span><span class="sxs-lookup"><span data-stu-id="c3403-115">Visual Studio 2015 or Visual Studio 2017 to modify the preconfigured solution back end with your new rules.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

<span data-ttu-id="c3403-116">Noteer de naam van de oplossing die u hebt gekozen voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="c3403-116">Make a note of the solution name you chose for your deployment.</span></span> <span data-ttu-id="c3403-117">Verderop in deze zelfstudie moet u de naam van deze oplossing.</span><span class="sxs-lookup"><span data-stu-id="c3403-117">You need this solution name later in this tutorial.</span></span>

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

<span data-ttu-id="c3403-118">U kunt de Node.js-consoletoepassing stoppen wanneer u hebt geverifieerd dat het verzendt **ExternalTemperature** telemetrie naar de vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="c3403-118">You can stop the Node.js console app when you have verified that it is sending **ExternalTemperature** telemetry to the preconfigured solution.</span></span> <span data-ttu-id="c3403-119">Houd het consolevenster open omdat u deze Node.js-consoletoepassing opnieuw uitvoeren nadat u de aangepaste regel aan de oplossing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c3403-119">Keep the console window open because you run this Node.js console app again after you add the custom rule to the solution.</span></span>

## <a name="rule-storage-locations"></a><span data-ttu-id="c3403-120">Opslaglocaties voor regel</span><span class="sxs-lookup"><span data-stu-id="c3403-120">Rule storage locations</span></span>

<span data-ttu-id="c3403-121">Informatie over de regels worden bewaard op twee locaties:</span><span class="sxs-lookup"><span data-stu-id="c3403-121">Information about rules is persisted in two locations:</span></span>

* <span data-ttu-id="c3403-122">**DeviceRulesNormalizedTable** tabel – deze tabel bevat een genormaliseerde verwijzing naar de regels die zijn gedefinieerd door de portal van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="c3403-122">**DeviceRulesNormalizedTable** table – This table stores a normalized reference to the rules defined by the solution portal.</span></span> <span data-ttu-id="c3403-123">Als de oplossingsportal apparaat regels weergegeven, wordt deze tabel voor de regeldefinities opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="c3403-123">When the solution portal displays device rules, it queries this table for the rule definitions.</span></span>
* <span data-ttu-id="c3403-124">**DeviceRules** blob – deze blob slaat de regels die zijn gedefinieerd voor alle apparaten geregistreerd en is gedefinieerd als een verwijzing naar de invoer voor de Azure Stream Analytics-taken.</span><span class="sxs-lookup"><span data-stu-id="c3403-124">**DeviceRules** blob – This blob stores all the rules defined for all registered devices and is defined as a reference input to the Azure Stream Analytics jobs.</span></span>
 
<span data-ttu-id="c3403-125">Wanneer u een bestaande regel bijwerken of een nieuwe regel in de oplossingsportal definiëren, zijn de tabel en de blob bijgewerkt, zodat de wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="c3403-125">When you update an existing rule or define a new rule in the solution portal, both the table and blob are updated to reflect the changes.</span></span> <span data-ttu-id="c3403-126">De regeldefinitie weergegeven in de portal is afkomstig uit de tabel-store en de regeldefinitie waarnaar wordt verwezen door de Stream Analytics-taken afkomstig zijn van de blob.</span><span class="sxs-lookup"><span data-stu-id="c3403-126">The rule definition displayed in the portal comes from the table store, and the rule definition referenced by the Stream Analytics jobs comes from the blob.</span></span> 

## <a name="update-the-remotemonitoring-visual-studio-solution"></a><span data-ttu-id="c3403-127">Update de RemoteMonitoring Visual Studio-oplossing</span><span class="sxs-lookup"><span data-stu-id="c3403-127">Update the RemoteMonitoring Visual Studio solution</span></span>

<span data-ttu-id="c3403-128">De volgende stappen ziet u hoe u wijzigt de RemoteMonitoring Visual Studio-oplossing voor het opnemen van een nieuwe regel die gebruikmaakt van de **ExternalTemperature** telemetrie vanaf het gesimuleerde apparaat verzonden:</span><span class="sxs-lookup"><span data-stu-id="c3403-128">The following steps show you how to modify the RemoteMonitoring Visual Studio solution to include a new rule that uses the **ExternalTemperature** telemetry sent from the simulated device:</span></span>

1. <span data-ttu-id="c3403-129">Als u dit nog niet hebt gedaan, kloon de **azure-iot-remote-monitoring** opslagplaats naar een geschikte locatie op uw lokale computer met de volgende Git-opdracht:</span><span class="sxs-lookup"><span data-stu-id="c3403-129">If you have not already done so, clone the **azure-iot-remote-monitoring** repository to a suitable location on your local machine using the following Git command:</span></span>

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. <span data-ttu-id="c3403-130">Open in Visual Studio het bestand RemoteMonitoring.sln in uw lokale exemplaar van de **azure-iot-remote-monitoring** opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="c3403-130">In Visual Studio, open the RemoteMonitoring.sln file from your local copy of the **azure-iot-remote-monitoring** repository.</span></span>

3. <span data-ttu-id="c3403-131">Open het bestand Infrastructure\Models\DeviceRuleBlobEntity.cs en voeg een **ExternalTemperature** eigenschap als volgt:</span><span class="sxs-lookup"><span data-stu-id="c3403-131">Open the file Infrastructure\Models\DeviceRuleBlobEntity.cs and add an **ExternalTemperature** property as follows:</span></span>

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. <span data-ttu-id="c3403-132">Voeg in hetzelfde bestand, een **ExternalTemperatureRuleOutput** eigenschap als volgt:</span><span class="sxs-lookup"><span data-stu-id="c3403-132">In the same file, add an **ExternalTemperatureRuleOutput** property as follows:</span></span>

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. <span data-ttu-id="c3403-133">Open het bestand Infrastructure\Models\DeviceRuleDataFields.cs en voeg de volgende **ExternalTemperature** eigenschap na de bestaande **vochtigheid** eigenschap:</span><span class="sxs-lookup"><span data-stu-id="c3403-133">Open the file Infrastructure\Models\DeviceRuleDataFields.cs and add the following **ExternalTemperature** property after the existing **Humidity** property:</span></span>

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. <span data-ttu-id="c3403-134">Werk in hetzelfde bestand de **_availableDataFields** methode om te nemen **ExternalTemperature** als volgt:</span><span class="sxs-lookup"><span data-stu-id="c3403-134">In the same file, update the **_availableDataFields** method to include **ExternalTemperature** as follows:</span></span>

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. <span data-ttu-id="c3403-135">Open het bestand Infrastructure\Repository\DeviceRulesRepository.cs en wijzig de **BuildBlobEntityListFromTableRows** methode als volgt:</span><span class="sxs-lookup"><span data-stu-id="c3403-135">Open the file Infrastructure\Repository\DeviceRulesRepository.cs and modify the **BuildBlobEntityListFromTableRows** method as follows:</span></span>

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

## <a name="rebuild-and-redeploy-the-solution"></a><span data-ttu-id="c3403-136">Opnieuw maken en implementeren van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="c3403-136">Rebuild and redeploy the solution.</span></span>

<span data-ttu-id="c3403-137">U kunt nu de bijgewerkte oplossing implementeren voor uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="c3403-137">You can now deploy the updated solution to your Azure subscription.</span></span>

1. <span data-ttu-id="c3403-138">Open een opdrachtprompt met verhoogde bevoegdheid en navigeer naar de hoofdmap van de lokale kopie van de azure-iot-remote-monitoring-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="c3403-138">Open an elevated command prompt and navigate to the root of your local copy of the azure-iot-remote-monitoring repository.</span></span>

2. <span data-ttu-id="c3403-139">Voor het implementeren van uw bijgewerkte oplossing, voer de volgende opdracht vervangen door **{implementatienaam}** met de naam van de implementatie van uw vooraf geconfigureerde oplossing die u eerder hebt genoteerd:</span><span class="sxs-lookup"><span data-stu-id="c3403-139">To deploy your updated solution, run the following command substituting **{deployment name}** with the name of your preconfigured solution deployment that you noted previously:</span></span>

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-the-stream-analytics-job"></a><span data-ttu-id="c3403-140">Bijwerken van de Stream Analytics-taak</span><span class="sxs-lookup"><span data-stu-id="c3403-140">Update the Stream Analytics job</span></span>

<span data-ttu-id="c3403-141">Wanneer de implementatie voltooid is, kunt u de Stream Analytics-taak voor het gebruik van de nieuwe regeldefinities bijwerken.</span><span class="sxs-lookup"><span data-stu-id="c3403-141">When the deployment is complete, you can update the Stream Analytics job to use the new rule definitions.</span></span>

1. <span data-ttu-id="c3403-142">Ga in de Azure-portal naar de resourcegroep die uw resources vooraf geconfigureerde oplossing bevat.</span><span class="sxs-lookup"><span data-stu-id="c3403-142">In the Azure portal, navigate to the resource group that contains your preconfigured solution resources.</span></span> <span data-ttu-id="c3403-143">Deze resourcegroep heeft dezelfde naam die u hebt opgegeven voor de oplossing tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="c3403-143">This resource group has the same name you specified for the solution during the deployment.</span></span>

2. <span data-ttu-id="c3403-144">Navigeer naar de {implementatienaam}-regels Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="c3403-144">Navigate to the {deployment name}-Rules Stream Analytics job.</span></span> 

3. <span data-ttu-id="c3403-145">Klik op **stoppen** stoppen van de Stream Analytics-taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c3403-145">Click **Stop** to stop the Stream Analytics job from running.</span></span> <span data-ttu-id="c3403-146">(U moet wachten voor de streaming-taak stoppen voordat u kunt de query bewerken).</span><span class="sxs-lookup"><span data-stu-id="c3403-146">(You must wait for the streaming job to stop before you can edit the query).</span></span>

4. <span data-ttu-id="c3403-147">Klik op **Query**.</span><span class="sxs-lookup"><span data-stu-id="c3403-147">Click **Query**.</span></span> <span data-ttu-id="c3403-148">De query om op te nemen bewerken de **Selecteer** -instructie voor **ExternalTemperature**.</span><span class="sxs-lookup"><span data-stu-id="c3403-148">Edit the query to include the **SELECT** statement for **ExternalTemperature**.</span></span> <span data-ttu-id="c3403-149">Het volgende voorbeeld toont de volledige query met de nieuwe **Selecteer** instructie:</span><span class="sxs-lookup"><span data-stu-id="c3403-149">The following sample shows the complete query with the new **SELECT** statement:</span></span>

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

5. <span data-ttu-id="c3403-150">Klik op **opslaan** wijzigen van de query voor bijgewerkte regel.</span><span class="sxs-lookup"><span data-stu-id="c3403-150">Click **Save** to change the updated rule query.</span></span>

6. <span data-ttu-id="c3403-151">Klik op **Start** starten van de Stream Analytics-taak opnieuw uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="c3403-151">Click **Start** to start the Stream Analytics job running again.</span></span>

## <a name="add-your-new-rule-in-the-dashboard"></a><span data-ttu-id="c3403-152">De nieuwe regel toevoegen in het dashboard</span><span class="sxs-lookup"><span data-stu-id="c3403-152">Add your new rule in the dashboard</span></span>

<span data-ttu-id="c3403-153">U kunt nu toevoegen de **ExternalTemperature** regel met een apparaat in het dashboard van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="c3403-153">You can now add the **ExternalTemperature** rule to a device in the solution dashboard.</span></span>

1. <span data-ttu-id="c3403-154">Navigeer naar de portal van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="c3403-154">Navigate to the solution portal.</span></span>

2. <span data-ttu-id="c3403-155">Navigeer naar de **apparaten** Configuratiescherm.</span><span class="sxs-lookup"><span data-stu-id="c3403-155">Navigate to the **Devices** panel.</span></span>

3. <span data-ttu-id="c3403-156">Zoek het aangepaste apparaat u hebt gemaakt die verzendt **ExternalTemperature** Telemetrie en klik op de **Apparaatdetails** -scherm, klikt u op **regel toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c3403-156">Locate the custom device you created that sends **ExternalTemperature** telemetry and on the **Device Details** panel, click **Add Rule**.</span></span>

4. <span data-ttu-id="c3403-157">Selecteer **ExternalTemperature** in **gegevensveld**.</span><span class="sxs-lookup"><span data-stu-id="c3403-157">Select **ExternalTemperature** in **Data Field**.</span></span>

5. <span data-ttu-id="c3403-158">Stel **drempelwaarde** tot 56.</span><span class="sxs-lookup"><span data-stu-id="c3403-158">Set **Threshold** to 56.</span></span> <span data-ttu-id="c3403-159">Klik vervolgens op **regels opslaan en weergeven**.</span><span class="sxs-lookup"><span data-stu-id="c3403-159">Then click **Save and view rules**.</span></span>

6. <span data-ttu-id="c3403-160">Ga terug naar het dashboard om de geschiedenis van waarschuwingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="c3403-160">Return to the dashboard to view the alarm history.</span></span>

7. <span data-ttu-id="c3403-161">In het consolevenster u opengelaten, start u de Node.js-consoletoepassing om te beginnen met verzenden **ExternalTemperature** telemetrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="c3403-161">In the console window you left open, start the Node.js console app to begin sending **ExternalTemperature** telemetry data.</span></span>

8. <span data-ttu-id="c3403-162">U ziet dat de **geschiedenis van waarschuwingen** tabel ziet u nieuwe alarmen wanneer de nieuwe regel wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="c3403-162">Notice that the **Alarm History** table shows new alarms when the new rule is triggered.</span></span>
 
## <a name="additional-information"></a><span data-ttu-id="c3403-163">Aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="c3403-163">Additional information</span></span>

<span data-ttu-id="c3403-164">Het wijzigen van de operator  **>**  complexer en zich verder uitstrekt dan de stappen in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="c3403-164">Changing the operator **>** is more complex and goes beyond the steps outlined in this tutorial.</span></span> <span data-ttu-id="c3403-165">Terwijl u de Stream Analytics-taak voor het gebruik van de operator die u wijzigen kunt, opgetreden bij het weergeven die operator in de oplossingsportal is een complexere taak.</span><span class="sxs-lookup"><span data-stu-id="c3403-165">While you can change the Stream Analytics job to use whatever operator you like, reflecting that operator in the solution portal is a more complex task.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c3403-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c3403-166">Next steps</span></span>
<span data-ttu-id="c3403-167">Nu dat u hebt gezien hoe u aangepaste regels maakt, kunt u meer informatie over de vooraf geconfigureerde oplossingen:</span><span class="sxs-lookup"><span data-stu-id="c3403-167">Now that you've seen how to create custom rules, you can learn more about the preconfigured solutions:</span></span>

- <span data-ttu-id="c3403-168">[Logic App verbinden met uw Azure IoT Suite Remote Monitoring vooraf geconfigureerde oplossing][lnk-logic-app]</span><span class="sxs-lookup"><span data-stu-id="c3403-168">[Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logic-app]</span></span>
- <span data-ttu-id="c3403-169">[Metagegevens van apparaten informatie in de externe controle vooraf geconfigureerde oplossing][lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="c3403-169">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md