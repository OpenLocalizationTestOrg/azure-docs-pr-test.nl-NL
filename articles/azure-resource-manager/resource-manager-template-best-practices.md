---
title: aaaBest procedures voor het maken van Resource Manager-sjablonen | Microsoft Docs
description: Richtlijnen voor het vereenvoudigen van uw Azure Resource Manager-sjablonen.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 31b10deb-0183-47ce-a5ba-6d0ff2ae8ab3
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: tomfitz
ms.openlocfilehash: ec9bbe218c4f2c6a92ca44b5e9c9c71029e22151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a><span data-ttu-id="9bac2-103">Aanbevolen procedures voor het maken van Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="9bac2-103">Best practices for creating Azure Resource Manager templates</span></span>
<span data-ttu-id="9bac2-104">Deze richtlijnen kunt u Azure Resource Manager-sjablonen die betrouwbare en eenvoudige toouse zijn maken.</span><span class="sxs-lookup"><span data-stu-id="9bac2-104">These guidelines can help you create Azure Resource Manager templates that are reliable and easy toouse.</span></span> <span data-ttu-id="9bac2-105">Hallo richtlijnen zijn alleen suggesties.</span><span class="sxs-lookup"><span data-stu-id="9bac2-105">hello guidelines are only suggestions.</span></span> <span data-ttu-id="9bac2-106">Ze zijn geen vereisten, tenzij anders wordt vermeld.</span><span class="sxs-lookup"><span data-stu-id="9bac2-106">They are not requirements, except where noted.</span></span> <span data-ttu-id="9bac2-107">Uw scenario mogelijk een variant van een van de Hallo wijze van aanpak of voorbeelden te volgen.</span><span class="sxs-lookup"><span data-stu-id="9bac2-107">Your scenario might require a variation of one of hello following approaches or examples.</span></span>

## <a name="resource-names"></a><span data-ttu-id="9bac2-108">Resourcenamen</span><span class="sxs-lookup"><span data-stu-id="9bac2-108">Resource names</span></span>
<span data-ttu-id="9bac2-109">In het algemeen werken u met drie soorten resourcenamen in Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="9bac2-109">Generally, you work with three types of resource names in Resource Manager:</span></span>

* <span data-ttu-id="9bac2-110">Resourcenamen moeten uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="9bac2-110">Resource names that must be unique.</span></span>
* <span data-ttu-id="9bac2-111">Resourcenamen die geen unieke toobe vereist, maar u een naam waarmee u kunt een resource op basis van de context waarin tooprovide kiezen.</span><span class="sxs-lookup"><span data-stu-id="9bac2-111">Resource names that are not required toobe unique, but you choose tooprovide a name that can help you identify a resource based on context.</span></span>
* <span data-ttu-id="9bac2-112">Resourcenamen kunnen niet algemeen zijn.</span><span class="sxs-lookup"><span data-stu-id="9bac2-112">Resource names that can be generic.</span></span>

 <span data-ttu-id="9bac2-113">Zie voor meer informatie over de beperkingen voor resource [aanbevolen naamgevingsregels voor Azure-resources](../guidance/guidance-naming-conventions.md).</span><span class="sxs-lookup"><span data-stu-id="9bac2-113">For information about resource name restrictions, see [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md).</span></span>

### <a name="unique-resource-names"></a><span data-ttu-id="9bac2-114">Unieke resourcenamen</span><span class="sxs-lookup"><span data-stu-id="9bac2-114">Unique resource names</span></span>
<span data-ttu-id="9bac2-115">U moet een unieke bronnaam voor resourcetype dat een data access-eindpunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="9bac2-115">You must provide a unique resource name for any resource type that has a data access endpoint.</span></span> <span data-ttu-id="9bac2-116">Sommige algemene brontypen waarvoor een unieke naam zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="9bac2-116">Some common resource types that require a unique name include:</span></span>

* <span data-ttu-id="9bac2-117">Azure Storage<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="9bac2-117">Azure Storage<sup>1</sup></span></span> 
* <span data-ttu-id="9bac2-118">Web Apps-functie van Azure App Service</span><span class="sxs-lookup"><span data-stu-id="9bac2-118">Web Apps feature of Azure App Service</span></span>
* <span data-ttu-id="9bac2-119">SQL Server</span><span class="sxs-lookup"><span data-stu-id="9bac2-119">SQL Server</span></span>
* <span data-ttu-id="9bac2-120">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="9bac2-120">Azure Key Vault</span></span>
* <span data-ttu-id="9bac2-121">Azure Redis-cache</span><span class="sxs-lookup"><span data-stu-id="9bac2-121">Azure Redis Cache</span></span>
* <span data-ttu-id="9bac2-122">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="9bac2-122">Azure Batch</span></span>
* <span data-ttu-id="9bac2-123">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="9bac2-123">Azure Traffic Manager</span></span>
* <span data-ttu-id="9bac2-124">Azure Search</span><span class="sxs-lookup"><span data-stu-id="9bac2-124">Azure Search</span></span>
* <span data-ttu-id="9bac2-125">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="9bac2-125">Azure HDInsight</span></span>

<span data-ttu-id="9bac2-126"><sup>1</sup> opslagaccountnamen ook moet een kleine letter, 24 tekens of korter is, en geen eventuele verbindingsstreepjes.</span><span class="sxs-lookup"><span data-stu-id="9bac2-126"><sup>1</sup> Storage account names also must be lowercase, 24 characters or less, and not have any hyphens.</span></span>

