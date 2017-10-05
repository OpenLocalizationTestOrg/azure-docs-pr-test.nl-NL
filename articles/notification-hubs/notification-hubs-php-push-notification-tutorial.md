---
title: Notification Hubs gebruiken met PHP
description: Informatie over het gebruik van Azure Notification Hubs vanuit een PHP-back-end.
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 0156f994-96d0-4878-b07b-49b7be4fd856
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: php
ms.devlang: php
ms.topic: article
ms.date: 06/07/2016
ms.author: yuaxu
ms.openlocfilehash: c27b6308ff528224a0398e0ff40537db05417bb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-notification-hubs-from-php"></a><span data-ttu-id="0f96c-103">Hoe Notification Hubs gebruiken vanuit PHP</span><span class="sxs-lookup"><span data-stu-id="0f96c-103">How to use Notification Hubs from PHP</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="0f96c-104">U kunt alle functies van de Notification Hubs kunt openen vanaf een PHP-Java/Ruby back-end met de Notification Hub REST-interface, zoals beschreven in de MSDN-onderwerp [Notification Hubs REST-API's](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f96c-104">You can access all Notification Hubs features from a Java/PHP/Ruby back-end using the Notification Hub REST interface as described in the MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

<span data-ttu-id="0f96c-105">In dit onderwerp laten we zien hoe:</span><span class="sxs-lookup"><span data-stu-id="0f96c-105">In this topic we show how to:</span></span>

* <span data-ttu-id="0f96c-106">Een REST-client voor Notification Hubs-functies in PHP;</span><span class="sxs-lookup"><span data-stu-id="0f96c-106">Build a REST client for Notification Hubs features in PHP;</span></span>
* <span data-ttu-id="0f96c-107">Ga als volgt de [Get gestart zelfstudie](notification-hubs-ios-apple-push-notification-apns-get-started.md) implementeren voor uw mobiele platform van de keuze van het back-end-gedeelte in PHP.</span><span class="sxs-lookup"><span data-stu-id="0f96c-107">Follow the [Get started tutorial](notification-hubs-ios-apple-push-notification-apns-get-started.md) for your mobile platform of choice, implementing the back-end portion in PHP.</span></span>

## <a name="client-interface"></a><span data-ttu-id="0f96c-108">Client-interface</span><span class="sxs-lookup"><span data-stu-id="0f96c-108">Client interface</span></span>
<span data-ttu-id="0f96c-109">De belangrijkste clientinterface kan bieden dezelfde methoden die beschikbaar zijn in de [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx), Hiermee kunt u rechtstreeks vertalen de zelfstudies en voorbeelden die momenteel beschikbaar is op deze site en die is bijgedragen door de community op het internet.</span><span class="sxs-lookup"><span data-stu-id="0f96c-109">The main client interface can provide the same methods that are available in the [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx), this will allow you to directly translate all the tutorials and samples currently available on this site, and contributed by the community on the internet.</span></span>

<span data-ttu-id="0f96c-110">U vindt de code die zijn beschikbaar in de [PHP REST wrapper voorbeeld].</span><span class="sxs-lookup"><span data-stu-id="0f96c-110">You can find all the code available in the [PHP REST wrapper sample].</span></span>

