---
title: aaaHow toouse hello SendGrid e-mailservice (Java) | Microsoft Docs
description: Meer informatie over hoe e-mailbericht met de SendGrid-e-mailservice Hallo verzenden in Azure. Codevoorbeelden geschreven in Java.
services: 
documentationcenter: java
author: thinkingserious
manager: sendgrid
editor: mollybos
ms.assetid: cc75c43e-ede9-492b-98c2-9147fcb92c21
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 10/30/2014
ms.author: elmer.thomas@sendgrid.com; erika.berkland@sendgrid.com; vibhork
ms.openlocfilehash: 542ce0003e94fc8f5551487d5a3cd6f75d27e8cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-java"></a><span data-ttu-id="9d1c9-104">Hoe tooSend E-mail met behulp van SendGrid met Java</span><span class="sxs-lookup"><span data-stu-id="9d1c9-104">How tooSend Email Using SendGrid from Java</span></span>
<span data-ttu-id="9d1c9-105">Deze handleiding wordt uitgelegd hoe e tooperform algemene programmeertaken met de SendGrid-service op Azure.</span><span class="sxs-lookup"><span data-stu-id="9d1c9-105">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="9d1c9-106">Hallo-voorbeelden zijn geschreven in Java.</span><span class="sxs-lookup"><span data-stu-id="9d1c9-106">hello samples are written in Java.</span></span> <span data-ttu-id="9d1c9-107">Hallo scenario's worden behandeld: **construeren e**, **verzenden van e-mail**, **bijlagen toevoegen**, **met filters**, en **eigenschappen bijwerken**.</span><span class="sxs-lookup"><span data-stu-id="9d1c9-107">hello scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="9d1c9-108">Zie voor meer informatie over SendGrid en verzenden van e-mail Hallo [Vervolgstappen](#next-steps) sectie.</span><span class="sxs-lookup"><span data-stu-id="9d1c9-108">For more information on SendGrid and sending email, see hello [Next steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="9d1c9-109">Wat is Hallo SendGrid e-mailservice?</span><span class="sxs-lookup"><span data-stu-id="9d1c9-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="9d1c9-110">SendGrid is een [cloud-gebaseerde e-mailservice] die biedt betrouwbare [levering van de transactionele e], schaalbaarheid en realtime-analyses samen met de flexibele API's die aangepaste integratie te vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="9d1c9-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="9d1c9-111">Veelvoorkomende gebruiksscenario's van SendGrid zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="9d1c9-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="9d1c9-112">Ontvangstbevestigingen toocustomers automatisch verzenden</span><span class="sxs-lookup"><span data-stu-id="9d1c9-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="9d1c9-113">Beheer van distributiepunt bevat voor het verzenden van klanten maandelijkse e-Folders en speciale aanbiedingen</span><span class="sxs-lookup"><span data-stu-id="9d1c9-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="9d1c9-114">Realtime metrische gegevens voor items zoals geblokkeerd e- en reactietijd van de klant verzamelen</span><span class="sxs-lookup"><span data-stu-id="9d1c9-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="9d1c9-115">Genereren van rapporten toohelp trends identificeren</span><span class="sxs-lookup"><span data-stu-id="9d1c9-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="9d1c9-116">Doorsturen van vragen van klanten</span><span class="sxs-lookup"><span data-stu-id="9d1c9-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="9d1c9-117">E-mailmeldingen van uw toepassing</span><span class="sxs-lookup"><span data-stu-id="9d1c9-117">Email notifications from your application</span></span>

<span data-ttu-id="9d1c9-118">Zie voor meer informatie <http://sendgrid.com>.</span><span class="sxs-lookup"><span data-stu-id="9d1c9-118">For more information, see <http://sendgrid.com>.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="9d1c9-119">Een SendGrid-account maken</span><span class="sxs-lookup"><span data-stu-id="9d1c9-119">Create a SendGrid account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-hello-javaxmail-libraries"></a><span data-ttu-id="9d1c9-120">Hoe: Hallo javax.mail bibliotheken</span><span class="sxs-lookup"><span data-stu-id="9d1c9-120">How to: Use hello javax.mail libraries</span></span>
<span data-ttu-id="9d1c9-121">Hallo javax.mail bibliotheken, bijvoorbeeld verkrijgen van <http://www.oracle.com/technetwork/java/javamail> en importeer ze in uw code.</span><span class="sxs-lookup"><span data-stu-id="9d1c9-121">Obtain hello javax.mail libraries, for example from <http://www.oracle.com/technetwork/java/javamail> and import them into your code.</span></span> <span data-ttu-id="9d1c9-122">Op een hoog niveau is hello proces voor het gebruik van Hallo javax.mail bibliotheek toosend e-mail via SMTP toodo Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="9d1c9-122">At a high-level, hello process for using hello javax.mail library toosend email using SMTP is toodo hello following:</span></span>

