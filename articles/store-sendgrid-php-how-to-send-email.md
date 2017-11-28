---
title: aaaHow toouse hello SendGrid e-mailservice (PHP) | Microsoft Docs
description: Meer informatie over hoe e-mailbericht met de SendGrid-e-mailservice Hallo verzenden in Azure. Codevoorbeelden geschreven in PHP.
documentationcenter: php
services: 
manager: sendgrid
editor: mollybos
author: thinkingserious
ms.assetid: 51a9928a-4c9e-4b0a-aca8-9a408aeb6f47
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 10/30/2014
ms.author: elmer.thomas@sendgrid.com; erika.berkland@sendgrid.com; vibhork; matt.bernier@sendgrid.com
ms.openlocfilehash: 0076e56dc185cb8f52e629395e7d2c143cb5cfa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-sendgrid-email-service-from-php"></a><span data-ttu-id="e88a8-104">Hoe tooUse Hallo SendGrid e-mailservice met PHP</span><span class="sxs-lookup"><span data-stu-id="e88a8-104">How tooUse hello SendGrid Email Service from PHP</span></span>
<span data-ttu-id="e88a8-105">Deze handleiding wordt uitgelegd hoe tooperform algemene programmeertaken Hello SendGrid e-service op Azure.</span><span class="sxs-lookup"><span data-stu-id="e88a8-105">This guide demonstrates how tooperform common programming tasks with hello SendGrid email service on Azure.</span></span> <span data-ttu-id="e88a8-106">Hallo-voorbeelden zijn geschreven in PHP.</span><span class="sxs-lookup"><span data-stu-id="e88a8-106">hello samples are written in PHP.</span></span>
<span data-ttu-id="e88a8-107">Hallo scenario's worden behandeld: **construeren e**, **verzenden van e-mail**, en **bijlagen toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e88a8-107">hello scenarios covered include **constructing email**, **sending email**, and **adding attachments**.</span></span> <span data-ttu-id="e88a8-108">Zie voor meer informatie over SendGrid en verzenden van e-mail Hallo [Vervolgstappen](#next-steps) sectie.</span><span class="sxs-lookup"><span data-stu-id="e88a8-108">For more information on SendGrid and sending email, see hello [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="e88a8-109">Wat is Hallo SendGrid e-mailservice?</span><span class="sxs-lookup"><span data-stu-id="e88a8-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="e88a8-110">SendGrid is een [cloud-gebaseerde e-mailservice] die biedt betrouwbare [levering van de transactionele e], schaalbaarheid en realtime-analyses samen met de flexibele API's die aangepaste integratie te vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="e88a8-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="e88a8-111">Veelvoorkomende gebruiksscenario's van SendGrid zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="e88a8-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="e88a8-112">Ontvangstbevestigingen toocustomers automatisch verzenden</span><span class="sxs-lookup"><span data-stu-id="e88a8-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="e88a8-113">Beheer van distributiepunt bevat voor het verzenden van klanten maandelijkse e-Folders en speciale aanbiedingen</span><span class="sxs-lookup"><span data-stu-id="e88a8-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="e88a8-114">Realtime metrische gegevens voor items zoals geblokkeerd e- en reactietijd van de klant verzamelen</span><span class="sxs-lookup"><span data-stu-id="e88a8-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="e88a8-115">Genereren van rapporten toohelp trends identificeren</span><span class="sxs-lookup"><span data-stu-id="e88a8-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="e88a8-116">Doorsturen van vragen van klanten</span><span class="sxs-lookup"><span data-stu-id="e88a8-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="e88a8-117">E-mailmeldingen van uw toepassing</span><span class="sxs-lookup"><span data-stu-id="e88a8-117">Email notifications from your application</span></span>

