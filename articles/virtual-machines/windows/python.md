---
title: aaaCreate en beheren van een Windows-VM in Azure met behulp van Python | Microsoft Docs
description: Meer informatie over toouse Python toocreate en beheren van een Windows-VM in Azure.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: davidmu
ms.openlocfilehash: c5553e4e7361e6b9a7183cd935be382f967160cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-python"></a>Maken en beheren van Windows-machines in Azure met Python

Een [Azure virtuele Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) moet meerdere ondersteunende Azure-resources. In dit artikel bevat informatie over het maken, beheren en het verwijderen van de VM-netwerkbronnen met behulp van Python. Procedures voor:

> [!div class="checklist"]
> * Een Visual Studio-project maken
> * Pakketten installeren
> * Referenties maken
> * Resources maken
> * Beheertaken uitvoeren
> * Resources verwijderen
> * Hallo-toepassing uitvoeren

Het duurt ongeveer 20 minuten toodo deze stappen.

## <a name="create-a-visual-studio-project"></a>Een Visual Studio-project maken

1. Als u nog niet gedaan hebt, installeert u [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio). Selecteer **ontwikkeling van een Python** op Hallo van werkbelastingen pagina en klik vervolgens op **installeren**. In Hallo samenvatting, kunt u zien dat **Python 3 64-bits (3.6.0)** automatisch voor u is geselecteerd. Als u Visual Studio al hebt geïnstalleerd, kunt u Hallo Python werkbelasting met behulp van Visual Studio starten Hallo toevoegen.
2. Klik na het installeren en starten van de Visual Studio, op **bestand** > **nieuw** > **Project**.
3. Klik op **sjablonen** > **Python** > **Python toepassing**, voer *myPythonProject* voor Hallo-naam Selecteer Hallo-locatie van het Hallo-project van Hallo-project en klik vervolgens op **OK**.

## <a name="install-packages"></a>Pakketten installeren

1. Klik in Solution Explorer onder *myPythonProject*, met de rechtermuisknop op **Python-omgevingen**, en selecteer vervolgens **virtuele omgeving toevoegen**.
2. Op het welkomstscherm van virtuele omgeving toevoegen, accepteer de standaardnaam Hallo van *env*, zorg ervoor dat *Python 3.6 (64-bits)* voor Hallo basisinterpreter is geselecteerd en klik vervolgens op **maken**.
3. Klik met de rechtermuisknop Hallo *env* omgeving die u hebt gemaakt, klikt u op **Install Python Package**, voer *azure* in Hallo zoekvak en druk op Enter.

U ziet in Hallo uitvoer windows azure hello-pakketten zijn geïnstalleerd. 

## <a name="create-credentials"></a>Referenties maken

Voordat u deze stap, zorg ervoor dat u hebt een [Active Directory-service-principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md). U moet ook Hallo toepassings-ID en verificatiesleutel Hallo Hallo tenant-ID die u nodig hebt in een later stadium vastleggen.

1. Open *myPythonProject.py* -bestand dat is gemaakt, en voeg deze code tooenable uw toepassing toorun:

    ```python
    if __name__ == "__main__":
    ```

2. tooimport hello code die is vereist, voeg deze instructies toohello bovenaan Hallo .py bestand:

    ```python
    from azure.common.credentials import ServicePrincipalCredentials
    from azure.mgmt.resource import ResourceManagementClient
    from azure.mgmt.compute import ComputeManagementClient
    from azure.mgmt.network import NetworkManagementClient
    from azure.mgmt.compute.models import DiskCreateOption
    ```

3. Naast in bestand .py hello, variabelen toevoegen nadat Hallo importinstructies toospecify algemene waarden gebruikt in Hallo code:
   
    ```
    SUBSCRIPTION_ID = 'subscription-id'
    GROUP_NAME = 'myResourceGroup'
    LOCATION = 'westus'
    VM_NAME = 'myVM'
    ```

    Vervang **abonnement-id** met uw abonnements-id.

4. Deze functie toevoegen Active Directory-referenties voor toocreate Hallo is dat u toomake aanvragen, moet na Hallo variabelen in Hallo .py bestand:

    ```python
    def get_credentials():
        credentials = ServicePrincipalCredentials(
            client_id = 'application-id',
            secret = 'authentication-key',
            tenant = 'tenant-id'
        )

        return credentials
    ```

    Vervang **toepassing-id**, **verificatiesleutel**, en **tenant-id** met Hallo-waarden die u eerder hebt verzameld tijdens het maken van uw Azure Active Directory service-principal.

