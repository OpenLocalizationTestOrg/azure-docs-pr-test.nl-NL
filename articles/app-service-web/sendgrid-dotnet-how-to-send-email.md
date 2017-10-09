---
title: aaaHow toouse hello SendGrid e-mailservice (.NET) | Microsoft Docs
description: Meer informatie over hoe e-mailbericht met de SendGrid-e-mailservice Hallo verzenden in Azure. Codevoorbeelden geschreven in C# en gebruik Hallo .NET API.
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
ms.openlocfilehash: b3d77bb67898b991c7293e6b9086b263f6bcb755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-with-azure"></a><span data-ttu-id="830d1-104">Hoe tooSend E-mail met behulp van SendGrid met Azure</span><span class="sxs-lookup"><span data-stu-id="830d1-104">How tooSend Email Using SendGrid with Azure</span></span>
## <a name="overview"></a><span data-ttu-id="830d1-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="830d1-105">Overview</span></span>
<span data-ttu-id="830d1-106">Deze handleiding wordt uitgelegd hoe e tooperform algemene programmeertaken met de SendGrid-service op Azure.</span><span class="sxs-lookup"><span data-stu-id="830d1-106">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="830d1-107">Hallo-voorbeelden zijn geschreven in C\# en biedt ondersteuning voor .NET Standard 1.3.</span><span class="sxs-lookup"><span data-stu-id="830d1-107">hello samples are written in C\# and supports .NET Standard 1.3.</span></span> <span data-ttu-id="830d1-108">Hallo scenario's worden behandeld omvatten construeren van e-mailbericht, verzenden van e-mail, bijlagen, toevoegen en verschillende mail inschakelen en instellingen voor bijhouden.</span><span class="sxs-lookup"><span data-stu-id="830d1-108">hello scenarios covered include constructing email, sending email, adding attachments, and enabling various mail and tracking settings.</span></span> <span data-ttu-id="830d1-109">Zie voor meer informatie over SendGrid en verzenden van e-mail Hallo [Vervolgstappen] [ Next steps] sectie.</span><span class="sxs-lookup"><span data-stu-id="830d1-109">For more information on SendGrid and sending email, see hello [Next steps][Next steps] section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="830d1-110">Wat is Hallo SendGrid e-mailservice?</span><span class="sxs-lookup"><span data-stu-id="830d1-110">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="830d1-111">SendGrid is een [cloud-gebaseerde e-mailservice] die biedt betrouwbare [levering van de transactionele e], schaalbaarheid en realtime-analyses samen met de flexibele API's die aangepaste integratie te vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="830d1-111">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="830d1-112">Algemene gebruiksvoorbeelden voor SendGrid zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="830d1-112">Common SendGrid use cases include:</span></span>

* <span data-ttu-id="830d1-113">Automatisch verzenden van ontvangsten of aankoop bevestigingen toocustomers.</span><span class="sxs-lookup"><span data-stu-id="830d1-113">Automatically sending receipts or purchase confirmations toocustomers.</span></span>
* <span data-ttu-id="830d1-114">Beheer van distributiepunt bevat voor het verzenden van klanten maandelijkse Folders en aanbiedingen.</span><span class="sxs-lookup"><span data-stu-id="830d1-114">Administering distribution lists for sending customers monthly fliers and promotions.</span></span>
* <span data-ttu-id="830d1-115">Het verzamelen van real-time metrische gegevens voor items zoals geblokkeerde e-mailadres en de betrokkenheid van de klant.</span><span class="sxs-lookup"><span data-stu-id="830d1-115">Collecting real-time metrics for things like blocked email and customer engagement.</span></span>
* <span data-ttu-id="830d1-116">Het doorsturen van vragen van klanten.</span><span class="sxs-lookup"><span data-stu-id="830d1-116">Forwarding customer inquiries.</span></span>
* <span data-ttu-id="830d1-117">Verwerking van inkomende e-mailberichten.</span><span class="sxs-lookup"><span data-stu-id="830d1-117">Processing incoming emails.</span></span>

