### <a name="create-a-console-application"></a>Een consoletoepassing maken

Start eerst Visual Studio en maak een nieuw project van het type **Consoletoepassing (.NET Framework)**.

### <a name="add-hello-relay-nuget-package"></a>Hallo Relay NuGet-pakket toevoegen

1. Met de rechtermuisknop op Hallo van een nieuw gemaakt project en klik vervolgens op **NuGet-pakketten beheren**.
2. Klik op Hallo **Bladeren** tabblad, zoekt u naar 'Microsoft.Azure.Relay' en selecteer Hallo **Microsoft Azure-Relay** item. Klik op **installeren** toocomplete Hallo installatie en sluit vervolgens dit dialoogvenster.

### <a name="write-some-code-tooreceive-messages"></a>Code schrijven tooreceive berichten

1. Hallo bestaande `using` instructies Hallo boven aan het bestand Program.cs Hallo Hallo volgende `using` instructies:
   
    ```csharp
    using System;
    using System.IO;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.Azure.Relay;
    ```
2. Toevoegen van constanten toohello `Program` klasse voor Hallo hybride verbinding meer informatie. Tijdelijke aanduidingen Hallo haakjes vervangen door Hallo-waarden die u hebt verkregen tijdens het Hallo hybride verbinding maken. Naam van de volledig gekwalificeerde naamruimte ervoor toouse Hallo worden:
   
    ```csharp
    private const string RelayNamespace = "{RelayNamespace}.servicebus.windows.net";
    private const string ConnectionName = "{HybridConnectionName}";
    private const string KeyName = "{SASKeyName}";
    private const string Key = "{SASKey}";
    ```
3. Hallo methode aangeroepen na toevoegen `ProcessMessagesOnConnection` toohello `Program` klasse:
   
    ```csharp
    // Method is used tooinitiate connection
    private static async void ProcessMessagesOnConnection(HybridConnectionStream relayConnection, CancellationTokenSource cts)
    {
        Console.WriteLine("New session");
   
        // hello connection is a fully bidrectional stream. 
        // We put a stream reader and a stream writer over it 
        // which allows us tooread UTF-8 text that comes from 
        // hello sender and toowrite text replies back.
        var reader = new StreamReader(relayConnection);
        var writer = new StreamWriter(relayConnection) { AutoFlush = true };
        while (!cts.IsCancellationRequested)
        {
            try
            {
                // Read a line of input until a newline is encountered
                var line = await reader.ReadLineAsync();
   
                if (string.IsNullOrEmpty(line))
                {
                    // If there's no input data, we will signal that 
                    // we will no longer send data on this connection
                    // and then break out of hello processing loop.
                    await relayConnection.ShutdownAsync(cts.Token);
                    break;
                }
   
                // Output hello line on hello console
                Console.WriteLine(line);
   
                // Write hello line back toohello client, prepending "Echo:"
                await writer.WriteLineAsync($"Echo: {line}");
            }
            catch (IOException)
            {
                // Catch an IO exception that is likely caused because
                // hello client disconnected.
                Console.WriteLine("Client closed connection");
                break;
            }
        }
   
        Console.WriteLine("End session");
   
        // Closing hello connection
        await relayConnection.CloseAsync(cts.Token);
    }
    ```
4. Toevoegen van een andere methode aangeroepen `RunAsync` toohello `Program` klasse als volgt:
   
    ```csharp
    private static async Task RunAsync()
    {
        var cts = new CancellationTokenSource();
   
        var tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(KeyName, Key);
        var listener = new HybridConnectionListener(new Uri(string.Format("sb://{0}/{1}", RelayNamespace, ConnectionName)), tokenProvider);
   
        // Subscribe toohello status events
        listener.Connecting += (o, e) => { Console.WriteLine("Connecting"); };
        listener.Offline += (o, e) => { Console.WriteLine("Offline"); };
        listener.Online += (o, e) => { Console.WriteLine("Online"); };
   
        // Opening hello listener will establish hello control channel to
        // hello Azure Relay service. hello control channel will be continuously 
        // maintained and reestablished when connectivity is disrupted.
        await listener.OpenAsync(cts.Token);
        Console.WriteLine("Server listening");
   
        // Providing callback for cancellation token that will close hello listener.
        cts.Token.Register(() => listener.CloseAsync(CancellationToken.None));
   
        // Start a new thread that will continuously read hello console.
        new Task(() => Console.In.ReadLineAsync().ContinueWith((s) => { cts.Cancel(); })).Start();
   
        // Accept hello next available, pending connection request. 
        // Shutting down hello listener will allow a clean exit with 
        // this method returning null
        while (true)
        {
            var relayConnection = await listener.AcceptConnectionAsync();
            if (relayConnection == null)
            {
                break;
            }
   
            ProcessMessagesOnConnection(relayConnection, cts);
        }
   
        // Close hello listener after we exit hello processing loop
        await listener.CloseAsync(cts.Token);
    }
    ```
