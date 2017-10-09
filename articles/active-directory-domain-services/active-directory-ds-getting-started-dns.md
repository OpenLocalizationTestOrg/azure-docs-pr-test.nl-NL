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
ms.openlocfilehash: e6eaff555cb9b7bb89ab7581d8de0b8cfc844529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a><span data-ttu-id="62d27-103">Azure Active Directory Domain Services (preview) inschakelen</span><span class="sxs-lookup"><span data-stu-id="62d27-103">Enable Azure Active Directory Domain Services (Preview)</span></span>

## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="62d27-104">Taak 4: DNS-instellingen bijwerken voor Hallo virtuele Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="62d27-104">Task 4: update DNS settings for hello Azure virtual network</span></span>
<span data-ttu-id="62d27-105">In de Hallo voorgaande configuratietaken, hebt u Azure Active Directory Domain Services voor uw directory is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="62d27-105">In hello preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="62d27-106">de volgende taak Hallo is tooensure dat computers in het virtuele netwerk Hallo kunnen verbinding maken en gebruiken van deze services.</span><span class="sxs-lookup"><span data-stu-id="62d27-106">hello next task is tooensure that computers within hello virtual network can connect and consume these services.</span></span> <span data-ttu-id="62d27-107">In dit artikel leert bijwerken u Hallo DNS-serverinstellingen voor uw virtuele netwerk toopoint toohello twee IP-adressen waarop Azure Active Directory Domain Services beschikbaar op Hallo virtueel netwerk is.</span><span class="sxs-lookup"><span data-stu-id="62d27-107">In this article, you update hello DNS server settings for your virtual network toopoint toohello two IP addresses where Azure Active Directory Domain Services is available on hello virtual network.</span></span>

<span data-ttu-id="62d27-108">tooupdate hello DNS-serverinstellingen voor Hallo virtuele netwerk waarin u Azure Active Directory Domain Services voltooid Hallo stappen hebt ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="62d27-108">tooupdate hello DNS server setting for hello virtual network in which you have enabled Azure Active Directory Domain Services, complete hello following steps:</span></span>

1. <span data-ttu-id="62d27-109">Hallo **overzicht** tabblad bevat een reeks **configuratiestappen vereist** toobe uitgevoerd nadat u uw beheerde domein volledig is ingericht.</span><span class="sxs-lookup"><span data-stu-id="62d27-109">hello **Overview** tab lists a set of **Required configuration steps** toobe performed after your managed domain is fully provisioned.</span></span> <span data-ttu-id="62d27-110">Hallo eerste configuratiestap is **Update DNS-serverinstellingen voor het virtuele netwerk**.</span><span class="sxs-lookup"><span data-stu-id="62d27-110">hello first configuration step is **Update DNS server settings for your virtual network**.</span></span>

    ![Domain Services: tabblad Overzicht nadat het domein volledig is ingericht](./media/getting-started/domain-services-provisioned-overview.png)

2. <span data-ttu-id="62d27-112">Wanneer uw domein volledig is ingericht, worden er twee IP-adressen weergegeven in deze tegel.</span><span class="sxs-lookup"><span data-stu-id="62d27-112">When your domain is fully provisioned, two IP addresses are displayed in this tile.</span></span> <span data-ttu-id="62d27-113">Elk IP-adres vertegenwoordigt een domeincontroller voor uw beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="62d27-113">Each of these IP addresses represents a domain controller for your managed domain.</span></span>

3. <span data-ttu-id="62d27-114">toocopy hello eerste IP-adres tooclipboard adres, klikt u op Hallo kopie knop volgende tooit.</span><span class="sxs-lookup"><span data-stu-id="62d27-114">toocopy hello first IP address tooclipboard, click hello copy button next tooit.</span></span> <span data-ttu-id="62d27-115">Klik vervolgens op Hallo **configureren van DNS-servers** knop.</span><span class="sxs-lookup"><span data-stu-id="62d27-115">Then click hello **Configure DNS servers** button.</span></span>

4. <span data-ttu-id="62d27-116">Hallo eerste IP-adres in Hallo plakken **toevoegen DNS-server** textbox in Hallo **DNS-servers** blade.</span><span class="sxs-lookup"><span data-stu-id="62d27-116">Paste hello first IP address into hello **Add DNS server** textbox in hello **DNS servers** blade.</span></span> <span data-ttu-id="62d27-117">Horizontaal schuiven toohello links toocopy Hallo tweede IP-adres en plak deze in Hallo **toevoegen DNS-server** textbox.</span><span class="sxs-lookup"><span data-stu-id="62d27-117">Scroll horizontally toohello left toocopy hello second IP address and paste it into hello **Add DNS server** textbox.</span></span>

    ![Domain Services: DNS bijwerken](./media/getting-started/domain-services-update-dns.png)

5. <span data-ttu-id="62d27-119">Klik op **opslaan** wanneer u tooupdate Hallo DNS-servers voor het virtuele netwerk Hallo zijn klaar.</span><span class="sxs-lookup"><span data-stu-id="62d27-119">Click **Save** when you are done tooupdate hello DNS servers for hello virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="62d27-120">Hallo nieuwe DNS-instellingen voor ophalen virtuele machines in Hallo netwerk alleen na het opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="62d27-120">Virtual machines in hello network only get hello new DNS settings after a restart.</span></span> <span data-ttu-id="62d27-121">Als u ze tooget Hallo bijgewerkt DNS-instellingen meteen moet, activeert u een herstart door het Hallo-portal, PowerShell of CLI Hallo.</span><span class="sxs-lookup"><span data-stu-id="62d27-121">If you need them tooget hello updated DNS settings right away, trigger a restart either by hello portal, PowerShell, or hello CLI.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="62d27-122">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="62d27-122">Next step</span></span>
[<span data-ttu-id="62d27-123">Taak 5: wachtwoord synchronisatie tooAzure Active Directory Domain Services inschakelen</span><span class="sxs-lookup"><span data-stu-id="62d27-123">Task 5: enable password synchronization tooAzure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-password-sync.md)
