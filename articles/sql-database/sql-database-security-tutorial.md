---
title: Beveiligen van uw Azure SQL database | Microsoft Docs
description: Meer informatie over de technieken en functies voor het beveiligen van uw Azure SQL database.
services: sql-database
documentationcenter: 
author: DRediske
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/28/2017
ms.author: daredis
ms.openlocfilehash: 4bc09ad13ed0c9dc9257e9c75ec6f9ff3d689a0b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="secure-your-azure-sql-database"></a><span data-ttu-id="e606f-103">Beveiligen van uw Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="e606f-103">Secure your Azure SQL Database</span></span>

<span data-ttu-id="e606f-104">Uw gegevens worden beveiligd met SQL Database door de toegang tot uw database te beperken met behulp van firewallregels, verificatiemechanismen die vereisen dat gebruikers hun identiteit bewijzen, en autorisatie voor gegevens via lidmaatschappen en machtigingen op basis van rollen. Ook wordt gebruikgemaakt van beveiliging op rijniveau en dynamische gegevensmaskering.</span><span class="sxs-lookup"><span data-stu-id="e606f-104">SQL Database secures your data by limiting access to your database using firewall rules, authentication mechanisms requiring users to prove their identity, and authorization to data through role-based memberships and permissions, as well as through row-level security and dynamic data masking.</span></span>

<span data-ttu-id="e606f-105">U kunt de beveiliging van uw database tegen kwaadwillende gebruikers of onbevoegde toegang met een paar eenvoudige stappen kunt verbeteren.</span><span class="sxs-lookup"><span data-stu-id="e606f-105">You can improve the protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="e606f-106">In deze zelfstudie leert u naar:</span><span class="sxs-lookup"><span data-stu-id="e606f-106">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="e606f-107">Niveau van de server firewallregels voor uw server in de Azure-portal instellen</span><span class="sxs-lookup"><span data-stu-id="e606f-107">Set up server-level firewall rules for your server in the Azure portal</span></span>
> * <span data-ttu-id="e606f-108">Regels voor uw database met behulp van SSMS firewallregel op databaseniveau instellen</span><span class="sxs-lookup"><span data-stu-id="e606f-108">Set up database-level firewall rules for your database using SSMS</span></span>
> * <span data-ttu-id="e606f-109">Verbinding maken met uw database met behulp van een beveiligde verbindingsreeks</span><span class="sxs-lookup"><span data-stu-id="e606f-109">Connect to your database using a secure connection string</span></span>
> * <span data-ttu-id="e606f-110">Gebruikerstoegang beheren</span><span class="sxs-lookup"><span data-stu-id="e606f-110">Manage user access</span></span>
> * <span data-ttu-id="e606f-111">Uw gegevens beschermen met versleuteling</span><span class="sxs-lookup"><span data-stu-id="e606f-111">Protect your data with encryption</span></span>
> * <span data-ttu-id="e606f-112">Inschakelen van controle voor SQL-Database</span><span class="sxs-lookup"><span data-stu-id="e606f-112">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="e606f-113">Detectie van dreigingen SQL-Database inschakelen</span><span class="sxs-lookup"><span data-stu-id="e606f-113">Enable SQL Database threat detection</span></span>