5. Toevoegen van de volgende regel code toohello hello `Main` methode in Hallo `Program` klasse:
   
    ```csharp
    RunAsync().GetAwaiter().GetResult();
    ```
   
    Het voltooide bestand Program.cs zou er als volgt moeten uitzien:
   
    ```csharp
    namespace Server
    {
        using System;
        using System.IO;
        using System.Threading;
        using System.Threading.Tasks;
        using Microsoft.Azure.Relay;
   
        public class Program
        {
            private const string RelayNamespace = "{RelayNamespace}.servicebus.windows.net";
            private const string ConnectionName = "{HybridConnectionName}";
            private const string KeyName = "{SASKeyName}";
            private const string Key = "{SASKey}";
   
            public static void Main(string[] args)
            {
                RunAsync().GetAwaiter().GetResult();
            }
   
            private static async Task RunAsync()
            {
                var cts = new CancellationTokenSource();
   
                var tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(KeyName, Key);
                var listener = new HybridConnectionListener(new Uri(string.Format("sb://{0}/{1}", RelayNamespace, ConnectionName)), tokenProvider);
   
                // Subscribe toohello status events
                listener.Connecting += (o, e) => { Console.WriteLine("Connecting"); };
                listener.Offline += (o, e) => { Console.WriteLine("Offline"); };
                listener.Online += (o, e) => { Console.WriteLine("Online"); };
   
                // Opening hello listener will establish hello control channel to
                // hello Azure Relay service. hello control channel will be continuously 
                // maintained and reestablished when connectivity is disrupted.
                await listener.OpenAsync(cts.Token);
                Console.WriteLine("Server listening");
   
                // Providing callback for cancellation token that will close hello listener.
                cts.Token.Register(() => listener.CloseAsync(CancellationToken.None));
   
                // Start a new thread that will continuously read hello console.
                new Task(() => Console.In.ReadLineAsync().ContinueWith((s) => { cts.Cancel(); })).Start();
   
                // Accept hello next available, pending connection request. 
                // Shutting down hello listener will allow a clean exit with 
                // this method returning null
                while (true)
                {
                    var relayConnection = await listener.AcceptConnectionAsync();
                    if (relayConnection == null)
                    {
                        break;
                    }
   
                    ProcessMessagesOnConnection(relayConnection, cts);
                }
   
                // Close hello listener after we exit hello processing loop
                await listener.CloseAsync(cts.Token);
            }
   
            private static async void ProcessMessagesOnConnection(HybridConnectionStream relayConnection, CancellationTokenSource cts)
            {
                Console.WriteLine("New session");
   
                // hello connection is a fully bidrectional stream. 
                // We put a stream reader and a stream writer over it 
                // which allows us tooread UTF-8 text that comes from 
                // hello sender and toowrite text replies back.
                var reader = new StreamReader(relayConnection);
                var writer = new StreamWriter(relayConnection) { AutoFlush = true };
                while (!cts.IsCancellationRequested)
                {
                    try
                    {
                        // Read a line of input until a newline is encountered
                        var line = await reader.ReadLineAsync();
   
                        if (string.IsNullOrEmpty(line))
                        {
                            // If there's no input data, we will signal that 
                            // we will no longer send data on this connection
                            // and then break out of hello processing loop.
                            await relayConnection.ShutdownAsync(cts.Token);
                            break;
                        }
   
                        // Output hello line on hello console
                        Console.WriteLine(line);
   
                        // Write hello line back toohello client, prepending "Echo:"
                        await writer.WriteLineAsync($"Echo: {line}");
                    }
                    catch (IOException)
                    {
                        // Catch an IO exception that is likely caused because
                        // hello client disconnected.
                        Console.WriteLine("Client closed connection");
                        break;
                    }
                }
   
                Console.WriteLine("End session");
   
                // Closing hello connection
                await relayConnection.CloseAsync(cts.Token);
            }
        }
    }
    ```

