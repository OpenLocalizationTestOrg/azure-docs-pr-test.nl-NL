---
title: aaaManage netwerk groep stroom beveiligingslogboeken met Azure-netwerk-Watcher | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe toomanage Netwerkbeveiligingsgroep stroom wordt geregistreerd in Azure-netwerk-Watcher
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 01606cbf-d70b-40ad-bc1d-f03bb642e0af
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fb250337ab9d1a0c0d0d3569c00bc221dd102a3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-group-flow-logs-in-hello-azure-portal"></a>Netwerk groep stroom beveiligingslogboeken in hello Azure-portal beheren

> [!div class="op_single_selector"]
> - [Azure Portal](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [CLI 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [REST API](network-watcher-nsg-flow-logging-rest.md)

Groep netwerk-stroom beveiligingslogboeken zijn een functie van netwerk-Watcher waarmee u tooview informatie over inkomende en uitgaande IP-verkeer via een netwerkbeveiligingsgroep. Deze stroom logboeken zijn geschreven in JSON-indeling en belangrijke informatie bevatten met inbegrip van: 

- Binnenkomende en uitgaande stromen per regel op basis van een.
- Hallo NIC die Hallo stroom is van toepassing op.
- 5-tuple informatie over het Hallo-stroom (bron/het doel-IP-poort van de bron/het doel, protocol).
- Informatie over of verkeer is toegestaan of geweigerd.

## <a name="before-you-begin"></a>Voordat u begint

Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een exemplaar van de netwerk-Watcher](network-watcher-create.md). Hallo scenario ook wordt ervan uitgegaan dat u een resourcegroep met een geldige virtuele machine.

## <a name="register-insights-provider"></a>Insights provider registreren

Voor verkeersstroom Hallo logboekregistratie toowork, **Microsoft.Insights** provider moet worden geregistreerd. tooregister Hallo-provider, nemen Hallo stappen te volgen: 

1. Ga te**abonnementen**, en selecteer vervolgens Hallo-abonnement waarvoor u tooenable stroom logboeken wilt. 
2. Op Hallo **abonnement** blade Selecteer **Resourceproviders**. 
3. Bekijkt hello lijst met providers en controleer of deze Hallo **microsoft.insights** provider is geregistreerd. Zo niet, selecteer vervolgens **registreren**.

![Weergave-providers][providers]

## <a name="enable-flow-logs"></a>Stroom Logboeken inschakelen

Deze stappen gaat u door Hallo-proces voor het inschakelen van Logboeken van de stroom op een netwerkbeveiligingsgroep.

### <a name="step-1"></a>Stap 1

Ga tooa netwerk-Watcher-exemplaar en selecteer vervolgens **NSG stromen logboeken**.

![Overzicht van de stroom-Logboeken][1]

### <a name="step-2"></a>Stap 2

Selecteer een netwerkbeveiligingsgroep in Hallo-lijst.

![Overzicht van de stroom-Logboeken][2]

### <a name="step-3"></a>Stap 3 

Op Hallo **stroom logboeken instellingen** blade Hallo status te instellen**op**, en configureer vervolgens een opslagaccount.  Wanneer u bent klaar, selecteert u **OK**. Selecteer vervolgens **opslaan**.

![Overzicht van de stroom-Logboeken][3]

## <a name="download-flow-logs"></a>Stroom logboeken downloaden

Stroom logboeken worden opgeslagen in een opslagaccount. De stroom logboeken tooview downloaden ze.

### <a name="step-1"></a>Stap 1

Logboeken van de stroom toodownload, selecteer **kunt u stroom logboeken downloaden van de geconfigureerde opslagaccounts**. Deze stap gaat u weergave tooa storage-account waarin u kunt kiezen welke toodownload Logboeken.

![Instellingen voor logboeken stromen][4]

### <a name="step-2"></a>Stap 2

Ga toohello juiste storage-account. Selecteer vervolgens **Containers** > **insights-log-networksecuritygroupflowevent**.

![Instellingen voor logboeken stromen][5]

### <a name="step-3"></a>Stap 3

Ga toohello locatie van Hallo stroom logboek, selecteert u deze en selecteer **downloaden**.

![Instellingen voor logboeken stromen][6]

Voor informatie over het Hallo-structuur van Hallo logboek, gaat u naar [netwerk groep stroom logboek beveiligingsoverzicht](network-watcher-nsg-flow-logging-overview.md).

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe te[visualiseren van uw NSG stroom logboeken met Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md).

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
