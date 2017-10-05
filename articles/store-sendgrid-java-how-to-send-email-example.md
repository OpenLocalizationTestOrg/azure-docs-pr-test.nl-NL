---
title: Store-sendgrid-Java-How-to-Send-email-example
description: Het verzenden van e-mail via SendGrid van Java in een Azure-implementatie
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
ms.openlocfilehash: d80d7d9c54bad12a4d26d8623eeccdf9bc2a743a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-send-email-using-sendgrid-from-java-in-an-azure-deployment"></a><span data-ttu-id="3c43f-103">Het verzenden van E-mail via SendGrid van Java in een Azure-implementatie</span><span class="sxs-lookup"><span data-stu-id="3c43f-103">How to Send Email Using SendGrid from Java in an Azure Deployment</span></span>
<span data-ttu-id="3c43f-104">Het volgende voorbeeld ziet u hoe u SendGrid kunt gebruiken om e-mails te verzenden van een webpagina die wordt gehost in Azure.</span><span class="sxs-lookup"><span data-stu-id="3c43f-104">The following example shows you how you can use SendGrid to send emails from a web page hosted in Azure.</span></span> <span data-ttu-id="3c43f-105">De resulterende toepassing wordt de gebruiker gevraagd om e-waarden, zoals wordt weergegeven in de volgende schermopname.</span><span class="sxs-lookup"><span data-stu-id="3c43f-105">The resulting application will prompt the user for email values, as shown in the following screen shot.</span></span>

![E-formulier][emailform]

<span data-ttu-id="3c43f-107">Het e-mailbericht ziet er ongeveer als de volgende schermopname.</span><span class="sxs-lookup"><span data-stu-id="3c43f-107">The resulting email will look similar to the following screen shot.</span></span>

![E-mailbericht][emailsent]

<span data-ttu-id="3c43f-109">U moet voor het gebruik van de code in dit onderwerp als volgt:</span><span class="sxs-lookup"><span data-stu-id="3c43f-109">You'll need to do the following to use the code in this topic:</span></span>

1. <span data-ttu-id="3c43f-110">De potten javax.mail bijvoorbeeld verkrijgen van <http://www.oracle.com/technetwork/java/javamail/index.html>.</span><span class="sxs-lookup"><span data-stu-id="3c43f-110">Obtain the javax.mail JARs, for example from <http://www.oracle.com/technetwork/java/javamail/index.html>.</span></span>
2. <span data-ttu-id="3c43f-111">De potten toevoegen aan uw Java build path.</span><span class="sxs-lookup"><span data-stu-id="3c43f-111">Add the JARs to your Java build path.</span></span>
3. <span data-ttu-id="3c43f-112">Als u Eclipse gebruikt voor het maken van deze Java-toepassing, kunt u de SendGrid-bibliotheken kunt opnemen in uw implementatie toepassingsbestand (WAR) met behulp van de functie van Eclipse implementatie-assembly.</span><span class="sxs-lookup"><span data-stu-id="3c43f-112">If you are using Eclipse to create this Java application, you can include the SendGrid libraries in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="3c43f-113">Als u Eclipse niet gebruikt voor deze Java-toepassing maakt, controleert u de bibliotheken worden opgenomen in dezelfde Azure rol heeft als uw Java-toepassing en toegevoegd aan het klassepad van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="3c43f-113">If you are not using Eclipse to create this Java application, ensure the libraries are included within the same Azure role as your Java application, and added to the class path of your application.</span></span>

