---
title: Azure Role-eigenschappen
description: Informatie over het gebruik van de Azure-Toolkit voor Eclipse om Azure-functie-instellingen te configureren.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5c0ec412-5702-465a-8f47-87a8ce99a267
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: cd734c64ba6d1394cb261bace92dee9dd579dd08
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-role-properties"></a>Azure Role-eigenschappen
Verschillende configuratie-instellingen voor uw Azure-rol kunnen worden ingesteld binnen de Azure-werkset voor Eclipse.

## <a name="configuring-azure-role-properties"></a>Eigenschappen van de Azure-functie configureren
De eigenschappen van uw Azure-functie configureren wordt via de eigenschap dialoogvensters voor uw werkrol gerealiseerd. Open het contextmenu voor de rol in de Eclipse-Project Explorer-venster en selecteer de **Azure** vervolgmenu. (Als u de rol in de Projectverkenner Eclipse niet ziet, vouwt u uw Azure-project in Projectverkenner.)

![][ic789599]

De diverse eigenschappen die kunnen worden ingesteld vanuit de **eigenschappen** dialoogvensters worden beschreven in dit onderwerp. Houd er rekening mee dat veel eigenschappen worden automatisch ingevuld bij het maken van een nieuw project in de Azure-implementatie.

De volgende eigenschappenpagina's zijn beschikbaar voor Azure-functies.

