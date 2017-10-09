---
title: aaaInstall MySQL op een VM OpenSUSE | Microsoft Docs
description: Meer informatie over tooinstall MySQL op een machine OpenSUSE Linux VMirtual in Azure.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1594e10e-c314-455a-9efb-a89441de364b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/19/2016
ms.author: cynthn
ms.openlocfilehash: 8f96d29f29cb9c466dd7fdaf92b378783fdaacd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-mysql-on-a-virtual-machine-running-opensuse-linux-in-azure"></a>MySQL op een a virtuele machine met OpenSUSE Linux installeren in Azure
[MySQL] [ MySQL] is een populaire, open-source SQL-database. Deze zelfstudie leert u hoe een virtuele machine waarop OpenSUSE Linux toocreate vervolgens MySQL installeren.

> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.

<br>

## <a name="create-a-virtual-machine-running-opensuse-linux"></a>Een virtuele machine met OpenSUSE Linux maken
[!INCLUDE [create-and-configure-opensuse-vm-in-portal](../../../../includes/create-and-configure-opensuse-vm-in-portal.md)]

## <a name="install-and-run-mysql-on-hello-virtual-machine"></a>Installeren en uitvoeren van MySQL op Hallo virtuele machine
[!INCLUDE [install-and-run-mysql-on-opensuse-vm](../../../../includes/install-and-run-mysql-on-opensuse-vm.md)]

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over MySQL Hallo [MySQL documentatie][MySQLDocs].

[MySQLDocs]:http://dev.mysql.com/doc/index-topic.html
[MySQL]:http://www.mysql.com

