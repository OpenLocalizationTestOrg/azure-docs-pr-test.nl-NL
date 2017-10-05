---
title: Aanbevolen procedures voor het maken van Resource Manager-sjablonen | Microsoft Docs
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
ms.openlocfilehash: a23301ba88279af3f7bf4d353ae808e9eeb0900d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a><span data-ttu-id="2efd9-103">Aanbevolen procedures voor het maken van Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="2efd9-103">Best practices for creating Azure Resource Manager templates</span></span>
<span data-ttu-id="2efd9-104">Deze richtlijnen kunt u bij het maken van Azure Resource Manager-sjablonen die betrouwbaar en eenvoudig te gebruiken zijn.</span><span class="sxs-lookup"><span data-stu-id="2efd9-104">These guidelines can help you create Azure Resource Manager templates that are reliable and easy to use.</span></span> <span data-ttu-id="2efd9-105">De richtlijnen zijn alleen suggesties.</span><span class="sxs-lookup"><span data-stu-id="2efd9-105">The guidelines are only suggestions.</span></span> <span data-ttu-id="2efd9-106">Ze zijn geen vereisten, tenzij anders wordt vermeld.</span><span class="sxs-lookup"><span data-stu-id="2efd9-106">They are not requirements, except where noted.</span></span> <span data-ttu-id="2efd9-107">Uw scenario mogelijk een variant van een van de volgende methoden of voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="2efd9-107">Your scenario might require a variation of one of the following approaches or examples.</span></span>

## <a name="resource-names"></a><span data-ttu-id="2efd9-108">Resourcenamen</span><span class="sxs-lookup"><span data-stu-id="2efd9-108">Resource names</span></span>
<span data-ttu-id="2efd9-109">In het algemeen werken u met drie soorten resourcenamen in Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="2efd9-109">Generally, you work with three types of resource names in Resource Manager:</span></span>

* <span data-ttu-id="2efd9-110">Resourcenamen moeten uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="2efd9-110">Resource names that must be unique.</span></span>
* <span data-ttu-id="2efd9-111">Resourcenamen die nodig zijn niet uniek te zijn, maar u kunt een naam waarmee u een resource op basis van context identificeren kunt geven.</span><span class="sxs-lookup"><span data-stu-id="2efd9-111">Resource names that are not required to be unique, but you choose to provide a name that can help you identify a resource based on context.</span></span>
* <span data-ttu-id="2efd9-112">Resourcenamen kunnen niet algemeen zijn.</span><span class="sxs-lookup"><span data-stu-id="2efd9-112">Resource names that can be generic.</span></span>

 <span data-ttu-id="2efd9-113">Zie voor meer informatie over de beperkingen voor resource [aanbevolen naamgevingsregels voor Azure-resources](../guidance/guidance-naming-conventions.md).</span><span class="sxs-lookup"><span data-stu-id="2efd9-113">For information about resource name restrictions, see [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md).</span></span>

### <a name="unique-resource-names"></a><span data-ttu-id="2efd9-114">Unieke resourcenamen</span><span class="sxs-lookup"><span data-stu-id="2efd9-114">Unique resource names</span></span>
<span data-ttu-id="2efd9-115">U moet een unieke bronnaam voor resourcetype dat een data access-eindpunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="2efd9-115">You must provide a unique resource name for any resource type that has a data access endpoint.</span></span> <span data-ttu-id="2efd9-116">Sommige algemene brontypen waarvoor een unieke naam zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="2efd9-116">Some common resource types that require a unique name include:</span></span>

* <span data-ttu-id="2efd9-117">Azure Storage<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="2efd9-117">Azure Storage<sup>1</sup></span></span> 
* <span data-ttu-id="2efd9-118">Web Apps-functie van Azure App Service</span><span class="sxs-lookup"><span data-stu-id="2efd9-118">Web Apps feature of Azure App Service</span></span>
* <span data-ttu-id="2efd9-119">SQL Server</span><span class="sxs-lookup"><span data-stu-id="2efd9-119">SQL Server</span></span>
* <span data-ttu-id="2efd9-120">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="2efd9-120">Azure Key Vault</span></span>
* <span data-ttu-id="2efd9-121">Azure Redis-cache</span><span class="sxs-lookup"><span data-stu-id="2efd9-121">Azure Redis Cache</span></span>
* <span data-ttu-id="2efd9-122">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="2efd9-122">Azure Batch</span></span>
* <span data-ttu-id="2efd9-123">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="2efd9-123">Azure Traffic Manager</span></span>
* <span data-ttu-id="2efd9-124">Azure Search</span><span class="sxs-lookup"><span data-stu-id="2efd9-124">Azure Search</span></span>
* <span data-ttu-id="2efd9-125">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="2efd9-125">Azure HDInsight</span></span>

<span data-ttu-id="2efd9-126"><sup>1</sup> opslagaccountnamen ook moet een kleine letter, 24 tekens of korter is, en geen eventuele verbindingsstreepjes.</span><span class="sxs-lookup"><span data-stu-id="2efd9-126"><sup>1</sup> Storage account names also must be lowercase, 24 characters or less, and not have any hyphens.</span></span>

