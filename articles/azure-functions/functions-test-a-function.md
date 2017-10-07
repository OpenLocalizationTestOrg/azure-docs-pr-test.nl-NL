---
title: aaaTesting Azure Functions | Microsoft Docs
description: Test uw Azure-functies met Postman cURL en Node.js.
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: Azure functions, functies, verwerking van gebeurtenissen, webhooks, dynamische compute, zonder server architectuur testen
ms.assetid: c00f3082-30d2-46b3-96ea-34faf2f15f77
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/02/2017
ms.author: wesmc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a084f8dbc8089356c3c19d789dc9098f2bb63052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="strategies-for-testing-your-code-in-azure-functions"></a><span data-ttu-id="af84f-104">Strategieën voor het testen van uw code in Azure Functions</span><span class="sxs-lookup"><span data-stu-id="af84f-104">Strategies for testing your code in Azure Functions</span></span>

<span data-ttu-id="af84f-105">Dit onderwerp wordt beschreven Hallo verschillende manieren tootest-functies, inclusief het gebruik van de volgende algemene Hallo nadert:</span><span class="sxs-lookup"><span data-stu-id="af84f-105">This topic demonstrates hello various ways tootest functions, including using hello following general approaches:</span></span>

+ <span data-ttu-id="af84f-106">HTTP-gebaseerde hulpprogramma's, zoals cURL Postman en zelfs een webbrowser voor triggers voor webgebaseerde</span><span class="sxs-lookup"><span data-stu-id="af84f-106">HTTP-based tools, such as cURL, Postman, and even a web browser for web-based triggers</span></span>
+ <span data-ttu-id="af84f-107">Azure Opslagverkenner tootest op basis van een Azure Storage-triggers</span><span class="sxs-lookup"><span data-stu-id="af84f-107">Azure Storage Explorer, tootest Azure Storage-based triggers</span></span>
+ <span data-ttu-id="af84f-108">Tabblad testresultaten in hello Azure Functions-portal</span><span class="sxs-lookup"><span data-stu-id="af84f-108">Test tab in hello Azure Functions portal</span></span>
+ <span data-ttu-id="af84f-109">Functie Timer geactiveerd</span><span class="sxs-lookup"><span data-stu-id="af84f-109">Timer-triggered function</span></span>
+ <span data-ttu-id="af84f-110">Testen van de toepassing of framework</span><span class="sxs-lookup"><span data-stu-id="af84f-110">Testing application or framework</span></span>

<span data-ttu-id="af84f-111">Al deze methoden testen een HTTP-trigger functie gebruiken die invoer via een accepteert query-tekenreeks parameter of Hallo aanvraagtekst.</span><span class="sxs-lookup"><span data-stu-id="af84f-111">All these testing methods use an HTTP trigger function that accepts input through either a query string parameter or hello request body.</span></span> <span data-ttu-id="af84f-112">U kunt deze functie maken in de eerste sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="af84f-112">You create this function in hello first section.</span></span>

