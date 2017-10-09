---
title: Verbinding maken met Database tooAzure voor MySQL van Node.js | Microsoft Docs
description: Deze snelstartgids bevat verschillende Node.js-codevoorbeelden kunt u een query over gegevens uit Azure-Database voor MySQL en tooconnect gebruiken.
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 07/17/2017
ms.openlocfilehash: ed9a39b5ab003e8216cef1c0f6a95a75c3db8458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-nodejs-tooconnect-and-query-data"></a><span data-ttu-id="2fa10-103">Azure MySQL-Database: gebruikt Node.js tooconnect en query-gegevens</span><span class="sxs-lookup"><span data-stu-id="2fa10-103">Azure Database for MySQL: Use Node.js tooconnect and query data</span></span>
<span data-ttu-id="2fa10-104">Deze snelstartgids demonstreert hoe tooconnect tooan Azure-Database voor het gebruik van MySQL [Node.js](https://nodejs.org/) van Windows, Ubuntu Linux en Mac-platforms.</span><span class="sxs-lookup"><span data-stu-id="2fa10-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using [Node.js](https://nodejs.org/) from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="2fa10-105">Er wordt weergegeven hoe toouse SQL-instructies tooquery invoegen, bijwerken en verwijderen van gegevens in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="2fa10-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="2fa10-106">Hallo stappen in dit artikel wordt ervan uitgegaan dat u bekend bent met behulp van Node.js ontwikkelen, en dat u een nieuwe tooworking met Azure-Database voor MySQL bent.</span><span class="sxs-lookup"><span data-stu-id="2fa10-106">hello steps in this article assume that you are familiar with developing using Node.js, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2fa10-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2fa10-107">Prerequisites</span></span>
<span data-ttu-id="2fa10-108">Deze snelstartgids Hallo bronnen die zijn gemaakt in een van deze handleidingen als uitgangspunt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="2fa10-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="2fa10-109">Een Azure-database voor een MySQL-server maken met behulp van Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2fa10-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="2fa10-110">Een Azure-database voor een MySQL-server maken met behulp van Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2fa10-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="2fa10-111">U moet ook het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="2fa10-111">You also need to:</span></span>
- <span data-ttu-id="2fa10-112">Hallo installeren [Node.js](https://nodejs.org) runtime.</span><span class="sxs-lookup"><span data-stu-id="2fa10-112">Install hello [Node.js](https://nodejs.org) runtime.</span></span>
- <span data-ttu-id="2fa10-113">Installeer [mysql2](https://www.npmjs.com/package/mysql2) tooconnect tooMySQL van Hallo Node.js-toepassing van het pakket.</span><span class="sxs-lookup"><span data-stu-id="2fa10-113">Install [mysql2](https://www.npmjs.com/package/mysql2) package tooconnect tooMySQL from hello Node.js application.</span></span> 

## <a name="install-nodejs-and-hello-mysql-connector"></a><span data-ttu-id="2fa10-114">Installeer Node.js en Hallo MySQL-connector</span><span class="sxs-lookup"><span data-stu-id="2fa10-114">Install Node.js and hello MySQL connector</span></span>
<span data-ttu-id="2fa10-115">Ga als volgt Hallo juiste instructies tooinstall Node.js afhankelijk van uw platform.</span><span class="sxs-lookup"><span data-stu-id="2fa10-115">Depending on your platform, follow hello appropriate instructions tooinstall Node.js.</span></span> <span data-ttu-id="2fa10-116">Gebruik npm tooinstall hello mysql2 pakket en de bijbehorende afhankelijkheden in de projectmap.</span><span class="sxs-lookup"><span data-stu-id="2fa10-116">Use npm tooinstall hello mysql2 package and its dependencies into your project folder.</span></span>

### <a name="windows"></a><span data-ttu-id="2fa10-117">**Windows**</span><span class="sxs-lookup"><span data-stu-id="2fa10-117">**Windows**</span></span>
1. <span data-ttu-id="2fa10-118">Ga naar Hallo [Node.js pagina met downloads](https://nodejs.org/en/download/) en selecteer de gewenste optie voor Windows installer.</span><span class="sxs-lookup"><span data-stu-id="2fa10-118">Visit hello [Node.js downloads page](https://nodejs.org/en/download/) and select your desired Windows installer option.</span></span>
2. <span data-ttu-id="2fa10-119">Maak een lokale projectmap, zoals `nodejsmysql`.</span><span class="sxs-lookup"><span data-stu-id="2fa10-119">Make a local project folder such as `nodejsmysql`.</span></span> 
3. <span data-ttu-id="2fa10-120">Hallo-opdrachtprompt en cd, zoals in de projectmap hello, starten`cd c:\nodejsmysql\`</span><span class="sxs-lookup"><span data-stu-id="2fa10-120">Launch hello command prompt and cd into hello project folder, such as `cd c:\nodejsmysql\`</span></span>
4. <span data-ttu-id="2fa10-121">Hallo NPM hulpprogramma tooinstall hello mysql2 bibliotheek in de projectmap Hallo worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2fa10-121">Run hello NPM tool tooinstall hello mysql2 library into hello project folder.</span></span>

   ```cmd
   cd c:\nodejsmysql\
   "C:\Program Files\nodejs\npm" install mysql2
   "C:\Program Files\nodejs\npm" list
   ```

5. <span data-ttu-id="2fa10-122">Hallo installatie controleren met Hallo `npm list` tekst voor de uitvoer `mysql2@1.3.5`.</span><span class="sxs-lookup"><span data-stu-id="2fa10-122">Verify hello installation by checking hello `npm list` output text for `mysql2@1.3.5`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="2fa10-123">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="2fa10-123">**Linux (Ubuntu)**</span></span>
1. <span data-ttu-id="2fa10-124">Voer Hallo deze opdrachten tooinstall **Node.js** en **npm** Hallo package manager voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="2fa10-124">Run hello following commands tooinstall **Node.js** and **npm** hello package manager for Node.js.</span></span>

   ```bash
   sudo apt-get install -y nodejs npm
   ```

2. <span data-ttu-id="2fa10-125">Voer Hallo opdrachten toomake na een projectmap `mysqlnodejs` en Hallo mysql2 pakket in die map te installeren.</span><span class="sxs-lookup"><span data-stu-id="2fa10-125">Run hello following commands toomake a project folder `mysqlnodejs` and install hello mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```
3. <span data-ttu-id="2fa10-126">Hallo installatie controleren met npm lijst uitvoertekst voor `mysql2@1.3.5`.</span><span class="sxs-lookup"><span data-stu-id="2fa10-126">Verify hello installation by checking npm list output text for `mysql2@1.3.5`.</span></span>

### <a name="mac-os"></a><span data-ttu-id="2fa10-127">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="2fa10-127">**Mac OS**</span></span>
1. <span data-ttu-id="2fa10-128">Voer Hallo opdrachten tooinstall na **brew**, een eenvoudig te gebruiken Pakketbeheer voor Mac OS X en **Node.js**.</span><span class="sxs-lookup"><span data-stu-id="2fa10-128">Enter hello following commands tooinstall **brew**, an easy-to-use package manager for Mac OS X and **Node.js**.</span></span>

   ```bash
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install node
   ```
2. <span data-ttu-id="2fa10-129">Voer Hallo opdrachten toomake na een projectmap `mysqlnodejs` en Hallo mysql2 pakket in die map te installeren.</span><span class="sxs-lookup"><span data-stu-id="2fa10-129">Run hello following commands toomake a project folder `mysqlnodejs` and install hello mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```

3. <span data-ttu-id="2fa10-130">Hallo installatie controleren met Hallo `npm list` tekst voor de uitvoer `mysql2@1.3.6`.</span><span class="sxs-lookup"><span data-stu-id="2fa10-130">Verify hello installation by checking hello `npm list` output text for `mysql2@1.3.6`.</span></span> <span data-ttu-id="2fa10-131">Hallo kan versienummer variëren als nieuwe patches worden vrijgegeven.</span><span class="sxs-lookup"><span data-stu-id="2fa10-131">hello version number may vary as new patches are released.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="2fa10-132">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="2fa10-132">Get connection information</span></span>
<span data-ttu-id="2fa10-133">Hallo verbinding informatie die nodig is tooconnect toohello Azure Database voor MySQL niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="2fa10-133">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="2fa10-134">U moet Hallo van server volledig gekwalificeerde servernaam en aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="2fa10-134">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="2fa10-135">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2fa10-135">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="2fa10-136">Klik in het linkerdeelvenster Hallo **alle resources**, en zoek vervolgens naar het Hallo-server die u hebt gemaakt (bijvoorbeeld **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="2fa10-136">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="2fa10-137">Klik op de servernaam Hallo **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="2fa10-137">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="2fa10-138">Selecteer Hallo-server **eigenschappen** pagina.</span><span class="sxs-lookup"><span data-stu-id="2fa10-138">Select hello server's **Properties** page.</span></span> <span data-ttu-id="2fa10-139">Maak een notitie van Hallo **servernaam** en **aanmeldingsnaam van Server-beheerder**.</span><span class="sxs-lookup"><span data-stu-id="2fa10-139">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="2fa10-140">![Azure Database voor MySQL - Aanmeldgegevens van de serverbeheerder](./media/connect-nodejs/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="2fa10-140">![Azure Database for MySQL - Server Admin Login](./media/connect-nodejs/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="2fa10-141">Als u uw aanmeldingsgegevens server bent vergeten, gaat u toohello **overzicht** pagina tooview Hallo Server admin-aanmeldingsnaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="2fa10-141">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="running-hello-javascript-code-in-nodejs"></a><span data-ttu-id="2fa10-142">Hallo JavaScript-code uitgevoerd in Node.js</span><span class="sxs-lookup"><span data-stu-id="2fa10-142">Running hello JavaScript code in Node.js</span></span>
1. <span data-ttu-id="2fa10-143">Hallo JavaScript-code in tekstbestanden te plakken en opslaan in een projectmap met bestand extensie .js, zoals C:\nodejsmysql\createtable.js of /home/username/nodejsmysql/createtable.js</span><span class="sxs-lookup"><span data-stu-id="2fa10-143">Paste hello JavaScript code into text files, and save into a project folder with file extension .js, such as C:\nodejsmysql\createtable.js or /home/username/nodejsmysql/createtable.js</span></span>
2. <span data-ttu-id="2fa10-144">Hallo-opdrachtregel starten of bash-shell.</span><span class="sxs-lookup"><span data-stu-id="2fa10-144">Launch hello command prompt or bash shell.</span></span> <span data-ttu-id="2fa10-145">Ga naar de projectmap `cd nodejsmysql`.</span><span class="sxs-lookup"><span data-stu-id="2fa10-145">Change directory into your project folder `cd nodejsmysql`.</span></span>
3. <span data-ttu-id="2fa10-146">toorun Hallo-toepassing hello knooppunt opdracht gevolgd door Hallo bestandsnaam op, zoals `node createtable.js`.</span><span class="sxs-lookup"><span data-stu-id="2fa10-146">toorun hello application, type hello node command followed by hello file name, such as `node createtable.js`.</span></span>
4. <span data-ttu-id="2fa10-147">Op Windows, als knooppunt-toepassing hello zich niet in uw omgeving variabele pad, wellicht moet u toouse Hallo volledig pad toolaunch Hallo knooppunttoepassing, zoals`"C:\Program Files\nodejs\node.exe" createtable.js`</span><span class="sxs-lookup"><span data-stu-id="2fa10-147">On Windows, if hello node application is not in your environment variable path, you may need toouse hello full path toolaunch hello node application, such as `"C:\Program Files\nodejs\node.exe" createtable.js`</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="2fa10-148">Verbinden, tabel maken en gegevens invoegen</span><span class="sxs-lookup"><span data-stu-id="2fa10-148">Connect, create table, and insert data</span></span>
<span data-ttu-id="2fa10-149">Gebruik Hallo volgende tooconnect code en laden van gegevens met Hallo **CREATE TABLE** en **INSERT INTO** SQL-instructies.</span><span class="sxs-lookup"><span data-stu-id="2fa10-149">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>

<span data-ttu-id="2fa10-150">Hallo [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) methode gebruikte toointerface met Hallo MySQL-server is.</span><span class="sxs-lookup"><span data-stu-id="2fa10-150">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="2fa10-151">Hallo [Connect ()](https://github.com/mysqljs/mysql#establishing-connections) functie gebruikte tooestablish Hallo verbinding toohello server is.</span><span class="sxs-lookup"><span data-stu-id="2fa10-151">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="2fa10-152">Hallo [query()](https://github.com/mysqljs/mysql#performing-queries) functie gebruikte tooexecute Hallo SQL-query op MySQL-database is.</span><span class="sxs-lookup"><span data-stu-id="2fa10-152">hello [query()](https://github.com/mysqljs/mysql#performing-queries) function is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="2fa10-153">Vervang Hallo `host`, `user`, `password`, en `database` parameters met Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2fa10-153">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
    if (err) { 
        console.log("!!! Cannot connect !!! Error:");
        throw err;
    }
    else
    {
       console.log("Connection established.");
           queryDatabase();
    }   
});

function queryDatabase(){
       conn.query('DROP TABLE IF EXISTS inventory;', function (err, results, fields) { 
            if (err) throw err; 
            console.log('Dropped inventory table if existed.');
        })
       conn.query('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);', 
            function (err, results, fields) {
                if (err) throw err;
            console.log('Created inventory table.');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['banana', 150], 
            function (err, results, fields) {
                if (err) throw err;
            else console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['orange', 154], 
            function (err, results, fields) {
                if (err) throw err;
            console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['apple', 100], 
        function (err, results, fields) {
                if (err) throw err;
            console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.end(function (err) { 
        if (err) throw err;
        else  console.log('Done.') 
        });
};
```

## <a name="read-data"></a><span data-ttu-id="2fa10-154">Gegevens lezen</span><span class="sxs-lookup"><span data-stu-id="2fa10-154">Read data</span></span>
<span data-ttu-id="2fa10-155">Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **Selecteer** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="2fa10-155">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="2fa10-156">Hallo [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) methode gebruikte toointerface met Hallo MySQL-server is.</span><span class="sxs-lookup"><span data-stu-id="2fa10-156">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="2fa10-157">Hallo [Connect ()](https://github.com/mysqljs/mysql#establishing-connections) methode gebruikte tooestablish Hallo verbinding toohello server is.</span><span class="sxs-lookup"><span data-stu-id="2fa10-157">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="2fa10-158">Hallo [query()](https://github.com/mysqljs/mysql#performing-queries) methode gebruikte tooexecute Hallo SQL-query op MySQL-database is.</span><span class="sxs-lookup"><span data-stu-id="2fa10-158">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> <span data-ttu-id="2fa10-159">Hallo resultaten matrix is gebruikte toohold Hallo resultaten van Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="2fa10-159">hello results array is used toohold hello results of hello query.</span></span>

<span data-ttu-id="2fa10-160">Vervang Hallo `host`, `user`, `password`, en `database` parameters met Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2fa10-160">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            readData();
        }   
    });

function readData(){
        conn.query('SELECT * FROM inventory', 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Selected ' + results.length + ' row(s).');
                for (i = 0; i < results.length; i++) {
                    console.log('Row: ' + JSON.stringify(results[i]));
                }
                console.log('Done.');
            })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Closing connection.') 
        });
};
```

## <a name="update-data"></a><span data-ttu-id="2fa10-161">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="2fa10-161">Update data</span></span>
<span data-ttu-id="2fa10-162">Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **UPDATE** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="2fa10-162">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="2fa10-163">Hallo [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) methode gebruikte toointerface met Hallo MySQL-server is.</span><span class="sxs-lookup"><span data-stu-id="2fa10-163">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="2fa10-164">Hallo [Connect ()](https://github.com/mysqljs/mysql#establishing-connections) methode gebruikte tooestablish Hallo verbinding toohello server is.</span><span class="sxs-lookup"><span data-stu-id="2fa10-164">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="2fa10-165">Hallo [query()](https://github.com/mysqljs/mysql#performing-queries) methode gebruikte tooexecute Hallo SQL-query op MySQL-database is.</span><span class="sxs-lookup"><span data-stu-id="2fa10-165">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="2fa10-166">Vervang Hallo `host`, `user`, `password`, en `database` parameters met Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2fa10-166">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            updateData();
        }   
    });

function updateData(){
       conn.query('UPDATE inventory SET quantity = ? WHERE name = ?', [200, 'banana'], 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Updated ' + results.affectedRows + ' row(s).');
        })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Done.') 
        });
};
```

