---
title: aaaAutoscale Linux virtuele-Machineschaalsets | Microsoft Docs
description: Automatisch schalen instellen voor een Linux VM-Schaalset met Azure CLI
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 83e93d9c-cac0-41d3-8316-6016f5ed0ce4
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 4352b94ec2973c37bc5616e3be25bd0c9442632b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-linux-machines-in-a-virtual-machine-scale-set"></a>Linux-machines automatisch schalen in een virtuele-machineschaalset
Virtuele-machineschaalsets eenvoudiger voor u toodeploy en identieke virtuele machines beheren als een set. Schaalsets bieden een uiterst schaalbare en aanpasbare berekeningslaag voor toepassingen die grootschalig en installatiekopieën voor Windows-platform, installatiekopieën van virtuele Linux-platform, aangepaste installatiekopieën en -extensies ondersteunen. toolearn meer, Zie [overzicht van virtuele machines Scale Sets](virtual-machine-scale-sets-overview.md).

Deze zelfstudie leert u hoe toocreate een schaal van Linux virtuele machines met behulp van de meest recente versie Hallo van Ubuntu Linux instelt. Hallo zelfstudie ook ziet u hoe tooautomatically scale Hallo-machines in Hallo instelt. U maakt Hallo schaal en instellen schalen door een Azure Resource Manager-sjabloon maken en implementeren met behulp van Azure CLI. Zie [Azure Resource Manager-sjablonen samenstellen](../azure-resource-manager/resource-group-authoring-templates.md) voor meer informatie over sjablonen. toolearn meer informatie over automatisch schalen van schaalsets, Zie [automatisch schalen en Virtual Machine-schaal stelt](virtual-machine-scale-sets-autoscale-overview.md).

In deze zelfstudie maakt u de volgende Hallo implementeren bronnen en -extensies:

* Microsoft.Storage/storageAccounts
* Microsoft.Network/virtualNetworks
* Microsoft.Network/publicIPAddresses
* Microsoft.Network/loadBalancers
* Microsoft.Network/networkInterfaces
* Microsoft.Compute/virtualMachines
* Microsoft.Compute/virtualMachineScaleSets
* Microsoft.Insights.VMDiagnosticsSettings
* Microsoft.Insights/autoscaleSettings

Zie voor meer informatie over het Resource Manager-resources [Azure Resource Manager versus klassieke implementatie](../azure-resource-manager/resource-manager-deployment-model.md).

Voordat u aan de slag met Hallo stappen in deze zelfstudie [hello Azure CLI installeren](../cli-install-nodejs.md).

## <a name="step-1-create-a-resource-group-and-a-storage-account"></a>Stap 1: Een resourcegroep en een opslagaccount maken

