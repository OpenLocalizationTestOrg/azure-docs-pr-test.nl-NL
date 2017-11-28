---
title: aaaTag Azure-resources voor logische organisatie | Microsoft Docs
description: Toont hoe tooapply tags tooorganize Azure-resources voor facturerings- en beheren.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 003a78e5-2ff8-4685-93b4-e94d6fb8ed5b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: AzurePortal
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tomfitz
ms.openlocfilehash: e07470463d160f8cefe5c80bc91e66a96af6ca45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-tags-tooorganize-your-azure-resources"></a><span data-ttu-id="16cb8-103">Gebruik tags tooorganize uw Azure-resources</span><span class="sxs-lookup"><span data-stu-id="16cb8-103">Use tags tooorganize your Azure resources</span></span>
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> <span data-ttu-id="16cb8-104">U kunt alleen tooresources labels die ondersteuning bieden voor Azure Resource Manager-bewerkingen toepassen.</span><span class="sxs-lookup"><span data-stu-id="16cb8-104">You can apply tags only tooresources that support Azure Resource Manager operations.</span></span> <span data-ttu-id="16cb8-105">Als u een virtuele machine, het virtuele netwerk of de storage-account via de klassieke implementatiemodel hello (zoals als via Hallo klassieke Azure-portal) gemaakt, kunt u een label toothat resource niet toepassen.</span><span class="sxs-lookup"><span data-stu-id="16cb8-105">If you created a virtual machine, virtual network, or storage account through hello classic deployment model (such as through hello Azure classic portal), you cannot apply a tag toothat resource.</span></span> <span data-ttu-id="16cb8-106">toosupport tagging, implementeert u deze resources via Resource Manager opnieuw.</span><span class="sxs-lookup"><span data-stu-id="16cb8-106">toosupport tagging, redeploy these resources through Resource Manager.</span></span> <span data-ttu-id="16cb8-107">Alle andere bronnen ondersteuning voor codering.</span><span class="sxs-lookup"><span data-stu-id="16cb8-107">All other resources support tagging.</span></span>
> 
> 

## <a name="policies-for-tag-consistency"></a><span data-ttu-id="16cb8-108">Beleid voor consistentie van de tag</span><span class="sxs-lookup"><span data-stu-id="16cb8-108">Policies for tag consistency</span></span>

<span data-ttu-id="16cb8-109">U kunt resource toocreate standaardregels-beleid gebruiken voor uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="16cb8-109">You can use resource policies toocreate standard rules for your organization.</span></span> <span data-ttu-id="16cb8-110">U kunt beleidsregels die zorg ervoor dat resources worden gemarkeerd met de juiste waarden Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="16cb8-110">You can create policies that ensure resources are tagged with hello appropriate values.</span></span> <span data-ttu-id="16cb8-111">Zie voor meer informatie [bronbeleid voor tags toepassen](resource-manager-policy-tags.md).</span><span class="sxs-lookup"><span data-stu-id="16cb8-111">For more information, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="16cb8-112">PowerShell</span><span class="sxs-lookup"><span data-stu-id="16cb8-112">PowerShell</span></span>
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a><span data-ttu-id="16cb8-113">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="16cb8-113">Azure CLI</span></span>

<span data-ttu-id="16cb8-114">toosee Hallo bestaande codes voor een *resourcegroep*, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="16cb8-114">toosee hello existing tags for a *resource group*, use:</span></span>

```azurecli
az group show -n examplegroup --query tags
```

<span data-ttu-id="16cb8-115">Script retourneert Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="16cb8-115">That script returns hello following format:</span></span>

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

<span data-ttu-id="16cb8-116">toosee Hallo bestaande codes voor een *resource met een opgegeven bron-ID*, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="16cb8-116">toosee hello existing tags for a *resource that has a specified resource ID*, use:</span></span>

```azurecli
az resource show --id {resource-id} --query tags
```

<span data-ttu-id="16cb8-117">Of toosee Hallo bestaande codes voor een *resource met een opgegeven groep met de naam, type en resource*, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="16cb8-117">Or, toosee hello existing tags for a *resource that has a specified name, type, and resource group*, use:</span></span>

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

<span data-ttu-id="16cb8-118">tooget-resourcegroepen die beschikken over een specifieke tag gebruiken `az group list`:</span><span class="sxs-lookup"><span data-stu-id="16cb8-118">tooget resource groups that have a specific tag, use `az group list`:</span></span>

```azurecli
az group list --tag Dept=IT
```

