---
title: aaaHow toouse Notification Hubs met PHP
description: Meer informatie over hoe toouse Azure Notification Hubs vanuit een PHP-back-end.
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
ms.openlocfilehash: 6cd426286a684006a07867fcf44a8ff71be7efa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-php"></a><span data-ttu-id="dfc8e-103">Hoe toouse Notification Hubs met PHP</span><span class="sxs-lookup"><span data-stu-id="dfc8e-103">How toouse Notification Hubs from PHP</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="dfc8e-104">U kunt alle functies van de Notification Hubs kunt openen vanaf een PHP-Java/Ruby back-end Hallo Notification Hub REST-interface gebruiken, zoals beschreven in de MSDN-onderwerp Hallo [Notification Hubs REST-API's](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="dfc8e-104">You can access all Notification Hubs features from a Java/PHP/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

<span data-ttu-id="dfc8e-105">In dit onderwerp laten we zien hoe:</span><span class="sxs-lookup"><span data-stu-id="dfc8e-105">In this topic we show how to:</span></span>

* <span data-ttu-id="dfc8e-106">Een REST-client voor Notification Hubs-functies in PHP;</span><span class="sxs-lookup"><span data-stu-id="dfc8e-106">Build a REST client for Notification Hubs features in PHP;</span></span>
* <span data-ttu-id="dfc8e-107">Ga als volgt Hallo [Get gestart zelfstudie](notification-hubs-ios-apple-push-notification-apns-get-started.md) voor uw mobiele platform keuze, het implementeren van Hallo back-end gedeelte in PHP.</span><span class="sxs-lookup"><span data-stu-id="dfc8e-107">Follow hello [Get started tutorial](notification-hubs-ios-apple-push-notification-apns-get-started.md) for your mobile platform of choice, implementing hello back-end portion in PHP.</span></span>

## <a name="client-interface"></a><span data-ttu-id="dfc8e-108">Client-interface</span><span class="sxs-lookup"><span data-stu-id="dfc8e-108">Client interface</span></span>
<span data-ttu-id="dfc8e-109">de belangrijkste clientinterface Hallo Hallo kan bieden dezelfde methoden die beschikbaar in Hallo zijn [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx), Hierdoor kunt u toodirectly vertalen alle Hallo zelfstudies en voorbeelden die momenteel beschikbaar is op deze site, en die is bijgedragen door Hallo-community op Hallo internet.</span><span class="sxs-lookup"><span data-stu-id="dfc8e-109">hello main client interface can provide hello same methods that are available in hello [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx), this will allow you toodirectly translate all hello tutorials and samples currently available on this site, and contributed by hello community on hello internet.</span></span>

<span data-ttu-id="dfc8e-110">U vindt alle Hallo-code die beschikbaar zijn in Hallo [PHP REST wrapper voorbeeld].</span><span class="sxs-lookup"><span data-stu-id="dfc8e-110">You can find all hello code available in hello [PHP REST wrapper sample].</span></span>

