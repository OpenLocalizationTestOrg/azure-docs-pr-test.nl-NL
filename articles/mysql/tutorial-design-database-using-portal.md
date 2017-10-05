---
title: Ontwerp van uw eerste Azure-Database voor de MySQL-database. Azure-Portal | Microsoft Docs
description: Deze zelfstudie wordt uitgelegd hoe maken en beheren van Azure-Database voor MySQL-server en database via Azure Portal.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: c7b76cacbdc4e483353f64cc4e50c974867bb5b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="c5723-103">Ontwerp van uw eerste Azure-Database voor de MySQL-database</span><span class="sxs-lookup"><span data-stu-id="c5723-103">Design your first Azure Database for MySQL database</span></span>
<span data-ttu-id="c5723-104">Azure Database voor MySQL is een beheerde service waarmee u MySQL-databases met hoge beschikbaarheid in de cloud kunt uitvoeren, beheren en schalen.</span><span class="sxs-lookup"><span data-stu-id="c5723-104">Azure Database for MySQL is a managed service that enables you to run, manage, and scale highly available MySQL databases in the cloud.</span></span> <span data-ttu-id="c5723-105">Met de Azure portal, kunt u eenvoudig beheren van uw server en ontwerpen van een database.</span><span class="sxs-lookup"><span data-stu-id="c5723-105">Using the Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="c5723-106">In deze zelfstudie maakt u de Azure portal gebruiken voor meer informatie over hoe:</span><span class="sxs-lookup"><span data-stu-id="c5723-106">In this tutorial, you use the Azure portal to learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c5723-107">Een Azure-Database maken voor MySQL</span><span class="sxs-lookup"><span data-stu-id="c5723-107">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="c5723-108">De serverfirewall configureren</span><span class="sxs-lookup"><span data-stu-id="c5723-108">Configure the server firewall</span></span>
> * <span data-ttu-id="c5723-109">Mysql-opdrachtregelprogramma gebruiken om een database te maken</span><span class="sxs-lookup"><span data-stu-id="c5723-109">Use mysql command-line tool to create a database</span></span>
> * <span data-ttu-id="c5723-110">Voorbeeldgegevens laden</span><span class="sxs-lookup"><span data-stu-id="c5723-110">Load sample data</span></span>
> * <span data-ttu-id="c5723-111">Querygegevens</span><span class="sxs-lookup"><span data-stu-id="c5723-111">Query data</span></span>
> * <span data-ttu-id="c5723-112">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="c5723-112">Update data</span></span>
> * <span data-ttu-id="c5723-113">Gegevens terugzetten</span><span class="sxs-lookup"><span data-stu-id="c5723-113">Restore data</span></span>

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="c5723-114">Aanmelden bij Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c5723-114">Sign in to the Azure portal</span></span>
<span data-ttu-id="c5723-115">Open uw favoriete webbrowser en Ga naar de [Microsoft Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c5723-115">Open your favorite web browser, and visit the [Microsoft Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="c5723-116">Voer uw referenties in om u aan te melden bij de portal.</span><span class="sxs-lookup"><span data-stu-id="c5723-116">Enter your credentials to sign in to the portal.</span></span> <span data-ttu-id="c5723-117">De standaardweergave is uw service-dashboard.</span><span class="sxs-lookup"><span data-stu-id="c5723-117">The default view is your service dashboard.</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="c5723-118">Een Azure-database voor MySQL-server maken</span><span class="sxs-lookup"><span data-stu-id="c5723-118">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="c5723-119">Een Azure Database voor MySQL-server wordt gemaakt met een gedefinieerde set [reken- en opslagresources](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="c5723-119">An Azure Database for MySQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="c5723-120">De server wordt gemaakt in een [Azure-resourcegroep](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="c5723-120">The server is created within an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span>

1. <span data-ttu-id="c5723-121">Navigeer naar **Databases** > **Azure MySQL-Database**.</span><span class="sxs-lookup"><span data-stu-id="c5723-121">Navigate to **Databases** > **Azure Database for MySQL**.</span></span> <span data-ttu-id="c5723-122">Als u niet kunt vinden MySQL-Server onder **Databases** categorie, klikt u op **alle** om alle beschikbare databaseservices weer te geven.</span><span class="sxs-lookup"><span data-stu-id="c5723-122">If you cannot find MySQL Server under **Databases** category, click **See all** to show all available database services.</span></span> <span data-ttu-id="c5723-123">U kunt ook typen **Azure Database voor MySQL** in het zoekvak om snel de service niet vinden.</span><span class="sxs-lookup"><span data-stu-id="c5723-123">You can also type **Azure Database for MySQL** in the search box to quickly find the service.</span></span>
<span data-ttu-id="c5723-124">![2-1, navigeer naar MySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span><span class="sxs-lookup"><span data-stu-id="c5723-124">![2-1 Navigate to MySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span></span>

2. <span data-ttu-id="c5723-125">Klik op **Azure Database voor MySQL** tegel en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="c5723-125">Click **Azure Database for MySQL** tile, and then click **Create**.</span></span>

<span data-ttu-id="c5723-126">Vul in ons voorbeeld wordt de Azure-Database MySQL formulier met de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="c5723-126">In our example, fill out the Azure Database for MySQL form with the following information:</span></span>

| <span data-ttu-id="c5723-127">**Instelling**</span><span class="sxs-lookup"><span data-stu-id="c5723-127">**Setting**</span></span> | <span data-ttu-id="c5723-128">**Voorgestelde waarde**</span><span class="sxs-lookup"><span data-stu-id="c5723-128">**Suggested value**</span></span> | <span data-ttu-id="c5723-129">**Beschrijving van veld**</span><span class="sxs-lookup"><span data-stu-id="c5723-129">**Field Description**</span></span> |
|---|---|---|
| <span data-ttu-id="c5723-130">*Servernaam*</span><span class="sxs-lookup"><span data-stu-id="c5723-130">*Server name*</span></span> | <span data-ttu-id="c5723-131">myserver4demo</span><span class="sxs-lookup"><span data-stu-id="c5723-131">myserver4demo</span></span>  | <span data-ttu-id="c5723-132">Servernaam moet globaal uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="c5723-132">Server name has to be globally unique.</span></span> |
| <span data-ttu-id="c5723-133">*Abonnement*</span><span class="sxs-lookup"><span data-stu-id="c5723-133">*Subscription*</span></span> | <span data-ttu-id="c5723-134">mysubscription</span><span class="sxs-lookup"><span data-stu-id="c5723-134">mysubscription</span></span> | <span data-ttu-id="c5723-135">Selecteer uw abonnement in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="c5723-135">Select your subscription from the drop-down.</span></span> |
| <span data-ttu-id="c5723-136">*Resourcegroep*</span><span class="sxs-lookup"><span data-stu-id="c5723-136">*Resource group*</span></span> | <span data-ttu-id="c5723-137">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c5723-137">myresourcegroup</span></span> | <span data-ttu-id="c5723-138">Maak een nieuwe resourcegroep of selecteer een bestaande.</span><span class="sxs-lookup"><span data-stu-id="c5723-138">Create a resource group or use an existing one.</span></span> |
| <span data-ttu-id="c5723-139">*Aanmeldgegevens van serverbeheerder*</span><span class="sxs-lookup"><span data-stu-id="c5723-139">*Server admin login*</span></span> | <span data-ttu-id="c5723-140">myadmin</span><span class="sxs-lookup"><span data-stu-id="c5723-140">myadmin</span></span> | <span data-ttu-id="c5723-141">Accountnaam van de Setup-beheerder.</span><span class="sxs-lookup"><span data-stu-id="c5723-141">Setup admin account name.</span></span> |
| <span data-ttu-id="c5723-142">*Wachtwoord*</span><span class="sxs-lookup"><span data-stu-id="c5723-142">*Password*</span></span> |  | <span data-ttu-id="c5723-143">Stel een wachtwoord voor het beheerdersaccount in.</span><span class="sxs-lookup"><span data-stu-id="c5723-143">Set a strong admin account password.</span></span> |
| <span data-ttu-id="c5723-144">*Wachtwoord bevestigen*</span><span class="sxs-lookup"><span data-stu-id="c5723-144">*Confirm password*</span></span> |  | <span data-ttu-id="c5723-145">Bevestig het wachtwoord voor het beheerdersaccount.</span><span class="sxs-lookup"><span data-stu-id="c5723-145">Confirm the admin account password.</span></span> |
| <span data-ttu-id="c5723-146">*Locatie*</span><span class="sxs-lookup"><span data-stu-id="c5723-146">*Location*</span></span> |  | <span data-ttu-id="c5723-147">Selecteer een beschikbare regio.</span><span class="sxs-lookup"><span data-stu-id="c5723-147">Select an available region.</span></span> |
| <span data-ttu-id="c5723-148">*Versie*</span><span class="sxs-lookup"><span data-stu-id="c5723-148">*Version*</span></span> | <span data-ttu-id="c5723-149">5.7</span><span class="sxs-lookup"><span data-stu-id="c5723-149">5.7</span></span> | <span data-ttu-id="c5723-150">Kies de nieuwste versie.</span><span class="sxs-lookup"><span data-stu-id="c5723-150">Choose the latest version.</span></span> |
| <span data-ttu-id="c5723-151">*Prestaties configureren*</span><span class="sxs-lookup"><span data-stu-id="c5723-151">*Configure performance*</span></span> | <span data-ttu-id="c5723-152">Basis, 50 compute-eenheden, 50 GB</span><span class="sxs-lookup"><span data-stu-id="c5723-152">Basic, 50 compute units, 50 GB</span></span>  | <span data-ttu-id="c5723-153">Kies **Prijscategorie**, **Rekeneenheden**, **Opslag (GB)** en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c5723-153">Choose **Pricing tier**, **Compute Units**, **Storage (GB)**, and then click **OK**.</span></span> |
| <span data-ttu-id="c5723-154">*Vastmaken aan dashboard*</span><span class="sxs-lookup"><span data-stu-id="c5723-154">*Pin to Dashboard*</span></span> | <span data-ttu-id="c5723-155">Selecteren</span><span class="sxs-lookup"><span data-stu-id="c5723-155">Check</span></span> | <span data-ttu-id="c5723-156">Het is raadzaam dit selectievakje in te schakelen zodat u de server later gemakkelijk kunt terugvinden</span><span class="sxs-lookup"><span data-stu-id="c5723-156">Recommended to check this box so you may find the server easily later on</span></span> |
<span data-ttu-id="c5723-157">Klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="c5723-157">Then, click **Create**.</span></span> <span data-ttu-id="c5723-158">Na een minuut of twee wordt een nieuwe Azure-database voor de MySQL-server uitgevoerd in de cloud.</span><span class="sxs-lookup"><span data-stu-id="c5723-158">In a minute or two, a new Azure Database for MySQL server is running in the cloud.</span></span> <span data-ttu-id="c5723-159">U kunt klikken op **meldingen** op de werkbalk om te controleren van het implementatieproces.</span><span class="sxs-lookup"><span data-stu-id="c5723-159">You can click **Notifications** button on the toolbar to monitor the deployment process.</span></span>

## <a name="configure-firewall"></a><span data-ttu-id="c5723-160">Firewall configureren</span><span class="sxs-lookup"><span data-stu-id="c5723-160">Configure firewall</span></span>
<span data-ttu-id="c5723-161">Azure voor MySQL-Databases worden beveiligd door een firewall.</span><span class="sxs-lookup"><span data-stu-id="c5723-161">Azure Databases for MySQL are protected by a firewall.</span></span> <span data-ttu-id="c5723-162">Standaard worden alle verbindingen met de server en de databases binnen de server geweigerd.</span><span class="sxs-lookup"><span data-stu-id="c5723-162">By default, all connections to the server and the databases inside the server are rejected.</span></span> <span data-ttu-id="c5723-163">Voordat u verbinding maakt met Azure-Database voor MySQL voor de eerste keer, de firewall configureren voor IP-adres van de client-computer openbaar netwerk (of IP-adresbereik) toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c5723-163">Before connecting to Azure Database for MySQL for the first time, configure the firewall to add the client machine's public network IP address (or IP address range).</span></span>

1. <span data-ttu-id="c5723-164">Klik op de nieuwe virtuele server en klik vervolgens op **verbindingsbeveiliging**.</span><span class="sxs-lookup"><span data-stu-id="c5723-164">Click your newly created server, and then click **Connection security**.</span></span>
   <span data-ttu-id="c5723-165">![Beveiliging 3-1-verbindingen](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span><span class="sxs-lookup"><span data-stu-id="c5723-165">![3-1 Connection security](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span></span>
2. <span data-ttu-id="c5723-166">U kunt **Mijn IP toevoegen**, of hier firewallregels configureren.</span><span class="sxs-lookup"><span data-stu-id="c5723-166">You can **Add My IP**, or configure firewall rules here.</span></span> <span data-ttu-id="c5723-167">Vergeet niet op **Opslaan** te klikken nadat u de regels hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c5723-167">Remember to click **Save** after you have created the rules.</span></span>
<span data-ttu-id="c5723-168">U kunt nu verbinding met de server met het opdrachtregelprogramma mysql of MySQL Workbench GUI-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="c5723-168">You can now connect to the server using mysql command-line tool or MySQL Workbench GUI tool.</span></span>

> [!TIP]
> <span data-ttu-id="c5723-169">Azure-Database voor de MySQL-server communiceert via poort 3306.</span><span class="sxs-lookup"><span data-stu-id="c5723-169">Azure Database for MySQL server communicates over port 3306.</span></span> <span data-ttu-id="c5723-170">Als u verbinding probeert te maken vanuit een bedrijfsnetwerk, wordt uitgaand verkeer via poort 3306 mogelijk niet toegestaan door de firewall van uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="c5723-170">If you are trying to connect from within a corporate network, outbound traffic over port 3306 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="c5723-171">Zo ja, u geen verbinding maken met Azure MySQL-server tenzij poort 3306 wordt geopend door uw IT-afdeling.</span><span class="sxs-lookup"><span data-stu-id="c5723-171">If so, you cannot connect to Azure MySQL server unless your IT department opens port 3306.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="c5723-172">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="c5723-172">Get connection information</span></span>
<span data-ttu-id="c5723-173">Ophalen van de volledig gekwalificeerde **servernaam** en **aanmeldingsnaam van Server-beheerder** voor uw Azure-Database voor MySQL-server van de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c5723-173">Get the fully qualified **Server name** and **Server admin login name** for your Azure Database for MySQL server from the Azure portal.</span></span> <span data-ttu-id="c5723-174">De volledig gekwalificeerde servernaam kunt u verbinding met de server met het opdrachtregelprogramma mysql.</span><span class="sxs-lookup"><span data-stu-id="c5723-174">You use the fully qualified server name to connect to your server using mysql command-line tool.</span></span> 

1. <span data-ttu-id="c5723-175">In [Azure-portal](https://portal.azure.com/), klikt u op **alle resources** in het menu links, typ de naam en zoek naar uw Azure-Database voor de MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="c5723-175">In [Azure portal](https://portal.azure.com/), click **All resources** from the left-hand menu, type the name, and search for your Azure Database for MySQL server.</span></span> <span data-ttu-id="c5723-176">Selecteer de naam van de server om de details weer te geven.</span><span class="sxs-lookup"><span data-stu-id="c5723-176">Select the server name to view the details.</span></span>

2. <span data-ttu-id="c5723-177">Onder de instellingen voor de kop, klikt u op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="c5723-177">Under the Settings heading, click **Properties**.</span></span> <span data-ttu-id="c5723-178">Noteer **servernaam** en **AANMELDINGSNAAM van SERVER-beheerder**.</span><span class="sxs-lookup"><span data-stu-id="c5723-178">Note down **SERVER NAME** and **SERVER ADMIN LOGIN NAME**.</span></span> <span data-ttu-id="c5723-179">U mag klikt u op de knop kopiëren naast elk veld naar het Klembord kopiëren.</span><span class="sxs-lookup"><span data-stu-id="c5723-179">You may click the copy button next to each field to copy to the clipboard.</span></span>
   <span data-ttu-id="c5723-180">![Eigenschappen van de server 4-2](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span><span class="sxs-lookup"><span data-stu-id="c5723-180">![4-2 server properties](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span></span>

<span data-ttu-id="c5723-181">In dit voorbeeld is de servernaam *myserver4demo.mysql.database.azure.com* en de aanmeldgegevens van de serverbeheerder zijn *myadmin@myserver4demo*.</span><span class="sxs-lookup"><span data-stu-id="c5723-181">In this example, the server name is *myserver4demo.mysql.database.azure.com*, and the server admin login is *myadmin@myserver4demo*.</span></span>

## <a name="connect-to-the-server-using-mysql"></a><span data-ttu-id="c5723-182">Verbinding maken met de server met behulp van mysql</span><span class="sxs-lookup"><span data-stu-id="c5723-182">Connect to the server using mysql</span></span>
<span data-ttu-id="c5723-183">Gebruik het [opdrachtregelprogramma mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) om een verbinding tot stand te brengen met uw Azure-database voor MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="c5723-183">Use [mysql command-line tool](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) to establish a connection to your Azure Database for MySQL server.</span></span> <span data-ttu-id="c5723-184">U kunt het opdrachtregelhulpprogramma mysql uitvoeren vanuit de Azure-Cloud-Shell in de browser of vanuit uw eigen computer lokaal met behulp van mysql-hulpprogramma's geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="c5723-184">You can run the mysql command-line tool from the Azure Cloud Shell in the browser or from your own machine using mysql tools installed locally.</span></span> <span data-ttu-id="c5723-185">Start de Azure-Cloud-Shell, klikt u op de `Try It` op een codeblok in dit artikel of Ga naar de Azure-portal en klik op de `>_` pictogram in de bovenste werkbalk rechts.</span><span class="sxs-lookup"><span data-stu-id="c5723-185">To launch the Azure Cloud Shell, click the `Try It` button on a code block in this article, or visit the Azure portal and click the `>_` icon in the top right toolbar.</span></span> 

<span data-ttu-id="c5723-186">Typ de opdracht voor verbinding:</span><span class="sxs-lookup"><span data-stu-id="c5723-186">Type the command to connect:</span></span>
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="c5723-187">Een lege database maken</span><span class="sxs-lookup"><span data-stu-id="c5723-187">Create a blank database</span></span>
<span data-ttu-id="c5723-188">Als u met de server verbonden bent, een lege database maken voor gebruik met.</span><span class="sxs-lookup"><span data-stu-id="c5723-188">Once you’re connected to the server, create a blank database to work with.</span></span>
```sql
CREATE DATABASE mysampledb;
```

<span data-ttu-id="c5723-189">Voer de volgende opdracht verbinding overschakelen naar de nieuwe database op de opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="c5723-189">At the prompt, run the following command to switch connection to this newly created database:</span></span>
```sql
USE mysampledb;
```

## <a name="create-tables-in-the-database"></a><span data-ttu-id="c5723-190">Tabellen maken in de database</span><span class="sxs-lookup"><span data-stu-id="c5723-190">Create tables in the database</span></span>
<span data-ttu-id="c5723-191">Nu dat u hoe u verbinding maken met de Azure-Database voor de MySQL-database weet, kunnen we gaan over hoe u enkele eenvoudige taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c5723-191">Now that you know how to connect to the Azure Database for MySQL database, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="c5723-192">We kunnen eerst een tabel maken en deze met enkele gegevens te laden.</span><span class="sxs-lookup"><span data-stu-id="c5723-192">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="c5723-193">We maken een tabel met inventarisatie-informatie.</span><span class="sxs-lookup"><span data-stu-id="c5723-193">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="c5723-194">Gegevens laden in de tabellen</span><span class="sxs-lookup"><span data-stu-id="c5723-194">Load data into the tables</span></span>
<span data-ttu-id="c5723-195">Nu dat we een tabel hebben, kunnen we sommige gegevens invoegen in het.</span><span class="sxs-lookup"><span data-stu-id="c5723-195">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="c5723-196">Voer de volgende query voor het invoegen van een aantal rijen van de gegevens in het venster opdrachtprompt openen.</span><span class="sxs-lookup"><span data-stu-id="c5723-196">At the open command prompt window, run the following query to insert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="c5723-197">U hebt nu twee rijen van de voorbeeldgegevens in de tabel die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c5723-197">Now you have two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="c5723-198">Vragen en de gegevens in de tabellen bijwerken</span><span class="sxs-lookup"><span data-stu-id="c5723-198">Query and update the data in the tables</span></span>
<span data-ttu-id="c5723-199">De volgende query om informatie te halen uit de databasetabel.</span><span class="sxs-lookup"><span data-stu-id="c5723-199">Execute the following query to retrieve information from the database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="c5723-200">U kunt ook de gegevens in de tabellen bijwerken.</span><span class="sxs-lookup"><span data-stu-id="c5723-200">You can also update the data in the tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="c5723-201">De rij wordt dienovereenkomstig bijgewerkt wanneer u gegevens ophaalt.</span><span class="sxs-lookup"><span data-stu-id="c5723-201">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="c5723-202">Een database herstellen naar een eerder tijdstip</span><span class="sxs-lookup"><span data-stu-id="c5723-202">Restore a database to a previous point in time</span></span>
<span data-ttu-id="c5723-203">Stel dat u een belangrijke databasetabel per ongeluk hebt verwijderd en de gegevens niet gemakkelijk kan niet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="c5723-203">Imagine you have accidentally deleted an important database table, and cannot recover the data easily.</span></span> <span data-ttu-id="c5723-204">Azure MySQL-Database kunt u de server te herstellen naar een punt in tijd, het maken van een kopie van de databases in de nieuwe server.</span><span class="sxs-lookup"><span data-stu-id="c5723-204">Azure Database for MySQL allows you to restore the server to a point in time, creating a copy of the databases into new server.</span></span> <span data-ttu-id="c5723-205">U kunt deze nieuwe server gebruiken om uw verwijderde gegevens te herstellen.</span><span class="sxs-lookup"><span data-stu-id="c5723-205">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="c5723-206">Voordat u de tabel is toegevoegd, de volgende stappen uit de voorbeeldserver herstellen naar een punt.</span><span class="sxs-lookup"><span data-stu-id="c5723-206">The following steps restore the sample server to a point before the table was added.</span></span>

1. <span data-ttu-id="c5723-207">Zoek uw Azure-Database voor MySQL in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c5723-207">In the Azure portal, locate your Azure Database for MySQL.</span></span> <span data-ttu-id="c5723-208">Op de **overzicht** pagina, klikt u op **herstellen** op de werkbalk.</span><span class="sxs-lookup"><span data-stu-id="c5723-208">On the **Overview** page, click **Restore** on the toolbar.</span></span> <span data-ttu-id="c5723-209">De pagina voor herstel wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="c5723-209">The Restore page opens.</span></span>

   ![10-1 herstel van een database](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. <span data-ttu-id="c5723-211">Vul de **herstellen** formulier met de vereiste informatie.</span><span class="sxs-lookup"><span data-stu-id="c5723-211">Fill out the **Restore** form with the required information.</span></span>
   
   ![10-2-formulier voor herstel](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - <span data-ttu-id="c5723-213">**Herstelpunt**: Selecteer een point-in-time die u herstellen wilt, binnen de periode die wordt vermeld.</span><span class="sxs-lookup"><span data-stu-id="c5723-213">**Restore point**: Select a point-in-time that you want to restore to, within the timeframe listed.</span></span> <span data-ttu-id="c5723-214">Zorg ervoor dat uw lokale tijdzone converteren naar UTC.</span><span class="sxs-lookup"><span data-stu-id="c5723-214">Make sure to convert your local timezone to UTC.</span></span>
   - <span data-ttu-id="c5723-215">**Herstellen naar de nieuwe server**: Geef een nieuwe servernaam die u wilt herstellen.</span><span class="sxs-lookup"><span data-stu-id="c5723-215">**Restore to new server**: Provide a new server name you want to restore to.</span></span>
   - <span data-ttu-id="c5723-216">**Locatie**: de regio is hetzelfde als de bronserver en kan niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="c5723-216">**Location**: The region is same as the source server, and cannot be changed.</span></span>
   - <span data-ttu-id="c5723-217">**Prijscategorie**: de prijscategorie is hetzelfde als de bronserver en kan niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="c5723-217">**Pricing tier**: The pricing tier is the same as the source server, and cannot be changed.</span></span>
   
3. <span data-ttu-id="c5723-218">Klik op **OK** de server te herstellen [herstellen naar een punt in tijd](./howto-restore-server-portal.md) voordat de tabel is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c5723-218">Click **OK** to restore the server to [restore to a point in time](./howto-restore-server-portal.md) before the table was deleted.</span></span> <span data-ttu-id="c5723-219">Herstellen van een server, maakt een nieuwe kopie van de server, vanaf het punt in tijd die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="c5723-219">Restoring a server creates a new copy of the server, as of the point in time you specify.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c5723-220">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c5723-220">Next steps</span></span>
<span data-ttu-id="c5723-221">In deze zelfstudie gebruikt u de Azure portal naar geleerde how to:</span><span class="sxs-lookup"><span data-stu-id="c5723-221">In this tutorial, you use the Azure portal to learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c5723-222">Een Azure-Database maken voor MySQL</span><span class="sxs-lookup"><span data-stu-id="c5723-222">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="c5723-223">De serverfirewall configureren</span><span class="sxs-lookup"><span data-stu-id="c5723-223">Configure the server firewall</span></span>
> * <span data-ttu-id="c5723-224">Mysql-opdrachtregelprogramma gebruiken om een database te maken</span><span class="sxs-lookup"><span data-stu-id="c5723-224">Use mysql command-line tool to create a database</span></span>
> * <span data-ttu-id="c5723-225">Voorbeeldgegevens laden</span><span class="sxs-lookup"><span data-stu-id="c5723-225">Load sample data</span></span>
> * <span data-ttu-id="c5723-226">Querygegevens</span><span class="sxs-lookup"><span data-stu-id="c5723-226">Query data</span></span>
> * <span data-ttu-id="c5723-227">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="c5723-227">Update data</span></span>
> * <span data-ttu-id="c5723-228">Gegevens terugzetten</span><span class="sxs-lookup"><span data-stu-id="c5723-228">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c5723-229">Verbinding maken tussen toepassingen met Azure-Database voor MySQL</span><span class="sxs-lookup"><span data-stu-id="c5723-229">How to connect applications to Azure Database for MySQL</span></span>](./howto-connection-string.md)
