---
title: een installatiekopie van een Linux-VM aaaCapture | Microsoft Docs
description: Meer informatie over hoe toocapture een installatiekopie van een Linux-gebaseerde Azure virtuele machine (VM) gemaakt met het klassieke implementatiemodel Hallo.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17d7ffee-a58e-4290-9de1-64c3cf1ddc05
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 33c4059d5bb919a86bdc3492abca540750f365ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocapture-a-classic-linux-virtual-machine-as-an-image"></a>Hoe toocapture klassieke virtuele Linux-machine als afbeelding
> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Meer informatie over hoe te[u deze stappen uitvoert met behulp van de Resource Manager-model Hallo](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Dit artikel ziet u hoe toocapture een klassieke Azure virtuele machine (VM) met Linux als een installatiekopie toocreate andere virtuele machines. Deze installatiekopie bevat Hallo besturingssysteemschijf en gegevensschijven toohello VM gekoppeld. Zijn niet opgenomen netwerkconfiguratie, dus u tooconfigure moet die bij het maken van Hallo andere virtuele machine uit Hallo-installatiekopie.

Azure winkels Hallo afbeelding onder **installatiekopieën**, samen met alle installatiekopieën die u hebt geüpload. Zie voor meer informatie over installatiekopieën [over installatiekopieën van virtuele machines in Azure][About Virtual Machine Images in Azure].

## <a name="before-you-begin"></a>Voordat u begint
Deze stappen wordt ervan uitgegaan dat u een virtuele machine in Azure met behulp van Hallo klassieke implementatiemodel en geconfigureerde Hallo-besturingssysteem, met inbegrip van eventuele gegevensschijven koppelen al hebt gemaakt. Als u een virtuele machine toocreate nodig hebt, leest u [hoe tooCreate virtuele Linux-Machine][How tooCreate a Linux Virtual Machine].

## <a name="capture-hello-virtual-machine"></a>Hallo-machine vastleggen
1. [Verbinding maken met toohello VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) met behulp van een SSH-client van uw keuze.
2. Typ in Hallo SSH venster Hallo opdracht te volgen. Hallo de uitvoer van `waagent` enigszins kunnen variëren afhankelijk van Hallo-versie van dit hulpprogramma:

    ```bash
    sudo waagent -deprovision+user
    ```

    Hallo voorgaande opdracht tooclean Hallo systeem probeert, waardoor het geschikt is voor reprovisioning. Deze bewerking uitvoert Hallo taken te volgen:

   * Hiermee verwijdert u SSH-sleutels voor host (als Provisioning.RegenerateSshHostKeyPair 'y' in het configuratiebestand Hallo)
   * Hiermee wist u de configuratie van de naamserver in /etc/resolv.conf
   * Hiermee verwijdert u Hallo `root` gebruikerswachtwoord uit/etc/shadow (als Provisioning.DeleteRootPassword 'y' in het configuratiebestand Hallo)
   * Verwijdering van DHCP-clientlease uit de cache
   * Opnieuw instellen van hosten naam toolocalhost.localdomain
   * Hallo laatste ingerichte gebruikersaccount (verkregen uit /var/lib/waagent) verwijdert **en bijbehorende gegevens**.

     > [!NOTE]
     > Opheffen van inrichting verwijdert u bestanden en gegevens te 'generaliseer' hello installatiekopie. Met deze opdracht op een virtuele machine die u van plan toocapture als een nieuwe sjabloon voor de installatiekopie bent alleen worden uitgevoerd. Er is geen garantie die installatiekopie Hallo van alle gevoelige informatie is uitgeschakeld of geschikt is voor de herdistributie toothird partijen.

3. Type **y** toocontinue. U kunt toevoegen Hallo `-force` parameter tooavoid deze bevestigingsstap.
4. Type **afsluiten** tooclose Hallo SSH-client.

   > [!NOTE]
   > Hallo resterende stappen wordt ervan uitgegaan dat u al hebt [geïnstalleerd hello Azure CLI](../../../cli-install-nodejs.md) op de clientcomputer. Alle Hallo stappen te volgen kan ook worden uitgevoerd in Hallo [Azure-portal](http://portal.azure.com).

5. Open Azure CLI en aanmelding tooyour Azure-abonnement op de clientcomputer. Voor meer informatie lezen [tooan Azure-abonnement verbinden van hello Azure CLI](../../../xplat-cli-connect.md).

   > [!NOTE]
   > Aanmelden in hello Azure-portal, toohello-portal.

6. Zorg ervoor dat u in Service Management-modus:

    ```azurecli
    azure config mode asm
    ```

7. Schakel Hallo VM die is al gemaakt. Hallo volgende voorbeeld wordt afgesloten Hallo VM met de naam `myVM`:

    ```azurecli
    azure vm shutdown myVM
    ```
   Indien nodig, kunt u een lijst alle Hallo VM's in uw abonnement worden gemaakt met behulp van weergeven`azure vm list`

   > [!NOTE]
   > Als u hello Azure-portal, selecteert u Hallo VM en klikt u op **stoppen** de Hallo VM af te sluiten.

8. Wanneer Hallo VM is gestopt, kunt u Hallo installatiekopie vastleggen. Hallo na voorbeeld opnamen Hallo VM met de naam `myVM` en maakt u een algemene installatiekopie met de naam `myNewVM`:

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    Hallo `-t` subopdracht verwijderingen Hallo oorspronkelijke virtuele machine.

    > [!NOTE]
    > In hello Azure-portal, kunt u een installatiekopie vastleggen selecteren **installatiekopie** van Hallo hub-menu. U moet toosupply Hallo volgende informatie voor de installatiekopie van het Hallo: naam, resourcegroep, locatie, het besturingssysteemtype en pad van opslag-blob.

9. de nieuwe installatiekopie Hallo is nu beschikbaar in de lijst Hallo van installatiekopieën die kunnen worden gebruikt tooconfigure een nieuwe virtuele machine. Hallo-opdracht kunt u deze bekijken:

   ```azurecli
   azure vm image list
   ```

   Op Hallo [Azure-portal](http://portal.azure.com), nieuwe Hallo-afbeelding wordt weergegeven in Hallo **VM-installatiekopieën (klassiek)** die behoort toohello **Compute** services. U hebt toegang tot **VM-installatiekopieën (klassiek)** door te klikken op _meer services_ service Hallo hello Azure onderaan in de lijst en bekijkt hello **Compute** services.   

   ![De installatiekopie is geslaagd](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a>Volgende stappen
Hallo-installatiekopie is gereed toobe gebruikt toocreate virtuele machines. U kunt Azure CLI-opdracht Hallo `azure vm create` en geef Hallo installatiekopie-naam die u hebt gemaakt. Zie voor meer informatie [Using hello Azure CLI met het klassieke implementatiemodel](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

Ook gebruiken Hallo [Azure-portal](http://portal.azure.com) toocreate een aangepaste virtuele machine met behulp van Hallo **installatiekopie** methode en het selecteren van Hallo installatiekopie hebt gemaakt. Zie voor meer informatie [hoe een aangepaste VM tooCreate][How tooCreate a Custom Virtual Machine].

**Zie ook:** [gebruikershandleiding voor Azure Linux-Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How tooCreate a Custom Virtual Machine]:create-custom.md
[How tooAttach a Data Disk tooa Virtual Machine]:attach-disk.md
[How tooCreate a Linux Virtual Machine]:create-custom.md
