<span data-ttu-id="75fc0-101">de opslagemulator Hallo ondersteunt één vaste account en een bekende verificatiesleutel voor verificatie met gedeelde sleutel.</span><span class="sxs-lookup"><span data-stu-id="75fc0-101">hello storage emulator supports a single fixed account and a well-known authentication key for Shared Key authentication.</span></span> <span data-ttu-id="75fc0-102">Dit account en de sleutel zijn Hallo alleen gedeelde sleutel referenties zijn toegestaan voor gebruik met Hallo-opslagemulator.</span><span class="sxs-lookup"><span data-stu-id="75fc0-102">This account and key are hello only Shared Key credentials permitted for use with hello storage emulator.</span></span> <span data-ttu-id="75fc0-103">Ze zijn:</span><span class="sxs-lookup"><span data-stu-id="75fc0-103">They are:</span></span>

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> <span data-ttu-id="75fc0-104">Hallo verificatiesleutel wordt ondersteund door de opslagemulator Hallo is alleen bedoeld voor testen Hallo-functionaliteit van de clientcode voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="75fc0-104">hello authentication key supported by hello storage emulator is intended only for testing hello functionality of your client authentication code.</span></span> <span data-ttu-id="75fc0-105">Deze dienen geen elk doeleinde beveiliging.</span><span class="sxs-lookup"><span data-stu-id="75fc0-105">It does not serve any security purpose.</span></span> <span data-ttu-id="75fc0-106">U kunt uw storage-account voor productie en de sleutel niet gebruiken met Hallo-opslagemulator.</span><span class="sxs-lookup"><span data-stu-id="75fc0-106">You cannot use your production storage account and key with hello storage emulator.</span></span> <span data-ttu-id="75fc0-107">U moet Hallo ontwikkeling account niet gebruiken met productiegegevens.</span><span class="sxs-lookup"><span data-stu-id="75fc0-107">You should not use hello development account with production data.</span></span>
> 
> <span data-ttu-id="75fc0-108">Hallo-opslagemulator ondersteunt alleen verbinding via HTTP.</span><span class="sxs-lookup"><span data-stu-id="75fc0-108">hello storage emulator supports connection via HTTP only.</span></span> <span data-ttu-id="75fc0-109">HTTPS is echter Hallo aanbevolen standaardprotocol voor toegang tot resources in een productie-Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="75fc0-109">However, HTTPS is hello recommended protocol for accessing resources in a production Azure storage account.</span></span>
> 

#### <a name="connect-toohello-emulator-account-using-a-shortcut"></a><span data-ttu-id="75fc0-110">Verbinding maken met toohello emulator account via een snelkoppeling</span><span class="sxs-lookup"><span data-stu-id="75fc0-110">Connect toohello emulator account using a shortcut</span></span>
<span data-ttu-id="75fc0-111">Hallo gemakkelijkste manier tooconnect toohello opslagemulator van uw toepassing is tooconfigure een verbindingsreeks in het configuratiebestand van de toepassing die verwijst naar de snelkoppeling Hallo `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="75fc0-111">hello easiest way tooconnect toohello storage emulator from your application is tooconfigure a connection string in your application's configuration file that references hello shortcut `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="75fc0-112">Hier volgt een voorbeeld van een verbinding tekenreeks toohello opslagemulator in een *app.config* bestand:</span><span class="sxs-lookup"><span data-stu-id="75fc0-112">Here's an example of a connection string toohello storage emulator in an *app.config* file:</span></span> 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-toohello-emulator-account-using-hello-well-known-account-name-and-key"></a><span data-ttu-id="75fc0-113">Verbinding maken met toohello emulator account met behulp van de bekende accountnaam Hallo en sleutel</span><span class="sxs-lookup"><span data-stu-id="75fc0-113">Connect toohello emulator account using hello well-known account name and key</span></span>
<span data-ttu-id="75fc0-114">toocreate een verbindingsreeks dat verwijzingen Hallo emulator accountnaam en sleutels, u Hallo eindpunten opgeven moet voor elk van de Hallo u services wilt toouse van Hallo-emulator in Hallo-verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="75fc0-114">toocreate a connection string that references hello emulator account name and key, you must specify hello endpoints for each of hello services you wish toouse from hello emulator in hello connection string.</span></span> <span data-ttu-id="75fc0-115">Dit is noodzakelijk om Hallo verbindingsreeks verwijst naar Hallo emulator eindpunten, anders dan de voor een productie-opslagaccount zijn.</span><span class="sxs-lookup"><span data-stu-id="75fc0-115">This is necessary so that hello connection string will reference hello emulator endpoints, which are different than those for a production storage account.</span></span> <span data-ttu-id="75fc0-116">Bijvoorbeeld, ziet Hallo-waarde van de verbindingsreeks er als volgt:</span><span class="sxs-lookup"><span data-stu-id="75fc0-116">For example, hello value of your connection string will look like this:</span></span>

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

<span data-ttu-id="75fc0-117">Deze waarde is identiek toohello snelkoppeling bovenstaande `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="75fc0-117">This value is identical toohello shortcut shown above, `UseDevelopmentStorage=true`.</span></span>

#### <a name="specify-an-http-proxy"></a><span data-ttu-id="75fc0-118">Geef een HTTP-proxy</span><span class="sxs-lookup"><span data-stu-id="75fc0-118">Specify an HTTP proxy</span></span>
<span data-ttu-id="75fc0-119">U kunt ook een HTTP-proxy toouse opgeven wanneer u bij het testen van uw service tegen Hallo-opslagemulator.</span><span class="sxs-lookup"><span data-stu-id="75fc0-119">You can also specify an HTTP proxy toouse when you're testing your service against hello storage emulator.</span></span> <span data-ttu-id="75fc0-120">Dit kan handig zijn voor de naleving van HTTP-aanvragen en antwoorden terwijl u fouten bewerkingen op Hallo storage-services opspoort zijn.</span><span class="sxs-lookup"><span data-stu-id="75fc0-120">This can be useful for observing HTTP requests and responses while you're debugging operations against hello storage services.</span></span> <span data-ttu-id="75fc0-121">een proxy toospecify toevoegen Hallo `DevelopmentStorageProxyUri` optie toohello verbindingsreeks en stel de waarde toohello proxy URI.</span><span class="sxs-lookup"><span data-stu-id="75fc0-121">toospecify a proxy, add hello `DevelopmentStorageProxyUri` option toohello connection string, and set its value toohello proxy URI.</span></span> <span data-ttu-id="75fc0-122">Hier is bijvoorbeeld een verbindingsreeks die de opslagemulator toohello verwijst en een HTTP-proxy configureert:</span><span class="sxs-lookup"><span data-stu-id="75fc0-122">For example, here is a connection string that points toohello storage emulator and configures an HTTP proxy:</span></span>

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```

