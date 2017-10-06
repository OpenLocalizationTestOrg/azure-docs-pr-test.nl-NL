---
title: aaaAzure Role-eigenschappen
description: Meer informatie over hoe toouse Azure Toolkit Hallo voor Eclipse tooconfigure Azure serverfunctie-instellingen.
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
ms.openlocfilehash: d111b4b9e4f12e49f38755bf6c9acc1a1de17a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-properties"></a>Azure Role-eigenschappen
Verschillende configuratie-instellingen voor uw Azure-rol kunnen worden ingesteld binnen hello Azure Toolkit voor Eclipse.

## <a name="configuring-azure-role-properties"></a>Eigenschappen van de Azure-functie configureren
Configureren van de eigenschappen van uw Azure-rol wordt uitgevoerd via Hallo eigenschap dialoogvensters voor uw werkrol. Open Hallo contextmenu voor Hallo-rol in de Projectverkenner deelvenster en selecteer Hallo van Eclipse **Azure** vervolgmenu. (Als er geen Hallo-rol in Eclipse Projectverkenner hello, vouwt u uw Azure-project in Projectverkenner.)

![][ic789599]

diverse eigenschappen die kunnen worden ingesteld van Hallo Hallo **eigenschappen** dialoogvensters worden beschreven in dit onderwerp. Houd er rekening mee dat veel eigenschappen worden automatisch ingevuld bij het maken van een nieuw project in de Azure-implementatie.

Hallo na eigenschappenpagina's zijn beschikbaar voor Azure-functies.

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
Hallo contextmenu voor Hallo rol in Eclipse van Projectverkenner deelvenster openen, klikt u op **Azure**, en klik vervolgens op **eigenschappen**, en u Hallo mogelijkheid toochange Hallo de grootte van virtuele machine, en ook wijzigen Hallo aantal exemplaren, zoals wordt weergegeven in Hallo installatiekopie te volgen.

![][ic719499]

> [!NOTE]
> Alleen Windows: wanneer u het aantal exemplaren Hallo tooa waarde groter is dan 1 instellen en u ook een toepassingsserver configureren, Hallo toolkit slechts 1 rol exemplaar toorun in Hallo-emulator, ongeacht deze instelling wordt toestaan. Dit is tooavoid poort bindingsconflicten tussen verschillende serverexemplaren hello (bijvoorbeeld alle poging toobind tooport 8080) wanneer ze worden uitgevoerd op Hallo dezelfde computer. De instelling voor uw exemplaar van het gewenste aantal wordt bewaard, maar wordt ingevoerd alleen wanneer u toohello cloud implementeert.
> 
> 

<a name="caching_properties"></a> 

### <a name="caching-properties"></a>Eigenschappen opslaan in cache
Hallo contextmenu voor Hallo rol in Eclipse van Projectverkenner deelvenster openen, klikt u op **Azure**, en klik vervolgens op **opslaan in cache**. In dit dialoogvenster kunt u met de naam CO-locaties memcache-compatibele caches inschakelen zodat u toohelp snelheid van uw webtoepassingen.

![][ic719483]

Binnen Hallo **opslaan in cache** eigenschappenpagina, kunt u algemene instellingen voor hello te volgen:

* Hiermee wordt aangegeven of CO-locaties opslaan in cache is ingeschakeld.
* Hallo cachegrootte als een percentage van het geheugen.
* Hallo opslagaccountnaam voor het opslaan van Hallo cache staat wanneer uw toepassing wordt uitgevoerd als een cloudservice of none als u niet dat toosave Hallo cache staat wilt. (Hallo opslagaccountnaam wordt niet gebruikt wanneer u uw toepassing in Hallo rekenemulator uitvoeren.) Als u instelt dat de opslagaccountnaam hello te**(automatisch)** (dit is de standaardwaarde Hallo), automatisch gebruikmaken van de configuratie van uw cache in hetzelfde opslagaccount hello, zoals een u in Hallo selecteert Hallo **publiceren tooAzure**dialoogvenster.

> [!NOTE]
> Hallo **(automatisch)** instelling heeft Hallo gewenst effect alleen als u uw implementatie met Hallo Eclipse toolkit publiceren wizard publiceren. Als u in plaats daarvan het publiceren van Hallo .cspkg bestand handmatig met een externe methode, zoals Hallo [Azure Management Portal][Azure Management Portal], Hallo-implementatie niet goed.
> 
> 

Hallo volgende dialoogvenster ziet Hallo-eigenschappen voor een cache.

![][ic719501]

* **Naam:** Hallo-naam van Hallo cache CO-locaties.
* **Poortnummer:** Hallo poort nummer toouse voor Hallo-cache.
* **Verloopbeleid:** een Hallo waarden te volgen die aangeeft wanneer een sleutel in Hallo cache verloopt.
  * **Absolute:** Hallo sleutel verloopt wanneer Hallo tijd die is opgegeven door **minuten toolive** is bereikt.
  * **NeverExpires:** Hallo sleutel heeft geen een verlooptijd.
  * **SlidingWindow:** Hallo sleutel verloopt als deze niet is geopend voor de hoeveelheid tijd die is opgegeven door Hallo **minuten toolive**; elke keer dat deze wordt geopend, Hallo verlopen klok wordt opnieuw ingesteld.
* **Minuten toolive:** het maximale aantal minuten voor een sleutel memcached toolive, toohello, vervaldatumbeleid onderwerpnaam.
* **Hoge beschikbaarheid met gerepliceerde back-ups voor andere rolinstanties:** als ingeschakeld, zorgt voor hoge beschikbaarheid met behulp van back-ups op andere rolinstanties gerepliceerd. Houd er rekening mee dat ten minste twee rolexemplaren van kracht voor uw implementatie voor deze functie toowork moeten zijn.

een nieuwe cache tooadd klikt u op Hallo **toevoegen** knop in Hallo **opslaan in cache** eigenschappenpagina, en een **configureren met de naam Cache** dialoogvenster wordt geopend. Geef waarden op voor het Hallo-eigenschappen die hierboven zijn beschreven.

