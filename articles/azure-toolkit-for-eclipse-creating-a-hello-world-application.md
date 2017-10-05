---
title: Maken van een Cloudservice van Hallo wereld voor Azure in Eclipse
description: Informatie over het maken van een eenvoudige Hallo wereld-toepassing met de Azure-Toolkit voor Eclipse.
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
ms.openlocfilehash: 9b31f0faeb6ee7b5e7b8fe3a1f2827133d6188e6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-hello-world-cloud-service-for-azure-in-eclipse"></a>Maken van een Cloudservice van Hallo wereld voor Azure in Eclipse
De volgende stappen ziet u het maken en implementeren van een eenvoudige JSP-toepassing naar Azure met de Azure-Toolkit voor Eclipse. Een voorbeeld van een JSP voor eenvoud wordt weergegeven, maar maximaal gelijksoortige stappen zou zijn geschikt voor een servlet Java wat betreft Azure-implementatie is.

De toepassing ziet er ongeveer als volgt:

![][ic600360]

## <a name="prerequisites"></a>Vereisten
* Een Java Developer Kit (JDK), v 1.7 of hoger.
* Eclipse IDE voor Java EE-ontwikkelaars Indigo of hoger. Dit kan worden gedownload vanaf <http://www.eclipse.org/downloads/>.
* Een distributiepunt van een Java gebaseerde webserver of toepassingsserver, zoals Apache Tomcat, GlassFish, JBoss-toepassingsserver, Jetty of IBM® WebSphere® Application Server Liberty Core.
* Een Azure-abonnement, die kan worden opgehaald uit <http://azure.microsoft.com/pricing/purchase-options/>.
* De Azure-werkset voor Eclipse. Zie voor meer informatie [installeren van de Azure-werkset voor Eclipse][Installing the Azure Toolkit for Eclipse].

## <a name="to-create-a-hello-world-application"></a>Een toepassing Hello World maken
Eerst beginnen we uitschakelen met een Java-project maken.

1. Start Eclipse en klik op het menu **bestand**, klikt u op **nieuw**, en klik vervolgens op **dynamisch webproject**. (Als er geen **dynamisch webproject** vermeld als een project beschikbaar wanneer u op **bestand**, **nieuw**, doet u het volgende: klik op **bestand**, klikt u op **nieuw**, klikt u op **Project...** , vouw **Web**, klikt u op **dynamisch webproject**, en klik op **volgende**.)

1. Noem het project voor deze zelfstudie **MyHelloWorld**. (Zorg ervoor dat u gebruikt deze naam, volgende stappen in deze zelfstudie verwacht dat uw naam MyHelloWorld WAR-bestand). Uw scherm ziet er ongeveer als volgt:

   ![][ic589576]

1. Klik op **Voltooien**.

1. Vouw in de weergave Project Explorer van Eclipse **MyHelloWorld**. Klik met de rechtermuisknop op **WebContent**(Webinhoud) en klik vervolgens op **New** (Nieuw) en **JSP File** (JSP-bestand).

1. In de **nieuw JSP-bestand** dialoogvenster, de naam van het bestand **index.jsp**. Bewaar de bovenliggende map als **MyHelloWorld/WebContent**, zoals wordt weergegeven in het volgende:

   ![][ic659262]

1. In de **JSP-sjabloon selecteren** dialoogvenster ten behoeve van deze zelfstudie selecteert **nieuw JSP-bestand (html)** en klik op **voltooien**.

1. Wanneer het bestand index.jsp wordt geopend in Eclipse, toevoegen in de tekst die moet dynamisch weergeven **Hello World!** in het bestaande `<body>`-element. Uw bijgewerkte `<body>` inhoud moet worden weergegeven als het volgende:
   ```
   <body>
   <b><% out.println("Hello World!"); %></b>
   </body>
   ```
1. Index.jsp opslaan.

## <a name="to-deploy-your-application-to-azure-the-quick-and-simple-way"></a>Voor het implementeren van uw toepassing in Azure, hoe snel en eenvoudig
Zodra u een Java-webtoepassing gereed om te testen hebt, kunt u de volgende snelkoppeling uitproberen rechtstreeks op de Azure-cloud.

