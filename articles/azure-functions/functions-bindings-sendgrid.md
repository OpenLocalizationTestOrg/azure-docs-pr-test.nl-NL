---
title: Azure Functions SendGrid-bindingen | Microsoft Docs
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
ms.openlocfilehash: 445a40a884e648cdb2a57f8ef43bed4f8a3efcf2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-sendgrid-bindings"></a><span data-ttu-id="7ad90-103">Azure Functions SendGrid-bindingen</span><span class="sxs-lookup"><span data-stu-id="7ad90-103">Azure Functions SendGrid bindings</span></span>

<span data-ttu-id="7ad90-104">In dit artikel wordt uitgelegd hoe configureren en werken met de SendGrid-bindingen in de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="7ad90-104">This article explains how to configure and work with SendGrid bindings in Azure Functions.</span></span> <span data-ttu-id="7ad90-105">Als de sendgrid, kunt u Azure Functions aangepaste om e-mail te verzenden via een programma.</span><span class="sxs-lookup"><span data-stu-id="7ad90-105">With SendGrid, you can use Azure Functions to send customized email programmatically.</span></span>

<span data-ttu-id="7ad90-106">Dit artikel is referentie-informatie voor ontwikkelaars voor Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="7ad90-106">This article is reference information for Azure Functions developers.</span></span> <span data-ttu-id="7ad90-107">Als u geen ervaring met Azure Functions, start u de volgende bronnen:</span><span class="sxs-lookup"><span data-stu-id="7ad90-107">If you're new to Azure Functions, start with the following resources:</span></span>

<span data-ttu-id="7ad90-108">[Uw eerste Azure-functie maken](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="7ad90-108">[Create your first Azure Function](functions-create-first-azure-function.md).</span></span> 
<span data-ttu-id="7ad90-109">[C#](functions-reference-csharp.md), [F #](functions-reference-fsharp.md), of [knooppunt](functions-reference-node.md) referenties voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="7ad90-109">[C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md), or [Node](functions-reference-node.md) developer references.</span></span>

## <a name="functionjson-for-sendgrid-bindings"></a><span data-ttu-id="7ad90-110">Function.JSON voor SendGrid-bindingen</span><span class="sxs-lookup"><span data-stu-id="7ad90-110">function.json for SendGrid bindings</span></span>

<span data-ttu-id="7ad90-111">Azure Functions bevat een uitvoer-binding voor SendGrid.</span><span class="sxs-lookup"><span data-stu-id="7ad90-111">Azure Functions provides an output binding for SendGrid.</span></span> <span data-ttu-id="7ad90-112">De SendGrid-uitvoer binding schakelt u maken en verzenden van e-programmatisch.</span><span class="sxs-lookup"><span data-stu-id="7ad90-112">The SendGrid output binding enables you to create and send email programmatically.</span></span> 

<span data-ttu-id="7ad90-113">De SendGrid-binding ondersteunt de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="7ad90-113">The SendGrid binding supports the following properties:</span></span>

- <span data-ttu-id="7ad90-114">`name`: Is vereist: de naam van de variabele in functiecode gebruikt voor de aanvraag of de hoofdtekst van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="7ad90-114">`name` : Required - the variable name used in function code for the request or request body.</span></span> <span data-ttu-id="7ad90-115">Deze waarde is ```$return``` wanneer er slechts één waarde.</span><span class="sxs-lookup"><span data-stu-id="7ad90-115">This value is ```$return``` when there is only one return value.</span></span> 
- <span data-ttu-id="7ad90-116">`type`: Vereist - moet worden ingesteld op 'sendGrid'.</span><span class="sxs-lookup"><span data-stu-id="7ad90-116">`type` : Required - must be set to "sendGrid."</span></span>
- <span data-ttu-id="7ad90-117">`direction`: Vereist - moet worden ingesteld op 'out'.</span><span class="sxs-lookup"><span data-stu-id="7ad90-117">`direction` : Required - must be set to "out."</span></span>
- <span data-ttu-id="7ad90-118">`apiKey`: Vereist - moet worden ingesteld op de naam van uw API-sleutel die is opgeslagen in de instellingen van de functie App-app.</span><span class="sxs-lookup"><span data-stu-id="7ad90-118">`apiKey` : Required - must be set to the name of your API key stored in the Function App's app settings.</span></span>
- <span data-ttu-id="7ad90-119">`to`: de ontvanger van e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="7ad90-119">`to` : the recipient's email address.</span></span>
- <span data-ttu-id="7ad90-120">`from`: het e-mailadres van de afzender.</span><span class="sxs-lookup"><span data-stu-id="7ad90-120">`from` : the sender's email address.</span></span>
- <span data-ttu-id="7ad90-121">`subject`: het onderwerp van het e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="7ad90-121">`subject` : the subject of the email.</span></span>
- <span data-ttu-id="7ad90-122">`text`: de inhoud van e-mail.</span><span class="sxs-lookup"><span data-stu-id="7ad90-122">`text` : the email content.</span></span>

<span data-ttu-id="7ad90-123">Voorbeeld van **function.json**:</span><span class="sxs-lookup"><span data-stu-id="7ad90-123">Example of **function.json**:</span></span>

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
> <span data-ttu-id="7ad90-124">Azure Functions slaat uw verbindingsgegevens en API-sleutels als de app-instellingen zodat ze niet zijn ingeschakeld in uw resourcebeheerbibliotheek.</span><span class="sxs-lookup"><span data-stu-id="7ad90-124">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="7ad90-125">Deze actie beschermt uw vertrouwelijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="7ad90-125">This action safeguards your sensitive information.</span></span>
>
>

## <a name="c-example-of-the-sendgrid-output-binding"></a><span data-ttu-id="7ad90-126">C#-voorbeeld van de SendGrid uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="7ad90-126">C# example of the SendGrid output binding</span></span>

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

## <a name="node-example-of-the-sendgrid-output-binding"></a><span data-ttu-id="7ad90-127">Voorbeeld van de knooppunten van het SendGrid uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="7ad90-127">Node example of the SendGrid output binding</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7ad90-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7ad90-128">Next steps</span></span>
<span data-ttu-id="7ad90-129">Zie voor meer informatie over andere bindingen en triggers voor Azure Functions</span><span class="sxs-lookup"><span data-stu-id="7ad90-129">For information about other bindings and triggers for Azure Functions, see</span></span> 
- [<span data-ttu-id="7ad90-130">Azure Functions triggers en bindingen referentie voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="7ad90-130">Azure Functions triggers and bindings developer reference</span></span>](functions-triggers-bindings.md)

- <span data-ttu-id="7ad90-131">[Aanbevolen procedures voor Azure Functions](functions-best-practices.md) vindt u enkele aanbevolen procedures voor gebruik bij het maken van Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="7ad90-131">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices to use when creating Azure Functions.</span></span>

- <span data-ttu-id="7ad90-132">[Naslaginformatie over Azure Functions developer](functions-reference.md) programmeurs verwijzing voor het coderen van functies en definiëren van triggers en bindingen.</span><span class="sxs-lookup"><span data-stu-id="7ad90-132">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>
