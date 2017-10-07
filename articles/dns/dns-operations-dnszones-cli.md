---
title: aaaManage DNS-zones in Azure DNS - Azure CLI 2.0 | Microsoft Docs
description: U kunt DNS-zones met Azure CLI 2.0 beheren. Dit artikel laat zien hoe tooupdate, verwijderen en DNS-zones maken op Azure DNS.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: gwallace
ms.openlocfilehash: 3945a558b2db3490e50678d8395a47e55a85c8fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-20"></a><span data-ttu-id="f5b00-104">Hoe toomanage DNS-Zones in Azure DNS met behulp van Azure CLI 2.0 Hallo</span><span class="sxs-lookup"><span data-stu-id="f5b00-104">How toomanage DNS Zones in Azure DNS using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f5b00-105">Portal</span><span class="sxs-lookup"><span data-stu-id="f5b00-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="f5b00-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5b00-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="f5b00-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f5b00-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="f5b00-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f5b00-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)


<span data-ttu-id="f5b00-109">Deze handleiding wordt getoond hoe toomanage uw DNS-zones met behulp van Hallo platformoverschrijdende CLI van Azure, die beschikbaar is voor Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="f5b00-109">This guide shows how toomanage your DNS zones by using hello cross-platform Azure CLI, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="f5b00-110">U kunt ook beheren met behulp van DNS-zones [Azure PowerShell](dns-operations-dnszones.md) of hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f5b00-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or hello Azure portal.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="f5b00-111">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="f5b00-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="f5b00-112">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f5b00-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="f5b00-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -onze CLI voor Hallo klassieke en resource management implementatiemodellen.</span><span class="sxs-lookup"><span data-stu-id="f5b00-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="f5b00-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="f5b00-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="f5b00-115">Inleiding</span><span class="sxs-lookup"><span data-stu-id="f5b00-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a><span data-ttu-id="f5b00-116">Azure CLI 2.0 instellen voor Azure DNS</span><span class="sxs-lookup"><span data-stu-id="f5b00-116">Set up Azure CLI 2.0 for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="f5b00-117">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="f5b00-117">Before you begin</span></span>

