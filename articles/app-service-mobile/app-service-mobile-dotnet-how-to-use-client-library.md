---
title: aaaWorking Hello App Service Mobile Apps-clientbibliotheek beheerd (Windows | Microsoft Docs
description: Meer informatie over hoe toouse een .NET-client voor Azure App Service Mobile Apps met Windows en Xamarin-apps.
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0280785c-e027-4e0d-aaf2-6f155e5a6197
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 01/04/2017
ms.author: glenga
ms.openlocfilehash: b056e606b19406398f5b6faabb0931ad651125e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-managed-client-for-azure-mobile-apps"></a>Hoe toouse Hallo-client voor mobiele Apps van Azure beheerd
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a>Overzicht
Deze handleiding wordt getoond hoe tooperform algemene scenario's met behulp van Hallo-clientbibliotheek voor apps in Azure App Service Mobile Apps voor Windows en Xamarin beheerd. Als u nieuwe tooMobile Apps, moet u eerst voltooit Hallo [Azure Mobile Apps Quick Start] [ 1] zelfstudie. In deze handleiding we richten op Hallo clientzijde beheerd SDK. informatie over hello serverzijde SDK's voor mobiele Apps, Zie Hallo-documentatie voor Hallo toolearn [.NET Server SDK] [ 2] of de [Node.js Server SDK] [ 3].

## <a name="reference-documentation"></a>Referentiedocumentatie
Hallo-naslagdocumentatie voor Hallo client SDK bevindt zich hier: [referentie voor Azure Mobile Apps .NET client][4].
U vindt ook enkele voorbeelden van de client in Hallo [Azure-Samples GitHub-opslagplaats][5].

## <a name="supported-platforms"></a>Ondersteunde Platforms
Hallo .NET-Platform ondersteunt Hallo volgende platforms:

* Xamarin Android-versies voor API-19 tot en met 24 (KitKat via deze)
* Xamarin iOS-versies voor iOS 8.0 en hoger
* Universele Windows-Platform
* Windows Phone 8.1
* Windows Phone 8.0, met uitzondering van Silverlight-toepassingen

Hallo 'server-flow' verificatie maakt gebruik van een webweergave voor Hallo gebruikersinterface weergegeven.  Als Hallo apparaat niet kunt toopresent een WebView UI, er zijn andere methoden voor verificatie nodig.  Deze SDK is derhalve niet geschikt voor controle-type of op dezelfde manier beperkte apparaten.

## <a name="setup"></a>Het installatieprogramma en vereisten
Er wordt ervan uitgegaan dat u hebt al gemaakt en gepubliceerd van uw mobiele App back-end-project, waaronder ten minste één tabel.  In het Hallo-code die wordt gebruikt in dit onderwerp, Hallo tabel heet `TodoItem` en of hieraan Hallo volgende kolommen: `Id`, `Text`, en `Complete`. Deze tabel is Hallo dezelfde tabel gemaakt wanneer u voltooit de [Azure Mobile Apps Quick Start][1].

Hallo corresponderende getypte clientzijde type in C# is Hallo klasse te volgen:

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }
}
```

Hallo [JsonPropertyAttribute] [ 6] gebruikte toodefine Hallo is *PropertyName* toewijzing tussen Hallo client velden en Hallo tabel.

toolearn hoe toocreate tabellen in uw Mobile Apps back-end, Zie Hallo [onderwerp SDK voor .NET-Server] [ 7] of Hallo [Node.js Server SDK onderwerp] [ 8] . Als u uw back-end voor de mobiele App gemaakt in hello Azure portal met behulp van Hallo Quick Start, kunt u ook Hallo **gemakkelijk tabellen** instellen in Hallo [Azure-portal].

### <a name="how-to-install-hello-managed-client-sdk-package"></a>Hoe: installatie Hallo beheerde client SDK-pakket
Gebruik een van de volgende methoden tooinstall Hallo Hallo beheerde client SDK-pakket voor mobiele Apps van [NuGet][9]:

* **Visual Studio** met de rechtermuisknop op uw project, klikt u op **NuGet-pakketten beheren**, zoekt u Hallo `Microsoft.Azure.Mobile.Client` van het pakket en klik vervolgens op **installeren**.
* **Xamarin Studio** met de rechtermuisknop op uw project, klikt u op **toevoegen** > **NuGet-pakketten toevoegen**, zoekt u Hallo `Microsoft.Azure.Mobile.Client `van het pakket en klik vervolgens op **toevoegen Pakket**.

In het bestand hoofdactiviteit Onthoud tooadd Hallo volgende **met** instructie:

```
using Microsoft.WindowsAzure.MobileServices;
```

### <a name="symbolsource"></a>Procedure: werken met symbolen in Visual Studio
Hallo symbolen voor Hallo Microsoft.Azure.Mobile naamruimte zijn beschikbaar op [SymbolSource][10].  Raadpleeg toothe [SymbolSource instructies] [ 11] toointegrate SymbolSource met Visual Studio.

## <a name="create-client"></a>Hallo Mobile Apps-client maken
Hallo volgende code maakt Hallo [MobileServiceClient] [ 12] -object dat is gebruikt tooaccess backend voor mobiele Apps.

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

Vervang in Hallo voorafgaand aan code, `MOBILE_APP_URL` met Hallo-URL van back-end van Hallo Mobile Apps, die is gevonden in de blade voor uw back-end voor mobiele App in Hallo [Azure-portal]. Hallo MobileServiceClient object moet een singleton.

## <a name="work-with-tables"></a>Werken met tabellen
Hallo hoe volgende van de sectie details toosearch records ophalen en Hallo gegevens binnen Hallo tabel wijzigen.  Hallo volgende onderwerpen komen aan bod:

* [De tabelverwijzing van een maken](#instantiating)
* [Opvragen van gegevens](#querying)
* [Geretourneerde gegevens filteren](#filtering)
* [Geretourneerde gegevens sorteren](#sorting)
* [Gegevens weergeven op pagina 's](#paging)
* [Selecteer specifieke kolommen](#selecting)
* [Een record door-Id niet opzoeken](#lookingup)
* [Omgaan met niet-getypeerde query 's](#untypedqueries)
* [Gegevens invoegen](#inserting)
* [Bijwerken van gegevens](#updating)
* [Verwijderen van gegevens](#deleting)
* [Conflictoplossing en optimistische gelijktijdigheid](#optimisticconcurrency)
* [Binding tooa Windows-gebruikersinterface](#binding)
* [Hallo paginagrootte wijzigen](#pagesize)

### <a name="instantiating"></a>Procedure: een tabelverwijzing maken
Alle Hallo-code die toegang heeft tot of gegevens wijzigt in een tabel van de back-end-functies aanroepen op Hallo `MobileServiceTable` object. Een toohello verwijzingstabel verkrijgen door de aanroepende Hallo [GetTable] methode als volgt:

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

Hallo geretourneerd object maakt gebruik van Hallo getypte serialisatie. Een model met niet-getypeerde serialisatie wordt ook ondersteund. Het volgende voorbeeld [maakt u een niet-getypeerde tabel tooan]:

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

In niet-getypeerde query's, moet u Hallo onderliggende OData-query-tekenreeks.

### <a name="querying"></a>Procedure: een Query over gegevens van uw mobiele App
Deze sectie wordt beschreven hoe tooissue backend voor mobiele Apps toohello, waaronder de volgende functionaliteit Hallo query:

* [Geretourneerde gegevens filteren](#filtering)
* [Geretourneerde gegevens sorteren](#sorting)
* [Gegevens weergeven op pagina 's](#paging)
* [Selecteer specifieke kolommen](#selecting)
* [Opzoeken van gegevens door-ID](#lookingup)

> [!NOTE]
> Een server aangestuurde paginaformaat is afgedwongen tooprevent alle rijen worden geretourneerd.  Standaard-aanvragen voor grote gegevenssets houdt paginering Hallo service negatief beïnvloeden.  tooreturn meer dan 50 rijen gebruiken Hallo `Skip` en `Take` methode, zoals beschreven in [gegevens retourneren op pagina's](#paging).

### <a name="filtering"></a>Hoe: Filter gegevens geretourneerd
Hallo volgende code laat zien hoe gegevens door te nemen toofilter een `Where` -component in een query. Deze retourneert alle items uit `todoTable` waarvan `Complete` eigenschap is gelijk te`false`. Hallo [waar] functie is van toepassing een rij predicaat Hallo-query op Hallo tabel filteren.

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

U kunt Hallo URI van aanvraag verzonden toohello back-end van Hallo weergeven met behulp van bericht inspectie software, zoals browser ontwikkelhulpprogramma's of [Fiddler]. Als u Hallo aanvraag-URI bekijkt, ziet u dat de queryreeks Hallo is gewijzigd:

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

Deze OData-aanvraag wordt omgezet in een SQL-query door Hallo Server SDK:

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

de functie die wordt doorgegeven toohello Hallo `Where` methode een willekeurig aantal voorwaarden kan hebben.

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

In dit voorbeeld zou worden vertaald naar een SQL-query door Hallo Server SDK:

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

Deze query kan ook worden gesplitst in meerdere componenten:

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

Hallo twee methoden zijn equivalent en door elkaar worden gebruikt.  Hallo voormalige optie&mdash;van meerdere predicaten in één query cookievalidatie&mdash;is compact en aanbevolen.

Hallo `Where` component ondersteunt bewerkingen die worden vertaald naar Hallo OData subset. Bewerkingen zijn onder andere:

* Relationele operators (==,! =, <, < =, >, > =),
* Rekenkundige operatoren (+, -, /, *, %),
* Number precision (Math.Floor, Math.Ceiling)
* Tekenreeks-functies (lengte, subtekenreeks, vervangen, IndexOf, StartsWith, EndsWith)
* Datumeigenschappen (jaar, maand, dag, uur, minuut, seconde)
* Toegang tot de eigenschappen van een object, en
* Expressies combineren van deze bewerkingen.

Wanneer u in overweging wat Hallo Server SDK ondersteunt, zou u kunnen Hallo [OData v3 documentatie].

### <a name="sorting"></a>Hoe: sorteren gegevens geretourneerd
Hallo volgende code laat zien hoe gegevens door te nemen toosort een [OrderBy] of [OrderByDescending] functie in Hallo-query. Deze items uit retourneert `todoTable` gesorteerd door Hallo oplopende `Text` veld.

```
// Sort items in ascending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderBy(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();

