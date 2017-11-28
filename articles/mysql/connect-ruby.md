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
# <a name="azure-database-for-mysql-use-ruby-tooconnect-and-query-data"></a><span data-ttu-id="4696c-103">Azure MySQL-Database: gebruik Ruby tooconnect en query-gegevens</span><span class="sxs-lookup"><span data-stu-id="4696c-103">Azure Database for MySQL: Use Ruby tooconnect and query data</span></span>
<span data-ttu-id="4696c-104">Deze snelstartgids demonstreert hoe tooconnect tooan Azure-Database voor het gebruik van MySQL een [Ruby](https://www.ruby-lang.org) toepassing en Hallo [mysql2](https://rubygems.org/gems/mysql2) gem van Windows, Ubuntu Linux en Mac-platforms.</span><span class="sxs-lookup"><span data-stu-id="4696c-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a [Ruby](https://www.ruby-lang.org) application and hello [mysql2](https://rubygems.org/gems/mysql2) gem from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="4696c-105">Er wordt weergegeven hoe toouse SQL-instructies tooquery invoegen, bijwerken en verwijderen van gegevens in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="4696c-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="4696c-106">In dit artikel wordt ervan uitgegaan dat u bekend bent met het ontwikkelen met behulp van Ruby, maar dat u nieuwe tooworking met Azure-Database voor MySQL zijn.</span><span class="sxs-lookup"><span data-stu-id="4696c-106">This article assumes you are familiar with development using Ruby, but that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4696c-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4696c-107">Prerequisites</span></span>
<span data-ttu-id="4696c-108">Deze snelstartgids Hallo bronnen die zijn gemaakt in een van deze handleidingen als uitgangspunt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="4696c-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="4696c-109">Een Azure-database voor een MySQL-server maken met behulp van Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4696c-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="4696c-110">Een Azure-database voor een MySQL-server maken met behulp van Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4696c-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="4696c-111">Ruby installeren</span><span class="sxs-lookup"><span data-stu-id="4696c-111">Install Ruby</span></span>
<span data-ttu-id="4696c-112">Ruby, Gem en Hallo MySQL2 bibliotheek installeren op uw computer.</span><span class="sxs-lookup"><span data-stu-id="4696c-112">Install Ruby, Gem, and hello MySQL2 library on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="4696c-113">Windows</span><span class="sxs-lookup"><span data-stu-id="4696c-113">Windows</span></span>
1. <span data-ttu-id="4696c-114">Download en installeer Hallo 2.3 versie van [Ruby](http://rubyinstaller.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="4696c-114">Download and Install hello 2.3 version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
2. <span data-ttu-id="4696c-115">Start een nieuwe opdrachtprompt (cmd) vanuit het startmenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="4696c-115">Launch a new command prompt (cmd) from hello Start menu.</span></span>
3. <span data-ttu-id="4696c-116">Wijzig de directory in Hallo Ruby directory voor versie 2.3.</span><span class="sxs-lookup"><span data-stu-id="4696c-116">Change directory into hello Ruby directory for version 2.3.</span></span> `cd c:\Ruby23-x64\bin`
4. <span data-ttu-id="4696c-117">Test Hallo Ruby installatie met Hallo opdracht `ruby -v` toosee Hallo versie is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="4696c-117">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
5. <span data-ttu-id="4696c-118">Hallo Gem installatie testen met de opdracht Hallo `gem -v` toosee Hallo versie is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="4696c-118">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
6. <span data-ttu-id="4696c-119">Hallo Mysql2-module maken voor Ruby Gem door Hallo opdracht uit te voeren met `gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="4696c-119">Build hello Mysql2 module for Ruby using Gem by running hello command `gem install mysql2`.</span></span>

### <a name="macos"></a><span data-ttu-id="4696c-120">MacOS</span><span class="sxs-lookup"><span data-stu-id="4696c-120">MacOS</span></span>
1. <span data-ttu-id="4696c-121">Installeren met behulp van Homebrew met Hallo opdracht Ruby `brew install ruby`.</span><span class="sxs-lookup"><span data-stu-id="4696c-121">Install Ruby using Homebrew by running hello command `brew install ruby`.</span></span> <span data-ttu-id="4696c-122">Zie voor meer opties voor installatie, Hallo Ruby [documentatie voor de installatie](https://www.ruby-lang.org/en/documentation/installation/#homebrew).</span><span class="sxs-lookup"><span data-stu-id="4696c-122">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew).</span></span>
2. <span data-ttu-id="4696c-123">Test Hallo Ruby installatie met Hallo opdracht `ruby -v` toosee Hallo versie is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="4696c-123">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
3. <span data-ttu-id="4696c-124">Hallo Gem installatie testen met de opdracht Hallo `gem -v` toosee Hallo versie is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="4696c-124">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
4. <span data-ttu-id="4696c-125">Hallo Mysql2-module maken voor Ruby Gem door Hallo opdracht uit te voeren met `gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="4696c-125">Build hello Mysql2 module for Ruby using Gem by running hello command `gem install mysql2`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="4696c-126">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="4696c-126">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="4696c-127">Ruby installeren met de opdracht Hallo `sudo apt-get install ruby-full`.</span><span class="sxs-lookup"><span data-stu-id="4696c-127">Install Ruby by running hello command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="4696c-128">Zie voor meer opties voor installatie, Hallo Ruby [documentatie voor de installatie](https://www.ruby-lang.org/en/documentation/installation/).</span><span class="sxs-lookup"><span data-stu-id="4696c-128">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
2. <span data-ttu-id="4696c-129">Test Hallo Ruby installatie met Hallo opdracht `ruby -v` toosee Hallo versie is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="4696c-129">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
3. <span data-ttu-id="4696c-130">Hallo meest recente updates installeren voor de Gem met Hallo opdracht `sudo gem update --system`.</span><span class="sxs-lookup"><span data-stu-id="4696c-130">Install hello latest updates for Gem by running hello command `sudo gem update --system`.</span></span>
4. <span data-ttu-id="4696c-131">Hallo Gem installatie testen met de opdracht Hallo `gem -v` toosee Hallo versie is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="4696c-131">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
5. <span data-ttu-id="4696c-132">Hallo gcc, type en andere build-hulpprogramma's installeren met de opdracht Hallo `sudo apt-get install build-essential`.</span><span class="sxs-lookup"><span data-stu-id="4696c-132">Install hello gcc, make, and other build tools by running hello command `sudo apt-get install build-essential`.</span></span>
6. <span data-ttu-id="4696c-133">Hallo MySQL-ontwikkelbibliotheken met client installeren met de opdracht Hallo `sudo apt-get install libmysqlclient-dev`.</span><span class="sxs-lookup"><span data-stu-id="4696c-133">Install hello MySQL client developer libraries by running hello command `sudo apt-get install libmysqlclient-dev`.</span></span>
7. <span data-ttu-id="4696c-134">Hallo mysql2 module maken voor Ruby Gem door Hallo opdracht uit te voeren met `sudo gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="4696c-134">Build hello mysql2 module for Ruby using Gem by running hello command `sudo gem install mysql2`.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="4696c-135">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="4696c-135">Get connection information</span></span>
<span data-ttu-id="4696c-136">Hallo verbinding informatie die nodig is tooconnect toohello Azure Database voor MySQL niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="4696c-136">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="4696c-137">U moet Hallo van server volledig gekwalificeerde servernaam en aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="4696c-137">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="4696c-138">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4696c-138">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4696c-139">Hallo links menu in Azure-portal en klik op **alle resources** en zoek naar Hallo-server die u hebt ook, zoals **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="4696c-139">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="4696c-140">Klik op de servernaam Hallo **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="4696c-140">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="4696c-141">Selecteer Hallo-server **eigenschappen** pagina.</span><span class="sxs-lookup"><span data-stu-id="4696c-141">Select hello server's **Properties** page.</span></span> <span data-ttu-id="4696c-142">Maak een notitie van Hallo **servernaam** en **aanmeldingsnaam van Server-beheerder**.</span><span class="sxs-lookup"><span data-stu-id="4696c-142">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="4696c-143">![Azure Database voor MySQL - Aanmeldgegevens van de serverbeheerder](./media/connect-ruby/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="4696c-143">![Azure Database for MySQL - Server Admin Login](./media/connect-ruby/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="4696c-144">Als u uw aanmeldingsgegevens server bent vergeten, gaat u toohello **overzicht** pagina tooview Hallo Server admin-aanmeldingsnaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="4696c-144">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="4696c-145">Ruby-code uitvoeren</span><span class="sxs-lookup"><span data-stu-id="4696c-145">Run Ruby code</span></span> 
1. <span data-ttu-id="4696c-146">Hallo Ruby code uit Hallo secties in tekstbestanden te plakken en Hallo bestanden zoals opslaan in een projectmap met bestand extensie .rb, `C:\rubymysql\createtable.rb` of `/home/username/rubymysql/createtable.rb`.</span><span class="sxs-lookup"><span data-stu-id="4696c-146">Paste hello Ruby code from hello sections below into text files, and save hello files into a project folder with file extension .rb, such as `C:\rubymysql\createtable.rb` or `/home/username/rubymysql/createtable.rb`.</span></span>
2. <span data-ttu-id="4696c-147">toorun hello code, opdrachtregel Hallo starten of bash-shell.</span><span class="sxs-lookup"><span data-stu-id="4696c-147">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="4696c-148">Ga naar de projectmap `cd rubymysql`</span><span class="sxs-lookup"><span data-stu-id="4696c-148">Change directory into your project folder `cd rubymysql`</span></span>
3. <span data-ttu-id="4696c-149">Typ Hallo ruby opdracht gevolgd door Hallo bestandsnaam op, zoals `ruby createtable.rb` toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="4696c-149">Then type hello ruby command followed by hello file name, such as `ruby createtable.rb` toorun hello application.</span></span>
4. <span data-ttu-id="4696c-150">Op Hallo Windows-besturingssysteem, als de toepassing hello ruby zich niet in de omgevingsvariabele path wellicht moet u toouse Hallo volledig pad toolaunch Hallo knooppunttoepassing, zoals`"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span><span class="sxs-lookup"><span data-stu-id="4696c-150">On hello Windows OS, if hello ruby application is not in your path environment variable, you may need toouse hello full path toolaunch hello node application, such as `"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="4696c-151">Verbinding maken en een tabel maken</span><span class="sxs-lookup"><span data-stu-id="4696c-151">Connect and create a table</span></span>
<span data-ttu-id="4696c-152">Gebruik Hallo volgende tooconnect code en maak een tabel met **CREATE TABLE** SQL-instructie, gevolgd door **INSERT INTO** SQL-instructies tooadd rijen in de tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="4696c-152">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="4696c-153">Hallo-code wordt een [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new() methode tooconnect tooAzure Database voor MySQL klasse.</span><span class="sxs-lookup"><span data-stu-id="4696c-153">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="4696c-154">Vervolgens deze methode roept [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) meerdere keren toorun Hallo neerzetten CREATE TABLE opdrachten, en INSERT INTO.</span><span class="sxs-lookup"><span data-stu-id="4696c-154">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) several times toorun hello DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="4696c-155">Vervolgens deze methode roept [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose Hallo verbinding voordat het wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="4696c-155">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="4696c-156">Vervang Hallo `host`, `database`, `username`, en `password` tekenreeksen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="4696c-156">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 
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

## <a name="read-data"></a><span data-ttu-id="4696c-157">Gegevens lezen</span><span class="sxs-lookup"><span data-stu-id="4696c-157">Read data</span></span>
<span data-ttu-id="4696c-158">Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **Selecteer** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="4696c-158">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="4696c-159">Hallo-code wordt een [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new() methode tooconnect tooAzure Database voor MySQL klasse.</span><span class="sxs-lookup"><span data-stu-id="4696c-159">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="4696c-160">Vervolgens deze methode roept [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun Hallo SELECT-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="4696c-160">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello SELECT commands.</span></span> <span data-ttu-id="4696c-161">Vervolgens deze methode roept [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose Hallo verbinding voordat het wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="4696c-161">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="4696c-162">Vervang Hallo `host`, `database`, `username`, en `password` tekenreeksen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="4696c-162">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="4696c-163">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="4696c-163">Update data</span></span>
<span data-ttu-id="4696c-164">Gebruik Hallo volgende tooconnect code en bij te werken Hallo gegevens met een **bijwerken** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="4696c-164">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="4696c-165">Hallo-code wordt een [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new() methode tooconnect tooAzure Database voor MySQL klasse.</span><span class="sxs-lookup"><span data-stu-id="4696c-165">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="4696c-166">Vervolgens deze methode roept [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun Hallo bijwerkopdrachten.</span><span class="sxs-lookup"><span data-stu-id="4696c-166">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello UPDATE commands.</span></span> <span data-ttu-id="4696c-167">Vervolgens deze methode roept [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose Hallo verbinding voordat het wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="4696c-167">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="4696c-168">Vervang Hallo `host`, `database`, `username`, en `password` tekenreeksen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="4696c-168">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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


## <a name="delete-data"></a><span data-ttu-id="4696c-169">Gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="4696c-169">Delete data</span></span>
<span data-ttu-id="4696c-170">Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **verwijderen** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="4696c-170">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="4696c-171">Hallo-code wordt een [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new() methode tooconnect tooAzure Database voor MySQL klasse.</span><span class="sxs-lookup"><span data-stu-id="4696c-171">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="4696c-172">Vervolgens deze methode roept [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun Hallo DELETE-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="4696c-172">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello DELETE commands.</span></span> <span data-ttu-id="4696c-173">Vervolgens deze methode roept [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose Hallo verbinding voordat het wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="4696c-173">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="4696c-174">Vervang Hallo `host`, `database`, `username`, en `password` tekenreeksen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="4696c-174">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="4696c-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4696c-175">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="4696c-176">Een database migreren met behulp van Exporteren en importeren</span><span class="sxs-lookup"><span data-stu-id="4696c-176">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
