---
title: 'Zelfstudie: DevOps Hello Azure Portal | Microsoft Docs'
description: Meer informatie over verschillende DevOps-werkstromen in Azure Portal Hallo Hallo.
services: azure-portal
documentationcenter: 
author: mlearned
manager: douge
editor: mlearned
ms.assetid: 4f1c5bc1-c732-4d35-b5df-0fd68e547d38
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2016
ms.author: mlearned
ms.openlocfilehash: 4c32dbbd4e4b1c3809ef4b01e1496e350183ebde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-devops-with-hello-azure-portal"></a>Zelfstudie: DevOps Hello Azure Portal
Hello Azure-platform is vol. van flexibele DevOps-werkstromen In deze zelfstudie leert u hoe tooleverage Hallo mogelijkheden van Azure Portal-toodevelop hello, testen, implementeren, oplossen, bewaken en beheren van actieve toepassingen. Deze zelfstudie richt zich op Hallo volgende:

1. Een webtoepassing maken en continue implementatie inschakelen
2. Een app ontwikkelen en testen
3. Een app bewaken en problemen oplossen
4. Algemene taken voor toepassingsbeheer

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a>Een webtoepassing maken en continue implementatie inschakelen
Maken van een Web-app met [Azure App Service](https://azure.microsoft.com/services/app-service/), gebruikt u in de rest van deze handleiding Hallo. In eerste instantie schakelt u continue implementatie in vanuit de opslagplaats van de broncode naar de actieve Azure-omgeving.

1. Meld u aan bij hello Azure Portal
2. Kies **App Services** &gt; **pictogram toevoegen** en voer een naam, kiest u uw abonnement en een nieuwe resource groep tooserve als Hallo-container voor Hallo service maken.
   
   Resourcegroepen kunnen u toomanage verschillende aspecten van Hallo oplossing zoals facturering, implementaties en bewaakt alle als één groep via [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
   
   ![image1][image1]
3. Na enkele ogenblikken is de app-service gemaakt. Haal een paar minuten tooexplore Hallo verschillende opties voor Hallo-service in Hallo-portal.
   
   ![image2][image2]    
4. Klik op Hallo-URL. U ziet Hallo verschillende beschikbare opties voor hulpprogramma's en -opslagplaatsen. U kunt ook Hallo talen en frameworks van uw keuze waaronder .NET, Java en Ruby gebruiken.
   
   ![image3][image3]    
5. Hello Azure-portal maakt continue implementatie een eenvoudig proces waarbij slechts een paar eenvoudige stappen. Kies in hello Azure-portal, instellingen van Hallo pictogram voor Hallo app service die u zojuist hebt gemaakt.
   
   ![image4][image4]
   
   Schuif blade die wordt geopend op de juiste Hallo Hallo toohello sectie publiceren.
   
   ![image5][image5]
6. Configureer vervolgens een aantal instellingen tooenable continue implementatie voor Hallo-app. Klik op Implementatiebron en vervolgens op Bron kiezen. U ziet Hallo verschillende opties die u voor de opslagplaats bronnen hebt.
   
   ![image6][image6]
7. Kies voor dit voorbeeld GitHub. (Optioneel) Kies Hallo opslagplaats van uw keuze en Hallo autorisatiereferenties instellen.
   
   ![image7][image7]
8. Na autorisatie tooyour opslagplaats, klikt u vervolgens kunt u een project en de gewenste toodeploy vertakking. Hieronder ziet u een aantal fictieve voorbeelden.
   
   ![image8][image8]
9. Klik op OK nadat u het project en de vertakking hebt gekozen. U moet eerst toosee meldingen van een implementatie.
   
   ![image9][image9]
10. Navigeer terug tooGitHub toosee hello webhook toointegrate Hallo bron besturingselement opslagplaats is gemaakt met Azure. Hello Azure Portal kunt integratie met GitHub met slechts een paar eenvoudige stappen.
    
    ![image10][image10]
11. doorlopende implementatie toodemonstrate, u de opslagplaats van bepaalde inhoud toohello snel toevoegen. Voor een eenvoudig voorbeeld voegt u een voorbeeld tekst bestand tooa GitHub-repo. U bent gratis toouse .NET, Ruby, Python of een ander type toepassing met App Service. Gratis tooadd een tekstbestand van mening bent dat ASP.NET MVC, Java of Ruby toepassing toohello opslagplaats van uw keuze.
    
    ![image11][image11]
12. Na het doorvoeren van wijzigingen tooyour opslagplaats, ziet u een nieuwe implementatie in de portal meldingengebied Hallo initiëren. Klik op synchroniseren als u snel geen wijzigingen ziet na het vastleggen van de opslagplaats tooyour.
    
    ![image12][image12]
13. Als u probeert en laden van pagina Hallo voor Hallo app service, wordt u op dit moment een fout 403. In dit voorbeeld is het omdat er geen typische standaard documentinstellingen voor Hallo pagina zoals een bestand zoals index.htm of default.html. U kunt snel lost dit probleem Hello tooling in hello Azure-Portal.  Kies in hello Azure Portal instellingen &gt; toepassingsinstellingen.
    
     ![image13][image13]
14. Er wordt nu een blade met toepassingsinstellingen geopend. Hallo-naam van Hallo pagina 'SamplePage.html' en klik op opslaan. Duren voordat u een paar minuten tooexplore Hallo andere instellingen.
    
    ![image14][image14]
15. Eventueel Vernieuw uw browser-URL tooensure ziet u de wijzigingen Hallo verwacht. Er is in dit geval een aantal eenvoudige tekst hello pagina nu in te vullen. Elke aanvullende wijzigen toohello opslagplaats zou leiden tot een nieuwe automatische implementatie.
    
    ![image15][image15]
    
    Inschakelen van continue implementatie met hello Azure Portal is een eenvoudige ervaring. U kunt ook complexere release pijplijnen bouwen en veel andere technieken gebruiken met bestaande broncodebeheer en continue integratie systemen toodeploy tooAzure, zoals het gebruik van geautomatiseerde build en release beheersystemen.

## <a name="develop-and-test-an-app"></a>Een app ontwikkelen en testen
Vervolgens brengt u enkele wijzigingen toohello code base en snel implementeren die wijzigingen. U wordt ook instellen om sommige prestatietests voor Hallo Web-app.

1. Kies App Services in het navigatiedeelvenster Hallo in hello Azure-Portal en zoek uw App Service.
   
   ![image16][image16]
2. Klik op Hulpprogramma’s
   
   ![image17][image17]
3. U ziet Hallo categorie onder Tools ontwikkelen. Er zijn enkele nuttige hulpmiddelen hier dat wij toowork met apps zonder hello Azure-Portal. Klik op Console.
   
   ![image18][image18]
4. In het consolevenster hello, kunt u live opdrachten uitgeven voor uw app. Typ Hallo dir opdracht en drukt op enter. Opdrachten waarvoor verhoogde bevoegdheden zijn vereist, werken echter niet.
   
   ![image19][image19]
5. Toohello ontwikkelen categorie terug en kies Visual Studio Online. Opmerking: Visual Studio Online heet nu Visual Studio Team Services.
   
   ![image20][image20]
6. In-of uitschakelen op Hallo in de browser bewerken ervaring voor uw App.
   
   ![image21][image21]
7. Er wordt een webservice-extensie voor uw app geïnstalleerd. Snel en eenvoudig toevoegen extensies tooapps functionaliteit in Azure. U ziet enkele Hallo andere Uitbreidingstypen beschikbaar is in onderstaande schermafbeelding voor Hallo.
   
   ![image22][image22]
8. Zodra Hallo Visual Studio Online-extensie is geïnstalleerd, klikt u op Start.
   
   ![image23][image23]
9. Een browser wordt geopend waarin u zien hoe een ontwikkeling IDE rechtstreeks in de browser Hallo tabblad. Kennisgeving Hallo ervaring onderstaande wordt Chrome.
   
   ![image24][image24]
10. U kunt uitvoeren van verschillende activiteiten zoals bewerken bestanden, bestanden en mappen toevoegen en downloaden inhoud vanaf Hallo live site. Een snelle bewerken toohello SamplePage.html-bestand maken.
    
    ![image25][image25]
11. Hallo wijzigingen worden automatisch opgeslagen in een paar seconden. Als u back-toohello pagina navigeert, kunt u Hallo wijzigingen kan zien. Let op: dit soort live bewerkingen is doorgaans niet geschikt voor productieomgevingen. Hallo-hulpprogramma's zijn echter maken het heel eenvoudig toomake snelle wijzigingen voor dev en testomgeving.
    
    ![image26][image26]
    
    ![image27][image27]
12. Toohello extra blade teruggaan en onder Hallo ontwikkelen categorie, klik op prestatietest.
    
    ![image28][image28]
13. U moet tooset een team services-account. Zie [Een Team Services-account maken](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services) voor meer informatie
14. Klik op nieuwe toocreate een prestatietest.
    
    ![image29][image29]
    
    Configureer Hallo verschillende waarden en klik op Test uitvoeren Hallo Hallo dialoog tooinitiate een prestatietest onderaan in.
    
    ![image30][image30]
    
    ![image31][image31]
15. Zodra Hallo test uitgevoerd start, kunt u Hallo status controleren.
    
    ![image32][image32]
    
    Zodra het Hallo-test is voltooid, bevat te klikken op Hallo resultaat meer informatie.
    
    ![image33][image33]
16. In dit voorbeeld moet u een korte test uitvoeren, zodat er beperkte gegevens tooanalyze, maar u kunt verschillende metrische gegevens te verzamelen, evenals uw test in deze weergave opnieuw gemaakt. Hello Azure Portal kunt maken, uitvoeren en analyseren van webtests voor prestaties van een eenvoudig proces. Hallo onderstaande schermafbeeldingen Hallo-prestatiegegevens weergegeven.
    
    ![image34][image34]
    
    ![image35][image35]
    
    ![image36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a>Een app bewaken en problemen oplossen
Azure biedt veel opties voor het bewaken van actieve toepassingen en het oplossen van problemen.

1. Kies de hulpprogramma's in hello Azure-Portal voor de Web-app.
   
   ![image37][image37]
2. Let op Hallo van verschillende opties voor het gebruik van hulpprogramma's voor tootroubleshoot potentiële problemen met een actieve app onder Hallo oplossen categorie. U kunt onder andere live HTTP-verkeer bewaken, zelfherstel inschakelen en logboeken weergeven.
   
   ![image38][image38]
3. Kies Site metrische gegevens tooquickly get een weergave van bepaalde HTTP-codes.
   
   ![image39][image39]
4. Kies Diagnostics as a Service. Kies het toepassingstype en klik op Uitvoeren.
   
   ![image40][image40]
   
   De gegevens worden verzameld.
   
   ![image41][image41]
5. U kunt Hallo juiste logboek toodiagnose potentiële problemen. U moet tooenable logboekregistratie toosee alle beschikbare gegevens Hallo opties zoals HTTP-Logboeken.
   
   ![image42][image42]
   
   Analyse rapport toohelp vinden door te klikken op Hallo geheugendumpbestand kunt u downloaden en analyseren van een DebugDiag potentiële problemen.
   
   ![image43][image43]
6. tooview meer gegevens, moet u aanvullende logboekregistratie tooenable. In hello Azure Portal, gaat u toohello Web-app en kies instellingen.
   
   ![image44][image44]
7. Schuif naar beneden toohello functies categorie en kies diagnostische logboeken.
   
      ![image45][image45]
8. Let op Hallo van verschillende opties voor logboekregistratie. Schakel Webserverlogboeken in en klik op Opslaan.
   
   ![image46][image46]
9. Toohello extra gebied voor Hallo app teruggaan en diagnostische gegevens als een service en klik op uitvoeren toorerun Hallo gegevensverzameling.
   
   ![image47][image47]
10. Instelling van Hallo HTTP-logboekregistratie is ingeschakeld, ziet u nu gegevens verzameld voor HTTP-Logboeken.
    
    ![image48][image48]
11. Door te klikken op Hallo HTML-logbestand, moet u een uitgebreid rapport op basis van een browser voor verder onderzoek produceren.
    
    ![image49][image49]
12. Toohello extra sectie in hello Azure-Portal voor Hallo app gaan. Schuif toohello extra sectie en kies Procesverkenner.
    
    ![image50][image50]
13. Kies Procesverkenner als u gegevens over actieve processen wilt bekijken. U ziet u kunt inzoomen processen en zelfs kill processen via hello Azure-Portal.
    
    ![image51][image51]
    
    ![image52][image52]
14. De blade instellingen toohello op Hallo links terugwaartse. Klik op Nieuw ondersteuningsverzoek.
    
    ![image53][image53]
15. Hallo blade op Hallo rechts kunt u meer informatie over problemen Hallo invullen, contactgegevens invoeren en zelfs diagnostische gegevens uploaden. Hello Azure Portal kunt werken met Microsoft ondersteuning naadloos.
    
    ![image54][image54]
    
    ![image55][image55]
    
    Hello Azure Portal biedt krachtige en bekend tooling ervaringen toohelp bewaken en problemen oplossen onze waarop toepassingen worden uitgevoerd. Bent u ook kunnen tootake actie snel door taken uitvoeren zoals het recyclen van processen, inschakelen en uitschakelen van verschillende verzamelen van gegevens en zelfs integreren met Microsoft ondersteuning op professional.

## <a name="general-application-management"></a>Algemeen toepassingsbeheer
Bij het beheren van toepassingen, moet u vaak tooperform tal van activiteiten, zoals back-strategieën configureren, implementeren en id-providers beheren en configureren van toegangsbeheer op basis van rollen. Als hello met andere ervaringen DevOps, hello Azure-platform geïntegreerd met deze taken rechtstreeks Hallo-portal.

1. tooensure die u bijhoudt Hallo Web-App tegen verlies van gegevens moet u tooconfigure back-ups. Navigeer toohello gebied voor instellingen voor uw Web-app.
   
   ![image56][image56]
2. Hallo-blade op Hallo rechts, schuif naar beneden toohello functies categorie.
   
    ![image57][image57]
3. Kies de back-ups; Er wordt een blade geopend op de juiste Hallo.
   
   ![image58][image58]
4. Klik op configureren, kiest u een opslagaccount Hallo-blade op Hallo rechts.
   
   ![image59][image59]
5. Nu maakt en kies een container opslag toohold uw back-ups. Klik op maken Hallo Hallo blade onderaan in. Selecteer vervolgens Hallo-container.
   
   ![image60][image60]
6. Zodra u Hallo container hebt gekozen, kunt u schema's, evenals de setup-back-ups kunt configureren voor uw databases. Klik op Hallo opslaan pictogram voor dit scenario.
   
    ![image61][image61]
7. Schuif terug toohello blade aan de linkerkant Hallo voor back-ups nadat ze zijn opgeslagen. Klik op Nu back-up tooback Hallo toepassing.
   
    ![image62][image62]
8. Binnen enkele tellen ziet u dat er een back-up wordt gemaakt. Kennisgeving hello nu terugzetten optie op Hallo schermafbeelding hieronder.
   
    ![image63][image63]
9. Klik op Nu terugzetten en Hallo opties toohello blade op Hallo rechts onderzoeken. U kunt dat een geschikte back-up en eenvoudig terugzetten tooan eerder status zo nodig. Hello Azure-portal heeft geholpen ons gemakkelijk een eenvoudige strategie voor noodherstel van Hallo app inschakelen.
   
    ![image64][image64]
10. Verplaats terug toohello instellingenblade op Hallo links en -functies en -verificatie/autorisatie kiezen.
    
     ![image65][image65]
11. Hallo-blade op Hallo rechts App Service-verificatie te kiezen. U ziet Hallo verschillende opties die u met populaire providers configureren kunt.
    
     ![image66][image66]
12. Kies een Hallo-provider van uw keuze en Hallo opties voor Hallo scope zien. U kunt een App-ID en de App geheim opgeeft en snel Facebook-verificatie inschakelen voor Hallo-app. Hello Azure Portal kunt verificatie als klare oplossing voor apps.
    
     ![image67][image67]
13. De blade instellingen toohello terug en kies gebruikers onder Hallo bronbeheer categorie.
    
     ![image68][image68]
14. Hallo-blade op Hallo rechts onderzoeken Hallo verschillende opties voor het toevoegen van rollen en gebruikers. Hello Azure Portal kunt u gemakkelijk RBAC (op rollen gebaseerde toegangsbeheer) voor de toepassing hello beheren.
    
     ![image69][image69]

## <a name="summary"></a>Samenvatting
Deze zelfstudie gedemonstreerd aantal Hallo power Hello Azure-platform door snel inschakelen van continue implementatie voor een web-app, uitvoeren van verschillende ontwikkeling en testen van activiteiten, bewaking en het oplossen van een live-app en ten slotte het beheren van de sleutel strategieën zoals herstel na noodgevallen, identiteit en toegangsbeheer op basis van rollen. Hello Azure-platform kan een geïntegreerde ervaring voor deze DevOps-werkstromen en u kunt efficiënt werken door in de context voor Hallo uit te voeren taak bijwerkt.

## <a name="next-steps"></a>Volgende stappen
* Azure Resource Manager is het belangrijk is voor het inschakelen van DevOps op Hallo Azure-platform.  Ga meer toolearn naar [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
* meer informatie over Azure App Service-implementatie gaat u naar toolearn [uw app tooAzure App Service implementeren](../app-service-web/web-sites-deploy.md)

[image1]: ./media/tutorial-azureportal-devops/image1.png
[image2]: ./media/tutorial-azureportal-devops/image2.png
[image3]: ./media/tutorial-azureportal-devops/image3.png
[image4]: ./media/tutorial-azureportal-devops/image4.png
[image5]: ./media/tutorial-azureportal-devops/image5.png
[image6]: ./media/tutorial-azureportal-devops/image6.png
[image7]: ./media/tutorial-azureportal-devops/image7.png
[image8]: ./media/tutorial-azureportal-devops/image8.png
[image9]: ./media/tutorial-azureportal-devops/image9.png
[image10]: ./media/tutorial-azureportal-devops/image10.png
[image11]: ./media/tutorial-azureportal-devops/image11.png
[image12]: ./media/tutorial-azureportal-devops/image12.png
[image13]: ./media/tutorial-azureportal-devops/image13.png
[image14]: ./media/tutorial-azureportal-devops/image14.png
[image15]: ./media/tutorial-azureportal-devops/image15.png
[image16]: ./media/tutorial-azureportal-devops/image16.png
[image17]: ./media/tutorial-azureportal-devops/image17.png
[image18]: ./media/tutorial-azureportal-devops/image18.png
[image19]: ./media/tutorial-azureportal-devops/image19.png
[image20]: ./media/tutorial-azureportal-devops/image20.png
[image21]: ./media/tutorial-azureportal-devops/image21.png
[image22]: ./media/tutorial-azureportal-devops/image22.png
[image23]: ./media/tutorial-azureportal-devops/image23.png
[image24]: ./media/tutorial-azureportal-devops/image24.png
[image25]: ./media/tutorial-azureportal-devops/image25.png
[image26]: ./media/tutorial-azureportal-devops/image26.png
[image27]: ./media/tutorial-azureportal-devops/image27.png
[image28]: ./media/tutorial-azureportal-devops/image28.png
[image29]: ./media/tutorial-azureportal-devops/image29.png
[image30]: ./media/tutorial-azureportal-devops/image30.png
[image31]: ./media/tutorial-azureportal-devops/image31.png
[image32]: ./media/tutorial-azureportal-devops/image32.png
[image33]: ./media/tutorial-azureportal-devops/image33.png
[image34]: ./media/tutorial-azureportal-devops/image34.png
[image35]: ./media/tutorial-azureportal-devops/image35.png
[image36]: ./media/tutorial-azureportal-devops/image36.png
[image37]: ./media/tutorial-azureportal-devops/image37.png
[image38]: ./media/tutorial-azureportal-devops/image38.png
[image39]: ./media/tutorial-azureportal-devops/image39.png
[image40]: ./media/tutorial-azureportal-devops/image40.png
[image41]: ./media/tutorial-azureportal-devops/image41.png
[image42]: ./media/tutorial-azureportal-devops/image42.png
[image43]: ./media/tutorial-azureportal-devops/image43.png
[image44]: ./media/tutorial-azureportal-devops/image44.png
[image45]: ./media/tutorial-azureportal-devops/image45.png
[image46]: ./media/tutorial-azureportal-devops/image46.png
[image47]: ./media/tutorial-azureportal-devops/image47.png
[image48]: ./media/tutorial-azureportal-devops/image48.png
[image49]: ./media/tutorial-azureportal-devops/image49.png
[image50]: ./media/tutorial-azureportal-devops/image50.png
[image51]: ./media/tutorial-azureportal-devops/image51.png
[image52]: ./media/tutorial-azureportal-devops/image52.png
[image53]: ./media/tutorial-azureportal-devops/image53.png
[image54]: ./media/tutorial-azureportal-devops/image54.png
[image55]: ./media/tutorial-azureportal-devops/image55.png
[image56]: ./media/tutorial-azureportal-devops/image56.png
[image57]: ./media/tutorial-azureportal-devops/image57.png
[image58]: ./media/tutorial-azureportal-devops/image58.png
[image59]: ./media/tutorial-azureportal-devops/image59.png
[image60]: ./media/tutorial-azureportal-devops/image60.png
[image61]: ./media/tutorial-azureportal-devops/image61.png
[image62]: ./media/tutorial-azureportal-devops/image62.png
[image63]: ./media/tutorial-azureportal-devops/image63.png
[image64]: ./media/tutorial-azureportal-devops/image64.png
[image65]: ./media/tutorial-azureportal-devops/image65.png
[image66]: ./media/tutorial-azureportal-devops/image66.png
[image67]: ./media/tutorial-azureportal-devops/image67.png
[image68]: ./media/tutorial-azureportal-devops/image68.png
[image69]: ./media/tutorial-azureportal-devops/image69.png
