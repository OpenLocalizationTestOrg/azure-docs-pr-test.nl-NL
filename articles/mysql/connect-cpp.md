---
title: Verbinding maken met Database tooAzure voor MySQL van C++ | Microsoft Docs
description: Deze snelstartgids bevat een codevoorbeeld C++ kunt u een query over gegevens uit Azure-Database voor MySQL en tooconnect gebruiken.
services: mysql
author: seanli1988
ms.author: seal
manager: janders
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: C++
ms.topic: hero-article
ms.date: 08/03/2017
ms.openlocfilehash: d027597bf02b1eacab9b8808957399f6e54e63cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-connectorc-tooconnect-and-query-data"></a>Azure MySQL-Database: gebruik Connector/C++ tooconnect en query-gegevens
Deze snelstartgids demonstreert hoe tooconnect tooan Azure-Database voor MySQL met behulp van een C++-toepassing. Er wordt weergegeven hoe toouse SQL-instructies tooquery invoegen, bijwerken en verwijderen van gegevens in Hallo-database. Hallo stappen in dit artikel wordt ervan uitgegaan dat u bekend bent met ontwikkelen met C++, en dat u een nieuwe tooworking met Azure-Database voor MySQL bent.

## <a name="prerequisites"></a>Vereisten
Deze snelstartgids Hallo bronnen die zijn gemaakt in een van deze handleidingen als uitgangspunt gebruikt:
- [Een Azure-database voor een MySQL-server maken met behulp van Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Een Azure-database voor een MySQL-server maken met behulp van Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)

