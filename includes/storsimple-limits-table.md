<!--author=alkohli last changed: 12/15/15-->

| Limiet-id | Limiet | Opmerkingen |
| --- | --- | --- |
| Maximum aantal opslagaccountreferenties |64 | |
| Maximum aantal volumecontainers |64 | |
| Maximum aantal volumes |255 | |
| Maximum aantal planningen per bandbreedtesjabloon |168 |Een planning voor elk uur wordt elke dag van week hello (24 * 7). |
| Maximale grootte van een gelaagd volume op fysieke apparaten |64 TB voor 8100 en 8600 |8100 en 8600 zijn fysieke apparaten. |
| Maximale grootte van een gelaagd volume op virtuele apparaten in Azure |8010 30 TB <br></br> 64 TB voor de 8020 |8010 als de 8020 zijn virtuele apparaten in Azure die gebruikmaken van Standard-opslag- en Premium-opslag respectievelijk. |
| Maximale grootte van een lokaal vastgemaakt volume op een fysieke apparaten |9 TB voor 8100 <br></br> 24 TB voor 8600 |8100 en 8600 zijn fysieke apparaten. |
| Maximum aantal iSCSI-verbindingen |512 | |
| Maximum aantal verbindingen iSCSI-initiators |512 | |
| Maximum aantal access control records per apparaat |64 | |
| Maximum aantal volumes per back-upbeleid |24 | |
| Maximum aantal back-ups die per back-upbeleid worden bewaard |64 | |
| Maximum aantal planningen per back-upbeleid |10 | |
| Maximum aantal momentopnamen van elk type kunnen worden bewaard per volume |256 |Dit omvat lokale momentopnamen en cloud worden opgeslagen. |
| Maximum aantal momentopnamen die gebruikt in elk apparaat worden kunnen |10.000 | |
| Maximum aantal volumes die kunnen worden verwerkt in de parallelle back-up, herstel, of te klonen |16 |<ul><li>Als er meer dan 16 volumes, worden deze opeenvolgend verwerkt verwerking sleuven beschikbaar komen.</li><li>Nieuwe back-ups van een kloon of een herstelde gelaagd volume is pas mogelijk nadat het Hallo-bewerking is voltooid. Back-ups zijn echter voor een lokaal volume nadat Hallo volume online is toegestaan.</li></ul> |
| Terugzetten en herstellen tijd voor gelaagde volumes klonen |< 2 minuten |<ul><li>Hallo-volume wordt binnen twee minuten na het terugzetten of kloon bewerking, ongeacht de volumegrootte Hallo beschikbaar gesteld.</li><li>Hallo volume de prestaties in eerste instantie mogelijk langzamer dan normaal omdat de meeste Hallo gegevens en metagegevens is nog steeds bevindt zich in Hallo cloud. Prestaties kan verhogen als gegevensoverdrachten van Hallo cloud toohello StorSimple-apparaat.</li><li>Hallo totale tijd toodownload metagegevens is afhankelijk van Hallo volumegrootte toegewezen. Metagegevens is automatisch onder Hallo-apparaat op de achtergrond Hallo met Hallo frequentie van 5 minuten per TB aan volumegegevens toegewezen gebracht. Deze snelheid kan worden beïnvloed door Internet bandbreedte toohello cloud.</li><li>Hallo herstellen of de kloonbewerking is voltooid als alle Hallo metagegevens op Hallo-apparaat is.</li><li>Back-upbewerkingen kunnen niet worden uitgevoerd totdat Hallo herstellen of de kloonbewerking is volledig is voltooid. |
| Herstel de tijd voor lokaal vastgemaakte volumes herstellen |< 2 minuten |<ul><li>Hallo-volume wordt binnen twee minuten Hallo terugzetbewerking, ongeacht de volumegrootte Hallo beschikbaar gesteld.</li><li>Hallo volume de prestaties in eerste instantie mogelijk langzamer dan normaal omdat de meeste Hallo gegevens en metagegevens is nog steeds bevindt zich in Hallo cloud. Prestaties kan verhogen als gegevensoverdrachten van Hallo cloud toohello StorSimple-apparaat.</li><li>Hallo totale tijd toodownload metagegevens is afhankelijk van Hallo volumegrootte toegewezen. Metagegevens is automatisch onder Hallo-apparaat op de achtergrond Hallo met Hallo frequentie van 5 minuten per TB aan volumegegevens toegewezen gebracht. Deze snelheid kan worden beïnvloed door Internet bandbreedte toohello cloud.</li><li>In tegenstelling tot gelaagde volumes, in geval van lokaal vastgemaakte volumes Hallo wordt Hallo volumegegevens ook lokaal gedownload op Hallo-apparaat. Hallo restore-bewerking is voltooid als alle Hallo volumegegevens toohello apparaat weer.</li><li>Hallo herstelbewerkingen mogelijk lang en Hallo totale tijd toocomplete Hallo terugzetten is afhankelijk van de Hallo-grootte van lokaal volume Hallo ingericht, uw internetbandbreedte en Hallo bestaande gegevens op Hallo-apparaat. Back-upbewerkingen op Hallo lokaal vastgemaakt volume zijn toegestaan terwijl het Hallo-herstelbewerking wordt uitgevoerd. |
| Beschikbaarheid van thin-herstel |Laatste failover | |
| Maximum aantal clients lezen/schrijven doorvoer (wanneer aangeboden via Hallo SSD-laag) * |920/720 MB/s met een enkele 10GbE netwerkinterface |Up too2x met MPIO en twee netwerkinterfaces. |
| Maximum aantal clients lezen/schrijven doorvoer (wanneer aangeboden via Hallo HDD-laag) * |120/250 MB/s | |
| Maximum aantal clients lezen/schrijven doorvoer (wanneer aangeboden via Hallo cloudlaag) * |11/41 MB/s |Lees doorvoer is afhankelijk van clients genereren en bijhouden van voldoende i/o-wachtrijdiepte. |

&#42; Maximale doorvoer per i/o-type is gemeten met 100 procent lezen en schrijven van 100 procent scenario's. Werkelijke doorvoer mogelijk lager en is afhankelijk van i/o mix en de voorwaarden.

