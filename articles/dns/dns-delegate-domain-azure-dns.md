---
title: aaaDelegate uw domein tooAzure DNS | Microsoft Docs
description: Begrijpen hoe domeindelegering toochange en gebruik Azure DNS name servers tooprovide domeinen te hosten.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: f780bdaa416150e5e3afe6c6845dc75ba54b6203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-a-domain-tooazure-dns"></a><span data-ttu-id="9ce5b-103">Een domein tooAzure DNS overdragen</span><span class="sxs-lookup"><span data-stu-id="9ce5b-103">Delegate a domain tooAzure DNS</span></span>

<span data-ttu-id="9ce5b-104">Azure DNS kunt u een DNS-zone toohost en Hallo DNS-records voor een domein in Azure beheren.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-104">Azure DNS allows you toohost a DNS zone and manage hello DNS records for a domain in Azure.</span></span> <span data-ttu-id="9ce5b-105">Om DNS-query's voor een domein tooreach Azure DNS, Hallo domein toobe heeft gedelegeerd tooAzure DNS van Hallo bovenliggende domein.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-105">In order for DNS queries for a domain tooreach Azure DNS, hello domain has toobe delegated tooAzure DNS from hello parent domain.</span></span> <span data-ttu-id="9ce5b-106">Houd er rekening mee Azure DNS is niet de domeinregistrar Hallo.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-106">Keep in mind Azure DNS is not hello domain registrar.</span></span> <span data-ttu-id="9ce5b-107">Dit artikel wordt uitgelegd hoe toodelegate uw domein tooAzure DNS.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-107">This article explains how toodelegate your domain tooAzure DNS.</span></span>

<span data-ttu-id="9ce5b-108">Voor domeinen die zijn aangeschaft bij een registrar, biedt uw registrar Hallo optie tooset van deze NS-records.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-108">For domains purchased from a registrar, your registrar offers hello option tooset up these NS records.</span></span> <span data-ttu-id="9ce5b-109">U hoeft geen tooown een toocreate domein een DNS-zone met die domeinnaam in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-109">You do not have tooown a domain toocreate a DNS zone with that domain name in Azure DNS.</span></span> <span data-ttu-id="9ce5b-110">U hoeft echter tooown Hallo domein tooset up Hallo delegering tooAzure DNS met Hallo registrar.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-110">However, you do need tooown hello domain tooset up hello delegation tooAzure DNS with hello registrar.</span></span>

<span data-ttu-id="9ce5b-111">Stel dat u koopt Hallo domein 'contoso.net' en een zone met contoso.net' hello name' in Azure DNS maakt.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-111">For example, suppose you purchase hello domain 'contoso.net' and create a zone with hello name 'contoso.net' in Azure DNS.</span></span> <span data-ttu-id="9ce5b-112">Als de eigenaar van de Hallo van Hallo domein biedt uw registrar dat u hello optie tooconfigure Hallo serveradressen (dat wil zeggen, Hallo NS-records) voor uw domein.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-112">As hello owner of hello domain, your registrar offers you hello option tooconfigure hello name server addresses (that is, hello NS records) for your domain.</span></span> <span data-ttu-id="9ce5b-113">Hallo registrar slaat deze NS-records in Hallo bovenliggende domein in dit geval '.net'.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-113">hello registrar stores these NS records in hello parent domain, in this case '.net'.</span></span> <span data-ttu-id="9ce5b-114">Vervolgens kunnen clients Hallo wereld gerichte tooyour domein in Azure DNS-zone worden bij het tooresolve DNS-records in 'contoso.net'.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-114">Clients around hello world can then be directed tooyour domain in Azure DNS zone when trying tooresolve DNS records in 'contoso.net'.</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="9ce5b-115">Een DNS-zone maken</span><span class="sxs-lookup"><span data-stu-id="9ce5b-115">Create a DNS zone</span></span>

