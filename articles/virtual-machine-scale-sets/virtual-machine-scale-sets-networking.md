---
title: aaaNetworking voor virtuele Azure-machine-schaalsets | Microsoft Docs
description: Eigenschappen van configuratienetwerken virtuele-machineschaalsets van Azure.
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: guybo
ms.openlocfilehash: ef3f0cfe648d2195c051a73987e654f0e15d13bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a>Netwerken voor virtuele-machineschaalsets in Azure

Wanneer u de schaal van een virtuele machine van Azure instelt via de portal Hallo implementeert, zijn bepaalde netwerkeigenschappen standaardinstellingen, bijvoorbeeld een Azure Load Balancer met binnenkomende NAT-regels. Dit artikel wordt beschreven hoe toouse aantal Hallo geavanceerdere netwerkfuncties die u met de schaal configureren kunt wordt ingesteld.

U kunt alle Hallo-functies die in dit artikel met behulp van Azure Resource Manager-sjablonen kunt configureren. Er zijn ook Azure CLI- en PowerShell-voorbeelden toegevoegd voor bepaalde functies. Gebruik CLI 2.10 en PowerShell 4.2.0 of hoger.

## <a name="accelerated-networking"></a>Versneld netwerken
Azure [versnelde netwerken](../virtual-network/virtual-network-create-vm-accelerated-networking.md) verbetert de prestaties van het netwerk met één hoofdmap i/o-virtualisatie (SR-IOV) tooa virtuele machine inschakelen. toouse versnelde netwerken met schaalsets, stelt u enableAcceleratedNetworking te**true** in de schaalset networkInterfaceConfigurations instellingen. Bijvoorbeeld:
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
      "name": "niconfig1",
      "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
          ...
        ]
      }
    }
   ]
}
```

## <a name="create-a-scale-set-that-references-an-existing-azure-load-balancer"></a>Een schaalset maken die verwijst naar een bestaande Azure Load Balancer
Wanneer een schaalset is gemaakt met behulp van hello Azure-portal, wordt een nieuwe load balancer gemaakt voor de meeste configuratieopties. Als u een schaalset die tooreference moet een bestaande load balancer maakt, kunt u dit doen met CLI. Hallo volgende voorbeeldscript wordt gemaakt van een load balancer en maakt vervolgens een schaalset die verwijst naar het:
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a>Configureerbare DNS-instellingen
Standaard nemen-schaalsets op Hallo specifieke DNS-instellingen van Hallo VNET en het subnet die ze zijn gemaakt. U kunt wel Hallo DNS-instellingen configureren voor een schaal rechtstreeks worden ingesteld.
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a>Een schaal met configureerbare DNS-servers maken
een schaal ingesteld met een aangepaste DNS-configuratie met CLI 2.0, toocreate toevoegen Hallo **--dns-servers** argument toohello **vmss maken** opdracht, gevolgd door een spatie gescheiden IP-adressen. Bijvoorbeeld:
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
tooconfigure aangepaste DNS-servers in een Azure-sjabloon toevoegen aan een dnsSettings eigenschap toohello schaalset networkInterfaceConfigurations-sectie. Bijvoorbeeld:
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a>Een schaalset maken met de configureerbare domeinnamen van virtuele machines
een schaalset met een aangepaste DNS-naam voor virtuele machines met CLI 2.0, toocreate toevoegen Hallo **--vm domeinnaam** argument toohello **vmss maken** opdracht, gevolgd door een tekenreeks voor Hallo domeinnaam.

tooset Hallo-domeinnaam in een Azure-sjabloon toevoegen een **dnsSettings** eigenschap toohello schaalset **networkInterfaceConfigurations** sectie. Bijvoorbeeld:

```json
"networkProfile": {
  "networkInterfaceConfigurations": [
    {
    "name": "nic1",
    "properties": {
      "primary": "true",
      "ipConfigurations": [
      {
        "name": "ip1",
        "properties": {
          "subnet": {
            "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
          },
          "publicIPAddressconfiguration": {
            "name": "publicip",
            "properties": {
            "idleTimeoutInMinutes": 10,
              "dnsSettings": {
                "domainNameLabel": "[parameters('vmssDnsName')]"
              }
            }
          }
        }
      }
    ]
    }
}
```

Hallo-uitvoer voor de DNS-naam van een afzonderlijke virtuele machine in de volgende formulier Hallo zou worden: 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a>Openbare IPv4 per virtuele machine
Virtuele machines in Azure-schaalsets hebben meestal geen eigen openbaar IP-adres nodig. Voor de meeste scenario is beter voordelige en veilige tooassociate een openbare IP-adres tooa load balancer of tooan afzonderlijke virtuele machine (ook wel een jumpbox) die vervolgens binnenkomende verbindingen tooscale set virtuele machines stuurt die u nodig (bijvoorbeeld: binnenkomende NAT-regels).

Echter een aantal scenario's hoeven virtuele machines toohave-schaalset hun eigen openbare IP-adressen. Een voorbeeld games, waarin een console moet toomake een rechtstreekse verbinding tooa cloud virtuele machine, die game fysische verwerking doet. Een ander voorbeeld is waarbij virtuele machines toomake externe verbindingen tooone moet een andere tussen regio's in een gedistribueerde database.

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a>Een schaalset met een openbaar IP-adres per virtuele machine maken
een schaalset waarmee een openbare IP-adres tooeach virtuele machine met CLI 2.0, toegewezen toocreate toevoegen Hallo **--openbare ip per vm** parameter toohello **vmss maken** opdracht. 

toocreate een schaal ingesteld met een Azure-sjabloon, zorg ervoor dat Hallo API-versie van Hallo Microsoft.Compute/virtualMachineScaleSets resource is ten minste **2017-03-30**, en voeg een **publicIpAddressConfiguration**JSON eigenschap toohello schaalset ipConfigurations-sectie. Bijvoorbeeld:

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
Voorbeeldsjabloon: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)

### <a name="querying-hello-public-ip-addresses-of-hello-virtual-machines-in-a-scale-set"></a>Hallo openbare IP-adres opvragen adressen van Hallo virtuele machines in een schaal instellen
toolist hello openbare IP-adressen toegewezen tooscale set virtuele machines met CLI 2.0, gebruikt u Hallo **az vmss lijst-exemplaar-openbare-IP-adressen** opdracht.

toolist schaalset openbare IP-adressen met behulp van PowerShell, gebruikt u Hallo _Get-AzureRmPublicIpAddress_ opdracht. Bijvoorbeeld:
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

U kunt ook query Hallo openbare IP-adressen door te verwijzen rechtstreeks naar de bron-id Hallo van Hallo openbare IP-adresconfiguratie. Bijvoorbeeld:
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

tooquery hello openbare IP-adressen toegewezen tooscale set virtuele machines met behulp van Hallo [Azure Resource Explorer](https://resources.azure.com), of REST API van Azure met versie Hallo **2017-03-30** of hoger.

tooview openbare IP-adressen voor een scale-Hallo Resource Explorer, met een set bekijkt hello **publicipaddresses** sectie onder uw schaalset. Bijvoorbeeld: https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses

```
GET https://management.azure.com/subscriptions/{your sub ID}/resourceGroups/{RG name}/providers/Microsoft.Compute/virtualMachineScaleSets/{scale set name}/publicipaddresses?api-version=2017-03-30
```

Voorbeelduitvoer:
```json
{
  "value": [
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/pipvmss/virtualMachines/0/networkInterfaces/pipvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"a64060d5-4dea-4379-a11d-b23cd49a3c8d\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "ee8cb20f-af8e-4cd6-892f-441ae2bf701f",
        "ipAddress": "13.84.190.11",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/0/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    },
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"5f6ff30c-a24c-4818-883c-61ebd5f9eee8\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "036ce266-403f-41bd-8578-d446d7397c2f",
        "ipAddress": "13.84.159.176",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    }
```

## <a name="multiple-ip-addresses-per-nic"></a>Meerdere IP-adressen per NIC
Elke NIC gekoppeld tooa die virtuele machine in een scale-set kan een of meer IP-configuraties die zijn gekoppeld aan deze hebben. Aan elke configuratie is één privé-IP-adres toegewezen. Aan elke configuratie kan ook één resource met een openbaar IP-adres zijn gekoppeld. hoeveel IP-adressen kunnen toounderstand tooa NIC, worden toegewezen en hoeveel openbare IP-adressen kunt u in een Azure-abonnement te verwijzen[Azure limieten](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).

## <a name="multiple-nics-per-virtual-machine"></a>Meerdere NIC's per virtuele machine
U kunt hebben up too8 NIC's per virtuele machine, afhankelijk van de grootte van de machine. Hallo maximum aantal NIC's per machine is beschikbaar in Hallo [VM-grootte artikel](../virtual-machines/windows/sizes.md). Hallo volgende voorbeeld is dat een schaalset netwerkprofiel met meerdere NIC-vermeldingen en meerdere openbare IP-adressen per virtuele machine:
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
        "name": "nic1",
        "properties": {
            "primary": "true",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        },
        {
        "name": "nic2",
        "properties": {
            "primary": "false",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        }
    ]
}
```

## <a name="nsg-per-scale-set"></a>NSG per schaalset
Netwerkbeveiligingsgroepen kunnen direct tooa scale set, ingesteld door een verwijzing toohello network interface-configuratiesectie van Hallo schaal toe te voegen eigenschappen van virtuele machine worden aangebracht.

Bijvoorbeeld: 
```
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

## <a name="next-steps"></a>Volgende stappen
Voor meer informatie over virtuele netwerken van Azure te verwijzen[deze documentatie](../virtual-network/virtual-networks-overview.md).
