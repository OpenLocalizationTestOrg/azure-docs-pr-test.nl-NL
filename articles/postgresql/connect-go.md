---
title: Met Go-taal verbinding maken met Azure Database voor PostgreSQL | Microsoft Docs
description: Deze snelstartgids bevat een voorbeeld van de programmeertaal Go dat u kunt gebruiken om verbinding te maken met en gegevens op te vragen uit een Azure Database voor PostgreSQL.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: go
ms.topic: quickstart
ms.date: 06/29/2017
ms.openlocfilehash: a7555464879826c5e4f55929d23163b002664e81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-go-language-to-connect-and-query-data"></a><span data-ttu-id="fc63d-103">Azure Database voor PostgreSQL: Go-taal gebruiken om verbinding te maken en gegevens op te vragen</span><span class="sxs-lookup"><span data-stu-id="fc63d-103">Azure Database for PostgreSQL: Use Go language to connect and query data</span></span>
<span data-ttu-id="fc63d-104">In deze snelstartgids ziet u hoe u met behulp van code in de [Go](https://golang.org/)-taal (golang) verbinding maakt met een Azure-database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="fc63d-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using code written in the [Go](https://golang.org/) language (golang).</span></span> <span data-ttu-id="fc63d-105">U ziet hier hoe u SQL-instructies gebruikt om gegevens in de database op te vragen, in te voegen, bij te werken en te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="fc63d-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="fc63d-106">In dit artikel wordt ervan uitgegaan dat u bekend bent met het ontwikkelen met Go, maar geen ervaring hebt met het werken met Azure Database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="fc63d-106">This article assumes you are familiar with development using Go, but that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc63d-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fc63d-107">Prerequisites</span></span>
<span data-ttu-id="fc63d-108">In deze snelstartgids worden de resources die in een van deze handleidingen zijn gemaakt, als uitgangspunt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="fc63d-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="fc63d-109">Database maken - Portal</span><span class="sxs-lookup"><span data-stu-id="fc63d-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="fc63d-110">Database maken - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fc63d-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-go-and-pq-connector"></a><span data-ttu-id="fc63d-111">Go en de pq-connector installeren</span><span class="sxs-lookup"><span data-stu-id="fc63d-111">Install Go and pq connector</span></span>
<span data-ttu-id="fc63d-112">Installeer [Go](https://golang.org/doc/install) en het [Pure Go Postgres-stuurprogramma (pq)](https://github.com/lib/pq) op uw computer.</span><span class="sxs-lookup"><span data-stu-id="fc63d-112">Install [Go](https://golang.org/doc/install) and the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) on your own machine.</span></span> <span data-ttu-id="fc63d-113">Volg de stappen voor uw platform uit:</span><span class="sxs-lookup"><span data-stu-id="fc63d-113">Depending on your platform, follow the steps:</span></span>

### <a name="windows"></a><span data-ttu-id="fc63d-114">Windows</span><span class="sxs-lookup"><span data-stu-id="fc63d-114">Windows</span></span>
1. <span data-ttu-id="fc63d-115">[Download](https://golang.org/dl/) en installeer Go voor Microsoft Windows volgens de [installatie-instructies](https://golang.org/doc/install).</span><span class="sxs-lookup"><span data-stu-id="fc63d-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according to the [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="fc63d-116">Open de opdrachtprompt vanuit het Startmenu.</span><span class="sxs-lookup"><span data-stu-id="fc63d-116">Launch the command prompt from the start menu.</span></span>
3. <span data-ttu-id="fc63d-117">Maak een map voor uw project, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="fc63d-117">Make a folder for your project such.</span></span> <span data-ttu-id="fc63d-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="fc63d-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span></span>
4. <span data-ttu-id="fc63d-119">Wijzig de map in de projectmap, bijvoorbeeld `cd %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="fc63d-119">Change directory into the project folder, such as `cd %USERPROFILE%\go\src\postgresqlgo`.</span></span>
5. <span data-ttu-id="fc63d-120">Stel de omgevingsvariabele voor GOPATH zo in dat deze verwijst naar de broncodemap.</span><span class="sxs-lookup"><span data-stu-id="fc63d-120">Set the environment variable for GOPATH to point to the source code directory.</span></span> <span data-ttu-id="fc63d-121">`set GOPATH=%USERPROFILE%\go`.</span><span class="sxs-lookup"><span data-stu-id="fc63d-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="fc63d-122">Installeer het [Pure Go Postgres-stuurprogramma (pq)](https://github.com/lib/pq) door de opdracht `go get github.com/lib/pq` uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="fc63d-122">Install the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running the `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="fc63d-123">Kortom: installeer Go en voer vervolgens deze opdrachten uit in de opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="fc63d-123">In summary, install Go, then run these commands in the command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\postgresqlgo
   cd %USERPROFILE%\go\src\postgresqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/lib/pq
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="fc63d-124">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="fc63d-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="fc63d-125">Open de Bash-shell.</span><span class="sxs-lookup"><span data-stu-id="fc63d-125">Launch the Bash shell.</span></span> 
2. <span data-ttu-id="fc63d-126">Installeer Go door `sudo apt-get install golang-go` uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="fc63d-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="fc63d-127">Maak in de basismap een map voor uw project, bijvoorbeeld `mkdir -p ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="fc63d-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="fc63d-128">Wijzig de map in de map, bijvoorbeeld `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="fc63d-128">Change directory into the folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="fc63d-129">Stel de omgevingsvariabele GOPATH zo in dat deze verwijst naar een geldige bronmap, zoals de Go-map in uw huidige basismap.</span><span class="sxs-lookup"><span data-stu-id="fc63d-129">Set the GOPATH environment variable to point to a valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="fc63d-130">Voer `export GOPATH=~/go` in de Bash-shell uit om de Go-map toe te voegen als GOPATH voor de huidige shellsessie.</span><span class="sxs-lookup"><span data-stu-id="fc63d-130">At the bash shell, run `export GOPATH=~/go` to add the go directory as the GOPATH for the current shell session.</span></span>
6. <span data-ttu-id="fc63d-131">Installeer het [Pure Go Postgres-stuurprogramma (pq)](https://github.com/lib/pq) door de opdracht `go get github.com/lib/pq` uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="fc63d-131">Install the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running the `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="fc63d-132">Kortom: voer deze Bash-opdrachten uit:</span><span class="sxs-lookup"><span data-stu-id="fc63d-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

### <a name="apple-macos"></a><span data-ttu-id="fc63d-133">Apple macOS</span><span class="sxs-lookup"><span data-stu-id="fc63d-133">Apple macOS</span></span>
1. <span data-ttu-id="fc63d-134">Download en installeer Go volgens de [installatie-instructies](https://golang.org/doc/install) die overeenkomen met uw platform.</span><span class="sxs-lookup"><span data-stu-id="fc63d-134">Download and install Go according to the [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="fc63d-135">Open de Bash-shell.</span><span class="sxs-lookup"><span data-stu-id="fc63d-135">Launch the Bash shell.</span></span> 
3. <span data-ttu-id="fc63d-136">Maak in de basismap een map voor uw project, bijvoorbeeld `mkdir -p ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="fc63d-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="fc63d-137">Wijzig de map in de map, bijvoorbeeld `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="fc63d-137">Change directory into the folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="fc63d-138">Stel de omgevingsvariabele GOPATH zo in dat deze verwijst naar een geldige bronmap, zoals de Go-map in uw huidige basismap.</span><span class="sxs-lookup"><span data-stu-id="fc63d-138">Set the GOPATH environment variable to point to a valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="fc63d-139">Voer `export GOPATH=~/go` in de Bash-shell uit om de Go-map toe te voegen als GOPATH voor de huidige shellsessie.</span><span class="sxs-lookup"><span data-stu-id="fc63d-139">At the bash shell, run `export GOPATH=~/go` to add the go directory as the GOPATH for the current shell session.</span></span>
6. <span data-ttu-id="fc63d-140">Installeer het [Pure Go Postgres-stuurprogramma (pq)](https://github.com/lib/pq) door de opdracht `go get github.com/lib/pq` uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="fc63d-140">Install the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running the `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="fc63d-141">Kortom: installeer Go en voer deze Bash-opdrachten uit:</span><span class="sxs-lookup"><span data-stu-id="fc63d-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

## <a name="get-connection-information"></a><span data-ttu-id="fc63d-142">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="fc63d-142">Get connection information</span></span>
<span data-ttu-id="fc63d-143">Haal de verbindingsgegevens op die nodig zijn om verbinding te maken met de Azure Database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="fc63d-143">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="fc63d-144">U hebt de volledig gekwalificeerde servernaam en aanmeldingsreferenties nodig.</span><span class="sxs-lookup"><span data-stu-id="fc63d-144">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="fc63d-145">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fc63d-145">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="fc63d-146">Klik in het menu links in Azure Portal op **Alle resources** en zoek de server die u hebt gemaakt (bijvoorbeeld **mypgserver-20170401**).</span><span class="sxs-lookup"><span data-stu-id="fc63d-146">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="fc63d-147">Klik op de servernaam **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="fc63d-147">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="fc63d-148">Selecteer de pagina **Overzicht** van de server.</span><span class="sxs-lookup"><span data-stu-id="fc63d-148">Select the server's **Overview** page.</span></span> <span data-ttu-id="fc63d-149">Noteer de **servernaam** en de **gebruikersnaam van de serverbeheerder**.</span><span class="sxs-lookup"><span data-stu-id="fc63d-149">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="fc63d-150">![Azure Database voor PostgreSQL - Aanmeldgegevens van de serverbeheerder](./media/connect-go/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="fc63d-150">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-go/1-connection-string.png)</span></span>
5. <span data-ttu-id="fc63d-151">Als u uw aanmeldingsgegevens voor de server bent vergeten, gaat u naar de pagina **Overzicht** om de aanmeldingsnaam van de serverbeheerder weer te geven.</span><span class="sxs-lookup"><span data-stu-id="fc63d-151">If you forget your server login information, navigate to the **Overview** page, and view the Server admin login name.</span></span> <span data-ttu-id="fc63d-152">Stel het wachtwoord indien nodig opnieuw in.</span><span class="sxs-lookup"><span data-stu-id="fc63d-152">If necessary, reset the password.</span></span>

## <a name="build-and-run-go-code"></a><span data-ttu-id="fc63d-153">Go-code schrijven en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="fc63d-153">Build and run Go code</span></span> 
1. <span data-ttu-id="fc63d-154">Als u Golang-code wilt schrijven, gebruikt u een eenvoudige teksteditor zoals Kladblok in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) of [Nano](https://www.nano-editor.org/) in Ubuntu en TextEdit in macOS.</span><span class="sxs-lookup"><span data-stu-id="fc63d-154">To write Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="fc63d-155">Als u liever een uitgebreidere Interactive Development Environment (IDE) gebruikt, gaat u aan de slag met [Gogland](https://www.jetbrains.com/go/) van Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) van Microsoft of [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="fc63d-155">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="fc63d-156">Plak de Golang-code uit de secties hieronder in tekstbestanden en sla deze in de projectmap op met de bestandsextensie \*.go, zoals het pad `%USERPROFILE%\go\src\postgresqlgo\createtable.go` (voor Windows) of het pad `~/go/src/postgresqlgo/createtable.go` (voor Linux).</span><span class="sxs-lookup"><span data-stu-id="fc63d-156">Paste the Golang code from the sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\postgresqlgo\createtable.go` or Linux path `~/go/src/postgresqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="fc63d-157">Zoek de constanten `HOST`, `DATABASE`, `USER` en `PASSWORD` in de code en vervang de voorbeeldwaarden door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="fc63d-157">Locate the `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in the code, and replace the example values with your own values.</span></span>  
4. <span data-ttu-id="fc63d-158">Open de opdrachtprompt of de Bash-shell.</span><span class="sxs-lookup"><span data-stu-id="fc63d-158">Launch the command prompt or bash shell.</span></span> <span data-ttu-id="fc63d-159">Wijzig de map in de projectmap.</span><span class="sxs-lookup"><span data-stu-id="fc63d-159">Change directory into your project folder.</span></span> <span data-ttu-id="fc63d-160">Voorbeeld voor Windows: `cd %USERPROFILE%\go\src\postgresqlgo\`.</span><span class="sxs-lookup"><span data-stu-id="fc63d-160">For example, on Windows `cd %USERPROFILE%\go\src\postgresqlgo\`.</span></span> <span data-ttu-id="fc63d-161">Voorbeeld voor Linux: `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="fc63d-161">On Linux `cd ~/go/src/postgresqlgo/`.</span></span> <span data-ttu-id="fc63d-162">Sommige van de vermelde IDE-omgevingen bieden mogelijkheden voor foutopsporing en runtime zonder dat daarvoor shell-opdrachten zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="fc63d-162">Some of the IDE environments mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="fc63d-163">Voer de code uit door de opdracht `go run createtable.go` te typen. De toepassing wordt nu gecompileerd en uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fc63d-163">Run the code by typing the command `go run createtable.go` to compile the application and run it.</span></span> 
6. <span data-ttu-id="fc63d-164">Als u de code wilt bouwen in een systeemeigen toepassing, kunt u ook `go build createtable.go` gebruiken en vervolgens `createtable.exe` starten om de toepassing uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="fc63d-164">Alternatively, to build the code into a native application, `go build createtable.go`, then launch `createtable.exe` to run the application.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="fc63d-165">Verbinding maken en een tabel maken</span><span class="sxs-lookup"><span data-stu-id="fc63d-165">Connect and create a table</span></span>
<span data-ttu-id="fc63d-166">Gebruik de volgende code om een tabel te verbinden en te maken met de SQL-instructie **CREATE TABLE**, gevolgd door **INSERT INTO**-instructies om rijen in de tabel toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="fc63d-166">Use the following code to connect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span></span>

<span data-ttu-id="fc63d-167">Met de code worden drie pakketten geïmporteerd: het [sql-pakket](https://golang.org/pkg/database/sql/), het [pq-pakket](http://godoc.org/github.com/lib/pq) als een stuurprogramma om te communiceren met de Postgres-server, en het [fmt-pakket](https://golang.org/pkg/fmt/) voor de weergave van invoer en uitvoer op de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="fc63d-167">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="fc63d-168">In de code wordt de methode [sql.Open()](http://godoc.org/github.com/lib/pq#Open) aangeroepen om verbinding te maken met Azure Database voor PostgreSQL, en wordt de verbinding gecontroleerd met de methode [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="fc63d-168">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="fc63d-169">Er wordt telkens gebruikgemaakt van een [database-ingang](https://golang.org/pkg/database/sql/#DB), die de verbindingsgroep voor de databaseserver bevat.</span><span class="sxs-lookup"><span data-stu-id="fc63d-169">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="fc63d-170">In de code wordt de methode [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) meerdere keren aangeroepen om diverse SQL-opdrachten uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="fc63d-170">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times to run several SQL commands.</span></span> <span data-ttu-id="fc63d-171">Telkens wordt een aangepaste checkError()-methode gebruikt om te controleren of er fouten zijn opgetreden en af te sluiten als er een fout is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="fc63d-171">Each time a custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="fc63d-172">Vervang de parameters `HOST`, `DATABASE`, `USER` en `PASSWORD` door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="fc63d-172">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

```go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/lib/pq"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    // Initialize connection string.
    var connectionString string = fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection to database")

    // Drop previous table of same name if one exists.
    _, err = db.Exec("DROP TABLE IF EXISTS inventory;")
    checkError(err)
    fmt.Println("Finished dropping table (if existed)")

    // Create table.
    _, err = db.Exec("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
    checkError(err)
    fmt.Println("Finished creating table")

    // Insert some data into table.
    sql_statement := "INSERT INTO inventory (name, quantity) VALUES ($1, $2);"
    _, err = db.Exec(sql_statement, "banana", 150)
    checkError(err)
    _, err = db.Exec(sql_statement, "orange", 154)
    checkError(err)
    _, err = db.Exec(sql_statement, "apple", 100)
    checkError(err)
    fmt.Println("Inserted 3 rows of data")
}
```

## <a name="read-data"></a><span data-ttu-id="fc63d-173">Gegevens lezen</span><span class="sxs-lookup"><span data-stu-id="fc63d-173">Read data</span></span>
<span data-ttu-id="fc63d-174">Gebruik de volgende code om verbinding te maken en de gegevens te lezen met de SQL-instructie **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="fc63d-174">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="fc63d-175">Met de code worden drie pakketten geïmporteerd: het [sql-pakket](https://golang.org/pkg/database/sql/), het [pq-pakket](http://godoc.org/github.com/lib/pq) als een stuurprogramma om te communiceren met de Postgres-server, en het [fmt-pakket](https://golang.org/pkg/fmt/) voor de weergave van invoer en uitvoer op de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="fc63d-175">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="fc63d-176">In de code wordt de methode [sql.Open()](http://godoc.org/github.com/lib/pq#Open) aangeroepen om verbinding te maken met Azure Database voor PostgreSQL, en wordt de verbinding gecontroleerd met de methode [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="fc63d-176">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="fc63d-177">Er wordt telkens gebruikgemaakt van een [database-ingang](https://golang.org/pkg/database/sql/#DB), die de verbindingsgroep voor de databaseserver bevat.</span><span class="sxs-lookup"><span data-stu-id="fc63d-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="fc63d-178">De selectiequery wordt uitgevoerd door de methode [db.Query()](https://golang.org/pkg/database/sql/#DB.Query) aan te roepen, en de resulterende rijen wordt bewaard in een variabele van het type [rijen](https://golang.org/pkg/database/sql/#Rows).</span><span class="sxs-lookup"><span data-stu-id="fc63d-178">The select query is run by calling method [db.Query()](https://golang.org/pkg/database/sql/#DB.Query), and the resulting rows is kept in a variable of type [rows](https://golang.org/pkg/database/sql/#Rows).</span></span> <span data-ttu-id="fc63d-179">In de code worden de kolomgegevenswaarden in de huidige rij gelezen met de methode [rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) en de rijen worden helemaal doorlopen met behulp van de iterator [rows.Next()](https://golang.org/pkg/database/sql/#Rows.Next), totdat er geen rijen meer zijn.</span><span class="sxs-lookup"><span data-stu-id="fc63d-179">The code reads the column data values in the current row using method [rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) and loops over the rows using the iterator [rows.Next()](https://golang.org/pkg/database/sql/#Rows.Next) until no more rows exist.</span></span> <span data-ttu-id="fc63d-180">De kolomwaarden van elke rij worden weergegeven in de console. Telkens wordt een aangepaste checkError()-methode gebruikt om te controleren of er fouten zijn opgetreden en af te sluiten als er een fout is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="fc63d-180">Each row's column values are printed to the console out. Each time a custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="fc63d-181">Vervang de parameters `HOST`, `DATABASE`, `USER` en `PASSWORD` door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="fc63d-181">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

```go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/lib/pq"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString string = fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection to database")

    // Read rows from table.
    var id int
    var name string
    var quantity int

    sql_statement := "SELECT * from inventory;"
    rows, err := db.Query(sql_statement)
    checkError(err)

    for rows.Next() {
        switch err := rows.Scan(&id, &name, &quantity); err {
        case sql.ErrNoRows:
            fmt.Println("No rows were returned")
        case nil:
            fmt.Printf("Data row = (%d, %s, %d)\n", id, name, quantity)
        default:
            checkError(err)
        }
    }
}
```

## <a name="update-data"></a><span data-ttu-id="fc63d-182">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="fc63d-182">Update data</span></span>
<span data-ttu-id="fc63d-183">Gebruik de volgende code om verbinding te maken en de gegevens bij te werken met de SQL-instructie **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="fc63d-183">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="fc63d-184">Met de code worden drie pakketten geïmporteerd: het [sql-pakket](https://golang.org/pkg/database/sql/), het [pq-pakket](http://godoc.org/github.com/lib/pq) als een stuurprogramma om te communiceren met de Postgres-server, en het [fmt-pakket](https://golang.org/pkg/fmt/) voor de weergave van invoer en uitvoer op de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="fc63d-184">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="fc63d-185">In de code wordt de methode [sql.Open()](http://godoc.org/github.com/lib/pq#Open) aangeroepen om verbinding te maken met Azure Database voor PostgreSQL, en wordt de verbinding gecontroleerd met de methode [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="fc63d-185">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="fc63d-186">Er wordt telkens gebruikgemaakt van een [database-ingang](https://golang.org/pkg/database/sql/#DB), die de verbindingsgroep voor de databaseserver bevat.</span><span class="sxs-lookup"><span data-stu-id="fc63d-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="fc63d-187">In de code wordt de methode [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) aangeroepen om de SQL-instructie uit te voeren waarmee de tabel wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="fc63d-187">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method to run the SQL statement that updates the table.</span></span> <span data-ttu-id="fc63d-188">Er wordt een aangepaste checkError()-methode gebruikt om te controleren of er fouten zijn opgetreden en af te sluiten als er een fout is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="fc63d-188">A custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="fc63d-189">Vervang de parameters `HOST`, `DATABASE`, `USER` en `PASSWORD` door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="fc63d-189">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
```go
package main

import (
  "database/sql"
  _ "github.com/lib/pq"
  "fmt"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    
    // Initialize connection string.
    var connectionString string = 
        fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection to database")

    // Modify some data in table.
    sql_statement := "UPDATE inventory SET quantity = $2 WHERE name = $1;"
    _, err = db.Exec(sql_statement, "banana", 200)
    checkError(err)
    fmt.Println("Updated 1 row of data")
}
```

## <a name="delete-data"></a><span data-ttu-id="fc63d-190">Gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="fc63d-190">Delete data</span></span>
<span data-ttu-id="fc63d-191">Gebruik de volgende code om verbinding te maken en de gegevens te lezen met de SQL-instructie **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="fc63d-191">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="fc63d-192">Met de code worden drie pakketten geïmporteerd: het [sql-pakket](https://golang.org/pkg/database/sql/), het [pq-pakket](http://godoc.org/github.com/lib/pq) als een stuurprogramma om te communiceren met de Postgres-server, en het [fmt-pakket](https://golang.org/pkg/fmt/) voor de weergave van invoer en uitvoer op de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="fc63d-192">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="fc63d-193">In de code wordt de methode [sql.Open()](http://godoc.org/github.com/lib/pq#Open) aangeroepen om verbinding te maken met Azure Database voor PostgreSQL, en wordt de verbinding gecontroleerd met de methode [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="fc63d-193">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="fc63d-194">Er wordt telkens gebruikgemaakt van een [database-ingang](https://golang.org/pkg/database/sql/#DB), die de verbindingsgroep voor de databaseserver bevat.</span><span class="sxs-lookup"><span data-stu-id="fc63d-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="fc63d-195">In de code wordt de methode [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) aangeroepen om de SQL-instructie uit te voeren waarmee de tabel wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="fc63d-195">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method to run the SQL statement that updates the table.</span></span> <span data-ttu-id="fc63d-196">Er wordt een aangepaste checkError()-methode gebruikt om te controleren of er fouten zijn opgetreden en af te sluiten als er een fout is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="fc63d-196">A custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="fc63d-197">Vervang de parameters `HOST`, `DATABASE`, `USER` en `PASSWORD` door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="fc63d-197">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
```go
package main

import (
  "database/sql"
  _ "github.com/lib/pq"
  "fmt"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    
    // Initialize connection string.
    var connectionString string = 
        fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection to database")

    // Delete some data from table.
    sql_statement := "DELETE FROM inventory WHERE name = $1;"
    _, err = db.Exec(sql_statement, "orange")
    checkError(err)
    fmt.Println("Deleted 1 row of data")
}
```

## <a name="next-steps"></a><span data-ttu-id="fc63d-198">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fc63d-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="fc63d-199">Een database migreren met behulp van Exporteren en importeren</span><span class="sxs-lookup"><span data-stu-id="fc63d-199">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