<span data-ttu-id="2efd9-127">Als u een parameter voor een resourcenaam opgeeft, moet u een unieke naam opgeven bij het implementeren van de resource.</span><span class="sxs-lookup"><span data-stu-id="2efd9-127">If you provide a parameter for a resource name, you must provide a unique name when you deploy the resource.</span></span> <span data-ttu-id="2efd9-128">Desgewenst kunt u een variabele die gebruikmaakt van de [uniqueString()](resource-group-template-functions-string.md#uniquestring) functie voor het genereren van een naam.</span><span class="sxs-lookup"><span data-stu-id="2efd9-128">Optionally, you can create a variable that uses the [uniqueString()](resource-group-template-functions-string.md#uniquestring) function to generate a name.</span></span> 

<span data-ttu-id="2efd9-129">Ook raadzaam een voorvoegsel toevoegen of een achtervoegsel aan de **uniqueString** resultaat.</span><span class="sxs-lookup"><span data-stu-id="2efd9-129">You also might want to add a prefix or suffix to the **uniqueString** result.</span></span> <span data-ttu-id="2efd9-130">De unieke naam wijzigen, kunt u gemakkelijk herkennen het brontype van de naam.</span><span class="sxs-lookup"><span data-stu-id="2efd9-130">Modifying the unique name can help you more easily identify the resource type from the name.</span></span> <span data-ttu-id="2efd9-131">U kunt bijvoorbeeld een unieke naam voor een opslagaccount genereren met behulp van de volgende variabele:</span><span class="sxs-lookup"><span data-stu-id="2efd9-131">For example, you can generate a unique name for a storage account by using the following variable:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a><span data-ttu-id="2efd9-132">Resourcenamen voor identificatie</span><span class="sxs-lookup"><span data-stu-id="2efd9-132">Resource names for identification</span></span>
<span data-ttu-id="2efd9-133">Sommige kunt u de naam, maar hun namen van resourcetypen hoeft geen uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="2efd9-133">Some resource types you might want to name, but their names do not have to be unique.</span></span> <span data-ttu-id="2efd9-134">U kunt een naam waarmee u zowel de context van de bron en het resourcetype opgeven voor deze resourcetypen.</span><span class="sxs-lookup"><span data-stu-id="2efd9-134">For these resource types, you can provide a name that identifies both the resource context and the resource type.</span></span> <span data-ttu-id="2efd9-135">Geef een beschrijvende naam waarmee u de resource in een lijst met bronnen identificeren.</span><span class="sxs-lookup"><span data-stu-id="2efd9-135">Provide a descriptive name that helps you identify the resource in a list of resources.</span></span> <span data-ttu-id="2efd9-136">Als u de naam van een andere bron voor verschillende implementaties gebruiken moet, kunt u een parameter voor de naam:</span><span class="sxs-lookup"><span data-stu-id="2efd9-136">If you need to use a different resource name for different deployments, you can use a parameter for the name:</span></span>

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "The name of the VM to create."
        }
    }
}
```

<span data-ttu-id="2efd9-137">Als u niet een naam opgeeft tijdens de implementatie wilt, kunt u een variabele gebruiken:</span><span class="sxs-lookup"><span data-stu-id="2efd9-137">If you do not need to pass in a name during deployment, you can use a variable:</span></span> 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

<span data-ttu-id="2efd9-138">U kunt ook een waarde vastgelegde gebruiken:</span><span class="sxs-lookup"><span data-stu-id="2efd9-138">You also can use a hard-coded value:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a><span data-ttu-id="2efd9-139">Algemene resourcenamen</span><span class="sxs-lookup"><span data-stu-id="2efd9-139">Generic resource names</span></span>
<span data-ttu-id="2efd9-140">Voor brontypen die u voornamelijk via een andere resource benaderen, kunt u een algemene naam die is vastgelegd in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2efd9-140">For resource types that you mostly access through a different resource, you can use a generic name that is hard-coded in the template.</span></span> <span data-ttu-id="2efd9-141">U kunt bijvoorbeeld een algemene naam op voor firewallregels instellen op een SQL server:</span><span class="sxs-lookup"><span data-stu-id="2efd9-141">For example, you can set a standard, generic name for firewall rules on a SQL server:</span></span>

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a><span data-ttu-id="2efd9-142">Parameters</span><span class="sxs-lookup"><span data-stu-id="2efd9-142">Parameters</span></span>
<span data-ttu-id="2efd9-143">De volgende informatie kan nuttig zijn wanneer u met parameters werkt:</span><span class="sxs-lookup"><span data-stu-id="2efd9-143">The following information can be helpful when you work with parameters:</span></span>

* <span data-ttu-id="2efd9-144">Beperk het gebruik van parameters.</span><span class="sxs-lookup"><span data-stu-id="2efd9-144">Minimize your use of parameters.</span></span> <span data-ttu-id="2efd9-145">Gebruik indien mogelijk een variabele of een letterlijke waarde.</span><span class="sxs-lookup"><span data-stu-id="2efd9-145">Whenever possible, use a variable or a literal value.</span></span> <span data-ttu-id="2efd9-146">Parameters gebruiken om alleen voor deze scenario's:</span><span class="sxs-lookup"><span data-stu-id="2efd9-146">Use parameters only for these scenarios:</span></span>
   
   * <span data-ttu-id="2efd9-147">Instellingen die u wilt gebruiken variaties van de basis van de omgeving (SKU, grootte, capaciteit).</span><span class="sxs-lookup"><span data-stu-id="2efd9-147">Settings that you want to use variations of according to environment (SKU, size, capacity).</span></span>
   * <span data-ttu-id="2efd9-148">Resourcenamen die u wilt opgeven voor eenvoudige identificatie.</span><span class="sxs-lookup"><span data-stu-id="2efd9-148">Resource names that you want to specify for easy identification.</span></span>
   * <span data-ttu-id="2efd9-149">De waarden die u vaak gebruikt om andere taken (zoals een beheerdersgebruikersnaam) te voltooien.</span><span class="sxs-lookup"><span data-stu-id="2efd9-149">Values that you use frequently to complete other tasks (such as an admin user name).</span></span>
   * <span data-ttu-id="2efd9-150">Geheimen (zoals wachtwoorden).</span><span class="sxs-lookup"><span data-stu-id="2efd9-150">Secrets (such as passwords).</span></span>
   * <span data-ttu-id="2efd9-151">Het nummer of de matrix met waarden te gebruiken als u meerdere exemplaren van een resourcetype.</span><span class="sxs-lookup"><span data-stu-id="2efd9-151">The number or array of values to use when you create multiple instances of a resource type.</span></span>
* <span data-ttu-id="2efd9-152">Gebruik kamelen voor namen van parameters.</span><span class="sxs-lookup"><span data-stu-id="2efd9-152">Use camel case for parameter names.</span></span>
* <span data-ttu-id="2efd9-153">Geef een beschrijving van elke parameter in de metagegevens:</span><span class="sxs-lookup"><span data-stu-id="2efd9-153">Provide a description of every parameter in the metadata:</span></span>

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "The type of the new storage account created to store the VM disks."
           }
       }
   }
   ```

