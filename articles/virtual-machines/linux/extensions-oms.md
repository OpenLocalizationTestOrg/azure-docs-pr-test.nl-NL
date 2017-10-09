---
title: virtuele machine van Azure-extensie voor Linux aaaOMS | Microsoft Docs
description: Hallo OMS-agent op Linux virtuele machine met de extensie van een virtuele machine implementeren.
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7bbf210-7d71-4a37-ba47-9c74567a9ea6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 0fc8003d1fae6c043eef18ae78d12f9304b70832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a><span data-ttu-id="7aa39-103">Extensie van de virtuele machine OMS voor Linux</span><span class="sxs-lookup"><span data-stu-id="7aa39-103">OMS virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="7aa39-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="7aa39-104">Overview</span></span>

<span data-ttu-id="7aa39-105">Operations Management Suite (OMS) biedt mogelijkheden voor bewaking, waarschuwingen en waarschuwing herstel tussen cloud en on-premises activa.</span><span class="sxs-lookup"><span data-stu-id="7aa39-105">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="7aa39-106">Hallo OMS-Agent de extensie van de virtuele machine voor Linux is gepubliceerd en ondersteund door Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7aa39-106">hello OMS Agent virtual machine extension for Linux is published and supported by Microsoft.</span></span> <span data-ttu-id="7aa39-107">Hallo-extensie Hallo OMS-agent is geïnstalleerd op virtuele machines in Azure en virtuele machines in een bestaande OMS-werkruimte inschrijft.</span><span class="sxs-lookup"><span data-stu-id="7aa39-107">hello extension installs hello OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="7aa39-108">Dit document details Hallo ondersteund platforms, configuraties en implementatie-opties voor de extensie van de virtuele machine OMS Hallo voor Linux.</span><span class="sxs-lookup"><span data-stu-id="7aa39-108">This document details hello supported platforms, configurations, and deployment options for hello OMS virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7aa39-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7aa39-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="7aa39-110">Besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="7aa39-110">Operating system</span></span>

<span data-ttu-id="7aa39-111">Hallo-extensie OMS-Agent kan worden uitgevoerd op basis van deze Linux-distributies.</span><span class="sxs-lookup"><span data-stu-id="7aa39-111">hello OMS Agent extension can be run against these Linux distributions.</span></span>

| <span data-ttu-id="7aa39-112">Distributie</span><span class="sxs-lookup"><span data-stu-id="7aa39-112">Distribution</span></span> | <span data-ttu-id="7aa39-113">Versie</span><span class="sxs-lookup"><span data-stu-id="7aa39-113">Version</span></span> |
|---|---|
| <span data-ttu-id="7aa39-114">CentOS Linux</span><span class="sxs-lookup"><span data-stu-id="7aa39-114">CentOS Linux</span></span> | <span data-ttu-id="7aa39-115">5, 6 en 7</span><span class="sxs-lookup"><span data-stu-id="7aa39-115">5, 6, and 7</span></span> |
| <span data-ttu-id="7aa39-116">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="7aa39-116">Oracle Linux</span></span> | <span data-ttu-id="7aa39-117">5, 6 en 7</span><span class="sxs-lookup"><span data-stu-id="7aa39-117">5, 6, and 7</span></span> |
| <span data-ttu-id="7aa39-118">Red Hat Enterprise Linux Server</span><span class="sxs-lookup"><span data-stu-id="7aa39-118">Red Hat Enterprise Linux Server</span></span> | <span data-ttu-id="7aa39-119">5, 6 en 7</span><span class="sxs-lookup"><span data-stu-id="7aa39-119">5, 6 and 7</span></span> |
| <span data-ttu-id="7aa39-120">Debian GNU/Linux</span><span class="sxs-lookup"><span data-stu-id="7aa39-120">Debian GNU/Linux</span></span> | <span data-ttu-id="7aa39-121">6, 7 en 8</span><span class="sxs-lookup"><span data-stu-id="7aa39-121">6, 7, and 8</span></span> |
| <span data-ttu-id="7aa39-122">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="7aa39-122">Ubuntu</span></span> | <span data-ttu-id="7aa39-123">12.04 TNS, 14.04 TNS, 15.04, 15.10, 16.04 TNS</span><span class="sxs-lookup"><span data-stu-id="7aa39-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span></span> |
| <span data-ttu-id="7aa39-124">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="7aa39-124">SUSE Linux Enterprise Server</span></span> | <span data-ttu-id="7aa39-125">11 en 12</span><span class="sxs-lookup"><span data-stu-id="7aa39-125">11 and 12</span></span> |

