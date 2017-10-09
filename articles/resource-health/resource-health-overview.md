---
title: overzicht van aaaAzure bronnen health | Microsoft Docs
description: Overzicht van Azure-resourcestatus
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: resource-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 06/01/2016
ms.author: BernardoAMunoz
ms.openlocfilehash: b920241b2f64a0695ba2c32e9ccb0c2c3739986d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-overview"></a><span data-ttu-id="bf54a-103">Overzicht van Azure-resource-status</span><span class="sxs-lookup"><span data-stu-id="bf54a-103">Azure resource health overview</span></span>
 
<span data-ttu-id="bf54a-104">Resource Health helpt u bij het diagnosticeren en krijgen van ondersteuning wanneer een Azure-probleem van invloed is op uw resources.</span><span class="sxs-lookup"><span data-stu-id="bf54a-104">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span></span> <span data-ttu-id="bf54a-105">Dit biedt u informatie over de huidige en eerdere status Hallo van uw resources en helpt u problemen verhelpen.</span><span class="sxs-lookup"><span data-stu-id="bf54a-105">It informs you about hello current and past health of your resources and helps you mitigate issues.</span></span> <span data-ttu-id="bf54a-106">Resource Health biedt technische ondersteuning als u hulp nodig heeft bij problemen met Azure-services.</span><span class="sxs-lookup"><span data-stu-id="bf54a-106">Resource health provides technical support when you need help with Azure service issues.</span></span>

