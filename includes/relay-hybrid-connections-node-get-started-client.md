### <a name="create-a-nodejs-application"></a>Een Node.js-toepassing maken

Maak een nieuw JavaScript-bestand met de naam `sender.js`.

### <a name="add-hello-relay-npm-package"></a>Hallo Relay NPM pakket toevoegen

Voer `npm install hyco-ws` uit vanaf een Node-opdrachtprompt in de projectmap.

### <a name="write-some-code-toosend-messages"></a>Code schrijven toosend berichten

1. Voeg de volgende Hallo `constants` toohello bovenaan Hallo `sender.js` bestand.
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. Toevoegen van de volgende constanten toohello hello `sender.js` bestand voor meer informatie Hallo hybride verbinding. Tijdelijke aanduidingen Hallo haakjes vervangen door Hallo-waarden die u hebt verkregen tijdens het Hallo hybride verbinding maken.
   
   1. `const ns`-Hallo Relay-naamruimte. Ervoor toouse Hallo naamruimte volledig gekwalificeerde naam; bijvoorbeeld: `{namespace}.servicebus.windows.net`.
   2. `const path`-de naam Hallo van Hallo hybride verbinding.
   3. `const keyrule`-naam op Hallo van Hallo SAS-sleutel.
   4. `const key`-Hallo SAS-sleutelwaarde.

3. Hallo na code toohello toevoegen `sender.js` bestand:
   
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
    Het bestand sender.js moet er als volgt uitzien:
   
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

