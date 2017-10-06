---
title: aaaAzure Data Catalog Veelgestelde vragen | Microsoft Docs
description: Veelgestelde vragen over Azure Data Catalog, met inbegrip van de mogelijkheden voor detectie van gegevensbron, aantekening en beheer.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 5c7e209a-458c-4bb4-96bb-7ed178f9528a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 03f9f4b801640b2e14232c62c8fc168e42e2c393
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-frequently-asked-questions"></a>Veelgestelde vragen over Azure Data Catalog
Dit artikel vindt antwoorden toofrequently gevraagd vragen gerelateerde toohello Azure Data Catalog-service.

## <a name="what-is-azure-data-catalog"></a>Wat is Azure Data Catalog?
Data Catalog is een volledig beheerde service wordt gehost in Microsoft Azure, die als een systeem van registratie en detectie van zakelijke gegevensbronnen fungeert. Met Data Catalog, kan alle gebruikers, van analisten toodata verzameld en ontwikkelaars registreren, detecteren, begrijpen en gebruiken gegevensbronnen.

## <a name="what-customer-challenges-does-it-solve"></a>Welke klant uitdagingen biedt deze oplossen?
Data Catalog adressen Hallo uitdagingen van de gegevensbron detectie en 'donkere gegevens' zodat gebruikers kunnen detecteren en begrijpen van zakelijke gegevensbronnen.

## <a name="what-are-its-target-audiences"></a>Wat zijn de doelgroepen?
Data Catalog is ontworpen voor technische en niet-technische gebruikers, waaronder:

* Ontwikkelaars van gegevens en BI en analytics-professionals: mensen die verantwoordelijk zijn voor het opstellen van gegevens en analyse van inhoud voor anderen tooconsume.
* Gegevens stewards: mensen Hallo kennis over Hallo gegevens, wat het betekent en hoe deze beoogde toobe gebruikt wordt.
* Gegevensgebruikers: mensen die nodig kunnen tooeasily toobe detecteren, begrijpen en verbinding maken met toohello gegevens die ze nodig toodo hun taak via hulpprogramma Hallo van hun keuze.
* Centrale IT: mensen die nodig toomake honderden van gegevensbronnen kunnen worden gedetecteerd door zakelijke gebruikers, en die toomaintain toezicht moet over hoe gegevens wordt gebruikt en door wie.

## <a name="what-is-its-availability-by-region"></a>Wat is de beschikbaarheid per regio?
Data catalogusservices zijn momenteel beschikbaar is in de volgende datacenters Hallo:

* VS - west
* VS - oost
* West-Europa
* Noord-Europa
* Australië - oost
* Zuidoost-Azië

## <a name="what-are-its-limits-on-hello-number-of-data-assets"></a>Wat zijn de beperkingen van het aantal gegevensassets Hallo?
Hallo is gratis editie van Data Catalog beperkt too5, 000 geregistreerde gegevensassets.

Hallo Standard-editie van Data Catalog ondersteunt up too100, 000 geregistreerde gegevensassets.

## <a name="what-are-its-supported-data-source-and-asset-types"></a>Wat zijn de ondersteunde bron- en asset gegevenstypen?
Zie voor een lijst met ondersteunde gegevensbronnen, [Data Catalog DSR](data-catalog-dsr.md).

## <a name="how-do-i-request-support-for-another-data-source"></a>Hoe ik ondersteuning voor een andere gegevensbron aanvragen?
toosubmit functie aanvragen en andere feedback, Ga toohello [Azure Data Catalog forum](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).

## <a name="how-do-i-get-started-with-data-catalog"></a>Hoe ga ik aan de slag met Data Catalog?
Hallo van de beste manier tooget is gestart door te gaan[aan de slag met Data Catalog](data-catalog-get-started.md). Dit artikel is een end-to-end-overzicht van Hallo mogelijkheden in Hallo-service.

## <a name="how-do-i-register-my-data"></a>Hoe registreer ik mijn gegevens?
tooregister uw gegevens in Data Catalog:
1. Hello Azure Data Catalog, in portal Hallo **publiceren** gebied, start hello Azure Data Catalog-hulpprogramma voor registratie. 
2. In Data Catalog Hallo publiceren van toepassing, meld u aan met Hallo dezelfde referenties gebruiken tooaccess Hallo Data Catalog-portal.
3. Selecteer gegevensbron Hallo en Hallo specifieke activa, dat u wilt dat tooregister.