<span data-ttu-id="e88a8-118">Zie voor meer informatie [https://sendgrid.com][https://sendgrid.com].</span><span class="sxs-lookup"><span data-stu-id="e88a8-118">For more information, see [https://sendgrid.com][https://sendgrid.com].</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="e88a8-119">Een SendGrid-Account maken</span><span class="sxs-lookup"><span data-stu-id="e88a8-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="using-sendgrid-from-your-php-application"></a><span data-ttu-id="e88a8-120">Met behulp van SendGrid van uw PHP-toepassing</span><span class="sxs-lookup"><span data-stu-id="e88a8-120">Using SendGrid from your PHP Application</span></span>
<span data-ttu-id="e88a8-121">SendGrid gebruiken in een Azure PHP-toepassing vereist geen speciale configuratie of coderen.</span><span class="sxs-lookup"><span data-stu-id="e88a8-121">Using SendGrid in an Azure PHP application requires no special configuration or coding.</span></span> <span data-ttu-id="e88a8-122">Omdat SendGrid een service is, kan deze worden geopend in exact Hallo dezelfde manier uit een cloudtoepassing kunt vanuit een on-premises toepassing.</span><span class="sxs-lookup"><span data-stu-id="e88a8-122">Because SendGrid is a service, it can be accessed in exactly hello same way from a cloud application as it can from an on-premises application.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="e88a8-123">Procedure: een e-mailbericht verzenden</span><span class="sxs-lookup"><span data-stu-id="e88a8-123">How to: Send an Email</span></span>
<span data-ttu-id="e88a8-124">U kunt e-mails via SMTP- of Hallo geleverd door SendGrid-Web-API verzenden.</span><span class="sxs-lookup"><span data-stu-id="e88a8-124">You can send email using either SMTP or hello Web API provided by SendGrid.</span></span>

### <a name="smtp-api"></a><span data-ttu-id="e88a8-125">SMTP-API</span><span class="sxs-lookup"><span data-stu-id="e88a8-125">SMTP API</span></span>
<span data-ttu-id="e88a8-126">toosend e-mail met Hallo SendGrid SMTP-API, gebruik *Swift e-mailprogramma*, een bibliotheek op basis van onderdelen voor het verzenden van e-mailberichten van PHP-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="e88a8-126">toosend email using hello SendGrid SMTP API, use *Swift Mailer*, a component-based library for sending emails from PHP applications.</span></span> <span data-ttu-id="e88a8-127">U kunt downloaden Hallo *Swift e-mailprogramma* bibliotheek van [http://swiftmailer.org/download] [ http://swiftmailer.org/download] v5.3.0 (Gebruik [Composer] tooinstall SWIFT e-mailprogramma).</span><span class="sxs-lookup"><span data-stu-id="e88a8-127">You can download hello *Swift Mailer* library from [http://swiftmailer.org/download][http://swiftmailer.org/download] v5.3.0 (use [Composer] tooinstall Swift Mailer).</span></span> <span data-ttu-id="e88a8-128">Verzenden van e-mail met Hallo bibliotheek omvat het maken van exemplaren van de <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_e-mailprogramma</span>, en <span class="auto-style2">Swift\_bericht </span> klassen, de juiste instellingen en het aanroepen van de <span class="auto-style2">Swift\_Mailer::send</span> methode.</span><span class="sxs-lookup"><span data-stu-id="e88a8-128">Sending email with hello library involves creating instances of the <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_Mailer</span>, and <span class="auto-style2">Swift\_Message</span> classes, setting the appropriate properties, and calling the <span class="auto-style2">Swift\_Mailer::send</span> method.</span></span>

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create hello body of hello message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of hello email
      * If hello receiver is able tooview html emails then only hello html
      * email will be displayed
      */
     $text = "Hi!\nHow are you?\n";
     $html = "<html>
           <head></head>
           <body>
               <p>Hi!<br>
                   How are you?<br>
               </p>
           </body>
           </html>";
     // This is your From email address
     $from = array('someone@example.com' => 'Name tooAppear');
     // Email recipients
     $too= array(
           'john@contoso.com'=>'Destination 1 Name',
           'anna@contoso.com'=>'Destination 2 Name'
     );
     // Email subject
     $subject = 'Example PHP Email';

     // Login credentials
     $username = 'yoursendgridusername';
     $password = 'yourpassword';

     // Setup Swift mailer parameters
     $transport = Swift_SmtpTransport::newInstance('smtp.sendgrid.net', 587);
     $transport->setUsername($username);
     $transport->setPassword($password);
     $swift = Swift_Mailer::newInstance($transport);

     // Create a message (subject)
     $message = new Swift_Message($subject);

     // attach hello body of hello email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
         // This will let us know how many users received this message
         echo 'Message sent out too'.$recipients.' users';
     }
     // something went wrong =(
     else
     {
         echo "Something went wrong - ";
         print_r($failures);
     }

### <a name="web-api"></a><span data-ttu-id="e88a8-129">Web-API</span><span class="sxs-lookup"><span data-stu-id="e88a8-129">Web API</span></span>
<span data-ttu-id="e88a8-130">Gebruik van PHP [functie curl] [ curl function] toosend e-mail via Hallo SendGrid-Web-API.</span><span class="sxs-lookup"><span data-stu-id="e88a8-130">Use PHP's [curl function][curl function] toosend email using hello SendGrid Web API.</span></span>

    <?php

     $url = 'https://api.sendgrid.com/';
     $user = 'USERNAME';
     $pass = 'PASSWORD';

     $params = array(
          'api_user' => $user,
          'api_key' => $pass,
          'to' => 'john@contoso.com',
          'subject' => 'testing from curl',
          'html' => 'testing body',
          'text' => 'testing body',
          'from' => 'anna@contoso.com',
       );

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl toouse HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is hello body of hello POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not tooreturn headers, but do return hello response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

<span data-ttu-id="e88a8-131">Web-API van SendGrid is heel vergelijkbaar tooa REST API, hoewel het niet echt een RESTful-API omdat in de meeste aanroepen, beide ophalen en POST-bewerkingen door elkaar kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e88a8-131">SendGrid's Web API is very similar tooa REST API, though it is not truly a RESTful API since, in most calls, both GET and POST verbs can be used interchangeably.</span></span>

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="e88a8-132">Procedure: een bijlage toevoegen</span><span class="sxs-lookup"><span data-stu-id="e88a8-132">How to: Add an Attachment</span></span>
### <a name="smtp-api"></a><span data-ttu-id="e88a8-133">SMTP-API</span><span class="sxs-lookup"><span data-stu-id="e88a8-133">SMTP API</span></span>
<span data-ttu-id="e88a8-134">Verzenden van een bijlage Hallo SMTP-API gebruiken, moet u een extra regel code toohello voorbeeldscript voor het verzenden van een e-mail met Swift e-mailprogramma.</span><span class="sxs-lookup"><span data-stu-id="e88a8-134">Sending an attachment using hello SMTP API involves one additional line of code toohello example script for sending an email with Swift Mailer.</span></span>

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create hello body of hello message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of hello email
      * If hello reciever is able tooview html emails then only hello html
      * email will be displayed
      */
     $text = "Hi!\nHow are you?\n";
      $html = "<html>
          <head></head>
          <body>
             <p>Hi!<br>
                How are you?<br>
             </p>
          </body>
          </html>";

     // This is your From email address
     $from = array('someone@example.com' => 'Name tooAppear');

     // Email recipients
     $too= array(
          'john@contoso.com'=>'Destination 1 Name',
          'anna@contoso.com'=>'Destination 2 Name'
     );
     // Email subject
     $subject = 'Example PHP Email';

     // Login credentials
     $username = 'yoursendgridusername';
     $password = 'yourpassword';

     // Setup Swift mailer parameters
     $transport = Swift_SmtpTransport::newInstance('smtp.sendgrid.net', 587);
     $transport->setUsername($username);
     $transport->setPassword($password);
     $swift = Swift_Mailer::newInstance($transport);

     // Create a message (subject)
     $message = new Swift_Message($subject);

     // attach hello body of hello email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');
     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName("file_name"));

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
          // This will let us know how many users received this message
          echo 'Message sent out too'.$recipients.' users';
     }
     // something went wrong =(
     else
     {
          echo "Something went wrong - ";
          print_r($failures);
     }

