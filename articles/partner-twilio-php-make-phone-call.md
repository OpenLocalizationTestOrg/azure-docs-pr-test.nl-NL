---
title: aaaHow toomake een telefonische oproep van Twilio (PHP) | Microsoft Docs
description: Meer informatie over hoe toomake een telefonische oproep en verzend een SMS-met Hallo Twilio-API-service op Azure bericht. Voorbeelden zijn bedoeld voor PHP-toepassing.
documentationcenter: php
services: 
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 44e35adc-be06-4700-beee-8c9e2c20c540
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: e6fecc345bf9ae787d14d533bd8d96b175c2453b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-php-application-on-azure"></a>Hoe tooMake een telefonische oproep met behulp van Twilio in een PHP-toepassing in Azure
Hallo volgende voorbeeld ziet u hoe u kunt Twilio toomake een aanroep van een PHP-webpagina gehost in Azure. de resulterende toepassing Hello wordt Hallo gebruiker gevraagd om telefoongesprek waarden, zoals wordt weergegeven in de volgende schermopname Hallo.

![De aanroep van de Azure-formulier met Twilio en PHP][twilio_php]

U moet toodo Hallo volgende toouse Hallo code in dit onderwerp:

1. Verkrijgen van een Twilio-account en verificatie-token van uw [Twilio Console][twilio_console]. tooget gestart met Twilio, evalueren prijzen op [http://www.twilio.com/pricing][twilio_pricing]. U kunt zich aanmelden voor een evaluatieaccount op [https://www.twilio.com/try-twilio][try_twilio].
2. Hallo verkrijgen [Twilio-bibliotheek voor PHP](https://github.com/twilio/twilio-php) of u deze installeert als een PEER-pakket. Zie voor meer informatie, Hallo [Leesmij-bestand](https://github.com/twilio/twilio-php/blob/master/README.md).
3. Hello Azure SDK voor PHP installeren. Zie voor een overzicht van Hallo SDK en instructies over het installeren van deze [hello Azure SDK voor PHP instellen](app-service-web/web-sites-php-mysql-deploy-use-git.md)

## <a name="create-a-web-form-for-making-a-call"></a>Maken van een webformulier voor het maken van een aanroep
Hallo HTML volgende code toont hoe toobuild een webpagina (**callform.html**) die gebruikersgegevens voor het maken van een aanroep van ophaalt:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Automated call form</title>
</head>
<body>
  <h1>Automated Call Form</h1>
  <p>Fill in all fields and click <b>Make this call</b>.</p>
  <form action="makecall.php" method="post">
    <table>
      <tr>
        <td>To:</td>
        <td><input name="callTo" size="50" type="text" value=""></td>
      </tr>
      <tr>
        <td>From:</td>
        <td><input name="callFrom" size="50" type="text" value=""></td>
      </tr>
      <tr>
        <td>Call message:</td>
        <td><input name="callText" size="100" type="text" value="Hello. This is hello call text. Good bye."></td>
      </tr>
      <tr>
        <td colspan="2"><input type="submit" value="Make this call"></td>
      </tr>
    </table>
  </form><br>
</body>
</html>
```

## <a name="create-hello-code-toomake-hello-call"></a>Hallo code toomake Hallo aanroep maken
Hallo van de volgende code wordt getoond hoe toobuild **makecall.php**, die wordt aangeroepen wanneer de Hallo gebruiker verzendt Hallo formulier weergegeven door **callform.html**. Hallo-code hieronder aanroep het Hallo-bericht maakt en genereert Hallo-aanroep. Bovendien worden ervoor toouse uw Twilio-account en de verificatie-van Hallo token [Twilio Console] [ twilio_console] in plaats van de waarden van de tijdelijke aanduiding hello te toegewezen**$sid** en **$token** in onderstaande Hallo-code.

```html
<html>
<head><title>Making call...</title></head>
<body>
<p>Your call is being made.</p>

<?php
require_once 'path/to/vendor/autoload.php';

$sid   = "your_account_sid";
$token = "your_authentication_token";

$from_number = $_POST['callFrom']; // Calls must be made from a registered Twilio number.
$to_number   = $_POST['callTo'];
$message     = $_POST['callText'];

$client = new Twilio\Rest\Client($sid, $token);

$call = $client->calls->create(
            $to_number,
            $from_number,
            array('url' => http://twimlets.com/message?Message=' . urlencode($message))
        );

echo "Call status: " . $call->status . "<br />";
echo "URI resource: " . $call->uri . "<br />";
?>
</body>
</html>
```

Bovendien toomaking Hallo-aanroep **makecall.php** bepaalde metagegevens aanroep wordt weergegeven zoals in Hallo in onderstaande afbeelding wordt weergegeven. Zie voor meer informatie over de metagegevens van de aanroep [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].

![De aanroep van de Azure-antwoord met Twilio en PHP][twilio_php_response]

## <a name="run-hello-application"></a>Hallo-toepassing uitvoeren
de volgende stap Hallo toodeploy is uw toepassing tooAzure Websites. Hallo bevatten volgende artikelen Hallo-informatie voor een website maken en implementeren van uw code met Git, FTP of WebMatrix (hoewel niet alle gegevens in elk artikel is van toepassing):

* [Een PHP-MySQL Azure-website maken en implementeren met Git](app-service-web/web-sites-php-mysql-deploy-use-git.md)
* [Een Azure-website van PHP MySQL maken en implementeren met FTP](app-service-web/web-sites-php-mysql-deploy-use-ftp.md)

## <a name="next-steps"></a>Volgende stappen
Deze code is opgegeven tooshow u basisfunctionaliteit met Twilio in PHP in Azure. Voordat u tooAzure in productie implementeert, kunt u tooadd meer foutafhandeling of andere onderdelen. Bijvoorbeeld:

* In plaats van een webformulier, Azure storage-blobs of SQL-Database toostore telefoonnummers te gebruiken en aanroepen van tekst. Zie voor meer informatie over het gebruik van Azure storage-blobs in PHP [Azure Storage gebruiken met PHP-toepassingen][howto_blob_storage_php]. Zie voor meer informatie over het gebruik van SQL-Database in PHP [met behulp van SQL Database met PHP-toepassingen][howto_sql_azure_php].
* Hallo **makecall.php** code gebruikt Twilio-geleverde URL ([http://twimlets.com/message][twimlet_message_url]) tooprovide een Twilio Markup Language (TwiML) antwoord dat Twilio hoe informeert tooproceed met Hallo-aanroep. Bijvoorbeeld, Hallo TwiML die wordt geretourneerd kunt bevatten een `<Say>` term die resulteert in de tekst wordt gesproken toohello aanroep ontvanger. In plaats van Hallo geleverde Twilio-URL, kan u uw eigen service toorespond tooTwilio aanvraag; samenstellen Zie voor meer informatie [hoe tooUse Twilio voor spraak- en SMS-mogelijkheden van PHP][howto_twilio_voice_sms_php]. Meer informatie over TwiML kan worden gevonden op [http://www.twilio.com/docs/api/twiml][twiml], en meer informatie over `<Say>` en andere Twilio-termen kunnen worden gevonden op [http:// www.twilio.com/Docs/API/twiml/say][twilio_say].
* Hallo Twilio-richtlijnen voor beveiliging op lezen [https://www.twilio.com/docs/security][twilio_docs_security].

Zie voor meer informatie over Twilio [https://www.twilio.com/docs][twilio_docs].

## <a name="see-also"></a>Zie ook
* [Hoe tooUse Twilio voor spraak- en SMS-mogelijkheden van PHP](partner-twilio-php-how-to-use-voice-sms.md)

[twilio_console]: https://www.twilio.com/console
[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/docs/api
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified
[twimlet_message_url]: http://twimlets.com/message
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api_service]: http://api.twilio.com
[build_php_azure_app]: http://azurephp.interoperabilitybridges.com/articles/build-and-deploy-a-windows-azure-php-application
[howto_twilio_voice_sms_php]: partner-twilio-php-how-to-use-voice-sms.md
[howto_blob_storage_php]: http://azure.microsoft.com/documentation/articles/storage-php-how-to-use-blobs/
[howto_sql_azure_php]: http://azure.microsoft.com/documentation/articles/sql-database-php-how-to-use/
[twilio_call_properties]: https://www.twilio.com/docs/api/rest/call#instance-properties
[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say
[ssl_validation]: http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html
[twilio_php]: ./media/partner-twilio-php-make-phone-call/WA_TwilioPHPCallForm.jpg
[twilio_php_response]: ./media/partner-twilio-php-make-phone-call/WA_TwilioPHPMakeCall.jpg
[website-git]: ./web-sites/web-sites-php-mysql-deploy-use-git.md
[website-ftp]: ./web-sites/web-sites-php-mysql-deploy-use-ftp.md
[twilio_php_github]: https://github.com/twilio/twilio-php
