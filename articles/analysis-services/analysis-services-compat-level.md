---
title: aaaData model compatibiliteitsniveau in Azure Analysis Services | Microsoft Docs
description: Understanding tabelgegevens model compatibiliteitsniveau.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/16/2017
ms.author: owend
ms.openlocfilehash: bfaf0c60666729d1e6e0baf082c046ea9faa4e86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a>Het compatibiliteitsniveau voor Analysis Services-modellen in tabelvorm

*Het compatibiliteitsniveau* toorelease-specifieke gedrag in de Analysis Services-engine Hallo verwijst. Wijzigingen toohello compatibiliteitsniveau wordt doorgaans samenvallen met belangrijke releases van SQL Server. Deze wijzigingen zijn ook geïmplementeerd in Azure Analysis Services toomaintain pariteit tussen beide platforms. Compatibiliteit niveau wijzigingen zijn ook van invloed op functies die beschikbaar zijn in uw modellen in tabelvorm. Bijvoorbeeld, hebben DirectQuery en metagegevens in tabelvorm object verschillende implementaties, afhankelijk van het compatibiliteitsniveau Hallo. 

Azure Analysis Services biedt ondersteuning voor tabelmodellen op Hallo 1200 en 1400 compatibiliteitsniveaus.

de meest recente compatibiliteitsniveau Hallo is 1400. Dit niveau samenvalt met SQL Server 2017 Analysis Services. Belangrijke functies in Hallo 1400 compatibiliteitsniveau:

*  Nieuwe infrastructuur voor toegang tot gegevens en importeren in modellen in tabelvorm met ondersteuning voor TOM APIs en TMSL scripting. Deze nieuwe functie biedt ondersteuning voor extra gegevensbronnen zoals Azure Blob-opslag.
*  Gegevenstransformatie en gegevens mashup mogelijkheden met behulp van expressies gegevens ophalen en M.
*  Metingen ondersteuning voor een eigenschap detailrijen met een DAX-expressie. Deze eigenschap kunt clienthulpprogramma's zoals Microsoft Excel toodrill omlaag toodetailed gegevens uit een samengevoegde lijst. Wanneer gebruikers totale verkoop voor een regio en de maand bekijken, kunnen ze bijvoorbeeld Hallo gekoppeld ordergegevens bekijken. 
*  Object beveiligingsniveau voor tabel- en kolomnamen benoemt bovendien toohello gegevens daarin.
*  Verbeterde ondersteuning voor niet-aaneengesloten hiërarchieën.
*  Bewaking van prestaties en verbeteringen.
  
## <a name="set-compatibility-level"></a>Het compatibiliteitsniveau instellen 
 Wanneer u een nieuw model in tabelvorm-project in SSDT, kunt u het compatibiliteitsniveau Hallo op Hallo **model in tabelvorm designer** dialoogvenster. 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 Als u Hallo selecteert **dit bericht niet meer weergeven** optie alle volgende projecten gebruiken Hallo compatibiliteitsniveau u hebt opgegeven als Hallo standaard. U kunt wijzigen Hallo standaard compatibiliteitsniveau in SSDT in **extra** > **opties**.  
  
 een bestaand project model in tabelvorm in SSDT, set Hallo tooupgrade **compatibiliteitsniveau** eigenschap in Hallo model **eigenschappen** venster. In rekening te houden, Hallo compatibiliteitsniveau upgraden is niet ongedaan worden gemaakt.
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a>Controleer het compatibiliteitsniveau voor een tabellaire modeldatabase in SQL Server Management Studio 
 SSMS, met de rechtermuisknop op Hallo-databasenaam > **eigenschappen** > **compatibiliteitsniveau**.  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a>Controleer het compatibiliteitsniveau van de ondersteunde versies voor een server in SSMS  
 SSMS, met de rechtermuisknop op Hallo-servernaam > **eigenschappen** > **compatibiliteitsniveau ondersteund**.  
  
 Deze eigenschap geeft Hallo hoogste compatibiliteitsniveau van een database die wordt uitgevoerd op Hallo-server (met uitzondering van de preview). Hallo ondersteund compatibiliteitsniveau kan niet worden gewijzigd.  

## <a name="next-steps"></a>Volgende stappen
  [Een model maken in Azure portal](analysis-services-create-model-portal.md)   
  [Analyseservices beheren](analysis-services-manage.md)  
