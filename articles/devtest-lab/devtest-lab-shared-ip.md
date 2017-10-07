---
title: aaaUnderstand gedeelde IP-adressen in Azure DevTest Labs | Microsoft Docs
description: Meer informatie over hoe Azure DevTest Labs gebruikmaakt van gedeelde IP-adressen toominimize Hallo openbare IP-adressen vereist tooaccess uw lab virtuele machines.
services: devtest-lab
documentationcenter: na
author: camsoper
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: casoper
ms.openlocfilehash: 8756410117a9d550d567d372174bf1ea96703c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a><span data-ttu-id="be7d1-103">Gedeelde IP-adressen in Azure DevTest Labs begrijpen</span><span class="sxs-lookup"><span data-stu-id="be7d1-103">Understand shared IP addresses in Azure DevTest Labs</span></span>

<span data-ttu-id="be7d1-104">Azure DevTest Labs kunt lab VMs share Hallo hetzelfde openbare IP-adres toominimize Hallo aantal openbare IP-adressen vereist tooaccess uw afzonderlijke lab virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="be7d1-104">Azure DevTest Labs lets lab VMs share hello same public IP address toominimize hello number of public IP addresses required tooaccess your individual lab VMs.</span></span>  <span data-ttu-id="be7d1-105">Dit artikel wordt beschreven hoe gedeelde IP-adressen werk en hun bijbehorende configuratie-opties.</span><span class="sxs-lookup"><span data-stu-id="be7d1-105">This article describes how shared IPs work and their related configuration options.</span></span>

## <a name="shared-ip-setting"></a><span data-ttu-id="be7d1-106">Gedeelde IP-instelling</span><span class="sxs-lookup"><span data-stu-id="be7d1-106">Shared IP setting</span></span>

