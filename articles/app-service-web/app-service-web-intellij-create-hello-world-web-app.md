---
title: een eenvoudige Azure-web-app in IntelliJ aaaCreate | Microsoft Docs
description: Deze zelfstudie leert u hoe toouse hello Azure Toolkit voor IntelliJ toocreate een Hallo wereld-Web-App voor Azure.
services: app-service\web
documentationcenter: java
author: selvasingh
manager: erikre
editor: 
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4667497213cac3ddf754d164e614c809f338cce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a>Een eenvoudige Azure-web-app maken in IntelliJ
Deze zelfstudie laat zien hoe toocreate en een eenvoudige Hallo wereld toepassing tooAzure implementeren als een Web-App met behulp van Hallo [Azure Toolkit voor IntelliJ]. Een eenvoudige JSP-voorbeeld voor eenvoud wordt weergegeven, maar gelijksoortige stappen zou zijn geschikt voor een servlet Java wat betreft Azure-implementatie is.

Wanneer u deze zelfstudie hebt voltooid, ziet uw toepassing vergelijkbare toohello afbeelding volgen wanneer u deze in een webbrowser bekijken:

![Voorbeeldwebpagina][01]

## <a name="prerequisites"></a>Vereisten
* Een Java Developer Kit (JDK), v 1.8 of hoger.
* IntelliJ IDEA Ultimate Edition. Dit kan worden gedownload vanaf <https://www.jetbrains.com/idea/download/index.html>.
* Een distributiepunt van een Java gebaseerde webserver of toepassingsserver, zoals [Apache Tomcat] of [Jetty].
* Een Azure-abonnement, die kan worden opgehaald uit <https://azure.microsoft.com/free/> of <http://azure.microsoft.com/pricing/purchase-options/>.
* Hallo [Azure Toolkit voor IntelliJ]. Zie voor meer informatie over het installeren van hello Azure Toolkit [installeren hello Azure Toolkit voor IntelliJ].

## <a name="toocreate-a-hello-world-application"></a>een toepassing Hello World toocreate
Eerst beginnen we uitschakelen met een Java-project maken.

1. IntelliJ Start en klik op Hallo **bestand** menu, klikt u vervolgens op **nieuw**, en klik vervolgens op **Project**.
   
    ![Bestand Nieuw Project][02]
2. Selecteer in het dialoogvenster Nieuw Project hello, **Java**, klikt u vervolgens **webtoepassing**, en klik vervolgens op **nieuw** tooadd een SDK-Project.
   
    ![Het dialoogvenster Nieuw project][03a]
   
3. In Hallo basismap selecteren voor het dialoogvenster JDK, selecteer map waarin uw JDK is geïnstalleerd en klik vervolgens op Hallo **OK**. Klik op **volgende** in Hallo nieuw Project dialoogvenster vak toocontinue.
   
    ![Basismap van de JDK opgeven][03b]
4. Naam voor deze zelfstudie Hallo project **Java-Web-App-op-Azure**, en klik vervolgens op **voltooien**.
   
    ![Het dialoogvenster Nieuw project][04]
5. Vouw in de weergave Project Explorer van IntelliJ **Java-Web-App-op-Azure**, vouw vervolgens **web**, en dubbelklik vervolgens op **index.jsp**.
   
    ![Open indexpagina][05c]
6. Wanneer het bestand index.jsp wordt geopend in IntelliJ, toevoegen in toodynamically tekstweergave **Hello World!** binnen de bestaande Hallo `<body>` element. Uw bijgewerkte `<body>` inhoud moet eruitzien als Hallo voorbeeld te volgen:
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. Index.jsp opslaan.

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a>toodeploy uw toepassing tooan Azure Web App-Container
Er zijn verschillende manieren waarop u een Java web application tooAzure kunt implementeren. Deze zelfstudie wordt beschreven in een van de eenvoudigste Hallo: uw toepassing worden geïmplementeerde tooan Azure Web App-Container - geen speciale projecttype of extra hulpprogramma's nodig zijn. Hallo JDK en Hallo web container software worden geleverd voor u door Azure, zodat er geen noodzaak tooupload uw eigen; u hoeft uw Java-Web-App is. Als gevolg hiervan wordt publicatieproces voor uw toepassing hello seconden, niet minuten duren.

