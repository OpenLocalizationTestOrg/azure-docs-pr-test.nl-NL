---
title: een Hello World Cloud Service voor Azure in Eclipse aaaCreate
description: Meer informatie over hoe een eenvoudig Hello World toepassing met toocreate hello Azure Toolkit voor Eclipse.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 7262e705-59d6-43ce-b888-29a21c8e0cb7
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: dfb81374aaf78e933c0bf83a1dbd98023801491a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-hello-world-cloud-service-for-azure-in-eclipse"></a>Maken van een Cloudservice van Hallo wereld voor Azure in Eclipse
Hallo volgende stappen ziet u hoe toocreate en implementeren van een eenvoudige JSP-toepassing tooAzure met hello Azure Toolkit voor Eclipse. Een voorbeeld van een JSP voor eenvoud wordt weergegeven, maar maximaal gelijksoortige stappen zou zijn geschikt voor een servlet Java wat betreft Azure-implementatie is.

Hallo-toepassing ziet vergelijkbare toohello volgende uit:

![][ic600360]

## <a name="prerequisites"></a>Vereisten
* Een Java Developer Kit (JDK), v 1.7 of hoger.
* Eclipse IDE voor Java EE-ontwikkelaars Indigo of hoger. Dit kan worden gedownload vanaf <http://www.eclipse.org/downloads/>.
* Een distributiepunt van een Java gebaseerde webserver of toepassingsserver, zoals Apache Tomcat, GlassFish, JBoss-toepassingsserver, Jetty of IBM® WebSphere® Application Server Liberty Core.
* Een Azure-abonnement, die kan worden opgehaald uit <http://azure.microsoft.com/pricing/purchase-options/>.
* Hello Azure Toolkit voor Eclipse. Zie voor meer informatie [installeren hello Azure Toolkit voor Eclipse][Installing hello Azure Toolkit for Eclipse].

## <a name="toocreate-a-hello-world-application"></a>een toepassing Hello World toocreate
Eerst beginnen we uitschakelen met een Java-project maken.

1. Start Eclipse en op Hallo-menu op **bestand**, klikt u op **nieuw**, en klik vervolgens op **dynamisch webproject**. (Als er geen **dynamisch webproject** vermeld als een project beschikbaar wanneer u op **bestand**, **nieuw**, vervolgens Hallo te volgen: klik op **bestand**, klikt u op **nieuw**, klikt u op **Project...** , vouw **Web**, klikt u op **dynamisch webproject**, en klik op **volgende**.)

1. Naam voor deze zelfstudie Hallo project **MyHelloWorld**. (Zorg ervoor dat u gebruikt deze naam, de volgende stappen in deze zelfstudie verwacht dat het WAR-bestand toobe MyHelloWorld met de naam). Het scherm wordt vergelijkbaar toohello volgende weergegeven:

   ![][ic589576]

1. Klik op **Voltooien**.

1. Vouw in de weergave Project Explorer van Eclipse **MyHelloWorld**. Klik met de rechtermuisknop op **WebContent**(Webinhoud) en klik vervolgens op **New** (Nieuw) en **JSP File** (JSP-bestand).

1. In Hallo **nieuw JSP-bestand** dialoogvenster, Hallo bestandsnaam **index.jsp**. Hallo bovenliggende map als houden **MyHelloWorld/WebContent**, zoals wordt weergegeven in de volgende Hallo:

   ![][ic659262]

1. In Hallo **JSP-sjabloon selecteren** dialoogvenster ten behoeve van deze zelfstudie selecteert **nieuw JSP-bestand (html)** en klik op **voltooien**.

1. Wanneer de bestand index.jsp hello wordt geopend in Eclipse, toevoegen in toodynamically tekstweergave **Hello World!** binnen de bestaande Hallo `<body>` element. Uw bijgewerkte `<body>` inhoud moet worden weergegeven als Hallo volgende:
   ```
   <body>
   <b><% out.println("Hello World!"); %></b>
   </body>
   ```
1. Index.jsp opslaan.

## <a name="toodeploy-your-application-tooazure-hello-quick-and-simple-way"></a>toodeploy van uw toepassing tooAzure, Hallo snelle en eenvoudige manier
Als u een Java web application gereed tootest hebt, kunt u Hallo snelkoppeling tootry het afmelden rechtstreeks op Hallo Azure cloud te volgen.

