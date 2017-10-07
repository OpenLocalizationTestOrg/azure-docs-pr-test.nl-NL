---
title: Application Insights schoorstenen aaaAzure
description: Meer informatie over hoe u kunt schoorstenen toodiscover hoe klanten communiceert met uw toepassing.
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
ms.openlocfilehash: 2a6125cf596570cfaee30bb3ff757916e90d7676
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="discover-how-customers-are-using-your-application-with-hello-application-insights-funnels"></a><span data-ttu-id="c0511-103">Hoe klanten gebruiken uw toepassing Hello Application Insights schoorstenen detecteren</span><span class="sxs-lookup"><span data-stu-id="c0511-103">Discover how customers are using your application with hello Application Insights Funnels</span></span>

<span data-ttu-id="c0511-104">Understanding klantervaring is van het Hallo grootste belang tooyour bedrijven.</span><span class="sxs-lookup"><span data-stu-id="c0511-104">Understanding customer experience is of hello utmost importance tooyour business.</span></span> <span data-ttu-id="c0511-105">Als uw toepassing meerdere fasen omvat, moet u tooknow als de voortgang van de meeste klanten door het hele proces hello, of als ze Hallo-proces op een bepaald moment beëindigt.</span><span class="sxs-lookup"><span data-stu-id="c0511-105">If your application involves multiple stages, you will need tooknow if most customers are progressing through hello entire process, or if they are ending hello process at some point.</span></span> <span data-ttu-id="c0511-106">Hallo voortgang door een reeks stappen in een webtoepassing staat bekend als een 'trechter'.</span><span class="sxs-lookup"><span data-stu-id="c0511-106">hello progression through a series of steps in a web application is known as a "funnel".</span></span> <span data-ttu-id="c0511-107">U kunt Hallo Application Insights schoorstenen toogain inzicht in uw gebruikers en de monitor stapsgewijze conversie tarief gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c0511-107">You can use hello Application Insights Funnels toogain insights into your users and monitor step-by-step conversion rates.</span></span> 

## <a name="get-started-with-hello-funnels-blade"></a><span data-ttu-id="c0511-108">Aan de slag met Hallo schoorstenen blade</span><span class="sxs-lookup"><span data-stu-id="c0511-108">Get started with hello Funnels blade</span></span>
<span data-ttu-id="c0511-109">Hallo gemakkelijkste manier toolearn over schoorstenen is toowalk, hoewel een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c0511-109">hello easiest way toolearn about Funnels is toowalk though an example.</span></span> <span data-ttu-id="c0511-110">Hallo volgende illustraties laten zien Hallo stappen eigenaren van een zakelijke e-commerce toolearn wisselwerking tussen hun klanten en hun webtoepassing zou duren.</span><span class="sxs-lookup"><span data-stu-id="c0511-110">hello following illustrations demonstrate hello steps owners of an e-commerce business would take toolearn how their customers interact with their web application.</span></span>  

### <a name="create-your-funnel"></a><span data-ttu-id="c0511-111">Maken van de trechter</span><span class="sxs-lookup"><span data-stu-id="c0511-111">Create your funnel</span></span>
<span data-ttu-id="c0511-112">Voordat u uw trechter maakt, moet u toodecide op Hallo vraag gewenste tooanswer.</span><span class="sxs-lookup"><span data-stu-id="c0511-112">Before you create your funnel, you need toodecide on hello question you want tooanswer.</span></span> <span data-ttu-id="c0511-113">Bijvoorbeeld, kunt u tooknow hoeveel klanten uw startpagina klikken op een advertentie bekijken.</span><span class="sxs-lookup"><span data-stu-id="c0511-113">For example, you might want tooknow how many customers viewing your home page click on an advertisement.</span></span> <span data-ttu-id="c0511-114">In dit voorbeeld wilt Hallo eigenaren van Hallo bedrijf Fabrikam Fiber tooknow Hallo percentage van de klanten die na het toevoegen van items tootheir winkelwagen tijdens de afgelopen maand Hallo kopen.</span><span class="sxs-lookup"><span data-stu-id="c0511-114">In this example, hello owners of hello Fabrikam Fiber company want tooknow hello percentage of customers who make a purchase after adding items tootheir shopping cart during hello last month.</span></span>