<span data-ttu-id="e88a8-135">Hallo aanvullende coderegel is als volgt:</span><span class="sxs-lookup"><span data-stu-id="e88a8-135">hello additional line of code is as follows:</span></span>

     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName('file_name'));

<span data-ttu-id="e88a8-136">Deze regel code aanroepen Hallo koppelen op de <span class="auto-style2">Swift\_bericht</span> object en maakt gebruik van statische methode <span class="auto-style2">fromPath</span> op de <span class="auto-style2">Swift\_bijlage</span>tooget klasse en het koppelen van een bestand tooa-bericht.</span><span class="sxs-lookup"><span data-stu-id="e88a8-136">This line of code calls hello attach method on the <span class="auto-style2">Swift\_Message</span> object and uses static method <span class="auto-style2">fromPath</span> on the <span class="auto-style2">Swift\_Attachment</span> class tooget and attach a file tooa message.</span></span>

### <a name="web-api"></a><span data-ttu-id="e88a8-137">Web-API</span><span class="sxs-lookup"><span data-stu-id="e88a8-137">Web API</span></span>
<span data-ttu-id="e88a8-138">Verzenden van een bijlage met Hallo Web-API is heel vergelijkbaar toosending een e-mail met behulp van Web-API Hallo.</span><span class="sxs-lookup"><span data-stu-id="e88a8-138">Sending an attachment using hello Web API is very similar toosending an email using hello Web API.</span></span> <span data-ttu-id="e88a8-139">Let echter op dat in voorbeeld dat volgt op Hallo Hallo parametermatrix dit element bevatten moet:</span><span class="sxs-lookup"><span data-stu-id="e88a8-139">However, note that in hello example that follows, hello parameter array must contain this element:</span></span>

    'files['.$fileName.']' => '@'.$filePath.'/'.$fileName

