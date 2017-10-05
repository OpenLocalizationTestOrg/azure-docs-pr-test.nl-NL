---
title: 'Azure App Service: Schalen App Service-toepassingen'
description: Lees alles van toepassing schalen in App Service.
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
ms.openlocfilehash: 4ebaafe69fc1f91c7890611b14e8600df5c40cde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a><span data-ttu-id="47c7d-104">Azure App Service: Schalen App Service-toepassingen</span><span class="sxs-lookup"><span data-stu-id="47c7d-104">Azure App Service: Scaling App Service Applications</span></span>
<span data-ttu-id="47c7d-105">Toepassingen die worden gehost in Azure App Service kunnen [bereiken grootschalige](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span><span class="sxs-lookup"><span data-stu-id="47c7d-105">Applications hosted in Azure App Service can [achieve massive scale](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span></span>
<span data-ttu-id="47c7d-106">Een toepassing schalen is echter een complex probleem dat u beschikt niet over een oplossing 'één maat alle'.</span><span class="sxs-lookup"><span data-stu-id="47c7d-106">However, scaling an application is a complex problem that does not have a "one size fits all" solution.</span></span> <span data-ttu-id="47c7d-107">Uw toepassing er zijn correct schaal 3 sleutelgebieden's dragen bij aan uw succes toepassingen:</span><span class="sxs-lookup"><span data-stu-id="47c7d-107">To correctly scale your application there are 3 key areas that will contribute to your applications success:</span></span>

1. <span data-ttu-id="47c7d-108">Informatie over de toepassingsarchitectuur van uw en de zwakke punten.</span><span class="sxs-lookup"><span data-stu-id="47c7d-108">Understanding your application architecture and its weaknesses.</span></span>
   * <span data-ttu-id="47c7d-109">Is de Stateful van uw toepassing?</span><span class="sxs-lookup"><span data-stu-id="47c7d-109">Is your Application Stateful?</span></span> <span data-ttu-id="47c7d-110">Staatloze?</span><span class="sxs-lookup"><span data-stu-id="47c7d-110">Stateless?</span></span>
   * <span data-ttu-id="47c7d-111">Wat zijn de onderdelen van uw toepassing?</span><span class="sxs-lookup"><span data-stu-id="47c7d-111">What are all the components of your application?</span></span>
     * <span data-ttu-id="47c7d-112">Waar worden de knelpunten in de toepassing?</span><span class="sxs-lookup"><span data-stu-id="47c7d-112">Where are the bottlenecks in the application?</span></span>
   * <span data-ttu-id="47c7d-113">Bij het laden naar uw app wordt toegepast, wat verbreekt de eerste?</span><span class="sxs-lookup"><span data-stu-id="47c7d-113">When load is applied to your app, what will break first?</span></span>
2. <span data-ttu-id="47c7d-114">Informatie over de verwachte vereisten van load en prestaties.</span><span class="sxs-lookup"><span data-stu-id="47c7d-114">Understanding the expected load and performance requirements.</span></span>
   * <span data-ttu-id="47c7d-115">Moet de toepassing fungeren 1000 gebruikers? of een miljoen?</span><span class="sxs-lookup"><span data-stu-id="47c7d-115">Does the application need to serve one thousand users? or one million?</span></span>
   * <span data-ttu-id="47c7d-116">Wordt met verkeer afkomstig zijn uit één geografische locatie of globaal?</span><span class="sxs-lookup"><span data-stu-id="47c7d-116">Will traffic come from a single geographic location or globally?</span></span>
   * <span data-ttu-id="47c7d-117">Zijn er seizoensgebonden variaties? verkeer pieken?</span><span class="sxs-lookup"><span data-stu-id="47c7d-117">Are there seasonal variations? traffic peaks?</span></span>
   * <span data-ttu-id="47c7d-118">Hoe snel moet de app reageren</span><span class="sxs-lookup"><span data-stu-id="47c7d-118">How fast should the app respond?</span></span> <span data-ttu-id="47c7d-119">1 seconde?</span><span class="sxs-lookup"><span data-stu-id="47c7d-119">1 second?</span></span> <span data-ttu-id="47c7d-120">1 milliseconde?</span><span class="sxs-lookup"><span data-stu-id="47c7d-120">1 millisecond?</span></span>
3. <span data-ttu-id="47c7d-121">Meer informatie over en correct gebruikmaken van het platform voor het hosten van uw app.</span><span class="sxs-lookup"><span data-stu-id="47c7d-121">Understanding and correctly leverage the platform hosting your app.</span></span>
   * <span data-ttu-id="47c7d-122">Welke functies moet ik gebruiken voor het bereiken van Mijn doelen schaal</span><span class="sxs-lookup"><span data-stu-id="47c7d-122">What features should I leverage to achieve my scale goals?</span></span>

<span data-ttu-id="47c7d-123">Deze sectie helpt u begrijpen van de factoren en hulp bij het opstellen van een strategie wordt gebruikgemaakt van de benodigde App Service-functies om uw schaalbaarheidsdoelstellingen te realiseren.</span><span class="sxs-lookup"><span data-stu-id="47c7d-123">This section will help you understand all the factors and help you devise a strategy that takes advantage of the necessary App Service features to achieve your scalability goals.</span></span>

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

