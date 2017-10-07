---
title: aaaAzure Service Bus-verificatie met handtekeningen voor gedeelde toegang | Microsoft Docs
description: Overzicht van Service Bus-verificatie met behulp van handtekeningen voor gedeelde toegang-overzicht, informatie over SAS-verificatie met Azure Service Bus.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: 773bb11720384d7245820b56dc25b8e064ffa746
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-authentication-with-shared-access-signatures"></a>Service Bus-verificatie met handtekeningen voor gedeelde toegang

*Shared Access Signatures* (SAS) zijn de primaire beveiligingsmechanisme Hallo voor Service Bus-berichtenservice. SAS, van dit artikel wordt beschreven hoe ze werken en hoe toouse ze op een manier platform networkdirect.

SAS-verificatie kunnen toepassingen tooauthenticate tooService Bus met behulp van een toegangssleutel die is geconfigureerd op Hallo naamruimte of op Hallo messaging-entiteit (wachtrij of onderwerp) met welke specifieke rechten gekoppeld zijn. Vervolgens kunt u deze sleutel toogenerate een SAS-token dat clients op zijn beurt tooauthenticate tooService Bus kunnen gebruiken.

Ondersteuning voor SAS-verificatie is opgenomen in hello Azure SDK-versie 2.0 en hoger.

## <a name="overview-of-sas"></a>Overzicht van de SAS

Handtekeningen voor gedeelde toegang zijn een verificatiemethode op basis van beveiligde SHA-256-hashes of URI's. SAS is een zeer krachtig mechanisme dat wordt gebruikt door alle Service Bus-services. In het werkelijke gebruik SAS bestaat uit twee onderdelen: een *gedeeld toegangsbeleid* en een *Shared Access Signature* (vaak genoemd een *token*).

SAS-verificatie in Service Bus omvat het Hallo-configuratie van een cryptografische sleutel met de gekoppelde rechten van een Service Bus-resource. Clients claim toegang tooService Bus-resources in de vorm van een SAS-token. Dit token bestaat uit Hallo resource-URI wordt geopend en een ondertekend met Hallo verstrijken sleutel geconfigureerd.

