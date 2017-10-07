---
title: schijven in Azure Resource Manager-sjablonen die worden beheerd aaaUsing | Microsoft Docs
description: Beschrijft hoe toouse beheerd misks in Azure Resource Manager-sjablonen
services: storage
documentationcenter: 
author: jboeshart
manager: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 06/01/2017
ms.author: jaboes
ms.openlocfilehash: ea83f4ed11acfd8f642dbc8331fa8cf077ef577c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-managed-disks-in-azure-resource-manager-templates"></a><span data-ttu-id="5fa0f-103">Met beheerde-schijven in Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="5fa0f-103">Using Managed Disks in Azure Resource Manager Templates</span></span>

<span data-ttu-id="5fa0f-104">Dit document wordt uitgelegd Hallo verschillen tussen beheerde en onbeheerde schijven bij gebruik van Azure Resource Manager sjablonen tooprovision virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-104">This document walks through hello differences between managed and unmanaged disks when using Azure Resource Manager templates tooprovision virtual machines.</span></span> <span data-ttu-id="5fa0f-105">Dit helpt u tooupdate bestaande sjablonen die van niet-beheerde schijven toomanaged schijven gebruikmaken.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-105">This will help you tooupdate existing templates that are using unmanaged Disks toomanaged disks.</span></span> <span data-ttu-id="5fa0f-106">Ter referentie gebruiken we Hallo [101 vm-eenvoudige windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) sjabloon als richtlijn.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-106">For reference, we are using hello [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) template as a guide.</span></span> <span data-ttu-id="5fa0f-107">U kunt zien Hallo sjabloon met zowel [schijven die worden beheerd](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) en het gebruik van een eerdere versie [schijven zonder begeleiding](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) als u wilt toodirectly vergelijken.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-107">You can see hello template using both [managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) and a prior version using [unmanaged disks](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) if you'd like toodirectly compare them.</span></span>

## <a name="unmanaged-disks-template-formatting"></a><span data-ttu-id="5fa0f-108">Niet-beheerde schijven van sjabloon</span><span class="sxs-lookup"><span data-stu-id="5fa0f-108">Unmanaged Disks template formatting</span></span>

<span data-ttu-id="5fa0f-109">toobegin, we een kijkje nemen op hoe niet-beheerde schijven zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-109">toobegin, we take a look at how unmanaged disks are deployed.</span></span> <span data-ttu-id="5fa0f-110">Wanneer u niet-beheerde schijven maakt, moet u een storage account toohold Hallo VHD-bestanden.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-110">When creating unmanaged disks, you need a storage account toohold hello VHD files.</span></span> <span data-ttu-id="5fa0f-111">U kunt een nieuw opslagaccount maken of gebruiken dat al bestaat.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-111">You can create a new storage account or use one that already exists.</span></span> <span data-ttu-id="5fa0f-112">In dit artikel wordt uitgelegd hoe u een nieuw opslagaccount toocreate.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-112">This article will show you how toocreate a new storage account.</span></span> <span data-ttu-id="5fa0f-113">tooaccomplish, moet u een account opslagresource in Hallo resources blok zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-113">tooaccomplish this, you need a storage account resource in hello resources block as shown below.</span></span>

```
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2016-01-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {}
}
```

<span data-ttu-id="5fa0f-114">Binnen een object van de virtuele machine hello moeten we een afhankelijkheid op Hallo storage account tooensure waarvoor deze is gemaakt voordat Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-114">Within hello virtual machine object, we need a dependency on hello storage account tooensure that it's created before hello virtual machine.</span></span> <span data-ttu-id="5fa0f-115">Binnen Hallo `storageProfile` sectie we geeft u de volledige URI van de locatie van de VHD, dat verwijst naar Hallo storage-account en is nodig voor Hallo OS-schijf en eventuele gegevensschijven Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-115">Within hello `storageProfile` section, we then specify hello full URI of hello VHD location, which references hello storage account and is needed for hello OS disk and any data disks.</span></span> 

