---
title: aaaSecure uw Azure SQL database | Microsoft Docs
description: Meer informatie over technieken en functies toosecure uw Azure SQL database.
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
ms.openlocfilehash: 1450d633d6f65faf1b8a2dc0dc7dfe996fb0719d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-azure-sql-database"></a><span data-ttu-id="24f2a-103">Beveiligen van uw Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="24f2a-103">Secure your Azure SQL Database</span></span>

<span data-ttu-id="24f2a-104">SQL-Database beveiligt uw gegevens door te beperken van toegang tooyour database met behulp van firewallregels, verificatiemechanismen vereisen tooprove gebruikers hun identiteit en autorisatie toodata via lidmaatschappen op basis van rollen en machtigingen, evenals via beveiliging en dynamische gegevensmaskering.</span><span class="sxs-lookup"><span data-stu-id="24f2a-104">SQL Database secures your data by limiting access tooyour database using firewall rules, authentication mechanisms requiring users tooprove their identity, and authorization toodata through role-based memberships and permissions, as well as through row-level security and dynamic data masking.</span></span>

<span data-ttu-id="24f2a-105">U kunt de beveiliging van uw database tegen kwaadwillende gebruikers of onbevoegde toegang met een paar eenvoudige stappen Hallo verbeteren.</span><span class="sxs-lookup"><span data-stu-id="24f2a-105">You can improve hello protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="24f2a-106">In deze zelfstudie leert u naar:</span><span class="sxs-lookup"><span data-stu-id="24f2a-106">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="24f2a-107">Niveau van de server firewallregels voor uw server in hello Azure-portal instellen</span><span class="sxs-lookup"><span data-stu-id="24f2a-107">Set up server-level firewall rules for your server in hello Azure portal</span></span>
> * <span data-ttu-id="24f2a-108">Regels voor uw database met behulp van SSMS firewallregel op databaseniveau instellen</span><span class="sxs-lookup"><span data-stu-id="24f2a-108">Set up database-level firewall rules for your database using SSMS</span></span>
> * <span data-ttu-id="24f2a-109">Verbinding maken met behulp van een beveiligde verbindingsreeks tooyour-database</span><span class="sxs-lookup"><span data-stu-id="24f2a-109">Connect tooyour database using a secure connection string</span></span>
> * <span data-ttu-id="24f2a-110">Gebruikerstoegang beheren</span><span class="sxs-lookup"><span data-stu-id="24f2a-110">Manage user access</span></span>
> * <span data-ttu-id="24f2a-111">Uw gegevens beschermen met versleuteling</span><span class="sxs-lookup"><span data-stu-id="24f2a-111">Protect your data with encryption</span></span>
> * <span data-ttu-id="24f2a-112">Inschakelen van controle voor SQL-Database</span><span class="sxs-lookup"><span data-stu-id="24f2a-112">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="24f2a-113">Detectie van dreigingen SQL-Database inschakelen</span><span class="sxs-lookup"><span data-stu-id="24f2a-113">Enable SQL Database threat detection</span></span>

