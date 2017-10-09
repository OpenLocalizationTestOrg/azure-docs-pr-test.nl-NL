---
title: aaastore-sendgrid-Java-How-to-Send-email-example
description: Hoe toosend e-SendGrid van Java gebruiken in een Azure-implementatie
services: 
documentationcenter: java
author: thinkingserious
manager: sendgrid
editor: mollybos
ms.assetid: af096a73-6985-4350-92e4-ce1722c8d72f
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 10/30/2014
ms.author: vibhork;dominic.may@sendgrid.com;elmer.thomas@sendgrid.com
ms.openlocfilehash: 51fde1fc71467f8252532b30d2f87856ec25067b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-java-in-an-azure-deployment"></a><span data-ttu-id="49c6f-103">Hoe tooSend e SendGrid met behulp van Java in een Azure-implementatie</span><span class="sxs-lookup"><span data-stu-id="49c6f-103">How tooSend Email Using SendGrid from Java in an Azure Deployment</span></span>
<span data-ttu-id="49c6f-104">Hallo volgende voorbeeld ziet u hoe u SendGrid toosend e-mailberichten van een webpagina die wordt gehost in Azure kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="49c6f-104">hello following example shows you how you can use SendGrid toosend emails from a web page hosted in Azure.</span></span> <span data-ttu-id="49c6f-105">de resulterende toepassing Hello wordt Hallo gebruiker gevraagd om e-waarden, zoals wordt weergegeven in de volgende schermopname Hallo.</span><span class="sxs-lookup"><span data-stu-id="49c6f-105">hello resulting application will prompt hello user for email values, as shown in hello following screen shot.</span></span>

![E-formulier][emailform]

<span data-ttu-id="49c6f-107">Hallo resulterende e eruit vergelijkbare toohello volgende schermopname.</span><span class="sxs-lookup"><span data-stu-id="49c6f-107">hello resulting email will look similar toohello following screen shot.</span></span>

![E-mailbericht][emailsent]

<span data-ttu-id="49c6f-109">U moet toodo Hallo volgende toouse Hallo code in dit onderwerp:</span><span class="sxs-lookup"><span data-stu-id="49c6f-109">You'll need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="49c6f-110">Verkrijgen javax.mail potten, bijvoorbeeld Hallo van <http://www.oracle.com/technetwork/java/javamail/index.html>.</span><span class="sxs-lookup"><span data-stu-id="49c6f-110">Obtain hello javax.mail JARs, for example from <http://www.oracle.com/technetwork/java/javamail/index.html>.</span></span>
2. <span data-ttu-id="49c6f-111">Hallo potten tooyour Java build path toevoegen.</span><span class="sxs-lookup"><span data-stu-id="49c6f-111">Add hello JARs tooyour Java build path.</span></span>
3. <span data-ttu-id="49c6f-112">Als u Eclipse toocreate deze Java-toepassing, kunt u Hallo SendGrid bibliotheken kunt opnemen in uw implementatie toepassingsbestand (WAR) met behulp van de functie van Eclipse implementatie-assembly.</span><span class="sxs-lookup"><span data-stu-id="49c6f-112">If you are using Eclipse toocreate this Java application, you can include hello SendGrid libraries in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="49c6f-113">Als u geen Eclipse toocreate deze Java-toepassing, zorg ervoor dat Hallo bibliotheken zijn opgenomen in Hallo dezelfde Azure rol als klassepad voor uw toepassing en toegevoegde toohello van Java van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="49c6f-113">If you are not using Eclipse toocreate this Java application, ensure hello libraries are included within hello same Azure role as your Java application, and added toohello class path of your application.</span></span>

