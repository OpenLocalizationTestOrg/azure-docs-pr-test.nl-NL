---
title: De Java-SDK gebruiken om toepassingen te ontwikkelen in Azure Data Lake Store | Microsoft Docs
description: De Java-SDK van Azure Data Lake Store gebruiken om een Data Lake Store-account te maken en basisbewerkingen in Data Lake Store uit te voeren
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
ms.openlocfilehash: 91128b53a2f1cd3ddcbee5b07da0d67668944fb4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-java"></a><span data-ttu-id="34c77-103">Aan de slag met Azure Data Lake Store met Java</span><span class="sxs-lookup"><span data-stu-id="34c77-103">Get started with Azure Data Lake Store using Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="34c77-104">Portal</span><span class="sxs-lookup"><span data-stu-id="34c77-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="34c77-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="34c77-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="34c77-106">.NET-SDK</span><span class="sxs-lookup"><span data-stu-id="34c77-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="34c77-107">Java-SDK</span><span class="sxs-lookup"><span data-stu-id="34c77-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="34c77-108">REST API</span><span class="sxs-lookup"><span data-stu-id="34c77-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="34c77-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="34c77-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="34c77-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="34c77-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="34c77-111">Python</span><span class="sxs-lookup"><span data-stu-id="34c77-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="34c77-112">Lees hoe u met de Azure Data Lake Store Java SDK basisbewerkingen uitvoert, zoals het maken van mappen, het uploaden en downloaden van gegevensbestanden enzovoort. Zie [Azure Data Lake Store](data-lake-store-overview.md) voor meer informatie over Data Lake.</span><span class="sxs-lookup"><span data-stu-id="34c77-112">Learn how to use the Azure Data Lake Store Java SDK to perform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="34c77-113">U kunt de Java SDK API-documenten voor Azure Data Lake Store openen via [Azure Data Lake Store Java API-documenten](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span><span class="sxs-lookup"><span data-stu-id="34c77-113">You can access the Java SDK API docs for Azure Data Lake Store at [Azure Data Lake Store Java API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34c77-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="34c77-114">Prerequisites</span></span>
* <span data-ttu-id="34c77-115">Java Development Kit (JDK 7 of hoger met Java versie 1.7 of hoger)</span><span class="sxs-lookup"><span data-stu-id="34c77-115">Java Development Kit (JDK 7 or higher, using Java version 1.7 or higher)</span></span>
* <span data-ttu-id="34c77-116">Azure Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="34c77-116">Azure Data Lake Store account.</span></span> <span data-ttu-id="34c77-117">Volg de instructies in [Aan de slag met Azure Data Lake Store met Azure Portal](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="34c77-117">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span>
* <span data-ttu-id="34c77-118">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="34c77-118">[Maven](https://maven.apache.org/install.html).</span></span> <span data-ttu-id="34c77-119">In deze zelfstudie wordt Maven gebruikt voor build- en projectafhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="34c77-119">This tutorial uses Maven for build and project dependencies.</span></span> <span data-ttu-id="34c77-120">Hoewel het mogelijk is te ontwikkelen zonder een buildsysteem als Maven of Gradle, maken deze systemen het veel eenvoudiger om afhankelijkheden te beheren.</span><span class="sxs-lookup"><span data-stu-id="34c77-120">Although it is possible to build without using a build system like Maven or Gradle, these systems make is much easier to manage dependencies.</span></span>
* <span data-ttu-id="34c77-121">(Optioneel) Een IDE zoals [IntelliJ IDEA](https://www.jetbrains.com/idea/download/), [Eclipse](https://www.eclipse.org/downloads/) of vergelijkbaar.</span><span class="sxs-lookup"><span data-stu-id="34c77-121">(Optional) And IDE like [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) or [Eclipse](https://www.eclipse.org/downloads/) or similar.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="34c77-122">Hoe verifieer ik met Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="34c77-122">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="34c77-123">In deze zelfstudie wordt een clientgeheim in de Azure AD-toepassing gebruikt om een Azure Active Directory-token (service-naar-serviceverificatie) op te halen.</span><span class="sxs-lookup"><span data-stu-id="34c77-123">In this tutorial we use a Azure AD application client secret to retrieve an Azure Active Directory token (service-to-service authentication).</span></span> <span data-ttu-id="34c77-124">Dit token wordt gebruikt om een Data Lake Store-clientobject te maken voor het uitvoeren van bestand- en mapbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="34c77-124">We use this token to create an Data Lake Store client object to perform operations file and directory operations.</span></span> <span data-ttu-id="34c77-125">Voer de volgende high-level stappen uit om de verificatie uit te voeren met het clientgeheim in Azure Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="34c77-125">For instructions on how to authenticate with Azure Data Lake Store using the client secret, we perform the following high-level steps:</span></span>

1. <span data-ttu-id="34c77-126">Een Azure AD-webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="34c77-126">Create an Azure AD web application</span></span>
2. <span data-ttu-id="34c77-127">Haal de client-id, het client-geheim en het tokeneindpunt voor de Azure AD-webtoepassing op.</span><span class="sxs-lookup"><span data-stu-id="34c77-127">Retrieve the client ID, client secret, and token endpoint for the Azure AD web application.</span></span>
3. <span data-ttu-id="34c77-128">Configureer de toegang tot de Azure AD-webtoepassing in het/de Data Lake Store-bestand/-map dat/die u wilt openen vanuit de Java-toepassing die u maakt.</span><span class="sxs-lookup"><span data-stu-id="34c77-128">Configure access for the Azure AD web application on the Data Lake Store file/folder that you want to access from the Java application you are creating.</span></span>

<span data-ttu-id="34c77-129">Zie [Een Active Directory-toepassing maken](data-lake-store-authenticate-using-active-directory.md) voor instructies om deze stappen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="34c77-129">For instructions on how to perform these steps, see [Create an Active Directory application](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="34c77-130">Azure Active Directory biedt andere opties naast het ophalen van een token.</span><span class="sxs-lookup"><span data-stu-id="34c77-130">Azure Active Directory provides other options as well to retrieve a token.</span></span> <span data-ttu-id="34c77-131">U kunt uit verschillende verificatiemechanismen kiezen aan de hand van uw scenario, bijvoorbeeld een toepassing die wordt uitgevoerd in een browser, een toepassing die wordt gedistribueerd als een bureaubladtoepassing of een servertoepassing die on-premises of in een virtuele Azure-machine wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="34c77-131">You can pick from a number of different authentication mechanisms to suit your scenario, for example, an application running in a browser, an application distributed as a desktop application, or a server application running on-premises or in an Azure virtual machine.</span></span> <span data-ttu-id="34c77-132">U kunt ook uit verschillende soorten referenties kiezen, zoals wachtwoorden, certificaten, tweeledige authenticatie enzovoort. Daarnaast stelt Azure Active Directory u in staat uw on-premises Active Directory-gebruikers te synchroniseren met de cloud.</span><span class="sxs-lookup"><span data-stu-id="34c77-132">You can also pick from different types of credentials like passwords, certificates, 2-factor authentication, etc. In addition, Azure Active Directory allows you to synchronize your on-premises Active Directory users with the cloud.</span></span> <span data-ttu-id="34c77-133">Zie [Verificatiescenario's voor Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="34c77-133">For details, see [Authentication Scenarios for Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span></span> 

## <a name="create-a-java-application"></a><span data-ttu-id="34c77-134">Een Java-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="34c77-134">Create a Java application</span></span>
<span data-ttu-id="34c77-135">Dit codevoorbeeld beschikbaar [in GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) doorloopt het proces waarin bestanden in het archief worden gemaakt, bestanden worden samengevoegd, een bestand wordt gedownload en een aantal bestanden uit het archief wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="34c77-135">The code sample available [on GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) walks you through the process of creating files in the store, concatenating files, downloading a file, and deleting some files in the store.</span></span> <span data-ttu-id="34c77-136">In dit gedeelte van het artikel komen de belangrijkste onderdelen van de code aan bod.</span><span class="sxs-lookup"><span data-stu-id="34c77-136">This section of the article walk you through the main parts of the code.</span></span>

1. <span data-ttu-id="34c77-137">Maak een Maven-project met behulp van [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) vanuit de opdrachtregel of met behulp van een IDE.</span><span class="sxs-lookup"><span data-stu-id="34c77-137">Create a Maven project using [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) from the command-line or using an IDE.</span></span> <span data-ttu-id="34c77-138">[Hier](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html) vindt u instructies over het maken van een Java-project met behulp van IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="34c77-138">For instructions on how to create a Java project using IntelliJ, see [here](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span></span> <span data-ttu-id="34c77-139">[Hier](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm) vindt u instructies over het maken van een Java-project met behulp van Eclipse.</span><span class="sxs-lookup"><span data-stu-id="34c77-139">For instructions on how to create a project using Eclipse, see [here](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span></span> 
2. <span data-ttu-id="34c77-140">Voeg de volgende afhankelijkheden toe aan het **pom.xml**-bestand in Maven.</span><span class="sxs-lookup"><span data-stu-id="34c77-140">Add the following dependencies to your Maven **pom.xml** file.</span></span> <span data-ttu-id="34c77-141">Voeg het volgende tekstfragment toe tussen de tag **\</version>** en de tag **\</project>**:</span><span class="sxs-lookup"><span data-stu-id="34c77-141">Add the following snippet of text between the **\</version>** tag and the **\</project>** tag:</span></span>
   
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
   
    <span data-ttu-id="34c77-142">De eerste afhankelijkheid is om Data Lake Store SDK (`azure-data-lake-store-sdk`) vanuit de Maven-opslag te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="34c77-142">The first dependency is to use the Data Lake Store SDK (`azure-data-lake-store-sdk`) from the maven repository.</span></span> <span data-ttu-id="34c77-143">De tweede afhankelijkheid (`slf4j-nop`) is om aan te geven welk framework voor logboekregistratie moet worden gebruikt voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="34c77-143">The second dependency (`slf4j-nop`) is to specify which logging framework to use for this application.</span></span> <span data-ttu-id="34c77-144">De Data Lake Store SDK gebruikt een [slf4j](http://www.slf4j.org/)-façade voor logboekregistratie, waarmee u uit een aantal populaire frameworks voor logboekregistratie, zoals log4j, Java logging, logback enzovoort, of voor geen logboekregistratie kunt kiezen.</span><span class="sxs-lookup"><span data-stu-id="34c77-144">The Data Lake Store SDK uses [slf4j](http://www.slf4j.org/) logging façade, which lets you choose from a number of popular logging frameworks, like log4j, Java logging, logback, etc., or no logging.</span></span> <span data-ttu-id="34c77-145">In dit voorbeeld wordt logboekregistratie uitgeschakeld. Daarom wordt de **slf4j-nop**-binding gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34c77-145">For this example, we will disable logging, hence we use the **slf4j-nop** binding.</span></span> <span data-ttu-id="34c77-146">[Hier](http://www.slf4j.org/manual.html#projectDep) vindt u andere opties voor logboekregistratie voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="34c77-146">To use other logging options in your app, see [here](http://www.slf4j.org/manual.html#projectDep).</span></span>

### <a name="add-the-application-code"></a><span data-ttu-id="34c77-147">De toepassingscode toevoegen</span><span class="sxs-lookup"><span data-stu-id="34c77-147">Add the application code</span></span>
<span data-ttu-id="34c77-148">Er zijn drie belangrijke onderdelen voor het toevoegen van de code.</span><span class="sxs-lookup"><span data-stu-id="34c77-148">There are three main parts to the code.</span></span>

1. <span data-ttu-id="34c77-149">De Azure Active Directory-token verkrijgen</span><span class="sxs-lookup"><span data-stu-id="34c77-149">Obtain the Azure Active Directory token</span></span>
2. <span data-ttu-id="34c77-150">Het token gebruiken om een Data Lake Store-client te maken.</span><span class="sxs-lookup"><span data-stu-id="34c77-150">Use the token to create a Data Lake Store client.</span></span>
3. <span data-ttu-id="34c77-151">De Data Lake Store-client gebruiken om bewerkingen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="34c77-151">Use the Data Lake Store client to perform operations.</span></span>

#### <a name="step-1-obtain-an-azure-active-directory-token"></a><span data-ttu-id="34c77-152">Stap 1: het Azure Active Directory-token verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="34c77-152">Step 1: Obtain an Azure Active Directory token.</span></span>
<span data-ttu-id="34c77-153">De Data Lake Store SDK biedt handige methoden om de beveiligingstokens te beheren die nodig zijn om te communiceren met het Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="34c77-153">The Data Lake Store SDK provides convenient methods that let you manage the security tokens needed to talk to the Data Lake Store account.</span></span> <span data-ttu-id="34c77-154">Dit zijn echter niet de enige methoden die met SDK kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34c77-154">However, the SDK does not mandate that only these methods be used.</span></span> <span data-ttu-id="34c77-155">U kunt elke andere methode voor het verkrijgen van een token gebruiken. Zo kunt u de [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java) gebruiken, of uw persoonlijke code.</span><span class="sxs-lookup"><span data-stu-id="34c77-155">You can use any other means of obtaining token as well, like using the [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), or your own custom code.</span></span>

<span data-ttu-id="34c77-156">Als u de Data Lake Store SDK wilt gebruiken om het token te verkrijgen voor de Active Directory-webtoepassing die u eerder hebt gemaakt, gebruikt u een van de subklassen `AccessTokenProvider` (in het onderstaande voorbeeld wordt `ClientCredsTokenProvider` gebruikt).</span><span class="sxs-lookup"><span data-stu-id="34c77-156">To use the Data Lake Store SDK to obtain token for the Active Directory Web application you created earlier, use one of the subclasses of `AccessTokenProvider` (the example below uses `ClientCredsTokenProvider`).</span></span> <span data-ttu-id="34c77-157">De tokenprovider slaat de referenties die worden gebruikt voor het ophalen van het token, op in de cache en vernieuwt het token automatisch als het bijna is verlopen.</span><span class="sxs-lookup"><span data-stu-id="34c77-157">The token provider caches the creds used to obtain the token in memory, and automatically renews the token if it is about to expire.</span></span> <span data-ttu-id="34c77-158">Het is mogelijk om uw eigen subklassen te maken van `AccessTokenProvider`, zodat tokens worden opgehaald door de code van de klant. In dit voorbeeld gebruiken we voor het gemak het token dat is opgegeven in de SDK.</span><span class="sxs-lookup"><span data-stu-id="34c77-158">It is possible to create your own subclasses of `AccessTokenProvider` so tokens are obtained by your customer code, but for now let's just use the one provided in the SDK.</span></span>

<span data-ttu-id="34c77-159">Vervang **FILL-IN-HERE** met de daadwerkelijke waarden voor de Azure Active Directory-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="34c77-159">Replace **FILL-IN-HERE** with the actual values for the Azure Active Directory Web application.</span></span>

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a><span data-ttu-id="34c77-160">Stap 2: een Azure Data Lake Store-clientobject (ADLStoreClient-object) verkrijgen</span><span class="sxs-lookup"><span data-stu-id="34c77-160">Step 2: Create an Azure Data Lake Store client (ADLStoreClient) object</span></span>
<span data-ttu-id="34c77-161">Voor het maken van een [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/)-object moet u de Data Lake Store-accountnaam en de tokenprovider opgeven die u in de vorige stap hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="34c77-161">Creating an [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) object requires you to specify the Data Lake Store account name and the token provider you generated in the last step.</span></span> <span data-ttu-id="34c77-162">De Data Lake Store-accountnaam moet een volledig gekwalificeerde domeinnaam zijn.</span><span class="sxs-lookup"><span data-stu-id="34c77-162">Note that the Data Lake Store account name needs to be a fully qualified domain name.</span></span> <span data-ttu-id="34c77-163">Vervang bijvoorbeeld **FILL-IN-HERE** met iets als **mydatalakestore.azuredatalakestore.net**.</span><span class="sxs-lookup"><span data-stu-id="34c77-163">For example, replace **FILL-IN-HERE** with something like **mydatalakestore.azuredatalakestore.net**.</span></span>

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just the account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

### <a name="step-3-use-the-adlstoreclient-to-perform-file-and-directory-operations"></a><span data-ttu-id="34c77-164">Stap 3: de ADLStoreClient gebruiken om bestand- en mapbewerkingen uit te voeren</span><span class="sxs-lookup"><span data-stu-id="34c77-164">Step 3: Use the ADLStoreClient to perform file and directory operations</span></span>
<span data-ttu-id="34c77-165">De code hieronder bevat voorbeelden van tekstfragmenten van een aantal veelvoorkomende bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="34c77-165">The code below contains example snippets of some common operations.</span></span> <span data-ttu-id="34c77-166">Bekijk de volledige [Data Lake Store Java SDK API-documenten](https://azure.github.io/azure-data-lake-store-java/javadoc/) van het **ADLStoreClient**-object om andere bewerkingen te bekijken.</span><span class="sxs-lookup"><span data-stu-id="34c77-166">You can look at the full [Data Lake Store Java SDK API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/) of the **ADLStoreClient** object to see other operations.</span></span>

<span data-ttu-id="34c77-167">Bestanden worden gelezen en geschreven met behulp van standaard Java-streams.</span><span class="sxs-lookup"><span data-stu-id="34c77-167">Note that files are read from and written into using standard Java streams.</span></span> <span data-ttu-id="34c77-168">Dit betekent dat u een willekeurige Java-stream gelaagd bovenop de Data Lake Store-streams kunt plaatsen om van standaard Java-functionaliteit te profiteren (bijv. printstreams voor uitvoer met opmaak, of een van de compressie- of versleutelingsstreams voor extra functionaliteit enzovoort).</span><span class="sxs-lookup"><span data-stu-id="34c77-168">This means that you can layer any of the Java streams on top of the Data Lake Store streams to benefit from standard Java functionality (e.g., Print streams for formatted output, or any of the compression or encryption streams for additional functionality on top, etc.).</span></span>

     // create file and write some content
     String filename = "/a/b/c.txt";
     OutputStream stream = client.createFile(filename, IfExists.OVERWRITE  );
     PrintStream out = new PrintStream(stream);
     for (int i = 1; i <= 10; i++) {
         out.println("This is line #" + i);
         out.format("This is the same line (%d), but using formatted output. %n", i);
     }
     out.close();
    
    // set file permission
    client.setPermission(filename, "744");

    // append to file
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

    // concatenate the two files into one
    List<String> fileList = Arrays.asList("/a/b/c.txt", "/a/b/d.txt");
    client.concatenateFiles("/a/b/f.txt", fileList);

    //rename the file
    client.rename("/a/b/f.txt", "/a/b/g.txt");

    // list directory contents
    List<DirectoryEntry> list = client.enumerateDirectory("/a/b", 2000);
    System.out.println("Directory listing for directory /a/b:");
    for (DirectoryEntry entry : list) {
        printDirectoryInfo(entry);
    }

    // delete directory along with all the subdirectories and files in it
    client.deleteRecursive("/a");

#### <a name="step-4-build-and-run-the-application"></a><span data-ttu-id="34c77-169">Stap 4: de toepassing bouwen en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="34c77-169">Step 4: Build and run the application</span></span>
1. <span data-ttu-id="34c77-170">Klik op de knop **Uitvoeren** om de toepassing vanuit een IDE uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="34c77-170">To run from within an IDE, locate and press the **Run** button.</span></span> <span data-ttu-id="34c77-171">Gebruik [exec:exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html) om deze vanuit Maven uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="34c77-171">To run from Maven, use [exec:exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span></span>
2. <span data-ttu-id="34c77-172">Als u een afzonderlijke jar wilt maken die u vanuit de opdrachtregel kunt uitvoeren, bouwt u de jar met alle afhankelijkheden geïntegreerd met behulp van de [Maven assembly-invoegtoepassing](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span><span class="sxs-lookup"><span data-stu-id="34c77-172">To produce a standalone jar that you can run from command-line build the jar with all dependencies included, using the [Maven assembly plugin](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span></span> <span data-ttu-id="34c77-173">De pom.xml in de [voorbeeldbroncode van GitHub](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) bevat een voorbeeld van hoe u dat doet.</span><span class="sxs-lookup"><span data-stu-id="34c77-173">The pom.xml in the [example source code on github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) has an example of how to do this.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34c77-174">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="34c77-174">Next steps</span></span>
* [<span data-ttu-id="34c77-175">JavaDoc verkennen voor de Java-SDK</span><span class="sxs-lookup"><span data-stu-id="34c77-175">Explore JavaDoc for the Java SDK</span></span>](https://azure.github.io/azure-data-lake-store-java/javadoc/)
* [<span data-ttu-id="34c77-176">Gegevens in Data Lake Store beveiligen</span><span class="sxs-lookup"><span data-stu-id="34c77-176">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="34c77-177">Azure Data Lake Analytics gebruiken met Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="34c77-177">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="34c77-178">Azure HDInsight gebruiken met Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="34c77-178">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

