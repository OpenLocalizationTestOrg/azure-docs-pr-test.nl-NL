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
# <a name="export-hello-azure-cosmos-db-emulator-certificates-for-use-with-java-python-and-nodejs"></a>Hello Azure Cosmos DB Emulator certificaten gebruiken met Java, Python en Node.js exporteren

[**Hallo Emulator downloaden**](https://aka.ms/cosmosdb-emulator)

Hello Azure Cosmos DB Emulator biedt een lokale omgeving waarin hello Azure DB die Cosmos-service voor ontwikkelingsdoeleinden, met inbegrip van het gebruik van SSL-verbindingen. Dit artikel laat zien hoe tooexport Hallo SSL-certificaten voor gebruik met talen en runtimes die niet worden geïntegreerd in de Windows-certificaatarchief zoals Java die gebruikmaakt van een eigen Hallo [certificaatarchief](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) en Python dat gebruikmaakt van [socket wrappers](https://docs.python.org/2/library/ssl.html) en Node.js dat gebruikmaakt van [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback). Meer informatie over het Hallo-emulator in [gebruik hello Azure Cosmos DB Emulator voor ontwikkeling en tests](./local-emulator.md).

Deze zelfstudie behandelt Hallo taken te volgen:

> [!div class="checklist"]
> * Certificaten draaien
> * SSL-certificaat exporteren
> * Leren hoe toouse Hallo certificaat in Java, Python en Node.js

## <a name="certification-rotation"></a>Rotatie van de certificeringsinstantie

Certificaten in hello dat Azure Cosmos DB lokale Emulator zijn gegenereerd Hallo eerst Hallo-emulator wordt gestart. Er zijn twee certificaten. Een gebruikt voor verbinding met lokale toohello-emulator en één voor het beheren van geheimen binnen Hallo-emulator. gewenste tooexport Hallo-certificaat is Hallo verbindingscertificaat met de weergavenaam 'DocumentDBEmulatorCertificate' Hallo.

Beide certificaten kunnen worden hersteld door te klikken op **gegevens opnieuw** zoals hieronder wordt weergegeven van Azure Cosmos DB-Emulator wordt uitgevoerd in Hallo Windows-systeemvak. Als u Hallo certificaten opnieuw genereren en hebben ze hebt geïnstalleerd in Hallo Java-certificaatarchief of ze ergens anders gebruikt, moet u tooupdate ze anders uw toepassing niet meer verbinding maakt toohello lokale emulator.

![Azure DB Cosmos lokale emulator opnieuw instellen van gegevens](./media/local-emulator-export-ssl-certificates/database-local-emulator-reset-data.png)

## <a name="how-tooexport-hello-azure-cosmos-db-ssl-certificate"></a>Hoe tooexport hello Azure Cosmos DB SSL-certificaat

1. Hallo Windows Certificate manager start met certlm.msc en navigeer toohello Personal -> map certificaten en open Hallo-certificaat met de beschrijvende naam Hallo **DocumentDbEmulatorCertificate**.

    ![Azure DB Cosmos lokale emulator exporteren stap 1](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-1.png)

2. Klik op **Details** vervolgens **OK**.

    ![Azure DB Cosmos lokale emulator exporteren stap 2](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-2.png)

3. Klik op **tooFile kopiëren...** .

    ![Azure DB Cosmos lokale emulator exporteren stap 3](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-3.png)

4. Klik op **Volgende**.

    ![Azure DB Cosmos lokale emulator exporteren stap 4](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-4.png)

5. Klik op **Nee, de persoonlijke sleutel niet exporteren**, klikt u vervolgens op **volgende**.

    ![Azure DB Cosmos lokale emulator exporteren stap 5](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-5.png)

6. Klik op **Base-64 gecodeerde X.509 (. CER)** en vervolgens **volgende**.

    ![Azure DB Cosmos lokale emulator stap 6 exporteren](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-6.png)

7. Hallo-certificaat van een naam geven. In dit geval **documentdbemulatorcert** en klik vervolgens op **volgende**.

    ![Azure DB Cosmos lokale emulator stap 7 exporteren](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-7.png)

8. Klik op **Voltooien**.

    ![Azure DB Cosmos lokale emulator stap 8 exporteren](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-8.png)

## <a name="how-toouse-hello-certificate-in-java"></a>Hoe toouse Hallo certificaat in Java

Bij het uitvoeren van Java-toepassingen of MongoDB-toepassingen die gebruikmaken van Hallo Java-client is eenvoudiger tooinstall Hallo certificaat in Hallo Java standaard certificaatarchief dan doorgeven Hallo '-Djavax.net.ssl.trustStore=<keystore> - Djavax.net.ssl.trustStorePassword= '<password>' vlaggen. Bijvoorbeeld Hallo opgenomen [Java-voorbeeldtoepassing](https://localhost:8081/_explorer/index.html) is afhankelijk van Hallo standaard certificaatarchief.

Volg de instructies Hallo in Hallo [toevoegen van een certificaat toohello Java CA certificatenarchief](https://docs.microsoft.com/azure/java-add-certificate-ca-store) tooimport Hallo x.509-certificaat in Hallo standaard Java-certificaatarchief. Houd werkt Vergeet niet dat u in map Hallo % JAVA_HOME % wanneer keytool wordt uitgevoerd.

Eenmaal Hallo 'CosmosDBEmulatorCertificate' SSL-certificaat is geïnstalleerd uw toepassing moet kunnen tooconnect en gebruik Hallo lokale Azure Cosmos DB-Emulator. Als u toohave problemen doorgaat kunt u toofollow hello [SSL/TLS-verbindingen voor foutopsporing](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) artikel. Is het zeer waarschijnlijk Hallo-certificaat is niet geïnstalleerd in Hallo %JAVA_HOME%/jre/lib/security/cacerts archief. Voor bijvoorbeeld als er meerdere geïnstalleerde versies van uw toepassing Java maakt mogelijk gebruik van een andere cacerts archief dan Hallo een die u bijgewerkt.

## <a name="how-toouse-hello-certificate-in-python"></a>Hoe toouse Hallo certificaat in Python

Door standaard Hallo [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) voor Hallo DocumentDB API wordt niet proberen en Hallo SSL-certificaat gebruiken om verbinding te maken van lokale toohello-emulator. Als u dat wilt toouse SSL-validatie u Hallo voorbeelden in Hallo voert [Python socket wrappers](https://docs.python.org/2/library/ssl.html) documentatie.

## <a name="how-toouse-hello-certificate-in-nodejs"></a>Hoe toouse Hallo certificaat in Node.js

Door standaard Hallo [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) voor Hallo DocumentDB API wordt niet proberen en Hallo SSL-certificaat gebruiken om verbinding te maken van lokale toohello-emulator. Als u dat wilt toouse SSL-validatie u Hallo voorbeelden in Hallo voert [Node.js documentatie](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u Hallo volgende gedaan:

> [!div class="checklist"]
> * Gedraaide certificaten
> * Geëxporteerde Hallo SSL-certificaat
> * Hebt u geleerd hoe toouse Hallo certificaat in Java, Python en Node.js

Nu kunt u verder toohello concepten sectie voor meer informatie over Cosmos-DB.

> [!div class="nextstepaction"]
> [Wereldwijde distributie](distribute-data-globally.md) 
