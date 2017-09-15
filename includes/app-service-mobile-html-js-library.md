## <span data-ttu-id="2ddae-101"><a name="create-client"></a>Een clientverbinding maken</span><span class="sxs-lookup"><span data-stu-id="2ddae-101"><a name="create-client"></a>Create a client connection</span></span>
<span data-ttu-id="2ddae-102">Maak een clientverbinding door een `WindowsAzure.MobileServiceClient`-object te maken.</span><span class="sxs-lookup"><span data-stu-id="2ddae-102">Create a client connection by creating a `WindowsAzure.MobileServiceClient` object.</span></span>  <span data-ttu-id="2ddae-103">Vervang `appUrl` door de URL van uw mobiele app.</span><span class="sxs-lookup"><span data-stu-id="2ddae-103">Replace `appUrl` with the URL to your Mobile App.</span></span>

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <span data-ttu-id="2ddae-104"><a name="table-reference"></a>Werken met tabellen</span><span class="sxs-lookup"><span data-stu-id="2ddae-104"><a name="table-reference"></a>Work with tables</span></span>
<span data-ttu-id="2ddae-105">Maak een verwijzing naar de back-endtabel als u gegevens wilt bekijken of bijwerken.</span><span class="sxs-lookup"><span data-stu-id="2ddae-105">To access or update data, create a reference to the backend table.</span></span> <span data-ttu-id="2ddae-106">Vervang `tableName` door de naam van uw tabel</span><span class="sxs-lookup"><span data-stu-id="2ddae-106">Replace `tableName` with the name of your table</span></span>

```
var table = client.getTable(tableName);
```

<span data-ttu-id="2ddae-107">Wanneer u een tabelverwijzing hebt, kunt u verder werken aan uw tabel:</span><span class="sxs-lookup"><span data-stu-id="2ddae-107">Once you have a table reference, you can work further with your table:</span></span>

