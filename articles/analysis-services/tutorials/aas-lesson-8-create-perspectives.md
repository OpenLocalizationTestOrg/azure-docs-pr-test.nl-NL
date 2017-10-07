---
title: aaa "Azure Analysis Services zelfstudie les 8 maken perspectieven | Microsoft Docs'
description: Hierin wordt beschreven hoe toocreate perspectieven in Hallo zelfstudie Azure Analysis Services-project.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: 25391813e1969ecb22af4d6f9c1ccd8358d812fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-8-create-perspectives"></a>Les 8: Perspectieven maken

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In deze les maakt u een perspectief voor internetverkopen. Een perspectief definieert een subset van een model dat u kunt weergeven om gerichte, bedrijfsspecifieke of toepassingsspecifieke standpunten inzichtelijk te maken. Wanneer een gebruiker verbinding tooa model maakt met behulp van een perspectief, zien ze alleen modelobjecten (tabellen, kolommen, metingen, hiërarchieën en KPI's) als velden die zijn gedefinieerd in dit perspectief. toolearn meer, Zie [perspectieven](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).
  
Hallo Internet verkoop perspectief die u in deze les maakt sluit Hallo DimCustomer table-object. Wanneer u een perspectief dat bepaalde objecten van weergave uitsluit maakt, bestaat dat object nog in Hallo model. Het object wordt echter niet vermeld in de lijst met velden van de rapportageclient. Berekende kolommen en metingen die al dan niet zijn opgenomen in een perspectief, kunnen nog steeds werken met uitgesloten objectgegevens.  
  
Hallo-doel van deze les is toodescribe hoe toocreate perspectieven en vertrouwd raken met het model in tabelvorm Hallo hulpprogramma's. Als u later in dit model tooinclude aanvullende tabellen uitvouwt, kunt u meer perspectieven toodefine verschillende standpunten van Hallo model bijvoorbeeld inventaris en verkoop.  
  
Geschatte tijd toocomplete deze les: **vijf minuten**  
  
## <a name="prerequisites"></a>Vereisten  
Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd. Voordat u Hallo taken uitvoert in deze les, u moet voltooid Hallo vorige les: [les 7: Key Performance Indicators maken](../tutorials/aas-lesson-7-create-key-performance-indicators.md).  
  
## <a name="create-perspectives"></a>Perspectieven maken  
  
#### <a name="toocreate-an-internet-sales-perspective"></a>toocreate een verkoop van de Internet-perspectief  
  
1.  Klik op Hallo **Model** menu > **perspectieven** > **maken en beheren**.  
  
2.  In Hallo **perspectieven** in het dialoogvenster, klikt u op **nieuw perspectief**.  
  
3.  Dubbelklik op Hallo **nieuw perspectief** kolomkop te klikken en vervolgens rename **Internet verkoop**.  
  
4.  Selecteer alle Hallo tabellen Hallo *behalve* **DimCustomer**.  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    In een latere les gebruikt u Hallo analyseren in Excel functie tootest dit perspectief wordt gemaakt. Hallo lijst Excel PivotTable-velden bevat elke tabel behalve Hallo DimCustomer tabel.  

## <a name="whats-next"></a>Volgende stappen
[Les 9: Hiërarchieën maken](../tutorials/aas-lesson-9-create-hierarchies.md).
  
  
  
  
