---
title: Het gebruik van SendGrid in Azure Functions | Microsoft Docs
description: Laat zien hoe u SendGrid in Azure Functions
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
ms.openlocfilehash: 05c9f4e4a4351219da68af8b702c25f21d7d4d02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-sendgrid-in-azure-functions"></a><span data-ttu-id="6239a-103">Het gebruik van SendGrid in Azure Functions</span><span class="sxs-lookup"><span data-stu-id="6239a-103">How to use SendGrid in Azure Functions</span></span>

## <a name="sendgrid-overview"></a><span data-ttu-id="6239a-104">SendGrid-overzicht</span><span class="sxs-lookup"><span data-stu-id="6239a-104">SendGrid Overview</span></span>

<span data-ttu-id="6239a-105">Azure Functions ondersteunt SendGrid uitvoer bindingen zodat uw functies voor het verzenden van e-mailberichten met een paar regels code en een SendGrid-account.</span><span class="sxs-lookup"><span data-stu-id="6239a-105">Azure Functions supports SendGrid output bindings to enable your functions to send email messages with a few lines of code and a SendGrid account.</span></span>

<span data-ttu-id="6239a-106">Als u de SendGrid-API in een Azure-functie, hebt u een [SendGrid account](http://SendGrid.com).</span><span class="sxs-lookup"><span data-stu-id="6239a-106">To use the SendGrid API in an Azure Function, you must have a [SendGrid account](http://SendGrid.com).</span></span> <span data-ttu-id="6239a-107">Bovendien moet u een SendGrid-API-sleutel hebben.</span><span class="sxs-lookup"><span data-stu-id="6239a-107">Additionally, you must have a SendGrid API Key.</span></span> <span data-ttu-id="6239a-108">Aanmelden bij uw SendGrid-account en klikt u op **instellingen** vervolgens **API-sleutel** voor het genereren van een API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="6239a-108">Log in to your SendGrid account and click **Settings** then **API Key** to generate an API key.</span></span> <span data-ttu-id="6239a-109">Houd deze sleutel is beschikbaar wanneer u deze in een toekomstige stap gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6239a-109">Keep this key available as you use it in an upcoming step.</span></span>

<span data-ttu-id="6239a-110">U bent nu klaar om te maken van een Azure-functie-app.</span><span class="sxs-lookup"><span data-stu-id="6239a-110">You are now ready to create an Azure Function app.</span></span>

## <a name="create-an-azure-function-app"></a><span data-ttu-id="6239a-111">Een Azure-functie-app maken</span><span class="sxs-lookup"><span data-stu-id="6239a-111">Create an Azure Function app</span></span> 

<span data-ttu-id="6239a-112">Apps van Azure functie zijn containers voor een of meer Azure functions.</span><span class="sxs-lookup"><span data-stu-id="6239a-112">Azure Function Apps are containers for one or more Azure functions.</span></span> <span data-ttu-id="6239a-113">Azure functions meer zijn dan - functie.</span><span class="sxs-lookup"><span data-stu-id="6239a-113">Azure functions are just that - a function.</span></span> <span data-ttu-id="6239a-114">Elke Azure-functie is gekoppeld aan één trigger die een gebeurtenis die ervoor zorgt dat de functie om uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="6239a-114">Each Azure function is tied to one trigger, which is an event that causes the function to run.</span></span>
<span data-ttu-id="6239a-115">Elke functie kan bevatten een willekeurig aantal invoer of uitvoer bindingen.</span><span class="sxs-lookup"><span data-stu-id="6239a-115">Each function can contain any number of input or output bindings.</span></span> <span data-ttu-id="6239a-116">Bindingen zijn services die u in een functie gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="6239a-116">Bindings are services that you can use in a function.</span></span> <span data-ttu-id="6239a-117">SendGrid is een uitvoer-binding die u gebruiken kunt om e-mail te verzenden.</span><span class="sxs-lookup"><span data-stu-id="6239a-117">SendGrid is an output binding you can use to send email.</span></span> 

1. <span data-ttu-id="6239a-118">Aanmelden bij de Azure-portal en [maken van een Azure-functie-App](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) of open een bestaande functie-app.</span><span class="sxs-lookup"><span data-stu-id="6239a-118">Log in to the Azure portal and [create an Azure Function App](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) or open an existing Function app.</span></span> 
2. <span data-ttu-id="6239a-119">Maak een Azure-functie.</span><span class="sxs-lookup"><span data-stu-id="6239a-119">Create an Azure function.</span></span> <span data-ttu-id="6239a-120">Kies een handmatige trigger en C# het gemak houden.</span><span class="sxs-lookup"><span data-stu-id="6239a-120">To keep it simple, choose a manual trigger and C#.</span></span> 

 ![Een Azure-functie maken](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a><span data-ttu-id="6239a-122">SendGrid configureren voor gebruik in een Azure-functie-app</span><span class="sxs-lookup"><span data-stu-id="6239a-122">Configure SendGrid for use in an Azure Function app</span></span>

<span data-ttu-id="6239a-123">U moet uw SendGrid-API-sleutel opslaan als een app-instelling te gebruiken in een functie.</span><span class="sxs-lookup"><span data-stu-id="6239a-123">You must store your SendGrid API Key as an app setting to use it in a function.</span></span> <span data-ttu-id="6239a-124">Het veld ApiKey is niet uw werkelijke SendGrid-API-sleutel, maar een instelling die u app definiëren waarmee uw werkelijke API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="6239a-124">The ApiKey field is not your actual SendGrid API key, but an app setting you define that represents your actual API key.</span></span> <span data-ttu-id="6239a-125">Uw sleutel opslaan op deze manier is voor beveiliging, omdat het gescheiden van alle code of bestanden die kunnen worden gecontroleerd in broncodebeheer.</span><span class="sxs-lookup"><span data-stu-id="6239a-125">Storing your key this way is for security, since it is separate from any code or files that might be checked into source code control.</span></span>

- <span data-ttu-id="6239a-126">Maak een **AppSettings** sleutel in de functie-app **toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="6239a-126">Create an **AppSettings** key in your function app's **Application Settings**.</span></span>

 ![Een Azure-functie maken](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a><span data-ttu-id="6239a-128">SendGrid uitvoer bindingen configureren</span><span class="sxs-lookup"><span data-stu-id="6239a-128">Configure SendGrid output bindings</span></span>

<span data-ttu-id="6239a-129">SendGrid is beschikbaar als een Azure functie uitvoer binding.</span><span class="sxs-lookup"><span data-stu-id="6239a-129">SendGrid is available as an Azure function output binding.</span></span> <span data-ttu-id="6239a-130">Als u wilt maken van een SendGrid uitvoer binding:</span><span class="sxs-lookup"><span data-stu-id="6239a-130">To create a SendGrid output binding:</span></span>

1. <span data-ttu-id="6239a-131">Ga naar de **integreren** tabblad van de functie in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6239a-131">Go to the **Integrate** tab of the function in the Azure portal.</span></span>
2. <span data-ttu-id="6239a-132">Klik op **nieuwe uitvoer** voor het maken van een SendGrid uitvoer binding.</span><span class="sxs-lookup"><span data-stu-id="6239a-132">Click **New Output** to create a SendGrid output binding.</span></span>
3. <span data-ttu-id="6239a-133">Vul de **API-sleutel** en **bericht parameternaam** eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="6239a-133">Fill in the **API Key** and **Message parameter name** properties.</span></span> <span data-ttu-id="6239a-134">Als u wilt, kunt u nu de overige eigenschappen opgeven of ze in plaats daarvan code.</span><span class="sxs-lookup"><span data-stu-id="6239a-134">If you want, you can enter the other properties now, or code them instead.</span></span> <span data-ttu-id="6239a-135">Deze instellingen kunnen worden gebruikt als standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="6239a-135">These settings can be used as defaults.</span></span>

 ![SendGrid uitvoer bindingen configureren](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

<span data-ttu-id="6239a-137">Toevoegen van een binding aan een functie maakt een bestand met de naam **function.json** in de map van de functie.</span><span class="sxs-lookup"><span data-stu-id="6239a-137">Adding a binding to a function creates a file called **function.json** in your function's folder.</span></span> <span data-ttu-id="6239a-138">Dit bestand bevat dezelfde informatie die u in de Azure functie ziet **integreren** tabblad, maar in Json-indeling.</span><span class="sxs-lookup"><span data-stu-id="6239a-138">This file contains all the same information that you see in the Azure function's **Integrate** tab, but in Json format.</span></span> <span data-ttu-id="6239a-139">Instellen van de **ApiKey**, **bericht**, en **van** velden maken de volgende vermeldingen in de **function.json** bestand:</span><span class="sxs-lookup"><span data-stu-id="6239a-139">Setting the **ApiKey**, **message**, and **from** fields create the following entries in the **function.json** file:</span></span> 

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

<span data-ttu-id="6239a-140">Als u liever, kunt u deze mogelijk wijzigen zelf rechtstreeks bestand.</span><span class="sxs-lookup"><span data-stu-id="6239a-140">If you prefer, you may modify this file yourself directly.</span></span>

<span data-ttu-id="6239a-141">Nu dat u hebt gemaakt en de functie-App en de functie geconfigureerd, kunt u de code voor het verzenden van een e-mailbericht schrijven.</span><span class="sxs-lookup"><span data-stu-id="6239a-141">Now that you have created and configured the Function App and function, you can write the code to send an email.</span></span>

## <a name="write-code-that-creates-and-sends-email"></a><span data-ttu-id="6239a-142">Schrijven van code die wordt gemaakt en verzendt e-mailbericht</span><span class="sxs-lookup"><span data-stu-id="6239a-142">Write code that creates and sends email</span></span>

<span data-ttu-id="6239a-143">De SendGrid-API bevat alle opdrachten die u wilt maken en verzenden van een e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="6239a-143">The SendGrid API contains all the commands you need to create and send an email.</span></span>  

- <span data-ttu-id="6239a-144">Vervang de code in de functie met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="6239a-144">Replace the code in the function with the following code:</span></span>

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
    // change to email of recipient
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

<span data-ttu-id="6239a-145">Let op de eerste regel bevat de ```#r``` richtlijn die verwijst naar de SendGrid-assembly.</span><span class="sxs-lookup"><span data-stu-id="6239a-145">Notice the first line contains the ```#r``` directive that references the SendGrid assembly.</span></span> <span data-ttu-id="6239a-146">Daarna kunt u een ```using``` instructie om eenvoudig toegang krijgen tot de objecten in die naamruimte.</span><span class="sxs-lookup"><span data-stu-id="6239a-146">After that, you can use a ```using``` statement to more easily access the objects in that namespace.</span></span> <span data-ttu-id="6239a-147">Maak in de code exemplaren van ```Mail```, ```Personalization```, en ```Content``` objecten uit de SendGrid-API die samen het e-mailbericht vormen.</span><span class="sxs-lookup"><span data-stu-id="6239a-147">In the code, create instances of ```Mail```, ```Personalization```, and ```Content``` objects from the SendGrid API that compose the email.</span></span> <span data-ttu-id="6239a-148">Wanneer u het bericht terugkeert, wordt het door SendGrid biedt.</span><span class="sxs-lookup"><span data-stu-id="6239a-148">When you return the message, SendGrid delivers it.</span></span> 

<span data-ttu-id="6239a-149">De handtekening van de functie bevat ook een extra uitvoerparameter van het type ```Mail``` met de naam ```message```.</span><span class="sxs-lookup"><span data-stu-id="6239a-149">The function's signature also contains an extra out parameter of type ```Mail``` named ```message```.</span></span> <span data-ttu-id="6239a-150">Beide invoer en bindingen express zelf uitvoer als parameters van de functie in de code.</span><span class="sxs-lookup"><span data-stu-id="6239a-150">Both input and output bindings express themselves as function parameters in code.</span></span> 

2. <span data-ttu-id="6239a-151">Testen van uw code door te klikken op **Test** en in te voeren van een bericht in de **aanvraagtekst** veld vervolgens te klikken op de **uitvoeren** knop.</span><span class="sxs-lookup"><span data-stu-id="6239a-151">Test your code by clicking **Test** and entering a message into the **Request body** field, then clicking the **Run** button.</span></span>

 ![Testen van uw code](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. <span data-ttu-id="6239a-153">Controleer de e-mail om te controleren dat SendGrid het e-mailadres verzonden.</span><span class="sxs-lookup"><span data-stu-id="6239a-153">Check email to verify that SendGrid sent the email.</span></span> <span data-ttu-id="6239a-154">Het bestand moet gaat u naar het adres in de code uit stap 1 en bevatten het bericht van de **aanvraagtekst**.</span><span class="sxs-lookup"><span data-stu-id="6239a-154">It should go to the address in the code from step 1, and contain the message from the **Request body**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6239a-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6239a-155">Next steps</span></span>
<span data-ttu-id="6239a-156">In dit artikel is gedemonstreerd hoe u met de SendGrid-service maken en verzenden van e-mail.</span><span class="sxs-lookup"><span data-stu-id="6239a-156">This article has demonstrated how to use the SendGrid service to create and send email.</span></span> <span data-ttu-id="6239a-157">Raadpleeg de volgende onderwerpen voor meer informatie over het gebruik van Azure Functions in uw apps:</span><span class="sxs-lookup"><span data-stu-id="6239a-157">To learn more about using Azure Functions in your apps, see the following topics:</span></span> 

- <span data-ttu-id="6239a-158">[Aanbevolen procedures voor Azure Functions](functions-best-practices.md) vindt u enkele aanbevolen procedures voor gebruik bij het maken van Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="6239a-158">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices to use when creating Azure Functions.</span></span>

- <span data-ttu-id="6239a-159">[Naslaginformatie over Azure Functions developer](functions-reference.md) programmeurs verwijzing voor het coderen van functies en definiëren van triggers en bindingen.</span><span class="sxs-lookup"><span data-stu-id="6239a-159">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>

- <span data-ttu-id="6239a-160">[Azure Functions testen](functions-test-a-function.md) beschrijving van verschillende hulpprogramma's en technieken voor het testen van uw functies.</span><span class="sxs-lookup"><span data-stu-id="6239a-160">[Testing Azure Functions](functions-test-a-function.md) Describes various tools and techniques for testing your functions.</span></span>