1. Klik in Projectverkenner van Eclipse **MyHelloWorld**.

2. Klik op Hallo Hallo Eclipse werkbalk **publiceren** vervolgkeuzepijl en klik vervolgens op **publiceren als Azure Cloud Service**

   ![][publishDropdownButton]

3. Als u nog geen gemaakt met een Azure-implementatie-project voor deze toepassing voordat u deze toepassing tooAzure voor Hallo publiceert eerst worden een webproject Azure-implementatie automatisch voor u gemaakt. U ziet toorun uw toepassing hello volgen vragen, waarin ook Hallo JDK pakket- en server die automatisch worden geïmplementeerd.

   ![][ic789598]
   
   Deze aanpak snelkoppeling kan een snelle en gemakkelijke manier tootest uw toepassing in Azure zonder tooconfigure een bepaalde server of de JDK die verschilt van Hallo standaardwaarden. Als u tevreden met Hallo standaardwaarden bent, klikt u op **OK** toocontinue Hello stappen te volgen.
   Echter, als u wilt dat toochange hello JDK of application server toouse voor uw toepassing, kunt u dat doen later door te bewerken hello Azure implementatieproject die automatisch voor u is gemaakt, of u kunt op **annuleren** nu weergeven en lezen Hallo **over Azure-implementatie projecten sectie** van deze zelfstudie.

4. In Hallo **tooAzure publiceren** dialoogvenster:

   1. Als er geen abonnementen tooselect in Hallo **abonnement** lijst nog Volg deze stappen tooimport uw abonnementsgegevens:
      1. Klik op **importeren uit bestand publiceren instellingen**.
      2. In Hallo **importeren abonnementsgegevens** dialoogvenster, klikt u op **publiceren-SETTINGS-bestand downloaden**. Als u nog niet aangemeld bij uw Azure-account, kunt u zich na vragen aan gebruiker toolog in. Vervolgens wordt u gevraagd een Azure toosave bestand publicatie-instellingen. Sla het op de lokale computer tooyour.
      3. Nog steeds in Hallo **importeren abonnementsgegevens** dialoogvenster, klikt u op Hallo **Bladeren** knop, selecteer Hallo bestand publicatie-instellingen die u lokaal in de vorige stap Hallo opgeslagen en klik vervolgens op  **Open**. Uw scherm ziet er vergelijkbare toohello volgende:![][ic644267]
      4. Klik op **OK**.
   2. Voor **abonnement**, selecteer Hallo abonnement die u gebruiken voor uw implementatie wilt.
   3. Voor **opslagaccount**, selecteer Hallo opslagaccount dat u wilt dat toouse of op **nieuw** toocreate een nieuw opslagaccount.
   4. Voor **servicenaam**, Hallo cloudservice wilt toouse of klik op selecteren **nieuw** toocreate een nieuwe cloudservice.
   5. Voor **doel OS**, selecteer Hallo-versie van besturingssysteem hello wilt u toouse voor uw implementatie.
   6. Voor **doelomgeving**, voor deze zelfstudie selecteert **fasering**. (Als u klaar toodeploy tooyour productiesite bent, wijzigt u dit te**productie**.)
   7. Optioneel: Zorg ervoor dat **overschrijven van de vorige implementatie** als u wilt dat uw nieuwe implementatie tooautomatically overschrijven Hallo vorige implementatie is ingeschakeld. Wanneer u deze optie inschakelt, wordt geen ervaring '409 conflict' problemen bij het publiceren van toohello dezelfde locatie.
      Houd er rekening mee dat Hallo **publiceren tooAzure** dialoogvenster bevat een sectie voor **RAS**. Standaard externe toegang niet is ingeschakeld en er wordt het niet inschakelen voor dit voorbeeld. tooenable externe toegang, voert u een gebruiker en het wachtwoord toouse bij het aanmelden op afstand. Zie voor meer informatie over externe toegang [externe toegang inschakelen voor Azure-implementaties in Eclipse][Enabling Remote Access for Azure Deployments in Eclipse].
      Uw **tooAzure publiceren** dialoogvenster vergelijkbare toohello volgende weergegeven:![][ic719488]

