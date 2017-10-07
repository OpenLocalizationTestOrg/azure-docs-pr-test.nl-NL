---
title: aaaContinuous levering met Visual Studio Team Services in Azure | Microsoft Docs
description: Meer informatie over hoe tooconfigure uw Visual Studio Team Services team projecten tooautomatically bouwen en implementeren van de functie van de toohello Web-App in Azure App Service- of cloud-services.
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
ms.openlocfilehash: eae75729e1c1a55f9bc3375604a8192f329d0042
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services"></a>Continue levering tooAzure met behulp van Visual Studio Team Services
U kunt uw Visual Studio Team Services team projecten tooautomatically build configureren en implementeren tooAzure web-apps of cloudservices.  (Voor meer informatie over hoe tooset-up maken van een doorlopende build en implementeren met behulp van system een *lokale* Team Foundation Server Zie [continue leveringsmethode voor Cloud-Services in Azure](cloud-services-dotnet-continuous-delivery.md).)

Deze zelfstudie wordt ervan uitgegaan dat u hebt Visual Studio 2013 en hello Azure SDK is geïnstalleerd. Als u nog geen Visual Studio 2013 hebt, downloadt u dit door te kiezen Hallo **gratis aan de slag** koppeling [www.visualstudio.com](http://www.visualstudio.com). Installeren Azure SDK Hallo [hier](http://go.microsoft.com/fwlink/?LinkId=239540).

> [!NOTE]
> U moet een toocomplete Visual Studio Team Services-account van deze zelfstudie: U kunt [gratis een Visual Studio Team Services-account openen](http://go.microsoft.com/fwlink/p/?LinkId=512979).
> 
> 

tooset van een cloud service tooautomatically bouwen en tooAzure implementeren met behulp van Visual Studio Team Services, als volgt te werk.

## <a name="1-create-a-team-project"></a>1: een teamproject maken
Volg de instructies Hallo [hier](http://go.microsoft.com/fwlink/?LinkId=512980) toocreate uw team project en een koppeling tooVisual Studio. In dit scenario wordt ervan uitgegaan dat u Team Foundation versie besturingselement (TFVC) gebruikt als oplossing voor uw gegevensbron. Als u toouse Git voor versiebeheer wilt, Zie [Hallo Git-versie van deze rondleiding](http://go.microsoft.com/fwlink/p/?LinkId=397358).

## <a name="2-check-in-a-project-toosource-control"></a>2: een project toosource besturingselement inchecken
1. Open in Visual Studio Hallo-oplossing u wilt dat toodeploy of maak een nieuwe.
   U kunt een web-app implementeren of een service in de cloud (Azure-toepassing) door de volgende Hallo stappen in dit scenario.
   Als u een nieuwe oplossing toocreate wilt, een nieuw Azure Cloud Service-project of een nieuwe ASP.NET MVC-project maken. Zorg ervoor dat Hallo project doelen .NET Framework 4 of 4.5, en als u een cloudserviceproject maakt een ASP.NET MVC-Webrol en een werkrol toevoegen en kies Internet-toepassing voor de Webrol Hallo. Als u wordt gevraagd, kiest u **internettoepassing**.
   Als u toocreate een web-app wilt, kies Hallo ASP.NET-webtoepassing projectsjabloon en kies vervolgens MVC. Zie [een ASP.NET-web-app maken in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).
   
   > [!NOTE]
   > Visual Studio Team Services ondersteunen alleen CI-implementaties van Visual Studio-webtoepassingen op dit moment. Website-projecten vallen buiten het bereik.
   > 
   > 
2. Open Hallo contextmenu voor Hallo oplossing en kies **oplossing toevoegen tooSource besturingselement**.
   
    ![][5]
3. Accepteer of Hallo standaardinstellingen wijzigen en klik op Hallo **OK** knop. Zodra het Hallo-proces is voltooid, bron besturingselement pictogrammen worden weergegeven in **Solution Explorer**.
   
    ![][6]
4. Open Hallo snelmenu voor Hallo oplossing en kies **inchecken**.
   
    ![][7]
5. In Hallo **wijzigingen in behandeling** gebied van **Team Explorer**en typ een opmerking bij inchecken Hallo Hallo kiezen **inchecken** knop.
   
    ![][8]
   
    Houd er rekening mee Hallo opties tooinclude of specifieke wijzigingen uitsluiten wanneer u incheckt. Indien gewenst wijzigingen zijn uitgesloten, kies Hallo **omvatten alle** koppeling.
   
    ![][9]

## <a name="3-connect-hello-project-tooazure"></a>3: verbinding maken met de Hallo project tooAzure
1. Nu dat u een teamproject tegenover Team Services met sommige broncode erin hebt, bent u klaar tooconnect uw team tooAzure project.  In Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885), selecteer uw cloud-service of web-app of een nieuwe maken door te kiezen Hallo  **+**  pictogram op Hallo linksonder en kiezen **Cloudservice** of **Web-App** en vervolgens **snelle invoer**. Kies Hallo **publiceren met Visual Studio Team Services instellen** koppeling.
   
    ![][10]
2. In de wizard Hallo Typ Hallo-naam van uw Visual Studio Team Services-account Hallo tekstvak en klik op Hallo **autoriseren nu** koppeling. U wordt mogelijk gevraagd toosign in.
   
    ![][11]
3. In Hallo **verbindingsaanvraag** pop-upvenster Hallo kiezen **accepteren** knop tooauthorize Azure tooconfigure uw team in VS-teamservices project.
   
    ![][12]
4. Als de autorisatie is geslaagd, ziet u een vervolgkeuzelijst met een lijst met uw teamprojecten Visual Studio Team Services. Kies de naam Hallo van teamproject dat u hebt gemaakt in de vorige stappen Hallo en kies vervolgens van de wizard Hallo vinkje knop.
   
    ![][13]
5. Nadat uw project is gekoppeld, ziet u enkele instructies voor het inchecken van wijzigingen tooyour Visual Studio Team Services teamproject.  Bij de volgende controle, Visual Studio Team Services bouwt en implementeren van uw project tooAzure.  Probeer deze nu door te klikken op Hallo **inchecken vanuit Visual Studio** koppelen en vervolgens Hallo **Visual Studio starten** koppeling (of gelijkwaardige Hallo **Visual Studio** knop Hallo onder aan portal welkomstscherm).
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4: de tabel opnieuw activeren en implementeren van uw project
1. In Visual Studio **Team Explorer**, kies Hallo **Source Control Explorer** koppeling.
   
    ![][15]
2. Navigeer tooyour oplossingsbestand en open het.
   
    ![][16]
3. In **Solution Explorer**, opent u een bestand en deze te wijzigen. Wijzig bijvoorbeeld Hallo bestand `_Layout.cshtml` onder Hallo weergaven\\gedeelde map in een MVC-Webrol.
   
    ![][17]
4. Hallo-logo voor Hallo site bewerken en kies **Ctrl + S** toosave Hallo-bestand.
   
    ![][18]
5. In **Team Explorer**, kies Hallo **wijzigingen in behandeling** koppeling.
   
    ![][19]
6. Voer een opmerking en kies vervolgens Hallo **inchecken** knop.
   
    ![][20]
7. Kies Hallo **thuis** knop tooreturn toohello **Team Explorer** startpagina.
   
    ![][21]
8. Kies Hallo **Builds** koppeling tooview Hallo builds uitgevoerd.
   
    ![][22]
   
    **In een team Explorer** ziet u dat een build voor uw inchecken is geactiveerd.
   
    ![][23]
9. Dubbelklik op Hallo van Hallo build in voortgang tooview een gedetailleerd logboek Hallo build loop.
   
    ![][24]
10. Hallo build is uitgevoerd, bekijk Hallo build definitie die is gemaakt toen u TFS tooAzure gekoppeld met behulp van de wizard Hallo.  Hallo snelmenu voor Hallo build definitie openen en kies **bouwen definitie bewerken**.
    
     ![][25]
    
     In Hallo **Trigger** tabblad ziet u dat Hallo build definitie is toobuild bij elke controle standaard ingesteld.
    
     ![][26]
    
     In Hallo **proces** tabblad ziet u de implementatieomgeving Hallo toohello naam van uw cloud-service of web-app is ingesteld. Als u met web-apps werkt, is er Hallo-eigenschappen worden afwijken van die hier wordt weergegeven.
    
     ![][27]
11. Geef waarden voor Hallo eigenschappen als u wilt dat andere waarden dan Hallo standaardwaarden. Hallo-eigenschappen voor Azure publicatie worden in Hallo **implementatie** sectie.
    
     Hallo volgende tabel bevat de beschikbare eigenschappen Hallo in Hallo **implementatie** sectie:
    
    | Eigenschap | Standaardwaarde |
    | --- | --- |
    | Niet-vertrouwde certificaten toestaan |Als het ONWAAR is, moeten de SSL-certificaten zijn ondertekend door een basisinstantie. |
    | Upgrade toestaan |Hiermee kunt Hallo implementatie tooupdate een bestaande implementatie in plaats van een nieuwe maken. Bewaart Hallo IP-adres. |
    | Niet verwijderen |Indien waar, de implementatie van een bestaande niet-verwante niet overschrijven (upgrade is toegestaan). |
    | Pad tooDeployment instellingen |Hallo pad tooyour .pubxml bestand voor een web-app relatieve toohello-hoofdmap van het Hallo-opslagplaats. Genegeerd voor cloud-services. |
    | SharePoint-omgeving voor implementatie |dezelfde als de servicenaam Hallo Hallo. |
    | Azure-implementatie-omgeving |Hallo-app of cloud naam van de webservice. |
12. Als u gebruikmaakt van serviceconfiguraties met meerdere (.cscfg-bestanden), kunt u de gewenste serviceconfiguratie Hallo opgeven in Hallo **bouwen, Geavanceerd MSBuild-argumenten** instelling. Bijvoorbeeld, toouse ServiceConfiguration.Test.cscfg, stelt MSBuild-argumenten regeloptie `/p:TargetProfile=Test`.
    
     ![][38]
    
     Op dit tijdstip moet uw build worden voltooid.
    
     ![][28]
13. Als u dubbelklikt op de naam van de build hello, ziet u Visual Studio een **bouwen samenvatting**, met inbegrip van de testresultaten van eenheid Testprojecten die is gekoppeld.
    
     ![][29]
14. In Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885), kunt u Hallo gekoppeld implementatie bekijken op Hallo **implementaties** tabblad wanneer Hallo staging-omgeving is geselecteerd.
    
     ![][30]
15. De URL van de site tooyour bladeren. Klik op Hallo voor een web-app **Bladeren** knop op de opdrachtbalk Hallo. Kies voor een cloudservice Hallo URL uit Hallo **snel in één oogopslag** sectie Hallo **Dashboard** pagina waarin de faseringsomgeving Hallo voor een cloudservice. Implementaties van continue integratie voor cloud-services worden gepubliceerde toohello faseringsomgeving standaard. U kunt dit wijzigen door de instelling Hallo **alternatieve Cloudserviceomgeving** eigenschap te**productie**. Deze Schermafbeelding toont waar hello dat site-URL is op de dashboardpagina Hallo cloudservice.
    
    ![][31]
    
    Een nieuw browsertabblad geopend tooreveal uw site uitgevoerd.
    
    ![][32]
    
    Cloud-services, als u andere wijzigingen tooyour-project maakt, u trigger builds meer en wordt u meerdere implementaties verzamelt. Hallo recentste is gemarkeerd als actief.
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5: een eerdere build implementeren
Deze stap geldt toocloud services en is optioneel. In klassieke Azure-portal hello, kiest u een eerdere implementatie en kies vervolgens Hallo **implementeren** knop toorewind uw site tooan eerder incheckt.  Houd er rekening mee dat dit een nieuwe build in TFS activeren en maken van een nieuwe vermelding in de geschiedenis van uw implementatie.

![][34]

## <a name="6-change-hello-production-deployment"></a>6: Hallo productie-implementatie wijzigen
Deze stap geldt alleen toocloud services, niet-web-apps. Wanneer u klaar bent, kunt u Hallo fasering toohello productieomgeving promoveren Hallo kiezen **wisselen** knop in Hallo klassieke Azure-portal. faseringsomgeving Hallo zojuist geïmplementeerde is gepromoveerde tooProduction en Hallo vorige productie-omgeving, indien aanwezig, wordt een Staging-omgeving. Hallo actieve implementatie mogelijk anders voor hello productie- en faseringsomgevingen, maar de implementatiegeschiedenis Hallo van recente builds is Hallo dezelfde omgeving ongeacht.

![][35]

## <a name="7-run-unit-tests"></a>7: eenheidstests uitvoeren
Deze stap geldt alleen tooweb apps, niet-cloudservices. tooput een quality-gate voor uw implementatie, kunt u eenheidstests uitvoeren en als ze mislukken, kunt u Hallo implementatie stoppen.

1. Voeg een eenheid test-project in Visual Studio.
   
   ![][39]
2. Project verwijst naar toohello project u tootest wilt toevoegen.
   
   ![][40]
3. Sommige eenheidstests toevoegen. tooget gestart, probeert u een dummy-test die altijd wordt doorgegeven.
   
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
4. De definitie van de build Hallo bewerken, kiest u Hallo **proces** tabblad uit en vouw Hallo **Test** knooppunt.
5. Set Hallo **mislukken build voor testfout** tooTrue. Dit betekent dat Hallo implementatie zich niet tenzij Hallo test zijn geslaagd.
   
   ![][41]
6. Een nieuwe build wachtrij.
   
   ![][42]
   
   ![][43]
7. Tijdens het Hallo-build nadert, informatie over de voortgang bekijken.
   
    ![][44]
   
    ![][45]
8. Wanneer Hallo build is voltooid, controleert u de resultaten bekijkt hello.
   
    ![][46]
   
    ![][47]
9. Maak een test die mislukt. Toevoegen van een nieuwe test door te kopiëren Hallo eerste, wijzigt u de naam en uitcommentariëren Hallo coderegel dat notimplementedexception is een verwachte uitzondering gemeld.
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. Inchecken Hallo tooqueue een nieuwe build wijzigen.
    
     ![][48]
11. Hallo test resultaten toosee details weergeven over Hallo-fout.
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over eenheid testen in Visual Studio Team Services, [eenheidstests uitvoeren in uw build](http://go.microsoft.com/fwlink/p/?LinkId=510474). Als u Git, Zie [delen van uw code in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) en [continue implementatie tooAzure App Service](../app-service-web/app-service-continuous-deployment.md).  Zie voor meer informatie over Visual Studio Team Services, [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).

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
