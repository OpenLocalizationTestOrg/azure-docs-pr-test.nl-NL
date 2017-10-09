---
title: 'Azure Active Directory Domain Services: Bijwerken DNS-instellingen voor virtuele Azure-netwerk Hallo | Microsoft Docs'
description: Aan de slag met Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4f3e82c-6807-4690-b298-4eabad2b7927
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: maheshu
ms.openlocfilehash: 484ff1a197a651bccb2b416448056acf69b0d8c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="4b2b3-103">DNS-instellingen bijwerken voor Hallo virtuele Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="4b2b3-103">Update DNS settings for hello Azure virtual network</span></span>
## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="4b2b3-104">Taak 4: Bijwerken van DNS-instellingen voor Hallo virtuele Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="4b2b3-104">Task 4: Update DNS settings for hello Azure virtual network</span></span>
<span data-ttu-id="4b2b3-105">In de Hallo voorgaande configuratietaken, hebt u Azure Active Directory Domain Services voor uw directory is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="4b2b3-105">In hello preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="4b2b3-106">de volgende taak Hallo is tooensure dat computers in het virtuele netwerk Hallo kunnen verbinding maken en gebruiken van deze services.</span><span class="sxs-lookup"><span data-stu-id="4b2b3-106">hello next task is tooensure that computers within hello virtual network can connect and consume these services.</span></span> <span data-ttu-id="4b2b3-107">In dit artikel leert bijwerken u Hallo DNS-serverinstellingen voor uw virtuele netwerk toopoint toohello twee IP-adressen waarop Azure Active Directory Domain Services beschikbaar op Hallo virtueel netwerk is.</span><span class="sxs-lookup"><span data-stu-id="4b2b3-107">In this article, you update hello DNS server settings for your virtual network toopoint toohello two IP addresses where Azure Active Directory Domain Services is available on hello virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="4b2b3-108">Nadat u Azure Active Directory Domain Services voor Hallo directory hebt ingeschakeld, houd er rekening mee Hallo IP-adressen voor Azure Active Directory Domain Services die worden weergegeven op Hallo **configureren** tabblad van uw directory.</span><span class="sxs-lookup"><span data-stu-id="4b2b3-108">After you've enabled Azure Active Directory Domain Services for hello directory, note hello IP addresses for Azure Active Directory Domain Services that are displayed on hello **Configure** tab of your directory.</span></span>
>
>

<span data-ttu-id="4b2b3-109">tooupdate hello DNS-serverinstellingen voor Hallo virtuele netwerk waarin u Azure Active Directory Domain Services voltooid Hallo stappen hebt ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="4b2b3-109">tooupdate hello DNS server setting for hello virtual network in which you have enabled Azure Active Directory Domain Services, complete hello following steps:</span></span>

1. <span data-ttu-id="4b2b3-110">Ga toohello [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="4b2b3-110">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="4b2b3-111">Selecteer in het linkerdeelvenster Hallo **netwerken**.</span><span class="sxs-lookup"><span data-stu-id="4b2b3-111">In hello left pane, select **Networks**.</span></span>  
    <span data-ttu-id="4b2b3-112">Hallo **netwerken** venster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="4b2b3-112">hello **Networks** window opens.</span></span>

    ![Venster met virtuele netwerken](./media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. <span data-ttu-id="4b2b3-114">Op Hallo **virtuele netwerken** tabblad, selecteer Hallo virtuele netwerk waarin u ingeschakeld Azure Active Directory Domain Services tooview eigenschappen ervan.</span><span class="sxs-lookup"><span data-stu-id="4b2b3-114">On hello **Virtual Networks** tab, select hello virtual network in which you enabled Azure Active Directory Domain Services tooview its properties.</span></span>
4. <span data-ttu-id="4b2b3-115">Klik op Hallo **configureren** tabblad.</span><span class="sxs-lookup"><span data-stu-id="4b2b3-115">Click hello **Configure** tab.</span></span>

    ![Venster met virtuele netwerken](./media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. <span data-ttu-id="4b2b3-117">In Hallo **DNS-servers** sectie, voert u beide Hallo IP-adressen die werden weergegeven in Hallo **domeinservices** sectie op Hallo **configureren** tabblad van uw directory.</span><span class="sxs-lookup"><span data-stu-id="4b2b3-117">In hello **DNS servers** section, enter both of hello IP addresses that were displayed in hello **Domain Services** section on hello **Configure** tab of your directory.</span></span>
6. <span data-ttu-id="4b2b3-118">toosave hello DNS-serverinstellingen voor dit virtuele netwerk, in het taakvenster Hallo Hallo onder aan Hallo venster, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="4b2b3-118">toosave hello DNS server settings for this virtual network, in hello task pane at hello bottom of hello window, click **Save**.</span></span>

   ![Hallo DNS-serverinstellingen voor het virtuele netwerk Hallo bijwerken](./media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
>  <span data-ttu-id="4b2b3-120">Hallo nieuwe DNS-instellingen voor ophalen virtuele machines in Hallo netwerk alleen na het opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="4b2b3-120">Virtual machines in hello network only get hello new DNS settings after a restart.</span></span> <span data-ttu-id="4b2b3-121">Als u ze tooget Hallo bijgewerkt DNS-instellingen meteen moet, activeert u een herstart door het Hallo-portal, PowerShell of CLI Hallo.</span><span class="sxs-lookup"><span data-stu-id="4b2b3-121">If you need them tooget hello updated DNS settings right away, trigger a restart either by hello portal, PowerShell, or hello CLI.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="4b2b3-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4b2b3-122">Next steps</span></span>
<span data-ttu-id="4b2b3-123">Taak 5: [wachtwoord synchronisatie tooAzure Active Directory Domain Services inschakelen](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="4b2b3-123">Task 5: [Enable password synchronization tooAzure Active Directory Domain Services](active-directory-ds-getting-started-password-sync.md)</span></span>
