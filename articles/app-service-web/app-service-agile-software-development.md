---
title: aaaAgile software ontwikkelen met Azure App Service
description: Meer informatie over hoe toocreate hoge schaalbaarheid complexe toepassingen met Azure App Service op een manier die flexibel software development ondersteunt.
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: c0fdb676-36a6-4738-925f-65b4835d187f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: a1c1c78cfff711774943b0235ed762f03f48fc6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="agile-software-development-with-azure-app-service"></a>Flexibele software ontwikkelen met Azure App Service
In deze zelfstudie leert u hoe toocreate hoge schaalbaarheid complexe toepassingen met [Azure App Service](/azure/app-service/) op een manier die ondersteuning biedt voor [flexibele software development](https://en.wikipedia.org/wiki/Agile_software_development). Er wordt vanuit gegaan dat u al hoe te weet[complexe toepassingen zoals verwacht in Azure implementeren](app-service-deploy-complex-application-predictably.md).

Beperkingen in technische processen kunnen vaak onafhankelijk zodanig Hallo van geslaagde implementatie van flexibele methoden. Azure App Service met functies zoals [continue publicatie](app-service-continuous-deployment.md), [faseringsomgevingen](web-sites-staged-publishing.md) (sleuven) en [bewaking](web-sites-monitor.md)wanneer goed samen met de Hallo orchestration en beheer van de implementatie in [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md), kan deel uitmaken van een uitstekende oplossing voor ontwikkelaars die flexibele software development spelen.

Hallo volgende tabel ziet u een korte lijst met vereisten die zijn gekoppeld aan de ontwikkeling van flexibele, en hoe Azure-services van deze inschakelen.

| Vereiste | Hoe Azure kunt |
| --- | --- |
| -Bouwen met elke doorvoer<br>-Automatisch bouwen en snelle |Wanneer met doorlopende implementatie is geconfigureerd, kunnen Azure App Service als builds van live uitgevoerd op basis van een vertakking dev functioneren. Telkens wanneer de code wordt toohello vertakking doorgeschoven, is automatisch gemaakt en wordt uitgevoerd live in Azure. |
| -Controleer builds zelf testen |Laden van de tests, webtests, enz., hello Azure Resource Manager-sjabloon kunnen worden geïmplementeerd. |
| -Tests uitvoeren in een kloon van de productie-omgeving |Azure Resource Manager-sjablonen kunnen worden gebruikt toocreate klonen van hello Azure productie-omgeving (met inbegrip van app-instellingen, verbinding tekenreeks sjablonen, schalen, enzovoort) voor het testen van snel en zoals verwacht. |
| -Weergeven resultaat van de laatste build eenvoudig |Doorlopende implementatie tooAzure vanuit een opslagplaats betekent dat u nieuwe code in een live-toepassing testen kunt onmiddellijk nadat u uw wijzigingen doorvoert. |
| -Doorvoeren toohello hoofdvertakking elke dag<br>-Implementatie automatiseren |Continue integratie van een productietoepassing met een opslagplaats hoofdvertakking implementeert automatisch elke tooproduction commit/merge toohello hoofdvertakking. |

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a>Wat u doet
Helpt u bij een typische dev-test-fase-productie-werkstroom in volgorde toopublish nieuwe wijzigingen toohello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) voorbeeldtoepassing, bestaat uit twee [web-apps](/services/app-service/web/), namelijk een frontend (FE) en Hallo andere wordt een end-Web-API (BE) en een [SQL-database](/services/sql-database/). U werkt met Hallo architectuur voor implementatie te volgen:

![](./media/app-service-agile-software-development/what-1-architecture.png)

afbeelding van tooput Hallo in woorden:

