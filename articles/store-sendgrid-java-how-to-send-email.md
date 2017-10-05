---
title: Het gebruik van de SendGrid-e-mailservice (Java) | Microsoft Docs
description: Meer informatie over hoe verzenden van e-mailbericht met de SendGrid-e-mailservice op Azure. Codevoorbeelden geschreven in Java.
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
ms.openlocfilehash: 85a0e302626ca14ac039ee6f662f372ddbeb62c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-send-email-using-sendgrid-from-java"></a><span data-ttu-id="ec39f-104">Het verzenden van E-mail via SendGrid met Java</span><span class="sxs-lookup"><span data-stu-id="ec39f-104">How to Send Email Using SendGrid from Java</span></span>
<span data-ttu-id="ec39f-105">Deze handleiding wordt uitgelegd hoe u algemene programmeertaken met de SendGrid-e-mailservice uitvoert op Azure.</span><span class="sxs-lookup"><span data-stu-id="ec39f-105">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="ec39f-106">De voorbeelden zijn geschreven in Java.</span><span class="sxs-lookup"><span data-stu-id="ec39f-106">The samples are written in Java.</span></span> <span data-ttu-id="ec39f-107">De scenario's worden behandeld: **construeren e**, **verzenden van e-mail**, **bijlagen toevoegen**, **met filters**, en **eigenschappen bijwerken**.</span><span class="sxs-lookup"><span data-stu-id="ec39f-107">The scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="ec39f-108">Zie voor meer informatie over SendGrid en verzenden van e-mail, de [Vervolgstappen](#next-steps) sectie.</span><span class="sxs-lookup"><span data-stu-id="ec39f-108">For more information on SendGrid and sending email, see the [Next steps](#next-steps) section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="ec39f-109">Wat is de SendGrid-e-mailservice?</span><span class="sxs-lookup"><span data-stu-id="ec39f-109">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="ec39f-110">SendGrid is een [cloud-gebaseerde e-mailservice] die biedt betrouwbare [levering van de transactionele e], schaalbaarheid en realtime-analyses samen met de flexibele API's die aangepaste integratie te vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="ec39f-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="ec39f-111">Veelvoorkomende gebruiksscenario's van SendGrid zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="ec39f-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="ec39f-112">Automatisch verzenden van meldingen op klanten</span><span class="sxs-lookup"><span data-stu-id="ec39f-112">Automatically sending receipts to customers</span></span>
* <span data-ttu-id="ec39f-113">Beheer van distributiepunt bevat voor het verzenden van klanten maandelijkse e-Folders en speciale aanbiedingen</span><span class="sxs-lookup"><span data-stu-id="ec39f-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="ec39f-114">Realtime metrische gegevens voor items zoals geblokkeerd e- en reactietijd van de klant verzamelen</span><span class="sxs-lookup"><span data-stu-id="ec39f-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="ec39f-115">Genereren van rapporten om trends te identificeren</span><span class="sxs-lookup"><span data-stu-id="ec39f-115">Generating reports to help identify trends</span></span>
* <span data-ttu-id="ec39f-116">Doorsturen van vragen van klanten</span><span class="sxs-lookup"><span data-stu-id="ec39f-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="ec39f-117">E-mailmeldingen van uw toepassing</span><span class="sxs-lookup"><span data-stu-id="ec39f-117">Email notifications from your application</span></span>

<span data-ttu-id="ec39f-118">Zie voor meer informatie <http://sendgrid.com>.</span><span class="sxs-lookup"><span data-stu-id="ec39f-118">For more information, see <http://sendgrid.com>.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="ec39f-119">Een SendGrid-account maken</span><span class="sxs-lookup"><span data-stu-id="ec39f-119">Create a SendGrid account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-the-javaxmail-libraries"></a><span data-ttu-id="ec39f-120">Procedure: de bibliotheken javax.mail gebruiken</span><span class="sxs-lookup"><span data-stu-id="ec39f-120">How to: Use the javax.mail libraries</span></span>
<span data-ttu-id="ec39f-121">De bibliotheken javax.mail bijvoorbeeld verkrijgen van <http://www.oracle.com/technetwork/java/javamail> en importeer ze in uw code.</span><span class="sxs-lookup"><span data-stu-id="ec39f-121">Obtain the javax.mail libraries, for example from <http://www.oracle.com/technetwork/java/javamail> and import them into your code.</span></span> <span data-ttu-id="ec39f-122">Op een hoog niveau is het proces voor het gebruik van de bibliotheek javax.mail om via SMTP e-mail te verzenden naar het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="ec39f-122">At a high-level, the process for using the javax.mail library to send email using SMTP is to do the following:</span></span>

1. <span data-ttu-id="ec39f-123">Geef de SMTP-waarden, met inbegrip van de SMTP-server die voor SendGrid smtp.sendgrid.net.</span><span class="sxs-lookup"><span data-stu-id="ec39f-123">Specify the SMTP values, including the SMTP server, which for SendGrid is smtp.sendgrid.net.</span></span>

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

