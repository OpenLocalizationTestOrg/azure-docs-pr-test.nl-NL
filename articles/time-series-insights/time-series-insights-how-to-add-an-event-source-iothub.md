---
title: aaaHow tooadd een IoT Hub gebeurtenis tooyour Azure Time Series Insights bronomgeving | Microsoft Docs
description: Deze zelfstudie bevat informatie over hoe een gebeurtenis die bron tooadd tooan IoT Hub tooyour Time Series Insights omgeving verbonden
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: c626f9653d1c012360120fa9fc3d211d7d5beb5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-an-iot-hub-event-source"></a><span data-ttu-id="cca30-103">Hoe tooadd een gebeurtenisbron IoT-Hub</span><span class="sxs-lookup"><span data-stu-id="cca30-103">How tooadd an IoT Hub event source</span></span>

<span data-ttu-id="cca30-104">Deze zelfstudie bevat informatie over hoe toouse hello Azure portal tooadd een gebeurtenisbron die uit een IoT Hub tooyour Time Series Insights-omgeving kan lezen.</span><span class="sxs-lookup"><span data-stu-id="cca30-104">This tutorial covers how toouse hello Azure portal tooadd an event source that reads from an IoT Hub tooyour Time Series Insights environment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cca30-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cca30-105">Prerequisites</span></span>

<span data-ttu-id="cca30-106">U hebt een IoT-Hub gemaakt en gebeurtenissen tooit schrijft.</span><span class="sxs-lookup"><span data-stu-id="cca30-106">You have created an IoT Hub and are writing events tooit.</span></span> <span data-ttu-id="cca30-107">Zie voor meer informatie over IoT Hubs <https://azure.microsoft.com/services/iot-hub/></span><span class="sxs-lookup"><span data-stu-id="cca30-107">For more information on IoT Hubs, see <https://azure.microsoft.com/services/iot-hub/></span></span>

> <span data-ttu-id="cca30-108">[Consumergroepen] Elke keer reeks Insights gebeurtenisbron moet toohave zijn eigen speciale klantengroep die niet wordt gedeeld met andere consumenten.</span><span class="sxs-lookup"><span data-stu-id="cca30-108">[Consumer Groups] Each Time Series Insights event source needs toohave its own dedicated consumer group that is not shared with any other consumers.</span></span> <span data-ttu-id="cca30-109">Als meerdere lezers verbruiken gebeurtenissen van dezelfde consumergroep hello, kunnen alle lezers waarschijnlijk toosee fouten.</span><span class="sxs-lookup"><span data-stu-id="cca30-109">If multiple readers consume events from hello same consumer group, all readers are likely toosee failures.</span></span> <span data-ttu-id="cca30-110">Zie voor meer informatie, Hallo [Ontwikkelaarshandleiding voor IoT Hub](../iot-hub/iot-hub-devguide.md).</span><span class="sxs-lookup"><span data-stu-id="cca30-110">For details, see hello [IoT Hub developer guide](../iot-hub/iot-hub-devguide.md).</span></span>

## <a name="choose-an-import-option"></a><span data-ttu-id="cca30-111">Kies een optie importeren</span><span class="sxs-lookup"><span data-stu-id="cca30-111">Choose an Import option</span></span>

<span data-ttu-id="cca30-112">Hallo-instellingen voor de gebeurtenisbron Hallo kunnen handmatig worden ingevoerd of een IoT-hub kan worden geselecteerd uit Hallo IoT hubs die tooyou beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="cca30-112">hello settings for hello event source can be entered manually or an IoT hub can be selected from hello IoT hubs that are available tooyou.</span></span>
<span data-ttu-id="cca30-113">In Hallo **optie importeren** selector een Hallo volgende opties kiezen:</span><span class="sxs-lookup"><span data-stu-id="cca30-113">In hello **Import Option** selector, choose one of hello following options:</span></span>

* <span data-ttu-id="cca30-114">Geef de IoT Hub-instellingen handmatig</span><span class="sxs-lookup"><span data-stu-id="cca30-114">Provide IoT Hub settings manually</span></span>
* <span data-ttu-id="cca30-115">Gebruik IoT Hub uit de beschikbare abonnementen</span><span class="sxs-lookup"><span data-stu-id="cca30-115">Use IoT Hub from available subscriptions</span></span>

### <a name="select-an-available-iot-hub"></a><span data-ttu-id="cca30-116">Selecteer een beschikbare IoT-Hub</span><span class="sxs-lookup"><span data-stu-id="cca30-116">Select an available IoT Hub</span></span>

<span data-ttu-id="cca30-117">Hallo volgende tabel bevat uitleg over elke optie Hallo nieuwe gebeurtenisbron tabblad met de beschrijving bij het selecteren van een IoT-Hub beschikbaar als een gebeurtenisbron:</span><span class="sxs-lookup"><span data-stu-id="cca30-117">hello following table explains each option in hello New Event Source tab with its description when selecting an available IoT Hub as an event source:</span></span>

