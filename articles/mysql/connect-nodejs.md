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
# <a name="azure-database-for-mysql-use-nodejs-tooconnect-and-query-data"></a>Azure MySQL-Database: gebruikt Node.js tooconnect en query-gegevens
Deze snelstartgids demonstreert hoe tooconnect tooan Azure-Database voor het gebruik van MySQL [Node.js](https://nodejs.org/) van Windows, Ubuntu Linux en Mac-platforms. Er wordt weergegeven hoe toouse SQL-instructies tooquery invoegen, bijwerken en verwijderen van gegevens in Hallo-database. Hallo stappen in dit artikel wordt ervan uitgegaan dat u bekend bent met behulp van Node.js ontwikkelen, en dat u een nieuwe tooworking met Azure-Database voor MySQL bent.

## <a name="prerequisites"></a>Vereisten
Deze snelstartgids Hallo bronnen die zijn gemaakt in een van deze handleidingen als uitgangspunt gebruikt:
- [Een Azure-database voor een MySQL-server maken met behulp van Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Een Azure-database voor een MySQL-server maken met behulp van Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)

U moet ook het volgende doen:
- Hallo installeren [Node.js](https://nodejs.org) runtime.
- Installeer [mysql2](https://www.npmjs.com/package/mysql2) tooconnect tooMySQL van Hallo Node.js-toepassing van het pakket. 

## <a name="install-nodejs-and-hello-mysql-connector"></a>Installeer Node.js en Hallo MySQL-connector
Ga als volgt Hallo juiste instructies tooinstall Node.js afhankelijk van uw platform. Gebruik npm tooinstall hello mysql2 pakket en de bijbehorende afhankelijkheden in de projectmap.

### <a name="windows"></a>**Windows**
1. Ga naar Hallo [Node.js pagina met downloads](https://nodejs.org/en/download/) en selecteer de gewenste optie voor Windows installer.
2. Maak een lokale projectmap, zoals `nodejsmysql`. 
3. Hallo-opdrachtprompt en cd, zoals in de projectmap hello, starten`cd c:\nodejsmysql\`
4. Hallo NPM hulpprogramma tooinstall hello mysql2 bibliotheek in de projectmap Hallo worden uitgevoerd.

   ```cmd
   cd c:\nodejsmysql\
   "C:\Program Files\nodejs\npm" install mysql2
   "C:\Program Files\nodejs\npm" list
   ```

5. Hallo installatie controleren met Hallo `npm list` tekst voor de uitvoer `mysql2@1.3.5`.

### <a name="linux-ubuntu"></a>**Linux (Ubuntu)**
1. Voer Hallo deze opdrachten tooinstall **Node.js** en **npm** Hallo package manager voor Node.js.

   ```bash
   sudo apt-get install -y nodejs npm
   ```

2. Voer Hallo opdrachten toomake na een projectmap `mysqlnodejs` en Hallo mysql2 pakket in die map te installeren.

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```
3. Hallo installatie controleren met npm lijst uitvoertekst voor `mysql2@1.3.5`.

### <a name="mac-os"></a>**Mac OS**
1. Voer Hallo opdrachten tooinstall na **brew**, een eenvoudig te gebruiken Pakketbeheer voor Mac OS X en **Node.js**.

   ```bash
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install node
   ```
2. Voer Hallo opdrachten toomake na een projectmap `mysqlnodejs` en Hallo mysql2 pakket in die map te installeren.

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```

3. Hallo installatie controleren met Hallo `npm list` tekst voor de uitvoer `mysql2@1.3.6`. Hallo kan versienummer variëren als nieuwe patches worden vrijgegeven.

## <a name="get-connection-information"></a>Verbindingsgegevens ophalen
Hallo verbinding informatie die nodig is tooconnect toohello Azure Database voor MySQL niet ophalen. U moet Hallo van server volledig gekwalificeerde servernaam en aanmeldingsreferenties.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com/).
2. Klik in het linkerdeelvenster Hallo **alle resources**, en zoek vervolgens naar het Hallo-server die u hebt gemaakt (bijvoorbeeld **myserver4demo**).
3. Klik op de servernaam Hallo **myserver4demo**.
4. Selecteer Hallo-server **eigenschappen** pagina. Maak een notitie van Hallo **servernaam** en **aanmeldingsnaam van Server-beheerder**.
 ![Azure Database voor MySQL - Aanmeldgegevens van de serverbeheerder](./media/connect-nodejs/1_server-properties-name-login.png)
5. Als u uw aanmeldingsgegevens server bent vergeten, gaat u toohello **overzicht** pagina tooview Hallo Server admin-aanmeldingsnaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo.

## <a name="running-hello-javascript-code-in-nodejs"></a>Hallo JavaScript-code uitgevoerd in Node.js
1. Hallo JavaScript-code in tekstbestanden te plakken en opslaan in een projectmap met bestand extensie .js, zoals C:\nodejsmysql\createtable.js of /home/username/nodejsmysql/createtable.js
2. Hallo-opdrachtregel starten of bash-shell. Ga naar de projectmap `cd nodejsmysql`.
3. toorun Hallo-toepassing hello knooppunt opdracht gevolgd door Hallo bestandsnaam op, zoals `node createtable.js`.
4. Op Windows, als knooppunt-toepassing hello zich niet in uw omgeving variabele pad, wellicht moet u toouse Hallo volledig pad toolaunch Hallo knooppunttoepassing, zoals`"C:\Program Files\nodejs\node.exe" createtable.js`

## <a name="connect-create-table-and-insert-data"></a>Verbinden, tabel maken en gegevens invoegen
Gebruik Hallo volgende tooconnect code en laden van gegevens met Hallo **CREATE TABLE** en **INSERT INTO** SQL-instructies.

Hallo [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) methode gebruikte toointerface met Hallo MySQL-server is. Hallo [Connect ()](https://github.com/mysqljs/mysql#establishing-connections) functie gebruikte tooestablish Hallo verbinding toohello server is. Hallo [query()](https://github.com/mysqljs/mysql#performing-queries) functie gebruikte tooexecute Hallo SQL-query op MySQL-database is. 

Vervang Hallo `host`, `user`, `password`, en `database` parameters met Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.

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

## <a name="read-data"></a>Gegevens lezen
Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **Selecteer** SQL-instructie. 

Hallo [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) methode gebruikte toointerface met Hallo MySQL-server is. Hallo [Connect ()](https://github.com/mysqljs/mysql#establishing-connections) methode gebruikte tooestablish Hallo verbinding toohello server is. Hallo [query()](https://github.com/mysqljs/mysql#performing-queries) methode gebruikte tooexecute Hallo SQL-query op MySQL-database is. Hallo resultaten matrix is gebruikte toohold Hallo resultaten van Hallo-query.

Vervang Hallo `host`, `user`, `password`, en `database` parameters met Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.

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

## <a name="update-data"></a>Gegevens bijwerken
Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **UPDATE** SQL-instructie. 

Hallo [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) methode gebruikte toointerface met Hallo MySQL-server is. Hallo [Connect ()](https://github.com/mysqljs/mysql#establishing-connections) methode gebruikte tooestablish Hallo verbinding toohello server is. Hallo [query()](https://github.com/mysqljs/mysql#performing-queries) methode gebruikte tooexecute Hallo SQL-query op MySQL-database is. 

Vervang Hallo `host`, `user`, `password`, en `database` parameters met Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.

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

## <a name="delete-data"></a>Gegevens verwijderen
Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **verwijderen** SQL-instructie. 

Hallo [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) methode gebruikte toointerface met Hallo MySQL-server is. Hallo [Connect ()](https://github.com/mysqljs/mysql#establishing-connections) methode gebruikte tooestablish Hallo verbinding toohello server is. Hallo [query()](https://github.com/mysqljs/mysql#performing-queries) methode gebruikte tooexecute Hallo SQL-query op MySQL-database is. 

Vervang Hallo `host`, `user`, `password`, en `database` parameters met Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.

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

## <a name="next-steps"></a>Volgende stappen
> [!div class="nextstepaction"]
> [Een database migreren met behulp van Exporteren en importeren](./concepts-migrate-import-export.md)
