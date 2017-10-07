---
title: een certificaatarchief voor toohello Java CA aaaAdd | Microsoft Docs
description: Meer informatie over hoe tooadd een certificaat (certificeringsinstantie) certificaat toohello Java CA-certificaat (cacerts) opslaan voor Twilio-service of Azure Service Bus.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: d3699b0a-835c-43fb-844d-9c25344e5cda
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 030e43129580023942dee662e72d2f443167f308
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-certificate-toohello-java-ca-certificates-store"></a>Toevoegen van een certificaat toohello Java CA-archief voor certificaten
Hallo stappen ziet u hoe tooadd een certificaat (certificeringsinstantie) certificaat toohello Java CA-certificaat (cacerts) opslaan. Hallo-voorbeeld gebruikt is voor Hallo CA-certificaat vereist voor Hallo Twilio-service. Informatie later in Hallo onderwerp wordt beschreven hoe tooinstall Hallo CA-certificaat voor hello Azure Service Bus. 

U kunt uw JDK en toe te voegen tooyour Azure-project van keytool tooadd Hallo CA-certificaat voorafgaande toozipping gebruiken **approot** map, of u een taak die voor Azure opstarten die keytool tooadd Hallo certificaat gebruikt kan worden uitgevoerd. In dit voorbeeld wordt ervan uitgegaan dat u een eerdere toohello voor CA-certificaat wordt ingepakt JDK toevoegt. Ook een specifieke CA-certificaat wordt gebruikt in Hallo voorbeeld, maar Hallo stappen voor het verkrijgen van een andere CA-certificaat en u deze importeert in Hallo cacerts store is vergelijkbaar.

## <a name="tooadd-a-certificate-toohello-cacerts-store"></a>tooadd een certificaat toohello cacerts opslaan
1. Bij een opdrachtprompt die is ingesteld van tooyour JDK **jdk\jre\lib\security** map Hallo na toosee welke certificaten zijn geïnstalleerd:
   
    `keytool -list -keystore cacerts`
   
    Wordt u gevraagd om Hallo store wachtwoord. is het standaardwachtwoord Hallo **changeit**. (Als u toochange Hallo wachtwoord wilt, Zie de documentatie bij de Hallo keytool op <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.) In dit voorbeeld wordt ervan uitgegaan dat certificaat Hallo met MD5 vingerafdruk 67:CB:9 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 niet wordt weergegeven, en dat u wilt dat tooimport it (dit bepaalde certificaat nodig door Hallo Twilio-API-service).
2. Hallo certificaat verkrijgen van de lijst van certificaten die wordt vermeld op Hallo [GeoTrust basiscertificaten](http://www.geotrust.com/resources/root-certificates/). Met de rechtermuisknop op de koppeling voor het Hallo-certificaat met serienummer 35:DE:F4:CF hello en sla het toohello **jdk\jre\lib\security** map. Voor dit voorbeeld is opgeslagen tooa-bestand met de naam **Equifax\_Secure\_certificaat\_Authority.cer**.
3. Hallo-certificaat importeren via Hallo volgende opdracht:
   
    `keytool -keystore cacerts -importcert -alias equifaxsecureca -file Equifax_Secure_Certificate_Authority.cer`
   
    Wanneer u daarom wordt gevraagd tootrust dit certificaat als Hallo certificaat MD5 vingerafdruk 67:CB:9 D heeft: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4, reageren door te typen **y**.
4. Voer Hallo na de opdracht tooensure Hallo CA-certificaat zijn geïmporteerd:
   
    `keytool -list -keystore cacerts`
5. ZIP-Hallo JDK en toe te voegen tooyour Azure-project van **approot** map.

Zie voor meer informatie over keytool <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.

## <a name="azure-root-certificates"></a>Azure basiscertificaten
De toepassingen die gebruikmaken van Azure-services (zoals Azure Service Bus) moeten tootrust hello Baltimore CyberTrust-basiscertificaat. (15 April 2013 vanaf Azure begon met het migreren van Hallo GTE CyberTrust globale Root toohello Baltimore CyberTrust Root. Deze migratie duurt enkele maanden toocomplete.)

Hallo Baltimore certificaat mogelijk al zijn geïnstalleerd in uw archief cacerts, dus onthouden toorun hello **keytool-lijst** eerste toosee opdracht als deze al bestaat.

Als u moet tooadd Baltimore CyberTrust Root hello, heeft het serienummer 02:00:00:b9 en SHA1 vingerafdruk d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2 c: 78:db:28:52:ca:e4:74. Kan worden gedownload vanaf <https://cacert.omniroot.com/bc2025.crt>, opgeslagen tooa lokaal bestand met extensie **.cer**, en vervolgens importeert met **keytool** zoals hierboven.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over het Hallo-basiscertificaten gebruikt door Azure [Azure Root Certificate migratie](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx).

Zie voor meer informatie over Java [Azure voor Java-ontwikkelaars](/java/azure).

