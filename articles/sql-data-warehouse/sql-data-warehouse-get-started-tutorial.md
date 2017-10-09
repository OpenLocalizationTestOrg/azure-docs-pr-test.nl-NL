---
title: aan de slag aaaAzure SQL Data Warehouse - zelfstudie | Microsoft Docs
description: Deze zelfstudie leert u hoe tooprovision en gegevens laden in Azure SQL Data Warehouse. U leert ook Hallo basisbeginselen van schalen, onderbreken en afstemmen.
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: barbkess
ms.assetid: 52DFC191-E094-4B04-893F-B64D5828A900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: quickstart
ms.date: 01/26/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: edd2a21b0fe49ca8e9792c7c512310339a822c55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-data-warehouse"></a><span data-ttu-id="448b4-104">Aan de slag met SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="448b4-104">Get started with SQL Data Warehouse</span></span>

<span data-ttu-id="448b4-105">Deze zelfstudie laat zien hoe tooprovision en gegevens laden in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="448b4-105">This tutorial shows how tooprovision and load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="448b4-106">U leert ook Hallo basisbeginselen van schalen, onderbreken en afstemmen.</span><span class="sxs-lookup"><span data-stu-id="448b4-106">You’ll also learn hello basics about scaling, pausing, and tuning.</span></span> <span data-ttu-id="448b4-107">Wanneer u klaar bent u klaar tooquery en Verken uw datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="448b4-107">When you’re finished, you’ll be ready tooquery and explore your data warehouse.</span></span>

<span data-ttu-id="448b4-108">**Geschatte tijd toocomplete:** dit is een end-to-end zelfstudie met voorbeeldcode die het duurt ongeveer 30 minuten toocomplete als u Hallo vereisten hebt voldaan.</span><span class="sxs-lookup"><span data-stu-id="448b4-108">**Estimated time toocomplete:** This is an end-to-end tutorial with example code that takes about 30 minutes toocomplete once you have met hello prerequisites.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="448b4-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="448b4-109">Prerequisites</span></span>

<span data-ttu-id="448b4-110">Hallo-zelfstudie wordt ervan uitgegaan dat u bekend bent met de basisconcepten van SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="448b4-110">hello tutorial assumes you are familiar with SQL Data Warehouse basic concepts.</span></span> <span data-ttu-id="448b4-111">Zie [Wat is SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md) als u eerst wat meer informatie nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="448b4-111">If you need an introduction, see [What is SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md)</span></span> 

### <a name="sign-up-for-microsoft-azure"></a><span data-ttu-id="448b4-112">Registreren voor Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="448b4-112">Sign up for Microsoft Azure</span></span>
<span data-ttu-id="448b4-113">Als u nog geen Microsoft Azure-account hebt, moet u toosign voor één toouse deze service.</span><span class="sxs-lookup"><span data-stu-id="448b4-113">If you don't already have a Microsoft Azure account, you need toosign up for one toouse this service.</span></span> <span data-ttu-id="448b4-114">Deze stap kunt u overslaan als u al een account hebt.</span><span class="sxs-lookup"><span data-stu-id="448b4-114">If you already have an account, you may skip this step.</span></span> 

1. <span data-ttu-id="448b4-115">Navigeer toohello account pagina's [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span><span class="sxs-lookup"><span data-stu-id="448b4-115">Navigate toohello account pages [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span></span>
2. <span data-ttu-id="448b4-116">Maak een gratis Azure-account of koop een account.</span><span class="sxs-lookup"><span data-stu-id="448b4-116">Create a free Azure account, or purchase an account.</span></span>
3. <span data-ttu-id="448b4-117">Volg de instructies Hallo</span><span class="sxs-lookup"><span data-stu-id="448b4-117">Follow hello instructions</span></span>

### <a name="install-appropriate-sql-client-drivers-and-tools"></a><span data-ttu-id="448b4-118">Toepasselijke stuurprogramma's en hulpprogramma's installeren voor SQL-client</span><span class="sxs-lookup"><span data-stu-id="448b4-118">Install appropriate SQL client drivers and tools</span></span>

<span data-ttu-id="448b4-119">De meeste hulpprogramma's van SQL-client verbinding kunnen maken voor tooSQL Data Warehouse via JDBC, ODBC- of ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="448b4-119">Most SQL client tools can connect tooSQL Data Warehouse by using JDBC, ODBC, or ADO.NET.</span></span> <span data-ttu-id="448b4-120">Vervaldatum toohello groot aantal functies van T-SQL die ondersteuning biedt voor SQL Data Warehouse, zijn sommige clienttoepassingen niet volledig compatibel is met SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="448b4-120">Due toohello large number of T-SQL features that SQL Data Warehouse supports, some client applications are not fully compatible with SQL Data Warehouse.</span></span>

<span data-ttu-id="448b4-121">Als u een Windows-besturingssysteem gebruikt, raden we u aan te kiezen voor [Visual Studio] of [SQL Server Management Studio].</span><span class="sxs-lookup"><span data-stu-id="448b4-121">If you are running a Windows operating system, we recommend using either [Visual Studio] or [SQL Server Management Studio].</span></span>

[!INCLUDE [Create a new logical server](../../includes/sql-data-warehouse-create-logical-server.md)] 

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="448b4-122">Een SQL Data Warehouse maken</span><span class="sxs-lookup"><span data-stu-id="448b4-122">Create a SQL Data Warehouse</span></span>

<span data-ttu-id="448b4-123">SQL Data Warehouse is een speciaal databasetype dat is ontworpen voor parallelle verwerking op zeer grote schaal.</span><span class="sxs-lookup"><span data-stu-id="448b4-123">A SQL Data Warehouse is a special type of database that is designed for massively parallel processing.</span></span> <span data-ttu-id="448b4-124">Hallo-database is verdeeld over meerdere knooppunten en query's parallel worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="448b4-124">hello database is distributed across multiple nodes and processes queries in parallel.</span></span> <span data-ttu-id="448b4-125">SQL Data Warehouse is een besturingselement-knooppunt dat activiteiten van alle knooppunten in Hallo Hallo ingedeeld.</span><span class="sxs-lookup"><span data-stu-id="448b4-125">SQL Data Warehouse has a control node that orchestrates hello activities of all hello nodes.</span></span> <span data-ttu-id="448b4-126">Hallo-knooppunten zelf uw gegevens toomanage SQL-Database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="448b4-126">hello nodes themselves use SQL Database toomanage your data.</span></span>  

