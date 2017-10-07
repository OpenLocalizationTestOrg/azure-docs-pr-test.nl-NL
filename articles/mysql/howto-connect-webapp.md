---
title: aaaConnect bestaande Azure App Service tooAzure Database voor MySQL | Microsoft Docs
description: Instructies voor hoe tooproperly verbinding maken met een bestaande Database van de Azure App Service-tooAzure voor MySQL
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 6d5b16f316e186d665370adcd8b7c7bb38c8d51a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-an-existing-azure-app-service-tooazure-database-for-mysql-server"></a><span data-ttu-id="67c39-103">Verbinding maken met een bestaande Azure App Service-tooAzure Database voor de MySQL-server</span><span class="sxs-lookup"><span data-stu-id="67c39-103">Connect an existing Azure App Service tooAzure Database for MySQL server</span></span>
<span data-ttu-id="67c39-104">Dit document wordt uitgelegd hoe u een bestaande Azure App Service-tooyour tooconnect Azure-Database voor MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="67c39-104">This document explains how tooconnect an existing Azure App Service tooyour Azure Database for MySQL server.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="67c39-105">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="67c39-105">Before you begin</span></span>
<span data-ttu-id="67c39-106">Meld u bij toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="67c39-106">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="67c39-107">Maak een Azure-Database voor de MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="67c39-107">Create an Azure Database for MySQL server.</span></span> <span data-ttu-id="67c39-108">Voor meer informatie, Raadpleeg te[hoe toocreate Azure-Database voor MySQL-server van de Portal](quickstart-create-mysql-server-database-using-azure-portal.md) of [hoe toocreate Azure-Database voor MySQL-server met CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="67c39-108">For details, refer too[How toocreate Azure Database for MySQL server from Portal](quickstart-create-mysql-server-database-using-azure-portal.md) or [How toocreate Azure Database for MySQL server using CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span></span>

<span data-ttu-id="67c39-109">Er zijn momenteel twee oplossingen tooenable toegang van een Azure App Service-tooan Azure Database voor MySQL.</span><span class="sxs-lookup"><span data-stu-id="67c39-109">Currently there are two solutions tooenable access from an Azure App Service tooan Azure Database for MySQL.</span></span> <span data-ttu-id="67c39-110">Beide oplossingen hebben betrekking op serverniveau firewallregels instellen.</span><span class="sxs-lookup"><span data-stu-id="67c39-110">Both solutions involve setting up server-level firewall rules.</span></span>

## <a name="solution-1---create-a-firewall-rule-tooallow-all-ips"></a><span data-ttu-id="67c39-111">Oplossing 1: Maak een regel firewall tooallow alle IP-adressen</span><span class="sxs-lookup"><span data-stu-id="67c39-111">Solution 1 - Create a firewall rule tooallow all IPs</span></span>
<span data-ttu-id="67c39-112">Azure MySQL-Database biedt toegang tot beveiliging op basis van een firewall tooprotect uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="67c39-112">Azure Database for MySQL provides access security using a firewall tooprotect your data.</span></span> <span data-ttu-id="67c39-113">Als u verbinding maakt vanaf een Azure App Service-tooAzure Database MySQL-server, houd er rekening mee dat Hallo uitgaande zijn IP-adressen van App Service dynamisch karakter.</span><span class="sxs-lookup"><span data-stu-id="67c39-113">When connecting from an Azure App Service tooAzure Database for MySQL server, keep in mind that hello outbound IPs of App Service are dynamic in nature.</span></span> 

<span data-ttu-id="67c39-114">tooensure hello beschikbaarheid van uw Azure App Service, wordt u aangeraden deze oplossing tooallow alle IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="67c39-114">tooensure hello availability of your Azure App Service, we recommend using this solution tooallow ALL IPs.</span></span>

> [!NOTE]
> <span data-ttu-id="67c39-115">Microsoft werkt voor een lange termijn oplossing tooavoid waardoor alle IP-adressen voor Azure-services tooconnect tooAzure Database MySQL.</span><span class="sxs-lookup"><span data-stu-id="67c39-115">Microsoft is working for a long-term solution tooavoid allowing all IPs for Azure services tooconnect tooAzure Database for MySQL.</span></span>

1. <span data-ttu-id="67c39-116">Op Hallo MySQL serverblade onder de instellingen voor kop, klikt u op **verbindingsbeveiliging** tooopen Hallo verbindingsbeveiliging blade voor hello Azure voor MySQL-Database.</span><span class="sxs-lookup"><span data-stu-id="67c39-116">On hello MySQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for MySQL.</span></span>

   ![Azure-portal - Klik op de beveiliging van de verbinding](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="67c39-118">Voer **REGELNAAM**, **START IP**, en **END-IP**.</span><span class="sxs-lookup"><span data-stu-id="67c39-118">Enter **RULE NAME**, **START IP**, and **END IP**.</span></span> <span data-ttu-id="67c39-119">Klik vervolgens op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="67c39-119">Then click **Save**.</span></span>
   - <span data-ttu-id="67c39-120">Regelnaam: toestaan-All-IP-adressen</span><span class="sxs-lookup"><span data-stu-id="67c39-120">Rule name: Allow-All-IPs</span></span>
   - <span data-ttu-id="67c39-121">Start-IP: 0.0.0.0</span><span class="sxs-lookup"><span data-stu-id="67c39-121">Start IP: 0.0.0.0</span></span>
   - <span data-ttu-id="67c39-122">End-IP: 255.255.255.255</span><span class="sxs-lookup"><span data-stu-id="67c39-122">End IP: 255.255.255.255</span></span>

   ![Azure-portal - alle IP-adressen toevoegen](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-tooexplicitly-allow-outbound-ips"></a><span data-ttu-id="67c39-124">Oplossing 2: Maak een firewall regel tooexplicitly uitgaande IP-adressen toestaan</span><span class="sxs-lookup"><span data-stu-id="67c39-124">Solution 2 - Create a firewall rule tooexplicitly allow outbound IPs</span></span>
<span data-ttu-id="67c39-125">U kunt expliciet toevoegen dat alle Hallo uitgaande IP-adressen van uw Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="67c39-125">You can explicitly add all hello outbound IPs of your Azure App Service.</span></span>

1. <span data-ttu-id="67c39-126">Hallo-App Service-eigenschappen blade voor de weergave uw **uitgaande IP-adres**.</span><span class="sxs-lookup"><span data-stu-id="67c39-126">On hello App Service Properties blade, view your **OUTBOUND IP ADDRESS**.</span></span>

   ![Azure portal - weergave uitgaande IP-adressen](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. <span data-ttu-id="67c39-128">Voeg op Hallo MySQL verbinding beveiliging blade uitgaande IP-adressen één voor één.</span><span class="sxs-lookup"><span data-stu-id="67c39-128">On hello MySQL Connection security blade, add outbound IPs one by one.</span></span>

   ![Azure-portal - expliciete IP-adressen toevoegen](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. <span data-ttu-id="67c39-130">Houd er rekening mee te**opslaan** uw firewallregels.</span><span class="sxs-lookup"><span data-stu-id="67c39-130">Remember too**Save** your firewall rules.</span></span>

<span data-ttu-id="67c39-131">Hoewel het Hallo-Azure App service probeert tookeep IP-adressen constante gedurende een bepaalde periode, zijn er ook gevallen waarbij Hallo IP-adressen mag wijzigen.</span><span class="sxs-lookup"><span data-stu-id="67c39-131">Though hello Azure App service attempts tookeep IP addresses constant over time, there are cases where hello IP addresses may change.</span></span> <span data-ttu-id="67c39-132">Bijvoorbeeld wanneer Hallo app recyclet of een schaalaanpassing deze gebeurtenis treedt op wanneer nieuwe machines worden toegevoegd in Azure regionale data centers tooincrease Hallo capaciteit.</span><span class="sxs-lookup"><span data-stu-id="67c39-132">For example, when hello app recycles or a scale operation occurs, or when new machines are added in Azure regional data centers tooincrease hello capacity.</span></span> <span data-ttu-id="67c39-133">Wanneer Hallo IP-wijzigen adressen, Hallo app uitvaltijd in deze niet langer verbinding kan maken Hallo-gebeurtenis kan optreden toohello MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="67c39-133">When hello IP addresses change, hello app could experience downtime in hello event it can no longer connect toohello MySQL server.</span></span> <span data-ttu-id="67c39-134">U kunt dit potentieel bij het kiezen van een van de voorgaande oplossingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="67c39-134">Consider this potential when choosing one of hello preceding solutions.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="67c39-135">SSL-configuratie</span><span class="sxs-lookup"><span data-stu-id="67c39-135">SSL configuration</span></span>
<span data-ttu-id="67c39-136">Azure MySQL-Database heeft SSL ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="67c39-136">Azure Database for MySQL has SSL Enabled by default.</span></span> <span data-ttu-id="67c39-137">Als uw toepassing niet van SSL tooconnect toohello database gebruikmaakt, moet u toodisable SSL op MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="67c39-137">If your application is not using SSL tooconnect toohello database, then you need toodisable SSL on MySQL server.</span></span> <span data-ttu-id="67c39-138">Voor meer informatie over het tooconfigure SSL, Zie [met behulp van SSL met Azure-Database voor MySQL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="67c39-138">For details on how tooconfigure SSL, See [Using SSL with Azure Database for MySQL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="67c39-139">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="67c39-139">Next steps</span></span>
<span data-ttu-id="67c39-140">Raadpleeg te voor meer informatie over verbindingsreeksen[verbindingsreeksen](howto-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="67c39-140">For more information about connection strings, refer too[Connection Strings](howto-connection-string.md).</span></span>