een benoemde cache toomodify Hallo cache selecteren en klik op Hallo **bewerken** knop in Hallo **opslaan in cache** eigenschappenpagina. Een dialoogvenster wordt geopend zodat u toomodify Hallo cache eigenschappen. Druk op **OK** toosave Hallo cachewaarden.

een cache toodelete Hallo cache selecteren en klik op Hallo **verwijderen** knop in Hallo **opslaan in cache** eigenschappenpagina en klik vervolgens op **Ja** tooconfirm Hallo verwijderen.

Voor meer informatie over het toouse caching, Zie [hoe tooUse CO-locaties opslaan in cache][How tooUse Co-located Caching].

<a name="certificates_properties"></a> 

### <a name="certificates-properties"></a>Eigenschappen van certificaten
Hallo contextmenu voor Hallo rol in Eclipse van Projectverkenner deelvenster openen, klikt u op **Azure**, en klik vervolgens op **certificaten**.

![][ic710964]

In dit dialoogvenster kunt u toevoegen of verwijderen van de certificaten waarnaar wordt verwezen door uw Eclipse-project. Houd er rekening mee dat Hallo certificaten hier vermeld niet automatisch in een Java-sleutelopslag opgeslagen worden en daarom niet automatisch beschikbaar voor gebruik van binnen een Java-toepassing zijn. Ze zijn alleen geregistreerd met Azure zodat ze vooraf kunnen worden geladen in Hallo Windows certificaat opslaan op Hallo virtuele machines waarop uw implementatie wordt uitgevoerd en vervolgens worden gebruikt door andere Windows-software. Op dit moment Hallo alleen functie van Hallo toolkit die gebruikmaakt van Hallo certificaten waarnaar wordt verwezen in Hallo op deze manier **certificaten** dialoogvenster is [SSL-Offloading][SSL Offloading], vanwege tooits de afhankelijkheid van Internet Information Services (IIS) en Application Request Routing (ARR), waarvoor Hallo juiste certificaat toobe beschikbaar op deze manier gemaakt.

Wanneer u uw project tooAzure met behulp van de wizard Publiceren Hallo implementeert, kunt u zich na vragen aan gebruiker toopoint op Hallo Personal Information Exchange (PFX) overeenkomen toothese certificaten, samen met hun wachtwoorden, in volgorde tooautomatically uploaden toohello Azure-service, maar alleen als ze zijn niet geüpload er eerder.

<a name="components_properties"></a> 

### <a name="components-properties"></a>Eigenschappen van onderdelen
Hallo contextmenu voor Hallo rol in Eclipse van Projectverkenner deelvenster openen, klikt u op **Azure**, en klik vervolgens op **onderdelen**. In dit dialoogvenster u Hallo mogelijkheid tooadd hebben, wijzigen, of Hallo onderdelen van uw rol verwijderen, evenals Hallo volgorde waarin ze worden verwerkt wijzigen.

![][ic719502]

Hallo onderdelen functie kunt u tooadd afhankelijkheden tooyour Azure implementatieproject, zoals Java-toepassing projecten, speciale bestanden en uitvoerbare opdrachtregel-instructies die nodig zijn voor uw implementatie.

Voor elk onderdeel, kunt u het volgende opgeven:

* Hallo stap toobe genomen bij het importeren van hello onderdeel in uw Azure-implementatie-project wanneer ze is opgebouwd.
* Hallo stap toobe genomen bij het implementeren van dit onderdeel in hello Azure-cloud.

> [!NOTE]
> Wanneer u opgeeft onderdeelbestanden of opdrachtregels, houd er rekening mee dat uw implementatie wordt gepubliceerde tooa virtuele Windows-computer, zodat uw aangepaste stappen geldig zijn voor een Windows-besturingssysteem moet. 
> 
> 

Onderdelen hebben Hallo volgende eigenschappen:

* **-Import:** methode die hoe Hallo onderdeel worden geïmporteerd in Hallo project aangeeft wanneer Hallo project is gebouwd. Dit kan een van de volgende waarden Hallo zijn:
  * **exemplaar:** Hallo-component wordt opgehaald uit Hallo lokale pad dat is opgegeven door Hallo **van** eigenschap in het Hallo-rol **approot** directory.
  * **WISSEN:** Hallo onderdeel is een Java enterprise-archief (wissen) geïmporteerd uit een Enterprise-toepassingsproject op Hallo lokaal pad opgegeven door Hallo **van** eigenschap. (Dit wordt automatisch gedetecteerd door Hallo toolkit op basis van Hallo aard van Hallo-project op die locatie).
  * **JAR:** Hallo onderdeel is van een Java-archief (JAR) en wordt geïmporteerd uit een Java-project op Hallo lokaal pad opgegeven door Hallo **van** eigenschap. (Dit wordt automatisch gedetecteerd door Hallo toolkit op basis van Hallo aard van Hallo-project op die locatie).
  * **geen:** tooimport Hallo onderdeel er geen actie ondernomen. Dit is van toepassing wanneer het Hallo-onderdeel wordt van uitgegaan tooalready aanwezig zijn in Hallo-rol **approot** directory, of wanneer Hallo-component is slechts een overzicht van het uitvoerbare vanaf de opdrachtregel, als opgegeven in de Hallo **als**eigenschap bij hello **implementeren** methode is **exec**.
  * **WAR:** Hallo onderdeel is van een Java web application-archief (WAR) en wordt geïmporteerd uit een dynamisch webproject op Hallo lokaal pad opgegeven door Hallo **van** eigenschap. (Dit wordt automatisch gedetecteerd door Hallo toolkit op basis van Hallo aard van Hallo-project op die locatie).
  * **ZIP:** Hallo onderdeel is van een zip-bestand en zijn geïmporteerd door de comprimeren Hallo directory of bestand dat is opgegeven door Hallo **van** eigenschap.
