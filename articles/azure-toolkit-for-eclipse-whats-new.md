---
title: Wat is er nieuw in de Azure werkset voor Eclipse
description: Meer informatie over de nieuwste functies in de Azure-werkset voor Eclipse.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 16b066ea-aae7-4c30-9a12-fa0c3711b93e
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm;asirveda;martinsawicki
ms.openlocfilehash: 71c4f2d2298ea54f18e9ed64b246966b470a4ff4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="whats-new-in-the-azure-toolkit-for-eclipse"></a>Wat is er nieuw in de Azure werkset voor Eclipse
## <a name="azure-toolkit-for-eclipse-releases"></a>Azure Toolkit voor Eclipse-versies
In dit artikel bevat informatie over de verschillende versies en de meest recente updates voor de Azure-werkset voor Eclipse.

> [!NOTE]
> Er is ook een Azure-werkset voor de IntelliJ IDE. Zie voor meer informatie [Azure Toolkit voor IntelliJ].
> 
> 

### <a name="april-14-2017"></a>14 april 2017
De Azure-werkset voor Eclipse - release van April 2017 omvat de volgende verbeteringen:

* **Verbeterde Azure-aanmelding In ervaring**: de Azure-Toolkit voor Eclipse ondersteunt nu twee methoden voor het aanmelden bij uw Azure-account: *interactief* en *automatisch*. Zie voor meer informatie [Azure aanmelding In instructies voor de Azure-werkset voor Eclipse].
* **Publiceren met behulp van Docker Containers**: U kunt nu uw webtoepassingen publiceren als Docker-Containers met Azure-Toolkit voor Eclipse. Zie voor meer informatie [het publiceren van een Web-App als een Docker-Container met de Azure-Toolkit voor Eclipse].
* **Opslagbeheer voor Account**: de Azure-Toolkit voor Eclipse biedt nu ondersteuning voor het beheer van uw storage-accounts vanuit de Verkenner-weergave van Azure. Zie voor meer informatie [beheren Storage-Accounts met de Azure-Explorer voor Eclipse].
* **Virtual Machine Management**: de Azure-Toolkit voor Eclipse biedt nu ondersteuning voor het beheren van uw virtuele machines vanuit de Verkenner-weergave van Azure. Zie voor meer informatie [het beheren van virtuele Machines met behulp van de Azure-Explorer voor Eclipse].
* **Verwijderen van de extern-ondersteuning voor foutopsporing**. Foutopsporing op afstand van Java-web-apps op Azure App Service is verwijderd uit de werkset Azure voor Eclipse; Dit is het nodig zijn voor het oplossen van problemen die klanten zijn krijgen als ze met de toolkit.

### <a name="august-26-2016"></a>26 augustus 2016
De Azure-werkset voor Eclipse - augustus 2016-release zijn de volgende uitbreidingen bevat:

* **Aangepaste JDK distributies**. De Azure-werkset voor Eclipse ondersteunt nu opgeven en het implementeren van een willekeurige versie van de JDK aan uw Azure-Web-App-container:
  * Naast de JDKs verstrekt door Azure, kunt u ook kiezen uit een breed selectie van Zulu OpenJDK versies beschikbaar gesteld in Azure door Azul systemen.
  * U kunt ook uw eigen distributie JDK opgeven als u deze als een ZIP-bestand naar uw opslagaccount uploaden.
* **Verbeteringen in de weergave Azure Explorer**:
  * Ondersteuning voor het beheer van virtuele Machine met behulp van de nieuwe Resource Manager-model van Azure: u kunt weergeven, maken en verwijderen van resource manager gebaseerde virtuele machines zonder de IDE.
  * Ondersteuning voor het Opslagaccount blob beheren met behulp van Azure Resource Manager, die is een aanvulling op de bestaande functionaliteit voor het beheren van 'klassiek' storage-accounts.
* **Microsoft JDBC-stuurprogramma 6.0 voor SQL Server**. Deze update bevat de meest recente JDBC-stuurprogramma voor Microsoft SQL Server (6.0), die is nu opgenomen als een bibliotheek die u eenvoudig aan uw Java-projecten toevoegen kunt, waardoor de oudere versie vervangen.

### <a name="june-29-2016"></a>29 juni 2016
De Azure-werkset voor Eclipse - release van juni 2016 omvat de volgende verbeteringen:

* **Java 8 vereiste**. De Azure-werkset voor Eclipse vereist nu Java 8, hoewel deze vereiste alleen voor de toolkit geldt-uw toepassingen kunnen blijven gebruiken van alle versies van Java die worden ondersteund door Azure.
* **Ondersteuning voor de meest recente Java-JDKs**. De nieuwste versies van de Java-JDKs worden nu ondersteund door de Azure-werkset voor Eclipse.
* **Ondersteuning voor Azure SDK v2.9.1**. De nieuwste versie van de Azure SDK is nu de minimale vereiste voor de Azure-werkset voor Eclipse.
* **Voorbeelden geïntegreerd**. De Azure-werkset voor Eclipse biedt nu verschillende voorbeeldtoepassingen waarmee ontwikkelaars aan de slag.
* **HDInsight-hulpprogramma integratie**. Azure HDInsight-hulpprogramma's worden nu gebundeld met de Azure-werkset voor Eclipse. Zie voor meer informatie [invoegtoepassing HDInsight Tools for Eclipse].
* **Foutopsporing op afstand van Java-Web-Apps**. De Azure-werkset voor Eclipse biedt nu ondersteuning voor foutopsporing op afstand van Java-web-apps op Azure App Service.
* **Ondersteuning voor de Eclipse-standaard-release.** De nieuwe Eclipse IDE voor minimaal vereiste versie is standaard.

### <a name="april-12-2016"></a>12 april 2016
De Azure-werkset voor Eclipse - release van April 2016 omvat de volgende verbeteringen:

* **Ondersteuning voor Azure SDK v2.9.0**. De nieuwste versie van de Azure SDK is nu de minimale vereiste voor de Azure-werkset voor Eclipse.
* **Diverse verbeteringen van bruikbaarheid, reactiesnelheid en prestaties gerelateerd aan Azure-Web-App ondersteuning**. Een aantal prestatieverbeteringen in hoe de Toolkit met Azure resultaat communiceert in een responsievere gebruikersinterface.
* **Mogelijkheid tot het verwijderen van een bestaande Web-App-container in Azure uit in Eclipse**. De Azure-werkset voor Eclipse kunt u nu een bestaande Azure-Web-container zonder Eclipse verwijderen.

### <a name="march-7-2016"></a>7 maart 2016
De Azure-werkset voor Eclipse - release van maart 2016 omvat de volgende verbeteringen:

* **Ondersteuning voor de snelle implementatie van lightweight Java-toepassingen**. De Azure-werkset voor Eclipse biedt nu ondersteuning voor de snelle implementatie van lightweight Java-toepassingen in Azure Web App Containers, zodat de Java-toepassingen nu implementeren seconden in plaats van minuten duurt.
* **Ondersteuning voor het beheer van Web-App de Azure-Verkenner-weergave**. De Azure-Verkenner-weergave in de werkset is nu ondersteuning biedt voor de aanbieding, starten en stoppen van Azure Web Apps.
* **Tomcat en Jetty Zulu OpenJDK distributies bijgewerkt**. De Azure-werkset voor Eclipse biedt ondersteuning voor bijgewerkte versies van Tomcat en Jetty van Zulu OpenJDK voor implementaties van Java in Azure-cloudservices.

