---
title: Continue levering met Visual Studio Team Services in Azure | Microsoft Docs
description: Informatie over het configureren van uw Visual Studio Team Services teamprojecten om automatisch te bouwen en implementeren voor de functie Web-App in Azure App Service- of cloud-services.
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 797f67ad-e4d4-4063-ae91-41cbdf154191
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: d80ce63eb7ddfd7c45726be887a772f9a7594b28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services"></a>Onafgebroken levering naar Azure met Visual Studio Team Services
U kunt uw teamprojecten Visual Studio Team Services om automatisch te bouwen en implementeren voor Azure-web-apps of cloudservices configureren.  (Voor meer informatie over het instellen van een doorlopende build en implementeren met behulp van system een *lokale* Team Foundation Server Zie [continue leveringsmethode voor Cloud-Services in Azure](cloud-services-dotnet-continuous-delivery.md).)

Deze zelfstudie wordt ervan uitgegaan dat u hebt Visual Studio 2013 en de Azure-SDK geïnstalleerd. Als u nog geen Visual Studio 2013 hebt, downloadt u dit door het kiezen van de **gratis aan de slag** koppeling [www.visualstudio.com](http://www.visualstudio.com). Installeer de Azure-SDK van [hier](http://go.microsoft.com/fwlink/?LinkId=239540).

> [!NOTE]
> U moet een Visual Studio Team Services-account om deze zelfstudie te voltooien: U kunt [gratis een Visual Studio Team Services-account openen](http://go.microsoft.com/fwlink/p/?LinkId=512979).
> 
> 

Voer de volgende stappen uit voordat u een cloudservice om automatisch te bouwen en implementeren in Azure met behulp van Visual Studio Team Services kunt instellen.

## <a name="1-create-a-team-project"></a>1: een teamproject maken
Volg de instructies [hier](http://go.microsoft.com/fwlink/?LinkId=512980) uw teamproject maken en koppelen aan Visual Studio. In dit scenario wordt ervan uitgegaan dat u Team Foundation versie besturingselement (TFVC) gebruikt als oplossing voor uw gegevensbron. Als u wilt met Git voor versiebeheer, Zie [de Git-versie van deze rondleiding](http://go.microsoft.com/fwlink/p/?LinkId=397358).

## <a name="2-check-in-a-project-to-source-control"></a>2: een project met resourcebeheer inchecken
1. In Visual Studio, opent u de oplossing die u wilt implementeren of een nieuwe maken.
   De stappen in dit scenario kunt u een web-app of een service in de cloud (Azure-toepassing) implementeren.
   Als u maken van een nieuwe oplossing wilt, maakt u een nieuw Azure Cloud Service-project of een nieuw ASP.NET MVC-project. Zorg ervoor dat het project gericht is op .NET Framework 4 of 4.5, en als u een cloudserviceproject maakt, een ASP.NET MVC-Webrol en een werkrol toevoegen en kiest u Internet-toepassing voor de Webrol. Als u wordt gevraagd, kiest u **internettoepassing**.
   Als u maken van een web-app wilt, kiest de ASP.NET-webtoepassing projectsjabloon, maken en kies vervolgens MVC. Zie [een ASP.NET-web-app maken in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).
   
   > [!NOTE]
   > Visual Studio Team Services ondersteunen alleen CI-implementaties van Visual Studio-webtoepassingen op dit moment. Website-projecten vallen buiten het bereik.
   > 
   > 
2. Open het snelmenu voor de oplossing en kies **oplossing toevoegen aan bronbeheer**.
   
    ![][5]
3. Accepteer of wijzig de standaardinstellingen en klik op de **OK** knop. Zodra het proces is voltooid, bron besturingselement pictogrammen worden weergegeven in **Solution Explorer**.
   
    ![][6]
4. Open het snelmenu voor de oplossing en kies **inchecken**.
   
    ![][7]
5. In de **wijzigingen in behandeling** gebied van **Team Explorer**, typ een opmerking voor het inchecken en kiest u de **inchecken** knop.
   
    ![][8]
   
    Noteer de opties die u wilt opnemen of uitsluiten van specifieke wijzigingen wanneer u incheckt. Indien gewenst wijzigingen zijn uitgesloten, kies de **omvatten alle** koppeling.
   
    ![][9]

## <a name="3-connect-the-project-to-azure"></a>3: verbinding maken met het project naar Azure
1. Nu dat u een teamproject tegenover Team Services met sommige broncode erin hebt, bent u klaar uw teamproject verbinding te maken met Azure.  In de [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885), selecteer uw cloud-service of web-app of een nieuwe maken door het kiezen van de  **+**  pictogram naar links en te kiezen onder **Cloudservice**of **Web-App** en vervolgens **snelle invoer**. Kies de **publiceren met Visual Studio Team Services instellen** koppeling.
   
    ![][10]
2. In de wizard, typ de naam van uw Visual Studio Team Services-account in het tekstvak en klik op de **autoriseren nu** koppeling. U wordt mogelijk gevraagd aan te melden.
   
    ![][11]
3. In de **verbindingsaanvraag** pop-upvenster, kies de **accepteren** knop voor het autoriseren van Azure uw teamproject in VS-Team Services configureren.
   
    ![][12]
4. Als de autorisatie is geslaagd, ziet u een vervolgkeuzelijst met een lijst met uw teamprojecten Visual Studio Team Services. Kies de naam van teamproject dat u in de vorige stappen hebt gemaakt en kies vervolgens de wizard vinkje knop.
   
    ![][13]
5. Nadat uw project is gekoppeld, ziet u enkele instructies voor het controleren van wijzigingen aan uw project Visual Studio Team Services-team.  Bij de volgende controle, Visual Studio Team Services bouwt en uw project implementeren in Azure.  Probeer deze nu door te klikken op de **inchecken vanuit Visual Studio** koppeling, en vervolgens de **Visual Studio starten** koppeling (of een vergelijkbare **Visual Studio** knop aan de onderkant van de Portal scherm).
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4: de tabel opnieuw activeren en implementeren van uw project
1. In Visual Studio **Team Explorer**, kies de **Source Control Explorer** koppeling.
   
    ![][15]
2. Ga naar uw oplossingsbestand en open het.
   
    ![][16]
3. In **Solution Explorer**, opent u een bestand en deze te wijzigen. Wijzig bijvoorbeeld het bestand `_Layout.cshtml` onder de weergaven\\gedeelde map in een MVC-Webrol.
   
    ![][17]
4. Het logo voor de site bewerken en kies **Ctrl + S** het bestand wilt opslaan.
   
    ![][18]
5. In **Team Explorer**, kies de **wijzigingen in behandeling** koppeling.
   
    ![][19]
6. Voer een opmerking en kies vervolgens de **inchecken** knop.
   
    ![][20]
7. Kies de **thuis** terug te keren naar de **Team Explorer** startpagina.
   
    ![][21]
8. Kies de **Builds** koppeling om de opbouw in voortgang weer te geven.
   
    ![][22]
   
    **In een team Explorer** ziet u dat een build voor uw inchecken is geactiveerd.
   
    ![][23]
9. Dubbelklik op de naam van de build uitgevoerd om een gedetailleerde logboekbestanden tijdens de voortgang van de build weer te geven.
   
    ![][24]
10. Hoewel de build in voortgang, bekijk de build-definitie die is gemaakt toen u TFS gekoppeld aan Azure met behulp van de wizard.  Open het snelmenu voor de definitie van de build en kies **bouwen definitie bewerken**.
    
     ![][25]
    
     In de **Trigger** tabblad ziet u dat de build-definitie is standaard ingesteld op voor elke inchecken bouwen.
    
     ![][26]
    
     In de **proces** tabblad ziet u de implementatieomgeving is ingesteld op de naam van uw cloud-service of web-app. Als u met web-apps werkt, niet de eigenschappen die u ziet verschillen van die hier wordt weergegeven.
    
     ![][27]
11. Geef waarden voor de eigenschappen als u wilt dat andere waarden dan de standaardwaarden. De eigenschappen voor Azure publicatie zijn de **implementatie** sectie.
    
     De volgende tabel bevat de beschikbare eigenschappen in de **implementatie** sectie:
    
    | Eigenschap | Standaardwaarde |
    | --- | --- |
    | Niet-vertrouwde certificaten toestaan |Als het ONWAAR is, moeten de SSL-certificaten zijn ondertekend door een basisinstantie. |
    | Upgrade toestaan |Hiermee kunt de implementatie bijwerken van een bestaande implementatie in plaats van een nieuwe maken. Het IP-adres, blijft behouden. |
    | Niet verwijderen |Indien waar, de implementatie van een bestaande niet-verwante niet overschrijven (upgrade is toegestaan). |
    | Pad naar de implementatie-instellingen |Het pad naar het bestand .pubxml voor een web-app, ten opzichte van de hoofdmap van de opslagplaats. Genegeerd voor cloud-services. |
    | SharePoint-omgeving voor implementatie |Hetzelfde als de naam van de service. |
    | Azure-implementatie-omgeving |De web-app of cloud servicenaam. |
12. Als u meerdere-configuraties (.cscfg-bestanden) gebruikt, kunt u de configuratie van de gewenste service in de **bouwen, Geavanceerd MSBuild-argumenten** instelling. Bijvoorbeeld, voor het gebruik van ServiceConfiguration.Test.cscfg ingesteld MSBuild-argumenten regeloptie `/p:TargetProfile=Test`.
    
     ![][38]
    
     Op dit tijdstip moet uw build worden voltooid.
    
     ![][28]
13. Als u dubbelklikt op de naam van de build, ziet u Visual Studio een **bouwen samenvatting**, met inbegrip van de testresultaten van eenheid Testprojecten die is gekoppeld.
    
     ![][29]
14. In de [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885), kunt u de gekoppelde implementatie bekijken op de **implementaties** tabblad wanneer de faseringsomgeving is geselecteerd.
    
     ![][30]
15. Blader naar de URL van uw site. Voor een web-app, klik op de **Bladeren** knop op de opdrachtbalk. Voor een cloudservice, kiest u de URL in de **snel in één oogopslag** sectie van de **Dashboard** pagina waarin de faseringsomgeving voor een cloudservice. Implementaties van continue integratie voor cloud-services worden gepubliceerd op de faseringsomgeving standaard. U kunt dit wijzigen door in te stellen de **alternatieve Cloudserviceomgeving** eigenschap **productie**. Deze schermafbeelding ziet waar de URL van de site is op de dashboardpagina van de cloudservice.
    
    ![][31]
    
    Een nieuw browsertabblad geopend om uw actieve site weer te geven.
    
    ![][32]
    
    Cloud-services, als u andere wijzigingen aan uw project aanbrengt, u trigger builds meer en wordt u meerdere implementaties verzamelt. Het recentste is gemarkeerd als actief.
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5: een eerdere build implementeren
Deze stap geldt voor cloudservices en is optioneel. In de klassieke Azure portal, kiest u een eerdere implementatie en kies vervolgens de **implementeren** knop terugspoelen van uw site een eerdere in te checken.  Houd er rekening mee dat dit een nieuwe build in TFS activeren en maken van een nieuwe vermelding in de geschiedenis van uw implementatie.

![][34]

## <a name="6-change-the-production-deployment"></a>6: de productie-implementatie wijzigen
Deze stap geldt alleen voor cloud-services, niet-web-apps. Wanneer u klaar bent, kunt u de faseringsomgeving naar de productieomgeving promoveren kiezen de **wisselen** knop in de klassieke Azure portal. De zojuist geïmplementeerde faseringsomgeving wordt gepromoveerd voor productie en de vorige productie-omgeving, indien aanwezig, wordt een Staging-omgeving. De actieve implementatie mogelijk anders voor de productie- en Faseringsomgevingen, maar de geschiedenis van de implementatie van recente builds is hetzelfde, ongeacht de omgeving.

![][35]

## <a name="7-run-unit-tests"></a>7: eenheidstests uitvoeren
Deze stap geldt alleen voor web-apps, niet cloudservices. Als u een quality-gate voor uw implementatie, kunt u eenheidstests uitvoeren en als ze mislukken, kunt u de implementatie stoppen.

1. Voeg een eenheid test-project in Visual Studio.
   
   ![][39]
2. Projectverwijzingen toevoegen aan het project dat u wilt testen.
   
   ![][40]
3. Sommige eenheidstests toevoegen. Probeer een dummy-test die altijd wordt doorgegeven aan de slag.
   
       ```
       using System;
       using Microsoft.VisualStudio.TestTools.UnitTesting;
   
       namespace UnitTestProject1
       {
           [TestClass]
           public class UnitTest1
           {
               [TestMethod]
               [ExpectedException(typeof(NotImplementedException))]
               public void TestMethod1()
               {
                   throw new NotImplementedException();
               }
           }
       }
       ```
4. Bewerk de build-definitie, kiest u de **proces** tabblad uit en vouw de **Test** knooppunt.
5. Stel de **mislukken build voor testfout** op True. Dit betekent dat de implementatie zich niet tenzij de tests zijn geslaagd.
   
   ![][41]
6. Een nieuwe build wachtrij.
   
   ![][42]
   
   ![][43]
7. Terwijl de build nadert, informatie over de voortgang bekijken.
   
    ![][44]
   
    ![][45]
8. Wanneer de build is voltooid, controleert u de testresultaten.
   
    ![][46]
   
    ![][47]
9. Maak een test die mislukt. Een nieuwe test toevoegen door te kopiëren van het eerste beheerpunt, wijzigt u de naam en de coderegel waarin wordt vermeld dat notimplementedexception is een verwachte uitzondering uitcommentariëren.
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. Controleer in de wijziging in de wachtrij een nieuwe build.
    
     ![][48]
11. Bekijk de testresultaten voor details over de fout.
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over eenheid testen in Visual Studio Team Services, [eenheidstests uitvoeren in uw build](http://go.microsoft.com/fwlink/p/?LinkId=510474). Als u Git, Zie [delen van uw code in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) en [continue implementatie naar Azure App Service](../app-service-web/app-service-continuous-deployment.md).  Zie voor meer informatie over Visual Studio Team Services, [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso/tfs1.png
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png

[5]: ./media/cloud-services-continuous-delivery-use-vso/tfs5.png
[6]: ./media/cloud-services-continuous-delivery-use-vso/tfs6.png
[7]: ./media/cloud-services-continuous-delivery-use-vso/tfs7.png
[8]: ./media/cloud-services-continuous-delivery-use-vso/tfs8.png
[9]: ./media/cloud-services-continuous-delivery-use-vso/tfs9.png
[10]: ./media/cloud-services-continuous-delivery-use-vso/tfs10.png
[11]: ./media/cloud-services-continuous-delivery-use-vso/tfs11.png
[12]: ./media/cloud-services-continuous-delivery-use-vso/tfs12.png
[13]: ./media/cloud-services-continuous-delivery-use-vso/tfs13.png
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso/tfs18.png
[19]: ./media/cloud-services-continuous-delivery-use-vso/tfs19.png
[20]: ./media/cloud-services-continuous-delivery-use-vso/tfs20.png
[21]: ./media/cloud-services-continuous-delivery-use-vso/tfs21.png
[22]: ./media/cloud-services-continuous-delivery-use-vso/tfs22.png
[23]: ./media/cloud-services-continuous-delivery-use-vso/tfs23.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso/tfs27.png
[28]: ./media/cloud-services-continuous-delivery-use-vso/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso/tfs37.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso/AdvancedMSBuildSettings.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso/AddUnitTestProject.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso/AddProjectReferences.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso/EditBuildDefinitionForTest.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso/QueueNewBuild.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso/QueueBuildDialog.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso/BuildInTeamExplorer.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso/BuildRequestInfo.PNG
[46]: ./media/cloud-services-continuous-delivery-use-vso/BuildSucceeded.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso/TestResultsPassed.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso/CheckInChangeToMakeTestsFail.PNG
[49]: ./media/cloud-services-continuous-delivery-use-vso/TestsFailed.PNG
[50]: ./media/cloud-services-continuous-delivery-use-vso/TestsResultsFailed.PNG