1. <span data-ttu-id="9ce5b-116">Meld u aan toohello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="9ce5b-116">Sign in toohello Azure portal</span></span>
1. <span data-ttu-id="9ce5b-117">Klik op Hallo Hub-menu en klik op **Nieuw > netwerken >** en klik vervolgens op **DNS-zone** tooopen Hallo maken DNS-zone blade.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-117">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![DNS-zone](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="9ce5b-119">Op Hallo **maken DNS-zone** blade Voer Hallo volgende waarden en klik vervolgens op **maken**:</span><span class="sxs-lookup"><span data-stu-id="9ce5b-119">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>

   | <span data-ttu-id="9ce5b-120">**Instelling**</span><span class="sxs-lookup"><span data-stu-id="9ce5b-120">**Setting**</span></span> | <span data-ttu-id="9ce5b-121">**Waarde**</span><span class="sxs-lookup"><span data-stu-id="9ce5b-121">**Value**</span></span> | <span data-ttu-id="9ce5b-122">**Details**</span><span class="sxs-lookup"><span data-stu-id="9ce5b-122">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="9ce5b-123">**Naam**</span><span class="sxs-lookup"><span data-stu-id="9ce5b-123">**Name**</span></span>|<span data-ttu-id="9ce5b-124">contoso.net</span><span class="sxs-lookup"><span data-stu-id="9ce5b-124">contoso.net</span></span>|<span data-ttu-id="9ce5b-125">Hallo-naam van Hallo DNS-zone</span><span class="sxs-lookup"><span data-stu-id="9ce5b-125">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="9ce5b-126">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="9ce5b-126">**Subscription**</span></span>|<span data-ttu-id="9ce5b-127">[Uw abonnement]</span><span class="sxs-lookup"><span data-stu-id="9ce5b-127">[Your subscription]</span></span>|<span data-ttu-id="9ce5b-128">Selecteer een abonnement toocreate Hallo toepassingsgateway in.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-128">Select a subscription toocreate hello application gateway in.</span></span>|
   |<span data-ttu-id="9ce5b-129">**Resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="9ce5b-129">**Resource group**</span></span>|<span data-ttu-id="9ce5b-130">**Nieuwe maken:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="9ce5b-130">**Create new:** contosoRG</span></span>|<span data-ttu-id="9ce5b-131">Maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-131">Create a resource group.</span></span> <span data-ttu-id="9ce5b-132">de naam van resourcegroep Hallo moet uniek zijn binnen het Hallo-abonnement die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-132">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="9ce5b-133">meer informatie over resourcegroepen lezen Hallo toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overzichtsartikel.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-133">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="9ce5b-134">**Locatie**</span><span class="sxs-lookup"><span data-stu-id="9ce5b-134">**Location**</span></span>|<span data-ttu-id="9ce5b-135">VS - west</span><span class="sxs-lookup"><span data-stu-id="9ce5b-135">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="9ce5b-136">Hallo resourcegroep toohello locatie van resourcegroep Hallo verwijst, en heeft geen invloed op Hallo DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-136">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="9ce5b-137">Hallo DNS-zone locatie is altijd 'global' en niet wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-137">hello DNS zone location is always "global", and is not shown.</span></span>

## <a name="retrieve-name-servers"></a><span data-ttu-id="9ce5b-138">Naamservers ophalen</span><span class="sxs-lookup"><span data-stu-id="9ce5b-138">Retrieve name servers</span></span>

<span data-ttu-id="9ce5b-139">Voordat u uw DNS-zone tooAzure DNS delegeren kunt, moet u eerst tooknow Hallo servernamen voor uw zone.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-139">Before you can delegate your DNS zone tooAzure DNS, you first need tooknow hello name server names for your zone.</span></span> <span data-ttu-id="9ce5b-140">Telkens wanneer er een zone wordt gemaakt, wijst Azure DNS naamservers uit een groep toe.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-140">Azure DNS allocates name servers from a pool each time a zone is created.</span></span>

1. <span data-ttu-id="9ce5b-141">Met de Hallo DNS-zone in hello Azure-portal gemaakt **Favorieten** deelvenster, klikt u op **alle resources**.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-141">With hello DNS zone created, in hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="9ce5b-142">Klik op Hallo **contoso.net** DNS-zone in Hallo **alle resources** blade.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-142">Click hello **contoso.net** DNS zone in hello **All resources** blade.</span></span> <span data-ttu-id="9ce5b-143">Als u hebt geselecteerd al Hallo-abonnement verschillende resources heeft, kunt u **contoso.net** in Hallo Filter met de naam...</span><span class="sxs-lookup"><span data-stu-id="9ce5b-143">If hello subscription you selected already has several resources in it, you can enter **contoso.net** in hello Filter by name…</span></span> <span data-ttu-id="9ce5b-144">vak tooeasily toegang Hallo toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-144">box tooeasily access hello application gateway.</span></span> 

