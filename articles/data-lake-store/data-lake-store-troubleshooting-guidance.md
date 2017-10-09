---
title: aaaFrequently vragen voor Azure Data Lake Store | Microsoft Docs
description: Hulp bij het oplossen en voorkomen van problemen met Azure Data Lake Store
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf7fd555-3e30-43ce-b28c-c3ad0a241fdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: eeabdeef18f3b72901bd1a14283f85dd9c0ead44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-data-lake-store"></a>Veelgestelde vragen over Azure Data Lake Store
In dit artikel leert u over veelgestelde vragen over verwante tooAzure Data Lake Store.

## <a name="how-can-i-further-protect-my-data-from-region-wide-disasters-or-accidental-deletions"></a>Hoe kan ik mijn gegevens beter beschermen tegen regiobrede noodgevallen of onbedoelde verwijderingen?
Hallo-gegevens in uw Azure Data Lake Store-account is een robuuste tootransient hardwarefouten binnen een regio via geautomatiseerde replica's. Dit zorgt ervoor duurzaamheid en hoge beschikbaarheid, vergadering Hallo SERVICEOVEREENKOMST van Azure Data Lake Store. Hier vindt u enkele richtlijnen op hoe toofurther uw gegevens beschermen tegen zeldzame regio hele uitval of onopzettelijke verwijderingen.

### <a name="disaster-recovery-guidance"></a>Richtlijnen voor herstel na noodgevallen
Het is essentieel voor elke klant tooprepare hun eigen noodherstelplan. Raadpleeg de documentatie voor Azure hieronder toobuild toohello het noodherstelplan. Hier volgen enkele bronnen waarmee u uw eigen plan kunt maken.

* [Herstel na noodgevallen en hoge beschikbaarheid voor Azure-toepassingen](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)
* [Technische richtlijnen voor flexibiliteit van Azure](../resiliency/resiliency-technical-guidance.md)

#### <a name="best-practices"></a>Aanbevolen procedures
Het is raadzaam dat u uw kritieke gegevens tooanother Data Lake Store-account in een andere regio met een frequentie uitgelijnd toohello behoeften van uw noodherstelplan kopieert. Er zijn verschillende methoden toocopy gegevens zoals [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [Azure PowerShell](data-lake-store-get-started-powershell.md) of [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md). Azure Data Factory is een handige service voor het regelmatig maken en implementeren van pijplijnen voor gegevensverplaatsing.

Als een regionale uitval, kunt u vervolgens toegang tot uw gegevens in Hallo regio waar Hallo gegevens is gekopieerd. U kunt bewaken Hallo [Azure Service Health Dashboard](https://azure.microsoft.com/status/) toodetermine hello Azure servicestatus over Hallo wereld.

### <a name="data-corruption-or-accidental-deletion-recovery-guidance"></a>Herstelrichtlijnen voor gegevensbeschadiging en onbedoelde verwijdering
Hoewel Azure Data Lake Store gegevensflexibiliteit biedt door middel van automatische replica's, sluit dit niet uit dat de gegevens door uw toepassing (of door ontwikkelaars/gebruikers) worden beschadigd of onbedoeld worden verwijderd.

#### <a name="best-practices"></a>Aanbevolen procedures
tooprevent per ongeluk verwijderen, wordt aangeraden dat u eerst de juiste toegangsbeleid Hallo ingesteld voor uw Data Lake Store-account.  Dit omvat het toepassen van [Azure-resource vergrendelingen](../azure-resource-manager/resource-group-lock-resources.md) toolock omlaag belangrijke bronnen, evenals toepassen en de bestandsnaam niveau van toegangsbeheer met Hallo beschikbaar [Data Lake Store-beveiligingsfuncties](data-lake-store-security-overview.md). We raden u ook aan regelmatig kopieën van uw kritieke gegevens te maken met [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [Azure PowerShell](data-lake-store-get-started-powershell.md) of [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) naar een ander Data Lake Store-account, een andere map of een ander Azure-abonnement.  Dit kan gebruikte toorecover vanuit een gegevens-beschadiging of verwijderen van een incident zijn. Azure Data Factory is een handige service voor het regelmatig maken en implementeren van pijplijnen voor gegevensverplaatsing.

Organisaties kunnen ook inschakelen [Diagnostische logboekregistratie](data-lake-store-diagnostic-logs.md) voor hun Azure Data Lake Store-account toocollect gegevens toegang audittrails die informatie biedt over die mogelijk verwijderd of een bestand wordt bijgewerkt.

## <a name="next-steps"></a>Volgende stappen
* [Aan de slag met Azure Data Lake Store](data-lake-store-get-started-portal.md)
* [Gegevens in Data Lake Store beveiligen](data-lake-store-secure-data.md)

