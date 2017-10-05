---
title: Een eenvoudige Azure-web-app maken in IntelliJ | Microsoft Docs
description: Deze zelfstudie laat zien hoe de Azure-werkset voor IntelliJ gebruiken voor het maken van een Hello World Web-App voor Azure.
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
ms.openlocfilehash: 20b2c3d86f5bde9302647f345aa99b030d78613a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a>Een eenvoudige Azure-web-app maken in IntelliJ
Deze zelfstudie laat zien hoe maken en implementeren van een eenvoudige toepassing van Hallo wereld naar Azure als een Web-App met behulp van de [Azure Toolkit voor IntelliJ]. Een eenvoudige JSP-voorbeeld voor eenvoud wordt weergegeven, maar gelijksoortige stappen zou zijn geschikt voor een servlet Java wat betreft Azure-implementatie is.

Wanneer u deze zelfstudie hebt voltooid, ziet uw toepassing er ongeveer als de volgende afbeelding wanneer u deze in een webbrowser bekijken:

![Voorbeeldwebpagina][01]

## <a name="prerequisites"></a>Vereisten
* Een Java Developer Kit (JDK), v 1.8 of hoger.
* IntelliJ IDEA Ultimate Edition. Dit kan worden gedownload vanaf <https://www.jetbrains.com/idea/download/index.html>.
* Een distributiepunt van een Java gebaseerde webserver of toepassingsserver, zoals [Apache Tomcat] of [Jetty].
* Een Azure-abonnement, die kan worden opgehaald uit <https://azure.microsoft.com/free/> of <http://azure.microsoft.com/pricing/purchase-options/>.
* De [Azure Toolkit voor IntelliJ]. Zie voor meer informatie over het installeren van de Azure-Toolkit [Toolkit Azure installeren voor IntelliJ].

## <a name="to-create-a-hello-world-application"></a>Een toepassing Hello World maken
Eerst beginnen we uitschakelen met een Java-project maken.

1. IntelliJ Start en klik op de **bestand** menu, klikt u vervolgens op **nieuw**, en klik vervolgens op **Project**.
   
    ![Bestand Nieuw Project][02]
2. Selecteer in het dialoogvenster Nieuw Project **Java**, klikt u vervolgens **webtoepassing**, en klik vervolgens op **nieuw** toevoegen van een Project-SDK.
   
    ![Het dialoogvenster Nieuw project][03a]
   
3. Selecteer de map waarin uw JDK is geïnstalleerd en klik vervolgens op in de basismap selecteren voor het dialoogvenster JDK, **OK**. Klik op **volgende** in het dialoogvenster Nieuw Project om door te gaan.
   
    ![Basismap van de JDK opgeven][03b]
4. Noem het project voor deze zelfstudie **Java-Web-App-op-Azure**, en klik vervolgens op **voltooien**.
   
    ![Het dialoogvenster Nieuw project][04]
5. Vouw in de weergave Project Explorer van IntelliJ **Java-Web-App-op-Azure**, vouw vervolgens **web**, en dubbelklik vervolgens op **index.jsp**.
   
    ![Open indexpagina][05c]
6. Wanneer het bestand index.jsp wordt geopend in IntelliJ, toevoegen in de tekst die moet dynamisch weergeven **Hello World!** in het bestaande `<body>`-element. Uw bijgewerkte `<body>` inhoud moet eruitzien als in het volgende voorbeeld:
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. Index.jsp opslaan.

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a>Voor het implementeren van uw toepassing in een Azure-Web-App-Container
Er zijn verschillende manieren waarop u een Java-webtoepassing naar Azure kunt implementeren. Deze zelfstudie wordt beschreven in een van de eenvoudigste: uw toepassing wordt geïmplementeerd op een Azure-Web-App-Container - geen speciale projecttype of extra hulpprogramma's nodig zijn. De JDK en de software van de container web worden geleverd voor u door Azure, zodat er geen nodig is voor het uploaden van uw eigen; u hoeft uw Java-Web-App is. Als gevolg hiervan wordt het publicatieproces voor uw toepassing seconden, niet minuten duren.

Voordat u uw toepassing publiceren, moet u eerst uw module-instellingen configureren. Volg hiervoor de volgende stappen:

1. In de IntelliJ Projectverkenner met de rechtermuisknop op de **Java-Web-App-op-Azure** project. Wanneer het contextmenu wordt weergegeven, klikt u op **Open Module-instellingen**.

    ![Open de Module-instellingen][05a]
