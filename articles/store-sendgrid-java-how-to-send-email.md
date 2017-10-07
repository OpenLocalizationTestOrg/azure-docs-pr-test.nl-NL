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
# <a name="how-toosend-email-using-sendgrid-from-java"></a>Hoe tooSend E-mail met behulp van SendGrid met Java
Deze handleiding wordt uitgelegd hoe e tooperform algemene programmeertaken met de SendGrid-service op Azure. Hallo-voorbeelden zijn geschreven in Java. Hallo scenario's worden behandeld: **construeren e**, **verzenden van e-mail**, **bijlagen toevoegen**, **met filters**, en **eigenschappen bijwerken**. Zie voor meer informatie over SendGrid en verzenden van e-mail Hallo [Vervolgstappen](#next-steps) sectie.

## <a name="what-is-hello-sendgrid-email-service"></a>Wat is Hallo SendGrid e-mailservice?
SendGrid is een [cloud-gebaseerde e-mailservice] die biedt betrouwbare [levering van de transactionele e], schaalbaarheid en realtime-analyses samen met de flexibele API's die aangepaste integratie te vereenvoudigen. Veelvoorkomende gebruiksscenario's van SendGrid zijn onder andere:

* Ontvangstbevestigingen toocustomers automatisch verzenden
* Beheer van distributiepunt bevat voor het verzenden van klanten maandelijkse e-Folders en speciale aanbiedingen
* Realtime metrische gegevens voor items zoals geblokkeerd e- en reactietijd van de klant verzamelen
* Genereren van rapporten toohelp trends identificeren
* Doorsturen van vragen van klanten
* E-mailmeldingen van uw toepassing

Zie voor meer informatie <http://sendgrid.com>.

## <a name="create-a-sendgrid-account"></a>Een SendGrid-account maken
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-hello-javaxmail-libraries"></a>Hoe: Hallo javax.mail bibliotheken
Hallo javax.mail bibliotheken, bijvoorbeeld verkrijgen van <http://www.oracle.com/technetwork/java/javamail> en importeer ze in uw code. Op een hoog niveau is hello proces voor het gebruik van Hallo javax.mail bibliotheek toosend e-mail via SMTP toodo Hallo volgende:

1. Hallo SMTP-waarden, met inbegrip van Hallo SMTP-server, waarop voor SendGrid smtp.sendgrid.net opgeven.

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

1. Hallo uitbreiden *javax.mail.Authenticator* klasse, en in uw implementatie van de *getPasswordAuthentication* methode, uw SendGrid-gebruikersnaam en wachtwoord worden geretourneerd.  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. Maken van een sessie geverifieerde e-mail via een *javax.mail.Session* object.  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. Maken van uw bericht en toewijzen **naar**, **van**, **onderwerp** en waarden van inhoud. Dit wordt weergegeven in Hallo [How To: maken van een e-mailbericht](#how-to-create-an-email) sectie.
4. Hallo-mailbericht verzenden via een *javax.mail.Transport* object. Dit wordt weergegeven in Hallo [How To: e-mailbericht verzenden] [hoe: e-mailbericht verzenden] sectie.

## <a name="how-to-create-an-email"></a>Procedure: een e-mailbericht maken
Hallo hieronder ziet u hoe toospecify waarden voor een e-mailbericht.

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

## <a name="how-to-send-an-email"></a>Procedure: een e-mailbericht verzenden
Hallo toont hoe na toosend een e-mailbericht.

    Transport transport = mailSession.getTransport();
    // Connect hello transport object.
    transport.connect();
    // Send hello message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close hello connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a>Procedure: een bijlage toevoegen
Hallo volgende code toont u hoe tooadd bijlage.

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

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a>Hoe: Gebruik filters tooenable voetteksten, bijhouden en analyses
SendGrid biedt extra e-mailfunctionaliteit via Hallo *filters*. Dit zijn de instellingen die kunnen worden toegevoegd als tooan e-mailbericht naar het inschakelen van specifieke functionaliteit, zoals het inschakelen van Klik bijhouden, Google analytics, abonnement bijhouden, enzovoort. Zie voor een volledige lijst met filters [filterinstellingen][Filter Settings].

* Hallo hieronder ziet u hoe tooinsert een voettekst filter die resulteert in een HTML-tekst die wordt weergegeven onder Hallo van Hallo e-mail worden verzonden.

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* Een ander voorbeeld van een filter is klikt u op bijhouden. Stel dat uw e-mailtekst bevat een hyperlink, zoals hello volgende, en u wilt dat tootrack Hallo klikt u op classificeren:

      messagePart.setContent(
          "Hello,
          <p>This is hello body of hello message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* tooenable hello klikt u op het bijhouden van gebruik Hallo code te volgen:

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a>Procedure: e-eigenschappen bijwerken
Sommige eigenschappen van de e-mail kunnen worden overschreven met  **ingesteld*eigenschap*** of toegevoegd met behulp van  **toevoegen*eigenschap***.

Bijvoorbeeld: toospecify **ReplyTo** adressen, gebruikt u Hallo volgende:

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

tooadd een **Cc** geadresseerde gebruik Hallo volgende:

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a>Procedure: aanvullende SendGrid-services gebruiken
SendGrid biedt op basis van een web-API's die u tooleverage aanvullende SendGrid-functionaliteit van uw Azure-toepassing kunt gebruiken. Zie voor meer details Hallo [SendGrid-API-documentatie][SendGrid API documentation].

## <a name="next-steps"></a>Volgende stappen
Nu u basisprincipes Hallo Hallo SendGrid-e-mailservice hebt geleerd, volgt u deze koppelingen toolearn meer.

* Voorbeeldbestand dat laat zien met SendGrid in een Azure-implementatie: [hoe toosend e-SendGrid van Java gebruiken in een Azure-implementatie](store-sendgrid-java-how-to-send-email-example.md)
* SendGrid Java SDK: <https://sendgrid.com/docs/Code_Examples/java.html>
* SendGrid-API-documentatie: <https://sendgrid.com/docs/API_Reference/index.html>
* SendGrid speciale aanbieding voor Azure-klanten: <https://sendgrid.com/windowsazure.html>

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
