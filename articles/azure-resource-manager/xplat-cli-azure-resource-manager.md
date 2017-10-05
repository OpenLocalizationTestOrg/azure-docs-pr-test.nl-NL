---
title: Resources beheren met de Azure CLI | Microsoft Docs
description: De Azure-opdrachtregelinterface (CLI) gebruiken voor het beheren van Azure-resources en groepen
editor: 
manager: timlt
documentationcenter: 
author: tfitzmac
services: azure-resource-manager
ms.assetid: bb0af466-4f65-4559-ac3a-43985fa096ff
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: tomfitz
ms.openlocfilehash: 3ad4e68b90979fd7f9d3ddf5278e65e19cb07152
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-cli-to-manage-azure-resources-and-resource-groups"></a><span data-ttu-id="f7ed3-103">De Azure CLI gebruiken voor het beheren van Azure-resources en resourcegroepen</span><span class="sxs-lookup"><span data-stu-id="f7ed3-103">Use the Azure CLI to manage Azure resources and resource groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f7ed3-104">Portal</span><span class="sxs-lookup"><span data-stu-id="f7ed3-104">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="f7ed3-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f7ed3-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="f7ed3-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7ed3-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="f7ed3-107">REST API</span><span class="sxs-lookup"><span data-stu-id="f7ed3-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="f7ed3-108">De Azure-opdrachtregelinterface (Azure CLI) is een van de verschillende hulpprogramma's die u gebruiken kunt om te implementeren en beheren van resources met Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-108">The Azure Command-Line Interface (Azure CLI) is one of several tools you can use to deploy and manage resources with Resource Manager.</span></span> <span data-ttu-id="f7ed3-109">Dit artikel bevat algemene manieren voor het beheren van Azure-resources en resourcegroepen met behulp van de Azure CLI in de modus Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-109">This article introduces common ways to manage Azure resources and resource groups by using the Azure CLI in Resource Manager mode.</span></span> <span data-ttu-id="f7ed3-110">Zie voor meer informatie over het implementeren van resources met de CLI [implementeren van resources met Resource Manager-sjablonen en Azure CLI](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="f7ed3-110">For information about using the CLI to deploy resources, see [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> <span data-ttu-id="f7ed3-111">Voor achtergrondinformatie over Azure-resources en Resource Manager, gaat u naar de [overzicht van Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f7ed3-111">For background about Azure resources and Resource Manager, visit the [Azure Resource Manager Overview](resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f7ed3-112">Voor het beheren van Azure-resources met de Azure CLI, moet u [Azure CLI installeren](../cli-install-nodejs.md), en [aanmelden bij Azure](../xplat-cli-connect.md) met behulp van de `azure login` opdracht.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-112">To manage Azure resources with the Azure CLI, you need to [install the Azure CLI](../cli-install-nodejs.md), and [log in to Azure](../xplat-cli-connect.md) by using the `azure login` command.</span></span> <span data-ttu-id="f7ed3-113">Controleer of de CLI in de modus Resource Manager (uitvoeren `azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="f7ed3-113">Make sure the CLI is in Resource Manager mode (run `azure config mode arm`).</span></span> <span data-ttu-id="f7ed3-114">Als u dit allemaal hebt gedaan, bent u klaar voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-114">If you've done these things, you're ready to go.</span></span>
> 
> 

## <a name="get-resource-groups-and-resources"></a><span data-ttu-id="f7ed3-115">Get-resourcegroepen en resources</span><span class="sxs-lookup"><span data-stu-id="f7ed3-115">Get resource groups and resources</span></span>
### <a name="resource-groups"></a><span data-ttu-id="f7ed3-116">Resourcegroepen</span><span class="sxs-lookup"><span data-stu-id="f7ed3-116">Resource groups</span></span>
<span data-ttu-id="f7ed3-117">Als u een lijst met alle resourcegroepen in uw abonnement en de locaties, moet u deze opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-117">To get a list of all resource groups in your subscription and their locations, run this command.</span></span>

    azure group list


### <a name="resources"></a><span data-ttu-id="f7ed3-118">Resources</span><span class="sxs-lookup"><span data-stu-id="f7ed3-118">Resources</span></span>
 <span data-ttu-id="f7ed3-119">Voor een lijst met alle bronnen in een groep, zoals een met de naam *testRG*, gebruik de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="f7ed3-119">To list all resources in a group, such as one with name *testRG*, use the following command:</span></span>

    azure resource list testRG

<span data-ttu-id="f7ed3-120">Om weer te geven van een afzonderlijke resource binnen de groep, zoals een virtuele machine met de naam *MyUbuntuVM*, een opdracht als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f7ed3-120">To view an individual resource within the group, such as a VM named *MyUbuntuVM*, use a command like the following:</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="f7ed3-121">U ziet de **Microsoft.Compute/virtualMachines** parameter.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-121">Notice the **Microsoft.Compute/virtualMachines** parameter.</span></span> <span data-ttu-id="f7ed3-122">Deze parameter geeft het type van de resource die u aanvraagt informatie op.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-122">This parameter indicates the type of the resource you are requesting information on.</span></span>

> [!NOTE]
> <span data-ttu-id="f7ed3-123">Wanneer u de **azure-resource** opdrachten anders dan de **lijst** opdracht, moet u de API-versie van de resource met de **-o** parameter.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-123">When using the **azure resource** commands other than the **list** command, you must specify the API version of the resource with the **-o** parameter.</span></span> <span data-ttu-id="f7ed3-124">Als u niet zeker weet over de API-versie, raadpleegt u het sjabloonbestand en het veld apiVersion voor de resource niet vinden.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-124">If you're unsure about the API version, consult the template file and find the apiVersion field for the resource.</span></span> <span data-ttu-id="f7ed3-125">Zie voor meer informatie over API-versies in Resource Manager [resourceproviders en typen](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="f7ed3-125">For more about API versions in Resource Manager, see [Resource providers and types](resource-manager-supported-services.md).</span></span>
> 
> 

<span data-ttu-id="f7ed3-126">Wanneer u details weergeven van een resource, is het vaak handig om te gebruiken de `--json` parameter.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-126">When viewing details on a resource, it is often useful to use the `--json` parameter.</span></span> <span data-ttu-id="f7ed3-127">Deze parameter wordt de uitvoer beter leesbaar omdat sommige waarden geneste structuren of verzamelingen zijn.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-127">This parameter makes the output more readable, because some values are nested structures, or collections.</span></span> <span data-ttu-id="f7ed3-128">Het volgende voorbeeld toont de resultaten van de **weergeven** opdracht als een JSON-document.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-128">The following example demonstrates returning the results of the **show** command as a JSON document.</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> <span data-ttu-id="f7ed3-129">Als u wilt, slaat u de JSON-gegevens naar bestand met behulp van de &gt; teken de uitvoer naar een bestand.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-129">If you want, save the JSON data to file by using the &gt; character to direct the output to a file.</span></span> <span data-ttu-id="f7ed3-130">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f7ed3-130">For example:</span></span>
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a><span data-ttu-id="f7ed3-131">Tags</span><span class="sxs-lookup"><span data-stu-id="f7ed3-131">Tags</span></span>
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a><span data-ttu-id="f7ed3-132">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="f7ed3-132">Manage resources</span></span>
<span data-ttu-id="f7ed3-133">Als u wilt een resource zoals een opslagaccount toevoegen aan een resourcegroep, een vergelijkbaar met opdracht wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="f7ed3-133">To add a resource such as a storage account to a resource group, run a command similar to:</span></span>

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

<span data-ttu-id="f7ed3-134">Naast het opgeven van de API-versie van de resource met de **-o** parameter, gebruik de **-p** parameter tekenreeks met de vereiste JSON-indeling of extra eigenschappen moeten worden doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-134">In addition to specifying the API version of the resource with the **-o** parameter, use the **-p** parameter to pass a JSON-formatted string with any required or additional properties.</span></span>

<span data-ttu-id="f7ed3-135">Voor het verwijderen van een bestaande resource, zoals de bron van een virtuele machine, moet u een opdracht als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f7ed3-135">To delete an existing resource such as a virtual machine resource, use a command like the following:</span></span>

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="f7ed3-136">U kunt bestaande resources verplaatsen naar een andere resourcegroep of abonnement met de **azure-resource verplaatsen** opdracht.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-136">To move existing resources to another resource group or subscription, use the **azure resource move** command.</span></span> <span data-ttu-id="f7ed3-137">Het volgende voorbeeld laat zien hoe een Redis-Cache verplaatsen naar een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-137">The following example shows how to move a Redis Cache to a new resource group.</span></span> <span data-ttu-id="f7ed3-138">In de **-i** parameter, Geef een door komma's gescheiden lijst van de resource-id's te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-138">In the **-i** parameter, provide a comma-separated list of the resource id's to move.</span></span>

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-to-resources"></a><span data-ttu-id="f7ed3-139">Toegang tot resources beheren</span><span class="sxs-lookup"><span data-stu-id="f7ed3-139">Control access to resources</span></span>
<span data-ttu-id="f7ed3-140">De Azure CLI kunt u beleidsregels voor het beheren van toegang tot Azure-resources maken en beheren.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-140">You can use the Azure CLI to create and manage policies to control access to Azure resources.</span></span> <span data-ttu-id="f7ed3-141">Zie voor achtergrondinformatie over beleidsregels en beleidsregels toewijzen aan resources [beleid gebruiken voor het beheren van resources en toegangsbeheer](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="f7ed3-141">For background about policy definitions and assigning policies to resources, see [Use policy to manage resources and control access](resource-manager-policy.md).</span></span>

<span data-ttu-id="f7ed3-142">Bijvoorbeeld het volgende beleid voor het weigeren van alle aanvragen waar locatie niet VS-West of Noordelijk Centraal, VS is definiëren en opslaan in het beleid definitie bestand policy.json:</span><span class="sxs-lookup"><span data-stu-id="f7ed3-142">For example, define the following policy to deny all requests where location is not West US or North Central US, and save it to the policy definition file policy.json:</span></span>

    {
    "if" : {
        "not" : {
        "field" : "location",
        "in" : ["westus" ,  "northcentralus"]
        }
    },
    "then" : {
        "effect" : "deny"
    }
    }

<span data-ttu-id="f7ed3-143">Voer vervolgens de **beleidsdefinitie maken** opdracht:</span><span class="sxs-lookup"><span data-stu-id="f7ed3-143">Then run the **policy definition create** command:</span></span>

    azure policy definition create MyPolicy -p c:\temp\policy.json

<span data-ttu-id="f7ed3-144">Deze opdracht geeft u de uitvoer ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="f7ed3-144">This command shows output similar to the following:</span></span>

    + <span data-ttu-id="f7ed3-145">Maken van de beleidsdefinitie MyPolicy gegevens: PolicyName: MyPolicy gegevens: PolicyDefinitionId: /subscriptions/###-###-###-###-###/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span><span class="sxs-lookup"><span data-stu-id="f7ed3-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span></span>

    <span data-ttu-id="f7ed3-146">gegevens: PolicyType: aangepaste gegevens: DisplayName: niet-gedefinieerde gegevens: Beschrijving: niet-gedefinieerde gegevens: PolicyRule: veld = locatie, in = [westus, northcentralus], effect = weigeren</span><span class="sxs-lookup"><span data-stu-id="f7ed3-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span></span>

 <span data-ttu-id="f7ed3-147">Als u een beleid voor het bereik dat u wilt toewijzen, gebruikt u de **PolicyDefinitionId** geretourneerd van de vorige opdracht.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-147">To assign a policy at the scope you want, use the **PolicyDefinitionId** returned from the previous command.</span></span> <span data-ttu-id="f7ed3-148">Dit bereik is het abonnement in het volgende voorbeeld, maar u kunt het bereik aan resourcegroepen of afzonderlijke resources:</span><span class="sxs-lookup"><span data-stu-id="f7ed3-148">In the following example, this scope is the subscription, but you can scope to resource groups or individual resources:</span></span>

    <span data-ttu-id="f7ed3-149">Azure beleidstoewijzing maken MyPolicyAssignment -p /subscriptions/###-###-###-###-###/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/###-###-###-###-### /</span><span class="sxs-lookup"><span data-stu-id="f7ed3-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span></span>

<span data-ttu-id="f7ed3-150">U kunt ophalen, wijzigen of beleidsdefinities verwijderen met behulp van de **beleid definitie weergeven**, **beleid definitieset**, en **beleidsdefinitie verwijderen** opdrachten.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-150">You can get, change, or remove policy definitions by using the **policy definition show**, **policy definition set**, and **policy definition delete** commands.</span></span>

<span data-ttu-id="f7ed3-151">Op dezelfde manier, u kunt ophalen, wijzigen of beleidstoewijzingen verwijderen met behulp van de **beleid toewijzing weergeven**, **beleid toewijzing set**, en **beleidstoewijzing verwijderen** opdrachten.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-151">Similarly, you can get, change, or remove policy assignments by using the **policy assignment show**, **policy assignment set**, and **policy assignment delete** commands.</span></span>

## <a name="export-a-resource-group-as-a-template"></a><span data-ttu-id="f7ed3-152">Een resourcegroep exporteren als een sjabloon</span><span class="sxs-lookup"><span data-stu-id="f7ed3-152">Export a resource group as a template</span></span>
<span data-ttu-id="f7ed3-153">U kunt de Resource Manager-sjabloon voor de resourcegroep weergeven voor een bestaande resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-153">For an existing resource group, you can view the Resource Manager template for the resource group.</span></span> <span data-ttu-id="f7ed3-154">De sjabloon exporteren biedt twee voordelen:</span><span class="sxs-lookup"><span data-stu-id="f7ed3-154">Exporting the template offers two benefits:</span></span>

1. <span data-ttu-id="f7ed3-155">Omdat de infrastructuur in de sjabloon is gedefinieerd, kunt u eenvoudig toekomstige implementaties van de oplossing automatiseren.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-155">You can easily automate future deployments of the solution because all the infrastructure is defined in the template.</span></span>
2. <span data-ttu-id="f7ed3-156">U kunt meer vertrouwd raken met de sjabloonsyntaxis van de door te kijken in de JSON die uw oplossing vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-156">You can become familiar with template syntax by looking at the JSON that represents your solution.</span></span>

<span data-ttu-id="f7ed3-157">Met de Azure CLI, kunt u een sjabloon met de huidige status van de resourcegroep exporteren of downloaden van de sjabloon die is gebruikt voor een bepaalde implementatie.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-157">Using the Azure CLI, you can either export a template that represents the current state of your resource group, or download the template that was used for a particular deployment.</span></span>

* <span data-ttu-id="f7ed3-158">**De sjabloon voor een resourcegroep exporteren** -dit is handig wanneer u wijzigingen aan een resourcegroep aangebracht en moet de JSON-weergave van de huidige status ophalen.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-158">**Export the template for a resource group** - This is helpful when you made changes to a resource group, and need to retrieve the JSON representation of its current state.</span></span> <span data-ttu-id="f7ed3-159">De gegenereerde sjabloon bevat echter alleen een minimum aantal parameters en geen variabelen.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-159">However, the generated template contains only a minimal number of parameters and no variables.</span></span> <span data-ttu-id="f7ed3-160">De meeste van de waarden in de sjabloon zijn vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-160">Most of the values in the template are hard-coded.</span></span> <span data-ttu-id="f7ed3-161">Voordat u de gegenereerde sjabloon implementeert, wilt u mogelijk meer van de waarden converteren naar parameters, zodat u de implementatie voor verschillende omgevingen kan aanpassen.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-161">Before deploying the generated template, you may wish to convert more of the values into parameters so you can customize the deployment for different environments.</span></span>
  
    <span data-ttu-id="f7ed3-162">Uitvoeren als u wilt de sjabloon voor een resourcegroep exporteren naar een lokale map, de `azure group export` opdracht zoals weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-162">To export the template for a resource group to a local directory, run the `azure group export` command as shown in the following example.</span></span> <span data-ttu-id="f7ed3-163">(Vervangen door een lokale map voor uw omgeving van het besturingssysteem.)</span><span class="sxs-lookup"><span data-stu-id="f7ed3-163">(Substitute a local directory appropriate for your operating system environment.)</span></span>
  
        azure group export testRG ~/azure/templates/
* <span data-ttu-id="f7ed3-164">**Download de sjabloon voor een bepaalde implementatie** --dit is handig als u weergeven van de werkelijke sjabloon die is gebruikt wilt voor het implementeren van resources.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-164">**Download the template for a particular deployment** -- This is helpful when you need to view the actual template that was used to deploy resources.</span></span> <span data-ttu-id="f7ed3-165">De sjabloon bevat alle parameters en variabelen die zijn gedefinieerd voor de oorspronkelijke implementatie.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-165">The template includes all parameters and variables defined for the original deployment.</span></span> <span data-ttu-id="f7ed3-166">Als iemand zich in uw organisatie wijzigingen in de resourcegroep buiten de definitie van de sjabloon aangebracht, vertegenwoordigen niet met deze sjabloon echter in de huidige status van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-166">However, if someone in your organization made changes to the resource group outside of the definition in the template, this template doesn't represent the current state of the resource group.</span></span>
  
    <span data-ttu-id="f7ed3-167">Voor het downloaden van de sjabloon voor een bepaalde implementatie naar een lokale map gebruikt, voer de `azure group deployment template download` opdracht.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-167">To download the template used for a particular deployment to a local directory, run the `azure group deployment template download` command.</span></span> <span data-ttu-id="f7ed3-168">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f7ed3-168">For example:</span></span>
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> <span data-ttu-id="f7ed3-169">Exporteren van de sjabloon is een Preview-versie en niet alle brontypen die momenteel ondersteuning voor het exporteren van een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-169">Template export is in preview, and not all resource types currently support exporting a template.</span></span> <span data-ttu-id="f7ed3-170">Wanneer u probeert om een sjabloon te exporteren, wordt er een fout die aangeeft dat sommige resources zijn niet geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-170">When attempting to export a template, you may see an error that states some resources were not exported.</span></span> <span data-ttu-id="f7ed3-171">Indien nodig, handmatig definiëren van deze resources in uw sjabloon nadat deze is gedownload.</span><span class="sxs-lookup"><span data-stu-id="f7ed3-171">If needed, manually define these resources in your template after downloading it.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f7ed3-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f7ed3-172">Next steps</span></span>
* <span data-ttu-id="f7ed3-173">U kunt details van implementatiebewerkingen ophalen en implementatie fouten met de Azure CLI, Zie [implementatiebewerkingen weergeven](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="f7ed3-173">To get details of deployment operations and troubleshoot deployment errors with the Azure CLI, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="f7ed3-174">Als u de CLI gebruik wilt voor het instellen van een toepassing of het script voor toegang tot bronnen, Zie [Azure CLI gebruiken voor het maken van een service-principal voor toegang tot bronnen](resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="f7ed3-174">If you want to use the CLI to set up an application or script to access resources, see [Use Azure CLI to create a service principal to access resources](resource-group-authenticate-service-principal-cli.md).</span></span>
* <span data-ttu-id="f7ed3-175">Voor begeleiding bij de manier waarop ondernemingen Resource Manager effectief kunnen gebruiken voor het beheer van abonnementen, gaat u naar [Azure enterprise-platform - Prescriptieve abonnementsgovernance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="f7ed3-175">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

