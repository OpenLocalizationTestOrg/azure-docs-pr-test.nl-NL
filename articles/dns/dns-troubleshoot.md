---
title: aaaAzure DNS-probleemoplossingsgids | Microsoft Docs
description: Hoe tootroubleshoot algemene problemen met een Azure DNS
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: 95b01dc3-ee69-4575-a259-4227131e4f9c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/20/2017
ms.author: jonatul
ms.openlocfilehash: 944aa1811c980063f739268cd2c79b647b2754a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-troubleshooting-guide"></a><span data-ttu-id="d0ff7-103">Azure DNS-probleemoplossingsgids</span><span class="sxs-lookup"><span data-stu-id="d0ff7-103">Azure DNS troubleshooting guide</span></span>

<span data-ttu-id="d0ff7-104">Deze pagina bevat informatie over probleemoplossing voor veelgestelde vragen voor Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-104">This page provides troubleshooting information for common Azure DNS questions.</span></span>

<span data-ttu-id="d0ff7-105">Als deze stappen uw probleem niet verhelpen, kunt u ook zoeken naar of uw probleem post een bericht op onze [ondersteuning communityforum op MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span><span class="sxs-lookup"><span data-stu-id="d0ff7-105">If these steps don't resolve your issue, you can also search for or post your issue on our [community support forum on MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span></span> <span data-ttu-id="d0ff7-106">U kunt ook een Azure ondersteuningsaanvraag openen.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-106">Alternatively, open an Azure support request.</span></span>


## <a name="i-cant-create-a-dns-zone"></a><span data-ttu-id="d0ff7-107">Ik kan een DNS-zone niet maken.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-107">I can't create a DNS zone</span></span>

<span data-ttu-id="d0ff7-108">algemene problemen tooresolve, probeer een of meer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d0ff7-108">tooresolve common issues, try one or more of hello following steps:</span></span>

1.  <span data-ttu-id="d0ff7-109">Bekijk hello die Azure DNS audit logboeken toodetermine Hallo foutreden.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-109">Review hello Azure DNS audit logs toodetermine hello failure reason.</span></span>
2.  <span data-ttu-id="d0ff7-110">Elke DNS-zonenaam moet uniek zijn binnen de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-110">Each DNS zone name must be unique within its resource group.</span></span> <span data-ttu-id="d0ff7-111">Dat wil zeggen, twee DNS-zones Hello dezelfde naam van een resourcegroep niet delen.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-111">That is, two DNS zones with hello same name cannot share a resource group.</span></span> <span data-ttu-id="d0ff7-112">Gebruik een andere zonenaam of een andere resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-112">Try using a different zone name, or a different resource group.</span></span>
3.  <span data-ttu-id="d0ff7-113">Er wordt een fout "Bereikt of overschreden Hallo maximumaantal zones in abonnement {abonnements-id}."</span><span class="sxs-lookup"><span data-stu-id="d0ff7-113">You may see an error "You have reached or exceeded hello maximum number of zones in subscription {subscription id}."</span></span> <span data-ttu-id="d0ff7-114">Gebruik een ander Azure-abonnement, verwijder een aantal zones, of neem contact op met ondersteuning van Azure tooraise limiet voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-114">Either use a different Azure subscription, delete some zones, or contact Azure Support tooraise your subscription limit.</span></span>
4.  <span data-ttu-id="d0ff7-115">Mogelijk ziet u een fout 'hello zone '{zone-name}' is niet beschikbaar'.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-115">You may see an error "hello zone '{zone name}' is not available."</span></span> <span data-ttu-id="d0ff7-116">Deze fout betekent dat Azure DNS naamservers niet kan tooallocate voor deze DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-116">This error means that Azure DNS was unable tooallocate name servers for this DNS zone.</span></span> <span data-ttu-id="d0ff7-117">Gebruik dan een andere zonenaam.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-117">Try using a different zone name.</span></span> <span data-ttu-id="d0ff7-118">U kunt ook als u de domeineigenaar naam hello, contact op met ondersteuning van Azure, die de naamservers voor u kunt toewijzen.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-118">Alternatively, if you are hello domain name owner, contact Azure support, who can allocate name servers for you.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="d0ff7-119">**Aanbevolen documenten**</span><span class="sxs-lookup"><span data-stu-id="d0ff7-119">**Recommended documents**</span></span>

<span data-ttu-id="d0ff7-120">[DNS-zones en -records](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="d0ff7-120">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="d0ff7-121">
[Een DNS-zone maken](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d0ff7-121">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>

## <a name="i-cant-create-a-dns-record"></a><span data-ttu-id="d0ff7-122">Ik kan geen DNS-record maken</span><span class="sxs-lookup"><span data-stu-id="d0ff7-122">I can't create a DNS record</span></span>

<span data-ttu-id="d0ff7-123">algemene problemen tooresolve, probeer een of meer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d0ff7-123">tooresolve common issues, try one or more of hello following steps:</span></span>

1.  <span data-ttu-id="d0ff7-124">Bekijk hello die Azure DNS audit logboeken toodetermine Hallo foutreden.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-124">Review hello Azure DNS audit logs toodetermine hello failure reason.</span></span>
2.  <span data-ttu-id="d0ff7-125">Hallo-Recordset bestaat er al?</span><span class="sxs-lookup"><span data-stu-id="d0ff7-125">Does hello record set exist already?</span></span>  <span data-ttu-id="d0ff7-126">Azure DNS beheert records met behulp van de record *ingesteld*, die zijn Hallo verzameling records Hallo dezelfde naam en hetzelfde Hallo type.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-126">Azure DNS manages records using record *sets*, which are hello collection of records of hello same name and hello same type.</span></span> <span data-ttu-id="d0ff7-127">Als een record met Hallo dezelfde naam en typ het al bestaat, wordt tooadd een andere deze record moet u bestaande record Hallo bewerken ingesteld.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-127">If a record with hello same name and type already exists, then tooadd another such record you should edit hello existing record set.</span></span>
3.  <span data-ttu-id="d0ff7-128">Probeert u toocreate een record op Hallo DNS-zone apex (Hallo 'root' hello zone)?</span><span class="sxs-lookup"><span data-stu-id="d0ff7-128">Are you trying toocreate a record at hello DNS zone apex (hello ‘root’ of hello zone)?</span></span> <span data-ttu-id="d0ff7-129">Als dus Hallo DNS-conventie toouse Hallo ' @' teken als Hallo recordnaam.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-129">If so, hello DNS convention is toouse hello ‘@’ character as hello record name.</span></span> <span data-ttu-id="d0ff7-130">Let ook op dat Hallo DNS-standaarden staan niet toe dat CNAME-records in het toppunt Hallo zone.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-130">Also note that hello DNS standards do not permit CNAME records at hello zone apex.</span></span>
4.  <span data-ttu-id="d0ff7-131">Is er sprake van een CNAME-conflict?</span><span class="sxs-lookup"><span data-stu-id="d0ff7-131">Do you have a CNAME conflict?</span></span>  <span data-ttu-id="d0ff7-132">Hallo DNS-standaarden toegestaan een CNAME-record met dezelfde naam als een record van een ander type Hallo niet.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-132">hello DNS standards do not allow a CNAME record with hello same name as a record of any other type.</span></span> <span data-ttu-id="d0ff7-133">Als u een bestaande CNAME, het maken van een record met dezelfde naam van een ander type mislukt Hallo hebt.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-133">If you have an existing CNAME, creating a record with hello same name of a different type fails.</span></span>  <span data-ttu-id="d0ff7-134">Maken van een CNAME mislukt op dezelfde manier als Hallo naam overeenkomt met een bestaande record van een ander type.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-134">Likewise, creating a CNAME fails if hello name matches an existing record of a different type.</span></span> <span data-ttu-id="d0ff7-135">Hallo conflict verwijderen door het verwijderen van Hallo andere record of een andere recordnaam kiezen.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-135">Remove hello conflict by removing hello other record or choosing a different record name.</span></span>
5.  <span data-ttu-id="d0ff7-136">Hallo maximale aantal recordsets zijn toegestaan in een DNS-zone Hallo bereikt? huidige aantal recordsets Hallo en hello zijn maximum aantal recordsets weergegeven in hello Azure-portal onder Hallo eigenschappen voor Hallo zone.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-136">Have you reached hello limit on hello number of record sets permitted in a DNS zone? hello current number of record sets and hello maximum number of record sets are shown in hello Azure portal, under hello 'Properties' for hello zone.</span></span> <span data-ttu-id="d0ff7-137">Als u deze limiet is bereikt, klikt u vervolgens een aantal recordsets verwijderen of neem contact op met ondersteuning van Azure tooraise de limiet van uw recordset voor deze zone, en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-137">If you have reached this limit, then either delete some record sets or contact Azure Support tooraise your record set limit for this zone, then try again.</span></span> 


### <a name="recommended-documents"></a><span data-ttu-id="d0ff7-138">**Aanbevolen documenten**</span><span class="sxs-lookup"><span data-stu-id="d0ff7-138">**Recommended documents**</span></span>

<span data-ttu-id="d0ff7-139">[DNS-zones en -records](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="d0ff7-139">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="d0ff7-140">
[Een DNS-zone maken](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d0ff7-140">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>



## <a name="i-cant-resolve-my-dns-record"></a><span data-ttu-id="d0ff7-141">Ik kan mijn DNS-record niet omzetten</span><span class="sxs-lookup"><span data-stu-id="d0ff7-141">I can't resolve my DNS record</span></span>

<span data-ttu-id="d0ff7-142">De DNS-naamomzetting vereist meerdere stappen en kan om verschillende redenen mislukken.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-142">DNS name resolution is a multi-step process, which can fail for many reasons.</span></span> <span data-ttu-id="d0ff7-143">Hallo volgende stappen kunt u onderzoeken waarom de DNS-omzetting is mislukt voor een DNS-record in een zone die wordt gehost in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-143">hello following steps help you investigate why DNS resolution is failing for a DNS record in a zone hosted in Azure DNS.</span></span>

1.  <span data-ttu-id="d0ff7-144">Bevestig dat Hallo DNS-records correct zijn geconfigureerd in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-144">Confirm that hello DNS records have been configured correctly in Azure DNS.</span></span> <span data-ttu-id="d0ff7-145">Bekijk Hallo DNS-records in hello Azure-portal controleren Hallo zonenaam en recordnaam recordtype juist zijn.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-145">Review hello DNS records in hello Azure portal, checking that hello zone name, record name, and record type are correct.</span></span>
2.  <span data-ttu-id="d0ff7-146">Bevestig dat Hallo DNS-records correct op Hallo Azure DNS-naamservers omzetten.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-146">Confirm that hello DNS records resolve correctly on hello Azure DNS name servers.</span></span>
    - <span data-ttu-id="d0ff7-147">Als u DNS-query's van uw lokale PC, ziet u mogelijk resultaten in het cachegeheugen die niet met huidige status van de naamservers Hallo Hallo overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-147">If you make DNS queries from your local PC, you may see cached results that don’t reflect hello current state of hello name servers.</span></span>  <span data-ttu-id="d0ff7-148">Bedrijfsnetwerken gebruiken ook vaak proxyservers DNS-naamservers toospecific die verhinderen dat DNS-query's worden omgeleid.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-148">Also, corporate networks often use DNS proxy servers, which prevent DNS queries from being directed toospecific name servers.</span></span>  <span data-ttu-id="d0ff7-149">tooavoid deze problemen gebruiken op basis van web service voor naamomzetting zoals [digwebinterface](http://digwebinterface.com).</span><span class="sxs-lookup"><span data-stu-id="d0ff7-149">tooavoid these problems, use a web-based name resolution service such as [digwebinterface](http://digwebinterface.com).</span></span>
    - <span data-ttu-id="d0ff7-150">Worden ervoor toospecify Hallo juist naamservers voor uw DNS-zone, zoals wordt weergegeven in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-150">Be sure toospecify hello correct name servers for your DNS zone, as shown in hello Azure portal.</span></span>
    - <span data-ttu-id="d0ff7-151">Controleer of Hallo DNS-naam klopt (u toospecify Hallo volledig gekwalificeerde naam hebben, inclusief de naam van de zone Hallo) en Hallo recordtype juist is</span><span class="sxs-lookup"><span data-stu-id="d0ff7-151">Check that hello DNS name is correct (you have toospecify hello fully qualified name, including hello zone name) and hello record type is correct</span></span>
3.  <span data-ttu-id="d0ff7-152">Bevestig dat Hallo DNS-domeinnaam juist is [toohello Azure DNS-naamservers overgedragen](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="d0ff7-152">Confirm that hello DNS domain name has been correctly [delegated toohello Azure DNS name servers](dns-domain-delegation.md).</span></span> <span data-ttu-id="d0ff7-153">Er zijn [veel websites van derden die de DNS-delegering kunnen valideren](https://www.bing.com/search?q=dns+check+tool).</span><span class="sxs-lookup"><span data-stu-id="d0ff7-153">There are a [many 3rd-party web sites that offer DNS delegation validation](https://www.bing.com/search?q=dns+check+tool).</span></span> <span data-ttu-id="d0ff7-154">Deze test is een *zone* delegering test, zodat u alleen Hallo DNS-zone en niet Hallo volledig gekwalificeerde naam van de record moet invoeren.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-154">This test is a *zone* delegation test, so you should only enter hello DNS zone name and not hello fully qualified record name.</span></span>
4.  <span data-ttu-id="d0ff7-155">Hallo bovenstaande nadat is voltooid, uw DNS-record moet nu worden omgezet correct.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-155">Having completed hello above, your DNS record should now resolve correctly.</span></span> <span data-ttu-id="d0ff7-156">tooverify, die u opnieuw kunt gebruiken [digwebinterface](http://digwebinterface.com), nu met de naam Hallo-server standaardinstellingen.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-156">tooverify, you can again use [digwebinterface](http://digwebinterface.com), this time using hello default name server settings.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="d0ff7-157">**Aanbevolen documenten**</span><span class="sxs-lookup"><span data-stu-id="d0ff7-157">**Recommended documents**</span></span>

[<span data-ttu-id="d0ff7-158">Een domein tooAzure DNS overdragen</span><span class="sxs-lookup"><span data-stu-id="d0ff7-158">Delegate a domain tooAzure DNS</span></span>](dns-domain-delegation.md)



## <a name="how-do-i-specify-hello-service-and-protocol-for-an-srv-record"></a><span data-ttu-id="d0ff7-159">Hoe geef ik Hallo 'service' en 'protocol' voor een SRV-record</span><span class="sxs-lookup"><span data-stu-id="d0ff7-159">How do I specify hello ‘service’ and ‘protocol’ for an SRV record?</span></span>

<span data-ttu-id="d0ff7-160">Azure DNS beheert DNS-records als recordsets-verzameling van records met Hallo dezelfde naam en hetzelfde Hallo Hallo type.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-160">Azure DNS manages DNS records as record sets—hello collection of records with hello same name and hello same type.</span></span> <span data-ttu-id="d0ff7-161">Hallo 'service' en 'protocol' moeten een SRV-Recordset toobe opgegeven als deel van naam van de recordset Hallo.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-161">For an SRV record set, hello 'service' and 'protocol' need toobe specified as part of hello record set name.</span></span> <span data-ttu-id="d0ff7-162">Hallo worden andere parameters SRV ('prioriteit', 'gewicht', 'poort' en 'target') afzonderlijk opgegeven voor elke record in de recordset Hallo.</span><span class="sxs-lookup"><span data-stu-id="d0ff7-162">hello other SRV parameters ('priority', 'weight', 'port' and 'target') are specified separately for each record in hello record set.</span></span>

<span data-ttu-id="d0ff7-163">Voorbeeld van SRV-recordnamen (servicenaam 'sip', protocol 'tcp'):</span><span class="sxs-lookup"><span data-stu-id="d0ff7-163">Example SRV record names (service name 'sip', protocol 'tcp'):</span></span>

- <span data-ttu-id="d0ff7-164">\_SIP. \_tcp (maakt een record in het toppunt zone Hallo)</span><span class="sxs-lookup"><span data-stu-id="d0ff7-164">\_sip.\_tcp (creates a record set at hello zone apex)</span></span>
- <span data-ttu-id="d0ff7-165">\_sip.\_tcp.sipservice (er wordt een recordset gemaakt met de naam 'sipservice')</span><span class="sxs-lookup"><span data-stu-id="d0ff7-165">\_sip.\_tcp.sipservice (creates a record set named 'sipservice')</span></span>

### <a name="recommended-documents"></a><span data-ttu-id="d0ff7-166">**Aanbevolen documenten**</span><span class="sxs-lookup"><span data-stu-id="d0ff7-166">**Recommended documents**</span></span>

<span data-ttu-id="d0ff7-167">[DNS-zones en -records](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="d0ff7-167">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="d0ff7-168">
[DNS-recordsets en records maken met behulp van hello Azure-portal](dns-getstarted-create-recordset-portal.md)
</span><span class="sxs-lookup"><span data-stu-id="d0ff7-168">
[Create DNS record sets and records by using hello Azure portal](dns-getstarted-create-recordset-portal.md)
</span></span><br><span data-ttu-id="d0ff7-169">
[SRV-recordtype (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span><span class="sxs-lookup"><span data-stu-id="d0ff7-169">
[SRV record type (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span></span>


## <a name="next-steps"></a><span data-ttu-id="d0ff7-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d0ff7-170">Next steps</span></span>

* <span data-ttu-id="d0ff7-171">Meer informatie over [Azure DNS-zones en records](dns-zones-records.md)</span><span class="sxs-lookup"><span data-stu-id="d0ff7-171">Learn about [Azure DNS zones and records](dns-zones-records.md)</span></span>
* <span data-ttu-id="d0ff7-172">met behulp van Azure DNS toostart meer informatie over hoe te[maken van een DNS-zone](dns-getstarted-create-dnszone-portal.md) en [DNS-records maken](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d0ff7-172">toostart using Azure DNS, learn how too[create a DNS zone](dns-getstarted-create-dnszone-portal.md) and [create DNS records](dns-getstarted-create-recordset-portal.md).</span></span>
* <span data-ttu-id="d0ff7-173">een bestaande DNS-zone toomigrate meer informatie over hoe te[importeren en exporteren van een DNS-zonebestand](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="d0ff7-173">toomigrate an existing DNS zone, learn how too[import and export a DNS zone file](dns-import-export.md).</span></span>

