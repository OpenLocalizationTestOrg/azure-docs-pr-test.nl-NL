### <a name="create-a-nodejs-application"></a><span data-ttu-id="3b06e-101">Een Node.js-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="3b06e-101">Create a Node.js application</span></span>

<span data-ttu-id="3b06e-102">Maak een nieuw JavaScript-bestand met de naam `listener.js`.</span><span class="sxs-lookup"><span data-stu-id="3b06e-102">Create a new JavaScript file called `listener.js`.</span></span>

### <a name="add-hello-relay-npm-package"></a><span data-ttu-id="3b06e-103">Hallo Relay NPM pakket toevoegen</span><span class="sxs-lookup"><span data-stu-id="3b06e-103">Add hello Relay NPM package</span></span>

<span data-ttu-id="3b06e-104">Voer `npm install hyco-ws` uit vanaf een Node-opdrachtprompt in de projectmap.</span><span class="sxs-lookup"><span data-stu-id="3b06e-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-tooreceive-messages"></a><span data-ttu-id="3b06e-105">Code schrijven tooreceive berichten</span><span class="sxs-lookup"><span data-stu-id="3b06e-105">Write some code tooreceive messages</span></span>

1. <span data-ttu-id="3b06e-106">Toevoegen van de volgende constante toohello bovenaan Hallo Hallo `listener.js` bestand.</span><span class="sxs-lookup"><span data-stu-id="3b06e-106">Add hello following constant toohello top of hello `listener.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. <span data-ttu-id="3b06e-107">Toevoegen van de volgende constanten toohello hello `listener.js` bestand voor meer informatie Hallo hybride verbinding.</span><span class="sxs-lookup"><span data-stu-id="3b06e-107">Add hello following constants toohello `listener.js` file for hello hybrid connection details.</span></span> <span data-ttu-id="3b06e-108">Tijdelijke aanduidingen Hallo haakjes vervangen door Hallo-waarden die u hebt verkregen tijdens het Hallo hybride verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="3b06e-108">Replace hello placeholders in brackets with hello values you obtained when you created hello hybrid connection.</span></span>
   
   1. <span data-ttu-id="3b06e-109">`const ns`-Hallo Relay-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="3b06e-109">`const ns` - hello Relay namespace.</span></span> <span data-ttu-id="3b06e-110">Ervoor toouse Hallo naamruimte volledig gekwalificeerde naam; bijvoorbeeld: `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="3b06e-110">Be sure toouse hello fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="3b06e-111">`const path`-de naam Hallo van Hallo hybride verbinding.</span><span class="sxs-lookup"><span data-stu-id="3b06e-111">`const path` - hello name of hello hybrid connection.</span></span>
   3. <span data-ttu-id="3b06e-112">`const keyrule`-naam op Hallo van Hallo SAS-sleutel.</span><span class="sxs-lookup"><span data-stu-id="3b06e-112">`const keyrule` - hello name of hello SAS key.</span></span>
   4. <span data-ttu-id="3b06e-113">`const key`-Hallo SAS-sleutelwaarde.</span><span class="sxs-lookup"><span data-stu-id="3b06e-113">`const key` - hello SAS key value.</span></span>

3. <span data-ttu-id="3b06e-114">Hallo na code toohello toevoegen `listener.js` bestand:</span><span class="sxs-lookup"><span data-stu-id="3b06e-114">Add hello following code toohello `listener.js` file:</span></span>
   
    ```js
    var wss = WebSocket.createRelayedServer(
    {
        server : WebSocket.createRelayListenUri(ns, path),
        token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(event.data);
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```
    <span data-ttu-id="3b06e-115">Zo zou het bestand listener.js er moeten uitzien:</span><span class="sxs-lookup"><span data-stu-id="3b06e-115">Here is what your listener.js file should look like:</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    var wss = WebSocket.createRelayedServer(
        {
            server : WebSocket.createRelayListenUri(ns, path),
            token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
        }, 
        function (ws) {
            console.log('connection accepted');
            ws.onmessage = function (event) {
                console.log(event.data);
            };
            ws.on('close', function () {
                console.log('connection closed');
            });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```