<span data-ttu-id="9bac2-127">Als u een parameter voor een resourcenaam opgeeft, moet u een unieke naam opgeven bij het implementeren van Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="9bac2-127">If you provide a parameter for a resource name, you must provide a unique name when you deploy hello resource.</span></span> <span data-ttu-id="9bac2-128">Desgewenst kunt u een variabele die gebruikmaakt van Hallo [uniqueString()](resource-group-template-functions-string.md#uniquestring) toogenerate naam van een functie.</span><span class="sxs-lookup"><span data-stu-id="9bac2-128">Optionally, you can create a variable that uses hello [uniqueString()](resource-group-template-functions-string.md#uniquestring) function toogenerate a name.</span></span> 

<span data-ttu-id="9bac2-129">Ook kunt of wilt u een voorvoegsel tooadd achtervoegsel toohello **uniqueString** resultaat.</span><span class="sxs-lookup"><span data-stu-id="9bac2-129">You also might want tooadd a prefix or suffix toohello **uniqueString** result.</span></span> <span data-ttu-id="9bac2-130">Wijzigen Hallo unieke naam kunt u gemakkelijk herkennen Hallo brontype van Hallo-naam.</span><span class="sxs-lookup"><span data-stu-id="9bac2-130">Modifying hello unique name can help you more easily identify hello resource type from hello name.</span></span> <span data-ttu-id="9bac2-131">U kunt bijvoorbeeld een unieke naam voor een opslagaccount genereren met behulp van de volgende variabele Hallo:</span><span class="sxs-lookup"><span data-stu-id="9bac2-131">For example, you can generate a unique name for a storage account by using hello following variable:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a><span data-ttu-id="9bac2-132">Resourcenamen voor identificatie</span><span class="sxs-lookup"><span data-stu-id="9bac2-132">Resource names for identification</span></span>
<span data-ttu-id="9bac2-133">Sommige brontypen kunt u tooname, maar hun namen hebben geen unieke toobe.</span><span class="sxs-lookup"><span data-stu-id="9bac2-133">Some resource types you might want tooname, but their names do not have toobe unique.</span></span> <span data-ttu-id="9bac2-134">U kunt een naam waarmee zowel Hallo resource context en het resourcetype Hallo opgeven voor deze resourcetypen.</span><span class="sxs-lookup"><span data-stu-id="9bac2-134">For these resource types, you can provide a name that identifies both hello resource context and hello resource type.</span></span> <span data-ttu-id="9bac2-135">Geef een beschrijvende naam die helpt u identificeren Hallo-bron in een lijst met bronnen.</span><span class="sxs-lookup"><span data-stu-id="9bac2-135">Provide a descriptive name that helps you identify hello resource in a list of resources.</span></span> <span data-ttu-id="9bac2-136">Als u de naam van een andere bron voor verschillende implementaties toouse moet, kunt u een parameter voor de naam van de Hallo:</span><span class="sxs-lookup"><span data-stu-id="9bac2-136">If you need toouse a different resource name for different deployments, you can use a parameter for hello name:</span></span>

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "hello name of hello VM toocreate."
        }
    }
}
```

<span data-ttu-id="9bac2-137">Als u niet toopass in een naam tijdens de implementatie hoeft, kunt u een variabele gebruiken:</span><span class="sxs-lookup"><span data-stu-id="9bac2-137">If you do not need toopass in a name during deployment, you can use a variable:</span></span> 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

<span data-ttu-id="9bac2-138">U kunt ook een waarde vastgelegde gebruiken:</span><span class="sxs-lookup"><span data-stu-id="9bac2-138">You also can use a hard-coded value:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a><span data-ttu-id="9bac2-139">Algemene resourcenamen</span><span class="sxs-lookup"><span data-stu-id="9bac2-139">Generic resource names</span></span>
<span data-ttu-id="9bac2-140">Voor brontypen die u voornamelijk via een andere resource benaderen, kunt u een algemene naam die is vastgelegd in Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="9bac2-140">For resource types that you mostly access through a different resource, you can use a generic name that is hard-coded in hello template.</span></span> <span data-ttu-id="9bac2-141">U kunt bijvoorbeeld een algemene naam op voor firewallregels instellen op een SQL server:</span><span class="sxs-lookup"><span data-stu-id="9bac2-141">For example, you can set a standard, generic name for firewall rules on a SQL server:</span></span>

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a><span data-ttu-id="9bac2-142">Parameters</span><span class="sxs-lookup"><span data-stu-id="9bac2-142">Parameters</span></span>
<span data-ttu-id="9bac2-143">Hallo kan volgende informatie nuttig zijn wanneer u met parameters werkt:</span><span class="sxs-lookup"><span data-stu-id="9bac2-143">hello following information can be helpful when you work with parameters:</span></span>

* <span data-ttu-id="9bac2-144">Beperk het gebruik van parameters.</span><span class="sxs-lookup"><span data-stu-id="9bac2-144">Minimize your use of parameters.</span></span> <span data-ttu-id="9bac2-145">Gebruik indien mogelijk een variabele of een letterlijke waarde.</span><span class="sxs-lookup"><span data-stu-id="9bac2-145">Whenever possible, use a variable or a literal value.</span></span> <span data-ttu-id="9bac2-146">Parameters gebruiken om alleen voor deze scenario's:</span><span class="sxs-lookup"><span data-stu-id="9bac2-146">Use parameters only for these scenarios:</span></span>
   
   * <span data-ttu-id="9bac2-147">De instellingen die u wilt dat toouse variaties volgens tooenvironment (SKU, grootte, capaciteit).</span><span class="sxs-lookup"><span data-stu-id="9bac2-147">Settings that you want toouse variations of according tooenvironment (SKU, size, capacity).</span></span>
   * <span data-ttu-id="9bac2-148">Resourcenamen wilt u toospecify voor eenvoudige identificatie.</span><span class="sxs-lookup"><span data-stu-id="9bac2-148">Resource names that you want toospecify for easy identification.</span></span>
   * <span data-ttu-id="9bac2-149">De waarden die u vaak toocomplete andere taken (zoals een beheerdersgebruikersnaam gebruikt).</span><span class="sxs-lookup"><span data-stu-id="9bac2-149">Values that you use frequently toocomplete other tasks (such as an admin user name).</span></span>
   * <span data-ttu-id="9bac2-150">Geheimen (zoals wachtwoorden).</span><span class="sxs-lookup"><span data-stu-id="9bac2-150">Secrets (such as passwords).</span></span>
   * <span data-ttu-id="9bac2-151">Hallo getal of matrix met waarden toouse wanneer u meerdere exemplaren van een resourcetype maakt.</span><span class="sxs-lookup"><span data-stu-id="9bac2-151">hello number or array of values toouse when you create multiple instances of a resource type.</span></span>
* <span data-ttu-id="9bac2-152">Gebruik kamelen voor namen van parameters.</span><span class="sxs-lookup"><span data-stu-id="9bac2-152">Use camel case for parameter names.</span></span>
* <span data-ttu-id="9bac2-153">Geef een beschrijving van elke parameter in metagegevens Hallo:</span><span class="sxs-lookup"><span data-stu-id="9bac2-153">Provide a description of every parameter in hello metadata:</span></span>

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "hello type of hello new storage account created toostore hello VM disks."
           }
       }
   }
   ```