1. <span data-ttu-id="9d1c9-123">Hallo SMTP-waarden, met inbegrip van Hallo SMTP-server, waarop voor SendGrid smtp.sendgrid.net opgeven.</span><span class="sxs-lookup"><span data-stu-id="9d1c9-123">Specify hello SMTP values, including hello SMTP server, which for SendGrid is smtp.sendgrid.net.</span></span>

```
        import java.util.Properties;
        import javax.activation.*;
        import javax.mail.*;
        import javax.mail.internet.*;

        public class MyEmailer {
           private static final String SMTP_HOST_NAME = "smtp.sendgrid.net";
           private static final String SMTP_AUTH_USER = "your_sendgrid_username";
           private static final String SMTP_AUTH_PWD = "your_sendgrid_password";

           public static void main(String[] args) throws Exception{
               new MyEmailer().SendMail();
           }

           public void SendMail() throws Exception
           {
              Properties properties = new Properties();
                 properties.put("mail.transport.protocol", "smtp");
                 properties.put("mail.smtp.host", SMTP_HOST_NAME);
                 properties.put("mail.smtp.port", 587);
                 properties.put("mail.smtp.auth", "true");
                 // …
```

1. <span data-ttu-id="9d1c9-124">Hallo uitbreiden *javax.mail.Authenticator* klasse, en in uw implementatie van de *getPasswordAuthentication* methode, uw SendGrid-gebruikersnaam en wachtwoord worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="9d1c9-124">Extend hello *javax.mail.Authenticator* class, and in your implementation of the *getPasswordAuthentication* method, return your SendGrid user name and password.</span></span>  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. <span data-ttu-id="9d1c9-125">Maken van een sessie geverifieerde e-mail via een *javax.mail.Session* object.</span><span class="sxs-lookup"><span data-stu-id="9d1c9-125">Create an authenticated email session through a *javax.mail.Session* object.</span></span>  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. <span data-ttu-id="9d1c9-126">Maken van uw bericht en toewijzen **naar**, **van**, **onderwerp** en waarden van inhoud.</span><span class="sxs-lookup"><span data-stu-id="9d1c9-126">Create your message and assign **To**, **From**, **Subject** and content values.</span></span> <span data-ttu-id="9d1c9-127">Dit wordt weergegeven in Hallo [How To: maken van een e-mailbericht](#how-to-create-an-email) sectie.</span><span class="sxs-lookup"><span data-stu-id="9d1c9-127">This is shown in hello [How To: Create an Email](#how-to-create-an-email) section.</span></span>
4. <span data-ttu-id="9d1c9-128">Hallo-mailbericht verzenden via een *javax.mail.Transport* object.</span><span class="sxs-lookup"><span data-stu-id="9d1c9-128">Send hello message through a *javax.mail.Transport* object.</span></span> <span data-ttu-id="9d1c9-129">Dit wordt weergegeven in Hallo [How To: e-mailbericht verzenden] [hoe: e-mailbericht verzenden] sectie.</span><span class="sxs-lookup"><span data-stu-id="9d1c9-129">This is shown in hello [How To: Send an Email][How to: Send an Email] section.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="9d1c9-130">Procedure: een e-mailbericht maken</span><span class="sxs-lookup"><span data-stu-id="9d1c9-130">How to: Create an email</span></span>
<span data-ttu-id="9d1c9-131">Hallo hieronder ziet u hoe toospecify waarden voor een e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="9d1c9-131">hello following shows how toospecify values for an email.</span></span>

    MimeMessage message = new MimeMessage(mailSession);
    Multipart multipart = new MimeMultipart("alternative");
    BodyPart part1 = new MimeBodyPart();
    part1.setText("Hello, Your Contoso order has shipped. Thank you, John");
    BodyPart part2 = new MimeBodyPart();
    part2.setContent(
        "<p>Hello,</p>
        <p>Your Contoso order has <b>shipped</b>.</p>
        <p>Thank you,<br>John</br></p>",
        "text/html");
    multipart.addBodyPart(part1);
    multipart.addBodyPart(part2);
    message.setFrom(new InternetAddress("john@contoso.com"));
    message.addRecipient(Message.RecipientType.TO,
       new InternetAddress("someone@example.com"));
    message.setSubject("Your recent order");
    message.setContent(multipart);

## <a name="how-to-send-an-email"></a><span data-ttu-id="9d1c9-132">Procedure: een e-mailbericht verzenden</span><span class="sxs-lookup"><span data-stu-id="9d1c9-132">How to: Send an email</span></span>
<span data-ttu-id="9d1c9-133">Hallo toont hoe na toosend een e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="9d1c9-133">hello following shows how toosend an email.</span></span>

    Transport transport = mailSession.getTransport();
    // Connect hello transport object.
    transport.connect();
    // Send hello message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close hello connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="9d1c9-134">Procedure: een bijlage toevoegen</span><span class="sxs-lookup"><span data-stu-id="9d1c9-134">How to: Add an attachment</span></span>
<span data-ttu-id="9d1c9-135">Hallo volgende code toont u hoe tooadd bijlage.</span><span class="sxs-lookup"><span data-stu-id="9d1c9-135">hello following code shows you how tooadd an attachment.</span></span>

    // Local file name and path.
    String attachmentName = "myfile.zip";
    String attachmentPath = "c:\\myfiles\\";
    MimeBodyPart attachmentPart = new MimeBodyPart();
    // Specify hello local file tooattach.
    DataSource source = new FileDataSource(attachmentPath + attachmentName);
    attachmentPart.setDataHandler(new DataHandler(source));
    // This example uses hello local file name as hello attachment name.
    // They could be different if you prefer.
    attachmentPart.setFileName(attachmentName);
    multipart.addBodyPart(attachmentPart);

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="9d1c9-136">Hoe: Gebruik filters tooenable voetteksten, bijhouden en analyses</span><span class="sxs-lookup"><span data-stu-id="9d1c9-136">How to: Use filters tooenable footers, tracking, and analytics</span></span>
<span data-ttu-id="9d1c9-137">SendGrid biedt extra e-mailfunctionaliteit via Hallo *filters*.</span><span class="sxs-lookup"><span data-stu-id="9d1c9-137">SendGrid provides additional email functionality through hello use of *filters*.</span></span> <span data-ttu-id="9d1c9-138">Dit zijn de instellingen die kunnen worden toegevoegd als tooan e-mailbericht naar het inschakelen van specifieke functionaliteit, zoals het inschakelen van Klik bijhouden, Google analytics, abonnement bijhouden, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="9d1c9-138">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="9d1c9-139">Zie voor een volledige lijst met filters [filterinstellingen][Filter Settings].</span><span class="sxs-lookup"><span data-stu-id="9d1c9-139">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

* <span data-ttu-id="9d1c9-140">Hallo hieronder ziet u hoe tooinsert een voettekst filter die resulteert in een HTML-tekst die wordt weergegeven onder Hallo van Hallo e-mail worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="9d1c9-140">hello following shows how tooinsert a footer filter that results in HTML text appearing at hello bottom of hello email being sent.</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* <span data-ttu-id="9d1c9-141">Een ander voorbeeld van een filter is klikt u op bijhouden.</span><span class="sxs-lookup"><span data-stu-id="9d1c9-141">Another example of a filter is click tracking.</span></span> <span data-ttu-id="9d1c9-142">Stel dat uw e-mailtekst bevat een hyperlink, zoals hello volgende, en u wilt dat tootrack Hallo klikt u op classificeren:</span><span class="sxs-lookup"><span data-stu-id="9d1c9-142">Let’s say that your email text contains a hyperlink, such as hello following, and you want tootrack hello click rate:</span></span>

      messagePart.setContent(
          "Hello,
          <p>This is hello body of hello message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* <span data-ttu-id="9d1c9-143">tooenable hello klikt u op het bijhouden van gebruik Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="9d1c9-143">tooenable hello click tracking, use hello following code:</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a><span data-ttu-id="9d1c9-144">Procedure: e-eigenschappen bijwerken</span><span class="sxs-lookup"><span data-stu-id="9d1c9-144">How to: Update email properties</span></span>
<span data-ttu-id="9d1c9-145">Sommige eigenschappen van de e-mail kunnen worden overschreven met  **ingesteld*eigenschap*** of toegevoegd met behulp van  **toevoegen*eigenschap***.</span><span class="sxs-lookup"><span data-stu-id="9d1c9-145">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span>

<span data-ttu-id="9d1c9-146">Bijvoorbeeld: toospecify **ReplyTo** adressen, gebruikt u Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="9d1c9-146">For example, toospecify **ReplyTo** addresses, use hello following:</span></span>

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

<span data-ttu-id="9d1c9-147">tooadd een **Cc** geadresseerde gebruik Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="9d1c9-147">tooadd a **Cc** recipient, use hello following:</span></span>

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="9d1c9-148">Procedure: aanvullende SendGrid-services gebruiken</span><span class="sxs-lookup"><span data-stu-id="9d1c9-148">How to: Use additional SendGrid services</span></span>
<span data-ttu-id="9d1c9-149">SendGrid biedt op basis van een web-API's die u tooleverage aanvullende SendGrid-functionaliteit van uw Azure-toepassing kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9d1c9-149">SendGrid offers web-based APIs that you can use tooleverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="9d1c9-150">Zie voor meer details Hallo [SendGrid-API-documentatie][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="9d1c9-150">For full details, see hello [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d1c9-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9d1c9-151">Next steps</span></span>
<span data-ttu-id="9d1c9-152">Nu u basisprincipes Hallo Hallo SendGrid-e-mailservice hebt geleerd, volgt u deze koppelingen toolearn meer.</span><span class="sxs-lookup"><span data-stu-id="9d1c9-152">Now that you’ve learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="9d1c9-153">Voorbeeldbestand dat laat zien met SendGrid in een Azure-implementatie: [hoe toosend e-SendGrid van Java gebruiken in een Azure-implementatie](store-sendgrid-java-how-to-send-email-example.md)</span><span class="sxs-lookup"><span data-stu-id="9d1c9-153">Sample that demonstrates using SendGrid in an Azure deployment: [How toosend email using SendGrid from Java in an Azure deployment](store-sendgrid-java-how-to-send-email-example.md)</span></span>
* <span data-ttu-id="9d1c9-154">SendGrid Java SDK: <https://sendgrid.com/docs/Code_Examples/java.html></span><span class="sxs-lookup"><span data-stu-id="9d1c9-154">SendGrid Java SDK: <https://sendgrid.com/docs/Code_Examples/java.html></span></span>
* <span data-ttu-id="9d1c9-155">SendGrid-API-documentatie: <https://sendgrid.com/docs/API_Reference/index.html></span><span class="sxs-lookup"><span data-stu-id="9d1c9-155">SendGrid API documentation: <https://sendgrid.com/docs/API_Reference/index.html></span></span>
* <span data-ttu-id="9d1c9-156">SendGrid speciale aanbieding voor Azure-klanten: <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="9d1c9-156">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

[http://sendgrid.com]: https://sendgrid.com
[http://sendgrid.com/pricing.html]: http://sendgrid.com/pricing.html
[http://www.sendgrid.com/azure.html]: https://www.sendgrid.com/windowsazure.html
[http://sendgrid.com/features]: https://sendgrid.com/features
[http://www.oracle.com/technetwork/java/javamail]: http://www.oracle.com/technetwork/java/javamail/index.html
[Filter Settings]: https://sendgrid.com/docs/API_Reference/Web_API/filter_settings.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/index.html
[http://sendgrid.com/azure.html]: https://sendgrid.com/windowsazure.html
[cloud-gebaseerde e-mailservice]: https://sendgrid.com/email-solutions
[levering van de transactionele e]: https://sendgrid.com/transactional-email
