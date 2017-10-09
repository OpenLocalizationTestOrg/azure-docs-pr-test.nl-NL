---
title: Azure Storage met een oplossing voor continue integratie van Jenkins aaaUsing | Microsoft Docs
description: Deze zelfstudie laat zien hoe toouse hello Azure blob-service als een opslagplaats voor artefacten die zijn gemaakt door een continue integratie Jenkins oplossing bouwen.
services: storage
documentationcenter: java
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: f4e5ca75-f6cb-4f74-981b-2aa06bb8de45
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: 853c0c6c028596b3057bdc1dbbc59a9415c0fb77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-storage-with-a-jenkins-continuous-integration-solution"></a>Azure Storage gebruiken met een Jenkins CI-oplossing
## <a name="overview"></a>Overzicht
Hallo volgende informatie wordt weergegeven hoe toouse Blob-opslag als een opslagplaats van build-artefacten die zijn gemaakt door een oplossing Jenkins continue integratie (CI) of als een bron van downloadbare bestanden toobe gebruikt in een buildproces. Een van de Hallo scenario's waarbij u dit nuttig vinden zou is wanneer u in een flexibele-ontwikkelomgeving coderen bent (met Java of andere talen) en u een opslagplaats voor uw artefacten build moet builds worden uitgevoerd op basis van continue integratie zodat u kan , bijvoorbeeld, ze delen met andere leden van de organisatie, uw klanten of houd een archief. Een ander scenario is als uw build-taak zelf vereist een andere bestanden, bijvoorbeeld afhankelijkheden toodownload als onderdeel van Hallo bouwen invoer.

In deze zelfstudie wordt u hello Azure Storage-invoegtoepassing voor Jenkins CI beschikbaar gesteld door Microsoft.

## <a name="overview-of-jenkins"></a>Overzicht van Jenkins
Jenkins schakelt continue integratie van een software-project doordat ontwikkelaars tooeasily hun codewijzigingen integreren en hebben geproduceerde automatisch en bouwt vaak, waardoor de productiviteit van ontwikkelaars Hallo Hallo. Builds worden samengesteld en build artefacten mag geüploade toovarious-opslagplaatsen. Dit onderwerp wordt beschreven hoe toouse Azure blob-opslag als Hallo opslagplaats van Hallo build-artefacten. Hierin ziet ook hoe toodownload afhankelijkheden van Azure blob-opslag.

