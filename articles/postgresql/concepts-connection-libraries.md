---
title: Verbindingsbibliotheken voor Azure-Database voor PostgreSQL | Microsoft Docs
description: In dit artikel beschrijft de verschillende bibliotheken en stuurprogramma's die ontwikkelaars wanneer gebruiken kunnen toepassingen verbinding maken en query uitvoeren op Azure-Database voor PostgreSQL coderen.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/15/2017
ms.openlocfilehash: 1f99ef7fefb1ff9d35f564a1f0ad77c8dd64659e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="connection-libraries-for-azure-database-for-postgresql"></a>Verbindingsbibliotheken voor Azure-Database voor PostgreSQL
Dit onderwerp worden de bibliotheken en stuurprogramma's voor gebruik door ontwikkelaars voor het programmeren van toepassingen kunnen verbinding maken en query uitvoeren op Azure-Database voor PostgreSQL.

## <a name="client-interfaces"></a>Clientinterfaces
De meeste taal clientbibliotheken verbinding maken met server PostgreSQL externe projecten zijn en onafhankelijk van elkaar worden gedistribueerd. Deze worden ondersteund op Windows, Linux en Mac-platforms. Sommige van de populaire clientstuurprogramma's worden vermeld:

| **Taal** | **Client-interface** | **Aanvullende informatie** | **Downloaden** |
|--------------|----------------------------------------------------------------|-------------------------------------|--------------------------------------------------------------------|
| Python | [psycopg](http://initd.org/psycopg/) | API voor DB 2.0-compatibel | [Downloaden](http://initd.org/psycopg/download/) |
| PHP | [PHP-pgsql](https://php.net/manual/en/book.pgsql.php) | Database-uitbreiding | [Installeren](https://secure.php.net/manual/en/pgsql.installation.php) |
| Node.js | [PG npm-pakket](https://www.npmjs.com/package/pg) | Niet-blokkerende client pure JavaScript | [Installeren](https://www.npmjs.com/package/pg) |
| Java | [JDBC](http://jdbc.postgresql.org/) | Type 4 JDBC-stuurprogramma | [Downloaden](https://jdbc.postgresql.org/download.html)  |
| Ruby | [PG gem](https://deveiate.org/code/pg/) | Ruby-Interface | [Downloaden](https://rubygems.org/downloads/pg-0.20.0.gem) |
| Aan de slag | [Pq pakket](https://godoc.org/github.com/lib/pq) | Pure Ga postgres stuurprogramma | [Installeren](https://github.com/lib/pq/blob/master/README.md) |
| C\#/ .NET | [Npgsql](http://www.npgsql.org/) | ADO.NET Data Provider | [Downloaden](https://www.microsoft.com/net/) |
| ODBC | [psqlODBC](https://odbc.postgresql.org/) | ODBC-stuurprogramma | [Downloaden](http://www.postgresql.org/ftp/odbc/versions/) |
| C | [libpq](https://www.postgresql.org/docs/9.6/static/libpq.html) | Primaire C taal interface | Inbegrepen |
| C++ | [libpqxx](http://pqxx.org/) | Nieuwe stijl C++-interface | [Downloaden](http://pqxx.org/download/software/) |

## <a name="next-steps"></a>Volgende stappen
Lees deze snelstartgidsen op verbinding maken met en Azure Database doorzoeken op PostgreSQL met behulp van de taal van uw keuze:

[Python](./connect-python.md) | [Node.JS](./connect-nodejs.md) | [.NET (C#)](./connect-csharp.md)
