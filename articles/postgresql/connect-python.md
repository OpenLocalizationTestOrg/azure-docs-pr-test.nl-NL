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
# <a name="azure-database-for-postgresql-use-python-tooconnect-and-query-data"></a><span data-ttu-id="29d11-103">Azure-Database voor PostgreSQL: gebruik Python tooconnect en query-gegevens</span><span class="sxs-lookup"><span data-stu-id="29d11-103">Azure Database for PostgreSQL: Use Python tooconnect and query data</span></span>
<span data-ttu-id="29d11-104">Deze snelstartgids demonstreert hoe toouse [Python](https://python.org) tooconnect tooan Azure voor PostgreSQL-Database.</span><span class="sxs-lookup"><span data-stu-id="29d11-104">This quickstart demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure Database for PostgreSQL.</span></span> <span data-ttu-id="29d11-105">U ziet ook hoe toouse SQL-instructies tooquery invoegen, bijwerken en verwijderen van gegevens in de database Hallo van Mac OS, Ubuntu Linux en Windows-platforms.</span><span class="sxs-lookup"><span data-stu-id="29d11-105">It also demonstrates how toouse SQL statements tooquery, insert, update, and delete data in hello database from macOS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="29d11-106">Hallo stappen in dit artikel wordt ervan uitgegaan dat u bekend bent met het ontwikkelen met behulp van Python en nieuwe tooworking met Azure-Database voor PostgreSQL zijn.</span><span class="sxs-lookup"><span data-stu-id="29d11-106">hello steps in this article assume that you are familiar with developing using Python and are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29d11-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="29d11-107">Prerequisites</span></span>
<span data-ttu-id="29d11-108">Deze snelstartgids Hallo bronnen die zijn gemaakt in een van deze handleidingen als uitgangspunt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="29d11-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="29d11-109">Database maken - Portal</span><span class="sxs-lookup"><span data-stu-id="29d11-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="29d11-110">Database maken - CLI</span><span class="sxs-lookup"><span data-stu-id="29d11-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="29d11-111">U hebt ook het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="29d11-111">You also need:</span></span>
- <span data-ttu-id="29d11-112">[Python](https://www.python.org/downloads/) geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="29d11-112">[python](https://www.python.org/downloads/) installed</span></span>
- <span data-ttu-id="29d11-113">[pip](https://pip.pypa.io/en/stable/installing/)-pakket geïnstalleerd (pip is al geïnstalleerd als u werkt met binaire bestanden van Python 2 > =2.7.9 of Python 3 >=3.4 die zijn gedownload van [python.org](https://python.org).)</span><span class="sxs-lookup"><span data-stu-id="29d11-113">[pip](https://pip.pypa.io/en/stable/installing/) package installed (pip is already installed if you're working with Python 2 >=2.7.9 or Python 3 >=3.4 binaries downloaded from [python.org](https://python.org).</span></span>

## <a name="install-hello-python-connection-libraries-for-postgresql"></a><span data-ttu-id="29d11-114">Hallo Python verbindingsbibliotheken voor PostgreSQL installeren</span><span class="sxs-lookup"><span data-stu-id="29d11-114">Install hello Python connection libraries for PostgreSQL</span></span>
<span data-ttu-id="29d11-115">Hallo installeren [psycopg2](http://initd.org/psycopg/docs/install.html) pakket, waarmee u tooconnect en query Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="29d11-115">Install hello [psycopg2](http://initd.org/psycopg/docs/install.html) package, which enables you tooconnect and query hello database.</span></span> <span data-ttu-id="29d11-116">psycopg2 is [beschikbaar op PyPI](https://pypi.python.org/pypi/psycopg2/) in de vorm van Hallo [wheel](http://pythonwheels.com/) pakketten voor de meest voorkomende Hallo-platforms (Linux, OS x, Windows).</span><span class="sxs-lookup"><span data-stu-id="29d11-116">psycopg2 is [available on PyPI](https://pypi.python.org/pypi/psycopg2/) in hello form of [wheel](http://pythonwheels.com/) packages for hello most common platforms (Linux, OSX, Windows).</span></span> <span data-ttu-id="29d11-117">Gebruik pip tooget Hallo binaire versie van inclusief alle afhankelijkheden van Hallo Hallo-module te installeren.</span><span class="sxs-lookup"><span data-stu-id="29d11-117">Use pip install tooget hello binary version of hello module including all hello dependencies.</span></span>

1. <span data-ttu-id="29d11-118">Start op uw eigen computer een opdrachtregelinterface:</span><span class="sxs-lookup"><span data-stu-id="29d11-118">On your own computer, launch a command-line interface:</span></span>
    - <span data-ttu-id="29d11-119">Start op Linux, Hallo Bash-shell.</span><span class="sxs-lookup"><span data-stu-id="29d11-119">On Linux, launch hello Bash shell.</span></span>
    - <span data-ttu-id="29d11-120">Start op Mac OS, Hallo Terminal.</span><span class="sxs-lookup"><span data-stu-id="29d11-120">On macOS, launch hello Terminal.</span></span>
    - <span data-ttu-id="29d11-121">Bij Windows, starten Hallo opdrachtprompt van Hallo Menu Start.</span><span class="sxs-lookup"><span data-stu-id="29d11-121">On Windows, launch hello Command Prompt from hello Start Menu.</span></span>
2. <span data-ttu-id="29d11-122">Zorg ervoor dat u van de meest recente versie Hallo van pip gebruikmaakt door het uitvoeren van een opdracht zoals:</span><span class="sxs-lookup"><span data-stu-id="29d11-122">Ensure that you are using hello most current version of pip by running a command such as:</span></span>
    ```cmd
    pip install -U pip
    ```

3. <span data-ttu-id="29d11-123">Voer Hallo opdracht tooinstall hello psycopg2 pakket te volgen:</span><span class="sxs-lookup"><span data-stu-id="29d11-123">Run hello following command tooinstall hello psycopg2 package:</span></span>
    ```cmd
    pip install psycopg2
    ```

## <a name="get-connection-information"></a><span data-ttu-id="29d11-124">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="29d11-124">Get connection information</span></span>
<span data-ttu-id="29d11-125">Hallo verbinding informatie die nodig is tooconnect toohello Azure Database voor PostgreSQL niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="29d11-125">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="29d11-126">U moet Hallo van server volledig gekwalificeerde servernaam en aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="29d11-126">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="29d11-127">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="29d11-127">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="29d11-128">Hallo links menu in Azure-portal en klik op **alle resources** en zoek naar **mypgserver 20170401** (Hallo server u zojuist hebt gemaakt).</span><span class="sxs-lookup"><span data-stu-id="29d11-128">From hello left-hand menu in Azure portal, click **All resources** and search for **mypgserver-20170401** (hello server you just created).</span></span>
3. <span data-ttu-id="29d11-129">Klik op de servernaam Hallo **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="29d11-129">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="29d11-130">Selecteer Hallo-server **overzicht** pagina en maak een notitie van Hallo **servernaam** en **aanmeldingsnaam van Server-beheerder**.</span><span class="sxs-lookup"><span data-stu-id="29d11-130">Select hello server's **Overview** page, and then make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="29d11-131">![Azure Database voor PostgreSQL - Aanmeldgegevens van de serverbeheerder](./media/connect-python/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="29d11-131">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-python/1-connection-string.png)</span></span>
5. <span data-ttu-id="29d11-132">Als u uw aanmeldingsgegevens server bent vergeten, gaat u toohello **overzicht** pagina tooview Hallo Server admin-aanmeldingsnaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="29d11-132">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="how-toorun-python-code"></a><span data-ttu-id="29d11-133">Hoe toorun Python-code</span><span class="sxs-lookup"><span data-stu-id="29d11-133">How toorun Python code</span></span>
<span data-ttu-id="29d11-134">Dit onderwerp bevat in totaal vier codevoorbeelden. Met elk van deze codes kan een specifieke functie worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="29d11-134">This topic contains a total of four code samples, each of which performs a specific function.</span></span> <span data-ttu-id="29d11-135">Hallo volgende instructies wordt aangeven hoe toocreate een tekstbestand, een codeblok invoegen en Hallo-bestand vervolgens opslaan zodat u deze later kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="29d11-135">hello following instructions indicate how toocreate a text file, insert a code block, and then save hello file so that you can run it later.</span></span> <span data-ttu-id="29d11-136">Worden ervoor toocreate vier afzonderlijke bestanden, één voor elk codeblok.</span><span class="sxs-lookup"><span data-stu-id="29d11-136">Be sure toocreate four separate files, one for each code block.</span></span>

- <span data-ttu-id="29d11-137">Maak een nieuw bestand in uw favoriete teksteditor.</span><span class="sxs-lookup"><span data-stu-id="29d11-137">Using your favorite text editor, create a new file.</span></span>
- <span data-ttu-id="29d11-138">Kopieer en plak een van de codevoorbeelden Hallo in de volgende secties in het tekstbestand Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="29d11-138">Copy and paste one of hello code samples in hello following sections into hello text file.</span></span> <span data-ttu-id="29d11-139">Vervang Hallo **host**, **dbname**, **gebruiker**, en **wachtwoord** Hallo waarden die u hebt opgegeven tijdens het maken van Hallo-parameters Server en database.</span><span class="sxs-lookup"><span data-stu-id="29d11-139">Replace hello **host**, **dbname**, **user**, and **password** parameters with hello values that you specified when you created hello server and database.</span></span>
- <span data-ttu-id="29d11-140">Hallo-bestand opslaan met Hallo .py extensie (bijvoorbeeld postgres.py) in de projectmap.</span><span class="sxs-lookup"><span data-stu-id="29d11-140">Save hello file with hello .py extension (for example postgres.py) into your project folder.</span></span> <span data-ttu-id="29d11-141">Als u Hallo Windows-besturingssysteem worden uitgevoerd, moet u ervoor dat tooselect UTF-8-codering bij het opslaan van Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="29d11-141">If you are running hello Windows OS, be sure tooselect UTF-8 encoding when saving hello file.</span></span> 
- <span data-ttu-id="29d11-142">Hallo-opdrachtprompt of Bash-shell starten en wijzig vervolgens de Hallo tooyour projectmap, bijvoorbeeld `cd postgres`.</span><span class="sxs-lookup"><span data-stu-id="29d11-142">Launch hello Command Prompt or Bash shell and then change hello directory tooyour project folder, for example `cd postgres`.</span></span>
-  <span data-ttu-id="29d11-143">toorun hello code, type Hallo Python opdracht gevolgd door Hallo bestandsnaam op, bijvoorbeeld `Python postgres.py`.</span><span class="sxs-lookup"><span data-stu-id="29d11-143">toorun hello code, type hello Python command followed by hello file name, for example `Python postgres.py`.</span></span>

> [!NOTE]
> <span data-ttu-id="29d11-144">Vanaf versie 3 Python, ziet u mogelijk Hallo fout `SyntaxError: Missing parentheses in call too'print'` bij het uitvoeren van Hallo codeblokken te volgen.</span><span class="sxs-lookup"><span data-stu-id="29d11-144">Starting in Python version 3, you may see hello error `SyntaxError: Missing parentheses in call too'print'` when running hello following code blocks.</span></span> <span data-ttu-id="29d11-145">Als dit gebeurt, vervangt u elke aanroep toohello opdracht `print "string"` met een functieaanroep met haakje, zoals `print("string")`.</span><span class="sxs-lookup"><span data-stu-id="29d11-145">If that happens, replace each call toohello command `print "string"` with a function call using parenthesis, such as `print("string")`.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="29d11-146">Verbinden, tabel maken en gegevens invoegen</span><span class="sxs-lookup"><span data-stu-id="29d11-146">Connect, create table, and insert data</span></span>
<span data-ttu-id="29d11-147">Gebruik Hallo volgende tooconnect code en laden van gegevens met Hallo [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) werken met **invoegen** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="29d11-147">Use hello following code tooconnect and load hello data using [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) function with **INSERT** SQL statement.</span></span> <span data-ttu-id="29d11-148">Hallo [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) functie gebruikte tooexecute Hallo SQL-query op PostgreSQL-database is.</span><span class="sxs-lookup"><span data-stu-id="29d11-148">hello [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> <span data-ttu-id="29d11-149">Vervangen door Hallo host, dbname, gebruiker en wachtwoordparameters Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="29d11-149">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

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

<span data-ttu-id="29d11-150">Nadat Hallo code wordt uitgevoerd, Hallo de uitvoer ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="29d11-150">After hello code runs successfully, hello output appears as follows:</span></span>

![Opdrachtregeluitvoer](media/connect-python/2-example-python-output.png)

## <a name="read-data"></a><span data-ttu-id="29d11-152">Gegevens lezen</span><span class="sxs-lookup"><span data-stu-id="29d11-152">Read data</span></span>
<span data-ttu-id="29d11-153">Gebruik Hallo volgende tooread Hallo gegevens ingevoegd met code [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) werken met **Selecteer** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="29d11-153">Use hello following code tooread hello data inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **SELECT** SQL statement.</span></span> <span data-ttu-id="29d11-154">Deze functie accepteert een query en retourneert een resultaat ingesteld die kunnen worden iteratie met gebruik van Hallo [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall).</span><span class="sxs-lookup"><span data-stu-id="29d11-154">This function accepts a query and returns a result set that can be iterated over with hello use of [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall).</span></span> <span data-ttu-id="29d11-155">Vervangen door Hallo host, dbname, gebruiker en wachtwoordparameters Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="29d11-155">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="update-data"></a><span data-ttu-id="29d11-156">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="29d11-156">Update data</span></span>
<span data-ttu-id="29d11-157">Gebruik Hallo volgende tooupdate Hallo inventaris rij die u eerder hebt ingevoegd met code [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) werken met **UPDATE** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="29d11-157">Use hello following code tooupdate hello inventory row that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **UPDATE** SQL statement.</span></span> <span data-ttu-id="29d11-158">Vervangen door Hallo host, dbname, gebruiker en wachtwoordparameters Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="29d11-158">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="delete-data"></a><span data-ttu-id="29d11-159">Gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="29d11-159">Delete data</span></span>
<span data-ttu-id="29d11-160">Gebruik Hallo volgende toodelete een inventarisatie-item dat u eerder hebt ingevoegd met code [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) werken met **verwijderen** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="29d11-160">Use hello following code toodelete an inventory item that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **DELETE** SQL statement.</span></span> <span data-ttu-id="29d11-161">Vervangen door Hallo host, dbname, gebruiker en wachtwoordparameters Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="29d11-161">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="29d11-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="29d11-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="29d11-163">Een database migreren met behulp van Exporteren en importeren</span><span class="sxs-lookup"><span data-stu-id="29d11-163">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
