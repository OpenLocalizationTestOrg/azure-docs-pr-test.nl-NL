---
title: Azure DNS-probleemoplossingsgids | Microsoft Docs
description: Het oplossen van veelvoorkomende problemen met Azure DNS
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
ms.openlocfilehash: 1d9bb681a864bdc3e5a2f9c9a531d9566b16ada4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-dns-troubleshooting-guide"></a><span data-ttu-id="9c452-103">Azure DNS-probleemoplossingsgids</span><span class="sxs-lookup"><span data-stu-id="9c452-103">Azure DNS troubleshooting guide</span></span>

<span data-ttu-id="9c452-104">Deze pagina bevat informatie over probleemoplossing voor veelgestelde vragen voor Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="9c452-104">This page provides troubleshooting information for common Azure DNS questions.</span></span>

<span data-ttu-id="9c452-105">Als deze stappen uw probleem niet verhelpen, kunt u ook zoeken naar of uw probleem post een bericht op onze [ondersteuning communityforum op MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span><span class="sxs-lookup"><span data-stu-id="9c452-105">If these steps don't resolve your issue, you can also search for or post your issue on our [community support forum on MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span></span> <span data-ttu-id="9c452-106">U kunt ook een Azure ondersteuningsaanvraag openen.</span><span class="sxs-lookup"><span data-stu-id="9c452-106">Alternatively, open an Azure support request.</span></span>


## <a name="i-cant-create-a-dns-zone"></a><span data-ttu-id="9c452-107">Ik kan een DNS-zone niet maken.</span><span class="sxs-lookup"><span data-stu-id="9c452-107">I can't create a DNS zone</span></span>

<span data-ttu-id="9c452-108">Probeer een of meer van de volgende stappen om veelvoorkomende problemen op te lossen:</span><span class="sxs-lookup"><span data-stu-id="9c452-108">To resolve common issues, try one or more of the following steps:</span></span>

1.  <span data-ttu-id="9c452-109">Controleer de auditlogboeken van Azure DNS om de reden van de fout vast te stellen.</span><span class="sxs-lookup"><span data-stu-id="9c452-109">Review the Azure DNS audit logs to determine the failure reason.</span></span>
2.  <span data-ttu-id="9c452-110">Elke DNS-zonenaam moet uniek zijn binnen de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="9c452-110">Each DNS zone name must be unique within its resource group.</span></span> <span data-ttu-id="9c452-111">Een resourcegroep kan dus niet twee DNS-zones met dezelfde naam bevatten.</span><span class="sxs-lookup"><span data-stu-id="9c452-111">That is, two DNS zones with the same name cannot share a resource group.</span></span> <span data-ttu-id="9c452-112">Gebruik een andere zonenaam of een andere resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="9c452-112">Try using a different zone name, or a different resource group.</span></span>
3.  <span data-ttu-id="9c452-113">U ziet mogelijk de foutmelding 'Het maximumaantal zones in abonnement {abonnements-id} is bereikt of overschreden'.</span><span class="sxs-lookup"><span data-stu-id="9c452-113">You may see an error "You have reached or exceeded the maximum number of zones in subscription {subscription id}."</span></span> <span data-ttu-id="9c452-114">Gebruik een ander Azure-abonnement, verwijder enkele zones of neem contact op met de ondersteuning van Azure om uw abonnementslimiet te verhogen.</span><span class="sxs-lookup"><span data-stu-id="9c452-114">Either use a different Azure subscription, delete some zones, or contact Azure Support to raise your subscription limit.</span></span>
4.  <span data-ttu-id="9c452-115">U ziet mogelijk de foutmelding 'De zone {zonenaam} is niet beschikbaar'.</span><span class="sxs-lookup"><span data-stu-id="9c452-115">You may see an error "The zone '{zone name}' is not available."</span></span> <span data-ttu-id="9c452-116">Dit betekent dat Azure DNS geen naamservers kan toewijzen voor deze DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="9c452-116">This error means that Azure DNS was unable to allocate name servers for this DNS zone.</span></span> <span data-ttu-id="9c452-117">Gebruik dan een andere zonenaam.</span><span class="sxs-lookup"><span data-stu-id="9c452-117">Try using a different zone name.</span></span> <span data-ttu-id="9c452-118">Als u de eigenaar van de domeinnaam bent, kunt u ook de ondersteuning van Azure vragen naamservers voor u toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="9c452-118">Alternatively, if you are the domain name owner, contact Azure support, who can allocate name servers for you.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="9c452-119">**Aanbevolen documenten**</span><span class="sxs-lookup"><span data-stu-id="9c452-119">**Recommended documents**</span></span>

<span data-ttu-id="9c452-120">[DNS-zones en -records](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="9c452-120">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="9c452-121">
[Een DNS-zone maken](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="9c452-121">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>

## <a name="i-cant-create-a-dns-record"></a><span data-ttu-id="9c452-122">Ik kan geen DNS-record maken</span><span class="sxs-lookup"><span data-stu-id="9c452-122">I can't create a DNS record</span></span>

<span data-ttu-id="9c452-123">Probeer een of meer van de volgende stappen om veelvoorkomende problemen op te lossen:</span><span class="sxs-lookup"><span data-stu-id="9c452-123">To resolve common issues, try one or more of the following steps:</span></span>

1.  <span data-ttu-id="9c452-124">Controleer de auditlogboeken van Azure DNS om de reden van de fout vast te stellen.</span><span class="sxs-lookup"><span data-stu-id="9c452-124">Review the Azure DNS audit logs to determine the failure reason.</span></span>
2.  <span data-ttu-id="9c452-125">Bestaat de recordset al?</span><span class="sxs-lookup"><span data-stu-id="9c452-125">Does the record set exist already?</span></span>  <span data-ttu-id="9c452-126">Azure DNS beheert records als *recordsets*. Hierin zijn records met dezelfde naam en van hetzelfde type opgenomen.</span><span class="sxs-lookup"><span data-stu-id="9c452-126">Azure DNS manages records using record *sets*, which are the collection of records of the same name and the same type.</span></span> <span data-ttu-id="9c452-127">Als er al een record met dezelfde naam en van hetzelfde type bestaat, kunt u nog een dergelijke record toevoegen door de bestaande recordset te bewerken.</span><span class="sxs-lookup"><span data-stu-id="9c452-127">If a record with the same name and type already exists, then to add another such record you should edit the existing record set.</span></span>
3.  <span data-ttu-id="9c452-128">Probeert u een record te maken in de apex (het hoofdniveau) van de DNS-zone?</span><span class="sxs-lookup"><span data-stu-id="9c452-128">Are you trying to create a record at the DNS zone apex (the ‘root’ of the zone)?</span></span> <span data-ttu-id="9c452-129">Dan is het de DNS-conventie om het @-teken te gebruiken als recordnaam.</span><span class="sxs-lookup"><span data-stu-id="9c452-129">If so, the DNS convention is to use the ‘@’ character as the record name.</span></span> <span data-ttu-id="9c452-130">De DNS-standaarden staan CNAME-records in de apex van de zone niet toe.</span><span class="sxs-lookup"><span data-stu-id="9c452-130">Also note that the DNS standards do not permit CNAME records at the zone apex.</span></span>
4.  <span data-ttu-id="9c452-131">Is er sprake van een CNAME-conflict?</span><span class="sxs-lookup"><span data-stu-id="9c452-131">Do you have a CNAME conflict?</span></span>  <span data-ttu-id="9c452-132">De DNS-standaarden staan niet toe dat een CNAME-record dezelfde naam heeft als een record van een ander type.</span><span class="sxs-lookup"><span data-stu-id="9c452-132">The DNS standards do not allow a CNAME record with the same name as a record of any other type.</span></span> <span data-ttu-id="9c452-133">Als u een bestaande CNAME hebt, kunt u geen record maken met dezelfde naam maar van een ander type.</span><span class="sxs-lookup"><span data-stu-id="9c452-133">If you have an existing CNAME, creating a record with the same name of a different type fails.</span></span>  <span data-ttu-id="9c452-134">Op dezelfde manier kunt u ook geen CNAME maken als de naam overeenkomt met een bestaande record van een ander type.</span><span class="sxs-lookup"><span data-stu-id="9c452-134">Likewise, creating a CNAME fails if the name matches an existing record of a different type.</span></span> <span data-ttu-id="9c452-135">Verhelp het conflict door de andere record te verwijderen of een andere recordnaam te kiezen.</span><span class="sxs-lookup"><span data-stu-id="9c452-135">Remove the conflict by removing the other record or choosing a different record name.</span></span>
5.  <span data-ttu-id="9c452-136">Hebt u de limiet voor het aantal toegestane recordsets in een DNS-zone bereikt?</span><span class="sxs-lookup"><span data-stu-id="9c452-136">Have you reached the limit on the number of record sets permitted in a DNS zone?</span></span> <span data-ttu-id="9c452-137">Het huidige aantal recordsets en het maximumaantal recordsets worden weergegeven in Azure Portal onder de eigenschappen van de zone.</span><span class="sxs-lookup"><span data-stu-id="9c452-137">The current number of record sets and the maximum number of record sets are shown in the Azure portal, under the 'Properties' for the zone.</span></span> <span data-ttu-id="9c452-138">Als u deze limiet hebt bereikt, verwijdert u een aantal recordsets of neemt u contact op met de ondersteuning van Azure om de limiet voor recordsets voor deze zone te laten verhogen. Probeer het vervolgens opnieuw.</span><span class="sxs-lookup"><span data-stu-id="9c452-138">If you have reached this limit, then either delete some record sets or contact Azure Support to raise your record set limit for this zone, then try again.</span></span> 


### <a name="recommended-documents"></a><span data-ttu-id="9c452-139">**Aanbevolen documenten**</span><span class="sxs-lookup"><span data-stu-id="9c452-139">**Recommended documents**</span></span>

<span data-ttu-id="9c452-140">[DNS-zones en -records](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="9c452-140">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="9c452-141">
[Een DNS-zone maken](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="9c452-141">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>



## <a name="i-cant-resolve-my-dns-record"></a><span data-ttu-id="9c452-142">Ik kan mijn DNS-record niet omzetten</span><span class="sxs-lookup"><span data-stu-id="9c452-142">I can't resolve my DNS record</span></span>

<span data-ttu-id="9c452-143">De DNS-naamomzetting vereist meerdere stappen en kan om verschillende redenen mislukken.</span><span class="sxs-lookup"><span data-stu-id="9c452-143">DNS name resolution is a multi-step process, which can fail for many reasons.</span></span> <span data-ttu-id="9c452-144">Aan de hand van de volgende stappen kunt u onderzoeken waarom de DNS-omzetting mislukt voor een DNS-record in een zone in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="9c452-144">The following steps help you investigate why DNS resolution is failing for a DNS record in a zone hosted in Azure DNS.</span></span>

1.  <span data-ttu-id="9c452-145">Controleer of de DNS-records correct zijn geconfigureerd in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="9c452-145">Confirm that the DNS records have been configured correctly in Azure DNS.</span></span> <span data-ttu-id="9c452-146">Controleer of de zonenaam, de naam en het type van de DNS-records in Azure Portal correct zijn.</span><span class="sxs-lookup"><span data-stu-id="9c452-146">Review the DNS records in the Azure portal, checking that the zone name, record name, and record type are correct.</span></span>
2.  <span data-ttu-id="9c452-147">Controleer of de DNS-records correct zijn omgezet in de Azure DNS-naamservers.</span><span class="sxs-lookup"><span data-stu-id="9c452-147">Confirm that the DNS records resolve correctly on the Azure DNS name servers.</span></span>
    - <span data-ttu-id="9c452-148">Als u DNS-query's maakt op uw lokale pc, tonen de resultaten in de cache mogelijk niet de huidige status van de naamservers.</span><span class="sxs-lookup"><span data-stu-id="9c452-148">If you make DNS queries from your local PC, you may see cached results that don’t reflect the current state of the name servers.</span></span>  <span data-ttu-id="9c452-149">Daarnaast maken bedrijfsnetwerken vaak gebruik van DNS-proxyservers, waardoor DNS-query's niet worden doorgestuurd naar specifieke naamservers.</span><span class="sxs-lookup"><span data-stu-id="9c452-149">Also, corporate networks often use DNS proxy servers, which prevent DNS queries from being directed to specific name servers.</span></span>  <span data-ttu-id="9c452-150">U kunt deze problemen voorkomen door een webservice voor naamomzetting te gebruiken, zoals [digwebinterface](http://digwebinterface.com).</span><span class="sxs-lookup"><span data-stu-id="9c452-150">To avoid these problems, use a web-based name resolution service such as [digwebinterface](http://digwebinterface.com).</span></span>
    - <span data-ttu-id="9c452-151">Zorg er wel voor dat u de juiste naamservers voor uw DNS-zone opgeeft, zoals weergegeven in Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9c452-151">Be sure to specify the correct name servers for your DNS zone, as shown in the Azure portal.</span></span>
    - <span data-ttu-id="9c452-152">Controleer of de DNS-naam (dit is de volledig gekwalificeerde naam, inclusief de zonenaam) en het recordtype kloppen.</span><span class="sxs-lookup"><span data-stu-id="9c452-152">Check that the DNS name is correct (you have to specify the fully qualified name, including the zone name) and the record type is correct</span></span>
3.  <span data-ttu-id="9c452-153">Controleer of de DNS-domeinnaam juist is [gedelegeerd naar de Azure DNS-naamservers](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="9c452-153">Confirm that the DNS domain name has been correctly [delegated to the Azure DNS name servers](dns-domain-delegation.md).</span></span> <span data-ttu-id="9c452-154">Er zijn [veel websites van derden die de DNS-delegering kunnen valideren](https://www.bing.com/search?q=dns+check+tool).</span><span class="sxs-lookup"><span data-stu-id="9c452-154">There are a [many 3rd-party web sites that offer DNS delegation validation](https://www.bing.com/search?q=dns+check+tool).</span></span> <span data-ttu-id="9c452-155">Dit is een delegeringstest voor de *zone*. Geef dus alleen de naam van de DNS-zone op en niet de volledig gekwalificeerde recordnaam.</span><span class="sxs-lookup"><span data-stu-id="9c452-155">This test is a *zone* delegation test, so you should only enter the DNS zone name and not the fully qualified record name.</span></span>
4.  <span data-ttu-id="9c452-156">Nadat u het bovenstaande hebt voltooid, zou uw DNS-record correct moeten worden omgezet.</span><span class="sxs-lookup"><span data-stu-id="9c452-156">Having completed the above, your DNS record should now resolve correctly.</span></span> <span data-ttu-id="9c452-157">U kunt dit controleren door opnieuw [digwebinterface](http://digwebinterface.com) te gebruiken, maar nu met de standaardinstellingen van de naamserver.</span><span class="sxs-lookup"><span data-stu-id="9c452-157">To verify, you can again use [digwebinterface](http://digwebinterface.com), this time using the default name server settings.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="9c452-158">**Aanbevolen documenten**</span><span class="sxs-lookup"><span data-stu-id="9c452-158">**Recommended documents**</span></span>

[<span data-ttu-id="9c452-159">Een domein delegeren naar Azure DNS</span><span class="sxs-lookup"><span data-stu-id="9c452-159">Delegate a domain to Azure DNS</span></span>](dns-domain-delegation.md)



## <a name="how-do-i-specify-the-service-and-protocol-for-an-srv-record"></a><span data-ttu-id="9c452-160">Hoe geef ik de 'service' en het 'protocol' voor een SRV-record op?</span><span class="sxs-lookup"><span data-stu-id="9c452-160">How do I specify the ‘service’ and ‘protocol’ for an SRV record?</span></span>

<span data-ttu-id="9c452-161">Azure DNS beheert DNS-records als recordsets. Hierin zijn records met dezelfde naam en van hetzelfde type opgenomen.</span><span class="sxs-lookup"><span data-stu-id="9c452-161">Azure DNS manages DNS records as record sets—the collection of records with the same name and the same type.</span></span> <span data-ttu-id="9c452-162">Voor een SRV-recordset moeten de 'service' en het 'protocol' worden opgegeven als onderdeel van de recordsetnaam.</span><span class="sxs-lookup"><span data-stu-id="9c452-162">For an SRV record set, the 'service' and 'protocol' need to be specified as part of the record set name.</span></span> <span data-ttu-id="9c452-163">De andere SRV-parameters ('prioriteit', 'gewicht', 'poort' en 'doel') worden afzonderlijk opgegeven voor elke record in de recordset.</span><span class="sxs-lookup"><span data-stu-id="9c452-163">The other SRV parameters ('priority', 'weight', 'port' and 'target') are specified separately for each record in the record set.</span></span>

<span data-ttu-id="9c452-164">Voorbeeld van SRV-recordnamen (servicenaam 'sip', protocol 'tcp'):</span><span class="sxs-lookup"><span data-stu-id="9c452-164">Example SRV record names (service name 'sip', protocol 'tcp'):</span></span>

- <span data-ttu-id="9c452-165">\_sip.\_tcp (er wordt een record gemaakt in de apex van de zone)</span><span class="sxs-lookup"><span data-stu-id="9c452-165">\_sip.\_tcp (creates a record set at the zone apex)</span></span>
- <span data-ttu-id="9c452-166">\_sip.\_tcp.sipservice (er wordt een recordset gemaakt met de naam 'sipservice')</span><span class="sxs-lookup"><span data-stu-id="9c452-166">\_sip.\_tcp.sipservice (creates a record set named 'sipservice')</span></span>

### <a name="recommended-documents"></a><span data-ttu-id="9c452-167">**Aanbevolen documenten**</span><span class="sxs-lookup"><span data-stu-id="9c452-167">**Recommended documents**</span></span>

<span data-ttu-id="9c452-168">[DNS-zones en -records](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="9c452-168">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="9c452-169">
[DNS-recordsets en -records maken met Azure Portal](dns-getstarted-create-recordset-portal.md)
</span><span class="sxs-lookup"><span data-stu-id="9c452-169">
[Create DNS record sets and records by using the Azure portal](dns-getstarted-create-recordset-portal.md)
</span></span><br><span data-ttu-id="9c452-170">
[SRV-recordtype (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span><span class="sxs-lookup"><span data-stu-id="9c452-170">
[SRV record type (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span></span>


## <a name="next-steps"></a><span data-ttu-id="9c452-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9c452-171">Next steps</span></span>

* <span data-ttu-id="9c452-172">Meer informatie over [Azure DNS-zones en records](dns-zones-records.md)</span><span class="sxs-lookup"><span data-stu-id="9c452-172">Learn about [Azure DNS zones and records](dns-zones-records.md)</span></span>
* <span data-ttu-id="9c452-173">Om te starten met behulp van Azure DNS, informatie over hoe [maken van een DNS-zone](dns-getstarted-create-dnszone-portal.md) en [DNS-records maken](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9c452-173">To start using Azure DNS, learn how to [create a DNS zone](dns-getstarted-create-dnszone-portal.md) and [create DNS records](dns-getstarted-create-recordset-portal.md).</span></span>
* <span data-ttu-id="9c452-174">Voor het migreren van een bestaande DNS-zone meer informatie over hoe [importeren en exporteren van een DNS-zonebestand](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="9c452-174">To migrate an existing DNS zone, learn how to [import and export a DNS zone file](dns-import-export.md).</span></span>

