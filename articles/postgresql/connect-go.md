---
title: aaaConnect tooAzure Database voor PostgreSQL Ga taal | Microsoft Docs
description: Deze snelstartgids bevat een Ga programming taal voorbeeld kunt u een query over gegevens uit Azure-Database voor PostgreSQL en tooconnect gebruiken.
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
ms.openlocfilehash: aa3c93da03116b8fcb54557494dccfad558e5f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-go-language-tooconnect-and-query-data"></a><span data-ttu-id="20f2d-103">Azure-Database voor PostgreSQL: gebruik gaat language tooconnect en query-gegevens</span><span class="sxs-lookup"><span data-stu-id="20f2d-103">Azure Database for PostgreSQL: Use Go language tooconnect and query data</span></span>
<span data-ttu-id="20f2d-104">Deze snelstartgids demonstreert hoe tooconnect tooan Azure Database voor het gebruik van PostgreSQL geschreven in Hallo code [gaat](https://golang.org/) taal (golang).</span><span class="sxs-lookup"><span data-stu-id="20f2d-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using code written in hello [Go](https://golang.org/) language (golang).</span></span> <span data-ttu-id="20f2d-105">Er wordt weergegeven hoe toouse SQL-instructies tooquery invoegen, bijwerken en verwijderen van gegevens in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="20f2d-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="20f2d-106">In dit artikel wordt ervan uitgegaan dat u bekend bent met het ontwikkelen met behulp van gaat, maar dat u nieuwe tooworking met Azure-Database voor PostgreSQL zijn.</span><span class="sxs-lookup"><span data-stu-id="20f2d-106">This article assumes you are familiar with development using Go, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20f2d-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="20f2d-107">Prerequisites</span></span>
<span data-ttu-id="20f2d-108">Deze snelstartgids Hallo bronnen die zijn gemaakt in een van deze handleidingen als uitgangspunt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="20f2d-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="20f2d-109">Database maken - Portal</span><span class="sxs-lookup"><span data-stu-id="20f2d-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="20f2d-110">Database maken - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="20f2d-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-go-and-pq-connector"></a><span data-ttu-id="20f2d-111">Go en de pq-connector installeren</span><span class="sxs-lookup"><span data-stu-id="20f2d-111">Install Go and pq connector</span></span>
<span data-ttu-id="20f2d-112">Installeer [gaat](https://golang.org/doc/install) en Hallo [Pure gaat Postgres stuurprogramma (pq)](https://github.com/lib/pq) op uw computer.</span><span class="sxs-lookup"><span data-stu-id="20f2d-112">Install [Go](https://golang.org/doc/install) and hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) on your own machine.</span></span> <span data-ttu-id="20f2d-113">Hallo stappen, afhankelijk van uw platform:</span><span class="sxs-lookup"><span data-stu-id="20f2d-113">Depending on your platform, follow hello steps:</span></span>

### <a name="windows"></a><span data-ttu-id="20f2d-114">Windows</span><span class="sxs-lookup"><span data-stu-id="20f2d-114">Windows</span></span>
1. <span data-ttu-id="20f2d-115">[Download](https://golang.org/dl/) en Ga voor Microsoft Windows toohello volgens installeren [installatie-instructies](https://golang.org/doc/install).</span><span class="sxs-lookup"><span data-stu-id="20f2d-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according toohello [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="20f2d-116">Hallo-opdrachtregel vanuit het startmenu Hallo starten.</span><span class="sxs-lookup"><span data-stu-id="20f2d-116">Launch hello command prompt from hello start menu.</span></span>
3. <span data-ttu-id="20f2d-117">Maak een map voor uw project, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="20f2d-117">Make a folder for your project such.</span></span> <span data-ttu-id="20f2d-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="20f2d-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span></span>
4. <span data-ttu-id="20f2d-119">Wijzig map in de projectmap hello, zoals `cd %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="20f2d-119">Change directory into hello project folder, such as `cd %USERPROFILE%\go\src\postgresqlgo`.</span></span>
5. <span data-ttu-id="20f2d-120">Hallo-omgevingsvariabele voor GOPATH toopoint toohello source code directory ingesteld.</span><span class="sxs-lookup"><span data-stu-id="20f2d-120">Set hello environment variable for GOPATH toopoint toohello source code directory.</span></span> <span data-ttu-id="20f2d-121">`set GOPATH=%USERPROFILE%\go`.</span><span class="sxs-lookup"><span data-stu-id="20f2d-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="20f2d-122">Hallo installeren [Pure gaat Postgres stuurprogramma (pq)](https://github.com/lib/pq) door het uitvoeren van Hallo `go get github.com/lib/pq` opdracht.</span><span class="sxs-lookup"><span data-stu-id="20f2d-122">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="20f2d-123">Kortom, installeer Ga en voer vervolgens deze opdrachten in het Hallo-opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="20f2d-123">In summary, install Go, then run these commands in hello command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\postgresqlgo
   cd %USERPROFILE%\go\src\postgresqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/lib/pq
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="20f2d-124">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="20f2d-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="20f2d-125">Hallo Bash-shell start.</span><span class="sxs-lookup"><span data-stu-id="20f2d-125">Launch hello Bash shell.</span></span> 
2. <span data-ttu-id="20f2d-126">Installeer Go door `sudo apt-get install golang-go` uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="20f2d-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="20f2d-127">Maak in de basismap een map voor uw project, bijvoorbeeld `mkdir -p ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="20f2d-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="20f2d-128">Wijzig map naar de map hello, zoals `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="20f2d-128">Change directory into hello folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="20f2d-129">Set Hallo GOPATH omgeving variabele toopoint tooa geldige bronmap, zoals uw huidige startpagina van de directory gaat map.</span><span class="sxs-lookup"><span data-stu-id="20f2d-129">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="20f2d-130">Uitvoeren op Hallo bash-shell, `export GOPATH=~/go` tooadd Hallo directory gaat u als hello GOPATH voor Hallo huidige shell-sessie.</span><span class="sxs-lookup"><span data-stu-id="20f2d-130">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="20f2d-131">Hallo installeren [Pure gaat Postgres stuurprogramma (pq)](https://github.com/lib/pq) door het uitvoeren van Hallo `go get github.com/lib/pq` opdracht.</span><span class="sxs-lookup"><span data-stu-id="20f2d-131">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="20f2d-132">Kortom: voer deze Bash-opdrachten uit:</span><span class="sxs-lookup"><span data-stu-id="20f2d-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

### <a name="apple-macos"></a><span data-ttu-id="20f2d-133">Apple macOS</span><span class="sxs-lookup"><span data-stu-id="20f2d-133">Apple macOS</span></span>
1. <span data-ttu-id="20f2d-134">Download en installeer gaat op basis van toohello [installatie-instructies](https://golang.org/doc/install) die overeenkomt met uw platform.</span><span class="sxs-lookup"><span data-stu-id="20f2d-134">Download and install Go according toohello [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="20f2d-135">Hallo Bash-shell start.</span><span class="sxs-lookup"><span data-stu-id="20f2d-135">Launch hello Bash shell.</span></span> 
3. <span data-ttu-id="20f2d-136">Maak in de basismap een map voor uw project, bijvoorbeeld `mkdir -p ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="20f2d-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="20f2d-137">Wijzig map naar de map hello, zoals `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="20f2d-137">Change directory into hello folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="20f2d-138">Set Hallo GOPATH omgeving variabele toopoint tooa geldige bronmap, zoals uw huidige startpagina van de directory gaat map.</span><span class="sxs-lookup"><span data-stu-id="20f2d-138">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="20f2d-139">Uitvoeren op Hallo bash-shell, `export GOPATH=~/go` tooadd Hallo directory gaat u als hello GOPATH voor Hallo huidige shell-sessie.</span><span class="sxs-lookup"><span data-stu-id="20f2d-139">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="20f2d-140">Hallo installeren [Pure gaat Postgres stuurprogramma (pq)](https://github.com/lib/pq) door het uitvoeren van Hallo `go get github.com/lib/pq` opdracht.</span><span class="sxs-lookup"><span data-stu-id="20f2d-140">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="20f2d-141">Kortom: installeer Go en voer deze Bash-opdrachten uit:</span><span class="sxs-lookup"><span data-stu-id="20f2d-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

## <a name="get-connection-information"></a><span data-ttu-id="20f2d-142">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="20f2d-142">Get connection information</span></span>
<span data-ttu-id="20f2d-143">Hallo verbinding informatie die nodig is tooconnect toohello Azure Database voor PostgreSQL niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="20f2d-143">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="20f2d-144">U moet Hallo van server volledig gekwalificeerde servernaam en aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="20f2d-144">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="20f2d-145">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="20f2d-145">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="20f2d-146">Hallo links menu in Azure-portal en klik op **alle resources** en zoek naar Hallo-server die u hebt gemaakt, zoals **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="20f2d-146">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="20f2d-147">Klik op de servernaam Hallo **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="20f2d-147">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="20f2d-148">Selecteer Hallo-server **overzicht** pagina.</span><span class="sxs-lookup"><span data-stu-id="20f2d-148">Select hello server's **Overview** page.</span></span> <span data-ttu-id="20f2d-149">Maak een notitie van Hallo **servernaam** en **aanmeldingsnaam van Server-beheerder**.</span><span class="sxs-lookup"><span data-stu-id="20f2d-149">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="20f2d-150">![Azure Database voor PostgreSQL - Aanmeldgegevens van de serverbeheerder](./media/connect-go/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="20f2d-150">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-go/1-connection-string.png)</span></span>
5. <span data-ttu-id="20f2d-151">Als u uw aanmeldingsgegevens server bent vergeten, gaat u toohello **overzicht** pagina en de aanmeldingsnaam voor weergave Hallo Server-beheerder.</span><span class="sxs-lookup"><span data-stu-id="20f2d-151">If you forget your server login information, navigate toohello **Overview** page, and view hello Server admin login name.</span></span> <span data-ttu-id="20f2d-152">Indien nodig, Hallo-wachtwoord opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="20f2d-152">If necessary, reset hello password.</span></span>

## <a name="build-and-run-go-code"></a><span data-ttu-id="20f2d-153">Go-code schrijven en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="20f2d-153">Build and run Go code</span></span> 
1. <span data-ttu-id="20f2d-154">toowrite Golang code, kunt u een eenvoudige teksteditor zoals Kladblok in Microsoft Windows [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) of [Nano](https://www.nano-editor.org/) in Ubuntu en TextEdit voor Mac OS.</span><span class="sxs-lookup"><span data-stu-id="20f2d-154">toowrite Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="20f2d-155">Als u liever een uitgebreidere Interactive Development Environment (IDE) gebruikt, gaat u aan de slag met [Gogland](https://www.jetbrains.com/go/) van Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) van Microsoft of [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="20f2d-155">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="20f2d-156">Hallo Golang code uit Hallo secties in tekstbestanden te plakken en opslaan in de projectmap van uw met de bestandsextensie \*.gaat u, zoals Windows-pad `%USERPROFILE%\go\src\postgresqlgo\createtable.go` of Linux-pad `~/go/src/postgresqlgo/createtable.go`.</span><span class="sxs-lookup"><span data-stu-id="20f2d-156">Paste hello Golang code from hello sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\postgresqlgo\createtable.go` or Linux path `~/go/src/postgresqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="20f2d-157">Zoek Hallo `HOST`, `DATABASE`, `USER`, en `PASSWORD` constanten in Hallo code en het Hallo-voorbeeldwaarden vervangen met uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="20f2d-157">Locate hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in hello code, and replace hello example values with your own values.</span></span>  
4. <span data-ttu-id="20f2d-158">Hallo-opdrachtregel starten of bash-shell.</span><span class="sxs-lookup"><span data-stu-id="20f2d-158">Launch hello command prompt or bash shell.</span></span> <span data-ttu-id="20f2d-159">Wijzig de map in de projectmap.</span><span class="sxs-lookup"><span data-stu-id="20f2d-159">Change directory into your project folder.</span></span> <span data-ttu-id="20f2d-160">Voorbeeld voor Windows: `cd %USERPROFILE%\go\src\postgresqlgo\`.</span><span class="sxs-lookup"><span data-stu-id="20f2d-160">For example, on Windows `cd %USERPROFILE%\go\src\postgresqlgo\`.</span></span> <span data-ttu-id="20f2d-161">Voorbeeld voor Linux: `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="20f2d-161">On Linux `cd ~/go/src/postgresqlgo/`.</span></span> <span data-ttu-id="20f2d-162">Aantal Hallo IDE omgevingen vermeld bieden mogelijkheden voor foutopsporing en runtime zonder shell-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="20f2d-162">Some of hello IDE environments mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="20f2d-163">Hallo code uitvoeren met de opdracht Hallo `go run createtable.go` toocompile Hallo toepassing en voer deze uit.</span><span class="sxs-lookup"><span data-stu-id="20f2d-163">Run hello code by typing hello command `go run createtable.go` toocompile hello application and run it.</span></span> 
6. <span data-ttu-id="20f2d-164">U kunt ook toobuild Hallo code in een systeemeigen toepassing `go build createtable.go`, start vervolgens `createtable.exe` toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="20f2d-164">Alternatively, toobuild hello code into a native application, `go build createtable.go`, then launch `createtable.exe` toorun hello application.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="20f2d-165">Verbinding maken en een tabel maken</span><span class="sxs-lookup"><span data-stu-id="20f2d-165">Connect and create a table</span></span>
<span data-ttu-id="20f2d-166">Gebruik Hallo volgende tooconnect code en maak een tabel met **CREATE TABLE** SQL-instructie, gevolgd door **INSERT INTO** SQL-instructies tooadd rijen in de tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="20f2d-166">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="20f2d-167">Hallo code importeert drie pakketten: Hallo [sql-pakket](https://golang.org/pkg/database/sql/), Hallo [pq pakket](http://godoc.org/github.com/lib/pq) als een stuurprogramma toocommunicate met Hallo Postgres server en Hallo [fmt pakket](https://golang.org/pkg/fmt/) voor afdrukken invoer en uitvoer op Hallo-opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="20f2d-167">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="20f2d-168">Hallo code roept de methode [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database voor PostgreSQL en controles Hallo verbinding heeft via de methode [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="20f2d-168">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="20f2d-169">Een [database ingang](https://golang.org/pkg/database/sql/#DB) wordt gebruikt in, houden van de verbindingsgroep Hallo voor Hallo database-server.</span><span class="sxs-lookup"><span data-stu-id="20f2d-169">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="20f2d-170">Hallo code aanroepen Hallo [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) methode meerdere keren toorun verschillende SQL-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="20f2d-170">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times toorun several SQL commands.</span></span> <span data-ttu-id="20f2d-171">Telkens wanneer een aangepaste checkError() methode toocheck als een fout opgetreden en tooexit zorgen als er een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="20f2d-171">Each time a custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="20f2d-172">Vervang Hallo `HOST`, `DATABASE`, `USER`, en `PASSWORD` parameters met uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="20f2d-172">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

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
    fmt.Println("Successfully created connection toodatabase")

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

## <a name="read-data"></a><span data-ttu-id="20f2d-173">Gegevens lezen</span><span class="sxs-lookup"><span data-stu-id="20f2d-173">Read data</span></span>
<span data-ttu-id="20f2d-174">Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **Selecteer** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="20f2d-174">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="20f2d-175">Hallo code importeert drie pakketten: Hallo [sql-pakket](https://golang.org/pkg/database/sql/), Hallo [pq pakket](http://godoc.org/github.com/lib/pq) als een stuurprogramma toocommunicate met Hallo Postgres server en Hallo [fmt pakket](https://golang.org/pkg/fmt/) voor afdrukken invoer en uitvoer op Hallo-opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="20f2d-175">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="20f2d-176">Hallo code roept de methode [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database voor PostgreSQL en controles Hallo verbinding heeft via de methode [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="20f2d-176">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="20f2d-177">Een [database ingang](https://golang.org/pkg/database/sql/#DB) wordt gebruikt in, houden van de verbindingsgroep Hallo voor Hallo database-server.</span><span class="sxs-lookup"><span data-stu-id="20f2d-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="20f2d-178">Hallo select-query wordt uitgevoerd door het aanroepen van methode [db. Query()](https://golang.org/pkg/database/sql/#DB.Query), en de resulterende rijen hello wordt bewaard in een variabele van het type [rijen](https://golang.org/pkg/database/sql/#Rows).</span><span class="sxs-lookup"><span data-stu-id="20f2d-178">hello select query is run by calling method [db.Query()](https://golang.org/pkg/database/sql/#DB.Query), and hello resulting rows is kept in a variable of type [rows](https://golang.org/pkg/database/sql/#Rows).</span></span> <span data-ttu-id="20f2d-179">Hallo code leest Hallo kolomwaarden gegevens in de huidige rij Hallo via methode [rijen. Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) en lussen over Hallo rijen met Hallo iterator [rijen. Next()](https://golang.org/pkg/database/sql/#Rows.Next) totdat meer rijen niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="20f2d-179">hello code reads hello column data values in hello current row using method [rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) and loops over hello rows using hello iterator [rows.Next()](https://golang.org/pkg/database/sql/#Rows.Next) until no more rows exist.</span></span> <span data-ttu-id="20f2d-180">Elke rij kolomwaarden zijn afgedrukte toohello console uit. Telkens wanneer een aangepaste checkError() methode toocheck als een fout opgetreden en tooexit zorgen als er een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="20f2d-180">Each row's column values are printed toohello console out. Each time a custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="20f2d-181">Vervang Hallo `HOST`, `DATABASE`, `USER`, en `PASSWORD` parameters met uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="20f2d-181">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

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
    fmt.Println("Successfully created connection toodatabase")

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

## <a name="update-data"></a><span data-ttu-id="20f2d-182">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="20f2d-182">Update data</span></span>
<span data-ttu-id="20f2d-183">Gebruik Hallo volgende tooconnect code en bij te werken Hallo gegevens met een **bijwerken** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="20f2d-183">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="20f2d-184">Hallo code importeert drie pakketten: Hallo [sql-pakket](https://golang.org/pkg/database/sql/), Hallo [pq pakket](http://godoc.org/github.com/lib/pq) als een stuurprogramma toocommunicate met Hallo Postgres server en Hallo [fmt pakket](https://golang.org/pkg/fmt/) voor afdrukken invoer en uitvoer op Hallo-opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="20f2d-184">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="20f2d-185">Hallo code roept de methode [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database voor PostgreSQL en controles Hallo verbinding heeft via de methode [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="20f2d-185">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="20f2d-186">Een [database ingang](https://golang.org/pkg/database/sql/#DB) wordt gebruikt in, houden van de verbindingsgroep Hallo voor Hallo database-server.</span><span class="sxs-lookup"><span data-stu-id="20f2d-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="20f2d-187">Hallo code aanroepen Hallo [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) methode toorun Hallo SQL-instructie waarmee Hallo tabel wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="20f2d-187">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello SQL statement that updates hello table.</span></span> <span data-ttu-id="20f2d-188">Een aangepaste checkError() methode toocheck optreedt als een fout opgetreden en tooexit zorgen er een fout.</span><span class="sxs-lookup"><span data-stu-id="20f2d-188">A custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="20f2d-189">Vervang Hallo `HOST`, `DATABASE`, `USER`, en `PASSWORD` parameters met uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="20f2d-189">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
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
    fmt.Println("Successfully created connection toodatabase")

    // Modify some data in table.
    sql_statement := "UPDATE inventory SET quantity = $2 WHERE name = $1;"
    _, err = db.Exec(sql_statement, "banana", 200)
    checkError(err)
    fmt.Println("Updated 1 row of data")
}
```

## <a name="delete-data"></a><span data-ttu-id="20f2d-190">Gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="20f2d-190">Delete data</span></span>
<span data-ttu-id="20f2d-191">Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **verwijderen** SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="20f2d-191">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="20f2d-192">Hallo code importeert drie pakketten: Hallo [sql-pakket](https://golang.org/pkg/database/sql/), Hallo [pq pakket](http://godoc.org/github.com/lib/pq) als een stuurprogramma toocommunicate met Hallo Postgres server en Hallo [fmt pakket](https://golang.org/pkg/fmt/) voor afdrukken invoer en uitvoer op Hallo-opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="20f2d-192">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="20f2d-193">Hallo code roept de methode [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database voor PostgreSQL en controles Hallo verbinding heeft via de methode [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="20f2d-193">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="20f2d-194">Een [database ingang](https://golang.org/pkg/database/sql/#DB) wordt gebruikt in, houden van de verbindingsgroep Hallo voor Hallo database-server.</span><span class="sxs-lookup"><span data-stu-id="20f2d-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="20f2d-195">Hallo code aanroepen Hallo [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) methode toorun Hallo SQL-instructie waarmee Hallo tabel wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="20f2d-195">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello SQL statement that updates hello table.</span></span> <span data-ttu-id="20f2d-196">Een aangepaste checkError() methode toocheck optreedt als een fout opgetreden en tooexit zorgen er een fout.</span><span class="sxs-lookup"><span data-stu-id="20f2d-196">A custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="20f2d-197">Vervang Hallo `HOST`, `DATABASE`, `USER`, en `PASSWORD` parameters met uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="20f2d-197">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
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
    fmt.Println("Successfully created connection toodatabase")

    // Delete some data from table.
    sql_statement := "DELETE FROM inventory WHERE name = $1;"
    _, err = db.Exec(sql_statement, "orange")
    checkError(err)
    fmt.Println("Deleted 1 row of data")
}
```

## <a name="next-steps"></a><span data-ttu-id="20f2d-198">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="20f2d-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="20f2d-199">Een database migreren met behulp van Exporteren en importeren</span><span class="sxs-lookup"><span data-stu-id="20f2d-199">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
