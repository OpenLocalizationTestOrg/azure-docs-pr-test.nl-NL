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
# <a name="how-toomake-a-phone-call-using-twilio-in-a-php-application-on-azure"></a><span data-ttu-id="3c5f3-104">Hoe tooMake een telefonische oproep met behulp van Twilio in een PHP-toepassing in Azure</span><span class="sxs-lookup"><span data-stu-id="3c5f3-104">How tooMake a Phone Call Using Twilio in a PHP Application on Azure</span></span>
<span data-ttu-id="3c5f3-105">Hallo volgende voorbeeld ziet u hoe u kunt Twilio toomake een aanroep van een PHP-webpagina gehost in Azure.</span><span class="sxs-lookup"><span data-stu-id="3c5f3-105">hello following example shows you how you can use Twilio toomake a call from a PHP web page hosted in Azure.</span></span> <span data-ttu-id="3c5f3-106">de resulterende toepassing Hello wordt Hallo gebruiker gevraagd om telefoongesprek waarden, zoals wordt weergegeven in de volgende schermopname Hallo.</span><span class="sxs-lookup"><span data-stu-id="3c5f3-106">hello resulting application will prompt hello user for phone call values, as shown in hello following screen shot.</span></span>

![De aanroep van de Azure-formulier met Twilio en PHP][twilio_php]

