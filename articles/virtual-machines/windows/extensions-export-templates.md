---
title: Azure-resourcegroepen die VM-extensies bevatten exporteren | Microsoft Docs
description: Resource Manager-sjablonen met uitbreidingen van de virtuele machine exporteren.
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7f4e2ca6-f1c7-4f59-a2cc-8f63132de279
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: nepeters
ms.openlocfilehash: cc3c705f1c9123de75ced016a5b39eb1a86b0f73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a><span data-ttu-id="316bd-103">Exporteren van resourcegroepen met VM-extensies</span><span class="sxs-lookup"><span data-stu-id="316bd-103">Exporting Resource Groups that contain VM extensions</span></span>

<span data-ttu-id="316bd-104">Azure-resourcegroepen kunnen worden geëxporteerd naar een nieuwe Resource Manager-sjabloon die vervolgens kan worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="316bd-104">Azure Resource Groups can be exported into a new Resource Manager template that can then be redeployed.</span></span> <span data-ttu-id="316bd-105">Het exportproces interpreteert bestaande resources en Resource Manager-sjabloon maakt die bij de implementatie resulteert in een vergelijkbare resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="316bd-105">The export process interprets existing resources, and creates a Resource Manager template that when deployed results in a similar Resource Group.</span></span> <span data-ttu-id="316bd-106">Wanneer u de optie voor het exporteren van resourcegroep tegen een bronnengroep met uitbreidingen van de virtuele Machine, worden meerdere items moeten worden overwogen zoals extensie compatibiliteit en instellingen beveiligd.</span><span class="sxs-lookup"><span data-stu-id="316bd-106">When using the Resource Group export option against a Resource Group containing Virtual Machine extensions, several items need to be considered such as extension compatibility and protected settings.</span></span>

<span data-ttu-id="316bd-107">De Documentdetails van dit de werking van het exportproces resourcegroep met betrekking tot de virtuele machine extensies, met inbegrip van een lijst met extensies ondersteund en informatie over de verwerking van beveiligde gegevens.</span><span class="sxs-lookup"><span data-stu-id="316bd-107">This document details how the Resource Group export process works regarding virtual machine extensions, including a list of supported extensions, and details on handling secured data.</span></span>

## <a name="supported-virtual-machine-extensions"></a><span data-ttu-id="316bd-108">Ondersteunde virtuele machines-extensies</span><span class="sxs-lookup"><span data-stu-id="316bd-108">Supported Virtual Machine Extensions</span></span>

<span data-ttu-id="316bd-109">Er zijn veel uitbreidingen van de virtuele Machine beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="316bd-109">Many Virtual Machine extensions are available.</span></span> <span data-ttu-id="316bd-110">Niet alle uitbreidingen kunnen worden geëxporteerd naar een Resource Manager-sjabloon met de functie 'Automatiseringsscript'.</span><span class="sxs-lookup"><span data-stu-id="316bd-110">Not all extensions can be exported into a Resource Manager template using the “Automation Script” feature.</span></span> <span data-ttu-id="316bd-111">Als de extensie van een virtuele machine niet wordt ondersteund, moet deze handmatig terug in de geëxporteerde sjabloon worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="316bd-111">If a virtual machine extension is not supported, it needs to be manually placed back into the exported template.</span></span>

<span data-ttu-id="316bd-112">De volgende extensies kunnen met de functie voor automatisering script worden geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="316bd-112">The following extensions can be exported with the automation script feature.</span></span>

