---
title: Lokale toepassing met blob storage (Java) | Microsoft Docs
description: Informatie over het maken van een consoletoepassing die een afbeelding uploadt naar Azure en vervolgens de installatiekopie in de browser weergegeven. Codevoorbeelden in Java.
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
ms.openlocfilehash: a172b881fa38a69f4510df94f5797b7a56940c52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="on-premises-application-with-blob-storage"></a><span data-ttu-id="dc10c-104">On-premises toepassing met blob storage</span><span class="sxs-lookup"><span data-stu-id="dc10c-104">On-premises application with blob storage</span></span>
## <a name="overview"></a><span data-ttu-id="dc10c-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="dc10c-105">Overview</span></span>
<span data-ttu-id="dc10c-106">Het volgende voorbeeld ziet u hoe u Azure-opslag kunt gebruiken voor het opslaan van afbeeldingen in Azure.</span><span class="sxs-lookup"><span data-stu-id="dc10c-106">The following example shows you how you can use Azure storage to store images in Azure.</span></span> <span data-ttu-id="dc10c-107">De code in dit artikel is bedoeld voor een consoletoepassing die een afbeelding uploadt naar Azure en maakt vervolgens een HTML-bestand waarin de installatiekopie worden weergegeven in uw browser.</span><span class="sxs-lookup"><span data-stu-id="dc10c-107">The code in this article is for a console application that uploads an image to Azure, and then creates an HTML file that displays the image in your browser.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc10c-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="dc10c-108">Prerequisites</span></span>
* <span data-ttu-id="dc10c-109">Een Java Developer Kit (JDK), versie 1.6 of hoger is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="dc10c-109">A Java Developer Kit (JDK), version 1.6 or later, is installed.</span></span>
* <span data-ttu-id="dc10c-110">De Azure SDK is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="dc10c-110">The Azure SDK is installed.</span></span>
* <span data-ttu-id="dc10c-111">De JAR voor de Azure-beheerbibliotheken voor Java, en eventuele potten afhankelijkheid van toepassing zijn geïnstalleerd en worden in de build pad dat wordt gebruikt door uw Java-compiler.</span><span class="sxs-lookup"><span data-stu-id="dc10c-111">The JAR for the Azure Libraries for Java, and any applicable dependency JARs, are installed and are in the build path used by your Java compiler.</span></span> <span data-ttu-id="dc10c-112">Zie voor meer informatie over het installeren van de Azure-beheerbibliotheken voor Java [downloaden van de Azure SDK voor Java](../java-download-azure-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="dc10c-112">For information about installing the Azure Libraries for Java, see [Download the Azure SDK for Java](../java-download-azure-sdk.md).</span></span>
* <span data-ttu-id="dc10c-113">Een Azure storage-account is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="dc10c-113">An Azure storage account has been set up.</span></span> <span data-ttu-id="dc10c-114">De accountnaam en accountsleutel voor het opslagaccount wordt gebruikt door de code in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="dc10c-114">The account name and account key for the storage account will be used by the code in this article.</span></span> <span data-ttu-id="dc10c-115">Zie [het maken van een Opslagaccount](storage-create-storage-account.md#create-a-storage-account) voor informatie over het maken van een opslagaccount en [weergeven en kopiëren opslagtoegangssleutels](storage-create-storage-account.md#view-and-copy-storage-access-keys) voor informatie over het ophalen van de accountsleutel.</span><span class="sxs-lookup"><span data-stu-id="dc10c-115">See [How to Create a Storage Account](storage-create-storage-account.md#create-a-storage-account) for information about creating a storage account, and [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys) for information about retrieving the account key.</span></span>
* <span data-ttu-id="dc10c-116">U hebt gemaakt een lokaal bestand met de naam opgeslagen in het pad c:\\myimages\\image1.jpg.</span><span class="sxs-lookup"><span data-stu-id="dc10c-116">You have created a local image file named stored at the path c:\\myimages\\image1.jpg.</span></span> <span data-ttu-id="dc10c-117">U kunt ook wijzigen de **FileInputStream** constructor in het voorbeeld in een andere installatiekopie pad en de bestandsnaam de naam te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="dc10c-117">Alternatively, modify the **FileInputStream** constructor in the example to use a different image path and file name.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="to-use-azure-blob-storage-to-upload-a-file"></a><span data-ttu-id="dc10c-118">Azure blob storage gebruiken om een bestand te uploaden</span><span class="sxs-lookup"><span data-stu-id="dc10c-118">To use Azure blob storage to upload a file</span></span>
<span data-ttu-id="dc10c-119">Een stapsgewijze procedure die hier voorgesteld.</span><span class="sxs-lookup"><span data-stu-id="dc10c-119">A step-by-step procedure is presented here.</span></span> <span data-ttu-id="dc10c-120">Als u overslaan wilt, wordt de volledige code weergegeven verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="dc10c-120">If you'd like to skip ahead, the entire code is presented later in this article.</span></span>

<span data-ttu-id="dc10c-121">Beginnen met de code door te nemen van invoer voor de opslag Azure core klassen, de klassen van Azure blob-client, de Java-i/o-klassen en de **URISyntaxException** klasse.</span><span class="sxs-lookup"><span data-stu-id="dc10c-121">Begin the code by including imports for the Azure core storage classes, the Azure blob client classes, the Java IO classes, and the **URISyntaxException** class.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

<span data-ttu-id="dc10c-122">Een klasse met de naam declareert **StorageSample**, en omvatten het open haakje **{**.</span><span class="sxs-lookup"><span data-stu-id="dc10c-122">Declare a class named **StorageSample**, and include the open bracket, **{**.</span></span>

```java
public class StorageSample {
```

<span data-ttu-id="dc10c-123">Binnen de **StorageSample** klasse, declareert u een string-variabele waarin u het eindpunt standaardprotocol, naam van uw opslagaccount en uw toegangssleutel voor opslag, zoals opgegeven in uw Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="dc10c-123">Within the **StorageSample** class, declare a string variable that will contain the default endpoint protocol, your storage account name, and your storage access key, as specified in your Azure storage account.</span></span> <span data-ttu-id="dc10c-124">Vervang de tijdelijke aanduiding voor waarden **uw\_account\_naam** en **uw\_account\_sleutel** met uw eigen accountnaam en accountsleutel, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="dc10c-124">Replace the placeholder values **your\_account\_name** and **your\_account\_key** with your own account name and account key, respectively.</span></span>

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

<span data-ttu-id="dc10c-125">Toevoegen aan uw-declaratie voor **belangrijkste**, bevatten een **probeer** blokkeren en de benodigde open vierkante haken, omvatten **{**.</span><span class="sxs-lookup"><span data-stu-id="dc10c-125">Add in your declaration for **main**, include a **try** block, and include the necessary open brackets, **{**.</span></span>

```java
    public static void main(String[] args)
    {
        try
        {
```

<span data-ttu-id="dc10c-126">Declareer de variabelen van het volgende type (voor hoe ze worden gebruikt in dit voorbeeld zijn de beschrijvingen):</span><span class="sxs-lookup"><span data-stu-id="dc10c-126">Declare variables of the following type (the descriptions are for how they are used in this example):</span></span>

* <span data-ttu-id="dc10c-127">**CloudStorageAccount**: gebruikt voor het initialiseren van het object rekening met uw Azure-opslag-accountnaam en de sleutel en het blob-client-object te maken.</span><span class="sxs-lookup"><span data-stu-id="dc10c-127">**CloudStorageAccount**: Used to initialize the account object with your Azure storage account name and key, and to create the blob client object.</span></span>
* <span data-ttu-id="dc10c-128">**CloudBlobClient**: gebruikt voor toegang tot de blob-service.</span><span class="sxs-lookup"><span data-stu-id="dc10c-128">**CloudBlobClient**: Used to access the blob service.</span></span>
* <span data-ttu-id="dc10c-129">**CloudBlobContainer**: gebruikt voor het maken van een blob-container, de blobs in de container weergeven en verwijderen van container.</span><span class="sxs-lookup"><span data-stu-id="dc10c-129">**CloudBlobContainer**: Used to create a blob container, list the blobs in the container, and delete the container.</span></span>
* <span data-ttu-id="dc10c-130">**CloudBlockBlob**: gebruikt voor het uploaden van een afbeelding voor lokaal bestand naar de container.</span><span class="sxs-lookup"><span data-stu-id="dc10c-130">**CloudBlockBlob**: Used to upload a local image file to the container.</span></span>

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

<span data-ttu-id="dc10c-131">Een waarde toewijzen aan de **account** variabele.</span><span class="sxs-lookup"><span data-stu-id="dc10c-131">Assign a value to the **account** variable.</span></span>

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

<span data-ttu-id="dc10c-132">Een waarde toewijzen aan de **serviceClient** variabele.</span><span class="sxs-lookup"><span data-stu-id="dc10c-132">Assign a value to the **serviceClient** variable.</span></span>

```java
serviceClient = account.createCloudBlobClient();
```

<span data-ttu-id="dc10c-133">Een waarde toewijzen aan de **container** variabele.</span><span class="sxs-lookup"><span data-stu-id="dc10c-133">Assign a value to the **container** variable.</span></span> <span data-ttu-id="dc10c-134">Je krijgt een verwijzing naar een container met de naam **gettingstarted**.</span><span class="sxs-lookup"><span data-stu-id="dc10c-134">We'll get a reference to a container named **gettingstarted**.</span></span>

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

<span data-ttu-id="dc10c-135">De container maken.</span><span class="sxs-lookup"><span data-stu-id="dc10c-135">Create the container.</span></span> <span data-ttu-id="dc10c-136">Deze methode maakt u de container als deze niet bestaat (en terug te keren **true**).</span><span class="sxs-lookup"><span data-stu-id="dc10c-136">This method will create the container if it doesn't exist (and return **true**).</span></span> <span data-ttu-id="dc10c-137">Als de container bestaat, wordt geretourneerd **false**.</span><span class="sxs-lookup"><span data-stu-id="dc10c-137">If the container does exist, it will return **false**.</span></span> <span data-ttu-id="dc10c-138">Een alternatief voor **createIfNotExists** is de **maken** methode (die retourneren een foutmelding als de container al bestaat).</span><span class="sxs-lookup"><span data-stu-id="dc10c-138">An alternative to **createIfNotExists** is the **create** method (which will return an error if the container already exists).</span></span>

```java
container.createIfNotExists();
```

<span data-ttu-id="dc10c-139">Anonieme toegang instellen voor de container.</span><span class="sxs-lookup"><span data-stu-id="dc10c-139">Set anonymous access for the container.</span></span>

```java
// Set anonymous access on the container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

<span data-ttu-id="dc10c-140">Een verwijzing naar de blok-blob die staat voor de blob in Azure-opslag ophalen.</span><span class="sxs-lookup"><span data-stu-id="dc10c-140">Get a reference to the block blob, which will represent the blob in Azure storage.</span></span>

```java
blob = container.getBlockBlobReference("image1.jpg");
```

<span data-ttu-id="dc10c-141">Gebruik de **bestand** constructor voor het ophalen van een verwijzing naar het lokaal bestand dat u zult uploaden.</span><span class="sxs-lookup"><span data-stu-id="dc10c-141">Use the **File** constructor to get a reference to the locally created file that you will upload.</span></span> <span data-ttu-id="dc10c-142">Zorg ervoor dat u dit bestand hebt gemaakt voordat de code wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="dc10c-142">Ensure you have created this file before running the code.</span></span>

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

<span data-ttu-id="dc10c-143">Upload het lokale bestand via een aanroep van de **CloudBlockBlob.upload** methode.</span><span class="sxs-lookup"><span data-stu-id="dc10c-143">Upload the local file through a call to the **CloudBlockBlob.upload** method.</span></span> <span data-ttu-id="dc10c-144">De eerste parameter voor de **CloudBlockBlob.upload** methode is een **FileInputStream** -object met het lokale bestand dat wordt geüpload naar Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="dc10c-144">The first parameter to the **CloudBlockBlob.upload** method is a **FileInputStream** object that represents the local file that will be uploaded to Azure storage.</span></span> <span data-ttu-id="dc10c-145">De tweede parameter is de grootte, in bytes, van het bestand.</span><span class="sxs-lookup"><span data-stu-id="dc10c-145">The second parameter is the size, in bytes, of the file.</span></span>

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

<span data-ttu-id="dc10c-146">Aanroepen van een Help-functie met de naam **MakeHTMLPage**om er een eenvoudige HTML-pagina met een  **&lt;installatiekopie&gt;**  element met de bron ingesteld op de blob die nu in uw Azure-opslag account.</span><span class="sxs-lookup"><span data-stu-id="dc10c-146">Call a helper function named **MakeHTMLPage**, to make a basic HTML page that contains an **&lt;image&gt;** element with the source set to the blob that is now in your Azure storage account.</span></span> <span data-ttu-id="dc10c-147">De code voor **MakeHTMLPage** wordt verderop in dit artikel worden besproken.</span><span class="sxs-lookup"><span data-stu-id="dc10c-147">The code for **MakeHTMLPage** will be discussed later in this article.</span></span>

```java
MakeHTMLPage(container);
```

<span data-ttu-id="dc10c-148">Een statusbericht en informatie over de gemaakte HTML-pagina afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="dc10c-148">Print out a status message and information about the created HTML page.</span></span>

```java
System.out.println("Processing complete.");
System.out.println("Open index.html to see the images stored in your storage account.");
```

<span data-ttu-id="dc10c-149">Sluit de **probeer** blokkeren door het invoegen van een haakje sluiten: **}**</span><span class="sxs-lookup"><span data-stu-id="dc10c-149">Close the **try** block by inserting a close bracket: **}**</span></span>

<span data-ttu-id="dc10c-150">Verwerken van de volgende uitzonderingen:</span><span class="sxs-lookup"><span data-stu-id="dc10c-150">Handle the following exceptions:</span></span>

* <span data-ttu-id="dc10c-151">**FileNotFoundException**: kan worden gegenereerd door de **FileInputStream** of **FileOutputStream** constructors.</span><span class="sxs-lookup"><span data-stu-id="dc10c-151">**FileNotFoundException**: Can be thrown by the **FileInputStream** or **FileOutputStream** constructors.</span></span>
* <span data-ttu-id="dc10c-152">**StorageException**: kan worden gegenereerd door de Azure storage-clientbibliotheek.</span><span class="sxs-lookup"><span data-stu-id="dc10c-152">**StorageException**: Can be thrown by the Azure client storage library.</span></span>
* <span data-ttu-id="dc10c-153">**URISyntaxException**: kan worden gegenereerd door de **ListBlobItem.getUri** methode.</span><span class="sxs-lookup"><span data-stu-id="dc10c-153">**URISyntaxException**: Can be thrown by the **ListBlobItem.getUri** method.</span></span>
* <span data-ttu-id="dc10c-154">**Uitzondering**: algemene uitzonderingsverwerking.</span><span class="sxs-lookup"><span data-stu-id="dc10c-154">**Exception**: Generic exception handling.</span></span>

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

<span data-ttu-id="dc10c-155">Sluit **belangrijkste** door het invoegen van een haakje sluiten: **}**</span><span class="sxs-lookup"><span data-stu-id="dc10c-155">Close **main** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="dc10c-156">Maken van een methode met de naam **MakeHTMLPage** voor het maken van een standaard HTML-pagina.</span><span class="sxs-lookup"><span data-stu-id="dc10c-156">Create a method named **MakeHTMLPage** to create a basic HTML page.</span></span> <span data-ttu-id="dc10c-157">Deze methode heeft een parameter van het type **CloudBlobContainer**, die wordt gebruikt om de lijst met geüploade BLOB's doorlopen.</span><span class="sxs-lookup"><span data-stu-id="dc10c-157">This method has a parameter of type **CloudBlobContainer**, which will be used to iterate through the list of uploaded blobs.</span></span> <span data-ttu-id="dc10c-158">Deze methode genereert uitzonderingen van het type **FileNotFoundException**, die kan worden gegenereerd door de **FileOutputStream** -constructor aan, en **URISyntaxException**, wat kan zijn gegenereerd door de **ListBlobItem.getUri** methode.</span><span class="sxs-lookup"><span data-stu-id="dc10c-158">This method will throw exceptions of type **FileNotFoundException**, which can be thrown by the **FileOutputStream** constructor, and **URISyntaxException**, which can be thrown by the **ListBlobItem.getUri** method.</span></span> <span data-ttu-id="dc10c-159">Het openingshaakje omvatten **{**.</span><span class="sxs-lookup"><span data-stu-id="dc10c-159">Include the opening bracket, **{**.</span></span>

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

<span data-ttu-id="dc10c-160">Maken van een lokaal bestand met de naam **index.html**.</span><span class="sxs-lookup"><span data-stu-id="dc10c-160">Create a local file named **index.html**.</span></span>

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

<span data-ttu-id="dc10c-161">Schrijven naar het lokale bestand, toe te voegen aan de  **&lt;html&gt;**,  **&lt;header&gt;**, en  **&lt;hoofdtekst&gt;**  elementen.</span><span class="sxs-lookup"><span data-stu-id="dc10c-161">Write to the local file, adding in the **&lt;html&gt;**, **&lt;header&gt;**, and **&lt;body&gt;** elements.</span></span>

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

<span data-ttu-id="dc10c-162">De lijst met geüploade BLOB's doorlopen.</span><span class="sxs-lookup"><span data-stu-id="dc10c-162">Iterate through the list of uploaded blobs.</span></span> <span data-ttu-id="dc10c-163">Voor elke blob in de HTML-pagina maken een  **&lt;img&gt;**  -element waarvoor de **src** kenmerk verzonden naar de URI van de blob, zoals dit zich in uw Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="dc10c-163">For each blob, in the HTML page create an **&lt;img&gt;** element that has its **src** attribute sent to the URI of the blob as it exists in your Azure storage account.</span></span>
<span data-ttu-id="dc10c-164">Hoewel u slechts één installatiekopie in dit voorbeeld wordt toegevoegd als u meer hebt toegevoegd, zou deze code allemaal herhalen.</span><span class="sxs-lookup"><span data-stu-id="dc10c-164">Although you added only one image in this sample, if you added more, this code would iterate all of them.</span></span>

<span data-ttu-id="dc10c-165">Voor eenvoud, in dit voorbeeld wordt ervan uitgegaan dat elke geüploade blob is een afbeelding.</span><span class="sxs-lookup"><span data-stu-id="dc10c-165">For simplicity, this example assumes each uploaded blob is an image.</span></span> <span data-ttu-id="dc10c-166">Als u blobs dan afbeeldingen of pagina-blobs in plaats van blok-blobs hebt bijgewerkt, de code naar wens aanpassen.</span><span class="sxs-lookup"><span data-stu-id="dc10c-166">If you've updated blobs other than images, or page blobs instead of block blobs, adjust the code as needed.</span></span>

```java
// Enumerate the uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in the HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

<span data-ttu-id="dc10c-167">Sluit de  **&lt;hoofdtekst&gt;**  element en de  **&lt;html&gt;**  element.</span><span class="sxs-lookup"><span data-stu-id="dc10c-167">Close the **&lt;body&gt;** element and the **&lt;html&gt;** element.</span></span>

```java
stream.println("</body>");
stream.println("</html>");
```

<span data-ttu-id="dc10c-168">Sluit het lokale bestand.</span><span class="sxs-lookup"><span data-stu-id="dc10c-168">Close the local file.</span></span>

```java
stream.close();
```

<span data-ttu-id="dc10c-169">Sluit **MakeHTMLPage** door het invoegen van een haakje sluiten: **}**</span><span class="sxs-lookup"><span data-stu-id="dc10c-169">Close **MakeHTMLPage** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="dc10c-170">Sluit **StorageSample** door het invoegen van een haakje sluiten: **}**</span><span class="sxs-lookup"><span data-stu-id="dc10c-170">Close **StorageSample** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="dc10c-171">Hieronder volgt de volledige code voor dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="dc10c-171">The following is the complete code for this example.</span></span> <span data-ttu-id="dc10c-172">Houd er rekening mee te wijzigen van de tijdelijke aanduiding voor waarden **uw\_account\_naam** en **uw\_account\_sleutel** uw accountnaam en accountsleutel, gebruiken respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="dc10c-172">Remember to modify the placeholder values **your\_account\_name** and **your\_account\_key** to use your account name and account key, respectively.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;

// Create an image, c:\myimages\image1.jpg, prior to running this sample.
// Alternatively, change the value used by the FileInputStream constructor
// to use a different image path and file that you have already created.
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

            // Set anonymous access on the container.
            BlobContainerPermissions containerPermissions;
            containerPermissions = new BlobContainerPermissions();
            containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
            container.uploadPermissions(containerPermissions);

            // Upload an image file.
            blob = container.getBlockBlobReference("image1.jpg");

            File fileReference = new File("c:\\myimages\\image1.jpg");
            blob.upload(new FileInputStream(fileReference), fileReference.length());

            // At this point the image is uploaded.
            // Next, create an HTML page that lists all of the uploaded images.
            MakeHTMLPage(container);

            System.out.println("Processing complete.");
            System.out.println("Open index.html to see the images stored in your storage account.");

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

    // Create an HTML page that can be used to display the uploaded images.
    // This example assumes all of the blobs are for images.
    public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
    {
        PrintStream stream;
        stream = new PrintStream(new FileOutputStream("index.html"));

        // Create the opening <html>, <header>, and <body> elements.
        stream.println("<html>");
        stream.println("<header/>");
        stream.println("<body>");

        // Enumerate the uploaded blobs.
        for (ListBlobItem blobItem : container.listBlobs()) {
            // List each blob as an <img> element in the HTML body.
            stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
        }

        stream.println("</body>");

        // Complete the <html> element and close the file.
        stream.println("</html>");
        stream.close();
    }
}
```

<span data-ttu-id="dc10c-173">De voorbeeldcode maakt naast uw afbeelding voor lokaal bestand uploaden naar Azure storage, een lokaal bestand namedindex.html, die u kunt openen in uw browser om te zien van uw geüploade installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="dc10c-173">In addition to uploading your local image file to Azure storage, the example code creates a local file namedindex.html, which you can open in your browser to see your uploaded image.</span></span>

<span data-ttu-id="dc10c-174">Omdat de code uw accountnaam en accountsleutel bevat, zorg ervoor dat de broncode beveiligd is.</span><span class="sxs-lookup"><span data-stu-id="dc10c-174">Because the code contains your account name and account key, ensure that your source code is secure.</span></span>

## <a name="to-delete-a-container"></a><span data-ttu-id="dc10c-175">Een container</span><span class="sxs-lookup"><span data-stu-id="dc10c-175">To delete a container</span></span>
<span data-ttu-id="dc10c-176">Omdat u in rekening voor opslag gebracht, kunt u verwijderen de **gettingstarted** container nadat u klaar bent met het volgende voorbeeld experimenteren.</span><span class="sxs-lookup"><span data-stu-id="dc10c-176">Because you are charged for storage, you may want to delete the **gettingstarted** container after you are done experimenting with this example.</span></span> <span data-ttu-id="dc10c-177">Als u wilt verwijderen van een container, gebruiken de **CloudBlobContainer.delete** methode.</span><span class="sxs-lookup"><span data-stu-id="dc10c-177">To delete a container, use the **CloudBlobContainer.delete** method.</span></span>

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

<span data-ttu-id="dc10c-178">Om aan te roepen de **CloudBlobContainer.delete** methode, het proces voor het initialiseren van **CloudStorageAccount**, **ClodBlobClient**, en **CloudBlobContainer**  objecten is hetzelfde als weergegeven voor de **createIfNotExist** methode.</span><span class="sxs-lookup"><span data-stu-id="dc10c-178">To call the **CloudBlobContainer.delete** method, the process of initializing **CloudStorageAccount**, **ClodBlobClient**, and **CloudBlobContainer** objects is the same as shown for the **createIfNotExist** method.</span></span> <span data-ttu-id="dc10c-179">Hieronder volgt een voorbeeld van een volledige die worden verwijderd van de container met de naam **gettingstarted**.</span><span class="sxs-lookup"><span data-stu-id="dc10c-179">The following is a complete example that deletes the container named **gettingstarted**.</span></span>

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

<span data-ttu-id="dc10c-180">Zie voor een overzicht van andere blob-opslag-klassen en methoden [hoe Blob storage gebruiken met Java](storage-java-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="dc10c-180">For an overview of other blob storage classes and methods, see [How to use Blob storage from Java](storage-java-how-to-use-blob-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc10c-181">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dc10c-181">Next steps</span></span>
<span data-ttu-id="dc10c-182">Volg deze koppelingen voor meer informatie over complexere opslagtaken.</span><span class="sxs-lookup"><span data-stu-id="dc10c-182">Follow these links to learn more about more complex storage tasks.</span></span>

* [<span data-ttu-id="dc10c-183">Azure-opslag-SDK voor Java</span><span class="sxs-lookup"><span data-stu-id="dc10c-183">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="dc10c-184">Azure Storage Client SDK-naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="dc10c-184">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="dc10c-185">REST-API voor Azure Storage-services</span><span class="sxs-lookup"><span data-stu-id="dc10c-185">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="dc10c-186">Blog van het Azure Storage-team</span><span class="sxs-lookup"><span data-stu-id="dc10c-186">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)

