---
title: Verbinding maken met Database tooAzure voor PostgreSQL van Python | Microsoft Docs
description: Deze snelstartgids bevat een Python-codevoorbeeld tooconnect gebruiken en een query over gegevens uit Azure-Database voor PostgreSQL.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: python
ms.topic: quickstart
ms.date: 08/15/2017
ms.openlocfilehash: 7d6d9f5424fb39ad8837999d4788b4363c818887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-python-tooconnect-and-query-data"></a>Azure-Database voor PostgreSQL: gebruik Python tooconnect en query-gegevens
Deze snelstartgids demonstreert hoe toouse [Python](https://python.org) tooconnect tooan Azure voor PostgreSQL-Database. U ziet ook hoe toouse SQL-instructies tooquery invoegen, bijwerken en verwijderen van gegevens in de database Hallo van Mac OS, Ubuntu Linux en Windows-platforms. Hallo stappen in dit artikel wordt ervan uitgegaan dat u bekend bent met het ontwikkelen met behulp van Python en nieuwe tooworking met Azure-Database voor PostgreSQL zijn.

## <a name="prerequisites"></a>Vereisten
Deze snelstartgids Hallo bronnen die zijn gemaakt in een van deze handleidingen als uitgangspunt gebruikt:
- [Database maken - Portal](quickstart-create-server-database-portal.md)
- [Database maken - CLI](quickstart-create-server-database-azure-cli.md)

U hebt ook het volgende nodig:
- [Python](https://www.python.org/downloads/) geïnstalleerd
- [pip](https://pip.pypa.io/en/stable/installing/)-pakket geïnstalleerd (pip is al geïnstalleerd als u werkt met binaire bestanden van Python 2 > =2.7.9 of Python 3 >=3.4 die zijn gedownload van [python.org](https://python.org).)

## <a name="install-hello-python-connection-libraries-for-postgresql"></a>Hallo Python verbindingsbibliotheken voor PostgreSQL installeren
Hallo installeren [psycopg2](http://initd.org/psycopg/docs/install.html) pakket, waarmee u tooconnect en query Hallo-database. psycopg2 is [beschikbaar op PyPI](https://pypi.python.org/pypi/psycopg2/) in de vorm van Hallo [wheel](http://pythonwheels.com/) pakketten voor de meest voorkomende Hallo-platforms (Linux, OS x, Windows). Gebruik pip tooget Hallo binaire versie van inclusief alle afhankelijkheden van Hallo Hallo-module te installeren.

1. Start op uw eigen computer een opdrachtregelinterface:
    - Start op Linux, Hallo Bash-shell.
    - Start op Mac OS, Hallo Terminal.
    - Bij Windows, starten Hallo opdrachtprompt van Hallo Menu Start.
2. Zorg ervoor dat u van de meest recente versie Hallo van pip gebruikmaakt door het uitvoeren van een opdracht zoals:
    ```cmd
    pip install -U pip
    ```

3. Voer Hallo opdracht tooinstall hello psycopg2 pakket te volgen:
    ```cmd
    pip install psycopg2
    ```

## <a name="get-connection-information"></a>Verbindingsgegevens ophalen
Hallo verbinding informatie die nodig is tooconnect toohello Azure Database voor PostgreSQL niet ophalen. U moet Hallo van server volledig gekwalificeerde servernaam en aanmeldingsreferenties.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com/).
2. Hallo links menu in Azure-portal en klik op **alle resources** en zoek naar **mypgserver 20170401** (Hallo server u zojuist hebt gemaakt).
3. Klik op de servernaam Hallo **mypgserver 20170401**.
4. Selecteer Hallo-server **overzicht** pagina en maak een notitie van Hallo **servernaam** en **aanmeldingsnaam van Server-beheerder**.
 ![Azure Database voor PostgreSQL - Aanmeldgegevens van de serverbeheerder](./media/connect-python/1-connection-string.png)
5. Als u uw aanmeldingsgegevens server bent vergeten, gaat u toohello **overzicht** pagina tooview Hallo Server admin-aanmeldingsnaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo.

## <a name="how-toorun-python-code"></a>Hoe toorun Python-code
Dit onderwerp bevat in totaal vier codevoorbeelden. Met elk van deze codes kan een specifieke functie worden uitgevoerd. Hallo volgende instructies wordt aangeven hoe toocreate een tekstbestand, een codeblok invoegen en Hallo-bestand vervolgens opslaan zodat u deze later kunt uitvoeren. Worden ervoor toocreate vier afzonderlijke bestanden, één voor elk codeblok.

- Maak een nieuw bestand in uw favoriete teksteditor.
- Kopieer en plak een van de codevoorbeelden Hallo in de volgende secties in het tekstbestand Hallo Hallo. Vervang Hallo **host**, **dbname**, **gebruiker**, en **wachtwoord** Hallo waarden die u hebt opgegeven tijdens het maken van Hallo-parameters Server en database.
- Hallo-bestand opslaan met Hallo .py extensie (bijvoorbeeld postgres.py) in de projectmap. Als u Hallo Windows-besturingssysteem worden uitgevoerd, moet u ervoor dat tooselect UTF-8-codering bij het opslaan van Hallo-bestand. 
- Hallo-opdrachtprompt of Bash-shell starten en wijzig vervolgens de Hallo tooyour projectmap, bijvoorbeeld `cd postgres`.
-  toorun hello code, type Hallo Python opdracht gevolgd door Hallo bestandsnaam op, bijvoorbeeld `Python postgres.py`.

> [!NOTE]
> Vanaf versie 3 Python, ziet u mogelijk Hallo fout `SyntaxError: Missing parentheses in call too'print'` bij het uitvoeren van Hallo codeblokken te volgen. Als dit gebeurt, vervangt u elke aanroep toohello opdracht `print "string"` met een functieaanroep met haakje, zoals `print("string")`.

## <a name="connect-create-table-and-insert-data"></a>Verbinden, tabel maken en gegevens invoegen
Gebruik Hallo volgende tooconnect code en laden van gegevens met Hallo [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) werken met **invoegen** SQL-instructie. Hallo [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) functie gebruikte tooexecute Hallo SQL-query op PostgreSQL-database is. Vervangen door Hallo host, dbname, gebruiker en wachtwoordparameters Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Drop previous table of same name if one exists
cursor.execute("DROP TABLE IF EXISTS inventory;")
print "Finished dropping table (if existed)"

# Create table
cursor.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
print "Finished creating table"

# Insert some data into table
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("banana", 150))
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("orange", 154))
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("apple", 100))
print "Inserted 3 rows of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

