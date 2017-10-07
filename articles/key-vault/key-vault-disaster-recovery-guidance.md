---
title: aaaWhat toodo in Hallo-gebeurtenis van een onderbreking van de Azure-service die gevolgen heeft voor Azure Sleutelkluis | Microsoft Docs
description: Meer informatie over welke toodo in Hallo-gebeurtenis van een onderbreking van de Azure-service die gevolgen heeft voor Azure Sleutelkluis.
services: key-vault
documentationcenter: 
author: adamglick
manager: mbaldwin
editor: 
ms.assetid: 19a9af63-3032-447b-9d1a-b0125f384edb
ms.service: key-vault
ms.workload: key-vault
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: sumedhb;aglick
ms.openlocfilehash: 88eec82ada401a28323b3eea126168185ba4cdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a><span data-ttu-id="f1adb-103">Azure Sleutelkluis beschikbaarheid en redundantie</span><span class="sxs-lookup"><span data-stu-id="f1adb-103">Azure Key Vault availability and redundancy</span></span>
<span data-ttu-id="f1adb-104">Azure Sleutelkluis is uitgerust met meerdere lagen van redundantie toomake u ervoor zorgen dat uw sleutels en geheimen toepassing tooyour beschikbaar blijven zelfs als afzonderlijke onderdelen van Hallo-service is mislukt.</span><span class="sxs-lookup"><span data-stu-id="f1adb-104">Azure Key Vault features multiple layers of redundancy toomake sure that your keys and secrets remain available tooyour application even if individual components of hello service fail.</span></span>

