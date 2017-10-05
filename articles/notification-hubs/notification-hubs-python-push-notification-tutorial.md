---
title: Het gebruik van Notification Hubs met behulp van Python
description: Informatie over het gebruik van Azure Notification Hubs vanuit een Python-back-end.
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
ms.openlocfilehash: 9ceedb9940759427fc8cec74a1307e42472563a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-notification-hubs-from-python"></a><span data-ttu-id="47f20-103">Het gebruik van Notification Hubs met Python</span><span class="sxs-lookup"><span data-stu-id="47f20-103">How to use Notification Hubs from Python</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="47f20-104">U kunt alle functies van de Notification Hubs kunt openen vanaf een Java/PHP/Python/Ruby back-end met de Notification Hub REST-interface, zoals beschreven in de MSDN-onderwerp [Notification Hubs REST-API's](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="47f20-104">You can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using the Notification Hub REST interface as described in the MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="47f20-105">Dit is een Voorbeeldimplementatie van de referentie voor de uitvoering van de meldingen verzendt in Python en is niet officieel ondersteund meldingen Hub Python SDK.</span><span class="sxs-lookup"><span data-stu-id="47f20-105">This is a sample reference implementation for implementing the notification sends in Python and is not the officially supported Notifications Hub Python SDK.</span></span>
> 
> <span data-ttu-id="47f20-106">Dit voorbeeld is geschreven met behulp van Python 3.4.</span><span class="sxs-lookup"><span data-stu-id="47f20-106">This sample is written using Python 3.4.</span></span>
> 
> 

<span data-ttu-id="47f20-107">In dit onderwerp laten we zien hoe:</span><span class="sxs-lookup"><span data-stu-id="47f20-107">In this topic we show how to:</span></span>

* <span data-ttu-id="47f20-108">Bouw een REST-client voor Notification Hubs-functies in Python.</span><span class="sxs-lookup"><span data-stu-id="47f20-108">Build a REST client for Notification Hubs features in Python.</span></span>
* <span data-ttu-id="47f20-109">Meldingen met de Python-interface om de Notification Hub REST-API's te verzenden.</span><span class="sxs-lookup"><span data-stu-id="47f20-109">Send notifications using the Python interface to the Notification Hub REST APIs.</span></span> 
* <span data-ttu-id="47f20-110">Een dump van de REST van de HTTP-aanvragen/reacties voor foutopsporing/educatieve doel niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="47f20-110">Get a dump of the HTTP REST request/response for debugging/educational purpose.</span></span> 

<span data-ttu-id="47f20-111">U kunt volgen de [Get gestart zelfstudie](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) implementeren voor uw mobiele platform van de keuze van het back-end-gedeelte in Python.</span><span class="sxs-lookup"><span data-stu-id="47f20-111">You can follow the [Get started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) for your mobile platform of choice, implementing the back-end portion in Python.</span></span>

> [!NOTE]
> <span data-ttu-id="47f20-112">Het bereik van de steekproef wordt alleen beperkt om meldingen te verzenden en deze bevat een registratie-management niet.</span><span class="sxs-lookup"><span data-stu-id="47f20-112">The scope of the sample is only limited to send notifications and it doesn't do any registration management.</span></span>
> 
> 

## <a name="client-interface"></a><span data-ttu-id="47f20-113">Client-interface</span><span class="sxs-lookup"><span data-stu-id="47f20-113">Client interface</span></span>
<span data-ttu-id="47f20-114">De belangrijkste clientinterface kan bieden dezelfde methoden die beschikbaar zijn in de [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx).</span><span class="sxs-lookup"><span data-stu-id="47f20-114">The main client interface can provide the same methods that are available in the [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx).</span></span> <span data-ttu-id="47f20-115">Dit kunt u rechtstreeks vertalen de zelfstudies en voorbeelden die momenteel beschikbaar is op deze site en die is bijgedragen door de community op het internet.</span><span class="sxs-lookup"><span data-stu-id="47f20-115">This will allow you to directly translate all the tutorials and samples currently available on this site, and contributed by the community on the internet.</span></span>

<span data-ttu-id="47f20-116">U vindt de code die zijn beschikbaar in de [Python REST wrapper voorbeeld].</span><span class="sxs-lookup"><span data-stu-id="47f20-116">You can find all the code available in the [Python REST wrapper sample].</span></span>

