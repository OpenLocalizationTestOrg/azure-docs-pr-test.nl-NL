---
title: aaaExport hello Azure Cosmos DB Emulator certificaten | Microsoft Docs
description: Bij het ontwikkelen van in talen en runtimes die geen van Windows-certificaatarchief Hallo gebruikmaken u moet tooexport en Hallo SSL-certificaten te beheren. Dit bericht geeft stapsgewijze instructies.
services: cosmos-db
documentationcenter: 
keywords: Azure Cosmos DB Emulator
author: voellm
manager: jhubbard
editor: 
ms.assetid: ef43deda-c2e9-4193-99e2-7f6a88a0319f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: tvoellm
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: db56cda856fccf93d71ae5b21c4090ccb9aa40a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="export-hello-azure-cosmos-db-emulator-certificates-for-use-with-java-python-and-nodejs"></a><span data-ttu-id="6e091-105">Hello Azure Cosmos DB Emulator certificaten gebruiken met Java, Python en Node.js exporteren</span><span class="sxs-lookup"><span data-stu-id="6e091-105">Export hello Azure Cosmos DB Emulator certificates for use with Java, Python, and Node.js</span></span>

[<span data-ttu-id="6e091-106">**Hallo Emulator downloaden**</span><span class="sxs-lookup"><span data-stu-id="6e091-106">**Download hello Emulator**</span></span>](https://aka.ms/cosmosdb-emulator)

<span data-ttu-id="6e091-107">Hello Azure Cosmos DB Emulator biedt een lokale omgeving waarin hello Azure DB die Cosmos-service voor ontwikkelingsdoeleinden, met inbegrip van het gebruik van SSL-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="6e091-107">hello Azure Cosmos DB Emulator provides a local environment that emulates hello Azure Cosmos DB service for development purposes including its use of SSL connections.</span></span> <span data-ttu-id="6e091-108">Dit artikel laat zien hoe tooexport Hallo SSL-certificaten voor gebruik met talen en runtimes die niet worden geïntegreerd in de Windows-certificaatarchief zoals Java die gebruikmaakt van een eigen Hallo [certificaatarchief](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) en Python dat gebruikmaakt van [socket wrappers](https://docs.python.org/2/library/ssl.html) en Node.js dat gebruikmaakt van [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="6e091-108">This post demonstrates how tooexport hello SSL certificates for use in languages and runtimes that do not integrate with hello Windows Certificate Store such as Java which uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) and Python which uses [socket wrappers](https://docs.python.org/2/library/ssl.html) and Node.js which uses [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span> <span data-ttu-id="6e091-109">Meer informatie over het Hallo-emulator in [gebruik hello Azure Cosmos DB Emulator voor ontwikkeling en tests](./local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="6e091-109">You can read more about hello emulator in [Use hello Azure Cosmos DB Emulator for development and testing](./local-emulator.md).</span></span>

<span data-ttu-id="6e091-110">Deze zelfstudie behandelt Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="6e091-110">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6e091-111">Certificaten draaien</span><span class="sxs-lookup"><span data-stu-id="6e091-111">Rotating certificates</span></span>
> * <span data-ttu-id="6e091-112">SSL-certificaat exporteren</span><span class="sxs-lookup"><span data-stu-id="6e091-112">Exporting SSL certificate</span></span>
> * <span data-ttu-id="6e091-113">Leren hoe toouse Hallo certificaat in Java, Python en Node.js</span><span class="sxs-lookup"><span data-stu-id="6e091-113">Learning how toouse hello certificate in Java, Python, and Node.js</span></span>

## <a name="certification-rotation"></a><span data-ttu-id="6e091-114">Rotatie van de certificeringsinstantie</span><span class="sxs-lookup"><span data-stu-id="6e091-114">Certification rotation</span></span>

<span data-ttu-id="6e091-115">Certificaten in hello dat Azure Cosmos DB lokale Emulator zijn gegenereerd Hallo eerst Hallo-emulator wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="6e091-115">Certificates in hello Azure Cosmos DB Local Emulator are generated hello first time hello emulator is run.</span></span> <span data-ttu-id="6e091-116">Er zijn twee certificaten.</span><span class="sxs-lookup"><span data-stu-id="6e091-116">There are two certificates.</span></span> <span data-ttu-id="6e091-117">Een gebruikt voor verbinding met lokale toohello-emulator en één voor het beheren van geheimen binnen Hallo-emulator.</span><span class="sxs-lookup"><span data-stu-id="6e091-117">One used for connecting toohello local emulator and one for managing secrets within hello emulator.</span></span> <span data-ttu-id="6e091-118">gewenste tooexport Hallo-certificaat is Hallo verbindingscertificaat met de weergavenaam 'DocumentDBEmulatorCertificate' Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e091-118">hello certificate you want tooexport is hello connection certificate with hello friendly name "DocumentDBEmulatorCertificate".</span></span>

<span data-ttu-id="6e091-119">Beide certificaten kunnen worden hersteld door te klikken op **gegevens opnieuw** zoals hieronder wordt weergegeven van Azure Cosmos DB-Emulator wordt uitgevoerd in Hallo Windows-systeemvak.</span><span class="sxs-lookup"><span data-stu-id="6e091-119">Both certificates can be regenerated by clicking **Reset Data** as shown below from Azure Cosmos DB Emulator running in hello Windows Tray.</span></span> <span data-ttu-id="6e091-120">Als u Hallo certificaten opnieuw genereren en hebben ze hebt geïnstalleerd in Hallo Java-certificaatarchief of ze ergens anders gebruikt, moet u tooupdate ze anders uw toepassing niet meer verbinding maakt toohello lokale emulator.</span><span class="sxs-lookup"><span data-stu-id="6e091-120">If you regenerate hello certificates and have installed them into hello Java certificate store or used them elsewhere you will need tooupdate them, otherwise your application will no longer connect toohello local emulator.</span></span>

![Azure DB Cosmos lokale emulator opnieuw instellen van gegevens](./media/local-emulator-export-ssl-certificates/database-local-emulator-reset-data.png)

## <a name="how-tooexport-hello-azure-cosmos-db-ssl-certificate"></a><span data-ttu-id="6e091-122">Hoe tooexport hello Azure Cosmos DB SSL-certificaat</span><span class="sxs-lookup"><span data-stu-id="6e091-122">How tooexport hello Azure Cosmos DB SSL certificate</span></span>

1. <span data-ttu-id="6e091-123">Hallo Windows Certificate manager start met certlm.msc en navigeer toohello Personal -> map certificaten en open Hallo-certificaat met de beschrijvende naam Hallo **DocumentDbEmulatorCertificate**.</span><span class="sxs-lookup"><span data-stu-id="6e091-123">Start hello Windows Certificate manager by running certlm.msc and navigate toohello Personal->Certificates folder and open hello certificate with hello friendly name **DocumentDbEmulatorCertificate**.</span></span>

    ![Azure DB Cosmos lokale emulator exporteren stap 1](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-1.png)

2. <span data-ttu-id="6e091-125">Klik op **Details** vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="6e091-125">Click on **Details** then **OK**.</span></span>

    ![Azure DB Cosmos lokale emulator exporteren stap 2](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-2.png)

3. <span data-ttu-id="6e091-127">Klik op **tooFile kopiëren...** .</span><span class="sxs-lookup"><span data-stu-id="6e091-127">Click **Copy tooFile...**.</span></span>

    ![Azure DB Cosmos lokale emulator exporteren stap 3](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-3.png)

4. <span data-ttu-id="6e091-129">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="6e091-129">Click **Next**.</span></span>

    ![Azure DB Cosmos lokale emulator exporteren stap 4](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-4.png)

5. <span data-ttu-id="6e091-131">Klik op **Nee, de persoonlijke sleutel niet exporteren**, klikt u vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="6e091-131">Click **No, do not export private key**, then click **Next**.</span></span>

    ![Azure DB Cosmos lokale emulator exporteren stap 5](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-5.png)

6. <span data-ttu-id="6e091-133">Klik op **Base-64 gecodeerde X.509 (. CER)** en vervolgens **volgende**.</span><span class="sxs-lookup"><span data-stu-id="6e091-133">Click on **Base-64 encoded X.509 (.CER)** and then **Next**.</span></span>

    ![Azure DB Cosmos lokale emulator stap 6 exporteren](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-6.png)

7. <span data-ttu-id="6e091-135">Hallo-certificaat van een naam geven.</span><span class="sxs-lookup"><span data-stu-id="6e091-135">Give hello certificate a name.</span></span> <span data-ttu-id="6e091-136">In dit geval **documentdbemulatorcert** en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="6e091-136">In this case **documentdbemulatorcert** and then click **Next**.</span></span>

    ![Azure DB Cosmos lokale emulator stap 7 exporteren](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-7.png)

8. <span data-ttu-id="6e091-138">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="6e091-138">Click **Finish**.</span></span>

    ![Azure DB Cosmos lokale emulator stap 8 exporteren](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-8.png)

## <a name="how-toouse-hello-certificate-in-java"></a><span data-ttu-id="6e091-140">Hoe toouse Hallo certificaat in Java</span><span class="sxs-lookup"><span data-stu-id="6e091-140">How toouse hello certificate in Java</span></span>

<span data-ttu-id="6e091-141">Bij het uitvoeren van Java-toepassingen of MongoDB-toepassingen die gebruikmaken van Hallo Java-client is eenvoudiger tooinstall Hallo certificaat in Hallo Java standaard certificaatarchief dan doorgeven Hallo '-Djavax.net.ssl.trustStore=<keystore> - Djavax.net.ssl.trustStorePassword= '<password>' vlaggen.</span><span class="sxs-lookup"><span data-stu-id="6e091-141">When running Java applications or MongoDB applications that use hello Java client it is easier tooinstall hello certificate into hello Java default certificate store than passing hello "-Djavax.net.ssl.trustStore=<keystore> -Djavax.net.ssl.trustStorePassword="<password>" flags.</span></span> <span data-ttu-id="6e091-142">Bijvoorbeeld Hallo opgenomen [Java-voorbeeldtoepassing](https://localhost:8081/_explorer/index.html) is afhankelijk van Hallo standaard certificaatarchief.</span><span class="sxs-lookup"><span data-stu-id="6e091-142">For example hello included [Java Demo application](https://localhost:8081/_explorer/index.html) depends on hello default certificate store.</span></span>

<span data-ttu-id="6e091-143">Volg de instructies Hallo in Hallo [toevoegen van een certificaat toohello Java CA certificatenarchief](https://docs.microsoft.com/azure/java-add-certificate-ca-store) tooimport Hallo x.509-certificaat in Hallo standaard Java-certificaatarchief.</span><span class="sxs-lookup"><span data-stu-id="6e091-143">Follow hello instructions in hello [Adding a Certificate toohello Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store) tooimport hello X.509 certificate into hello default Java certificate store.</span></span> <span data-ttu-id="6e091-144">Houd werkt Vergeet niet dat u in map Hallo % JAVA_HOME % wanneer keytool wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6e091-144">Keep in mind you will be working in hello %JAVA_HOME% directory when running keytool.</span></span>

<span data-ttu-id="6e091-145">Eenmaal Hallo 'CosmosDBEmulatorCertificate' SSL-certificaat is geïnstalleerd uw toepassing moet kunnen tooconnect en gebruik Hallo lokale Azure Cosmos DB-Emulator.</span><span class="sxs-lookup"><span data-stu-id="6e091-145">Once hello "CosmosDBEmulatorCertificate" SSL certificate is installed your application should be able tooconnect and use hello local Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="6e091-146">Als u toohave problemen doorgaat kunt u toofollow hello [SSL/TLS-verbindingen voor foutopsporing](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) artikel.</span><span class="sxs-lookup"><span data-stu-id="6e091-146">If you continue toohave trouble you may want toofollow hello [Debugging SSL/TLS Connections](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) article.</span></span> <span data-ttu-id="6e091-147">Is het zeer waarschijnlijk Hallo-certificaat is niet geïnstalleerd in Hallo %JAVA_HOME%/jre/lib/security/cacerts archief.</span><span class="sxs-lookup"><span data-stu-id="6e091-147">It is very likely hello certificate is not installed into hello %JAVA_HOME%/jre/lib/security/cacerts store.</span></span> <span data-ttu-id="6e091-148">Voor bijvoorbeeld als er meerdere geïnstalleerde versies van uw toepassing Java maakt mogelijk gebruik van een andere cacerts archief dan Hallo een die u bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="6e091-148">For example if you have multiple installed versions of Java your application may be using a different cacerts store than hello one you updated.</span></span>

## <a name="how-toouse-hello-certificate-in-python"></a><span data-ttu-id="6e091-149">Hoe toouse Hallo certificaat in Python</span><span class="sxs-lookup"><span data-stu-id="6e091-149">How toouse hello certificate in Python</span></span>

<span data-ttu-id="6e091-150">Door standaard Hallo [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) voor Hallo DocumentDB API wordt niet proberen en Hallo SSL-certificaat gebruiken om verbinding te maken van lokale toohello-emulator.</span><span class="sxs-lookup"><span data-stu-id="6e091-150">By default hello [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) for hello DocumentDB API will not try and use hello SSL certificate when connecting toohello local emulator.</span></span> <span data-ttu-id="6e091-151">Als u dat wilt toouse SSL-validatie u Hallo voorbeelden in Hallo voert [Python socket wrappers](https://docs.python.org/2/library/ssl.html) documentatie.</span><span class="sxs-lookup"><span data-stu-id="6e091-151">If however you want toouse SSL validation you can follow hello examples in hello [Python socket wrappers](https://docs.python.org/2/library/ssl.html) documentation.</span></span>

## <a name="how-toouse-hello-certificate-in-nodejs"></a><span data-ttu-id="6e091-152">Hoe toouse Hallo certificaat in Node.js</span><span class="sxs-lookup"><span data-stu-id="6e091-152">How toouse hello certificate in Node.js</span></span>

<span data-ttu-id="6e091-153">Door standaard Hallo [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) voor Hallo DocumentDB API wordt niet proberen en Hallo SSL-certificaat gebruiken om verbinding te maken van lokale toohello-emulator.</span><span class="sxs-lookup"><span data-stu-id="6e091-153">By default hello [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) for hello DocumentDB API will not try and use hello SSL certificate when connecting toohello local emulator.</span></span> <span data-ttu-id="6e091-154">Als u dat wilt toouse SSL-validatie u Hallo voorbeelden in Hallo voert [Node.js documentatie](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="6e091-154">If however you want toouse SSL validation you can follow hello examples in hello [Node.js documentation](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e091-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6e091-155">Next steps</span></span>

<span data-ttu-id="6e091-156">In deze zelfstudie hebt u Hallo volgende gedaan:</span><span class="sxs-lookup"><span data-stu-id="6e091-156">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6e091-157">Gedraaide certificaten</span><span class="sxs-lookup"><span data-stu-id="6e091-157">Rotated certificates</span></span>
> * <span data-ttu-id="6e091-158">Geëxporteerde Hallo SSL-certificaat</span><span class="sxs-lookup"><span data-stu-id="6e091-158">Exported hello SSL certificate</span></span>
> * <span data-ttu-id="6e091-159">Hebt u geleerd hoe toouse Hallo certificaat in Java, Python en Node.js</span><span class="sxs-lookup"><span data-stu-id="6e091-159">Learned how toouse hello certificate in Java, Python and Node.js</span></span>

<span data-ttu-id="6e091-160">Nu kunt u verder toohello concepten sectie voor meer informatie over Cosmos-DB.</span><span class="sxs-lookup"><span data-stu-id="6e091-160">You can now proceed toohello Concepts section for more information about Cosmos DB.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6e091-161">Wereldwijde distributie</span><span class="sxs-lookup"><span data-stu-id="6e091-161">Global distribution</span></span>](distribute-data-globally.md) 
