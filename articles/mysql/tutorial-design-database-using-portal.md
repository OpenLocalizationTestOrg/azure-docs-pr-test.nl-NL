---
title: uw eerste Azure-Database voor de MySQL-database. Azure-Portal aaaDesign | Microsoft Docs
description: Deze zelfstudie wordt uitgelegd hoe toocreate en beheren van Azure-Database voor de MySQL-server en database gebruiken met Azure Portal.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: 06dd952acc5356b8cccaf36917df1ff8db4f7139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="c6ae7-103">Ontwerp van uw eerste Azure-Database voor de MySQL-database</span><span class="sxs-lookup"><span data-stu-id="c6ae7-103">Design your first Azure Database for MySQL database</span></span>
<span data-ttu-id="c6ae7-104">Azure MySQL-Database is een beheerde service waarmee u toorun, beheren en schalen van maximaal beschikbare MySQL-databases in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-104">Azure Database for MySQL is a managed service that enables you toorun, manage, and scale highly available MySQL databases in hello cloud.</span></span> <span data-ttu-id="c6ae7-105">Hello Azure-portal gebruikt, kunt u eenvoudig beheren van uw server en ontwerpen van een database.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-105">Using hello Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="c6ae7-106">In deze zelfstudie gebruikt u Azure portal toolearn Hallo hoe naar:</span><span class="sxs-lookup"><span data-stu-id="c6ae7-106">In this tutorial, you use hello Azure portal toolearn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c6ae7-107">Een Azure-Database maken voor MySQL</span><span class="sxs-lookup"><span data-stu-id="c6ae7-107">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="c6ae7-108">Hallo serverfirewall configureren</span><span class="sxs-lookup"><span data-stu-id="c6ae7-108">Configure hello server firewall</span></span>
> * <span data-ttu-id="c6ae7-109">Gebruik van mysql opdrachtregelprogramma toocreate een database</span><span class="sxs-lookup"><span data-stu-id="c6ae7-109">Use mysql command-line tool toocreate a database</span></span>
> * <span data-ttu-id="c6ae7-110">Voorbeeldgegevens laden</span><span class="sxs-lookup"><span data-stu-id="c6ae7-110">Load sample data</span></span>
> * <span data-ttu-id="c6ae7-111">Querygegevens</span><span class="sxs-lookup"><span data-stu-id="c6ae7-111">Query data</span></span>
> * <span data-ttu-id="c6ae7-112">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="c6ae7-112">Update data</span></span>
> * <span data-ttu-id="c6ae7-113">Gegevens terugzetten</span><span class="sxs-lookup"><span data-stu-id="c6ae7-113">Restore data</span></span>

