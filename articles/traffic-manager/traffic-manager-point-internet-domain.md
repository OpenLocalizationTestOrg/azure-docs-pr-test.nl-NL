---
title: een bedrijf Internet domein tooa Traffic Manager-domeinnaam aaaPoint | Microsoft Docs
description: In dit artikel helpt u uw bedrijf domain name tooa Traffic Manager-domeinnaam wijst.
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 29822946-2d45-4434-ba47-fc180a445cc3
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: kumud
ms.openlocfilehash: 84c428f60a1dc70452bf957d98a68c95e0b51715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="point-a-company-internet-domain-tooan-azure-traffic-manager-domain"></a>Wijs een bedrijf Internet domein tooan Azure Traffic Manager-domein

Wanneer u een Traffic Manager-profiel maakt, wijst Azure automatisch een DNS-naam toe voor dat profiel. toouse een naam van uw DNS-zone, een DNS CNAME-record maken die wijst toohello domeinnaam van uw Traffic Manager-profiel. U vindt Hallo Traffic Manager-domeinnaam in Hallo **algemene** sectie op de configuratiepagina Hallo Hallo Traffic Manager-profiel.

Bijvoorbeeld: toopoint naam www.contoso.com toohello contoso.trafficmanager.net van Traffic Manager-DNS-naam, maakt u Hallo DNS-resourcerecord te volgen:

    www.contoso.com IN CNAME contoso.trafficmanager.net

Alle aanvragen te*www.contoso.com* te worden doorgestuurd*contoso.trafficmanager.net*.

> [!IMPORTANT]
> U een tweede niveau domein, zoals kan niet verwijzen *contoso.com*, toohello Traffic Manager-domein. DNS-protocolstandaarden staan geen CNAME-records toe voor domeinnamen van het tweede niveau.

## <a name="next-steps"></a>Volgende stappen

* [Methoden voor het doorsturen van Traffic Manager](traffic-manager-routing-methods.md)
* [Traffic Manager - Een profiel uitschakelen, inschakelen of verwijderen](disable-enable-or-delete-a-profile.md)
* [Traffic Manager - Een eindpunt in- of uitschakelen](disable-or-enable-an-endpoint.md)
