## <span data-ttu-id="9e9dd-101"><a name="create-client"></a>Een clientverbinding maken</span><span class="sxs-lookup"><span data-stu-id="9e9dd-101"><a name="create-client"></a>Create a client connection</span></span>
<span data-ttu-id="9e9dd-102">Maak een clientverbinding door een `WindowsAzure.MobileServiceClient`-object te maken.</span><span class="sxs-lookup"><span data-stu-id="9e9dd-102">Create a client connection by creating a `WindowsAzure.MobileServiceClient` object.</span></span>  <span data-ttu-id="9e9dd-103">Vervang `appUrl` met de URL tooyour mobiele App.</span><span class="sxs-lookup"><span data-stu-id="9e9dd-103">Replace `appUrl` with the URL tooyour Mobile App.</span></span>

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <span data-ttu-id="9e9dd-104"><a name="table-reference"></a>Werken met tabellen</span><span class="sxs-lookup"><span data-stu-id="9e9dd-104"><a name="table-reference"></a>Work with tables</span></span>
<span data-ttu-id="9e9dd-105">tooaccess of update gegevens, maken een verwijzing toohello back-end-tabel.</span><span class="sxs-lookup"><span data-stu-id="9e9dd-105">tooaccess or update data, create a reference toohello backend table.</span></span> <span data-ttu-id="9e9dd-106">Vervang `tableName` met de naam van de tabel Hallo</span><span class="sxs-lookup"><span data-stu-id="9e9dd-106">Replace `tableName` with hello name of your table</span></span>

```
var table = client.getTable(tableName);
```

<span data-ttu-id="9e9dd-107">Wanneer u een tabelverwijzing hebt, kunt u verder werken aan uw tabel:</span><span class="sxs-lookup"><span data-stu-id="9e9dd-107">Once you have a table reference, you can work further with your table:</span></span>

