---
title: Continue levering met Git en Visual Studio Team Services in Azure | Microsoft Docs
description: Informatie over het configureren van uw teamprojecten Visual Studio Team Services voor het gebruik van Git om automatisch te bouwen en implementeren voor de functie Web-App in Azure App Service- of cloud-services.
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
ms.openlocfilehash: f4f5f231536bc381d17898ff2c592be821168a65
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services-and-git"></a>Onafgebroken levering naar Azure met Visual Studio Team Services en Git
Teamprojecten Visual Studio Team Services kunt u een Git-opslagplaats host voor de broncode en om automatisch te bouwen en implementeren voor Azure-web-apps of cloudservices wanneer u een doorvoeren naar de opslagplaats forceren.

U moet Visual Studio 2013 en de Azure-SDK geïnstalleerd. Als u nog geen Visual Studio 2013 hebt, downloadt u dit door het kiezen van de **gratis aan de slag** koppeling [www.visualstudio.com](http://www.visualstudio.com). Installeer de Azure-SDK van [hier](http://go.microsoft.com/fwlink/?LinkId=239540).

> [!NOTE]
> U moet een Visual Studio Team Services-account om deze zelfstudie te voltooien: U kunt [gratis een Visual Studio Team Services-account openen](http://go.microsoft.com/fwlink/p/?LinkId=512979).
> 
> 

Voer de volgende stappen uit voordat u een cloudservice om automatisch te bouwen en implementeren in Azure met behulp van Visual Studio Team Services kunt instellen.

## <a name="1-create-a-git-repository"></a>1: een Git-opslagplaats maken
1. Als u nog een Visual Studio Team Services-account hebt, kunt u een [hier](http://go.microsoft.com/fwlink/?LinkId=397665). Wanneer u uw teamproject maakt, kiest u Git als uw bronbeheersysteem. Volg de instructies voor het verbinden van Visual Studio aan uw teamproject.
2. In **Team Explorer**, kies de **deze opslagplaats klonen** koppeling.
   
    ![][3]
3. Geef de locatie van de lokale kopie en kies vervolgens de **kloon** knop.

## <a name="2-create-a-project-and-commit-it-to-the-repository"></a>2: Maak een project en het doorvoeren naar de opslagplaats
1. In **Team Explorer**, in de **oplossingen** sectie, kiest u de **nieuw** koppeling naar een nieuw project maken in de lokale opslagplaats.
   
    ![][4]
2. De stappen in dit scenario kunt u een web-app of een service in de cloud (Azure-toepassing) implementeren. Maak een nieuw Azure Cloud Service-project of een nieuw ASP.NET MVC-project. Controleer of het project gericht op .NET Framework 4 of hoger. Als u een cloudserviceproject maakt, een ASP.NET MVC-Webrol en een werkrol toevoegen.
   Als u maken van een web-app wilt, kiest u de **ASP.NET-webtoepassing** sjabloon project en kies vervolgens **MVC**. Zie [een ASP.NET-web-app maken in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) voor meer informatie.
3. Open het snelmenu voor de oplossing en kies **doorvoeren**.
   
    ![][7]
4. Als dit de eerste keer dat u Git in Visual Studio Team Services hebt gebruikt, moet u bepaalde informatie gegeven om u te identificeren in Git. In de **wijzigingen in behandeling** gebied van **Team Explorer**, Voer uw gebruikersnaam en e-mailadres. Voer een opmerking in voor het doorvoeren en kies vervolgens de **doorvoeren** knop.
   
    ![][8]
5. Noteer de opties die u wilt opnemen of uitsluiten van specifieke wijzigingen wanneer u incheckt. Als u de gewenste wijzigingen zijn uitgesloten, kiest u **omvatten alle**.
6. U hebt nu de wijzigingen doorgevoerd in het lokale exemplaar van de opslagplaats. Vervolgens deze wijzigingen met de server te synchroniseren door het kiezen van de **Sync** koppeling.

## <a name="3-connect-the-project-to-azure"></a>3: verbinding maken met het project naar Azure
1. Nu dat u een Git-opslagplaats in Visual Studio Team Services met sommige broncode erin hebt, bent u klaar om de git-opslagplaats met in Azure.  In de [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885), selecteer uw cloud-service of web-app of een nieuwe maken door het kiezen van de + pictogram naar links en te kiezen onder **Cloudservice** of **Web-App** en vervolgens **snelle invoer**.
   
    ![][9]
2. Kies voor cloudservices, de **publiceren met Visual Studio Team Services instellen** koppeling. Kies voor web-apps, de **implementatie vanuit resourcebeheer instellen** koppeling.
   
    ![][10]
3. Typ de naam van uw Visual Studio Team Services-account in het tekstvak in de wizard en kies de **autoriseren nu** koppeling. U wordt mogelijk gevraagd aan te melden.
   
    ![][11]
4. In de **verbindingsaanvraag** pop-upvenster kiezen **accepteren** voor het autoriseren van Azure voor het configureren van uw teamproject in Visual Studio Team Services.
   
    ![][12]
5. Nadat de autorisatie is geslaagd, ziet u een vervolgkeuzelijst met uw teamprojecten Visual Studio Team Services.  Selecteer de naam van teamproject dat u in de vorige stappen hebt gemaakt en kies selectievakje-knop van de wizard.
   
    ![][13]
   
    De volgende keer dat u het doorvoeren van gegevens naar uw opslagplaats pushen Visual Studio Team Services bouwt en uw project implementeren in Azure.

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4: de tabel opnieuw activeren en implementeren van uw project
1. In Visual Studio, opent u een bestand en deze te wijzigen. Wijzig bijvoorbeeld het bestand `_Layout.cshtml` onder de weergaven\\gedeelde map in een MVC-Webrol.
   
    ![][17]
2. Bewerk de voettekst voor de site en sla het bestand.
   
    ![][18]
3. In **Solution Explorer**, open het snelmenu voor het knooppunt oplossing, projectknooppunt of het bestand gewijzigd, en kies vervolgens **doorvoeren**.
4. Typ in een opmerking en kies **doorvoeren**.
   
    ![][20]
5. Kies de **Sync** koppeling.
   
    ![][38]
6. Kies de **Push** koppeling naar uw commit push naar de opslagplaats in Visual Studio Team Services. (U kunt ook de **Sync** knop uw doorvoeracties kopiëren naar de opslagplaats. Het verschil is dat **Sync** ook de meest recente wijzigingen ophaalt uit de opslagplaats.)
   
    ![][39]
7. Kies de **thuis** terug te keren naar de **Team Explorer** startpagina.
   
    ![][21]
8. Kies **Builds** om weer te geven van de opbouw uitgevoerd.
   
    ![][22]
   
    **In een team Explorer** ziet u dat een build voor uw inchecken is geactiveerd.
   
    ![][23]
9. Om weer te geven een gedetailleerd logboek in de loop van de build, dubbelklikt u op de naam van de build uitgevoerd.
10. Hoewel de build in voortgang, bekijk de build-definitie die is gemaakt toen u de wizard hebt gebruikt om te koppelen aan Azure.  Open het snelmenu voor de definitie van de build en kies **bouwen definitie bewerken**.
    
    ![][25]
11. In de **Trigger** tabblad ziet u dat de definitie van de build is standaard ingesteld op voor elke inchecken bouwen. (Voor een cloudservice, Visual Studio Team Services bouwt en worden de hoofdvertakking geïmplementeerd op de testomgeving. U hebt nog wel een handmatige stap naar de live site implementeren. Voor een web-app dat geen staging-omgeving, wordt de hoofdvertakking geïmplementeerd rechtstreeks naar de live site.
    
    ![][26]
12. In de **proces** tabblad ziet u de implementatieomgeving is ingesteld op de naam van uw cloud-service of web-app.
    
     ![][27]
13. Geef waarden voor de eigenschappen als u wilt dat andere waarden dan de standaardwaarden. De eigenschappen voor Azure publicatie zijn de **implementatie** sectie en kunt u wellicht ook MSBuild-parameters instellen. Bijvoorbeeld in een cloud service-project op te geven van een serviceconfiguratie dan 'Cloud' ingesteld de MSbuild-parameters op `/p:TargetProfile=[YourProfile]` waar *[YourProfile]* overeenkomt met een configuratiebestand voor de service met een naam zoals serviceconfiguration zijn. *YourProfile*cscfg-bestand.
    
     De volgende tabel bevat de beschikbare eigenschappen in de **implementatie** sectie:
    
    | Eigenschap | Standaardwaarde |
    | --- | --- |
    | Niet-vertrouwde certificaten toestaan |Als het ONWAAR is, moeten de SSL-certificaten zijn ondertekend door een basisinstantie. |
    | Upgrade toestaan |Hiermee kunt de implementatie bijwerken van een bestaande implementatie in plaats van een nieuwe maken. Het IP-adres, blijft behouden. |
    | Niet verwijderen |Indien waar, de implementatie van een bestaande niet-verwante niet overschrijven (upgrade is toegestaan). |
    | Pad naar de implementatie-instellingen |Het pad naar het bestand .pubxml voor een web-app, ten opzichte van de hoofdmap van de opslagplaats. Genegeerd voor cloud-services. |
    | SharePoint-omgeving voor implementatie |Hetzelfde als de naam van de service. |
    | Azure-implementatie-omgeving |De web-app of cloud servicenaam. |
14. Op dit tijdstip moet uw build worden voltooid.
    
     ![][28]
15. Als u dubbelklikt op de naam van de build, ziet u Visual Studio een **bouwen samenvatting**, met inbegrip van de testresultaten van eenheid Testprojecten die is gekoppeld.
    
     ![][29]
16. In de [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885), kunt u de gekoppelde implementatie bekijken op de **implementaties** tabblad wanneer de faseringsomgeving is geselecteerd.
    
     ![][30]
17. Blader naar de URL van uw site. Voor een web-app, kies de **Bladeren** knop in de portal. Voor een cloudservice, kiest u de URL in de **snel in één oogopslag** sectie van de **Dashboard** pagina waarin de Staging-omgeving.
    
    Implementaties van continue integratie voor cloud-services worden gepubliceerd op de faseringsomgeving standaard. U kunt dit wijzigen door in te stellen de **alternatieve Cloudserviceomgeving** eigenschap **productie**. Hier is waarbij de URL van de site op de dashboardpagina van de cloudservice.
    
    ![][31]
    
    Een nieuw browsertabblad geopend om uw actieve site weer te geven.
    
    ![][32]
18. Als u andere wijzigingen aan uw project aanbrengt, u trigger meer maakt en u kunt meerdere implementaties wordt verzameld. De meest recente versie is gemarkeerd als actief.
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5: een eerdere build implementeren
Deze stap is optioneel. In de klassieke Azure portal, kiest u een eerdere implementatie en kies **implementeren** terugspoelen van uw site een eerdere in te checken. Houd er rekening mee dat dit een nieuwe build in TFS activeren en maken van een nieuwe vermelding in de geschiedenis van uw implementatie.

![][34]

## <a name="6-change-the-production-deployment"></a>6: de productie-implementatie wijzigen
Wanneer u klaar bent, kunt u de faseringsomgeving naar de productieomgeving promoveren kiezen **wisselen** in de klassieke Azure portal. De zojuist geïmplementeerde faseringsomgeving wordt gepromoveerd voor productie en de vorige productie-omgeving, indien aanwezig, wordt een Staging-omgeving. De actieve implementatie mogelijk anders voor de productie- en Faseringsomgevingen, maar de geschiedenis van de implementatie van recente builds is hetzelfde, ongeacht de omgeving.

![][35]

## <a name="7-deploy-from-a-working-branch"></a>7: implementeren vanuit een werkvertakking.
Wanneer u met Git, meestal wijzigingen aanbrengt in een werkvertakking en integreren in de hoofdvertakking wanneer de ontwikkeling van een voltooide status bereikt. Tijdens de ontwikkelingsfase van een project, moet u het bouwen en implementeren van de werkvertakking in Azure.

1. In **Team Explorer**, kies de **Start** knop en kies vervolgens de **vertakkingen** knop.
   
    ![][40]
2. Kies de **nieuwe vertakking** koppeling.
   
    ![][41]
3. Voer de naam van de vertakking, zoals 'werken', en kies **vertakking maken**. Hiermee maakt u een nieuwe lokale vertakking.
   
    ![][42]
4. Publiceer de vertakking. Kies de naam van de vertakking in **niet gepubliceerd vertakkingen**, en kies **publiceren**.
   
    ![][44]
5. Alleen de wijzigingen naar de hoofdvertakking activeren standaard een continue build. Als u continue build voor een werkvertakking instelt, kies de **Builds** pagina in **Team Explorer**, en kies **bouwen definitie bewerken**.
6. Open de **broninstellingen** tabblad. Onder **bewaakt vertakkingen voor continue integratie en build**, kies **Klik hier om een nieuwe rij toegevoegd**.
   
    ![][47]
7. Geef de vertakking die u hebt gemaakt, zoals koppen refs werkende.
   
    ![][48]
8. Een wijziging aanbrengt in de code en kies vervolgens opent u het snelmenu voor het gewijzigde bestand **doorvoeren**.
   
    ![][43]
9. Kies de **niet-gesynchroniseerde doorvoeracties** koppeling en kies de **Sync** knop of de **Push** koppeling kopiëren van de wijzigingen naar de kopie van de werkvertakking in Visual Studio Team Services.
   
   ![][45]
10. Navigeer naar de **Builds** bekijken en de build die zojuist is geactiveerd voor de werkvertakking niet vinden.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer tips over het gebruik van Git met Visual Studio Team Services meer [ontwikkelen en delen van uw code in Git met Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) en Zie voor meer informatie over het gebruik van een Git-opslagplaats die niet wordt beheerd door Visual Studio Team Services te publiceren naar Azure [continue implementatie naar Azure App Service](../app-service-web/app-service-continuous-deployment.md). Zie voor meer informatie over Visual Studio Team Services [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).

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