## <a name="what-properties-does-it-extract-for-data-assets-that-are-registered"></a>Welke eigenschappen wordt deze uitgepakt voor bedrijfsmiddelen die met gegevens die zijn geregistreerd
Hallo-specifieke eigenschappen van gegevensbron bron toodata verschillen, maar in het algemeen Hallo Data Catalog publishing-service extraheert Hallo volgende informatie:

* De Assetnaam van de
* Activatype
* Beschrijving Asset
* Kenmerk-/ kolomnamen
* Kenmerk-/ kolomgegevenstypen
* Beschrijving van het kenmerk/kolom

> [!IMPORTANT]
> Registreren van gegevensassets met Data Catalog niet verplaatsen of kopiëren van uw gegevens toohello cloud. Registreren van de activa van een gegevensbron kopieën Hallo activa metagegevens tooAzure, maar Hallo gegevens blijft Hallo bestaande gegevensbron locatie. Hallo-uitzonderingsregel toothis is als u tooupload preview records of een profiel gegevens Hallo activa te registreren. Wanneer u een voorbeeld opnemen, up too20 zijn records gekopieerd vanaf elke asset en opgeslagen als een momentopname in Data Catalog. Wanneer u een profiel gegevens opneemt, worden de verzamelde gegevens berekend en opgenomen in het Hallo-metagegevens die zijn opgeslagen in de catalogus Hallo. Verzamelde gegevens kunt omvatten Hallo grootte van tabellen, Hallo percentage van null-waarden per kolom of Hallo minimum, maximum en gemiddelde waarden voor kolommen. 
>
>

