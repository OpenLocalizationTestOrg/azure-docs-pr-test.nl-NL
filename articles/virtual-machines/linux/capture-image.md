---
title: een installatiekopie van een Linux-VM in Azure met CLI 2.0 aaaCapture | Microsoft Docs
description: Een installatiekopie van een virtuele machine van Azure toouse voor grootschalige implementaties met hello Azure CLI 2.0.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: 9558332a86186b282775097428df462709373012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-image-of-a-virtual-machine-or-vhd"></a>Hoe toocreate een installatiekopie van een virtuele machine of de VHD

<!-- generalize, image - extended version of hello tutorial-->

toocreate meerdere exemplaren van een virtuele machine (VM) toouse in Azure, een installatiekopie van Hallo VM of Hallo OS VHD. een installatiekopie van een toocreate, moet u persoonlijke gegevens die het maakt veiliger toodeploy meerdere keren verwijderen. Toewijzing in Hallo volgende stappen uit die u een bestaande VM inrichting ervan ongedaan, en een installatiekopie maken. U kunt deze installatiekopie toocreate VM's op elke willekeurige resourcegroep gebruiken in uw abonnement.

Als u een kopie van uw bestaande Linux VM toocreate voor back-up of foutopsporing wilt of een gespecialiseerde Linux VHD van een lokale virtuele machine uploaden, Zie [uploaden en Linux-VM te maken van aangepaste schijfimage](upload-vhd.md).  

U kunt ook **verpakker** toocreate uw aangepaste configuratie. Zie voor meer informatie over het gebruik van verpakker [hoe toouse verpakker toocreate virtuele Linux-machine in Azure afbeeldingen](build-image-with-packer.md).


## <a name="before-you-begin"></a>Voordat u begint
Zorg ervoor dat u voldoet aan de Hallo volgende vereisten:

* U moet een Azure VM gemaakt in Hallo Resource Manager-implementatiemodel met beheerde schijven. Als u een Linux-VM nog niet hebt gemaakt, kunt u Hallo [portal](quick-create-portal.md), Hallo [Azure CLI](quick-create-cli.md), of [Resource Manager-sjablonen](create-ssh-secured-vm-from-template.md). Configureer Hallo VM indien nodig. Bijvoorbeeld: [gegevensschijven toevoegen](add-disk.md), toepassen van updates en toepassingen te installeren. 

* U moet ook toohave Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en worden vastgelegd in het Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).

## <a name="quick-commands"></a>Snelle opdrachten

Zie voor een vereenvoudigde versie van dit onderwerp voor het testen, evalueren of leren over virtuele machines in Azure, [maken van een aangepaste installatiekopie van een virtuele machine van Azure CLI Hallo met](tutorial-custom-images.md).


## <a name="step-1-deprovision-hello-vm"></a>Stap 1: Deprovision Hallo VM
U inrichting ervan ongedaan Hallo VM, met hello Azure VM-agent, toodelete machine specifieke bestanden en gegevens. Gebruik Hallo `waagent` opdracht Hello *-deprovision + user* parameter bij de bron-Linux-VM. Zie voor meer informatie, Hallo [gebruikershandleiding voor Azure Linux Agent](../windows/agent-user-guide.md).

1. Verbinding maken met behulp van een SSH-client voor Linux-VM tooyour.
2. Typ in Hallo SSH venster Hallo volgende opdracht:
   
    ```bash
    sudo waagent -deprovision+user
    ```
<br>
   > [!NOTE]
   > Alleen worden uitgevoerd met deze opdracht op een virtuele machine die u van plan toocapture als afbeelding bent. Het is geen die installatiekopie Hallo van alle gevoelige informatie is uitgeschakeld of geschikt is voor de herdistributie van garantie. Hallo *+ user* parameter Hallo laatste ingerichte gebruikersaccount, worden ook verwijderd. Desgewenst kunt u de accountreferenties tookeep in Hallo VM gebruiken *-deprovision* tooleave Hallo-gebruikersaccount in plaats.
 
3. Type **y** toocontinue. U kunt Hallo toevoegen **-afdwingen** parameter tooavoid deze bevestigingsstap.
4. Nadat het Hallo-opdracht is voltooid, typt u **sluiten**. Deze stap wordt gesloten Hallo SSH-client.

