---
title: Maken van een eenvoudige Azure-web-app met behulp van Eclipse | Microsoft Docs
description: Deze zelfstudie laat zien hoe u met de Azure-werkset voor Eclipse een Hello World Web-App maken voor Azure.
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
ms.openlocfilehash: 683d6828546995a4dc60d8cac0669f356501c723
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a>Een eenvoudige Azure-web-app met behulp van Eclipse maken
Deze zelfstudie laat zien hoe maken en implementeren van een eenvoudige toepassing van Hallo wereld naar Azure als een Web-App met behulp van de [Azure Toolkit voor Eclipse]. Een eenvoudige JSP-voorbeeld voor eenvoud wordt weergegeven, maar gelijksoortige stappen zou zijn geschikt voor een servlet Java wat betreft Azure-implementatie is.

Wanneer u deze zelfstudie hebt voltooid, ziet uw toepassing er ongeveer als de volgende afbeelding wanneer u deze in een webbrowser bekijken:

![Voorbeeld van Hallo wereld-app][01]

## <a name="prerequisites"></a>Vereisten
* Een Java Developer Kit (JDK), v 1.8 of hoger.
* Eclipse IDE voor Java EE-ontwikkelaars, standaard of hoger. Dit kan worden gedownload vanaf <http://www.eclipse.org/downloads/>.
* Een distributiepunt van een Java gebaseerde webserver of toepassingsserver, zoals [Apache Tomcat] of [Jetty].
* Een Azure-abonnement, die kan worden opgehaald uit <https://azure.microsoft.com/free/> of <http://azure.microsoft.com/pricing/purchase-options/>.
* De [Azure Toolkit voor Eclipse]. Zie voor meer informatie over het installeren van de Azure-Toolkit [installeren van de Azure-werkset voor Eclipse].

## <a name="to-create-a-hello-world-application"></a>Een toepassing Hello World maken
Eerst beginnen we uitschakelen met een Java-project maken.

1. Start Eclipse en klik op het menu **bestand**, klikt u op **nieuw**, en klik vervolgens op **dynamisch webproject**. (Als er geen **dynamisch webproject** vermeld als een project beschikbaar wanneer u op **bestand** en **nieuw**, doet u het volgende: klik op **bestand**, klikt u op **nieuw**, klikt u op **Project...** , vouw **Web**, klikt u op **dynamisch webproject**, en klik op **volgende**.)
2. Noem het project voor deze zelfstudie **MyWebApp**. Uw scherm ziet er ongeveer als volgt:
   
    ![Een nieuw Dynamic Web Project maken][02]
3. Klik op **Voltooien**.
4. Vouw in de weergave Project Explorer van Eclipse **MyWebApp**. Klik met de rechtermuisknop op **WebContent**(Webinhoud) en klik vervolgens op **New** (Nieuw) en **JSP File** (JSP-bestand).
5. In de **nieuw JSP-bestand** in het dialoogvenster de naam van het bestand **index.jsp**, bewaar de bovenliggende map als **MyWebApp/WebContent**, en klik vervolgens op **volgende**.
6. In de **JSP-sjabloon selecteren** in het dialoogvenster voor de doeleinden van deze zelfstudie geselecteerd **nieuw JSP-bestand (html)**, en klik vervolgens op **voltooien**.
7. Wanneer het bestand index.jsp wordt geopend in Eclipse, toevoegen in de tekst die moet dynamisch weergeven **Hello World!** in het bestaande `<body>`-element. Uw bijgewerkte `<body>` inhoud moet eruitzien als in het volgende voorbeeld:
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
8. Index.jsp opslaan.

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a>Voor het implementeren van uw toepassing in een Azure-Web-App-Container
Er zijn verschillende manieren waarop u een Java-webtoepassing naar Azure kunt implementeren. Deze zelfstudie wordt beschreven in een van de eenvoudigste: uw toepassing wordt geïmplementeerd op een Azure-Web-App-Container - geen speciale projecttype of extra hulpprogramma's nodig zijn. De JDK en de software van de container web worden geleverd voor u door Azure, zodat er geen nodig is voor het uploaden van uw eigen; u hoeft uw Java-Web-App is. Als gevolg hiervan wordt het publicatieproces voor uw toepassing seconden, niet minuten duren.

