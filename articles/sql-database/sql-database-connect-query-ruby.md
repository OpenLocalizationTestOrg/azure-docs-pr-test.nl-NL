---
title: aaaUse Ruby tooquery Azure SQL Database | Microsoft Docs
description: Dit onderwerp leest u hoe toouse Ruby toocreate een programma dat verbinding tooan Azure SQL Database en de query maakt met behulp van Transact-SQL-instructies.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 94fec528-58ba-4352-ba0d-25ae4b273e90
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: hero-article
ms.date: 07/14/2017
ms.author: carlrab
ms.openlocfilehash: 0d4b16b8aacb5e376ab80cbe37569130f2fd52b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-ruby-tooquery-an-azure-sql-database"></a>Ruby tooquery een Azure SQL database gebruiken

Deze zelfstudie laat zien hoe toouse [Ruby](https://www.ruby-lang.org) toocreate een programma tooconnect tooan Azure SQL database en Transact-SQL-instructies tooquery gegevens.

## <a name="prerequisites"></a>Vereisten

toocomplete dit snelle zelfstudie starten, zorg er Hallo volgende vereisten:

- Een Azure SQL-database. Hallo-resources die zijn gemaakt in een van deze snel aan de slag maakt gebruik van deze snel starten: 

   - [Database maken - Portal](sql-database-get-started-portal.md)
   - [Database maken - CLI](sql-database-get-started-cli.md)
   - [Database maken - PowerShell](sql-database-get-started-powershell.md)

- Een [firewallregel op serverniveau](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) voor openbaar IP-adres van de computer Hallo Hallo u gebruiken voor deze zelfstudie voor snel starten.
- U hebt Ruby en verwante software voor uw besturingssysteem geïnstalleerd.
    - **Mac OS**: installeer Homebrew, installeer rbenv en ruby-build, installeer Ruby en installeer vervolgens FreeTDS. Zie [Stap 1.2, 1.3, 1.4 en 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).
    - **Ubuntu**: installeer de vereisten voor Ruby, installeer rbenv en ruby-build, installeer Ruby en installeer vervolgens FreeTDS. Zie [Stap 1.2, 1.3, 1.4 en 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).

## <a name="sql-server-connection-information"></a>SQL Server-verbindingsgegevens

Hallo verbinding informatie die nodig is tooconnect toohello Azure SQL-database worden opgehaald. U moet Hallo volledig gekwalificeerde servernaam, databasenaam en aanmeldingsgegevens in de volgende procedures Hallo.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com/).
2. Selecteer **SQL-Databases** Hallo links menu en klik op de database op Hallo **SQL-databases** pagina. 
3. Op Hallo **overzicht** pagina voor uw database, controleert u de volledig gekwalificeerde servernaam Hallo. U kunt de muisaanwijzer op Hallo server name toobring up Hallo **klikt u op toocopy** optie, zoals wordt weergegeven in Hallo installatiekopie te volgen:

   ![servernaam](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Als u Hallo aanmeldingsgegevens voor uw Azure SQL Database-server bent vergeten, navigeer toohello SQL server pagina tooview Hallo beheerder databaseservernaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo.

> [!IMPORTANT]
> U moet beschikken over een firewallregel voor het openbare IP-adres Hallo van Hallo-computer waarop u deze zelfstudie uitvoert. Als u zich op een andere computer of een ander openbaar IP-adres hebben, maakt u een [serverniveau firewall-regel met Azure-portal Hallo](sql-database-get-started-portal.md#create-a-server-level-firewall-rule). 

## <a name="insert-code-tooquery-sql-database"></a>Code tooquery SQL-database invoegen

1. Maak een nieuw bestand in uw favoriete teksteditor **sqltest.rb**

2. Hallo inhoud vervangen door Hallo volgende code en voeg de juiste waarden Hallo voor uw server, de database, de gebruiker en het wachtwoord.

```ruby
require 'tiny_tds'
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
client = TinyTds::Client.new username: username, password: password, 
    host: server, port: 1433, database: database, azure: true

puts "Reading data from table"
tsql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
        FROM [SalesLT].[ProductCategory] pc
        JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid"
result = client.execute(tsql)
result.each do |row|
    puts row
end
```

## <a name="run-hello-code"></a>Hallo code uitvoeren

1. Voer bij de opdrachtprompt Hallo Hallo opdrachten na:

   ```bash
   ruby sqltest.rb
   ```

2. Verifieer dat Hallo top 20 rijen worden geretourneerd en het venster Hallo-toepassing sluit.


## <a name="next-steps"></a>Volgende stappen
- [Uw eerste Azure SQL-database ontwerpen](sql-database-design-first-database.md)
- [GitHub-opslagplaats voor TinyTDS](https://github.com/rails-sqlserver/tiny_tds)
- [Problemen melden of vragen over TinyTDS stellen](https://github.com/rails-sqlserver/tiny_tds/issues)
- [Ruby-stuurprogramma's voor SQL Server](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/)