// Sort items in descending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderByDescending(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();
```

### <a name="paging"></a>Procedure: gegevens retourneren op pagina's
Standaard Hallo back-end van alleen Hallo eerste 50 rijen geretourneerd. U kunt het aantal geretourneerde rijen Hallo vergroten door aanroepen Hallo [nemen] methode. Gebruik `Take` samen met de Hallo [overslaan] methode toorequest een bepaalde 'pagina' van de totale gegevensset Hallo geretourneerd door Hallo-query. Hallo retourneert volgende tijdens de uitvoering van query Hallo drie belangrijkste items in de tabel Hallo.

```
// Define a filtered query that returns hello top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

Hallo volgende slaat het gereviseerde query Hallo eerste drie resultaten en retourneert de volgende drie resultaten Hallo. Deze query produceert tweede Hallo 'pagina"gegevens, waarbij de paginagrootte Hallo drie items is.

```
// Define a filtered query that skips hello top 3 items and returns hello next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

Hallo [IncludeTotalCount] Hallo totale aantal voor aanvragen voor methode *alle* Hallo records die zou zijn geretourneerd, eventuele opgegeven paginering/limiet-component wordt genegeerd:

```
query = query.IncludeTotalCount();
```

In werkelijkheid-app kunt u query's vergelijkbaar toohello voorgaande voorbeeld met een pagineringsbesturingselement of een vergelijkbare UI navigeren tussen pagina's.

> [!NOTE]
> toooverride hello 50-Rijlimiet in een back-end voor de mobiele App, moet u ook Hallo toepassen [EnableQueryAttribute] toohello openbare methode GET en Hallo paginering gedrag opgeven. Toegepaste toohello methode Hallo na ingesteld wanneer het maximum aantal geretourneerde rijen too1000:
>
> `[EnableQuery(MaxTop=1000)]`


### <a name="selecting"></a>Hoe: specifieke kolommen selecteren
U kunt opgeven welke set eigenschappen tooinclude in Hallo resulteert door toe te voegen een [Selecteer] component tooyour query. Bijvoorbeeld, Hallo volgende code wordt getoond hoe tooselect één veld en ook hoe tooselect en formatteren van meerdere velden:

```
// Select one field -- just hello Text
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => todoItem.Text);
List<string> items = await query.ToListAsync();

// Select multiple fields -- both Complete and Text info
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => string.Format("{0} -- {1}",
                    todoItem.Text.PadRight(30), todoItem.Complete ?
                    "Now complete!" : "Incomplete!"));
