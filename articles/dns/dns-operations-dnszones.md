---
title: aaaManage DNS-zones in Azure DNS - PowerShell | Microsoft Docs
description: U kunt DNS-zones met Azure Powershell beheren. Dit artikel wordt beschreven hoe tooupdate, verwijderen en DNS-zones maken op Azure DNS
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: a67992ab-8166-4052-9b28-554c5a39e60c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: 261b89f72213aa9784034d47ff9d1c55a4e80d65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-using-powershell"></a><span data-ttu-id="68d5b-104">Hoe toomanage DNS-Zones met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="68d5b-104">How toomanage DNS Zones using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="68d5b-105">Portal</span><span class="sxs-lookup"><span data-stu-id="68d5b-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="68d5b-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="68d5b-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="68d5b-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="68d5b-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="68d5b-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="68d5b-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="68d5b-109">Dit artikel laat zien hoe toomanage uw DNS-zones met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="68d5b-109">This article shows you how toomanage your DNS zones by using Azure PowerShell.</span></span> <span data-ttu-id="68d5b-110">U kunt ook de DNS-zones met behulp van de platformoverschrijdende Hallo beheren [Azure CLI](dns-operations-dnszones-cli.md) of hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="68d5b-110">You can also manage your DNS zones using hello cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or hello Azure portal.</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a><span data-ttu-id="68d5b-111">Een DNS-zone maken</span><span class="sxs-lookup"><span data-stu-id="68d5b-111">Create a DNS zone</span></span>

<span data-ttu-id="68d5b-112">Een DNS-zone wordt gemaakt met behulp van Hallo `New-AzureRmDnsZone` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="68d5b-112">A DNS zone is created by using hello `New-AzureRmDnsZone` cmdlet.</span></span>

