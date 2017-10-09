---
title: aaaInject gegevens in de Windows-machines in Azure | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe tooinject aangepaste gegevens in een Azure virtuele machine wanneer Hallo-exemplaar wordt gemaakt en hoe toolocate Hallo aangepaste gegevens op Windows of Linux.
services: virtual-machines-windows
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 48759f76-eaa0-4202-ada0-706d3f9a9467
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: 2b2a12e5d0942fa957387ace7e38a353dbf27197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="injecting-custom-data-into-an-azure-virtual-machine"></a><span data-ttu-id="210ad-103">Injecteren van aangepaste gegevens in Azure een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="210ad-103">Injecting custom data into an Azure virtual machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="210ad-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="210ad-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="210ad-105">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="210ad-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="210ad-106">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="210ad-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="210ad-107">Zie voor meer informatie over het gebruik van aangepaste Scriptextensie Hallo met Resource Manager-model Hallo [hier](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="210ad-107">For information about using hello Custom Script Extension with hello Resource Manager model, see [here](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-inject-custom-data](../../../../includes/virtual-machines-common-classic-inject-custom-data.md)]