## <a name="sign-in-toohello-azure-portal"></a><span data-ttu-id="c6ae7-114">Meld u aan toohello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="c6ae7-114">Sign in toohello Azure portal</span></span>
<span data-ttu-id="c6ae7-115">Open uw favoriete webbrowser en Ga naar Hallo [Microsoft Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c6ae7-115">Open your favorite web browser, and visit hello [Microsoft Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="c6ae7-116">Voer uw referenties toosign in toohello-portal.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-116">Enter your credentials toosign in toohello portal.</span></span> <span data-ttu-id="c6ae7-117">Hallo standaardweergave is uw servicedashboard.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-117">hello default view is your service dashboard.</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="c6ae7-118">Een Azure-database voor MySQL-server maken</span><span class="sxs-lookup"><span data-stu-id="c6ae7-118">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="c6ae7-119">Een Azure Database voor MySQL-server wordt gemaakt met een gedefinieerde set [reken- en opslagresources](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="c6ae7-119">An Azure Database for MySQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="c6ae7-120">Hallo-server is gemaakt binnen een [Azure-resourcegroep](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="c6ae7-120">hello server is created within an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span>

1. <span data-ttu-id="c6ae7-121">Navigeer te**Databases** > **Azure Database voor MySQL**.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-121">Navigate too**Databases** > **Azure Database for MySQL**.</span></span> <span data-ttu-id="c6ae7-122">Als u niet kunt vinden MySQL-Server onder **Databases** categorie, klikt u op **alle** tooshow alle beschikbare services-database.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-122">If you cannot find MySQL Server under **Databases** category, click **See all** tooshow all available database services.</span></span> <span data-ttu-id="c6ae7-123">U kunt ook typen **Azure Database voor MySQL** in Hallo zoeken vak tooquickly Hallo service vinden.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-123">You can also type **Azure Database for MySQL** in hello search box tooquickly find hello service.</span></span>
<span data-ttu-id="c6ae7-124">![2-1 navigeren tooMySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span><span class="sxs-lookup"><span data-stu-id="c6ae7-124">![2-1 Navigate tooMySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span></span>

2. <span data-ttu-id="c6ae7-125">Klik op **Azure Database voor MySQL** tegel en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-125">Click **Azure Database for MySQL** tile, and then click **Create**.</span></span>

<span data-ttu-id="c6ae7-126">Vul in ons voorbeeld hello Azure Database voor MySQL formulier Hello volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="c6ae7-126">In our example, fill out hello Azure Database for MySQL form with hello following information:</span></span>

| <span data-ttu-id="c6ae7-127">**Instelling**</span><span class="sxs-lookup"><span data-stu-id="c6ae7-127">**Setting**</span></span> | <span data-ttu-id="c6ae7-128">**Voorgestelde waarde**</span><span class="sxs-lookup"><span data-stu-id="c6ae7-128">**Suggested value**</span></span> | <span data-ttu-id="c6ae7-129">**Beschrijving van veld**</span><span class="sxs-lookup"><span data-stu-id="c6ae7-129">**Field Description**</span></span> |
|---|---|---|
| <span data-ttu-id="c6ae7-130">*Servernaam*</span><span class="sxs-lookup"><span data-stu-id="c6ae7-130">*Server name*</span></span> | <span data-ttu-id="c6ae7-131">myserver4demo</span><span class="sxs-lookup"><span data-stu-id="c6ae7-131">myserver4demo</span></span>  | <span data-ttu-id="c6ae7-132">De servernaam van de heeft toobe globaal uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-132">Server name has toobe globally unique.</span></span> |
| <span data-ttu-id="c6ae7-133">*Abonnement*</span><span class="sxs-lookup"><span data-stu-id="c6ae7-133">*Subscription*</span></span> | <span data-ttu-id="c6ae7-134">mysubscription</span><span class="sxs-lookup"><span data-stu-id="c6ae7-134">mysubscription</span></span> | <span data-ttu-id="c6ae7-135">Uw abonnement te selecteren in de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-135">Select your subscription from hello drop-down.</span></span> |
| <span data-ttu-id="c6ae7-136">*Resourcegroep*</span><span class="sxs-lookup"><span data-stu-id="c6ae7-136">*Resource group*</span></span> | <span data-ttu-id="c6ae7-137">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c6ae7-137">myresourcegroup</span></span> | <span data-ttu-id="c6ae7-138">Maak een nieuwe resourcegroep of selecteer een bestaande.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-138">Create a resource group or use an existing one.</span></span> |
| <span data-ttu-id="c6ae7-139">*Aanmeldgegevens van serverbeheerder*</span><span class="sxs-lookup"><span data-stu-id="c6ae7-139">*Server admin login*</span></span> | <span data-ttu-id="c6ae7-140">myadmin</span><span class="sxs-lookup"><span data-stu-id="c6ae7-140">myadmin</span></span> | <span data-ttu-id="c6ae7-141">Accountnaam van de Setup-beheerder.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-141">Setup admin account name.</span></span> |
| <span data-ttu-id="c6ae7-142">*Wachtwoord*</span><span class="sxs-lookup"><span data-stu-id="c6ae7-142">*Password*</span></span> |  | <span data-ttu-id="c6ae7-143">Stel een wachtwoord voor het beheerdersaccount in.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-143">Set a strong admin account password.</span></span> |
| <span data-ttu-id="c6ae7-144">*Wachtwoord bevestigen*</span><span class="sxs-lookup"><span data-stu-id="c6ae7-144">*Confirm password*</span></span> |  | <span data-ttu-id="c6ae7-145">Hallo beheerder accountwachtwoord bevestigen.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-145">Confirm hello admin account password.</span></span> |
| <span data-ttu-id="c6ae7-146">*Locatie*</span><span class="sxs-lookup"><span data-stu-id="c6ae7-146">*Location*</span></span> |  | <span data-ttu-id="c6ae7-147">Selecteer een beschikbare regio.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-147">Select an available region.</span></span> |
| <span data-ttu-id="c6ae7-148">*Versie*</span><span class="sxs-lookup"><span data-stu-id="c6ae7-148">*Version*</span></span> | <span data-ttu-id="c6ae7-149">5.7</span><span class="sxs-lookup"><span data-stu-id="c6ae7-149">5.7</span></span> | <span data-ttu-id="c6ae7-150">Kies de meest recente versie Hallo.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-150">Choose hello latest version.</span></span> |
| <span data-ttu-id="c6ae7-151">*Prestaties configureren*</span><span class="sxs-lookup"><span data-stu-id="c6ae7-151">*Configure performance*</span></span> | <span data-ttu-id="c6ae7-152">Basis, 50 compute-eenheden, 50 GB</span><span class="sxs-lookup"><span data-stu-id="c6ae7-152">Basic, 50 compute units, 50 GB</span></span>  | <span data-ttu-id="c6ae7-153">Kies **Prijscategorie**, **Rekeneenheden**, **Opslag (GB)** en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-153">Choose **Pricing tier**, **Compute Units**, **Storage (GB)**, and then click **OK**.</span></span> |
| <span data-ttu-id="c6ae7-154">*Pincode tooDashboard*</span><span class="sxs-lookup"><span data-stu-id="c6ae7-154">*Pin tooDashboard*</span></span> | <span data-ttu-id="c6ae7-155">Selecteren</span><span class="sxs-lookup"><span data-stu-id="c6ae7-155">Check</span></span> | <span data-ttu-id="c6ae7-156">Toocheck aanbevolen dit selectievakje in zodat u mogelijk eenvoudig later op Hallo server zoeken</span><span class="sxs-lookup"><span data-stu-id="c6ae7-156">Recommended toocheck this box so you may find hello server easily later on</span></span> |
<span data-ttu-id="c6ae7-157">Klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-157">Then, click **Create**.</span></span> <span data-ttu-id="c6ae7-158">In een minuut of twee, wordt een nieuwe Azure-Database voor de MySQL-server in de cloud Hallo uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-158">In a minute or two, a new Azure Database for MySQL server is running in hello cloud.</span></span> <span data-ttu-id="c6ae7-159">U kunt klikken op **meldingen** knop op Hallo werkbalk toomonitor Hallo-implementatieproces.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-159">You can click **Notifications** button on hello toolbar toomonitor hello deployment process.</span></span>

## <a name="configure-firewall"></a><span data-ttu-id="c6ae7-160">Firewall configureren</span><span class="sxs-lookup"><span data-stu-id="c6ae7-160">Configure firewall</span></span>
<span data-ttu-id="c6ae7-161">Azure voor MySQL-Databases worden beveiligd door een firewall.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-161">Azure Databases for MySQL are protected by a firewall.</span></span> <span data-ttu-id="c6ae7-162">Standaard worden alle verbindingen toohello server- en Hallo databases binnen Hallo server geweigerd.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-162">By default, all connections toohello server and hello databases inside hello server are rejected.</span></span> <span data-ttu-id="c6ae7-163">Voordat u verbinding maakt tooAzure Database voor MySQL voor Hallo eerst, Hallo firewall tooadd Hallo clientmachine van openbare IP-adres (of IP-adresbereik) te configureren.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-163">Before connecting tooAzure Database for MySQL for hello first time, configure hello firewall tooadd hello client machine's public network IP address (or IP address range).</span></span>

1. <span data-ttu-id="c6ae7-164">Klik op de nieuwe virtuele server en klik vervolgens op **verbindingsbeveiliging**.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-164">Click your newly created server, and then click **Connection security**.</span></span>
   <span data-ttu-id="c6ae7-165">![Beveiliging 3-1-verbindingen](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span><span class="sxs-lookup"><span data-stu-id="c6ae7-165">![3-1 Connection security](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span></span>
2. <span data-ttu-id="c6ae7-166">U kunt **Mijn IP toevoegen**, of hier firewallregels configureren.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-166">You can **Add My IP**, or configure firewall rules here.</span></span> <span data-ttu-id="c6ae7-167">Houd er rekening mee tooclick **opslaan** nadat u Hallo regels hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-167">Remember tooclick **Save** after you have created hello rules.</span></span>
<span data-ttu-id="c6ae7-168">U kunt nu verbinding toohello-server met het opdrachtregelprogramma mysql of MySQL Workbench GUI-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-168">You can now connect toohello server using mysql command-line tool or MySQL Workbench GUI tool.</span></span>

> [!TIP]
> <span data-ttu-id="c6ae7-169">Azure-Database voor de MySQL-server communiceert via poort 3306.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-169">Azure Database for MySQL server communicates over port 3306.</span></span> <span data-ttu-id="c6ae7-170">Als u tooconnect van binnen een bedrijfsnetwerk probeert, kan uitgaand verkeer via poort 3306 niet worden toegestaan door de firewall van uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-170">If you are trying tooconnect from within a corporate network, outbound traffic over port 3306 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="c6ae7-171">Als dit het geval is, kunt u tooAzure MySQL-server kan geen verbinding tenzij uw IT-afdeling poort 3306 wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-171">If so, you cannot connect tooAzure MySQL server unless your IT department opens port 3306.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="c6ae7-172">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="c6ae7-172">Get connection information</span></span>
<span data-ttu-id="c6ae7-173">Get-Hallo volledig gekwalificeerd **servernaam** en **aanmeldingsnaam van Server-beheerder** voor uw Azure-Database voor de server MySQL van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-173">Get hello fully qualified **Server name** and **Server admin login name** for your Azure Database for MySQL server from hello Azure portal.</span></span> <span data-ttu-id="c6ae7-174">U gebruikt Hallo server volledig gekwalificeerde naam tooconnect tooyour server met het opdrachtregelprogramma mysql.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-174">You use hello fully qualified server name tooconnect tooyour server using mysql command-line tool.</span></span> 

1. <span data-ttu-id="c6ae7-175">In [Azure-portal](https://portal.azure.com/), klikt u op **alle resources** van menu links van hello, Hallo typenaam en zoeken naar uw Azure-Database voor de MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-175">In [Azure portal](https://portal.azure.com/), click **All resources** from hello left-hand menu, type hello name, and search for your Azure Database for MySQL server.</span></span> <span data-ttu-id="c6ae7-176">Selecteer Hallo naam tooview Hallo-servergegevens.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-176">Select hello server name tooview hello details.</span></span>

2. <span data-ttu-id="c6ae7-177">Onder Hallo instellingen kop, klikt u op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-177">Under hello Settings heading, click **Properties**.</span></span> <span data-ttu-id="c6ae7-178">Noteer **servernaam** en **AANMELDINGSNAAM van SERVER-beheerder**.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-178">Note down **SERVER NAME** and **SERVER ADMIN LOGIN NAME**.</span></span> <span data-ttu-id="c6ae7-179">Klikt u op Hallo knop volgende tooeach veld toocopy toohello Klembord kopiëren.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-179">You may click hello copy button next tooeach field toocopy toohello clipboard.</span></span>
   <span data-ttu-id="c6ae7-180">![Eigenschappen van de server 4-2](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span><span class="sxs-lookup"><span data-stu-id="c6ae7-180">![4-2 server properties](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span></span>

<span data-ttu-id="c6ae7-181">In dit voorbeeld Hallo-servernaam is *myserver4demo.mysql.database.azure.com*, en aanmeldgegevens van serverbeheerder Hallo  *myadmin@myserver4demo* .</span><span class="sxs-lookup"><span data-stu-id="c6ae7-181">In this example, hello server name is *myserver4demo.mysql.database.azure.com*, and hello server admin login is *myadmin@myserver4demo*.</span></span>

## <a name="connect-toohello-server-using-mysql"></a><span data-ttu-id="c6ae7-182">Verbinding maken met behulp van mysql toohello-server</span><span class="sxs-lookup"><span data-stu-id="c6ae7-182">Connect toohello server using mysql</span></span>
<span data-ttu-id="c6ae7-183">Gebruik [mysql opdrachtregelprogramma](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) tooestablish een verbinding tooyour Azure Database voor de MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-183">Use [mysql command-line tool](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) tooestablish a connection tooyour Azure Database for MySQL server.</span></span> <span data-ttu-id="c6ae7-184">U kunt Hallo mysql opdrachtregelprogramma uitvoeren vanuit hello Azure Cloud Shell in Hallo browser of vanuit uw eigen computer lokaal met behulp van mysql-hulpprogramma's geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-184">You can run hello mysql command-line tool from hello Azure Cloud Shell in hello browser or from your own machine using mysql tools installed locally.</span></span> <span data-ttu-id="c6ae7-185">toolaunch hello Azure Cloud-Shell, klikt u op Hallo `Try It` knop op een codeblok in dit artikel of gaat u naar hello Azure-portal en klikt u op Hallo `>_` pictogram in het bovenste rechts werkbalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-185">toolaunch hello Azure Cloud Shell, click hello `Try It` button on a code block in this article, or visit hello Azure portal and click hello `>_` icon in hello top right toolbar.</span></span> 

<span data-ttu-id="c6ae7-186">Hallo opdracht tooconnect typt u:</span><span class="sxs-lookup"><span data-stu-id="c6ae7-186">Type hello command tooconnect:</span></span>
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="c6ae7-187">Een lege database maken</span><span class="sxs-lookup"><span data-stu-id="c6ae7-187">Create a blank database</span></span>
<span data-ttu-id="c6ae7-188">Als u verbonden toohello server bent, maakt u een lege database toowork met.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-188">Once you’re connected toohello server, create a blank database toowork with.</span></span>
```sql
CREATE DATABASE mysampledb;
```

<span data-ttu-id="c6ae7-189">Voer bij Hallo-prompt Hallo opdracht tooswitch verbinding toothis nieuw gemaakte database te volgen:</span><span class="sxs-lookup"><span data-stu-id="c6ae7-189">At hello prompt, run hello following command tooswitch connection toothis newly created database:</span></span>
```sql
USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="c6ae7-190">Tabellen maken in Hallo-database</span><span class="sxs-lookup"><span data-stu-id="c6ae7-190">Create tables in hello database</span></span>
<span data-ttu-id="c6ae7-191">Als u weet hoe tooconnect toohello Azure Database voor de MySQL-database, we kunt gaan om de manier waarop toocomplete sommige basistaken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-191">Now that you know how tooconnect toohello Azure Database for MySQL database, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="c6ae7-192">We kunnen eerst een tabel maken en deze met enkele gegevens te laden.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-192">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="c6ae7-193">We maken een tabel met inventarisatie-informatie.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-193">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="c6ae7-194">Gegevens laden in Hallo tabellen</span><span class="sxs-lookup"><span data-stu-id="c6ae7-194">Load data into hello tables</span></span>
<span data-ttu-id="c6ae7-195">Nu dat we een tabel hebben, kunnen we sommige gegevens invoegen in het.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-195">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="c6ae7-196">Op Hallo open opdrachtpromptvenster, typt u Hallo query tooinsert volgen een aantal rijen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-196">At hello open command prompt window, run hello following query tooinsert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="c6ae7-197">U hebt nu twee rijen van de voorbeeldgegevens in Hallo tabel die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-197">Now you have two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="c6ae7-198">Vragen en het Hallo-gegevens in het Hallo-tabellen bijwerken</span><span class="sxs-lookup"><span data-stu-id="c6ae7-198">Query and update hello data in hello tables</span></span>
<span data-ttu-id="c6ae7-199">Hallo volgende tooretrieve querygegevens uit Hallo-databasetabel worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-199">Execute hello following query tooretrieve information from hello database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="c6ae7-200">U kunt ook Hallo-gegevens in Hallo-tabellen bijwerken.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-200">You can also update hello data in hello tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="c6ae7-201">Hallo rij opgehaald dienovereenkomstig bijgewerkt wanneer u gegevens ophaalt.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-201">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="c6ae7-202">Een database tooa eerder punt herstellen in-time</span><span class="sxs-lookup"><span data-stu-id="c6ae7-202">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="c6ae7-203">Stel dat u een belangrijke databasetabel per ongeluk hebt verwijderd en Hallo gegevens gemakkelijk niet herstellen.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-203">Imagine you have accidentally deleted an important database table, and cannot recover hello data easily.</span></span> <span data-ttu-id="c6ae7-204">Azure MySQL-Database kunt u toorestore Hallo server tooa punt in tijd, het maken van een kopie van Hallo databases in de nieuwe server.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-204">Azure Database for MySQL allows you toorestore hello server tooa point in time, creating a copy of hello databases into new server.</span></span> <span data-ttu-id="c6ae7-205">U kunt deze nieuwe server toorecover uw verwijderde gegevens te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-205">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="c6ae7-206">Hallo na stappen Hallo voorbeeld server tooa herstelpunt voordat Hallo tabel toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-206">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

1. <span data-ttu-id="c6ae7-207">Zoek uw Azure-Database voor MySQL in Azure-portal hello.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-207">In hello Azure portal, locate your Azure Database for MySQL.</span></span> <span data-ttu-id="c6ae7-208">Op Hallo **overzicht** pagina, klikt u op **herstellen** op Hallo-werkbalk.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-208">On hello **Overview** page, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="c6ae7-209">Hallo terugzetten pagina wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-209">hello Restore page opens.</span></span>

   ![10-1 herstel van een database](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. <span data-ttu-id="c6ae7-211">Hallo invullen **herstellen** formulier met Hallo vereiste informatie.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-211">Fill out hello **Restore** form with hello required information.</span></span>
   
   ![10-2-formulier voor herstel](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - <span data-ttu-id="c6ae7-213">**Herstelpunt**: Selecteer een point-in-time-dat u wilt dat toorestore, binnen Hallo tijdsbestek vermeld.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-213">**Restore point**: Select a point-in-time that you want toorestore to, within hello timeframe listed.</span></span> <span data-ttu-id="c6ae7-214">Zorg ervoor dat tooconvert de tooUTC van uw lokale tijdzone.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-214">Make sure tooconvert your local timezone tooUTC.</span></span>
   - <span data-ttu-id="c6ae7-215">**Herstellen van de server toonew**: Geef een nieuwe naam van een server gewenste toorestore aan.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-215">**Restore toonew server**: Provide a new server name you want toorestore to.</span></span>
   - <span data-ttu-id="c6ae7-216">**Locatie**: Hallo regio is hetzelfde als de bronserver Hallo en kan niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-216">**Location**: hello region is same as hello source server, and cannot be changed.</span></span>
   - <span data-ttu-id="c6ae7-217">**Prijscategorie**: Hallo prijscategorie is Hallo dezelfde zijn als Hallo bron van de server en kan niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-217">**Pricing tier**: hello pricing tier is hello same as hello source server, and cannot be changed.</span></span>
   
3. <span data-ttu-id="c6ae7-218">Klik op **OK** toorestore Hallo server te[tooa herstelpunt in de tijd](./howto-restore-server-portal.md) voordat het Hallo-tabel is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-218">Click **OK** toorestore hello server too[restore tooa point in time](./howto-restore-server-portal.md) before hello table was deleted.</span></span> <span data-ttu-id="c6ae7-219">Herstellen van een server, maakt een nieuwe kopie van de server hello, vanaf Hallo punt in tijd die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="c6ae7-219">Restoring a server creates a new copy of hello server, as of hello point in time you specify.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c6ae7-220">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c6ae7-220">Next steps</span></span>
<span data-ttu-id="c6ae7-221">In deze zelfstudie gebruikt u Azure portal toolearned Hallo hoe naar:</span><span class="sxs-lookup"><span data-stu-id="c6ae7-221">In this tutorial, you use hello Azure portal toolearned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c6ae7-222">Een Azure-Database maken voor MySQL</span><span class="sxs-lookup"><span data-stu-id="c6ae7-222">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="c6ae7-223">Hallo serverfirewall configureren</span><span class="sxs-lookup"><span data-stu-id="c6ae7-223">Configure hello server firewall</span></span>
> * <span data-ttu-id="c6ae7-224">Gebruik van mysql opdrachtregelprogramma toocreate een database</span><span class="sxs-lookup"><span data-stu-id="c6ae7-224">Use mysql command-line tool toocreate a database</span></span>
> * <span data-ttu-id="c6ae7-225">Voorbeeldgegevens laden</span><span class="sxs-lookup"><span data-stu-id="c6ae7-225">Load sample data</span></span>
> * <span data-ttu-id="c6ae7-226">Querygegevens</span><span class="sxs-lookup"><span data-stu-id="c6ae7-226">Query data</span></span>
> * <span data-ttu-id="c6ae7-227">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="c6ae7-227">Update data</span></span>
> * <span data-ttu-id="c6ae7-228">Gegevens terugzetten</span><span class="sxs-lookup"><span data-stu-id="c6ae7-228">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c6ae7-229">Hoe tooconnect toepassingen tooAzure voor MySQL-Database</span><span class="sxs-lookup"><span data-stu-id="c6ae7-229">How tooconnect applications tooAzure Database for MySQL</span></span>](./howto-connection-string.md)