U kunt de Shared Access Signature-autorisatieregels configureren op Service Bus [doorstuurt](service-bus-fundamentals-hybrid-solutions.md#relays), [wachtrijen](service-bus-fundamentals-hybrid-solutions.md#queues), en [onderwerpen](service-bus-fundamentals-hybrid-solutions.md#topics).

SAS-verificatie gebruikt Hallo volgende elementen:

* [Gedeelde toegang autorisatieregel](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule): A 256-bits primaire cryptografische sleutel in Base64-weergave, een optionele secundaire sleutel en een sleutelnaam en gekoppelde rechten (een verzameling van *luisteren*, *verzenden*, of *beheren* rechten).
* [Shared Access Signature](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) token: gegenereerd met Hallo HMAC SHA256 van een resourcetekenreeks, die bestaan uit het Hallo-URI van Hallo resource die wordt geopend en een verloopbewerking met Hallo cryptografische sleutel. Hallo handtekening en andere elementen beschreven in de volgende secties Hallo worden opgemaakt in een tekenreeks tooform Hallo SAS-token.

## <a name="shared-access-policy"></a>Beleid voor gedeelde toegang

Een toounderstand belangrijkste over SAS is dat deze met een beleid begint. Voor elk beleid dat u besluit op drie soorten informatie: **naam**, **bereik**, en **machtigingen**. Hallo **naam** is slechts; een unieke naam binnen dit bereik. Hallo bereik zijn simpel: de URI van Hallo desbetreffende Hallo. Voor een Service Bus-naamruimte is Hallo bereik Hallo volledig gekwalificeerde domeinnaam (FQDN), zoals `https://<yournamespace>.servicebus.windows.net/`.

Hallo beschikbare machtigingen voor een beleid zijn grotendeels spreken voor zich:

* Verzenden
* Luisteren
* Beheren

Nadat u Hallo beleid hebt gemaakt, krijgt het een *primaire sleutel* en een *secundaire sleutel*. Dit zijn cryptografisch sterke sleutels. Niet verliezen ze of ze lekken - ze moet altijd beschikbaar zijn in Hallo [Azure-portal][Azure portal]. U kunt een Hallo gegenereerd sleutels gebruiken en u ze op elk gewenst moment kunt opnieuw genereren. Als u opnieuw genereren of primaire sleutel in het beleid voor Hallo Hallo wijzigt, worden er handtekeningen voor gedeelde toegang gemaakt op basis van het ongeldig.

Wanneer u een Service Bus-naamruimte maakt, een beleid wordt automatisch gemaakt voor de gehele naamruimte Hallo aangeroepen **RootManageSharedAccessKey**, en alle machtigingen voor dit beleid heeft. U niet aanmelden als **hoofdmap**, zodat dit beleid niet gebruiken tenzij er een goede reden. U kunt extra beleidsregels maken in Hallo **configureren** tabblad voor de naamruimte Hallo in Hallo-portal. Het is belangrijk toonote die een niveau één tree in Service Bus (naamruimte, wachtrij, enz.) kan alleen up too12 beleid gekoppeld tooit hebben.

## <a name="configuration-for-shared-access-signature-authentication"></a>Configuratie voor Shared Access Signature-verificatie
U kunt configureren Hallo [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) -regel op de Service Bus-naamruimten, wachtrijen en onderwerpen. Configureren van een [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) in een Service Bus abonnement wordt momenteel niet ondersteund, maar u kunt regels die zijn geconfigureerd op een naamruimte of onderwerp toosecure toegang toosubscriptions gebruiken. Zie voor een werkende-voorbeeldtoepassing die u ziet u deze procedure, Hallo [met behulp van Shared Access Signature (SAS)-verificatie met Service Bus abonnementen](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c) voorbeeld.

Maximaal 12 dergelijke regels kan worden geconfigureerd op een Service Bus-naamruimte, wachtrij of onderwerp. Regels die zijn geconfigureerd op een Service Bus-naamruimte tooall entiteiten in waarmee de naamruimte van toepassing.

![SAS](./media/service-bus-sas/service-bus-namespace.png)

In deze afbeelding Hallo *manageRuleNS*, *sendRuleNS*, en *listenRuleNS* autorisatieregels tooboth wachtrij W1 en onderwerp T1, toepassen terwijl *listenRuleQ*  en *sendRuleQ* alleen tooqueue W1 toepassen en *sendRuleT* alleen tootopic T1 van toepassing is.

Hallo belangrijke parameters van een [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) zijn als volgt:

| Parameter | Beschrijving |
| --- | --- |
| *Sleutelnaam* |Een tekenreeks die Hallo-autorisatieregel beschrijft. |
| *PrimaryKey* |Een base64-gecodeerd 256-bits primaire sleutel voor ondertekening en valideren van Hallo SAS-token. |
| *Secundaire sleutel* |Een base64-gecodeerd 256-bits secundaire sleutel voor ondertekening en valideren van Hallo SAS-token. |
| *AccessRights* |Een lijst met rechten verleend door Hallo-autorisatieregel. Deze rechten kunnen worden van een verzameling van rechten luisteren, verzenden en beheren. |

Wanneer een Service Bus-naamruimte is ingericht, een [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule), met [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) instellen te**RootManageSharedAccessKey**, wordt standaard gemaakt.

## <a name="generate-a-shared-access-signature-token"></a>Genereren van een Shared Access Signature (token)

Hallo-beleid zelf is niet Hallo toegangstoken voor Service Bus. Het is Hallo-object op basis van welke Hallo toegangstoken wordt gegenereerd - met behulp van Hallo primaire of secundaire sleutel. Een client die toegang toohello ondertekeningssleutels opgegeven in de autorisatieregel voor gedeelde toegang Hallo heeft kunt Hallo SAS-token te genereren. Hallo-token wordt gegenereerd door zorgvuldig een tekenreeks in de volgende indeling Hallo:

```
SharedAccessSignature sig=<signature-string>&se=<expiry>&skn=<keyName>&sr=<URL-encoded-resourceURI>
```

Waar `signature-string` is Hallo SHA-256-hash van het Hallo-bereik van Hallo-token (**bereik** zoals beschreven in de vorige sectie Hallo) met een CRLF toegevoegd en een verlooptijd (in seconden sinds het Hallo-epoche: `00:00:00 UTC` op 1 januari 1970). 

> [!NOTE]
> tooavoid een korte token verlooptijdstip verdient het coderen van Hallo verstrijken tijd-waarde als ten minste een 32-bits geheel getal zonder teken of bij voorkeur een geheel getal zijn lange (64-bits).  
> 
> 

Hallo hash lijkt vergelijkbare toohello pseudocode te volgen en retourneert 32 bytes.

```
SHA-256('https://<yournamespace>.servicebus.windows.net/'+'\n'+ 1438205742)
```

Hallo niet gehasht waarden zijn in Hallo **SharedAccessSignature** string zodat hello ontvanger Hallo hash berekenen kunt Hello Hallo dezelfde parameters, toobe ervoor dat deze als resultaat geeft hetzelfde resultaat. Hallo URI geeft Hallo bereik en sleutelnaam Hallo Hallo beleid toobe gebruikt toocompute Hallo hash identificeert. Dit is belangrijk uit veiligheidsoverwegingen. Als het Hallo-handtekening komt niet overeen met die welke Hallo ontvanger (Service Bus) worden berekend, is toegang geweigerd. Op dit moment kunt u zeker die afzender Hallo toohello toegangssleutel had en Hallo rechten die zijn opgegeven in het Hallo-beleid moet krijgen zijn.

Houd er rekening mee dat u Hallo gecodeerd resource-URI voor deze bewerking gebruiken moet. Hallo resource-URI is Hallo die volledige URI van Hallo Service Bus toowhich brontoegang wordt geclaimd. Bijvoorbeeld: `http://<namespace>.servicebus.windows.net/<entityPath>` of `sb://<namespace>.servicebus.windows.net/<entityPath>`; dat wil zeggen, `http://contoso.servicebus.windows.net/contosoTopics/T1/Subscriptions/S3`.

Hallo autorisatieregel voor gedeelde toegang gebruikt voor de ondertekening moet worden geconfigureerd op Hallo entiteit die door deze URI of door een van de hiërarchische bovenliggende items hebt opgegeven. Bijvoorbeeld: `http://contoso.servicebus.windows.net/contosoTopics/T1` of `http://contoso.servicebus.windows.net` in het vorige voorbeeld Hallo.

Een SAS-token is geldig voor alle resources onder Hallo `<resourceURI>` gebruikt in Hallo `signature-string`.

Hallo [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) in Hallo SAS-token verwijst toohello **keyName** Hallo autorisatieregel voor gedeelde toegang toogenerate Hallo-token hebt gebruikt.

Hallo *URL-codering resourceURI* moet zijn hetzelfde als de URI die wordt gebruikt in Hallo tekenreeks te ondertekenen tijdens Hallo berekening van de handtekening Hallo HALLO hallo. Deze moet [procent gecodeerd](https://msdn.microsoft.com/library/4fkewx0t.aspx).

Het is raadzaam dat u regelmatig Hallo opnieuw sleutels gebruikt in Hallo genereert [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) object. Toepassingen in het algemeen gebruik Hallo [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) toogenerate een SAS-token. Wanneer het opnieuw genereren van sleutels hello, vervangt u Hallo [secundaire sleutel](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) met Hallo oude primaire sleutel en een nieuwe sleutel als Hallo nieuwe primaire sleutel genereren. Hiermee kunt u toocontinue tokens gebruiken voor autorisatie die zijn uitgegeven met Hallo oude primaire sleutel en die nog niet zijn verlopen.

Als een sleutel is geknoeid en u toorevoke Hallo-sleutels hebt, kunt u opnieuw genereren beide Hallo [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) en Hallo [secundaire sleutel](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) van een [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule), Vervang ze door nieuwe sleutels. Deze procedure ongeldig alle tokens die zijn ondertekend met de oude Hallo-sleutels.

## <a name="how-toouse-shared-access-signature-authentication-with-service-bus"></a>Hoe toouse Shared Access Signature-verificatie met Service Bus

Hallo volgen scenario's zijn configuratie van autorisatieregels, het genereren van SAS-tokens en Clientautorisatie.

Voor een volledig werkend voorbeeld van een Service Bus-toepassing die laat Hallo configuratie en gebruik SAS autorisatie zien, Zie [Shared Access Signature-verificatie met Service Bus](http://code.msdn.microsoft.com/Shared-Access-Signature-0a88adf8). Een gerelateerde steekproef die het illustreert Hallo gebruik van SAS-autorisatieregels geconfigureerd op de naamruimten of onderwerpen toosecure Service Bus-abonnementen is hier beschikbaar: [met behulp van Shared Access Signature (SAS)-verificatie met Service Bus-abonnementen ](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c).

## <a name="access-shared-access-authorization-rules-on-a-namespace"></a>Toegang tot gedeelde toegang autorisatieregels voor een naamruimte

Bewerkingen op basis van Hallo Service Bus-naamruimte vereist verificatie via certificaat. U moet een beheercertificaat uploaden voor uw Azure-abonnement. een beheercertificaat tooupload Hallo stappen [hier](../cloud-services/cloud-services-configure-ssl-certificate-portal.md#step-3-upload-a-certificate), met behulp van Hallo [Azure-portal][Azure portal]. Zie voor meer informatie over Azure-beheercertificaten hello [overzicht van Azure-certificaten](../cloud-services/cloud-services-certs-create.md#what-are-management-certificates).

Hallo-eindpunt voor toegang tot autorisatieregels voor gedeelde toegang voor een Service Bus-naamruimte is als volgt:

```http
https://management.core.windows.net/{subscriptionId}/services/ServiceBus/namespaces/{namespace}/AuthorizationRules/
```

toocreate een [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) object op een Service Bus-naamruimte, voert u een POST-bewerking op dit eindpunt met Hallo regelgegevens geserialiseerd als JSON of XML. Bijvoorbeeld:

```csharp
// Base address for accessing authorization rules on a namespace
string baseAddress = @"https://management.core.windows.net/<subscriptionId>/services/ServiceBus/namespaces/<namespace>/AuthorizationRules/";

// Configure authorization rule with base64-encoded 256-bit key and Send rights
var sendRule = new SharedAccessAuthorizationRule("contosoSendAll",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Send });

// Operations on hello Service Bus namespace root require certificate authentication.
WebRequestHandler handler = new WebRequestHandler
{
    ClientCertificateOptions = ClientCertificateOption.Manual
};
// Access hello management certificate by subject name
handler.ClientCertificates.Add(GetCertificate(<certificateSN>));

HttpClient httpClient = new HttpClient(handler)
{
    BaseAddress = new Uri(baseAddress)
};
httpClient.DefaultRequestHeaders.Accept.Add(
    new MediaTypeWithQualityHeaderValue("application/json"));
httpClient.DefaultRequestHeaders.Add("x-ms-version", "2015-01-01");

// Execute a POST operation on hello baseAddress above toocreate an auth rule
var postResult = httpClient.PostAsJsonAsync("", sendRule).Result;
```

Op deze manier een GET-bewerking op Hallo eindpunt tooread Hallo autorisatieregels geconfigureerd op Hallo naamruimte gebruiken.

tooupdate of een specifieke autorisatieregel verwijderen gebruiken om Hallo eindpunt te volgen:

```http
https://management.core.windows.net/{subscriptionId}/services/ServiceBus/namespaces/{namespace}/AuthorizationRules/{KeyName}
```

## <a name="access-shared-access-authorization-rules-on-an-entity"></a>Toegang tot gedeelde toegang autorisatieregels voor een entiteit

U hebt toegang tot een [Microsoft.ServiceBus.Messaging.SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) object is geconfigureerd voor een Service Bus-wachtrij of onderwerp via Hallo [AuthorizationRules](/dotnet/api/microsoft.servicebus.messaging.authorizationrules) verzameling in hello bijbehorende [QueueDescription](/dotnet/api/microsoft.servicebus.messaging.queuedescription) of [TopicDescription](/dotnet/api/microsoft.servicebus.messaging.topicdescription).

Hallo volgende code toont hoe tooadd verificatieregels voor een wachtrij.

```csharp
// Create an instance of NamespaceManager for hello operation
NamespaceManager nsm = NamespaceManager.CreateFromConnectionString(
    <connectionString> );
QueueDescription qd = new QueueDescription( <qPath> );

// Create a rule with send rights with keyName as "contosoQSendKey"
// and add it toohello queue description.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoSendKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Send }));

// Create a rule with listen rights with keyName as "contosoQListenKey"
// and add it toohello queue description.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoQListenKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Listen }));

// Create a rule with manage rights with keyName as "contosoQManageKey"
// and add it toohello queue description.
// A rule with manage rights must also have send and receive rights.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoQManageKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] {AccessRights.Manage, AccessRights.Listen, AccessRights.Send }));

// Create hello queue.
nsm.CreateQueue(qd);
```

## <a name="use-shared-access-signature-authorization"></a>Shared Access Signature-verificatie gebruiken

Toepassingen met Azure .NET SDK Hallo met Hallo Service Bus .NET-bibliotheken kunnen gebruikmaken van SAS-autorisatie via Hallo [SharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) klasse. Hallo volgende code laat zien Hallo gebruik van Hallo tokenprovider toosend berichten tooa Service Bus-wachtrij.

```csharp
Uri runtimeUri = ServiceBusEnvironment.CreateServiceUri("sb",
    <yourServiceNamespace>, string.Empty);
MessagingFactory mf = MessagingFactory.Create(runtimeUri,
    TokenProvider.CreateSharedAccessSignatureTokenProvider(keyName, key));
QueueClient sendClient = mf.CreateQueueClient(qPath);

//Sending hello message tooqueue.
BrokeredMessage helloMessage = new BrokeredMessage("Hello, Service Bus!");
helloMessage.MessageId = "SAS-Sample-Message";
sendClient.Send(helloMessage);
```

Toepassingen kunnen ook SAS gebruiken voor verificatie met behulp van een SAS-verbindingsreeks in de methoden die verbindingsreeksen accepteren.

Houd er rekening mee dat autorisatie toouse SAS met Service Bus relays, kunt u SAS-sleutels die zijn geconfigureerd op Hallo Service Bus-naamruimte. Als u expliciet een relay op Hallo-naamruimte maakt ([NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) met een [RelayDescription](/dotnet/api/microsoft.servicebus.messaging.relaydescription))-object, kunt u Hallo SAS regels alleen voor die relay opgeven. toouse SAS autorisatie met Service Bus-abonnementen, kunt u SAS-sleutels die zijn geconfigureerd op een Service Bus-naamruimte of op een onderwerp.

## <a name="use-hello-shared-access-signature-at-http-level"></a>Gebruik Hallo Shared Access Signature (op http-niveau)

Nu dat u weet hoe toocreate Shared Access Signatures voor alle entiteiten in Service Bus, u gereed tooperform een HTTP POST:

```http
POST https://<yournamespace>.servicebus.windows.net/<yourentity>/messages
Content-Type: application/json
Authorization: SharedAccessSignature sr=https%3A%2F%2F<yournamespace>.servicebus.windows.net%2F<yourentity>&sig=<yoursignature from code above>&se=1438205742&skn=KeyName
ContentType: application/atom+xml;type=entry;charset=utf-8
``` 

Denk eraan dat dit werkt voor alles. U kunt een SAS maken voor een wachtrij, onderwerp of abonnement. 

Als u een afzender of de client een SAS-token geeft, niet de Hallo sleutel rechtstreeks hebben en Hallo hash tooobtain kan niet worden omgekeerd deze. Hierdoor hebt u controle over wat ze kunnen openen en hoe lang. Een tooremember belangrijkste is dat als u de primaire sleutel Hallo in Hallo beleid wijzigt, wordt alle handtekeningen voor gedeelde toegang gemaakt op basis van het ongeldig.

## <a name="use-hello-shared-access-signature-at-amqp-level"></a>Gebruik Hallo Shared Access Signature (op AMQP niveau)

In de vorige sectie hello, hebt u gezien hoe toouse Hallo SAS-token met een HTTP POST-aanvraag voor het verzenden van gegevens toohello Service Bus. Als u weet, kunt u toegang tot Service Bus geavanceerde Message Queuing-Protocol (AMQP) die Hallo voorkeur protocol toouse voor betere prestaties in veel scenario's met behulp van Hallo. Hallo SAS-token gebruik met AMQP wordt beschreven in het document Hallo [AMQP Claim-Based Security versie 1.0](https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc) die in werkende concept sinds 2013 maar goed ondersteund door Azure vandaag.

Voordat u begint toosend gegevens tooService Bus, Hallo publisher Hallo SAS-token binnen een AMQP bericht tooa goed gedefinieerde AMQP-knooppunt met de naam moet verzenden **$cbs** (u kunt zien als een 'speciale' wachtrij die wordt gebruikt door Hallo service tooacquire en Alles valideren Hallo SAS-tokens). Hallo uitgever moet opgeven Hallo **ReplyTo** veld binnen AMQP het Hallo-bericht; dit Hallo-knooppunt in welke Hallo service toohello publisher met Hallo resultaat van de validatie van Hallo tokens (een eenvoudige aanvraag/antwoordbewerking patroon tussen antwoorden uitgever en service). Dit antwoord-knooppunt wordt gemaakt 'aan' hello snel,' over 'dynamische maken van het externe knooppunt' spreken, zoals beschreven door Hallo AMQP 1.0-specificatie. Nadat u hebt gecontroleerd dat Hallo SAS-token is geldig, Hallo publisher vooruit en toosend gegevens toohello service starten.

Hallo volgende stappen laten zien hoe toosend SAS-token met AMQP-protocol met Hallo Hallo [AMQP.Net Lite](https://github.com/Azure/amqpnetlite) bibliotheek. Dit is handig als u niet Hallo officiële kunt Service Bus-SDK (bijvoorbeeld op WinRT, .net Compact Framework, .net Framework Micro en Mono) ontwikkeling in C\#. Deze bibliotheek is natuurlijk nuttig toohelp begrijpen hoe op claims gebaseerde beveiliging werkt op Hallo AMQP niveau, zoals u hebt gezien hoe het werkt op Hallo HTTP-niveau (met een HTTP POST-aanvraag en Hallo SAS-token verzonden binnen Hallo ' ' verificatieheader). Als u niet grondige kennis over AMQP hoeft, kunt u Hallo officiële Service Bus-SDK met .net Framework-toepassingen, wat het voor u doen.

### <a name="c35"></a>C&#35;

```csharp
/// <summary>
/// Send claim-based security (CBS) token
/// </summary>
/// <param name="shareAccessSignature">Shared access signature (token) toosend</param>
private bool PutCbsToken(Connection connection, string sasToken)
{
    bool result = true;
    Session session = new Session(connection);

    string cbsClientAddress = "cbs-client-reply-to";
    var cbsSender = new SenderLink(session, "cbs-sender", "$cbs");
    var cbsReceiver = new ReceiverLink(session, cbsClientAddress, "$cbs");

    // construct hello put-token message
    var request = new Message(sasToken);
    request.Properties = new Properties();
    request.Properties.MessageId = Guid.NewGuid().ToString();
    request.Properties.ReplyTo = cbsClientAddress;
    request.ApplicationProperties = new ApplicationProperties();
    request.ApplicationProperties["operation"] = "put-token";
    request.ApplicationProperties["type"] = "servicebus.windows.net:sastoken";
    request.ApplicationProperties["name"] = Fx.Format("amqp://{0}/{1}", sbNamespace, entity);
    cbsSender.Send(request);

    // receive hello response
    var response = cbsReceiver.Receive();
    if (response == null || response.Properties == null || response.ApplicationProperties == null)
    {
        result = false;
    }
    else
    {
        int statusCode = (int)response.ApplicationProperties["status-code"];
        if (statusCode != (int)HttpStatusCode.Accepted && statusCode != (int)HttpStatusCode.OK)
        {
            result = false;
        }
    }

    // hello sender/receiver may be kept open for refreshing tokens
    cbsSender.Close();
    cbsReceiver.Close();
    session.Close();

    return result;
}
```

Hallo `PutCbsToken()` methode ontvangt Hallo *verbinding* (AMQP verbinding klasse-instantie worden geleverd door Hallo [AMQP .NET Lite-bibliotheek](https://github.com/Azure/amqpnetlite)) die Hallo TCP-verbinding toohello service en Hallo vertegenwoordigt *sasToken* parameter Hallo SAS-token toosend. 

> [!NOTE]
> Het is belangrijk dat Hallo verbinding wordt gemaakt met **SASL verificatiemechanisme ingesteld tooEXTERNAL** (en niet Hallo standaard zonder opmaak met gebruikersnaam en wachtwoord die worden gebruikt wanneer u toosend Hallo SAS-token niet nodig).
> 
> 

Hallo publisher maakt vervolgens twee AMQP koppelingen voor Hallo SAS-token verzenden en ontvangen van Hallo antwoord (resultaat Hallo token validatie) van Hallo-service.

AMQP het Hallo-bericht bevat een set eigenschappen en meer informatie dan een eenvoudige bericht. Hallo SAS-token is Hallo hoofdtekst van het Hallo-bericht (met behulp van de constructor). Hallo **'ReplyTo'** eigenschap toohello knooppuntnaam voor het ontvangen van Hallo validatieresultaat op Hallo ontvanger koppeling (u kunt de naam wijzigen als u wilt en het wordt dynamisch worden gemaakt met Hallo-service) is ingesteld. Hallo laatste drie toepassing/aangepast eigenschappen worden gebruikt door Hallo service tooindicate wat van bewerking heeft tooexecute. Zoals is beschreven door Hallo CBS conceptspecificatie, moeten ze Hallo **bewerkingsnaam** ('put-token'), Hallo **type token** (in dit geval een ' servicebus.windows.net:sastoken'), en Hallo **' naam' van de doelgroep Hallo** toowhich Hallo-token is van toepassing (Hallo volledige entiteit).

Na het Hallo-SAS-token op Hallo afzender koppeling verzenden, moet de Hallo publisher Hallo-antwoorden op Hallo ontvanger koppeling lezen. Hallo-antwoord is een eenvoudige AMQP-bericht met de eigenschap van een toepassing met de naam **'statuscode'** die dezelfde als een HTTP-statuscode waarden Hallo kan bevatten.

## <a name="rights-required-for-service-bus-operations"></a>Rechten die vereist zijn voor Service Bus-bewerkingen

Hallo toont volgende tabel Hallo toegangsrechten nodig zijn voor verschillende bewerkingen voor Service Bus-resources.

| Bewerking | Claim vereist | Claim-bereik |
| --- | --- | --- |
| **Namespace** | | |
| Verificatieregel configureren op een naamruimte |Beheren |Een naamruimte-adres |
| **Service-register** | | |
| Beleid voor persoonlijke opsommen |Beheren |Een naamruimte-adres |
| Beginnen met luisteren op een naamruimte |Luisteren |Een naamruimte-adres |
| Berichten tooa listener op een naamruimte verzenden |Verzenden |Een naamruimte-adres |
| **Wachtrij** | | |
| Een wachtrij maken |Beheren |Een naamruimte-adres |
| Een wachtrij verwijderen |Beheren |Geldige wachtrij-adres |
| Wachtrijen opsommen |Beheren |Map resources/wachtrijen |
| Beschrijving van de wachtrij Hallo ophalen |Beheren |Geldige wachtrij-adres |
| Autorisatieregel voor een wachtrij configureren |Beheren |Geldige wachtrij-adres |
| In de wachtrij toohello verzenden |Verzenden |Geldige wachtrij-adres |
| Berichten ontvangen uit een wachtrij |Luisteren |Geldige wachtrij-adres |
| Afbreken of berichten voltooien na de ontvangst van het Hallo-bericht in de modus peek vergrendelen |Luisteren |Geldige wachtrij-adres |
| Een bericht voor later gebruik stellen |Luisteren |Geldige wachtrij-adres |
| Wachtrij voor onbestelbare een bericht |Luisteren |Geldige wachtrij-adres |
| Hallo-status is gekoppeld aan een sessie van de wachtrij bericht ophalen |Luisteren |Geldige wachtrij-adres |
| De status van de Hallo instellen die zijn gekoppeld aan een sessie van de wachtrij bericht |Luisteren |Geldige wachtrij-adres |
| **Onderwerp** | | |
| Een onderwerp maken |Beheren |Een naamruimte-adres |
| Een onderwerp verwijderen |Beheren |Elk adres ongeldig onderwerp |
| Onderwerpen over opsommen |Beheren |Resources: map/onderwerpen |
| Beschrijving van Hallo onderwerp ophalen |Beheren |Elk adres ongeldig onderwerp |
| Autorisatieregel voor een onderwerp configureren |Beheren |Elk adres ongeldig onderwerp |
| Toohello onderwerp verzenden |Verzenden |Elk adres ongeldig onderwerp |
| **Abonnement** | | |
| Een abonnement maken |Beheren |Een naamruimte-adres |
| Abonnement verwijderen |Beheren |.. /myTopic/Subscriptions/mySubscription |
| Abonnementen opsommen |Beheren |.. / myTopic/abonnementen |
| Beschrijving van het abonnement ophalen |Beheren |.. /myTopic/Subscriptions/mySubscription |
| Afbreken of berichten voltooien na de ontvangst van het Hallo-bericht in de modus peek vergrendelen |Luisteren |.. /myTopic/Subscriptions/mySubscription |
| Een bericht voor later gebruik stellen |Luisteren |.. /myTopic/Subscriptions/mySubscription |
| Wachtrij voor onbestelbare een bericht |Luisteren |.. /myTopic/Subscriptions/mySubscription |
| Hallo-status is gekoppeld aan een sessie onderwerp ophalen |Luisteren |.. /myTopic/Subscriptions/mySubscription |
| De status van de Hallo instellen die zijn gekoppeld aan een sessie onderwerp |Luisteren |.. /myTopic/Subscriptions/mySubscription |
| **Regels** | | |
| Een regel maken |Beheren |.. /myTopic/Subscriptions/mySubscription |
| Een regel verwijderen |Beheren |.. /myTopic/Subscriptions/mySubscription |
| Regels opsommen |Beheren of luisteren |.. /myTopic/Subscriptions/mySubscription/Rules 

## <a name="next-steps"></a>Volgende stappen

toolearn meer informatie over Service Bus-berichtenservice, Zie Hallo volgende onderwerpen.

* [Grondbeginselen van Service Bus](service-bus-fundamentals-hybrid-solutions.md)
* [Service Bus-wachtrijen, -onderwerpen en -abonnementen](service-bus-queues-topics-subscriptions.md)
* [Hoe toouse Service Bus-wachtrijen](service-bus-dotnet-get-started-with-queues.md)
* [Hoe toouse Service Bus-onderwerpen en abonnementen](service-bus-dotnet-how-to-use-topics-subscriptions.md)

[Azure portal]: https://portal.azure.com