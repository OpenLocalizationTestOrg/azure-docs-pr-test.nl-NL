---
title: aaaAdd hello queryactie in logic apps | Microsoft Docs
description: Overzicht van Hallo queryactie voor het uitvoeren van acties zoals matrix van filter.
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 34e702c7-f9e5-4885-9266-fc7404adecfe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2016
ms.author: jehollan
ms.openlocfilehash: 3d4be901e7e6bf1b644057648930667ab34f2124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-query-action"></a><span data-ttu-id="2a36c-103">Aan de slag met Hallo queryactie</span><span class="sxs-lookup"><span data-stu-id="2a36c-103">Get started with hello query action</span></span>
<span data-ttu-id="2a36c-104">Met behulp van de actie query Hallo, kunt u met de batches en matrices tooaccomplish werkstromen te werken:</span><span class="sxs-lookup"><span data-stu-id="2a36c-104">By using hello query action, you can work with batches and arrays tooaccomplish workflows to:</span></span>

* <span data-ttu-id="2a36c-105">Een taak maken voor alle hoge prioriteit records uit een database.</span><span class="sxs-lookup"><span data-stu-id="2a36c-105">Create a task for all high-priority records from a database.</span></span>
* <span data-ttu-id="2a36c-106">Sla alle PDF-bijlagen voor e-mailberichten naar een Azure-blob.</span><span class="sxs-lookup"><span data-stu-id="2a36c-106">Save all PDF attachments for emails into an Azure blob.</span></span>

