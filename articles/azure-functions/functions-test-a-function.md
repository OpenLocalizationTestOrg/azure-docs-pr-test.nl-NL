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
# <a name="strategies-for-testing-your-code-in-azure-functions"></a>Strategieën voor het testen van uw code in Azure Functions

Dit onderwerp wordt beschreven Hallo verschillende manieren tootest-functies, inclusief het gebruik van de volgende algemene Hallo nadert:

+ HTTP-gebaseerde hulpprogramma's, zoals cURL Postman en zelfs een webbrowser voor triggers voor webgebaseerde
+ Azure Opslagverkenner tootest op basis van een Azure Storage-triggers
+ Tabblad testresultaten in hello Azure Functions-portal
+ Functie Timer geactiveerd
+ Testen van de toepassing of framework

Al deze methoden testen een HTTP-trigger functie gebruiken die invoer via een accepteert query-tekenreeks parameter of Hallo aanvraagtekst. U kunt deze functie maken in de eerste sectie Hallo.

## <a name="create-a-function-for-testing"></a>Maak een functie voor het testen
Voor de meeste van deze zelfstudie gebruiken we een enigszins gewijzigde versie Hallo HttpTrigger JavaScript-sjabloon voor de functie die beschikbaar is wanneer u een functie. Als u informatie over het maken van een functie nodig, Bekijk dit [zelfstudie](functions-create-first-azure-function.md). Kies Hallo **HttpTrigger - JavaScript** sjabloon bij het maken van de functie test Hallo in Hallo [Azure-portal].

Hallo functie standaardsjabloon is in feite een "Hallo wereld" functie die echo back Hallo-naam van Hallo aanvraag hoofdtekst of de query tekenreeksparameter `name=<your name>`.  Hallo code ontvangt updates tooalso kunt u tooprovide Hallo naam en een adres als JSON-inhoud in de aanvraagtekst Hallo. Hallo functie echo vervolgens deze client back toohello indien beschikbaar.   

Hallo-functie met de volgende code, die zullen worden gebruikt voor het testen van Hallo bijwerken:

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

## <a name="test-a-function-with-tools"></a>Een functie met hulpprogramma's testen
Buiten hello Azure-portal zijn er verschillende hulpprogramma's waarmee u tootrigger uw functies voor het testen kunt. Het gaat hierbij om HTTP-hulpprogramma's (zowel gebruikersinterface gebaseerde als command line), programma's voor Azure Storage-toegang en zelfs een eenvoudige webbrowser testen.

### <a name="test-with-a-browser"></a>Testen met een browser
Hallo-webbrowser is een eenvoudige manier tootrigger functies via HTTP. U kunt een browser gebruiken voor GET-aanvragen die niet te worden een nettolading in de hoofdtekst hoeven en dat gebruik alleen een query tekenreeksparameters.

tootest hello functie we eerder hebt gedefinieerd, kopie Hallo **Function Url** van Hallo-portal. Hallo volgende vorm heeft:

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

Hallo toevoegen `name` parameter toohello query-tekenreeks. Werkelijke bestandsnaam Hallo `<Enter a name here>` tijdelijke aanduiding.

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

Hallo-URL plakken in uw browser en u krijgt een reactie vergelijkbaar toohello volgende.

![Schermopname van Chrome browsertabblad met de reactie van de test](./media/functions-test-a-function/browser-test.png)

In dit voorbeeld is de Chrome-browser hello, die geschikt is voor Hallo tekenreeks geretourneerd in XML. Andere browsers weergeven NET Hallo string-waarde.

In de portal Hallo **logboeken** venster uitvoer vergelijkbare toohello volgende wordt vastgelegd in het Hallo-functie wordt uitgevoerd:

    2016-03-23T07:34:59  Welcome, you are now connected toolog-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a>Testen met Postman
