---
title: DNS-zones in Azure DNS - Azure CLI 2.0 beheren | Microsoft Docs
description: U kunt DNS-zones met Azure CLI 2.0 beheren. In dit artikel laat zien hoe bijwerken, verwijderen en DNS-zones maken op Azure DNS.
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
ms.openlocfilehash: 1414baf9e51d648cc3a46c4f8635040b4d276910
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-in-azure-dns-using-the-azure-cli-20"></a><span data-ttu-id="0cb9c-104">Het beheren van DNS-Zones in Azure DNS met de Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0cb9c-104">How to manage DNS Zones in Azure DNS using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0cb9c-105">Portal</span><span class="sxs-lookup"><span data-stu-id="0cb9c-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="0cb9c-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0cb9c-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="0cb9c-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0cb9c-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="0cb9c-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0cb9c-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)


<span data-ttu-id="0cb9c-109">Deze handleiding laat zien hoe uw DNS-zones beheren met behulp van de platformoverschrijdende Azure CLI, die beschikbaar is voor Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-109">This guide shows how to manage your DNS zones by using the cross-platform Azure CLI, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="0cb9c-110">U kunt ook beheren met behulp van DNS-zones [Azure PowerShell](dns-operations-dnszones.md) of de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or the Azure portal.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="0cb9c-111">CLI-versies om de taak uit te voeren</span><span class="sxs-lookup"><span data-stu-id="0cb9c-111">CLI versions to complete the task</span></span>

<span data-ttu-id="0cb9c-112">U kunt de taak uitvoeren met behulp van een van de volgende CLI-versies:</span><span class="sxs-lookup"><span data-stu-id="0cb9c-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="0cb9c-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md): onze CLI voor het klassieke implementatiemodel en het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="0cb9c-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md): onze CLI van de volgende generatie voor het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="0cb9c-115">Inleiding</span><span class="sxs-lookup"><span data-stu-id="0cb9c-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a><span data-ttu-id="0cb9c-116">Azure CLI 2.0 instellen voor Azure DNS</span><span class="sxs-lookup"><span data-stu-id="0cb9c-116">Set up Azure CLI 2.0 for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="0cb9c-117">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="0cb9c-117">Before you begin</span></span>

<span data-ttu-id="0cb9c-118">Controleer voordat u met de configuratie begint of u de volgende items hebt.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-118">Verify that you have the following items before beginning your configuration.</span></span>