2. Wanneer het projectstructuur dialoogvenster wordt weergegeven:

   a. Klik op **artefacten** in de lijst met **projectinstellingen**.
   b. Wijzig de naam van het artefact in de **naam** vak zodat het geen spaties of speciale tekens bevat; dit is nodig omdat de naam wordt gebruikt in de Uniform Resource Identifier (URI).
   c. Wijzig de **Type** naar **webtoepassing: archief**.
   d. Klik op **OK** om het projectstructuur dialoogvenster te sluiten.

    ![Open de Module-instellingen][05b]

Wanneer u uw module-instellingen hebt geconfigureerd, kunt u uw toepassing in Azure publiceren met behulp van de volgende stappen uit:

1. In de IntelliJ Projectverkenner met de rechtermuisknop op de **Java-Web-App-op-Azure** project. Wanneer het contextmenu wordt weergegeven, selecteert u **Azure**, en klik vervolgens op **publiceren als Azure-Web-App...**
   
    ![Azure contextmenu publiceren][06]
2. Als u hebt nog niet aangemeld bij Azure van IntelliJ, wordt u gevraagd om aan te melden bij uw Azure-account. (Als er meerdere Azure-accounts, enkele van de prompts tijdens de aanmelding in proces worden mogelijk weergegeven meer dan één keer, zelfs als ze niet dezelfde worden weergegeven. Als dit gebeurt, blijven de aanmeldingspagina instructies te volgen.)
   
    ![Azure-logboekanalyse In het dialoogvenster][07]
3. Nadat u zich heeft aangemeld bij uw Azure-account, de **abonnementen beheren** in het dialoogvenster een lijst met abonnementen die gekoppeld aan uw referenties zijn worden weergegeven. (Als er zijn meerdere abonnementen weergegeven en u wilt werken met alleen een specifieke subset van deze, u kunt desgewenst uitschakelen de abonnementen die u niet wilt gebruiken.) Wanneer u uw abonnementen hebt geselecteerd, klikt u op **sluiten**.
   
    ![Abonnementen beheren][08]
4. Wanneer de **implementeren in Azure Web App-Container** dialoogvenster wordt weergegeven, wordt deze in een Web-App-containers die u eerder hebt gemaakt weergegeven; als u geen containers niet gemaakt hebt, wordt de lijst leeg zijn.
   
    ![App-Containers][09]