U moet ook het volgende doen:
- [.NET Framework](https://www.microsoft.com/net/download) installeren
- [Visual Studio](https://www.visualstudio.com/downloads/) installeren
- [MySQL-connector/C++](https://dev.mysql.com/downloads/connector/cpp/) installeren 
- [Boost](http://www.boost.org/) installeren

## <a name="install-visual-studio-and-net"></a>Visual Studio en .NET installeren
Hallo stappen in deze sectie wordt ervan uitgegaan dat u bekend bent met ontwikkelen met behulp van .NET.

### <a name="windows"></a>**Windows**
1. Installeer Visual Studio 2017 Community. Dit is een volledig functionele, uitbreidbare en gratis IDE voor het maken van moderne toepassingen voor Android, iOS en Windows, voor web- en databasetoepassingen, en voor cloudservices. U kunt ofwel Hallo volledige .NET Framework of alleen .NET Core installeren. Hallo codefragmenten in Hallo Quick Start met een werken. Als u Visual Studio is geïnstalleerd op uw computer al hebt, moet u de volgende twee stappen Hallo overslaan.
   - Hallo downloaden [Visual Studio 2017 installer](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15). 
   - Hallo-installatieprogramma uitvoeren en volg Hallo installatie wordt u gevraagd toocomplete Hallo-installatie.

### <a name="configure-visual-studio"></a>**Visual Studio configureren**
1. Eigenschap vanuit Visual Studio-project > configuratie-eigenschappen > C/C++ > linker > Algemeen > aanvullende bibliotheekmappen, Hallo lib\opt map toevoegen (dat wil zeggen: C:\Program Files (x86) \MySQL\MySQL Connector C++ 1.1.9\lib\opt) van Hallo c++ Connector.
2. Ga in Visual Studio naar projecteigenschap > configuratie-eigenschappen > C/C++ > algemeen > aanvullende includemappen
   - Voeg include/map van c++-connector toe (bijvoorbeeld: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)
   - Voeg de hoofdmap van de Boost-bibliotheek toe (bijvoorbeeld: C:\boost_1_64_0\)
3. Eigenschap vanuit Visual Studio-project > configuratie-eigenschappen > C/C++ > linker > invoer > Extra afhankelijkheden mysqlcppconn.lib in Hallo tekstveld toevoegen
4. Beide mysqlcppconn.dll kopie van Hallo c++ connector bibliotheekmap in stap 3 toohello dezelfde directory als Hallo toepassing uitvoerbaar bestand of deze omgevingsvariabele toohello toevoegen zodat uw toepassing kan worden gedetecteerd.

## <a name="get-connection-information"></a>Verbindingsgegevens ophalen
Hallo verbinding informatie die nodig is tooconnect toohello Azure Database voor MySQL niet ophalen. U moet Hallo van server volledig gekwalificeerde servernaam en aanmeldingsreferenties.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com/).
2. Hallo links menu in Azure-portal en klik op **alle resources** en zoek naar Hallo-server die u hebt gemaakt, zoals **myserver4demo**.
3. Klik op Hallo servernaam.
4. Selecteer Hallo-server **eigenschappen** pagina. Maak een notitie van Hallo **servernaam** en **aanmeldingsnaam van Server-beheerder**.
 ![Naam van Azure Database voor MySQL-server](./media/connect-cpp/1_server-properties-name-login.png)
5. Als u uw aanmeldingsgegevens server bent vergeten, gaat u toohello **overzicht** pagina tooview Hallo Server admin-aanmeldingsnaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo.

## <a name="connect-create-table-and-insert-data"></a>Verbinden, tabel maken en gegevens invoegen
Gebruik Hallo volgende tooconnect code en laden van gegevens met Hallo **CREATE TABLE** en **INSERT INTO** SQL-instructies. Hallo code sql::Driver klasse Hallo Connect ()-methode tooestablish een tooMySQL verbinding gebruikt. Hallo code gebruikt vervolgens de methode createStatement() en execute() toorun Hallo databaseopdrachten. 

Hallo-Host, DBName, gebruiker en het wachtwoord parameters vervangen door Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt. 

```c++
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::Statement *stmt;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }

    stmt = con>createStatement();
    stmt>execute("DROP TABLE IF EXISTS inventory");
    cout << "Finished dropping table (if existed)" << endl;
    stmt>execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);");
    cout << "Finished creating table" << endl;
    delete stmt;

    pstmt = con>prepareStatement("INSERT INTO inventory(name, quantity) VALUES(?,?)");
    pstmt>setString(1, "banana");
    pstmt>setInt(2, 150);
    pstmt>execute();
    cout << "One row inserted." << endl;

    pstmt>setString(1, "orange");
    pstmt>setInt(2, 154);
    pstmt>execute();
    cout << "One row inserted." << endl;

    pstmt>setString(1, "apple");
    pstmt>setInt(2, 100);
    pstmt>execute();
    cout << "One row inserted." << endl;
    
    delete pstmt;   
    delete con;
    system("pause");
    return 0;

```

## <a name="read-data"></a>Gegevens lezen

Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **Selecteer** SQL-instructie. Hallo code sql::Driver klasse Hallo Connect ()-methode tooestablish een tooMySQL verbinding gebruikt. Vervolgens Hallo code gebruikt methode prepareStatement() en executeQuery() toorun Hallo Selecteer opdrachten. Ten slotte gebruikt Hallo code next() tooadvance toohello records in Hallo resultaten. Hallo code gebruikt vervolgens getInt() en getString() tooparse Hallo waarden in Hallo-record.

Hallo-Host, DBName, gebruiker en het wachtwoord parameters vervangen door Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt. 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }   

//  select  
    pstmt = con>prepareStatement("SELECT * FROM inventory;");
    result = pstmt>executeQuery();  
    
    while (result>next())
        printf("Reading from table=(%d, %s, %d)\n", result>getInt(1), result>getString(2).c_str(), result>getInt(3));   
    
    delete result;
    delete pstmt;   
    delete con;
    system("pause");
    return 0;
}
```

## <a name="update-data"></a>Gegevens bijwerken
Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **UPDATE** SQL-instructie. Hallo code sql::Driver klasse Hallo Connect ()-methode tooestablish een tooMySQL verbinding gebruikt. Hallo code gebruikt vervolgens de methode prepareStatement() en executeQuery() toorun Hallo bijwerkopdrachten. 

Hallo-Host, DBName, gebruiker en het wachtwoord parameters vervangen door Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt. 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }   

    //update
    pstmt = con>prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?");
    pstmt>setInt(1, 200);
    pstmt>setString(2, "banana");
    pstmt>executeQuery();
    printf("Row updated\n");
    
    delete con;
    delete pstmt;
    system("pause");
    return 0;
}
```


## <a name="delete-data"></a>Gegevens verwijderen
Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **verwijderen** SQL-instructie. Hallo code sql::Driver klasse Hallo Connect ()-methode tooestablish een tooMySQL verbinding gebruikt. Hallo code gebruikt vervolgens de methode prepareStatement() executeQuery() toorun Hallo opdrachten of verwijderen.

Hallo-Host, DBName, gebruiker en het wachtwoord parameters vervangen door Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt. 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }
        
    //delete
    pstmt = con>prepareStatement("DELETE FROM inventory WHERE name = ?");
    pstmt>setString(1, "orange");
    result = pstmt>executeQuery();
    printf("Row deleted\n");    
    
    delete pstmt;
    delete con;
    delete result;
    system("pause");
    return 0;
}
```

## <a name="next-steps"></a>Volgende stappen
> [!div class="nextstepaction"]
> [Migreren van uw MySQL-database tooAzure Database voor MySQL met behulp van de dump en terugzetten](concepts-migrate-dump-restore.md)
