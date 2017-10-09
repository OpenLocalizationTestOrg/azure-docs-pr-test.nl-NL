---
title: aaaAdd verwijzing gegevensset tooyour Azure Time Series Insights omgeving | Microsoft Docs
description: In deze zelfstudie maakt u een verwijzing gegevensset tooyour Time Series Insights omgeving toevoegen
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
ms.openlocfilehash: 05e626ed81a22f2a8710b23a931ccd17c0f38ca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-reference-data-set-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a><span data-ttu-id="42118-103">Een verwijzing gegevensset voor uw Time Series Insights-omgeving met behulp van de portal Ibiza Hallo maken</span><span class="sxs-lookup"><span data-stu-id="42118-103">Create a reference data set for your Time Series Insights environment using hello Ibiza portal</span></span>

<span data-ttu-id="42118-104">Een gegevensset verwijzing is een verzameling van items die zijn uitgebreid met Hallo gebeurtenissen van de gebeurtenisbron.</span><span class="sxs-lookup"><span data-stu-id="42118-104">A Reference Data Set is a collection of items that are augmented with hello events from your event source.</span></span> <span data-ttu-id="42118-105">De engine voor inkomende gebeurtenissen van Time Series Insights koppelt een gebeurtenis van uw gebeurtenisbron aan een item in uw referentiegegevensset.</span><span class="sxs-lookup"><span data-stu-id="42118-105">Time Series Insights ingress engine joins an event from your event source with an item in your reference data set.</span></span> <span data-ttu-id="42118-106">Deze uitgebreide gebeurtenis is vervolgens beschikbaar voor query’s.</span><span class="sxs-lookup"><span data-stu-id="42118-106">This augmented event is then available for query.</span></span> <span data-ttu-id="42118-107">Deze koppeling is gebaseerd op Hallo sleutels die zijn gedefinieerd in uw gegevensset verwijzing.</span><span class="sxs-lookup"><span data-stu-id="42118-107">This join is based on hello keys defined in your reference data set.</span></span>

## <a name="steps-tooadd-a-reference-data-set-tooyour-environment"></a><span data-ttu-id="42118-108">Stappen tooadd een verwijzing gegevensset tooyour omgeving</span><span class="sxs-lookup"><span data-stu-id="42118-108">Steps tooadd a reference data set tooyour environment</span></span>

1. <span data-ttu-id="42118-109">Meld u aan toohello [portal Ibiza](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="42118-109">Sign in toohello [Ibiza portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="42118-110">Klik op 'Alle resources' in hello menu aan de linkerkant van de portal Ibiza Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="42118-110">Click “All resources” in hello menu on hello left side of hello Ibiza portal.</span></span>
3. <span data-ttu-id="42118-111">Selecteer uw Time Series Insights-omgeving.</span><span class="sxs-lookup"><span data-stu-id="42118-111">Select your Time Series Insights environment.</span></span>

    ![Hallo Time Series Insights verwijzing gegevensset maken](media/add-reference-data-set/getstarted-create-reference-data-set-1.png)

4. <span data-ttu-id="42118-113">Selecteer 'Referentiegegevensset', klik op '+ Toevoegen.'</span><span class="sxs-lookup"><span data-stu-id="42118-113">Select “Reference Data Sets”, click “+ Add.”</span></span>

    ![Hallo Time Series Insights verwijzing gegevensset maken - details](media/add-reference-data-set/getstarted-create-reference-data-set-2.png)

5. <span data-ttu-id="42118-115">Geef de naam Hallo van gegevensset Hallo-verwijzing.</span><span class="sxs-lookup"><span data-stu-id="42118-115">Specify hello name of hello reference data set.</span></span>
6. <span data-ttu-id="42118-116">Hallo-sleutelnaam en het type opgeven.</span><span class="sxs-lookup"><span data-stu-id="42118-116">Specify hello key name and its type.</span></span> <span data-ttu-id="42118-117">Deze naam en type is gebruikte toopick Hallo de juiste eigenschap van Hallo-gebeurtenis in de bron van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="42118-117">This name and type is used toopick hello correct property from hello event in your event source.</span></span> <span data-ttu-id="42118-118">Hallo bijvoorbeeld tijd reeks Insights ingress-engine wordt gezocht naar een eigenschap met de naam van de Hallo 'DeviceId' van het type 'Tekenreeks' in inkomende hello-gebeurtenis op als u de sleutelnaam als 'DeviceId' en type als 'Tekenreeks' opgeeft, klikt u vervolgens.</span><span class="sxs-lookup"><span data-stu-id="42118-118">For instance, if you provide key name as “DeviceId” and type as “String”, then hello Time Series Insights ingress engine looks for a property with hello name “DeviceId” of type “String” in hello incoming event.</span></span> <span data-ttu-id="42118-119">U kunt meer dan één sleutel toojoin met Hallo gebeurtenis opgeven.</span><span class="sxs-lookup"><span data-stu-id="42118-119">You can provide more than one key toojoin with hello event.</span></span> <span data-ttu-id="42118-120">Hallo eigenschap naam overeenkomst is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="42118-120">hello property name match is case-sensitive.</span></span>

     ![Hallo Time Series Insights verwijzing gegevensset maken - details](media/add-reference-data-set/getstarted-create-reference-data-set-3.png)

7. <span data-ttu-id="42118-122">Klik op Maken.</span><span class="sxs-lookup"><span data-stu-id="42118-122">Click “Create.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="42118-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="42118-123">Next steps</span></span>

* <span data-ttu-id="42118-124">Programmatisch [referentiegegevens beheren](time-series-insights-manage-reference-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="42118-124">[Manage reference data](time-series-insights-manage-reference-data-csharp.md) programmatically.</span></span>
* <span data-ttu-id="42118-125">Zie voor volledige API-verwijzing hello, [API van Data-verwijzing](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) document.</span><span class="sxs-lookup"><span data-stu-id="42118-125">For hello complete API reference, see [Reference Data API](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) document.</span></span>
