---
title: Netwerken voor virtuele-machineschaalsets in Azure | Microsoft Docs
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
ms.openlocfilehash: a8520c6d8962cc362fc935f6b515a299c0ce75b3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a>Netwerken voor virtuele-machineschaalsets in Azure

Wanneer u een virtuele-machineschaalset van Azure instelt via de portal, zijn bepaalde netwerkeigenschappen standaard ingesteld, bijvoorbeeld een Azure Load Balancer met binnenkomende NAT-regels. In dit artikel wordt beschreven hoe u een aantal van de meer geavanceerde netwerkfuncties gebruikt die u kunt configureren met schaalsets.

U kunt alle functies die in dit artikel configureren met behulp van Azure Resource Manager-sjablonen. Er zijn ook Azure CLI- en PowerShell-voorbeelden toegevoegd voor bepaalde functies. Gebruik CLI 2.10 en PowerShell 4.2.0 of hoger.

## <a name="accelerated-networking"></a>Versneld netwerken
[Versnelde netwerken](../virtual-network/virtual-network-create-vm-accelerated-networking.md) in Azure verbetert de prestaties van het netwerk door het inschakelen van I/O-virtualisatie met één hoofdmap (SR-IOV) bij een virtuele machine. Als u versneld netwerken wilt gebruiken met schaalsets, stelt u enableAcceleratedNetworking in op **true** in de instelling networkInterfaceConfigurations van uw schaalset. Bijvoorbeeld:
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
Wanneer een schaalset is gemaakt met Azure Portal, wordt er voor de meeste configuratieopties een nieuwe load balancer gemaakt. Als u een schaalset maakt die moet verwijzen naar een bestaande load balancer, kunt u dit doen met de CLI. Het volgende voorbeeldscript maakt een load balancer en maakt vervolgens een schaalset die ernaar verwijst:
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a>Configureerbare DNS-instellingen
Standaard nemen schaalsets de specifieke DNS-instellingen van het VNET en het subnet waarin ze zijn gemaakt over. U kunt de DNS-instellingen voor een schaalset echter rechtstreeks configureren.
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a>Een schaal met configureerbare DNS-servers maken
Als u een schaalset met een aangepaste DNS-configuratie met CLI 2.0 wilt maken, voegt u het argument **--dns-servers** toe aan de opdracht **vmss create** gevolgd door met spaties gescheiden IP-adressen. Bijvoorbeeld:
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
Als u aangepaste DNS-servers wilt configureren in een Azure-sjabloon, voegt u de eigenschap dnsSettings toe aan het gedeelte networkInterfaceConfigurations van de schaalset. Bijvoorbeeld:
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a>Een schaalset maken met de configureerbare domeinnamen van virtuele machines
Als u een schaalset wilt maken met een aangepaste DNS-naam voor virtuele machines met CLI 2.0, voegt u het argument **--vm-domain-name** toe aan de opdracht **vmss create**, gevolgd door een tekenreeks met de domeinnaam.

Als u de domeinnaam wilt instellen in een Azure-sjabloon, voegt u de eigenschap **dnsSettings** toe aan het gedeelte **networkInterfaceConfigurations** van de schaalset. Bijvoorbeeld:

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

De uitvoer voor de DNS-naam van een afzonderlijke virtuele machine heeft de volgende notatie: 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a>Openbare IPv4 per virtuele machine
Virtuele machines in Azure-schaalsets hebben meestal geen eigen openbaar IP-adres nodig. Het is in de meeste gevallen voordeliger en veiliger om een openbaar IP-adres aan een load balancer of een afzonderlijke virtuele machine (ook wel een jumpbox) te koppelen. Deze stuurt vervolgens binnenkomende verbindingen indien nodig door naar virtuele machines van de schaalset (bijvoorbeeld via de binnenkomende NAT-regels).

In sommige gevallen hebben virtuele machines van een schaalset echter hun eigen openbare IP-adressen nodig. Dit is bijvoorbeeld het geval bij games, waarbij een console rechtstreeks verbinding moet maken met een virtuele cloudmachine, die de physics van de game verwerkt. Een ander voorbeeld is de situatie waarbij virtuele machines externe verbindingen met elkaar moeten maken via regio's in een gedistribueerde database.

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a>Een schaalset met een openbaar IP-adres per virtuele machine maken
Als u een schaalset wilt maken waarmee een openbaar IP-adres wordt toegewezen aan elke virtuele machine met CLI 2.0, voegt u de parameter **--public-ip-per-vm** toe aan de opdracht **vmss create**. 

Als u een schaalset maakt met een Azure-sjabloon, zorg er dan voor dat de API-versie van de resource Microsoft.Compute/virtualMachineScaleSets ten minste **2017-03-30** is en voeg de JSON-eigenschap **publicIpAddressConfiguration** toe aan het gedeelte ipConfigurations van de schaalset. Bijvoorbeeld:

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
Voorbeeldsjabloon: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)

### <a name="querying-the-public-ip-addresses-of-the-virtual-machines-in-a-scale-set"></a>Query’s uitvoeren op de openbare IP-adressen van de virtuele machines in een schaalset
U kunt de openbare IP-adressen die zijn toegewezen aan de virtuele machines van de schaalset met CLI 2.0 in een lijst weergeven met de opdracht **az vmss list-instance-public-ips**.

Gebruik de opdracht _Get-AzureRmPublicIpAddress_ om openbare IP-adressen voor schaalsets weer te geven met behulp van PowerShell. Bijvoorbeeld:
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

U kunt ook query’s uitvoeren op de openbare IP-adressen door rechtstreeks naar de resource-id van de openbare IP-adresconfiguratie te verwijzen. Bijvoorbeeld:
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

Query’s uitvoeren op de openbare IP-adressen die zijn toegewezen aan de virtuele machines in de schaalset met de [Azure Resource Explorer](https://resources.azure.com) of de REST API van Azure met versie **2017-03-30** of hoger.

Als u de openbare IP-adressen van een schaalset wilt bekijken met behulp van de Resource Explorer, bekijkt u het gedeelte **publicipaddresses** onder uw schaalset. Bijvoorbeeld: https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses

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
Aan elke NIC die aan een virtuele machine in een schaalset is gekoppeld, zijn een of meer IP-configuraties gekoppeld. Aan elke configuratie is één privé-IP-adres toegewezen. Aan elke configuratie kan ook één resource met een openbaar IP-adres zijn gekoppeld. Om te begrijpen hoeveel IP adressen kunnen worden toegewezen aan een NIC en hoeveel openbare IP-adressen u kunt gebruiken in een Azure-abonnement, bekijkt u de [Azure-limieten](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).

## <a name="multiple-nics-per-virtual-machine"></a>Meerdere NIC's per virtuele machine
U kunt maximaal 8 NIC's per virtuele machine hebben, afhankelijk van de grootte van de machine. Het maximale aantal NIC's per computer is beschikbaar in het artikel [VM-grootte](../virtual-machines/windows/sizes.md). Het volgende voorbeeld is een netwerkprofiel van een schaalset met meerdere NIC-vermeldingen en meerdere openbare IP-adressen per virtuele machine:
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
Netwerkbeveiligingsgroepen kunnen rechtstreeks op een schaalset worden toegepast door een verwijzing naar de sectie Configuratie van netwerkinterface van de eigenschappen van de virtuele machine van de schaalset toe te voegen.

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
Raadpleeg [deze documentatie](../virtual-network/virtual-networks-overview.md) voor meer informatie over virtuele netwerken in Azure.