<span data-ttu-id="47f20-117">Als u bijvoorbeeld wilt maken van een client:</span><span class="sxs-lookup"><span data-stu-id="47f20-117">For example, to create a client:</span></span>

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="47f20-118">Verzenden van een pop-upmelding voor Windows:</span><span class="sxs-lookup"><span data-stu-id="47f20-118">To send a Windows toast notification:</span></span>

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a><span data-ttu-id="47f20-119">Implementatie</span><span class="sxs-lookup"><span data-stu-id="47f20-119">Implementation</span></span>
<span data-ttu-id="47f20-120">Als u nog niet hebt gedaan, volgt u onze [Get gestart zelfstudie] omhoog naar de laatste sectie waar u hebt voor het implementeren van de back-end.</span><span class="sxs-lookup"><span data-stu-id="47f20-120">If you did not already, please follow our [Get started tutorial] up to the last section where you have to implement the back-end.</span></span>

<span data-ttu-id="47f20-121">De details voor het implementeren van een volledige REST-wrapper vindt u op [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="47f20-121">All the details to implement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="47f20-122">In deze sectie worden beschreven de Python-implementatie van de belangrijkste stappen die nodig zijn voor toegang tot Notification Hubs REST-eindpunten en meldingen verzenden</span><span class="sxs-lookup"><span data-stu-id="47f20-122">In this section we will describe the Python implementation of the main steps required to access Notification Hubs REST endpoints and send notifications</span></span>

1. <span data-ttu-id="47f20-123">De verbindingsreeks parseren</span><span class="sxs-lookup"><span data-stu-id="47f20-123">Parse the connection string</span></span>
2. <span data-ttu-id="47f20-124">Het verificatietoken genereren</span><span class="sxs-lookup"><span data-stu-id="47f20-124">Generate the authorization token</span></span>
3. <span data-ttu-id="47f20-125">Een melding verzenden via HTTP REST-API</span><span class="sxs-lookup"><span data-stu-id="47f20-125">Send a notification using HTTP REST API</span></span>

### <a name="parse-the-connection-string"></a><span data-ttu-id="47f20-126">De verbindingsreeks parseren</span><span class="sxs-lookup"><span data-stu-id="47f20-126">Parse the connection string</span></span>
<span data-ttu-id="47f20-127">Dit is de hoofdklasse uitvoering van de client, waarvan constructor de verbindingsreeks parseert:</span><span class="sxs-lookup"><span data-stu-id="47f20-127">Here is the main class implementing the client, whose constructor parses the connection string:</span></span>

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


### <a name="create-security-token"></a><span data-ttu-id="47f20-128">Beveiligingstoken maken</span><span class="sxs-lookup"><span data-stu-id="47f20-128">Create security token</span></span>
<span data-ttu-id="47f20-129">De details van het token maken voor beveiliging zijn beschikbaar [hier](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="47f20-129">The details of the security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="47f20-130">De volgende methoden moeten worden toegevoegd aan de **NotificationHub** klasse te maken van het token op basis van de URI van de huidige aanvraag en de referenties die zijn opgehaald uit de verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="47f20-130">The following methods have to be added to the **NotificationHub** class to create the token based on the URI of the current request and the credentials extracted from the connection string.</span></span>

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

### <a name="send-a-notification-using-http-rest-api"></a><span data-ttu-id="47f20-131">Een melding verzenden via HTTP REST-API</span><span class="sxs-lookup"><span data-stu-id="47f20-131">Send a notification using HTTP REST API</span></span>
<span data-ttu-id="47f20-132">Eerste, laat gebruik definiëren een klasse die een melding vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="47f20-132">First, let use define a class representing a notification.</span></span>

    class Notification:
        def __init__(self, notification_format=None, payload=None, debug=0):
            valid_formats = ['template', 'apple', 'gcm', 'windows', 'windowsphone', "adm", "baidu"]
            if not any(x in notification_format for x in valid_formats):
                raise Exception(
                    "Invalid Notification format. " +
                    "Must be one of the following - 'template', 'apple', 'gcm', 'windows', 'windowsphone', 'adm', 'baidu'")

            self.format = notification_format
            self.payload = payload

            # array with keynames for headers
            # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
            # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry
            # in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
            self.headers = None

<span data-ttu-id="47f20-133">Deze klasse is een container voor de hoofdtekst van een systeemeigen melding of een set eigenschappen in het geval van een melding van de sjabloon, een reeks headers die-indeling (systeemeigen platform of sjabloon) en platform-specifieke eigenschappen (zoals Apple verlopen eigenschap en WNS headers) bevat .</span><span class="sxs-lookup"><span data-stu-id="47f20-133">This class is a container for a native notification body or a set of properties in case of a template notification, a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="47f20-134">Raadpleeg de [Notification Hubs REST-API's, documentatie](http://msdn.microsoft.com/library/dn495827.aspx) en de specifieke notification-platforms worden gebruikt voor alle beschikbare opties.</span><span class="sxs-lookup"><span data-stu-id="47f20-134">Please refer to the [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and the specific notification platforms' formats for all the options available.</span></span>

<span data-ttu-id="47f20-135">Nu u met deze klasse kunnen we de verzenden waarschuwingsmethoden binnen van schrijven de **NotificationHub** klasse.</span><span class="sxs-lookup"><span data-stu-id="47f20-135">Now with this class, we can write the send notification methods inside of the **NotificationHub** class.</span></span>

    def make_http_request(self, url, payload, headers):
        parsed_url = urllib.parse.urlparse(url)
        connection = http.client.HTTPSConnection(parsed_url.hostname, parsed_url.port)

        if self.Debug > 0:
            connection.set_debuglevel(self.Debug)
            # adding this querystring parameter gets detailed information about the PNS send notification outcome
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

        # add the tags/tag expressions to the headers collection
        if tag_list != "":
            headers.update({'ServiceBusNotification-Tags': tag_list})

        # add any custom headers to the headers collection that the user may have added
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

<span data-ttu-id="47f20-136">De bovenstaande methoden verzenden een HTTP POST-aanvraag naar het eindpunt /messages van uw notification hub, met de juiste instantie en -koppen om de melding te verzenden.</span><span class="sxs-lookup"><span data-stu-id="47f20-136">The above methods send an HTTP POST request to the /messages endpoint of your notification hub, with the correct body and headers to send the notification.</span></span>

### <a name="using-debug-property-to-enable-detailed-logging"></a><span data-ttu-id="47f20-137">Met behulp van de eigenschap debug gedetailleerde logboekregistratie inschakelen</span><span class="sxs-lookup"><span data-stu-id="47f20-137">Using debug property to enable detailed logging</span></span>
<span data-ttu-id="47f20-138">Eigenschap debug inschakelen tijdens het initialiseren van de Notification Hub wordt schrijven gedetailleerde logboekregistratie informatie over de HTTP-aanvraag en antwoord dump, evenals gedetailleerde melding verzenden resultaat.</span><span class="sxs-lookup"><span data-stu-id="47f20-138">Enabling debug property while initializing the Notification Hub will write out detailed logging information about the HTTP request and response dump as well as detailed Notification message send outcome.</span></span> <span data-ttu-id="47f20-139">We hebben onlangs deze eigenschap met de naam toegevoegd [Notification Hubs TestZenden eigenschap](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) die gedetailleerde informatie over de melding verzenden uitkomst als resultaat gegeven.</span><span class="sxs-lookup"><span data-stu-id="47f20-139">We recently added this property called [Notification Hubs TestSend property](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) which returns detailed information about the notification send outcome.</span></span> <span data-ttu-id="47f20-140">Voor het gebruik van deze - initialiseren met behulp van de volgende:</span><span class="sxs-lookup"><span data-stu-id="47f20-140">To use it - initialize using the following:</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="47f20-141">De Notification Hub verzenden aanvraag HTTP-URL wordt toegevoegd aan een querystring 'test' als gevolg hiervan.</span><span class="sxs-lookup"><span data-stu-id="47f20-141">The Notification Hub Send request HTTP URL gets appended with a "test" querystring as a result.</span></span> 

## <span data-ttu-id="47f20-142"><a name="complete-tutorial"></a>Voltooi de zelfstudie</span><span class="sxs-lookup"><span data-stu-id="47f20-142"><a name="complete-tutorial"></a>Complete the tutorial</span></span>
<span data-ttu-id="47f20-143">U kunt nu de zelfstudie aan de slag uitvoeren met de melding verzenden vanuit een Python-back-end.</span><span class="sxs-lookup"><span data-stu-id="47f20-143">Now you can complete the Get Started tutorial by sending the notification from a Python back-end.</span></span>

<span data-ttu-id="47f20-144">Uw Notification Hubs-client initialiseren (vervangen door de verbindingsreeks en hubnaam verbindingsnaam volgens de instructies in de [Get gestart zelfstudie]):</span><span class="sxs-lookup"><span data-stu-id="47f20-144">Initialize your Notification Hubs client (substitute the connection string and hub name as instructed in the [Get started tutorial]):</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

<span data-ttu-id="47f20-145">Voeg de code verzenden, afhankelijk van uw mobiele doelplatform.</span><span class="sxs-lookup"><span data-stu-id="47f20-145">Then add the send code depending on your target mobile platform.</span></span> <span data-ttu-id="47f20-146">Dit voorbeeld voegt ook hoger niveau methoden voor het verzenden van meldingen op basis van het platform bijvoorbeeld send_windows_notification voor windows; inschakelen send_apple_notification (voor apple) enzovoort.</span><span class="sxs-lookup"><span data-stu-id="47f20-146">This sample also adds higher level methods to enable sending notifications based on the platform e.g. send_windows_notification for windows; send_apple_notification (for apple) etc.</span></span> 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="47f20-147">Windows Store en Windows Phone 8.1 (zonder Silverlight)</span><span class="sxs-lookup"><span data-stu-id="47f20-147">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="47f20-148">Windows Phone 8.0 en 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="47f20-148">Windows Phone 8.0 and 8.1 Silverlight</span></span>
    hub.send_mpns_notification(toast)

### <a name="ios"></a><span data-ttu-id="47f20-149">iOS</span><span class="sxs-lookup"><span data-stu-id="47f20-149">iOS</span></span>
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a><span data-ttu-id="47f20-150">Android</span><span class="sxs-lookup"><span data-stu-id="47f20-150">Android</span></span>
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a><span data-ttu-id="47f20-151">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="47f20-151">Kindle Fire</span></span>
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a><span data-ttu-id="47f20-152">Baidu</span><span class="sxs-lookup"><span data-stu-id="47f20-152">Baidu</span></span>
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

<span data-ttu-id="47f20-153">Uitvoeren van uw Python-code moet een melding weergegeven op het doelapparaat produceren.</span><span class="sxs-lookup"><span data-stu-id="47f20-153">Running your Python code should produce a notification appearing on your target device.</span></span>

## <a name="examples"></a><span data-ttu-id="47f20-154">Voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="47f20-154">Examples:</span></span>
### <a name="enabling-debug-property"></a><span data-ttu-id="47f20-155">Eigenschap debug inschakelen</span><span class="sxs-lookup"><span data-stu-id="47f20-155">Enabling debug property</span></span>
<span data-ttu-id="47f20-156">Wanneer u de vlag foutopsporing inschakelt tijdens het initialiseren van de NotificationHub ziet u gedetailleerde HTTP-aanvraag en antwoord dump, evenals NotificationOutcome als volgt waar u inzicht in welke HTTP-headers worden doorgegeven in de aanvraag en welke HTTP-antwoord zijn ontvangen van de Notification Hub:![][1]</span><span class="sxs-lookup"><span data-stu-id="47f20-156">When you enable debug flag while initializing the NotificationHub then you will see detailed HTTP request and response dump as well as NotificationOutcome like the following where you can understand what HTTP headers are passed in the request and what HTTP response was received from the Notification Hub: ![][1]</span></span>

<span data-ttu-id="47f20-157">U ziet bijvoorbeeld gedetailleerde van resultaat van de Notification Hub</span><span class="sxs-lookup"><span data-stu-id="47f20-157">You will see detailed Notification Hub result e.g.</span></span> 

* <span data-ttu-id="47f20-158">Wanneer het bericht is verzonden naar de Push Notification Service.</span><span class="sxs-lookup"><span data-stu-id="47f20-158">when the message is successfully sent to the Push Notification Service.</span></span> 
  
        <Outcome>The Notification was successfully sent to the Push Notification System</Outcome>
* <span data-ttu-id="47f20-159">Als er geen doelen gevonden voor een push-melding zijn vervolgens gaat u waarschijnlijk ziet het volgende in het antwoord (waarmee wordt aangegeven dat er geen registraties gevonden voor het leveren van de melding is het waarschijnlijk omdat de registraties had een niet-overeenkomende labels zijn)</span><span class="sxs-lookup"><span data-stu-id="47f20-159">If there were no targets found for any push notification then you are likely going to see the following in the response (which indicates that there were no registrations found to deliver the notification probably because the registrations had some mismatched tags)</span></span>
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-to-windows"></a><span data-ttu-id="47f20-160">Pop-upmelding naar Windows-broadcast</span><span class="sxs-lookup"><span data-stu-id="47f20-160">Broadcast toast notification to Windows</span></span>
<span data-ttu-id="47f20-161">U ziet de headers die verzonden ophalen wanneer u een broadcast pop-upmelding naar Windows-client verzendt.</span><span class="sxs-lookup"><span data-stu-id="47f20-161">Notice the headers that get sent out when you are sending a broadcast toast notification to Windows client.</span></span> 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a><span data-ttu-id="47f20-162">Verzenden van meldingen geven een tag (of labelexpressie)</span><span class="sxs-lookup"><span data-stu-id="47f20-162">Send notification specifying a tag (or tag expression)</span></span>
<span data-ttu-id="47f20-163">U ziet de labels HTTP-header die wordt toegevoegd aan de HTTP-aanvraag (in het volgende voorbeeld wordt de melding alleen naar verzendt registraties met 'Sport' nettolading)</span><span class="sxs-lookup"><span data-stu-id="47f20-163">Notice the Tags HTTP header which gets added to the HTTP request (in the example below, we are sending the notification only to registrations with 'sports' payload)</span></span>

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a><span data-ttu-id="47f20-164">Meerdere labels geven melding verzenden</span><span class="sxs-lookup"><span data-stu-id="47f20-164">Send notification specifying multiple tags</span></span>
<span data-ttu-id="47f20-165">U ziet hoe de labels HTTP-header verandert wanneer meerdere labels worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="47f20-165">Notice how the Tags HTTP header changes when multiple tags are sent.</span></span> 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a><span data-ttu-id="47f20-166">Sjablonen melding</span><span class="sxs-lookup"><span data-stu-id="47f20-166">Templated notification</span></span>
<span data-ttu-id="47f20-167">U ziet dat de indeling HTTP-header wordt gewijzigd en de hoofdtekst van de nettolading wordt verzonden als onderdeel van het hoofdgedeelte van de HTTP-aanvraag:</span><span class="sxs-lookup"><span data-stu-id="47f20-167">Notice that the Format HTTP header changes and the payload body is sent as part of the HTTP request body:</span></span>

<span data-ttu-id="47f20-168">**Client-side - geregistreerde sjabloon**</span><span class="sxs-lookup"><span data-stu-id="47f20-168">**Client side - registered template**</span></span>

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

<span data-ttu-id="47f20-169">**Server side - verzenden van de nettolading**</span><span class="sxs-lookup"><span data-stu-id="47f20-169">**Server side - sending the payload**</span></span>

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a><span data-ttu-id="47f20-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="47f20-170">Next Steps</span></span>
<span data-ttu-id="47f20-171">In dit onderwerp we hebt u geleerd hoe u een eenvoudige Python REST-client voor Notification Hubs maakt.</span><span class="sxs-lookup"><span data-stu-id="47f20-171">In this topic we showed how to create a simple Python REST client for Notification Hubs.</span></span> <span data-ttu-id="47f20-172">Hier kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="47f20-172">From here you can:</span></span>

* <span data-ttu-id="47f20-173">Downloaden van de volledige [Python REST wrapper voorbeeld], die de bovenstaande code bevat.</span><span class="sxs-lookup"><span data-stu-id="47f20-173">Download the full [Python REST wrapper sample], which contains all the code above.</span></span>
* <span data-ttu-id="47f20-174">Gaan leren over Notification Hubs tagging functie in de [nieuws op te splitsen-zelfstudie]</span><span class="sxs-lookup"><span data-stu-id="47f20-174">Continue learning about Notification Hubs tagging feature in the [Breaking News tutorial]</span></span>
* <span data-ttu-id="47f20-175">Gaan leren over de functie Notification Hubs sjablonen in de [nieuws lokalisatie-zelfstudie]</span><span class="sxs-lookup"><span data-stu-id="47f20-175">Continue learning about Notification Hubs Templates feature in the [Localizing News tutorial]</span></span>

<!-- URLs -->
<span data-ttu-id="47f20-176">[Python REST wrapper voorbeeld]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python</span><span class="sxs-lookup"><span data-stu-id="47f20-176">[Python REST wrapper sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python</span></span>
<span data-ttu-id="47f20-177">[Get gestart zelfstudie]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span><span class="sxs-lookup"><span data-stu-id="47f20-177">[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span></span>
<span data-ttu-id="47f20-178">[nieuws op te splitsen-zelfstudie]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/</span><span class="sxs-lookup"><span data-stu-id="47f20-178">[Breaking News tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/</span></span>
<span data-ttu-id="47f20-179">[nieuws lokalisatie-zelfstudie]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/</span><span class="sxs-lookup"><span data-stu-id="47f20-179">[Localizing News tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-python-backend-how-to/DetailedLoggingInfo.png
[2]: ./media/notification-hubs-python-backend-how-to/BroadcastScenario.png
[3]: ./media/notification-hubs-python-backend-how-to/SendWithOneTag.png
[4]: ./media/notification-hubs-python-backend-how-to/SendWithMultipleTags.png
[5]: ./media/notification-hubs-python-backend-how-to/TemplatedNotification.png

