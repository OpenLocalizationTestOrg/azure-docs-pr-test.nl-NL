---
title: een CI/CD-pijplijn in Azure met Team Services aaaCreate | Microsoft Docs
description: "Meer informatie over hoe een Visual Studio Team Services toocreate pijplijn voor continue integratie en aflevering waarmee een tooIIS web-app op een Windows-virtuele machine wordt geïmplementeerd"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: b758a124c4742854dd3b543f747fd8700f954414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-continuous-integration-pipeline-with-visual-studio-team-services-and-iis"></a>Een continue integratie-pijplijn maken met Visual Studio Team Services en IIS
tooautomate hello build, test en fasen van de implementatie van de ontwikkeling van toepassingen, kunt u een continue integratie en implementatie (CI/CD) pijplijn. In deze zelfstudie maakt u een CI/CD-pijplijn met Visual Studio Team Services en virtuele Windows-machine (VM) in Azure waarop IIS wordt uitgevoerd. Procedures voor:

> [!div class="checklist"]
> * Een ASP.NET-toepassing tooa Team Services webproject publiceren
> * Een build-definitie die wordt geactiveerd door doorvoeracties code maken
> * IIS installeren en configureren op een virtuele machine in Azure
> * Hallo IIS tooa implementatie instantiegroep in Team Services toevoegen
> * Maak een nieuwe website voor release definitie toopublish pakketten tooIIS implementeren
> * Test Hallo CI/CD-pipeline

Deze zelfstudie vereist hello Azure PowerShell-moduleversie 3,6 of hoger. Voer `Get-Module -ListAvailable AzureRM` toofind Hallo versie. Als u tooupgrade moet, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).


