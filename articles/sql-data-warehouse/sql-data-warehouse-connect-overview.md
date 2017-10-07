---
title: aaaConnect tooAzure SQL Data Warehouse | Microsoft Docs
description: Hoe toofind Hallo-servernaam en verbinding met de tekenreeks van uw tooAzure SQL Data Warehouse
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: e52872ca-ae74-4e25-9c56-d49c85c8d0f0
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: f15e098026afb7c5efbbbfaf62b681e8cd7936bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-sql-data-warehouse"></a><span data-ttu-id="d73c9-103">Verbinding maken met SQL Data Warehouse tooAzure</span><span class="sxs-lookup"><span data-stu-id="d73c9-103">Connect tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="d73c9-104">In dit artikel helpt u bij verbonden tooSQL Data Warehouse voor Hallo eerst ophalen.</span><span class="sxs-lookup"><span data-stu-id="d73c9-104">This article helps you get connected tooSQL Data Warehouse for hello first time.</span></span>

## <a name="find-your-server-name"></a><span data-ttu-id="d73c9-105">Uw servernaam vinden</span><span class="sxs-lookup"><span data-stu-id="d73c9-105">Find your server name</span></span>
<span data-ttu-id="d73c9-106">Hallo eerste stap tooconnecting tooSQL Data Warehouse is weten hoe toofind naam van uw server.</span><span class="sxs-lookup"><span data-stu-id="d73c9-106">hello first step tooconnecting tooSQL Data Warehouse is knowing how toofind your server name.</span></span>  <span data-ttu-id="d73c9-107">Hallo-servernaam in het volgende voorbeeld Hallo is bijvoorbeeld sample.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="d73c9-107">For example, hello server name in hello following example is sample.database.windows.net.</span></span> <span data-ttu-id="d73c9-108">toofind hello volledig gekwalificeerde servernaam:</span><span class="sxs-lookup"><span data-stu-id="d73c9-108">toofind hello fully qualified server name:</span></span>