List<string> items = await query.ToListAsync();
```

Alle functies beschreven dusver Hallo additieve, zodat we kunt houden chaining ze zijn. Elke aanroep van de keten is van invloed op meer Hallo-query. Een voorbeeld van meer:

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <a name="lookingup"></a>Hoe: opzoeken van gegevens door-ID
Hallo [LookupAsync] functie gebruikte toolook objecten uit de database met een bepaalde ID. Hallo kan zijn

```
// This query filters out hello item with hello ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <a name="untypedqueries"></a>Hoe: niet-getypeerde query's uitvoeren
Bij het uitvoeren van een query met een niet-getypeerde tabelobject moet u expliciet Hallo OData-query-tekenreeks opgeven door het aanroepen van [ReadAsync], Hallo voorbeeld te volgen:

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

U terughalen JSON-waarden die u, zoals een eigenschappenverzameling gebruiken kunt. Zie voor meer informatie over JToken en Newtonsoft Json.NET hello [Json.NET] site.

### <a name="inserting"></a>Procedure: gegevens invoegen in een back-end voor de mobiele App
Alle clienttypen moeten bevatten een lid genaamd **Id**, dit is standaard een tekenreeks. Dit **Id** CRUD-bewerkingen uit te voeren is vereist en voor het offline synchroniseren. Hallo volgende code laat zien hoe toouse hello [InsertAsync] methode tooinsert nieuwe rijen in een tabel. Hallo-parameter bevat Hallo gegevens toobe ingevoegd als .NET-object.

```
await todoTable.InsertAsync(todoItem);
```

Als een unieke aangepaste ID-waarde niet is opgenomen in Hallo `todoItem` tijdens een insert-, een GUID wordt gegenereerd door Hallo-server.
U kunt ophalen Hallo Id gegenereerd door het Hallo-object te bekijken nadat Hallo aanroep retourneert.

tooinsert getypeerde gegevens, kunt u profiteren van Json.NET:

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

Hier volgt een voorbeeld van een e-mailadres als een unieke tekenreeks-id:

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a>Werken met de id-waarden
Mobile Apps ondersteunt unieke aangepaste tekenreekswaarden voor van Hallo tabel **id** kolom. Een string-waarde zorgt ervoor dat toepassingen toouse aangepaste waarden zoals e-mailadressen of gebruikersnamen voor Hallo-ID.  Tekenreeks-id's bieden u Hallo volgende voordelen:

* Id's worden zonder dat een round trip toohello database gegenereerd.
* Records zijn eenvoudiger toomerge uit verschillende tabellen of databases.
* Id-waarden kunnen beter geïntegreerd met een toepassing logica.

Wanneer de waarde van een tekenreeks-ID niet is ingesteld op een ingevoegde record, backend voor mobiele Apps hello wordt gegenereerd voor een unieke waarde voor de ID. U kunt Hallo [Guid.NewGuid] methode toogenerate uw eigen ID-, op Hallo-client of in Hallo back-end waarden.

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <a name="modifying"></a>Procedure: gegevens wijzigen in een back-end voor de mobiele App
Hallo volgende code laat zien hoe toouse hello [UpdateAsync] methode tooupdate een bestaande record met Hallo met dezelfde ID met nieuwe informatie. Hallo-parameter bevat Hallo gegevens toobe bijgewerkt als .NET-object.

```
await todoTable.UpdateAsync(todoItem);
```

tooupdate getypeerde gegevens, kunt u profiteren van [Json.NET] als volgt:

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

Een `id` veld moet worden opgegeven bij het maken van een update. Hallo back-end gebruikt Hallo `id` veld tooidentify die tooupdate rij. Hallo `id` veld kan worden verkregen van Hallo resultaat Hallo `InsertAsync` aanroepen. Een `ArgumentException` treedt op als u een item tooupdate probeert zonder Hallo `id` waarde.

### <a name="deleting"></a>Hoe: verwijderen van gegevens in een back-end voor de mobiele App
Hallo volgende code laat zien hoe toouse hello [DeleteAsync] methode toodelete een bestaand exemplaar. Hallo-exemplaar wordt geïdentificeerd door Hallo `id` veld is ingesteld op Hallo `todoItem`.

```
await todoTable.DeleteAsync(todoItem);
```

toodelete getypeerde gegevens, u kunt profiteren van Json.NET als volgt:

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

Wanneer u een aanvraag verwijderen, moet een ID worden opgegeven. Andere eigenschappen toohello service niet worden doorgegeven of worden genegeerd op Hallo-service. Hallo resultaat van een `DeleteAsync` aanroep is meestal `null`. Hallo-ID toopass in kunnen worden verkregen van Hallo resultaat Hallo `InsertAsync` aanroepen. Een `MobileServiceInvalidOperationException` wordt gegenereerd wanneer u een item toodelete probeert zonder op te geven Hallo `id` veld.

### <a name="optimisticconcurrency"></a>Hoe: gebruikt optimistische gelijktijdigheid voor conflictoplossing
Twee of meer clients kunnen schrijven van wijzigingen toohello dezelfde item op Hallo dezelfde tijd. Zonder conflictdetectie overschrijft Hallo laatste schrijven alle vorige updates. **Optimistisch gelijktijdigheidbeheer** wordt ervan uitgegaan dat elke transactie kan worden doorgevoerd en daarom geen vergrendeling van elke resource gebruikt.  Voordat u een transactie doorvoert, controleert Optimistisch gelijktijdigheidbeheer of dat er geen andere transactie Hallo gegevens is gewijzigd. Als Hallo gegevens is gewijzigd, is Hallo vastleggen van de transactie teruggedraaid.

Mobiele Apps biedt ondersteuning voor Optimistisch gelijktijdigheidbeheer door het bijhouden van wijzigingen tooeach item Hallo met `version` systeemkolom eigenschap die is gedefinieerd voor elke tabel in uw back-end voor de mobiele App. Telkens wanneer een record is bijgewerkt, Mobile Apps ingesteld Hallo `version` eigenschap voor dat de nieuwe waarde tooa vastleggen. Tijdens elke updateaanvraag Hallo `version` eigenschap van het Hallo-record die deel uitmaakt van het Hallo-aanvraag is vergeleken toohello dezelfde eigenschap voor Hallo record op Hallo-server. Als de versie die is doorgegeven met Hallo-aanvraag komt niet overeen met de Hallo back-end en vervolgens Hallo-clientbibliotheek genereert een `MobileServicePreconditionFailedException<T>` uitzondering. Hallo-type opgenomen met de Hallo uitzondering is Hallo-record van Hallo back-end met Hallo servers versie van het Hallo-record. Hallo toepassing kan vervolgens worden gebruikt deze informatie toodecide of tooexecute Hallo updateaanvraag opnieuw met de juiste Hallo `version` waarde van Hallo back-end toocommit wijzigingen.

