---
title: 'Azure App Service: Schalen App Service-toepassingen'
description: Meer informatie over Hallo alles over toepassing schalen in App Service.
keywords: App Service, Azure App Service, schaal, schaalbaar, App Service-abonnement, kosten App Service
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: f403c971-4450-432b-8cea-3eeb426c0147
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/07/2016
ms.author: byvinyal
ms.openlocfilehash: d8cd12f73915a916a75d46da2f751a40d567b189
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a><span data-ttu-id="2712b-104">Azure App Service: Schalen App Service-toepassingen</span><span class="sxs-lookup"><span data-stu-id="2712b-104">Azure App Service: Scaling App Service Applications</span></span>
<span data-ttu-id="2712b-105">Toepassingen die worden gehost in Azure App Service kunnen [bereiken grootschalige](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span><span class="sxs-lookup"><span data-stu-id="2712b-105">Applications hosted in Azure App Service can [achieve massive scale](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span></span>
<span data-ttu-id="2712b-106">Een toepassing schalen is echter een complex probleem dat u beschikt niet over een oplossing 'één maat alle'.</span><span class="sxs-lookup"><span data-stu-id="2712b-106">However, scaling an application is a complex problem that does not have a "one size fits all" solution.</span></span> <span data-ttu-id="2712b-107">toocorrectly uw toepassing schalen er zijn 3 sleutelgebieden waarmee tooyour toepassingen geslaagd:</span><span class="sxs-lookup"><span data-stu-id="2712b-107">toocorrectly scale your application there are 3 key areas that will contribute tooyour applications success:</span></span>

1. <span data-ttu-id="2712b-108">Informatie over de toepassingsarchitectuur van uw en de zwakke punten.</span><span class="sxs-lookup"><span data-stu-id="2712b-108">Understanding your application architecture and its weaknesses.</span></span>
   * <span data-ttu-id="2712b-109">Is de Stateful van uw toepassing?</span><span class="sxs-lookup"><span data-stu-id="2712b-109">Is your Application Stateful?</span></span> <span data-ttu-id="2712b-110">Staatloze?</span><span class="sxs-lookup"><span data-stu-id="2712b-110">Stateless?</span></span>
   * <span data-ttu-id="2712b-111">Wat zijn alle Hallo onderdelen van uw toepassing?</span><span class="sxs-lookup"><span data-stu-id="2712b-111">What are all hello components of your application?</span></span>
     * <span data-ttu-id="2712b-112">Waar zijn Hallo knelpunten in de toepassing hello?</span><span class="sxs-lookup"><span data-stu-id="2712b-112">Where are hello bottlenecks in hello application?</span></span>
   * <span data-ttu-id="2712b-113">Wanneer de belasting wordt toegepaste tooyour app, wat verbreekt de eerste?</span><span class="sxs-lookup"><span data-stu-id="2712b-113">When load is applied tooyour app, what will break first?</span></span>
2. <span data-ttu-id="2712b-114">Understanding Hallo verwacht laden en prestaties.</span><span class="sxs-lookup"><span data-stu-id="2712b-114">Understanding hello expected load and performance requirements.</span></span>
   * <span data-ttu-id="2712b-115">Hoeft de toepassing hello tooserve 1000 gebruikers? of een miljoen?</span><span class="sxs-lookup"><span data-stu-id="2712b-115">Does hello application need tooserve one thousand users? or one million?</span></span>
   * <span data-ttu-id="2712b-116">Wordt met verkeer afkomstig zijn uit één geografische locatie of globaal?</span><span class="sxs-lookup"><span data-stu-id="2712b-116">Will traffic come from a single geographic location or globally?</span></span>
   * <span data-ttu-id="2712b-117">Zijn er seizoensgebonden variaties? verkeer pieken?</span><span class="sxs-lookup"><span data-stu-id="2712b-117">Are there seasonal variations? traffic peaks?</span></span>
   * <span data-ttu-id="2712b-118">Hoe snel moet Hallo app reageren</span><span class="sxs-lookup"><span data-stu-id="2712b-118">How fast should hello app respond?</span></span> <span data-ttu-id="2712b-119">1 seconde?</span><span class="sxs-lookup"><span data-stu-id="2712b-119">1 second?</span></span> <span data-ttu-id="2712b-120">1 milliseconde?</span><span class="sxs-lookup"><span data-stu-id="2712b-120">1 millisecond?</span></span>
3. <span data-ttu-id="2712b-121">Meer informatie over en correct hefboomwerking Hallo-platform die als host fungeert voor uw app.</span><span class="sxs-lookup"><span data-stu-id="2712b-121">Understanding and correctly leverage hello platform hosting your app.</span></span>
   * <span data-ttu-id="2712b-122">Wat functies moeten ik mijn doelstellingen scale tooachieve gebruiken?</span><span class="sxs-lookup"><span data-stu-id="2712b-122">What features should I leverage tooachieve my scale goals?</span></span>

<span data-ttu-id="2712b-123">Deze sectie wordt informatie over alle Hallo factoren en ontwerpen van een strategie wordt gebruikgemaakt van Hallo nodig App Service functies tooachieve uw schaalbaarheidsdoelstellingen help.</span><span class="sxs-lookup"><span data-stu-id="2712b-123">This section will help you understand all hello factors and help you devise a strategy that takes advantage of hello necessary App Service features tooachieve your scalability goals.</span></span>

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

