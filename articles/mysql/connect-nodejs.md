---
title: Vanuit Node.js verbinding maken met Azure Database voor MySQL | Microsoft Docs
description: Deze snelstartgids bevat enkele voorbeelden van Node.js-code die u kunt gebruiken om verbinding te maken met en gegevens op te vragen uit Azure Database voor MySQL.
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
ms.openlocfilehash: 0c0bd4b707c114d2991e5f0473a4bfbe9e463e3c
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="azure-database-for-mysql-use-nodejs-to-connect-and-query-data"></a><span data-ttu-id="5c8a9-103">Azure Database voor MySQL: Node.js gebruiken om verbinding te maken en query's uit te voeren op gegevens</span><span class="sxs-lookup"><span data-stu-id="5c8a9-103">Azure Database for MySQL: Use Node.js to connect and query data</span></span>
<span data-ttu-id="5c8a9-104">In deze snelstartgids ziet u hoe u vanuit de platformen Windows, Ubuntu Linux, en Mac met behulp van [Node.js](https://nodejs.org/) verbinding maakt met een Azure Database voor MySQL.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using [Node.js](https://nodejs.org/) from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="5c8a9-105">U ziet hier hoe u SQL-instructies gebruikt om gegevens in de database op te vragen, in te voegen, bij te werken en te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="5c8a9-106">In de stappen van dit artikel wordt ervan uitgegaan dat u bekend bent met het ontwikkelen met behulp van Node.js, maar geen ervaring hebt met het werken met Azure Database voor MySQL.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-106">The steps in this article assume that you are familiar with developing using Node.js, and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c8a9-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5c8a9-107">Prerequisites</span></span>
<span data-ttu-id="5c8a9-108">In deze snelstartgids worden de resources die in een van deze handleidingen zijn gemaakt, als uitgangspunt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="5c8a9-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="5c8a9-109">Een Azure-database voor een MySQL-server maken met behulp van Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5c8a9-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="5c8a9-110">Een Azure-database voor een MySQL-server maken met behulp van Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5c8a9-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="5c8a9-111">U moet ook het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="5c8a9-111">You also need to:</span></span>
- <span data-ttu-id="5c8a9-112">De [Node.js](https://nodejs.org)-runtime installeren.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-112">Install the [Node.js](https://nodejs.org) runtime.</span></span>
- <span data-ttu-id="5c8a9-113">Het [mysql2](https://www.npmjs.com/package/mysql2)-pakket installeren om vanuit de Node.js-toepassing verbinding te maken met MySQL.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-113">Install [mysql2](https://www.npmjs.com/package/mysql2) package to connect to MySQL from the Node.js application.</span></span> 

## <a name="install-nodejs-and-the-mysql-connector"></a><span data-ttu-id="5c8a9-114">Node.js en de MySQL-connector installeren</span><span class="sxs-lookup"><span data-stu-id="5c8a9-114">Install Node.js and the MySQL connector</span></span>
<span data-ttu-id="5c8a9-115">Volg afhankelijk van uw platform de juiste instructies voor het installeren van Node.js.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-115">Depending on your platform, follow the appropriate instructions to install Node.js.</span></span> <span data-ttu-id="5c8a9-116">Gebruik NPM voor het installeren van het mysql2-pakket en de bijbehorende afhankelijkheden in de projectmap.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-116">Use npm to install the mysql2 package and its dependencies into your project folder.</span></span>

### <a name="windows"></a><span data-ttu-id="5c8a9-117">**Windows**</span><span class="sxs-lookup"><span data-stu-id="5c8a9-117">**Windows**</span></span>
1. <span data-ttu-id="5c8a9-118">Ga naar de [downloadpagina van Node.js](https://nodejs.org/en/download/) en selecteer het gewenste Windows-installatieprogramma.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-118">Visit the [Node.js downloads page](https://nodejs.org/en/download/) and select your desired Windows installer option.</span></span>
2. <span data-ttu-id="5c8a9-119">Maak een lokale projectmap, zoals `nodejsmysql`.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-119">Make a local project folder such as `nodejsmysql`.</span></span> 
3. <span data-ttu-id="5c8a9-120">Start de opdrachtprompt en ga naar de juiste projectmap, zoals `cd c:\nodejsmysql\`</span><span class="sxs-lookup"><span data-stu-id="5c8a9-120">Launch the command prompt and cd into the project folder, such as `cd c:\nodejsmysql\`</span></span>
4. <span data-ttu-id="5c8a9-121">Voer het hulpprogramma NPM uit om de mysql2-bibliotheek in de projectmap te installeren.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-121">Run the NPM tool to install the mysql2 library into the project folder.</span></span>

   ```cmd
   cd c:\nodejsmysql\
   "C:\Program Files\nodejs\npm" install mysql2
   "C:\Program Files\nodejs\npm" list
   ```

5. <span data-ttu-id="5c8a9-122">Controleer de installatie door de `npm list`-uitvoertekst voor `mysql2@1.3.5` te controleren.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-122">Verify the installation by checking the `npm list` output text for `mysql2@1.3.5`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="5c8a9-123">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="5c8a9-123">**Linux (Ubuntu)**</span></span>
1. <span data-ttu-id="5c8a9-124">Voer de volgende opdrachten uit om **Node.js** en **NPM**, het pakketbeheerprogramma voor Node.js, te installeren.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-124">Run the following commands to install **Node.js** and **npm** the package manager for Node.js.</span></span>

   ```bash
   sudo apt-get install -y nodejs npm
   ```

2. <span data-ttu-id="5c8a9-125">Voer de volgende opdrachten uit om een projectmap `mysqlnodejs` te maken en installeer het mysql2-pakket in die map.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-125">Run the following commands to make a project folder `mysqlnodejs` and install the mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```
3. <span data-ttu-id="5c8a9-126">Controleer de installatie door de uitvoertekst van de npm-lijst te controleren voor `mysql2@1.3.5`.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-126">Verify the installation by checking npm list output text for `mysql2@1.3.5`.</span></span>

### <a name="mac-os"></a><span data-ttu-id="5c8a9-127">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="5c8a9-127">**Mac OS**</span></span>
1. <span data-ttu-id="5c8a9-128">Voer de volgende opdrachten in om **brew** te installeren, een gebruiksvriendelijk pakketbeheerprogramma voor Mac OS X en **Node.js**.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-128">Enter the following commands to install **brew**, an easy-to-use package manager for Mac OS X and **Node.js**.</span></span>

   ```bash
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install node
   ```
2. <span data-ttu-id="5c8a9-129">Voer de volgende opdrachten uit om een projectmap `mysqlnodejs` te maken en installeer het mysql2-pakket in die map.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-129">Run the following commands to make a project folder `mysqlnodejs` and install the mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```

3. <span data-ttu-id="5c8a9-130">Controleer de installatie door de `npm list`-uitvoertekst voor `mysql2@1.3.6` te controleren.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-130">Verify the installation by checking the `npm list` output text for `mysql2@1.3.6`.</span></span> <span data-ttu-id="5c8a9-131">Het versienummer kan variëren als nieuwe patches worden vrijgegeven.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-131">The version number may vary as new patches are released.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="5c8a9-132">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="5c8a9-132">Get connection information</span></span>
<span data-ttu-id="5c8a9-133">Haal de verbindingsgegevens op die nodig zijn om verbinding te maken met de Azure Database voor MySQL.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-133">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="5c8a9-134">U hebt de volledig gekwalificeerde servernaam en aanmeldingsreferenties nodig.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-134">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="5c8a9-135">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5c8a9-135">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5c8a9-136">Klik in het linkerdeelvenster op **Alle resources** en zoek vervolgens naar de server die u hebt gemaakt (bijvoorbeeld **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="5c8a9-136">In the left pane, click **All resources**, and then search for the server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="5c8a9-137">Klik op de servernaam **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-137">Click the server name **myserver4demo**.</span></span>
4. <span data-ttu-id="5c8a9-138">Selecteer de pagina **Eigenschappen** van de server.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-138">Select the server's **Properties** page.</span></span> <span data-ttu-id="5c8a9-139">Noteer de **servernaam** en de **gebruikersnaam van de serverbeheerder**.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-139">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="5c8a9-140">![Azure Database voor MySQL - Aanmeldgegevens van de serverbeheerder](./media/connect-nodejs/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="5c8a9-140">![Azure Database for MySQL - Server Admin Login](./media/connect-nodejs/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="5c8a9-141">Als u uw aanmeldingsgegevens voor de server bent vergeten, gaat u naar de pagina **Overzicht** om de aanmeldingsnaam van de serverbeheerder weer te geven en indien nodig het wachtwoord opnieuw in te stellen.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-141">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="running-the-javascript-code-in-nodejs"></a><span data-ttu-id="5c8a9-142">De JavaScript-code in Node.js uitvoeren</span><span class="sxs-lookup"><span data-stu-id="5c8a9-142">Running the JavaScript code in Node.js</span></span>
1. <span data-ttu-id="5c8a9-143">Plak de JavaScript-code in tekstbestanden en sla deze op in een projectmap met de bestandsextensie .js, zoals C:\nodejsmysql\createtable.js of /home/username/nodejsmysql/createtable.js</span><span class="sxs-lookup"><span data-stu-id="5c8a9-143">Paste the JavaScript code into text files, and save into a project folder with file extension .js, such as C:\nodejsmysql\createtable.js or /home/username/nodejsmysql/createtable.js</span></span>
2. <span data-ttu-id="5c8a9-144">Open de opdrachtprompt of de bash-shell.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-144">Launch the command prompt or bash shell.</span></span> <span data-ttu-id="5c8a9-145">Ga naar de projectmap `cd nodejsmysql`.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-145">Change directory into your project folder `cd nodejsmysql`.</span></span>
3. <span data-ttu-id="5c8a9-146">Typ de knooppuntopdracht, gevolgd door de bestandsnaam `node createtable.js` om de toepassing uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-146">To run the application, type the node command followed by the file name, such as `node createtable.js`.</span></span>
4. <span data-ttu-id="5c8a9-147">In Windows moet u als de knooppunttoepassing zich niet in uw omgevingsvariabelepad bevindt mogelijk het volledige pad gebruiken om de knooppunttoepassing te starten, zoals `"C:\Program Files\nodejs\node.exe" createtable.js`</span><span class="sxs-lookup"><span data-stu-id="5c8a9-147">On Windows, if the node application is not in your environment variable path, you may need to use the full path to launch the node application, such as `"C:\Program Files\nodejs\node.exe" createtable.js`</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="5c8a9-148">Verbinden, tabel maken en gegevens invoegen</span><span class="sxs-lookup"><span data-stu-id="5c8a9-148">Connect, create table, and insert data</span></span>
<span data-ttu-id="5c8a9-149">Gebruik de volgende code om verbinding te maken en de gegevens te laden met de SQL-instructies **CREATE TABLE** EN **INSERT INTO**.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-149">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>

<span data-ttu-id="5c8a9-150">De methode [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) wordt gebruikt om een koppeling te maken met de MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-150">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="5c8a9-151">De functie [connect()](https://github.com/mysqljs/mysql#establishing-connections) wordt gebruikt om verbinding met de server te maken.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-151">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) function is used to establish the connection to the server.</span></span> <span data-ttu-id="5c8a9-152">De functie [query()](https://github.com/mysqljs/mysql#performing-queries) wordt gebruikt om de SQL-query uit te voeren op de MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-152">The [query()](https://github.com/mysqljs/mysql#performing-queries) function is used to execute the SQL query against MySQL database.</span></span> 

<span data-ttu-id="5c8a9-153">Vervang de parameters `host`, `user`, `password` en `database` door de waarden die u hebt opgegeven tijdens het maken van de server en database.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-153">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

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

## <a name="read-data"></a><span data-ttu-id="5c8a9-154">Gegevens lezen</span><span class="sxs-lookup"><span data-stu-id="5c8a9-154">Read data</span></span>
<span data-ttu-id="5c8a9-155">Gebruik de volgende code om verbinding te maken en de gegevens te lezen met de SQL-instructie **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-155">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="5c8a9-156">De methode [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) wordt gebruikt om een koppeling te maken met de MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-156">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="5c8a9-157">De methode [connect()](https://github.com/mysqljs/mysql#establishing-connections) wordt gebruikt om verbinding met de server te maken.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-157">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used to establish the connection to the server.</span></span> <span data-ttu-id="5c8a9-158">De methode [query()](https://github.com/mysqljs/mysql#performing-queries) wordt gebruikt om de SQL-query uit te voeren op de MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-158">The [query()](https://github.com/mysqljs/mysql#performing-queries) method is used to execute the SQL query against MySQL database.</span></span> <span data-ttu-id="5c8a9-159">De resultatenmatrix wordt gebruikt om de resultaten van de query op te slaan.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-159">The results array is used to hold the results of the query.</span></span>

<span data-ttu-id="5c8a9-160">Vervang de parameters `host`, `user`, `password` en `database` door de waarden die u hebt opgegeven tijdens het maken van de server en database.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-160">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

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

## <a name="update-data"></a><span data-ttu-id="5c8a9-161">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="5c8a9-161">Update data</span></span>
<span data-ttu-id="5c8a9-162">Gebruik de volgende code om verbinding te maken en de gegevens te lezen met de SQL-instructie **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-162">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="5c8a9-163">De methode [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) wordt gebruikt om een koppeling te maken met de MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-163">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="5c8a9-164">De methode [connect()](https://github.com/mysqljs/mysql#establishing-connections) wordt gebruikt om verbinding met de server te maken.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-164">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used to establish the connection to the server.</span></span> <span data-ttu-id="5c8a9-165">De methode [query()](https://github.com/mysqljs/mysql#performing-queries) wordt gebruikt om de SQL-query uit te voeren op de MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-165">The [query()](https://github.com/mysqljs/mysql#performing-queries) method is used to execute the SQL query against MySQL database.</span></span> 

<span data-ttu-id="5c8a9-166">Vervang de parameters `host`, `user`, `password` en `database` door de waarden die u hebt opgegeven tijdens het maken van de server en database.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-166">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

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

## <a name="delete-data"></a><span data-ttu-id="5c8a9-167">Gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="5c8a9-167">Delete data</span></span>
<span data-ttu-id="5c8a9-168">Gebruik de volgende code om verbinding te maken en de gegevens te lezen met de SQL-instructie **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-168">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="5c8a9-169">De methode [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) wordt gebruikt om een koppeling te maken met de MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-169">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="5c8a9-170">De methode [connect()](https://github.com/mysqljs/mysql#establishing-connections) wordt gebruikt om verbinding met de server te maken.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-170">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used to establish the connection to the server.</span></span> <span data-ttu-id="5c8a9-171">De methode [query()](https://github.com/mysqljs/mysql#performing-queries) wordt gebruikt om de SQL-query uit te voeren op de MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-171">The [query()](https://github.com/mysqljs/mysql#performing-queries) method is used to execute the SQL query against MySQL database.</span></span> 

<span data-ttu-id="5c8a9-172">Vervang de parameters `host`, `user`, `password` en `database` door de waarden die u hebt opgegeven tijdens het maken van de server en database.</span><span class="sxs-lookup"><span data-stu-id="5c8a9-172">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5c8a9-173">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5c8a9-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="5c8a9-174">Een database migreren met behulp van Exporteren en importeren</span><span class="sxs-lookup"><span data-stu-id="5c8a9-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