### <a name="january-4-2016"></a>4 januari 2016
De Azure-werkset voor Eclipse - januari 2016-release zijn de volgende uitbreidingen bevat:

* **Ondersteuning voor de updates Zulu OpenJDK**. Zie voor meer informatie de [Azul systemen webpagina voor de OpenJDK Zulu].
* **Tomcat en Jetty distributies bijgewerkt**. De Jetty en Tomcat-distributies die beschikbaar op Microsoft Azure voor gebruik met de Azure-Toolkit voor Eclipse zijn zijn bijgewerkt.
* **Pariteit tussen Eclipse en IntelliJ Toolkits voor Azure functie**. De Azure-werkset voor Eclipse en de [Azure Toolkit voor IntelliJ] nu ondersteuning voor dezelfde reeks functies.

### <a name="september-1-2015"></a>1 september 2015
De Azure-werkset voor Eclipse - release van September 2015 omvat de volgende verbeteringen:

* **Ondersteuning voor de updates Zulu OpenJDK**. Zie voor meer informatie de [Azul systemen webpagina voor de OpenJDK Zulu].
* **Tomcat en Jetty distributies bijgewerkt**. De Jetty en Tomcat-distributies die beschikbaar op Microsoft Azure voor gebruik met de Azure-Toolkit voor Eclipse zijn zijn bijgewerkt. (Deze verdelingen kunnen ontwikkelaars maken snelle ontwikkeling en testen van de Azure-werkset voor Eclipse-projecten.
* **Ondersteuning voor automatisch bijgewerkt Tomcat en Jetty verwijzingen**. Naast de specifieke versies van Tomcat en Jetty die beschikbaar op Azure zijn, ontwikkelaars kunnen nu verwijzen naar een distributiepunt aangeduid als de ' nieuwste (automatisch bijgewerkt) ', die automatisch bijgewerkt naar de meest recente distributie van elke primaire versie van de Jetty of de volgende keer dat uw rolinstanties gerecycled zijn Tomcat. (Herhaald automatisch, maar ontwikkelaars kunnen handmatig een recyclebewerking via de Azure portal activeren.) Deze nieuwe functie betekent dat ontwikkelaars niet hoeft te implementeren om mogelijk zijn de server-software bijgewerkt om de toepassing. (
* Deze functionaliteit is momenteel alleen bedoeld voor ontwikkelings- en testdoeleinden of niet-bedrijfskritieke toepassingen, en wordt niet aanbevolen voor productie.)
* **Azure Verkenner-weergave voor blobs, wachtrijen en tabellen in Azure storage**. Hierdoor kunnen ontwikkelaars een aantal algemene taken met hun artefacten opslag rechtstreeks vanuit de Eclipse IDE uitvoeren. Bijvoorbeeld: verwijderen, uploaden of blobs downloaden.

### <a name="august-1-2015"></a>1 augustus 2015
De Azure-werkset voor Eclipse - augustus 2015-release zijn de volgende uitbreidingen bevat:

* **Application Insights Instrumentation Sleutelbeheer**. Deze update kunt u verkrijgen, maken en beheren van uw Application Insights-instrumentatiesleutels rechtstreeks vanuit de Eclipse IDE.
* **Microsoft JDBC-stuurprogramma 4.1 voor SQL Server**. Deze update bevat ondersteuning voor de meest recente JDBC-stuurprogramma voor Microsoft SQL Server.
* **2.7-versie van de Azure SDK**. Deze meest recente update voor de Azure SDK is de nieuwe vereiste voor de Toolkit wanneer geïnstalleerd onder Windows. (Opmerking: dit is niet nodig op niet-Windows-besturingssystemen.)
* **Ondersteuning voor het bijwerken van de v7 Zulu OpenJDK**. Zie voor meer informatie de [Azul systemen webpagina voor de OpenJDK Zulu].

### <a name="may-1-2015"></a>1 mei 2015
De Azure-werkset voor Eclipse - release van mei 2015 omvat de volgende verbeteringen:

* **Verbeterde serverselectie UI**. Deze release vereenvoudigt het gebruik van de toolkit op niet-Windows-besturingssystemen.
* **Ondersteuning voor Maven-projecten**. Deze release ondersteunt Maven-projecten als toepassingen, wat de toolkit in Azure kunt implementeren en configureren van Application Insights.
* **Versie 2.6 van de Azure SDK**. Deze meest recente update voor de Azure SDK is de nieuwe vereiste voor de Toolkit wanneer geïnstalleerd onder Windows. (Opmerking: dit is niet nodig op niet-Windows-besturingssystemen.)
* **Upgrade van de implementatie in plaats van opnieuw publiceren**. Als u opnieuw een implementatieproject publiceert wanneer de vorige versie al live is, gebruikt de toolkit nu upgrade functionaliteit van Azure implementatie in plaats van de vorige implementatie wordt afgesloten en opnieuw vanaf het begin te publiceren als in het verleden. Hiermee kunt de cloudservice om uit te voeren zonder onderbreking waar mogelijk, zodat een maximale beschikbaarheid realiseren zelfs tijdens een update en sneller opnieuw publiceren.
* **Ondersteuning voor de meest recente Zulu OpenJDK v8 - 40 bijwerken**. Zie voor meer informatie de [Azul systemen webpagina voor de OpenJDK Zulu].

### <a name="march-9-2015"></a>9 maart 2015
De Azure-werkset voor Eclipse - release van maart 2015 omvat de volgende verbeteringen:

* **Ondersteuning voor Mac, Ubuntu en aanvullende versies van Linux**. Deze versie van de Azure-werkset voor Eclipse voegt ondersteuning toe voor Mac OS en verschillende Unix-platforms, zodat ontwikkelaars de toolkit als u wilt maken, configureren en publiceren van Java-projecten voor Azure-Cloudservices (PaaS) van Eclipse dan uitgevoerd op besturingssystemen kunnen installeren Windows.

> [!NOTE]
> Deze mogelijkheid is een Preview-versie en het wordt niet aangeraden voor gebruik in productieomgevingen. Er is geen ondersteuning voor customer Service Level Agreement (SLA), maar alle feedback op prijs gesteld en aangemoedigd.
> 
> 

* **Nieuwe Application Insights-invoegtoepassing**. Ontwikkelaars kunnen nu voor het configureren van automatische servertelemetrie met behulp van Application Insights in Azure.
* **Opdrachtregel ant gebaseerde implementatie automation**. Deze functie kan ontwikkelaars de publicatie voor nieuwere versies van implementaties met Ant buiten Eclipse automatiseren. Een vooraf gegenereerde script wordt automatisch geconfigureerd voor een project nadat de eerste keer dat deze is geïmplementeerd vanaf Eclipse en latere implementaties het script gebruiken kunnen voor een volledig automatische implementaties via de opdrachtregel gebruikt.
* **Beschikbaarheid in Azure voor de implementatie van eenvoudiger, sneller Tomcat en Jetty**. Ontwikkelaars kunnen nu verwijzen naar verschillende versies voor Tomcat en Jetty die beschikbaar op Azure zijn rechtstreeks in plaats daarvan een Java-server bij hun account (of via de Toolkit), dus uploaden dat niet nodig is voor het uploaden van een Java-server voor snel aan de slag scenario's.
* **Snelle methode voor het publiceren van Java-web-apps naar Azure-cloudservices**. Als u het leerproces voor eenvoudige scenario's voor ontwikkeling en tests, kunnen ontwikkelaars Java-toepassingen meer direct naar Azure nu publiceren. In plaats van te doorlopen van het proces van het maken en configureren van een Azure-implementatie-project, zullen toepassingen worden geïmplementeerd met een standaardexemplaar van Tomcat v8 en Zulu JVM (OpenJDK).

### <a name="january-30-2015"></a>30 januari 2015
De Azure-werkset voor Eclipse - release van januari 2015 omvat de volgende verbeteringen:

* **Ondersteuning voor IBM® WebSphere® Application Server Liberty Core**. Deze release voegt IBM WebSphere Application Server Liberty Core toe aan de lijst met ondersteunde toepassingsservers van waaruit de toolkit kunt implementeren naar Azure is. De huidige lijst van de toepassingsservers die worden ondersteund door de meest recente toevoeging wordt uitgebreid &quot;out-of-the-box&quot; door de Toolkit die verschillende versies van Tomcat, Jetty, JBoss en GlassFish al is opgenomen.
* **Opname van Application Insights-SDK**. Deze bibliotheek nieuw uitgebrachte client-API (v0.9.0) maakt nu deel uit van het pakket voor Azure-beheerbibliotheken voor Java.
* **Pakket bijgewerkt voor Azure-beheerbibliotheken voor Java**. Deze update bevat de Azure-beheerbibliotheken voor Java v0.7.0 en v2.0.0 Storage Client-API, evenals de v0.9.0 nieuw uitgebrachte Application Insights-SDK.

### <a name="november-12-2014"></a>12 november 2014
De Azure-werkset voor Eclipse - release van November 2014, bevat de volgende verbeteringen:

* **Ondersteuning voor Azure SDK 2.5**. Deze meest recente update voor de Azure SDK is de nieuwe vereiste voor de Toolkit.
* **Ondersteuning voor bijgewerkte versie van de Zulu OpenJDK v1.8, v1.7 en v1.6 pakketten**. Zie voor meer informatie de [Azul systemen webpagina voor de OpenJDK Zulu].
* **Ondersteuning voor de nieuwe standaard D grootten voor cloudservices**, die betere prestaties en extra geheugenbronnen bieden. Zie voor meer informatie [virtuele Machine en Cloud Service Sizes for Azure].

### <a name="october-17-2014"></a>17 oktober 2014
De Azure-werkset voor Eclipse - release van oktober 2014, bevat de volgende verbeteringen:

* **Dankzij de prestatieverbeteringen in de publiceren op scenario's voor de**. Laden van gegevens van abonnementen is veel sneller wanneer gebruikers meerdere abonnementen en opslagaccounts hebben.
* **Ondersteuning voor bijgewerkte versie van het pakket met Zulu OpenJDK v1.8**. Zie voor meer informatie de [Azul systemen webpagina voor de OpenJDK Zulu].
* **Ondersteuning voor oudere versies van 3e partij JDKs bestandstypen**. Afgeschafte JDK pakketten wordt niet meer weergegeven in het vervolgkeuzemenu voor nieuwe implementatieprojecten. Bestaande projecten verwijzende afgeschaft JDK-pakketten te kunnen doen voor de tijd wordt, maar het wordt aanbevolen om bij te werken van dergelijke projecten zijn afhankelijk van de meest recente wordt voortgezet.
* **Bijgewerkte versie van het pakket voor Azure-beheerbibliotheken voor Java-clientbibliotheek API**. Zie voor meer informatie de [Microsoft Azure-Client API].
* **Oplossingen voor problemen.** Deze release bevat een aantal verschillende oplossingen voor problemen die zijn gebaseerd op Gebruikersrapporten en het testen.

### <a name="august-5-2014"></a>5 augustus 2014
Bevat de volgende uitbreidingen van de Azure-werkset voor Eclipse - augustus 2014-release

* **Ondersteuning voor Azure SDK 2.4.** Oudere versies van de Toolkit Eclipse werkt niet met deze nieuw uitgebrachte SDK.
* **Bijgewerkte versies van de v1.6 Zulu OpenJDK 1.7 en v1.8 pakketten.** Zie voor meer informatie de [Azul systemen webpagina voor de OpenJDK Zulu].
* **Bijgewerkte versie van het pakket voor Azure-beheerbibliotheken voor Java-clientbibliotheek API.** Zie voor meer informatie de [Microsoft Azure-Client API].
* **Ondersteuning voor de meest recente instellingen bestandsindeling publiceren.** Er is ondersteuning toegevoegd voor versie 2.0 van de bestandsindeling van de publicatie-instellingen.
* **Wijzigingen in de architectuur achter de publiceren naar de Cloud-functie.** De Toolkit maakt nu gebruik van de nieuw uitgebrachte Microsoft Azure-Client-API voor Java voor de ondersteuning voor publiceren-naar-cloud.
* **Oplossingen voor problemen.** Deze release bevat een aantal van de gebruiker heeft aangevraagd oplossingen voor problemen.

### <a name="june-12-2014"></a>12 juni 2014
De Azure-werkset voor Eclipse - release van juni 2014 is een kleine onderhoud update waarmee u de volgende verbeteringen:

* **Ondersteuning voor het pakket Zulu OpenJDK v1.8.** Zie voor meer informatie de [Azul systemen webpagina voor de OpenJDK Zulu].
* **Bijgewerkte versies van de v1.6 Zulu OpenJDK en 1,7 pakketten.** Zie voor meer informatie de [Azul systemen webpagina voor de OpenJDK Zulu].
* **Bijgewerkte versie van het pakket voor Azure-beheerbibliotheken voor Java-clientbibliotheek API.** Zie voor meer informatie de [Microsoft Azure-Client API].
* **Oplossingen voor problemen.** Deze release bevat een aantal van de gebruiker heeft aangevraagd oplossingen voor problemen.

### <a name="april-4-2014"></a>4 april 2014
De Azure-invoegtoepassing voor de Eclipse - release van April 2014 is uitgebracht. Dit is een update bij de release van de Azure SDK 2.3, die een vereiste is en automatisch worden gedownload wanneer u de invoegtoepassing installeren. Deze update bevat nieuwe functies, oplossingen voor problemen en een aantal verbeteringen feedback aangestuurde bruikbaarheid omdat de februari 2014 bekijken:

* **Ondersteuning voor de Azure SDK 2.3-release.** De Azure-invoegtoepassing voor de Eclipse - release van April 2014 vereist Azure SDK 2.3. Wanneer u de nieuwe invoegtoepassing gebruikt als u nog geen Azure SDK 2.3, wordt u gevraagd om toe te staan van de installatie. Gebruik geen Azure SDK 2.3 met eerdere versies van de invoegtoepassing.
* **Een upgrade van toepassingen zonder de volledige package-implementatie.** Bij het implementeren van Java-toepassingen die deel van uw project uitmaken, de invoegtoepassing nu automatisch geüpload in het geselecteerde opslagaccount zodat u kunt bijwerken en de Prullenbak van de rolinstanties voor het implementeren van de meest recente bits van de toepassing zonder te bouwen en Implementeer het volledige pakket opnieuw.
* **Tomcat 8 is nu een herkende toepassingsserver.** Als u een Tomcat-8-installatiemap op uw computer in de **Server** tabblad van de **Azure implementatieproject** dialoogvenster de invoegtoepassing wordt nu automatisch worden gedetecteerd en kunnen implementeren Tomcat 8 in een Automatische wijze, vergelijkbaar met de oudere versies van Tomcat al in de lijst.
* **Azul Zulu OpenJDK pakket updates: v1.7 update 51 en v1.6 47 bijwerken.** Met name handig bij deze release, van het systeem Azul Zulu Open JDK v7 pakketupdate 51 is beschikbaar. Bovendien gestart Zulu Open JDK v6-pakketten beschikbaar vanaf update 47. Deze updates zijn naast de eerder beschikbaar Zulu Open JDK v7 pakket update 45, 40 en 25 bijwerken.
* **Ondersteuning voor de grootte van A8 en A9 Microsoft Azure virtuele Machine.** U kunt nu een cloudservice op het hoge geheugen A8 en A9-VM-grootten implementeren. Zie voor meer informatie over deze VM-grootten [virtuele Machine en Cloud Service Sizes for Azure].
* **Automatische omleiding van HTTP naar HTTPS voor rollen SSL zijn ingeschakeld.** Wanneer de cloudservice alleen HTTPS-rollen, bevat als de aanvraag van de gebruiker is opgegeven voor HTTP, wordt het automatisch omgeleid naar HTTPS. Er is niet nodig voor het maken van een afzonderlijke rol voor het afhandelen van de HTTP-aanvragen.
* **Snelle Emulator gebruikt voor lokale geëmuleerd.** De Azure-Emulator Express wordt nu gebruikt als de emulator als uw toepassingen lokaal fouten opsporen.
* **Azure heeft is rebranded als Microsoft Azure.** UI-schermen weerspiegelen nu Azure rebranded en niet langer Azure aangeroepen.

### <a name="february-6-2014"></a>6 februari 2014
De Azure-invoegtoepassing voor de Eclipse - februari 2014 Preview heeft uitgegeven. Deze update bevat nieuwe functies, oplossingen voor problemen en een aantal verbeteringen feedback aangestuurde bruikbaarheid omdat de oktober 2013 Preview:

* **Ondersteuning voor SSL-offloading.** Offloading van Secure Sockets Layer (SSL) is toegevoegd als een functie, zodat u eenvoudig Hypertext Transfer Protocol Secure (HTTPS)-ondersteuning inschakelen in uw implementatie Java in Azure, zonder dat u SSL configureren op uw Java-toepassingsserver. Dit is met name relevant is in de sessie affiniteit en/of communicatiescenario geverifieerd. Bijvoorbeeld wanneer u het Filter Access Control Service (ACS), die al wordt ondersteund door de toolkit. Zie voor meer informatie [SSL-Offloading] en [hoe gebruik SSL-Offloading].
* **GlassFish 4 is nu een herkende toepassingsserver.** Als u een GlassFish 4-installatiemap op uw computer in de **Server** tabblad van de **Azure implementatieproject** dialoogvenster de invoegtoepassing wordt nu automatisch worden gedetecteerd en GlassFish implementeren UITEN 4 op automatische wijze, vergelijkbaar met de versie GlassFish UITEN 3 al in de lijst.
* **Pakketupdate Azul Zulu OpenJDK 45.** Effectieve met deze release, van het systeem Azul Zulu (v7-pakket openen JDK) update 45 is nu beschikbaar zijn; Dit is naast de update eerder beschikbaar 40 en update 25.
* **Ondersteuning voor 'auto' voor particuliere eindpuntpoorten.** U kunt een particuliere poort instellen op automatisch voor invoereindpunten en interne eindpunten om Azure automatisch toewijzen van een poort naar dat eindpunt te laten. Eerder kon u slechts een specifiek poortnummer toewijzen.
* **Ondersteuning voor het aanpassen van de naam (CN) van het certificaat in de gebruikersinterface voor het maken van de zelf-ondertekend certificaat.** Eerder is vastgelegde gelijknamige gebruikt voor alle nieuwe certificaten; Nu kunt u de naam van uw eigen certificaat te onderscheiden meerdere certificaten in de Azure portal gebruikt voor verschillende doeleinden.
* **Azure werkbalk:** de Azure-werkbalk heeft een bijgewerkt met de volgende wijzigingen: 
  * ![][ic710876]Dit pictogram is toegevoegd voor de **nieuwe Azure-implementatieproject**.
  * ![][ic710877]Dit pictogram is als een snelkoppeling toegevoegd aan het dialoogvenster voor het zelfondertekend certificaat maken.
* **Ondersteuning voor de grootte A5 Azure virtuele Machine.** U kunt nu een cloudservice implementeren voor het hoge geheugen A5-VM-grootte. Zie voor meer informatie over deze VM-grootte [virtuele Machine en Cloud Service Sizes for Azure].
* **Ondersteuning voor Microsoft Windows Server 2012 R2.** Windows Server 2012 R2 kunt u nu selecteren als het besturingssysteem van de cloud.

### <a name="october-22-2013"></a>22 oktober 2013
De Azure-invoegtoepassing voor de Eclipse - oktober 2013 Preview heeft uitgegeven. Deze update bevat nieuwe functies, oplossingen voor problemen en een aantal verbeteringen feedback aangestuurde bruikbaarheid nadat de September 2013 Preview:

* **Ondersteuning voor de Azure SDK 2.2-release.** De Azure-invoegtoepassing voor de Eclipse - Preview oktober 2013 ondersteunt Azure SDK 2.2. De invoegtoepassing wordt nog steeds werken met Azure SDK 2.1 en Azure SDK 2.2 worden automatisch geïnstalleerd als u nog geen ten minste Azure SDK 2.1 geïnstalleerd.
* **Pakketupdate Azul Zulu OpenJDK 40.** Als voor de September 2013 aangekondigd bekijken, de invoegtoepassing nu kunt met behulp van een derde partij geleverde JDK rechtstreeks in Azure, zonder dat u uw eigen JDK uploaden. In de release van oktober 2013 is van het systeem Azul Zulu (v7-pakket openen JDK) update 40 nu beschikbaar. Dit is naast de oorspronkelijk gepubliceerde update 25.
* **Koppeling van de cloud-implementatie in het gebeurtenissenlogboek.** Binnen Azure Activity Log, wanneer uw implementatie de status van heeft **gepubliceerde**, klikt u op **gepubliceerde** sinds het is nu een koppeling naar uw implementatie; uw implementatie wordt vervolgens in uw browser worden geopend. (De status van **gepubliceerde** eerder is met het label **met**.)
* **OS doelselectie beschikbaar op tijd publiceren.** De **publiceren naar Azure** dialoogvenster bevat een nieuw veld **doel OS**, waarmee u een overzichtelijker manier voor het instellen van het beoogde besturingssysteem.
* **De vorige implementatie automatisch overschreven.** De **publiceren naar Azure** dialoogvenster bevat een nieuwe selectievakje **overschrijven van de vorige implementatie**. Als deze optie is ingeschakeld, wanneer uw nieuwe implementatie gepubliceerd overschrijft automatisch de vorige implementatie; u zou niet ervaren &quot;409 conflict&quot; problemen bij het publiceren naar dezelfde locatie zonder eerst de vorige implementatie publicatie.
* **Jetty 9 is nu een herkende toepassingsserver.** Als u een Jetty 9-installatiemap op uw computer in de **Server** tabblad van de **Azure implementatieproject** dialoogvenster de invoegtoepassing wordt nu automatisch worden gedetecteerd en kunnen implementeren Jetty 9 in een Automatische wijze, vergelijkbaar met de oudere versies van Jetty al in de lijst.
* **Een functie in het contextmenu Project toevoegen.** De **Azure** contextmenu project bevat nu een nieuwe menuopdracht **rol toevoegen**, waarmee u een snellere en meer detecteerbaar manier om een nieuwe rol toevoegen aan uw Azure-project.
* **Een update van het pakket voor de Azure-beheerbibliotheken voor Java-bibliotheek.** Dit is gebaseerd op versie 0.4.6 van de [Microsoft Azure-Client API].

### <a name="september-25-2013"></a>25 september 2013
De Azure-invoegtoepassing voor de Eclipse - September 2013 Preview heeft uitgegeven. Deze update bevat nieuwe functies, oplossingen voor problemen en een aantal verbeteringen feedback aangestuurde bruikbaarheid omdat de augustus 2013 Preview:

* **Mogelijkheid tot het implementeren van het pakket Azul Zulu OpenJDK beschikbaar zijn op Azure.** Een nieuwe optie is toegevoegd bij het opgeven van de JDK die voor gebruik met uw Azure-implementatie. Deze optie gebruikt, kunt u een pakket van derden JDK rechtstreeks op de Azure-cloud implementeren zonder voor het uploaden van uw eigen. De eerste zoals opgeroepen Zulu pakket, op basis van de OpenJDK, kan nu worden geïmplementeerd met deze optie is het bieden van Azul systemen.
* **Een update van het pakket voor de Azure-beheerbibliotheken voor Java-bibliotheek.** Dit is gebaseerd op versie 0.4.5 van de [Microsoft Azure-Client API].

### <a name="august-1-2013"></a>1 augustus 2013
De Azure-invoegtoepassing voor de Eclipse - augustus 2013 Preview heeft uitgegeven. Dit is een update bij de release van de Azure SDK 2.1, die een vereiste is en automatisch worden gedownload wanneer u de invoegtoepassing installeren. Deze update bevat nieuwe functies, oplossingen voor problemen en een aantal verbeteringen feedback aangestuurde bruikbaarheid omdat de juli 2013 Preview:

* **Het verwijderen van de opties voor de lokale JDK en lokale toepassingsserver opnemen als onderdeel van het implementatiepakket.** Downloaden van de JDK en toepassingsserver van cloud-opslag tijdens de implementatie is voor het insluiten van deze onderdelen in het pakket, omdat het downloaden van de items resulteert in kleinere implementatie pakket grootte, of sneller implementatietijden beter en eenvoudiger onderhoud. Als gevolg hiervan zijn de opties om op te nemen van de JDK en de toepassingsserver in het implementatiepakket zijn verwijderd. Bestaande projecten die zijn geconfigureerd voor de lokale JDK en lokale toepassingsserver opnemen als onderdeel van het implementatiepakket wordt automatisch geconverteerd naar de JDK automatisch-upload en cloud-opslag-toepassingsserver.
* **Ondersteuning voor de Azure SDK 2.1-release.** De Azure-invoegtoepassing voor de Eclipse - augustus 2013 Preview vereist Azure SDK 2.1. Gebruik niet de augustus 2013 preview met eerdere versies van de Azure SDK en gebruik geen Azure SDK 2.1 met eerdere versies van de Azure-invoegtoepassing voor Eclipse.
* **Ondersteuning voor de Eclipse Kepler-release.** Daarmee kunnen vereiste de nieuwe minimaal versie Eclipse IDE Indigo is. De Azure-invoegtoepassing voor Eclipse is niet langer officieel getest op Helios.

### <a name="july-3-2013"></a>3 juli 2013
De Azure-invoegtoepassing voor de Eclipse - juli 2013 Preview heeft uitgegeven. Deze update bevat nieuwe functies, oplossingen voor problemen en een aantal verbeteringen feedback aangestuurde bruikbaarheid omdat de mei 2013 Preview:

* **De mogelijkheid een nieuw opslagaccount maken.** Een **nieuw** knop is toegevoegd aan de **Storage-Account toevoegen** dialoogvenster. Hiermee kunt u een opslagaccount binnen de Eclipse-invoegtoepassing maken zonder dat u zich aanmelden bij de Azure-beheerportal. (U moet al een Azure-abonnement om deze functie te gebruiken.) Zie voor meer informatie over het maken van een nieuw opslagaccount [voor het maken van een nieuw opslagaccount].
* **Nieuwe &quot;(automatisch)&quot; optie voor het opslagaccount voor automatische implementatie van JDK en de server en voor het opslaan in cache gebruikt.** Wanneer u de **automatisch uploaden** optie voor de JDK en toepassingsserver, kunt u nu opgeven **(automatisch)** voor het account-URL en de opslag moet worden gebruikt tijdens het uploaden van de JDK en toepassingsserver, of wanneer met behulp van Azure Caching. Vervolgens deze functies worden automatisch gebruikt hetzelfde opslagaccount als het account dat u selecteert in de **publiceren naar Azure** dialoogvenster. De [maken van een Hallo wereld-toepassing voor Azure in Eclipse] zelfstudie is bijgewerkt, zodat het gebruik van de nieuwe **(automatisch)** optie.
* **De mogelijkheid om in te stellen van uw Azure-service-eindpunten.** Geef op de service-eindpunten die bepalen dat of uw toepassing is geïmplementeerd en beheerd door de globale Azure-platform, door Azure worden beheerd door 21Vianet in China, of een persoonlijk die door Azure-platform. Zie voor meer informatie [Azure Service-eindpunten].
* **Grote implementaties kunnen opgeven van een resource voor lokale opslag.** In het geval dat de implementatie te groot om te worden opgenomen in de standaard approot-map is, kunt u nu een resource voor lokale opslag opgeven als het doel van de implementatie voor uw JDK en toepassingsservers. Zie voor meer informatie [grote implementaties implementeren].
* **Ondersteuning voor de grootte van A6 en A7 Azure virtuele Machine.** U kunt nu een cloudservice op het hoge geheugen A6 en A7-VM-grootten implementeren. Zie voor meer informatie over deze formaten [virtuele Machine en Cloud Service Sizes for Azure].
* **Een update van het pakket voor de Azure-beheerbibliotheken voor Java-bibliotheek.** Dit is gebaseerd op versie 0.4.4 van de [Microsoft Azure-Client API].

### <a name="may-1-2013"></a>1 mei 2013
De Azure-Eclipse - invoegtoepassing kan 2013 Preview is vrijgegeven. Dit is een belangrijke update bij de release van de Azure SDK 2.0, die een vereiste is en automatisch worden gedownload wanneer u de invoegtoepassing installeren. Deze versie bevat nieuwe functies, oplossingen voor problemen en een aantal verbeteringen feedback aangestuurde bruikbaarheid, omdat de februari 2013 Preview:

* **Automatische uploaden van de JDK en de toepassingsserver en de implementatie van Azure-opslag.** Een nieuwe optie die automatisch wordt geüpload de geselecteerde JDK en toepassingsservers, indien nodig, naar een opgegeven Azure storage-account en implementeert deze onderdelen van daaruit in plaats van insluiten in het implementatiepakket of het uploaden van de gebruiker vervolgens handmatig hebben. Deze veelvuldig opgevraagde functie kunt u het gemak van de implementatie van de JDK- en serveronderdelen, met name voor beginnende gebruikers aanzienlijk verbeteren. Zie voor een procedure die deze opties gebruikt, [maken van een Hallo wereld-toepassing voor Azure in Eclipse].
* **Centraal opslagaccount bijhouden en de mogelijkheid om verwijzing storage-accounts meer eenvoudig (via een besturingselement voor vervolgkeuzelijst).** Dit geldt voor meerdere functies die van opslag, zoals JDK en implementatie van de server-onderdeel en opslaan in cache gebruikmaken. Zie voor meer informatie [Azure Storage-Accountlijst].
* **Eenvoudig instellen van externe toegang in het publiceren naar de wizard Cloud.** U hoeft alleen type in een gebruikersnaam en wachtwoord inschakelen van externe toegang of laat dit veld leeg te houden van externe toegang uitgeschakeld is.
* **Een update van het pakket voor de Azure-beheerbibliotheken voor Java-bibliotheek.** Dit is gebaseerd op versie 0.4.2 van de [Microsoft Azure-Client API].
* **Ondersteuning voor een tijdelijke sessies op Windows Server 2012.** Een tijdelijke sessies gewerkt voorheen alleen op Windows Server 2008 R2 nu beide besturingssysteem doelen ondersteuning sessie affiniteit cloud.
* **Prestatieverbeteringen voor pakket uploaden.** Zelfs wanneer de JDK en toepassingsserver zijn ingesloten in het implementatiepakket, is het gedeelte van het uploaden van het implementatieproces kan ongeveer twee keer zo snel in vergelijking met vorige versies.

### <a name="february-8-2013"></a>8 februari 2013
De Azure-invoegtoepassing voor de Eclipse - februari 2013 Preview heeft uitgegeven. Dit is een kleine update waaronder bugfixes, feedback aangestuurde gebruiksvriendelijkheid en enkele nieuwe functies sinds de November 2012 bekijken:

* Ondersteuning voor het implementeren van JDKs, toepassingsservers, en willekeurige andere onderdelen van openbare of persoonlijke Azure blob-opslag-downloads in plaats van in het implementatiepakket inclusief, bij het implementeren van de cloud.
* Mogelijkheid om de volgorde waarin een gebruiker gedefinieerde onderdelen van een rol worden verwerkt, door de toevoeging van **omhoog** en **omlaag** knoppen in de **onderdelen** sectie van de **Azure roleigenschappen**.
* Een update voor de **-pakket voor de Azure-beheerbibliotheken voor Java** bibliotheek, gebaseerd op versie 0.4.0 van de [Microsoft Azure-Client API].

### <a name="november-5-2012"></a>5 november 2012
De Azure-invoegtoepassing voor de Eclipse - November 2012 Preview heeft uitgegeven. Dit is een belangrijke update waaronder een aantal nieuwe functies, evenals aanvullende oplossingen voor problemen en bruikbaarheid feedback aangestuurde verbeteringen, omdat de September 2012 bekijken:

* Ondersteuning voor Microsoft Windows Server 2012 als het besturingssysteem van de cloud.
* Ondersteuning voor Azure CO-locaties opslaan in cache-ondersteuning voor memcached-clients.
* Het opnemen van de Apache Qpid JMS clientbibliotheken voor profiteren van Azure AMQP gebaseerde uitwisseling van berichten.
* Een verbeterde **nieuw Project** wizard met een nieuwe pagina aan het einde waarmee gebruikers de mogelijkheid om te snel geschikt maken van verschillende algemene belangrijke functies in hun project: een tijdelijke sessies, opslaan in cache en foutopsporing op afstand.
* Automatische vermindering van rolinstanties op 1 wanneer uitgevoerd in de rekenemulator om te voorkomen dat poort bindingsconflicten tussen serverexemplaren.

### <a name="september-28-2012"></a>28 september 2012
De Azure-invoegtoepassing voor de Eclipse - September 2012 Preview heeft uitgegeven. Deze service-update bevat een aantal aanvullende oplossingen voor problemen, omdat de augustus 2012 bekijken, evenals een aantal feedback aangestuurde verbeteringen in bestaande functies:

* Ondersteuning voor Microsoft Windows 8 en Microsoft Windows Server 2012 als het besturingssysteem van de ontwikkeling, het oplossen van problemen die eerder voorkomen dat de invoegtoepassing goed werkt in deze besturingssystemen.
* Verbeterde ondersteuning voor het eindpunt poortbereiken opgeven.
* Oplossingen voor problemen betrekking hebben op paden die spaties bevat.
* Rol context menu verbeteringen voor sneller toegang tot specifieke configuratie-instellingen.
* Secundaire verfijningen in de **publiceren naar de cloud** wizard en een aantal aanvullende oplossingen voor problemen.

### <a name="august-28-2012"></a>28 augustus 2012
De Azure-invoegtoepassing voor de Eclipse - augustus 2012 Preview heeft uitgegeven. Deze service-update bevat aanvullende oplossingen voor problemen, omdat de juli-2012 bekijken, evenals verschillende feedback aangestuurde bruikbaarheid verbeteringen voor bestaande functies:

* In het dialoogvenster Azure Access Control-servicefilter:
  * **Optie voor het insluiten van het handtekeningcertificaat** in uw toepassing WAR-bestand voor het vereenvoudigen van cloudimplementatie.
  * **Optie voor het maken van een zelfondertekend certificaat** binnen de ACS filteren gebruikersinterface. Zie voor meer informatie over het Filter Azure Access Control-Services, [Web gebruikers verifiëren met Azure Access Control-Service met behulp van Eclipse].
* In de wizard Azure-implementatieproject (ook van toepassing op de eigenschappenpagina van de rol-serverconfiguratie):
  * **Automatische detectie van de locatie JDK** op uw computer (die u kunt desgewenst overschrijven).
  * **Automatische detectie van het servertype** wanneer u de installatiemap van de toepassing-server selecteert.

### <a name="july-15-2012"></a>15 juli 2012
De Azure-invoegtoepassing voor de Eclipse - juli 2012 Preview waarin een aantal van de hoogste prioriteit fouten gevonden en/of door gebruikers zijn gerapporteerd na de release van juni 2012 heeft uitgegeven. Dit is een service-update alleen, er zijn geen nieuwe functies zijn opgenomen.

### <a name="june-7-2012"></a>7 juni 2012
Azure-invoegtoepassing voor de Eclipse - juni 2012 CTP heeft uitgegeven. Nieuwe functies:

* **Wizard Nieuw Project voor Azure-implementatie:** kunt u uw JDK Java-toepassingsserver en Java-toepassingen rechtstreeks in de verbeterde wizard gebruikersinterface. Opgenomen in de lijst met out-of-the-box-serverconfiguraties kiezen die zijn Tomcat 6 Tomcat 7, GlassFish UITEN 3, Jetty 7, 8 Jetty, 6 JBoss en JBoss 7 (zelfstandig). Bovendien kunt u de lijst met serverconfiguraties aanpassen. Deze gebruikersinterface verbetering vormt een alternatief slepen en neerzetten van gecomprimeerde bestanden en kopiëren over opstartscripts, voorheen de belangrijkste benadering. Deze methode werkt goed samen, maar die waarschijnlijk alleen voor meer geavanceerde scenario's wordt gebruikt.
* **Configuratie-eigenschappenpagina met de serverfunctie:** kunt u gemakkelijk veranderen de JDKs, Java-toepassingsservers en toepassingen die zijn gekoppeld aan uw implementatie, nadat u het project hebt gemaakt. Zie voor meer informatie [configuratie-eigenschappen Server].
* **&quot;Publiceren naar cloud&quot; wizard:** biedt een eenvoudige manier voor het implementeren van uw project naar Azure rechtstreeks vanaf Eclipse automatisering van de eerder handmatige zware-verhoging van het ophalen van referenties, aanmelding bij de Azure-beheerportal uploaden van een pakket, enzovoort. Zie voor een voorbeeld van het implementeren van uw project direct naar Azure, [maken van een Hallo wereld-toepassing voor Azure in Eclipse].
* **Azure werkbalk:** Azure werkbalk is nu beschikbaar in Eclipse met knoppen die gebruikmaken van de volgende functies:
  * ![][ic710879]**Uitvoeren in Azure-Emulator**: uw project in de emulator wordt uitgevoerd.
  * ![][ic710880]**Opnieuw instellen van de Azure-Emulator**: Hiermee stelt u de emulator.
  * ![][ic710881]**Cloud-pakket voor Azure bouwen**: het pakket voor de implementatie wordt gecompileerd.
  * ![][ic710876]**Nieuwe Azure-implementatieproject**: maakt een nieuw project in de Azure-implementatie.
  * ![][ic710882]**Publiceren naar Azure-Cloud**: uw project naar Azure publiceert.
  * ![][ic710883]**Publicatie ongedaan maken**: Hiermee verwijdert u uw implementatie.
  * Veel van deze Azure werkbalkknoppen worden gebruikt in [maken van een Hallo wereld-toepassing voor Azure in Eclipse].
* **Azure-beheerbibliotheken voor Java:** nu beschikbaar als onderdeel van het één pakket voor Azure-beheerbibliotheken voor Java-bibliotheek in Eclipse, waarvan de installatie van de invoegtoepassing en met alle vereiste afhankelijkheden. Alleen een verwijzing naar de bibliotheek toevoegen in uw Java-project en u hoeft niet te downloaden van items die afzonderlijk. Zie voor meer informatie [installeren van de Azure-werkset voor Eclipse].
* **Microsoft JDBC-stuurprogramma 4.0 voor SQL Server beschikbaar is tijdens de installatie van de invoegtoepassing:** tijdens de installatie van de nieuwe invoegtoepassing de nieuwste versie van het Microsoft JDBC-stuurprogramma voor SQL Server kan worden geïnstalleerd.
* **Azure Access Control Service Filter beschikbaar tijdens de installatie van de invoegtoepassing:** deze nieuw onderdeel als een Eclipse-bibliotheek in de werkset kunt u uw Java-webtoepassing naadloos profiteren van Azure Access Control Service (ACS) verificatie met behulp van verschillende identiteitsproviders, zoals Google en Live.com Yahoo!. U hoeft niet te verificatielogica zelf schrijven, slechts enkele opties configureren en kunt het filter doen het zware werk gebruikers zich aanmelden met ACS in te schakelen. U kunt alleen zich richten op het schrijven van de code die gebruikers toegang tot bronnen op basis van hun identiteit biedt voor uw toepassing door het filter in het Request-object geretourneerd. Zie voor een zelfstudie over het gebruik van de ACS-filter [Web gebruikers verifiëren met Azure Access Control-Service met behulp van Eclipse].
* **Automatische detectie van de Azure SDK 1.7 vereiste:** wanneer u een nieuw Project voor de Azure-implementatie maakt, Azure SDK 1.7 automatisch wordt gedownload als deze nog niet is geïnstalleerd.
* **Exemplaar van eindpunten:** Hiermee kunt u directe poort eindpunt toegang voor communicatie met load balanced rolinstanties. Exemplaareindpunten kunnen worden toegevoegd via de eindpunten-gebruikersinterface beschikbaar via de [eindpunten eigenschappen] pagina. Dit helpt foutopsporing op afstand inschakelen en JMX diagnostische gegevens voor bepaalde berekeningen uitgevoerd in de cloud in scenario's met meerdere exemplaren-implementaties-instantie. 
* **UI-onderdelen:** eenvoudiger voor ervaren gebruikers voor het instellen van projectafhankelijkheden tussen de afzonderlijke Azure rollen in het project en andere externe bronnen zoals Java-toepassing projecten; ook kunt u eenvoudig de logica van de implementatie wordt beschreven. Zie voor meer informatie [onderdelen eigenschappen].
* **Automatische upgrade van eerdere versies van de projecten:** wanneer u een werkruimte met Azure-project gemaakt met een eerdere versie van de invoegtoepassing opent, de oude projecten wordt weergegeven in Eclipse als gesloten, omdat eerdere versies van de projecten niet compatibel met de nieuwe versie. Als u probeert een van deze oude projecten wilt openen, wordt een wizard upgrade wordt gestart. Als u akkoord met de upgrade, een nieuw project met gaat **_Upgraded** toegevoegd aan de naam, wordt gemaakt en automatisch bijgewerkt om te werken met de nieuwe versie. U kunt het nieuwe project hernoemen naar behoefte. Als onderdeel van de upgrade wordt het oorspronkelijke project worden niet gewijzigd (en blijft gesloten).

### <a name="december-10-2011"></a>10 december 2011
Azure-invoegtoepassing voor de Eclipse - December 2011 CTP heeft uitgegeven. Nieuwe functies:

* **Sessie affiniteit (&quot;een tijdelijke sessies&quot;) ondersteunen:** helpen inschakelen stateful, Java-toepassingen met één checkbox geclusterd. Zie voor meer informatie [sessie affiniteit].
* **Starten van de script-voorbeelden en-klare:** voor de meest populaire Java-servers (Tomcat, Jetty, JBoss, GlassFish), die u kunt alleen kopiëren en plakken van uw project voorbeelden directory in uw opstartscript.
* **Uitvoer van de emulator opstarten in realtime:** u kunt nu bekijken tijdens de uitvoering van alle stappen van het opstartscript in een speciale consolevenster, waarin u de voortgang en fouten in het script als deze wordt uitgevoerd door Azure.
* **Automatische, lichte java.exe bewaking:** die een rol recycle forceert nadat java.exe uitgevoerd, met een lichtgewicht, vooraf gemaakte script automatisch opgenomen in uw implementatie.
* **Externe Java-app foutopsporing van de gebruikersinterface voor configuratie:** kunt u eenvoudig inschakelen van Eclipse externe foutopsporingsprogramma voor toegang tot uw Java-app uitgevoerd in de Emulator of de Azure-cloud, zodat u kunt doorlopen en foutopsporing van uw Java-code in realtime. Zie voor meer informatie [Azure-toepassingen foutopsporing in Eclipse].
* **Lokale opslag resourceconfiguratie UI:** zodat u niet langer hoeft te configureren van lokale bronnen door het XML-bestand rechtstreeks bewerken. Deze functie kunt u toegang tot het effectieve bestandspad van de lokale resource nadat deze geïmplementeerd via een omgevingsvariabele die u kunt verwijzen naar rechtstreeks vanuit uw opstartscript. Zie voor meer informatie [eigenschappen van lokale opslag].
* **Configuratie van de omgeving variabele gebruikersinterface:** zodat u niet langer hoeft in te stellen omgevingsvariabelen via handmatige bewerking van de configuratie-XML. Zie voor meer informatie [variabelen omgevingseigenschappen].
* **JDBC-stuurprogramma voor SQL Azure:** via de invoegtoepassing wordt geïnstalleerd als een naadloos geïntegreerde Eclipse-bibliotheek eenvoudiger programmeren voor SQL Azure inschakelen. 
* **Contextmenu is snel toegang tot rolconfiguratie UI**: alleen met de rechtermuisknop op de map voor de rol en klikt u op **eigenschappen**.
* **Aangepaste Azure project en rol pictogrammen van de map:** voor betere zichtbaarheid en navigatie in uw werkruimte en het project te vereenvoudigen.

## <a name="see-also"></a>Zie ook
Voor meer informatie over de Azure Toolkits voor Java-IDE's klikt u op de volgende koppelingen:

* [Azure Toolkit voor Eclipse]
  * *Wat is er nieuw in de Azure werkset voor Eclipse (in dit artikel)*
  * [installeren van de Azure-werkset voor Eclipse] (De Azure Toolkit voor Eclipse installeren)
  * [Een Hallo wereld Web-App maken voor Azure in Eclipse]
  * [Sign In Instructions for the Azure Toolkit for Eclipse] (Aanmeldingsinstructies voor de Azure Toolkit voor Eclipse)
* [Azure Toolkit voor IntelliJ] (Azure Toolkit voor IntelliJ)
  * [What's New in the Azure Toolkit for IntelliJ] (Nieuw in de Azure Toolkit voor IntelliJ)
  * [Installing the Azure Toolkit for IntelliJ] (De Azure Toolkit voor IntelliJ installeren)
  * [Sign In Instructions for the Azure Toolkit for IntelliJ] (Aanmeldingsinstructies voor de Azure Toolkit voor IntelliJ)
  * [Een Hallo wereld Web-App maken voor Azure in IntelliJ]

In het [Azure Java Developer Center] vindt u meer informatie over het gebruik van Azure met Java.

<!-- URL List -->

[Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit voor IntelliJ]: ./azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)
[Een Hallo wereld Web-App maken voor Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Een Hallo wereld Web-App maken voor Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[installeren van de Azure-werkset voor Eclipse]: ./azure-toolkit-for-eclipse-installation.md (De Azure Toolkit voor Eclipse installeren)
[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (De Azure Toolkit voor IntelliJ installeren)
[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md (Aanmeldingsinstructies voor de Azure Toolkit voor Eclipse)
[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md (Aanmeldingsinstructies voor de Azure Toolkit voor IntelliJ)
[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md (Nieuw in de Azure Toolkit voor IntelliJ)

[Azure aanmelding In instructies voor de Azure-werkset voor Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[het publiceren van een Web-App als een Docker-Container met de Azure-Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse-publish-as-docker-container.md
[beheren Storage-Accounts met de Azure-Explorer voor Eclipse]: ./azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer.md
[het beheren van virtuele Machines met behulp van de Azure-Explorer voor Eclipse]: ./azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer.md

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547

[Azul systemen webpagina voor de OpenJDK Zulu]: http://go.microsoft.com/fwlink/?LinkId=402457
[Azure Service-eindpunten]: http://go.microsoft.com/fwlink/?LinkID=699526
[Azure Storage-Accountlijst]: http://go.microsoft.com/fwlink/?LinkID=699528
[onderdelen eigenschappen]: http://go.microsoft.com/fwlink/?LinkID=699525#components_properties
[maken van een Hallo wereld-toepassing voor Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Azure-toepassingen foutopsporing in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699535
[grote implementaties implementeren]: http://go.microsoft.com/fwlink/?LinkID=699536
[eindpunten eigenschappen]: http://go.microsoft.com/fwlink/?LinkID=699525#endpoints_properties
[variabelen omgevingseigenschappen]: http://go.microsoft.com/fwlink/?LinkID=699525#environment_variables_properties
[invoegtoepassing HDInsight Tools for Eclipse]: ./hdinsight/hdinsight-apache-spark-eclipse-tool-plugin.md
[Web gebruikers verifiëren met Azure Access Control-Service met behulp van Eclipse]: http://go.microsoft.com/fwlink/?LinkID=264703
[hoe gebruik SSL-Offloading]: http://go.microsoft.com/fwlink/?LinkID=699545
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546 (De Azure Toolkit voor Eclipse installeren)
[eigenschappen van lokale opslag]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties
[Microsoft Azure-Client API]: http://go.microsoft.com/fwlink/?LinkId=280397
[configuratie-eigenschappen Server]: http://go.microsoft.com/fwlink/?LinkID=699525#server_configuration_properties
[sessie affiniteit]: http://go.microsoft.com/fwlink/?LinkID=699548
[SSL-Offloading]: http://go.microsoft.com/fwlink/?LinkID=699549
[voor het maken van een nieuw opslagaccount]: http://go.microsoft.com/fwlink/?LinkID=699528#create_new
[virtuele Machine en Cloud Service Sizes for Azure]: http://go.microsoft.com/fwlink/?LinkId=466520

<!-- IMG List -->

[ic710876]: ./media/azure-toolkit-for-eclipse-whats-new/ic710876.png
[ic710877]: ./media/azure-toolkit-for-eclipse-whats-new/ic710877.png
[ic710879]: ./media/azure-toolkit-for-eclipse-whats-new/ic710879.png
[ic710880]: ./media/azure-toolkit-for-eclipse-whats-new/ic710880.png
[ic710881]: ./media/azure-toolkit-for-eclipse-whats-new/ic710881.png
[ic710876]: ./media/azure-toolkit-for-eclipse-whats-new/ic710876.png
[ic710882]: ./media/azure-toolkit-for-eclipse-whats-new/ic710882.png
[ic710883]: ./media/azure-toolkit-for-eclipse-whats-new/ic710883.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh694270.aspx -->
