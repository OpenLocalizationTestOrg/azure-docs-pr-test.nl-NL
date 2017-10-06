---
title: een eenvoudige Azure-web-app met aaaCreate Eclipse | Microsoft Docs
description: Deze zelfstudie leert u hoe toouse hello Azure Toolkit voor Eclipse toocreate een Hallo wereld-Web-App voor Azure.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: b2f42e0e7a5b98760ec02fab2fc38f9f07b1156b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a>Een eenvoudige Azure-web-app met behulp van Eclipse maken
Deze zelfstudie laat zien hoe toocreate en een eenvoudige Hallo wereld toepassing tooAzure implementeren als een Web-App met behulp van Hallo [Azure Toolkit voor Eclipse]. Een eenvoudige JSP-voorbeeld voor eenvoud wordt weergegeven, maar gelijksoortige stappen zou zijn geschikt voor een servlet Java wat betreft Azure-implementatie is.

Wanneer u deze zelfstudie hebt voltooid, ziet uw toepassing vergelijkbare toohello afbeelding volgen wanneer u deze in een webbrowser bekijken:

![Voorbeeld van Hallo wereld-app][01]

## <a name="prerequisites"></a>Vereisten
* Een Java Developer Kit (JDK), v 1.8 of hoger.
* Eclipse IDE voor Java EE-ontwikkelaars, standaard of hoger. Dit kan worden gedownload vanaf <http://www.eclipse.org/downloads/>.
* Een distributiepunt van een Java gebaseerde webserver of toepassingsserver, zoals [Apache Tomcat] of [Jetty].
* Een Azure-abonnement, die kan worden opgehaald uit <https://azure.microsoft.com/free/> of <http://azure.microsoft.com/pricing/purchase-options/>.
* Hallo [Azure Toolkit voor Eclipse]. Zie voor meer informatie over het installeren van hello Azure Toolkit [installeren hello Azure Toolkit voor Eclipse].

## <a name="toocreate-a-hello-world-application"></a>een toepassing Hello World toocreate
Eerst beginnen we uitschakelen met een Java-project maken.

1. Start Eclipse en op Hallo-menu op **bestand**, klikt u op **nieuw**, en klik vervolgens op **dynamisch webproject**. (Als er geen **dynamisch webproject** vermeld als een project beschikbaar wanneer u op **bestand** en **nieuw**, vervolgens Hallo te volgen: klik op **bestand**, klikt u op **nieuw**, klikt u op **Project...** , vouw **Web**, klikt u op **dynamisch webproject**, en klik op **volgende**.)
2. Naam voor deze zelfstudie Hallo project **MyWebApp**. Het scherm wordt vergelijkbaar toohello volgende weergegeven:
   
    ![Een nieuw Dynamic Web Project maken][02]
3. Klik op **Voltooien**.
4. Vouw in de weergave Project Explorer van Eclipse **MyWebApp**. Klik met de rechtermuisknop op **WebContent**(Webinhoud) en klik vervolgens op **New** (Nieuw) en **JSP File** (JSP-bestand).
5. In Hallo **nieuw JSP-bestand** in het dialoogvenster, naam Hallo bestand **index.jsp**, houden Hallo bovenliggende map als **MyWebApp/WebContent**, en klik vervolgens op **volgende**.
6. In Hallo **JSP-sjabloon selecteren** in het dialoogvenster voor de doeleinden van deze zelfstudie geselecteerd **nieuw JSP-bestand (html)**, en klik vervolgens op **voltooien**.
7. Wanneer het bestand index.jsp wordt geopend in Eclipse, toevoegen in toodynamically tekstweergave **Hello World!** binnen de bestaande Hallo `<body>` element. Uw bijgewerkte `<body>` inhoud moet eruitzien als Hallo voorbeeld te volgen:
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
8. Index.jsp opslaan.

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a>toodeploy uw toepassing tooan Azure Web App-Container
Er zijn verschillende manieren waarop u een Java web application tooAzure kunt implementeren. Deze zelfstudie wordt beschreven in een van de eenvoudigste Hallo: uw toepassing worden geïmplementeerde tooan Azure Web App-Container - geen speciale projecttype of extra hulpprogramma's nodig zijn. Hallo JDK en Hallo web container software worden geleverd voor u door Azure, zodat er geen noodzaak tooupload uw eigen; u hoeft uw Java-Web-App is. Als gevolg hiervan wordt publicatieproces voor uw toepassing hello seconden, niet minuten duren.

