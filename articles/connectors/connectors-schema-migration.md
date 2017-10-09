---
title: aaaHow toomigrate tooschema versie 2015-08-01-preview-logic apps | Microsoft Docs
description: U kunt de nieuwste schemaversie van logic apps toohello eenvoudig migreren. Volg deze stappen.
services: logic-apps
documentationcenter: 
author: MSFTMAN
manager: erikre
editor: 
tags: connectors
ms.assetid: 3e177e49-fd69-43e9-9b9b-218abb250c31
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2016
ms.author: deonhe
ms.openlocfilehash: c7b42aaec547eddd28b0c649a3c0625047f9f805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-logic-apps-tooschema-version-2015-08-01-preview"></a>Hoe toomigrate logic apps tooschema versie 2015-08-01-preview
toomove uw bestaande logic apps toohello nieuwe schema, Hallo te volgen:  

1. Open uw logische app in hello Azure-portal  
2. Klik op Schema bijwerken:
   
   ![API-pictogram][step1]   
   Hallo Schema bijwerken pagina weergegeven en bevat een koppeling tooa document dat gedetailleerde informatie over verbeteringen in het nieuwe schema Hallo Hallo: ![API-pictogram][step2]

> [!NOTE]
> Wanneer u selecteert **Schema bijwerken**, automatisch Hallo migratiestappen uitgevoerd en krijgt u Hallo code-uitvoer. U kunt deze tooupdate echter uw definitie gebruiken, zorg ervoor dat u goed codering Volg zoals die zijn beschreven in Hallo **Best practices** hieronder.
> 
> 

## <a name="best-practices-when-migrating-your-logic-apps-toohello-latest-schema-version"></a>Aanbevolen procedures bij het migreren van de nieuwste schemaversie van Logic apps toohello:
* Kopiëren Hallo gemigreerd script tooa nieuwe Logic App - niet overschrijven Hallo oude pas nadat u hebt uw gemigreerde app testen en bevestigd hello voltooid werkt zoals verwacht.
* Uw logische app testen **voordat** u deze in productie neemt
* Nadat de migratie is voltooid, start u het bijwerken van uw logische apps toouse hello [beheerde API's](apis-list.md) waar mogelijk. U kunt bijvoorbeeld starten met het gebruik van de Dropbox v2-versie overal waar u DropBox v1 gebruikt.

## <a name="whats-next"></a>Volgend onderwerp
* [Meer informatie over hoe toomanually uw logische apps migreren](../logic-apps/logic-apps-schema-2015-08-01.md)

<!--Icon references-->
[step1]: ./media/connectors-schema-migration/migrateschema1.png
[step2]: ./media/connectors-schema-migration/migrateschema2.png






