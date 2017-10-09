---
title: aaaUse hello Java SDK toodevelop toepassingen in Azure Data Lake Store | Microsoft Docs
description: Gebruik van Azure Data Lake Store Java SDK toocreate een Data Lake Store-account en uitvoeren van basisbewerkingen in Data Lake Store Hallo
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d10e09db-5232-4e84-bb50-52efc2c21887
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/28/2017
ms.author: nitinme
ms.openlocfilehash: d3bcee449c2a2a4bd2f7b241af46ecc010b6b62e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-java"></a>Aan de slag met Azure Data Lake Store met Java
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET-SDK](data-lake-store-get-started-net-sdk.md)
> * [Java-SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

Meer informatie over hoe toouse hello Azure Data Lake Store Java SDK tooperform basisbewerkingen, zoals maken van mappen, uploaden en downloaden van gegevensbestanden, enzovoort. Zie [Azure Data Lake Store](data-lake-store-overview.md) voor meer informatie over Data Lake.

U hebt toegang tot Hallo Java SDK API documenten voor Azure Data Lake Store op [API van Azure Data Lake Store Java docs](https://azure.github.io/azure-data-lake-store-java/javadoc/).

## <a name="prerequisites"></a>Vereisten
* Java Development Kit (JDK 7 of hoger met Java versie 1.7 of hoger)
* Azure Data Lake Store-account. Volg de instructies Hallo voor [aan de slag met Azure Data Lake Store met Azure Portal Hallo](data-lake-store-get-started-portal.md).
* [Maven](https://maven.apache.org/install.html). In deze zelfstudie wordt Maven gebruikt voor build- en projectafhankelijkheden. Hoewel het mogelijk toobuild zonder een build-systeem, zoals Maven of Gradle, is het maken van deze systemen veel gemakkelijker toomanage afhankelijkheden.
* (Optioneel) Een IDE zoals [IntelliJ IDEA](https://www.jetbrains.com/idea/download/), [Eclipse](https://www.eclipse.org/downloads/) of vergelijkbaar.

## <a name="how-do-i-authenticate-using-azure-active-directory"></a>Hoe verifieer ik met Azure Active Directory?
In deze zelfstudie gebruiken we een Azure AD-toepassing client geheime tooretrieve een Azure Active Directory-token (service-naar-service-verificatie). We gebruiken deze token toocreate een Data Lake Store client object tooperform operations-bestand en de directory-bewerkingen. Voor instructies over hoe tooauthenticate met het gebruik van Azure Data Lake Store clientgeheim Hallo, uitvoeren we Hallo volgende stappen op hoog niveau:

1. Een Azure AD-webtoepassing maken
2. Hallo client-ID en clientgeheim token eindpunt voor hello Azure AD-webtoepassing worden opgehaald.
3. Configureer de toegang voor hello Azure AD-webtoepassing op Hallo Data Lake Store-bestand/map die u wilt tooaccess van Hallo Java-toepassing die u maakt.

Voor instructies over hoe tooperform deze stappen zien [maken van een Active Directory-toepassing](data-lake-store-authenticate-using-active-directory.md).

Azure Active Directory biedt dat andere opties ook tooretrieve een token. U kunt kiezen uit een aantal verschillende mechanismen toosuit uw scenario, bijvoorbeeld een toepassing die wordt uitgevoerd in een browser, een toepassing die wordt gedistribueerd als een bureaubladtoepassing of een servertoepassing lokale uitgevoerd of in een virtuele Azure machine. U kunt ook uit verschillende soorten referenties kiezen, zoals wachtwoorden, certificaten, tweeledige authenticatie enzovoort. Bovendien Azure Active Directory kunt u toosynchronize uw on-premises Active Directory-gebruikers met Hallo cloud. Zie [Verificatiescenario's voor Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md) voor meer informatie. 

## <a name="create-a-java-application"></a>Een Java-toepassing maken
Voorbeeld van code Hallo beschikbaar [op GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) begeleidt u bij Hallo proces van het maken van bestanden in archief hello, bestanden worden samengevoegd, downloaden van een bestand en verwijder enkele bestanden in archief Hallo. Deze sectie van Hallo artikel leest u Hallo hoofdonderdelen Hallo-code.

1. Maak een Maven-project met [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) Hallo uit vanaf de opdrachtregel of met behulp van een IDE. Zie voor instructies over hoe toocreate een Java-project met behulp van IntelliJ, [hier](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html). Voor instructies over het toocreate een project met behulp van Eclipse Zie [hier](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm). 
2. Hallo afhankelijkheden tooyour Maven na toevoegen **pom.xml** bestand. Hallo tekstfragment na tussen Hallo toevoegen  **\</version >** tag en Hallo  **\</project >** tag:
   
        <dependencies>
          <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-data-lake-store-sdk</artifactId>
            <version>2.1.5</version>
          </dependency>
          <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-nop</artifactId>
            <version>1.7.21</version>
          </dependency>
        </dependencies>
   
    Hallo eerste afhankelijkheid is toouse Hallo Data Lake Store SDK (`azure-data-lake-store-sdk`) vanuit de opslagplaats met maven Hallo. tweede afhankelijkheid Hallo (`slf4j-nop`) toospecify welke toouse logboekregistratie framework voor deze toepassing is. Hallo Data Lake Store SDK maakt gebruik van [slf4j](http://www.slf4j.org/) logboekregistratie façade, waarin u kiezen uit een aantal logboekregistratie populaire frameworks, zoals log4j kunt, aan te melden, logback, enz., Java of geen logboekregistratie. Logboekregistratie uitgeschakeld voor dit voorbeeld, daarom gebruiken we Hallo **slf4j nop** binding. toouse andere opties voor logboekregistratie in uw app Zie [hier](http://www.slf4j.org/manual.html#projectDep).

### <a name="add-hello-application-code"></a>Hallo-toepassingscode toevoegen
Er zijn drie belangrijkste onderdelen toohello code.

1. Hello Azure Active Directory-token verkrijgen
2. Hallo token toocreate een Data Lake Store-client gebruiken.
3. Hallo Data Lake Store-clientbewerkingen tooperform gebruiken.

#### <a name="step-1-obtain-an-azure-active-directory-token"></a>Stap 1: het Azure Active Directory-token verkrijgen.
Hallo Data Lake Store SDK biedt handige methoden die u kunnen beheren, Hallo beveiligingstokens tootalk toohello Data Lake Store-account nodig. Hallo SDK schrijft echter niet dat deze twee methoden worden gebruikt. U kunt een andere manier voor het verkrijgen van token, zoals het gebruik van Hallo [Azure Active Directory-SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), of uw eigen aangepaste code.

toouse hello Data Lake Store SDK tooobtain token voor Hallo Active Directory-webtoepassing u eerder hebt gemaakt, gebruikt u een van de Hallo subklassen van `AccessTokenProvider` (Hallo voorbeeld hieronder wordt `ClientCredsTokenProvider`). Hallo tokenprovider caches Hallo referenties tooobtain Hallo token in het geheugen gebruikt en wordt automatisch verlengd Hallo token als over tooexpire. Het is mogelijk toocreate uw eigen subklassen van `AccessTokenProvider` zodat tokens worden verkregen door de code van uw klant, maar nu gaan we zojuist gebruik Hallo één in Hallo SDK opgegeven.

Vervang **invullen-hier** met de werkelijke waarden Hallo voor hello Azure Active Directory-webtoepassing.

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a>Stap 2: een Azure Data Lake Store-clientobject (ADLStoreClient-object) verkrijgen
Maken van een [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) object, moet u toospecify Hallo Data Lake Store-account naam en het Hallo tokenprovider u in de laatste stap Hallo gegenereerd. Houd er rekening mee dat Hallo naam moet toobe een volledig gekwalificeerde domeinnaam van Data Lake Store-account. Vervang bijvoorbeeld **FILL-IN-HERE** met iets als **mydatalakestore.azuredatalakestore.net**.

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just hello account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

### <a name="step-3-use-hello-adlstoreclient-tooperform-file-and-directory-operations"></a>Stap 3: Hallo ADLStoreClient tooperform bestands- en bewerkingen gebruiken
Hallo-code hieronder bevat enkele veelvoorkomende bewerkingen voorbeeld codefragmenten. U kunt zoeken op volledige Hallo [Data Lake Store Java SDK API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/) Hallo **ADLStoreClient** object toosee andere bewerkingen.

Bestanden worden gelezen en geschreven met behulp van standaard Java-streams. Dit betekent dat u kunt van Hallo de streams Java boven op Hallo die Data Lake Store streams toobenefit van standaard Java-functionaliteit (bijv, afdrukken stromen voor opgemaakte uitvoer, of een van de Hallo compressie of codering stromen voor aanvullende functionaliteit op de laag boven, enz.).

     // create file and write some content
     String filename = "/a/b/c.txt";
     OutputStream stream = client.createFile(filename, IfExists.OVERWRITE  );
     PrintStream out = new PrintStream(stream);
     for (int i = 1; i <= 10; i++) {
         out.println("This is line #" + i);
         out.format("This is hello same line (%d), but using formatted output. %n", i);
     }
     out.close();
    
    // set file permission
    client.setPermission(filename, "744");

    // append toofile
    stream = client.getAppendStream(filename);
    stream.write(getSampleContent());
    stream.close();

    // Read File
    InputStream in = client.getReadStream(filename);
    byte[] b = new byte[64000];
    while (in.read(b) != -1) {
        System.out.write(b);
    }
    in.close();

    // concatenate hello two files into one
    List<String> fileList = Arrays.asList("/a/b/c.txt", "/a/b/d.txt");
    client.concatenateFiles("/a/b/f.txt", fileList);

    //rename hello file
    client.rename("/a/b/f.txt", "/a/b/g.txt");

    // list directory contents
    List<DirectoryEntry> list = client.enumerateDirectory("/a/b", 2000);
    System.out.println("Directory listing for directory /a/b:");
    for (DirectoryEntry entry : list) {
        printDirectoryInfo(entry);
    }

    // delete directory along with all hello subdirectories and files in it
    client.deleteRecursive("/a");

#### <a name="step-4-build-and-run-hello-application"></a>Stap 4: Toepassing bouwen en uitvoeren Hallo
1. toorun van binnen een IDE vinden en druk op Hallo **uitvoeren** knop. toorun van Maven, gebruik [exec: exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).
2. een zelfstandige jar die u vanaf de opdrachtregel build Hallo jar met alle afhankelijkheden die zijn opgenomen uitvoeren kunt, met behulp van Hallo tooproduce [Maven assembly invoegtoepassing](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html). pom.xml in Hallo Hallo [broncode voorbeeld op github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) is een voorbeeld van hoe toodo dit.

## <a name="next-steps"></a>Volgende stappen
* [Ontdek de JavaDoc voor Hallo Java SDK](https://azure.github.io/azure-data-lake-store-java/javadoc/)
* [Gegevens in Data Lake Store beveiligen](data-lake-store-secure-data.md)
* [Azure Data Lake Analytics gebruiken met Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight gebruiken met Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

