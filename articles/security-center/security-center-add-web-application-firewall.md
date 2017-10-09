---
title: aaaAdd web application firewall in Azure Security Center | Microsoft Docs
description: Dit document leest u hoe tooimplement hello Azure Security Center aanbevelingen ** toevoegen van een web application firewall ** en ** voltooien toepassing beveiliging **.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 8f56139a-4466-48ac-90fb-86d002cf8242
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: terrylan
ms.openlocfilehash: bff0aa2a5c6e0dde23396f93de52abe295053581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-web-application-firewall-in-azure-security-center"></a>Web application firewall toevoegen in Azure Security Center
Azure Security Center kan aanbevelen dat u, web application firewall (WAF) van een Microsoft-partner toosecure uw webtoepassingen toevoegt. Dit document vindt u via een voorbeeld van hoe tooapply deze aanbeveling.

Een WAF aanbeveling wordt voor een openbare internetgerichte IP (exemplaar niveau IP- of Load Balanced IP) met een gekoppelde netwerkbeveiligingsgroep met poorten voor inkomend web openen (80,443) weergegeven.

Security Center raadt aan dat u een WAF toohelp inrichten bescherming tegen aanvallen die gericht is op uw webtoepassingen op virtuele machines en op App Service-omgeving. Een as-omgeving (App Service omgeving) is een [Premium](https://azure.microsoft.com/pricing/details/app-service/) service-plan optie van Azure App Service die een volledig geïsoleerde en toegewezen omgeving biedt voor het veilig uitvoeren van Azure App Service-apps. toolearn meer informatie over het as-omgeving, Zie Hallo [documentatie van App Service-omgeving](../app-service/app-service-app-service-environments-readme.md).

> [!NOTE]
> Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.  Dit document is niet een stapsgewijze handleiding.
>
>

## <a name="implement-hello-recommendation"></a>Hallo aanbeveling implementeren
1. In Hallo **aanbevelingen** blade Selecteer **-webtoepassing met web application firewall Secure**.
   ![Web Application beveiligen][1]
2. In Hallo **beveiligen van uw webtoepassingen met web application firewall** blade, selecteert u een webtoepassing. Hallo **Web Application Firewall toevoegen** blade wordt geopend.
   ![Een firewall voor webtoepassingen toevoegen][2]
3. U kunt toouse een bestaande web application firewall indien beschikbaar of u kunt een nieuwe maken. In dit voorbeeld zijn er geen bestaande WAFs beschikbaar, dus we een WAF maken.
4. een WAF toocreate Selecteer een oplossing uit de lijst Hallo van geïntegreerde partners. In dit voorbeeld selecteren we **Barracuda Web Application Firewall**.
5. Hallo **Barracuda Web Application Firewall** blade wordt geopend zodat u informatie over Hallo partneroplossing. Selecteer **maken** Hallo informatie blade.

   ![Firewall-informatie-blade][3]

6. Hallo **nieuwe Web Application Firewall** blade wordt geopend, waar u kunt uitvoeren **VM-configuratie** stappen en geef **WAF informatie**. Selecteer **VM-configuratie**.
7. In Hallo **VM-configuratie** blade, voert u gegevens vereist toospin Hallo virtuele machine die wordt uitgevoerd Hallo WAF.
   ![VM-configuratie][4]
8. Retourneren van toohello **nieuwe Web Application Firewall** blade en selecteer **WAF informatie**. In Hallo **WAF informatie** blade u Hallo WAF zelf configureren. Stap 7 kunt u tooconfigure Hallo virtuele machine op welke Hallo WAF wordt uitgevoerd en stap 8 kunt u tooprovision hello WAF zelf.

## <a name="finalize-application-protection"></a>Toepassingsbeveiliging voltooien
1. Retourneren van toohello **aanbevelingen** blade. Een nieuwe vermelding is gegenereerd nadat u hebt gemaakt Hallo WAF, aangeroepen **Toepassingsbeveiliging voltooien**. Deze vermelding laat u weten dat u nodig hebt toocomplete Hallo proces daadwerkelijk voorbereiden Hallo WAF binnen hello Azure Virtual Network zodat het Hallo-toepassing kunt beveiligen.

   ![Toepassingsbeveiliging voltooien][5]

2. Selecteer **Toepassingsbeveiliging voltooien**. Er wordt een nieuwe blade geopend. U ziet dat er een webtoepassing die toohave de verkeer gerouteerd moet.
3. Selecteer Hallo-webtoepassing. Er wordt een blade geopend waarmee u stappen voor het Hallo web application firewall setup te voltooien. Hallo stappen hebt uitgevoerd en selecteer vervolgens **verkeer te beperken**. Security Center vervolgens Hallo bedrading-up voor u.

   ![Verkeer te beperken][6]

> [!NOTE]
> U kunt meerdere webtoepassingen in Security Center beveiligen door deze toepassingen tooyour bestaande WAF implementaties toe te voegen.
>
>

Hallo-logboeken van die WAF zijn nu volledig geïntegreerd. Security Center kunt starten automatisch verzamelen en analyseren van Hallo Logboeken zodat deze kan belangrijke waarschuwingen tooyou surface.

## <a name="next-steps"></a>Volgende stappen
Dit document hebt u geleerd hoe tooimplement Hallo Security Center aanbeveling "Een webtoepassing toevoegen". toolearn meer informatie over het configureren van een web application firewall Hallo ziet:

* [Web Application Firewall (WAF) configureren voor App Service-omgeving](../app-service-web/app-service-app-service-environment-web-application-firewall.md)

toolearn meer informatie over Security Center Hallo ziet:

* [Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --meer informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) --meer informatie over hoe toomonitor Hallo status van uw Azure-resources.
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) --meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.
* [Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md) --Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
* [Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) --Lees blogberichten over Azure-beveiliging en naleving.

<!--Image references-->
[1]: ./media/security-center-add-web-application-firewall/secure-web-application.png
[2]:./media/security-center-add-web-application-firewall/add-a-waf.png
[3]: ./media/security-center-add-web-application-firewall/info-blade.png
[4]: ./media/security-center-add-web-application-firewall/select-vm-config.png
[5]: ./media/security-center-add-web-application-firewall/finalize-waf.png
[6]: ./media/security-center-add-web-application-firewall/restrict-traffic.png