* **Van:** bronpad op uw lokale machine toohello map of het bestand dat Hallo items tooimport tooyour implementatie vertegenwoordigt. Windows-omgevingsvariabelen kunnen worden gebruikt in deze eigenschap. Alle importeerbare onderdelen worden geïmporteerd in het Hallo-rol **approot** map bevindt wanneer Hallo project is gebouwd.
  
    Houd er rekening mee dat u Hallo mogelijkheid toodeploy een onderdeel van een download hebt bij het implementeren van toohello cloud (niet-rekenemulator Hallo). Zie Verwante informatie hieronder over het toevoegen van een onderdeel.    
* **Net als:** bestandsnaam onder welke Hallo onderdeel worden geïmporteerd in het Hallo-rol **approot** directory en uiteindelijk geïmplementeerde in hello Azure-cloud. Laat deze leeg tookeep eigenschap Hallo naam Hallo dezelfde manier als op de lokale machine Hallo is. (Voor uitvoerbare onderdelen, dat wil zeggen, deze waarvan **implementeren** methode te is ingesteld**exec**, dit kan een willekeurige Windows-opdrachtregel-instructie zijn.)
  
  > [!IMPORTANT]
  > Als u voor deze waarde spaties, ze worden verwerkt verschillend, afhankelijk van Hallo methode implementeren. Als Hallo methode implementeert is **exec**, spaties, wordt geïnterpreteerd als scheidingstekens voor de opdrachtregel-argumenten en niet als onderdeel van het Hallo-bestandsnaam. Implementeren voor alle andere methoden, spaties, wordt geïnterpreteerd als onderdeel van het Hallo-bestandsnaam.
  > 
  > 
* **Implementeren:** methode die Hallo actie geeft toohello onderdeel toegepast wanneer het Hallo-implementatie is gestart. Dit kan een van de volgende waarden Hallo zijn:
  
  * **exemplaar:** Hallo onderdeel is gekopieerde toohello doelpad is opgegeven door Hallo **naar** eigenschap.
  * **exec:** Hallo onderdeel is een uitvoerbare Windows-opdrachtregel instructie uitgevoerd in context van Hallo pad is opgegeven door Hallo Hallo **naar** eigenschap gelijktijdig Hallo Hallo implementatie start.
  * **geen:** is geen actie toegepaste toohello onderdeel wanneer Hallo-implementatie wordt gestart.
  * **ZIP:** Hallo onderdeel is uitgepakt toohello doelpad is opgegeven door Hallo **naar** eigenschap. Deze methode is alleen beschikbaar wanneer hello **importeren** eigenschap is **zip**.
* **Naar:** doelpad op Hallo virtuele machine waarop Hallo-component wordt geïmplementeerd. Windows-omgevingsvariabelen kunnen worden gebruikt in deze eigenschap en bestandspaden zijn relatieve te**approot**.

een nieuw onderdeel tooadd klikt u op Hallo **toevoegen** knop in Hallo **onderdelen** eigenschappenpagina, en een **Azure rol onderdeel** dialoogvenster wordt geopend. Geef waarden op voor het Hallo-eigenschappen die hierboven zijn beschreven. 

Hallo hieronder toont een voorbeeld voor het toevoegen van een nieuwe WAR-component.

![][ic719503]

Wanneer het implementeren van toohello cloud (geen Hallo compute-emulator) als u wilt dat toodeploy Hallo onderdeel van een download ervoor te zorgen dat **implementeren in de cloud, in plaats van in Hallo pakket, inclusief vanaf** is ingeschakeld. Als u toodownload van uw Azure storage-account, selecteert u Hallo storage-account van Hallo **Storage-account** vervolgkeuzelijst (u kunt klikken op Hallo **Accounts** koppelen toomodify wat is er in de lijst Hallo), die gedeeltelijk hello wordt ingevuld **URL** veld en vul vervolgens de resterende deel van de URL Hallo Hallo. Als u niet dat toouse Azure-opslag wilt, selecteert u **(geen)** van Hallo **opslagaccount** vervolgkeuzelijst, en voert u Hallo URL tooyour onderdeel in Hallo **URL** veld. Geef een van de volgende methoden Hallo:

* **exemplaar:** Hallo downloaden onderdeel is gekopieerde toohello doelpad is opgegeven door Hallo **tooDirectory** pad.
* **dezelfde:** Hallo dezelfde methode gebruikt voor **implementeren van downloaden** als voor **distribueren van pakket**.
* **ZIP:** Hallo downloaden onderdeel is uitgepakt toohello doelpad is opgegeven door Hallo **tooDirectory** pad.

een onderdeel, selecteer Hallo-onderdeel en klikt u op Hallo toomodify **bewerken** knop in Hallo **onderdelen** eigenschappenpagina. Een dialoogvenster wordt geopend zodat u toomodify Hallo eigenschappen van onderdeel. Druk op **OK** toosave Hallo onderdeelwaarden.

een onderdeel, selecteer Hallo-onderdeel en klikt u op Hallo toodelete **verwijderen** knop in Hallo **onderdelen** eigenschappenpagina en klik vervolgens op **Ja** tooconfirm Hallo verwijderen.

Onderdelen worden in volgorde van Hallo verwerkt. Gebruik Hallo **omhoog** en **omlaag** tooarrange Hallo volgorde knoppen.

> [!NOTE]
> Hallo-serverfunctie configuratie afhankelijk van de onderdelen ook. Deze onderdelen kunnen worden verwijderd of gewijzigd zonder de bijbehorende serverconfiguratie Hallo worden verwijderd. U wordt gevraagd over die tijdens een poging de toomake wijzigingen toosuch onderdelen.
> 
> 

<!-- <a name="debugging_properties"></a> -->

<!-- ### Debugging properties -->
<!-- Open hello context menu for hello role in Eclipse's Project Explorer pane, click **Azure**, and then click **Debugging**. Within this dialog, you have hello ability tooenable or disable remote debugging, as well as create debug configurations, as shown in hello following image. -->

