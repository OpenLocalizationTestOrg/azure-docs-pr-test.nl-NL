---
title: aaaCreate een internetgerichte load balancer - Azure classic-portal | Microsoft Docs
description: Meer informatie over hoe een Internet gerichte load balancer aan classic deployment model met toocreate Hallo klassieke Azure-portal
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fa3e93c0-968a-472d-a17c-65665c050db2
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 27b0d5af6e7b493fa94a9dfbfa260483ae95a2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-classic-portal"></a>Maken van een Internetgericht load balancer (klassiek) Hallo klassieke Azure-portal aan de slag

> [!div class="op_single_selector"]
> * [Klassieke Azure Portal](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Azure Cloud Services](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Voordat u met Azure-resources werkt, is het belangrijk toounderstand dat Azure momenteel twee implementatiemodellen heeft: Azure Resource Manager en het klassieke model. Zorg ervoor dat u begrijpt wat [implementatiemodellen en hulpprogramma's](../azure-classic-rm.md) zijn voordat u met een Azure-resource gaat werken. U kunt Hallo-documentatie voor verschillende hulpprogramma's bekijken door te klikken op de tabbladen Hallo Hallo boven aan dit artikel. In dit artikel bevat informatie over Hallo klassieke implementatiemodel. U kunt ook [meer informatie over hoe een internetverbinding toocreate netwerktaakverdeler met Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a>Een internetgerichte load balancer voor virtuele machines instellen

In de volgorde tooload saldo netwerkverkeer van Hallo Internet over Hallo virtuele machines van een cloudservice, moet u een set met gelijke taakverdeling maken. Deze procedure wordt ervan uitgegaan dat u al Hallo virtuele machines hebt gemaakt en dat ze alle zijn binnen Hallo dezelfde cloudservice.

**tooconfigure een set met gelijke taakverdeling voor virtuele machines**

1. Klik in de klassieke Azure-portal hello, **virtuele Machines**, en klik vervolgens op Hallo-naam van een virtuele machine in Hallo taakverdeling set.
2. Klik op **Eindpunten** en vervolgens op **Toevoegen**.
3. Op Hallo **toevoegen van een virtuele machine van de endpoint tooa** pagina, klikt u op Hallo pijl-rechts.
4. Op Hallo **Geef details op Hallo van Hallo eindpunt** pagina:

   * In **naam**, typ een naam voor het Hallo-eindpunt of selecteer Hallo naam in Hallo lijst met vooraf gedefinieerde eindpunten voor algemene protocollen.
   * In **Protocol**, selecteer Hallo-protocol is vereist voor het Hallo-type van het eindpunt, TCP of UDP, indien nodig.
   * In **poort van de openbare en particuliere poort**, typt u Hallo poortnummers die u wilt dat Hallo toouse van de virtuele machine, indien nodig. U kunt Hallo particuliere poort en firewallregels op Hallo virtuele machine tooredirect verkeer op een manier die geschikt is voor uw toepassing gebruiken. Hallo particuliere poort kan hetzelfde als de openbare poort Hallo Hallo. U kan bijvoorbeeld poort 80 tooboth Hallo openbare en particuliere poort toewijzen voor een eindpunt voor internetverkeer (HTTP).

5. Selecteer **een set met gelijke taakverdeling maken**, en klik vervolgens op pijl-rechts Hallo.
6. Op Hallo **Hallo taakverdeling set configureren** pagina, typ een naam voor Hallo Netwerktaakverdeling instellen en vervolgens Hallo waarden voor het gedrag van de test Hallo Azure Load Balancer worden toegewezen. Hallo Load Balancer gebruikt tests toodetermine indien Hallo virtuele machines in Hallo taakverdeling set beschikbaar tooreceive inkomend verkeer zijn.
7. Klik op Hallo vinkje toocreate Hallo taakverdeling eindpunt. U ziet **Ja** in Hallo **taakverdeling setnaam** kolom Hallo **eindpunten** pagina voor Hallo virtuele machine.
8. Klik in de portal Hallo op **virtuele Machines**, klikt u op naam van een extra virtuele machine in Hallo taakverdeling set hello, klik op **eindpunten**, en klik vervolgens op **toevoegen**.
9. Op Hallo **toevoegen van een virtuele machine van de endpoint tooa** pagina, klikt u op **eindpunt tooan bestaande taakverdeling set toevoegen**, selecteert u de naam Hallo van Hallo taakverdeling set en klik op Hallo pijl-rechts.
10. Op Hallo **Geef details op Hallo van Hallo eindpunt** pagina en klik vervolgens op het vinkje Hallo Typ een naam voor het Hallo-eindpunt.

Herhaal stap 8-10 voor Hallo aanvullende virtuele machines in Hallo taakverdeling set.

## <a name="next-steps"></a>Volgende stappen

[Aan de slag met het configureren van een interne load balancer](load-balancer-get-started-ilb-arm-ps.md)

[Een distributiemodus voor de load balancer configureren](load-balancer-distribution-mode.md)

[TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren](load-balancer-tcp-idle-timeout.md)