* [<span data-ttu-id="2ddae-108">Een query uitvoeren op een tabel</span><span class="sxs-lookup"><span data-stu-id="2ddae-108">Query a Table</span></span>](#querying)
  * [<span data-ttu-id="2ddae-109">Gegevens filteren</span><span class="sxs-lookup"><span data-stu-id="2ddae-109">Filtering Data</span></span>](#table-filter)
  * [<span data-ttu-id="2ddae-110">Door gegevens bladeren</span><span class="sxs-lookup"><span data-stu-id="2ddae-110">Paging through Data</span></span>](#table-paging)
  * [<span data-ttu-id="2ddae-111">Gegevens sorteren</span><span class="sxs-lookup"><span data-stu-id="2ddae-111">Sorting Data</span></span>](#sorting-data)
* [<span data-ttu-id="2ddae-112">Gegevens invoegen</span><span class="sxs-lookup"><span data-stu-id="2ddae-112">Inserting Data</span></span>](#inserting)
* [<span data-ttu-id="2ddae-113">Gegevens wijzigen</span><span class="sxs-lookup"><span data-stu-id="2ddae-113">Modifying Data</span></span>](#modifying)
* [<span data-ttu-id="2ddae-114">Gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="2ddae-114">Deleting Data</span></span>](#deleting)

### <span data-ttu-id="2ddae-115"><a name="querying"></a>Procedure: Een query uitvoeren op een tabelverwijzing</span><span class="sxs-lookup"><span data-stu-id="2ddae-115"><a name="querying"></a>How to: Query a table reference</span></span>
<span data-ttu-id="2ddae-116">Als u een tabelverwijzing hebt, kunt u deze gebruiken om een query uit te voeren op gegevens op de server.</span><span class="sxs-lookup"><span data-stu-id="2ddae-116">Once you have a table reference, you can use it to query for data on the server.</span></span>  <span data-ttu-id="2ddae-117">Query's worden gemaakt in een LINQ-achtige taal.</span><span class="sxs-lookup"><span data-stu-id="2ddae-117">Queries are made in a "LINQ-like" language.</span></span>
<span data-ttu-id="2ddae-118">Gebruik de volgende code om alle gegevens uit de tabel op te halen:</span><span class="sxs-lookup"><span data-stu-id="2ddae-118">To return all data from the table, use the following code:</span></span>

```
/**
 * Process the results that are received by a call to table.read()
 *
 * @param {Object} results the results as a pseudo-array
 * @param {int} results.length the length of the results array
 * @param {Object} results[] the individual results
 */
function success(results) {
   var numItemsRead = results.length;

   for (var i = 0 ; i < results.length ; i++) {
       var row = results[i];
       // Each row is an object - the properties are the columns
   }
}

function failure(error) {
    throw new Error('Error loading data: ', error);
}

table
    .read()
    .then(success, failure);
```

<span data-ttu-id="2ddae-119">De functie voor geslaagde pogingen wordt aangeroepen met de resultaten.</span><span class="sxs-lookup"><span data-stu-id="2ddae-119">The success function is called with the results.</span></span>  <span data-ttu-id="2ddae-120">Gebruik `for (var i in results)` niet in de functie voor geslaagde pogingen, aangezien dit wordt herhaald voor informatie die is opgenomen in de resultaten wanneer andere queryfuncties (zoals `.includeTotalCount()`) worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2ddae-120">Do not use `for (var i in results)` in the success function as that will iterate over information that is included in the results when other query functions (such as `.includeTotalCount()`) are used.</span></span>

<span data-ttu-id="2ddae-121">Zie de [Documentatie over queryobjecten] voor meer informatie over de querysyntaxis.</span><span class="sxs-lookup"><span data-stu-id="2ddae-121">For more information on the Query syntax, see the [Query object documentation].</span></span>

#### <span data-ttu-id="2ddae-122"><a name="table-filter"></a>Gegevens filteren op de server</span><span class="sxs-lookup"><span data-stu-id="2ddae-122"><a name="table-filter"></a>Filtering data on the server</span></span>
<span data-ttu-id="2ddae-123">U kunt in de tabelverwijzing een `where`-clausule gebruiken:</span><span class="sxs-lookup"><span data-stu-id="2ddae-123">You can use a `where` clause on the table reference:</span></span>

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

<span data-ttu-id="2ddae-124">U kunt ook een functie gebruiken die het object filtert.</span><span class="sxs-lookup"><span data-stu-id="2ddae-124">You can also use a function that filters the object.</span></span>  <span data-ttu-id="2ddae-125">In dit geval wordt de `this`-variabele toegewezen aan het huidige object dat wordt gefilterd.</span><span class="sxs-lookup"><span data-stu-id="2ddae-125">In this case, the `this` variable is assigned to the current object being filtered.</span></span>  <span data-ttu-id="2ddae-126">De volgende code is functioneel equivalent aan het vorige voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2ddae-126">The following code is functionally equivalent to the prior example:</span></span>

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <span data-ttu-id="2ddae-127"><a name="table-paging"></a>Door gegevens bladeren</span><span class="sxs-lookup"><span data-stu-id="2ddae-127"><a name="table-paging"></a>Paging through data</span></span>
<span data-ttu-id="2ddae-128">Gebruik de methode `take()` en `skip()`.</span><span class="sxs-lookup"><span data-stu-id="2ddae-128">Utilize the `take()` and `skip()` methods.</span></span>  <span data-ttu-id="2ddae-129">Bijvoorbeeld als u de tabel wilt splitsen in records met 100 rijen:</span><span class="sxs-lookup"><span data-stu-id="2ddae-129">For example, if you wish to split the table into 100-row records:</span></span>

```
var totalCount = 0, pages = 0;

// Step 1 - get the total number of records
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

<span data-ttu-id="2ddae-130">De methode `.includeTotalCount()` wordt gebruikt om een totalCount-veld toe te voegen aan het resultaatobject.</span><span class="sxs-lookup"><span data-stu-id="2ddae-130">The `.includeTotalCount()` method is used to add a totalCount field to the results object.</span></span>  <span data-ttu-id="2ddae-131">Het veld totalCount wordt gevuld met het totale aantal records dat zou worden geretourneerd als er geen paginering zou zijn gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2ddae-131">The totalCount field is filled with the total number of records that would be returned if no paging is used.</span></span>

<span data-ttu-id="2ddae-132">U kunt vervolgens de paginavariabelen en sommige UI-knoppen gebruiken om een paginalijst op te geven; gebruik `loadPage()` om de nieuwe records voor elke pagina te laden.</span><span class="sxs-lookup"><span data-stu-id="2ddae-132">You can then use the pages variable and some UI buttons to provide a page list; use `loadPage()` to load the new records for each page.</span></span>  <span data-ttu-id="2ddae-133">Implementeer caching voor snellere toegang tot de records die al zijn geladen.</span><span class="sxs-lookup"><span data-stu-id="2ddae-133">Implement caching to speed access to records that have already been loaded.</span></span>

#### <span data-ttu-id="2ddae-134"><a name="sorting-data"></a>Procedure: Gesorteerde gegevens retourneren</span><span class="sxs-lookup"><span data-stu-id="2ddae-134"><a name="sorting-data"></a>How to: Return sorted data</span></span>
<span data-ttu-id="2ddae-135">Gebruik de querymethode `.orderBy()` of `.orderByDescending()`:</span><span class="sxs-lookup"><span data-stu-id="2ddae-135">Use the `.orderBy()` or `.orderByDescending()` query methods:</span></span>

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

<span data-ttu-id="2ddae-136">Zie de [Documentatie over queryobjecten] voor meer informatie over het queryobject.</span><span class="sxs-lookup"><span data-stu-id="2ddae-136">For more information on the Query object, see the [Query object documentation].</span></span>

### <span data-ttu-id="2ddae-137"><a name="inserting"></a>Procedure: Gegevens invoegen</span><span class="sxs-lookup"><span data-stu-id="2ddae-137"><a name="inserting"></a>How to: Insert data</span></span>
<span data-ttu-id="2ddae-138">Maak een JavaScript-object met de juiste datum en roep `table.insert()` asynchroon aan:</span><span class="sxs-lookup"><span data-stu-id="2ddae-138">Create a JavaScript object with the appropriate date and call `table.insert()` asynchronously:</span></span>

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

<span data-ttu-id="2ddae-139">Wanneer het invoegen is geslaagd, wordt het ingevoegde item geretourneerd met de aanvullende velden die vereist zijn voor synchronisatiebewerkingen.</span><span class="sxs-lookup"><span data-stu-id="2ddae-139">On successful insertion, the inserted item is returned with the additional fields that are required for sync operations.</span></span>  <span data-ttu-id="2ddae-140">Werk uw eigen cache bij met deze gegevens voor latere updates.</span><span class="sxs-lookup"><span data-stu-id="2ddae-140">Update your own cache with this information for later updates.</span></span>

<span data-ttu-id="2ddae-141">De Azure Mobile Apps Node.js Server SDK biedt ondersteuning voor dynamische schema's voor ontwikkelingsdoeleinden.</span><span class="sxs-lookup"><span data-stu-id="2ddae-141">The Azure Mobile Apps Node.js Server SDK supports dynamic schema for development purposes.</span></span>  <span data-ttu-id="2ddae-142">Met een dynamisch schema kunt u kolommen toevoegen aan de tabel door deze op te geven in een Insert- of Update-bewerking.</span><span class="sxs-lookup"><span data-stu-id="2ddae-142">Dynamic Schema allows you to add columns to the table by specifying them in an insert or update operation.</span></span>  <span data-ttu-id="2ddae-143">We raden u aan het dynamische schema uit te schakelen voordat u uw toepassing in productie neemt.</span><span class="sxs-lookup"><span data-stu-id="2ddae-143">We recommend that you turn off dynamic schema before moving your application to production.</span></span>

### <span data-ttu-id="2ddae-144"><a name="modifying"></a>Procedure: Gegevens wijzigen</span><span class="sxs-lookup"><span data-stu-id="2ddae-144"><a name="modifying"></a>How to: Modify data</span></span>
<span data-ttu-id="2ddae-145">Net als bij de methode `.insert()` moet u een Update-object maken en vervolgens `.update()` aanroepen.</span><span class="sxs-lookup"><span data-stu-id="2ddae-145">Similar to the `.insert()` method, you should create an Update object and then call `.update()`.</span></span>  <span data-ttu-id="2ddae-146">Het Update-object moet de id van het bij te werken record bevatten: de id wordt verkregen tijdens het lezen van het record of het aanroepen van `.insert()`.</span><span class="sxs-lookup"><span data-stu-id="2ddae-146">The update object must contain the ID of the record to be updated - the ID is obtained when reading the record or when calling `.insert()`.</span></span>

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

### <span data-ttu-id="2ddae-147"><a name="deleting"></a>Procedure: Gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="2ddae-147"><a name="deleting"></a>How to: Delete data</span></span>
<span data-ttu-id="2ddae-148">Roep de methode `.del()` aan als u een record wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2ddae-148">To delete a record, call the `.del()` method.</span></span>  <span data-ttu-id="2ddae-149">Geef de id door in een objectverwijzing:</span><span class="sxs-lookup"><span data-stu-id="2ddae-149">Pass the ID in an object reference:</span></span>

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
