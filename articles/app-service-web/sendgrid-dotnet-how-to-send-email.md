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
# <a name="how-toosend-email-using-sendgrid-with-azure"></a>Hoe tooSend E-mail met behulp van SendGrid met Azure
## <a name="overview"></a>Overzicht
Deze handleiding wordt uitgelegd hoe e tooperform algemene programmeertaken met de SendGrid-service op Azure. Hallo-voorbeelden zijn geschreven in C\# en biedt ondersteuning voor .NET Standard 1.3. Hallo scenario's worden behandeld omvatten construeren van e-mailbericht, verzenden van e-mail, bijlagen, toevoegen en verschillende mail inschakelen en instellingen voor bijhouden. Zie voor meer informatie over SendGrid en verzenden van e-mail Hallo [Vervolgstappen] [ Next steps] sectie.

## <a name="what-is-hello-sendgrid-email-service"></a>Wat is Hallo SendGrid e-mailservice?
SendGrid is een [cloud-gebaseerde e-mailservice] die biedt betrouwbare [levering van de transactionele e], schaalbaarheid en realtime-analyses samen met de flexibele API's die aangepaste integratie te vereenvoudigen. Algemene gebruiksvoorbeelden voor SendGrid zijn onder andere:

* Automatisch verzenden van ontvangsten of aankoop bevestigingen toocustomers.
* Beheer van distributiepunt bevat voor het verzenden van klanten maandelijkse Folders en aanbiedingen.
* Het verzamelen van real-time metrische gegevens voor items zoals geblokkeerde e-mailadres en de betrokkenheid van de klant.
* Het doorsturen van vragen van klanten.
* Verwerking van inkomende e-mailberichten.