<span data-ttu-id="f5b00-118">Controleer of u Hallo volgende items voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="f5b00-118">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="f5b00-119">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f5b00-119">An Azure subscription.</span></span> <span data-ttu-id="f5b00-120">Als u nog geen Azure-abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of [u aanmelden voor een gratis account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f5b00-120">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="f5b00-121">Installeer de nieuwste versie Hallo van hello Azure CLI 2.0, die beschikbaar zijn voor Windows, Linux of MAC.</span><span class="sxs-lookup"><span data-stu-id="f5b00-121">Install hello latest version of hello Azure CLI 2.0, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="f5b00-122">Meer informatie vindt u op [installeren hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="f5b00-122">More information is available at [Install hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="f5b00-123">Meld u aan tooyour Azure-account</span><span class="sxs-lookup"><span data-stu-id="f5b00-123">Sign in tooyour Azure account</span></span>

<span data-ttu-id="f5b00-124">Open een consolevenster en doorloop de verificatie met uw referenties.</span><span class="sxs-lookup"><span data-stu-id="f5b00-124">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="f5b00-125">Zie het logboek voor meer informatie in tooAzure van hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f5b00-125">For more information, see Log in tooAzure from hello Azure CLI</span></span>

```
az login
```

### <a name="select-hello-subscription"></a><span data-ttu-id="f5b00-126">Hallo-abonnement selecteren</span><span class="sxs-lookup"><span data-stu-id="f5b00-126">Select hello subscription</span></span>

<span data-ttu-id="f5b00-127">Controleer de abonnementen Hallo voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="f5b00-127">Check hello subscriptions for hello account.</span></span>

```
az account list
```

<span data-ttu-id="f5b00-128">Kies welke van uw Azure-abonnementen toouse.</span><span class="sxs-lookup"><span data-stu-id="f5b00-128">Choose which of your Azure subscriptions toouse.</span></span>

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="f5b00-129">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="f5b00-129">Create a resource group</span></span>

<span data-ttu-id="f5b00-130">Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f5b00-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="f5b00-131">Dit wordt gebruikt als Hallo standaardlocatie voor resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="f5b00-131">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="f5b00-132">Echter, omdat alle DNS-resources globaal en niet regionaal zijn, heeft Hallo keuze van de locatie voor resourcegroep geen invloed op Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="f5b00-132">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="f5b00-133">U kunt deze stap overslaan als u een bestaande resourcegroep gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f5b00-133">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a><span data-ttu-id="f5b00-134">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="f5b00-134">Getting help</span></span>

<span data-ttu-id="f5b00-135">Alle betreffende tooAzure DNS CLI 2.0-opdrachten starten met `az network dns`.</span><span class="sxs-lookup"><span data-stu-id="f5b00-135">All CLI 2.0 commands relating tooAzure DNS start with `az network dns`.</span></span> <span data-ttu-id="f5b00-136">Help beschikbaar is voor elke opdracht met Hallo `--help` optie (korte versie `-h`).</span><span class="sxs-lookup"><span data-stu-id="f5b00-136">Help is available for each command using hello `--help` option (short form `-h`).</span></span>  <span data-ttu-id="f5b00-137">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f5b00-137">For example:</span></span>

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="f5b00-138">Een DNS-zone maken</span><span class="sxs-lookup"><span data-stu-id="f5b00-138">Create a DNS zone</span></span>

<span data-ttu-id="f5b00-139">Een DNS-zone wordt gemaakt met Hallo `az network dns zone create` opdracht.</span><span class="sxs-lookup"><span data-stu-id="f5b00-139">A DNS zone is created using hello `az network dns zone create` command.</span></span> <span data-ttu-id="f5b00-140">Zie `az network dns zone create -h` voor help.</span><span class="sxs-lookup"><span data-stu-id="f5b00-140">For help, see `az network dns zone create -h`.</span></span>

<span data-ttu-id="f5b00-141">Hallo volgende voorbeeld maakt u een DNS-zone aangeroepen *contoso.com* in de resourcegroep Hallo aangeroepen *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="f5b00-141">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a><span data-ttu-id="f5b00-142">toocreate een DNS-zone met labels</span><span class="sxs-lookup"><span data-stu-id="f5b00-142">toocreate a DNS zone with tags</span></span>

<span data-ttu-id="f5b00-143">Hallo volgende voorbeeld laat zien hoe toocreate een DNS-zone met twee [Azure Resource Manager-tags](dns-zones-records.md#tags), *project = demo* en *env = test*, met behulp van Hallo `--tags` parameter (korte versie `-t`):</span><span class="sxs-lookup"><span data-stu-id="f5b00-143">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using hello `--tags` parameter (short form `-t`):</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="f5b00-144">Ophalen van een DNS-zone</span><span class="sxs-lookup"><span data-stu-id="f5b00-144">Get a DNS zone</span></span>

<span data-ttu-id="f5b00-145">gebruik van een DNS-zone tooretrieve `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="f5b00-145">tooretrieve a DNS zone, use `az network dns zone show`.</span></span> <span data-ttu-id="f5b00-146">Zie `az network dns zone show --help` voor help.</span><span class="sxs-lookup"><span data-stu-id="f5b00-146">For help, see `az network dns zone show --help`.</span></span>

<span data-ttu-id="f5b00-147">Hallo volgende voorbeeld retourneert Hallo DNS-zone *contoso.com* en de bijbehorende gegevens van de resourcegroep *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="f5b00-147">hello following example returns hello DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

<span data-ttu-id="f5b00-148">Hallo volgende voorbeeld is Hallo antwoord.</span><span class="sxs-lookup"><span data-stu-id="f5b00-148">hello following example is hello response.</span></span>

```json
{
  "etag": "00000002-0000-0000-3d4d-64aa3689d201",
  "id": "/subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-04.azure-dns.com.",
    "ns2-04.azure-dns.net.",
    "ns3-04.azure-dns.org.",
    "ns4-04.azure-dns.info."
  ],
  "numberOfRecordSets": 4,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="f5b00-149">Houd er rekening mee dat DNS-records worden niet geretourneerd door `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="f5b00-149">Note that DNS records are not returned by `az network dns zone show`.</span></span> <span data-ttu-id="f5b00-150">gebruik van DNS-records van toolist `az network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="f5b00-150">toolist DNS records, use `az network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="f5b00-151">Lijst met DNS-zones</span><span class="sxs-lookup"><span data-stu-id="f5b00-151">List DNS zones</span></span>

<span data-ttu-id="f5b00-152">tooenumerate DNS-zones, gebruik `az network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="f5b00-152">tooenumerate DNS zones, use `az network dns zone list`.</span></span> <span data-ttu-id="f5b00-153">Zie `az network dns zone list --help` voor help.</span><span class="sxs-lookup"><span data-stu-id="f5b00-153">For help, see `az network dns zone list --help`.</span></span>

<span data-ttu-id="f5b00-154">Het opgeven van het Hallo-resourcegroep bevat alleen deze zones in de resourcegroep Hallo:</span><span class="sxs-lookup"><span data-stu-id="f5b00-154">Specifying hello resource group lists only those zones within hello resource group:</span></span>

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

<span data-ttu-id="f5b00-155">Hallo resourcegroep als weggelaten een lijst met alle zones in abonnement Hallo:</span><span class="sxs-lookup"><span data-stu-id="f5b00-155">Omitting hello resource group lists all zones in hello subscription:</span></span>

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="f5b00-156">Bijwerken van een DNS-zone</span><span class="sxs-lookup"><span data-stu-id="f5b00-156">Update a DNS zone</span></span>

<span data-ttu-id="f5b00-157">Wijzigingen tooa DNS-zoneresource kan worden gemaakt met behulp van `az network dns zone update`.</span><span class="sxs-lookup"><span data-stu-id="f5b00-157">Changes tooa DNS zone resource can be made using `az network dns zone update`.</span></span> <span data-ttu-id="f5b00-158">Zie `az network dns zone update --help` voor help.</span><span class="sxs-lookup"><span data-stu-id="f5b00-158">For help, see `az network dns zone update --help`.</span></span>

<span data-ttu-id="f5b00-159">Met deze opdracht wordt niet Hallo DNS-recordsets binnen de zone Hallo bijgewerkt (Zie [hoe tooManage DNS-records](dns-operations-recordsets-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="f5b00-159">This command does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets-cli.md)).</span></span> <span data-ttu-id="f5b00-160">Alleen gebruikte tooupdate eigenschappen van Hallo zoneresource zelf is.</span><span class="sxs-lookup"><span data-stu-id="f5b00-160">It is only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="f5b00-161">Deze eigenschappen zijn momenteel beperkt toohello [Azure Resource Manager 'labels'](dns-zones-records.md#tags) voor Hallo zoneresource.</span><span class="sxs-lookup"><span data-stu-id="f5b00-161">These properties are currently limited toohello [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for hello zone resource.</span></span>

<span data-ttu-id="f5b00-162">Hallo volgende voorbeeld ziet u hoe tooupdate Hallo codes op een DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="f5b00-162">hello following example shows how tooupdate hello tags on a DNS zone.</span></span> <span data-ttu-id="f5b00-163">Hallo bestaande labels worden vervangen door Hallo waarde die is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f5b00-163">hello existing tags are replaced by hello value specified.</span></span>

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="f5b00-164">Een DNS-zone verwijderen</span><span class="sxs-lookup"><span data-stu-id="f5b00-164">Delete a DNS zone</span></span>

<span data-ttu-id="f5b00-165">DNS-zones worden verwijderd met een `az network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="f5b00-165">DNS zones can be deleted using `az network dns zone delete`.</span></span> <span data-ttu-id="f5b00-166">Zie `az network dns zone delete --help` voor help.</span><span class="sxs-lookup"><span data-stu-id="f5b00-166">For help, see `az network dns zone delete --help`.</span></span>

> [!NOTE]
> <span data-ttu-id="f5b00-167">Een DNS-zone verwijderen, verwijdert tevens alle DNS-records in Hallo zone.</span><span class="sxs-lookup"><span data-stu-id="f5b00-167">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="f5b00-168">Deze bewerking kan niet ongedaan worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f5b00-168">This operation cannot be undone.</span></span> <span data-ttu-id="f5b00-169">Als Hallo DNS-zone gebruikt wordt, mislukt services met behulp van de zone Hallo wanneer Hallo zone wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="f5b00-169">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="f5b00-170">tooprotect tegen het onbedoeld zone verwijderen, Zie [hoe tooprotect DNS-zones en registreert](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="f5b00-170">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="f5b00-171">Met deze opdracht vraagt om bevestiging.</span><span class="sxs-lookup"><span data-stu-id="f5b00-171">This command prompts for confirmation.</span></span> <span data-ttu-id="f5b00-172">Hallo optionele `--yes` schakeloptie deze vraag wordt geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="f5b00-172">hello optional `--yes` switch suppresses this prompt.</span></span>

<span data-ttu-id="f5b00-173">Hallo volgende voorbeeld laat zien hoe toodelete zone Hallo *contoso.com* uit resourcegroep *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="f5b00-173">hello following example shows how toodelete hello zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="f5b00-174">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f5b00-174">Next steps</span></span>

<span data-ttu-id="f5b00-175">Meer informatie over hoe te[beheren recordsets en records](dns-getstarted-create-recordset-cli.md) in uw DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="f5b00-175">Learn how too[manage record sets and records](dns-getstarted-create-recordset-cli.md) in your DNS zone.</span></span>

<span data-ttu-id="f5b00-176">Meer informatie over hoe te[delegeren van uw domein tooAzure DNS-](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="f5b00-176">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

