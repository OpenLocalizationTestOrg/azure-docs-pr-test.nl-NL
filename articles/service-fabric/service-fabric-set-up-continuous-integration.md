---
title: aaaSet van continue integratie met Azure microservices | Microsoft Docs
description: Een overzicht van hoe tooset up continue integratie en implementatie voor een Service Fabric-toepassing met behulp van Visual Studio Team Services (VSTS).
services: service-fabric
documentationcenter: na
author: mthalman-msft
manager: timlt
editor: 
ms.assetid: 3e8c2290-9e7a-456a-9b2c-db44d1b3988d
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 12/06/2016
ms.author: mthalman;mikhegn
ms.openlocfilehash: 041e081f4a42f379394f2d21f07db4f6de045b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-service-fabric-continuous-integration-and-deployment-with-visual-studio-team-services"></a>Service Fabric continue integratie en implementatie met Visual Studio Team Services instellen
In dit artikel beschrijft Hallo stappen tooset up continue integratie en implementatie voor een Azure Service Fabric-toepassing met behulp van Visual Studio Team Services (VSTS).

Dit document weerspiegelt de huidige procedure Hallo en verwachte toochange is gedurende een bepaalde periode.

## <a name="prerequisites"></a>Vereisten
tooget gestart, als volgt te werk:

