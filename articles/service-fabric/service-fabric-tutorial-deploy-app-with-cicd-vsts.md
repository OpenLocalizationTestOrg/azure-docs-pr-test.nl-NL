---
title: aaaDeploy een Azure Service Fabric-toepassing met continue integratie (Team Services) | Microsoft Docs
description: Meer informatie over hoe tooset up continue integratie en implementatie voor een Service Fabric-toepassing met behulp van Visual Studio Team Services.  Een toepassing tooa Service Fabric-cluster in Azure implementeren.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi
ms.openlocfilehash: ba9a632b247b0f467e7b66fbe77b4ad54fb3d9ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-with-cicd-tooa-service-fabric-cluster"></a>Implementeer een toepassing met CI/CD tooa Service Fabric-cluster
Deze zelfstudie maakt deel uit drie van een reeks en wordt beschreven hoe tooset up continue integratie en implementatie voor een Azure Service Fabric-toepassing met behulp van Visual Studio Team Services.  Een bestaande Service Fabric-toepassing nodig is, de toepassing hello gemaakt in [een .NET-toepassing bouwen](service-fabric-tutorial-create-dotnet-app.md) wordt gebruikt als een voorbeeld.

In het onderdeel drie van Hallo-serie, leert u hoe:

> [!div class="checklist"]
> * Source control tooyour project toevoegen
> * Een build-definitie maken in een Team Services
> * De definitie van een release in Team Services maken
> * Automatisch implementeren en bijwerken van een toepassing

