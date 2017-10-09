---
title: aaaLog op tooa klassieke virtuele machine in Azure | Microsoft Docs
description: Hello Azure portal toolog op tooa Windows virtuele machine gemaakt met het klassieke implementatiemodel hello gebruiken.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 3c1239ed-07dc-48b8-8b3d-dc8c5f0ab20e
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 2e32b7036c2538e73b46580e0f5f8f4979e8a685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="log-on-tooa-windows-virtual-machine-using-hello-azure-portal"></a>Meld u aan tooa Windows virtuele machine met behulp van hello Azure-portal
In hello Azure-portal, gebruikt u Hallo **Connect** knop toostart een extern bureaublad-sessie en meld u aan tooa virtuele machine van Windows.

Wilt u tooconnect tooa Linux VM? Zie [hoe toolog op tooa virtuele machine met Linux](../../linux/mac-create-ssh-keys.md).

<!--
Deleting, but not 100% sure
Learn how too[perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Voor informatie over hoe toolog over het gebruik van tooa VM Resource Manager Hallo model, Zie [hier](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="connect-toohello-virtual-machine"></a>Verbinding maken met toohello virtuele machine
1. Meld u aan toohello Azure-portal.
2. Klik op Hallo virtuele machine die u tooaccess wilt. Hallo-naam wordt weergegeven in Hallo **alle resources** deelvenster.

    ![Virtuele-machine-locaties](./media/connect-logon/azureportaldashboard.png)

3. Klik op **Connect** op de opdrachtbalk Hallo op Hallo virtuele machine dashboard.

    ![Pictogram voor Hallo virtuele machine verbinding maken](./media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If hello **Connect** button isn't available, see hello troubleshooting tips at hello end of this article.
>
>
-->

## <a name="log-on-toohello-virtual-machine"></a>Meld u aan toohello virtuele machine
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a>Volgende stappen
* Als hello **Connect** knop is niet actief of er andere problemen met extern bureaublad-verbinding hello, probeert u Hallo-configuratie wordt opnieuw ingesteld. Klik op **externe toegang opnieuw instellen** vanuit Hallo virtuele machine dashboard.

    ![Opnieuw instellen van externe toegang](./media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* Probeer de fabrieksinstellingen voor problemen met het wachtwoord. Klik op **wachtwoord opnieuw instellen** langs Hallo de linkerrand van virtuele machine dashboard onder **ondersteuning + probleemoplossing**.

    ![Wachtwoord opnieuw instellen](./media/connect-logon/virtualmachine_dashboard_reset_password.png)

Als deze tips werken niet of niet wat u nodig hebt, gaat u naar [tooa van problemen met extern bureaublad-verbindingen op basis van Windows Azure virtuele Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Dit artikel leidt u door het opsporen en oplossen van veelvoorkomende problemen.
