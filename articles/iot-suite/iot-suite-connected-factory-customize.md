---
title: Azure IoT Suite aaaCustomize verbonden factory | Microsoft Docs
description: Een beschrijving van hoe toocustomize Hallo gedrag van Hallo factory verbonden vooraf geconfigureerde oplossing.
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
ms.openlocfilehash: 53f2fef7a76b5d8e6ad023945a7812dc7fabd12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-how-hello-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a><span data-ttu-id="c0302-103">Aanpassen hoe Hallo factory oplossing geeft gegevens van uw servers OPC UA verbonden</span><span class="sxs-lookup"><span data-stu-id="c0302-103">Customize how hello connected factory solution displays data from your OPC UA servers</span></span>

## <a name="introduction"></a><span data-ttu-id="c0302-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="c0302-104">Introduction</span></span>

<span data-ttu-id="c0302-105">Hallo verbonden factory oplossing samenvoegt en gegevens uit Hallo OPC UA servers verbonden toohello oplossing worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c0302-105">hello connected factory solution aggregates and displays data from hello OPC UA servers connected toohello solution.</span></span> <span data-ttu-id="c0302-106">U kunt bladeren en het verzenden van de opdrachten toohello OPC UA servers in uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="c0302-106">You can browse and send commands toohello OPC UA servers in your solution.</span></span> <span data-ttu-id="c0302-107">Zie voor meer informatie over OPC UA Hallo [verbonden factory Veelgestelde vragen over](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="c0302-107">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

