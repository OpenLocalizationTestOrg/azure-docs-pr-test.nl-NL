---
title: Azure Application Insights schoorstenen
description: Meer informatie over hoe u schoorstenen kunt gebruiken om te ontdekken hoe klanten communiceert met uw toepassing.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 59c4dfafc102b26e3b9873f433065715f4aec9ec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="discover-how-customers-are-using-your-application-with-the-application-insights-funnels"></a><span data-ttu-id="11267-103">Hoe klanten gebruikmaakt van uw toepassing met de Application Insights schoorstenen detecteren</span><span class="sxs-lookup"><span data-stu-id="11267-103">Discover how customers are using your application with the Application Insights Funnels</span></span>

<span data-ttu-id="11267-104">Understanding klantervaring is van het grootste belang voor uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="11267-104">Understanding customer experience is of the utmost importance to your business.</span></span> <span data-ttu-id="11267-105">Als uw toepassing meerdere fasen omvat, moet u weten als u de voortgang van de meeste klanten door het hele proces, of als ze beëindigt het proces op een bepaald moment.</span><span class="sxs-lookup"><span data-stu-id="11267-105">If your application involves multiple stages, you will need to know if most customers are progressing through the entire process, or if they are ending the process at some point.</span></span> <span data-ttu-id="11267-106">De voortgang door een reeks stappen in een webtoepassing staat bekend als een 'trechter'.</span><span class="sxs-lookup"><span data-stu-id="11267-106">The progression through a series of steps in a web application is known as a "funnel".</span></span> <span data-ttu-id="11267-107">De Application Insights schoorstenen kunt u inzicht in uw gebruikers en de monitor stapsgewijze conversie tarieven.</span><span class="sxs-lookup"><span data-stu-id="11267-107">You can use the Application Insights Funnels to gain insights into your users and monitor step-by-step conversion rates.</span></span> 

## <a name="get-started-with-the-funnels-blade"></a><span data-ttu-id="11267-108">Aan de slag met de blade schoorstenen</span><span class="sxs-lookup"><span data-stu-id="11267-108">Get started with the Funnels blade</span></span>
<span data-ttu-id="11267-109">De eenvoudigste manier om meer informatie over schoorstenen is op hoe u een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="11267-109">The easiest way to learn about Funnels is to walk though an example.</span></span> <span data-ttu-id="11267-110">De volgende illustraties ziet u dat de stappen eigenaren van een zakelijke e-commerce zou hebben voor meer informatie over hoe hun klanten communiceren met de webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="11267-110">The following illustrations demonstrate the steps owners of an e-commerce business would take to learn how their customers interact with their web application.</span></span>  

### <a name="create-your-funnel"></a><span data-ttu-id="11267-111">Maken van de trechter</span><span class="sxs-lookup"><span data-stu-id="11267-111">Create your funnel</span></span>
<span data-ttu-id="11267-112">Voordat u uw trechter maakt, moet u beslissen over de vraag die u wilt beantwoorden.</span><span class="sxs-lookup"><span data-stu-id="11267-112">Before you create your funnel, you need to decide on the question you want to answer.</span></span> <span data-ttu-id="11267-113">U wilt weten hoe veel klanten uw startpagina klikken op een advertentie bekijken.</span><span class="sxs-lookup"><span data-stu-id="11267-113">For example, you might want to know how many customers viewing your home page click on an advertisement.</span></span> <span data-ttu-id="11267-114">In dit voorbeeld wilt de eigenaars van het bedrijf Fabrikam Fiber weet het percentage van de klanten die een aankoop na het toevoegen van items aan de winkelwagen tijdens de afgelopen maand.</span><span class="sxs-lookup"><span data-stu-id="11267-114">In this example, the owners of the Fabrikam Fiber company want to know the percentage of customers who make a purchase after adding items to their shopping cart during the last month.</span></span>

<span data-ttu-id="11267-115">Hier volgen de stappen waarmee ze hun trechter maken.</span><span class="sxs-lookup"><span data-stu-id="11267-115">Here are the steps they take to create their funnel.</span></span>

1. <span data-ttu-id="11267-116">Klik op de knop Nieuw op de blade schoorstenen.</span><span class="sxs-lookup"><span data-stu-id="11267-116">Click the New button on the Funnels blade.</span></span>
1. <span data-ttu-id="11267-117">Selecteer het tijdsbereik van 'Afgelopen maand' in de **tijdsbereik** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="11267-117">Select the time range of "Last month" from the **Time Range** drop-down.</span></span> 
1. <span data-ttu-id="11267-118">Selecteer de **productpagina** gebeurtenis op basis van de **stap 1** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="11267-118">Select the **Product page** event from the **Step 1** drop-down list.</span></span> 
1. <span data-ttu-id="11267-119">Selecteer de **toevoegen aan winkelwagen** gebeurtenis op basis van de **stap 2** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="11267-119">Select the **Add to shopping cart** event from the **Step 2** drop-down list.</span></span>
1. <span data-ttu-id="11267-120">Selecteer de **Klik op inkoop** gebeurtenis op basis van de **stap 3** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="11267-120">Select the **Click purchase** event from the **Step 3** drop-down list.</span></span>
1. <span data-ttu-id="11267-121">Een naam in de trechter toevoegen en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="11267-121">Add a name to the funnel and click **Save**.</span></span>

<span data-ttu-id="11267-122">De volgende afbeelding ziet u hoe dat de gegevens van de blade schoorstenen genereert.</span><span class="sxs-lookup"><span data-stu-id="11267-122">The following illustration demonstrates the data the Funnels blade generates.</span></span> <span data-ttu-id="11267-123">Eigenaars kunnen hier de Fabrikam zien dat de 22.7% aan hun klanten die een item toegevoegd aan de winkelwagen tijdens de laatste week, de aankoop voltooid.</span><span class="sxs-lookup"><span data-stu-id="11267-123">From here the Fabrikam owners can see that during the last week, 22.7% of their customers who added an item to their shopping cart completed the purchase.</span></span> <span data-ttu-id="11267-124">Ze kunnen ook zien dat 1% van de klanten een advertentie geklikt voordat de productpagina en 20% van hun klanten afgemeld na het voltooien van hun aankoop.</span><span class="sxs-lookup"><span data-stu-id="11267-124">They can also see that 1% of the customers clicked an advertisement before visiting the product page, and 20% of their customers signed out after completing their purchase.</span></span>


![Blade schoorstenen met gegevens](./media/app-insights-understand-usage-patterns/funnel1.png)

## <a name="next-steps"></a><span data-ttu-id="11267-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="11267-126">Next steps</span></span>
  * [<span data-ttu-id="11267-127">Overzicht gebruik</span><span class="sxs-lookup"><span data-stu-id="11267-127">Usage overview</span></span>](app-insights-usage-overview.md)
  * [<span data-ttu-id="11267-128">Gebruikers, sessies en gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="11267-128">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
  * [<span data-ttu-id="11267-129">Retentie</span><span class="sxs-lookup"><span data-stu-id="11267-129">Retention</span></span>](app-insights-usage-retention.md)
  * [<span data-ttu-id="11267-130">Werkmappen</span><span class="sxs-lookup"><span data-stu-id="11267-130">Workbooks</span></span>](app-insights-usage-workbooks.md)
  * [<span data-ttu-id="11267-131">Gebruikerscontext toevoegen</span><span class="sxs-lookup"><span data-stu-id="11267-131">Add user context</span></span>](app-insights-usage-send-user-context.md)