<span data-ttu-id="16cb8-119">alle Hallo-resources die een bepaalde tag en-waarde, gebruikt u tooget `az resource list`:</span><span class="sxs-lookup"><span data-stu-id="16cb8-119">tooget all hello resources that have a particular tag and value, use `az resource list`:</span></span>

```azurecli
az resource list --tag Dept=Finance
```

<span data-ttu-id="16cb8-120">Telkens wanneer u labels tooa resource of een resourcegroep hebt toegepast, kunt u bestaande labels op die resource of resourcegroep Hallo overschrijven.</span><span class="sxs-lookup"><span data-stu-id="16cb8-120">Every time you apply tags tooa resource or a resource group, you overwrite hello existing tags on that resource or resource group.</span></span> <span data-ttu-id="16cb8-121">Daarom moet u een andere benadering, op basis van of Hallo resource of resourcegroep bestaande labels heeft.</span><span class="sxs-lookup"><span data-stu-id="16cb8-121">Therefore, you must use a different approach based on whether hello resource or resource group has existing tags.</span></span> 

<span data-ttu-id="16cb8-122">tooadd tags tooa *resourcegroep zonder bestaande tags*, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="16cb8-122">tooadd tags tooa *resource group without existing tags*, use:</span></span>

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

<span data-ttu-id="16cb8-123">tooadd tags tooa *resource zonder bestaande tags*, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="16cb8-123">tooadd tags tooa *resource without existing tags*, use:</span></span>

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

<span data-ttu-id="16cb8-124">tooadd labels tooa resource die al is tags, Hallo bestaande labels ophalen, die waarde opnieuw indelen en Hallo bestaande en nieuwe tags toepassen:</span><span class="sxs-lookup"><span data-stu-id="16cb8-124">tooadd tags tooa resource that already has tags, retrieve hello existing tags, reformat that value, and reapply hello existing and new tags:</span></span> 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

<span data-ttu-id="16cb8-125">tooapply die alle labels van een resource tooits groepsbronnen en *bestaande labels op Hallo resources niet bewaren*, Hallo script volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="16cb8-125">tooapply all tags from a resource group tooits resources, and *not retain existing tags on hello resources*, use hello following script:</span></span>

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    az resource tag --tags $t --id $resid
  done 
done
```

<span data-ttu-id="16cb8-126">tooapply die alle labels van een resource tooits groepsbronnen en *bestaande tags voor bronnen behouden*, Hallo script volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="16cb8-126">tooapply all tags from a resource group tooits resources, and *retain existing tags on resources*, use hello following script:</span></span>

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    jsonrtag=$(az resource show --id $resid --query tags)
    rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
    az resource tag --tags $t$rt --id $resid
  done 
done
```


