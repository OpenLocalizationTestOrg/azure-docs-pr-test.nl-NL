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
# <a name="migrate-your-postgresql-database-using-dump-and-restore"></a>Migreer uw PostgreSQL-database met behulp van de dump en terugzetten
U kunt [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract een PostgreSQL-database in een dumpbestand en [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) toorestore hello PostgreSQL-database uit een archiefbestand gemaakt door pg_dump.

## <a name="prerequisites"></a>Vereisten
toostep via deze procedure-tooguide die u nodig:
- Een [Azure-Database voor PostgreSQL server](quickstart-create-server-database-portal.md) met firewall-regels tooallow toegang en database eronder.
- [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) en [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) opdrachtregelprogramma's geïnstalleerd

Volg deze stappen toodump en uw PostgreSQL-database terugzetten:

## <a name="create-a-dump-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a>Maken van een bestand met pg_dump Hallo gegevens toobe geladen met
tooback van een bestaande PostgreSQL lokale database of in een VM uitvoeren Hallo volgende opdracht:
```bash
pg_dump -Fc -v --host=<host> --username=<name> --dbname=<database name> > <database>.dump
```
Bijvoorbeeld, als er een lokale server en een database met de naam **testdb** erin
```bash
pg_dump -Fc -v --host=localhost --username=masterlogin --dbname=testdb > testdb.dump
```

## <a name="restore-hello-data-into-hello-target-azure-database-for-postrgesql-using-pgrestore"></a>Hallo-gegevens herstellen op Hallo doel-Azure-Database voor PostrgeSQL met pg_restore
Nadat u de doeldatabase Hallo hebt gemaakt, kunt u Hallo pg_restore opdracht en Hallo -d,--dbname parameter toorestore Hallo gegevens in de doeldatabase Hallo van het dumpbestand Hallo.
```bash
pg_restore -v –-host=<server name> --port=<port> --username=<user@servername> --dbname=<target database name> <database>.dump
```
In dit voorbeeld kunt u Hallo gegevens terugzetten van het dumpbestand Hallo **testdb.dump** in Hallo database **mypgsqldb** op doelserver **mypgserver-20170401.postgres.database.azure.com**.
```bash
pg_restore -v --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb testdb.dump
```

## <a name="next-steps"></a>Volgende stappen
- toomigrate een PostgreSQL-database met behulp van exporteren en importeren, Zie [Migreer uw PostgreSQL-database met exporteren en importeren](howto-migrate-using-export-and-import.md)
