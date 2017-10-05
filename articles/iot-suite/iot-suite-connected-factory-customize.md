---
title: Azure IoT Suite verbonden factory aanpassen | Microsoft Docs
description: Een beschrijving van het aanpassen van het gedrag van de verbonden factory vooraf geconfigureerde oplossing.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: c#
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 90a6172dbd887ecda5a9f5d9082a4e136092bc10
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="customize-how-the-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a><span data-ttu-id="e60fc-103">Aanpassen hoe de gegevens van uw OPC UA-servers worden weergegeven in de verbonden factory-oplossing</span><span class="sxs-lookup"><span data-stu-id="e60fc-103">Customize how the connected factory solution displays data from your OPC UA servers</span></span>

## <a name="introduction"></a><span data-ttu-id="e60fc-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="e60fc-104">Introduction</span></span>

<span data-ttu-id="e60fc-105">De oplossing verbonden factory samenvoegt en gegevens uit de OPC UA-servers die is verbonden met de oplossing worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e60fc-105">The connected factory solution aggregates and displays data from the OPC UA servers connected to the solution.</span></span> <span data-ttu-id="e60fc-106">U kunt bladeren en opdrachten verzenden naar de OPC UA-servers in uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="e60fc-106">You can browse and send commands to the OPC UA servers in your solution.</span></span> <span data-ttu-id="e60fc-107">Zie de [veelgestelde vragen over Connected Factory](iot-suite-faq-cf.md) voor meer informatie over OPC UA.</span><span class="sxs-lookup"><span data-stu-id="e60fc-107">For more information about OPC UA, see the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