1. <span data-ttu-id="d73c9-109">Ga toohello [Azure-portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="d73c9-109">Go toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="d73c9-110">Klik op **SQL-databases**</span><span class="sxs-lookup"><span data-stu-id="d73c9-110">Click on **SQL databases**</span></span> 
3. <span data-ttu-id="d73c9-111">Klik op de gewenste tooconnect op Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="d73c9-111">Click on hello database you want tooconnect to.</span></span>
4. <span data-ttu-id="d73c9-112">Zoek de volledige servernaam Hallo.</span><span class="sxs-lookup"><span data-stu-id="d73c9-112">Locate hello full server name.</span></span>
   
    ![Volledige servernaam][1]

## <a name="supported-drivers-and-connection-strings"></a><span data-ttu-id="d73c9-114">Ondersteunde stuurprogramma's en verbindingsreeksen</span><span class="sxs-lookup"><span data-stu-id="d73c9-114">Supported drivers and connection strings</span></span>
<span data-ttu-id="d73c9-115">Azure SQL Data Warehouse biedt ondersteuning voor [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP] en [JDBC][JDBC].</span><span class="sxs-lookup"><span data-stu-id="d73c9-115">Azure SQL Data Warehouse supports [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP], and [JDBC][JDBC].</span></span> <span data-ttu-id="d73c9-116">Klik op een van de Hallo voorafgaand aan de meest recente versie van stuurprogramma's toofind hello en documentatie.</span><span class="sxs-lookup"><span data-stu-id="d73c9-116">Click on one of hello preceding drivers toofind hello latest version and documentation.</span></span> <span data-ttu-id="d73c9-117">tooautomatically Hallo-verbindingsreeks voor Hallo-stuurprogramma dat u gebruikt genereren van hello Azure portal, kunt u klikken op Hallo **databaseverbindingsreeksen tonen** van Hallo voorgaande voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="d73c9-117">tooautomatically generate hello connection string for hello driver that you are using from hello Azure portal, you can click on hello **Show database connection strings** from hello preceding example.</span></span>  <span data-ttu-id="d73c9-118">Hier volgen ook enkele voorbeelden van hoe een verbindingsreeks er voor elk stuurprogramma uitziet.</span><span class="sxs-lookup"><span data-stu-id="d73c9-118">Following are also some examples of what a connection string looks like for each driver.</span></span>

> [!NOTE]
> <span data-ttu-id="d73c9-119">U kunt instellen Hallo verbinding time-out too300 seconden tooallow uw verbinding toosurvive korte perioden niet beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="d73c9-119">Consider setting hello connection timeout too300 seconds tooallow your connection toosurvive short periods of unavailability.</span></span>
> 
> 

### <a name="adonet-connection-string-example"></a><span data-ttu-id="d73c9-120">Voorbeeld van ADO.NET-verbindingsreeks</span><span class="sxs-lookup"><span data-stu-id="d73c9-120">ADO.NET connection string example</span></span>
```C#
Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};User ID={your_user_name};Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
```

### <a name="odbc-connection-string-example"></a><span data-ttu-id="d73c9-121">Voorbeeld van ODBC-verbindingsreeks</span><span class="sxs-lookup"><span data-stu-id="d73c9-121">ODBC connection string example</span></span>
```C#
Driver={SQL Server Native Client 11.0};Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};Uid={your_user_name};Pwd={your_password_here};Encrypt=yes;TrustServerCertificate=no;Connection Timeout=30;
```

### <a name="php-connection-string-example"></a><span data-ttu-id="d73c9-122">Voorbeeld van PHP-verbindingsreeks</span><span class="sxs-lookup"><span data-stu-id="d73c9-122">PHP connection string example</span></span>
```PHP
Server: {your_server}.database.windows.net,1433 \r\nSQL Database: {your_database}\r\nUser Name: {your_user_name}\r\n\r\nPHP Data Objects(PDO) Sample Code:\r\n\r\ntry {\r\n   $conn = new PDO ( \"sqlsrv:server = tcp:{your_server}.database.windows.net,1433; Database = {your_database}\", \"{your_user_name}\", \"{your_password_here}\");\r\n    $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );\r\n}\r\ncatch ( PDOException $e ) {\r\n   print( \"Error connecting tooSQL Server.\" );\r\n   die(print_r($e));\r\n}\r\n\rSQL Server Extension Sample Code:\r\n\r\n$connectionInfo = array(\"UID\" => \"{your_user_name}\", \"pwd\" => \"{your_password_here}\", \"Database\" => \"{your_database}\", \"LoginTimeout\" => 30, \"Encrypt\" => 1, \"TrustServerCertificate\" => 0);\r\n$serverName = \"tcp:{your_server}.database.windows.net,1433\";\r\n$conn = sqlsrv_connect($serverName, $connectionInfo);
```

### <a name="jdbc-connection-string-example"></a><span data-ttu-id="d73c9-123">Voorbeeld van JDBC-verbindingsreeks</span><span class="sxs-lookup"><span data-stu-id="d73c9-123">JDBC connection string example</span></span>
```Java
jdbc:sqlserver://yourserver.database.windows.net:1433;database=yourdatabase;user={your_user_name};password={your_password_here};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
```

## <a name="connection-settings"></a><span data-ttu-id="d73c9-124">Verbindingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="d73c9-124">Connection settings</span></span>
<span data-ttu-id="d73c9-125">SQL Data Warehouse standaardiseert enkele instellingen tijdens het maken van de verbinding en het maken van objecten.</span><span class="sxs-lookup"><span data-stu-id="d73c9-125">SQL Data Warehouse standardizes some settings during connection and object creation.</span></span> <span data-ttu-id="d73c9-126">Deze instellingen kunnen niet worden overschreven, en omvatten:</span><span class="sxs-lookup"><span data-stu-id="d73c9-126">These settings cannot be overridden and include:</span></span>

| <span data-ttu-id="d73c9-127">Database-instelling</span><span class="sxs-lookup"><span data-stu-id="d73c9-127">Database Setting</span></span> | <span data-ttu-id="d73c9-128">Waarde</span><span class="sxs-lookup"><span data-stu-id="d73c9-128">Value</span></span> |
|:--- |:--- |
| <span data-ttu-id="d73c9-129">[ANSI_NULLS][ANSI_NULLS]</span><span class="sxs-lookup"><span data-stu-id="d73c9-129">[ANSI_NULLS][ANSI_NULLS]</span></span> |<span data-ttu-id="d73c9-130">AAN</span><span class="sxs-lookup"><span data-stu-id="d73c9-130">ON</span></span> |
| <span data-ttu-id="d73c9-131">[QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS]</span><span class="sxs-lookup"><span data-stu-id="d73c9-131">[QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS]</span></span> |<span data-ttu-id="d73c9-132">AAN</span><span class="sxs-lookup"><span data-stu-id="d73c9-132">ON</span></span> |
| <span data-ttu-id="d73c9-133">[DATEFORMAT][DATEFORMAT]</span><span class="sxs-lookup"><span data-stu-id="d73c9-133">[DATEFORMAT][DATEFORMAT]</span></span> |<span data-ttu-id="d73c9-134">mdy</span><span class="sxs-lookup"><span data-stu-id="d73c9-134">mdy</span></span> |
| <span data-ttu-id="d73c9-135">[DATEFIRST][DATEFIRST]</span><span class="sxs-lookup"><span data-stu-id="d73c9-135">[DATEFIRST][DATEFIRST]</span></span> |<span data-ttu-id="d73c9-136">7</span><span class="sxs-lookup"><span data-stu-id="d73c9-136">7</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d73c9-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d73c9-137">Next steps</span></span>
<span data-ttu-id="d73c9-138">tooconnect en de query met Visual Studio, Zie [Query met Visual Studio][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="d73c9-138">tooconnect and query with Visual Studio, see [Query with Visual Studio][Query with Visual Studio].</span></span> <span data-ttu-id="d73c9-139">toolearn meer informatie over opties voor verificatie, Zie [verificatie tooAzure SQL Data Warehouse][Authentication tooAzure SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="d73c9-139">toolearn more about authentication options, see [Authentication tooAzure SQL Data Warehouse][Authentication tooAzure SQL Data Warehouse].</span></span>

<!--Articles-->
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[Authentication tooAzure SQL Data Warehouse]: ./sql-data-warehouse-authentication.md

<!--MSDN references-->
[ADO.NET]: https://msdn.microsoft.com/library/e80y5yhx(v=vs.110).aspx
[ODBC]: https://msdn.microsoft.com/library/jj730314.aspx
[PHP]: https://msdn.microsoft.com/library/cc296172.aspx?f=255&MSPPError=-2147217396
[JDBC]: https://msdn.microsoft.com/library/mt484311(v=sql.110).aspx
[ANSI_NULLS]: https://msdn.microsoft.com/library/ms188048.aspx
[QUOTED_IDENTIFIERS]: https://msdn.microsoft.com/library/ms174393.aspx
[DATEFORMAT]: https://msdn.microsoft.com/library/ms189491.aspx
[DATEFIRST]: https://msdn.microsoft.com/library/ms181598.aspx

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->
[1]: media/sql-data-warehouse-connect-overview/get-server-name.png