* <span data-ttu-id="9bac2-154">Definieer de standaardwaarden voor parameters (met uitzondering van wachtwoorden en SSH-sleutels):</span><span class="sxs-lookup"><span data-stu-id="9bac2-154">Define default values for parameters (except for passwords and SSH keys):</span></span>
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "hello type of hello new storage account created toostore hello VM disks."
            }
        }
   }
   ```

* <span data-ttu-id="9bac2-155">Gebruik **SecureString** voor alle wachtwoorden en geheimen:</span><span class="sxs-lookup"><span data-stu-id="9bac2-155">Use **SecureString** for all passwords and secrets:</span></span> 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "hello value of hello secret toostore in hello vault."
           }
       }
   }
   ```

* <span data-ttu-id="9bac2-156">Indien mogelijk niet gebruiken voor een parameter toospecify locatie.</span><span class="sxs-lookup"><span data-stu-id="9bac2-156">Whenever possible, don't use a parameter toospecify location.</span></span> <span data-ttu-id="9bac2-157">Gebruik in plaats daarvan Hallo **locatie** eigenschap van het Hallo-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="9bac2-157">Instead, use hello **location** property of hello resource group.</span></span> <span data-ttu-id="9bac2-158">Met behulp van Hallo **resourceGroup () .location** -expressie voor al uw resources, resources in de sjabloon Hallo zijn geïmplementeerd in dezelfde locatie als de resourcegroep Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="9bac2-158">By using hello **resourceGroup().location** expression for all your resources, resources in hello template are deployed in hello same location as hello resource group:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         ...
     }
   ]
   ```
   
   <span data-ttu-id="9bac2-159">Als een resourcetype wordt ondersteund in een beperkt aantal locaties, kunt u een geldige locatie is direct in de sjabloon Hallo toospecify.</span><span class="sxs-lookup"><span data-stu-id="9bac2-159">If a resource type is supported in only a limited number of locations, you might want toospecify a valid location directly in hello template.</span></span> <span data-ttu-id="9bac2-160">Als u moet een **locatie** parameter, die zo veel mogelijk parameterwaarde delen met bronnen die zich waarschijnlijk toobe in Hallo dezelfde locatie.</span><span class="sxs-lookup"><span data-stu-id="9bac2-160">If you must use a **location** parameter, share that parameter value as much as possible with resources that are likely toobe in hello same location.</span></span> <span data-ttu-id="9bac2-161">Hierdoor minimaliseert Hallo aantal keren dat gebruikers worden gevraagd tooprovide locatie-informatie.</span><span class="sxs-lookup"><span data-stu-id="9bac2-161">This minimizes hello number of times users are asked tooprovide location information.</span></span>
* <span data-ttu-id="9bac2-162">Vermijd het gebruik van een parameter of variabele voor Hallo API-versie voor een resourcetype.</span><span class="sxs-lookup"><span data-stu-id="9bac2-162">Avoid using a parameter or variable for hello API version for a resource type.</span></span> <span data-ttu-id="9bac2-163">Resource-eigenschappen en waarden kunnen variëren door versienummer.</span><span class="sxs-lookup"><span data-stu-id="9bac2-163">Resource properties and values can vary by version number.</span></span> <span data-ttu-id="9bac2-164">IntelliSense in een code-editor kan niet het juiste schema Hallo bepalen wanneer Hallo API-versie tooa parameter of variabele is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="9bac2-164">IntelliSense in a code editor cannot determine hello correct schema when hello API version is set tooa parameter or variable.</span></span> <span data-ttu-id="9bac2-165">In plaats daarvan Hallo harde code in Hallo sjabloon API-versie.</span><span class="sxs-lookup"><span data-stu-id="9bac2-165">Instead, hard-code hello API version in hello template.</span></span>

## <a name="variables"></a><span data-ttu-id="9bac2-166">Variabelen</span><span class="sxs-lookup"><span data-stu-id="9bac2-166">Variables</span></span>
<span data-ttu-id="9bac2-167">Hallo kan volgende informatie nuttig zijn wanneer u met variabelen werkt:</span><span class="sxs-lookup"><span data-stu-id="9bac2-167">hello following information can be helpful when you work with variables:</span></span>

* <span data-ttu-id="9bac2-168">Variabelen voor waarden die u nodig hebt toouse meer dan één keer in een sjabloon gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9bac2-168">Use variables for values that you need toouse more than once in a template.</span></span> <span data-ttu-id="9bac2-169">Als een waarde slechts één keer gebruikt wordt, kunt u een waarde vastgelegde uw sjabloon eenvoudiger tooread.</span><span class="sxs-lookup"><span data-stu-id="9bac2-169">If a value is used only once, a hard-coded value makes your template easier tooread.</span></span>
* <span data-ttu-id="9bac2-170">U kunt geen hello gebruiken [verwijzing](resource-group-template-functions-resource.md#reference) functie in Hallo **variabelen** gedeelte van de sjabloon Hallo.</span><span class="sxs-lookup"><span data-stu-id="9bac2-170">You cannot use hello [reference](resource-group-template-functions-resource.md#reference) function in hello **variables** section of hello template.</span></span> <span data-ttu-id="9bac2-171">Hallo **verwijzing** functie is afgeleid van de waarde van de runtimestatus van Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="9bac2-171">hello **reference** function derives its value from hello resource's runtime state.</span></span> <span data-ttu-id="9bac2-172">Variabelen worden echter omgezet tijdens de eerste parseren van de sjabloon Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="9bac2-172">However, variables are resolved during hello initial parsing of hello template.</span></span> <span data-ttu-id="9bac2-173">Waarden die Hallo moet samenstellen **verwijzing** functie rechtstreeks in Hallo **resources** of **levert** gedeelte van Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="9bac2-173">Construct values that need hello **reference** function directly in hello **resources** or **outputs** section of hello template.</span></span>
* <span data-ttu-id="9bac2-174">Variabelen voor de resourcenamen die uniek zijn, zoals beschreven in [Resourcenamen](#resource-names).</span><span class="sxs-lookup"><span data-stu-id="9bac2-174">Include variables for resource names that must be unique, as described in [Resource names](#resource-names).</span></span>
* <span data-ttu-id="9bac2-175">U kunt variabelen groeperen in complexe objecten.</span><span class="sxs-lookup"><span data-stu-id="9bac2-175">You can group variables into complex objects.</span></span> <span data-ttu-id="9bac2-176">Gebruik Hallo **variable.subentry** tooreference een waarde van een complex object opmaken.</span><span class="sxs-lookup"><span data-stu-id="9bac2-176">Use hello **variable.subentry** format tooreference a value from a complex object.</span></span> <span data-ttu-id="9bac2-177">Variabelen groeperen, kunt u gerelateerde variabelen volgen.</span><span class="sxs-lookup"><span data-stu-id="9bac2-177">Grouping variables can help you track related variables.</span></span> <span data-ttu-id="9bac2-178">Dit verbetert de leesbaarheid van Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="9bac2-178">It also improves readability of hello template.</span></span> <span data-ttu-id="9bac2-179">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9bac2-179">Here's an example:</span></span>
   
   ```json
   "variables": {
       "storage": {
           "name": "[concat(uniqueString(resourceGroup().id),'storage')]",
           "type": "Standard_LRS"
       }
   },
   "resources": [
     {
         "type": "Microsoft.Storage/storageAccounts",
         "name": "[variables('storage').name]",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "sku": {
             "name": "[variables('storage').type]"
         },
         ...
     }
   ]
   ```
   
   > [!NOTE]
   > <span data-ttu-id="9bac2-180">Een complex object kan niet een expressie die verwijst naar een waarde van een complex object bevatten.</span><span class="sxs-lookup"><span data-stu-id="9bac2-180">A complex object cannot contain an expression that references a value from a complex object.</span></span> <span data-ttu-id="9bac2-181">Definieer een afzonderlijke variabele voor dit doel.</span><span class="sxs-lookup"><span data-stu-id="9bac2-181">Define a separate variable for this purpose.</span></span>
   > 
   > 
   
     <span data-ttu-id="9bac2-182">Zie voor geavanceerde voorbeelden van het gebruik van complexe objecten als variabelen [delen status in Azure Resource Manager-sjablonen](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="9bac2-182">For advanced examples of using complex objects as variables, see [Share state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="resources"></a><span data-ttu-id="9bac2-183">Resources</span><span class="sxs-lookup"><span data-stu-id="9bac2-183">Resources</span></span>
<span data-ttu-id="9bac2-184">Hallo kan volgende informatie nuttig zijn wanneer u met resources werkt:</span><span class="sxs-lookup"><span data-stu-id="9bac2-184">hello following information can be helpful when you work with resources:</span></span>

* <span data-ttu-id="9bac2-185">toohelp andere medewerkers Hallo doel van Hallo resource begrijpen, geef **opmerkingen** voor elke resource in Hallo sjabloon:</span><span class="sxs-lookup"><span data-stu-id="9bac2-185">toohelp other contributors understand hello purpose of hello resource, specify **comments** for each resource in hello template:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used toostore hello VM disks.",
         ...
     }
   ]
   ```

