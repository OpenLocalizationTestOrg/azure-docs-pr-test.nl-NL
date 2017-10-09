---
title: aaaEnable controle en detectie van bedreigingen op SQL-servers in Azure Security Center | Microsoft Docs
description: Dit document leest u hoe tooimplement hello Azure Security Center aanbeveling ** controle inschakelen en detectie van bedreigingen op SQL-servers **.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 042fca4d-7dab-4172-8614-e8c21ccb4960
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: b082c48cdbc386f14e677f4e13a7f306f37fd0e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-servers-in-azure-security-center"></a>Inschakelen van controle en detectie van bedreigingen op SQL-servers in Azure Security Center
Azure Security Center beveelt aan dat u controle inschakelt en detectie van dreigingen voor alle databases op uw Azure SQL-servers als controle is niet ingeschakeld. Controle en threat detectie kunt u de naleving van regelgeving onderhouden, de activiteit in een database begrijpen en meer van inzicht krijgen in discrepanties en afwijkingen die kunnen wijzen op problemen voor het bedrijf of vermoedelijke beveiligingsschendingen.

Wanneer u eenmaal hebt ingeschakeld controle kunt u de detectie van dreigingen instellingen en e-mailberichten tooreceive beveiligingswaarschuwingen configureren. Detectie van dreigingen detecteert afwijkende databaseactiviteiten die wijzen op mogelijke bedreigingen toohello database met. Hiermee kunt u toodetect en toopotential bedreigingen reageert wanneer deze zich voordoen.

Deze aanbeveling is van toepassing toohello Azure SQL-service. SQL Server wordt uitgevoerd op uw virtuele machines in Azure-infrastructuurservices (Azure IaaS) zijn niet opgenomen.

> [!NOTE]
> Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.  Dit is geen stapsgewijze handleiding.
>
>

## <a name="implement-hello-recommendation"></a>Hallo aanbeveling implementeren
1. In Hallo **aanbevelingen** blade Selecteer **controle inschakelen en detectie van bedreigingen op SQL-servers**.  Hiermee opent u Hallo **controle inschakelen en detectie van bedreigingen op SQL-servers** blade.

   ![Controleren voor SQL-servers inschakelen][1]
2. Selecteer een SQL server tooenable controle en detectie van bedreigingen op. Hiermee opent u Hallo **controle en detectie van dreigingen** blade.

3. Op Hallo **controle en detectie van dreigingen** blade Selecteer **ON** onder **controle**.

   ![Controle-instellingen inschakelen][2]
4. Volg de stappen Hallo in [SQL database auditing in Azure-portal Hallo](../sql-database/sql-database-auditing-portal.md) tooconfigure opslag waar de controlelogboeken worden opgeslagen. Hallo is van abonnement storage-account voor gegevensverzameling Hallo storage-standaardaccount.
5. Hallo stappen in [aan de slag met SQL Database-Bedreigingsdetectie](../sql-database/sql-database-threat-detection.md) tooturn op en configureren van detectie van dreigingen en tooconfigure Hallo lijst met e-mailberichten die beveiligingswaarschuwingen bij vreemde activiteiten worden ontvangen.

## <a name="see-also"></a>Zie ook
In dit artikel hebt u geleerd hoe tooimplement Security Center aanbeveling Hallo 'Bedreigingendetectie op SQL-servers en controle in te schakelen.' toolearn meer informatie over het beveiligen van uw SQL-database Hallo ziet:

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
[1]: ./media/security-center-enable-auditing-on-sql-server/enable-auditing-on-sql-servers.png
[2]: ./media/security-center-enable-auditing-on-sql-server/auditing-settings-blade.png
