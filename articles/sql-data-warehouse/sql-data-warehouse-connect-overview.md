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
# <a name="connect-tooazure-sql-data-warehouse"></a>Verbinding maken met SQL Data Warehouse tooAzure
In dit artikel helpt u bij verbonden tooSQL Data Warehouse voor Hallo eerst ophalen.

## <a name="find-your-server-name"></a>Uw servernaam vinden
Hallo eerste stap tooconnecting tooSQL Data Warehouse is weten hoe toofind naam van uw server.  Hallo-servernaam in het volgende voorbeeld Hallo is bijvoorbeeld sample.database.windows.net. toofind hello volledig gekwalificeerde servernaam:

1. Ga toohello [Azure-portal][Azure portal].
2. Klik op **SQL-databases** 
3. Klik op de gewenste tooconnect op Hallo-database.
4. Zoek de volledige servernaam Hallo.
   
    ![Volledige servernaam][1]

## <a name="supported-drivers-and-connection-strings"></a>Ondersteunde stuurprogramma's en verbindingsreeksen
Azure SQL Data Warehouse biedt ondersteuning voor [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP] en [JDBC][JDBC]. Klik op een van de Hallo voorafgaand aan de meest recente versie van stuurprogramma's toofind hello en documentatie. tooautomatically Hallo-verbindingsreeks voor Hallo-stuurprogramma dat u gebruikt genereren van hello Azure portal, kunt u klikken op Hallo **databaseverbindingsreeksen tonen** van Hallo voorgaande voorbeeld.  Hier volgen ook enkele voorbeelden van hoe een verbindingsreeks er voor elk stuurprogramma uitziet.

> [!NOTE]
> U kunt instellen Hallo verbinding time-out too300 seconden tooallow uw verbinding toosurvive korte perioden niet beschikbaar zijn.
> 
> 

### <a name="adonet-connection-string-example"></a>Voorbeeld van ADO.NET-verbindingsreeks
```C#
Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};User ID={your_user_name};Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
```

### <a name="odbc-connection-string-example"></a>Voorbeeld van ODBC-verbindingsreeks
```C#
Driver={SQL Server Native Client 11.0};Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};Uid={your_user_name};Pwd={your_password_here};Encrypt=yes;TrustServerCertificate=no;Connection Timeout=30;
```

### <a name="php-connection-string-example"></a>Voorbeeld van PHP-verbindingsreeks
```PHP
Server: {your_server}.database.windows.net,1433 \r\nSQL Database: {your_database}\r\nUser Name: {your_user_name}\r\n\r\nPHP Data Objects(PDO) Sample Code:\r\n\r\ntry {\r\n   $conn = new PDO ( \"sqlsrv:server = tcp:{your_server}.database.windows.net,1433; Database = {your_database}\", \"{your_user_name}\", \"{your_password_here}\");\r\n    $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );\r\n}\r\ncatch ( PDOException $e ) {\r\n   print( \"Error connecting tooSQL Server.\" );\r\n   die(print_r($e));\r\n}\r\n\rSQL Server Extension Sample Code:\r\n\r\n$connectionInfo = array(\"UID\" => \"{your_user_name}\", \"pwd\" => \"{your_password_here}\", \"Database\" => \"{your_database}\", \"LoginTimeout\" => 30, \"Encrypt\" => 1, \"TrustServerCertificate\" => 0);\r\n$serverName = \"tcp:{your_server}.database.windows.net,1433\";\r\n$conn = sqlsrv_connect($serverName, $connectionInfo);
```

### <a name="jdbc-connection-string-example"></a>Voorbeeld van JDBC-verbindingsreeks
```Java
jdbc:sqlserver://yourserver.database.windows.net:1433;database=yourdatabase;user={your_user_name};password={your_password_here};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
```

## <a name="connection-settings"></a>Verbindingsinstellingen
SQL Data Warehouse standaardiseert enkele instellingen tijdens het maken van de verbinding en het maken van objecten. Deze instellingen kunnen niet worden overschreven, en omvatten:

| Database-instelling | Waarde |
|:--- |:--- |
| [ANSI_NULLS][ANSI_NULLS] |AAN |
| [QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS] |AAN |
| [DATEFORMAT][DATEFORMAT] |mdy |
| [DATEFIRST][DATEFIRST] |7 |

## <a name="next-steps"></a>Volgende stappen
tooconnect en de query met Visual Studio, Zie [Query met Visual Studio][Query with Visual Studio]. toolearn meer informatie over opties voor verificatie, Zie [verificatie tooAzure SQL Data Warehouse][Authentication tooAzure SQL Data Warehouse].

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


