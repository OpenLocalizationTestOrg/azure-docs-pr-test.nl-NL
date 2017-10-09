---
title: Azure-resourcegroepen die VM-extensies bevatten aaaExporting | Microsoft Docs
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
ms.openlocfilehash: cdbc2030988a19fe68429e8733dc60536c264abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a><span data-ttu-id="71f7b-103">Exporteren van resourcegroepen met VM-extensies</span><span class="sxs-lookup"><span data-stu-id="71f7b-103">Exporting Resource Groups that contain VM extensions</span></span>

<span data-ttu-id="71f7b-104">Azure-resourcegroepen kunnen worden geëxporteerd naar een nieuwe Resource Manager-sjabloon die vervolgens kan worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="71f7b-104">Azure Resource Groups can be exported into a new Resource Manager template that can then be redeployed.</span></span> <span data-ttu-id="71f7b-105">Hallo exportproces interpreteert bestaande resources en Resource Manager-sjabloon maakt die bij de implementatie resulteert in een vergelijkbare resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="71f7b-105">hello export process interprets existing resources, and creates a Resource Manager template that when deployed results in a similar Resource Group.</span></span> <span data-ttu-id="71f7b-106">Wanneer u Hallo resourcegroep exportoptie tegen een bronnengroep met uitbreidingen van de virtuele Machine, worden de verschillende items moeten toobe beschouwd als zoals extensie compatibiliteit en beveiligde instellingen.</span><span class="sxs-lookup"><span data-stu-id="71f7b-106">When using hello Resource Group export option against a Resource Group containing Virtual Machine extensions, several items need toobe considered such as extension compatibility and protected settings.</span></span>

<span data-ttu-id="71f7b-107">De Documentdetails van dit hoe Hallo resourcegroep exportproces werkt met betrekking tot de virtuele machine extensies, met inbegrip van een lijst met ondersteunde extensies en meer informatie over de verwerking van beveiligde gegevens.</span><span class="sxs-lookup"><span data-stu-id="71f7b-107">This document details how hello Resource Group export process works regarding virtual machine extensions, including a list of supported extensions, and details on handling secured data.</span></span>

## <a name="supported-virtual-machine-extensions"></a><span data-ttu-id="71f7b-108">Ondersteunde virtuele machines-extensies</span><span class="sxs-lookup"><span data-stu-id="71f7b-108">Supported Virtual Machine Extensions</span></span>

<span data-ttu-id="71f7b-109">Er zijn veel uitbreidingen van de virtuele Machine beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="71f7b-109">Many Virtual Machine extensions are available.</span></span> <span data-ttu-id="71f7b-110">Niet alle uitbreidingen kunnen worden geëxporteerd naar een Resource Manager-sjabloon Hallo 'Automatiseringsscript' gebruiken.</span><span class="sxs-lookup"><span data-stu-id="71f7b-110">Not all extensions can be exported into a Resource Manager template using hello “Automation Script” feature.</span></span> <span data-ttu-id="71f7b-111">Als de extensie van een virtuele machine niet wordt ondersteund, moet deze toobe handmatig terug in de geëxporteerde sjabloon Hallo geplaatst.</span><span class="sxs-lookup"><span data-stu-id="71f7b-111">If a virtual machine extension is not supported, it needs toobe manually placed back into hello exported template.</span></span>

<span data-ttu-id="71f7b-112">Hallo kunnen volgende extensies worden geëxporteerd met Hallo automation script functie.</span><span class="sxs-lookup"><span data-stu-id="71f7b-112">hello following extensions can be exported with hello automation script feature.</span></span>