5. toocall hello functie die u eerder hebt toegevoegd, voeg deze code onder Hallo **als** instructie op Hallo bestandseindemarkering Hallo .py:

    ```python
    credentials = get_credentials()
    ```

## <a name="create-resources"></a>Resources maken
 
### <a name="initialize-management-clients"></a>Van beheerclients te initialiseren

Management-clients nodig toocreate en beheren van resources met behulp van Python SDK Hallo in Azure. toocreate hello management clients, voeg deze code onder Hallo **als** instructie vervolgens na Hallo .py bestand:

```python
resource_group_client = ResourceManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
network_client = NetworkManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
compute_client = ComputeManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
```

### <a name="create-hello-vm-and-supporting-resources"></a>Hallo VM maken en de ondersteunende resources

Alle resources moeten zijn opgenomen in een [resourcegroep](../../azure-resource-manager/resource-group-overview.md).

1. Deze functie toocreate een resourcegroep toevoegen na Hallo variabelen in Hallo .py bestand:

    ```python
    def create_resource_group(resource_group_client):
        resource_group_params = { 'location':LOCATION }
        resource_group_result = resource_group_client.resource_groups.create_or_update(
            GROUP_NAME, 
            resource_group_params
        )
    ```

2. toocall hello functie die u eerder hebt toegevoegd, voeg deze code onder Hallo **als** instructie op Hallo bestandseindemarkering Hallo .py:

    ```python
    create_resource_group(resource_group_client)
    input('Resource group created. Press enter toocontinue...')
    ```

[Beschikbaarheidssets](tutorial-availability-sets.md) eenvoudiger voor u toomaintain Hallo virtuele machines die worden gebruikt door uw toepassing.

1. toocreate een beschikbaarheid ingesteld, wordt deze functie na Hallo variabelen in Hallo .py bestand toevoegen:
   
    ```python
    def create_availability_set(compute_client):
        avset_params = {
            'location': LOCATION,
            'sku': { 'name': 'Aligned' },
            'platform_fault_domain_count': 3
        }
        availability_set_result = compute_client.availability_sets.create_or_update(
            GROUP_NAME,
            'myAVSet',
            avset_params
        )
    ```

2. toocall hello functie die u eerder hebt toegevoegd, voeg deze code onder Hallo **als** instructie op Hallo bestandseindemarkering Hallo .py:

    ```python
    create_availability_set(compute_client)
    print("------------------------------------------------------")
    input('Availability set created. Press enter toocontinue...')
    ```

Een [openbaar IP-adres](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) benodigde toocommunicate met Hallo virtuele machine is.

1. Deze functie toocreate Hallo virtuele machine, een openbare IP-adres toevoegen na Hallo variabelen in Hallo .py bestand:

    ```python
    def create_public_ip_address(network_client):
        public_ip_addess_params = {
            'location': LOCATION,
            'public_ip_allocation_method': 'Dynamic'
        }
        creation_result = network_client.public_ip_addresses.create_or_update(
            GROUP_NAME,
            'myIPAddress',
            public_ip_addess_params
        )

        return creation_result.result()
    ```

2. toocall hello functie die u eerder hebt toegevoegd, voeg deze code onder Hallo **als** instructie op Hallo bestandseindemarkering Hallo .py:

    ```python
    creation_result = create_public_ip_address(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

Een virtuele machine moet worden in een subnet van een [virtueel netwerk](../../virtual-network/virtual-networks-overview.md).

1. Deze functie toocreate een virtueel netwerk toevoegen na Hallo variabelen in Hallo .py bestand:

    ```python
    def create_vnet(network_client):
        vnet_params = {
            'location': LOCATION,
            'address_space': {
                'address_prefixes': ['10.0.0.0/16']
            }
        }
        creation_result = network_client.virtual_networks.create_or_update(
            GROUP_NAME,
            'myVNet',
            vnet_params
        )
        return creation_result.result()
    ```

2. toocall hello functie die u eerder hebt toegevoegd, voeg deze code onder Hallo **als** instructie op Hallo bestandseindemarkering Hallo .py:
   
    ```python
    creation_result = create_vnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

