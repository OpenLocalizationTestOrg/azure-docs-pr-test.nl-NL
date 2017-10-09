---
title: aaaHow toouse Notification Hubs met behulp van Python
description: Meer informatie over hoe toouse Azure Notification Hubs vanuit een Python-back-end.
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 5640dd4a-a91e-4aa0-a833-93615bde49b4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: python
ms.devlang: php
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 21d5aaf7fc24c9936fac8e0a8de640c66c51ab0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-python"></a>Hoe toouse Notification Hubs met Python
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

U kunt alle functies van de Notification Hubs kunt openen vanaf een Java/PHP/Python/Ruby back-end Hallo Notification Hub REST-interface gebruiken, zoals beschreven in de MSDN-onderwerp Hallo [Notification Hubs REST-API's](http://msdn.microsoft.com/library/dn223264.aspx).

> [!NOTE]
> Dit is een Voorbeeldimplementatie van de referentie voor het implementeren van Hallo melding verzendt in Python en is niet officieel ondersteund meldingen Hub Python SDK Hallo.
> 
> Dit voorbeeld is geschreven met behulp van Python 3.4.
> 
> 

In dit onderwerp laten we zien hoe:

* Bouw een REST-client voor Notification Hubs-functies in Python.
* Verzenden van meldingen via Hallo Python interface toohello Notification Hub REST-API's. 
* Een dump Hallo HTTP REST/reactie op aanvragen voor foutopsporing/educatieve doel niet ophalen. 

U kunt volgen Hallo [Get gestart zelfstudie](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) voor uw mobiele platform keuze, het implementeren van Hallo back-end gedeelte in Python.

> [!NOTE]
> Hallo-bereik van Hallo voorbeeld is alleen beperkt toosend meldingen en deze bevat een registratie-management niet.
> 
> 

## <a name="client-interface"></a>Client-interface
de belangrijkste clientinterface Hallo Hallo kan bieden dezelfde methoden die beschikbaar in Hallo zijn [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx). Hierdoor kunt u toodirectly vertalen alle Hallo zelfstudies en voorbeelden die momenteel beschikbaar is op deze site en die is bijgedragen door Hallo-community op Hallo internet.

U vindt alle Hallo-code die beschikbaar zijn in Hallo [Python REST wrapper voorbeeld].

Bijvoorbeeld, toocreate een client:

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

een Windows toosend toasten we melding:

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a>Implementatie
Als u nog niet hebt gedaan, volgt u onze [Get gestart zelfstudie] -up maken van de laatste sectie toohello waar u tooimplement Hallo back-end hebt.

Alle details tooimplement een volledige REST-wrapper vindt u op Hallo [MSDN](http://msdn.microsoft.com/library/dn530746.aspx). In deze sectie wordt beschreven Hallo Python-implementatie van Hallo belangrijke stappen vereist tooaccess Notification Hubs REST-eindpunten en meldingen verzenden

1. Hallo-verbindingsreeks parseren
2. Hallo-Autorisatietoken te genereren
3. Een melding verzenden via HTTP REST-API

### <a name="parse-hello-connection-string"></a>Hallo-verbindingsreeks parseren
Hier volgt hoofdklasse Hallo Hallo-client, waarvan constructor Hallo verbindingsreeks parseert implementeren:

    class NotificationHub:
        API_VERSION = "?api-version=2013-10"
        DEBUG_SEND = "&test"

        def __init__(self, connection_string=None, hub_name=None, debug=0):
            self.HubName = hub_name
            self.Debug = debug

            # Parse connection string
            parts = connection_string.split(';')
            if len(parts) != 3:
                raise Exception("Invalid ConnectionString.")

            for part in parts:
                if part.startswith('Endpoint'):
                    self.Endpoint = 'https' + part[11:]
                if part.startswith('SharedAccessKeyName'):
                    self.SasKeyName = part[20:]
                if part.startswith('SharedAccessKey'):
                    self.SasKeyValue = part[16:]


### <a name="create-security-token"></a>Beveiligingstoken maken
Hallo-details van hello security token maken zijn beschikbaar [hier](http://msdn.microsoft.com/library/dn495627.aspx).
Hallo volgende methoden hebt toegevoegd toobe toohello **NotificationHub** klassentoken toocreate Hallo op basis van Hallo-URI van de huidige aanvraag Hallo en opgehaald uit de verbindingsreeks Hallo Hallo-referenties.

    @staticmethod
    def get_expiry():
        # By default returns an expiration of 5 minutes (=300 seconds) from now
        return int(round(time.time() + 300))

    @staticmethod
    def encode_base64(data):
        return base64.b64encode(data)

    def sign_string(self, to_sign):
        key = self.SasKeyValue.encode('utf-8')
        to_sign = to_sign.encode('utf-8')
        signed_hmac_sha256 = hmac.HMAC(key, to_sign, hashlib.sha256)
        digest = signed_hmac_sha256.digest()
        encoded_digest = self.encode_base64(digest)
        return encoded_digest

    def generate_sas_token(self):
        target_uri = self.Endpoint + self.HubName
        my_uri = urllib.parse.quote(target_uri, '').lower()
        expiry = str(self.get_expiry())
        to_sign = my_uri + '\n' + expiry
        signature = urllib.parse.quote(self.sign_string(to_sign))
        auth_format = 'SharedAccessSignature sig={0}&se={1}&skn={2}&sr={3}'
        sas_token = auth_format.format(signature, expiry, self.SasKeyName, my_uri)
        return sas_token

### <a name="send-a-notification-using-http-rest-api"></a>Een melding verzenden via HTTP REST-API
Eerste, laat gebruik definiëren een klasse die een melding vertegenwoordigt.

    class Notification:
        def __init__(self, notification_format=None, payload=None, debug=0):
            valid_formats = ['template', 'apple', 'gcm', 'windows', 'windowsphone', "adm", "baidu"]
            if not any(x in notification_format for x in valid_formats):
                raise Exception(
                    "Invalid Notification format. " +
                    "Must be one of hello following - 'template', 'apple', 'gcm', 'windows', 'windowsphone', 'adm', 'baidu'")

            self.format = notification_format
            self.payload = payload

            # array with keynames for headers
            # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
            # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry
            # in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
            self.headers = None

Deze klasse is een container voor de hoofdtekst van een systeemeigen melding of een set eigenschappen in het geval van een melding van de sjabloon, een reeks headers die-indeling (systeemeigen platform of sjabloon) en platform-specifieke eigenschappen (zoals Apple verlopen eigenschap en WNS headers) bevat .

Raadpleeg toohello [Notification Hubs REST-API's, documentatie](http://msdn.microsoft.com/library/dn495827.aspx) en specifieke notification-platforms indelingen Hallo voor alle beschikbare opties Hallo.

Nu u met deze klasse kunnen we Hallo verzenden waarschuwingsmethoden binnen Hallo schrijven **NotificationHub** klasse.

    def make_http_request(self, url, payload, headers):
        parsed_url = urllib.parse.urlparse(url)
        connection = http.client.HTTPSConnection(parsed_url.hostname, parsed_url.port)

        if self.Debug > 0:
            connection.set_debuglevel(self.Debug)
            # adding this querystring parameter gets detailed information about hello PNS send notification outcome
            url += self.DEBUG_SEND
            print("--- REQUEST ---")
            print("URI: " + url)
            print("Headers: " + json.dumps(headers, sort_keys=True, indent=4, separators=(' ', ': ')))
            print("--- END REQUEST ---\n")

        connection.request('POST', url, payload, headers)
        response = connection.getresponse()

        if self.Debug > 0:
            # print out detailed response information for debugging purpose
            print("\n\n--- RESPONSE ---")
            print(str(response.status) + " " + response.reason)
            print(response.msg)
            print(response.read())
            print("--- END RESPONSE ---")

        elif response.status != 201:
            # Successful outcome of send message is HTTP 201 - Created
            raise Exception(
                "Error sending notification. Received HTTP code " + str(response.status) + " " + response.reason)

        connection.close()

    def send_notification(self, notification, tag_or_tag_expression=None):
        url = self.Endpoint + self.HubName + '/messages' + self.API_VERSION

        json_platforms = ['template', 'apple', 'gcm', 'adm', 'baidu']

        if any(x in notification.format for x in json_platforms):
            content_type = "application/json"
            payload_to_send = json.dumps(notification.payload)
        else:
            content_type = "application/xml"
            payload_to_send = notification.payload

        headers = {
            'Content-type': content_type,
            'Authorization': self.generate_sas_token(),
            'ServiceBusNotification-Format': notification.format
        }

        if isinstance(tag_or_tag_expression, set):
            tag_list = ' || '.join(tag_or_tag_expression)
        else:
            tag_list = tag_or_tag_expression

        # add hello tags/tag expressions toohello headers collection
        if tag_list != "":
            headers.update({'ServiceBusNotification-Tags': tag_list})

        # add any custom headers toohello headers collection that hello user may have added
        if notification.headers is not None:
            headers.update(notification.headers)

        self.make_http_request(url, payload_to_send, headers)

    def send_apple_notification(self, payload, tags=""):
        nh = Notification("apple", payload)
        self.send_notification(nh, tags)

    def send_gcm_notification(self, payload, tags=""):
        nh = Notification("gcm", payload)
        self.send_notification(nh, tags)

    def send_adm_notification(self, payload, tags=""):
        nh = Notification("adm", payload)
        self.send_notification(nh, tags)

    def send_baidu_notification(self, payload, tags=""):
        nh = Notification("baidu", payload)
        self.send_notification(nh, tags)

    def send_mpns_notification(self, payload, tags=""):
        nh = Notification("windowsphone", payload)

        if "<wp:Toast>" in payload:
            nh.headers = {'X-WindowsPhone-Target': 'toast', 'X-NotificationClass': '2'}
        elif "<wp:Tile>" in payload:
            nh.headers = {'X-WindowsPhone-Target': 'tile', 'X-NotificationClass': '1'}

        self.send_notification(nh, tags)

    def send_windows_notification(self, payload, tags=""):
        nh = Notification("windows", payload)

        if "<toast>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/toast'}
        elif "<tile>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/tile'}
        elif "<badge>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/badge'}

        self.send_notification(nh, tags)

    def send_template_notification(self, properties, tags=""):
        nh = Notification("template", properties)
        self.send_notification(nh, tags)

Hallo hierboven methoden een HTTP POST-aanvraag toohello /messages eindpunt van uw notification hub, met de juiste hoofdtekst Hallo en headers toosend Hallo melding verzenden.

### <a name="using-debug-property-tooenable-detailed-logging"></a>Met behulp van foutopsporing eigenschap tooenable gedetailleerde logboekregistratie
Eigenschap debug inschakelen tijdens het initialiseren van Hallo Notification Hub wordt uitschrijven gedetailleerde logboekgegevens over Hallo HTTP-aanvraag en antwoord dump, evenals gedetailleerde melding verzenden resultaat. We hebben onlangs deze eigenschap met de naam toegevoegd [Notification Hubs TestZenden eigenschap](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) die gedetailleerde informatie over Hallo melding verzenden resultaat retourneert. toouse het - gebruik van de volgende Hallo initialiseren:

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

Hallo Notification Hub verzenden aanvraag HTTP-URL wordt toegevoegd aan een querystring 'test' als gevolg hiervan. 

## <a name="complete-tutorial"></a>Volledige Hallo-zelfstudie
U kunt nu Hallo-zelfstudie aan de slag uitvoeren met het Hallo-bericht verzenden vanuit een Python-back-end.

Uw Notification Hubs-client initialiseren (vervangen door Hallo verbindingsreeks en hubnaam verbindingsnaam volgens de instructies in Hallo [Get gestart zelfstudie]):

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

Voeg Hallo verzenden code, afhankelijk van uw mobiele doelplatform toe. Dit voorbeeld voegt ook hoger niveau methoden tooenable verzenden van meldingen op basis van Hallo platform bijvoorbeeld send_windows_notification voor windows. send_apple_notification (voor apple) enzovoort. 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a>Windows Store en Windows Phone 8.1 (zonder Silverlight)
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a>Windows Phone 8.0 en 8.1 Silverlight
    hub.send_mpns_notification(toast)

### <a name="ios"></a>iOS
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a>Android
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a>Kindle Fire
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a>Baidu
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

Uitvoeren van uw Python-code moet een melding weergegeven op het doelapparaat produceren.

## <a name="examples"></a>Voorbeelden:
### <a name="enabling-debug-property"></a>Eigenschap debug inschakelen
Wanneer u de vlag foutopsporing inschakelt tijdens het initialiseren van Hallo NotificationHub ziet u gedetailleerde HTTP-aanvraag en -antwoord dump, evenals NotificationOutcome Hallo volgende waarbij u inzicht in welke HTTP-headers worden doorgegeven in Hallo-aanvraag en welke HTTP Er is een reactie ontvangen van Hallo Notification Hub:![][1]

U ziet bijvoorbeeld gedetailleerde van resultaat van de Notification Hub 

* Wanneer het Hallo-bericht is verzonden toohello Push Notification Service. 
  
        <Outcome>hello Notification was successfully sent toohello Push Notification System</Outcome>
* Als er waren geen doelen gevonden voor een push-melding wordt u waarschijnlijk toosee Hallo volgende Hallo-reactie (waarmee wordt aangegeven dat er geen registraties toodeliver Hallo melding waarschijnlijk gevonden zijn omdat Hallo registraties hadden gaat niet-overeenkomende tags)
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-toowindows"></a>Toast-melding tooWindows-broadcast
U ziet Hallo headers die verzonden ophalen wanneer u een broadcast toast melding tooWindows client verzendt. 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a>Verzenden van meldingen geven een tag (of labelexpressie)
Kennisgeving Hallo labels HTTP-header die toohello HTTP-aanvraag wordt toegevoegd (in Hallo onderstaand voorbeeld we sturen Hallo melding alleen tooregistrations met 'Sport' payload)

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a>Meerdere labels geven melding verzenden
U ziet hoe Hallo labels HTTP-header verandert wanneer meerdere labels worden verzonden. 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a>Sjablonen melding
Hallo indeling http-header wijzigingen en Hallo nettolading instantie wordt verzonden als onderdeel van de aanvraagtekst Hallo HTTP:

**Client-side - geregistreerde sjabloon**

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

**Server side - Hallo nettolading verzenden**

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a>Volgende stappen
In dit onderwerp we hebt u geleerd hoe toocreate een eenvoudige Python REST-client voor Notification Hubs. Hier kunt u het volgende doen:

* Hallo volledige downloaden [Python REST wrapper voorbeeld], die alle Hallo code bovenstaande bevat.
* Meer informatie over Notification Hubs functie tags in Hallo gaan [nieuws op te splitsen-zelfstudie]
* Meer informatie over de functie voor Notification Hubs sjablonen gaan in Hallo [nieuws lokalisatie-zelfstudie]

<!-- URLs -->
[Python REST wrapper voorbeeld]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python
[Get gestart zelfstudie]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/
[nieuws op te splitsen-zelfstudie]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/
[nieuws lokalisatie-zelfstudie]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/

<!-- Images. -->
[1]: ./media/notification-hubs-python-backend-how-to/DetailedLoggingInfo.png
[2]: ./media/notification-hubs-python-backend-how-to/BroadcastScenario.png
[3]: ./media/notification-hubs-python-backend-how-to/SendWithOneTag.png
[4]: ./media/notification-hubs-python-backend-how-to/SendWithMultipleTags.png
[5]: ./media/notification-hubs-python-backend-how-to/TemplatedNotification.png