* <span data-ttu-id="9bac2-186">U kunt tags tooadd metagegevens tooresources gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9bac2-186">You can use tags tooadd metadata tooresources.</span></span> <span data-ttu-id="9bac2-187">Gebruik metagegevens tooadd informatie over uw resources.</span><span class="sxs-lookup"><span data-stu-id="9bac2-187">Use metadata tooadd information about your resources.</span></span> <span data-ttu-id="9bac2-188">U kunt bijvoorbeeld metagegevens toorecord Factureringsdetails voor een resource toevoegen.</span><span class="sxs-lookup"><span data-stu-id="9bac2-188">For example, you can add metadata toorecord billing details for a resource.</span></span> <span data-ttu-id="9bac2-189">Zie voor meer informatie [Using tags tooorganize uw Azure-resources](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="9bac2-189">For more information, see [Using tags tooorganize your Azure resources](resource-group-using-tags.md).</span></span>
* <span data-ttu-id="9bac2-190">Als u een *openbaar eindpunt* in uw sjabloon (zoals een Azure Blob storage openbaar eindpunt), *komen niet vastleggen* Hallo naamruimte.</span><span class="sxs-lookup"><span data-stu-id="9bac2-190">If you use a *public endpoint* in your template (such as an Azure Blob storage public endpoint), *do not hard-code* hello namespace.</span></span> <span data-ttu-id="9bac2-191">Gebruik Hallo **verwijzing** functie toodynamically Hallo-naamruimte ophalen.</span><span class="sxs-lookup"><span data-stu-id="9bac2-191">Use hello **reference** function toodynamically retrieve hello namespace.</span></span> <span data-ttu-id="9bac2-192">U kunt deze benadering toodeploy Hallo sjabloon toodifferent naamruimte public omgevingen gebruiken zonder Hallo eindpunt in Hallo sjabloon handmatig wijzigen.</span><span class="sxs-lookup"><span data-stu-id="9bac2-192">You can use this approach toodeploy hello template toodifferent public namespace environments without manually changing hello endpoint in hello template.</span></span> <span data-ttu-id="9bac2-193">Hallo API-versie toohello ingesteld dezelfde versie die u in de sjabloon voor Hallo storage-account gebruikt:</span><span class="sxs-lookup"><span data-stu-id="9bac2-193">Set hello API version toohello same version that you are using for hello storage account in your template:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="9bac2-194">Als Hallo storage-account is geïmplementeerd in Hallo dezelfde sjabloon die u maakt, hoeft u niet de naamruimte van de provider Hallo toospecify wanneer u verwijst naar Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="9bac2-194">If hello storage account is deployed in hello same template that you are creating, you do not need toospecify hello provider namespace when you reference hello resource.</span></span> <span data-ttu-id="9bac2-195">Dit is Hallo vereenvoudigde syntaxis:</span><span class="sxs-lookup"><span data-stu-id="9bac2-195">This is hello simplified syntax:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="9bac2-196">Als u andere waarden in de sjabloon die geconfigureerde toouse een openbare naamruimte hebt, kunt u deze waarden wijzigen tooreflect Hallo dezelfde **verwijzing** functie.</span><span class="sxs-lookup"><span data-stu-id="9bac2-196">If you have other values in your template that are configured toouse a public namespace, change these values tooreflect hello same **reference** function.</span></span> <span data-ttu-id="9bac2-197">U kunt bijvoorbeeld Hallo instellen **storageUri** eigenschap van Hallo virtuele machine diagnostische profiel:</span><span class="sxs-lookup"><span data-stu-id="9bac2-197">For example, you can set hello **storageUri** property of hello virtual machine diagnostics profile:</span></span>
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   <span data-ttu-id="9bac2-198">Ook kunt u verwijzen naar een bestaand opslagaccount die zich in een andere resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="9bac2-198">You also can reference an existing storage account that is in a different resource group:</span></span>

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* <span data-ttu-id="9bac2-199">Wijs openbare IP-adressen tooa virtuele machine alleen wanneer dit vereist is voor een toepassing.</span><span class="sxs-lookup"><span data-stu-id="9bac2-199">Assign public IP addresses tooa virtual machine only when an application requires it.</span></span> <span data-ttu-id="9bac2-200">tooconnect tooa virtuele machine (VM) voor foutopsporing of voor beheer of administratieve doeleinden inkomende NAT-regels, een virtuele netwerkgateway of een jumpbox gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9bac2-200">tooconnect tooa virtual machine (VM) for debugging, or for management or administrative purposes, use inbound NAT rules, a virtual network gateway, or a jumpbox.</span></span>
   
     <span data-ttu-id="9bac2-201">Zie voor meer informatie over het aansluiten van toovirtual machines:</span><span class="sxs-lookup"><span data-stu-id="9bac2-201">For more information about connecting toovirtual machines, see:</span></span>
   
   * [<span data-ttu-id="9bac2-202">Virtuele machines worden uitgevoerd voor een architectuur N-aantal lagen in Azure</span><span class="sxs-lookup"><span data-stu-id="9bac2-202">Run VMs for an N-tier architecture in Azure</span></span>](../guidance/guidance-compute-n-tier-vm.md)
   * [<span data-ttu-id="9bac2-203">WinRM toegang instellen voor virtuele machines in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9bac2-203">Set up WinRM access for VMs in Azure Resource Manager</span></span>](../virtual-machines/windows/winrm.md)
   * [<span data-ttu-id="9bac2-204">Toestaan van externe toegang tooyour VM via hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="9bac2-204">Allow external access tooyour VM by using hello Azure portal</span></span>](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [<span data-ttu-id="9bac2-205">Toestaan van externe toegang tooyour virtuele machine met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bac2-205">Allow external access tooyour VM by using PowerShell</span></span>](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [<span data-ttu-id="9bac2-206">Toestaan van externe toegang tooyour Linux-VM met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9bac2-206">Allow external access tooyour Linux VM by using Azure CLI</span></span>](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* <span data-ttu-id="9bac2-207">Hallo **domainNameLabel** eigenschap voor openbare IP-adressen moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="9bac2-207">hello **domainNameLabel** property for public IP addresses must be unique.</span></span> <span data-ttu-id="9bac2-208">Hallo **domainNameLabel** waarde moet tussen 3 en 63 tekens lang en volg Hallo regels die door deze reguliere expressie opgegeven: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span><span class="sxs-lookup"><span data-stu-id="9bac2-208">hello **domainNameLabel** value must be between 3 and 63 characters long, and follow hello rules specified by this regular expression: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span></span> <span data-ttu-id="9bac2-209">Omdat Hallo **uniqueString** functie genereert een tekenreeks die is 13 tekens lang zijn, hello **dnsPrefixString** parameter is beperkt too50 tekens:</span><span class="sxs-lookup"><span data-stu-id="9bac2-209">Because hello **uniqueString** function generates a string that is 13 characters long, hello **dnsPrefixString** parameter is limited too50 characters:</span></span>

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "hello DNS label for hello public IP address. It must be lowercase. It should match hello following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* <span data-ttu-id="9bac2-210">Wanneer u een extensie voor aangepaste scripts tooa wachtwoord toevoegt, gebruikt u Hallo **commandToExecute** eigenschap in Hallo **protectedSettings** eigenschap:</span><span class="sxs-lookup"><span data-stu-id="9bac2-210">When you add a password tooa custom script extension, use hello **commandToExecute** property in hello **protectedSettings** property:</span></span>
   
   ```json
   "properties": {
       "publisher": "Microsoft.Azure.Extensions",
       "type": "CustomScript",
       "typeHandlerVersion": "2.0",
       "autoUpgradeMinorVersion": true,
       "settings": {
           "fileUris": [
               "[concat(variables('template').assets, '/lamp-app/install_lamp.sh')]"
           ]
       },
       "protectedSettings": {
           "commandToExecute": "[concat('sh install_lamp.sh ', parameters('mySqlPassword'))]"
       }
   }
   ```
   
   > [!NOTE]
   > <span data-ttu-id="9bac2-211">tooensure die geheimen zijn versleuteld wanneer ze worden doorgegeven als parameters tooVMs en -extensies, gebruikt u Hallo **protectedSettings** eigenschap van de relevante Hallo-extensies.</span><span class="sxs-lookup"><span data-stu-id="9bac2-211">tooensure that secrets are encrypted when they are passed as parameters tooVMs and extensions, use hello **protectedSettings** property of hello relevant extensions.</span></span>
   > 
   > 

## <a name="outputs"></a><span data-ttu-id="9bac2-212">uitvoer</span><span class="sxs-lookup"><span data-stu-id="9bac2-212">Outputs</span></span>
<span data-ttu-id="9bac2-213">Als u een sjabloon toocreate openbare IP-adressen gebruikt, voegt u een **levert** sectie gegevens van Hallo IP-adres en Hallo volledig gekwalificeerde domeinnaam (FQDN retourneert).</span><span class="sxs-lookup"><span data-stu-id="9bac2-213">If you use a template toocreate public IP addresses, include an **outputs** section that returns details of hello IP address and hello fully qualified domain name (FQDN).</span></span> <span data-ttu-id="9bac2-214">U kunt uitvoer waarden tooeasily ophalen informatie over de openbare IP-adressen en FQDN's gebruiken na de implementatie.</span><span class="sxs-lookup"><span data-stu-id="9bac2-214">You can use output values tooeasily retrieve details about public IP addresses and FQDNs after deployment.</span></span> <span data-ttu-id="9bac2-215">Wanneer u verwijst naar resource hello, Hallo API-versie die u hebt gebruikt toocreate gebruiken het:</span><span class="sxs-lookup"><span data-stu-id="9bac2-215">When you reference hello resource, use hello API version that you used toocreate it:</span></span> 

```json
"outputs": {
    "fqdn": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').dnsSettings.fqdn]",
        "type": "string"
    },
    "ipaddress": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').ipAddress]",
        "type": "string"
    }
}
```

## <a name="single-template-vs-nested-templates"></a><span data-ttu-id="9bac2-216">Één sjabloon versus geneste sjablonen</span><span class="sxs-lookup"><span data-stu-id="9bac2-216">Single template vs. nested templates</span></span>
<span data-ttu-id="9bac2-217">toodeploy uw oplossing kunt u één sjabloon of een sjabloon van de belangrijkste met meerdere geneste sjablonen.</span><span class="sxs-lookup"><span data-stu-id="9bac2-217">toodeploy your solution, you can use either a single template or a main template with multiple nested templates.</span></span> <span data-ttu-id="9bac2-218">Geneste sjablonen gelden voor meer geavanceerde scenario's.</span><span class="sxs-lookup"><span data-stu-id="9bac2-218">Nested templates are common for more advanced scenarios.</span></span> <span data-ttu-id="9bac2-219">Met behulp van een geneste sjabloon biedt u Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="9bac2-219">Using a nested template gives you hello following advantages:</span></span>

* <span data-ttu-id="9bac2-220">U kunt een oplossing in de betreffende onderdelen uitgesplitst.</span><span class="sxs-lookup"><span data-stu-id="9bac2-220">You can break down a solution into targeted components.</span></span>
* <span data-ttu-id="9bac2-221">U kunt geneste sjablonen met verschillende belangrijke sjablonen hergebruiken.</span><span class="sxs-lookup"><span data-stu-id="9bac2-221">You can reuse nested templates with different main templates.</span></span>

<span data-ttu-id="9bac2-222">Als u toouse geneste sjablonen kiest, kunt Hallo richtlijnen u uw sjabloonontwerp standaardiseren.</span><span class="sxs-lookup"><span data-stu-id="9bac2-222">If you choose toouse nested templates, hello following guidelines can help you standardize your template design.</span></span> <span data-ttu-id="9bac2-223">Deze richtlijnen zijn gebaseerd op [patronen voor Azure Resource Manager-sjablonen ontwerpen](best-practices-resource-manager-design-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9bac2-223">These guidelines are based on [patterns for designing Azure Resource Manager templates](best-practices-resource-manager-design-templates.md).</span></span> <span data-ttu-id="9bac2-224">U wordt aangeraden een ontwerp dat het Hallo-sjablonen te volgen:</span><span class="sxs-lookup"><span data-stu-id="9bac2-224">We recommend a design that has hello following templates:</span></span>

* <span data-ttu-id="9bac2-225">**Belangrijkste sjabloon** (azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="9bac2-225">**Main template** (azuredeploy.json).</span></span> <span data-ttu-id="9bac2-226">Gebruik dit voor de invoerparameters Hallo.</span><span class="sxs-lookup"><span data-stu-id="9bac2-226">Use for hello input parameters.</span></span>
* <span data-ttu-id="9bac2-227">**Gedeelde bronnen sjabloon**.</span><span class="sxs-lookup"><span data-stu-id="9bac2-227">**Shared resources template**.</span></span> <span data-ttu-id="9bac2-228">Gebruik toodeploy gedeelde resources die gebruikmaken van alle andere bronnen (bijvoorbeeld virtuele-netwerk en beschikbaarheid sets).</span><span class="sxs-lookup"><span data-stu-id="9bac2-228">Use toodeploy shared resources that all other resources use (for example, virtual network and availability sets).</span></span> <span data-ttu-id="9bac2-229">Gebruik Hallo **dependsOn** expressie tooensure dat deze sjabloon wordt geïmplementeerd voordat andere sjablonen.</span><span class="sxs-lookup"><span data-stu-id="9bac2-229">Use hello **dependsOn** expression tooensure that this template is deployed before other templates.</span></span>
* <span data-ttu-id="9bac2-230">**Optionele resources sjabloon**.</span><span class="sxs-lookup"><span data-stu-id="9bac2-230">**Optional resources template**.</span></span> <span data-ttu-id="9bac2-231">Gebruik tooconditionally resources op basis van een parameter (bijvoorbeeld een jumpbox) implementeren.</span><span class="sxs-lookup"><span data-stu-id="9bac2-231">Use tooconditionally deploy resources based on a parameter (for example, a jumpbox).</span></span>
* <span data-ttu-id="9bac2-232">**Lid resources sjabloon**.</span><span class="sxs-lookup"><span data-stu-id="9bac2-232">**Member resources template**.</span></span> <span data-ttu-id="9bac2-233">Elk exemplaartype binnen een toepassingslaag heeft een eigen configuratie.</span><span class="sxs-lookup"><span data-stu-id="9bac2-233">Each instance type within an application tier has its own configuration.</span></span> <span data-ttu-id="9bac2-234">Binnen een laag, kunt u een ander exemplaar typen definiëren.</span><span class="sxs-lookup"><span data-stu-id="9bac2-234">Within a tier, you can define different instance types.</span></span> <span data-ttu-id="9bac2-235">(Bijvoorbeeld Hallo eerste instantie wordt gemaakt van een cluster en extra exemplaren toohello bestaand cluster worden toegevoegd.) Elk exemplaartype heeft een eigen sjabloon voor de implementatie.</span><span class="sxs-lookup"><span data-stu-id="9bac2-235">(For example, hello first instance creates a cluster, and additional instances are added toohello existing cluster.) Each instance type has its own deployment template.</span></span>
* <span data-ttu-id="9bac2-236">**Scripts**.</span><span class="sxs-lookup"><span data-stu-id="9bac2-236">**Scripts**.</span></span> <span data-ttu-id="9bac2-237">Algemeen herbruikbare scripts zijn van toepassing voor elk van exemplaartype (bijvoorbeeld, initialiseren en formatteren extra schijven).</span><span class="sxs-lookup"><span data-stu-id="9bac2-237">Widely reusable scripts are applicable for each instance type (for example, initialize and format additional disks).</span></span> <span data-ttu-id="9bac2-238">Aangepaste scripts die u voor een specifieke aanpassing doel maakt zijn verschillend, op basis van het Hallo-instanceType.</span><span class="sxs-lookup"><span data-stu-id="9bac2-238">Custom scripts that you create for a specific customization purpose are different, based on hello instance type.</span></span>

![Geneste sjabloon](./media/resource-manager-template-best-practices/nestedTemplateDesign.png)

<span data-ttu-id="9bac2-240">Zie voor meer informatie [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9bac2-240">For more information, see [Use linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="conditionally-link-toonested-templates"></a><span data-ttu-id="9bac2-241">Voorwaardelijk toonested sjablonen koppelen</span><span class="sxs-lookup"><span data-stu-id="9bac2-241">Conditionally link toonested templates</span></span>
<span data-ttu-id="9bac2-242">U kunt een parameter tooconditionally koppeling toonested sjablonen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9bac2-242">You can use a parameter tooconditionally link toonested templates.</span></span> <span data-ttu-id="9bac2-243">Hallo parameter maakt deel uit van Hallo URI voor Hallo sjabloon:</span><span class="sxs-lookup"><span data-stu-id="9bac2-243">hello parameter becomes part of hello URI for hello template:</span></span>

```json
"parameters": {
    "newOrExisting": {
        "type": "String",
        "allowedValues": [
            "new",
            "existing"
        ]
    }
},
"variables": {
    "templatelink": "[concat('https://raw.githubusercontent.com/Contoso/Templates/master/',parameters('newOrExisting'),'StorageAccount.json')]"
},
"resources": [
    {
        "apiVersion": "2015-01-01",
        "name": "nestedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
            "mode": "incremental",
            "templateLink": {
                "uri": "[variables('templatelink')]",
                "contentVersion": "1.0.0.0"
            },
            "parameters": {
            }
        }
    }
]
```

## <a name="template-format"></a><span data-ttu-id="9bac2-244">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="9bac2-244">Template format</span></span>
<span data-ttu-id="9bac2-245">Het is een goede gewoonte toopass uw sjabloon via een JSON-validator.</span><span class="sxs-lookup"><span data-stu-id="9bac2-245">It's a good practice toopass your template through a JSON validator.</span></span> <span data-ttu-id="9bac2-246">Een validatiefunctie kunt u Verwijder overbodige komma's, haakjes en haakjes ertoe leiden een fout opgetreden tijdens de implementatie dat kunnen.</span><span class="sxs-lookup"><span data-stu-id="9bac2-246">A validator can help you remove extraneous commas, parentheses, and brackets that might cause an error during deployment.</span></span> <span data-ttu-id="9bac2-247">Probeer [JSONLint](http://jsonlint.com/) of een pakket linter voor uw favoriete omgeving (Visual Studio Code, Atom, Sublime tekst, Visual Studio) bewerken.</span><span class="sxs-lookup"><span data-stu-id="9bac2-247">Try [JSONLint](http://jsonlint.com/) or a linter package for your favorite editing environment (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span></span>

<span data-ttu-id="9bac2-248">Het is ook een goed idee tooformat uw JSON voor een betere leesbaarheid.</span><span class="sxs-lookup"><span data-stu-id="9bac2-248">It's also a good idea tooformat your JSON for better readability.</span></span> <span data-ttu-id="9bac2-249">Voor uw lokale editor kunt u een pakket van JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="9bac2-249">You can use a JSON formatter package for your local editor.</span></span> <span data-ttu-id="9bac2-250">Druk in Visual Studio, tooformat Hallo-document op **Ctrl + K, Ctrl + D**.</span><span class="sxs-lookup"><span data-stu-id="9bac2-250">In Visual Studio, tooformat hello document, press **Ctrl+K, Ctrl+D**.</span></span> <span data-ttu-id="9bac2-251">Druk in Visual Studio Code op **Alt + Shift + F**.</span><span class="sxs-lookup"><span data-stu-id="9bac2-251">In Visual Studio Code, press **Alt+Shift+F**.</span></span> <span data-ttu-id="9bac2-252">Als uw lokale editor niet Hallo document opmaken, kunt u een [online formatter](https://www.bing.com/search?q=json+formatter).</span><span class="sxs-lookup"><span data-stu-id="9bac2-252">If your local editor doesn't format hello document, you can use an [online formatter](https://www.bing.com/search?q=json+formatter).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9bac2-253">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9bac2-253">Next steps</span></span>
* <span data-ttu-id="9bac2-254">Zie voor instructies over het aanpassen van uw oplossing voor virtuele machines, [een virtuele machine van Windows worden uitgevoerd in Azure](../guidance/guidance-compute-single-vm.md) en [een Linux-VM in Azure uitvoeren](../guidance/guidance-compute-single-vm-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9bac2-254">For guidance on architecting your solution for virtual machines, see [Run a Windows VM in Azure](../guidance/guidance-compute-single-vm.md) and [Run a Linux VM in Azure](../guidance/guidance-compute-single-vm-linux.md).</span></span>
* <span data-ttu-id="9bac2-255">Zie voor instructies over het instellen van een opslagaccount [controlelijst voor prestaties en schaalbaarheid van Azure Storage](../storage/common/storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="9bac2-255">For guidance on setting up a storage account, see [Azure Storage performance and scalability checklist](../storage/common/storage-performance-checklist.md).</span></span>
* <span data-ttu-id="9bac2-256">toolearn over hoe een onderneming met Resource Manager tooeffectively abonnementen beheren, Zie [Azure enterprise scaffold: Prescriptieve abonnement governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="9bac2-256">toolearn about how an enterprise can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold: Prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

