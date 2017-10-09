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
# <a name="how-toouse-notification-hubs-from-php"></a>Hoe toouse Notification Hubs met PHP
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

U kunt alle functies van de Notification Hubs kunt openen vanaf een PHP-Java/Ruby back-end Hallo Notification Hub REST-interface gebruiken, zoals beschreven in de MSDN-onderwerp Hallo [Notification Hubs REST-API's](http://msdn.microsoft.com/library/dn223264.aspx).

In dit onderwerp laten we zien hoe:

* Een REST-client voor Notification Hubs-functies in PHP;
* Ga als volgt Hallo [Get gestart zelfstudie](notification-hubs-ios-apple-push-notification-apns-get-started.md) voor uw mobiele platform keuze, het implementeren van Hallo back-end gedeelte in PHP.

## <a name="client-interface"></a>Client-interface
de belangrijkste clientinterface Hallo Hallo kan bieden dezelfde methoden die beschikbaar in Hallo zijn [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx), Hierdoor kunt u toodirectly vertalen alle Hallo zelfstudies en voorbeelden die momenteel beschikbaar is op deze site, en die is bijgedragen door Hallo-community op Hallo internet.

U vindt alle Hallo-code die beschikbaar zijn in Hallo [PHP REST wrapper voorbeeld].

Bijvoorbeeld, toocreate een client:

    $hub = new NotificationHub("connection string", "hubname");    

toosend een systeemeigen iOS-meldingen:

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a>Implementatie
Als u nog niet hebt gedaan, volgt u onze [Get gestart zelfstudie] -up maken van de laatste sectie toohello waar u tooimplement Hallo back-end hebt.
Als u wilt dat kunt u ook Hallo code uit Hallo gebruiken [PHP REST wrapper voorbeeld] en gaat u rechtstreeks toohello [voltooid Hallo zelfstudie](#complete-tutorial) sectie.

Alle details tooimplement een volledige REST-wrapper vindt u op Hallo [MSDN](http://msdn.microsoft.com/library/dn530746.aspx). In deze sectie wordt beschreven Hallo PHP uitvoering van Hallo belangrijke stappen vereist tooaccess Notification Hubs REST-eindpunten:

1. Hallo-verbindingsreeks parseren
2. Hallo-Autorisatietoken te genereren
3. Hallo HTTP-aanroep uitvoeren

### <a name="parse-hello-connection-string"></a>Hallo-verbindingsreeks parseren
Hier volgt Hallo hoofdklasse geïmplementeerd Hallo client, waarvan constructor die kan worden geparseerd Hallo-verbindingsreeks:

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


### <a name="create-security-token"></a>Beveiligingstoken maken
Hallo-details van hello security token maken zijn beschikbaar [hier](http://msdn.microsoft.com/library/dn495627.aspx).
Hallo volgende methode heeft toegevoegd toobe toohello **NotificationHub** klassentoken toocreate Hallo op basis van Hallo-URI van de huidige aanvraag Hallo en opgehaald uit de verbindingsreeks Hallo Hallo-referenties.

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

### <a name="send-a-notification"></a>Geen melding verzenden
Laat het ons definiëren eerst een klasse die een melding vertegenwoordigt.

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

Deze klasse is een container voor een native notification-instantie, of een set eigenschappen in geval van een melding van de sjabloon en een set headers die-indeling (systeemeigen platform of sjabloon) en platform-specifieke eigenschappen (zoals Apple verlopen eigenschap en WNS bevat headers).

Raadpleeg toohello [Notification Hubs REST-API's, documentatie](http://msdn.microsoft.com/library/dn495827.aspx) en specifieke notification-platforms indelingen Hallo voor alle beschikbare opties Hallo.

. Met deze klasse worden we kunnen nu schrijven Hallo verzenden waarschuwingsmethoden binnen Hallo **NotificationHub** klasse.

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

Hallo hierboven methoden een HTTP POST-aanvraag toohello /messages eindpunt van uw notification hub, met de juiste hoofdtekst Hallo en headers toosend Hallo melding verzenden.

## <a name="complete-tutorial"></a>Volledige Hallo-zelfstudie
U kunt nu Hallo-zelfstudie aan de slag uitvoeren met het Hallo-bericht verzenden vanuit een PHP-back-end.

Uw Notification Hubs-client initialiseren (vervangen door Hallo verbindingsreeks en hubnaam verbindingsnaam volgens de instructies in Hallo [Get gestart zelfstudie]):

    $hub = new NotificationHub("connection string", "hubname");    

Voeg Hallo verzenden code, afhankelijk van uw mobiele doelplatform toe.

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a>Windows Store en Windows Phone 8.1 (zonder Silverlight)
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a>iOS
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a>Android
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a>Windows Phone 8.0 en 8.1 Silverlight
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


### <a name="kindle-fire"></a>Kindle Fire
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

Uitvoeren van uw PHP-code moet produceren nu een melding weergegeven op het doelapparaat.

## <a name="next-steps"></a>Volgende stappen
In dit onderwerp we hebt u geleerd hoe toocreate een eenvoudige Java REST-client voor Notification Hubs. Hier kunt u het volgende doen:

* Hallo volledige downloaden [PHP REST wrapper voorbeeld], die alle Hallo code bovenstaande bevat.
* Meer informatie over Notification Hubs functie tags in Hallo [nieuws op te splitsen zelfstudie] gaan
* Meer informatie over het pushen van meldingen tooindividual gebruikers in [gebruikers waarschuwen zelfstudie]

Zie voor meer informatie, ook Hallo [PHP-ontwikkelaarscentrum](/develop/php/).

[PHP REST wrapper voorbeeld]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php
[Get gestart zelfstudie]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/

