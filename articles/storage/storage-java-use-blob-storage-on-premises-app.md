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
# <a name="on-premises-application-with-blob-storage"></a>On-premises toepassing met blob storage
## <a name="overview"></a>Overzicht
Hallo volgende voorbeeld ziet u hoe u Azure-opslag kunt gebruiken voor het opslaan van afbeeldingen in Azure. Hallo-code in dit artikel is bedoeld voor een consoletoepassing die een tooAzure afbeelding uploadt en maakt vervolgens een HTML-bestand waarin Hallo afbeelding worden weergegeven in uw browser.

## <a name="prerequisites"></a>Vereisten
* Een Java Developer Kit (JDK), versie 1.6 of hoger is geïnstalleerd.
* Hello Azure SDK is geïnstalleerd.
* Hallo JAR voor hello Azure-beheerbibliotheken voor Java, en eventuele potten afhankelijkheid van toepassing zijn geïnstalleerd en in Hallo build pad dat wordt gebruikt door uw Java-compiler. Zie voor meer informatie over het installeren van hello Azure-beheerbibliotheken voor Java [downloaden hello Azure SDK voor Java](../java-download-azure-sdk.md).
* Een Azure storage-account is ingesteld. Hallo wordt accountnaam en accountsleutel voor Hallo storage-account gebruikt door Hallo-code in dit artikel. Zie [hoe tooCreate een Opslagaccount](storage-create-storage-account.md#create-a-storage-account) voor informatie over het maken van een opslagaccount en [weergeven en kopiëren opslagtoegangssleutels](storage-create-storage-account.md#view-and-copy-storage-access-keys) voor informatie over het Hallo-accountcode ophalen.
* U hebt gemaakt een lokaal bestand met de naam opgeslagen op Hallo pad c:\\myimages\\image1.jpg. U kunt ook wijzigen de **FileInputStream** Hallo voorbeeld toouse een andere installatiekopie pad en de naam-constructor.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="toouse-azure-blob-storage-tooupload-a-file"></a>toouse Azure blob storage tooupload een bestand
Een stapsgewijze procedure die hier voorgesteld. Als u tooskip vooruit wilt, is de volledige code Hallo verderop in dit artikel opgenomen.

Hallo code beginnen door Imports-instructie voor hello Azure core Opslagklassen, hello Azure blob-clientklassen, Hallo Java i/o-klassen en Hallo **URISyntaxException** klasse.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

Een klasse met de naam declareert **StorageSample**, en open haakje hello, bevatten **{**.

```java
public class StorageSample {
```

Binnen Hallo **StorageSample** klasse, declareert u een string-variabele die Hallo-standaardprotocol eindpunt, naam van uw opslagaccount en uw toegangssleutel voor opslag, zoals opgegeven in uw Azure storage-account bevat. Vervang de waarden van de tijdelijke aanduiding Hallo **uw\_account\_naam** en **uw\_account\_sleutel** met uw eigen accountnaam en accountsleutel, respectievelijk.

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

Toevoegen aan uw-declaratie voor **belangrijkste**, bevatten een **probeer** blokkeren en Hallo nodig open vierkante haken, omvatten **{**.

```java
    public static void main(String[] args)
    {
        try
        {
```

Declareer de variabelen Hallo type (hello beschrijvingen zijn voor hoe ze worden gebruikt in dit voorbeeld) te volgen:

* **CloudStorageAccount**: gebruikte tooinitialize Hallo accountobject met uw Azure-opslag-accountnaam en -sleutel en toocreate het blob-client-object.
* **CloudBlobClient**: tooaccess Hallo blob-service gebruikt.
* **CloudBlobContainer**: gebruikte toocreate een blob-container lijst de blobs in Hallo-container en delete Hallo container.
* **CloudBlockBlob**: gebruikte tooupload een afbeelding voor lokaal bestand toothe container.

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

Toewijzen van een waarde toohello **account** variabele.

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

Toewijzen van een waarde toohello **serviceClient** variabele.

```java
serviceClient = account.createCloudBlobClient();
```

Toewijzen van een waarde toohello **container** variabele. Je krijgt een verwijzing tooa container met de naam **gettingstarted**.

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

Hallo-container maken. Deze methode maakt Hallo container als deze niet bestaat (en terug te keren **true**). Als Hallo-container bestaat nog, wordt geretourneerd **false**. Een alternatief te**createIfNotExists** Hallo is **maken** methode (die retourneren een foutmelding als Hallo container al bestaat).

```java
container.createIfNotExists();
```

Anonieme toegang voor Hallo-container instellen.

```java
// Set anonymous access on hello container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

Haal een verwijzing toohello blok-blob, die Hallo blob in Azure-opslag vertegenwoordigt.

```java
blob = container.getBlockBlobReference("image1.jpg");
```

Gebruik Hallo **bestand** constructor tooget een referentiebestand toohello lokaal gemaakt dat u zult uploaden. Zorg ervoor dat u dit bestand hebt gemaakt voordat u Hallo code uitvoert.

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

Upload Hallo lokale bestand via een aanroep van toohello **CloudBlockBlob.upload** methode. eerste parameter toohello Hallo **CloudBlockBlob.upload** methode is een **FileInputStream** object vertegenwoordigt Hallo lokale bestand die worden geüpload tooAzure opslag. de tweede parameter Hallo is Hallo grootte, in bytes, van Hallo-bestand.

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

Aanroepen van een Help-functie met de naam **MakeHTMLPage**, toomake een basic HTML-pagina waarop een  **&lt;installatiekopie&gt;**  element met Hallo bron set toohello blob die nu in uw Azure Storage-account. code voor Hallo **MakeHTMLPage** wordt verderop in dit artikel worden besproken.

```java
MakeHTMLPage(container);
```

Afdrukken een statusbericht en informatie over Hallo HTML-pagina gemaakt.

```java
System.out.println("Processing complete.");
System.out.println("Open index.html toosee hello images stored in your storage account.");
```

Sluit Hallo **probeer** blokkeren door het invoegen van een haakje sluiten: **}**

Verwerken Hallo volgende uitzonderingen:

* **FileNotFoundException**: kan worden gegenereerd door Hallo **FileInputStream** of **FileOutputStream** constructors.
* **StorageException**: door opslagbibliotheek van hello Azure-client kan worden gegenereerd.
* **URISyntaxException**: kan worden gegenereerd door Hallo **ListBlobItem.getUri** methode.
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

Maken van een methode met de naam **MakeHTMLPage** toocreate een basic HTML-pagina. Deze methode heeft een parameter van het type **CloudBlobContainer**, die wordt gebruikt tooiterate door Hallo lijst met geüploade BLOB's zijn. Deze methode genereert uitzonderingen van het type **FileNotFoundException**, die kan worden gegenereerd door Hallo **FileOutputStream** -constructor aan, en **URISyntaxException**, dit kan worden veroorzaakt door Hallo **ListBlobItem.getUri** methode. Het openingshaakje omvatten **{**.

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

Maken van een lokaal bestand met de naam **index.html**.

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

Schrijven naar lokale bestand toohello, toe te voegen in Hallo  **&lt;html&gt;**,  **&lt;header&gt;**, en  **&lt;hoofdtekst&gt;**  elementen.

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

Hallo-lijst met geüploade blobs doorlopen. Voor elke blob in Hallo HTML-pagina maken een  **&lt;img&gt;**  -element waarvoor de **src** kenmerk verzonden op Hallo van URI van de blob Hallo zoals dit zich in uw Azure storage-account.
Hoewel u slechts één installatiekopie in dit voorbeeld wordt toegevoegd als u meer hebt toegevoegd, zou deze code allemaal herhalen.

Voor eenvoud, in dit voorbeeld wordt ervan uitgegaan dat elke geüploade blob is een afbeelding. Als u blobs dan afbeeldingen of pagina-blobs in plaats van blok-blobs hebt bijgewerkt, past u Hallo code indien nodig.

```java
// Enumerate hello uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in hello HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

Sluit Hallo  **&lt;hoofdtekst&gt;**  -element en Hallo  **&lt;html&gt;**  element.

```java
stream.println("</body>");
stream.println("</html>");
```

Sluit Hallo lokaal bestand.

```java
stream.close();
```

Sluit **MakeHTMLPage** door het invoegen van een haakje sluiten: **}**

Sluit **StorageSample** door het invoegen van een haakje sluiten: **}**

Hallo volgt Hallo volledige code voor dit voorbeeld. Vergeet niet de waarden van de tijdelijke aanduiding Hallo toomodify **uw\_account\_naam** en **uw\_account\_sleutel** toouse uw accountnaam en -account sleutel, respectievelijk.

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

In aanvulling toouploading uw afbeelding voor lokaal tooAzure bestandsopslag Hallo voorbeeldcode wordt gemaakt een lokaal bestand namedindex.html, die u in uw browser toosee openen kunt uw geüploade installatiekopie.

Omdat het Hallo-code bevat uw accountnaam en accountsleutel, zorg ervoor dat de broncode beveiligd is.

## <a name="toodelete-a-container"></a>een container toodelete
Omdat u in rekening voor opslag gebracht, kunt u toodelete de **gettingstarted** container nadat u klaar bent met het volgende voorbeeld experimenteren. toodelete een container gebruiken Hallo **CloudBlobContainer.delete** methode.

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

Hallo toocall **CloudBlobContainer.delete** methode, Hallo-proces voor het initialiseren van **CloudStorageAccount**, **ClodBlobClient**, en  **CloudBlobContainer** objecten is Hallo dezelfde zoals weergegeven voor de **createIfNotExist** methode. Hallo Hier volgt een voorbeeld van een volledige dat Hiermee verwijdert u de container met de naam Hallo **gettingstarted**.

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

Zie voor een overzicht van andere blob-opslag-klassen en methoden [hoe toouse Blob-opslag met Java](storage-java-how-to-use-blob-storage.md).

## <a name="next-steps"></a>Volgende stappen
Volg deze koppelingen toolearn meer informatie over complexere opslagtaken.

* [Azure-opslag-SDK voor Java](https://github.com/azure/azure-storage-java)
* [Azure Storage Client SDK-naslaginformatie](http://dl.windowsazure.com/storage/javadoc/)
* [REST-API voor Azure Storage-services](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog van het Azure Storage-team](http://blogs.msdn.com/b/windowsazurestorage/)