Hallo aanbevolen hulpprogramma tootest het merendeel van uw functies is Postman die kan worden geïntegreerd met Hallo Chrome-browser. tooinstall Postman, Zie [Postman ophalen](https://www.getpostman.com/). Postman biedt controle over veel meer kenmerken van een HTTP-aanvraag.

> [!TIP]
> Hallo HTTP-test hulpprogramma dat u meest vertrouwd met bent gebruiken. Hier volgen enkele tooPostman alternatieven:  
>
> * [Fiddler](http://www.telerik.com/fiddler)  
> * [Paw](https://luckymarmot.com/paw)  
>
>

tootest Hallo-functie met een aanvraagtekst in Postman:

1. Postman starten vanuit Hallo **Apps** knop in Hallo linkerbovenhoek van een Chrome-browservenster.
2. Kopieer uw **Function Url**, en plak deze in Postman. Het bevat Hallo toegangscode querytekenreeksparameter.
3. Hallo HTTP-methode te wijzigen**POST**.
4. Klik op **hoofdtekst** > **onbewerkte**, en voeg een JSON-aanvraag hoofdtekst vergelijkbare toohello volgende:

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. Klik op **verzenden**.

Hallo ziet volgende afbeelding u testen Hallo eenvoudige echo functie voorbeeld in deze zelfstudie.

![Schermopname van Postman-gebruikersinterface](./media/functions-test-a-function/postman-test.png)

In de portal Hallo **logboeken** venster uitvoer vergelijkbare toohello volgende wordt vastgelegd in het Hallo-functie wordt uitgevoerd:

    2016-03-23T08:04:51  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-hello-command-line"></a>Testen met cURL vanaf de opdrachtregel Hallo
Vaak wanneer u software test, is het niet nodig toolook ieder verder dan Hallo opdrachtregel toohelp foutopsporing van uw toepassing. Dit gaat niet anders zijn met het testen van functies. Houd er rekening mee dat cURL Hallo op Linux gebaseerde systemen standaard beschikbaar is. In Windows, moet u eerst downloaden en installeren van Hallo [cURL hulpprogramma](https://curl.haxx.se/).

tootest hello functie dat we eerder hebt gedefinieerd, kopie Hallo **Function URL** van Hallo-portal. Hallo volgende vorm heeft:

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

Dit is Hallo-URL voor activering van de functie. Dit testen met behulp van Hallo cURL-opdracht op Hallo opdrachtregel toomake een GET (`-G` of `--get`)-aanvraag in voor de functie Hallo:

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

Dit voorbeeld vereist een queryreeksparameter als gegevens kan worden doorgegeven (`-d`) in Hallo cURL-opdracht:

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

Voer Hallo-opdracht, en u ziet Hallo na de uitvoer van de functie Hallo op Hallo-opdrachtregel:

![Schermopname van opdrachtprompt uitvoer](./media/functions-test-a-function/curl-test.png)

In de portal Hallo **logboeken** venster uitvoer vergelijkbare toohello volgende wordt vastgelegd in het Hallo-functie wordt uitgevoerd:

    2016-04-05T21:55:09  Welcome, you are now connected toolog-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a>Een blob-trigger testen met behulp van Opslagverkenner
U kunt een blob-activeringsfunctie testen met behulp van [Azure Opslagverkenner](http://storageexplorer.com/).

1. In Hallo [Azure-portal] maken voor uw app functie activeringsfunctie voor C#, F # of JavaScript-blob. Hallo toomonitor toohello padnaam van uw blob-container instellen. Bijvoorbeeld:

        files
2. Klik op Hallo  **+**  tooselect knop of Hallo gewenste toouse storage-account maken. Klik vervolgens op **Maken**.
3. Maak een tekstbestand met de volgende tekst hello en sla het:

        A text file for blob trigger function testing.
4. Voer [Azure Opslagverkenner](http://storageexplorer.com/), en maak verbinding toohello blob-container in Hallo storage-account wordt bewaakt.
5. Klik op **uploaden** tooupload Hallo-tekstbestand.

    ![Schermopname van Opslagverkenner](./media/functions-test-a-function/azure-storage-explorer-test.png)

Hallo standaard blob-activeringscode functie rapporten Hallo verwerking van Hallo blob in Hallo Logboeken:

    2016-03-24T11:30:10  Welcome, you are now connected toolog-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a>Een functie binnen functies testen
Hello Azure Functions-portal is ontworpen toolet testen van HTTP- en timer functies geactiveerd. U kunt functies tootrigger ook andere functies die u wilt testen maken.

### <a name="test-with-hello-functions-portal-run-button"></a>Testen met de knop portal uitvoeren functies Hallo
Hallo-portal biedt een **uitvoeren** knop waarmee u toodo sommige kunt beperkt testen. U kunt een aanvraaginhoud opgeven met behulp van de knop hello, maar u kan bieden queryreeksparameters of bijwerken van de aanvraagheaders.

Hallo HTTP-activeringsfunctie we eerder hebben gemaakt door een JSON-tekenreeks vergelijkbare toohello na toe te voegen in Hallo testen **aanvraagtekst** veld. Klik vervolgens op Hallo **uitvoeren** knop.

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

In de portal Hallo **logboeken** venster uitvoer vergelijkbare toohello volgende wordt vastgelegd in het Hallo-functie wordt uitgevoerd:

    2016-03-23T08:03:12  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a>Testen met een timertrigger
Sommige functies kunnen niet correct worden getest met Hallo-hulpprogramma's die eerder is vermeld. Neem bijvoorbeeld een wachtrij trigger-functie die wordt uitgevoerd als er een bericht is verwijderd in [Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md). U kunt altijd schrijven code toodrop een bericht in de wachtrij en een voorbeeld hiervan in een consoleproject verderop in dit artikel wordt aangeboden. Er is echter een andere benadering die kunt u functies rechtstreeks te testen.  

U kunt een timertrigger geconfigureerd met een wachtrij uitvoer van de binding. Dat timer activeringscode Hallo test berichten toohello wachtrij vervolgens schrijven kunt. Deze sectie wordt een voorbeeld uitgelegd.

Zie voor meer gedetailleerde informatie over het gebruik van bindingen met Azure Functions Hallo [naslaginformatie voor ontwikkelaars van Azure Functions](functions-reference.md).

#### <a name="create-a-queue-trigger-for-testing"></a>Maken van een wachtrij-trigger voor het testen
toodemonstrate deze benadering eerst maken we een wachtrij trigger-functie die we tootest voor een wachtrij met de naam willen `queue-newusers`. Deze functie verwerkt naam en adres informatie verwijderd in de wachtrij opslag voor een nieuwe gebruiker.

> [!NOTE]
> Als u de naam van een andere wachtrij gebruikt, controleert u of Hallo-naam die u gebruikt voldoet toohello [naamgeving van wachtrijen en metagegevens](https://msdn.microsoft.com/library/dd179349.aspx) regels. Anders kunt u een foutmelding krijgt.
>
>

1. In Hallo [Azure-portal] voor functie-app klikt u op **nieuwe functie** > **QueueTrigger - C#**.
2. Voer Hallo wachtrij naam toobe bewaakt door Hallo wachtrij functie:

        queue-newusers
3. Klik op Hallo  **+**  tooselect knop of Hallo gewenste toouse storage-account maken. Klik vervolgens op **Maken**.
4. Laat deze portal browservenster geopend, zodat u Hallo logboekvermeldingen voor Hallo wachtrij functie sjabloon standaardcode kunt bewaken.

#### <a name="create-a-timer-trigger-toodrop-a-message-in-hello-queue"></a>Een timer trigger toodrop van een bericht in Hallo wachtrij maken
1. Open Hallo [Azure-portal] in een nieuw browservenster en navigeer tooyour functie-app.
2. Klik op **nieuwe functie** > **TimerTrigger - C#**. Voer een expressie cron tooset hoe vaak hello timer code wordt getest uw wachtrij-functie. Klik vervolgens op **Maken**. Als u Hallo test toorun elke 30 seconden wilt, kunt u de volgende Hallo [CRON expressie](https://wikipedia.org/wiki/Cron#CRON_expression):

        */30 * * * * *
3. Klik op Hallo **integreren** tabblad voor de nieuwe timertrigger.
4. Onder **uitvoer**, klikt u op **+ nieuw uitvoer**. Klik vervolgens op **wachtrij** en **Selecteer**.
5. Opmerking Hallo die u voor Hallo gebruikt **bericht wachtrijobject**. U gebruikt dit in Hallo timer functiecode.

        myQueue
6. Voer Hallo wachtrijnaam, waarbij het Hallo-bericht wordt verzonden:

        queue-newusers
7. Klik op Hallo  **+**  knop tooselect Hallo storage-account die u eerder hebt gebruikt met Hallo wachtrij trigger. Klik vervolgens op **Opslaan**.
8. Klik op Hallo **ontwikkelen** tabblad voor de timertrigger.
9. Kunt u Hallo na de code voor de functie Hallo C#-timer, zolang u dezelfde wachtrij bericht objectnaam hierboven Hallo gebruikt. Klik vervolgens op **Opslaan**.

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

Hallo functie van C#-timer wordt op dit punt wordt elke 30 seconden uitgevoerd als u Hallo voorbeeld cron-expressie gebruikt. Hallo-logboeken voor de functie timer Hallo report elke uitvoering:

    2016-03-24T10:27:02  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

In het browservenster Hallo voor Hallo wachtrij functie ziet u elk bericht wordt verwerkt:

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a>Testen van een functie met code
Mogelijk moet u een externe toepassing of framework tootest toocreate uw functies.

### <a name="test-an-http-trigger-function-with-code-nodejs"></a>Testen van een HTTP-trigger-functie met code: Node.js
U kunt een Node.js-app tooexecute een HTTP-aanvraag tootest uw functie te gebruiken.
Zorg ervoor dat tooset:

* Hallo `host` in Hallo aanvraag opties tooyour functie app-host.
* De functienaam in Hallo `path`.
* Uw toegangscode (`<your code>`) in Hallo `path`.

Codevoorbeeld:

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


Uitvoer:

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    hello address you provided is Dallas, T.X. 75201

In de portal Hallo **logboeken** venster uitvoer vergelijkbare toohello volgende wordt vastgelegd in het Hallo-functie wordt uitgevoerd:

    2016-03-23T08:08:55  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a>Testen van een functie van de trigger wachtrij met code: C# #
Eerder vermeld dat u een trigger wachtrij testen kunt met behulp van code toodrop een bericht in de wachtrij. Hallo volgende voorbeeldcode is gebaseerd op Hallo C#-code die zijn gepresenteerd in Hallo [aan de slag met Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md) zelfstudie. Code voor andere talen is ook beschikbaar via deze koppeling.

tootest deze code in een console-app, moet u:

* [De opslagverbindingsreeks configureren in Hallo app.config-bestand](../storage/queues/storage-dotnet-how-to-use-queues.md).
* Geeft een `name` en `address` als parameters toohello app. Bijvoorbeeld `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`. (Deze code accepteert Hallo naam en adres voor een nieuwe gebruiker als opdrachtregelargumenten tijdens runtime.)

Van C#-voorbeeldcode:

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

In het browservenster Hallo voor Hallo wachtrij functie ziet u elk bericht wordt verwerkt:

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[Azure-portal]: https://portal.azure.com