<!-- ![][ic719504] -->

<!-- For related information about debugging, see [Debugging Azure Applications in Eclipse][Debugging Azure Applications in Eclipse]. -->

<a name="endpoints_properties"></a> 

### <a name="endpoints-properties"></a>Eigenschappen van de eindpunten
Hallo contextmenu voor Hallo rol in Eclipse van Projectverkenner deelvenster openen, klikt u op **Azure**, en klik vervolgens op **eindpunten**. In dit dialoogvenster u hebt Hallo mogelijkheid toocreate een eindpunt evenals bewerken of verwijderen van een eindpunt zoals weergegeven in Hallo installatiekopie te volgen.

![][ic719505]

tooadd een eindpunt, klikt u op Hallo **toevoegen** knop in Hallo **eindpunten** eigenschappenpagina, en een **eindpunt toevoegen** dialoogvenster wordt geopend.

![][ic710897]

Geef een naam voor het Hallo-eindpunt, Hallo-type selecteren (ofwel **invoer**, **intern**, of **InstanceInput**), en Hallo openbare en particuliere poort opgeven. Druk op **OK** toosave Hallo nieuwe waarden van het eindpunt.

Afhankelijk van Hallo type eindpunt, kunt u poortbereiken als volgt gebruiken:

* Hallo openbare poort is voor een eindpunt invoer exemplaar een poortbereik (bijvoorbeeld **2000 2010**) en particuliere poort Hallo is een vaste waarde.
* Voor een interne eindpunt kan Hallo openbare poort wordt niet gebruikt, en particuliere poort Hallo een bereik, of leeg worden gelaten of set tooan sterretje tooindicate die wordt automatisch ingesteld door Azure.
* Hallo openbare poort kan alleen worden voor een vaste waarde voor invoereindpunten, en particuliere poort Hallo mag een vaste waarde, of leeg worden gelaten of set tooan sterretje tooindicate die wordt automatisch ingesteld door Azure.

Als u toouse een enkele poortnummer in plaats van een bereik wilt, in het tekstvak voor Hallo einde van Hallo bereik Hallo leeg laten.

Voor de poorten die ingesteld tooautomatic, zijn als u nodig hebt toodetermine welke poort daadwerkelijk wordt gebruikt tijdens runtime, kunt uw toepassing hello Azure Service Runtime API, die wordt beschreven in Hallo [com.microsoft.windowsazure.serviceruntime-pakket Samenvatting][com.microsoft.windowsazure.serviceruntime package summary].

<!-- toosee how instance input endpoints can be used toohelp with debugging a multi-instance deployment, see [Debugging a specific role instance in a multi-instance deployment][Debugging a specific role instance in a multi-instance deployment]. -->

toomodify een eindpunt, selecteer Hallo eindpunt en klikt u op Hallo **bewerken** knop in Hallo **eindpunten** eigenschappenpagina. Een dialoogvenster wordt geopend zodat u toomodify Hallo eindpuntnaam, type en openbare en particuliere poort. Druk op **OK** toosave Hallo eindpunt waarden gewijzigd.

toodelete een eindpunt, selecteer Hallo eindpunt en klikt u op Hallo **verwijderen** knop in Hallo **eindpunten** eigenschappenpagina en klik vervolgens op **Ja** tooconfirm Hallo verwijderen.

In de volgorde tooproperly configureren aantal Hallo functies (zoals Caching, sessie affiniteit of SSL-offloading) ingeschakeld door de gebruiker op een rol hello, Hallo toolkit mogelijk automatisch speciale eindpunten die u samen met de gebruiker gedefinieerde eindpunten configureren. Hallo toolkit verhindert dat Hallo-gebruiker bewerken of verwijderen van dergelijke automatisch gegenereerde eindpunten, zolang Hallo gekoppeld functie is ingeschakeld.

<a name="environment_variables_properties"></a> 

### <a name="environment-variables-properties"></a>Variabelen omgevingseigenschappen
Hallo contextmenu voor Hallo rol in Eclipse van Projectverkenner deelvenster openen, klikt u op **Azure**, en klik vervolgens op **omgevingsvariabelen**. In dit dialoogvenster u Hallo mogelijkheid toocreate een omgevingsvariabele hebt, evenals wijzigen of verwijderen van een omgevingsvariabele zoals weergegeven in Hallo installatiekopie te volgen.

![][ic719506]

Omgevingsvariabelen zijn beschikbaar tooyour opstartscript wanneer Hallo-rol wordt gestart.

> [!NOTE]
> Houd er rekening mee dat uw implementatie wordt gepubliceerde tooa virtuele Windows-computer, zodat de omgevingsvariabelen geldig zijn voor een besturingssysteem op basis van Windows moet bij het opgeven van omgevingsvariabelen.
> 
> 

Als een voorbeeld van een omgevingsvariabele wordt beschikbaar wanneer Hallo-rol wordt gestart, kunt u een nieuwe omgevingsvariabele maken door te klikken op Hallo **toevoegen** knop. Hallo hieronder vindt u een omgevingsvariabele **MyRoleVersion** wordt gemaakt en toegewezen Hallo waarde **1.0**.

![][ic659268]

Binnen uw code jsp Hallo-waarde met behulp van Hallo kan worden weergegeven `System.getenv` methode:

    <body>
      <b> Hello World!</b>
      <p>Running role version: <%= System.getenv("MyRoleVersion") %></p>
    </body>

Waardoor deze uitvoer wanneer uw toepassing wordt uitgevoerd:

![][ic552233]

een omgevingsvariabele toomodify Hallo omgevingsvariabele selecteren en klik op Hallo **bewerken** knop in Hallo **omgevingsvariabelen** eigenschappenpagina. Een dialoogvenster wordt geopend zodat u toomodify Hallo omgeving variabele eigenschappen. Druk op **OK** toosave Hallo omgeving de waarden van variabelen.

