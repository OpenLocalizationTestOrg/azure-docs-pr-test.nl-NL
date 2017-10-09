### <a name="create-a-nodejs-application"></a><span data-ttu-id="8192e-101">Een Node.js-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="8192e-101">Create a Node.js application</span></span>

<span data-ttu-id="8192e-102">Maak een nieuw JavaScript-bestand met de naam `sender.js`.</span><span class="sxs-lookup"><span data-stu-id="8192e-102">Create a new JavaScript file called `sender.js`.</span></span>

### <a name="add-hello-relay-npm-package"></a><span data-ttu-id="8192e-103">Hallo Relay NPM pakket toevoegen</span><span class="sxs-lookup"><span data-stu-id="8192e-103">Add hello Relay NPM package</span></span>

<span data-ttu-id="8192e-104">Voer `npm install hyco-ws` uit vanaf een Node-opdrachtprompt in de projectmap.</span><span class="sxs-lookup"><span data-stu-id="8192e-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-toosend-messages"></a><span data-ttu-id="8192e-105">Code schrijven toosend berichten</span><span class="sxs-lookup"><span data-stu-id="8192e-105">Write some code toosend messages</span></span>

1. <span data-ttu-id="8192e-106">Voeg de volgende Hallo `constants` toohello bovenaan Hallo `sender.js` bestand.</span><span class="sxs-lookup"><span data-stu-id="8192e-106">Add hello following `constants` toohello top of hello `sender.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. <span data-ttu-id="8192e-107">Toevoegen van de volgende constanten toohello hello `sender.js` bestand voor meer informatie Hallo hybride verbinding.</span><span class="sxs-lookup"><span data-stu-id="8192e-107">Add hello following constants toohello `sender.js` file for hello hybrid connection details.</span></span> <span data-ttu-id="8192e-108">Tijdelijke aanduidingen Hallo haakjes vervangen door Hallo-waarden die u hebt verkregen tijdens het Hallo hybride verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="8192e-108">Replace hello placeholders in brackets with hello values you obtained when you created hello hybrid connection.</span></span>
   
   1. <span data-ttu-id="8192e-109">`const ns`-Hallo Relay-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="8192e-109">`const ns` - hello Relay namespace.</span></span> <span data-ttu-id="8192e-110">Ervoor toouse Hallo naamruimte volledig gekwalificeerde naam; bijvoorbeeld: `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="8192e-110">Be sure toouse hello fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="8192e-111">`const path`-de naam Hallo van Hallo hybride verbinding.</span><span class="sxs-lookup"><span data-stu-id="8192e-111">`const path` - hello name of hello hybrid connection.</span></span>
   3. <span data-ttu-id="8192e-112">`const keyrule`-naam op Hallo van Hallo SAS-sleutel.</span><span class="sxs-lookup"><span data-stu-id="8192e-112">`const keyrule` - hello name of hello SAS key.</span></span>
   4. <span data-ttu-id="8192e-113">`const key`-Hallo SAS-sleutelwaarde.</span><span class="sxs-lookup"><span data-stu-id="8192e-113">`const key` - hello SAS key value.</span></span>

3. <span data-ttu-id="8192e-114">Hallo na code toohello toevoegen `sender.js` bestand:</span><span class="sxs-lookup"><span data-stu-id="8192e-114">Add hello following code toohello `sender.js` file:</span></span>
   
    ```js
    WebSocket.relayedConnect(
        WebSocket.createRelaySendUri(ns, path),
        WebSocket.createRelayToken('http://'+ns, keyrule, key),
        function (wss) {
            readline.on('line', (input) => {
                wss.send(input, null);
            });
   
            console.log('Started client interval.');
            wss.on('close', function () {
                console.log('stopping client interval');
                process.exit();
            });
        }
    );
    ```
    <span data-ttu-id="8192e-115">Het bestand sender.js moet er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="8192e-115">Here is what your sender.js file should look like:</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    WebSocket.relayedConnect(
        WebSocket.createRelaySendUri(ns, path),
        WebSocket.createRelayToken('http://'+ns, keyrule, key),
        function (wss) {
            readline.on('line', (input) => {
                wss.send(input, null);
            });
   
            console.log('Started client interval.');
            wss.on('close', function () {
                console.log('stopping client interval');
                process.exit();
            });
        }
    );
    ```

