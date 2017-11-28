---
title: 'Azure Active Directory Domain Services: DNS-instellingen bijwerken voor het virtuele Azure-netwerk | Microsoft Docs'
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
ms.openlocfilehash: 8bee2a25f196d645b27f30f21305b1550e44e07a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="update-dns-settings-for-the-azure-virtual-network"></a><span data-ttu-id="6252b-103">DNS-instellingen bijwerken voor het virtuele Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="6252b-103">Update DNS settings for the Azure virtual network</span></span>
## <a name="task-4-update-dns-settings-for-the-azure-virtual-network"></a><span data-ttu-id="6252b-104">Taak 4: DNS-instellingen bijwerken voor het virtuele Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="6252b-104">Task 4: Update DNS settings for the Azure virtual network</span></span>
<span data-ttu-id="6252b-105">In de voorgaande configuratietaken hebt u Azure Active Directory Domain Services ingeschakeld voor uw directory.</span><span class="sxs-lookup"><span data-stu-id="6252b-105">In the preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="6252b-106">De volgende taak is om ervoor te zorgen dat computers binnen het virtuele netwerk verbinding kunnen maken met deze services en ze kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6252b-106">The next task is to ensure that computers within the virtual network can connect and consume these services.</span></span> <span data-ttu-id="6252b-107">In dit artikel werkt u de DNS-serverinstellingen voor het virtuele netwerk zo bij dat deze verwijzen naar de twee IP-adressen waarop Azure Active Directory Domain Services beschikbaar is op het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="6252b-107">In this article, you update the DNS server settings for your virtual network to point to the two IP addresses where Azure Active Directory Domain Services is available on the virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="6252b-108">Noteer de IP-adressen voor Azure Active Directory Domain Services die worden weergegeven op het tabblad **Configureren** van uw directory nadat u Azure Active Directory Domain Services hebt ingeschakeld voor de directory.</span><span class="sxs-lookup"><span data-stu-id="6252b-108">After you've enabled Azure Active Directory Domain Services for the directory, note the IP addresses for Azure Active Directory Domain Services that are displayed on the **Configure** tab of your directory.</span></span>
>
>

<span data-ttu-id="6252b-109">Voer de volgende stappen uit om de DNS-serverinstellingen bij te werken voor het virtuele netwerk waarin u Azure Active Directory Domain Services hebt ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="6252b-109">To update the DNS server setting for the virtual network in which you have enabled Azure Active Directory Domain Services, complete the following steps:</span></span>

1. <span data-ttu-id="6252b-110">Ga naar de [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="6252b-110">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="6252b-111">Selecteer **Netwerken** in het linkerdeelvenster.</span><span class="sxs-lookup"><span data-stu-id="6252b-111">In the left pane, select **Networks**.</span></span>  
    <span data-ttu-id="6252b-112">Het venster **Netwerken** wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="6252b-112">The **Networks** window opens.</span></span>

    ![Venster met virtuele netwerken](./media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. <span data-ttu-id="6252b-114">Selecteer op het tabblad **Virtuele netwerken** het virtuele netwerk waarin u Azure Active Directory Domain Services hebt ingeschakeld om de eigenschappen te bekijken.</span><span class="sxs-lookup"><span data-stu-id="6252b-114">On the **Virtual Networks** tab, select the virtual network in which you enabled Azure Active Directory Domain Services to view its properties.</span></span>
4. <span data-ttu-id="6252b-115">Klik op het tabblad **Configureren**.</span><span class="sxs-lookup"><span data-stu-id="6252b-115">Click the **Configure** tab.</span></span>

    ![Venster met virtuele netwerken](./media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. <span data-ttu-id="6252b-117">In de sectie **DNS-servers** geeft u beide IP-adressen op die werden weergegeven in de sectie **Domeinservices** op het tabblad **Configureren** van uw directory.</span><span class="sxs-lookup"><span data-stu-id="6252b-117">In the **DNS servers** section, enter both of the IP addresses that were displayed in the **Domain Services** section on the **Configure** tab of your directory.</span></span>
6. <span data-ttu-id="6252b-118">Klik op **Opslaan** in het taakvenster onderin om de DNS-serverinstellingen voor dit virtuele netwerk op te slaan.</span><span class="sxs-lookup"><span data-stu-id="6252b-118">To save the DNS server settings for this virtual network, in the task pane at the bottom of the window, click **Save**.</span></span>

   ![De DNS-serverinstellingen bijwerken voor het virtuele netwerk](./media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
>  <span data-ttu-id="6252b-120">De nieuwe DNS-instellingen worden pas op de virtuele machines toegepast na het opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="6252b-120">Virtual machines in the network only get the new DNS settings after a restart.</span></span> <span data-ttu-id="6252b-121">Als u de bijgewerkte DNS-instellingen meteen wilt toepassen, activeert u opnieuw opstarten via de portal, PowerShell of de CLI.</span><span class="sxs-lookup"><span data-stu-id="6252b-121">If you need them to get the updated DNS settings right away, trigger a restart either by the portal, PowerShell, or the CLI.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="6252b-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6252b-122">Next steps</span></span>
<span data-ttu-id="6252b-123">Taak 5: [wachtwoordsynchronisatie inschakelen voor Azure Active Directory Domain Services](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="6252b-123">Task 5: [Enable password synchronization to Azure Active Directory Domain Services](active-directory-ds-getting-started-password-sync.md)</span></span>