```
{
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "name": "osdisk",
                "vhd": {
                    "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/osdisk.vhd')]"
                },
                "caching": "ReadWrite",
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "name": "datadisk1",
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "vhd": {
                        "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/datadisk1.vhd')]"
                    },
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

## <a name="managed-disks-template-formatting"></a><span data-ttu-id="5fa0f-116">Beheerde opmaak van schijven</span><span class="sxs-lookup"><span data-stu-id="5fa0f-116">Managed disks template formatting</span></span>

<span data-ttu-id="5fa0f-117">Met Azure beheerd schijven Hallo schijf wordt een bron op het hoogste niveau en vereist niet langer een storage account toobe gemaakt door gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-117">With Azure Managed Disks, hello disk becomes a top-level resource and no longer requires a storage account toobe created by hello user.</span></span> <span data-ttu-id="5fa0f-118">Beheerde schijven zijn eerst worden weergegeven in Hallo `2016-04-30-preview` API-versie zijn beschikbaar in alle daaropvolgende API-versies en nu Hallo schijf standaardtype.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-118">Managed disks were first exposed in hello `2016-04-30-preview` API version, they are available in all subsequent API versions and are now hello default disk type.</span></span> <span data-ttu-id="5fa0f-119">Hallo volgende secties helpt bij de standaardinstellingen Hallo toegelicht en hoe toofurther aanpassen voor uw schijven.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-119">hello following sections walk through hello default settings and detail how toofurther customize your disks.</span></span>

> [!NOTE]
> <span data-ttu-id="5fa0f-120">Het verdient aanbeveling toouse een API-versie hoger dan `2016-04-30-preview` omdat er grote wijzigingen tussen `2016-04-30-preview` en `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-120">It is recommended toouse an API version later than `2016-04-30-preview` as there were breaking changes between `2016-04-30-preview` and `2017-03-30`.</span></span>
>
>

### <a name="default-managed-disk-settings"></a><span data-ttu-id="5fa0f-121">Standaard beheerde Schijfinstellingen</span><span class="sxs-lookup"><span data-stu-id="5fa0f-121">Default managed disk settings</span></span>

