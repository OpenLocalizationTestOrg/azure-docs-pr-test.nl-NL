
* [Snel een virtuele machine maken in Azure](#quick-create-a-vm-in-azure)
* [Een virtuele machine vanuit een sjabloon implementeren in Azure](#deploy-a-vm-in-azure-from-a-template)
* [Een virtuele machine vanuit een aangepaste installatiekopie maken](#create-a-custom-vm-image)
* [Een virtuele machine implementeren die gebruikmaakt van een virtueel netwerk en een load balancer](#deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer)
* [Een resourcegroep verwijderen](#remove-a-resource-group)
* [Hallo-logboek voor een implementatie van de groep resource weergeven](#show-the-log-for-a-resource-group-deployment)
* [Informatie weergeven over een virtuele machine](#display-information-about-a-virtual-machine)
* [Verbinding maken met tooa op basis van Linux virtuele machine](#log-on-to-a-linux-based-virtual-machine)
* [Een virtuele machine stoppen](#stop-a-virtual-machine)
* [Een virtuele machine starten](#start-a-virtual-machine)
* [Een gegevensschijf koppelen](#attach-a-data-disk)

## <a name="getting-ready"></a>Voorbereiding
Voordat u hello Azure CLI met Azure-resourcegroepen gebruiken kunt, moet u toohave Hallo rechts Azure CLI versie en een Azure-account. Als u geen hello Azure CLI [installeren](../articles/cli-install-nodejs.md).

### <a name="update-your-azure-cli-version-too090-or-later"></a>Bijwerken van uw Azure CLI versie too0.9.0 of hoger
Type `azure --version` toosee versie 0.9.0 of u al hebt geïnstalleerd of hoger.

```azurecli
azure --version
0.9.0 (node: 0.10.25)
```

Als uw versie is niet 0.9.0 of hoger, moet u tooupdate Hallo deze met behulp van een van de systeemeigen installatieprogramma's of via **npm** door `npm update -g azure-cli`.

U kunt ook Azure CLI uitvoeren als een Docker-container met behulp van de volgende Hallo [Docker-afbeelding](https://registry.hub.docker.com/u/microsoft/azure-cli/). Voer vanaf een Docker-host, Hallo volgende opdracht:

```bash
docker run -it microsoft/azure-cli
```

### <a name="set-your-azure-account-and-subscription"></a>Uw Azure-account en -abonnement instellen
Als u nog geen Azure-abonnement hebt, maar wel een MSDM-abonnement, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/). U kunt zich ook aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).

Nu [tooyour Azure-account interactief aanmelden](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) door `azure login` en hello wordt u gevraagd om een interactieve aanmelding ervaring tooyour Azure-account te volgen. 

> [!NOTE]
> Als u hebt een werk- of schoolaccount ID en u weet dat u hebt geen tweeledige verificatie is ingeschakeld, kunt u **ook** gebruiken `azure login -u` samen met de Hallo werk of school ID toolog in *zonder* een interactieve sessie. Als u niet een werk- of schoolaccount ID hebt, kunt u [maakt u een werk- of schoolaccount-id van uw persoonlijke Microsoft-account](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toolog in Hallo dezelfde manier.
>
>

Uw account kan meer dan één abonnement hebben. U kunt uw abonnementen weergeven door `azure account list` te typen. Dit ziet er mogelijk als volgt uit:

```azurecli
azure account list
info:    Executing command account list
data:    Name                              Id                                    Tenant Id                            Current
data:    --------------------------------  ------------------------------------  ------------------------------------  -------
data:    Contoso Admin                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  true
data:    Fabrikam dev                      xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Fabrikam test                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Contoso production                xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
```

Hallo huidige Azure-abonnement kunt u instellen door Hallo volgende te typen. Hallo abonnement naam of het Hallo-ID gebruiken met de gewenste toomanage Hallo-resources.

```azurecli
azure account set <subscription name or ID> true
```

### <a name="switch-toohello-azure-cli-resource-group-mode"></a>Toohello Azure CLI resource group-modus schakelen
Standaard hello Azure CLI in beheermodus Hallo-service wordt gestart (**asm** modus). Type hello tooswitch tooresource groepmodus te volgen.

```azurecli
azure config mode arm
```

## <a name="understanding-azure-resource-templates-and-resource-groups"></a>Informatie over resourcesjablonen en resourcegroepen in Azure
De meeste toepassingen worden gebouwd met een combinatie van verschillende resourcetypen (zoals een of meer virtuele machines en opslagaccounts, een SQL-database, een virtueel netwerk of een netwerk voor contentlevering). Hallo standaard Azure service management API en hello klassieke Azure-portal weergegeven deze items met een service door de service-benadering. Deze aanpak toodeploy, moet u Hallo afzonderlijke services afzonderlijk te beheren (of andere hulpprogramma's die doen vinden), en niet als één logische eenheid van de implementatie.

*Azure Resource Manager-sjablonen*, echter maken het mogelijk dat u toodeploy en deze verschillende resources beheren als één implementatie van de logische eenheid in een declaratieve manier. In plaats van imperatively waarin Azure welke toodeploy één opdracht na de andere, u uw hele implementatie in een JSON-bestand--alle Hallo bronnen en bijbehorende configuratie en implementatieparameters--beschrijven en u deze resources als een vertelt Azure toodeploy groep.

U kunt beheren Hallo algehele levenscyclus van resources met behulp van Azure CLI resource management-opdrachten voor het Hallo-groep:

* Stoppen, starten of alle resources binnen de groep Hallo Hallo tegelijk verwijderen.
* Op rollen gebaseerde toegangsbeheer (RBAC) regels toolock omlaag beveiligingsmachtigingen op deze toepassing.
* Controlebewerkingen uitvoeren.
* Aanvullende metagegevens toevoegen aan resources om ze beter bij te houden.

Ontdek meer over Azure-resourcegroepen en wat ze kunnen voor u doen in Hallo veel [overzicht van Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md). Als u geïnteresseerd bent in het ontwerpen van sjablonen, raadpleegt u [Azure Resource Manager-sjablonen maken](../articles/resource-group-authoring-templates.md).

## <a id="quick-create-a-vm-in-azure"></a>Taak: Snel een virtuele machine maken in Azure
Soms weet u welke installatiekopie die u nodig hebt, en moet u een virtuele machine vanuit die installatiekopie nu en u hebt geen belang te veel over Hallo infrastructuur--misschien hebt u tootest iets op een nieuwe virtuele machine. Als u wilt dat toouse hello `azure vm quick-create` opdracht en een virtuele machine en de infrastructuur Hallo argumenten nodig toocreate doorgeven.

Eerst maakt u een resourcegroep.

```azurecli
azure group create coreos-quick westus
info:    Executing command group create
+ Getting resource group coreos-quick
+ Creating resource group coreos-quick
info:    Created resource group coreos-quick
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick
data:    Name:                coreos-quick
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

Daarna hebt u een installatiekopie nodig. Zie toofind een afbeelding met hello Azure CLI [navigeren en het selecteren van installatiekopieën van virtuele machine van Azure met PowerShell en Azure CLI Hallo](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Voor dit artikel vindt u hier een korte lijst met populaire installatiekopieën. Voor deze quick-create gebruiken we de installatiekopie Stable van CoreOS.

> [!NOTE]
> Voor ComputeImageVersion, kunt u ook gewoon opgeven 'nieuwste' zoals Hallo parameter in beide sjabloontaal hello en in hello Azure CLI. Hierdoor kunt dat u tooalways Hallo meest recente patches en -versie op van de installatiekopie hello gebruiken zonder toomodify uw scripts of sjablonen. Dit wordt hieronder weergegeven.
>
>

| PublisherName | Aanbieding | Sku | Versie |
|:--- |:--- |:--- |:--- |
| OpenLogic |CentOS |7 |7.0.201503 |
| OpenLogic |CentOS |7.1 |7.1.201504 |
| CoreOS |CoreOS |Bèta |647.0.0 |
| CoreOS |CoreOS |Stabiel |633.1.0 |
| MicrosoftDynamicsNAV |DynamicsNAV |2015 |8.0.40459 |
| MicrosoftSharePoint |MicrosoftSharePointServer |2013 |1.0.0 |
| msopentech |Oracle-Database-12c-Weblogic-Server-12c |Standard |1.0.0 |
| msopentech |Oracle-Database-12c-Weblogic-Server-12c |Enterprise |1.0.0 |
| MicrosoftSQLServer |SQL2014-WS2012R2 |Enterprise-Optimized-for-DW |12.0.2430 |
| MicrosoftSQLServer |SQL2014-WS2012R2 |Enterprise-Optimized-for-OLTP |12.0.2430 |
| Canonical |UbuntuServer |12.04.5-LTS |12.04.201504230 |
| Canonical |UbuntuServer |14.04.2-LTS |14.04.201503090 |
| MicrosoftWindowsServer |WindowsServer |2012-Datacenter |3.0.201503 |
| MicrosoftWindowsServer |WindowsServer |2012-R2-Datacenter |4.0.201503 |
| MicrosoftWindowsServer |WindowsServer |Windows-Server-Technical-Preview |5.0.201504 |
| MicrosoftWindowsServerEssentials |WindowsServerEssentials |WindowsServerEssentials |1.0.141204 |
| MicrosoftWindowsServerHPCPack |WindowsServerHPCPack |2012R2 |4.3.4665 |

Maak uw virtuele machine door te voeren Hallo `azure vm quick-create` opdracht en gereed voor wordt Hallo prompts. Het ziet er ongeveer als volgt uit:

```azurecli
azure vm quick-create
info:    Executing command vm quick-create
Resource group name: coreos-quick
Virtual machine name: coreos
Location name: westus
Operating system Type [Windows, Linux]: linux
ImageURN (format: "publisherName:offer:skus:version"): coreos:coreos:stable:latest
User name: ops
Password: *********
Confirm password: *********
+ Looking up hello VM "coreos"
info:    Using hello VM Size "Standard_A1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Retrieving storage accounts
info:    Could not find any storage accounts in hello region "westus", trying toocreate new one
+ Creating storage account "cli9fd3fce49e9a9b3d14302" in "westus"
+ Looking up hello storage account cli9fd3fce49e9a9b3d14302
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
info:    An nic with given name "coreo-westu-1430261891570-nic" not found, creating a new one
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
info:    Preparing toocreate new virtual network and subnet
/ Creating a new virtual network "coreo-westu-1430261891570-vnet" [address prefix: "10.0.0.0/16"] with subnet "coreo-westu-1430261891570-sne+" [address prefix: "10.0.1.0/24"]
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
+ Looking up hello subnet "coreo-westu-1430261891570-snet" under hello virtual network "coreo-westu-1430261891570-vnet"
info:    Found public ip parameters, trying toosetup PublicIP profile
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
info:    PublicIP with given name "coreo-westu-1430261891570-pip" not found, creating a new one
+ Creating public ip "coreo-westu-1430261891570-pip"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
+ Creating NIC "coreo-westu-1430261891570-nic"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Creating VM "coreos"
+ Looking up hello VM "coreos"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Compute/virtualMachines/coreos
data:    ProvisioningState               :Succeeded
data:    Name                            :coreos
data:    Location                        :westus
data:    FQDN                            :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :coreos
data:        Offer                       :coreos
data:        Sku                         :stable
data:        Version                     :633.1.0
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :cli9fd3fce49e9a9b3d-os-1430261892283
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli9fd3fce49e9a9b3d14302.blob.core.windows.net/vhds/cli9fd3fce49e9a9b3d-os-1430261892283.vhd
data:
data:    OS Profile:
data:      Computer Name                 :coreos
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :false
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Network/networkInterfaces/coreo-westu-1430261891570-nic
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-30-72-E3
data:          Provisioning State        :Succeeded
data:          Name                      :coreo-westu-1430261891570-nic
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.1.4
data:            Public IP address       :104.40.24.124
data:            FQDN                    :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
info:    vm quick-create command OK
```

U kunt nu verdergaan met de nieuwe virtuele machine.

## <a id="deploy-a-vm-in-azure-from-a-template"></a>Taak: Een virtuele machine in Azure implementeren vanuit een sjabloon
Gebruik Hallo-instructies in deze secties toodeploy een nieuwe virtuele machine in Azure met behulp van een sjabloon met hello Azure CLI. Deze sjabloon maakt u één virtuele machine in een nieuw virtueel netwerk met één subnet en in tegenstelling tot `azure vm quick-create`, kunt u toodescribe wilt nauwkeurig en Herhaal deze zonder fouten. Dit is wat deze sjabloon maakt:

![](./media/virtual-machines-common-cli-deploy-templates/new-vm.png)

### <a name="step-1-examine-hello-json-file-for-hello-template-parameters"></a>Stap 1: Controleer Hallo JSON-bestand op Hallo Sjabloonparameters
Hier volgen Hallo inhoud van Hallo JSON-bestand voor Hallo-sjabloon. (Hallo-sjabloon bevindt zich ook in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)

Sjablonen zijn flexibele, dus Hallo designer hebt gekozen toogive veel van de parameters of worden gekozen toooffer slechts enkele door het maken van een sjabloon die meer kan worden opgelost. Open Hallo sjabloonbestand (in dit onderwerp heeft een inline sjabloon hieronder) in volgorde toocollect Hallo informatie moet u toopass Hallo sjabloon als parameters en onderzoeken Hallo **parameters** waarden.

In dit geval vraagt naar Hallo sjabloon hieronder:

* Een unieke naam voor het opslagaccount.
* De gebruikersnaam van een beheerder voor Hallo VM.
* Een wachtwoord.
* Een domeinnaam voor Hallo buiten world toouse.
* Een versienummer van Ubuntu Server. Er wordt slechts één nummer uit een lijst geaccepteerd.

Zie meer informatie over [vereisten voor gebruikersnaam en wachtwoord](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).

Als u op deze waarden besluit, kunt u bent klaar toocreate voor een groep en deze sjabloon implementeren in uw Azure-abonnement.

```json
{
"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"parameters": {
    "newStorageAccountName": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello storage account where hello virtual machine's disks will be placed."
    }
    },
    "adminUsername": {
    "type": "string",
    "metadata": {
        "description": "User name for hello virtual machine."
    }
    },
    "adminPassword": {
    "type": "securestring",
    "metadata": {
        "description": "Password for hello virtual machine."
    }
    },
    "dnsNameForPublicIP": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello public IP used tooaccess hello virtual machine."
    }
    },
    "ubuntuOSVersion": {
    "type": "string",
    "defaultValue": "14.04.2-LTS",
    "allowedValues": [
        "12.04.5-LTS",
        "14.04.2-LTS",
        "15.04"
    ],
    "metadata": {
        "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version. Allowed values: 12.04.5-LTS, 14.04.2-LTS, 15.04."
    }
    }
},
"variables": {
    "location": "West US",
    "imagePublisher": "Canonical",
    "imageOffer": "UbuntuServer",
    "OSDiskName": "osdiskforlinuxsimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyUbuntuVM",
    "vmSize": "Standard_D1",
    "virtualNetworkName": "MyVNET",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
},
"resources": [
    {
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[parameters('newStorageAccountName')]",
    "apiVersion": "2015-05-01-preview",
    "location": "[variables('location')]",
    "properties": {
        "accountType": "[variables('storageAccountType')]"
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/publicIPAddresses",
    "name": "[variables('publicIPAddressName')]",
    "location": "[variables('location')]",
    "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
        "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
        }
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[variables('virtualNetworkName')]",
    "location": "[variables('location')]",
    "properties": {
        "addressSpace": {
        "addressPrefixes": [
            "[variables('addressPrefix')]"
        ]
        },
        "subnets": [
        {
            "name": "[variables('subnetName')]",
            "properties": {
            "addressPrefix": "[variables('subnetPrefix')]"
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('nicName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
    ],
    "properties": {
        "ipConfigurations": [
        {
            "name": "ipconfig1",
            "properties": {
            "privateIPAllocationMethod": "Dynamic",
            "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
            },
            "subnet": {
                "id": "[variables('subnetRef')]"
            }
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', parameters('newStorageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
        "computername": "[variables('vmName')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
        "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('ubuntuOSVersion')]",
            "version": "latest"
        },
        "osDisk": {
            "name": "osdisk",
            "vhd": {
            "uri": "[concat('http://',parameters('newStorageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
        }
        },
        "networkProfile": {
        "networkInterfaces": [
            {
            "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
        ]
        }
    }
    }
]
}
```

### <a name="step-2-create-hello-virtual-machine-by-using-hello-template"></a>Stap 2: Hallo virtuele machine met behulp van Hallo-sjabloon maken
Zodra u de parameterwaarden gereed hebt, moet u een resourcegroep maken voor de sjabloonimplementatie van uw en implementeer vervolgens Hallo-sjabloon.

toocreate Hallo-resourcegroep, type `azure group create <group name> <location>` Hallo-naam van Hallo-groep die u wilt en Hallo datacenter locatie waarin u toodeploy. Dit gebeurt snel:

```azurecli
azure group create myResourceGroup westus
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

Nu toocreate Hallo implementatie, aanroep `azure group deployment create` en doorgeven:

* Hallo-sjabloonbestand (als u Hallo hierboven JSON tooa lokale sjabloonbestand opgeslagen).
* Een sjabloon URI (als u toopoint op Hallo-bestand in GitHub of enige andere webadres wilt).
* Hallo resourcegroep waarin u wilt dat toodeploy.
* Een optionele implementatienaam.

U zult na vragen aan gebruiker toosupply Hallo waarden van parameters in Hallo 'parameters' sectie van Hallo JSON-bestand. Wanneer u alle Hallo parameterwaarden hebt opgegeven, wordt uw implementatie begint.

Hier volgt een voorbeeld:

```azurecli
azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json myResourceGroup firstDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
newStorageAccountName: storageaccount
adminUsername: ops
adminPassword: password
dnsNameForPublicIP: newdomainname
```

U ontvangt Hallo type informatie op te volgen:

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "firstDeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
data:    DeploymentName     : firstDeployment
data:    ResourceGroupName  : myResourceGroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T07:53:55.1828878Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  -------------
data:    newStorageAccountName  String        storageaccount
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameForPublicIP     String        newdomainname
data:    ubuntuOSVersion        String        14.10
info:    group deployment create command OK
```


## <a id="create-a-custom-vm-image"></a>Taak: Een aangepaste VM-installatiekopie maken
U hebt gezien Hallo basisgebruik van sjablonen bovenstaande, dus Hallo nu kunnen we gebruiken vergelijkbaar instructies toocreate een aangepaste virtuele machine uit een specifieke VHD-bestand in Azure met behulp van een sjabloon via Azure CLI. Hier Hallo verschil is dat deze sjabloon maakt u één virtuele machine van een opgegeven virtuele harde schijf (VHD).

### <a name="step-1-examine-hello-json-file-for-hello-template"></a>Stap 1: Controleer Hallo JSON-bestand voor Hallo-sjabloon
Hier volgen Hallo inhoud van Hallo JSON-bestand voor Hallo-sjabloon die in deze sectie als voorbeeld wordt. (Hallo-sjabloon bevindt zich ook in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)

U moet opnieuw toofind Hallo gewenste waarden tooenter voor Hallo parameters waarvoor geen standaardwaarden. Bij het uitvoeren van Hallo `azure group deployment create` opdracht hello Azure CLI vraagt u tooenter die waarden.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters" : {
        "userImageStorageAccountName": {
            "type": "string",
            "defaultValue" : "userImageStorageAccountName"
        },
        "userImageStorageContainerName" : {
            "type" : "string",
            "defaultValue" : "userImageStorageContainerName"
        },
        "userImageVhdName" : {
            "type" : "string",
            "defaultValue" : "userImageVhdName"
        },
        "dnsNameForPublicIP" : {
            "type" : "string",
            "defaultValue": "uniqueDnsNameForPublicIP"
        },
        "adminUserName": {
            "type": "string"
        },
        "adminPassword": {
            "type": "securestring"
        },
        "osType" : {
            "type" : "string",
            "allowedValues" : [
                "windows",
                "linux"
            ]
        },
        "subscriptionId":{
            "type" : "string"
        },
        "location": {
            "type": "String",
            "defaultValue" : "West US"
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A2"
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue" : "myPublicIP"
        },
        "vmName": {
            "type": "string",
            "defaultValue" : "myVM"
        },
        "virtualNetworkName":{
            "type" : "string",
            "defaultValue" : "myVNET"
        },
        "nicName":{
            "type" : "string",
            "defaultValue":"myNIC"
        }
    },
    "variables": {
        "addressPrefix":"10.0.0.0/16",
        "subnet1Name": "Subnet-1",
        "subnet2Name": "Subnet-2",
        "subnet1Prefix" : "10.0.0.0/24",
        "subnet2Prefix" : "10.0.1.0/24",
        "publicIPAddressType" : "Dynamic",
        "vnetID":"[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",
        "subnet1Ref" : "[concat(variables('vnetID'),'/subnets/',variables('subnet1Name'))]",
        "userImageName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('userImageVhdName'))]",
        "osDiskVhdName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('vmName'),'osDisk.vhd')]"
    },
    "resources": [
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[parameters('publicIPAddressName')]",
        "location": "[parameters('location')]",
        "properties": {
            "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
            }
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/virtualNetworks",
        "name": "[parameters('virtualNetworkName')]",
        "location": "[parameters('location')]",
        "properties": {
        "addressSpace": {
            "addressPrefixes": [
            "[variables('addressPrefix')]"
            ]
        },
        "subnets": [
            {
            "name": "[variables('subnet1Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet1Prefix')]"
            }
            },
            {
            "name": "[variables('subnet2Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet2Prefix')]"
            }
            }
        ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/networkInterfaces",
        "name": "[parameters('nicName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]",
            "[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]"
        ],
        "properties": {
            "ipConfigurations": [
            {
                "name": "ipconfig1",
                "properties": {
                    "privateIPAllocationMethod": "Dynamic",
                    "publicIPAddress": {
                        "id": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]"
                    },
                    "subnet": {
                        "id": "[variables('subnet1Ref')]"
                    }
                }
            }
            ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Compute/virtualMachines",
        "name": "[parameters('vmName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/networkInterfaces/', parameters('nicName'))]"
        ],
        "properties": {
            "hardwareProfile": {
                "vmSize": "[parameters('vmSize')]"
            },
            "osProfile": {
                "computername": "[parameters('vmName')]",
                "adminUsername": "[parameters('adminUsername')]",
                "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
                "osDisk" : {
                    "name" : "[concat(parameters('vmName'),'-osDisk')]",
                    "osType" : "[parameters('osType')]",
                    "caching" : "ReadWrite",
                    "image" : {
                        "uri" : "[variables('userImageName')]"
                    },
                    "vhd" : {
                        "uri" : "[variables('osDiskVhdName')]"
                    }
                }
            },
            "networkProfile": {
                "networkInterfaces" : [
                {
                    "id": "[resourceId('Microsoft.Network/networkInterfaces',parameters('nicName'))]"
                }
                ]
            }
        }
    }
    ]
}
```

### <a name="step-2-obtain-hello-vhd"></a>Stap 2: Hallo VHD verkrijgen
Uiteraard hebt u hier een .VHD-bestand voor nodig. U kunt een bestand gebruiken dat zich al in Azure bevindt, maar u kunt er ook een uploaden.

Zie voor een Windows-virtuele machine, [maken en uploaden van een Windows Server-VHD tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Zie voor een op basis van Linux virtuele machine, [maken en uploaden van een virtuele harde schijf waarop Linux-besturingssysteem Hallo](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

### <a name="step-3-create-hello-virtual-machine-by-using-hello-template"></a>Stap 3: Hallo virtuele machine met behulp van Hallo-sjabloon maken
Nu bent u klaar toocreate een nieuwe virtuele machine op basis van Hallo VHD. Maken van een groep toodeploy in, met behulp van `azure group create <location>`:

```azurecli
azure group create myResourceGroupUser eastus
info:    Executing command group create
+ Getting resource group myResourceGroupUser
+ Creating resource group myResourceGroupUser
info:    Created resource group myResourceGroupUser
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupUser
data:    Name:                myResourceGroupUser
data:    Location:            eastus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

Hallo-implementatie maakt met behulp van Hallo `--template-uri` optie toocall in rechtstreeks Hallo-sjabloon (of kunt u Hallo `--template-file` optie toouse een bestand dat u lokaal hebt opgeslagen). Houd er rekening mee dat omdat Hallo sjabloon de standaardinstellingen heeft, u wordt gevraagd om slechts een paar dingen. Als u de sjabloon Hallo op verschillende plaatsen implementeert, kunt u wellicht dat sommige naming conflicten optreden met standaardwaarden hello (Hallo met name een u maken van DNS-naam).

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json \
> myResourceGroup \
> customVhdDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
adminUserName: ops
adminPassword: password
osType: linux
subscriptionId: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

Uitvoer ziet er ongeveer als volgt Hallo volgende uit:

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "customVhdDeployment"
+ Registering providers
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
error:   Deployment provisioning state was not successful
data:    DeploymentName     : customVhdDeployment
data:    ResourceGroupName  : myResourceGroupUser
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T14:55:48.0963829Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                           Type          Value
data:    -----------------------------  ------------  ------------------------------------
data:    userImageStorageAccountName    String        userImageStorageAccountName
data:    userImageStorageContainerName  String        userImageStorageContainerName
data:    userImageVhdName               String        userImageVhdName
data:    dnsNameForPublicIP             String        uniqueDnsNameForPublicIP
data:    adminUserName                  String        ops
data:    adminPassword                  SecureString  undefined
data:    osType                         String        linux
data:    subscriptionId                 String        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
data:    location                       String        West US
data:    vmSize                         String        Standard_A2
data:    publicIPAddressName            String        myPublicIP
data:    vmName                         String        myVM
data:    virtualNetworkName             String        myVNET
data:    nicName                        String        myNIC
info:    group deployment create command OK
```

## <a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Taak: Een multi-VM-toepassing implementeren die gebruikmaakt van een virtueel netwerk en een externe load balancer
Deze sjabloon kunt u twee virtuele machines onder een load balancer toocreate en configureren van een regel voor load balancing op poort 80. Deze sjabloon implementeert ook een opslagaccount, een virtueel netwerk, een openbaar IP-adres, een beschikbaarheidsset en netwerkinterfaces.

![](./media/virtual-machines-common-cli-deploy-templates/multivmextlb.png)

Volg deze stappen toodeploy een multi-VM-toepassing die gebruikmaakt van een virtueel netwerk en een load balancer met een Resource Manager-sjabloon in Hallo GitHub-opslagplaats voor sjabloon via Azure PowerShell-opdrachten.

### <a name="step-1-examine-hello-json-file-for-hello-template"></a>Stap 1: Controleer Hallo JSON-bestand voor Hallo-sjabloon
Hier volgen Hallo inhoud van Hallo JSON-bestand voor Hallo-sjabloon. Als u wilt dat de meest recente versie hello, het gevonden [in GitHub-opslagplaats voor sjablonen Hallo](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json). In dit onderwerp maakt gebruik van Hallo `--template-uri` switch toocall in Hallo-sjabloon, maar u kunt ook Hallo `--template-file` overschakelen toopass een lokale versie.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "location": {
            "type": "string",
            "metadata": {
                "description": "Location of resources"
            }
        },
        "storageAccountName": {
            "type": "string",
            "metadata": {
                "description": "Name of storage account"
            }
        },
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "Admin user name"
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Admin password"
            }
        },
        "dnsNameforLBIP": {
            "type": "string",
            "metadata": {
                "description": "DNS for load balancer IP"
            }
        },
        "backendPort": {
            "type": "int",
            "defaultValue": 3389,
            "metadata": {
                "description": "Back-end port"
            }
        },
        "vmNamePrefix": {
            "type": "string",
            "defaultValue": "myVM",
            "metadata": {
                "description": "Prefix toouse for VM names"
            }
        },
        "vmSourceImageName": {
            "type": "string",
            "defaultValue": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201412.01-en.us-127GB.vhd"
        },
        "lbName": {
            "type": "string",
            "defaultValue": "myLB",
            "metadata": {
                "description": "Load balancer name"
            }
        },
        "nicNamePrefix": {
            "type": "string",
            "defaultValue": "nic",
            "metadata": {
                "description": "Network interface name prefix"
            }
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue": "myPublicIP",
            "metadata": {
                "description": "Public IP name"
            }
        },
        "vnetName": {
            "type": "string",
            "defaultValue": "myVNET",
            "metadata": {
                "description": "Virtual network name"
            }
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A1",
            "metadata": {
                "description": "Size of hello VM"
            }
        }
    },
    "variables": {
        "storageAccountType": "Standard_LRS",
        "vmStorageAccountContainerName": "vhds",
        "availabilitySetName": "myAvSet",
        "addressPrefix": "10.0.0.0/16",
        "subnetName": "Subnet-1",
        "subnetPrefix": "10.0.0.0/24",
        "publicIPAddressType": "Dynamic",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('vnetName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables ('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',parameters('lbName'))]",
        "numberOfInstances": 2,
        "nicId1": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 0))]",
        "nicId2": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 1))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/LBFE')]",
        "backEndIPConfigID1": "[concat(variables('nicId1'),'/ipConfigurations/ipconfig1')]",
        "backEndIPConfigID2": "[concat(variables('nicId2'),'/ipConfigurations/ipconfig1')]",
        "sourceImageName": "[concat('/', subscription().subscriptionId,'/services/images/',parameters('vmSourceImageName'))]",
        "lbPoolID": "[concat(variables('lbID'),'/backendAddressPools/LBBE')]",
        "lbProbeID": "[concat(variables('lbID'),'/probes/tcpProbe')]"
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('storageAccountName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": { }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/publicIPAddresses",
            "name": "[parameters('publicIPAddressName')]",
            "location": "[parameters('location')]",
            "properties": {
                "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
                "dnsSettings": {
                    "domainNameLabel": "[parameters('dnsNameforLBIP')]"
                }
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/virtualNetworks",
            "name": "[parameters('vnetName')]",
            "location": "[parameters('location')]",
            "properties": {
                "addressSpace": {
                    "addressPrefixes": [
                        "[variables('addressPrefix')]"
                    ]
                },
                "subnets": [
                    {
                        "name": "[variables('subnetName')]",
                        "properties": {
                            "addressPrefix": "[variables('subnetPrefix')]"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/networkInterfaces",
            "name": "[concat(parameters('nicNamePrefix'), copyindex())]",
            "location": "[parameters('location')]",
            "copy": {
                "name": "nicLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "dependsOn": [
                "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
            ],
            "properties": {
                "ipConfigurations": [
                    {
                        "name": "ipconfig1",
                        "properties": {
                            "privateIPAllocationMethod": "Dynamic",
                            "subnet": {
                                "id": "[variables('subnetRef')]"
                            }
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/backendAddressPools/LBBE')]"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/inboundNatRule/RDP-VM', copyindex())]"
                            }
                        ]


                    }
                ]

            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "name": "[parameters('lbName')]",
            "type": "Microsoft.Network/loadBalancers",
            "location": "[parameters('location')]",
            "dependsOn": [
                "nicLoop",
                "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]"
            ],
            "properties": {
                "frontendIPConfigurations": [
                    {
                        "name": "LBFE",
                        "properties": {
                            "publicIPAddress": {
                                "id": "[variables('publicIPAddressID')]"
                            }
                        }
                    }
                ],
                "backendAddressPools": [
                    {
                        "name": "LBBE"

                    }
                ],
                "inboundNatRules": [
                    {
                        "name": "RDP-VM1",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50001,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    },
                    {
                        "name": "RDP-VM2",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50002,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    }
                ],
                "loadBalancingRules": [
                    {
                        "name": "LBRule",
                        "properties": {
                            "frontendIPConfiguration": {
                                "id": "[variables('frontEndIPConfigID')]"
                            },
                            "backendAddressPool": {
                                "id": "[variables('lbPoolID')]"
                            },
                            "protocol": "tcp",
                            "frontendPort": 80,
                            "backendPort": 80,
                            "enableFloatingIP": false,
                            "idleTimeoutInMinutes": 5,
                            "probe": {
                                "id": "[variables('lbProbeID')]"
                            }
                        }
                    }
                ],
                "probes": [
                    {
                        "name": "tcpProbe",
                        "properties": {
                            "protocol": "tcp",
                            "port": 80,
                            "intervalInSeconds": "5",
                            "numberOfProbes": "2"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Compute/virtualMachines",
            "name": "[concat(parameters('vmNamePrefix'), copyindex())]",
            "copy": {
                "name": "virtualMachineLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "location": "[parameters('location')]",
            "dependsOn": [
                "[concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName'))]",
                "[concat('Microsoft.Network/networkInterfaces/', parameters('nicNamePrefix'), copyindex())]",
                "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]"
            ],
            "properties": {
                "availabilitySet": {
                    "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
                },
                "hardwareProfile": {
                    "vmSize": "[parameters('vmSize')]"
                },
                "osProfile": {
                    "computername": "[concat(parameters('vmNamePrefix'), copyIndex())]",
                    "adminUsername": "[parameters('adminUsername')]",
                    "adminPassword": "[parameters('adminPassword')]"
                },
                "storageProfile": {
                    "sourceImage": {
                        "id": "[variables('sourceImageName')]"
                    },
                    "destinationVhdsContainer": "[concat('http://',parameters('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/')]"
                },
                "networkProfile": {
                    "networkInterfaces": [
                        {
                            "id": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'),copyindex()))]"
                        }
                    ]
                }
            }
        }
    ]
}
```

### <a name="step-2-create-hello-deployment-by-using-hello-template"></a>Stap 2: Hallo-implementatie met behulp van Hallo-sjabloon maken
Een resourcegroep voor Hallo-sjabloon maken met behulp van `azure group create <location>`. Maak vervolgens een implementatie in die resourcegroep via `azure group deployment create` en resourcegroep hello wordt doorgegeven, de naam van een toepassingsimplementatie wordt doorgegeven en Hallo vragen beantwoorden voor parameters in Hallo-sjabloon die geen standaardwaarden.

```azurecli
azure group create lbgroup westus
info:    Executing command group create
+ Getting resource group lbgroup
+ Creating resource group lbgroup
info:    Created resource group lbgroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/lbgroup
data:    Name:                lbgroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

Gebruik nu Hallo `azure group deployment create` opdracht en Hallo `--template-uri` optie toodeploy Hallo sjabloon. Geef uw parameterwaarden op wanneer hierom wordt gevraagd, zoals hieronder weergegeven.

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json \
> lbgroup \
> newdeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
location: westus
newStorageAccountName: storagename
adminUsername: ops
adminPassword: password
dnsNameforLBIP: lbdomainname
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "newdeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.compute
info:    Registering provider microsoft.network
+ Waiting for deployment toocomplete
data:    DeploymentName     : newdeployment
data:    ResourceGroupName  : lbgroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T20:58:40.1678876Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  ----------------------
data:    location               String        westus
data:    newStorageAccountName  String        storagename
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameforLBIP         String        lbdomainname
data:    backendPort            Int           3389
data:    vmNamePrefix           String        myVM
data:    imagePublisher         String        MicrosoftWindowsServer
data:    imageOffer             String        WindowsServer
data:    imageSKU               String        2012-R2-Datacenter
data:    lbName                 String        myLB
data:    nicNamePrefix          String        nic
data:    publicIPAddressName    String        myPublicIP
data:    vnetName               String        myVNET
data:    vmSize                 String        Standard_A1
info:    group deployment create command OK
```

Met deze sjabloon implementeert u een installatiekopie van Windows Server. Deze kan echter eenvoudig worden vervangen door een installatiekopie van Linux. Wilt u toocreate een Docker-cluster met meerdere swarm managers? [Ook dat is mogelijk](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).

## <a id="remove-a-resource-group"></a>Taak: Een resourcegroep verwijderen
Houd er rekening mee dat u de resourcegroep tooa kunt implementeren, maar als u klaar bent met een, u deze verwijderen met behulp van kunt `azure group delete <group name>`.

```azurecli
azure group delete myResourceGroup
info:    Executing command group delete
Delete resource group myResourceGroup? [y/n] y
+ Deleting resource group myResourceGroup
info:    group delete command OK
```

## <a id="show-the-log-for-a-resource-group-deployment"></a>Taak: Hallo-logboek voor een implementatie van de groep resource weergeven
Dit is een veelvoorkomende bewerking wanneer u sjablonen maakt of gebruikt. Hallo aanroep toodisplay Hallo implementatie-logboeken voor een groep is `azure group log show <groupname>`, die heel wat informatie die nuttig zijn om te begrijpen waarom iets is er gebeurd-- of niet wordt weergegeven. (Zie [Veelvoorkomende fouten bij de Azure-implementatie oplossen met Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md) voor meer informatie over het oplossen van problemen met uw implementaties, evenals andere informatie over problemen.)

specifieke problemen met tootarget bijvoorbeeld, kunt u hulpprogramma's zoals **jq** tooquery dingen iets meer nauwkeurig, zoals welke afzonderlijke fouten u toocorrect nodig. Hallo volgende voorbeeld wordt **jq** tooparse Meld u een implementatie voor **lbgroup**zoek zijn naar fouten.

```azurecli
azure group log show lbgroup -l --json | jq '.[] | select(.status.value == "Failed") | .properties'
```
U kunt zeer snel ontdekken wat er mis ging, het probleem herstellen en het opnieuw proberen. Hallo geval te volgen, Hallo sjabloon had is maakt in twee virtuele machines op Hallo hetzelfde moment die een vergrendeling op Hallo VHD gemaakt. (Nadat we Hallo sjabloon hebt gewijzigd, Hallo implementatie is voltooid snel.)

```json
{
    "statusCode": "Conflict",
    "statusMessage": "{\"status\":\"Failed\",\"error\":{\"code\":\"ResourceDeploymentFailure\",\"message\":\"hello resource operation completed with terminal provisioning state 'Failed'.\",\"details\":[{\"code\":\"AcquireDiskLeaseFailed\",\"message\":\"Failed tooacquire lease while creating disk 'osdisk' using blob with URI http://storage.blob.core.windows.net/vhds/osdisk.vhd.\"}]}}"
}
```

## <a id="display-information-about-a-virtual-machine"></a>Taak: Informatie weergeven over een virtuele machine
U kunt informatie over specifieke virtuele machines in de resourcegroep zien door middel van Hallo `azure vm show <groupname> <vmname>` opdracht. Als u meer dan één VM in uw groep hebt, moet u mogelijk eerst toolist hello, virtuele machines in een groep met behulp van `azure vm list <groupname>`.

```azurecli
azure vm list zoo
info:    Executing command vm list
+ Getting virtual machines
data:    Name   ProvisioningState  Location  Size
data:    -----  -----------------  --------  -----------
data:    myVM0  Succeeded          westus    Standard_A1
data:    myVM1  Failed             westus    Standard_A1
```

Vervolgens zoekt u myVM1 op:

```azurecli
azure vm show zoo myVM1
info:    Executing command vm show
+ Looking up hello VM "myVM1"
+ Looking up hello NIC "nic1"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Failed
data:    Name                            :myVM1
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :MicrosoftWindowsServer
data:        Offer                       :WindowsServer
data:        Sku                         :2012-R2-Datacenter
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Windows
data:        Name                        :osdisk
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :http://zoostorageralph.blob.core.windows.net/vhds/osdisk.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Windows Configuration:
data:        Provision VM Agent          :true
data:        Enable automatic updates    :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Network/networkInterfaces/nic1
data:          Primary                   :false
data:          Provisioning State        :Succeeded
data:          Name                      :nic1
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.0.5
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/availabilitySets/MYAVSET
info:    vm show command OK
```

> [!NOTE]
> Als u tooprogrammatically store wilt en Hallo-uitvoer van de consoleopdrachten manipuleren, kunt u, zoals een JSON-parseren hulpprogramma toouse  **[jq](https://github.com/stedolan/jq)**  of  **[jsawk](https://github.com/micha/jsawk)** , of taal bibliotheken die geschikt voor het Hallo-taak zijn.
>
>

## <a id="log-on-to-a-linux-based-virtual-machine"></a>Taak: Meld u aan tooa op basis van Linux virtuele machine
Linux-machines zijn meestal verbonden toothrough SSH. Zie voor meer informatie [hoe toouse SSH met Linux op Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a id="stop-a-virtual-machine"></a>Taak: Een virtuele machine stoppen
Voer deze opdracht uit:

```azurecli
azure vm stop <group name> <virtual machine name>
```

> [!IMPORTANT]
> Gebruik deze parameter tookeep Hallo virtueel IP-adres (VIP) van Hallo vnet, mocht dat Hallo laatste VM in dit vnet. <br><br> Als u Hallo `StayProvisioned` parameter, zult u nog steeds worden gefactureerd voor Hallo VM.
>
>

## <a id="start-a-virtual-machine"></a>Taak: Een virtuele machine starten
Voer deze opdracht uit:

```azurecli
azure vm start <group name> <virtual machine name>
```

## <a id="attach-a-data-disk"></a>Taak: Een gegevensschijf koppelen
U moet ook toodecide of tooattach een nieuwe schijf of een die bevat gegevens. Voor een nieuwe schijf Hallo opdracht maakt u Hallo .vhd-bestand en koppelt u deze in Hallo dezelfde opdracht.

een nieuwe schijf tooattach deze opdracht uitvoeren:

```azurecli
    azure vm disk attach-new <resource-group> <vm-name> <size-in-gb>
```

een bestaande gegevensschijf tooattach deze opdracht uitvoeren:

```azurecli
azure vm disk attach <resource-group> <vm-name> [vhd-url]
```

Vervolgens moet u toomount Hallo schijf, zoals u dat gewend in Linux bent.

## <a name="next-steps"></a>Volgende stappen
Voor veel meer voorbeelden van Azure CLI gebruik Hello **arm** modus, Zie [Using hello Azure CLI voor Mac, Linux en Windows Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md). Zie toolearn meer informatie over Azure-resources en hun concepten [overzicht van Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md).

Zie voor meer sjablonen die u kunt gebruiken, [Azure Quickstart-sjablonen](https://azure.microsoft.com/documentation/templates/) en [Toepassingsframeworks met sjablonen](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
