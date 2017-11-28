---
title: MySQL installeren op een VM OpenSUSE | Microsoft Docs
description: Informatie over het installeren van MySQL op een machine OpenSUSE Linux VMirtual in Azure.
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
ms.openlocfilehash: 01b798a25575b66f89057315ce80d6cc0cde53b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="install-mysql-on-a-virtual-machine-running-opensuse-linux-in-azure"></a><span data-ttu-id="4a99b-103">MySQL op een a virtuele machine met OpenSUSE Linux installeren in Azure</span><span class="sxs-lookup"><span data-stu-id="4a99b-103">Install MySQL on a virtual machine running OpenSUSE Linux in Azure</span></span>
<span data-ttu-id="4a99b-104">[MySQL] [ MySQL] is een populaire, open-source SQL-database.</span><span class="sxs-lookup"><span data-stu-id="4a99b-104">[MySQL][MySQL] is a popular, open-source SQL database.</span></span> <span data-ttu-id="4a99b-105">Deze zelfstudie laat zien hoe u een virtuele machine met OpenSUSE Linux maken en vervolgens MySQL installeren.</span><span class="sxs-lookup"><span data-stu-id="4a99b-105">This tutorial shows you how to create a virtual machine running OpenSUSE Linux, then install MySQL.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="4a99b-106">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4a99b-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4a99b-107">In dit artikel bevat informatie over met behulp van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="4a99b-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="4a99b-108">U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4a99b-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<br>

## <a name="create-a-virtual-machine-running-opensuse-linux"></a><span data-ttu-id="4a99b-109">Een virtuele machine met OpenSUSE Linux maken</span><span class="sxs-lookup"><span data-stu-id="4a99b-109">Create a virtual machine running OpenSUSE Linux</span></span>
[!INCLUDE [create-and-configure-opensuse-vm-in-portal](../../../../includes/create-and-configure-opensuse-vm-in-portal.md)]

## <a name="install-and-run-mysql-on-the-virtual-machine"></a><span data-ttu-id="4a99b-110">Installeren en uitvoeren van MySQL op de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="4a99b-110">Install and run MySQL on the virtual machine</span></span>
[!INCLUDE [install-and-run-mysql-on-opensuse-vm](../../../../includes/install-and-run-mysql-on-opensuse-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="4a99b-111">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4a99b-111">Next steps</span></span>
<span data-ttu-id="4a99b-112">Zie voor meer informatie over MySQL, de [MySQL documentatie][MySQLDocs].</span><span class="sxs-lookup"><span data-stu-id="4a99b-112">For details about MySQL, see the [MySQL Documentation][MySQLDocs].</span></span>

[MySQLDocs]:http://dev.mysql.com/doc/index-topic.html
[MySQL]:http://www.mysql.com

