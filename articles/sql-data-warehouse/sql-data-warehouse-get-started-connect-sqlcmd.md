---
title: aaaConnect tooAzure SQL Data Warehouse sqlcmd | Microsoft Docs
description: Gebruik [sqlcmd] [sqlcmd] opdrachtregelprogramma tooconnect tooand query een Azure SQL Data Warehouse.
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
ms.openlocfilehash: 0334df7b969da1966ba29c97f835a2dc9e383e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sqlcmd"></a><span data-ttu-id="52375-103">Verbinding maken met tooSQL Data Warehouse met sqlcmd</span><span class="sxs-lookup"><span data-stu-id="52375-103">Connect tooSQL Data Warehouse with sqlcmd</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="52375-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="52375-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="52375-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="52375-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="52375-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="52375-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="52375-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="52375-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="52375-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="52375-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="52375-109">Gebruik [sqlcmd] [ sqlcmd] opdrachtregelprogramma tooconnect tooand query uitvoeren op een Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="52375-109">Use [sqlcmd][sqlcmd] command-line utility tooconnect tooand query an Azure SQL Data Warehouse.</span></span>  

## <a name="1-connect"></a><span data-ttu-id="52375-110">1. Verbinding maken</span><span class="sxs-lookup"><span data-stu-id="52375-110">1. Connect</span></span>
<span data-ttu-id="52375-111">tooget gestart met [sqlcmd][sqlcmd], open Hallo-opdrachtprompt en voer **sqlcmd** gevolgd door de verbindingsreeks Hallo voor uw SQL Data Warehouse-database.</span><span class="sxs-lookup"><span data-stu-id="52375-111">tooget started with [sqlcmd][sqlcmd], open hello command prompt and enter **sqlcmd** followed by hello connection string for your SQL Data Warehouse database.</span></span> <span data-ttu-id="52375-112">Hallo-verbindingsreeks vereist Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="52375-112">hello connection string requires hello following parameters:</span></span>

* <span data-ttu-id="52375-113">**Server (-S):** Server in de vorm Hallo `<`servernaam`>`. database.windows.net</span><span class="sxs-lookup"><span data-stu-id="52375-113">**Server (-S):** Server in hello form `<`Server Name`>`.database.windows.net</span></span>
* <span data-ttu-id="52375-114">**Database (-d):** databasenaam.</span><span class="sxs-lookup"><span data-stu-id="52375-114">**Database (-d):** Database name.</span></span>
* <span data-ttu-id="52375-115">**Id's tussen aanhalingstekens inschakelen (-I):** id's tussen aanhalingstekens moet worden ingeschakeld tooconnect tooa SQL Data Warehouse-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="52375-115">**Enable Quoted Identifiers (-I):** Quoted identifiers must be enabled tooconnect tooa SQL Data Warehouse instance.</span></span>

<span data-ttu-id="52375-116">toouse SQL Server-verificatie, moet u tooadd Hallo gebruikersnaam en wachtwoord parameters:</span><span class="sxs-lookup"><span data-stu-id="52375-116">toouse SQL Server Authentication, you need tooadd hello username/password parameters:</span></span>

* <span data-ttu-id="52375-117">**Gebruiker (-U):** Servergebruiker in de vorm Hallo `<`gebruiker`>`</span><span class="sxs-lookup"><span data-stu-id="52375-117">**User (-U):** Server user in hello form `<`User`>`</span></span>
* <span data-ttu-id="52375-118">**Wachtwoord (-P):** wachtwoord Hallo gebruiker gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="52375-118">**Password (-P):** Password associated with hello user.</span></span>

<span data-ttu-id="52375-119">De verbindingsreeks kan er bijvoorbeeld Hallo volgende uitzien:</span><span class="sxs-lookup"><span data-stu-id="52375-119">For example, your connection string might look like hello following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

<span data-ttu-id="52375-120">Azure Active Directory Integrated authentication toouse, moet u tooadd hello Azure Active Directory-parameters:</span><span class="sxs-lookup"><span data-stu-id="52375-120">toouse Azure Active Directory Integrated authentication, you need tooadd hello Azure Active Directory parameters:</span></span>

* <span data-ttu-id="52375-121">**Azure Active Directory Authentication (-G):** Azure Active Directory gebruiken voor verificatie</span><span class="sxs-lookup"><span data-stu-id="52375-121">**Azure Active Directory Authentication (-G):** use Azure Active Directory for authentication</span></span>

<span data-ttu-id="52375-122">De verbindingsreeks kan er bijvoorbeeld Hallo volgende uitzien:</span><span class="sxs-lookup"><span data-stu-id="52375-122">For example, your connection string might look like hello following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> <span data-ttu-id="52375-123">U moet te[Azure Active Directory-verificatie inschakelen](sql-data-warehouse-authentication.md) tooauthenticate met Active Directory.</span><span class="sxs-lookup"><span data-stu-id="52375-123">You need too[enable Azure Active Directory Authentication](sql-data-warehouse-authentication.md) tooauthenticate using Active Directory.</span></span>
> 
> 

## <a name="2-query"></a><span data-ttu-id="52375-124">2. Query’s uitvoeren</span><span class="sxs-lookup"><span data-stu-id="52375-124">2. Query</span></span>
<span data-ttu-id="52375-125">Nadat de verbinding, kunt u elke ondersteunde Transact-SQL-instructie voor Hallo exemplaar uitgeven.</span><span class="sxs-lookup"><span data-stu-id="52375-125">After connection, you can issue any supported Transact-SQL statements against hello instance.</span></span>  <span data-ttu-id="52375-126">In dit voorbeeld worden query's in de interactieve modus verzonden.</span><span class="sxs-lookup"><span data-stu-id="52375-126">In this example, queries are submitted in interactive mode.</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

<span data-ttu-id="52375-127">Deze volgende voorbeelden laten zien hoe u uw query's in de batchmodus Hallo -Q gebruiken of uw SQL-toosqlcmd sluizen kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="52375-127">These next examples show how you can run your queries in batch mode using hello -Q option or piping your SQL toosqlcmd.</span></span>

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a><span data-ttu-id="52375-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="52375-128">Next steps</span></span>
<span data-ttu-id="52375-129">Zie [sqlcmd-documentatie] [ sqlcmd] voor meer informatie over informatie over opties voor Hallo beschikbaar in sqlcmd.</span><span class="sxs-lookup"><span data-stu-id="52375-129">See [sqlcmd documentation][sqlcmd] for more about details about hello options available in sqlcmd.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->
