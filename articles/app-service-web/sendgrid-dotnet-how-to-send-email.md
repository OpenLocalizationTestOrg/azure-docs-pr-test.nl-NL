---
title: Het gebruik van de SendGrid-e-mailservice (.NET) | Microsoft Docs
description: Meer informatie over hoe verzenden van e-mailbericht met de SendGrid-e-mailservice op Azure. Codevoorbeelden geschreven in C# en gebruiken de .NET API.
services: app-service-web
documentationcenter: .net
author: thinkingserious
manager: erikre
editor: 
ms.assetid: 21bf4028-9046-476b-9799-3d3082a0f84c
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/15/2017
ms.author: dx@sendgrid.com
ms.openlocfilehash: b3a48b3c838763b022a18e55817ec7455fe94c85
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-send-email-using-sendgrid-with-azure"></a><span data-ttu-id="70696-104">Het verzenden van E-mail via SendGrid met Azure</span><span class="sxs-lookup"><span data-stu-id="70696-104">How to Send Email Using SendGrid with Azure</span></span>
## <a name="overview"></a><span data-ttu-id="70696-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="70696-105">Overview</span></span>
<span data-ttu-id="70696-106">Deze handleiding wordt uitgelegd hoe u algemene programmeertaken met de SendGrid-e-mailservice uitvoert op Azure.</span><span class="sxs-lookup"><span data-stu-id="70696-106">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="70696-107">De voorbeelden zijn geschreven in C\# en biedt ondersteuning voor .NET Standard 1.3.</span><span class="sxs-lookup"><span data-stu-id="70696-107">The samples are written in C\# and supports .NET Standard 1.3.</span></span> <span data-ttu-id="70696-108">De scenario's worden behandeld omvatten construeren van e-mailbericht, verzenden van e-mail, bijlagen, toevoegen en verschillende mail inschakelen en instellingen voor bijhouden.</span><span class="sxs-lookup"><span data-stu-id="70696-108">The scenarios covered include constructing email, sending email, adding attachments, and enabling various mail and tracking settings.</span></span> <span data-ttu-id="70696-109">Zie voor meer informatie over SendGrid en verzenden van e-mail, de [Vervolgstappen] [ Next steps] sectie.</span><span class="sxs-lookup"><span data-stu-id="70696-109">For more information on SendGrid and sending email, see the [Next steps][Next steps] section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="70696-110">Wat is de SendGrid-e-mailservice?</span><span class="sxs-lookup"><span data-stu-id="70696-110">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="70696-111">SendGrid is een [cloud-gebaseerde e-mailservice] die biedt betrouwbare [levering van de transactionele e], schaalbaarheid en realtime-analyses samen met de flexibele API's die aangepaste integratie te vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="70696-111">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="70696-112">Algemene gebruiksvoorbeelden voor SendGrid zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="70696-112">Common SendGrid use cases include:</span></span>

* <span data-ttu-id="70696-113">Automatisch verzenden van ontvangsten of aankoop bevestigingen aan klanten.</span><span class="sxs-lookup"><span data-stu-id="70696-113">Automatically sending receipts or purchase confirmations to customers.</span></span>
* <span data-ttu-id="70696-114">Beheer van distributiepunt bevat voor het verzenden van klanten maandelijkse Folders en aanbiedingen.</span><span class="sxs-lookup"><span data-stu-id="70696-114">Administering distribution lists for sending customers monthly fliers and promotions.</span></span>
* <span data-ttu-id="70696-115">Het verzamelen van real-time metrische gegevens voor items zoals geblokkeerde e-mailadres en de betrokkenheid van de klant.</span><span class="sxs-lookup"><span data-stu-id="70696-115">Collecting real-time metrics for things like blocked email and customer engagement.</span></span>
* <span data-ttu-id="70696-116">Het doorsturen van vragen van klanten.</span><span class="sxs-lookup"><span data-stu-id="70696-116">Forwarding customer inquiries.</span></span>
* <span data-ttu-id="70696-117">Verwerking van inkomende e-mailberichten.</span><span class="sxs-lookup"><span data-stu-id="70696-117">Processing incoming emails.</span></span>

