---
title: Data Lake Store regio-overschrijdende migratie aaaAzure | Microsoft Docs
description: Meer informatie over de migratie van de regio-overschrijdende voor Azure Data Lake Store.
services: data-lake-store
documentationcenter: 
author: swums
manager: amitkul
editor: swums
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/27/2017
ms.author: stewu
ms.openlocfilehash: 561ac821c1bd555886035867678cb685997564eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-data-lake-store-across-regions"></a>Data Lake Store migreren tussen regio 's

Wanneer nieuwe regio's Azure Data Lake Store beschikbaar wordt, kunt u toodo een eenmalige migratie tootake profiteren van nieuwe Hallo-gebied. Meer informatie over welke tooconsider bij het plannen en Hallo migratie voltooien.

## <a name="prerequisites"></a>Vereisten

* **Een Azure-abonnement**. Zie voor meer informatie [maken van uw gratis Azure-account vandaag](https://azure.microsoft.com/pricing/free-trial/).
* **Een Data Lake Store-account in twee verschillende regio's**. Zie voor meer informatie [aan de slag met Azure Data Lake Store](data-lake-store-get-started-portal.md).
* **Azure Data Factory**. Zie voor meer informatie [inleiding tooAzure Data Factory](../data-factory/data-factory-introduction.md).


## <a name="migration-considerations"></a>Overwegingen bij migratie

Bepaal eerst Hallo migratiestrategie die geschikt is voor uw toepassing die u schrijft, leest of gegevens in Data Lake Store worden verwerkt. Wanneer u een strategie kiest, houd rekening met de beschikbaarheidsvereisten van uw toepassing en de Hallo downtime die deze gebeurtenis treedt op tijdens een migratie. De eenvoudigste manier is bijvoorbeeld mogelijk toouse Hallo 'lift-en-shift' cloud migratie model. In deze methode voert onderbreken u Hallo-toepassing in uw bestaande regio terwijl alle uw gegevens toohello nieuw gebied gekopieerd. Wanneer Hallo kopieerproces is voltooid, moet u uw toepassing in de nieuwe regio Hallo hervatten en vervolgens verwijdert Hallo oude Data Lake Store-account. Uitvaltijd tijdens de migratie Hallo is vereist.

tooreduce uitvaltijd, kunt u bijvoorbeeld onmiddellijk starten nieuwe gegevens in de nieuwe regio Hallo opnemen. Wanneer u Hallo minimumhoeveelheid gegevens nodig hebt, Voer uw toepassing in Hallo nieuwe regio. Op de achtergrond hello, blijven toocopy oudere gegevens van de nieuwe Data Lake Store-account in Hallo bestaande Data Lake Store-account toohello Hallo nieuw gebied. Met behulp van deze benadering kunt u Hallo switch toohello nieuw gebied weinig uitvaltijd. Wanneer alle Hallo oudere gegevens zijn gekopieerd, moet u Hallo oude Data Lake Store-account verwijderen.

Andere belangrijke informatie tooconsider bij het plannen van de migratie zijn:

* **Gegevensvolume**. Hallo volume aan gegevens (in gigabytes, Hallo aantal bestanden en mappen, enzovoort) is van invloed op Hallo tijd en bronnen die u nodig hebt voor Hallo-migratie.

* **Data Lake Store-accountnaam**. nieuwe accountnaam in de nieuwe regio Hallo Hallo moet wereldwijd uniek zijn. Hallo-naam van uw oude Data Lake Store-account in VS-Oost 2 kan bijvoorbeeld contosoeastus2.azuredatalakestore.net zijn. U kunt uw nieuwe Data Lake Store-account in Noord EU contosonortheu.azuredatalakestore.net naam.

* **Hulpprogramma's voor**. Het is raadzaam dat u Hallo [Azure Data Factory-Kopieeractiviteit](../data-factory/data-factory-azure-datalake-connector.md) toocopy Data Lake Store-bestanden. Data Factory ondersteunt de verplaatsing van gegevens met hoge prestaties en betrouwbaarheid. Houd er rekening mee dat Data Factory alleen Hallo mappenhiërarchie en inhoud van het Hallo-bestanden worden gekopieerd. U moet toomanually toepassen van een toegangsbeheerlijsten (ACL's) die u in Hallo oude account toohello nieuwe account gebruiken. Zie voor meer informatie, waaronder prestatiedoelen voor de best mogelijke scenario's Hallo [Kopieeractiviteit prestaties en prestatieafstemming handleiding](../data-factory/data-factory-copy-activity-performance.md). Als u gegevens kopiëren sneller wilt, moet u mogelijk toouse aanvullende Cloud Data Movement eenheden. Sommige andere hulpmiddelen, zoals AdlCopy, bieden geen ondersteuning voor kopiëren van gegevens tussen regio's.  

* **Kosten van bandbreedte**. [Kosten van bandbreedte](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) toepassen omdat de gegevens worden overgebracht buiten een Azure-regio.

* **ACL's voor uw gegevens**. Beveilig uw gegevens in de nieuwe regio Hallo door toe te passen toofiles ACL's en mappen. Zie voor meer informatie [beveiligen van gegevens die zijn opgeslagen in Azure Data Lake Store](data-lake-store-secure-data.md). U wordt aangeraden dat u Hallo migratie tooupdate gebruiken en aanpassen van de ACL's. U kunt toouse instellingen vergelijkbare tooyour huidige instellingen. U kunt Hallo-ACL's die toegepast tooany-bestand zijn met behulp van hello Azure-portal bekijken [PowerShell-cmdlets](/powershell/module/azurerm.datalakestore/get-azurermdatalakestoreitempermission), of de SDK's.  

* **Locatie van de services analytics**. Voor optimale prestaties moet uw analytics-services, zoals Azure Data Lake Analytics of Azure HDInsight in Hallo dezelfde regio bevinden als uw gegevens.  

## <a name="next-steps"></a>Volgende stappen
* [Overzicht van Azure Data Lake Store](data-lake-store-overview.md)
