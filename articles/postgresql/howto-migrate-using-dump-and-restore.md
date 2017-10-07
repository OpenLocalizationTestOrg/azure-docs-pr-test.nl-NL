---
title: aaaHow tooDump en herstel in de Azure-Database voor PostgreSQL | Microsoft Docs
description: Beschrijft hoe tooextract een PostgreSQL-database in een dumpbestand en terugzetten Hallo PostgreSQL-database uit een archiefbestand voor PostgreSQL door pg_dump in Azure-Database gemaakt.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 9ad28e9dec3927b0f80b5e6bab6423cc944f5156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-postgresql-database-using-dump-and-restore"></a><span data-ttu-id="e2feb-103">Migreer uw PostgreSQL-database met behulp van de dump en terugzetten</span><span class="sxs-lookup"><span data-stu-id="e2feb-103">Migrate your PostgreSQL database using dump and restore</span></span>
<span data-ttu-id="e2feb-104">U kunt [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract een PostgreSQL-database in een dumpbestand en [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) toorestore hello PostgreSQL-database uit een archiefbestand gemaakt door pg_dump.</span><span class="sxs-lookup"><span data-stu-id="e2feb-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract a PostgreSQL database into a dump file and [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) toorestore hello PostgreSQL database from an archive file created by pg_dump.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2feb-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e2feb-105">Prerequisites</span></span>
<span data-ttu-id="e2feb-106">toostep via deze procedure-tooguide die u nodig:</span><span class="sxs-lookup"><span data-stu-id="e2feb-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="e2feb-107">Een [Azure-Database voor PostgreSQL server](quickstart-create-server-database-portal.md) met firewall-regels tooallow toegang en database eronder.</span><span class="sxs-lookup"><span data-stu-id="e2feb-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules tooallow access and database under it.</span></span>
- <span data-ttu-id="e2feb-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) en [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) opdrachtregelprogramma's geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="e2feb-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) and [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) command-line utilities installed</span></span>

<span data-ttu-id="e2feb-109">Volg deze stappen toodump en uw PostgreSQL-database terugzetten:</span><span class="sxs-lookup"><span data-stu-id="e2feb-109">Follow these steps toodump and restore your PostgreSQL database:</span></span>

## <a name="create-a-dump-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a><span data-ttu-id="e2feb-110">Maken van een bestand met pg_dump Hallo gegevens toobe geladen met</span><span class="sxs-lookup"><span data-stu-id="e2feb-110">Create a dump file using pg_dump that contains hello data toobe loaded</span></span>
<span data-ttu-id="e2feb-111">tooback van een bestaande PostgreSQL lokale database of in een VM uitvoeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="e2feb-111">tooback up an existing PostgreSQL database on-premises or in a VM, run hello following command:</span></span>
```bash
pg_dump -Fc -v --host=<host> --username=<name> --dbname=<database name> > <database>.dump
```
<span data-ttu-id="e2feb-112">Bijvoorbeeld, als er een lokale server en een database met de naam **testdb** erin</span><span class="sxs-lookup"><span data-stu-id="e2feb-112">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump -Fc -v --host=localhost --username=masterlogin --dbname=testdb > testdb.dump
```

## <a name="restore-hello-data-into-hello-target-azure-database-for-postrgesql-using-pgrestore"></a><span data-ttu-id="e2feb-113">Hallo-gegevens herstellen op Hallo doel-Azure-Database voor PostrgeSQL met pg_restore</span><span class="sxs-lookup"><span data-stu-id="e2feb-113">Restore hello data into hello target Azure Database for PostrgeSQL using pg_restore</span></span>
<span data-ttu-id="e2feb-114">Nadat u de doeldatabase Hallo hebt gemaakt, kunt u Hallo pg_restore opdracht en Hallo -d,--dbname parameter toorestore Hallo gegevens in de doeldatabase Hallo van het dumpbestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="e2feb-114">Once you have created hello target database, you can use hello pg_restore command and hello -d, --dbname parameter toorestore hello data into hello target database from hello dump file.</span></span>
```bash
pg_restore -v –-host=<server name> --port=<port> --username=<user@servername> --dbname=<target database name> <database>.dump
```
<span data-ttu-id="e2feb-115">In dit voorbeeld kunt u Hallo gegevens terugzetten van het dumpbestand Hallo **testdb.dump** in Hallo database **mypgsqldb** op doelserver **mypgserver-20170401.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="e2feb-115">In this example, restore hello data from hello dump file **testdb.dump** into hello database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
pg_restore -v --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb testdb.dump
```

## <a name="next-steps"></a><span data-ttu-id="e2feb-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e2feb-116">Next steps</span></span>
- <span data-ttu-id="e2feb-117">toomigrate een PostgreSQL-database met behulp van exporteren en importeren, Zie [Migreer uw PostgreSQL-database met exporteren en importeren](howto-migrate-using-export-and-import.md)</span><span class="sxs-lookup"><span data-stu-id="e2feb-117">toomigrate a PostgreSQL database using export and import, see [Migrate your PostgreSQL database using export and import](howto-migrate-using-export-and-import.md)</span></span>