1. Klik in Projectverkenner van Eclipse **MyHelloWorld**.

2. Klik in de werkbalk van Eclipse op de **publiceren** vervolgkeuzepijl en klik vervolgens op **publiceren als Azure Cloud Service**

   ![][publishDropdownButton]

3. Als u deze toepassing in Azure voor het eerst publiceert en u niet voor deze toepassing voordat u een Azure-implementatie-project hebt gemaakt, worden een project Azure-implementatie automatisch voor u gemaakt. U ziet de volgende prompt, die ook een lijst met het pakket JDK en de toepassingsserver die automatisch worden geïmplementeerd als uw toepassing wilt uitvoeren.

   ![][ic789598]
   
   Deze aanpak snelkoppeling kunt een snelle en gemakkelijke manier om te testen van uw toepassing in Azure zonder een bepaalde server of de JDK die verschilt van de standaardinstellingen configureren. Als u tevreden met de standaardinstellingen bent, klikt u op **OK** om door te gaan met de volgende stappen.
   Echter, als u wilt wijzigen van de JDK of toepassingsserver te gebruiken voor uw toepassing kunt u dat later doen door het bewerken van het project Azure-implementatie die automatisch voor u is gemaakt, of u kunt op **annuleren** nu uit en lees de  **Over Azure-implementatie projecten sectie** van deze zelfstudie.

4. In de **publiceren naar Azure** dialoogvenster:

   1. Als er geen abonnementen om te selecteren zijn de **abonnement** lijst nog als volgt te werk als u wilt uw abonnementsgegevens importeren:
      1. Klik op **importeren uit bestand publiceren instellingen**.
      2. In de **importeren abonnementsgegevens** dialoogvenster, klikt u op **publiceren-SETTINGS-bestand downloaden**. Als u nog niet aangemeld bij uw Azure-account, wordt u gevraagd om aan te melden. U wordt vervolgens gevraagd te Sla een Azure bestand publicatie-instellingen. Sla deze op uw lokale computer.
      3. Nog steeds in de **importeren abonnementsgegevens** dialoogvenster, klikt u op de **Bladeren** knop, selecteer het publish settings-bestand dat u lokaal in de vorige stap opgeslagen en klik vervolgens op **openen**. Uw scherm ziet er ongeveer als volgt:![][ic644267]
      4. Klik op **OK**.
   2. Voor **abonnement**, selecteer het abonnement die u gebruiken voor uw implementatie wilt.
   3. Voor **opslagaccount**, selecteert u het opslagaccount dat u wilt gebruiken, of klik op **nieuw** een nieuw opslagaccount maken.
   4. Voor **servicenaam**, selecteer de cloudservice die u wilt gebruiken, of klik op **nieuw** voor het maken van een nieuwe cloudservice.
   5. Voor **doel OS**, selecteer de versie van het besturingssysteem dat u wilt gebruiken voor uw implementatie.
   6. Voor **doelomgeving**, voor deze zelfstudie selecteert **fasering**. (Wanneer u klaar bent om te implementeren voor uw productiesite, past u deze optie om te **productie**.)
   7. Optioneel: Zorg ervoor dat **overschrijven van de vorige implementatie** als u wilt dat uw nieuwe implementatie moeten worden overschreven de vorige implementatie is ingeschakeld. Wanneer u deze optie inschakelt, wordt geen ervaring '409 conflict' problemen bij het publiceren naar dezelfde locatie.
      Houd er rekening mee dat de **publiceren naar Azure** dialoogvenster bevat een sectie voor **RAS**. Standaard externe toegang niet is ingeschakeld en er wordt het niet inschakelen voor dit voorbeeld. Voor externe toegang, voert u een gebruikersnaam en wachtwoord voor gebruik bij het aanmelden op afstand. Zie voor meer informatie over externe toegang [externe toegang inschakelen voor Azure-implementaties in Eclipse][Enabling Remote Access for Azure Deployments in Eclipse].
      Uw **publiceren naar Azure** dialoogvenster ziet er ongeveer als volgt:![][ic719488]