* <span data-ttu-id="2efd9-154">Definieer de standaardwaarden voor parameters (met uitzondering van wachtwoorden en SSH-sleutels):</span><span class="sxs-lookup"><span data-stu-id="2efd9-154">Define default values for parameters (except for passwords and SSH keys):</span></span>
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "The type of the new storage account created to store the VM disks."
            }
        }
   }
   ```

* <span data-ttu-id="2efd9-155">Gebruik **SecureString** voor alle wachtwoorden en geheimen:</span><span class="sxs-lookup"><span data-stu-id="2efd9-155">Use **SecureString** for all passwords and secrets:</span></span> 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "The value of the secret to store in the vault."
           }
       }
   }
   ```

* <span data-ttu-id="2efd9-156">Gebruik indien mogelijk niet een parameter locatie op te geven.</span><span class="sxs-lookup"><span data-stu-id="2efd9-156">Whenever possible, don't use a parameter to specify location.</span></span> <span data-ttu-id="2efd9-157">Gebruik in plaats daarvan de **locatie** eigenschap van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="2efd9-157">Instead, use the **location** property of the resource group.</span></span> <span data-ttu-id="2efd9-158">Met behulp van de **resourceGroup () .location** -expressie voor al uw resources resources in de sjabloon zijn geïmplementeerd op dezelfde locatie als de resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="2efd9-158">By using the **resourceGroup().location** expression for all your resources, resources in the template are deployed in the same location as the resource group:</span></span>
   
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
   
   <span data-ttu-id="2efd9-159">Als u een resourcetype wordt ondersteund in een beperkt aantal locaties, is het raadzaam om op te geven van een geldige locatie rechtstreeks in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2efd9-159">If a resource type is supported in only a limited number of locations, you might want to specify a valid location directly in the template.</span></span> <span data-ttu-id="2efd9-160">Als u moet een **locatie** parameter, die zo veel mogelijk parameterwaarde met bronnen die zich waarschijnlijk op dezelfde locatie delen.</span><span class="sxs-lookup"><span data-stu-id="2efd9-160">If you must use a **location** parameter, share that parameter value as much as possible with resources that are likely to be in the same location.</span></span> <span data-ttu-id="2efd9-161">Hiermee wordt het aantal keren dat gebruikers worden gevraagd om informatie over de locatie geminimaliseerd.</span><span class="sxs-lookup"><span data-stu-id="2efd9-161">This minimizes the number of times users are asked to provide location information.</span></span>