1. <span data-ttu-id="9ce5b-145">Hallo-naamservers ophalen met Hallo DNS-zone-blade.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-145">Retrieve hello name servers from hello DNS zone blade.</span></span> <span data-ttu-id="9ce5b-146">In dit voorbeeld Hallo zone 'contoso.net' is toegewezen naamservers ' ns1-01.azure-dns.com', 'ns2-01.', ' ns3-01.azure-Azure ', en ' ns4-01.azure-dns.info':</span><span class="sxs-lookup"><span data-stu-id="9ce5b-146">In this example, hello zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![DNS-naamserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="9ce5b-148">Azure DNS maakt automatisch gezaghebbende NS-records in uw zone die Hallo toegewezen naamservers.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-148">Azure DNS automatically creates authoritative NS records in your zone containing hello assigned name servers.</span></span>  <span data-ttu-id="9ce5b-149">de namen van toosee Hallo naamserver via Azure PowerShell of Azure CLI, hoeft u alleen tooretrieve deze records.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-149">toosee hello name server names via Azure PowerShell or Azure CLI, you simply need tooretrieve these records.</span></span>

<span data-ttu-id="9ce5b-150">Hallo bieden volgende voorbeelden ook Hallo stappen tooretrieve Hallo-naamservers voor een zone in Azure DNS met PowerShell en Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-150">hello following examples also provide hello steps tooretrieve hello name servers for a zone in Azure DNS with PowerShell and Azure CLI.</span></span>

### <a name="powershell"></a><span data-ttu-id="9ce5b-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9ce5b-151">PowerShell</span></span>

```powershell
# hello record name "@" is used toorefer toorecords at hello top of hello zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

<span data-ttu-id="9ce5b-152">Hallo volgende voorbeeld is Hallo antwoord.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-152">hello following example is hello response.</span></span>

```
Name              : @
ZoneName          : contoso.net
ResourceGroupName : contosorg
Ttl               : 172800
Etag              : 03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5
RecordType        : NS
Records           : {ns1-07.azure-dns.com., ns2-07.azure-dns.net., ns3-07.azure-dns.org.,
                    ns4-07.azure-dns.info.}
