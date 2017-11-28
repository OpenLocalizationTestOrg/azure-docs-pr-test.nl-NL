---
title: aaaCreate en beheren van Azure-Database voor firewallregels PostgreSQL hello Azure-portal met | Microsoft Docs
description: Maken en beheren van Azure-Database voor firewallregels PostgreSQL met hello Azure-portal
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6a41a077168657769e442401e9df9931aa809240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-hello-azure-portal"></a><span data-ttu-id="18649-103">Maken en beheren van Azure-Database voor firewallregels PostgreSQL met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="18649-103">Create and manage Azure Database for PostgreSQL firewall rules using hello Azure portal</span></span>
<span data-ttu-id="18649-104">Firewallregels op serverniveau inschakelen beheerders tooaccess een Azure-Database voor PostgreSQL-Server uit een opgegeven IP-adres of een bereik van IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="18649-104">Server-level firewall rules enable administrators tooaccess an Azure Database for PostgreSQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="18649-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="18649-105">Prerequisites</span></span>
<span data-ttu-id="18649-106">toostep via deze procedure-tooguide die u nodig:</span><span class="sxs-lookup"><span data-stu-id="18649-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="18649-107">Een server [PostgreSQL een Azure-Database gemaakt](quickstart-create-server-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="18649-107">A server [Create an Azure Database for PostgreSQL](quickstart-create-server-database-portal.md)</span></span>

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="18649-108">Maken van een firewallregel op serverniveau in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="18649-108">Create a server-level firewall rule in hello Azure portal</span></span>
1. <span data-ttu-id="18649-109">Op Hallo PostgreSQL serverblade onder de instellingen voor kop, klikt u op **verbindingsbeveiliging** tooopen Hallo verbindingsbeveiliging blade voor hello Azure voor PostgreSQL-Database.</span><span class="sxs-lookup"><span data-stu-id="18649-109">On hello PostgreSQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for PostgreSQL.</span></span>

  ![Azure-portal - Klik op de beveiliging van de verbinding](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="18649-111">Klik op **Mijn IP toevoegen** op Hallo-werkbalk.</span><span class="sxs-lookup"><span data-stu-id="18649-111">Click **Add My IP** on hello toolbar.</span></span> <span data-ttu-id="18649-112">Hiermee maakt u een regel automatisch met Hallo IP-adres van uw computer, zoals waargenomen door hello Azure systeem.</span><span class="sxs-lookup"><span data-stu-id="18649-112">This will create a rule automatically with hello IP address of your computer, as perceived by hello Azure system.</span></span>

  ![Azure-portal - Klik op toevoegen Mijn IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="18649-114">Controleer of uw IP-adres voordat u opslaat Hallo-configuratie.</span><span class="sxs-lookup"><span data-stu-id="18649-114">Verify your IP address before saving hello configuration.</span></span> <span data-ttu-id="18649-115">In sommige situaties Hallo IP-adres door Azure-portal waargenomen verschilt Hallo IP-adres dat wordt gebruikt wanneer toegang tot Hallo internet en Azure-servers.</span><span class="sxs-lookup"><span data-stu-id="18649-115">In some situations, hello IP address observed by Azure portal differs from hello IP address used when accessing hello internet and Azure servers.</span></span> <span data-ttu-id="18649-116">Daarom moet u toochange Hallo eerste IP- en eind-IP-toomake Hallo regel functie zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="18649-116">Therefore, you may need toochange hello Start IP and End IP toomake hello rule function as expected.</span></span>
<span data-ttu-id="18649-117">Gebruik een zoekmachine of andere toocheck online hulpprogramma uw eigen IP-adres (bijvoorbeeld Bing zoeken 'Wat is Mijn IP').</span><span class="sxs-lookup"><span data-stu-id="18649-117">Use a search engine or other online tool toocheck your own IP address (for example, Bing search "what is my IP").</span></span>

  ![Bing zoeken naar wat Mijn IP is](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="18649-119">Voeg aanvullende adresbereiken.</span><span class="sxs-lookup"><span data-stu-id="18649-119">Add additional address ranges.</span></span> <span data-ttu-id="18649-120">In het Hallo-regels voor hello Azure Database voor PostgreSQL firewall, kunt u één IP-adres of een bereik aan adressen opgeven.</span><span class="sxs-lookup"><span data-stu-id="18649-120">In hello rules for hello Azure Database for PostgreSQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="18649-121">Als u wilt dat toolimit Hallo regel tooone één IP-adres, type Hallo dezelfde in Hallo veld voor het eerste IP- en eind-IP-adres.</span><span class="sxs-lookup"><span data-stu-id="18649-121">If you want toolimit hello rule tooone single IP address, type hello same address in hello field for Start IP and End IP.</span></span> <span data-ttu-id="18649-122">Hallo firewall openen kan beheerders en gebruikers toologin tooany-database op Hallo PostgreSQL server toowhich ze geldige referenties bevatten.</span><span class="sxs-lookup"><span data-stu-id="18649-122">Opening hello firewall enables administrators and users toologin tooany database on hello PostgreSQL server toowhich they have valid credentials.</span></span>

  ![<span data-ttu-id="18649-123">Azure portal - firewall-regels</span><span class="sxs-lookup"><span data-stu-id="18649-123">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. <span data-ttu-id="18649-124">Klik op **opslaan** op Hallo werkbalk toosave deze firewallregel op serverniveau.</span><span class="sxs-lookup"><span data-stu-id="18649-124">Click **Save** on hello toolbar toosave this server-level firewall rule.</span></span> <span data-ttu-id="18649-125">Wacht op bevestiging van Hallo Hallo update toohello firewallregels is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="18649-125">Wait for hello confirmation that hello update toohello firewall rules was successful.</span></span>

  ![Azure-portal - Klik op Opslaan](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="18649-127">Bestaande serverniveau firewallregels via hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="18649-127">Manage existing server-level firewall rules through hello Azure portal</span></span>
<span data-ttu-id="18649-128">Herhaal Hallo stappen toomanage Hallo firewall-regels.</span><span class="sxs-lookup"><span data-stu-id="18649-128">Repeat hello steps toomanage hello firewall rules.</span></span>
* <span data-ttu-id="18649-129">tooadd hello huidige computer, klik op de knop hello te + **Mijn IP toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="18649-129">tooadd hello current computer, click hello button too+ **Add My IP**.</span></span> <span data-ttu-id="18649-130">Klik op **opslaan** toosave Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="18649-130">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="18649-131">tooadd extra IP-adressen, typt u in Hallo regelnaam, eerste IP-adres en laatste IP-adres.</span><span class="sxs-lookup"><span data-stu-id="18649-131">tooadd additional IP addresses, type in hello Rule Name, Start IP Address, and End IP Address.</span></span> <span data-ttu-id="18649-132">Klik op **opslaan** toosave Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="18649-132">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="18649-133">een bestaande regel toomodify klikt u op een van de velden in de regel Hallo Hallo en wijzigen.</span><span class="sxs-lookup"><span data-stu-id="18649-133">toomodify an existing rule, click any of hello fields in hello rule and modify.</span></span> <span data-ttu-id="18649-134">Klik op **opslaan** toosave Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="18649-134">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="18649-135">een bestaande regel toodelete Hallo weglatingsteken [...] en klik op Hallo regel voor het verwijderen van verwijderen.</span><span class="sxs-lookup"><span data-stu-id="18649-135">toodelete an existing rule, click hello ellipsis […] and click Delete remove hello rule.</span></span> <span data-ttu-id="18649-136">Klik op **opslaan** toosave Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="18649-136">Click **Save** toosave hello changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18649-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="18649-137">Next steps</span></span>
- <span data-ttu-id="18649-138">Op deze manier kunt in een script te[maken en beheren van Azure-Database voor firewallregels PostgreSQL met Azure CLI](howto-manage-firewall-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="18649-138">Similarly, you can script too[Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI](howto-manage-firewall-using-cli.md)</span></span>
- <span data-ttu-id="18649-139">Zie voor informatie over verbinding tooan Azure Database voor PostgreSQL server [verbindingsbibliotheken voor Azure-Database voor PostgreSQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="18649-139">For help in connecting tooan Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
