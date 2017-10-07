---
title: aaaAzure functies SendGrid bindingen | Microsoft Docs
description: Naslaginformatie over Azure Functions SendGrid bindingen
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/16/2017
ms.author: rachelap
ms.openlocfilehash: 10a3837875eb6ae18e6c789bcf64cc401cf5f26a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-sendgrid-bindings"></a>Azure Functions SendGrid-bindingen

Dit artikel wordt uitgelegd hoe tooconfigure en werken met de SendGrid-bindingen in de Azure Functions. Als sendgrid zijn, kunt u Azure Functions toosend aangepast e-mail via een programma.

Dit artikel is referentie-informatie voor ontwikkelaars voor Azure Functions. Als u nieuwe functies voor tooAzure bent, kunt u beginnen met Hallo resources te volgen:

[Uw eerste Azure-functie maken](functions-create-first-azure-function.md). 
[C#](functions-reference-csharp.md), [F #](functions-reference-fsharp.md), of [knooppunt](functions-reference-node.md) referenties voor ontwikkelaars.

## <a name="functionjson-for-sendgrid-bindings"></a>Function.JSON voor SendGrid-bindingen

Azure Functions bevat een uitvoer-binding voor SendGrid. Hallo SendGrid uitvoer binding kunt u toocreate en verzendt e-mail via een programma. 

Hallo SendGrid binding ondersteunt Hallo volgende eigenschappen:

- `name`: Vereist - Hallo variabelenaam in functiecode gebruikt voor het Hallo-aanvraag of de hoofdtekst van de aanvraag. Deze waarde is ```$return``` wanneer er slechts één waarde. 
- `type`: Vereist - moet worden ingesteld te 'sendGrid'.
- `direction`: Vereist - moet zijn ingesteld te 'out'.
- `apiKey`: Vereist - moet toohello naam van uw API-sleutel die is opgeslagen in de instellingen van de Hallo functie App-app.
- `to`: Hallo e-mailadres van de geadresseerde.
- `from`: het e-mailadres van afzender Hallo.
- `subject`: Hallo onderwerp Hallo e-mailadres.
- `text`: Hallo inhoud van e-mail.

Voorbeeld van **function.json**:

```json 
{
    "bindings": [
        {
            "name": "$return",
            "type": "sendGrid",
            "direction": "out",
            "apiKey" : "MySendGridKey",
            "to": "{ToEmail}",
            "from": "{FromEmail}",
            "subject": "SendGrid output bindings"
        }
    ]
}
```

> [!NOTE]
> Azure Functions slaat uw verbindingsgegevens en API-sleutels als de app-instellingen zodat ze niet zijn ingeschakeld in uw resourcebeheerbibliotheek. Deze actie beschermt uw vertrouwelijke gegevens.
>
>

## <a name="c-example-of-hello-sendgrid-output-binding"></a>C#-voorbeeld Hallo SendGrid uitvoer binding

```csharp
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static Mail Run(TraceWriter log, string input, out Mail message)
{
     message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    personalization.AddTo(new Email("recipient@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

## <a name="node-example-of-hello-sendgrid-output-binding"></a>Voorbeeld van de knooppunten van Hallo SendGrid uitvoer binding

```javascript
module.exports = function (context, input) {    
    var message = {
         "personalizations": [ { "to": [ { "email": "sample@sample.com" } ] } ],
        from: "sender@contoso.com",        
        subject: "Azure news",
        content: [{
            type: 'text/plain',
            value: input
        }]
    };

    context.done(null, message);
};

```

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over andere bindingen en triggers voor Azure Functions 
- [Azure Functions triggers en bindingen referentie voor ontwikkelaars](functions-triggers-bindings.md)

- [Aanbevolen procedures voor Azure Functions](functions-best-practices.md) vindt u enkele aanbevolen procedures toouse bij het maken van Azure Functions.

- [Naslaginformatie over Azure Functions developer](functions-reference.md) programmeurs verwijzing voor het coderen van functies en definiëren van triggers en bindingen.
