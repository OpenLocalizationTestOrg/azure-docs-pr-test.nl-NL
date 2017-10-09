### <a name="create-a-nodejs-application"></a>Een Node.js-toepassing maken

Maak een nieuw JavaScript-bestand met de naam `listener.js`.

### <a name="add-hello-relay-npm-package"></a>Hallo Relay NPM pakket toevoegen

Voer `npm install hyco-ws` uit vanaf een Node-opdrachtprompt in de projectmap.

### <a name="write-some-code-tooreceive-messages"></a>Code schrijven tooreceive berichten

1. Toevoegen van de volgende constante toohello bovenaan Hallo Hallo `listener.js` bestand.
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. Toevoegen van de volgende constanten toohello hello `listener.js` bestand voor meer informatie Hallo hybride verbinding. Tijdelijke aanduidingen Hallo haakjes vervangen door Hallo-waarden die u hebt verkregen tijdens het Hallo hybride verbinding maken.
   
   1. `const ns`-Hallo Relay-naamruimte. Ervoor toouse Hallo naamruimte volledig gekwalificeerde naam; bijvoorbeeld: `{namespace}.servicebus.windows.net`.
   2. `const path`-de naam Hallo van Hallo hybride verbinding.
   3. `const keyrule`-naam op Hallo van Hallo SAS-sleutel.
   4. `const key`-Hallo SAS-sleutelwaarde.

3. Hallo na code toohello toevoegen `listener.js` bestand:
   
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
    Zo zou het bestand listener.js er moeten uitzien:
   
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

