# <a name="using-managed-disks-in-azure-resource-manager-templates"></a><span data-ttu-id="5e70d-101">Met beheerde-schijven in Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="5e70d-101">Using Managed Disks in Azure Resource Manager Templates</span></span>

<span data-ttu-id="5e70d-102">Dit document helpt bij de verschillen tussen beheerde en onbeheerde schijven bij gebruik van Azure Resource Manager-sjablonen voor het inrichten van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="5e70d-102">This document walks through the differences between managed and unmanaged disks when using Azure Resource Manager templates to provision virtual machines.</span></span> <span data-ttu-id="5e70d-103">Dit helpt u bij te werken van bestaande sjablonen die van niet-beheerde schijven aan beheerde schijven gebruikmaken.</span><span class="sxs-lookup"><span data-stu-id="5e70d-103">This will help you to update existing templates that are using unmanaged Disks to managed disks.</span></span> <span data-ttu-id="5e70d-104">Ter referentie: we gebruiken de [101 vm-eenvoudige windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) sjabloon als richtlijn.</span><span class="sxs-lookup"><span data-stu-id="5e70d-104">For reference, we are using the [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) template as a guide.</span></span> <span data-ttu-id="5e70d-105">Ziet u de sjabloon met gebruik van beide [schijven die worden beheerd](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) en het gebruik van een eerdere versie [zonder begeleiding schijven](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) als u deze rechtstreeks te vergelijken.</span><span class="sxs-lookup"><span data-stu-id="5e70d-105">You can see the template using both [managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) and a prior version using [unmanaged disks](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) if you'd like to directly compare them.</span></span>

## <a name="unmanaged-disks-template-formatting"></a><span data-ttu-id="5e70d-106">Niet-beheerde schijven van sjabloon</span><span class="sxs-lookup"><span data-stu-id="5e70d-106">Unmanaged Disks template formatting</span></span>

<span data-ttu-id="5e70d-107">Om te beginnen, we een kijkje nemen op hoe niet-beheerde schijven zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="5e70d-107">To begin, we take a look at how unmanaged disks are deployed.</span></span> <span data-ttu-id="5e70d-108">Wanneer u niet-beheerde schijven maakt, moet u een opslagaccount voor de VHD-bestanden.</span><span class="sxs-lookup"><span data-stu-id="5e70d-108">When creating unmanaged disks, you need a storage account to hold the VHD files.</span></span> <span data-ttu-id="5e70d-109">U kunt een nieuw opslagaccount maken of gebruiken dat al bestaat.</span><span class="sxs-lookup"><span data-stu-id="5e70d-109">You can create a new storage account or use one that already exists.</span></span> <span data-ttu-id="5e70d-110">In dit artikel wordt beschreven hoe u een nieuw opslagaccount maken.</span><span class="sxs-lookup"><span data-stu-id="5e70d-110">This article will show you how to create a new storage account.</span></span> <span data-ttu-id="5e70d-111">Hiervoor moet u een resource van de storage-account in het blok resources zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5e70d-111">To accomplish this, you need a storage account resource in the resources block as shown below.</span></span>

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

<span data-ttu-id="5e70d-112">In de virtuele machine-object moet een afhankelijkheid van het opslagaccount om ervoor te zorgen dat deze gemaakt voordat de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="5e70d-112">Within the virtual machine object, we need a dependency on the storage account to ensure that it's created before the virtual machine.</span></span> <span data-ttu-id="5e70d-113">Binnen de `storageProfile` sectie we vervolgens geeft u de volledige URI van de VHD-locatie, die verwijst naar het storage-account en is nodig voor de besturingssysteemschijf en alle gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="5e70d-113">Within the `storageProfile` section, we then specify the full URI of the VHD location, which references the storage account and is needed for the OS disk and any data disks.</span></span> 

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

## <a name="managed-disks-template-formatting"></a><span data-ttu-id="5e70d-114">Beheerde opmaak van schijven</span><span class="sxs-lookup"><span data-stu-id="5e70d-114">Managed disks template formatting</span></span>

<span data-ttu-id="5e70d-115">Met Azure beheerd schijven, de schijf wordt een bron op het hoogste niveau en vereist niet langer een opslagaccount worden gemaakt door de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="5e70d-115">With Azure Managed Disks, the disk becomes a top-level resource and no longer requires a storage account to be created by the user.</span></span> <span data-ttu-id="5e70d-116">Beheerde schijven zijn eerst worden weergegeven in de `2016-04-30-preview` API-versie zijn beschikbaar in alle daaropvolgende API-versies en nu het type standaard schijf.</span><span class="sxs-lookup"><span data-stu-id="5e70d-116">Managed disks were first exposed in the `2016-04-30-preview` API version, they are available in all subsequent API versions and are now the default disk type.</span></span> <span data-ttu-id="5e70d-117">De volgende secties helpt bij de standaardinstellingen en details van het verder aanpassen van uw schijven.</span><span class="sxs-lookup"><span data-stu-id="5e70d-117">The following sections walk through the default settings and detail how to further customize your disks.</span></span>