<span data-ttu-id="5fa0f-122">toocreate met beheerde schijven, u niet langer een virtuele machine moet toocreate hello opslagresource account en de bron van de virtuele machine kunt als volgt bijwerken.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-122">toocreate a VM with managed disks, you no longer need toocreate hello storage account resource and can update your virtual machine resource as follows.</span></span> <span data-ttu-id="5fa0f-123">Specifiek Houd er rekening mee dat Hallo `apiVersion` weerspiegelt `2017-03-30` en Hallo `osDisk` en `dataDisks` niet langer verwijzen tooa specifieke URI voor Hallo VHD.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-123">Specifically note that hello `apiVersion` reflects `2017-03-30` and hello `osDisk` and `dataDisks` no longer refer tooa specific URI for hello VHD.</span></span> <span data-ttu-id="5fa0f-124">Bij het implementeren zonder aanvullende eigenschappen, Hallo schijf gebruikt [standaard LRS opslag](storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="5fa0f-124">When deploying without specifying additional properties, hello disk will use [Standard LRS storage](storage-redundancy.md).</span></span> <span data-ttu-id="5fa0f-125">Als er geen naam is opgegeven, duurt het Hallo-indeling van `<VMName>_OsDisk_1_<randomstring>` voor Hallo OS-schijf en `<VMName>_disk<#>_<randomstring>` voor elke gegevensschijf.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-125">If no name is specified, it takes hello format of `<VMName>_OsDisk_1_<randomstring>` for hello OS disk and `<VMName>_disk<#>_<randomstring>` for each data disk.</span></span> <span data-ttu-id="5fa0f-126">Azure disk encryption is standaard uitgeschakeld. opslaan in cache is lezen/schrijven voor Hallo OS-schijf en er is geen voor gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-126">By default, Azure disk encryption is disabled; caching is Read/Write for hello OS disk and None for data disks.</span></span> <span data-ttu-id="5fa0f-127">Merkt u wellicht in Hallo onderstaande voorbeeld dat is er nog steeds een afhankelijkheid van storage-account, maar dit alleen voor de opslag van diagnostische gegevens is en is niet nodig voor schijfopslag.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-127">You may notice in hello example below there is still a storage account dependency, though this is only for storage of diagnostics and is not needed for disk storage.</span></span>

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="using-a-top-level-managed-disk-resource"></a><span data-ttu-id="5fa0f-128">Met behulp van een beheerde schijfbron op het hoogste niveau</span><span class="sxs-lookup"><span data-stu-id="5fa0f-128">Using a top-level managed disk resource</span></span>

<span data-ttu-id="5fa0f-129">U kunt als een alternatieve toospecifying Hallo schijfconfiguratie in het virtuele-machineobject hello, een schijfbron op het hoogste niveau maken en koppelen als onderdeel van Hallo virtuele machines worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-129">As an alternative toospecifying hello disk configuration in hello virtual machine object, you can create a top-level disk resource and attach it as part of hello virtual machine creation.</span></span> <span data-ttu-id="5fa0f-130">We kunnen bijvoorbeeld een schijfbron als volgt toouse als een gegevensschijf maken.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-130">For example, we can create a disk resource as follows toouse as a data disk.</span></span>

```
{
    "type": "Microsoft.Compute/disks",
    "name": "[concat(variables('vmName'),'-datadisk1')]",
    "apiVersion": "2017-03-30",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "properties": {
        "creationData": {
            "createOption": "Empty"
        },
        "diskSizeGB": 1023
    }
}
```

<span data-ttu-id="5fa0f-131">We kunnen binnen Hallo VM-object, naar deze schijf object toobe gekoppeld verwijzen.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-131">Within hello VM object, we can then reference this disk object toobe attached.</span></span> <span data-ttu-id="5fa0f-132">Schijf wordt gemaakt in Hallo Hallo bron-ID van Hallo geven beheerde `managedDisk` eigenschap kunt Hallo koppelen van Hallo-schijf als Hallo virtuele machine wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-132">Specifying hello resource ID of hello managed disk we created in hello `managedDisk` property allows hello attachment of hello disk as hello VM is created.</span></span> <span data-ttu-id="5fa0f-133">Houd er rekening mee dat Hallo `apiVersion` voor Hallo VM-resource is ingesteld, te`2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-133">Note that hello `apiVersion` for hello VM resource is set too`2017-03-30`.</span></span> <span data-ttu-id="5fa0f-134">Houd er ook rekening mee dat we een afhankelijkheid op Hallo schijf resource tooensure die deze is gemaakt voordat het maken van VM's hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-134">Also note that we've created a dependency on hello disk resource tooensure it's successfully created before VM creation.</span></span> 

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]",
        "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "lun": 0,
                    "name": "[concat(variables('vmName'),'-datadisk1')]",
                    "createOption": "attach",
                    "managedDisk": {
                        "id": "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
                    }
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a><span data-ttu-id="5fa0f-135">Beheerde beschikbaarheidssets maken met virtuele machines met beheerde schijven</span><span class="sxs-lookup"><span data-stu-id="5fa0f-135">Create managed availability sets with VMs using managed disks</span></span>

<span data-ttu-id="5fa0f-136">toocreate beheerd beschikbaarheid sets met virtuele machines met beheerde schijven toevoegen Hallo `sku` object toohello beschikbaarheid resource ingesteld en de Hallo `name` eigenschap te`Aligned`.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-136">toocreate managed availability sets with VMs using managed disks, add hello `sku` object toohello availability set resource and set hello `name` property too`Aligned`.</span></span> <span data-ttu-id="5fa0f-137">Dit zorgt ervoor dat Hallo schijven voor elke virtuele machine voldoende geïsoleerd van elkaar tooavoid individuele storingspunten zijn.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-137">This ensures that hello disks for each VM are sufficiently isolated from each other tooavoid single points of failure.</span></span> <span data-ttu-id="5fa0f-138">Vergeet niet dat Hallo `apiVersion` hello beschikbaarheidsset resource is ingesteld dat te`2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-138">Also note that hello `apiVersion` for hello availability set resource is set too`2017-03-30`.</span></span>

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/availabilitySets",
    "location": "[resourceGroup().location]",
    "name": "[variables('avSetName')]",
    "properties": {
        "PlatformUpdateDomainCount": 3,
        "PlatformFaultDomainCount": 2
    },
    "sku": {
        "name": "Aligned"
    }
}
```

### <a name="additional-scenarios-and-customizations"></a><span data-ttu-id="5fa0f-139">Aanvullende scenario's en aanpassingen</span><span class="sxs-lookup"><span data-stu-id="5fa0f-139">Additional scenarios and customizations</span></span>

<span data-ttu-id="5fa0f-140">toofind volledige informatie over specificaties van de REST-API Hallo, bekijk Hallo [maken van een beheerde schijf REST API-documentatie](/rest/api/manageddisks/disks/disks-create-or-update).</span><span class="sxs-lookup"><span data-stu-id="5fa0f-140">toofind full information on hello REST API specifications, please review hello [create a managed disk REST API documentation](/rest/api/manageddisks/disks/disks-create-or-update).</span></span> <span data-ttu-id="5fa0f-141">U vindt aanvullende scenario's, evenals standaard- en acceptabele waarden die verzonden toohello API via sjabloonimplementaties te maken worden kunnen.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-141">You will find additional scenarios, as well as default and acceptable values that can be submitted toohello API through template deployments.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5fa0f-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5fa0f-142">Next steps</span></span>

* <span data-ttu-id="5fa0f-143">Ga naar hello Azure Quickstart-opslagplaats koppelingen volgen voor volledige-sjablonen die gebruikmaken van beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-143">For full templates that use managed disks visit hello following Azure Quickstart Repo links.</span></span>
    * [<span data-ttu-id="5fa0f-144">Windows-VM met beheerde-schijf</span><span class="sxs-lookup"><span data-stu-id="5fa0f-144">Windows VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [<span data-ttu-id="5fa0f-145">Linux-VM met beheerde-schijf</span><span class="sxs-lookup"><span data-stu-id="5fa0f-145">Linux VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [<span data-ttu-id="5fa0f-146">Volledige lijst met beheerde schijf-sjablonen</span><span class="sxs-lookup"><span data-stu-id="5fa0f-146">Full list of managed disk templates</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="5fa0f-147">Ga naar Hallo [overzicht van Azure beheerde schijven](storage-managed-disks-overview.md) document toolearn informatie over schijven die worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-147">Visit hello [Azure Managed Disks Overview](storage-managed-disks-overview.md) document toolearn more about managed disks.</span></span>
* <span data-ttu-id="5fa0f-148">Hallo sjabloon-naslagdocumentatie voor bronnen voor virtuele machines controleren door te bezoeken Hallo [Microsoft.Compute/virtualMachines sjabloonverwijzing](/templates/microsoft.compute/virtualmachines) document.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-148">Review hello template reference documentation for virtual machine resources by visiting hello [Microsoft.Compute/virtualMachines template reference](/templates/microsoft.compute/virtualmachines) document.</span></span>
* <span data-ttu-id="5fa0f-149">Hallo-naslagdocumentatie voor schijfbronnen sjabloon bekijken via Hallo [Microsoft.Compute/disks sjabloonverwijzing](/templates/microsoft.compute/disks) document.</span><span class="sxs-lookup"><span data-stu-id="5fa0f-149">Review hello template reference documentation for disk resources by visiting hello [Microsoft.Compute/disks template reference](/templates/microsoft.compute/disks) document.</span></span>
 
