---
title: aaaConvert een virtuele machine van Azure tooa schaalset | Microsoft Docs
description: Maken en implementeren van een Linux Azure virtuele-machineschaalset hello Azure CLI in te stellen.
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 04/05/2017
ms.author: adegeo
ms.openlocfilehash: e228282ac4855cef589b8500e74e9d461f9aed84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="convert-an-existing-azure-virtual-machine-tooa-scale-set"></a>Een bestaande virtuele machine van Azure tooa scale set converteren

Deze zelfstudie laat zien hoe Azure CLI 2.0 toouse tooconvert een virtuele machine tooa virtuele-machineschaalset. U leert ook hoe tooautomate Hallo configuratie van Hallo virtuele machines in Hallo scale ingesteld. Voor meer informatie over hoe tooinstall Azure CLI 2.0, Zie [aan de slag met Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md). Zie voor meer informatie over schaalsets [virtuele Machine Scale ingesteld](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).

## <a name="step-1---deprovision-hello-vm"></a>Stap 1 - Deprovision Hallo VM

Gebruik SSH tooconnect toohello VM.

Identiteitsgegevens Hallo VM hello Azure VM-agent toodelete bestanden en gegevens. Zie voor een gedetailleerd overzicht van het opheffen van inrichting [Linux-machine vastleggen](capture-image.md).

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-hello-vm"></a>Stap 2: een installatiekopie van Hallo VM

Zie voor een gedetailleerd overzicht van het vastleggen van [Linux-machine vastleggen](capture-image.md).

Toewijzing ongedaan maken met virtuele machine Hallo [az vm ongedaan](/cli/azure/vm#deallocate):

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

Generalize Hallo VM met [az vm generalize](/cli/azure/vm#generalize):

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

Een installatiekopie maken van VM-resource met Hallo [az installatiekopie maken](/cli/azure/image#create):

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-hello-scale-set"></a>Stap 3: Hallo scale set maken

Hallo ophalen **id** van Hallo-afbeelding.

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

Een virtuele machine maken van uw Afbeeldingsbron met [az vmss maken](/cli/azure/vmss#create):

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

Met deze opdracht wordt ook een 10gb-gegevensschijf gekoppeld. Houd er rekening mee die, afhankelijk van Hallo VM gekozen grootte (we gebruikt **Standard_DS1_v2**), Hallo aantal gegevensschijven dat mag niet hetzelfde is. Raadpleeg voor meer informatie, Hallo [grootten van virtuele machines](sizes.md).

Zodra Hallo scale ingesteld is voltooid, sluit u tooit. Een lijst met IP-adressen voor Hallo exemplaren ophalen voor SSH met [az vmss lijst--verbinding-Instantiegegevens](/cli/azure/vmss#list-instance-connection-info):

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

Nu u toohello gegevensschijf voor virtuele machine exemplaar tooinitialize Hallo verbinding kunt maken

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-hello-data-disk"></a>Stap 4 - schijf initialiseren Hallo-gegevens

Tijdens het verbonden toohello virtuele machine, partitie-Hallo-schijf met `fdisk`:

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

Schrijven van een bestand toohello systeempartitie Hello `mkfs` opdracht:

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Hallo nieuwe schijf koppelen zodat deze toegankelijk is in Hallo-besturingssysteem:

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

Hallo-schijf kan nu worden opent via Hallo datadrive koppelpunt, kan worden gecontroleerd met `ls /datadrive/`.

Hallo SSH-sessie wordt beëindigd.


## <a name="step-5---configure-firewall"></a>Stap 5: de firewall configureren

Een gat in Hallo firewall toohello webserver gehost door Hallo schaalset perforeren. Wanneer het Hallo-schaalset is gemaakt, is ook een load balancer gemaakt en u gebruikt deze **SSH** toohello afzonderlijke virtuele machines. een poort tooopen, moet u twee soorten gegevens, die u kunt krijgen met Azure CLI.

* **Frontend-IP-adresgroep**  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* **Backend-IP-adresgroep**  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

Met deze twee namen, kunt u poort openen **80**.

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a>Stap 6: configuratie automatiseren

Hallo gegevensschijf moet toobe geconfigureerd op elk exemplaar van de virtuele machine. We Hallo configuratie van virtuele machine Hallo Hello kunt automatiseren **CustomScript** extensie.

Maak eerst een *.sh* script dat Hallo schijf-indeling opdrachten bevat.

```sh
#!/bin/bash

# Setup hello data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

Vervolgens uploaden dat script bestand toowhere hello **CustomScript** extensie toegang hebt tot het. Een kopie beschikbaar is [hier](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).

Maken van een lokaal bestand met de naam **settings.json** en put hello volgende blok in het JSON. Hallo `flieUris` eigenschap toowhere het scriptbestand is geüpload naar moet worden ingesteld.

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

Implementeren van deze opdracht tooyour schaal ingesteld met Hallo **CustomScript** extensie, die verwijzen naar Hallo **settings.json** bestand die we zojuist hebben gemaakt.

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

Deze extensie wordt automatisch uitgevoerd op alle huidige exemplaren en alle exemplaren die later wordt gemaakt door te schalen.

## <a name="step-7---configure-autoscale-rules"></a>Stap 7: regels voor automatisch schalen configureren

Op dit moment kunnen kunnen niet regels voor automatisch schalen worden ingesteld in de Azure CLI. Gebruik Hallo [Azure-portal](https://portal.azure.com) tooconfigure automatisch schalen.

## <a name="step-8---management-tasks"></a>Stap 8 - beheertaken

Gedurende de levenscyclus van de Hallo van Hallo scale is ingesteld, moet u mogelijk toorun een of meer beheertaken. Bovendien kunt u toocreate scripts die verschillende lifecycle-taken automatiseren en hello Azure CLI biedt een snelle manier toodo deze taken. Hier volgen enkele algemene taken.

### <a name="get-connection-info"></a>Verbindingsgegevens ophalen

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a>Set-exemplaren (handmatige schaal)

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a>Verwijderen van resourcegroep

Verwijderen van een resourcegroep, worden ook alle resources binnen verwijderd.

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Volgende stappen
meer informatie over een aantal virtuele-machineschaalset Hallo functies geïntroduceerd in deze zelfstudie ingesteld toolearn Zie Hallo volgende informatie:

- [Overzicht van Azure virtuele-Machineschaalsets](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [Overzicht van Azure Load Balancer](../../load-balancer/load-balancer-overview.md)
- [Beheren van netwerkverkeer met netwerkbeveiligingsgroepen](../../virtual-network/virtual-networks-nsg.md)