## <a name="delete-data"></a><span data-ttu-id="2fa10-167">Gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="2fa10-167">Delete data</span></span>
<span data-ttu-id="2fa10-168">Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **verwijderen** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="2fa10-168">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="2fa10-169">Hallo [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) methode gebruikte toointerface met Hallo MySQL-server is.</span><span class="sxs-lookup"><span data-stu-id="2fa10-169">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="2fa10-170">Hallo [Connect ()](https://github.com/mysqljs/mysql#establishing-connections) methode gebruikte tooestablish Hallo verbinding toohello server is.</span><span class="sxs-lookup"><span data-stu-id="2fa10-170">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="2fa10-171">Hallo [query()](https://github.com/mysqljs/mysql#performing-queries) methode gebruikte tooexecute Hallo SQL-query op MySQL-database is.</span><span class="sxs-lookup"><span data-stu-id="2fa10-171">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="2fa10-172">Vervang Hallo `host`, `user`, `password`, en `database` parameters met Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2fa10-172">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            deleteData();
        }   
    });

function deleteData(){
       conn.query('DELETE FROM inventory WHERE name = ?', ['orange'], 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Deleted ' + results.affectedRows + ' row(s).');
        })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Done.') 
        });
};
```

## <a name="next-steps"></a><span data-ttu-id="2fa10-173">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2fa10-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="2fa10-174">Een database migreren met behulp van Exporteren en importeren</span><span class="sxs-lookup"><span data-stu-id="2fa10-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