1. **Meld u aan tooMicrosoft Azure**  
In de opdrachtregelinterface (Bash, Terminal-opdrachtprompt), overschakelen tooResource Manager-modus, en vervolgens [Meld u aan met uw werk of school-id](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Volg de aanwijzingen Hallo voor een interactieve aanmelding ervaring tooyour Azure-account.

    ```cli   
    azure config mode arm

    azure login
    ```
   
    > [!NOTE]
    > Als u hebt een werk- of schoolaccount ID en u niet tweeledige verificatie zijn ingeschakeld, gebruikt u `azure login -u` met Hallo ID toolog in zonder een interactieve sessie. Als u niet een werk- of schoolaccount ID hebt, kunt u [maakt u een werk- of schoolaccount-id van uw persoonlijke Microsoft-account](../active-directory/active-directory-users-create-azure-portal.md).
    
2. **Een resourcegroep maken**  
Alle resources moet geïmplementeerde tooa resourcegroep. Voor deze zelfstudie Hallo resourcegroep een naam **vmsstest1**.
   
    ```cli
    azure group create vmsstestrg1 centralus
    ```

3. **Implementeren van een opslagaccount in de nieuwe resourcegroep Hallo**  
Dit opslagaccount is waar Hallo sjabloon wordt opgeslagen. Maken van een opslagaccount met de naam **vmsstestsa**.
   
    ```cli
    azure storage account create -g vmsstestrg1 -l centralus --kind Storage --sku-name LRS vmsstestsa
    ```

## <a name="step-2-create-hello-template"></a>Stap 2: Hallo-sjabloon maken
Een Azure Resource Manager-sjabloon maakt het mogelijk dat u toodeploy en gezamenlijk Azure-resources beheren met behulp van een JSON-beschrijving van Hallo resources en de bijbehorende implementatie-parameters.

1. In uw favoriete editor Hallo bestand VMSSTemplate.json maken en toevoegen van Hallo initiële JSON-structuur toosupport Hallo-sjabloon.

    ```json
    {
      "$schema":"http://schema.management.azure.com/schemas/2014-04-01-preview/VM.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      },
      "variables": {
      },
      "resources": [
      ]
    }
    ```

2. Parameters zijn niet altijd vereist, maar ze bieden een manier tooinput waarden wanneer Hallo sjabloon wordt geïmplementeerd. Toevoegen van deze parameters onder Hallo parameters bovenliggende element dat u de sjabloon toohello toegevoegd.

    ```json
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
   * Een naam voor het afzonderlijke virtuele machine hello, die gebruikte tooaccess Hallo-machines in de schaalset Hallo.
   * Een naam voor het opslagaccount Hallo waar Hallo sjabloon wordt opgeslagen.
   * het aantal exemplaren van virtuele machines tooinitially Hallo maken in de schaalset Hallo.
   * Een naam en het wachtwoord van Hallo administrator-account op Hallo virtuele machines.
   * Een voorvoegsel voor Hallo-resources die zijn gemaakt toosupport Hallo scale ingesteld.

3. Variabelen kunnen worden gebruikt in een sjabloon toospecify-waarden die kunnen worden regelmatig gewijzigd of waarden die toobe moet gemaakt uit een combinatie van parameterwaarden. Voeg deze variabelen onder Hallo variabelen bovenliggende element dat u de sjabloon toohello toegevoegd.

    ```json
    "dnsName1": "[concat(parameters('resourcePrefix'),'dn1')]",
    "dnsName2": "[concat(parameters('resourcePrefix'),'dn2')]",
    "publicIP1": "[concat(parameters('resourcePrefix'),'ip1')]",
    "publicIP2": "[concat(parameters('resourcePrefix'),'ip2')]",
    "loadBalancerName": "[concat(parameters('resourcePrefix'),'lb1')]",
    "virtualNetworkName": "[concat(parameters('resourcePrefix'),'vn1')]",
    "nicName": "[concat(parameters('resourcePrefix'),'nc1')]",
    "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
    "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
    "storageAccountSuffix": [ "a", "g", "m", "s", "y" ],
    "diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'a')]",
    "accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/','Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
    "wadlogs": "<WadCfg><DiagnosticMonitorConfiguration>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor\\PercentProcessorTime\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU percentage guest OS\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```

   * DNS-namen die worden gebruikt door Hallo netwerkinterfaces.
   * namen van Hallo IP-adres en de voorvoegsels voor het virtuele netwerk Hallo en subnetten.
   * Hallo namen en id van het virtuele netwerk hello, en voor de load balancer, netwerkinterfaces.
   * Namen van opslagaccounts voor Hallo-accounts die zijn gekoppeld aan het Hallo-machines in de schaalset Hallo.
   * Instellingen voor het Hallo-extensie voor diagnostische gegevens die op Hallo virtuele machines is geïnstalleerd. Zie voor meer informatie over het Hallo-extensie voor diagnostische gegevens [maken van een virtuele Windows-machine met de controle en diagnostische gegevens met Azure Resource Manager-sjabloon](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

4. Hallo storage account resource onder Hallo resources bovenliggende element dat u hebt toegevoegd toohello sjabloon toevoegen. Deze sjabloon worden gebruikt in een lus toocreate Hallo aanbevolen vijf opslagaccounts waar Hallo besturingssysteem schijven en diagnostische gegevens worden opgeslagen. Deze set accounts kan van too100 virtuele machines in een schaalset, die staat voor de huidige maximaal Hallo ondersteunen. De naam van elk opslagaccount is met een letter eenheidsaanduiding die is gedefinieerd in gecombineerd met Hallo-achtervoegsel dat u in het Hallo-parameters voor de sjabloon Hallo opgeeft Hallo-variabelen.
   
        {
          "type": "Microsoft.Storage/storageAccounts",
          "name": "[concat(parameters('resourcePrefix'), variables('storageAccountSuffix')[copyIndex()])]",
          "apiVersion": "2015-06-15",
          "copy": {
            "name": "storageLoop",
            "count": 5
          },
          "location": "[resourceGroup().location]",
          "properties": { "accountType": "Standard_LRS" }
        },

5. Hallo virtueel netwerk resource toevoegen. Zie voor meer informatie [Netwerkresourceprovider](../virtual-network/resource-groups-networking.md).

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
        "subnets": [
          {
            "name": "subnet1",
            "properties": { "addressPrefix": "10.0.0.0/24" }
          }
        ]
      }
    },
    ```

6. Voeg Hallo openbare IP-adres resources die worden gebruikt door Hallo load balancer en netwerkinterface.

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP1')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName1')]"
        }
      }
    },
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP2')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName2')]"
        }
      }
    },
    ```

