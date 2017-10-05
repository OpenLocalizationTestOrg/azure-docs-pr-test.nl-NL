---
title: Maken van de basisinfrastructuur in Azure met behulp van Terraform | Microsoft Docs
description: Informatie over het maken van Azure-resources met behulp van Terraform
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: 9660a95b440c2e4311829979e270d9f10099f624
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a>Maken van de basisinfrastructuur in Azure met behulp van Terraform
In dit artikel beschrijft de stappen die u nemen moet voor het inrichten van een virtuele machine, samen met de onderliggende infrastructuur in Azure. U leert hoe Terraform scripts schrijven en hoe de wijzigingen te visualiseren voordat u ze in uw cloudinfrastructuur. Ook leert u hoe infrastructuur in Azure maken met behulp van Terraform.

Maak een bestand met de naam van \terraform_azure101.tf in een teksteditor naar keuze (Visual Studio Code/Sublime/Vim/enz.) om te beginnen. De exacte naam van het bestand niet van belang omdat de naam van de map als parameter wordt geaccepteerd Terraform: alle scripts in de map worden uitgevoerd. Plak de volgende code in het nieuwe bestand:

~~~~
# Configure the Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have to include this block
provider "azurerm" {
  subscription_id = "your_subscription_id_from_script_execution"
  client_id       = "your_appId_from_script_execution"
  client_secret   = "your_password_from_script_execution"
  tenant_id       = "your_tenant_id_from_script_execution"
}

# create a resource group 
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}
~~~~
In de `provider` sectie van het script, geeft u aan Terraform gebruik van een Azure-provider tot inrichten bronnen in het script. Als u de waarden voor subscription_id, appId, wachtwoord en tenant_id, Zie de [installeren en configureren van Terraform](terraform-install-configure.md) handleiding. Als u omgevingsvariabelen voor de waarden in dit blok hebt gemaakt, moet u niet wilt opnemen. 

De `azurerm_resource_group` resource Hiermee geeft u Terraform om een nieuwe resourcegroep te maken. U kunt meer brontypen die beschikbaar in Terraform verderop in dit artikel zijn kunt zien.

## <a name="execute-the-script"></a>Het script uitvoeren
Nadat u het script opslaat, wordt de console/opdrachtregel sluiten en typ het volgende:
```
terraform init
```
initialiseren Terraform-provider voor Azure. Typ het volgende:
```
terraform plan terraformscripts
```
Er wordt ervan uitgegaan dat `terraformscripts` is de map waarin het script is opgeslagen. We gebruiken de `plan` Terraform-opdracht wordt gekeken naar de resources die zijn gedefinieerd in de scripts. Het vergelijkt ze met de informatie over de opgeslagen door Terraform en vervolgens voert u de geplande uitvoering _zonder_ resources daadwerkelijk maken in Azure. 

Nadat u de vorige opdracht uitvoert, ziet u ongeveer het volgende scherm:

![Terraform plannen](linux/media/terraform/tf_plan2.png)

Als alles er goed uitziet, richt u deze nieuwe resourcegroep in Azure door het uitvoeren van de volgende: 
```
terraform apply terraformscripts
```
In de Azure portal, ziet u de nieuwe lege resourcegroep aangeroepen `terraformtest`. In de volgende sectie u een een virtuele machine en de ondersteunende infrastructuur voor die virtuele machine toevoegen aan de resourcegroep.

## <a name="provision-an-ubuntu-vm-with-terraform"></a>Een virtuele Ubuntu-machine met Terraform inrichten
Laten we het Terraform script dat we hebt gemaakt met de gegevens die nodig zijn voor het inrichten van een virtuele machine met Ubuntu uitbreiden. De bronnen die u in de volgende secties inricht zijn:

* Een netwerk met één subnet
* Een netwerkinterfacekaart 
* Een opslagaccount met storage-container
* Een openbaar IP-adres
* Een virtuele machine die gebruikmaakt van de eerdere bronnen 

Zie voor uitgebreide documentatie voor elk van de resources Azure Terraform de [Terraform documentatie](https://www.terraform.io/docs/providers/azurerm/index.html).

De volledige versie van de [inrichting script](#complete-terraform-script) is ook voor uw gemak geleverd.

### <a name="extend-the-terraform-script"></a>Het script Terraform uitbreiden
Uitbreiden van het script dat is gemaakt met de volgende bronnen: 
~~~~
# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}
~~~~
Het vorige script maakt een virtueel netwerk en een subnet binnen dit virtuele netwerk. Noteer de verwijzing naar de resourcegroep die u al hebt gemaakt via "${azurerm_resource_group.helloterraform.name}' in het virtuele netwerk en de subnetdefinitie van.

~~~~
# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "TerraformDemo"
    }
}