## <a name="step-2-create-vm-image"></a>Stap 2: Maak een VM-installatiekopie
Hello Azure CLI 2.0 toomark Hallo VM gebruiken zoals gegeneraliseerd en Hallo installatiekopie vastleggen. In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden. De namen van de voorbeeld-parameter *myResourceGroup*, *myVnet*, en *myVM*.

1. Toewijzing van Hallo VM die u gemaakt met [az vm ongedaan](/cli//azure/vm#deallocate). Hallo volgende voorbeeld deallocates Hallo VM met de naam *myVM* in Hallo resourcegroep met de naam *myResourceGroup*:
   
    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myVM
    ```

2. Markeren Hallo VM zoals gegeneraliseerd met [az vm generalize](/cli//azure/vm#generalize). Hallo na voorbeeld aanhalingstekens Hallo Hallo VM met de naam *myVM* in Hallo resourcegroep met de naam *myResourceGroup* zoals gegeneraliseerd:
   
    ```azurecli
    az vm generalize \
      --resource-group myResourceGroup \
      --name myVM
    ```

3. Maak nu een afbeelding van Hallo VM-resource met [az installatiekopie maken](/cli//azure/image#create). Hallo volgende voorbeeld wordt een installatiekopie met de naam *myImage* in Hallo resourcegroep met de naam *myResourceGroup* Hallo VM-resource met de naam met *myVM*:
   
    ```azurecli
    az image create \
      --resource-group myResourceGroup \
      --name myImage --source myVM
    ```
   
   > [!NOTE]
   > Hallo installatiekopie is gemaakt in Hallo dezelfde resourcegroep bevindt als de bron-VM. U kunt virtuele machines in elke willekeurige resourcegroep maken in uw abonnement vanuit deze installatiekopie. Vanuit het perspectief van een management, kunt u desgewenst toocreate een specifieke resourcegroep voor uw VM netwerkbronnen en afbeeldingen.

## <a name="step-3-create-a-vm-from-hello-captured-image"></a>Stap 3: Een virtuele machine maken vanuit Hallo vastgelegde installatiekopie
Een virtuele machine maken met Hallo-installatiekopie die u hebt gemaakt met [az vm maken](/cli/azure/vm#create). Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVMDeployed* uit Hallo installatiekopie met de naam *myImage*:

```azurecli
az vm create \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --image myImage\
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```

### <a name="creating-hello-vm-in-another-resource-group"></a>Hallo VM maken in een andere resourcegroep 

U kunt virtuele machines maken van een installatiekopie in elke willekeurige resourcegroep binnen uw abonnement. een virtuele machine in een andere resourcegroep dan Hallo-installatiekopie toocreate Hallo volledige resource-ID tooyour afbeelding opgeven. Gebruik [az afbeeldingenlijst](/cli/azure/image#list) tooview een lijst met afbeeldingen. Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

Hallo volgende voorbeeld wordt [az vm maken](/cli/azure/vm#create) toocreate een virtuele machine in een andere resourcegroep dan de broninstallatiekopie Hallo door te geven Hallo Afbeeldingsbron-ID:

```azurecli
az vm create \
   --resource-group myOtherResourceGroup \
   --name myOtherVMDeployed \
   --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage" \
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```


## <a name="step-4-verify-hello-deployment"></a>Stap 4: Hallo implementatie controleren

Nu SSH toohello virtuele machine u tooverify Hallo implementatie en begin met behulp van gemaakt Hallo nieuwe virtuele machine. tooconnect via SSH, vinden Hallo IP-adres of FQDN-naam van uw virtuele machine met [az vm weergeven](/cli/azure/vm#show):

```azurecli
az vm show \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --show-details
```

## <a name="next-steps"></a>Volgende stappen
U kunt meerdere virtuele machines maken van de bron-VM-installatiekopie. Als u toomake wijzigingen tooyour installatiekopie moet: 

- Een virtuele machine maken van uw installatiekopie.
- Controleer op updates of wijzigingen in de configuratie.
- Ga als volgt Hallo stappen opnieuw toodeprovision, toewijzing generaliseren en een installatiekopie maken.
- Deze nieuwe installatiekopie gebruiken voor toekomstige implementaties. Indien gewenst, verwijder Hallo originele installatiekopie.

Zie voor meer informatie over het beheren van uw virtuele machines met Hallo CLI [Azure CLI 2.0](/cli/azure/overview).
