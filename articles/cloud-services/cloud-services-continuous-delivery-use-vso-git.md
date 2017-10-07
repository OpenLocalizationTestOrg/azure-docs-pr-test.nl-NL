---
title: aaaContinuous levering met Git en Visual Studio Team Services in Azure | Microsoft Docs
description: Meer informatie over hoe tooconfigure uw Visual Studio Team Services team projecten toouse Git tooautomatically bouwen en implementeren van de functie van de toohello Web-App in Azure App Service- of cloud-services.
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 4b3297ef-0de6-4d5f-925c-fcdacc3085ac
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: 936c42194f45be55597a77f9a3a6deb4480ed94b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services-and-git"></a>Continue levering tooAzure met behulp van Visual Studio Team Services en Git
U kunt Visual Studio Team Services team projecten toohost een Git-opslagplaats gebruiken voor de broncode en automatisch bouwen en tooAzure web-apps implementeren of cloudservices wanneer u een commit toohello opslagplaats pushen.

U moet Visual Studio 2013 en hello Azure SDK is geïnstalleerd. Als u nog geen Visual Studio 2013 hebt, downloadt u dit door te kiezen Hallo **gratis aan de slag** koppeling [www.visualstudio.com](http://www.visualstudio.com). Installeren Azure SDK Hallo [hier](http://go.microsoft.com/fwlink/?LinkId=239540).

> [!NOTE]
> U moet een toocomplete Visual Studio Team Services-account van deze zelfstudie: U kunt [gratis een Visual Studio Team Services-account openen](http://go.microsoft.com/fwlink/p/?LinkId=512979).
> 
> 

tooset van een cloud service tooautomatically bouwen en tooAzure implementeren met behulp van Visual Studio Team Services, als volgt te werk.

## <a name="1-create-a-git-repository"></a>1: een Git-opslagplaats maken
1. Als u nog een Visual Studio Team Services-account hebt, kunt u een [hier](http://go.microsoft.com/fwlink/?LinkId=397665). Wanneer u uw teamproject maakt, kiest u Git als uw bronbeheersysteem. Ga als volgt Hallo instructies tooconnect Visual Studio tooyour teamproject.
2. In **Team Explorer**, kies Hallo **deze opslagplaats klonen** koppeling.
   
    ![][3]
3. Locatie van de lokale kopie Hallo Hallo opgeven en kies vervolgens Hallo **kloon** knop.

## <a name="2-create-a-project-and-commit-it-toohello-repository"></a>2: een project maken en deze opslagplaats toohello doorvoeren
1. In **Team Explorer**, in Hallo **oplossingen** sectie, kiest u Hallo **nieuw** toocreate een nieuw project in de lokale opslagplaats Hallo koppelen.
   
    ![][4]
2. U kunt een web-app implementeren of een service in de cloud (Azure-toepassing) door de volgende Hallo stappen in dit scenario. Maak een nieuw Azure Cloud Service-project of een nieuw ASP.NET MVC-project. Controleer of dat Hallo project doelen Hallo .NET Framework 4 of hoger. Als u een cloudserviceproject maakt, een ASP.NET MVC-Webrol en een werkrol toevoegen.
   Als u een web-app toocreate wilt, kunt u Hallo **ASP.NET-webtoepassing** sjabloon project en kies vervolgens **MVC**. Zie [een ASP.NET-web-app maken in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) voor meer informatie.
3. Open Hallo snelmenu voor Hallo oplossing en kies **doorvoeren**.
   
    ![][7]
4. Als dit Hallo eerst die u Git in Visual Studio Team Services hebt gebruikt, moet u tooprovide sommige tooidentify informatie zelf in Git. In Hallo **wijzigingen in behandeling** gebied van **Team Explorer**, Voer uw gebruikersnaam en e-mailadres. Voer een opmerking voor Hallo doorvoeren en kies vervolgens Hallo **doorvoeren** knop.
   
    ![][8]
5. Houd er rekening mee Hallo opties tooinclude of specifieke wijzigingen uitsluiten wanneer u incheckt. Als Hallo wijzigingen u wilt worden uitgesloten, kiest u **omvatten alle**.
6. U hebt nu doorgevoerd Hallo in de lokale kopie van het Hallo-opslagplaats wijzigingen. Vervolgens deze wijzigingen met Hallo-server te synchroniseren door te kiezen Hallo **Sync** koppeling.

## <a name="3-connect-hello-project-tooazure"></a>3: verbinding maken met de Hallo project tooAzure
1. Nu dat u een Git-opslagplaats in Visual Studio Team Services met sommige broncode erin hebt, bent u klaar tooconnect uw tooAzure git-opslagplaats.  In Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885), selecteer uw cloud-service of web-app of een nieuwe maken door te kiezen Hallo + pictogram op Hallo linksonder en kiezen **Cloudservice** of **Web-App**en vervolgens **snelle invoer**.
   
    ![][9]
2. Kies voor cloudservices, Hallo **publiceren met Visual Studio Team Services instellen** koppeling. Kies voor web-apps, Hallo **implementatie vanuit resourcebeheer instellen** koppeling.
   
    ![][10]
3. In de wizard Hallo typenaam Hallo van uw Visual Studio Team Services-account in Hallo tekstvak en kies Hallo **autoriseren nu** koppeling. U wordt mogelijk gevraagd toosign in.
   
    ![][11]
4. In Hallo **verbindingsaanvraag** pop-upvenster kiezen **accepteren** tooauthorize Azure tooconfigure uw team in Visual Studio Team Services project.
   
    ![][12]
5. Nadat de autorisatie is geslaagd, ziet u een vervolgkeuzelijst met uw teamprojecten Visual Studio Team Services.  Selecteer de naam Hallo van teamproject dat u hebt gemaakt in de vorige stappen Hallo en kies van de wizard Hallo vinkje knop.
   
    ![][13]
   
    Hallo volgende keer dat u Visual Studio Team Services van een commit tooyour opslagplaats pushen bouwt en implementeren van uw project tooAzure.

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4: de tabel opnieuw activeren en implementeren van uw project
1. In Visual Studio, opent u een bestand en deze te wijzigen. Wijzig bijvoorbeeld Hallo bestand `_Layout.cshtml` onder Hallo weergaven\\gedeelde map in een MVC-Webrol.
   
    ![][17]
2. Hallo voettekst voor Hallo site bewerken en sla Hallo-bestand.
   
    ![][18]
3. In **Solution Explorer**, open de Hallo snelmenu voor hello oplossing knooppunt, projectknooppunt of Hallo bestand dat u gewijzigd en kies vervolgens **doorvoeren**.
4. Typ in een opmerking en kies **doorvoeren**.
   
    ![][20]
5. Kies Hallo **Sync** koppeling.
   
    ![][38]
6. Kies Hallo **Push** koppelen toopush uw opslagplaats doorvoeren toohello in Visual Studio Team Services. (U kunt ook Hallo **Sync** knop toocopy uw doorvoeracties toohello-opslagplaats. Hallo verschil is dat **Sync** ook worden de meest recente wijzigingen in de opslagplaats voor Hallo Hallo.)
   
    ![][39]
7. Kies Hallo **thuis** knop tooreturn toohello **Team Explorer** startpagina.
   
    ![][21]
8. Kies **Builds** tooview hello-bouwt uitgevoerd.
   
    ![][22]
   
    **In een team Explorer** ziet u dat een build voor uw inchecken is geactiveerd.
   
    ![][23]
9. tooview een gedetailleerd logboek terwijl Hallo maakt de voortgang van Dubbelklik op Hallo van Hallo build uitgevoerd.
10. Hallo build is uitgevoerd, bekijk Hallo build definitie die is gemaakt toen u Hallo wizard toolink tooAzure gebruikt.  Hallo snelmenu voor Hallo build definitie openen en kies **bouwen definitie bewerken**.
    
    ![][25]
11. In Hallo **Trigger** tabblad ziet u dat Hallo build definitie toobuild is ingesteld op elke inchecken standaard. (Voor een cloudservice Visual Studio Team Services maakt en implementeert Hallo hoofdvertakking toohello automatisch staging-omgeving. U hebt nog toodo een handmatige stap toodeploy toohello live site. Voor een web-app dat geen staging-omgeving, wordt het Hallo hoofdvertakking direct toohello live site geïmplementeerd.
    
    ![][26]
12. In Hallo **proces** tabblad ziet u de implementatieomgeving Hallo toohello naam van uw cloud-service of web-app is ingesteld.
    
     ![][27]
13. Geef waarden voor Hallo eigenschappen als u wilt dat andere waarden dan Hallo standaardwaarden. Hallo-eigenschappen voor Azure publicatie worden in Hallo **implementatie** sectie en kunt u wellicht ook tooset MSBuild-parameters. Bijvoorbeeld in een cloud service-project toospecify een serviceconfiguratie dan 'Cloud' hello MSbuild parameters instellen te`/p:TargetProfile=[YourProfile]` waar *[YourProfile]* overeenkomt met een configuratiebestand voor de service met een naam zoals Serviceconfiguration zijn. *YourProfile*cscfg-bestand.
    
     Hallo volgende tabel bevat de beschikbare eigenschappen Hallo in Hallo **implementatie** sectie:
    
    | Eigenschap | Standaardwaarde |
    | --- | --- |
    | Niet-vertrouwde certificaten toestaan |Als het ONWAAR is, moeten de SSL-certificaten zijn ondertekend door een basisinstantie. |
    | Upgrade toestaan |Hiermee kunt Hallo implementatie tooupdate een bestaande implementatie in plaats van een nieuwe maken. Bewaart Hallo IP-adres. |
    | Niet verwijderen |Indien waar, de implementatie van een bestaande niet-verwante niet overschrijven (upgrade is toegestaan). |
    | Pad tooDeployment instellingen |Hallo pad tooyour .pubxml bestand voor een web-app relatieve toohello-hoofdmap van het Hallo-opslagplaats. Genegeerd voor cloud-services. |
    | SharePoint-omgeving voor implementatie |dezelfde als de servicenaam Hallo Hallo. |
    | Azure-implementatie-omgeving |Hallo-app of cloud naam van de webservice. |
14. Op dit tijdstip moet uw build worden voltooid.
    
     ![][28]
15. Als u dubbelklikt op de naam van de build hello, ziet u Visual Studio een **bouwen samenvatting**, met inbegrip van de testresultaten van eenheid Testprojecten die is gekoppeld.
    
     ![][29]
16. In Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885), kunt u Hallo gekoppeld implementatie bekijken op Hallo **implementaties** tabblad wanneer Hallo staging-omgeving is geselecteerd.
    
     ![][30]
17. De URL van de site tooyour bladeren. Kies voor een web-app Hallo **Bladeren** knop in Hallo-portal. Kies voor een cloudservice Hallo URL uit Hallo **snel in één oogopslag** sectie Hallo **Dashboard** pagina waarin de faseringsomgeving Hallo.
    
    Implementaties van continue integratie voor cloud-services worden gepubliceerde toohello faseringsomgeving standaard. U kunt dit wijzigen door de instelling Hallo **alternatieve Cloudserviceomgeving** eigenschap te**productie**. Hier is waarbij Hallo site-URL op de dashboardpagina Hallo cloudservice.
    
    ![][31]
    
    Een nieuw browsertabblad geopend tooreveal uw site uitgevoerd.
    
    ![][32]
18. Als u andere wijzigingen tooyour project, u trigger builds meer en wordt u meerdere implementaties verzamelt. Hallo laatste één is gemarkeerd als actief.
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5: een eerdere build implementeren
Deze stap is optioneel. In klassieke Azure-portal hello, kies een eerdere implementatie en **implementeren** toorewind uw site tooan eerder incheckt. Houd er rekening mee dat dit een nieuwe build in TFS activeren en maken van een nieuwe vermelding in de geschiedenis van uw implementatie.

![][34]

## <a name="6-change-hello-production-deployment"></a>6: Hallo productie-implementatie wijzigen
Wanneer u klaar bent, kunt u Hallo fasering toohello productieomgeving promoveren kiezen **wisselen** in Hallo klassieke Azure-portal. faseringsomgeving Hallo zojuist geïmplementeerde is gepromoveerde tooProduction en Hallo vorige productie-omgeving, indien aanwezig, wordt een Staging-omgeving. Hallo actieve implementatie mogelijk anders voor hello productie- en faseringsomgevingen, maar de implementatiegeschiedenis Hallo van recente builds is Hallo dezelfde omgeving ongeacht.

![][35]

## <a name="7-deploy-from-a-working-branch"></a>7: implementeren vanuit een werkvertakking.
Wanneer u met Git, meestal wijzigingen aanbrengt in een werkvertakking en integreren in de hoofdvertakking Hallo wanneer de ontwikkeling van een voltooide status bereikt. Tijdens de ontwikkelingsfase Hallo van een project, u wilt toobuild en Hallo werkende vertakking tooAzure implementeren.

1. In **Team Explorer**, kies Hallo **Start** knop en kies vervolgens Hallo **vertakkingen** knop.
   
    ![][40]
2. Kies Hallo **nieuwe vertakking** koppeling.
   
    ![][41]
3. Geef de naam Hallo van Hallo vertakking, zoals 'werken', en kies **vertakking maken**. Hiermee maakt u een nieuwe lokale vertakking.
   
    ![][42]
4. Hallo vertakking publiceren. Kies Hallo vertakking naam in **niet gepubliceerd vertakkingen**, en kies **publiceren**.
   
    ![][44]
5. Standaard verandert alleen toohello hoofdvertakking trigger een continue build. tooset up continue build voor een werkvertakking, kies Hallo **Builds** pagina in **Team Explorer**, en kies **bouwen definitie bewerken**.
6. Open Hallo **broninstellingen** tabblad. Onder **bewaakt vertakkingen voor continue integratie en build**, kies **Klik hier tooadd een nieuwe rij**.
   
    ![][47]
7. Hallo vertakking die u hebt gemaakt, zoals koppen refs werkende opgeven.
   
    ![][48]
8. Een wijziging aanbrengt in Hallo code, open Hallo snelmenu voor het bestand Hallo gewijzigd, en kies vervolgens **doorvoeren**.
   
    ![][43]
9. Kies Hallo **niet-gesynchroniseerde doorvoeracties** koppeling en kies Hallo **synchronisatie** knop of Hallo **Push** koppeling toocopy Hallo wijzigingen toohello kopie van de werkvertakking Hallo in Visual Studio Teamservices.
   
   ![][45]
10. Navigeer toohello **Builds** weergeven en Hallo-build die zojuist is geactiveerd voor Hallo werkvertakking niet vinden.

## <a name="next-steps"></a>Volgende stappen
toolearn meer tips over het gebruik van Git met Visual Studio Team Services, Zie [ontwikkelen en delen van uw code in Git met Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) en voor informatie over het gebruik van een Git-opslagplaats die niet wordt beheerd door Visual Studio Team Services toopublish tooAzure, Zie [continue implementatie tooAzure App Service](../app-service-web/app-service-continuous-deployment.md). Zie voor meer informatie over Visual Studio Team Services [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateTeamProjectInGit.PNG
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png
[3]: ./media/cloud-services-continuous-delivery-use-vso-git/CloneThisRepository.PNG
[4]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateNewSolutionInClonedRepo.PNG
[7]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitMenuItem.PNG
[8]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[9]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateCloudService.PNG
[10]: ./media/cloud-services-continuous-delivery-use-vso-git/SetUpPublishingWithVSO.PNG
[11]: ./media/cloud-services-continuous-delivery-use-vso-git/AuthorizeConnection.PNG
[12]: ./media/cloud-services-continuous-delivery-use-vso-git/ConnectionRequest.PNG
[13]: ./media/cloud-services-continuous-delivery-use-vso-git/ChooseARepo3.PNG
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso-git/MakeACodeChange.PNG
[20]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[21]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerHome.png
[22]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerBuilds.PNG
[23]: ./media/cloud-services-continuous-delivery-use-vso-git/BuildInQueue.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso-git/ProcessTab.PNG
[28]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateANewAccount.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso-git/PushCurrentBranch.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso-git/BranchesInTeamExplorer.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso-git/NewBranch.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateBranch.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso-git/PublishBranch.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso-git/SourceSettingsPage.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso-git/IncludeWorkingBranch.PNG
