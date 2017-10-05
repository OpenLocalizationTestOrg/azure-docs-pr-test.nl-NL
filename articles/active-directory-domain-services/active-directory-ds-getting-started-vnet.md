---
title: 'Azure Active Directory Domain Services: een virtueel netwerk maken of selecteren | Microsoft Docs'
description: Azure Active Directory Domain Services inschakelen met behulp van de klassieke Azure-portal
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 13ab1608-e3d8-40de-9f7b-9b5b42199af4
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 457519b00b65b0157effe2d4aba033a1c99852e8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a><span data-ttu-id="2cb4f-103">Een virtueel netwerk voor Azure Active Directory Domain Services maken of selecteren</span><span class="sxs-lookup"><span data-stu-id="2cb4f-103">Create or select a virtual network for Azure Active Directory Domain Services</span></span>
## <a name="before-you-begin"></a><span data-ttu-id="2cb4f-104">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="2cb4f-104">Before you begin</span></span>
<span data-ttu-id="2cb4f-105">Raadpleeg [Networking considerations for Azure AD Domain Services](active-directory-ds-networking.md) (Overwegingen voor netwerken voor Azure AD Domain Services).</span><span class="sxs-lookup"><span data-stu-id="2cb4f-105">Refer to [Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>

## <a name="task-2-create-an-azure-virtual-network"></a><span data-ttu-id="2cb4f-106">Taak 2: een virtueel netwerk van Azure maken</span><span class="sxs-lookup"><span data-stu-id="2cb4f-106">Task 2: Create an Azure virtual network</span></span>
<span data-ttu-id="2cb4f-107">De volgende configuratietaak bestaat uit het maken van een virtueel Azure-netwerk met daarbinnen een subnet.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-107">The next configuration task is to create an Azure virtual network and a subnet within it.</span></span> <span data-ttu-id="2cb4f-108">U schakelt Azure Active Directory Domain Services in dit subnet binnen uw virtuele netwerk in.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="2cb4f-109">Als u een bestaand virtueel netwerk hebt dat u wilt gebruiken, kunt u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-109">If you have an existing virtual network that you’d prefer to use, you can skip this step.</span></span>

> [!NOTE]
> <span data-ttu-id="2cb4f-110">Controleer of het virtuele netwerk van Azure dat u maakt of wilt gebruiken met Azure Active Directory Domain Services, deel uitmaakt van een Azure-regio die wordt ondersteund door Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-110">Make sure that the Azure virtual network you create or choose to use with Azure Active Directory Domain Services belongs to an Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="2cb4f-111">Zie de pagina [Azure-services per regio](https://azure.microsoft.com/regions/#services/) om te bekijken in welke Azure-regio's Azure Active Directory Domain Services beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-111">To ascertain the Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
>
><span data-ttu-id="2cb4f-112">Noteer de naam van het virtuele netwerk, zodat u het juiste virtuele netwerk selecteert wanneer u Azure Active Directory Domain Services inschakelt in een volgende configuratiestap.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-112">Note the name of the virtual network to ensure that you select the right virtual network when you enable Azure Active Directory Domain Services in a subsequent configuration step.</span></span>


<span data-ttu-id="2cb4f-113">Volg deze configuratie-instructies als u een virtueel Azure-netwerk wilt maken waarin Azure Active Directory Domain Services moet zijn ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="2cb4f-113">To create an Azure virtual network in which you want to enable Azure Active Directory Domain Services, follow these configuration instructions:</span></span>

1. <span data-ttu-id="2cb4f-114">Ga naar de [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="2cb4f-114">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="2cb4f-115">Selecteer **Netwerken** in het linkerdeelvenster.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-115">In the left pane, select **Networks**.</span></span>

    <span data-ttu-id="2cb4f-116">![Knooppunt Netwerken](./media/active-directory-domain-services-getting-started/networks-node.png)</span><span class="sxs-lookup"><span data-stu-id="2cb4f-116">![Networks node](./media/active-directory-domain-services-getting-started/networks-node.png)</span></span>  
    <span data-ttu-id="2cb4f-117">Het venster **Virtuele netwerken** wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-117">The **Virtual Networks** window opens.</span></span>
3. <span data-ttu-id="2cb4f-118">Klik op **Nieuw** in het taakvenster onder in het venster.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-118">In the task pane at the bottom of the window, click **New**.</span></span>

    ![Venster Virtuele netwerken](./media/active-directory-domain-services-getting-started/virtual-networks.png)
4. <span data-ttu-id="2cb4f-120">Klik op **Netwerkservices** en selecteer **Virtueel netwerk**.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-120">Click **Network Services**, and then select **Virtual Network**.</span></span>

    ![Virtueel netwerk - Snel maken](./media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. <span data-ttu-id="2cb4f-122">Klik op **Snel maken** om een virtueel netwerk te maken.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-122">To create a virtual network, click **Quick Create**.</span></span>

6. <span data-ttu-id="2cb4f-123">Geef een **Naam** op voor het virtuele netwerk en stel desgewenst het volgende in:</span><span class="sxs-lookup"><span data-stu-id="2cb4f-123">Specify a **Name** for your virtual network, and consider doing the following:</span></span>
    * <span data-ttu-id="2cb4f-124">U kunt ervoor kiezen om **Adresruimte** of **Maximum aantal VM’s** op te geven voor dit netwerk.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-124">You can choose to configure **Address space** or **Maximum VM count** for this network.</span></span>
    * <span data-ttu-id="2cb4f-125">U kunt de instelling van **DNS-server** voorlopig op **Geen** laten staan.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-125">You can leave the **DNS server** setting as **None** for now.</span></span> <span data-ttu-id="2cb4f-126">U kunt de instelling bijwerken nadat u Azure Active Directory Domain Services hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-126">You can update the setting after you enable Azure Active Directory Domain Services.</span></span>
7. <span data-ttu-id="2cb4f-127">Selecteer een ondersteunde Azure-regio selecteert in de vervolgkeuzelijst **Locatie**.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-127">In the **Location** drop-down list, select a supported Azure region.</span></span>  
    <span data-ttu-id="2cb4f-128">Zie de pagina [Azure-services per regio](https://azure.microsoft.com/regions/#services/) om te bekijken in welke Azure-regio's Azure Active Directory Domain Services beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-128">To ascertain the Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
8. <span data-ttu-id="2cb4f-129">Klik op **Een virtueel netwerk maken** om het virtuele netwerk te maken.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-129">To create your virtual network, click **Create a Virtual Network**.</span></span>

    ![Een virtueel netwerk voor Azure Active Directory Domain Services maken](./media/active-directory-domain-services-getting-started/create-vnet.png)
9. <span data-ttu-id="2cb4f-131">Nadat u het virtuele netwerk hebt gemaakt, selecteert u dit virtuele netwerk en klikt u op het tabblad **Configureren**.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-131">After you've created a virtual network, select the name of the virtual network, and then click the **Configure** tab.</span></span>

    ![Een subnet maken](./media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. <span data-ttu-id="2cb4f-133">Klik onder **Virtual Network-adresruimten** op **Subnet toevoegen** en geef een subnet op met de naam **AaddsSubnet**.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-133">Under **virtual network address spaces**, click **add subnet**, and then specify a subnet with the name **AaddsSubnet**.</span></span>

    ![Een subnet voor Azure Active Directory Domain Services maken](./media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. <span data-ttu-id="2cb4f-135">Klik op **Opslaan** om het subnet te maken.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-135">To create the subnet, click **Save**.</span></span>


## <a name="next-step"></a><span data-ttu-id="2cb4f-136">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="2cb4f-136">Next step</span></span>
[<span data-ttu-id="2cb4f-137">Taak 3: Azure Active Directory Domain Services inschakelen</span><span class="sxs-lookup"><span data-stu-id="2cb4f-137">Task 3: enable Azure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-enableaadds.md)