> [!NOTE]
> Voor gegevensbronnen zoals SQL Server Analysis Services die u een eersteklas hebt **beschrijving** Hallo Data Catalog uitgepakt toepassing publiceren die eigenschapwaarde-eigenschap. Voor relationele databases van SQL Server, die een uitstekende gebrek **beschrijving** eigenschap Hallo Data Catalog publishing toepassing haalt uit Hallo Hallo waarde **ms_description** uitgebreide eigenschap voor objecten en kolommen. Zie voor meer informatie [met behulp van uitgebreide eigenschappen voor databaseobjecten](https://technet.microsoft.com/library/ms190243%28v=sql.105%29.aspx).
>
>

## <a name="how-long-should-it-take-for-newly-registered-assets-tooappear-in-hello-catalog"></a>Hoe lang moet het duren zojuist geregistreerde assets tooappear in Hallo catalogus?
Nadat u activa met Data Catalog registreert, kan er een periode van 5 seconden op too10 voordat ze worden weergegeven in Hallo Data Catalog-portal.

## <a name="how-do-i-annotate-and-enrich-hello-metadata-for-my-registered-data-assets"></a>Hoe ik aantekeningen toevoegen aan en verrijken Hallo metagegevens voor mijn geregistreerde gegevensassets?
Hallo eenvoudigste manier tooprovide metagegevens voor geregistreerde assets tooselect Hallo bedrijfsmiddel in Hallo Data Catalog-portal en Voer Hallo waarden voor het geselecteerde object Hallo in Hallo eigenschappendeelvenster of schema.

U kunt ook bepaalde metagegevens, zoals tags en experts tijdens het registratieproces Hallo opgeven. Hallo-waarden die u in het Hallo-publicatieservice Data Catalog opgeeft toepassing tooall activa op dat moment wordt geregistreerd. objecten tooview Hallo onlangs geregistreerd in de portal Hallo voor aanvullende opmerkingen, selecteer Hallo **Portal weergeven** knop op de laatste scherm Hallo Hallo publishing application Data Catalog.

## <a name="how-do-i-delete-my-registered-data-objects"></a>Hoe verwijder ik mijn objecten geregistreerde gegevens?
U kunt een object verwijderen uit de catalogus met gegevens door Hallo object selecteren in Hallo-portal en vervolgens te klikken op Hallo **verwijderen** knop. Hallo-object verwijderen Hiermee verwijdert u de metagegevens van Data Catalog, maar heeft geen invloed op de onderliggende gegevensbron Hallo.

## <a name="what-is-an-expert"></a>Wat is er een expert?
Een expert is een persoon die een perspectief op de hoogte over een gegevensobject heeft. Een object kan meerdere experts hebben. Een expert hoeft niet toobe Hallo 'eigenaar' voor een object, maar is gewoon iemand die weet hoe Hallo gegevens kan en moet worden gebruikt.

## <a name="how-do-i-share-information-with-hello-data-catalog-team-if-i-encounter-problems"></a>Hoe moet ik informatie delen met Hallo Data Catalog team als ik problemen?
problemen met tooreport informatie delen en vragen, Ga toohello [Azure Data Catalog forum](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).

## <a name="does-hello-catalog-work-with-another-data-source-that-im-interested-in"></a>Hallo catalogus werkt met een andere gegevensbron die ik ben?
We proberen actief over het toevoegen van meer gegevensbronnen tooData catalogus. Als u wilt dat een specifieke gegevensbron ondersteund toosee, raden deze (of stem de ondersteuning als deze al is voorgesteld) door te gaan toohello [Azure Data Catalog forum](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).

## <a name="how-is-azure-data-catalog-related-toohello-data-catalog-in-power-bi-for-office-365"></a>Wat is Azure Data Catalog verwante toohello catalogus met gegevens in Power BI voor Office 365?
U kunt Azure Data Catalog beschouwen als een evolutie van Hallo catalogus met gegevens in Power BI. Vanaf versie die voorjaar 2017 is Azure Data Catalog gebruikte tooenable Hallo delen en detectie van query's in Excel 2016 en Power Query voor Excel. Mogelijkheden van Data Catalog in Excel zijn beschikbaar toousers met Power BI Pro licenties.

## <a name="what-permissions-do-i-need-tooregister-assets-with-data-catalog"></a>Wat machtigingen doen ik tooregister activa met Data Catalog nodig?
hulpprogramma voor registratie toorun Hallo Data Catalog, moet u machtigingen op Hallo-gegevensbron waarmee u tooread Hallo metagegevens van Hallo bron. tooalso omvatten een preview, moet u gemachtigd waarmee u tooread in Hallo gegevens uit Hallo-objecten wordt geregistreerd.

## <a name="will-data-catalog-be-made-available-for-on-premises-deployment-as-well"></a>Data Catalog beschikbaar gesteld voor on-premises implementatie ook?
Data Catalog is een cloudservice die een oplossing voor hybride gegevensbron detectie met toodeliver bronnen zowel cloud als on-premises kunt werken. Er zijn momenteel geen plannen voor een versie van Data Catalog-service die wordt uitgevoerd op de lokale Hallo.

## <a name="can-i-extract-more-or-richer-metadata-from-hello-data-sources-i-register"></a>Kan ik meer of uitgebreidere metagegevens extraheren uit gegevensbronnen Hallo die ik registreren
We proberen actief tooexpand Hallo mogelijkheden van Data Catalog. Als u wilt dat de aanvullende metagegevens toohave opgehaald uit de gegevensbron Hallo tijdens de registratie, voorgesteld deze (of stem voor, als deze al is voorgesteld) in Hallo [Azure Data Catalog forum](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409). In toekomstige hello mag derde partijen tooadd nieuwe gegevensbrontypen via een API voor uitbreidbaarheid.

## <a name="how-do-i-restrict-hello-visibility-of-registered-data-assets-so-that-only-certain-people-can-discover-them"></a>Hoe beperk ik Hallo zichtbaarheid van geregistreerde gegevensassets, zodat alleen bepaalde personen kan ze detecteren?
Hallo gegevensassets in Hallo Data Catalog selecteren en klik vervolgens op Hallo **eigenaar** knop. Eigenaars van gegevensassets in Data Catalog kunnen wijzigen Hallo zichtbaarheid instellingen tooeither toestaan van alle gebruikers toodiscover Hallo activa eigendom of zichtbaarheid toospecific gebruikers beperken.

## <a name="how-do-i-update-hello-registration-for-a-data-asset-so-that-changes-in-hello-data-source-are-reflected-in-hello-catalog"></a>Hoe kan ik Hallo-registratie voor een gegevensasset bijwerken zodat de wijzigingen in gegevensbron Hallo worden doorgevoerd in de catalogus Hallo?
tooupdate hello metagegevens voor de gegevensassets die al zijn geregistreerd in de catalogus Hallo gewoon opnieuw Hallo gegevensbron registreren met Hallo activa. Eventuele wijzigingen in gegevensbron hello, zoals kolommen worden toegevoegd of verwijderd uit de tabellen of weergaven, worden bijgewerkt in de catalogus hello, maar alle aantekeningen die door gebruikers worden bewaard.

## <a name="my-question-isnt-answered-here-where-can-i-go-for-answers"></a>Mijn vraag niet wordt hier beantwoord. Waar kan ik voor antwoorden gaan?
Ga toohello [Azure Data Catalog forum](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409). Er vragen vindt u hier hun manier.
