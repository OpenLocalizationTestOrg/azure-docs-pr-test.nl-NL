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
# <a name="on-premises-application-with-blob-storage"></a>On-premises toepassing met blob storage
## <a name="overview"></a>Overzicht
Het volgende voorbeeld ziet u hoe u Azure-opslag kunt gebruiken voor het opslaan van afbeeldingen in Azure. De code in dit artikel is bedoeld voor een consoletoepassing die een afbeelding uploadt naar Azure en maakt vervolgens een HTML-bestand waarin de installatiekopie worden weergegeven in uw browser.

## <a name="prerequisites"></a>Vereisten
* Een Java Developer Kit (JDK), versie 1.6 of hoger is geïnstalleerd.
* De Azure SDK is geïnstalleerd.
* De JAR voor de Azure-beheerbibliotheken voor Java, en eventuele potten afhankelijkheid van toepassing zijn geïnstalleerd en worden in de build pad dat wordt gebruikt door uw Java-compiler. Zie voor meer informatie over het installeren van de Azure-beheerbibliotheken voor Java [downloaden van de Azure SDK voor Java](../java-download-azure-sdk.md).
* Een Azure storage-account is ingesteld. De accountnaam en accountsleutel voor het opslagaccount wordt gebruikt door de code in dit artikel. Zie [het maken van een Opslagaccount](storage-create-storage-account.md#create-a-storage-account) voor informatie over het maken van een opslagaccount en [weergeven en kopiëren opslagtoegangssleutels](storage-create-storage-account.md#view-and-copy-storage-access-keys) voor informatie over het ophalen van de accountsleutel.
* U hebt gemaakt een lokaal bestand met de naam opgeslagen in het pad c:\\myimages\\image1.jpg. U kunt ook wijzigen de **FileInputStream** constructor in het voorbeeld in een andere installatiekopie pad en de bestandsnaam de naam te gebruiken.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="to-use-azure-blob-storage-to-upload-a-file"></a>Azure blob storage gebruiken om een bestand te uploaden
Een stapsgewijze procedure die hier voorgesteld. Als u overslaan wilt, wordt de volledige code weergegeven verderop in dit artikel.

Beginnen met de code door te nemen van invoer voor de opslag Azure core klassen, de klassen van Azure blob-client, de Java-i/o-klassen en de **URISyntaxException** klasse.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

Een klasse met de naam declareert **StorageSample**, en omvatten het open haakje **{**.

```java
public class StorageSample {
```

Binnen de **StorageSample** klasse, declareert u een string-variabele waarin u het eindpunt standaardprotocol, naam van uw opslagaccount en uw toegangssleutel voor opslag, zoals opgegeven in uw Azure storage-account. Vervang de tijdelijke aanduiding voor waarden **uw\_account\_naam** en **uw\_account\_sleutel** met uw eigen accountnaam en accountsleutel, respectievelijk.

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

Toevoegen aan uw-declaratie voor **belangrijkste**, bevatten een **probeer** blokkeren en de benodigde open vierkante haken, omvatten **{**.

```java
    public static void main(String[] args)
    {
        try
        {
```

Declareer de variabelen van het volgende type (voor hoe ze worden gebruikt in dit voorbeeld zijn de beschrijvingen):

* **CloudStorageAccount**: gebruikt voor het initialiseren van het object rekening met uw Azure-opslag-accountnaam en de sleutel en het blob-client-object te maken.
* **CloudBlobClient**: gebruikt voor toegang tot de blob-service.
* **CloudBlobContainer**: gebruikt voor het maken van een blob-container, de blobs in de container weergeven en verwijderen van container.
* **CloudBlockBlob**: gebruikt voor het uploaden van een afbeelding voor lokaal bestand naar de container.

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

Een waarde toewijzen aan de **account** variabele.

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

Een waarde toewijzen aan de **serviceClient** variabele.

```java
serviceClient = account.createCloudBlobClient();
```

Een waarde toewijzen aan de **container** variabele. Je krijgt een verwijzing naar een container met de naam **gettingstarted**.

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

De container maken. Deze methode maakt u de container als deze niet bestaat (en terug te keren **true**). Als de container bestaat, wordt geretourneerd **false**. Een alternatief voor **createIfNotExists** is de **maken** methode (die retourneren een foutmelding als de container al bestaat).

```java
container.createIfNotExists();
```

Anonieme toegang instellen voor de container.

```java
// Set anonymous access on the container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

Een verwijzing naar de blok-blob die staat voor de blob in Azure-opslag ophalen.

```java
blob = container.getBlockBlobReference("image1.jpg");
```

Gebruik de **bestand** constructor voor het ophalen van een verwijzing naar het lokaal bestand dat u zult uploaden. Zorg ervoor dat u dit bestand hebt gemaakt voordat de code wordt uitgevoerd.

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

Upload het lokale bestand via een aanroep van de **CloudBlockBlob.upload** methode. De eerste parameter voor de **CloudBlockBlob.upload** methode is een **FileInputStream** -object met het lokale bestand dat wordt geüpload naar Azure-opslag. De tweede parameter is de grootte, in bytes, van het bestand.

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

Aanroepen van een Help-functie met de naam **MakeHTMLPage**om er een eenvoudige HTML-pagina met een  **&lt;installatiekopie&gt;**  element met de bron ingesteld op de blob die nu in uw Azure-opslag account. De code voor **MakeHTMLPage** wordt verderop in dit artikel worden besproken.

```java
MakeHTMLPage(container);
```

Een statusbericht en informatie over de gemaakte HTML-pagina afgedrukt.

```java
System.out.println("Processing complete.");
System.out.println("Open index.html to see the images stored in your storage account.");
```

Sluit de **probeer** blokkeren door het invoegen van een haakje sluiten: **}**

Verwerken van de volgende uitzonderingen:

* **FileNotFoundException**: kan worden gegenereerd door de **FileInputStream** of **FileOutputStream** constructors.
* **StorageException**: kan worden gegenereerd door de Azure storage-clientbibliotheek.
* **URISyntaxException**: kan worden gegenereerd door de **ListBlobItem.getUri** methode.
* **Uitzondering**: algemene uitzonderingsverwerking.

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

Sluit **belangrijkste** door het invoegen van een haakje sluiten: **}**

Maken van een methode met de naam **MakeHTMLPage** voor het maken van een standaard HTML-pagina. Deze methode heeft een parameter van het type **CloudBlobContainer**, die wordt gebruikt om de lijst met geüploade BLOB's doorlopen. Deze methode genereert uitzonderingen van het type **FileNotFoundException**, die kan worden gegenereerd door de **FileOutputStream** -constructor aan, en **URISyntaxException**, wat kan zijn gegenereerd door de **ListBlobItem.getUri** methode. Het openingshaakje omvatten **{**.

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

Maken van een lokaal bestand met de naam **index.html**.

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

Schrijven naar het lokale bestand, toe te voegen aan de  **&lt;html&gt;**,  **&lt;header&gt;**, en  **&lt;hoofdtekst&gt;**  elementen.

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

De lijst met geüploade BLOB's doorlopen. Voor elke blob in de HTML-pagina maken een  **&lt;img&gt;**  -element waarvoor de **src** kenmerk verzonden naar de URI van de blob, zoals dit zich in uw Azure storage-account.
Hoewel u slechts één installatiekopie in dit voorbeeld wordt toegevoegd als u meer hebt toegevoegd, zou deze code allemaal herhalen.

Voor eenvoud, in dit voorbeeld wordt ervan uitgegaan dat elke geüploade blob is een afbeelding. Als u blobs dan afbeeldingen of pagina-blobs in plaats van blok-blobs hebt bijgewerkt, de code naar wens aanpassen.

```java
// Enumerate the uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in the HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

Sluit de  **&lt;hoofdtekst&gt;**  element en de  **&lt;html&gt;**  element.

```java
stream.println("</body>");
stream.println("</html>");
```

Sluit het lokale bestand.

```java
stream.close();
```

Sluit **MakeHTMLPage** door het invoegen van een haakje sluiten: **}**

Sluit **StorageSample** door het invoegen van een haakje sluiten: **}**

Hieronder volgt de volledige code voor dit voorbeeld. Houd er rekening mee te wijzigen van de tijdelijke aanduiding voor waarden **uw\_account\_naam** en **uw\_account\_sleutel** uw accountnaam en accountsleutel, gebruiken respectievelijk.

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

De voorbeeldcode maakt naast uw afbeelding voor lokaal bestand uploaden naar Azure storage, een lokaal bestand namedindex.html, die u kunt openen in uw browser om te zien van uw geüploade installatiekopie.

Omdat de code uw accountnaam en accountsleutel bevat, zorg ervoor dat de broncode beveiligd is.

## <a name="to-delete-a-container"></a>Een container
Omdat u in rekening voor opslag gebracht, kunt u verwijderen de **gettingstarted** container nadat u klaar bent met het volgende voorbeeld experimenteren. Als u wilt verwijderen van een container, gebruiken de **CloudBlobContainer.delete** methode.

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

Om aan te roepen de **CloudBlobContainer.delete** methode, het proces voor het initialiseren van **CloudStorageAccount**, **ClodBlobClient**, en **CloudBlobContainer**  objecten is hetzelfde als weergegeven voor de **createIfNotExist** methode. Hieronder volgt een voorbeeld van een volledige die worden verwijderd van de container met de naam **gettingstarted**.

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

Zie voor een overzicht van andere blob-opslag-klassen en methoden [hoe Blob storage gebruiken met Java](storage-java-how-to-use-blob-storage.md).

## <a name="next-steps"></a>Volgende stappen
Volg deze koppelingen voor meer informatie over complexere opslagtaken.

* [Azure-opslag-SDK voor Java](https://github.com/azure/azure-storage-java)
* [Azure Storage Client SDK-naslaginformatie](http://dl.windowsazure.com/storage/javadoc/)
* [REST-API voor Azure Storage-services](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog van het Azure Storage-team](http://blogs.msdn.com/b/windowsazurestorage/)