een omgevingsvariabele toodelete Hallo omgevingsvariabele selecteren en klik op Hallo **verwijderen** knop in Hallo **omgevingsvariabelen** eigenschappenpagina en klik vervolgens op **Ja**tooconfirm Hallo verwijderen.

In de volgorde tooproperly configureren aantal Hallo functies (zoals serverconfiguratie foutopsporing op afstand of de lokale opslag) ingeschakeld door de gebruiker Hallo op een rol, het Hallo toolkit mogelijk automatisch configureren voor speciale omgevingsvariabelen die wordt weergegeven samen met gebruiker gedefinieerde omgevingsvariabelen. Hallo toolkit verhindert dat Hallo-gebruiker bewerken of verwijderen van deze automatisch gegenereerde omgevingsvariabelen zolang Hallo gekoppeld functie is ingeschakeld.

<a name="session_affinity_properties"></a> 

### <a name="load-balancing--session-affinity-aka-sticky-sessions-properties"></a>Taakverdeling / sessie affiniteit (ook wel 'een tijdelijke sessies')-eigenschappen
Hallo contextmenu voor Hallo rol in Eclipse van Projectverkenner deelvenster openen, klikt u op **Azure**, en klik vervolgens op **Load Balancing**. In dit dialoogvenster hebt Hallo mogelijkheid tooenable of uitschakelen affiniteit van de sessie, zoals wordt weergegeven in Hallo installatiekopie te volgen.

![][ic719492]

Zie voor meer informatie kunt [sessie affiniteit][Session Affinity]. Let ook op deze functie gedrag in Hallo context van het SSL-offloading, zoals beschreven op [SSL-Offloading][SSL Offloading].

<a name="local_storage_properties"></a> 

### <a name="local-storage-properties"></a>Eigenschappen van lokale opslag
Hallo contextmenu voor Hallo rol in Eclipse van Projectverkenner deelvenster openen, klikt u op **Azure**, en klik vervolgens op **lokale opslag**. In dit dialoogvenster Hallo mogelijkheid toocreate hebt u, wijzigen of verwijderen van tijdelijke lokale opslag voor Hallo virtuele machine die uw toepassing wordt uitgevoerd. Specifieke waarden kunnen worden ingesteld voor Hallo grootte van de lokale opslag hello, evenals of Hallo inhoud blijven behouden wanneer Hallo-rol wordt gerecycled, zoals wordt weergegeven in Hallo installatiekopie te volgen.

![][ic719508]

U kunt eventueel ook een omgevingsvariabele die overeenkomt met de lokale opslag toohello opgeven.

Standaard alles wat u in Azure implementeert geplaatst (en zijn uitgepakt) in Hallo **approot** map van de rolinstantie Hallo. Terwijl de meeste implementaties van eenvoudige past er zelfs na het ritsen, Hallo toegewezen ruimte voor Hallo **approot** directory is beperkt en niet goed gedefinieerde (minder dan 1 GB is een redelijke vuistregel). Daarom tooensure Azure voldoende schijfruimte toewijst voor grotere implementaties die mogelijk niet in het Hallo passen **approot** map, u moet een lokale opslagresource instellen met behulp van Hallo **lokale opslag** het dialoogvenster. Voor een eenvoudige manier toodo deze, Zie [grote implementaties implementeren][Deploying Large Deployments].

U kunt eenvoudig verwijzen naar opslagresource Hallo van opstartscripts (bijvoorbeeld uw **startup.cmd**) met Hallo omgevingsvariabele automatisch gekoppeld door Hallo Eclipse toolkit Hallo resource, zoals in Hallo  **Lokale opslag** dialoogvenster. Deze omgevingsvariabele bevat volledige pad op Hallo van Hallo lokale resource die u hebt geconfigureerd op Hallo moment die uw opstartscript wordt uitgevoerd. 

toomodify een resource lokale opslag, selecteer Hallo lokale opslagresource en op Hallo **bewerken** knop in Hallo **lokale opslag** eigenschappenpagina. Een dialoogvenster wordt geopend zodat u toomodify Hallo lokale opslag broneigenschappen. Druk op **OK** toosave Hallo waarden voor lokale opslag van resources.

toodelete een resource lokale opslag, selecteer Hallo lokale opslagresource en op Hallo **verwijderen** knop in Hallo **lokale opslag** eigenschappenpagina en klik vervolgens op **Ja** tooconfirm hello verwijderen.

<a name="server_configuration_properties"></a> 

### <a name="server-configuration-properties"></a>Configuratie-eigenschappen van server
Hallo contextmenu voor Hallo rol in Eclipse van Projectverkenner deelvenster openen, klikt u op **Azure**, en klik vervolgens op **serverconfiguratie**. In dit dialoogvenster hebt u de mogelijkheid tooadd hello, verwijderen, en Hallo JDK en Java-toepassingsserver, die wordt gebruikt door uw implementatie wijzigen evenals toepassingen toevoegen of verwijderen hello (zoals WAR, JAR of OOR-bestanden) die wordt gebruikt door uw implementatie.

### <a name="jdk-configuration"></a>JDK-configuratie
Dit dialoogvenster kunt u toospecify hello JDK pakket toouse voor uw implementatie. Als u Eclipse op Windows gebruikt, kunt u Hallo JDK pakket toouse lokaal wanneer uitgevoerd in hello Azure-emulator en u Hallo optie toodeploy die tooAzure lokale installatie opgeven. Op niet-Windows-besturingssystemen, Hallo emulator JDK instelling is niet van toepassing en kan niet worden geïmplementeerd Hallo lokaal JDK geïnstalleerd omdat het is niet compatibel met Windows. Ongeacht Hallo-besturingssysteem die u gebruikt, u kunt echter altijd kiezen tussen Hallo 3e partij JDK pakketten toodeploy tooAzure of wijst op uw eigen Windows-compatibele JDK-pakket van een alternatieve locatie.