* Hallo-architectuur voor implementatie is onderverdeeld in drie verschillende omgevingen (of [resourcegroepen](../azure-resource-manager/resource-group-overview.md) in Azure), elk met een eigen [App Service-abonnement](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), [schalen](web-sites-scale.md) -instellingen en SQL-database. 
* Elke omgeving kan afzonderlijk worden beheerd. Ze kunnen zelfs bestaan uit verschillende abonnementen.
* Fasering en productie worden geïmplementeerd als twee sleuven Hallo dezelfde App Service-app. Hallo hoofdvertakking is ingesteld voor continue integratie met Hallo staging site.
* Wanneer een commit toomaster vertakking is geverifieerd op Hallo faseringssleuven (met productiegegevens), gecontroleerd of Hallo staging-app wordt gewisseld naar de productiesite Hallo [zonder uitvaltijd](web-sites-staged-publishing.md).

Hallo productie- en staging-omgeving is in Hallo sjabloon gedefinieerd op [  *&lt;repository_root >*/ARMTemplates/ProdandStage.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/ProdAndStage.json).

Hallo dev en testomgevingen worden gedefinieerd door de sjabloon op Hallo [  *&lt;repository_root >*/ARMTemplates/Dev.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/Dev.json).

U zult ook Hallo typische vertakkende strategie gebruiken met code verplaatsen van Hallo dev vertakking up toohello test vertakking en vervolgens de hoofdvertakking toohello (omhoog verplaatst van de kwaliteit, geval toospeak).

![](./media/app-service-agile-software-development/what-2-branches.png) 