<span data-ttu-id="68d5b-113">Hallo volgende voorbeeld maakt u een DNS-zone aangeroepen *contoso.com* in de resourcegroep Hallo aangeroepen *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="68d5b-113">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="68d5b-114">Hallo volgende voorbeeld laat zien hoe toocreate een DNS-zone met twee [Azure Resource Manager-tags](dns-zones-records.md#tags), *project = demo* en *env = test*:</span><span class="sxs-lookup"><span data-stu-id="68d5b-114">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="68d5b-115">Ophalen van een DNS-zone</span><span class="sxs-lookup"><span data-stu-id="68d5b-115">Get a DNS zone</span></span>

<span data-ttu-id="68d5b-116">een DNS-zone tooretrieve gebruiken Hallo `Get-AzureRmDnsZone` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="68d5b-116">tooretrieve a DNS zone, use hello `Get-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="68d5b-117">Deze bewerking retourneert een DNS-zone-object bijbehorende tooan bestaande zone in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="68d5b-117">This operation returns a DNS zone object corresponding tooan existing zone in Azure DNS.</span></span> <span data-ttu-id="68d5b-118">Hallo object bevat gegevens over Hallo zone (zoals Hallo aantal recordsets), maar bevat geen Hallo-recordsets zelf (Zie `Get-AzureRmDnsRecordSet`).</span><span class="sxs-lookup"><span data-stu-id="68d5b-118">hello object contains data about hello zone (such as hello number of record sets), but does not contain hello record sets themselves (see `Get-AzureRmDnsRecordSet`).</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com –ResourceGroupName MyAzureResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-8ec2-f4879750d201
Tags                  : {project, env}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org.,
                        ns4-01.azure-dns.info.}
NumberOfRecordSets    : 2
MaxNumberOfRecordSets : 5000
```

## <a name="list-dns-zones"></a><span data-ttu-id="68d5b-119">Lijst met DNS-zones</span><span class="sxs-lookup"><span data-stu-id="68d5b-119">List DNS zones</span></span>

<span data-ttu-id="68d5b-120">Door de zonenaam Hallo van weg te laten `Get-AzureRmDnsZone`, kunt u alle zones in een resourcegroep opsommen.</span><span class="sxs-lookup"><span data-stu-id="68d5b-120">By omitting hello zone name from `Get-AzureRmDnsZone`, you can enumerate all zones in a resource group.</span></span> <span data-ttu-id="68d5b-121">Deze bewerking retourneert een matrix van objecten van de zone.</span><span class="sxs-lookup"><span data-stu-id="68d5b-121">This operation returns an array of zone objects.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="68d5b-122">Door zowel zonenaam Hallo Hallo Resourcegroepnaam van weg te laten `Get-AzureRmDnsZone`, kunt u alle zones in hello Azure-abonnement opsommen.</span><span class="sxs-lookup"><span data-stu-id="68d5b-122">By omitting both hello zone name and hello resource group name from `Get-AzureRmDnsZone`, you can enumerate all zones in hello Azure subscription.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="68d5b-123">Bijwerken van een DNS-zone</span><span class="sxs-lookup"><span data-stu-id="68d5b-123">Update a DNS zone</span></span>

<span data-ttu-id="68d5b-124">DNS-zoneresource kan worden gemaakt met behulp van tooa wijzigingen `Set-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="68d5b-124">Changes tooa DNS zone resource can be made by using `Set-AzureRmDnsZone`.</span></span> <span data-ttu-id="68d5b-125">Deze cmdlet werkt niet Hallo DNS-recordsets binnen de zone Hallo bij (Zie [hoe tooManage DNS-records](dns-operations-recordsets.md)).</span><span class="sxs-lookup"><span data-stu-id="68d5b-125">This cmdlet does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets.md)).</span></span> <span data-ttu-id="68d5b-126">Het is alleen tooupdate eigenschappen van Hallo zoneresource zelf gebruikt.</span><span class="sxs-lookup"><span data-stu-id="68d5b-126">It's only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="68d5b-127">Hallo beschrijfbare zone-eigenschappen zijn momenteel beperkt toohello [Azure Resource Manager '-tags' voor Hallo zoneresource](dns-zones-records.md#tags).</span><span class="sxs-lookup"><span data-stu-id="68d5b-127">hello writable zone properties are currently limited toohello [Azure Resource Manager ‘tags’ for hello zone resource](dns-zones-records.md#tags).</span></span>

<span data-ttu-id="68d5b-128">Gebruik een van de volgende twee manieren tooupdate Hallo een DNS-zone:</span><span class="sxs-lookup"><span data-stu-id="68d5b-128">Use one of hello following two ways tooupdate a DNS zone:</span></span>

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group"></a><span data-ttu-id="68d5b-129">Hallo-zone met Hallo zone en de bron-groep opgeven</span><span class="sxs-lookup"><span data-stu-id="68d5b-129">Specify hello zone using hello zone name and resource group</span></span>

<span data-ttu-id="68d5b-130">Deze aanpak vervangen Hallo bestaande zone codes door Hallo waarden die zijn opgegeven.</span><span class="sxs-lookup"><span data-stu-id="68d5b-130">This approach replaces hello existing zone tags with hello values specified.</span></span>

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-hello-zone-using-a-zone-object"></a><span data-ttu-id="68d5b-131">Hallo-zone met behulp van een object $zone opgeven</span><span class="sxs-lookup"><span data-stu-id="68d5b-131">Specify hello zone using a $zone object</span></span>

<span data-ttu-id="68d5b-132">Deze aanpak Hallo bestaande zone object opgehaald, Hallo labels wijzigt en vervolgens Hallo wijzigingen worden doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="68d5b-132">This approach retrieves hello existing zone object, modifies hello tags, and then commits hello changes.</span></span> <span data-ttu-id="68d5b-133">Op deze manier kunnen u bestaande labels behouden.</span><span class="sxs-lookup"><span data-stu-id="68d5b-133">In this way, existing tags can be preserved.</span></span>

```powershell
# Get hello zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="68d5b-134">Wanneer u `Set-AzureRmDnsZone` met een object $zone [Etag controleert](dns-zones-records.md#etags) worden gebruikt tooensure gelijktijdige wijzigingen worden niet overschreven.</span><span class="sxs-lookup"><span data-stu-id="68d5b-134">When using `Set-AzureRmDnsZone` with a $zone object, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="68d5b-135">U kunt optioneel Hallo `-Overwrite` overschakelen toosuppress deze controles.</span><span class="sxs-lookup"><span data-stu-id="68d5b-135">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

## <a name="delete-a-dns-zone"></a><span data-ttu-id="68d5b-136">Een DNS-Zone verwijderen</span><span class="sxs-lookup"><span data-stu-id="68d5b-136">Delete a DNS Zone</span></span>

<span data-ttu-id="68d5b-137">DNS-zones worden verwijderd met de Hallo `Remove-AzureRmDnsZone` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="68d5b-137">DNS zones can be deleted using hello `Remove-AzureRmDnsZone` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="68d5b-138">Een DNS-zone verwijderen, verwijdert tevens alle DNS-records in Hallo zone.</span><span class="sxs-lookup"><span data-stu-id="68d5b-138">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="68d5b-139">Deze bewerking kan niet ongedaan worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="68d5b-139">This operation cannot be undone.</span></span> <span data-ttu-id="68d5b-140">Als Hallo DNS-zone gebruikt wordt, mislukt services met behulp van de zone Hallo wanneer Hallo zone wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="68d5b-140">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="68d5b-141">tooprotect tegen het onbedoeld zone verwijderen, Zie [hoe tooprotect DNS-zones en registreert](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="68d5b-141">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>


<span data-ttu-id="68d5b-142">Gebruik een van de volgende twee manieren toodelete Hallo een DNS-zone:</span><span class="sxs-lookup"><span data-stu-id="68d5b-142">Use one of hello following two ways toodelete a DNS zone:</span></span>

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group-name"></a><span data-ttu-id="68d5b-143">Geef Hallo-zone met behulp van de zonenaam Hallo en de naam van resourcegroep</span><span class="sxs-lookup"><span data-stu-id="68d5b-143">Specify hello zone using hello zone name and resource group name</span></span>

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-hello-zone-using-a-zone-object"></a><span data-ttu-id="68d5b-144">Hallo-zone met behulp van een object $zone opgeven</span><span class="sxs-lookup"><span data-stu-id="68d5b-144">Specify hello zone using a $zone object</span></span>

<span data-ttu-id="68d5b-145">U kunt opgeven dat Hallo zone toobe verwijderd met een `$zone` object dat wordt geretourneerd door `Get-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="68d5b-145">You can specify hello zone toobe deleted using a `$zone` object returned by `Get-AzureRmDnsZone`.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="68d5b-146">Hallo zone object kan ook worden doorgesluisd in plaats van dat wordt doorgegeven als parameter:</span><span class="sxs-lookup"><span data-stu-id="68d5b-146">hello zone object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

<span data-ttu-id="68d5b-147">Net als bij `Set-AzureRmDnsZone`, geven Hallo zone met behulp van een `$zone` object kunt Etag controleert tooensure gelijktijdige wijzigingen worden niet verwijderd.</span><span class="sxs-lookup"><span data-stu-id="68d5b-147">As with `Set-AzureRmDnsZone`, specifying hello zone using a `$zone` object enables Etag checks tooensure concurrent changes are not deleted.</span></span> <span data-ttu-id="68d5b-148">Gebruik Hallo `-Overwrite` overschakelen toosuppress deze controles.</span><span class="sxs-lookup"><span data-stu-id="68d5b-148">Use hello `-Overwrite` switch toosuppress these checks.</span></span>

## <a name="confirmation-prompts"></a><span data-ttu-id="68d5b-149">Bevestiging vragen</span><span class="sxs-lookup"><span data-stu-id="68d5b-149">Confirmation prompts</span></span>

<span data-ttu-id="68d5b-150">Hallo `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, en `Remove-AzureRmDnsZone` cmdlets alle bevestiging vragen ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="68d5b-150">hello `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, and `Remove-AzureRmDnsZone` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="68d5b-151">Beide `New-AzureRmDnsZone` en `Set-AzureRmDnsZone` vragen om bevestiging als hello `$ConfirmPreference` PowerShell voorkeursvariabele een waarde heeft van `Medium` of lager.</span><span class="sxs-lookup"><span data-stu-id="68d5b-151">Both `New-AzureRmDnsZone` and `Set-AzureRmDnsZone` prompt for confirmation if hello `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="68d5b-152">Vanwege het potentieel grote invloed van de toohello van het verwijderen van een DNS-zone hello `Remove-AzureRmDnsZone` cmdlet vraagt om bevestiging als hello `$ConfirmPreference` PowerShell variabele heeft de waarde van een andere waarde dan `None`.</span><span class="sxs-lookup"><span data-stu-id="68d5b-152">Due toohello potentially high impact of deleting a DNS zone, hello `Remove-AzureRmDnsZone` cmdlet prompts for confirmation if hello `$ConfirmPreference` PowerShell variable has any value other than `None`.</span></span>

<span data-ttu-id="68d5b-153">Sinds de standaardwaarde Hallo voor `$ConfirmPreference` is `High`, alleen `Remove-AzureRmDnsZone` vraagt om bevestiging standaard.</span><span class="sxs-lookup"><span data-stu-id="68d5b-153">Since hello default value for `$ConfirmPreference` is `High`, only `Remove-AzureRmDnsZone` prompts for confirmation by default.</span></span>

<span data-ttu-id="68d5b-154">U kunt de huidige Hallo overschrijven `$ConfirmPreference` instelling met de Hallo `-Confirm` parameter.</span><span class="sxs-lookup"><span data-stu-id="68d5b-154">You can override hello current `$ConfirmPreference` setting using hello `-Confirm` parameter.</span></span> <span data-ttu-id="68d5b-155">Als u opgeeft `-Confirm` of `-Confirm:$True` , Hallo cmdlet vraagt u om bevestiging voordat deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="68d5b-155">If you specify `-Confirm` or `-Confirm:$True` , hello cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="68d5b-156">Als u opgeeft `-Confirm:$False` , Hallo cmdlet wordt u niet gevraagd om bevestiging.</span><span class="sxs-lookup"><span data-stu-id="68d5b-156">If you specify `-Confirm:$False` , hello cmdlet does not prompt you for confirmation.</span></span>

<span data-ttu-id="68d5b-157">Voor meer informatie over `-Confirm` en `$ConfirmPreference`, Zie [over Voorkeursvariabelen](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span><span class="sxs-lookup"><span data-stu-id="68d5b-157">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="68d5b-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="68d5b-158">Next steps</span></span>

<span data-ttu-id="68d5b-159">Meer informatie over hoe te[beheren recordsets en records](dns-operations-recordsets.md) in uw DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="68d5b-159">Learn how too[manage record sets and records](dns-operations-recordsets.md) in your DNS zone.</span></span>
<br>
<span data-ttu-id="68d5b-160">Meer informatie over hoe te[delegeren van uw domein tooAzure DNS-](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="68d5b-160">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>
<br>
<span data-ttu-id="68d5b-161">Bekijk Hallo [Azure DNS PowerShell-naslagdocumentatie](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="68d5b-161">Review hello [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>