1. In de Projectverkenner van Eclipse met de rechtermuisknop op **MyWebApp**.
2. Selecteer in het contextmenu hello, **Azure**, klikt u vervolgens op **publiceren als Azure-Web-App...**
   
    ![Als Azure-Web-App publiceren][03]
   
    U kunt ook terwijl uw toepassing webproject in Hallo Projectverkenner is geselecteerd, klikt u op Hallo **publiceren** vervolgkeuzeknop op Hallo werkbalk en selecteer **publiceren als Azure-Web-App** van daaruit:
   
    ![Als Azure-Web-App publiceren][14]
3. Als u hebt nog niet aangemeld bij Azure van Eclipse, kunt u zich na vragen aan gebruiker toosign in uw Azure-account:
   
    ![Azure Sign In het dialoogvenster][04]
   
    Als er meerdere Azure-accounts, aantal Hallo prompts tijdens Hallo aanmelden proces worden mogelijk weergegeven meer dan één keer, zelfs als ze worden weergegeven toobe Hallo dezelfde. Als dit gebeurt, blijven Hallo aanmelden instructies te volgen.
4. Nadat u bent aangemeld bij uw Azure-account, Hallo **abonnementen beheren** in het dialoogvenster een lijst met abonnementen die gekoppeld aan uw referenties zijn worden weergegeven. Als er meerdere abonnementen die worden vermeld en toowork met alleen een specifieke subset ervan gewenste, kan u eventueel Hallo die u wilt dat toouse uitschakelen. Wanneer u uw abonnementen hebt geselecteerd, klikt u op **sluiten**.
   
    ![Dialoogvenster abonnementen beheren][05]
5. Wanneer Hallo **tooAzure Web-App-Container implementeren** dialoogvenster wordt weergegeven, wordt deze in een Web-App-containers die u eerder hebt gemaakt weergegeven; als u geen containers niet gemaakt hebt, Hallo lijst is leeg.
   
    ![Dialoogvenster tooAzure-Web-App-Container implementeren][06]
6. Als u geen hebt gemaakt een Azure-Web-App-Container vóór of als u wilt toopublish uw toepassing tooa nieuwe container, gebruik Hallo stappen te volgen. Anders selecteert u een bestaande Web-App-Container en toostep 7 hieronder overslaan.
   
   1. Klik op **nieuwe...**
      
       ![Dialoogvenster tooAzure-Web-App-Container implementeren][15]
   2. Hallo **nieuwe Web-App-Container** in het dialoogvenster wordt weergegeven:
      
       ![Dialoogvenster Nieuwe Web-App-Container][07a]
   3. Voer een **DNS-Label** voor uw Web-App-Container; vormt dit Hallo leaf DNS-label van Hallo host-URL voor uw webtoepassing in Azure. (Houd er rekening mee dat Hallo-naam moet beschikbaar zijn en voldoen naamgevingsvereisten tooAzure voor Web-App.)
   4. In Hallo **webcontainer** vervolgkeuzelijst, selecteer Hallo geschikte software voor uw toepassing.
      
       U kunt op dit moment van Tomcat-8, 7 Tomcat of Jetty 9. Een recente distributie van software Hallo geselecteerd door Azure worden verstrekt en het wordt uitgevoerd op een recente verdeling van JDK 8 gemaakt door Oracle en geleverd door Azure.
   5. In Hallo **abonnement** vervolgkeuzelijst, selecteer Hallo abonnement gewenste toouse voor deze implementatie.
   6. In Hallo **resourcegroep** vervolgkeuzelijst, selecteer Hallo resourcegroep waarmee u tooassociate uw Web-App wilt. (Azure resourcegroepen kunt u toogroup verwante resources samen zodat bijvoorbeeld ze samen kunnen worden verwijderd.)
      
       U kunt een bestaande resourcegroep selecteren (als u een hebt) en overslaan toostep g onderstaande of gebruik Hallo na deze stappen een nieuwe resourcegroep toocreate:
      
      * Klik op **nieuwe...**
      * Hallo **nieuwe resourcegroep** in het dialoogvenster wordt weergegeven:
        
          ![Dialoogvenster nieuwe resourcegroep][08]
      * In Hallo Hallo **naam** textbox, Geef een naam voor uw nieuwe resourcegroep.
      * In Hallo Hallo **regio** vervolgkeuzelijst, selecteer Hallo juiste Azure datacentrum locatie voor de resourcegroep.
      * Optioneel: Standaard een recente verdeling van Java 8 worden geïmplementeerd door Azure automatisch tooyour webcontainer app als uw JVM. U kunt echter een andere versie en de distributie van Hallo JVM opgeven als dit vereist is voor uw Web-App. toospecify hello JDK voor uw Web-App klikt u op Hallo **JDK** tabblad en selecteer een van Hallo volgende opties:
        
        * **Hallo standaard JDK die worden aangeboden door de service Azure Web Apps implementeren**: deze optie wordt een recente verdeling van Java 8 implementeren.
        * **Een 3e party JDK die beschikbaar zijn in Azure implementeren**: deze optie kunt u toochoose uit Hallo lijst met JDKs die worden geleverd door Microsoft Azure.
        * **Mijn eigen JDK vanaf deze downloadlocatie implementeren**: deze optie kunt u toospecify uw eigen JDK-distributiepunt dat als een ZIP-bestand moet worden verpakt en geüpload tooeither een openbaar downloadlocatie of een Azure storage-account waarvoor u toegang hebben.
          
          ![Dialoogvenster Nieuwe Web-App-Container][07b]
   7. Klik op **OK**.
   8. Hallo **App Service-Plan** vervolgkeuzelijst bevat Hallo-app service-abonnementen die zijn gekoppeld aan Hallo resourcegroep die u hebt geselecteerd. (Informatie zoals Hallo-locatie van uw Web-App Hallo prijscategorie en Hallo compute exemplaargrootte app Service-abonnementen opgeven. Een enkele App Service-Plan kan worden gebruikt voor meerdere Web-Apps, dat is waarom deze afzonderlijk van een specifieke implementatie van Web-App onderhouden.)
      
       Selecteer een bestaand App Service-abonnement (als u een hebt) en toostep h onderstaande overslaan of na deze stappen toocreate een nieuwe App Service-Plan hello gebruiken:
      
      * Klik op **nieuwe...**
      * Hallo **nieuwe App Service-Plan** in het dialoogvenster wordt weergegeven:
        
          ![Nieuwe App Service-Plan in het dialoogvenster][09]
      * In Hallo Hallo **naam** textbox, Geef een naam voor uw nieuwe App Service-Plan.
      * In Hallo Hallo **locatie** vervolgkeuzelijst, selecteer Hallo juiste Azure datacentrum locatie voor Hallo plan.
      * In Hallo Hallo **prijscategorie** vervolgkeuzelijst, selecteer Hallo toepasselijke prijzen voor Hallo plan. Voor testdoeleinden kunt u **vrije**.
      * In Hallo Hallo **Exemplaargrootte** vervolgkeuzelijst, selecteer Hallo juiste exemplaargrootte voor Hallo plan. Voor testdoeleinden kunt u **kleine**.
   9. Nadat u alle Hallo bovenstaande stappen hebt voltooid, ziet er Hallo nieuwe Web-App-Container dialoogvenster Hallo volgende afbeelding:
      
       ![Dialoogvenster Nieuwe Web-App-Container][10]
   10. Klik op **OK** toocomplete Hallo maken van uw nieuwe Web-App-container.
       
        Wacht een paar seconden voor Hallo lijst met Hallo Web-App containers toobe vernieuwd en de zojuist gemaakte web-app-container moet nu worden geselecteerd in het Hallo-lijst.