> [!NOTE]
> <span data-ttu-id="448b4-127">Het maken van een SQL Data Warehouse kan een nieuwe factureerbare service tot gevolg hebben.</span><span class="sxs-lookup"><span data-stu-id="448b4-127">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="448b4-128">Zie [Prijzen van SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="448b4-128">For more information, see [SQL Data Warehouse pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>
>

### <a name="create-a-data-warehouse"></a><span data-ttu-id="448b4-129">Een datawarehouse maken</span><span class="sxs-lookup"><span data-stu-id="448b4-129">Create a data warehouse</span></span>

1. <span data-ttu-id="448b4-130">Meld u aan bij Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="448b4-130">Sign into hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="448b4-131">Klik op **Nieuw** > **Databases** > **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="448b4-131">Click **New** > **Databases** > **SQL Data Warehouse**.</span></span>

    <span data-ttu-id="448b4-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span><span class="sxs-lookup"><span data-stu-id="448b4-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span></span>

3. <span data-ttu-id="448b4-133">Vul de implementatiegegevens in</span><span class="sxs-lookup"><span data-stu-id="448b4-133">Fill out deployment details</span></span>

    <span data-ttu-id="448b4-134">**Databasenaam**: kies een naam.</span><span class="sxs-lookup"><span data-stu-id="448b4-134">**Database Name**: Pick anything you'd like.</span></span> <span data-ttu-id="448b4-135">Als u meerdere datawarehouses hebt, raden wij aan uw namen bevatten gegevens zoals Hallo regio, omgeving, bijvoorbeeld *mydw-westus-1-test*.</span><span class="sxs-lookup"><span data-stu-id="448b4-135">If you have multiple data warehouses, we recommend your names include details such as hello region, environment, for example *mydw-westus-1-test*.</span></span>

    <span data-ttu-id="448b4-136">**Abonnement:** uw Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="448b4-136">**Subscription**: Your Azure subscription</span></span>

    <span data-ttu-id="448b4-137">**Resourcegroep**: maak een resourcegroep of gebruik een bestaande resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="448b4-137">**Resource Group**: Create a resource group or use an existing resource group.</span></span>
    > [!NOTE]
    > <span data-ttu-id="448b4-138">Resourcegroepen zijn handig voor het beheren van resources, waaronder het bereik van toegangsbeheer controleren en het implementeren met sjablonen.</span><span class="sxs-lookup"><span data-stu-id="448b4-138">Resource groups are useful for resource administration such as scoping access control and templated deployment.</span></span> <span data-ttu-id="448b4-139">[Hier](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) vindt u meer informatie over resourcegroepen en aanbevolen procedures voor Azure</span><span class="sxs-lookup"><span data-stu-id="448b4-139">Read more about Azure resource groups and best practices [here](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)</span></span>

    <span data-ttu-id="448b4-140">**Bron**: lege database</span><span class="sxs-lookup"><span data-stu-id="448b4-140">**Source**: Blank Database</span></span>

    <span data-ttu-id="448b4-141">**Server**: Selecteer Hallo-server die u hebt gemaakt in [vereisten].</span><span class="sxs-lookup"><span data-stu-id="448b4-141">**Server**: Select hello server you created in [Prerequisites].</span></span>

    <span data-ttu-id="448b4-142">**Sortering**: laat Hallo standaardsortering SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="448b4-142">**Collation**: Leave hello default collation SQL_Latin1_General_CP1_CI_AS.</span></span>

    <span data-ttu-id="448b4-143">**Selecteer prestaties**: het is raadzaam beginnen met het standaard 400DWU Hallo.</span><span class="sxs-lookup"><span data-stu-id="448b4-143">**Select performance**: We recommend starting with hello standard 400DWU.</span></span>

4. <span data-ttu-id="448b4-144">Kies **pincode toodashboard** ![pincode tooDashboard](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="448b4-144">Choose **Pin toodashboard** ![Pin tooDashboard](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span></span>

5. <span data-ttu-id="448b4-145">Terug zitten en wachten op uw datawarehouse toodeploy!</span><span class="sxs-lookup"><span data-stu-id="448b4-145">Sit back and wait for your data warehouse toodeploy!</span></span> <span data-ttu-id="448b4-146">Dit is normaal voor dit proces tootake enkele minuten.</span><span class="sxs-lookup"><span data-stu-id="448b4-146">It's normal for this process tootake several minutes.</span></span> <span data-ttu-id="448b4-147">Hallo portal waarschuwt u als uw datawarehouse gereed toouse is.</span><span class="sxs-lookup"><span data-stu-id="448b4-147">hello portal notifies you when your data warehouse is ready toouse.</span></span> 

## <a name="connect-toosql-data-warehouse"></a><span data-ttu-id="448b4-148">Verbinding maken met tooSQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="448b4-148">Connect tooSQL Data Warehouse</span></span>

<span data-ttu-id="448b4-149">Deze zelfstudie maakt gebruik van SQL Server Management Studio (SSMS) tooconnect toohello-datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="448b4-149">This tutorial uses SQL Server Management Studio (SSMS) tooconnect toohello data warehouse.</span></span> <span data-ttu-id="448b4-150">TooSQL Data Warehouse verbinding kunnen maken via deze ondersteunde connectors: ADO.NET, JDBC, ODBC- en PHP.</span><span class="sxs-lookup"><span data-stu-id="448b4-150">You can connect tooSQL Data Warehouse through these supported connectors: ADO.NET, JDBC, ODBC, and PHP.</span></span> <span data-ttu-id="448b4-151">Let op: de functionaliteit van hulpprogramma's die niet door Microsoft worden ondersteund, is mogelijk beperkt.</span><span class="sxs-lookup"><span data-stu-id="448b4-151">Remember, functionality might be limited for tools that are not supported by Microsoft.</span></span>


### <a name="get-connection-information"></a><span data-ttu-id="448b4-152">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="448b4-152">Get connection information</span></span>

<span data-ttu-id="448b4-153">tooconnect tooyour datawarehouse, moet u tooconnect via Hallo logische SQL-server u hebt gemaakt in [vereisten].</span><span class="sxs-lookup"><span data-stu-id="448b4-153">tooconnect tooyour data warehouse, you need tooconnect through hello logical SQL server you created in [Prerequisites].</span></span>

1. <span data-ttu-id="448b4-154">Selecteer uw datawarehouse in Hallo dashboard of zoekt u het in uw resources.</span><span class="sxs-lookup"><span data-stu-id="448b4-154">Select your data warehouse from hello dashboard or search for it in your resources.</span></span>

    ![Dashboard van SQL Data Warehouse](./media/sql-data-warehouse-get-started-tutorial/sql-dw-dashboard.png)

2. <span data-ttu-id="448b4-156">Volledige naam van de Hallo voor Hallo logische SQL-server vinden.</span><span class="sxs-lookup"><span data-stu-id="448b4-156">Find hello full name for hello logical SQL server.</span></span>

    ![Servernaam selecteren](./media/sql-data-warehouse-get-started-tutorial/select-server.png)

3. <span data-ttu-id="448b4-158">SSMS openen en gebruiken van object explorer tooconnect toothis server met behulp van Hallo server admin-referenties die u hebt gemaakt in [vereisten]</span><span class="sxs-lookup"><span data-stu-id="448b4-158">Open SSMS and use object explorer tooconnect toothis server using hello server admin credentials you created in [Prerequisites]</span></span>

    ![Verbinden met SSMS](./media/sql-data-warehouse-get-started-tutorial/ssms-connect.png)

<span data-ttu-id="448b4-160">Als alles goed gaat, moet u nu verbonden tooyour logische SQL-server.</span><span class="sxs-lookup"><span data-stu-id="448b4-160">If all goes correctly, you should now be connected tooyour logical SQL server.</span></span> <span data-ttu-id="448b4-161">Aangezien u aangemeld als serverbeheerder hello, kunt u tooany database gehost door Hallo-server, inclusief Hallo-hoofddatabase.</span><span class="sxs-lookup"><span data-stu-id="448b4-161">Since you logged in as hello server admin, you can connect tooany database hosted by hello server, including hello master database.</span></span> 

<span data-ttu-id="448b4-162">Er is slechts één server-beheerdersaccount en de meeste bevoegdheden van een gebruiker Hallo heeft.</span><span class="sxs-lookup"><span data-stu-id="448b4-162">There is only one server admin account and it has hello most privileges of any user.</span></span> <span data-ttu-id="448b4-163">Wees voorzichtig niet tooallow te veel mensen in uw organisatie tooknow Hallo admin-wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="448b4-163">Be careful not tooallow too many people in your organization tooknow hello admin password.</span></span> 

<span data-ttu-id="448b4-164">U kunt ook een Azure Active Directory-beheerdersaccount hebben.</span><span class="sxs-lookup"><span data-stu-id="448b4-164">You can also have an Azure active directory admin account.</span></span> <span data-ttu-id="448b4-165">Wij niet hier Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="448b4-165">We don't provide hello details here.</span></span> <span data-ttu-id="448b4-166">Als u toolearn meer wilt over het gebruik van Azure Active Directory-verificatie, Zie [Azure AD authentication](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span><span class="sxs-lookup"><span data-stu-id="448b4-166">If you want toolearn more about using Azure Active Directory authentication, see [Azure AD authentication](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span></span>

<span data-ttu-id="448b4-167">Hierna bespreken we het maken van extra aanmeldingen en gebruikers.</span><span class="sxs-lookup"><span data-stu-id="448b4-167">Next, we explore creating additional logins and users.</span></span>


## <a name="create-a-database-user"></a><span data-ttu-id="448b4-168">Een databasegebruiker maken</span><span class="sxs-lookup"><span data-stu-id="448b4-168">Create a database user</span></span>

<span data-ttu-id="448b4-169">In deze stap maakt u een gebruiker account tooaccess uw datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="448b4-169">In this step, you create a user account tooaccess your data warehouse.</span></span> <span data-ttu-id="448b4-170">We ook ziet u hoe toogive die gebruiker Hallo mogelijkheid toorun query's met een grote hoeveelheid geheugen en CPU-resources.</span><span class="sxs-lookup"><span data-stu-id="448b4-170">We also show you how toogive that user hello ability toorun queries with a large amount of memory and CPU resources.</span></span>

### <a name="notes-about-resource-classes-for-allocating-resources-tooqueries"></a><span data-ttu-id="448b4-171">Opmerkingen over de resource-klassen voor het toewijzen van resources tooqueries</span><span class="sxs-lookup"><span data-stu-id="448b4-171">Notes about resource classes for allocating resources tooqueries</span></span>

- <span data-ttu-id="448b4-172">tookeep het gebruik van uw gegevens beschermen, niet Hallo server admin toorun-query's op uw productiedatabases.</span><span class="sxs-lookup"><span data-stu-id="448b4-172">tookeep your data safe, don't use hello server admin toorun queries on your production databases.</span></span> <span data-ttu-id="448b4-173">Hieraan Hallo meeste bevoegdheden van een gebruiker en gebruik van tooperform brengt bewerkingen op gegevens van gebruiker met uw gegevens in gevaar.</span><span class="sxs-lookup"><span data-stu-id="448b4-173">It has hello most privileges of any user and using it tooperform operations on user data puts your data at risk.</span></span> <span data-ttu-id="448b4-174">Ook omdat Hallo serverbeheerder is tooperform beheerbewerkingen bedoeld, voert deze bewerkingen met slechts een kleine toewijzing van geheugen en CPU-resources.</span><span class="sxs-lookup"><span data-stu-id="448b4-174">Also, since hello server admin is meant tooperform management operations, it runs operations with only a small allocation of memory and CPU resources.</span></span> 

- <span data-ttu-id="448b4-175">SQL Data Warehouse maakt gebruik van vooraf gedefinieerde databaserollen resource klassen, tooallocate verschillende hoeveelheden geheugen, CPU-bronnen en gelijktijdigheid sleuven toousers aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="448b4-175">SQL Data Warehouse uses pre-defined database roles, called resource classes, tooallocate different amounts of memory, CPU resources, and concurrency slots toousers.</span></span> <span data-ttu-id="448b4-176">Elke gebruiker kan tooa klein, normaal, groot of extra groot bronklasse behoren.</span><span class="sxs-lookup"><span data-stu-id="448b4-176">Each user can belong tooa small, medium, large, or extra-large resource class.</span></span> <span data-ttu-id="448b4-177">Hallo van gebruiker bronklasse bepaalt Hallo resources Hallo gebruiker heeft toorun query's en bewerkingen worden geladen.</span><span class="sxs-lookup"><span data-stu-id="448b4-177">hello user's resource class determines hello resources hello user has toorun queries and load operations.</span></span>

- <span data-ttu-id="448b4-178">Voor optimale gegevenscompressie, Hallo gebruiker mogelijk tooload grote of extra groot toewijzingen.</span><span class="sxs-lookup"><span data-stu-id="448b4-178">For optimal data compression, hello user may need tooload with large or extra large resource allocations.</span></span> <span data-ttu-id="448b4-179">Meer informatie over resourceklassen vindt u [hier](./sql-data-warehouse-develop-concurrency.md#resource-classes):</span><span class="sxs-lookup"><span data-stu-id="448b4-179">Read more about resource classes [here](./sql-data-warehouse-develop-concurrency.md#resource-classes):</span></span>

### <a name="create-an-account-that-can-control-a-database"></a><span data-ttu-id="448b4-180">Een account maken waarmee een database kan worden beheerd</span><span class="sxs-lookup"><span data-stu-id="448b4-180">Create an account that can control a database</span></span>

<span data-ttu-id="448b4-181">Nadat u bent momenteel aangemeld in Hallo serverbeheerder hebt machtigingen toocreate aanmeldingen en gebruikers.</span><span class="sxs-lookup"><span data-stu-id="448b4-181">Since you are currently logged in as hello server admin you have permissions toocreate logins and users.</span></span>

1. <span data-ttu-id="448b4-182">Open een nieuwe query voor **Hoofd** met behulp van SSMS of een andere queryclient.</span><span class="sxs-lookup"><span data-stu-id="448b4-182">Using SSMS or another query client, open a new query for **master**.</span></span>

    ![Nieuwe query in Hoofd](./media/sql-data-warehouse-get-started-tutorial/query-on-server.png)

    ![Nieuwe query in Hoofd1](./media/sql-data-warehouse-get-started-tutorial/query-on-master.png)

2. <span data-ttu-id="448b4-185">Voer in het queryvenster Hallo, deze toocreate T-SQL-opdracht een aanmelding met de naam MedRCLogin en een gebruiker met de naam LoadingUser.</span><span class="sxs-lookup"><span data-stu-id="448b4-185">In hello query window, run this T-SQL command toocreate a login named MedRCLogin and user named LoadingUser.</span></span> <span data-ttu-id="448b4-186">Deze aanmelding kan verbinding maken toohello logische SQL-server.</span><span class="sxs-lookup"><span data-stu-id="448b4-186">This login can connect toohello logical SQL server.</span></span>

    ```sql
    CREATE LOGIN MedRCLogin WITH PASSWORD = 'a123reallySTRONGpassword!';
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

3. <span data-ttu-id="448b4-187">Nu opvragen Hallo *SQL Data Warehouse-database*, op basis van een database-gebruikersaccount maken Hallo aanmelding u tooaccess gemaakt en worden bewerkingen uitvoeren op Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="448b4-187">Now querying hello *SQL Data Warehouse database*, create a database user based on hello login you created tooaccess and perform operations on hello database.</span></span>

    ```sql
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

4. <span data-ttu-id="448b4-188">Hallo database gebruiker besturingselement machtigingen toohello database aangeroepen NYT geven.</span><span class="sxs-lookup"><span data-stu-id="448b4-188">Give hello database user control permissions toohello database called NYT.</span></span> 

    ```sql
    GRANT CONTROL ON DATABASE::[NYT] tooLoadingUser;
    ```
    > [!NOTE]
    > <span data-ttu-id="448b4-189">Als de databasenaam van uw afbreekstreepjes in het heeft, moet u ervoor toowrap deze haakjes!</span><span class="sxs-lookup"><span data-stu-id="448b4-189">If your database name has hyphens in it, be sure toowrap it in brackets!</span></span> 
    >

### <a name="give-hello-user-medium-resource-allocations"></a><span data-ttu-id="448b4-190">Hallo gebruiker gemiddeld toewijzingen geven</span><span class="sxs-lookup"><span data-stu-id="448b4-190">Give hello user medium resource allocations</span></span>

1. <span data-ttu-id="448b4-191">Voer deze opdracht T-SQL toomake deze in een lid van Hallo gemiddeld resourceklasse, mediumrc wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="448b4-191">Run this T-SQL command toomake it a member of hello medium resource class, which is called mediumrc.</span></span> 

    ```sql
    EXEC sp_addrolemember 'mediumrc', 'LoadingUser';
    ```
    > [!NOTE]
    > <span data-ttu-id="448b4-192">Klik op [hier](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn meer informatie over klassen gelijktijdigheid van taken en resource!</span><span class="sxs-lookup"><span data-stu-id="448b4-192">Click [here](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn more about concurrency and resource classes!</span></span> 
    >

2. <span data-ttu-id="448b4-193">Toohello logische server verbinden met de nieuwe referenties Hallo</span><span class="sxs-lookup"><span data-stu-id="448b4-193">Connect toohello logical server with hello new credentials</span></span>

    ![Aanmelden met nieuwe aanmeldgegevens](./media/sql-data-warehouse-get-started-tutorial/new-login.png)


## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="448b4-195">Gegevens laden vanuit Azure-blobopslag</span><span class="sxs-lookup"><span data-stu-id="448b4-195">Load data from Azure blob storage</span></span>

<span data-ttu-id="448b4-196">U bent nu klaar tooload gegevens in uw datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="448b4-196">You are now ready tooload data into your data warehouse.</span></span> <span data-ttu-id="448b4-197">Deze stap ziet u hoe tooload New York City taxi CAB-bestand van een openbare Azure-opslag-blob.</span><span class="sxs-lookup"><span data-stu-id="448b4-197">This step shows you how tooload New York City taxi cab data from a public Azure storage blob.</span></span> 

- <span data-ttu-id="448b4-198">Een veelgebruikte manier tooload gegevens in SQL Data Warehouse is toofirst Hallo gegevens tooAzure blob-opslag verplaatsen en vervolgens in uw datawarehouse te laden.</span><span class="sxs-lookup"><span data-stu-id="448b4-198">A common way tooload data into SQL Data Warehouse is toofirst move hello data tooAzure blob storage, and then load it into your data warehouse.</span></span> <span data-ttu-id="448b4-199">toomake deze eenvoudiger toounderstand hoe tooload, hebben we Den Haag taxi cab-gegevens die al worden gehost in een openbare Azure-opslag-blob.</span><span class="sxs-lookup"><span data-stu-id="448b4-199">toomake it easier toounderstand how tooload, we have New York taxi cab data already hosted in a public Azure storage blob.</span></span> 

- <span data-ttu-id="448b4-200">Voor toekomstig gebruik, toolearn hoe tooget uw gegevens tooAzure blob-opslag- of deze rechtstreeks vanuit uw bron in SQL Data Warehouse, Zie tooload hello [laden overzicht](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="448b4-200">For future reference, toolearn how tooget your data tooAzure blob storage or tooload it directly from your source into SQL Data Warehouse, see hello [loading overview](sql-data-warehouse-overview-load.md).</span></span>


### <a name="define-external-data"></a><span data-ttu-id="448b4-201">Externe gegevens definiëren</span><span class="sxs-lookup"><span data-stu-id="448b4-201">Define external data</span></span>

1. <span data-ttu-id="448b4-202">Maak een hoofdsleutel.</span><span class="sxs-lookup"><span data-stu-id="448b4-202">Create a master key.</span></span> <span data-ttu-id="448b4-203">U hoeft alleen toocreate een hoofdsleutel eenmaal per database.</span><span class="sxs-lookup"><span data-stu-id="448b4-203">You only need toocreate a master key once per database.</span></span> 

    ```sql
    CREATE MASTER KEY;
    ```

2. <span data-ttu-id="448b4-204">Hallo-locatie van hello Azure blob met Hallo taxi CAB-bestand gegevens definiëren.</span><span class="sxs-lookup"><span data-stu-id="448b4-204">Define hello location of hello Azure blob that contains hello taxi cab data.</span></span>  

    ```sql
    CREATE EXTERNAL DATA SOURCE NYTPublic
    WITH
    (
        TYPE = Hadoop,
        LOCATION = 'wasbs://2013@nytpublic.blob.core.windows.net/'
    );
    ```

3. <span data-ttu-id="448b4-205">Hallo externe bestandsindelingen definiëren</span><span class="sxs-lookup"><span data-stu-id="448b4-205">Define hello external file formats</span></span>

    <span data-ttu-id="448b4-206">Hallo ```CREATE EXTERNAL FILE FORMAT``` opdracht is gebruikte toospecify de indeling van de bestanden die Hallo externe gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="448b4-206">hello ```CREATE EXTERNAL FILE FORMAT``` command is used toospecify the format of files that contain hello external data.</span></span> <span data-ttu-id="448b4-207">Ze bevatten tekst gescheiden door een of meer tekens, genaamd scheidingstekens.</span><span class="sxs-lookup"><span data-stu-id="448b4-207">They contain text separated by one or more characters called delimiters.</span></span> <span data-ttu-id="448b4-208">Voor demonstratiedoeleinden Hallo taxi CAB-bestand gegevens opgeslagen als niet-gecomprimeerde gegevens en als gzip gecomprimeerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="448b4-208">For demonstration purposes, hello taxi cab data is stored both as uncompressed data and as gzip compressed data.</span></span>

    <span data-ttu-id="448b4-209">Voer deze opdrachten T-SQL toodefine twee verschillende indelingen: niet-gecomprimeerd en gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="448b4-209">Run these T-SQL commands toodefine two different formats: uncompressed and compressed.</span></span>

    ```sql
    CREATE EXTERNAL FILE FORMAT uncompressedcsv
    WITH (
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( 
            FIELD_TERMINATOR = ',',
            STRING_DELIMITER = '',
            DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        )
    );

    CREATE EXTERNAL FILE FORMAT compressedcsv
    WITH ( 
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( FIELD_TERMINATOR = '|',
            STRING_DELIMITER = '',
        DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        ),
        DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
    );
    ```

4.  <span data-ttu-id="448b4-210">Maak een schema voor de externe bestandsindeling.</span><span class="sxs-lookup"><span data-stu-id="448b4-210">Create a schema for your external file format.</span></span> 

    ```sql
    CREATE SCHEMA ext;
    ```
5. <span data-ttu-id="448b4-211">Hallo externe tabellen maken.</span><span class="sxs-lookup"><span data-stu-id="448b4-211">Create hello external tables.</span></span> <span data-ttu-id="448b4-212">Deze tabellen verwijzen naar gegevens die zijn opgeslagen in Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="448b4-212">These tables reference data stored in Azure blob storage.</span></span> <span data-ttu-id="448b4-213">Hallo T-SQL-opdrachten toocreate na enkele externe tabellen dat alle punt toohello Azure blob we eerder in onze externe gegevensbron gedefinieerde uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="448b4-213">Run hello following T-SQL commands toocreate several external tables that all point toohello Azure blob we defined previously in our external data source.</span></span>

```sql
    CREATE EXTERNAL TABLE [ext].[Date] 
    (
        [DateID] int NOT NULL,
        [Date] datetime NULL,
        [DateBKey] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DaySuffix] varchar(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeek] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfQuarter] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfYear] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfMonth] varchar(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Month] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Quarter] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [QuarterName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Year] char(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [YearName] char(7) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthYear] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MMYYYY] char(6) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FirstDayOfMonth] date NULL,
        [LastDayOfMonth] date NULL,
        [FirstDayOfQuarter] date NULL,
        [LastDayOfQuarter] date NULL,
        [FirstDayOfYear] date NULL,
        [LastDayOfYear] date NULL,
        [IsHolidayUSA] bit NULL,
        [IsWeekday] bit NULL,
        [HolidayUSA] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Date',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    );
    
    CREATE EXTERNAL TABLE [ext].[Geography]
    (
        [GeographyID] int NOT NULL,
        [ZipCodeBKey] varchar(10) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [County] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [City] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [State] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Country] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [ZipCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Geography',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0 
    );
        
    
    CREATE EXTERNAL TABLE [ext].[HackneyLicense]
    (
        [HackneyLicenseID] int NOT NULL,
        [HackneyLicenseBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HackneyLicenseCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'HackneyLicense',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    
    CREATE EXTERNAL TABLE [ext].[Medallion]
    (
        [MedallionID] int NOT NULL,
        [MedallionBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [MedallionCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Medallion',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    CREATE EXTERNAL TABLE [ext].[Time]
    (
        [TimeID] int NOT NULL,
        [TimeBKey] varchar(8) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HourNumber] tinyint NOT NULL,
        [MinuteNumber] tinyint NOT NULL,
        [SecondNumber] tinyint NOT NULL,
        [TimeInSecond] int NOT NULL,
        [HourlyBucket] varchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [DayTimeBucketGroupKey] int NOT NULL,
        [DayTimeBucket] varchar(100) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL
    )
    WITH
    (
        LOCATION = 'Time',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    
    CREATE EXTERNAL TABLE [ext].[Trip]
    (
        [DateID] int NOT NULL,
        [MedallionID] int NOT NULL,
        [HackneyLicenseID] int NOT NULL,
        [PickupTimeID] int NOT NULL,
        [DropoffTimeID] int NOT NULL,
        [PickupGeographyID] int NULL,
        [DropoffGeographyID] int NULL,
        [PickupLatitude] float NULL,
        [PickupLongitude] float NULL,
        [PickupLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DropoffLatitude] float NULL,
        [DropoffLongitude] float NULL,
        [DropoffLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [PassengerCount] int NULL,
        [TripDurationSeconds] int NULL,
        [TripDistanceMiles] float NULL,
        [PaymentType] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FareAmount] money NULL,
        [SurchargeAmount] money NULL,
        [TaxAmount] money NULL,
        [TipAmount] money NULL,
        [TollsAmount] money NULL,
        [TotalAmount] money NULL
    )
    WITH
    (
        LOCATION = 'Trip2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = compressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    CREATE EXTERNAL TABLE [ext].[Weather]
    (
        [DateID] int NOT NULL,
        [GeographyID] int NOT NULL,
        [PrecipitationInches] float NOT NULL,
        [AvgTemperatureFahrenheit] float NOT NULL
    )
    WITH
    (
        LOCATION = 'Weather2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
```

### <a name="import-hello-data-from-azure-blob-storage"></a><span data-ttu-id="448b4-214">Hallo-gegevens importeren uit Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="448b4-214">Import hello data from Azure blob storage.</span></span>

<span data-ttu-id="448b4-215">SQL Data Warehouse ondersteunt een sleutelinstructie met de naam CREATE TABLE AS SELECT (CTAS).</span><span class="sxs-lookup"><span data-stu-id="448b4-215">SQL Data Warehouse supports a key statement called CREATE TABLE AS SELECT (CTAS).</span></span> <span data-ttu-id="448b4-216">Deze instructie maakt een nieuwe tabel op basis van Hallo resultaten van een select-instructie.</span><span class="sxs-lookup"><span data-stu-id="448b4-216">This statement creates a new table based on hello results of a select statement.</span></span> <span data-ttu-id="448b4-217">Hallo nieuwe tabel heeft dezelfde kolommen en gegevenstypen Hallo Hallo resultaten van Hallo selecteert u de instructie.</span><span class="sxs-lookup"><span data-stu-id="448b4-217">hello new table has hello same columns and data types as hello results of hello select statement.</span></span>  <span data-ttu-id="448b4-218">Dit is een elegante manier tooimport gegevens uit Azure blob storage in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="448b4-218">This is an elegant way tooimport data from Azure blob storage into SQL Data Warehouse.</span></span>

1. <span data-ttu-id="448b4-219">Voer dit script tooimport uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="448b4-219">Run this script tooimport your data.</span></span>

    ```sql
    CREATE TABLE [dbo].[Date]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Date]
    OPTION (LABEL = 'CTAS : Load [dbo].[Date]')
    ;
    
    CREATE TABLE [dbo].[Geography]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS
    SELECT * FROM [ext].[Geography]
    OPTION (LABEL = 'CTAS : Load [dbo].[Geography]')
    ;
    
    CREATE TABLE [dbo].[HackneyLicense]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[HackneyLicense]
    OPTION (LABEL = 'CTAS : Load [dbo].[HackneyLicense]')
    ;
    
    CREATE TABLE [dbo].[Medallion]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Medallion]
    OPTION (LABEL = 'CTAS : Load [dbo].[Medallion]')
    ;
    
    CREATE TABLE [dbo].[Time]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Time]
    OPTION (LABEL = 'CTAS : Load [dbo].[Time]')
    ;
    
    CREATE TABLE [dbo].[Weather]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Weather]
    OPTION (LABEL = 'CTAS : Load [dbo].[Weather]')
    ;
    
    CREATE TABLE [dbo].[Trip]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Trip]
    OPTION (LABEL = 'CTAS : Load [dbo].[Trip]')
    ;
    ```

2. <span data-ttu-id="448b4-220">Bekijk uw gegevens tijdens het laden.</span><span class="sxs-lookup"><span data-stu-id="448b4-220">View your data as it loads.</span></span>

   <span data-ttu-id="448b4-221">U laadt meerdere GB's aan gegevens en comprimeert die tot hoogwaardige geclusterde columnstore-indexen.</span><span class="sxs-lookup"><span data-stu-id="448b4-221">You’re loading several GBs of data and compressing it into highly performant clustered columnstore indexes.</span></span> <span data-ttu-id="448b4-222">Hallo volgende query worden uitgevoerd die gebruikmaakt van een dynamische Beheerweergave weergaven (DMV's) tooshow Hallo status Hallo belast.</span><span class="sxs-lookup"><span data-stu-id="448b4-222">Run hello following query that uses a dynamic management views (DMVs) tooshow hello status of hello load.</span></span> <span data-ttu-id="448b4-223">Na het starten van de query Hallo halen een koffie en een gevulde terwijl SQL Data Warehouse enkele zware werk bevat.</span><span class="sxs-lookup"><span data-stu-id="448b4-223">After starting hello query, grab a coffee and a snack while SQL Data Warehouse does some heavy lifting.</span></span>
    
    ```sql
    SELECT
        r.command,
        s.request_id,
        r.status,
        count(distinct input_name) as nbr_files,
        sum(s.bytes_processed)/1024/1024/1024 as gb_processed
    FROM 
        sys.dm_pdw_exec_requests r
        INNER JOIN sys.dm_pdw_dms_external_work s
        ON r.request_id = s.request_id
    WHERE
        r.[label] = 'CTAS : Load [dbo].[Date]' OR
        r.[label] = 'CTAS : Load [dbo].[Geography]' OR
        r.[label] = 'CTAS : Load [dbo].[HackneyLicense]' OR
        r.[label] = 'CTAS : Load [dbo].[Medallion]' OR
        r.[label] = 'CTAS : Load [dbo].[Time]' OR
        r.[label] = 'CTAS : Load [dbo].[Weather]' OR
        r.[label] = 'CTAS : Load [dbo].[Trip]'
    GROUP BY
        r.command,
        s.request_id,
        r.status
    ORDER BY
        nbr_files desc, 
        gb_processed desc;
    ```

3. <span data-ttu-id="448b4-224">Bekijk alle systeemquery's.</span><span class="sxs-lookup"><span data-stu-id="448b4-224">View all system queries.</span></span>

    ```sql
    SELECT * FROM sys.dm_pdw_exec_requests;
    ```

4. <span data-ttu-id="448b4-225">Al uw gegevens zijn netjes geladen in uw Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="448b4-225">Enjoy seeing your data nicely loaded into your Azure SQL Data Warehouse.</span></span>

    ![Geladen gegevens bekijken](./media/sql-data-warehouse-get-started-tutorial/see-data-loaded.png)


## <a name="improve-query-performance"></a><span data-ttu-id="448b4-227">Queryprestaties verbeteren</span><span class="sxs-lookup"><span data-stu-id="448b4-227">Improve query performance</span></span>

<span data-ttu-id="448b4-228">Er zijn verschillende manieren tooimprove prestaties van query's en tooachieve Hallo snelle prestaties van SQL Data Warehouse tooprovide ontworpen.</span><span class="sxs-lookup"><span data-stu-id="448b4-228">There are several ways tooimprove query performance and tooachieve hello high-speed performance that SQL Data Warehouse is designed tooprovide.</span></span>  

### <a name="see-hello-effect-of-scaling-on-query-performance"></a><span data-ttu-id="448b4-229">Zie Hallo effect van het schalen van op de prestaties van query 's</span><span class="sxs-lookup"><span data-stu-id="448b4-229">See hello effect of scaling on query performance</span></span> 

<span data-ttu-id="448b4-230">Eenzijdige tooimprove queryprestaties is tooscale bronnen door Hallo DWU-serviceniveau voor uw datawarehouse wijzigen.</span><span class="sxs-lookup"><span data-stu-id="448b4-230">One way tooimprove query performance is tooscale resources by changing hello DWU service level for your data warehouse.</span></span> <span data-ttu-id="448b4-231">Elk serviceniveau kost meer, maar u kunt op elk gewenst moment terugschalen of resources onderbreken.</span><span class="sxs-lookup"><span data-stu-id="448b4-231">Each service level costs more, but you can scale back or pause resources at any time.</span></span> 

<span data-ttu-id="448b4-232">In deze stap vergelijkt u de prestaties bij twee verschillende DWU-instellingen.</span><span class="sxs-lookup"><span data-stu-id="448b4-232">In this step, you compare performance at two different DWU settings.</span></span>

<span data-ttu-id="448b4-233">Eerst schalen we Hallo sizing omlaag too100 DWU zodat we een beter beeld van hoe een rekenknooppunt krijgt op zichzelf uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="448b4-233">First, let's scale hello sizing down too100 DWU so we can get an idea of how one compute node might perform on its own.</span></span>

1. <span data-ttu-id="448b4-234">Ga toohello portal en selecteer uw SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="448b4-234">Go toohello portal and select your SQL Data Warehouse.</span></span>

2. <span data-ttu-id="448b4-235">Selecteer schaal in de blade SQL Data Warehouse Hallo.</span><span class="sxs-lookup"><span data-stu-id="448b4-235">Select scale in hello SQL Data Warehouse blade.</span></span> 

    ![DW schalen vanuit de portal](./media/sql-data-warehouse-get-started-tutorial/scale-dw.png)

3. <span data-ttu-id="448b4-237">Hallo-prestaties balk too100 DWU terugschroeven en klik op opslaan.</span><span class="sxs-lookup"><span data-stu-id="448b4-237">Scale down hello performance bar too100 DWU and hit save.</span></span>

    ![Schalen en opslaan](./media/sql-data-warehouse-get-started-tutorial/scale-and-save.png)

4. <span data-ttu-id="448b4-239">Wacht tot de schaal bewerking toofinish.</span><span class="sxs-lookup"><span data-stu-id="448b4-239">Wait for your scale operation toofinish.</span></span>

    > [!NOTE]
    > <span data-ttu-id="448b4-240">Query's kunnen niet worden uitgevoerd tijdens het Hallo schaal wijzigen.</span><span class="sxs-lookup"><span data-stu-id="448b4-240">Queries cannot run while changing hello scale.</span></span> <span data-ttu-id="448b4-241">Het schalen **beëindigt** uw huidige actieve query's.</span><span class="sxs-lookup"><span data-stu-id="448b4-241">Scaling **kills** your currently running queries.</span></span> <span data-ttu-id="448b4-242">U kunt ze opnieuw wanneer het Hallo-bewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="448b4-242">You can restart them when hello operation is finished.</span></span>
    >
    
5. <span data-ttu-id="448b4-243">Voer een scanbewerking op Hallo reis gegevens, Hallo bovenste miljoen vermeldingen voor alle Hallo kolommen te selecteren.</span><span class="sxs-lookup"><span data-stu-id="448b4-243">Do a scan operation on hello trip data, selecting hello top million entries for all hello columns.</span></span> <span data-ttu-id="448b4-244">Als u meteen toomove snel op bent, kunt u gratis tooselect minder rijen.</span><span class="sxs-lookup"><span data-stu-id="448b4-244">If you're eager toomove on quickly, feel free tooselect fewer rows.</span></span> <span data-ttu-id="448b4-245">Let op Hallo duurt toorun deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="448b4-245">Take note of hello time it takes toorun this operation.</span></span>

    ```sql
    SELECT TOP(1000000) * FROM dbo.[Trip]
    ```
6. <span data-ttu-id="448b4-246">Schalen van uw datawarehouse back-too400 DWU.</span><span class="sxs-lookup"><span data-stu-id="448b4-246">Scale your data warehouse back too400 DWU.</span></span> <span data-ttu-id="448b4-247">Denk eraan dat elke 100 DWU is het toevoegen van een andere compute knooppunt tooyour Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="448b4-247">Remember, each 100 DWU is adding another compute node tooyour Azure SQL Data Warehouse.</span></span>

7. <span data-ttu-id="448b4-248">Hallo query opnieuw uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="448b4-248">Run hello query again!</span></span> <span data-ttu-id="448b4-249">U zou een duidelijk verschil moeten zien.</span><span class="sxs-lookup"><span data-stu-id="448b4-249">You should notice a significant difference.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="448b4-250">Omdat Hallo query een grote hoeveelheid gegevens retourneert, mogelijk Hallo bandbreedte beschikbaarheid van SSMS machine Hallo een prestatieknelpunt.</span><span class="sxs-lookup"><span data-stu-id="448b4-250">Because hello query returns a lot of data, hello bandwidth availability of hello machine running SSMS may be a performance bottleneck.</span></span> <span data-ttu-id="448b4-251">Dit kan tot gevolg hebben dat er helemaal geen sprake is van prestatieverbetering!</span><span class="sxs-lookup"><span data-stu-id="448b4-251">This can result in you not seeing any performance improvements!</span></span>

> [!NOTE]
> <span data-ttu-id="448b4-252">SQL Data Warehouse gebruikt MPP (Massively Parallel Processing).</span><span class="sxs-lookup"><span data-stu-id="448b4-252">Since SQL Data Warehouse uses massively parallel processing.</span></span> <span data-ttu-id="448b4-253">Query's die bij het scannen of analytische functies uitvoeren op miljoenen rijen ervaren Hallo true kracht van Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="448b4-253">Queries that scan or perform analytic functions on millions of rows experience hello true power of Azure SQL Data Warehouse.</span></span>
>

### <a name="see-hello-effect-of-statistics-on-query-performance"></a><span data-ttu-id="448b4-254">Zie Hallo effect van statistieken op de prestaties van query 's</span><span class="sxs-lookup"><span data-stu-id="448b4-254">See hello effect of statistics on query performance</span></span>

1. <span data-ttu-id="448b4-255">Voer een query dat joins datum-tabel met de Hallo reis tabel Hallo</span><span class="sxs-lookup"><span data-stu-id="448b4-255">Run a query that joins hello Date table with hello Trip table</span></span>

    ```sql
    SELECT TOP (1000000) 
        dt.[DayOfWeek],
        tr.[MedallionID],
        tr.[HackneyLicenseID],
        tr.[PickupTimeID],
        tr.[DropoffTimeID],
        tr.[PickupGeographyID],
        tr.[DropoffGeographyID],
        tr.[PickupLatitude],
        tr.[PickupLongitude],
        tr.[PickupLatLong],
        tr.[DropoffLatitude],
        tr.[DropoffLongitude],
        tr.[DropoffLatLong],
        tr.[PassengerCount],
        tr.[TripDurationSeconds],
        tr.[TripDistanceMiles],
        tr.[PaymentType],
        tr.[FareAmount],
        tr.[SurchargeAmount],
        tr.[TaxAmount],
        tr.[TipAmount],
        tr.[TollsAmount],
        tr.[TotalAmount]
    FROM [dbo].[Trip] as tr
        JOIN dbo.[Date] as dt
        ON  tr.DateID = dt.DateID
    ```

    <span data-ttu-id="448b4-256">Deze query heeft een tijdje omdat SQL Data Warehouse tooshuffle gegevens heeft voordat het Hallo join kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="448b4-256">This query takes a while because SQL Data Warehouse has tooshuffle data before it can perform hello join.</span></span> <span data-ttu-id="448b4-257">Joins geen tooshuffle gegevens als ze ontworpen toojoin gegevens in Hallo zijn dezelfde manier als deze is gedistribueerd.</span><span class="sxs-lookup"><span data-stu-id="448b4-257">Joins do not have tooshuffle data if they are designed toojoin data in hello same way it is distributed.</span></span> <span data-ttu-id="448b4-258">Dat is een ingewikkelder onderwerp.</span><span class="sxs-lookup"><span data-stu-id="448b4-258">That's a deeper subject.</span></span> 

2. <span data-ttu-id="448b4-259">Statistieken maken een groot verschil.</span><span class="sxs-lookup"><span data-stu-id="448b4-259">Statistics make a difference.</span></span> 
3. <span data-ttu-id="448b4-260">Deze instructie toocreate statistieken worden uitgevoerd op Hallo join-kolommen.</span><span class="sxs-lookup"><span data-stu-id="448b4-260">Run this statement toocreate statistics on hello join columns.</span></span>

    ```sql
    CREATE STATISTICS [dbo.Date DateID stats] ON dbo.Date (DateID);
    CREATE STATISTICS [dbo.Trip DateID stats] ON dbo.Trip (DateID);
    ```

    > [!NOTE]
    > <span data-ttu-id="448b4-261">SQL DW beheert niet automatisch statistieken voor u.</span><span class="sxs-lookup"><span data-stu-id="448b4-261">SQL DW does not automatically manage statistics for you.</span></span> <span data-ttu-id="448b4-262">Statistieken zijn belangrijk voor de prestaties van query's en we raden u ten zeerste aan statistieken te maken en bij te werken.</span><span class="sxs-lookup"><span data-stu-id="448b4-262">Statistics are important for query performance and it is highly recommended you create and update statistics.</span></span>
    > 
    > <span data-ttu-id="448b4-263">**Krijgt u Hallo profiteren door statistieken op kolommen die betrokken zijn in joins van kolommen die worden gebruikt in Hallo waar component en kolommen gevonden in de GROUP BY.**</span><span class="sxs-lookup"><span data-stu-id="448b4-263">**You gain hello most benefit by having statistics on columns involved in joins, columns used in hello WHERE clause and columns found in GROUP BY.**</span></span>
    >

3. <span data-ttu-id="448b4-264">Hallo query opnieuw uitvoeren van de vereisten en bekijk eventuele prestatieverschillen in.</span><span class="sxs-lookup"><span data-stu-id="448b4-264">Run hello query from Prerequisites again and observe any performance differences.</span></span> <span data-ttu-id="448b4-265">Bij Hallo verschillen in prestaties van query's wordt niet als ingrijpende als omhoog schalen, ziet u een versnellen.</span><span class="sxs-lookup"><span data-stu-id="448b4-265">While hello differences in query performance will not be as drastic as scaling up, you should notice a  speed-up.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="448b4-266">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="448b4-266">Next steps</span></span>

<span data-ttu-id="448b4-267">U bent nu klaar tooquery en verkennen.</span><span class="sxs-lookup"><span data-stu-id="448b4-267">You're now ready tooquery and explore.</span></span> <span data-ttu-id="448b4-268">Bekijk onze aanbevolen procedures en tips.</span><span class="sxs-lookup"><span data-stu-id="448b4-268">Check out our best practices or tips.</span></span>

<span data-ttu-id="448b4-269">Als u klaar bent verkennen voor Hallo dag, zodat toopause ervoor dat uw exemplaar!</span><span class="sxs-lookup"><span data-stu-id="448b4-269">If you're done exploring for hello day, make sure toopause your instance!</span></span> <span data-ttu-id="448b4-270">In productie, kunt u enorm veel besparingen ervaring door te onderbreken en schalen toomeet behoeften van uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="448b4-270">In production, you can experience enormous savings by pausing and scaling toomeet your business needs.</span></span>

![Onderbreken](./media/sql-data-warehouse-get-started-tutorial/pause.png)

## <a name="useful-readings"></a><span data-ttu-id="448b4-272">Handige documentatie</span><span class="sxs-lookup"><span data-stu-id="448b4-272">Useful readings</span></span>

<span data-ttu-id="448b4-273">[Gelijktijdigheid en werklastbeheer][]</span><span class="sxs-lookup"><span data-stu-id="448b4-273">[Concurrency and Workload Management][]</span></span>

<span data-ttu-id="448b4-274">[Aanbevolen procedures voor Azure SQL Data Warehouse][]</span><span class="sxs-lookup"><span data-stu-id="448b4-274">[Best practices for Azure SQL Data Warehouse][]</span></span>

<span data-ttu-id="448b4-275">[Querybewaking][]</span><span class="sxs-lookup"><span data-stu-id="448b4-275">[Query Monitoring][]</span></span>

<span data-ttu-id="448b4-276">[Top 10 aanbevolen procedures voor het bouwen van een grootschalige relationele Data Warehouse][]</span><span class="sxs-lookup"><span data-stu-id="448b4-276">[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][]</span></span>

<span data-ttu-id="448b4-277">[Migreren gegevens tooAzure SQL Data Warehouse][]</span><span class="sxs-lookup"><span data-stu-id="448b4-277">[Migrating Data tooAzure SQL Data Warehouse][]</span></span>

[Gelijktijdigheid en werklastbeheer]: sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example
[Aanbevolen procedures voor Azure SQL Data Warehouse]: sql-data-warehouse-best-practices.md#hash-distribute-large-tables
[Querybewaking]: sql-data-warehouse-manage-monitor.md
[Top 10 aanbevolen procedures voor het bouwen van een grootschalige relationele Data Warehouse]: https://blogs.msdn.microsoft.com/sqlcat/2013/09/16/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse/
[Migreren gegevens tooAzure SQL Data Warehouse]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/



[!INCLUDE [Additional Resources](../../includes/sql-data-warehouse-article-footer.md)]

<!-- Internal Links -->
[vereisten]: sql-data-warehouse-get-started-tutorial.md#prerequisites

<!--Other Web references-->
[Visual Studio]: https://www.visualstudio.com/
[SQL Server Management Studio]: https://msdn.microsoft.com/en-us/library/mt238290.aspx
