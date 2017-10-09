---
title: Verbinding maken met Database tooAzure voor PostgreSQL van Node.js | Microsoft Docs
description: Deze snelstartgids bevat een Node.js-codevoorbeeld kunt u een query over gegevens uit Azure-Database voor PostgreSQL en tooconnect gebruiken.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: nodejs
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: 9b269d72068ecc24bcf3fb447a2efeda512c698c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-nodejs-tooconnect-and-query-data"></a>Azure-Database voor PostgreSQL: gebruik Node.js tooconnect en query-gegevens
Deze snelstartgids demonstreert hoe tooconnect tooan Azure-Database voor het gebruik van PostgreSQL [Node.js](https://nodejs.org/). Er wordt weergegeven hoe toouse SQL-instructies tooquery invoegen, bijwerken en verwijderen van gegevens in Hallo-database. Hallo stappen in dit artikel wordt ervan uitgegaan dat u bekend bent met behulp van Node.js ontwikkelen, en dat u een nieuwe tooworking met Azure-Database voor PostgreSQL bent.

## <a name="prerequisites"></a>Vereisten
Deze snelstartgids Hallo bronnen die zijn gemaakt in een van deze handleidingen als uitgangspunt gebruikt:
- [Database maken - Portal](quickstart-create-server-database-portal.md)
- [Database maken - CLI](quickstart-create-server-database-azure-cli.md)

U moet ook het volgende doen:
- [Node.js](https://nodejs.org) installeren

## <a name="install-pg-client"></a>pg-client installeren
Installeer [pg](https://www.npmjs.com/package/pg), dit is een PostgreSQL-client voor Node.js.

toodo dus Pakketbeheer Hallo-knooppunt (npm) voor JavaScript uitvoeren van de opdrachtregel tooinstall Hallo pg-client.
```bash
npm install pg
```

Hallo installatie controleren door hello-pakketten die zijn geïnstalleerd.
```bash
npm list
```

## <a name="get-connection-information"></a>Verbindingsgegevens ophalen
Hallo verbinding informatie die nodig is tooconnect toohello Azure Database voor PostgreSQL niet ophalen. U moet Hallo van server volledig gekwalificeerde servernaam en aanmeldingsreferenties.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com/).
2. Hallo links menu in Azure-portal en klik op **alle resources** en zoek naar Hallo-server die u zojuist hebt gemaakt.
3. Klik op Hallo servernaam.
4. Selecteer Hallo-server **overzicht** pagina. Maak een notitie van Hallo **servernaam** en **aanmeldingsnaam van Server-beheerder**.
 ![Azure Database voor PostgreSQL - Aanmeldgegevens van de serverbeheerder](./media/connect-nodejs/1-connection-string.png)
5. Als u uw aanmeldingsgegevens server bent vergeten, gaat u toohello **overzicht** pagina tooview Hallo Server admin-aanmeldingsnaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo.

## <a name="running-hello-javascript-code-in-nodejs"></a>Hallo JavaScript-code uitgevoerd in Node.js
U mag Node.js vanaf Hallo-bash-shell of windows opdrachtprompt starten door in te voeren `node`, Hallo voorbeeld JavaScript-code interactief worden uitgevoerd door kopiëren en plakken naar het Hallo-prompt. U kunt ook Hallo JavaScript-code opslaan in een tekstbestand in en start `node filename.js` met Hallo-bestandsnaam als een parameter toorun deze.

## <a name="connect-create-table-and-insert-data"></a>Verbinden, tabel maken en gegevens invoegen
Gebruik Hallo volgende tooconnect code en laden van gegevens met Hallo **CREATE TABLE** en **INSERT INTO** SQL-instructies.
Hallo [pg. Client](https://github.com/brianc/node-postgres/wiki/Client) -object is gebruikte toointerface met Hallo PostgreSQL-server. Hallo [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) functie gebruikte tooestablish Hallo verbinding toohello server is. Hallo [pg. Client.query()](https://github.com/brianc/node-postgres/wiki/Query) functie gebruikte tooexecute Hallo SQL-query op PostgreSQL-database is. 

Vervangen door Hallo host, dbname, gebruiker en wachtwoordparameters Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        DROP TABLE IF EXISTS inventory;
        CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
        INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
        INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
        INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    `;

    client
        .query(query)
        .then(() => {
            console.log('Table created successfully!');
            client.end(console.log('Closed client connection'));
        })
        .catch(err => console.log(err))
        .then(() => {
            console.log('Finished execution, exiting now');
            process.exit();
        });
}
```

## <a name="read-data"></a>Gegevens lezen
Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **Selecteer** SQL-instructie. Hallo [pg. Client](https://github.com/brianc/node-postgres/wiki/Client) -object is gebruikte toointerface met Hallo PostgreSQL-server. Hallo [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) functie gebruikte tooestablish Hallo verbinding toohello server is. Hallo [pg. Client.query()](https://github.com/brianc/node-postgres/wiki/Query) functie gebruikte tooexecute Hallo SQL-query op PostgreSQL-database is. 

Vervangen door Hallo host, dbname, gebruiker en wachtwoordparameters Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt. 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else { queryDatabase(); }
});

function queryDatabase() {
  
    console.log(`Running query tooPostgreSQL server: ${config.host}`);

    const query = 'SELECT * FROM inventory;';

    client.query(query)
        .then(res => {
            const rows = res.rows;

            rows.map(row => {
                console.log(`Read: ${JSON.stringify(row)}`);
            });

            process.exit();
        })
        .catch(err => {
            console.log(err);
        });
}
```

## <a name="update-data"></a>Gegevens bijwerken
Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **UPDATE** SQL-instructie. Hallo [pg. Client](https://github.com/brianc/node-postgres/wiki/Client) -object is gebruikte toointerface met Hallo PostgreSQL-server. Hallo [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) functie gebruikte tooestablish Hallo verbinding toohello server is. Hallo [pg. Client.query()](https://github.com/brianc/node-postgres/wiki/Query) functie gebruikte tooexecute Hallo SQL-query op PostgreSQL-database is. 

Vervangen door Hallo host, dbname, gebruiker en wachtwoordparameters Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt. 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        UPDATE inventory 
        SET quantity= 1000 WHERE name='banana';
    `;

    client
        .query(query)
        .then(result => {
            console.log('Update completed');
            console.log(`Rows affected: ${result.rowCount}`);
        })
        .catch(err => {
            console.log(err);
            throw err;
        });
}
```

## <a name="delete-data"></a>Gegevens verwijderen
Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **verwijderen** SQL-instructie. Hallo [pg. Client](https://github.com/brianc/node-postgres/wiki/Client) -object is gebruikte toointerface met Hallo PostgreSQL-server. Hallo [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) functie gebruikte tooestablish Hallo verbinding toohello server is. Hallo [pg. Client.query()](https://github.com/brianc/node-postgres/wiki/Query) functie gebruikte tooexecute Hallo SQL-query op PostgreSQL-database is. 

Vervangen door Hallo host, dbname, gebruiker en wachtwoordparameters Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt. 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) {
        throw err;
    } else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        DELETE FROM inventory 
        WHERE name = 'apple';
    `;

    client
        .query(query)
        .then(result => {
            console.log('Delete completed');
            console.log(`Rows affected: ${result.rowCount}`);
        })
        .catch(err => {
            console.log(err);
            throw err;
        });
}
```

## <a name="next-steps"></a>Volgende stappen
> [!div class="nextstepaction"]
> [Een database migreren met behulp van Exporteren en importeren](./howto-migrate-using-export-and-import.md)
