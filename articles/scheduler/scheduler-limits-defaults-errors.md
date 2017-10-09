---
title: aaaScheduler limieten en de standaardinstellingen
description: Scheduler-limieten en de standaardinstellingen
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 88f4a3e9-6dbd-4943-8543-f0649d423061
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 6fe0600d3ce3249d5aab1b877369b175316b5437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-limits-and-defaults"></a><span data-ttu-id="657ba-103">Scheduler-limieten en de standaardinstellingen</span><span class="sxs-lookup"><span data-stu-id="657ba-103">Scheduler Limits and Defaults</span></span>
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a><span data-ttu-id="657ba-104">Scheduler-quota, limieten, standaardwaarden en vertragingen</span><span class="sxs-lookup"><span data-stu-id="657ba-104">Scheduler Quotas, Limits, Defaults, and Throttles</span></span>
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="hello-x-ms-request-id-header"></a><span data-ttu-id="657ba-105">x-ms-aanvraag-id Hallo koptekst</span><span class="sxs-lookup"><span data-stu-id="657ba-105">hello x-ms-request-id Header</span></span>
<span data-ttu-id="657ba-106">Elk verzoek tegen Hallo Scheduler-service retourneert een antwoordheader genaamd**x-ms-aanvraag-id**. Deze koptekst bevat een ondoorzichtige waarde met een unieke identificatie Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="657ba-106">Every request made against hello Scheduler service returns a response header named**x-ms-request-id**. This header contains an opaque value that uniquely identifies hello request.</span></span>

<span data-ttu-id="657ba-107">Als een aanvraag consistent is hebt mislukt en u gecontroleerd dat Hallo verzoek goed geformuleerd is, mag u deze waarde tooreport Hallo fout tooMicrosoft.</span><span class="sxs-lookup"><span data-stu-id="657ba-107">If a request is consistently failing and you have verified that hello request is properly formulated, you may use this value tooreport hello error tooMicrosoft.</span></span> <span data-ttu-id="657ba-108">Opnemen in uw rapport Hallo-waarde van de x-ms-aanvraag-id Hallo bij benadering de tijd die Hallo-aanvraag is aangebracht, Hallo-id van het Hallo-abonnement, taakverzameling en/of taak en type bewerking dat verzoek heeft geprobeerd Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="657ba-108">In your report, include hello value of x-ms-request-id, hello approximate time that hello request was made, hello identifier of hello subscription, job collection, and/or job, and hello type of operation that hello request attempted.</span></span>

## <a name="see-also"></a><span data-ttu-id="657ba-109">Zie ook</span><span class="sxs-lookup"><span data-stu-id="657ba-109">See Also</span></span>
 [<span data-ttu-id="657ba-110">Wat is Scheduler?</span><span class="sxs-lookup"><span data-stu-id="657ba-110">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="657ba-111">Azure Scheduler-concepten, -terminologie en -entiteitenhiërarchie</span><span class="sxs-lookup"><span data-stu-id="657ba-111">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="657ba-112">Aan de slag met behulp van Scheduler in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="657ba-112">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="657ba-113">Plannen en facturering in Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="657ba-113">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="657ba-114">Naslaginformatie over REST API van Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="657ba-114">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="657ba-115">Naslaginformatie over Azure Scheduler PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="657ba-115">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="657ba-116">Hoge beschikbaarheid en betrouwbaarheid van Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="657ba-116">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="657ba-117">Azure Scheduler uitgaande verificatie</span><span class="sxs-lookup"><span data-stu-id="657ba-117">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

