---
title: aaaEnable Transparent Data Encryption in Azure Security Center | Microsoft Docs
description: Dit document leest u hoe tooimplement hello Azure Security Center aanbeveling ** inschakelen Transparent Data Encryption **.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e4be8a0e-2118-4ee9-a266-69e52d9f7f8e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 94c6e9a1feddaa48faac6c835d416c4d131cd5c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a>Transparante gegevensversleuteling in Azure Security Center inschakelen
Azure Security Center beveelt aan dat u Transparent Data Encryption (TDE) voor SQL-databases inschakelen als TDE nog niet is ingeschakeld. TDE beschermt u uw gegevens en kunt u voldoen aan nalevingsvereisten door uw database, gekoppelde back-ups en transactielogboekbestanden in rust, zonder dat wijzigingen tooyour toepassing te versleutelen. toolearn Zie meer [Transparent Data Encryption met Azure SQL Database](https://msdn.microsoft.com/library/dn948096).

Deze aanbeveling is van toepassing toohello Azure SQL-service. bevat geen SQL uitgevoerd op uw virtuele machines.

> [!NOTE]
> Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.  Dit is geen stapsgewijze handleiding.
>
>

## <a name="implement-hello-recommendation"></a>Hallo aanbeveling implementeren
1. In Hallo **aanbevelingen** blade Selecteer **Transparent Data Encryption inschakelen**.
   ![Transparante gegevensversleuteling inschakelen][1]
2. Hiermee opent u Hallo **Transparent Data Encryption voor SQL-databases inschakelen** blade. Selecteer een SQL-database tooenable TDE op.
   ![Selecteer SQL DB tooenable TDE op][2]
3. Op Hallo **transparante gegevensversleuteling** blade Selecteer **ON** onder gegevensversleuteling en selecteer **opslaan** in de bovenste lint Hallo van Hallo-blade.
   ![TDE inschakelen][3]

   Zodra TDE is ingeschakeld voor Hallo geselecteerd SQL-database, hello **coderingsstatus** wordt ook wijzigen**versleutelde**.    

   ![Coderingsstatus][4]

## <a name="see-also"></a>Zie ook
In dit artikel hebt u geleerd hoe tooimplement Hallo Security Center aanbeveling 'Enable Transparent Data Encryption'. toolearn meer informatie over SQL TDE Hallo ziet:

* [Transparante gegevensversleuteling met Azure SQL Database](https://msdn.microsoft.com/library/dn948096)
* [Aan de slag met Transparent Data Encryption (TDE)](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

toolearn meer informatie over Security Center Hallo ziet:

* [Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --meer informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.
* [Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) --meer informatie over hoe toomonitor Hallo status van uw Azure-resources.
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) --meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.
* [Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) --meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md) --Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
* [Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) --Hallo nieuwste Azure-beveiliging nieuws en informatie.

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