<span data-ttu-id="0f96c-111">Als u bijvoorbeeld wilt maken van een client:</span><span class="sxs-lookup"><span data-stu-id="0f96c-111">For example, to create a client:</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="0f96c-112">Een iOS systeemeigen bericht verzenden:</span><span class="sxs-lookup"><span data-stu-id="0f96c-112">To send an iOS native notification:</span></span>

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a><span data-ttu-id="0f96c-113">Implementatie</span><span class="sxs-lookup"><span data-stu-id="0f96c-113">Implementation</span></span>
<span data-ttu-id="0f96c-114">Als u nog niet hebt gedaan, volgt u onze [Get gestart zelfstudie] omhoog naar de laatste sectie waar u hebt voor het implementeren van de back-end.</span><span class="sxs-lookup"><span data-stu-id="0f96c-114">If you did not already, please follow our [Get started tutorial] up to the last section where you have to implement the back-end.</span></span>
<span data-ttu-id="0f96c-115">Ook als u wilt dat u kunt de code uit de [PHP REST wrapper voorbeeld] en rechtstreeks naar de [Voltooi de zelfstudie](#complete-tutorial) sectie.</span><span class="sxs-lookup"><span data-stu-id="0f96c-115">Also, if you want you can use the code from the [PHP REST wrapper sample] and go directly to the [Complete the tutorial](#complete-tutorial) section.</span></span>

<span data-ttu-id="0f96c-116">De details voor het implementeren van een volledige REST-wrapper vindt u op [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f96c-116">All the details to implement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="0f96c-117">In deze sectie wordt de PHP-implementatie van de belangrijkste stappen vereist voor toegang tot Notification Hubs REST-eindpunten worden beschreven:</span><span class="sxs-lookup"><span data-stu-id="0f96c-117">In this section we will describe the PHP implementation of the main steps required to access Notification Hubs REST endpoints:</span></span>

1. <span data-ttu-id="0f96c-118">De verbindingsreeks parseren</span><span class="sxs-lookup"><span data-stu-id="0f96c-118">Parse the connection string</span></span>
2. <span data-ttu-id="0f96c-119">Het verificatietoken genereren</span><span class="sxs-lookup"><span data-stu-id="0f96c-119">Generate the authorization token</span></span>
3. <span data-ttu-id="0f96c-120">De HTTP-aanroep uitvoeren</span><span class="sxs-lookup"><span data-stu-id="0f96c-120">Perform the HTTP call</span></span>

### <a name="parse-the-connection-string"></a><span data-ttu-id="0f96c-121">De verbindingsreeks parseren</span><span class="sxs-lookup"><span data-stu-id="0f96c-121">Parse the connection string</span></span>
<span data-ttu-id="0f96c-122">Dit is de hoofdklasse uitvoering van de client, waarvan constructor die kan worden geparseerd de verbindingsreeks:</span><span class="sxs-lookup"><span data-stu-id="0f96c-122">Here is the main class implementing the client, whose constructor that parses the connection string:</span></span>

    class NotificationHub {
        const API_VERSION = "?api-version=2013-10";

        private $endpoint;
        private $hubPath;
        private $sasKeyName;
        private $sasKeyValue;

        function __construct($connectionString, $hubPath) {
            $this->hubPath = $hubPath;

            $this->parseConnectionString($connectionString);
        }

        private function parseConnectionString($connectionString) {
            $parts = explode(";", $connectionString);
            if (sizeof($parts) != 3) {
                throw new Exception("Error parsing connection string: " . $connectionString);
            }

            foreach ($parts as $part) {
                if (strpos($part, "Endpoint") === 0) {
                    $this->endpoint = "https" . substr($part, 11);
                } else if (strpos($part, "SharedAccessKeyName") === 0) {
                    $this->sasKeyName = substr($part, 20);
                } else if (strpos($part, "SharedAccessKey") === 0) {
                    $this->sasKeyValue = substr($part, 16);
                }
            }
        }
    }


### <a name="create-security-token"></a><span data-ttu-id="0f96c-123">Beveiligingstoken maken</span><span class="sxs-lookup"><span data-stu-id="0f96c-123">Create security token</span></span>
<span data-ttu-id="0f96c-124">De details van het token maken voor beveiliging zijn beschikbaar [hier](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f96c-124">The details of the security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="0f96c-125">De volgende methode moet worden toegevoegd aan de **NotificationHub** klasse te maken van het token op basis van de URI van de huidige aanvraag en de referenties die zijn opgehaald uit de verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="0f96c-125">The following method has to be added to the **NotificationHub** class to create the token based on the URI of the current request and the credentials extracted from the connection string.</span></span>

    private function generateSasToken($uri) {
        $targetUri = strtolower(rawurlencode(strtolower($uri)));

        $expires = time();
        $expiresInMins = 60;
        $expires = $expires + $expiresInMins * 60;
        $toSign = $targetUri . "\n" . $expires;

        $signature = rawurlencode(base64_encode(hash_hmac('sha256', $toSign, $this->sasKeyValue, TRUE)));

        $token = "SharedAccessSignature sr=" . $targetUri . "&sig="
                    . $signature . "&se=" . $expires . "&skn=" . $this->sasKeyName;

        return $token;
    }

### <a name="send-a-notification"></a><span data-ttu-id="0f96c-126">Geen melding verzenden</span><span class="sxs-lookup"><span data-stu-id="0f96c-126">Send a notification</span></span>
<span data-ttu-id="0f96c-127">Laat het ons definiëren eerst een klasse die een melding vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="0f96c-127">First, let us define a class representing a notification.</span></span>

    class Notification {
        public $format;
        public $payload;

        # array with keynames for headers
        # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
        # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
        public $headers;

        function __construct($format, $payload) {
            if (!in_array($format, ["template", "apple", "windows", "gcm", "windowsphone"])) {
                throw new Exception('Invalid format: ' . $format);
            }

            $this->format = $format;
            $this->payload = $payload;
        }
    }

<span data-ttu-id="0f96c-128">Deze klasse is een container voor een native notification-instantie, of een set eigenschappen in geval van een melding van de sjabloon en een set headers die-indeling (systeemeigen platform of sjabloon) en platform-specifieke eigenschappen (zoals Apple verlopen eigenschap en WNS bevat headers).</span><span class="sxs-lookup"><span data-stu-id="0f96c-128">This class is a container for a native notification body, or a set of properties on case of a template notification, and a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="0f96c-129">Raadpleeg de [Notification Hubs REST-API's, documentatie](http://msdn.microsoft.com/library/dn495827.aspx) en de specifieke notification-platforms worden gebruikt voor alle beschikbare opties.</span><span class="sxs-lookup"><span data-stu-id="0f96c-129">Please refer to the [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and the specific notification platforms' formats for all the options available.</span></span>

<span data-ttu-id="0f96c-130">. Met deze klasse worden we kunnen nu schrijven de verzenden waarschuwingsmethoden binnen de **NotificationHub** klasse.</span><span class="sxs-lookup"><span data-stu-id="0f96c-130">Armed with this class, we can now write the send notification methods inside of the **NotificationHub** class.</span></span>

    public function sendNotification($notification, $tagsOrTagExpression="") {
        if (is_array($tagsOrTagExpression)) {
            $tagExpression = implode(" || ", $tagsOrTagExpression);
        } else {
            $tagExpression = $tagsOrTagExpression;
        }

        # build uri
        $uri = $this->endpoint . $this->hubPath . "/messages" . NotificationHub::API_VERSION;
        $ch = curl_init($uri);

        if (in_array($notification->format, ["template", "apple", "gcm"])) {
            $contentType = "application/json";
        } else {
            $contentType = "application/xml";
        }

        $token = $this->generateSasToken($uri);

        $headers = [
            'Authorization: '.$token,
            'Content-Type: '.$contentType,
            'ServiceBusNotification-Format: '.$notification->format
        ];

        if ("" !== $tagExpression) {
            $headers[] = 'ServiceBusNotification-Tags: '.$tagExpression;
        }

        # add headers for other platforms
        if (is_array($notification->headers)) {
            $headers = array_merge($headers, $notification->headers);
        }

        curl_setopt_array($ch, array(
            CURLOPT_POST => TRUE,
            CURLOPT_RETURNTRANSFER => TRUE,
            CURLOPT_SSL_VERIFYPEER => FALSE,
            CURLOPT_HTTPHEADER => $headers,
            CURLOPT_POSTFIELDS => $notification->payload
        ));

        // Send the request
        $response = curl_exec($ch);

        // Check for errors
        if($response === FALSE){
            throw new Exception(curl_error($ch));
        }

        $info = curl_getinfo($ch);

        if ($info['http_code'] <> 201) {
            throw new Exception('Error sending notificaiton: '. $info['http_code'] . ' msg: ' . $response);
        }
    } 

<span data-ttu-id="0f96c-131">De bovenstaande methoden verzenden een HTTP POST-aanvraag naar het eindpunt /messages van uw notification hub, met de juiste instantie en -koppen om de melding te verzenden.</span><span class="sxs-lookup"><span data-stu-id="0f96c-131">The above methods send an HTTP POST request to the /messages endpoint of your notification hub, with the correct body and headers to send the notification.</span></span>

## <span data-ttu-id="0f96c-132"><a name="complete-tutorial"></a>Voltooi de zelfstudie</span><span class="sxs-lookup"><span data-stu-id="0f96c-132"><a name="complete-tutorial"></a>Complete the tutorial</span></span>
<span data-ttu-id="0f96c-133">U kunt nu de zelfstudie aan de slag uitvoeren met de melding verzenden vanuit een PHP-back-end.</span><span class="sxs-lookup"><span data-stu-id="0f96c-133">Now you can complete the Get Started tutorial by sending the notification from a PHP back-end.</span></span>

<span data-ttu-id="0f96c-134">Uw Notification Hubs-client initialiseren (vervangen door de verbindingsreeks en hubnaam verbindingsnaam volgens de instructies in de [Get gestart zelfstudie]):</span><span class="sxs-lookup"><span data-stu-id="0f96c-134">Initialize your Notification Hubs client (substitute the connection string and hub name as instructed in the [Get started tutorial]):</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="0f96c-135">Voeg de code verzenden, afhankelijk van uw mobiele doelplatform.</span><span class="sxs-lookup"><span data-stu-id="0f96c-135">Then add the send code depending on your target mobile platform.</span></span>

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="0f96c-136">Windows Store en Windows Phone 8.1 (zonder Silverlight)</span><span class="sxs-lookup"><span data-stu-id="0f96c-136">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a><span data-ttu-id="0f96c-137">iOS</span><span class="sxs-lookup"><span data-stu-id="0f96c-137">iOS</span></span>
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a><span data-ttu-id="0f96c-138">Android</span><span class="sxs-lookup"><span data-stu-id="0f96c-138">Android</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="0f96c-139">Windows Phone 8.0 en 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="0f96c-139">Windows Phone 8.0 and 8.1 Silverlight</span></span>
    $toast = '<?xml version="1.0" encoding="utf-8"?>' .
                '<wp:Notification xmlns:wp="WPNotification">' .
                   '<wp:Toast>' .
                        '<wp:Text1>Hello from PHP!</wp:Text1>' .
                   '</wp:Toast> ' .
                '</wp:Notification>';
    $notification = new Notification("windowsphone", $toast);
    $notification->headers[] = 'X-WindowsPhone-Target : toast';
    $notification->headers[] = 'X-NotificationClass : 2';
    $hub->sendNotification($notification, null);


### <a name="kindle-fire"></a><span data-ttu-id="0f96c-140">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="0f96c-140">Kindle Fire</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

<span data-ttu-id="0f96c-141">Uitvoeren van uw PHP-code moet produceren nu een melding weergegeven op het doelapparaat.</span><span class="sxs-lookup"><span data-stu-id="0f96c-141">Running your PHP code should produce now a notification appearing on your target device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f96c-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0f96c-142">Next Steps</span></span>
<span data-ttu-id="0f96c-143">In dit onderwerp we hebt u geleerd hoe u een eenvoudige Java REST-client voor Notification Hubs maakt.</span><span class="sxs-lookup"><span data-stu-id="0f96c-143">In this topic we showed how to create a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="0f96c-144">Hier kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="0f96c-144">From here you can:</span></span>

* <span data-ttu-id="0f96c-145">Downloaden van de volledige [PHP REST wrapper voorbeeld], die de bovenstaande code bevat.</span><span class="sxs-lookup"><span data-stu-id="0f96c-145">Download the full [PHP REST wrapper sample], which contains all the code above.</span></span>
* <span data-ttu-id="0f96c-146">Meer informatie over Notification Hubs functie labels in de [nieuws op te splitsen zelfstudie] gaan</span><span class="sxs-lookup"><span data-stu-id="0f96c-146">Continue learning about Notification Hubs tagging feature in the [Breaking News tutorial]</span></span>
* <span data-ttu-id="0f96c-147">Meer informatie over pushmeldingen naar afzonderlijke gebruikers in [gebruikers waarschuwen zelfstudie]</span><span class="sxs-lookup"><span data-stu-id="0f96c-147">Learn about pushing notifications to individual users in [Notify Users tutorial]</span></span>

<span data-ttu-id="0f96c-148">Zie voor meer informatie, ook de [PHP-ontwikkelaarscentrum](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="0f96c-148">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

<span data-ttu-id="0f96c-149">[PHP REST wrapper voorbeeld]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php</span><span class="sxs-lookup"><span data-stu-id="0f96c-149">[PHP REST wrapper sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php</span></span>
<span data-ttu-id="0f96c-150">[Get gestart zelfstudie]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/</span><span class="sxs-lookup"><span data-stu-id="0f96c-150">[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/</span></span>