Een kolom definiëren op Hallo tabel klasse voor Hallo `version` system eigenschap tooenable optimistische gelijktijdigheid. Bijvoorbeeld:

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }

    // *** Enable Optimistic Concurrency *** //
    [JsonProperty(PropertyName = "version")]
    public string Version { set; get; }
}
```

Toepassingen die gebruikmaken van niet-getypeerde tabellen optimistische gelijktijdigheid inschakelen door de instelling Hallo `Version` vlag op de `SystemProperties` Hallo tabel als volgt.

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

In aanvulling tooenabling optimistische gelijktijdigheid, moet u ook Hallo catch `MobileServicePreconditionFailedException<T>` uitzondering in uw code bij het aanroepen van [UpdateAsync].  Hallo conflict oplossen door toe te passen Hallo juist `version` toothe bijgewerkt record en aanroep [UpdateAsync] Hello opgelost record. Hallo volgende code toont hoe tooresolve een schrijfconflict eenmaal gedetecteerd:

```
private async void UpdateToDoItem(TodoItem item)
{
    MobileServicePreconditionFailedException<TodoItem> exception = null;

    try
    {
        //update at hello remote table
        await todoTable.UpdateAsync(item);
    }
    catch (MobileServicePreconditionFailedException<TodoItem> writeException)
    {
        exception = writeException;
    }

    if (exception != null)
    {
        // Conflict detected, hello item has changed since hello last query
        // Resolve hello conflict between hello local and server item
        await ResolveConflict(item, exception.Item);
    }
}


private async Task ResolveConflict(TodoItem localItem, TodoItem serverItem)
{
    //Ask user toochoose hello resoltion between versions
    MessageDialog msgDialog = new MessageDialog(
        String.Format("Server Text: \"{0}\" \nLocal Text: \"{1}\"\n",
        serverItem.Text, localItem.Text),
        "CONFLICT DETECTED - Select a resolution:");

    UICommand localBtn = new UICommand("Commit Local Text");
    UICommand ServerBtn = new UICommand("Leave Server Text");
    msgDialog.Commands.Add(localBtn);
    msgDialog.Commands.Add(ServerBtn);

    localBtn.Invoked = async (IUICommand command) =>
    {
        // tooresolve hello conflict, update hello version of hello item being committed. Otherwise, you will keep
        // catching a MobileServicePreConditionFailedException.
        localItem.Version = serverItem.Version;

        // Updating recursively here just in case another change happened while hello user was making a decision
        UpdateToDoItem(localItem);
    };

    ServerBtn.Invoked = async (IUICommand command) =>
    {
        RefreshTodoItems();
    };

    await msgDialog.ShowAsync();
}
```

Zie voor meer informatie, Hallo [Offline synchroniseren van gegevens in Azure Mobile Apps] onderwerp.

### <a name="binding"></a>Hoe: Bind Mobile Apps gegevens tooa Windows-gebruikersinterface
Deze sectie wordt beschreven hoe toodisplay geretourneerd met behulp van UI-elementen in een Windows-app-gegevensobjecten.  De volgende voorbeeldcode wordt gebonden toohello bron van Hallo lijst met een query voor onvolledige items. De [MobileServiceCollection] maakt een mobiele Apps-bewuste binding-verzameling.

```
// This query filters out completed TodoItems.
MobileServiceCollection<TodoItem, TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToCollectionAsync();

// itemsControl is an IEnumerable that could be bound tooa UI list control
IEnumerable itemsControl  = items;

