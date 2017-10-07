---
title: aaaITSM verbindingen in OMS IT Service Management-Connector | Microsoft Docs
description: Verbinding maken met uw ITSM producten/services met IT Service Management-Connector in OMS toocentrally bewaken en beheren van Hallo ITSM werkitems.
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 8231b7ce-d67f-4237-afbf-465e2e397105
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2017
ms.author: v-jysur
ms.openlocfilehash: 53ef51bf75fb8ed15ea3ce5072d9365c221f9f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-itsm-productsservices-with-it-service-management-connector-preview"></a>Verbinding maken met ITSM producten/services met IT Service Management-Connector (Preview)
In dit artikel bevat informatie over het tooconnect uw ITSM product of dienst tooIT Service Management-Connector in OMS en centraal beheren van uw werkitems. Zie voor meer informatie over IT Service Management-Connector [overzicht](log-analytics-itsmc-overview.md).

Hallo na producten of diensten die worden ondersteund:

- [System Center Service Manager](#connect-system-center-service-manager-to-it-service-management-connector-in-oms)
- [ServiceNow](#connect-servicenow-to-it-service-management-connector-in-oms)
- [Provance](#connect-provance-to-it-service-management-connector-in-oms)
- [Cherwell](#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="connect-system-center-service-manager-tooit-service-management-connector-in-oms"></a>Verbinding maken met System Center Service Manager tooIT Service Management-Connector in OMS

Hallo volgende secties bevatten informatie over het tooconnect uw System Center Service Manager product toohello IT Service Management-Connector in OMS.

### <a name="prerequisites"></a>Vereisten

Controleer of er Hallo volgen de vereisten is voldaan:

- IT-Service Management-Connector is geïnstalleerd.
Meer informatie: [configuratie](log-analytics-itsmc-overview.md#configuration).
- Hallo Service Manager-webtoepassing (Web-app) is geïmplementeerd en geconfigureerd. Informatie over Web-app is [hier](#create-and-deploy-service-manager-web-app-service).
- Hybride verbinding gemaakt en geconfigureerd. Meer informatie: [configureren Hallo hybride verbinding](#configure-the-hybrid-connection).
- Ondersteunde versies van Service Manager: 2012 R2 of 2016.
- Gebruikersrol: [geavanceerde operator](https://technet.microsoft.com/library/ff461054.aspx).

### <a name="connection-procedure"></a>Verbindingsprocedure

Hallo te volgen procedure tooconnect uw System Center Service Manager exemplaar toohello IT Service Management-Connector gebruikt:

1. Ga te**OMS** >**instellingen** > **verbonden bronnen**.
2. Selecteer **ITSM Connector** klikt u op **nieuwe verbinding toevoegen**.

    ![Servicemanager ](./media/log-analytics-itsmc/itsmc-service-manager-connection.png)
3. Geef informatie op Hallo zoals beschreven in de volgende tabel Hallo en klik op **opslaan** toocreate Hallo verbinding:

> [!NOTE]
> Alle volgende parameters zijn verplicht.

| **Veld** | **Beschrijving** |
| --- | --- |
| **Naam**   | Typ een naam voor Hallo System Center Service Manager-exemplaar dat u wilt dat tooconnect Hello IT Service Management-Connector.  U gebruikt deze naam later wanneer u werkitems in dit exemplaar te configureren / gedetailleerde logboekanalyse bekijken. |
| **Selecteer het type verbinding**   | Selecteer **System Center Service Manager**. |
| **Server-URL**   | Typ de URL Hallo Hallo Service Manager-Web-app. Meer informatie over Service Manager-Web-app is [hier](#create-and-deploy-service-manager-web-app-service).
| **Client-ID**   | Typ Hallo client-ID gegenereerd u (met behulp van automatische script Hallo) voor het verifiëren van Hallo Web-app. Meer informatie over automatische Hallo script [hier.](log-analytics-itsmc-service-manager-script.md)|
| **Clientgeheim**   | Type Hallo clientgeheim, gegenereerd voor deze ID.   |
| **Gegevens synchroniseren bereik**   | Selecteer Hallo Service Manager-werkitems die u wilt dat toosync via Hallo IT Service Management-Connector.  Deze items worden geïmporteerd in logboekanalyse werk. **Opties:** incidenten, wijzigingsaanvragen.|
| **Gegevens synchroniseren** | Typ Hallo aantal voorbije dagen gewenste Hallo gegevens uit. **Maximum aantal**: 120 dagen. |
| **Nieuw configuratie-item maken in ITSM oplossing** | Selecteer deze optie als u wilt dat toocreate Hallo configuratie-items in Hallo ITSM product. Wanneer u selecteert, maakt OMS Hallo van invloed op een configuratie-items als configuratie-items (in geval van een niet-bestaande configuratie-items) in Hallo ITSM systeem ondersteund. **Standaard**: uitgeschakeld. |

Wanneer er verbinding gemaakt en gesynchroniseerd:

- Geselecteerde werkitems van Service Manager worden geïmporteerd in OMS **logboekanalyse.** U kunt Hallo overzicht van deze werkitems op Hallo IT Service Management-Connector tegel.

- Van OMS, kunt u incidenten van OMS waarschuwingen of van de zoekopdracht op logboek in deze Service Manager-instantie.

Meer informatie: [werkitems ITSM maken voor OMS waarschuwingen](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) en [ITSM maken werkitems uit logboeken van OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

### <a name="create-and-deploy-service-manager-web-app-service"></a>Maken en implementeren van Service Manager web-app service

tooconnect Hallo lokale Service Manager Hello IT Service Management-Connector op OMS, Microsoft heeft een Service Manager-Web-app gemaakt op Hallo GitHub.

tooset van Hallo ITSM Web-app voor uw Service Manager Hallo te volgen:

- **Hallo Web-app implementeren** : Hallo Web-app implementeren, Hallo-eigenschappen worden ingesteld en verifiëren met Azure AD. U Hallo web-app kunt implementeren met behulp van Hallo [script geautomatiseerde](log-analytics-itsmc-service-manager-script.md) dat Microsoft u heeft gekregen.
- **Configureer de Hallo hybride verbinding** - [configureren van deze verbinding](#configure-the-hybrid-connection)handmatig.

#### <a name="deploy-hello-web-app"></a>Hallo-web-app implementeren
Gebruik Hallo geautomatiseerde [script](log-analytics-itsmc-service-manager-script.md) toodeploy Web-app Hallo Hallo-eigenschappen worden ingesteld en verifiëren met Azure AD.

Hallo-script uitvoeren door te geven Hallo vereiste gegevens te volgen:

- Details van de Azure-abonnement
- De naam van resourcegroep
- Locatie
- Details van Service Manager-server (server name, domein, gebruikersnaam en wachtwoord)
- Site-voorvoegsel voor uw Web-app
- Service Bus-Namespace.

Hallo script maakt Hallo Web-app met Hallo-naam die u hebt opgegeven (samen met enkele extra tekenreeksen toomake deze unieke). Hallo genereert **Web-app-URL**, **client-ID** en **clientgeheim**.

Sla het Hallo-waarden, u deze gebruiken wanneer u een verbinding met de IT-Service Management-Connector maakt.

**Hallo Web-app-installatie controleren**

1. Ga te**Azure-portal** > **Resources**.
2. Hallo-Web-app selecteren, klikt u op **instellingen** > **toepassingsinstellingen**.
3. Bevestig Hallo informatie over Hallo Service Manager-instantie die u hebt opgegeven tijdens het Hallo voor het implementeren van Hallo app via Hallo script.

### <a name="configure-hello-hybrid-connection"></a>Hallo hybride verbinding configureren

Gebruik hello te volgen procedure tooconfigure Hallo hybride verbinding Service Manager-instantie Hallo Hello IT Service Management-Connector in OMS tussen.

1. Hallo Service Manager-Web-app onder zoeken **Azure-Resources**.
2. Klik op **instellingen** > **Networking**.
3. Onder **hybride verbindingen**, klikt u op **uw hybride-verbindingseindpunten configureren**.

    ![Netwerken voor hybride verbinding](./media/log-analytics-itsmc/itsmc-hybrid-connection-networking-and-end-points.png)
4. In Hallo **hybride verbindingen** blade, klikt u op **hybride verbinding toevoegen**.

    ![Hybride verbinding toevoegen](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-add.png)

5. In Hallo **hybride verbindingen toevoegen** blade, klikt u op **maken nieuwe hybride verbinding**.

    ![Nieuwe hybride verbinding](./media/log-analytics-itsmc/itsmc-create-new-hybrid-connection.png)

6. Type Hallo volgende waarden:

    - **Eindpuntnaam**: Geef een naam voor het nieuwe hybride verbinding Hallo.
    -  **Eindpunt Host**: FQDN-naam van Hallo Service Manager-beheerserver.
    - **Eindpuntpoort**: Typ 5724
    - **Service Bus-naamruimte**: gebruik een bestaande service bus-naamruimte of een nieuwe maken.
    - **Locatie**: Hallo locatie selecteren.
    -  **Naam**: Geef een naam toohello servicebus als u deze maakt.

    ![Waarden voor hybride verbinding](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-values.png)
6. Klik op **OK** tooclose hello **hybride verbinding maken** blade en Hallo hybride verbinding hebt gemaakt.

    Zodra Hallo hybride verbinding is gemaakt, wordt dit weergegeven onder het Hallo-blade.

7. Nadat Hallo hybride verbinding is gemaakt, selecteert u Hallo verbinding en klikt u op **toevoegen geselecteerd hybride verbinding**.

    ![Nieuwe hybride verbinding](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-added.png)

#### <a name="configure-hello-listener-setup"></a>Hallo-listener-instellingen configureren

Hallo te volgen procedure tooconfigure Hallo-listener-instellingen voor Hallo hybride verbinding gebruiken.

1. In Hallo **hybride verbindingen** blade, klikt u op **downloaden Hallo Verbindingsbeheer** en installeer deze op Hallo-computer waarop een exemplaar van System Center Service Manager wordt uitgevoerd.

    Wanneer Hallo-installatie voltooid is, **hybride Verbindingsbeheer UI** optie is beschikbaar onder **Start** menu.

2. Klik op **hybride Verbindingsbeheer UI** , wordt u gevraagd om uw Azure-referenties.

3. Meld u aan met uw Azure-referenties en selecteer uw abonnement waarin Hallo hybride verbinding is gemaakt.

4. Klik op **Opslaan**.

Uw hybride verbinding is verbonden.

![geslaagde hybride verbinding](./media/log-analytics-itsmc/itsmc-hybrid-connection-listener-set-up-successful.png)
> [!NOTE]

> Nadat Hallo hybride verbinding is gemaakt, controleren en Hallo testverbinding via Hallo Service Manager-Web-app geïmplementeerd. Zorg ervoor dat Hallo verbinding is geslaagd voordat u tooconnect toohello IT Service Management-Connector in OMS probeert.

Hallo toont volgende afbeelding Hallo details van de verbinding is geslaagd:

![Hybride verbinding testen](./media/log-analytics-itsmc/itsmc-hybrid-connection-test.png)

## <a name="connect-servicenow-tooit-service-management-connector-in-oms"></a>Verbinding maken tussen ServiceNow tooIT Service Management-Connector in OMS

Hallo volgende secties bevatten informatie over het tooconnect uw ServiceNow product toohello IT Service Management-Connector in OMS.

### <a name="prerequisites"></a>Vereisten

Controleer of er Hallo volgen de vereisten is voldaan:

- IT-Service Management-Connector is geïnstalleerd. Meer informatie: [configuratie.](log-analytics-itsmc-overview.md#configuration)
- ServiceNow versies – Fuji, Geneva, Helsinki ondersteund.

ServiceNow Admins moet doen Hallo in hun ServiceNow-exemplaar te volgen:
- Client-ID en clientgeheim voor Hallo ServiceNow product genereren. Voor informatie over hoe toogenerate client-ID en geheim, Zie [OAuth-installatie](http://wiki.servicenow.com/index.php?title=OAuth_Setup).
- Installeer Hallo App gebruiker voor Microsoft OMS-integratie (ServiceNow-app). [Meer informatie](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0 ).
- De gebruikersrol integratie voor Hallo gebruiker app geïnstalleerd maken. Informatie over hoe toocreate Hallo integratie-gebruikersrol is [hier](#create-integration-user-role-in-servicenow-app).


### <a name="connection-procedure"></a>**Verbindingsprocedure**

Hallo te volgen procedure toocreate een ServiceNow-verbinding gebruikt:

1. Ga te**OMS** > **instellingen** > **verbonden bronnen**.
2. Selecteer **ITSM Connector** klikt u op **nieuwe verbinding toevoegen**.

    ![ServiceNow-verbinding](./media/log-analytics-itsmc/itsmc-servicenow-connection.png)

3. Geef informatie op Hallo zoals beschreven in de volgende tabel Hallo en klik op **opslaan** toocreate Hallo verbinding:

> [!NOTE]
> Alle volgende parameters zijn verplicht.

| **Veld** | **Beschrijving** |
| --- | --- |
| **Naam**   | Typ een naam voor Hallo ServiceNow-exemplaar dat u wilt dat tooconnect Hello IT Service Management-Connector.  U gebruikt deze naam verderop in OMS wanneer u werkitems in deze ITSM configureren / gedetailleerde logboekanalyse bekijken. |
| **Selecteer het type verbinding**   | Selecteer **ServiceNow**. |
| **Gebruikersnaam**   | Typ de gebruikersnaam van het Hallo-integratie die u hebt gemaakt in Hallo ServiceNow app toosupport Hallo verbinding toohello IT Service Management-Connector. Meer informatie: [gebruikersrol maken tussen ServiceNow-app](#create-integration-user-role-in-servicenow-app).|
| **Wachtwoord**   | Typ het wachtwoord Hallo die zijn gekoppeld aan deze gebruikersnaam. **Opmerking**: gebruikersnaam en wachtwoord voor het genereren van verificatietokens alleen worden gebruikt, en worden niet overal opgeslagen in Hallo OMS-service.  |
| **Server-URL**   | Typ de URL Hallo van Hallo ServiceNow-exemplaar dat u wilt dat tooconnect tooIT Service Management-Connector. |
| **Client-ID**   | Typ Hallo client-ID die u wilt dat toouse voor OAuth2-authenticatie, wat u eerder hebt gegenereerd.  Meer informatie over het genereren van client-ID en geheim: [OAuth-installatie](http://wiki.servicenow.com/index.php?title=OAuth_Setup). |
| **Clientgeheim**   | Type Hallo clientgeheim, gegenereerd voor deze ID.   |
| **Gegevens synchroniseren bereik**   | Selecteer Hallo ServiceNow-werkitems die u wilt dat toosync tooOMS, via Hallo IT Service Management-Connector.  Hallo geselecteerd waarden worden geïmporteerd in logboekanalyse.   **Opties:** incidenten en wijzigingsaanvragen.|
| **Gegevens synchroniseren** | Typ Hallo aantal voorbije dagen gewenste Hallo gegevens uit. **Maximum aantal**: 120 dagen. |
| **Nieuw configuratie-item maken in ITSM oplossing** | Selecteer deze optie als u wilt dat toocreate Hallo configuratie-items in Hallo ITSM product. Wanneer u selecteert, maakt OMS Hallo van invloed op een configuratie-items als configuratie-items (in geval van een niet-bestaande configuratie-items) in Hallo ITSM systeem ondersteund. **Standaard**: uitgeschakeld. |


Wanneer er verbinding gemaakt en gesynchroniseerd:

- Werk items uit ServiceNow-verbinding worden geïmporteerd in de OMS-logboekanalyse geselecteerd.  U kunt Hallo overzicht van deze werkitems op Hallo IT Service Management-Connector tegel.
- U kunt de incidenten, waarschuwingen en gebeurtenissen van OMS waarschuwingen of logboek zoeken in dit ServiceNow-exemplaar maken.  


Meer informatie: [werkitems ITSM maken voor OMS waarschuwingen](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) en [ITSM maken werkitems uit logboeken van OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

### <a name="create-integration-user-role-in-servicenow-app"></a>Integratie-gebruikersrol in ServiceNow-app maken

Gebruiker Hallo procedure te volgen:

1.  Bezoek Hallo [ServiceNow store](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0) en installeer Hallo **gebruiker-App voor ServiceNow en Microsoft OMS-integratie** naar uw ServiceNow-exemplaar.
2.  Ga naar links navigatiebalk van Hallo ServiceNow-exemplaar, zoeken en selecteer Microsoft OMS integrator Hallo na de installatie.  
3.  Klik op **controlelijst voor de installatie**.

    Hallo-status wordt weergegeven als **niet voltooien** als Hallo gebruikersrol is nog toobe gemaakt.

4.  In de tekst hello vakken, naast te**integratie van de gebruiker**, geef de gebruikersnaam Hallo voor Hallo-gebruiker die verbinding van toohello IT Service Management-Connector in OMS maken kan.
5.  Hallo wachtwoord invoeren voor deze gebruiker en klikt u op **OK**.  

>[!NOTE]

> U gebruikt deze referenties toomake hello ServiceNow-verbinding in OMS.

Hallo nieuw aangemaakte gebruiker weergegeven met de Hallo standaardrollen toegewezen.

Standaardrollen:
- personalize_choices
- import_transformer
-   x_mioms_microsoft.User
-   ITIL
-   template_editor
-   view_changer

Als de gebruiker Hallo is gemaakt, de status van Hallo **controlelijst voor de installatie controleren** tooCompleted, Hallo details van Hallo gebruikersrol is gemaakt voor Hallo app van de aanbieding wordt verplaatst.

> [!NOTE]

> een gebruiker toocreate tooallow **waarschuwingen** en **gebeurtenissen** in ServiceNow van OMS:

> - Zorg ervoor dat er Hallo gebeurtenis Management-module geïnstalleerd op uw ServiceNow-exemplaar.

> - Hallo na rollen toohello integration-gebruiker toevoegen:
>      - evt_mgmt_integration
>      - evt_mgmt_operator  


## <a name="connect-provance-tooit-service-management-connector-in-oms"></a>Verbinding maken met Provance tooIT Service Management-Connector in OMS

Hallo volgende secties bevatten informatie over het tooconnect uw Provance product toohello IT Service Management-Connector in OMS.

### <a name="prerequisites"></a>Vereisten

Controleer of er Hallo volgen de vereisten is voldaan:

- IT-Service Management-Connector is geïnstalleerd. Meer informatie: [configuratie](log-analytics-itsmc-overview.md#configuration).
- Provance App moet worden geregistreerd met Azure AD - en client-ID beschikbaar wordt gesteld. Zie voor gedetailleerde informatie [hoe tooconfigure active directory-verificatie](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).
- Gebruikersrol: beheerder.

### <a name="connection-procedure"></a>Verbindingsprocedure

Hallo te volgen procedure toocreate Provance verbinding gebruiken:

1. Ga te**OMS** > **instellingen** > **verbonden bronnen**.
2. Selecteer **ITSM Connector** klikt u op **nieuwe verbinding toevoegen**.  

    ![Provance verbinding](./media/log-analytics-itsmc/itsmc-provance-connection.png)
3. Geef informatie op Hallo zoals beschreven in de volgende tabel Hallo en klik op **opslaan** toocreate Hallo verbinding.

> [!NOTE]
> Alle volgende parameters zijn verplicht.

| **Veld** | **Beschrijving** |
| --- | --- |
| **Naam**   | Typ een naam voor Hallo Provance-exemplaar dat u wilt dat tooconnect Hello IT Service Management-Connector.  U gebruikt deze naam verderop in OMS wanneer u werkitems in deze ITSM configureren / gedetailleerde logboekanalyse bekijken. |
| **Selecteer het type verbinding**   | Selecteer **Provance**. |
| **Gebruikersnaam**   | Typ de gebruikersnaam Hallo die verbinding van toohello IT Service Management-Connector maken kan.    |
| **Wachtwoord**   | Typ het wachtwoord Hallo die zijn gekoppeld aan deze gebruikersnaam. **Opmerking:** gebruikersnaam en wachtwoord voor het genereren van verificatietokens alleen worden gebruikt, en worden niet overal opgeslagen in de OMS-service Hallo. _|
| **Server-URL**   | Typ Hallo-URL van uw Provance-exemplaar dat u wilt dat tooconnect tooIT Service Management-Connector. |
| **Client-ID**   | Type Hallo client-ID voor het verifiëren van deze verbinding die u in uw exemplaar Provance gegenereerd.  Zie voor meer informatie over client-ID [hoe tooconfigure active directory-verificatie](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). |
| **Gegevens synchroniseren bereik**   | Selecteer Hallo Provance work items die u wilt dat toosync tooOMS, via Hallo IT Service Management-Connector.  Deze items worden geïmporteerd in logboekanalyse werk.   **Opties:** incidenten, wijzigingsaanvragen.|
| **Gegevens synchroniseren** | Typ Hallo aantal voorbije dagen gewenste Hallo gegevens uit. **Maximum aantal**: 120 dagen. |
| **Nieuw configuratie-item maken in ITSM oplossing** | Selecteer deze optie als u wilt dat toocreate Hallo configuratie-items in Hallo ITSM product. Wanneer u selecteert, maakt OMS Hallo van invloed op een configuratie-items als configuratie-items (in geval van een niet-bestaande configuratie-items) in Hallo ITSM systeem ondersteund. **Standaard**: uitgeschakeld.|

Wanneer er verbinding gemaakt en gesynchroniseerd:

- Geselecteerde werkitems van Provance verbinding worden geïmporteerd in OMS **logboekanalyse.**  U kunt Hallo overzicht van deze werkitems op Hallo IT Service Management-Connector tegel.
- U kunt incidenten en gebeurtenissen van OMS waarschuwingen of logboek zoeken in dit exemplaar Provance maken.

Meer informatie: [werkitems ITSM maken voor OMS waarschuwingen](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) en [ITSM maken werkitems uit logboeken van OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

## <a name="connect-cherwell-tooit-service-management-connector-in-oms"></a>Verbinding maken met Cherwell tooIT Service Management-Connector in OMS

Hallo volgende secties bevatten informatie over het tooconnect uw Cherwell product toohello IT Service Management-Connector in OMS.

### <a name="prerequisites"></a>Vereisten

Controleer of er Hallo volgen de vereisten is voldaan:

- IT-Service Management-Connector is geïnstalleerd. Meer informatie: [configuratie](log-analytics-itsmc-overview.md#configuration).
- Client-ID gegenereerd. Meer informatie: [client-ID genereren voor Cherwell](#generate-client-id-for-cherwell).
- Gebruikersrol: beheerder.

### <a name="connection-procedure"></a>Verbindingsprocedure

Hallo te volgen procedure toocreate Cherwell verbinding gebruiken:

1. Ga te**OMS** >  **instellingen** > **verbonden bronnen**.
2. Selecteer **ITSM Connector** klikt u op **nieuwe verbinding toevoegen**.  

    ![Cherwell gebruikers-id](./media/log-analytics-itsmc/itsmc-cherwell-connection.png)

3. Geef informatie op Hallo zoals beschreven in de volgende tabel Hallo en klik op **opslaan** toocreate Hallo verbinding.

> [!NOTE]
> Alle volgende parameters zijn verplicht.

| **Veld** | **Beschrijving** |
| --- | --- |
| **Naam**   | Typ een naam voor Hallo Cherwell-exemplaar dat u wilt dat tooconnect toohello IT Service Management-Connector.  U gebruikt deze naam verderop in OMS wanneer u werkitems in deze ITSM configureren / gedetailleerde logboekanalyse bekijken. |
| **Selecteer het type verbinding**   | Selecteer **Cherwell.** |
| **Gebruikersnaam**   | Typ de gebruikersnaam van het Hallo-Cherwell die verbinding van toohello IT Service Management-Connector maken kan. |
| **Wachtwoord**   | Typ het wachtwoord Hallo die zijn gekoppeld aan deze gebruikersnaam. **Opmerking:** gebruikersnaam en wachtwoord voor het genereren van verificatietokens alleen worden gebruikt, en worden niet overal opgeslagen in Hallo OMS-service.|
| **Server-URL**   | Typ Hallo-URL van uw Cherwell-exemplaar dat u wilt dat tooconnect tooIT Service Management-Connector. |
| **Client-ID**   | Type Hallo client-ID voor het verifiëren van deze verbinding die u in uw exemplaar Cherwell gegenereerd.   |
| **Gegevens synchroniseren bereik**   | Selecteer Hallo Cherwell work items die u wilt dat toosync via Hallo IT Service Management-Connector.  Deze items worden geïmporteerd in logboekanalyse werk.   **Opties:** incidenten, wijzigingsaanvragen. |
| **Gegevens synchroniseren** | Typ Hallo aantal voorbije dagen gewenste Hallo gegevens uit. **Maximum aantal**: 120 dagen. |
| **Nieuw configuratie-item maken in ITSM oplossing** | Selecteer deze optie als u wilt dat toocreate Hallo configuratie-items in Hallo ITSM product. Wanneer u selecteert, maakt OMS Hallo van invloed op een configuratie-items als configuratie-items (in geval van een niet-bestaande configuratie-items) in Hallo ITSM systeem ondersteund. **Standaard**: uitgeschakeld. |

Wanneer er verbinding gemaakt en gesynchroniseerd:

- Werk items uit deze verbinding Cherwell worden geïmporteerd in de OMS-logboekanalyse geselecteerd. U kunt Hallo overzicht van deze werkitems op Hallo IT Service Management-Connector tegel.
- U kunt maken van incidenten en gebeurtenissen in dit exemplaar Cherwell van OMS. Meer informatie: maken ITSM werkitems voor OMS-waarschuwingen en ITSM maken werkitems uit logboeken van OMS.

Meer informatie: [werkitems ITSM maken voor OMS waarschuwingen](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) en [ITSM maken werkitems uit logboeken van OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

### <a name="generate-client-id-for-cherwell"></a>Client-ID voor Cherwell genereren

toogenerate Hallo van client-ID/sleutel voor Cherwell, gebruikt u Hallo procedure te volgen:

1. Meld u aan tooyour Cherwell exemplaar als beheerder.
2. Klik op **beveiliging** > **bewerken REST-API-clientinstellingen**.
3. Selecteer **maken nieuwe client** > **clientgeheim**.

    ![Cherwell gebruikers-id](./media/log-analytics-itsmc/itsmc-cherwell-client-id.png)


## <a name="next-steps"></a>Volgende stappen
 - [Werkitems ITSM voor OMS waarschuwingen maken](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts)

 - [Maken van werkitems ITSM van OMS-Logboeken](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)

- [Logboekanalyse weergave voor de verbinding](log-analytics-itsmc-overview.md#using-the-solution)
