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
# <a name="azure-database-for-postgresql-use-go-language-tooconnect-and-query-data"></a>Azure-Database voor PostgreSQL: gebruik gaat language tooconnect en query-gegevens
Deze snelstartgids demonstreert hoe tooconnect tooan Azure Database voor het gebruik van PostgreSQL geschreven in Hallo code [gaat](https://golang.org/) taal (golang). Er wordt weergegeven hoe toouse SQL-instructies tooquery invoegen, bijwerken en verwijderen van gegevens in Hallo-database. In dit artikel wordt ervan uitgegaan dat u bekend bent met het ontwikkelen met behulp van gaat, maar dat u nieuwe tooworking met Azure-Database voor PostgreSQL zijn.

## <a name="prerequisites"></a>Vereisten
Deze snelstartgids Hallo bronnen die zijn gemaakt in een van deze handleidingen als uitgangspunt gebruikt:
- [Database maken - Portal](quickstart-create-server-database-portal.md)
- [Database maken - Azure CLI](quickstart-create-server-database-azure-cli.md)

## <a name="install-go-and-pq-connector"></a>Go en de pq-connector installeren
Installeer [gaat](https://golang.org/doc/install) en Hallo [Pure gaat Postgres stuurprogramma (pq)](https://github.com/lib/pq) op uw computer. Hallo stappen, afhankelijk van uw platform:

### <a name="windows"></a>Windows
1. [Download](https://golang.org/dl/) en Ga voor Microsoft Windows toohello volgens installeren [installatie-instructies](https://golang.org/doc/install).
2. Hallo-opdrachtregel vanuit het startmenu Hallo starten.
3. Maak een map voor uw project, bijvoorbeeld: `mkdir  %USERPROFILE%\go\src\postgresqlgo`.
4. Wijzig map in de projectmap hello, zoals `cd %USERPROFILE%\go\src\postgresqlgo`.
5. Hallo-omgevingsvariabele voor GOPATH toopoint toohello source code directory ingesteld. `set GOPATH=%USERPROFILE%\go`.
6. Hallo installeren [Pure gaat Postgres stuurprogramma (pq)](https://github.com/lib/pq) door het uitvoeren van Hallo `go get github.com/lib/pq` opdracht.

   Kortom, installeer Ga en voer vervolgens deze opdrachten in het Hallo-opdrachtprompt:
   ```cmd
   mkdir  %USERPROFILE%\go\src\postgresqlgo
   cd %USERPROFILE%\go\src\postgresqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/lib/pq
   ```

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. Hallo Bash-shell start. 
2. Installeer Go door `sudo apt-get install golang-go` uit te voeren.
3. Maak in de basismap een map voor uw project, bijvoorbeeld `mkdir -p ~/go/src/postgresqlgo/`.
4. Wijzig map naar de map hello, zoals `cd ~/go/src/postgresqlgo/`.
5. Set Hallo GOPATH omgeving variabele toopoint tooa geldige bronmap, zoals uw huidige startpagina van de directory gaat map. Uitvoeren op Hallo bash-shell, `export GOPATH=~/go` tooadd Hallo directory gaat u als hello GOPATH voor Hallo huidige shell-sessie.
6. Hallo installeren [Pure gaat Postgres stuurprogramma (pq)](https://github.com/lib/pq) door het uitvoeren van Hallo `go get github.com/lib/pq` opdracht.

   Kortom: voer deze Bash-opdrachten uit:
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

### <a name="apple-macos"></a>Apple macOS
1. Download en installeer gaat op basis van toohello [installatie-instructies](https://golang.org/doc/install) die overeenkomt met uw platform. 
2. Hallo Bash-shell start. 
3. Maak in de basismap een map voor uw project, bijvoorbeeld `mkdir -p ~/go/src/postgresqlgo/`.
4. Wijzig map naar de map hello, zoals `cd ~/go/src/postgresqlgo/`.
5. Set Hallo GOPATH omgeving variabele toopoint tooa geldige bronmap, zoals uw huidige startpagina van de directory gaat map. Uitvoeren op Hallo bash-shell, `export GOPATH=~/go` tooadd Hallo directory gaat u als hello GOPATH voor Hallo huidige shell-sessie.
6. Hallo installeren [Pure gaat Postgres stuurprogramma (pq)](https://github.com/lib/pq) door het uitvoeren van Hallo `go get github.com/lib/pq` opdracht.

   Kortom: installeer Go en voer deze Bash-opdrachten uit:
   ```bash
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

## <a name="get-connection-information"></a>Verbindingsgegevens ophalen
Hallo verbinding informatie die nodig is tooconnect toohello Azure Database voor PostgreSQL niet ophalen. U moet Hallo van server volledig gekwalificeerde servernaam en aanmeldingsreferenties.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com/).
2. Hallo links menu in Azure-portal en klik op **alle resources** en zoek naar Hallo-server die u hebt gemaakt, zoals **mypgserver 20170401**.
3. Klik op de servernaam Hallo **mypgserver 20170401**.
4. Selecteer Hallo-server **overzicht** pagina. Maak een notitie van Hallo **servernaam** en **aanmeldingsnaam van Server-beheerder**.
 ![Azure Database voor PostgreSQL - Aanmeldgegevens van de serverbeheerder](./media/connect-go/1-connection-string.png)
5. Als u uw aanmeldingsgegevens server bent vergeten, gaat u toohello **overzicht** pagina en de aanmeldingsnaam voor weergave Hallo Server-beheerder. Indien nodig, Hallo-wachtwoord opnieuw instellen.

## <a name="build-and-run-go-code"></a>Go-code schrijven en uitvoeren 
1. toowrite Golang code, kunt u een eenvoudige teksteditor zoals Kladblok in Microsoft Windows [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) of [Nano](https://www.nano-editor.org/) in Ubuntu en TextEdit voor Mac OS. Als u liever een uitgebreidere Interactive Development Environment (IDE) gebruikt, gaat u aan de slag met [Gogland](https://www.jetbrains.com/go/) van Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) van Microsoft of [Atom](https://atom.io/).
2. Hallo Golang code uit Hallo secties in tekstbestanden te plakken en opslaan in de projectmap van uw met de bestandsextensie \*.gaat u, zoals Windows-pad `%USERPROFILE%\go\src\postgresqlgo\createtable.go` of Linux-pad `~/go/src/postgresqlgo/createtable.go`.
3. Zoek Hallo `HOST`, `DATABASE`, `USER`, en `PASSWORD` constanten in Hallo code en het Hallo-voorbeeldwaarden vervangen met uw eigen waarden.  
4. Hallo-opdrachtregel starten of bash-shell. Wijzig de map in de projectmap. Voorbeeld voor Windows: `cd %USERPROFILE%\go\src\postgresqlgo\`. Voorbeeld voor Linux: `cd ~/go/src/postgresqlgo/`. Aantal Hallo IDE omgevingen vermeld bieden mogelijkheden voor foutopsporing en runtime zonder shell-opdrachten.
5. Hallo code uitvoeren met de opdracht Hallo `go run createtable.go` toocompile Hallo toepassing en voer deze uit. 
6. U kunt ook toobuild Hallo code in een systeemeigen toepassing `go build createtable.go`, start vervolgens `createtable.exe` toorun Hallo-toepassing.

## <a name="connect-and-create-a-table"></a>Verbinding maken en een tabel maken
Gebruik Hallo volgende tooconnect code en maak een tabel met **CREATE TABLE** SQL-instructie, gevolgd door **INSERT INTO** SQL-instructies tooadd rijen in de tabel Hallo.

Hallo code importeert drie pakketten: Hallo [sql-pakket](https://golang.org/pkg/database/sql/), Hallo [pq pakket](http://godoc.org/github.com/lib/pq) als een stuurprogramma toocommunicate met Hallo Postgres server en Hallo [fmt pakket](https://golang.org/pkg/fmt/) voor afdrukken invoer en uitvoer op Hallo-opdrachtregel.

Hallo code roept de methode [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database voor PostgreSQL en controles Hallo verbinding heeft via de methode [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Een [database ingang](https://golang.org/pkg/database/sql/#DB) wordt gebruikt in, houden van de verbindingsgroep Hallo voor Hallo database-server. Hallo code aanroepen Hallo [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) methode meerdere keren toorun verschillende SQL-opdrachten. Telkens wanneer een aangepaste checkError() methode toocheck als een fout opgetreden en tooexit zorgen als er een fout optreedt.

Vervang Hallo `HOST`, `DATABASE`, `USER`, en `PASSWORD` parameters met uw eigen waarden. 

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

## <a name="read-data"></a>Gegevens lezen
Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **Selecteer** SQL-instructie. 

Hallo code importeert drie pakketten: Hallo [sql-pakket](https://golang.org/pkg/database/sql/), Hallo [pq pakket](http://godoc.org/github.com/lib/pq) als een stuurprogramma toocommunicate met Hallo Postgres server en Hallo [fmt pakket](https://golang.org/pkg/fmt/) voor afdrukken invoer en uitvoer op Hallo-opdrachtregel.

Hallo code roept de methode [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database voor PostgreSQL en controles Hallo verbinding heeft via de methode [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Een [database ingang](https://golang.org/pkg/database/sql/#DB) wordt gebruikt in, houden van de verbindingsgroep Hallo voor Hallo database-server. Hallo select-query wordt uitgevoerd door het aanroepen van methode [db. Query()](https://golang.org/pkg/database/sql/#DB.Query), en de resulterende rijen hello wordt bewaard in een variabele van het type [rijen](https://golang.org/pkg/database/sql/#Rows). Hallo code leest Hallo kolomwaarden gegevens in de huidige rij Hallo via methode [rijen. Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) en lussen over Hallo rijen met Hallo iterator [rijen. Next()](https://golang.org/pkg/database/sql/#Rows.Next) totdat meer rijen niet bestaat. Elke rij kolomwaarden zijn afgedrukte toohello console uit. Telkens wanneer een aangepaste checkError() methode toocheck als een fout opgetreden en tooexit zorgen als er een fout optreedt.

Vervang Hallo `HOST`, `DATABASE`, `USER`, en `PASSWORD` parameters met uw eigen waarden. 

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

## <a name="update-data"></a>Gegevens bijwerken
Gebruik Hallo volgende tooconnect code en bij te werken Hallo gegevens met een **bijwerken** SQL-instructie.

Hallo code importeert drie pakketten: Hallo [sql-pakket](https://golang.org/pkg/database/sql/), Hallo [pq pakket](http://godoc.org/github.com/lib/pq) als een stuurprogramma toocommunicate met Hallo Postgres server en Hallo [fmt pakket](https://golang.org/pkg/fmt/) voor afdrukken invoer en uitvoer op Hallo-opdrachtregel.

Hallo code roept de methode [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database voor PostgreSQL en controles Hallo verbinding heeft via de methode [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Een [database ingang](https://golang.org/pkg/database/sql/#DB) wordt gebruikt in, houden van de verbindingsgroep Hallo voor Hallo database-server. Hallo code aanroepen Hallo [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) methode toorun Hallo SQL-instructie waarmee Hallo tabel wordt bijgewerkt. Een aangepaste checkError() methode toocheck optreedt als een fout opgetreden en tooexit zorgen er een fout.

Vervang Hallo `HOST`, `DATABASE`, `USER`, en `PASSWORD` parameters met uw eigen waarden. 
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

## <a name="delete-data"></a>Gegevens verwijderen
Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **verwijderen** SQL-instructie. 

Hallo code importeert drie pakketten: Hallo [sql-pakket](https://golang.org/pkg/database/sql/), Hallo [pq pakket](http://godoc.org/github.com/lib/pq) als een stuurprogramma toocommunicate met Hallo Postgres server en Hallo [fmt pakket](https://golang.org/pkg/fmt/) voor afdrukken invoer en uitvoer op Hallo-opdrachtregel.

Hallo code roept de methode [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database voor PostgreSQL en controles Hallo verbinding heeft via de methode [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Een [database ingang](https://golang.org/pkg/database/sql/#DB) wordt gebruikt in, houden van de verbindingsgroep Hallo voor Hallo database-server. Hallo code aanroepen Hallo [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) methode toorun Hallo SQL-instructie waarmee Hallo tabel wordt bijgewerkt. Een aangepaste checkError() methode toocheck optreedt als een fout opgetreden en tooexit zorgen er een fout.

Vervang Hallo `HOST`, `DATABASE`, `USER`, en `PASSWORD` parameters met uw eigen waarden. 
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

## <a name="next-steps"></a>Volgende stappen
> [!div class="nextstepaction"]
> [Een database migreren met behulp van Exporteren en importeren](./howto-migrate-using-export-and-import.md)
