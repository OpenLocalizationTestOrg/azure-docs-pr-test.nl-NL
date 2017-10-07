---
title: Verbinding maken met Ruby MySQL tooAzure Database | Microsoft Docs
description: Deze snelstartgids vindt u enkele codevoorbeelden van Ruby kunt u een query over gegevens uit Azure-Database voor MySQL en tooconnect gebruiken.
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: ruby
ms.topic: hero-article
ms.date: 07/13/2017
ms.openlocfilehash: ff0880dcc24e96f467c9092bc663ce3dc4c2637a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-ruby-tooconnect-and-query-data"></a>Azure MySQL-Database: gebruik Ruby tooconnect en query-gegevens
Deze snelstartgids demonstreert hoe tooconnect tooan Azure-Database voor het gebruik van MySQL een [Ruby](https://www.ruby-lang.org) toepassing en Hallo [mysql2](https://rubygems.org/gems/mysql2) gem van Windows, Ubuntu Linux en Mac-platforms. Er wordt weergegeven hoe toouse SQL-instructies tooquery invoegen, bijwerken en verwijderen van gegevens in Hallo-database. In dit artikel wordt ervan uitgegaan dat u bekend bent met het ontwikkelen met behulp van Ruby, maar dat u nieuwe tooworking met Azure-Database voor MySQL zijn.

## <a name="prerequisites"></a>Vereisten
Deze snelstartgids Hallo bronnen die zijn gemaakt in een van deze handleidingen als uitgangspunt gebruikt:
- [Een Azure-database voor een MySQL-server maken met behulp van Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Een Azure-database voor een MySQL-server maken met behulp van Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-ruby"></a>Ruby installeren
Ruby, Gem en Hallo MySQL2 bibliotheek installeren op uw computer. 

### <a name="windows"></a>Windows
1. Download en installeer Hallo 2.3 versie van [Ruby](http://rubyinstaller.org/downloads/).
2. Start een nieuwe opdrachtprompt (cmd) vanuit het startmenu Hallo.
3. Wijzig de directory in Hallo Ruby directory voor versie 2.3. `cd c:\Ruby23-x64\bin`
4. Test Hallo Ruby installatie met Hallo opdracht `ruby -v` toosee Hallo versie is geïnstalleerd.
5. Hallo Gem installatie testen met de opdracht Hallo `gem -v` toosee Hallo versie is geïnstalleerd.
6. Hallo Mysql2-module maken voor Ruby Gem door Hallo opdracht uit te voeren met `gem install mysql2`.

### <a name="macos"></a>MacOS
1. Installeren met behulp van Homebrew met Hallo opdracht Ruby `brew install ruby`. Zie voor meer opties voor installatie, Hallo Ruby [documentatie voor de installatie](https://www.ruby-lang.org/en/documentation/installation/#homebrew).
2. Test Hallo Ruby installatie met Hallo opdracht `ruby -v` toosee Hallo versie is geïnstalleerd.
3. Hallo Gem installatie testen met de opdracht Hallo `gem -v` toosee Hallo versie is geïnstalleerd.
4. Hallo Mysql2-module maken voor Ruby Gem door Hallo opdracht uit te voeren met `gem install mysql2`.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. Ruby installeren met de opdracht Hallo `sudo apt-get install ruby-full`. Zie voor meer opties voor installatie, Hallo Ruby [documentatie voor de installatie](https://www.ruby-lang.org/en/documentation/installation/).
2. Test Hallo Ruby installatie met Hallo opdracht `ruby -v` toosee Hallo versie is geïnstalleerd.
3. Hallo meest recente updates installeren voor de Gem met Hallo opdracht `sudo gem update --system`.
4. Hallo Gem installatie testen met de opdracht Hallo `gem -v` toosee Hallo versie is geïnstalleerd.
5. Hallo gcc, type en andere build-hulpprogramma's installeren met de opdracht Hallo `sudo apt-get install build-essential`.
6. Hallo MySQL-ontwikkelbibliotheken met client installeren met de opdracht Hallo `sudo apt-get install libmysqlclient-dev`.
7. Hallo mysql2 module maken voor Ruby Gem door Hallo opdracht uit te voeren met `sudo gem install mysql2`.

## <a name="get-connection-information"></a>Verbindingsgegevens ophalen
Hallo verbinding informatie die nodig is tooconnect toohello Azure Database voor MySQL niet ophalen. U moet Hallo van server volledig gekwalificeerde servernaam en aanmeldingsreferenties.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com/).
2. Hallo links menu in Azure-portal en klik op **alle resources** en zoek naar Hallo-server die u hebt ook, zoals **myserver4demo**.
3. Klik op de servernaam Hallo **myserver4demo**.
4. Selecteer Hallo-server **eigenschappen** pagina. Maak een notitie van Hallo **servernaam** en **aanmeldingsnaam van Server-beheerder**.
 ![Azure Database voor MySQL - Aanmeldgegevens van de serverbeheerder](./media/connect-ruby/1_server-properties-name-login.png)
5. Als u uw aanmeldingsgegevens server bent vergeten, gaat u toohello **overzicht** pagina tooview Hallo Server admin-aanmeldingsnaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo.

## <a name="run-ruby-code"></a>Ruby-code uitvoeren 
1. Hallo Ruby code uit Hallo secties in tekstbestanden te plakken en Hallo bestanden zoals opslaan in een projectmap met bestand extensie .rb, `C:\rubymysql\createtable.rb` of `/home/username/rubymysql/createtable.rb`.
2. toorun hello code, opdrachtregel Hallo starten of bash-shell. Ga naar de projectmap `cd rubymysql`
3. Typ Hallo ruby opdracht gevolgd door Hallo bestandsnaam op, zoals `ruby createtable.rb` toorun Hallo-toepassing.
4. Op Hallo Windows-besturingssysteem, als de toepassing hello ruby zich niet in de omgevingsvariabele path wellicht moet u toouse Hallo volledig pad toolaunch Hallo knooppunttoepassing, zoals`"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`

## <a name="connect-and-create-a-table"></a>Verbinding maken en een tabel maken
Gebruik Hallo volgende tooconnect code en maak een tabel met **CREATE TABLE** SQL-instructie, gevolgd door **INSERT INTO** SQL-instructies tooadd rijen in de tabel Hallo.

Hallo-code wordt een [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new() methode tooconnect tooAzure Database voor MySQL klasse. Vervolgens deze methode roept [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) meerdere keren toorun Hallo neerzetten CREATE TABLE opdrachten, en INSERT INTO. Vervolgens deze methode roept [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose Hallo verbinding voordat het wordt beëindigd.

Vervang Hallo `host`, `database`, `username`, en `password` tekenreeksen door uw eigen waarden. 
```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Drop previous table of same name if one exists
    client.query('DROP TABLE IF EXISTS inventory;')
    puts 'Finished dropping table (if existed).'

    # Drop previous table of same name if one exists.
    client.query('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);')
    puts 'Finished creating table.'

    # Insert some data into table.
    client.query("INSERT INTO inventory VALUES(1, 'banana', 150)")
    client.query("INSERT INTO inventory VALUES(2, 'orange', 154)")
    client.query("INSERT INTO inventory VALUES(3, 'apple', 100)")
    puts 'Inserted 3 rows of data.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="read-data"></a>Gegevens lezen
Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **Selecteer** SQL-instructie. 

Hallo-code wordt een [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new() methode tooconnect tooAzure Database voor MySQL klasse. Vervolgens deze methode roept [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun Hallo SELECT-opdrachten. Vervolgens deze methode roept [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose Hallo verbinding voordat het wordt beëindigd.

Vervang Hallo `host`, `database`, `username`, en `password` tekenreeksen door uw eigen waarden. 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Read data
    resultSet = client.query('SELECT * from inventory;')
    resultSet.each do |row|
        puts 'Data row = (%s, %s, %s)' % [row['id'], row['name'], row['quantity']]
    end
    puts 'Read ' + resultSet.count.to_s + ' row(s).'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="update-data"></a>Gegevens bijwerken
Gebruik Hallo volgende tooconnect code en bij te werken Hallo gegevens met een **bijwerken** SQL-instructie.

Hallo-code wordt een [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new() methode tooconnect tooAzure Database voor MySQL klasse. Vervolgens deze methode roept [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun Hallo bijwerkopdrachten. Vervolgens deze methode roept [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose Hallo verbinding voordat het wordt beëindigd.

Vervang Hallo `host`, `database`, `username`, en `password` tekenreeksen door uw eigen waarden. 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Update data
   client.query('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
   puts 'Updated 1 row of data.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```


## <a name="delete-data"></a>Gegevens verwijderen
Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **verwijderen** SQL-instructie. 

Hallo-code wordt een [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new() methode tooconnect tooAzure Database voor MySQL klasse. Vervolgens deze methode roept [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun Hallo DELETE-opdrachten. Vervolgens deze methode roept [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose Hallo verbinding voordat het wordt beëindigd.

Vervang Hallo `host`, `database`, `username`, en `password` tekenreeksen door uw eigen waarden. 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Delete data
    resultSet = client.query('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="next-steps"></a>Volgende stappen
> [!div class="nextstepaction"]
> [Een database migreren met behulp van Exporteren en importeren](./concepts-migrate-import-export.md)