Voordat u uw toepassing publiceren, moet u eerst tooconfigure module-instellingen. toodo gebruik dus Hallo stappen te volgen:

1. In de IntelliJ Projectverkenner met de rechtermuisknop op Hallo **Java-Web-App-op-Azure** project. Wanneer het Hallo-contextmenu wordt weergegeven, klikt u op **Open Module-instellingen**.

    ![Open de Module-instellingen][05a]
2. Wanneer de Hallo structuur Project dialoogvenster wordt weergegeven:

   a. Klik op **artefacten** in de lijst met Hallo **projectinstellingen**.
   b. Naam van wijzigen Hallo artefacten in Hallo **naam** vak zodat het geen spaties of speciale tekens bevat; dit is nodig omdat het Hallo-naam wordt gebruikt in Hallo Uniform Resource Identifier (URI).
   c. Wijziging Hallo **Type** te**webtoepassing: archief**.
   d. Klik op **OK** tooclose Hallo structuur Project dialoogvenster.

    ![Open de Module-instellingen][05b]

Wanneer u uw module-instellingen hebt geconfigureerd, kunt u uw toepassing tooAzure publiceren met behulp van Hallo stappen te volgen:

1. In de IntelliJ Projectverkenner met de rechtermuisknop op Hallo **Java-Web-App-op-Azure** project. Wanneer het Hallo-contextmenu wordt weergegeven, selecteert u **Azure**, en klik vervolgens op **publiceren als Azure-Web-App...**
   
    ![Azure contextmenu publiceren][06]
2. Als u hebt nog niet aangemeld bij Azure van IntelliJ, kunt u zich na vragen aan gebruiker toosign in uw Azure-account. (Als er meerdere Azure-accounts, aantal Hallo prompts tijdens de aanmelding Hallo in proces worden mogelijk weergegeven meer dan één keer zelfs als ze worden weergegeven toobe Hallo dezelfde. Als dit gebeurt, blijven toofollow Hallo aanmelding instructies.)
   
    ![Azure-logboekanalyse In het dialoogvenster][07]
3. Nadat u bent aangemeld bij uw Azure-account, Hallo **abonnementen beheren** in het dialoogvenster een lijst met abonnementen die gekoppeld aan uw referenties zijn worden weergegeven. (Als er meerdere abonnementen die worden vermeld en toowork met alleen een specifieke subset van deze gewenste, u kan desgewenst uitschakelen Hallo-abonnementen die u niet wilt dat toouse.) Wanneer u uw abonnementen hebt geselecteerd, klikt u op **sluiten**.
   
    ![Abonnementen beheren][08]
4. Wanneer Hallo **tooAzure Web-App-Container implementeren** dialoogvenster wordt weergegeven, wordt deze in een Web-App-containers die u eerder hebt gemaakt weergegeven; als u geen containers niet gemaakt hebt, Hallo lijst is leeg.
   
    ![App-Containers][09]
