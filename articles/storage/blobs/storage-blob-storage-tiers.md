---
title: aaaAzure hot, koel, en archiefopslag voor blobs | Microsoft Docs
description: Hot, Cool en Archive Storage voor Azure Blob Storage-accounts.
services: storage
documentationcenter: 
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: eb33ed4f-1b17-4fd6-82e2-8d5372800eef
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/05/2017
ms.author: mihauss
ms.openlocfilehash: 42fb699bf16147ba8a4d9f75a62debadea5af65e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-blob-storage-hot-cool-and-archive-preview-storage-tiers"></a>Azure Blob Storage: Hot, Cool en Archive (preview) Storage-lagen

## <a name="overview"></a>Overzicht

Azure Storage biedt twee opslaglagen voor de opslag van blob-objecten, zodat u gegevens zeer voordelig kunt opslaan afhankelijk van hoe u deze gebruikt. Hello Azure **hot storage-laag** is geoptimaliseerd voor het opslaan van gegevens die regelmatig worden geopend. Hello Azure **cool storage-laag** is geoptimaliseerd voor het opslaan van gegevens die minder vaak wordt geopend en opgeslagen voor ten minste een maand. Hallo [archief storage-laag (preview)](https://azure.microsoft.com/blog/announcing-the-public-preview-of-azure-archive-blob-storage-and-blob-level-tiering) is geoptimaliseerd voor het opslaan van gegevens die zelden wordt geopend en opgeslagen voor ten minste zes maanden met flexibele latentievereisten (op volgorde Hallo van uur). Hallo *archief* storage-laag kan alleen worden gebruikt op Hallo blob niveau en niet op het hele opslagaccount Hallo. Gegevens in de cool storage-laag Hallo tolereert iets lagere beschikbaarheid, maar nog steeds vereist hoge duurzaamheid en vergelijkbare kenmerken voor de tijd voor toegang en doorvoer als hot gegevens. Voor gegevens in de Cool en Archive Storage-laag zijn een SLA met een iets lagere beschikbaarheid en hogere toegangskosten aanvaardbaar vanwege de veel lagere opslagkosten.

Gegevens die zijn opgeslagen in de cloud Hallo groeit vandaag de dag exponentieel. toomanage kosten voor uw groeiende opslagbehoeften, is het handig tooorganize uw gegevens op basis van kenmerken, zoals de frequentie van toegang en geplande bewaarperiode. Gegevens die zijn opgeslagen in de cloud Hallo kan afwijken in termen van hoe deze wordt gegenereerd, verwerkt en toegankelijk is via de levensduur. Sommige gegevens worden tijdens hun hele levensduur actief geopend en gewijzigd. Sommige gegevens wordt vaak vroeg in de levensduur geopend met verstrijkt, aanzienlijk als Hallo gebeurt. Sommige gegevens in de cloud Hallo inactief blijft en zelden, als ooit geopend eenmaal opgeslagen.

Het is nuttig om voor elk van deze scenario‘s voor toegang tot gegevens een gedifferentieerde opslaglaag te maken die is geoptimaliseerd voor een specifiek toegangspatroon. Door middel van de lagen Hot, Cool en Archive Storage wordt in Azure Blob Storage voorzien in deze behoefte aan gedifferentieerde opslaglagen met afzonderlijke prijsmodellen.

## <a name="blob-storage-accounts"></a>Blob Storage-accounts

**Blob Storage-accounts** zijn gespecialiseerde opslagaccounts voor het opslaan van ongestructureerde gegevens als blobs (objecten) in Azure Storage. Met Blob storage-accounts, kunt u nu kiezen tussen hot en cool opslaglagen op niveau van de account of heet cool en lagen op Hallo blob niveau, op basis van toegangspatronen archiveren. Uw zelden gebruikte koude gegevens tegen Hallo laagste opslagkosten, minder regelmatig geopende gegevens tegen lagere opslagkosten kosten dan hot en regelmatiger geopende gegevens tegen Hallo laagste toegangskosten opslaan opslaan. BLOB storage-accounts zijn vergelijkbaar tooyour bestaande opslagaccounts en delen Hallo geweldige duurzaamheid, beschikbaarheid, schaalbaarheid en prestatiefuncties waarmee u vandaag, inclusief 100 procent API-consistentie voor blok-blobs en toevoeg- BLOBs.

> [!NOTE]
> Blob Storage-accounts ondersteunen alleen blok-blobs en toevoeg-blobs. Pagina-blobs worden niet ondersteund.

BLOB storage-accounts beschikbaar Hallo **Toegangslaag** kenmerk waarmee u toospecify Hallo storage-laag als **Hot** of **Cool** afhankelijk van het Hallo-gegevens die zijn opgeslagen in Hallo account. Als er een wijziging in het gebruikspatroon Hallo van uw gegevens, kunt u ook schakelen tussen deze opslaglagen op elk gewenst moment. Hallo archief laag (preview) kan alleen worden toegepast op Hallo blob-niveau.

> [!NOTE]
> Veranderende Hallo storage-laag kan leiden tot extra kosten. Zie Hallo [prijzen en facturering](#pricing-and-billing) sectie voor meer informatie.

### <a name="hot-access-tier"></a>Hot Storage-toegangslaag

Voorbeeld gebruiksscenario's voor Hallo hot storage-laag omvatten:

* Gegevens die in gebruik of de verwachte toobe regelmatig worden geopend (Lees- en schrijfbewerkingen).
* Gegevens die tijdelijk worden opgeslagen voor verwerking en uiteindelijk migratie toohello cool storage-laag.

### <a name="cool-access-tier"></a>Cool Storage-toegangslaag

Voorbeeld gebruiksscenario's voor Hallo cool storage-laag omvatten:

* Gegevenssets waarvan voor de korte termijn een back-up is gemaakt en die na een noodgeval zijn hersteld.
* Oudere media-inhoud is niet meer regelmatig wordt bekeken maar verwachte toobe beschikbaar is bij direct toegankelijk.
* Grote gegevenssets waarvoor toobe opgeslagen kosten effectief terwijl er meer gegevens worden verzameld voor toekomstige verwerking. (*Bijvoorbeeld*: langetermijnopslag van wetenschappelijke gegevens, onbewerkte telemetriegegevens van een productiefaciliteit)

### <a name="archive-access-tier-preview"></a>Archive Storage-toegangslaag (preview)

[Archiefopslag](https://azure.microsoft.com/blog/announcing-the-public-preview-of-azure-archive-blob-storage-and-blob-level-tiering) heeft de laagste opslag Hallo kosten en hogere kosten vergeleken toohot van de gegevens voor het ophalen en cool storage.

Een blob in Archive Storage kan niet worden gelezen, gekopieerd, overschreven of gewijzigd. Ook kunt u geen momentopnamen maken van een blob in Archive Storage. U kan echter bestaande operations toodelete gebruiken, weergeven, blobmetagegevens eigenschappen ophalen of Hallo laag van uw blob wijzigen. tooread gegevens in archiefopslag, moet u eerst Hallo laag van Hallo blob toohot of coolbar wijzigen. Dit proces staat bekend als rehydratering en een too15 uren toocomplete voor blobs die kleiner is dan 50 GB in beslag kan nemen. Extra tijd die nodig is voor grotere blobs varieert met Hallo blob doorvoer limiet.

Tijdens de rehydratering Controleer Hallo 'archief status' blob-eigenschap tooconfirm als Hallo laag is gewijzigd. Hallo status leest 'rehydrate in behandeling zijnde-naar-hot-' of 'rehydrate-in behandeling zijnde-naar-coolbar', afhankelijk van Hallo bestemming laag. Blob-eigenschap weerspiegelt van voltooiing, Hallo blob-eigenschap 'archiveren status' wordt verwijderd en wat Hallo 'laag' hello hot of cool laag.  

Voorbeeld gebruiksscenario's voor Hallo archief opslaglaag zijn onder andere:

* Gegevenssets waarvan voor de lange termijn een back-up is gemaakt, die zijn gearchiveerd of die na een noodgeval zijn hersteld.
* Oorspronkelijke (onbewerkte) gegevens die moeten worden bewaard, zelfs nadat deze zijn verwerkt tot hun uiteindelijke, bruikbare vorm. (*Bijvoorbeeld*: onbewerkte mediabestanden na transcodering naar andere indelingen)
* Compatibiliteit en archivering van gegevens die u moet beschikken over toobe gedurende een lange periode zijn opgeslagen en bijna nooit worden geopend. (*Bijvoorbeeld*: beeldmateriaal van beveiligingscamera‘s, oude röntgenfoto‘s/MRI‘s in ziekenhuizen, geluidsopnamen en transcripties van verkoopgesprekken voor financiële diensten)

### <a name="recommendations"></a>Aanbevelingen

Zie [Over Azure Storage-accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) voor meer informatie over opslagaccounts.

Voor toepassingen die alleen blok- of toevoeg-blob-opslag, wordt aangeraden Blob storage-accounts, tootake profiteren van Hallo gedifferentieerde prijsmodel voor gelaagde opslag. We begrijpen dat dit mogelijk niet worden onder bepaalde omstandigheden waarin algemene opslag accounts zou worden Hallo manier toogo, zoals:

* U moet toouse tabellen, wachtrijen of bestanden en wilt dat uw blobs die zijn opgeslagen in hetzelfde opslagaccount Hallo. Houd er rekening mee dat er is geen technisch voordeel toostoring in Hallo die dezelfde account anders dan dat Hallo dezelfde sleutels gedeelde.

* U moet nog steeds toouse Hallo klassieke implementatiemodel. BLOB storage-accounts zijn alleen beschikbaar via hello Azure Resource Manager-implementatiemodel.

* U moet toouse pagina-blobs. Blob Storage-accounts bieden geen ondersteuning voor pagina-blobs. Over het algemeen raden we het gebruik van blok-blobs aan, tenzij u specifiek behoefte hebt aan pagina-blobs.

* U gebruikt een versie van Hallo [REST-API voor Storage Services](https://msdn.microsoft.com/library/azure/dd894041.aspx) die ouder is dan 2014-02-14 of een clientbibliotheek met een versie lager dan 4.x en uw toepassing niet bijwerken.

> [!NOTE]
> Blob Storage-accounts worden momenteel ondersteund in alle Azure-regio's.
 

## <a name="blob-level-tiering-feature-preview"></a>Toegangslagen op blob-niveau (preview)

BLOB-niveau lagen kunt u nu toochange Hallo laag van uw gegevens op Hallo objectniveau met een eenmalige bewerking aangeroepen [Blob laag ingesteld](/rest/api/storageservices/set-blob-tier). U kunt eenvoudig hello toegangslaag van een blob tussen Hallo hot, cool of archief lagen als gebruikspatronen wijziging, zonder toomove gegevens tussen accounts wijzigen. Alle laagwijzigingen vinden direct plaats, behalve wanneer een blob wordt gerehydrateerd uit Archive Storage. BLOBs in alle drie opslag lagen kunnen naast elkaar bestaan binnen hetzelfde account Hallo. Elke blob die geen een expliciet toegewezen laag overgenomen Hallo laag van Hallo account toegangsinstelling laag.

toouse deze functies in preview Hallo instructies in Hallo [Azure archief en de Blob-niveau lagen blog aankondiging](https://azure.microsoft.com/blog/announcing-the-public-preview-of-azure-archive-blob-storage-and-blob-level-tiering).

Hallo Volg vindt u enkele beperkingen die van toepassing tijdens de preview voor blob-niveau lagen:

* Alleen nieuwe Blob Storage-accounts die zijn gemaakt in VS Oost 2 en waarvoor de preview-inschrijving is geslaagd, ondersteunen archiefopslag.

* Alleen nieuwe Blob Storage-accounts die zijn gemaakt in openbare regio's en waarvoor de preview-inschrijving is geslaagd, ondersteunen toegangslagen op blob-niveau.

* Toegangslagen op blob-niveau en archiefopslag worden alleen ondersteund in [LRS](../common/storage-redundancy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#locally-redundant-storage)-opslag. [GRS](../common/storage-redundancy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#geo-redundant-storage) en [RA-GRS](../common/storage-redundancy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#read-access-geo-redundant-storage) worden ondersteund in toekomstige Hallo.

* U kunt Hallo laag van een blob met de momentopnamen niet wijzigen.

* U mag een blob in archiefopslag niet kopiëren of er een momentopname van maken.

## <a name="comparison-of-hello-storage-tiers"></a>Vergelijking van opslaglagen Hallo

Hallo volgende tabel bevat een vergelijking van Hallo hot en cool storage-laag. Hallo archief blob-niveau tier is preview, dus er zijn geen serviceovereenkomsten voor deze.

| | **Hot Storage-laag** | **Cool Storage-laag** |
| ---- | ----- | ----- |
| **Beschikbaarheid** | 99,9% | 99% |
| **Beschikbaarheid** <br> **(RA-GRS-leesbewerkingen)**| 99,99% | 99,9% |
| **Gebruikskosten** | Hogere opslagkosten, lagere toegangs- en transactiekosten | Lagere opslagkosten, hogere toegangs- en transactiekosten |
| **Minimale objectgrootte** | N.v.t. | N.v.t. |
| **Minimale opslagduur** | N.v.t. | N.v.t. |
| **Latentie** <br> **(Tijd toofirst byte)** | milliseconden | milliseconden |
| **Schaalbaarheids- en prestatiedoelen** | Dezelfde als bij opslagaccounts voor algemeen gebruik | Dezelfde als bij opslagaccounts voor algemeen gebruik |

> [!NOTE]
> BLOB storage accounts ondersteuning Hallo dezelfde prestaties en schaalbaarheid doelen als opslagaccounts voor algemeen gebruik. Zie [Schaalbaarheids- en prestatiedoelen in Azure Storage](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) voor meer informatie.


## <a name="pricing-and-billing"></a>Prijzen en facturering
BLOB storage-accounts gebruiken een prijsmodel voor blob-opslag op basis van Hallo storage-laag. Wanneer u een Blob storage-account, Hallo volgende factureringsvoorwaarden van toepassing:

* **Opslagkosten**: bovendien toohello hoeveelheid opgeslagen gegevens Hallo kosten voor het opslaan van gegevens varieert afhankelijk van Hallo storage-laag. de kosten per GB Hallo is lagere voor Hallo cool storage-laag dan voor Hallo hot storage-laag.

* **Data access-kosten**: voor gegevens in de cool storage-laag Hallo u worden in rekening gebracht per GB gegevens toegang kosten met zich mee voor lees- en schrijfbewerkingen.

* **Transactiekosten**: voor beide lagen worden kosten in rekening gebracht per transactie. Kosten per transactie zijn Hallo voor Hallo cool storage-laag is echter hoger dan voor Hallo hot storage-laag.

* **Kosten voor gegevensoverdracht geo-replicatie**: dit is alleen van toepassing tooaccounts waarvoor geo-replicatie is geconfigureerd, inclusief GRS en RA-GRS. Kosten voor gegevensoverdracht met geo-replicatie worden in rekening gebracht per GB.

* **Kosten voor uitgaande gegevensoverdracht**: uitgaande gegevensoverdracht (gegevens die buiten een Azure-regio worden overgedragen) worden gefactureerd voor bandbreedtegebruik per GB, net zoals bij opslagaccounts voor algemeen gebruik.

* **Veranderende Hallo opslaglaag**: een kosten gelijk tooreading alle Hallo bestaande gegevens in Hallo storage-account voor elke overgang als Hallo opslaglaag wijzigt van cool toohot maakt. Daarentegen als Hallo opslaglaag wijzigt van hot toocool is op Hallo gratis.

> [!NOTE]
> Zie voor meer informatie over prijzen voor Blob storage-accounts Hallo [prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/storage/) pagina. Zie voor meer informatie over Hallo uitgaande gegevensoverdracht kosten [prijsinformatie over gegevensoverdracht](https://azure.microsoft.com/pricing/details/data-transfers/) pagina.

## <a name="quickstart"></a>Snelstartgids

In deze sectie ziet u Hallo volgen scenario's die gebruikmaken van hello Azure-portal:

* Hoe toocreate een Blob storage-account.
* Hoe toomanage een Blob storage-account.

U kunt Hallo toegang laag tooarchive niet instellen in Hallo volgen voorbeelden omdat deze instelling toohello hele storage-account geldt. Archive Storage kan alleen worden ingesteld voor een specifieke blob.

### <a name="create-a-blob-storage-account-using-hello-azure-portal"></a>Een Blob storage-account maken met hello Azure-portal

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).

2. Selecteer op de Hub-menu Hallo **nieuw** > **gegevens en opslag** > **opslagaccount**.

3. Voer een naam in voor het opslagaccount.
   
    Deze naam moet globaal uniek zijn. het wordt gebruikt als onderdeel van Hallo-URL van tooaccess Hallo objecten in Hallo storage-account gebruikt.  

4. Selecteer **Resource Manager** als Hallo-implementatiemodel.
   
    Gelaagde opslag kan alleen worden gebruikt met Resource Manager-opslagaccounts; Dit is Hallo aanbevolen implementatiemodel voor nieuwe resources. Bekijk voor meer informatie Hallo [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).  

5. Selecteer in de vervolgkeuzelijst Hallo soort Account, **Blob Storage**.
   
    Dit is waar u Hallo type opslagaccount selecteren. Gelaagde opslag is niet beschikbaar in de opslagaccount; Dit is alleen beschikbaar in Hallo Blob storage-type account.     
   
    Houd er rekening mee dat wanneer u deze optie selecteert, Hallo prestatielaag ingesteld tooStandard. Gelaagde opslag is niet beschikbaar met de prestatielaag van Hallo Premium.

6. Selecteer de replicatieoptie Hallo voor Hallo storage-account: **LRS**, **GRS**, of **RA-GRS**. Hallo standaardwaarde is **RA-GRS**.
   
    LRS = lokaal redundante opslag; GRS = geografisch redundante opslag (2 regio's); RA-GRS is geografisch redundante opslag met leestoegang (2 regio's met lees access toohello seconde).
   
    Zie [Azure Storage-replicatie](../common/storage-redundancy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) voor meer informatie over Azure Storage-replicatieopties.

7. Selecteer Hallo rechts storage-laag voor uw behoeften: Set Hallo **toegangslaag** tooeither **Cool** of **Hot**. Hallo standaardwaarde is **Hot**. 

8. Hallo-abonnement waaraan u toocreate Hallo nieuw opslagaccount wilt selecteren.

9. Geef een nieuwe resourcegroep op of selecteer een bestaande resourcegroep. Zie [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md) (Overzicht van Azure Resource Manager) voor meer informatie over resourcegroepen.

10. Hallo-regio voor uw storage-account selecteren.

11. Klik op **maken** toocreate Hallo storage-account.

### <a name="change-hello-storage-tier-of-a-blob-storage-account-using-hello-azure-portal"></a>Hallo storage-laag van een Blob storage-account met behulp van hello Azure-portal wijzigen

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).

2. toonavigate tooyour storage-account, selecteert u alle Resources, en selecteer vervolgens uw storage-account.

3. Klik op de blade instellingen hello, **configuratie** Hallo-accountconfiguratie tooview en/of wijzigen.

4. Selecteer Hallo rechts storage-laag voor uw behoeften: Set Hallo **toegangslaag** tooeither **Cool** of **Hot**...

5. Klik op Opslaan Hallo boven aan het Hallo-blade.

> [!NOTE]
> Veranderende Hallo storage-laag kan leiden tot extra kosten. Zie Hallo [prijzen en facturering](#pricing-and-billing) sectie voor meer informatie.


## <a name="evaluating-and-migrating-tooblob-storage-accounts"></a>Evalueren en het migreren van tooBlob storage-accounts
Hallo doel van deze sectie is toohelp gebruikers toomake een vloeiende overgang toousing Blob storage-accounts. Er zijn twee scenario's voor gebruikers:

* U hebt een bestaande opslagaccounts voor algemeen gebruik-account en een wijziging tooa Blob storage-account met de juiste opslaglaag Hallo tooevaluate wilt.
* U hebt besloten toouse een Blob storage-account of al een en wilt tooevaluate of moet u Hallo hot of cool storage-laag.

In beide gevallen Hallo eerste volgorde van zakelijke tooestimate Hallo kosten voor het opslaan van en toegang tot uw gegevens opgeslagen in een Blob storage-account is en die worden vergeleken op basis van uw huidige kosten.

## <a name="evaluating-blob-storage-account-tiers"></a>Lagen voor Blob Storage-accounts evalueren

In de volgorde tooestimate Hallo kosten van het opslaan van en toegang tot gegevens die zijn opgeslagen in een Blob storage-account, of u kunt tooevaluate uw bestaande gebruikspatroon bij benadering de verwachte gebruikspatroon. In het algemeen kunt u tooknow:

* Wat is het gebruik van de opslag? Hoeveel gegevens worden er opgeslagen en hoe wijzigt dit maandelijks?

* Uw opslag toegangstijden - hoeveel gegevens worden van de gelezen en geschreven toohello-account (inclusief nieuwe gegevens)? Hoeveel transacties worden gebruikt voor toegang tot gegevens? En wat voor soort transacties zijn dit?

## <a name="monitoring-existing-storage-accounts"></a>Bewaking van bestaande opslagaccounts

toomonitor uw bestaande opslagruimte, accounts en deze gegevens te verzamelen, kunt u het gebruik van Azure Storage Analytics waardoor voert logboekregistratie en metrische gegevens voor een opslagaccount. Storage Analytics metrische gegevens die samengevoegde statistieken en capaciteit transactiegegevens over aanvragen toohello Blob storage-service voor zowel opslagaccounts als Blob storage-accounts zijn kunnen worden opgeslagen. Deze gegevens worden opgeslagen in een bekende tabellen in Hallo hetzelfde opslagaccount.

Raadpleeg voor meer informatie [About Storage Analytics Metrics](https://msdn.microsoft.com/library/azure/hh343258.aspx) (Metrische gegevens in Storage Analytics) en [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx) (Tabelschema van metrische gegevens in Storage Analytics).

> [!NOTE]
> BLOB storage-accounts beschikbaar Hallo tabel service-eindpunt alleen voor het opslaan en openen van Hallo metrische gegevens voor dat account.

Hallo opslagverbruik toomonitor voor Hallo Blob storage-service, moet u tooenable hello capaciteitsmetrieken.
Dit is ingeschakeld, capaciteitsgegevens dagelijks voor de Blob-service een opslagaccount worden vastgelegd en geregistreerd als een vermelding die is geschreven toohello *$MetricsCapacityBlob* tabel binnen Hallo dezelfde storage-account.

toomonitor hello gegevenstoegangspatroon voor Hallo Blob storage-service, moet u tooenable Hallo per uur transactie metrische gegevens op een API-niveau. Met deze ingeschakeld per API transacties worden samengevoegd om het uur, en geregistreerd als een vermelding die is geschreven toohello *$MetricsHourPrimaryTransactionsBlob* tabel binnen Hallo hetzelfde opslagaccount. Hallo *$MetricsHourSecondaryTransactionsBlob* tabelrecords Hallo transacties toohello secundair eindpunt bij gebruik van RA-GRS-accounts voor opslag.

> [!NOTE]
> Als u een algemeen opslagaccount hebt waarin u pagina-blobs en virtuele-machineschijven hebt opgeslagen naast blok- en toevoegblobgegevens, is dit schattingsproces niet van toepassing. Dit komt doordat er geen enkele manier capaciteit onderscheid te maken en transactie metrische gegevens op basis van Hallo type blob voor alleen blokkeren en toevoeg-blobs die kunnen worden gemigreerd tooa Blob storage-account.

een goede benadering van uw gegevens gebruiks- en toegangspatroon tooget, wordt aangeraden u kiest een bewaarperiode voor Hallo metrische gegevens die representatief is voor het gebruik van uw normale en afleiden. Een mogelijkheid is tooretain Hallo metrische gegevens voor 7 dagen en gegevens verzamelen Hallo elke week voor analyse aan Hallo einde van Hallo maand. Een andere optie tooretain Hallo metrische gegevens voor Hallo is afgelopen 30 dagen en verzamelen en analyseren van gegevens Hallo Hallo na 30 dagen Hallo.

Voor meer informatie over het inschakelen, verzamelen en weergeven van metrische gegevens, raadpleegt u [Enabling Azure Storage metrics and viewing metrics data](../common/storage-enable-and-view-metrics.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) (Metrische gegevens voor Azure Storage inschakelen en metrische gegevens weergeven).

> [!NOTE]
> Het opslaan, openen en downloaden van analytische gegevens wordt op dezelfde manier in rekening gebracht als normale gebruikersgegevens.

### <a name="utilizing-usage-metrics-tooestimate-costs"></a>Met metrische gegevens tooestimate gebruikskosten

### <a name="storage-costs"></a>Opslagkosten

meest recente vermelding in de Hallo capaciteit metrische gegevens tabel Hallo *$MetricsCapacityBlob* met Hallo rijsleutel *'data'* toont Hallo opslagcapaciteit verbruikt door gebruikersgegevens. meest recente vermelding in de Hallo capaciteit metrische gegevens tabel Hallo *$MetricsCapacityBlob* met Hallo rijsleutel *'analytics'* toont Hallo opslagcapaciteit verbruikt door Hallo analytics Logboeken.

Deze totale capaciteit is verbruikt door beide gebruiker gegevens en analyse-Logboeken (indien ingeschakeld) vervolgens kan worden gebruikt tooestimate Hallo kosten voor het opslaan van gegevens in Hallo storage-account. Hallo dezelfde methode kan ook worden gebruikt voor het schatten van de opslagkosten voor blok- en toevoeg-blobs in opslagaccounts.

### <a name="transaction-costs"></a>Transactiekosten

Hallo som van *'TotalBillableRequests'*, in alle items voor een API in Hallo transactie geeft metrische gegevens tabel Hallo kunt u het totale aantal transacties voor die bepaalde API. *Bijvoorbeeld*, totaalaantal Hallo *'GetBlob'* transacties in een bepaalde periode kunnen worden berekend door Hallo som van de totale factureerbare aanvragen voor alle vermeldingen met Hallo rijsleutel *' gebruiker. GetBlob'*.

In de volgorde tooestimate transactiekosten voor Blob storage-accounts moet u toobreak omlaag Hallo transacties in drie groepen omdat ze anders zijn berekend.

* Schrijftransacties zoals *'PutBlob'*, *'PutBlock'*, *'PutBlockList'*, *'AppendBlock'*, *'ListBlobs'*, *'ListContainers'*, *'CreateContainer'*, *'SnapshotBlob'* en *'CopyBlob'*.
* Verwijdertransacties zoals *'DeleteBlob'* en *'DeleteContainer'*.
* Alle andere transacties.

In de volgorde tooestimate transactiekosten voor opslagaccounts voor algemeen gebruik moet u tooaggregate alle transacties ongeacht Hallo bewerking/API.

### <a name="data-access-and-geo-replication-data-transfer-costs"></a>Gegevenstoegang en overdrachtskosten voor geo-replicatiegegevens

Hoewel storage analytics geen biedt Hallo hoeveelheid gegevens gelezen uit en geschreven tooa storage-account, deze kan worden ongeveer geschat door te kijken Hallo transactie metrische gegevens tabel. Hallo som van *'TotalIngress'* in alle items voor een API in Hallo transactie metrische gegevens geeft tabel Hallo totale hoeveelheid inkomend gegevens in bytes voor die bepaalde API. Op dezelfde manier Hallo som van *'TotalEgress'* geeft Hallo totale hoeveelheid uitgaande gegevens, in bytes.

In de volgorde tooestimate Hallo gegevens toegangskosten voor Blob storage-accounts moet u toobreak omlaag Hallo transacties in twee groepen. 

* Hallo en de hoeveelheid gegevens die zijn opgehaald uit Hallo storage-account kan worden geschat door te kijken Hallo som van *'TotalEgress'* voor voornamelijk Hallo *'GetBlob'* en *'CopyBlob'* bewerkingen.

* Hallo en de hoeveelheid gegevens geschreven toohello storage-account kan worden geschat door te kijken Hallo som van *'TotalIngress'* voor voornamelijk Hallo *'PutBlob'*, *'PutBlock'*, *'CopyBlob'* en *'AppendBlock'* bewerkingen.

Hallo kosten van de gegevensoverdracht geo-replicatie voor Blob storage-accounts kunnen worden berekend met behulp van Hallo schatting voor Hallo en de hoeveelheid gegevens geschreven wanneer een GRS of RA-GRS-opslagaccount gebruikt.

> [!NOTE]
> Voor een meer gedetailleerd voorbeeld over het berekenen van de kosten voor het gebruik van Hallo hot of cool storage-laag Hallo, bekijk Hallo Veelgestelde vragen over met de titel *'wat Hot en Cool toegangslagen zijn en hoe moet ik bepalen welke één toouse?'* in Hallo [Azure Storage-prijzen pagina](https://azure.microsoft.com/pricing/details/storage/).
 
## <a name="migrating-existing-data"></a>Bestaande gegevens migreren

Een Blob Storage-account is speciaal bedoeld voor het opslaan van blok-blobs en toevoeg-blobs. Bestaande opslagaccounts, waarmee u toostore tabellen, wachtrijen, bestanden en schijven, evenals blobs, niet geconverteerd tooBlob storage-accounts. toouse Hallo opslaglagen, u nieuwe Blob storage-accounts toocreate nodig hebt en uw bestaande gegevens migreren naar nieuw gemaakte Hallo-accounts.

Kunt u de volgende methoden toomigrate bestaande gegevens in Blob storage-accounts van lokale opslagapparaten, van derden cloudopslagproviders of uw bestaande opslagaccounts in Azure Hallo gebruiken:

### <a name="azcopy"></a>AzCopy

AzCopy is een Windows-opdrachtregelprogramma ontworpen voor high-performance kopiëren van gegevens tooand uit Azure Storage. U kunt AzCopy toocopy-gegevens in Blob storage-account van uw bestaande opslagaccounts of tooupload van uw opslag on-premises apparaten in Blob storage-account gebruiken.

Zie voor meer informatie [gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

### <a name="data-movement-library"></a>Bibliotheek voor gegevensverplaatsing

Azure Storage-bibliotheek voor gegevensverplaatsing voor .NET is gebaseerd op Hallo data movement basisschema die ook door AzCopy. Hallo-bibliotheek is ontworpen voor high-performance, betrouwbare, en eenvoudige gegevensoverdracht vergelijkbaar tooAzCopy bewerkingen. Hiermee kunt u tootake voordelen van Hallo functies die AzCopy in uw toepassing systeemeigen zonder toodeal aan het uitvoeren en controleren van externe exemplaren van AzCopy.

Zie [Bibliotheek voor gegevensverplaatsing van Azure Storage voor .Net](https://github.com/Azure/azure-storage-net-data-movement) voor meer informatie.

### <a name="rest-api-or-client-library"></a>REST-API of clientbibliotheek

U kunt een aangepaste toepassing toomigrate van uw gegevens naar een Blob storage-account met behulp van een Azure-clientbibliotheken Hallo maken of Hallo REST-API van Azure storage-services. Azure Storage biedt uitgebreide clientbibliotheken voor meerdere talen en platforms, zoals  .NET, Java, C++, Node.JS, PHP, Ruby en Python. Hallo-clientbibliotheken bieden geavanceerde mogelijkheden, zoals Pogingslogica, logboekregistratie en parallelle uploads. U kunt ook rechtstreeks met de REST-API kan worden aangeroepen door elke taal waarin HTTP/HTTPS-aanvragen Hallo ontwikkelen.

Zie [Aan de slag met Azure Blob Storage](storage-dotnet-how-to-use-blobs.md) voor meer informatie.

> [!NOTE]
> BLOBs die zijn versleuteld met behulp van versleuteling aan clientzijde opslaan versleutelingsgerelateerde metagegevens die zijn opgeslagen met Hallo blob. Het is absoluut essentieel dat kopiëren ervoor zorgen moet dat Hallo blobmetagegevens, en vooral Hallo versleutelingsgerelateerde metagegevens, blijft behouden. Als u blobs Hallo zonder deze metagegevens kopieert, kan Hallo blob-inhoud niet opnieuw worden opgehaald. Zie [Azure Storage-versleuteling aan de clientzijde](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) voor meer informatie over versleutelingsgerelateerde metagegevens.
 
## <a name="faq"></a>Veelgestelde vragen

1. **Zijn de bestaande opslagaccounts nog steeds beschikbaar?**
   
    Ja, de bestaande opslagaccounts zijn nog steeds beschikbaar. De prijs en de functionaliteit hiervan zijn niet gewijzigd.  Ze hebben geen Hallo mogelijkheid toochoose storage-laag en wordt geen toegangslagen in toekomstige Hallo.

2. **Waarom en wanneer is het een goed idee om Blob Storage-accounts te gebruiken?**
   
    BLOB storage-accounts zijn speciaal bedoeld voor het opslaan van blobs en kunnen we toointroduce nieuwe blobfuncties mogelijk. Voortaan kunt zijn Blob storage-accounts Hallo aanbevolen manier voor het opslaan van blobs, als toekomstige mogelijkheden bijvoorbeeld hiërarchische opslag en lagen worden ingevoerd op basis van dit accounttype. Het is echter up tooyou helemaal zelf wanneer u toomigrate op basis van uw zakelijke vereisten.

3. **Kan ik mijn bestaande storage account tooa Blob storage-account converteren**
   
    Nee. Een Blob Storage-account is een ander soort opslagaccount. Daarom moet u dit account afzonderlijk maken en dient u de gegevens naar dit account te migreren zoals eerder is uitgelegd.

4. **Kan ik objecten opslaan in beide opslaglagen in Hallo hetzelfde account?**
   
    Hallo *'Laag'* kenmerk geeft Hallo-waarde van de opslaglaag Hallo op accountniveau ingesteld en tooall objecten in het account is van toepassing. Echter Hallo blob-niveau lagen (preview)-functie kunt u tooset hello toegangslaag op specifieke blobs en Hallo toegangsinstelling laag op Hallo-account, worden hiermee overschreven. 

5. **Kan ik Hallo storage-laag van mijn Blob storage-account wijzigen?**
   
    Ja. U kunt Hallo opslaglaag wijzigen door Hallo instelling *'Laag'* -kenmerk op Hallo storage-account. Veranderende Hallo storage-laag geldt tooall-objecten die zijn opgeslagen in het Hallo-account. Veranderende Hallo storage-laag van hot toocool veroorzaakt eventuele kosten tijdens het wijzigen van cool toohot heeft gevolgen voor een per GB kosten voor het lezen van gegevens van alle Hallo Hallo-account.

6. **Hoe vaak kan ik Hallo storage-laag van mijn Blob storage-account wijzigen?**
   
    Terwijl we doen geen beperking op hoe vaak Hallo storage-laag kan worden gewijzigd, houd er rekening mee dat als Hallo opslaglaag wijzigt van cool toohot kan aanzienlijke kosten worden. We raden niet Hallo opslaglaag vaak wijzigen.

7. **Hallo blobs in de cool storage-laag Hallo gedragen anders dan de waarden in de hot storage-laag Hallo Hallo?**
   
    BLOBs in de hot storage-laag Hallo Hallo hebben dezelfde latentie als blobs in opslagaccounts. BLOBs in de cool storage-laag Hallo hebben een gelijksoortige latentie (in milliseconden) als blobs in opslagaccounts voor algemeen gebruik.
   
    BLOBs in de cool storage-laag Hallo hebben een iets lagere beschikbaarheid serviceniveau (SLA) dan Hallo blobs die zijn opgeslagen in Hallo hot storage-laag. Zie [SLA voor opslag](https://azure.microsoft.com/support/legal/sla/storage) voor meer informatie.

8. **Kan ik pagina-blobs en virtuele-machineschijven opslaan in Blob Storage-accounts?**
   
    Blob Storage-accounts ondersteunen alleen blok-blobs en toevoeg-blobs. Pagina-blobs worden niet ondersteund. Virtuele machine van Azure-schijven worden ondersteund door de pagina-blobs en als gevolg hiervan toostore gebruikte virtuele-machineschijven mag niet in Blob storage-accounts. Maar het is mogelijk toostore back-ups van Hallo virtuele-machineschijven als blok-blobs in een Blob storage-account.

9. **Moet ik toochange mijn bestaande toepassingen toouse Blob storage-accounts?**
   
    Blob Storage-accounts zijn voor 100 procent API-consistent met opslagaccounts voor algemeen gebruik voor blok- en toevoeg-blobs. Zolang uw toepassing gebruikmaakt van blok-blobs of toevoeg-blobs en gebruik Hallo 2014-02-14 versie Hallo [REST-API voor Storage Services](https://msdn.microsoft.com/library/azure/dd894041.aspx) of hoger moet samenwerken met uw toepassing. Als u een oudere versie van het Hallo-protocol gebruikt, vervolgens moet u bijwerken uw toouse Hallo nieuwe toepassingsversie dus als toowork naadloos met beide typen opslagaccounts. In het algemeen altijd wordt aangeraden de nieuwste versie Hallo ongeacht welke opslagaccounttype dat u gebruikt.

10. **Is de gebruikerservaring gewijzigd?**
    
    BLOB storage-accounts zijn vergelijkbaar tooa opslagaccounts voor voor het opslaan van blok en toevoeg-blobs en ondersteuning van alle onderdelen met de Hallo van Azure Storage, met inbegrip van hoge duurzaamheid en beschikbaarheid, schaalbaarheid, prestaties en beveiliging. Dan Hallo functies en -beperkingen specifieke tooBlob storage-accounts en de opslaglagen die hierboven, alles is genoemd Hallo anders blijft hetzelfde.

## <a name="next-steps"></a>Volgende stappen

### <a name="evaluate-blob-storage-accounts"></a>Blob Storage-accounts evalueren

[Beschikbaarheid van Blob Storage-accounts per regio controleren](https://azure.microsoft.com/regions/#services)

[Gebruik van de huidige opslagaccounts evalueren door metrische gegevens voor Azure Storage in te schakelen](../common/storage-enable-and-view-metrics.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Prijzen voor Blob Storage per regio controleren](https://azure.microsoft.com/pricing/details/storage/)

[Prijzen voor gegevensoverdracht controleren](https://azure.microsoft.com/pricing/details/data-transfers/)

### <a name="start-using-blob-storage-accounts"></a>Blob Storage-accounts gebruiken

[Aan de slag met Azure Blob Storage](storage-dotnet-how-to-use-blobs.md)

[Verplaatsen van gegevens tooand van Azure Storage](../common/storage-moving-data.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Uw opslagaccounts bekijken en verkennen](http://storageexplorer.com/)