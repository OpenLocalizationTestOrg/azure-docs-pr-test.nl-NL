---
title: aaaHow toouse hello SendGrid e-mailservice (Node.js) | Microsoft Docs
description: Meer informatie over hoe e-mailbericht met de SendGrid-e-mailservice Hallo verzenden in Azure. Codevoorbeelden geschreven met behulp van Hallo Node.js-API.
services: 
documentationcenter: nodejs
author: erikre
manager: wpickett
editor: 
ms.assetid: cac444b4-26b0-45ea-9c3d-eca28d57dacb
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 01/05/2016
ms.author: erikre
ms.openlocfilehash: fd617b6aaa656e7b5dd51c51ebb0db1e848450f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-nodejs"></a><span data-ttu-id="8f65f-104">Hoe tooSend e SendGrid met behulp van Node.js</span><span class="sxs-lookup"><span data-stu-id="8f65f-104">How tooSend Email Using SendGrid from Node.js</span></span>
<span data-ttu-id="8f65f-105">Deze handleiding wordt uitgelegd hoe e tooperform algemene programmeertaken met de SendGrid-service op Azure.</span><span class="sxs-lookup"><span data-stu-id="8f65f-105">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="8f65f-106">Hallo-voorbeelden zijn geschreven met behulp van Hallo Node.js-API.</span><span class="sxs-lookup"><span data-stu-id="8f65f-106">hello samples are written using hello Node.js API.</span></span> <span data-ttu-id="8f65f-107">Hallo scenario's worden behandeld: **construeren e**, **verzenden van e-mail**, **bijlagen toevoegen**, **met filters**, en **eigenschappen bijwerken**.</span><span class="sxs-lookup"><span data-stu-id="8f65f-107">hello scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="8f65f-108">Zie voor meer informatie over SendGrid en verzenden van e-mail Hallo [Vervolgstappen](#next-steps) sectie.</span><span class="sxs-lookup"><span data-stu-id="8f65f-108">For more information on SendGrid and sending email, see hello [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="8f65f-109">Wat is Hallo SendGrid e-mailservice?</span><span class="sxs-lookup"><span data-stu-id="8f65f-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="8f65f-110">SendGrid is een [cloud-gebaseerde e-mailservice] die biedt betrouwbare [levering van de transactionele e], schaalbaarheid en realtime-analyses samen met de flexibele API's die aangepaste integratie te vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="8f65f-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="8f65f-111">Veelvoorkomende gebruiksscenario's van SendGrid zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="8f65f-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="8f65f-112">Ontvangstbevestigingen toocustomers automatisch verzenden</span><span class="sxs-lookup"><span data-stu-id="8f65f-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="8f65f-113">Beheer van distributiepunt bevat voor het verzenden van klanten maandelijkse e-Folders en speciale aanbiedingen</span><span class="sxs-lookup"><span data-stu-id="8f65f-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="8f65f-114">Realtime metrische gegevens voor items zoals geblokkeerd e- en reactietijd van de klant verzamelen</span><span class="sxs-lookup"><span data-stu-id="8f65f-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="8f65f-115">Genereren van rapporten toohelp trends identificeren</span><span class="sxs-lookup"><span data-stu-id="8f65f-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="8f65f-116">Doorsturen van vragen van klanten</span><span class="sxs-lookup"><span data-stu-id="8f65f-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="8f65f-117">E-mailmeldingen van uw toepassing</span><span class="sxs-lookup"><span data-stu-id="8f65f-117">Email notifications from your application</span></span>