5. Als u geen hebt gemaakt een Azure-Web-App-Container vóór of als u wilt toopublish uw toepassing tooa nieuwe container, gebruik Hallo stappen te volgen. Anders selecteert u een bestaande Web-App-Container en skip-toostep 6 hieronder.
   
   1. Klik op**+**
      
       ![App-Container toevoegen][10]
   2. Hallo **nieuwe Web-App-Container** in het dialoogvenster wordt weergegeven, die worden gebruikt voor Hallo naast verschillende stappen.
      
       ![Nieuwe App-Container][11a]
   3. Voer een **DNS-Label** voor uw Web-App-Container; vormt dit Hallo leaf DNS-label van Hallo host-URL voor uw webtoepassing in Azure. Houd er rekening mee dat Hallo-naam moet beschikbaar zijn en voldoen naamgevingsvereisten tooAzure voor Web-App.
   4. In Hallo **webcontainer** vervolgkeuzelijst, selecteer Hallo geschikte software voor uw toepassing.
      
       U kunt op dit moment van Tomcat-8, 7 Tomcat of Jetty 9. Een recente distributie van software Hallo geselecteerd door Azure worden verstrekt en het wordt uitgevoerd op een recente verdeling van JDK 8 gemaakt door Oracle en geleverd door Azure.
   5. In Hallo **abonnement** vervolgkeuzelijst, selecteer Hallo abonnement gewenste toouse voor deze implementatie.
   6. In Hallo **resourcegroep** vervolgkeuzelijst, selecteer Hallo resourcegroep waarmee u tooassociate uw Web-App wilt. (Azure resourcegroepen kunt u toogroup verwante resources samen zodat bijvoorbeeld ze samen kunnen worden verwijderd.)
      
       U kunt een bestaande resourcegroep selecteren (als u een hebt) en overslaan toostep g onderstaande of gebruik Hallo volgende stappen toocreate een nieuwe resourcegroep:
      
      * Selecteer  **&lt; &lt; nieuwe resourcegroep maken &gt; &gt;**  in Hallo **resourcegroep** vervolgkeuzelijst.
      * Hallo **nieuwe resourcegroep** in het dialoogvenster wordt weergegeven:
        
          ![Nieuwe resourcegroep][12]
      * In Hallo Hallo **naam** textbox, Geef een naam voor uw nieuwe resourcegroep.
      * In Hallo Hallo **regio** vervolgkeuzelijst, selecteer Hallo juiste Azure datacentrum locatie voor de resourcegroep.
      * Klik op **OK**.
   7. Hallo **App Service-Plan** vervolgkeuzelijst bevat Hallo-app service-abonnementen die zijn gekoppeld aan Hallo resourcegroep die u hebt geselecteerd. (Een App Service-Plan bevat informatie zoals Hallo-locatie van uw Web-App Hallo prijscategorie en Hallo compute exemplaargrootte. Een enkele App Service-Plan kan worden gebruikt voor meerdere Web-Apps, dat is waarom deze afzonderlijk van een specifieke implementatie van Web-App onderhouden.)
      
       Selecteer een bestaand App Service-abonnement (als u een hebt) en toostep h onderstaande overslaan of gebruik een Hallo stappen toocreate een nieuwe App Service-Plan te volgen:
      
      * Selecteer  **&lt; &lt; maken nieuwe App Service-Plan &gt; &gt;**  in Hallo **App Service-Plan** vervolgkeuzelijst.
      * Hallo **nieuwe App Service-Plan** in het dialoogvenster wordt weergegeven:
        
          ![Nieuwe App Service-abonnement][13]
      * In Hallo Hallo **naam** textbox, Geef een naam voor uw nieuwe App Service-Plan.
      * In Hallo Hallo **locatie** vervolgkeuzelijst, selecteer Hallo juiste Azure datacentrum locatie voor Hallo plan.
      * In Hallo Hallo **prijscategorie** vervolgkeuzelijst, selecteer Hallo toepasselijke prijzen voor Hallo plan. Voor testdoeleinden kunt u **vrije**.
      * In Hallo Hallo **Exemplaargrootte** vervolgkeuzelijst, selecteer Hallo juiste exemplaargrootte voor Hallo plan. Voor testdoeleinden kunt u **kleine**.
      * Klik op **OK**.
   8. (Optioneel) Standaard worden een recente verdeling van Java 8 automatisch geïmplementeerd als uw JVM door Azure tooyour web-app-container. U kunt echter een andere versie en de distributie van Hallo JVM selecteren. toodo gebruik dus Hallo stappen te volgen:
      
      * Klik op Hallo **JDK** tabblad in Hallo **nieuwe Web-App-Container** in het dialoogvenster.
      * U kunt kiezen uit een Hallo volgende opties:
        
        * Hallo standaard JDK die wordt aangeboden door Azure implementeren
        * Een 3e party JDK uit een vervolgkeuzelijst van aanvullende JDKs die beschikbaar op Azure zijn implementeren
        * Implementeren van een aangepaste JDK die moet worden opgenomen als een ZIP-bestand en een openbaar of in uw Azure storage-account
        
        ![Nieuw App-Container JDK tabblad][11b]
   9. Nadat u alle Hallo bovenstaande stappen hebt voltooid, ziet er Hallo nieuwe Web-App-Container dialoogvenster Hallo volgende afbeelding:
      
       ![Nieuwe App-Container][14]
   10. Klik op **OK** toocomplete Hallo maken van uw nieuwe Web-App-container.
       
        Wacht een paar seconden voor Hallo lijst met Hallo Web-App containers toobe vernieuwd en de zojuist gemaakte web-app-container moet nu worden geselecteerd in het Hallo-lijst.