| <span data-ttu-id="316bd-113">Toestelnummer</span><span class="sxs-lookup"><span data-stu-id="316bd-113">Extension</span></span> ||||
|---|---|---|---|
| <span data-ttu-id="316bd-114">Acronis back-up</span><span class="sxs-lookup"><span data-stu-id="316bd-114">Acronis Backup</span></span> | <span data-ttu-id="316bd-115">Datadog Windows-Agent</span><span class="sxs-lookup"><span data-stu-id="316bd-115">Datadog Windows Agent</span></span> | <span data-ttu-id="316bd-116">Patches voor Linux OS</span><span class="sxs-lookup"><span data-stu-id="316bd-116">OS Patching For Linux</span></span> | <span data-ttu-id="316bd-117">VM-momentopname Linux</span><span class="sxs-lookup"><span data-stu-id="316bd-117">VM Snapshot Linux</span></span>
| <span data-ttu-id="316bd-118">Back-up Acronis Linux</span><span class="sxs-lookup"><span data-stu-id="316bd-118">Acronis Backup Linux</span></span> | <span data-ttu-id="316bd-119">Docker-uitbreiding</span><span class="sxs-lookup"><span data-stu-id="316bd-119">Docker Extension</span></span> | <span data-ttu-id="316bd-120">Puppet-Agent</span><span class="sxs-lookup"><span data-stu-id="316bd-120">Puppet Agent</span></span> |
| <span data-ttu-id="316bd-121">BG Info</span><span class="sxs-lookup"><span data-stu-id="316bd-121">Bg Info</span></span> | <span data-ttu-id="316bd-122">DSC-extensie</span><span class="sxs-lookup"><span data-stu-id="316bd-122">DSC Extension</span></span> | <span data-ttu-id="316bd-123">Site 24 x 7 Apm inzicht</span><span class="sxs-lookup"><span data-stu-id="316bd-123">Site 24x7 Apm Insight</span></span> |
| <span data-ttu-id="316bd-124">BMC CTM Agent Linux</span><span class="sxs-lookup"><span data-stu-id="316bd-124">BMC CTM Agent Linux</span></span> | <span data-ttu-id="316bd-125">Dynatrace Linux</span><span class="sxs-lookup"><span data-stu-id="316bd-125">Dynatrace Linux</span></span> | <span data-ttu-id="316bd-126">24 x 7 Linux siteserver</span><span class="sxs-lookup"><span data-stu-id="316bd-126">Site 24x7 Linux Server</span></span> |
| <span data-ttu-id="316bd-127">BMC CTM Agent Windows</span><span class="sxs-lookup"><span data-stu-id="316bd-127">BMC CTM Agent Windows</span></span> | <span data-ttu-id="316bd-128">Dynatrace Windows</span><span class="sxs-lookup"><span data-stu-id="316bd-128">Dynatrace Windows</span></span> | <span data-ttu-id="316bd-129">24 x 7 Windows siteserver</span><span class="sxs-lookup"><span data-stu-id="316bd-129">Site 24x7 Windows Server</span></span> |
| <span data-ttu-id="316bd-130">Chef-Client</span><span class="sxs-lookup"><span data-stu-id="316bd-130">Chef Client</span></span> | <span data-ttu-id="316bd-131">HPE beveiliging toepassing Defender</span><span class="sxs-lookup"><span data-stu-id="316bd-131">HPE Security Application Defender</span></span> | <span data-ttu-id="316bd-132">Trend Micro DSA</span><span class="sxs-lookup"><span data-stu-id="316bd-132">Trend Micro DSA</span></span> |
| <span data-ttu-id="316bd-133">Aangepast Script</span><span class="sxs-lookup"><span data-stu-id="316bd-133">Custom Script</span></span> | <span data-ttu-id="316bd-134">IaaS Antimalware</span><span class="sxs-lookup"><span data-stu-id="316bd-134">IaaS Antimalware</span></span> | <span data-ttu-id="316bd-135">Trend Micro DSA Linux</span><span class="sxs-lookup"><span data-stu-id="316bd-135">Trend Micro DSA Linux</span></span> |
| <span data-ttu-id="316bd-136">Aangepaste scriptextensie</span><span class="sxs-lookup"><span data-stu-id="316bd-136">Custom Script Extension</span></span> | <span data-ttu-id="316bd-137">IaaS diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="316bd-137">IaaS Diagnostics</span></span> | <span data-ttu-id="316bd-138">Toegang voor Linux VM</span><span class="sxs-lookup"><span data-stu-id="316bd-138">VM Access For Linux</span></span> |
| <span data-ttu-id="316bd-139">Aangepast Script voor Linux</span><span class="sxs-lookup"><span data-stu-id="316bd-139">Custom Script for Linux</span></span> | <span data-ttu-id="316bd-140">Linux Chef-Client</span><span class="sxs-lookup"><span data-stu-id="316bd-140">Linux Chef Client</span></span> | <span data-ttu-id="316bd-141">Toegang voor Linux VM</span><span class="sxs-lookup"><span data-stu-id="316bd-141">VM Access For Linux</span></span> |
| <span data-ttu-id="316bd-142">Datadog Linux-Agent</span><span class="sxs-lookup"><span data-stu-id="316bd-142">Datadog Linux Agent</span></span> | <span data-ttu-id="316bd-143">Diagnose van Linux</span><span class="sxs-lookup"><span data-stu-id="316bd-143">Linux Diagnostic</span></span> | <span data-ttu-id="316bd-144">VM-momentopname</span><span class="sxs-lookup"><span data-stu-id="316bd-144">VM Snapshot</span></span> |

## <a name="export-the-resource-group"></a><span data-ttu-id="316bd-145">De resourcegroep exporteren</span><span class="sxs-lookup"><span data-stu-id="316bd-145">Export the Resource Group</span></span>

<span data-ttu-id="316bd-146">Als u wilt een resourcegroep exporteren naar een herbruikbare sjabloon, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="316bd-146">To export a Resource Group into a reusable template, complete the following steps:</span></span>

