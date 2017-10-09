<span data-ttu-id="510b9-101">Als u een shared access signature (SAS)-URL waarmee dat u toegang krijgt tooresources in een opslagaccount beschikt, kunt u Hallo SAS in een verbindingsreeks gebruiken.</span><span class="sxs-lookup"><span data-stu-id="510b9-101">If you possess a shared access signature (SAS) URL that grants you access tooresources in a storage account, you can use hello SAS in a connection string.</span></span> <span data-ttu-id="510b9-102">Omdat Hallo SAS Hallo informatie vereist tooauthenticate Hallo aanvraag bevat, biedt een verbindingsreeks met een SAS Hallo-protocol, Hallo service-eindpunt en Hallo benodigde referenties tooaccess Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="510b9-102">Because hello SAS contains hello information required tooauthenticate hello request, a connection string with a SAS provides hello protocol, hello service endpoint, and hello necessary credentials tooaccess hello resource.</span></span>

<span data-ttu-id="510b9-103">Hallo tekenreeks toocreate een verbindingsreeks met een shared access signature, opgeven in Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="510b9-103">toocreate a connection string that includes a shared access signature, specify hello string in hello following format:</span></span>

```
BlobEndpoint=myBlobEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
FileEndpoint=myFileEndpoint;
SharedAccessSignature=sasToken
```

<span data-ttu-id="510b9-104">Elk service-eindpunt is optioneel, hoewel het Hallo-verbindingsreeks moet ten minste één bevatten.</span><span class="sxs-lookup"><span data-stu-id="510b9-104">Each service endpoint is optional, although hello connection string must contain at least one.</span></span>

> [!NOTE]
> <span data-ttu-id="510b9-105">Gebruik van HTTPS met een SAS wordt aanbevolen als aanbevolen procedure.</span><span class="sxs-lookup"><span data-stu-id="510b9-105">Using HTTPS with a SAS is recommended as a best practice.</span></span>
>
> <span data-ttu-id="510b9-106">Als u een SAS in een verbindingsreeks in een configuratiebestand opgeeft, moet u mogelijk tooencode speciale tekens in Hallo-URL.</span><span class="sxs-lookup"><span data-stu-id="510b9-106">If you are specifying a SAS in a connection string in a configuration file, you may need tooencode special characters in hello URL.</span></span>
>
>

### <a name="service-sas-example"></a><span data-ttu-id="510b9-107">Voorbeeld van de service-SAS</span><span class="sxs-lookup"><span data-stu-id="510b9-107">Service SAS example</span></span>
<span data-ttu-id="510b9-108">Hier volgt een voorbeeld van een verbindingsreeks met een service-SAS voor Blob-opslag:</span><span class="sxs-lookup"><span data-stu-id="510b9-108">Here's an example of a connection string that includes a service SAS for Blob storage:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&sr=b&si=tutorial-policy-635959936145100803&sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

<span data-ttu-id="510b9-109">En Hier volgt een voorbeeld van Hallo dezelfde verbindingsreeks met de codering van speciale tekens bevatten:</span><span class="sxs-lookup"><span data-stu-id="510b9-109">And here's an example of hello same connection string with encoding of special characters:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&amp;sr=b&amp;si=tutorial-policy-635959936145100803&amp;sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

### <a name="account-sas-example"></a><span data-ttu-id="510b9-110">Voorbeeld van account-SAS</span><span class="sxs-lookup"><span data-stu-id="510b9-110">Account SAS example</span></span>
<span data-ttu-id="510b9-111">Hier volgt een voorbeeld van een verbindingsreeks waarin een SAS-account voor Blob en File storage.</span><span class="sxs-lookup"><span data-stu-id="510b9-111">Here's an example of a connection string that includes an account SAS for Blob and File storage.</span></span> <span data-ttu-id="510b9-112">Houd er rekening mee dat eindpunten voor beide services worden opgegeven:</span><span class="sxs-lookup"><span data-stu-id="510b9-112">Note that endpoints for both services are specified:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&spr=https&st=2016-04-12T03%3A24%3A31Z&se=2016-04-13T03%3A29%3A31Z&srt=s&ss=bf&sp=rwl
```

<span data-ttu-id="510b9-113">En Hier volgt een voorbeeld van Hallo dezelfde verbindingsreeks met URL-codering:</span><span class="sxs-lookup"><span data-stu-id="510b9-113">And here's an example of hello same connection string with URL encoding:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&amp;sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&amp;spr=https&amp;st=2016-04-12T03%3A24%3A31Z&amp;se=2016-04-13T03%3A29%3A31Z&amp;srt=s&amp;ss=bf&amp;sp=rwl
```