# create network interface
resource "azurerm_network_interface" "helloterraformnic" {
    name = "tfni"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    ip_configuration {
        name = "testconfiguration1"
        subnet_id = "${azurerm_subnet.helloterraformsubnet.id}"
        private_ip_address_allocation = "static"
        private_ip_address = "10.0.2.5"
        public_ip_address_id = "${azurerm_public_ip.helloterraformips.id}"
    }
}
~~~~
De vorige script codefragmenten maken een openbaar IP-adres en een netwerkinterface die gebruik maakt van het openbare IP-adres gemaakt. Noteer de verwijzingen naar subnet_id en public_ip_address_id. Terraform beschikt over ingebouwde intelligentie om te begrijpen dat de netwerkinterface afhankelijk is van de resources die moeten worden gemaakt voordat het maken van de netwerkinterface.

~~~~
# create a random id
resource "random_id" "randomId" {
  byte_length = 4
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "tfstorage${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "westus"
    account_type = "Standard_LRS"

    tags {
        environment = "staging"
    }
}

# create storage container
resource "azurerm_storage_container" "helloterraformstoragestoragecontainer" {
    name = "vhd"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    storage_account_name = "${azurerm_storage_account.helloterraformstorage.name}"
    container_access_type = "private"
    depends_on = ["azurerm_storage_account.helloterraformstorage"]
}
~~~~
Hier kunt u een opslagaccount hebt gemaakt en een storage-container binnen dit opslagaccount wordt gedefinieerd. Dit opslagaccount is waar het opslaan van virtuele harde schijven (VHD's) voor de virtuele machine gemaakt.

~~~~
# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_A0"

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "14.04.2-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        vhd_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}${azurerm_storage_container.helloterraformstoragestoragecontainer.name}/myosdisk.vhd"
        caching = "ReadWrite"
        create_option = "FromImage"
    }

    os_profile {
        computer_name = "hostname"
        admin_username = "testadmin"
        admin_password = "Password1234!"
    }

    os_profile_linux_config {
        disable_password_authentication = false
    }

    tags {
        environment = "staging"
    }
}
~~~~
Ten slotte maakt het vorige codefragment u een virtuele machine die gebruikmaakt van alle resources die al ingericht. Een opslagaccount en container voor een VHD, een netwerkinterface met openbare IP- en subnet opgegeven, zijn en de resourcegroep waarin u al hebt gemaakt. Let op de eigenschap vm_size, waarbij het script een Azure A0 SKU geeft.

### <a name="execute-the-script"></a>Het script uitvoeren
Terugkeren naar de console/opdrachtregel met het volledige script opgeslagen, en typ het volgende:
```
terraform apply terraformscripts
```
Na enige tijd de bronnen, met inbegrip van een virtuele machine, worden weergegeven in de `terraformtest` resourcegroep in de Azure portal.

## <a name="complete-terraform-script"></a>Volledige Terraform script

Voor uw gemak ziet hieronder u het volledige Terraform-script dat voorziet in alle van de infrastructuur die wordt besproken in dit artikel.

```
variable "resourcesname" {
  default = "helloterraform"
}

# Configure the Microsoft Azure Provider
provider "azurerm" {
  subscription_id = "XXX"
  client_id       = "XXX"
  client_secret   = "XXX"
  tenant_id       = "XXX"
}

# create a resource group if it doesn't exist
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}

# create virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "tfvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "tfsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}


# create public IPs
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "TerraformDemo"
    }
}

# create network interface
resource "azurerm_network_interface" "helloterraformnic" {
    name = "tfni"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    ip_configuration {
        name = "testconfiguration1"
        subnet_id = "${azurerm_subnet.helloterraformsubnet.id}"
        private_ip_address_allocation = "static"
        private_ip_address = "10.0.2.5"
        public_ip_address_id = "${azurerm_public_ip.helloterraformips.id}"
    }
}

# create a random id
resource "random_id" "randomId" {
  byte_length = 4
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "tfstorage${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "westus"
    account_type = "Standard_LRS"

    tags {
        environment = "staging"
    }
}

# create storage container
resource "azurerm_storage_container" "helloterraformstoragestoragecontainer" {
    name = "vhd"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    storage_account_name = "${azurerm_storage_account.helloterraformstorage.name}"
    container_access_type = "private"
    depends_on = ["azurerm_storage_account.helloterraformstorage"]
}

# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_A0"

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "14.04.2-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        vhd_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}${azurerm_storage_container.helloterraformstoragestoragecontainer.name}/myosdisk.vhd"
        caching = "ReadWrite"
        create_option = "FromImage"
    }

    os_profile {
        computer_name = "hostname"
        admin_username = "testadmin"
        admin_password = "Password1234!"
    }

    os_profile_linux_config {
        disable_password_authentication = false
    }

    tags {
        environment = "staging"
    }
}
```

## <a name="next-steps"></a>Volgende stappen
U kunt de basisinfrastructuur in Azure hebt gemaakt met behulp van Terraform. Voor complexere scenario's, inclusief voorbeelden die gebruik load balancers en de virtuele machine worden geschaald sets, Zie talrijke [Terraform voorbeelden voor Azure](https://github.com/hashicorp/terraform/tree/master/examples). Zie voor een bijgewerkte lijst met ondersteunde providers voor Azure de [Terraform documentatie](https://www.terraform.io/docs/providers/azurerm/index.html).