5. Klik op **publiceren** publiceren naar de Staging-omgeving.

   Wanneer u wordt gevraagd om uit te voeren van een volledige build, klikt u op **Ja**. Dit kan enkele minuten voor de eerste build duren.
   Een **Azure Activity Log** wordt weergegeven in de sectie met tabs Eclipse weergaven.
   ![][ic719489]U kunt dit logboek, evenals de **Console** weergeven om te zien van de voortgang van uw implementatie. Een alternatief is aan te melden bij de [Azure Management Portal][Azure Management Portal], en gebruik de **Cloudservices** sectie om de status te controleren.

6. Wanneer uw implementatie succes is geïmplementeerd, de **Azure Activity Log** ziet de status van **gepubliceerde**. Klik op **gepubliceerde**, zoals wordt weergegeven in de volgende afbeelding en de browser een exemplaar van uw implementatie wordt geopend.

   ![][ic719490]

Omdat dit een implementatie met een testomgeving, worden de DNS-naam van het formulier http://&lt;*guid*&gt;. cloudapp.net en de URL wordt de DNS-naam, plus een achtervoegsel voor de toepassing bevatten. Bijvoorbeeld: http://447564652c20426f6220526f636b7321.cloudapp.net/MyHelloWorld. (De **MyHelloWorld** gedeelte hoofdlettergevoelig is.) U ziet ook de DNS-naam als u de implementatienaam van de in het beheerportal van Azure-Platform (in de Cloud Services-gedeelte van de beheerportal) op.

Hoewel deze procedure voor een implementatie van de testomgeving is, een productie-implementatie dezelfde stappen volgt, behalve binnen de **publiceren naar Azure** dialoogvenster Selecteer **productie** in plaats van **Fasering** voor de **doelomgeving**. Een implementatie naar productie resulteert in een URL op basis van de DNS-naam van uw keuze, in plaats van een GUID als gebruikt voor fasering.

> [!WARNING]
> U hebt op dit moment uw Azure-toepassing naar de cloud geïmplementeerd. Echter, voordat u doorgaat, houd er rekening mee dat een geïmplementeerde toepassing, zelfs als deze niet wordt uitgevoerd, blijft toenemen factureerbare tijd voor uw abonnement. Het is daarom zeer belangrijk dat u ongewenste implementaties van uw Azure-abonnement verwijdert.
> 
> 

## <a name="about-azure-deployment-projects"></a>Over Azure-implementatie-projecten
Als een of meer Java-toepassingen in Azure implementeert, is een Azure-implementatieproject vereist. Het speelt de rol van het 'pakket' dat uw toepassingen worden verpakt moeten in om te kunnen worden gepubliceerd in Azure.

Naast de informatie over uw toepassingen een Azure-implementatie-project bevat ook informatie over andere belangrijke onderdelen van uw implementatie belangrijker: de container van de toepassing om uit te voeren van uw web-app in en uit te voeren op de Java-runtime. Azure biedt ondersteuning voor een groot aantal Java runtimes en Java-toepassingsservers die u kunt kiezen uit.

