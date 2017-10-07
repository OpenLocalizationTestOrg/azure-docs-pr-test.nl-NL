---
title: Verbinding maken met tooAzure Database voor MySQL Ga met | Microsoft Docs
description: Deze snelstartgids bevat verschillende Ga codevoorbeelden kunt u een query over gegevens uit Azure-Database voor MySQL en tooconnect gebruiken.
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: go
ms.topic: hero-article
ms.date: 07/18/2017
ms.openlocfilehash: e8067b807ee729e04850c5325f476806bcd54983
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-go-language-tooconnect-and-query-data"></a>Azure MySQL-Database: taal tooconnect en query gegevens gaat gebruiken
Deze snelstartgids demonstreert hoe tooconnect tooan Azure Database voor het gebruik van MySQL geschreven in Hallo code [gaat](https://golang.org/) taal van Windows-, Ubuntu Linux- en Apple Mac OS-platformen. Er wordt weergegeven hoe toouse SQL-instructies tooquery invoegen, bijwerken en verwijderen van gegevens in Hallo-database. In dit artikel wordt ervan uitgegaan dat u bekend bent met het ontwikkelen met behulp van gaat, maar in dat u nieuwe tooworking met Azure-Database voor MySQL.

## <a name="prerequisites"></a>Vereisten
Deze snelstartgids Hallo bronnen die zijn gemaakt in een van deze handleidingen als uitgangspunt gebruikt:
- [Een Azure-database voor een MySQL-server maken met behulp van Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Een Azure-database voor een MySQL-server maken met behulp van Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-go-and-mysql-connector"></a>Go en de MySQL-connector installeren
Installeer [gaat](https://golang.org/doc/install) en Hallo [gaat u-sql-stuurprogramma voor MySQL](https://github.com/go-sql-driver/mysql#installation) op uw computer. Hallo stappen, afhankelijk van uw platform:

### <a name="windows"></a>Windows
1. [Download](https://golang.org/dl/) en Ga voor Microsoft Windows toohello volgens installeren [installatie-instructies](https://golang.org/doc/install).
2. Hallo-opdrachtregel vanuit het startmenu Hallo starten.
3. Maak een map voor uw project, bijvoorbeeld: `mkdir  %USERPROFILE%\go\src\mysqlgo`.
4. Wijzig map in de projectmap hello, zoals `cd %USERPROFILE%\go\src\mysqlgo`.
5. Hallo-omgevingsvariabele voor GOPATH toopoint toohello source code directory ingesteld. `set GOPATH=%USERPROFILE%\go`.
6. Hallo installeren [gaat u-sql-stuurprogramma voor mysql](https://github.com/go-sql-driver/mysql#installation) door het uitvoeren van Hallo `go get github.com/go-sql-driver/mysql` opdracht.

   Kortom, installeer Ga en voer vervolgens deze opdrachten in het Hallo-opdrachtprompt:
   ```cmd
   mkdir  %USERPROFILE%\go\src\mysqlgo
   cd %USERPROFILE%\go\src\mysqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/go-sql-driver/mysql
   ```

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. Hallo Bash-shell start. 
2. Installeer Go door `sudo apt-get install golang-go` uit te voeren.
3. Maak in de basismap een map voor uw project, bijvoorbeeld `mkdir -p ~/go/src/mysqlgo/`.
4. Wijzig map naar de map hello, zoals `cd ~/go/src/mysqlgo/`.
5. Set Hallo GOPATH omgeving variabele toopoint tooa geldige bronmap, zoals uw huidige startpagina van de directory gaat map. Uitvoeren op Hallo bash-shell, `export GOPATH=~/go` tooadd Hallo directory gaat u als hello GOPATH voor Hallo huidige shell-sessie.
6. Hallo installeren [gaat u-sql-stuurprogramma voor mysql](https://github.com/go-sql-driver/mysql#installation) door het uitvoeren van Hallo `go get github.com/go-sql-driver/mysql` opdracht.

   Kortom: voer deze Bash-opdrachten uit:
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

### <a name="apple-macos"></a>Apple macOS
1. Download en installeer gaat op basis van toohello [installatie-instructies](https://golang.org/doc/install) die overeenkomt met uw platform. 
2. Hallo Bash-shell start. 
3. Maak in de basismap een map voor uw project, bijvoorbeeld `mkdir -p ~/go/src/mysqlgo/`.
4. Wijzig map naar de map hello, zoals `cd ~/go/src/mysqlgo/`.
5. Set Hallo GOPATH omgeving variabele toopoint tooa geldige bronmap, zoals uw huidige startpagina van de directory gaat map. Uitvoeren op Hallo bash-shell, `export GOPATH=~/go` tooadd Hallo directory gaat u als hello GOPATH voor Hallo huidige shell-sessie.
6. Hallo installeren [gaat u-sql-stuurprogramma voor mysql](https://github.com/go-sql-driver/mysql#installation) door het uitvoeren van Hallo `go get github.com/go-sql-driver/mysql` opdracht.

   Kortom: installeer Go en voer deze Bash-opdrachten uit:
   ```bash
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

## <a name="get-connection-information"></a>Verbindingsgegevens ophalen
Hallo verbinding informatie die nodig is tooconnect toohello Azure Database voor MySQL niet ophalen. U moet Hallo van server volledig gekwalificeerde servernaam en aanmeldingsreferenties.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com/).
2. Hallo links menu in Azure-portal en klik op **alle resources** en zoek naar Hallo-server die u hebt ook, zoals **myserver4demo**.
3. Klik op de servernaam Hallo **myserver4demo**.
4. Selecteer Hallo-server **eigenschappen** pagina. Maak een notitie van Hallo **servernaam** en **aanmeldingsnaam van Server-beheerder**.
 ![Azure Database voor MySQL - Aanmeldgegevens van de serverbeheerder](./media/connect-go/1_server-properties-name-login.png)
5. Als u uw aanmeldingsgegevens server bent vergeten, gaat u toohello **overzicht** pagina tooview Hallo Server admin-aanmeldingsnaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo.
   

## <a name="build-and-run-go-code"></a>Go-code schrijven en uitvoeren 
1. toowrite Golang code, kunt u een eenvoudige teksteditor zoals Kladblok in Microsoft Windows [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) of [Nano](https://www.nano-editor.org/) in Ubuntu en TextEdit voor Mac OS. Als u liever een uitgebreidere Interactive Development Environment (IDE) gebruikt, gaat u aan de slag met [Gogland](https://www.jetbrains.com/go/) van Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) van Microsoft of [Atom](https://atom.io/).
2. Hallo gaat u de code van Hallo secties in tekstbestanden te plakken en opslaan in de projectmap van uw met de bestandsextensie \*.gaat u, zoals Windows-pad `%USERPROFILE%\go\src\mysqlgo\createtable.go` of Linux-pad `~/go/src/mysqlgo/createtable.go`.
3. Zoek Hallo `HOST`, `DATABASE`, `USER`, en `PASSWORD` constanten in Hallo code en het Hallo-voorbeeldwaarden vervangen met uw eigen waarden. 
4. Hallo-opdrachtregel starten of bash-shell. Wijzig de map in de projectmap. Voorbeeld voor Windows: `cd %USERPROFILE%\go\src\mysqlgo\`. Voorbeeld voor Linux: `cd ~/go/src/mysqlgo/`.  Aantal Hallo IDE editors vermeld bieden mogelijkheden voor foutopsporing en runtime zonder shell-opdrachten.
5. Hallo code uitvoeren met de opdracht Hallo `go run createtable.go` toocompile Hallo toepassing en voer deze uit. 
6. U kunt ook toobuild Hallo code in een systeemeigen toepassing `go build createtable.go`, start vervolgens `createtable.exe` toorun Hallo-toepassing.

## <a name="connect-create-table-and-insert-data"></a>Verbinden, tabel maken en gegevens invoegen
Gebruik Hallo volgende code tooconnect toohello server, een tabel maken en laden Hallo gegevens met een **invoegen** SQL-instructie. 

Hallo code importeert drie pakketten: Hallo [sql-pakket](https://golang.org/pkg/database/sql/), Hallo [Ga sql-stuurprogramma voor mysql](https://github.com/go-sql-driver/mysql#installation) als een stuurprogramma toocommunicate met hello Azure Database voor MySQL en Hallo [fmt pakket](https://golang.org/pkg/fmt/)voor afgedrukte invoer en uitvoer op Hallo-opdrachtregel.

Hallo code roept de methode [sql. Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database voor MySQL en controles Hallo verbinding heeft via de methode [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Een [database ingang](https://golang.org/pkg/database/sql/#DB) wordt gebruikt in, houden van de verbindingsgroep Hallo voor Hallo database-server. Hallo code aanroepen Hallo [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) methode meerdere keren toorun verschillende DDL-opdrachten. Hallo code gebruikt ook Hallo [Prepare()](http://go-database-sql.org/prepared.html) en Exec() toorun voorbereid instructies met andere parameters tooinsert drie rijen. Telkens wanneer een aangepaste checkError()-methode is gebruikte toocheck als een fout opgetreden en tooexit zorgen.

Vervang Hallo `host`, `database`, `user`, en `password` constanten met uw eigen waarden. 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Drop previous table of same name if one exists.
    _, err = db.Exec("DROP TABLE IF EXISTS inventory;")
    checkError(err)
    fmt.Println("Finished dropping table (if existed).")

    // Create table.
    _, err = db.Exec("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
    checkError(err)
    fmt.Println("Finished creating table.")

    // Insert some data into table.
    sqlStatement, err := db.Prepare("INSERT INTO inventory (name, quantity) VALUES (?, ?);")
    res, err := sqlStatement.Exec("banana", 150)
    checkError(err)
    rowCount, err := res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)

    res, err = sqlStatement.Exec("orange", 154)
    checkError(err)
    rowCount, err = res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)

    res, err = sqlStatement.Exec("apple", 100)
    checkError(err)
    rowCount, err = res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}

```

## <a name="read-data"></a>Gegevens lezen
Gebruik Hallo volgende tooconnect code en lezen Hallo gegevens met een **Selecteer** SQL-instructie. 

Hallo code importeert drie pakketten: Hallo [sql-pakket](https://golang.org/pkg/database/sql/), Hallo [Ga sql-stuurprogramma voor mysql](https://github.com/go-sql-driver/mysql#installation) als een stuurprogramma toocommunicate met hello Azure Database voor MySQL en Hallo [fmt pakket](https://golang.org/pkg/fmt/)voor afgedrukte invoer en uitvoer op Hallo-opdrachtregel.

Hallo code roept de methode [sql. Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database voor MySQL en controles Hallo verbinding heeft via de methode [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Een [database ingang](https://golang.org/pkg/database/sql/#DB) wordt gebruikt in, houden van de verbindingsgroep Hallo voor Hallo database-server. Hallo code aanroepen Hallo [Query()](https://golang.org/pkg/database/sql/#DB.Query) methode toorun Hallo select-opdracht. Vervolgens wordt uitgevoerd [Next()](https://golang.org/pkg/database/sql/#Rows.Next) tooiterate door Hallo resultaatset en [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) tooparse Hallo kolomwaarden, Hallo waarde opslaan naar variabelen. Telkens wanneer een aangepaste checkError()-methode is gebruikte toocheck als een fout opgetreden en tooexit zorgen.

Vervang Hallo `host`, `database`, `user`, en `password` constanten met uw eigen waarden. 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Variables for printing column data when scanned.
    var (
        id       int
        name     string
        quantity int
    )

    // Read some data from hello table.
    rows, err := db.Query("SELECT id, name, quantity from inventory;")
    checkError(err)
    defer rows.Close()
    fmt.Println("Reading data:")
    for rows.Next() {
        err := rows.Scan(&id, &name, &quantity)
        checkError(err)
        fmt.Printf("Data row = (%d, %s, %d)\n", id, name, quantity)
    }
    err = rows.Err()
    checkError(err)
    fmt.Println("Done.")
}
```

## <a name="update-data"></a>Gegevens bijwerken
Gebruik Hallo volgende tooconnect code en bij te werken Hallo gegevens met een **bijwerken** SQL-instructie. 

Hallo code importeert drie pakketten: Hallo [sql-pakket](https://golang.org/pkg/database/sql/), Hallo [Ga sql-stuurprogramma voor mysql](https://github.com/go-sql-driver/mysql#installation) als een stuurprogramma toocommunicate met hello Azure Database voor MySQL en Hallo [fmt pakket](https://golang.org/pkg/fmt/)voor afgedrukte invoer en uitvoer op Hallo-opdrachtregel.

Hallo code roept de methode [sql. Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database voor MySQL en controles Hallo verbinding heeft via de methode [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Een [database ingang](https://golang.org/pkg/database/sql/#DB) wordt gebruikt in, houden van de verbindingsgroep Hallo voor Hallo database-server. Hallo code aanroepen Hallo [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) opdracht methode toorun Hallo-update. Telkens wanneer een aangepaste checkError()-methode is gebruikte toocheck als een fout opgetreden en tooexit zorgen.

Vervang Hallo `host`, `database`, `user`, en `password` constanten met uw eigen waarden. 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Modify some data in table.
    rows, err := db.Exec("UPDATE inventory SET quantity = ? WHERE name = ?", 200, "banana")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="delete-data"></a>Gegevens verwijderen
Gebruik Hallo volgende tooconnect code en verwijderen van gegevens met een **verwijderen** SQL-instructie. 

Hallo code importeert drie pakketten: Hallo [sql-pakket](https://golang.org/pkg/database/sql/), Hallo [Ga sql-stuurprogramma voor mysql](https://github.com/go-sql-driver/mysql#installation) als een stuurprogramma toocommunicate met hello Azure Database voor MySQL en Hallo [fmt pakket](https://golang.org/pkg/fmt/)voor afgedrukte invoer en uitvoer op Hallo-opdrachtregel.

Hallo code roept de methode [sql. Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database voor MySQL en controles Hallo verbinding heeft via de methode [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Een [database ingang](https://golang.org/pkg/database/sql/#DB) wordt gebruikt in, houden van de verbindingsgroep Hallo voor Hallo database-server. Hallo code aanroepen Hallo [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) methode toorun Hallo opdracht verwijderen. Telkens wanneer een aangepaste checkError()-methode is gebruikte toocheck als een fout opgetreden en tooexit zorgen.

Vervang Hallo `host`, `database`, `user`, en `password` constanten met uw eigen waarden. 

```Go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Modify some data in table.
    rows, err := db.Exec("DELETE FROM inventory WHERE name = ?", "orange")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="next-steps"></a>Volgende stappen
> [!div class="nextstepaction"]
> [Een database migreren met behulp van Exporteren en importeren](./concepts-migrate-import-export.md)
