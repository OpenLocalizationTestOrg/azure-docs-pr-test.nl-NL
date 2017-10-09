---
title: aaaEnable controle en detectie van bedreigingen op de SQL-databases in Azure Security Center | Microsoft Docs
description: Dit document leest u hoe tooimplement hello Azure Security Center aanbeveling ** inschakelen van controle en detectie van bedreigingen op SQL-databases **.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 224b6755-2b36-4ecd-9af8-139a198e0df1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: c94140acf37cabaca3e681ba5db79d6827e7b9db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-databases-in-azure-security-center"></a>Inschakelen van controle en detectie van bedreigingen op SQL-databases in Azure Security Center
Azure Security Center beveelt aan dat u controle en detectie van bedreigingen voor alle SQL-databases inschakelen als de controle en detectie van dreigingen nog niet is ingeschakeld. Controle en threat detectie kunt u de naleving van regelgeving onderhouden, de activiteit in een database begrijpen en meer van inzicht krijgen in discrepanties en afwijkingen die kunnen wijzen op problemen voor het bedrijf of vermoedelijke beveiligingsschendingen.

Wanneer u eenmaal hebt ingeschakeld controle kunt u de detectie van dreigingen instellingen en e-mailberichten tooreceive beveiligingswaarschuwingen configureren. Detectie van dreigingen detecteert afwijkende databaseactiviteiten die wijzen op mogelijke bedreigingen toohello database met. Hiermee kunt u toodetect en toopotential bedreigingen reageert wanneer deze zich voordoen.

Deze aanbeveling is van toepassing toohello Azure SQL-service. SQL uitgevoerd op uw virtuele machines zijn niet opgenomen.

> [!NOTE]
> Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.  Dit is geen stapsgewijze handleiding.
>
>

## <a name="implement-hello-recommendation"></a>Hallo aanbeveling implementeren
1. In Hallo **aanbevelingen** blade Selecteer **controle inschakelen en detectie van bedreigingen op SQL-databases**.  Hiermee opent u Hallo **controle inschakelen en detectie van bedreigingen op SQL-databases** blade.

   ![Controleren voor SQL-databases inschakelen][1]
2. Selecteer een SQL database tooenable controle op. Hiermee opent u Hallo **controle en detectie van dreigingen** blade.

3. Op Hallo **controle en detectie van dreigingen** blade Selecteer **ON** onder **controle**.

   ![Inschakelen van controle en detectie van bedreigingen][2]
4. Volg de stappen Hallo in [SQL Database met detectie van dreigingen in hello Azure-portal](../sql-database/sql-database-threat-detection-portal.md) tooturn op en configureren van detectie van dreigingen en tooconfigure Hallo lijst met e-mailberichten die u waarschuwingen op vreemde activiteiten ontvangt.

## <a name="see-also"></a>Zie ook
In dit artikel hebt u geleerd hoe tooimplement Hallo Security Center aanbeveling ' Enable controle en detectie van bedreigingen op SQL-databases.' toolearn meer informatie over het beveiligen van uw SQL-database Hallo ziet:

* [Uw SQL-database beveiligen](../sql-database/sql-database-security-overview.md)

toolearn meer informatie over Security Center Hallo ziet:

* [Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --meer informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.
* [Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) --meer informatie over hoe toomonitor Hallo status van uw Azure-resources.
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) --meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.
* [Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) --meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md) --Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
* [Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) --Hallo nieuwste Azure-beveiliging nieuws en informatie.

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-databases/enable-auditing-on-sql-databases.png
[2]: ./media/security-center-enable-auditing-on-sql-databases/auditing-threat-detection-blade.png