## <a name="create-a-function-for-testing"></a><span data-ttu-id="af84f-113">Maak een functie voor het testen</span><span class="sxs-lookup"><span data-stu-id="af84f-113">Create a function for testing</span></span>
<span data-ttu-id="af84f-114">Voor de meeste van deze zelfstudie gebruiken we een enigszins gewijzigde versie Hallo HttpTrigger JavaScript-sjabloon voor de functie die beschikbaar is wanneer u een functie.</span><span class="sxs-lookup"><span data-stu-id="af84f-114">For most of this tutorial, we use a slightly modified version of hello HttpTrigger JavaScript function template that is available when you create a function.</span></span> <span data-ttu-id="af84f-115">Als u informatie over het maken van een functie nodig, Bekijk dit [zelfstudie](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="af84f-115">If you need help creating a function, review this [tutorial](functions-create-first-azure-function.md).</span></span> <span data-ttu-id="af84f-116">Kies Hallo **HttpTrigger - JavaScript** sjabloon bij het maken van de functie test Hallo in Hallo [Azure-portal].</span><span class="sxs-lookup"><span data-stu-id="af84f-116">Choose hello **HttpTrigger- JavaScript** template when creating hello test function in hello [Azure portal].</span></span>

<span data-ttu-id="af84f-117">Hallo functie standaardsjabloon is in feite een "Hallo wereld" functie die echo back Hallo-naam van Hallo aanvraag hoofdtekst of de query tekenreeksparameter `name=<your name>`.</span><span class="sxs-lookup"><span data-stu-id="af84f-117">hello default function template is basically a "hello world" function that echoes back hello name from hello request body or query string parameter, `name=<your name>`.</span></span>  <span data-ttu-id="af84f-118">Hallo code ontvangt updates tooalso kunt u tooprovide Hallo naam en een adres als JSON-inhoud in de aanvraagtekst Hallo.</span><span class="sxs-lookup"><span data-stu-id="af84f-118">We'll update hello code tooalso allow you tooprovide hello name and an address as JSON content in hello request body.</span></span> <span data-ttu-id="af84f-119">Hallo functie echo vervolgens deze client back toohello indien beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="af84f-119">Then hello function echoes these back toohello client when available.</span></span>   

<span data-ttu-id="af84f-120">Hallo-functie met de volgende code, die zullen worden gebruikt voor het testen van Hallo bijwerken:</span><span class="sxs-lookup"><span data-stu-id="af84f-120">Update hello function with hello following code, which we will use for testing:</span></span>

```javascript
module.exports = function (context, req) {
    context.log("HTTP trigger function processed a request. RequestUri=%s", req.originalUrl);
    context.log("Request Headers = " + JSON.stringify(req.headers));
    var res;

    if (req.query.name || (req.body && req.body.name)) {
        if (typeof req.query.name != "undefined") {
            context.log("Name was provided as a query string param...");
            res = ProcessNewUserInformation(context, req.query.name);
        }
        else {
            context.log("Processing user info from request body...");
            res = ProcessNewUserInformation(context, req.body.name, req.body.address);
        }
    }
    else {
        res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done(null, res);
};
function ProcessNewUserInformation(context, name, address) {
    context.log("Processing user information...");
    context.log("name = " + name);
    var echoString = "Hello " + name;
    var res;

    if (typeof address != "undefined") {
        echoString += "\n" + "hello address you provided is " + address;
        context.log("address = " + address);
    }
    res = {
        // status: 200, /* Defaults too200 */
        body: echoString
    };
    return res;
}
```

## <a name="test-a-function-with-tools"></a><span data-ttu-id="af84f-121">Een functie met hulpprogramma's testen</span><span class="sxs-lookup"><span data-stu-id="af84f-121">Test a function with tools</span></span>
<span data-ttu-id="af84f-122">Buiten hello Azure-portal zijn er verschillende hulpprogramma's waarmee u tootrigger uw functies voor het testen kunt.</span><span class="sxs-lookup"><span data-stu-id="af84f-122">Outside hello Azure portal, there are various tools that you can use tootrigger your functions for testing.</span></span> <span data-ttu-id="af84f-123">Het gaat hierbij om HTTP-hulpprogramma's (zowel gebruikersinterface gebaseerde als command line), programma's voor Azure Storage-toegang en zelfs een eenvoudige webbrowser testen.</span><span class="sxs-lookup"><span data-stu-id="af84f-123">These include HTTP testing tools (both UI-based and command line), Azure Storage access tools, and even a simple web browser.</span></span>

### <a name="test-with-a-browser"></a><span data-ttu-id="af84f-124">Testen met een browser</span><span class="sxs-lookup"><span data-stu-id="af84f-124">Test with a browser</span></span>
<span data-ttu-id="af84f-125">Hallo-webbrowser is een eenvoudige manier tootrigger functies via HTTP.</span><span class="sxs-lookup"><span data-stu-id="af84f-125">hello web browser is a simple way tootrigger functions via HTTP.</span></span> <span data-ttu-id="af84f-126">U kunt een browser gebruiken voor GET-aanvragen die niet te worden een nettolading in de hoofdtekst hoeven en dat gebruik alleen een query tekenreeksparameters.</span><span class="sxs-lookup"><span data-stu-id="af84f-126">You can use a browser for GET requests that do not require a body payload, and that use only query string parameters.</span></span>

<span data-ttu-id="af84f-127">tootest hello functie we eerder hebt gedefinieerd, kopie Hallo **Function Url** van Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="af84f-127">tootest hello function we defined earlier, copy hello **Function Url** from hello portal.</span></span> <span data-ttu-id="af84f-128">Hallo volgende vorm heeft:</span><span class="sxs-lookup"><span data-stu-id="af84f-128">It has hello following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="af84f-129">Hallo toevoegen `name` parameter toohello query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="af84f-129">Append hello `name` parameter toohello query string.</span></span> <span data-ttu-id="af84f-130">Werkelijke bestandsnaam Hallo `<Enter a name here>` tijdelijke aanduiding.</span><span class="sxs-lookup"><span data-stu-id="af84f-130">Use an actual name for hello `<Enter a name here>` placeholder.</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

<span data-ttu-id="af84f-131">Hallo-URL plakken in uw browser en u krijgt een reactie vergelijkbaar toohello volgende.</span><span class="sxs-lookup"><span data-stu-id="af84f-131">Paste hello URL into your browser, and you should get a response similar toohello following.</span></span>

![Schermopname van Chrome browsertabblad met de reactie van de test](./media/functions-test-a-function/browser-test.png)

<span data-ttu-id="af84f-133">In dit voorbeeld is de Chrome-browser hello, die geschikt is voor Hallo tekenreeks geretourneerd in XML.</span><span class="sxs-lookup"><span data-stu-id="af84f-133">This example is hello Chrome browser, which wraps hello returned string in XML.</span></span> <span data-ttu-id="af84f-134">Andere browsers weergeven NET Hallo string-waarde.</span><span class="sxs-lookup"><span data-stu-id="af84f-134">Other browsers display just hello string value.</span></span>

<span data-ttu-id="af84f-135">In de portal Hallo **logboeken** venster uitvoer vergelijkbare toohello volgende wordt vastgelegd in het Hallo-functie wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="af84f-135">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T07:34:59  Welcome, you are now connected toolog-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a><span data-ttu-id="af84f-136">Testen met Postman</span><span class="sxs-lookup"><span data-stu-id="af84f-136">Test with Postman</span></span>
<span data-ttu-id="af84f-137">Hallo aanbevolen hulpprogramma tootest het merendeel van uw functies is Postman die kan worden geïntegreerd met Hallo Chrome-browser.</span><span class="sxs-lookup"><span data-stu-id="af84f-137">hello recommended tool tootest most of your functions is Postman, which integrates with hello Chrome browser.</span></span> <span data-ttu-id="af84f-138">tooinstall Postman, Zie [Postman ophalen](https://www.getpostman.com/).</span><span class="sxs-lookup"><span data-stu-id="af84f-138">tooinstall Postman, see [Get Postman](https://www.getpostman.com/).</span></span> <span data-ttu-id="af84f-139">Postman biedt controle over veel meer kenmerken van een HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="af84f-139">Postman provides control over many more attributes of an HTTP request.</span></span>

> [!TIP]
> <span data-ttu-id="af84f-140">Hallo HTTP-test hulpprogramma dat u meest vertrouwd met bent gebruiken.</span><span class="sxs-lookup"><span data-stu-id="af84f-140">Use hello HTTP testing tool that you are most comfortable with.</span></span> <span data-ttu-id="af84f-141">Hier volgen enkele tooPostman alternatieven:</span><span class="sxs-lookup"><span data-stu-id="af84f-141">Here are some alternatives tooPostman:</span></span>  
>
> * [<span data-ttu-id="af84f-142">Fiddler</span><span class="sxs-lookup"><span data-stu-id="af84f-142">Fiddler</span></span>](http://www.telerik.com/fiddler)  
> * [<span data-ttu-id="af84f-143">Paw</span><span class="sxs-lookup"><span data-stu-id="af84f-143">Paw</span></span>](https://luckymarmot.com/paw)  
>
>

<span data-ttu-id="af84f-144">tootest Hallo-functie met een aanvraagtekst in Postman:</span><span class="sxs-lookup"><span data-stu-id="af84f-144">tootest hello function with a request body in Postman:</span></span>

1. <span data-ttu-id="af84f-145">Postman starten vanuit Hallo **Apps** knop in Hallo linkerbovenhoek van een Chrome-browservenster.</span><span class="sxs-lookup"><span data-stu-id="af84f-145">Start Postman from hello **Apps** button in hello upper-left corner of a Chrome browser window.</span></span>
2. <span data-ttu-id="af84f-146">Kopieer uw **Function Url**, en plak deze in Postman.</span><span class="sxs-lookup"><span data-stu-id="af84f-146">Copy your **Function Url**, and paste it into Postman.</span></span> <span data-ttu-id="af84f-147">Het bevat Hallo toegangscode querytekenreeksparameter.</span><span class="sxs-lookup"><span data-stu-id="af84f-147">It includes hello access code query string parameter.</span></span>
3. <span data-ttu-id="af84f-148">Hallo HTTP-methode te wijzigen**POST**.</span><span class="sxs-lookup"><span data-stu-id="af84f-148">Change hello HTTP method too**POST**.</span></span>
4. <span data-ttu-id="af84f-149">Klik op **hoofdtekst** > **onbewerkte**, en voeg een JSON-aanvraag hoofdtekst vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="af84f-149">Click **Body** > **raw**, and add a JSON request body similar toohello following:</span></span>

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. <span data-ttu-id="af84f-150">Klik op **verzenden**.</span><span class="sxs-lookup"><span data-stu-id="af84f-150">Click **Send**.</span></span>

<span data-ttu-id="af84f-151">Hallo ziet volgende afbeelding u testen Hallo eenvoudige echo functie voorbeeld in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="af84f-151">hello following image shows testing hello simple echo function example in this tutorial.</span></span>

![Schermopname van Postman-gebruikersinterface](./media/functions-test-a-function/postman-test.png)

<span data-ttu-id="af84f-153">In de portal Hallo **logboeken** venster uitvoer vergelijkbare toohello volgende wordt vastgelegd in het Hallo-functie wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="af84f-153">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:04:51  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-hello-command-line"></a><span data-ttu-id="af84f-154">Testen met cURL vanaf de opdrachtregel Hallo</span><span class="sxs-lookup"><span data-stu-id="af84f-154">Test with cURL from hello command line</span></span>
<span data-ttu-id="af84f-155">Vaak wanneer u software test, is het niet nodig toolook ieder verder dan Hallo opdrachtregel toohelp foutopsporing van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="af84f-155">Often when you're testing software, it's not necessary toolook any further than hello command line toohelp debug your application.</span></span> <span data-ttu-id="af84f-156">Dit gaat niet anders zijn met het testen van functies.</span><span class="sxs-lookup"><span data-stu-id="af84f-156">This is no different with testing functions.</span></span> <span data-ttu-id="af84f-157">Houd er rekening mee dat cURL Hallo op Linux gebaseerde systemen standaard beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="af84f-157">Note that hello cURL is available by default on Linux-based systems.</span></span> <span data-ttu-id="af84f-158">In Windows, moet u eerst downloaden en installeren van Hallo [cURL hulpprogramma](https://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="af84f-158">On Windows, you must first download and install hello [cURL tool](https://curl.haxx.se/).</span></span>

<span data-ttu-id="af84f-159">tootest hello functie dat we eerder hebt gedefinieerd, kopie Hallo **Function URL** van Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="af84f-159">tootest hello function that we defined earlier, copy hello **Function URL** from hello portal.</span></span> <span data-ttu-id="af84f-160">Hallo volgende vorm heeft:</span><span class="sxs-lookup"><span data-stu-id="af84f-160">It has hello following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="af84f-161">Dit is Hallo-URL voor activering van de functie.</span><span class="sxs-lookup"><span data-stu-id="af84f-161">This is hello URL for triggering your function.</span></span> <span data-ttu-id="af84f-162">Dit testen met behulp van Hallo cURL-opdracht op Hallo opdrachtregel toomake een GET (`-G` of `--get`)-aanvraag in voor de functie Hallo:</span><span class="sxs-lookup"><span data-stu-id="af84f-162">Test this by using hello cURL command on hello command line toomake a GET (`-G` or `--get`) request against hello function:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="af84f-163">Dit voorbeeld vereist een queryreeksparameter als gegevens kan worden doorgegeven (`-d`) in Hallo cURL-opdracht:</span><span class="sxs-lookup"><span data-stu-id="af84f-163">This particular example requires a query string parameter, which can be passed as Data (`-d`) in hello cURL command:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

<span data-ttu-id="af84f-164">Voer Hallo-opdracht, en u ziet Hallo na de uitvoer van de functie Hallo op Hallo-opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="af84f-164">Run hello command, and you see hello following output of hello function on hello command line:</span></span>

![Schermopname van opdrachtprompt uitvoer](./media/functions-test-a-function/curl-test.png)

<span data-ttu-id="af84f-166">In de portal Hallo **logboeken** venster uitvoer vergelijkbare toohello volgende wordt vastgelegd in het Hallo-functie wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="af84f-166">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-04-05T21:55:09  Welcome, you are now connected toolog-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a><span data-ttu-id="af84f-167">Een blob-trigger testen met behulp van Opslagverkenner</span><span class="sxs-lookup"><span data-stu-id="af84f-167">Test a blob trigger by using Storage Explorer</span></span>
<span data-ttu-id="af84f-168">U kunt een blob-activeringsfunctie testen met behulp van [Azure Opslagverkenner](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="af84f-168">You can test a blob trigger function by using [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

1. <span data-ttu-id="af84f-169">In Hallo [Azure-portal] maken voor uw app functie activeringsfunctie voor C#, F # of JavaScript-blob.</span><span class="sxs-lookup"><span data-stu-id="af84f-169">In hello [Azure portal] for your function app, create a C#, F# or JavaScript blob trigger function.</span></span> <span data-ttu-id="af84f-170">Hallo toomonitor toohello padnaam van uw blob-container instellen.</span><span class="sxs-lookup"><span data-stu-id="af84f-170">Set hello path toomonitor toohello name of your blob container.</span></span> <span data-ttu-id="af84f-171">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="af84f-171">For example:</span></span>

        files
2. <span data-ttu-id="af84f-172">Klik op Hallo  **+**  tooselect knop of Hallo gewenste toouse storage-account maken.</span><span class="sxs-lookup"><span data-stu-id="af84f-172">Click hello **+** button tooselect or create hello storage account you want toouse.</span></span> <span data-ttu-id="af84f-173">Klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="af84f-173">Then click **Create**.</span></span>
3. <span data-ttu-id="af84f-174">Maak een tekstbestand met de volgende tekst hello en sla het:</span><span class="sxs-lookup"><span data-stu-id="af84f-174">Create a text file with hello following text, and save it:</span></span>

        A text file for blob trigger function testing.
4. <span data-ttu-id="af84f-175">Voer [Azure Opslagverkenner](http://storageexplorer.com/), en maak verbinding toohello blob-container in Hallo storage-account wordt bewaakt.</span><span class="sxs-lookup"><span data-stu-id="af84f-175">Run [Azure Storage Explorer](http://storageexplorer.com/), and connect toohello blob container in hello storage account being monitored.</span></span>
5. <span data-ttu-id="af84f-176">Klik op **uploaden** tooupload Hallo-tekstbestand.</span><span class="sxs-lookup"><span data-stu-id="af84f-176">Click **Upload** tooupload hello text file.</span></span>

    ![Schermopname van Opslagverkenner](./media/functions-test-a-function/azure-storage-explorer-test.png)

<span data-ttu-id="af84f-178">Hallo standaard blob-activeringscode functie rapporten Hallo verwerking van Hallo blob in Hallo Logboeken:</span><span class="sxs-lookup"><span data-stu-id="af84f-178">hello default blob trigger function code reports hello processing of hello blob in hello logs:</span></span>

    2016-03-24T11:30:10  Welcome, you are now connected toolog-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a><span data-ttu-id="af84f-179">Een functie binnen functies testen</span><span class="sxs-lookup"><span data-stu-id="af84f-179">Test a function within functions</span></span>
<span data-ttu-id="af84f-180">Hello Azure Functions-portal is ontworpen toolet testen van HTTP- en timer functies geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="af84f-180">hello Azure Functions portal is designed toolet you test HTTP and timer triggered functions.</span></span> <span data-ttu-id="af84f-181">U kunt functies tootrigger ook andere functies die u wilt testen maken.</span><span class="sxs-lookup"><span data-stu-id="af84f-181">You can also create functions tootrigger other functions that you are testing.</span></span>

### <a name="test-with-hello-functions-portal-run-button"></a><span data-ttu-id="af84f-182">Testen met de knop portal uitvoeren functies Hallo</span><span class="sxs-lookup"><span data-stu-id="af84f-182">Test with hello Functions portal Run button</span></span>
<span data-ttu-id="af84f-183">Hallo-portal biedt een **uitvoeren** knop waarmee u toodo sommige kunt beperkt testen.</span><span class="sxs-lookup"><span data-stu-id="af84f-183">hello portal provides a **Run** button that you can use toodo some limited testing.</span></span> <span data-ttu-id="af84f-184">U kunt een aanvraaginhoud opgeven met behulp van de knop hello, maar u kan bieden queryreeksparameters of bijwerken van de aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="af84f-184">You can provide a request body by using hello button, but you can't provide query string parameters or update request headers.</span></span>

<span data-ttu-id="af84f-185">Hallo HTTP-activeringsfunctie we eerder hebben gemaakt door een JSON-tekenreeks vergelijkbare toohello na toe te voegen in Hallo testen **aanvraagtekst** veld.</span><span class="sxs-lookup"><span data-stu-id="af84f-185">Test hello HTTP trigger function we created earlier by adding a JSON string similar toohello following in hello **Request body** field.</span></span> <span data-ttu-id="af84f-186">Klik vervolgens op Hallo **uitvoeren** knop.</span><span class="sxs-lookup"><span data-stu-id="af84f-186">Then click hello **Run** button.</span></span>

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

<span data-ttu-id="af84f-187">In de portal Hallo **logboeken** venster uitvoer vergelijkbare toohello volgende wordt vastgelegd in het Hallo-functie wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="af84f-187">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:03:12  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a><span data-ttu-id="af84f-188">Testen met een timertrigger</span><span class="sxs-lookup"><span data-stu-id="af84f-188">Test with a timer trigger</span></span>
<span data-ttu-id="af84f-189">Sommige functies kunnen niet correct worden getest met Hallo-hulpprogramma's die eerder is vermeld.</span><span class="sxs-lookup"><span data-stu-id="af84f-189">Some functions can't be adequately tested with hello tools mentioned previously.</span></span> <span data-ttu-id="af84f-190">Neem bijvoorbeeld een wachtrij trigger-functie die wordt uitgevoerd als er een bericht is verwijderd in [Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="af84f-190">For example, consider a queue trigger function that runs when a message is dropped into [Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="af84f-191">U kunt altijd schrijven code toodrop een bericht in de wachtrij en een voorbeeld hiervan in een consoleproject verderop in dit artikel wordt aangeboden.</span><span class="sxs-lookup"><span data-stu-id="af84f-191">You can always write code toodrop a message into your queue, and an example of this in a console project is provided later in this article.</span></span> <span data-ttu-id="af84f-192">Er is echter een andere benadering die kunt u functies rechtstreeks te testen.</span><span class="sxs-lookup"><span data-stu-id="af84f-192">However, there is another approach you can use that tests functions directly.</span></span>  

<span data-ttu-id="af84f-193">U kunt een timertrigger geconfigureerd met een wachtrij uitvoer van de binding.</span><span class="sxs-lookup"><span data-stu-id="af84f-193">You can use a timer trigger configured with a queue output binding.</span></span> <span data-ttu-id="af84f-194">Dat timer activeringscode Hallo test berichten toohello wachtrij vervolgens schrijven kunt.</span><span class="sxs-lookup"><span data-stu-id="af84f-194">That timer trigger code can then write hello test messages toohello queue.</span></span> <span data-ttu-id="af84f-195">Deze sectie wordt een voorbeeld uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="af84f-195">This section walks through an example.</span></span>

<span data-ttu-id="af84f-196">Zie voor meer gedetailleerde informatie over het gebruik van bindingen met Azure Functions Hallo [naslaginformatie voor ontwikkelaars van Azure Functions](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="af84f-196">For more in-depth information on using bindings with Azure Functions, see hello [Azure Functions developer reference](functions-reference.md).</span></span>

#### <a name="create-a-queue-trigger-for-testing"></a><span data-ttu-id="af84f-197">Maken van een wachtrij-trigger voor het testen</span><span class="sxs-lookup"><span data-stu-id="af84f-197">Create a queue trigger for testing</span></span>
<span data-ttu-id="af84f-198">toodemonstrate deze benadering eerst maken we een wachtrij trigger-functie die we tootest voor een wachtrij met de naam willen `queue-newusers`.</span><span class="sxs-lookup"><span data-stu-id="af84f-198">toodemonstrate this approach, we first create a queue trigger function that we want tootest for a queue named `queue-newusers`.</span></span> <span data-ttu-id="af84f-199">Deze functie verwerkt naam en adres informatie verwijderd in de wachtrij opslag voor een nieuwe gebruiker.</span><span class="sxs-lookup"><span data-stu-id="af84f-199">This function processes name and address information dropped into Queue storage for a new user.</span></span>

> [!NOTE]
> <span data-ttu-id="af84f-200">Als u de naam van een andere wachtrij gebruikt, controleert u of Hallo-naam die u gebruikt voldoet toohello [naamgeving van wachtrijen en metagegevens](https://msdn.microsoft.com/library/dd179349.aspx) regels.</span><span class="sxs-lookup"><span data-stu-id="af84f-200">If you use a different queue name, make sure hello name you use conforms toohello [Naming Queues and MetaData](https://msdn.microsoft.com/library/dd179349.aspx) rules.</span></span> <span data-ttu-id="af84f-201">Anders kunt u een foutmelding krijgt.</span><span class="sxs-lookup"><span data-stu-id="af84f-201">Otherwise, you get an error.</span></span>
>
>

1. <span data-ttu-id="af84f-202">In Hallo [Azure-portal] voor functie-app klikt u op **nieuwe functie** > **QueueTrigger - C#**.</span><span class="sxs-lookup"><span data-stu-id="af84f-202">In hello [Azure portal] for your function app, click **New Function** > **QueueTrigger - C#**.</span></span>
2. <span data-ttu-id="af84f-203">Voer Hallo wachtrij naam toobe bewaakt door Hallo wachtrij functie:</span><span class="sxs-lookup"><span data-stu-id="af84f-203">Enter hello queue name toobe monitored by hello queue function:</span></span>

        queue-newusers
3. <span data-ttu-id="af84f-204">Klik op Hallo  **+**  tooselect knop of Hallo gewenste toouse storage-account maken.</span><span class="sxs-lookup"><span data-stu-id="af84f-204">Click hello **+** button tooselect or create hello storage account you want toouse.</span></span> <span data-ttu-id="af84f-205">Klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="af84f-205">Then click **Create**.</span></span>
4. <span data-ttu-id="af84f-206">Laat deze portal browservenster geopend, zodat u Hallo logboekvermeldingen voor Hallo wachtrij functie sjabloon standaardcode kunt bewaken.</span><span class="sxs-lookup"><span data-stu-id="af84f-206">Leave this portal browser window open, so you can monitor hello log entries for hello default queue function template code.</span></span>

#### <a name="create-a-timer-trigger-toodrop-a-message-in-hello-queue"></a><span data-ttu-id="af84f-207">Een timer trigger toodrop van een bericht in Hallo wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="af84f-207">Create a timer trigger toodrop a message in hello queue</span></span>
1. <span data-ttu-id="af84f-208">Open Hallo [Azure-portal] in een nieuw browservenster en navigeer tooyour functie-app.</span><span class="sxs-lookup"><span data-stu-id="af84f-208">Open hello [Azure portal] in a new browser window, and navigate tooyour function app.</span></span>
2. <span data-ttu-id="af84f-209">Klik op **nieuwe functie** > **TimerTrigger - C#**.</span><span class="sxs-lookup"><span data-stu-id="af84f-209">Click **New Function** > **TimerTrigger - C#**.</span></span> <span data-ttu-id="af84f-210">Voer een expressie cron tooset hoe vaak hello timer code wordt getest uw wachtrij-functie.</span><span class="sxs-lookup"><span data-stu-id="af84f-210">Enter a cron expression tooset how often hello timer code tests your queue function.</span></span> <span data-ttu-id="af84f-211">Klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="af84f-211">Then click **Create**.</span></span> <span data-ttu-id="af84f-212">Als u Hallo test toorun elke 30 seconden wilt, kunt u de volgende Hallo [CRON expressie](https://wikipedia.org/wiki/Cron#CRON_expression):</span><span class="sxs-lookup"><span data-stu-id="af84f-212">If you want hello test toorun every 30 seconds, you can use hello following [CRON expression](https://wikipedia.org/wiki/Cron#CRON_expression):</span></span>

        */30 * * * * *
3. <span data-ttu-id="af84f-213">Klik op Hallo **integreren** tabblad voor de nieuwe timertrigger.</span><span class="sxs-lookup"><span data-stu-id="af84f-213">Click hello **Integrate** tab for your new timer trigger.</span></span>
4. <span data-ttu-id="af84f-214">Onder **uitvoer**, klikt u op **+ nieuw uitvoer**.</span><span class="sxs-lookup"><span data-stu-id="af84f-214">Under **Output**, click **+ New Output**.</span></span> <span data-ttu-id="af84f-215">Klik vervolgens op **wachtrij** en **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="af84f-215">Then click **queue** and **Select**.</span></span>
5. <span data-ttu-id="af84f-216">Opmerking Hallo die u voor Hallo gebruikt **bericht wachtrijobject**.</span><span class="sxs-lookup"><span data-stu-id="af84f-216">Note hello name you use for hello **queue message object**.</span></span> <span data-ttu-id="af84f-217">U gebruikt dit in Hallo timer functiecode.</span><span class="sxs-lookup"><span data-stu-id="af84f-217">You use this in hello timer function code.</span></span>

        myQueue
6. <span data-ttu-id="af84f-218">Voer Hallo wachtrijnaam, waarbij het Hallo-bericht wordt verzonden:</span><span class="sxs-lookup"><span data-stu-id="af84f-218">Enter hello queue name where hello message is sent:</span></span>

        queue-newusers
7. <span data-ttu-id="af84f-219">Klik op Hallo  **+**  knop tooselect Hallo storage-account die u eerder hebt gebruikt met Hallo wachtrij trigger.</span><span class="sxs-lookup"><span data-stu-id="af84f-219">Click hello **+** button tooselect hello storage account you used previously with hello queue trigger.</span></span> <span data-ttu-id="af84f-220">Klik vervolgens op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="af84f-220">Then click **Save**.</span></span>
8. <span data-ttu-id="af84f-221">Klik op Hallo **ontwikkelen** tabblad voor de timertrigger.</span><span class="sxs-lookup"><span data-stu-id="af84f-221">Click hello **Develop** tab for your timer trigger.</span></span>
9. <span data-ttu-id="af84f-222">Kunt u Hallo na de code voor de functie Hallo C#-timer, zolang u dezelfde wachtrij bericht objectnaam hierboven Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="af84f-222">You can use hello following code for hello C# timer function, as long as you used hello same queue message object name shown earlier.</span></span> <span data-ttu-id="af84f-223">Klik vervolgens op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="af84f-223">Then click **Save**.</span></span>

    ```cs
    using System;

    public static void Run(TimerInfo myTimer, out String myQueue, TraceWriter log)
    {
        String newUser =
        "{\"name\":\"User testing from C# timer function\",\"address\":\"XYZ\"}";

        log.Verbose($"C# Timer trigger function executed at: {DateTime.Now}");   
        log.Verbose($"{newUser}");   

        myQueue = newUser;
    }
    ```

<span data-ttu-id="af84f-224">Hallo functie van C#-timer wordt op dit punt wordt elke 30 seconden uitgevoerd als u Hallo voorbeeld cron-expressie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="af84f-224">At this point, hello C# timer function executes every 30 seconds if you used hello example cron expression.</span></span> <span data-ttu-id="af84f-225">Hallo-logboeken voor de functie timer Hallo report elke uitvoering:</span><span class="sxs-lookup"><span data-stu-id="af84f-225">hello logs for hello timer function report each execution:</span></span>

    2016-03-24T10:27:02  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

<span data-ttu-id="af84f-226">In het browservenster Hallo voor Hallo wachtrij functie ziet u elk bericht wordt verwerkt:</span><span class="sxs-lookup"><span data-stu-id="af84f-226">In hello browser window for hello queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a><span data-ttu-id="af84f-227">Testen van een functie met code</span><span class="sxs-lookup"><span data-stu-id="af84f-227">Test a function with code</span></span>
<span data-ttu-id="af84f-228">Mogelijk moet u een externe toepassing of framework tootest toocreate uw functies.</span><span class="sxs-lookup"><span data-stu-id="af84f-228">You may need toocreate an external application or framework tootest your functions.</span></span>

### <a name="test-an-http-trigger-function-with-code-nodejs"></a><span data-ttu-id="af84f-229">Testen van een HTTP-trigger-functie met code: Node.js</span><span class="sxs-lookup"><span data-stu-id="af84f-229">Test an HTTP trigger function with code: Node.js</span></span>
<span data-ttu-id="af84f-230">U kunt een Node.js-app tooexecute een HTTP-aanvraag tootest uw functie te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="af84f-230">You can use a Node.js app tooexecute an HTTP request tootest your function.</span></span>
<span data-ttu-id="af84f-231">Zorg ervoor dat tooset:</span><span class="sxs-lookup"><span data-stu-id="af84f-231">Make sure tooset:</span></span>

* <span data-ttu-id="af84f-232">Hallo `host` in Hallo aanvraag opties tooyour functie app-host.</span><span class="sxs-lookup"><span data-stu-id="af84f-232">hello `host` in hello request options tooyour function app host.</span></span>
* <span data-ttu-id="af84f-233">De functienaam in Hallo `path`.</span><span class="sxs-lookup"><span data-stu-id="af84f-233">Your function name in hello `path`.</span></span>
* <span data-ttu-id="af84f-234">Uw toegangscode (`<your code>`) in Hallo `path`.</span><span class="sxs-lookup"><span data-stu-id="af84f-234">Your access code (`<your code>`) in hello `path`.</span></span>

<span data-ttu-id="af84f-235">Codevoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="af84f-235">Code example:</span></span>

```javascript
var http = require("http");

var nameQueryString = "name=Wes%20Query%20String%20Test%20From%20Node.js";

var nameBodyJSON = {
    name : "Wes testing with Node.JS code",
    address : "Dallas, T.X. 75201"
};

var bodyString = JSON.stringify(nameBodyJSON);

var options = {
  host: "functions841def78.azurewebsites.net",
  //path: "/api/HttpTriggerNodeJS2?code=sc1wt62opn7k9buhrm8jpds4ikxvvj42m5ojdt0p91lz5jnhfr2c74ipoujyq26wab3wk5gkfbt9&" + nameQueryString,
  path: "/api/HttpTriggerNodeJS2?code=sc1wt62opn7k9buhrm8jpds4ikxvvj42m5ojdt0p91lz5jnhfr2c74ipoujyq26wab3wk5gkfbt9",
  method: "POST",
  headers : {
      "Content-Type":"application/json",
      "Content-Length": Buffer.byteLength(bodyString)
    }    
};

callback = function(response) {
  var str = ""
  response.on("data", function (chunk) {
    str += chunk;
  });

  response.on("end", function () {
    console.log(str);
  });
}

var req = http.request(options, callback);
console.log("*** Sending name and address in body ***");
console.log(bodyString);
req.end(bodyString);
```


<span data-ttu-id="af84f-236">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="af84f-236">Output:</span></span>

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    hello address you provided is Dallas, T.X. 75201

<span data-ttu-id="af84f-237">In de portal Hallo **logboeken** venster uitvoer vergelijkbare toohello volgende wordt vastgelegd in het Hallo-functie wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="af84f-237">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:08:55  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a><span data-ttu-id="af84f-238">Testen van een functie van de trigger wachtrij met code: C#</span><span class="sxs-lookup"><span data-stu-id="af84f-238">Test a queue trigger function with code: C#</span></span> #
<span data-ttu-id="af84f-239">Eerder vermeld dat u een trigger wachtrij testen kunt met behulp van code toodrop een bericht in de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="af84f-239">We mentioned earlier that you can test a queue trigger by using code toodrop a message in your queue.</span></span> <span data-ttu-id="af84f-240">Hallo volgende voorbeeldcode is gebaseerd op Hallo C#-code die zijn gepresenteerd in Hallo [aan de slag met Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="af84f-240">hello following example code is based on hello C# code presented in hello [Getting started with Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md) tutorial.</span></span> <span data-ttu-id="af84f-241">Code voor andere talen is ook beschikbaar via deze koppeling.</span><span class="sxs-lookup"><span data-stu-id="af84f-241">Code for other languages is also available from that link.</span></span>

<span data-ttu-id="af84f-242">tootest deze code in een console-app, moet u:</span><span class="sxs-lookup"><span data-stu-id="af84f-242">tootest this code in a console app, you must:</span></span>

* <span data-ttu-id="af84f-243">[De opslagverbindingsreeks configureren in Hallo app.config-bestand](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="af84f-243">[Configure your storage connection string in hello app.config file](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>
* <span data-ttu-id="af84f-244">Geeft een `name` en `address` als parameters toohello app.</span><span class="sxs-lookup"><span data-stu-id="af84f-244">Pass a `name` and `address` as parameters toohello app.</span></span> <span data-ttu-id="af84f-245">Bijvoorbeeld `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span><span class="sxs-lookup"><span data-stu-id="af84f-245">For example, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span></span> <span data-ttu-id="af84f-246">(Deze code accepteert Hallo naam en adres voor een nieuwe gebruiker als opdrachtregelargumenten tijdens runtime.)</span><span class="sxs-lookup"><span data-stu-id="af84f-246">(This code accepts hello name and address for a new user as command-line arguments during runtime.)</span></span>

<span data-ttu-id="af84f-247">Van C#-voorbeeldcode:</span><span class="sxs-lookup"><span data-stu-id="af84f-247">Example C# code:</span></span>

```cs
static void Main(string[] args)
{
    string name = null;
    string address = null;
    string queueName = "queue-newusers";
    string JSON = null;

    if (args.Length > 0)
    {
        name = args[0];
    }
    if (args.Length > 1)
    {
        address = args[1];
    }

    // Retrieve storage account from connection string
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConfigurationManager.AppSettings["StorageConnectionString"]);

    // Create hello queue client
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

    // Retrieve a reference tooa queue
    CloudQueue queue = queueClient.GetQueueReference(queueName);

    // Create hello queue if it doesn't already exist
    queue.CreateIfNotExists();

    // Create a message and add it toohello queue.
    if (name != null)
    {
        if (address != null)
            JSON = String.Format("{{\"name\":\"{0}\",\"address\":\"{1}\"}}", name, address);
        else
            JSON = String.Format("{{\"name\":\"{0}\"}}", name);
    }

    Console.WriteLine("Adding message too" + queueName + "...");
    Console.WriteLine(JSON);

    CloudQueueMessage message = new CloudQueueMessage(JSON);
    queue.AddMessage(message);
}
```

<span data-ttu-id="af84f-248">In het browservenster Hallo voor Hallo wachtrij functie ziet u elk bericht wordt verwerkt:</span><span class="sxs-lookup"><span data-stu-id="af84f-248">In hello browser window for hello queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[Azure-portal]: https://portal.azure.com
