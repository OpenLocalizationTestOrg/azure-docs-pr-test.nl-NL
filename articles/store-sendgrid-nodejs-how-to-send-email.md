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
# <a name="how-toosend-email-using-sendgrid-from-nodejs"></a>Hoe tooSend e SendGrid met behulp van Node.js
Deze handleiding wordt uitgelegd hoe e tooperform algemene programmeertaken met de SendGrid-service op Azure. Hallo-voorbeelden zijn geschreven met behulp van Hallo Node.js-API. Hallo scenario's worden behandeld: **construeren e**, **verzenden van e-mail**, **bijlagen toevoegen**, **met filters**, en **eigenschappen bijwerken**. Zie voor meer informatie over SendGrid en verzenden van e-mail Hallo [Vervolgstappen](#next-steps) sectie.

## <a name="what-is-hello-sendgrid-email-service"></a>Wat is Hallo SendGrid e-mailservice?
SendGrid is een [cloud-gebaseerde e-mailservice] die biedt betrouwbare [levering van de transactionele e], schaalbaarheid en realtime-analyses samen met de flexibele API's die aangepaste integratie te vereenvoudigen. Veelvoorkomende gebruiksscenario's van SendGrid zijn onder andere:

* Ontvangstbevestigingen toocustomers automatisch verzenden
* Beheer van distributiepunt bevat voor het verzenden van klanten maandelijkse e-Folders en speciale aanbiedingen
* Realtime metrische gegevens voor items zoals geblokkeerd e- en reactietijd van de klant verzamelen
* Genereren van rapporten toohelp trends identificeren
* Doorsturen van vragen van klanten
* E-mailmeldingen van uw toepassing

Zie voor meer informatie [https://sendgrid.com](https://sendgrid.com).

## <a name="create-a-sendgrid-account"></a>Een SendGrid-Account maken
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-nodejs-module"></a>Verwijzing Hallo SendGrid Node.js-Module
Hallo SendGrid-module voor Node.js kan worden geïnstalleerd via Pakketbeheer Hallo-knooppunt (npm) met behulp van de volgende opdracht Hallo:

    npm install sendgrid

Na de installatie, kunt u met behulp van de volgende code Hallo Hallo module in uw toepassing vereisen:

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

Hallo SendGrid module exporteert Hallo **SendGrid** en **e** functies.
**SendGrid** is verantwoordelijk voor het verzenden van e-mail via Web-API, terwijl **e** ingekapseld een e-mailbericht.

## <a name="how-to-create-an-email"></a>Procedure: een e-mailbericht maken
Maken van een e-mailbericht met Hallo SendGrid-module, moet eerst een e-mailbericht met de functie e Hallo en vervolgens te verzenden met de SendGrid-functie Hallo maken. Hallo Hieronder volgt een voorbeeld van het maken van een nieuw bericht met de functie e Hallo:

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

U kunt ook een HTML-bericht opgeven voor clients die deze ondersteunen door Hallo HTML-eigenschap. Bijvoorbeeld:

    html: This is a sample <b>HTML<b> email message.

Instellen van de eigenschappen van beide Hallo tekst en html biedt correcte terugvallen op tekstinhoud voor clients die HTML-berichten niet ondersteunt.

Zie voor meer informatie over alle eigenschappen die worden ondersteund door Hallo e functie [sendgrid nodejs][sendgrid-nodejs].

## <a name="how-to-send-an-email"></a>Procedure: een e-mailbericht verzenden
Na het maken van een e-mailbericht met Hallo e-functie kunt u met behulp van Web-API is geleverd door SendGrid Hallo verzenden. 

### <a name="web-api"></a>Web-API
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> Terwijl Hallo bovenstaande voorbeelden doorgeven in een e-object en de callback-functie wilt weergeven, kunt u kunt ook rechtstreeks Hallo verzenden functie aanroepen door direct e-eigenschappen op te geven. Bijvoorbeeld:  
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

## <a name="how-to-add-an-attachment"></a>Procedure: een bijlage toevoegen
Bijlagen kunnen tooa bericht worden toegevoegd door te geven Hallo/logboekbestandsnamen en het pad in Hallo **bestanden** eigenschap. Hallo volgende voorbeeld ziet u een bijlage verzenden:

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
> Wanneer u Hallo **bestanden** eigenschap Hallo-bestand moet toegankelijk zijn via [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile). Als u wenst dat tooattach Hallo-bestand wordt gehost in Azure Storage, zoals in een Blob-container, moet u eerst kopiëren Hallo toolocal bestandsopslag of tooan Azure station voordat deze kan worden verzonden als een bijlage met Hallo **bestanden** eigenschap.
> 
> 

## <a name="how-to-use-filters-tooenable-footers-and-tracking"></a>Procedure: Filters gebruiken om tooEnable voetteksten en bijhouden
SendGrid biedt extra e-mailfunctionaliteit via Hallo gebruik van filters. Dit zijn de instellingen die kunnen worden toegevoegd als tooan e-mailbericht naar het inschakelen van specifieke functionaliteit, zoals het inschakelen van Klik bijhouden, Google analytics, abonnement bijhouden, enzovoort. Zie voor een volledige lijst met filters [filterinstellingen][Filter Settings].

Filters kunnen toegepaste tooa bericht worden met behulp van Hallo **filters** eigenschap.
Elk filter wordt opgegeven met een hash met filter-specifieke instellingen.
Hallo volgende voorbeelden laten zien Hallo voettekst en klik op filters bijhouden:

### <a name="footer"></a>Voettekst
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

### <a name="click-tracking"></a>Klik op bijhouden
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

## <a name="how-to-update-email-properties"></a>How to: de eigenschappen van het e-mailadres bijwerken
Sommige eigenschappen van de e-mail kunnen worden overschreven met  **ingesteld*eigenschap*** of toegevoegd met behulp van  **toevoegen*eigenschap***. U kunt extra ontvangers bijvoorbeeld toevoegen met behulp van

    email.addTo('jeff@contoso.com');

of een filter instellen met behulp van

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

Zie voor meer informatie [sendgrid nodejs][sendgrid-nodejs].

## <a name="how-to-use-additional-sendgrid-services"></a>How to: extra SendGrid-Services gebruiken
SendGrid biedt op basis van een web-API's die u tooleverage aanvullende SendGrid-functionaliteit van uw Azure-toepassing kunt gebruiken. Zie voor meer details Hallo [SendGrid-API-documentatie][SendGrid API documentation].

## <a name="next-steps"></a>Volgende stappen
Nu u basisprincipes Hallo Hallo SendGrid-e-mailservice hebt geleerd, volgt u deze koppelingen toolearn meer.

* Module-opslagplaats SendGrid Node.js: [sendgrid nodejs][sendgrid-nodejs]
* SendGrid-API-documentatie: <https://sendgrid.com/docs>
* SendGrid speciale aanbieding voor Azure-klanten: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
[cloud-gebaseerde e-mailservice]: https://sendgrid.com/email-solutions
[levering van de transactionele e]: https://sendgrid.com/transactional-email