| <span data-ttu-id="71f7b-113">Toestelnummer</span><span class="sxs-lookup"><span data-stu-id="71f7b-113">Extension</span></span> ||||
|---|---|---|---|
| <span data-ttu-id="71f7b-114">Acronis back-up</span><span class="sxs-lookup"><span data-stu-id="71f7b-114">Acronis Backup</span></span> | <span data-ttu-id="71f7b-115">Datadog Windows-Agent</span><span class="sxs-lookup"><span data-stu-id="71f7b-115">Datadog Windows Agent</span></span> | <span data-ttu-id="71f7b-116">Patches voor Linux OS</span><span class="sxs-lookup"><span data-stu-id="71f7b-116">OS Patching For Linux</span></span> | <span data-ttu-id="71f7b-117">VM-momentopname Linux</span><span class="sxs-lookup"><span data-stu-id="71f7b-117">VM Snapshot Linux</span></span>
| <span data-ttu-id="71f7b-118">Back-up Acronis Linux</span><span class="sxs-lookup"><span data-stu-id="71f7b-118">Acronis Backup Linux</span></span> | <span data-ttu-id="71f7b-119">Docker-uitbreiding</span><span class="sxs-lookup"><span data-stu-id="71f7b-119">Docker Extension</span></span> | <span data-ttu-id="71f7b-120">Puppet-Agent</span><span class="sxs-lookup"><span data-stu-id="71f7b-120">Puppet Agent</span></span> |
| <span data-ttu-id="71f7b-121">BG Info</span><span class="sxs-lookup"><span data-stu-id="71f7b-121">Bg Info</span></span> | <span data-ttu-id="71f7b-122">DSC-extensie</span><span class="sxs-lookup"><span data-stu-id="71f7b-122">DSC Extension</span></span> | <span data-ttu-id="71f7b-123">Site 24 x 7 Apm inzicht</span><span class="sxs-lookup"><span data-stu-id="71f7b-123">Site 24x7 Apm Insight</span></span> |
| <span data-ttu-id="71f7b-124">BMC CTM Agent Linux</span><span class="sxs-lookup"><span data-stu-id="71f7b-124">BMC CTM Agent Linux</span></span> | <span data-ttu-id="71f7b-125">Dynatrace Linux</span><span class="sxs-lookup"><span data-stu-id="71f7b-125">Dynatrace Linux</span></span> | <span data-ttu-id="71f7b-126">24 x 7 Linux siteserver</span><span class="sxs-lookup"><span data-stu-id="71f7b-126">Site 24x7 Linux Server</span></span> |
| <span data-ttu-id="71f7b-127">BMC CTM Agent Windows</span><span class="sxs-lookup"><span data-stu-id="71f7b-127">BMC CTM Agent Windows</span></span> | <span data-ttu-id="71f7b-128">Dynatrace Windows</span><span class="sxs-lookup"><span data-stu-id="71f7b-128">Dynatrace Windows</span></span> | <span data-ttu-id="71f7b-129">24 x 7 Windows siteserver</span><span class="sxs-lookup"><span data-stu-id="71f7b-129">Site 24x7 Windows Server</span></span> |
| <span data-ttu-id="71f7b-130">Chef-Client</span><span class="sxs-lookup"><span data-stu-id="71f7b-130">Chef Client</span></span> | <span data-ttu-id="71f7b-131">HPE beveiliging toepassing Defender</span><span class="sxs-lookup"><span data-stu-id="71f7b-131">HPE Security Application Defender</span></span> | <span data-ttu-id="71f7b-132">Trend Micro DSA</span><span class="sxs-lookup"><span data-stu-id="71f7b-132">Trend Micro DSA</span></span> |
| <span data-ttu-id="71f7b-133">Aangepast Script</span><span class="sxs-lookup"><span data-stu-id="71f7b-133">Custom Script</span></span> | <span data-ttu-id="71f7b-134">IaaS Antimalware</span><span class="sxs-lookup"><span data-stu-id="71f7b-134">IaaS Antimalware</span></span> | <span data-ttu-id="71f7b-135">Trend Micro DSA Linux</span><span class="sxs-lookup"><span data-stu-id="71f7b-135">Trend Micro DSA Linux</span></span> |
| <span data-ttu-id="71f7b-136">Aangepaste scriptextensie</span><span class="sxs-lookup"><span data-stu-id="71f7b-136">Custom Script Extension</span></span> | <span data-ttu-id="71f7b-137">IaaS diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="71f7b-137">IaaS Diagnostics</span></span> | <span data-ttu-id="71f7b-138">Toegang voor Linux VM</span><span class="sxs-lookup"><span data-stu-id="71f7b-138">VM Access For Linux</span></span> |
| <span data-ttu-id="71f7b-139">Aangepast Script voor Linux</span><span class="sxs-lookup"><span data-stu-id="71f7b-139">Custom Script for Linux</span></span> | <span data-ttu-id="71f7b-140">Linux Chef-Client</span><span class="sxs-lookup"><span data-stu-id="71f7b-140">Linux Chef Client</span></span> | <span data-ttu-id="71f7b-141">Toegang voor Linux VM</span><span class="sxs-lookup"><span data-stu-id="71f7b-141">VM Access For Linux</span></span> |
| <span data-ttu-id="71f7b-142">Datadog Linux-Agent</span><span class="sxs-lookup"><span data-stu-id="71f7b-142">Datadog Linux Agent</span></span> | <span data-ttu-id="71f7b-143">Diagnose van Linux</span><span class="sxs-lookup"><span data-stu-id="71f7b-143">Linux Diagnostic</span></span> | <span data-ttu-id="71f7b-144">VM-momentopname</span><span class="sxs-lookup"><span data-stu-id="71f7b-144">VM Snapshot</span></span> |

## <a name="export-hello-resource-group"></a><span data-ttu-id="71f7b-145">Hallo resourcegroep exporteren</span><span class="sxs-lookup"><span data-stu-id="71f7b-145">Export hello Resource Group</span></span>