5. Klik op **publiceren** toopublish toohello faseringsomgeving.

   Wanneer na vragen aan gebruiker tooperform een volledige build, klikt u op **Ja**. Dit kan enkele minuten voor de eerste build Hallo duren.
   Een **Azure Activity Log** wordt weergegeven in de sectie met tabs Eclipse weergaven.
   ![][ic719489]U kunt dit logboek gebruiken, evenals Hallo **Console** toosee Hallo voortgang van uw implementatie weergeven. Een alternatief is toolog in toohello [Azure Management Portal][Azure Management Portal], en gebruik Hallo **Cloudservices** sectie toomonitor Hallo status.

6. Wanneer uw implementatie succes is geïmplementeerd, Hallo **Azure Activity Log** ziet de status van **gepubliceerde**. Klik op **gepubliceerde**, zoals wordt weergegeven in de volgende Hallo installatiekopie en de browser wordt geopend een exemplaar van uw implementatie.

   ![][ic719490]

Omdat dit een implementatie tooa staging-omgeving, Hallo DNS-naam is van Hallo formulier http://&lt;*guid*&gt;. cloudapp.net en Hallo-URL bevat Hallo DNS-naam, plus een achtervoegsel voor uw toepassing. Bijvoorbeeld: http://447564652c20426f6220526f636b7321.cloudapp.net/MyHelloWorld. (Hallo **MyHelloWorld** gedeelte hoofdlettergevoelig is.) U ziet ook Hallo DNS als u de implementatienaam Hallo in Hallo beheerportal van Azure-Platform (binnen Hallo Cloud Services-gedeelte van de beheerportal Hallo) op naam.

Hoewel deze procedure voor een implementatie toohello staging-omgeving is, een implementatie tooproduction volgt dezelfde stappen behalve binnen Hallo Hallo **publiceren tooAzure** dialoogvenster Selecteer **productie** in plaats van **fasering** voor Hallo **doelomgeving**. Een implementatie tooproduction resulteert in een URL die is gebaseerd op Hallo DNS-naam van uw keuze, in plaats van een GUID als gebruikt voor fasering.

> [!WARNING]
> Nu hebt u uw Azure-toepassing toohello cloud geïmplementeerd. Echter, voordat u doorgaat, houd er rekening mee dat een geïmplementeerde toepassing, zelfs als deze niet wordt uitgevoerd, de factureerbare tijd tooaccrue voor uw abonnement blijft. Het is daarom zeer belangrijk dat u ongewenste implementaties van uw Azure-abonnement verwijdert.
> 
> 

## <a name="about-azure-deployment-projects"></a>Over Azure-implementatie-projecten
In volgorde toodeploy een of meer Java-toepassingen tooAzure, een Azure-implementatieproject nodig is. Het speelt Hallo rol Hallo 'pakket' dat uw toepassingen toobe samengevoegd moeten in in de volgorde toobe gepubliceerd in Azure.

Naast het Hallo-informatie over uw toepassingen, een Azure-implementatie-project bevat ook informatie over andere belangrijke onderdelen van uw implementatie belangrijker: Hallo application server container toorun in uw web-app en Java runtime toorun Hallo deze op. Azure biedt ondersteuning voor een groot aantal Java runtimes en Java-toepassingsservers die u kunt kiezen uit.

