---
title: aaaGet slag met Data Catalog | Microsoft Docs
description: End-to-end zelfstudie presenteren Hallo scenario's en mogelijkheden van Azure Data Catalog.
documentationcenter: 
services: data-catalog
author: steelanddata
manager: jhubbard
editor: 
tags: 
ms.assetid: 03332872-8d84-44a0-8a78-04fd30e14b18
ms.service: data-catalog
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 7652918b5a8254f5cff9e32d77b1fd3e1bf59d59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-catalog"></a>Aan de slag met Azure Data Catalog
Azure Data Catalog is een volledig beheerde cloudservice die als een registratie- en detectiesysteem voor gegevensassets van ondernemingen fungeert. Zie [Wat is Azure Data Catalog?](data-catalog-what-is-data-catalog.md) voor een gedetailleerd overzicht.

Deze zelfstudie helpt u om aan de slag te gaan met Azure Data Catalog. U voert Hallo procedures in deze zelfstudie te volgen:

| Procedure | Beschrijving |
|:--- |:--- |
| [Gegevenscatalogus inrichten](#provision-data-catalog) |In deze procedure richt of stelt u een Azure Data Catalog in. U doen deze stap alleen als Hallo catalogus voordat niet is ingesteld. Zelfs als er aan uw Azure-account meerdere abonnementen zijn gekoppeld, kunt u slechts één gegevenscatalogus per organisatie (Microsoft Azure Active Directory-domein) hebben. |
| [Gegevensassets registreren](#register-data-assets) |In deze procedure kunt u gegevensassets van Hallo AdventureWorks2014 voorbeelddatabase registreren met Hallo data catalog. Registratie is Hallo proces uitpakken belangrijke structurele metagegevens zoals namen, typen en locaties van de gegevensbron Hallo en die metagegevens toohello catalogus te kopiëren. Hallo gegevensbron en gegevensassets blijven waar ze zijn, maar het Hallo-metagegevens wordt gebruikt door Hallo catalogus toomake ze eenvoudiger kunnen worden gedetecteerd en begrijpelijk. |
| [Gegevensassets detecteren](#discover-data-assets) |In deze procedure gebruikt u hello Azure Data Catalog portal toodiscover gegevensassets die zijn geregistreerd in de vorige stap Hallo. Nadat een gegevensbron is geregistreerd met Azure Data Catalog, worden de metagegevens wordt geïndexeerd door Hallo-service zodat gebruikers eenvoudig kunnen zoeken naar Hallo-gegevens die ze nodig hebben. |
| [Aantekeningen toevoegen aan gegevensassets](#annotate-data-assets) |In deze procedure kunt opgeven u aantekeningen (informatie zoals beschrijvingen, tags, documentatie of deskundigen) voor Hallo gegevensassets. Deze informatie is een aanvulling op Hallo metagegevens die zijn geëxtraheerd uit de gegevensbron Hallo en meer te begrijpen toomore mensen toomake Hallo-gegevensbron. |
| [Verbinding maken met toodata activa](#connect-to-data-assets) |In deze procedure opent u gegevensassets in geïntegreerde clienthulpprogramma's (zoals Excel en SQL Server Data Tools) en een niet-geïntegreerd hulpprogramma (SQL Server Management Studio). |
| [Gegevensassets beheren](#manage-data-assets) |In deze procedure stelt u beveiliging in voor uw gegevensassets. Data Catalog geeft gebruikers geen toegang tot toohello gegevens zelf. Hallo-eigenaar van de gegevensbron Hallo beheert de gegevenstoegang. <br/><br/> Met Data Catalog, u kunt detecteren, gegevensbronnen en weergave Hallo **metagegevens** toohello gegevensbronnen die zijn geregistreerd in de catalogus Hallo gerelateerd. Mogelijk zijn er situaties echter waar gegevensbronnen zichtbaar alleen toospecific gebruikers of toomembers van specifieke groepen moet. Voor deze scenario's, kunt u Data Catalog tootake eigendom van geregistreerde gegevensassets binnen Hallo catalogus en beheer Hallo zichtbaarheid van Hallo activa die u bezit. |
| [Gegevensassets verwijderen](#remove-data-assets) |In deze procedure leert u hoe de gegevensassets tooremove van Hallo gegevenscatalogus. |

## <a name="tutorial-prerequisites"></a>Vereisten voor de zelfstudie
### <a name="azure-subscription"></a>Azure-abonnement
tooset van Azure Data Catalog, moet u de eigenaar van het Hallo of mede-eigenaar van een Azure-abonnement.

Azure-abonnementen kunnen u toegang tot toocloud servicebronnen zoals Azure Data Catalog indelen. Ze helpen u ook om te bepalen hoe resourcegebruik wordt gerapporteerd, gefactureerd en betaald. Elk abonnement kan een andere facturerings- en betalingsinstelling hebben, zodat u per afdeling, project, regiokantoor, enzovoort verschillende abonnementen en plannen kunt hebben. Elke cloudservice tooa abonnement behoort en moet u een abonnement voordat het instellen van Azure Data Catalog toohave. toolearn meer, Zie [beheren van accounts, abonnementen en beheerdersrollen](../active-directory/active-directory-how-subscriptions-associated-directory.md).

Als u geen abonnement hebt, kunt u binnen een paar minuten een gratis proefaccount maken. Zie [Gratis proefversie](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.

### <a name="azure-active-directory"></a>Azure Active Directory
tooset van Azure Data Catalog, als u bent aangemeld met een gebruikersaccount van Azure Active Directory (Azure AD). U moet de eigenaar van het Hallo of mede-eigenaar van een Azure-abonnement.  

Azure AD biedt een eenvoudige manier voor uw zakelijke toomanage identiteits- en toegangsbeheer, zowel in Hallo cloud en on-premises. U kunt een enkel werk of school-account toosign in tooany cloud of lokale webtoepassing. Azure Data Catalog maakt gebruik van Azure AD tooauthenticate aanmelden. toolearn meer, Zie [wat is Azure Active Directory](../active-directory/active-directory-whatis.md).

### <a name="azure-active-directory-policy-configuration"></a>Azure Active Directory-beleid configureren
Een situatie kunnen optreden wanneer u zich kunt aanmelden toohello Azure Data Catalog-portal, maar wanneer u probeert toosign in hulpprogramma voor registratie van gegevensbronnen toohello, u ontvangt een foutmelding dat u niet aanmelden. Deze fout kan optreden wanneer u gebruikmaakt van het bedrijfsnetwerk Hallo of wanneer u verbinding maakt vanaf een externe Hallo-netwerk van bedrijf.

maakt gebruik van hulpprogramma voor registratie Hallo *formulierverificatie* toovalidate gebruikersaanmeldingen op basis van Azure Active Directory. Geslaagde aanmelden, een Azure Active Directory-beheerder moet inschakelen formulierverificatie in Hallo *globale verificatiebeleid*.

Met het globale verificatiebeleid Hallo kunt u de verificatie afzonderlijk voor intranet en extranet-verbindingen, zoals wordt weergegeven in Hallo installatiekopie te volgen. Aanmelden fouten optreden als formulierverificatie niet is ingeschakeld voor het Hallo-netwerk van waaruit u verbinding maakt.

 ![Het algemene verificatiebeleid van Azure Active Directory](./media/data-catalog-prerequisites/global-auth-policy.png)

Zie [Verificatiebeleid configureren](https://technet.microsoft.com/library/dn486781.aspx) voor meer informatie.

## <a name="provision-data-catalog"></a>Gegevenscatalogus inrichten
U kunt per organisatie (Azure Active Directory-domein) slechts één gegevenscatalogus inrichten. Daarom als Hallo eigenaar of mede-eigenaar van een Azure-abonnement die lid is van toothis Azure Active Directory-domein is al een catalogus worden gemaakt, zich u niet kunnen toocreate een catalogus opnieuw zelfs als u meerdere Azure-abonnementen hebt. tootest of een catalogus met gegevens is gemaakt door een gebruiker in uw Azure Active Directory-domein, gaat u toohello [startpagina van Azure Data Catalog](http://azuredatacatalog.com) en controleer of u de catalogus Hallo bekijken. Als u al een catalogus is gemaakt, slaat u hello te volgen procedure en gaat u naar toohello volgende sectie.    

1. Ga toohello [Data Catalog servicepagina](https://azure.microsoft.com/services/data-catalog) en klik op **aan de slag**.
   
    ![Azure Data Catalog - marketingstartpagina](media/data-catalog-get-started/data-catalog-marketing-landing-page.png)
2. Aanmelden met een gebruikersaccount dat is Hallo eigenaar of mede-eigenaar van een Azure-abonnement. U ziet Hallo na pagina na het aanmelden.
   
    ![Azure Data Catalog - gegevenscatalogus inrichten](media/data-catalog-get-started/data-catalog-create-azure-data-catalog.png)
3. Geef een **naam** voor Hallo data catalog, Hallo **abonnement** u wilt toouse en Hallo **locatie** voor Hallo-catalogus.
4. Vouw **Prijzen** uit en selecteer een Azure Data Catalog-**editie** (gratis of Standard).
    ![Azure Data Catalog - editie selecteren](media/data-catalog-get-started/data-catalog-create-catalog-select-edition.png)
5. Vouw **Catalogusgebruikers** en klik op **toevoegen** tooadd gebruikers voor Hallo data catalog. U wordt automatisch toothis groep toegevoegd.
    ![Azure Data Catalog - gebruikers](media/data-catalog-get-started/data-catalog-add-catalog-user.png)
6. Vouw **catalogus beheerders** en klik op **toevoegen** tooadd extra beheerders voor Hallo data catalog. U wordt automatisch toothis groep toegevoegd.
    ![Azure Data Catalog - beheerders](media/data-catalog-get-started/data-catalog-add-catalog-admins.png)
7. Klik op **catalogus maken** toocreate Hallo gegevenscatalogus voor uw organisatie. U ziet Hallo startpagina voor Hallo data catalog nadat deze is gemaakt.
    ![Azure Data Catalog - gemaakt](media/data-catalog-get-started/data-catalog-created.png)    

### <a name="find-a-data-catalog-in-hello-azure-portal"></a>Een catalogus met gegevens niet vinden in hello Azure-portal
1. Ga op een afzonderlijke tabblad in de webbrowser Hallo of in een afzonderlijke browservenster toohello [Azure-portal](https://portal.azure.com) en meld u aan met Hallo dezelfde account die u gebruikte toocreate Hallo catalogus met gegevens in de vorige stap Hallo.
2. Selecteer **Bladeren** en klik vervolgens op **Gegevenscatalogus**.
   
    ![Azure Data Catalog--Azure Bladeren](media/data-catalog-get-started/data-catalog-browse-azure-portal.png) Hallo gegevens catalogus u hebt gemaakt.
   
    ![Azure Data Catalog - catalogus in lijst bekijken](media/data-catalog-get-started/data-catalog-azure-portal-show-catalog.png)
3. Klik op Hallo catalogus die u hebt gemaakt. U ziet Hallo **Data Catalog** blade in Hallo-portal.
   
   ![Azure Data Catalog - blade in portal ](media/data-catalog-get-started/data-catalog-blade-azure-portal.png)
4. U kunt eigenschappen van de gegevenscatalogus Hallo bekijken en deze relaties bijwerken. Bijvoorbeeld, klik op **prijscategorie** en Hallo editie wijzigen.
   
    ![Azure Data Catalog - prijscategorie](media/data-catalog-get-started/data-catalog-change-pricing-tier.png)

### <a name="adventure-works-sample-database"></a>Adventure Works-voorbeelddatabase
In deze zelfstudie registreert u gegevensassets (tabellen) uit Hallo AdventureWorks2014 voorbeelddatabase voor SQL Server Database Engine hello, maar u kunt elke ondersteunde gegevensbron gebruiken als u liever toowork met gegevens die wordt vertrouwd en relevant tooyour rol. Zie voor een lijst met ondersteunde gegevensbronnen [Ondersteunde gegevensbronnen](data-catalog-dsr.md).

### <a name="install-hello-adventure-works-2014-oltp-database"></a>Hallo Adventure Works 2014 OLTP-database installeren
database van Adventure Works Hallo ondersteunt standaard online transaction processing-scenario's voor een fictieve fietsfabrikant (Adventure Works Cycles), waaronder producten, verkoop en inkoop. In deze zelfstudie registreert u informatie over producten in Azure Data Catalog.

voorbeelddatabase voor tooinstall Hallo Adventure Works:

1. Download [Adventure Works 2014 Full Database Backup.zip](https://msftdbprodsamples.codeplex.com/downloads/get/880661) in CodePlex.
2. Hallo-database op uw machine toorestore Hallo instructies in [een databaseback-up herstellen met behulp van SQL Server Management Studio](http://msdn.microsoft.com/library/ms177429.aspx), of met de volgende stappen:
   1. Open SQL Server Management Studio en maak verbinding toohello SQL Server Database Engine.
   2. Klik met de rechtermuisknop op **Databases** en klik op **Database terugzetten**.
   3. Onder **Restore Database**, klikt u op Hallo **apparaat** optie voor **bron** en klik op **Bladeren**.
   4. Klik onder **Apparaat voor back-up selecteren** op **Toevoegen**.
   5. Ga toohello map waar u Hallo hebt **AdventureWorks2014.bak** bestand, selecteer Hallo-bestand en klik op **OK** tooclose hello **vinden back-upbestand** in het dialoogvenster.
   6. Klik op **OK** tooclose hello **back-upapparaten Selecteer** in het dialoogvenster.    
   7. Klik op **OK** tooclose hello **Restore Database** in het dialoogvenster.

U kunt nu gegevensassets van Adventure Works-voorbeelddatabase Hallo registreren met behulp van Azure Data Catalog.

## <a name="register-data-assets"></a>Gegevensassets registreren
In deze oefening maakt u Hallo registratie hulpprogramma tooregister gegevensassets uit de database van Adventure Works Hallo met Hallo catalog gebruiken. Registratie is Hallo proces waarbij belangrijke structurele metagegevens zoals namen, typen en locaties van gegevensbron Hallo en Hallo activa bevat en die metagegevens toohello catalogus te kopiëren. Hallo gegevensbron en gegevensassets blijven waar ze zijn, maar het Hallo-metagegevens wordt gebruikt door Hallo catalogus toomake ze eenvoudiger kunnen worden gedetecteerd en begrijpelijk.

### <a name="register-a-data-source"></a>Een gegevensbron registreren
1. Ga toohello [startpagina van Azure Data Catalog](http://azuredatacatalog.com) en klik op **gegevens publiceren**.
   
   ![Azure Data Catalog - de knop Gegevens publiceren](media/data-catalog-get-started/data-catalog-publish-data.png)
2. Klik op **toepassing starten** toodownload, installeren en uitvoeren Hallo hulpprogramma voor registratie op uw computer.
   
   ![Azure Data Catalog - de knop Starten](media/data-catalog-get-started/data-catalog-launch-application.png)
3. Op Hallo **Welkom** pagina, klikt u op **aanmelden** en voer uw referenties.     
   
    ![Azure Data Catalog - Welkomstpagina](media/data-catalog-get-started/data-catalog-welcome-dialog.png)
4. Op Hallo **Microsoft Azure Data Catalog** pagina, klikt u op **SQL Server** en **volgende**.
   
    ![Azure Data Catalog - gegevensbronnen](media/data-catalog-get-started/data-catalog-data-sources.png)
5. Voer Hallo SQL Server-verbindingseigenschappen voor **AdventureWorks2014** (Zie het volgende voorbeeld Hallo) en klik op **CONNECT**.
   
   ![Azure Data Catalog - SQL Server-verbindingsinstellingen](media/data-catalog-get-started/data-catalog-sql-server-connection.png)
6. Hallo-metagegevens van uw gegevensasset registreren. In dit voorbeeld registreert u **Production/Product** objecten uit de naamruimte AdventureWorks Production Hallo:
   
   1. In Hallo **serverhiërarchie** structuur uit, vouw **AdventureWorks2014** en klik op **productie**.
   2. Ctrl+klik op **Product**, **ProductCategory**, **ProductDescription** en **ProductPhoto**.
   3. Klik op Hallo **geselecteerde pijl verplaatsen** (**>**). Deze actie worden alle geselecteerde objecten verplaatst in Hallo **objecten toobe geregistreerd** lijst.
      
      ![Zelfstudie voor Azure Data Catalog - bladeren door objecten en objecten selecteren](media/data-catalog-get-started/data-catalog-server-hierarchy.png)
   4. Selecteer **voorbeeld** tooinclude een voorbeeld van de momentopname van Hallo-gegevens. Hallo momentopname too20 records uit elke tabel bevat en deze is gekopieerd in Hallo-catalogus.
   5. Selecteer **gegevens profiel opnemen** tooinclude een momentopname van Hallo object statistieken voor Hallo gegevens profiel (bijvoorbeeld: minimum, maximum en gemiddelde waarden voor een kolom, het aantal rijen).
   6. In Hallo **labels toevoegen** veld **adventure works, replicatiecycli**. Met deze actie worden zoektags voor deze gegevensassets toegevoegd. Labels zijn een goede manier toohelp gebruikers een geregistreerde gegevensbron vinden.
   7. Hallo naam opgeven van een **deskundige** gegevens (optioneel).
      
      ![Zelfstudie voor Azure Data Catalog--objecten toobe geregistreerd](media/data-catalog-get-started/data-catalog-objects-register.png)
   8. Klik op **REGISTREREN**. Azure Data Catalog registreert uw geselecteerde objecten. In deze oefening worden Hallo geselecteerde objecten van Adventure Works geregistreerd. hulpprogramma voor registratie Hallo haalt metagegevens uit Hallo gegevensasset en worden die gegevens gekopieerd naar hello Azure Data Catalog-service. Hallo gegevens blijven waar deze zich momenteel bevindt, en blijft onder Hallo-besturingselement van het Hallo-beheerders en het beleid van het huidige systeem Hallo.
      
      ![Azure Data Catalog - geregistreerde objecten](media/data-catalog-get-started/data-catalog-registered-objects.png)
   9. Klik op toosee uw geregistreerde gegevensbronobjecten **Portal weergeven**. Bevestig dat u alle vier tabellen en Hallo-database in de rasterweergave Hallo ziet in hello Azure Data Catalog-portal.
      
      ![Objecten in hello Azure Data Catalog-portal ](media/data-catalog-get-started/data-catalog-view-portal.png)

In deze oefening maakt u objecten uit de voorbeelddatabase van Adventure Works Hallo geregistreerd, zodat ze eenvoudig kunnen worden gevonden door gebruikers in uw organisatie. In Hallo volgende oefening leert u hoe toodiscover geregistreerde gegevensassets.

## <a name="discover-data-assets"></a>Gegevensassets detecteren
Voor detectie in Azure Data Catalog worden twee primaire mechanismen gebruikt: zoeken en filteren.

Het zoeken is ontworpen toobe intuïtieve en krachtige. Standaard worden zoektermen vergeleken met een eigenschap in het Hallo catalog, met inbegrip van de gebruiker opgegeven aantekeningen.

Voor het filteren is ontworpen toocomplement zoeken. U kunt specifieke kenmerken zoals deskundigen, gegevensbrontype, objecttype selecteren en labels tooview overeenkomende gegevensassets en tooconstrain zoeken resultaten toomatching activa.

Met behulp van een combinatie van zoeken en filteren kunt u snel Hallo gegevensbronnen die zijn geregistreerd met Azure Data Catalog toodiscover hello gegevensassets u moet navigeren.

In deze oefening gebruikt u hello Azure Data Catalog portal toodiscover gegevensassets die u in de vorige oefening Hallo geregistreerd. Zie [Verwijzing naar de zoeksyntaxis van Data Catalog](https://msdn.microsoft.com/library/azure/mt267594.aspx) voor meer informatie over de zoeksyntaxis.

Hier volgen enkele voorbeelden voor het detecteren van gegevensassets in Hallo-catalogus.  

### <a name="discover-data-assets-with-basic-search"></a>Gegevensassets met een basiszoekopdracht detecteren
Met een basiszoekopdracht kunt u in een catalogus zoeken met behulp van een of meer zoektermen. De resultaten zijn elementen die overeenkomen met een eigenschap met een of meer Hallo voorwaarden opgegeven.

1. Klik op **Start** in hello Azure Data Catalog-portal. Als u Hallo webbrowser hebt gesloten, gaat u toohello [startpagina van Azure Data Catalog](https://www.azuredatacatalog.com).
2. Voer in het zoekvak Hallo `cycles` en druk op **ENTER**.
   
    ![Azure Data Catalog - basiszoekopdracht naar tekst](media/data-catalog-get-started/data-catalog-basic-text-search.png)
3. Controleer of u alle vier tabellen en Hallo-database (AdventureWorks2014) in Hallo resultaten. U kunt schakelen tussen **rasterweergave** en **lijstweergave** door te klikken op knoppen op de werkbalk hello, zoals wordt weergegeven in Hallo installatiekopie te volgen. U ziet dat trefwoord Hallo is gemarkeerd in de zoekresultaten Hallo omdat Hallo **Markeer** optie is **ON**. U kunt ook opgeven Hallo aantal **resultaten per pagina** in de zoekresultaten.
   
    ![Azure Data Catalog - resultaten van basiszoekopdracht naar tekst](media/data-catalog-get-started/data-catalog-basic-text-search-results.png)
   
    Hallo **zoekopdrachten** deelvenster is op Hallo links en Hallo **eigenschappen** deelvenster is op de juiste Hallo. Op Hallo **zoekopdrachten** Configuratiescherm kunt u zoekcriteria wijzigen en resultaten filteren. Hallo **eigenschappen** deelvenster Eigenschappen van een geselecteerd object weergegeven in het raster hello of een lijst.
4. Klik op **Product** in zoekresultaten Hallo. Klik op Hallo **Preview**, **kolommen**, **gegevens profiel**, en **documentatie** tabbladen, of klik op Hallo pijl tooexpand Hallo onderste deelvenster.  
   
    ![Azure Data Catalog - onderste deelvenster](media/data-catalog-get-started/data-catalog-data-asset-preview.png)
   
    Op Hallo **Preview** tabblad ziet u een voorbeeld van gegevens in Hallo Hallo **Product** tabel.  
5. Klik op Hallo **kolommen** tabblad toofind details over kolommen (zoals **naam** en **gegevenstype**) in Hallo gegevensasset.
6. Klik op Hallo **gegevens profiel** tabblad toosee Hallo profileren van gegevens (bijvoorbeeld: aantal rijen, de grootte van gegevens of de minimale waarde in een kolom) in Hallo gegevensasset.
7. Hallo resultaten filteren met behulp van **Filters** op Hallo links. Bijvoorbeeld, klik op **tabel** voor **objecttype**, en u enige Hallo vier tabellen zien, niet Hallo database.
   
    ![Azure Data Catalog - zoekresultaten filteren](media/data-catalog-get-started/data-catalog-filter-search-results.png)

### <a name="discover-data-assets-with-property-scoping"></a>Gegevens detecteren door het bereik van eigenschappen te definiëren
Eigenschap helpt bij het detecteren van gegevensassets waarbij de zoekterm Hallo komt met de Hallo overeen scoping opgegeven eigenschap.

1. Schakel Hallo **tabel** filteren onder **objecttype** in **Filters**.  
2. Voer in het zoekvak Hallo `tags:cycles` en druk op **ENTER**. Zie [verwijzing naar de Zoeksyntaxis van Data Catalog](https://msdn.microsoft.com/library/azure/mt267594.aspx) voor alle eigenschappen die u gebruiken kunt voor het zoeken van de gegevenscatalogus Hallo Hallo.
3. Controleer of u alle vier tabellen en Hallo-database (AdventureWorks2014) in Hallo resultaten.  
   
    ![Data Catalog - resultaten van het definiëren van het bereik van eigenschappen](media/data-catalog-get-started/data-catalog-property-scoping-results.png)

### <a name="save-hello-search"></a>Hallo zoekopdracht opslaan
1. In Hallo **zoekopdrachten** deelvenster in Hallo **huidige zoekopdracht** sectie, voer een naam voor Hallo zoeken en klikt u op **opslaan**.
   
    ![Azure Data Catalog - zoekopdracht opslaan](media/data-catalog-get-started/data-catalog-save-search.png)
2. Bevestig die Hallo opgeslagen zoekopdracht wordt weergegeven onder **opgeslagen zoekacties**.
   
    ![Azure Data Catalog - opgeslagen zoekopdrachten](media/data-catalog-get-started/data-catalog-saved-search.png)
3. Selecteer een van de Hallo-acties die u op Hallo opgeslagen zoekopdracht uitvoeren kunt (**naam**, **verwijderen**, **opslaan als standaard** zoeken).
   
    ![Azure Data Catalog - opties voor opgeslagen zoekopdrachten](media/data-catalog-get-started/data-catalog-saved-search-options.png)

### <a name="boolean-operators"></a>Booleaanse operators
U kunt uw zoekopdracht uitbreiden of beperken met Booleaanse operators.

1. Voer in het zoekvak Hallo `tags:cycles AND objectType:table`, en druk op **ENTER**.
2. Controleer of u alleen tabellen (geen Hallo database) in Hallo resultaten.  
   
    ![Azure Data Catalog - Booleaanse operator in zoekopdracht](media/data-catalog-get-started/data-catalog-search-boolean-operator.png)

### <a name="grouping-with-parentheses"></a>Groeperen met haakjes
U kunt delen van Hallo query tooachieve logische isolatie, met name in combinatie met Booleaanse operators groeperen door groeperen met haakjes.

1. Voer in het zoekvak Hallo `name:product AND (tags:cycles AND objectType:table)` en druk op **ENTER**.
2. Controleer of u alleen Hallo **Product** tabel in de zoekresultaten Hallo.
   
    ![Azure Data Catalog - zoekopdracht groeperen](media/data-catalog-get-started/data-catalog-grouping-search.png)   

### <a name="comparison-operators"></a>Vergelijkingsoperators
Met vergelijkingsoperators kunt u andere vergelijkingen dan gelijkheid gebruiken voor eigenschappen die de gegevenstypen numeriek en datum hebben.

1. Voer in het zoekvak Hallo `lastRegisteredTime:>"06/09/2016"`.
2. Schakel Hallo **tabel** filteren onder **objecttype**.
3. Druk op **ENTER**.
4. Controleer of u Hallo **Product**, **ProductCategory**, **ProductDescription**, en **ProductPhoto** tabellen en Hallo De database AdventureWorks2014 die u geregistreerd in de zoekresultaten.
   
    ![Azure Data Catalog - vergelijking van zoekresultaten](media/data-catalog-get-started/data-catalog-comparison-operator-results.png)

Zie [hoe toodiscover gegevensassets](data-catalog-how-to-discover.md) voor gedetailleerde informatie over het detecteren van gegevensassets en [verwijzing naar de Zoeksyntaxis van Data Catalog](https://msdn.microsoft.com/library/azure/mt267594.aspx) voor zoeksyntaxis.

## <a name="annotate-data-assets"></a>Aantekeningen toevoegen aan gegevensassets
In deze oefening gebruikt u hello Azure Data Catalog portal tooannotate (gegevens zoals beschrijvingen, tags of deskundigen toevoegen) gegevensassets die u eerder hebt geregistreerd in het Hallo-catalogus. Hallo aantekeningen vormen een aanvulling op en verbeteren van de structurele metagegevens Hallo opgehaald uit de gegevensbron Hallo tijdens de registratie en Hallo gegevensassets veel eenvoudiger toodiscover maakt en begrijpen.

In deze oefening maakt u aantekeningen voor een enkele gegevensasset (ProductPhoto). U toevoegen een beschrijvende naam en beschrijving toohello ProductPhoto gegevensasset.  

1. Ga toohello [startpagina van Azure Data Catalog](https://www.azuredatacatalog.com) en zoek met `tags:cycles` toofind Hallo-gegevensassets u hebt geregistreerd.  
2. Klik in de zoekresultaten op **ProductPhoto**.  
3. Voer **productafbeeldingen** voor **beschrijvende naam** en **Productfoto's voor marketingmateriaal** voor Hallo **beschrijving**.
   
    ![Azure Data Catalog - beschrijving van ProductPhoto](media/data-catalog-get-started/data-catalog-productphoto-description.png)
   
    Hallo **beschrijving** helpt anderen detecteren en begrijpen waarom en hoe toouse hello gegevensasset geselecteerd. U kunt ook meer tags toevoegen en kolommen weergeven. Nu kunt u zoeken en filteren toodiscover gegevensassets met behulp van de beschrijvende metagegevens Hallo proberen kunt u de catalogus toohello hebt toegevoegd.

U kunt ook doen Hallo op deze pagina te volgen:

* Experts voor Hallo gegevensasset toevoegen. Klik op **toevoegen** in Hallo **Experts** gebied.
* Labels toevoegen op Hallo gegevensset niveau. Klik op **toevoegen** in Hallo **labels** gebied. Een label kan een gebruikerstag of een woordenlijsttag zijn. Hallo Standard-editie van Data Catalog bevat een zakelijke woordenlijst waarmee catalogus beheerders kunnen een centrale zakelijke taxonomie definiëren. Catalogusgebruikers kunnen vervolgens aantekeningen toevoegen aan gegevensassets met behulp van termen in de woordenlijst. Zie voor meer informatie [hoe tooset van zakelijke woordenlijst Hallo voor Governed Tagging](data-catalog-how-to-business-glossary.md)
* Labels toevoegen op kolomniveau Hallo. Klik op **toevoegen** onder **labels** voor Hallo kolom gewenste tooannotate.
* Beschrijving op kolomniveau Hallo toevoegen. Voer een **Beschrijving** in voor een kolom. U kunt ook Hallo beschrijving metagegevens opgehaald uit de gegevensbron Hallo weergeven.
* Voeg **toegang aanvragen** informatie die gebruikers laat zien hoe toorequest toegang krijgen tot toohello gegevensasset.
  
    ![Azure Data Catalog - tags en beschrijvingen toevoegen](media/data-catalog-get-started/data-catalog-add-tags-experts-descriptions.png)
* Kies Hallo **documentatie** tabblad en documentatie voor Hallo gegevensasset bieden. Met Azure Data Catalog documentatie, kunt u de catalogus met gegevens als een opslagplaats voor inhoud toocreate voltooid sprekersnotities van uw gegevensassets.
  
    ![Azure Data Catalog - het tabblad Documentatie](media/data-catalog-get-started/data-catalog-documentation.png)

U kunt ook de gegevensassets van een aantekening toomultiple toevoegen. U kunt bijvoorbeeld alle Hallo gegevensassets die u geregistreerd selecteren en een expert voor hen opgeven.

![Azure Data Catalog - aantekeningen toevoegen aan meerdere gegevensassets](media/data-catalog-get-started/data-catalog-multi-select-annotate.png)

Azure Data Catalog biedt ondersteuning voor een benadering springen bron tooannotations. Elke gebruiker Data Catalog kunt tags (gebruiker of verklarende woordenlijst), beschrijvingen en andere metagegevens toevoegen zodat elke gebruiker met een perspectief op een gegevensasset en het gebruik ervan hebben kunt die perspectief vastgelegd en beschikbaar tooother gebruikers.

Zie [hoe tooannotate gegevensassets](data-catalog-how-to-annotate.md) voor gedetailleerde informatie over gegevensassets aantekeningen maken.

## <a name="connect-toodata-assets"></a>Verbinding maken met toodata activa
In deze oefening opent u gegevensassets in geïntegreerde clienthulpprogramma's en een niet-geïntegreerd hulpprogramma (SQL Server Management Studio) met behulp van verbindingsgegevens.

> [!NOTE]
> Het is belangrijk tooremember die Azure Data Catalog geeft geen toegang tot de werkelijke gegevensbron toohello — deze gewoon eenvoudiger voor u toodiscover en begrijpt. Wanneer u verbinding maakt met de gegevensbron tooa, Hallo client-toepassing die u gebruikt uw Windows-referenties of u wordt gevraagd om referenties indien nodig. Als u niet eerder zijn toegewezen toegang toohello gegevensbron, moet u toobe toegang verleend voordat u verbinding kunt maken.
> 
> 

### <a name="connect-tooa-data-asset-from-excel"></a>Verbinding maken met tooa gegevensasset uit Excel
1. Selecteer in de zoekresultaten de optie **Product**. Klik op **openen In** op Hallo werkbalk en klikt u op **Excel**.
   
    ![Azure Data Catalog--toodata asset verbinding](media/data-catalog-get-started/data-catalog-connect1.png)
2. Klik op **Open** in Hallo downloaden pop-upvenster. Deze ervaring kan variëren, afhankelijk van het Hallo-browser.
   
    ![Azure Data Catalog - gedownload Excel-verbindingsbestand](media/data-catalog-get-started/data-catalog-download-open.png)
3. In Hallo **beveiligingsbericht Microsoft Excel** venster, klikt u op **inschakelen**.
   
    ![Azure Data Catalog - beveiligingspop-upvenster van Excel](media/data-catalog-get-started/data-catalog-excel-security-popup.png)
4. Houd Hallo standaardwaarden Hallo **importgegevens** dialoogvenster en klik op **OK**.
   
    ![Azure Data Catalog - Excel-gegevens importeren](media/data-catalog-get-started/data-catalog-excel-import-data.png)
5. Hallo gegevensbron weergeven in Excel.
   
    ![Azure Data Catalog - producttabel in Excel](media/data-catalog-get-started/data-catalog-connect2.png)

In deze oefening maakt u een verbinding toodata activa gedetecteerd met Azure Data Catalog. Met hello Azure Data Catalog-portal, kunt u verbinden via Hallo-clienttoepassingen die is geïntegreerd in Hallo **openen in** menu. U kunt ook verbinding maken met elke toepassing die u met behulp van locatie-informatie voor Hallo verbinding is opgenomen in de metagegevens van de asset Hallo kiezen. Bijvoorbeeld, kunt u SQL Server Management Studio tooconnect toohello AdventureWorks2014 tooaccess Hallo databasegegevens in Hallo gegevensassets geregistreerd in deze zelfstudie.

1. Open **SQL Server Management Studio**.
2. In Hallo **verbinding tooServer** dialoogvenster Hallo servernaam Voer van Hallo **eigenschappen** deelvenster in hello Azure Data Catalog-portal.
3. Juiste authenticatie en referenties tooaccess hello gegevensasset gebruiken. Als u geen toegang hebt, gebruikt u gegevens in Hallo **toegang aanvragen** veld tooget deze.
   
    ![Azure Data Catalog - verzoeken tot toegang](media/data-catalog-get-started/data-catalog-request-access.png)

Klik op **weergave verbindingsreeksen** tooview en kopieer ADF.NET en ODBC, OLEDB verbinding tekenreeksen toohello Klembord voor gebruik in uw toepassing.

## <a name="manage-data-assets"></a>Gegevensassets beheren
In deze stap ziet u hoe tooset beveiliging voor uw gegevensassets. Data Catalog geeft gebruikers geen toegang tot toohello gegevens zelf. Hallo-eigenaar van de gegevensbron Hallo beheert de gegevenstoegang.

U kunt Data Catalog gegevensbronnen toodiscover en tooview Hallo metagegevens gerelateerde toohello gegevensbronnen die zijn geregistreerd in Hallo-catalogus. Mogelijk zijn er situaties echter waar gegevensbronnen alleen zichtbaar toospecific gebruikers of toomembers van specifieke groepen worden mogen. Voor deze scenario's, kunt u Data Catalog tootake eigendom van geregistreerde gegevensassets binnen Hallo-catalogus en toothen besturingselement Hallo zichtbaarheid van Hallo activa die u bezit.

> [!NOTE]
> Hallo beheermogelijkheden die worden beschreven in deze oefening zijn alleen beschikbaar in Standard-editie van Azure Data Catalog hello, Hallo niet in de editie Free.
> In Azure Data Catalog, kunt u eigenaar worden van gegevensassets, mede-eigenaren toodata elementen toevoegen en Hallo zichtbaarheid van gegevensassets instellen.
> 
> 

### <a name="take-ownership-of-data-assets-and-restrict-visibility"></a>Eigenaar worden van gegevensassets en de zichtbaarheid beperken
1. Ga toohello [startpagina van Azure Data Catalog](https://www.azuredatacatalog.com). In Hallo **Search** tekst Voer `tags:cycles` en druk op **ENTER**.
2. Klik op een item in de lijst met resultaten van Hallo en op **eigenaar** op Hallo-werkbalk.
3. In Hallo **Management** sectie Hallo **eigenschappen** -scherm, klikt u op **eigenaar**.
   
    ![Azure Data Catalog - eigenaar worden](media/data-catalog-get-started/data-catalog-take-ownership.png)
4. toorestrict zichtbaarheid, kies **eigenaars en deze gebruikers** in Hallo **zichtbaarheid** sectie en klik op **toevoegen**. Gebruiker e-mailadressen invoeren in het tekstvak Hallo en druk op **ENTER**.
   
    ![Azure Data Catalog - toegang beperken](media/data-catalog-get-started/data-catalog-ownership.png)

## <a name="remove-data-assets"></a>Gegevensassets verwijderen
In deze oefening gebruikt hello Azure Data Catalog portal tooremove preview gegevens uit geregistreerde gegevensassets en gegevensassets uit Hallo catalogus verwijderen.

In Azure Data Catalog kunt u een individuele asset of meerdere assets verwijderen.

1. Ga toohello [startpagina van Azure Data Catalog](https://www.azuredatacatalog.com).
2. In Hallo **Search** tekst Voer `tags:cycles` en klik op **ENTER**.
3. Selecteer een item in de lijst met resultaten van Hallo en klik op **verwijderen** op Hallo werkbalk zoals weergegeven in Hallo installatiekopie te volgen:
   
    ![Azure Data Catalog - rasteritem verwijderen](media/data-catalog-get-started/data-catalog-delete-grid-item.png)
   
    Als u van de lijstweergave hello gebruikmaakt, is Hallo selectievakje toohello links van Hallo item zoals weergegeven in Hallo installatiekopie te volgen:
   
    ![Azure Data Catalog - lijstitem verwijderen](media/data-catalog-get-started/data-catalog-delete-list-item.png)
   
    U kunt ook meerdere gegevensassets selecteren en deze te verwijderen in Hallo volgende afbeelding wordt weergegeven:
   
    ![Azure Data Catalog - meerdere gegevensassets verwijderen](media/data-catalog-get-started/data-catalog-delete-assets.png)

> [!NOTE]
> standaardgedrag van de catalogus Hallo Hallo is tooallow eventuele tooregister gebruiker gegevensbron en tooallow elke gebruiker toodelete gegevensasset die is geregistreerd. Hallo beheermogelijkheden opgenomen in de Standard-editie van Azure Data Catalog Hallo bieden extra opties voor de eigenaar van assets, te beperken wie assets kunnen detecteren en beperken wie assets kunnen verwijderen.
> 
> 

## <a name="summary"></a>Samenvatting
In deze zelfstudie hebt u essentiële mogelijkheden van Azure Data Catalog verkend, inclusief het registreren, annoteren, detecteren en beheren van zakelijke gegevensassets. Nu u Hallo-zelfstudie hebt voltooid, is het tijd tooget gestart. U kunt vandaag nog beginnen door het registreren van gegevensbronnen Hallo die u en uw team vertrouwen op en collega's toouse Hallo catalogus uitnodigen.

## <a name="references"></a>Verwijzingen
* [Hoe tooregister gegevensassets](data-catalog-how-to-register.md)
* [Hoe toodiscover gegevensassets](data-catalog-how-to-discover.md)
* [Hoe tooannotate gegevensassets](data-catalog-how-to-annotate.md)
* [Hoe toodocument gegevensassets](data-catalog-how-to-documentation.md)
* [Hoe tooconnect toodata activa](data-catalog-how-to-connect.md)
* [Hoe toomanage gegevensassets](data-catalog-how-to-manage.md)

