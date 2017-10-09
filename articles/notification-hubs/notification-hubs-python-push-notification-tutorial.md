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
# <a name="how-toouse-notification-hubs-from-python"></a><span data-ttu-id="fbd57-103">Hoe toouse Notification Hubs met Python</span><span class="sxs-lookup"><span data-stu-id="fbd57-103">How toouse Notification Hubs from Python</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="fbd57-104">U kunt alle functies van de Notification Hubs kunt openen vanaf een Java/PHP/Python/Ruby back-end Hallo Notification Hub REST-interface gebruiken, zoals beschreven in de MSDN-onderwerp Hallo [Notification Hubs REST-API's](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="fbd57-104">You can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="fbd57-105">Dit is een Voorbeeldimplementatie van de referentie voor het implementeren van Hallo melding verzendt in Python en is niet officieel ondersteund meldingen Hub Python SDK Hallo.</span><span class="sxs-lookup"><span data-stu-id="fbd57-105">This is a sample reference implementation for implementing hello notification sends in Python and is not hello officially supported Notifications Hub Python SDK.</span></span>
> 
> <span data-ttu-id="fbd57-106">Dit voorbeeld is geschreven met behulp van Python 3.4.</span><span class="sxs-lookup"><span data-stu-id="fbd57-106">This sample is written using Python 3.4.</span></span>
> 
> 

<span data-ttu-id="fbd57-107">In dit onderwerp laten we zien hoe:</span><span class="sxs-lookup"><span data-stu-id="fbd57-107">In this topic we show how to:</span></span>

* <span data-ttu-id="fbd57-108">Bouw een REST-client voor Notification Hubs-functies in Python.</span><span class="sxs-lookup"><span data-stu-id="fbd57-108">Build a REST client for Notification Hubs features in Python.</span></span>
* <span data-ttu-id="fbd57-109">Verzenden van meldingen via Hallo Python interface toohello Notification Hub REST-API's.</span><span class="sxs-lookup"><span data-stu-id="fbd57-109">Send notifications using hello Python interface toohello Notification Hub REST APIs.</span></span> 
* <span data-ttu-id="fbd57-110">Een dump Hallo HTTP REST/reactie op aanvragen voor foutopsporing/educatieve doel niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="fbd57-110">Get a dump of hello HTTP REST request/response for debugging/educational purpose.</span></span> 

<span data-ttu-id="fbd57-111">U kunt volgen Hallo [Get gestart zelfstudie](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) voor uw mobiele platform keuze, het implementeren van Hallo back-end gedeelte in Python.</span><span class="sxs-lookup"><span data-stu-id="fbd57-111">You can follow hello [Get started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) for your mobile platform of choice, implementing hello back-end portion in Python.</span></span>

> [!NOTE]
> <span data-ttu-id="fbd57-112">Hallo-bereik van Hallo voorbeeld is alleen beperkt toosend meldingen en deze bevat een registratie-management niet.</span><span class="sxs-lookup"><span data-stu-id="fbd57-112">hello scope of hello sample is only limited toosend notifications and it doesn't do any registration management.</span></span>
> 
> 

## <a name="client-interface"></a><span data-ttu-id="fbd57-113">Client-interface</span><span class="sxs-lookup"><span data-stu-id="fbd57-113">Client interface</span></span>
<span data-ttu-id="fbd57-114">de belangrijkste clientinterface Hallo Hallo kan bieden dezelfde methoden die beschikbaar in Hallo zijn [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx).</span><span class="sxs-lookup"><span data-stu-id="fbd57-114">hello main client interface can provide hello same methods that are available in hello [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx).</span></span> <span data-ttu-id="fbd57-115">Hierdoor kunt u toodirectly vertalen alle Hallo zelfstudies en voorbeelden die momenteel beschikbaar is op deze site en die is bijgedragen door Hallo-community op Hallo internet.</span><span class="sxs-lookup"><span data-stu-id="fbd57-115">This will allow you toodirectly translate all hello tutorials and samples currently available on this site, and contributed by hello community on hello internet.</span></span>

<span data-ttu-id="fbd57-116">U vindt alle Hallo-code die beschikbaar zijn in Hallo [Python REST wrapper voorbeeld].</span><span class="sxs-lookup"><span data-stu-id="fbd57-116">You can find all hello code available in hello [Python REST wrapper sample].</span></span>

