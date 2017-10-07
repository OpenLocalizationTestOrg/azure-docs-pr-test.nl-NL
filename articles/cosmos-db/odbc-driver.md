---
title: aaaConnect tooAzure Cosmos DB met BI-hulpprogramma's voor webanalyse | Microsoft Docs
description: Meer informatie over hoe toouse hello Azure Cosmos DB ODBC-stuurprogramma toocreate tabellen en weergaven zodat genormaliseerde gegevens kunnen worden weergegeven in de BI- en gegevens analytics-software.
keywords: ODBC, odbc-stuurprogramma
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 9967f4e5-4b71-4cd7-8324-221a8c789e6b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.openlocfilehash: e12a70f7805445f09fac01411e4bfbccc9a29c7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-cosmos-db-using-bi-analytics-tools-with-hello-odbc-driver"></a>Verbinding maken met tooAzure Cosmos DB met BI-hulpprogramma's voor webanalyse met Hallo ODBC-stuurprogramma

Hello Azure Cosmos DB ODBC-stuurprogramma schakelt u tooconnect tooAzure Cosmos DB met BI analytics tools zoals SQL Server Integration Services-, Power BI Desktop- en Tableau zodat u kunt analyseren en visualisaties van uw Azure DB die Cosmos-gegevens in die maken oplossingen.

Hello Azure Cosmos DB ODBC-stuurprogramma ODBC 3.8 compatibel is en de syntaxis van de ANSI SQL-92 ondersteunt. Hallo stuurprogramma biedt uitgebreide functies toohelp renormalize van gegevens in Azure Cosmos DB. Hallo stuurprogramma gebruikt, kunt u gegevens in Azure Cosmos DB als tabellen en weergaven weergeven. Hallo stuurprogramma stelt u de SQL-bewerkingen tooperform tegen Hallo-tabellen en weergaven met inbegrip van de group by-query's, invoeg-, updates en verwijderingen.

## <a name="why-do-i-need-toonormalize-my-data"></a>Waarom moet ik toonormalize mijn gegevens?
Azure Cosmos-database is een database zonder, zodat snelle ontwikkeling van apps door in te schakelen tooiterate toepassingen kunnen hun gegevens model op Hallo snel en niet beperken ze tooa strikte schema. Eén Azure DB die Cosmos-database kan de JSON-documenten van verschillende structuren bevatten. Dit is ideaal voor snelle ontwikkeling van toepassingen, maar wanneer u wilt dat tooanalyze en rapporten van uw gegevens met behulp van gegevensanalyse en BI-hulpprogramma's maken, Hallo gegevens vaak moet toobe afgevlakt en specifieke schema tooa voldoen.

Dit is waar Hallo ODBC-stuurprogramma wordt geleverd. Hallo ODBC-stuurprogramma gebruikt, kunt u nu gegevens in Azure Cosmos DB in tabellen en weergaven aanpassen tooyour gegevens analyse- en renormalized moet. Hallo renormalized schema's hebben geen invloed op de onderliggende gegevens Hallo en ontwikkelaars tooadhere toothem niet wilt beperken, ze gewoon u tooleverage ODBC compatibele extra tooaccess Hallo gegevens inschakelen. Nu wordt uw Azure DB die Cosmos-database niet alleen een favoriet voor uw ontwikkelteam, maar uw gegevensanalisten wordt de evaluatieversie te.

Nu kunt aan de slag met Hallo ODBC-stuurprogramma.

## <a id="install"></a>Stap 1: Installeer hello Azure Cosmos DB ODBC-stuurprogramma