<span data-ttu-id="e606f-114">Als u een Azure-abonnement geen [een gratis account maken](https://azure.microsoft.com/free/) voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="e606f-114">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e606f-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e606f-115">Prerequisites</span></span>

<span data-ttu-id="e606f-116">Voor het voltooien van deze zelfstudie, zorg ervoor dat u hebt het volgende:</span><span class="sxs-lookup"><span data-stu-id="e606f-116">To complete this tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="e606f-117">De nieuwste versie van geïnstalleerd [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="e606f-117">Installed the newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span> 
- <span data-ttu-id="e606f-118">Geïnstalleerde Microsoft Excel</span><span class="sxs-lookup"><span data-stu-id="e606f-118">Installed Microsoft Excel</span></span>
- <span data-ttu-id="e606f-119">Zie gemaakt van een Azure SQL-server en database - [maken van een Azure SQL database in de Azure portal](sql-database-get-started-portal.md), [maken van één Azure SQL database met de Azure CLI](sql-database-get-started-cli.md), en [maken van een enkele Azure SQL de database met behulp van PowerShell](sql-database-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e606f-119">Created an Azure SQL server and database - See [Create an Azure SQL database in the Azure portal](sql-database-get-started-portal.md), [Create a single Azure SQL database using the Azure CLI](sql-database-get-started-cli.md), and [Create a single Azure SQL database using PowerShell](sql-database-get-started-powershell.md).</span></span> 

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="e606f-120">Aanmelden bij Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e606f-120">Log in to the Azure portal</span></span>

<span data-ttu-id="e606f-121">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e606f-121">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="e606f-122">Een serverfirewallregel maken in Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e606f-122">Create a server-level firewall rule in the Azure portal</span></span>

<span data-ttu-id="e606f-123">SQL-databases worden beveiligd door een firewall in Azure.</span><span class="sxs-lookup"><span data-stu-id="e606f-123">SQL databases are protected by a firewall in Azure.</span></span> <span data-ttu-id="e606f-124">Standaard worden alle verbindingen met de server en de databases binnen de server geweigerd, met uitzondering van verbindingen met andere Azure-services.</span><span class="sxs-lookup"><span data-stu-id="e606f-124">By default, all connections to the server and the databases inside the server are rejected except for connections from other Azure services.</span></span> <span data-ttu-id="e606f-125">Zie voor meer informatie [Azure SQL Database server- en databaseniveau firewallregels](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e606f-125">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="e606f-126">De veiligste configuratie is 'Toegang tot Azure-services toestaan' op OFF instellen.</span><span class="sxs-lookup"><span data-stu-id="e606f-126">The most secure configuration is to set 'Allow access to Azure services' to OFF.</span></span> <span data-ttu-id="e606f-127">Als u verbinding maken met de database vanaf een virtuele machine in Azure of cloud-service wilt, moet u een [gereserveerde IP-adres](../virtual-network/virtual-networks-reserved-public-ip.md) en alleen de gereserveerde IP-adres toegang toestaan via de firewall.</span><span class="sxs-lookup"><span data-stu-id="e606f-127">If you need to connect to the database from an Azure VM or cloud service, you should create a [Reserved IP](../virtual-network/virtual-networks-reserved-public-ip.md) and allow only the reserved IP address access through the firewall.</span></span> 

<span data-ttu-id="e606f-128">Volg deze stappen voor het maken van een [SQL-Database firewallregel op serverniveau](sql-database-firewall-configure.md) voor uw server verbindingen van een specifiek IP-adres wilt toestaan.</span><span class="sxs-lookup"><span data-stu-id="e606f-128">Follow these steps to create a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your server to allow connections from a specific IP address.</span></span> 

> [!NOTE]
> <span data-ttu-id="e606f-129">Als u een voorbeelddatabase in Azure met behulp van een van de vorige zelfstudies of snelstartgidsen hebt gemaakt en deze zelfstudie op een computer met hetzelfde IP-adres hebben uitvoert wanneer u deze zelfstudie hebt doorlopen, kunt u deze stap overslaan als u al maken hebt hand een firewallregel op serverniveau.</span><span class="sxs-lookup"><span data-stu-id="e606f-129">If you have created a sample database in Azure using one of the previous tutorials or quickstarts and are performing this tutorial on a computer with the same IP address that it had when you walked through those tutorials, you can skip this step as you will have already created a server-level firewall rule.</span></span>
>

1. <span data-ttu-id="e606f-130">Klik op **SQL-databases** vanaf de linkerkant en klik op de database die u wilt configureren, de firewall-regel voor op de **SQL-databases** pagina.</span><span class="sxs-lookup"><span data-stu-id="e606f-130">Click **SQL databases** from the left-hand menu and click the database you would like to configure the firewall rule for on the **SQL databases** page.</span></span> <span data-ttu-id="e606f-131">De overzichtspagina voor uw database wordt geopend, waarin u de volledig gekwalificeerde servernaam (zoals **mynewserver 20170313.database.windows.net**) en biedt opties voor verdere configuratie.</span><span class="sxs-lookup"><span data-stu-id="e606f-131">The overview page for your database opens, showing you the fully qualified server name (such as **mynewserver-20170313.database.windows.net**) and provides options for further configuration.</span></span>

      ![serverfirewallregel](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. <span data-ttu-id="e606f-133">Klik op de werkbalk op **Serverfirewall instellen** zoals in de vorige afbeelding is weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e606f-133">Click **Set server firewall** on the toolbar as shown in the previous image.</span></span> <span data-ttu-id="e606f-134">De pagina **Firewallinstellingen** voor de SQL Database-server wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="e606f-134">The **Firewall settings** page for the SQL Database server opens.</span></span> 

3. <span data-ttu-id="e606f-135">Klik op **client-IP toevoegen** op de werkbalk om het openbare IP-adres van de computer die is verbonden met de portal met toevoegen of de firewallregel handmatig invoeren en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e606f-135">Click **Add client IP** on the toolbar to add the public IP address of the computer connected to the portal with or enter the firewall rule manually and then click **Save**.</span></span>

      ![serverfirewallregel instellen](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. <span data-ttu-id="e606f-137">Klik op **OK** en vervolgens op **X** om de pagina **Firewallinstellingen** te sluiten.</span><span class="sxs-lookup"><span data-stu-id="e606f-137">Click **OK** and then click the **X** to close the **Firewall settings** page.</span></span>

<span data-ttu-id="e606f-138">U kunt nu verbinding met een database in de server met de opgegeven IP-adres of IP-adresbereik.</span><span class="sxs-lookup"><span data-stu-id="e606f-138">You can now connect to any database in the server with the specified IP address or IP address range.</span></span>

> [!NOTE]
> <span data-ttu-id="e606f-139">SQL Database communiceert via poort 1433.</span><span class="sxs-lookup"><span data-stu-id="e606f-139">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="e606f-140">Als u verbinding probeert te maken vanuit een bedrijfsnetwerk, wordt uitgaand verkeer via poort 1433 mogelijk niet toegestaan door de firewall van uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="e606f-140">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="e606f-141">In dat geval kunt u alleen verbinding maken met uw Azure SQL Database-server als uw IT-afdeling poort 1433 openstelt.</span><span class="sxs-lookup"><span data-stu-id="e606f-141">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a><span data-ttu-id="e606f-142">Een firewallregel op databaseniveau met behulp van SSMS maken</span><span class="sxs-lookup"><span data-stu-id="e606f-142">Create a database-level firewall rule using SSMS</span></span>

<span data-ttu-id="e606f-143">Firewallregel op databaseniveau regels kunt u verschillende firewall-instellingen voor verschillende databases binnen dezelfde logische server maken en te maken van de firewall-regels die draagbare zijn-wat betekent dat ze volgt u de database tijdens een [failover](sql-database-geo-replication-overview.md) in plaats van op de SQL-server worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="e606f-143">Database-level firewall rules enable you to create different firewall settings for different databases within the same logical server and to create firewall rules that are portable - meaning that they follow the database during a [failover](sql-database-geo-replication-overview.md) rather than being stored on the SQL server.</span></span> <span data-ttu-id="e606f-144">Firewallregels databaseniveau kunnen alleen worden geconfigureerd met behulp van Transact-SQL-instructies en alleen nadat u de eerste niveau van de server-firewallregel hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="e606f-144">Database-level firewall rules can only be configured by using Transact-SQL statements and only after you have configured the first server-level firewall rule.</span></span> <span data-ttu-id="e606f-145">Zie voor meer informatie [Azure SQL Database server- en databaseniveau firewallregels](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e606f-145">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="e606f-146">Volg deze stappen voor het maken van een database-specifieke firewallregel.</span><span class="sxs-lookup"><span data-stu-id="e606f-146">Follows these steps to create a database-specific firewall rule.</span></span>

1. <span data-ttu-id="e606f-147">Verbinding maken met uw database, bijvoorbeeld met behulp van [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="e606f-147">Connect to your database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span></span>

2. <span data-ttu-id="e606f-148">In Object Explorer met de rechtermuisknop op de database die u wilt een firewallregel voor toevoegen en klik op **nieuwe Query**.</span><span class="sxs-lookup"><span data-stu-id="e606f-148">In Object Explorer, right-click on the database you want to add a firewall rule for and click **New Query**.</span></span> <span data-ttu-id="e606f-149">Er wordt een leeg queryvenster geopend dat is verbonden met uw database.</span><span class="sxs-lookup"><span data-stu-id="e606f-149">A blank query window opens that is connected to your database.</span></span>

3. <span data-ttu-id="e606f-150">Het IP-adres van uw openbare IP-adres wijzigen en vervolgens de volgende query wordt uitgevoerd in het queryvenster:</span><span class="sxs-lookup"><span data-stu-id="e606f-150">In the query window, modify the IP address to your public IP address and then execute the following query:</span></span>

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. <span data-ttu-id="e606f-151">Klik op de werkbalk op **Execute** om de firewallregel te maken.</span><span class="sxs-lookup"><span data-stu-id="e606f-151">On the toolbar, click **Execute** to create the firewall rule.</span></span>

## <a name="view-how-to-connect-an-application-to-your-database-using-a-secure-connection-string"></a><span data-ttu-id="e606f-152">Verbinding maken tussen een toepassing met de database met behulp van een beveiligde verbindingsreeks weergeven</span><span class="sxs-lookup"><span data-stu-id="e606f-152">View how to connect an application to your database using a secure connection string</span></span>

<span data-ttu-id="e606f-153">Een beveiligde, gecodeerde verbinding tussen een client-toepassing en de SQL-Database, zodat heeft de verbindingsreeks om te worden geconfigureerd:</span><span class="sxs-lookup"><span data-stu-id="e606f-153">To ensure a secure, encrypted connection between a client application and SQL Database, the connection string has to be configured to:</span></span>

- <span data-ttu-id="e606f-154">Aanvragen van een versleutelde verbinding, en</span><span class="sxs-lookup"><span data-stu-id="e606f-154">Request an encrypted connection, and</span></span>
- <span data-ttu-id="e606f-155">Het servercertificaat niet vertrouwen.</span><span class="sxs-lookup"><span data-stu-id="e606f-155">To not trust the server certificate.</span></span> 

<span data-ttu-id="e606f-156">Dit een verbinding maken met behulp van Transport Layer Security (TLS) en vermindert het risico van man-in-the-middle-aanvallen.</span><span class="sxs-lookup"><span data-stu-id="e606f-156">This establishes a connection using Transport Layer Security (TLS) and reduces the risk of man-in-the-middle attacks.</span></span> <span data-ttu-id="e606f-157">U kunt verkrijgen juist geconfigureerde verbindingsreeksen voor uw SQL-Database voor ondersteunde client stuurprogramma's vanuit de Azure-portal zoals weergegeven voor ADO.net in deze schermafbeelding.</span><span class="sxs-lookup"><span data-stu-id="e606f-157">You can obtain correctly configured connection strings for your SQL Database for supported client drivers from the Azure portal as shown for ADO.net in this screenshot.</span></span>

1. <span data-ttu-id="e606f-158">Selecteer **SQL-databases** in het menu links, en klikt u op uw database in de **SQL-databases** pagina.</span><span class="sxs-lookup"><span data-stu-id="e606f-158">Select **SQL databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span>

2. <span data-ttu-id="e606f-159">Op de **overzicht** pagina voor uw database, klikt u op **databaseverbindingsreeksen tonen**.</span><span class="sxs-lookup"><span data-stu-id="e606f-159">On the **Overview** page for your database, click **Show database connection strings**.</span></span>

3. <span data-ttu-id="e606f-160">Bekijk de volledige **ADO.NET**-verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="e606f-160">Review the complete **ADO.NET** connection string.</span></span>

    ![ADO.NET-verbindingsreeks](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a><span data-ttu-id="e606f-162">Databasegebruikers te maken</span><span class="sxs-lookup"><span data-stu-id="e606f-162">Creating database users</span></span>

<span data-ttu-id="e606f-163">Voordat u alle gebruikers, moet u eerst kiezen uit twee soorten verificatie wordt ondersteund door Azure SQL Database:</span><span class="sxs-lookup"><span data-stu-id="e606f-163">Before creating any users, you must first choose from one of two authentication types supported by Azure SQL Database:</span></span> 

<span data-ttu-id="e606f-164">**SQL-verificatie**, die gebruikmaakt van gebruikersnaam en wachtwoord voor aanmeldingen en gebruikers die alleen geldig in de context van een bepaalde database binnen een logische server zijn.</span><span class="sxs-lookup"><span data-stu-id="e606f-164">**SQL Authentication**, which uses username and password for logins and users that are valid only in the context of a specific database within a logical server.</span></span> 

<span data-ttu-id="e606f-165">**Azure Active Directory-verificatie**, waarbij identiteiten die worden beheerd door Azure Active Directory wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e606f-165">**Azure Active Directory Authentication**, which uses identities managed by Azure Active Directory.</span></span> 

<span data-ttu-id="e606f-166">Als u wilt gebruiken [Azure Active Directory](./sql-database-aad-authentication.md) om te verifiëren op SQL-Database, een ingevuld Azure Active Directory moet bestaan voordat u verder kunt gaan.</span><span class="sxs-lookup"><span data-stu-id="e606f-166">If you want to use [Azure Active Directory](./sql-database-aad-authentication.md) to authenticate against SQL Database, a populated Azure Active Directory must exist before you can proceed.</span></span>

<span data-ttu-id="e606f-167">Volg deze stappen voor het maken van een gebruiker via SQL-verificatie:</span><span class="sxs-lookup"><span data-stu-id="e606f-167">Follow these steps to create a user using SQL Authentication:</span></span>

1. <span data-ttu-id="e606f-168">Verbinding maken met uw database, bijvoorbeeld met behulp van [SQL Server Management Studio](./sql-database-connect-query-ssms.md) met uw beheerdersreferenties voor de server.</span><span class="sxs-lookup"><span data-stu-id="e606f-168">Connect to your database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) using your server admin credentials.</span></span>

2. <span data-ttu-id="e606f-169">In Object Explorer met de rechtermuisknop op de database die u wilt een nieuwe gebruiker toevoegen aan en klik op **nieuwe Query**.</span><span class="sxs-lookup"><span data-stu-id="e606f-169">In Object Explorer, right-click on the database you want to add a new user on and click **New Query**.</span></span> <span data-ttu-id="e606f-170">Een lege queryvenster wordt geopend die is verbonden met de geselecteerde database.</span><span class="sxs-lookup"><span data-stu-id="e606f-170">A blank query window opens that is connected to the selected database.</span></span>

3. <span data-ttu-id="e606f-171">Voer de volgende query in het queryvenster in:</span><span class="sxs-lookup"><span data-stu-id="e606f-171">In the query window, enter the following query:</span></span>

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. <span data-ttu-id="e606f-172">Klik op de werkbalk op **Execute** voor het maken van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="e606f-172">On the toolbar, click **Execute** to create the user.</span></span>

5. <span data-ttu-id="e606f-173">Standaard wordt in de gebruiker verbinding kan maken met de database, maar heeft geen machtigingen om te lezen of schrijven van gegevens.</span><span class="sxs-lookup"><span data-stu-id="e606f-173">By default, the user can connect to the database, but has no permissions to read or write data.</span></span> <span data-ttu-id="e606f-174">Als u wilt deze machtigingen verlenen voor de nieuwe gebruiker, de volgende twee opdrachten in een nieuwe queryvenster uitvoeren</span><span class="sxs-lookup"><span data-stu-id="e606f-174">To grant these permissions to the newly created user, execute the following two commands in a new query window</span></span>

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

<span data-ttu-id="e606f-175">Het is best practice voor het maken van deze accounts niet-beheerders op databaseniveau verbinding maken met uw database, tenzij u beheerderstaken moet zoals het maken van nieuwe gebruikers uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e606f-175">It is best practice to create these non-administrator accounts at the database level to connect to your database unless you need to execute administrator tasks like creating new users.</span></span> <span data-ttu-id="e606f-176">Controleer de [Azure Active Directory-zelfstudie](./sql-database-aad-authentication-configure.md) over het verifiëren met behulp van Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e606f-176">Please review the [Azure Active Directory tutorial](./sql-database-aad-authentication-configure.md) on how to authenticate using Azure Active Directory.</span></span>


## <a name="protect-your-data-with-encryption"></a><span data-ttu-id="e606f-177">Uw gegevens beschermen met versleuteling</span><span class="sxs-lookup"><span data-stu-id="e606f-177">Protect your data with encryption</span></span>

<span data-ttu-id="e606f-178">Azure SQL Database transparante gegevensversleuteling (TDE) versleutelt uw gegevens in rust, automatisch zonder wijzigingen aan de toepassing toegang tot de versleutelde database.</span><span class="sxs-lookup"><span data-stu-id="e606f-178">Azure SQL Database transparent data encryption (TDE) automatically encrypts your data at rest, without requiring any changes to the application accessing the encrypted database.</span></span> <span data-ttu-id="e606f-179">Voor nieuwe databases is TDE standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e606f-179">For newly created databases, TDE is on by default.</span></span> <span data-ttu-id="e606f-180">Ga als volgt TDE inschakelen voor uw database of om te controleren of TDE op:</span><span class="sxs-lookup"><span data-stu-id="e606f-180">To enable TDE for your database or to verify that TDE is on, follow these steps:</span></span>

1. <span data-ttu-id="e606f-181">Selecteer **SQL-databases** in het menu links, en klikt u op uw database in de **SQL-databases** pagina.</span><span class="sxs-lookup"><span data-stu-id="e606f-181">Select **SQL databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 

2. <span data-ttu-id="e606f-182">Klik op **transparante gegevensversleuteling** de configuratiepagina voor TDE openen.</span><span class="sxs-lookup"><span data-stu-id="e606f-182">Click on **Transparent data encryption** to open the configuration page for TDE.</span></span>

    ![Transparante gegevensversleuteling](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. <span data-ttu-id="e606f-184">Indien nodig stelt **gegevensversleuteling** op ON en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e606f-184">If necessary, set **Data encryption** to ON and click **Save**.</span></span>

<span data-ttu-id="e606f-185">Het versleutelingsproces wordt gestart op de achtergrond.</span><span class="sxs-lookup"><span data-stu-id="e606f-185">The encryption process starts in the background.</span></span> <span data-ttu-id="e606f-186">U kunt de voortgang controleren door verbinding te maken voor het gebruik van SQL-Database [SQL Server Management Studio](./sql-database-connect-query-ssms.md) door het opvragen van de kolom encryption_state van de `sys.dm_database_encryption_keys` weergeven.</span><span class="sxs-lookup"><span data-stu-id="e606f-186">You can monitor the progress by connecting to SQL Database using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) by querying the encryption_state column of the `sys.dm_database_encryption_keys` view.</span></span>

## <a name="enable-sql-database-auditing-if-necessary"></a><span data-ttu-id="e606f-187">Controle in te schakelen SQL-Database, indien nodig</span><span class="sxs-lookup"><span data-stu-id="e606f-187">Enable SQL Database auditing, if necessary</span></span>

<span data-ttu-id="e606f-188">Azure SQL Database Auditing houdt databasegebeurtenissen en schrijft die deze naar een auditlogboek Meld u bij uw Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="e606f-188">Azure SQL Database Auditing tracks database events and writes them to an audit log in your Azure Storage account.</span></span> <span data-ttu-id="e606f-189">Controle, kunt u de naleving van regelgeving onderhouden, de activiteit in een database begrijpen en meer inzicht krijgen in discrepanties en afwijkingen die kunnen wijzen op mogelijke schendingen van de beveiliging.</span><span class="sxs-lookup"><span data-stu-id="e606f-189">Auditing can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate potential security violations.</span></span> <span data-ttu-id="e606f-190">Volg deze stappen om een standaard controlebeleid voor de SQL-database te maken:</span><span class="sxs-lookup"><span data-stu-id="e606f-190">Follow these steps to create a default auditing policy for your SQL database:</span></span>

1. <span data-ttu-id="e606f-191">Selecteer **SQL-databases** in het menu links, en klikt u op uw database in de **SQL-databases** pagina.</span><span class="sxs-lookup"><span data-stu-id="e606f-191">Select **SQL databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 

2. <span data-ttu-id="e606f-192">Selecteer in de blade instellingen **controle en detectie van dreigingen**.</span><span class="sxs-lookup"><span data-stu-id="e606f-192">In the Settings blade, select **Auditing & Threat Detection**.</span></span> <span data-ttu-id="e606f-193">Kennisgeving serverniveaus controle is uitgeschakeld en of er een **serverinstellingen weergeven** koppeling waarmee u weergeven of wijzigen van de server controle-instellingen in deze context.</span><span class="sxs-lookup"><span data-stu-id="e606f-193">Notice that sever-level auditing is diabled and that there is a **View server settings** link that allows you to view or modify the server auditing settings from this context.</span></span>

    ![Controle-Blade](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. <span data-ttu-id="e606f-195">Als u liever een Audit type (of locatie?) inschakelen verschilt van de opgegeven op serverniveau, schakelt u **ON** controle, en kies de **Blob** controletype.</span><span class="sxs-lookup"><span data-stu-id="e606f-195">If you prefer to enable an Audit type (or location?) different from the one specified at the server level, turn **ON** Auditing, and choose the **Blob** Auditing Type.</span></span> <span data-ttu-id="e606f-196">Als server Auditingfunctie voor blobs is ingeschakeld, wordt de database geconfigureerd audit bestaan naast de Blob-controle-server.</span><span class="sxs-lookup"><span data-stu-id="e606f-196">If server Blob auditing is enabled, the database configured audit will exist side by side with the server Blob audit.</span></span>

    ![Controle inschakelen](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. <span data-ttu-id="e606f-198">Selecteer **opslaggroep** om de Blade Audit logboeken opslag te openen.</span><span class="sxs-lookup"><span data-stu-id="e606f-198">Select **Storage Details** to open the Audit Logs Storage Blade.</span></span> <span data-ttu-id="e606f-199">Selecteer de Azure storage-account waarbij logboeken worden opgeslagen en de bewaarperiode, waarna de oude logboeken worden verwijderd, klikt u vervolgens op **OK** onderaan.</span><span class="sxs-lookup"><span data-stu-id="e606f-199">Select the Azure storage account where logs will be saved, and the retention period, after which the old logs will be deleted, then click **OK** at the bottom.</span></span> 

   > [!TIP]
   > <span data-ttu-id="e606f-200">Gebruik hetzelfde opslagaccount voor alle gecontroleerde databases optimaal buiten de controle rapporten sjablonen.</span><span class="sxs-lookup"><span data-stu-id="e606f-200">Use the same storage account for all audited databases to get the most out of the auditing reports templates.</span></span>
   > 

5. <span data-ttu-id="e606f-201">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e606f-201">Click **Save**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e606f-202">Als u aanpassen van de gecontroleerde gebeurtenissen wilt, kunt u dit doen via PowerShell of REST-API - Zie de [Automation (PowerShell / REST-API)](sql-database-auditing.md#subheading-7) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e606f-202">If you want to customize the audited events, you can do this via PowerShell or REST API - see the [Automation (PowerShell / REST API)](sql-database-auditing.md#subheading-7) section for more details.</span></span>
>

## <a name="enable-sql-database-threat-detection"></a><span data-ttu-id="e606f-203">Detectie van dreigingen SQL-Database inschakelen</span><span class="sxs-lookup"><span data-stu-id="e606f-203">Enable SQL Database threat detection</span></span>

<span data-ttu-id="e606f-204">Detectie van dreigingen biedt een nieuwe laag van beveiliging, waarmee klanten om te detecteren en op mogelijke bedreigingen reageert wanneer deze zich voordoen doordat beveiligingswaarschuwingen op vreemde activiteiten worden gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="e606f-204">Threat Detection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="e606f-205">Gebruikers kunnen de verdachte gebeurtenissen om te bepalen of ze het gevolg zijn van een poging om te openen, inbreuk of misbruik van gegevens in de database met behulp van SQL Database Auditing verkennen.</span><span class="sxs-lookup"><span data-stu-id="e606f-205">Users can explore the suspicious events using SQL Database Auditing to determine if they result from an attempt to access, breach or exploit data in the database.</span></span> <span data-ttu-id="e606f-206">Detectie van dreigingen kunt u eenvoudig op mogelijke bedreigingen adres met de database hoeft te worden van een deskundige beveiliging of systemen bewaking van de geavanceerde beveiliging te beheren.</span><span class="sxs-lookup"><span data-stu-id="e606f-206">Threat Detection makes it simple to address potential threats to the database without the need to be a security expert or manage advanced security monitoring systems.</span></span>
<span data-ttu-id="e606f-207">Detectie van dreigingen detecteert bijvoorbeeld bepaalde afwijkende databaseactiviteiten potentiële SQL-injectie pogingen die aangeeft.</span><span class="sxs-lookup"><span data-stu-id="e606f-207">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="e606f-208">SQL-injectie is een van de algemene Web application beveiligingsproblemen op het Internet worden gebruikt voor aanvallen op gegevensgestuurde toepassingen.</span><span class="sxs-lookup"><span data-stu-id="e606f-208">SQL injection is one of the common Web application security issues on the Internet, used to attack data-driven applications.</span></span> <span data-ttu-id="e606f-209">Aanvallers te profiteren van de toepassing zwakke plekken in het injecteren schadelijke SQL-instructies in de invoervelden toepassing voor schendingen veroorzaken of wijzigen van gegevens in de database.</span><span class="sxs-lookup"><span data-stu-id="e606f-209">Attackers take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, for breaching or modifying data in the database.</span></span>

1. <span data-ttu-id="e606f-210">Navigeer naar de blade van de configuratie van de SQL-database die u wilt bewaken.</span><span class="sxs-lookup"><span data-stu-id="e606f-210">Navigate to the configuration blade of the SQL database you want to monitor.</span></span> <span data-ttu-id="e606f-211">Selecteer in de blade instellingen **controle en detectie van dreigingen**.</span><span class="sxs-lookup"><span data-stu-id="e606f-211">In the Settings blade, select **Auditing & Threat Detection**.</span></span>

    ![Navigatiedeelvenster](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. <span data-ttu-id="e606f-213">In de **controle en detectie van dreigingen** configuratie blade Schakel **ON** controle, wordt die de threat detectie-instellingen weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e606f-213">In the **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display the threat detection settings.</span></span>

3. <span data-ttu-id="e606f-214">Schakel **ON** bedreigingendetectie.</span><span class="sxs-lookup"><span data-stu-id="e606f-214">Turn **ON** threat detection.</span></span>

4. <span data-ttu-id="e606f-215">Configureer de lijst met e-mailberichten die beveiligingswaarschuwingen na detectie van afwijkende databaseactiviteiten ontvangt.</span><span class="sxs-lookup"><span data-stu-id="e606f-215">Configure the list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>

5. <span data-ttu-id="e606f-216">Klik op **opslaan** in de **controle en detectie van bedreigingen** blade op te slaan de nieuwe of bijgewerkte controle dreiging van beleid.</span><span class="sxs-lookup"><span data-stu-id="e606f-216">Click **Save** in the **Auditing & Threat detection** blade to save the new or updated auditing and threat detection policy.</span></span>

    ![Navigatiedeelvenster](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    <span data-ttu-id="e606f-218">Als er worden afwijkende databaseactiviteiten gedetecteerd, ontvangt u een e-mailmelding na detectie van afwijkende databaseactiviteiten.</span><span class="sxs-lookup"><span data-stu-id="e606f-218">If anomalous database activities are detected, you will receive an email notification upon detection of anomalous database activities.</span></span> <span data-ttu-id="e606f-219">Het e-mailadres bevatten informatie over de verdachte-gebeurtenis met inbegrip van de aard van de afwijkende activiteiten, databasenaam, de servernaam van de en de tijd van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="e606f-219">The email will provide information on the suspicious security event including the nature of the anomalous activities, database name, server name and the event time.</span></span> <span data-ttu-id="e606f-220">Bovendien bevatten informatie over mogelijke oorzaken en aanbevolen acties te onderzoeken en de mogelijke bedreiging voor de database te verminderen.</span><span class="sxs-lookup"><span data-stu-id="e606f-220">In addition, it will provide information on possible causes and recommended actions to investigate and mitigate the potential threat to the database.</span></span> <span data-ttu-id="e606f-221">De volgende stappen maakt u via wat te doen moet u deze een e-mail ontvangen:</span><span class="sxs-lookup"><span data-stu-id="e606f-221">The next steps walk you through what to do should you receive such an email:</span></span>

    ![Threat detectie e](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. <span data-ttu-id="e606f-223">Klik in de e-mail op de **Azure SQL-controle logboek** koppeling, die wordt de Azure-portal te starten en de relevante controle records rond de tijd van de verdachte gebeurtenis wilt weergeven.</span><span class="sxs-lookup"><span data-stu-id="e606f-223">In the email, click on the **Azure SQL Auditing Log** link, which will launch the Azure portal and show the relevant auditing records around the time of the suspicious event.</span></span>

    ![AuditRecords](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. <span data-ttu-id="e606f-225">Klik op de controlerecords naar meer details weergeven over de op verdachte databaseactiviteiten zoals SQL-instructie is mislukt reden en client-IP.</span><span class="sxs-lookup"><span data-stu-id="e606f-225">Click on the audit records to view more details on the suspicious database activities such as SQL statement, failure reason and client IP.</span></span>

    ![Details van de records](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. <span data-ttu-id="e606f-227">Klik op de blade controle Records **openen in Excel** openen van een vooraf geconfigureerde excel sjabloon importeren en uitvoeren van de diepgaande analyse van het controlelogboek rond de tijd van de verdachte activiteit.</span><span class="sxs-lookup"><span data-stu-id="e606f-227">In the Auditing Records blade, click  **Open in Excel** to open a pre-configured excel template to import and run deeper analysis of the audit log around the time of the suspicious event.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e606f-228">In Excel 2010 of hoger, Power Query en de **snel combineren** instelling is vereist.</span><span class="sxs-lookup"><span data-stu-id="e606f-228">In Excel 2010 or later, Power Query and the **Fast Combine** setting is required.</span></span>

    ![Open records in Excel](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. <span data-ttu-id="e606f-230">Voor het configureren van de **snel combineren** instellen - In de **POWER QUERY** linttabblad, selecteer **opties** om het dialoogvenster opties weer te geven.</span><span class="sxs-lookup"><span data-stu-id="e606f-230">To configure the **Fast Combine** setting - In the **POWER QUERY** ribbon tab, select **Options** to display the Options dialog.</span></span> <span data-ttu-id="e606f-231">Selecteer de sectie Privacy en kiest u de tweede optie - 'Negeren van de privacyniveaus en mogelijk verbeterde prestaties':</span><span class="sxs-lookup"><span data-stu-id="e606f-231">Select the Privacy section and choose the second option - 'Ignore the Privacy Levels and potentially improve performance':</span></span>

    ![Excel snel combineren](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. <span data-ttu-id="e606f-233">Als u wilt laden controlelogboeken SQL, zorg ervoor dat de parameters in de instellingen juist zijn ingesteld en selecteer vervolgens het lint 'Data' en klik op de knop Alles vernieuwen tabblad.</span><span class="sxs-lookup"><span data-stu-id="e606f-233">To load SQL audit logs, ensure that the parameters in the settings tab are set correctly and then select the 'Data' ribbon and click the 'Refresh All' button.</span></span>

    ![Excel-parameters](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. <span data-ttu-id="e606f-235">De resultaten worden weergegeven de **SQL controlelogboeken** blad waarmee u meer gedetailleerde analyse van de afwijkende activiteiten die zijn gedetecteerd uitvoeren, en het effect van de beveiligingsgebeurtenis in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="e606f-235">The results appear in the **SQL Audit Logs** sheet which enables you to run deeper analysis of the anomalous activities that were detected, and mitigate the impact of the security event in your application.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e606f-236">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e606f-236">Next steps</span></span>
<span data-ttu-id="e606f-237">U kunt de beveiliging van uw database tegen kwaadwillende gebruikers of onbevoegde toegang met een paar eenvoudige stappen kunt verbeteren.</span><span class="sxs-lookup"><span data-stu-id="e606f-237">You can improve the protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="e606f-238">In deze zelfstudie leert u naar:</span><span class="sxs-lookup"><span data-stu-id="e606f-238">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="e606f-239">Firewallregels voor de server en of de database instellen</span><span class="sxs-lookup"><span data-stu-id="e606f-239">Set up firewall rules for your sever and or database</span></span>
> * <span data-ttu-id="e606f-240">Verbinding maken met uw database met behulp van een beveiligde verbindingsreeks</span><span class="sxs-lookup"><span data-stu-id="e606f-240">Connect to your database using a secure connection string</span></span>
> * <span data-ttu-id="e606f-241">Gebruikerstoegang beheren</span><span class="sxs-lookup"><span data-stu-id="e606f-241">Manage user access</span></span>
> * <span data-ttu-id="e606f-242">Uw gegevens beschermen met versleuteling</span><span class="sxs-lookup"><span data-stu-id="e606f-242">Protect your data with encryption</span></span>
> * <span data-ttu-id="e606f-243">Inschakelen van controle voor SQL-Database</span><span class="sxs-lookup"><span data-stu-id="e606f-243">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="e606f-244">Detectie van dreigingen SQL-Database inschakelen</span><span class="sxs-lookup"><span data-stu-id="e606f-244">Enable SQL Database threat detection</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="e606f-245">De prestaties van uw SQL-database verbeteren</span><span class="sxs-lookup"><span data-stu-id="e606f-245">Improve SQL Database performance</span></span>](sql-database-performance-tutorial.md)

