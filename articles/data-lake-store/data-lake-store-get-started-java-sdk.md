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
# <a name="get-started-with-azure-data-lake-store-using-java"></a><span data-ttu-id="0618b-103">Aan de slag met Azure Data Lake Store met Java</span><span class="sxs-lookup"><span data-stu-id="0618b-103">Get started with Azure Data Lake Store using Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0618b-104">Portal</span><span class="sxs-lookup"><span data-stu-id="0618b-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="0618b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0618b-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="0618b-106">.NET-SDK</span><span class="sxs-lookup"><span data-stu-id="0618b-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="0618b-107">Java-SDK</span><span class="sxs-lookup"><span data-stu-id="0618b-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="0618b-108">REST API</span><span class="sxs-lookup"><span data-stu-id="0618b-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="0618b-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0618b-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="0618b-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="0618b-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="0618b-111">Python</span><span class="sxs-lookup"><span data-stu-id="0618b-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="0618b-112">Meer informatie over hoe toouse hello Azure Data Lake Store Java SDK tooperform basisbewerkingen, zoals maken van mappen, uploaden en downloaden van gegevensbestanden, enzovoort. Zie [Azure Data Lake Store](data-lake-store-overview.md) voor meer informatie over Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0618b-112">Learn how toouse hello Azure Data Lake Store Java SDK tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="0618b-113">U hebt toegang tot Hallo Java SDK API documenten voor Azure Data Lake Store op [API van Azure Data Lake Store Java docs](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span><span class="sxs-lookup"><span data-stu-id="0618b-113">You can access hello Java SDK API docs for Azure Data Lake Store at [Azure Data Lake Store Java API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0618b-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0618b-114">Prerequisites</span></span>
* <span data-ttu-id="0618b-115">Java Development Kit (JDK 7 of hoger met Java versie 1.7 of hoger)</span><span class="sxs-lookup"><span data-stu-id="0618b-115">Java Development Kit (JDK 7 or higher, using Java version 1.7 or higher)</span></span>
* <span data-ttu-id="0618b-116">Azure Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="0618b-116">Azure Data Lake Store account.</span></span> <span data-ttu-id="0618b-117">Volg de instructies Hallo voor [aan de slag met Azure Data Lake Store met Azure Portal Hallo](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0618b-117">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span>
* <span data-ttu-id="0618b-118">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="0618b-118">[Maven](https://maven.apache.org/install.html).</span></span> <span data-ttu-id="0618b-119">In deze zelfstudie wordt Maven gebruikt voor build- en projectafhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="0618b-119">This tutorial uses Maven for build and project dependencies.</span></span> <span data-ttu-id="0618b-120">Hoewel het mogelijk toobuild zonder een build-systeem, zoals Maven of Gradle, is het maken van deze systemen veel gemakkelijker toomanage afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="0618b-120">Although it is possible toobuild without using a build system like Maven or Gradle, these systems make is much easier toomanage dependencies.</span></span>
* <span data-ttu-id="0618b-121">(Optioneel) Een IDE zoals [IntelliJ IDEA](https://www.jetbrains.com/idea/download/), [Eclipse](https://www.eclipse.org/downloads/) of vergelijkbaar.</span><span class="sxs-lookup"><span data-stu-id="0618b-121">(Optional) And IDE like [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) or [Eclipse](https://www.eclipse.org/downloads/) or similar.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="0618b-122">Hoe verifieer ik met Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0618b-122">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="0618b-123">In deze zelfstudie gebruiken we een Azure AD-toepassing client geheime tooretrieve een Azure Active Directory-token (service-naar-service-verificatie).</span><span class="sxs-lookup"><span data-stu-id="0618b-123">In this tutorial we use a Azure AD application client secret tooretrieve an Azure Active Directory token (service-to-service authentication).</span></span> <span data-ttu-id="0618b-124">We gebruiken deze token toocreate een Data Lake Store client object tooperform operations-bestand en de directory-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="0618b-124">We use this token toocreate an Data Lake Store client object tooperform operations file and directory operations.</span></span> <span data-ttu-id="0618b-125">Voor instructies over hoe tooauthenticate met het gebruik van Azure Data Lake Store clientgeheim Hallo, uitvoeren we Hallo volgende stappen op hoog niveau:</span><span class="sxs-lookup"><span data-stu-id="0618b-125">For instructions on how tooauthenticate with Azure Data Lake Store using hello client secret, we perform hello following high-level steps:</span></span>

1. <span data-ttu-id="0618b-126">Een Azure AD-webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="0618b-126">Create an Azure AD web application</span></span>
2. <span data-ttu-id="0618b-127">Hallo client-ID en clientgeheim token eindpunt voor hello Azure AD-webtoepassing worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="0618b-127">Retrieve hello client ID, client secret, and token endpoint for hello Azure AD web application.</span></span>
3. <span data-ttu-id="0618b-128">Configureer de toegang voor hello Azure AD-webtoepassing op Hallo Data Lake Store-bestand/map die u wilt tooaccess van Hallo Java-toepassing die u maakt.</span><span class="sxs-lookup"><span data-stu-id="0618b-128">Configure access for hello Azure AD web application on hello Data Lake Store file/folder that you want tooaccess from hello Java application you are creating.</span></span>

<span data-ttu-id="0618b-129">Voor instructies over hoe tooperform deze stappen zien [maken van een Active Directory-toepassing](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="0618b-129">For instructions on how tooperform these steps, see [Create an Active Directory application](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="0618b-130">Azure Active Directory biedt dat andere opties ook tooretrieve een token.</span><span class="sxs-lookup"><span data-stu-id="0618b-130">Azure Active Directory provides other options as well tooretrieve a token.</span></span> <span data-ttu-id="0618b-131">U kunt kiezen uit een aantal verschillende mechanismen toosuit uw scenario, bijvoorbeeld een toepassing die wordt uitgevoerd in een browser, een toepassing die wordt gedistribueerd als een bureaubladtoepassing of een servertoepassing lokale uitgevoerd of in een virtuele Azure machine.</span><span class="sxs-lookup"><span data-stu-id="0618b-131">You can pick from a number of different authentication mechanisms toosuit your scenario, for example, an application running in a browser, an application distributed as a desktop application, or a server application running on-premises or in an Azure virtual machine.</span></span> <span data-ttu-id="0618b-132">U kunt ook uit verschillende soorten referenties kiezen, zoals wachtwoorden, certificaten, tweeledige authenticatie enzovoort. Bovendien Azure Active Directory kunt u toosynchronize uw on-premises Active Directory-gebruikers met Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="0618b-132">You can also pick from different types of credentials like passwords, certificates, 2-factor authentication, etc. In addition, Azure Active Directory allows you toosynchronize your on-premises Active Directory users with hello cloud.</span></span> <span data-ttu-id="0618b-133">Zie [Verificatiescenario's voor Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0618b-133">For details, see [Authentication Scenarios for Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span></span> 

## <a name="create-a-java-application"></a><span data-ttu-id="0618b-134">Een Java-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="0618b-134">Create a Java application</span></span>
<span data-ttu-id="0618b-135">Voorbeeld van code Hallo beschikbaar [op GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) begeleidt u bij Hallo proces van het maken van bestanden in archief hello, bestanden worden samengevoegd, downloaden van een bestand en verwijder enkele bestanden in archief Hallo.</span><span class="sxs-lookup"><span data-stu-id="0618b-135">hello code sample available [on GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) walks you through hello process of creating files in hello store, concatenating files, downloading a file, and deleting some files in hello store.</span></span> <span data-ttu-id="0618b-136">Deze sectie van Hallo artikel leest u Hallo hoofdonderdelen Hallo-code.</span><span class="sxs-lookup"><span data-stu-id="0618b-136">This section of hello article walk you through hello main parts of hello code.</span></span>

1. <span data-ttu-id="0618b-137">Maak een Maven-project met [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) Hallo uit vanaf de opdrachtregel of met behulp van een IDE.</span><span class="sxs-lookup"><span data-stu-id="0618b-137">Create a Maven project using [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) from hello command-line or using an IDE.</span></span> <span data-ttu-id="0618b-138">Zie voor instructies over hoe toocreate een Java-project met behulp van IntelliJ, [hier](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span><span class="sxs-lookup"><span data-stu-id="0618b-138">For instructions on how toocreate a Java project using IntelliJ, see [here](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span></span> <span data-ttu-id="0618b-139">Voor instructies over het toocreate een project met behulp van Eclipse Zie [hier](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span><span class="sxs-lookup"><span data-stu-id="0618b-139">For instructions on how toocreate a project using Eclipse, see [here](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span></span> 
2. <span data-ttu-id="0618b-140">Hallo afhankelijkheden tooyour Maven na toevoegen **pom.xml** bestand.</span><span class="sxs-lookup"><span data-stu-id="0618b-140">Add hello following dependencies tooyour Maven **pom.xml** file.</span></span> <span data-ttu-id="0618b-141">Hallo tekstfragment na tussen Hallo toevoegen  **\</version >** tag en Hallo  **\</project >** tag:</span><span class="sxs-lookup"><span data-stu-id="0618b-141">Add hello following snippet of text between hello **\</version>** tag and hello **\</project>** tag:</span></span>
   
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
   
    <span data-ttu-id="0618b-142">Hallo eerste afhankelijkheid is toouse Hallo Data Lake Store SDK (`azure-data-lake-store-sdk`) vanuit de opslagplaats met maven Hallo.</span><span class="sxs-lookup"><span data-stu-id="0618b-142">hello first dependency is toouse hello Data Lake Store SDK (`azure-data-lake-store-sdk`) from hello maven repository.</span></span> <span data-ttu-id="0618b-143">tweede afhankelijkheid Hallo (`slf4j-nop`) toospecify welke toouse logboekregistratie framework voor deze toepassing is.</span><span class="sxs-lookup"><span data-stu-id="0618b-143">hello second dependency (`slf4j-nop`) is toospecify which logging framework toouse for this application.</span></span> <span data-ttu-id="0618b-144">Hallo Data Lake Store SDK maakt gebruik van [slf4j](http://www.slf4j.org/) logboekregistratie façade, waarin u kiezen uit een aantal logboekregistratie populaire frameworks, zoals log4j kunt, aan te melden, logback, enz., Java of geen logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="0618b-144">hello Data Lake Store SDK uses [slf4j](http://www.slf4j.org/) logging façade, which lets you choose from a number of popular logging frameworks, like log4j, Java logging, logback, etc., or no logging.</span></span> <span data-ttu-id="0618b-145">Logboekregistratie uitgeschakeld voor dit voorbeeld, daarom gebruiken we Hallo **slf4j nop** binding.</span><span class="sxs-lookup"><span data-stu-id="0618b-145">For this example, we will disable logging, hence we use hello **slf4j-nop** binding.</span></span> <span data-ttu-id="0618b-146">toouse andere opties voor logboekregistratie in uw app Zie [hier](http://www.slf4j.org/manual.html#projectDep).</span><span class="sxs-lookup"><span data-stu-id="0618b-146">toouse other logging options in your app, see [here](http://www.slf4j.org/manual.html#projectDep).</span></span>

### <a name="add-hello-application-code"></a><span data-ttu-id="0618b-147">Hallo-toepassingscode toevoegen</span><span class="sxs-lookup"><span data-stu-id="0618b-147">Add hello application code</span></span>
<span data-ttu-id="0618b-148">Er zijn drie belangrijkste onderdelen toohello code.</span><span class="sxs-lookup"><span data-stu-id="0618b-148">There are three main parts toohello code.</span></span>

1. <span data-ttu-id="0618b-149">Hello Azure Active Directory-token verkrijgen</span><span class="sxs-lookup"><span data-stu-id="0618b-149">Obtain hello Azure Active Directory token</span></span>
2. <span data-ttu-id="0618b-150">Hallo token toocreate een Data Lake Store-client gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0618b-150">Use hello token toocreate a Data Lake Store client.</span></span>
3. <span data-ttu-id="0618b-151">Hallo Data Lake Store-clientbewerkingen tooperform gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0618b-151">Use hello Data Lake Store client tooperform operations.</span></span>

#### <a name="step-1-obtain-an-azure-active-directory-token"></a><span data-ttu-id="0618b-152">Stap 1: het Azure Active Directory-token verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="0618b-152">Step 1: Obtain an Azure Active Directory token.</span></span>
<span data-ttu-id="0618b-153">Hallo Data Lake Store SDK biedt handige methoden die u kunnen beheren, Hallo beveiligingstokens tootalk toohello Data Lake Store-account nodig.</span><span class="sxs-lookup"><span data-stu-id="0618b-153">hello Data Lake Store SDK provides convenient methods that let you manage hello security tokens needed tootalk toohello Data Lake Store account.</span></span> <span data-ttu-id="0618b-154">Hallo SDK schrijft echter niet dat deze twee methoden worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0618b-154">However, hello SDK does not mandate that only these methods be used.</span></span> <span data-ttu-id="0618b-155">U kunt een andere manier voor het verkrijgen van token, zoals het gebruik van Hallo [Azure Active Directory-SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), of uw eigen aangepaste code.</span><span class="sxs-lookup"><span data-stu-id="0618b-155">You can use any other means of obtaining token as well, like using hello [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), or your own custom code.</span></span>

<span data-ttu-id="0618b-156">toouse hello Data Lake Store SDK tooobtain token voor Hallo Active Directory-webtoepassing u eerder hebt gemaakt, gebruikt u een van de Hallo subklassen van `AccessTokenProvider` (Hallo voorbeeld hieronder wordt `ClientCredsTokenProvider`).</span><span class="sxs-lookup"><span data-stu-id="0618b-156">toouse hello Data Lake Store SDK tooobtain token for hello Active Directory Web application you created earlier, use one of hello subclasses of `AccessTokenProvider` (hello example below uses `ClientCredsTokenProvider`).</span></span> <span data-ttu-id="0618b-157">Hallo tokenprovider caches Hallo referenties tooobtain Hallo token in het geheugen gebruikt en wordt automatisch verlengd Hallo token als over tooexpire.</span><span class="sxs-lookup"><span data-stu-id="0618b-157">hello token provider caches hello creds used tooobtain hello token in memory, and automatically renews hello token if it is about tooexpire.</span></span> <span data-ttu-id="0618b-158">Het is mogelijk toocreate uw eigen subklassen van `AccessTokenProvider` zodat tokens worden verkregen door de code van uw klant, maar nu gaan we zojuist gebruik Hallo één in Hallo SDK opgegeven.</span><span class="sxs-lookup"><span data-stu-id="0618b-158">It is possible toocreate your own subclasses of `AccessTokenProvider` so tokens are obtained by your customer code, but for now let's just use hello one provided in hello SDK.</span></span>

<span data-ttu-id="0618b-159">Vervang **invullen-hier** met de werkelijke waarden Hallo voor hello Azure Active Directory-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="0618b-159">Replace **FILL-IN-HERE** with hello actual values for hello Azure Active Directory Web application.</span></span>

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a><span data-ttu-id="0618b-160">Stap 2: een Azure Data Lake Store-clientobject (ADLStoreClient-object) verkrijgen</span><span class="sxs-lookup"><span data-stu-id="0618b-160">Step 2: Create an Azure Data Lake Store client (ADLStoreClient) object</span></span>
<span data-ttu-id="0618b-161">Maken van een [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) object, moet u toospecify Hallo Data Lake Store-account naam en het Hallo tokenprovider u in de laatste stap Hallo gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="0618b-161">Creating an [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) object requires you toospecify hello Data Lake Store account name and hello token provider you generated in hello last step.</span></span> <span data-ttu-id="0618b-162">Houd er rekening mee dat Hallo naam moet toobe een volledig gekwalificeerde domeinnaam van Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="0618b-162">Note that hello Data Lake Store account name needs toobe a fully qualified domain name.</span></span> <span data-ttu-id="0618b-163">Vervang bijvoorbeeld **FILL-IN-HERE** met iets als **mydatalakestore.azuredatalakestore.net**.</span><span class="sxs-lookup"><span data-stu-id="0618b-163">For example, replace **FILL-IN-HERE** with something like **mydatalakestore.azuredatalakestore.net**.</span></span>

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just hello account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

### <a name="step-3-use-hello-adlstoreclient-tooperform-file-and-directory-operations"></a><span data-ttu-id="0618b-164">Stap 3: Hallo ADLStoreClient tooperform bestands- en bewerkingen gebruiken</span><span class="sxs-lookup"><span data-stu-id="0618b-164">Step 3: Use hello ADLStoreClient tooperform file and directory operations</span></span>
<span data-ttu-id="0618b-165">Hallo-code hieronder bevat enkele veelvoorkomende bewerkingen voorbeeld codefragmenten.</span><span class="sxs-lookup"><span data-stu-id="0618b-165">hello code below contains example snippets of some common operations.</span></span> <span data-ttu-id="0618b-166">U kunt zoeken op volledige Hallo [Data Lake Store Java SDK API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/) Hallo **ADLStoreClient** object toosee andere bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="0618b-166">You can look at hello full [Data Lake Store Java SDK API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/) of hello **ADLStoreClient** object toosee other operations.</span></span>

<span data-ttu-id="0618b-167">Bestanden worden gelezen en geschreven met behulp van standaard Java-streams.</span><span class="sxs-lookup"><span data-stu-id="0618b-167">Note that files are read from and written into using standard Java streams.</span></span> <span data-ttu-id="0618b-168">Dit betekent dat u kunt van Hallo de streams Java boven op Hallo die Data Lake Store streams toobenefit van standaard Java-functionaliteit (bijv, afdrukken stromen voor opgemaakte uitvoer, of een van de Hallo compressie of codering stromen voor aanvullende functionaliteit op de laag boven, enz.).</span><span class="sxs-lookup"><span data-stu-id="0618b-168">This means that you can layer any of hello Java streams on top of hello Data Lake Store streams toobenefit from standard Java functionality (e.g., Print streams for formatted output, or any of hello compression or encryption streams for additional functionality on top, etc.).</span></span>

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

#### <a name="step-4-build-and-run-hello-application"></a><span data-ttu-id="0618b-169">Stap 4: Toepassing bouwen en uitvoeren Hallo</span><span class="sxs-lookup"><span data-stu-id="0618b-169">Step 4: Build and run hello application</span></span>
1. <span data-ttu-id="0618b-170">toorun van binnen een IDE vinden en druk op Hallo **uitvoeren** knop.</span><span class="sxs-lookup"><span data-stu-id="0618b-170">toorun from within an IDE, locate and press hello **Run** button.</span></span> <span data-ttu-id="0618b-171">toorun van Maven, gebruik [exec: exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span><span class="sxs-lookup"><span data-stu-id="0618b-171">toorun from Maven, use [exec:exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span></span>
2. <span data-ttu-id="0618b-172">een zelfstandige jar die u vanaf de opdrachtregel build Hallo jar met alle afhankelijkheden die zijn opgenomen uitvoeren kunt, met behulp van Hallo tooproduce [Maven assembly invoegtoepassing](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span><span class="sxs-lookup"><span data-stu-id="0618b-172">tooproduce a standalone jar that you can run from command-line build hello jar with all dependencies included, using hello [Maven assembly plugin](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span></span> <span data-ttu-id="0618b-173">pom.xml in Hallo Hallo [broncode voorbeeld op github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) is een voorbeeld van hoe toodo dit.</span><span class="sxs-lookup"><span data-stu-id="0618b-173">hello pom.xml in hello [example source code on github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) has an example of how toodo this.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0618b-174">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0618b-174">Next steps</span></span>
* [<span data-ttu-id="0618b-175">Ontdek de JavaDoc voor Hallo Java SDK</span><span class="sxs-lookup"><span data-stu-id="0618b-175">Explore JavaDoc for hello Java SDK</span></span>](https://azure.github.io/azure-data-lake-store-java/javadoc/)
* [<span data-ttu-id="0618b-176">Gegevens in Data Lake Store beveiligen</span><span class="sxs-lookup"><span data-stu-id="0618b-176">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="0618b-177">Azure Data Lake Analytics gebruiken met Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0618b-177">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="0618b-178">Azure HDInsight gebruiken met Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0618b-178">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

