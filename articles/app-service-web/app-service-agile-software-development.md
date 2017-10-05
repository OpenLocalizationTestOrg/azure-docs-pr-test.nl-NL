---
title: Flexibele software ontwikkelen met Azure App Service
description: Informatie over het hoge schaalbaarheid complexe toepassingen met Azure App Service maken op een manier die flexibel software development ondersteunt.
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
ms.openlocfilehash: 5ed888cbb422766cf2094f5980dfd1c599bd431c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="agile-software-development-with-azure-app-service"></a>Flexibele software ontwikkelen met Azure App Service
In deze zelfstudie leert u het maken van complexe toepassingen met hoge schaalbaarheid [Azure App Service](/azure/app-service/) op een manier die ondersteuning biedt voor [flexibele software development](https://en.wikipedia.org/wiki/Agile_software_development). Er wordt vanuit gegaan dat u al weet hoe [complexe toepassingen zoals verwacht in Azure implementeren](app-service-deploy-complex-application-predictably.md).

Beperkingen in technische processen kunnen de geslaagde implementatie van flexibele methoden vaak verhinderen. Azure App Service met functies zoals [continue publicatie](app-service-continuous-deployment.md), [faseringsomgevingen](web-sites-staged-publishing.md) (sleuven) en [bewaking](web-sites-monitor.md)wanneer goed samen met de orchestration en het beheer van implementatie in [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md), kan deel uitmaken van een uitstekende oplossing voor ontwikkelaars die open staan voor ontwikkeling van flexibele software.

De volgende tabel bevat een overzicht van vereisten die zijn gekoppeld aan de ontwikkeling van flexibele, en hoe Azure-services van deze inschakelen.

| Vereiste | Hoe Azure kunt |
| --- | --- |
| -Bouwen met elke doorvoer<br>-Automatisch bouwen en snelle |Wanneer met doorlopende implementatie is geconfigureerd, kunnen Azure App Service als builds van live uitgevoerd op basis van een vertakking dev functioneren. Telkens wanneer de code voor de vertakking wordt doorgeschoven, is het automatisch gebouwd en actief live in Azure. |
| -Controleer builds zelf testen |Laden van de tests, webtests, enz., kan worden geïmplementeerd met Azure Resource Manager-sjabloon. |
| -Tests uitvoeren in een kloon van de productie-omgeving |Azure Resource Manager-sjablonen kunnen worden gebruikt voor het maken van klonen van de Azure productie-omgeving (met inbegrip van app-instellingen, verbinding tekenreeks sjablonen, schalen, enzovoort) voor het testen van snel en zoals verwacht. |
| -Weergeven resultaat van de laatste build eenvoudig |Continue implementatie naar Azure van een opslagplaats betekent dat u nieuwe code in een live-toepassing testen kunt onmiddellijk nadat u uw wijzigingen doorvoert. |
| -Doorvoeren naar de hoofdvertakking elke dag<br>-Implementatie automatiseren |Elke commit/merge continue integratie van een productietoepassing met een opslagplaats hoofdvertakking automatisch geïmplementeerd naar de hoofdvertakking naar productie. |

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a>Wat u doet
U helpt bij een typische dev-test-fase-productie-werkstroom om te kunnen publiceren van nieuwe wijzigingen in de [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) voorbeeldtoepassing, bestaat uit twee [web-apps](/services/app-service/web/), een wordt een frontend (FE) en de andere wordt een end-Web-API (BE) en een [SQL-database](/services/sql-database/). U werkt met de volgende implementatiearchitectuur:

![](./media/app-service-agile-software-development/what-1-architecture.png)

De afbeelding in woorden plaatsen:

* De architectuur voor implementatie is onderverdeeld in drie verschillende omgevingen (of [resourcegroepen](../azure-resource-manager/resource-group-overview.md) in Azure), elk met een eigen [App Service-abonnement](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), [schalen](web-sites-scale.md) instellingen en SQL-database. 
* Elke omgeving kan afzonderlijk worden beheerd. Ze kunnen zelfs bestaan uit verschillende abonnementen.
* Fasering en productie worden geïmplementeerd als twee sleuven van dezelfde App Service-app. De hoofdvertakking is voor continue integratie met de faseringssleuf ingesteld.
* Wanneer een doorvoeren naar de hoofdvertakking is geverifieerd op de faseringssleuf (met productiegegevens), de geverifieerde staging-app wordt gewisseld naar de productiesite [zonder uitvaltijd](web-sites-staged-publishing.md).

De productie- en staging-omgeving wordt gedefinieerd door de sjabloon op [  *&lt;repository_root >*/ARMTemplates/ProdandStage.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/ProdAndStage.json).

De ontwikkeling en testomgevingen zijn gedefinieerd door de sjabloon op [  *&lt;repository_root >*/ARMTemplates/Dev.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/Dev.json).

U zult ook de typische vertakkende strategie gebruiken met de code van de dev-vertakking naar de vertakking test vervolgens verplaatst naar de hoofdvertakking (omhoog verplaatst van de kwaliteit, dus tot speak).

![](./media/app-service-agile-software-development/what-2-branches.png) 

## <a name="what-you-need"></a>Wat u nodig hebt
* Een Azure-account
* Een [GitHub](https://github.com/) account
* GIT-Shell (geïnstalleerd met [GitHub voor Windows](https://windows.github.com/))-kunt u de Git- en PowerShell-opdrachten uitvoeren in dezelfde sessie 
* Meest recente [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps) bits
* Basiskennis van de volgende hulpprogramma's:
  * [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) sjabloonimplementatie (Zie ook [een complexe toepassing zoals verwacht in Azure implementeert](app-service-deploy-complex-application-predictably.md))
  * [Git](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> U hebt een Azure-account nodig om deze zelfstudie te voltooien.
> 
> * U kunt [gratis een Azure-account openen](https://azure.microsoft.com/pricing/free-trial/) -u ontvangt tegoed kunt u uitproberen betaalde Azure-services en zelfs nadat ze zijn gebruikt kunt u het account houden en gebruik gratis Azure-services, zoals Web-Apps.
> * U kunt [voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -uw Visual Studio-abonnement ontvangt u elke maand tegoeden die u voor betaalde Azure-services kunt gebruiken.
> 
> Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

## <a name="set-up-your-production-environment"></a>Uw productieomgeving instellen
> [!NOTE]
> Het script automatisch gebruikt in deze zelfstudie configureert u continue publiceren vanaf uw GitHub-opslagplaats. Dit is vereist dat uw referenties GitHub al zijn opgeslagen in Azure, anders de scriptmethode implementatie mislukt bij een poging tot het configureren van instellingen voor bronbeheer voor de web-apps. 
> 
> Als u wilt uw GitHub-referenties in Azure opslaat, maakt u een web-app in de [Azure-portal](https://portal.azure.com/) en [GitHub implementatie configureren](app-service-continuous-deployment.md). U hoeft hiervoor eenmaal. 
> 
> 

In een typische DevOps-scenario hebt u een toepassing die live in Azure wordt uitgevoerd en u wilt wijzigen via continue publiceren. In dit scenario hebt u een sjabloon die is ontwikkeld, getest en gebruikt voor het implementeren van de productie-omgeving. Stelt u deze in deze sectie.

1. Maak uw eigen fork van de [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) opslagplaats. Zie voor meer informatie over het maken van uw fork [een opslagplaats vertakken](https://help.github.com/articles/fork-a-repo/). Zodra uw fork is gemaakt, kunt u deze bekijken in uw browser.
   
    ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. Open een Git-Shell-sessie. Als u nog Git-Shell hebt, installeert u [GitHub voor Windows](https://windows.github.com/) nu.
3. Maak een lokale kloon van uw fork door het uitvoeren van de volgende opdracht:

        git clone https://github.com/<your_fork>/ToDoApp.git 
4. Wanneer u uw lokale kloon hebt, gaat u naar  *&lt;repository_root >*\ARMTemplates en de deploy.ps1 script als volgt uitvoeren:
   
        .\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git
5. Wanneer u wordt gevraagd, typt u in de gewenste gebruikersnaam en het wachtwoord voor toegang tot de database.
   
   U ziet de voortgang van de inrichting van verschillende Azure-resources. Wanneer implementatie is voltooid, wordt het script start de toepassing in de browser en geeft u een beschrijvende geluid.
   
    ![](./media/app-service-agile-software-development/production-2-app-in-browser.png)
   
   > [!TIP]
   > Kijk eens naar  *&lt;repository_root >*\ARMTemplates\Deploy.ps1 om te zien hoe resources met unieke id's worden gegenereerd. Klonen van de implementatie van dezelfde maken zonder dat u conflicterende resourcenamen kunt u dezelfde aanpak.
   > 
   > 
6. Terug in uw sessie Git Shell uitvoeren:
   
        .\swap –Name ToDoApp<unique_string>master
   
    ![](./media/app-service-agile-software-development/production-4-swap.png)
7. Wanneer het script is voltooid, gaat u terug om te bladeren naar de frontend-adres (http://ToDoApp*&lt;unique_string >*master.azurewebsites.net/) om te zien van de toepassing die wordt uitgevoerd in de productieomgeving.
8. Meld u aan bij de [Azure-portal](https://portal.azure.com/) en eens kijken wat wordt gemaakt.
   
   U moet kunnen zien van twee web-apps in dezelfde resourcegroep bevinden, één met de `Api` achtervoegsel in de naam. Als u de resourcegroepweergave bekijkt, ziet u ook de SQL-Database en -server, de App Service-abonnement en de staging-sleuven voor de web-apps. Blader door de verschillende bronnen en vergelijkt ze met  *&lt;repository_root >*\ARMTemplates\ProdAndStage.json om te zien hoe deze zijn geconfigureerd in de sjabloon.
   
    ![](./media/app-service-agile-software-development/production-3-resource-group-view.png)

U hebt nu de productie-omgeving instellen. Vervolgens wordt u een nieuwe update om de toepassing te starten.

## <a name="create-dev-and-test-branches"></a>Dev maken en testen van vertakkingen
Nu dat u een complexe toepassing die wordt uitgevoerd in de productieomgeving in Azure hebt, brengt u een update aan uw toepassing in overeenstemming met flexibele methodologie. In deze sectie u maakt de ontwikkeling en testen vertakkingen die u moet de vereiste updates.

1. Maak eerst de testomgeving. Voer de volgende opdrachten voor het maken van de omgeving voor een nieuwe vertakking aangeroepen in uw sessie Git Shell **NewUpdate**. 
   
        git checkout -b NewUpdate
        git push origin NewUpdate 
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch NewUpdate
2. Wanneer u wordt gevraagd, typt u in de gewenste gebruikersnaam en het wachtwoord voor toegang tot de database. 
   
   Wanneer implementatie is voltooid, wordt het script start de toepassing in de browser en geeft u een beschrijvende geluid. U hebt nu een nieuwe vertakking met een eigen testomgeving. Neem even de tijd om te controleren van enkele zaken over deze testomgeving:
   
   * U kunt dit in een Azure-abonnement maken. Dit betekent dat de productie-omgeving kan afzonderlijk worden beheerd vanaf uw testomgeving.
   * Uw testomgeving wordt live in Azure uitgevoerd.
   * Uw testomgeving is identiek aan de productie-omgeving, met uitzondering van de staging-sleuven en de instellingen voor schalen. Weet u het omdat ze het enige verschil tussen ProdandStage.json en Dev.json.
   * U kunt uw testomgeving beheren in een eigen App Service-abonnement, met een andere prijs-laag (zoals **vrije**).
   * Verwijderen van deze testomgeving is net zo eenvoudig als het verwijderen van de resourcegroep. U leert hoe u dit doet [later](#delete).
3. Gaat u naar een vertakking dev maken met de volgende opdrachten:
   
        git checkout -b Dev
        git push origin Dev
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch Dev
4. Wanneer u wordt gevraagd, typt u in de gewenste gebruikersnaam en het wachtwoord voor toegang tot de database. 
   
   Neem even de tijd om te controleren van enkele zaken over deze dev-omgeving: 
   
   * Uw omgeving dev heeft een configuratie die identiek is aan de testomgeving omdat het wordt geïmplementeerd met behulp van dezelfde sjabloon.
   * Elke dev-omgeving kan worden gemaakt in de ontwikkelaar eigen Azure-abonnement als u de testomgeving worden afzonderlijk beheerd.
   * Uw omgeving dev wordt live in Azure uitgevoerd.
   * Verwijderen van de dev-omgeving is net zo eenvoudig als het verwijderen van de resourcegroep. U leert hoe u dit doet [later](#delete).

> [!NOTE]
> Wanneer u meerdere ontwikkelaars die werken op de nieuwe update hebt, kunt elk van deze eenvoudig een vertakking en speciale dev-omgeving maken met de volgende stappen uit:
> 
> 1. Maken van hun eigen fork van de opslagplaats in GitHub (Zie [een opslagplaats vertakken](https://help.github.com/articles/fork-a-repo/)).
> 2. Kloon de fork op hun lokale computer
> 3. Voer de dezelfde opdrachten om hun eigen dev vertakking en de omgeving te maken.
> 
> 

Wanneer u bent klaar, moet uw GitHub-fork drie vertakkingen hebt:

![](./media/app-service-agile-software-development/test-1-github-view.png)

En moet u zes web-apps (drie sets van twee) hebben in drie afzonderlijke resourcegroepen:

![](./media/app-service-agile-software-development/test-2-all-webapps.png)

> [!NOTE]
> ProdandStage.json Hiermee geeft u de productieomgeving te gebruiken de **standaard** prijscategorie op geschikt is voor schaalbaarheid van de productietoepassing.
> 
> 

## <a name="build-and-test-every-commit"></a>Bouwen en testen van elke doorvoer
De sjabloonbestanden ProdAndStage.json en Dev.json opgeven al de parameters voor de bron, wat standaard stelt continue publiceren voor de web-app. Elke doorvoer naar de GitHub-vertakking activeert daarom een automatische implementatie naar Azure uit dat filiaal. Laten we zien hoe uw setup werkt nu.

1. Zorg ervoor dat u in de Dev-vertakking van de lokale opslagplaats. Voer hiertoe de volgende opdracht in de Git-Shell:
   
        git checkout Dev
2. Een wijziging aanbrengt aan de app UI laag door het wijzigen van de code [Bootstrap](http://getbootstrap.com/components/) bevat. Open  *&lt;repository_root >*\src\MultiChannelToDo.Web\index.cshtml en maak de volgende gemarkeerd wijzigen:
   
    ![](./media/app-service-agile-software-development/commit-1-changes.png)
   
    > [!NOTE]
    > Als u de voorgaande afbeelding kan niet lezen: 
    > 
    > * Wijzig in regel 18 `check-list` naar `list-group`.
    > * Wijzig in regel 19 `class="check-list-item"` naar `class="list-group-item"`.
    > 
    > 
3. Sla de wijziging. Terug in de Git-Shell, voer de volgende opdrachten:
   
        cd <repository_root>
        git add .
        git commit -m "changed to bootstrap style"
        git push origin Dev
   
   Deze git-opdrachten zijn vergelijkbaar met 'controleren in uw code' in een ander bronbeheersysteem zoals TFS. Bij het uitvoeren van `git push`, het nieuwe doorvoeren activeert een automatische code te pushen naar Azure, die vervolgens de toepassing wordt aan de wijziging in de dev-omgeving.
4. Om te controleren dat deze code te pushen naar uw omgeving dev heeft plaatsgevonden, gaat u naar de webpagina app uw Developer-omgeving en bekijk de **implementatie** onderdeel. U moet mogelijk uw meest recente commit-bericht te zien.
   
    ![](./media/app-service-agile-software-development/commit-2-deployed.png)
5. Van daaruit, klikt u op **Bladeren** voor een overzicht van nieuwe wijzigingen in de live-toepassing in Azure.
   
    ![](./media/app-service-agile-software-development/commit-3-webapp-in-browser.png)
   
   Het is een kleine wijziging in de toepassing. Veel tijden nieuwe wijzigingen aan een complexe webtoepassing wel onbedoelde en ongewenste neveneffecten. Kunnen eenvoudig elke doorvoer in live builds testen, kunt u deze problemen catch voordat ze uw klanten zien.

Nu moet u vertrouwd met de realisatie die als een ontwikkelaar van de **NewUpdate** project, kunt u een dev-omgeving maken voor uzelf, en vervolgens elke doorvoer bouwen en testen van elke build.

## <a name="merge-code-into-test-environment"></a>Code in de testomgeving samenvoegen
Wanneer u klaar bent om uw code vanuit Dev vertakking maximaal NewUpdate vertakking, is het proces standaard git:

1. Een nieuwe doorvoeracties naar NewUpdate samenvoegen met de vertakking Dev in GitHub, zoals doorvoeracties gemaakt door andere ontwikkelaars. Een nieuwe doorvoeren op GitHub triggers een code-push en bouwen in de dev-omgeving. U kunt er vervolgens voor zorgen dat uw code in Dev vertakking werkt nog altijd met de meest recente bits NewUpdate vertakken.
2. Uw nieuwe doorvoeracties Dev vertakken samenvoegen met NewUpdate vertakking op GitHub. Deze actie activeert een code-push en build in de testomgeving. 

Opmerking opnieuw dat omdat doorlopende implementatie is al ingesteld met deze vertakkingen git, u hoeft niet te doen andere lijkt op het uitvoeren van de integratie bouwt. U hoeft uit te voeren standaard bron besturingselement procedures met git en Azure voert alle processen van de build voor u.

Nu gaan we uw code push **NewUpdate** vertakking. Git-shell, voer de volgende opdrachten:

    git checkout NewUpdate
    git pull origin NewUpdate
    git merge Dev
    git push origin NewUpdate

Dat is alles. 

Ga naar de webpagina van de app voor uw testomgeving om te zien van uw nieuwe doorvoeren (NewUpdate vertakking samengevoegd) nu naar de testomgeving worden gepusht. Klik vervolgens op **Bladeren** om te zien dat de stijlwijziging die wordt nu uitgevoerd in Azure in.

## <a name="deploy-update-to-production"></a>Update implementeert naar productie
Code pushen naar de fasering en productie-omgeving moet u kunt niet anders dan wat u hebt al gedaan wanneer u code naar de testomgeving gepusht. Het is heel eenvoudig. 

Git-shell, voer de volgende opdrachten:

    git checkout master
    git pull origin master
    git merge NewUpdate
    git push origin master

Vergeet niet dat op basis van de manier waarop de fasering en productie-omgeving in ProdandStage.json is ingesteld, wordt doorgeschoven, is je nieuwe code aan de **fasering** sleuf en er wordt uitgevoerd. Dus als u naar de faseringssleuf URL navigeert, u de nieuwe code er uitgevoerd ziet. Voer hiervoor de volgende cmdlet in de Git-Shell.

    Start-Process -FilePath "http://ToDoApp<unique_string>master-Staging.azurewebsites.net"

En nu, nadat u hebt geverifieerd dat de update in de faseringssleuf, het enige dat links om te doen vervangt in productie. Git-shell, voert de volgende opdrachten:

    cd <repository_root>\ARMTemplates
    .\swap.ps1 -Name ToDoApp<unique_string>master

Gefeliciteerd. U hebt een nieuwe update heeft gepubliceerd naar uw productie-webtoepassing. Sterker nog is die dit gedaan met eenvoudig dev- en testomgevingen, maken en bouwen en testen van elke doorvoer. Dit zijn essentieel bouwstenen voor ontwikkeling van flexibele software.

<a name="delete"></a>

## <a name="delete-dev-and-test-environments"></a>Dev verwijderen en omgevingen testen
Omdat u opzettelijk uw dev- en testomgevingen om onafhankelijke resourcegroepen hebt ontworpen, is het eenvoudig om ze te verwijderen. Als u wilt verwijderen die u hebt gemaakt in deze zelfstudie, de GitHub-vertakkingen en de Azure-artefacten, voert de volgende opdrachten in de Git-Shell:

    git branch -d Dev
    git push origin :Dev
    git branch -d NewUpdate
    git push origin :NewUpdate
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>dev-group -Force -Verbose
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>newupdate-group -Force -Verbose

## <a name="summary"></a>Samenvatting
Flexibele software development is een moet zijn voor veel bedrijven willen vast te stellen Azure als het toepassingsplatform van hun. In deze zelfstudie hebt u geleerd maken en trek omlaag exacte replica's of in de buurt van replica's van de productie-omgeving met gemak, zelfs voor complexe toepassingen. U hebt ook geleerd hoe u deze mogelijkheid te maken van een ontwikkelingsproces die kan bouwen en testen van elke één doorvoer in Azure. Deze zelfstudie ideale geval leert u hoe u best kunt Azure App Service en Azure Resource Manager samen een DevOps-oplossing die caters om flexibele methoden te maken. Vervolgens kunt u in dit scenario door het uitvoeren van geavanceerde DevOps technieken zoals [testen in productie](app-service-web-test-in-production-get-start.md). Zie voor een algemeen scenario voor het testen in productie [Flighting implementatie (bètaversie testen) in Azure App Service](app-service-web-test-in-production-controlled-test-flight.md).

## <a name="more-resources"></a>Meer bronnen
* [Een complexe toepassing zoals verwacht in Azure implementeren](app-service-deploy-complex-application-predictably.md)
* [Flexibel ontwikkelen in de praktijk: Tips en trucs voor gemoderniseerde ontwikkelingscyclus](http://channel9.msdn.com/Events/Ignite/2015/BRK3707)
* [Geavanceerde implementatie van strategieën voor Web-Apps van Azure Resource Manager-sjablonen](http://channel9.msdn.com/Events/Build/2015/2-620)
* [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint - de validatiefunctie JSON](http://jsonlint.com/)
* [ARMClient – ingesteld GitHub publiceren naar site](https://github.com/projectKudu/ARMClient/wiki/Setup-GitHub-publishing-to-Site)
* [GIT vertakking – basis vertakking en samenvoegen](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [David Ebbo van Blog](http://blog.davidebbo.com/)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure platformoverschrijdende-opdrachtregelprogramma 's](../cli-install-nodejs.md)
* [Gebruikers maken of bewerken in Azure AD](https://msdn.microsoft.com/library/azure/hh967632.aspx#BKMK_1)
* [Project Kudu Wiki](https://github.com/projectkudu/kudu/wiki)

