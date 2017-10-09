---
title: Service Fabric-invoegtoepassing voor Eclipse aaaAzure | Microsoft Docs
description: Aan de slag met Hallo Service Fabric-invoegtoepassing voor Eclipse.
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2016
ms.author: saysa
ms.openlocfilehash: 4ba5a28a6282387249a2bd4e62314e891ff04162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a>Service Fabric-invoegtoepassing voor de ontwikkeling van Eclipse Java-toepassingen
Eclipse is een van de meest gebruikte Hallo ontwikkelomgevingen (IDE's) voor Java-ontwikkelaars geïntegreerd. In dit artikel wordt beschreven hoe tooset van uw Eclipse development environment toowork met Azure Service Fabric. Ontdek hoe tooinstall Hallo Service Fabric-invoegtoepassing, een Service Fabric-toepassing maken en implementeren van uw Service Fabric-toepassing tooa lokale of externe Service Fabric-cluster in Eclipse Neon.

## <a name="install-or-update-hello-service-fabric-plug-in-in-eclipse-neon"></a>Installeren of bijwerken van Service Fabric-invoegtoepassing in Eclipse Neon Hallo
U kunt een Service Fabric-invoegtoepassing in Eclipse installeren. Hallo invoegtoepassing vereenvoudigen Hallo-proces voor het maken en implementeren van Java-services.

1.  Zorg ervoor dat u de meest recente versie Hallo van Eclipse Neon en Hallo meest recente versie van Buildship (1.0.17 of een latere versie) geïnstalleerd:
    -   toocheck hello versies van geïnstalleerde onderdelen, in Eclipse Neon, gaat u te**Help** > **installatiegegevens**.
    -   tooupdate Buildship, Zie [Eclipse Buildship: Eclipse-invoegtoepassingen voor Gradle][buildship-update].
    -   Ga te toocheck voor en installeren van updates voor de Eclipse-Neon**Help** > **controleren op Updates**.

2.  tooinstall hello Service Fabric-invoegtoepassing in Eclipse Neon, gaat u te**Help** > **nieuwe Software installeren**.
  1.    In Hallo **werken met** Voer **http://dl.microsoft.com/eclipse**.
  2.    Klik op **Add**.

         ![De Service Fabric-invoegtoepassing voor Eclipse Neon][sf-eclipse-plugin-install]
  3.    Hallo Service Fabric-invoegtoepassing selecteren en klik vervolgens op **volgende**.
  4.    Hallo installatiestappen voltooien en accepteer de licentievoorwaarden voor Microsoft-Software Hallo.

Als u al Hallo Service Fabric-invoegtoepassing is geïnstalleerd, zorg ervoor dat hebt u Hallo meest recente versie. toocheck naar beschikbare updates te gaan**Help** > **installatiegegevens**. Selecteer Service Fabric in Hallo lijst met geïnstalleerde invoegtoepassingen, en klik vervolgens op **Update**. Beschikbare updates worden geïnstalleerd.

> [!NOTE]
> Als installeren of bijwerken van Service Fabric-invoegtoepassing Hallo traag is, mogelijk vanwege tooan Eclipse-instelling. Eclipse verzamelt metagegevens op alle wijzigingen tooupdate sites die zijn geregistreerd met uw Eclipse-exemplaar. toospeed Hallo-installatieproces van controleren en de installatie van een Service Fabric-invoegtoepassing update te gaan**beschikbare Software Sites**. Schakel de selectievakjes Hallo voor alle sites, met uitzondering van Hallo die toohello Service Fabric invoegtoepassing locatie (http://dl.microsoft.com/eclipse/azure/servicefabric wijst).

## <a name="create-a-service-fabric-application-in-eclipse"></a>Een Service Fabric-toepassing maken in Eclipse

1.  Ga te in Eclipse-Neon**bestand** > **nieuw** > **andere**. Selecteer **Fabric Service Project** en klik op **Next**.

    ![Nieuw Service Fabric-project pagina 1][create-application/p1]

2.  Voer een naam in voor het project en klik op **Next**.

    ![Nieuw Service Fabric-project pagina 2][create-application/p2]

3.  Selecteer in de lijst met sjablonen Hallo **servicesjabloon**. Selecteer het type servicesjabloon (Actor, Stateless, Container of Guest Binary) en klik op **Next**.

    ![Nieuw Service Fabric-project pagina 3][create-application/p3]

4.  Voer Hallo servicenaam en servicedetails en klik vervolgens op **voltooien**.

    ![Nieuw Service Fabric-project pagina 4][create-application/p4]

5. Wanneer u uw eerste Service Fabric-project maken in Hallo **openen die zijn gekoppeld perspectief** in het dialoogvenster klikt u op **Ja**.

    ![Nieuw Service Fabric-project pagina 5][create-application/p5]

6.  Het nieuwe project ziet er als volgt uit:

    ![Nieuw Service Fabric-project pagina 6][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a>Een Service Fabric-toepassing maken en implementeren in Eclipse

1.  Klik met de rechtermuisknop op de nieuwe Service Fabric-toepassing en selecteer **Service Fabric**.

    ![Snelmenu van Service Fabric][publish/RightClick]

2. Selecteer in vervolgmenu hello, Hallo-optie die u wilt:
    -   toobuild hello toepassing zonder reinigen, klikt u op **toepassing bouwen**.
    -   toodo leegmaken en opnieuw opbouwen van de toepassing hello, klikt u op **toepassing bouwen**.
    -   tooclean hello toepassing van ingebouwde artefacten, klikt u op **schone toepassing**.

3.  Vanuit dit menu kunt u de toepassing ook implementeren, de implementatie ervan verwijderen en de toepassing publiceren:
    -   toodeploy tooyour lokale cluster, klik op **toepassing implementeren**.
    -   In Hallo **toepassing publiceren** dialoogvenster Selecteer een publicatieprofiel:
        -  **Local.json**
        -  **Cloud.json**

     Deze notatie JSON (JavaScript Object)-bestanden opgeslagen informatie (zoals verbindingseindpunten en beveiligingsgegevens) die is vereist tooconnect tooyour lokale cloud (Azure)-cluster.

  ![Service Fabric-menu Publish][publish/Publish]

Een andere manier toodeploy Service Fabric-toepassing is via Eclipse uitvoeren configuraties.

  1.    Ga te**uitvoeren** > **configuratie uitvoeren**.
  2.    Onder **Project met Gradle**, selecteer Hallo **ServiceFabricDeployer** configuratie uitvoeren.
  3.    In het rechterdeelvenster Hallo op Hallo **argumenten** tabblad voor **publishProfile**, selecteer **lokale** of **cloud**.  Hallo standaardwaarde is **lokale**. toodeploy tooa externe of selecteer cloud cluster **cloud**.
  4.    tooensure dat de juiste informatie Hallo is ingevuld in Hallo profielen publiceren, bewerken **Local.json** of **Cloud.json** indien nodig. U kunt eindpuntdetails en beveiligingsreferenties toevoegen of bijwerken.
  5.    Zorg ervoor dat **werkmap** gewenste toodeploy toohello-toepassing verwijst. toochange toepassing hello, klikt u op Hallo **werkruimte** knop en selecteer vervolgens de gewenste Hallo-toepassing.
  6.    Klik op **Apply** en vervolgens op **Run**.

De toepassing is binnen enkele ogenblikken gemaakt en geïmplementeerd. U kunt de implementatiestatus Hallo in Service Fabric Explorer bewaken.  

## <a name="add-a-service-fabric-service-tooyour-service-fabric-application"></a>Een Service Fabric-service tooyour Service Fabric-toepassing toevoegen

een Service Fabric-service tooan bestaande Service Fabric-toepassing, tooadd Hallo volgende stappen:

1.  Met de rechtermuisknop op Hallo-project dat u wilt dat een service tooadd en klik vervolgens op **Service Fabric**.

    ![Service aan Service Fabric toevoegen pagina 1][add-service/p1]

2.  Klik op **Service Fabric-Service toevoegen**, en volledige Hallo set stappen tooadd een toohello serviceproject.
3.  Selecteer Hallo servicesjabloon u wilt tooadd tooyour project en klik vervolgens op **volgende**.

    ![Service aan Service Fabric toevoegen pagina 2][add-service/p2]

4.  Voer de naam van de service Hallo (en andere details, indien nodig) en klik vervolgens op Hallo **Service toevoegen** knop.  

    ![Service aan Service Fabric toevoegen pagina 3][add-service/p3]

5.  Nadat Hallo-service wordt toegevoegd, zoekt de projectstructuur van uw algehele vergelijkbare toohello project te volgen:

    ![Service aan Service Fabric toevoegen pagina 4][add-service/p4]

## <a name="edit-manifest-versions-of-your-service-fabric-java-application"></a>Manifestversies van uw Service Fabric Java-toepassing bewerken

tooedit manifest versies, klik met de rechtermuisknop op het Hallo-project, gaat u te**Service Fabric** en selecteer **Manifest versies bewerken...**  van Hallo vervolgmenu. In de wizard hello, kunt u manifest versies voor het manifest, servicemanifest toepassing hello en Hallo voor bijwerken **Code**, **Config** en **gegevens** pakketten.

Als u het selectievakje Hallo optie **automatisch bijwerken van toepassing en Serviceversies** en werk vervolgens een versie, Hallo manifest versies vervolgens automatisch bijgewerkt. toogive bijvoorbeeld u eerst Kies selectievakje Hallo Hallo updateversie van **Code** -versie uit 0.0.0 too0.0.1 en klik op **voltooien**, klikt u vervolgens service manifest versie en het toepassingsmanifest versie wordt automatisch bijgewerkt too0.0.1 zijn.

## <a name="upgrade-your-service-fabric-java-application"></a>Uw Service Fabric Java-toepassing upgraden

Voor een upgradescenario aannemen dat u hebt gemaakt Hallo **App1** project met behulp van Hallo Service Fabric-invoegtoepassing in Eclipse. Hebt geïmplementeerd met behulp van de invoegtoepassing toocreate Hallo een toepassing met de naam **fabric: / App1Application**. Hallo toepassingstype **App1AppicationType**, en versie van de toepassing hello 1.0 is. Nu u tooupgrade uw toepassing zonder de beschikbaarheid te onderbreken.

Controleer eerst eventuele wijzigingen tooyour toepassing en vervolgens opnieuw opbouwen Hallo service gewijzigd. Hallo update gewijzigd van service manifestbestand (ServiceManifest.xml) met de Hallo bijgewerkt versies voor het Hallo-service (en, Config of gegevens, zoals relevante). Ook wijzigen van de toepassing hello-manifest (ApplicationManifest.xml) met versienummer Hallo bijgewerkt voor de toepassing hello en Hallo gewijzigde service.  

tooupgrade uw toepassing met behulp van Eclipse Neon, kunt u een dubbele uitvoeren configuratieprofiel. Gebruik vervolgens tooupgrade uw toepassing naar behoefte.

1.  Ga te**uitvoeren** > **configuratie uitvoeren**. Klik in het linkerdeelvenster Hallo Hallo pijltje toohello links van **Project met Gradle**.
2.  Klik met de rechtermuisknop op **ServiceFabricDeployer** en selecteer **Duplicate**. Voer een nieuwe naam in voor deze configuratie, bijvoorbeeld **ServiceFabricUpgrader**.
3.  In het rechterpaneel Hallo op Hallo **argumenten** en wijzig **- Pconfig = 'implementeren'** te**- Pconfig = 'bijwerken'**, en klik vervolgens op **toepassen**.

Dit proces wordt gemaakt en opgeslagen configuratieprofiel uitvoeren u kunt gebruiken om uw toepassing op alle tooupgrade tijd. Ook krijgt Hallo meest recente bijgewerkte versie van het toepassingstype van manifestbestand van de toepassing hello.

upgrade van de toepassing Hello duurt een paar minuten. U kunt de upgrade van de toepassing hello in Service Fabric Explorer bewaken.

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a>Oude Service Fabric-Java-toepassingen toobe gebruikt met Maven migreren
We hebben onlangs Service Fabric-Java-bibliotheken verplaatst vanuit Service Fabric Java SDK tooMaven opslagplaats. Tijdens het Hallo nieuwe toepassingen die u met behulp van Eclipse genereren genereert de meest recente bijgewerkte projecten (die worden kunnen toowork met Maven), kunt u uw bestaande Service Fabric staatloze of actor Java-toepassingen, wat Hallo Service Fabric Java SDK gebruikten bijwerken eerdere versies, toouse Hallo Service Fabric Java afhankelijkheden van Maven. Stappen Hallo vermeld [hier](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure de oudere toepassing met Maven werkt.

<!-- Images -->

[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-eclipse/service-fabric-eclipse-plugin.png

[create-application/p1]:./media/service-fabric-get-started-eclipse/create-application/p1.png
[create-application/p2]:./media/service-fabric-get-started-eclipse/create-application/p2.png
[create-application/p3]:./media/service-fabric-get-started-eclipse/create-application/p3.png
[create-application/p4]:./media/service-fabric-get-started-eclipse/create-application/p4.png
[create-application/p5]:./media/service-fabric-get-started-eclipse/create-application/p5.png
[create-application/p6]:./media/service-fabric-get-started-eclipse/create-application/p6.png

[publish/Publish]: ./media/service-fabric-get-started-eclipse/publish/Publish.png
[publish/RightClick]: ./media/service-fabric-get-started-eclipse/publish/RightClick.png

[add-service/p1]: ./media/service-fabric-get-started-eclipse/add-service/p1.png
[add-service/p2]: ./media/service-fabric-get-started-eclipse/add-service/p2.png
[add-service/p3]: ./media/service-fabric-get-started-eclipse/add-service/p3.png
[add-service/p4]: ./media/service-fabric-get-started-eclipse/add-service/p4.png

<!-- Links -->
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
