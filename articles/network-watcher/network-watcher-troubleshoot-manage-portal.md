---
title: aaaTroubleshoot Azure Virtual Network Gateway en verbindingen - PowerShell | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe de PowerShell-cmdlet voor het oplossen van toouse hello Azure-netwerk-Watcher
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: bd568d34091209390c57d22475559bdb99ad2c59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a>Problemen met virtuele netwerkgateway en verbindingen met behulp van PowerShell voor Azure-netwerk-Watcher

> [!div class="op_single_selector"]
> - [Portal](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [REST API](network-watcher-troubleshoot-manage-rest.md)

Netwerk-Watcher biedt veel mogelijkheden met betrekking toounderstanding uw netwerkbronnen in Azure. Een van deze mogelijkheden resource is het oplossen van problemen. Het oplossen van bron kan worden aangeroepen via Hallo-portal, PowerShell, CLI of REST-API. Als deze wordt aangeroepen, netwerk-Watcher Hallo status van de Gateway van een virtueel netwerk of een verbinding inspecteert en retourneert de bevindingen zijn.

## <a name="before-you-begin"></a>Voordat u begint

Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.

Voor een lijst met ondersteunde gateway typen bezoek, [ondersteund gatewaytypen](network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Overzicht

Het oplossen van resource biedt Hallo mogelijkheid oplossen van problemen die zich bij het virtuele netwerkgateways en verbindingen voordoen. Wanneer een aanvraag wordt gedaan tooresource probleemoplossing, logboeken worden opgevraagd en geïnspecteerd. Als controle voltooid is, worden Hallo resultaten geretourneerd. Resources voor probleemoplossing aanvragen zijn langlopende aanvragen die meerdere minuten tooreturn een resultaat kan krijgen. Hallo-logboeken van het oplossen van problemen worden opgeslagen in een container voor een opslagaccount die is opgegeven.

## <a name="troubleshoot-a-gateway-or-connection"></a>Problemen oplossen met een gateway of de verbinding

1. Navigeer toohello [Azure-portal](https://portal.azure.com) en klik op **Networking** > **netwerk-Watcher** > **VPN-diagnostische gegevens**
2. Selecteer een **abonnement**, **resourcegroep**, en **locatie**.
3. Het oplossen van resource retourneert gegevens over de status Hallo van Hallo resource. Bovendien bespaart u relevante logboeken tooa storage-account toobe gecontroleerd. Klik op **Opslagaccount** tooselect een opslagaccount.
4. Op Hallo **opslagaccounts** blade, selecteer een bestaand opslagaccount of klik op **+ opslagaccount** toocreate een nieuwe.
5. Op Hallo **Containers** blade, kies een bestaande container of klik op **+ Container** toocreate een nieuwe container. Klik wanneer u klaar **selecteren**
6. Hallo-Gateway en verbinding resources tootroubleshoot selecteren en op **probleemoplossing starten**

Als meerdere resources zijn geselecteerd, wordt het oplossen van problemen gelijktijdig op bronnen van de gateway uitgevoerd. Taak kan niet worden uitgevoerd op een verbinding en de bijbehorende gateway op Hallo hetzelfde moment. Het verdient aanbeveling tootroubleshoot gateways eerst verbinding probleemoplossing is meer tijd in beslag. Terwijl de VPN-diagnostische gegevens wordt uitgevoerd op een resource Hallo **probleemoplossing STATUS** kolom geeft de status van **uitgevoerd**

Als u klaar Hallo u kolom statuswijzigingen te**goed** of **niet in orde**.

![volledige oplossen][2]

## <a name="understanding-hello-results"></a>Understanding Hallo resultaten

In Hallo **Details** sectie van het venster Hallo Hallo **Status** tabblad toont Hallo status van laatste probleemoplossing Hallo uitvoeren op Hallo geselecteerd resource. Resultaten van de meest recente diagnose Hallo zijn weergegeven xx minuten na Hallo het laatst is uitgevoerd.

|Eigenschap  |Beschrijving  |
|---------|---------|
|Resource     | Een koppeling toohello bron.        |
|Pad voor opslag     |  Pad toohello opslagaccount en container die Hallo logboeken bevatten (als er een zijn geproduceerd tijdens Hallo uitvoeren). Deze instelling niet bewaard is gebleven nadat u de portal Hallo verlaten.        |
|Samenvatting     | Samenvatting van de resourcestatus Hallo.        |
|Details     | Gedetailleerde informatie over de resourcestatus Hallo.        |
|Laatste uitvoering     | Hallo Hallo tijd laatste tijd probleemoplossing is uitgevoerd.        |


Hallo **actie** tabblad bevat algemene richtlijnen over hoe tooresolve Hallo probleem. Als een actie kan worden ondernomen voor Hallo probleem, wordt een koppeling geboden met aanvullende richtlijnen. In geval van Hallo wanneer er geen aanvullende richtlijnen, antwoord Hallo biedt Hallo url tooopen een ondersteuningsaanvraag.  Voor meer informatie over het Hallo-eigenschappen van antwoord Hallo en wat is opgenomen, gaat u naar [overzicht van netwerk-Watcher oplossen](network-watcher-troubleshoot-overview.md)


## <a name="next-steps"></a>Volgende stappen

Als de instellingen zijn gewijzigd die stop VPN-verbindingen, raadpleegt u [Netwerkbeveiligingsgroepen beheren](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack omlaag Hallo groep en beveiliging netwerkbeveiligingsregels die betrokken zijn.


[2]: ./media/network-watcher-troubleshoot-manage-portal/2.png