### <a name="internet-connectivity"></a><span data-ttu-id="7aa39-126">Internetconnectiviteit</span><span class="sxs-lookup"><span data-stu-id="7aa39-126">Internet connectivity</span></span>

<span data-ttu-id="7aa39-127">Hallo-extensie OMS-Agent voor Linux is vereist dat Hallo doel-virtuele machine is verbonden toohello internet.</span><span class="sxs-lookup"><span data-stu-id="7aa39-127">hello OMS Agent extension for Linux requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="7aa39-128">Uitbreidingsschema</span><span class="sxs-lookup"><span data-stu-id="7aa39-128">Extension schema</span></span>

<span data-ttu-id="7aa39-129">Hallo toont volgende JSON Hallo-schema voor Hallo OMS-Agent-extensie.</span><span class="sxs-lookup"><span data-stu-id="7aa39-129">hello following JSON shows hello schema for hello OMS Agent extension.</span></span> <span data-ttu-id="7aa39-130">Hallo-uitbreiding vereist Hallo werkruimte-ID en werkruimte sleutel uit Hallo doel OMS-werkruimte. Deze waarden kunnen worden gevonden in Hallo OMS-portal.</span><span class="sxs-lookup"><span data-stu-id="7aa39-130">hello extension requires hello workspace ID and workspace key from hello target OMS workspace; these values can be found in hello OMS portal.</span></span> <span data-ttu-id="7aa39-131">Omdat Hallo werkruimtesleutel moet worden behandeld als gevoelige gegevens, moet deze worden opgeslagen in de configuratie van een beveiligde instelling.</span><span class="sxs-lookup"><span data-stu-id="7aa39-131">Because hello workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="7aa39-132">Azure VM-extensie beveiligde instellingsgegevens versleuteld en alleen op de virtuele doelmachine Hallo ontsleuteld.</span><span class="sxs-lookup"><span data-stu-id="7aa39-132">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span> <span data-ttu-id="7aa39-133">Houd er rekening mee dat **workspaceId** en **workspaceKey** zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="7aa39-133">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

### <a name="property-values"></a><span data-ttu-id="7aa39-134">Eigenschapswaarden</span><span class="sxs-lookup"><span data-stu-id="7aa39-134">Property values</span></span>

