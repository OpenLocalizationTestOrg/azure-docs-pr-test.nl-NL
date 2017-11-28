---
title: 'Azure Active Directory Domain Services: Aan de slag | Microsoft Docs'
description: Azure Active Directory Domain Services met behulp van hello Azure-portal (Preview) inschakelen
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 7695dabb11df8d9dcfdac24996edf021af2e7f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="df1e3-103">Azure Active Directory Domain Services met behulp van hello Azure-portal (Preview) inschakelen</span><span class="sxs-lookup"><span data-stu-id="df1e3-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="df1e3-104">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="df1e3-104">Before you begin</span></span>
<span data-ttu-id="df1e3-105">Raadpleeg te[netwerken overwegingen voor Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="df1e3-105">Refer too[Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>


## <a name="task-2-configure-network-settings"></a><span data-ttu-id="df1e3-106">Taak 2: netwerkinstellingen configureren</span><span class="sxs-lookup"><span data-stu-id="df1e3-106">Task 2: configure network settings</span></span>
<span data-ttu-id="df1e3-107">de volgende configuratietaak Hallo toocreate is een Azure-netwerk en een specifieke subnet in het.</span><span class="sxs-lookup"><span data-stu-id="df1e3-107">hello next configuration task is toocreate an Azure virtual network and a dedicated subnet within it.</span></span> <span data-ttu-id="df1e3-108">U schakelt Azure Active Directory Domain Services in dit subnet binnen uw virtuele netwerk in.</span><span class="sxs-lookup"><span data-stu-id="df1e3-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="df1e3-109">U kunt ook kiezen een bestaand virtueel netwerk en subnet binnen het Hallo-specifieke maken.</span><span class="sxs-lookup"><span data-stu-id="df1e3-109">You may also pick an existing virtual network and create hello dedicated subnet within it.</span></span>

1. <span data-ttu-id="df1e3-110">Klik op **virtueel netwerk** tooselect een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="df1e3-110">Click **Virtual network** tooselect a virtual network.</span></span>
2. <span data-ttu-id="df1e3-111">Op Hallo **virtueel netwerk kiezen** blade ziet u alle bestaande virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="df1e3-111">On hello **Choose virtual network** blade, you see all existing virtual networks.</span></span> <span data-ttu-id="df1e3-112">U ziet alleen Hallo virtuele netwerken die deel uitmaken van de resourcegroep toohello en Azure-locatie die u hebt geselecteerd op Hallo **basisbeginselen** wizardpagina.</span><span class="sxs-lookup"><span data-stu-id="df1e3-112">You see only hello virtual networks that belong toohello resource group and Azure location you have selected on hello **Basics** wizard page.</span></span>

3. <span data-ttu-id="df1e3-113">Kies Hallo virtuele netwerk waarin Azure AD Domain Services moeten worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="df1e3-113">Choose hello virtual network in which Azure AD Domain Services should be enabled.</span></span> <span data-ttu-id="df1e3-114">Klik op **nieuw**, als u liever toocreate een nieuw virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="df1e3-114">Click **Create new**, if you prefer toocreate a new virtual network.</span></span> <span data-ttu-id="df1e3-115">We raden met behulp van een toegewezen subnet voor Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="df1e3-115">We highly recommend using a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="df1e3-116">Als u een bestaand virtueel netwerk kiezen [Maak een toegewezen subnet met Hallo virtuele netwerken extensie](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) en selecteer vervolgens dat subnet.</span><span class="sxs-lookup"><span data-stu-id="df1e3-116">If you pick an existing virtual network, [create a dedicated subnet using hello virtual networks extension](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) and then pick that subnet.</span></span> 

    ![Virtueel netwerk kiezen](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. <span data-ttu-id="df1e3-118">Klik op **Subnet** toopick Hallo specifieke subnet in dit virtuele netwerk, in welke tooenable uw nieuwe beheerd domein.</span><span class="sxs-lookup"><span data-stu-id="df1e3-118">Click **Subnet** toopick hello dedicated subnet in this virtual network, within which tooenable your new managed domain.</span></span> <span data-ttu-id="df1e3-119">In Hallo **subnet maken** blade Geef een naam voor het Hallo-subnet en klik op **OK** wanneer u klaar bent.</span><span class="sxs-lookup"><span data-stu-id="df1e3-119">In hello **Create subnet** blade, specify a name for hello subnet, and click **OK** when you're done.</span></span> <span data-ttu-id="df1e3-120">Bijvoorbeeld, een subnet maken met de naam van de Hallo DomainServices, zodat u gemakkelijk voor andere beheerders toounderstand wat binnen Hallo subnet is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="df1e3-120">For example, create a subnet with hello name 'DomainServices', making it easy for other administrators toounderstand what is deployed within hello subnet.</span></span>

    ![Subnet binnen Hallo virtueel netwerk kiezen](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > <span data-ttu-id="df1e3-122">**Richtlijnen voor het selecteren van een subnet**</span><span class="sxs-lookup"><span data-stu-id="df1e3-122">**Guidelines for selecting a subnet**</span></span>
  > 1. <span data-ttu-id="df1e3-123">Gebruik een toegewezen subnet voor Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="df1e3-123">Use a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="df1e3-124">Implementeer geen eventuele andere virtuele machines toothis-subnet.</span><span class="sxs-lookup"><span data-stu-id="df1e3-124">Do not deploy any other virtual machines toothis subnet.</span></span> <span data-ttu-id="df1e3-125">Deze configuratie kunt u tooconfigure netwerkbeveiligingsgroepen (nsg's) voor uw werkbelastingen/virtuele machines zonder te verstoren uw beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="df1e3-125">This configuration enables you tooconfigure network security groups (NSGs) for your workloads/virtual machines without disrupting your managed domain.</span></span> <span data-ttu-id="df1e3-126">Zie voor meer informatie [networking overwegingen voor Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="df1e3-126">For details, see [networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>
  2. <span data-ttu-id="df1e3-127">Selecteer Hallo gatewaysubnet voor het implementeren van Azure AD Domain Services niet omdat het is niet een ondersteunde configuratie.</span><span class="sxs-lookup"><span data-stu-id="df1e3-127">Do not select hello Gateway subnet for deploying Azure AD Domain Services, because it is not a supported configuration.</span></span>
  3. <span data-ttu-id="df1e3-128">Zorg ervoor dat u hebt geselecteerd Hallo-subnet heeft voldoende beschikbare-adresruimte - ten minste 3-5 beschikbare IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="df1e3-128">Ensure that hello subnet you've selected has sufficient available address space - at least 3-5 available IP addresses.</span></span>
  >

5. <span data-ttu-id="df1e3-129">Wanneer u klaar bent, klikt u op **OK** toomove op toohello **beheerdersgroep** pagina van wizard Hallo.</span><span class="sxs-lookup"><span data-stu-id="df1e3-129">When you are done, click **OK** toomove on toohello **Administrator group** page of hello wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="df1e3-130">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="df1e3-130">Next step</span></span>
[<span data-ttu-id="df1e3-131">Taak 3: Configureer beheergroep en Azure AD Domain Services inschakelen</span><span class="sxs-lookup"><span data-stu-id="df1e3-131">Task 3: configure administrative group and enable Azure AD Domain Services</span></span>](active-directory-ds-getting-started-admingroup.md)
