---
title: aaaAvailability zelfstudie stelt voor virtuele Linux-machines in Azure | Microsoft Docs
description: Meer informatie over Hallo Beschikbaarheidssets voor virtuele Linux-machines in Azure.
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
ms.openlocfilehash: 2a91e4a6057180035ec51410d9fffccaca343758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a>Hoe toouse beschikbaarheidssets


In deze zelfstudie leert u hoe tooincrease Hallo beschikbaarheid en betrouwbaarheid van uw virtuele Machine-oplossingen in Azure met een mogelijkheid Beschikbaarheidssets aangeroepen. Beschikbaarheidssets Zorg ervoor dat u implementeert op Azure VM's zijn verdeeld over meerdere geïsoleerde hardware clusters Hallo. Dit zorgt ervoor dat als een storing hardware of software in Azure gebeurt, van invloed op een onderliggende reeks uw virtuele machines die uw algehele oplossing blijft beschikbaar en operationele vanuit het oogpunt van uw klanten die gebruikmaken van het Hallo van.

In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Een beschikbaarheidsset maken
> * Een virtuele machine in een beschikbaarheidsset maken
> * Controleer de beschikbare grootten voor virtuele machine


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="availability-set-overview"></a>Overzicht van de beschikbaarheidsset

Een Beschikbaarheidsset, is een logische groepering-functie die u kunt gebruiken in Azure tooensure dat Hallo VM resources die u in het plaatsen van elkaar geïsoleerd zijn wanneer ze zijn geïmplementeerd in een Azure-datacenter. Azure zorgt ervoor dat Hallo virtuele machines die u binnen een Beschikbaarheidsset uitvoeren op meerdere fysieke servers plaatst, compute rekken eenheden voor opslag en netwerkswitches. Dit zorgt ervoor dat in geval van een softwarestoring van de Azure-of hardware Hallo slechts een subset van uw virtuele machines worden beïnvloed en uw algehele toepassing blijft en doorgaan toobe beschikbaar tooyour klanten. Gebruik Beschikbaarheidssets is een tooleverage essentiële mogelijkheden als u wilt dat toobuild betrouwbare cloudoplossingen.

Laten we eens een typische VM-oplossing op basis van waar u mogelijk 4 front-end-webservers en 2 back-end virtuele machines die een database te hosten. Met Azure, kunt u twee beschikbaarheidssets toodefine voordat u uw virtuele machines implementeren: één beschikbaarheid instellen voor Hallo 'web' laag en een beschikbaarheidsset voor Hallo 'database' laag. Bij het maken van een nieuwe virtuele machine vervolgens u Hallo beschikbaarheid instellen opgeven kunt als een parameter toohello az vm-opdracht maken en Azure zorgt u dat Hallo virtuele machines die u binnen Hallo beschikbaar maken automatisch worden ingesteld op de resources van meerdere fysieke hardware geïsoleerd. Dit betekent dat als Hallo fysieke hardware die een van uw webserver of VM's Database-Server wordt uitgevoerd op een probleem, u dat Hallo weet andere exemplaren van uw webserver en de Database virtuele machines blijven actief probleemloos omdat ze op andere hardware.

Als u wilt dat toodeploy betrouwbare VM gebaseerde oplossingen in Azure, moet u altijd Beschikbaarheidssets gebruiken.


## <a name="create-an-availability-set"></a>Een beschikbaarheidsset maken