<span data-ttu-id="bf54a-107">Terwijl [Azure Status](https://status.azure.com) biedt u informatie over problemen met de service die invloed hebben op een uitgebreide reeks Azure-klanten, resourcestatus biedt u een aangepaste dashboard van Hallo status van uw resources.</span><span class="sxs-lookup"><span data-stu-id="bf54a-107">Whereas [Azure Status](https://status.azure.com) informs you about service issues that affect a broad set of Azure customers, resource health provides you with a personalized dashboard of hello health of your resources.</span></span> <span data-ttu-id="bf54a-108">Resourcestatus ziet u alle Hallo tijden uw resources niet beschikbaar in Hallo zijn achterstallige tooAzure problemen met de service.</span><span class="sxs-lookup"><span data-stu-id="bf54a-108">Resource health shows you all hello times your resources were unavailable in hello past due tooAzure service issues.</span></span> <span data-ttu-id="bf54a-109">Dit maakt het eenvoudig voor u toounderstand als een SLA is geschonden.</span><span class="sxs-lookup"><span data-stu-id="bf54a-109">This makes it simple for you toounderstand if an SLA was violated.</span></span> 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a><span data-ttu-id="bf54a-110">Wat wordt beschouwd als een resource en hoe gaat resourcestatus besluit als een bron in orde is?</span><span class="sxs-lookup"><span data-stu-id="bf54a-110">What is considered a resource and how does resource health decides if a resource is healthy or not?</span></span>
<span data-ttu-id="bf54a-111">Een bron is een exemplaar van een resourcetype die worden aangeboden door een Azure-service via Azure Resource Manager, bijvoorbeeld: een virtuele machine, een web-app of een SQL-database.</span><span class="sxs-lookup"><span data-stu-id="bf54a-111">A resource is an instance of a resource type offered by an Azure service through Azure Resource Manager, for example: a virtual machine, a web app, or a SQL database.</span></span>

<span data-ttu-id="bf54a-112">Resourcestatus is afhankelijk van signalen door Hallo verschillende Azure-services tooassess verzonden als een resource in orde of niet is.</span><span class="sxs-lookup"><span data-stu-id="bf54a-112">Resource health relies on signals emitted by hello different Azure services tooassess if a resource is healthy or not.</span></span> <span data-ttu-id="bf54a-113">Als een resource niet in orde is, analyseert resourcestatus aanvullende informatie toodetermine Hallo bron van Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="bf54a-113">If a resource is unhealthy, resource health analyzes additional information toodetermine hello source of hello problem.</span></span> <span data-ttu-id="bf54a-114">Ook worden acties die Microsoft duurt toofix Hallo probleem of acties die u kunt uitvoeren tooaddress Hallo veroorzaken van Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="bf54a-114">It also identifies actions Microsoft is taking toofix hello issue or what actions you can take tooaddress hello cause of hello problem.</span></span> 

<span data-ttu-id="bf54a-115">Bekijk Hallo volledige lijst met brontypen en health controleert [Azure resourcestatus](resource-health-checks-resource-types.md) voor meer informatie over hoe status wordt beoordeeld.</span><span class="sxs-lookup"><span data-stu-id="bf54a-115">Review hello full list of resource types and health checks in [Azure resource health](resource-health-checks-resource-types.md) for additional details on how health is assessed.</span></span>

## <a name="health-status-provided-by-resource-health"></a><span data-ttu-id="bf54a-116">Gezondheidsstatus geleverd door de resourcestatus</span><span class="sxs-lookup"><span data-stu-id="bf54a-116">Health status provided by resource health</span></span>
<span data-ttu-id="bf54a-117">Hallo-status van een bron is een van volgende statussen Hallo:</span><span class="sxs-lookup"><span data-stu-id="bf54a-117">hello health of a resource is one of hello following statuses:</span></span>

### <a name="available"></a><span data-ttu-id="bf54a-118">Beschikbaar</span><span class="sxs-lookup"><span data-stu-id="bf54a-118">Available</span></span>
<span data-ttu-id="bf54a-119">Hallo-service heeft alle gebeurtenissen die invloed hebben op Hallo status van Hallo resource niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="bf54a-119">hello service has not detected any events impacting hello health of hello resource.</span></span> <span data-ttu-id="bf54a-120">In gevallen waarbij Hallo resource is hersteld van niet-geplande uitvaltijd tijdens Hallo laatste 24 uur, u ziet Hallo **recent is hersteld** melding.</span><span class="sxs-lookup"><span data-stu-id="bf54a-120">In cases where hello resource has recovered from unplanned downtime during hello last 24 hours you will see hello **recently recovered** notification.</span></span>

![Bron health beschikbare virtuele machine](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a><span data-ttu-id="bf54a-122">Niet beschikbaar</span><span class="sxs-lookup"><span data-stu-id="bf54a-122">Unavailable</span></span>
<span data-ttu-id="bf54a-123">Hallo-service heeft een lopende platformupdate of niet-platformgebeurtenis die invloed hebben op Hallo status van Hallo resource gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="bf54a-123">hello service has detected an ongoing platform or non-platform event impacting hello health of hello resource.</span></span>

#### <a name="platform-events"></a><span data-ttu-id="bf54a-124">Platform-gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="bf54a-124">Platform events</span></span>
<span data-ttu-id="bf54a-125">Deze gebeurtenissen worden geactiveerd door meerdere onderdelen van hello Azure-infrastructuur en omvatten zowel geplande acties zoals gepland onderhoud en onverwachte incidenten, zoals een niet-geplande host opnieuw worden opgestart.</span><span class="sxs-lookup"><span data-stu-id="bf54a-125">These events are triggered by multiple components of hello Azure infrastructure and include both scheduled actions like planned maintenance and unexpected incidents like an unplanned host reboot.</span></span>

<span data-ttu-id="bf54a-126">Resourcestatus biedt aanvullende details over Hallo-gebeurtenis met het herstelproces Hallo en kunt u toocontact ondersteuning zelfs als u een actieve Microsoft overeenkomst ondersteunen geen hebt.</span><span class="sxs-lookup"><span data-stu-id="bf54a-126">Resource health provides additional details on hello event, hello recovery process and enables you toocontact support even if you don't have an active Microsoft support agreement.</span></span>

![Resource health niet via een virtuele machine vanwege tooplatform gebeurtenis](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a><span data-ttu-id="bf54a-128">Niet-Platform-gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="bf54a-128">Non-Platform events</span></span>
<span data-ttu-id="bf54a-129">Deze gebeurtenissen worden geactiveerd door acties die worden uitgevoerd door gebruikers, bijvoorbeeld een virtuele machine stoppen of het maximum aantal verbindingen tooa Redis-Cache Hallo bereikt.</span><span class="sxs-lookup"><span data-stu-id="bf54a-129">These events are triggered by actions taken by users, for example stopping a virtual machine or reaching hello maximum number of connections tooa Redis Cache.</span></span>

![Resource health niet via een virtuele machine vanwege toonon platformgebeurtenis](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a><span data-ttu-id="bf54a-131">Onbekend</span><span class="sxs-lookup"><span data-stu-id="bf54a-131">Unknown</span></span>
<span data-ttu-id="bf54a-132">Deze health-status geeft aan dat resourcestatus informatie over deze bron voor meer dan 10 minuten niet heeft ontvangen.</span><span class="sxs-lookup"><span data-stu-id="bf54a-132">This health status indicates that resource health has not received information about this resource for more than 10 minutes.</span></span> <span data-ttu-id="bf54a-133">Deze status is niet een definitieve indicatie van Hallo status van Hallo bron, zijn maar er een belangrijk gegevenspunt in Hallo procedure voor probleemoplossing:</span><span class="sxs-lookup"><span data-stu-id="bf54a-133">While this status is not a definitive indication of hello state of hello resource, it is an important data point in hello troubleshooting process:</span></span>
* <span data-ttu-id="bf54a-134">Als Hallo resource wordt uitgevoerd als de status van de verwachte Hallo van Hallo resource wordt tooAvailable bijgewerkt na een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="bf54a-134">If hello resource is running as expected hello status of hello resource will update tooAvailable after a few minutes.</span></span>
* <span data-ttu-id="bf54a-135">Als u problemen met Hallo resource ondervindt, hello onbekende gezondheidsstatus kan worden voorgesteld Hallo resource wordt beïnvloed door een gebeurtenis in het Hallo-platform.</span><span class="sxs-lookup"><span data-stu-id="bf54a-135">If you are experiencing problems with hello resource, hello Unknown health status may suggest hello resource is impacted by an event in hello platform.</span></span>

![Bron health onbekende virtuele machine](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a><span data-ttu-id="bf54a-137">Een onjuiste status rapporteren</span><span class="sxs-lookup"><span data-stu-id="bf54a-137">Report an incorrect status</span></span>
<span data-ttu-id="bf54a-138">Als u Hallo huidige health-status is onjuist op elk gewenst moment denkt, kunt u laat ons weten door te klikken op **rapporteren onjuist gezondheidsstatus**.</span><span class="sxs-lookup"><span data-stu-id="bf54a-138">If at any point you believe hello current health status is incorrect, you can let us know by clicking **Report incorrect health status**.</span></span> <span data-ttu-id="bf54a-139">In gevallen waarin u worden beïnvloed door een probleem met de Azure, raden we u toocontact ondersteuning van de resourceblade health Hallo.</span><span class="sxs-lookup"><span data-stu-id="bf54a-139">In cases where you are impacted by an Azure problem, we encourage you toocontact support from hello resource health blade.</span></span> 

![Resourcestatus rapport onjuiste Status](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a><span data-ttu-id="bf54a-141">Historische gegevens</span><span class="sxs-lookup"><span data-stu-id="bf54a-141">Historical Information</span></span>
<span data-ttu-id="bf54a-142">U toegang hebt tot too14 dagen van historische gegevens door te klikken op **Historie weergeven** Hallo bron health-blade.</span><span class="sxs-lookup"><span data-stu-id="bf54a-142">You can access up too14 days of historical health data by clicking **View History** in hello Resource health blade.</span></span> 

![Resourcestatus rapportgeschiedenis](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a><span data-ttu-id="bf54a-144">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="bf54a-144">Getting started</span></span>
<span data-ttu-id="bf54a-145">tooopen resourcestatus voor één resource</span><span class="sxs-lookup"><span data-stu-id="bf54a-145">tooopen Resource health for one resource</span></span>
1.  <span data-ttu-id="bf54a-146">Meld u aan bij hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="bf54a-146">Sign in into hello Azure portal.</span></span>
2.  <span data-ttu-id="bf54a-147">Navigeer tooyour resource.</span><span class="sxs-lookup"><span data-stu-id="bf54a-147">Navigate tooyour resource.</span></span>
3.  <span data-ttu-id="bf54a-148">Hallo resource menu zich in de linkerkant hello, klik op **resourcestatus**.</span><span class="sxs-lookup"><span data-stu-id="bf54a-148">In hello resource menu located in hello left-hand side, click **Resource health**.</span></span>

![Open resourcestatus van Resource-blade](./media/resource-health-overview/from-resource-blade.png)

<span data-ttu-id="bf54a-150">U kunt de resourcestatus ook openen door te klikken op **meer services**, en typ **resourcestatus** in filter tekst vak tooopen hello **Help + ondersteuning** blade.</span><span class="sxs-lookup"><span data-stu-id="bf54a-150">You can also access resource health by clicking **More services**, and typing **resource health** in filter text box tooopen hello **Help + Support** blade.</span></span> <span data-ttu-id="bf54a-151">Klik tot slot [ **resourcestatus**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span><span class="sxs-lookup"><span data-stu-id="bf54a-151">Finally click [**Resource health**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span></span>

![Resourcestatus openen vanuit meer service](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a><span data-ttu-id="bf54a-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bf54a-153">Next steps</span></span>

<span data-ttu-id="bf54a-154">Bekijk deze resources toolearn meer informatie over de resourcestatus:</span><span class="sxs-lookup"><span data-stu-id="bf54a-154">Check out these resources toolearn more about resource health:</span></span>
-  [<span data-ttu-id="bf54a-155">Status van resourcetypen en controleert in Azure resourcestatus</span><span class="sxs-lookup"><span data-stu-id="bf54a-155">Resource types and health checks in Azure resource health</span></span>](resource-health-checks-resource-types.md)
-  [<span data-ttu-id="bf54a-156">Veelgestelde vragen over Azure-resource-status</span><span class="sxs-lookup"><span data-stu-id="bf54a-156">Frequently asked questions about Azure resource health</span></span>](resource-health-faq.md)




