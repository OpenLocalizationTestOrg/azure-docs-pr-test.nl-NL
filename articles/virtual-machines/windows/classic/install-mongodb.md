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
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="a5698-103">MongoDB installeren op een Windows virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="a5698-103">Install MongoDB on a Windows VM in Azure</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a5698-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a5698-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="a5698-105">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="a5698-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="a5698-106">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a5698-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="a5698-107">tooinstall en MongoDB met Resource Manager-implementatiemodel Hallo configureren, Zie [in dit artikel](../install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="a5698-107">tooinstall and configure MongoDB using hello Resource Manager deployment model, see [this article](../install-mongodb.md).</span></span>

<span data-ttu-id="a5698-108">[MongoDB] [ MongoDB] is een populaire open-source, hoogwaardige NoSQL-database.</span><span class="sxs-lookup"><span data-stu-id="a5698-108">[MongoDB][MongoDB] is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="a5698-109">In dit artikel begeleidt u bij het maken van een Windows Server virtuele machine (VM) met Hallo [Azure-portal][AzurePortal].</span><span class="sxs-lookup"><span data-stu-id="a5698-109">This article guides you through creating a Windows Server virtual machine (VM) using hello [Azure portal][AzurePortal].</span></span> <span data-ttu-id="a5698-110">U maken en koppelen van een data schijf toohello VM voordat installeren en configureren van MongoDB.</span><span class="sxs-lookup"><span data-stu-id="a5698-110">You then create and attach a data disk toohello VM before installing and configuring MongoDB.</span></span> <span data-ttu-id="a5698-111">Als u een bestaande virtuele machine in Azure dat u toouse wilt hebt, kunt u gaan meteen te[installeren en configureren van MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="a5698-111">If you have an existing VM in Azure that you would like toouse, you can jump straight too[installing and configuring MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span></span>

## <a name="create-a-virtual-machine-running-windows-server"></a><span data-ttu-id="a5698-112">Een virtuele machine maken waarop Windows Server wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="a5698-112">Create a virtual machine running Windows Server</span></span>
<span data-ttu-id="a5698-113">Volg deze instructies toocreate een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="a5698-113">Follow these instructions toocreate a virtual machine.</span></span>

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> <span data-ttu-id="a5698-114">U kunt een eindpunt voor MongoDB toevoegen tijdens het Hallo virtuele machine maken en als volgt configureren: deze als de naam **Mongo**, gebruik **TCP** zoals Hallo-protocol en stel beide Hallo openbare en particuliere poort te**27017**.</span><span class="sxs-lookup"><span data-stu-id="a5698-114">You can add an endpoint for MongoDB while creating hello virtual machine, and configure it as follows: name it as **Mongo**, use **TCP** as hello protocol, and set both hello public and private ports too**27017**.</span></span>
>
>

## <a name="attach-a-data-disk"></a><span data-ttu-id="a5698-115">Een gegevensschijf koppelen</span><span class="sxs-lookup"><span data-stu-id="a5698-115">Attach a data disk</span></span>
<span data-ttu-id="a5698-116">tooprovide opslag voor Hallo virtuele machine, een gegevensschijf koppelen en initialiseren zodat Windows kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a5698-116">tooprovide storage for hello virtual machine, attach a data disk and then initialize it so that Windows can use it.</span></span> <span data-ttu-id="a5698-117">Als u een gegevensschijf al hebt, kunt u de bestaande schijf koppelen of kunt u een lege schijf koppelen.</span><span class="sxs-lookup"><span data-stu-id="a5698-117">If you already have a data disk, you can attach that existing disk, or you can attach an empty disk.</span></span>

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

<span data-ttu-id="a5698-118">Zie voor instructies voor het initialiseren van Hallo schijf, ' How to: initialiseren van een nieuwe gegevensschijf in WindowsServer "in [hoe tooattach data tooa virtuele Windows-machine schijf](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="a5698-118">For instructions on initializing hello disk, see "How to: Initialize a new data disk in Windows Server" in [How tooattach a data disk tooa Windows virtual machine](attach-disk.md).</span></span>

## <a name="install-and-run-mongodb-on-hello-virtual-machine"></a><span data-ttu-id="a5698-119">Installeren en uitvoeren van MongoDB op Hallo virtuele machine</span><span class="sxs-lookup"><span data-stu-id="a5698-119">Install and run MongoDB on hello virtual machine</span></span>
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a><span data-ttu-id="a5698-120">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="a5698-120">Summary</span></span>
<span data-ttu-id="a5698-121">In deze zelfstudie hebt u geleerd hoe toocreate een virtuele machine met Windows Server op afstand verbinding tooit en een gegevensschijf koppelen.</span><span class="sxs-lookup"><span data-stu-id="a5698-121">In this tutorial, you learned how toocreate a virtual machine running Windows Server, remotely connect tooit, and attach a data disk.</span></span>  <span data-ttu-id="a5698-122">U hebt ook geleerd hoe tooinstall en het configureren van MongoDB op Hallo Windows gebaseerde virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="a5698-122">You also learned how tooinstall and configure MongoDB on hello Windows-based virtual machine.</span></span> <span data-ttu-id="a5698-123">U kunt nu toegang tot MongoDB op Hallo Windows gebaseerde virtuele machine door na Hallo geavanceerde onderwerpen in Hallo [MongoDB-documentatie][MongoDocs].</span><span class="sxs-lookup"><span data-stu-id="a5698-123">You can now access MongoDB on hello Windows-based virtual machine, by following hello advanced topics in hello [MongoDB documentation][MongoDocs].</span></span>

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/