6. U bent nu klaar toocomplete Hallo initiële implementatie van uw Web-App tooAzure; Klik op **OK** toodeploy uw Java-toepassing toohello geselecteerd Web-App-container. Standaard wordt uw toepassing wordt geïmplementeerd als een submap van de toepassingsserver Hallo. Als u toobe geïmplementeerd als de hoofdtoepassing hello wilt, Controleer Hallo **implementeren tooroot** selectievakje voordat u op **OK**.
   
    ![TooAzure implementeren][15]
7. Vervolgens ziet u Hallo **Azure Activity Log** waarmee wordt aangegeven Hallo implementatiestatus van uw Web-App bekijken.
   
    ![Voortgangsindicator][16]
   
    Hallo-proces voor het implementeren van uw Web-App tooAzure duurt slechts enkele seconden toocomplete. Wanneer uw toepassing ready, ziet u een koppeling met de naam **gepubliceerde** in Hallo **Status** kolom. Wanneer u Hallo koppeling klikt, duurt het u startpagina tooyour geïmplementeerd van Web-App of kunt u Hallo stappen in de volgende sectie toobrowse tooyour web-app Hallo.

## <a name="browsing-tooyour-web-app-on-azure"></a>Bladeren door tooyour Web-App in Azure
toobrowse tooyour Web-App in Azure, kunt u Hallo **Azure Explorer** weergeven.

Als hello **Azure Explorer** weergave nog niet is geopend, kunt u deze openen door te klikken op vervolgens **weergave** menu in IntelliJ, klikt u vervolgens op **hulpprogramma Windows**, en klik vervolgens op  **Service-Explorer**. Als u eerder niet hebt aangemeld, wordt u gevraagd toodo dus.

Wanneer Hallo **Azure Explorer** weergave wordt weergegeven, gebruik Volg deze stappen toobrowse tooyour Web-App: 

1. Vouw Hallo **Azure** knooppunt.
2. Vouw Hallo **Web-Apps** knooppunt. 
3. Klik met de rechtermuisknop Hallo gewenste Web-App.
4. Wanneer het Hallo-contextmenu wordt weergegeven, klikt u op **openen in Browser**.
   
    ![Web-App bladeren][17]

## <a name="updating-your-web-app"></a>De web-app beveiligen
Bijwerken van een bestaande Azure-Web-App uitgevoerd is een snelle en eenvoudige proces en hebt u twee opties voor het bijwerken van:

* U kunt Hallo-implementatie van een bestaande Java-Web-App kunt bijwerken.
* U kunt een extra toohello voor Java-toepassing publiceren dezelfde Web-App-Container.

In beide gevallen Hallo proces identieke en duurt slechts enkele seconden:

1. Hallo IntelliJ Projectverkenner met de rechtermuisknop op Hallo Java-toepassing die u wilt dat tooupdate of tooan bestaande Web-App-Container toevoegen.
2. Wanneer het Hallo-contextmenu wordt weergegeven, selecteert u **Azure** en vervolgens **publiceren als Azure-Web-App...**
3. Nadat u hebt al aangemeld eerder, ziet u een lijst met uw bestaande Web-App-containers. Selecteer een of wilt u toopublish opnieuw publiceren, uw Java-toepassing tooand Klik Hallo **OK**.

Een paar seconden later Hallo **Azure Activity Log** weer uw bijgewerkte implementatie als **gepubliceerde** en u kunt tooverify uw bijgewerkte toepassing in een webbrowser worden.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Starten, stoppen of opnieuw starten van een bestaande web-app
toostart of stoppen van een bestaande Azure-Web-App-container (inclusief alle Hallo geïmplementeerd Java-toepassingen in deze), kunt u Hallo **Azure Explorer** weergeven.