1. In de Projectverkenner van Eclipse met de rechtermuisknop op **MyWebApp**.
2. Selecteer in het contextmenu **Azure**, klikt u vervolgens op **publiceren als Azure-Web-App...**
   
    ![Als Azure-Web-App publiceren][03]
   
    Terwijl uw webproject van toepassing is geselecteerd in de Projectverkenner, u kunt ook klikken op de **publiceren** vervolgkeuzeknop op de werkbalk en selecteer **publiceren als Azure-Web-App** van daaruit:
   
    ![Als Azure-Web-App publiceren][14]
3. Als u hebt nog niet aangemeld bij Azure van Eclipse, wordt u gevraagd om aan te melden bij uw Azure-account:
   
    ![Azure Sign In het dialoogvenster][04]
   
    Als er meerdere Azure-accounts, enkele van de prompts tijdens de aanmelding in proces worden mogelijk weergegeven meer dan één keer, zelfs als ze niet dezelfde worden weergegeven. Wanneer dit gebeurt, blijven na het aanmelden instructies.
4. Nadat u zich heeft aangemeld bij uw Azure-account, de **abonnementen beheren** in het dialoogvenster een lijst met abonnementen die gekoppeld aan uw referenties zijn worden weergegeven. Als er meerdere abonnementen weergegeven en u wilt werken met alleen een specifieke subset ervan, kan u eventueel schakelt u degene die u wilt gebruiken. Wanneer u uw abonnementen hebt geselecteerd, klikt u op **sluiten**.
   
    ![Dialoogvenster abonnementen beheren][05]
5. Wanneer de **implementeren in Azure Web App-Container** dialoogvenster wordt weergegeven, wordt deze in een Web-App-containers die u eerder hebt gemaakt weergegeven; als u geen containers niet gemaakt hebt, wordt de lijst leeg zijn.
   
    ![Het dialoogvenster Azure Web App-Container te implementeren][06]
