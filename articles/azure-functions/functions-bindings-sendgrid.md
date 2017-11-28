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
# <a name="azure-functions-sendgrid-bindings"></a><span data-ttu-id="0ee41-103">Azure Functions SendGrid-bindingen</span><span class="sxs-lookup"><span data-stu-id="0ee41-103">Azure Functions SendGrid bindings</span></span>

<span data-ttu-id="0ee41-104">Dit artikel wordt uitgelegd hoe tooconfigure en werken met de SendGrid-bindingen in de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="0ee41-104">This article explains how tooconfigure and work with SendGrid bindings in Azure Functions.</span></span> <span data-ttu-id="0ee41-105">Als sendgrid zijn, kunt u Azure Functions toosend aangepast e-mail via een programma.</span><span class="sxs-lookup"><span data-stu-id="0ee41-105">With SendGrid, you can use Azure Functions toosend customized email programmatically.</span></span>

<span data-ttu-id="0ee41-106">Dit artikel is referentie-informatie voor ontwikkelaars voor Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="0ee41-106">This article is reference information for Azure Functions developers.</span></span> <span data-ttu-id="0ee41-107">Als u nieuwe functies voor tooAzure bent, kunt u beginnen met Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="0ee41-107">If you're new tooAzure Functions, start with hello following resources:</span></span>

<span data-ttu-id="0ee41-108">[Uw eerste Azure-functie maken](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="0ee41-108">[Create your first Azure Function](functions-create-first-azure-function.md).</span></span> 
<span data-ttu-id="0ee41-109">[C#](functions-reference-csharp.md), [F #](functions-reference-fsharp.md), of [knooppunt](functions-reference-node.md) referenties voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="0ee41-109">[C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md), or [Node](functions-reference-node.md) developer references.</span></span>

## <a name="functionjson-for-sendgrid-bindings"></a><span data-ttu-id="0ee41-110">Function.JSON voor SendGrid-bindingen</span><span class="sxs-lookup"><span data-stu-id="0ee41-110">function.json for SendGrid bindings</span></span>

<span data-ttu-id="0ee41-111">Azure Functions bevat een uitvoer-binding voor SendGrid.</span><span class="sxs-lookup"><span data-stu-id="0ee41-111">Azure Functions provides an output binding for SendGrid.</span></span> <span data-ttu-id="0ee41-112">Hallo SendGrid uitvoer binding kunt u toocreate en verzendt e-mail via een programma.</span><span class="sxs-lookup"><span data-stu-id="0ee41-112">hello SendGrid output binding enables you toocreate and send email programmatically.</span></span> 

<span data-ttu-id="0ee41-113">Hallo SendGrid binding ondersteunt Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="0ee41-113">hello SendGrid binding supports hello following properties:</span></span>

- <span data-ttu-id="0ee41-114">`name`: Vereist - Hallo variabelenaam in functiecode gebruikt voor het Hallo-aanvraag of de hoofdtekst van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="0ee41-114">`name` : Required - hello variable name used in function code for hello request or request body.</span></span> <span data-ttu-id="0ee41-115">Deze waarde is ```$return``` wanneer er slechts één waarde.</span><span class="sxs-lookup"><span data-stu-id="0ee41-115">This value is ```$return``` when there is only one return value.</span></span> 
- <span data-ttu-id="0ee41-116">`type`: Vereist - moet worden ingesteld te 'sendGrid'.</span><span class="sxs-lookup"><span data-stu-id="0ee41-116">`type` : Required - must be set too"sendGrid."</span></span>
- <span data-ttu-id="0ee41-117">`direction`: Vereist - moet zijn ingesteld te 'out'.</span><span class="sxs-lookup"><span data-stu-id="0ee41-117">`direction` : Required - must be set too"out."</span></span>
- <span data-ttu-id="0ee41-118">`apiKey`: Vereist - moet toohello naam van uw API-sleutel die is opgeslagen in de instellingen van de Hallo functie App-app.</span><span class="sxs-lookup"><span data-stu-id="0ee41-118">`apiKey` : Required - must be set toohello name of your API key stored in hello Function App's app settings.</span></span>
- <span data-ttu-id="0ee41-119">`to`: Hallo e-mailadres van de geadresseerde.</span><span class="sxs-lookup"><span data-stu-id="0ee41-119">`to` : hello recipient's email address.</span></span>
- <span data-ttu-id="0ee41-120">`from`: het e-mailadres van afzender Hallo.</span><span class="sxs-lookup"><span data-stu-id="0ee41-120">`from` : hello sender's email address.</span></span>
- <span data-ttu-id="0ee41-121">`subject`: Hallo onderwerp Hallo e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="0ee41-121">`subject` : hello subject of hello email.</span></span>
- <span data-ttu-id="0ee41-122">`text`: Hallo inhoud van e-mail.</span><span class="sxs-lookup"><span data-stu-id="0ee41-122">`text` : hello email content.</span></span>

<span data-ttu-id="0ee41-123">Voorbeeld van **function.json**:</span><span class="sxs-lookup"><span data-stu-id="0ee41-123">Example of **function.json**:</span></span>

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
> <span data-ttu-id="0ee41-124">Azure Functions slaat uw verbindingsgegevens en API-sleutels als de app-instellingen zodat ze niet zijn ingeschakeld in uw resourcebeheerbibliotheek.</span><span class="sxs-lookup"><span data-stu-id="0ee41-124">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="0ee41-125">Deze actie beschermt uw vertrouwelijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="0ee41-125">This action safeguards your sensitive information.</span></span>
>
>

## <a name="c-example-of-hello-sendgrid-output-binding"></a><span data-ttu-id="0ee41-126">C#-voorbeeld Hallo SendGrid uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="0ee41-126">C# example of hello SendGrid output binding</span></span>

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

## <a name="node-example-of-hello-sendgrid-output-binding"></a><span data-ttu-id="0ee41-127">Voorbeeld van de knooppunten van Hallo SendGrid uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="0ee41-127">Node example of hello SendGrid output binding</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0ee41-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0ee41-128">Next steps</span></span>
<span data-ttu-id="0ee41-129">Zie voor meer informatie over andere bindingen en triggers voor Azure Functions</span><span class="sxs-lookup"><span data-stu-id="0ee41-129">For information about other bindings and triggers for Azure Functions, see</span></span> 
- [<span data-ttu-id="0ee41-130">Azure Functions triggers en bindingen referentie voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="0ee41-130">Azure Functions triggers and bindings developer reference</span></span>](functions-triggers-bindings.md)

- <span data-ttu-id="0ee41-131">[Aanbevolen procedures voor Azure Functions](functions-best-practices.md) vindt u enkele aanbevolen procedures toouse bij het maken van Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="0ee41-131">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices toouse when creating Azure Functions.</span></span>

- <span data-ttu-id="0ee41-132">[Naslaginformatie over Azure Functions developer](functions-reference.md) programmeurs verwijzing voor het coderen van functies en definiëren van triggers en bindingen.</span><span class="sxs-lookup"><span data-stu-id="0ee41-132">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>
