---
title: aaaHow toouse toegangsbeheer (Java) | Microsoft Docs
description: Meer informatie over hoe toodevelop en gebruik toegang beheren met Java in Azure.
services: active-directory
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 247dfd59-0221-4193-97ec-4f3ebe01d3c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.custom: aaddev
ms.openlocfilehash: cbbce3b1a05eabf3b86a8cb91db1bde92dbb8960
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthenticate-web-users-with-azure-access-control-service-using-eclipse"></a>Hoe tooAuthenticate webgebruikers met Azure Access Control-Service met behulp van Eclipse
Deze handleiding leert u hoe toouse Azure Access Control Service (ACS) Hallo binnen hello Azure Toolkit voor Eclipse. Zie voor meer informatie over ACS Hallo [Vervolgstappen](#next_steps) sectie.

> [!NOTE]
> Hello Azure Access Control servicefilter is een community technology preview. Als de bètasoftware, wordt deze niet formeel ondersteund door Microsoft.
> 
> 

## <a name="what-is-acs"></a>Wat is ACS?
De meeste ontwikkelaars zijn niet identiteit deskundigen en over het algemeen niet wilt besteden aan de tijd ontwikkelen verificatie en autorisatie mechanismen voor hun toepassingen en services. ACS is een Azure-service waarmee u een eenvoudige manier voor het authenticeren van gebruikers hoeven tooaccess uw webtoepassingen en services zonder toofactor verificatie complexe logica in uw code.

Hallo volgende functies zijn beschikbaar in ACS:

* Integratie met Windows Identity Foundation (WIF).
* Ondersteuning voor populaire web id-providers (IP's) dat met inbegrip van Windows Live ID, Google, Yahoo! en Facebook.
* Ondersteuning voor Active Directory Federatieservices (AD FS) 2.0.
* Een Open Data Protocol (OData)-management-service die programmatisch toegang tooACS instellingen biedt.
* Een beheerportal waarmee beheerderstoegang toohello ACS-instellingen.

Zie voor meer informatie over ACS [Access Control Service 2.0][Access Control Service 2.0].

## <a name="concepts"></a>Concepten
Azure ACS is gebouwd op Hallo principals van op claims gebaseerde identiteit - een consistente werkwijze toocreating verificatiemechanismen voor toepassingen die lokaal wordt uitgevoerd of in Hallo cloud. Op claims gebaseerde identiteit biedt een veelgebruikte manier voor toepassingen en services tooacquire de identiteit de benodigde informatie over gebruikers binnen hun organisatie in andere organisaties en op Hallo Internet.

toocomplete hello taken in deze handleiding, moet u weten Hallo volgende concepten:

**Client** -In Hallo context van deze procedure-tooguide, is dit een browser die toogain toegang tooyour-webtoepassing probeert.

**Relying party (RP)-toepassing** -een RP-toepassing is een website of de service die externe verificatie tooone-instantie heeft. Identiteit jargon spreken we dat Hallo RP vertrouwt die instantie. Deze handleiding wordt uitgelegd hoe tooconfigure uw toepassing tootrust ACS.

**Token** -token is een verzameling van beveiligingsgegevens die meestal na een geslaagde verificatie van een gebruiker wordt verleend. Deze bevat een reeks *claims*, kenmerken van Hallo geverifieerde gebruiker. Een claim kan vertegenwoordigen een gebruikersnaam, een id voor een functie van een gebruiker behoort, van een gebruiker leeftijd, enzovoort. Een token wordt meestal digitaal zijn ondertekend, wat betekent dat deze kan altijd worden brongegevens back tooits verlener en de inhoud ervan kan worden geknoeid. Een gebruiker krijgt toegang tot tooa RP toepassing in de vorm van een geldig token dat is uitgegeven door een instantie dat Hallo RP toepassing vertrouwt.

**ID-Provider (IP)** -een IP-adres is een instantie die verifieert gebruikers-id's en verstrekt beveiligingstokens. Hallo eigenlijke werk van het uitgeven van tokens wordt geïmplementeerd als een speciale service Security Token Service (STS) genoemd. Typische voorbeelden van IP-adressen zijn Windows Live ID, Facebook en zakelijke gebruiker opslagplaatsen (zoals Active Directory).
Als ACS geconfigureerde tootrust een IP-adres is, Hallo system accepteert en valideren van tokens die zijn uitgegeven door die IP. ACS kan meerdere IP-adressen in één keer dat betekent dat als uw toepassing ACS vertrouwt, u direct uw toepassing tooall Hallo aanbieden kunt geverifieerde gebruikers van alle Hallo IP-adressen die ACS vertrouwensrelaties namens jou worden vertrouwd.

**Federation-Provider (EP)** -IP-adressen direct kennis hebben van gebruikers, en ze met hun referenties worden geverifieerd en claims over wat ze over deze weten uitgeven. Een Federation-Provider (EP) is een ander soort autoriteit: in plaats van rechtstreeks verifiëren van gebruikers die deze fungeert als een tussenkomst en beleggingsmakelaars verificatie tussen één RP en een of meer IP-adressen. Zowel de IP-adressen en de FPs beveiligingstokens, daarom ze gebruiken allebei Security Token Services (STS). ACS is één FrontPage.

**ACS regel Engine** -Hallo logica gebruikte tootransform binnenkomende tokens van vertrouwde IP-adressen tootokens bedoeld toobe verbruikt door Hallo RP is overgegaan in de vorm van eenvoudige claims transformatie-regels. ACS is uitgerust met een regel-engine die al worden verzorgd door gelijk welke logica transformatie is opgegeven voor uw RP toe te passen.

**ACS-Namespace** -een-naamruimte is een partitie van het hoogste niveau van ACS die u gebruikt voor het ordenen van uw instellingen. Een naamruimte bevat een lijst met IP-adressen u vertrouwt, Hallo RP toepassingen die u wilt dat tooserve, Hallo-regels die u verwacht Hallo regel engine tooprocess binnenkomende tokens, enzovoort. Een naamruimte beschrijft de verschillende eindpunten die worden gebruikt door het Hallo-toepassing en de ontwikkelaar tooget ACS tooperform de functie.

Hallo volgende afbeelding ziet u hoe de ACS-verificatie werkt met een webtoepassing:

![Stroomdiagram van ACS][acs_flow]

1. Hallo-client (in dit geval een browser) wordt een pagina opvraagt bij Hallo RP.
2. Aangezien Hallo aanvraag nog niet is geverifieerd, leidt Hallo RP Hallo gebruiker toohello de certificeringsinstantie die wordt vertrouwd, namelijk ACS. Hallo ACS biedt Hallo keuze van IP-adressen die zijn opgegeven voor deze RP Hallo-gebruiker. Hallo-gebruiker selecteert het juiste IP Hallo.
3. Hallo-client op de verificatiepagina toohello IP's gezocht en vraagt Hallo gebruiker toolog op.
4. Nadat het Hallo-client is geverifieerd (bijvoorbeeld Hallo identiteit referenties zijn ingevoerd), wordt IP Hallo een beveiligingstoken.
5. Na het uitgeven van een beveiligingstoken Hallo IP worden omgeleid Hallo client tooACS en Hallo client verzendt Hallo beveiligingstoken uitgegeven door Hallo IP-tooACS.
6. ACS valideert Hallo-beveiligingstoken dat is uitgegeven door Hallo IP-adres invoer Hallo identiteit in Hallo ACS regelengine-claims in dit token, berekent identiteitsclaims Hallo-uitvoer en geeft een nieuw beveiligingstoken dat deze uitvoer claims bevat.
7. ACS leidt Hallo client toohello RP. Hallo-client verzendt Hallo nieuw beveiligingstoken uitgegeven door ACS toohello RP. Hallo RP valideert Hallo handtekening op Hallo-beveiligingstoken dat is uitgegeven door ACS, Hallo claims in dit token valideert en retourneert Hallo pagina die oorspronkelijk zijn aangevraagd.

## <a name="prerequisites"></a>Vereisten
toocomplete hello taken in deze handleiding, moet u de volgende Hallo:

* Een Java Developer Kit (JDK), v 1.6 of hoger.
* Eclipse IDE voor Java EE-ontwikkelaars Indigo of hoger. Dit kan worden gedownload vanaf <http://www.eclipse.org/downloads/>. 
* Een distributiepunt van een Java gebaseerde webserver of toepassingsserver, zoals Apache Tomcat, GlassFish, JBoss-toepassingsserver of Jetty.
* een Azure-abonnement, die kan worden opgehaald uit <http://www.microsoft.com/windowsazure/offers/>.
* Hello Azure Toolkit voor Eclipse April 2014 release of hoger. Zie voor meer informatie [installeren hello Azure Toolkit voor Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690946.aspx).
* Een x.509-certificaat toouse met uw toepassing. U moet dit certificaat in openbaar certificaat (.cer) en Personal Information Exchange (. (PFX)-indeling. (Opties voor het maken van dit certificaat wordt verderop in deze zelfstudie worden beschreven).
* Bekend bent met hello Azure compute-emulator en implementatie technieken besproken op [maken van een toepassing Hello World voor Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx).

## <a name="create-an-acs-namespace"></a>Maken van een ACS-Namespace
toobegin met Access Control Service (ACS) in Azure, moet u een ACS-naamruimte maken. Hallo naamruimte biedt een unieke bereik op voor het verwerken van ACS-resources van uw toepassing.

1. Meld u aan bij Hallo [Azure Management Portal][Azure Management Portal].
2. Klik op **Active Directory**. 
3. toocreate een nieuwe Access Control-naamruimte, klikt u op **nieuw**, klikt u op **App Services**, klikt u op **toegangsbeheer**, en klik vervolgens op **snelle invoer** . 
4. Voer een naam voor Hallo-naamruimte. Azure verifieert dat naam Hallo uniek is.
5. Selecteer Hallo regio in welke Hallo naamruimte wordt gebruikt. Gebruik voor de beste prestaties Hallo Hallo regio waarin u uw toepassing implementeert.
6. Als u meer dan één abonnement hebt, selecteert u Hallo-abonnement dat u toouse Hallo ACS-naamruimte wenst.
7. Klik op **Create**.

Azure maakt en Hallo-naamruimte wordt geactiveerd. Wacht totdat de status van de nieuwe naamruimte Hallo Hallo **Active** voordat u doorgaat. 

## <a name="add-identity-providers"></a>Id-providers toevoegen
In deze taak kunt u IP-adressen toouse toevoegen aan uw toepassing RP voor verificatie. Voor demonstratiedoeleinden ziet deze taak u hoe tooadd Windows Live als een IP-adres, maar een van de IP-adressen die worden vermeld in de ACS-beheerportal Hallo Hallo kan gebruiken.

1. In Hallo [Azure Management Portal][Azure Management Portal], klikt u op **Active Directory**, selecteert u een Access Control-naamruimte en klik vervolgens op **beheren**. Hallo ACS-beheerportal geopend.
2. Klik in het Hallo navigatiedeelvenster links Hallo ACS-beheerportal op **identiteitsproviders**.
3. Windows Live ID is standaard ingeschakeld en kan niet worden verwijderd. Voor deze zelfstudie wordt alleen Windows Live ID gebruikt. Dit scherm is echter waar u andere IP-adressen kunnen toevoegen door te klikken op Hallo **toevoegen** knop.

Windows Live ID is nu ingeschakeld als een IP-adres voor de ACS-naamruimte. Vervolgens moet u uw Java-webtoepassing (toobe later gemaakt) opgeven als een RP.

## <a name="add-a-relying-party-application"></a>Toevoegen van een relying party-toepassing
In deze taak configureert u ACS toorecognize uw Java-webtoepassing als een geldige RP-toepassing.

1. Klik op Hallo ACS-beheerportal, **Relying party-toepassingen**.
2. Op Hallo **Relying Party-toepassingen** pagina, klikt u op **toevoegen**.
3. Op Hallo **Relying Party-toepassing toevoegen** pagina, Hallo te volgen:
   
   1. In **naam**, Hallo typenaam Hallo RP. Typ voor deze zelfstudie **Azure-Web-App**.
   2. In **modus**, selecteer **Voer instellingen handmatig**.
   3. In **Realm**, type Hallo URI toowhich hello security token dat is uitgegeven door ACS is van toepassing. Typ voor deze taak **http://localhost: 8080 /**.
      ![Realm voor de relying party voor gebruik in rekenemulator][relying_party_realm_emulator]
   4. In **retour-URL** type Hallo URL toowhich ACS retourneert Hallo-beveiligingstoken. Typ voor deze taak **http://localhost:8080/MyACSHelloWorld/index.jsp**
      ![Relying party retour-URL voor gebruik in rekenemulator][relying_party_return_url_emulator]
   5. Accepteer de standaardwaarden Hallo in Hallo rest van Hallo velden.
4. Klik op **Opslaan**.

U hebt nu geconfigureerd uw Java-webtoepassing wanneer deze wordt uitgevoerd in Azure-rekenemulator hello (op http://localhost: 8080 /) toobe een RP in uw ACS-naamruimte. Maak vervolgens Hallo regels die ACS tooprocess claims voor Hallo RP gebruikt.

## <a name="create-rules"></a>Regels maken
In deze taak definieert u Hallo-regels die station hoe claims van de IP-adressen tooyour RP worden doorgestuurd. Voor Hallo doel van deze handleiding configureert we gewoon ACS toocopy Hallo invoer claimtypen en claimwaarden rechtstreeks in Hallo uitvoertoken, zonder deze wijzigen of filteren.

1. Klik op Hallo ACS-beheerportal hoofdpagina **regel groepen**.
2. Op Hallo **regelgroepen** pagina, klikt u op **regelgroep standaard voor Azure-Web-App**.
3. Op Hallo **regelgroep bewerken** pagina, klikt u op **genereren**.
4. Op Hallo **-regels genereren: standaard regelgroep voor Azure-Web-App** pagina, zorg ervoor dat Windows Live ID is ingeschakeld en klik vervolgens op **genereren**.    
5. Op Hallo **regelgroep bewerken** pagina, klikt u op **opslaan**.

## <a name="upload-a-certificate-tooyour-acs-namespace"></a>Upload een certificaat tooyour ACS-naamruimte
In deze taak die u uploadt een. PFX-certificaat die gebruikt toosign aanvragen voor beveiligingstokens die door de ACS-naamruimte gemaakt worden.

1. Klik op Hallo ACS-beheerportal hoofdpagina **certificaten en sleutels**.
2. Op Hallo **certificaten en sleutels** pagina, klikt u op **toevoegen** hierboven **Token-ondertekening**.
3. Op Hallo **certificaat toevoegen Token-ondertekening of sleutel** pagina:
   1. In Hallo **gebruikt voor** sectie, klikt u op **Relying Party-toepassing** en selecteer **Azure-Web-App** (die u eerder hebt ingesteld als naam van uw relying party-toepassing hello).
   2. In Hallo **Type** sectie **X.509-certificaat**.
   3. In Hallo **certificaat** sectie en klik op de knop Bladeren Hallo toohello X.509-certificaat-bestand dat u wilt dat toouse navigeren. Dit is een. PFX-bestand. Hallo-bestand selecteren, klikt u op **Open**, en voer het certificaatwachtwoord Hallo in Hallo **wachtwoord** in het tekstvak. Houd er rekening mee dat een zelfstandige-signed-certificaat voor testdoeleinden kan gebruiken. toocreate een zelfondertekend certificaat gebruiken Hallo **nieuw** knop in Hallo **ACS Filter bibliotheek** dialoogvenster (later beschreven), of gebruik Hallo **encutil.exe** hulpprogramma van Hallo [project website] [ project website] Hallo Azure Starter Kit voor Java.
   4. Zorg ervoor dat **primair maken** is ingeschakeld. Uw **certificaat toevoegen Token-ondertekening of sleutel** pagina ziet er vergelijkbare toohello volgende.
       ![Certificaat voor token-ondertekening toevoegen][add_token_signing_cert]
   5. Klik op **opslaan** toosave uw instellingen en sluit Hallo **certificaat toevoegen Token-ondertekening of sleutel** pagina.

Informatie van de Hallo op Hallo toepassingsintegratie pagina en kopieer Hallo URI moet u tooconfigure uw Java web application toouse ACS vervolgens controleren.

## <a name="review-hello-application-integration-page"></a>Voorbeeldpagina Hallo integratie van toepassingen
U vindt alle Hallo informatie en Hallo code nodig tooconfigure uw web Java in toowork met ACS wordt toepassing (RP toepassing hello) op Hallo toepassingsintegratie pagina Hallo ACS-beheerportal. U moet deze informatie bij het configureren van uw Java-webtoepassing voor federatieve verificatie.

1. Klik op Hallo ACS-beheerportal, **toepassingsintegratie**.  
2. In Hallo **toepassingsintegratie** pagina, klikt u op **aanmeldingspagina's**.
3. In Hallo **aanmelding pagina integratie** pagina, klikt u op **Azure-Web-App**.

In Hallo **aanmelding pagina integratie: Azure-Web-App** pagina Hallo-URL die wordt vermeld **optie 1: koppeling tooan ACS gehost aanmeldingspagina** wordt gebruikt in uw Java-webtoepassing. U moet deze waarde als u hello Azure Access Control-servicefilter bibliotheek tooyour Java-toepassing toevoegt.

## <a name="create-a-java-web-application"></a>Een Java-webtoepassing maken
1. Klik in Eclipse op Hallo-menu op **bestand**, klikt u op **nieuw**, en klik vervolgens op **dynamisch webproject**. (Als er geen **dynamisch webproject** vermeld als een project beschikbaar wanneer u op **bestand**, **nieuw**, vervolgens Hallo te volgen: klik op **bestand**, klikt u op **nieuw**, klikt u op **Project**, vouw **Web**, klikt u op **dynamisch webproject**, en klik op  **Naast**.) Naam voor deze zelfstudie Hallo project **MyACSHelloWorld**. (Zorg ervoor dat u gebruikt deze naam, de volgende stappen in deze zelfstudie verwacht dat het WAR-bestand toobe MyACSHelloWorld met de naam). Het scherm wordt vergelijkbaar toohello volgende weergegeven:
   
    ![Maak een project Hallo wereld voor ACS exampple][create_acs_hello_world]
   
    Klik op **Voltooien**.
2. Vouw in de weergave Project Explorer van Eclipse **MyACSHelloWorld**. Klik met de rechtermuisknop op **WebContent**(Webinhoud) en klik vervolgens op **New** (Nieuw) en **JSP File** (JSP-bestand).
3. In Hallo **nieuw JSP-bestand** dialoogvenster, Hallo bestandsnaam **index.jsp**. Houd Hallo bovenliggende map als MyACSHelloWorld/WebContent, zoals wordt weergegeven in de volgende Hallo:
   
    ![Een JSP-bestand bijvoorbeeld ACS toevoegen][add_jsp_file_acs]
   
    Klik op **Volgende**.
4. In Hallo **JSP-sjabloon selecteren** dialoogvenster **nieuw JSP-bestand (html)** en klik op **voltooien**.
5. Wanneer de bestand index.jsp hello wordt geopend in Eclipse, toevoegen in de tekst toodisplay **Hello ACS World!** binnen de bestaande Hallo `<body>` element. Uw bijgewerkte `<body>` inhoud moet worden weergegeven als Hallo volgende:
   
        <body>
          <b><% out.println("Hello ACS World!"); %></b>
        </body>
   
    Index.jsp opslaan.

## <a name="add-hello-acs-filter-library-tooyour-application"></a>Hallo ACS Filter bibliotheek tooyour toepassing toevoegen
1. In de Projectverkenner van Eclipse met de rechtermuisknop op **MyACSHelloWorld**, klikt u op **pad**, en klik vervolgens op **configureren pad**.
2. In Hallo **Javabuild-pad** dialoogvenster, klikt u op Hallo **bibliotheken** tabblad.
3. Klik op **bibliotheek toevoegen**.
4. Klik op **Azure Access Control servicefilter (door MS Open Tech)** en klik vervolgens op **volgende**. Hallo **Azure Access Control-servicefilter** dialoogvenster wordt weergegeven.  (Hallo **locatie** veld heeft misschien een ander pad, afhankelijk van waar u Eclipse hebt geïnstalleerd en Hallo versienummer kan verschillen, afhankelijk van de software-updates.)
   
    ![Bibliotheek van ACS-Filter toevoegen][add_acs_filter_lib]
5. Met een browser geopend toohello **aanmelding pagina integratie** pagina Hallo-beheerportal kopie Hallo-URL die wordt vermeld in Hallo **optie 1: koppeling tooan ACS gehost aanmeldingspagina** veld en plak deze in Hallo **ACS-eindpunt voor authenticatie** veld van Hallo Eclipse dialoogvenster.
6. Met een browser geopend toohello **Relying Party-toepassing bewerken** pagina Hallo-beheerportal kopie Hallo-URL die wordt vermeld in Hallo **Realm** veld en plak deze in Hallo **Realm voor de Relying Party**  veld van Hallo Eclipse dialoogvenster.
7. Binnen Hallo **beveiliging** sectie van Hallo Eclipse dialoogvenster, als u wilt dat toouse een bestaand certificaat, klik op **Bladeren**, navigeer toohello certificaat wilt toouse, selecteert u deze en klikt u op  **Open**. Als u een nieuw certificaat toocreate wilt, klikt u op **nieuw** toodisplay hello **nieuw certificaat** dialoogvenster geeft Hallo wachtwoord, de naam van Hallo cer-bestand en de naam van PFX-bestand voor de nieuwe Hallo Hallo certificaat.
8. Controleer **insluiten Hallo certificaat in het WAR-bestand Hallo**. Opgenomen in de insluiten Hallo-certificaat op deze manier in uw implementatie zonder dat u toomanually toevoegen als een onderdeel. (Als in plaats daarvan moet u uw certificaat voor extern opslaan van het WAR-bestand, kan u Hallo certificaat als een onderdeel van de rol toevoegen en schakel het selectievakje **insluiten Hallo certificaat in het WAR-bestand Hallo**.)
9. [Optioneel] Houd **vereisen HTTPS-verbindingen** gecontroleerd. Als u deze optie instelt, moet u tooaccess uw toepassing met Hallo HTTPS-protocol. Als u niet toorequire HTTPS-verbindingen wilt, schakelt u deze optie.
10. Voor een implementatie toohello rekenemulator, uw **Azure ACS Filter** instellingen eruitzien vergelijkbare toohello volgende.
    
    ![Azure ACS filterinstellingen voor een implementatie toohello rekenemulator][add_acs_filter_lib_emulator]
11. Klik op **Voltooien**.
12. Klik op **Ja** wanneer krijgt met een dialoogvenster waarin wordt vermeld dat een web.xml-bestand wordt gemaakt.
13. Klik op **OK** tooclose hello **Javabuild-pad** dialoogvenster.

## <a name="deploy-toohello-compute-emulator"></a>De rekenemulator toohello implementeren
1. In de Projectverkenner van Eclipse met de rechtermuisknop op **MyACSHelloWorld**, klikt u op **Azure**, en klik vervolgens op **-pakket voor Azure**.
2. Voor **projectnaam**, type **MyAzureACSProject** en klik op **volgende**.
3. Selecteer een JDK en toepassingsservers. (Deze stappen worden behandeld in detail in Hallo [maken van een toepassing Hello World voor Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx) zelfstudie).
4. Klik op **Voltooien**.
5. Klik op Hallo **uitvoeren in Azure-Emulator** knop.
6. Nadat uw Java-webtoepassing is gestart in de rekenemulator hello, sluit u alle exemplaren van uw browser (zodat alle huidige browsersessies veroorzaken geen met ACS aanmelding testen conflicten).
7. Voer uw toepassing via <http://localhost: 8080/MyACSHelloWorld/> in uw browser (of <https://localhost:8080/MyACSHelloWorld/> als u dit selectievakje inschakelt **vereisen HTTPS-verbindingen** ). U moet worden gevraagd om een Windows Live ID-aanmelding en u toohello retour-URL opgegeven voor de relying party-toepassing moet worden gehouden.
8. Wanneer u klaar bent met het weergeven van uw toepassing, klikt u op Hallo **opnieuw instellen van de Azure-Emulator** knop.

## <a name="deploy-tooazure"></a>TooAzure implementeren
toodeploy tooAzure, moet u toochange Hallo relying party realm en retour-URL voor de ACS-naamruimte.

1. Binnen hello Azure-beheerportal in Hallo **Relying Party-toepassing bewerken** pagina, wijzigt u **Realm** toobe Hallo-URL van uw geïmplementeerde site. Vervang **voorbeeld** met Hallo DNS-naam die u hebt opgegeven voor uw implementatie.
   
    ![Realm voor de relying party voor gebruik in productie][relying_party_realm_production]
2. Wijzig **retour-URL** toobe Hallo-URL van uw toepassing. Vervang **voorbeeld** met Hallo DNS-naam die u hebt opgegeven voor uw implementatie.
   
    ![Relying party retour-URL voor gebruik in productie][relying_party_return_url_production]
3. Klik op **opslaan** toosave de bijgewerkte beantwoorden partij realm en retour-URL gewijzigd.
4. Hallo houden **aanmelding pagina integratie** pagina openen in uw browser, moet u toocopy hieruit binnenkort.
5. In de Projectverkenner van Eclipse met de rechtermuisknop op **MyACSHelloWorld**, klikt u op **pad**, en klik vervolgens op **configureren pad**.
6. Klik op Hallo **bibliotheken** tabblad **Azure Access Control-servicefilter**, en klik vervolgens op **bewerken**.
7. Met een browser geopend toohello **aanmelding pagina integratie** pagina Hallo-beheerportal kopie Hallo-URL die wordt vermeld in Hallo **optie 1: koppeling tooan ACS gehost aanmeldingspagina** veld en plak deze in Hallo **ACS-eindpunt voor authenticatie** veld van Hallo Eclipse dialoogvenster.
8. Met een browser geopend toohello **Relying Party-toepassing bewerken** pagina Hallo-beheerportal kopie Hallo-URL die wordt vermeld in Hallo **Realm** veld en plak deze in Hallo **Realm voor de Relying Party**  veld van Hallo Eclipse dialoogvenster.
9. Binnen Hallo **beveiliging** sectie van Hallo Eclipse dialoogvenster, als u wilt dat toouse een bestaand certificaat, klik op **Bladeren**, navigeer toohello certificaat wilt toouse, selecteert u deze en klikt u op  **Open**. Als u een nieuw certificaat toocreate wilt, klikt u op **nieuw** toodisplay hello **nieuw certificaat** dialoogvenster geeft Hallo wachtwoord, de naam van Hallo cer-bestand en de naam van PFX-bestand voor de nieuwe Hallo Hallo certificaat.
10. Houd **insluiten Hallo certificaat in het WAR-bestand Hallo** dit selectievakje inschakelt, ervan uitgaande dat u wilt dat tooembed Hallo certificaat in Hallo WAR-bestand.
11. [Optioneel] Houd **vereisen HTTPS-verbindingen** gecontroleerd. Als u deze optie instelt, moet u tooaccess uw toepassing met Hallo HTTPS-protocol. Als u niet toorequire HTTPS-verbindingen wilt, schakelt u deze optie.
12. Voor een tooAzure implementatie eruit ziet uw Azure-ACS filterinstellingen vergelijkbare toohello volgende.
    
    ![Azure ACS filterinstellingen voor een productie-implementatie][add_acs_filter_lib_production]
13. Klik op **voltooien** tooclose hello **bibliotheek bewerken** dialoogvenster.
14. Klik op **OK** tooclose hello **eigenschappen voor MyACSHelloWorld** dialoogvenster.
15. Klik in Eclipse op Hallo **tooAzure Cloud publiceren** knop. Vergelijkbare zoals gedaan in Hallo toohello prompts reageren **toodeploy uw toepassing tooAzure** sectie Hallo [maken van een toepassing Hello World voor Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx) onderwerp. 

Nadat uw webtoepassing is geïmplementeerd, sluit eventuele geopende browsersessies uitvoeren van uw webtoepassing en wordt u gevraagd het toosign met Windows Live ID-referenties, gevolgd door verstuurd toohello retour-URL van uw relying party-toepassing.

Wanneer u klaar bent met behulp van uw toepassing ACS Hallo wereld Hallo-implementatie toodelete onthouden (leert u hoe een implementatie in Hallo toodelete [maken van een toepassing Hello World voor Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx) onderwerp).

## <a name="next_steps"></a>Volgende stappen
Zie voor een onderzoek Hallo Security Assertion Markup Language (SAML) geretourneerd door ACS tooyour toepassing [hoe tooview SAML geretourneerd door hello Azure Access Control Service][How tooview SAML returned by hello Azure Access Control Service]. toofurther verkennen van ACS-functionaliteit en tooexperiment met meer geavanceerde scenario's, Zie [Access Control Service 2.0][Access Control Service 2.0].

Ook in dit voorbeeld gebruikt Hallo **insluiten Hallo certificaat in het WAR-bestand Hallo** optie. Deze optie maakt het eenvoudig toodeploy Hallo certificaat. Desgewenst in plaats daarvan tookeep het handtekeningcertificaat gescheiden van het WAR-bestand, kunt u Hallo techniek te volgen:

1. Binnen Hallo **beveiliging** sectie Hallo **Azure Access Control-servicefilter** dialoogvenster, type **${env. JAVA_HOME}/mycert.cer** en schakelt u **insluiten Hallo certificaat in het WAR-bestand Hallo**. (Mijncert.cer aanpassen als de naam van uw certificaat verschilt.) Klik op **voltooien** tooclose Hallo dialoogvenster.
2. Kopiëren Hallo certificaat als onderdeel van uw implementatie: vouw In Projectverkenner van Eclipse **MyAzureACSProject**, met de rechtermuisknop op **WorkerRole1**, klikt u op **eigenschappen** , vouw **Azure rol**, en klik op **onderdelen**.
3. Klik op **Add**.
4. Binnen Hallo **onderdeel toevoegen** dialoogvenster:
   
   1. In Hallo **importeren** sectie:
      1. Gebruik Hallo **bestand** knop toonavigate toohello certificaat dat u wilt toouse. 
      2. Voor **methode**, selecteer **kopie**.
   2. Voor **als naam**, klik op Hallo tekstvak in en accepteer de standaardnaam Hallo.
   3. In Hallo **implementeren** sectie:
      1. Voor **methode**, selecteer **kopie**.
      2. Voor **toodirectory**, type **% JAVA_HOME %**.
   4. Uw **onderdeel toevoegen** dialoogvenster ziet er vergelijkbare toohello volgende.
      
       ![Certificaatonderdeel toevoegen][add_cert_component]
   5. Klik op **OK**.

Op dit moment zou uw certificaat worden opgenomen in uw implementatie. Ongeacht of u insluiten Hallo certificaat Hallo WAR-bestand of toevoegen als een onderdeel tooyour-implementatie, u moet tooupload Hallo certificaat tooyour naamruimte zoals beschreven in Hallo [uploaden van een certificaat tooyour ACS-naamruimte] [ Upload a certificate tooyour ACS namespace] sectie.

[What is ACS?]: #what-is
[Concepts]: #concepts
[Prerequisites]: #pre
[Create a Java web application]: #create-java-app
[Create an ACS Namespace]: #create-namespace
[Add Identity Providers]: #add-IP
[Add a Relying Party Application]: #add-RP
[Create Rules]: #create-rules
[Upload a certificate tooyour ACS namespace]: #upload-certificate
[Review hello Application Integration Page]: #review-app-int
[Configure Trust between ACS and Your ASP.NET Web Application]: #config-trust
[Add hello ACS Filter library tooyour application]: #add_acs_filter_library
[Deploy toohello compute emulator]: #deploy_compute_emulator
[Deploy tooAzure]: #deploy_azure
[Next steps]: #next_steps
[project website]: http://wastarterkit4java.codeplex.com/releases/view/61026
[How tooview SAML returned by hello Azure Access Control Service]: active-directory-java-view-saml-returned-by-access-control.md
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[Windows Identity Foundation]: http://www.microsoft.com/download/en/details.aspx?id=17331
[Windows Identity Foundation SDK]: http://www.microsoft.com/download/en/details.aspx?id=4451
[Azure Management Portal]: https://manage.windowsazure.com
[acs_flow]: ./media/active-directory-java-authenticate-users-access-control-eclipse/ACSFlow.png

<!-- Eclipse-specific -->
[add_acs_filter_lib]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibrary.png
[add_acs_filter_lib_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibraryEmulator.png
[add_acs_filter_lib_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibraryProduction.png

[relying_party_realm_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyRealmEmulator.png
[relying_party_return_url_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyReturnURLEmulator.png
[relying_party_realm_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyRealmProduction.png
[relying_party_return_url_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyReturnURLProduction.png
[add_cert_component]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddCertificateComponent.png
[add_jsp_file_acs]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddJSPFileACS.png
[create_acs_hello_world]: ./media/active-directory-java-authenticate-users-access-control-eclipse/CreateACSHelloWorld.png
[add_token_signing_cert]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddTokenSigningCertificate.png