7. U bent nu klaar toocomplete Hallo initiële implementatie van uw Web-App-tooAzure:
   
    ![Dialoogvenster tooAzure-Web-App-Container implementeren][11]
   
    Klik op **OK** toodeploy uw Java-toepassing toohello geselecteerd Web-App-container.
   
    Standaard wordt uw toepassing wordt geïmplementeerd als een submap van de toepassingsserver Hallo. Als u toobe geïmplementeerd als de hoofdtoepassing hello wilt, Controleer Hallo **implementeren tooroot** selectievakje voordat u op **OK**.
8. Vervolgens ziet u Hallo **Azure Activity Log** waarmee wordt aangegeven Hallo implementatiestatus van uw Web-App bekijken.
   
    ![Azure Activity Log][12]
   
    Hallo-proces voor het implementeren van uw Web-App tooAzure duurt slechts enkele seconden toocomplete. Wanneer uw toepassing ready, ziet u een koppeling met de naam **gepubliceerde** in Hallo **Status** kolom. Wanneer u Hallo koppeling klikt, wordt uitgevoerd, u startpagina tooyour geïmplementeerd van Web-App.

## <a name="updating-your-web-app"></a>De web-app beveiligen
Bijwerken van een bestaande Azure-Web-App uitgevoerd is een snelle en eenvoudige proces en hebt u twee opties voor het bijwerken van:

* U kunt Hallo-implementatie van een bestaande Java-Web-App kunt bijwerken.
* U kunt een extra toohello voor Java-toepassing publiceren dezelfde Web-App-Container.

In beide gevallen Hallo proces identieke en duurt slechts enkele seconden:

1. Hallo Eclipse-project explorer met de rechtermuisknop op Hallo Java-toepassing die u wilt dat tooupdate of tooan bestaande Web-App-Container toevoegen.
2. Wanneer het Hallo-contextmenu wordt weergegeven, selecteert u **Azure** en vervolgens **publiceren als Azure-Web-App...**
3. Nadat u hebt al aangemeld eerder, ziet u een lijst met uw bestaande Web-App-containers. Selecteer een of wilt u toopublish opnieuw publiceren, uw Java-toepassing tooand Klik Hallo **OK**.

Een paar seconden later Hallo **Azure Activity Log** weer uw bijgewerkte implementatie als **gepubliceerde** en u kunt tooverify uw bijgewerkte toepassing in een webbrowser worden.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Starten, stoppen of opnieuw starten van een bestaande web-app
toostart of stoppen van een bestaande Azure-Web-App-container (inclusief alle Hallo geïmplementeerd Java-toepassingen in deze), kunt u Hallo **Azure Explorer** weergeven.

Als hello **Azure Explorer** weergave nog niet is geopend, kunt u deze openen door te klikken op vervolgens **venster** menu in Eclipse, klikt u vervolgens op **weergave tonen**, klikt u vervolgens **andere...** , klikt u vervolgens **Azure**, en klik vervolgens op **Azure Explorer**. Als u eerder niet hebt aangemeld, wordt u gevraagd toodo dus.

Wanneer Hallo **Azure Explorer** weergave wordt weergegeven, gebruik Volg deze stappen toostart of stoppen van uw Web-App: 

1. Vouw Hallo **Azure** knooppunt.
2. Vouw Hallo **Web-Apps** knooppunt. 
3. Klik met de rechtermuisknop Hallo gewenste Web-App.
4. Wanneer het Hallo-contextmenu wordt weergegeven, klikt u op **Start**, **stoppen**, of **opnieuw**. Houd er rekening mee dat Hallo menu-Opties contextbewuste, zijn zodat u kunt alleen een actieve WebApp stoppen of starten van een web-app die niet wordt uitgevoerd.
   
    ![Stoppen van een bestaande Web-App][13]

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over hello Azure Toolkits voor IDE voor Java Hallo koppelingen te volgen:

* [Azure Toolkit voor Eclipse]
  * [installeren hello Azure Toolkit voor Eclipse]
  * *Een Hallo wereld Web-App maken voor Azure in Eclipse (in dit artikel)*
  * [Wat is er nieuw in hello Azure Toolkit voor Eclipse]
* [Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)
  * [Hello Azure Toolkit voor IntelliJ installeren]
  * [Een Hallo wereld Web-App maken voor Azure in IntelliJ]
  * [Wat is er nieuw in hello Azure Toolkit voor IntelliJ]

Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center].

Zie voor meer informatie over het maken van Azure Web Apps Hallo [overzicht van Web Apps].

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Azure Toolkit voor Eclipse]: ../azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)
[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Een Hallo wereld Web-App maken voor Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[installeren hello Azure Toolkit voor Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[Hello Azure Toolkit voor IntelliJ installeren]: ../azure-toolkit-for-intellij-installation.md
[Wat is er nieuw in hello Azure Toolkit voor Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md
[Wat is er nieuw in hello Azure Toolkit voor IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[overzicht van Web Apps]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-eclipse-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-eclipse-create-hello-world-web-app/02-Dynamic-Web-Project.png
[03]: ./media/app-service-web-eclipse-create-hello-world-web-app/03-Context-Menu.png
[04]: ./media/app-service-web-eclipse-create-hello-world-web-app/04-Log-In-Dialog.png
[05]: ./media/app-service-web-eclipse-create-hello-world-web-app/05-Manage-Subscriptions-Dialog.png
[06]: ./media/app-service-web-eclipse-create-hello-world-web-app/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/app-service-web-eclipse-create-hello-world-web-app/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/app-service-web-eclipse-create-hello-world-web-app/07b-New-Web-App-Container-Dialog.png
[08]: ./media/app-service-web-eclipse-create-hello-world-web-app/08-New-Resource-Group-Dialog.png
[09]: ./media/app-service-web-eclipse-create-hello-world-web-app/09-New-Service-Plan-Dialog.png
[10]: ./media/app-service-web-eclipse-create-hello-world-web-app/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/app-service-web-eclipse-create-hello-world-web-app/11-Completed-Deploy-Dialog.png
[12]: ./media/app-service-web-eclipse-create-hello-world-web-app/12-Activity-Log-View.png
[13]: ./media/app-service-web-eclipse-create-hello-world-web-app/13-Azure-Explorer-Web-App.png
[14]: ./media/app-service-web-eclipse-create-hello-world-web-app/14-publishDropdownButton.png
[15]: ./media/app-service-web-eclipse-create-hello-world-web-app/15-New-Azure-Web-Container.png