| <span data-ttu-id="7aa39-135">Naam</span><span class="sxs-lookup"><span data-stu-id="7aa39-135">Name</span></span> | <span data-ttu-id="7aa39-136">Waarde / voorbeeld</span><span class="sxs-lookup"><span data-stu-id="7aa39-136">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="7aa39-137">apiVersion</span><span class="sxs-lookup"><span data-stu-id="7aa39-137">apiVersion</span></span> | <span data-ttu-id="7aa39-138">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="7aa39-138">2015-06-15</span></span> |
| <span data-ttu-id="7aa39-139">Uitgever</span><span class="sxs-lookup"><span data-stu-id="7aa39-139">publisher</span></span> | <span data-ttu-id="7aa39-140">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="7aa39-140">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="7aa39-141">type</span><span class="sxs-lookup"><span data-stu-id="7aa39-141">type</span></span> | <span data-ttu-id="7aa39-142">OmsAgentForLinux</span><span class="sxs-lookup"><span data-stu-id="7aa39-142">OmsAgentForLinux</span></span> |
| <span data-ttu-id="7aa39-143">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="7aa39-143">typeHandlerVersion</span></span> | <span data-ttu-id="7aa39-144">1.4</span><span class="sxs-lookup"><span data-stu-id="7aa39-144">1.4</span></span> |
| <span data-ttu-id="7aa39-145">workspaceId (bijvoorbeeld)</span><span class="sxs-lookup"><span data-stu-id="7aa39-145">workspaceId (e.g)</span></span> | <span data-ttu-id="7aa39-146">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="7aa39-146">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="7aa39-147">workspaceKey (bijvoorbeeld)</span><span class="sxs-lookup"><span data-stu-id="7aa39-147">workspaceKey (e.g)</span></span> | <span data-ttu-id="7aa39-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI + rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ ==</span><span class="sxs-lookup"><span data-stu-id="7aa39-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="7aa39-149">Sjabloonimplementatie</span><span class="sxs-lookup"><span data-stu-id="7aa39-149">Template deployment</span></span>

