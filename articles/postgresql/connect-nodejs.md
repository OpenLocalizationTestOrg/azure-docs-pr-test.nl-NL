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
# <a name="azure-database-for-postgresql-use-nodejs-tooconnect-and-query-data"></a><span data-ttu-id="6fa62-103">Azure-Database voor PostgreSQL: gebruik Node.js tooconnect en query-gegevens</span><span class="sxs-lookup"><span data-stu-id="6fa62-103">Azure Database for PostgreSQL: Use Node.js tooconnect and query data</span></span>
<span data-ttu-id="6fa62-104">Deze snelstartgids demonstreert hoe tooconnect tooan Azure-Database voor het gebruik van PostgreSQL [Node.js](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="6fa62-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using [Node.js](https://nodejs.org/).</span></span> <span data-ttu-id="6fa62-105">Er wordt weergegeven hoe toouse SQL-instructies tooquery invoegen, bijwerken en verwijderen van gegevens in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="6fa62-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="6fa62-106">Hallo stappen in dit artikel wordt ervan uitgegaan dat u bekend bent met behulp van Node.js ontwikkelen, en dat u een nieuwe tooworking met Azure-Database voor PostgreSQL bent.</span><span class="sxs-lookup"><span data-stu-id="6fa62-106">hello steps in this article assume that you are familiar with developing using Node.js, and that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6fa62-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6fa62-107">Prerequisites</span></span>
<span data-ttu-id="6fa62-108">Deze snelstartgids Hallo bronnen die zijn gemaakt in een van deze handleidingen als uitgangspunt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="6fa62-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="6fa62-109">Database maken - Portal</span><span class="sxs-lookup"><span data-stu-id="6fa62-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="6fa62-110">Database maken - CLI</span><span class="sxs-lookup"><span data-stu-id="6fa62-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="6fa62-111">U moet ook het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="6fa62-111">You also need to:</span></span>
- <span data-ttu-id="6fa62-112">[Node.js](https://nodejs.org) installeren</span><span class="sxs-lookup"><span data-stu-id="6fa62-112">Install [Node.js](https://nodejs.org)</span></span>

## <a name="install-pg-client"></a><span data-ttu-id="6fa62-113">pg-client installeren</span><span class="sxs-lookup"><span data-stu-id="6fa62-113">Install pg client</span></span>
<span data-ttu-id="6fa62-114">Installeer [pg](https://www.npmjs.com/package/pg), dit is een PostgreSQL-client voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="6fa62-114">Install [pg](https://www.npmjs.com/package/pg), which is a PostgreSQL client for Node.js.</span></span>

<span data-ttu-id="6fa62-115">toodo dus Pakketbeheer Hallo-knooppunt (npm) voor JavaScript uitvoeren van de opdrachtregel tooinstall Hallo pg-client.</span><span class="sxs-lookup"><span data-stu-id="6fa62-115">toodo so, run hello node package manager (npm) for JavaScript from your command line tooinstall hello pg client.</span></span>
```bash
npm install pg
```

<span data-ttu-id="6fa62-116">Hallo installatie controleren door hello-pakketten die zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="6fa62-116">Verify hello installation by listing hello packages installed.</span></span>
```bash
npm list
```

## <a name="get-connection-information"></a><span data-ttu-id="6fa62-117">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="6fa62-117">Get connection information</span></span>
<span data-ttu-id="6fa62-118">Hallo verbinding informatie die nodig is tooconnect toohello Azure Database voor PostgreSQL niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="6fa62-118">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="6fa62-119">U moet Hallo van server volledig gekwalificeerde servernaam en aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="6fa62-119">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="6fa62-120">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6fa62-120">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6fa62-121">Hallo links menu in Azure-portal en klik op **alle resources** en zoek naar Hallo-server die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6fa62-121">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you just created.</span></span>
3. <span data-ttu-id="6fa62-122">Klik op Hallo servernaam.</span><span class="sxs-lookup"><span data-stu-id="6fa62-122">Click hello server name.</span></span>
4. <span data-ttu-id="6fa62-123">Selecteer Hallo-server **overzicht** pagina.</span><span class="sxs-lookup"><span data-stu-id="6fa62-123">Select hello server's **Overview** page.</span></span> <span data-ttu-id="6fa62-124">Maak een notitie van Hallo **servernaam** en **aanmeldingsnaam van Server-beheerder**.</span><span class="sxs-lookup"><span data-stu-id="6fa62-124">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="6fa62-125">![Azure Database voor PostgreSQL - Aanmeldgegevens van de serverbeheerder](./media/connect-nodejs/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="6fa62-125">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-nodejs/1-connection-string.png)</span></span>
5. <span data-ttu-id="6fa62-126">Als u uw aanmeldingsgegevens server bent vergeten, gaat u toohello **overzicht** pagina tooview Hallo Server admin-aanmeldingsnaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="6fa62-126">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="running-hello-javascript-code-in-nodejs"></a><span data-ttu-id="6fa62-127">Hallo JavaScript-code uitgevoerd in Node.js</span><span class="sxs-lookup"><span data-stu-id="6fa62-127">Running hello JavaScript code in Node.js</span></span>
<span data-ttu-id="6fa62-128">U mag Node.js vanaf Hallo-bash-shell of windows opdrachtprompt starten door in te voeren `node`, Hallo voorbeeld JavaScript-code interactief worden uitgevoerd door kopiëren en plakken naar het Hallo-prompt.</span><span class="sxs-lookup"><span data-stu-id="6fa62-128">You may launch Node.js from hello bash shell or windows command prompt by typing `node`, then run hello example JavaScript code interactively by copy and pasting it onto hello prompt.</span></span> <span data-ttu-id="6fa62-129">U kunt ook Hallo JavaScript-code opslaan in een tekstbestand in en start `node filename.js` met Hallo-bestandsnaam als een parameter toorun deze.</span><span class="sxs-lookup"><span data-stu-id="6fa62-129">Alternatively, you may save hello JavaScript code into a text file and launch `node filename.js` with hello file name as a parameter toorun it.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="6fa62-130">Verbinden, tabel maken en gegevens invoegen</span><span class="sxs-lookup"><span data-stu-id="6fa62-130">Connect, create table, and insert data</span></span>
<span data-ttu-id="6fa62-131">Gebruik Hallo volgende tooconnect code en laden van gegevens met Hallo **CREATE TABLE** en **INSERT INTO** SQL-instructies.</span><span class="sxs-lookup"><span data-stu-id="6fa62-131">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>
<span data-ttu-id="6fa62-132">Hallo [pg. Client](https://github.com/brianc/node-postgres/wiki/Client) -object is gebruikte toointerface met Hallo PostgreSQL-server.</span><span class="sxs-lookup"><span data-stu-id="6fa62-132">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="6fa62-133">Hallo [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) functie gebruikte tooestablish Hallo verbinding toohello server is.</span><span class="sxs-lookup"><span data-stu-id="6fa62-133">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="6fa62-134">Hallo [pg. Client.query()](https://github.com/brianc/node-postgres/wiki/Query) functie gebruikte tooexecute Hallo SQL-query op PostgreSQL-database is.</span><span class="sxs-lookup"><span data-stu-id="6fa62-134">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="6fa62-135">Vervangen door Hallo host, dbname, gebruiker en wachtwoordparameters Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6fa62-135">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="read-data"></a><span data-ttu-id="6fa62-136">Gegevens lezen</span><span class="sxs-lookup"><span data-stu-id="6fa62-136">Read data</span></span>
<span data-ttu-id="6fa62-137">Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **Selecteer** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="6fa62-137">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="6fa62-138">Hallo [pg. Client](https://github.com/brianc/node-postgres/wiki/Client) -object is gebruikte toointerface met Hallo PostgreSQL-server.</span><span class="sxs-lookup"><span data-stu-id="6fa62-138">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="6fa62-139">Hallo [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) functie gebruikte tooestablish Hallo verbinding toohello server is.</span><span class="sxs-lookup"><span data-stu-id="6fa62-139">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="6fa62-140">Hallo [pg. Client.query()](https://github.com/brianc/node-postgres/wiki/Query) functie gebruikte tooexecute Hallo SQL-query op PostgreSQL-database is.</span><span class="sxs-lookup"><span data-stu-id="6fa62-140">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="6fa62-141">Vervangen door Hallo host, dbname, gebruiker en wachtwoordparameters Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6fa62-141">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="6fa62-142">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="6fa62-142">Update data</span></span>
<span data-ttu-id="6fa62-143">Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **UPDATE** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="6fa62-143">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="6fa62-144">Hallo [pg. Client](https://github.com/brianc/node-postgres/wiki/Client) -object is gebruikte toointerface met Hallo PostgreSQL-server.</span><span class="sxs-lookup"><span data-stu-id="6fa62-144">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="6fa62-145">Hallo [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) functie gebruikte tooestablish Hallo verbinding toohello server is.</span><span class="sxs-lookup"><span data-stu-id="6fa62-145">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="6fa62-146">Hallo [pg. Client.query()](https://github.com/brianc/node-postgres/wiki/Query) functie gebruikte tooexecute Hallo SQL-query op PostgreSQL-database is.</span><span class="sxs-lookup"><span data-stu-id="6fa62-146">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="6fa62-147">Vervangen door Hallo host, dbname, gebruiker en wachtwoordparameters Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6fa62-147">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

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

## <a name="delete-data"></a><span data-ttu-id="6fa62-148">Gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="6fa62-148">Delete data</span></span>
<span data-ttu-id="6fa62-149">Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **verwijderen** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="6fa62-149">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="6fa62-150">Hallo [pg. Client](https://github.com/brianc/node-postgres/wiki/Client) -object is gebruikte toointerface met Hallo PostgreSQL-server.</span><span class="sxs-lookup"><span data-stu-id="6fa62-150">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="6fa62-151">Hallo [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) functie gebruikte tooestablish Hallo verbinding toohello server is.</span><span class="sxs-lookup"><span data-stu-id="6fa62-151">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="6fa62-152">Hallo [pg. Client.query()](https://github.com/brianc/node-postgres/wiki/Query) functie gebruikte tooexecute Hallo SQL-query op PostgreSQL-database is.</span><span class="sxs-lookup"><span data-stu-id="6fa62-152">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="6fa62-153">Vervangen door Hallo host, dbname, gebruiker en wachtwoordparameters Hallo waarden die u hebt opgegeven toen u Hallo-server en database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6fa62-153">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="6fa62-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6fa62-154">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="6fa62-155">Een database migreren met behulp van Exporteren en importeren</span><span class="sxs-lookup"><span data-stu-id="6fa62-155">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