3. Deze functie een subnet toohello virtueel netwerk, tooadd toevoegen na Hallo variabelen in Hallo .py bestand:
    
    ```python
    def create_subnet(network_client):
        subnet_params = {
            'address_prefix': '10.0.0.0/24'
        }
        creation_result = network_client.subnets.create_or_update(
            GROUP_NAME,
            'myVNet',
            'mySubnet',
            subnet_params
        )

        return creation_result.result()
    ```
        
4. toocall hello functie die u eerder hebt toegevoegd, voeg deze code onder Hallo **als** instructie op Hallo bestandseindemarkering Hallo .py:
   
    ```python
    creation_result = create_subnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

Een virtuele machine moet een network interface-toocommunicate op Hallo virtueel netwerk.

1. Deze functie toocreate een netwerkinterface toevoegen na Hallo variabelen in Hallo .py bestand:

    ```python
    def create_nic(network_client):
        subnet_info = network_client.subnets.get(
            GROUP_NAME, 
            'myVNet', 
            'mySubnet'
        )
        publicIPAddress = network_client.public_ip_addresses.get(
            GROUP_NAME,
            'myIPAddress'
        )
        nic_params = {
            'location': LOCATION,
            'ip_configurations': [{
                'name': 'myIPConfig',
                'public_ip_address': publicIPAddress,
                'subnet': {
                    'id': subnet_info.id
                }
            }]
        }
        creation_result = network_client.network_interfaces.create_or_update(
            GROUP_NAME,
            'myNic',
            nic_params
        )

        return creation_result.result()
    ```

2. toocall hello functie die u eerder hebt toegevoegd, voeg deze code onder Hallo **als** instructie op Hallo bestandseindemarkering Hallo .py:

    ```python
    creation_result = create_nic(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

Nu dat u alle Hallo ondersteunende resources hebt gemaakt, kunt u een virtuele machine.

1. toocreate Hallo van virtuele machine, het toevoegen van deze functie na Hallo variabelen in Hallo .py bestand:
   
    ```python
    def create_vm(network_client, compute_client):  
        nic = network_client.network_interfaces.get(
            GROUP_NAME, 
            'myNic'
        )
        avset = compute_client.availability_sets.get(
            GROUP_NAME,
            'myAVSet'
        )
        vm_parameters = {
            'location': LOCATION,
            'os_profile': {
                'computer_name': VM_NAME,
                'admin_username': 'azureuser',
                'admin_password': 'Azure12345678'
            },
            'hardware_profile': {
                'vm_size': 'Standard_DS1'
            },
            'storage_profile': {
                'image_reference': {
                    'publisher': 'MicrosoftWindowsServer',
                    'offer': 'WindowsServer',
                    'sku': '2012-R2-Datacenter',
                    'version': 'latest'
                }
            },
            'network_profile': {
                'network_interfaces': [{
                    'id': nic.id
                }]
            },
            'availability_set': {
                'id': avset.id
            }
        }
        creation_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME, 
            VM_NAME, 
            vm_parameters
        )
    
        return creation_result.result()
    ```

    > [!NOTE]
    > Deze zelfstudie maakt een virtuele machine met een versie van Windows Server-besturingssysteem Hallo. Zie toolearn meer informatie over het selecteren van de andere afbeeldingen [navigeren door en selecteren van installatiekopieën van virtuele machine van Azure met Windows PowerShell en Azure CLI Hallo](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
    > 
    > 

2. toocall hello functie die u eerder hebt toegevoegd, voeg deze code onder Hallo **als** instructie op Hallo bestandseindemarkering Hallo .py:

    ```python
    creation_result = create_vm(network_client, compute_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

## <a name="perform-management-tasks"></a>Beheertaken uitvoeren

Tijdens het Hallo-levensduur van een virtuele machine kunt u beheertaken toorun zoals starten, stoppen of een virtuele machine wordt verwijderd. U kunt bovendien toocreate code tooautomate herhalende of complexe taken.

### <a name="get-information-about-hello-vm"></a>Informatie ophalen over Hallo VM

1. Deze functie tooget informatie over de virtuele machine Hallo toevoegen na Hallo variabelen in Hallo .py bestand:

    ```python
    def get_vm(compute_client):
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME, expand='instanceView')
        print("hardwareProfile")
        print("   vmSize: ", vm.hardware_profile.vm_size)
        print("\nstorageProfile")
        print("  imageReference")
        print("    publisher: ", vm.storage_profile.image_reference.publisher)
        print("    offer: ", vm.storage_profile.image_reference.offer)
        print("    sku: ", vm.storage_profile.image_reference.sku)
        print("    version: ", vm.storage_profile.image_reference.version)
        print("  osDisk")
        print("    osType: ", vm.storage_profile.os_disk.os_type.value)
        print("    name: ", vm.storage_profile.os_disk.name)
        print("    createOption: ", vm.storage_profile.os_disk.create_option.value)
        print("    caching: ", vm.storage_profile.os_disk.caching.value)
        print("\nosProfile")
        print("  computerName: ", vm.os_profile.computer_name)
        print("  adminUsername: ", vm.os_profile.admin_username)
        print("  provisionVMAgent: {0}".format(vm.os_profile.windows_configuration.provision_vm_agent))
        print("  enableAutomaticUpdates: {0}".format(vm.os_profile.windows_configuration.enable_automatic_updates))
        print("\nnetworkProfile")
        for nic in vm.network_profile.network_interfaces:
            print("  networkInterface id: ", nic.id)
        print("\nvmAgent")
        print("  vmAgentVersion", vm.instance_view.vm_agent.vm_agent_version)
        print("    statuses")
        for stat in vm_result.instance_view.vm_agent.statuses:
            print("    code: ", stat.code)
            print("    displayStatus: ", stat.display_status)
            print("    message: ", stat.message)
            print("    time: ", stat.time)
        print("\ndisks");
        for disk in vm.instance_view.disks:
            print("  name: ", disk.name)
            print("  statuses")
            for stat in disk.statuses:
                print("    code: ", stat.code)
                print("    displayStatus: ", stat.display_status)
                print("    time: ", stat.time)
        print("\nVM general status")
        print("  provisioningStatus: ", vm.provisioning_state)
        print("  id: ", vm.id)
        print("  name: ", vm.name)
        print("  type: ", vm.type)
        print("  location: ", vm.location)
        print("\nVM instance status")
        for stat in vm.instance_view.statuses:
            print("  code: ", stat.code)
            print("  displayStatus: ", stat.display_status)
    ```
2. toocall hello functie die u eerder hebt toegevoegd, voeg deze code onder Hallo **als** instructie op Hallo bestandseindemarkering Hallo .py:

    ```python
    get_vm(compute_client)
    print("------------------------------------------------------")
    input('Press enter toocontinue...')
    ```

### <a name="stop-hello-vm"></a>Hallo VM stoppen

Stoppen van een virtuele machine en alle bijbehorende instellingen behouden, maar blijven toobe in rekening gebracht voor of u kunt een virtuele machine stoppen en deze ongedaan gemaakt. Wanneer een virtuele machine in de toewijzing is opgeheven, zijn alle resources die zijn gekoppeld ook toewijzing ongedaan is gemaakt en facturering eindigt voor.

1. Deze functie toostop Hallo virtuele machine zonder toewijzing, toevoegen na Hallo variabelen in Hallo .py bestand:

    ```python
    def stop_vm(compute_client):
        compute_client.virtual_machines.power_off(GROUP_NAME, VM_NAME)
    ```

    Als u toodeallocate Hallo virtuele machine wilt, Hallo power_off aanroep toothis code wijzigen:

    ```python
    compute_client.virtual_machines.deallocate(GROUP_NAME, VM_NAME)
    ```

2. toocall hello functie die u eerder hebt toegevoegd, voeg deze code onder Hallo **als** instructie op Hallo bestandseindemarkering Hallo .py:

    ```python
    stop_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="start-hello-vm"></a>Hallo VM starten

1. toostart Hallo van virtuele machine, het toevoegen van deze functie na Hallo variabelen in Hallo .py bestand:

    ```python
    def start_vm(compute_client):
        compute_client.virtual_machines.start(GROUP_NAME, VM_NAME)
    ```

2. toocall hello functie die u eerder hebt toegevoegd, voeg deze code onder Hallo **als** instructie op Hallo bestandseindemarkering Hallo .py:

    ```python
    start_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="resize-hello-vm"></a>Hallo VM vergroten of verkleinen

Veel aspecten van de implementatie moeten worden beschouwd bij het kiezen van een grootte voor de virtuele machine. Zie voor meer informatie [VM-grootten](sizes.md).

1. Deze functie toochange Hallo grootte van virtuele machine Hallo toevoegen na Hallo variabelen in Hallo .py bestand:

    ```python
    def update_vm(compute_client):
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME)
        vm.hardware_profile.vm_size = 'Standard_DS3'
        update_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME, 
            VM_NAME, 
            vm
        )

    return update_result.result()
    ```

2. toocall hello functie die u eerder hebt toegevoegd, voeg deze code onder Hallo **als** instructie op Hallo bestandseindemarkering Hallo .py:

    ```python
    update_result = update_vm(compute_client)
    print("------------------------------------------------------")
    print(update_result)
    input('Press enter toocontinue...')
    ```

### <a name="add-a-data-disk-toohello-vm"></a>Toevoegen van een data schijf toohello VM

Virtuele machines hebben een of meer [gegevensschijven](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) die als virtuele harde schijven zijn opgeslagen.

1. Deze functie tooadd een gegevens schijf toohello virtuele machine toevoegen na Hallo variabelen in Hallo .py bestand: 

    ```python
    def add_datadisk(compute_client):
        disk_creation = compute_client.disks.create_or_update(
            GROUP_NAME,
            'myDataDisk1',
            {
                'location': LOCATION,
                'disk_size_gb': 1,
                'creation_data': {
                    'create_option': DiskCreateOption.empty
                }
            }
        )
        data_disk = disk_creation.result()
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME)
        add_result = vm.storage_profile.data_disks.append({
            'lun': 1,
            'name': 'myDataDisk1',
            'create_option': DiskCreateOption.attach,
            'managed_disk': {
                'id': data_disk.id
            }
        })
        add_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME,
            VM_NAME,
            vm)

        return add_result.result()
    ```

2. toocall hello functie die u eerder hebt toegevoegd, voeg deze code onder Hallo **als** instructie op Hallo bestandseindemarkering Hallo .py:

    ```python
    add_result = add_datadisk(compute_client)
    print("------------------------------------------------------")
    print(add_result)
    input('Press enter toocontinue...')
    ```

## <a name="delete-resources"></a>Resources verwijderen

Omdat u in rekening voor resources die worden gebruikt in Azure gebracht, maar het is altijd een goede gewoonte toodelete-resources die niet langer nodig zijn. Als u toodelete Hallo virtuele machines wilt en alle Hallo bronnen ondersteunen, alle toodo hebt is Hallo-resourcegroep verwijderen.

1. toodelete hello resourcegroep en alle resources, moet u deze functie toevoegen na Hallo variabelen in Hallo .py bestand:
   
    ```python
    def delete_resources(resource_group_client):
        resource_group_client.resource_groups.delete(GROUP_NAME)
    ```

2. toocall hello functie die u eerder hebt toegevoegd, voeg deze code onder Hallo **als** instructie op Hallo bestandseindemarkering Hallo .py:
   
    ```python
    delete_resources(resource_group_client)
    ```

3. Sla *myPythonProject.py*.

## <a name="run-hello-application"></a>Hallo-toepassing uitvoeren

1. toorun Hallo-consoletoepassing, klikt u op **Start** in Visual Studio.

2. Druk op **Enter** nadat het Hallo-status van elke bron wordt geretourneerd. In de statusinformatie hello, ziet u een **geslaagd** Inrichtingsstatus. Als Hallo virtuele machine is gemaakt, hebt u Hallo kans toodelete alle Hallo-resources die u maakt. Voordat u op **Enter** toostart verwijderen resources, u kan een paar minuten tooverify hun maken in nemen hello Azure-portal. Als u hebt Azure portal openen hello, hebt u mogelijk toorefresh Hallo blade toosee nieuwe resources.  

    Het moet over vijf minuten duren voordat deze toorun console toepassing volledig van toofinish start. Duurt enkele minuten na het Hallo-toepassing heeft voltooid voordat u alle Hallo resources en Hallo resourcegroep worden verwijderd.


## <a name="next-steps"></a>Volgende stappen

- Als er problemen met de Hallo-implementatie zijn, een volgende stap toolook op zou zijn [probleemoplossing resourcegroepimplementaties in Azure-portal](../../resource-manager-troubleshoot-deployments-portal.md)
- Meer informatie over Hallo [Azure Python-bibliotheek](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)

