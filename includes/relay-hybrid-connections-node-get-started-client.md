### <a name="create-a-nodejs-application"></a><span data-ttu-id="afe5d-101">Een Node.js-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="afe5d-101">Create a Node.js application</span></span>

<span data-ttu-id="afe5d-102">Maak een nieuw JavaScript-bestand met de naam `sender.js`.</span><span class="sxs-lookup"><span data-stu-id="afe5d-102">Create a new JavaScript file called `sender.js`.</span></span>

### <a name="add-the-relay-npm-package"></a><span data-ttu-id="afe5d-103">Het pakket Relay NPM toevoegen</span><span class="sxs-lookup"><span data-stu-id="afe5d-103">Add the Relay NPM package</span></span>

<span data-ttu-id="afe5d-104">Voer `npm install hyco-ws` uit vanaf een Node-opdrachtprompt in de projectmap.</span><span class="sxs-lookup"><span data-stu-id="afe5d-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-to-send-messages"></a><span data-ttu-id="afe5d-105">Code schrijven om berichten te verzenden</span><span class="sxs-lookup"><span data-stu-id="afe5d-105">Write some code to send messages</span></span>

1. <span data-ttu-id="afe5d-106">Plaats de volgende `constants` boven aan het bestand `sender.js`.</span><span class="sxs-lookup"><span data-stu-id="afe5d-106">Add the following `constants` to the top of the `sender.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. <span data-ttu-id="afe5d-107">Voeg de volgende constanten toe aan het bestand `sender.js` voor de gegevens van de hybride verbinding.</span><span class="sxs-lookup"><span data-stu-id="afe5d-107">Add the following constants to the `sender.js` file for the hybrid connection details.</span></span> <span data-ttu-id="afe5d-108">Vervang de tijdelijke aanduidingen tussen punthaken door de waarden die u hebt verkregen bij het maken van de hybride verbinding.</span><span class="sxs-lookup"><span data-stu-id="afe5d-108">Replace the placeholders in brackets with the values you obtained when you created the hybrid connection.</span></span>
   
   1. <span data-ttu-id="afe5d-109">`const ns`: de Relay-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="afe5d-109">`const ns` - The Relay namespace.</span></span> <span data-ttu-id="afe5d-110">Zorg ervoor dat u de volledig gekwalificeerde naamruimte gebruikt, bijvoorbeeld `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="afe5d-110">Be sure to use the fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="afe5d-111">`const path`: de naam van de hybride verbinding.</span><span class="sxs-lookup"><span data-stu-id="afe5d-111">`const path` - The name of the hybrid connection.</span></span>
   3. <span data-ttu-id="afe5d-112">`const keyrule`: de naam van de SAS-sleutel.</span><span class="sxs-lookup"><span data-stu-id="afe5d-112">`const keyrule` - The name of the SAS key.</span></span>
   4. <span data-ttu-id="afe5d-113">`const key`: de waarde van de SAS-sleutel.</span><span class="sxs-lookup"><span data-stu-id="afe5d-113">`const key` - The SAS key value.</span></span>

3. <span data-ttu-id="afe5d-114">Voeg de volgende code toe aan het bestand `sender.js`:</span><span class="sxs-lookup"><span data-stu-id="afe5d-114">Add the following code to the `sender.js` file:</span></span>
   
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
    <span data-ttu-id="afe5d-115">Het bestand sender.js moet er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="afe5d-115">Here is what your sender.js file should look like:</span></span>
   
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