Hallo Hieronder volgt een voorbeeld van hoe u een JDK in Windows kunt opgeven:

![][ic780647]

Als u Eclipse op Windows gebruikt, kunt u een toouse JDK Hello rekenemulator; toodo dus zorg ervoor dat **gebruik Hallo JDK van dit bestandspad om lokaal te testen** Hallo is ingecheckt **Emulator implementatie** sectie. Geef vervolgens Hallo lokaal pad tooyour JDK; u kunt toodifferent JDK bladeren desgewenst hello één toouse wordt niet automatisch geselecteerd. U hebt ook Hallo optie toodeploy uw JDK tooyour Azure-cloudservice; toodo Selecteer daarom Hallo **mijn lokale JDK (automatisch uploaden toocloud opslag) implementeren** optie in Hallo **Cloud implementatie** sectie.

Opmerking: Op niet-Windows-besturingssystemen, Hallo **Emulator implementatie** instellingen en Hallo **implementeren mijn lokale JDK** optie zijn niet beschikbaar. Hallo volgende voorbeeld ziet u een JDK geven op een Mac of andere niet-Windows-besturingssysteem wordt ondersteund:

![][ic789643]

Ongeacht Hallo besturingssysteem u zich bevindt, hebt u na twee Hallo **Cloud implementatie** opties voor het Hallo-bron en het type van uw pakket JDK:

* **Een beschikbaar is op Azure 3e partij JDK pakket implementeren** 
* **Implementeren vanaf een aangepast downloaden** 

Als u van Hallo gebruikmaakt **implementeren van een beschikbaar is via Azure 3e partij JDK pakket** optie:

1. Hallo selectievakje met de naam **implementeren van een beschikbaar is via Azure 3e partij JDK pakket**.
2. Selecteer in de vervolgkeuzelijst hello, Hallo 3e partij JDK pakket dat beschikbaar is in Azure.
3. Uw **JDK** tabblad eruit vergelijkbare toohello volgende in Windows: ![][ic780648] en wordt er gezocht op Mac OS vergelijkbare toohello volgende of andere niet-Windows-besturingssystemen ondersteund:![][ic789643]
4. Klik op **OK** toosave uw wijzigingen.
5. Wanneer de vraag tooaccept hello gebruiksrechtovereenkomst van Hallo 3e partij JDK Pakketprovider, bekijkt u Hallo-licentievoorwaarden. Ervan uitgaande dat u akkoord gaat met hello, klikt u op **Ja** tooclose hello **gebruiksrechtovereenkomst** dialoogvenster.
    Houd er rekening mee dat de onderliggende logica waarvoor items worden weergegeven in de keuzelijst Hallo voor Hallo Hallo **implementeren van een beschikbaar is via Azure 3e partij JDK pakket** optie kan worden aangepast. toocustomize hello items in Hallo **JDK** dialoogvenster, klikt u op Hallo **aanpassen** koppeling. Hiermee sluit u Hallo **JDK** eigenschappenpagina en open Hallo **componentsets.xml** bestand in Eclipse, die u kunt zo nodig wijzigen. Documentatie voor **componentsets.xml** is opgenomen in Hallo **componentsets.xml** -bestand zelf.

Als u van Hallo gebruikmaakt **implementeren van een JDK van downloaden van een aangepaste** optie:

1. Maak een ZIP van de installatiemap van JDK ervoor te zorgen dat Hallo directory knooppunt zelf is Hallo onderliggende van Hallo ZIP structuur en niet de inhoud ervan. Let op Hallo-naam van het Hallo-directory, als u deze later nodig en houd er rekening mee deze JDK installatie worden geïmplementeerde tooa virtuele Windows-machine.
2. Hallo ZIP naar uw Azure storage-account als een blob uploaden. U kunt dit doen met een hulpprogramma voor het extern beschikbaar voor het uploaden van BLOB's tooAzure opslag. Het is aanbevolen toouse een persoonlijke blob. Let op de URL van de blob Hallo Hallo ZIP-inhoud.
3. Hallo selectievakje met de naam **implementeren van een JDK van downloaden van een aangepaste**.
    Als u toodownload van uw Azure storage-account, selecteert u Hallo storage-account van Hallo **Storage-account** vervolgkeuzelijst (u kunt klikken op Hallo **Accounts** koppelen toomodify wat is er in de lijst Hallo), die gedeeltelijk hello wordt ingevuld **URL** veld en vul vervolgens de resterende deel van de URL Hallo Hallo. Als u niet dat toouse Azure-opslag wilt, selecteert u **(geen)** van Hallo **opslagaccount** vervolgkeuzelijst, en voert u Hallo URL tooyour JDK downloaden in Hallo **URL** veld. Als u Azure-opslag gebruikt, is blobnamen in Hallo URL moeten kleine letters.
4. Zorg ervoor dat Hallo **JAVA_HOME** tekstvak voor de naam van de juiste map toohello verwijst. Standaard wordt verwezen naar dezelfde JDK mapnaam Hallo-waarde die u hebt gekozen voor uw lokale gebruik Hallo. Maar als een andere naam Hallo map in Hallo ZIP heeft (bijvoorbeeld vanwege toousing een andere versie), update Hallo mapnaam in Hallo **JAVA_HOME** textbox dienovereenkomstig, aangezien deze instelling worden gebruikt in Hallo cloud () niet in Hallo rekenemulator).
5. Klik op **OK** toosave uw wijzigingen.

Dat is alles. Nu, als u voor Hallo cloud bouwen, zult u Hallo pakketgrootte is veel kleiner, Hallo buildproces duurt meestal minder tijd en Hallo implementatie zelf wanneer u toohello cloud publiceert moet ook rekening houden met minder tijd. Houd er rekening mee dat Hallo **mijn lokale JDK (automatisch uploaden toocloud opslag) implementeren** of **implementeren van een JDK van downloaden van een aangepaste** opties zijn alleen van kracht wanneer uw toepassing wordt geïmplementeerd in de cloud Hallo. Ze hebben geen invloed op uw ervaring van de compute-emulator; Hallo lokale versie van Hallo-onderdelen wordt nog steeds worden gebruikt wanneer u de rekenemulator toohello implementeert. 

