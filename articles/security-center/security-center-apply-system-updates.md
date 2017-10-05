---
title: Toepassing systeemupdates in Azure Security Center | Microsoft Docs
description: Dit document ziet u hoe de Azure Security Center aanbevelingen implementeren ** toepassen system updates ** en ** na system updates ** opnieuw opgestart.
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
ms.openlocfilehash: 50cdea437db5387813c6a3905d14b6904d2aba34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a>Systeemupdates in Azure Security Center toepassen
Azure Security Center bewaakt dagelijks Windows en Linux virtuele machines (VM's) voor besturingssysteemupdates ontbreken. Security Center haalt een lijst met beschikbare beveiligingsupdates en essentiële updates via Windows Update of Windows Server Update Services (WSUS), afhankelijk van welke service is geconfigureerd op een virtuele machine van Windows.  Security Center controleert ook of de meest recente updates in de Linux-systemen. Als uw VM een systeemupdate ontbreekt is, wordt Security Center aangeraden systeemupdates

> [!NOTE]
> In dit document wordt de service geïntroduceerd aan de hand van een voorbeeldimplementatie.  Dit is geen stapsgewijze handleiding.
>
>

## <a name="implement-the-recommendation"></a>De aanbeveling implementeren
1. In de **aanbevelingen** blade Selecteer **toepassen systeemupdates**.

   ![Systeemupdates toepassen][1]
2. De **toepassen systeemupdates** blade wordt geopend met een lijst van ontbrekende systeemupdates virtuele machines. Selecteer een virtuele machine.

   ![Selecteer een virtuele machine][2]
3. Er wordt een blade geopend met een lijst van ontbrekende updates voor die VM. Selecteer een systeemupdate. In dit voorbeeld gaan we KB3156016 selecteren.

   ![Ontbrekende beveiligingsupdates][3]

4. Volg de stappen in de **beveiligingsupdate** blade de ontbrekende update toe te passen.

   ![Beveiligingsupdate][4]

## <a name="reboot-after-system-updates"></a>Opnieuw opstarten na systeemupdates
1. Ga terug naar de **aanbevelingen** blade. Een nieuwe vermelding is gegenereerd nadat u systeemupdates, aangeroepen toegepast **opnieuw opgestart na systeemupdates**. Deze vermelding laat u weten dat u de virtuele machine moet voor het voltooien van het proces van het toepassen van systeemupdates opnieuw opstarten.

   ![Opnieuw opstarten na systeemupdates][5]
2. Selecteer **opnieuw opgestart na systeemupdates**. Hiermee opent u **opnieuw worden opgestart om te voltooien systeemupdates** blade met een lijst van virtuele machines die u nodig hebt om opnieuw te starten voor het voltooien van het systeem toepassen updates proces.

   ![Opnieuw opstarten in behandeling][6]

Start opnieuw op de virtuele machine van Azure om het proces te voltooien.

## <a name="see-also"></a>Zie ook
Zie de volgende onderwerpen voor meer informatie over het Beveiligingscentrum:

* [Setting security policies in Azure Security Center](security-center-policies.md) (Beveiligingsbeleid instellen in Azure Security Center): leer hoe u beveiligingsbeleid voor uw Azure-abonnementen en -resourcegroepen configureert.
* [Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) --informatie over het bewaken van de status van uw Azure-resources.
* [Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) (Beveiligingswaarschuwingen beheren en erop reageren in Azure Security Center): ontdek hoe u beveiligingswaarschuwingen kunt beheren en erop kunt reageren.
* [Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md): leer hoe u de integriteitsstatus van uw partneroplossingen kunt bewaken.
* [Azure Security Center FAQ](security-center-faq.md) (Veelgestelde vragen over Azure Security Center): raadpleeg veelgestelde vragen over het gebruik van de service.
* [Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) --Lees blogberichten over Azure-beveiliging en naleving.

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
