---
title: aaaEnable automatische afstemming voor Azure SQL Database | Microsoft Docs
description: U kunt inschakelen automatische afstemming op uw Azure SQL Database eenvoudig.
services: sql-database
documentationcenter: 
author: vvasic
manager: drasumic
editor: vvasic
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 06/05/2016
ms.author: vvasic
ms.openlocfilehash: af9da161eabc0f8c4cb100c050288f234efb8093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-automatic-tuning"></a>Automatisch instellen inschakelen

Azure SQL-Database is een automatisch beheerd gegevens-service die voortdurend bewaakt uw query's en identificeert Hallo actie dat u de prestaties van uw workload tooimprove kunt uitvoeren. U kunt bekijken van aanbevelingen en handmatig toepassen of Azure SQL Database automatisch toegepast corrigerende maatregelen kunt: dit staat bekend als **automatische afstemmen modus**. Automatische afstemming kan worden ingeschakeld op de server voor Hallo of Hallo databaseniveau.

## <a name="enable-automatic-tuning-on-server"></a>Automatische afstemming op server inschakelen

tooenable automatische afstemming op Azure SQL Database-server, gaat u toohello-server in Azure portal en selecteer vervolgens **automatische afstemming** in Hallo-menu. Selecteer opties voor automatische afstemmen gewenste tooenable en selecteer Hallo **toepassen**:

![Server](./media/sql-database-automatic-tuning-enable/server.png)

Automatische afstemming van de opties op de server zijn toegepaste tooall databases op Hallo-server. Standaard alle databases Hallo configuratie overnemen van hun bovenliggende server, maar dit kan worden genegeerd en afzonderlijk opgegeven voor elke database.

## <a name="configure-automatic-tuning-on-database"></a>Configureer Automatische afstemming op database

Hallo Azure portal kunt u tooindividually Hallo-configuratie voor automatische afstemmen op elke database opgeven.

> [!NOTE]
> Hallo algemene aanbeveling is toomanage Hallo automatische afstemmen configuratie op serverniveau in dat geval Hallo dezelfde configuratie-instellingen kunnen worden toegepast op elke database automatisch. Configureer Automatische afstemming op een individuele database als Hallo database verschilt dat anderen op dezelfde server Hallo.
>

Automatische afstemming op een individuele database tooenable toohello database in Azure-portal Hallo navigeren en vervolgens selecteert **automatische afstemming**. U kunt een individuele database tooinherit Hallo instellingen uit de database Hallo Hallo vinken configureren of u kunt Hallo-configuratie voor een database afzonderlijk opgeven.

![Database](./media/sql-database-automatic-tuning-enable/database.png)

Nadat u de juiste configuratie hebt geselecteerd, klikt u op **toepassen**.

## <a name="next-steps"></a>Volgende stappen
* Lees Hallo [automatische afstemmen artikel](sql-database-automatic-tuning.md) toolearn meer over automatische afstemming en hoe deze kan u helpen de prestaties worden verbeterd.
* Zie [prestaties aanbevelingen](sql-database-advisor.md) voor een overzicht van Azure SQL Database prestaties aanbevelingen.
* Zie [inzichten voor queryprestaties](sql-database-query-performance.md) toolearn over het weergeven van Hallo prestatie-invloed van de meest gebruikte query's.