Metadata          :
```

### <a name="azure-cli"></a><span data-ttu-id="9ce5b-153">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9ce5b-153">Azure CLI</span></span>

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

<span data-ttu-id="9ce5b-154">Hallo volgende voorbeeld is Hallo antwoord.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-154">hello following example is hello response.</span></span>

```json
{
  "etag": "03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosoRG/providers/Microsoft.Network/dnszones/contoso.net/NS/@",
  "metadata": null,
  "name": "@",
  "nsRecords": [
    {
      "nsdname": "ns1-07.azure-dns.com."
    },
    {
      "nsdname": "ns2-07.azure-dns.net."
    },
    {
      "nsdname": "ns3-07.azure-dns.org."
    },
    {
      "nsdname": "ns4-07.azure-dns.info."
    }
  ],
  "resourceGroup": "contosoRG",
  "ttl": 172800,
  "type": "Microsoft.Network/dnszones/NS"
}
```

## <a name="delegate-hello-domain"></a><span data-ttu-id="9ce5b-155">Gemachtigde Hallo domein</span><span class="sxs-lookup"><span data-stu-id="9ce5b-155">Delegate hello domain</span></span>

<span data-ttu-id="9ce5b-156">Nu dat Hallo DNS-zone wordt gemaakt en u de naamservers Hallo hebt, moet Hallo bovenliggend domein toobe bijgewerkt met hello Azure DNS-naamservers.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-156">Now that hello DNS zone is created and you have hello name servers, hello parent domain needs toobe updated with hello Azure DNS name servers.</span></span> <span data-ttu-id="9ce5b-157">Elke registrar heeft eigen DNS-beheer extra toochange hello naamserverrecords voor een domein.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-157">Each registrar has their own DNS management tools toochange hello name server records for a domain.</span></span> <span data-ttu-id="9ce5b-158">Van Hallo registrar DNS-beheer pagina bewerken Hallo NS-records en vervang Hallo NS-records door Hallo die zijn gemaakt voor Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-158">In hello registrar's DNS management page, edit hello NS records and replace hello NS records with hello ones Azure DNS created.</span></span>

<span data-ttu-id="9ce5b-159">Wanneer u een domein tooAzure DNS, moet u Hallo naamservernamen verstrekt door Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-159">When delegating a domain tooAzure DNS, you must use hello name server names provided by Azure DNS.</span></span> <span data-ttu-id="9ce5b-160">Het verdient aanbeveling toouse alle vier naam servernamen, ongeacht het Hallo-naam van uw domein.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-160">It is recommended toouse all four name server names, regardless of hello name of your domain.</span></span> <span data-ttu-id="9ce5b-161">Domeindelegering vereist geen Hallo naam server name toouse Hallo van hetzelfde domein bevinden op het hoogste niveau als uw domein.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-161">Domain delegation does not require hello name server name toouse hello same top-level domain as your domain.</span></span>

<span data-ttu-id="9ce5b-162">Gebruik niet 'glue records' toopoint toohello Azure DNS-naam server IP-adressen, aangezien deze IP-adressen in de toekomst kunnen worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-162">You should not use 'glue records' toopoint toohello Azure DNS name server IP addresses, since these IP addresses may change in future.</span></span> <span data-ttu-id="9ce5b-163">Delegeringen die gebruikmaken van de naamservernamen in uw eigen zone, ook wel vanity naamservers genoemd, worden momenteel niet ondersteund in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-163">Delegations using name server names in your own zone, sometimes called 'vanity name servers', are not currently supported in Azure DNS.</span></span>

## <a name="verify-name-resolution-is-working"></a><span data-ttu-id="9ce5b-164">Controleren of de naamomzetting werkt</span><span class="sxs-lookup"><span data-stu-id="9ce5b-164">Verify name resolution is working</span></span>

<span data-ttu-id="9ce5b-165">Na het voltooien van Hallo overdracht, kunt u controleren of naamomzetting werkt met behulp van een hulpprogramma zoals 'nslookup' tooquery Hallo SOA-record voor uw zone (die ook automatisch wordt gemaakt wanneer Hallo zone wordt gemaakt).</span><span class="sxs-lookup"><span data-stu-id="9ce5b-165">After completing hello delegation, you can verify that name resolution is working by using a tool such as 'nslookup' tooquery hello SOA record for your zone (which is also automatically created when hello zone is created).</span></span>

<span data-ttu-id="9ce5b-166">U hebt geen toospecify hello Azure DNS-naamservers, als Hallo overdracht is ingesteld correct Hallo normale DNS-omzettingsproces vindt de naamservers Hallo automatisch.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-166">You do not have toospecify hello Azure DNS name servers, if hello delegation has been set up correctly, hello normal DNS resolution process finds hello name servers automatically.</span></span>

```
nslookup -type=SOA contoso.com
```

<span data-ttu-id="9ce5b-167">Hallo Hier volgt een voorbeeld van antwoord van de voorgaande opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="9ce5b-167">hello following is an example response from hello preceding command:</span></span>

```
Server: ns1-04.azure-dns.com
Address: 208.76.47.4

