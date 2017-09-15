### <a name="create-a-nodejs-application"></a><span data-ttu-id="62083-101">Een Node.js-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="62083-101">Create a Node.js application</span></span>

<span data-ttu-id="62083-102">Maak een nieuw JavaScript-bestand met de naam `listener.js`.</span><span class="sxs-lookup"><span data-stu-id="62083-102">Create a new JavaScript file called `listener.js`.</span></span>

### <a name="add-the-relay-npm-package"></a><span data-ttu-id="62083-103">Het pakket Relay NPM toevoegen</span><span class="sxs-lookup"><span data-stu-id="62083-103">Add the Relay NPM package</span></span>

<span data-ttu-id="62083-104">Voer `npm install hyco-ws` uit vanaf een Node-opdrachtprompt in de projectmap.</span><span class="sxs-lookup"><span data-stu-id="62083-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-to-receive-messages"></a><span data-ttu-id="62083-105">Code schrijven om berichten te ontvangen</span><span class="sxs-lookup"><span data-stu-id="62083-105">Write some code to receive messages</span></span>

1. <span data-ttu-id="62083-106">Voeg de volgende constante toe aan het begin van het bestand `listener.js`.</span><span class="sxs-lookup"><span data-stu-id="62083-106">Add the following constant to the top of the `listener.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. <span data-ttu-id="62083-107">Voeg de volgende constanten toe aan het bestand `listener.js` voor de gegevens van de hybride verbinding.</span><span class="sxs-lookup"><span data-stu-id="62083-107">Add the following constants to the `listener.js` file for the hybrid connection details.</span></span> <span data-ttu-id="62083-108">Vervang de tijdelijke aanduidingen tussen punthaken door de waarden die u hebt verkregen bij het maken van de hybride verbinding.</span><span class="sxs-lookup"><span data-stu-id="62083-108">Replace the placeholders in brackets with the values you obtained when you created the hybrid connection.</span></span>
   
   1. <span data-ttu-id="62083-109">`const ns`: de Relay-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="62083-109">`const ns` - The Relay namespace.</span></span> <span data-ttu-id="62083-110">Zorg ervoor dat u de volledig gekwalificeerde naamruimte gebruikt, bijvoorbeeld `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="62083-110">Be sure to use the fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="62083-111">`const path`: de naam van de hybride verbinding.</span><span class="sxs-lookup"><span data-stu-id="62083-111">`const path` - The name of the hybrid connection.</span></span>
   3. <span data-ttu-id="62083-112">`const keyrule`: de naam van de SAS-sleutel.</span><span class="sxs-lookup"><span data-stu-id="62083-112">`const keyrule` - The name of the SAS key.</span></span>
   4. <span data-ttu-id="62083-113">`const key`: de waarde van de SAS-sleutel.</span><span class="sxs-lookup"><span data-stu-id="62083-113">`const key` - The SAS key value.</span></span>

3. <span data-ttu-id="62083-114">Voeg de volgende code toe aan het bestand `listener.js`:</span><span class="sxs-lookup"><span data-stu-id="62083-114">Add the following code to the `listener.js` file:</span></span>
   
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
    <span data-ttu-id="62083-115">Zo zou het bestand listener.js er moeten uitzien:</span><span class="sxs-lookup"><span data-stu-id="62083-115">Here is what your listener.js file should look like:</span></span>
   
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

