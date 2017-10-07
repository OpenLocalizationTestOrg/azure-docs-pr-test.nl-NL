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
# <a name="securing-access-tooazure-cosmos-db-data"></a>Toegang tot tooAzure Cosmos DB gegevens beveiligen
In dit artikel biedt een overzicht van de beveiliging van toegang toodata opgeslagen in [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).

Azure Cosmos DB gebruikt twee typen sleutels tooauthenticate gebruikers en bieden toegang tot tooits gegevens en bronnen. 

|sleuteltype|Resources|
|---|---|
|[Hoofdsleutels](#master-keys) |Gebruikt voor administratieve resources: database-accounts, databases, gebruikers en machtigingen|
|[Resource-tokens](#resource-tokens)|Voor toepassingsresources gebruikt: verzamelingen, documenten, bijlagen, opgeslagen procedures, triggers en UDF's|

<a id="master-keys"></a>

## <a name="master-keys"></a>Hoofdsleutels 

Hoofdsleutels bieden toegang toohello alle Hallo beheerdersrechten resources voor het account database Hallo. Hoofdsleutels:  
- Toegang tooaccounts, databases, gebruikers en machtigingen geven. 
- Kan niet worden gebruikt tooprovide gedetailleerde toegang toocollections en -documenten.
- Tijdens het maken van een account Hallo worden gemaakt.
- Op elk gewenst moment kunnen worden hersteld.

Elk account bestaat uit twee hoofdsleutels: een primaire en secundaire sleutel. Hallo-doel van dubbele sleutels is zodat u kunt opnieuw genereren of sleutels draaien, bieden continue toegangsaccount voor tooyour en gegevens. 

In aanvulling toohello twee hoofdsleutels voor Hallo Cosmos-DB-account zijn er twee sleutels voor alleen-lezen. Deze sleutels alleen-lezen kunnen alleen leesbewerkingen op Hallo-account. Alleen-lezen-sleutels, geen toegang biedt tooread machtigingen resources.

Primaire, secundaire alleen-lezen en lezen-schrijven hoofdsleutels kunnen worden opgehaald en opnieuw gegenereerd met hello Azure-portal. Zie voor instructies [weergeven, kopiëren en opnieuw genereren toegangstoetsen](manage-account.md#keys).

![Toegangsbeheer (IAM) in de hello Azure portal - beveiliging voor NoSQL-database te demonstreren](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

Hallo-proces van het roteren van de hoofdsleutel is eenvoudig. Navigeer toohello Azure portal tooretrieve uw secundaire sleutel vervolgens uw primaire sleutel vervangen door de secundaire sleutel in uw toepassing draaien Hallo primaire sleutel in hello Azure-portal.

![Rotatie van de hoofdsleutel in hello Azure portal - beveiliging voor NoSQL-database te demonstreren](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-toouse-a-master-key"></a>Voorbeeld toouse een hoofdsleutel code

Hallo volgende codevoorbeeld ziet u hoe een Cosmos-DB toouse account eindpunt en de hoofdsleutel tooinstantiate een DocumentClient en maak een database. 

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

## <a name="resource-tokens"></a>Resource-tokens

Resource-tokens bieden toegang toohello toepassingsresources in een database. Resource-tokens:
- Toegang toospecific verzamelingen, partitiesleutels, documenten, bijlagen, opgeslagen procedures, triggers en UDF's bieden.
- Worden gemaakt wanneer een [gebruiker](#users) is verleend [machtigingen](#permissions) tooa bepaalde resource.
- Worden opnieuw gemaakt wanneer een resource machtiging wordt gereageerd op door POST of GET PUT-aanroep.
- Gebruik een hash-resource token specifiek gebouwd voor Hallo gebruiker en resource de machtiging.
- Tijdsgebonden met een geldigheidsperiode aanpasbaar zijn. Hallo standaard geldige timespan is een uur. Levensduur van token, maar kan expliciet worden opgegeven, up tooa maximaal vijf uur.
- Geef een veilige alternatieve toogiving uit Hallo hoofdsleutel. 
- Schakel clients tooread-, schrijf- en delete-bronnen in Hallo Cosmos DB account volgens toohello machtigingen die ze hebt gekregen.

U kunt een resource-token (door het maken van Cosmos-DB-gebruikers en machtigingen) als u wilt dat tooprovide toegang tooresources in uw database Cosmos account tooa client vertrouwd met Hallo hoofdsleutel kunnen niet.  

Cosmos DB resource tokens bieden een veilige alternatief waarmee clients tooread-, schrijf- en delete-resources in uw Cosmos-DB-account op basis van toohello machtigingen die u hebt verleend en zonder dat nodig is voor beide modellen of alleen sleutel lezen.

Hier volgt een typisch ontwerppatroon waarbij resource tokens kunnen worden aangevraagd, gegenereerd en tooclients geleverd:

1. Een service middelste laag is ingesteld tooserve met een mobiele toepassing tooshare gebruiker foto's. 
2. Hallo halverwege tier-service beschikt over de hoofdsleutel Hallo Hallo Cosmos-DB-account.
3. Hallo foto-app is geïnstalleerd op mobiele apparaten van eindgebruikers. 
4. Aanmelden stelt u Hallo foto-app Hallo identiteit van de gebruiker Hallo met Hallo halverwege tier-service. Dit mechanisme van tot stand brengen van de identiteit is alleen van toepassing toohello.
5. Wanneer Hallo identiteit is gemaakt, aanvragen Hallo halverwege tier-service op basis van identiteit Hallo machtigingen.
6. Hallo halverwege tier-service verzendt een resource token back toohello telefoon-app.
7. Hallo phone-app kunt toouse Hallo resource token toodirectly toegang tot Cosmos DB bronnen doorgaan met de Hallo-machtigingen die zijn gedefinieerd door Hallo resource token en voor hello-interval is toegestaan door Hallo resource token. 
8. Wanneer Hallo resource token is verlopen, ontvangt de volgende aanvragen een 401-niet-geautoriseerde uitzondering.  Op dit moment Hallo telefoonapp herstelt Hallo identiteit en vraagt een token van een nieuwe resource.

    ![Azure DB Cosmos resource tokens werkstroom](./media/secure-access-to-data/resourcekeyworkflow.png)

Resource token genereren en beheren wordt verwerkt door de clientbibliotheken van Hallo systeemeigen Cosmos DB; Als u gebruikmaakt van REST moet u Hallo aanvraag/verificatieheaders opgeven. Zie voor meer informatie over het maken van verificatieheaders voor REST [toegangsbeheer voor bronnen voor Cosmos DB](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) of Hallo [broncode voor onze SDK's](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).

Zie voor een voorbeeld van een service voor de middelste laag toogenerate of broker-resource-tokens gebruikt, Hallo [ResourceTokenBroker app](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).

<a id="users"></a>

## <a name="users"></a>Gebruikers
Cosmos DB gebruikers zijn gekoppeld aan een Cosmos-DB-database.  Elke database kan nul of meer Cosmos-DB-gebruikers bevatten.  Hallo met het volgende codevoorbeeld ziet u hoe toocreate een gebruikersbron Cosmos DB.

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> Elke gebruiker Cosmos DB heeft een PermissionsLink-eigenschap die gebruikt tooretrieve Hallo lijst met worden kan [machtigingen](#permissions) Hallo gebruiker gekoppeld.
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a>Machtigingen
Een Cosmos-DB machtiging-bron is gekoppeld aan een Cosmos-DB-gebruiker.  Elke gebruiker kan nul of meer Cosmos DB machtigingen bevatten.  Een machtiging-bron biedt tooa beveiliging toegangstoken dat Hallo behoeften van de gebruiker bij het tooaccess de bron van een specifieke toepassing.
Er zijn twee beschikbare toegangsniveaus die door een resource machtiging worden verleend:

* Alle: Hallo gebruiker volledige machtigingen heeft op Hallo resource.
* Lees: gebruiker Hallo Hallo inhoud van Hallo resource kan alleen worden gelezen, maar schrijven, update of delete-bewerkingen op Hallo resource kan niet worden uitgevoerd.

> [!NOTE]
> In de volgorde toorun Cosmos DB moet opgeslagen procedures Hallo gebruiker gemachtigd Hallo alle op Hallo-verzameling in welke Hallo opgeslagen procedure wordt uitgevoerd.
> 
> 

### <a name="code-sample-toocreate-permission"></a>Code voorbeeld toocreate machtiging

Hallo volgende voorbeeldcode laat zien hoe toocreate een resource machtiging lezen Hallo resource-token van Hallo machtiging resource en Hallo machtigingen koppelen aan Hallo [gebruiker](#users) die eerder is gemaakt.

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

Als u hebt opgegeven dat een partitiesleutel voor uw verzameling, klikt u vervolgens Hallo-machtiging voor verzameling, document en bijlage bronnen omvat tevens Hallo ResourcePartitionKey in toevoeging toohello ResourceLink.

### <a name="code-sample-tooread-permissions-for-user"></a>Code voorbeeld tooread machtigingen voor gebruiker

tooeasily verkrijgen alle machtigingen resources die zijn gekoppeld aan een bepaalde gebruiker, Cosmos DB een machtiging voor het beschikbaar maakt voor elk gebruikersobject feed.  Hallo volgende codefragment toont hoe tooretrieve Hallo machtiging die is gekoppeld aan de gebruiker Hallo die eerder is gemaakt, maken een lijst met machtigingen en exemplaar maken van een nieuwe DocumentClient namens Hallo-gebruiker.

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

## <a name="next-steps"></a>Volgende stappen
* toolearn meer informatie over de beveiliging van de database Cosmos DB, Zie [Cosmos DB: beveiliging van de Database](database-security.md).
* toolearn over het beheer van hoofd- en alleen-lezen-sleutels, Zie [hoe toomanage een account voor Azure Cosmos DB](manage-account.md#keys).
* hoe tooconstruct Azure Cosmos DB autorisatie tokens zien toolearn [toegangsbeheer op Azure Cosmos DB bronnen](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).
