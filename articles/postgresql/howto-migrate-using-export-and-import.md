---
title: aaaMigrate een database met importeren en exporteren in Azure-Database voor PostgreSQL | Microsoft Docs
description: Beschrijft hoe een PostgreSQL-database in een scriptbestand en Hallo gegevens importeren in de doeldatabase Hallo van dat bestand.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 5ca4650782b02e1067c5a8a3710f2dfbc8c76063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-postgresql-database-using-export-and-import"></a><span data-ttu-id="1b537-103">Migreer uw PostgreSQL-database met exporteren en importeren</span><span class="sxs-lookup"><span data-stu-id="1b537-103">Migrate your PostgreSQL database using export and import</span></span>
<span data-ttu-id="1b537-104">U kunt [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract een PostgreSQL-database in een scriptbestand en [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooimport Hallo gegevens in de doeldatabase Hallo van dat bestand.</span><span class="sxs-lookup"><span data-stu-id="1b537-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract a PostgreSQL database into a script file and [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooimport hello data into hello target database from that file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b537-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1b537-105">Prerequisites</span></span>
<span data-ttu-id="1b537-106">toostep via deze procedure-tooguide die u nodig:</span><span class="sxs-lookup"><span data-stu-id="1b537-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="1b537-107">Een [Azure-Database voor PostgreSQL server](quickstart-create-server-database-portal.md) met firewall-regels tooallow toegang en database eronder.</span><span class="sxs-lookup"><span data-stu-id="1b537-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules tooallow access and database under it.</span></span>
- <span data-ttu-id="1b537-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) opdrachtregelprogramma geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="1b537-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) command-line utility installed</span></span>
- <span data-ttu-id="1b537-109">[psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) opdrachtregelprogramma geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="1b537-109">[psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) command-line utility installed</span></span>

<span data-ttu-id="1b537-110">Volg deze stappen tooexport en PostgreSQL-database importeren.</span><span class="sxs-lookup"><span data-stu-id="1b537-110">Follow these steps tooexport and import your PostgreSQL database.</span></span>

## <a name="create-a-script-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a><span data-ttu-id="1b537-111">Een scriptbestand met pg_dump met Hallo gegevens toobe geladen maken</span><span class="sxs-lookup"><span data-stu-id="1b537-111">Create a script file using pg_dump that contains hello data toobe loaded</span></span>
<span data-ttu-id="1b537-112">tooexport uw bestaande PostgreSQL lokale database of uit te voeren in een scriptbestand VM tooa sql Hallo-opdracht in uw bestaande omgeving te volgen:</span><span class="sxs-lookup"><span data-stu-id="1b537-112">tooexport your existing PostgreSQL database on-premises or in a VM tooa sql script file, run hello following command in your existing environment:</span></span>
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
<span data-ttu-id="1b537-113">Bijvoorbeeld, als er een lokale server en een database met de naam **testdb** erin</span><span class="sxs-lookup"><span data-stu-id="1b537-113">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-hello-data-on-target-azure-database-for-postrgesql"></a><span data-ttu-id="1b537-114">Hallo-gegevens op de doel-Azure-Database importeren voor PostrgeSQL</span><span class="sxs-lookup"><span data-stu-id="1b537-114">Import hello data on target Azure Database for PostrgeSQL</span></span>
<span data-ttu-id="1b537-115">U kunt Hallo psql vanaf de opdrachtregel en Hallo -d,--dbname tooimport Hallo parametergegevens in Azure-Database voor PostrgeSQL we hebben gemaakt en gegevens uit sql-bestand Hallo laden.</span><span class="sxs-lookup"><span data-stu-id="1b537-115">You can use hello psql command line and hello -d, --dbname parameter tooimport hello data into Azure Database for PostrgeSQL we created and load data from hello sql file.</span></span>
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
<span data-ttu-id="1b537-116">In dit voorbeeld wordt psql hulpprogramma en een scriptbestand met de naam **testdb.sql** uit de vorige stap tooimport gegevens in de database Hallo **mypgsqldb** op doelserver  **mypgserver 20170401.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="1b537-116">This example uses psql utility and a script file named **testdb.sql** from previous step tooimport data into hello database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a><span data-ttu-id="1b537-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1b537-117">Next steps</span></span>
- <span data-ttu-id="1b537-118">toomigrate een PostgreSQL-database met behulp van de dump en herstellen, Zie [Migreer uw PostgreSQL-database met behulp van de dump en terugzetten](howto-migrate-using-dump-and-restore.md)</span><span class="sxs-lookup"><span data-stu-id="1b537-118">toomigrate a PostgreSQL database using dump and restore, see [Migrate your PostgreSQL database using dump and restore](howto-migrate-using-dump-and-restore.md)</span></span>