1. <span data-ttu-id="316bd-147">Aanmelden bij Azure Portal</span><span class="sxs-lookup"><span data-stu-id="316bd-147">Sign in to the Azure portal</span></span>
2. <span data-ttu-id="316bd-148">Klik in het Menu Hub op resourcegroepen</span><span class="sxs-lookup"><span data-stu-id="316bd-148">On the Hub Menu, click Resource Groups</span></span>
3. <span data-ttu-id="316bd-149">Selecteer de doelresourcegroep in de lijst</span><span class="sxs-lookup"><span data-stu-id="316bd-149">Select the target resource group from the list</span></span>
4. <span data-ttu-id="316bd-150">Klik op de blade resourcegroep automatiseringsscript</span><span class="sxs-lookup"><span data-stu-id="316bd-150">In the Resource Group blade, click Automation Script</span></span>

![Sjabloon exporteren](./media/extensions-export-templates/template-export.png)

<span data-ttu-id="316bd-152">Het Azure Resource Manager-script voor automatische produceert een Resource Manager-sjabloon, een parameterbestand en implementatie van verschillende voorbeeldscripts zoals PowerShell en Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="316bd-152">The Azure Resource Manager automations script produces a Resource Manager template, a parameters file, and several sample deployment scripts such as PowerShell and Azure CLI.</span></span> <span data-ttu-id="316bd-153">De geëxporteerde sjabloon kan op dit moment worden gedownload met behulp van de downloadknop als een nieuwe sjabloon wordt toegevoegd aan de sjabloonbibliotheek of geïmplementeerd met behulp van de knop implementeren.</span><span class="sxs-lookup"><span data-stu-id="316bd-153">At this point, the exported template can be downloaded using the download button, added as a new template to the template library, or redeployed using the deploy button.</span></span>

## <a name="configure-protected-settings"></a><span data-ttu-id="316bd-154">Beveiligde instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="316bd-154">Configure protected settings</span></span>

<span data-ttu-id="316bd-155">Veel virtuele machine van Azure-extensies bevatten een beveiligde instellingen configuratie, waarbij gevoelige gegevens zoals referenties en configuratie tekenreeksen worden gecodeerd.</span><span class="sxs-lookup"><span data-stu-id="316bd-155">Many Azure virtual machine extensions include a protected settings configuration, that encrypts sensitive data such as credentials and configuration strings.</span></span> <span data-ttu-id="316bd-156">Beveiligde instellingen worden niet geëxporteerd met een automatiseringsscript.</span><span class="sxs-lookup"><span data-stu-id="316bd-156">Protected settings are not exported with the automation script.</span></span> <span data-ttu-id="316bd-157">Indien nodig, beveiligde instellingen moeten opnieuw worden ingevoegd in de geëxporteerde sjablonen.</span><span class="sxs-lookup"><span data-stu-id="316bd-157">If necessary, protected settings need to be reinserted into the exported templated.</span></span>

### <a name="step-1---remove-template-parameter"></a><span data-ttu-id="316bd-158">Stap 1 - sjabloonparameter verwijderen</span><span class="sxs-lookup"><span data-stu-id="316bd-158">Step 1 - Remove template parameter</span></span>

<span data-ttu-id="316bd-159">Als de resourcegroep wordt geëxporteerd, wordt een enkele sjabloonparameter gemaakt voor een waarde opgeven voor de geëxporteerde beveiligde instellingen.</span><span class="sxs-lookup"><span data-stu-id="316bd-159">When the Resource Group is exported, a single template parameter is created to provide a value to the exported protected settings.</span></span> <span data-ttu-id="316bd-160">Deze parameter kan worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="316bd-160">This parameter can be removed.</span></span> <span data-ttu-id="316bd-161">Verwijder de parameter, bekijk de parameterlijst en verwijderen van de parameter dat op dit JSON-voorbeeld lijkt.</span><span class="sxs-lookup"><span data-stu-id="316bd-161">To remove the parameter, look through the parameter list and delete the parameter that looks similar to this JSON example.</span></span>

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a><span data-ttu-id="316bd-162">Stap 2: Get beveiligde eigenschappen</span><span class="sxs-lookup"><span data-stu-id="316bd-162">Step 2 - Get protected settings properties</span></span>

