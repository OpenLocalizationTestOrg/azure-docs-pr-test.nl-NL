---
title: Verbinding maken met Database tooAzure voor MySQL van Python | Microsoft Docs
description: Deze snelstartgids bevat dat verschillende Python-codevoorbeelden kunt u tooconnect en query gegevens uit Azure-Database voor MySQL.
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: python
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: 9df5211adcab886a502fd138347aed8fb587cd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-python-tooconnect-and-query-data"></a>Azure MySQL-Database: gebruik Python tooconnect en query-gegevens
Deze snelstartgids demonstreert hoe toouse [Python](https://python.org) tooconnect tooan Azure voor MySQL-Database. Dit maakt gebruik van SQL instructies tooquery, invoegen, bijwerken en verwijderen van gegevens in de database Hallo van Mac OS, Ubuntu Linux en Windows-platforms. Hallo stappen in dit artikel wordt ervan uitgegaan dat u bekend bent met het ontwikkelen met behulp van Python en nieuwe tooworking met Azure-Database voor MySQL zijn.

## <a name="prerequisites"></a>Vereisten
Deze snelstartgids Hallo bronnen die zijn gemaakt in een van deze handleidingen als uitgangspunt gebruikt:
- [Een Azure-database voor een MySQL-server maken met behulp van Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Een Azure-database voor een MySQL-server maken met behulp van Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-python-and-hello-mysql-connector"></a>Installeren van Python en Hallo MySQL-connector
Installeer [Python](https://www.python.org/downloads/) en Hallo [MySQL-connector voor Python](https://dev.mysql.com/downloads/connector/python/) op uw computer. Hallo stappen, afhankelijk van uw platform:

### <a name="windows"></a>Windows
1. Download en installeer Python 2.7 van [python.org](https://www.python.org/downloads/windows/). 
2. Hallo Python installatie controleren door het Hallo-opdrachtprompt te starten. Hallo-opdracht uitvoeren `C:\python27\python.exe -V` met Hallo hoofdletters V switch toosee Hallo versienummer.
3. Hallo Python-connector installeren voor MySQL van [mysql.com](https://dev.mysql.com/downloads/connector/python/) overeenkomstige tooyour versie van Python.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. In Linux (Ubuntu), is doorgaans Python geïnstalleerd als onderdeel van de standaardinstallatie Hallo.
2. Hallo Python installatie controleren door het Hallo bash-shell te starten. Hallo-opdracht uitvoeren `python -V` met Hallo hoofdletters V switch toosee Hallo versienummer.
3. Hallo PIP-installatie controleren door te voeren Hallo `pip show pip -V` opdracht toosee Hallo versienummer. 
4. PIP kan zijn opgenomen in sommige versies van Python. Als PIP niet is geïnstalleerd, kunt u Hallo [PIP] (https://pip.pypa.io/en/stable/installing/) installeren pakket met opdracht `sudo apt-get install python-pip`.
5. Update PIP toohello nieuwste versie, door te voeren Hallo `pip install -U pip` opdracht.
6. Hallo MySQL-connector installeren voor Python en de bijbehorende afhankelijkheden met behulp van Hallo PIP-opdracht:

   ```bash
   sudo pip install mysql-connector-python-rf
   ```
 
### <a name="macos"></a>MacOS
1. In Mac OS is doorgaans Python geïnstalleerd als onderdeel van de installatie van het besturingssysteem Hallo standaard.
2. Hallo Python installatie controleren door het Hallo bash-shell te starten. Hallo-opdracht uitvoeren `python -V` met Hallo hoofdletters V switch toosee Hallo versienummer.
3. Hallo PIP-installatie controleren door te voeren Hallo `pip show pip -V` opdracht toosee Hallo versienummer.
4. PIP kan zijn opgenomen in sommige versies van Python. Als PIP niet is geïnstalleerd, kunt u Hallo installeren [PIP](https://pip.pypa.io/en/stable/installing/) pakket.
5. Update PIP toohello nieuwste versie, door te voeren Hallo `pip install -U pip` opdracht.
6. Hallo MySQL-connector installeren voor Python en de bijbehorende afhankelijkheden met behulp van Hallo PIP-opdracht:

   ```bash
   pip install mysql-connector-python-rf
   ```

## <a name="get-connection-information"></a>Verbindingsgegevens ophalen
Hallo verbinding informatie die nodig is tooconnect toohello Azure Database voor MySQL niet ophalen. U moet Hallo van server volledig gekwalificeerde servernaam en aanmeldingsreferenties.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com/).
2. Hallo links menu in Azure-portal en klik op **alle resources** en zoek naar Hallo-server die u hebt ook, zoals **myserver4demo**.
3. Klik op de servernaam Hallo **myserver4demo**.
4. Selecteer Hallo-server **eigenschappen** pagina. Maak een notitie van Hallo **servernaam** en **aanmeldingsnaam van Server-beheerder**.
 ![Azure Database voor MySQL - Aanmeldgegevens van de serverbeheerder](./media/connect-python/1_server-properties-name-login.png)
5. Als u uw aanmeldingsgegevens server bent vergeten, gaat u toohello **overzicht** pagina tooview Hallo Server admin-aanmeldingsnaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo.
   

## <a name="run-python-code"></a>Python-code uitvoeren
- Hallo-code in een tekstbestand te plakken en opslaan in een projectmap met bestand extensie .py zoals C:\pythonmysql\createtable.py of /home/username/pythonmysql/createtable.py Hallo
- toorun hello code, opdrachtregel Hallo starten of bash-shell. Ga naar de projectmap `cd pythonmysql`. Typ Hallo python opdracht gevolgd door de bestandsnaam Hallo `python createtable.py` toorun Hallo-toepassing. Op Hallo Windows-besturingssysteem, als python.exe niet wordt gevonden, kan u bieden Hallo volledig pad toohello uitvoerbare of Hallo Python pad toevoegen aan de omgevingsvariabele path van Hallo. `C:\python27\python.exe createtable.py`

## <a name="connect-create-table-and-insert-data"></a>Verbinden, tabel maken en gegevens invoegen
Gebruik Hallo volgende code tooconnect toohello server, een tabel maken en laden Hallo gegevens met een **invoegen** SQL-instructie. 

In Hallo code is Hallo mysql.connector bibliotheek geïmporteerd. Hallo [Connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) functie is gebruikte tooconnect tooAzure Database voor MySQL Hallo met [verbinding argumenten](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in Hallo config-verzameling. Hallo code maakt gebruik van een cursor op Hallo-verbinding en [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) methode voert Hallo SQL-query op MySQL-database. 

Vervang Hallo `host`, `user`, `password`, en `database` parameters met Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Drop previous table of same name if one exists
  cursor.execute("DROP TABLE IF EXISTS inventory;")
  print("Finished dropping table (if existed).")

  # Create table
  cursor.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
  print("Finished creating table.")

  # Insert some data into table
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("banana", 150))
  print("Inserted",cursor.rowcount,"row(s) of data.")
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("orange", 154))
  print("Inserted",cursor.rowcount,"row(s) of data.")
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("apple", 100))
  print("Inserted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="read-data"></a>Gegevens lezen
Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **Selecteer** SQL-instructie. 

In Hallo code is Hallo mysql.connector bibliotheek geïmporteerd. Hallo [Connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) functie is gebruikte tooconnect tooAzure Database voor MySQL Hallo met [verbinding argumenten](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in Hallo config-verzameling. Hallo code maakt gebruik van een cursor op Hallo-verbinding en [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) methode voert de SQL-instructie Hallo tegen MySQL-database. Hallo gegevensrijen worden gelezen met Hallo [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) methode. Hello resultaat wordt bewaard in de rij van een verzameling en een voor iterator gebruikte tooloop over Hallo rijen is.

Vervang Hallo `host`, `user`, `password`, en `database` parameters met Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Read data
  cursor.execute("SELECT * FROM inventory;")
  rows = cursor.fetchall()
  print("Read",cursor.rowcount,"row(s) of data.")

  # Print all rows
  for row in rows:
    print("Data row = (%s, %s, %s)" %(str(row[0]), str(row[1]), str(row[2])))

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="update-data"></a>Gegevens bijwerken
Gebruik Hallo volgende tooconnect code en bij te werken Hallo gegevens met een **bijwerken** SQL-instructie. 

In Hallo code is Hallo mysql.connector bibliotheek geïmporteerd.  Hallo [Connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) functie is gebruikte tooconnect tooAzure Database voor MySQL Hallo met [verbinding argumenten](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in Hallo config-verzameling. Hallo code maakt gebruik van een cursor op Hallo-verbinding en [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) methode voert de SQL-instructie Hallo tegen MySQL-database. 

Vervang Hallo `host`, `user`, `password`, en `database` parameters met Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Update a data row in hello table
  cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
  print("Updated",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="delete-data"></a>Gegevens verwijderen
Gebruik Hallo volgende tooconnect code en verwijderen van gegevens met een **verwijderen** SQL-instructie. 

In Hallo code is Hallo mysql.connector bibliotheek geïmporteerd.  Hallo [Connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) functie is gebruikte tooconnect tooAzure Database voor MySQL Hallo met [verbinding argumenten](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in Hallo config-verzameling. Hallo code maakt gebruik van een cursor op Hallo-verbinding en [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) methode voert Hallo SQL-query op MySQL-database. 

Vervang Hallo `host`, `user`, `password`, en `database` parameters met Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established.")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password.")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist.")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Delete a data row in hello table
  cursor.execute("DELETE FROM inventory WHERE name=%(param1)s;", {'param1':"orange"})
  print("Deleted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="next-steps"></a>Volgende stappen
> [!div class="nextstepaction"]
> [Een database migreren met behulp van Exporteren en importeren](./concepts-migrate-import-export.md)