Als hello **Azure Explorer** weergave nog niet is geopend, kunt u deze openen door te klikken op vervolgens **weergave** menu in IntelliJ, klikt u vervolgens op **hulpprogramma Windows**, en klik vervolgens op  **Service-Explorer**. Als u eerder niet hebt aangemeld, wordt u gevraagd toodo dus.

Wanneer Hallo **Azure Explorer** weergave wordt weergegeven, gebruik Volg deze stappen toostart of stoppen van uw Web-App: 

1. Vouw Hallo **Azure** knooppunt.
2. Vouw Hallo **Web-Apps** knooppunt. 
3. Klik met de rechtermuisknop Hallo gewenste Web-App.
4. Wanneer het Hallo-contextmenu wordt weergegeven, klikt u op **Start**, **stoppen**, of **opnieuw**. Houd er rekening mee dat Hallo menu-Opties contextbewuste, zijn zodat u kunt alleen een actieve WebApp stoppen of starten van een web-app die niet wordt uitgevoerd.
   
    ![Web-App stoppen][18]

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over hello Azure Toolkits voor IDE voor Java Hallo koppelingen te volgen:

* [Azure Toolkit voor Eclipse]
  * [Hello Azure Toolkit voor Eclipse installeren]
  * [Een Hallo wereld Web-App maken voor Azure in Eclipse]
  * [Wat is er nieuw in hello Azure Toolkit voor Eclipse]
* [Azure Toolkit voor IntelliJ] (Azure Toolkit voor IntelliJ)
  * [installeren hello Azure Toolkit voor IntelliJ]
  * *Een Hallo wereld Web-App maken voor Azure in IntelliJ (in dit artikel)*
  * [Wat is er nieuw in hello Azure Toolkit voor IntelliJ]

<a name="see-also"></a>

## <a name="see-also"></a>Zie ook
Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center].

Zie voor meer informatie over het maken van Azure Web Apps Hallo [overzicht van Web Apps].

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Azure Toolkit voor Eclipse]: ../azure-toolkit-for-eclipse.md
[Azure Toolkit voor IntelliJ]: ../azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)
[Een Hallo wereld Web-App maken voor Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Hello Azure Toolkit voor Eclipse installeren]: ../azure-toolkit-for-eclipse-installation.md
[installeren hello Azure Toolkit voor IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[Wat is er nieuw in hello Azure Toolkit voor Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md
[Wat is er nieuw in hello Azure Toolkit voor IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[overzicht van Web Apps]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-intellij-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-intellij-create-hello-world-web-app/02-File-New-Project.png
[03a]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-Dialog.png
[03b]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-SDK-Dialog.png
[04]: ./media/app-service-web-intellij-create-hello-world-web-app/04-New-Project-Dialog.png
[05a]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Module-Settings.png
[05b]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Project-Structure-Dialog.png
[05c]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Index-Page.png
[06]: ./media/app-service-web-intellij-create-hello-world-web-app/06-Azure-Publish-Context-Menu.png
[07]: ./media/app-service-web-intellij-create-hello-world-web-app/07-Azure-Log-In-Dialog.png
[08]: ./media/app-service-web-intellij-create-hello-world-web-app/08-Manage-Subscriptions.png
[09]: ./media/app-service-web-intellij-create-hello-world-web-app/09-App-Containers.png
[10]: ./media/app-service-web-intellij-create-hello-world-web-app/10-Add-App-Container.png
[11a]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container.png
[11b]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container-JDK-Tab.png
[12]: ./media/app-service-web-intellij-create-hello-world-web-app/12-New-Resource-Group.png
[13]: ./media/app-service-web-intellij-create-hello-world-web-app/13-New-App-Service-Plan.png
[14]: ./media/app-service-web-intellij-create-hello-world-web-app/14-New-App-Container.png
[15]: ./media/app-service-web-intellij-create-hello-world-web-app/15-Deploy-To-Azure.png
[16]: ./media/app-service-web-intellij-create-hello-world-web-app/16-Progress-Indicator.png
[17]: ./media/app-service-web-intellij-create-hello-world-web-app/17-Browse-Web-App.png
[18]: ./media/app-service-web-intellij-create-hello-world-web-app/18-Stop-Web-App.png