<span data-ttu-id="c0511-115">Hier volgen Hallo stappen ze toocreate hun trechter.</span><span class="sxs-lookup"><span data-stu-id="c0511-115">Here are hello steps they take toocreate their funnel.</span></span>

1. <span data-ttu-id="c0511-116">Klik op de nieuwe knop Hallo op Hallo schoorstenen blade.</span><span class="sxs-lookup"><span data-stu-id="c0511-116">Click hello New button on hello Funnels blade.</span></span>
1. <span data-ttu-id="c0511-117">Selecteer Hallo tijdsbereik van 'Afgelopen maand' in hello **tijdsbereik** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="c0511-117">Select hello time range of "Last month" from hello **Time Range** drop-down.</span></span> 
1. <span data-ttu-id="c0511-118">Selecteer Hallo **productpagina** gebeurtenis uit Hallo **stap 1** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="c0511-118">Select hello **Product page** event from hello **Step 1** drop-down list.</span></span> 
1. <span data-ttu-id="c0511-119">Selecteer Hallo **toevoegen tooshopping winkelwagen** gebeurtenis uit Hallo **stap 2** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="c0511-119">Select hello **Add tooshopping cart** event from hello **Step 2** drop-down list.</span></span>
1. <span data-ttu-id="c0511-120">Selecteer Hallo **Klik op inkoop** gebeurtenis uit Hallo **stap 3** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="c0511-120">Select hello **Click purchase** event from hello **Step 3** drop-down list.</span></span>
1. <span data-ttu-id="c0511-121">Een naam toohello trechter toevoegen en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c0511-121">Add a name toohello funnel and click **Save**.</span></span>

<span data-ttu-id="c0511-122">Hallo volgende afbeelding ziet u hoe Hallo gegevens Hallo schoorstenen blade genereert.</span><span class="sxs-lookup"><span data-stu-id="c0511-122">hello following illustration demonstrates hello data hello Funnels blade generates.</span></span> <span data-ttu-id="c0511-123">Fabrikam eigenaren kunnen zien dat de 22.7% aan hun klanten die een item tootheir winkelen toegevoegd tijdens de afgelopen week hello, voltooide Hallo aankoop winkelwagen van hier Hallo.</span><span class="sxs-lookup"><span data-stu-id="c0511-123">From here hello Fabrikam owners can see that during hello last week, 22.7% of their customers who added an item tootheir shopping cart completed hello purchase.</span></span> <span data-ttu-id="c0511-124">Ze kunnen ook zien dat 1% van het Hallo-klanten een advertentie geklikt voordat het Hallo-productpagina en 20% van hun klanten afgemeld na het voltooien van hun aankoop.</span><span class="sxs-lookup"><span data-stu-id="c0511-124">They can also see that 1% of hello customers clicked an advertisement before visiting hello product page, and 20% of their customers signed out after completing their purchase.</span></span>


![Blade schoorstenen met gegevens](./media/app-insights-understand-usage-patterns/funnel1.png)

## <a name="next-steps"></a><span data-ttu-id="c0511-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c0511-126">Next steps</span></span>
  * [<span data-ttu-id="c0511-127">Overzicht gebruik</span><span class="sxs-lookup"><span data-stu-id="c0511-127">Usage overview</span></span>](app-insights-usage-overview.md)
  * [<span data-ttu-id="c0511-128">Gebruikers, sessies en gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="c0511-128">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
  * [<span data-ttu-id="c0511-129">Retentie</span><span class="sxs-lookup"><span data-stu-id="c0511-129">Retention</span></span>](app-insights-usage-retention.md)
  * [<span data-ttu-id="c0511-130">Werkmappen</span><span class="sxs-lookup"><span data-stu-id="c0511-130">Workbooks</span></span>](app-insights-usage-workbooks.md)
  * [<span data-ttu-id="c0511-131">Gebruikerscontext toevoegen</span><span class="sxs-lookup"><span data-stu-id="c0511-131">Add user context</span></span>](app-insights-usage-send-user-context.md)
