---
title: Inzicht in gedeelde IP-adressen in Azure DevTest Labs | Microsoft Docs
description: Meer informatie over hoe Azure DevTest Labs gedeelde IP-adressen gebruikt om te beperken van het openbare IP-adressen vereist voor toegang tot uw lab virtuele machines.
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
ms.openlocfilehash: 9f6e1980bf5ea5b41da98a135d89f1c5159921a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a><span data-ttu-id="49591-103">Gedeelde IP-adressen in Azure DevTest Labs begrijpen</span><span class="sxs-lookup"><span data-stu-id="49591-103">Understand shared IP addresses in Azure DevTest Labs</span></span>

<span data-ttu-id="49591-104">Azure DevTest Labs kunt lab VMs delen hetzelfde openbare IP-adres om te beperken het aantal openbare IP-adressen die zijn vereist voor toegang tot uw afzonderlijke lab virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="49591-104">Azure DevTest Labs lets lab VMs share the same public IP address to minimize the number of public IP addresses required to access your individual lab VMs.</span></span>  <span data-ttu-id="49591-105">Dit artikel wordt beschreven hoe gedeelde IP-adressen werk en hun bijbehorende configuratie-opties.</span><span class="sxs-lookup"><span data-stu-id="49591-105">This article describes how shared IPs work and their related configuration options.</span></span>

## <a name="shared-ip-setting"></a><span data-ttu-id="49591-106">Gedeelde IP-instelling</span><span class="sxs-lookup"><span data-stu-id="49591-106">Shared IP setting</span></span>