1. Zorg ervoor dat er toegang tooa Team Services-account of [maken van een](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services) zelf.
2. Zorg ervoor dat er toegang tooa Team Services teamproject of [maken van een](https://www.visualstudio.com/docs/setup-admin/create-team-project) zelf.
3. Zorg ervoor dat er een Service Fabric-cluster toowhich kunt u uw toepassing implementeren of een maken met behulp van Hallo [Azure-portal](service-fabric-cluster-creation-via-portal.md), een [Azure Resource Manager-sjabloon](service-fabric-cluster-creation-via-arm.md), of [Visual Studio ](service-fabric-cluster-creation-via-visual-studio.md).
4. Zorg ervoor dat u al een Service Fabric-toepassing (.sfproj)-project hebt gemaakt. U moet een project dat is gemaakt of bijgewerkt met de Service Fabric SDK 2.1 of hoger hebben (Hallo .sfproj bestand moet bevatten een waarde van de eigenschap ProjectVersion van 1.1 of hoger).

> [!NOTE]
> Aangepaste build agents zijn niet langer vereist. Teamservices gehost agents nu afkomstig zijn vooraf worden geïnstalleerd met de software voor beheer van Service Fabric-cluster, zodat voor de implementatie van uw toepassingen rechtstreeks vanuit de agents.
> 
> 

## <a name="configure-and-share-your-source-files"></a>Configureren en delen van de bronbestanden
Hallo eerste wat u wilt dat toodo is voor het voorbereiden van een publicatieprofiel voor gebruik door Hallo-implementatieproces die wordt uitgevoerd binnen Team Services.  Hallo publicatieprofiel moet geconfigureerde tootarget Hallo cluster die u eerder hebt voorbereid:

1. Kies een publicatieprofiel binnen uw toepassingsproject wilt u toouse voor uw werkstroom continue integratie. Ga als volgt Hallo [publiceren instructies](service-fabric-publish-app-remote-cluster.md) over het toopublish een externe toepassing tooa-cluster. Hoeft u niet daadwerkelijk toopublish uw toepassing al. U kunt klikken op Hallo **opslaan** hyperlink in Hallo dialoogvenster publiceren wanneer u op de juiste wijze dingen hebt geconfigureerd.
2. Als u wilt dat uw toepassing toobe bijgewerkt voor elke implementatie die in een Team Services, wilt u tooconfigure Hallo profiel tooenable upgrade publiceren. Zorg ervoor dat Hallo in Hallo dezelfde dialoogvenster gebruikt in stap 1 publiceren, **Upgrade Hallo toepassing** selectievakje is ingeschakeld.  Meer informatie over [extra upgrade-instellingen configureren](service-fabric-visualstudio-configure-upgrade.md). Klik op Hallo **opslaan** hyperlink toosave Hallo instellingen toohello publicatieprofiel.
3. Zorg ervoor dat u uw wijzigingen publiceren toohello profiel hebt opgeslagen en Hallo annuleren dialoogvenster publiceren.
4. Nu gaat u te[delen van de bronbestanden van uw toepassing project](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services#vs) met Team Services. Wanneer de bronbestanden toegankelijk in Team Services zijn, kunt u nu op de volgende stap voor het genereren van builds toohello verplaatsen. 

## <a name="create-a-build-definition"></a>Een build-definitie maken
De definitie van een Team Services build beschrijft een werkstroom die bestaat uit een reeks build stappen die sequentieel worden uitgevoerd. Hallo-doel van Hallo build definitie die u maakt is een Service Fabric-toepassingspakket tooproduce en andere artefacten die gebruikte toodeploy Hallo toepassing kunnen zijn. Meer informatie over Services Team [bouwen definities](https://www.visualstudio.com/docs/build/define/create).

### <a name="create-a-definition-from-hello-build-template"></a>Een definitie van Hallo build-sjabloon maken
1. Open uw teamproject in Visual Studio Team Services.
2. Selecteer Hallo **bouwen** tabblad.
3. Selecteer Hallo groen  **+**  toocreate de definitie van een nieuwe build te ondertekenen.
4. Selecteer in het dialoogvenster dat wordt geopend Hallo **Azure Service Fabric-toepassing** binnen Hallo **bouwen** sjablooncategorie.
5. Selecteer **volgende**.
6. Hallo-opslagplaats en de vertakking die zijn gekoppeld aan uw Service Fabric-toepassing selecteren.
7. Hallo agent wachtrij u toouse wilt selecteren. Gehoste agents worden ondersteund.
8. Selecteer **Maken**.
9. Hallo build definitie opslaan en geef een naam.
10. Hallo is volgende lid een beschrijving van de Hallo build stappen die worden gegenereerd door Hallo sjabloon:

| Stap bouwen | Beschrijving |
| --- | --- |
| NuGet terugzetten |Hallo NuGet-pakketten voor Hallo oplossing herstelt. |
| Oplossing bouwen \*.sln |Hallo volledige oplossing is gebaseerd. |
| Oplossing bouwen \*.sfproj |Hallo Service Fabric-toepassingspakket dat is gebruikt toodeploy Hallo toepassing genereert. Hallo toepassing pakketlocatie is opgegeven toobe binnen Hallo build van artefacten directory. |
| Bijwerken van Service Fabric-App-versies |Updates Hallo Versiewaarden in Hallo toepassingspakket manifestbestanden tooallow voor ondersteuning van upgrades. Zie Hallo [taak documentatiepagina](https://go.microsoft.com/fwlink/?LinkId=820529) voor meer informatie. |
| Bestanden kopiëren |Kopieën Hallo publiceren profiel en toepassing parameters bestanden toohello build van artefacten toobe verbruikt voor implementatie. |
| Publiceren van artefacten |Hallo build van artefacten publiceert. Kan de definitie van een release tooconsume Hallo build-artefacten. |

### <a name="verify-hello-default-set-of-tasks"></a>Controleer of de standaardset Hallo van taken
1. Controleren of Hallo **oplossing** invoerveld voor Hallo **NuGet terugzetten** en **oplossing bouwen** stappen bouwen.  Standaard deze build-stappen uitvoeren op alle oplossingsbestanden die zijn opgenomen in de opslagplaats Hallo die zijn gekoppeld.  Als u wilt dat alleen Hallo build definitie toooperate op een van deze oplossingsbestanden, moet u tooexplicitly Hallo pad toothat updatebestand.
2. Controleer of Hallo **oplossing** invoerveld voor Hallo **pakkettoepassing** stap bouwen.  Standaard deze build-stap wordt ervan uitgegaan dat slechts één Service Fabric-toepassing-project (.sfproj) bestaat in Hallo-opslagplaats.  Als u meerdere dergelijke bestanden in de opslagplaats en tootarget slechts één van deze voor deze definitie build wilt, moet u tooexplicitly Hallo pad toothat updatebestand.  Als u toopackage toepassing meerdere projecten in uw opslagplaats wilt, moet u toocreate extra **Visual Studio bouwen** stappen in de definitie van de build Hallo elk gericht op een project voor een toepassing.  Zou vervolgens moet u ook tooupdate hello **MSBuild-argumenten** veld voor elk van deze stappen bouwen zodat Hallo pakketlocatie is uniek voor elk van deze.
3. Hallo versioning gedrag is gedefinieerd in Hallo controleren **updateversies Service Fabric-App** stap bouwen.  Standaard wordt deze stap build toegevoegd Hallo build tooall versie getalwaarden in Hallo toepassingspakket manifest-bestanden. Zie Hallo [taak documentatiepagina](https://go.microsoft.com/fwlink/?LinkId=820529) voor meer informatie. Dit is handig voor het ondersteunen van upgrade van uw toepassing omdat elke upgrade-implementatie vereist een andere Versiewaarden uit de vorige implementatie Hallo. Als u geen upgrade van de toepassing toouse in de werkstroom wilde bent, kunt u overwegen deze build stap uitschakelen. Worden moet uitgeschakeld als het uw bedoeling is tooproduce een build waarvan gebruikte toooverwrite een bestaande Service Fabric-toepassing kan worden. Hallo implementatie mislukt als Hallo-versie van Hallo-toepassing die wordt geproduceerd door Hallo build komt niet overeen met de Hallo versie van de toepassing hello in Hallo-cluster.
4. Als uw oplossing een .NET Core-project bevat, moet u ervoor zorgen dat de definitie van de build bevat een build-stap die wordt hersteld Hallo afhankelijkheden:
   1. Selecteer **build-stap toevoegen...** .
   2. Zoek Hallo **opdrachtregelprogramma** taak binnen Hallo hulpprogramma tabblad en klik op de knop toevoegen.
   3. Gebruik voor invoervelden van Hallo taak, Hallo volgende waarden:
   4. Hulpprogramma: dotnet
   5. Argumenten: herstellen
   6. Sleep Hallo taak zodat deze onmiddellijk na Hallo **NuGet terugzetten** stap.
5. Sla de wijzigingen die hebt u toohello build definitie aangebracht.

### <a name="try-it"></a>Probeer het nu
Selecteer **wachtrij bouwen** toomanually start een build. Voortbouwt ook triggers op push of inchecken. Nadat u hebt geverifieerd dat Hallo build met succes wordt uitgevoerd, kunt u nu gaan toodefining de definitie van een versie die uw toepassing tooa cluster implementeert.

## <a name="create-a-release-definition"></a>Een release-definitie maken
De definitie van een Team Services release beschrijft een werkstroom die bestaat uit een aantal taken die sequentieel worden uitgevoerd. Hallo-doel van Hallo release definitie die u maakt is tootake een toepassingspakket en tooa-cluster implementeren. Wanneer samen worden gebruikt, Hallo definitie bouwen en release definitie Hallo volledige werkstroom kunt uitvoeren met bron bestanden tooending met een actieve toepassing in het cluster wordt gestart. Meer informatie over Services Team [definities release](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition).

### <a name="create-a-definition-from-hello-release-template"></a>Een definitie van Hallo releasesjabloon maken
1. Open het project in Visual Studio Team Services.
2. Selecteer Hallo **Release** tabblad.
3. Selecteer Hallo groen  **+**  toocreate de definitie van een nieuwe versie en selecteer **maken release definitie** in Hallo-menu.
4. Selecteer in het dialoogvenster dat wordt geopend Hallo **Azure Service Fabric-implementatie** binnen Hallo **implementatie** sjablooncategorie.
5. Selecteer **volgende**.
6. Hallo build definitie u toouse als Hallo bron van de definitie van deze release wilt selecteren.  Hallo release definitie verwijzingen Hallo artefacten die zijn gemaakt door Hallo geselecteerd bouwen definitie.
7. Controleer de Hallo **continue implementatie** selectievakje in als u wilt dat toohave Team Services automatisch een nieuwe release gemaakt en Hallo Service Fabric-toepassing implementeren wanneer een build is voltooid.
8. Hallo agent wachtrij u toouse wilt selecteren. Gehoste agents worden ondersteund.
9. Selecteer **Maken**.
10. Hallo Definitienaam door te klikken op Hallo potloodpictogram bovenaan Hallo Hallo pagina bewerken.
11. Selecteer Hallo cluster toowhich uw toepassing moet worden geïmplementeerd in Hallo **Cluster verbinding** invoerveld van Hallo-taak. Hallo cluster verbinding biedt Hallo benodigde informatie op waarmee Hallo implementatie taak tooconnect toohello cluster. Als u nog geen cluster-verbinding voor uw cluster, selecteert u Hallo **beheren** hyperlink volgende toohello veld tooadd een. Op Hallo pagina die wordt geopend, voert u Hallo stappen te volgen:
    1. Selecteer **nieuwe Service-eindpunt** en selecteer vervolgens **Azure Service Fabric** in Hallo-menu.
    2. Selecteer Hallo type verificatie wordt gebruikt door Hallo cluster gericht door dit eindpunt.
    3. Definieer een naam voor de verbinding in Hallo **verbindingsnaam** veld.  Normaal gesproken gebruikt u Hallo-naam van het cluster.
    4. Hallo-client verbinding eindpunt-URL opgeven in Hallo **Clustereindpunt** veld.  Voorbeeld: tcp://contoso.westus.cloudapp.azure.com:19000.
    5. Voor Azure Active Directory-referenties, definiëren Hallo referenties gewenste toouse tooconnect toohello cluster in Hallo **gebruikersnaam** en **wachtwoord** velden.
    6. Voor verificatie op basis van certificaten definiëren Hallo Base64-codering Hallo certificaatbestand in Hallo **clientcertificaat** veld.  Hallo help pop-up bekijken op het veld voor informatie over het tooget die waarde.  Als uw certificaat beveiligd met een wachtwoord is, hello wachtwoord definiëren in Hallo **wachtwoord** veld.
    7. Controleer uw wijzigingen door te klikken op **OK**. Na de back-tooyour navigeren definitie release, klikt u op Hallo pictogram op Hallo **Cluster verbinding** veld toosee Hallo eindpunt u zojuist hebt toegevoegd.
12. Hallo release definitie opslaan.

> [!NOTE]
> Microsoft-Accounts (bijvoorbeeld @hotmail.com of @outlook.com) worden niet ondersteund met Azure Active Directory-verificatie.
> 
> 

Hallo-definitie die is gemaakt, bestaat uit één taak van het type **Service Fabric-toepassingsimplementatie**. Zie Hallo [taak documentatiepagina](https://go.microsoft.com/fwlink/?LinkId=820528) voor meer informatie over deze taak.

### <a name="verify-hello-template-defaults"></a>Controleer of de standaardinstellingen van de sjabloon Hallo
1. Controleer of Hallo **publiceren profiel** invoerveld voor Hallo **Service Fabric-toepassing implementeren** taak. Standaard is dit veld verwijst naar een publicatieprofiel met de naam Cloud.xml opgenomen in Hallo build van artefacten. Als u wilt dat een andere publicatieprofiel tooreference of Hallo build meerdere toepassingspakketten in de artefacten bevat, moet u tooupdate Hallo pad op de juiste wijze.
2. Controleer of Hallo **toepassingspakket** invoerveld voor Hallo **Service Fabric-toepassing implementeren** taak. Standaard is dit veld verwijst naar Hallo standaard pakket toepassingspad in Hallo build definitie sjabloon gebruikt.  Als u de toepassing hello-pakket standaardpad hebt gewijzigd in Hallo bouwen definition, moet u tooupdate Hallo pad op de juiste wijze hier ook.

### <a name="try-it"></a>Probeer het nu
Selecteer **maken Release** van Hallo **Release** knop menu toomanually een release gemaakt. Selecteer in het dialoogvenster dat wordt geopend Hallo Hallo-build die u wilt toobase Hallo release op en klik vervolgens op **maken**. Als u continue implementatie hebt ingeschakeld, wordt releases automatisch gemaakt wanneer Hallo gekoppeld build definitie een build is voltooid.

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over de continue integratie met Service Fabric-toepassingen en lezen Hallo artikelen te volgen:

* [Thuis Team Services-documentatie](https://www.visualstudio.com/docs/overview)
* [Beheer in Team Services bouwen](https://www.visualstudio.com/docs/build/overview)
* [Releasebeheer in Team Services](https://www.visualstudio.com/docs/release/overview)

