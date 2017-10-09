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
# <a name="azure-database-for-mysql-use-python-tooconnect-and-query-data"></a><span data-ttu-id="73a65-103">Azure MySQL-Database: gebruik Python tooconnect en query-gegevens</span><span class="sxs-lookup"><span data-stu-id="73a65-103">Azure Database for MySQL: Use Python tooconnect and query data</span></span>
<span data-ttu-id="73a65-104">Deze snelstartgids demonstreert hoe toouse [Python](https://python.org) tooconnect tooan Azure voor MySQL-Database.</span><span class="sxs-lookup"><span data-stu-id="73a65-104">This quickstart demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure Database for MySQL.</span></span> <span data-ttu-id="73a65-105">Dit maakt gebruik van SQL instructies tooquery, invoegen, bijwerken en verwijderen van gegevens in de database Hallo van Mac OS, Ubuntu Linux en Windows-platforms.</span><span class="sxs-lookup"><span data-stu-id="73a65-105">It uses SQL statements tooquery, insert, update, and delete data in hello database from Mac OS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="73a65-106">Hallo stappen in dit artikel wordt ervan uitgegaan dat u bekend bent met het ontwikkelen met behulp van Python en nieuwe tooworking met Azure-Database voor MySQL zijn.</span><span class="sxs-lookup"><span data-stu-id="73a65-106">hello steps in this article assume that you are familiar with developing using Python and are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73a65-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="73a65-107">Prerequisites</span></span>
<span data-ttu-id="73a65-108">Deze snelstartgids Hallo bronnen die zijn gemaakt in een van deze handleidingen als uitgangspunt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="73a65-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="73a65-109">Een Azure-database voor een MySQL-server maken met behulp van Azure Portal</span><span class="sxs-lookup"><span data-stu-id="73a65-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="73a65-110">Een Azure-database voor een MySQL-server maken met behulp van Azure CLI</span><span class="sxs-lookup"><span data-stu-id="73a65-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-python-and-hello-mysql-connector"></a><span data-ttu-id="73a65-111">Installeren van Python en Hallo MySQL-connector</span><span class="sxs-lookup"><span data-stu-id="73a65-111">Install Python and hello MySQL connector</span></span>
<span data-ttu-id="73a65-112">Installeer [Python](https://www.python.org/downloads/) en Hallo [MySQL-connector voor Python](https://dev.mysql.com/downloads/connector/python/) op uw computer.</span><span class="sxs-lookup"><span data-stu-id="73a65-112">Install [Python](https://www.python.org/downloads/) and hello [MySQL connector for Python](https://dev.mysql.com/downloads/connector/python/) on your own machine.</span></span> <span data-ttu-id="73a65-113">Hallo stappen, afhankelijk van uw platform:</span><span class="sxs-lookup"><span data-stu-id="73a65-113">Depending on your platform, follow hello steps:</span></span>

### <a name="windows"></a><span data-ttu-id="73a65-114">Windows</span><span class="sxs-lookup"><span data-stu-id="73a65-114">Windows</span></span>
1. <span data-ttu-id="73a65-115">Download en installeer Python 2.7 van [python.org](https://www.python.org/downloads/windows/).</span><span class="sxs-lookup"><span data-stu-id="73a65-115">Download and Install Python 2.7 from [python.org](https://www.python.org/downloads/windows/).</span></span> 
2. <span data-ttu-id="73a65-116">Hallo Python installatie controleren door het Hallo-opdrachtprompt te starten.</span><span class="sxs-lookup"><span data-stu-id="73a65-116">Check hello Python installation by launching hello command prompt.</span></span> <span data-ttu-id="73a65-117">Hallo-opdracht uitvoeren `C:\python27\python.exe -V` met Hallo hoofdletters V switch toosee Hallo versienummer.</span><span class="sxs-lookup"><span data-stu-id="73a65-117">Run hello command `C:\python27\python.exe -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="73a65-118">Hallo Python-connector installeren voor MySQL van [mysql.com](https://dev.mysql.com/downloads/connector/python/) overeenkomstige tooyour versie van Python.</span><span class="sxs-lookup"><span data-stu-id="73a65-118">Install hello Python connector for MySQL from [mysql.com](https://dev.mysql.com/downloads/connector/python/) corresponding tooyour version of Python.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="73a65-119">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="73a65-119">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="73a65-120">In Linux (Ubuntu), is doorgaans Python geïnstalleerd als onderdeel van de standaardinstallatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="73a65-120">In Linux (Ubuntu), Python is typically installed as part of hello default installation.</span></span>
2. <span data-ttu-id="73a65-121">Hallo Python installatie controleren door het Hallo bash-shell te starten.</span><span class="sxs-lookup"><span data-stu-id="73a65-121">Check hello Python installation by launching hello bash shell.</span></span> <span data-ttu-id="73a65-122">Hallo-opdracht uitvoeren `python -V` met Hallo hoofdletters V switch toosee Hallo versienummer.</span><span class="sxs-lookup"><span data-stu-id="73a65-122">Run hello command `python -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="73a65-123">Hallo PIP-installatie controleren door te voeren Hallo `pip show pip -V` opdracht toosee Hallo versienummer.</span><span class="sxs-lookup"><span data-stu-id="73a65-123">Check hello PIP installation by running hello `pip show pip -V` command toosee hello version number.</span></span> 
4. <span data-ttu-id="73a65-124">PIP kan zijn opgenomen in sommige versies van Python.</span><span class="sxs-lookup"><span data-stu-id="73a65-124">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="73a65-125">Als PIP niet is geïnstalleerd, kunt u Hallo [PIP] (https://pip.pypa.io/en/stable/installing/) installeren pakket met opdracht `sudo apt-get install python-pip`.</span><span class="sxs-lookup"><span data-stu-id="73a65-125">If PIP is not installed, you may install hello [PIP] (https://pip.pypa.io/en/stable/installing/) package, by running command `sudo apt-get install python-pip`.</span></span>
5. <span data-ttu-id="73a65-126">Update PIP toohello nieuwste versie, door te voeren Hallo `pip install -U pip` opdracht.</span><span class="sxs-lookup"><span data-stu-id="73a65-126">Update PIP toohello latest version, by running hello `pip install -U pip` command.</span></span>
6. <span data-ttu-id="73a65-127">Hallo MySQL-connector installeren voor Python en de bijbehorende afhankelijkheden met behulp van Hallo PIP-opdracht:</span><span class="sxs-lookup"><span data-stu-id="73a65-127">Install hello MySQL connector for Python, and its dependencies by using hello PIP command:</span></span>

   ```bash
   sudo pip install mysql-connector-python-rf
   ```
 
### <a name="macos"></a><span data-ttu-id="73a65-128">MacOS</span><span class="sxs-lookup"><span data-stu-id="73a65-128">MacOS</span></span>
1. <span data-ttu-id="73a65-129">In Mac OS is doorgaans Python geïnstalleerd als onderdeel van de installatie van het besturingssysteem Hallo standaard.</span><span class="sxs-lookup"><span data-stu-id="73a65-129">In Mac OS, Python is typically installed as part of hello default OS installation.</span></span>
2. <span data-ttu-id="73a65-130">Hallo Python installatie controleren door het Hallo bash-shell te starten.</span><span class="sxs-lookup"><span data-stu-id="73a65-130">Check hello Python installation by launching hello bash shell.</span></span> <span data-ttu-id="73a65-131">Hallo-opdracht uitvoeren `python -V` met Hallo hoofdletters V switch toosee Hallo versienummer.</span><span class="sxs-lookup"><span data-stu-id="73a65-131">Run hello command `python -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="73a65-132">Hallo PIP-installatie controleren door te voeren Hallo `pip show pip -V` opdracht toosee Hallo versienummer.</span><span class="sxs-lookup"><span data-stu-id="73a65-132">Check hello PIP installation by running hello `pip show pip -V` command toosee hello version number.</span></span>
4. <span data-ttu-id="73a65-133">PIP kan zijn opgenomen in sommige versies van Python.</span><span class="sxs-lookup"><span data-stu-id="73a65-133">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="73a65-134">Als PIP niet is geïnstalleerd, kunt u Hallo installeren [PIP](https://pip.pypa.io/en/stable/installing/) pakket.</span><span class="sxs-lookup"><span data-stu-id="73a65-134">If PIP is not installed, you may install hello [PIP](https://pip.pypa.io/en/stable/installing/) package.</span></span>
5. <span data-ttu-id="73a65-135">Update PIP toohello nieuwste versie, door te voeren Hallo `pip install -U pip` opdracht.</span><span class="sxs-lookup"><span data-stu-id="73a65-135">Update PIP toohello latest version, by running hello `pip install -U pip` command.</span></span>
6. <span data-ttu-id="73a65-136">Hallo MySQL-connector installeren voor Python en de bijbehorende afhankelijkheden met behulp van Hallo PIP-opdracht:</span><span class="sxs-lookup"><span data-stu-id="73a65-136">Install hello MySQL connector for Python, and its dependencies by using hello PIP command:</span></span>

   ```bash
   pip install mysql-connector-python-rf
   ```

## <a name="get-connection-information"></a><span data-ttu-id="73a65-137">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="73a65-137">Get connection information</span></span>
<span data-ttu-id="73a65-138">Hallo verbinding informatie die nodig is tooconnect toohello Azure Database voor MySQL niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="73a65-138">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="73a65-139">U moet Hallo van server volledig gekwalificeerde servernaam en aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="73a65-139">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="73a65-140">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="73a65-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="73a65-141">Hallo links menu in Azure-portal en klik op **alle resources** en zoek naar Hallo-server die u hebt ook, zoals **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="73a65-141">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="73a65-142">Klik op de servernaam Hallo **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="73a65-142">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="73a65-143">Selecteer Hallo-server **eigenschappen** pagina.</span><span class="sxs-lookup"><span data-stu-id="73a65-143">Select hello server's **Properties** page.</span></span> <span data-ttu-id="73a65-144">Maak een notitie van Hallo **servernaam** en **aanmeldingsnaam van Server-beheerder**.</span><span class="sxs-lookup"><span data-stu-id="73a65-144">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="73a65-145">![Azure Database voor MySQL - Aanmeldgegevens van de serverbeheerder](./media/connect-python/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="73a65-145">![Azure Database for MySQL - Server Admin Login](./media/connect-python/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="73a65-146">Als u uw aanmeldingsgegevens server bent vergeten, gaat u toohello **overzicht** pagina tooview Hallo Server admin-aanmeldingsnaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="73a65-146">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>
   

## <a name="run-python-code"></a><span data-ttu-id="73a65-147">Python-code uitvoeren</span><span class="sxs-lookup"><span data-stu-id="73a65-147">Run Python Code</span></span>
- <span data-ttu-id="73a65-148">Hallo-code in een tekstbestand te plakken en opslaan in een projectmap met bestand extensie .py zoals C:\pythonmysql\createtable.py of /home/username/pythonmysql/createtable.py Hallo</span><span class="sxs-lookup"><span data-stu-id="73a65-148">Paste hello code into a text file, and save hello file into a project folder with file extension .py, such as C:\pythonmysql\createtable.py or /home/username/pythonmysql/createtable.py</span></span>
- <span data-ttu-id="73a65-149">toorun hello code, opdrachtregel Hallo starten of bash-shell.</span><span class="sxs-lookup"><span data-stu-id="73a65-149">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="73a65-150">Ga naar de projectmap `cd pythonmysql`.</span><span class="sxs-lookup"><span data-stu-id="73a65-150">Change directory into your project folder `cd pythonmysql`.</span></span> <span data-ttu-id="73a65-151">Typ Hallo python opdracht gevolgd door de bestandsnaam Hallo `python createtable.py` toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="73a65-151">Then type hello python command followed by hello file name `python createtable.py` toorun hello application.</span></span> <span data-ttu-id="73a65-152">Op Hallo Windows-besturingssysteem, als python.exe niet wordt gevonden, kan u bieden Hallo volledig pad toohello uitvoerbare of Hallo Python pad toevoegen aan de omgevingsvariabele path van Hallo.</span><span class="sxs-lookup"><span data-stu-id="73a65-152">On hello Windows OS, if python.exe is not found, you may provide hello full path toohello executable, or add hello Python path into hello path environment variable.</span></span> `C:\python27\python.exe createtable.py`

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="73a65-153">Verbinden, tabel maken en gegevens invoegen</span><span class="sxs-lookup"><span data-stu-id="73a65-153">Connect, create table, and insert data</span></span>
<span data-ttu-id="73a65-154">Gebruik Hallo volgende code tooconnect toohello server, een tabel maken en laden Hallo gegevens met een **invoegen** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="73a65-154">Use hello following code tooconnect toohello server, create a table, and load hello data using an **INSERT** SQL statement.</span></span> 

<span data-ttu-id="73a65-155">In Hallo code is Hallo mysql.connector bibliotheek geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="73a65-155">In hello code, hello mysql.connector library is imported.</span></span> <span data-ttu-id="73a65-156">Hallo [Connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) functie is gebruikte tooconnect tooAzure Database voor MySQL Hallo met [verbinding argumenten](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in Hallo config-verzameling.</span><span class="sxs-lookup"><span data-stu-id="73a65-156">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="73a65-157">Hallo code maakt gebruik van een cursor op Hallo-verbinding en [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) methode voert Hallo SQL-query op MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="73a65-157">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="73a65-158">Vervang Hallo `host`, `user`, `password`, en `database` parameters met Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="73a65-158">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="read-data"></a><span data-ttu-id="73a65-159">Gegevens lezen</span><span class="sxs-lookup"><span data-stu-id="73a65-159">Read data</span></span>
<span data-ttu-id="73a65-160">Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **Selecteer** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="73a65-160">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="73a65-161">In Hallo code is Hallo mysql.connector bibliotheek geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="73a65-161">In hello code, hello mysql.connector library is imported.</span></span> <span data-ttu-id="73a65-162">Hallo [Connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) functie is gebruikte tooconnect tooAzure Database voor MySQL Hallo met [verbinding argumenten](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in Hallo config-verzameling.</span><span class="sxs-lookup"><span data-stu-id="73a65-162">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="73a65-163">Hallo code maakt gebruik van een cursor op Hallo-verbinding en [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) methode voert de SQL-instructie Hallo tegen MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="73a65-163">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL statement against MySQL database.</span></span> <span data-ttu-id="73a65-164">Hallo gegevensrijen worden gelezen met Hallo [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) methode.</span><span class="sxs-lookup"><span data-stu-id="73a65-164">hello data rows are read using hello [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) method.</span></span> <span data-ttu-id="73a65-165">Hello resultaat wordt bewaard in de rij van een verzameling en een voor iterator gebruikte tooloop over Hallo rijen is.</span><span class="sxs-lookup"><span data-stu-id="73a65-165">hello result set is kept in a collection row and a for iterator is used tooloop over hello rows.</span></span>

<span data-ttu-id="73a65-166">Vervang Hallo `host`, `user`, `password`, en `database` parameters met Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="73a65-166">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="update-data"></a><span data-ttu-id="73a65-167">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="73a65-167">Update data</span></span>
<span data-ttu-id="73a65-168">Gebruik Hallo volgende tooconnect code en bij te werken Hallo gegevens met een **bijwerken** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="73a65-168">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="73a65-169">In Hallo code is Hallo mysql.connector bibliotheek geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="73a65-169">In hello code, hello mysql.connector library is imported.</span></span>  <span data-ttu-id="73a65-170">Hallo [Connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) functie is gebruikte tooconnect tooAzure Database voor MySQL Hallo met [verbinding argumenten](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in Hallo config-verzameling.</span><span class="sxs-lookup"><span data-stu-id="73a65-170">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="73a65-171">Hallo code maakt gebruik van een cursor op Hallo-verbinding en [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) methode voert de SQL-instructie Hallo tegen MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="73a65-171">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL statement against MySQL database.</span></span> 

<span data-ttu-id="73a65-172">Vervang Hallo `host`, `user`, `password`, en `database` parameters met Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="73a65-172">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="delete-data"></a><span data-ttu-id="73a65-173">Gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="73a65-173">Delete data</span></span>
<span data-ttu-id="73a65-174">Gebruik Hallo volgende tooconnect code en verwijderen van gegevens met een **verwijderen** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="73a65-174">Use hello following code tooconnect and remove data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="73a65-175">In Hallo code is Hallo mysql.connector bibliotheek geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="73a65-175">In hello code, hello mysql.connector library is imported.</span></span>  <span data-ttu-id="73a65-176">Hallo [Connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) functie is gebruikte tooconnect tooAzure Database voor MySQL Hallo met [verbinding argumenten](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in Hallo config-verzameling.</span><span class="sxs-lookup"><span data-stu-id="73a65-176">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="73a65-177">Hallo code maakt gebruik van een cursor op Hallo-verbinding en [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) methode voert Hallo SQL-query op MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="73a65-177">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="73a65-178">Vervang Hallo `host`, `user`, `password`, en `database` parameters met Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="73a65-178">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="73a65-179">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="73a65-179">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="73a65-180">Een database migreren met behulp van Exporteren en importeren</span><span class="sxs-lookup"><span data-stu-id="73a65-180">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
