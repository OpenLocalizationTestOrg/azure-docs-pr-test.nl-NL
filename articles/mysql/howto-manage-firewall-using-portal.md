---
title: Maken en beheren van Azure-Database voor firewallregels MySQL met de Azure portal | Microsoft Docs
description: Maken en beheren van Azure-Database voor firewallregels MySQL met de Azure portal
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 33198e5a6e11df2db3a17fc96a0b3cd4b1a284e8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-the-azure-portal"></a><span data-ttu-id="b95fa-103">Maken en beheren van Azure-Database voor firewallregels MySQL met de Azure portal</span><span class="sxs-lookup"><span data-stu-id="b95fa-103">Create and manage Azure Database for MySQL firewall rules using the Azure portal</span></span>
<span data-ttu-id="b95fa-104">Firewallregels op serverniveau kunnen beheerders toegang krijgen tot een Azure-Database voor MySQL-Server uit een opgegeven IP-adres of een bereik van IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="b95fa-104">Server-level firewall rules enable administrators to access an Azure Database for MySQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="b95fa-105">Een serverfirewallregel maken in Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b95fa-105">Create a server-level firewall rule in the Azure portal</span></span>

1. <span data-ttu-id="b95fa-106">Op de blade MySQL-server onder de instellingen voor kop, klikt u op **verbindingsbeveiliging** de verbindingsbeveiliging blade voor de Azure-Database voor MySQL openen.</span><span class="sxs-lookup"><span data-stu-id="b95fa-106">On the MySQL server blade, under Settings heading, click **Connection Security** to open the Connection Security blade for the Azure Database for MySQL.</span></span>

   ![Azure-portal - Klik op de beveiliging van de verbinding](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="b95fa-108">Klik op **Mijn IP toevoegen** op de werkbalk om een regel maken met het IP-adres van uw computer, zoals waargenomen door het Azure-systeem.</span><span class="sxs-lookup"><span data-stu-id="b95fa-108">Click **Add My IP** on the toolbar to create a rule with the IP address of your computer, as perceived by the Azure system.</span></span>

   ![Azure-portal - Klik op toevoegen Mijn IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="b95fa-110">Controleer of uw IP-adres voor het opslaan van de configuratie.</span><span class="sxs-lookup"><span data-stu-id="b95fa-110">Verify your IP address before saving the configuration.</span></span> <span data-ttu-id="b95fa-111">In sommige gevallen is verschilt het IP-adres dat door de Azure-portal waargenomen van het IP-adres gebruikt bij het openen van het internet en de Azure-servers.</span><span class="sxs-lookup"><span data-stu-id="b95fa-111">In some situations, the IP address observed by Azure portal differs from the IP address used when accessing the internet and Azure servers.</span></span> <span data-ttu-id="b95fa-112">Daarom moet u mogelijk het eerste IP- en eind-IP-ervoor zorgen dat de regel werkt zoals verwacht wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b95fa-112">Therefore, you may need to change the Start IP and End IP to make the rule function as expected.</span></span>

   <span data-ttu-id="b95fa-113">Gebruik een zoekmachine of andere online hulpprogramma om te controleren van uw eigen IP-adres (Zoek bijvoorbeeld naar 'Wat is Mijn IP-adres').</span><span class="sxs-lookup"><span data-stu-id="b95fa-113">Use a search engine or other online tool to check your own IP address (for example, search "what is my IP address").</span></span>

   ![Bing voor Mijn IP](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="b95fa-115">Voeg aanvullende adresbereiken.</span><span class="sxs-lookup"><span data-stu-id="b95fa-115">Add additional address ranges.</span></span> <span data-ttu-id="b95fa-116">U kunt één IP-adres of een bereik aan adressen opgeven in de regels voor de Azure-Database voor de MySQL-firewall.</span><span class="sxs-lookup"><span data-stu-id="b95fa-116">In the rules for the Azure Database for MySQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="b95fa-117">Als u beperken van de regel toe aan een enkel IP-adres wilt, typt u hetzelfde adres in het veld voor het eerste IP- en End IP-adres.</span><span class="sxs-lookup"><span data-stu-id="b95fa-117">If you want to limit the rule to one single IP address, type the same address in the field for Start IP and End IP.</span></span> <span data-ttu-id="b95fa-118">De firewall te openen, kunnen beheerders en gebruikers toegang krijgen tot een database op de MySQL-server waartoe ze geldige referenties hebben.</span><span class="sxs-lookup"><span data-stu-id="b95fa-118">Opening the firewall enables administrators and users to access any database on the MySQL server to which they have valid credentials.</span></span>

   ![<span data-ttu-id="b95fa-119">Azure portal - firewall-regels</span><span class="sxs-lookup"><span data-stu-id="b95fa-119">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. <span data-ttu-id="b95fa-120">Klik op **opslaan** op de werkbalk om op te slaan deze firewallregel op serverniveau.</span><span class="sxs-lookup"><span data-stu-id="b95fa-120">Click **Save** on the toolbar to save this server-level firewall rule.</span></span> <span data-ttu-id="b95fa-121">Wacht totdat de bevestiging dat de update voor de firewallregels geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="b95fa-121">Wait for the confirmation that the update to the firewall rules was successful.</span></span>

   ![Azure-portal - Klik op Opslaan](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="b95fa-123">Bestaande firewallregels op serverniveau beheren via Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b95fa-123">Manage existing server-level firewall rules through the Azure portal</span></span>
<span data-ttu-id="b95fa-124">Herhaal de stappen voor het beheren van de firewall-regels.</span><span class="sxs-lookup"><span data-stu-id="b95fa-124">Repeat the steps to manage the firewall rules.</span></span>
* <span data-ttu-id="b95fa-125">Als u wilt toevoegen in de huidige computer, klikt u op **+ Mijn IP toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b95fa-125">To add the current computer, click **+ Add My IP**.</span></span>
* <span data-ttu-id="b95fa-126">Extra IP-adressen, typt u de **REGELNAAM**, **eerste IP-**, en **END-IP**.</span><span class="sxs-lookup"><span data-stu-id="b95fa-126">To add additional IP addresses, type in the **RULE NAME**, **START IP**, and **END IP**.</span></span>
* <span data-ttu-id="b95fa-127">Als u een bestaande regel wilt wijzigen, klikt u op een willekeurig veld in de regel om dit aan te passen.</span><span class="sxs-lookup"><span data-stu-id="b95fa-127">To modify an existing rule, click any of the fields in the rule and modify.</span></span>
* <span data-ttu-id="b95fa-128">Verwijder een bestaande regel, klik op het weglatingsteken [...] te klikken en **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="b95fa-128">To delete an existing rule, click the ellipsis […] and click **Delete**.</span></span>
* <span data-ttu-id="b95fa-129">Klik op **Opslaan** om de wijzigingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="b95fa-129">Click **Save** to save the changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b95fa-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b95fa-130">Next steps</span></span>
- <span data-ttu-id="b95fa-131">Voor hulp bij het verbinding maken met een Azure-Database voor de MySQL-server, Zie [verbindingsbibliotheken voor Azure-Database voor MySQL](./concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="b95fa-131">For help in connecting to an Azure Database for MySQL server, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md)</span></span>