<span data-ttu-id="830d1-118">Voor meer informatie gaat u naar [https://sendgrid.com](https://sendgrid.com) of van SendGrid [C#-bibliotheek] [ sendgrid-csharp] GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="830d1-118">For more information, visit [https://sendgrid.com](https://sendgrid.com) or SendGrid's [C# library][sendgrid-csharp] GitHub repo.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="830d1-119">Een SendGrid-Account maken</span><span class="sxs-lookup"><span data-stu-id="830d1-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-net-class-library"></a><span data-ttu-id="830d1-120">Verwijzing Hallo SendGrid .NET Class Library</span><span class="sxs-lookup"><span data-stu-id="830d1-120">Reference hello SendGrid .NET Class Library</span></span>
<span data-ttu-id="830d1-121">Hallo [SendGrid NuGet-pakket](https://www.nuget.org/packages/Sendgrid) is Hallo gemakkelijkste manier tooget hello SendGrid-API en tooconfigure uw toepassing met alle afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="830d1-121">hello [SendGrid NuGet package](https://www.nuget.org/packages/Sendgrid) is hello easiest way tooget hello SendGrid API and tooconfigure your application with all dependencies.</span></span> <span data-ttu-id="830d1-122">NuGet is een Visual Studio extensie opgenomen met Microsoft Visual Studio 2015 en hoger die het eenvoudig tooinstall en update-bibliotheken en hulpprogramma's maakt.</span><span class="sxs-lookup"><span data-stu-id="830d1-122">NuGet is a Visual Studio extension included with Microsoft Visual Studio 2015 and above that makes it easy tooinstall and update libraries and tools.</span></span>

> [!NOTE]
> <span data-ttu-id="830d1-123">tooinstall NuGet als u een eerdere versie van Visual Studio dan Visual Studio 2015, gaat u naar [http://www.nuget.org](http://www.nuget.org), en klik op Hallo **NuGet installeren** knop.</span><span class="sxs-lookup"><span data-stu-id="830d1-123">tooinstall NuGet if you are running a version of Visual Studio earlier than Visual Studio 2015, visit [http://www.nuget.org](http://www.nuget.org), and click hello **Install NuGet** button.</span></span>
>
>

<span data-ttu-id="830d1-124">tooinstall hello SendGrid NuGet-pakket in uw toepassing Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="830d1-124">tooinstall hello SendGrid NuGet package in your application, do hello following:</span></span>

1. <span data-ttu-id="830d1-125">Klik op **nieuw Project** en selecteer een **sjabloon**.</span><span class="sxs-lookup"><span data-stu-id="830d1-125">Click on **New Project** and select a **Template**.</span></span>

   ![Een nieuw project maken][create-new-project]
2. <span data-ttu-id="830d1-127">In **Solution Explorer**, met de rechtermuisknop op **verwijzingen**, klikt u vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="830d1-127">In **Solution Explorer**, right-click **References**, then click **Manage NuGet Packages**.</span></span>

   ![SendGrid NuGet-pakket][SendGrid-NuGet-package]
3. <span data-ttu-id="830d1-129">Zoeken naar **SendGrid** en selecteer Hallo **SendGrid** item in de lijst met resultaten.</span><span class="sxs-lookup"><span data-stu-id="830d1-129">Search for **SendGrid** and select hello **SendGrid** item in the results list.</span></span>
4. <span data-ttu-id="830d1-130">Selecteer Hallo nieuwste stabiele versie van Hallo Nuget-pakket in Hallo versie dropdown toobe kunnen toowork met Hallo-objectmodel en API's die in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="830d1-130">Select hello latest stable version of hello Nuget package from hello version dropdown toobe able toowork with hello object model and APIs demonstrated in this article.</span></span>

   ![SendGrid-pakket][sendgrid-package]
5. <span data-ttu-id="830d1-132">Klik op **installeren** toocomplete Hallo installatie en sluit vervolgens dit dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="830d1-132">Click **Install** toocomplete hello installation, and then close this dialog.</span></span>

<span data-ttu-id="830d1-133">SendGrid van .NET-klassenbibliotheek heet **SendGrid**.</span><span class="sxs-lookup"><span data-stu-id="830d1-133">SendGrid's .NET class library is called **SendGrid**.</span></span> <span data-ttu-id="830d1-134">Hallo naamruimten volgende bevat:</span><span class="sxs-lookup"><span data-stu-id="830d1-134">It contains hello following namespaces:</span></span>

* <span data-ttu-id="830d1-135">**SendGrid** voor communicatie met de SendGrid-API.</span><span class="sxs-lookup"><span data-stu-id="830d1-135">**SendGrid** for communicating with SendGrid’s API.</span></span>
* <span data-ttu-id="830d1-136">**SendGrid.Helpers.Mail** voor helper methoden tooeasily SendGridMessage-objecten die opgeeft hoe toosend e-mails maken.</span><span class="sxs-lookup"><span data-stu-id="830d1-136">**SendGrid.Helpers.Mail** for helper methods tooeasily create SendGridMessage objects that specify how toosend emails.</span></span>

<span data-ttu-id="830d1-137">Hallo na code naamruimte declaraties toohello boven van een C#-bestand waarin u wilt dat tooprogrammatically toegang Hallo SendGrid e-mailservice toevoegen.</span><span class="sxs-lookup"><span data-stu-id="830d1-137">Add hello following code namespace declarations toohello top of any C# file in which you want tooprogrammatically access hello SendGrid email service.</span></span>

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a><span data-ttu-id="830d1-138">Procedure: een e-mailbericht maken</span><span class="sxs-lookup"><span data-stu-id="830d1-138">How to: Create an Email</span></span>
<span data-ttu-id="830d1-139">Gebruik Hallo **SendGridMessage** object toocreate een e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="830d1-139">Use hello **SendGridMessage** object toocreate an email message.</span></span> <span data-ttu-id="830d1-140">Als het Hallo-bericht-object is gemaakt, kunt u eigenschappen en methoden, met inbegrip van de afzender Hallo e-mailbericht, Hallo-e-mailontvanger en Hallo-onderwerp en hoofdtekst van e-mail Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="830d1-140">Once hello message object is created, you can set properties and methods, including hello email sender, hello email recipient, and hello subject and body of hello email.</span></span>

<span data-ttu-id="830d1-141">Hallo volgende voorbeeld laat zien hoe toocreate een volledig ingevuld e-object:</span><span class="sxs-lookup"><span data-stu-id="830d1-141">hello following example demonstrates how toocreate a fully populated email object:</span></span>

    var msg = new SendGridMessage();

    msg.SetFrom(new EmailAddress("dx@example.com", "SendGrid DX Team"));

    var recipients = new List<EmailAddress>
    {
        new EmailAddress("jeff@example.com", "Jeff Smith"),
        new EmailAddress("anna@example.com", "Anna Lidman"),
        new EmailAddress("peter@example.com", "Peter Saddow")
    };
    msg.AddTos(recipients);

    msg.SetSubject("Testing hello SendGrid C# Library");

    msg.AddContent(MimeType.Text, "Hello World plain text!");
    msg.AddContent(MimeType.Html, "<p>Hello World!</p>");

<span data-ttu-id="830d1-142">Voor meer informatie over alle eigenschappen en methoden die worden ondersteund door de **SendGrid** typt, Zie [sendgrid csharp] [ sendgrid-csharp] op GitHub.</span><span class="sxs-lookup"><span data-stu-id="830d1-142">For more information on all properties and methods supported by the **SendGrid** type, see [sendgrid-csharp][sendgrid-csharp] on GitHub.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="830d1-143">Procedure: een e-mailbericht verzenden</span><span class="sxs-lookup"><span data-stu-id="830d1-143">How to: Send an Email</span></span>
<span data-ttu-id="830d1-144">Na het maken van een e-mailbericht, kunt u met behulp van de SendGrid-API verzenden.</span><span class="sxs-lookup"><span data-stu-id="830d1-144">After creating an email message, you can send it using SendGrid's API.</span></span> <span data-ttu-id="830d1-145">U kunt ook [. De NET ingebouwd in de bibliotheek][NET-library].</span><span class="sxs-lookup"><span data-stu-id="830d1-145">Alternatively, you may use [.NET's built in library][NET-library].</span></span>

<span data-ttu-id="830d1-146">Verzenden van e-mail is vereist dat u uw SendGrid-API-sleutel opgeven.</span><span class="sxs-lookup"><span data-stu-id="830d1-146">Sending email requires that you supply your SendGrid API Key.</span></span> <span data-ttu-id="830d1-147">Als u meer informatie over hoe moet tooconfigure API-sleutels, gaat u naar de API-sleutels van SendGrid [documentatie][documentation].</span><span class="sxs-lookup"><span data-stu-id="830d1-147">If you need details about how tooconfigure API Keys, please visit SendGrid's API Keys [documentation][documentation].</span></span>

<span data-ttu-id="830d1-148">U kunt deze referenties via uw Azure-Portal door te klikken op toepassings- en toe te voegen Hallo sleutel/waarde-paren onder App-instellingen opslaan.</span><span class="sxs-lookup"><span data-stu-id="830d1-148">You may store these credentials via your Azure Portal by clicking Application settings and adding hello key/value pairs under App settings.</span></span>

 ![Azure app-instellingen][azure_app_settings]

 <span data-ttu-id="830d1-150">Vervolgens u mogelijk toegang tot deze als volgt:</span><span class="sxs-lookup"><span data-stu-id="830d1-150">Then, you may access them as follows:</span></span>

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

<span data-ttu-id="830d1-151">Hallo volgen voorbeelden laten zien hoe een bericht met toosend Hallo Web-API.</span><span class="sxs-lookup"><span data-stu-id="830d1-151">hello following examples show how toosend a message using hello Web API.</span></span>

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
                    Subject = "Hello World from hello SendGrid CSharp SDK!",
                    PlainTextContent = "Hello, Email!",
                    HtmlContent = "<strong>Hello, Email!</strong>"
                };
                msg.AddTo(new EmailAddress("test@example.com", "Test User"));
                var response = await client.SendEmailAsync(msg);
            }
        }
    }

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="830d1-152">Procedure: een bijlage toevoegen</span><span class="sxs-lookup"><span data-stu-id="830d1-152">How to: Add an attachment</span></span>
<span data-ttu-id="830d1-153">Bijlagen kunnen tooa bericht worden toegevoegd door de aanroepende Hallo **AddAttachment** methode en minimaal geven Hallo-bestandsnaam en Base64-gecodeerde inhoud wilt tooattach.</span><span class="sxs-lookup"><span data-stu-id="830d1-153">Attachments can be added tooa message by calling hello **AddAttachment** method and minimally specifying hello file name and Base64 encoded content you want tooattach.</span></span> <span data-ttu-id="830d1-154">U kunt meerdere bijlagen opnemen door het aanroepen van deze methode wanneer u voor elk bestand dat u wenst dat tooattach of met behulp van Hallo **AddAttachments** methode.</span><span class="sxs-lookup"><span data-stu-id="830d1-154">You can include multiple attachments by calling this method once for each file you wish tooattach or by using hello **AddAttachments** method.</span></span> <span data-ttu-id="830d1-155">Hallo volgende voorbeeld ziet u een bijlage tooa bericht toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="830d1-155">hello following example demonstrates adding an attachment tooa message:</span></span>

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="830d1-156">Procedure: e-mail instellingen tooenable voetteksten, bijhouden en analytics gebruiken</span><span class="sxs-lookup"><span data-stu-id="830d1-156">How to: Use mail settings tooenable footers, tracking, and analytics</span></span>
<span data-ttu-id="830d1-157">SendGrid biedt extra e-mailfunctionaliteit via Hallo gebruik van e-mailinstellingen en instellingen voor bijhouden.</span><span class="sxs-lookup"><span data-stu-id="830d1-157">SendGrid provides additional email functionality through hello use of mail settings and tracking settings.</span></span> <span data-ttu-id="830d1-158">Deze instellingen kunnen worden toegevoegd als tooan e bericht tooenable specifieke functionaliteit zoals Klik bijhouden, Google analytics en abonnement bijhouden.</span><span class="sxs-lookup"><span data-stu-id="830d1-158">These settings can be added tooan email message tooenable specific functionality such as click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="830d1-159">Zie voor een volledige lijst met apps Hallo [instellingen documentatie][settings-documentation].</span><span class="sxs-lookup"><span data-stu-id="830d1-159">For a full list of apps, see hello [Settings Documentation][settings-documentation].</span></span>