contoso.com
primary name server = ns1-04.azure-dns.com
responsible mail addr = msnhst.microsoft.com
serial = 1
refresh = 900 (15 mins)
retry = 300 (5 mins)
expire = 604800 (7 days)
default TTL = 300 (5 mins)
```

## <a name="delegate-sub-domains-in-azure-dns"></a><span data-ttu-id="9ce5b-168">Subdomeinen delegeren in Azure DNS</span><span class="sxs-lookup"><span data-stu-id="9ce5b-168">Delegate sub-domains in Azure DNS</span></span>

<span data-ttu-id="9ce5b-169">Als u tooset van een afzonderlijke onderliggende zone wilt, kunt u een subdomein in Azure DNS kunt delegeren.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-169">If you want tooset up a separate child zone, you can delegate a sub-domain in Azure DNS.</span></span> <span data-ttu-id="9ce5b-170">Stel dat u wilt dat tooset van een afzonderlijke onderliggende zone, bijvoorbeeld hebt ingesteld en gedelegeerd 'contoso.net' in Azure DNS 'partners.contoso.net'.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-170">For example, having set up and delegated 'contoso.net' in Azure DNS, suppose you would like tooset up a separate child zone, 'partners.contoso.net'.</span></span>

1. <span data-ttu-id="9ce5b-171">Maak partners.contoso.net' hello onderliggende zone, in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-171">Create hello child zone 'partners.contoso.net' in Azure DNS.</span></span>
2. <span data-ttu-id="9ce5b-172">Hallo gezaghebbende NS-records in Hallo onderliggende zone tooobtain Hallo naamservers Hallo onderliggende zone in Azure DNS hosten opzoeken.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-172">Look up hello authoritative NS records in hello child zone tooobtain hello name servers hosting hello child zone in Azure DNS.</span></span>
3. <span data-ttu-id="9ce5b-173">Hallo onderliggende zone door NS-records configureren in Hallo bovenliggende zone en wijst toohello onderliggende zone delegeren.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-173">Delegate hello child zone by configuring NS records in hello parent zone pointing toohello child zone.</span></span>

### <a name="create-a-dns-zone"></a><span data-ttu-id="9ce5b-174">Een DNS-zone maken</span><span class="sxs-lookup"><span data-stu-id="9ce5b-174">Create a DNS zone</span></span>

1. <span data-ttu-id="9ce5b-175">Meld u aan toohello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="9ce5b-175">Sign in toohello Azure portal</span></span>
1. <span data-ttu-id="9ce5b-176">Klik op Hallo Hub-menu en klik op **Nieuw > netwerken >** en klik vervolgens op **DNS-zone** tooopen Hallo maken DNS-zone blade.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-176">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![DNS-zone](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="9ce5b-178">Op Hallo **maken DNS-zone** blade Voer Hallo volgende waarden en klik vervolgens op **maken**:</span><span class="sxs-lookup"><span data-stu-id="9ce5b-178">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>

   | <span data-ttu-id="9ce5b-179">**Instelling**</span><span class="sxs-lookup"><span data-stu-id="9ce5b-179">**Setting**</span></span> | <span data-ttu-id="9ce5b-180">**Waarde**</span><span class="sxs-lookup"><span data-stu-id="9ce5b-180">**Value**</span></span> | <span data-ttu-id="9ce5b-181">**Details**</span><span class="sxs-lookup"><span data-stu-id="9ce5b-181">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="9ce5b-182">**Naam**</span><span class="sxs-lookup"><span data-stu-id="9ce5b-182">**Name**</span></span>|<span data-ttu-id="9ce5b-183">partners.contoso.net</span><span class="sxs-lookup"><span data-stu-id="9ce5b-183">partners.contoso.net</span></span>|<span data-ttu-id="9ce5b-184">Hallo-naam van Hallo DNS-zone</span><span class="sxs-lookup"><span data-stu-id="9ce5b-184">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="9ce5b-185">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="9ce5b-185">**Subscription**</span></span>|<span data-ttu-id="9ce5b-186">[Uw abonnement]</span><span class="sxs-lookup"><span data-stu-id="9ce5b-186">[Your subscription]</span></span>|<span data-ttu-id="9ce5b-187">Selecteer een abonnement toocreate Hallo toepassingsgateway in.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-187">Select a subscription toocreate hello application gateway in.</span></span>|
   |<span data-ttu-id="9ce5b-188">**Resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="9ce5b-188">**Resource group**</span></span>|<span data-ttu-id="9ce5b-189">**Bestaande gebruiken:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="9ce5b-189">**Use Existing:** contosoRG</span></span>|<span data-ttu-id="9ce5b-190">Maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-190">Create a resource group.</span></span> <span data-ttu-id="9ce5b-191">de naam van resourcegroep Hallo moet uniek zijn binnen het Hallo-abonnement die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-191">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="9ce5b-192">meer informatie over resourcegroepen lezen Hallo toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overzichtsartikel.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-192">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="9ce5b-193">**Locatie**</span><span class="sxs-lookup"><span data-stu-id="9ce5b-193">**Location**</span></span>|<span data-ttu-id="9ce5b-194">VS - west</span><span class="sxs-lookup"><span data-stu-id="9ce5b-194">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="9ce5b-195">Hallo resourcegroep toohello locatie van resourcegroep Hallo verwijst, en heeft geen invloed op Hallo DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-195">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="9ce5b-196">Hallo DNS-zone locatie is altijd 'global' en niet wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-196">hello DNS zone location is always "global", and is not shown.</span></span>

### <a name="retrieve-name-servers"></a><span data-ttu-id="9ce5b-197">Naamservers ophalen</span><span class="sxs-lookup"><span data-stu-id="9ce5b-197">Retrieve name servers</span></span>

1. <span data-ttu-id="9ce5b-198">Met de Hallo DNS-zone in hello Azure-portal gemaakt **Favorieten** deelvenster, klikt u op **alle resources**.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-198">With hello DNS zone created, in hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="9ce5b-199">Klik op Hallo **partners.contoso.net** DNS-zone in Hallo **alle resources** blade.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-199">Click hello **partners.contoso.net** DNS zone in hello **All resources** blade.</span></span> <span data-ttu-id="9ce5b-200">Als u hebt geselecteerd al Hallo-abonnement verschillende resources heeft, kunt u **partners.contoso.net** in Hallo Filter met de naam...</span><span class="sxs-lookup"><span data-stu-id="9ce5b-200">If hello subscription you selected already has several resources in it, you can enter **partners.contoso.net** in hello Filter by name…</span></span> <span data-ttu-id="9ce5b-201">vak tooeasily toegang Hallo DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-201">box tooeasily access hello DNS zone.</span></span>

1. <span data-ttu-id="9ce5b-202">Hallo-naamservers ophalen met Hallo DNS-zone-blade.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-202">Retrieve hello name servers from hello DNS zone blade.</span></span> <span data-ttu-id="9ce5b-203">In dit voorbeeld Hallo zone 'contoso.net' is toegewezen naamservers ' ns1-01.azure-dns.com', 'ns2-01.', ' ns3-01.azure-Azure ', en ' ns4-01.azure-dns.info':</span><span class="sxs-lookup"><span data-stu-id="9ce5b-203">In this example, hello zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![DNS-naamserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="9ce5b-205">Azure DNS maakt automatisch gezaghebbende NS-records in uw zone die Hallo toegewezen naamservers.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-205">Azure DNS automatically creates authoritative NS records in your zone containing hello assigned name servers.</span></span>  <span data-ttu-id="9ce5b-206">de namen van toosee Hallo naamserver via Azure PowerShell of Azure CLI, hoeft u alleen tooretrieve deze records.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-206">toosee hello name server names via Azure PowerShell or Azure CLI, you simply need tooretrieve these records.</span></span>

### <a name="create-name-server-record-in-parent-zone"></a><span data-ttu-id="9ce5b-207">Een naamserverrecord maken in de bovenliggende zone</span><span class="sxs-lookup"><span data-stu-id="9ce5b-207">Create name server record in parent zone</span></span>

1. <span data-ttu-id="9ce5b-208">Navigeer toohello **contoso.net** DNS-zone in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-208">Navigate toohello **contoso.net** DNS zone in hello Azure portal.</span></span>
1. <span data-ttu-id="9ce5b-209">Klik op **Recordset toevoegen**</span><span class="sxs-lookup"><span data-stu-id="9ce5b-209">Click **+ Record set**</span></span>
1. <span data-ttu-id="9ce5b-210">Op Hallo **recordset toevoegen** blade Voer Hallo volgende waarden en klik vervolgens op **OK**:</span><span class="sxs-lookup"><span data-stu-id="9ce5b-210">On hello **Add record set** blade, enter hello following values, then click **OK**:</span></span>

   | <span data-ttu-id="9ce5b-211">**Instelling**</span><span class="sxs-lookup"><span data-stu-id="9ce5b-211">**Setting**</span></span> | <span data-ttu-id="9ce5b-212">**Waarde**</span><span class="sxs-lookup"><span data-stu-id="9ce5b-212">**Value**</span></span> | <span data-ttu-id="9ce5b-213">**Details**</span><span class="sxs-lookup"><span data-stu-id="9ce5b-213">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="9ce5b-214">**Naam**</span><span class="sxs-lookup"><span data-stu-id="9ce5b-214">**Name**</span></span>|<span data-ttu-id="9ce5b-215">partners</span><span class="sxs-lookup"><span data-stu-id="9ce5b-215">partners</span></span>|<span data-ttu-id="9ce5b-216">Hallo-naam van Hallo onderliggende DNS-zone</span><span class="sxs-lookup"><span data-stu-id="9ce5b-216">hello name of hello child DNS zone</span></span>|
   |<span data-ttu-id="9ce5b-217">**Type**</span><span class="sxs-lookup"><span data-stu-id="9ce5b-217">**Type**</span></span>|<span data-ttu-id="9ce5b-218">NS</span><span class="sxs-lookup"><span data-stu-id="9ce5b-218">NS</span></span>|<span data-ttu-id="9ce5b-219">Gebruik NS voor naamserverrecords.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-219">Use NS for name server records.</span></span>|
   |<span data-ttu-id="9ce5b-220">**TTL**</span><span class="sxs-lookup"><span data-stu-id="9ce5b-220">**TTL**</span></span>|<span data-ttu-id="9ce5b-221">1</span><span class="sxs-lookup"><span data-stu-id="9ce5b-221">1</span></span>|<span data-ttu-id="9ce5b-222">Tijd toolive.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-222">Time toolive.</span></span>|
   |<span data-ttu-id="9ce5b-223">**TTL-eenheid**</span><span class="sxs-lookup"><span data-stu-id="9ce5b-223">**TTL unit**</span></span>|<span data-ttu-id="9ce5b-224">Uren</span><span class="sxs-lookup"><span data-stu-id="9ce5b-224">Hours</span></span>|<span data-ttu-id="9ce5b-225">Hiermee stelt u tijd toolive eenheid toohours</span><span class="sxs-lookup"><span data-stu-id="9ce5b-225">sets time toolive unit toohours</span></span>|
   |<span data-ttu-id="9ce5b-226">**NAAMSERVER**</span><span class="sxs-lookup"><span data-stu-id="9ce5b-226">**NAME SERVER**</span></span>|<span data-ttu-id="9ce5b-227">{naamservers van zone partners.contoso.net}</span><span class="sxs-lookup"><span data-stu-id="9ce5b-227">{name servers from partners.contoso.net zone}</span></span>|<span data-ttu-id="9ce5b-228">Voer alle 4 Hallo naamservers uit partners.contoso.net zone.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-228">Enter all 4 of hello name servers from partners.contoso.net zone.</span></span> |

   ![DNS-naamserver](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a><span data-ttu-id="9ce5b-230">Subdomeinen in Azure DNS delegeren met andere hulpprogramma’s</span><span class="sxs-lookup"><span data-stu-id="9ce5b-230">Delegating sub-domains in Azure DNS with other tools</span></span>

<span data-ttu-id="9ce5b-231">Hallo bieden volgende voorbeelden Hallo stappen toodelegate subdomeinen in Azure DNS met PowerShell en CLI:</span><span class="sxs-lookup"><span data-stu-id="9ce5b-231">hello following examples provide hello steps toodelegate sub-domains in Azure DNS with PowerShell and CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="9ce5b-232">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9ce5b-232">PowerShell</span></span>

<span data-ttu-id="9ce5b-233">Hallo volgende PowerShell-voorbeeld laat zien hoe dit werkt.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-233">hello following PowerShell example demonstrates how this works.</span></span> <span data-ttu-id="9ce5b-234">Hallo dezelfde stappen kunnen worden uitgevoerd via hello Azure-portal of via Hallo platformoverschrijdende Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-234">hello same steps can be executed via hello Azure portal, or via hello cross-platform Azure CLI.</span></span>

```powershell
# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
$parent = New-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
$child = New-AzureRmDnsZone -Name partners.contoso.net -ResourceGroupName contosoRG