<span data-ttu-id="e88a8-140">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e88a8-140">Example:</span></span>

    <?php

     $url = 'https://api.sendgrid.com/';
     $user = 'USERNAME';
     $pass = 'PASSWORD';

     $fileName = 'myfile';
     $filePath = dirname(__FILE__);

     $params = array(
         'api_user' => $user,
         'api_key' => $pass,
         'to' =>'john@contoso.com',
         'subject' => 'test of file sends',
         'html' => '<p> hello HTML </p>',
         'text' => 'hello plain text',
         'from' => 'anna@contoso.com',
         'files['.$fileName.']' => '@'.$filePath.'/'.$fileName
     );

     print_r($params);

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl toouse HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is hello body of hello POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not tooreturn headers, but do return hello response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="e88a8-141">Procedure: Filters gebruiken om tooEnable voetteksten, tracerings- en analyses</span><span class="sxs-lookup"><span data-stu-id="e88a8-141">How to: Use Filters tooEnable Footers, Tracking, and Analytics</span></span>
<span data-ttu-id="e88a8-142">SendGrid biedt extra e-mailfunctionaliteit via Hallo 'filters'.</span><span class="sxs-lookup"><span data-stu-id="e88a8-142">SendGrid provides additional email functionality through hello use of 'filters'.</span></span> <span data-ttu-id="e88a8-143">Dit zijn de instellingen die kunnen worden toegevoegd als tooan e-mailbericht naar het inschakelen van specifieke functionaliteit, zoals het inschakelen van Klik bijhouden, Google analytics, abonnement bijhouden, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="e88a8-143">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span>

<span data-ttu-id="e88a8-144">Filters kunnen toegepaste tooa bericht worden met behulp van de eigenschap Hallo-filters.</span><span class="sxs-lookup"><span data-stu-id="e88a8-144">Filters can be applied tooa message by using hello filters property.</span></span> <span data-ttu-id="e88a8-145">Elk filter wordt opgegeven met een hash met filter-specifieke instellingen.</span><span class="sxs-lookup"><span data-stu-id="e88a8-145">Each filter is specified by a hash containing filter-specific settings.</span></span> <span data-ttu-id="e88a8-146">Het volgende voorbeeld wordt Hallo voettekst filter en geeft een bericht op dat wordt toegevoegd onder toohello van Hallo e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="e88a8-146">The following example enables hello footer filter and specifies a text message that will be appended toohello bottom of hello email message.</span></span>
<span data-ttu-id="e88a8-147">In dit voorbeeld gebruiken we [sendgrid-php bibliotheek].</span><span class="sxs-lookup"><span data-stu-id="e88a8-147">For this example we will use [sendgrid-php library].</span></span>
<span data-ttu-id="e88a8-148">Gebruik [Composer] tooinstall bibliotheek:</span><span class="sxs-lookup"><span data-stu-id="e88a8-148">Use [Composer] tooinstall library:</span></span>

    php composer.phar require sendgrid/sendgrid 2.1.1