6. Als u een Azure Web App-Container voordat niet hebt gemaakt, of als u uw toepassing naar een nieuwe container publiceren, gebruikt u de volgende stappen uit. Anders selecteert u een bestaande Web-App-Container en gaat u verder met stap 7 hieronder.
   
   1. Klik op **nieuwe...**
      
       ![Het dialoogvenster Azure Web App-Container te implementeren][15]
   2. De **nieuwe Web-App-Container** in het dialoogvenster wordt weergegeven:
      
       ![Dialoogvenster Nieuwe Web-App-Container][07a]
   3. Voer een **DNS-Label** voor uw Web-App-Container; vormt dit het leaf DNS-label van de host-URL voor uw webtoepassing in Azure. (Houd er rekening mee dat de naam moet beschikbaar zijn en voldoen aan de naamgeving van de vereisten voor Azure-webtoepassing.)
   4. In de **webcontainer** vervolgkeuzelijst, selecteer de juiste software voor uw toepassing.
      
       U kunt op dit moment van Tomcat-8, 7 Tomcat of Jetty 9. Een recente distributie van de geselecteerde software door Azure worden verstrekt en het wordt uitgevoerd op een recente verdeling van JDK 8 gemaakt door Oracle en geleverd door Azure.
   5. In de **abonnement** vervolgkeuzelijst, selecteer het abonnement dat u wilt gebruiken voor deze implementatie.
   6. In de **resourcegroep** vervolgkeuzelijst, selecteer de resourcegroep die u wilt koppelen van uw Web-App. (Azure resourcegroepen kunt u voor het groeperen van gerelateerde resources samen zodat bijvoorbeeld ze samen kunnen worden verwijderd.)
      
       U kunt Selecteer een bestaande resourcegroep (als u een hebt) en overslaan naar stap g onderstaande of gebruikt u de volgende deze stappen uit om een nieuwe resourcegroep maken:
      
      * Klik op **nieuwe...**
      * De **nieuwe resourcegroep** in het dialoogvenster wordt weergegeven:
        
          ![Dialoogvenster nieuwe resourcegroep][08]
      * In de de **naam** textbox, Geef een naam voor uw nieuwe resourcegroep.
      * In de de **regio** vervolgkeuzelijst, selecteer de juiste Azure datacentrum locatie voor de resourcegroep.
      * Optioneel: Standaard een recente verdeling van Java 8 wordt geïmplementeerd door Azure automatisch aan uw web-app-container als uw JVM. U kunt echter een andere versie en de distributie van de JVM opgeven als dit vereist is voor uw Web-App. Als u de JDK die voor uw Web-App, klikt u op de **JDK** tabblad en selecteer een van de volgende opties:
        
        * **De standaardwaarde JDK die worden aangeboden door de service Azure Web Apps implementeren**: deze optie wordt een recente verdeling van Java 8 implementeren.
        * **Een 3e party JDK die beschikbaar zijn in Azure implementeren**: deze optie kunt u kiezen uit de lijst met JDKs die worden geleverd door Microsoft Azure.
        * **Mijn eigen JDK vanaf deze downloadlocatie implementeren**: deze optie kunt u uw eigen JDK-distributie, die moet worden geleverd als een ZIP-bestand en geüpload naar een openbaar downloadlocatie of waarvoor u hebt Azure storage-account opgeven toegang.
          
          ![Dialoogvenster Nieuwe Web-App-Container][07b]
   7. Klik op **OK**.
   8. De **App Service-Plan** vervolgkeuzelijst geeft een lijst van de app service-abonnementen die zijn gekoppeld aan de resourcegroep die u hebt geselecteerd. (App Service-abonnementen geven informatie zoals de locatie van uw Web-App, de prijscategorie en de grootte van de compute-exemplaar. Een enkele App Service-Plan kan worden gebruikt voor meerdere Web-Apps, dat is waarom deze afzonderlijk van een specifieke implementatie van Web-App onderhouden.)
      
       U kunt een bestaand App Service-abonnement (als u een hebt) en overslaan voor selecteren h onderstaande stap of gebruikt u de volgende deze stappen voor het maken van een nieuwe App Service-Plan:
      
      * Klik op **nieuwe...**
      * De **nieuwe App Service-Plan** in het dialoogvenster wordt weergegeven:
        
          ![Nieuwe App Service-Plan in het dialoogvenster][09]
      * In de de **naam** textbox, Geef een naam voor uw nieuwe App Service-Plan.
      * In de de **locatie** vervolgkeuzelijst, selecteer de juiste Azure datacentrum locatie voor het plan.
      * In de de **prijscategorie** vervolgkeuzelijst, selecteer de juiste prijs voor het plan. Voor testdoeleinden kunt u **vrije**.
      * In de de **Exemplaargrootte** vervolgkeuzelijst, selecteer het juiste exemplaar grootte voor het plan. Voor testdoeleinden kunt u **kleine**.
   9. Nadat u alle bovenstaande stappen hebt voltooid, moet het dialoogvenster Nieuwe Web-App-Container zijn vergelijkbaar met de volgende afbeelding:
      
       ![Dialoogvenster Nieuwe Web-App-Container][10]
   10. Klik op **OK** voor het maken van uw nieuwe Web-App-container niet voltooien.
       
        Wacht een paar seconden voor een overzicht van de Web-App-containers worden vernieuwd en de zojuist gemaakte web-app-container moet nu worden geselecteerd in de lijst.
7. U bent nu klaar voor het uitvoeren van de eerste implementatie van uw Web-App in Azure:
   
    ![Het dialoogvenster Azure Web App-Container te implementeren][11]
   
    Klik op **OK** voor het implementeren van uw Java-toepassing aan de geselecteerde container van Web-App.
   
    Standaard wordt uw toepassing wordt geïmplementeerd als een submap van de toepassingsserver. Als u wilt dat deze worden geïmplementeerd als de hoofdtoepassing, controleert u de **implementeren in de hoofdmap** selectievakje voordat u op **OK**.
8. Vervolgens ziet u de **Azure Activity Log** weergave, die de status van de implementatie van uw Web-App wordt aangegeven.
   
    ![Azure Activity Log][12]
   
    Het proces voor het implementeren van uw Web-App naar Azure duren slechts een paar seconden. Wanneer uw toepassing ready, ziet u een koppeling met de naam **gepubliceerde** in de **Status** kolom. Wanneer u op de koppeling klikt, duurt het u naar de startpagina van de geïmplementeerde Web-App.