1. Hallo-stuurprogramma's voor uw omgeving downloaden:

    * [Microsoft Azure DB Cosmos ODBC-64-bit.msi](https://aka.ms/documentdb-odbc-64x64) voor 64-bits Windows
    * [Microsoft Azure DB Cosmos ODBC 32 x 64-bit.msi](https://aka.ms/documentdb-odbc-32x64) voor 32-bits op 64-bits Windows
    * [Microsoft Azure DB Cosmos ODBC 32 bit.msi](https://aka.ms/documentdb-odbc-32x32) voor 32-bits Windows

    Voer Hallo msi-bestand lokaal, welke hello wordt gestart **Azure Cosmos DB ODBC-stuurprogramma Wizard installatie van Microsoft**. 
2. Voltooi de installatiewizard Hallo Hallo standaard invoer tooinstall Hallo ODBC-stuurprogramma.
3. Open Hallo **ODBC-gegevensbron beheerder** app op uw computer, u kunt dit doen door typen **ODBC-gegevensbronnen** in Windows hello het zoekvak. 
    U kunt bevestigen Hallo-stuurprogramma is geïnstalleerd door te klikken op Hallo **stuurprogramma's** tabblad en ervoor te zorgen **Microsoft Azure Cosmos DB ODBC-stuurprogramma** wordt vermeld.

    ![Azure Cosmos DB-gegevensbron](./media/odbc-driver/odbc-driver.png)

## <a id="connect"></a>Stap 2: Verbinding maken met tooyour Azure DB die Cosmos-database

1. Na [installeren hello Azure Cosmos DB ODBC-stuurprogramma](#install), in Hallo **ODBC Data Source Administrator** venster, klikt u op **toevoegen**. U kunt een gebruiker of systeem-DSN maken. In dit voorbeeld maakt u een gebruikers-DSN.
2. In Hallo **nieuwe gegevensbron maken** Selecteer **DB ODBC-stuurprogramma van Microsoft Azure Cosmos**, en klik vervolgens op **voltooien**.
3. In Hallo **Azure Cosmos DB ODBC-stuurprogramma SDN Setup** venster invullen Hallo volgende: 

    ![Azure Cosmos DB ODBC-stuurprogramma DSN instellingen venster](./media/odbc-driver/odbc-driver-dsn-setup.png)
    - **Naam van de gegevensbron**: uw eigen beschrijvende naam voor Hallo ODBC DSN. Deze naam uniek tooyour Azure DB die Cosmos-account is, dus op de juiste wijze name als u meerdere accounts hebt.
    - **Beschrijving**: een korte beschrijving van het Hallo-gegevensbron.
    - **Host**: URI voor uw Azure DB die Cosmos-account. U kunt dit ophalen uit de blade van de hello Azure Cosmos DB sleutels in hello Azure-portal, zoals wordt weergegeven in de volgende schermafbeelding Hallo. 
    - **Toegangstoets**: Hallo primaire of secundaire, alleen-lezen of alleen-lezen sleutel uit hello Azure Cosmos DB sleutels blade in hello Azure-portal, zoals wordt weergegeven in de volgende schermafbeelding Hallo. U wordt aangeraden gebruik Hallo alleen-lezen sleutel als Hallo DSN-naam wordt gebruikt voor het kenmerk alleen-lezen gegevensverwerking en rapportage.
    ![Blade van Azure Cosmos DB sleutels](./media/odbc-driver/odbc-driver-keys.png)
    - **Versleutelen van de toegangssleutel voor**: Selecteer de beste keuze Hallo op basis van gebruikers van deze machine Hallo. 
4. Klik op Hallo **Test** knop toomake zeker dat u verbinding kunt maken met tooyour Azure DB die Cosmos-account. 
5. Klik op **geavanceerde opties** en set Hallo de volgende waarden:
    - **Query uitvoeren op consistentie**: Selecteer Hallo [consistentieniveau](consistency-levels.md) voor uw doeleinden. Hallo standaard wordt de sessie.
    - **Aantal nieuwe pogingen**: Geef het aantal keren Hallo tooretry een bewerking als de eerste aanvraag Hallo vanwege tooservice beperking niet wordt voltooid.
    - **Schemabestand**: U hebt een aantal opties hier.
        - Als u deze vermelding (leeg) is standaard scant Hallo stuurprogramma Hallo eerste paginagegevens voor alle verzamelingen toodetermine Hallo schema met elke verzameling. Dit staat bekend als de toewijzing van de verzameling. Zonder een schemabestand dat is gedefinieerd, Hallo stuurprogramma tooperform Hallo scan voor elke sessie stuurprogramma is en kan leiden tot een hogere opstarttijd van een toepassing met Hallo DSN-naam. Het is raadzaam dat u altijd een schemabestand voor een DSN koppelen.
        - Als u al een schemabestand (mogelijk één die u hebt gemaakt met Hallo [Schema-Editor](#schema-editor)), klikt u op **Bladeren**, navigeer tooyour bestand, klik op **opslaan**, en klik vervolgens op **OK**.
        - Als u een nieuw schema toocreate wilt, klikt u op **OK**, en klik vervolgens op **Schema-Editor** in het hoofdvenster Hallo. Ga verder toohello [Schema-Editor](#schema-editor) informatie. Vergeet niet vorige toohello toogo bij het maken van nieuwe schemabestand Hallo **geavanceerde opties** schemabestand van venster tooinclude Hallo nieuw gemaakt.

6. Zodra u voltooien en Hallo sluit **Azure Cosmos DB ODBC-stuurprogramma DSN Setup** venster Hallo nieuwe gebruikers-DSN is toegevoegd toohello gebruiker DSN-tabblad.

    ![Nieuwe Azure Cosmos DB ODBC DSN-naam op Hallo gebruiker DSN-tabblad](./media/odbc-driver/odbc-driver-user-dsn.png)

## <a id="#collection-mapping"></a>Stap 3: Maak een schemadefinitie waarin toewijzingsmethode Hallo-verzameling

Er zijn twee soorten steekproeven methoden die u kunt gebruiken: **verzameling toewijzing** of **tabel scheidingstekens**. Een sessie steekproeven kan gebruikmaken van beide methoden steekproeven, maar elke verzameling kunt alleen een specifieke methode gebruiken. Hallo onderstaande stappen maken een schema voor Hallo gegevens in een of meer verzamelingen met Hallo verzameling toewijzingsmethode. Deze methode haalt gegevens op Hallo Hallo-pagina van een verzameling toodetermine Hallo structuur van Hallo-gegevens. Deze zet een verzameling tooa tabel op Hallo ODBC-zijde. Deze methode is snel en efficiënt wanneer Hallo-gegevens in een verzameling homogene. Als een verzameling heterogene type gegevens bevat, raden wij aan u Hallo [tabel scheidingstekens toewijzingsmethode](#table-mapping) aangezien deze een meer robuuste methode toodetermine Hallo gegevensstructuren in Hallo-verzameling biedt. 

1. Na het voltooien van stap 1 en 4 in [Connect tooyour Azure Cosmos DB database](#connect), klikt u op **Schema-Editor** in Hallo **Azure Cosmos DB ODBC-stuurprogramma DSN Setup** venster.

    ![Knop voor schema-editor in hello Azure Cosmos DB ODBC-stuurprogramma DSN Setup venster](./media/odbc-driver/odbc-driver-schema-editor.png)
2. In Hallo **Schema-Editor** venster, klikt u op **nieuw**.
    Hallo **Schema genereren** venster bevat alle Hallo verzamelingen in hello Azure DB die Cosmos-account. 
3. Selecteer een of meer verzamelingen toosample en klik vervolgens op **voorbeeld**. 
4. In Hallo **ontwerpweergave** tabblad, Hallo-database, schema en tabel worden weergegeven. In tabelweergave hello weergegeven Hallo scan Hallo set eigenschappen die zijn gekoppeld aan Hallo kolomnamen (SQL-naam, de naam van gegevensbron, enzovoort).
    Voor elke kolom, kunt u de kolomnaam SQL hello, Hallo SQL-type, SQL-lengte (indien van toepassing), schalen (indien van toepassing), Precision (indien van toepassing) en null-waarden bevatten.
    - U kunt instellen **kolom verbergen** te**true** desgewenst tooexclude die kolom van de queryresultaten. Kolommen kolom verbergen gemarkeerd = true niet worden geretourneerd voor de selectie en projectie, hoewel ze nog steeds deel van Hallo schema uitmaken. U kunt bijvoorbeeld alle hello Azure Cosmos DB vereiste eigenschappen beginnen met '_' verbergen.
    - Hallo **id** kolom Hallo enige veld dat kan niet worden verborgen, zoals het wordt gebruikt als primaire sleutel in het Hallo genormaliseerde schema Hallo is. 
5. Wanneer u klaar bent met het Hallo-schema definiëren, klikt u op **bestand** | **opslaan**, toohello directory toosave Hallo-schema te navigeren en klik op **opslaan**.

    Desgewenst in toekomstige Hallo toouse dit schema met een DSN hello Azure Cosmos DB ODBC-stuurprogramma DSN Setup venster (via een ODBC Data Source Administrator Hallo) openen, klikt u op Geavanceerde opties en navigeert u vervolgens in Hallo schemabestand vak toohello schema opgeslagen. Opslaan van een bestand schema tooan wijzigt bestaande DSN Hallo DSN verbinding tooscope toohello gegevens en de structuur gedefinieerd door het schema.

## <a id="table-mapping"></a>Stap 4: Een schemadefinitie waarin Hallo tabel-scheidingstekens maken toewijzingsmethode

Er zijn twee soorten steekproeven methoden die u kunt gebruiken: **verzameling toewijzing** of **tabel scheidingstekens**. Een sessie steekproeven kan gebruikmaken van beide methoden steekproeven, maar elke verzameling kunt alleen een specifieke methode gebruiken. 

Hallo volgende stappen maakt u een schema voor Hallo gegevens in een of meer verzamelingen met Hallo **tabel scheidingstekens** toewijzingsmethode. Het is raadzaam dat u deze methode gebruiken wanneer uw verzamelingen heterogene type gegevens bevatten. U kunt deze methode tooscope Hallo steekproef nemen tooa set kenmerken en de bijbehorende waarden. Bijvoorbeeld, als een document bevat een eigenschap 'Type', u kunt het bereik Hallo steekproeven toohello waarden van deze eigenschap. Hallo eindresultaat van Hallo steekproeven is een set met tabellen voor elk Hallo waarden voor het Type dat u hebt opgegeven. Typ bijvoorbeeld = auto produceert een auto-tabel bij het Type = vlak geeft als resultaat een tabel vlak.

1. Na het voltooien van stap 1 en 4 in [Connect tooyour Azure Cosmos DB database](#connect), klikt u op **Schema-Editor** hello Azure Cosmos DB ODBC-stuurprogramma instellen van de DSN-venster.
2. In Hallo **Schema-Editor** venster, klikt u op **nieuw**.
    Hallo **Schema genereren** venster bevat alle Hallo verzamelingen in hello Azure DB die Cosmos-account. 
3. Selecteer een verzameling op Hallo **voorbeeldweergave** tabblad in Hallo **toewijzing definitie** kolom voor de verzameling hello, klikt u op **bewerken**. Klik dan in Hallo **toewijzing definitie** Selecteer **tabel scheidingstekens** methode. Vervolgens Hallo na:

    a. In Hallo **kenmerken** vak, Hallo typenaam van de eigenschap van een scheidingsteken. Dit is een eigenschap in het document dat u wilt dat tooscope Hallo steekproeven, bijvoorbeeld plaats en druk op enter. 

    b. Als u alleen tooscope Hallo steekproeven toocertain waarden voor het Hallo-kenmerk die u zojuist hebt ingevoerd wilt, selecteert u Hallo-kenmerk in Hallo selecteren in het vak en typt u een waarde in Hallo **waarde** vak bijvoorbeeld Seattle en druk op enter. U kunt tooadd blijven meerdere waarden voor kenmerken. NET ervoor te zorgen dat Hallo juiste kenmerk is ingeschakeld wanneer u waarden invoert.

    Als u bijvoorbeeld een **kenmerken** toolimit waarde van plaats en u wilt dat uw tabel tooonly rijen met een waarde van de plaats van New York en Dubai opnemen, zou u plaats in Hallo kenmerken vak en New York en vervolgens Dubai in Hallo  **Waarden** vak.
4. Klik op **OK**. 
5. Na het voltooien van Hallo toewijzing definities voor Hallo verzamelingen die u wilt toosample in Hallo **Schema-Editor** venster, klikt u op **voorbeeld**.
     Voor elke kolom, kunt u de kolomnaam SQL hello, Hallo SQL-type, SQL-lengte (indien van toepassing), schalen (indien van toepassing), Precision (indien van toepassing) en null-waarden bevatten.
    - U kunt instellen **kolom verbergen** te**true** desgewenst tooexclude die kolom van de queryresultaten. Kolommen kolom verbergen gemarkeerd = true niet worden geretourneerd voor de selectie en projectie, hoewel ze nog steeds deel van Hallo schema uitmaken. U kunt bijvoorbeeld alle hello Azure Cosmos DB vereist Systeemeigenschappen beginnen met '_' verbergen.
    - Hallo **id** kolom Hallo enige veld dat kan niet worden verborgen, zoals het wordt gebruikt als primaire sleutel in het Hallo genormaliseerde schema Hallo is. 
6. Wanneer u klaar bent met het Hallo-schema definiëren, klikt u op **bestand** | **opslaan**, toohello directory toosave Hallo-schema te navigeren en klik op **opslaan**.
7. Terug in Hallo **Azure Cosmos DB ODBC-stuurprogramma DSN Setup** venster, klikt u op ** Geavanceerde opties **. Klik op Hallo **schemabestand** vak, gaat u schemabestand toohello opgeslagen en klik op **OK**. Klik op **OK** opnieuw toosave Hallo DSN-naam. Dit bespaart Hallo schema gemaakt van toohello DSN-naam. 

## <a name="optional-creating-views"></a>(Optioneel) Maken van weergaven
U kunt definiëren en weergaven maken als onderdeel van Hallo steekproeven proces. Deze weergaven zijn equivalent tooSQL weergaven. Ze zijn alleen-lezen en zijn bereik Hallo selecties en projecties Hallo die Azure Cosmos DB SQL gedefinieerd. 

een weergave voor uw gegevens, op Hallo toocreate **Schema-Editor** in Hallo van het venster **definities weergeven** kolom, klikt u op **toevoegen** op Hallo rij van Hallo verzameling toosample. Klik dan in Hallo **definities** venster Hallo te volgen:
1. Klik op **nieuw**, voer een naam voor Hallo weergave, bijvoorbeeld EmployeesfromSeattleView en klik vervolgens op **OK**.
2. In Hallo **weergave bewerken** venster een Azure Cosmos DB-query invoeren. Dit moet een Azure Cosmos DB SQL-query, bijvoorbeeld`SELECT c.City, c.EmployeeName, c.Level, c.Age, c.Gender, c.Manager FROM c WHERE c.City = “Seattle”`, en klik vervolgens op **OK**.

Als u wilt, kunt u een groot aantal weergaven maken. Wanneer u klaar bent met definiëren Hallo weergaven, kunt u vervolgens voorbeeldgegevens Hallo. 

## <a name="step-5-view-your-data-in-bi-tools-such-as-power-bi-desktop"></a>Stap 5: Uw gegevens weergeven in de BI-tools zoals Power BI Desktop

U kunt uw nieuwe DSN tooconnect DocumentADB gebruiken met een ODBC-hulpprogramma's - deze stap kunt u eenvoudig zien hoe tooconnect tooPower BI Desktop en maak een visualisatie in Power BI.

1. Power BI Desktop openen.
2. Klik op **gegevens ophalen**.
3. In Hallo **gegevens ophalen** venster, klikt u op **andere** | **ODBC** | **Connect**.
4. In Hallo **van ODBC** venster, selecteer Hallo gegevensbronnaam u gemaakt en klik vervolgens op **OK**. U kunt laten Hallo **geavanceerde opties** vermeldingen leeg.
5. In Hallo **toegang krijgen tot een gegevensbron met behulp van een ODBC-stuurprogramma** Selecteer **standaard of aangepast** en klik vervolgens op **Connect**. U hoeft geen tooinclude hello **referentie-eigenschappen van een verbindingsreeks**.
6. In Hallo **Navigator** venster in het linkerdeelvenster hello, vouw Hallo-database, Hallo schema en selecteer vervolgens Hallo tabel. deelvenster met resultaten Hallo omvat Hallo-gegevens met behulp van Hallo schema die u hebt gemaakt.
7. toovisualize hello gegevens in Power BI desktop Hallo selectievakje voor de tabelnaam Hallo en klik vervolgens op **Load**.
8. Selecteer in Power BI Desktop op Hallo ver links, tabblad Hallo-gegevens ![Tabblad gegevens in Power BI Desktop](./media/odbc-driver/odbc-driver-data-tab.png) tooconfirm die uw gegevens zijn geïmporteerd.
9. U kunt nu visuele elementen waarvoor Power BI door te klikken op het tabblad Hallo-rapport maken ![tabblad van het rapport in Power BI Desktop](./media/odbc-driver/odbc-driver-report-tab.png), te klikken op **nieuwe Visual**, en vervolgens aanpassen van uw tegel. Zie voor meer informatie over het maken van visualisaties in Power BI Desktop [visualisatietypen in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-visualization-types-for-reports-and-q-and-a/).

## <a name="troubleshooting"></a>Problemen oplossen

Als u de volgende fout Hallo ontvangt, zorg ervoor dat Hallo **Host** en **toegangssleutel** waarden die u hebt gekopieerd hello Azure-portal op [stap 2](#connect) juist zijn en probeer het vervolgens opnieuw. Hallo kopie knoppen toohello rechts van hello gebruiken **Host** en **toegangssleutel** waarden in hello Azure portal toocopy Hallo waarden fout gratis.

    [HY000]: [Microsoft][Azure Cosmos DB] (401) HTTP 401 Authentication Error: {"code":"Unauthorized","message":"hello input authorization token can't serve hello request. Please check that hello expected payload is built as per hello protocol, and check hello key being used. Server used hello following payload toosign: 'get\ndbs\n\nfri, 20 jan 2017 03:43:55 gmt\n\n'\r\nActivityId: 9acb3c0d-cb31-4b78-ac0a-413c8d33e373"}`

## <a name="next-steps"></a>Volgende stappen

Zie toolearn meer informatie over Azure Cosmos DB [wat is Azure Cosmos DB?](introduction.md).