5. Als u een Azure Web App-Container voordat niet hebt gemaakt, of als u uw toepassing naar een nieuwe container publiceren, gebruikt u de volgende stappen uit. Anders selecteert u een bestaande Web-App-Container en gaat u verder met stap 6 hieronder.
   
   1. Klik op**+**
      
       ![App-Container toevoegen][10]
   2. De **nieuwe Web-App-Container** in het dialoogvenster wordt weergegeven, die wordt gebruikt voor de volgende stappen.
      
       ![Nieuwe App-Container][11a]
   3. Voer een **DNS-Label** voor uw Web-App-Container; vormt dit het leaf DNS-label van de host-URL voor uw webtoepassing in Azure. Houd er rekening mee dat de naam moet beschikbaar zijn en voldoen aan de naamgeving van de vereisten voor Azure-webtoepassing.
   4. In de **webcontainer** vervolgkeuzelijst, selecteer de juiste software voor uw toepassing.
      
       U kunt op dit moment van Tomcat-8, 7 Tomcat of Jetty 9. Een recente distributie van de geselecteerde software door Azure worden verstrekt en het wordt uitgevoerd op een recente verdeling van JDK 8 gemaakt door Oracle en geleverd door Azure.
   5. In de **abonnement** vervolgkeuzelijst, selecteer het abonnement dat u wilt gebruiken voor deze implementatie.
   6. In de **resourcegroep** vervolgkeuzelijst, selecteer de resourcegroep die u wilt koppelen van uw Web-App. (Azure resourcegroepen kunt u voor het groeperen van gerelateerde resources samen zodat bijvoorbeeld ze samen kunnen worden verwijderd.)
      
       U kunt Selecteer een bestaande resourcegroep (als u een hebt) en overslaan naar stap g onderstaande of gebruik de volgende stappen om een nieuwe resourcegroep te maken:
      
      * Selecteer  **&lt; &lt; nieuwe resourcegroep maken &gt; &gt;**  in de **resourcegroep** vervolgkeuzelijst.
      * De **nieuwe resourcegroep** in het dialoogvenster wordt weergegeven:
        
          ![Nieuwe resourcegroep][12]
      * In de de **naam** textbox, Geef een naam voor uw nieuwe resourcegroep.
      * In de de **regio** vervolgkeuzelijst, selecteer de juiste Azure datacentrum locatie voor de resourcegroep.
      * Klik op **OK**.
   7. De **App Service-Plan** vervolgkeuzelijst geeft een lijst van de app service-abonnementen die zijn gekoppeld aan de resourcegroep die u hebt geselecteerd. (Een App Service-Plan bevat informatie zoals de locatie van uw Web-App, de prijscategorie en de grootte van de compute-exemplaar. Een enkele App Service-Plan kan worden gebruikt voor meerdere Web-Apps, dat is waarom deze afzonderlijk van een specifieke implementatie van Web-App onderhouden.)
      
       U kunt een bestaand App Service-abonnement (als u een hebt) en overslaan voor selecteren h onderstaande stap of gebruik de volgende stappen voor het maken van een nieuwe App Service-Plan:
      
      * Selecteer  **&lt; &lt; maken nieuwe App Service-Plan &gt; &gt;**  in de **App Service-Plan** vervolgkeuzelijst.
      * De **nieuwe App Service-Plan** in het dialoogvenster wordt weergegeven:
        
          ![Nieuwe App Service-abonnement][13]
      * In de de **naam** textbox, Geef een naam voor uw nieuwe App Service-Plan.
      * In de de **locatie** vervolgkeuzelijst, selecteer de juiste Azure datacentrum locatie voor het plan.
      * In de de **prijscategorie** vervolgkeuzelijst, selecteer de juiste prijs voor het plan. Voor testdoeleinden kunt u **vrije**.
      * In de de **Exemplaargrootte** vervolgkeuzelijst, selecteer het juiste exemplaar grootte voor het plan. Voor testdoeleinden kunt u **kleine**.
      * Klik op **OK**.
   8. (Optioneel) Standaard worden een recente verdeling van Java 8 automatisch geïmplementeerd als uw JVM door Azure voor uw web-app-container. U kunt echter een andere versie en de distributie van de JVM selecteren. Volg hiervoor de volgende stappen:
      
      * Klik op de **JDK** tabblad de **nieuwe Web-App-Container** in het dialoogvenster.
      * U kunt kiezen uit een van de volgende opties:
        
        * De standaardwaarde JDK die wordt aangeboden door Azure implementeren
        * Een 3e party JDK uit een vervolgkeuzelijst van aanvullende JDKs die beschikbaar op Azure zijn implementeren
        * Implementeren van een aangepaste JDK die moet worden opgenomen als een ZIP-bestand en een openbaar of in uw Azure storage-account
        
        ![Nieuw App-Container JDK tabblad][11b]
   9. Nadat u alle bovenstaande stappen hebt voltooid, moet het dialoogvenster Nieuwe Web-App-Container zijn vergelijkbaar met de volgende afbeelding:
      
       ![Nieuwe App-Container][14]
   10. Klik op **OK** voor het maken van uw nieuwe Web-App-container niet voltooien.
       
        Wacht een paar seconden voor een overzicht van de Web-App-containers worden vernieuwd en de zojuist gemaakte web-app-container moet nu worden geselecteerd in de lijst.
6. U bent nu klaar voor het uitvoeren van de eerste implementatie van uw Web-App in Azure; Klik op **OK** voor het implementeren van uw Java-toepassing aan de geselecteerde container van Web-App. Standaard wordt uw toepassing wordt geïmplementeerd als een submap van de toepassingsserver. Als u wilt dat deze worden geïmplementeerd als de hoofdtoepassing, controleert u de **implementeren in de hoofdmap** selectievakje voordat u op **OK**.
   
    ![Implementeren in Azure][15]
7. Vervolgens ziet u de **Azure Activity Log** weergave, die de status van de implementatie van uw Web-App wordt aangegeven.
   
    ![Voortgangsindicator][16]
   
    Het proces voor het implementeren van uw Web-App naar Azure duren slechts een paar seconden. Wanneer uw toepassing ready, ziet u een koppeling met de naam **gepubliceerde** in de **Status** kolom. Wanneer u de koppeling klikt, wordt deze gaat u naar de startpagina van de geïmplementeerde Web-App of kunt u de stappen in de volgende sectie om te bladeren naar uw web-app.

## <a name="browsing-to-your-web-app-on-azure"></a>Bladeren naar uw Web-App in Azure
Om te bladeren naar uw Web-App in Azure, kunt u de **Azure Explorer** weergeven.

Als de **Azure Explorer** weergave nog niet is geopend, kunt u deze openen door te klikken op vervolgens **weergave** menu in IntelliJ, klikt u vervolgens op **hulpprogramma Windows**, en klik vervolgens op  **Service-Explorer**. Als u eerder niet hebt aangemeld, wordt u gevraagd.

Wanneer de **Azure Explorer** weergave wordt weergegeven, gebruik als volgt te werk om te bladeren naar uw Web-App: 

