---
title: Beschikbaarheidssets zelfstudie voor virtuele Linux-machines in Azure | Microsoft Docs
description: Meer informatie over de Beschikbaarheidssets voor virtuele Linux-machines in Azure.
documentationcenter: 
services: virtual-machines-linux
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 63fe3f165864f06228604cac56d06cc061ab25f5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-availability-sets"></a>Het gebruik van beschikbaarheidssets


In deze zelfstudie leert u hoe u verhoogt de beschikbaarheid en betrouwbaarheid van uw virtuele Machine-oplossingen in Azure met een mogelijkheid Beschikbaarheidssets aangeroepen. Beschikbaarheidssets Zorg ervoor dat de virtuele machines die u implementeert in Azure worden gedistribueerd over meerdere geïsoleerde hardware-clusters. Dit zorgt ervoor dat als een storing hardware of software in Azure gebeurt, van invloed op een onderliggende reeks uw virtuele machines en die uw algehele oplossing blijft beschikbaar en operationele vanuit het perspectief van uw gebruik van klanten.

In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Een beschikbaarheidsset maken
> * Een virtuele machine in een beschikbaarheidsset maken
> * Controleer de beschikbare grootten voor virtuele machine


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u wilt installeren en gebruiken van de CLI lokaal, in deze zelfstudie vereist dat u de Azure CLI versie 2.0.4 zijn uitgevoerd of hoger. Voer `az --version` uit om de versie te bekijken. Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli). 

## <a name="availability-set-overview"></a>Overzicht van de beschikbaarheidsset

Een Beschikbaarheidsset is een logische groepering-functie die u in Azure gebruiken kunt om ervoor te zorgen dat de VM-resources die u in het plaatsen van elkaar geïsoleerd zijn wanneer ze zijn geïmplementeerd in een Azure-datacenter. Azure zorgt ervoor dat de virtuele machines die u binnen een Beschikbaarheidsset uitvoeren op meerdere fysieke servers plaatst, compute rekken eenheden voor opslag en netwerkswitches. Dit zorgt ervoor dat in het geval van een hardware- of Azure software fout slechts een subset van uw virtuele machines worden beïnvloed en uw algehele toepassing blijft en blijven beschikbaar voor uw klanten. Met behulp van Beschikbaarheidssets is een essentiële functie gebruiken als u wilt om betrouwbare cloudoplossingen te bouwen.

Laten we eens een typische VM-oplossing op basis van waar u mogelijk 4 front-end-webservers en 2 back-end virtuele machines die een database te hosten. Met Azure twee beschikbaarheidssets definiëren voordat u uw virtuele machines implementeert u zou willen: één beschikbaarheidsset voor de laag 'web' en een beschikbaarheidsset voor de laag 'database'. Bij het maken van een nieuwe virtuele machine vervolgens u kunt de beschikbaarheidsset als een parameter voor de vm az opdracht maken en Azure automatisch zorgt u dat de virtuele machines die u in de set beschikbaar maakt zijn geïsoleerd over meerdere fysieke hardware-resources. Dit betekent dat als de fysieke hardware die een van uw webserver of VM's Database-Server wordt uitgevoerd op een probleem is, u kent dat de andere exemplaren van uw webserver en de Database virtuele machines actief probleemloos blijven wordt omdat ze op andere hardware.

U moet altijd Beschikbaarheidssets gebruiken wanneer u wilt implementeren, betrouwbare oplossingen op basis van virtuele machine in Azure.


## <a name="create-an-availability-set"></a>Een beschikbaarheidsset maken