Voor meer informatie gaat u naar [https://sendgrid.com](https://sendgrid.com) of van SendGrid [C#-bibliotheek] [ sendgrid-csharp] GitHub-opslagplaats.

## <a name="create-a-sendgrid-account"></a>Een SendGrid-Account maken
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-net-class-library"></a>Verwijzing Hallo SendGrid .NET Class Library
Hallo [SendGrid NuGet-pakket](https://www.nuget.org/packages/Sendgrid) is Hallo gemakkelijkste manier tooget hello SendGrid-API en tooconfigure uw toepassing met alle afhankelijkheden. NuGet is een Visual Studio extensie opgenomen met Microsoft Visual Studio 2015 en hoger die het eenvoudig tooinstall en update-bibliotheken en hulpprogramma's maakt.

> [!NOTE]
> tooinstall NuGet als u een eerdere versie van Visual Studio dan Visual Studio 2015, gaat u naar [http://www.nuget.org](http://www.nuget.org), en klik op Hallo **NuGet installeren** knop.
>
>

tooinstall hello SendGrid NuGet-pakket in uw toepassing Hallo te volgen:

1. Klik op **nieuw Project** en selecteer een **sjabloon**.

   ![Een nieuw project maken][create-new-project]
2. In **Solution Explorer**, met de rechtermuisknop op **verwijzingen**, klikt u vervolgens op **NuGet-pakketten beheren**.

   ![SendGrid NuGet-pakket][SendGrid-NuGet-package]
3. Zoeken naar **SendGrid** en selecteer Hallo **SendGrid** item in de lijst met resultaten.
4. Selecteer Hallo nieuwste stabiele versie van Hallo Nuget-pakket in Hallo versie dropdown toobe kunnen toowork met Hallo-objectmodel en API's die in dit artikel.

   ![SendGrid-pakket][sendgrid-package]
5. Klik op **installeren** toocomplete Hallo installatie en sluit vervolgens dit dialoogvenster.

SendGrid van .NET-klassenbibliotheek heet **SendGrid**. Hallo naamruimten volgende bevat:

* **SendGrid** voor communicatie met de SendGrid-API.
* **SendGrid.Helpers.Mail** voor helper methoden tooeasily SendGridMessage-objecten die opgeeft hoe toosend e-mails maken.

Hallo na code naamruimte declaraties toohello boven van een C#-bestand waarin u wilt dat tooprogrammatically toegang Hallo SendGrid e-mailservice toevoegen.

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a>Procedure: een e-mailbericht maken
Gebruik Hallo **SendGridMessage** object toocreate een e-mailbericht. Als het Hallo-bericht-object is gemaakt, kunt u eigenschappen en methoden, met inbegrip van de afzender Hallo e-mailbericht, Hallo-e-mailontvanger en Hallo-onderwerp en hoofdtekst van e-mail Hallo instellen.

Hallo volgende voorbeeld laat zien hoe toocreate een volledig ingevuld e-object:

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

Voor meer informatie over alle eigenschappen en methoden die worden ondersteund door de **SendGrid** typt, Zie [sendgrid csharp] [ sendgrid-csharp] op GitHub.

## <a name="how-to-send-an-email"></a>Procedure: een e-mailbericht verzenden
Na het maken van een e-mailbericht, kunt u met behulp van de SendGrid-API verzenden. U kunt ook [. De NET ingebouwd in de bibliotheek][NET-library].

Verzenden van e-mail is vereist dat u uw SendGrid-API-sleutel opgeven. Als u meer informatie over hoe moet tooconfigure API-sleutels, gaat u naar de API-sleutels van SendGrid [documentatie][documentation].

U kunt deze referenties via uw Azure-Portal door te klikken op toepassings- en toe te voegen Hallo sleutel/waarde-paren onder App-instellingen opslaan.

 ![Azure app-instellingen][azure_app_settings]

 Vervolgens u mogelijk toegang tot deze als volgt:

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

Hallo volgen voorbeelden laten zien hoe een bericht met toosend Hallo Web-API.

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

## <a name="how-to-add-an-attachment"></a>Procedure: een bijlage toevoegen
Bijlagen kunnen tooa bericht worden toegevoegd door de aanroepende Hallo **AddAttachment** methode en minimaal geven Hallo-bestandsnaam en Base64-gecodeerde inhoud wilt tooattach. U kunt meerdere bijlagen opnemen door het aanroepen van deze methode wanneer u voor elk bestand dat u wenst dat tooattach of met behulp van Hallo **AddAttachments** methode. Hallo volgende voorbeeld ziet u een bijlage tooa bericht toe te voegen:

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-tooenable-footers-tracking-and-analytics"></a>Procedure: e-mail instellingen tooenable voetteksten, bijhouden en analytics gebruiken
SendGrid biedt extra e-mailfunctionaliteit via Hallo gebruik van e-mailinstellingen en instellingen voor bijhouden. Deze instellingen kunnen worden toegevoegd als tooan e bericht tooenable specifieke functionaliteit zoals Klik bijhouden, Google analytics en abonnement bijhouden. Zie voor een volledige lijst met apps Hallo [instellingen documentatie][settings-documentation].

Apps te kunnen worden toegepast**SendGrid** e-mailberichten met behulp van methoden die worden geïmplementeerd als onderdeel van Hallo **SendGridMessage** klasse. Hallo volgende voorbeelden laten zien Hallo voettekst en klik op filters bijhouden:

Hallo volgende voorbeelden laten zien Hallo voettekst en klik op filters bijhouden:

### <a name="footer-settings"></a>Instellingen voor voettekst
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a>Klik op bijhouden
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a>How to: extra SendGrid-Services gebruiken
SendGrid biedt verschillende API's en webhooks dat u aanvullende functionaliteit tooleverage binnen uw Azure-toepassing kunt gebruiken. Zie voor meer informatie, Hallo [SendGrid API Reference][SendGrid API documentation].

## <a name="next-steps"></a>Volgende stappen
Nu u basisprincipes Hallo Hallo SendGrid-e-mailservice hebt geleerd, volgt u deze koppelingen toolearn meer.

* SendGrid C\# -repo-bibliotheek: [sendgrid csharp][sendgrid-csharp]
* SendGrid-API-documentatie: <https://sendgrid.com/docs>

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