1. Vouw de **Azure** knooppunt.
2. Vouw de **Web-Apps** knooppunt. 
3. Met de rechtermuisknop op de gewenste Web-App.
4. Wanneer het contextmenu wordt weergegeven, klikt u op **openen in Browser**.
   
    ![Web-App bladeren][17]

## <a name="updating-your-web-app"></a>De web-app beveiligen
Bijwerken van een bestaande Azure-Web-App uitgevoerd is een snelle en eenvoudige proces en hebt u twee opties voor het bijwerken van:

* U kunt de implementatie van een bestaande Java-Web-App kunt bijwerken.
* U kunt een extra Java-toepassing tot dezelfde Container voor de Web-App publiceren.

In beide gevallen is het proces identieke en duurt slechts enkele seconden:

1. In de Projectverkenner IntelliJ met de rechtermuisknop op de Java-toepassing die u wilt bijwerken of toevoegen aan een bestaande Web-App-Container.
2. Wanneer het contextmenu wordt weergegeven, selecteert u **Azure** en vervolgens **publiceren als Azure-Web-App...**
3. Nadat u hebt al aangemeld eerder, ziet u een lijst met uw bestaande Web-App-containers. Selecteer de gewenste publiceren of uw Java-toepassing opnieuw te publiceren en klik op **OK**.

Een paar seconden later, de **Azure Activity Log** weer uw bijgewerkte implementatie als **gepubliceerde** en u kunt controleren of uw bijgewerkte toepassing in een webbrowser.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Starten, stoppen of opnieuw starten van een bestaande web-app
Om te starten of stoppen van een bestaande Azure-Web-App-container (en alle geïmplementeerde Java-toepassingen erin), kunt u de **Azure Explorer** weergeven.

Als de **Azure Explorer** weergave nog niet is geopend, kunt u deze openen door te klikken op vervolgens **weergave** menu in IntelliJ, klikt u vervolgens op **hulpprogramma Windows**, en klik vervolgens op  **Service-Explorer**. Als u eerder niet hebt aangemeld, wordt u gevraagd.

Wanneer de **Azure Explorer** weergave wordt weergegeven, gebruik als volgt te werk om te starten of stoppen van uw Web-App: 

1. Vouw de **Azure** knooppunt.
2. Vouw de **Web-Apps** knooppunt. 
3. Met de rechtermuisknop op de gewenste Web-App.
4. Wanneer het contextmenu wordt weergegeven, klikt u op **Start**, **stoppen**, of **opnieuw**. Houd er rekening mee dat de menu-Opties contextbewuste, zijn zodat u kunt alleen een actieve WebApp stoppen of starten van een web-app die niet wordt uitgevoerd.
   
    ![Web-App stoppen][18]

## <a name="next-steps"></a>Volgende stappen
Voor meer informatie over de Azure Toolkits voor Java-IDE's klikt u op de volgende koppelingen:

* [Azure Toolkit voor Eclipse]
  * [Installing the Azure Toolkit for Eclipse] (De Azure Toolkit voor Eclipse installeren)
  * [Een Hallo wereld Web-App maken voor Azure in Eclipse]
  * [What's New in the Azure Toolkit for Eclipse] (Nieuw in de Azure Toolkit voor Eclipse)
* [Azure Toolkit voor IntelliJ] (Azure Toolkit voor IntelliJ)
  * [Toolkit Azure installeren voor IntelliJ] (De Azure Toolkit voor IntelliJ installeren)
  * *Een Hallo wereld Web-App maken voor Azure in IntelliJ (in dit artikel)*
  * [What's New in the Azure Toolkit for IntelliJ] (Nieuw in de Azure Toolkit voor IntelliJ)

<a name="see-also"></a>

## <a name="see-also"></a>Zie ook
In het [Azure Java Developer Center] vindt u meer informatie over het gebruik van Azure met Java.

Zie voor meer informatie over het maken van Azure Web Apps, de [overzicht van Web Apps].

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Azure Toolkit voor Eclipse]: ../azure-toolkit-for-eclipse.md
[Azure Toolkit voor IntelliJ]: ../azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)
[Een Hallo wereld Web-App maken voor Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Installing the Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-installation.md (De Azure Toolkit voor Eclipse installeren)
[Toolkit Azure installeren voor IntelliJ]: ../azure-toolkit-for-intellij-installation.md (De Azure Toolkit voor IntelliJ installeren)
[What's New in the Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md (Nieuw in de Azure Toolkit voor Eclipse)
[What's New in the Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md (Nieuw in de Azure Toolkit voor IntelliJ)

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
