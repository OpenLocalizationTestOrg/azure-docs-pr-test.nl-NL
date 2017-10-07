---
title: een interne load balancer - Azure-portal aaaCreate | Microsoft Docs
description: Meer informatie over hoe de toocreate een interne load balancer in Resource Manager, met behulp van hello Azure-portal
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ac14fb9-8d14-4892-bfe6-8bc74c48ae2c
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 80124217a84857b542eb41cb814ec97234176dd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-in-hello-azure-portal"></a>Maken van een interne load balancer in hello Azure-portal

> [!div class="op_single_selector"]
> * [Azure Portal](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Sjabloon](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).  In dit artikel wordt beschreven hoe u Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van Hallo aanbeveelt [klassieke implementatiemodel](load-balancer-get-started-ilb-classic-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a>Aan de slag met het maken van een interne load balancer met behulp van Azure Portal

Hallo volgende stappen toocreate een interne load balancer uit hello Azure Portal gebruiken.

1. Open een browser en ga toohello [Azure-portal](http://portal.azure.com), en meld u aan met uw Azure-account.
2. In Hallo bovenste linkerzijde van Hallo scherm, klikt u op **nieuw** > **Networking** > **Load balancer**.
3. In Hallo **maken load balancer** blade, voer een **naam** voor de load balancer.
4. Klik onder **Schema** op **Intern**.
5. Klik op **virtueel netwerk**, en vervolgens selecteert Hallo virtueel netwerk waar u toocreate Hallo load balancer.

   > [!NOTE]
   > Als u Hallo virtueel netwerk die u wilt dat toouse niet ziet, controleert u Hallo **locatie** u gebruikt voor Hallo load balancer en dienovereenkomstig wijzigen.

6. Klik op **Subnet**, en selecteer vervolgens Hallo subnet waar u toocreate Hallo load balancer.
7. Onder **IP-adrestoewijzing**, klikt u op **dynamische** of **statische**, afhankelijk van of u Hallo IP-adres wilt voor Hallo load balancer toobe vaste (statische) of niet.

   > [!NOTE]
   > Als u een statisch IP-adres toouse selecteert, hebt u tooprovide een adres voor Hallo load balancer.

8. Onder **resourcegroep** Geef Hallo-naam van een nieuwe resourcegroep voor Hallo load balancer, of klik op **Selecteer een bestaande** en selecteer een bestaande resourcegroep.
9. Klik op **Create**.

## <a name="configure-load-balancing-rules"></a>Taakverdelingsregels configureren

Na het Hallo load balancer maken, gaat u toohello load balancer resource tooconfigure deze.
U moet tooconfigure eerst een back-end-adresgroep en een test voordat u een load-balancingregel configureert.

### <a name="step-1-configure-a-back-end-pool"></a>Stap 1: Een back-endgroep configureren

1. Klik in hello Azure-portal, op **Bladeren** > **Taakverdelers**, en klik vervolgens op Hallo load balancer die eerder is gemaakt.
2. In Hallo **instellingen** blade, klikt u op **back-endpools**.
3. In Hallo **back-end-adresgroepen** blade, klikt u op **toevoegen**.
4. In Hallo **back-endpool toevoegen** blade, voer een **naam** voor Hallo back-endpool en klik vervolgens op **OK**.

### <a name="step-2-configure-a-probe"></a>Stap 2: Een test configureren

1. Klik in hello Azure-portal, op **Bladeren** > **Taakverdelers**, en klik vervolgens op Hallo load balancer die eerder is gemaakt.
2. In Hallo **instellingen** blade, klikt u op **tests**.
3. In Hallo **Probes** blade, klikt u op **toevoegen**.
4. In Hallo **toevoegen test** blade, voer een **naam** voor de test Hallo.
5. Selecteer onder **Protocol** **HTTP** (voor websites) of **TCP** (voor andere TCP-toepassingen).
6. Onder **poort**, Hallo poort toouse opgeven bij het openen van Hallo test.
7. Onder **pad** (voor HTTP-tests alleen) Hallo pad toouse als een test opgeven.
8. Onder **Interval** opgeven hoe vaak tooprobe toepassing hello.
9. Onder **drempelwaarde voor onjuiste status**, geef het aantal pogingen moeten worden gemist voordat Hallo back-end virtuele machine is als beschadigd gemarkeerd.
10. Klik op **OK** toocreate test.

### <a name="step-3-configure-load-balancing-rules"></a>Stap 3: Taakverdelingsregels configureren

1. Klik in hello Azure-portal, op **Bladeren** > **Taakverdelers**, en klik vervolgens op Hallo load balancer die eerder is gemaakt.
2. In Hallo **instellingen** blade, klikt u op **Taakverdelingsregels**.
3. In Hallo **Taakverdelingsregels** blade, klikt u op **toevoegen**.
4. In Hallo **toevoegen taakverdelingsregel** blade, voer een **naam** voor Hallo regel.
5. Selecteer onder **Protocol** **HTTP** (voor websites) of **TCP** (voor andere TCP-toepassingen).
6. Onder **poort**, opgeven Hallo poort clients verbinding tooin Hallo load balancer.
7. Onder **backendpoort**, Hallo poort toobe gebruikt in de back-endpool Hallo opgeven (meestal Hallo load balancer-poort en back-endpoort Hallo zijn Hallo dezelfde).
8. Onder **back-endpool**, selecteer Hallo back-end-groep u die eerder is gemaakt.
9. Onder **sessiepersistentie**, selecteer de manier waarop u wilt dat toopersist sessies.
10. Onder **time-out voor inactiviteit (minuten)**, time-out voor inactiviteit van Hallo opgeven.
11. Klik onder **Zwevend IP (Direct Server Return)** op **Uitgeschakeld** of **Ingeschakeld**.
12. Klik op **OK**.

## <a name="next-steps"></a>Volgende stappen

[Een distributiemodus voor de load balancer configureren](load-balancer-distribution-mode.md)

[TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren](load-balancer-tcp-idle-timeout.md)