<span data-ttu-id="71f7b-146">tooexport een resourcegroep in een sjabloon voor herbruikbare voltooid Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="71f7b-146">tooexport a Resource Group into a reusable template, complete hello following steps:</span></span>

1. <span data-ttu-id="71f7b-147">Meld u aan toohello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="71f7b-147">Sign in toohello Azure portal</span></span>
2. <span data-ttu-id="71f7b-148">Klik op Hallo Hub-Menu, resourcegroepen</span><span class="sxs-lookup"><span data-stu-id="71f7b-148">On hello Hub Menu, click Resource Groups</span></span>
3. <span data-ttu-id="71f7b-149">Hallo doelresourcegroep in de lijst Hallo selecteren</span><span class="sxs-lookup"><span data-stu-id="71f7b-149">Select hello target resource group from hello list</span></span>
4. <span data-ttu-id="71f7b-150">Klik op Hallo resourcegroep blade Automation-Script</span><span class="sxs-lookup"><span data-stu-id="71f7b-150">In hello Resource Group blade, click Automation Script</span></span>

![Sjabloon exporteren](./media/extensions-export-templates/template-export.png)

<span data-ttu-id="71f7b-152">Hello Azure Resource Manager-script voor automatische produceert een Resource Manager-sjabloon, een parameterbestand en implementatie van verschillende voorbeeldscripts zoals PowerShell en Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="71f7b-152">hello Azure Resource Manager automations script produces a Resource Manager template, a parameters file, and several sample deployment scripts such as PowerShell and Azure CLI.</span></span> <span data-ttu-id="71f7b-153">Op dit moment Hallo geëxporteerde sjabloon kan worden gedownload met Hallo downloadknop toegevoegd als een nieuwe sjabloon toohello sjabloonbibliotheek of gedistribueerd met behulp van Hallo implementatieknop.</span><span class="sxs-lookup"><span data-stu-id="71f7b-153">At this point, hello exported template can be downloaded using hello download button, added as a new template toohello template library, or redeployed using hello deploy button.</span></span>

## <a name="configure-protected-settings"></a><span data-ttu-id="71f7b-154">Beveiligde instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="71f7b-154">Configure protected settings</span></span>

<span data-ttu-id="71f7b-155">Veel virtuele machine van Azure-extensies bevatten een beveiligde instellingen configuratie, waarbij gevoelige gegevens zoals referenties en configuratie tekenreeksen worden gecodeerd.</span><span class="sxs-lookup"><span data-stu-id="71f7b-155">Many Azure virtual machine extensions include a protected settings configuration, that encrypts sensitive data such as credentials and configuration strings.</span></span> <span data-ttu-id="71f7b-156">Beveiligde instellingen worden niet geëxporteerd met Hallo automatiseringsscript.</span><span class="sxs-lookup"><span data-stu-id="71f7b-156">Protected settings are not exported with hello automation script.</span></span> <span data-ttu-id="71f7b-157">Als nodig is, beveiligde instellingen toobe opnieuw in Hallo ingevoegd moeten geëxporteerd sjablonen.</span><span class="sxs-lookup"><span data-stu-id="71f7b-157">If necessary, protected settings need toobe reinserted into hello exported templated.</span></span>

### <a name="step-1---remove-template-parameter"></a><span data-ttu-id="71f7b-158">Stap 1 - sjabloonparameter verwijderen</span><span class="sxs-lookup"><span data-stu-id="71f7b-158">Step 1 - Remove template parameter</span></span>

<span data-ttu-id="71f7b-159">Wanneer Hallo die resourcegroep wordt geëxporteerd, een parameter één sjabloon wordt gemaakt tooprovide geëxporteerd een toohello waarde beveiligde instellingen.</span><span class="sxs-lookup"><span data-stu-id="71f7b-159">When hello Resource Group is exported, a single template parameter is created tooprovide a value toohello exported protected settings.</span></span> <span data-ttu-id="71f7b-160">Deze parameter kan worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="71f7b-160">This parameter can be removed.</span></span> <span data-ttu-id="71f7b-161">tooremove hello parameter bekijkt hello parameterlijst en Hallo-parameter die er ongeveer vergelijkbaar toothis JSON-voorbeeld uitziet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="71f7b-161">tooremove hello parameter, look through hello parameter list and delete hello parameter that looks similar toothis JSON example.</span></span>

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a><span data-ttu-id="71f7b-162">Stap 2: Get beveiligde eigenschappen</span><span class="sxs-lookup"><span data-stu-id="71f7b-162">Step 2 - Get protected settings properties</span></span>

