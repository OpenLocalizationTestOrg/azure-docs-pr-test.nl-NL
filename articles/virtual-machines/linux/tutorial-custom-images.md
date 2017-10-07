---
title: "aangepaste VM-installatiekopieën aaaCreate Hello Azure CLI | Microsoft Docs"
description: Zelfstudie - een aangepaste VM-installatiekopie met behulp van Azure CLI Hallo maken.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/21/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 217a993c0c1d48939b74108ac6c5f7a1a619416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-hello-cli"></a>Een aangepaste installatiekopie van een virtuele machine in Azure met behulp van Hallo CLI maken

Aangepaste installatiekopieën zijn zoals marketplace-installatiekopieën, maar u deze zelf maken. Aangepaste installatiekopieën kunnen worden gebruikt toobootstrap configuraties zoals vooraf laden van toepassingen, toepassingsconfiguraties en andere configuraties OS. In deze zelfstudie maakt u uw eigen aangepaste installatiekopie van een virtuele machine van Azure. Procedures voor:

> [!div class="checklist"]
> * Inrichting ervan ongedaan en generalize van virtuele machines
> * Een aangepaste installatiekopie maken
> * Een virtuele machine van een aangepaste installatiekopie maken
> * Lijst van alle Hallo-installatiekopieën in uw abonnement
> * Een afbeelding verwijderen


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="before-you-begin"></a>Voordat u begint

Hallo stappen hieronder wordt beschreven hoe tootake een bestaande virtuele machine en schakel dit in een herbruikbare aangepaste installatiekopie die u hebt de nieuwe VM-instanties toocreate kunnen gebruiken.

toocomplete hello voorbeeld in deze zelfstudie, moet u een bestaande virtuele machine hebben. Indien nodig, dit [voorbeeldscript](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) kunt maken voor u. Wanneer werkende Hallo-zelfstudie vervangt benoemt Hallo resourcegroep en de VM waar nodig.

## <a name="create-a-custom-image"></a>Een aangepaste installatiekopie maken

toocreate een installatiekopie van een virtuele machine, moet u tooprepare Hallo VM opheffen van inrichting, toewijzing en wordt vervolgens markeren Hallo bron-VM als gegeneraliseerd. Eenmaal Hallo die VM is voorbereid, kunt u een installatiekopie.

### <a name="deprovision-hello-vm"></a>Identiteitsgegevens Hallo VM 

Opheffen van inrichting Hallo VM generaliseert door machine-specifieke informatie te verwijderen. Deze generaliseren maakt het mogelijk toodeploy veel virtuele machines van één installatiekopie. Tijdens het opheffen van inrichting, Hallo hostnaam op te stellen*localhost.localdomain*. Host-SSH-sleutels, naamserver configuraties hoofdwachtwoord en in de cache DHCP-leases worden ook verwijderd.

toodeprovision hello virtuele machine, gebruik hello Azure VM-agent (waagent). Hello Azure VM-agent is geïnstalleerd op Hallo VM en inrichting en interactie met hello Azure-Infrastructuurcontroller beheert. Zie voor meer informatie, Hallo [gebruikershandleiding voor Azure Linux Agent](agent-user-guide.md).

Tooyour VM verbinding maken met behulp van SSH en Voer Hallo opdracht toodeprovision Hallo VM. Hello `+user` argument, Hallo laatste ingerichte gebruikersaccount en alle bijbehorende gegevens worden ook verwijderd. Hallo voorbeeld IP-adres vervangen door Hallo openbare IP-adres van uw virtuele machine.

SSH toohello VM.
```bash
ssh azureuser@52.174.34.95
```
Identiteitsgegevens hello VM.

```bash
sudo waagent -deprovision+user -force
```
Hallo SSH-sessie te sluiten.

```bash
exit
```

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a>Toewijzing ongedaan maken en Hallo VM zoals gegeneraliseerd markeren

een installatiekopie van een toocreate, Hallo VM moet toobe toewijzing ongedaan gemaakt. Toewijzing virtuele machine met behulp van Hallo [az vm ongedaan](/cli//azure/vm#deallocate). 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

Tot slot stelt Hallo status Hallo VM zoals gegeneraliseerd met [az vm generalize](/cli//azure/vm#generalize) zodat hello Azure-platform Hallo VM is gegeneraliseerd. U kunt alleen een installatiekopie van het maken van een gegeneraliseerde virtuele machine.
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-hello-image"></a>Hallo installatiekopie maken

Nu u een installatiekopie van Hallo VM maken met behulp van kunt [az installatiekopie maken](/cli//azure/image#create). Hallo volgende voorbeeld wordt een installatiekopie met de naam *myImage* van een virtuele machine met de naam *myVM*.
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-hello-image"></a>Virtuele machines uit Hallo installatiekopie maken

Nu dat u een installatiekopie hebt, kunt u een of meer nieuwe virtuele machines kunt maken van het Hallo-installatiekopie met [az vm maken](/cli/azure/vm#create). Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVMfromImage* uit Hallo installatiekopie met de naam *myImage*.

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a>Beheer van installatiekopieën 

Hier volgen enkele voorbeelden van algemene beheertaken voor de installatiekopie en hoe toocomplete ze met behulp van hello Azure CLI.

Lijst van alle installatiekopieën met de naam in een tabel.

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

Een afbeelding verwijderen. In dit voorbeeld verwijderingen Hallo installatiekopie met de naam *myOldImage* van Hallo *myResourceGroup*.

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie maakt u een aangepaste installatiekopie van de virtuele machine gemaakt. U hebt geleerd hoe u:

> [!div class="checklist"]
> * Inrichting ervan ongedaan en generalize van virtuele machines
> * Een aangepaste installatiekopie maken
> * Een virtuele machine van een aangepaste installatiekopie maken
> * Lijst van alle Hallo-installatiekopieën in uw abonnement
> * Een afbeelding verwijderen

Ga toohello volgende zelfstudie toolearn over maximaal beschikbare virtuele machines.

> [!div class="nextstepaction"]
> [Maximaal beschikbare virtuele machines maken](tutorial-availability-sets.md).