<span data-ttu-id="70696-118">Voor meer informatie gaat u naar [https://sendgrid.com](https://sendgrid.com) of van SendGrid [C#-bibliotheek] [ sendgrid-csharp] GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="70696-118">For more information, visit [https://sendgrid.com](https://sendgrid.com) or SendGrid's [C# library][sendgrid-csharp] GitHub repo.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="70696-119">Een SendGrid-Account maken</span><span class="sxs-lookup"><span data-stu-id="70696-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-the-sendgrid-net-class-library"></a><span data-ttu-id="70696-120">Verwijst naar de bibliotheek SendGrid .NET-klasse</span><span class="sxs-lookup"><span data-stu-id="70696-120">Reference the SendGrid .NET Class Library</span></span>
<span data-ttu-id="70696-121">De [SendGrid NuGet-pakket](https://www.nuget.org/packages/Sendgrid) is de eenvoudigste manier om op te halen van de SendGrid-API en uw toepassing configureren met alle afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="70696-121">The [SendGrid NuGet package](https://www.nuget.org/packages/Sendgrid) is the easiest way to get the SendGrid API and to configure your application with all dependencies.</span></span> <span data-ttu-id="70696-122">NuGet is een Visual Studio-extensie opgenomen met Microsoft Visual Studio 2015 en hoger die eenvoudig kunt installeren en bijwerken van bibliotheken en hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="70696-122">NuGet is a Visual Studio extension included with Microsoft Visual Studio 2015 and above that makes it easy to install and update libraries and tools.</span></span>

> [!NOTE]
> <span data-ttu-id="70696-123">U kunt NuGet installeren als u een eerdere versie van Visual Studio dan Visual Studio 2015 uitvoert vanaf [http://www.nuget.org](http://www.nuget.org), en klik op de **NuGet installeren** knop.</span><span class="sxs-lookup"><span data-stu-id="70696-123">To install NuGet if you are running a version of Visual Studio earlier than Visual Studio 2015, visit [http://www.nuget.org](http://www.nuget.org), and click the **Install NuGet** button.</span></span>
>
>

<span data-ttu-id="70696-124">Als u wilt het SendGrid-NuGet-pakket installeren in uw toepassing, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="70696-124">To install the SendGrid NuGet package in your application, do the following:</span></span>

1. <span data-ttu-id="70696-125">Klik op **nieuw Project** en selecteer een **sjabloon**.</span><span class="sxs-lookup"><span data-stu-id="70696-125">Click on **New Project** and select a **Template**.</span></span>

   ![Een nieuw project maken][create-new-project]
2. <span data-ttu-id="70696-127">In **Solution Explorer**, met de rechtermuisknop op **verwijzingen**, klikt u vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="70696-127">In **Solution Explorer**, right-click **References**, then click **Manage NuGet Packages**.</span></span>

   ![SendGrid NuGet-pakket][SendGrid-NuGet-package]
3. <span data-ttu-id="70696-129">Zoeken naar **SendGrid** en selecteer de **SendGrid** item in de lijst met resultaten.</span><span class="sxs-lookup"><span data-stu-id="70696-129">Search for **SendGrid** and select the **SendGrid** item in the results list.</span></span>
4. <span data-ttu-id="70696-130">Selecteer de meest recente stabiele versie van het Nuget-pakket uit de vervolgkeuzelijst versie te kunnen werken met het objectmodel en API's die in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="70696-130">Select the latest stable version of the Nuget package from the version dropdown to be able to work with the object model and APIs demonstrated in this article.</span></span>

   ![SendGrid-pakket][sendgrid-package]
5. <span data-ttu-id="70696-132">Klik op **installeren** voor de installatie te voltooien en sluit vervolgens dit dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="70696-132">Click **Install** to complete the installation, and then close this dialog.</span></span>

<span data-ttu-id="70696-133">SendGrid van .NET-klassenbibliotheek heet **SendGrid**.</span><span class="sxs-lookup"><span data-stu-id="70696-133">SendGrid's .NET class library is called **SendGrid**.</span></span> <span data-ttu-id="70696-134">Bevat de volgende naamruimten:</span><span class="sxs-lookup"><span data-stu-id="70696-134">It contains the following namespaces:</span></span>

* <span data-ttu-id="70696-135">**SendGrid** voor communicatie met de SendGrid-API.</span><span class="sxs-lookup"><span data-stu-id="70696-135">**SendGrid** for communicating with SendGrid’s API.</span></span>
* <span data-ttu-id="70696-136">**SendGrid.Helpers.Mail** voor Help-methoden eenvoudig SendGridMessage om objecten te maken waarmee wordt aangegeven hoe om e-mails te verzenden.</span><span class="sxs-lookup"><span data-stu-id="70696-136">**SendGrid.Helpers.Mail** for helper methods to easily create SendGridMessage objects that specify how to send emails.</span></span>

<span data-ttu-id="70696-137">De volgende code naamruimtedeclaraties toevoegen aan het begin van een C#-bestand waarin u wilt programmatisch toegang biedt tot de SendGrid-e-mailservice.</span><span class="sxs-lookup"><span data-stu-id="70696-137">Add the following code namespace declarations to the top of any C# file in which you want to programmatically access the SendGrid email service.</span></span>

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a><span data-ttu-id="70696-138">Procedure: een e-mailbericht maken</span><span class="sxs-lookup"><span data-stu-id="70696-138">How to: Create an Email</span></span>
<span data-ttu-id="70696-139">Gebruik de **SendGridMessage** object te maken van een e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="70696-139">Use the **SendGridMessage** object to create an email message.</span></span> <span data-ttu-id="70696-140">Zodra het berichtobject is gemaakt, kunt u de eigenschappen en methoden, met inbegrip van de afzender voor e-mailadres, de e-mailontvanger en het onderwerp en hoofdtekst van het e-mailadres kunt instellen.</span><span class="sxs-lookup"><span data-stu-id="70696-140">Once the message object is created, you can set properties and methods, including the email sender, the email recipient, and the subject and body of the email.</span></span>

<span data-ttu-id="70696-141">Het volgende voorbeeld laat zien hoe een volledig ingevuld e-object te maken:</span><span class="sxs-lookup"><span data-stu-id="70696-141">The following example demonstrates how to create a fully populated email object:</span></span>

    var msg = new SendGridMessage();

    msg.SetFrom(new EmailAddress("dx@example.com", "SendGrid DX Team"));

    var recipients = new List<EmailAddress>
    {
        new EmailAddress("jeff@example.com", "Jeff Smith"),
        new EmailAddress("anna@example.com", "Anna Lidman"),
        new EmailAddress("peter@example.com", "Peter Saddow")
    };
    msg.AddTos(recipients);

    msg.SetSubject("Testing the SendGrid C# Library");

    msg.AddContent(MimeType.Text, "Hello World plain text!");
    msg.AddContent(MimeType.Html, "<p>Hello World!</p>");

<span data-ttu-id="70696-142">Voor meer informatie over alle eigenschappen en methoden die worden ondersteund door de **SendGrid** typt, Zie [sendgrid csharp] [ sendgrid-csharp] op GitHub.</span><span class="sxs-lookup"><span data-stu-id="70696-142">For more information on all properties and methods supported by the **SendGrid** type, see [sendgrid-csharp][sendgrid-csharp] on GitHub.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="70696-143">Procedure: een e-mailbericht verzenden</span><span class="sxs-lookup"><span data-stu-id="70696-143">How to: Send an Email</span></span>
<span data-ttu-id="70696-144">Na het maken van een e-mailbericht, kunt u met behulp van de SendGrid-API verzenden.</span><span class="sxs-lookup"><span data-stu-id="70696-144">After creating an email message, you can send it using SendGrid's API.</span></span> <span data-ttu-id="70696-145">U kunt ook [. De NET ingebouwd in de bibliotheek][NET-library].</span><span class="sxs-lookup"><span data-stu-id="70696-145">Alternatively, you may use [.NET's built in library][NET-library].</span></span>

<span data-ttu-id="70696-146">Verzenden van e-mail is vereist dat u uw SendGrid-API-sleutel opgeven.</span><span class="sxs-lookup"><span data-stu-id="70696-146">Sending email requires that you supply your SendGrid API Key.</span></span> <span data-ttu-id="70696-147">Als u meer informatie over het configureren van de API-sleutels nodig hebt, gaat u naar de API-sleutels van SendGrid [documentatie][documentation].</span><span class="sxs-lookup"><span data-stu-id="70696-147">If you need details about how to configure API Keys, please visit SendGrid's API Keys [documentation][documentation].</span></span>

<span data-ttu-id="70696-148">U kunt deze referenties kan opslaan via uw Azure-Portal door te klikken toepassingsinstellingen en de sleutel-waardeparen onder App-instellingen toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="70696-148">You may store these credentials via your Azure Portal by clicking Application settings and adding the key/value pairs under App settings.</span></span>

 ![Azure app-instellingen][azure_app_settings]

 <span data-ttu-id="70696-150">Vervolgens u mogelijk toegang tot deze als volgt:</span><span class="sxs-lookup"><span data-stu-id="70696-150">Then, you may access them as follows:</span></span>

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

<span data-ttu-id="70696-151">De volgende voorbeelden laten zien hoe een bericht verzenden met de Web-API.</span><span class="sxs-lookup"><span data-stu-id="70696-151">The following examples show how to send a message using the Web API.</span></span>

    using System;
    using System.Threading.Tasks;
    using SendGrid;
    using SendGrid.Helpers.Mail;

    namespace Example
    {
        internal class Example
        {
            private static void Main()
            {
                Execute().Wait();
            }

            static async Task Execute()
            {
                var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
                var client = new SendGridClient(apiKey);
                var msg = new SendGridMessage()
                {
                    From = new EmailAddress("test@example.com", "DX Team"),
                    Subject = "Hello World from the SendGrid CSharp SDK!",
                    PlainTextContent = "Hello, Email!",
                    HtmlContent = "<strong>Hello, Email!</strong>"
                };
                msg.AddTo(new EmailAddress("test@example.com", "Test User"));
                var response = await client.SendEmailAsync(msg);
            }
        }
    }

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="70696-152">Procedure: een bijlage toevoegen</span><span class="sxs-lookup"><span data-stu-id="70696-152">How to: Add an attachment</span></span>
<span data-ttu-id="70696-153">Bijlagen kunnen worden toegevoegd aan een bericht door het aanroepen van de **AddAttachment** methode en minimaal geven de bestandsnaam en Base64-gecodeerde inhoud wilt koppelen.</span><span class="sxs-lookup"><span data-stu-id="70696-153">Attachments can be added to a message by calling the **AddAttachment** method and minimally specifying the file name and Base64 encoded content you want to attach.</span></span> <span data-ttu-id="70696-154">U kunt meerdere bijlagen opnemen door het aanroepen van deze methode wanneer u voor elk bestand dat u wilt koppelen, of met behulp van de **AddAttachments** methode.</span><span class="sxs-lookup"><span data-stu-id="70696-154">You can include multiple attachments by calling this method once for each file you wish to attach or by using the **AddAttachments** method.</span></span> <span data-ttu-id="70696-155">Het volgende voorbeeld toont een bijlage aan een bericht toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="70696-155">The following example demonstrates adding an attachment to a message:</span></span>

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-to-enable-footers-tracking-and-analytics"></a><span data-ttu-id="70696-156">Procedure: e-mailinstellingen gebruiken om in te schakelen voetteksten, tracerings- en analyses</span><span class="sxs-lookup"><span data-stu-id="70696-156">How to: Use mail settings to enable footers, tracking, and analytics</span></span>
<span data-ttu-id="70696-157">SendGrid biedt extra e-mailfunctionaliteit door het gebruik van e-mailinstellingen en instellingen voor bijhouden.</span><span class="sxs-lookup"><span data-stu-id="70696-157">SendGrid provides additional email functionality through the use of mail settings and tracking settings.</span></span> <span data-ttu-id="70696-158">Deze instellingen kunnen worden toegevoegd aan een e-mailbericht om in te schakelen van specifieke functionaliteit, zoals Klik bijhouden, Google analytics en abonnement bijhouden.</span><span class="sxs-lookup"><span data-stu-id="70696-158">These settings can be added to an email message to enable specific functionality such as click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="70696-159">Zie voor een volledige lijst met apps de [instellingen documentatie][settings-documentation].</span><span class="sxs-lookup"><span data-stu-id="70696-159">For a full list of apps, see the [Settings Documentation][settings-documentation].</span></span>

<span data-ttu-id="70696-160">Apps kunnen worden toegepast op **SendGrid** e-mailberichten met behulp van methoden die worden geïmplementeerd als onderdeel van de **SendGridMessage** klasse.</span><span class="sxs-lookup"><span data-stu-id="70696-160">Apps can be applied to **SendGrid** email messages using methods implemented as part of the **SendGridMessage** class.</span></span> <span data-ttu-id="70696-161">De volgende voorbeelden tonen de voettekst en klik op filters bijhouden:</span><span class="sxs-lookup"><span data-stu-id="70696-161">The following examples demonstrate the footer and click tracking filters:</span></span>

<span data-ttu-id="70696-162">De volgende voorbeelden tonen de voettekst en klik op filters bijhouden:</span><span class="sxs-lookup"><span data-stu-id="70696-162">The following examples demonstrate the footer and click tracking filters:</span></span>

### <a name="footer-settings"></a><span data-ttu-id="70696-163">Instellingen voor voettekst</span><span class="sxs-lookup"><span data-stu-id="70696-163">Footer settings</span></span>
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a><span data-ttu-id="70696-164">Klik op bijhouden</span><span class="sxs-lookup"><span data-stu-id="70696-164">Click tracking</span></span>
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="70696-165">How to: extra SendGrid-Services gebruiken</span><span class="sxs-lookup"><span data-stu-id="70696-165">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="70696-166">SendGrid biedt verschillende API's en webhooks die u kunt gebruikmaken van aanvullende functionaliteit binnen uw Azure-toepassing.</span><span class="sxs-lookup"><span data-stu-id="70696-166">SendGrid offers several APIs and webhooks that you can use to leverage additional functionality within your Azure application.</span></span> <span data-ttu-id="70696-167">Zie voor meer informatie de [SendGrid API Reference][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="70696-167">For more details, see the [SendGrid API Reference][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="70696-168">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="70696-168">Next steps</span></span>
<span data-ttu-id="70696-169">Nu u de basisprincipes van de SendGrid-e-mailservice hebt geleerd, volgt u deze koppelingen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="70696-169">Now that you've learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="70696-170">SendGrid C\# -repo-bibliotheek: [sendgrid csharp][sendgrid-csharp]</span><span class="sxs-lookup"><span data-stu-id="70696-170">SendGrid C\# library repo: [sendgrid-csharp][sendgrid-csharp]</span></span>
* <span data-ttu-id="70696-171">SendGrid-API-documentatie: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="70696-171">SendGrid API documentation: <https://sendgrid.com/docs></span></span>

[Next steps]: #next-steps
[What is the SendGrid Email Service?]: #whatis
[Create a SendGrid Account]: #createaccount
[Reference the SendGrid .NET Class Library]: #reference
[How to: Create an Email]: #createemail
[How to: Send an Email]: #sendemail
[How to: Add an Attachment]: #addattachment
[How to: Use Filters to Enable Footers, Tracking, and Analytics]: #usefilters
[How to: Use Additional SendGrid Services]: #useservices

[create-new-project]: ./media/sendgrid-dotnet-how-to-send-email/new-project.png
[SendGrid-NuGet-package]: ./media/sendgrid-dotnet-how-to-send-email/reference.png
[sendgrid-package]: ./media/sendgrid-dotnet-how-to-send-email/sendgrid-package.png
[azure_app_settings]: ./media/sendgrid-dotnet-how-to-send-email/azure-app-settings.png
[sendgrid-csharp]: https://github.com/sendgrid/sendgrid-csharp
[SMTP vs. Web API]: https://sendgrid.com/docs/Integrate/index.html
[App Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/api_v3.html
[NET-library]: https://sendgrid.com/docs/Integrate/Code_Examples/v2_Mail/csharp.html#-Using-NETs-Builtin-SMTP-Library
[documentation]: https://sendgrid.com/docs/Classroom/Send/api_keys.html
[settings-documentation]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html

<span data-ttu-id="70696-172">[cloud-gebaseerde e-mailservice]: https://sendgrid.com/solutions</span><span class="sxs-lookup"><span data-stu-id="70696-172">[cloud-based email service]: https://sendgrid.com/solutions</span></span>
<span data-ttu-id="70696-173">[levering van de transactionele e]: https://sendgrid.com/use-cases/transactional-email</span><span class="sxs-lookup"><span data-stu-id="70696-173">[transactional email delivery]: https://sendgrid.com/use-cases/transactional-email</span></span>

