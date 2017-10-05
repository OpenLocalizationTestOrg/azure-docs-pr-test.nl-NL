---
title: Azure Functions testen | Microsoft Docs
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
ms.openlocfilehash: aca03ba4137893157fcbe6650336782ab88cd234
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="strategies-for-testing-your-code-in-azure-functions"></a><span data-ttu-id="14cca-104">Strategieën voor het testen van uw code in Azure Functions</span><span class="sxs-lookup"><span data-stu-id="14cca-104">Strategies for testing your code in Azure Functions</span></span>

<span data-ttu-id="14cca-105">In dit onderwerp toont de verschillende manieren voor het testen van functies, inclusief het gebruik van de volgende algemene methoden:</span><span class="sxs-lookup"><span data-stu-id="14cca-105">This topic demonstrates the various ways to test functions, including using the following general approaches:</span></span>

+ <span data-ttu-id="14cca-106">HTTP-gebaseerde hulpprogramma's, zoals cURL Postman en zelfs een webbrowser voor triggers voor webgebaseerde</span><span class="sxs-lookup"><span data-stu-id="14cca-106">HTTP-based tools, such as cURL, Postman, and even a web browser for web-based triggers</span></span>
+ <span data-ttu-id="14cca-107">Azure Storage Explorer voor het testen van triggers op basis van een Azure Storage</span><span class="sxs-lookup"><span data-stu-id="14cca-107">Azure Storage Explorer, to test Azure Storage-based triggers</span></span>
+ <span data-ttu-id="14cca-108">Tabblad testresultaten in de Azure Functions-portal</span><span class="sxs-lookup"><span data-stu-id="14cca-108">Test tab in the Azure Functions portal</span></span>
+ <span data-ttu-id="14cca-109">Functie Timer geactiveerd</span><span class="sxs-lookup"><span data-stu-id="14cca-109">Timer-triggered function</span></span>
+ <span data-ttu-id="14cca-110">Testen van de toepassing of framework</span><span class="sxs-lookup"><span data-stu-id="14cca-110">Testing application or framework</span></span>

<span data-ttu-id="14cca-111">Deze test methoden gebruiken een HTTP-trigger-functie die invoer via een queryreeksparameter opgeven of de aanvraagtekst accepteert.</span><span class="sxs-lookup"><span data-stu-id="14cca-111">All these testing methods use an HTTP trigger function that accepts input through either a query string parameter or the request body.</span></span> <span data-ttu-id="14cca-112">U kunt deze functie maakt in de eerste sectie.</span><span class="sxs-lookup"><span data-stu-id="14cca-112">You create this function in the first section.</span></span>

