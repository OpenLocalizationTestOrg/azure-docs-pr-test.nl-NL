---
title: aaaLog Analytics HTTP Data Collector API | Microsoft Docs
description: Kunt u Hallo Log Analytics HTTP Data Collector API tooadd POST JSON data toohello Log Analytics-opslagplaats vanaf elke client die kunt Hallo REST-API aanroepen. Dit artikel wordt beschreven hoe u toouse Hallo API en voorbeelden van hoe heeft toopublish gegevens met behulp van verschillende programmeertalen.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: c2921082831c49da764d946ac9c4fab975a38185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="send-data-toolog-analytics-with-hello-http-data-collector-api"></a>Verzenden van gegevens tooLog Analytics Hello HTTP Data Collector API
Dit artikel laat zien hoe toouse Hallo HTTP Data Collector API toosend gegevens tooLog Analytics van een REST-API-client.  Het beschrijft hoe tooformat gegevens verzameld door het script of een toepassing, opneemt in een aanvraag en die aanvraag geautoriseerd door logboekanalyse hebben.  Voorbeelden zijn bedoeld voor PowerShell, C# en Python.

## <a name="concepts"></a>Concepten
U kunt Hallo HTTP Data Collector API toosend gegevens tooLog Analytics vanaf elke client die een REST-API kan aanroepen.  Dit wordt mogelijk een runbook in Azure Automation die management verzamelt gegevens uit Azure of een andere cloud, of het mogelijk een alternatieve beheersysteem die gebruikmaakt van logboekanalyse tooconsolidate en analyseren van gegevens.

Alle gegevens in Hallo Log Analytics-bibliotheek is opgeslagen als een record met een bepaald recordtype.  U kunt uw gegevens toosend toohello HTTP Data Collector API opmaken als meerdere records in JSON.  Wanneer u hello gegevens verzenden, wordt een afzonderlijke record gemaakt in Hallo-opslagplaats voor elke record in de aanvraaglading van de Hallo.


![Overzicht van de HTTP-gegevensverzamelaar](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a>Een aanvraag maken
toouse hello HTTP gegevensverzamelaar API u maakt een POST-aanvraag met Hallo gegevens toosend in JSON JavaScript Object Notation ().  Hallo volgende drie tabellen lijst Hallo kenmerken die vereist voor elke aanvraag zijn. Elk kenmerk later in Hallo artikel nader worden beschreven.

### <a name="request-uri"></a>Aanvraag-URI
| Kenmerk | Eigenschap |
|:--- |:--- |
| Methode |VERZENDEN |
| URI |https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01 |
| Type inhoud |application/json |

### <a name="request-uri-parameters"></a>De parameters van de aanvraag-URI
| Parameter | Beschrijving |
|:--- |:--- |
| Klant-id |de unieke id voor de Microsoft Operations Management Suite-werkruimte Hallo Hallo. |
| Resource |de resourcenaam Hallo API: / api/Logboeken. |
| API-versie |Hallo-versie van Hallo API toouse aan deze aanvraag. Het is momenteel 2016-04-01. |

### <a name="request-headers"></a>Aanvraagheaders
| Koptekst | Beschrijving |
|:--- |:--- |
| Autorisatie |Hallo autorisatie handtekening. Verderop in Hallo artikel, kunt u meer informatie over het toocreate een HMAC-SHA256-header. |
| Logboek-Type |Geef Hallo recordtype Hallo-gegevens die wordt verzonden. Hallo Logboektype ondersteunt momenteel alleen alfanumerieke tekens. Het ondersteunt geen numerieke waarden of speciale tekens. |
| x-ms-datum |Hallo datum die Hallo-aanvraag is verwerkt, in RFC 1123-indeling. |
| Time-gegenereerd-veld |Hallo-naam van een veld in Hallo-gegevens die Hallo tijdstempel van gegevensitem Hallo bevat. Als u een veld opgeven en vervolgens de inhoud ervan worden gebruikt voor **TimeGenerated**. Als dit veld niet wordt opgegeven, de standaardwaarde voor Hallo **TimeGenerated** Hallo tijd is die Hallo bericht wordt ingenomen. Hallo-inhoud van het veld Hallo-bericht moeten volgen Hallo ISO 8601-notatie jjjj-MM-ssZ. |

## <a name="authorization"></a>Autorisatie
Een aanvraag toohello Log Analytics HTTP Data Collector API moet een autorisatie-header bevatten. tooauthenticate een aanvraag, moet u zich aanmelden Hallo-aanvraag met Hallo primaire of secundaire sleutel Hallo voor Hallo-werkruimte die Hallo heeft aangevraagd. Vervolgens moet die handtekening doorgegeven als onderdeel van Hallo-aanvraag.   

Hier volgt Hallo-indeling voor Hallo autorisatie-header:

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

*WorkspaceID* is de unieke id Hallo voor Hallo Operations Management Suite-werkruimte. *Handtekening* is een [HMAC Hash-based Message Authentication Code ()](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) die is gemaakt op basis van aanvraag Hallo en vervolgens wordt berekend met behulp van Hallo [algoritme SHA256](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx). Vervolgens coderen u deze met behulp van Base64-codering.

Gebruik deze indeling tooencode hello **SharedKey** handtekening tekenreeks:

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

Hier volgt een voorbeeld van een tekenreeks in handtekening:

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

Wanneer u Hallo handtekening tekenreeks, deze coderen met behulp van Hallo HMAC SHA256-algoritme op Hallo UTF-8-gecodeerde tekenreeks en vervolgens coderen Hallo resultaat als Base64. Gebruik deze indeling:

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

Hallo-voorbeelden in de volgende secties Hallo hebben voorbeeld code toohelp maken van een autorisatie-header.

## <a name="request-body"></a>Aanvraagtekst
Hallo-hoofdtekst van het Hallo-bericht moet zich in JSON. Er moet een of meer records met de eigenschap naam- en waardeparen Hallo opnemen in deze indeling:

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

U kunt meerdere records in één aanvraag samen met behulp van de volgende indeling Hallo batch. Alle Hallo records moet Hallo dezelfde recordtype.

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
},
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