<span data-ttu-id="e88a8-149">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e88a8-149">Example:</span></span>    

    <?php
     /*
      * This example is used for sendgrid-php V2.1.1 (https://github.com/sendgrid/sendgrid-php/tree/v2.1.1)
      */
     include "vendor/autoload.php";

     $email = new SendGrid\Email();
     // hello list of addresses this message will be sent to
     // [This list is used for sending multiple emails using just ONE request tooSendGrid]
     $toList = array('john@contoso.com', 'anna@contoso.com');

     // Specify hello names of hello recipients
     $nameList = array('Name 1', 'Name 2');

     // Used as an example of variable substitution
     $timeList = array('4 PM', '5 PM');

     // Set all of hello above variables
     $email->setTos($toList);
     $email->addSubstitution('-name-', $nameList);
     $email->addSubstitution('-time-', $timeList);

     // Specify that this is an initial contact message
     $email->addCategory("initial");

     // You can optionally setup individual filters here, in this example, we have
     // enabled hello footer filter
     $email->addFilter('footer', 'enable', 1);
     $email->addFilter('footer', "text/plain", "Thank you for your business");
     $email->addFilter('footer', "text/html", "Thank you for your business");

     // hello subject of your email
     $subject = 'Example SendGrid Email';

     // Where is this message coming from. For example, this message can be from
     // support@yourcompany.com, info@yourcompany.com
     $from = 'someone@example.com';

     // If you do not specify a sender list above, you can specifiy hello user here. If
     // a sender list IS specified above, this email address becomes irrelevant.
     $too= 'john@contoso.com';

     # Create hello body of hello message (a plain-text and an HTML version).
     # text is your plain-text email
     # html is your html version of hello email
     # if hello receiver is able tooview html emails then only hello html
     # email will be displayed

     /*
      * Note hello variable substitution here =)
      */
     $text = "
     Hello -name-,
     Thank you for your interest in our products. We have set up an appointment toocall you at -time- EST toodiscuss your needs in more detail.
     Regards,
     Fred";

     $html = "
     <html>
     <head></head>
     <body>
     <p>Hello -name-,<br>
     Thank you for your interest in our products. We have set up an appointment
     toocall you at -time- EST toodiscuss your needs in more detail.

     Regards,

     Fred<br>
     </p>
     </body>
     </html>";

     // set subject
     $email->setSubject($subject);

     // attach hello body of hello email
     $email->setFrom($from);
     $email->setHtml($html);
     $email->addTo($to);
     $email->setText($text);

     // Your SendGrid account credentials
     $username = 'sendgridusername@yourdomain.com';
     $password = 'example';

     // Create SendGrid object
     $sendgrid = new SendGrid($username, $password);

     // send message
     $response = $sendgrid->send($email);

     print_r($response);

## <a name="next-steps"></a><span data-ttu-id="e88a8-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e88a8-150">Next Steps</span></span>
<span data-ttu-id="e88a8-151">Nu u basisprincipes Hallo Hallo SendGrid-e-mailservice hebt geleerd, volgt u deze koppelingen toolearn meer.</span><span class="sxs-lookup"><span data-stu-id="e88a8-151">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="e88a8-152">SendGrid-documentatie: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="e88a8-152">SendGrid documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="e88a8-153">SendGrid PHP-bibliotheek: <https://github.com/sendgrid/sendgrid-php></span><span class="sxs-lookup"><span data-stu-id="e88a8-153">SendGrid PHP library: <https://github.com/sendgrid/sendgrid-php></span></span>
* <span data-ttu-id="e88a8-154">SendGrid speciale aanbieding voor Azure-klanten: <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="e88a8-154">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

<span data-ttu-id="e88a8-155">Zie voor meer informatie, ook Hallo [PHP-ontwikkelaarscentrum](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="e88a8-155">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[https://sendgrid.com]: https://sendgrid.com
[https://sendgrid.com/transactional-email/pricing]: https://sendgrid.com/transactional-email/pricing
[special offer]: https://www.sendgrid.com/windowsazure.html
[Packaging and Deploying PHP Applications for Azure]: http://msdn.microsoft.com/library/windowsazure/hh674499(v=VS.103).aspx
[http://swiftmailer.org/download]: http://swiftmailer.org/download
[curl function]: http://php.net/curl
[cloud-gebaseerde e-mailservice]: https://sendgrid.com/email-solutions
[levering van de transactionele e]: https://sendgrid.com/transactional-email
[sendgrid-php bibliotheek]: https://github.com/sendgrid/sendgrid-php/tree/v2.1.1
[Composer]: https://getcomposer.org/download/
