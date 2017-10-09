---
title: een installatiekopie van een Windows Azure VM aaaCapture | Microsoft Docs
description: Een installatiekopie van een Windows Azure virtuele machine gemaakt met het klassieke implementatiemodel Hallo.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: a5986eac-4cf3-40bd-9b79-7c811806b880
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: b9bbc437012aa44295f90941c9d72e39509df28f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="capture-an-image-of-an-azure-windows-virtual-machine-created-with-hello-classic-deployment-model"></a>Een installatiekopie van een Windows Azure virtuele machine gemaakt met het klassieke implementatiemodel Hallo.
> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Zie voor informatie over het model van de Resource Manager, [beheerde-installatiekopie van een gegeneraliseerde virtuele machine in Azure](../capture-image-resource.md).

Dit artikel ziet u hoe toocapture Azure een virtuele machine met Windows zodat u deze als een installatiekopie toocreate gebruiken kunt andere virtuele machines. Deze installatiekopie bevat schijf Hallo-besturingssysteem en eventuele gegevensschijven die zijn gekoppeld toohello virtuele machine. Het bevat geen netwerkconfiguraties, dus u tooset up netwerkconfiguraties moet wanneer u andere virtuele machines die gebruikmaken van de installatiekopie van het Hallo Hallo maakt.

Azure winkels Hallo afbeelding onder **VM-installatiekopieën (klassiek)**, een **Compute** service die wordt weergegeven wanneer u alle bekijkt hello Azure-services. Dit is Hallo dezelfde locatie waar alle installatiekopieën die u hebt geüpload worden opgeslagen. Zie voor meer informatie over installatiekopieën [over installatiekopieën voor virtuele machines](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).

## <a name="before-you-begin"></a>Voordat u begint
Deze stappen wordt ervan uitgegaan dat u hebt al een virtuele machine in Azure gemaakt en geconfigureerd Hallo-besturingssysteem, met inbegrip van eventuele gegevensschijven koppelen. Als u dit nog niet hebt gedaan, raadpleegt u Hallo volgende artikelen voor meer informatie over het maken en Hallo virtuele machine wordt voorbereid:

* [Een virtuele machine van een installatiekopie maken](createportal.md)
* [Hoe tooattach data schijf tooa virtuele machine](attach-disk.md)
* Zorg ervoor dat het Hallo-serverfuncties worden ondersteund met Sysprep. Zie voor meer informatie [Sysprep-ondersteuning voor serverrollen](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).

> [!WARNING]
> Dit proces verwijderd Hallo oorspronkelijke virtuele machine nadat deze vastgelegd.
>
>

Eerdere toocapturing een afbeelding van een virtuele machine van Azure wordt aanbevolen Hallo doel-virtuele machine een back-up. Virtuele machines van Azure kan een back-up maken met Azure Backup. Zie [Back-ups maken van virtuele machines van Azure](../../../backup/backup-azure-vms.md) voor meer informatie. Andere oplossingen zijn beschikbaar van gecertificeerde partners. toofind informatie over wat er momenteel beschikbaar is, zoek hello Azure Marketplace.

## <a name="capture-hello-virtual-machine"></a>Hallo-machine vastleggen
1. In Hallo [Azure-portal](http://portal.azure.com), **Connect** toohello virtuele machine. Zie voor instructies [hoe toosign in tooa virtuele machine met Windows Server][How toosign in tooa virtual machine running Windows Server].
2. Open een opdrachtpromptvenster als administrator.
3. Hallo directory ook wijzigen`%windir%\system32\sysprep`, en voer vervolgens sysprep.exe.
4. Hallo **hulpprogramma voor systeemvoorbereiding** dialoogvenster wordt weergegeven. Hallo te volgen:

   * In **System opschonen actie**, selecteer **System Voer Out-of-Box Experience (OOBE)** en zorg ervoor dat **Generalize** is ingeschakeld. Zie voor meer informatie over het gebruik van Sysprep [hoe tooUse Sysprep: An Introduction][How tooUse Sysprep: An Introduction].
   * In **afsluitopties**, selecteer **afsluiten**.
   * Klik op **OK**.

   ![Voer Sysprep uit](./media/capture-image/SysprepGeneral.png)
5. Sysprep is afgesloten Hallo virtuele machine, waardoor Hallo status van Hallo virtuele machine in hello Azure-portal te wijzigt**gestopt**.
6. Klik in hello Azure-portal, op **virtuele Machines (klassiek)** en selecteer de virtuele machine die u wilt dat toocapture Hallo. Hallo **VM-installatiekopieën (klassiek)** groep wordt vermeld onder **Compute** wanneer u bekijkt **meer services**.

7. Klik op de opdrachtbalk Hallo **vastleggen**.

   ![Virtuele machine vastleggen](./media/capture-image/CaptureVM.png)

   Hallo **vastleggen Hallo virtuele Machine** dialoogvenster wordt weergegeven.

8. In **installatiekopienaam**, typ een naam voor de nieuwe installatiekopie Hallo. In **installatiekopie label**, typt u een label voor de nieuwe installatiekopie Hallo.

9. Klik op **ik heb Sysprep uitgevoerd op de virtuele machine van Hallo**. Dit selectievakje verwijst toohello acties met Sysprep in stap 3-5. Een installatiekopie van een _moet_ worden gegeneraliseerd met Sysprep voordat u een Windows-Server toevoegen installatiekopie tooyour set aangepaste installatiekopieën.

10. Zodra Hallo vastleggen is voltooid, de nieuwe installatiekopie Hallo beschikbaar in Hallo **Marketplace**, in Hallo **Compute**, **VM-installatiekopieën (klassiek)** container.

    ![De installatiekopie is geslaagd](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a>Volgende stappen
Hallo-installatiekopie is gereed toobe gebruikt toocreate virtuele machines. toodo dit, maakt u een virtuele machine door het selecteren van Hallo **meer services** menuopdracht Hallo Hallo services menu, klikt u vervolgens onder aan **VM-installatiekopieën (klassiek)** in Hallo **Compute**groep. Zie voor instructies [een virtuele machine maken van een installatiekopie van een](createportal.md).

[How toosign in tooa virtual machine running Windows Server]:connect-logon.md
[How tooUse Sysprep: An Introduction]: http://technet.microsoft.com/library/bb457073.aspx
[Run Sysprep.exe]: ./media/virtual-machines-capture-image-windows-server/SysprepCommand.png
[Enter Sysprep.exe options]: ./media/capture-image/SysprepGeneral.png
[hello virtual machine is stopped]: ./media/virtual-machines-capture-image-windows-server/SysprepStopped.png
[Capture an image of hello virtual machine]: ./media/capture-image/CaptureVM.png
[Enter hello image name]: ./media/virtual-machines-capture-image-windows-server/Capture.png
[Image capture successful]: ./media/virtual-machines-capture-image-windows-server/CaptureSuccess.png
[Use hello captured image]: ./media/virtual-machines-capture-image-windows-server/MyImagesWindows.png