<span data-ttu-id="49c6f-114">U moet ook uw eigen SendGrid-gebruikersnaam en wachtwoord, toobe kunnen toosend Hallo e-mailadres hebben.</span><span class="sxs-lookup"><span data-stu-id="49c6f-114">You must also have your own SendGrid username and password, toobe able toosend hello email.</span></span> <span data-ttu-id="49c6f-115">tooget gestart als de sendgrid, Zie [hoe toosend e-SendGrid met Java met](store-sendgrid-java-how-to-send-email.md).</span><span class="sxs-lookup"><span data-stu-id="49c6f-115">tooget started with SendGrid, see [How toosend email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

<span data-ttu-id="49c6f-116">Bovendien bekend bent met de informatie op Hallo [maken van een toepassing Hello World voor Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), of met andere technieken voor het hosten van Java-toepassingen in Azure als u geen van Eclipse gebruikmaakt wordt sterk aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="49c6f-116">Additionally, familiarity with hello information at [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-sending-email"></a><span data-ttu-id="49c6f-117">Maken van een webformulier voor het verzenden van e-mail</span><span class="sxs-lookup"><span data-stu-id="49c6f-117">Create a web form for sending email</span></span>
<span data-ttu-id="49c6f-118">Hallo volgende code toont hoe een web toocreate formulier tooretrieve gebruikersgegevens voor het verzenden van e-mail.</span><span class="sxs-lookup"><span data-stu-id="49c6f-118">hello following code shows how toocreate a web form tooretrieve user data for sending email.</span></span> <span data-ttu-id="49c6f-119">Voor de doeleinden van deze inhoud Hallo JSP-bestand met de naam **emailform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="49c6f-119">For purposes of this content, hello JSP file is named **emailform.jsp**.</span></span>

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Email form</title>
    </head>
    <body>
     <p>Fill in all fields and click <b>Send this email</b>.</p>
     <br/>
      <form action="sendemail.jsp" method="post">
       <table>
         <tr>
           <td>To:</td>
           <td><input type="text" size=50 name="emailTo">
           </td>
         </tr>
         <tr>
           <td>From:</td>
           <td><input type="text" size=50 name="emailFrom">
           </td>
         </tr>
         <tr>
           <td>Subject:</td>
           <td><input type="text" size=100 name="emailSubject" value="My email subject">
           </td>
         </tr>
         <tr>
           <td>Text:</td>
           <td><input type="text" size=400 name="emailText" value="Hello,<p>This is my message.</p>Thank you." />
           </td>
         </tr>
         <tr>
           <td>SendGrid user name:</td>
           <td><input type="text" name="sendGridUser">
           </td>
         </tr>
         <tr>
           <td>SendGrid password:</td>
           <td><input type="password" name="sendGridPassword">
           </td>
         </tr>
         <tr>
           <td colspan=2><input type="submit" value="Send this email">
           </td>
         </tr>
       </table>
     </form>
     <br/>
    </body>
    </html>

## <a name="create-hello-code-toosend-hello-email"></a><span data-ttu-id="49c6f-120">Hallo code toosend Hallo e-mail maken</span><span class="sxs-lookup"><span data-stu-id="49c6f-120">Create hello code toosend hello email</span></span>
<span data-ttu-id="49c6f-121">Hallo volgende code, die wordt aangeroepen wanneer Hallo formulier in emailform.jsp is voltooid, maakt Hallo e-mailbericht en stuurt deze.</span><span class="sxs-lookup"><span data-stu-id="49c6f-121">hello following code, which is called when you complete hello form in emailform.jsp, creates hello email message and sends it.</span></span> <span data-ttu-id="49c6f-122">Voor de doeleinden van deze inhoud Hallo JSP-bestand met de naam **sendemail.jsp**.</span><span class="sxs-lookup"><span data-stu-id="49c6f-122">For purposes of this content, hello JSP file is named **sendemail.jsp**.</span></span>

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" import="javax.activation.*, javax.mail.*, javax.mail.internet.*, java.util.Date, java.util.Properties" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Email processing happens here</title>
    </head>
    <body>
        <b>This is my send mail page.</b><p/>
     <%

     final String sendGridUser = request.getParameter("sendGridUser");
     final String sendGridPassword = request.getParameter("sendGridPassword");

     class SMTPAuthenticator extends Authenticator
     {
       public PasswordAuthentication getPasswordAuthentication()
       {
            String username = sendGridUser;
            String password = sendGridPassword;

            return new PasswordAuthentication(username, password);   
       }
     }
     try
     {

         // hello SendGrid SMTP server.
         String SMTP_HOST_NAME = "smtp.sendgrid.net";

         Properties properties;

         properties = new Properties();

         // Specify SMTP values.
         properties.put("mail.transport.protocol", "smtp");
         properties.put("mail.smtp.host", SMTP_HOST_NAME);
         properties.put("mail.smtp.port", 587);
         properties.put("mail.smtp.auth", "true");

         // Display hello email fields entered by hello user. 
         out.println("Value entered for email Subject: " + request.getParameter("emailSubject") + "<br/>");        
         out.println("Value entered for email      To: " + request.getParameter("emailTo") + "<br/>");
         out.println("Value entered for email    From: " + request.getParameter("emailFrom") + "<br/>");
         out.println("Value entered for email    Text: " + "<br/>" + request.getParameter("emailText") + "<br/>");

         // Create hello authenticator object.
         Authenticator authenticator = new SMTPAuthenticator();

         // Create hello mail session object.
         Session mailSession;
         mailSession = Session.getDefaultInstance(properties, authenticator);

         // Display debug information toostdout, useful when using the
         // compute emulator during development.
         mailSession.setDebug(true);

         // Create hello message and message part objects.
         MimeMessage message;
         Multipart multipart;
         MimeBodyPart messagePart; 

         message = new MimeMessage(mailSession);

         multipart = new MimeMultipart("alternative");
         messagePart = new MimeBodyPart();
         messagePart.setContent(request.getParameter("emailText"), "text/html");
         multipart.addBodyPart(messagePart);            

         // Specify hello email To, From, Subject and Content. 
         message.setFrom(new InternetAddress(request.getParameter("emailFrom")));
         message.addRecipient(Message.RecipientType.TO, new InternetAddress(request.getParameter("emailTo")));
         message.setSubject(request.getParameter("emailSubject")); 
         message.setContent(multipart);

         // Uncomment hello following if you want tooadd a footer.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"footer\": {\"settings\": {\"enable\":1,\"text/html\": \"<html>This is my <b>email footer</b>.</html>\"}}}}");

         // Uncomment hello following if you want tooenable click tracking.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"clicktrack\": {\"settings\": {\"enable\":1}}}}");

         Transport transport;
         transport = mailSession.getTransport();
         // Connect hello transport object.
         transport.connect();
         // Send hello message.
         transport.sendMessage(message,  message.getRecipients(Message.RecipientType.TO));
         // Close hello connection.
         transport.close();

        out.println("<p>Email processing completed.</p>");

     }
     catch (Exception e)
     {
         out.println("<p>Exception encountered: " + 
                            e.getMessage()     +
                            "</p>");   
     }
    %>

    </body>
    </html>

<span data-ttu-id="49c6f-123">Bovendien toosending Hallo e-mail, emailform.jsp biedt een resultaat voor de gebruiker Hallo; een voorbeeld is de volgende schermopname Hallo:</span><span class="sxs-lookup"><span data-stu-id="49c6f-123">In addition toosending hello email, emailform.jsp provides a result for hello user; an example is hello following screen shot:</span></span>

![Resultaat van de e-mail verzenden][emailresult]

## <a name="next-steps"></a><span data-ttu-id="49c6f-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="49c6f-125">Next steps</span></span>
<span data-ttu-id="49c6f-126">Implementeren van uw toepassing toohello-rekenemulator en vanuit een browser emailform.jsp uitvoeren, kunt u waarden opgeven in formulier hello, klik op **dit e-mailbericht verzenden**, en resulteert in een sendemail.jsp weergegeven.</span><span class="sxs-lookup"><span data-stu-id="49c6f-126">Deploy your application toohello compute emulator and within a browser run emailform.jsp, enter values in hello form, click **Send this email**, and then see results in sendemail.jsp.</span></span>

<span data-ttu-id="49c6f-127">Deze code is opgegeven tooshow u hoe toouse SendGrid in Java in Azure.</span><span class="sxs-lookup"><span data-stu-id="49c6f-127">This code was provided tooshow you how toouse SendGrid in Java on Azure.</span></span> <span data-ttu-id="49c6f-128">Voordat u tooAzure in productie implementeert, kunt u tooadd meer foutafhandeling of andere onderdelen.</span><span class="sxs-lookup"><span data-stu-id="49c6f-128">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="49c6f-129">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="49c6f-129">For example:</span></span> 

* <span data-ttu-id="49c6f-130">U kunt Azure storage-blobs of SQL-Database toostore e-mailadressen en e-mailberichten, in plaats van een webformulier.</span><span class="sxs-lookup"><span data-stu-id="49c6f-130">You could use Azure storage blobs or SQL Database toostore email addresses and email messages, instead of using a web form.</span></span> <span data-ttu-id="49c6f-131">Zie voor meer informatie over het gebruik van Azure storage-blobs in Java [hoe tooUse Blob Storage-Service vanuit Java Hallo](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/).</span><span class="sxs-lookup"><span data-stu-id="49c6f-131">For information about using Azure storage blobs in Java, see [How tooUse hello Blob Storage Service from Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/).</span></span> <span data-ttu-id="49c6f-132">Zie voor meer informatie over het gebruik van SQL-Database in Java [met behulp van SQL-Database in Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).</span><span class="sxs-lookup"><span data-stu-id="49c6f-132">For information about using SQL Database in Java, see [Using SQL Database in Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).</span></span>
* <span data-ttu-id="49c6f-133">U kunt `RoleEnvironment.getConfigurationSettings` tooretrieve hello SendGrid-gebruikersnaam en wachtwoord van uw implementatie-configuratie-instellingen, in plaats van Hallo web formulier tooretrieve die waarden.</span><span class="sxs-lookup"><span data-stu-id="49c6f-133">You could use `RoleEnvironment.getConfigurationSettings` tooretrieve hello SendGrid username and password from your deployment's configuration settings, instead of using hello web form tooretrieve those values.</span></span> <span data-ttu-id="49c6f-134">Voor informatie over Hallo `RoleEnvironment` klasse, Zie [Using hello Azure Service Runtime-bibliotheek in JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) en hello Azure Service Runtime pakket documentatie op <http://dl.windowsazure.com/javadoc>.</span><span class="sxs-lookup"><span data-stu-id="49c6f-134">For information about hello `RoleEnvironment` class, see [Using hello Azure Service Runtime Library in JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) and hello Azure Service Runtime package documentation at <http://dl.windowsazure.com/javadoc>.</span></span>
* <span data-ttu-id="49c6f-135">Zie voor meer informatie over het gebruik van SendGrid in Java [hoe toosend e-SendGrid met Java met](store-sendgrid-java-how-to-send-email.md).</span><span class="sxs-lookup"><span data-stu-id="49c6f-135">For more information about using SendGrid in Java, see [How toosend email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

[emailform]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailform.jpg
[emailsent]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailSent.jpg
[emailresult]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaResult.jpg