* <span data-ttu-id="2efd9-162">Vermijd het gebruik van een parameter of variabele voor de API-versie voor een resourcetype.</span><span class="sxs-lookup"><span data-stu-id="2efd9-162">Avoid using a parameter or variable for the API version for a resource type.</span></span> <span data-ttu-id="2efd9-163">Resource-eigenschappen en waarden kunnen variëren door versienummer.</span><span class="sxs-lookup"><span data-stu-id="2efd9-163">Resource properties and values can vary by version number.</span></span> <span data-ttu-id="2efd9-164">IntelliSense in een code-editor kan niet het juiste schema bepalen wanneer de API-versie is ingesteld op een parameter of variabele.</span><span class="sxs-lookup"><span data-stu-id="2efd9-164">IntelliSense in a code editor cannot determine the correct schema when the API version is set to a parameter or variable.</span></span> <span data-ttu-id="2efd9-165">In plaats daarvan harde code de API-versie in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2efd9-165">Instead, hard-code the API version in the template.</span></span>

## <a name="variables"></a><span data-ttu-id="2efd9-166">Variabelen</span><span class="sxs-lookup"><span data-stu-id="2efd9-166">Variables</span></span>
<span data-ttu-id="2efd9-167">De volgende informatie kan nuttig zijn wanneer u met variabelen werkt:</span><span class="sxs-lookup"><span data-stu-id="2efd9-167">The following information can be helpful when you work with variables:</span></span>