<span data-ttu-id="49591-107">Wanneer u een testomgeving maakt, bevindt het zich in een subnet van een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="49591-107">When you create a lab, it resides in a subnet of a virtual network.</span></span>  <span data-ttu-id="49591-108">Dit subnet is standaard gemaakt met **Schakel gedeelde openbare IP-adres** ingesteld op *Ja*.</span><span class="sxs-lookup"><span data-stu-id="49591-108">By default, this subnet is created with **Enable shared public IP** set to *Yes*.</span></span>  <span data-ttu-id="49591-109">Deze configuratie maakt een openbaar IP-adres voor het hele subnet.</span><span class="sxs-lookup"><span data-stu-id="49591-109">This configuration creates one public IP address for the entire subnet.</span></span>  <span data-ttu-id="49591-110">Zie voor meer informatie over het configureren van virtuele netwerken en subnetten [configureren van een virtueel netwerk in Azure DevTest Labs](devtest-lab-configure-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="49591-110">For more information about configuring virtual networks and subnets, see [Configure a virtual network in Azure DevTest Labs](devtest-lab-configure-vnet.md).</span></span>

![Nieuw lab-subnet](media/devtest-lab-shared-ip/lab-subnet.png)

<span data-ttu-id="49591-112">Voor bestaande labs, kunt u deze optie inschakelen door het selecteren van **configuratie en het beleid > virtuele netwerken**.</span><span class="sxs-lookup"><span data-stu-id="49591-112">For existing labs, you can enable this option by selecting **Configuration and policies > Virtual Networks**.</span></span> <span data-ttu-id="49591-113">Vervolgens selecteert u een virtueel netwerk in de lijst en kies **inschakelen gedeelde openbare IP-adres** voor een geselecteerde subnet.</span><span class="sxs-lookup"><span data-stu-id="49591-113">Then, select a virtual network from the list and choose **ENABLE SHARED PUBLIC IP** for a selected subnet.</span></span> <span data-ttu-id="49591-114">U kunt deze optie in een testomgeving ook uitschakelen als u niet wilt delen van een openbaar IP-adres in het lab virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="49591-114">You can also disable this option in any lab if you don't want to share a public IP address across lab VMs.</span></span>

<span data-ttu-id="49591-115">Alle virtuele machines in dit lab standaard voor het gebruik van een gedeelde IP-adres hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="49591-115">Any VMs created in this lab default to using a shared IP.</span></span>  <span data-ttu-id="49591-116">Bij het maken van de virtuele machine met deze instelling kan worden waargenomen de **geavanceerde instellingen** blade onder **IP-adresconfiguratie**.</span><span class="sxs-lookup"><span data-stu-id="49591-116">When creating the VM, this setting can be observed in the **Advanced settings** blade under **IP address configuration**.</span></span>

![Nieuwe virtuele machine](media/devtest-lab-shared-ip/new-vm.png)

- <span data-ttu-id="49591-118">**Gedeelde:** alle virtuele machines die zijn gemaakt als **gedeelde** in één resourcegroep (RG) worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="49591-118">**Shared:** All VMs created as **Shared** are placed into one resource group (RG).</span></span> <span data-ttu-id="49591-119">Een enkel IP-adres is toegewezen voor die RG en alle virtuele machines in de RG dat IP-adres wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="49591-119">A single IP address is assigned for that RG and all VMs in the RG will use that IP address.</span></span>
- <span data-ttu-id="49591-120">**Openbaar:** elke VM die u maakt een eigen IP-adres heeft en in een eigen resourcegroep wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="49591-120">**Public:** Every VM you create has its own IP address and is created in its own resource group.</span></span>
- <span data-ttu-id="49591-121">**Persoonlijk:** elke VM die u maakt een particuliere IP-adres gebruikt.</span><span class="sxs-lookup"><span data-stu-id="49591-121">**Private:** Every VM you create uses a private IP address.</span></span> <span data-ttu-id="49591-122">Niet mogelijk rechtstreeks vanaf het internet met extern bureaublad verbinding maken met deze virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="49591-122">You will not be able to connect to this VM directly from the internet with Remote Desktop.</span></span>

<span data-ttu-id="49591-123">Wanneer een virtuele machine met gedeelde IP ingeschakeld wordt toegevoegd aan het subnet, DevTest Labs automatisch voegt van de virtuele machine aan een load balancer toe en wijst een TCP-poortnummer op het openbare IP-adres, worden doorgestuurd naar de RDP-poort op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="49591-123">Whenever a VM with shared IP enabled is added to the subnet, DevTest Labs automatically adds the VM to a load balancer and assigns a TCP port number on the public IP address, forwarding to the RDP port on the VM.</span></span>  

## <a name="using-the-shared-ip"></a><span data-ttu-id="49591-124">Met behulp van het gedeelde IP-adres</span><span class="sxs-lookup"><span data-stu-id="49591-124">Using the shared IP</span></span>

- <span data-ttu-id="49591-125">**Linux-gebruikers:** SSH naar de virtuele machine met behulp van de IP-adres of FQDN-naam, gevolgd door een dubbelepunt, gevolgd door de poort.</span><span class="sxs-lookup"><span data-stu-id="49591-125">**Linux users:** SSH to the VM by using the IP address or fully qualified domain name, followed by a colon, followed by the port.</span></span> <span data-ttu-id="49591-126">In de onderstaande afbeelding de RDP-adres voor de verbinding met de virtuele machine is bijvoorbeeld `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span><span class="sxs-lookup"><span data-stu-id="49591-126">For example, in the image below, the RDP address to connect to the VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span></span>

  ![Voorbeeld van de virtuele machine](media/devtest-lab-shared-ip/vm-info.png)

- <span data-ttu-id="49591-128">**Windows-gebruikers:** selecteert u de **Connect** knop op de Azure-portal voor het downloaden van een vooraf geconfigureerde RDP-bestand en toegang tot de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="49591-128">**Windows users:** Select the **Connect** button on the Azure portal to download a pre-configured RDP file and access the VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49591-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="49591-129">Next steps</span></span>

* [<span data-ttu-id="49591-130">Labbeleidsregels definiëren in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="49591-130">Define lab policies in Azure DevTest Labs</span></span>](devtest-lab-set-lab-policy.md)
* [<span data-ttu-id="49591-131">Een virtueel netwerk configureren in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="49591-131">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md)