> [!NOTE]
> <span data-ttu-id="5e70d-118">Het verdient aanbeveling gebruik van een API-versie hoger dan `2016-04-30-preview` omdat er grote wijzigingen tussen `2016-04-30-preview` en `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="5e70d-118">It is recommended to use an API version later than `2016-04-30-preview` as there were breaking changes between `2016-04-30-preview` and `2017-03-30`.</span></span>
>
>

### <a name="default-managed-disk-settings"></a><span data-ttu-id="5e70d-119">Standaard beheerde Schijfinstellingen</span><span class="sxs-lookup"><span data-stu-id="5e70d-119">Default managed disk settings</span></span>

<span data-ttu-id="5e70d-120">Als een virtuele machine maken met beheerde schijven, u niet langer te maken van de opslag resource-account en de bron van de virtuele machine kunt als volgt bijwerken.</span><span class="sxs-lookup"><span data-stu-id="5e70d-120">To create a VM with managed disks, you no longer need to create the storage account resource and can update your virtual machine resource as follows.</span></span> <span data-ttu-id="5e70d-121">Specifiek merk op dat de `apiVersion` weerspiegelt `2017-03-30` en de `osDisk` en `dataDisks` niet langer wordt verwijzen naar een specifieke URI voor de VHD.</span><span class="sxs-lookup"><span data-stu-id="5e70d-121">Specifically note that the `apiVersion` reflects `2017-03-30` and the `osDisk` and `dataDisks` no longer refer to a specific URI for the VHD.</span></span> <span data-ttu-id="5e70d-122">Bij het implementeren zonder aanvullende eigenschappen, de schijf gebruikt [standaard LRS opslag](../articles/storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="5e70d-122">When deploying without specifying additional properties, the disk will use [Standard LRS storage](../articles/storage/common/storage-redundancy.md).</span></span> <span data-ttu-id="5e70d-123">Als er geen naam is opgegeven, wordt de indeling van `<VMName>_OsDisk_1_<randomstring>` voor de besturingssysteemschijf en `<VMName>_disk<#>_<randomstring>` voor elke gegevensschijf.</span><span class="sxs-lookup"><span data-stu-id="5e70d-123">If no name is specified, it takes the format of `<VMName>_OsDisk_1_<randomstring>` for the OS disk and `<VMName>_disk<#>_<randomstring>` for each data disk.</span></span> <span data-ttu-id="5e70d-124">Azure disk encryption is standaard uitgeschakeld. opslaan in cache is lezen/schrijven voor de besturingssysteemschijf en er is geen voor gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="5e70d-124">By default, Azure disk encryption is disabled; caching is Read/Write for the OS disk and None for data disks.</span></span> <span data-ttu-id="5e70d-125">U merkt wellicht in het onderstaande voorbeeld dat is er nog steeds een afhankelijkheid van storage-account, maar dit alleen voor de opslag van diagnostische gegevens is en is niet nodig voor schijfopslag.</span><span class="sxs-lookup"><span data-stu-id="5e70d-125">You may notice in the example below there is still a storage account dependency, though this is only for storage of diagnostics and is not needed for disk storage.</span></span>

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

### <a name="using-a-top-level-managed-disk-resource"></a><span data-ttu-id="5e70d-126">Met behulp van een beheerde schijfbron op het hoogste niveau</span><span class="sxs-lookup"><span data-stu-id="5e70d-126">Using a top-level managed disk resource</span></span>

<span data-ttu-id="5e70d-127">U kunt als alternatief voor het opgeven van de schijfconfiguratie in het object van de virtuele machine maken van een schijfbron op het hoogste niveau en koppelt u dit als onderdeel van de virtuele machine wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5e70d-127">As an alternative to specifying the disk configuration in the virtual machine object, you can create a top-level disk resource and attach it as part of the virtual machine creation.</span></span> <span data-ttu-id="5e70d-128">We kunnen bijvoorbeeld een schijfbron als volgt om te gebruiken als een gegevensschijf maken.</span><span class="sxs-lookup"><span data-stu-id="5e70d-128">For example, we can create a disk resource as follows to use as a data disk.</span></span>

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

<span data-ttu-id="5e70d-129">We kunnen vervolgens binnen het VM-object verwijzen naar dit schijfobject moet worden gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="5e70d-129">Within the VM object, we can then reference this disk object to be attached.</span></span> <span data-ttu-id="5e70d-130">Het opgeven van de resource-ID van de beheerde schijf wordt gemaakt in de `managedDisk` eigenschap kan het koppelen van de schijf als de virtuele machine wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5e70d-130">Specifying the resource ID of the managed disk we created in the `managedDisk` property allows the attachment of the disk as the VM is created.</span></span> <span data-ttu-id="5e70d-131">Houd er rekening mee dat de `apiVersion` voor de virtuele machine resource is ingesteld op `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="5e70d-131">Note that the `apiVersion` for the VM resource is set to `2017-03-30`.</span></span> <span data-ttu-id="5e70d-132">Rekening mee dat er een afhankelijkheid van de schijfbron gemaakt om te controleren of dat deze is gemaakt voordat de virtuele machine is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5e70d-132">Also note that we've created a dependency on the disk resource to ensure it's successfully created before VM creation.</span></span> 

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

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a><span data-ttu-id="5e70d-133">Beheerde beschikbaarheidssets maken met virtuele machines met beheerde schijven</span><span class="sxs-lookup"><span data-stu-id="5e70d-133">Create managed availability sets with VMs using managed disks</span></span>

