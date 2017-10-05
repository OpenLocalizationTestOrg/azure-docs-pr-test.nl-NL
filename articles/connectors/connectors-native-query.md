---
title: De queryactie in logic apps toevoegen | Microsoft Docs
description: Overzicht van de queryactie voor het uitvoeren van acties zoals matrix van filter.
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
ms.openlocfilehash: a992fa17a07d6167297c4cf5fe9fb3b58181d7df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-query-action"></a><span data-ttu-id="765b6-103">Aan de slag met de queryactie</span><span class="sxs-lookup"><span data-stu-id="765b6-103">Get started with the query action</span></span>
<span data-ttu-id="765b6-104">Met behulp van de queryactie, kunt u met de batches en matrices voor het uitvoeren van werkstromen te werken:</span><span class="sxs-lookup"><span data-stu-id="765b6-104">By using the query action, you can work with batches and arrays to accomplish workflows to:</span></span>

* <span data-ttu-id="765b6-105">Een taak maken voor alle hoge prioriteit records uit een database.</span><span class="sxs-lookup"><span data-stu-id="765b6-105">Create a task for all high-priority records from a database.</span></span>
* <span data-ttu-id="765b6-106">Sla alle PDF-bijlagen voor e-mailberichten naar een Azure-blob.</span><span class="sxs-lookup"><span data-stu-id="765b6-106">Save all PDF attachments for emails into an Azure blob.</span></span>

