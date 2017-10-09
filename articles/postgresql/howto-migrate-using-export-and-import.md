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
# <a name="migrate-your-postgresql-database-using-export-and-import"></a>Migreer uw PostgreSQL-database met exporteren en importeren
U kunt [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract een PostgreSQL-database in een scriptbestand en [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooimport Hallo gegevens in de doeldatabase Hallo van dat bestand.

## <a name="prerequisites"></a>Vereisten
toostep via deze procedure-tooguide die u nodig:
- Een [Azure-Database voor PostgreSQL server](quickstart-create-server-database-portal.md) met firewall-regels tooallow toegang en database eronder.
- [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) opdrachtregelprogramma geïnstalleerd
- [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) opdrachtregelprogramma geïnstalleerd

Volg deze stappen tooexport en PostgreSQL-database importeren.

## <a name="create-a-script-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a>Een scriptbestand met pg_dump met Hallo gegevens toobe geladen maken
tooexport uw bestaande PostgreSQL lokale database of uit te voeren in een scriptbestand VM tooa sql Hallo-opdracht in uw bestaande omgeving te volgen:
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
Bijvoorbeeld, als er een lokale server en een database met de naam **testdb** erin
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-hello-data-on-target-azure-database-for-postrgesql"></a>Hallo-gegevens op de doel-Azure-Database importeren voor PostrgeSQL
U kunt Hallo psql vanaf de opdrachtregel en Hallo -d,--dbname tooimport Hallo parametergegevens in Azure-Database voor PostrgeSQL we hebben gemaakt en gegevens uit sql-bestand Hallo laden.
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
In dit voorbeeld wordt psql hulpprogramma en een scriptbestand met de naam **testdb.sql** uit de vorige stap tooimport gegevens in de database Hallo **mypgsqldb** op doelserver  **mypgserver 20170401.postgres.database.azure.com**.
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a>Volgende stappen
- toomigrate een PostgreSQL-database met behulp van de dump en herstellen, Zie [Migreer uw PostgreSQL-database met behulp van de dump en terugzetten](howto-migrate-using-dump-and-restore.md)
