---
title: 'Azure Active Directory Domain Services: een virtueel netwerk maken of selecteren | Microsoft Docs'
description: Azure Active Directory Domain Services met behulp van de klassieke Azure-portal Hallo inschakelen
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
ms.openlocfilehash: 212c741b20e846742d94f70342c4263ce8984153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a><span data-ttu-id="649d5-103">Een virtueel netwerk voor Azure Active Directory Domain Services maken of selecteren</span><span class="sxs-lookup"><span data-stu-id="649d5-103">Create or select a virtual network for Azure Active Directory Domain Services</span></span>
## <a name="before-you-begin"></a><span data-ttu-id="649d5-104">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="649d5-104">Before you begin</span></span>
<span data-ttu-id="649d5-105">Raadpleeg te[netwerken overwegingen voor Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="649d5-105">Refer too[Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>

## <a name="task-2-create-an-azure-virtual-network"></a><span data-ttu-id="649d5-106">Taak 2: een virtueel netwerk van Azure maken</span><span class="sxs-lookup"><span data-stu-id="649d5-106">Task 2: Create an Azure virtual network</span></span>
<span data-ttu-id="649d5-107">de volgende configuratietaak Hallo toocreate is een Azure-netwerk en een subnet binnen het.</span><span class="sxs-lookup"><span data-stu-id="649d5-107">hello next configuration task is toocreate an Azure virtual network and a subnet within it.</span></span> <span data-ttu-id="649d5-108">U schakelt Azure Active Directory Domain Services in dit subnet binnen uw virtuele netwerk in.</span><span class="sxs-lookup"><span data-stu-id="649d5-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="649d5-109">Als u een bestaand virtueel netwerk dat u liever toouse hebt, kunt u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="649d5-109">If you have an existing virtual network that you’d prefer toouse, you can skip this step.</span></span>

> [!NOTE]
> <span data-ttu-id="649d5-110">Zorg ervoor dat Hallo virtuele Azure-netwerk u maakt of kies toouse met Azure Active Directory Domain Services behoort tooan Azure-regio die wordt ondersteund door Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="649d5-110">Make sure that hello Azure virtual network you create or choose toouse with Azure Active Directory Domain Services belongs tooan Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="649d5-111">tooascertain Hallo Azure-regio's waarin Azure Active Directory Domain Services beschikbaar is, Zie [Azure-services per regio](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="649d5-111">tooascertain hello Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
>
><span data-ttu-id="649d5-112">Noteer de naam Hallo van Hallo virtueel netwerk tooensure dat u de juiste virtuele netwerk Hallo selecteert wanneer u Azure Active Directory Domain Services in een volgende configuratiestap inschakelen.</span><span class="sxs-lookup"><span data-stu-id="649d5-112">Note hello name of hello virtual network tooensure that you select hello right virtual network when you enable Azure Active Directory Domain Services in a subsequent configuration step.</span></span>


<span data-ttu-id="649d5-113">toocreate een Azure-netwerk waarin u wilt dat tooenable Azure Active Directory Domain Services, volgt u deze configuratie-instructies:</span><span class="sxs-lookup"><span data-stu-id="649d5-113">toocreate an Azure virtual network in which you want tooenable Azure Active Directory Domain Services, follow these configuration instructions:</span></span>

1. <span data-ttu-id="649d5-114">Ga toohello [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="649d5-114">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="649d5-115">Selecteer in het linkerdeelvenster Hallo **netwerken**.</span><span class="sxs-lookup"><span data-stu-id="649d5-115">In hello left pane, select **Networks**.</span></span>

    <span data-ttu-id="649d5-116">![Knooppunt Netwerken](./media/active-directory-domain-services-getting-started/networks-node.png)</span><span class="sxs-lookup"><span data-stu-id="649d5-116">![Networks node](./media/active-directory-domain-services-getting-started/networks-node.png)</span></span>  
    <span data-ttu-id="649d5-117">Hallo **virtuele netwerken** venster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="649d5-117">hello **Virtual Networks** window opens.</span></span>
3. <span data-ttu-id="649d5-118">Klik in het taakvenster Hallo HALLO hallo venster onderaan in op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="649d5-118">In hello task pane at hello bottom of hello window, click **New**.</span></span>

    ![Venster Virtuele netwerken](./media/active-directory-domain-services-getting-started/virtual-networks.png)
4. <span data-ttu-id="649d5-120">Klik op **Netwerkservices** en selecteer **Virtueel netwerk**.</span><span class="sxs-lookup"><span data-stu-id="649d5-120">Click **Network Services**, and then select **Virtual Network**.</span></span>

    ![Virtueel netwerk - Snel maken](./media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. <span data-ttu-id="649d5-122">toocreate een virtueel netwerk, klikt u op **snelle invoer**.</span><span class="sxs-lookup"><span data-stu-id="649d5-122">toocreate a virtual network, click **Quick Create**.</span></span>

6. <span data-ttu-id="649d5-123">Geef een **naam** voor uw virtuele netwerk en overweeg Hallo volgende manier:</span><span class="sxs-lookup"><span data-stu-id="649d5-123">Specify a **Name** for your virtual network, and consider doing hello following:</span></span>
    * <span data-ttu-id="649d5-124">U kunt tooconfigure **adresruimte** of **Maximum aantal VM's** voor dit netwerk.</span><span class="sxs-lookup"><span data-stu-id="649d5-124">You can choose tooconfigure **Address space** or **Maximum VM count** for this network.</span></span>
    * <span data-ttu-id="649d5-125">U kunt laten Hallo **DNS-server** instellen als de **geen** nu.</span><span class="sxs-lookup"><span data-stu-id="649d5-125">You can leave hello **DNS server** setting as **None** for now.</span></span> <span data-ttu-id="649d5-126">Nadat u Azure Active Directory Domain Services hebt ingeschakeld, kunt u de instelling Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="649d5-126">You can update hello setting after you enable Azure Active Directory Domain Services.</span></span>
7. <span data-ttu-id="649d5-127">In Hallo **locatie** vervolgkeuzelijst, selecteert u een ondersteunde Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="649d5-127">In hello **Location** drop-down list, select a supported Azure region.</span></span>  
    <span data-ttu-id="649d5-128">tooascertain Hallo Azure-regio's waarin Azure Active Directory Domain Services beschikbaar is, Zie [Azure-services per regio](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="649d5-128">tooascertain hello Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
8. <span data-ttu-id="649d5-129">toocreate uw virtuele netwerk, klikt u op **een virtueel netwerk maken**.</span><span class="sxs-lookup"><span data-stu-id="649d5-129">toocreate your virtual network, click **Create a Virtual Network**.</span></span>

    ![Een virtueel netwerk voor Azure Active Directory Domain Services maken](./media/active-directory-domain-services-getting-started/create-vnet.png)
9. <span data-ttu-id="649d5-131">Nadat u een virtueel netwerk hebt gemaakt, selecteert u de naam van het virtuele netwerk Hallo Hallo en klik vervolgens op Hallo **configureren** tabblad.</span><span class="sxs-lookup"><span data-stu-id="649d5-131">After you've created a virtual network, select hello name of hello virtual network, and then click hello **Configure** tab.</span></span>

    ![Een subnet maken](./media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. <span data-ttu-id="649d5-133">Onder **adresruimten voor virtueel netwerk**, klikt u op **subnet toevoegen**, en geef vervolgens een subnet met de naam van de Hallo **AaddsSubnet**.</span><span class="sxs-lookup"><span data-stu-id="649d5-133">Under **virtual network address spaces**, click **add subnet**, and then specify a subnet with hello name **AaddsSubnet**.</span></span>

    ![Een subnet voor Azure Active Directory Domain Services maken](./media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. <span data-ttu-id="649d5-135">toocreate Hallo subnet, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="649d5-135">toocreate hello subnet, click **Save**.</span></span>


## <a name="next-step"></a><span data-ttu-id="649d5-136">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="649d5-136">Next step</span></span>
[<span data-ttu-id="649d5-137">Taak 3: Azure Active Directory Domain Services inschakelen</span><span class="sxs-lookup"><span data-stu-id="649d5-137">Task 3: enable Azure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-enableaadds.md)
