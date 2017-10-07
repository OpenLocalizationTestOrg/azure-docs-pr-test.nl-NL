---
title: aaaAlerts validatie in Azure Security Center | Microsoft Docs
description: Dit document helpt u toovalidate Hallo beveiligingswaarschuwingen in Azure Security Center.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f8f17a55-e672-4d86-8ba9-6c3ce2e71a57
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 030e9e74303758192eedaf517f1cb0d2e4a7852e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="alerts-validation-in-azure-security-center"></a>Validatie van waarschuwingen in Azure Security Center
Dit document helpt u meer informatie over hoe tooverify als uw systeem juist is geconfigureerd voor Azure Security Center-waarschuwingen.

## <a name="what-are-security-alerts"></a>Wat zijn beveiligingswaarschuwingen?
Security Center automatisch verzamelt, analyseert en integreert logboekgegevens van uw Azure-resources, het Hallo-netwerk en de verbonden partneroplossingen, zoals een firewall en endpoint protection-oplossingen, toodetect en waarschuwing toothreats u. Lees [beheren en reageert toosecurity waarschuwingen in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) voor meer informatie over beveiligingswaarschuwingen en lezen [beveiligingswaarschuwingen in Azure Security Center begrijpen](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn meer over de verschillende typen Hallo van waarschuwingen.

## <a name="alert-validation"></a>Waarschuwingen valideren
Security Center-agent is geïnstalleerd op uw computer, Volg na Hallo stappen hieronder van Hallo computer waar u toobe Hallo aangevallen bron van het Hallo-waarschuwing:

1. Het bureaublad van de computer van een uitvoerbaar bestand (voor voorbeeld calc.exe) toohello of andere directory van uw gemak kopiëren.
2. Wijzig de naam van dit bestand te**ASC_AlertTest_662jfi039N.exe**.
3. Hallo-opdrachtprompt openen en het uitvoeren van dit bestand met een argument (alleen een valse argumentnaam), zoals: *ASC_AlertTest_662jfi039N.exe - foo*
4. Wacht 5 minuten voor too10 en open Security Center Alerts. Hier vindt u een waarschuwing vergelijkbare toofollowing een:

    ![Waarschuwingen valideren](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

Als deze waarschuwing wordt bekeken, controleert u Hallo veld argumenten controle ingeschakeld wordt weergegeven als waar. Als u deze waarde false ziet, moet u opdrachtregelargumenten tooenable controle. U kunt deze optie met behulp van de opdrachtregel na Hallo inschakelen:

*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*


## <a name="see-also"></a>Zie ook
In dit artikel geïntroduceerd toohello waarschuwingen validatieproces. Nu u bekend bent met deze validatie, proberen Hallo artikelen te volgen:

* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts). Meer informatie over hoe toomanage waarschuwingen en reageren toosecurity incidenten in Security Center.
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md). Meer informatie over hoe toomonitor Hallo status van uw Azure-resources.
* [Beveiligingswaarschuwingen in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type). Meer informatie over de verschillende soorten beveiligingswaarschuwingen Hallo.
* [Handleiding voor het oplossen van problemen met Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide). Meer informatie over hoe tootroubleshoot algemene problemen in Security Center. 
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md). Veelgestelde vragen over het gebruik van Hallo service vinden.
* [Azure-beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/). Raadpleeg de blogberichten over beveiliging en naleving in Azure.