<span data-ttu-id="830d1-160">Apps te kunnen worden toegepast**SendGrid** e-mailberichten met behulp van methoden die worden geïmplementeerd als onderdeel van Hallo **SendGridMessage** klasse.</span><span class="sxs-lookup"><span data-stu-id="830d1-160">Apps can be applied too**SendGrid** email messages using methods implemented as part of hello **SendGridMessage** class.</span></span> <span data-ttu-id="830d1-161">Hallo volgende voorbeelden laten zien Hallo voettekst en klik op filters bijhouden:</span><span class="sxs-lookup"><span data-stu-id="830d1-161">hello following examples demonstrate hello footer and click tracking filters:</span></span>

<span data-ttu-id="830d1-162">Hallo volgende voorbeelden laten zien Hallo voettekst en klik op filters bijhouden:</span><span class="sxs-lookup"><span data-stu-id="830d1-162">hello following examples demonstrate hello footer and click tracking filters:</span></span>

### <a name="footer-settings"></a><span data-ttu-id="830d1-163">Instellingen voor voettekst</span><span class="sxs-lookup"><span data-stu-id="830d1-163">Footer settings</span></span>
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a><span data-ttu-id="830d1-164">Klik op bijhouden</span><span class="sxs-lookup"><span data-stu-id="830d1-164">Click tracking</span></span>
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="830d1-165">How to: extra SendGrid-Services gebruiken</span><span class="sxs-lookup"><span data-stu-id="830d1-165">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="830d1-166">SendGrid biedt verschillende API's en webhooks dat u aanvullende functionaliteit tooleverage binnen uw Azure-toepassing kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="830d1-166">SendGrid offers several APIs and webhooks that you can use tooleverage additional functionality within your Azure application.</span></span> <span data-ttu-id="830d1-167">Zie voor meer informatie, Hallo [SendGrid API Reference][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="830d1-167">For more details, see hello [SendGrid API Reference][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="830d1-168">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="830d1-168">Next steps</span></span>
<span data-ttu-id="830d1-169">Nu u basisprincipes Hallo Hallo SendGrid-e-mailservice hebt geleerd, volgt u deze koppelingen toolearn meer.</span><span class="sxs-lookup"><span data-stu-id="830d1-169">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="830d1-170">SendGrid C\# -repo-bibliotheek: [sendgrid csharp][sendgrid-csharp]</span><span class="sxs-lookup"><span data-stu-id="830d1-170">SendGrid C\# library repo: [sendgrid-csharp][sendgrid-csharp]</span></span>
* <span data-ttu-id="830d1-171">SendGrid-API-documentatie: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="830d1-171">SendGrid API documentation: <https://sendgrid.com/docs></span></span>

[Next steps]: #next-steps
[What is hello SendGrid Email Service?]: #whatis
[Create a SendGrid Account]: #createaccount
[Reference hello SendGrid .NET Class Library]: #reference
[How to: Create an Email]: #createemail
[How to: Send an Email]: #sendemail
[How to: Add an Attachment]: #addattachment
[How to: Use Filters tooEnable Footers, Tracking, and Analytics]: #usefilters
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

[cloud-gebaseerde e-mailservice]: https://sendgrid.com/solutions
[levering van de transactionele e]: https://sendgrid.com/use-cases/transactional-email