Kunt u een beschikbaarheidsset met [az vm beschikbaarheidsset maken](/cli/azure/vm/availability-set#create). In dit voorbeeld wordt zowel het aantal update en fouttolerantie domeinen op ingesteld *2* voor de beschikbaarheid van de set met de naam *myAvailabilitySet* in de *myResourceGroupAvailability* resourcegroep.

Maak een resourcegroep.

```azurecli-interactive 
az group create --name myResourceGroupAvailability --location eastus
```


```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupAvailability \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

Beschikbaarheidssets kunnen u resources in 'foutdomeinen' en 'domeinen bijwerken' isoleren. Een **foutdomein** vertegenwoordigt een geïsoleerd verzameling server + netwerk en opslag resources. In het voorgaande voorbeeld geven we willen we onze beschikbaarheidsset verdeeld over ten minste twee domeinen met fouten als onze virtuele machines worden geïmplementeerd. We ook aangeven dat we onze beschikbaarheidsset gedistribueerde in twee **domeinen bijwerken**.  Twee update domeinen Zorg ervoor dat wanneer Azure voert de software-updates onze VM-netwerkbronnen geïsoleerd, waardoor alle software die worden uitgevoerd onder de virtuele machine tegelijk worden bijgewerkt.

## <a name="configure-virtual-network"></a>Virtueel netwerk configureren
Voordat u een aantal virtuele machines implementeren en uw balancer kunt testen, moet u de resources van de ondersteunende virtueel netwerk maken. Zie voor meer informatie over virtuele netwerken van de [Azure Virtual Networks beheren](tutorial-virtual-network.md) zelfstudie.

### <a name="create-network-resources"></a>Maken van netwerkbronnen
Maak een virtueel netwerk met [az network vnet maken](/cli/azure/network/vnet#create). Het volgende voorbeeld wordt een virtueel netwerk met de naam *myVnet* met een subnet met de naam *mySubnet*:

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
Virtuele NIC's zijn gemaakt met [az netwerk nic maken](/cli/azure/network/nic#create). Het volgende voorbeeld maakt drie virtuele NIC's. (Een virtuele NIC voor elke VM die u maakt voor uw app in de volgende stappen uit). U kunt extra virtuele NIC's en virtuele machines maken op elk gewenst moment en toe te voegen aan de load balancer:

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupAvailability \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-vms-inside-an-availability-set"></a>Virtuele machines in een beschikbaarheidsset maken

Virtuele machines moeten worden gemaakt binnen de beschikbaarheidsset om ervoor te zorgen dat ze correct zijn verdeeld over de hardware. U kunt een bestaande virtuele machine toevoegen aan een beschikbaarheidsset nadat deze is gemaakt. 

Wanneer u een virtuele machine met maakt [az vm maken](/cli/azure/vm#create) opgeven van de beschikbaarheidsset met behulp van de `--availability-set` parameter om de naam van de beschikbaarheidsset.

```azurecli-interactive 
for i in `seq 1 2`; do
   az vm create \
     --resource-group myResourceGroupAvailability \
     --name myVM$i \
     --availability-set myAvailabilitySet \
     --nics myNic$i \
     --size Standard_DS1_v2  \
     --image Canonical:UbuntuServer:14.04.4-LTS:latest \
     --admin-username azureuser \
     --generate-ssh-keys \
     --no-wait
done 
```

Nu hebben we twee virtuele machines in onze nieuwe beschikbaarheidsset. Omdat ze zich in dezelfde beschikbaarheidsset, kan Azure zorgt ervoor dat de virtuele machines en alle bijbehorende resources (inclusief gegevensschijven) worden gedistribueerd over geïsoleerde fysieke hardware. Deze verdeling kan ervoor zorgen veel hogere beschikbaarheid van de algehele oplossing voor de VM.

Wat die u tegenkomen kunt wanneer u virtuele machines toevoegt is een bepaalde VM-grootte is niet meer beschikbaar voor gebruik binnen uw beschikbaarheidsset. Dit probleem kan zich voordoen als er niet langer voldoende capaciteit toe te voegen is behoud de isolatie van regels voor de beschikbaarheidsset worden afgedwongen. U kunt controleren om te zien welke VM-grootten zijn beschikbaar voor gebruik binnen de bestaande beschikbaarheidsset ingesteld met de `--availability-set list-sizes` parameter.

## <a name="check-for-available-vm-sizes"></a>Controleren op beschikbare VM-grootten 

U kunt meer virtuele machines toevoegen aan de beschikbaarheid later instellen, maar u moet weten welke VM-grootten zijn beschikbaar op de hardware. Gebruik [az vm beschikbaarheidsset lijst met grootten](/cli/azure/availability-set#list-sizes) voor een lijst met alle van de beschikbare grootten van de hardware-cluster gebruikt voor de beschikbaarheidsset.

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie heeft u het volgende geleerd:

> [!div class="checklist"]
> * Een beschikbaarheidsset maken
> * Een virtuele machine in een beschikbaarheidsset maken
> * Controleer de beschikbare grootten voor virtuele machine

Ga naar de volgende zelfstudie voor meer informatie over virtuele-machineschaalsets.

> [!div class="nextstepaction"]
> [Een VM-schaalset maken](tutorial-create-vmss.md)