<span data-ttu-id="e60fc-108">Voorbeelden van geaggregeerde gegevens in de oplossing zijn de algehele apparatuur efficiëntie (OEE) en de Key Performance Indicators (KPI's) die u in het dashboard op de factory-, lijn- en station niveaus bekijken kunt.</span><span class="sxs-lookup"><span data-stu-id="e60fc-108">Examples of aggregated data in the solution include the Overall Equipment Efficiency (OEE) and Key Performance Indicators (KPIs) that you can view in the dashboard at the factory, line, and station levels.</span></span> <span data-ttu-id="e60fc-109">De volgende schermafbeelding ziet u de waarden OEE en KPI's voor de **Assembly** station op **productie-regel 1**, in de **München** factory:</span><span class="sxs-lookup"><span data-stu-id="e60fc-109">The following screenshot shows the OEE and KPI values for the **Assembly** station, on **Production line 1**, in the **Munich** factory:</span></span>

![Voorbeeld van OEE en KPI waarden in de oplossing][img-oee-kpi]

<span data-ttu-id="e60fc-111">De oplossing kunt u gedetailleerde informatie weergeven vanaf specifieke gegevensitems uit de OPC UA-servers, zogenaamde *stations*.</span><span class="sxs-lookup"><span data-stu-id="e60fc-111">The solution enables you to view detailed information from specific data items from the OPC UA servers, called *stations*.</span></span> <span data-ttu-id="e60fc-112">De volgende schermafbeelding ziet curve van het aantal geproduceerde items van een specifiek station:</span><span class="sxs-lookup"><span data-stu-id="e60fc-112">The following screenshot shows plots of the number of manufactured items from a specific station:</span></span>

![Curve van het aantal geproduceerde artikelen][img-manufactured-items]

<span data-ttu-id="e60fc-114">Als u klikt op een van de grafieken, vindt u de gegevens verder met Time Series Insights (TSI):</span><span class="sxs-lookup"><span data-stu-id="e60fc-114">If you click one of the graphs, you can explore the data further using Time Series Insights (TSI):</span></span>

![Gegevens met behulp van de Time Series Insights verkennen][img-tsi]

<span data-ttu-id="e60fc-116">Dit artikel wordt beschreven:</span><span class="sxs-lookup"><span data-stu-id="e60fc-116">This article describes:</span></span>

- <span data-ttu-id="e60fc-117">Hoe de gegevens beschikbaar worden gesteld aan de verschillende weergaven in de oplossing.</span><span class="sxs-lookup"><span data-stu-id="e60fc-117">How the data is made available to the various views in the solution.</span></span>
- <span data-ttu-id="e60fc-118">Hoe u de manier waarop de oplossing kunt aanpassen, worden de gegevens weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e60fc-118">How you can customize the way the solution displays the data.</span></span>

## <a name="data-sources"></a><span data-ttu-id="e60fc-119">Gegevensbronnen</span><span class="sxs-lookup"><span data-stu-id="e60fc-119">Data sources</span></span>

<span data-ttu-id="e60fc-120">De verbonden factory-oplossing worden gegevens uit de OPC UA-servers die is verbonden met de oplossing.</span><span class="sxs-lookup"><span data-stu-id="e60fc-120">The connected factory solution displays data from the OPC UA servers connected to the solution.</span></span> <span data-ttu-id="e60fc-121">De standaardinstallatie bevat verschillende OPC UA-servers met een factory simulatie.</span><span class="sxs-lookup"><span data-stu-id="e60fc-121">The default installation includes several OPC UA servers running a factory simulation.</span></span> <span data-ttu-id="e60fc-122">U kunt uw eigen servers OPC UA toevoegen die [verbinding maken via een gateway] [ lnk-connect-cf] aan uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="e60fc-122">You can add your own OPC UA servers that [connect through a gateway][lnk-connect-cf] to your solution.</span></span>

<span data-ttu-id="e60fc-123">U kunt de gegevensitems die een verbonden OPC UA-server om uw oplossing in het dashboard te verzenden kunt bladeren:</span><span class="sxs-lookup"><span data-stu-id="e60fc-123">You can browse the data items that a connected OPC UA server can send to your solution in the dashboard:</span></span>

1. <span data-ttu-id="e60fc-124">Navigeer naar de **selecteert u een server OPC UA** weergeven:</span><span class="sxs-lookup"><span data-stu-id="e60fc-124">Navigate to the **Select an OPC UA server** view:</span></span>

    ![Navigeer naar het selecteren van een weergave OPC UA-server][img-select-server]

1. <span data-ttu-id="e60fc-126">Selecteer een server en klik op **Connect**.</span><span class="sxs-lookup"><span data-stu-id="e60fc-126">Select a server and click **Connect**.</span></span> <span data-ttu-id="e60fc-127">Klik op **doorgaan** wanneer de beveiligingswaarschuwing wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e60fc-127">Click **Proceed** when the security warning appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e60fc-128">Deze waarschuwing alleen verschijnt eenmaal voor elke server en er wordt een vertrouwensrelatie tussen het dashboard van de oplossing en de server.</span><span class="sxs-lookup"><span data-stu-id="e60fc-128">This warning only appears once for each server and establishes a trust relationship between the solution dashboard and the server.</span></span>

1. <span data-ttu-id="e60fc-129">U kunt nu de gegevensitems die de server naar de oplossing verzenden kan bladeren.</span><span class="sxs-lookup"><span data-stu-id="e60fc-129">You can now browse the data items that the server can send to the solution.</span></span> <span data-ttu-id="e60fc-130">Items die worden verzonden naar de oplossing hebt een groen vinkje:</span><span class="sxs-lookup"><span data-stu-id="e60fc-130">Items that are being sent to the solution have a green check mark:</span></span>

    ![Gepubliceerde items][img-published]

1. <span data-ttu-id="e60fc-132">Als u een *beheerder* in de oplossing kunt u kiezen voor het publiceren van een gegevensitem zodat deze beschikbaar zijn in de verbonden factory-oplossing.</span><span class="sxs-lookup"><span data-stu-id="e60fc-132">If you are an *Administrator* in the solution, you can choose to publish a data item to make it available in the connected factory solution.</span></span> <span data-ttu-id="e60fc-133">U kunt ook de waarde van gegevensitems wijzigen en methoden aanroepen op de OPC UA-server als beheerder.</span><span class="sxs-lookup"><span data-stu-id="e60fc-133">As an Administrator, you can also change the value of data items and call methods in the OPC UA server.</span></span>

## <a name="map-the-data"></a><span data-ttu-id="e60fc-134">De gegevens moeten worden toegewezen</span><span class="sxs-lookup"><span data-stu-id="e60fc-134">Map the data</span></span>

<span data-ttu-id="e60fc-135">De oplossing verbonden factory toegewezen en de gepubliceerde-gegevensitems van de OPC UA-server samenvoegt met de verschillende weergaven in de oplossing.</span><span class="sxs-lookup"><span data-stu-id="e60fc-135">The connected factory solution maps and aggregates the published data items from the OPC UA server to the various views in the solution.</span></span> <span data-ttu-id="e60fc-136">De verbonden factory-oplossing implementeert in uw Azure-account wanneer u de oplossing inricht.</span><span class="sxs-lookup"><span data-stu-id="e60fc-136">The connected factory solution deploys to your Azure account when you provision the solution.</span></span> <span data-ttu-id="e60fc-137">Een JSON-bestand in de Visual Studio verbonden factory oplossing slaat deze informatie over de Identiteitstoewijzing.</span><span class="sxs-lookup"><span data-stu-id="e60fc-137">A JSON file in the Visual Studio connected factory solution stores this mapping information.</span></span> <span data-ttu-id="e60fc-138">U kunt weergeven en wijzigen van dit JSON-configuratiebestand in de verbonden fabriek Visual Studio-oplossing.</span><span class="sxs-lookup"><span data-stu-id="e60fc-138">You can view and modify this JSON configuration file in the connected factory Visual Studio solution.</span></span> <span data-ttu-id="e60fc-139">U kunt de oplossing opnieuw implementeren nadat u een wijziging aanbrengt.</span><span class="sxs-lookup"><span data-stu-id="e60fc-139">You can redeploy the solution after you make a change.</span></span>

<span data-ttu-id="e60fc-140">U kunt het configuratiebestand te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e60fc-140">You can use the configuration file to:</span></span>

- <span data-ttu-id="e60fc-141">Bewerk de bestaande gesimuleerde fabrieken, de regels voor productie en de stations.</span><span class="sxs-lookup"><span data-stu-id="e60fc-141">Edit the existing simulated factories, production lines, and stations.</span></span>
- <span data-ttu-id="e60fc-142">Gegevens van echte OPC UA-servers waarop u verbinding met de oplossing maken toewijzen.</span><span class="sxs-lookup"><span data-stu-id="e60fc-142">Map data from real OPC UA servers that you connect to the solution.</span></span>

<span data-ttu-id="e60fc-143">Als u wilt klonen van een kopie van de verbonden factory Visual Studio-oplossing, kunt u de volgende git-opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e60fc-143">To clone a copy of the connected factory Visual Studio solution, use the following git command:</span></span>

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

<span data-ttu-id="e60fc-144">Het bestand **ContosoTopologyDescription.json** definieert u de toewijzing van de items OPC UA-server gegevens naar de weergaven in het dashboard van de verbonden factory-oplossing.</span><span class="sxs-lookup"><span data-stu-id="e60fc-144">The file **ContosoTopologyDescription.json** defines the mapping from the OPC UA server data items to the views in the connected factory solution dashboard.</span></span> <span data-ttu-id="e60fc-145">U vindt dit configuratiebestand in de **Contoso\Topology** map in de **WebApp** -project in Visual Studio-oplossing.</span><span class="sxs-lookup"><span data-stu-id="e60fc-145">You can find this configuration file in the **Contoso\Topology** folder in the **WebApp** project in the Visual Studio solution.</span></span>

<span data-ttu-id="e60fc-146">De inhoud van het JSON-bestand is ingedeeld als een hiërarchie van de factory-, productie-lijn- en station knooppunten.</span><span class="sxs-lookup"><span data-stu-id="e60fc-146">The content of the JSON file is organized as a hierarchy of factory, production line, and station nodes.</span></span> <span data-ttu-id="e60fc-147">Deze hiërarchie definieert de navigatiehiërarchie in het dashboard verbonden factory.</span><span class="sxs-lookup"><span data-stu-id="e60fc-147">This hierarchy defines the navigation hierarchy in the connected factory dashboard.</span></span> <span data-ttu-id="e60fc-148">Waarden op elk knooppunt van de hiërarchie bepalen van de informatie die wordt weergegeven in het dashboard.</span><span class="sxs-lookup"><span data-stu-id="e60fc-148">Values at each node of the hierarchy determine the information displayed in the dashboard.</span></span> <span data-ttu-id="e60fc-149">Het JSON-bestand bevat bijvoorbeeld de volgende waarden voor de factory München:</span><span class="sxs-lookup"><span data-stu-id="e60fc-149">For example, the JSON file contains the following values for the Munich factory:</span></span>

```json
"Guid": "73B534AE-7C7E-4877-B826-F1C0EA339F65",
"Name": "Munich",
"Description": "Braking system",
"Location": {
    "City": "Munich",
    "Country": "Germany",
    "Latitude": 48.13641,
    "Longitude": 11.57754
},
"Image": "munich.jpg"
```

<span data-ttu-id="e60fc-150">De naam, beschrijving en locatie worden weergegeven op deze weergave in het dashboard:</span><span class="sxs-lookup"><span data-stu-id="e60fc-150">The name, description, and location appear on this view in the dashboard:</span></span>

![München gegevens in het dashboard][img-munich]

<span data-ttu-id="e60fc-152">Elke factory-, productie-lijn- en station hebt een eigenschap van de afbeelding.</span><span class="sxs-lookup"><span data-stu-id="e60fc-152">Each factory, production line, and station have an image property.</span></span> <span data-ttu-id="e60fc-153">U vindt deze JPEG-bestanden in de **Content\img** map in de **WebApp** project.</span><span class="sxs-lookup"><span data-stu-id="e60fc-153">You can find these JPEG files in the **Content\img** folder in the **WebApp** project.</span></span> <span data-ttu-id="e60fc-154">Deze installatiekopiebestanden weergeven in het dashboard verbonden factory.</span><span class="sxs-lookup"><span data-stu-id="e60fc-154">These image files display in the connected factory dashboard.</span></span>

<span data-ttu-id="e60fc-155">Elk station bevat verschillende gedetailleerde eigenschappen waarmee de toewijzing van de gegevens OPC UA items definiëren.</span><span class="sxs-lookup"><span data-stu-id="e60fc-155">Each station includes several detailed properties that define the mapping from the OPC UA data items.</span></span> <span data-ttu-id="e60fc-156">Deze eigenschappen worden beschreven in de volgende secties:</span><span class="sxs-lookup"><span data-stu-id="e60fc-156">These properties are described in the following sections:</span></span>

### <a name="opcuri"></a><span data-ttu-id="e60fc-157">OpcUri</span><span class="sxs-lookup"><span data-stu-id="e60fc-157">OpcUri</span></span>

<span data-ttu-id="e60fc-158">De **OpcUri** waarde is de OPC UA toepassing URI die een unieke identificatie van de OPC UA-server.</span><span class="sxs-lookup"><span data-stu-id="e60fc-158">The **OpcUri** value is the OPC UA Application URI that uniquely identifies the OPC UA server.</span></span> <span data-ttu-id="e60fc-159">Bijvoorbeeld, de **OpcUri** waarde voor de assembly-station op productie regel 1 in München op het volgende lijkt: **urn: scada2194:ua:munich:productionline0:assemblystation**.</span><span class="sxs-lookup"><span data-stu-id="e60fc-159">For example, the **OpcUri** value for the assembly station on production line 1 in Munich looks like the following: **urn:scada2194:ua:munich:productionline0:assemblystation**.</span></span>

<span data-ttu-id="e60fc-160">U kunt de URI's van de gekoppelde OPC UA-servers bekijken in het dashboard van oplossing:</span><span class="sxs-lookup"><span data-stu-id="e60fc-160">You can view the URIs of the connected OPC UA servers in the solution dashboard:</span></span>

![Het OPC UA-server URI's weergeven][img-server-uris]

### <a name="simulation"></a><span data-ttu-id="e60fc-162">Simulatie</span><span class="sxs-lookup"><span data-stu-id="e60fc-162">Simulation</span></span>

<span data-ttu-id="e60fc-163">De informatie in de **simulatie** knooppunt is specifiek voor de simulatie OPC UA die wordt uitgevoerd in de OPC UA-servers die standaard zijn ingericht.</span><span class="sxs-lookup"><span data-stu-id="e60fc-163">The information in the **Simulation** node is specific to the OPC UA simulation that runs in the OPC UA servers that are provisioned by default.</span></span> <span data-ttu-id="e60fc-164">Dit wordt niet gebruikt voor een echte OPC UA-server.</span><span class="sxs-lookup"><span data-stu-id="e60fc-164">It is not used for a real OPC UA server.</span></span>

### <a name="kpi1-and-kpi2"></a><span data-ttu-id="e60fc-165">Kpi1 en Kpi2</span><span class="sxs-lookup"><span data-stu-id="e60fc-165">Kpi1 and Kpi2</span></span>

<span data-ttu-id="e60fc-166">Deze knooppunten wordt beschreven hoe gegevens uit het station draagt bij aan de twee KPI-waarden in het dashboard.</span><span class="sxs-lookup"><span data-stu-id="e60fc-166">These nodes describe how data from the station contributes to the two KPI values in the dashboard.</span></span> <span data-ttu-id="e60fc-167">Deze KPI-waarden zijn in een standaardimplementatie eenheden per uur en kWh per uur.</span><span class="sxs-lookup"><span data-stu-id="e60fc-167">In a default deployment, these KPI values are units per hour and kWh per hour.</span></span> <span data-ttu-id="e60fc-168">De oplossing KPI-waarden op het niveau van een station berekend en ze op het niveau van de factory en productie regel samenvoegt.</span><span class="sxs-lookup"><span data-stu-id="e60fc-168">The solution calculates KPI vales at the level of a station and aggregates them at the production line and factory levels.</span></span>

<span data-ttu-id="e60fc-169">Elke KPI heeft een minimum, maximum- en doel-waarde.</span><span class="sxs-lookup"><span data-stu-id="e60fc-169">Each KPI has a minimum, maximum, and target value.</span></span> <span data-ttu-id="e60fc-170">Elke KPI-waarde kunt ook definiëren voor meldingen voor de verbonden factory-oplossing om uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="e60fc-170">Each KPI value can also define alert actions for the connected factory solution to perform.</span></span> <span data-ttu-id="e60fc-171">Het volgende codefragment bevat de definities van de KPI voor de assembly-station op productie regel 1 in München:</span><span class="sxs-lookup"><span data-stu-id="e60fc-171">The following snippet shows the KPI definitions for the assembly station on production line 1 in Munich:</span></span>

```json
"Kpi1": {
  "Minimum": 150,
  "Target": 300,
  "Maximum": 600
},
"Kpi2": {
  "Minimum": 50,
  "Target": 100,
  "Maximum": 200,
  "MinimumAlertActions": [
    {
      "Type": "None"
    }
  ]
}
```

<span data-ttu-id="e60fc-172">De volgende schermafbeelding ziet de KPI-gegevens in het dashboard.</span><span class="sxs-lookup"><span data-stu-id="e60fc-172">The following screenshot shows the KPI data in the dashboard.</span></span>

![KPI-gegevens in het dashboard][lnk-kpi]

### <a name="opcnodes"></a><span data-ttu-id="e60fc-174">OpcNodes</span><span class="sxs-lookup"><span data-stu-id="e60fc-174">OpcNodes</span></span>

<span data-ttu-id="e60fc-175">De **OpcNodes** knooppunten de gepubliceerde gegevens herstellen vanaf de OPC UA-server en geef het verwerken van die gegevens.</span><span class="sxs-lookup"><span data-stu-id="e60fc-175">The **OpcNodes** nodes identify the published data items from the OPC UA server and specify how to process that data.</span></span>

<span data-ttu-id="e60fc-176">De **NodeId** waarde identificeert de specifieke OPC UA NodeID van de OPC UA-server.</span><span class="sxs-lookup"><span data-stu-id="e60fc-176">The **NodeId** value identifies the specific OPC UA NodeID from the OPC UA server.</span></span> <span data-ttu-id="e60fc-177">Het eerste knooppunt in het station assembly voor productie-regel 1 in München heeft een waarde **ns = 2; ik 385 =**.</span><span class="sxs-lookup"><span data-stu-id="e60fc-177">The first node in the assembly station for production line 1 in Munich has a value **ns=2;i=385**.</span></span> <span data-ttu-id="e60fc-178">Een **NodeId** waarde geeft aan dat het gegevensitem lezen uit de OPC UA-server en de **symbolische naam** biedt een gebruiksvriendelijke naam moet worden gebruikt in het dashboard voor die gegevens.</span><span class="sxs-lookup"><span data-stu-id="e60fc-178">A **NodeId** value specifies the data item to read from the OPC UA server, and the **SymbolicName** provides a user-friendly name to use in the dashboard for that data.</span></span>

<span data-ttu-id="e60fc-179">Andere waarden die zijn gekoppeld aan elk knooppunt worden in de volgende tabel samengevat:</span><span class="sxs-lookup"><span data-stu-id="e60fc-179">Other values associated with each node are summarized in the following table:</span></span>

| <span data-ttu-id="e60fc-180">Waarde</span><span class="sxs-lookup"><span data-stu-id="e60fc-180">Value</span></span> | <span data-ttu-id="e60fc-181">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e60fc-181">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="e60fc-182">Relevantie</span><span class="sxs-lookup"><span data-stu-id="e60fc-182">Relevance</span></span>  | <span data-ttu-id="e60fc-183">Waarden voor de KPI en OEE deze gegevens draagt bij aan.</span><span class="sxs-lookup"><span data-stu-id="e60fc-183">The KPI and OEE values this data contributes to.</span></span> |
| <span data-ttu-id="e60fc-184">OpCode</span><span class="sxs-lookup"><span data-stu-id="e60fc-184">OpCode</span></span>     | <span data-ttu-id="e60fc-185">Hoe de gegevens worden samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="e60fc-185">How the data is aggregated.</span></span> |
| <span data-ttu-id="e60fc-186">Eenheden</span><span class="sxs-lookup"><span data-stu-id="e60fc-186">Units</span></span>      | <span data-ttu-id="e60fc-187">De eenheden die worden gebruikt in het dashboard.</span><span class="sxs-lookup"><span data-stu-id="e60fc-187">The units to use in the dashboard.</span></span>  |
| <span data-ttu-id="e60fc-188">Zichtbaar</span><span class="sxs-lookup"><span data-stu-id="e60fc-188">Visible</span></span>    | <span data-ttu-id="e60fc-189">Of u wilt weergeven van deze waarde in het dashboard.</span><span class="sxs-lookup"><span data-stu-id="e60fc-189">Whether to display this value in the dashboard.</span></span> <span data-ttu-id="e60fc-190">Sommige waarden worden gebruikt voor berekeningen, maar niet weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e60fc-190">Some values are used in calculations but not displayed.</span></span>  |
| <span data-ttu-id="e60fc-191">Maximum</span><span class="sxs-lookup"><span data-stu-id="e60fc-191">Maximum</span></span>    | <span data-ttu-id="e60fc-192">De maximumwaarde die een waarschuwing in het dashboard.</span><span class="sxs-lookup"><span data-stu-id="e60fc-192">The maximum value that triggers an alert in the dashboard.</span></span> |
| <span data-ttu-id="e60fc-193">MaximumAlertActions</span><span class="sxs-lookup"><span data-stu-id="e60fc-193">MaximumAlertActions</span></span> | <span data-ttu-id="e60fc-194">Een actie moet worden uitgevoerd in reactie op een waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="e60fc-194">An action to take in response to an alert.</span></span> <span data-ttu-id="e60fc-195">Bijvoorbeeld: een opdracht verzenden naar een station.</span><span class="sxs-lookup"><span data-stu-id="e60fc-195">For example, send a command to a station.</span></span> |
| <span data-ttu-id="e60fc-196">ConstValue</span><span class="sxs-lookup"><span data-stu-id="e60fc-196">ConstValue</span></span> | <span data-ttu-id="e60fc-197">Een constante waarde die wordt gebruikt in een berekening.</span><span class="sxs-lookup"><span data-stu-id="e60fc-197">A constant value used in a calculation.</span></span> |

## <a name="deploy-the-changes"></a><span data-ttu-id="e60fc-198">De wijzigingen te implementeren</span><span class="sxs-lookup"><span data-stu-id="e60fc-198">Deploy the changes</span></span>

<span data-ttu-id="e60fc-199">Wanneer u klaar bent met het aanbrengen van wijzigingen naar de **ContosoTopologyDescription.json** -bestand, moet u de oplossing verbonden factory opnieuw implementeren bij uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="e60fc-199">When you have finished making changes to the **ContosoTopologyDescription.json** file, you must redeploy the connected factory solution to your Azure account.</span></span>

<span data-ttu-id="e60fc-200">De **azure-iot-verbonden-factory** opslagplaats bevat een **build.ps1** PowerShell-script die u gebruiken kunt om te bouwen en implementeren van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="e60fc-200">The **azure-iot-connected-factory** repository includes a **build.ps1** PowerShell script you can use to rebuild and deploy the solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e60fc-201">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e60fc-201">Next Steps</span></span>

<span data-ttu-id="e60fc-202">Meer informatie over de verbonden factory vooraf geconfigureerde oplossing door te lezen van de volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="e60fc-202">Learn more about the connected factory preconfigured solution by reading the following articles:</span></span>

* <span data-ttu-id="e60fc-203">[Overzicht van de vooraf geconfigureerde oplossing voor verbonden factory's][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="e60fc-203">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="e60fc-204">[Implementeer een gateway voor verbonden factory][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="e60fc-204">[Deploy a gateway for connected factory][lnk-connect-cf]</span></span>
* <span data-ttu-id="e60fc-205">[Machtigingen op de site azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="e60fc-205">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="e60fc-206">Veelgestelde vragen over verbonden factory's</span><span class="sxs-lookup"><span data-stu-id="e60fc-206">Connected factory FAQ</span></span>](iot-suite-faq-cf.md)
* <span data-ttu-id="e60fc-207">[FAQ][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="e60fc-207">[FAQ][lnk-faq]</span></span>


[img-oee-kpi]: ./media/iot-suite-connected-factory-customize/oeenadkpi.png
[img-manufactured-items]: ./media/iot-suite-connected-factory-customize/manufactured.png
[img-tsi]: ./media/iot-suite-connected-factory-customize/tsi.png
[img-select-server]: ./media/iot-suite-connected-factory-customize/selectserver.png
[img-published]: ./media/iot-suite-connected-factory-customize/published.png
[img-munich]: ./media/iot-suite-connected-factory-customize/munich.png
[img-server-uris]: ./media/iot-suite-connected-factory-customize/serveruris.png
[lnk-kpi]: ./media/iot-suite-connected-factory-customize/kpidisplay.png

[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md