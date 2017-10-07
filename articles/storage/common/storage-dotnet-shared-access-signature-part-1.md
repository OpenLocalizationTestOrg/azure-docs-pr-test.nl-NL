---
title: aaaUsing shared access signatures (SAS) in Azure Storage | Microsoft Docs
description: Meer informatie over toouse shared access signatures (SAS) toodelegate toegang tooAzure opslagbronnen, zoals blobs, wachtrijen, tabellen en bestanden.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 46fd99d7-36b3-4283-81e3-f214b29f1152
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/18/2017
ms.author: marsma
ms.openlocfilehash: 5b75a3c25bcfb9f1ceb81f31dc2d42376bd105cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-shared-access-signatures-sas"></a>Met behulp van handtekeningen voor gedeelde toegang (SAS)

Een shared access signature (SAS) biedt een manier toogrant beperkte toegang tooobjects in uw opslagaccount tooother clients, zonder dat de sleutel van uw account. In dit artikel wordt een overzicht gegeven van SAS-model hello, SAS aanbevolen procedures en bekijk enkele voorbeelden.

Zie voor aanvullende codevoorbeelden via SAS afgezien van wat die hier wordt gepresenteerd, [aan de slag met Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) en andere voorbeelden die beschikbaar zijn in Hallo [Azure codevoorbeelden](https://azure.microsoft.com/documentation/samples/?service=storage) bibliotheek. Hallo voorbeeldtoepassingen downloaden en uitvoeren, of blader Hallo-code op GitHub.

## <a name="what-is-a-shared-access-signature"></a>Wat is er een shared access signature?
Een shared access signature biedt tooresources gedelegeerde toegang in uw opslagaccount. U kunt met een SAS verlenen clients toegang krijgen tot tooresources in uw opslagaccount zonder het delen van de sleutels van uw account. Dit is de belangrijkste punt Hallo van het gebruik van handtekeningen voor gedeelde toegang in uw toepassingen--een SAS is een veilige manier tooshare uw opslagresources zonder uw sleutels account gevaar te brengen.

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

Een SAS biedt gedetailleerde controle over Hallo type toegang u tooclients die Hallo SAS verleent hebben, met inbegrip van:

* via welke Hallo SAS geldig is, met inbegrip van de begin- en verlooptijd Hallo Hallo Hello-interval.
* Hallo machtigingen verleend door Hallo SAS. Een SAS voor een blob kan bijvoorbeeld verleent u lees en machtigingen toothat blob schrijven maar machtigingen niet verwijderen.
* Een optionele IP-adres of een bereik met IP-adressen waarop Azure Storage accepteert Hallo SAS. U kunt bijvoorbeeld een bereik met IP-adressen die behoren tooyour organisatie opgeven.
* Hallo-protocol gedurende welke Azure Storage Hallo SAS accepteert. U kunt deze optionele parameter toorestrict toegang tooclients via HTTPS gebruiken.

## <a name="when-should-you-use-a-shared-access-signature"></a>Wanneer moet u een shared access signature gebruiken?
U kunt een SAS gebruiken als u wilt tooprovide toegang tooresources in uw storage-account tooany client niet toegangssleutels van uw storage-account beschikken. Uw opslagaccount omvat zowel een primaire en secundaire toegangssleutel voor, die beide Verleen beheerderstoegang tooyour account en alle resources binnen het. De mogelijkheid om uw account toohello van schadelijke of Achteloos gebruik blootstellen van een van deze sleutels worden geopend. Handtekeningen voor gedeelde toegang bieden een veilige alternatief waarmee clients tooread-, schrijf- en verwijderen van gegevens in uw opslagaccount volgens toohello machtigingen die u expliciet hebt verleend, en zonder dat nodig is voor de accountsleutel van een.

Een veelvoorkomend scenario waarin een SAS handig is, is een service waar gebruikers lezen en schrijven van hun eigen gegevens tooyour storage-account. In een scenario waar de gebruikersgegevens worden opgeslagen in een opslagaccount, zijn er twee typische ontwerppatronen:

1. Clients uploaden en downloaden van gegevens via een front-proxyservice, die verificatie uitvoert. Deze front-proxyservice heeft Hallo voordeel van het toestaan van validatie van bedrijfsregels, maar voor grote hoeveelheden gegevens of transacties, hoog volume, maken van een service die kan worden geschaald toomatch vraag mogelijk dure of moeilijk.

  ![Scenario-diagram: front-proxy-service](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-fe-proxy-service.png)   

1. Een lichtgewicht service verifieert Hallo-client zo nodig en genereert vervolgens een SAS. Zodra het Hallo-client ontvangt Hallo SAS, toegang te krijgen tot resources voor storage-account rechtstreeks met de Hallo-machtigingen die zijn gedefinieerd door Hallo SAS en voor hello-interval is toegestaan door Hallo SAS. Hallo SAS vermindert Hallo nodig voor het doorsturen van alle gegevens via Hallo front-proxy-service.

  ![Scenario-diagram: SAS provider-service](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-provider-service.png)   

Veel echte services kunnen een hybride versie van deze twee methoden gebruiken. Sommige gegevens kunnen bijvoorbeeld worden verwerkt en gevalideerd via Hallo front-proxy, terwijl andere gegevens wordt opgeslagen en/of rechtstreeks via SAS lezen.

Bovendien moet u toouse een SAS tooauthenticate Hallo bronobject in een kopieerbewerking in bepaalde scenario's:

* Wanneer u een blob tooanother blob die zich in een ander opslagaccount bevindt kopieert, moet u een blob SAS tooauthenticate Hallo bron. U kunt desgewenst een SAS tooauthenticate Hallo bestemmings-blob ook gebruiken.
* Wanneer u een bestand tooanother die zich in een ander opslagaccount bevindt kopieert, moet u een SAS tooauthenticate Hallo-bronbestand. U kunt desgewenst een SAS tooauthenticate Hallo doelbestand ook gebruiken.
* Wanneer u een blob tooa-bestand of een bestand tooa blob kopieert, moet u een SAS tooauthenticate Hallo bronobject, zelfs als Hallo bron- en doelserver objecten zich binnen Hallo hetzelfde bevinden opslagaccount.

## <a name="types-of-shared-access-signatures"></a>Typen handtekeningen voor gedeelde toegang
U kunt twee soorten handtekeningen voor gedeelde toegang maken:

* **Service-SAS.** Hallo-service-SAS gemachtigden toegang tot tooa resource in slechts één van de opslagservices Hallo: Hallo Blob, Queue, Table of bestand service. Zie [samenstellen van een Service-SAS](https://msdn.microsoft.com/library/dn140255.aspx) en [voorbeelden van Service-SAS](https://msdn.microsoft.com/library/dn140256.aspx) voor gedetailleerde informatie over het maken van Hallo service-SAS-token.
* **Account-SAS.** Hallo-account-SAS gemachtigden toegang tot tooresources in een of meer van de opslagservices Hallo. Alle Hallo bewerkingen die beschikbaar zijn via een service-SAS zijn ook beschikbaar via een account-SAS. Met account-SAS hello, kunt u bovendien toegang toooperations die van toepassing zijn tooa service, zoals gegeven delegeren **Get/Set-Service-eigenschappen** en **Service statistieken ophalen**. U kunt ook toegang tooread-, schrijf- en delete-bewerkingen op de blob-containers, tabellen, wachtrijen en bestandsshares die niet zijn toegestaan als een service-SAS delegeren. Zie [samenstellen van een Account-SAS](https://msdn.microsoft.com/library/mt584140.aspx) voor gedetailleerde informatie over het maken van Hallo account-SAS-token.

## <a name="how-a-shared-access-signature-works"></a>De werking van een shared access signature
Een shared access signature is een ondertekende URI die wijst tooone of meer opslagbronnen en bevat een token dat een speciale reeks queryparameters bevat. Hallo token geeft aan hoe Hallo bronnen zijn toegankelijk door Hallo-client. Een van de queryparameters Hallo, Hallo handtekening, is gemaakt op basis van Hallo SAS-parameters en ondertekend door de sleutel van Hallo. Deze handtekening wordt gebruikt door Azure Storage tooauthenticate Hallo SAS.

Hier volgt een voorbeeld van een SAS-URI en weergeeft Hallo resource-URI Hallo SAS-token:

![Onderdelen van een SAS-URI](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-uri.png)   

Hallo SAS-token is een tekenreeks die u op Hallo genereren *client* kant (Zie Hallo [SAS-voorbeelden](#sas-examples) sectie voor codevoorbeelden). Een SAS-token met Hallo storage-clientbibliotheek genereren bijvoorbeeld wordt niet bijgehouden door Azure Storage op elke manier. Aan de clientzijde Hallo kunt u een onbeperkt aantal SAS-tokens.

Wanneer een client een SAS-URI tooAzure opslag als onderdeel van een aanvraag biedt, controleert Hallo service Hallo SAS-parameters en handtekening tooverify geldig voor het verifiëren van Hallo-aanvraag is. Hallo-aanvraag is geverifieerd als Hallo-service wordt gecontroleerd dat Hallo-handtekening is geldig. Anders is Hallo verzoek afgewezen met foutcode 403 (verboden).

## <a name="shared-access-signature-parameters"></a>Parameters voor gedeelde toegang handtekening
Hallo account-SAS en service-SAS-tokens bevatten enkele algemene parameters en ook rekening houden met een aantal parameters die anders zijn.

### <a name="parameters-common-tooaccount-sas-and-service-sas-tokens"></a>Parameters algemene tooaccount SAS en service-SAS-tokens
* **API-versie** een optionele parameter waarmee Hallo opslag versie toouse tooexecute Hallo serviceaanvraag.
* **Service-versie** een vereiste parameter waarmee Hallo opslag versie toouse tooauthenticate Hallo serviceaanvraag.
* **De begintijd.** Dit is Hallo tijd op welke Hallo SAS geldig wordt. de begintijd Hallo voor een shared access signature is optioneel. Als een begintijd wordt weggelaten, wordt Hallo SAS onmiddellijk van kracht. Hallo begintijd moet worden uitgedrukt in UTC (Coordinated Universal Time), met een speciale UTC-aanduiding ('Z'), bijvoorbeeld `1994-11-05T13:15:30Z`.
* **Verlooptijd.** Dit is Hallo tijd waarna hello SAS niet meer geldig is. Aanbevolen dat u een verlooptijd voor een SAS opgeven, of deze aan een opgeslagen toegangsbeleid koppelen. Hallo verlooptijdstip moet worden uitgedrukt in UTC (Coordinated Universal Time), met een speciale UTC-aanduiding ('Z'), bijvoorbeeld `1994-11-05T13:15:30Z` (Zie meer hieronder).
* **Machtigingen.** Hallo-machtigingen die zijn opgegeven op Hallo SAS aangeven welke bewerkingen Hallo client tegen Hallo storage resource met behulp van Hallo SAS kunt uitvoeren. Beschikbare machtigingen verschillen voor een account-SAS en een service-SAS.
* **IP-ADRES.** Een optionele parameter waarmee een IP-adres of een bereik met IP-adressen buiten Azure (Zie de sectie Hallo [routering configuratie sessiestatus](../../expressroute/expressroute-workflows.md#routing-session-configuration-state) voor Express Route) uit welke tooaccept-aanvragen.
* **Protocol.** Een optionele parameter waarmee Hallo protocol toegestaan voor een aanvraag. Mogelijke waarden zijn zowel HTTP als HTTPS (`https,http`), wordt de standaardwaarde Hallo- of HTTPS (`https`). Houd er rekening mee dat HTTP alleen geen toegestane waarde is.
* **Handtekening.** Hallo-handtekening is samengesteld uit Hallo andere parameters opgegeven als deel token, en vervolgens versleuteld. Deze tooauthenticate Hallo SAS gebruikt.

### <a name="parameters-for-a-service-sas-token"></a>Parameters voor een service-SAS-token
* **Storage-resource.** Storage-resources die u kunt toegang met een service te delegeren SAS zijn onder andere:
  * Containers en blobs
  * Bestandsshares en bestanden
  * Wachtrijen
  * Tabellen en -bereiken van de tabelentiteiten.

### <a name="parameters-for-an-account-sas-token"></a>Parameters voor een account-SAS-token
* **De service of services.** Een account-SAS delegeert toegang tooone of meer van de opslagservices Hallo. U kunt bijvoorbeeld een account-SAS of gemachtigden toegang toohello Blob en het bestand service tot maken. Of u een SAS of gemachtigden toegang hebt tot vier services tooall (Blob, Queue, Table en -bestand) kunt maken.
* **Opslag resourcetypen.** Een account-SAS geldt tooone of meer klassen van opslagbronnen in plaats van een specifieke bron. U kunt een account SAS toodelegate toegang te maken:
  * Serviceniveau-API's, die worden aangeroepen voor Hallo storage account resource. Voorbeelden zijn onder meer **Get/Set-Service-eigenschappen**, **ophalen Service statistieken**, en **lijst Containers/wachtrijen/tabellen, Shares**.
  * Niveau van de container-API's, die tegen Hallo containerobjecten worden aangeroepen voor elke service: blob-containers, wachtrijen, tabellen en bestandsshares. Voorbeelden zijn **maken/verwijderen Container**, **wachtrij maken/verwijderen**, **maken/verwijderen tabel**, **Share maken/verwijderen**, en  **Blobs/bestanden en mappen weergeven**.
  * Op objectniveau API's, die worden aangeroepen voor blobs, Wachtrijberichten, tabelentiteiten en bestanden. Bijvoorbeeld: **Blob plaatsen**, **Query entiteit**, **berichten ophalen**, en **bestand maken**.

## <a name="examples-of-sas-uris"></a>Voorbeelden van SAS-URI 's

### <a name="service-sas-uri-example"></a>Voorbeeld van de service-SAS-URI

Hier volgt een voorbeeld van een SAS-URI die biedt lezen en schrijven machtigingen tooa blob-service. Hallo tabel uitsplitsing van elk deel van Hallo URI toounderstand hoe het bijdraagt toohello SAS:

```
https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2015-04-05&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D
```

| Naam | SAS gedeelte | Beschrijving |
| --- | --- | --- |
| BLOB-URI |`https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt` |Hallo-adres van Hallo blob. Houd er rekening mee dat via HTTPS wordt sterk aanbevolen. |
| Storage services versie |`sv=2015-04-05` |Voor services versie 2012-02-12-opslag en later Hallo versie toouse door deze parameter wordt aangegeven. |
| Begintijd |`st=2015-04-29T22%3A18%3A26Z` |Opgegeven in UTC-tijd. Als u Hallo SAS toobe geldig onmiddellijk wilt, weglaten Hallo begintijd. |
| Verlooptijd |`se=2015-04-30T02%3A23%3A26Z` |Opgegeven in UTC-tijd. |
| Resource |`sr=b` |Hallo-bron is een blob. |
| Machtigingen |`sp=rw` |Hallo machtigingen verleend door Hallo SAS Read (r) opnemen en (b) schrijven. |
| IP-bereik |`sip=168.1.5.60-168.1.5.70` |Hallo bereik van IP-adressen waaruit een aanvraag wordt geaccepteerd. |
| Protocol |`spr=https` |Alleen-aanvragen via HTTPS zijn toegestaan. |
| Handtekening |`sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D` |Tooauthenticate toegang toohello blob wordt gebruikt. Hallo-handtekening is een HMAC berekend over een tekenreeks te ondertekenen en de sleutel met behulp van de algoritme SHA256 hello en vervolgens gecodeerd met Base64-codering. |

### <a name="account-sas-uri-example"></a>Voorbeeld van account-SAS-URI

Hier volgt een voorbeeld van een SAS-account dat wordt gebruikt dezelfde algemene parameters op Hallo token Hallo. Sinds deze parameters hierboven zijn beschreven, worden ze hier niet beschreven. Alleen Hallo parameters die zijn specifieke tooaccount die SAS in Hallo onderstaande tabel worden beschreven.

```
https://myaccount.blob.core.windows.net/?restype=service&comp=properties&sv=2015-04-05&ss=bf&srt=s&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=F%6GRVAZ5Cdj2Pw4tgU7IlSTkWgn7bUkkAg8P6HESXwmf%4B
```

| Naam | SAS gedeelte | Beschrijving |
| --- | --- | --- |
| Resource-URI |`https://myaccount.blob.core.windows.net/?restype=service&comp=properties` |Hallo eindpunt Blob-service, en de parameters voor service-eigenschappen (als deze wordt aangeroepen met GET) ophalen of instellen van eigenschappen (als deze wordt aangeroepen met SET) van de service. |
| Services |`ss=bf` |Hallo SAS bestands- en toohello Blob is van toepassing |
| Brontypen |`srt=s` |Hallo SAS geldt tooservice serviceniveaubewerkingen. |
| Machtigingen |`sp=rw` |Hallo machtigingen verlenen toegang tooread- en schrijfbewerkingen. |

Gezien het feit dat machtigingen zijn beperkt toohello serviceniveau, toegankelijk bewerkingen met deze SAS zijn **Blob-Service-eigenschappen ophalen** (gelezen) en **Blob-Service-eigenschappen instellen** (schrijven). Met een andere resource URI hello dezelfde SAS-token kan echter ook wel toodelegate toegang te gebruikt**statistieken voor Blob-Service ophalen** (gelezen).

## <a name="controlling-a-sas-with-a-stored-access-policy"></a>Een SAS met een opgeslagen-beleid beheren
Een shared access signature kan duren voordat een van twee vormen:

* **Ad-hoc SAS:** wanneer u een ad-hoc SAS, begintijd hello, verlooptijd maken en machtigingen voor Hallo SAS zijn opgegeven in Hallo SAS-URI (of impliciet, in geval van Hallo waar de begintijd wordt weggelaten). Dit type SAS kan worden gemaakt als een account-SAS of een service-SAS.
* **SAS met opgeslagen toegangsbeleid:** een opgeslagen-beleid is gedefinieerd in een resourcecontainer een blob-container, tabel, wachtrijen of bestandsshare-- en gebruikte toomanage beperkingen voor een of meer handtekeningen voor gedeelde toegang kan worden. Als u een SAS aan een opgeslagen toegangsbeleid koppelt, overgenomen Hallo SAS Hallo beperkingen--Hallo begintijd, verlooptijd en machtigingen--gedefinieerd voor toegangsbeleid Hallo opgeslagen.

> [!NOTE]
> Op dit moment moet een SAS-account een ad-hoc SAS. Opgeslagen-beleidsregels worden nog niet ondersteund voor account-SAS.

Hallo verschil tussen twee Hallo formulieren is belangrijk voor één key '-scenario: intrekken. Omdat een SAS-URI een URL is, iedereen die Hallo verkrijgt SAS kunt gebruiken, ongeacht wie deze oorspronkelijk is gemaakt. Als een SAS openbaar wordt gepubliceerd, kan deze worden gebruikt door iedereen in Hallo wereld. Een SAS verleent toegang tooresources tooanyone beschikken deze totdat een van de vier dingen gebeurt:

1. Hallo verlooptijd opgegeven op Hallo die SAS is bereikt.
2. Hallo verlooptijd opgegeven op Hallo opgeslagen toegangsbeleid waarnaar wordt verwezen door Hallo die SAS is bereikt (als een opgeslagen-beleid wordt verwezen, en als een verlooptijd is opgegeven). Dit kan optreden omdat hello-interval is verstreken of omdat u Hallo opgeslagen toegangsbeleid met een verlooptijd in Hallo vroeger, namelijk eenrichtingssessie toorevoke Hallo SAS hebt gewijzigd.
3. Hallo toegangsbeleid waarnaar wordt verwezen door Hallo die SAS wordt verwijderd, die een andere manier toorevoke Hallo SAS is opgeslagen. Let op: als u het opnieuw maken Hallo opgeslagen toegangsbeleid met exact dezelfde naam, alle bestaande SAS Hallo tokens zal opnieuw worden geldig volgens toohello machtigingen die zijn gekoppeld aan deze opgeslagen toegangsbeleid (ervan uitgaande dat Hallo verlooptijd op Hallo SAS is niet verstreken). Als u toorevoke Hallo SAS zijn wilde, worden toouse ervoor dat een andere naam op als u het Hallo-beleid met een verlooptijd in toekomstige Hallo opnieuw maken.
4. Hallo accountsleutel die gebruikt toocreate Hallo SAS is wordt gegenereerd. De accountsleutel van een opnieuw gegenereerd, wordt alle toepassingsonderdelen met die sleutel toofail tooauthenticate totdat ze zijn bijgewerkt toouse ofwel Hallo andere geldig accountsleutel of Hallo account zojuist opnieuw gegenereerd.

> [!IMPORTANT]
> Een shared access signature-URI is gekoppeld aan Hallo account key gebruikte toocreate Hallo handtekening en Hallo opgeslagen toegangsbeleid dat is gekoppeld (indien aanwezig). Als er geen opgeslagen toegangsbeleid is opgegeven, is hello alleen manier toorevoke een shared access signature toochange hello accountsleutel.

## <a name="authenticating-from-a-client-application-with-a-sas"></a>Verificatie van een clienttoepassing met een SAS
Een client die in bezit van een SAS kunt Hallo SAS tooauthenticate een aanvraag in voor een opslagaccount waarvoor ze geen Hallo toegangscodes bezitten. Een SAS worden opgenomen in een verbindingsreeks, of gebruik rechtstreeks vanuit de juiste Hallo-constructor of methode.

### <a name="using-a-sas-in-a-connection-string"></a>Met behulp van een SAS in een verbindingsreeks
[!INCLUDE [storage-use-sas-in-connection-string-include](../../../includes/storage-use-sas-in-connection-string-include.md)]

### <a name="using-a-sas-in-a-constructor-or-method"></a>Met behulp van een SAS in een constructor of methode
Verschillende Azure Storage client bibliotheek constructors en methode overloads bieden een SAS-parameter, zodat u kunt een aanvraag toohello-service met een SAS verifiëren.

Bijvoorbeeld, is hier een SAS-URI gebruikte toocreate een verwijzing tooa blok-blob. Hallo SAS biedt alleen Hallo-referenties die nodig zijn voor Hallo-aanvraag. Hallo blok-blobverwijzing wordt vervolgens gebruikt voor een schrijfbewerking:

```csharp
string sasUri = "https://storagesample.blob.core.windows.net/sample-container/" +
    "sampleBlob.txt?sv=2015-07-08&sr=b&sig=39Up9JzHkxhUIhFEjEH9594DJxe7w6cIRCg0V6lCGSo%3D" +
    "&se=2016-10-18T21%3A51%3A37Z&sp=rcw";

CloudBlockBlob blob = new CloudBlockBlob(new Uri(sasUri));

// Create operation: Upload a blob with hello specified name toohello container.
// If hello blob does not exist, it will be created. If it does exist, it will be overwritten.
try
{
    MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    msWrite.Position = 0;
    using (msWrite)
    {
        await blob.UploadFromStreamAsync(msWrite);
    }

    Console.WriteLine("Create operation succeeded for SAS {0}", sasUri);
    Console.WriteLine();
}
catch (StorageException e)
{
    if (e.RequestInformation.HttpStatusCode == 403)
    {
        Console.WriteLine("Create operation failed for SAS {0}", sasUri);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    else
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}

```

## <a name="best-practices-when-using-sas"></a>Aanbevolen procedures voor via SAS
Wanneer u handtekeningen voor gedeelde toegang in uw toepassingen gebruikt, moet u toobe op de hoogte van de twee mogelijke risico's:

* Als een SAS is gelekt, kan deze worden gebruikt door iedereen die verkrijgt, die mogelijk uw storage-account kan vormen.
* Als een SAS-clienttoepassing tooa vervalt en toepassing hello niet kan tooretrieve een nieuwe SAS van uw service hebt opgegeven, kan de functionaliteit van de toepassing hello worden gehinderd.

Hallo kunnen volgende aanbevelingen voor het gebruik van handtekeningen voor gedeelde toegang helpen deze risico's verminderen:

1. **Altijd gebruik van HTTPS** toocreate of een SAS te verdelen. Als een SAS doorgegeven via HTTP en onderschept, een aanvaller uitvoeren van een man-in-the-middle-aanval kunnen tooread Hallo SAS en gebruiken zoals Hallo bedoeld gebruiker kan bijvoorbeeld mogelijk inbreuk op gevoelige gegevens of waardoor het beschadigde gegevens door Hallo kwaadwillende gebruiker.
2. **Verwijzing opgeslagen toegangsbeleid waar mogelijk.** Toegang beleidsregels geven u optie toorevoke machtigingen Hallo zonder tooregenerate hello opslagaccountsleutels opgeslagen. Instellen dat verlopen Hallo op deze zeer veel verdiept in het Hallo toekomstige (of oneindige) en zorg ervoor dat deze regelmatig bijgewerkt toomove heeft verder in toekomstige Hallo.
3. **Korte termijn verlopen keren gebruiken op een ad-hoc SAS.** Op deze manier, zelfs als een SAS is geknoeid, is dit alleen geldig voor een korte periode. Deze procedure is vooral belangrijk als u niet verwijzen naar een opgeslagen toegangsbeleid. Korte termijn verlopen keren Hallo hoeveelheid gegevens die worden tooa blob geschreven kunnen door te beperken Hallo tijd beschikbaar tooupload tooit ook worden beperkt.
4. **Clients automatisch vernieuwen Hallo SAS indien nodig hebt.** Clients moeten vernieuwen Hallo SAS goed voordat Hallo verlopen, in volgorde tooallow tijd voor nieuwe pogingen als Hallo-service met de Hallo SAS niet beschikbaar is. Als uw SAS is gebruikt voor een klein aantal onmiddellijke toobe bedoeld, tijdelijke bewerkingen die zijn voltooid binnen de verloopperiode Hallo toobe verwacht, wordt dit mogelijk overbodig zoals Hallo die SAS niet is vernieuwd toobe verwacht. Echter, hebt u een client die regelmatig aanvragen via SAS maakt, vervolgens Hallo mogelijkheid van verlopen binnenkomt in play. Hallo belangrijkste overweging is toobalance Hallo nodig voor Hallo SAS toobe tijdelijke (zoals eerder vermeld) met Hallo nodig tooensure die Hallo van client vernieuwing vroeg vraagt voldoende (tooavoid wordt onderbroken vanwege toohello SAS verlopende voorafgaande toosuccessful vernieuwen).
5. **Wees voorzichtig met SAS-begintijd.** Als u Hallo starttijd voor een SAS te instellen**nu**, en vervolgens vanwege tooclock tijdverschil (verschillen in de huidige tijd op basis van toodifferent machines), fouten kunnen worden waargenomen afwisselend voor Hallo eerste enkele minuten. In het algemeen ingesteld Hallo start tijd toobe ten minste 15 minuten in de afgelopen Hallo. Of niet zijn ingesteld dat deze, waarmee u het geldige direct in alle gevallen. Hallo geldt doorgaans ook--tooexpiry tijd Vergeet niet dat u waarnemen up too15 minuten klok scheeftrekken in beide richtingen op een aanvraag. Hallo maximale duur van een SAS die niet verwijst naar een opgeslagen toegangsbeleid is voor clients met behulp van een REST versie voorafgaande too2012-02-12, 1 uur en alle regels voor het opgeven van de lange termijn dan die zal mislukken.
6. **Specifieke met Hallo resource toobe toegankelijk zijn.** Aanbevolen beveiligingsprocedure is een gebruiker met de minimale vereiste bevoegdheden Hallo tooprovide. Als een gebruiker alleen leestoegang tooa één entiteit moet, verleen hen leestoegang toothat één entiteit en niet lezen, schrijven, verwijderen toegang tooall entiteiten. Hierdoor kunnen ook verkleinen Hallo schade, als er een SAS is geknoeid omdat Hallo SAS minder stroom in handen Hallo van een aanvaller heeft.
7. **Begrijpen dat uw account wordt gefactureerd voor gebruik, met inbegrip van die klaar met SAS.** Als u schrijftoegang tooa blob opgeeft, een gebruiker kan kiezen tooupload een blob 200GB. Als u een ze ook leestoegang gegeven, kiezen zij toodownload 10 keer steeds 2 TB uitgaande kost voor u. Opnieuw, Geef beperkte machtigingen toohelp verhelpen Hallo mogelijke acties van kwaadwillende gebruikers. Tijdelijke SAS tooreduce gebruiken deze bedreiging (maar houd ook rekening met het tijdsverschil op Hallo eindtijd).
8. **Gegevens die zijn geschreven met behulp van SAS valideren.** Wanneer een client-toepassing gegevens tooyour storage-account schrijft, houd er rekening mee dat er problemen met deze gegevens kunnen worden. Als uw toepassing dat gegevens worden gevalideerd of is geautoriseerd vereist voordat het klaar toouse is, moet u deze validatie uitvoeren nadat het Hallo-gegevens worden geschreven en voordat deze wordt gebruikt door uw toepassing. Deze procedure biedt ook bescherming tegen beschadigd of schadelijke gegevens tooyour-account door een gebruiker die goed verkregen Hallo SAS of door een gebruiker die misbruik van een gelekte SAS wordt geschreven.
9. **Altijd gebruik geen SAS.** Soms is Hallo risico's die zijn gekoppeld aan een bepaalde bewerking op basis van uw opslagaccount opwegen tegen Hallo voordelen van SAS. Voor dergelijke bewerkingen maken van een service voor middelste laag die tooyour storage-account schrijft na het uitvoeren van zakelijke regel validatie, verificatie en controle. Soms is ook eenvoudiger toomanage toegang op andere manieren. Bijvoorbeeld, als u toomake alle blobs in een container openbaar leesbaar wilt, kunt u Hallo container openbaar, in plaats van een SAS tooevery client geven om toegang te krijgen.
10. **Storage Analytics toomonitor uw toepassing gebruiken.** U kunt logboekregistratie en metrische gegevens tooobserve een in mislukte verificaties vanwege tooan stroomstoring in het SAS provider-service of toohello onbedoeld verwijderen van een opgeslagen-beleid pieken gebruiken. Zie Hallo [Blog van Azure Storage-Team](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx) voor meer informatie.

## <a name="sas-examples"></a>SAS-voorbeelden
Hieronder volgen enkele voorbeelden van beide typen handtekeningen voor gedeelde toegang, account-SAS en service-SAS.

toorun deze C# voorbeelden, moet u tooreference hello NuGet-pakketten in uw project te volgen:

* [Azure Storage-clientbibliotheek voor .NET](http://www.nuget.org/packages/WindowsAzure.Storage), versie 6.x of hoger (toouse account SAS).
* [Azure Configuration Manager](http://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager)

Voor meer voorbeelden die laten zien hoe toocreate en test een SAS zien [Azure codevoorbeelden voor opslag](https://azure.microsoft.com/documentation/samples/?service=storage).

### <a name="example-create-and-use-an-account-sas"></a>Voorbeeld: Maken en gebruiken van een account-SAS
Hallo volgende codevoorbeeld maakt een account-SAS die geldig is voor bestands- en Hallo Blob en biedt Hallo clientmachtigingen voor lezen, schrijven en lijstmachtigingen tooaccess serviceniveau-API's. Hallo account-SAS beperkt Hallo protocol tooHTTPS, zodat het Hallo-aanvraag moet worden uitgevoerd met HTTPS.

```csharp
static string GetAccountSASToken()
{
    // toocreate hello account SAS, you need toouse your shared key credentials. Modify for your account.
    const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

    // Create a new access policy for hello account.
    SharedAccessAccountPolicy policy = new SharedAccessAccountPolicy()
        {
            Permissions = SharedAccessAccountPermissions.Read | SharedAccessAccountPermissions.Write | SharedAccessAccountPermissions.List,
            Services = SharedAccessAccountServices.Blob | SharedAccessAccountServices.File,
            ResourceTypes = SharedAccessAccountResourceTypes.Service,
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Protocols = SharedAccessProtocol.HttpsOnly
        };

    // Return hello SAS token.
    return storageAccount.GetSharedAccessSignature(policy);
}
```

toouse Hallo account SAS tooaccess serviceniveau API's voor Hallo Blob-service, een Blob-client-object met behulp van Hallo SAS maken en Hallo eindpunt voor Blob-opslag voor uw opslagaccount.

```csharp
static void UseAccountSAS(string sasToken)
{
    // Create new storage credentials using hello SAS token.
    StorageCredentials accountSAS = new StorageCredentials(sasToken);
    // Use these credentials and hello account name toocreate a Blob service client.
    CloudStorageAccount accountWithSAS = new CloudStorageAccount(accountSAS, "account-name", endpointSuffix: null, useHttps: true);
    CloudBlobClient blobClientWithSAS = accountWithSAS.CreateCloudBlobClient();

    // Now set hello service properties for hello Blob client created with hello SAS.
    blobClientWithSAS.SetServiceProperties(new ServiceProperties()
    {
        HourMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        MinuteMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        Logging = new LoggingProperties()
        {
            LoggingOperations = LoggingOperations.All,
            RetentionDays = 14,
            Version = "1.0"
        }
    });

    // hello permissions granted by hello account SAS also permit you tooretrieve service properties.
    ServiceProperties serviceProperties = blobClientWithSAS.GetServiceProperties();
    Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
    Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
    Console.WriteLine(serviceProperties.HourMetrics.Version);
}
```

### <a name="example-create-a-stored-access-policy"></a>Voorbeeld: Een opgeslagen-beleid maken
Hallo volgende code maakt een toegangsbeleid opgeslagen in een container. U kunt Hallo toegang beleidsbeperkingen toospecify gebruiken voor een service-SAS op Hallo-container of de blobs.

```csharp
private static async Task CreateSharedAccessPolicyAsync(CloudBlobContainer container, string policyName)
{
    // Create a new shared access policy and define its constraints.
    // hello access policy provides create, write, read, list, and delete permissions.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
        // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
        SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.List |
            SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create | SharedAccessBlobPermissions.Delete
    };

    // Get hello container's existing permissions.
    BlobContainerPermissions permissions = await container.GetPermissionsAsync();

    // Add hello new policy toohello container's permissions, and set hello container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    await container.SetPermissionsAsync(permissions);
}
```

### <a name="example-create-a-service-sas-on-a-container"></a>Voorbeeld: Een SAS-service op een container maken
Hallo volgende code maakt een SAS in een container. Als Hallo-naam van een bestaande opgeslagen toegangsbeleid is opgegeven, is dat beleid gekoppeld aan Hallo SAS. Als er geen opgeslagen toegangsbeleid is opgegeven, maakt Hallo code vervolgens een ad-hoc-SAS op Hallo-container.

```csharp
private static string GetContainerSasUri(CloudBlobContainer container, string storedPolicyName = null)
{
    string sasContainerToken;

    // If no stored policy is specified, create a new access policy and define its constraints.
    if (storedPolicyName == null)
    {
        // Note that hello SharedAccessBlobPolicy class is used both toodefine hello parameters of an ad-hoc SAS, and
        // tooconstruct a shared access policy that is saved toohello container's shared access policies.
        SharedAccessBlobPolicy adHocPolicy = new SharedAccessBlobPolicy()
        {
            // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
            // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List
        };

        // Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
        sasContainerToken = container.GetSharedAccessSignature(adHocPolicy, null);

        Console.WriteLine("SAS for blob container (ad hoc): {0}", sasContainerToken);
        Console.WriteLine();
    }
    else
    {
        // Generate hello shared access signature on hello container. In this case, all of hello constraints for the
        // shared access signature are specified on hello stored access policy, which is provided by name.
        // It is also possible toospecify some constraints on an ad-hoc SAS and others on hello stored access policy.
        sasContainerToken = container.GetSharedAccessSignature(null, storedPolicyName);

        Console.WriteLine("SAS for blob container (stored access policy): {0}", sasContainerToken);
        Console.WriteLine();
    }

    // Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

### <a name="example-create-a-service-sas-on-a-blob"></a>Voorbeeld: Een SAS-service op een blob maken
Hallo volgende code maakt een SAS op een blob. Als Hallo-naam van een bestaande opgeslagen toegangsbeleid is opgegeven, is dat beleid gekoppeld aan Hallo SAS. Als er geen opgeslagen toegangsbeleid is opgegeven, maakt Hallo code vervolgens een ad-hoc-SAS op Hallo blob.

```csharp
private static string GetBlobSasUri(CloudBlobContainer container, string blobName, string policyName = null)
{
    string sasBlobToken;

    // Get a reference tooa blob within hello container.
    // Note that hello blob may not exist yet, but a SAS can still be created for it.
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    if (policyName == null)
    {
        // Create a new access policy and define its constraints.
        // Note that hello SharedAccessBlobPolicy class is used both toodefine hello parameters of an ad-hoc SAS, and
        // tooconstruct a shared access policy that is saved toohello container's shared access policies.
        SharedAccessBlobPolicy adHocSAS = new SharedAccessBlobPolicy()
        {
            // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
            // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create
        };

        // Generate hello shared access signature on hello blob, setting hello constraints directly on hello signature.
        sasBlobToken = blob.GetSharedAccessSignature(adHocSAS);

        Console.WriteLine("SAS for blob (ad hoc): {0}", sasBlobToken);
        Console.WriteLine();
    }
    else
    {
        // Generate hello shared access signature on hello blob. In this case, all of hello constraints for the
        // shared access signature are specified on hello container's stored access policy.
        sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

        Console.WriteLine("SAS for blob (stored access policy): {0}", sasBlobToken);
        Console.WriteLine();
    }

    // Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

## <a name="conclusion"></a>Conclusie
Shared access signatures zijn nuttig voor het leveren van beperkte machtigingen tooyour storage account tooclients Hallo accountsleutel niet hebben. Ze zijn als zodanig een essentieel onderdeel van het beveiligingsmodel Hallo voor elke toepassing met behulp van Azure Storage. Als u Hallo aanbevolen procedures die hier worden vermeld volgt, kunt u SAS tooprovide meer flexibiliteit van tooresources toegang in uw opslagaccount in gevaar Hallo beveiliging van uw toepassing.

## <a name="next-steps"></a>Volgende stappen
* [Anonieme leestoegang toocontainers en blobs beheren](../blobs/storage-manage-access-to-resources.md)
* [Toegang delegeren met een Shared Access Signature](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [Inleiding tot Table en Queue SAS](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
