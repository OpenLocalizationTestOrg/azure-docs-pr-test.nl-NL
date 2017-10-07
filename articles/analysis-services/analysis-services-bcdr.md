---
title: hoge beschikbaarheid van Analysis Services aaaAzure | Microsoft Docs
description: Zodat zeker Azure Analysis Services met hoge beschikbaarheid.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 6e09536c5bd7dc7f88f9b662e1a9f42d2b8c969b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analysis-services-high-availability"></a><span data-ttu-id="4fac8-103">Hoge beschikbaarheid van Analysis Services</span><span class="sxs-lookup"><span data-stu-id="4fac8-103">Analysis Services high availability</span></span>
<span data-ttu-id="4fac8-104">Dit artikel wordt beschreven zodat zeker hoge beschikbaarheid voor Azure Analysis Services-servers.</span><span class="sxs-lookup"><span data-stu-id="4fac8-104">This article describes assuring high availability for Azure Analysis Services servers.</span></span> 


## <a name="assuring-high-availability-during-a-service-disruption"></a><span data-ttu-id="4fac8-105">Hoge beschikbaarheid zodat zeker tijdens een service wordt onderbroken</span><span class="sxs-lookup"><span data-stu-id="4fac8-105">Assuring high availability during a service disruption</span></span>
<span data-ttu-id="4fac8-106">Hoewel dit zelden voorkomt, kan een storing in een Azure-datacenter hebben.</span><span class="sxs-lookup"><span data-stu-id="4fac8-106">While rare, an Azure data center can have an outage.</span></span> <span data-ttu-id="4fac8-107">Wanneer er een storing optreedt, wordt er een onderbreking van de bedrijven die mogelijk een paar minuten laatste of uur kan duren.</span><span class="sxs-lookup"><span data-stu-id="4fac8-107">When an outage occurs, it causes a business disruption that might last a few minutes or might last for hours.</span></span> <span data-ttu-id="4fac8-108">Hoge beschikbaarheid wordt vaak bereikt met server redundantie.</span><span class="sxs-lookup"><span data-stu-id="4fac8-108">High availability is most often achieved with server redundancy.</span></span> <span data-ttu-id="4fac8-109">U kunt met Azure Analysis Services redundantie bereiken door het maken van aanvullende, secundaire servers in een of meer regio's.</span><span class="sxs-lookup"><span data-stu-id="4fac8-109">With Azure Analysis Services, you can achieve redundancy by creating additional, secondary servers in one or more regions.</span></span> <span data-ttu-id="4fac8-110">Bij het maken van redundante servers, tooassure Hallo gegevens en metagegevens op die servers in de synchronisatie is met Hallo-server in een regio die is geworden offline, kunt u:</span><span class="sxs-lookup"><span data-stu-id="4fac8-110">When creating redundant servers, tooassure hello data and metadata on those servers is in-sync with hello server in a region that has gone offline, you can:</span></span>

* <span data-ttu-id="4fac8-111">Modellen tooredundant servers in andere regio's implementeren.</span><span class="sxs-lookup"><span data-stu-id="4fac8-111">Deploy models tooredundant servers in other regions.</span></span> <span data-ttu-id="4fac8-112">Deze methode moet verwerken van gegevens op uw primaire server en de redundante servers in parallel, zodat alle servers zeker synchroon.</span><span class="sxs-lookup"><span data-stu-id="4fac8-112">This method requires processing data on both your primary server and redundant servers in-parallel, assuring all servers are in-sync.</span></span>

* <span data-ttu-id="4fac8-113">Back-up databases uit de primaire server en terugzetten op servers met redundante.</span><span class="sxs-lookup"><span data-stu-id="4fac8-113">Back up databases from your primary server and restore on redundant servers.</span></span> <span data-ttu-id="4fac8-114">U kunt bijvoorbeeld elke nacht back-ups tooAzure opslag automatiseren en tooother redundante servers in andere regio's herstellen.</span><span class="sxs-lookup"><span data-stu-id="4fac8-114">For example, you can automate nightly backups tooAzure storage, and restore tooother redundant servers in other regions.</span></span> 

<span data-ttu-id="4fac8-115">Als een storing optreedt in de primaire server moet u in beide gevallen Hallo-verbindingsreeksen in rapportageserver clients tooconnect toohello in een andere regionale datacenter wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4fac8-115">In either case, if your primary server experiences an outage, you must change hello connection strings in reporting clients tooconnect toohello server in a different regional datacenter.</span></span> <span data-ttu-id="4fac8-116">Deze wijziging als een laatste toevlucht moet worden beschouwd en alleen als een onherstelbare regionale datacentrum optreedt.</span><span class="sxs-lookup"><span data-stu-id="4fac8-116">This change should be considered a last resort and only if a catastrophic regional data center outage occurs.</span></span> <span data-ttu-id="4fac8-117">Het is waarschijnlijk een datacentrum die als host fungeert voor de primaire server weer online zou komen voordat verbindingen op alle clients kan worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="4fac8-117">It's more likely a data center outage hosting your primary server would come back online before you could update connections on all clients.</span></span> 



## <a name="related-information"></a><span data-ttu-id="4fac8-118">Gerelateerde informatie</span><span class="sxs-lookup"><span data-stu-id="4fac8-118">Related information</span></span>
<span data-ttu-id="4fac8-119">[Back-up en herstel](analysis-services-backup.md) </span><span class="sxs-lookup"><span data-stu-id="4fac8-119">[Backup and restore](analysis-services-backup.md) </span></span>  
[<span data-ttu-id="4fac8-120">Azure analyseservices beheren</span><span class="sxs-lookup"><span data-stu-id="4fac8-120">Manage Azure Analysis Services</span></span>](analysis-services-manage.md) 

