<span data-ttu-id="80bfc-101">Als u een shared access signature (SAS)-URL die u toegang tot bronnen in een opslagaccount verleent beschikt, kunt u de SAS in een verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="80bfc-101">If you possess a shared access signature (SAS) URL that grants you access to resources in a storage account, you can use the SAS in a connection string.</span></span> <span data-ttu-id="80bfc-102">Omdat de SAS de benodigde informatie om te verifiëren van de aanvraag bevat, biedt een verbindingsreeks met een SAS het protocol, het service-eindpunt en de benodigde referenties voor toegang tot de bron.</span><span class="sxs-lookup"><span data-stu-id="80bfc-102">Because the SAS contains the information required to authenticate the request, a connection string with a SAS provides the protocol, the service endpoint, and the necessary credentials to access the resource.</span></span>

<span data-ttu-id="80bfc-103">Geef voor het maken van een verbindingsreeks die een shared access signature bevat de tekenreeks in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="80bfc-103">To create a connection string that includes a shared access signature, specify the string in the following format:</span></span>

```
BlobEndpoint=myBlobEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
FileEndpoint=myFileEndpoint;
SharedAccessSignature=sasToken
```

<span data-ttu-id="80bfc-104">Elk service-eindpunt is optioneel, hoewel de verbindingsreeks moet ten minste één bevatten.</span><span class="sxs-lookup"><span data-stu-id="80bfc-104">Each service endpoint is optional, although the connection string must contain at least one.</span></span>

> [!NOTE]
> <span data-ttu-id="80bfc-105">Gebruik van HTTPS met een SAS wordt aanbevolen als aanbevolen procedure.</span><span class="sxs-lookup"><span data-stu-id="80bfc-105">Using HTTPS with a SAS is recommended as a best practice.</span></span>
>
> <span data-ttu-id="80bfc-106">Als u een SAS in een verbindingsreeks in een configuratiebestand opgeeft, moet u wellicht de speciale tekens in de URL's coderen.</span><span class="sxs-lookup"><span data-stu-id="80bfc-106">If you are specifying a SAS in a connection string in a configuration file, you may need to encode special characters in the URL.</span></span>
>
>

### <a name="service-sas-example"></a><span data-ttu-id="80bfc-107">Voorbeeld van de service-SAS</span><span class="sxs-lookup"><span data-stu-id="80bfc-107">Service SAS example</span></span>
<span data-ttu-id="80bfc-108">Hier volgt een voorbeeld van een verbindingsreeks met een service-SAS voor Blob-opslag:</span><span class="sxs-lookup"><span data-stu-id="80bfc-108">Here's an example of a connection string that includes a service SAS for Blob storage:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&sr=b&si=tutorial-policy-635959936145100803&sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

<span data-ttu-id="80bfc-109">En Hier volgt een voorbeeld van de verbindingsreeks met codering van speciale tekens bevatten:</span><span class="sxs-lookup"><span data-stu-id="80bfc-109">And here's an example of the same connection string with encoding of special characters:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&amp;sr=b&amp;si=tutorial-policy-635959936145100803&amp;sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

### <a name="account-sas-example"></a><span data-ttu-id="80bfc-110">Voorbeeld van account-SAS</span><span class="sxs-lookup"><span data-stu-id="80bfc-110">Account SAS example</span></span>
<span data-ttu-id="80bfc-111">Hier volgt een voorbeeld van een verbindingsreeks waarin een SAS-account voor Blob en File storage.</span><span class="sxs-lookup"><span data-stu-id="80bfc-111">Here's an example of a connection string that includes an account SAS for Blob and File storage.</span></span> <span data-ttu-id="80bfc-112">Houd er rekening mee dat eindpunten voor beide services worden opgegeven:</span><span class="sxs-lookup"><span data-stu-id="80bfc-112">Note that endpoints for both services are specified:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&spr=https&st=2016-04-12T03%3A24%3A31Z&se=2016-04-13T03%3A29%3A31Z&srt=s&ss=bf&sp=rwl
```

<span data-ttu-id="80bfc-113">En Hier volgt een voorbeeld van de verbindingsreeks met URL-codering:</span><span class="sxs-lookup"><span data-stu-id="80bfc-113">And here's an example of the same connection string with URL encoding:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&amp;sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&amp;spr=https&amp;st=2016-04-12T03%3A24%3A31Z&amp;se=2016-04-13T03%3A29%3A31Z&amp;srt=s&amp;ss=bf&amp;sp=rwl
```