# Retrieve hello authoritative NS records from hello child zone as shown in hello next example. This contains hello name servers assigned toohello child zone.
$child_ns_recordset = Get-AzureRmDnsRecordSet -Zone $child -Name "@" -RecordType NS

# Create hello corresponding NS record set in hello parent zone toocomplete hello delegation. hello record set name in hello parent zone matches hello child zone name, in this case "partners".
$parent_ns_recordset = New-AzureRmDnsRecordSet -Zone $parent -Name "partners" -RecordType NS -Ttl 3600
$parent_ns_recordset.Records = $child_ns_recordset.Records
Set-AzureRmDnsRecordSet -RecordSet $parent_ns_recordset
```

<span data-ttu-id="9ce5b-235">Gebruik `nslookup` tooverify dat alles juist is ingesteld door het opzoeken van Hallo SOA-record van Hallo onderliggende zone.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-235">Use `nslookup` tooverify that everything is set up correctly by looking up hello SOA record of hello child zone.</span></span>

```
nslookup -type=SOA partners.contoso.com
```

```
Server: ns1-08.azure-dns.com
Address: 208.76.47.8

partners.contoso.com
    primary name server = ns1-08.azure-dns.com
    responsible mail addr = msnhst.microsoft.com
    serial = 1
    refresh = 900 (15 mins)
    retry = 300 (5 mins)
    expire = 604800 (7 days)
    default TTL = 300 (5 mins)
