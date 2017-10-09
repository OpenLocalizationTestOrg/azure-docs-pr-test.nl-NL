---
title: aaaOn-premises toepassing met blob storage (Java) | Microsoft Docs
description: Meer informatie over hoe een consoletoepassing die een installatiekopie tooAzure en geeft vervolgens uploadt toocreate Hallo-installatiekopie in uw browser. Codevoorbeelden in Java.
services: storage
documentationcenter: java
author: mmacy
manager: carmonm
editor: tysonn
ms.assetid: ccc9a7d7-6fe4-467b-b7fd-a73f17539e3f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/17/2016
ms.author: marsma
ms.openlocfilehash: ed8eb4c1045691c25abe94bf6c1b18b797adc3e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="on-premises-application-with-blob-storage"></a><span data-ttu-id="376ea-104">On-premises toepassing met blob storage</span><span class="sxs-lookup"><span data-stu-id="376ea-104">On-premises application with blob storage</span></span>
## <a name="overview"></a><span data-ttu-id="376ea-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="376ea-105">Overview</span></span>
<span data-ttu-id="376ea-106">Hallo volgende voorbeeld ziet u hoe u Azure-opslag kunt gebruiken voor het opslaan van afbeeldingen in Azure.</span><span class="sxs-lookup"><span data-stu-id="376ea-106">hello following example shows you how you can use Azure storage to store images in Azure.</span></span> <span data-ttu-id="376ea-107">Hallo-code in dit artikel is bedoeld voor een consoletoepassing die een tooAzure afbeelding uploadt en maakt vervolgens een HTML-bestand waarin Hallo afbeelding worden weergegeven in uw browser.</span><span class="sxs-lookup"><span data-stu-id="376ea-107">hello code in this article is for a console application that uploads an image tooAzure, and then creates an HTML file that displays hello image in your browser.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="376ea-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="376ea-108">Prerequisites</span></span>
* <span data-ttu-id="376ea-109">Een Java Developer Kit (JDK), versie 1.6 of hoger is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="376ea-109">A Java Developer Kit (JDK), version 1.6 or later, is installed.</span></span>
* <span data-ttu-id="376ea-110">Hello Azure SDK is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="376ea-110">hello Azure SDK is installed.</span></span>
* <span data-ttu-id="376ea-111">Hallo JAR voor hello Azure-beheerbibliotheken voor Java, en eventuele potten afhankelijkheid van toepassing zijn geïnstalleerd en in Hallo build pad dat wordt gebruikt door uw Java-compiler.</span><span class="sxs-lookup"><span data-stu-id="376ea-111">hello JAR for hello Azure Libraries for Java, and any applicable dependency JARs, are installed and are in hello build path used by your Java compiler.</span></span> <span data-ttu-id="376ea-112">Zie voor meer informatie over het installeren van hello Azure-beheerbibliotheken voor Java [downloaden hello Azure SDK voor Java](../java-download-azure-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="376ea-112">For information about installing hello Azure Libraries for Java, see [Download hello Azure SDK for Java](../java-download-azure-sdk.md).</span></span>
* <span data-ttu-id="376ea-113">Een Azure storage-account is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="376ea-113">An Azure storage account has been set up.</span></span> <span data-ttu-id="376ea-114">Hallo wordt accountnaam en accountsleutel voor Hallo storage-account gebruikt door Hallo-code in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="376ea-114">hello account name and account key for hello storage account will be used by hello code in this article.</span></span> <span data-ttu-id="376ea-115">Zie [hoe tooCreate een Opslagaccount](storage-create-storage-account.md#create-a-storage-account) voor informatie over het maken van een opslagaccount en [weergeven en kopiëren opslagtoegangssleutels](storage-create-storage-account.md#view-and-copy-storage-access-keys) voor informatie over het Hallo-accountcode ophalen.</span><span class="sxs-lookup"><span data-stu-id="376ea-115">See [How tooCreate a Storage Account](storage-create-storage-account.md#create-a-storage-account) for information about creating a storage account, and [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys) for information about retrieving hello account key.</span></span>
* <span data-ttu-id="376ea-116">U hebt gemaakt een lokaal bestand met de naam opgeslagen op Hallo pad c:\\myimages\\image1.jpg.</span><span class="sxs-lookup"><span data-stu-id="376ea-116">You have created a local image file named stored at hello path c:\\myimages\\image1.jpg.</span></span> <span data-ttu-id="376ea-117">U kunt ook wijzigen de **FileInputStream** Hallo voorbeeld toouse een andere installatiekopie pad en de naam-constructor.</span><span class="sxs-lookup"><span data-stu-id="376ea-117">Alternatively, modify the **FileInputStream** constructor in hello example toouse a different image path and file name.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="toouse-azure-blob-storage-tooupload-a-file"></a><span data-ttu-id="376ea-118">toouse Azure blob storage tooupload een bestand</span><span class="sxs-lookup"><span data-stu-id="376ea-118">toouse Azure blob storage tooupload a file</span></span>
<span data-ttu-id="376ea-119">Een stapsgewijze procedure die hier voorgesteld.</span><span class="sxs-lookup"><span data-stu-id="376ea-119">A step-by-step procedure is presented here.</span></span> <span data-ttu-id="376ea-120">Als u tooskip vooruit wilt, is de volledige code Hallo verderop in dit artikel opgenomen.</span><span class="sxs-lookup"><span data-stu-id="376ea-120">If you'd like tooskip ahead, hello entire code is presented later in this article.</span></span>

<span data-ttu-id="376ea-121">Hallo code beginnen door Imports-instructie voor hello Azure core Opslagklassen, hello Azure blob-clientklassen, Hallo Java i/o-klassen en Hallo **URISyntaxException** klasse.</span><span class="sxs-lookup"><span data-stu-id="376ea-121">Begin hello code by including imports for hello Azure core storage classes, hello Azure blob client classes, hello Java IO classes, and hello **URISyntaxException** class.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

<span data-ttu-id="376ea-122">Een klasse met de naam declareert **StorageSample**, en open haakje hello, bevatten **{**.</span><span class="sxs-lookup"><span data-stu-id="376ea-122">Declare a class named **StorageSample**, and include hello open bracket, **{**.</span></span>

```java
public class StorageSample {
```

<span data-ttu-id="376ea-123">Binnen Hallo **StorageSample** klasse, declareert u een string-variabele die Hallo-standaardprotocol eindpunt, naam van uw opslagaccount en uw toegangssleutel voor opslag, zoals opgegeven in uw Azure storage-account bevat.</span><span class="sxs-lookup"><span data-stu-id="376ea-123">Within hello **StorageSample** class, declare a string variable that will contain hello default endpoint protocol, your storage account name, and your storage access key, as specified in your Azure storage account.</span></span> <span data-ttu-id="376ea-124">Vervang de waarden van de tijdelijke aanduiding Hallo **uw\_account\_naam** en **uw\_account\_sleutel** met uw eigen accountnaam en accountsleutel, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="376ea-124">Replace hello placeholder values **your\_account\_name** and **your\_account\_key** with your own account name and account key, respectively.</span></span>

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

<span data-ttu-id="376ea-125">Toevoegen aan uw-declaratie voor **belangrijkste**, bevatten een **probeer** blokkeren en Hallo nodig open vierkante haken, omvatten **{**.</span><span class="sxs-lookup"><span data-stu-id="376ea-125">Add in your declaration for **main**, include a **try** block, and include hello necessary open brackets, **{**.</span></span>

```java
    public static void main(String[] args)
    {
        try
        {
```

<span data-ttu-id="376ea-126">Declareer de variabelen Hallo type (hello beschrijvingen zijn voor hoe ze worden gebruikt in dit voorbeeld) te volgen:</span><span class="sxs-lookup"><span data-stu-id="376ea-126">Declare variables of hello following type (hello descriptions are for how they are used in this example):</span></span>

* <span data-ttu-id="376ea-127">**CloudStorageAccount**: gebruikte tooinitialize Hallo accountobject met uw Azure-opslag-accountnaam en -sleutel en toocreate het blob-client-object.</span><span class="sxs-lookup"><span data-stu-id="376ea-127">**CloudStorageAccount**: Used tooinitialize hello account object with your Azure storage account name and key, and toocreate the blob client object.</span></span>
* <span data-ttu-id="376ea-128">**CloudBlobClient**: tooaccess Hallo blob-service gebruikt.</span><span class="sxs-lookup"><span data-stu-id="376ea-128">**CloudBlobClient**: Used tooaccess hello blob service.</span></span>
* <span data-ttu-id="376ea-129">**CloudBlobContainer**: gebruikte toocreate een blob-container lijst de blobs in Hallo-container en delete Hallo container.</span><span class="sxs-lookup"><span data-stu-id="376ea-129">**CloudBlobContainer**: Used toocreate a blob container, list the blobs in hello container, and delete hello container.</span></span>
* <span data-ttu-id="376ea-130">**CloudBlockBlob**: gebruikte tooupload een afbeelding voor lokaal bestand toothe container.</span><span class="sxs-lookup"><span data-stu-id="376ea-130">**CloudBlockBlob**: Used tooupload a local image file toothe container.</span></span>

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

<span data-ttu-id="376ea-131">Toewijzen van een waarde toohello **account** variabele.</span><span class="sxs-lookup"><span data-stu-id="376ea-131">Assign a value toohello **account** variable.</span></span>

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

<span data-ttu-id="376ea-132">Toewijzen van een waarde toohello **serviceClient** variabele.</span><span class="sxs-lookup"><span data-stu-id="376ea-132">Assign a value toohello **serviceClient** variable.</span></span>

```java
serviceClient = account.createCloudBlobClient();
```

<span data-ttu-id="376ea-133">Toewijzen van een waarde toohello **container** variabele.</span><span class="sxs-lookup"><span data-stu-id="376ea-133">Assign a value toohello **container** variable.</span></span> <span data-ttu-id="376ea-134">Je krijgt een verwijzing tooa container met de naam **gettingstarted**.</span><span class="sxs-lookup"><span data-stu-id="376ea-134">We'll get a reference tooa container named **gettingstarted**.</span></span>

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

<span data-ttu-id="376ea-135">Hallo-container maken.</span><span class="sxs-lookup"><span data-stu-id="376ea-135">Create hello container.</span></span> <span data-ttu-id="376ea-136">Deze methode maakt Hallo container als deze niet bestaat (en terug te keren **true**).</span><span class="sxs-lookup"><span data-stu-id="376ea-136">This method will create hello container if it doesn't exist (and return **true**).</span></span> <span data-ttu-id="376ea-137">Als Hallo-container bestaat nog, wordt geretourneerd **false**.</span><span class="sxs-lookup"><span data-stu-id="376ea-137">If hello container does exist, it will return **false**.</span></span> <span data-ttu-id="376ea-138">Een alternatief te**createIfNotExists** Hallo is **maken** methode (die retourneren een foutmelding als Hallo container al bestaat).</span><span class="sxs-lookup"><span data-stu-id="376ea-138">An alternative too**createIfNotExists** is hello **create** method (which will return an error if hello container already exists).</span></span>

```java
container.createIfNotExists();
```

<span data-ttu-id="376ea-139">Anonieme toegang voor Hallo-container instellen.</span><span class="sxs-lookup"><span data-stu-id="376ea-139">Set anonymous access for hello container.</span></span>

```java
// Set anonymous access on hello container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

<span data-ttu-id="376ea-140">Haal een verwijzing toohello blok-blob, die Hallo blob in Azure-opslag vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="376ea-140">Get a reference toohello block blob, which will represent hello blob in Azure storage.</span></span>

```java
blob = container.getBlockBlobReference("image1.jpg");
```

<span data-ttu-id="376ea-141">Gebruik Hallo **bestand** constructor tooget een referentiebestand toohello lokaal gemaakt dat u zult uploaden.</span><span class="sxs-lookup"><span data-stu-id="376ea-141">Use hello **File** constructor tooget a reference toohello locally created file that you will upload.</span></span> <span data-ttu-id="376ea-142">Zorg ervoor dat u dit bestand hebt gemaakt voordat u Hallo code uitvoert.</span><span class="sxs-lookup"><span data-stu-id="376ea-142">Ensure you have created this file before running hello code.</span></span>

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

<span data-ttu-id="376ea-143">Upload Hallo lokale bestand via een aanroep van toohello **CloudBlockBlob.upload** methode.</span><span class="sxs-lookup"><span data-stu-id="376ea-143">Upload hello local file through a call toohello **CloudBlockBlob.upload** method.</span></span> <span data-ttu-id="376ea-144">eerste parameter toohello Hallo **CloudBlockBlob.upload** methode is een **FileInputStream** object vertegenwoordigt Hallo lokale bestand die worden geüpload tooAzure opslag.</span><span class="sxs-lookup"><span data-stu-id="376ea-144">hello first parameter toohello **CloudBlockBlob.upload** method is a **FileInputStream** object that represents hello local file that will be uploaded tooAzure storage.</span></span> <span data-ttu-id="376ea-145">de tweede parameter Hallo is Hallo grootte, in bytes, van Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="376ea-145">hello second parameter is hello size, in bytes, of hello file.</span></span>

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

<span data-ttu-id="376ea-146">Aanroepen van een Help-functie met de naam **MakeHTMLPage**, toomake een basic HTML-pagina waarop een  **&lt;installatiekopie&gt;**  element met Hallo bron set toohello blob die nu in uw Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="376ea-146">Call a helper function named **MakeHTMLPage**, toomake a basic HTML page that contains an **&lt;image&gt;** element with hello source set toohello blob that is now in your Azure storage account.</span></span> <span data-ttu-id="376ea-147">code voor Hallo **MakeHTMLPage** wordt verderop in dit artikel worden besproken.</span><span class="sxs-lookup"><span data-stu-id="376ea-147">hello code for **MakeHTMLPage** will be discussed later in this article.</span></span>

```java
MakeHTMLPage(container);
```

<span data-ttu-id="376ea-148">Afdrukken een statusbericht en informatie over Hallo HTML-pagina gemaakt.</span><span class="sxs-lookup"><span data-stu-id="376ea-148">Print out a status message and information about hello created HTML page.</span></span>

```java
System.out.println("Processing complete.");
System.out.println("Open index.html toosee hello images stored in your storage account.");
```

<span data-ttu-id="376ea-149">Sluit Hallo **probeer** blokkeren door het invoegen van een haakje sluiten: **}**</span><span class="sxs-lookup"><span data-stu-id="376ea-149">Close hello **try** block by inserting a close bracket: **}**</span></span>

<span data-ttu-id="376ea-150">Verwerken Hallo volgende uitzonderingen:</span><span class="sxs-lookup"><span data-stu-id="376ea-150">Handle hello following exceptions:</span></span>

* <span data-ttu-id="376ea-151">**FileNotFoundException**: kan worden gegenereerd door Hallo **FileInputStream** of **FileOutputStream** constructors.</span><span class="sxs-lookup"><span data-stu-id="376ea-151">**FileNotFoundException**: Can be thrown by hello **FileInputStream** or **FileOutputStream** constructors.</span></span>
* <span data-ttu-id="376ea-152">**StorageException**: door opslagbibliotheek van hello Azure-client kan worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="376ea-152">**StorageException**: Can be thrown by hello Azure client storage library.</span></span>
* <span data-ttu-id="376ea-153">**URISyntaxException**: kan worden gegenereerd door Hallo **ListBlobItem.getUri** methode.</span><span class="sxs-lookup"><span data-stu-id="376ea-153">**URISyntaxException**: Can be thrown by hello **ListBlobItem.getUri** method.</span></span>
* <span data-ttu-id="376ea-154">**Uitzondering**: algemene uitzonderingsverwerking.</span><span class="sxs-lookup"><span data-stu-id="376ea-154">**Exception**: Generic exception handling.</span></span>

<!-- -->

```java
catch (FileNotFoundException fileNotFoundException)
{
    System.out.print("FileNotFoundException encountered: ");
    System.out.println(fileNotFoundException.getMessage());
    System.exit(-1);
}
catch (StorageException storageException)
{
    System.out.print("StorageException encountered: ");
    System.out.println(storageException.getMessage());
    System.exit(-1);
}
catch (URISyntaxException uriSyntaxException)
{
    System.out.print("URISyntaxException encountered: ");
    System.out.println(uriSyntaxException.getMessage());
    System.exit(-1);
}
catch (Exception e)
{
    System.out.print("Exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="376ea-155">Sluit **belangrijkste** door het invoegen van een haakje sluiten: **}**</span><span class="sxs-lookup"><span data-stu-id="376ea-155">Close **main** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="376ea-156">Maken van een methode met de naam **MakeHTMLPage** toocreate een basic HTML-pagina.</span><span class="sxs-lookup"><span data-stu-id="376ea-156">Create a method named **MakeHTMLPage** toocreate a basic HTML page.</span></span> <span data-ttu-id="376ea-157">Deze methode heeft een parameter van het type **CloudBlobContainer**, die wordt gebruikt tooiterate door Hallo lijst met geüploade BLOB's zijn.</span><span class="sxs-lookup"><span data-stu-id="376ea-157">This method has a parameter of type **CloudBlobContainer**, which will be used tooiterate through hello list of uploaded blobs.</span></span> <span data-ttu-id="376ea-158">Deze methode genereert uitzonderingen van het type **FileNotFoundException**, die kan worden gegenereerd door Hallo **FileOutputStream** -constructor aan, en **URISyntaxException**, dit kan worden veroorzaakt door Hallo **ListBlobItem.getUri** methode.</span><span class="sxs-lookup"><span data-stu-id="376ea-158">This method will throw exceptions of type **FileNotFoundException**, which can be thrown by hello **FileOutputStream** constructor, and **URISyntaxException**, which can be thrown by hello **ListBlobItem.getUri** method.</span></span> <span data-ttu-id="376ea-159">Het openingshaakje omvatten **{**.</span><span class="sxs-lookup"><span data-stu-id="376ea-159">Include the opening bracket, **{**.</span></span>

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

<span data-ttu-id="376ea-160">Maken van een lokaal bestand met de naam **index.html**.</span><span class="sxs-lookup"><span data-stu-id="376ea-160">Create a local file named **index.html**.</span></span>

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

<span data-ttu-id="376ea-161">Schrijven naar lokale bestand toohello, toe te voegen in Hallo  **&lt;html&gt;**,  **&lt;header&gt;**, en  **&lt;hoofdtekst&gt;**  elementen.</span><span class="sxs-lookup"><span data-stu-id="376ea-161">Write toohello local file, adding in hello **&lt;html&gt;**, **&lt;header&gt;**, and **&lt;body&gt;** elements.</span></span>

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

<span data-ttu-id="376ea-162">Hallo-lijst met geüploade blobs doorlopen.</span><span class="sxs-lookup"><span data-stu-id="376ea-162">Iterate through hello list of uploaded blobs.</span></span> <span data-ttu-id="376ea-163">Voor elke blob in Hallo HTML-pagina maken een  **&lt;img&gt;**  -element waarvoor de **src** kenmerk verzonden op Hallo van URI van de blob Hallo zoals dit zich in uw Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="376ea-163">For each blob, in hello HTML page create an **&lt;img&gt;** element that has its **src** attribute sent to hello URI of hello blob as it exists in your Azure storage account.</span></span>
<span data-ttu-id="376ea-164">Hoewel u slechts één installatiekopie in dit voorbeeld wordt toegevoegd als u meer hebt toegevoegd, zou deze code allemaal herhalen.</span><span class="sxs-lookup"><span data-stu-id="376ea-164">Although you added only one image in this sample, if you added more, this code would iterate all of them.</span></span>

<span data-ttu-id="376ea-165">Voor eenvoud, in dit voorbeeld wordt ervan uitgegaan dat elke geüploade blob is een afbeelding.</span><span class="sxs-lookup"><span data-stu-id="376ea-165">For simplicity, this example assumes each uploaded blob is an image.</span></span> <span data-ttu-id="376ea-166">Als u blobs dan afbeeldingen of pagina-blobs in plaats van blok-blobs hebt bijgewerkt, past u Hallo code indien nodig.</span><span class="sxs-lookup"><span data-stu-id="376ea-166">If you've updated blobs other than images, or page blobs instead of block blobs, adjust hello code as needed.</span></span>

```java
// Enumerate hello uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in hello HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

<span data-ttu-id="376ea-167">Sluit Hallo  **&lt;hoofdtekst&gt;**  -element en Hallo  **&lt;html&gt;**  element.</span><span class="sxs-lookup"><span data-stu-id="376ea-167">Close hello **&lt;body&gt;** element and hello **&lt;html&gt;** element.</span></span>

```java
stream.println("</body>");
stream.println("</html>");
```

<span data-ttu-id="376ea-168">Sluit Hallo lokaal bestand.</span><span class="sxs-lookup"><span data-stu-id="376ea-168">Close hello local file.</span></span>

```java
stream.close();
```

<span data-ttu-id="376ea-169">Sluit **MakeHTMLPage** door het invoegen van een haakje sluiten: **}**</span><span class="sxs-lookup"><span data-stu-id="376ea-169">Close **MakeHTMLPage** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="376ea-170">Sluit **StorageSample** door het invoegen van een haakje sluiten: **}**</span><span class="sxs-lookup"><span data-stu-id="376ea-170">Close **StorageSample** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="376ea-171">Hallo volgt Hallo volledige code voor dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="376ea-171">hello following is hello complete code for this example.</span></span> <span data-ttu-id="376ea-172">Vergeet niet de waarden van de tijdelijke aanduiding Hallo toomodify **uw\_account\_naam** en **uw\_account\_sleutel** toouse uw accountnaam en -account sleutel, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="376ea-172">Remember toomodify hello placeholder values **your\_account\_name** and **your\_account\_key** toouse your account name and account key, respectively.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;

// Create an image, c:\myimages\image1.jpg, prior toorunning this sample.
// Alternatively, change hello value used by hello FileInputStream constructor
// toouse a different image path and file that you have already created.
public class StorageSample {

    public static final String storageConnectionString =
            "DefaultEndpointsProtocol=http;" +
                    "AccountName=your_account_name;" +
                    "AccountKey=your_account_name";

    public static void main(String[] args) {
        try {
            CloudStorageAccount account;
            CloudBlobClient serviceClient;
            CloudBlobContainer container;
            CloudBlockBlob blob;

            account = CloudStorageAccount.parse(storageConnectionString);
            serviceClient = account.createCloudBlobClient();
            // Container name must be lower case.
            container = serviceClient.getContainerReference("gettingstarted");
            container.createIfNotExists();

            // Set anonymous access on hello container.
            BlobContainerPermissions containerPermissions;
            containerPermissions = new BlobContainerPermissions();
            containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
            container.uploadPermissions(containerPermissions);

            // Upload an image file.
            blob = container.getBlockBlobReference("image1.jpg");

            File fileReference = new File("c:\\myimages\\image1.jpg");
            blob.upload(new FileInputStream(fileReference), fileReference.length());

            // At this point hello image is uploaded.
            // Next, create an HTML page that lists all of hello uploaded images.
            MakeHTMLPage(container);

            System.out.println("Processing complete.");
            System.out.println("Open index.html toosee hello images stored in your storage account.");

        } catch (FileNotFoundException fileNotFoundException) {
            System.out.print("FileNotFoundException encountered: ");
            System.out.println(fileNotFoundException.getMessage());
            System.exit(-1);
        } catch (StorageException storageException) {
            System.out.print("StorageException encountered: ");
            System.out.println(storageException.getMessage());
            System.exit(-1);
        } catch (URISyntaxException uriSyntaxException) {
            System.out.print("URISyntaxException encountered: ");
            System.out.println(uriSyntaxException.getMessage());
            System.exit(-1);
        } catch (Exception e) {
            System.out.print("Exception encountered: ");
            System.out.println(e.getMessage());
            System.exit(-1);
        }
    }

    // Create an HTML page that can be used toodisplay hello uploaded images.
    // This example assumes all of hello blobs are for images.
    public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
    {
        PrintStream stream;
        stream = new PrintStream(new FileOutputStream("index.html"));

        // Create hello opening <html>, <header>, and <body> elements.
        stream.println("<html>");
        stream.println("<header/>");
        stream.println("<body>");

        // Enumerate hello uploaded blobs.
        for (ListBlobItem blobItem : container.listBlobs()) {
            // List each blob as an <img> element in hello HTML body.
            stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
        }

        stream.println("</body>");

        // Complete hello <html> element and close hello file.
        stream.println("</html>");
        stream.close();
    }
}
```

<span data-ttu-id="376ea-173">In aanvulling toouploading uw afbeelding voor lokaal tooAzure bestandsopslag Hallo voorbeeldcode wordt gemaakt een lokaal bestand namedindex.html, die u in uw browser toosee openen kunt uw geüploade installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="376ea-173">In addition toouploading your local image file tooAzure storage, hello example code creates a local file namedindex.html, which you can open in your browser toosee your uploaded image.</span></span>

<span data-ttu-id="376ea-174">Omdat het Hallo-code bevat uw accountnaam en accountsleutel, zorg ervoor dat de broncode beveiligd is.</span><span class="sxs-lookup"><span data-stu-id="376ea-174">Because hello code contains your account name and account key, ensure that your source code is secure.</span></span>

## <a name="toodelete-a-container"></a><span data-ttu-id="376ea-175">een container toodelete</span><span class="sxs-lookup"><span data-stu-id="376ea-175">toodelete a container</span></span>
<span data-ttu-id="376ea-176">Omdat u in rekening voor opslag gebracht, kunt u toodelete de **gettingstarted** container nadat u klaar bent met het volgende voorbeeld experimenteren.</span><span class="sxs-lookup"><span data-stu-id="376ea-176">Because you are charged for storage, you may want toodelete the **gettingstarted** container after you are done experimenting with this example.</span></span> <span data-ttu-id="376ea-177">toodelete een container gebruiken Hallo **CloudBlobContainer.delete** methode.</span><span class="sxs-lookup"><span data-stu-id="376ea-177">toodelete a container, use hello **CloudBlobContainer.delete** method.</span></span>

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

<span data-ttu-id="376ea-178">Hallo toocall **CloudBlobContainer.delete** methode, Hallo-proces voor het initialiseren van **CloudStorageAccount**, **ClodBlobClient**, en  **CloudBlobContainer** objecten is Hallo dezelfde zoals weergegeven voor de **createIfNotExist** methode.</span><span class="sxs-lookup"><span data-stu-id="376ea-178">toocall hello **CloudBlobContainer.delete** method, hello process of initializing **CloudStorageAccount**, **ClodBlobClient**, and **CloudBlobContainer** objects is hello same as shown for the **createIfNotExist** method.</span></span> <span data-ttu-id="376ea-179">Hallo Hier volgt een voorbeeld van een volledige dat Hiermee verwijdert u de container met de naam Hallo **gettingstarted**.</span><span class="sxs-lookup"><span data-stu-id="376ea-179">hello following is a complete example that deletes hello container named **gettingstarted**.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;

public class DeleteContainer {

    public static final String storageConnectionString =
            "DefaultEndpointsProtocol=http;" +
                "AccountName=your_account_name;" +
                "AccountKey=your_account_key";

    public static void main(String[] args)
    {
        try
        {
            CloudStorageAccount account;
            CloudBlobClient serviceClient;
            CloudBlobContainer container;

            account = CloudStorageAccount.parse(storageConnectionString);
            serviceClient = account.createCloudBlobClient();
            // Container name must be lower case.
            container = serviceClient.getContainerReference("gettingstarted");
            container.delete();

            System.out.println("Container deleted.");

        }
        catch (StorageException storageException)
        {
            System.out.print("StorageException encountered: ");
            System.out.println(storageException.getMessage());
            System.exit(-1);
        }
        catch (Exception e)
        {
            System.out.print("Exception encountered: ");
            System.out.println(e.getMessage());
            System.exit(-1);
        }
    }
}
```

<span data-ttu-id="376ea-180">Zie voor een overzicht van andere blob-opslag-klassen en methoden [hoe toouse Blob-opslag met Java](storage-java-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="376ea-180">For an overview of other blob storage classes and methods, see [How toouse Blob storage from Java](storage-java-how-to-use-blob-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="376ea-181">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="376ea-181">Next steps</span></span>
<span data-ttu-id="376ea-182">Volg deze koppelingen toolearn meer informatie over complexere opslagtaken.</span><span class="sxs-lookup"><span data-stu-id="376ea-182">Follow these links toolearn more about more complex storage tasks.</span></span>

* [<span data-ttu-id="376ea-183">Azure-opslag-SDK voor Java</span><span class="sxs-lookup"><span data-stu-id="376ea-183">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="376ea-184">Azure Storage Client SDK-naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="376ea-184">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="376ea-185">REST-API voor Azure Storage-services</span><span class="sxs-lookup"><span data-stu-id="376ea-185">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="376ea-186">Blog van het Azure Storage-team</span><span class="sxs-lookup"><span data-stu-id="376ea-186">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)