<span data-ttu-id="2a36c-107">tooget gestart met Hallo queryactie in een logische app, Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="2a36c-107">tooget started using hello query action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-query-action"></a><span data-ttu-id="2a36c-108">Gebruik Hallo queryactie</span><span class="sxs-lookup"><span data-stu-id="2a36c-108">Use hello query action</span></span>
<span data-ttu-id="2a36c-109">Een actie is een bewerking die wordt uitgevoerd door Hallo werkstroom die is gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="2a36c-109">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="2a36c-110">[Meer informatie over acties](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2a36c-110">[Learn more about actions](connectors-overview.md).</span></span>  

<span data-ttu-id="2a36c-111">Hallo queryactie heeft momenteel een bewerking, Hallo filter matrix, die wordt weergegeven in de ontwerpfunctie Hallo aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2a36c-111">hello query action currently has one operation, called hello filter array, that is exposed in hello designer.</span></span> <span data-ttu-id="2a36c-112">Dit kunt u een matrix tooquery en een set gefilterde resultaten geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="2a36c-112">This allows you tooquery an array and return a set of filtered results.</span></span>

<span data-ttu-id="2a36c-113">Hier ziet u hoe u deze in een logische app kunt toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2a36c-113">Here's how you can add it in a logic app:</span></span>

1. <span data-ttu-id="2a36c-114">Selecteer Hallo **nieuwe stap** knop.</span><span class="sxs-lookup"><span data-stu-id="2a36c-114">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="2a36c-115">Kies **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="2a36c-115">Choose **Add an action**.</span></span>
3. <span data-ttu-id="2a36c-116">Typ in het zoekvak Hallo actie, **filter** toolist hello **matrix van Filter** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="2a36c-116">In hello action search box, type **filter** toolist hello **Filter array** action.</span></span>
   
    ![Selecteer Hallo queryactie](./media/connectors-native-query/using-action-1.png)
4. <span data-ttu-id="2a36c-118">Selecteer een toofilter matrix.</span><span class="sxs-lookup"><span data-stu-id="2a36c-118">Select an array toofilter.</span></span> <span data-ttu-id="2a36c-119">(hello volgende schermafbeelding ziet u Hallo-matrix van resultaten van een zoekopdracht Twitter.)</span><span class="sxs-lookup"><span data-stu-id="2a36c-119">(hello following screenshot shows hello array of results from a Twitter search.)</span></span>
5. <span data-ttu-id="2a36c-120">Maak een voorwaarde tooevaluate op elk item.</span><span class="sxs-lookup"><span data-stu-id="2a36c-120">Create a condition tooevaluate on each item.</span></span> <span data-ttu-id="2a36c-121">(Hallo schermopname na filters tweets van gebruikers die beschikken over meer dan 100 PC-gebruikers.)</span><span class="sxs-lookup"><span data-stu-id="2a36c-121">(hello following screenshot filters tweets from users who have more than 100 followers.)</span></span>
   
    ![Actie voltooid Hallo-query](./media/connectors-native-query/using-action-2.png)
   
    <span data-ttu-id="2a36c-123">Hallo-actie wordt een nieuwe matrix die alleen de resultaten die voldoen aan de vereisten voor Hallo filter bevat uitvoer.</span><span class="sxs-lookup"><span data-stu-id="2a36c-123">hello action will output a new array that contains only results that met hello filter requirements.</span></span>
6. <span data-ttu-id="2a36c-124">Klik op Hallo linkerbovenhoek van Hallo werkbalk toosave en uw logische app worden beide opslaan en publiceren (activeren).</span><span class="sxs-lookup"><span data-stu-id="2a36c-124">Click hello upper-left corner of hello toolbar toosave, and your logic app will both save and publish (activate).</span></span>

## <a name="query-action"></a><span data-ttu-id="2a36c-125">Queryactie</span><span class="sxs-lookup"><span data-stu-id="2a36c-125">Query action</span></span>
<span data-ttu-id="2a36c-126">Hier vindt u details Hallo voor Hallo-actie die ondersteuning biedt voor deze connector.</span><span class="sxs-lookup"><span data-stu-id="2a36c-126">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="2a36c-127">Hallo-connector heeft een mogelijke actie.</span><span class="sxs-lookup"><span data-stu-id="2a36c-127">hello connector has one possible action.</span></span>

| <span data-ttu-id="2a36c-128">Actie</span><span class="sxs-lookup"><span data-stu-id="2a36c-128">Action</span></span> | <span data-ttu-id="2a36c-129">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="2a36c-129">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2a36c-130">Matrix van filter</span><span class="sxs-lookup"><span data-stu-id="2a36c-130">Filter array</span></span> |<span data-ttu-id="2a36c-131">Evalueert een voorwaarde voor elk item in een matrix en Hallo resultaten retourneert</span><span class="sxs-lookup"><span data-stu-id="2a36c-131">Evaluates a condition for each item in an array and returns hello results</span></span> |

## <a name="action-details"></a><span data-ttu-id="2a36c-132">Actiedetails</span><span class="sxs-lookup"><span data-stu-id="2a36c-132">Action details</span></span>
<span data-ttu-id="2a36c-133">Hallo queryactie wordt geleverd met een mogelijke actie.</span><span class="sxs-lookup"><span data-stu-id="2a36c-133">hello query action comes with one possible action.</span></span> <span data-ttu-id="2a36c-134">Hallo volgende tabellen worden beschreven Hallo vereiste en optionele invoervelden voor Hallo actie en het bijbehorende uitvoerdetails hello, die gekoppeld zijn aan het Hallo-actie.</span><span class="sxs-lookup"><span data-stu-id="2a36c-134">hello following tables describe hello required and optional input fields for hello action and hello corresponding output details that are associated with using hello action.</span></span>

### <a name="filter-array"></a><span data-ttu-id="2a36c-135">Matrix van filter</span><span class="sxs-lookup"><span data-stu-id="2a36c-135">Filter array</span></span>
<span data-ttu-id="2a36c-136">Hallo volgen invoervelden voor Hallo actie, waardoor een uitgaande HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="2a36c-136">hello following are input fields for hello action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="2a36c-137">A * houdt in dat een vereist veld.</span><span class="sxs-lookup"><span data-stu-id="2a36c-137">A * means that it is a required field.</span></span>

| <span data-ttu-id="2a36c-138">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="2a36c-138">Display name</span></span> | <span data-ttu-id="2a36c-139">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="2a36c-139">Property name</span></span> | <span data-ttu-id="2a36c-140">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="2a36c-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2a36c-141">Van *</span><span class="sxs-lookup"><span data-stu-id="2a36c-141">From*</span></span> |<span data-ttu-id="2a36c-142">Van</span><span class="sxs-lookup"><span data-stu-id="2a36c-142">from</span></span> |<span data-ttu-id="2a36c-143">Hallo matrix toofilter</span><span class="sxs-lookup"><span data-stu-id="2a36c-143">hello array toofilter</span></span> |
| <span data-ttu-id="2a36c-144">Voorwaarde *</span><span class="sxs-lookup"><span data-stu-id="2a36c-144">Condition*</span></span> |<span data-ttu-id="2a36c-145">waar</span><span class="sxs-lookup"><span data-stu-id="2a36c-145">where</span></span> |<span data-ttu-id="2a36c-146">Hallo voorwaarde tooevaluate voor elk item</span><span class="sxs-lookup"><span data-stu-id="2a36c-146">hello condition tooevaluate for each item</span></span> |

<br>

### <a name="output-details"></a><span data-ttu-id="2a36c-147">Uitvoerdetails</span><span class="sxs-lookup"><span data-stu-id="2a36c-147">Output details</span></span>
<span data-ttu-id="2a36c-148">Hallo hieronder vindt u uitvoerdetails voor Hallo HTTP-antwoord.</span><span class="sxs-lookup"><span data-stu-id="2a36c-148">hello following are output details for hello HTTP response.</span></span>

| <span data-ttu-id="2a36c-149">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="2a36c-149">Property name</span></span> | <span data-ttu-id="2a36c-150">Gegevenstype</span><span class="sxs-lookup"><span data-stu-id="2a36c-150">Data type</span></span> | <span data-ttu-id="2a36c-151">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="2a36c-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2a36c-152">Gefilterde matrix</span><span class="sxs-lookup"><span data-stu-id="2a36c-152">Filtered array</span></span> |<span data-ttu-id="2a36c-153">matrix</span><span class="sxs-lookup"><span data-stu-id="2a36c-153">array</span></span> |<span data-ttu-id="2a36c-154">Een matrix met een object voor elk gefilterde resultaat</span><span class="sxs-lookup"><span data-stu-id="2a36c-154">An array that contains an object for each filtered result</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2a36c-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2a36c-155">Next steps</span></span>
<span data-ttu-id="2a36c-156">Nu uitproberen Hallo-platform en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="2a36c-156">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="2a36c-157">U kunt verkennen Hallo van andere beschikbare connectors in logische apps door te kijken onze [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="2a36c-157">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

