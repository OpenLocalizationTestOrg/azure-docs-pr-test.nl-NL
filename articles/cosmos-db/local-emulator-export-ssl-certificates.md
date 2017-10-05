---
title: De Azure Cosmos DB Emulator certificaten exporteren | Microsoft Docs
description: Bij het ontwikkelen van in talen en runtimes die geen van de Windows-certificaatarchief gebruikmaken moet u exporteren en de SSL-certificaten te beheren. Dit bericht geeft stapsgewijze instructies.
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
ms.openlocfilehash: 4add5028d50972316902cecd8c399781c012cb77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="export-the-azure-cosmos-db-emulator-certificates-for-use-with-java-python-and-nodejs"></a><span data-ttu-id="04ca6-105">Exporteren van de certificaten Azure Cosmos DB Emulator voor gebruiken met Java, Python en Node.js</span><span class="sxs-lookup"><span data-stu-id="04ca6-105">Export the Azure Cosmos DB Emulator certificates for use with Java, Python, and Node.js</span></span>

[<span data-ttu-id="04ca6-106">**Downloaden van de Emulator**</span><span class="sxs-lookup"><span data-stu-id="04ca6-106">**Download the Emulator**</span></span>](https://aka.ms/cosmosdb-emulator)

<span data-ttu-id="04ca6-107">De Azure-Emulator Cosmos DB biedt een lokale omgeving waarin de service Azure Cosmos DB voor ontwikkelingsdoeleinden, met inbegrip van het gebruik van SSL-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="04ca6-107">The Azure Cosmos DB Emulator provides a local environment that emulates the Azure Cosmos DB service for development purposes including its use of SSL connections.</span></span> <span data-ttu-id="04ca6-108">Dit artikel laat zien hoe u exporteert u het SSL-certificaat voor gebruik met talen en runtimes die niet worden geïntegreerd in de Windows-certificaatarchief zoals Java die gebruikmaakt van een eigen [certificaatarchief](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) en Python dat gebruikmaakt van [socket wrappers](https://docs.python.org/2/library/ssl.html) en Node.js dat gebruikmaakt van [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="04ca6-108">This post demonstrates how to export the SSL certificates for use in languages and runtimes that do not integrate with the Windows Certificate Store such as Java which uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) and Python which uses [socket wrappers](https://docs.python.org/2/library/ssl.html) and Node.js which uses [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span> <span data-ttu-id="04ca6-109">U kunt meer lezen over de emulator in [de Emulator Azure Cosmos DB gebruiken voor ontwikkeling en tests](./local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="04ca6-109">You can read more about the emulator in [Use the Azure Cosmos DB Emulator for development and testing](./local-emulator.md).</span></span>

<span data-ttu-id="04ca6-110">Deze zelfstudie bevat de volgende taken:</span><span class="sxs-lookup"><span data-stu-id="04ca6-110">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="04ca6-111">Certificaten draaien</span><span class="sxs-lookup"><span data-stu-id="04ca6-111">Rotating certificates</span></span>
> * <span data-ttu-id="04ca6-112">SSL-certificaat exporteren</span><span class="sxs-lookup"><span data-stu-id="04ca6-112">Exporting SSL certificate</span></span>
> * <span data-ttu-id="04ca6-113">Het gebruik van het certificaat in Java, Python en Node.js leren</span><span class="sxs-lookup"><span data-stu-id="04ca6-113">Learning how to use the certificate in Java, Python, and Node.js</span></span>

## <a name="certification-rotation"></a><span data-ttu-id="04ca6-114">Rotatie van de certificeringsinstantie</span><span class="sxs-lookup"><span data-stu-id="04ca6-114">Certification rotation</span></span>

<span data-ttu-id="04ca6-115">Certificaten in de Azure Cosmos DB lokale Emulator worden de eerste keer die is uitgevoerd op de emulator gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="04ca6-115">Certificates in the Azure Cosmos DB Local Emulator are generated the first time the emulator is run.</span></span> <span data-ttu-id="04ca6-116">Er zijn twee certificaten.</span><span class="sxs-lookup"><span data-stu-id="04ca6-116">There are two certificates.</span></span> <span data-ttu-id="04ca6-117">Een gebruikt voor het verbinden met de lokale emulator en één voor het beheren van geheimen in de emulator.</span><span class="sxs-lookup"><span data-stu-id="04ca6-117">One used for connecting to the local emulator and one for managing secrets within the emulator.</span></span> <span data-ttu-id="04ca6-118">Het certificaat dat u wilt exporteren, is het verbindingscertificaat met de beschrijvende naam 'DocumentDBEmulatorCertificate'.</span><span class="sxs-lookup"><span data-stu-id="04ca6-118">The certificate you want to export is the connection certificate with the friendly name "DocumentDBEmulatorCertificate".</span></span>

<span data-ttu-id="04ca6-119">Beide certificaten kunnen worden hersteld door te klikken op **gegevens opnieuw** zoals hieronder wordt weergegeven in Azure Cosmos DB-Emulator wordt uitgevoerd in het Windows-systeemvak.</span><span class="sxs-lookup"><span data-stu-id="04ca6-119">Both certificates can be regenerated by clicking **Reset Data** as shown below from Azure Cosmos DB Emulator running in the Windows Tray.</span></span> <span data-ttu-id="04ca6-120">Als u de certificaten opnieuw genereren en hebben ze in het certificaatarchief Java hebt geïnstalleerd of gebruikt ze ergens anders moet u deze bijwerken, anders uw toepassing wordt niet meer verbinding maken met de lokale emulator.</span><span class="sxs-lookup"><span data-stu-id="04ca6-120">If you regenerate the certificates and have installed them into the Java certificate store or used them elsewhere you will need to update them, otherwise your application will no longer connect to the local emulator.</span></span>

![Azure DB Cosmos lokale emulator opnieuw instellen van gegevens](./media/local-emulator-export-ssl-certificates/database-local-emulator-reset-data.png)

## <a name="how-to-export-the-azure-cosmos-db-ssl-certificate"></a><span data-ttu-id="04ca6-122">Het exporteren van het Azure Cosmos DB SSL-certificaat</span><span class="sxs-lookup"><span data-stu-id="04ca6-122">How to export the Azure Cosmos DB SSL certificate</span></span>

1. <span data-ttu-id="04ca6-123">Start de Windows-certificaatbeheerder door certlm.msc uitgevoerd en navigeer naar de map persoonlijke-> certificaten en het certificaat openen met de beschrijvende naam **DocumentDbEmulatorCertificate**.</span><span class="sxs-lookup"><span data-stu-id="04ca6-123">Start the Windows Certificate manager by running certlm.msc and navigate to the Personal->Certificates folder and open the certificate with the friendly name **DocumentDbEmulatorCertificate**.</span></span>

    ![Azure DB Cosmos lokale emulator exporteren stap 1](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-1.png)

2. <span data-ttu-id="04ca6-125">Klik op **Details** vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="04ca6-125">Click on **Details** then **OK**.</span></span>

    ![Azure DB Cosmos lokale emulator exporteren stap 2](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-2.png)

3. <span data-ttu-id="04ca6-127">Klik op **kopiëren naar bestand...** .</span><span class="sxs-lookup"><span data-stu-id="04ca6-127">Click **Copy to File...**.</span></span>

    ![Azure DB Cosmos lokale emulator exporteren stap 3](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-3.png)

4. <span data-ttu-id="04ca6-129">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="04ca6-129">Click **Next**.</span></span>

    ![Azure DB Cosmos lokale emulator exporteren stap 4](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-4.png)

5. <span data-ttu-id="04ca6-131">Klik op **Nee, de persoonlijke sleutel niet exporteren**, klikt u vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="04ca6-131">Click **No, do not export private key**, then click **Next**.</span></span>

    ![Azure DB Cosmos lokale emulator exporteren stap 5](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-5.png)

6. <span data-ttu-id="04ca6-133">Klik op **Base-64 gecodeerde X.509 (. CER)** en vervolgens **volgende**.</span><span class="sxs-lookup"><span data-stu-id="04ca6-133">Click on **Base-64 encoded X.509 (.CER)** and then **Next**.</span></span>

    ![Azure DB Cosmos lokale emulator stap 6 exporteren](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-6.png)

7. <span data-ttu-id="04ca6-135">Het certificaat een naam geven.</span><span class="sxs-lookup"><span data-stu-id="04ca6-135">Give the certificate a name.</span></span> <span data-ttu-id="04ca6-136">In dit geval **documentdbemulatorcert** en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="04ca6-136">In this case **documentdbemulatorcert** and then click **Next**.</span></span>

    ![Azure DB Cosmos lokale emulator stap 7 exporteren](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-7.png)

8. <span data-ttu-id="04ca6-138">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="04ca6-138">Click **Finish**.</span></span>

    ![Azure DB Cosmos lokale emulator stap 8 exporteren](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-8.png)

## <a name="how-to-use-the-certificate-in-java"></a><span data-ttu-id="04ca6-140">Het gebruik van het certificaat in Java</span><span class="sxs-lookup"><span data-stu-id="04ca6-140">How to use the certificate in Java</span></span>

<span data-ttu-id="04ca6-141">Bij het uitvoeren van Java-toepassingen of MongoDB-toepassingen die gebruikmaken van de Java-client is het eenvoudiger om het certificaat installeren in het certificaatarchief van Java standaard dan geven de '-Djavax.net.ssl.trustStore=<keystore> -Djavax.net.ssl.trustStorePassword= '<password>'vlaggen.</span><span class="sxs-lookup"><span data-stu-id="04ca6-141">When running Java applications or MongoDB applications that use the Java client it is easier to install the certificate into the Java default certificate store than passing the "-Djavax.net.ssl.trustStore=<keystore> -Djavax.net.ssl.trustStorePassword="<password>" flags.</span></span> <span data-ttu-id="04ca6-142">Bijvoorbeeld de opgenomen [Java-voorbeeldtoepassing](https://localhost:8081/_explorer/index.html) is afhankelijk van het standaard certificaatarchief.</span><span class="sxs-lookup"><span data-stu-id="04ca6-142">For example the included [Java Demo application](https://localhost:8081/_explorer/index.html) depends on the default certificate store.</span></span>

<span data-ttu-id="04ca6-143">Volg de instructies in de [een certificaat toevoegen aan de Java CA certificatenarchief](https://docs.microsoft.com/azure/java-add-certificate-ca-store) het X.509-certificaat importeren in het certificaatarchief van de standaard Java.</span><span class="sxs-lookup"><span data-stu-id="04ca6-143">Follow the instructions in the [Adding a Certificate to the Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store) to import the X.509 certificate into the default Java certificate store.</span></span> <span data-ttu-id="04ca6-144">Houd werkt Vergeet niet dat u in de map % JAVA_HOME % wanneer keytool wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="04ca6-144">Keep in mind you will be working in the %JAVA_HOME% directory when running keytool.</span></span>

<span data-ttu-id="04ca6-145">Eenmaal de 'CosmosDBEmulatorCertificate' SSL-certificaat is geïnstalleerd uw toepassing moet kunnen verbinding maken en gebruiken van de lokale Azure Cosmos DB-Emulator.</span><span class="sxs-lookup"><span data-stu-id="04ca6-145">Once the "CosmosDBEmulatorCertificate" SSL certificate is installed your application should be able to connect and use the local Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="04ca6-146">Als u problemen blijft ondervinden kunt u volgen de [SSL/TLS-verbindingen voor foutopsporing](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) artikel.</span><span class="sxs-lookup"><span data-stu-id="04ca6-146">If you continue to have trouble you may want to follow the [Debugging SSL/TLS Connections](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) article.</span></span> <span data-ttu-id="04ca6-147">Het is zeer waarschijnlijk dat het certificaat is niet geïnstalleerd in het archief %JAVA_HOME%/jre/lib/security/cacerts.</span><span class="sxs-lookup"><span data-stu-id="04ca6-147">It is very likely the certificate is not installed into the %JAVA_HOME%/jre/lib/security/cacerts store.</span></span> <span data-ttu-id="04ca6-148">Voor bijvoorbeeld als er meerdere geïnstalleerde versies van uw toepassing Java mogelijk gebruik van een andere cacerts archief dan één die u bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="04ca6-148">For example if you have multiple installed versions of Java your application may be using a different cacerts store than the one you updated.</span></span>

## <a name="how-to-use-the-certificate-in-python"></a><span data-ttu-id="04ca6-149">Het gebruik van het certificaat in Python</span><span class="sxs-lookup"><span data-stu-id="04ca6-149">How to use the certificate in Python</span></span>

<span data-ttu-id="04ca6-150">Standaard de [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) voor de DocumentDB-API wordt niet proberen en de SSL-certificaat gebruiken bij het verbinden met de lokale emulator.</span><span class="sxs-lookup"><span data-stu-id="04ca6-150">By default the [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) for the DocumentDB API will not try and use the SSL certificate when connecting to the local emulator.</span></span> <span data-ttu-id="04ca6-151">Als maar u wilt gebruiken, SSL-validatie voert u de voorbeelden in de [Python socket wrappers](https://docs.python.org/2/library/ssl.html) documentatie.</span><span class="sxs-lookup"><span data-stu-id="04ca6-151">If however you want to use SSL validation you can follow the examples in the [Python socket wrappers](https://docs.python.org/2/library/ssl.html) documentation.</span></span>

## <a name="how-to-use-the-certificate-in-nodejs"></a><span data-ttu-id="04ca6-152">Het gebruik van het certificaat in Node.js</span><span class="sxs-lookup"><span data-stu-id="04ca6-152">How to use the certificate in Node.js</span></span>

<span data-ttu-id="04ca6-153">Standaard de [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) voor de DocumentDB-API wordt niet proberen en de SSL-certificaat gebruiken bij het verbinden met de lokale emulator.</span><span class="sxs-lookup"><span data-stu-id="04ca6-153">By default the [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) for the DocumentDB API will not try and use the SSL certificate when connecting to the local emulator.</span></span> <span data-ttu-id="04ca6-154">Als maar u wilt gebruiken, SSL-validatie voert u de voorbeelden in de [Node.js documentatie](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="04ca6-154">If however you want to use SSL validation you can follow the examples in the [Node.js documentation](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="04ca6-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="04ca6-155">Next steps</span></span>

<span data-ttu-id="04ca6-156">In deze zelfstudie hebt u het volgende gedaan:</span><span class="sxs-lookup"><span data-stu-id="04ca6-156">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="04ca6-157">Gedraaide certificaten</span><span class="sxs-lookup"><span data-stu-id="04ca6-157">Rotated certificates</span></span>
> * <span data-ttu-id="04ca6-158">Het SSL-certificaat wordt geëxporteerd</span><span class="sxs-lookup"><span data-stu-id="04ca6-158">Exported the SSL certificate</span></span>
> * <span data-ttu-id="04ca6-159">Geleerd hoe u het certificaat in Java, Python en Node.js</span><span class="sxs-lookup"><span data-stu-id="04ca6-159">Learned how to use the certificate in Java, Python and Node.js</span></span>

<span data-ttu-id="04ca6-160">U kunt nu doorgaan naar de sectie concepten voor meer informatie over Cosmos-DB.</span><span class="sxs-lookup"><span data-stu-id="04ca6-160">You can now proceed to the Concepts section for more information about Cosmos DB.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="04ca6-161">Wereldwijde distributie</span><span class="sxs-lookup"><span data-stu-id="04ca6-161">Global distribution</span></span>](distribute-data-globally.md) 