<span data-ttu-id="3c5f3-108">U moet toodo Hallo volgende toouse Hallo code in dit onderwerp:</span><span class="sxs-lookup"><span data-stu-id="3c5f3-108">You'll need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="3c5f3-109">Verkrijgen van een Twilio-account en verificatie-token van uw [Twilio Console][twilio_console].</span><span class="sxs-lookup"><span data-stu-id="3c5f3-109">Acquire a Twilio account and authentication token from your [Twilio Console][twilio_console].</span></span> <span data-ttu-id="3c5f3-110">tooget gestart met Twilio, evalueren prijzen op [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="3c5f3-110">tooget started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="3c5f3-111">U kunt zich aanmelden voor een evaluatieaccount op [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="3c5f3-111">You can sign up for a trial account at [https://www.twilio.com/try-twilio][try_twilio].</span></span>
2. <span data-ttu-id="3c5f3-112">Hallo verkrijgen [Twilio-bibliotheek voor PHP](https://github.com/twilio/twilio-php) of u deze installeert als een PEER-pakket.</span><span class="sxs-lookup"><span data-stu-id="3c5f3-112">Obtain hello [Twilio library for PHP](https://github.com/twilio/twilio-php) or install it as a PEAR package.</span></span> <span data-ttu-id="3c5f3-113">Zie voor meer informatie, Hallo [Leesmij-bestand](https://github.com/twilio/twilio-php/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="3c5f3-113">For more information, see hello [readme file](https://github.com/twilio/twilio-php/blob/master/README.md).</span></span>
3. <span data-ttu-id="3c5f3-114">Hello Azure SDK voor PHP installeren.</span><span class="sxs-lookup"><span data-stu-id="3c5f3-114">Install hello Azure SDK for PHP.</span></span> <span data-ttu-id="3c5f3-115">Zie voor een overzicht van Hallo SDK en instructies over het installeren van deze [hello Azure SDK voor PHP instellen](app-service-web/web-sites-php-mysql-deploy-use-git.md)</span><span class="sxs-lookup"><span data-stu-id="3c5f3-115">For an overview of hello SDK and instructions on installing it, see [Set up hello Azure SDK for PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="3c5f3-116">Maken van een webformulier voor het maken van een aanroep</span><span class="sxs-lookup"><span data-stu-id="3c5f3-116">Create a web form for making a call</span></span>
<span data-ttu-id="3c5f3-117">Hallo HTML volgende code toont hoe toobuild een webpagina (**callform.html**) die gebruikersgegevens voor het maken van een aanroep van ophaalt:</span><span class="sxs-lookup"><span data-stu-id="3c5f3-117">hello following HTML code shows how toobuild a web page (**callform.html**) that retrieves user data for making a call:</span></span>

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

## <a name="create-hello-code-toomake-hello-call"></a><span data-ttu-id="3c5f3-118">Hallo code toomake Hallo aanroep maken</span><span class="sxs-lookup"><span data-stu-id="3c5f3-118">Create hello code toomake hello call</span></span>
<span data-ttu-id="3c5f3-119">Hallo van de volgende code wordt getoond hoe toobuild **makecall.php**, die wordt aangeroepen wanneer de Hallo gebruiker verzendt Hallo formulier weergegeven door **callform.html**.</span><span class="sxs-lookup"><span data-stu-id="3c5f3-119">hello following code shows how toobuild **makecall.php**, which is called when hello user submits hello form displayed by **callform.html**.</span></span> <span data-ttu-id="3c5f3-120">Hallo-code hieronder aanroep het Hallo-bericht maakt en genereert Hallo-aanroep.</span><span class="sxs-lookup"><span data-stu-id="3c5f3-120">hello code shown below creates hello call message and generates hello call.</span></span> <span data-ttu-id="3c5f3-121">Bovendien worden ervoor toouse uw Twilio-account en de verificatie-van Hallo token [Twilio Console] [ twilio_console] in plaats van de waarden van de tijdelijke aanduiding hello te toegewezen**$sid** en **$token** in onderstaande Hallo-code.</span><span class="sxs-lookup"><span data-stu-id="3c5f3-121">Also, be sure toouse your Twilio account and authentication token from hello [Twilio Console][twilio_console] instead of hello placeholder values assigned too**$sid** and **$token** in hello code below.</span></span>

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

<span data-ttu-id="3c5f3-122">Bovendien toomaking Hallo-aanroep **makecall.php** bepaalde metagegevens aanroep wordt weergegeven zoals in Hallo in onderstaande afbeelding wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3c5f3-122">In addition toomaking hello call, **makecall.php** displays some call metadata, as is shown in hello image below.</span></span> <span data-ttu-id="3c5f3-123">Zie voor meer informatie over de metagegevens van de aanroep [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].</span><span class="sxs-lookup"><span data-stu-id="3c5f3-123">For more information about call metadata, see [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].</span></span>

![De aanroep van de Azure-antwoord met Twilio en PHP][twilio_php_response]

## <a name="run-hello-application"></a><span data-ttu-id="3c5f3-125">Hallo-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="3c5f3-125">Run hello application</span></span>
<span data-ttu-id="3c5f3-126">de volgende stap Hallo toodeploy is uw toepassing tooAzure Websites.</span><span class="sxs-lookup"><span data-stu-id="3c5f3-126">hello next step is toodeploy your application tooAzure Websites.</span></span> <span data-ttu-id="3c5f3-127">Hallo bevatten volgende artikelen Hallo-informatie voor een website maken en implementeren van uw code met Git, FTP of WebMatrix (hoewel niet alle gegevens in elk artikel is van toepassing):</span><span class="sxs-lookup"><span data-stu-id="3c5f3-127">hello following articles contain hello information for creating a website and deploying your code with Git, FTP, or WebMatrix (though not all information in each article is relevant):</span></span>

* [<span data-ttu-id="3c5f3-128">Een PHP-MySQL Azure-website maken en implementeren met Git</span><span class="sxs-lookup"><span data-stu-id="3c5f3-128">Create a PHP-MySQL Azure Web Site and deploy using Git</span></span>](app-service-web/web-sites-php-mysql-deploy-use-git.md)
* [<span data-ttu-id="3c5f3-129">Een Azure-website van PHP MySQL maken en implementeren met FTP</span><span class="sxs-lookup"><span data-stu-id="3c5f3-129">Create a PHP-MySQL Azure Web Site and Deploy Using FTP</span></span>](app-service-web/web-sites-php-mysql-deploy-use-ftp.md)

## <a name="next-steps"></a><span data-ttu-id="3c5f3-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3c5f3-130">Next steps</span></span>
<span data-ttu-id="3c5f3-131">Deze code is opgegeven tooshow u basisfunctionaliteit met Twilio in PHP in Azure.</span><span class="sxs-lookup"><span data-stu-id="3c5f3-131">This code was provided tooshow you basic functionality using Twilio in PHP on Azure.</span></span> <span data-ttu-id="3c5f3-132">Voordat u tooAzure in productie implementeert, kunt u tooadd meer foutafhandeling of andere onderdelen.</span><span class="sxs-lookup"><span data-stu-id="3c5f3-132">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="3c5f3-133">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3c5f3-133">For example:</span></span>

* <span data-ttu-id="3c5f3-134">In plaats van een webformulier, Azure storage-blobs of SQL-Database toostore telefoonnummers te gebruiken en aanroepen van tekst.</span><span class="sxs-lookup"><span data-stu-id="3c5f3-134">Instead of using a web form, you could use Azure storage blobs or SQL Database toostore phone numbers and call text.</span></span> <span data-ttu-id="3c5f3-135">Zie voor meer informatie over het gebruik van Azure storage-blobs in PHP [Azure Storage gebruiken met PHP-toepassingen][howto_blob_storage_php].</span><span class="sxs-lookup"><span data-stu-id="3c5f3-135">For information about using Azure storage blobs in PHP, see [Using Azure Storage with PHP Applications][howto_blob_storage_php].</span></span> <span data-ttu-id="3c5f3-136">Zie voor meer informatie over het gebruik van SQL-Database in PHP [met behulp van SQL Database met PHP-toepassingen][howto_sql_azure_php].</span><span class="sxs-lookup"><span data-stu-id="3c5f3-136">For information about using SQL Database in PHP, see [Using SQL Database with PHP Applications][howto_sql_azure_php].</span></span>
* <span data-ttu-id="3c5f3-137">Hallo **makecall.php** code gebruikt Twilio-geleverde URL ([http://twimlets.com/message][twimlet_message_url]) tooprovide een Twilio Markup Language (TwiML) antwoord dat Twilio hoe informeert tooproceed met Hallo-aanroep.</span><span class="sxs-lookup"><span data-stu-id="3c5f3-137">hello **makecall.php** code uses Twilio-provided URL ([http://twimlets.com/message][twimlet_message_url]) tooprovide a Twilio Markup Language (TwiML) response that informs Twilio how tooproceed with hello call.</span></span> <span data-ttu-id="3c5f3-138">Bijvoorbeeld, Hallo TwiML die wordt geretourneerd kunt bevatten een `<Say>` term die resulteert in de tekst wordt gesproken toohello aanroep ontvanger.</span><span class="sxs-lookup"><span data-stu-id="3c5f3-138">For example, hello TwiML that is returned can contain a `<Say>` verb that results in text being spoken toohello call recipient.</span></span> <span data-ttu-id="3c5f3-139">In plaats van Hallo geleverde Twilio-URL, kan u uw eigen service toorespond tooTwilio aanvraag; samenstellen Zie voor meer informatie [hoe tooUse Twilio voor spraak- en SMS-mogelijkheden van PHP][howto_twilio_voice_sms_php].</span><span class="sxs-lookup"><span data-stu-id="3c5f3-139">Instead of using hello Twilio-provided URL, you could build your own service toorespond tooTwilio's request; for more information, see [How tooUse Twilio for Voice and SMS Capabilities in PHP][howto_twilio_voice_sms_php].</span></span> <span data-ttu-id="3c5f3-140">Meer informatie over TwiML kan worden gevonden op [http://www.twilio.com/docs/api/twiml][twiml], en meer informatie over `<Say>` en andere Twilio-termen kunnen worden gevonden op [http:// www.twilio.com/Docs/API/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="3c5f3-140">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about `<Say>` and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="3c5f3-141">Hallo Twilio-richtlijnen voor beveiliging op lezen [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="3c5f3-141">Read hello Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="3c5f3-142">Zie voor meer informatie over Twilio [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="3c5f3-142">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="3c5f3-143">Zie ook</span><span class="sxs-lookup"><span data-stu-id="3c5f3-143">See Also</span></span>
* [<span data-ttu-id="3c5f3-144">Hoe tooUse Twilio voor spraak- en SMS-mogelijkheden van PHP</span><span class="sxs-lookup"><span data-stu-id="3c5f3-144">How tooUse Twilio for Voice and SMS Capabilities in PHP</span></span>](partner-twilio-php-how-to-use-voice-sms.md)

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