```

#### <a name="azure-cli"></a><span data-ttu-id="9ce5b-236">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9ce5b-236">Azure CLI</span></span>

```azurecli
#!/bin/bash

# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

<span data-ttu-id="9ce5b-237">Ophalen van de naamservers Hallo voor Hallo `partners.contoso.net` zone uit Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-237">Retrieve hello name servers for hello `partners.contoso.net` zone from hello output.</span></span>

```
{
  "etag": "00000003-0000-0000-418f-250de2b2d201",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosorg/providers/Microsoft.Network/dnszones/partners.contoso.net",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "partners.contoso.net",
  "nameServers": [
    "ns1-09.azure-dns.com.",
    "ns2-09.azure-dns.net.",
    "ns3-09.azure-dns.org.",
    "ns4-09.azure-dns.info."
  ],
  "numberOfRecordSets": 2,
  "resourceGroup": "contosorg",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="9ce5b-238">Hallo-Recordset en NS-records voor elke naamserver maken.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-238">Create hello record set and NS records for each name server.</span></span>

```azurecli
#!/bin/bash

# Create hello record set
az network dns record-set ns create --resource-group contosorg --zone-name contoso.net --name partners

# Create a ns record for each name server.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns1-09.azure-dns.com.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns2-09.azure-dns.net.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns3-09.azure-dns.org.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns4-09.azure-dns.info.
```

## <a name="delete-all-resources"></a><span data-ttu-id="9ce5b-239">Alle resources verwijderen</span><span class="sxs-lookup"><span data-stu-id="9ce5b-239">Delete all resources</span></span>

<span data-ttu-id="9ce5b-240">toodelete alle resources die worden gemaakt in dit artikel wordt voltooid Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="9ce5b-240">toodelete all resources created in this article, complete hello following steps:</span></span>

1. <span data-ttu-id="9ce5b-241">In de Azure-portal Hallo **Favorieten** deelvenster, klikt u op **alle resources**.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-241">In hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="9ce5b-242">Klik op Hallo **contosorg** resourcegroep in Hallo alle resources blade.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-242">Click hello **contosorg** resource group in hello All resources blade.</span></span> <span data-ttu-id="9ce5b-243">Als u hebt geselecteerd al Hallo-abonnement verschillende resources heeft, kunt u **contosorg** in Hallo **filteren op naam...**</span><span class="sxs-lookup"><span data-stu-id="9ce5b-243">If hello subscription you selected already has several resources in it, you can enter **contosorg** in hello **Filter by name…**</span></span> <span data-ttu-id="9ce5b-244">vak tooeasily toegang Hallo resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-244">box tooeasily access hello resource group.</span></span>
1. <span data-ttu-id="9ce5b-245">In Hallo **contosorg** blade, klikt u op Hallo **verwijderen** knop.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-245">In hello **contosorg** blade, click hello **Delete** button.</span></span>
1. <span data-ttu-id="9ce5b-246">Hallo portal, moet u tootype Hallo-naam van Hallo resource groep tooconfirm dat u wilt dat toodelete deze.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-246">hello portal requires you tootype hello name of hello resource group tooconfirm that you want toodelete it.</span></span> <span data-ttu-id="9ce5b-247">Type *contosorg* hello Resourcegroepnaam, vervolgens klikt u op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-247">Type *contosorg* for hello resource group name, then click **Delete**.</span></span> <span data-ttu-id="9ce5b-248">Een resourcegroep verwijdert, worden alle bronnen binnen de resourcegroep hello, dus altijd zeker tooconfirm Hallo inhoud van een resourcegroep voordat u het verwijdert.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-248">Deleting a resource group deletes all resources within hello resource group, so always be sure tooconfirm hello contents of a resource group before deleting it.</span></span> <span data-ttu-id="9ce5b-249">Hallo portal Hiermee verwijdert u alle resources binnen de resourcegroep Hallo vervolgens Hallo resourcegroep zelf verwijdert.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-249">hello portal deletes all resources contained within hello resource group, then deletes hello resource group itself.</span></span> <span data-ttu-id="9ce5b-250">Dit proces duurt enkele minuten.</span><span class="sxs-lookup"><span data-stu-id="9ce5b-250">This process takes several minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ce5b-251">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9ce5b-251">Next steps</span></span>

[<span data-ttu-id="9ce5b-252">DNS-zones beheren</span><span class="sxs-lookup"><span data-stu-id="9ce5b-252">Manage DNS zones</span></span>](dns-operations-dnszones.md)

[<span data-ttu-id="9ce5b-253">DNS-records beheren</span><span class="sxs-lookup"><span data-stu-id="9ce5b-253">Manage DNS records</span></span>](dns-operations-recordsets.md)