7. Hallo load balancerresource die wordt gebruikt door Hallo scale set toevoegen. Zie voor meer informatie [Azure Resource Manager-ondersteuning voor de Load Balancer](../load-balancer/load-balancer-arm.md).

    ```json   
    {
      "apiVersion": "2015-06-15",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
              }
            }
          }
        ],
        "backendAddressPools": [ { "name": "bepool1" } ],
        "inboundNatPools": [
          {
            "name": "natpool1",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPortRangeStart": 50000,
              "frontendPortRangeEnd": 50500,
              "backendPort": 22
            }
          }
        ]
      }
    },
    ```

8. Hallo network interface-resource die wordt gebruikt door Hallo afzonderlijke virtuele machine toevoegen. Omdat computers in een scale-set niet toegankelijk zijn via een openbaar IP-adres, een aparte virtuele machine wordt gemaakt in Hallo hetzelfde virtuele netwerk tooremotely toegang Hallo-machines.

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP2'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIP2'))]"
              },
              "subnet": {
                "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
              }
            }
          }
        ]
      }
    },
    ```

9. Hallo afzonderlijke virtuele machine in Hallo netwerk als Hallo scale set toevoegen.

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[parameters('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": { "vmSize": "Standard_A1" },
        "osProfile": {
          "computername": "[parameters('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "Canonical",
            "offer": "UbuntuServer",
            "sku": "14.04.4-LTS",
            "version": "latest"
          },
          "osDisk": {
            "name": "[concat(parameters('resourcePrefix'), 'os1')]",
            "vhd": {
              "uri":  "[concat('https://',parameters('resourcePrefix'),'a.blob.core.windows.net/vhds/',parameters('resourcePrefix'),'os1.vhd')]"
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
    },
    ```