<span data-ttu-id="be7d1-107">Wanneer u een testomgeving maakt, bevindt het zich in een subnet van een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="be7d1-107">When you create a lab, it resides in a subnet of a virtual network.</span></span>  <span data-ttu-id="be7d1-108">Dit subnet is standaard gemaakt met **Schakel gedeelde openbare IP-adres** instellen te*Ja*.</span><span class="sxs-lookup"><span data-stu-id="be7d1-108">By default, this subnet is created with **Enable shared public IP** set too*Yes*.</span></span>  <span data-ttu-id="be7d1-109">Deze configuratie maakt een openbaar IP-adres voor het hele subnet Hallo.</span><span class="sxs-lookup"><span data-stu-id="be7d1-109">This configuration creates one public IP address for hello entire subnet.</span></span>  <span data-ttu-id="be7d1-110">Zie voor meer informatie over het configureren van virtuele netwerken en subnetten [configureren van een virtueel netwerk in Azure DevTest Labs](devtest-lab-configure-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="be7d1-110">For more information about configuring virtual networks and subnets, see [Configure a virtual network in Azure DevTest Labs](devtest-lab-configure-vnet.md).</span></span>

![Nieuw lab-subnet](media/devtest-lab-shared-ip/lab-subnet.png)

<span data-ttu-id="be7d1-112">Voor bestaande labs, kunt u deze optie inschakelen door het selecteren van **configuratie en het beleid > virtuele netwerken**.</span><span class="sxs-lookup"><span data-stu-id="be7d1-112">For existing labs, you can enable this option by selecting **Configuration and policies > Virtual Networks**.</span></span> <span data-ttu-id="be7d1-113">Vervolgens selecteert u een virtueel netwerk in Hallo lijst en kies **inschakelen gedeelde openbare IP-adres** voor een geselecteerde subnet.</span><span class="sxs-lookup"><span data-stu-id="be7d1-113">Then, select a virtual network from hello list and choose **ENABLE SHARED PUBLIC IP** for a selected subnet.</span></span> <span data-ttu-id="be7d1-114">U kunt deze optie in een testomgeving ook uitschakelen als u niet dat tooshare een openbaar IP-adres in het lab virtuele machines wilt.</span><span class="sxs-lookup"><span data-stu-id="be7d1-114">You can also disable this option in any lab if you don't want tooshare a public IP address across lab VMs.</span></span>

<span data-ttu-id="be7d1-115">Alle virtuele machines in dit lab standaard toousing gemaakt van een gedeelde IP-adres.</span><span class="sxs-lookup"><span data-stu-id="be7d1-115">Any VMs created in this lab default toousing a shared IP.</span></span>  <span data-ttu-id="be7d1-116">Bij het maken van VM hello, deze instelling kan worden waargenomen in Hallo **geavanceerde instellingen** blade onder **IP-adresconfiguratie**.</span><span class="sxs-lookup"><span data-stu-id="be7d1-116">When creating hello VM, this setting can be observed in hello **Advanced settings** blade under **IP address configuration**.</span></span>

![Nieuwe virtuele machine](media/devtest-lab-shared-ip/new-vm.png)

- <span data-ttu-id="be7d1-118">**Gedeelde:** alle virtuele machines die zijn gemaakt als **gedeelde** in één resourcegroep (RG) worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="be7d1-118">**Shared:** All VMs created as **Shared** are placed into one resource group (RG).</span></span> <span data-ttu-id="be7d1-119">Een enkel IP-adres is toegewezen voor die RG en alle virtuele machines in Hallo RG dat IP-adres wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="be7d1-119">A single IP address is assigned for that RG and all VMs in hello RG will use that IP address.</span></span>
- <span data-ttu-id="be7d1-120">**Openbaar:** elke VM die u maakt een eigen IP-adres heeft en in een eigen resourcegroep wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="be7d1-120">**Public:** Every VM you create has its own IP address and is created in its own resource group.</span></span>
- <span data-ttu-id="be7d1-121">**Persoonlijk:** elke VM die u maakt een particuliere IP-adres gebruikt.</span><span class="sxs-lookup"><span data-stu-id="be7d1-121">**Private:** Every VM you create uses a private IP address.</span></span> <span data-ttu-id="be7d1-122">U zich niet kunnen tooconnect toothis VM rechtstreeks vanuit Hallo internet met extern bureaublad.</span><span class="sxs-lookup"><span data-stu-id="be7d1-122">You will not be able tooconnect toothis VM directly from hello internet with Remote Desktop.</span></span>

<span data-ttu-id="be7d1-123">Wanneer een virtuele machine met gedeelde IP ingeschakeld wordt toegevoegd toohello subnet, DevTest Labs automatisch voegt van Hallo VM tooa load balancer toe en wijst een TCP-poortnummer op Hallo openbare IP-adres, doorsturen toohello RDP-poort op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="be7d1-123">Whenever a VM with shared IP enabled is added toohello subnet, DevTest Labs automatically adds hello VM tooa load balancer and assigns a TCP port number on hello public IP address, forwarding toohello RDP port on hello VM.</span></span>  

## <a name="using-hello-shared-ip"></a><span data-ttu-id="be7d1-124">Met behulp van Hallo gedeeld IP</span><span class="sxs-lookup"><span data-stu-id="be7d1-124">Using hello shared IP</span></span>

- <span data-ttu-id="be7d1-125">**Linux-gebruikers:** SSH toohello VM via Hallo IP-adres of FQDN-naam, gevolgd door een dubbelepunt, gevolgd door Hallo-poort.</span><span class="sxs-lookup"><span data-stu-id="be7d1-125">**Linux users:** SSH toohello VM by using hello IP address or fully qualified domain name, followed by a colon, followed by hello port.</span></span> <span data-ttu-id="be7d1-126">In onderstaande Hallo afbeelding, bijvoorbeeld adres Hallo RDP tooconnect toohello VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span><span class="sxs-lookup"><span data-stu-id="be7d1-126">For example, in hello image below, hello RDP address tooconnect toohello VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span></span>

  ![Voorbeeld van de virtuele machine](media/devtest-lab-shared-ip/vm-info.png)

- <span data-ttu-id="be7d1-128">**Windows-gebruikers:** Selecteer Hallo **Connect** in Azure portal toodownload Hallo vooraf geconfigureerde RDP-bestand en toegang tot Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="be7d1-128">**Windows users:** Select hello **Connect** button on hello Azure portal toodownload a pre-configured RDP file and access hello VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be7d1-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="be7d1-129">Next steps</span></span>

* [<span data-ttu-id="be7d1-130">Labbeleidsregels definiëren in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="be7d1-130">Define lab policies in Azure DevTest Labs</span></span>](devtest-lab-set-lab-policy.md)
* [<span data-ttu-id="be7d1-131">Een virtueel netwerk configureren in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="be7d1-131">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md)