<span data-ttu-id="dfc8e-111">Bijvoorbeeld, toocreate een client:</span><span class="sxs-lookup"><span data-stu-id="dfc8e-111">For example, toocreate a client:</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="dfc8e-112">toosend een systeemeigen iOS-meldingen:</span><span class="sxs-lookup"><span data-stu-id="dfc8e-112">toosend an iOS native notification:</span></span>

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a><span data-ttu-id="dfc8e-113">Implementatie</span><span class="sxs-lookup"><span data-stu-id="dfc8e-113">Implementation</span></span>
<span data-ttu-id="dfc8e-114">Als u nog niet hebt gedaan, volgt u onze [Get gestart zelfstudie] -up maken van de laatste sectie toohello waar u tooimplement Hallo back-end hebt.</span><span class="sxs-lookup"><span data-stu-id="dfc8e-114">If you did not already, please follow our [Get started tutorial] up toohello last section where you have tooimplement hello back-end.</span></span>
<span data-ttu-id="dfc8e-115">Als u wilt dat kunt u ook Hallo code uit Hallo gebruiken [PHP REST wrapper voorbeeld] en gaat u rechtstreeks toohello [voltooid Hallo zelfstudie](#complete-tutorial) sectie.</span><span class="sxs-lookup"><span data-stu-id="dfc8e-115">Also, if you want you can use hello code from hello [PHP REST wrapper sample] and go directly toohello [Complete hello tutorial](#complete-tutorial) section.</span></span>

<span data-ttu-id="dfc8e-116">Alle details tooimplement een volledige REST-wrapper vindt u op Hallo [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="dfc8e-116">All hello details tooimplement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="dfc8e-117">In deze sectie wordt beschreven Hallo PHP uitvoering van Hallo belangrijke stappen vereist tooaccess Notification Hubs REST-eindpunten:</span><span class="sxs-lookup"><span data-stu-id="dfc8e-117">In this section we will describe hello PHP implementation of hello main steps required tooaccess Notification Hubs REST endpoints:</span></span>

1. <span data-ttu-id="dfc8e-118">Hallo-verbindingsreeks parseren</span><span class="sxs-lookup"><span data-stu-id="dfc8e-118">Parse hello connection string</span></span>
2. <span data-ttu-id="dfc8e-119">Hallo-Autorisatietoken te genereren</span><span class="sxs-lookup"><span data-stu-id="dfc8e-119">Generate hello authorization token</span></span>
3. <span data-ttu-id="dfc8e-120">Hallo HTTP-aanroep uitvoeren</span><span class="sxs-lookup"><span data-stu-id="dfc8e-120">Perform hello HTTP call</span></span>

### <a name="parse-hello-connection-string"></a><span data-ttu-id="dfc8e-121">Hallo-verbindingsreeks parseren</span><span class="sxs-lookup"><span data-stu-id="dfc8e-121">Parse hello connection string</span></span>
<span data-ttu-id="dfc8e-122">Hier volgt Hallo hoofdklasse geïmplementeerd Hallo client, waarvan constructor die kan worden geparseerd Hallo-verbindingsreeks:</span><span class="sxs-lookup"><span data-stu-id="dfc8e-122">Here is hello main class implementing hello client, whose constructor that parses hello connection string:</span></span>

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


### <a name="create-security-token"></a><span data-ttu-id="dfc8e-123">Beveiligingstoken maken</span><span class="sxs-lookup"><span data-stu-id="dfc8e-123">Create security token</span></span>
<span data-ttu-id="dfc8e-124">Hallo-details van hello security token maken zijn beschikbaar [hier](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="dfc8e-124">hello details of hello security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="dfc8e-125">Hallo volgende methode heeft toegevoegd toobe toohello **NotificationHub** klassentoken toocreate Hallo op basis van Hallo-URI van de huidige aanvraag Hallo en opgehaald uit de verbindingsreeks Hallo Hallo-referenties.</span><span class="sxs-lookup"><span data-stu-id="dfc8e-125">hello following method has toobe added toohello **NotificationHub** class toocreate hello token based on hello URI of hello current request and hello credentials extracted from hello connection string.</span></span>

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

### <a name="send-a-notification"></a><span data-ttu-id="dfc8e-126">Geen melding verzenden</span><span class="sxs-lookup"><span data-stu-id="dfc8e-126">Send a notification</span></span>
<span data-ttu-id="dfc8e-127">Laat het ons definiëren eerst een klasse die een melding vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="dfc8e-127">First, let us define a class representing a notification.</span></span>

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

<span data-ttu-id="dfc8e-128">Deze klasse is een container voor een native notification-instantie, of een set eigenschappen in geval van een melding van de sjabloon en een set headers die-indeling (systeemeigen platform of sjabloon) en platform-specifieke eigenschappen (zoals Apple verlopen eigenschap en WNS bevat headers).</span><span class="sxs-lookup"><span data-stu-id="dfc8e-128">This class is a container for a native notification body, or a set of properties on case of a template notification, and a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="dfc8e-129">Raadpleeg toohello [Notification Hubs REST-API's, documentatie](http://msdn.microsoft.com/library/dn495827.aspx) en specifieke notification-platforms indelingen Hallo voor alle beschikbare opties Hallo.</span><span class="sxs-lookup"><span data-stu-id="dfc8e-129">Please refer toohello [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and hello specific notification platforms' formats for all hello options available.</span></span>

<span data-ttu-id="dfc8e-130">. Met deze klasse worden we kunnen nu schrijven Hallo verzenden waarschuwingsmethoden binnen Hallo **NotificationHub** klasse.</span><span class="sxs-lookup"><span data-stu-id="dfc8e-130">Armed with this class, we can now write hello send notification methods inside of hello **NotificationHub** class.</span></span>

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

        // Send hello request
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

<span data-ttu-id="dfc8e-131">Hallo hierboven methoden een HTTP POST-aanvraag toohello /messages eindpunt van uw notification hub, met de juiste hoofdtekst Hallo en headers toosend Hallo melding verzenden.</span><span class="sxs-lookup"><span data-stu-id="dfc8e-131">hello above methods send an HTTP POST request toohello /messages endpoint of your notification hub, with hello correct body and headers toosend hello notification.</span></span>

## <span data-ttu-id="dfc8e-132"><a name="complete-tutorial"></a>Volledige Hallo-zelfstudie</span><span class="sxs-lookup"><span data-stu-id="dfc8e-132"><a name="complete-tutorial"></a>Complete hello tutorial</span></span>
<span data-ttu-id="dfc8e-133">U kunt nu Hallo-zelfstudie aan de slag uitvoeren met het Hallo-bericht verzenden vanuit een PHP-back-end.</span><span class="sxs-lookup"><span data-stu-id="dfc8e-133">Now you can complete hello Get Started tutorial by sending hello notification from a PHP back-end.</span></span>

<span data-ttu-id="dfc8e-134">Uw Notification Hubs-client initialiseren (vervangen door Hallo verbindingsreeks en hubnaam verbindingsnaam volgens de instructies in Hallo [Get gestart zelfstudie]):</span><span class="sxs-lookup"><span data-stu-id="dfc8e-134">Initialize your Notification Hubs client (substitute hello connection string and hub name as instructed in hello [Get started tutorial]):</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="dfc8e-135">Voeg Hallo verzenden code, afhankelijk van uw mobiele doelplatform toe.</span><span class="sxs-lookup"><span data-stu-id="dfc8e-135">Then add hello send code depending on your target mobile platform.</span></span>

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="dfc8e-136">Windows Store en Windows Phone 8.1 (zonder Silverlight)</span><span class="sxs-lookup"><span data-stu-id="dfc8e-136">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a><span data-ttu-id="dfc8e-137">iOS</span><span class="sxs-lookup"><span data-stu-id="dfc8e-137">iOS</span></span>
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a><span data-ttu-id="dfc8e-138">Android</span><span class="sxs-lookup"><span data-stu-id="dfc8e-138">Android</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="dfc8e-139">Windows Phone 8.0 en 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="dfc8e-139">Windows Phone 8.0 and 8.1 Silverlight</span></span>
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


### <a name="kindle-fire"></a><span data-ttu-id="dfc8e-140">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="dfc8e-140">Kindle Fire</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

<span data-ttu-id="dfc8e-141">Uitvoeren van uw PHP-code moet produceren nu een melding weergegeven op het doelapparaat.</span><span class="sxs-lookup"><span data-stu-id="dfc8e-141">Running your PHP code should produce now a notification appearing on your target device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfc8e-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dfc8e-142">Next Steps</span></span>
<span data-ttu-id="dfc8e-143">In dit onderwerp we hebt u geleerd hoe toocreate een eenvoudige Java REST-client voor Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="dfc8e-143">In this topic we showed how toocreate a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="dfc8e-144">Hier kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="dfc8e-144">From here you can:</span></span>

* <span data-ttu-id="dfc8e-145">Hallo volledige downloaden [PHP REST wrapper voorbeeld], die alle Hallo code bovenstaande bevat.</span><span class="sxs-lookup"><span data-stu-id="dfc8e-145">Download hello full [PHP REST wrapper sample], which contains all hello code above.</span></span>
* <span data-ttu-id="dfc8e-146">Meer informatie over Notification Hubs functie tags in Hallo [nieuws op te splitsen zelfstudie] gaan</span><span class="sxs-lookup"><span data-stu-id="dfc8e-146">Continue learning about Notification Hubs tagging feature in hello [Breaking News tutorial]</span></span>
* <span data-ttu-id="dfc8e-147">Meer informatie over het pushen van meldingen tooindividual gebruikers in [gebruikers waarschuwen zelfstudie]</span><span class="sxs-lookup"><span data-stu-id="dfc8e-147">Learn about pushing notifications tooindividual users in [Notify Users tutorial]</span></span>

<span data-ttu-id="dfc8e-148">Zie voor meer informatie, ook Hallo [PHP-ontwikkelaarscentrum](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="dfc8e-148">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[PHP REST wrapper voorbeeld]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php
[Get gestart zelfstudie]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/