Meer informatie over Jenkins kan worden gevonden op [Jenkins voldoen aan](https://wiki.jenkins-ci.org/display/JENKINS/Meet+Jenkins).

## <a name="benefits-of-using-hello-blob-service"></a>Voordelen van het gebruik van Hallo Blob-service
Voordelen van het gebruik van Hallo Blob-service toohost zijn voor uw build-artefacten flexibele ontwikkeling:

* Hoge beschikbaarheid van uw artefacten build en/of downloadbare afhankelijkheden.
* Prestaties wanneer uw oplossing Jenkins CI uw build-artefacten uploadt.
* Prestaties wanneer uw klanten en partners downloadt uw build-artefacten.
* De controle over het toegangsbeleid van de gebruiker de keuze tussen anonieme toegang, gedeelde toegang op basis van een verlopen handtekening toegang, persoonlijke toegang, enzovoort.

## <a name="prerequisites"></a>Vereisten
U wordt moet Hallo na toouse Hallo Blob-service met uw Jenkins CI-oplossing:

* Een oplossing Jenkins continue integratie.
  
    Als u een oplossing Jenkins CI momenteel geen hebt, kunt u een Jenkins CI-oplossing met behulp van de volgende techniek Hallo uitvoeren:
  
  1. Downloaden op een machine Java ingeschakeld jenkins.war van <http://jenkins-ci.org>.
  2. Voer bij een opdrachtprompt die is geopend toohello map jenkins.war met:
     
      `java -jar jenkins.war`

  3. Open in uw browser `http://localhost:8080/`. Hiermee opent u Hallo Jenkins dashboard, dat u gaat gebruiken tooinstall en hello Azure Storage-invoegtoepassing configureren.
     
      Terwijl een standaardoplossing Jenkins CI zou worden ingesteld in toorun als een service, toereikend Hallo Jenkins war uitgevoerd op de opdrachtregel Hallo voor deze zelfstudie.
* Een Azure-account. U kunt zich aanmelden voor een Azure-account op <http://www.azure.com>.
* Een Azure Storage-account. Als u nog een opslagaccount hebt, kunt u een maken met behulp van Hallo stappen op [een Opslagaccount maken](../common/storage-create-storage-account.md#create-a-storage-account).
* Bekend bent met de Hallo Jenkins CI-oplossing wordt aanbevolen, maar niet vereist, zoals hello volgende inhoud gebruikt een eenvoudig voorbeeld tooshow u stappen die nodig zijn bij gebruik van Hallo Blob-service als een opslagplaats voor Jenkins CI Hallo artefacten bouwen.

## <a name="how-toouse-hello-blob-service-with-jenkins-ci"></a>Hoe toouse Hallo Blob-service met Jenkins CI
toouse hello Blob-service met Jenkins, moet u tooinstall hello Azure Storage-invoegtoepassing, Hallo invoegtoepassing toouse uw storage-account configureren en maak vervolgens een na build-actie die uw opslagaccount build artefacten tooyour uploadt. Deze stappen worden beschreven in Hallo uit te voeren.

## <a name="how-tooinstall-hello-azure-storage-plugin"></a>Hoe tooinstall hello Azure Storage-invoegtoepassing
1. Klik in het Hallo Jenkins dashboard op **Jenkins beheren**.
2. In Hallo **beheren Jenkins** pagina, klikt u op **invoegtoepassingen beheren**.
3. Klik op Hallo **beschikbaar** tabblad.
4. In Hallo **artefact Uploaders** sectie selectievakje **invoegtoepassing voor Microsoft Azure Storage**.
5. Klik op **installeren zonder opnieuw opstarten** of **nu downloaden en installeren na opnieuw opstarten**.
6. Opnieuw opstarten Jenkins.

## <a name="how-tooconfigure-hello-azure-storage-plugin-toouse-your-storage-account"></a>Hoe tooconfigure hello Azure Storage-invoegtoepassing toouse uw storage-account
1. Klik in het Hallo Jenkins dashboard op **Jenkins beheren**.
2. In Hallo **beheren Jenkins** pagina, klikt u op **System configureren**.
3. In Hallo **configuratie van Microsoft Azure Storage-Account** sectie:
   1. Voer de naam van uw opslagaccount, die u van Hallo verkrijgen kunt [Azure Portal](https://portal.azure.com).
   2. Voer de sleutel van uw opslagaccount, ook kan worden verkregen uit Hallo [Azure Portal](https://portal.azure.com).
   3. Gebruik de standaardwaarde Hallo voor **eindpunt-URL van Blob-Service** als u van Hallo openbare Azure-cloud gebruikmaakt. Als u van een andere Azure-cloud gebruikmaakt, gebruikt u Hallo eindpunt als opgegeven in de Hallo [Azure Portal](https://portal.azure.com) voor uw opslagaccount. 
   4. Klik op **storage-referenties gevalideerd** toovalidate uw storage-account. 
   5. [Optioneel] Als u extra opslagaccounts die u en-klare beschikbaar tooyour Jenkins CI wilt hebt, klikt u op **Voeg meer Accounts voor opslag**.
   6. Klik op **opslaan** toosave uw instellingen.

## <a name="how-toocreate-a-post-build-action-that-uploads-your-build-artifacts-tooyour-storage-account"></a>Hoe toocreate een na build-actie die uw opslagaccount build artefacten tooyour geüpload
Instructie oog wordt eerst moeten we toocreate een taak die verschillende bestanden maken en vervolgens in Hallo na build actie tooupload Hallo bestanden tooyour storage-account toevoegen.

1. Klik in het Hallo Jenkins dashboard op **Nieuw Item**.
2. Naam Hallo taak **MyJob**, klikt u op **bouwen van een project vrije-stijl software**, en klik vervolgens op **OK**.
3. In Hallo **bouwen** sectie van configuratie van de taak hello, klikt u op **toevoegen build stap** en kies **Windows uitvoeren van batch-opdracht**.
4. In **opdracht**, Hallo volgende opdrachten gebruiken:

    ```   
    md text
    cd text
    echo Hello Azure Storage from Jenkins > hello.txt
    date /t > date.txt
    time /t >> date.txt
    ```

5. In Hallo **na build acties** sectie van configuratie van de taak hello, klikt u op **na build actie toevoegen** en kies **uploaden van Blob-opslag van artefacten tooAzure**.
6. Voor **opslagaccountnaam**, selecteer Hallo storage account toouse.
7. Voor **containernaam**, Hallo-container opgeven. (Hallo-container gemaakt als deze niet bestaat nog wanneer Hallo build artefacten worden geüpload.) U kunt gebruik maken van omgevingsvariabelen, dus voor dit voorbeeld geeft **${JOB_NAME}** als Hallo containernaam.
   
    **Tip**
   
    Hieronder Hallo **opdracht** sectie waarin u hebt opgegeven een script voor **Windows uitvoeren van batch-opdracht** is een koppeling toohello omgevingsvariabelen herkend door Jenkins. Klik op deze koppeling toolearn Hallo namen van omgevingsvariabelen en beschrijvingen. Houd er rekening mee dat omgeving variabelen die speciale tekens, zoals Hallo bevatten **BUILD_URL** omgevingsvariabele, zijn niet toegestaan als een containernaam of algemene virtueel pad.
8. Klik op **nieuwe container openbaar maken standaard** voor dit voorbeeld. (Als u een persoonlijke container toouse wilt, moet u een shared access signature tooallow toegang toocreate. Dat is buiten bereik Hallo van dit onderwerp. U kunt meer informatie over handtekeningen voor gedeelde toegang op [met behulp van Shared Access Signatures (SAS)](../storage-dotnet-shared-access-signature-part-1.md).)
9. [Optioneel] Klik op **schone container voordat u uploadt** als u wilt dat Hallo container toobe gewist van inhoud voordat build artefacten worden geüpload (laat het vakje uitgeschakeld als u niet dat tooclean Hallo inhoud van Hallo container wilt).
10. Voor **lijst van artefacten tooupload**, voer  **tekst /*.txt**.
11. Voor **algemene virtuele pad voor de geüploade artefacten**, voert u deze zelfstudie **${bouwen\_ID} / ${bouwen\_getal}**.
12. Klik op **opslaan** toosave uw instellingen.
13. Klik in het Hallo Jenkins dashboard op **nu bouwen** toorun **MyJob**. Bekijk Hallo console-uitvoer voor de status. Statusberichten voor Azure-opslag worden opgenomen in de console-uitvoer Hallo wanneer Hallo na build actie tooupload build artefacten wordt gestart.
14. Hallo-taak is voltooid, kunt u Hallo build artefacten bestuderen met openbare blob Hallo openen.
    1. Aanmelding toohello [Azure Portal](https://portal.azure.com).
    2. Klik op **opslag**.
    3. Klik op Hallo opslagaccountnaam die u voor Jenkins gebruikt.
    4. Klik op **Containers**.
    5. Klik op Hallo-container met de naam **myjob**, kleine letters versie Hallo van Hallo taaknaam die u tijdens het maken van Hallo Jenkins taak hebt toegewezen. Namen van containers en blobs namen zijn kleine letters (en hoofdlettergevoelig) in Azure-opslag. In de lijst Hallo blobs voor Hallo-container met de naam **myjob** ziet u **hello.txt** en **date.txt**. Hallo-URL voor een van deze items te kopiëren en in uw browser te openen. Als een artefact build ziet u Hallo-tekstbestand dat is geüpload.

Slechts één na build-actie die u artefacten tooAzure blob-opslag uploadt kan per taak worden gemaakt. Hallo één na build actie tooupload artefacten tooAzure blob-opslag kunt opgeven verschillende bestanden (inclusief jokertekens) en paden toofiles binnen **lijst van artefacten tooupload** met een puntkomma als scheidingsteken. Bijvoorbeeld, als uw Jenkins bouwen produceert JAR-bestanden en TXT-bestanden in uw werkruimte **bouwen** map en u tooupload beide tooAzure blob-opslag wilt, gebruikt u Hallo volgende voor Hallo **lijst van artefacten tooupload** waarde: **bouwen /\*JAR; build /\*.txt**. U kunt ook de syntaxis van de dubbele toospecify een toouse pad binnen Hallo blob-naam gebruiken. Bijvoorbeeld, als u wilt dat Hallo potten tooget geüpload met behulp van **binaire bestanden** in Hallo blobpad en de Hallo TXT-bestanden tooget geüpload met behulp van **mededelingen** in Hallo-blobpad Hallo volgende voor hello gebruiken  **Lijst met artefacten tooupload** waarde: **bouwen /\*. jar::binaries; build /\*. txt::notices**.

## <a name="how-toocreate-a-build-step-that-downloads-from-azure-blob-storage"></a>Hoe een stap build toocreate die downloadt van Azure blob-opslag
Hallo stappen te volgen laten zien hoe een build tooconfigure toodownload items stap uit Azure blob-opslag. Dit is handig als u tooinclude items in de build wilt, bijvoorbeeld potten die u in Azure bewaren blob-opslag.

1. In Hallo **bouwen** sectie van configuratie van de taak hello, klikt u op **toevoegen build stap** en kies **downloaden uit Azure Blob storage**.
2. Voor **opslagaccountnaam**, selecteer Hallo storage account toouse.
3. Voor **containernaam**, Hallo-naam van het Hallo-container met Hallo blobs gewenste toodownload opgeven. U kunt de omgevingsvariabelen.
4. Voor **Blob-naam**, Hallo blob-naam opgeven. U kunt de omgevingsvariabelen. U kunt ook een sterretje als jokerteken nadat u Hallo initiële (s) van Hallo blob-naam opgeven. Bijvoorbeeld: **project\***  geeft alle blobs die met beginnen **project**.
5. [Optioneel] Voor **downloadpad**, Hallo pad opgeven op Hallo Jenkins machine waar u bestanden toodownload uit Azure blob-opslag. Omgevingsvariabelen kunnen ook worden gebruikt. (Als u geen waarde voor opgeeft **downloadpad**, Hallo-bestanden uit Azure blob storage van de taak van de gedownloade toohello werkruimte zijn.)

Als er extra items die u wilt dat toodownload uit Azure blob storage, kunt u aanvullende build stappen.

Nadat u een build uitgevoerd, kunt u controleren of Hallo blobs die u verwacht zijn gedownload blik op de downloadlocatie, toosee of Hallo bouwen geschiedenis console-uitvoer.  

## <a name="components-used-by-hello-blob-service"></a>Onderdelen die worden gebruikt door Hallo Blob-service
Hallo hieronder biedt een overzicht van onderdelen Hallo Blob-service.

* **Storage-Account**: alle toegang tot tooAzure opslag wordt gedaan via een opslagaccount. Dit is Hallo hoogste niveau van de naamruimte Hallo voor toegang tot blobs. Een account kan een onbeperkt aantal containers bevatten, zolang de totale grootte minder dan 100TB is.
* **Container**: een container is een groepering van een reeks blobs. Alle blobs moeten zich in een container bevinden. Een account kan een onbeperkt aantal containers bevatten. Een container kan een onbeperkt aantal blobs bevatten.
* **BLOB**: een bestand van willekeurig type en de grootte. Er zijn twee typen kunnen worden opgeslagen in Azure Storage blobs: blok en pagina-blobs. De meeste bestanden zijn blok-blobs. Een enkel blok-blob kan up too200GB in grootte zijn. Deze zelfstudie maakt gebruik van blok-blobs. Pagina-blobs, een ander blobtype, kunnen worden up too1TB in grootte en zijn efficiënter bij het bereiken van de bytes in een bestand vaak worden gewijzigd. Zie voor meer informatie over blobs [blok-Blobs, toevoeg-Blobs en pagina-Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).
* **URL-indeling**: Blobs worden opgevraagd met Hallo URL-indeling te volgen:
  
    `http://storageaccount.blob.core.windows.net/container_name/blob_name`
  
    (Hallo de indeling van de van toepassing toohello openbare Azure-cloud. Als u een andere Azure-cloud gebruikt, gebruik Hallo endpoint binnen Hallo [Azure Portal](https://portal.azure.com) toodetermine URL-eindpunt.)
  
    In bovenstaande Hallo-indeling `storageaccount` vertegenwoordigt de naam van uw opslagaccount Hallo `container_name` vertegenwoordigt de naam van de container Hallo en `blob_name` vertegenwoordigt Hallo naam van uw blob, respectievelijk. Binnen de containernaam hello, kunt u meerdere paden, gescheiden door een slash hebben  **/** . Hallo voorbeeld containernaam in deze zelfstudie is **MyJob**, en **${bouwen\_ID} / ${bouwen\_getal}** is gebruikt voor Hallo algemene virtueel pad, wat resulteert in het Hallo-blob met een URL van de Hallo formulier te volgen:
  
    `http://example.blob.core.windows.net/myjob/2014-04-14_23-57-00/1/hello.txt`

## <a name="next-steps"></a>Volgende stappen
* [Voldoen aan Jenkins](https://wiki.jenkins-ci.org/display/JENKINS/Meet+Jenkins)
* [Azure-opslag-SDK voor Java](https://github.com/azure/azure-storage-java)
* [Azure Storage Client SDK-naslaginformatie](http://dl.windowsazure.com/storage/javadoc/)
* [REST-API voor Azure Storage-services](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog van het Azure Storage-team](http://blogs.msdn.com/b/windowsazurestorage/)

Voor meer informatie gaat u naar [Azure voor Java-ontwikkelaars](/java/azure).