| <span data-ttu-id="cca30-118">DE NAAM VAN EIGENSCHAP</span><span class="sxs-lookup"><span data-stu-id="cca30-118">PROPERTY NAME</span></span> | <span data-ttu-id="cca30-119">BESCHRIJVING</span><span class="sxs-lookup"><span data-stu-id="cca30-119">DESCRIPTION</span></span> |
| --- | --- |
| <span data-ttu-id="cca30-120">De naam van de gebeurtenis-bron</span><span class="sxs-lookup"><span data-stu-id="cca30-120">Event source name</span></span> | <span data-ttu-id="cca30-121">Hallo-naam van de gebeurtenisbron.</span><span class="sxs-lookup"><span data-stu-id="cca30-121">hello name of your event source.</span></span> <span data-ttu-id="cca30-122">Deze naam moet uniek zijn binnen uw omgeving Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="cca30-122">This name must be unique within your Time Series Insights environment.</span></span>
| <span data-ttu-id="cca30-123">Bron</span><span class="sxs-lookup"><span data-stu-id="cca30-123">Source</span></span> | <span data-ttu-id="cca30-124">Kies **IoT Hub** toocreate een gebeurtenisbron IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cca30-124">Choose **IoT Hub** toocreate an IoT Hub event source.</span></span>
| <span data-ttu-id="cca30-125">Abonnements-Id</span><span class="sxs-lookup"><span data-stu-id="cca30-125">Subscription Id</span></span> | <span data-ttu-id="cca30-126">Selecteer Hallo abonnement waarin deze iothub is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cca30-126">Select hello subscription in which this IoT hub was created.</span></span>
| <span data-ttu-id="cca30-127">De naam van de IoT-hub</span><span class="sxs-lookup"><span data-stu-id="cca30-127">IoT hub name</span></span> | <span data-ttu-id="cca30-128">Selecteer de naam Hallo Hallo IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cca30-128">Select hello name of hello IoT Hub.</span></span>
| <span data-ttu-id="cca30-129">Naam voor het IoT-hub</span><span class="sxs-lookup"><span data-stu-id="cca30-129">IoT hub policy name</span></span> | <span data-ttu-id="cca30-130">Selecteer Hallo gedeeld-beleid, u op Hallo tabblad IoT Hub-instellingen vinden kunt. Elk gedeeld toegangsbeleid heeft een naam, machtigingen die u instelt en toegangssleutels.</span><span class="sxs-lookup"><span data-stu-id="cca30-130">Select hello shared access policy, which can be found on hello IoT Hub settings tab. Each shared access policy has a name, permissions that you set, and access keys.</span></span> <span data-ttu-id="cca30-131">Hallo gedeeld toegangsbeleid voor de gebeurtenisbron *moet* hebben **service verbinding** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="cca30-131">hello shared access policy for your event source *must* have **service connect** permissions.</span></span>
| <span data-ttu-id="cca30-132">IoT hub klantengroep</span><span class="sxs-lookup"><span data-stu-id="cca30-132">IoT hub consumer group</span></span> | <span data-ttu-id="cca30-133">Hallo Consumergroep tooread gebeurtenissen van Hallo IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cca30-133">hello Consumer Group tooread events from hello IoT Hub.</span></span> <span data-ttu-id="cca30-134">U wordt ten zeerste aanbevolen toouse een speciale klantengroep voor de gebeurtenisbron.</span><span class="sxs-lookup"><span data-stu-id="cca30-134">It is highly recommended toouse a dedicated consumer group for your event source.</span></span>

### <a name="provide-iot-hub-settings-manually"></a><span data-ttu-id="cca30-135">Geef de IoT Hub-instellingen handmatig</span><span class="sxs-lookup"><span data-stu-id="cca30-135">Provide IoT Hub settings manually</span></span>

<span data-ttu-id="cca30-136">Hallo volgende tabel bevat uitleg over elke eigenschap in Hallo nieuwe gebeurtenisbron tabblad met de beschrijving bij het invoeren van de instellingen handmatig:</span><span class="sxs-lookup"><span data-stu-id="cca30-136">hello following table explains each property in hello New Event Source tab with its description when entering settings manually:</span></span>