<span data-ttu-id="316bd-163">Omdat elk beveiligd instellen van een reeks vereiste eigenschappen heeft, moet een lijst van deze eigenschappen worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="316bd-163">Because each protected setting has a set of required properties, a list of these properties need to be gathered.</span></span> <span data-ttu-id="316bd-164">Alle parameters van de configuratie van de beveiligde vindt u in de [Azure Resource Manager-schema op GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span><span class="sxs-lookup"><span data-stu-id="316bd-164">Each parameter of the protected settings configuration can be found in the [Azure Resource Manager schema on GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span></span> <span data-ttu-id="316bd-165">Dit schema bevat alleen de parametersets voor de uitbreidingen die worden vermeld in de sectie overzicht van dit document.</span><span class="sxs-lookup"><span data-stu-id="316bd-165">This schema only includes the parameter sets for the extensions listed in the overview section of this document.</span></span> 

<span data-ttu-id="316bd-166">Uit binnen de schema-opslagplaats, zoekt u de gewenste extensie voor dit voorbeeld `IaaSDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="316bd-166">From within the schema repository, search for the desired extension, for this example `IaaSDiagnostics`.</span></span> <span data-ttu-id="316bd-167">Eenmaal de extensies `protectedSettings` object is gevonden, dient u elke parameter.</span><span class="sxs-lookup"><span data-stu-id="316bd-167">Once the extensions `protectedSettings` object has been located, take note of each parameter.</span></span> <span data-ttu-id="316bd-168">In het voorbeeld van de `IaasDiagnostic` uitbreiding, de parameters zijn vereist `storageAccountName`, `storageAccountKey`, en `storageAccountEndPoint`.</span><span class="sxs-lookup"><span data-stu-id="316bd-168">In the example of the `IaasDiagnostic` extension, the require parameters are `storageAccountName`, `storageAccountKey`, and `storageAccountEndPoint`.</span></span>

```json
"protectedSettings": {
    "type": "object",
    "properties": {
        "storageAccountName": {
            "type": "string"
        },
        "storageAccountKey": {
            "type": "string"
        },
        "storageAccountEndPoint": {
            "type": "string"
        }
    },
    "required": [
        "storageAccountName",
        "storageAccountKey",
        "storageAccountEndPoint"
    ]
}
```

### <a name="step-3---re-create-the-protected-configuration"></a><span data-ttu-id="316bd-169">Stap 3: de configuratie van de beveiligde opnieuw maken</span><span class="sxs-lookup"><span data-stu-id="316bd-169">Step 3 - Re-create the protected configuration</span></span>

<span data-ttu-id="316bd-170">Op de geëxporteerde sjabloon en zoek naar `protectedSettings` en het geëxporteerde beveiligde instellingsobject vervangen door een nieuwe met de vereiste extensie-parameters en een waarde voor elk criterium.</span><span class="sxs-lookup"><span data-stu-id="316bd-170">On the exported template, search for `protectedSettings` and replace the exported protected setting object with a new one that includes the required extension parameters and a value for each one.</span></span>

<span data-ttu-id="316bd-171">In het voorbeeld van de `IaasDiagnostic` uitbreiding, de nieuwe configuratie van de instelling voor beveiligde eruit als in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="316bd-171">In the example of the `IaasDiagnostic` extension, the new protected setting configuration would look like the following example:</span></span>

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

<span data-ttu-id="316bd-172">De resource eindextensie lijkt op het volgende JSON-voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="316bd-172">The final extension resource looks similar to the following JSON example:</span></span>

```json
{
    "name": "Microsoft.Insights.VMDiagnosticsSettings",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "[variables('apiVersion')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "tags": {
        "displayName": "AzureDiagnostics"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
            "storageAccountName": "[parameters('storageAccountName')]",
            "storageAccountKey": "[parameters('storageAccountKey')]",
            "storageAccountEndPoint": "https://core.windows.net"
        }
    }
}
```

<span data-ttu-id="316bd-173">Als u Sjabloonparameters eigenschapswaarden opgeven, moeten deze worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="316bd-173">If using template parameters to provide property values, these need to be created.</span></span> <span data-ttu-id="316bd-174">Bij het maken van Sjabloonparameters voor beveiligd waarden in te stellen, moet u de `SecureString` parametertype zodat gevoelige waarden zijn beveiligd.</span><span class="sxs-lookup"><span data-stu-id="316bd-174">When creating template parameters for protected setting values, make sure to use the `SecureString` parameter type so that sensitive values are secured.</span></span> <span data-ttu-id="316bd-175">Zie voor meer informatie over het gebruik van parameters [Azure Resource Manager-sjablonen samenstellen](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="316bd-175">For more information on using parameters, see [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="316bd-176">In het voorbeeld van de `IaasDiagnostic` uitbreiding mag de volgende parameters moeten worden gemaakt in de sectie parameters van de Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="316bd-176">In the example of the `IaasDiagnostic` extension, the following parameters would be created in the parameters section of the Resource Manager template.</span></span>

```json
"storageAccountName": {
    "defaultValue": null,
    "type": "SecureString"
},
"storageAccountKey": {
    "defaultValue": null,
    "type": "SecureString"
}
```

<span data-ttu-id="316bd-177">De sjabloon kan op dit moment worden geïmplementeerd met behulp van de implementatiemethode van een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="316bd-177">At this point, the template can be deployed using any template deployment method.</span></span>