<span data-ttu-id="fbd57-117">Bijvoorbeeld, toocreate een client:</span><span class="sxs-lookup"><span data-stu-id="fbd57-117">For example, toocreate a client:</span></span>

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="fbd57-118">een Windows toosend toasten we melding:</span><span class="sxs-lookup"><span data-stu-id="fbd57-118">toosend a Windows toast notification:</span></span>

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a><span data-ttu-id="fbd57-119">Implementatie</span><span class="sxs-lookup"><span data-stu-id="fbd57-119">Implementation</span></span>
<span data-ttu-id="fbd57-120">Als u nog niet hebt gedaan, volgt u onze [Get gestart zelfstudie] -up maken van de laatste sectie toohello waar u tooimplement Hallo back-end hebt.</span><span class="sxs-lookup"><span data-stu-id="fbd57-120">If you did not already, please follow our [Get started tutorial] up toohello last section where you have tooimplement hello back-end.</span></span>

<span data-ttu-id="fbd57-121">Alle details tooimplement een volledige REST-wrapper vindt u op Hallo [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="fbd57-121">All hello details tooimplement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="fbd57-122">In deze sectie wordt beschreven Hallo Python-implementatie van Hallo belangrijke stappen vereist tooaccess Notification Hubs REST-eindpunten en meldingen verzenden</span><span class="sxs-lookup"><span data-stu-id="fbd57-122">In this section we will describe hello Python implementation of hello main steps required tooaccess Notification Hubs REST endpoints and send notifications</span></span>

1. <span data-ttu-id="fbd57-123">Hallo-verbindingsreeks parseren</span><span class="sxs-lookup"><span data-stu-id="fbd57-123">Parse hello connection string</span></span>
2. <span data-ttu-id="fbd57-124">Hallo-Autorisatietoken te genereren</span><span class="sxs-lookup"><span data-stu-id="fbd57-124">Generate hello authorization token</span></span>
3. <span data-ttu-id="fbd57-125">Een melding verzenden via HTTP REST-API</span><span class="sxs-lookup"><span data-stu-id="fbd57-125">Send a notification using HTTP REST API</span></span>

### <a name="parse-hello-connection-string"></a><span data-ttu-id="fbd57-126">Hallo-verbindingsreeks parseren</span><span class="sxs-lookup"><span data-stu-id="fbd57-126">Parse hello connection string</span></span>
<span data-ttu-id="fbd57-127">Hier volgt hoofdklasse Hallo Hallo-client, waarvan constructor Hallo verbindingsreeks parseert implementeren:</span><span class="sxs-lookup"><span data-stu-id="fbd57-127">Here is hello main class implementing hello client, whose constructor parses hello connection string:</span></span>

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


### <a name="create-security-token"></a><span data-ttu-id="fbd57-128">Beveiligingstoken maken</span><span class="sxs-lookup"><span data-stu-id="fbd57-128">Create security token</span></span>
<span data-ttu-id="fbd57-129">Hallo-details van hello security token maken zijn beschikbaar [hier](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="fbd57-129">hello details of hello security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="fbd57-130">Hallo volgende methoden hebt toegevoegd toobe toohello **NotificationHub** klassentoken toocreate Hallo op basis van Hallo-URI van de huidige aanvraag Hallo en opgehaald uit de verbindingsreeks Hallo Hallo-referenties.</span><span class="sxs-lookup"><span data-stu-id="fbd57-130">hello following methods have toobe added toohello **NotificationHub** class toocreate hello token based on hello URI of hello current request and hello credentials extracted from hello connection string.</span></span>

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

### <a name="send-a-notification-using-http-rest-api"></a><span data-ttu-id="fbd57-131">Een melding verzenden via HTTP REST-API</span><span class="sxs-lookup"><span data-stu-id="fbd57-131">Send a notification using HTTP REST API</span></span>
<span data-ttu-id="fbd57-132">Eerste, laat gebruik definiëren een klasse die een melding vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="fbd57-132">First, let use define a class representing a notification.</span></span>

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

<span data-ttu-id="fbd57-133">Deze klasse is een container voor de hoofdtekst van een systeemeigen melding of een set eigenschappen in het geval van een melding van de sjabloon, een reeks headers die-indeling (systeemeigen platform of sjabloon) en platform-specifieke eigenschappen (zoals Apple verlopen eigenschap en WNS headers) bevat .</span><span class="sxs-lookup"><span data-stu-id="fbd57-133">This class is a container for a native notification body or a set of properties in case of a template notification, a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="fbd57-134">Raadpleeg toohello [Notification Hubs REST-API's, documentatie](http://msdn.microsoft.com/library/dn495827.aspx) en specifieke notification-platforms indelingen Hallo voor alle beschikbare opties Hallo.</span><span class="sxs-lookup"><span data-stu-id="fbd57-134">Please refer toohello [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and hello specific notification platforms' formats for all hello options available.</span></span>

<span data-ttu-id="fbd57-135">Nu u met deze klasse kunnen we Hallo verzenden waarschuwingsmethoden binnen Hallo schrijven **NotificationHub** klasse.</span><span class="sxs-lookup"><span data-stu-id="fbd57-135">Now with this class, we can write hello send notification methods inside of hello **NotificationHub** class.</span></span>

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

<span data-ttu-id="fbd57-136">Hallo hierboven methoden een HTTP POST-aanvraag toohello /messages eindpunt van uw notification hub, met de juiste hoofdtekst Hallo en headers toosend Hallo melding verzenden.</span><span class="sxs-lookup"><span data-stu-id="fbd57-136">hello above methods send an HTTP POST request toohello /messages endpoint of your notification hub, with hello correct body and headers toosend hello notification.</span></span>

### <a name="using-debug-property-tooenable-detailed-logging"></a><span data-ttu-id="fbd57-137">Met behulp van foutopsporing eigenschap tooenable gedetailleerde logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="fbd57-137">Using debug property tooenable detailed logging</span></span>
<span data-ttu-id="fbd57-138">Eigenschap debug inschakelen tijdens het initialiseren van Hallo Notification Hub wordt uitschrijven gedetailleerde logboekgegevens over Hallo HTTP-aanvraag en antwoord dump, evenals gedetailleerde melding verzenden resultaat.</span><span class="sxs-lookup"><span data-stu-id="fbd57-138">Enabling debug property while initializing hello Notification Hub will write out detailed logging information about hello HTTP request and response dump as well as detailed Notification message send outcome.</span></span> <span data-ttu-id="fbd57-139">We hebben onlangs deze eigenschap met de naam toegevoegd [Notification Hubs TestZenden eigenschap](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) die gedetailleerde informatie over Hallo melding verzenden resultaat retourneert.</span><span class="sxs-lookup"><span data-stu-id="fbd57-139">We recently added this property called [Notification Hubs TestSend property](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) which returns detailed information about hello notification send outcome.</span></span> <span data-ttu-id="fbd57-140">toouse het - gebruik van de volgende Hallo initialiseren:</span><span class="sxs-lookup"><span data-stu-id="fbd57-140">toouse it - initialize using hello following:</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="fbd57-141">Hallo Notification Hub verzenden aanvraag HTTP-URL wordt toegevoegd aan een querystring 'test' als gevolg hiervan.</span><span class="sxs-lookup"><span data-stu-id="fbd57-141">hello Notification Hub Send request HTTP URL gets appended with a "test" querystring as a result.</span></span> 

## <span data-ttu-id="fbd57-142"><a name="complete-tutorial"></a>Volledige Hallo-zelfstudie</span><span class="sxs-lookup"><span data-stu-id="fbd57-142"><a name="complete-tutorial"></a>Complete hello tutorial</span></span>
<span data-ttu-id="fbd57-143">U kunt nu Hallo-zelfstudie aan de slag uitvoeren met het Hallo-bericht verzenden vanuit een Python-back-end.</span><span class="sxs-lookup"><span data-stu-id="fbd57-143">Now you can complete hello Get Started tutorial by sending hello notification from a Python back-end.</span></span>

<span data-ttu-id="fbd57-144">Uw Notification Hubs-client initialiseren (vervangen door Hallo verbindingsreeks en hubnaam verbindingsnaam volgens de instructies in Hallo [Get gestart zelfstudie]):</span><span class="sxs-lookup"><span data-stu-id="fbd57-144">Initialize your Notification Hubs client (substitute hello connection string and hub name as instructed in hello [Get started tutorial]):</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

<span data-ttu-id="fbd57-145">Voeg Hallo verzenden code, afhankelijk van uw mobiele doelplatform toe.</span><span class="sxs-lookup"><span data-stu-id="fbd57-145">Then add hello send code depending on your target mobile platform.</span></span> <span data-ttu-id="fbd57-146">Dit voorbeeld voegt ook hoger niveau methoden tooenable verzenden van meldingen op basis van Hallo platform bijvoorbeeld send_windows_notification voor windows. send_apple_notification (voor apple) enzovoort.</span><span class="sxs-lookup"><span data-stu-id="fbd57-146">This sample also adds higher level methods tooenable sending notifications based on hello platform e.g. send_windows_notification for windows; send_apple_notification (for apple) etc.</span></span> 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="fbd57-147">Windows Store en Windows Phone 8.1 (zonder Silverlight)</span><span class="sxs-lookup"><span data-stu-id="fbd57-147">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="fbd57-148">Windows Phone 8.0 en 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="fbd57-148">Windows Phone 8.0 and 8.1 Silverlight</span></span>
    hub.send_mpns_notification(toast)

### <a name="ios"></a><span data-ttu-id="fbd57-149">iOS</span><span class="sxs-lookup"><span data-stu-id="fbd57-149">iOS</span></span>
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a><span data-ttu-id="fbd57-150">Android</span><span class="sxs-lookup"><span data-stu-id="fbd57-150">Android</span></span>
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a><span data-ttu-id="fbd57-151">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="fbd57-151">Kindle Fire</span></span>
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a><span data-ttu-id="fbd57-152">Baidu</span><span class="sxs-lookup"><span data-stu-id="fbd57-152">Baidu</span></span>
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

<span data-ttu-id="fbd57-153">Uitvoeren van uw Python-code moet een melding weergegeven op het doelapparaat produceren.</span><span class="sxs-lookup"><span data-stu-id="fbd57-153">Running your Python code should produce a notification appearing on your target device.</span></span>

## <a name="examples"></a><span data-ttu-id="fbd57-154">Voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="fbd57-154">Examples:</span></span>
### <a name="enabling-debug-property"></a><span data-ttu-id="fbd57-155">Eigenschap debug inschakelen</span><span class="sxs-lookup"><span data-stu-id="fbd57-155">Enabling debug property</span></span>
<span data-ttu-id="fbd57-156">Wanneer u de vlag foutopsporing inschakelt tijdens het initialiseren van Hallo NotificationHub ziet u gedetailleerde HTTP-aanvraag en -antwoord dump, evenals NotificationOutcome Hallo volgende waarbij u inzicht in welke HTTP-headers worden doorgegeven in Hallo-aanvraag en welke HTTP Er is een reactie ontvangen van Hallo Notification Hub:![][1]</span><span class="sxs-lookup"><span data-stu-id="fbd57-156">When you enable debug flag while initializing hello NotificationHub then you will see detailed HTTP request and response dump as well as NotificationOutcome like hello following where you can understand what HTTP headers are passed in hello request and what HTTP response was received from hello Notification Hub: ![][1]</span></span>

<span data-ttu-id="fbd57-157">U ziet bijvoorbeeld gedetailleerde van resultaat van de Notification Hub</span><span class="sxs-lookup"><span data-stu-id="fbd57-157">You will see detailed Notification Hub result e.g.</span></span> 

* <span data-ttu-id="fbd57-158">Wanneer het Hallo-bericht is verzonden toohello Push Notification Service.</span><span class="sxs-lookup"><span data-stu-id="fbd57-158">when hello message is successfully sent toohello Push Notification Service.</span></span> 
  
        <Outcome>hello Notification was successfully sent toohello Push Notification System</Outcome>
* <span data-ttu-id="fbd57-159">Als er waren geen doelen gevonden voor een push-melding wordt u waarschijnlijk toosee Hallo volgende Hallo-reactie (waarmee wordt aangegeven dat er geen registraties toodeliver Hallo melding waarschijnlijk gevonden zijn omdat Hallo registraties hadden gaat niet-overeenkomende tags)</span><span class="sxs-lookup"><span data-stu-id="fbd57-159">If there were no targets found for any push notification then you are likely going toosee hello following in hello response (which indicates that there were no registrations found toodeliver hello notification probably because hello registrations had some mismatched tags)</span></span>
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-toowindows"></a><span data-ttu-id="fbd57-160">Toast-melding tooWindows-broadcast</span><span class="sxs-lookup"><span data-stu-id="fbd57-160">Broadcast toast notification tooWindows</span></span>
<span data-ttu-id="fbd57-161">U ziet Hallo headers die verzonden ophalen wanneer u een broadcast toast melding tooWindows client verzendt.</span><span class="sxs-lookup"><span data-stu-id="fbd57-161">Notice hello headers that get sent out when you are sending a broadcast toast notification tooWindows client.</span></span> 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a><span data-ttu-id="fbd57-162">Verzenden van meldingen geven een tag (of labelexpressie)</span><span class="sxs-lookup"><span data-stu-id="fbd57-162">Send notification specifying a tag (or tag expression)</span></span>
<span data-ttu-id="fbd57-163">Kennisgeving Hallo labels HTTP-header die toohello HTTP-aanvraag wordt toegevoegd (in Hallo onderstaand voorbeeld we sturen Hallo melding alleen tooregistrations met 'Sport' payload)</span><span class="sxs-lookup"><span data-stu-id="fbd57-163">Notice hello Tags HTTP header which gets added toohello HTTP request (in hello example below, we are sending hello notification only tooregistrations with 'sports' payload)</span></span>

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a><span data-ttu-id="fbd57-164">Meerdere labels geven melding verzenden</span><span class="sxs-lookup"><span data-stu-id="fbd57-164">Send notification specifying multiple tags</span></span>
<span data-ttu-id="fbd57-165">U ziet hoe Hallo labels HTTP-header verandert wanneer meerdere labels worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="fbd57-165">Notice how hello Tags HTTP header changes when multiple tags are sent.</span></span> 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a><span data-ttu-id="fbd57-166">Sjablonen melding</span><span class="sxs-lookup"><span data-stu-id="fbd57-166">Templated notification</span></span>
<span data-ttu-id="fbd57-167">Hallo indeling http-header wijzigingen en Hallo nettolading instantie wordt verzonden als onderdeel van de aanvraagtekst Hallo HTTP:</span><span class="sxs-lookup"><span data-stu-id="fbd57-167">Notice that hello Format HTTP header changes and hello payload body is sent as part of hello HTTP request body:</span></span>

<span data-ttu-id="fbd57-168">**Client-side - geregistreerde sjabloon**</span><span class="sxs-lookup"><span data-stu-id="fbd57-168">**Client side - registered template**</span></span>

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

<span data-ttu-id="fbd57-169">**Server side - Hallo nettolading verzenden**</span><span class="sxs-lookup"><span data-stu-id="fbd57-169">**Server side - sending hello payload**</span></span>

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a><span data-ttu-id="fbd57-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fbd57-170">Next Steps</span></span>
<span data-ttu-id="fbd57-171">In dit onderwerp we hebt u geleerd hoe toocreate een eenvoudige Python REST-client voor Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="fbd57-171">In this topic we showed how toocreate a simple Python REST client for Notification Hubs.</span></span> <span data-ttu-id="fbd57-172">Hier kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="fbd57-172">From here you can:</span></span>

* <span data-ttu-id="fbd57-173">Hallo volledige downloaden [Python REST wrapper voorbeeld], die alle Hallo code bovenstaande bevat.</span><span class="sxs-lookup"><span data-stu-id="fbd57-173">Download hello full [Python REST wrapper sample], which contains all hello code above.</span></span>
* <span data-ttu-id="fbd57-174">Meer informatie over Notification Hubs functie tags in Hallo gaan [nieuws op te splitsen-zelfstudie]</span><span class="sxs-lookup"><span data-stu-id="fbd57-174">Continue learning about Notification Hubs tagging feature in hello [Breaking News tutorial]</span></span>
* <span data-ttu-id="fbd57-175">Meer informatie over de functie voor Notification Hubs sjablonen gaan in Hallo [nieuws lokalisatie-zelfstudie]</span><span class="sxs-lookup"><span data-stu-id="fbd57-175">Continue learning about Notification Hubs Templates feature in hello [Localizing News tutorial]</span></span>

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