<span data-ttu-id="7aa39-150">Azure VM-extensies kunnen worden geïmplementeerd met Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="7aa39-150">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="7aa39-151">Sjablonen zijn ideaal bij het implementeren van een of meer virtuele machines die na implementatieconfiguratie zoals onboarding tooOMS vereisen.</span><span class="sxs-lookup"><span data-stu-id="7aa39-151">Templates are ideal when deploying one or more virtual machines that require post deployment configuration such as onboarding tooOMS.</span></span> <span data-ttu-id="7aa39-152">Een voorbeeldsjabloon voor Resource Manager met OMS-Agent VM-extensie voor Hallo vindt u op Hallo [galerie van Azure Quick Start](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span><span class="sxs-lookup"><span data-stu-id="7aa39-152">A sample Resource Manager template that includes hello OMS Agent VM extension can be found on hello [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span></span> 

<span data-ttu-id="7aa39-153">Hallo JSON-configuratie voor de extensie van een virtuele machine worden genest in de bron van de virtuele machine Hallo of geplaatst op Hallo bovenste niveau van een Resource Manager JSON-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="7aa39-153">hello JSON configuration for a virtual machine extension can be nested inside hello virtual machine resource, or placed at hello root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="7aa39-154">Hallo plaatsing van Hallo JSON-configuratie is van invloed op Hallo-waarde van Hallo resourcenaam en het type.</span><span class="sxs-lookup"><span data-stu-id="7aa39-154">hello placement of hello JSON configuration affects hello value of hello resource name and type.</span></span> <span data-ttu-id="7aa39-155">Zie voor meer informatie [naam en type voor de onderliggende resources instellen](../../azure-resource-manager/resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="7aa39-155">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="7aa39-156">Hallo volgende voorbeeld wordt ervan uitgegaan Hallo OMS-extensie is genest binnen de bron van de virtuele machine Hallo.</span><span class="sxs-lookup"><span data-stu-id="7aa39-156">hello following example assumes hello OMS extension is nested inside hello virtual machine resource.</span></span> <span data-ttu-id="7aa39-157">Wanneer het nesten van Hallo extensie resource Hallo JSON wordt geplaatst in Hallo `"resources": []` object van het Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7aa39-157">When nesting hello extension resource, hello JSON is placed in hello `"resources": []` object of hello virtual machine.</span></span>

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

<span data-ttu-id="7aa39-158">Bij het plaatsen van Hallo extensie JSON aan Hallo basis van sjabloon hello, Hallo Resourcenaam bevat een verwijzing toohello bovenliggende virtuele machine en Hallo type reflecteert Hallo geneste configuratie.</span><span class="sxs-lookup"><span data-stu-id="7aa39-158">When placing hello extension JSON at hello root of hello template, hello resource name includes a reference toohello parent virtual machine, and hello type reflects hello nested configuration.</span></span>  

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "<parentVmResource>/OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

## <a name="azure-cli-deployment"></a><span data-ttu-id="7aa39-159">Azure CLI-implementatie</span><span class="sxs-lookup"><span data-stu-id="7aa39-159">Azure CLI deployment</span></span>

<span data-ttu-id="7aa39-160">Hello Azure CLI mag gebruikte toodeploy Hallo OMS-Agent VM-extensie tooan bestaande virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7aa39-160">hello Azure CLI can be used toodeploy hello OMS Agent VM extension tooan existing virtual machine.</span></span> <span data-ttu-id="7aa39-161">Vervangen door Hallo OMS-sleutel en OMS-ID die uit de OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="7aa39-161">Replace hello OMS key and OMS ID with those from your OMS workspace.</span></span> 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="7aa39-162">Oplossen van problemen en ondersteunen</span><span class="sxs-lookup"><span data-stu-id="7aa39-162">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="7aa39-163">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="7aa39-163">Troubleshoot</span></span>

<span data-ttu-id="7aa39-164">Gegevens over Hallo status van extensie-implementaties kunnen worden opgehaald uit hello Azure-portal en met behulp van hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="7aa39-164">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure CLI.</span></span> <span data-ttu-id="7aa39-165">Implementatiestatus van toosee Hallo van uitbreidingen voor een bepaalde virtuele machine Hallo volgende opdracht uitvoeren hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="7aa39-165">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure CLI.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="7aa39-166">Uitvoering van de extensie uitvoer volgt geregistreerde toohello bestand:</span><span class="sxs-lookup"><span data-stu-id="7aa39-166">Extension execution output is logged toohello following file:</span></span>

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a><span data-ttu-id="7aa39-167">Foutcodes en hun betekenis</span><span class="sxs-lookup"><span data-stu-id="7aa39-167">Error codes and their meanings</span></span>

| <span data-ttu-id="7aa39-168">Foutcode</span><span class="sxs-lookup"><span data-stu-id="7aa39-168">Error Code</span></span> | <span data-ttu-id="7aa39-169">Betekenis</span><span class="sxs-lookup"><span data-stu-id="7aa39-169">Meaning</span></span> | <span data-ttu-id="7aa39-170">Mogelijke actie</span><span class="sxs-lookup"><span data-stu-id="7aa39-170">Possible Action</span></span> |
| :---: | --- | --- |
| <span data-ttu-id="7aa39-171">10</span><span class="sxs-lookup"><span data-stu-id="7aa39-171">10</span></span> | <span data-ttu-id="7aa39-172">Virtuele machine is al verbonden tooan OMS-werkruimte</span><span class="sxs-lookup"><span data-stu-id="7aa39-172">VM is already connected tooan OMS workspace</span></span> | <span data-ttu-id="7aa39-173">tooconnect hello VM toohello werkruimte die is opgegeven in het Uitbreidingsschema hello, stopOnMultipleConnections toofalse instellen in instellingen voor openbare of verwijdert u deze eigenschap.</span><span class="sxs-lookup"><span data-stu-id="7aa39-173">tooconnect hello VM toohello workspace specified in hello extension schema, set stopOnMultipleConnections toofalse in public settings or remove this property.</span></span> <span data-ttu-id="7aa39-174">Deze virtuele machine opgehaald in rekening gebracht zodra voor elke werkruimte is verbonden met.</span><span class="sxs-lookup"><span data-stu-id="7aa39-174">This VM gets billed once for each workspace it is connected to.</span></span> |
| <span data-ttu-id="7aa39-175">11</span><span class="sxs-lookup"><span data-stu-id="7aa39-175">11</span></span> | <span data-ttu-id="7aa39-176">Ongeldige configuratie opgegeven toohello extensie</span><span class="sxs-lookup"><span data-stu-id="7aa39-176">Invalid config provided toohello extension</span></span> | <span data-ttu-id="7aa39-177">Ga als volgt Hallo voorgaande voorbeelden tooset alle eigenschapswaarden die nodig zijn voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="7aa39-177">Follow hello preceding examples tooset all property values necessary for deployment.</span></span> |
| <span data-ttu-id="7aa39-178">12</span><span class="sxs-lookup"><span data-stu-id="7aa39-178">12</span></span> | <span data-ttu-id="7aa39-179">Hallo dpkg Pakketbeheer is vergrendeld</span><span class="sxs-lookup"><span data-stu-id="7aa39-179">hello dpkg package manager is locked</span></span> | <span data-ttu-id="7aa39-180">Zorg ervoor dat alle dpkg update-bewerkingen op Hallo machine hebt opgegeven en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="7aa39-180">Make sure all dpkg update operations on hello machine have finished and retry.</span></span> |
| <span data-ttu-id="7aa39-181">20</span><span class="sxs-lookup"><span data-stu-id="7aa39-181">20</span></span> | <span data-ttu-id="7aa39-182">Voortijdig aangeroepen inschakelen</span><span class="sxs-lookup"><span data-stu-id="7aa39-182">Enable called prematurely</span></span> | <span data-ttu-id="7aa39-183">[Update hello Azure Linux Agent](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello meest recente versie.</span><span class="sxs-lookup"><span data-stu-id="7aa39-183">[Update hello Azure Linux Agent](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello latest available version.</span></span> |
| <span data-ttu-id="7aa39-184">51</span><span class="sxs-lookup"><span data-stu-id="7aa39-184">51</span></span> | <span data-ttu-id="7aa39-185">Deze extensie wordt niet ondersteund op Hallo van de virtuele machine als besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="7aa39-185">This extension is not supported on hello VM's operation system</span></span> | |
| <span data-ttu-id="7aa39-186">55</span><span class="sxs-lookup"><span data-stu-id="7aa39-186">55</span></span> | <span data-ttu-id="7aa39-187">Kan geen verbinding maken toohello Microsoft Operations Management Suite-service</span><span class="sxs-lookup"><span data-stu-id="7aa39-187">Cannot connect toohello Microsoft Operations Management Suite service</span></span> | <span data-ttu-id="7aa39-188">Controleer of Hallo systeem toegang heeft toegang tot Internet of een geldige HTTP-proxy is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="7aa39-188">Check that hello system either has Internet access, or that a valid HTTP proxy has been provided.</span></span> <span data-ttu-id="7aa39-189">Controleer daarnaast Hallo juistheid van Hallo werkruimte-ID.</span><span class="sxs-lookup"><span data-stu-id="7aa39-189">Additionally, check hello correctness of hello workspace ID.</span></span> |

<span data-ttu-id="7aa39-190">Extra informatie over probleemoplossing vindt u op Hallo [OMS-Agent voor Linux Troubleshooting Guide](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span><span class="sxs-lookup"><span data-stu-id="7aa39-190">Additional troubleshooting information can be found on hello [OMS-Agent-for-Linux Troubleshooting Guide](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span></span>

### <a name="support"></a><span data-ttu-id="7aa39-191">Ondersteuning</span><span class="sxs-lookup"><span data-stu-id="7aa39-191">Support</span></span>

<span data-ttu-id="7aa39-192">Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op Hallo [MSDN Azure en Stack Overflow-forums](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="7aa39-192">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="7aa39-193">U kunt ook een incident voor ondersteuning van Azure indienen.</span><span class="sxs-lookup"><span data-stu-id="7aa39-193">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="7aa39-194">Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/en-us/support/options/) en selecteer de Get-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="7aa39-194">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="7aa39-195">Lees voor informatie over het gebruik van de ondersteuning van Azure Hallo [ondersteuning van Microsoft Azure Veelgestelde vragen over](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="7aa39-195">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