* [Eigenschappen van virtuele machine](#virtual_machine_properties)
* [Eigenschappen opslaan in cache](#caching_properties)
* [Eigenschappen van certificaten](#certificates_properties)
* [Eigenschappen van onderdelen](#components_properties)
<!-- * [Debugging properties](#debugging_properties) -->
* [Eigenschappen van de eindpunten](#endpoints_properties)
* [Variabelen omgevingseigenschappen](#environment_variables_properties)
* [Taakverdeling / sessie affiniteit (ook wel 'een tijdelijke sessies')-eigenschappen](#session_affinity_properties)
* [Eigenschappen van lokale opslag](#local_storage_properties)
* [Configuratie-eigenschappen van server](#server_configuration_properties)
* [SSL-offloading eigenschappen](#ssl_offloading_properties)

<a name="virtual_machine_properties"></a>

### <a name="virtual-machine-properties"></a>Eigenschappen van virtuele machine
Open het contextmenu voor de rol in het deelvenster van de Eclipse Projectverkenner, klik op **Azure**, en klik vervolgens op **eigenschappen**, en u hebt de mogelijkheid om de grootte van de virtuele machine te wijzigen en het nummer ook wijzigen van exemplaren, zoals wordt weergegeven in de volgende afbeelding.

![][ic719499]

> [!NOTE]
> Alleen Windows: als u het aantal exemplaren op een waarde groter dan 1 en u ook een toepassingsserver configureren, kunt de toolkit slechts 1 rolexemplaar in de emulator, ongeacht deze instelling uit te voeren. Dit is de poort binding om conflicten te voorkomen tussen de exemplaren van de andere server (bijvoorbeeld alle probeert te binden aan poort 8080) wanneer ze op dezelfde computer worden uitgevoerd. De instelling voor uw exemplaar van het gewenste aantal wordt bewaard, maar wordt ingevoerd alleen wanneer u naar de cloud implementeert.
> 
> 

<a name="caching_properties"></a> 

### <a name="caching-properties"></a>Eigenschappen opslaan in cache
Open het contextmenu voor de rol in het deelvenster van de Eclipse Projectverkenner, klik op **Azure**, en klik vervolgens op **opslaan in cache**. In dit dialoogvenster kunt u met de naam CO-locaties memcache-compatibele caches inschakelen zodat u sneller webtoepassingen te.

![][ic719483]

Binnen de **opslaan in cache** eigenschappenpagina, kunt u algemene instellingen voor het volgende opgeven:

* Hiermee wordt aangegeven of CO-locaties opslaan in cache is ingeschakeld.
* de grootte van de cache als een percentage van het geheugen.
* naam van het opslagaccount voor het opslaan van de status van de cache wanneer uw toepassing wordt uitgevoerd als een cloudservice of none als u niet wilt dat de status van de cache opslaan. (Naam van het opslagaccount wordt niet gebruikt wanneer u uw toepassing in de rekenemulator uitvoeren.) Als u de naam van het opslagaccount ingesteld op **(automatisch)** (dit is de standaardwaarde), de configuratie van de cache automatisch gebruikmaken van hetzelfde opslagaccount als het account dat u selecteert in de **publiceren naar Azure** dialoogvenster.

> [!NOTE]
> De **(automatisch)** instelling heeft het gewenste effect alleen als u uw implementatie met de Eclipse-toolkit publiceren wizard publiceren. Als u in plaats daarvan het publiceren van het .cspkg-bestand met een externe methode, handmatig, zoals de [Azure Management Portal][Azure Management Portal], de implementatie niet goed.
> 
> 

Het volgende dialoogvenster ziet u de eigenschappen voor een cache.

![][ic719501]

* **Naam:** de naam van de cache geplaatst.
* **Poortnummer:** het poortnummer dat moet worden gebruikt voor de cache.
* **Verloopbeleid:** een van de volgende waarden die aangeeft wanneer een sleutel in de cache verloopt.
  * **Absolute:** is verlopen wanneer de tijd die is opgegeven door de sleutel **minuten live** is bereikt.
  * **NeverExpires:** de sleutel heeft geen een verlooptijd.
  * **SlidingWindow:** de sleutel verloopt als deze niet is geopend voor de hoeveelheid tijd die is opgegeven door **minuten live**; elke keer dat deze wordt geopend, de vervaldatum klok wordt opnieuw ingesteld.
* **Minuten live:** het maximale aantal minuten een memcached-sleutel voor live onderworpen aan het verloopbeleid.
* **Hoge beschikbaarheid met gerepliceerde back-ups voor andere rolinstanties:** als ingeschakeld, zorgt voor hoge beschikbaarheid met behulp van back-ups op andere rolinstanties gerepliceerd. Houd er rekening mee dat ten minste twee rolexemplaren van kracht voor uw implementatie voor deze functie zijn moeten te gebruiken.

Klik op als u een nieuwe cache de **toevoegen** knop in de **opslaan in cache** eigenschappenpagina, en een **configureren met de naam Cache** dialoogvenster wordt geopend. Geef waarden op voor de eigenschappen die hierboven zijn beschreven.

Voor het wijzigen van een benoemde cache, selecteert u de cache en klikt u op de **bewerken** knop in de **opslaan in cache** eigenschappenpagina. Een dialoogvenster wordt geopend zodat u de eigenschappen van de cache. Druk op **OK** de cachewaarden op te slaan.

Verwijder een cache, selecteert u de cache te klikken en de **verwijderen** knop in de **opslaan in cache** eigenschappenpagina en klik vervolgens op **Ja** om de verwijdering te bevestigen.

Zie voor meer informatie over het gebruik van caching [hoe gebruiken Co-located Caching][How to Use Co-located Caching].

<a name="certificates_properties"></a> 

### <a name="certificates-properties"></a>Eigenschappen van certificaten
Open het contextmenu voor de rol in het deelvenster van de Eclipse Projectverkenner, klik op **Azure**, en klik vervolgens op **certificaten**.

![][ic710964]

In dit dialoogvenster kunt u toevoegen of verwijderen van de certificaten waarnaar wordt verwezen door uw Eclipse-project. Houd er rekening mee dat de certificaten die hier niet automatisch in een Java-sleutelopslag opgeslagen worden en daarom niet automatisch beschikbaar voor gebruik van binnen een Java-toepassing zijn. Ze zijn alleen geregistreerd met Azure zodat ze vooraf kunnen worden geladen in de Windows certificaat opslaan op de virtuele machines waarop uw implementatie wordt uitgevoerd en vervolgens worden gebruikt door andere Windows-software. Op dit moment de enige functie van de toolkit die gebruikmaakt van de certificaten waarnaar wordt verwezen in deze manier de **certificaten** dialoogvenster is [SSL-Offloading][SSL Offloading], vanwege de afhankelijkheid van Internet Information Services (IIS) en Application Request Routing (ARR), waarvoor het juiste certificaat beschikbaar op deze manier wordt gemaakt.

Wanneer u uw project in Azure maken met de wizard Publiceren implementeert, wordt u gevraagd om te verwijzen naar de de Personal Information Exchange (PFX)-bestanden die overeenkomt met deze certificaten, samen met hun wachtwoorden om automatisch te uploaden naar de Azure-service , maar alleen als ze zijn niet geüpload er eerder.

<a name="components_properties"></a> 

### <a name="components-properties"></a>Eigenschappen van onderdelen
Open het contextmenu voor de rol in het deelvenster van de Eclipse Projectverkenner, klik op **Azure**, en klik vervolgens op **onderdelen**. U hebt de mogelijkheid om te toevoegen, wijzigen, of de onderdelen van uw rol verwijderen, evenals de volgorde waarin ze worden verwerkt wijzigen binnen dit dialoogvenster.

![][ic719502]

De functie onderdelen kunt u afhankelijkheden toevoegen aan uw project Azure-implementatie, zoals Java-toepassing projecten, speciale bestanden en uitvoerbare opdrachtregel-instructies die nodig zijn voor uw implementatie.

Voor elk onderdeel, kunt u het volgende opgeven:

* De stap moeten worden genomen bij het importeren van het onderdeel in uw Azure-implementatie-project wanneer ze is opgebouwd.
* De stap moeten worden genomen bij het implementeren van dit onderdeel in de Azure-cloud.

> [!NOTE]
> Wanneer u opgeeft onderdeelbestanden of opdrachtregels, houd er rekening mee dat uw implementatie wordt gepubliceerd naar een virtuele Windows-computer, zodat uw aangepaste stappen geldig zijn voor een besturingssysteem op basis van Windows moet. 
> 
> 

Onderdelen van hebben de volgende eigenschappen:

* **-Import:** methode waarmee wordt aangegeven hoe het onderdeel worden geïmporteerd in het project wanneer het project is gebouwd. Dit kan een van de volgende waarden zijn:
  * **exemplaar:** het onderdeel wordt opgehaald uit het lokale pad dat is opgegeven door de **van** eigenschap aan de rol **approot** directory.
  * **WISSEN:** het onderdeel is een Java enterprise-archief (wissen) geïmporteerd uit een Enterprise-toepassingsproject in het lokale pad dat is opgegeven door de **van** eigenschap. (Dit wordt automatisch gedetecteerd door de toolkit op basis van de aard van het project op die locatie).
  * **JAR:** het onderdeel is van een Java-archief (JAR) en wordt geïmporteerd uit een Java-project in het lokale pad dat is opgegeven door de **van** eigenschap. (Dit wordt automatisch gedetecteerd door de toolkit op basis van de aard van het project op die locatie).
  * **geen:** geen actie is ondernomen voor het importeren van het onderdeel. Dit is van toepassing wanneer het onderdeel wordt ervan uitgegaan dat al aanwezig in de rol **approot** directory, of wanneer het onderdeel is slechts een instructie van het uitvoerbare bestand vanaf de opdrachtregel, zoals opgegeven in de **als** eigenschap wanneer de **implementeren** methode is **exec**.
  * **WAR:** het onderdeel is van een Java web application-archief (WAR) en wordt geïmporteerd uit een dynamisch webproject in het lokale pad dat is opgegeven door de **van** eigenschap. (Dit wordt automatisch gedetecteerd door de toolkit op basis van de aard van het project op die locatie).
  * **ZIP:** het onderdeel is van een zip-bestand en wordt geïmporteerd door het comprimeren van de map of bestand dat is opgegeven door de **van** eigenschap.
* **Van:** bronpad op uw lokale computer naar de map of bestand dat staat voor de items te importeren voor uw implementatie. Windows-omgevingsvariabelen kunnen worden gebruikt in deze eigenschap. Alle importeerbare onderdelen worden geïmporteerd in de rol **approot** directory wanneer het project is gebouwd.
  
    Houd er rekening mee dat u de mogelijkheid hebt tot het implementeren van een onderdeel van een download bij het implementeren van de cloud (niet de rekenemulator). Zie Verwante informatie hieronder over het toevoegen van een onderdeel.    
* **Net als:** bestandsnaam waaronder het onderdeel worden geïmporteerd in de rol **approot** directory en uiteindelijk geïmplementeerd in de Azure-cloud. Deze eigenschap wilt niets behouden de naam omdat deze zich op de lokale computer. (Voor uitvoerbare onderdelen, dat wil zeggen, deze waarvan **implementeren** methode is ingesteld op **exec**, dit kan een willekeurige Windows-opdrachtregel-instructie zijn.)
  
  > [!IMPORTANT]
  > Als u spaties voor deze waarde gebruikt, wordt ze anders afgehandeld, afhankelijk van de methode implementeren. Als de methode implementeren **exec**, spaties, wordt geïnterpreteerd als scheidingstekens voor de opdrachtregel-argumenten en niet als onderdeel van de bestandsnaam. Implementeren voor alle andere methoden, spaties, wordt geïnterpreteerd als onderdeel van de bestandsnaam.
  > 
  > 
* **Implementeren:** methode waarmee wordt aangegeven welke actie op het onderdeel moet worden toegepast wanneer de implementatie wordt gestart. Dit kan een van de volgende waarden zijn:
  
  * **exemplaar:** het onderdeel wordt gekopieerd naar het doelpad dat is opgegeven door de **naar** eigenschap.
  * **exec:** het onderdeel is een uitvoerbare Windows-opdrachtregel instructie uitgevoerd in de context van het pad dat is opgegeven door de **naar** -eigenschap op het moment dat de implementatie start.
  * **geen:** geen actie op het onderdeel wordt toegepast wanneer de implementatie start.
  * **ZIP:** het onderdeel is uitgepakt naar het doelpad dat is opgegeven door de **naar** eigenschap. Deze methode is alleen beschikbaar wanneer de **importeren** eigenschap is **zip**.
* **Naar:** doelpad op de virtuele machine waarop het onderdeel wordt geïmplementeerd. Windows-omgevingsvariabelen kunnen worden gebruikt in deze eigenschap en bestandspaden zijn relatief **approot**.

Als u wilt een nieuw onderdeel toevoegen, klikt u op de **toevoegen** knop in de **onderdelen** eigenschappenpagina, en een **Azure rol onderdeel** dialoogvenster wordt geopend. Geef waarden op voor de eigenschappen die hierboven zijn beschreven. 

Hieronder ziet u een voorbeeld voor het toevoegen van een nieuwe WAR-component.

![][ic719503]

Wanneer implementeren naar de cloud (niet de rekenemulator), als u wilt implementeren van het onderdeel van een download ervoor te zorgen dat **implementeren in de cloud, in plaats van in het pakket, inclusief vanaf** is ingeschakeld. Als u downloaden van uw Azure storage-account wilt, selecteert u het opslagaccount van de **opslagaccount** vervolgkeuzelijst (u kunt klikken op de **Accounts** koppeling om te wijzigen wat is er in de lijst), die wordt gedeeltelijk Vul de **URL** veld en vult u het resterende deel van de URL. Als u niet gebruiken van Azure storage wilt, selecteert u **(geen)** van de **opslagaccount** vervolgkeuzelijst lijst en voer de URL naar uw onderdeel in de **URL** veld. Geef een van de volgende methoden:

* **exemplaar:** het onderdeel downloaden wordt gekopieerd naar het doelpad dat is opgegeven door de **To Directory** pad.
* **dezelfde:** dezelfde methode gebruikt voor **implementeren van downloaden** als voor **distribueren van pakket**.
* **ZIP:** het onderdeel downloaden is uitgepakt naar het doelpad dat is opgegeven door de **To Directory** pad.

Selecteer het onderdeel voor het wijzigen van een onderdeel, en klik op de **bewerken** knop in de **onderdelen** eigenschappenpagina. Een dialoogvenster wordt geopend zodat u de onderdeeleigenschappen wijzigen. Druk op **OK** de onderdeelwaarden op te slaan.

Selecteer het onderdeel voor het verwijderen van een onderdeel, en klik op de **verwijderen** knop in de **onderdelen** eigenschappenpagina en klik vervolgens op **Ja** om de verwijdering te bevestigen.

Onderdelen worden verwerkt in de volgorde weergegeven. Gebruik de **omhoog** en **omlaag** knoppen om de volgorde te bepalen.

> [!NOTE]
> De functie server configuratie afhankelijk van de onderdelen ook. Deze onderdelen kunnen worden verwijderd of gewijzigd zonder de bijbehorende serverconfiguratie worden verwijderd. U wordt gevraagd over die bij een poging om deze onderdelen te wijzigen.
> 
> 

<!-- <a name="debugging_properties"></a> -->

<!-- ### Debugging properties -->
<!-- Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **Debugging**. Within this dialog, you have the ability to enable or disable remote debugging, as well as create debug configurations, as shown in the following image. -->

<!-- ![][ic719504] -->

<!-- For related information about debugging, see [Debugging Azure Applications in Eclipse][Debugging Azure Applications in Eclipse]. -->

<a name="endpoints_properties"></a> 

### <a name="endpoints-properties"></a>Eigenschappen van de eindpunten
Open het contextmenu voor de rol in het deelvenster van de Eclipse Projectverkenner, klik op **Azure**, en klik vervolgens op **eindpunten**. In dit dialoogvenster hebt u de mogelijkheid een eindpunt worden gemaakt, evenals bewerken of verwijderen van een eindpunt, zoals wordt weergegeven in de volgende afbeelding.

![][ic719505]

Als u wilt een eindpunt toevoegen, klikt u op de **toevoegen** knop in de **eindpunten** eigenschappenpagina, en een **eindpunt toevoegen** dialoogvenster wordt geopend.

![][ic710897]

Geef een naam voor het eindpunt, selecteer het type (ofwel **invoer**, **intern**, of **InstanceInput**), en de openbare en particuliere poort opgeven. Druk op **OK** het nieuwe eindpunt waarden op te slaan.

Afhankelijk van het type eindpunt, kunt u poortbereiken als volgt gebruiken:

* De openbare poort is voor een eindpunt invoer exemplaar een poortbereik (bijvoorbeeld **2000 2010**) en de particuliere poort is een vaste waarde.
* Voor een interne eindpunt, kan de openbare poort wordt niet gebruikt, en de particuliere poort een bereik, of u leeg of is ingesteld op een sterretje om aan te geven dat deze automatisch door Azure is ingesteld.
* Voor invoereindpunten, een vaste waarde kan alleen worden door de openbare poort en de particuliere poort kan een vaste waarde, of u leeg of is ingesteld als een sterretje om aan te geven dat wordt automatisch ingesteld door Azure.

Als u een enkele poortnummer gebruiken in plaats van een bereik wilt, laat u het tekstvak voor het einde van het bereik leeg.

Voor de poorten die zijn ingesteld op automatisch, als u nodig hebt om te bepalen welke poort daadwerkelijk wordt gebruikt tijdens runtime, toepassingen kunnen gebruikmaken van de Azure Service Runtime API, die wordt beschreven in de [com.microsoft.windowsazure.serviceruntime pakket samenvatting ][com.microsoft.windowsazure.serviceruntime package summary].

<!-- To see how instance input endpoints can be used to help with debugging a multi-instance deployment, see [Debugging a specific role instance in a multi-instance deployment][Debugging a specific role instance in a multi-instance deployment]. -->

Selecteer het eindpunt voor het wijzigen van een eindpunt en klik op de **bewerken** knop in de **eindpunten** eigenschappenpagina. Een dialoogvenster wordt geopend zodat u de naam van het eindpunt, type en openbare en particuliere poort wijzigen. Druk op **OK** de gewijzigde endpoint-waarden op te slaan.

Verwijder een eindpunt, selecteer het eindpunt te klikken en de **verwijderen** knop in de **eindpunten** eigenschappenpagina en klik vervolgens op **Ja** om de verwijdering te bevestigen.

Om correcte configuratie van enkele van de functies (zoals Caching, sessie affiniteit of SSL-offloading) door de gebruiker op een rol is ingeschakeld, kan de toolkit automatisch speciale eindpunten die u samen met de gebruiker gedefinieerde eindpunten configureren. De toolkit wordt voorkomen dat de gebruiker bewerken of eindpunten verwijderen van deze automatisch worden gegenereerd als de bijbehorende functie is ingeschakeld.

<a name="environment_variables_properties"></a> 

### <a name="environment-variables-properties"></a>Variabelen omgevingseigenschappen
Open het contextmenu voor de rol in het deelvenster van de Eclipse Projectverkenner, klik op **Azure**, en klik vervolgens op **omgevingsvariabelen**. In dit dialoogvenster hebt u de mogelijkheid een omgevingsvariabele maakt, evenals wijzigen of verwijderen van een omgevingsvariabele betreft, zoals wordt weergegeven in de volgende afbeelding.

![][ic719506]

Omgevingsvariabelen zijn beschikbaar voor uw opstartscript wanneer de functie wordt gestart.

> [!NOTE]
> Houd er rekening mee dat uw implementatie wordt gepubliceerd naar een virtuele Windows-computer, zodat de omgevingsvariabelen geldig zijn voor een Windows-besturingssysteem moet bij het opgeven van omgevingsvariabelen.
> 
> 

Als een voorbeeld van een omgevingsvariabele wordt beschikbaar wanneer de functie wordt gestart, kunt u een nieuwe omgevingsvariabele maken door te klikken op de **toevoegen** knop. Hieronder vindt u een omgevingsvariabele **MyRoleVersion** wordt gemaakt en de waarde aan toegewezen **1.0**.

![][ic659268]

Binnen uw jsp-code, kunt u weergeven de waarde met behulp van de `System.getenv` methode:

    <body>
      <b> Hello World!</b>
      <p>Running role version: <%= System.getenv("MyRoleVersion") %></p>
    </body>

Waardoor deze uitvoer wanneer uw toepassing wordt uitgevoerd:

![][ic552233]

Selecteer de omgevingsvariabele voor het wijzigen van een omgevingsvariabele, en klik op de **bewerken** knop in de **omgevingsvariabelen** eigenschappenpagina. Een dialoogvenster wordt geopend zodat u de omgeving variabele eigenschappen wijzigen. Druk op **OK** om op te slaan van de omgeving de waarden van variabelen.

Als u wilt verwijderen van een omgevingsvariabele, selecteer de omgevingsvariabele en klik op de **verwijderen** knop in de **omgevingsvariabelen** eigenschappenpagina en klik vervolgens op **Ja** naar Bevestig de verwijdering.

Om correcte configuratie van enkele van de functies (zoals serverconfiguratie foutopsporing op afstand of de lokale opslag) ingeschakeld door de gebruiker op een rol, de toolkit automatisch speciale omgevingsvariabelen die wordt weergegeven naast de gebruiker gedefinieerde mogelijk configureren omgevingsvariabelen. De toolkit wordt voorkomen dat de gebruiker bewerken of verwijderen van deze automatisch gegenereerd omgevingsvariabelen, zolang de bijbehorende functie is ingeschakeld.

<a name="session_affinity_properties"></a> 

### <a name="load-balancing--session-affinity-aka-sticky-sessions-properties"></a>Taakverdeling / sessie affiniteit (ook wel 'een tijdelijke sessies')-eigenschappen
Open het contextmenu voor de rol in het deelvenster van de Eclipse Projectverkenner, klik op **Azure**, en klik vervolgens op **Load Balancing**. In dit dialoogvenster hebt u de mogelijkheid-of uitschakelen van affiniteit van de sessie, zoals wordt weergegeven in de volgende afbeelding.

![][ic719492]

Zie voor meer informatie kunt [sessie affiniteit][Session Affinity]. Let ook op deze functie gedrag in de context van het SSL-offloading, zoals beschreven op [SSL-Offloading][SSL Offloading].

<a name="local_storage_properties"></a> 

### <a name="local-storage-properties"></a>Eigenschappen van lokale opslag
Open het contextmenu voor de rol in het deelvenster van de Eclipse Projectverkenner, klik op **Azure**, en klik vervolgens op **lokale opslag**. In dit dialoogvenster hebt u de mogelijkheid om te maken, wijzigen of verwijderen van tijdelijke lokale opslag voor de virtuele machine die uw toepassing wordt uitgevoerd. Specifieke waarden kunnen worden ingesteld voor de grootte van de lokale opslag, en geeft aan of de inhoud behouden blijven wanneer de functie wordt gerecycled, zoals wordt weergegeven in de volgende afbeelding.

![][ic719508]

U kunt eventueel ook een omgevingsvariabele die overeenkomt met de lokale opslag opgeven.

Standaard alles wat u in Azure implementeert geplaatst (en zijn uitgepakt) in de **approot** map van de rolinstantie. Terwijl de meeste implementaties van eenvoudige past er zelfs na het ritsen, de ruimte toegewezen voor de **approot** directory is beperkt en niet goed gedefinieerde (minder dan 1 GB is een redelijke vuistregel). Toewijst daarom om ervoor te zorgen Azure voldoende schijfruimte beschikbaar voor grotere implementaties die niet passen mogelijk in de **approot** map, moet u instellen een lokale opslag resource met de **lokale opslag** dialoogvenster. Zie voor een eenvoudige manier om dit te doen, [grote implementaties implementeren][Deploying Large Deployments].

U kunt eenvoudig verwijzen naar de opslagbronnen van opstartscripts (bijvoorbeeld uw **startup.cmd**) met behulp van de omgevingsvariabele automatisch door de Eclipse-toolkit zijn gekoppeld aan de resource, zoals wordt weergegeven in de  **Lokale opslag** dialoogvenster. Deze omgevingsvariabele bevat het volledige pad van de lokale resource die u hebt geconfigureerd op het moment dat het opstartscript wordt uitgevoerd. 

Voor het wijzigen van een resource voor lokale opslag, selecteer de bron van de lokale opslag en klik op de **bewerken** knop in de **lokale opslag** eigenschappenpagina. Een dialoogvenster wordt geopend zodat u de eigenschappen van lokale opslag resource wijzigen. Druk op **OK** de waarden van de resource lokale opslag op te slaan.

Als u wilt verwijderen van een resource voor lokale opslag, selecteer de bron van de lokale opslag en klik op de **verwijderen** knop in de **lokale opslag** eigenschappenpagina en klik vervolgens op **Ja** om te bevestigen de verwijdering.

<a name="server_configuration_properties"></a> 

### <a name="server-configuration-properties"></a>Configuratie-eigenschappen van server
Open het contextmenu voor de rol in het deelvenster van de Eclipse Projectverkenner, klik op **Azure**, en klik vervolgens op **serverconfiguratie**. In dit dialoogvenster de mogelijkheid wilt toevoegen, verwijderen en wijzigen van de JDK en Java-toepassingsserver die wordt gebruikt door uw implementatie hebt u evenals toevoegen of verwijderen van de toepassingen (zoals WAR, JAR of OOR-bestanden) die door uw implementatie.

### <a name="jdk-configuration"></a>JDK-configuratie
Dit dialoogvenster kunt u de JDK-pakket moet worden gebruikt voor uw implementatie op te geven. Als u Eclipse op Windows gebruikt, kunt u het pakket JDK naar lokaal gebruiken bij het uitvoeren in de Azure-emulator en hebt u de optie die lokale installatie implementeren naar Azure. De emulator JDK-instelling is niet van toepassing op niet-Windows-besturingssystemen en het lokaal geïnstalleerde JDK kan niet worden geïmplementeerd omdat deze niet compatibel met Windows. Echter, ongeacht het besturingssysteem die u gebruikt, u kunt altijd kiezen uit de 3e partij JDK pakketten om te implementeren naar Azure of op uw eigen Windows-compatibele JDK-pakket van het rapportageservicepunt vanuit een alternatieve locatie.

Hier volgt een voorbeeld van hoe u een JDK in Windows kunt opgeven:

![][ic780647]

Als u Eclipse op Windows gebruikt, kunt u een JDK voor gebruik met de rekenemulator; om dit te doen, zorg ervoor dat **de JDK die van dit bestandspad gebruiken om lokaal te testen** is ingeschakeld de **Emulator implementatie** sectie. Geef het lokale pad naar uw JDK; u kunt bladeren naar andere JDK als degene die u wilt gebruiken, wordt niet automatisch geselecteerd. U hebt ook de optie voor het implementeren van uw JDK met uw Azure-cloud-service; om dit te doen, selecteert u de **mijn lokale JDK (automatische-uploaden naar de cloudopslag) implementeren** optie in de **Cloud implementatie** sectie.

Opmerking: op niet-Windows-besturingssystemen, de **Emulator implementatie** instellingen en de **implementeren mijn lokale JDK** optie zijn niet beschikbaar. Het volgende voorbeeld ziet u het opgeven van een JDK op een Mac- of andere ondersteund niet-Windows-besturingssysteem:

![][ic789643]

Ongeacht het besturingssysteem dat u zich bevindt, hebt u de volgende twee **Cloud implementatie** opties voor de bron en het type van uw pakket JDK:

* **Een beschikbaar is op Azure 3e partij JDK pakket implementeren** 
* **Implementeren vanaf een aangepast downloaden** 

Als u de **implementeren van een beschikbaar is via Azure 3e partij JDK pakket** optie:

1. Schakel het selectievakje in met de naam **implementeren van een beschikbaar is via Azure 3e partij JDK pakket**.
2. Selecteer het pakket met 3e partij JDK die beschikbaar is in Azure uit de vervolgkeuzelijst.
3. Uw **JDK** tabblad ziet er ongeveer als volgt in Windows: ![][ic780648] en deze ziet er ongeveer als volgt op de Mac OS of andere niet-Windows-besturingssystemen ondersteund:![][ic789643]
4. Klik op **OK** om uw wijzigingen op te slaan.
5. Wanneer u wordt gevraagd om te accepteren van de gebruiksrechtovereenkomst van de 3e JDK Pakketprovider, lees de licentievoorwaarden. Ervan uitgaande dat u de voorwaarden accepteren klikt u op **Ja** sluiten de **gebruiksrechtovereenkomst** dialoogvenster.
    Let op de onderliggende logica voor welke items worden weergegeven in de vervolgkeuzelijst voor de **implementeren van een beschikbaar is via Azure 3e partij JDK pakket** optie kan worden aangepast. Voor het aanpassen van de items in de **JDK** dialoogvenster, klikt u op de **aanpassen** koppeling. Hiermee sluit u de **JDK** eigenschappenpagina en open de **componentsets.xml** bestand in Eclipse, die u kunt zo nodig wijzigen. Documentatie voor **componentsets.xml** is opgenomen in de **componentsets.xml** -bestand zelf.

Als u de **implementeren van een JDK van downloaden van een aangepaste** optie:

1. Maak een ZIP van de installatiemap van JDK, zorgt u ervoor dat de directory-knooppunt zelf is het onderliggende element van het ZIP-structuur en niet de inhoud ervan. Noteer de naam van de map en als u deze later nodig en houd er rekening mee dat deze installatie JDK wordt geïmplementeerd op een virtuele Windows-computer.
2. Upload het ZIP-bestand naar uw Azure storage-account als een blob. U kunt doen dit met een extern beschikbare hulpprogramma voor uploaden naar Azure storage-blobs. Het verdient aanbeveling gebruik van een persoonlijke blob. Let op de blob-URL van het ZIP-inhoud.
3. Schakel het selectievakje in met de naam **implementeren van een JDK van downloaden van een aangepaste**.
    Als u downloaden van uw Azure storage-account wilt, selecteert u het opslagaccount van de **opslagaccount** vervolgkeuzelijst (u kunt klikken op de **Accounts** koppeling om te wijzigen wat is er in de lijst), die wordt gedeeltelijk Vul de **URL** veld en vult u het resterende deel van de URL. Als u niet gebruiken van Azure storage wilt, selecteert u **(geen)** van de **opslagaccount** vervolgkeuzelijst lijst en voer de URL naar uw download JDK in de **URL** veld. Als u Azure-opslag gebruikt, zijn blob-namen in de URL in kleine letters.
4. Zorg ervoor dat de **JAVA_HOME** textbox verwijst naar de naam van de juiste map. Standaard wordt verwezen naar de naam van de dezelfde JDK map als de waarde die u hebt gekozen voor uw lokale gebruik. Maar als de map in het ZIP-bestand heeft een andere naam (bijvoorbeeld door middel van een andere versie) bijwerken van de naam van de map in de **JAVA_HOME** dienovereenkomstig textbox sinds deze instelling wordt in de cloud worden gebruikt (niet in de rekenemulator).
5. Klik op **OK** om uw wijzigingen op te slaan.

Dat is alles. Nu, als u voor de cloud bouwen, zult u grootte van het pakket is veel kleiner, het buildproces duurt meestal minder tijd en de implementatie zelf wanneer u naar de cloud publiceert moet ook rekening houden met minder tijd. Houd er rekening mee dat de **mijn lokale JDK (automatische-uploaden naar de cloudopslag) implementeren** of **implementeren van een JDK van downloaden van een aangepaste** opties zijn alleen van kracht wanneer uw toepassing wordt geïmplementeerd in de cloud. Ze hebben geen invloed op uw ervaring van de compute-emulator; de lokale versie van de onderdelen wordt nog steeds worden gebruikt wanneer u in de rekenemulator implementeert. 

### <a name="server-configuration"></a>Serverconfiguratie
Hier volgt een voorbeeld van hoe u een toepassingsserver kunt opgeven.

![][ic796926]

Controleer de **implementeren van een server van dit type** selectievakje is ingeschakeld en kies vervolgens het type van de toepassingsserver die u wilt gebruiken.

Voor het opgeven van een server wilt gebruiken voor de implementatie van cloud, kunt u profiteren van de volgende opties:

1. **Een 3e partij-server beschikbaar zijn in Azure implementeren** -dit is vooral van toepassing in ontwikkelen en testen scenario's waarbij implementatie efficiëntie en eenvoud een prioriteit en de server is niet vereist voor een aangepaste configuratie. Of als u wilt een van deze servers als uitgangspunt te gebruiken, maar u bevatten aanpassing van de juiste server in uw implementatie opstartlogica stappen.
2. **Implementeren vanaf het downloaden van een aangepaste** -dit is vooral van toepassing in productiescenario's wanneer er een speciaal voorbereid en geconfigureerde server die u wilt gebruiken in de cloud.
3. **De installatie van de lokale server implementeren** -dit is vooral van toepassing in als de installatie van de lokale server al aangepaste geconfigureerd voor gebruik is. Als u deze optie kiest, moet u ook opgeven van de lokale server pad in de **pad naar de lokale server** onderstaande tekstvak.

Als u de **3e partij-server implementeren in Azure beschikbaar** optie:

1. Schakel het selectievakje in met de naam **3e partij-server implementeren in Azure beschikbaar**.
2. Selecteer de gewenste server-software voor gebruik met uw implementatie in de cloud in de vervolgkeuzelijst. Opmerking: als u al een type van server naar het eerder opgegeven, kunt u zich beperkt tot het kiezen van een cloud-server die zich in de familie van dat servertype. Maar als u geen servertype hebt gekozen, kunt u kiezen uit een van de servers die momenteel beschikbaar op Azure zijn en het servertype wordt automatisch voor u geselecteerd.
3. Klik op **OK** om uw wijzigingen op te slaan.

Als de **implementeren van een aangepaste download** optie:

1. Zorg ervoor dat u al een servertype volgens de voorgaande stappen hebt geselecteerd. Dit vertelt de invoegtoepassing voor het implementeren van de server van uw aangepaste downloaden, zoals het moet uit dezelfde familie als uw type geselecteerde server.
2. Schakel het selectievakje in met de naam **implementeren van een aangepaste download**.
    Als u downloaden van uw Azure storage-account wilt, selecteert u het opslagaccount van de **opslagaccount** vervolgkeuzelijst (u kunt klikken op de **Accounts** koppeling om te wijzigen wat is er in de lijst), die wordt gedeeltelijk Vul de **URL** veld en vult u het resterende deel van de URL van uw server ZIP downloaden (wanneer met behulp van Azure-opslag, blob-namen in de URL een kleine letter moet). Als u niet gebruiken van Azure storage wilt, selecteert u **(geen)** van de **opslagaccount** vervolgkeuzelijst, en voert u de URL naar uw server in het ZIP downloaden de **URL** veld. Het ZIP-bestand bevat een onderliggende map voor de installatiemap van uw toepassing-server. Bijvoorbeeld, als u van een zip voor Apache Tomcat 7.0.35 gebruikmaakt, binnen het ZIP-bestand zou zijn de onderliggende map voor de map wilt installeren, zoals **apache-tomcat-7.0.35**. 
3. Geef de waarde voor de basismap-omgevingsvariabele. De standaardinstelling is de waarde die voor uw lokale toepassingsserver, indien van toepassing, maar u kunt een andere waarde opgeven als de cloud-toepassingsserver af van uw lokale toepassingsserver wijkt. Echter, moet u ervoor zorgen dat uw cloud-toepassingsserver uit dezelfde familie als de server is type eerder hebt geselecteerd.
    Als u uw postcode cloud application server in de toekomst bijwerkt, kunt u handmatig de instelling voor de basismap, wijzigen of om deze opnieuw overeenkomen met uw lokale instelling (als u uw lokale toepassingsserver te gewijzigd).
4. Klik op **OK** om uw wijzigingen op te slaan.

De onderliggende logica waarvoor items worden weergegeven in de **Server** tabblad van de **serverconfiguratie** eigenschappenpagina kan worden aangepast. Dit is een geavanceerde functie die u wellicht als uw behoeften buiten de standaardwaarden uitbreiden of als u wilt toevoegen, andere servers. Voor het aanpassen van de logica de **Server** dialoogvenster, klikt u op de **aanpassen** koppeling. Hiermee sluit u de **serverconfiguratie** eigenschappenpagina en open de **componentsets.xml** bestand in Eclipse, die u naar behoefte uitbreiden van de server configuratiesjabloon vervolgens kunt wijzigen. Documentatie voor **componentsets.xml** is opgenomen in de **componentsets.xml** -bestand zelf.

Als u de **mijn lokale server (automatische-uploaden naar de cloudopslag) implementeren** optie:

1. Schakel het selectievakje in met de naam **mijn lokale server (automatische-uploaden naar de cloudopslag) implementeren**.
2. Met behulp van de **opslagaccount** vervolgkeuzelijst, selecteer **(automatisch)**. Als u opgeeft **(automatisch)** hier de Eclipse-toolkit hetzelfde opslagaccount wordt gebruikt voor uw server als het account dat u hebt geselecteerd voor uw implementatie in de **publiceren naar Azure** dialoogvenster.
3. Klik op **OK** om uw wijzigingen op te slaan.

Selecteer een installatiepad voor de server op uw computer in de **pad naar de lokale server** tekstvak als een van de volgende voorwaarden voldaan wordt:

* Wilt u uw implementatie testen in de emulator (alleen van toepassing op Windows).
* Wilt u uw lokaal geïnstalleerde server implementeren in de cloud.
* U wilt downloaden van uw eigen in de cloud, waarin de aanvraag door een aangepaste server gebruiken, zorg er ook voor de **mijn lokale server (automatische-uploaden naar de cloudopslag) implementeren** hierboven is ingeschakeld.

Als geen van de opties hierboven van toepassing op uw situatie, is de instelling van de lokale server is optioneel.

### <a name="applications-configuration"></a>Configuratie van de toepassing
Hier volgt een voorbeeld van hoe u een toepassing kunt opgeven.

![][ic719512]

Klik op **toevoegen** toevoegen van een andere toepassing of **verwijderen** om een toepassing te verwijderen. Voor efficiëntie doeleinden, als u een download voor de bron van een toepassing gebruiken wilt bij het implementeren van de cloud, gebruik de [onderdelen eigenschappen](#components_properties) om op te geven van een URL, storage-account, enzovoort. 

Vanaf de release van April 2014, worden de toepassingen automatisch geüpload in hetzelfde opslagaccount (onder de **eclipsedeploy** container) als het account dat is geselecteerd voor uw implementatie. Het starten van de logica van uw implementatie bevat een stap die u downloadt eerst deze toepassingen uit dat opslagaccount. Dit betekent dat u uw toepassingen in uw implementatie kan upgraden zonder opnieuw maken en implementeren van het volledige pakket door handmatig uploaden nieuwere versies van de toepassing rechtstreeks in dit opslagaccount (met behulp van de Azure-portal bijvoorbeeld), vervangen van de bestanden WAR oorspronkelijk geüpload er door de toolkit. Vervolgens net start het recyclen van alle die rolinstanties met behulp van de Azure-beheerportal opnieuw, of via de opdrachtregel-hulpprogramma's. (Rollen recyclen rechtstreeks vanuit binnen de Eclipse-toolkit activerende is momenteel niet ondersteund.)

### <a name="notes-about-server-configuration"></a>Opmerkingen over de serverconfiguratie van de
Wijzigingen die zijn aangebracht via de **serverconfiguratie** eigenschappenpagina worden doorgevoerd in de `<component>` elementen van het bestand Package.xml heeft.

Wanneer u gebruikt de **automatisch uploaden...**  of **implementeren niet worden gedownload...**  opties voor de JDK of toepassingsserver en u wilt maken voor de cloud (niet de rekenemulator), en u bent verbonden met het netwerk, merkt u berichten, zoals het volgende in de Console-uitvoer bouwen als de opbouwfunctie voor het Ant wordt gecontroleerd de download beschikbaarheid:

`[windowsazurepackage] Verifying blob availability (https://example.blob.core.windows.net/temp/tomcat6.zip)...` 

Als u hebt geselecteerd de **implementeren niet worden gedownload...**  optie, worden mogelijk de volgende waarschuwing weergegeven, maar de build gaat verder:

`[windowsazurepackage] warning: Failed to confirm blob availability! Make sure the URL and/or the access key is correct (https://example.blob.core.windows.net/temp/tomcat6.zip).` 

Deze waarschuwing is de enige indicatie dat de beschikbaarheid van de download niet is gecontroleerd. Dus als een implementatie is in de cloud voor een bepaalde reden mislukt, controleert u of u deze waarschuwing ontvangen.

Als u wilt de controle downloaden (bijvoorbeeld als u denkt dat dit onnodig de build vertraagt) niet uitschakelen, stelt u de `verifydownloads` kenmerk `false` in de `<windowsazurepackage>` element van Package.xml heeft: 

`<windowsazurepackage verifydownloads="false" ...>` 

Als u hebt geselecteerd de **automatisch uploaden...**  optie, klikt u vervolgens in het consolevenster u ziet bouwen berichten rapportage van de voortgang van het uploaden van elke vijf seconden telkens wanneer een upload nodig is.

<a name="ssl_offloading_properties"></a> 

### <a name="ssl-offloading-properties"></a>SSL-offloading eigenschappen
Open het contextmenu voor de rol in het deelvenster van de Eclipse Projectverkenner, klik op **Azure**, en klik vervolgens op **SSL-Offloading**. 

![][ic719481]

In dit dialoogvenster kunt u SSL-offloading, zodat u eenvoudig Hypertext Transfer Protocol Secure (HTTPS)-ondersteuning inschakelen in uw implementatie Java in Azure, zonder dat u SSL configureren op uw Java-toepassingsserver. Zie voor meer informatie [SSL-Offloading] [ SSL Offloading] en [hoe gebruik SSL-Offloading][How to Use SSL Offloading].

## <a name="see-also"></a>Zie ook
[Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]

[De installatie van de Azure Toolkit voor Eclipse][Installing the Azure Toolkit for Eclipse]

[Maken van een Hallo wereld-toepassing voor Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Eigenschappen van de Azure-Project][Azure Project Properties]

[Lijst met Azure Storage-Account][Azure Storage Account List]

Zie voor meer informatie over het gebruik van Azure met Java de [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Project Properties]: http://go.microsoft.com/fwlink/?LinkID=699524
[Azure Storage Account List]: http://go.microsoft.com/fwlink/?LinkID=699528
[com.microsoft.windowsazure.serviceruntime package summary]: http://azure.github.io/azure-sdk-for-java/com/microsoft/windowsazure/serviceruntime/package-summary.html
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Debugging a specific role instance in a multi-instance deployment]: http://go.microsoft.com/fwlink/?LinkID=699535#debugging_specific_role_instance
[Debugging Azure Applications in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699535
[Deploying Large Deployments]: http://go.microsoft.com/fwlink/?LinkID=699536
[How to Use Co-located Caching]: http://go.microsoft.com/fwlink/?LinkID=699542
[How to Use SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699545
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699548
[SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699549

<!-- IMG List -->

[ic789599]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789599.png
[ic719499]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719499.png
[ic719483]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719483.png
[ic719501]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719501.png
[ic710964]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic710964.png
[ic719502]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719502.png
[ic719503]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719503.png
[ic719504]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719504.png
[ic719505]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719505.png
[ic710897]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic710897.png
[ic719506]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719506.png
[ic659268]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic659268.png
[ic552233]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic552233.png
[ic719492]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719492.png
[ic719508]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719508.png
[ic780647]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic780647.png
[ic789643]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789643.png
[ic780648]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic780648.png
[ic789643]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789643.png
[ic796926]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic796926.png
[ic719512]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719512.png
[ic719481]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719481.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690945.aspx -->