<span data-ttu-id="24f2a-114">Als u een Azure-abonnement geen [een gratis account maken](https://azure.microsoft.com/free/) voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="24f2a-114">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24f2a-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="24f2a-115">Prerequisites</span></span>

<span data-ttu-id="24f2a-116">toocomplete deze zelfstudie, zorg ervoor dat u hebt hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="24f2a-116">toocomplete this tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="24f2a-117">Meest recente versie van geïnstalleerde Hallo [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="24f2a-117">Installed hello newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span> 
- <span data-ttu-id="24f2a-118">Geïnstalleerde Microsoft Excel</span><span class="sxs-lookup"><span data-stu-id="24f2a-118">Installed Microsoft Excel</span></span>
- <span data-ttu-id="24f2a-119">Zie gemaakt van een Azure SQL-server en database - [maken van een Azure SQL database in Azure-portal Hallo](sql-database-get-started-portal.md), [maken van één Azure SQL database met behulp van Azure CLI Hallo](sql-database-get-started-cli.md), en [maken van een enkele Azure SQL de database met behulp van PowerShell](sql-database-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="24f2a-119">Created an Azure SQL server and database - See [Create an Azure SQL database in hello Azure portal](sql-database-get-started-portal.md), [Create a single Azure SQL database using hello Azure CLI](sql-database-get-started-cli.md), and [Create a single Azure SQL database using PowerShell](sql-database-get-started-powershell.md).</span></span> 

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="24f2a-120">Meld u bij toohello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="24f2a-120">Log in toohello Azure portal</span></span>

<span data-ttu-id="24f2a-121">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="24f2a-121">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="24f2a-122">Maken van een firewallregel op serverniveau in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="24f2a-122">Create a server-level firewall rule in hello Azure portal</span></span>

<span data-ttu-id="24f2a-123">SQL-databases worden beveiligd door een firewall in Azure.</span><span class="sxs-lookup"><span data-stu-id="24f2a-123">SQL databases are protected by a firewall in Azure.</span></span> <span data-ttu-id="24f2a-124">Standaard worden alle verbindingen toohello server- en Hallo databases binnen Hallo server geweigerd, met uitzondering van verbindingen met andere Azure-services.</span><span class="sxs-lookup"><span data-stu-id="24f2a-124">By default, all connections toohello server and hello databases inside hello server are rejected except for connections from other Azure services.</span></span> <span data-ttu-id="24f2a-125">Zie voor meer informatie [Azure SQL Database server- en databaseniveau firewallregels](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="24f2a-125">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="24f2a-126">de veiligste configuratie Hallo is tooset 'Toestaan dat toegang tot services tooAzure' tooOFF.</span><span class="sxs-lookup"><span data-stu-id="24f2a-126">hello most secure configuration is tooset 'Allow access tooAzure services' tooOFF.</span></span> <span data-ttu-id="24f2a-127">Als u nodig hebt tooconnect toohello-database van een virtuele machine in Azure of cloud-service, moet u een [gereserveerde IP-adres](../virtual-network/virtual-networks-reserved-public-ip.md) en alleen Hallo gereserveerd IP-adres toegang toestaan via Hallo firewall.</span><span class="sxs-lookup"><span data-stu-id="24f2a-127">If you need tooconnect toohello database from an Azure VM or cloud service, you should create a [Reserved IP](../virtual-network/virtual-networks-reserved-public-ip.md) and allow only hello reserved IP address access through hello firewall.</span></span> 

<span data-ttu-id="24f2a-128">Volg deze stappen toocreate een [SQL-Database firewallregel op serverniveau](sql-database-firewall-configure.md) voor uw server tooallow verbindingen van een specifiek IP-adres.</span><span class="sxs-lookup"><span data-stu-id="24f2a-128">Follow these steps toocreate a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your server tooallow connections from a specific IP address.</span></span> 

> [!NOTE]
> <span data-ttu-id="24f2a-129">Als u een voorbeelddatabase hebt gemaakt in Azure met behulp van een van de vorige zelfstudies Hallo of snelstartgidsen en zijn de u deze zelfstudie op een computer met de Hallo dezelfde IP, dat het adres had toen u deze zelfstudie hebt doorlopen, kunt u deze stap overslaan als u een firewallregel op serverniveau al gemaakt.</span><span class="sxs-lookup"><span data-stu-id="24f2a-129">If you have created a sample database in Azure using one of hello previous tutorials or quickstarts and are performing this tutorial on a computer with hello same IP address that it had when you walked through those tutorials, you can skip this step as you will have already created a server-level firewall rule.</span></span>
>

1. <span data-ttu-id="24f2a-130">Klik op **SQL-databases** uit Hallo links en klik op Hallo database gewenst tooconfigure Hallo firewallregel voor op Hallo **SQL-databases** pagina.</span><span class="sxs-lookup"><span data-stu-id="24f2a-130">Click **SQL databases** from hello left-hand menu and click hello database you would like tooconfigure hello firewall rule for on hello **SQL databases** page.</span></span> <span data-ttu-id="24f2a-131">Hallo overzichtspagina voor uw database wordt geopend, waarin u Hallo volledig gekwalificeerde servernaam (zoals **mynewserver 20170313.database.windows.net**) en biedt opties voor verdere configuratie.</span><span class="sxs-lookup"><span data-stu-id="24f2a-131">hello overview page for your database opens, showing you hello fully qualified server name (such as **mynewserver-20170313.database.windows.net**) and provides options for further configuration.</span></span>

      ![serverfirewallregel](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. <span data-ttu-id="24f2a-133">Klik op **serverfirewall ingesteld** op Hallo werkbalk zoals weergegeven in de vorige afbeelding Hallo.</span><span class="sxs-lookup"><span data-stu-id="24f2a-133">Click **Set server firewall** on hello toolbar as shown in hello previous image.</span></span> <span data-ttu-id="24f2a-134">Hallo **Firewall-instellingen** pagina voor Hallo SQL Database-server wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="24f2a-134">hello **Firewall settings** page for hello SQL Database server opens.</span></span> 

3. <span data-ttu-id="24f2a-135">Klik op **client-IP toevoegen** op Hallo werkbalk tooadd Hallo openbaar IP-adres van Hallo computer verbonden toohello portal met of Hallo firewallregel handmatig invoeren en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="24f2a-135">Click **Add client IP** on hello toolbar tooadd hello public IP address of hello computer connected toohello portal with or enter hello firewall rule manually and then click **Save**.</span></span>

      ![serverfirewallregel instellen](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. <span data-ttu-id="24f2a-137">Klik op **OK** en klik vervolgens op Hallo **X** tooclose hello **Firewall-instellingen** pagina.</span><span class="sxs-lookup"><span data-stu-id="24f2a-137">Click **OK** and then click hello **X** tooclose hello **Firewall settings** page.</span></span>

<span data-ttu-id="24f2a-138">U kunt nu verbinding maken met de database tooany in Hallo server Hello opgegeven IP-adres of IP-adresbereik.</span><span class="sxs-lookup"><span data-stu-id="24f2a-138">You can now connect tooany database in hello server with hello specified IP address or IP address range.</span></span>

> [!NOTE]
> <span data-ttu-id="24f2a-139">SQL Database communiceert via poort 1433.</span><span class="sxs-lookup"><span data-stu-id="24f2a-139">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="24f2a-140">Als u tooconnect van binnen een bedrijfsnetwerk probeert, kan uitgaand verkeer via poort 1433 niet worden toegestaan door de firewall van uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="24f2a-140">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="24f2a-141">Zo ja, zich u niet kunnen tooconnect tooyour Azure SQL Database-server tenzij uw IT-afdeling poort 1433 wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="24f2a-141">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a><span data-ttu-id="24f2a-142">Een firewallregel op databaseniveau met behulp van SSMS maken</span><span class="sxs-lookup"><span data-stu-id="24f2a-142">Create a database-level firewall rule using SSMS</span></span>

<span data-ttu-id="24f2a-143">Firewallregel op databaseniveau regels kunt u toocreate verschillende firewall-instellingen voor de verschillende databases binnen dezelfde logische server en toocreate firewallregels die zijn draagbare - wat betekent dat ze Hallo database tijdens volgen Hallo een [failover ](sql-database-geo-replication-overview.md) in plaats van op Hallo SQL server worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="24f2a-143">Database-level firewall rules enable you toocreate different firewall settings for different databases within hello same logical server and toocreate firewall rules that are portable - meaning that they follow hello database during a [failover](sql-database-geo-replication-overview.md) rather than being stored on hello SQL server.</span></span> <span data-ttu-id="24f2a-144">Firewallregels databaseniveau kunnen alleen worden geconfigureerd met behulp van Transact-SQL-instructies en alleen nadat u het eerste niveau van de server firewallregel Hallo hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="24f2a-144">Database-level firewall rules can only be configured by using Transact-SQL statements and only after you have configured hello first server-level firewall rule.</span></span> <span data-ttu-id="24f2a-145">Zie voor meer informatie [Azure SQL Database server- en databaseniveau firewallregels](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="24f2a-145">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="24f2a-146">Deze stappen toocreate een database-specifieke firewallregel volgt.</span><span class="sxs-lookup"><span data-stu-id="24f2a-146">Follows these steps toocreate a database-specific firewall rule.</span></span>

1. <span data-ttu-id="24f2a-147">Verbinding maken met tooyour-database, bijvoorbeeld met behulp van [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="24f2a-147">Connect tooyour database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span></span>

2. <span data-ttu-id="24f2a-148">In Object Explorer met de rechtermuisknop op de gewenste tooadd een firewall voor regel en klik op Hallo-database **nieuwe Query**.</span><span class="sxs-lookup"><span data-stu-id="24f2a-148">In Object Explorer, right-click on hello database you want tooadd a firewall rule for and click **New Query**.</span></span> <span data-ttu-id="24f2a-149">Een lege queryvenster wordt geopend die verbonden tooyour database.</span><span class="sxs-lookup"><span data-stu-id="24f2a-149">A blank query window opens that is connected tooyour database.</span></span>

3. <span data-ttu-id="24f2a-150">In het queryvenster hello, Hallo IP-adres tooyour openbaar IP-adres wijzigen en vervolgens Hallo volgende query wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="24f2a-150">In hello query window, modify hello IP address tooyour public IP address and then execute hello following query:</span></span>

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. <span data-ttu-id="24f2a-151">Op de werkbalk Hallo **Execute** toocreate Hallo firewallregel.</span><span class="sxs-lookup"><span data-stu-id="24f2a-151">On hello toolbar, click **Execute** toocreate hello firewall rule.</span></span>

## <a name="view-how-tooconnect-an-application-tooyour-database-using-a-secure-connection-string"></a><span data-ttu-id="24f2a-152">Hoe een toepassing tooyour tooconnect database met behulp van een beveiligde verbindingsreeks weergeven</span><span class="sxs-lookup"><span data-stu-id="24f2a-152">View how tooconnect an application tooyour database using a secure connection string</span></span>

<span data-ttu-id="24f2a-153">tooensure een beveiligde, gecodeerde verbinding tussen een client-toepassing en de SQL-Database, Hallo-verbindingsreeks heeft toobe geconfigureerd:</span><span class="sxs-lookup"><span data-stu-id="24f2a-153">tooensure a secure, encrypted connection between a client application and SQL Database, hello connection string has toobe configured to:</span></span>

- <span data-ttu-id="24f2a-154">Aanvragen van een versleutelde verbinding, en</span><span class="sxs-lookup"><span data-stu-id="24f2a-154">Request an encrypted connection, and</span></span>
- <span data-ttu-id="24f2a-155">toonot vertrouwensrelatie Hallo-servercertificaat.</span><span class="sxs-lookup"><span data-stu-id="24f2a-155">toonot trust hello server certificate.</span></span> 

<span data-ttu-id="24f2a-156">Dit maakt een verbinding met behulp van Transport Layer Security (TLS) en Hallo risico van man-in-the-middle-aanvallen vermindert.</span><span class="sxs-lookup"><span data-stu-id="24f2a-156">This establishes a connection using Transport Layer Security (TLS) and reduces hello risk of man-in-the-middle attacks.</span></span> <span data-ttu-id="24f2a-157">U kunt ophalen met juist geconfigureerde verbindingsreeksen voor uw SQL-Database voor ondersteunde client stuurprogramma's hello Azure-portal zoals weergegeven voor ADO.net in deze schermafbeelding.</span><span class="sxs-lookup"><span data-stu-id="24f2a-157">You can obtain correctly configured connection strings for your SQL Database for supported client drivers from hello Azure portal as shown for ADO.net in this screenshot.</span></span>

1. <span data-ttu-id="24f2a-158">Selecteer **SQL-databases** Hallo links menu en klik op de database op Hallo **SQL-databases** pagina.</span><span class="sxs-lookup"><span data-stu-id="24f2a-158">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span>

2. <span data-ttu-id="24f2a-159">Op Hallo **overzicht** pagina voor uw database, klikt u op **databaseverbindingsreeksen tonen**.</span><span class="sxs-lookup"><span data-stu-id="24f2a-159">On hello **Overview** page for your database, click **Show database connection strings**.</span></span>

3. <span data-ttu-id="24f2a-160">Bekijk Hallo voltooid **ADO.NET** verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="24f2a-160">Review hello complete **ADO.NET** connection string.</span></span>

    ![ADO.NET-verbindingsreeks](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a><span data-ttu-id="24f2a-162">Databasegebruikers te maken</span><span class="sxs-lookup"><span data-stu-id="24f2a-162">Creating database users</span></span>

<span data-ttu-id="24f2a-163">Voordat u alle gebruikers, moet u eerst kiezen uit twee soorten verificatie wordt ondersteund door Azure SQL Database:</span><span class="sxs-lookup"><span data-stu-id="24f2a-163">Before creating any users, you must first choose from one of two authentication types supported by Azure SQL Database:</span></span> 

<span data-ttu-id="24f2a-164">**SQL-verificatie**, die gebruikmaakt van gebruikersnaam en wachtwoord voor aanmeldingen en gebruikers die geldig zijn alleen in de context van een bepaalde database binnen een logische server Hallo.</span><span class="sxs-lookup"><span data-stu-id="24f2a-164">**SQL Authentication**, which uses username and password for logins and users that are valid only in hello context of a specific database within a logical server.</span></span> 

<span data-ttu-id="24f2a-165">**Azure Active Directory-verificatie**, waarbij identiteiten die worden beheerd door Azure Active Directory wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="24f2a-165">**Azure Active Directory Authentication**, which uses identities managed by Azure Active Directory.</span></span> 

<span data-ttu-id="24f2a-166">Als u wilt dat toouse [Azure Active Directory](./sql-database-aad-authentication.md) tooauthenticate op SQL-Database ingevuld Azure Active Directory moet bestaan voordat u verder kunt gaan.</span><span class="sxs-lookup"><span data-stu-id="24f2a-166">If you want toouse [Azure Active Directory](./sql-database-aad-authentication.md) tooauthenticate against SQL Database, a populated Azure Active Directory must exist before you can proceed.</span></span>

<span data-ttu-id="24f2a-167">Volg deze stappen toocreate een gebruiker via SQL-verificatie:</span><span class="sxs-lookup"><span data-stu-id="24f2a-167">Follow these steps toocreate a user using SQL Authentication:</span></span>

1. <span data-ttu-id="24f2a-168">Verbinding maken met tooyour-database, bijvoorbeeld met behulp van [SQL Server Management Studio](./sql-database-connect-query-ssms.md) met uw beheerdersreferenties voor de server.</span><span class="sxs-lookup"><span data-stu-id="24f2a-168">Connect tooyour database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) using your server admin credentials.</span></span>

2. <span data-ttu-id="24f2a-169">In Object Explorer met de rechtermuisknop op Hallo database tooadd een nieuwe gebruiker op en klik op **nieuwe Query**.</span><span class="sxs-lookup"><span data-stu-id="24f2a-169">In Object Explorer, right-click on hello database you want tooadd a new user on and click **New Query**.</span></span> <span data-ttu-id="24f2a-170">Een lege queryvenster wordt geopend dat de geselecteerde database verbonden toohello.</span><span class="sxs-lookup"><span data-stu-id="24f2a-170">A blank query window opens that is connected toohello selected database.</span></span>

3. <span data-ttu-id="24f2a-171">Voer in het queryvenster hello, Hallo query te volgen:</span><span class="sxs-lookup"><span data-stu-id="24f2a-171">In hello query window, enter hello following query:</span></span>

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. <span data-ttu-id="24f2a-172">Op de werkbalk Hallo **Execute** toocreate Hallo gebruiker.</span><span class="sxs-lookup"><span data-stu-id="24f2a-172">On hello toolbar, click **Execute** toocreate hello user.</span></span>

5. <span data-ttu-id="24f2a-173">Standaard Hallo gebruiker verbinding kan maken van toohello database, maar heeft geen machtigingen tooread of schrijven gegevens.</span><span class="sxs-lookup"><span data-stu-id="24f2a-173">By default, hello user can connect toohello database, but has no permissions tooread or write data.</span></span> <span data-ttu-id="24f2a-174">toogrant deze machtigingen toohello nieuw aangemaakte gebruiker, het uitvoeren van de volgende twee opdrachten in een nieuwe queryvenster Hallo</span><span class="sxs-lookup"><span data-stu-id="24f2a-174">toogrant these permissions toohello newly created user, execute hello following two commands in a new query window</span></span>

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

<span data-ttu-id="24f2a-175">Het is best practice toocreate deze accounts niet-beheerders op Hallo database niveau tooconnect tooyour database tenzij u tooexecute beheerderstaken, zoals het maken van nieuwe gebruikers wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="24f2a-175">It is best practice toocreate these non-administrator accounts at hello database level tooconnect tooyour database unless you need tooexecute administrator tasks like creating new users.</span></span> <span data-ttu-id="24f2a-176">Controleer op Hallo [Azure Active Directory-zelfstudie](./sql-database-aad-authentication-configure.md) over het tooauthenticate met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="24f2a-176">Please review hello [Azure Active Directory tutorial](./sql-database-aad-authentication-configure.md) on how tooauthenticate using Azure Active Directory.</span></span>


## <a name="protect-your-data-with-encryption"></a><span data-ttu-id="24f2a-177">Uw gegevens beschermen met versleuteling</span><span class="sxs-lookup"><span data-stu-id="24f2a-177">Protect your data with encryption</span></span>

<span data-ttu-id="24f2a-178">Azure SQL Database transparante gegevensversleuteling (TDE) versleutelt automatisch uw gegevens in rust, zonder eventuele wijzigingen toohello toepassing toegang tot Hallo versleutelde database.</span><span class="sxs-lookup"><span data-stu-id="24f2a-178">Azure SQL Database transparent data encryption (TDE) automatically encrypts your data at rest, without requiring any changes toohello application accessing hello encrypted database.</span></span> <span data-ttu-id="24f2a-179">Voor nieuwe databases is TDE standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="24f2a-179">For newly created databases, TDE is on by default.</span></span> <span data-ttu-id="24f2a-180">tooenable TDE voor uw database of tooverify die TDE ingeschakeld is, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="24f2a-180">tooenable TDE for your database or tooverify that TDE is on, follow these steps:</span></span>

1. <span data-ttu-id="24f2a-181">Selecteer **SQL-databases** Hallo links menu en klik op de database op Hallo **SQL-databases** pagina.</span><span class="sxs-lookup"><span data-stu-id="24f2a-181">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 

2. <span data-ttu-id="24f2a-182">Klik op **transparante gegevensversleuteling** tooopen Hallo-configuratiepagina voor TDE.</span><span class="sxs-lookup"><span data-stu-id="24f2a-182">Click on **Transparent data encryption** tooopen hello configuration page for TDE.</span></span>

    ![Transparante gegevensversleuteling](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. <span data-ttu-id="24f2a-184">Indien nodig stelt **gegevensversleuteling** tooON en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="24f2a-184">If necessary, set **Data encryption** tooON and click **Save**.</span></span>

<span data-ttu-id="24f2a-185">Hallo-versleutelingsproces op Hallo achtergrond gestart.</span><span class="sxs-lookup"><span data-stu-id="24f2a-185">hello encryption process starts in hello background.</span></span> <span data-ttu-id="24f2a-186">U kunt Hallo voortgang via verbindende tooSQL Database [SQL Server Management Studio](./sql-database-connect-query-ssms.md) door het uitvoeren van query's Hallo encryption_state kolom Hallo `sys.dm_database_encryption_keys` weergeven.</span><span class="sxs-lookup"><span data-stu-id="24f2a-186">You can monitor hello progress by connecting tooSQL Database using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) by querying hello encryption_state column of hello `sys.dm_database_encryption_keys` view.</span></span>

## <a name="enable-sql-database-auditing-if-necessary"></a><span data-ttu-id="24f2a-187">Controle in te schakelen SQL-Database, indien nodig</span><span class="sxs-lookup"><span data-stu-id="24f2a-187">Enable SQL Database auditing, if necessary</span></span>

<span data-ttu-id="24f2a-188">Azure SQL Database Auditing houdt databasegebeurtenissen bij en schrijft deze tooan controlelogboek in uw Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="24f2a-188">Azure SQL Database Auditing tracks database events and writes them tooan audit log in your Azure Storage account.</span></span> <span data-ttu-id="24f2a-189">Controle, kunt u de naleving van regelgeving onderhouden, de activiteit in een database begrijpen en meer inzicht krijgen in discrepanties en afwijkingen die kunnen wijzen op mogelijke schendingen van de beveiliging.</span><span class="sxs-lookup"><span data-stu-id="24f2a-189">Auditing can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate potential security violations.</span></span> <span data-ttu-id="24f2a-190">Volg deze stappen toocreate een controle standaardbeleid voor uw SQL-database:</span><span class="sxs-lookup"><span data-stu-id="24f2a-190">Follow these steps toocreate a default auditing policy for your SQL database:</span></span>

1. <span data-ttu-id="24f2a-191">Selecteer **SQL-databases** Hallo links menu en klik op de database op Hallo **SQL-databases** pagina.</span><span class="sxs-lookup"><span data-stu-id="24f2a-191">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 

2. <span data-ttu-id="24f2a-192">Selecteer in de blade beleidinstellingen Hallo **controle en detectie van dreigingen**.</span><span class="sxs-lookup"><span data-stu-id="24f2a-192">In hello Settings blade, select **Auditing & Threat Detection**.</span></span> <span data-ttu-id="24f2a-193">Kennisgeving serverniveaus controle is uitgeschakeld en of er een **serverinstellingen weergeven** koppeling kunt u tooview of wijzigen van Hallo server controle-instellingen in deze context.</span><span class="sxs-lookup"><span data-stu-id="24f2a-193">Notice that sever-level auditing is diabled and that there is a **View server settings** link that allows you tooview or modify hello server auditing settings from this context.</span></span>

    ![Controle-Blade](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. <span data-ttu-id="24f2a-195">Als u liever tooenable een Audit type (of locatie?) verschilt van Hallo opgegeven op het serverniveau hello, schakelt u **ON** controle, en kies Hallo **Blob** controletype.</span><span class="sxs-lookup"><span data-stu-id="24f2a-195">If you prefer tooenable an Audit type (or location?) different from hello one specified at hello server level, turn **ON** Auditing, and choose hello **Blob** Auditing Type.</span></span> <span data-ttu-id="24f2a-196">Als server Auditingfunctie voor blobs is ingeschakeld, wordt naast Hallo server Blob audit Hallo geconfigureerd databaseaudit bestaan.</span><span class="sxs-lookup"><span data-stu-id="24f2a-196">If server Blob auditing is enabled, hello database configured audit will exist side by side with hello server Blob audit.</span></span>

    ![Controle inschakelen](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. <span data-ttu-id="24f2a-198">Selecteer **opslaggroep** tooopen Hallo Audit logboeken opslag Blade.</span><span class="sxs-lookup"><span data-stu-id="24f2a-198">Select **Storage Details** tooopen hello Audit Logs Storage Blade.</span></span> <span data-ttu-id="24f2a-199">Selecteer hello Azure storage-account waarin de logboeken worden opgeslagen en de bewaarperiode hello, als u welke Hallo oude logboeken worden verwijderd, klikt u **OK** Hallo onderaan.</span><span class="sxs-lookup"><span data-stu-id="24f2a-199">Select hello Azure storage account where logs will be saved, and hello retention period, after which hello old logs will be deleted, then click **OK** at hello bottom.</span></span> 

   > [!TIP]
   > <span data-ttu-id="24f2a-200">Gebruik dezelfde Hallo opslagaccount voor alle gecontroleerde databases tooget Hallo optimaal gebruik van Hallo controle rapporteert sjablonen.</span><span class="sxs-lookup"><span data-stu-id="24f2a-200">Use hello same storage account for all audited databases tooget hello most out of hello auditing reports templates.</span></span>
   > 

5. <span data-ttu-id="24f2a-201">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="24f2a-201">Click **Save**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="24f2a-202">Als u toocustomize Hallo gecontroleerd gebeurtenissen wilt, u kunt dit doen via PowerShell of REST-API - Zie Hallo [Automation (PowerShell / REST-API)](sql-database-auditing.md#subheading-7) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="24f2a-202">If you want toocustomize hello audited events, you can do this via PowerShell or REST API - see hello [Automation (PowerShell / REST API)](sql-database-auditing.md#subheading-7) section for more details.</span></span>
>

## <a name="enable-sql-database-threat-detection"></a><span data-ttu-id="24f2a-203">Detectie van dreigingen SQL-Database inschakelen</span><span class="sxs-lookup"><span data-stu-id="24f2a-203">Enable SQL Database threat detection</span></span>

<span data-ttu-id="24f2a-204">Detectie van dreigingen biedt een nieuwe laag van beveiliging, waarbij kan klanten toodetect en hierop reageren toopotential bedreigingen wanneer deze zich voordoen doordat beveiligingswaarschuwingen op vreemde activiteiten worden gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="24f2a-204">Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="24f2a-205">Gebruikers kunnen Hallo verdachte gebeurtenissen met SQL Database Auditing toodetermine als ze het gevolg zijn van een poging tooaccess, inbreuk of misbruik van gegevens in Hallo database verkennen.</span><span class="sxs-lookup"><span data-stu-id="24f2a-205">Users can explore hello suspicious events using SQL Database Auditing toodetermine if they result from an attempt tooaccess, breach or exploit data in hello database.</span></span> <span data-ttu-id="24f2a-206">Detectie van dreigingen maakt het eenvoudig tooaddress potentiële bedreigingen toohello database zonder Hallo nodig toobe een expert beveiliging of systemen bewaking van de geavanceerde beveiliging te beheren.</span><span class="sxs-lookup"><span data-stu-id="24f2a-206">Threat Detection makes it simple tooaddress potential threats toohello database without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>
<span data-ttu-id="24f2a-207">Detectie van dreigingen detecteert bijvoorbeeld bepaalde afwijkende databaseactiviteiten potentiële SQL-injectie pogingen die aangeeft.</span><span class="sxs-lookup"><span data-stu-id="24f2a-207">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="24f2a-208">SQL-injectie is een van de Hallo algemene Web application beveiligingsproblemen op Hallo Internet, gebruikte tooattack gegevensgestuurde toepassingen.</span><span class="sxs-lookup"><span data-stu-id="24f2a-208">SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="24f2a-209">Aanvallers te profiteren van de toepassing beveiligingslekken tooinject schadelijke SQL-instructies in de invoervelden toepassing voor schendingen veroorzaken of wijzigen van gegevens in de database Hallo.</span><span class="sxs-lookup"><span data-stu-id="24f2a-209">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, for breaching or modifying data in hello database.</span></span>

1. <span data-ttu-id="24f2a-210">Navigeer toohello configuratie blade Hallo gewenste toomonitor SQL-database.</span><span class="sxs-lookup"><span data-stu-id="24f2a-210">Navigate toohello configuration blade of hello SQL database you want toomonitor.</span></span> <span data-ttu-id="24f2a-211">Selecteer in de blade beleidinstellingen Hallo **controle en detectie van dreigingen**.</span><span class="sxs-lookup"><span data-stu-id="24f2a-211">In hello Settings blade, select **Auditing & Threat Detection**.</span></span>

    ![Navigatiedeelvenster](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. <span data-ttu-id="24f2a-213">In Hallo **controle en detectie van dreigingen** configuratie blade Schakel **ON** controle, wordt die Hallo threat detectie-instellingen weergegeven.</span><span class="sxs-lookup"><span data-stu-id="24f2a-213">In hello **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display hello threat detection settings.</span></span>

3. <span data-ttu-id="24f2a-214">Schakel **ON** bedreigingendetectie.</span><span class="sxs-lookup"><span data-stu-id="24f2a-214">Turn **ON** threat detection.</span></span>

4. <span data-ttu-id="24f2a-215">Hallo lijst configureren van e-mailberichten die beveiligingswaarschuwingen na detectie van afwijkende databaseactiviteiten ontvangt.</span><span class="sxs-lookup"><span data-stu-id="24f2a-215">Configure hello list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>

5. <span data-ttu-id="24f2a-216">Klik op **opslaan** in Hallo **controle en detectie van bedreigingen** blade toosave Hallo nieuwe of bijgewerkte controle en threat beleid.</span><span class="sxs-lookup"><span data-stu-id="24f2a-216">Click **Save** in hello **Auditing & Threat detection** blade toosave hello new or updated auditing and threat detection policy.</span></span>

    ![Navigatiedeelvenster](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    <span data-ttu-id="24f2a-218">Als er worden afwijkende databaseactiviteiten gedetecteerd, ontvangt u een e-mailmelding na detectie van afwijkende databaseactiviteiten.</span><span class="sxs-lookup"><span data-stu-id="24f2a-218">If anomalous database activities are detected, you will receive an email notification upon detection of anomalous database activities.</span></span> <span data-ttu-id="24f2a-219">Hallo e bevatten informatie over verdachte beveiligingslogboek Hallo Hallo aard van Hallo afwijkende activiteiten, databasenaam, server-naam en het Hallo gebeurtenistijd inclusief.</span><span class="sxs-lookup"><span data-stu-id="24f2a-219">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name and hello event time.</span></span> <span data-ttu-id="24f2a-220">Bovendien bevatten informatie over mogelijke oorzaken en aanbevolen acties tooinvestigate en Hallo mogelijke bedreiging toohello database beperken.</span><span class="sxs-lookup"><span data-stu-id="24f2a-220">In addition, it will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span> <span data-ttu-id="24f2a-221">Hallo volgende stappen walk via welke toodo moet u deze een e-mail ontvangen:</span><span class="sxs-lookup"><span data-stu-id="24f2a-221">hello next steps walk you through what toodo should you receive such an email:</span></span>

    ![Threat detectie e](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. <span data-ttu-id="24f2a-223">Hallo e-mail, klik op Hallo **Azure SQL-controle logboek** koppeling waarmee u hello Azure-portal te starten en relevante Hallo controle records rond de tijd Hallo van Hallo verdachte activiteit weer te geven.</span><span class="sxs-lookup"><span data-stu-id="24f2a-223">In hello email, click on hello **Azure SQL Auditing Log** link, which will launch hello Azure portal and show hello relevant auditing records around hello time of hello suspicious event.</span></span>

    ![AuditRecords](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. <span data-ttu-id="24f2a-225">Klik op Hallo audit records tooview meer informatie over Hallo database verdachte activiteiten zoals SQL-instructie is mislukt reden en client-IP.</span><span class="sxs-lookup"><span data-stu-id="24f2a-225">Click on hello audit records tooview more details on hello suspicious database activities such as SQL statement, failure reason and client IP.</span></span>

    ![Details van de records](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. <span data-ttu-id="24f2a-227">Klik op Hallo controle Records blade **openen in Excel** tooopen een vooraf geconfigureerde excel sjabloon tooimport en uitvoeren diepgaande analyse van Hallo controlelogboek rond de tijd Hallo van verdachte Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="24f2a-227">In hello Auditing Records blade, click  **Open in Excel** tooopen a pre-configured excel template tooimport and run deeper analysis of hello audit log around hello time of hello suspicious event.</span></span>

    > [!NOTE]
    > <span data-ttu-id="24f2a-228">In Excel 2010 of hoger, Power Query en Hallo **snel combineren** instelling is vereist.</span><span class="sxs-lookup"><span data-stu-id="24f2a-228">In Excel 2010 or later, Power Query and hello **Fast Combine** setting is required.</span></span>

    ![Open records in Excel](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. <span data-ttu-id="24f2a-230">Hallo tooconfigure **snel combineren** instelling - In Hallo **POWER QUERY** linttabblad, selecteer **opties** dialoogvenster toodisplay Hallo-opties.</span><span class="sxs-lookup"><span data-stu-id="24f2a-230">tooconfigure hello **Fast Combine** setting - In hello **POWER QUERY** ribbon tab, select **Options** toodisplay hello Options dialog.</span></span> <span data-ttu-id="24f2a-231">Selecteer Hallo privacysectie en kies Hallo tweede optie - 'Negeren Hallo privacyniveaus en mogelijk verbeterde prestaties':</span><span class="sxs-lookup"><span data-stu-id="24f2a-231">Select hello Privacy section and choose hello second option - 'Ignore hello Privacy Levels and potentially improve performance':</span></span>

    ![Excel snel combineren](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. <span data-ttu-id="24f2a-233">controlelogboeken tooload SQL, zorg ervoor dat Hallo-parameters in tabblad Hallo-instellingen juist zijn ingesteld en selecteer Hallo 'Data' lint en klikt u op Hallo Alles vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="24f2a-233">tooload SQL audit logs, ensure that hello parameters in hello settings tab are set correctly and then select hello 'Data' ribbon and click hello 'Refresh All' button.</span></span>

    ![Excel-parameters](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. <span data-ttu-id="24f2a-235">Hallo resultaten worden weergegeven in Hallo **SQL controlelogboeken** blad waarmee u toorun diepgaande analyse van Hallo afwijkende activiteiten die zijn gedetecteerd en verhelpen van Hallo gevolgen van het beveiligingslogboek Hallo in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="24f2a-235">hello results appear in hello **SQL Audit Logs** sheet which enables you toorun deeper analysis of hello anomalous activities that were detected, and mitigate hello impact of hello security event in your application.</span></span>


## <a name="next-steps"></a><span data-ttu-id="24f2a-236">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="24f2a-236">Next steps</span></span>
<span data-ttu-id="24f2a-237">U kunt de beveiliging van uw database tegen kwaadwillende gebruikers of onbevoegde toegang met een paar eenvoudige stappen Hallo verbeteren.</span><span class="sxs-lookup"><span data-stu-id="24f2a-237">You can improve hello protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="24f2a-238">In deze zelfstudie leert u naar:</span><span class="sxs-lookup"><span data-stu-id="24f2a-238">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="24f2a-239">Firewallregels voor de server en of de database instellen</span><span class="sxs-lookup"><span data-stu-id="24f2a-239">Set up firewall rules for your sever and or database</span></span>
> * <span data-ttu-id="24f2a-240">Verbinding maken met behulp van een beveiligde verbindingsreeks tooyour-database</span><span class="sxs-lookup"><span data-stu-id="24f2a-240">Connect tooyour database using a secure connection string</span></span>
> * <span data-ttu-id="24f2a-241">Gebruikerstoegang beheren</span><span class="sxs-lookup"><span data-stu-id="24f2a-241">Manage user access</span></span>
> * <span data-ttu-id="24f2a-242">Uw gegevens beschermen met versleuteling</span><span class="sxs-lookup"><span data-stu-id="24f2a-242">Protect your data with encryption</span></span>
> * <span data-ttu-id="24f2a-243">Inschakelen van controle voor SQL-Database</span><span class="sxs-lookup"><span data-stu-id="24f2a-243">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="24f2a-244">Detectie van dreigingen SQL-Database inschakelen</span><span class="sxs-lookup"><span data-stu-id="24f2a-244">Enable SQL Database threat detection</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="24f2a-245">De prestaties van uw SQL-database verbeteren</span><span class="sxs-lookup"><span data-stu-id="24f2a-245">Improve SQL Database performance</span></span>](sql-database-performance-tutorial.md)

