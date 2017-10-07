---
title: aaaApplication Gateway integratie met Azure Security Center | Microsoft Docs
description: "Deze pagina bevat informatie over hoe Application Gateway is geïntegreerd in Azure Security Center."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: e5ea5cf9-3b41-4b85-a12c-e758bff7f3ec
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 06/07/2017
ms.author: gwallace
ms.openlocfilehash: 6f6ace105e84c01f525ab02938e81ce040c5c9d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a>Overzicht van de integratie tussen Application Gateway en Azure Security Center

Meer informatie over hoe Application Gateway en Security Center beter beveiligen van uw webtoepassingsbronnen. Application gateway web application firewall (WAF) kan worden geïntegreerd met [Security Center](../security-center/security-center-intro.md) tooprovide een tooprevent naadloze weergave detecteren en reageren toothreats toounprotected webtoepassingen in uw omgeving.

## <a name="overview"></a>Overzicht

Application Gateway WAF wordt aanbevolen in Security Center voor het beveiligen van webtoepassingen van aanvallen en beveiligingsproblemen. Ingeschakeld webbronnen die niet zijn beveiligd door WAF weergegeven in het Beveiligingscentrum Hallo als hoog dreigingsniveau aanbevelingen. Aanbevelingen voor web application firewalls worden weergegeven op Hallo **overzicht** pagina onder **toepassingen**.

![integratie met security center][1]

Geen aanbevelingen met betrekking tot de web application firewall op, wordt een nieuwe blade met details op Hallo van Hallo aanbeveling geopend.

## <a name="add-a-web-application-firewall-tooan-existing-resource"></a>Een web application firewall tooan bestaande resource toevoegen

Navigeer te**meer Services** > **beveiliging en identiteit** > **Security Center** en op Hallo **Security Center - overzicht**  blade, klikt u op **toepassingen**. Op Hallo **Security Center - toepassingen** blade Hallo tabel bevat een lijst met toepassingen die Security Center gedetecteerd in uw abonnement.

![webtoepassingen][3]

Door te klikken op een webtoepassing met een kritiek probleem, u Hallo **beveiligingsstatus van de toepassing** blade. Hallo-webtoepassing die niet wordt beveiligd door een web application firewall in Hallo afbeelding hieronder. 

![webbronnen niet beveiligd][2]

Klik op **web application firewall toevoegen** onder **aanbevelingen** tooopen hello **Web Application Firewall toevoegen** blade.

Als u geen hebben van een bestaande toepassingsgateway of toocreate een nieuwe wilt, klikt u op **nieuw** en op Hallo **maken van een nieuwe Web Application Firewall** blade en klik op **Microsoft - Toepassingsgateway**. Hiermee gaat u door Hallo stappen toocreate een toepassingsgateway. Uw webtoepassing is op dit punt wordt toegevoegd als een beveiligde bron, nu Security Center, houdt dat deze bron wordt beveiligd door een web application firewall. Hiermee wordt het niet als een lid van de groep back-end toegevoegd.

Als u een bestaande toepassingsgateway hebt, kunt u deze onder **bestaande oplossing gebruiken**

![blade Web application firewall toevoegen][4]

Toevoegen van dat een toepassingsgateway web application tooan door Security Center voegt geen Hallo resource als lid van de groep back-end, moet u dit doen op Hallo toepassingsgatewayresource rechtstreeks.

## <a name="add-a-resource-tooan-existing-web-application-firewall"></a>Een resource tooan bestaande web application firewall toevoegen

Navigeer te**meer Services** > **beveiliging en identiteit** > **Security Center** en op Hallo **Security Center - overzicht**  blade, klikt u op **partneroplossingen**. Bestaande Security Center op de hoogte Toepassingsgateways weergeven in Hallo **partneroplossingen** blade.

![partneroplossingen][7]

Klik op **app koppelen** tooopen hello **toepassingen koppelen** blade Hier krijgt u Hallo opties tooselect bestaande toepassingen. Kies Hallo toepassingen tooprotect en klik op **OK**. Hiermee voegt geen Hallo web application toohello back-endpool van de toepassingsgateway Hallo. Hiermee stelt u Hallo resources als een beveiligde bron zodat Security Center kunnen worden bijgehouden. tooadd hello resource als lid van de groep back-end, moet u dit doen in de toepassingsgateway hello, huidige Hallo-blade kunt u op **oplossingenconsole** toobe genomen toohello toepassingsgatewayresource waarin u web Hallo kunt toevoegen toepassingsgroep toohello back-end.

![toepassingen van partners oplossingen][6]

## <a name="finalize-configuration"></a>Configuratie voltooien

Toepassingsgateway tooan Security Center houdt toepassingen toegevoegd als een beveiligde bron.  Hallo-status van deze bron wordt gecontroleerd en zorgt ervoor dat deze wordt beveiligd door een toepassingsgateway. de volgende stap Hallo is tooadd Hallo privé-IP, openbare IP-adres of NIC van uw virtuele machine toohello back-endpool van de toepassingsgateway Hallo. Totdat een extra aanbeveling van dit is **Toepassingsbeveiliging voltooien** wordt weergegeven totdat Hallo resource is toegevoegd.

![blade Web application firewall toevoegen][5]

## <a name="security-alerts"></a>Beveiligingswaarschuwingen

In Security Center te navigeren**detectie** > **beveiligingswaarschuwingen**.  Hier vindt u WAF waarschuwingen voor uw Toepassingsgateways. Waarschuwingen worden opgesplitst op WAF regel.

![beveiligingswaarschuwingen][8]

Te klikken op een regel om een lijst met waarschuwingen voor die specifieke WAF regel te bieden. Elke waarschuwing bevat aanvullende informatie op Hallo kan vinden. Hallo details bevatten een koppeling toohello application gateway.
 
![Waarschuwingsdetails][9]

## <a name="next-steps"></a>Volgende stappen

hoe tooenable web application firewall op een bestaande toepassingsgateway gaat u naar toolearn [maken of bijwerken van een Azure-toepassingsgateway met web application firewall](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png