---
title: aaaConnect tooAzure Database voor Ruby met PostgreSQL | Microsoft Docs
description: Deze snelstartgids bevat een Ruby codevoorbeeld kunt u een query over gegevens uit Azure-Database voor PostgreSQL en tooconnect gebruiken.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: ruby
ms.topic: quickstart
ms.date: 06/30/2017
ms.openlocfilehash: 7a0c8c92023452b40ca19d76fa659744f3e9a236
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-ruby-tooconnect-and-query-data"></a><span data-ttu-id="54254-103">Azure-Database voor PostgreSQL: gebruik Ruby tooconnect en query-gegevens</span><span class="sxs-lookup"><span data-stu-id="54254-103">Azure Database for PostgreSQL: Use Ruby tooconnect and query data</span></span>
<span data-ttu-id="54254-104">Deze snelstartgids demonstreert hoe tooconnect tooan Azure-Database voor het gebruik van PostgreSQL een [Ruby](https://www.ruby-lang.org) toepassing.</span><span class="sxs-lookup"><span data-stu-id="54254-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a [Ruby](https://www.ruby-lang.org) application.</span></span> <span data-ttu-id="54254-105">Er wordt weergegeven hoe toouse SQL-instructies tooquery invoegen, bijwerken en verwijderen van gegevens in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="54254-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="54254-106">In dit artikel wordt ervan uitgegaan dat u bekend bent met het ontwikkelen met behulp van Ruby, maar dat u nieuwe tooworking met Azure-Database voor PostgreSQL zijn.</span><span class="sxs-lookup"><span data-stu-id="54254-106">This article assumes you are familiar with development using Ruby, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54254-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="54254-107">Prerequisites</span></span>
<span data-ttu-id="54254-108">Deze snelstartgids Hallo bronnen die zijn gemaakt in een van deze handleidingen als uitgangspunt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="54254-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="54254-109">Database maken - Portal</span><span class="sxs-lookup"><span data-stu-id="54254-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="54254-110">Database maken - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="54254-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="54254-111">Ruby installeren</span><span class="sxs-lookup"><span data-stu-id="54254-111">Install Ruby</span></span>
<span data-ttu-id="54254-112">Installeer Ruby op uw eigen machine.</span><span class="sxs-lookup"><span data-stu-id="54254-112">Install Ruby on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="54254-113">Windows</span><span class="sxs-lookup"><span data-stu-id="54254-113">Windows</span></span>
- <span data-ttu-id="54254-114">Download en installeer Hallo meest recente versie van [Ruby](http://rubyinstaller.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="54254-114">Download and Install hello latest version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
- <span data-ttu-id="54254-115">Op Hallo voltooien scherm van de MSI-installer hello, Hallo selectievakje met de tekst 'uitvoeren 'ridk installeren' tooinstall MSYS2 en ontwikkeling toolchain'.</span><span class="sxs-lookup"><span data-stu-id="54254-115">On hello finish screen of hello MSI installer, check hello box that says "Run 'ridk install' tooinstall MSYS2 and development toolchain."</span></span> <span data-ttu-id="54254-116">Klik vervolgens op **voltooien** toolaunch Hallo volgende installatieprogramma.</span><span class="sxs-lookup"><span data-stu-id="54254-116">Then click **Finish** toolaunch hello next installer.</span></span>
- <span data-ttu-id="54254-117">Hallo RubyInstaller2 voor Windows installer wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="54254-117">hello RubyInstaller2 for Windows installer launches.</span></span> <span data-ttu-id="54254-118">Typ 2 tooinstall hello MSYS2 opslagplaats update.</span><span class="sxs-lookup"><span data-stu-id="54254-118">Type 2 tooinstall hello MSYS2 repository update.</span></span> <span data-ttu-id="54254-119">Nadat deze is voltooid en toohello gevraagd te installeren retourneert, sluit u Hallo-opdrachtvenster.</span><span class="sxs-lookup"><span data-stu-id="54254-119">After it finishes and returns toohello installation prompt, close hello command window.</span></span>
- <span data-ttu-id="54254-120">Start een nieuwe opdrachtprompt (cmd) vanuit het startmenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="54254-120">Launch a new command prompt (cmd) from hello Start menu.</span></span>
- <span data-ttu-id="54254-121">Test Hallo Ruby installatie `ruby -v` toosee Hallo versie is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="54254-121">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="54254-122">Hallo Gem installatie testen `gem -v` toosee Hallo versie is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="54254-122">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="54254-123">Hallo PostgreSQL-module maken voor Ruby Gem door Hallo opdracht uit te voeren met `gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="54254-123">Build hello PostgreSQL module for Ruby using Gem by running hello command `gem install pg`.</span></span>

### <a name="macos"></a><span data-ttu-id="54254-124">MacOS</span><span class="sxs-lookup"><span data-stu-id="54254-124">MacOS</span></span>
- <span data-ttu-id="54254-125">Installeren met behulp van Homebrew met Hallo opdracht Ruby `brew install ruby`.</span><span class="sxs-lookup"><span data-stu-id="54254-125">Install Ruby using Homebrew by running hello command `brew install ruby`.</span></span> <span data-ttu-id="54254-126">Zie voor meer opties voor installatie, Hallo Ruby [documentatie voor de installatie](https://www.ruby-lang.org/en/documentation/installation/#homebrew)</span><span class="sxs-lookup"><span data-stu-id="54254-126">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew)</span></span>
- <span data-ttu-id="54254-127">Test Hallo Ruby installatie `ruby -v` toosee Hallo versie is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="54254-127">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="54254-128">Hallo Gem installatie testen `gem -v` toosee Hallo versie is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="54254-128">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="54254-129">Hallo PostgreSQL-module maken voor Ruby Gem door Hallo opdracht uit te voeren met `gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="54254-129">Build hello PostgreSQL module for Ruby using Gem by running hello command `gem install pg`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="54254-130">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="54254-130">Linux (Ubuntu)</span></span>
- <span data-ttu-id="54254-131">Ruby installeren met de opdracht Hallo `sudo apt-get install ruby-full`.</span><span class="sxs-lookup"><span data-stu-id="54254-131">Install Ruby by running hello command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="54254-132">Zie voor meer opties voor installatie, Hallo Ruby [documentatie voor de installatie](https://www.ruby-lang.org/en/documentation/installation/).</span><span class="sxs-lookup"><span data-stu-id="54254-132">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
- <span data-ttu-id="54254-133">Test Hallo Ruby installatie `ruby -v` toosee Hallo versie is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="54254-133">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="54254-134">Hallo meest recente updates installeren voor de Gem met Hallo opdracht `sudo gem update --system`.</span><span class="sxs-lookup"><span data-stu-id="54254-134">Install hello latest updates for Gem by running hello command `sudo gem update --system`.</span></span>
- <span data-ttu-id="54254-135">Hallo Gem installatie testen `gem -v` toosee Hallo versie is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="54254-135">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="54254-136">Hallo gcc, type en andere build-hulpprogramma's installeren met de opdracht Hallo `sudo apt-get install build-essential`.</span><span class="sxs-lookup"><span data-stu-id="54254-136">Install hello gcc, make, and other build tools by running hello command `sudo apt-get install build-essential`.</span></span>
- <span data-ttu-id="54254-137">Hallo PostgreSQL bibliotheken installeren met de opdracht Hallo `sudo apt-get install libpq-dev`.</span><span class="sxs-lookup"><span data-stu-id="54254-137">Install hello PostgreSQL libraries by running hello command `sudo apt-get install libpq-dev`.</span></span>
- <span data-ttu-id="54254-138">Hallo Ruby pg-module met behulp van Gem met Hallo opdracht maken `sudo gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="54254-138">Build hello Ruby pg module using Gem by running hello command `sudo gem install pg`.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="54254-139">Ruby-code uitvoeren</span><span class="sxs-lookup"><span data-stu-id="54254-139">Run Ruby code</span></span> 
- <span data-ttu-id="54254-140">Hallo-code in een tekstbestand op te slaan en opslaan Hallo in een projectmap met bestand extensie .rb, zoals `C:\rubypostgres\read.rb` of`/home/username/rubypostgres/read.rb`</span><span class="sxs-lookup"><span data-stu-id="54254-140">Save hello code into a text file, and save hello file into a project folder with file extension .rb, such as `C:\rubypostgres\read.rb` or `/home/username/rubypostgres/read.rb`</span></span>
- <span data-ttu-id="54254-141">toorun hello code, opdrachtregel Hallo starten of bash-shell.</span><span class="sxs-lookup"><span data-stu-id="54254-141">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="54254-142">De map wijzigen in de projectmap `cd rubypostgres`, typt u de opdracht Hallo `ruby read.rb` toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="54254-142">Change directory into your project folder `cd rubypostgres`, then type hello command `ruby read.rb` toorun hello application.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="54254-143">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="54254-143">Get connection information</span></span>
<span data-ttu-id="54254-144">Hallo verbinding informatie die nodig is tooconnect toohello Azure Database voor PostgreSQL niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="54254-144">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="54254-145">U moet Hallo van server volledig gekwalificeerde servernaam en aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="54254-145">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="54254-146">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="54254-146">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="54254-147">Hallo links menu in Azure-portal en klik op **alle resources** en zoek naar Hallo-server die u hebt gemaakt, zoals **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="54254-147">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="54254-148">Klik op de servernaam Hallo **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="54254-148">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="54254-149">Selecteer Hallo-server **overzicht** pagina.</span><span class="sxs-lookup"><span data-stu-id="54254-149">Select hello server's **Overview** page.</span></span> <span data-ttu-id="54254-150">Maak een notitie van Hallo **servernaam** en **aanmeldingsnaam van Server-beheerder**.</span><span class="sxs-lookup"><span data-stu-id="54254-150">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="54254-151">![Azure Database voor PostgreSQL - Aanmeldgegevens van de serverbeheerder](./media/connect-ruby/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="54254-151">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-ruby/1-connection-string.png)</span></span>
5. <span data-ttu-id="54254-152">Als u uw aanmeldingsgegevens server bent vergeten, gaat u toohello **overzicht** pagina tooview Hallo aanmeldingsnaam van de serverbeheerder.</span><span class="sxs-lookup"><span data-stu-id="54254-152">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name.</span></span> <span data-ttu-id="54254-153">Indien nodig, Hallo-wachtwoord opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="54254-153">If necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="54254-154">Verbinding maken en een tabel maken</span><span class="sxs-lookup"><span data-stu-id="54254-154">Connect and create a table</span></span>
<span data-ttu-id="54254-155">Gebruik Hallo volgende tooconnect code en maak een tabel met **CREATE TABLE** SQL-instructie, gevolgd door **INSERT INTO** SQL-instructies tooadd rijen in de tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="54254-155">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="54254-156">Hallo-code wordt een [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object met de constructor [New](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="54254-156">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="54254-157">Vervolgens deze methode roept [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun Hallo neerzetten CREATE TABLE en INSERT INTO-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="54254-157">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="54254-158">Hallo code controleert op fouten bij het gebruik van Hallo [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) klasse.</span><span class="sxs-lookup"><span data-stu-id="54254-158">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="54254-159">Vervolgens deze methode roept [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose Hallo verbinding voordat het wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="54254-159">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="54254-160">Vervang Hallo `host`, `database`, `user`, en `password` tekenreeksen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="54254-160">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 
```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase'

    # Drop previous table of same name if one exists
    connection.exec('DROP TABLE IF EXISTS inventory;')
    puts 'Finished dropping table (if existed).'

    # Drop previous table of same name if one exists.
    connection.exec('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);')
    puts 'Finished creating table.'

    # Insert some data into table.
    connection.exec("INSERT INTO inventory VALUES(1, 'banana', 150)")
    connection.exec("INSERT INTO inventory VALUES(2, 'orange', 154)")
    connection.exec("INSERT INTO inventory VALUES(3, 'apple', 100)")
    puts 'Inserted 3 rows of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="read-data"></a><span data-ttu-id="54254-161">Gegevens lezen</span><span class="sxs-lookup"><span data-stu-id="54254-161">Read data</span></span>
<span data-ttu-id="54254-162">Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **Selecteer** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="54254-162">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="54254-163">Hallo-code wordt een [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object met de constructor [New](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="54254-163">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="54254-164">Vervolgens deze methode roept [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun Hallo SELECT-opdracht, waarbij u Hallo resultaten in een resultatenset.</span><span class="sxs-lookup"><span data-stu-id="54254-164">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello SELECT command, keeping hello results in a result set.</span></span> <span data-ttu-id="54254-165">Hallo resultaat set collectie wordt herhaald ten opzichte van Hallo `resultSet.each do` lus, waarbij u de huidige rijwaarden Hallo in Hallo `row` variabele.</span><span class="sxs-lookup"><span data-stu-id="54254-165">hello result set collection is iterated over using hello `resultSet.each do` loop, keeping hello current row values in hello `row` variable.</span></span> <span data-ttu-id="54254-166">Hallo code controleert op fouten bij het gebruik van Hallo [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) klasse.</span><span class="sxs-lookup"><span data-stu-id="54254-166">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="54254-167">Vervolgens deze methode roept [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose Hallo verbinding voordat het wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="54254-167">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="54254-168">Vervang Hallo `host`, `database`, `user`, en `password` tekenreeksen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="54254-168">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :database => dbname, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase.'

    resultSet = connection.exec('SELECT * from inventory;')
    resultSet.each do |row|
        puts 'Data row = (%s, %s, %s)' % [row['id'], row['name'], row['quantity']]
    end

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="update-data"></a><span data-ttu-id="54254-169">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="54254-169">Update data</span></span>
<span data-ttu-id="54254-170">Gebruik Hallo volgende tooconnect code en bij te werken Hallo gegevens met een **bijwerken** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="54254-170">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="54254-171">Hallo-code wordt een [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object met de constructor [New](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="54254-171">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="54254-172">Vervolgens deze methode roept [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun Hallo opdracht bijwerken.</span><span class="sxs-lookup"><span data-stu-id="54254-172">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello UPDATE command.</span></span> <span data-ttu-id="54254-173">Hallo code controleert op fouten bij het gebruik van Hallo [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) klasse.</span><span class="sxs-lookup"><span data-stu-id="54254-173">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="54254-174">Vervolgens deze methode roept [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose Hallo verbinding voordat het wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="54254-174">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="54254-175">Vervang Hallo `host`, `database`, `user`, en `password` tekenreeksen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="54254-175">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase.'

    # Modify some data in table.
    connection.exec('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
    puts 'Updated 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```


## <a name="delete-data"></a><span data-ttu-id="54254-176">Gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="54254-176">Delete data</span></span>
<span data-ttu-id="54254-177">Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **verwijderen** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="54254-177">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="54254-178">Hallo-code wordt een [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object met de constructor [New](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="54254-178">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="54254-179">Vervolgens deze methode roept [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun Hallo opdracht bijwerken.</span><span class="sxs-lookup"><span data-stu-id="54254-179">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello UPDATE command.</span></span> <span data-ttu-id="54254-180">Hallo code controleert op fouten bij het gebruik van Hallo [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) klasse.</span><span class="sxs-lookup"><span data-stu-id="54254-180">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="54254-181">Vervolgens deze methode roept [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose Hallo verbinding voordat het wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="54254-181">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="54254-182">Vervang Hallo `host`, `database`, `user`, en `password` tekenreeksen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="54254-182">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase.'

    # Modify some data in table.
    connection.exec('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="next-steps"></a><span data-ttu-id="54254-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="54254-183">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="54254-184">Een database migreren met behulp van Exporteren en importeren</span><span class="sxs-lookup"><span data-stu-id="54254-184">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
