---
title: Vanuit Node.js verbinding maken met Azure Database voor PostgreSQL | Microsoft Docs
description: Deze snelstartgids bevat een voorbeeld van Node.js-code die u kunt gebruiken om verbinding te maken met en gegevens op te vragen uit een Azure Database voor PostgreSQL.
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
ms.openlocfilehash: f6c98833c73b70bcf1f8ca53596a34f09807b276
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-nodejs-to-connect-and-query-data"></a><span data-ttu-id="9b88a-103">Azure Database voor PostgreSQL: Node.js gebruiken om verbinding te maken en query's uit te voeren op gegevens</span><span class="sxs-lookup"><span data-stu-id="9b88a-103">Azure Database for PostgreSQL: Use Node.js to connect and query data</span></span>
<span data-ttu-id="9b88a-104">Deze snelstartgids demonstreert hoe u verbinding maken met een Azure-Database voor het gebruik van PostgreSQL [Node.js](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="9b88a-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using [Node.js](https://nodejs.org/).</span></span> <span data-ttu-id="9b88a-105">U ziet hier hoe u SQL-instructies gebruikt om gegevens in de database op te vragen, in te voegen, bij te werken en te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9b88a-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="9b88a-106">In de stappen van dit artikel wordt ervan uitgegaan dat u bekend bent met het ontwikkelen met behulp van Node.js, maar geen ervaring hebt met het werken met Azure Database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="9b88a-106">The steps in this article assume that you are familiar with developing using Node.js, and that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b88a-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9b88a-107">Prerequisites</span></span>
<span data-ttu-id="9b88a-108">In deze snelstartgids worden de resources die in een van deze handleidingen zijn gemaakt, als uitgangspunt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="9b88a-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="9b88a-109">Database maken - Portal</span><span class="sxs-lookup"><span data-stu-id="9b88a-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="9b88a-110">Database maken - CLI</span><span class="sxs-lookup"><span data-stu-id="9b88a-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="9b88a-111">U moet ook het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="9b88a-111">You also need to:</span></span>
- <span data-ttu-id="9b88a-112">[Node.js](https://nodejs.org) installeren</span><span class="sxs-lookup"><span data-stu-id="9b88a-112">Install [Node.js](https://nodejs.org)</span></span>

## <a name="install-pg-client"></a><span data-ttu-id="9b88a-113">pg-client installeren</span><span class="sxs-lookup"><span data-stu-id="9b88a-113">Install pg client</span></span>
<span data-ttu-id="9b88a-114">Installeer [pg](https://www.npmjs.com/package/pg), dit is een PostgreSQL-client voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="9b88a-114">Install [pg](https://www.npmjs.com/package/pg), which is a PostgreSQL client for Node.js.</span></span>

<span data-ttu-id="9b88a-115">Voer de Node Package Manager (NPM) voor JavaScript uit vanaf de opdrachtregel om de pg-client te installeren.</span><span class="sxs-lookup"><span data-stu-id="9b88a-115">To do so, run the node package manager (npm) for JavaScript from your command line to install the pg client.</span></span>
```bash
npm install pg
```

<span data-ttu-id="9b88a-116">Controleer de installatie door de geïnstalleerde pakketten weer te geven.</span><span class="sxs-lookup"><span data-stu-id="9b88a-116">Verify the installation by listing the packages installed.</span></span>
```bash
npm list
```

## <a name="get-connection-information"></a><span data-ttu-id="9b88a-117">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="9b88a-117">Get connection information</span></span>
<span data-ttu-id="9b88a-118">Haal de verbindingsgegevens op die nodig zijn om verbinding te maken met de Azure Database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="9b88a-118">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="9b88a-119">U hebt de volledig gekwalificeerde servernaam en aanmeldingsreferenties nodig.</span><span class="sxs-lookup"><span data-stu-id="9b88a-119">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="9b88a-120">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9b88a-120">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9b88a-121">Klik in het menu links in Azure-portal op **alle resources** en zoek naar de server die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9b88a-121">From the left-hand menu in Azure portal, click **All resources** and search for the server you just created.</span></span>
3. <span data-ttu-id="9b88a-122">Klik op de servernaam.</span><span class="sxs-lookup"><span data-stu-id="9b88a-122">Click the server name.</span></span>
4. <span data-ttu-id="9b88a-123">Selecteer de pagina **Overzicht** van de server.</span><span class="sxs-lookup"><span data-stu-id="9b88a-123">Select the server's **Overview** page.</span></span> <span data-ttu-id="9b88a-124">Noteer de **servernaam** en de **gebruikersnaam van de serverbeheerder**.</span><span class="sxs-lookup"><span data-stu-id="9b88a-124">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="9b88a-125">![Azure Database voor PostgreSQL - Aanmeldgegevens van de serverbeheerder](./media/connect-nodejs/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="9b88a-125">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-nodejs/1-connection-string.png)</span></span>
5. <span data-ttu-id="9b88a-126">Als u uw aanmeldingsgegevens voor de server bent vergeten, gaat u naar de pagina **Overzicht** om de aanmeldingsnaam van de serverbeheerder weer te geven en indien nodig het wachtwoord opnieuw in te stellen.</span><span class="sxs-lookup"><span data-stu-id="9b88a-126">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="running-the-javascript-code-in-nodejs"></a><span data-ttu-id="9b88a-127">De JavaScript-code in Node.js uitvoeren</span><span class="sxs-lookup"><span data-stu-id="9b88a-127">Running the JavaScript code in Node.js</span></span>
<span data-ttu-id="9b88a-128">U kunt Node.js starten vanuit de Bash-shell of opdrachtprompt van Windows door `node` in te voeren. Voer vervolgens de JavaScript-voorbeeldcode interactief uit door deze te kopiëren en in de prompt te plakken.</span><span class="sxs-lookup"><span data-stu-id="9b88a-128">You may launch Node.js from the bash shell or windows command prompt by typing `node`, then run the example JavaScript code interactively by copy and pasting it onto the prompt.</span></span> <span data-ttu-id="9b88a-129">U kunt de JavaScript-code ook in een tekstbestand opslaan en `node filename.js` starten met de bestandsnaam als parameter om de code uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="9b88a-129">Alternatively, you may save the JavaScript code into a text file and launch `node filename.js` with the file name as a parameter to run it.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="9b88a-130">Verbinden, tabel maken en gegevens invoegen</span><span class="sxs-lookup"><span data-stu-id="9b88a-130">Connect, create table, and insert data</span></span>
<span data-ttu-id="9b88a-131">Gebruik de volgende code om verbinding te maken en de gegevens te laden met de SQL-instructies **CREATE TABLE** EN **INSERT INTO**.</span><span class="sxs-lookup"><span data-stu-id="9b88a-131">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>
<span data-ttu-id="9b88a-132">Het object [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) wordt gebruikt voor interactie met de PostgreSQL-server.</span><span class="sxs-lookup"><span data-stu-id="9b88a-132">The [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used to interface with the PostgreSQL server.</span></span> <span data-ttu-id="9b88a-133">De functie [pg.Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) wordt gebruikt om verbinding met de server te maken.</span><span class="sxs-lookup"><span data-stu-id="9b88a-133">The [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used to establish the connection to the server.</span></span> <span data-ttu-id="9b88a-134">De functie [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) wordt gebruikt om de SQL-query uit te voeren op de PostgreSQL-database.</span><span class="sxs-lookup"><span data-stu-id="9b88a-134">The [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used to execute the SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="9b88a-135">Vervang de parameters host, dbname, user en password door de waarden die u hebt opgegeven tijdens het maken van de server en database.</span><span class="sxs-lookup"><span data-stu-id="9b88a-135">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span>

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

## <a name="read-data"></a><span data-ttu-id="9b88a-136">Gegevens lezen</span><span class="sxs-lookup"><span data-stu-id="9b88a-136">Read data</span></span>
<span data-ttu-id="9b88a-137">Gebruik de volgende code om verbinding te maken en de gegevens te lezen met de SQL-instructie **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="9b88a-137">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="9b88a-138">Het object [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) wordt gebruikt voor interactie met de PostgreSQL-server.</span><span class="sxs-lookup"><span data-stu-id="9b88a-138">The [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used to interface with the PostgreSQL server.</span></span> <span data-ttu-id="9b88a-139">De functie [pg.Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) wordt gebruikt om verbinding met de server te maken.</span><span class="sxs-lookup"><span data-stu-id="9b88a-139">The [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used to establish the connection to the server.</span></span> <span data-ttu-id="9b88a-140">De functie [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) wordt gebruikt om de SQL-query uit te voeren op de PostgreSQL-database.</span><span class="sxs-lookup"><span data-stu-id="9b88a-140">The [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used to execute the SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="9b88a-141">Vervang de parameters host, dbname, user en password door de waarden die u hebt opgegeven tijdens het maken van de server en database.</span><span class="sxs-lookup"><span data-stu-id="9b88a-141">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span> 

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
  
    console.log(`Running query to PostgreSQL server: ${config.host}`);

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

## <a name="update-data"></a><span data-ttu-id="9b88a-142">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="9b88a-142">Update data</span></span>
<span data-ttu-id="9b88a-143">Gebruik de volgende code om verbinding te maken en de gegevens te lezen met de SQL-instructie **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="9b88a-143">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="9b88a-144">Het object [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) wordt gebruikt voor interactie met de PostgreSQL-server.</span><span class="sxs-lookup"><span data-stu-id="9b88a-144">The [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used to interface with the PostgreSQL server.</span></span> <span data-ttu-id="9b88a-145">De functie [pg.Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) wordt gebruikt om verbinding met de server te maken.</span><span class="sxs-lookup"><span data-stu-id="9b88a-145">The [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used to establish the connection to the server.</span></span> <span data-ttu-id="9b88a-146">De functie [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) wordt gebruikt om de SQL-query uit te voeren op de PostgreSQL-database.</span><span class="sxs-lookup"><span data-stu-id="9b88a-146">The [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used to execute the SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="9b88a-147">Vervang de parameters host, dbname, user en password door de waarden die u hebt opgegeven tijdens het maken van de server en database.</span><span class="sxs-lookup"><span data-stu-id="9b88a-147">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span> 

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

## <a name="delete-data"></a><span data-ttu-id="9b88a-148">Gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="9b88a-148">Delete data</span></span>
<span data-ttu-id="9b88a-149">Gebruik de volgende code om verbinding te maken en de gegevens te lezen met de SQL-instructie **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="9b88a-149">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="9b88a-150">Het object [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) wordt gebruikt voor interactie met de PostgreSQL-server.</span><span class="sxs-lookup"><span data-stu-id="9b88a-150">The [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used to interface with the PostgreSQL server.</span></span> <span data-ttu-id="9b88a-151">De functie [pg.Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) wordt gebruikt om verbinding met de server te maken.</span><span class="sxs-lookup"><span data-stu-id="9b88a-151">The [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used to establish the connection to the server.</span></span> <span data-ttu-id="9b88a-152">De functie [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) wordt gebruikt om de SQL-query uit te voeren op de PostgreSQL-database.</span><span class="sxs-lookup"><span data-stu-id="9b88a-152">The [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used to execute the SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="9b88a-153">Vervang de parameters host, dbname, user en password door de waarden die u hebt opgegeven tijdens het maken van de server en database.</span><span class="sxs-lookup"><span data-stu-id="9b88a-153">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="9b88a-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9b88a-154">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="9b88a-155">Een database migreren met behulp van Exporteren en importeren</span><span class="sxs-lookup"><span data-stu-id="9b88a-155">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