Hoewel het voorbeeld dat hier gebruikt sterk vereenvoudigd voor educatieve doeleinden, kan een Azure-implementatie-project ook andere belangrijke configuratie-informatie waarmee u bijna willekeurig complexe, schaalbare en maximaal beschikbaar maken bevatten meerdere lagen cloudservices met uw toepassingen. U kunt inschakelen **affiniteit sessie ("een tijdelijke sessies')**, **Snelle caching**, **SSL-offloading**, **firewallpoort routering**, **RAS**, en een aantal andere krachtige mogelijkheden.

Als u de vorige sectie van deze zelfstudie (' voor het implementeren van uw toepassing naar Azure, de snelle en eenvoudige manier') hebt voltooid, ziet u nu een nieuw project in de Azure-implementatie in de Projectverkenner automatisch voor u gegenereerd en de naam ' **MyHelloWorld_onAzure**'.

U kan hebben ook gestart in deze zelfstudie een Azure-implementatie leeg project eerst maken zelf en vervolgens toe te voegen uw toepassingen aan. Er is een langer proces, maar geeft u meer controle over de eerste configuratie vanaf het begin.

Klik op maken om een nieuw project in de Azure-implementatie de **nieuwe Azure-implementatieproject** knop ![][ic710876].

Ongeacht of u werken met een bestaand Azure-implementatie-project, of maken van een geheel nieuw, u kunt wijzigen van de configuratie-instellingen en -onderdelen, zoals de JDK of de toepassingsserver gelijkmatig zijn gemakkelijk op elk gewenst moment.

De JDK of de toepassingsserver of de lijst met toepassingen in een bestaand project in de Azure-implementatie wijzigen:

1. Vouw het projectknooppunt (bijvoorbeeld **MyHelloWorld_onAzure**) in de Projectverkenner

2. Met de rechtermuisknop op **WorkerRole1**

3. Vouw de **Azure** submenu in het contextmenu

4. Klik op **serverconfiguratie**

Ongeacht of u bent gestart deze serverconfiguratiestappen door een bestaand project in de Azure-implementatie te bewerken, zoals hierboven, of u een nieuwe maakt vanaf het begin, ziet u hetzelfde type dialoogvensters zodat u kunt uw JDK, servers en toepassingen configureren onderdelen. Zie voor meer informatie over het wijzigen van de instellingen in de dialoogvensters, bijvoorbeeld om te wijzigen van de JDK, de toepassingsserver en toepassingen toevoegen of verwijderen in een implementatie, de [configuratie-eigenschappen Server] [ Server configuration properties] artikel.

## <a name="windows-only-to-deploy-your-application-to-the-compute-emulator"></a>Alleen Windows: voor het implementeren van uw toepassing de rekenemulator

> [!NOTE]
> De Azure-emulator is alleen beschikbaar in Windows. Deze sectie overslaan als u een besturingssysteem dan Windows.
> 
> 

Als u de stappen eerder, dat wil zeggen impliciet een nieuw Azure-implementatie-project hebt gemaakt door uw toepassing met Azure, de JDK en de toepassing te publiceren zijn servers geconfigureerd voor de cloud, maar niet voor lokale geëmuleerd. Als u uw project voorbereiden voor het testen in de lokale emulator, de volgende stappen uit:

1. Klik in Projectverkenner van Eclipse **MyHelloWorld_onAzure**.

2. Met de rechtermuisknop op **WorkerRole1**.

3. Vouw de **Azure** submenu in het contextmenu.

4. Klik op **serverconfiguratie**.

5. Op de **JDK** tabblad, moet u controleren als de toolkit een standaardwaarde heeft vooraf geconfigureerde lokale JDK voor u. Als dat niet, of als u wilt wijzigen van de veronderstelde standaardwaarden, zorg ervoor dat de **de JDK die van dit bestandspad gebruiken om lokaal te testen** selectievakje is ingeschakeld en de installatielocatie JDK die u wilt gebruiken is opgegeven. Als u wijzigen wilt, klikt u op de **Bladeren** knop en selecteer de Active directory-locatie van de JDK die moet worden gebruikt met het besturingselement bladeren.

6. Klik op de **Server** tabblad.

7. In de **pad naar de lokale server** in het tekstvak onder in het dialoogvenster voert u het pad van een server met lokaal zijn geïnstalleerd die overeenkomt met het type en het primaire versienummer van de server die geselecteerd onder aan de bovenkant van het dialoogvenster de  **Een server van dit type implementeren** selectievakje. Als u gebruiken een ander type of de primaire versie van de toepassingsserver wilt, eerst de selectie onder dit selectievakje wijzigen.

8. Klik op **OK**.

9. Klik in de werkbalk van Eclipse op de **uitvoeren in Azure-Emulator** knop ![][ic710879]. Als de **uitvoeren in Azure-Emulator** knop is niet ingeschakeld, zorg ervoor dat **MyHelloWorld_onAzure** is geselecteerd in de Projectverkenner van Eclipse en zorg ervoor dat de Eclipse-Project Explorer focus als de huidige venster. Dit wordt eerst een volledige versie van uw project te starten en start vervolgens de Java-webtoepassing in de rekenemulator. (Afhankelijk van de prestatiekenmerken van de computer, de eerste build tussen een paar seconden een paar minuten kan duren, maar volgende builds krijgen sneller.) Nadat de eerste stap van de build is voltooid, wordt u door Windows Gebruikersaccountbeheer (UAC) gevraagd om toe te staan van deze opdracht om uw computer te wijzigen. Klik op **Ja**.

> [!IMPORTANT]
> Als u de UAC-prompt niet ziet, kijk op de taakbalk van Windows voor het pictogram UAC en klikt u op het eerst. Soms Gebruikersaccountbeheer prompt niet wordt weergegeven als een bovenste venster, maar alleen als een pictogram op de taakbalk zichtbaar is.
> 
> 

1. Bekijk de uitvoer van de rekenemulator gebruikersinterface om te bepalen of er problemen met uw project zijn. Afhankelijk van de inhoud van uw implementatie duurt enkele minuten duren voor uw toepassing volledig binnen de rekenemulator worden gestart.

2. Start uw browser en gebruikt u de URL `http://localhost:8080/MyHelloWorld` als het adres (de `MyHelloWorld` deel van de URL is hoofdlettergevoelig). U ziet nu uw toepassing MyHelloWorld (de uitvoer van index.jsp), vergelijkbaar met de volgende afbeelding:

   ![][ic589579]

Wanneer u klaar bent voor het stoppen van uw toepassing wordt uitgevoerd in de rekenemulator op de werkbalk van Eclipse, klikt u op de **opnieuw instellen van de Azure-Emulator** knop ![][ic710880].

## <a name="to-delete-your-deployment"></a>Verwijderen van uw implementatie
Zorg ervoor dat voor het verwijderen van uw implementatie binnen de Azure-werkset voor Eclipse **MyHelloWorld_onAzure** is geselecteerd in de Eclipse-Project Explorer, Controleer de Eclipse-Project Explorer heeft het huidige venster richten en klik vervolgens op de  **Publicatie ongedaan maken** knop ![][ic710883], op de werkbalk van Eclipse. (U kunt dezelfde bewerking doen met de rechtermuisknop op **MyHelloWorld_onAzure** in Eclipse van Projectverkenner te klikken op **Azure** en vervolgens te klikken op **Undeploy vanuit Azure Cloud**.) Hiermee wordt weergegeven de **ongedaan maken van de Azure-Project** dialoogvenster.

![][ic719491]

Selecteer het abonnement en cloud-service die uw implementatie bevat, selecteert u de implementatie die u wilt verwijderen en klik vervolgens op **publicatie ongedaan maken**.

(Een alternatief voor het gebruik van de toolkit verwijderen van de implementatie is met de **Cloud Services** sectie van de Azure-beheerportal: Ga naar uw implementatie, selecteert u deze en klik op de **verwijderen** de knop. Hiermee stopt en verwijder de implementatie. Als u alleen wilt stoppen met de implementatie en niet wordt verwijderd, klikt u op de **stoppen** knop in plaats van de **verwijderen** knop, maar als hierboven vermeld, als u de implementatie niet hebt verwijderd, factureerbare blijven de kosten samenvoegen voor uw implementatie zelfs als deze is gestopt).

## <a name="see-also"></a>Zie ook
[Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]

[De installatie van de Azure Toolkit voor Eclipse][Installing the Azure Toolkit for Eclipse] 

[Wat is er nieuw in de Azure werkset voor Eclipse][What's New in the Azure Toolkit for Eclipse]

Zie voor meer informatie over het gebruik van Azure met Java de [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Role Properties]: http://go.microsoft.com/fwlink/?LinkID=699525
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Enabling Remote Access for Azure Deployments in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699538
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Server configuration properties]: http://go.microsoft.com/fwlink/?LinkID=699525#server_configuration_properties
[What's New in the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

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