10. Hallo virtuele-machineschaalset resource toevoegen en geef Hallo-extensie voor diagnostische gegevens die op alle virtuele machines in de schaalset Hallo is geïnstalleerd. Veel van Hallo-instellingen voor deze resource zijn vergelijkbaar met de bron van de virtuele machine Hallo. de belangrijkste verschillen Hallo zijn Hallo capaciteit element waarmee Hallo aantal virtuele machines in de schaalset hello en upgradePolicy waarmee wordt aangegeven hoe updates toovirtual machines worden gemaakt. Hallo scale set wordt niet gemaakt totdat alle Hallo-opslagaccounts worden gemaakt die is opgegeven met Hallo dependsOn element.

    ```json
    {
      "type": "Microsoft.Compute/virtualMachineScaleSets",
      "apiVersion": "2016-03-30",
      "name": "[parameters('vmSSName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "sku": {
        "name": "Standard_A1",
        "tier": "Standard",
        "capacity": "[parameters('instanceCount')]"
      },
      "properties": {
        "upgradePolicy": {
          "mode": "Manual"
        },
        "virtualMachineProfile": {
          "storageProfile": {
            "osDisk": {
              "vhdContainers": [
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4],'.blob.core.windows.net/vmss')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "Canonical",
              "offer": "UbuntuServer",
              "sku": "14.04.4-LTS",
              "version": "latest"
            }
          },
          "osProfile": {
            "computerNamePrefix": "[parameters('vmSSName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
          },
          "networkProfile": {
            "networkInterfaceConfigurations": [
              {
                "name": "networkconfig1",
                "properties": {
                  "primary": "true",
                  "ipConfigurations": [
                    {
                      "name": "ip1",
                      "properties": {
                        "subnet": {
                          "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
                        },
                        "loadBalancerBackendAddressPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/backendAddressPools/bepool1')]"
                          }
                        ],
                        "loadBalancerInboundNatPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/inboundNatPools/natpool1')]"
                          }
                        ]
                      }
                    }
                  ]
                }
              }
            ]
          },
          "extensionProfile": {
            "extensions": [
              {
                "name":"LinuxDiagnostic",
                "properties": {
                  "publisher":"Microsoft.OSTCExtensions",
                  "type":"LinuxDiagnostic",
                  "typeHandlerVersion":"2.1",
                  "autoUpgradeMinorVersion":false,
                  "settings": {
                    "xmlCfg":"[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount":"[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName":"[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey":"[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint":"https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. Hallo autoscaleSettings resource die definieert hoe Hallo scale set wordt aangepast op basis van het processorgebruik op Hallo virtuele machines in Hallo set toevoegen.

    ```json
    {
      "type": "Microsoft.Insights/autoscaleSettings",
      "apiVersion": "2015-04-01",
      "name": "[concat(parameters('resourcePrefix'),'as1')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      ],
      "properties": {
        "enabled": true,
        "name": "[concat(parameters('resourcePrefix'),'as1')]",
        "profiles": [
          {
            "name": "Profile1",
            "capacity": {
              "minimum": "1",
              "maximum": "10",
              "default": "1"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "\\Processor\\PercentProcessorTime",
                  "metricNamespace": "",
                  "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 50.0
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          }
        ],
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      }
    }
    ```
    
    Deze waarden zijn belangrijk voor deze zelfstudie:
    
    * **metricName**  
    Deze waarde is hetzelfde als het Hallo-prestatiemeteritem dat is gedefinieerd in Hallo wadperfcounter variabele Hallo. Met behulp van die variabele Hallo extensie voor diagnostische gegevens verzamelt Hallo **Processor\PercentProcessorTime** teller.
    
    * **metricResourceUri**  
    Deze waarde is Hallo resource-id van de virtuele-machineschaalset Hallo weergeven.
    
    * **timeGrain**  
    Deze waarde is Hallo granulatie van Hallo metrische gegevens die worden verzameld. In deze sjabloon is ingesteld tooone minuut.
    
    * **statistiek**  
    Deze waarde bepaalt hoe Hallo metrische gegevens worden gecombineerd tooaccommodate Hallo automatisch vergroten / verkleinen in te grijpen. Hallo mogelijke waarden zijn: gemiddelde, Min, Max. In deze sjabloon Hallo gemiddelde totale CPU-gebruik van Hallo virtuele machines worden verzameld.

    * **waarde voor timeWindow**  
    Deze waarde is Hallo tijdbereik waarin de gegevens worden verzameld. Deze moet tussen 5 minuten en 12 uur.
    
    * **TimeAggregation van**  
    de waarde bepaalt hoe Hallo-gegevens die worden verzameld gedurende een bepaalde periode moeten worden gecombineerd. Hallo-standaardwaarde is de gemiddelde. Hallo mogelijke waarden zijn: gemiddeld, Minimum, Maximum, laatste, totaal, Count.
    
    * **operator**  
    Deze waarde is Hallo-operator die wordt gebruikt toocompare Hallo metrische gegevens en Hallo drempelwaarde. Hallo mogelijke waarden zijn: gelijk is aan NotEquals, groter dan, GreaterThanOrEqual, LessThan, LessThanOrEqual.
    
    * **drempelwaarde**  
    Deze waarde activeert Hallo schaalactie. In deze sjabloon wordt toegevoegd machines toohello schaal instellen als de gemiddelde CPU-gebruik Hallo tussen computers in het Hallo-set is meer dan 50%.
    
    * **richting**  
    Deze waarde bepaalt Hallo-actie die wordt uitgevoerd wanneer het Hallo-drempelwaarde wordt bereikt. Hallo mogelijke waarden zijn vergroten of verkleinen. In deze sjabloon wordt hello aantal virtuele machines in de schaalset hello verhoogd als Hallo drempelwaarde meer dan 50% in tijdvenster Hallo gedefinieerd.

    * **type**  
    Deze waarde is Hallo type actie dat moet worden uitgevoerd en tooChangeCount moet worden ingesteld.
    
    * **waarde**  
    Deze waarde is het aantal virtuele machines die zijn toegevoegd of verwijderd uit schaalset Hallo Hallo. Deze waarde moet 1 of hoger. Hallo-standaardwaarde is 1. In deze sjabloon Hallo aantal machines in Hallo schaal instellen toeneemt 1 wanneer Hallo drempelwaarde wordt voldaan.

    * **cooldown**  
    Deze waarde is Hallo hoeveelheid tijd toowait sinds de laatste vergroten/verkleinen actie Hallo voordat de volgende actie Hallo optreedt. Deze waarde moet tussen 1 minuut en één week.

12. Hallo-sjabloonbestand opslaan.    

## <a name="step-3-upload-hello-template-toostorage"></a>Stap 3: Hallo sjabloon toostorage uploaden
Hallo-sjabloon kan worden geüpload, zolang u weet Hallo naam en de primaire sleutel van Hallo storage-account dat u in stap 1 hebt gemaakt.

1. In de opdrachtregelinterface (Bash, Terminal-opdrachtprompt), voer deze opdrachten tooset Hallo omgevingsvariabelen nodig tooaccess Hallo storage-account:

    ```cli   
    export AZURE_STORAGE_ACCOUNT={account_name}
    export AZURE_STORAGE_ACCESS_KEY={key}
    ```
    
    U kunt Hallo sleutel verkrijgen door te klikken op het sleutelpictogram Hallo wanneer u bekijkt hello storage account resource in hello Azure-portal. Wanneer u een Windows-opdrachtprompt, typ **ingesteld** in plaats van de export.

2. Hallo-container voor het opslaan van Hallo-sjabloon maken.
   
    ```cli
    azure storage container create -p Blob templates
    ```

3. Hallo sjabloon bestand toohello nieuwe container uploaden.
   
    ```cli
    azure storage blob upload VMSSTemplate.json templates VMSSTemplate.json
    ```

## <a name="step-4-deploy-hello-template"></a>Stap 4: Hallo sjabloon implementeren
Nu dat u Hallo sjabloon hebt gemaakt, kunt u beginnen met het Hallo-resources te implementeren. Gebruik deze opdracht toostart Hallo proces:

```cli
azure group deployment create --template-uri https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json vmsstestrg1 vmsstestdp1
```

Wanneer u op invoeren, vraag tooprovide waarden voor Hallo variabelen die u hebt toegewezen. Deze waarden bevatten:

```cli
vmName: vmsstestvm1
vmSSName: vmsstest1
instanceCount: 5
adminUserName: vmadmin1
adminPassword: VMpass1
resourcePrefix: vmsstest
```

Het duurt ongeveer 15 minuten voor alle Hallo resources toosuccessfully worden geïmplementeerd.

> [!NOTE]
> U kunt ook Hallo-portal mogelijkheid toodeploy Hallo resources gebruiken. Gebruik deze koppeling: https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>


## <a name="step-5-monitor-resources"></a>Stap 5: Monitor resources
U kunt sommige informatie ophalen over virtuele-machineschaalsets met behulp van deze methoden:

* Azure-portal Hallo - kunt u een beperkte hoeveelheid informatie met Hallo portal momenteel krijgen.

* Hallo [Azure Resource Explorer](https://resources.azure.com/) -dit hulpprogramma is Hallo aanbevolen voor de huidige status van uw scale set Hallo verkennen. Volg dit pad en ziet u Hallo instantieweergave van de schaal Hallo instellen die u hebt gemaakt:
  
    ```cli
    subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines
    ```

* Azure CLI - Gebruik deze opdracht tooget sommige informatie:

    ```cli  
    azure resource show -n vmsstest1 -r Microsoft.Compute/virtualMachineScaleSets -o 2015-06-15 -g vmsstestrg1
    ```

* Net zoals u zou een andere machine en klikt u op afstand toegang Hallo virtuele machines in Hallo scale set toomonitor afzonderlijke processen tot, verbinding maken met toohello jumpbox virtuele machine.

> [!NOTE]
> Een complete REST-API voor het verkrijgen van informatie over schaalsets vindt u in [virtuele Machine Scale ingesteld](https://msdn.microsoft.com/library/mt589023.aspx).

## <a name="step-6-remove-hello-resources"></a>Stap 6: Hallo resources verwijderen
Omdat u in rekening voor resources die worden gebruikt in Azure gebracht, maar het is altijd een goede gewoonte toodelete-resources die niet langer nodig zijn. U hoeft niet toodelete elke resource afzonderlijk van een resourcegroep. U kunt Hallo resourcegroep verwijderen en de bijhorende resources automatisch worden verwijderd.

```cli
azure group delete vmsstestrg1
```

## <a name="next-steps"></a>Volgende stappen
* Voorbeelden van Azure Monitor bewakingsfuncties in [Azure Monitor platformoverschrijdende CLI snel starten voorbeelden](../monitoring-and-diagnostics/insights-cli-samples.md)
* Meer informatie over functies in [gebruiken voor automatisch schalen acties toosend e-mail en -webhook waarschuwingsmeldingen in de Azure-Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)
* Meer informatie over hoe te[gebruik auditlogboeken toosend e-mail en -webhook waarschuwingsmeldingen in de Azure-Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)
* Bekijk Hallo [demo-app automatisch schalen op Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) sjabloon instellen van een Python/bottle app tooexercise Hallo automatisch vergroten / verkleinen functionaliteit van de virtuele Machine Scale ingesteld.

