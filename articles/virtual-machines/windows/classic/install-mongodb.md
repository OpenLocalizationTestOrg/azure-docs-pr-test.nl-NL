---
title: aaaInstall MongoDB op een Windows-virtuele machine in Azure | Microsoft Docs
description: Meer informatie over hoe tooinstall MongoDB op een Azure VM is gemaakt met het klassieke implementatiemodel Hallo met Windows Server.
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4095df41-bb69-4bbe-9c1c-70923b0d84ba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: iainfou
ms.openlocfilehash: aafd86b4c49c6a97ae8a1a2191ae375b6c47483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a>MongoDB installeren op een Windows virtuele machine in Azure
> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).  In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. tooinstall en MongoDB met Resource Manager-implementatiemodel Hallo configureren, Zie [in dit artikel](../install-mongodb.md).

[MongoDB] [ MongoDB] is een populaire open-source, hoogwaardige NoSQL-database. In dit artikel begeleidt u bij het maken van een Windows Server virtuele machine (VM) met Hallo [Azure-portal][AzurePortal]. U maken en koppelen van een data schijf toohello VM voordat installeren en configureren van MongoDB. Als u een bestaande virtuele machine in Azure dat u toouse wilt hebt, kunt u gaan meteen te[installeren en configureren van MongoDB](#install-and-run-mongodb-on-the-virtual-machine).

## <a name="create-a-virtual-machine-running-windows-server"></a>Een virtuele machine maken waarop Windows Server wordt uitgevoerd
Volg deze instructies toocreate een virtuele machine.

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> U kunt een eindpunt voor MongoDB toevoegen tijdens het Hallo virtuele machine maken en als volgt configureren: deze als de naam **Mongo**, gebruik **TCP** zoals Hallo-protocol en stel beide Hallo openbare en particuliere poort te**27017**.
>
>

## <a name="attach-a-data-disk"></a>Een gegevensschijf koppelen
tooprovide opslag voor Hallo virtuele machine, een gegevensschijf koppelen en initialiseren zodat Windows kan worden gebruikt. Als u een gegevensschijf al hebt, kunt u de bestaande schijf koppelen of kunt u een lege schijf koppelen.

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

Zie voor instructies voor het initialiseren van Hallo schijf, ' How to: initialiseren van een nieuwe gegevensschijf in WindowsServer "in [hoe tooattach data tooa virtuele Windows-machine schijf](attach-disk.md).

## <a name="install-and-run-mongodb-on-hello-virtual-machine"></a>Installeren en uitvoeren van MongoDB op Hallo virtuele machine
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a>Samenvatting
In deze zelfstudie hebt u geleerd hoe toocreate een virtuele machine met Windows Server op afstand verbinding tooit en een gegevensschijf koppelen.  U hebt ook geleerd hoe tooinstall en het configureren van MongoDB op Hallo Windows gebaseerde virtuele machine. U kunt nu toegang tot MongoDB op Hallo Windows gebaseerde virtuele machine door na Hallo geavanceerde onderwerpen in Hallo [MongoDB-documentatie][MongoDocs].

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/