## <a name="what-you-need"></a>Wat u nodig hebt
* Een Azure-account
* Een [GitHub](https://github.com/) account
* GIT-Shell (geïnstalleerd met [GitHub voor Windows](https://windows.github.com/))-Hiermee schakelt u toorun beide Hallo Git en PowerShell-opdrachten in Hallo dezelfde sessie 
* Meest recente [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps) bits
* Basiskennis van Hallo hulpprogramma's te volgen:
  * [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) sjabloonimplementatie (Zie ook [een complexe toepassing zoals verwacht in Azure implementeert](app-service-deploy-complex-application-predictably.md))
  * [Git](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> U moet een Azure-account toocomplete in deze zelfstudie:
> 
> * U kunt [gratis een Azure-account openen](https://azure.microsoft.com/pricing/free-trial/) -u ontvangt tegoed kunt u tootry uit betaalde Azure-services en zelfs nadat ze zijn gebruikt u Hallo rekening kunt houden en gebruik gratis Azure-services, zoals Web-Apps.
> * U kunt [voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -uw Visual Studio-abonnement ontvangt u elke maand tegoeden die u voor betaalde Azure-services kunt gebruiken.
> 
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

## <a name="set-up-your-production-environment"></a>Uw productieomgeving instellen
> [!NOTE]
> Hallo script automatisch gebruikt in deze zelfstudie configureert u continue publiceren vanaf uw GitHub-opslagplaats. Dit is vereist dat uw GitHub-referenties worden al opgeslagen in Azure, anders Hallo in een script vastgelegd implementatie mislukt tijdens een poging de instellingen voor bronbeheer tooconfigure voor Hallo web-apps. 
> 
> toostore uw GitHub-referenties in Azure, een web-app maken in Hallo [Azure-portal](https://portal.azure.com/) en [GitHub implementatie configureren](app-service-continuous-deployment.md). U hoeft alleen toodo dit één keer. 
> 
> 

In een typisch scenario voor DevOps, hebt u een toepassing die wordt uitgevoerd in Azure in en gewenste toomake wijzigingen tooit via continue publiceren. In dit scenario hebt u een sjabloon die u ontwikkeld, getest en gebruikte toodeploy Hallo productie-omgeving. Stelt u deze in deze sectie.

1. Maak uw eigen fork Hallo [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) opslagplaats. Zie voor meer informatie over het maken van uw fork [een opslagplaats vertakken](https://help.github.com/articles/fork-a-repo/). Zodra uw fork is gemaakt, kunt u deze bekijken in uw browser.
   
    ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. Open een Git-Shell-sessie. Als u nog Git-Shell hebt, installeert u [GitHub voor Windows](https://windows.github.com/) nu.
3. Maak een lokale kloon van uw fork door het uitvoeren van de volgende opdracht Hallo:

        git clone https://github.com/<your_fork>/ToDoApp.git 
4. Zodra u uw lokale kloon hebt, te navigeren*&lt;repository_root >*\ARMTemplates en Voer Hallo deploy.ps1 script als volgt:
   
        .\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git
5. Wanneer u wordt gevraagd, typt u in Hallo gewenst gebruikersnaam en wachtwoord voor toegang tot de database.
   
   U ziet de voortgang van de verschillende Azure-resources inrichten Hallo. Wanneer implementatie is voltooid, wordt Hallo script Hallo-toepassing in Hallo browser wordt gestart en geeft u een beschrijvende geluid.
   
    ![](./media/app-service-agile-software-development/production-2-app-in-browser.png)
   
   > [!TIP]
   > Kijk eens naar  *&lt;repository_root >*\ARMTemplates\Deploy.ps1, toosee hoe resources met unieke id's worden gegenereerd. U kunt dezelfde benadering toocreate wordt gekloond van Hallo Hallo dezelfde implementatie zonder dat u conflicterende resourcenamen.
   > 
   > 
6. Terug in uw sessie Git Shell uitvoeren:
   
        .\swap –Name ToDoApp<unique_string>master
   
    ![](./media/app-service-agile-software-development/production-4-swap.png)
7. Wanneer Hallo-script is voltooid, gaat u terug toobrowse toohello frontend-adres (http://ToDoApp*&lt;unique_string >*master.azurewebsites.net/) toosee Hallo toepassing die wordt uitgevoerd in de productieomgeving.
8. Meld u bij toohello [Azure-portal](https://portal.azure.com/) en eens kijken wat wordt gemaakt.
   
   U moet de web-apps kunnen toosee twee in Hallo dezelfde resourcegroep bevinden, één met de Hallo `Api` achtervoegsel in Hallo naam. Als u Hallo resourcegroepweergave bekijkt, ziet u ook Hallo SQL-Database en -server, Hallo App Service-abonnement en fasering sleuven Hallo voor Hallo web-apps. Blader door de verschillende bronnen Hallo en vergelijkt ze met  *&lt;repository_root >*\ARMTemplates\ProdAndStage.json toosee hoe deze zijn geconfigureerd in Hallo-sjabloon.
   
    ![](./media/app-service-agile-software-development/production-3-resource-group-view.png)

U hebt nu Hallo productie-omgeving instellen. Vervolgens wordt u een nieuwe update toohello toepassing starten.

## <a name="create-dev-and-test-branches"></a>Dev maken en testen van vertakkingen
Nu dat u een complexe toepassing die wordt uitgevoerd in de productieomgeving in Azure hebt, kunt u een update tooyour toepassing in overeenstemming met flexibele methodologie maakt. In deze sectie maakt u Hallo ontwikkeling en tests vertakkingen dat u toomake Hallo vereiste updates moet.

1. Maak eerst Hallo-testomgeving. In de Git-Shell-sessie uitvoeren Hallo volgende toocreate Hallo omgeving voor een nieuwe vertakking aangeroepen opdrachten **NewUpdate**. 
   
        git checkout -b NewUpdate
        git push origin NewUpdate 
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch NewUpdate
2. Wanneer u wordt gevraagd, typt u in Hallo gewenst gebruikersnaam en wachtwoord voor toegang tot de database. 
   
   Wanneer implementatie is voltooid, wordt Hallo script Hallo-toepassing in Hallo browser wordt gestart en geeft u een beschrijvende geluid. U hebt nu een nieuwe vertakking met een eigen testomgeving. Een tooreview moment dat een aantal zaken over deze testomgeving nemen:
   
   * U kunt dit in een Azure-abonnement maken. Dit betekent dat Hallo productie-omgeving kan afzonderlijk worden beheerd vanaf uw testomgeving.
   * Uw testomgeving wordt live in Azure uitgevoerd.
   * Uw testomgeving is identiek toohello productie-omgeving, met uitzondering van Hallo sleuven voor fasering en Hallo schalen. Weet u het omdat ze Hallo alleen verschillen tussen ProdandStage.json en Dev.json.
   * U kunt uw testomgeving beheren in een eigen App Service-abonnement, met een andere prijs-laag (zoals **vrije**).
   * Verwijderen van deze testomgeving is net zo eenvoudig als het Hallo-resourcegroep verwijderen. U leert hoe toodo dit [later](#delete).
3. Ga op toocreate een vertakking dev door te voeren Hallo volgende opdrachten:
   
        git checkout -b Dev
        git push origin Dev
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch Dev
4. Wanneer u wordt gevraagd, typt u in Hallo gewenst gebruikersnaam en wachtwoord voor toegang tot de database. 
   
   Een tooreview moment dat een aantal zaken over deze omgeving dev nemen: 
   
   * Uw omgeving dev heeft een configuratie identieke toohello-testomgeving omdat het wordt geïmplementeerd met behulp van Hallo dezelfde sjabloon.
   * Elke dev-omgeving kan worden gemaakt in Hallo van ontwikkelaars Azure-abonnement, Hallo test omgeving toobe afzonderlijk beheerd verlaten.
   * Uw omgeving dev wordt live in Azure uitgevoerd.
   * Verwijderen van Hallo dev-omgeving is net zo eenvoudig als het verwijderen van resourcegroep Hallo. U leert hoe toodo dit [later](#delete).

> [!NOTE]
> Wanneer u meerdere ontwikkelaars die werken op nieuwe update Hallo hebt, kunt elk van deze eenvoudig een vertakking en speciale dev-omgeving maken met Hallo stappen te volgen:
> 
> 1. Maken van hun eigen fork van Hallo-opslagplaats in GitHub (Zie [een opslagplaats vertakken](https://help.github.com/articles/fork-a-repo/)).
> 2. Kloon Hallo fork op hun lokale computer
> 3. Hallo voeren opdrachten dezelfde toocreate dev vertakking en hun eigen omgeving.
> 
> 

Wanneer u bent klaar, moet uw GitHub-fork drie vertakkingen hebt:

![](./media/app-service-agile-software-development/test-1-github-view.png)

En moet u zes web-apps (drie sets van twee) hebben in drie afzonderlijke resourcegroepen:

![](./media/app-service-agile-software-development/test-2-all-webapps.png)

> [!NOTE]
> ProdandStage.json geeft Hallo productie-omgeving toouse hello **standaard** prijscategorie op geschikt is voor schaalbaarheid van Hallo productie-toepassing.
> 
> 

## <a name="build-and-test-every-commit"></a>Bouwen en testen van elke doorvoer
Hallo sjabloonbestanden ProdAndStage.json en Dev.json al Hallo bron besturingselement parameters opgeeft, die standaard continue publiceren voor Hallo web-app ingesteld. Elke vertakking doorvoeren toohello GitHub activeert daarom een automatische implementatie tooAzure van die vertakking. Laten we zien hoe uw setup werkt nu.

1. Zorg ervoor dat u in Hallo Dev vertakking van lokale Hallo-opslagplaats. toodo deze, Voer Hallo opdracht in de Git-Shell te volgen:
   
        git checkout Dev
2. Een wijziging toohello app UI laag maken door het wijzigen van Hallo code toouse [Bootstrap](http://getbootstrap.com/components/) bevat. Open  *&lt;repository_root >*\src\MultiChannelToDo.Web\index.cshtml en maak Hallo na gemarkeerde wijziging:
   
    ![](./media/app-service-agile-software-development/commit-1-changes.png)
   
    > [!NOTE]
    > Als u niet kunt lezen Hallo voorgaande afbeelding: 
    > 
    > * Wijzig in regel 18 `check-list` te`list-group`.
    > * Wijzig in regel 19 `class="check-list-item"` te`class="list-group-item"`.
    > 
    > 
3. Hallo wijziging opslaan. Terug Git Shell, start Hallo volgende opdrachten:
   
        cd <repository_root>
        git add .
        git commit -m "changed toobootstrap style"
        git push origin Dev
   
   Deze git-opdrachten zijn vergelijkbaar te 'controleren in uw code' in een ander bronbeheersysteem zoals TFS. Bij het uitvoeren van `git push`, nieuwe commit Hallo activeert een automatische code push tooAzure, welke vervolgens opnieuw worden opgebouwd Hallo toepassing tooreflect Hallo wijzigen in Hallo dev-omgeving.
4. tooverify die deze code push tooyour dev-omgeving heeft plaatsgevonden, gaat u pagina tooyour dev omgeving web-app en bekijkt hello **implementatie** onderdeel. U moet kunnen toosee er uw meest recente commit-bericht.
   
    ![](./media/app-service-agile-software-development/commit-2-deployed.png)
5. Van daaruit, klikt u op **Bladeren** toosee Hallo nieuwe wijzigingen in Hallo live-toepassing in Azure.
   
    ![](./media/app-service-agile-software-development/commit-3-webapp-in-browser.png)
   
   Er is een kleine wijziging toohello-toepassing. Veel tijden nieuwe wijzigingen tooa complexe webtoepassing wel onbedoelde en ongewenste neveneffecten. Kan tooeasily test wordt kunt elke doorvoer live builds u toocatch deze problemen voordat ze uw klanten zien.

Nu moet u vertrouwd met de Hallo realisatie die als een ontwikkelaar op Hallo **NewUpdate** project, kunt u een dev-omgeving maken voor uzelf, en vervolgens elke doorvoer bouwen en testen van elke build.

## <a name="merge-code-into-test-environment"></a>Code in de testomgeving samenvoegen
Wanneer u klaar toopush uw code uit Dev vertakking up tooNewUpdate vertakking bent, is het Hallo standaard git proces:

1. Een nieuwe doorvoeracties tooNewUpdate samenvoegen met Hallo Dev vertakking in GitHub, zoals doorvoeracties gemaakt door andere ontwikkelaars. Een nieuwe doorvoeren op GitHub activeert een code-push- en Buildgegevens in Hallo dev-omgeving. U kunt er vervolgens voor zorgen dat uw code in Dev vertakking werkt nog altijd met de meest recente bits Hallo NewUpdate vertakken.
2. Uw nieuwe doorvoeracties Dev vertakken samenvoegen met NewUpdate vertakking op GitHub. Deze actie wordt een code-push en build in de testomgeving Hallo geactiveerd. 

Opmerking opnieuw omdat met deze vertakkingen git al doorlopende implementatie is ingesteld, u niet tootake geen andere acties hoeft zoals integratie met bouwt. U hoeft alleen tooperform standaard bron besturingselement procedures met git en Azure alle Hallo build processen voor u uitvoert.

Nu gaan we uw code te pushen**NewUpdate** vertakking. Git-Shell, start Hallo volgende opdrachten:

    git checkout NewUpdate
    git pull origin NewUpdate
    git merge Dev
    git push origin NewUpdate

Dat is alles. 

Pagina Ga toohello web-app voor uw omgeving testen toosee uw nieuwe doorvoeren (NewUpdate vertakking samengevoegd) nu toohello testomgeving gepusht. Klik vervolgens op **Bladeren** toosee die Hallo stijl wijzigen wordt nu uitgevoerd in Azure in.

## <a name="deploy-update-tooproduction"></a>Update tooproduction implementeren
Code toohello pushen fasering en productie-omgeving moet u kunt niet anders dan wat u hebt al gedaan wanneer u code toohello testomgeving gepusht. Het is heel eenvoudig. 

Git-Shell, start Hallo volgende opdrachten:

    git checkout master
    git pull origin master
    git merge NewUpdate
    git push origin master

Houd er rekening mee dat op basis van Hallo manier Hallo fasering en productie-omgeving is ingesteld in ProdandStage.json, toohello wordt doorgeschoven, is je nieuwe code **fasering** sleuf en er wordt uitgevoerd. Als u toohello faseringssleuf gewisseld URL navigeert, ziet u dus Hallo nieuwe code er uitgevoerd. toodo deze, Voer Hallo volgende cmdlet in de Git-Shell.

    Start-Process -FilePath "http://ToDoApp<unique_string>master-Staging.azurewebsites.net"

En nu, nadat u hebt geverifieerd Hallo update in faseringssleuven hello, Hallo alleen ding links toodo tooswap is deze in productie. Git-Shell, net start Hallo volgende opdrachten:

    cd <repository_root>\ARMTemplates
    .\swap.ps1 -Name ToDoApp<unique_string>master

Gefeliciteerd. U hebt een nieuwe update tooyour productie-webtoepassing heeft gepubliceerd. Sterker nog is die dit gedaan met eenvoudig dev- en testomgevingen, maken en bouwen en testen van elke doorvoer. Dit zijn essentieel bouwstenen voor ontwikkeling van flexibele software.

<a name="delete"></a>

## <a name="delete-dev-and-test-environments"></a>Dev verwijderen en omgevingen testen
Omdat u uw dev opzettelijk hebt ontworpen en omgevingen toobe zelfstandig resourcegroepen getest, is het eenvoudig toodelete ze. toodelete hello die u hebt gemaakt in deze zelfstudie Hallo GitHub vertakkingen zowel Azure artefacten voert Hallo opdrachten in de Git-Shell te volgen:

    git branch -d Dev
    git push origin :Dev
    git branch -d NewUpdate
    git push origin :NewUpdate
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>dev-group -Force -Verbose
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>newupdate-group -Force -Verbose

## <a name="summary"></a>Samenvatting
Flexibele software development is een moet zijn voor veel bedrijven willen tooadopt Azure als het toepassingsplatform van hun. In deze zelfstudie hebt u geleerd hoe toocreate en tear omlaag exacte replica's of in de buurt van replica's van productie-omgeving Hallo met gemak, zelfs voor complexe toepassingen. U hebt ook geleerd hoe tooleverage deze mogelijkheid toocreate een ontwikkeling verwerken die kan bouwen en testen van elke één doorvoer in Azure. Deze zelfstudie ideale geval leert u het beste gebruik van Azure App Service en Azure Resource Manager samen toocreate een DevOps-oplossing die caters tooagile methoden. Vervolgens kunt u in dit scenario door het uitvoeren van geavanceerde DevOps technieken zoals [testen in productie](app-service-web-test-in-production-get-start.md). Zie voor een algemeen scenario voor het testen in productie [Flighting implementatie (bètaversie testen) in Azure App Service](app-service-web-test-in-production-controlled-test-flight.md).

## <a name="more-resources"></a>Meer bronnen
* [Een complexe toepassing zoals verwacht in Azure implementeren](app-service-deploy-complex-application-predictably.md)
* [Flexibel ontwikkelen in de praktijk: Tips en trucs voor gemoderniseerde ontwikkelingscyclus](http://channel9.msdn.com/Events/Ignite/2015/BRK3707)
* [Geavanceerde implementatie van strategieën voor Web-Apps van Azure Resource Manager-sjablonen](http://channel9.msdn.com/Events/Build/2015/2-620)
* [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint - Hallo JSON Validator](http://jsonlint.com/)
* [ARMClient – GitHub publishing toosite instellen](https://github.com/projectKudu/ARMClient/wiki/Setup-GitHub-publishing-to-Site)
* [GIT vertakking – basis vertakking en samenvoegen](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [David Ebbo van Blog](http://blog.davidebbo.com/)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure platformoverschrijdende-opdrachtregelprogramma 's](../cli-install-nodejs.md)
* [Gebruikers maken of bewerken in Azure AD](https://msdn.microsoft.com/library/azure/hh967632.aspx#BKMK_1)
* [Project Kudu Wiki](https://github.com/projectkudu/kudu/wiki)