| <span data-ttu-id="cca30-137">DE NAAM VAN EIGENSCHAP</span><span class="sxs-lookup"><span data-stu-id="cca30-137">PROPERTY NAME</span></span> | <span data-ttu-id="cca30-138">BESCHRIJVING</span><span class="sxs-lookup"><span data-stu-id="cca30-138">DESCRIPTION</span></span> |
| --- | --- |
| <span data-ttu-id="cca30-139">De naam van de gebeurtenis-bron</span><span class="sxs-lookup"><span data-stu-id="cca30-139">Event source name</span></span> | <span data-ttu-id="cca30-140">Hallo-naam van de gebeurtenisbron.</span><span class="sxs-lookup"><span data-stu-id="cca30-140">hello name of your event source.</span></span> <span data-ttu-id="cca30-141">Deze naam moet uniek zijn binnen uw omgeving Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="cca30-141">This name must be unique within your Time Series Insights environment.</span></span>
| <span data-ttu-id="cca30-142">Bron</span><span class="sxs-lookup"><span data-stu-id="cca30-142">Source</span></span> | <span data-ttu-id="cca30-143">Kies **IoT Hub** toocreate een gebeurtenisbron IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cca30-143">Choose **IoT Hub** toocreate an IoT Hub event source.</span></span>
| <span data-ttu-id="cca30-144">Abonnements-Id</span><span class="sxs-lookup"><span data-stu-id="cca30-144">Subscription Id</span></span> | <span data-ttu-id="cca30-145">Hallo abonnement waarin deze iothub is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cca30-145">hello subscription in which this IoT hub was created.</span></span>
| <span data-ttu-id="cca30-146">Resourcegroep</span><span class="sxs-lookup"><span data-stu-id="cca30-146">Resource group</span></span> | <span data-ttu-id="cca30-147">Hallo abonnement waarin deze iothub is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cca30-147">hello subscription in which this IoT hub was created.</span></span>
| <span data-ttu-id="cca30-148">De naam van de IoT-hub</span><span class="sxs-lookup"><span data-stu-id="cca30-148">IoT hub name</span></span> | <span data-ttu-id="cca30-149">Hallo-naam van uw IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="cca30-149">hello name of your IoT Hub.</span></span> <span data-ttu-id="cca30-150">Wanneer u uw IoT-hub gemaakt, u dit ook een specifieke naam gegeven</span><span class="sxs-lookup"><span data-stu-id="cca30-150">When you created your IoT hub, you also gave it a specific name</span></span>
| <span data-ttu-id="cca30-151">Naam voor het IoT-hub</span><span class="sxs-lookup"><span data-stu-id="cca30-151">IoT hub policy name</span></span> | <span data-ttu-id="cca30-152">Hallo gedeeld toegangsbeleid, die kan worden gemaakt op Hallo tabblad IoT Hub-instellingen. Elk gedeeld toegangsbeleid heeft een naam, machtigingen die u instelt en toegangssleutels.</span><span class="sxs-lookup"><span data-stu-id="cca30-152">hello shared access policy, which can be created on hello IoT Hub settings tab. Each shared access policy has a name, permissions that you set, and access keys.</span></span> <span data-ttu-id="cca30-153">Hallo gedeeld toegangsbeleid voor de gebeurtenisbron *moet* hebben **service verbinding** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="cca30-153">hello shared access policy for your event source *must* have **service connect** permissions.</span></span>
| <span data-ttu-id="cca30-154">IoT hub beleidssleutel</span><span class="sxs-lookup"><span data-stu-id="cca30-154">IoT hub policy key</span></span> | <span data-ttu-id="cca30-155">Hallo toegang tot gedeelde sleutel gebruikt tooauthenticate toegang toohello Service Bus-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="cca30-155">hello Shared Access key used tooauthenticate access toohello Service Bus namespace.</span></span> <span data-ttu-id="cca30-156">Typ Hallo primaire of secundaire sleutel hier in.</span><span class="sxs-lookup"><span data-stu-id="cca30-156">Type hello primary or secondary key here.</span></span>
| <span data-ttu-id="cca30-157">IoT hub klantengroep</span><span class="sxs-lookup"><span data-stu-id="cca30-157">IoT hub consumer group</span></span> | <span data-ttu-id="cca30-158">Hallo Consumergroep tooread gebeurtenissen van Hallo IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cca30-158">hello Consumer Group tooread events from hello IoT Hub.</span></span> <span data-ttu-id="cca30-159">U wordt ten zeerste aanbevolen toouse een speciale klantengroep voor de gebeurtenisbron.</span><span class="sxs-lookup"><span data-stu-id="cca30-159">It is highly recommended toouse a dedicated consumer group for your event source.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cca30-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cca30-160">Next steps</span></span>

1. <span data-ttu-id="cca30-161">Toevoegen van een data access-beleid tooyour omgeving [definiëren data access-beleid](time-series-insights-data-access.md)</span><span class="sxs-lookup"><span data-stu-id="cca30-161">Add a data access policy tooyour environment [Define data access policies](time-series-insights-data-access.md)</span></span>
1. <span data-ttu-id="cca30-162">Toegang tot uw omgeving in Hallo [Time Series Insights-Portal](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="cca30-162">Access your environment in hello [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