Nadat Hallo code wordt uitgevoerd, Hallo de uitvoer ziet er als volgt:

![Opdrachtregeluitvoer](media/connect-python/2-example-python-output.png)

## <a name="read-data"></a>Gegevens lezen
Gebruik Hallo volgende tooread Hallo gegevens ingevoegd met code [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) werken met **Selecteer** SQL-instructie. Deze functie accepteert een query en retourneert een resultaat ingesteld die kunnen worden iteratie met gebruik van Hallo [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall). Vervangen door Hallo host, dbname, gebruiker en wachtwoordparameters Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Fetch all rows from table
cursor.execute("SELECT * FROM inventory;")
rows = cursor.fetchall()

# Print all rows
for row in rows:
    print "Data row = (%s, %s, %s)" %(str(row[0]), str(row[1]), str(row[2]))

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="update-data"></a>Gegevens bijwerken
Gebruik Hallo volgende tooupdate Hallo inventaris rij die u eerder hebt ingevoegd met code [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) werken met **UPDATE** SQL-instructie. Vervangen door Hallo host, dbname, gebruiker en wachtwoordparameters Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Update a data row in hello table
cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
print "Updated 1 row of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="delete-data"></a>Gegevens verwijderen
Gebruik Hallo volgende toodelete een inventarisatie-item dat u eerder hebt ingevoegd met code [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) werken met **verwijderen** SQL-instructie. Vervangen door Hallo host, dbname, gebruiker en wachtwoordparameters Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Delete data row from table
cursor.execute("DELETE FROM inventory WHERE name = %s;", ("orange",))
print "Deleted 1 row of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="next-steps"></a>Volgende stappen
> [!div class="nextstepaction"]
> [Een database migreren met behulp van Exporteren en importeren](./howto-migrate-using-export-and-import.md)