<span data-ttu-id="5e70d-134">Maken van beheerde beschikbaarheidssets met virtuele machines met beheerde schijven, het toevoegen van de `sku` -object op voor de beschikbaarheid van de resource ingesteld en de `name` eigenschap `Aligned`.</span><span class="sxs-lookup"><span data-stu-id="5e70d-134">To create managed availability sets with VMs using managed disks, add the `sku` object to the availability set resource and set the `name` property to `Aligned`.</span></span> <span data-ttu-id="5e70d-135">Dit zorgt ervoor dat de schijven voor elke virtuele machine voldoende los van elkaar te vermijden individuele storingspunten zijn.</span><span class="sxs-lookup"><span data-stu-id="5e70d-135">This ensures that the disks for each VM are sufficiently isolated from each other to avoid single points of failure.</span></span> <span data-ttu-id="5e70d-136">Merk ook op dat de `apiVersion` voor de bron van de beschikbaarheidsset is ingesteld op `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="5e70d-136">Also note that the `apiVersion` for the availability set resource is set to `2017-03-30`.</span></span>

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

### <a name="additional-scenarios-and-customizations"></a><span data-ttu-id="5e70d-137">Aanvullende scenario's en aanpassingen</span><span class="sxs-lookup"><span data-stu-id="5e70d-137">Additional scenarios and customizations</span></span>

<span data-ttu-id="5e70d-138">Als u wilt zoeken in volledige informatie over de REST-API-specificaties, Controleer de [maken van een beheerde schijf REST API-documentatie](/rest/api/manageddisks/disks/disks-create-or-update).</span><span class="sxs-lookup"><span data-stu-id="5e70d-138">To find full information on the REST API specifications, please review the [create a managed disk REST API documentation](/rest/api/manageddisks/disks/disks-create-or-update).</span></span> <span data-ttu-id="5e70d-139">U vindt aanvullende scenario's, evenals standaard- en acceptabele waarden die kunnen worden verzonden naar de API via sjabloonimplementaties te maken.</span><span class="sxs-lookup"><span data-stu-id="5e70d-139">You will find additional scenarios, as well as default and acceptable values that can be submitted to the API through template deployments.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5e70d-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5e70d-140">Next steps</span></span>

* <span data-ttu-id="5e70d-141">Ga naar de volgende koppelingen voor de Azure Quickstart-opslagplaats voor volledige-sjablonen die gebruikmaken van beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="5e70d-141">For full templates that use managed disks visit the following Azure Quickstart Repo links.</span></span>
    * [<span data-ttu-id="5e70d-142">Windows-VM met beheerde-schijf</span><span class="sxs-lookup"><span data-stu-id="5e70d-142">Windows VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [<span data-ttu-id="5e70d-143">Linux-VM met beheerde-schijf</span><span class="sxs-lookup"><span data-stu-id="5e70d-143">Linux VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [<span data-ttu-id="5e70d-144">Volledige lijst met beheerde schijf-sjablonen</span><span class="sxs-lookup"><span data-stu-id="5e70d-144">Full list of managed disk templates</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="5e70d-145">Ga naar de [overzicht van Azure schijven beheerd](../articles/virtual-machines/windows/managed-disks-overview.md) document voor meer informatie over beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="5e70d-145">Visit the [Azure Managed Disks Overview](../articles/virtual-machines/windows/managed-disks-overview.md) document to learn more about managed disks.</span></span>
* <span data-ttu-id="5e70d-146">De sjabloon-naslagdocumentatie voor bronnen voor virtuele machines controleren in via de [Microsoft.Compute/virtualMachines sjabloonverwijzing](/templates/microsoft.compute/virtualmachines) document.</span><span class="sxs-lookup"><span data-stu-id="5e70d-146">Review the template reference documentation for virtual machine resources by visiting the [Microsoft.Compute/virtualMachines template reference](/templates/microsoft.compute/virtualmachines) document.</span></span>
* <span data-ttu-id="5e70d-147">Bekijk de naslagdocumentatie over de sjabloon voor de schijfbronnen in via de [Microsoft.Compute/disks sjabloonverwijzing](/templates/microsoft.compute/disks) document.</span><span class="sxs-lookup"><span data-stu-id="5e70d-147">Review the template reference documentation for disk resources by visiting the [Microsoft.Compute/disks template reference](/templates/microsoft.compute/disks) document.</span></span>
 