### <a name="server-configuration"></a>Serverconfiguratie
Hallo Hier volgt een voorbeeld van hoe u een toepassingsserver kunt opgeven.

![][ic796926]

Controleren dat Hallo **implementeren van een server van dit type** selectievakje is ingeschakeld, en kies vervolgens Hallo-type van de toepassingsserver die u wilt toouse.

Voor het opgeven van een server toouse voor cloudimplementatie, kunt u profiteren van Hallo volgende opties:

1. **Een 3e partij-server beschikbaar zijn in Azure implementeren** -dit is vooral van toepassing in ontwikkelen en testen scenario's waarbij implementatie efficiëntie en eenvoud een prioriteit en Hallo-server geen een aangepaste configuratie vereist. Of als u toouse een van deze servers wilt gebruiken als startpunt hello, maar u bevatten aanpassing van de juiste server in uw implementatie opstartlogica stappen.
2. **Implementeren vanaf het downloaden van een aangepaste** -dit is vooral van toepassing in productiescenario's wanneer u een speciaal voorbereid en geconfigureerde server die u wilt dat toouse in Hallo cloud hebt.
3. **De installatie van de lokale server implementeren** -dit is vooral van toepassing in als de installatie van de lokale server al aangepaste geconfigureerd voor gebruik is. Als u deze optie kiest, moet u ook de lokale server pad opgeeft in Hallo **pad naar de lokale server** onderstaande tekstvak.

Als u van Hallo gebruikmaakt **3e partij-server implementeren in Azure beschikbaar** optie:

1. Hallo selectievakje met de naam **3e partij-server implementeren in Azure beschikbaar**.
2. Selecteer in het vervolgkeuzemenu Hallo, Hallo gewenst server software toouse met uw implementatie in Hallo cloud. Opmerking: als u al een type server toouse eerder hebt opgegeven, worden beperkt toochoosing een cloud-server die zich in Hallo uit dezelfde familie als het type van die server. Maar als u geen servertype hebt gekozen, kunt u kiezen uit Hallo-servers die momenteel beschikbaar op Azure zijn en Hallo servertype wordt automatisch voor u geselecteerd.
3. Klik op **OK** toosave uw wijzigingen.

Als u Hallo **implementeren van een aangepaste download** optie:

1. Zorg ervoor dat u al een servertype volgens toohello vorige stappen hebt geselecteerd. Dit vertelt Hallo invoegtoepassing hoe toodeploy Hallo server van uw aangepaste downloaden, zoals deze moet vallen tussen-Hallo uit dezelfde familie als uw type geselecteerde server.
2. Hallo selectievakje met de naam **implementeren van een aangepaste download**.
    Als u toodownload van uw Azure storage-account, selecteert u Hallo storage-account van Hallo **Storage-account** vervolgkeuzelijst (u kunt klikken op Hallo **Accounts** koppelen toomodify wat is er in de lijst Hallo), die gedeeltelijk hello wordt ingevuld **URL** veld en vult u Hallo resterende deel van Hallo URL tooyour server ZIP downloaden (wanneer met behulp van Azure-opslag, blob-namen in Hallo-URL een kleine letter moet). Als u niet dat toouse Azure-opslag wilt, selecteert u **(geen)** van Hallo **opslagaccount** vervolgkeuzelijst, en voert u Hallo URL tooyour server download ZIP in Hallo **URL** veld. Hallo ZIP zou een onderliggende map voor de installatiemap van uw toepassing-server bevatten. Bijvoorbeeld, als u van een zip voor Apache Tomcat 7.0.35 gebruikmaakt, binnen Hallo zip zou zijn Hallo onderliggende map die Hallo installatiemap, zoals **apache-tomcat-7.0.35**. 
3. Hallo waarde opgeven voor Hallo basismap omgevingsvariabele. Wordt standaard toohello-waarde gebruikt voor uw lokale toepassingsserver, indien van toepassing, maar u kunt een andere waarde opgeven als de cloud-toepassingsserver af van uw lokale toepassingsserver wijkt. Echter, moet u ervoor dat uw cloud-toepassingsserver Hallo toomake uit dezelfde familie als type Hallo-server eerder hebt geselecteerd.
    Als u uw cloud application server zip in toekomstige Hallo bijwerkt, kunt u handmatig wijzigen Hallo basismap instelling of toohave deze opnieuw overeenkomt met uw lokale instelling (als u uw lokale toepassingsserver te gewijzigd).
4. Klik op **OK** toosave uw wijzigingen.

Hallo onderliggende logica waarvoor items worden weergegeven in Hallo **Server** tabblad Hallo **serverconfiguratie** eigenschappenpagina kan worden aangepast. Dit is een geavanceerde functie die u wellicht als uw behoeften Hallo standaardwaarden overschrijden of als u tooadd andere servers wilt. toocustomize hello logica in Hallo **Server** dialoogvenster, klikt u op Hallo **aanpassen** koppeling. Hiermee sluit u Hallo **serverconfiguratie** eigenschappenpagina en open Hallo **componentsets.xml** bestand in Eclipse, die u als sjabloon benodigde tooextend Hallo server-configuratie kunt wijzigen. Documentatie voor **componentsets.xml** is opgenomen in Hallo **componentsets.xml** -bestand zelf.

Als u van Hallo gebruikmaakt **mijn lokale server (automatisch uploaden toocloud opslag) implementeren** optie:

1. Hallo selectievakje met de naam **mijn lokale server (automatisch uploaden toocloud opslag) implementeren**.
2. Met behulp van Hallo **opslagaccount** vervolgkeuzelijst, selecteer **(automatisch)**. Als u opgeeft **(automatisch)** hier Hallo Eclipse toolkit gebruikt hetzelfde opslagaccount voor uw server als Hallo Hallo een u voor uw implementatie in Hallo **tooAzure publiceren** dialoogvenster.
3. Klik op **OK** toosave uw wijzigingen.

