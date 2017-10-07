---
title: aaaLearn hoe toosecure toegang krijgen tot toodata in Azure Cosmos DB | Microsoft Docs
description: Meer informatie over de access control-concepten in Azure Cosmos DB, met inbegrip van hoofdsleutels, alleen-lezen-sleutels, gebruikers en machtigingen.
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 8641225d-e839-4ba6-a6fd-d6314ae3a51c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.openlocfilehash: fef7f8e14b488f6ceab0f2aa279a1e99d4416f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="securing-access-tooazure-cosmos-db-data"></a><span data-ttu-id="ce552-103">Toegang tot tooAzure Cosmos DB gegevens beveiligen</span><span class="sxs-lookup"><span data-stu-id="ce552-103">Securing access tooAzure Cosmos DB data</span></span>
<span data-ttu-id="ce552-104">In dit artikel biedt een overzicht van de beveiliging van toegang toodata opgeslagen in [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="ce552-104">This article provides an overview of securing access toodata stored in [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

<span data-ttu-id="ce552-105">Azure Cosmos DB gebruikt twee typen sleutels tooauthenticate gebruikers en bieden toegang tot tooits gegevens en bronnen.</span><span class="sxs-lookup"><span data-stu-id="ce552-105">Azure Cosmos DB uses two types of keys tooauthenticate users and provide access tooits data and resources.</span></span> 

|<span data-ttu-id="ce552-106">sleuteltype</span><span class="sxs-lookup"><span data-stu-id="ce552-106">Key type</span></span>|<span data-ttu-id="ce552-107">Resources</span><span class="sxs-lookup"><span data-stu-id="ce552-107">Resources</span></span>|
|---|---|
|[<span data-ttu-id="ce552-108">Hoofdsleutels</span><span class="sxs-lookup"><span data-stu-id="ce552-108">Master keys</span></span>](#master-keys) |<span data-ttu-id="ce552-109">Gebruikt voor administratieve resources: database-accounts, databases, gebruikers en machtigingen</span><span class="sxs-lookup"><span data-stu-id="ce552-109">Used for administrative resources: database accounts, databases, users, and permissions</span></span>|
|[<span data-ttu-id="ce552-110">Resource-tokens</span><span class="sxs-lookup"><span data-stu-id="ce552-110">Resource tokens</span></span>](#resource-tokens)|<span data-ttu-id="ce552-111">Voor toepassingsresources gebruikt: verzamelingen, documenten, bijlagen, opgeslagen procedures, triggers en UDF's</span><span class="sxs-lookup"><span data-stu-id="ce552-111">Used for application resources: collections, documents, attachments, stored procedures, triggers, and UDFs</span></span>|

<a id="master-keys"></a>

## <a name="master-keys"></a><span data-ttu-id="ce552-112">Hoofdsleutels</span><span class="sxs-lookup"><span data-stu-id="ce552-112">Master keys</span></span> 

<span data-ttu-id="ce552-113">Hoofdsleutels bieden toegang toohello alle Hallo beheerdersrechten resources voor het account database Hallo.</span><span class="sxs-lookup"><span data-stu-id="ce552-113">Master keys provide access toohello all hello administrative resources for hello database account.</span></span> <span data-ttu-id="ce552-114">Hoofdsleutels:</span><span class="sxs-lookup"><span data-stu-id="ce552-114">Master keys:</span></span>  
- <span data-ttu-id="ce552-115">Toegang tooaccounts, databases, gebruikers en machtigingen geven.</span><span class="sxs-lookup"><span data-stu-id="ce552-115">Provide access tooaccounts, databases, users, and permissions.</span></span> 
- <span data-ttu-id="ce552-116">Kan niet worden gebruikt tooprovide gedetailleerde toegang toocollections en -documenten.</span><span class="sxs-lookup"><span data-stu-id="ce552-116">Cannot be used tooprovide granular access toocollections and documents.</span></span>
- <span data-ttu-id="ce552-117">Tijdens het maken van een account Hallo worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ce552-117">Are created during hello creation of an account.</span></span>
- <span data-ttu-id="ce552-118">Op elk gewenst moment kunnen worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="ce552-118">Can be regenerated at any time.</span></span>

<span data-ttu-id="ce552-119">Elk account bestaat uit twee hoofdsleutels: een primaire en secundaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="ce552-119">Each account consists of two Master keys: a primary key and secondary key.</span></span> <span data-ttu-id="ce552-120">Hallo-doel van dubbele sleutels is zodat u kunt opnieuw genereren of sleutels draaien, bieden continue toegangsaccount voor tooyour en gegevens.</span><span class="sxs-lookup"><span data-stu-id="ce552-120">hello purpose of dual keys is so that you can regenerate, or roll keys, providing continuous access tooyour account and data.</span></span> 

<span data-ttu-id="ce552-121">In aanvulling toohello twee hoofdsleutels voor Hallo Cosmos-DB-account zijn er twee sleutels voor alleen-lezen.</span><span class="sxs-lookup"><span data-stu-id="ce552-121">In addition toohello two master keys for hello Cosmos DB account, there are two read-only keys.</span></span> <span data-ttu-id="ce552-122">Deze sleutels alleen-lezen kunnen alleen leesbewerkingen op Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="ce552-122">These read-only keys only allow read operations on hello account.</span></span> <span data-ttu-id="ce552-123">Alleen-lezen-sleutels, geen toegang biedt tooread machtigingen resources.</span><span class="sxs-lookup"><span data-stu-id="ce552-123">Read-only keys do not provide access tooread permissions resources.</span></span>

<span data-ttu-id="ce552-124">Primaire, secundaire alleen-lezen en lezen-schrijven hoofdsleutels kunnen worden opgehaald en opnieuw gegenereerd met hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ce552-124">Primary, secondary, read only, and read-write master keys can be retrieved and regenerated using hello Azure portal.</span></span> <span data-ttu-id="ce552-125">Zie voor instructies [weergeven, kopiëren en opnieuw genereren toegangstoetsen](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="ce552-125">For instructions, see [View, copy, and regenerate access keys](manage-account.md#keys).</span></span>

![Toegangsbeheer (IAM) in de hello Azure portal - beveiliging voor NoSQL-database te demonstreren](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

<span data-ttu-id="ce552-127">Hallo-proces van het roteren van de hoofdsleutel is eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="ce552-127">hello process of rotating your master key is simple.</span></span> <span data-ttu-id="ce552-128">Navigeer toohello Azure portal tooretrieve uw secundaire sleutel vervolgens uw primaire sleutel vervangen door de secundaire sleutel in uw toepassing draaien Hallo primaire sleutel in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ce552-128">Navigate toohello Azure portal tooretrieve your secondary key, then replace your primary key with your secondary key in your application, then rotate hello primary key in hello Azure portal.</span></span>

![Rotatie van de hoofdsleutel in hello Azure portal - beveiliging voor NoSQL-database te demonstreren](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-toouse-a-master-key"></a><span data-ttu-id="ce552-130">Voorbeeld toouse een hoofdsleutel code</span><span class="sxs-lookup"><span data-stu-id="ce552-130">Code sample toouse a master key</span></span>

<span data-ttu-id="ce552-131">Hallo volgende codevoorbeeld ziet u hoe een Cosmos-DB toouse account eindpunt en de hoofdsleutel tooinstantiate een DocumentClient en maak een database.</span><span class="sxs-lookup"><span data-stu-id="ce552-131">hello following code sample illustrates how toouse a Cosmos DB account endpoint and master key tooinstantiate a DocumentClient and create a database.</span></span> 

```csharp
//Read hello Azure Cosmos DB endpointUrl and authorization keys from config.
//These values are available from hello Azure portal on hello Azure Cosmos DB account blade under "Keys".
//NB > Keep these values in a safe and secure location. Together they provide Administrative access tooyour DocDB account.

private static readonly string endpointUrl = ConfigurationManager.AppSettings["EndPointUrl"];
private static readonly SecureString authorizationKey = ToSecureString(ConfigurationManager.AppSettings["AuthorizationKey"]);

client = new DocumentClient(new Uri(endpointUrl), authorizationKey);

// Create Database
Database database = await client.CreateDatabaseAsync(
    new Database
    {
        Id = databaseName
    });
```

<a id="resource-tokens"></a>

## <a name="resource-tokens"></a><span data-ttu-id="ce552-132">Resource-tokens</span><span class="sxs-lookup"><span data-stu-id="ce552-132">Resource tokens</span></span>

<span data-ttu-id="ce552-133">Resource-tokens bieden toegang toohello toepassingsresources in een database.</span><span class="sxs-lookup"><span data-stu-id="ce552-133">Resource tokens provide access toohello application resources within a database.</span></span> <span data-ttu-id="ce552-134">Resource-tokens:</span><span class="sxs-lookup"><span data-stu-id="ce552-134">Resource tokens:</span></span>
- <span data-ttu-id="ce552-135">Toegang toospecific verzamelingen, partitiesleutels, documenten, bijlagen, opgeslagen procedures, triggers en UDF's bieden.</span><span class="sxs-lookup"><span data-stu-id="ce552-135">Provide access toospecific collections, partition keys, documents, attachments, stored procedures, triggers, and UDFs.</span></span>
- <span data-ttu-id="ce552-136">Worden gemaakt wanneer een [gebruiker](#users) is verleend [machtigingen](#permissions) tooa bepaalde resource.</span><span class="sxs-lookup"><span data-stu-id="ce552-136">Are created when a [user](#users) is granted [permissions](#permissions) tooa specific resource.</span></span>
- <span data-ttu-id="ce552-137">Worden opnieuw gemaakt wanneer een resource machtiging wordt gereageerd op door POST of GET PUT-aanroep.</span><span class="sxs-lookup"><span data-stu-id="ce552-137">Are recreated when a permission resource is acted upon on by POST, GET, or PUT call.</span></span>
- <span data-ttu-id="ce552-138">Gebruik een hash-resource token specifiek gebouwd voor Hallo gebruiker en resource de machtiging.</span><span class="sxs-lookup"><span data-stu-id="ce552-138">Use a hash resource token specifically constructed for hello user, resource, and permission.</span></span>
- <span data-ttu-id="ce552-139">Tijdsgebonden met een geldigheidsperiode aanpasbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="ce552-139">Are time bound with a customizable validity period.</span></span> <span data-ttu-id="ce552-140">Hallo standaard geldige timespan is een uur.</span><span class="sxs-lookup"><span data-stu-id="ce552-140">hello default valid timespan is one hour.</span></span> <span data-ttu-id="ce552-141">Levensduur van token, maar kan expliciet worden opgegeven, up tooa maximaal vijf uur.</span><span class="sxs-lookup"><span data-stu-id="ce552-141">Token lifetime, however, may be explicitly specified, up tooa maximum of five hours.</span></span>
- <span data-ttu-id="ce552-142">Geef een veilige alternatieve toogiving uit Hallo hoofdsleutel.</span><span class="sxs-lookup"><span data-stu-id="ce552-142">Provide a safe alternative toogiving out hello master key.</span></span> 
- <span data-ttu-id="ce552-143">Schakel clients tooread-, schrijf- en delete-bronnen in Hallo Cosmos DB account volgens toohello machtigingen die ze hebt gekregen.</span><span class="sxs-lookup"><span data-stu-id="ce552-143">Enable clients tooread, write, and delete resources in hello Cosmos DB account according toohello permissions they've been granted.</span></span>

<span data-ttu-id="ce552-144">U kunt een resource-token (door het maken van Cosmos-DB-gebruikers en machtigingen) als u wilt dat tooprovide toegang tooresources in uw database Cosmos account tooa client vertrouwd met Hallo hoofdsleutel kunnen niet.</span><span class="sxs-lookup"><span data-stu-id="ce552-144">You can use a resource token (by creating Cosmos DB users and permissions) when you want tooprovide access tooresources in your Cosmos DB account tooa client that cannot be trusted with hello master key.</span></span>  

<span data-ttu-id="ce552-145">Cosmos DB resource tokens bieden een veilige alternatief waarmee clients tooread-, schrijf- en delete-resources in uw Cosmos-DB-account op basis van toohello machtigingen die u hebt verleend en zonder dat nodig is voor beide modellen of alleen sleutel lezen.</span><span class="sxs-lookup"><span data-stu-id="ce552-145">Cosmos DB resource tokens provide a safe alternative that enables clients tooread, write, and delete resources in your Cosmos DB account according toohello permissions you've granted, and without need for either a master or read only key.</span></span>

<span data-ttu-id="ce552-146">Hier volgt een typisch ontwerppatroon waarbij resource tokens kunnen worden aangevraagd, gegenereerd en tooclients geleverd:</span><span class="sxs-lookup"><span data-stu-id="ce552-146">Here is a typical design pattern whereby resource tokens may be requested, generated, and delivered tooclients:</span></span>

1. <span data-ttu-id="ce552-147">Een service middelste laag is ingesteld tooserve met een mobiele toepassing tooshare gebruiker foto's.</span><span class="sxs-lookup"><span data-stu-id="ce552-147">A mid-tier service is set up tooserve a mobile application tooshare user photos.</span></span> 
2. <span data-ttu-id="ce552-148">Hallo halverwege tier-service beschikt over de hoofdsleutel Hallo Hallo Cosmos-DB-account.</span><span class="sxs-lookup"><span data-stu-id="ce552-148">hello mid-tier service possesses hello master key of hello Cosmos DB account.</span></span>
3. <span data-ttu-id="ce552-149">Hallo foto-app is geïnstalleerd op mobiele apparaten van eindgebruikers.</span><span class="sxs-lookup"><span data-stu-id="ce552-149">hello photo app is installed on end-user mobile devices.</span></span> 
4. <span data-ttu-id="ce552-150">Aanmelden stelt u Hallo foto-app Hallo identiteit van de gebruiker Hallo met Hallo halverwege tier-service.</span><span class="sxs-lookup"><span data-stu-id="ce552-150">On login, hello photo app establishes hello identity of hello user with hello mid-tier service.</span></span> <span data-ttu-id="ce552-151">Dit mechanisme van tot stand brengen van de identiteit is alleen van toepassing toohello.</span><span class="sxs-lookup"><span data-stu-id="ce552-151">This mechanism of identity establishment is purely up toohello application.</span></span>
5. <span data-ttu-id="ce552-152">Wanneer Hallo identiteit is gemaakt, aanvragen Hallo halverwege tier-service op basis van identiteit Hallo machtigingen.</span><span class="sxs-lookup"><span data-stu-id="ce552-152">Once hello identity is established, hello mid-tier service requests permissions based on hello identity.</span></span>
6. <span data-ttu-id="ce552-153">Hallo halverwege tier-service verzendt een resource token back toohello telefoon-app.</span><span class="sxs-lookup"><span data-stu-id="ce552-153">hello mid-tier service sends a resource token back toohello phone app.</span></span>
7. <span data-ttu-id="ce552-154">Hallo phone-app kunt toouse Hallo resource token toodirectly toegang tot Cosmos DB bronnen doorgaan met de Hallo-machtigingen die zijn gedefinieerd door Hallo resource token en voor hello-interval is toegestaan door Hallo resource token.</span><span class="sxs-lookup"><span data-stu-id="ce552-154">hello phone app can continue toouse hello resource token toodirectly access Cosmos DB resources with hello permissions defined by hello resource token and for hello interval allowed by hello resource token.</span></span> 
8. <span data-ttu-id="ce552-155">Wanneer Hallo resource token is verlopen, ontvangt de volgende aanvragen een 401-niet-geautoriseerde uitzondering.</span><span class="sxs-lookup"><span data-stu-id="ce552-155">When hello resource token expires, subsequent requests receive a 401 unauthorized exception.</span></span>  <span data-ttu-id="ce552-156">Op dit moment Hallo telefoonapp herstelt Hallo identiteit en vraagt een token van een nieuwe resource.</span><span class="sxs-lookup"><span data-stu-id="ce552-156">At this point, hello phone app re-establishes hello identity and requests a new resource token.</span></span>

    ![Azure DB Cosmos resource tokens werkstroom](./media/secure-access-to-data/resourcekeyworkflow.png)

<span data-ttu-id="ce552-158">Resource token genereren en beheren wordt verwerkt door de clientbibliotheken van Hallo systeemeigen Cosmos DB; Als u gebruikmaakt van REST moet u Hallo aanvraag/verificatieheaders opgeven.</span><span class="sxs-lookup"><span data-stu-id="ce552-158">Resource token generation and management is handled by hello native Cosmos DB client libraries; however, if you use REST you must construct hello request/authentication headers.</span></span> <span data-ttu-id="ce552-159">Zie voor meer informatie over het maken van verificatieheaders voor REST [toegangsbeheer voor bronnen voor Cosmos DB](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) of Hallo [broncode voor onze SDK's](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span><span class="sxs-lookup"><span data-stu-id="ce552-159">For more information on creating authentication headers for REST, see [Access Control on Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) or hello [source code for our SDKs](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span></span>

<span data-ttu-id="ce552-160">Zie voor een voorbeeld van een service voor de middelste laag toogenerate of broker-resource-tokens gebruikt, Hallo [ResourceTokenBroker app](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span><span class="sxs-lookup"><span data-stu-id="ce552-160">For an example of a middle tier service used toogenerate or broker resource tokens, see hello [ResourceTokenBroker app](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span></span>

<a id="users"></a>

## <a name="users"></a><span data-ttu-id="ce552-161">Gebruikers</span><span class="sxs-lookup"><span data-stu-id="ce552-161">Users</span></span>
<span data-ttu-id="ce552-162">Cosmos DB gebruikers zijn gekoppeld aan een Cosmos-DB-database.</span><span class="sxs-lookup"><span data-stu-id="ce552-162">Cosmos DB users are associated with a Cosmos DB database.</span></span>  <span data-ttu-id="ce552-163">Elke database kan nul of meer Cosmos-DB-gebruikers bevatten.</span><span class="sxs-lookup"><span data-stu-id="ce552-163">Each database can contain zero or more Cosmos DB users.</span></span>  <span data-ttu-id="ce552-164">Hallo met het volgende codevoorbeeld ziet u hoe toocreate een gebruikersbron Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ce552-164">hello following code sample shows how toocreate a Cosmos DB user resource.</span></span>

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> <span data-ttu-id="ce552-165">Elke gebruiker Cosmos DB heeft een PermissionsLink-eigenschap die gebruikt tooretrieve Hallo lijst met worden kan [machtigingen](#permissions) Hallo gebruiker gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="ce552-165">Each Cosmos DB user has a PermissionsLink property that can be used tooretrieve hello list of [permissions](#permissions) associated with hello user.</span></span>
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a><span data-ttu-id="ce552-166">Machtigingen</span><span class="sxs-lookup"><span data-stu-id="ce552-166">Permissions</span></span>
<span data-ttu-id="ce552-167">Een Cosmos-DB machtiging-bron is gekoppeld aan een Cosmos-DB-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ce552-167">A Cosmos DB permission resource is associated with a Cosmos DB user.</span></span>  <span data-ttu-id="ce552-168">Elke gebruiker kan nul of meer Cosmos DB machtigingen bevatten.</span><span class="sxs-lookup"><span data-stu-id="ce552-168">Each user may contain zero or more Cosmos DB permissions.</span></span>  <span data-ttu-id="ce552-169">Een machtiging-bron biedt tooa beveiliging toegangstoken dat Hallo behoeften van de gebruiker bij het tooaccess de bron van een specifieke toepassing.</span><span class="sxs-lookup"><span data-stu-id="ce552-169">A permission resource provides access tooa security token that hello user needs when trying tooaccess a specific application resource.</span></span>
<span data-ttu-id="ce552-170">Er zijn twee beschikbare toegangsniveaus die door een resource machtiging worden verleend:</span><span class="sxs-lookup"><span data-stu-id="ce552-170">There are two available access levels that may be provided by a permission resource:</span></span>

* <span data-ttu-id="ce552-171">Alle: Hallo gebruiker volledige machtigingen heeft op Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="ce552-171">All: hello user has full permission on hello resource.</span></span>
* <span data-ttu-id="ce552-172">Lees: gebruiker Hallo Hallo inhoud van Hallo resource kan alleen worden gelezen, maar schrijven, update of delete-bewerkingen op Hallo resource kan niet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ce552-172">Read: hello user can only read hello contents of hello resource but cannot perform write, update, or delete operations on hello resource.</span></span>

> [!NOTE]
> <span data-ttu-id="ce552-173">In de volgorde toorun Cosmos DB moet opgeslagen procedures Hallo gebruiker gemachtigd Hallo alle op Hallo-verzameling in welke Hallo opgeslagen procedure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ce552-173">In order toorun Cosmos DB stored procedures hello user must have hello All permission on hello collection in which hello stored procedure will be run.</span></span>
> 
> 

### <a name="code-sample-toocreate-permission"></a><span data-ttu-id="ce552-174">Code voorbeeld toocreate machtiging</span><span class="sxs-lookup"><span data-stu-id="ce552-174">Code sample toocreate permission</span></span>

<span data-ttu-id="ce552-175">Hallo volgende voorbeeldcode laat zien hoe toocreate een resource machtiging lezen Hallo resource-token van Hallo machtiging resource en Hallo machtigingen koppelen aan Hallo [gebruiker](#users) die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ce552-175">hello following code sample shows how toocreate a permission resource, read hello resource token of hello permission resource, and associate hello permissions with hello [user](#users) created above.</span></span>

```csharp
// Create a permission.
Permission docPermission = new Permission
{
    PermissionMode = PermissionMode.Read,
    ResourceLink = documentCollection.SelfLink,
    Id = "readperm"
};
  
docPermission = await client.CreatePermissionAsync(UriFactory.CreateUserUri("db", "user"), docPermission);
Console.WriteLine(docPermission.Id + " has token of: " + docPermission.Token);
```

<span data-ttu-id="ce552-176">Als u hebt opgegeven dat een partitiesleutel voor uw verzameling, klikt u vervolgens Hallo-machtiging voor verzameling, document en bijlage bronnen omvat tevens Hallo ResourcePartitionKey in toevoeging toohello ResourceLink.</span><span class="sxs-lookup"><span data-stu-id="ce552-176">If you have specified a partition key for your collection, then hello permission for collection, document, and attachment resources must also include hello ResourcePartitionKey in addition toohello ResourceLink.</span></span>

### <a name="code-sample-tooread-permissions-for-user"></a><span data-ttu-id="ce552-177">Code voorbeeld tooread machtigingen voor gebruiker</span><span class="sxs-lookup"><span data-stu-id="ce552-177">Code sample tooread permissions for user</span></span>

<span data-ttu-id="ce552-178">tooeasily verkrijgen alle machtigingen resources die zijn gekoppeld aan een bepaalde gebruiker, Cosmos DB een machtiging voor het beschikbaar maakt voor elk gebruikersobject feed.</span><span class="sxs-lookup"><span data-stu-id="ce552-178">tooeasily obtain all permission resources associated with a particular user, Cosmos DB makes available a permission feed for each user object.</span></span>  <span data-ttu-id="ce552-179">Hallo volgende codefragment toont hoe tooretrieve Hallo machtiging die is gekoppeld aan de gebruiker Hallo die eerder is gemaakt, maken een lijst met machtigingen en exemplaar maken van een nieuwe DocumentClient namens Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ce552-179">hello following code snippet shows how tooretrieve hello permission associated with hello user created above, construct a permission list, and instantiate a new DocumentClient on behalf of hello user.</span></span>

```csharp
//Read a permission feed.
FeedResponse<Permission> permFeed = await client.ReadPermissionFeedAsync(
  UriFactory.CreateUserUri("db", "myUser"));
 List<Permission> permList = new List<Permission>();

foreach (Permission perm in permFeed)
{
    permList.Add(perm);
}

DocumentClient userClient = new DocumentClient(new Uri(endpointUrl), permList);
```

## <a name="next-steps"></a><span data-ttu-id="ce552-180">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ce552-180">Next steps</span></span>
* <span data-ttu-id="ce552-181">toolearn meer informatie over de beveiliging van de database Cosmos DB, Zie [Cosmos DB: beveiliging van de Database](database-security.md).</span><span class="sxs-lookup"><span data-stu-id="ce552-181">toolearn more about Cosmos DB database security, see [Cosmos DB: Database security](database-security.md).</span></span>
* <span data-ttu-id="ce552-182">toolearn over het beheer van hoofd- en alleen-lezen-sleutels, Zie [hoe toomanage een account voor Azure Cosmos DB](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="ce552-182">toolearn about managing master and read-only keys, see [How toomanage an Azure Cosmos DB account](manage-account.md#keys).</span></span>
* <span data-ttu-id="ce552-183">hoe tooconstruct Azure Cosmos DB autorisatie tokens zien toolearn [toegangsbeheer op Azure Cosmos DB bronnen](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).</span><span class="sxs-lookup"><span data-stu-id="ce552-183">toolearn how tooconstruct Azure Cosmos DB authorization tokens, see [Access Control on Azure Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).</span></span>