* [<span data-ttu-id="9e9dd-108">Een query uitvoeren op een tabel</span><span class="sxs-lookup"><span data-stu-id="9e9dd-108">Query a Table</span></span>](#querying)
  * [<span data-ttu-id="9e9dd-109">Gegevens filteren</span><span class="sxs-lookup"><span data-stu-id="9e9dd-109">Filtering Data</span></span>](#table-filter)
  * [<span data-ttu-id="9e9dd-110">Door gegevens bladeren</span><span class="sxs-lookup"><span data-stu-id="9e9dd-110">Paging through Data</span></span>](#table-paging)
  * [<span data-ttu-id="9e9dd-111">Gegevens sorteren</span><span class="sxs-lookup"><span data-stu-id="9e9dd-111">Sorting Data</span></span>](#sorting-data)
* [<span data-ttu-id="9e9dd-112">Gegevens invoegen</span><span class="sxs-lookup"><span data-stu-id="9e9dd-112">Inserting Data</span></span>](#inserting)
* [<span data-ttu-id="9e9dd-113">Gegevens wijzigen</span><span class="sxs-lookup"><span data-stu-id="9e9dd-113">Modifying Data</span></span>](#modifying)
* [<span data-ttu-id="9e9dd-114">Gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="9e9dd-114">Deleting Data</span></span>](#deleting)

### <span data-ttu-id="9e9dd-115"><a name="querying"></a>Procedure: Een query uitvoeren op een tabelverwijzing</span><span class="sxs-lookup"><span data-stu-id="9e9dd-115"><a name="querying"></a>How to: Query a table reference</span></span>
<span data-ttu-id="9e9dd-116">Zodra u een tabelverwijzing hebt, kunt u dit tooquery gebruiken voor gegevens op Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="9e9dd-116">Once you have a table reference, you can use it tooquery for data on hello server.</span></span>  <span data-ttu-id="9e9dd-117">Query's worden gemaakt in een LINQ-achtige taal.</span><span class="sxs-lookup"><span data-stu-id="9e9dd-117">Queries are made in a "LINQ-like" language.</span></span>
<span data-ttu-id="9e9dd-118">tooreturn alle gegevens van de tabel hello, gebruik Hallo volgende code:</span><span class="sxs-lookup"><span data-stu-id="9e9dd-118">tooreturn all data from hello table, use hello following code:</span></span>

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

<span data-ttu-id="9e9dd-119">Hallo geslaagd functie is aangeroepen met Hallo resultaten.</span><span class="sxs-lookup"><span data-stu-id="9e9dd-119">hello success function is called with hello results.</span></span>  <span data-ttu-id="9e9dd-120">Gebruik geen `for (var i in results)` in Hallo geslaagd werkt zoals die wordt herhaald over informatie die is opgenomen in de resultaten Hallo wanneer andere queryfuncties (zoals `.includeTotalCount()`) worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9e9dd-120">Do not use `for (var i in results)` in hello success function as that will iterate over information that is included in hello results when other query functions (such as `.includeTotalCount()`) are used.</span></span>

<span data-ttu-id="9e9dd-121">Zie voor meer informatie over Hallo querysyntaxis Hallo [object Querydocumentatie].</span><span class="sxs-lookup"><span data-stu-id="9e9dd-121">For more information on hello Query syntax, see hello [Query object documentation].</span></span>

#### <span data-ttu-id="9e9dd-122"><a name="table-filter"></a>Filteren van gegevens op Hallo-server</span><span class="sxs-lookup"><span data-stu-id="9e9dd-122"><a name="table-filter"></a>Filtering data on hello server</span></span>
<span data-ttu-id="9e9dd-123">U kunt een `where` component op Hallo tabelverwijzing:</span><span class="sxs-lookup"><span data-stu-id="9e9dd-123">You can use a `where` clause on hello table reference:</span></span>

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

<span data-ttu-id="9e9dd-124">U kunt ook een functie die Hallo object filtert gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9e9dd-124">You can also use a function that filters hello object.</span></span>  <span data-ttu-id="9e9dd-125">In dit geval Hallo `this` variabele toothe huidige object replicatiefilterprocedure is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="9e9dd-125">In this case, hello `this` variable is assigned toothe current object being filtered.</span></span>  <span data-ttu-id="9e9dd-126">Hallo na de code is functioneel equivalent toohello voorafgaande voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9e9dd-126">hello following code is functionally equivalent toohello prior example:</span></span>

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <span data-ttu-id="9e9dd-127"><a name="table-paging"></a>Door gegevens bladeren</span><span class="sxs-lookup"><span data-stu-id="9e9dd-127"><a name="table-paging"></a>Paging through data</span></span>
<span data-ttu-id="9e9dd-128">Gebruikmaken van Hallo `take()` en `skip()` methoden.</span><span class="sxs-lookup"><span data-stu-id="9e9dd-128">Utilize hello `take()` and `skip()` methods.</span></span>  <span data-ttu-id="9e9dd-129">Bijvoorbeeld, u kunt eventueel toosplit Hallo tabel in de rij 100 records:</span><span class="sxs-lookup"><span data-stu-id="9e9dd-129">For example, if you wish toosplit hello table into 100-row records:</span></span>

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

<span data-ttu-id="9e9dd-130">Hallo `.includeTotalCount()` methode gebruikte tooadd een totalCount veld toohello results-object is.</span><span class="sxs-lookup"><span data-stu-id="9e9dd-130">hello `.includeTotalCount()` method is used tooadd a totalCount field toohello results object.</span></span>  <span data-ttu-id="9e9dd-131">Het veld totalCount wordt gevuld met Hallo kunt u het totale aantal records dat wordt geretourneerd als geen paginering wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9e9dd-131">The totalCount field is filled with hello total number of records that would be returned if no paging is used.</span></span>

<span data-ttu-id="9e9dd-132">U kunt Hallo pagina's variabele en sommige UI knoppen tooprovide een paginalijst. Gebruik `loadPage()` Hallo nieuwe records voor elke pagina te laden.</span><span class="sxs-lookup"><span data-stu-id="9e9dd-132">You can then use hello pages variable and some UI buttons tooprovide a page list; use `loadPage()` to load hello new records for each page.</span></span>  <span data-ttu-id="9e9dd-133">Implementeren in het cachegeheugen toospeed toegang toorecords die al zijn geladen.</span><span class="sxs-lookup"><span data-stu-id="9e9dd-133">Implement caching toospeed access toorecords that have already been loaded.</span></span>

#### <span data-ttu-id="9e9dd-134"><a name="sorting-data"></a>Procedure: Gesorteerde gegevens retourneren</span><span class="sxs-lookup"><span data-stu-id="9e9dd-134"><a name="sorting-data"></a>How to: Return sorted data</span></span>
<span data-ttu-id="9e9dd-135">Gebruik Hallo `.orderBy()` of `.orderByDescending()` query methoden:</span><span class="sxs-lookup"><span data-stu-id="9e9dd-135">Use hello `.orderBy()` or `.orderByDescending()` query methods:</span></span>

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

<span data-ttu-id="9e9dd-136">Zie voor meer informatie over het queryobject Hallo Hallo [object Querydocumentatie].</span><span class="sxs-lookup"><span data-stu-id="9e9dd-136">For more information on hello Query object, see hello [Query object documentation].</span></span>

### <span data-ttu-id="9e9dd-137"><a name="inserting"></a>Procedure: Gegevens invoegen</span><span class="sxs-lookup"><span data-stu-id="9e9dd-137"><a name="inserting"></a>How to: Insert data</span></span>
<span data-ttu-id="9e9dd-138">Een JavaScript-object maken met de juiste datum Hallo en aanroep `table.insert()` asynchroon:</span><span class="sxs-lookup"><span data-stu-id="9e9dd-138">Create a JavaScript object with hello appropriate date and call `table.insert()` asynchronously:</span></span>

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

<span data-ttu-id="9e9dd-139">Op geslaagde invoegen Hallo ingevoegd item geretourneerd met de Hallo aanvullende velden die vereist voor synchronisatiebewerkingen zijn.</span><span class="sxs-lookup"><span data-stu-id="9e9dd-139">On successful insertion, hello inserted item is returned with hello additional fields that are required for sync operations.</span></span>  <span data-ttu-id="9e9dd-140">Werk uw eigen cache bij met deze gegevens voor latere updates.</span><span class="sxs-lookup"><span data-stu-id="9e9dd-140">Update your own cache with this information for later updates.</span></span>

<span data-ttu-id="9e9dd-141">Hello Azure Mobile Apps-Node.js-SDK biedt ondersteuning voor dynamische-schema voor ontwikkelingsdoeleinden.</span><span class="sxs-lookup"><span data-stu-id="9e9dd-141">hello Azure Mobile Apps Node.js Server SDK supports dynamic schema for development purposes.</span></span>  <span data-ttu-id="9e9dd-142">Dynamische Schema kunt u tooadd kolommen toohello tabel in een bewerking insert of update opgeven.</span><span class="sxs-lookup"><span data-stu-id="9e9dd-142">Dynamic Schema allows you tooadd columns toohello table by specifying them in an insert or update operation.</span></span>  <span data-ttu-id="9e9dd-143">U wordt aangeraden dat u dynamische schema uitschakelen voordat u uw toepassing tooproduction verplaatst.</span><span class="sxs-lookup"><span data-stu-id="9e9dd-143">We recommend that you turn off dynamic schema before moving your application tooproduction.</span></span>

### <span data-ttu-id="9e9dd-144"><a name="modifying"></a>Procedure: Gegevens wijzigen</span><span class="sxs-lookup"><span data-stu-id="9e9dd-144"><a name="modifying"></a>How to: Modify data</span></span>
<span data-ttu-id="9e9dd-145">Vergelijkbare toohello `.insert()` methode die u moet een Update-object maken en vervolgens aanroepen `.update()`.</span><span class="sxs-lookup"><span data-stu-id="9e9dd-145">Similar toohello `.insert()` method, you should create an Update object and then call `.update()`.</span></span>  <span data-ttu-id="9e9dd-146">Hallo update object mag Hallo-ID van de record toobe Hallo bijgewerkt - Hallo-ID is verkregen tijdens het lezen van Hallo record of bij het aanroepen van `.insert()`.</span><span class="sxs-lookup"><span data-stu-id="9e9dd-146">hello update object must contain hello ID of hello record toobe updated - hello ID is obtained when reading hello record or when calling `.insert()`.</span></span>

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

### <span data-ttu-id="9e9dd-147"><a name="deleting"></a>Procedure: Gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="9e9dd-147"><a name="deleting"></a>How to: Delete data</span></span>
<span data-ttu-id="9e9dd-148">toodelete een record aanroep Hallo `.del()` methode.</span><span class="sxs-lookup"><span data-stu-id="9e9dd-148">toodelete a record, call hello `.del()` method.</span></span>  <span data-ttu-id="9e9dd-149">Hallo-ID doorgeven in een objectverwijzing:</span><span class="sxs-lookup"><span data-stu-id="9e9dd-149">Pass hello ID in an object reference:</span></span>

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