Hoewel het Hallo-voorbeeld hier gebruikt sterk vereenvoudigd voor educatieve doeleinden, kan een Azure-implementatie-project ook andere belangrijke configuratie-informatie waarmee u toocreate bijna willekeurig complexe, schaalbare en maximaal beschikbaar, bevatten meerdere lagen cloudservices met uw toepassingen. U kunt inschakelen **affiniteit sessie ("een tijdelijke sessies')**, **Snelle caching**, **SSL-offloading**, **firewallpoort routering**, **RAS**, en een aantal andere krachtige mogelijkheden.

Als u de vorige sectie Hallo van deze zelfstudie hebt voltooid ("toodeploy van uw toepassing tooAzure, Hallo snelle en eenvoudige manier '), ziet u nu een nieuw project in de Azure-implementatie in Hallo Projectverkenner automatisch voor u gegenereerd en de naam ' **MyHelloWorld_onAzure**'.

U kan hebben ook gestart in deze zelfstudie een Azure-implementatie leeg project eerst maken zelf en vervolgens toe te voegen uw tooit toepassing(en). Er is een langer proces, maar geeft u meer controle over de eerste configuratie van de Hallo Hallo vanaf.

toocreate een nieuw Azure-implementatie-project maken, klikt u op Hallo **nieuwe Azure-implementatieproject** knop ![][ic710876].

Ongeacht of u werken met een bestaand Azure-implementatie-project, of maken van een geheel nieuw, u kunt toochange de configuratie-instellingen en -onderdelen, zoals Hallo JDK of toepassingsserver, net zo eenvoudig hello op elk gewenst moment.

toochange hello JDK, of toepassingsserver Hallo of lijst met toepassingen in een bestaand Azure-implementatieproject Hallo:

1. Vouw Hallo projectknooppunt (bijvoorbeeld **MyHelloWorld_onAzure**) in Hallo Projectverkenner

2. Met de rechtermuisknop op **WorkerRole1**

3. Vouw Hallo **Azure** submenu in het contextmenu Hallo

4. Klik op **serverconfiguratie**

Ongeacht of u deze serverconfiguratiestappen gestart door een bestaand project in de Azure-implementatie te bewerken, zoals hierboven of maakt een nieuwe maken, u Hallo ziet dezelfde soort dialoogvensters zodat u tooconfigure uw JDK servers en toepassingen onderdelen. toolearn meer hoe toochange Hallo instellingen in de dialoogvensters, bijvoorbeeld toochange hello JDK, Hallo toepassingsserver en toepassingen toevoegen of verwijderen in een implementatie, Zie Hallo [configuratie-eigenschappen Server] [ Server configuration properties] artikel.

## <a name="windows-only-toodeploy-your-application-toohello-compute-emulator"></a>Alleen Windows: toodeploy rekenemulator voor uw toepassing toohello

> [!NOTE]
> Hello Azure-emulator is alleen beschikbaar in Windows. Deze sectie overslaan als u een besturingssysteem dan Windows.
> 
> 

Als u een nieuw Azure-implementatieproject Hallo stappen eerder, dat wil zeggen impliciet door het publiceren van uw tooAzure toepassing hebt gemaakt Hallo JDK en toepassingsservers zijn geconfigureerd voor Hallo cloud, maar niet voor lokale geëmuleerd. tooprepare uw project voor het testen in lokale Hallo-emulator, als volgt te werk:

1. Klik in Projectverkenner van Eclipse **MyHelloWorld_onAzure**.

2. Met de rechtermuisknop op **WorkerRole1**.

3. Vouw Hallo **Azure** submenu in het contextmenu Hallo.

4. Klik op **serverconfiguratie**.

5. Op Hallo **JDK** tabblad, moet u controleren als Hallo toolkit is een standaard vooraf geconfigureerde lokale JDK voor u. Als dat niet, of als u wilt toochange Hallo aangenomen dat de standaardinstellingen, zorg ervoor dat Hallo **gebruik Hallo JDK van dit bestandspad om lokaal te testen** selectievakje is ingeschakeld en Hallo installatielocatie JDK die u wilt dat toouse is opgegeven. Als u wilt dat toochange, klikt u op Hallo **Bladeren** en Hallo bladeren besturingselement gebruikt, selecteer de maplocatie Hallo van Hallo JDK toouse.

6. Klik op Hallo **Server** tabblad.

7. In Hallo **pad naar de lokale server** in het tekstvak onder Hallo van dialoogvenster Hallo Hallo pad opgeven van een server met lokaal zijn geïnstalleerd die overeenkomt met Hallo type en het primaire versienummer van Hallo server geselecteerd Hallo boven aan het Hallo-dialoogvenster, klikt u onder Hallo **implementeren van een server van dit type** selectievakje. Als u toouse een ander type of de primaire versie van de toepassingsserver hello wilt, eerst de selectie Hallo onder dit selectievakje wijzigen.

8. Klik op **OK**.

9. Klik op Hallo Hallo Eclipse werkbalk **uitvoeren in Azure-Emulator** knop ![][ic710879]. Als hello **uitvoeren in Azure-Emulator** knop is niet ingeschakeld, zorg ervoor dat **MyHelloWorld_onAzure** is geselecteerd in de Projectverkenner van Eclipse en zorg ervoor dat de Eclipse-Project Explorer focus als Hallo huidige venster. Hiermee wordt een volledige versie van uw project voor de eerste keer en start vervolgens uw Java-webtoepassing in Hallo rekenemulator. (Afhankelijk van de prestatiekenmerken van de computer, Hallo eerste build tussen een paar seconden tooa enkele minuten kan duren, maar volgende builds krijgen sneller.) Nadat de eerste build stap Hallo is voltooid, wordt u gevraagd deze opdracht toomake wijzigt Windows Gebruikersaccountbeheer (UAC) tooallow tooyour computer. Klik op **Ja**.

> [!IMPORTANT]
> Als er geen Hallo UAC-prompt, selectievakje Hallo van Windows-taakbalk voor Hallo UAC-pictogram en klik op de eerste. Soms Hallo UAC-prompt niet wordt weergegeven als een bovenste venster, maar alleen als een pictogram op de taakbalk zichtbaar is.
> 
> 

1. Bekijk de uitvoer op Hallo van Hallo compute-emulator UI toodetermine als er problemen met uw project zijn. Afhankelijk van de inhoud van de Hallo van uw implementatie duurt een paar minuten voor uw toepassing toobe volledig binnen het Hallo-rekenemulator is gestart.

2. Start uw browser en gebruik Hallo URL `http://localhost:8080/MyHelloWorld` als Hallo-adres (Hallo `MyHelloWorld` gedeelte van het Hallo-URL is hoofdlettergevoelig). U ziet uw MyHelloWorld toepassing (Hallo uitvoer van index.jsp), vergelijkbaar toohello installatiekopie te volgen:

   ![][ic589579]

Wanneer u bent klaar toostop uw toepassing wordt uitgevoerd in de rekenemulator Hallo Hallo Eclipse werkbalk klikt u op Hallo **opnieuw instellen van de Azure-Emulator** knop ![][ic710880].

## <a name="toodelete-your-deployment"></a>toodelete uw implementatie
toodelete uw implementatie binnen hello Azure Toolkit voor Eclipse ervoor te zorgen dat **MyHelloWorld_onAzure** is geselecteerd in de Eclipse-Project Explorer, Controleer Hallo Eclipse Projectverkenner heeft Hallo huidige venster richten en klik vervolgens op Hallo **publicatie ongedaan maken** knop ![][ic710883], op Hallo Eclipse werkbalk. (U kan doen dezelfde bewerking met de rechtermuisknop op Hallo **MyHelloWorld_onAzure** in Eclipse van Projectverkenner te klikken op **Azure** en vervolgens te klikken op **Undeploy vanuit Azure Cloud**.) Hiermee wordt weergegeven Hallo **ongedaan maken van de Azure-Project** dialoogvenster.

![][ic719491]

Selecteer Hallo abonnement en cloud service met uw implementatie, selecteer Hallo-implementatie wilt toodelete en klik vervolgens op **publicatie ongedaan maken**.

(Een alternatieve toousing Hallo toolkit toodelete Hallo-implementatie is toouse hello **Cloudservices** sectie Hallo Azure Management Portal: navigeer tooyour implementatie, selecteert u deze en klik op Hallo **verwijderen** knop. Hiermee stoppen en vervolgens verwijdert, Hallo-implementatie. Als u wilt dat alleen toostop Hallo implementatie en niet wordt verwijderd, klikt u op Hallo **stoppen** knop in plaats van Hallo **verwijderen** knop, maar zoals hierboven vermeld als Hallo-implementatie, factureerbare kosten wordt niet verwijderd blijven tooaccrue voor uw implementatie zelfs als deze is gestopt).

## <a name="see-also"></a>Zie ook
[Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]

[Hello Azure Toolkit voor Eclipse installeren][Installing hello Azure Toolkit for Eclipse] 

[Wat is er nieuw in hello Azure Toolkit voor Eclipse][What's New in hello Azure Toolkit for Eclipse]

Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Role Properties]: http://go.microsoft.com/fwlink/?LinkID=699525
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Enabling Remote Access for Azure Deployments in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699538
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Server configuration properties]: http://go.microsoft.com/fwlink/?LinkID=699525#server_configuration_properties
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic589576]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic589576.png
[ic589579]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic589579.png
[ic600360]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic600360.png
[ic644267]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic644267.png
[ic659262]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic659262.png
[ic710876]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710876.png
[ic710879]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710879.png
[ic710880]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710880.png
[ic710882]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710882.png
[ic710883]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710883.png
[ic719488]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719488.png
[ic719489]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719489.png
[ic719490]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719490.png
[ic719491]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719491.png
[ic789598]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic789598.png
[publishDropdownButton]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/publishDropdownButton.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690944.aspx -->