## <a name="templates"></a><span data-ttu-id="16cb8-127">Sjablonen</span><span class="sxs-lookup"><span data-stu-id="16cb8-127">Templates</span></span>

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a><span data-ttu-id="16cb8-128">Portal</span><span class="sxs-lookup"><span data-stu-id="16cb8-128">Portal</span></span>
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a><span data-ttu-id="16cb8-129">REST API</span><span class="sxs-lookup"><span data-stu-id="16cb8-129">REST API</span></span>
<span data-ttu-id="16cb8-130">Hello Azure-portal en PowerShell gebruiken Hallo [REST-API van Resource Manager](https://docs.microsoft.com/rest/api/resources/) achter de schermen Hallo.</span><span class="sxs-lookup"><span data-stu-id="16cb8-130">hello Azure portal and PowerShell both use hello [Resource Manager REST API](https://docs.microsoft.com/rest/api/resources/) behind hello scenes.</span></span> <span data-ttu-id="16cb8-131">Als u toointegrate labels in een andere omgeving nodig hebt, kunt u de labels krijgen met behulp van **ophalen** op Hallo resource-ID en update Hallo set van labels met behulp van een **PATCH** aanroepen.</span><span class="sxs-lookup"><span data-stu-id="16cb8-131">If you need toointegrate tagging into another environment, you can get tags by using **GET** on hello resource ID and update hello set of tags by using a **PATCH** call.</span></span>

## <a name="tags-and-billing"></a><span data-ttu-id="16cb8-132">Labels en facturering</span><span class="sxs-lookup"><span data-stu-id="16cb8-132">Tags and billing</span></span>
<span data-ttu-id="16cb8-133">U kunt uw factureringsgegevens toogroup labels.</span><span class="sxs-lookup"><span data-stu-id="16cb8-133">You can use tags toogroup your billing data.</span></span> <span data-ttu-id="16cb8-134">Bijvoorbeeld, als u meerdere virtuele machines voor verschillende organisaties uitvoert, gebruik Hallo labels toogroup gebruik door kostenplaats.</span><span class="sxs-lookup"><span data-stu-id="16cb8-134">For example, if you are running multiple VMs for different organizations, use hello tags toogroup usage by cost center.</span></span> <span data-ttu-id="16cb8-135">U kunt ook labels toocategorize kosten door de runtimeomgeving, zoals facturering gebruik Hallo voor virtuele machines die worden uitgevoerd in de productieomgeving hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="16cb8-135">You can also use tags toocategorize costs by runtime environment, such as hello billing usage for VMs running in hello production environment.</span></span>


<span data-ttu-id="16cb8-136">U kunt informatie over tags via Hallo ophalen [Azure brongebruik en RateCard APIs](../billing/billing-usage-rate-card-overview.md) of Hallo-gebruik door komma's gescheiden waarden (CSV)-bestand.</span><span class="sxs-lookup"><span data-stu-id="16cb8-136">You can retrieve information about tags through hello [Azure Resource Usage and RateCard APIs](../billing/billing-usage-rate-card-overview.md) or hello usage comma-separated values (CSV) file.</span></span> <span data-ttu-id="16cb8-137">U Hallo gebruik bestand downloaden van Hallo [Azure accountportal](https://account.windowsazure.com/) of [EA portal](https://ea.azure.com).</span><span class="sxs-lookup"><span data-stu-id="16cb8-137">You download hello usage file from hello [Azure account portal](https://account.windowsazure.com/) or [EA portal](https://ea.azure.com).</span></span> <span data-ttu-id="16cb8-138">Zie voor meer informatie over toegang op programmeerniveau toobilling [inzicht in uw Microsoft Azure-brongebruik](../billing/billing-usage-rate-card-overview.md).</span><span class="sxs-lookup"><span data-stu-id="16cb8-138">For more information about programmatic access toobilling information, see [Gain insights into your Microsoft Azure resource consumption](../billing/billing-usage-rate-card-overview.md).</span></span> <span data-ttu-id="16cb8-139">Zie voor REST-API-bewerkingen, [Azure Billing REST API-verwijzing](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span><span class="sxs-lookup"><span data-stu-id="16cb8-139">For REST API operations, see [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span></span>


<span data-ttu-id="16cb8-140">Wanneer u Hallo gebruik CSV voor services die ondersteuning bieden voor facturerings-tags downloadt, Hallo labels worden weergegeven in Hallo **labels** kolom.</span><span class="sxs-lookup"><span data-stu-id="16cb8-140">When you download hello usage CSV for services that support tags with billing, hello tags appear in hello **Tags** column.</span></span> <span data-ttu-id="16cb8-141">Zie voor meer informatie [inzicht in uw factuur voor Microsoft Azure](../billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="16cb8-141">For more information, see [Understand your bill for Microsoft Azure](../billing/billing-understand-your-bill.md).</span></span>

![Zie de labels in facturering](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a><span data-ttu-id="16cb8-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="16cb8-143">Next steps</span></span>
* <span data-ttu-id="16cb8-144">U kunt beperkingen en conventies met behulp van aangepaste beleidsregels toepassen voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="16cb8-144">You can apply restrictions and conventions across your subscription by using customized policies.</span></span> <span data-ttu-id="16cb8-145">Een beleid dat u definieert mogelijk dat alle resources voor een bepaald label een waarde hebben.</span><span class="sxs-lookup"><span data-stu-id="16cb8-145">A policy that you define might require that all resources have a value for a particular tag.</span></span> <span data-ttu-id="16cb8-146">Zie voor meer informatie [beleid toomanage resources gebruiken en toegangsbeheer](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="16cb8-146">For more information, see [Use policies toomanage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="16cb8-147">Zie voor een inleiding toousing Azure PowerShell gebruiken wanneer u resources implementeert, [Azure PowerShell gebruiken met Azure Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="16cb8-147">For an introduction toousing Azure PowerShell when you're deploying resources, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="16cb8-148">Zie voor een inleiding toousing hello Azure CLI gebruiken wanneer u resources implementeert, [Using hello Azure CLI voor Mac, Linux en Windows Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="16cb8-148">For an introduction toousing hello Azure CLI when you're deploying resources, see [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="16cb8-149">Zie voor een inleiding toousing Hallo-portal [Using hello Azure portal toomanage uw Azure-resources](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="16cb8-149">For an introduction toousing hello portal, see [Using hello Azure portal toomanage your Azure resources](resource-group-portal.md).</span></span>  
* <span data-ttu-id="16cb8-150">Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="16cb8-150">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