## <a name="record-type-and-properties"></a>Recordtype en de eigenschappen
U kunt een aangepaste recordtype definiëren bij het indienen van gegevens via Hallo Log Analytics HTTP Data Collector API. Op dit moment kunt u kan niet schrijven gegevens tooexisting recordtypen die zijn gemaakt door andere gegevenstypen en oplossingen. Log Analytics Hallo binnenkomende gegevens leest en maakt vervolgens eigenschappen die overeenkomen met de gegevenstypen Hallo van Hallo-waarden die u invoert.

Elke aanvraag toohello Log Analytics-API moet bevatten een **Logboektype** header met de naam Hallo voor Hallo recordtype. Hallo achtervoegsel **_CL** automatisch toegevoegde toohello naam invoeren van toodistinguish uit andere logboek als een aangepast logboek typen. Bijvoorbeeld, als u Hallo naam invoeren **MyNewRecordType**, Log Analytics maakt een record met Hallo type **MyNewRecordType_CL**. Dit zorgt ervoor dat er geen conflicten tussen typenamen die door de gebruiker is gemaakt en die in de huidig of toekomstig Microsoft-oplossingen hebt verzonden zijn.

gegevenstype tooidentify een eigenschap, logboekanalyse eigenschapsnaam toohello achtervoegsel wordt toegevoegd. Als een eigenschap een null-waarde bevat, wordt Hallo-eigenschap is niet opgenomen in deze record. Deze tabel ziet u het gegevenstype van de eigenschap Hallo en bijbehorende achtervoegsel:

| Het gegevenstype eigenschap | Achtervoegsel |
|:--- |:--- |
| Tekenreeks |_K |
| Booleaanse waarde |_b |
| dubbele |_D |
| Datum/tijd |_Nauw |
| GUID |_g |

Hallo-gegevenstype dat Log Analytics voor elke eigenschap gebruikt, is afhankelijk van of Hallo recordtype voor de nieuwe record Hallo al bestaat.

* Als er recordtype Hallo niet bestaat, maakt Log Analytics een nieuwe. Log Analytics Hallo JSON type Deductie toodetermine Hallo met gegevenstype gebruikt voor elke eigenschap voor de nieuwe record Hallo.
* Als er recordtype Hallo bestaat, probeert logboekanalyse toocreate een nieuwe record op basis van bestaande eigenschappen. Als hello gegevenstype voor een eigenschap in de nieuwe record Hallo komt niet overeen met en kan niet worden geconverteerd toohello bestaande type of als hello record bevat een eigenschap die niet bestaat, maakt u een nieuwe eigenschap Log Analytics heeft dat Hallo relevante achtervoegsel.