<span data-ttu-id="f1adb-105">Hallo inhoud van uw sleutelkluis wordt gerepliceerd binnen Hallo regio en de secundaire regio tooa ten minste 150 mijl verwijderd, maar binnen Hallo hetzelfde Geografie.</span><span class="sxs-lookup"><span data-stu-id="f1adb-105">hello contents of your key vault are replicated within hello region and tooa secondary region at least 150 miles away but within hello same geography.</span></span> <span data-ttu-id="f1adb-106">Dit onderhoudt gebied van duurzaamheid van uw sleutels en geheimen.</span><span class="sxs-lookup"><span data-stu-id="f1adb-106">This maintains high durability of your keys and secrets.</span></span> <span data-ttu-id="f1adb-107">Zie Hallo [Azure regio's gekoppeld](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) document voor meer informatie over specifieke regio-paren.</span><span class="sxs-lookup"><span data-stu-id="f1adb-107">See hello [Azure paired regions](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) document for details on specific region pairs.</span></span>

<span data-ttu-id="f1adb-108">Als afzonderlijke onderdelen in de sleutelkluis-service Hallo mislukken, stap alternatieve onderdelen binnen Hallo regio in tooserve uw aanvraag toomake ervoor dat er geen verslechtering van de functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="f1adb-108">If individual components within hello key vault service fail, alternate components within hello region step in tooserve your request toomake sure that there is no degradation of functionality.</span></span> <span data-ttu-id="f1adb-109">U hoeft geen tootake elke actie tootrigger dit.</span><span class="sxs-lookup"><span data-stu-id="f1adb-109">You do not need tootake any action tootrigger this.</span></span> <span data-ttu-id="f1adb-110">Dit gebeurt automatisch en transparant tooyou zijn.</span><span class="sxs-lookup"><span data-stu-id="f1adb-110">It happens automatically and will be transparent tooyou.</span></span>

<span data-ttu-id="f1adb-111">In Hallo zeldzame geval dat een volledige Azure-regio niet beschikbaar is, Hallo-aanvragen die u van Azure Sleutelkluis in deze regio aanbrengt automatisch doorgestuurd (*failover*) tooa secundaire regio.</span><span class="sxs-lookup"><span data-stu-id="f1adb-111">In hello rare event that an entire Azure region is unavailable, hello requests that you make of Azure Key Vault in that region are automatically routed (*failed over*) tooa secondary region.</span></span> <span data-ttu-id="f1adb-112">Wanneer de primaire regio Hallo weer beschikbaar is, aanvragen terug doorgestuurd (*kan niet terug*) toohello primaire regio.</span><span class="sxs-lookup"><span data-stu-id="f1adb-112">When hello primary region is available again, requests are routed back (*failed back*) toohello primary region.</span></span> <span data-ttu-id="f1adb-113">Opnieuw, u hoeft niet tootake geen actie omdat dit automatisch gebeurt.</span><span class="sxs-lookup"><span data-stu-id="f1adb-113">Again, you do not need tootake any action because this happens automatically.</span></span>

<span data-ttu-id="f1adb-114">Er zijn enkele aanvullende opmerkingen toobe op de hoogte van:</span><span class="sxs-lookup"><span data-stu-id="f1adb-114">There are a few caveats toobe aware of:</span></span>

* <span data-ttu-id="f1adb-115">In geval van een failover regio Hallo duurt enkele minuten duren voordat Hallo service toofail via.</span><span class="sxs-lookup"><span data-stu-id="f1adb-115">In hello event of a region failover, it may take a few minutes for hello service toofail over.</span></span> <span data-ttu-id="f1adb-116">Aanvragen die afkomstig zijn gedurende deze tijd mislukken totdat de Hallo failover is voltooid.</span><span class="sxs-lookup"><span data-stu-id="f1adb-116">Requests that are made during this time may fail until hello failover completes.</span></span>
* <span data-ttu-id="f1adb-117">Nadat een failover voltooid is, wordt de sleutelkluis in de modus alleen-lezen is.</span><span class="sxs-lookup"><span data-stu-id="f1adb-117">After a failover is complete, your key vault is in read-only mode.</span></span> <span data-ttu-id="f1adb-118">Aanvragen die worden ondersteund in deze modus zijn:</span><span class="sxs-lookup"><span data-stu-id="f1adb-118">Requests that are supported in this mode are:</span></span>
  * <span data-ttu-id="f1adb-119">Lijst sleutelkluizen</span><span class="sxs-lookup"><span data-stu-id="f1adb-119">List key vaults</span></span>
  * <span data-ttu-id="f1adb-120">Eigenschappen van sleutelkluizen opgehaald</span><span class="sxs-lookup"><span data-stu-id="f1adb-120">Get properties of key vaults</span></span>
  * <span data-ttu-id="f1adb-121">Lijst met geheimen</span><span class="sxs-lookup"><span data-stu-id="f1adb-121">List secrets</span></span>
  * <span data-ttu-id="f1adb-122">Ophalen van geheimen</span><span class="sxs-lookup"><span data-stu-id="f1adb-122">Get secrets</span></span>
  * <span data-ttu-id="f1adb-123">Lijst met sleutels</span><span class="sxs-lookup"><span data-stu-id="f1adb-123">List keys</span></span>
  * <span data-ttu-id="f1adb-124">(Eigenschappen van)-sleutels ophalen</span><span class="sxs-lookup"><span data-stu-id="f1adb-124">Get (properties of) keys</span></span>
  * <span data-ttu-id="f1adb-125">Versleutelen</span><span class="sxs-lookup"><span data-stu-id="f1adb-125">Encrypt</span></span>
  * <span data-ttu-id="f1adb-126">Ontsleutelen</span><span class="sxs-lookup"><span data-stu-id="f1adb-126">Decrypt</span></span>
  * <span data-ttu-id="f1adb-127">Tekstterugloop</span><span class="sxs-lookup"><span data-stu-id="f1adb-127">Wrap</span></span>
  * <span data-ttu-id="f1adb-128">Uitpakken</span><span class="sxs-lookup"><span data-stu-id="f1adb-128">Unwrap</span></span>
  * <span data-ttu-id="f1adb-129">Verifiëren</span><span class="sxs-lookup"><span data-stu-id="f1adb-129">Verify</span></span>
  * <span data-ttu-id="f1adb-130">Aanmelding</span><span class="sxs-lookup"><span data-stu-id="f1adb-130">Sign</span></span>
  * <span data-ttu-id="f1adb-131">Back-up</span><span class="sxs-lookup"><span data-stu-id="f1adb-131">Backup</span></span>
* <span data-ttu-id="f1adb-132">Na een failover terug mislukte is, alle aanvraagtypen (inclusief lezen *en* schrijfaanvragen) beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="f1adb-132">After a failover is failed back, all request types (including read *and* write requests) are available.</span></span>

