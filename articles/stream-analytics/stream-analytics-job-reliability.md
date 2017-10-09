---
title: Vermijd serviceonderbrekingen met Azure Stream Analytics-taken | Microsoft Docs
description: Richtlijnen voor het maken van uw Stream Analytics taken robuuste upgrade.
services: stream-analytics
documentationCenter: 
authors: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3ac65c93ecb47e93e963dd9869a7af70f73b19c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="guarantee-stream-analytics-job-reliability-during-service-updates"></a><span data-ttu-id="26c6d-103">Stream Analytics-taak betrouwbaarheid garanderen tijdens de service-updates</span><span class="sxs-lookup"><span data-stu-id="26c6d-103">Guarantee Stream Analytics job reliability during service updates</span></span>

<span data-ttu-id="26c6d-104">Deel van een volledig beheerde service wordt is Hallo mogelijkheid toointroduce nieuwe service-functionaliteit en verbeteringen in een snelle tempo.</span><span class="sxs-lookup"><span data-stu-id="26c6d-104">Part of being a fully managed service is hello capability toointroduce new service functionality and improvements at a rapid pace.</span></span> <span data-ttu-id="26c6d-105">Stream Analytics kan hierdoor een service-update implementeert op basis van wekelijkse (of vaker) hebben.</span><span class="sxs-lookup"><span data-stu-id="26c6d-105">As a result, Stream Analytics can have a service update deploy on a weekly (or more frequent) basis.</span></span> <span data-ttu-id="26c6d-106">Ongeacht hoeveel tests worden uitgevoerd nog er steeds het risico bestaat dat een bestaande, actieve taak is het vanwege toohello introductie van een fout verbroken mogelijk.</span><span class="sxs-lookup"><span data-stu-id="26c6d-106">No matter how much testing is done there is still a risk that an existing, running job may break due toohello introduction of a bug.</span></span> <span data-ttu-id="26c6d-107">Voor klanten die kritieke streaming verwerking taken die risico's uitvoeren nodig toobe vermeden.</span><span class="sxs-lookup"><span data-stu-id="26c6d-107">For customers who run critical streaming processing jobs these risks need toobe avoided.</span></span> <span data-ttu-id="26c6d-108">Een mechanisme voor klanten kunt tooreduce dit risico is een Azure  **[gekoppelde regio](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  model.</span><span class="sxs-lookup"><span data-stu-id="26c6d-108">A mechanism customers can use tooreduce this risk is Azure’s **[paired region](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** model.</span></span> 

## <a name="how-do-azure-paired-regions-address-this-concern"></a><span data-ttu-id="26c6d-109">Hoe gekoppelde Azure-regio adresseren van dit te voorkomen?</span><span class="sxs-lookup"><span data-stu-id="26c6d-109">How do Azure paired regions address this concern?</span></span>

<span data-ttu-id="26c6d-110">Stream Analytics-taken in de gekoppelde regio's worden bijgewerkt in afzonderlijke batches wordt gegarandeerd.</span><span class="sxs-lookup"><span data-stu-id="26c6d-110">Stream Analytics guarantees jobs in paired regions are updated in separate batches.</span></span> <span data-ttu-id="26c6d-111">Er is als gevolg hiervan een voldoende tijdsverschil tussen Hallo updates tooidentify potentiële nieuwste fouten en ze herstellen.</span><span class="sxs-lookup"><span data-stu-id="26c6d-111">As a result there is a sufficient time gap between hello updates tooidentify potential breaking bugs and remediate them.</span></span>

<span data-ttu-id="26c6d-112">_Met uitzondering van centrale India Hallo_ (waarvan gekoppelde regio, Zuid, India geen Stream Analytics aanwezigheid), Hallo-implementatie van een update tooStream Analytics niet op Hallo plaatsvindt dezelfde periode in een set van gekoppelde regio's.</span><span class="sxs-lookup"><span data-stu-id="26c6d-112">_With hello exception of Central India_ (whose paired region, South India, does not have Stream Analytics presence), hello deployment of an update tooStream Analytics would not occur at hello same time in a set of paired regions.</span></span> <span data-ttu-id="26c6d-113">Implementaties in meerdere regio's **in Hallo dezelfde groep** optreden **op Hallo hetzelfde moment**.</span><span class="sxs-lookup"><span data-stu-id="26c6d-113">Deployments in multiple regions **in hello same group** may occur **at hello same time**.</span></span>

<span data-ttu-id="26c6d-114">Hallo-artikel op  **[beschikbaarheid en gekoppelde regio's](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  heeft de meest actuele informatie Hallo op welke regio's zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="26c6d-114">hello article on **[availability and paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** has hello most up-to-date information on which regions are paired.</span></span>

<span data-ttu-id="26c6d-115">Klanten wordt aangeraden toodeploy identiek taken tooboth gekoppeld regio's.</span><span class="sxs-lookup"><span data-stu-id="26c6d-115">Customers are advised toodeploy identical jobs tooboth paired regions.</span></span> <span data-ttu-id="26c6d-116">Bovendien tooStream Analytics interne bewakingsmogelijkheden, klanten ook zijn aangeraden toomonitor Hallo taken als **beide** zijn productietaken.</span><span class="sxs-lookup"><span data-stu-id="26c6d-116">In addition tooStream Analytics internal monitoring capabilities, customers are also advised toomonitor hello jobs as if **both** are production jobs.</span></span> <span data-ttu-id="26c6d-117">Als een einde geïdentificeerde toobe een resultaat van Hallo Stream Analytics-service-update, escaleren op de juiste wijze en downstream consumenten toohello orde taakuitvoer failover.</span><span class="sxs-lookup"><span data-stu-id="26c6d-117">If a break is identified toobe a result of hello Stream Analytics service update, escalate appropriately and fail over any downstream consumers toohello healthy job output.</span></span> <span data-ttu-id="26c6d-118">Escalatie toosupport wordt Hallo gekoppelde regio te voorkomen dat wordt beïnvloed door de nieuwe implementatie Hallo en Hallo integriteit van Hallo gekoppeld taken beheren.</span><span class="sxs-lookup"><span data-stu-id="26c6d-118">Escalation toosupport will prevent hello paired region from being affected by hello new deployment and maintain hello integrity of hello paired jobs.</span></span>