<span data-ttu-id="8f65f-118">Zie voor meer informatie [https://sendgrid.com](https://sendgrid.com).</span><span class="sxs-lookup"><span data-stu-id="8f65f-118">For more information, see [https://sendgrid.com](https://sendgrid.com).</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="8f65f-119">Een SendGrid-Account maken</span><span class="sxs-lookup"><span data-stu-id="8f65f-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-nodejs-module"></a><span data-ttu-id="8f65f-120">Verwijzing Hallo SendGrid Node.js-Module</span><span class="sxs-lookup"><span data-stu-id="8f65f-120">Reference hello SendGrid Node.js Module</span></span>
<span data-ttu-id="8f65f-121">Hallo SendGrid-module voor Node.js kan worden geïnstalleerd via Pakketbeheer Hallo-knooppunt (npm) met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8f65f-121">hello SendGrid module for Node.js can be installed through hello node package manager (npm) by using hello following command:</span></span>

    npm install sendgrid

<span data-ttu-id="8f65f-122">Na de installatie, kunt u met behulp van de volgende code Hallo Hallo module in uw toepassing vereisen:</span><span class="sxs-lookup"><span data-stu-id="8f65f-122">After installation, you can require hello module in your application by using hello following code:</span></span>

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

<span data-ttu-id="8f65f-123">Hallo SendGrid module exporteert Hallo **SendGrid** en **e** functies.</span><span class="sxs-lookup"><span data-stu-id="8f65f-123">hello SendGrid module exports hello **SendGrid** and **Email** functions.</span></span>
<span data-ttu-id="8f65f-124">**SendGrid** is verantwoordelijk voor het verzenden van e-mail via Web-API, terwijl **e** ingekapseld een e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="8f65f-124">**SendGrid** is responsible for sending email through Web API, while **Email** encapsulates an email message.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="8f65f-125">Procedure: een e-mailbericht maken</span><span class="sxs-lookup"><span data-stu-id="8f65f-125">How to: Create an Email</span></span>
<span data-ttu-id="8f65f-126">Maken van een e-mailbericht met Hallo SendGrid-module, moet eerst een e-mailbericht met de functie e Hallo en vervolgens te verzenden met de SendGrid-functie Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="8f65f-126">Creating an email message using hello SendGrid module involves first creating an email message using hello Email function, and then sending it using hello SendGrid function.</span></span> <span data-ttu-id="8f65f-127">Hallo Hieronder volgt een voorbeeld van het maken van een nieuw bericht met de functie e Hallo:</span><span class="sxs-lookup"><span data-stu-id="8f65f-127">hello following is an example of creating a new message using hello Email function:</span></span>

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

<span data-ttu-id="8f65f-128">U kunt ook een HTML-bericht opgeven voor clients die deze ondersteunen door Hallo HTML-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="8f65f-128">You can also specify an HTML message for clients that support it by setting hello html property.</span></span> <span data-ttu-id="8f65f-129">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8f65f-129">For example:</span></span>

    html: This is a sample <b>HTML<b> email message.

<span data-ttu-id="8f65f-130">Instellen van de eigenschappen van beide Hallo tekst en html biedt correcte terugvallen op tekstinhoud voor clients die HTML-berichten niet ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="8f65f-130">Setting both hello text and html properties provides graceful fallback to text content for clients that cannot support HTML messages.</span></span>

<span data-ttu-id="8f65f-131">Zie voor meer informatie over alle eigenschappen die worden ondersteund door Hallo e functie [sendgrid nodejs][sendgrid-nodejs].</span><span class="sxs-lookup"><span data-stu-id="8f65f-131">For more information on all properties supported by hello Email function, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="8f65f-132">Procedure: een e-mailbericht verzenden</span><span class="sxs-lookup"><span data-stu-id="8f65f-132">How to: Send an Email</span></span>
<span data-ttu-id="8f65f-133">Na het maken van een e-mailbericht met Hallo e-functie kunt u met behulp van Web-API is geleverd door SendGrid Hallo verzenden.</span><span class="sxs-lookup"><span data-stu-id="8f65f-133">After creating an email message using hello Email function, you can send it using hello Web API provided by SendGrid.</span></span> 

### <a name="web-api"></a><span data-ttu-id="8f65f-134">Web-API</span><span class="sxs-lookup"><span data-stu-id="8f65f-134">Web API</span></span>
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> <span data-ttu-id="8f65f-135">Terwijl Hallo bovenstaande voorbeelden doorgeven in een e-object en de callback-functie wilt weergeven, kunt u kunt ook rechtstreeks Hallo verzenden functie aanroepen door direct e-eigenschappen op te geven.</span><span class="sxs-lookup"><span data-stu-id="8f65f-135">While hello above examples show passing in an email object and callback function, you can also directly invoke hello send function by directly specifying email properties.</span></span> <span data-ttu-id="8f65f-136">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8f65f-136">For example:</span></span>  
> 
> `````
> sendgrid.send({
> to: 'john@contoso.com',
> from: 'anna@contoso.com',
> subject: 'test mail',
> text: 'This is a sample email message.'
> });
> `````
> 
> 

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="8f65f-137">Procedure: een bijlage toevoegen</span><span class="sxs-lookup"><span data-stu-id="8f65f-137">How to: Add an Attachment</span></span>
<span data-ttu-id="8f65f-138">Bijlagen kunnen tooa bericht worden toegevoegd door te geven Hallo/logboekbestandsnamen en het pad in Hallo **bestanden** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="8f65f-138">Attachments can be added tooa message by specifying hello file name(s) and path(s) in hello **files** property.</span></span> <span data-ttu-id="8f65f-139">Hallo volgende voorbeeld ziet u een bijlage verzenden:</span><span class="sxs-lookup"><span data-stu-id="8f65f-139">hello following example demonstrates sending an attachment:</span></span>

    sendgrid.send({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.',
        files: [
            {
                filename:     '',           // required only if file.content is used.
                contentType:  '',           // optional
                cid:          '',           // optional, used toospecify cid for inline content
                path:         '',           //
                url:          '',           // == One of these three options is required
                content:      ('' | Buffer) //
            }
        ],
    });

> [!NOTE]
> <span data-ttu-id="8f65f-140">Wanneer u Hallo **bestanden** eigenschap Hallo-bestand moet toegankelijk zijn via [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span><span class="sxs-lookup"><span data-stu-id="8f65f-140">When using hello **files** property, hello file must be accessible through [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span></span> <span data-ttu-id="8f65f-141">Als u wenst dat tooattach Hallo-bestand wordt gehost in Azure Storage, zoals in een Blob-container, moet u eerst kopiëren Hallo toolocal bestandsopslag of tooan Azure station voordat deze kan worden verzonden als een bijlage met Hallo **bestanden** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="8f65f-141">If hello file you wish tooattach is hosted in Azure Storage, such as in a Blob container, you must first copy hello file toolocal storage or tooan Azure drive before it can be sent as an attachment using hello **files** property.</span></span>
> 
> 

## <a name="how-to-use-filters-tooenable-footers-and-tracking"></a><span data-ttu-id="8f65f-142">Procedure: Filters gebruiken om tooEnable voetteksten en bijhouden</span><span class="sxs-lookup"><span data-stu-id="8f65f-142">How to: Use Filters tooEnable Footers and Tracking</span></span>
<span data-ttu-id="8f65f-143">SendGrid biedt extra e-mailfunctionaliteit via Hallo gebruik van filters.</span><span class="sxs-lookup"><span data-stu-id="8f65f-143">SendGrid provides additional email functionality through hello use of filters.</span></span> <span data-ttu-id="8f65f-144">Dit zijn de instellingen die kunnen worden toegevoegd als tooan e-mailbericht naar het inschakelen van specifieke functionaliteit, zoals het inschakelen van Klik bijhouden, Google analytics, abonnement bijhouden, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="8f65f-144">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="8f65f-145">Zie voor een volledige lijst met filters [filterinstellingen][Filter Settings].</span><span class="sxs-lookup"><span data-stu-id="8f65f-145">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

<span data-ttu-id="8f65f-146">Filters kunnen toegepaste tooa bericht worden met behulp van Hallo **filters** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="8f65f-146">Filters can be applied tooa message by using hello **filters** property.</span></span>
<span data-ttu-id="8f65f-147">Elk filter wordt opgegeven met een hash met filter-specifieke instellingen.</span><span class="sxs-lookup"><span data-stu-id="8f65f-147">Each filter is specified by a hash containing filter-specific settings.</span></span>
<span data-ttu-id="8f65f-148">Hallo volgende voorbeelden laten zien Hallo voettekst en klik op filters bijhouden:</span><span class="sxs-lookup"><span data-stu-id="8f65f-148">hello following examples demonstrate hello footer and click tracking filters:</span></span>

### <a name="footer"></a><span data-ttu-id="8f65f-149">Voettekst</span><span class="sxs-lookup"><span data-stu-id="8f65f-149">Footer</span></span>
    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

    email.setFilters({
        'footer': {
            'settings': {
                'enable': 1,
                'text/plain': 'This is a text footer.'
            }
        }
    });

    sendgrid.send(email);

### <a name="click-tracking"></a><span data-ttu-id="8f65f-150">Klik op bijhouden</span><span class="sxs-lookup"><span data-stu-id="8f65f-150">Click Tracking</span></span>
    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

    email.setFilters({
        'clicktrack': {
            'settings': {
                'enable': 1
            }
        }
    });

    sendgrid.send(email);

## <a name="how-to-update-email-properties"></a><span data-ttu-id="8f65f-151">How to: de eigenschappen van het e-mailadres bijwerken</span><span class="sxs-lookup"><span data-stu-id="8f65f-151">How to: Update Email Properties</span></span>
<span data-ttu-id="8f65f-152">Sommige eigenschappen van de e-mail kunnen worden overschreven met  **ingesteld*eigenschap*** of toegevoegd met behulp van  **toevoegen*eigenschap***.</span><span class="sxs-lookup"><span data-stu-id="8f65f-152">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span> <span data-ttu-id="8f65f-153">U kunt extra ontvangers bijvoorbeeld toevoegen met behulp van</span><span class="sxs-lookup"><span data-stu-id="8f65f-153">For example, you can add additional recipients by using</span></span>

    email.addTo('jeff@contoso.com');

<span data-ttu-id="8f65f-154">of een filter instellen met behulp van</span><span class="sxs-lookup"><span data-stu-id="8f65f-154">or set a filter by using</span></span>

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

<span data-ttu-id="8f65f-155">Zie voor meer informatie [sendgrid nodejs][sendgrid-nodejs].</span><span class="sxs-lookup"><span data-stu-id="8f65f-155">For more information, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="8f65f-156">How to: extra SendGrid-Services gebruiken</span><span class="sxs-lookup"><span data-stu-id="8f65f-156">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="8f65f-157">SendGrid biedt op basis van een web-API's die u tooleverage aanvullende SendGrid-functionaliteit van uw Azure-toepassing kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8f65f-157">SendGrid offers web-based APIs that you can use tooleverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="8f65f-158">Zie voor meer details Hallo [SendGrid-API-documentatie][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="8f65f-158">For full details, see hello [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f65f-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8f65f-159">Next Steps</span></span>
<span data-ttu-id="8f65f-160">Nu u basisprincipes Hallo Hallo SendGrid-e-mailservice hebt geleerd, volgt u deze koppelingen toolearn meer.</span><span class="sxs-lookup"><span data-stu-id="8f65f-160">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="8f65f-161">Module-opslagplaats SendGrid Node.js: [sendgrid nodejs][sendgrid-nodejs]</span><span class="sxs-lookup"><span data-stu-id="8f65f-161">SendGrid Node.js module repository: [sendgrid-nodejs][sendgrid-nodejs]</span></span>
* <span data-ttu-id="8f65f-162">SendGrid-API-documentatie: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="8f65f-162">SendGrid API documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="8f65f-163">SendGrid speciale aanbieding voor Azure-klanten: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span><span class="sxs-lookup"><span data-stu-id="8f65f-163">SendGrid special offer for Azure customers: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span></span>

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
[cloud-gebaseerde e-mailservice]: https://sendgrid.com/email-solutions
[levering van de transactionele e]: https://sendgrid.com/transactional-email