<span data-ttu-id="71f7b-163">Omdat elk beveiligd instellen van een reeks vereiste eigenschappen heeft, moet een lijst van deze eigenschappen toobe verzameld.</span><span class="sxs-lookup"><span data-stu-id="71f7b-163">Because each protected setting has a set of required properties, a list of these properties need toobe gathered.</span></span> <span data-ttu-id="71f7b-164">Alle parameters van de configuratie van beveiligde Hallo vindt u in Hallo [Azure Resource Manager-schema op GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span><span class="sxs-lookup"><span data-stu-id="71f7b-164">Each parameter of hello protected settings configuration can be found in hello [Azure Resource Manager schema on GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span></span> <span data-ttu-id="71f7b-165">Dit schema bevat alleen de parametersets Hallo voor Hallo-uitbreidingen die worden vermeld in Hallo overzicht sectie van dit document.</span><span class="sxs-lookup"><span data-stu-id="71f7b-165">This schema only includes hello parameter sets for hello extensions listed in hello overview section of this document.</span></span> 

<span data-ttu-id="71f7b-166">Uit binnen Hallo schema-opslagplaats, zoeken naar Hallo desired-extensie voor dit voorbeeld `IaaSDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="71f7b-166">From within hello schema repository, search for hello desired extension, for this example `IaaSDiagnostics`.</span></span> <span data-ttu-id="71f7b-167">Eenmaal Hallo extensies `protectedSettings` object is gevonden, dient u elke parameter.</span><span class="sxs-lookup"><span data-stu-id="71f7b-167">Once hello extensions `protectedSettings` object has been located, take note of each parameter.</span></span> <span data-ttu-id="71f7b-168">In voorbeeld Hallo Hallo `IaasDiagnostic` uitbreiding, Hallo vereisen parameters zijn `storageAccountName`, `storageAccountKey`, en `storageAccountEndPoint`.</span><span class="sxs-lookup"><span data-stu-id="71f7b-168">In hello example of hello `IaasDiagnostic` extension, hello require parameters are `storageAccountName`, `storageAccountKey`, and `storageAccountEndPoint`.</span></span>

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

### <a name="step-3---re-create-hello-protected-configuration"></a><span data-ttu-id="71f7b-169">Stap 3 - Hallo beveiligd configuratie opnieuw maken</span><span class="sxs-lookup"><span data-stu-id="71f7b-169">Step 3 - Re-create hello protected configuration</span></span>

<span data-ttu-id="71f7b-170">Op Hallo van de geëxporteerde sjabloon, zoekt u `protectedSettings` en Hallo geëxporteerde beveiligde instellingsobject vervangen door een nieuwe met extensieparameters Hallo vereist en een waarde voor elk criterium.</span><span class="sxs-lookup"><span data-stu-id="71f7b-170">On hello exported template, search for `protectedSettings` and replace hello exported protected setting object with a new one that includes hello required extension parameters and a value for each one.</span></span>

<span data-ttu-id="71f7b-171">In voorbeeld Hallo Hallo `IaasDiagnostic` uitbreiding, Hallo nieuwe beveiligde instelling configuratie eruit zou Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="71f7b-171">In hello example of hello `IaasDiagnostic` extension, hello new protected setting configuration would look like hello following example:</span></span>

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

<span data-ttu-id="71f7b-172">Hallo eindextensie resource lijkt vergelijkbare toohello JSON-voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="71f7b-172">hello final extension resource looks similar toohello following JSON example:</span></span>

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

<span data-ttu-id="71f7b-173">Als u de sjabloon parameters tooprovide eigenschapswaarden, moeten deze toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="71f7b-173">If using template parameters tooprovide property values, these need toobe created.</span></span> <span data-ttu-id="71f7b-174">Als u Sjabloonparameters voor beveiligd waarden in te stellen maakt, ervoor toouse hello `SecureString` parametertype zodat gevoelige waarden zijn beveiligd.</span><span class="sxs-lookup"><span data-stu-id="71f7b-174">When creating template parameters for protected setting values, make sure toouse hello `SecureString` parameter type so that sensitive values are secured.</span></span> <span data-ttu-id="71f7b-175">Zie voor meer informatie over het gebruik van parameters [Azure Resource Manager-sjablonen samenstellen](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="71f7b-175">For more information on using parameters, see [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="71f7b-176">In voorbeeld Hallo Hallo `IaasDiagnostic` uitbreiding, Hallo volgende parameters zouden worden gemaakt in Hallo parameters sectie van Hallo Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="71f7b-176">In hello example of hello `IaasDiagnostic` extension, hello following parameters would be created in hello parameters section of hello Resource Manager template.</span></span>

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

<span data-ttu-id="71f7b-177">Hallo-sjabloon kan op dit moment worden geïmplementeerd met behulp van de implementatiemethode van een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="71f7b-177">At this point, hello template can be deployed using any template deployment method.</span></span>