## <a name="create-project-in-team-services"></a>Project maken in een Team Services
Visual Studio Team Services kunt u eenvoudig samenwerking en ontwikkeling zonder het onderhouden van een on-premises-oplossing voor het beheer van code. Teamservices biedt cloud code testen, build en application insights. U kunt een besturingselement-repo-versie en IDE die het beste past bij de ontwikkeling van uw code. Voor deze zelfstudie kunt u een gratis account toocreate een eenvoudige ASP.NET-web-app en CI/CD-pijplijn. Als u nog geen een Team Services-account [maken van een](http://go.microsoft.com/fwlink/?LinkId=307137).

toomanage hello code commit proces definities, bouwen en definities release, in een project maakt Team Services als volgt:

1. Open uw dashboard Team Services in een webbrowser en kies **nieuw project**.
2. Voer *myWebApp* voor Hallo **projectnaam**. Andere toouse voor de waarden standaard laat *Git* versiebeheer en *Agile* proces werkitem.
3. Hallo-optie te kiezen**delen met** *teamleden*, selecteer daarna **maken**.
5. Wanneer uw project is gemaakt, kiest u Hallo optie te**initialiseren met een Leesmij-bestand of gitignore**, klikt u vervolgens **initialiseren**.
6. Kies in het nieuwe project **Dashboards** aan de bovenkant hello, selecteer **openen in Visual Studio**.


## <a name="create-aspnet-web-application"></a>ASP.NET-webtoepassing maken
In de vorige stap hello, moet u een project in Team Services gemaakt. de laatste stap Hallo Hiermee opent u het nieuwe project in Visual Studio. Beheren van uw code doorvoeringen in Hallo **Team Explorer** venster. Maken van een lokale kopie van het nieuwe project en maak vervolgens een ASP.NET-webtoepassing vanuit een sjabloon als volgt:

1. Selecteer **kloon** toocreate een lokale git-opslagplaats van uw Team Services-project.
    
    ![De opslagplaats klonen uit Team Services-project](media/tutorial-vsts-iis-cicd/clone_repo.png)

2. Onder **oplossingen**, selecteer **nieuw**.

    ![Oplossing voor webtoepassing maken](media/tutorial-vsts-iis-cicd/new_solution.png)

3. Selecteer **Web** sjablonen, en kies vervolgens Hallo **ASP.NET-webtoepassing** sjabloon.
    1. Voer een naam voor uw toepassing, zoals *myWebApp*, en schakel Hallo selectievakje uit voor **map voor oplossing maken**.
    2. Als het Hallo-optie beschikbaar is, schakelt u Hallo vak te**Application Insights toevoegen tooproject**. Application Insights vereist tooauthorize u uw webtoepassing met Azure Application Insights. tookeep het eenvoudig is in deze zelfstudie dit proces overslaan.
    3. Selecteer **OK**.
4. Kies **MVC** in lijst Hallo-sjabloon.
    1. Selecteer **verificatie wijzigen**, kies **geen verificatie**, selecteer daarna **OK**.
    2. Selecteer **OK** toocreate uw oplossing.
5. In Hallo **Team Explorer** venster kiezen **wijzigingen**.

    ![Lokale wijzigingen tooTeam Services git-opslagplaats doorvoeren](media/tutorial-vsts-iis-cicd/commit_changes.png)

6. Voer in het tekstvak Hallo doorvoeren, een bericht zoals *initiële doorvoeren*. Kies **alle doorvoeren en Sync** uit de vervolgkeuzelijst Hallo.


## <a name="create-build-definition"></a>Build-definitie maken
In het Team Services gebruikt u een build definitie toooutline hoe uw toepassing moet worden samengesteld. In deze zelfstudie maken we een basisdefinitie dat vergt onze broncode Hallo oplossing bouwt en maakt vervolgens web pakket gebruiken we toorun Hallo web-app op een IIS-server implementeren.

1. Kies in het project Team Services **bouwen & Release** aan de bovenkant hello, selecteer **Builds**.
3. Selecteer **+ nieuwe definitie**.
4. Kies Hallo **ASP.NET (PREVIEW)** sjabloon en selecteer **toepassen**.
5. Laat alle Hallo standaard waarden van de taak. Onder **bronnen ophalen**, zorg ervoor dat Hallo *myWebApp* opslagplaats en *master* vertakking worden geselecteerd.

    ![Definitie van de build in Team Services-project maken](media/tutorial-vsts-iis-cicd/create_build_definition.png)

6. Op Hallo **Triggers** tabblad, verplaats de schuifregelaar Hallo voor **inschakelen van deze trigger** te*ingeschakeld*.
7. Hallo build definitie en wachtrij een nieuwe build opslaan door **opslaan en wachtrij** , klikt u vervolgens **opslaan en wachtrij** opnieuw. Hallo standaardinstellingen laten staan en selecteer **wachtrij**.

Bekijk begint zoals Hallo build is gepland op een gehoste agent vervolgens toobuild. Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:

![Geslaagde build van het Team Services-project](media/tutorial-vsts-iis-cicd/successful_build.png)


## <a name="create-virtual-machine"></a>Virtuele machine maken
een platform toorun tooprovide uw ASP.NET-web-app, moet u een virtuele Windows-machine waarop IIS wordt uitgevoerd. Teamservices maakt gebruik van een agent toointeract met Hallo IIS-exemplaar als u code doorvoert en builds worden geactiveerd.

Maak een VM van Windows Server 2016 met [dit voorbeeldscript](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json). Het duurt enkele minuten voor Hallo script toorun en Hallo VM maken. Zodra het Hallo VM is gemaakt, opent u poort 80 voor internetverkeer met [toevoegen AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) als volgt:

```powershell
Get-AzureRmNetworkSecurityGroup `
  -ResourceGroupName $resourceGroup `
  -Name "myNetworkSecurityGroup" | `
Add-AzureRmNetworkSecurityRuleConfig `
  -Name "myNetworkSecurityGroupRuleWeb" `
  -Protocol "Tcp" `
  -Direction "Inbound" `
  -Priority "1001" `
  -SourceAddressPrefix "*" `
  -SourcePortRange "*" `
  -DestinationAddressPrefix "*" `
  -DestinationPortRange "80" `
  -Access "Allow" | `
Set-AzureRmNetworkSecurityGroup
```

tooconnect tooyour VM, verkrijgen Hallo openbare IP-adres met [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) als volgt:

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName $resourceGroup | Select IpAddress
```

Een extern bureaublad-sessiehost tooyour VM maken:

```cmd
mstsc /v:<publicIpAddress>
```

Open op Hallo VM, een **beheerder PowerShell** opdrachtprompt. IIS en de vereiste .NET-functies als volgt installeren:

```powershell
Install-WindowsFeature Web-Server,Web-Asp-Net45,NET-Framework-Features
```


## <a name="create-deployment-group"></a>Implementatiegroep maken
toopush uit Hallo web pakket toohello IIS-server implementeren, het definiëren van een implementatiegroep in een Team Services. Deze groep kunt u toospecify welke servers Hallo doel van de nieuwe builds worden als het doorvoeren van code tooTeam Services en builds zijn voltooid.

1. Kies in het Team Services, **bouwen & Release** en selecteer vervolgens **implementatiegroepen**.
2. Kies **implementatie toevoegen groep**.
3. Voer een naam voor de groep hello, zoals *myIIS*, selecteer daarna **maken**.
4. In Hallo **machines registreren** sectie, moet u zorgen *Windows* is ingeschakeld, wordt het selectievakje hello te**een persoonlijk toegangstoken in Hallo script gebruiken voor verificatie**.
5. Selecteer **tooclipboard script kopiëren**.


### <a name="add-iis-vm-toohello-deployment-group"></a>IIS VM toohello implementatiegroep toevoegen
Elke groep van IIS-exemplaar toohello Hallo implementatie-groep is gemaakt, toevoegen. Teamservices genereert een script dat downloadt en configureert u een agent op Hallo implementeren van virtuele machine die u ontvangt van de nieuwe web-pakketten en vervolgens tooIIS wordt toegepast.

1. Terug in Hallo **beheerder PowerShell** sessie op de virtuele machine, plakken en opgehaald uit het Team Services Hallo-script uitvoeren.
2. Wanneer de vraag tooconfigure labels voor Hallo-agent, optie *Y* en voer *web*.
3. Wanneer u wordt gevraagd voor het gebruikersaccount hello, drukt u op *retourneren* tooaccept Hallo standaardwaarden.
4. Wachten op Hallo script toofinish met een bericht *vstsagent.account.computername Service is gestart*.
5. In Hallo **implementatiegroepen** pagina Hallo **bouwen & Release** menu, open Hallo *myIIS* implementatiegroep. Op Hallo **Machines** tabblad, controleert u of uw virtuele machine wordt weergegeven.

    ![Virtuele machine toegevoegd tooTeam Services implementatiegroep](media/tutorial-vsts-iis-cicd/deployment_group.png)


## <a name="create-release-definition"></a>Release-definitie maken
toopublish uw builds u de definitie van een release maken in een Team Services. Deze definitie wordt automatisch geactiveerd door een geslaagde build van uw toepassing. U kiest Hallo implementatie groep toopush uw web-pakket te implementeren en de juiste IIS-instellingen Hallo definiëren.

1. Kies **bouwen & Release**, selecteer daarna **Builds**. Kies Hallo build definitie die is gemaakt in de vorige stap.
2. Onder **onlangs voltooid**, kies de meest recente build hello, en selecteer **Release**.
3. Kies **Ja** toocreate een release-definitie.
4. Kies Hallo **leeg** sjabloon, selecteer vervolgens **volgende**.
5. Controleer of het Hallo-project en de brontabel build-definitie zijn gevuld met uw project.
6. Selecteer Hallo **continue implementatie** in en selecteer **maken**.
7. Selecteer de vervolgkeuzelijst Hallo naast te**+ taken toevoegen** en kies *toevoegen van een groep implementatiefase*.
    
    ![Toorelease taakdefinitie in Team Services toevoegen](media/tutorial-vsts-iis-cicd/add_release_task.png)

8. Kies **toevoegen** volgende te**IIS Web-App Deploy(Preview)**, selecteer daarna **sluiten**.
9. Selecteer Hallo **uitvoeren op implementatiegroep** bovenliggende taak.
    1. Voor **Implementatiegroep**, selecteer Hallo implementatie groep die u hebt gemaakt uit eerder, zoals *myIIS*.
    2. In Hallo **Machine labels** de optie **toevoegen** en kies Hallo *web* label.
    
    ![De definitie van implementatie groepstaak vrijgeven voor IIS](media/tutorial-vsts-iis-cicd/release_definition_iis.png)
 
11. Selecteer Hallo **implementeren: IIS Web-App implementeren** taak tooconfigure uw IIS-instantie instellingen als volgt:
    1. Voor **Websitenaam**, voer *standaardwebsite*.
    2. Laat alle Hallo andere standaardinstellingen.
12. Kies **opslaan**, selecteer daarna **OK** twee keer.


## <a name="create-a-release-and-publish"></a>Een releaserecord maken en publiceren
U kunt nu uw web-push pakket als een nieuwe release implementeren. Deze stap communiceert met de Hallo-agent op elke instantie die deel uitmaakt van de implementatiegroep hello, pushes Hallo web pakket implementeren en vervolgens configureert u IIS-webtoepassing voor toorun Hallo bijgewerkt.

1. Selecteer in de definitie van de release **+ Release**, en kies vervolgens **maken Release**.
2. Controleer of de laatste build Hallo is geselecteerd in de vervolgkeuzelijst hello, samen met **geautomatiseerde implementatie: na het maken van de release**. Selecteer **Maken**.
3. Een kleine weergegeven dat aan de bovenkant Hallo van de definitie van de release, zoals *Release Release-1 is aangemaakt*. Selecteer Hallo release-koppeling.
4. Open Hallo **logboeken** tabblad toowatch Hallo release uitgevoerd.
    
    ![Geslaagde teamservices release en web implementeren push pakket](media/tutorial-vsts-iis-cicd/successful_release.png)

5. Nadat het Hallo-release is voltooid, open een webbrowser en Voer Hallo openbare IPP-adres van uw virtuele machine. Uw ASP.NET-webtoepassing wordt uitgevoerd.

    ![ASP.NET-web-app uitgevoerd op IIS VM](media/tutorial-vsts-iis-cicd/running_web_app.png)


## <a name="test-hello-whole-cicd-pipeline"></a>Test Hallo hele CI/CD-pipeline
Met uw webtoepassing die wordt uitgevoerd op IIS, probeer het nu Hallo hele CI/CD-pijplijn. Nadat u een wijziging aanbrengt in Visual Studio en doorvoeren uw code, een build wordt geactiveerd, die vervolgens een versie van uw web-bijgewerkte activeert, pakket tooIIS implementeren:

1. Open in Visual Studio Hallo **Solution Explorer** venster.
2. Navigeer tooand open *myWebApp | Weergaven | Start | Index.cshtml*
3. Regel 6 tooread bewerken:

    `<h1>ASP.NET with VSTS and CI/CD!</h1>`

4. Hallo-bestand opslaan.
5. Open Hallo **Team Explorer** venster, selecteer Hallo *myWebApp* project en kies vervolgens **wijzigingen**.
6. Voer een bericht doorvoeren, zoals *testen CI/CD-pijplijn*, en kies vervolgens **alle doorvoeren en Sync** uit de vervolgkeuzelijst Hallo.
7. In de werkruimte Team Services, wordt een nieuwe build van Hallo code commit geactiveerd. 
    - Kies **bouwen & Release**, selecteer daarna **Builds**. 
    - Kies de definitie van de build en selecteer vervolgens Hallo **in de wachtrij geplaatst & uitgevoerd** build toowatch als Hallo bouwen verloopt.
9. Wanneer Hallo build voltooid is, wordt een nieuwe release wordt geactiveerd.
    - Kies **bouwen & Release**, klikt u vervolgens **Releases** toosee hello webimplementatiepakket tooyour IIS VM gepusht. 
    - Selecteer Hallo **vernieuwen** pictogram tooupdate Hallo status. Wanneer Hallo *omgevingen* kolom ziet u een groen vinkje, Hallo release tooIIS is geïmplementeerd.
11. de wijzigingen toegepast, toosee, vernieuw uw IIS-website in een browser.

    ![ASP.NET-web-app uitgevoerd op IIS VM vanuit CI/CD-pipeline](media/tutorial-vsts-iis-cicd/running_web_app_cicd.png)


## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie maakt u een ASP.NET-webtoepassing hebt gemaakt in Team Services en geconfigureerde build en release definities toodeploy nieuwe web implementeert pakketten tooIIS op elke doorvoer code. U hebt geleerd hoe u:

> [!div class="checklist"]
> * Een ASP.NET-toepassing tooa Team Services webproject publiceren
> * Een build-definitie die wordt geactiveerd door doorvoeracties code maken
> * IIS installeren en configureren op een virtuele machine in Azure
> * Hallo IIS tooa implementatie instantiegroep in Team Services toevoegen
> * Maak een nieuwe website voor release definitie toopublish pakketten tooIIS implementeren
> * Test Hallo CI/CD-pipeline

Hoe gaan van de volgende zelfstudie toolearn toohello toosecure een webserver met SSL-certificaten.

> [!div class="nextstepaction"]
> [Webserver met SSL beveiligde](tutorial-secure-web-server.md)