<span data-ttu-id="c0302-108">Voorbeelden van geaggregeerde gegevens in het Hallo-oplossing zijn Hallo algehele apparatuur efficiëntie (OEE) en de Key Performance Indicators (KPI's) die u in het Hallo-dashboard Hallo factory-, lijn- en station niveaus bekijken kunt.</span><span class="sxs-lookup"><span data-stu-id="c0302-108">Examples of aggregated data in hello solution include hello Overall Equipment Efficiency (OEE) and Key Performance Indicators (KPIs) that you can view in hello dashboard at hello factory, line, and station levels.</span></span> <span data-ttu-id="c0302-109">Hallo volgende schermafbeelding ziet u Hallo OEE en KPI-waarden voor Hallo **Assembly** station op **productie-regel 1**, in Hallo **München** factory:</span><span class="sxs-lookup"><span data-stu-id="c0302-109">hello following screenshot shows hello OEE and KPI values for hello **Assembly** station, on **Production line 1**, in hello **Munich** factory:</span></span>

![Voorbeeld van OEE en KPI waarden in Hallo-oplossing][img-oee-kpi]

<span data-ttu-id="c0302-111">Hallo-oplossing kunt u tooview gedetailleerde gegevens van specifieke gegevensitems uit Hallo OPC UA-servers, zogenaamde *stations*.</span><span class="sxs-lookup"><span data-stu-id="c0302-111">hello solution enables you tooview detailed information from specific data items from hello OPC UA servers, called *stations*.</span></span> <span data-ttu-id="c0302-112">Hallo ziet volgende schermafbeelding curve van Hallo aantal geproduceerde items van een specifiek station:</span><span class="sxs-lookup"><span data-stu-id="c0302-112">hello following screenshot shows plots of hello number of manufactured items from a specific station:</span></span>

![Curve van het aantal geproduceerde artikelen][img-manufactured-items]

<span data-ttu-id="c0302-114">Als u klikt op een van de grafieken hello, vindt u Hallo gegevens verder met Time Series Insights (TSI):</span><span class="sxs-lookup"><span data-stu-id="c0302-114">If you click one of hello graphs, you can explore hello data further using Time Series Insights (TSI):</span></span>

![Gegevens met behulp van de Time Series Insights verkennen][img-tsi]

<span data-ttu-id="c0302-116">Dit artikel wordt beschreven:</span><span class="sxs-lookup"><span data-stu-id="c0302-116">This article describes:</span></span>

- <span data-ttu-id="c0302-117">Hoe bestaat gegevens Hallo beschikbaar toohello verschillende weergaven in Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="c0302-117">How hello data is made available toohello various views in hello solution.</span></span>
- <span data-ttu-id="c0302-118">Het aanpassen van Hallo manier Hallo oplossing Hallo gegevens weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c0302-118">How you can customize hello way hello solution displays hello data.</span></span>

## <a name="data-sources"></a><span data-ttu-id="c0302-119">Gegevensbronnen</span><span class="sxs-lookup"><span data-stu-id="c0302-119">Data sources</span></span>

<span data-ttu-id="c0302-120">Hallo verbonden factory-oplossing worden gegevens uit Hallo OPC UA servers verbonden toohello oplossing.</span><span class="sxs-lookup"><span data-stu-id="c0302-120">hello connected factory solution displays data from hello OPC UA servers connected toohello solution.</span></span> <span data-ttu-id="c0302-121">Hallo standaardinstallatie bevat verschillende OPC UA-servers met een factory simulatie.</span><span class="sxs-lookup"><span data-stu-id="c0302-121">hello default installation includes several OPC UA servers running a factory simulation.</span></span> <span data-ttu-id="c0302-122">U kunt uw eigen servers OPC UA toevoegen die [verbinding maken via een gateway] [ lnk-connect-cf] tooyour oplossing.</span><span class="sxs-lookup"><span data-stu-id="c0302-122">You can add your own OPC UA servers that [connect through a gateway][lnk-connect-cf] tooyour solution.</span></span>

<span data-ttu-id="c0302-123">U kunt bladeren Hallo gegevensitems verbonden OPC UA-server kunt tooyour oplossing in een dashboard Hallo verzenden:</span><span class="sxs-lookup"><span data-stu-id="c0302-123">You can browse hello data items that a connected OPC UA server can send tooyour solution in hello dashboard:</span></span>

1. <span data-ttu-id="c0302-124">Navigeer toohello **selecteert u een server OPC UA** weergeven:</span><span class="sxs-lookup"><span data-stu-id="c0302-124">Navigate toohello **Select an OPC UA server** view:</span></span>

    ![Selecteer een weergave van de server OPC UA toohello navigeren][img-select-server]

1. <span data-ttu-id="c0302-126">Selecteer een server en klik op **Connect**.</span><span class="sxs-lookup"><span data-stu-id="c0302-126">Select a server and click **Connect**.</span></span> <span data-ttu-id="c0302-127">Klik op **doorgaan** wanneer Hallo beveiligingswaarschuwing wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c0302-127">Click **Proceed** when hello security warning appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c0302-128">Deze waarschuwing alleen verschijnt eenmaal voor elke server en er wordt een vertrouwensrelatie tussen Hallo oplossing dashboard en Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="c0302-128">This warning only appears once for each server and establishes a trust relationship between hello solution dashboard and hello server.</span></span>

1. <span data-ttu-id="c0302-129">U kunt nu bladeren Hallo-gegevensitems die server Hallo toohello oplossing kunnen verzenden.</span><span class="sxs-lookup"><span data-stu-id="c0302-129">You can now browse hello data items that hello server can send toohello solution.</span></span> <span data-ttu-id="c0302-130">Items die worden verzonden toohello oplossing hebben een groen vinkje:</span><span class="sxs-lookup"><span data-stu-id="c0302-130">Items that are being sent toohello solution have a green check mark:</span></span>

    ![Gepubliceerde items][img-published]

1. <span data-ttu-id="c0302-132">Als u een *beheerder* in Hallo-oplossing, kunt u toopublish een item gegevens toomake deze beschikbaar zijn in Hallo verbonden factory-oplossing.</span><span class="sxs-lookup"><span data-stu-id="c0302-132">If you are an *Administrator* in hello solution, you can choose toopublish a data item toomake it available in hello connected factory solution.</span></span> <span data-ttu-id="c0302-133">U kunt ook Hallo-waarde van gegevensitems wijzigen en methoden aanroepen in Hallo OPC UA-server als beheerder.</span><span class="sxs-lookup"><span data-stu-id="c0302-133">As an Administrator, you can also change hello value of data items and call methods in hello OPC UA server.</span></span>

## <a name="map-hello-data"></a><span data-ttu-id="c0302-134">Hallo kaartgegevens</span><span class="sxs-lookup"><span data-stu-id="c0302-134">Map hello data</span></span>

<span data-ttu-id="c0302-135">Hallo verbonden factory oplossing maps en statistische functies Hallo gepubliceerde gegevensitems van Hallo OPC UA-server toohello verschillende weergaven in Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="c0302-135">hello connected factory solution maps and aggregates hello published data items from hello OPC UA server toohello various views in hello solution.</span></span> <span data-ttu-id="c0302-136">Hallo implementeert verbonden factory-oplossing tooyour Azure-account wanneer u Hallo oplossing inricht.</span><span class="sxs-lookup"><span data-stu-id="c0302-136">hello connected factory solution deploys tooyour Azure account when you provision hello solution.</span></span> <span data-ttu-id="c0302-137">Een JSON-bestand in Visual Studio verbonden factory-oplossing Hallo slaat deze informatie over de Identiteitstoewijzing.</span><span class="sxs-lookup"><span data-stu-id="c0302-137">A JSON file in hello Visual Studio connected factory solution stores this mapping information.</span></span> <span data-ttu-id="c0302-138">U kunt weergeven en wijzigen van dit JSON-configuratiebestand in Hallo verbonden fabriek Visual Studio-oplossing.</span><span class="sxs-lookup"><span data-stu-id="c0302-138">You can view and modify this JSON configuration file in hello connected factory Visual Studio solution.</span></span> <span data-ttu-id="c0302-139">U kunt de Hallo oplossing opnieuw te implementeren nadat u een wijziging aanbrengt.</span><span class="sxs-lookup"><span data-stu-id="c0302-139">You can redeploy hello solution after you make a change.</span></span>

<span data-ttu-id="c0302-140">U kunt Hallo-configuratiebestand te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="c0302-140">You can use hello configuration file to:</span></span>

- <span data-ttu-id="c0302-141">Hallo bestaande gesimuleerde fabrieken, de regels voor productie en de stations bewerken.</span><span class="sxs-lookup"><span data-stu-id="c0302-141">Edit hello existing simulated factories, production lines, and stations.</span></span>
- <span data-ttu-id="c0302-142">Gegevens van echte OPC UA-servers dat u verbinding toohello oplossing maakt toewijzen.</span><span class="sxs-lookup"><span data-stu-id="c0302-142">Map data from real OPC UA servers that you connect toohello solution.</span></span>

<span data-ttu-id="c0302-143">een kopie van Hallo tooclone verbonden factory Visual Studio-oplossing, gebruik Hallo volgende git-opdracht:</span><span class="sxs-lookup"><span data-stu-id="c0302-143">tooclone a copy of hello connected factory Visual Studio solution, use hello following git command:</span></span>

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

<span data-ttu-id="c0302-144">Hallo bestand **ContosoTopologyDescription.json** Hallo toewijzing van Hallo OPC UA-servergegevens items toohello weergaven in Hallo verbonden factory oplossing dashboard definieert.</span><span class="sxs-lookup"><span data-stu-id="c0302-144">hello file **ContosoTopologyDescription.json** defines hello mapping from hello OPC UA server data items toohello views in hello connected factory solution dashboard.</span></span> <span data-ttu-id="c0302-145">U vindt dit configuratiebestand in Hallo **Contoso\Topology** map in Hallo **WebApp** -project in Visual Studio-oplossing Hallo.</span><span class="sxs-lookup"><span data-stu-id="c0302-145">You can find this configuration file in hello **Contoso\Topology** folder in hello **WebApp** project in hello Visual Studio solution.</span></span>

<span data-ttu-id="c0302-146">Hallo-inhoud van het Hallo JSON-bestand is ingedeeld als een hiërarchie van de factory-, productie-lijn- en station knooppunten.</span><span class="sxs-lookup"><span data-stu-id="c0302-146">hello content of hello JSON file is organized as a hierarchy of factory, production line, and station nodes.</span></span> <span data-ttu-id="c0302-147">Deze hiërarchie definieert Hallo navigatiehiërarchie in Hallo verbonden factory dashboard.</span><span class="sxs-lookup"><span data-stu-id="c0302-147">This hierarchy defines hello navigation hierarchy in hello connected factory dashboard.</span></span> <span data-ttu-id="c0302-148">Waarden op elk knooppunt van de hiërarchie Hallo bepalen Hallo informatie die wordt weergegeven in het Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="c0302-148">Values at each node of hello hierarchy determine hello information displayed in hello dashboard.</span></span> <span data-ttu-id="c0302-149">Hallo JSON-bestand bevat bijvoorbeeld Hallo waarden voor Hallo München factory te volgen:</span><span class="sxs-lookup"><span data-stu-id="c0302-149">For example, hello JSON file contains hello following values for hello Munich factory:</span></span>

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

<span data-ttu-id="c0302-150">Hallo-naam, beschrijving en locatie worden weergegeven op deze weergave in Hallo dashboard:</span><span class="sxs-lookup"><span data-stu-id="c0302-150">hello name, description, and location appear on this view in hello dashboard:</span></span>

![München gegevens in Hallo-dashboard][img-munich]

<span data-ttu-id="c0302-152">Elke factory-, productie-lijn- en station hebt een eigenschap van de afbeelding.</span><span class="sxs-lookup"><span data-stu-id="c0302-152">Each factory, production line, and station have an image property.</span></span> <span data-ttu-id="c0302-153">U vindt deze JPEG-bestanden in Hallo **Content\img** map in Hallo **WebApp** project.</span><span class="sxs-lookup"><span data-stu-id="c0302-153">You can find these JPEG files in hello **Content\img** folder in hello **WebApp** project.</span></span> <span data-ttu-id="c0302-154">Deze installatiekopiebestanden weergeven in Hallo verbonden factory dashboard.</span><span class="sxs-lookup"><span data-stu-id="c0302-154">These image files display in hello connected factory dashboard.</span></span>

<span data-ttu-id="c0302-155">Elk station bevat verschillende gedetailleerde eigenschappen waarmee Hallo toewijzing van Hallo OPC UA gegevensitems definiëren.</span><span class="sxs-lookup"><span data-stu-id="c0302-155">Each station includes several detailed properties that define hello mapping from hello OPC UA data items.</span></span> <span data-ttu-id="c0302-156">Deze eigenschappen worden beschreven in Hallo uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="c0302-156">These properties are described in hello following sections:</span></span>

### <a name="opcuri"></a><span data-ttu-id="c0302-157">OpcUri</span><span class="sxs-lookup"><span data-stu-id="c0302-157">OpcUri</span></span>

<span data-ttu-id="c0302-158">Hallo **OpcUri** waarde Hallo OPC UA toepassing URI die een unieke identificatie van Hallo OPC UA-server is.</span><span class="sxs-lookup"><span data-stu-id="c0302-158">hello **OpcUri** value is hello OPC UA Application URI that uniquely identifies hello OPC UA server.</span></span> <span data-ttu-id="c0302-159">Bijvoorbeeld, Hallo **OpcUri** Hallo assembly station op productie regel 1 in München ziet eruit als Hallo volgende waarde: **urn: scada2194:ua:munich:productionline0:assemblystation**.</span><span class="sxs-lookup"><span data-stu-id="c0302-159">For example, hello **OpcUri** value for hello assembly station on production line 1 in Munich looks like hello following: **urn:scada2194:ua:munich:productionline0:assemblystation**.</span></span>

<span data-ttu-id="c0302-160">Hallo URI's van Hallo verbonden OPC UA servers vindt u in het dashboard van de oplossing Hallo:</span><span class="sxs-lookup"><span data-stu-id="c0302-160">You can view hello URIs of hello connected OPC UA servers in hello solution dashboard:</span></span>

![Het OPC UA-server URI's weergeven][img-server-uris]

### <a name="simulation"></a><span data-ttu-id="c0302-162">Simulatie</span><span class="sxs-lookup"><span data-stu-id="c0302-162">Simulation</span></span>

<span data-ttu-id="c0302-163">informatie in Hallo Hallo **simulatie** knooppunt is specifiek toohello OPC UA simulatie die wordt uitgevoerd in Hallo OPC UA-servers die standaard zijn ingericht.</span><span class="sxs-lookup"><span data-stu-id="c0302-163">hello information in hello **Simulation** node is specific toohello OPC UA simulation that runs in hello OPC UA servers that are provisioned by default.</span></span> <span data-ttu-id="c0302-164">Dit wordt niet gebruikt voor een echte OPC UA-server.</span><span class="sxs-lookup"><span data-stu-id="c0302-164">It is not used for a real OPC UA server.</span></span>

### <a name="kpi1-and-kpi2"></a><span data-ttu-id="c0302-165">Kpi1 en Kpi2</span><span class="sxs-lookup"><span data-stu-id="c0302-165">Kpi1 and Kpi2</span></span>

<span data-ttu-id="c0302-166">Deze knooppunten wordt beschreven hoe gegevens van Hallo station bijdraagt toohello twee KPI-waarden in Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="c0302-166">These nodes describe how data from hello station contributes toohello two KPI values in hello dashboard.</span></span> <span data-ttu-id="c0302-167">Deze KPI-waarden zijn in een standaardimplementatie eenheden per uur en kWh per uur.</span><span class="sxs-lookup"><span data-stu-id="c0302-167">In a default deployment, these KPI values are units per hour and kWh per hour.</span></span> <span data-ttu-id="c0302-168">Hallo oplossing berekent de waarden van de KPI op Hallo niveau van een station en ze aggregeert Hallo productieregel en factory niveaus.</span><span class="sxs-lookup"><span data-stu-id="c0302-168">hello solution calculates KPI vales at hello level of a station and aggregates them at hello production line and factory levels.</span></span>

<span data-ttu-id="c0302-169">Elke KPI heeft een minimum, maximum- en doel-waarde.</span><span class="sxs-lookup"><span data-stu-id="c0302-169">Each KPI has a minimum, maximum, and target value.</span></span> <span data-ttu-id="c0302-170">Elke KPI-waarde kunt ook meldingen voor Hallo verbonden factory oplossing tooperform definiëren.</span><span class="sxs-lookup"><span data-stu-id="c0302-170">Each KPI value can also define alert actions for hello connected factory solution tooperform.</span></span> <span data-ttu-id="c0302-171">Hallo volgende fragment toont Hallo KPI definities voor Hallo assembly station op productie-regel 1 in München:</span><span class="sxs-lookup"><span data-stu-id="c0302-171">hello following snippet shows hello KPI definitions for hello assembly station on production line 1 in Munich:</span></span>

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

<span data-ttu-id="c0302-172">Hallo volgende schermafbeelding ziet u Hallo KPI-gegevens in Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="c0302-172">hello following screenshot shows hello KPI data in hello dashboard.</span></span>

![KPI-gegevens in Hallo-dashboard][lnk-kpi]

### <a name="opcnodes"></a><span data-ttu-id="c0302-174">OpcNodes</span><span class="sxs-lookup"><span data-stu-id="c0302-174">OpcNodes</span></span>

<span data-ttu-id="c0302-175">Hallo **OpcNodes** knooppunten identificeren Hallo gepubliceerde-gegevensitems van Hallo OPC UA-server en opgeven hoe tooprocess die gegevens.</span><span class="sxs-lookup"><span data-stu-id="c0302-175">hello **OpcNodes** nodes identify hello published data items from hello OPC UA server and specify how tooprocess that data.</span></span>

<span data-ttu-id="c0302-176">Hallo **NodeId** waarde identificeert Hallo specifieke OPC UA NodeID van Hallo OPC UA-server.</span><span class="sxs-lookup"><span data-stu-id="c0302-176">hello **NodeId** value identifies hello specific OPC UA NodeID from hello OPC UA server.</span></span> <span data-ttu-id="c0302-177">Hallo eerste knooppunt in Hallo assembly station voor productie-regel 1 in München heeft een waarde **ns = 2; ik 385 =**.</span><span class="sxs-lookup"><span data-stu-id="c0302-177">hello first node in hello assembly station for production line 1 in Munich has a value **ns=2;i=385**.</span></span> <span data-ttu-id="c0302-178">Een **NodeId** waarde geeft aan Hallo gegevens item tooread van Hallo OPC UA-server en Hallo **symbolische naam** biedt een gebruiksvriendelijke naam toouse in Hallo dashboard voor die gegevens.</span><span class="sxs-lookup"><span data-stu-id="c0302-178">A **NodeId** value specifies hello data item tooread from hello OPC UA server, and hello **SymbolicName** provides a user-friendly name toouse in hello dashboard for that data.</span></span>

<span data-ttu-id="c0302-179">Andere waarden die zijn gekoppeld aan elk knooppunt worden samengevat in de volgende tabel Hallo:</span><span class="sxs-lookup"><span data-stu-id="c0302-179">Other values associated with each node are summarized in hello following table:</span></span>

| <span data-ttu-id="c0302-180">Waarde</span><span class="sxs-lookup"><span data-stu-id="c0302-180">Value</span></span> | <span data-ttu-id="c0302-181">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c0302-181">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="c0302-182">Relevantie</span><span class="sxs-lookup"><span data-stu-id="c0302-182">Relevance</span></span>  | <span data-ttu-id="c0302-183">Hallo KPI en OEE waarden deze gegevens draagt bij aan.</span><span class="sxs-lookup"><span data-stu-id="c0302-183">hello KPI and OEE values this data contributes to.</span></span> |
| <span data-ttu-id="c0302-184">OpCode</span><span class="sxs-lookup"><span data-stu-id="c0302-184">OpCode</span></span>     | <span data-ttu-id="c0302-185">Hoe Hallo gegevens worden samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="c0302-185">How hello data is aggregated.</span></span> |
| <span data-ttu-id="c0302-186">Eenheden</span><span class="sxs-lookup"><span data-stu-id="c0302-186">Units</span></span>      | <span data-ttu-id="c0302-187">Hallo eenheden toouse in Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="c0302-187">hello units toouse in hello dashboard.</span></span>  |
| <span data-ttu-id="c0302-188">Zichtbaar</span><span class="sxs-lookup"><span data-stu-id="c0302-188">Visible</span></span>    | <span data-ttu-id="c0302-189">Of toodisplay deze waarde in Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="c0302-189">Whether toodisplay this value in hello dashboard.</span></span> <span data-ttu-id="c0302-190">Sommige waarden worden gebruikt voor berekeningen, maar niet weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c0302-190">Some values are used in calculations but not displayed.</span></span>  |
| <span data-ttu-id="c0302-191">Maximum</span><span class="sxs-lookup"><span data-stu-id="c0302-191">Maximum</span></span>    | <span data-ttu-id="c0302-192">Hallo maximumwaarde die een waarschuwing in Hallo dashboard activeert.</span><span class="sxs-lookup"><span data-stu-id="c0302-192">hello maximum value that triggers an alert in hello dashboard.</span></span> |
| <span data-ttu-id="c0302-193">MaximumAlertActions</span><span class="sxs-lookup"><span data-stu-id="c0302-193">MaximumAlertActions</span></span> | <span data-ttu-id="c0302-194">Een actie tootake in antwoord tooan waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="c0302-194">An action tootake in response tooan alert.</span></span> <span data-ttu-id="c0302-195">Bijvoorbeeld: een opdracht tooa station verzenden.</span><span class="sxs-lookup"><span data-stu-id="c0302-195">For example, send a command tooa station.</span></span> |
| <span data-ttu-id="c0302-196">ConstValue</span><span class="sxs-lookup"><span data-stu-id="c0302-196">ConstValue</span></span> | <span data-ttu-id="c0302-197">Een constante waarde die wordt gebruikt in een berekening.</span><span class="sxs-lookup"><span data-stu-id="c0302-197">A constant value used in a calculation.</span></span> |

## <a name="deploy-hello-changes"></a><span data-ttu-id="c0302-198">Hallo wijzigingen implementeren</span><span class="sxs-lookup"><span data-stu-id="c0302-198">Deploy hello changes</span></span>

<span data-ttu-id="c0302-199">Wanneer u toohello wijzigingen hebt aangebracht **ContosoTopologyDescription.json** -bestand, die u moet implementeren Hallo verbonden factory oplossing tooyour Azure-account.</span><span class="sxs-lookup"><span data-stu-id="c0302-199">When you have finished making changes toohello **ContosoTopologyDescription.json** file, you must redeploy hello connected factory solution tooyour Azure account.</span></span>

<span data-ttu-id="c0302-200">Hallo **azure-iot-verbonden-factory** opslagplaats bevat een **build.ps1** PowerShell-script kunt u toorebuild gebruiken en Hallo oplossing implementeren.</span><span class="sxs-lookup"><span data-stu-id="c0302-200">hello **azure-iot-connected-factory** repository includes a **build.ps1** PowerShell script you can use toorebuild and deploy hello solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0302-201">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c0302-201">Next Steps</span></span>

<span data-ttu-id="c0302-202">Meer informatie over Hallo verbonden factory vooraf geconfigureerde oplossing door lezen Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c0302-202">Learn more about hello connected factory preconfigured solution by reading hello following articles:</span></span>

* <span data-ttu-id="c0302-203">[Overzicht van de vooraf geconfigureerde oplossing voor verbonden factory's][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="c0302-203">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="c0302-204">[Implementeer een gateway voor verbonden factory][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="c0302-204">[Deploy a gateway for connected factory][lnk-connect-cf]</span></span>
* <span data-ttu-id="c0302-205">[Machtigingen op Hallo azureiotsuite.com site][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="c0302-205">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="c0302-206">Veelgestelde vragen over verbonden factory's</span><span class="sxs-lookup"><span data-stu-id="c0302-206">Connected factory FAQ</span></span>](iot-suite-faq-cf.md)
* <span data-ttu-id="c0302-207">[FAQ][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="c0302-207">[FAQ][lnk-faq]</span></span>


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