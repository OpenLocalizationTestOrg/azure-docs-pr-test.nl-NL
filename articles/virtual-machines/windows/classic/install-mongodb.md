---
title: MongoDB installeren op een Windows virtuele machine in Azure | Microsoft Docs
description: Informatie over het MongoDB installeren op een virtuele machine in Azure gemaakt met het klassieke implementatiemodel met Windows Server.
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
ms.openlocfilehash: 6b5af18d02fd508a21cdc21b38b1c16e79f07ecb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="aa95c-103">MongoDB installeren op een Windows virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="aa95c-103">Install MongoDB on a Windows VM in Azure</span></span>
> [!IMPORTANT]
> <span data-ttu-id="aa95c-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="aa95c-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="aa95c-105">In dit artikel bevat informatie over met behulp van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="aa95c-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="aa95c-106">U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aa95c-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="aa95c-107">Als u wilt installeren en configureren met het implementatiemodel van Resource Manager MongoDB, Zie [in dit artikel](../install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="aa95c-107">To install and configure MongoDB using the Resource Manager deployment model, see [this article](../install-mongodb.md).</span></span>

<span data-ttu-id="aa95c-108">[MongoDB] [ MongoDB] is een populaire open-source, hoogwaardige NoSQL-database.</span><span class="sxs-lookup"><span data-stu-id="aa95c-108">[MongoDB][MongoDB] is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="aa95c-109">In dit artikel begeleidt u bij het maken van een Windows Server-virtuele machine (VM) met de [Azure-portal][AzurePortal].</span><span class="sxs-lookup"><span data-stu-id="aa95c-109">This article guides you through creating a Windows Server virtual machine (VM) using the [Azure portal][AzurePortal].</span></span> <span data-ttu-id="aa95c-110">U maakt en een gegevensschijf koppelen aan de virtuele machine voor het installeren en configureren van MongoDB.</span><span class="sxs-lookup"><span data-stu-id="aa95c-110">You then create and attach a data disk to the VM before installing and configuring MongoDB.</span></span> <span data-ttu-id="aa95c-111">Hebt u een bestaande virtuele machine in Azure die u wilt gebruiken, kunt u meteen naar gaan [installeren en configureren van MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="aa95c-111">If you have an existing VM in Azure that you would like to use, you can jump straight to [installing and configuring MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span></span>

## <a name="create-a-virtual-machine-running-windows-server"></a><span data-ttu-id="aa95c-112">Een virtuele machine maken waarop Windows Server wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="aa95c-112">Create a virtual machine running Windows Server</span></span>
<span data-ttu-id="aa95c-113">Volg deze instructies voor het maken van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="aa95c-113">Follow these instructions to create a virtual machine.</span></span>

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> <span data-ttu-id="aa95c-114">U kunt een eindpunt voor MongoDB toevoegen tijdens het maken van de virtuele machine en als volgt configureren: deze als de naam **Mongo**, gebruiken **TCP** als het protocol en de openbare en particuliere poorten instellen op **27017**.</span><span class="sxs-lookup"><span data-stu-id="aa95c-114">You can add an endpoint for MongoDB while creating the virtual machine, and configure it as follows: name it as **Mongo**, use **TCP** as the protocol, and set both the public and private ports to **27017**.</span></span>
>
>

## <a name="attach-a-data-disk"></a><span data-ttu-id="aa95c-115">Een gegevensschijf koppelen</span><span class="sxs-lookup"><span data-stu-id="aa95c-115">Attach a data disk</span></span>
<span data-ttu-id="aa95c-116">Als u wilt opslag bieden voor de virtuele machine, een gegevensschijf koppelen en initialiseren zodat Windows kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="aa95c-116">To provide storage for the virtual machine, attach a data disk and then initialize it so that Windows can use it.</span></span> <span data-ttu-id="aa95c-117">Als u een gegevensschijf al hebt, kunt u de bestaande schijf koppelen of kunt u een lege schijf koppelen.</span><span class="sxs-lookup"><span data-stu-id="aa95c-117">If you already have a data disk, you can attach that existing disk, or you can attach an empty disk.</span></span>

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

<span data-ttu-id="aa95c-118">Zie voor instructies voor het initialiseren van de schijf, ' How to: initialiseren van een nieuwe gegevensschijf in WindowsServer "in [hoe een gegevensschijf koppelen aan een virtuele Windows-machine](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="aa95c-118">For instructions on initializing the disk, see "How to: Initialize a new data disk in Windows Server" in [How to attach a data disk to a Windows virtual machine](attach-disk.md).</span></span>

## <a name="install-and-run-mongodb-on-the-virtual-machine"></a><span data-ttu-id="aa95c-119">Installeren en uitvoeren van MongoDB op de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="aa95c-119">Install and run MongoDB on the virtual machine</span></span>
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a><span data-ttu-id="aa95c-120">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="aa95c-120">Summary</span></span>
<span data-ttu-id="aa95c-121">In deze zelfstudie hebt u geleerd hoe maakt u een virtuele machine met Windows Server op afstand verbinding mee maken en een gegevensschijf koppelen.</span><span class="sxs-lookup"><span data-stu-id="aa95c-121">In this tutorial, you learned how to create a virtual machine running Windows Server, remotely connect to it, and attach a data disk.</span></span>  <span data-ttu-id="aa95c-122">U hebt ook geleerd hoe installeren en configureren van MongoDB op Windows gebaseerde VM.</span><span class="sxs-lookup"><span data-stu-id="aa95c-122">You also learned how to install and configure MongoDB on the Windows-based virtual machine.</span></span> <span data-ttu-id="aa95c-123">U kunt nu toegang tot MongoDB op Windows gebaseerde virtuele machine aan de hand van de geavanceerde onderwerpen in de [MongoDB-documentatie][MongoDocs].</span><span class="sxs-lookup"><span data-stu-id="aa95c-123">You can now access MongoDB on the Windows-based virtual machine, by following the advanced topics in the [MongoDB documentation][MongoDocs].</span></span>

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/