* <span data-ttu-id="0cb9c-119">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-119">An Azure subscription.</span></span> <span data-ttu-id="0cb9c-120">Als u nog geen Azure-abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of [u aanmelden voor een gratis account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0cb9c-120">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="0cb9c-121">Installeer de nieuwste versie van de Azure CLI 2.0, beschikbaar voor Windows, Linux of MAC.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-121">Install the latest version of the Azure CLI 2.0, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="0cb9c-122">Ga naar [Azure-CLI 2.0 installeren](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-122">More information is available at [Install the Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

### <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="0cb9c-123">Aanmelden bij uw Azure-account</span><span class="sxs-lookup"><span data-stu-id="0cb9c-123">Sign in to your Azure account</span></span>

<span data-ttu-id="0cb9c-124">Open een consolevenster en doorloop de verificatie met uw referenties.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-124">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="0cb9c-125">Zie Aanmelden bij Azure vanaf de Azure CLI voor meer informatie</span><span class="sxs-lookup"><span data-stu-id="0cb9c-125">For more information, see Log in to Azure from the Azure CLI</span></span>

```
az login
```

### <a name="select-the-subscription"></a><span data-ttu-id="0cb9c-126">Het abonnement selecteren</span><span class="sxs-lookup"><span data-stu-id="0cb9c-126">Select the subscription</span></span>

<span data-ttu-id="0cb9c-127">Controleer de abonnementen voor het account.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-127">Check the subscriptions for the account.</span></span>

```
az account list
```

<span data-ttu-id="0cb9c-128">Kies welk Azure-abonnement u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-128">Choose which of your Azure subscriptions to use.</span></span>

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="0cb9c-129">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="0cb9c-129">Create a resource group</span></span>

<span data-ttu-id="0cb9c-130">Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="0cb9c-131">Deze locatie wordt gebruikt als de standaardlocatie voor resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-131">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="0cb9c-132">Aangezien alle DNS-resources globaal en niet regionaal zijn, is de keuze van de locatie voor de resourcegroep niet van invloed op Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-132">However, because all DNS resources are global, not regional, the choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="0cb9c-133">U kunt deze stap overslaan als u een bestaande resourcegroep gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-133">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a><span data-ttu-id="0cb9c-134">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="0cb9c-134">Getting help</span></span>

<span data-ttu-id="0cb9c-135">Alle 2.0 CLI-opdrachten met betrekking tot de Azure DNS beginnen met `az network dns`.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-135">All CLI 2.0 commands relating to Azure DNS start with `az network dns`.</span></span> <span data-ttu-id="0cb9c-136">Help beschikbaar is voor elke opdracht met behulp van de `--help` optie (korte versie `-h`).</span><span class="sxs-lookup"><span data-stu-id="0cb9c-136">Help is available for each command using the `--help` option (short form `-h`).</span></span>  <span data-ttu-id="0cb9c-137">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0cb9c-137">For example:</span></span>

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="0cb9c-138">Een DNS-zone maken</span><span class="sxs-lookup"><span data-stu-id="0cb9c-138">Create a DNS zone</span></span>

<span data-ttu-id="0cb9c-139">Een DNS-zone wordt gemaakt met de opdracht `az network dns zone create`.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-139">A DNS zone is created using the `az network dns zone create` command.</span></span> <span data-ttu-id="0cb9c-140">Zie `az network dns zone create -h` voor help.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-140">For help, see `az network dns zone create -h`.</span></span>

<span data-ttu-id="0cb9c-141">Het volgende voorbeeld wordt een DNS-zone aangeroepen *contoso.com* aangeroepen in de resourcegroep *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="0cb9c-141">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="to-create-a-dns-zone-with-tags"></a><span data-ttu-id="0cb9c-142">Een DNS-zone maken met labels</span><span class="sxs-lookup"><span data-stu-id="0cb9c-142">To create a DNS zone with tags</span></span>

<span data-ttu-id="0cb9c-143">Het volgende voorbeeld laat zien hoe een DNS-zone maken met twee [Azure Resource Manager-tags](dns-zones-records.md#tags), *project = demo* en *env = test*, met behulp van de `--tags` parameter (korte versie `-t`):</span><span class="sxs-lookup"><span data-stu-id="0cb9c-143">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using the `--tags` parameter (short form `-t`):</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="0cb9c-144">Ophalen van een DNS-zone</span><span class="sxs-lookup"><span data-stu-id="0cb9c-144">Get a DNS zone</span></span>

<span data-ttu-id="0cb9c-145">Gebruik voor het ophalen van een DNS-zone `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-145">To retrieve a DNS zone, use `az network dns zone show`.</span></span> <span data-ttu-id="0cb9c-146">Zie `az network dns zone show --help` voor help.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-146">For help, see `az network dns zone show --help`.</span></span>

<span data-ttu-id="0cb9c-147">Het volgende voorbeeld retourneert de DNS-zone *contoso.com* en de bijbehorende gegevens van de resourcegroep *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-147">The following example returns the DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

<span data-ttu-id="0cb9c-148">Het volgende voorbeeld is het antwoord.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-148">The following example is the response.</span></span>

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

<span data-ttu-id="0cb9c-149">Houd er rekening mee dat DNS-records worden niet geretourneerd door `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-149">Note that DNS records are not returned by `az network dns zone show`.</span></span> <span data-ttu-id="0cb9c-150">DNS-records weergeven door gebruiken `az network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-150">To list DNS records, use `az network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="0cb9c-151">Lijst met DNS-zones</span><span class="sxs-lookup"><span data-stu-id="0cb9c-151">List DNS zones</span></span>

<span data-ttu-id="0cb9c-152">Gebruik voor het inventariseren van DNS-zones `az network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-152">To enumerate DNS zones, use `az network dns zone list`.</span></span> <span data-ttu-id="0cb9c-153">Zie `az network dns zone list --help` voor help.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-153">For help, see `az network dns zone list --help`.</span></span>

<span data-ttu-id="0cb9c-154">Het opgeven van de resourcegroep bevat alleen deze zones binnen de resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="0cb9c-154">Specifying the resource group lists only those zones within the resource group:</span></span>

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

<span data-ttu-id="0cb9c-155">Als de resourcegroep wordt weggelaten, worden alle zones in het abonnement:</span><span class="sxs-lookup"><span data-stu-id="0cb9c-155">Omitting the resource group lists all zones in the subscription:</span></span>

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="0cb9c-156">Bijwerken van een DNS-zone</span><span class="sxs-lookup"><span data-stu-id="0cb9c-156">Update a DNS zone</span></span>

<span data-ttu-id="0cb9c-157">Een DNS-zone-bron kan worden gewijzigd met behulp van `az network dns zone update`.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-157">Changes to a DNS zone resource can be made using `az network dns zone update`.</span></span> <span data-ttu-id="0cb9c-158">Zie `az network dns zone update --help` voor help.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-158">For help, see `az network dns zone update --help`.</span></span>

<span data-ttu-id="0cb9c-159">Met deze opdracht wordt de DNS-recordsets binnen de zone niet bijgewerkt (Zie [het beheren van DNS-records](dns-operations-recordsets-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="0cb9c-159">This command does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets-cli.md)).</span></span> <span data-ttu-id="0cb9c-160">Het wordt alleen gebruikt om de eigenschappen van de bron van de zone zelf te werken.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-160">It is only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="0cb9c-161">Deze eigenschappen zijn momenteel beperkt tot de [Azure Resource Manager 'labels'](dns-zones-records.md#tags) voor de zoneresource.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-161">These properties are currently limited to the [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for the zone resource.</span></span>

<span data-ttu-id="0cb9c-162">Het volgende voorbeeld laat zien hoe de labels voor een DNS-zone bijwerken.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-162">The following example shows how to update the tags on a DNS zone.</span></span> <span data-ttu-id="0cb9c-163">De bestaande labels worden vervangen door de opgegeven waarde.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-163">The existing tags are replaced by the value specified.</span></span>

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="0cb9c-164">Een DNS-zone verwijderen</span><span class="sxs-lookup"><span data-stu-id="0cb9c-164">Delete a DNS zone</span></span>

<span data-ttu-id="0cb9c-165">DNS-zones worden verwijderd met een `az network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-165">DNS zones can be deleted using `az network dns zone delete`.</span></span> <span data-ttu-id="0cb9c-166">Zie `az network dns zone delete --help` voor help.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-166">For help, see `az network dns zone delete --help`.</span></span>

> [!NOTE]
> <span data-ttu-id="0cb9c-167">Een DNS-zone verwijderen, verwijdert tevens alle DNS-records in de zone.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-167">Deleting a DNS zone also deletes all DNS records within the zone.</span></span> <span data-ttu-id="0cb9c-168">Deze bewerking kan niet ongedaan worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-168">This operation cannot be undone.</span></span> <span data-ttu-id="0cb9c-169">Als de DNS-zone gebruikt wordt, worden services met behulp van de zone mislukt wanneer de zone wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-169">If the DNS zone is in use, services using the zone will fail when the zone is deleted.</span></span>
>
><span data-ttu-id="0cb9c-170">Als u wilt beveiligen tegen het onbedoeld zone verwijderen, Zie [het beveiligen van DNS-zones en records](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="0cb9c-170">To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="0cb9c-171">Met deze opdracht vraagt om bevestiging.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-171">This command prompts for confirmation.</span></span> <span data-ttu-id="0cb9c-172">De optionele `--yes` schakeloptie deze vraag wordt geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-172">The optional `--yes` switch suppresses this prompt.</span></span>

<span data-ttu-id="0cb9c-173">Het volgende voorbeeld laat zien hoe de zone verwijderen *contoso.com* uit resourcegroep *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-173">The following example shows how to delete the zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="0cb9c-174">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0cb9c-174">Next steps</span></span>

<span data-ttu-id="0cb9c-175">Meer informatie over hoe [beheren recordsets en records](dns-getstarted-create-recordset-cli.md) in uw DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="0cb9c-175">Learn how to [manage record sets and records](dns-getstarted-create-recordset-cli.md) in your DNS zone.</span></span>

<span data-ttu-id="0cb9c-176">Meer informatie over hoe [uw domein delegeren naar Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="0cb9c-176">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