In deze zelfstudie reeks leert u hoe:
> [!div class="checklist"]
> * [Een .NET-Service Fabric-toepassing bouwen](service-fabric-tutorial-create-dotnet-app.md)
> * [Hallo toepassing tooa RAS-cluster implementeren](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * CI/CD met behulp van Visual Studio Team Services configureren

## <a name="prerequisites"></a>Vereisten
Voordat u deze zelfstudie begint:
- Als u geen Azure-abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- [Installeer Visual Studio 2017](https://www.visualstudio.com/) en installeer Hallo **ontwikkelen van Azure** en **ASP.NET en web ontwikkeling** werkbelastingen.
- [Hallo Service Fabric SDK installeren](service-fabric-get-started.md)
- Maak een Service Fabric-toepassing, bijvoorbeeld door [deze zelfstudie](service-fabric-tutorial-create-dotnet-app.md). 
- Maak een Windows-Service Fabric-cluster in Azure, bijvoorbeeld door [deze zelfstudie](service-fabric-tutorial-create-cluster-azure-ps.md)
- Maak een [Team Services-account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).

## <a name="download-hello-voting-sample-application"></a>Hallo Voting voorbeeldtoepassing downloaden
Als u geen Hallo Voting voorbeeldtoepassing heeft bouwen [deel uitmaken van een van deze zelfstudie reeks](service-fabric-tutorial-create-dotnet-app.md), u kunt dit downloaden. In een opdrachtvenster Hallo na de opdracht tooclone Hallo voorbeeld-app-opslagplaats tooyour lokale computer worden uitgevoerd.

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="prepare-a-publish-profile"></a>Een publicatieprofiel voorbereiden
Nu dat u hebt [gemaakt van een toepassing](service-fabric-tutorial-create-dotnet-app.md) en [geïmplementeerd Hallo toepassing tooAzure](service-fabric-tutorial-deploy-app-to-party-cluster.md), bent u klaar tooset van continue integratie.  Bereid eerst een publicatieprofiel in uw toepassing voor gebruik door Hallo-implementatieproces die wordt uitgevoerd binnen Team Services.  Hallo publicatieprofiel moet geconfigureerde tootarget Hallo cluster dat u eerder hebt gemaakt.  Visual Studio starten en opent u een bestaand project van de Service Fabric-toepassing.  In **Solution Explorer**, met de rechtermuisknop op het Hallo-toepassing en selecteer **publiceren...** .

Een profiel van de doelcomputer in uw toepassing project toouse voor uw werkstroom continue integratie kiezen, bijvoorbeeld Cloud.  Geef verbindingseindpunt Hallo-cluster.  Controleer Hallo **Upgrade Hallo toepassing** selectievakje in zodat uw toepassing upgrades voor elke implementatie in een Team Services.  Klik op Hallo **opslaan** hyperlink toosave Hallo instellingen toohello publicatieprofiel en klik vervolgens op **annuleren** tooclose Hallo dialoogvenster.  

![Push-profiel][publish-app-profile]

## <a name="share-your-visual-studio-solution-tooa-new-team-services-git-repo"></a>Delen van uw Visual Studio-oplossing tooa nieuw Team Services Git-opslagplaats
De bronbestanden van uw toepassing tooa teamproject in Team Services zodat u kunt genereren builds delen.  

Een nieuwe lokale Git-opslagplaats voor uw project maken door te selecteren **tooSource besturingselement toevoegen** -> **Git** op de statusbalk Hallo in Hallo rechterbenedenhoek van Visual Studio. 

In Hallo **Push** weergeven in **Team Explorer**, selecteer Hallo **Git-opslagplaats publiceren** knop onder **tooVisual Studio Team Services Push**.

![Push Git-opslagplaats][push-git-repo]

Controleer of uw e-mailadres in en selecteer uw account Hallo **Team Services domein** vervolgkeuzelijst. Voer de naam van uw opslagplaats en selecteer **publiceren opslagplaats**.

![Push Git-opslagplaats][publish-code]

Hallo opslagplaats publiceren, maakt een nieuw teamproject in uw account met dezelfde naam als lokale opslagplaats Hallo Hallo. toocreate Hallo-opslagplaats in een bestaande teamproject, klikt u op **Geavanceerd** volgende te**opslagplaats** naam en selecteer een teamproject. U kunt uw code op Hallo web weergeven door **zien op Hallo web**.

## <a name="configure-continuous-delivery-with-vsts"></a>Continue levering met VSTS configureren
De definitie van een Team Services build beschrijft een werkstroom die bestaat uit een reeks build stappen die sequentieel worden uitgevoerd. Een build-definitie maken die die een Service Fabric-toepassingspakket en andere artefacten, toodeploy tooa Service Fabric-cluster produceert. Meer informatie over [Team Services bouwen definities](https://www.visualstudio.com/docs/build/define/create). 

De definitie van een Team Services release beschrijft een werkstroom die een toepassing pakket tooa cluster implementeert. Wanneer samen worden gebruikt, Hallo definitie bouwen en release definitie uitvoeren Hallo van de volledige werkstroom beginnen met bron bestanden tooending met een actieve toepassing in uw cluster. Meer informatie over Services Team [definities release](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition).

### <a name="create-a-build-definition"></a>Een build-definitie maken
Open een webbrowser en navigeer tooyour nieuw teamproject op: https://myaccount.visualstudio.com/Voting/Voting%20Team/_git/Voting. 

Selecteer Hallo **bouwen & Release** tabblad vervolgens **Builds**, klikt u vervolgens **+ nieuwe definitie**.  In **Selecteer een sjabloon**, selecteer Hallo **Azure Service Fabric-toepassing** sjabloon en klikt u op **toepassen**. 

![Kies build-sjabloon][select-build-template] 

Hallo stemmen toepassing bevat een project .NET Core, dus een taak die wordt hersteld Hallo afhankelijkheden toevoegen. In Hallo **taken** weergave, selecteer **+ taak toevoegen** in Hallo linksonder. Zoeken op 'Opdrachtregel' toofind hello opdrachtregeltaak en klik vervolgens op **toevoegen**. 

![Taak toevoegen][add-task] 

Voer in de nieuwe taak Hallo 'Dotnet.exe uitvoeren' in **weergavenaam**, 'dotnet.exe' in **hulpprogramma**, en "herstellen" in **argumenten**. 

![Nieuwe taak][new-task] 

In Hallo **Triggers** weergeven, klikt u op Hallo **inschakelen van deze trigger** overschakelen onder **continue integratie**. 

Selecteer **opslaan en wachtrij** en voer 'VS2017 gehost' als Hallo **Agent wachtrij**. Selecteer **wachtrij** toomanually start een build.  Voortbouwt ook triggers op push of inchecken.

toocheck uw voortgang build, switch toohello **Builds** tabblad.  Zodra u hebt gecontroleerd dat Hallo build met succes wordt uitgevoerd, definieert u de definitie van een versie die uw toepassing tooa cluster implementeert. 

### <a name="create-a-release-definition"></a>Een release-definitie maken  

Selecteer Hallo **bouwen & Release** tabblad vervolgens **Releases**, klikt u vervolgens **+ nieuwe definitie**.  In **maken release definitie**, selecteer Hallo **Azure Service Fabric-implementatie** sjabloon van Hallo lijst en klikt u op **volgende**.  Selecteer Hallo **bouwen** bron, controleert u Hallo **continue implementatie** vak en klikt u op **maken**. 

In Hallo **omgevingen** weergeven, klikt u op **toevoegen** toohello rechts van **Cluster verbinding**.  Geef de verbindingsnaam van een van 'mysftestcluster', een clustereindpunt van 'tcp://mysftestcluster.westus.cloudapp.azure.com:19000' en hello Azure Active Directory of referenties van het computercertificaat voor Hallo-cluster. Voor Azure Active Directory-referenties, definiëren Hallo referenties gewenste toouse tooconnect toohello cluster in Hallo **gebruikersnaam** en **wachtwoord** velden. Voor verificatie op basis van certificaten definiëren Hallo Base64-codering Hallo certificaatbestand in Hallo **clientcertificaat** veld.  Hallo help pop-up bekijken op het veld voor informatie over het tooget die waarde.  Als uw certificaat beveiligd met een wachtwoord is, hello wachtwoord definiëren in Hallo **wachtwoord** veld.  Klik op **opslaan** toosave Hallo release definitie.

![Cluster-verbinding toevoegen][add-cluster-connection] 

Klik op **uitvoeren op de agent**, selecteer daarna **VS2017 gehost** voor **implementatie wachtrij**. Klik op **opslaan** toosave Hallo release definitie.

![Voer op de agent][run-on-agent]

Selecteer **+ Release** -> **maken Release** -> **maken** toomanually een release gemaakt.  Controleer of Hallo-implementatie is voltooid en Hallo toepassing wordt uitgevoerd in Hallo-cluster.  Open een webbrowser en navigeer te[http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).  Houd er rekening mee Hallo toepassingsversie, in dit voorbeeld is '1.0.0.20170616.3'. 

## <a name="commit-and-push-changes-trigger-a-release"></a>Doorvoeren en wijzigingen forceren, een release activeren
tooverify die continue integratie pijplijn Hallo werkt door te controleren in een aantal codewijzigingen tooTeam Services.    

Als u uw code schrijft, worden uw wijzigingen automatisch bijgehouden door Visual Studio. Het doorvoeren van wijzigingen tooyour lokale Git-opslagplaats door Hallo in behandeling zijnde wijzigingen pictogram (selecteren![In behandeling][pending]) van de statusbalk Hallo in Hallo rechtsonder.

Op Hallo **wijzigingen** weergeven in Verkenner-Team, een bericht met een beschrijving van de update toevoegen en uw wijzigingen.

![Alle doorvoeren][changes]

Selecteer Hallo niet-gepubliceerde wijzigingen statuspictogram balk (![niet-gepubliceerde wijzigingen][unpublished-changes]) of Hallo Sync weergave in de Explorer-Team. Selecteer **Push** tooupdate uw code in Services/TFS Team.

![Wijzigingen][push]

Hallo wijzigingen tooTeam pushen Services automatisch triggers een build.  Wanneer Hallo build definitie is voltooid, wordt een versie wordt automatisch gemaakt en begint met het upgraden van de toepassing hello op Hallo-cluster.

toocheck uw voortgang build, switch toohello **Builds** tabblad **Team Explorer** in Visual Studio.  Zodra u hebt gecontroleerd dat Hallo build met succes wordt uitgevoerd, definieert u de definitie van een versie die uw toepassing tooa cluster implementeert.

Controleer of Hallo-implementatie is voltooid en Hallo toepassing wordt uitgevoerd in Hallo-cluster.  Open een webbrowser en navigeer te[http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).  Houd er rekening mee Hallo toepassingsversie, in dit voorbeeld is '1.0.0.20170815.3'.

![Service Fabric Explorer][sfx1]

## <a name="update-hello-application"></a>Hallo toepassing bijwerken
Codewijzigingen aanbrengen in de toepassing hello.  Opslaan en wijzigingen hello, Hallo vorige stappen te volgen.

Zodra het Hallo-upgrade van Hallo toepassing wordt gestart, kunt u de voortgang van Hallo upgrade in Service Fabric Explorer bekijken:

![Service Fabric Explorer][sfx2]

upgrade van de toepassing Hello kan enkele minuten duren. Wanneer het Hallo-upgrade is voltooid, wordt Hallo toepassing hello volgende versie worden uitgevoerd.  In dit voorbeeld '1.0.0.20170815.4'.

![Service Fabric Explorer][sfx3]

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie heeft u het volgende geleerd:

> [!div class="checklist"]
> * Source control tooyour project toevoegen
> * Een build-definitie maken
> * Een release-definitie maken
> * Automatisch implementeren en bijwerken van een toepassing

Nu dat u hebt een toepassing is geïmplementeerd en geconfigureerd continue integratie, voer een van de volgende Hallo:
- [Een app bijwerken](service-fabric-application-upgrade.md)
- [Een app testen](service-fabric-testability-overview.md) 
- [Controle en diagnose](service-fabric-diagnostics-overview.md)


<!-- Image References -->
[publish-app-profile]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishAppProfile.png
[push-git-repo]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishGitRepo.png
[publish-code]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishCode.png
[select-build-template]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SelectBuildTemplate.png
[add-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddTask.png
[new-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewTask.png
[set-continuous-integration]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SetContinuousIntegration.png
[add-cluster-connection]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddClusterConnection.png
[sfx1]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX1.png
[sfx2]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX2.png
[sfx3]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX3.png
[pending]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Pending.png
[changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Changes.png
[unpublished-changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/UnpublishedChanges.png
[push]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Push.png
[continuous-delivery-with-VSTS]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/VSTS-Dialog.png
[new-service-endpoint]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpoint.png
[new-service-endpoint-dialog]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpointDialog.png
[run-on-agent]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/RunOnAgent.png