* <span data-ttu-id="2efd9-168">Variabelen voor waarden die u moet meer dan één keer gebruiken in een sjabloon gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2efd9-168">Use variables for values that you need to use more than once in a template.</span></span> <span data-ttu-id="2efd9-169">Als een waarde slechts één keer gebruikt wordt, een vastgelegde waarde maakt de sjabloon gemakkelijker te lezen.</span><span class="sxs-lookup"><span data-stu-id="2efd9-169">If a value is used only once, a hard-coded value makes your template easier to read.</span></span>
* <span data-ttu-id="2efd9-170">U kunt geen gebruiken de [verwijzing](resource-group-template-functions-resource.md#reference) werken in de **variabelen** gedeelte van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2efd9-170">You cannot use the [reference](resource-group-template-functions-resource.md#reference) function in the **variables** section of the template.</span></span> <span data-ttu-id="2efd9-171">De **verwijzing** functie is afgeleid van de waarde van de runtimestatus van de resource.</span><span class="sxs-lookup"><span data-stu-id="2efd9-171">The **reference** function derives its value from the resource's runtime state.</span></span> <span data-ttu-id="2efd9-172">Variabelen zijn echter opgelost bij het eerste parseren van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2efd9-172">However, variables are resolved during the initial parsing of the template.</span></span> <span data-ttu-id="2efd9-173">Constructie waarden die moeten de **verwijzing** werken rechtstreeks in de **resources** of **levert** gedeelte van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2efd9-173">Construct values that need the **reference** function directly in the **resources** or **outputs** section of the template.</span></span>
* <span data-ttu-id="2efd9-174">Variabelen voor de resourcenamen die uniek zijn, zoals beschreven in [Resourcenamen](#resource-names).</span><span class="sxs-lookup"><span data-stu-id="2efd9-174">Include variables for resource names that must be unique, as described in [Resource names](#resource-names).</span></span>
* <span data-ttu-id="2efd9-175">U kunt variabelen groeperen in complexe objecten.</span><span class="sxs-lookup"><span data-stu-id="2efd9-175">You can group variables into complex objects.</span></span> <span data-ttu-id="2efd9-176">Gebruik de **variable.subentry** notatie om te verwijzen naar een waarde van een complex object.</span><span class="sxs-lookup"><span data-stu-id="2efd9-176">Use the **variable.subentry** format to reference a value from a complex object.</span></span> <span data-ttu-id="2efd9-177">Variabelen groeperen, kunt u gerelateerde variabelen volgen.</span><span class="sxs-lookup"><span data-stu-id="2efd9-177">Grouping variables can help you track related variables.</span></span> <span data-ttu-id="2efd9-178">Dit verbetert de leesbaarheid van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2efd9-178">It also improves readability of the template.</span></span> <span data-ttu-id="2efd9-179">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2efd9-179">Here's an example:</span></span>
   
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
   > <span data-ttu-id="2efd9-180">Een complex object kan niet een expressie die verwijst naar een waarde van een complex object bevatten.</span><span class="sxs-lookup"><span data-stu-id="2efd9-180">A complex object cannot contain an expression that references a value from a complex object.</span></span> <span data-ttu-id="2efd9-181">Definieer een afzonderlijke variabele voor dit doel.</span><span class="sxs-lookup"><span data-stu-id="2efd9-181">Define a separate variable for this purpose.</span></span>
   > 
   > 
   
     <span data-ttu-id="2efd9-182">Zie voor geavanceerde voorbeelden van het gebruik van complexe objecten als variabelen [delen status in Azure Resource Manager-sjablonen](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="2efd9-182">For advanced examples of using complex objects as variables, see [Share state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="resources"></a><span data-ttu-id="2efd9-183">Resources</span><span class="sxs-lookup"><span data-stu-id="2efd9-183">Resources</span></span>
<span data-ttu-id="2efd9-184">De volgende informatie kan nuttig zijn wanneer u met resources werkt:</span><span class="sxs-lookup"><span data-stu-id="2efd9-184">The following information can be helpful when you work with resources:</span></span>

* <span data-ttu-id="2efd9-185">Andere inzenders leert wat het doel van de resource Geef, om te **opmerkingen** voor elke resource in de sjabloon:</span><span class="sxs-lookup"><span data-stu-id="2efd9-185">To help other contributors understand the purpose of the resource, specify **comments** for each resource in the template:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used to store the VM disks.",
         ...
     }
   ]
   ```

* <span data-ttu-id="2efd9-186">U kunt tags metagegevens aan resources toevoegen.</span><span class="sxs-lookup"><span data-stu-id="2efd9-186">You can use tags to add metadata to resources.</span></span> <span data-ttu-id="2efd9-187">Informatie over uw resources toevoegen met behulp van de metagegevens.</span><span class="sxs-lookup"><span data-stu-id="2efd9-187">Use metadata to add information about your resources.</span></span> <span data-ttu-id="2efd9-188">U kunt bijvoorbeeld metagegevens om vast te leggen Factureringsdetails voor een resource toevoegen.</span><span class="sxs-lookup"><span data-stu-id="2efd9-188">For example, you can add metadata to record billing details for a resource.</span></span> <span data-ttu-id="2efd9-189">Zie voor meer informatie [met labels om uw Azure-resources te organiseren](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="2efd9-189">For more information, see [Using tags to organize your Azure resources](resource-group-using-tags.md).</span></span>
* <span data-ttu-id="2efd9-190">Als u een *openbaar eindpunt* in uw sjabloon (zoals een Azure Blob storage openbaar eindpunt), *komen niet vastleggen* de naamruimte.</span><span class="sxs-lookup"><span data-stu-id="2efd9-190">If you use a *public endpoint* in your template (such as an Azure Blob storage public endpoint), *do not hard-code* the namespace.</span></span> <span data-ttu-id="2efd9-191">Gebruik de **verwijzing** functie voor het dynamisch ophalen van de naamruimte.</span><span class="sxs-lookup"><span data-stu-id="2efd9-191">Use the **reference** function to dynamically retrieve the namespace.</span></span> <span data-ttu-id="2efd9-192">Deze aanpak kunt u de sjabloon kan implementeren op andere openbare naamruimte omgevingen zonder handmatig wijzigen van het eindpunt in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2efd9-192">You can use this approach to deploy the template to different public namespace environments without manually changing the endpoint in the template.</span></span> <span data-ttu-id="2efd9-193">Stel de API-versie naar dezelfde versie die u voor het opslagaccount in de sjabloon gebruikt:</span><span class="sxs-lookup"><span data-stu-id="2efd9-193">Set the API version to the same version that you are using for the storage account in your template:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="2efd9-194">Als het opslagaccount is geïmplementeerd in dezelfde sjabloon die u maakt, hoeft u geen naamruimte van de provider opgeven wanneer u verwijst naar de resource.</span><span class="sxs-lookup"><span data-stu-id="2efd9-194">If the storage account is deployed in the same template that you are creating, you do not need to specify the provider namespace when you reference the resource.</span></span> <span data-ttu-id="2efd9-195">Dit is de vereenvoudigde syntaxis:</span><span class="sxs-lookup"><span data-stu-id="2efd9-195">This is the simplified syntax:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="2efd9-196">Als u andere waarden in de sjabloon die zijn geconfigureerd voor gebruik van een openbare naamruimte hebt, deze waarden zodat dezelfde wijzigen **verwijzing** functie.</span><span class="sxs-lookup"><span data-stu-id="2efd9-196">If you have other values in your template that are configured to use a public namespace, change these values to reflect the same **reference** function.</span></span> <span data-ttu-id="2efd9-197">U kunt bijvoorbeeld instellen de **storageUri** eigenschap van de virtuele machine diagnostische profiel:</span><span class="sxs-lookup"><span data-stu-id="2efd9-197">For example, you can set the **storageUri** property of the virtual machine diagnostics profile:</span></span>
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   <span data-ttu-id="2efd9-198">Ook kunt u verwijzen naar een bestaand opslagaccount die zich in een andere resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="2efd9-198">You also can reference an existing storage account that is in a different resource group:</span></span>

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* <span data-ttu-id="2efd9-199">Openbare IP-adressen toewijzen aan een virtuele machine alleen als dit vereist is voor een toepassing.</span><span class="sxs-lookup"><span data-stu-id="2efd9-199">Assign public IP addresses to a virtual machine only when an application requires it.</span></span> <span data-ttu-id="2efd9-200">Voor verbinding met een virtuele machine (VM) voor foutopsporing of voor beheer of administratieve doeleinden, inkomende NAT-regels, een virtuele netwerkgateway of een jumpbox te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2efd9-200">To connect to a virtual machine (VM) for debugging, or for management or administrative purposes, use inbound NAT rules, a virtual network gateway, or a jumpbox.</span></span>
   
     <span data-ttu-id="2efd9-201">Zie voor meer informatie over verbinding maken met virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="2efd9-201">For more information about connecting to virtual machines, see:</span></span>
   
   * [<span data-ttu-id="2efd9-202">Virtuele machines worden uitgevoerd voor een architectuur N-aantal lagen in Azure</span><span class="sxs-lookup"><span data-stu-id="2efd9-202">Run VMs for an N-tier architecture in Azure</span></span>](../guidance/guidance-compute-n-tier-vm.md)
   * [<span data-ttu-id="2efd9-203">WinRM toegang instellen voor virtuele machines in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2efd9-203">Set up WinRM access for VMs in Azure Resource Manager</span></span>](../virtual-machines/windows/winrm.md)
   * [<span data-ttu-id="2efd9-204">Toestaan van externe toegang tot uw virtuele machine met behulp van de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="2efd9-204">Allow external access to your VM by using the Azure portal</span></span>](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [<span data-ttu-id="2efd9-205">Toestaan van externe toegang tot uw virtuele machine met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="2efd9-205">Allow external access to your VM by using PowerShell</span></span>](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [<span data-ttu-id="2efd9-206">Toestaan van externe toegang tot uw Linux-VM met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2efd9-206">Allow external access to your Linux VM by using Azure CLI</span></span>](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* <span data-ttu-id="2efd9-207">De **domainNameLabel** eigenschap voor openbare IP-adressen moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="2efd9-207">The **domainNameLabel** property for public IP addresses must be unique.</span></span> <span data-ttu-id="2efd9-208">De **domainNameLabel** waarde moet tussen 3 en 63 tekens lang en volgt u de regels die door deze reguliere expressie opgegeven: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span><span class="sxs-lookup"><span data-stu-id="2efd9-208">The **domainNameLabel** value must be between 3 and 63 characters long, and follow the rules specified by this regular expression: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span></span> <span data-ttu-id="2efd9-209">Omdat de **uniqueString** functie een tekenreeks die is 13 tekens lang zijn, genereert de **dnsPrefixString** parameter is beperkt tot 50 tekens bevatten:</span><span class="sxs-lookup"><span data-stu-id="2efd9-209">Because the **uniqueString** function generates a string that is 13 characters long, the **dnsPrefixString** parameter is limited to 50 characters:</span></span>

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "The DNS label for the public IP address. It must be lowercase. It should match the following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* <span data-ttu-id="2efd9-210">Wanneer u een wachtwoord aan een extensie voor aangepaste scripts toevoegt, gebruiken de **commandToExecute** eigenschap in de **protectedSettings** eigenschap:</span><span class="sxs-lookup"><span data-stu-id="2efd9-210">When you add a password to a custom script extension, use the **commandToExecute** property in the **protectedSettings** property:</span></span>
   
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
   > <span data-ttu-id="2efd9-211">Om ervoor te zorgen dat de geheimen worden versleuteld wanneer ze als parameters worden doorgegeven aan VM's en -extensies, gebruiken de **protectedSettings** eigenschap van de relevante extensies.</span><span class="sxs-lookup"><span data-stu-id="2efd9-211">To ensure that secrets are encrypted when they are passed as parameters to VMs and extensions, use the **protectedSettings** property of the relevant extensions.</span></span>
   > 
   > 

## <a name="outputs"></a><span data-ttu-id="2efd9-212">uitvoer</span><span class="sxs-lookup"><span data-stu-id="2efd9-212">Outputs</span></span>
<span data-ttu-id="2efd9-213">Als u een sjabloon voor het openbare IP-adressen maken, voegt een **levert** sectie gegevens van het IP-adres en de volledig gekwalificeerde domeinnaam (FQDN retourneert).</span><span class="sxs-lookup"><span data-stu-id="2efd9-213">If you use a template to create public IP addresses, include an **outputs** section that returns details of the IP address and the fully qualified domain name (FQDN).</span></span> <span data-ttu-id="2efd9-214">Uitvoerwaarden kunt u eenvoudig ophalen van informatie over de openbare IP-adressen en FQDN's na de implementatie.</span><span class="sxs-lookup"><span data-stu-id="2efd9-214">You can use output values to easily retrieve details about public IP addresses and FQDNs after deployment.</span></span> <span data-ttu-id="2efd9-215">Wanneer u verwijst naar de resource, gebruikt u de API-versie die u hebt gebruikt om deze te maken:</span><span class="sxs-lookup"><span data-stu-id="2efd9-215">When you reference the resource, use the API version that you used to create it:</span></span> 

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

## <a name="single-template-vs-nested-templates"></a><span data-ttu-id="2efd9-216">Één sjabloon versus geneste sjablonen</span><span class="sxs-lookup"><span data-stu-id="2efd9-216">Single template vs. nested templates</span></span>
<span data-ttu-id="2efd9-217">Voor het implementeren van uw oplossing, kunt u één sjabloon of een belangrijkste sjabloon kunt gebruiken met meerdere geneste sjablonen.</span><span class="sxs-lookup"><span data-stu-id="2efd9-217">To deploy your solution, you can use either a single template or a main template with multiple nested templates.</span></span> <span data-ttu-id="2efd9-218">Geneste sjablonen gelden voor meer geavanceerde scenario's.</span><span class="sxs-lookup"><span data-stu-id="2efd9-218">Nested templates are common for more advanced scenarios.</span></span> <span data-ttu-id="2efd9-219">Met behulp van een geneste sjabloon biedt u de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="2efd9-219">Using a nested template gives you the following advantages:</span></span>

* <span data-ttu-id="2efd9-220">U kunt een oplossing in de betreffende onderdelen uitgesplitst.</span><span class="sxs-lookup"><span data-stu-id="2efd9-220">You can break down a solution into targeted components.</span></span>
* <span data-ttu-id="2efd9-221">U kunt geneste sjablonen met verschillende belangrijke sjablonen hergebruiken.</span><span class="sxs-lookup"><span data-stu-id="2efd9-221">You can reuse nested templates with different main templates.</span></span>

<span data-ttu-id="2efd9-222">Als u ervoor kiest om geneste sjablonen te gebruiken, kunt de volgende richtlijnen u uw sjabloonontwerp standaardiseren.</span><span class="sxs-lookup"><span data-stu-id="2efd9-222">If you choose to use nested templates, the following guidelines can help you standardize your template design.</span></span> <span data-ttu-id="2efd9-223">Deze richtlijnen zijn gebaseerd op [patronen voor Azure Resource Manager-sjablonen ontwerpen](best-practices-resource-manager-design-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2efd9-223">These guidelines are based on [patterns for designing Azure Resource Manager templates](best-practices-resource-manager-design-templates.md).</span></span> <span data-ttu-id="2efd9-224">U wordt aangeraden een ontwerp dat de volgende sjablonen bevat:</span><span class="sxs-lookup"><span data-stu-id="2efd9-224">We recommend a design that has the following templates:</span></span>

* <span data-ttu-id="2efd9-225">**Belangrijkste sjabloon** (azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="2efd9-225">**Main template** (azuredeploy.json).</span></span> <span data-ttu-id="2efd9-226">Gebruik dit voor de invoerparameters.</span><span class="sxs-lookup"><span data-stu-id="2efd9-226">Use for the input parameters.</span></span>
* <span data-ttu-id="2efd9-227">**Gedeelde bronnen sjabloon**.</span><span class="sxs-lookup"><span data-stu-id="2efd9-227">**Shared resources template**.</span></span> <span data-ttu-id="2efd9-228">Gebruiken voor het implementeren van gedeelde resources die gebruikmaken van alle andere bronnen (bijvoorbeeld virtuele-netwerk en beschikbaarheid sets).</span><span class="sxs-lookup"><span data-stu-id="2efd9-228">Use to deploy shared resources that all other resources use (for example, virtual network and availability sets).</span></span> <span data-ttu-id="2efd9-229">Gebruik de **dependsOn** expressie om ervoor te zorgen dat deze sjabloon wordt geïmplementeerd voordat andere sjablonen.</span><span class="sxs-lookup"><span data-stu-id="2efd9-229">Use the **dependsOn** expression to ensure that this template is deployed before other templates.</span></span>
* <span data-ttu-id="2efd9-230">**Optionele resources sjabloon**.</span><span class="sxs-lookup"><span data-stu-id="2efd9-230">**Optional resources template**.</span></span> <span data-ttu-id="2efd9-231">Gebruik voor het implementeren van voorwaardelijk bronnen op basis van een parameter (bijvoorbeeld een jumpbox).</span><span class="sxs-lookup"><span data-stu-id="2efd9-231">Use to conditionally deploy resources based on a parameter (for example, a jumpbox).</span></span>
* <span data-ttu-id="2efd9-232">**Lid resources sjabloon**.</span><span class="sxs-lookup"><span data-stu-id="2efd9-232">**Member resources template**.</span></span> <span data-ttu-id="2efd9-233">Elk exemplaartype binnen een toepassingslaag heeft een eigen configuratie.</span><span class="sxs-lookup"><span data-stu-id="2efd9-233">Each instance type within an application tier has its own configuration.</span></span> <span data-ttu-id="2efd9-234">Binnen een laag, kunt u een ander exemplaar typen definiëren.</span><span class="sxs-lookup"><span data-stu-id="2efd9-234">Within a tier, you can define different instance types.</span></span> <span data-ttu-id="2efd9-235">(Bijvoorbeeld de eerste instantie wordt gemaakt van een cluster en extra exemplaren worden toegevoegd aan het bestaande cluster.) Elk exemplaartype heeft een eigen sjabloon voor de implementatie.</span><span class="sxs-lookup"><span data-stu-id="2efd9-235">(For example, the first instance creates a cluster, and additional instances are added to the existing cluster.) Each instance type has its own deployment template.</span></span>
* <span data-ttu-id="2efd9-236">**Scripts**.</span><span class="sxs-lookup"><span data-stu-id="2efd9-236">**Scripts**.</span></span> <span data-ttu-id="2efd9-237">Algemeen herbruikbare scripts zijn van toepassing voor elk van exemplaartype (bijvoorbeeld, initialiseren en formatteren extra schijven).</span><span class="sxs-lookup"><span data-stu-id="2efd9-237">Widely reusable scripts are applicable for each instance type (for example, initialize and format additional disks).</span></span> <span data-ttu-id="2efd9-238">Aangepaste scripts die u voor een specifieke aanpassing doel maakt zijn verschillend, op basis van het type.</span><span class="sxs-lookup"><span data-stu-id="2efd9-238">Custom scripts that you create for a specific customization purpose are different, based on the instance type.</span></span>

![Geneste sjabloon](./media/resource-manager-template-best-practices/nestedTemplateDesign.png)

<span data-ttu-id="2efd9-240">Zie voor meer informatie [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2efd9-240">For more information, see [Use linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="conditionally-link-to-nested-templates"></a><span data-ttu-id="2efd9-241">Voorwaardelijk koppeling naar geneste sjablonen</span><span class="sxs-lookup"><span data-stu-id="2efd9-241">Conditionally link to nested templates</span></span>
<span data-ttu-id="2efd9-242">Een parameter kunt u voorwaardelijk koppelen aan geneste sjablonen.</span><span class="sxs-lookup"><span data-stu-id="2efd9-242">You can use a parameter to conditionally link to nested templates.</span></span> <span data-ttu-id="2efd9-243">De parameter maakt deel uit van de URI voor de sjabloon:</span><span class="sxs-lookup"><span data-stu-id="2efd9-243">The parameter becomes part of the URI for the template:</span></span>

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

## <a name="template-format"></a><span data-ttu-id="2efd9-244">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="2efd9-244">Template format</span></span>
<span data-ttu-id="2efd9-245">Het is raadzaam om door te geven van uw sjabloon via een JSON-validator.</span><span class="sxs-lookup"><span data-stu-id="2efd9-245">It's a good practice to pass your template through a JSON validator.</span></span> <span data-ttu-id="2efd9-246">Een validatiefunctie kunt u Verwijder overbodige komma's, haakjes en haakjes ertoe leiden een fout opgetreden tijdens de implementatie dat kunnen.</span><span class="sxs-lookup"><span data-stu-id="2efd9-246">A validator can help you remove extraneous commas, parentheses, and brackets that might cause an error during deployment.</span></span> <span data-ttu-id="2efd9-247">Probeer [JSONLint](http://jsonlint.com/) of een pakket linter voor uw favoriete omgeving (Visual Studio Code, Atom, Sublime tekst, Visual Studio) bewerken.</span><span class="sxs-lookup"><span data-stu-id="2efd9-247">Try [JSONLint](http://jsonlint.com/) or a linter package for your favorite editing environment (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span></span>

<span data-ttu-id="2efd9-248">Het is ook een goed idee om uw JSON voor een betere leesbaarheid.</span><span class="sxs-lookup"><span data-stu-id="2efd9-248">It's also a good idea to format your JSON for better readability.</span></span> <span data-ttu-id="2efd9-249">Voor uw lokale editor kunt u een pakket van JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="2efd9-249">You can use a JSON formatter package for your local editor.</span></span> <span data-ttu-id="2efd9-250">In Visual Studio om het document, drukt u op **Ctrl + K, Ctrl + D**.</span><span class="sxs-lookup"><span data-stu-id="2efd9-250">In Visual Studio, to format the document, press **Ctrl+K, Ctrl+D**.</span></span> <span data-ttu-id="2efd9-251">Druk in Visual Studio Code op **Alt + Shift + F**.</span><span class="sxs-lookup"><span data-stu-id="2efd9-251">In Visual Studio Code, press **Alt+Shift+F**.</span></span> <span data-ttu-id="2efd9-252">Als uw lokale editor het document niet opmaken, kunt u een [online formatter](https://www.bing.com/search?q=json+formatter).</span><span class="sxs-lookup"><span data-stu-id="2efd9-252">If your local editor doesn't format the document, you can use an [online formatter](https://www.bing.com/search?q=json+formatter).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2efd9-253">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2efd9-253">Next steps</span></span>
* <span data-ttu-id="2efd9-254">Zie voor instructies over het aanpassen van uw oplossing voor virtuele machines, [een virtuele machine van Windows worden uitgevoerd in Azure](../guidance/guidance-compute-single-vm.md) en [een Linux-VM in Azure uitvoeren](../guidance/guidance-compute-single-vm-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2efd9-254">For guidance on architecting your solution for virtual machines, see [Run a Windows VM in Azure](../guidance/guidance-compute-single-vm.md) and [Run a Linux VM in Azure](../guidance/guidance-compute-single-vm-linux.md).</span></span>
* <span data-ttu-id="2efd9-255">Zie voor instructies over het instellen van een opslagaccount [controlelijst voor prestaties en schaalbaarheid van Azure Storage](../storage/common/storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="2efd9-255">For guidance on setting up a storage account, see [Azure Storage performance and scalability checklist](../storage/common/storage-performance-checklist.md).</span></span>
* <span data-ttu-id="2efd9-256">Zie voor meer informatie over hoe een onderneming met Resource Manager effectief abonnementen wilt beheren, [Azure enterprise scaffold: Prescriptieve abonnement governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="2efd9-256">To learn about how an enterprise can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold: Prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