1. <span data-ttu-id="ec39f-124">Breid de *javax.mail.Authenticator* klasse, en in uw implementatie van de *getPasswordAuthentication* methode, uw SendGrid-gebruikersnaam en wachtwoord worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="ec39f-124">Extend the *javax.mail.Authenticator* class, and in your implementation of the *getPasswordAuthentication* method, return your SendGrid user name and password.</span></span>  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. <span data-ttu-id="ec39f-125">Maken van een sessie geverifieerde e-mail via een *javax.mail.Session* object.</span><span class="sxs-lookup"><span data-stu-id="ec39f-125">Create an authenticated email session through a *javax.mail.Session* object.</span></span>  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. <span data-ttu-id="ec39f-126">Maken van uw bericht en toewijzen **naar**, **van**, **onderwerp** en waarden van inhoud.</span><span class="sxs-lookup"><span data-stu-id="ec39f-126">Create your message and assign **To**, **From**, **Subject** and content values.</span></span> <span data-ttu-id="ec39f-127">Dit wordt weergegeven in de [How To: maken van een e-mailbericht](#how-to-create-an-email) sectie.</span><span class="sxs-lookup"><span data-stu-id="ec39f-127">This is shown in the [How To: Create an Email](#how-to-create-an-email) section.</span></span>
4. <span data-ttu-id="ec39f-128">Het bericht verzenden via een *javax.mail.Transport* object.</span><span class="sxs-lookup"><span data-stu-id="ec39f-128">Send the message through a *javax.mail.Transport* object.</span></span> <span data-ttu-id="ec39f-129">Dit wordt weergegeven in de [How To: e-mailbericht verzenden] [hoe: e-mailbericht verzenden] sectie.</span><span class="sxs-lookup"><span data-stu-id="ec39f-129">This is shown in the [How To: Send an Email][How to: Send an Email] section.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="ec39f-130">Procedure: een e-mailbericht maken</span><span class="sxs-lookup"><span data-stu-id="ec39f-130">How to: Create an email</span></span>
<span data-ttu-id="ec39f-131">Hieronder ziet u hoe u waarden opgeven voor een e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="ec39f-131">The following shows how to specify values for an email.</span></span>

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

## <a name="how-to-send-an-email"></a><span data-ttu-id="ec39f-132">Procedure: een e-mailbericht verzenden</span><span class="sxs-lookup"><span data-stu-id="ec39f-132">How to: Send an email</span></span>
<span data-ttu-id="ec39f-133">Hieronder ziet u hoe u een e-mailbericht verzendt.</span><span class="sxs-lookup"><span data-stu-id="ec39f-133">The following shows how to send an email.</span></span>

    Transport transport = mailSession.getTransport();
    // Connect the transport object.
    transport.connect();
    // Send the message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close the connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="ec39f-134">Procedure: een bijlage toevoegen</span><span class="sxs-lookup"><span data-stu-id="ec39f-134">How to: Add an attachment</span></span>
<span data-ttu-id="ec39f-135">De volgende code laat zien hoe een bijlage toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ec39f-135">The following code shows you how to add an attachment.</span></span>

    // Local file name and path.
    String attachmentName = "myfile.zip";
    String attachmentPath = "c:\\myfiles\\";
    MimeBodyPart attachmentPart = new MimeBodyPart();
    // Specify the local file to attach.
    DataSource source = new FileDataSource(attachmentPath + attachmentName);
    attachmentPart.setDataHandler(new DataHandler(source));
    // This example uses the local file name as the attachment name.
    // They could be different if you prefer.
    attachmentPart.setFileName(attachmentName);
    multipart.addBodyPart(attachmentPart);

## <a name="how-to-use-filters-to-enable-footers-tracking-and-analytics"></a><span data-ttu-id="ec39f-136">Procedure: filters gebruiken om in te schakelen voetteksten, tracerings- en analyses</span><span class="sxs-lookup"><span data-stu-id="ec39f-136">How to: Use filters to enable footers, tracking, and analytics</span></span>
<span data-ttu-id="ec39f-137">SendGrid biedt extra e-mailfunctionaliteit met behulp van *filters*.</span><span class="sxs-lookup"><span data-stu-id="ec39f-137">SendGrid provides additional email functionality through the use of *filters*.</span></span> <span data-ttu-id="ec39f-138">Dit zijn de instellingen die kunnen worden toegevoegd aan een e-mailbericht om in te schakelen van specifieke functionaliteit, zoals het inschakelen van Klik bijhouden, Google analytics en abonnement bijhouden.</span><span class="sxs-lookup"><span data-stu-id="ec39f-138">These are settings that can be added to an email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="ec39f-139">Zie voor een volledige lijst met filters [filterinstellingen][Filter Settings].</span><span class="sxs-lookup"><span data-stu-id="ec39f-139">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

* <span data-ttu-id="ec39f-140">Hieronder ziet u hoe u een filter voettekst die resulteert in HTML-tekst die wordt weergegeven aan de onderkant van het e-mailbericht wordt verzonden invoegen.</span><span class="sxs-lookup"><span data-stu-id="ec39f-140">The following shows how to insert a footer filter that results in HTML text appearing at the bottom of the email being sent.</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* <span data-ttu-id="ec39f-141">Een ander voorbeeld van een filter is klikt u op bijhouden.</span><span class="sxs-lookup"><span data-stu-id="ec39f-141">Another example of a filter is click tracking.</span></span> <span data-ttu-id="ec39f-142">Stel dat uw e-mailtekst een hyperlink, zoals de volgende bevat, en u wilt bijhouden van de snelheid klikt u op:</span><span class="sxs-lookup"><span data-stu-id="ec39f-142">Let’s say that your email text contains a hyperlink, such as the following, and you want to track the click rate:</span></span>

      messagePart.setContent(
          "Hello,
          <p>This is the body of the message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* <span data-ttu-id="ec39f-143">Zodat het klikt u op het bijhouden van de volgende code gebruiken:</span><span class="sxs-lookup"><span data-stu-id="ec39f-143">To enable the click tracking, use the following code:</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a><span data-ttu-id="ec39f-144">Procedure: e-eigenschappen bijwerken</span><span class="sxs-lookup"><span data-stu-id="ec39f-144">How to: Update email properties</span></span>
<span data-ttu-id="ec39f-145">Sommige eigenschappen van de e-mail kunnen worden overschreven met  **ingesteld*eigenschap*** of toegevoegd met behulp van  **toevoegen*eigenschap***.</span><span class="sxs-lookup"><span data-stu-id="ec39f-145">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span>

<span data-ttu-id="ec39f-146">Bijvoorbeeld, om op te geven **ReplyTo** adressen, gebruikt u de volgende:</span><span class="sxs-lookup"><span data-stu-id="ec39f-146">For example, to specify **ReplyTo** addresses, use the following:</span></span>

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

<span data-ttu-id="ec39f-147">Om toe te voegen een **Cc** ontvanger, gebruikt u de volgende:</span><span class="sxs-lookup"><span data-stu-id="ec39f-147">To add a **Cc** recipient, use the following:</span></span>

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="ec39f-148">Procedure: aanvullende SendGrid-services gebruiken</span><span class="sxs-lookup"><span data-stu-id="ec39f-148">How to: Use additional SendGrid services</span></span>
<span data-ttu-id="ec39f-149">SendGrid biedt web-API's waarmee u kunt gebruikmaken van aanvullende SendGrid-functionaliteit van uw Azure-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ec39f-149">SendGrid offers web-based APIs that you can use to leverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="ec39f-150">Zie voor meer informatie de [SendGrid-API-documentatie][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="ec39f-150">For full details, see the [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec39f-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ec39f-151">Next steps</span></span>
<span data-ttu-id="ec39f-152">Nu u de basisprincipes van de SendGrid-e-mailservice hebt geleerd, volgt u deze koppelingen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ec39f-152">Now that you’ve learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="ec39f-153">Voorbeeldbestand dat laat zien met SendGrid in een Azure-implementatie: [het verzenden van e-mail via SendGrid van Java in een Azure-implementatie](store-sendgrid-java-how-to-send-email-example.md)</span><span class="sxs-lookup"><span data-stu-id="ec39f-153">Sample that demonstrates using SendGrid in an Azure deployment: [How to send email using SendGrid from Java in an Azure deployment](store-sendgrid-java-how-to-send-email-example.md)</span></span>
* <span data-ttu-id="ec39f-154">SendGrid Java SDK: <https://sendgrid.com/docs/Code_Examples/java.html></span><span class="sxs-lookup"><span data-stu-id="ec39f-154">SendGrid Java SDK: <https://sendgrid.com/docs/Code_Examples/java.html></span></span>
* <span data-ttu-id="ec39f-155">SendGrid-API-documentatie: <https://sendgrid.com/docs/API_Reference/index.html></span><span class="sxs-lookup"><span data-stu-id="ec39f-155">SendGrid API documentation: <https://sendgrid.com/docs/API_Reference/index.html></span></span>
* <span data-ttu-id="ec39f-156">SendGrid speciale aanbieding voor Azure-klanten: <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="ec39f-156">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

[http://sendgrid.com]: https://sendgrid.com
[http://sendgrid.com/pricing.html]: http://sendgrid.com/pricing.html
[http://www.sendgrid.com/azure.html]: https://www.sendgrid.com/windowsazure.html
[http://sendgrid.com/features]: https://sendgrid.com/features
[http://www.oracle.com/technetwork/java/javamail]: http://www.oracle.com/technetwork/java/javamail/index.html
[Filter Settings]: https://sendgrid.com/docs/API_Reference/Web_API/filter_settings.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/index.html
[http://sendgrid.com/azure.html]: https://sendgrid.com/windowsazure.html
<span data-ttu-id="ec39f-157">[cloud-gebaseerde e-mailservice]: https://sendgrid.com/email-solutions</span><span class="sxs-lookup"><span data-stu-id="ec39f-157">[cloud-based email service]: https://sendgrid.com/email-solutions</span></span>
<span data-ttu-id="ec39f-158">[levering van de transactionele e]: https://sendgrid.com/transactional-email</span><span class="sxs-lookup"><span data-stu-id="ec39f-158">[transactional email delivery]: https://sendgrid.com/transactional-email</span></span>
