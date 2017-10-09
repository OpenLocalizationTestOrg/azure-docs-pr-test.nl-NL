---
title: systeemupdates aaaApply in Azure Security Center | Microsoft Docs
description: Dit document leest u hoe tooimplement hello Azure Security Center aanbevelingen ** toepassen system updates ** en ** na system updates ** opnieuw opgestart.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e5bd7f55-38fd-4ebb-84ab-32bd60e9fa7a
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: 02024f1558b4758c09141fe1934c2e1a9845cc96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a>Systeemupdates in Azure Security Center toepassen
Azure Security Center bewaakt dagelijks Windows en Linux virtuele machines (VM's) voor besturingssysteemupdates ontbreken. Security Center haalt een lijst met beschikbare beveiligingsupdates en essentiële updates via Windows Update of Windows Server Update Services (WSUS), afhankelijk van welke service is geconfigureerd op een virtuele machine van Windows.  Security Center controleert ook of de meest recente updates Hallo in Linux-systemen. Als uw VM een systeemupdate ontbreekt is, wordt Security Center aangeraden systeemupdates

> [!NOTE]
> Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.  Dit is geen stapsgewijze handleiding.
>
>

## <a name="implement-hello-recommendation"></a>Hallo aanbeveling implementeren
1. In Hallo **aanbevelingen** blade Selecteer **toepassen systeemupdates**.

   ![Systeemupdates toepassen][1]
2. Hallo **toepassen systeemupdates** blade wordt geopend met een lijst van ontbrekende systeemupdates virtuele machines. Selecteer een virtuele machine.

   ![Selecteer een virtuele machine][2]
3. Er wordt een blade geopend met een lijst van ontbrekende updates voor die VM. Selecteer een systeemupdate. In dit voorbeeld gaan we KB3156016 selecteren.

   ![Ontbrekende beveiligingsupdates][3]

4. Volg de stappen Hallo in Hallo **beveiligingsupdate** blade tooapply Hallo update ontbreekt.

   ![Beveiligingsupdate][4]

## <a name="reboot-after-system-updates"></a>Opnieuw opstarten na systeemupdates
1. Retourneren van toohello **aanbevelingen** blade. Een nieuwe vermelding is gegenereerd nadat u systeemupdates, aangeroepen toegepast **opnieuw opgestart na systeemupdates**. Deze vermelding laat u weten dat u nodig hebt tooreboot Hallo VM toocomplete Hallo proces van het toepassen van systeemupdates.

   ![Opnieuw opstarten na systeemupdates][5]
2. Selecteer **opnieuw opgestart na systeemupdates**. Hiermee opent u **opnieuw opstarten is in behandeling toocomplete systeemupdates** blade met een lijst van virtuele machines dat u nodig hebt toorestart toocomplete Hallo systeemproces-updates toepassen.

   ![Opnieuw opstarten in behandeling][6]

Opnieuw opstarten Hallo VM van Azure toocomplete Hallo proces.

## <a name="see-also"></a>Zie ook
toolearn meer informatie over Security Center Hallo ziet:

* [Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --meer informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.
* [Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) --meer informatie over hoe toomonitor Hallo status van uw Azure-resources.
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) --meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.
* [Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) --meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md) --Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
* [Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) --Lees blogberichten over Azure-beveiliging en naleving.

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
