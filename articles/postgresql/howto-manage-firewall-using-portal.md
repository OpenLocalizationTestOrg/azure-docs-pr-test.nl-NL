---
title: Maken en beheren van Azure-Database voor firewallregels PostgreSQL met de Azure portal | Microsoft Docs
description: Maken en beheren van Azure-Database voor firewallregels PostgreSQL met de Azure portal
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 20ac1392949a6f604e68d984cb50273b61051037
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-the-azure-portal"></a><span data-ttu-id="a362a-103">Maken en beheren van Azure-Database voor firewallregels PostgreSQL met de Azure portal</span><span class="sxs-lookup"><span data-stu-id="a362a-103">Create and manage Azure Database for PostgreSQL firewall rules using the Azure portal</span></span>
<span data-ttu-id="a362a-104">Firewallregels op serverniveau kunnen beheerders toegang krijgen tot een Azure-Database voor PostgreSQL-Server uit een opgegeven IP-adres of een bereik van IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="a362a-104">Server-level firewall rules enable administrators to access an Azure Database for PostgreSQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a362a-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a362a-105">Prerequisites</span></span>
<span data-ttu-id="a362a-106">Stap in deze handleiding instructies, wilt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="a362a-106">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="a362a-107">Een server [PostgreSQL een Azure-Database gemaakt](quickstart-create-server-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="a362a-107">A server [Create an Azure Database for PostgreSQL](quickstart-create-server-database-portal.md)</span></span>

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="a362a-108">Een serverfirewallregel maken in Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a362a-108">Create a server-level firewall rule in the Azure portal</span></span>
1. <span data-ttu-id="a362a-109">Op de blade PostgreSQL server onder de instellingen voor kop, klikt u op **verbindingsbeveiliging** de verbindingsbeveiliging blade voor de Azure-Database voor PostgreSQL openen.</span><span class="sxs-lookup"><span data-stu-id="a362a-109">On the PostgreSQL server blade, under Settings heading, click **Connection Security** to open the Connection Security blade for the Azure Database for PostgreSQL.</span></span>

  ![Azure-portal - Klik op de beveiliging van de verbinding](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="a362a-111">Klik op **Mijn IP toevoegen** op de werkbalk.</span><span class="sxs-lookup"><span data-stu-id="a362a-111">Click **Add My IP** on the toolbar.</span></span> <span data-ttu-id="a362a-112">Hiermee maakt u een regel automatisch met het IP-adres van uw computer, zoals waargenomen door het Azure-systeem.</span><span class="sxs-lookup"><span data-stu-id="a362a-112">This will create a rule automatically with the IP address of your computer, as perceived by the Azure system.</span></span>

  ![Azure-portal - Klik op toevoegen Mijn IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="a362a-114">Controleer of uw IP-adres voor het opslaan van de configuratie.</span><span class="sxs-lookup"><span data-stu-id="a362a-114">Verify your IP address before saving the configuration.</span></span> <span data-ttu-id="a362a-115">In sommige gevallen is verschilt het IP-adres dat door de Azure-portal waargenomen van het IP-adres gebruikt bij het openen van het internet en de Azure-servers.</span><span class="sxs-lookup"><span data-stu-id="a362a-115">In some situations, the IP address observed by Azure portal differs from the IP address used when accessing the internet and Azure servers.</span></span> <span data-ttu-id="a362a-116">Daarom moet u mogelijk het eerste IP- en eind-IP-ervoor zorgen dat de regel werkt zoals verwacht wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a362a-116">Therefore, you may need to change the Start IP and End IP to make the rule function as expected.</span></span>
<span data-ttu-id="a362a-117">Gebruik een zoekmachine of andere online hulpprogramma om te controleren van uw eigen IP-adres (bijvoorbeeld Bing zoeken 'Wat is Mijn IP').</span><span class="sxs-lookup"><span data-stu-id="a362a-117">Use a search engine or other online tool to check your own IP address (for example, Bing search "what is my IP").</span></span>

  ![Bing zoeken naar wat Mijn IP is](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="a362a-119">Voeg aanvullende adresbereiken.</span><span class="sxs-lookup"><span data-stu-id="a362a-119">Add additional address ranges.</span></span> <span data-ttu-id="a362a-120">U kunt één IP-adres of een bereik aan adressen opgeven in de regels voor de Azure-Database voor PostgreSQL-firewall.</span><span class="sxs-lookup"><span data-stu-id="a362a-120">In the rules for the Azure Database for PostgreSQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="a362a-121">Als u beperken van de regel toe aan een enkel IP-adres wilt, typt u hetzelfde adres in het veld voor het eerste IP- en End IP-adres.</span><span class="sxs-lookup"><span data-stu-id="a362a-121">If you want to limit the rule to one single IP address, type the same address in the field for Start IP and End IP.</span></span> <span data-ttu-id="a362a-122">De firewall te openen, kunnen beheerders en gebruikers om aan te melden met een database op de PostgreSQL-server waarmee ze geldige referenties bevatten.</span><span class="sxs-lookup"><span data-stu-id="a362a-122">Opening the firewall enables administrators and users to login to any database on the PostgreSQL server to which they have valid credentials.</span></span>

  ![<span data-ttu-id="a362a-123">Azure portal - firewall-regels</span><span class="sxs-lookup"><span data-stu-id="a362a-123">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. <span data-ttu-id="a362a-124">Klik op **opslaan** op de werkbalk om op te slaan deze firewallregel op serverniveau.</span><span class="sxs-lookup"><span data-stu-id="a362a-124">Click **Save** on the toolbar to save this server-level firewall rule.</span></span> <span data-ttu-id="a362a-125">Wacht totdat de bevestiging dat de update voor de firewallregels geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="a362a-125">Wait for the confirmation that the update to the firewall rules was successful.</span></span>

  ![Azure-portal - Klik op Opslaan](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="a362a-127">Bestaande firewallregels op serverniveau beheren via Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a362a-127">Manage existing server-level firewall rules through the Azure portal</span></span>
<span data-ttu-id="a362a-128">Herhaal de stappen voor het beheren van de firewall-regels.</span><span class="sxs-lookup"><span data-stu-id="a362a-128">Repeat the steps to manage the firewall rules.</span></span>
* <span data-ttu-id="a362a-129">Als u wilt toevoegen in de huidige computer, klik op de knop + **Mijn IP toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a362a-129">To add the current computer, click the button to + **Add My IP**.</span></span> <span data-ttu-id="a362a-130">Klik op **Opslaan** om de wijzigingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="a362a-130">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="a362a-131">As u extra IP-adressen wilt toevoegen, typt u de Regelnaam, het Eerste IP-adres en het Laatste IP-adres in.</span><span class="sxs-lookup"><span data-stu-id="a362a-131">To add additional IP addresses, type in the Rule Name, Start IP Address, and End IP Address.</span></span> <span data-ttu-id="a362a-132">Klik op **Opslaan** om de wijzigingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="a362a-132">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="a362a-133">Als u een bestaande regel wilt wijzigen, klikt u op een willekeurig veld in de regel om dit aan te passen.</span><span class="sxs-lookup"><span data-stu-id="a362a-133">To modify an existing rule, click any of the fields in the rule and modify.</span></span> <span data-ttu-id="a362a-134">Klik op **Opslaan** om de wijzigingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="a362a-134">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="a362a-135">Klik op het weglatingsteken [...] en klik op verwijderen verwijderen de regel voor het verwijderen van een bestaande regel.</span><span class="sxs-lookup"><span data-stu-id="a362a-135">To delete an existing rule, click the ellipsis […] and click Delete remove the rule.</span></span> <span data-ttu-id="a362a-136">Klik op **Opslaan** om de wijzigingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="a362a-136">Click **Save** to save the changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a362a-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a362a-137">Next steps</span></span>
- <span data-ttu-id="a362a-138">Op deze manier kunt script naar [maken en beheren van Azure-Database voor firewallregels PostgreSQL met Azure CLI](howto-manage-firewall-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="a362a-138">Similarly, you can script to [Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI](howto-manage-firewall-using-cli.md)</span></span>
- <span data-ttu-id="a362a-139">Zie voor meer informatie in de verbinding te maken met een Azure-Database voor PostgreSQL server [verbindingsbibliotheken voor Azure-Database voor PostgreSQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="a362a-139">For help in connecting to an Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
