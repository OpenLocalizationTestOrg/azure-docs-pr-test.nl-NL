---
title: aaaEnabling end tooend SSL op Azure Application Gateway | Microsoft Docs
description: Deze pagina bevat een overzicht van Hallo Application Gateway end tooend ondersteuning voor SSL.
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 3976399b-25ad-45eb-8eb3-fdb736a598c5
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: amsriva
ms.openlocfilehash: c5cb398a1e7d9a08662a3120baad98edb5575917
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-end-tooend-ssl-with-application-gateway"></a>Overzicht van end tooend SSL met Application Gateway

Toepassingsgateway biedt ondersteuning voor SSL-beëindiging aan Hallo-gateway, na welk verkeer stroomt doorgaans niet-versleuteld toohello back-endservers. Deze functie kunt web servers toobe unburdened van dure versleuteling en ontsleuteling overhead. Voor sommige klanten echter is het niet-versleutelde communicatie toohello back-endservers geen acceptabele optie. Deze niet-versleutelde communicatie kan vanwege toosecurity vereisten, nalevingsvereisten, of Hallo-toepassing kan alleen een beveiligde verbinding accepteren. Voor dergelijke toepassingen ondersteunt toepassingsgateway end tooend SSL versleuteling.

## <a name="overview"></a>Overzicht

Einde tooend SSL kunt u toosecurely verzenden gevoelige gegevens toohello back-end versleuteld terwijl nog steeds profiteren van de voordelen van de functies voor taakverdeling laag 7 Hallo welke toepassingsgateway bevat. Sommige van deze functies zijn sessie cookies gebaseerde affiniteit, URL gebaseerde routering, ondersteuning voor routering op basis van sites of mogelijkheid tooinject X - doorgestuurd-* headers.

Wanneer met einde tooend SSL-communicatie-modus is geconfigureerd, wordt toepassingsgateway beëindigt Hallo SSL-sessies op Hallo-gateway en gebruikersverkeer ontsleutelt. Het is van toepassing hello geconfigureerd regels tooselect een geschikte back-end groep exemplaar tooroute verkeer naar. Toepassingsgateway vervolgens een nieuwe SSL-verbinding toohello back-endserver initieert en opnieuw versleutelt gegevens met behulp van de openbare-sleutelcertificaat Hallo back-end van de server voordat het Hallo-aanvraag toohello back-end verzendt. Einde tooend die SSL is ingeschakeld protocolinstelling door in te stellen BackendHTTPSetting tooHTTPS, die vervolgens toegepast tooa back-endpool. Elke back-endserver in de back-endpool Hallo met einde tooend die SSL ingeschakeld moet worden geconfigureerd met een certificaat tooallow veilige communicatie.

![einde tooend ssl scenario][1]

In dit voorbeeld worden aanvragen TLS1.2 via gerouteerde toobackend-servers in Pool1 end tooend SSL gebruiken.

## <a name="end-tooend-ssl-and-whitelisting-of-certificates"></a>End tooend SSL en whitelisting van certificaten

Toepassingsgateway communiceert alleen met bekende back-end-instanties die goedgekeurde lijst hun certificaat met de toepassingsgateway Hallo hebben. tooenable whitelisting van certificaten, moet u de openbare sleutel Hallo van back-end server certificaten toohello toepassingsgateway (geen basiscertificaat Hallo) uploaden. Alleen verbindingen tooknown en goedgekeurde lijst back-ends zijn vervolgens toegestaan. back-ends resterende Hallo resulteert in een gateway-fout. Zelfondertekende certificaten zijn uitsluitend bedoeld voor testdoeleinden en het wordt afgeraden om deze in een productieomgeving te gebruiken. Deze certificaten hebben toobe goedgekeurde lijst met Hallo toepassingsgateway zoals beschreven in Hallo vorige stappen voordat ze kunnen worden gebruikt.

## <a name="next-steps"></a>Volgende stappen

Nadat u hebt leren over end tooend SSL gaat te[end tooend SSL in toepassingsgateway inschakelen](application-gateway-end-to-end-ssl-powershell.md) toocreate wordt gebruikt door een toepassing gateway eindigen tooend SSL.

<!--Image references-->

[1]: ./media/application-gateway-backend-ssl/scenario.png
