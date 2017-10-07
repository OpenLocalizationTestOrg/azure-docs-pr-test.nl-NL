---
title: aaaCreate en beheren van Azure-Database voor firewallregels MySQL hello Azure-portal met | Microsoft Docs
description: Maken en beheren van Azure-Database voor firewallregels MySQL met hello Azure-portal
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 30dbdde4299df564fbf6581419e908186fe3b823
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-hello-azure-portal"></a><span data-ttu-id="b084d-103">Maken en beheren van Azure-Database voor firewallregels MySQL met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="b084d-103">Create and manage Azure Database for MySQL firewall rules using hello Azure portal</span></span>
<span data-ttu-id="b084d-104">Firewallregels op serverniveau inschakelen beheerders tooaccess een Azure-Database voor MySQL-Server uit een opgegeven IP-adres of een bereik van IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="b084d-104">Server-level firewall rules enable administrators tooaccess an Azure Database for MySQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="b084d-105">Maken van een firewallregel op serverniveau in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="b084d-105">Create a server-level firewall rule in hello Azure portal</span></span>

1. <span data-ttu-id="b084d-106">Op Hallo MySQL serverblade onder de instellingen voor kop, klikt u op **verbindingsbeveiliging** tooopen Hallo verbindingsbeveiliging blade voor hello Azure voor MySQL-Database.</span><span class="sxs-lookup"><span data-stu-id="b084d-106">On hello MySQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for MySQL.</span></span>

   ![Azure-portal - Klik op de beveiliging van de verbinding](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="b084d-108">Klik op **Mijn IP toevoegen** op Hallo werkbalk toocreate een regel met Hallo IP-adres van uw computer, zoals waargenomen door hello Azure systeem.</span><span class="sxs-lookup"><span data-stu-id="b084d-108">Click **Add My IP** on hello toolbar toocreate a rule with hello IP address of your computer, as perceived by hello Azure system.</span></span>

   ![Azure-portal - Klik op toevoegen Mijn IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="b084d-110">Controleer of uw IP-adres voordat u opslaat Hallo-configuratie.</span><span class="sxs-lookup"><span data-stu-id="b084d-110">Verify your IP address before saving hello configuration.</span></span> <span data-ttu-id="b084d-111">In sommige situaties Hallo IP-adres door Azure-portal waargenomen verschilt Hallo IP-adres dat wordt gebruikt wanneer toegang tot Hallo internet en Azure-servers.</span><span class="sxs-lookup"><span data-stu-id="b084d-111">In some situations, hello IP address observed by Azure portal differs from hello IP address used when accessing hello internet and Azure servers.</span></span> <span data-ttu-id="b084d-112">Daarom moet u toochange Hallo eerste IP- en eind-IP-toomake Hallo regel functie zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="b084d-112">Therefore, you may need toochange hello Start IP and End IP toomake hello rule function as expected.</span></span>

   <span data-ttu-id="b084d-113">Gebruik een zoekmachine of andere toocheck online hulpprogramma uw eigen IP-adres (Zoek bijvoorbeeld naar 'Wat is Mijn IP-adres').</span><span class="sxs-lookup"><span data-stu-id="b084d-113">Use a search engine or other online tool toocheck your own IP address (for example, search "what is my IP address").</span></span>

   ![Bing voor Mijn IP](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="b084d-115">Voeg aanvullende adresbereiken.</span><span class="sxs-lookup"><span data-stu-id="b084d-115">Add additional address ranges.</span></span> <span data-ttu-id="b084d-116">In het Hallo-regels voor hello Azure Database voor MySQL firewall, kunt u één IP-adres of een bereik aan adressen opgeven.</span><span class="sxs-lookup"><span data-stu-id="b084d-116">In hello rules for hello Azure Database for MySQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="b084d-117">Als u wilt dat toolimit Hallo regel tooone één IP-adres, type Hallo dezelfde in Hallo veld voor het eerste IP- en eind-IP-adres.</span><span class="sxs-lookup"><span data-stu-id="b084d-117">If you want toolimit hello rule tooone single IP address, type hello same address in hello field for Start IP and End IP.</span></span> <span data-ttu-id="b084d-118">Hallo firewall openen kan beheerders en gebruikers tooaccess alle databases op Hallo MySQL server toowhich ze geldige referenties bevatten.</span><span class="sxs-lookup"><span data-stu-id="b084d-118">Opening hello firewall enables administrators and users tooaccess any database on hello MySQL server toowhich they have valid credentials.</span></span>

   ![<span data-ttu-id="b084d-119">Azure portal - firewall-regels</span><span class="sxs-lookup"><span data-stu-id="b084d-119">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. <span data-ttu-id="b084d-120">Klik op **opslaan** op Hallo werkbalk toosave deze firewallregel op serverniveau.</span><span class="sxs-lookup"><span data-stu-id="b084d-120">Click **Save** on hello toolbar toosave this server-level firewall rule.</span></span> <span data-ttu-id="b084d-121">Wacht op bevestiging van Hallo Hallo update toohello firewallregels is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="b084d-121">Wait for hello confirmation that hello update toohello firewall rules was successful.</span></span>

   ![Azure-portal - Klik op Opslaan](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="b084d-123">Bestaande serverniveau firewallregels via hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="b084d-123">Manage existing server-level firewall rules through hello Azure portal</span></span>
<span data-ttu-id="b084d-124">Herhaal Hallo stappen toomanage Hallo firewall-regels.</span><span class="sxs-lookup"><span data-stu-id="b084d-124">Repeat hello steps toomanage hello firewall rules.</span></span>
* <span data-ttu-id="b084d-125">tooadd hello huidige computer, klikt u op **+ Mijn IP toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b084d-125">tooadd hello current computer, click **+ Add My IP**.</span></span>
* <span data-ttu-id="b084d-126">tooadd extra IP-adressen, typt u Hallo **REGELNAAM**, **eerste IP-**, en **END-IP**.</span><span class="sxs-lookup"><span data-stu-id="b084d-126">tooadd additional IP addresses, type in hello **RULE NAME**, **START IP**, and **END IP**.</span></span>
* <span data-ttu-id="b084d-127">een bestaande regel toomodify klikt u op een van de velden in de regel Hallo Hallo en wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b084d-127">toomodify an existing rule, click any of hello fields in hello rule and modify.</span></span>
* <span data-ttu-id="b084d-128">een bestaande toodelete sluiten, klikt u op Hallo weglatingsteken [...] en klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="b084d-128">toodelete an existing rule, click hello ellipsis […] and click **Delete**.</span></span>
* <span data-ttu-id="b084d-129">Klik op **opslaan** toosave Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="b084d-129">Click **Save** toosave hello changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b084d-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b084d-130">Next steps</span></span>
- <span data-ttu-id="b084d-131">Zie voor informatie over tooan Azure Database voor de MySQL-server verbinding [verbindingsbibliotheken voor Azure-Database voor MySQL](./concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="b084d-131">For help in connecting tooan Azure Database for MySQL server, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md)</span></span>
