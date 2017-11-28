---
title: Een referentiegegevensset toevoegen aan uw Azure Time Series Insights-omgeving | Microsoft Docs
description: In deze zelfstudie koppelt u een referentiegegevensset aan uw Time Series Insights-omgeving
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: venkatja
ms.openlocfilehash: 23444297b5231e6a026bcd9ce3ee9f943bf05867
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-reference-data-set-for-your-time-series-insights-environment-using-the-ibiza-portal"></a><span data-ttu-id="7986e-103">Een referentiegegevensset voor uw Time Series Insights-omgeving maken met Ibiza-portal</span><span class="sxs-lookup"><span data-stu-id="7986e-103">Create a reference data set for your Time Series Insights environment using the Ibiza portal</span></span>

<span data-ttu-id="7986e-104">Een referentiegegevensset is een verzameling items die is uitgebreid met de gebeurtenissen uit uw gebeurtenisbron.</span><span class="sxs-lookup"><span data-stu-id="7986e-104">A Reference Data Set is a collection of items that are augmented with the events from your event source.</span></span> <span data-ttu-id="7986e-105">De engine voor inkomende gebeurtenissen van Time Series Insights koppelt een gebeurtenis van uw gebeurtenisbron aan een item in uw referentiegegevensset.</span><span class="sxs-lookup"><span data-stu-id="7986e-105">Time Series Insights ingress engine joins an event from your event source with an item in your reference data set.</span></span> <span data-ttu-id="7986e-106">Deze uitgebreide gebeurtenis is vervolgens beschikbaar voor query’s.</span><span class="sxs-lookup"><span data-stu-id="7986e-106">This augmented event is then available for query.</span></span> <span data-ttu-id="7986e-107">Deze koppeling is gebaseerd op de sleutels die zijn gedefinieerd in uw referentiegegevensset.</span><span class="sxs-lookup"><span data-stu-id="7986e-107">This join is based on the keys defined in your reference data set.</span></span>

## <a name="steps-to-add-a-reference-data-set-to-your-environment"></a><span data-ttu-id="7986e-108">Stappen voor het toevoegen van een referentiegegevensset aan uw omgeving</span><span class="sxs-lookup"><span data-stu-id="7986e-108">Steps to add a reference data set to your environment</span></span>

1. <span data-ttu-id="7986e-109">Meld u aan bij [Ibiza-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7986e-109">Sign in to the [Ibiza portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7986e-110">Klik op Alle resources in het menu aan de linkerkant van de Ibiza-portal.</span><span class="sxs-lookup"><span data-stu-id="7986e-110">Click “All resources” in the menu on the left side of the Ibiza portal.</span></span>
3. <span data-ttu-id="7986e-111">Selecteer uw Time Series Insights-omgeving.</span><span class="sxs-lookup"><span data-stu-id="7986e-111">Select your Time Series Insights environment.</span></span>

    ![De Time Series Insights-referentiegegevensset maken](media/add-reference-data-set/getstarted-create-reference-data-set-1.png)

4. <span data-ttu-id="7986e-113">Selecteer 'Referentiegegevensset', klik op '+ Toevoegen.'</span><span class="sxs-lookup"><span data-stu-id="7986e-113">Select “Reference Data Sets”, click “+ Add.”</span></span>

    ![De Time Series Insights-referentiegegevensset maken - details](media/add-reference-data-set/getstarted-create-reference-data-set-2.png)

5. <span data-ttu-id="7986e-115">Geef de naam van de referentiegegevensset op.</span><span class="sxs-lookup"><span data-stu-id="7986e-115">Specify the name of the reference data set.</span></span>
6. <span data-ttu-id="7986e-116">Geef de sleutelnaam en het bijbehorende type op.</span><span class="sxs-lookup"><span data-stu-id="7986e-116">Specify the key name and its type.</span></span> <span data-ttu-id="7986e-117">Deze naam en dit type worden gebruikt om de juiste eigenschap van de gebeurtenis in de gebeurtenisbron te kiezen.</span><span class="sxs-lookup"><span data-stu-id="7986e-117">This name and type is used to pick the correct property from the event in your event source.</span></span> <span data-ttu-id="7986e-118">Als u bijvoorbeeld de sleutelnaam 'DeviceId' en het type 'Tekenreeks' opgeeft, zoekt de Time Series Insights-engine naar een eigenschap met de naam 'DeviceId' van het type 'Tekenreeks' in de inkomende gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="7986e-118">For instance, if you provide key name as “DeviceId” and type as “String”, then the Time Series Insights ingress engine looks for a property with the name “DeviceId” of type “String” in the incoming event.</span></span> <span data-ttu-id="7986e-119">U kunt meer meerdere sleutels opgeven om samen te voegen met de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="7986e-119">You can provide more than one key to join with the event.</span></span> <span data-ttu-id="7986e-120">De naamsovereenkomst van de eigenschap is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="7986e-120">The property name match is case-sensitive.</span></span>

     ![De Time Series Insights-referentiegegevensset maken - details](media/add-reference-data-set/getstarted-create-reference-data-set-3.png)

7. <span data-ttu-id="7986e-122">Klik op Maken.</span><span class="sxs-lookup"><span data-stu-id="7986e-122">Click “Create.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="7986e-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7986e-123">Next steps</span></span>

* <span data-ttu-id="7986e-124">Programmatisch [referentiegegevens beheren](time-series-insights-manage-reference-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="7986e-124">[Manage reference data](time-series-insights-manage-reference-data-csharp.md) programmatically.</span></span>
* <span data-ttu-id="7986e-125">Zie voor de volledige API-verwijzing het document [Reference Data API](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api).</span><span class="sxs-lookup"><span data-stu-id="7986e-125">For the complete API reference, see [Reference Data API](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) document.</span></span>