Deze vermelding verzending zou bijvoorbeeld een record maken met drie eigenschappen **number_d**, **boolean_b**, en **string_s**:

![Voorbeeldrecord 1](media/log-analytics-data-collector-api/record-01.png)

Als u vervolgens de volgende post ingediend met alle waarden die zijn opgemaakt als tekenreeksen, zou niet Hallo eigenschappen wijzigen. Deze waarden kunnen geconverteerde tooexisting gegevenstypen zijn:

![Voorbeeldrecord 2](media/log-analytics-data-collector-api/record-02.png)

Maar als u vervolgens het volgende indienen hebt aangebracht, logboekanalyse Hallo nieuwe eigenschappen maakt **boolean_d** en **string_d**. Deze waarden kunnen niet worden geconverteerd:

![Voorbeeldrecord 3](media/log-analytics-data-collector-api/record-03.png)

Als u de volgende vermelding, voordat het Hallo-recordtype werd gemaakt Hallo vervolgens ingediend, Log Analytics maakt een record met drie eigenschappen **gunstig**, **boolean_s**, en **string_s**. In dit item is elk van de oorspronkelijke waarden Hallo opgemaakt als een tekenreeks:

![Voorbeeldrecord 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a>Gegevenslimieten
Er zijn enkele beperkingen rond Hallo gegevens toohello Log Analytics gegevensverzameling API geplaatst.

* Maximaal 30 MB per post tooLog Analytics Data Collector API. Dit is een maximale grootte voor een enkele post. Als Hallo gegevens uit een enkele post die langer is dan 30 MB, u moet splitsen Hallo gegevens up toosmaller grootte segmenten gedownload en deze gelijktijdig te verzenden.
* Maximum van 32 KB limiet voor veldwaarden. Als de veldwaarde Hallo groter dan 32 KB is, worden Hallo gegevens afgekapt.
* Aanbevolen maximumaantal velden voor een bepaald type is 50. Dit is een limiet van bruikbaarheid en zoeken ervaring perspectief.  

## <a name="return-codes"></a>Retourcodes
Hallo HTTP-statuscode 200 betekent dat Hallo-aanvraag is ontvangen voor verwerking. Hiermee wordt aangegeven die Hallo-bewerking is voltooid.

Deze tabel bevat de volledige reeks statuscodes die Hallo-service retourneert mogelijk Hallo:

| Code | Status | Foutcode | Beschrijving |
|:--- |:--- |:--- |:--- |
| 200 |OK | |Hallo-aanvraag is geaccepteerd. |
| 400 |Onjuiste aanvraag |InactiveCustomer |Hallo-werkruimte is gesloten. |
| 400 |Onjuiste aanvraag |InvalidApiVersion |Hallo API-versie die u hebt opgegeven, is niet herkend door Hallo-service. |
| 400 |Onjuiste aanvraag |InvalidCustomerId |Hallo opgegeven werkruimte-ID is ongeldig. |
| 400 |Onjuiste aanvraag |InvalidDataFormat |Ongeldige JSON is ingediend. Hallo-antwoordtekst mogelijk meer informatie over hoe tooresolve fout Hallo bevatten. |
| 400 |Onjuiste aanvraag |InvalidLogType |Hallo Logboektype opgegeven opgenomen speciale tekens of cijfers. |
| 400 |Onjuiste aanvraag |MissingApiVersion |Hallo-API-versie is niet opgegeven. |
| 400 |Onjuiste aanvraag |MissingContentType |Hallo-inhoudstype is niet opgegeven. |
| 400 |Onjuiste aanvraag |MissingLogType |Hallo vereist logboek waardetype is niet opgegeven. |
| 400 |Onjuiste aanvraag |UnsupportedContentType |Hallo-inhoudstype is niet ingesteld te**application/json**. |
| 403 |Is niet toegestaan |InvalidAuthorization |Hallo-service niet tooauthenticate Hallo-aanvraag. Controleer of deze sleutel Hallo werkruimte-ID en de verbinding zijn geldig. |
| 404 |Niet gevonden | | De opgegeven Hallo-URL is onjuist of Hallo-aanvraag is te groot. |
| 429 |Te veel aanvragen | | Hallo-service is in korte tijd een groot aantal gegevens uit uw account. Probeer het Hallo-aanvraag later opnieuw. |
| 500 |Interne serverfout |UnspecifiedError |Hallo-service heeft een interne fout. Probeer het Hallo-aanvraag. |
| 503 |Service is niet beschikbaar |ServiceUnavailable |Hallo-service is momenteel niet beschikbaar tooreceive aanvragen. Probeer uw aanvraag. |

## <a name="query-data"></a>Querygegevens
tooquery gegevens die zijn ingediend door Hallo Log Analytics HTTP Data Collector API, zoekt u records met **Type** is gelijk toohello **LogType** waarde die u hebt opgegeven, worden toegevoegd aan de **_CL**. Als u gebruikt bijvoorbeeld **MyCustomLog**, zou u alle records met geretourneerd **Type = MyCustomLog_CL**.

>[!NOTE]
> Als uw werkruimte bijgewerkte toohello is [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), Hallo hierboven query zou Wijzig toohello volgende.

> `MyCustomLog_CL`

## <a name="sample-requests"></a>Voorbeeld aanvragen
In de volgende secties hello, vindt u voorbeelden van hoe toosubmit gegevens toohello Log Analytics HTTP Data Collector API met behulp van verschillende programmeertalen.

Voor elk voorbeeld als volgt te werk tooset Hallo variabelen voor Hallo autorisatie-header:

1. Selecteer in de Operations Management Suite-portal Hallo Hallo **instellingen** tegel en selecteer vervolgens Hallo **verbonden bronnen** tabblad.
2. toohello rechts van **werkruimte-ID**Hallo kopie-pictogram en selecteer plak Hallo-ID als de waarde Hallo Hallo **klant-ID** variabele.
3. toohello rechts van **primaire sleutel**Hallo kopie-pictogram en selecteer plak Hallo-ID als de waarde Hallo Hallo **gedeelde sleutel** variabele.

U kunt ook Hallo variabelen voor Hallo Logboektype en JSON-gegevens wijzigen.

### <a name="powershell-sample"></a>PowerShell-voorbeeld
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify hello name of hello record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with hello created time for hello records
$TimeStampField = "DateValue"


# Create two records with hello same set of properties toocreate
$json = @"
[{  "StringValue": "MyString1",
    "NumberValue": 42,
    "BooleanValue": true,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "9909ED01-A74C-4874-8ABF-D2678E3AE23D"
},
{   "StringValue": "MyString2",
    "NumberValue": 43,
    "BooleanValue": false,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "8809ED01-A74C-4874-8ABF-D2678E3AE23D"
}]
"@

# Create hello function toocreate hello authorization signature
Function Build-Signature ($customerId, $sharedKey, $date, $contentLength, $method, $contentType, $resource)
{
    $xHeaders = "x-ms-date:" + $date
    $stringToHash = $method + "`n" + $contentLength + "`n" + $contentType + "`n" + $xHeaders + "`n" + $resource

    $bytesToHash = [Text.Encoding]::UTF8.GetBytes($stringToHash)
    $keyBytes = [Convert]::FromBase64String($sharedKey)

    $sha256 = New-Object System.Security.Cryptography.HMACSHA256
    $sha256.Key = $keyBytes
    $calculatedHash = $sha256.ComputeHash($bytesToHash)
    $encodedHash = [Convert]::ToBase64String($calculatedHash)
    $authorization = 'SharedKey {0}:{1}' -f $customerId,$encodedHash
    return $authorization
}


# Create hello function toocreate and post hello request
Function Post-OMSData($customerId, $sharedKey, $body, $logType)
{
    $method = "POST"
    $contentType = "application/json"
    $resource = "/api/logs"
    $rfc1123date = [DateTime]::UtcNow.ToString("r")
    $contentLength = $body.Length
    $signature = Build-Signature `
        -customerId $customerId `
        -sharedKey $sharedKey `
        -date $rfc1123date `
        -contentLength $contentLength `
        -fileName $fileName `
        -method $method `
        -contentType $contentType `
        -resource $resource
    $uri = "https://" + $customerId + ".ods.opinsights.azure.com" + $resource + "?api-version=2016-04-01"

    $headers = @{
        "Authorization" = $signature;
        "Log-Type" = $logType;
        "x-ms-date" = $rfc1123date;
        "time-generated-field" = $TimeStampField;
    }

    $response = Invoke-WebRequest -Uri $uri -Method $method -ContentType $contentType -Headers $headers -Body $body -UseBasicParsing
    return $response.StatusCode

}

# Submit hello data toohello API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a>C#-voorbeeld
```
using System;
using System.Net;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Security.Cryptography;
using System.Text;
using System.Threading.Tasks;

namespace OIAPIExample
{
    class ApiExample
    {
        // An example JSON object, with key/value pairs
        static string json = @"[{""DemoField1"":""DemoValue1"",""DemoField2"":""DemoValue2""},{""DemoField3"":""DemoValue3"",""DemoField4"":""DemoValue4""}]";

        // Update customerId tooyour Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either hello primary or hello secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of hello event type that is being submitted tooLog Analytics
        static string LogName = "DemoExample";

        // You can use an optional field toospecify hello timestamp from hello data. If hello time field is not specified, Log Analytics assumes hello time is hello message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for hello API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;

            PostData(signature, datestring, json);
        }

        // Build hello API signature
        public static string BuildSignature(string message, string secret)
        {
            var encoding = new System.Text.ASCIIEncoding();
            byte[] keyByte = Convert.FromBase64String(secret);
            byte[] messageBytes = encoding.GetBytes(message);
            using (var hmacsha256 = new HMACSHA256(keyByte))
            {
                byte[] hash = hmacsha256.ComputeHash(messageBytes);
                return Convert.ToBase64String(hash);
            }
        }

        // Send a request toohello POST API endpoint
        public static void PostData(string signature, string date, string json)
        {
            try
            {
                string url = "https://" + customerId + ".ods.opinsights.azure.com/api/logs?api-version=2016-04-01";

                System.Net.Http.HttpClient client = new System.Net.Http.HttpClient();
                client.DefaultRequestHeaders.Add("Accept", "application/json");
                client.DefaultRequestHeaders.Add("Log-Type", LogName);
                client.DefaultRequestHeaders.Add("Authorization", signature);
                client.DefaultRequestHeaders.Add("x-ms-date", date);
                client.DefaultRequestHeaders.Add("time-generated-field", TimeStampField);

                System.Net.Http.HttpContent httpContent = new StringContent(json, Encoding.UTF8);
                httpContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");
                Task<System.Net.Http.HttpResponseMessage> response = client.PostAsync(new Uri(url), httpContent);

                System.Net.Http.HttpContent responseContent = response.Result.Content;
                string result = responseContent.ReadAsStringAsync().Result;
                Console.WriteLine("Return Result: " + result);
            }
            catch (Exception excep)
            {
                Console.WriteLine("API Post Exception: " + excep.Message);
            }
        }
    }
}

```

### <a name="python-sample"></a>Python-voorbeeld
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update hello customer ID tooyour Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For hello shared key, use either hello primary or hello secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# hello log type is hello name of hello event that is being submitted
log_type = 'WebMonitorTest'

# An example JSON web monitor object
json_data = [{
   "slot_ID": 12345,
    "ID": "5cdad72f-c848-4df0-8aaa-ffe033e75d57",
    "availability_Value": 100,
    "performance_Value": 6.954,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "true"
},
{   
    "slot_ID": 67890,
    "ID": "b6bee458-fb65-492e-996d-61c4d7fbb942",
    "availability_Value": 100,
    "performance_Value": 3.379,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "false"
}]
body = json.dumps(json_data)

#####################
######Functions######  
#####################

# Build hello API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request toohello POST API
def post_data(customer_id, shared_key, body, log_type):
    method = 'POST'
    content_type = 'application/json'
    resource = '/api/logs'
    rfc1123date = datetime.datetime.utcnow().strftime('%a, %d %b %Y %H:%M:%S GMT')
    content_length = len(body)
    signature = build_signature(customer_id, shared_key, rfc1123date, content_length, method, content_type, resource)
    uri = 'https://' + customer_id + '.ods.opinsights.azure.com' + resource + '?api-version=2016-04-01'

    headers = {
        'content-type': content_type,
        'Authorization': signature,
        'Log-Type': log_type,
        'x-ms-date': rfc1123date
    }

    response = requests.post(uri,data=body, headers=headers)
    if (response.status_code >= 200 and response.status_code <= 299):
        print 'Accepted'
    else:
        print "Response code: {}".format(response.status_code)

post_data(customer_id, shared_key, body, log_type)
```

## <a name="next-steps"></a>Volgende stappen
- Gebruik Hallo [Log-API van zoekservice](log-analytics-log-search-api.md) tooretrieve gegevens van Hallo Log Analytics-opslagplaats.
