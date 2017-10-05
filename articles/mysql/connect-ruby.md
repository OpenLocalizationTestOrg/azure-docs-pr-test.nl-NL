---
title: Via Ruby verbinding maken met Azure Database voor MySQL | Microsoft Docs
description: Deze snelstartgids bevat enkele voorbeelden van Ruby-code die u kunt gebruiken om verbinding te maken met en gegevens op te vragen uit een Azure Database voor MySQL.
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
ms.openlocfilehash: e54f1dccbae060c52f48bfeb277c045b99a91715
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="azure-database-for-mysql-use-ruby-to-connect-and-query-data"></a><span data-ttu-id="33670-103">Azure Database voor MySQL: Ruby gebruiken om verbinding te maken en gegevens op te vragen</span><span class="sxs-lookup"><span data-stu-id="33670-103">Azure Database for MySQL: Use Ruby to connect and query data</span></span>
<span data-ttu-id="33670-104">In deze snelstartgids ziet u hoe u vanuit de platformen Windows, Ubuntu Linux en Mac met behulp van een [Ruby](https://www.ruby-lang.org)-toepassing en de [mysql2](https://rubygems.org/gems/mysql2)-gem verbinding maakt met een Azure Database voor MySQL.</span><span class="sxs-lookup"><span data-stu-id="33670-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a [Ruby](https://www.ruby-lang.org) application and the [mysql2](https://rubygems.org/gems/mysql2) gem from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="33670-105">U ziet hier hoe u SQL-instructies gebruikt om gegevens in de database op te vragen, in te voegen, bij te werken en te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="33670-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="33670-106">In dit artikel wordt ervan uitgegaan dat u bekend bent met ontwikkelen met Ruby, maar geen ervaring hebt met werken met Azure Database voor MySQL.</span><span class="sxs-lookup"><span data-stu-id="33670-106">This article assumes you are familiar with development using Ruby, but that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33670-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="33670-107">Prerequisites</span></span>
<span data-ttu-id="33670-108">In deze snelstartgids worden de resources die in een van deze handleidingen zijn gemaakt, als uitgangspunt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="33670-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="33670-109">Een Azure-database voor een MySQL-server maken met behulp van Azure Portal</span><span class="sxs-lookup"><span data-stu-id="33670-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="33670-110">Een Azure-database voor een MySQL-server maken met behulp van Azure CLI</span><span class="sxs-lookup"><span data-stu-id="33670-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="33670-111">Ruby installeren</span><span class="sxs-lookup"><span data-stu-id="33670-111">Install Ruby</span></span>
<span data-ttu-id="33670-112">Installeer Ruby, Gem en de MySQL2-bibliotheek op uw computer.</span><span class="sxs-lookup"><span data-stu-id="33670-112">Install Ruby, Gem, and the MySQL2 library on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="33670-113">Windows</span><span class="sxs-lookup"><span data-stu-id="33670-113">Windows</span></span>
1. <span data-ttu-id="33670-114">Download en installeer versie 2.3 van [Ruby](http://rubyinstaller.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="33670-114">Download and Install the 2.3 version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
2. <span data-ttu-id="33670-115">Open een nieuw opdrachtprompt (cmd) vanuit het menu Start.</span><span class="sxs-lookup"><span data-stu-id="33670-115">Launch a new command prompt (cmd) from the Start menu.</span></span>
3. <span data-ttu-id="33670-116">Wijzig de map in de Ruby-map voor versie 2.3.</span><span class="sxs-lookup"><span data-stu-id="33670-116">Change directory into the Ruby directory for version 2.3.</span></span> `cd c:\Ruby23-x64\bin`
4. <span data-ttu-id="33670-117">Test de Ruby-installatie door met de opdracht `ruby -v` te controleren welke versie er is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="33670-117">Test the Ruby installation by running the command `ruby -v` to see the version installed.</span></span>
5. <span data-ttu-id="33670-118">Test de Gem-installatie door met de opdracht `gem -v` te controleren welke versie er is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="33670-118">Test the Gem installation by running the command `gem -v` to see the version installed.</span></span>
6. <span data-ttu-id="33670-119">Bouw de MySQL2-module voor Ruby. Gebruik hiervoor Gem en voer de opdracht `gem install mysql2` uit.</span><span class="sxs-lookup"><span data-stu-id="33670-119">Build the Mysql2 module for Ruby using Gem by running the command `gem install mysql2`.</span></span>

### <a name="macos"></a><span data-ttu-id="33670-120">MacOS</span><span class="sxs-lookup"><span data-stu-id="33670-120">MacOS</span></span>
1. <span data-ttu-id="33670-121">Installeer Ruby met Homebrew. Voer daarvoor de opdracht `brew install ruby` uit.</span><span class="sxs-lookup"><span data-stu-id="33670-121">Install Ruby using Homebrew by running the command `brew install ruby`.</span></span> <span data-ttu-id="33670-122">Zie de Ruby-[documentatie voor installatie](https://www.ruby-lang.org/en/documentation/installation/#homebrew) voor meer installatieopties.</span><span class="sxs-lookup"><span data-stu-id="33670-122">For more installation options, see the Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew).</span></span>
2. <span data-ttu-id="33670-123">Test de Ruby-installatie door met de opdracht `ruby -v` te controleren welke versie er is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="33670-123">Test the Ruby installation by running the command `ruby -v` to see the version installed.</span></span>
3. <span data-ttu-id="33670-124">Test de Gem-installatie door met de opdracht `gem -v` te controleren welke versie er is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="33670-124">Test the Gem installation by running the command `gem -v` to see the version installed.</span></span>
4. <span data-ttu-id="33670-125">Bouw de MySQL2-module voor Ruby. Gebruik hiervoor Gem en voer de opdracht `gem install mysql2` uit.</span><span class="sxs-lookup"><span data-stu-id="33670-125">Build the Mysql2 module for Ruby using Gem by running the command `gem install mysql2`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="33670-126">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="33670-126">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="33670-127">Installeer Ruby door de opdracht `sudo apt-get install ruby-full` uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="33670-127">Install Ruby by running the command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="33670-128">Zie de Ruby-[documentatie voor installatie](https://www.ruby-lang.org/en/documentation/installation/) voor meer installatieopties.</span><span class="sxs-lookup"><span data-stu-id="33670-128">For more installation options, see the Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
2. <span data-ttu-id="33670-129">Test de Ruby-installatie door met de opdracht `ruby -v` te controleren welke versie er is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="33670-129">Test the Ruby installation by running the command `ruby -v` to see the version installed.</span></span>
3. <span data-ttu-id="33670-130">Installeer de nieuwste updates voor Gem door de opdracht `sudo gem update --system` uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="33670-130">Install the latest updates for Gem by running the command `sudo gem update --system`.</span></span>
4. <span data-ttu-id="33670-131">Test de Gem-installatie door met de opdracht `gem -v` te controleren welke versie er is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="33670-131">Test the Gem installation by running the command `gem -v` to see the version installed.</span></span>
5. <span data-ttu-id="33670-132">Installeer gcc, make en andere buildhulpprogramma's door de opdracht `sudo apt-get install build-essential` uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="33670-132">Install the gcc, make, and other build tools by running the command `sudo apt-get install build-essential`.</span></span>
6. <span data-ttu-id="33670-133">Installeer de clientontwikkelaarsbibliotheken van MySQL door de opdracht `sudo apt-get install libmysqlclient-dev` uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="33670-133">Install the MySQL client developer libraries by running the command `sudo apt-get install libmysqlclient-dev`.</span></span>
7. <span data-ttu-id="33670-134">Bouw de MySQL2-module voor Ruby. Gebruik hiervoor Gem en voer de opdracht `sudo gem install mysql2` uit.</span><span class="sxs-lookup"><span data-stu-id="33670-134">Build the mysql2 module for Ruby using Gem by running the command `sudo gem install mysql2`.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="33670-135">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="33670-135">Get connection information</span></span>
<span data-ttu-id="33670-136">Haal de verbindingsgegevens op die nodig zijn om verbinding te maken met de Azure Database voor MySQL.</span><span class="sxs-lookup"><span data-stu-id="33670-136">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="33670-137">U hebt de volledig gekwalificeerde servernaam en aanmeldingsreferenties nodig.</span><span class="sxs-lookup"><span data-stu-id="33670-137">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="33670-138">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="33670-138">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="33670-139">Klik in het menu links in Azure Portal op **Alle resources** en zoek de server die u hebt gemaakt (bijvoorbeeld **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="33670-139">From the left-hand menu in Azure portal, click **All resources** and search for the server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="33670-140">Klik op de servernaam **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="33670-140">Click the server name **myserver4demo**.</span></span>
4. <span data-ttu-id="33670-141">Selecteer de pagina **Eigenschappen** van de server.</span><span class="sxs-lookup"><span data-stu-id="33670-141">Select the server's **Properties** page.</span></span> <span data-ttu-id="33670-142">Noteer de **servernaam** en de **gebruikersnaam van de serverbeheerder**.</span><span class="sxs-lookup"><span data-stu-id="33670-142">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="33670-143">![Azure Database voor MySQL - Aanmeldgegevens van de serverbeheerder](./media/connect-ruby/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="33670-143">![Azure Database for MySQL - Server Admin Login](./media/connect-ruby/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="33670-144">Als u uw aanmeldingsgegevens voor de server bent vergeten, gaat u naar de pagina **Overzicht** om de aanmeldingsnaam van de serverbeheerder weer te geven en indien nodig het wachtwoord opnieuw in te stellen.</span><span class="sxs-lookup"><span data-stu-id="33670-144">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="33670-145">Ruby-code uitvoeren</span><span class="sxs-lookup"><span data-stu-id="33670-145">Run Ruby code</span></span> 
1. <span data-ttu-id="33670-146">Plak de Ruby-code uit de onderstaande secties in tekstbestanden en sla de bestanden op in een projectmap met de bestandsextensie .rb, zoals `C:\rubymysql\createtable.rb` of `/home/username/rubymysql/createtable.rb`.</span><span class="sxs-lookup"><span data-stu-id="33670-146">Paste the Ruby code from the sections below into text files, and save the files into a project folder with file extension .rb, such as `C:\rubymysql\createtable.rb` or `/home/username/rubymysql/createtable.rb`.</span></span>
2. <span data-ttu-id="33670-147">Voor het uitvoeren van de code opent u het opdrachtprompt of de bash-shell.</span><span class="sxs-lookup"><span data-stu-id="33670-147">To run the code, launch the command prompt or bash shell.</span></span> <span data-ttu-id="33670-148">Ga naar de projectmap `cd rubymysql`</span><span class="sxs-lookup"><span data-stu-id="33670-148">Change directory into your project folder `cd rubymysql`</span></span>
3. <span data-ttu-id="33670-149">Typ vervolgens de Ruby-opdracht, gevolgd door de bestandsnaam, zoals `ruby createtable.rb`, om de toepassing uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="33670-149">Then type the ruby command followed by the file name, such as `ruby createtable.rb` to run the application.</span></span>
4. <span data-ttu-id="33670-150">Als de Ruby-toepassing zich niet in uw padomgevingsvariabele bevindt, moet u in Windows mogelijk het volledige pad, zoals `"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`, gebruiken om de knooppunttoepassing te starten</span><span class="sxs-lookup"><span data-stu-id="33670-150">On the Windows OS, if the ruby application is not in your path environment variable, you may need to use the full path to launch the node application, such as `"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="33670-151">Verbinding maken en een tabel maken</span><span class="sxs-lookup"><span data-stu-id="33670-151">Connect and create a table</span></span>
<span data-ttu-id="33670-152">Gebruik de volgende code om een tabel te verbinden en te maken met de SQL-instructie **CREATE TABLE**, gevolgd door **INSERT INTO**-instructies om rijen in de tabel toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="33670-152">Use the following code to connect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span></span>

<span data-ttu-id="33670-153">De code gebruikt een [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new()-methode om verbinding te maken met Azure Database voor MySQL.</span><span class="sxs-lookup"><span data-stu-id="33670-153">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="33670-154">Vervolgens wordt de methode [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) meerdere keren aangeroepen om de opdrachten DROP, CREATE TABLE en INSERT INTO uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="33670-154">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) several times to run the DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="33670-155">Vervolgens wordt methode [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) aangeroepen om de verbinding vóór het sluiten te verbreken.</span><span class="sxs-lookup"><span data-stu-id="33670-155">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="33670-156">Vervang de tekenreeksen `host`, `database`, `username` en `password` door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="33670-156">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 
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
    puts 'Successfully created connection to database.'

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

## <a name="read-data"></a><span data-ttu-id="33670-157">Gegevens lezen</span><span class="sxs-lookup"><span data-stu-id="33670-157">Read data</span></span>
<span data-ttu-id="33670-158">Gebruik de volgende code om verbinding te maken en de gegevens te lezen met de SQL-instructie **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="33670-158">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="33670-159">De code gebruikt een [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new()-methode om verbinding te maken met Azure Database voor MySQL.</span><span class="sxs-lookup"><span data-stu-id="33670-159">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="33670-160">Daarna wordt de methode [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) aangeroepen om de SELECT-opdrachten uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="33670-160">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) to run the SELECT commands.</span></span> <span data-ttu-id="33670-161">Vervolgens wordt methode [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) aangeroepen om de verbinding vóór het sluiten te verbreken.</span><span class="sxs-lookup"><span data-stu-id="33670-161">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="33670-162">Vervang de tekenreeksen `host`, `database`, `username` en `password` door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="33670-162">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection to database.'

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

## <a name="update-data"></a><span data-ttu-id="33670-163">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="33670-163">Update data</span></span>
<span data-ttu-id="33670-164">Gebruik de volgende code om verbinding te maken en de gegevens bij te werken met de SQL-instructie **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="33670-164">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="33670-165">De code gebruikt een [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new()-methode om verbinding te maken met Azure Database voor MySQL.</span><span class="sxs-lookup"><span data-stu-id="33670-165">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="33670-166">Daarna wordt de methode [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) aangeroepen om de UPDATE-opdrachten uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="33670-166">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) to run the UPDATE commands.</span></span> <span data-ttu-id="33670-167">Vervolgens wordt methode [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) aangeroepen om de verbinding vóór het sluiten te verbreken.</span><span class="sxs-lookup"><span data-stu-id="33670-167">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="33670-168">Vervang de tekenreeksen `host`, `database`, `username` en `password` door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="33670-168">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection to database.'

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


## <a name="delete-data"></a><span data-ttu-id="33670-169">Gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="33670-169">Delete data</span></span>
<span data-ttu-id="33670-170">Gebruik de volgende code om verbinding te maken en de gegevens te lezen met de SQL-instructie **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="33670-170">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="33670-171">De code gebruikt een [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new()-methode om verbinding te maken met Azure Database voor MySQL.</span><span class="sxs-lookup"><span data-stu-id="33670-171">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="33670-172">Daarna wordt de methode [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) aangeroepen om de DELETE-opdrachten uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="33670-172">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) to run the DELETE commands.</span></span> <span data-ttu-id="33670-173">Vervolgens wordt methode [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) aangeroepen om de verbinding vóór het sluiten te verbreken.</span><span class="sxs-lookup"><span data-stu-id="33670-173">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="33670-174">Vervang de tekenreeksen `host`, `database`, `username` en `password` door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="33670-174">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection to database.'

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

## <a name="next-steps"></a><span data-ttu-id="33670-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="33670-175">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="33670-176">Een database migreren met behulp van Exporteren en importeren</span><span class="sxs-lookup"><span data-stu-id="33670-176">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