Selecteer een installatiepad voor de server op uw computer in Hallo **pad naar de lokale server** tekstvak als een van de Hallo volgende voorwaarden voldaan wordt:

* Wilt u tootest uw implementatie in Hallo-emulator (geldt alleen tooWindows).
* Wilt u toodeploy uw lokaal geïnstalleerde server toohello cloud.
* U wilt dat toouse downloaden van uw eigen in cloud hello, in welk geval door een aangepaste server, zorg er ook voor Hallo **mijn lokale server (automatisch uploaden toocloud opslag) implementeren** hierboven is ingeschakeld.

Als geen van de voorgaande opties Hallo tooyour situatie toepassing, is Hallo lokale server optioneel.

### <a name="applications-configuration"></a>Configuratie van de toepassing
Hallo Hier volgt een voorbeeld van hoe u een toepassing kunt opgeven.

![][ic719512]

Klik op **toevoegen** tooadd een andere toepassing of **verwijderen** tooremove een toepassing. Voor de efficiëntie, als u downloaden van een toouse voor Hallo bron van een toepassing wilt bij het implementeren van cloud toohello, gebruik Hallo [onderdelen eigenschappen](#components_properties) toospecify een URL, storage-account, enzovoort. 

Beginnend met Hallo release van April 2014, worden uw toepassingen automatisch geüpload naar Hallo hetzelfde opslagaccount (onder Hallo **eclipsedeploy** container) zoals Hallo geselecteerd voor uw implementatie. Hallo opstartlogica van uw implementatie bevat een stap die u downloadt eerst deze toepassingen uit dat opslagaccount. Dit betekent dat u mogelijk uw toepassingen in uw implementatie bijwerken zonder toorebuild en Hallo gehele pakket, opnieuw implementeren door de nieuwere versies van de toepassing hello rechtstreeks in dit opslagaccount (bijvoorbeeld hello Azure-portal met) handmatig uploaden , vervangen, Hallo WAR bestanden oorspronkelijk er geüpload door Hallo toolkit. Vervolgens net start Hallo recycling van alle die rolinstanties met behulp van de Azure-beheerportal opnieuw, of via de opdrachtregel-hulpprogramma's. (Rol rechtstreeks vanuit het recyclen binnen Hallo Eclipse toolkit activerende is momenteel niet ondersteund.)

### <a name="notes-about-server-configuration"></a>Opmerkingen over de serverconfiguratie van de
Wijzigingen via Hallo **serverconfiguratie** eigenschappenpagina worden doorgevoerd in Hallo `<component>` elementen van het bestand Hallo-Package.xml heeft.

Wanneer u Hallo gebruikt **automatisch uploaden...**  of **implementeren niet worden gedownload...**  opties voor Hallo JDK of toepassingsserver en u wilt maken voor Hallo cloud (geen Hallo rekenemulator), en u bent verbonden toohello netwerk, merkt u berichten, zoals het volgende in de Console-uitvoer Hallo Hallo bouwen, zoals Ant Hallo Builder controleert de beschikbaarheid van Hallo downloaden:

`[windowsazurepackage] Verifying blob availability (https://example.blob.core.windows.net/temp/tomcat6.zip)...` 

Als u geselecteerd Hallo **implementeren niet worden gedownload...**  optie Hallo waarschuwing na kan worden weergegeven, maar Hallo build gaat verder:

`[windowsazurepackage] warning: Failed tooconfirm blob availability! Make sure hello URL and/or hello access key is correct (https://example.blob.core.windows.net/temp/tomcat6.zip).` 

Deze waarschuwing is Hallo enige aanwijzing dat Hallo downloaden van beschikbaarheid niet is gecontroleerd. Dus als een implementatie is mislukt in de cloud Hallo voor een bepaalde reden, Controleer toosee als u deze waarschuwing hebt ontvangen.

Als u wilt dat toodisable Hallo downloaden verificatie (bijvoorbeeld, als u denkt dit onnodig vertraagt de Hallo build dat) stelt hello `verifydownloads` te kenmerk`false` in Hallo `<windowsazurepackage>` element van Package.xml heeft: 

`<windowsazurepackage verifydownloads="false" ...>` 

Als u geselecteerd Hallo **automatisch uploaden...**  optie, en vervolgens in het consolevenster Hallo ziet u hoe build berichten reporting Hallo voortgang van Hallo uploaden om de vijf seconden, wanneer een upload nodig is.

<a name="ssl_offloading_properties"></a> 

### <a name="ssl-offloading-properties"></a>SSL-offloading eigenschappen
Hallo contextmenu voor Hallo rol in Eclipse van Projectverkenner deelvenster openen, klikt u op **Azure**, en klik vervolgens op **SSL-Offloading**. 

![][ic719481]

In dit dialoogvenster kunt u SSL-offloading, zodat u tooeasily inschakelen Hypertext Transfer Protocol Secure (HTTPS) in uw implementatie Java in Azure, ondersteunen zonder dat u tooconfigure SSL in uw Java-toepassingsserver inschakelen. Zie voor meer informatie [SSL-Offloading] [ SSL Offloading] en [hoe tooUse SSL-Offloading][How tooUse SSL Offloading].

## <a name="see-also"></a>Zie ook
[Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]

[Hello Azure Toolkit voor Eclipse installeren][Installing hello Azure Toolkit for Eclipse]

[Maken van een Hallo wereld-toepassing voor Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Eigenschappen van de Azure-Project][Azure Project Properties]

[Lijst met Azure Storage-Account][Azure Storage Account List]

Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center][Azure Java Developer Center].

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
[How tooUse Co-located Caching]: http://go.microsoft.com/fwlink/?LinkID=699542
[How tooUse SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699545
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
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
