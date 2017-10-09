---
title: aaaGet slag met Azure Search in Java | Microsoft Docs
description: Hoe zoeken toobuild een gehoste cloud toepassing in Azure met behulp van Java als uw programmeertaal.
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 8b4df3c9-3ae5-4e3a-b4bb-74b516a91c8e
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 07/14/2016
ms.author: evboyle
ms.openlocfilehash: 5476a2103f3b60fe6ec78ff3d3fdba9fcff55c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-java"></a>Aan de slag met Azure Search in Java
> [!div class="op_single_selector"]
> * [Portal](search-get-started-portal.md)
> * [.NET](search-howto-dotnet-sdk.md)
> 
> 

Meer informatie over hoe toobuild een aangepaste Java-toepassing die gebruikmaakt van Azure Search voor de zoekfunctie zoeken. Deze zelfstudie wordt gebruikgemaakt van Hallo [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct Hallo objecten en bewerkingen in deze oefening.

toorun dit voorbeeld hebt u een Azure Search-service, u voor Hallo aanmelden kunt [Azure Portal](https://portal.azure.com). Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor stapsgewijze instructies.

We Hallo na software toobuild gebruikt en testen van dit voorbeeld:

* [Eclipse IDE voor Java EE-ontwikkelaars](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar). Worden ervoor toodownload Hallo EE-versie. Een van de verificatiestappen Hallo vereist een functie die alleen in deze versie is gevonden.
* [JDK 8u40](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Apache Tomcat 8.0](http://tomcat.apache.org/download-80.cgi)

## <a name="about-hello-data"></a>Over Hallo-gegevens
Deze voorbeeldtoepassing gebruikt gegevens uit Hallo [Verenigde Staten Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), gefilterd op Hallo staat Rhode Island tooreduce Hallo gegevensset grootte. We gebruiken deze gegevens toobuild een zoektoepassing die kenmerkende gebouwen zoals ziekenhuizen en scholen, evenals geologische kenmerken, zoals stromen, meren en toppen retourneert.

In deze toepassing hello **SearchServlet.java** programma bouwt en belastingen Hallo index met behulp van een [indexeerfunctie](https://msdn.microsoft.com/library/azure/dn798918.aspx) constructie, bij het ophalen van Hallo gefilterde USGS-gegevensset uit een openbare Azure SQL Database. Vooraf gedefinieerde referenties en informatie toohello Onlinegegevens verbindingsbron vindt u in Hallo programmacode. Voor de toegang tot de gegevens hoeft u verder niets te configureren.

> [!NOTE]
> We een filter toegepast op deze gegevensset toostay onder Hallo 10.000 Documentlimiet Hallo gratis prijscategorie. Als u de standaardcategorie Hallo gebruikt, deze limiet niet van toepassing en kunt u deze code toouse een grotere gegevensset wijzigen. Zie [Limieten en beperkingen](search-limits-quotas-capacity.md) voor meer informatie over de capaciteit voor elke prijscategorie.
> 
> 

## <a name="about-hello-program-files"></a>Over het Hallo-programmabestanden
Hallo hieronder wordt beschreven Hallo-bestanden die betrokken toothis voorbeeld zijn.

* Search.JSP: Levert Hallo-gebruikersinterface
* SearchServlet.java: Biedt methoden (vergelijkbaar tooa controller in MVC)
* SearchServiceClient.java: verwerkt de HTTP-aanvragen
* SearchServiceHelper.java: een helperklasse die statische methoden biedt
* Document.Java: Levert het gegevensmodel Hallo
* Config.Properties: stelt Hallo Search-service-URL en api-sleutel
* Pom.XML: een Maven-afhankelijkheid

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a>Hallo-servicenaam en api-sleutel van uw Azure Search-service zoeken
Alle REST-API-aanroepen in Azure Search is vereist dat u Hallo service-URL en api-sleutel opgeven. 

1. Meld u aan toohello [Azure Portal](https://portal.azure.com).
2. Klik in de snelbalk hello **zoekservice** toolist alle hello Azure Search-services worden ingericht voor uw abonnement.
3. Selecteer de gewenste toouse Hallo-service.
4. Op Hallo servicedashboard ziet u tegels weergegeven voor essentiële informatie evenals sleutelpictogram voor toegang tot de beheersleutels Hallo Hallo.
   
      ![][3]
5. Kopieer Hallo service-URL en een beheersleutel. Moet u ze later, wanneer u ze toohello toevoegt **config.properties** bestand.

## <a name="download-hello-sample-files"></a>Hallo voorbeeldbestanden downloaden
1. Ga te[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) op GitHub.
2. Klik op **ZIP downloaden**, Hallo ZIP-bestand toodisk opslaan en pak vervolgens alle Hallo bestanden bevat. Houd rekening met het uitpakken van Hallo-bestanden in uw werkruimte Java toomake eenvoudiger toofind Hallo project later.
3. Hallo voorbeeldbestanden zijn alleen-lezen. Met de rechtermuisknop op mapeigenschappen en wissen Hallo-kenmerk voor alleen-lezen.

Alle volgende bestandswijzigingen en uitvoerinstructies worden uitgevoerd voor de bestanden in deze map.  

## <a name="import-project"></a>Project importeren
1. Klik in Eclipse achtereenvolgens op **File** >  (Bestand)**Import** (Importeren) > **General** (Algemeen) > **Existing Projects into Workspace** (Bestaand project naar werkruimte).
   
    ![][4]
2. In **Selecteer hoofdmap**, toohello map met de voorbeeldbestanden bladeren. Selecteer Hallo-map met de map .project Hallo. Hallo-project moet worden weergegeven in Hallo **projecten** lijst als een geselecteerd item.
   
    ![][12]
3. Klik op **Voltooien**.
4. Gebruik **Projectverkenner** tooview en bewerk Hallo-bestanden. Als deze nog niet is geopend, klikt u op **venster** > **weergave tonen** > **Projectverkenner** of gebruik Hallo snelkoppeling tooopen deze.

## <a name="configure-hello-service-url-and-api-key"></a>Hallo-service-URL en api-sleutel configureren
1. In **Projectverkenner**, dubbelklikt u op **config.properties** tooedit Hallo configuratie-instellingen met de Hallo-servernaam en api-sleutel.
2. Raadpleeg toohello eerdere stappen in dit artikel, waarin u Hallo service-URL en api-sleutel in Hallo gevonden [Azure Portal](https://portal.azure.com), tooget Hallo waarden die u nu moet opgeven in **config.properties**.
3. In **config.properties**, vervangen door 'Api Key' hello api-sleutel voor uw service. Vervolgens servicenaam (Hallo eerste onderdeel van Hallo URL http://servicename.search.windows.net) vervangen door 'service name' in hello hetzelfde bestand.
   
    ![][5]

## <a name="configure-hello-project-build-and-runtime-environments"></a>Hallo-project, build en runtime-omgeving configureren
1. In Eclipse in Projectverkenner met de rechtermuisknop op Hallo project > **eigenschappen** > **Project-facetten**.
2. Selecteer **Dynamic Web Module** (Dynamische webmodule), **Java** en **JavaScript**.
   
    ![][6]
3. Klik op **Apply** (Toepassen).
4. Selecteer **Window** (Venster) > **Preferences** (Voorkeuren) > **Server** > **Runtime Environments** (Runtime-omgevingen) > **Add..** (Toevoegen).
5. Vouw Apache uit en selecteer Hallo-versie van Hallo Apache Tomcat-server die u eerder hebt geïnstalleerd. Op ons systeem hebben we versie 8 geïnstalleerd.
   
    ![][7]
6. Geef op de volgende pagina Hallo Hallo Tomcat-installatiedirectory. Op een Windows-computer is dit waarschijnlijk C:\Program Files\Apache Software Foundation\Tomcat *versie*.
7. Klik op **Voltooien**.
8. Selecteer **Window** (Venster) > **Preferences** (Voorkeuren) > **Java** > **Installed JREs**(Geïnstalleerde JRE's) > **Add** (Toevoegen).
9. Selecteer in het venster **Add JRE** (JRE toevoegen) de optie **Standard VM** (Standaard-VM).
10. Klik op **Volgende**.
11. Klik in JRE Definition (JRE-definitie), in JRE home (JRE-startpagina), op **Directory**.
12. Navigeer te**Program Files** > **Java** en selecteer Hallo JDK die u eerder hebt geïnstalleerd. Het is belangrijk tooselect hello JDK als Hallo JRE.
13. Kies in de geïnstalleerd JREs hello **JDK**. Uw instellingen ziet vergelijkbare toohello volgende schermopname.
    
    ![][9]
14. Selecteer desgewenst **venster** > **webbrowser** > **Internet Explorer** tooopen Hallo toepassing in een extern browservenster. Het gebruik van de externe browser biedt een betere gebruikservaring voor de webtoepassing.
    
    ![][8]

U hebt nu Hallo configuratietaken voltooid. U moet vervolgens bouwen en uitvoeren van Hallo-project.

## <a name="build-hello-project"></a>Hallo-project maken
1. In Projectverkenner met de rechtermuisknop op de projectnaam Hallo en kies **uitvoeren als** > **Maven build...**  tooconfigure Hallo project.
   
    ![][10]
2. Ga naar Edit Configuration (Configuratie bewerken), typ bij Goals (Doelen) 'clean install' en klik vervolgens op **Run** (Uitvoeren).

Statusberichten die zijn uitvoer toohello-consolevenster. U ziet BUILD SUCCESS die duiden Hallo project zonder fouten is gebouwd.

## <a name="run-hello-app"></a>Hallo-app uitvoeren
In deze laatste stap wordt u Hallo toepassing uitvoert in een lokale server runtime-omgeving.

Als u dit nog niet hebt nog geen serverruntime-omgeving in Eclipse opgegeven, moet u dat eerst toodo.

1. Vouw in Projectverkenner **WebContent** uit.
2. Klik met de rechtermuisknop op **Search.jsp** > **Run As** (Uitvoeren als) > **Run on Server** (Uitvoeren op server). Selecteer Hallo Apache Tomcat-server en klik vervolgens op **uitvoeren**.

> [!TIP]
> Als u een niet-standaard werkruimte toostore op uw project gebruikt, moet u toomodify **Run configuratie** toopoint toohello project locatie tooavoid een opstartfout voor de server. Klik in Projectverkenner met de rechtermuisknop op **Search.jsp** > **Uitvoeren als** > **Configuratie uitvoeren**. Selecteer Hallo Apache Tomcat-server. Klik op **Argumenten**. Klik op **werkruimte** of **bestandssysteem** tooset Hallo map met de Hallo-project.
> 
> 

Wanneer u de toepassing hello uitvoert, ziet u een browservenster biedt een zoekvak waarin u termen.

Wacht ongeveer een minuut voordat u op **Search** toogive Hallo service tijd toocreate en load Hallo index. Als u een HTTP 404-fout krijgt, hoeft u alleen toowait iets langer voordat u opnieuw probeert.

## <a name="search-on-usgs-data"></a>Zoeken in USGS-gegevens
Hallo USGS-gegevensset bevat records die relevant toohello staat Rhode Island. Als u op **Search** op het zoekvak leeg is, ontvangt u een Hallo bovenste 50 vermeldingen, Hallo standaardinstelling.

Een zoekterm invoert, krijgt Hallo zoekmachine iets toogo op. Voer een regionale naam in. 'Roger Williams' was Hallo eerste gouverneur van Rhode Island. Er zijn verschillende parken, gebouwen en scholen naar hem vernoemd.

![][11]

U kunt ook de volgende termen proberen:

* Pawtucket
* Pembroke
* goose +cape

## <a name="next-steps"></a>Volgende stappen
Dit is Hallo eerste Azure Search-zelfstudie op basis van Java en Hallo USGS-gegevensset. Na verloop van tijd hebt we deze zelfstudie toodemonstrate aanvullende zoekfuncties kunt u toouse in uw aangepaste oplossingen uitbreiden.

Als u al enige ervaring in Azure Search hebt, kunt u dit voorbeeld als Springplank voor verdere experimenten, om Hallo [zoekpagina](search-pagination-page-layout.md), of implementeren van een [facetnavigatie](search-faceted-navigation.md). U kunt ook op Hallo pagina met zoekresultaten verbeteren door tellers toe te voegen document in batch zodat gebruikers kunnen via Hallo resultaten.

Nieuwe tooAzure zoeken? Het is raadzaam om bij andere zelfstudies toodevelop een goed begrip van kunt maken. Ga naar onze [documentatiepagina](https://azure.microsoft.com/documentation/services/search/) toofind meer bronnen. U kunt ook weergeven Hallo koppelingen in onze [Video's en zelfstudies lijst](search-video-demo-tutorial-list.md) tooaccess meer informatie.

<!--Image references-->
[1]: ./media/search-get-started-java/create-search-portal-1.PNG
[2]: ./media/search-get-started-java/create-search-portal-21.PNG
[3]: ./media/search-get-started-java/create-search-portal-31.PNG
[4]: ./media/search-get-started-java/AzSearch-Java-Import1.PNG
[5]: ./media/search-get-started-java/AzSearch-Java-config1.PNG
[6]: ./media/search-get-started-java/AzSearch-Java-ProjectFacets1.PNG
[7]: ./media/search-get-started-java/AzSearch-Java-runtime1.PNG
[8]: ./media/search-get-started-java/AzSearch-Java-Browser1.PNG
[9]: ./media/search-get-started-java/AzSearch-Java-JREPref1.PNG
[10]: ./media/search-get-started-java/AzSearch-Java-BuildProject1.PNG
[11]: ./media/search-get-started-java/rogerwilliamsschool1.PNG
[12]: ./media/search-get-started-java/AzSearch-Java-SelectProject.png