<span data-ttu-id="765b6-107">Om te beginnen met de queryactie in een logische app, Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="765b6-107">To get started using the query action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-query-action"></a><span data-ttu-id="765b6-108">Gebruik de queryactie</span><span class="sxs-lookup"><span data-stu-id="765b6-108">Use the query action</span></span>
<span data-ttu-id="765b6-109">Een actie is een bewerking die wordt uitgevoerd door de werkstroom die is gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="765b6-109">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> <span data-ttu-id="765b6-110">[Meer informatie over acties](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="765b6-110">[Learn more about actions](connectors-overview.md).</span></span>  

<span data-ttu-id="765b6-111">De actie van de query heeft momenteel een bewerking, die de matrix van filter, die wordt weergegeven in de ontwerpfunctie wordt genoemd.</span><span class="sxs-lookup"><span data-stu-id="765b6-111">The query action currently has one operation, called the filter array, that is exposed in the designer.</span></span> <span data-ttu-id="765b6-112">Hiermee kunt u een matrix doorzoeken en een set gefilterde resultaten geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="765b6-112">This allows you to query an array and return a set of filtered results.</span></span>

<span data-ttu-id="765b6-113">Hier ziet u hoe u deze in een logische app kunt toevoegen:</span><span class="sxs-lookup"><span data-stu-id="765b6-113">Here's how you can add it in a logic app:</span></span>

1. <span data-ttu-id="765b6-114">Selecteer de **nieuwe stap** knop.</span><span class="sxs-lookup"><span data-stu-id="765b6-114">Select the **New Step** button.</span></span>
2. <span data-ttu-id="765b6-115">Kies **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="765b6-115">Choose **Add an action**.</span></span>
3. <span data-ttu-id="765b6-116">Typ in het zoekvak actie **filter** aan lijst met de **matrix van Filter** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="765b6-116">In the action search box, type **filter** to list the **Filter array** action.</span></span>
   
    ![Selecteer de queryactie](./media/connectors-native-query/using-action-1.png)
4. <span data-ttu-id="765b6-118">Selecteer een matrix om te filteren.</span><span class="sxs-lookup"><span data-stu-id="765b6-118">Select an array to filter.</span></span> <span data-ttu-id="765b6-119">(De volgende schermafbeelding ziet u de matrix van resultaten van een zoekopdracht Twitter.)</span><span class="sxs-lookup"><span data-stu-id="765b6-119">(The following screenshot shows the array of results from a Twitter search.)</span></span>
5. <span data-ttu-id="765b6-120">Een voorwaarde om te evalueren voor elk item maken.</span><span class="sxs-lookup"><span data-stu-id="765b6-120">Create a condition to evaluate on each item.</span></span> <span data-ttu-id="765b6-121">(In de volgende schermafbeelding filters tweets van gebruikers die beschikken over meer dan 100 PC-gebruikers.)</span><span class="sxs-lookup"><span data-stu-id="765b6-121">(The following screenshot filters tweets from users who have more than 100 followers.)</span></span>
   
    ![De queryactie niet voltooien](./media/connectors-native-query/using-action-2.png)
   
    <span data-ttu-id="765b6-123">De uitvoer van de actie wordt een nieuwe matrix die alleen de resultaten die voldoet aan de vereisten van het filter bevat.</span><span class="sxs-lookup"><span data-stu-id="765b6-123">The action will output a new array that contains only results that met the filter requirements.</span></span>
6. <span data-ttu-id="765b6-124">Klik op de linkerbovenhoek van de werkbalk om op te slaan en uw logische app wordt opslaan en publiceren (activeren).</span><span class="sxs-lookup"><span data-stu-id="765b6-124">Click the upper-left corner of the toolbar to save, and your logic app will both save and publish (activate).</span></span>

## <a name="query-action"></a><span data-ttu-id="765b6-125">Queryactie</span><span class="sxs-lookup"><span data-stu-id="765b6-125">Query action</span></span>
<span data-ttu-id="765b6-126">Hier volgen de details voor de actie die ondersteuning biedt voor deze connector.</span><span class="sxs-lookup"><span data-stu-id="765b6-126">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="765b6-127">De connector is een mogelijke actie.</span><span class="sxs-lookup"><span data-stu-id="765b6-127">The connector has one possible action.</span></span>

| <span data-ttu-id="765b6-128">Actie</span><span class="sxs-lookup"><span data-stu-id="765b6-128">Action</span></span> | <span data-ttu-id="765b6-129">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="765b6-129">Description</span></span> |
| --- | --- |
| <span data-ttu-id="765b6-130">Matrix van filter</span><span class="sxs-lookup"><span data-stu-id="765b6-130">Filter array</span></span> |<span data-ttu-id="765b6-131">Evalueert een voorwaarde voor elk item in een matrix en de resultaten geretourneerd</span><span class="sxs-lookup"><span data-stu-id="765b6-131">Evaluates a condition for each item in an array and returns the results</span></span> |

## <a name="action-details"></a><span data-ttu-id="765b6-132">Actiedetails</span><span class="sxs-lookup"><span data-stu-id="765b6-132">Action details</span></span>
<span data-ttu-id="765b6-133">De queryactie wordt geleverd met een mogelijke actie.</span><span class="sxs-lookup"><span data-stu-id="765b6-133">The query action comes with one possible action.</span></span> <span data-ttu-id="765b6-134">De volgende tabellen beschrijven de vereiste en optionele invoervelden voor de actie en de bijbehorende uitvoerdetails die zijn gekoppeld met de actie.</span><span class="sxs-lookup"><span data-stu-id="765b6-134">The following tables describe the required and optional input fields for the action and the corresponding output details that are associated with using the action.</span></span>

### <a name="filter-array"></a><span data-ttu-id="765b6-135">Matrix van filter</span><span class="sxs-lookup"><span data-stu-id="765b6-135">Filter array</span></span>
<span data-ttu-id="765b6-136">Hier volgen de invoervelden voor de actie, waardoor een uitgaande HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="765b6-136">The following are input fields for the action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="765b6-137">A * houdt in dat een vereist veld.</span><span class="sxs-lookup"><span data-stu-id="765b6-137">A * means that it is a required field.</span></span>

| <span data-ttu-id="765b6-138">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="765b6-138">Display name</span></span> | <span data-ttu-id="765b6-139">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="765b6-139">Property name</span></span> | <span data-ttu-id="765b6-140">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="765b6-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="765b6-141">Van *</span><span class="sxs-lookup"><span data-stu-id="765b6-141">From*</span></span> |<span data-ttu-id="765b6-142">Van</span><span class="sxs-lookup"><span data-stu-id="765b6-142">from</span></span> |<span data-ttu-id="765b6-143">De matrix om te filteren</span><span class="sxs-lookup"><span data-stu-id="765b6-143">The array to filter</span></span> |
| <span data-ttu-id="765b6-144">Voorwaarde *</span><span class="sxs-lookup"><span data-stu-id="765b6-144">Condition*</span></span> |<span data-ttu-id="765b6-145">waar</span><span class="sxs-lookup"><span data-stu-id="765b6-145">where</span></span> |<span data-ttu-id="765b6-146">De voorwaarde om te evalueren voor elk item</span><span class="sxs-lookup"><span data-stu-id="765b6-146">The condition to evaluate for each item</span></span> |

<br>

### <a name="output-details"></a><span data-ttu-id="765b6-147">Uitvoerdetails</span><span class="sxs-lookup"><span data-stu-id="765b6-147">Output details</span></span>
<span data-ttu-id="765b6-148">Hier volgen de uitvoerdetails voor het HTTP-antwoord.</span><span class="sxs-lookup"><span data-stu-id="765b6-148">The following are output details for the HTTP response.</span></span>

| <span data-ttu-id="765b6-149">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="765b6-149">Property name</span></span> | <span data-ttu-id="765b6-150">Gegevenstype</span><span class="sxs-lookup"><span data-stu-id="765b6-150">Data type</span></span> | <span data-ttu-id="765b6-151">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="765b6-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="765b6-152">Gefilterde matrix</span><span class="sxs-lookup"><span data-stu-id="765b6-152">Filtered array</span></span> |<span data-ttu-id="765b6-153">matrix</span><span class="sxs-lookup"><span data-stu-id="765b6-153">array</span></span> |<span data-ttu-id="765b6-154">Een matrix met een object voor elk gefilterde resultaat</span><span class="sxs-lookup"><span data-stu-id="765b6-154">An array that contains an object for each filtered result</span></span> |

## <a name="next-steps"></a><span data-ttu-id="765b6-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="765b6-155">Next steps</span></span>
<span data-ttu-id="765b6-156">Nu uitproberen van het platform en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="765b6-156">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="765b6-157">U kunt de beschikbare connectors in logische apps door te kijken verkennen onze [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="765b6-157">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