Kunt u een beschikbaarheidsset met [az vm beschikbaarheidsset maken](/cli/azure/vm/availability-set#create). In dit voorbeeld we beide Hallo aantal update en fouttolerantie domeinen op instellen *2* voor Hallo beschikbaarheidsset benoemde *myAvailabilitySet* in Hallo *myResourceGroupAvailability*resourcegroep.

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

Beschikbaarheidssets kunnen u resources tooisolate over 'foutdomeinen' en 'domeinen bijwerken'. Een **foutdomein** vertegenwoordigt een geïsoleerd verzameling server + netwerk en opslag resources. Hallo voorgaande voorbeeld, geven we dat we dat onze beschikbaarheidsset toobe verdeeld over ten minste twee domeinen met fouten willen als onze virtuele machines worden geïmplementeerd. We ook aangeven dat we onze beschikbaarheidsset gedistribueerde in twee **domeinen bijwerken**.  Twee domeinen van de update ervoor te zorgen dat wanneer Azure voert de software-updates voor onze VM-netwerkbronnen geïsoleerd, waardoor alle Hallo software uitgevoerd onder de virtuele machine wordt bijgewerkt op Hallo hetzelfde moment.

## <a name="configure-virtual-network"></a>Virtueel netwerk configureren
Voordat u een aantal virtuele machines implementeren en uw balancer kunt testen, maak Hallo ondersteunende resources van een virtueel netwerk. Zie voor meer informatie over virtuele netwerken Hallo [Azure Virtual Networks beheren](tutorial-virtual-network.md) zelfstudie.

### <a name="create-network-resources"></a>Maken van netwerkbronnen
Maak een virtueel netwerk met [az network vnet maken](/cli/azure/network/vnet#create). Hallo volgende voorbeeld wordt een virtueel netwerk met de naam *myVnet* met een subnet met de naam *mySubnet*:

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
Virtuele NIC's zijn gemaakt met [az netwerk nic maken](/cli/azure/network/nic#create). Hallo maakt volgende voorbeeld drie virtuele NIC's. (Een virtuele NIC voor elke VM die u maakt voor uw app in hello te volgen stappen.) U kunt extra virtuele NIC's en virtuele machines maken op elk gewenst moment en ze toohello load balancer toevoegen:

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

Virtuele machines moeten worden gemaakt binnen Hallo beschikbaarheid set toomake zeker van te zijn dat ze correct zijn verdeeld over Hallo hardware. U kunt een bestaande VM tooan beschikbaarheidsset nadat deze is gemaakt niet toevoegen. 

Wanneer u een virtuele machine met maakt [az vm maken](/cli/azure/vm#create) u Hallo beschikbaarheid instellen met behulp van Hallo opgeven `--availability-set` toospecify Hallo parameternaam van Hallo beschikbaarheidsset.

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

Nu hebben we twee virtuele machines in onze nieuwe beschikbaarheidsset. Omdat ze zich in dezelfde Hallo beschikbaarheidsset, Azure zorgt ervoor dat Hallo VM's en alle hun bronnen (met inbegrip van gegevensschijven) worden gedistribueerd over geïsoleerde fysieke hardware. Deze verdeling kan ervoor zorgen veel hogere beschikbaarheid van de algehele oplossing voor de VM.

Wat die u tegenkomen kunt wanneer u virtuele machines toevoegt is een bepaalde VM-grootte is niet langer beschikbaar toouse binnen uw beschikbaarheidsset. Dit probleem kan zich voordoen als er niet langer voldoende capaciteit tooadd het is behoud van Hallo beschikbaarheidsset voor Hallo isolatie regels worden afgedwongen. U kunt toosee controleren welke VM-grootten zijn beschikbaar toouse binnen een bestaande beschikbaarheidsset gebruiken Hallo `--availability-set list-sizes` parameter.

## <a name="check-for-available-vm-sizes"></a>Controleren op beschikbare VM-grootten 

U kunt meer virtuele machines toohello beschikbaarheidsset later toevoegen, maar u moet tooknow welke VM-grootten zijn beschikbaar op Hallo hardware. Gebruik [az vm beschikbaarheidsset lijst met grootten](/cli/azure/availability-set#list-sizes) toolist alle beschikbare grootten van Hallo op Hallo hardware-cluster voor Hallo beschikbaarheidsset.

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

Toohello volgende zelfstudie toolearn over virtuele-machineschaalsets gaan.

> [!div class="nextstepaction"]
> [Een VM-schaalset maken](tutorial-create-vmss.md)

