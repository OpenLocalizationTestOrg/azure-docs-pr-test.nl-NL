---
title: Meer informatie over het beveiligen van toegang tot gegevens in Azure Cosmos DB | Microsoft Docs
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
ms.openlocfilehash: 383e04f91eec2f465b381ce30f2d6d24c488b731
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="securing-access-to-azure-cosmos-db-data"></a><span data-ttu-id="5ddc3-103">Toegang tot Azure DB die Cosmos-gegevens beveiligen</span><span class="sxs-lookup"><span data-stu-id="5ddc3-103">Securing access to Azure Cosmos DB data</span></span>
<span data-ttu-id="5ddc3-104">In dit artikel biedt een overzicht van de beveiliging van toegang tot gegevens die zijn opgeslagen in [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="5ddc3-104">This article provides an overview of securing access to data stored in [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

<span data-ttu-id="5ddc3-105">Azure Cosmos DB gebruikt twee typen sleutels voor het verifiëren van gebruikers en toegang bieden tot de gegevens en bronnen.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-105">Azure Cosmos DB uses two types of keys to authenticate users and provide access to its data and resources.</span></span> 

|<span data-ttu-id="5ddc3-106">sleuteltype</span><span class="sxs-lookup"><span data-stu-id="5ddc3-106">Key type</span></span>|<span data-ttu-id="5ddc3-107">Resources</span><span class="sxs-lookup"><span data-stu-id="5ddc3-107">Resources</span></span>|
|---|---|
|[<span data-ttu-id="5ddc3-108">Hoofdsleutels</span><span class="sxs-lookup"><span data-stu-id="5ddc3-108">Master keys</span></span>](#master-keys) |<span data-ttu-id="5ddc3-109">Gebruikt voor administratieve resources: database-accounts, databases, gebruikers en machtigingen</span><span class="sxs-lookup"><span data-stu-id="5ddc3-109">Used for administrative resources: database accounts, databases, users, and permissions</span></span>|
|[<span data-ttu-id="5ddc3-110">Resource-tokens</span><span class="sxs-lookup"><span data-stu-id="5ddc3-110">Resource tokens</span></span>](#resource-tokens)|<span data-ttu-id="5ddc3-111">Voor toepassingsresources gebruikt: verzamelingen, documenten, bijlagen, opgeslagen procedures, triggers en UDF's</span><span class="sxs-lookup"><span data-stu-id="5ddc3-111">Used for application resources: collections, documents, attachments, stored procedures, triggers, and UDFs</span></span>|

<a id="master-keys"></a>

## <a name="master-keys"></a><span data-ttu-id="5ddc3-112">Hoofdsleutels</span><span class="sxs-lookup"><span data-stu-id="5ddc3-112">Master keys</span></span> 

<span data-ttu-id="5ddc3-113">Hoofdsleutels bieden toegang tot de alle beheerdersrechten resources voor het account van de database.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-113">Master keys provide access to the all the administrative resources for the database account.</span></span> <span data-ttu-id="5ddc3-114">Hoofdsleutels:</span><span class="sxs-lookup"><span data-stu-id="5ddc3-114">Master keys:</span></span>  
- <span data-ttu-id="5ddc3-115">Bieden toegang tot accounts, databases, gebruikers en machtigingen.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-115">Provide access to accounts, databases, users, and permissions.</span></span> 
- <span data-ttu-id="5ddc3-116">Kan niet worden gebruikt voor gedetailleerde toegang tot de verzamelingen en documenten.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-116">Cannot be used to provide granular access to collections and documents.</span></span>
- <span data-ttu-id="5ddc3-117">Tijdens het maken van een account zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-117">Are created during the creation of an account.</span></span>
- <span data-ttu-id="5ddc3-118">Op elk gewenst moment kunnen worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-118">Can be regenerated at any time.</span></span>

<span data-ttu-id="5ddc3-119">Elk account bestaat uit twee hoofdsleutels: een primaire en secundaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-119">Each account consists of two Master keys: a primary key and secondary key.</span></span> <span data-ttu-id="5ddc3-120">Het doel van dubbele sleutels is zodat u kunt opnieuw genereren of sleutels draaien, continue toegang tot uw account en -gegevens.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-120">The purpose of dual keys is so that you can regenerate, or roll keys, providing continuous access to your account and data.</span></span> 

<span data-ttu-id="5ddc3-121">Naast de twee hoofdsleutels voor het account van de Cosmos-DB zijn er twee sleutels voor alleen-lezen.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-121">In addition to the two master keys for the Cosmos DB account, there are two read-only keys.</span></span> <span data-ttu-id="5ddc3-122">Deze sleutels alleen-lezen kunnen alleen leesbewerkingen op het account.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-122">These read-only keys only allow read operations on the account.</span></span> <span data-ttu-id="5ddc3-123">Alleen-lezen sleutels bieden geen toegang tot bronnen van de machtigingen lezen.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-123">Read-only keys do not provide access to read permissions resources.</span></span>

<span data-ttu-id="5ddc3-124">Primaire, secundaire alleen-lezen en lezen-schrijven hoofdsleutels kunnen worden opgehaald en wordt opnieuw gegenereerd met de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-124">Primary, secondary, read only, and read-write master keys can be retrieved and regenerated using the Azure portal.</span></span> <span data-ttu-id="5ddc3-125">Zie voor instructies [weergeven, kopiëren en opnieuw genereren toegangstoetsen](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="5ddc3-125">For instructions, see [View, copy, and regenerate access keys](manage-account.md#keys).</span></span>

![Toegangsbeheer (IAM) in de Azure portal - beveiliging voor NoSQL-database te demonstreren](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

<span data-ttu-id="5ddc3-127">Het proces van het roteren van de hoofdsleutel is eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-127">The process of rotating your master key is simple.</span></span> <span data-ttu-id="5ddc3-128">Navigeer naar de Azure-portal en ophalen van de secundaire sleutel vervolgens uw primaire sleutel vervangen door de secundaire sleutel in uw toepassing vervolgens roteren van de primaire sleutel in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-128">Navigate to the Azure portal to retrieve your secondary key, then replace your primary key with your secondary key in your application, then rotate the primary key in the Azure portal.</span></span>

![Rotatie van de hoofdsleutel in de Azure portal - beveiliging voor NoSQL-database te demonstreren](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-to-use-a-master-key"></a><span data-ttu-id="5ddc3-130">Voorbeeld van code een hoofdsleutel gebruiken</span><span class="sxs-lookup"><span data-stu-id="5ddc3-130">Code sample to use a master key</span></span>

<span data-ttu-id="5ddc3-131">De volgende voorbeeldcode laat zien hoe een Cosmos-DB account eindpunt en de hoofdsleutel gebruiken om te instantiëren van een DocumentClient en een database maken.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-131">The following code sample illustrates how to use a Cosmos DB account endpoint and master key to instantiate a DocumentClient and create a database.</span></span> 

```csharp
//Read the Azure Cosmos DB endpointUrl and authorization keys from config.
//These values are available from the Azure portal on the Azure Cosmos DB account blade under "Keys".
//NB > Keep these values in a safe and secure location. Together they provide Administrative access to your DocDB account.

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

## <a name="resource-tokens"></a><span data-ttu-id="5ddc3-132">Resource-tokens</span><span class="sxs-lookup"><span data-stu-id="5ddc3-132">Resource tokens</span></span>

<span data-ttu-id="5ddc3-133">Resource-tokens bieden toegang tot de toepassingsresources in een database.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-133">Resource tokens provide access to the application resources within a database.</span></span> <span data-ttu-id="5ddc3-134">Resource-tokens:</span><span class="sxs-lookup"><span data-stu-id="5ddc3-134">Resource tokens:</span></span>
- <span data-ttu-id="5ddc3-135">Toegang tot specifieke verzamelingen, partitiesleutels, documenten, bijlagen, opgeslagen procedures, triggers en UDF's bieden.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-135">Provide access to specific collections, partition keys, documents, attachments, stored procedures, triggers, and UDFs.</span></span>
- <span data-ttu-id="5ddc3-136">Worden gemaakt wanneer een [gebruiker](#users) is verleend [machtigingen](#permissions) op een specifieke bron.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-136">Are created when a [user](#users) is granted [permissions](#permissions) to a specific resource.</span></span>
- <span data-ttu-id="5ddc3-137">Worden opnieuw gemaakt wanneer een resource machtiging wordt gereageerd op door POST of GET PUT-aanroep.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-137">Are recreated when a permission resource is acted upon on by POST, GET, or PUT call.</span></span>
- <span data-ttu-id="5ddc3-138">Een hash-resource-token die specifiek voor de gebruiker, de bron en de machtiging is gebouwd gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-138">Use a hash resource token specifically constructed for the user, resource, and permission.</span></span>
- <span data-ttu-id="5ddc3-139">Tijdsgebonden met een geldigheidsperiode aanpasbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-139">Are time bound with a customizable validity period.</span></span> <span data-ttu-id="5ddc3-140">De standaard geldige timespan is een uur.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-140">The default valid timespan is one hour.</span></span> <span data-ttu-id="5ddc3-141">Levensduur van token, maar kan expliciet worden opgegeven, maximaal vijf uur.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-141">Token lifetime, however, may be explicitly specified, up to a maximum of five hours.</span></span>
- <span data-ttu-id="5ddc3-142">Geef een veilige alternatief voor het geven van de hoofdsleutel.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-142">Provide a safe alternative to giving out the master key.</span></span> 
- <span data-ttu-id="5ddc3-143">Inschakelen voor clients om te lezen, schrijven en verwijderen van resources in het account van de Cosmos-DB volgens de machtigingen die ze hebt gekregen.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-143">Enable clients to read, write, and delete resources in the Cosmos DB account according to the permissions they've been granted.</span></span>

<span data-ttu-id="5ddc3-144">U kunt een resource-token (door het maken van Cosmos-DB-gebruikers en machtigingen) als u wilt toegang bieden tot bronnen in uw account Cosmos-database naar een client die niet kan vertrouwd met de hoofdsleutel worden.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-144">You can use a resource token (by creating Cosmos DB users and permissions) when you want to provide access to resources in your Cosmos DB account to a client that cannot be trusted with the master key.</span></span>  

<span data-ttu-id="5ddc3-145">Cosmos DB resource tokens bieden een veilige alternatief waarmee clients lezen, schrijven en verwijderen van resources in uw account Cosmos DB volgens de machtigingen die u hebt verleend en zonder dat nodig is voor een model- of alleen belangrijke lezen.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-145">Cosmos DB resource tokens provide a safe alternative that enables clients to read, write, and delete resources in your Cosmos DB account according to the permissions you've granted, and without need for either a master or read only key.</span></span>

<span data-ttu-id="5ddc3-146">Hier volgt een typisch ontwerppatroon waarbij resource tokens kunnen worden aangevraagd, gegenereerd en aan clients geleverd:</span><span class="sxs-lookup"><span data-stu-id="5ddc3-146">Here is a typical design pattern whereby resource tokens may be requested, generated, and delivered to clients:</span></span>

1. <span data-ttu-id="5ddc3-147">Een service middelste laag is ingesteld voor het uitvoeren van een mobiele toepassing Gebruikersfoto delen.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-147">A mid-tier service is set up to serve a mobile application to share user photos.</span></span> 
2. <span data-ttu-id="5ddc3-148">De middelste laag-service beschikt over de hoofdsleutel van de Cosmos-DB-account.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-148">The mid-tier service possesses the master key of the Cosmos DB account.</span></span>
3. <span data-ttu-id="5ddc3-149">De foto-app is geïnstalleerd op mobiele apparaten van eindgebruikers.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-149">The photo app is installed on end-user mobile devices.</span></span> 
4. <span data-ttu-id="5ddc3-150">Aanmelden stelt u de app foto de identiteit van de gebruiker met de service voor de middelste laag.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-150">On login, the photo app establishes the identity of the user with the mid-tier service.</span></span> <span data-ttu-id="5ddc3-151">Dit mechanisme van tot stand brengen van de identiteit is uitsluitend tot de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-151">This mechanism of identity establishment is purely up to the application.</span></span>
5. <span data-ttu-id="5ddc3-152">Wanneer de identiteit is gemaakt, serviceaanvragen de middelste laag machtigingen op basis van de identiteit.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-152">Once the identity is established, the mid-tier service requests permissions based on the identity.</span></span>
6. <span data-ttu-id="5ddc3-153">De middelste laag service verzendt een resource-token terug naar de telefoonapp.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-153">The mid-tier service sends a resource token back to the phone app.</span></span>
7. <span data-ttu-id="5ddc3-154">De telefoonapp kunt blijven gebruiken van de resource-token rechtstreeks toegang krijgen tot bronnen van de Cosmos-database met de machtigingen die zijn gedefinieerd door de resource-token en voor het interval dat is toegestaan door de resource-token.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-154">The phone app can continue to use the resource token to directly access Cosmos DB resources with the permissions defined by the resource token and for the interval allowed by the resource token.</span></span> 
8. <span data-ttu-id="5ddc3-155">Wanneer de bron-token is verlopen, ontvangt de volgende aanvragen een 401-niet-geautoriseerde uitzondering.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-155">When the resource token expires, subsequent requests receive a 401 unauthorized exception.</span></span>  <span data-ttu-id="5ddc3-156">Op dit moment de telefoonapp herstelt de identiteit en vraagt een token van een nieuwe resource.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-156">At this point, the phone app re-establishes the identity and requests a new resource token.</span></span>

    ![Azure DB Cosmos resource tokens werkstroom](./media/secure-access-to-data/resourcekeyworkflow.png)

<span data-ttu-id="5ddc3-158">Resource token genereren en beheren wordt verwerkt door de systeemeigen Cosmos DB clientbibliotheken; Als u gebruikmaakt van REST moet u de aanvraag-/ verificatieheaders opgeven.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-158">Resource token generation and management is handled by the native Cosmos DB client libraries; however, if you use REST you must construct the request/authentication headers.</span></span> <span data-ttu-id="5ddc3-159">Zie voor meer informatie over het maken van verificatieheaders voor REST [toegangsbeheer voor bronnen voor Cosmos DB](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) of de [broncode voor onze SDK's](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span><span class="sxs-lookup"><span data-stu-id="5ddc3-159">For more information on creating authentication headers for REST, see [Access Control on Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) or the [source code for our SDKs](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span></span>

<span data-ttu-id="5ddc3-160">Zie voor een voorbeeld van een van de middelste laag-service gebruikt voor het genereren of resource tokens broker de [ResourceTokenBroker app](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span><span class="sxs-lookup"><span data-stu-id="5ddc3-160">For an example of a middle tier service used to generate or broker resource tokens, see the [ResourceTokenBroker app](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span></span>

<a id="users"></a>

## <a name="users"></a><span data-ttu-id="5ddc3-161">Gebruikers</span><span class="sxs-lookup"><span data-stu-id="5ddc3-161">Users</span></span>
<span data-ttu-id="5ddc3-162">Cosmos DB gebruikers zijn gekoppeld aan een Cosmos-DB-database.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-162">Cosmos DB users are associated with a Cosmos DB database.</span></span>  <span data-ttu-id="5ddc3-163">Elke database kan nul of meer Cosmos-DB-gebruikers bevatten.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-163">Each database can contain zero or more Cosmos DB users.</span></span>  <span data-ttu-id="5ddc3-164">De volgende voorbeeldcode laat zien hoe een Cosmos-DB gebruikersbron maken.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-164">The following code sample shows how to create a Cosmos DB user resource.</span></span>

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> <span data-ttu-id="5ddc3-165">Elke gebruiker Cosmos DB heeft een PermissionsLink-eigenschap die kan worden gebruikt voor het ophalen van de lijst met [machtigingen](#permissions) die zijn gekoppeld aan de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-165">Each Cosmos DB user has a PermissionsLink property that can be used to retrieve the list of [permissions](#permissions) associated with the user.</span></span>
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a><span data-ttu-id="5ddc3-166">Machtigingen</span><span class="sxs-lookup"><span data-stu-id="5ddc3-166">Permissions</span></span>
<span data-ttu-id="5ddc3-167">Een Cosmos-DB machtiging-bron is gekoppeld aan een Cosmos-DB-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-167">A Cosmos DB permission resource is associated with a Cosmos DB user.</span></span>  <span data-ttu-id="5ddc3-168">Elke gebruiker kan nul of meer Cosmos DB machtigingen bevatten.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-168">Each user may contain zero or more Cosmos DB permissions.</span></span>  <span data-ttu-id="5ddc3-169">Een machtiging resource biedt toegang tot een beveiligingstoken dat de gebruiker moet wanneer u probeert te krijgen tot de bron van een specifieke toepassing.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-169">A permission resource provides access to a security token that the user needs when trying to access a specific application resource.</span></span>
<span data-ttu-id="5ddc3-170">Er zijn twee beschikbare toegangsniveaus die door een resource machtiging worden verleend:</span><span class="sxs-lookup"><span data-stu-id="5ddc3-170">There are two available access levels that may be provided by a permission resource:</span></span>

* <span data-ttu-id="5ddc3-171">Alle: De gebruiker heeft volledige machtigingen voor de bron.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-171">All: The user has full permission on the resource.</span></span>
* <span data-ttu-id="5ddc3-172">Lees: De gebruiker de inhoud van de resource kan alleen worden gelezen, maar schrijven, update of delete-bewerkingen op de bron kan niet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-172">Read: The user can only read the contents of the resource but cannot perform write, update, or delete operations on the resource.</span></span>

> [!NOTE]
> <span data-ttu-id="5ddc3-173">Opgeslagen procedures die de gebruiker moet de machtiging All hebben voor de verzameling waarin u de opgeslagen procedure wordt uitgevoerd om te kunnen uitvoeren van de Cosmos-DB.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-173">In order to run Cosmos DB stored procedures the user must have the All permission on the collection in which the stored procedure will be run.</span></span>
> 
> 

### <a name="code-sample-to-create-permission"></a><span data-ttu-id="5ddc3-174">Voorbeeld van code voor het maken van de machtiging</span><span class="sxs-lookup"><span data-stu-id="5ddc3-174">Code sample to create permission</span></span>

<span data-ttu-id="5ddc3-175">De volgende voorbeeldcode laat zien hoe een machtiging resource maken en koppelen van de machtigingen met het resource-token van de bron van de machtiging lezen de [gebruiker](#users) die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-175">The following code sample shows how to create a permission resource, read the resource token of the permission resource, and associate the permissions with the [user](#users) created above.</span></span>

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

<span data-ttu-id="5ddc3-176">Als u een partitiesleutel voor uw verzameling hebt opgegeven, moet klikt u vervolgens de machtiging voor het verzamelen, document en bijlage resources ook de ResourcePartitionKey naast de ResourceLink.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-176">If you have specified a partition key for your collection, then the permission for collection, document, and attachment resources must also include the ResourcePartitionKey in addition to the ResourceLink.</span></span>

### <a name="code-sample-to-read-permissions-for-user"></a><span data-ttu-id="5ddc3-177">Voorbeeld van code lezen machtigingen voor gebruiker</span><span class="sxs-lookup"><span data-stu-id="5ddc3-177">Code sample to read permissions for user</span></span>

<span data-ttu-id="5ddc3-178">Eenvoudig alle om toestemming te krijgen resources die zijn gekoppeld aan een bepaalde gebruiker, Cosmos DB beschikbaar stelt een machtiging voor elk gebruikersobject feed.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-178">To easily obtain all permission resources associated with a particular user, Cosmos DB makes available a permission feed for each user object.</span></span>  <span data-ttu-id="5ddc3-179">Het volgende codefragment laat zien hoe ophalen van de machtiging die is gekoppeld aan de gebruiker die eerder is gemaakt, maken een lijst met machtigingen en exemplaar maken van een nieuwe DocumentClient namens de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="5ddc3-179">The following code snippet shows how to retrieve the permission associated with the user created above, construct a permission list, and instantiate a new DocumentClient on behalf of the user.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5ddc3-180">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5ddc3-180">Next steps</span></span>
* <span data-ttu-id="5ddc3-181">Zie voor meer informatie over de beveiliging van de Cosmos-DB-database, [Cosmos DB: beveiliging van de Database](database-security.md).</span><span class="sxs-lookup"><span data-stu-id="5ddc3-181">To learn more about Cosmos DB database security, see [Cosmos DB: Database security](database-security.md).</span></span>
* <span data-ttu-id="5ddc3-182">Zie voor meer informatie over het beheer van hoofd- en alleen-lezen-sleutels, [het beheren van een account voor Azure Cosmos DB](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="5ddc3-182">To learn about managing master and read-only keys, see [How to manage an Azure Cosmos DB account](manage-account.md#keys).</span></span>
* <span data-ttu-id="5ddc3-183">Zie voor meer informatie over het maken van Azure DB die Cosmos autorisatie tokens, [toegangsbeheer op Azure Cosmos DB bronnen](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).</span><span class="sxs-lookup"><span data-stu-id="5ddc3-183">To learn how to construct Azure Cosmos DB authorization tokens, see [Access Control on Azure Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).</span></span>
