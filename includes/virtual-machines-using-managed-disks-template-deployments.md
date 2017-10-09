# <a name="using-managed-disks-in-azure-resource-manager-templates"></a>Met beheerde-schijven in Azure Resource Manager-sjablonen

Dit document wordt uitgelegd Hallo verschillen tussen beheerde en onbeheerde schijven bij gebruik van Azure Resource Manager sjablonen tooprovision virtuele machines. Dit helpt u tooupdate bestaande sjablonen die van niet-beheerde schijven toomanaged schijven gebruikmaken. Ter referentie gebruiken we Hallo [101 vm-eenvoudige windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) sjabloon als richtlijn. U kunt zien Hallo sjabloon met zowel [schijven die worden beheerd](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) en het gebruik van een eerdere versie [schijven zonder begeleiding](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) als u wilt toodirectly vergelijken.

## <a name="unmanaged-disks-template-formatting"></a>Niet-beheerde schijven van sjabloon

toobegin, we een kijkje nemen op hoe niet-beheerde schijven zijn geïmplementeerd. Wanneer u niet-beheerde schijven maakt, moet u een storage account toohold Hallo VHD-bestanden. U kunt een nieuw opslagaccount maken of gebruiken dat al bestaat. In dit artikel wordt uitgelegd hoe u een nieuw opslagaccount toocreate. tooaccomplish, moet u een account opslagresource in Hallo resources blok zoals hieronder wordt weergegeven.

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

Binnen een object van de virtuele machine hello moeten we een afhankelijkheid op Hallo storage account tooensure waarvoor deze is gemaakt voordat Hallo virtuele machine. Binnen Hallo `storageProfile` sectie we geeft u de volledige URI van de locatie van de VHD, dat verwijst naar Hallo storage-account en is nodig voor Hallo OS-schijf en eventuele gegevensschijven Hallo Hallo. 

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

## <a name="managed-disks-template-formatting"></a>Beheerde opmaak van schijven

Met Azure beheerd schijven Hallo schijf wordt een bron op het hoogste niveau en vereist niet langer een storage account toobe gemaakt door gebruiker Hallo. Beheerde schijven zijn eerst worden weergegeven in Hallo `2016-04-30-preview` API-versie zijn beschikbaar in alle daaropvolgende API-versies en nu Hallo schijf standaardtype. Hallo volgende secties helpt bij de standaardinstellingen Hallo toegelicht en hoe toofurther aanpassen voor uw schijven.

> [!NOTE]
> Het verdient aanbeveling toouse een API-versie hoger dan `2016-04-30-preview` omdat er grote wijzigingen tussen `2016-04-30-preview` en `2017-03-30`.
>
>

### <a name="default-managed-disk-settings"></a>Standaard beheerde Schijfinstellingen

toocreate met beheerde schijven, u niet langer een virtuele machine moet toocreate hello opslagresource account en de bron van de virtuele machine kunt als volgt bijwerken. Specifiek Houd er rekening mee dat Hallo `apiVersion` weerspiegelt `2017-03-30` en Hallo `osDisk` en `dataDisks` niet langer verwijzen tooa specifieke URI voor Hallo VHD. Bij het implementeren zonder aanvullende eigenschappen, Hallo schijf gebruikt [standaard LRS opslag](../articles/storage/common/storage-redundancy.md). Als er geen naam is opgegeven, duurt het Hallo-indeling van `<VMName>_OsDisk_1_<randomstring>` voor Hallo OS-schijf en `<VMName>_disk<#>_<randomstring>` voor elke gegevensschijf. Azure disk encryption is standaard uitgeschakeld. opslaan in cache is lezen/schrijven voor Hallo OS-schijf en er is geen voor gegevensschijven. Merkt u wellicht in Hallo onderstaande voorbeeld dat is er nog steeds een afhankelijkheid van storage-account, maar dit alleen voor de opslag van diagnostische gegevens is en is niet nodig voor schijfopslag.

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

### <a name="using-a-top-level-managed-disk-resource"></a>Met behulp van een beheerde schijfbron op het hoogste niveau

U kunt als een alternatieve toospecifying Hallo schijfconfiguratie in het virtuele-machineobject hello, een schijfbron op het hoogste niveau maken en koppelen als onderdeel van Hallo virtuele machines worden gemaakt. We kunnen bijvoorbeeld een schijfbron als volgt toouse als een gegevensschijf maken.

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

We kunnen binnen Hallo VM-object, naar deze schijf object toobe gekoppeld verwijzen. Schijf wordt gemaakt in Hallo Hallo bron-ID van Hallo geven beheerde `managedDisk` eigenschap kunt Hallo koppelen van Hallo-schijf als Hallo virtuele machine wordt gemaakt. Houd er rekening mee dat Hallo `apiVersion` voor Hallo VM-resource is ingesteld, te`2017-03-30`. Houd er ook rekening mee dat we een afhankelijkheid op Hallo schijf resource tooensure die deze is gemaakt voordat het maken van VM's hebt gemaakt. 

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

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a>Beheerde beschikbaarheidssets maken met virtuele machines met beheerde schijven

toocreate beheerd beschikbaarheid sets met virtuele machines met beheerde schijven toevoegen Hallo `sku` object toohello beschikbaarheid resource ingesteld en de Hallo `name` eigenschap te`Aligned`. Dit zorgt ervoor dat Hallo schijven voor elke virtuele machine voldoende geïsoleerd van elkaar tooavoid individuele storingspunten zijn. Vergeet niet dat Hallo `apiVersion` hello beschikbaarheidsset resource is ingesteld dat te`2017-03-30`.

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

### <a name="additional-scenarios-and-customizations"></a>Aanvullende scenario's en aanpassingen

toofind volledige informatie over specificaties van de REST-API Hallo, bekijk Hallo [maken van een beheerde schijf REST API-documentatie](/rest/api/manageddisks/disks/disks-create-or-update). U vindt aanvullende scenario's, evenals standaard- en acceptabele waarden die verzonden toohello API via sjabloonimplementaties te maken worden kunnen. 

## <a name="next-steps"></a>Volgende stappen

* Ga naar hello Azure Quickstart-opslagplaats koppelingen volgen voor volledige-sjablonen die gebruikmaken van beheerde schijven.
    * [Windows-VM met beheerde-schijf](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [Linux-VM met beheerde-schijf](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [Volledige lijst met beheerde schijf-sjablonen](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* Ga naar Hallo [overzicht van Azure beheerde schijven](../articles/virtual-machines/windows/managed-disks-overview.md) document toolearn informatie over schijven die worden beheerd.
* Hallo sjabloon-naslagdocumentatie voor bronnen voor virtuele machines controleren door te bezoeken Hallo [Microsoft.Compute/virtualMachines sjabloonverwijzing](/templates/microsoft.compute/virtualmachines) document.
* Hallo-naslagdocumentatie voor schijfbronnen sjabloon bekijken via Hallo [Microsoft.Compute/disks sjabloonverwijzing](/templates/microsoft.compute/disks) document.
 
