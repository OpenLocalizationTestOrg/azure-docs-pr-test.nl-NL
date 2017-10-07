---
title: aaaHow toouse SendGrid in Azure Functions | Microsoft Docs
description: Toont hoe toouse SendGrid in Azure Functions
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 01/31/2017
ms.author: rachelap
ms.openlocfilehash: a0ffdae04e5924c773d2d26427626fc1f570f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-sendgrid-in-azure-functions"></a><span data-ttu-id="225ab-103">Hoe toouse SendGrid in Azure Functions</span><span class="sxs-lookup"><span data-stu-id="225ab-103">How toouse SendGrid in Azure Functions</span></span>

## <a name="sendgrid-overview"></a><span data-ttu-id="225ab-104">SendGrid-overzicht</span><span class="sxs-lookup"><span data-stu-id="225ab-104">SendGrid Overview</span></span>

<span data-ttu-id="225ab-105">Azure Functions ondersteunt SendGrid uitvoer bindingen tooenable uw functies toosend e-mailberichten met een paar regels code en een SendGrid-account.</span><span class="sxs-lookup"><span data-stu-id="225ab-105">Azure Functions supports SendGrid output bindings tooenable your functions toosend email messages with a few lines of code and a SendGrid account.</span></span>

<span data-ttu-id="225ab-106">toouse hello SendGrid-API in een Azure-functie, hebt u een [SendGrid account](http://SendGrid.com).</span><span class="sxs-lookup"><span data-stu-id="225ab-106">toouse hello SendGrid API in an Azure Function, you must have a [SendGrid account](http://SendGrid.com).</span></span> <span data-ttu-id="225ab-107">Bovendien moet u een SendGrid-API-sleutel hebben.</span><span class="sxs-lookup"><span data-stu-id="225ab-107">Additionally, you must have a SendGrid API Key.</span></span> <span data-ttu-id="225ab-108">Meld u bij tooyour SendGrid-account en klikt u op **instellingen** vervolgens **API-sleutel** toogenerate een API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="225ab-108">Log in tooyour SendGrid account and click **Settings** then **API Key** toogenerate an API key.</span></span> <span data-ttu-id="225ab-109">Houd deze sleutel is beschikbaar wanneer u deze in een toekomstige stap gebruiken.</span><span class="sxs-lookup"><span data-stu-id="225ab-109">Keep this key available as you use it in an upcoming step.</span></span>

<span data-ttu-id="225ab-110">U bent nu klaar toocreate een Azure-functie-app.</span><span class="sxs-lookup"><span data-stu-id="225ab-110">You are now ready toocreate an Azure Function app.</span></span>

## <a name="create-an-azure-function-app"></a><span data-ttu-id="225ab-111">Een Azure-functie-app maken</span><span class="sxs-lookup"><span data-stu-id="225ab-111">Create an Azure Function app</span></span> 

<span data-ttu-id="225ab-112">Apps van Azure functie zijn containers voor een of meer Azure functions.</span><span class="sxs-lookup"><span data-stu-id="225ab-112">Azure Function Apps are containers for one or more Azure functions.</span></span> <span data-ttu-id="225ab-113">Azure functions meer zijn dan - functie.</span><span class="sxs-lookup"><span data-stu-id="225ab-113">Azure functions are just that - a function.</span></span> <span data-ttu-id="225ab-114">Elke Azure-functie is gebonden tooone worden geactiveerd, dit is een gebeurtenis die het Hallo functie toorun veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="225ab-114">Each Azure function is tied tooone trigger, which is an event that causes hello function toorun.</span></span>
<span data-ttu-id="225ab-115">Elke functie kan bevatten een willekeurig aantal invoer of uitvoer bindingen.</span><span class="sxs-lookup"><span data-stu-id="225ab-115">Each function can contain any number of input or output bindings.</span></span> <span data-ttu-id="225ab-116">Bindingen zijn services die u in een functie gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="225ab-116">Bindings are services that you can use in a function.</span></span> <span data-ttu-id="225ab-117">SendGrid is een binding u uitvoer toosend e-mail kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="225ab-117">SendGrid is an output binding you can use toosend email.</span></span> 

1. <span data-ttu-id="225ab-118">Meld u bij toohello Azure-portal en [maken van een Azure-functie-App](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) of open een bestaande functie-app.</span><span class="sxs-lookup"><span data-stu-id="225ab-118">Log in toohello Azure portal and [create an Azure Function App](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) or open an existing Function app.</span></span> 
2. <span data-ttu-id="225ab-119">Maak een Azure-functie.</span><span class="sxs-lookup"><span data-stu-id="225ab-119">Create an Azure function.</span></span> <span data-ttu-id="225ab-120">tookeep het eenvoudig, kies een handmatige trigger en C#.</span><span class="sxs-lookup"><span data-stu-id="225ab-120">tookeep it simple, choose a manual trigger and C#.</span></span> 

 ![Een Azure-functie maken](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a><span data-ttu-id="225ab-122">SendGrid configureren voor gebruik in een Azure-functie-app</span><span class="sxs-lookup"><span data-stu-id="225ab-122">Configure SendGrid for use in an Azure Function app</span></span>

<span data-ttu-id="225ab-123">U moet uw SendGrid-API-sleutel opslaan als een toouse app-instelling in een functie.</span><span class="sxs-lookup"><span data-stu-id="225ab-123">You must store your SendGrid API Key as an app setting toouse it in a function.</span></span> <span data-ttu-id="225ab-124">Hallo ApiKey veld is niet uw werkelijke SendGrid-API-sleutel, maar een instelling die u app definiëren waarmee uw werkelijke API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="225ab-124">hello ApiKey field is not your actual SendGrid API key, but an app setting you define that represents your actual API key.</span></span> <span data-ttu-id="225ab-125">Uw sleutel opslaan op deze manier is voor beveiliging, omdat het gescheiden van alle code of bestanden die kunnen worden gecontroleerd in broncodebeheer.</span><span class="sxs-lookup"><span data-stu-id="225ab-125">Storing your key this way is for security, since it is separate from any code or files that might be checked into source code control.</span></span>

- <span data-ttu-id="225ab-126">Maak een **AppSettings** sleutel in de functie-app **toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="225ab-126">Create an **AppSettings** key in your function app's **Application Settings**.</span></span>

 ![Een Azure-functie maken](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a><span data-ttu-id="225ab-128">SendGrid uitvoer bindingen configureren</span><span class="sxs-lookup"><span data-stu-id="225ab-128">Configure SendGrid output bindings</span></span>

<span data-ttu-id="225ab-129">SendGrid is beschikbaar als een Azure functie uitvoer binding.</span><span class="sxs-lookup"><span data-stu-id="225ab-129">SendGrid is available as an Azure function output binding.</span></span> <span data-ttu-id="225ab-130">een SendGrid toocreate uitvoer binding:</span><span class="sxs-lookup"><span data-stu-id="225ab-130">toocreate a SendGrid output binding:</span></span>

1. <span data-ttu-id="225ab-131">Ga toohello **integreren** tabblad van de functie Hallo in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="225ab-131">Go toohello **Integrate** tab of hello function in hello Azure portal.</span></span>
2. <span data-ttu-id="225ab-132">Klik op **nieuwe uitvoer** toocreate een SendGrid uitvoer binding.</span><span class="sxs-lookup"><span data-stu-id="225ab-132">Click **New Output** toocreate a SendGrid output binding.</span></span>
3. <span data-ttu-id="225ab-133">Vul Hallo **API-sleutel** en **bericht parameternaam** eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="225ab-133">Fill in hello **API Key** and **Message parameter name** properties.</span></span> <span data-ttu-id="225ab-134">Als u wilt, kunt u nu andere eigenschappen hello, of ze in plaats daarvan code.</span><span class="sxs-lookup"><span data-stu-id="225ab-134">If you want, you can enter hello other properties now, or code them instead.</span></span> <span data-ttu-id="225ab-135">Deze instellingen kunnen worden gebruikt als standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="225ab-135">These settings can be used as defaults.</span></span>

 ![SendGrid uitvoer bindingen configureren](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

<span data-ttu-id="225ab-137">Toevoegen van een binding tooa functie maakt een bestand met de naam **function.json** in de map van de functie.</span><span class="sxs-lookup"><span data-stu-id="225ab-137">Adding a binding tooa function creates a file called **function.json** in your function's folder.</span></span> <span data-ttu-id="225ab-138">Dit bestand bevat alle dezelfde informatie die u in hello Azure functie ziet Hallo **integreren** tabblad, maar in Json-indeling.</span><span class="sxs-lookup"><span data-stu-id="225ab-138">This file contains all hello same information that you see in hello Azure function's **Integrate** tab, but in Json format.</span></span> <span data-ttu-id="225ab-139">Instelling Hallo **ApiKey**, **bericht**, en **van** velden maken de volgende vermeldingen in Hallo Hallo **function.json** bestand:</span><span class="sxs-lookup"><span data-stu-id="225ab-139">Setting hello **ApiKey**, **message**, and **from** fields create hello following entries in hello **function.json** file:</span></span> 

```json
{
  "bindings": [    
    {
      "type": "sendGrid",
      "name": "message",
      "apiKey": "SendGridKey",
      "direction": "out",
      "from": "azure@contoso.com"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="225ab-140">Als u liever, kunt u deze mogelijk wijzigen zelf rechtstreeks bestand.</span><span class="sxs-lookup"><span data-stu-id="225ab-140">If you prefer, you may modify this file yourself directly.</span></span>

<span data-ttu-id="225ab-141">Nu dat u hebt gemaakt en geconfigureerd Hallo functie-App en de functie, kunt u een e-mailbericht Hallo code toosend schrijven.</span><span class="sxs-lookup"><span data-stu-id="225ab-141">Now that you have created and configured hello Function App and function, you can write hello code toosend an email.</span></span>

## <a name="write-code-that-creates-and-sends-email"></a><span data-ttu-id="225ab-142">Schrijven van code die wordt gemaakt en verzendt e-mailbericht</span><span class="sxs-lookup"><span data-stu-id="225ab-142">Write code that creates and sends email</span></span>

<span data-ttu-id="225ab-143">Hallo SendGrid-API bevat alle Hallo opdrachten u toocreate nodig hebt en een e-mail sturen.</span><span class="sxs-lookup"><span data-stu-id="225ab-143">hello SendGrid API contains all hello commands you need toocreate and send an email.</span></span>  

- <span data-ttu-id="225ab-144">Hallo-code in Hallo functie vervangen door Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="225ab-144">Replace hello code in hello function with hello following code:</span></span>

```cs
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static void Run(TraceWriter log, string input, out Mail message)
{
    message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    // change tooemail of recipient
    personalization.AddTo(new Email("MoreEmailPlease@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

<span data-ttu-id="225ab-145">Kennisgeving Hallo eerste regel bevat Hallo ```#r``` richtlijn die verwijst naar Hallo SendGrid-assembly.</span><span class="sxs-lookup"><span data-stu-id="225ab-145">Notice hello first line contains hello ```#r``` directive that references hello SendGrid assembly.</span></span> <span data-ttu-id="225ab-146">Daarna kunt u een ```using``` instructie toomore eenvoudig toegang krijgen tot Hallo-objecten in die naamruimte.</span><span class="sxs-lookup"><span data-stu-id="225ab-146">After that, you can use a ```using``` statement toomore easily access hello objects in that namespace.</span></span> <span data-ttu-id="225ab-147">Maak in code hello, exemplaren van ```Mail```, ```Personalization```, en ```Content``` objecten uit Hallo SendGrid-API die e-mailbericht Hallo opstellen.</span><span class="sxs-lookup"><span data-stu-id="225ab-147">In hello code, create instances of ```Mail```, ```Personalization```, and ```Content``` objects from hello SendGrid API that compose hello email.</span></span> <span data-ttu-id="225ab-148">Wanneer u Hallo-bericht terugkeert, wordt het door SendGrid biedt.</span><span class="sxs-lookup"><span data-stu-id="225ab-148">When you return hello message, SendGrid delivers it.</span></span> 

<span data-ttu-id="225ab-149">Hallo van functie handtekening bevat ook een extra uitvoerparameter van het type ```Mail``` met de naam ```message```.</span><span class="sxs-lookup"><span data-stu-id="225ab-149">hello function's signature also contains an extra out parameter of type ```Mail``` named ```message```.</span></span> <span data-ttu-id="225ab-150">Beide invoer en bindingen express zelf uitvoer als parameters van de functie in de code.</span><span class="sxs-lookup"><span data-stu-id="225ab-150">Both input and output bindings express themselves as function parameters in code.</span></span> 

2. <span data-ttu-id="225ab-151">Testen van uw code door te klikken op **Test** en u een bericht in Hallo invoert **aanvraagtekst** veld en vervolgens te klikken op Hallo **uitvoeren** knop.</span><span class="sxs-lookup"><span data-stu-id="225ab-151">Test your code by clicking **Test** and entering a message into hello **Request body** field, then clicking hello **Run** button.</span></span>

 ![Testen van uw code](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. <span data-ttu-id="225ab-153">Controleer de e-tooverify dat SendGrid Hallo e-mailadres verzonden.</span><span class="sxs-lookup"><span data-stu-id="225ab-153">Check email tooverify that SendGrid sent hello email.</span></span> <span data-ttu-id="225ab-154">Het moet gaan toohello adres in Hallo code uit stap 1 en Hallo-bericht van Hallo bevatten **aanvraagtekst**.</span><span class="sxs-lookup"><span data-stu-id="225ab-154">It should go toohello address in hello code from step 1, and contain hello message from hello **Request body**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="225ab-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="225ab-155">Next steps</span></span>
<span data-ttu-id="225ab-156">In dit artikel is gebleken hoe toouse SendGrid service toocreate Hallo en e-mail te sturen.</span><span class="sxs-lookup"><span data-stu-id="225ab-156">This article has demonstrated how toouse hello SendGrid service toocreate and send email.</span></span> <span data-ttu-id="225ab-157">toolearn meer informatie over het gebruik van Azure Functions in uw apps, Zie Hallo volgende onderwerpen:</span><span class="sxs-lookup"><span data-stu-id="225ab-157">toolearn more about using Azure Functions in your apps, see hello following topics:</span></span> 

- <span data-ttu-id="225ab-158">[Aanbevolen procedures voor Azure Functions](functions-best-practices.md) vindt u enkele aanbevolen procedures toouse bij het maken van Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="225ab-158">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices toouse when creating Azure Functions.</span></span>

- <span data-ttu-id="225ab-159">[Naslaginformatie over Azure Functions developer](functions-reference.md) programmeurs verwijzing voor het coderen van functies en definiëren van triggers en bindingen.</span><span class="sxs-lookup"><span data-stu-id="225ab-159">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>

- <span data-ttu-id="225ab-160">[Azure Functions testen](functions-test-a-function.md) beschrijving van verschillende hulpprogramma's en technieken voor het testen van uw functies.</span><span class="sxs-lookup"><span data-stu-id="225ab-160">[Testing Azure Functions](functions-test-a-function.md) Describes various tools and techniques for testing your functions.</span></span>