// Bind this tooa ListBox
ListBox lb = new ListBox();
lb.ItemsSource = items;
```

Sommige besturingselementen in Hallo beheerde runtimeondersteuning die een interface aangeroepen [ISupportIncrementalLoading]. Deze interface kunt besturingselementen toorequest extra gegevens wanneer hello wordt geschoven. Er is ingebouwde ondersteuning voor deze interface voor universele Windows-apps via [MobileServiceIncrementalLoadingCollection], die automatisch de aanroepen van Hallo besturingselementen verwerkt. Gebruik `MobileServiceIncrementalLoadingCollection` in Windows-apps als volgt:

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

toouse nieuwe verzameling op Windows Phone 8 en 'Silverlight' apps, gebruik Hallo Hallo `ToCollection` uitbreidingsmethoden op `IMobileServiceTableQuery<T>` en `IMobileServiceTable<T>`. tooload gegevens, roepen `LoadMoreItemsAsync()`.

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

Bij het gebruik van Hallo-verzameling gemaakt door het aanroepen van `ToCollectionAsync` of `ToCollection`, ophalen van een verzameling die gebonden tooUI besturingselementen worden kan.  Deze verzameling is paginering-bewust.  Aangezien Hallo verzameling gegevens worden geladen vanaf het netwerk, soms laden is mislukt. toohandle dergelijke fouten negeren Hallo `OnException` methode op `MobileServiceIncrementalLoadingCollection` toohandle uitzonderingen ten gevolge van aanroepen te`LoadMoreItemsAsync`.

Overweeg als de tabel veel velden heeft, maar u wilt dat alleen toodisplay enkele ervan in het besturingselement. Hallo richtlijnen kunt u in de voorgaande sectie Hallo '[specifieke kolommen selecteren](#selecting)' tooselect specifieke kolommen toodisplay in Hallo gebruikersinterface.

### <a name="pagesize"></a>Wijziging Hallo paginagrootte
Azure Mobile Apps retourneert een maximum van 50 items per aanvraag standaard.  U kunt Hallo paginering grootte wijzigen door het verhogen van de maximale paginagrootte Hallo op Hallo-client en server.  tooincrease Hallo van de grootte van de aangevraagde pagina, geef `PullOptions` bij gebruik van `PullAsync()`:

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

Ervan uitgaande dat u hebt aangebracht Hallo `PageSize` gelijk tooor groter zijn dan 100 binnen Hallo-server een aanvraag maximaal 100 items geretourneerd.

## <a name="#offlinesync"></a>Werken met Offline tabellen
Een lokale SQLite store toostore gegevens offline tabellen gebruiken voor gebruik wanneer u offline bent.  Alle tabel bewerkingen worden uitgevoerd voor Hallo lokale SQLite opslaan in plaats van het archief van de externe server Hallo.  toocreate een offline tabel eerst uw project voorbereiden:

1. In Visual Studio met de rechtermuisknop op Hallo oplossing > **NuGet-pakketten beheren voor oplossing...** , zoek vervolgens naar en installeren de **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet-pakket voor alle projecten in Hallo-oplossing.
2. Windows-apparaten (optioneel) toosupport, installeert u een Hallo SQLite runtime pakketten te volgen:

   * **Windows 8.1 Runtime:** installeren [SQLite voor Windows 8.1][3].
   * **Windows Phone 8.1:** installeren [SQLite voor Windows Phone 8.1][4].
   * **Universele Windows-Platform** installeren [SQLite voor universele Windows hello][5].
3. (Optioneel). Voor Windows-apparaten, klikt u op **verwijzingen** > **verwijzing toevoegen...** , vouw Hallo **Windows** map > **extensies**, schakel vervolgens de juiste Hallo **SQLite voor Windows** SDK samen met de Hallo  **Visual C++ 2013-Runtime voor Windows** SDK.
    Hallo verschillen SQLite SDK namen met elke Windows-platform.

Voordat een tabelverwijzing kan worden gemaakt, moet het lokale archief Hallo worden voorbereid:

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

Initialiseren van de wordt normaal uitgevoerd onmiddellijk nadat het Hallo-client wordt gemaakt.  Hallo **OfflineDbPath** moet een bestandsnaam hebben die geschikt zijn voor gebruik op alle platforms die u ondersteunt.  Als het Hallo-pad is een volledig gekwalificeerde pad (dat wil zeggen, begint met een slash), wordt dat pad gebruikt.  Als Hallo pad niet volledig opgegeven is, wordt Hallo-bestand in een platform-specifieke locatie geplaatst.

* Voor iOS en Android-apparaten is het standaardpad Hallo Hallo 'Persoonlijke bestanden' map.
* Voor Windows-apparaten is het standaardpad Hallo Hallo toepassingsspecifieke 'AppData' map.

Een tabelverwijzing kan worden verkregen met Hallo `GetSyncTable<>` methode:

```
var table = client.GetSyncTable<TodoItem>();
```

U hoeft niet tooauthenticate toouse een offline-tabel.  U hoeft alleen tooauthenticate wanneer u met de Hallo back-endservice communiceert.

### <a name="syncoffline"></a>Synchroniseren van een Offline-tabel
Offline tabellen zijn niet gesynchroniseerd met Hallo back-end standaard.  Synchronisatie is opgesplitst in twee delen.  U kunt wijzigingen afzonderlijk forceren nieuwe items worden gedownload.  Hier volgt een typisch synchronisatiemethode:

```
public async Task SyncAsync()
{
    ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

    try
    {
        await this.client.SyncContext.PushAsync();

        await this.todoTable.PullAsync(
            //hello first parameter is a query name that is used internally by hello client SDK tooimplement incremental sync.
            //Use a different query name for each unique query in your program
            "allTodoItems",
            this.todoTable.CreateQuery());
    }
    catch (MobileServicePushFailedException exc)
    {
        if (exc.PushResult != null)
        {
            syncErrors = exc.PushResult.Errors;
        }
    }

    // Simple error/conflict handling. A real application would handle hello various errors like network conditions,
    // server conflicts and others via hello IMobileServiceSyncHandler.
    if (syncErrors != null)
    {
        foreach (var error in syncErrors)
        {
            if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
            {
                //Update failed, reverting tooserver's copy.
                await error.CancelAndUpdateItemAsync(error.Result);
            }
            else
            {
                // Discard local change.
                await error.CancelAndDiscardItemAsync();
            }

            Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.", error.TableName, error.Item["id"]);
        }
    }
}
```

Als eerste argument te Hallo`PullAsync` null incrementele synchronisatie wordt niet gebruikt.  Elke synchronisatiebewerking haalt alle records.

Hallo SDK voert een impliciete `PushAsync()` voordat binnenhalen van records.

Conflict verwerking wordt uitgevoerd op een `PullAsync()` methode.  U kunt bekommeren om conflicten in Hallo dezelfde manier als online-tabellen.  Hallo conflict wordt gemaakt wanneer `PullAsync()` wordt aangeroepen in plaats van tijdens het Hallo insert, update of delete. Als meerdere conflicten optreden, worden ze in een enkel MobileServicePushFailedException gebundeld.  Elke fout afzonderlijk verwerkt.

## <a name="#customapi"></a>Werken met een aangepaste API gebruiken
Een aangepaste API kunt u toodefine aangepaste eindpunten die serverfunctionaliteit weergeven die geen toewijzen tooan invoegen, bijwerken, verwijderen of leesbewerking. Met behulp van een aangepaste API gebruiken, kunt u meer controle over messaging, hebben waaronder lezen en HTTP-bericht headers instellen en definiëren van een berichttekst de indeling dan JSON.

U een aangepaste API aanroepen door een Hallo [InvokeApiAsync] methoden op Hallo-client. Hallo volgende regel code verzendt bijvoorbeeld een POST-aanvraag toohello **completeAll** API op Hallo back-end:

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

Dit formulier is een methodeaanroep getypte en vereist dat Hallo **MarkAllResult** retourneren type is gedefinieerd. Getypte en niet-getypeerde methoden worden ondersteund.

Hallo InvokeApiAsync() methode voegt toe toohello API/api/u wenst toocall tenzij Hallo API met begint een '/'.
Bijvoorbeeld:

* `InvokeApiAsync("completeAll",...)`/api/completeAll aanroepen op Hallo back-end
* `InvokeApiAsync("/.auth/me",...)`/.auth/me aanroepen op Hallo back-end

U kunt WebAPI, met inbegrip van deze WebAPIs die niet zijn gedefinieerd met Azure Mobile Apps InvokeApiAsync toocall.  Wanneer u InvokeApiAsync() gebruikt, worden met Hallo aanvraag Hallo juiste headers, waaronder verificatieheaders, verzonden.

## <a name="authentication"></a>Verificatie van gebruikers
Mobiele Apps biedt ondersteuning voor verificatie en autorisatie van app-gebruikers met behulp van verschillende externe id-providers: Facebook, Google, Microsoft-Account, Twitter en Azure Active Directory. U kunt machtigingen instellen voor tabellen toorestrict toegang voor specifieke bewerkingen tooonly geverifieerde gebruikers. U kunt ook Hallo identiteit van autorisatieregels voor geverifieerde gebruikers tooimplement in server-scripts gebruiken. Zie voor meer informatie, Hallo zelfstudie [toevoegen verificatie tooyour app].

Twee verificatie stromen worden ondersteund: *client beheerd* en *server beheerd* stroom. Hallo server beheerd stroom biedt Hallo eenvoudigste verificatie-ervaring, is afhankelijk van de webinterface verificatie Hallo-provider. Hallo client beheerd stroom kan voor de diepgaande integratie met apparaatspecifieke mogelijkheden, zoals is afhankelijk van de provider-specifieke apparaat-specifieke SDK's.

> [!NOTE]
> U wordt aangeraden met behulp van een stroom client beheerd in uw productie-apps.

tooset van verificatie, moet u uw app registreren bij een of meer id-providers.  Hallo-identiteitsprovider genereert een client-ID en een clientgeheim voor uw app.  Deze waarden worden vervolgens ingesteld in uw back-end tooenable Azure App Service-verificatie/autorisatie.  Volg voor meer informatie Hallo gedetailleerde instructies in de zelfstudie [toevoegen verificatie tooyour app].

Hallo volgende onderwerpen worden in deze sectie behandeld:

* [Verificatie van client beheerd](#clientflow)
* [Beheerde server-verificatie](#serverflow)
* [In het cachegeheugen Hallo-verificatietoken](#caching)

### <a name="clientflow"></a>Verificatie van client beheerd
Uw app kan onafhankelijk contact Hallo id-provider en geef vervolgens Hallo geretourneerde token tijdens het aanmelden met uw back-end. Deze stroom client kunt u een ervaring voor eenmalige aanmelding voor gebruikers of tooretrieve extra gebruikersgegevens van de identiteitsprovider Hallo tooprovide. Verificatie van de stroom is voorkeur toousing een stroom server als Hallo identiteitsprovider SDK een meer systeemeigen UX idee biedt en kunt u extra aanpassingen.

Voorbeelden zijn bedoeld voor Hallo-stroom verificatie patronen te volgen:

* [Active Directory Authentication Library](#adal)
* [Facebook of Google](#client-facebook)
* [Live SDK](#client-livesdk)

#### <a name="adal"></a>Verificatie van gebruikers met Active Directory Authentication Library Hallo
U kunt Hallo Active Directory Authentication Library (ADAL) tooinitiate gebruikersverificatie van Hallo-client met behulp van Azure Active Directory-verificatie gebruiken.

1. Uw mobiele app back-end voor AAD eenmalige aanmelding configureren door de volgende Hallo [hoe tooconfigure App Service voor Active Directory-aanmelding] zelfstudie. Zorg ervoor dat toocomplete Hallo optionele stap voor het registreren van een systeemeigen clienttoepassing van.
2. In Visual Studio of Xamarin Studio, open het project en voeg een verwijzing toothe `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet-pakket. Wanneer u zoekt, omvatten voorlopige versies.
3. Hallo code tooyour toepassing te volgen, op basis van toohello platform u toevoegen. Controleer in elk, Hallo vervangingen te volgen:

   * Vervang **INSERT-instantie-hier** met de naam van de Hallo van Hallo tenant waarin u uw toepassing hebt ingericht. De indeling moet https://login.microsoftonline.com/contoso.onmicrosoft.com. Deze waarde kan worden gekopieerd vanaf Hallo domein tabblad in uw Azure Active Directory in Hallo [klassieke Azure-portal].
   * Vervang **INSERT RESOURCE-ID hier** met Hallo client-ID voor uw back-end voor de mobiele app. U kunt Hallo client-ID verkrijgen van Hallo **Geavanceerd** tabblad onder **Azure Active Directory-instellingen** in Hallo-portal.
   * Vervang **INSERT-CLIENT-ID-hier** met client-ID Hallo u hebt gekopieerd uit Hallo native client-toepassing.
   * Vervang **INSERT-OMLEIDINGS-URI-hier** aan uw site */.auth/login/done* eindpunt, met Hallo HTTPS-schema. Deze waarde moet er ongeveer te*https://contoso.azurewebsites.net/.auth/login/done*.

     Hallo-code die nodig is voor elk platform volgt:

     **Windows:**

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        while (user == null)
        {
            string message;
            try
            {
                AuthenticationContext ac = new AuthenticationContext(authority);
                AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                    new Uri(redirectUri), new PlatformParameters(PromptBehavior.Auto, false) );
                JObject payload = new JObject();
                payload["access_token"] = ar.AccessToken;
                user = await App.MobileService.LoginAsync(
                    MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
                message = string.Format("You are now logged in - {0}", user.UserId);
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
    ```

     **Xamarin.iOS**

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync(UIViewController view)
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(view));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine(@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
        }
    }
    ```

     **Xamarin.Android**

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(this));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(ex.Message);
            builder.SetTitle("You must log in. Login Required");
            builder.Create().Show();
        }
    }
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {

        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ```

#### <a name="client-facebook"></a>Eenmalige aanmelding met behulp van een token van Facebook of Google
U kunt Hallo stroom kunt gebruiken, zoals weergegeven in dit fragment voor Facebook of Google.

```
var token = new JObject();
// Replace access_token_value with actual value of your access token obtained
// using hello Facebook or Google SDK.
token.Add("access_token", "access_token_value");

private MobileServiceUser user;
private async Task AuthenticateAsync()
{
    while (user == null)
    {
        string message;
        try
        {
            // Change MobileServiceAuthenticationProvider.Facebook
            // tooMobileServiceAuthenticationProvider.Google if using Google auth.
            user = await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
            message = string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

#### <a name="client-livesdk"></a>Eenmalige aanmelding met Microsoft-Account met Hallo Live SDK
tooauthenticate gebruikers, moet u uw app op Hallo van Microsoft-account Developer Center registreren. Configureer de registratiedetails op uw mobiele App back-end. toocreate een Microsoft account is geregistreerd en verbindt u deze back-end van tooyour Mobile Apps, volledige Hallo stappen in [registreren van uw app toouse een Microsoft-account aanmelding]. Als u zowel de Windows Store en Windows Phone 8/Silverlight-versies van uw app hebt, registreert u eerst Hallo Windows Store-versie.

Hallo volgende code wordt geverifieerd met Live SDK en Hallo token toosign geretourneerd in backend voor mobiele Apps tooyour gebruikt.

```
private LiveConnectSession session;
    //private static string clientId = "<microsoft-account-client-id>";
private async System.Threading.Tasks.Task AuthenticateAsync()
{

    // Get hello URL hello Mobile App backend.
    var serviceUrl = App.MobileService.ApplicationUri.AbsoluteUri;

    // Create hello authentication client for Windows Store using hello service URL.
    LiveAuthClient liveIdClient = new LiveAuthClient(serviceUrl);
    //// Create hello authentication client for Windows Phone using hello client ID of hello registration.
    //LiveAuthClient liveIdClient = new LiveAuthClient(clientId);

    while (session == null)
    {
        // Request hello authentication token from hello Live authentication service.
        // hello wl.basic scope should always be requested.  Other scopes can be added
        LiveLoginResult result = await liveIdClient.LoginAsync(new string[] { "wl.basic" });
        if (result.Status == LiveConnectSessionStatus.Connected)
        {
            session = result.Session;

            // Get information about hello logged-in user.
            LiveConnectClient client = new LiveConnectClient(session);
            LiveOperationResult meResult = await client.GetAsync("me");

            // Use hello Microsoft account auth token toosign in tooApp Service.
            MobileServiceUser loginResult = await App.MobileService
                .LoginWithMicrosoftAccountAsync(result.Session.AuthenticationToken);

            // Display a personalized sign-in greeting.
            string title = string.Format("Welcome {0}!", meResult.Result["first_name"]);
            var message = string.Format("You are now logged in - {0}", loginResult.UserId);
            var dialog = new MessageDialog(message, title);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
        else
        {
            session = null;
            var dialog = new MessageDialog("You must log in.", "Login Required");
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
}
```

Zie voor meer informatie, Hallo [Windows Live SDK] documentatie.

### <a name="serverflow"></a>Beheerde server-verificatie
Wanneer u de id-provider hebt geregistreerd, aanroepen Hallo [LoginAsync] methode op Hallo [MobileServiceClient] Hello [MobileServiceAuthenticationProvider] waarde van de provider. Bijvoorbeeld: hello volgende code initieert een server stroom aanmelden via Facebook.

```
private MobileServiceUser user;
private async System.Threading.Tasks.Task Authenticate()
{
    while (user == null)
    {
        string message;
        try
        {
            user = await client
                .LoginAsync(MobileServiceAuthenticationProvider.Facebook);
            message =
                string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

Als u van een id-provider dan Facebook gebruikmaakt, wijzigt u de waarde Hallo van [MobileServiceAuthenticationProvider] toohello waarde voor de provider.

In een stroom server beheert Azure App Service Hallo OAuth-authenticatiestroom door Hallo aanmeldingspagina van de geselecteerde provider Hallo weer te geven.  Hallo-id-provider retourneert, Azure App Service genereert eenmaal een App Service-verificatietoken. Hallo [LoginAsync] methode retourneert een [MobileServiceUser], waarmee u zowel Hallo [UserId] Hallo geverifieerde gebruiker en Hallo [ MobileServiceAuthenticationToken], als een JSON web token (JWT). Dit token kan worden opgeslagen in de cache en opnieuw worden gebruikt totdat het verloopt. Zie voor meer informatie [opslaan in cache Hallo-verificatietoken](#caching).

### <a name="caching"></a>In het cachegeheugen Hallo-verificatietoken
In sommige gevallen kan na de eerste geslaagde verificatie Hallo doordat Hallo-verificatietoken van Hallo provider toohello Hallo-aanmelding aanroepmethode worden vermeden.  Windows Store en UWP-apps kunt gebruiken [PasswordVault] toocache de huidige verificatie token na een geslaagde aanmelden, als volgt:

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

Hallo UserId waarde wordt opgeslagen als gebruikersnaam van de referentie Hallo Hallo en Hallo-token is opgeslagen als Hallo wachtwoord Hallo. Op de volgende startende, kunt u controleren Hallo **PasswordVault** voor in cache opgeslagen referenties. Hallo volgende voorbeeld wordt in de cache opgeslagen referenties wanneer ze worden gevonden, en anders probeert tooauthenticate opnieuw met de Hallo back-end.

```
// Try tooretrieve stored credentials.
var creds = vault.FindAllByResource("Facebook").FirstOrDefault();
if (creds != null)
{
    // Create hello current user from hello stored credentials.
    client.currentUser = new MobileServiceUser(creds.UserName);
    client.currentUser.MobileServiceAuthenticationToken =
        vault.Retrieve("Facebook", creds.UserName).Password;
}
else
{
    // Regular login flow and cache hello token as shown above.
}
```

Wanneer u een gebruiker afmelden, moet u Hallo opgeslagen referentie, ook als volgt verwijderen:

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

Xamarin-apps gebruiken Hallo [Xamarin.Auth] referenties voor de gegevensopslag van API's toosecurely in een **Account** object. Zie voor een voorbeeld van het gebruik van deze API's, Hallo [AuthStore.cs] codebestand in Hallo [ContosoMoments photo delen voorbeeld](https://github.com/azure-appservice-samples/ContosoMoments).

Als u client beheerd authenticatie gebruikt, u kunt ook de cache Hallo toegangstoken is verkregen van uw provider zoals Facebook en Twitter. Dit token kan worden opgegeven toorequest verificatietoken voor een nieuwe vanuit Hallo back-end, als volgt:

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using hello access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <a name="pushnotifications"></a>Pushmeldingen
Hallo volgende onderwerpen vindt u Pushmeldingen:

* [Registreren voor Pushmeldingen](#register-for-push)
* [Verkrijgen van een pakket-SID van de Windows Store](#package-sid)
* [Registreren bij platformoverschrijdende sjablonen](#register-xplat)

### <a name="register-for-push"></a>How to: registreren voor Pushmeldingen
Hallo Mobile Apps-client kunt u tooregister voor pushmeldingen met Azure Notification Hubs. Als u registreert, krijgt u een koppeling die u Hallo platform-specifieke aanschaft Push Notification Service (PNS). Deze waarde samen met eventuele labels wordt vervolgens opgeven wanneer u Hallo registratie maakt. Hallo registreert volgende code uw Windows-app voor pushmeldingen Hello Windows Notification Service (WNS):

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using hello new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

Als u tooWNS worden gepusht, dan u moet [verkrijgen van een pakket-SID van de Windows Store](#package-sid).  Voor meer informatie over Windows-apps, met inbegrip van hoe tooregister voor registraties van de sjabloon zien [Add push notifications tooyour app].

Aanvragen van de labels van Hallo-client wordt niet ondersteund.  Tag aanvragen zijn achtergrond verwijderd uit de inschrijving.
Als u wenst dat tooregister uw apparaat met labels, maakt u een aangepaste API die gebruikmaakt van Hallo Notification Hubs-API tooperform Hallo registratie namens jou.  [Hallo aangepaste API aanroepen](#customapi) in plaats van Hallo `RegisterNativeAsync()` methode.

### <a name="package-sid"></a>Hoe: verkrijgen van een pakket-SID van de Windows Store
Een pakket-SID is nodig voor het inschakelen van pushmeldingen in Windows Store-apps.  tooreceive een pakket-SID, wordt uw toepassing registreren met Hallo Windows Store.

tooobtain deze waarde:

1. Klik in Visual Studio Solution Explorer met de rechtermuisknop op Hallo Windows Store-app-project, klikt u op **Store** > **App aan Hallo Store koppelen...** .
2. Klik in de wizard Hallo op **volgende**, meld u aan met uw Microsoft-account, typ een naam voor uw app in **een nieuwe appnaam reserveren**, klikt u vervolgens op **Reserve**.
3. Nadat het Hallo-app-registratie is de naam van de app is gemaakt, selecteer hello, klikt u op **volgende**, en klik vervolgens op **koppelen**.
4. Meld u bij toohello [Windows-ontwikkelaarscentrum] met uw Microsoft-Account. Onder **mijn apps**, klikt u op Hallo app registratie die u hebt gemaakt.
5. Klik op **appbeheer** > **App identiteit**, en schuif omlaag toofind uw **pakket-SID**.

Vele toepassingen van Hallo pakket-SID behandelen als een URI in dat geval moet u toouse *ms-app: / /* als Hallo schema. Noteer Hallo-versie van uw pakket-SID gevormd door samenvoeging van deze waarde als voorvoegsel.

Xamarin-apps nodig enkele aanvullende code toobe kunnen tooregister een app die wordt uitgevoerd op Hallo iOS of Android-platform. Zie voor meer informatie Hallo-onderwerp voor uw platform:

* [Xamarin.Android](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [Xamarin.iOS](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <a name="register-xplat"></a>Hoe: Register sjablonen toosend platformoverschrijdende pushmeldingen
tooregister sjablonen gebruiken Hallo `RegisterAsync()` methode met Hallo-sjablonen, als volgt:

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

Uw sjablonen moet `JObject` van het type en kan meerdere sjablonen in de volgende JSON-indeling Hallo bevatten:

```
public JObject myTemplates()
{
    // single template for Windows Notification Service toast
    var template = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(message)</text></binding></visual></toast>";

    var templates = new JObject
    {
        ["generic-message"] = new JObject
        {
            ["body"] = template,
            ["headers"] = new JObject
            {
                ["X-WNS-Type"] = "wns/toast"
            },
            ["tags"] = new JArray()
        },
        ["more-templates"] = new JObject {...}
    };
    return templates;
}
```

Hallo methode **RegisterAsync()** accepteert ook secundaire tegels:

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

Alle codes zijn te vertalen tijdens de registratie voor beveiliging. tooadd tags tooinstallations of sjablonen binnen installaties, Zie [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps].

toosend meldingen met behulp van deze geregistreerde sjablonen verwijzen toohello [Notification Hubs-API's].

## <a name="misc"></a>Diverse onderwerpen
### <a name="errors"></a>Hoe: afhandelen van fouten
Wanneer een fout in Hallo back-end optreedt, Hallo client SDK leidt tot een `MobileServiceInvalidOperationException`.  Het volgende voorbeeld wordt getoond hoe toohandle een uitzondering die is geretourneerd door Hallo back-end:

```
private async void InsertTodoItem(TodoItem todoItem)
{
    // This code inserts a new TodoItem into hello database. When hello operation completes
    // and App Service has assigned an Id, hello item is added toohello CollectionView
    try
    {
        await todoTable.InsertAsync(todoItem);
        items.Add(todoItem);
    }
    catch (MobileServiceInvalidOperationException e)
    {
        // Handle error
    }
}
```

Een ander voorbeeld van moeten omgaan met de foutvoorwaarden vindt u in Hallo [Mobile Apps bestanden voorbeeld]. De [LoggingHandler] voorbeeld bevat een gemachtigde logboekregistratie handler toolog Hallo aanvragen wordt toohello back-end.

### <a name="headers"></a>Hoe: aanpassen aanvraagheaders
toosupport uw specifieke app-scenario, moet u mogelijk toocustomize communicatie met Hallo mobiele App back-end. U kunt bijvoorbeeld wilt tooadd een aangepaste header tooevery uitgaande aanvraag of zelfs antwoorden statuscodes wijzigen. U kunt een aangepaste [DelegatingHandler], Hallo voorbeeld te volgen:

```
public async Task CallClientWithHandler()
{
    MobileServiceClient client = new MobileServiceClient("AppUrl", new MyHandler());
    IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
    var newItem = new TodoItem { Text = "Hello world", Complete = false };
    await todoTable.InsertAsync(newItem);
}

public class MyHandler : DelegatingHandler
{
    protected override async Task<HttpResponseMessage>
        SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)
    {
        // Change hello request-side here based on hello HttpRequestMessage
        request.Headers.Add("x-my-header", "my value");

        // Do hello request
        var response = await base.SendAsync(request, cancellationToken);

        // Change hello response-side here based on hello HttpResponseMessage

        // Return hello modified response
        return response;
    }
}
```


<!-- Anchors. -->


<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-windows-store-dotnet-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[4]: https://msdn.microsoft.com/en-us/library/azure/mt419521(v=azure.10).aspx
[5]: https://github.com/Azure-Samples
[6]: http://www.newtonsoft.com/json/help/html/Properties_T_Newtonsoft_Json_JsonPropertyAttribute.htm
[7]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[8]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[9]: https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/
[10]: http://www.symbolsource.org/
[11]: http://www.symbolsource.org/Public/Wiki/Using
[12]: https://msdn.microsoft.com/en-us/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient(v=azure.10).aspx

[toevoegen verificatie tooyour app]: app-service-mobile-windows-store-dotnet-get-started-users.md
[Offline synchroniseren van gegevens in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md
[Add push notifications tooyour app]: app-service-mobile-windows-store-dotnet-get-started-push.md
[registreren van uw app toouse een Microsoft-account aanmelding]: app-service-mobile-how-to-configure-microsoft-authentication.md
[hoe tooconfigure App Service voor Active Directory-aanmelding]: app-service-mobile-how-to-configure-active-directory-authentication.md

<!-- Microsoft URLs. -->
[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx
[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx
[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx
[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx
[ MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx
[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx
[maakt u een niet-getypeerde tabel tooan]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx
[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx
[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx
[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx
[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx
[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx
[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx
[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx
[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx
[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx
[nemen]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx
[Selecteer]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx
[overslaan]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx
[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx
[Gebruikers-id]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx
[waar]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx
[Azure-portal]: https://portal.azure.com/
[klassieke Azure-portal]: https://manage.windowsazure.com/
[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx
[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx
[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx
[Windows-ontwikkelaarscentrum]: https://dev.windows.com/en-us/overview
[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx
[Windows Live SDK]: https://msdn.microsoft.com/en-us/library/bb404787.aspx
[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx
[ProtectedData]: http://msdn.microsoft.com/library/system.security.cryptography.protecteddata%28VS.95%29.aspx
[Notification Hubs-API's]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[Mobile Apps bestanden voorbeeld]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files
[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63

<!-- External URLs -->
[OData v3 documentatie]: http://www.odata.org/documentation/odata-version-3-0/
[Fiddler]: http://www.telerik.com/fiddler
[Json.NET]: http://www.newtonsoft.com/json
[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/
[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments
[ContosoMoments photo sharing sample]: https://github.com/azure-appservice-samples/ContosoMoments