## <a name="create-a-function-for-testing"></a><span data-ttu-id="14cca-113">Maak een functie voor het testen</span><span class="sxs-lookup"><span data-stu-id="14cca-113">Create a function for testing</span></span>
<span data-ttu-id="14cca-114">Voor de meeste van deze zelfstudie gebruiken we een enigszins gewijzigde versie van de sjabloon van de HttpTrigger JavaScript-functie die beschikbaar is wanneer u een functie.</span><span class="sxs-lookup"><span data-stu-id="14cca-114">For most of this tutorial, we use a slightly modified version of the HttpTrigger JavaScript function template that is available when you create a function.</span></span> <span data-ttu-id="14cca-115">Als u informatie over het maken van een functie nodig, Bekijk dit [zelfstudie](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="14cca-115">If you need help creating a function, review this [tutorial](functions-create-first-azure-function.md).</span></span> <span data-ttu-id="14cca-116">Kies de **HttpTrigger - JavaScript** sjabloon bij het maken van de functie test in de [Azure-portal].</span><span class="sxs-lookup"><span data-stu-id="14cca-116">Choose the **HttpTrigger- JavaScript** template when creating the test function in the [Azure portal].</span></span>

<span data-ttu-id="14cca-117">De functie standaardsjabloon is in feite een 'Hallo wereld'-functie die de naam van de aanvraag hoofdtekst of de query tekenreeksparameter, een echo terug `name=<your name>`.</span><span class="sxs-lookup"><span data-stu-id="14cca-117">The default function template is basically a "hello world" function that echoes back the name from the request body or query string parameter, `name=<your name>`.</span></span>  <span data-ttu-id="14cca-118">De code ook dat u kunt de naam en een adres opgeven als JSON-inhoud in de aanvraagtekst ontvangt updates.</span><span class="sxs-lookup"><span data-stu-id="14cca-118">We'll update the code to also allow you to provide the name and an address as JSON content in the request body.</span></span> <span data-ttu-id="14cca-119">De functie echo vervolgens deze weer aan de client, indien beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="14cca-119">Then the function echoes these back to the client when available.</span></span>   

<span data-ttu-id="14cca-120">De functie bijgewerkt met de volgende code, die zullen worden gebruikt voor het testen:</span><span class="sxs-lookup"><span data-stu-id="14cca-120">Update the function with the following code, which we will use for testing:</span></span>

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
            body: "Please pass a name on the query string or in the request body"
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
        echoString += "\n" + "The address you provided is " + address;
        context.log("address = " + address);
    }
    res = {
        // status: 200, /* Defaults to 200 */
        body: echoString
    };
    return res;
}
```

## <a name="test-a-function-with-tools"></a><span data-ttu-id="14cca-121">Een functie met hulpprogramma's testen</span><span class="sxs-lookup"><span data-stu-id="14cca-121">Test a function with tools</span></span>
<span data-ttu-id="14cca-122">Er zijn verschillende hulpmiddelen die u gebruiken kunt voor het activeren van uw functies voor het testen van buiten de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="14cca-122">Outside the Azure portal, there are various tools that you can use to trigger your functions for testing.</span></span> <span data-ttu-id="14cca-123">Het gaat hierbij om HTTP-hulpprogramma's (zowel gebruikersinterface gebaseerde als command line), programma's voor Azure Storage-toegang en zelfs een eenvoudige webbrowser testen.</span><span class="sxs-lookup"><span data-stu-id="14cca-123">These include HTTP testing tools (both UI-based and command line), Azure Storage access tools, and even a simple web browser.</span></span>

### <a name="test-with-a-browser"></a><span data-ttu-id="14cca-124">Testen met een browser</span><span class="sxs-lookup"><span data-stu-id="14cca-124">Test with a browser</span></span>
<span data-ttu-id="14cca-125">De webbrowser is een eenvoudige manier om functies via HTTP-trigger.</span><span class="sxs-lookup"><span data-stu-id="14cca-125">The web browser is a simple way to trigger functions via HTTP.</span></span> <span data-ttu-id="14cca-126">U kunt een browser gebruiken voor GET-aanvragen die niet te worden een nettolading in de hoofdtekst hoeven en dat gebruik alleen een query tekenreeksparameters.</span><span class="sxs-lookup"><span data-stu-id="14cca-126">You can use a browser for GET requests that do not require a body payload, and that use only query string parameters.</span></span>

<span data-ttu-id="14cca-127">Om de functie eerder testen, kopieert u de **Function Url** vanuit de portal.</span><span class="sxs-lookup"><span data-stu-id="14cca-127">To test the function we defined earlier, copy the **Function Url** from the portal.</span></span> <span data-ttu-id="14cca-128">Heeft de volgende notatie:</span><span class="sxs-lookup"><span data-stu-id="14cca-128">It has the following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="14cca-129">Toevoeg-de `name` -parameter voor de queryreeks.</span><span class="sxs-lookup"><span data-stu-id="14cca-129">Append the `name` parameter to the query string.</span></span> <span data-ttu-id="14cca-130">Werkelijke naam van de `<Enter a name here>` tijdelijke aanduiding.</span><span class="sxs-lookup"><span data-stu-id="14cca-130">Use an actual name for the `<Enter a name here>` placeholder.</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

<span data-ttu-id="14cca-131">Plak de URL in uw browser en krijgt u een reactie vergelijkbaar met het volgende.</span><span class="sxs-lookup"><span data-stu-id="14cca-131">Paste the URL into your browser, and you should get a response similar to the following.</span></span>

![Schermopname van Chrome browsertabblad met de reactie van de test](./media/functions-test-a-function/browser-test.png)

<span data-ttu-id="14cca-133">In dit voorbeeld is de Chrome-browser die geschikt is voor de geretourneerde tekenreeks in XML.</span><span class="sxs-lookup"><span data-stu-id="14cca-133">This example is the Chrome browser, which wraps the returned string in XML.</span></span> <span data-ttu-id="14cca-134">Andere browsers weergeven de string-waarde.</span><span class="sxs-lookup"><span data-stu-id="14cca-134">Other browsers display just the string value.</span></span>

<span data-ttu-id="14cca-135">In de portal **logboeken** venster uitvoer lijkt op de volgende wordt vastgelegd in de functie wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="14cca-135">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T07:34:59  Welcome, you are now connected to log-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a><span data-ttu-id="14cca-136">Testen met Postman</span><span class="sxs-lookup"><span data-stu-id="14cca-136">Test with Postman</span></span>
<span data-ttu-id="14cca-137">De aanbevolen hulpprogramma voor het testen van de meeste van uw functies is Postman die kan worden geïntegreerd met de Chrome-browser.</span><span class="sxs-lookup"><span data-stu-id="14cca-137">The recommended tool to test most of your functions is Postman, which integrates with the Chrome browser.</span></span> <span data-ttu-id="14cca-138">Zie het installeren van Postman [Postman ophalen](https://www.getpostman.com/).</span><span class="sxs-lookup"><span data-stu-id="14cca-138">To install Postman, see [Get Postman](https://www.getpostman.com/).</span></span> <span data-ttu-id="14cca-139">Postman biedt controle over veel meer kenmerken van een HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="14cca-139">Postman provides control over many more attributes of an HTTP request.</span></span>

> [!TIP]
> <span data-ttu-id="14cca-140">Gebruik het hulpprogramma dat u meest vertrouwd met bent testen HTTP.</span><span class="sxs-lookup"><span data-stu-id="14cca-140">Use the HTTP testing tool that you are most comfortable with.</span></span> <span data-ttu-id="14cca-141">Hier volgen enkele alternatieven voor Postman:</span><span class="sxs-lookup"><span data-stu-id="14cca-141">Here are some alternatives to Postman:</span></span>  
>
> * [<span data-ttu-id="14cca-142">Fiddler</span><span class="sxs-lookup"><span data-stu-id="14cca-142">Fiddler</span></span>](http://www.telerik.com/fiddler)  
> * [<span data-ttu-id="14cca-143">Paw</span><span class="sxs-lookup"><span data-stu-id="14cca-143">Paw</span></span>](https://luckymarmot.com/paw)  
>
>

<span data-ttu-id="14cca-144">De functie met een aanvraagtekst in Postman testen:</span><span class="sxs-lookup"><span data-stu-id="14cca-144">To test the function with a request body in Postman:</span></span>

1. <span data-ttu-id="14cca-145">Start Postman van de **Apps** knop in de linkerbovenhoek van een Chrome-browservenster.</span><span class="sxs-lookup"><span data-stu-id="14cca-145">Start Postman from the **Apps** button in the upper-left corner of a Chrome browser window.</span></span>
2. <span data-ttu-id="14cca-146">Kopieer uw **Function Url**, en plak deze in Postman.</span><span class="sxs-lookup"><span data-stu-id="14cca-146">Copy your **Function Url**, and paste it into Postman.</span></span> <span data-ttu-id="14cca-147">Dit omvat de toegangscode queryreeksparameter opgeven.</span><span class="sxs-lookup"><span data-stu-id="14cca-147">It includes the access code query string parameter.</span></span>
3. <span data-ttu-id="14cca-148">De HTTP-methode te wijzigen **POST**.</span><span class="sxs-lookup"><span data-stu-id="14cca-148">Change the HTTP method to **POST**.</span></span>
4. <span data-ttu-id="14cca-149">Klik op **hoofdtekst** > **onbewerkte**, en voeg een JSON-aanvraagtekst vergelijkbaar met het volgende:</span><span class="sxs-lookup"><span data-stu-id="14cca-149">Click **Body** > **raw**, and add a JSON request body similar to the following:</span></span>

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. <span data-ttu-id="14cca-150">Klik op **verzenden**.</span><span class="sxs-lookup"><span data-stu-id="14cca-150">Click **Send**.</span></span>

<span data-ttu-id="14cca-151">De volgende afbeelding ziet u het voorbeeld van de functie eenvoudige echo testen in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="14cca-151">The following image shows testing the simple echo function example in this tutorial.</span></span>

![Schermopname van Postman-gebruikersinterface](./media/functions-test-a-function/postman-test.png)

<span data-ttu-id="14cca-153">In de portal **logboeken** venster uitvoer lijkt op de volgende wordt vastgelegd in de functie wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="14cca-153">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T08:04:51  Welcome, you are now connected to log-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-the-command-line"></a><span data-ttu-id="14cca-154">Testen met cURL vanaf de opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="14cca-154">Test with cURL from the command line</span></span>
<span data-ttu-id="14cca-155">Vaak wanneer u test software, is het niet nodig een verder dan de opdrachtregel om te helpen bij foutopsporing van uw toepassing opzoeken.</span><span class="sxs-lookup"><span data-stu-id="14cca-155">Often when you're testing software, it's not necessary to look any further than the command line to help debug your application.</span></span> <span data-ttu-id="14cca-156">Dit gaat niet anders zijn met het testen van functies.</span><span class="sxs-lookup"><span data-stu-id="14cca-156">This is no different with testing functions.</span></span> <span data-ttu-id="14cca-157">Houd er rekening mee dat de cURL op Linux gebaseerde systemen standaard beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="14cca-157">Note that the cURL is available by default on Linux-based systems.</span></span> <span data-ttu-id="14cca-158">In Windows, moet u eerst downloaden en installeren de [cURL hulpprogramma](https://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="14cca-158">On Windows, you must first download and install the [cURL tool](https://curl.haxx.se/).</span></span>

<span data-ttu-id="14cca-159">Voor het testen van de functie die we eerder hebt gedefinieerd, kopieert u de **Function URL** vanuit de portal.</span><span class="sxs-lookup"><span data-stu-id="14cca-159">To test the function that we defined earlier, copy the **Function URL** from the portal.</span></span> <span data-ttu-id="14cca-160">Heeft de volgende notatie:</span><span class="sxs-lookup"><span data-stu-id="14cca-160">It has the following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="14cca-161">Dit is de URL voor activering van de functie.</span><span class="sxs-lookup"><span data-stu-id="14cca-161">This is the URL for triggering your function.</span></span> <span data-ttu-id="14cca-162">Dit testen met behulp van de cURL-opdracht op de opdrachtregel om te maken van een GET (`-G` of `--get`)-aanvraag in voor de functie:</span><span class="sxs-lookup"><span data-stu-id="14cca-162">Test this by using the cURL command on the command line to make a GET (`-G` or `--get`) request against the function:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="14cca-163">Dit voorbeeld vereist een queryreeksparameter als gegevens kan worden doorgegeven (`-d`) in de cURL-opdracht:</span><span class="sxs-lookup"><span data-stu-id="14cca-163">This particular example requires a query string parameter, which can be passed as Data (`-d`) in the cURL command:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

<span data-ttu-id="14cca-164">Voer de opdracht en ziet u de volgende uitvoer van de functie op de opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="14cca-164">Run the command, and you see the following output of the function on the command line:</span></span>

![Schermopname van opdrachtprompt uitvoer](./media/functions-test-a-function/curl-test.png)

<span data-ttu-id="14cca-166">In de portal **logboeken** venster uitvoer lijkt op de volgende wordt vastgelegd in de functie wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="14cca-166">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-04-05T21:55:09  Welcome, you are now connected to log-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a><span data-ttu-id="14cca-167">Een blob-trigger testen met behulp van Opslagverkenner</span><span class="sxs-lookup"><span data-stu-id="14cca-167">Test a blob trigger by using Storage Explorer</span></span>
<span data-ttu-id="14cca-168">U kunt een blob-activeringsfunctie testen met behulp van [Azure Opslagverkenner](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="14cca-168">You can test a blob trigger function by using [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

1. <span data-ttu-id="14cca-169">In de [Azure-portal] maken voor uw app functie activeringsfunctie voor C#, F # of JavaScript-blob.</span><span class="sxs-lookup"><span data-stu-id="14cca-169">In the [Azure portal] for your function app, create a C#, F# or JavaScript blob trigger function.</span></span> <span data-ttu-id="14cca-170">Het pad voor het bewaken van de naam van uw blob-container instellen.</span><span class="sxs-lookup"><span data-stu-id="14cca-170">Set the path to monitor to the name of your blob container.</span></span> <span data-ttu-id="14cca-171">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="14cca-171">For example:</span></span>

        files
2. <span data-ttu-id="14cca-172">Klik op de  **+**  knop om te selecteren of maken van het opslagaccount dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="14cca-172">Click the **+** button to select or create the storage account you want to use.</span></span> <span data-ttu-id="14cca-173">Klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="14cca-173">Then click **Create**.</span></span>
3. <span data-ttu-id="14cca-174">Maak een tekstbestand met de volgende tekst en sla het:</span><span class="sxs-lookup"><span data-stu-id="14cca-174">Create a text file with the following text, and save it:</span></span>

        A text file for blob trigger function testing.
4. <span data-ttu-id="14cca-175">Voer [Azure Opslagverkenner](http://storageexplorer.com/), en maak verbinding met de blob-container in het opslagaccount wordt bewaakt.</span><span class="sxs-lookup"><span data-stu-id="14cca-175">Run [Azure Storage Explorer](http://storageexplorer.com/), and connect to the blob container in the storage account being monitored.</span></span>
5. <span data-ttu-id="14cca-176">Klik op **uploaden** voor het uploaden van het tekstbestand.</span><span class="sxs-lookup"><span data-stu-id="14cca-176">Click **Upload** to upload the text file.</span></span>

    ![Schermopname van Opslagverkenner](./media/functions-test-a-function/azure-storage-explorer-test.png)

<span data-ttu-id="14cca-178">De code van de standaard blob trigger functie rapporteert de verwerking van de blob in de logboeken:</span><span class="sxs-lookup"><span data-stu-id="14cca-178">The default blob trigger function code reports the processing of the blob in the logs:</span></span>

    2016-03-24T11:30:10  Welcome, you are now connected to log-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a><span data-ttu-id="14cca-179">Een functie binnen functies testen</span><span class="sxs-lookup"><span data-stu-id="14cca-179">Test a function within functions</span></span>
<span data-ttu-id="14cca-180">De Azure portal is ontworpen om te laten u testen HTTP-functies en -functies van de timer geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="14cca-180">The Azure Functions portal is designed to let you test HTTP and timer triggered functions.</span></span> <span data-ttu-id="14cca-181">U kunt ook functies voor het activeren van andere functies die u wilt testen maken.</span><span class="sxs-lookup"><span data-stu-id="14cca-181">You can also create functions to trigger other functions that you are testing.</span></span>

### <a name="test-with-the-functions-portal-run-button"></a><span data-ttu-id="14cca-182">Testen met de knop portal functies uitvoeren</span><span class="sxs-lookup"><span data-stu-id="14cca-182">Test with the Functions portal Run button</span></span>
<span data-ttu-id="14cca-183">De portal biedt een **uitvoeren** knop waarmee u kunt doen sommige testen beperkt.</span><span class="sxs-lookup"><span data-stu-id="14cca-183">The portal provides a **Run** button that you can use to do some limited testing.</span></span> <span data-ttu-id="14cca-184">U kunt een aanvraaginhoud opgeven met behulp van de knop, maar u kan bieden queryreeksparameters of bijwerken van de aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="14cca-184">You can provide a request body by using the button, but you can't provide query string parameters or update request headers.</span></span>

<span data-ttu-id="14cca-185">Testen van de HTTP-trigger-functie die we eerder hebben gemaakt door het toevoegen van een JSON-tekenreeks die vergelijkbaar is met het volgende in de **aanvraagtekst** veld.</span><span class="sxs-lookup"><span data-stu-id="14cca-185">Test the HTTP trigger function we created earlier by adding a JSON string similar to the following in the **Request body** field.</span></span> <span data-ttu-id="14cca-186">Klik vervolgens op de **uitvoeren** knop.</span><span class="sxs-lookup"><span data-stu-id="14cca-186">Then click the **Run** button.</span></span>

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

<span data-ttu-id="14cca-187">In de portal **logboeken** venster uitvoer lijkt op de volgende wordt vastgelegd in de functie wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="14cca-187">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T08:03:12  Welcome, you are now connected to log-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a><span data-ttu-id="14cca-188">Testen met een timertrigger</span><span class="sxs-lookup"><span data-stu-id="14cca-188">Test with a timer trigger</span></span>
<span data-ttu-id="14cca-189">Sommige functies kunnen niet correct worden getest met de hulpprogramma's die eerder is vermeld.</span><span class="sxs-lookup"><span data-stu-id="14cca-189">Some functions can't be adequately tested with the tools mentioned previously.</span></span> <span data-ttu-id="14cca-190">Neem bijvoorbeeld een wachtrij trigger-functie die wordt uitgevoerd als er een bericht is verwijderd in [Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="14cca-190">For example, consider a queue trigger function that runs when a message is dropped into [Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="14cca-191">U kunt altijd code schrijven voor het verwijderen van een bericht in de wachtrij en een voorbeeld hiervan in een consoleproject verderop in dit artikel wordt aangeboden.</span><span class="sxs-lookup"><span data-stu-id="14cca-191">You can always write code to drop a message into your queue, and an example of this in a console project is provided later in this article.</span></span> <span data-ttu-id="14cca-192">Er is echter een andere benadering die kunt u functies rechtstreeks te testen.</span><span class="sxs-lookup"><span data-stu-id="14cca-192">However, there is another approach you can use that tests functions directly.</span></span>  

<span data-ttu-id="14cca-193">U kunt een timertrigger geconfigureerd met een wachtrij uitvoer van de binding.</span><span class="sxs-lookup"><span data-stu-id="14cca-193">You can use a timer trigger configured with a queue output binding.</span></span> <span data-ttu-id="14cca-194">Die code van de trigger timer kunt vervolgens de testberichten schrijven naar de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="14cca-194">That timer trigger code can then write the test messages to the queue.</span></span> <span data-ttu-id="14cca-195">Deze sectie wordt een voorbeeld uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="14cca-195">This section walks through an example.</span></span>

<span data-ttu-id="14cca-196">Zie voor meer gedetailleerde informatie over het gebruik van bindingen met Azure Functions, de [naslaginformatie voor ontwikkelaars van Azure Functions](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="14cca-196">For more in-depth information on using bindings with Azure Functions, see the [Azure Functions developer reference](functions-reference.md).</span></span>

#### <a name="create-a-queue-trigger-for-testing"></a><span data-ttu-id="14cca-197">Maken van een wachtrij-trigger voor het testen</span><span class="sxs-lookup"><span data-stu-id="14cca-197">Create a queue trigger for testing</span></span>
<span data-ttu-id="14cca-198">Om te demonstreren deze benadering, maken we eerst een wachtrij-activeringsfunctie die we voor een wachtrij met de naam wilt testen `queue-newusers`.</span><span class="sxs-lookup"><span data-stu-id="14cca-198">To demonstrate this approach, we first create a queue trigger function that we want to test for a queue named `queue-newusers`.</span></span> <span data-ttu-id="14cca-199">Deze functie verwerkt naam en adres informatie verwijderd in de wachtrij opslag voor een nieuwe gebruiker.</span><span class="sxs-lookup"><span data-stu-id="14cca-199">This function processes name and address information dropped into Queue storage for a new user.</span></span>

> [!NOTE]
> <span data-ttu-id="14cca-200">Als u de naam van een andere wachtrij gebruikt, zorg ervoor dat de naam die u gebruikt voldoet aan de [naamgeving van wachtrijen en metagegevens](https://msdn.microsoft.com/library/dd179349.aspx) regels.</span><span class="sxs-lookup"><span data-stu-id="14cca-200">If you use a different queue name, make sure the name you use conforms to the [Naming Queues and MetaData](https://msdn.microsoft.com/library/dd179349.aspx) rules.</span></span> <span data-ttu-id="14cca-201">Anders kunt u een foutmelding krijgt.</span><span class="sxs-lookup"><span data-stu-id="14cca-201">Otherwise, you get an error.</span></span>
>
>

1. <span data-ttu-id="14cca-202">In de [Azure-portal] voor functie-app klikt u op **nieuwe functie** > **QueueTrigger - C#**.</span><span class="sxs-lookup"><span data-stu-id="14cca-202">In the [Azure portal] for your function app, click **New Function** > **QueueTrigger - C#**.</span></span>
2. <span data-ttu-id="14cca-203">Voer de naam van de wachtrij moeten worden bewaakt door de functie van de wachtrij:</span><span class="sxs-lookup"><span data-stu-id="14cca-203">Enter the queue name to be monitored by the queue function:</span></span>

        queue-newusers
3. <span data-ttu-id="14cca-204">Klik op de  **+**  knop om te selecteren of maken van het opslagaccount dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="14cca-204">Click the **+** button to select or create the storage account you want to use.</span></span> <span data-ttu-id="14cca-205">Klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="14cca-205">Then click **Create**.</span></span>
4. <span data-ttu-id="14cca-206">Laat deze portal browservenster geopend, zodat u de logboekvermeldingen voor de standaard wachtrij functiecode sjabloon kunt bewaken.</span><span class="sxs-lookup"><span data-stu-id="14cca-206">Leave this portal browser window open, so you can monitor the log entries for the default queue function template code.</span></span>

#### <a name="create-a-timer-trigger-to-drop-a-message-in-the-queue"></a><span data-ttu-id="14cca-207">Een timertrigger voor het verwijderen van een bericht in de wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="14cca-207">Create a timer trigger to drop a message in the queue</span></span>
1. <span data-ttu-id="14cca-208">Open de [Azure-portal] in een nieuw browservenster en navigeer naar de functie-app.</span><span class="sxs-lookup"><span data-stu-id="14cca-208">Open the [Azure portal] in a new browser window, and navigate to your function app.</span></span>
2. <span data-ttu-id="14cca-209">Klik op **nieuwe functie** > **TimerTrigger - C#**.</span><span class="sxs-lookup"><span data-stu-id="14cca-209">Click **New Function** > **TimerTrigger - C#**.</span></span> <span data-ttu-id="14cca-210">Voer een expressie cron om in te stellen hoe vaak de timer-code wordt de functie van uw wachtrij getest.</span><span class="sxs-lookup"><span data-stu-id="14cca-210">Enter a cron expression to set how often the timer code tests your queue function.</span></span> <span data-ttu-id="14cca-211">Klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="14cca-211">Then click **Create**.</span></span> <span data-ttu-id="14cca-212">Als u wilt dat de test uitgevoerd elke 30 seconden, kunt u de volgende [CRON expressie](https://wikipedia.org/wiki/Cron#CRON_expression):</span><span class="sxs-lookup"><span data-stu-id="14cca-212">If you want the test to run every 30 seconds, you can use the following [CRON expression](https://wikipedia.org/wiki/Cron#CRON_expression):</span></span>

        */30 * * * * *
3. <span data-ttu-id="14cca-213">Klik op de **integreren** tabblad voor de nieuwe timertrigger.</span><span class="sxs-lookup"><span data-stu-id="14cca-213">Click the **Integrate** tab for your new timer trigger.</span></span>
4. <span data-ttu-id="14cca-214">Onder **uitvoer**, klikt u op **+ nieuw uitvoer**.</span><span class="sxs-lookup"><span data-stu-id="14cca-214">Under **Output**, click **+ New Output**.</span></span> <span data-ttu-id="14cca-215">Klik vervolgens op **wachtrij** en **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="14cca-215">Then click **queue** and **Select**.</span></span>
5. <span data-ttu-id="14cca-216">Opmerking van de naam die u gebruikt voor de **bericht wachtrijobject**.</span><span class="sxs-lookup"><span data-stu-id="14cca-216">Note the name you use for the **queue message object**.</span></span> <span data-ttu-id="14cca-217">U gebruikt dit in de code van de functie timer.</span><span class="sxs-lookup"><span data-stu-id="14cca-217">You use this in the timer function code.</span></span>

        myQueue
6. <span data-ttu-id="14cca-218">Voer de naam van de wachtrij waarin het bericht wordt verzonden:</span><span class="sxs-lookup"><span data-stu-id="14cca-218">Enter the queue name where the message is sent:</span></span>

        queue-newusers
7. <span data-ttu-id="14cca-219">Klik op de  **+**  knop om te selecteren van het opslagaccount dat u eerder hebt gebruikt met de wachtrij-trigger.</span><span class="sxs-lookup"><span data-stu-id="14cca-219">Click the **+** button to select the storage account you used previously with the queue trigger.</span></span> <span data-ttu-id="14cca-220">Klik vervolgens op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="14cca-220">Then click **Save**.</span></span>
8. <span data-ttu-id="14cca-221">Klik op de **ontwikkelen** tabblad voor de timertrigger.</span><span class="sxs-lookup"><span data-stu-id="14cca-221">Click the **Develop** tab for your timer trigger.</span></span>
9. <span data-ttu-id="14cca-222">Als u de dezelfde wachtrij bericht objectnaam hierboven hebt gebruikt, kunt u de volgende code voor de functie C#-timer.</span><span class="sxs-lookup"><span data-stu-id="14cca-222">You can use the following code for the C# timer function, as long as you used the same queue message object name shown earlier.</span></span> <span data-ttu-id="14cca-223">Klik vervolgens op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="14cca-223">Then click **Save**.</span></span>

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

<span data-ttu-id="14cca-224">De C# timerfunctie wordt op dit punt wordt elke 30 seconden uitgevoerd als u de voorbeeld-cron-expressie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="14cca-224">At this point, the C# timer function executes every 30 seconds if you used the example cron expression.</span></span> <span data-ttu-id="14cca-225">De logboeken voor de timerfunctie report elke uitvoering:</span><span class="sxs-lookup"><span data-stu-id="14cca-225">The logs for the timer function report each execution:</span></span>

    2016-03-24T10:27:02  Welcome, you are now connected to log-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

<span data-ttu-id="14cca-226">In het browservenster voor de wachtrij-functie ziet u elk bericht wordt verwerkt:</span><span class="sxs-lookup"><span data-stu-id="14cca-226">In the browser window for the queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected to log-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a><span data-ttu-id="14cca-227">Testen van een functie met code</span><span class="sxs-lookup"><span data-stu-id="14cca-227">Test a function with code</span></span>
<span data-ttu-id="14cca-228">U wilt maken van een externe toepassing of het framework voor het testen van uw functies.</span><span class="sxs-lookup"><span data-stu-id="14cca-228">You may need to create an external application or framework to test your functions.</span></span>

### <a name="test-an-http-trigger-function-with-code-nodejs"></a><span data-ttu-id="14cca-229">Testen van een HTTP-trigger-functie met code: Node.js</span><span class="sxs-lookup"><span data-stu-id="14cca-229">Test an HTTP trigger function with code: Node.js</span></span>
<span data-ttu-id="14cca-230">Een Node.js-app kunt u een HTTP-aanvraag voor het testen van uw functie uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="14cca-230">You can use a Node.js app to execute an HTTP request to test your function.</span></span>
<span data-ttu-id="14cca-231">Controleer of in te stellen:</span><span class="sxs-lookup"><span data-stu-id="14cca-231">Make sure to set:</span></span>

* <span data-ttu-id="14cca-232">De `host` in de aanvraag-opties voor de functie app-host.</span><span class="sxs-lookup"><span data-stu-id="14cca-232">The `host` in the request options to your function app host.</span></span>
* <span data-ttu-id="14cca-233">De functienaam in de `path`.</span><span class="sxs-lookup"><span data-stu-id="14cca-233">Your function name in the `path`.</span></span>
* <span data-ttu-id="14cca-234">Uw toegangscode (`<your code>`) in de `path`.</span><span class="sxs-lookup"><span data-stu-id="14cca-234">Your access code (`<your code>`) in the `path`.</span></span>

<span data-ttu-id="14cca-235">Codevoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="14cca-235">Code example:</span></span>

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


<span data-ttu-id="14cca-236">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="14cca-236">Output:</span></span>

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    The address you provided is Dallas, T.X. 75201

<span data-ttu-id="14cca-237">In de portal **logboeken** venster uitvoer lijkt op de volgende wordt vastgelegd in de functie wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="14cca-237">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T08:08:55  Welcome, you are now connected to log-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a><span data-ttu-id="14cca-238">Testen van een functie van de trigger wachtrij met code: C#</span><span class="sxs-lookup"><span data-stu-id="14cca-238">Test a queue trigger function with code: C#</span></span> #
<span data-ttu-id="14cca-239">Eerder vermeld dat u een trigger wachtrij testen kunt met code verwijderen van een bericht in de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="14cca-239">We mentioned earlier that you can test a queue trigger by using code to drop a message in your queue.</span></span> <span data-ttu-id="14cca-240">De volgende voorbeeldcode is gebaseerd op de C#-code die zijn gepresenteerd in de [aan de slag met Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="14cca-240">The following example code is based on the C# code presented in the [Getting started with Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md) tutorial.</span></span> <span data-ttu-id="14cca-241">Code voor andere talen is ook beschikbaar via deze koppeling.</span><span class="sxs-lookup"><span data-stu-id="14cca-241">Code for other languages is also available from that link.</span></span>

<span data-ttu-id="14cca-242">Test deze code in een console-app, moet u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="14cca-242">To test this code in a console app, you must:</span></span>

* <span data-ttu-id="14cca-243">[De opslagverbindingsreeks configureren in het bestand app.config](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="14cca-243">[Configure your storage connection string in the app.config file](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>
* <span data-ttu-id="14cca-244">Geeft een `name` en `address` als parameters naar de app.</span><span class="sxs-lookup"><span data-stu-id="14cca-244">Pass a `name` and `address` as parameters to the app.</span></span> <span data-ttu-id="14cca-245">Bijvoorbeeld `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span><span class="sxs-lookup"><span data-stu-id="14cca-245">For example, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span></span> <span data-ttu-id="14cca-246">(Deze code accepteert de naam en adres voor een nieuwe gebruiker als opdrachtregelargumenten tijdens runtime.)</span><span class="sxs-lookup"><span data-stu-id="14cca-246">(This code accepts the name and address for a new user as command-line arguments during runtime.)</span></span>

<span data-ttu-id="14cca-247">Van C#-voorbeeldcode:</span><span class="sxs-lookup"><span data-stu-id="14cca-247">Example C# code:</span></span>

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

    // Create the queue client
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

    // Retrieve a reference to a queue
    CloudQueue queue = queueClient.GetQueueReference(queueName);

    // Create the queue if it doesn't already exist
    queue.CreateIfNotExists();

    // Create a message and add it to the queue.
    if (name != null)
    {
        if (address != null)
            JSON = String.Format("{{\"name\":\"{0}\",\"address\":\"{1}\"}}", name, address);
        else
            JSON = String.Format("{{\"name\":\"{0}\"}}", name);
    }

    Console.WriteLine("Adding message to " + queueName + "...");
    Console.WriteLine(JSON);

    CloudQueueMessage message = new CloudQueueMessage(JSON);
    queue.AddMessage(message);
}
```

<span data-ttu-id="14cca-248">In het browservenster voor de wachtrij-functie ziet u elk bericht wordt verwerkt:</span><span class="sxs-lookup"><span data-stu-id="14cca-248">In the browser window for the queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected to log-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[Azure-portal]: https://portal.azure.com
