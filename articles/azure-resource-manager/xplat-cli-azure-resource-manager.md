---
title: aaaManage resources met hello Azure CLI | Microsoft Docs
description: Gebruik hello Azure-opdrachtregelinterface (CLI) toomanage Azure resources en groepen
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
ms.openlocfilehash: 3df70e123d14d3bbf2648c71970bac1db4afc025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cli-toomanage-azure-resources-and-resource-groups"></a><span data-ttu-id="ce696-103">Gebruik hello Azure CLI toomanage Azure resources en resourcegroepen</span><span class="sxs-lookup"><span data-stu-id="ce696-103">Use hello Azure CLI toomanage Azure resources and resource groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ce696-104">Portal</span><span class="sxs-lookup"><span data-stu-id="ce696-104">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="ce696-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ce696-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="ce696-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ce696-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="ce696-107">REST API</span><span class="sxs-lookup"><span data-stu-id="ce696-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="ce696-108">Hello Azure-opdrachtregelinterface (Azure CLI) is een van verschillende hulpprogramma's kunt u toodeploy gebruiken en beheren van resources met Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ce696-108">hello Azure Command-Line Interface (Azure CLI) is one of several tools you can use toodeploy and manage resources with Resource Manager.</span></span> <span data-ttu-id="ce696-109">Dit artikel bevat algemene manieren toomanage Azure resources en resourcegroepen met behulp van Azure CLI Hallo in de modus Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ce696-109">This article introduces common ways toomanage Azure resources and resource groups by using hello Azure CLI in Resource Manager mode.</span></span> <span data-ttu-id="ce696-110">Zie voor meer informatie over het gebruik van Hallo CLI toodeploy resources [implementeren van resources met Resource Manager-sjablonen en Azure CLI](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ce696-110">For information about using hello CLI toodeploy resources, see [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> <span data-ttu-id="ce696-111">Voor achtergrondinformatie over Azure-resources en Resource Manager, gaat u naar Hallo [overzicht van Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ce696-111">For background about Azure resources and Resource Manager, visit hello [Azure Resource Manager Overview](resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ce696-112">toomanage Azure resources Hello Azure CLI, hoeft te[hello Azure CLI installeren](../cli-install-nodejs.md), en [aanmelden tooAzure](../xplat-cli-connect.md) met behulp van Hallo `azure login` opdracht.</span><span class="sxs-lookup"><span data-stu-id="ce696-112">toomanage Azure resources with hello Azure CLI, you need too[install hello Azure CLI](../cli-install-nodejs.md), and [log in tooAzure](../xplat-cli-connect.md) by using hello `azure login` command.</span></span> <span data-ttu-id="ce696-113">Zorg ervoor dat Hallo CLI bevindt zich in de modus Resource Manager (uitvoeren `azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="ce696-113">Make sure hello CLI is in Resource Manager mode (run `azure config mode arm`).</span></span> <span data-ttu-id="ce696-114">Als u dit allemaal hebt gedaan, bent u klaar toogo.</span><span class="sxs-lookup"><span data-stu-id="ce696-114">If you've done these things, you're ready toogo.</span></span>
> 
> 

## <a name="get-resource-groups-and-resources"></a><span data-ttu-id="ce696-115">Get-resourcegroepen en resources</span><span class="sxs-lookup"><span data-stu-id="ce696-115">Get resource groups and resources</span></span>
### <a name="resource-groups"></a><span data-ttu-id="ce696-116">Resourcegroepen</span><span class="sxs-lookup"><span data-stu-id="ce696-116">Resource groups</span></span>
<span data-ttu-id="ce696-117">een lijst met alle resourcegroepen in uw abonnement en de locaties tooget deze opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ce696-117">tooget a list of all resource groups in your subscription and their locations, run this command.</span></span>

    azure group list


### <a name="resources"></a><span data-ttu-id="ce696-118">Resources</span><span class="sxs-lookup"><span data-stu-id="ce696-118">Resources</span></span>
 <span data-ttu-id="ce696-119">alle resources in een groep, zoals een met een naam toolist *testRG*, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="ce696-119">toolist all resources in a group, such as one with name *testRG*, use hello following command:</span></span>

    azure resource list testRG

<span data-ttu-id="ce696-120">een afzonderlijke bron binnen Hallo-groep, zoals een virtuele machine met de naam tooview *MyUbuntuVM*, een opdracht zoals Hallo volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="ce696-120">tooview an individual resource within hello group, such as a VM named *MyUbuntuVM*, use a command like hello following:</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="ce696-121">Kennisgeving Hallo **Microsoft.Compute/virtualMachines** parameter.</span><span class="sxs-lookup"><span data-stu-id="ce696-121">Notice hello **Microsoft.Compute/virtualMachines** parameter.</span></span> <span data-ttu-id="ce696-122">Deze parameter geeft Hallo type Hallo resource aangevraagde informatie op.</span><span class="sxs-lookup"><span data-stu-id="ce696-122">This parameter indicates hello type of hello resource you are requesting information on.</span></span>

> [!NOTE]
> <span data-ttu-id="ce696-123">Wanneer u Hallo **azure-resource** opdrachten dan Hallo **lijst** uitvoert, moet u Hallo API-versie van Hallo resource Hello **-o** parameter.</span><span class="sxs-lookup"><span data-stu-id="ce696-123">When using hello **azure resource** commands other than hello **list** command, you must specify hello API version of hello resource with hello **-o** parameter.</span></span> <span data-ttu-id="ce696-124">Als u niet zeker weet over Hallo API-versie, raadpleegt u het sjabloonbestand Hallo en Hallo apiVersion veld vinden voor Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="ce696-124">If you're unsure about hello API version, consult hello template file and find hello apiVersion field for hello resource.</span></span> <span data-ttu-id="ce696-125">Zie voor meer informatie over API-versies in Resource Manager [resourceproviders en typen](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="ce696-125">For more about API versions in Resource Manager, see [Resource providers and types](resource-manager-supported-services.md).</span></span>
> 
> 

<span data-ttu-id="ce696-126">Wanneer ze informatie van een resource, is het vaak nuttig toouse hello `--json` parameter.</span><span class="sxs-lookup"><span data-stu-id="ce696-126">When viewing details on a resource, it is often useful toouse hello `--json` parameter.</span></span> <span data-ttu-id="ce696-127">Deze parameter maakt Hallo uitvoer beter leesbaar omdat sommige waarden geneste structuren of verzamelingen zijn.</span><span class="sxs-lookup"><span data-stu-id="ce696-127">This parameter makes hello output more readable, because some values are nested structures, or collections.</span></span> <span data-ttu-id="ce696-128">Hallo volgende voorbeeld toont terugkerende Hallo resultaten van Hallo **weergeven** opdracht als een JSON-document.</span><span class="sxs-lookup"><span data-stu-id="ce696-128">hello following example demonstrates returning hello results of hello **show** command as a JSON document.</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> <span data-ttu-id="ce696-129">Als u wilt, sla Hallo JSON gegevens toofile met behulp van Hallo &gt; teken toodirect Hallo-uitvoerbestand tooa.</span><span class="sxs-lookup"><span data-stu-id="ce696-129">If you want, save hello JSON data toofile by using hello &gt; character toodirect hello output tooa file.</span></span> <span data-ttu-id="ce696-130">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ce696-130">For example:</span></span>
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a><span data-ttu-id="ce696-131">Tags</span><span class="sxs-lookup"><span data-stu-id="ce696-131">Tags</span></span>
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a><span data-ttu-id="ce696-132">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="ce696-132">Manage resources</span></span>
<span data-ttu-id="ce696-133">een resource, zoals een resourcegroep storage account tooa tooadd een vergelijkbaar met opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ce696-133">tooadd a resource such as a storage account tooa resource group, run a command similar to:</span></span>

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

<span data-ttu-id="ce696-134">Bovendien toospecifying API-versie van de resource Hallo Hallo Hello **-o** parameter, gebruik Hallo **-p** parameter toopass JSON-indeling tekenreeks met de vereiste of aanvullende eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="ce696-134">In addition toospecifying hello API version of hello resource with hello **-o** parameter, use hello **-p** parameter toopass a JSON-formatted string with any required or additional properties.</span></span>

<span data-ttu-id="ce696-135">toodelete een bestaande resource, zoals de bron van een virtuele machine, een opdracht zoals Hallo volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="ce696-135">toodelete an existing resource such as a virtual machine resource, use a command like hello following:</span></span>

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="ce696-136">toomove bestaande resources tooanother resourcegroep of abonnement, gebruikt u Hallo **azure-resource verplaatsen** opdracht.</span><span class="sxs-lookup"><span data-stu-id="ce696-136">toomove existing resources tooanother resource group or subscription, use hello **azure resource move** command.</span></span> <span data-ttu-id="ce696-137">Hallo volgende voorbeeld wordt getoond hoe toomove een Redis-Cache tooa nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="ce696-137">hello following example shows how toomove a Redis Cache tooa new resource group.</span></span> <span data-ttu-id="ce696-138">In Hallo **-i** parameter, Geef een door komma's gescheiden lijst met Hallo resource id toomove.</span><span class="sxs-lookup"><span data-stu-id="ce696-138">In hello **-i** parameter, provide a comma-separated list of hello resource id's toomove.</span></span>

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-tooresources"></a><span data-ttu-id="ce696-139">Beheer toegang tooresources</span><span class="sxs-lookup"><span data-stu-id="ce696-139">Control access tooresources</span></span>
<span data-ttu-id="ce696-140">U kunt gebruiken hello Azure CLI toocreate en beleidsregels toocontrol toegang tooAzure resources beheren.</span><span class="sxs-lookup"><span data-stu-id="ce696-140">You can use hello Azure CLI toocreate and manage policies toocontrol access tooAzure resources.</span></span> <span data-ttu-id="ce696-141">Zie voor achtergrondinformatie over beleidsdefinities en toewijzen beleid tooresources [beleid toomanage resources gebruiken en toegangsbeheer](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="ce696-141">For background about policy definitions and assigning policies tooresources, see [Use policy toomanage resources and control access](resource-manager-policy.md).</span></span>

<span data-ttu-id="ce696-142">Bijvoorbeeld Hallo beleid toodeny na alle aanvragen waar locatie niet VS-West of Noordelijk Centraal, VS is definiëren en sla het bestand policy.json van toohello beleid definitie:</span><span class="sxs-lookup"><span data-stu-id="ce696-142">For example, define hello following policy toodeny all requests where location is not West US or North Central US, and save it toohello policy definition file policy.json:</span></span>

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

<span data-ttu-id="ce696-143">Voer Hallo **beleidsdefinitie maken** opdracht:</span><span class="sxs-lookup"><span data-stu-id="ce696-143">Then run hello **policy definition create** command:</span></span>

    azure policy definition create MyPolicy -p c:\temp\policy.json

<span data-ttu-id="ce696-144">Deze opdracht geeft de vergelijkbare toohello volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="ce696-144">This command shows output similar toohello following:</span></span>

    + <span data-ttu-id="ce696-145">Maken van de beleidsdefinitie MyPolicy gegevens: PolicyName: MyPolicy gegevens: PolicyDefinitionId: /subscriptions/###-###-###-###-###/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span><span class="sxs-lookup"><span data-stu-id="ce696-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span></span>

    <span data-ttu-id="ce696-146">gegevens: PolicyType: aangepaste gegevens: DisplayName: niet-gedefinieerde gegevens: Beschrijving: niet-gedefinieerde gegevens: PolicyRule: veld = locatie, in = [westus, northcentralus], effect = weigeren</span><span class="sxs-lookup"><span data-stu-id="ce696-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span></span>

 <span data-ttu-id="ce696-147">een beleid voor het Hallo bereik u wilt, gebruik Hallo tooassign **PolicyDefinitionId** geretourneerd van de vorige opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="ce696-147">tooassign a policy at hello scope you want, use hello **PolicyDefinitionId** returned from hello previous command.</span></span> <span data-ttu-id="ce696-148">In Hallo voorbeeld te volgen, is dit bereik Hallo abonnement, maar u kunt het bereik tooresource groepen of afzonderlijke resources:</span><span class="sxs-lookup"><span data-stu-id="ce696-148">In hello following example, this scope is hello subscription, but you can scope tooresource groups or individual resources:</span></span>

    <span data-ttu-id="ce696-149">Azure beleidstoewijzing maken MyPolicyAssignment -p /subscriptions/###-###-###-###-###/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/###-###-###-###-### /</span><span class="sxs-lookup"><span data-stu-id="ce696-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span></span>

<span data-ttu-id="ce696-150">Ophalen, wijzigen of beleidsdefinities verwijderen met behulp van Hallo **beleid definitie weergeven**, **beleid definitieset**, en **beleidsdefinitie verwijderen** opdrachten.</span><span class="sxs-lookup"><span data-stu-id="ce696-150">You can get, change, or remove policy definitions by using hello **policy definition show**, **policy definition set**, and **policy definition delete** commands.</span></span>

<span data-ttu-id="ce696-151">Op dezelfde manier, u kunt ophalen, wijzigen of beleidstoewijzingen verwijderen met behulp van Hallo **beleid toewijzing weergeven**, **beleid toewijzing set**, en **beleidstoewijzing verwijderen** opdrachten .</span><span class="sxs-lookup"><span data-stu-id="ce696-151">Similarly, you can get, change, or remove policy assignments by using hello **policy assignment show**, **policy assignment set**, and **policy assignment delete** commands.</span></span>

## <a name="export-a-resource-group-as-a-template"></a><span data-ttu-id="ce696-152">Een resourcegroep exporteren als een sjabloon</span><span class="sxs-lookup"><span data-stu-id="ce696-152">Export a resource group as a template</span></span>
<span data-ttu-id="ce696-153">U kunt Hallo Resource Manager-sjabloon voor de resourcegroep Hallo weergeven voor een bestaande resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="ce696-153">For an existing resource group, you can view hello Resource Manager template for hello resource group.</span></span> <span data-ttu-id="ce696-154">Uitvoer Hallo sjabloon biedt twee voordelen:</span><span class="sxs-lookup"><span data-stu-id="ce696-154">Exporting hello template offers two benefits:</span></span>

1. <span data-ttu-id="ce696-155">Omdat alle Hallo-infrastructuur in Hallo-sjabloon is gedefinieerd, kunt u eenvoudig toekomstige implementaties van Hallo oplossing automatiseren.</span><span class="sxs-lookup"><span data-stu-id="ce696-155">You can easily automate future deployments of hello solution because all hello infrastructure is defined in hello template.</span></span>
2. <span data-ttu-id="ce696-156">U kunt meer vertrouwd raken met de sjabloonsyntaxis van de door te kijken Hallo JSON dat uw oplossing vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="ce696-156">You can become familiar with template syntax by looking at hello JSON that represents your solution.</span></span>

<span data-ttu-id="ce696-157">Met behulp van hello Azure CLI, kunt u exporteren van een sjabloon waarmee de huidige status van de resourcegroep Hallo of Hallo-sjabloon die is gebruikt voor een bepaalde implementatie downloaden.</span><span class="sxs-lookup"><span data-stu-id="ce696-157">Using hello Azure CLI, you can either export a template that represents hello current state of your resource group, or download hello template that was used for a particular deployment.</span></span>

* <span data-ttu-id="ce696-158">**Exporteer de sjabloon voor een resourcegroep Hallo** -dit is handig wanneer u wijzigingen tooa resourcegroep hebt gemaakt en moet tooretrieve Hallo JSON-weergave van de huidige status.</span><span class="sxs-lookup"><span data-stu-id="ce696-158">**Export hello template for a resource group** - This is helpful when you made changes tooa resource group, and need tooretrieve hello JSON representation of its current state.</span></span> <span data-ttu-id="ce696-159">Deze gegenereerde sjabloon Hallo bevat echter alleen een minimum aantal parameters en geen variabelen.</span><span class="sxs-lookup"><span data-stu-id="ce696-159">However, hello generated template contains only a minimal number of parameters and no variables.</span></span> <span data-ttu-id="ce696-160">De meeste van waarden in de sjabloon Hallo Hallo zijn vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="ce696-160">Most of hello values in hello template are hard-coded.</span></span> <span data-ttu-id="ce696-161">Voordat u implementeert Hallo gegenereerd sjabloon, kunt u desgewenst tooconvert meer van de waarden Hallo parameters zodat u Hallo-implementatie voor verschillende omgevingen kan aanpassen.</span><span class="sxs-lookup"><span data-stu-id="ce696-161">Before deploying hello generated template, you may wish tooconvert more of hello values into parameters so you can customize hello deployment for different environments.</span></span>
  
    <span data-ttu-id="ce696-162">tooexport hello sjabloon voor een resource groep tooa lokale map uitvoeren Hallo `azure group export` zoals weergegeven in het volgende voorbeeld Hallo opdracht.</span><span class="sxs-lookup"><span data-stu-id="ce696-162">tooexport hello template for a resource group tooa local directory, run hello `azure group export` command as shown in hello following example.</span></span> <span data-ttu-id="ce696-163">(Vervangen door een lokale map voor uw omgeving van het besturingssysteem.)</span><span class="sxs-lookup"><span data-stu-id="ce696-163">(Substitute a local directory appropriate for your operating system environment.)</span></span>
  
        azure group export testRG ~/azure/templates/
* <span data-ttu-id="ce696-164">**Hallo-sjabloon voor een bepaalde implementatie downloaden** --dit is handig wanneer u tooview Hallo werkelijke sjabloon die gebruikt toodeploy bronnen is nodig.</span><span class="sxs-lookup"><span data-stu-id="ce696-164">**Download hello template for a particular deployment** -- This is helpful when you need tooview hello actual template that was used toodeploy resources.</span></span> <span data-ttu-id="ce696-165">Hallo-sjabloon bevat alle parameters en variabelen die zijn gedefinieerd voor de oorspronkelijke implementatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="ce696-165">hello template includes all parameters and variables defined for hello original deployment.</span></span> <span data-ttu-id="ce696-166">Als iemand in uw organisatie wijzigingen toohello resourcegroep buiten Hallo definitie in Hallo sjabloon hebt gemaakt, vertegenwoordigen niet met deze sjabloon echter Hallo huidige status van de resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="ce696-166">However, if someone in your organization made changes toohello resource group outside of hello definition in hello template, this template doesn't represent hello current state of hello resource group.</span></span>
  
    <span data-ttu-id="ce696-167">toodownload Hallo-sjabloon die wordt gebruikt voor een bepaalde implementatie tooa lokale map uitvoeren Hallo `azure group deployment template download` opdracht.</span><span class="sxs-lookup"><span data-stu-id="ce696-167">toodownload hello template used for a particular deployment tooa local directory, run hello `azure group deployment template download` command.</span></span> <span data-ttu-id="ce696-168">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ce696-168">For example:</span></span>
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> <span data-ttu-id="ce696-169">Exporteren van de sjabloon is een Preview-versie en niet alle brontypen die momenteel ondersteuning voor het exporteren van een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="ce696-169">Template export is in preview, and not all resource types currently support exporting a template.</span></span> <span data-ttu-id="ce696-170">Wanneer u probeert een sjabloon tooexport, wordt er een fout die aangeeft dat sommige resources zijn niet geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="ce696-170">When attempting tooexport a template, you may see an error that states some resources were not exported.</span></span> <span data-ttu-id="ce696-171">Indien nodig, handmatig definiëren van deze resources in uw sjabloon nadat deze is gedownload.</span><span class="sxs-lookup"><span data-stu-id="ce696-171">If needed, manually define these resources in your template after downloading it.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ce696-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ce696-172">Next steps</span></span>
* <span data-ttu-id="ce696-173">details van implementatiebewerkingen tooget en implementatiefouten Hello Azure CLI oplossen, raadpleegt [implementatiebewerkingen weergeven](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="ce696-173">tooget details of deployment operations and troubleshoot deployment errors with hello Azure CLI, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="ce696-174">Als u toouse Hallo CLI tooset van een toepassing of script tooaccess bronnen wilt, Zie [gebruik Azure CLI toocreate een service-principal tooaccess resources](resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ce696-174">If you want toouse hello CLI tooset up an application or script tooaccess resources, see [Use Azure CLI toocreate a service principal tooaccess resources](resource-group-authenticate-service-principal-cli.md).</span></span>
* <span data-ttu-id="ce696-175">Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="ce696-175">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

