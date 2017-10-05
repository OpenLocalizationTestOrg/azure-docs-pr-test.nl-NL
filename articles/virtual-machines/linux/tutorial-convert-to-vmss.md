---
title: Een Azure VM converteren naar een schaalset | Microsoft Docs
description: Maken en implementeren van een Linux Azure virtuele-machineschaalset ingesteld met de Azure CLI.
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
ms.openlocfilehash: 8d3376d2791b1349298db618d475ce5573083702
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="convert-an-existing-azure-virtual-machine-to-a-scale-set"></a>Een bestaande Azure virtuele machine converteren naar een schaalset

Deze zelfstudie laat zien hoe u Azure CLI 2.0 gebruiken een virtuele machine converteren naar een virtuele-machineschaalset. U leert ook hoe u de configuratie van de virtuele machines in de schaalset automatiseren. Zie voor meer informatie over het installeren van Azure CLI 2.0 [aan de slag met Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md). Zie voor meer informatie over schaalsets [virtuele Machine Scale ingesteld](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).

## <a name="step-1---deprovision-the-vm"></a>Stap 1: inrichting ervan ongedaan maakt de virtuele machine

SSH gebruiken voor verbinding met de virtuele machine.

Inrichting ervan ongedaan maakt de virtuele machine met behulp van de Azure VM-agent verwijderen van bestanden en gegevens. Zie voor een gedetailleerd overzicht van het opheffen van inrichting [Linux-machine vastleggen](capture-image.md).

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-the-vm"></a>Stap 2: een installatiekopie van de virtuele machine

Zie voor een gedetailleerd overzicht van het vastleggen van [Linux-machine vastleggen](capture-image.md).

Toewijzing van de virtuele machine met [az vm ongedaan](/cli/azure/vm#deallocate):

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

De virtuele machine met generalize [az vm generalize](/cli/azure/vm#generalize):

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

Een installatiekopie maken van de VM-resource met [az installatiekopie maken](/cli/azure/image#create):

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-the-scale-set"></a>Stap 3: de schaalaanpassingsset maken

Ophalen van de **id** van de afbeelding.

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

Met deze opdracht wordt ook een 10gb-gegevensschijf gekoppeld. Houd er rekening mee dat, afhankelijk van de virtuele machine door u gekozen grootte (we gebruikt **Standard_DS1_v2**), het aantal gegevensschijven toegestaan verschilt. Raadpleeg voor meer informatie de [grootten van virtuele machines](sizes.md).

Zodra de schaal ingesteld is voltooid, er verbinding mee maken. Een lijst met IP-adressen voor de exemplaren ophalen voor SSH met [az vmss lijst--verbinding-Instantiegegevens](/cli/azure/vmss#list-instance-connection-info):

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

Nu u verbinding kunt maken met het exemplaar van de virtuele machine voor het initialiseren van de gegevensschijf

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-the-data-disk"></a>Stap 4: de gegevensschijf initialiseren

Verbinding gemaakt met de virtuele machine en de schijf met partitioneren `fdisk`:

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

Een bestandssysteem schrijven naar de partitie met de `mkfs` opdracht:

```bash
sudo mkfs -t ext4 /dev/sdc1
```

De nieuwe schijf koppelen zodat deze toegankelijk is in het besturingssysteem:

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

De schijf kan nu worden toegang via het koppelpunt datadrive, die kan worden gecontroleerd met `ls /datadrive/`.

De SSH-sessie te beëindigen.


## <a name="step-5---configure-firewall"></a>Stap 5: de firewall configureren

Een gat in de firewall op de webserver dat wordt gehost door de schaalaanpassingsset perforeren. Wanneer de schaalaanpassingsset is gemaakt, ook een load balancer gemaakt is en u deze gebruikt **SSH** aan de afzonderlijke virtuele machines. Als u wilt een poort opent, moet u twee soorten gegevens, die u kunt krijgen met Azure CLI.

* **Frontend-IP-adresgroep**  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* **Backend-IP-adresgroep**  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

Met deze twee namen, kunt u poort openen **80**.

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a>Stap 6: configuratie automatiseren

De gegevensschijf moet worden geconfigureerd op elk exemplaar van de virtuele machine. We kunnen de configuratie van de virtuele machine met automatiseren de **CustomScript** extensie.

Maak eerst een *.sh* script dat de opdrachten van schijf-indeling bevat.

```sh
#!/bin/bash

# Setup the data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

Vervolgens scriptbestand uploaden naar waar de **CustomScript** extensie toegang hebt tot het. Een kopie beschikbaar is [hier](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).

Maken van een lokaal bestand met de naam **settings.json** en het volgende JSON-blok in het plaatsen. De `flieUris` eigenschap moet worden ingesteld op waar het scriptbestand is geüpload naar.

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

Met deze opdracht implementeren voor uw scale ingesteld met de **CustomScript** extensie, die verwijzen naar de **settings.json** bestand die we zojuist hebben gemaakt.

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

Deze extensie wordt automatisch uitgevoerd op alle huidige exemplaren en alle exemplaren die later wordt gemaakt door te schalen.

## <a name="step-7---configure-autoscale-rules"></a>Stap 7: regels voor automatisch schalen configureren

Op dit moment kunnen kunnen niet regels voor automatisch schalen worden ingesteld in de Azure CLI. Gebruik de [Azure-portal](https://portal.azure.com) automatisch schalen configureren.

## <a name="step-8---management-tasks"></a>Stap 8 - beheertaken

Gedurende de levenscyclus van de schaal is ingesteld, moet u wellicht een of meer beheertaken uitvoeren. Bovendien kunt u scripts maken die verschillende lifecycle-taken automatiseren en de Azure CLI biedt een snelle manier om deze taken. Hier volgen enkele algemene taken.

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
Zie voor meer informatie over enkele van de virtuele machine scale set functies geïntroduceerd in deze zelfstudie, de volgende informatie:

- [Overzicht van Azure virtuele-Machineschaalsets](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [Overzicht van Azure Load Balancer](../../load-balancer/load-balancer-overview.md)
- [Beheren van netwerkverkeer met netwerkbeveiligingsgroepen](../../virtual-network/virtual-networks-nsg.md)