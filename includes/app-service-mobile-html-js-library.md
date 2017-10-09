## <a name="create-client"></a>Een clientverbinding maken
Maak een clientverbinding door een `WindowsAzure.MobileServiceClient`-object te maken.  Vervang `appUrl` met de URL tooyour mobiele App.

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <a name="table-reference"></a>Werken met tabellen
tooaccess of update gegevens, maken een verwijzing toohello back-end-tabel. Vervang `tableName` met de naam van de tabel Hallo

```
var table = client.getTable(tableName);
```

Wanneer u een tabelverwijzing hebt, kunt u verder werken aan uw tabel:

* [Een query uitvoeren op een tabel](#querying)
  * [Gegevens filteren](#table-filter)
  * [Door gegevens bladeren](#table-paging)
  * [Gegevens sorteren](#sorting-data)
* [Gegevens invoegen](#inserting)
* [Gegevens wijzigen](#modifying)
* [Gegevens verwijderen](#deleting)

### <a name="querying"></a>Procedure: Een query uitvoeren op een tabelverwijzing
Zodra u een tabelverwijzing hebt, kunt u dit tooquery gebruiken voor gegevens op Hallo-server.  Query's worden gemaakt in een LINQ-achtige taal.
tooreturn alle gegevens van de tabel hello, gebruik Hallo volgende code:

```
/**
 * Process hello results that are received by a call tootable.read()
 *
 * @param {Object} results hello results as a pseudo-array
 * @param {int} results.length hello length of hello results array
 * @param {Object} results[] hello individual results
 */
function success(results) {
   var numItemsRead = results.length;

   for (var i = 0 ; i < results.length ; i++) {
       var row = results[i];
       // Each row is an object - hello properties are hello columns
   }
}

function failure(error) {
    throw new Error('Error loading data: ', error);
}

table
    .read()
    .then(success, failure);
```

Hallo geslaagd functie is aangeroepen met Hallo resultaten.  Gebruik geen `for (var i in results)` in Hallo geslaagd werkt zoals die wordt herhaald over informatie die is opgenomen in de resultaten Hallo wanneer andere queryfuncties (zoals `.includeTotalCount()`) worden gebruikt.

Zie voor meer informatie over Hallo querysyntaxis Hallo [object Querydocumentatie].

#### <a name="table-filter"></a>Filteren van gegevens op Hallo-server
U kunt een `where` component op Hallo tabelverwijzing:

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

U kunt ook een functie die Hallo object filtert gebruiken.  In dit geval Hallo `this` variabele toothe huidige object replicatiefilterprocedure is toegewezen.  Hallo na de code is functioneel equivalent toohello voorafgaande voorbeeld:

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <a name="table-paging"></a>Door gegevens bladeren
Gebruikmaken van Hallo `take()` en `skip()` methoden.  Bijvoorbeeld, u kunt eventueel toosplit Hallo tabel in de rij 100 records:

```
var totalCount = 0, pages = 0;

// Step 1 - get hello total number of records
table.includeTotalCount().take(0).read(function (results) {
    totalCount = results.totalCount;
    pages = Math.floor(totalCount/100) + 1;
    loadPage(0);
}, failure);

function loadPage(pageNum) {
    let skip = pageNum * 100;
    table.skip(skip).take(100).read(function (results) {
        for (var i = 0 ; i < results.length ; i++) {
            var row = results[i];
            // Process each row
        }
    }
}
```

Hallo `.includeTotalCount()` methode gebruikte tooadd een totalCount veld toohello results-object is.  Het veld totalCount wordt gevuld met Hallo kunt u het totale aantal records dat wordt geretourneerd als geen paginering wordt gebruikt.

U kunt Hallo pagina's variabele en sommige UI knoppen tooprovide een paginalijst. Gebruik `loadPage()` Hallo nieuwe records voor elke pagina te laden.  Implementeren in het cachegeheugen toospeed toegang toorecords die al zijn geladen.

#### <a name="sorting-data"></a>Procedure: Gesorteerde gegevens retourneren
Gebruik Hallo `.orderBy()` of `.orderByDescending()` query methoden:

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

Zie voor meer informatie over het queryobject Hallo Hallo [object Querydocumentatie].

### <a name="inserting"></a>Procedure: Gegevens invoegen
Een JavaScript-object maken met de juiste datum Hallo en aanroep `table.insert()` asynchroon:

```javascript
var newItem = {
    name: 'My Name',
    signupDate: new Date()
};

table
    .insert(newItem)
    .done(function (insertedItem) {
        var id = insertedItem.id;
    }, failure);
```

Op geslaagde invoegen Hallo ingevoegd item geretourneerd met de Hallo aanvullende velden die vereist voor synchronisatiebewerkingen zijn.  Werk uw eigen cache bij met deze gegevens voor latere updates.

Hello Azure Mobile Apps-Node.js-SDK biedt ondersteuning voor dynamische-schema voor ontwikkelingsdoeleinden.  Dynamische Schema kunt u tooadd kolommen toohello tabel in een bewerking insert of update opgeven.  U wordt aangeraden dat u dynamische schema uitschakelen voordat u uw toepassing tooproduction verplaatst.

### <a name="modifying"></a>Procedure: Gegevens wijzigen
Vergelijkbare toohello `.insert()` methode die u moet een Update-object maken en vervolgens aanroepen `.update()`.  Hallo update object mag Hallo-ID van de record toobe Hallo bijgewerkt - Hallo-ID is verkregen tijdens het lezen van Hallo record of bij het aanroepen van `.insert()`.

```javascript
var updateItem = {
    id: '7163bc7a-70b2-4dde-98e9-8818969611bd',
    name: 'My New Name'
};

table
    .update(updateItem)
    .done(function (updatedItem) {
        // You can now update your cached copy
    }, failure);
```

### <a name="deleting"></a>Procedure: Gegevens verwijderen
toodelete een record aanroep Hallo `.del()` methode.  Hallo-ID doorgeven in een objectverwijzing:

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