## <a name="updating-your-web-app"></a>De web-app beveiligen
Bijwerken van een bestaande Azure-Web-App uitgevoerd is een snelle en eenvoudige proces en hebt u twee opties voor het bijwerken van:

* U kunt de implementatie van een bestaande Java-Web-App kunt bijwerken.
* U kunt een extra Java-toepassing tot dezelfde Container voor de Web-App publiceren.

In beide gevallen is het proces identieke en duurt slechts enkele seconden:

1. In de Projectverkenner Eclipse met de rechtermuisknop op de Java-toepassing die u wilt bijwerken of toevoegen aan een bestaande Web-App-Container.
2. Wanneer het contextmenu wordt weergegeven, selecteert u **Azure** en vervolgens **publiceren als Azure-Web-App...**
3. Nadat u hebt al aangemeld eerder, ziet u een lijst met uw bestaande Web-App-containers. Selecteer de gewenste publiceren of uw Java-toepassing opnieuw te publiceren en klik op **OK**.

Een paar seconden later, de **Azure Activity Log** weer uw bijgewerkte implementatie als **gepubliceerde** en u kunt controleren of uw bijgewerkte toepassing in een webbrowser.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Starten, stoppen of opnieuw starten van een bestaande web-app
Om te starten of stoppen van een bestaande Azure-Web-App-container (en alle geïmplementeerde Java-toepassingen erin), kunt u de **Azure Explorer** weergeven.

Als de **Azure Explorer** weergave nog niet is geopend, kunt u deze openen door te klikken op vervolgens **venster** menu in Eclipse, klikt u vervolgens op **weergave tonen**, klikt u vervolgens **andere...** , klikt u vervolgens **Azure**, en klik vervolgens op **Azure Explorer**. Als u eerder niet hebt aangemeld, wordt u gevraagd.

Wanneer de **Azure Explorer** weergave wordt weergegeven, gebruik als volgt te werk om te starten of stoppen van uw Web-App: 

1. Vouw de **Azure** knooppunt.
2. Vouw de **Web-Apps** knooppunt. 
3. Met de rechtermuisknop op de gewenste Web-App.
4. Wanneer het contextmenu wordt weergegeven, klikt u op **Start**, **stoppen**, of **opnieuw**. Houd er rekening mee dat de menu-Opties contextbewuste, zijn zodat u kunt alleen een actieve WebApp stoppen of starten van een web-app die niet wordt uitgevoerd.
   
    ![Stoppen van een bestaande Web-App][13]

## <a name="next-steps"></a>Volgende stappen
Voor meer informatie over de Azure Toolkits voor Java-IDE's klikt u op de volgende koppelingen:

* [Azure Toolkit voor Eclipse]
  * [installeren van de Azure-werkset voor Eclipse] (De Azure Toolkit voor Eclipse installeren)
  * *Een Hallo wereld Web-App maken voor Azure in Eclipse (in dit artikel)*
  * [What's New in the Azure Toolkit for Eclipse] (Nieuw in de Azure Toolkit voor Eclipse)
* [Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)
  * [Installing the Azure Toolkit for IntelliJ] (De Azure Toolkit voor IntelliJ installeren)
  * [Een Hallo wereld Web-App maken voor Azure in IntelliJ]
  * [What's New in the Azure Toolkit for IntelliJ] (Nieuw in de Azure Toolkit voor IntelliJ)

In het [Azure Java Developer Center] vindt u meer informatie over het gebruik van Azure met Java.

Zie voor meer informatie over het maken van Azure Web Apps, de [overzicht van Web Apps].

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Azure Toolkit voor Eclipse]: ../azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)
[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Een Hallo wereld Web-App maken voor Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[installeren van de Azure-werkset voor Eclipse]: ../azure-toolkit-for-eclipse-installation.md (De Azure Toolkit voor Eclipse installeren)
[Installing the Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-installation.md (De Azure Toolkit voor IntelliJ installeren)
[What's New in the Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md (Nieuw in de Azure Toolkit voor Eclipse)
[What's New in the Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md (Nieuw in de Azure Toolkit voor IntelliJ)

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
