---
title: Verbinding maken met Azure SQL Data Warehouse sqlcmd | Microsoft Docs
description: Gebruik het opdrachtregelhulpprogramma [sqlcmd][sqlcmd] om verbinding te maken met en een query uit te voeren op een Azure SQL-datawarehouse.
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 6e2b69e5-4806-4e91-9ea1-e2b63bf28c46
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 5a3fe1046c3417070ba8ff5bd18a0485e2152eff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-sql-data-warehouse-with-sqlcmd"></a><span data-ttu-id="22d0a-103">Verbinding maken met SQL Data Warehouse met sqlcmd</span><span class="sxs-lookup"><span data-stu-id="22d0a-103">Connect to SQL Data Warehouse with sqlcmd</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="22d0a-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="22d0a-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="22d0a-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="22d0a-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="22d0a-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="22d0a-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="22d0a-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="22d0a-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="22d0a-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="22d0a-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="22d0a-109">Gebruik het opdrachtregelhulpprogramma [sqlcmd][sqlcmd] om verbinding te maken met en een query uit te voeren op een Azure SQL-datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="22d0a-109">Use [sqlcmd][sqlcmd] command-line utility to connect to and query an Azure SQL Data Warehouse.</span></span>  

## <a name="1-connect"></a><span data-ttu-id="22d0a-110">1. Verbinding maken</span><span class="sxs-lookup"><span data-stu-id="22d0a-110">1. Connect</span></span>
<span data-ttu-id="22d0a-111">U gaat als volgt aan de slag met [sqlcmd][sqlcmd]: open de opdrachtprompt en voer **sqlcmd** in, gevolgd door de verbindingstekenreeks voor uw SQL Data Warehouse-database.</span><span class="sxs-lookup"><span data-stu-id="22d0a-111">To get started with [sqlcmd][sqlcmd], open the command prompt and enter **sqlcmd** followed by the connection string for your SQL Data Warehouse database.</span></span> <span data-ttu-id="22d0a-112">De verbindingstekenreeks moet de volgende parameters bevatten:</span><span class="sxs-lookup"><span data-stu-id="22d0a-112">The connection string requires the following parameters:</span></span>

* <span data-ttu-id="22d0a-113">**Server (-S):** server in de notatie `<`servernaam`>`.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="22d0a-113">**Server (-S):** Server in the form `<`Server Name`>`.database.windows.net</span></span>
* <span data-ttu-id="22d0a-114">**Database (-d):** databasenaam.</span><span class="sxs-lookup"><span data-stu-id="22d0a-114">**Database (-d):** Database name.</span></span>
* <span data-ttu-id="22d0a-115">**Id's tussen aanhalingstekens inschakelen (-I):** id's tussen aanhalingstekens moeten zijn ingeschakeld om verbinding te kunnen maken met een exemplaar van SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="22d0a-115">**Enable Quoted Identifiers (-I):** Quoted identifiers must be enabled to connect to a SQL Data Warehouse instance.</span></span>

<span data-ttu-id="22d0a-116">Als u gebruik wilt maken van SQL Server-verificatie, moet u de gebruikersnaam- en wachtwoordparameters toevoegen:</span><span class="sxs-lookup"><span data-stu-id="22d0a-116">To use SQL Server Authentication, you need to add the username/password parameters:</span></span>

* <span data-ttu-id="22d0a-117">**Gebruiker (-U):** servergebruiker in de notatie `<`gebruiker`>`</span><span class="sxs-lookup"><span data-stu-id="22d0a-117">**User (-U):** Server user in the form `<`User`>`</span></span>
* <span data-ttu-id="22d0a-118">**Wachtwoord (-P):** wachtwoord dat is gekoppeld aan de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="22d0a-118">**Password (-P):** Password associated with the user.</span></span>

<span data-ttu-id="22d0a-119">Een voorbeeld: uw verbindingstekenreeks kan er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="22d0a-119">For example, your connection string might look like the following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

<span data-ttu-id="22d0a-120">Als u geïntegreerde verificatie van Azure Active Directory wilt gebruiken, moet u de Azure Active Directory-parameters toevoegen:</span><span class="sxs-lookup"><span data-stu-id="22d0a-120">To use Azure Active Directory Integrated authentication, you need to add the Azure Active Directory parameters:</span></span>

* <span data-ttu-id="22d0a-121">**Azure Active Directory Authentication (-G):** Azure Active Directory gebruiken voor verificatie</span><span class="sxs-lookup"><span data-stu-id="22d0a-121">**Azure Active Directory Authentication (-G):** use Azure Active Directory for authentication</span></span>

<span data-ttu-id="22d0a-122">Een voorbeeld: uw verbindingstekenreeks kan er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="22d0a-122">For example, your connection string might look like the following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> <span data-ttu-id="22d0a-123">U moet [Azure Active Directory Authentication inschakelen](sql-data-warehouse-authentication.md) om te verifiëren met Active Directory.</span><span class="sxs-lookup"><span data-stu-id="22d0a-123">You need to [enable Azure Active Directory Authentication](sql-data-warehouse-authentication.md) to authenticate using Active Directory.</span></span>
> 
> 

## <a name="2-query"></a><span data-ttu-id="22d0a-124">2. Query’s uitvoeren</span><span class="sxs-lookup"><span data-stu-id="22d0a-124">2. Query</span></span>
<span data-ttu-id="22d0a-125">Wanneer verbinding is gemaakt, kunt u elke ondersteunde Transact-SQL-instructie voor het exemplaar uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="22d0a-125">After connection, you can issue any supported Transact-SQL statements against the instance.</span></span>  <span data-ttu-id="22d0a-126">In dit voorbeeld worden query's in de interactieve modus verzonden.</span><span class="sxs-lookup"><span data-stu-id="22d0a-126">In this example, queries are submitted in interactive mode.</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

<span data-ttu-id="22d0a-127">In de volgende voorbeelden ziet u hoe u uw query's in de batchmodus uitvoert met behulp van de optie -Q of door uw SQL naar sqlcmd te sluizen.</span><span class="sxs-lookup"><span data-stu-id="22d0a-127">These next examples show how you can run your queries in batch mode using the -Q option or piping your SQL to sqlcmd.</span></span>

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a><span data-ttu-id="22d0a-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="22d0a-128">Next steps</span></span>
<span data-ttu-id="22d0a-129">Zie [sqlcmd-documentatie][sqlcmd] voor meer informatie over de opties die beschikbaar zijn in sqlcmd.</span><span class="sxs-lookup"><span data-stu-id="22d0a-129">See [sqlcmd documentation][sqlcmd] for more about details about the options available in sqlcmd.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->