<span data-ttu-id="3c43f-114">Ook moet u uw eigen SendGrid-gebruikersnaam en wachtwoord, kunnen de e-mail verzenden.</span><span class="sxs-lookup"><span data-stu-id="3c43f-114">You must also have your own SendGrid username and password, to be able to send the email.</span></span> <span data-ttu-id="3c43f-115">Als u wilt beginnen met de SendGrid, Zie [het verzenden van e-mail via SendGrid met Java](store-sendgrid-java-how-to-send-email.md).</span><span class="sxs-lookup"><span data-stu-id="3c43f-115">To get started with SendGrid, see [How to send email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

<span data-ttu-id="3c43f-116">Bovendien bekend bent met de informatie op [maken van een Hallo wereld-toepassing voor Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), of met andere technieken voor het hosten van Java-toepassingen in Azure als u geen van Eclipse gebruikmaakt wordt sterk aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="3c43f-116">Additionally, familiarity with the information at [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-sending-email"></a><span data-ttu-id="3c43f-117">Maken van een webformulier voor het verzenden van e-mail</span><span class="sxs-lookup"><span data-stu-id="3c43f-117">Create a web form for sending email</span></span>
<span data-ttu-id="3c43f-118">De volgende code toont het maken van een webformulier voor het ophalen van gebruikersgegevens voor het verzenden van e-mail.</span><span class="sxs-lookup"><span data-stu-id="3c43f-118">The following code shows how to create a web form to retrieve user data for sending email.</span></span> <span data-ttu-id="3c43f-119">Voor de doeleinden van deze inhoud, het JSP-bestand de naam **emailform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="3c43f-119">For purposes of this content, the JSP file is named **emailform.jsp**.</span></span>

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

## <a name="create-the-code-to-send-the-email"></a><span data-ttu-id="3c43f-120">De code voor het verzenden van het e-mailbericht maken</span><span class="sxs-lookup"><span data-stu-id="3c43f-120">Create the code to send the email</span></span>
<span data-ttu-id="3c43f-121">De volgende code, die wordt aangeroepen wanneer het formulier in emailform.jsp is voltooid, maakt het e-mailbericht en stuurt deze.</span><span class="sxs-lookup"><span data-stu-id="3c43f-121">The following code, which is called when you complete the form in emailform.jsp, creates the email message and sends it.</span></span> <span data-ttu-id="3c43f-122">Voor de doeleinden van deze inhoud, het JSP-bestand de naam **sendemail.jsp**.</span><span class="sxs-lookup"><span data-stu-id="3c43f-122">For purposes of this content, the JSP file is named **sendemail.jsp**.</span></span>

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

         // The SendGrid SMTP server.
         String SMTP_HOST_NAME = "smtp.sendgrid.net";

         Properties properties;

         properties = new Properties();

         // Specify SMTP values.
         properties.put("mail.transport.protocol", "smtp");
         properties.put("mail.smtp.host", SMTP_HOST_NAME);
         properties.put("mail.smtp.port", 587);
         properties.put("mail.smtp.auth", "true");

         // Display the email fields entered by the user. 
         out.println("Value entered for email Subject: " + request.getParameter("emailSubject") + "<br/>");        
         out.println("Value entered for email      To: " + request.getParameter("emailTo") + "<br/>");
         out.println("Value entered for email    From: " + request.getParameter("emailFrom") + "<br/>");
         out.println("Value entered for email    Text: " + "<br/>" + request.getParameter("emailText") + "<br/>");

         // Create the authenticator object.
         Authenticator authenticator = new SMTPAuthenticator();

         // Create the mail session object.
         Session mailSession;
         mailSession = Session.getDefaultInstance(properties, authenticator);

         // Display debug information to stdout, useful when using the
         // compute emulator during development.
         mailSession.setDebug(true);

         // Create the message and message part objects.
         MimeMessage message;
         Multipart multipart;
         MimeBodyPart messagePart; 

         message = new MimeMessage(mailSession);

         multipart = new MimeMultipart("alternative");
         messagePart = new MimeBodyPart();
         messagePart.setContent(request.getParameter("emailText"), "text/html");
         multipart.addBodyPart(messagePart);            

         // Specify the email To, From, Subject and Content. 
         message.setFrom(new InternetAddress(request.getParameter("emailFrom")));
         message.addRecipient(Message.RecipientType.TO, new InternetAddress(request.getParameter("emailTo")));
         message.setSubject(request.getParameter("emailSubject")); 
         message.setContent(multipart);

         // Uncomment the following if you want to add a footer.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"footer\": {\"settings\": {\"enable\":1,\"text/html\": \"<html>This is my <b>email footer</b>.</html>\"}}}}");

         // Uncomment the following if you want to enable click tracking.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"clicktrack\": {\"settings\": {\"enable\":1}}}}");

         Transport transport;
         transport = mailSession.getTransport();
         // Connect the transport object.
         transport.connect();
         // Send the message.
         transport.sendMessage(message,  message.getRecipients(Message.RecipientType.TO));
         // Close the connection.
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

<span data-ttu-id="3c43f-123">Naast het e-mailbericht verzendt, biedt emailform.jsp een resultaat voor de gebruiker. een voorbeeld is de volgende schermopname:</span><span class="sxs-lookup"><span data-stu-id="3c43f-123">In addition to sending the email, emailform.jsp provides a result for the user; an example is the following screen shot:</span></span>

![Resultaat van de e-mail verzenden][emailresult]

## <a name="next-steps"></a><span data-ttu-id="3c43f-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3c43f-125">Next steps</span></span>
<span data-ttu-id="3c43f-126">Uw toepassing naar de rekenemulator implementeren en uitvoeren vanuit een browser emailform.jsp, voer waarden in de vorm, klik op **dit e-mailbericht verzenden**, en resulteert in een sendemail.jsp weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3c43f-126">Deploy your application to the compute emulator and within a browser run emailform.jsp, enter values in the form, click **Send this email**, and then see results in sendemail.jsp.</span></span>

<span data-ttu-id="3c43f-127">Deze code is opgegeven zodat u het gebruik van SendGrid in Java in Azure.</span><span class="sxs-lookup"><span data-stu-id="3c43f-127">This code was provided to show you how to use SendGrid in Java on Azure.</span></span> <span data-ttu-id="3c43f-128">Voordat u Azure implementeert in productie, wilt u mogelijk meer foutafhandeling of andere functies toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3c43f-128">Before deploying to Azure in production, you may want to add more error handling or other features.</span></span> <span data-ttu-id="3c43f-129">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3c43f-129">For example:</span></span> 

* <span data-ttu-id="3c43f-130">U kunt Azure storage-blobs of SQL-Database voor het opslaan van e-mailadressen en e-mailberichten, in plaats van een webformulier.</span><span class="sxs-lookup"><span data-stu-id="3c43f-130">You could use Azure storage blobs or SQL Database to store email addresses and email messages, instead of using a web form.</span></span> <span data-ttu-id="3c43f-131">Zie voor meer informatie over het gebruik van Azure storage-blobs in Java [het gebruik van de Blob Storage-Service vanuit Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/).</span><span class="sxs-lookup"><span data-stu-id="3c43f-131">For information about using Azure storage blobs in Java, see [How to Use the Blob Storage Service from Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/).</span></span> <span data-ttu-id="3c43f-132">Zie voor meer informatie over het gebruik van SQL-Database in Java [met behulp van SQL-Database in Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).</span><span class="sxs-lookup"><span data-stu-id="3c43f-132">For information about using SQL Database in Java, see [Using SQL Database in Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).</span></span>
* <span data-ttu-id="3c43f-133">U kunt `RoleEnvironment.getConfigurationSettings` SendGrid-gebruikersnaam en wachtwoord van uw implementatie-configuratie-instellingen, in plaats van het webformulier voor het ophalen van deze waarden ophalen.</span><span class="sxs-lookup"><span data-stu-id="3c43f-133">You could use `RoleEnvironment.getConfigurationSettings` to retrieve the SendGrid username and password from your deployment's configuration settings, instead of using the web form to retrieve those values.</span></span> <span data-ttu-id="3c43f-134">Voor informatie over de `RoleEnvironment` klasse, Zie [met behulp van de Azure Service Runtime-bibliotheek in JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) en de documentatie van het pakket Azure Service Runtime op <http://dl.windowsazure.com/javadoc>.</span><span class="sxs-lookup"><span data-stu-id="3c43f-134">For information about the `RoleEnvironment` class, see [Using the Azure Service Runtime Library in JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) and the Azure Service Runtime package documentation at <http://dl.windowsazure.com/javadoc>.</span></span>
* <span data-ttu-id="3c43f-135">Zie voor meer informatie over het gebruik van SendGrid in Java [het verzenden van e-mail via SendGrid met Java](store-sendgrid-java-how-to-send-email.md).</span><span class="sxs-lookup"><span data-stu-id="3c43f-135">For more information about using SendGrid in Java, see [How to send email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

[emailform]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailform.jpg
[emailsent]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailSent.jpg
[emailresult]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaResult.jpg
