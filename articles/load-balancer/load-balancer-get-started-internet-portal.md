---
title: aaaCreate een internetgerichte load balancer - Azure-portal | Microsoft Docs
description: Meer informatie over hoe een internetgerichte toocreate load balancer met behulp van Resource Manager hello Azure-portal
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: aa9d26ca-3d8a-4a99-83b7-c410dd20b9d0
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: annahar
ms.openlocfilehash: 390ba8ec1474c54cf2c0022c4a3c219d21b1a659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-hello-azure-portal"></a>Maken van een Internet gerichte load balancer met hello Azure-portal

> [!div class="op_single_selector"]
> * [Portal](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Sjabloon](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel. U kunt ook [meer informatie over hoe een internetgerichte toocreate netwerktaakverdeler via de klassieke implementatie](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

Dit heeft betrekking op Hallo volgorde van de afzonderlijke taken die zijn gedaan toobe toocreate een load balancer en in detail uitgelegd wat tooaccomplish Hallo doel wordt uitgevoerd.

## <a name="what-is-required-toocreate-an-internet-facing-load-balancer"></a>Wat is vereist toocreate een internetgerichte load balancer?

U moet toocreate en configureer Hallo objecten toodeploy een load balancer te volgen.

* Front-end-IP-configuratie: bevat openbare IP-adressen voor inkomend netwerkverkeer.
* Back-end-adresgroep - bevat netwerkinterfaces (NIC's) voor virtuele machines tooreceive-netwerkverkeer Hallo van Hallo load balancer.
* Taakverdeling regels - bevat regels voor toewijzing van een openbare poort op Hallo load balancer tooport in Hallo back-end-adresgroep.
* Binnenkomende NAT-regels: regels voor toewijzing van een openbare poort op Hallo load balancer tooa poort voor een specifieke virtuele machine in het back-end-adresgroep Hallo bevat.
* Tests - beschikbaarheid van health-tests gebruikt toocheck van exemplaren van virtuele machines in het back-end-adresgroep Hallo bevat.

Meer informatie over de load balancer-onderdelen in Azure Resource Manager vindt u op [Ondersteuning van Azure Resource Manager voor Azure Load Balancer](load-balancer-arm.md).

## <a name="set-up-a-load-balancer-in-azure-portal"></a>Een load balancer instellen in Azure Portal

> [!IMPORTANT]
> In dit voorbeeld wordt ervan uitgegaan dat u een virtueel netwerk hebt met de naam **myVNet**. Raadpleeg te[virtueel netwerk maken](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) toodo dit. Ook wordt ervan uitgegaan er is een subnet binnen **myVNet** aangeroepen **LB Subnet worden** en twee virtuele machines genoemd **web1** en **web2** respectievelijk binnen Hallo dezelfde beschikbaarheidsset aangeroepen **myAvailSet** in **myVNet**. Raadpleeg te[deze koppeling](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toocreate virtuele machines.

1. Ga vanuit een browser toohello Azure-portal: [http://portal.azure.com](http://portal.azure.com) en meld u aan met uw Azure-account.
2. Selecteer op de bovenste linkerkant met Hallo van welkomstscherm **nieuw** > **Networking** > **Load Balancer.**
3. In Hallo **maken load balancer** blade, typ een naam voor de load balancer. Hier wordt deze **myLoadBalancer** genoemd.
4. Selecteer onder **Type** de optie **Openbaar**.
5. Maak onder **Openbaar IP-adres** een nieuw openbaar IP-adres met de naam **myPublicIP**.
6. Selecteer onder Resourcegroep de optie **myRG**. Selecteer een geschikte **Locatie** en klik vervolgens op **OK**. Hallo load balancer wordt toodeploy start en duurt een paar minuten toosuccessfully volledige implementatie.

    ![Resourcegroep voor load balancer bijwerken](./media/load-balancer-get-started-internet-portal/1-load-balancer.png)

## <a name="create-a-back-end-address-pool"></a>Een back-endadresgroep maken

1. Zodra de load balancer is geïmplementeerd, selecteert u deze in uw resources. Selecteer in de instellingen Back-endgroepen. Voer een naam voor uw back-endgroep in. Klik vervolgens op Hallo **toevoegen** knop naar de bovenkant Hallo van Hallo-blade die wordt weergegeven.
2. Klik op **toevoegen van een virtuele machine** in Hallo **toevoegen van de back-endpool** blade.  Selecteer **Een beschikbaarheidsset kiezen** onder **Beschikbaarheidsset** en selecteer **myAvailSet**. Selecteer vervolgens **Hallo virtuele machines kiezen** onder sectie voor virtuele Machines in de blade Hallo Hallo en klik op **web1** en **web2**, Hallo twee virtuele machines die zijn gemaakt voor taakverdeling. Zorg ervoor dat beide selectievakjes in blauw toohello links zoals weergegeven in onderstaande afbeelding voor Hallo. Klik vervolgens op **Selecteer** op die blade gevolgd door OK in Hallo **kiezen virtuele machines** blade en vervolgens **OK** in Hallo **toevoegen van de back-endpool** blade.

    ![Toohello back-endadresgroep - toevoegen ](./media/load-balancer-get-started-internet-portal/3-load-balancer-backend-02.png)

3. Controleer of uw meldingen vervolgkeuzelijst toomake is een update met betrekking tot opgeslagen Hallo load balancer back-endpool in toevoeging tooupdating Hallo netwerkinterface voor zowel virtuele machines Hallo **web1** en **web2**.

## <a name="create-a-probe-lb-rule-and-nat-rules"></a>Een test, LB-regel en NAT-regels maken

1. Maak een statustest.

    Selecteer Testen in de instellingen van de load balancer. Klik vervolgens op **toevoegen** Hallo boven aan de blade Hallo.

    Er zijn twee manieren tooconfigure een test: HTTP of TCP. In dit voorbeeld wordt HTTP gebruikt, maar TCP kan op een vergelijkbare manier worden geconfigureerd.
    De benodigde informatie Hallo bijwerken. Zoals is vermeld, verdeelt **myLoadBalancer** het verkeer op poort 80. geselecteerde Hallo-pad is HealthProbe.aspx, Interval is 15 seconden en drempelwaarde voor onjuiste status 2 is. Wanneer u klaar bent, klikt u op **OK** toocreate Hallo test.

    Laat de aanwijzer op Hallo 'i' pictogram toolearn meer over deze afzonderlijke configuraties en hoe deze gewijzigde toocater tooyour vereisten kunnen zijn.

    ![Een test toevoegen](./media/load-balancer-get-started-internet-portal/4-load-balancer-probes.png)

2. Maak een load balancer-regel.

    Klik op de Load-balancingregels in Hallo sectie instellingen van de load balancer. Klik in de nieuwe blade hello, op **toevoegen**. Geef uw regel een naam. Hier gebruiken we HTTP. Kies Hallo frontend-poort en back-end. Hier is 80 gekozen voor beide. Kies **LB-back-end** als uw back-endpool en de eerder gemaakte Hallo **HealthProbe** zoals Hallo test. Andere configuraties kunnen worden ingesteld op basis van tooyour vereisten. Klik vervolgens op OK toosave hello taakverdelingsregel.

    ![Een taakverdelingsregel toevoegen](./media/load-balancer-get-started-internet-portal/5-load-balancing-rules.png)

3. Inkomende NAT-regels maken

    Klik op de binnenkomende NAT-regels onder de sectie settings Hallo van de load balancer. Hallo nieuwe blade die, klikt u op **toevoegen**. Geef uw inkomende NAT-regel een naam. Hier gebruiken we de naam **inboundNATrule1**. Hallo-doel moet Hallo die openbare IP-adres eerder hebt gemaakt. Selecteer aangepast onder Service en selecteert u graag toouse Hallo-protocol. Hier is TCP geselecteerd. Hallo-poort, voer 3441 en Hallo doelpoort, in dit geval 3389. Klik vervolgens op OK toosave met deze regel.

    Zodra de eerste regel Hallo is gemaakt, kunt u deze stap herhalen voor Hallo tweede binnenkomende NAT-regel inboundNATrule2 aangeroepen vanuit poort 3442 tooTarget poort 3389.

    ![Een inkomende NAT-regel toevoegen](./media/load-balancer-get-started-internet-portal/6-load-balancer-inbound-nat-rules.png)

## <a name="remove-a-load-balancer"></a>Een load balancer verwijderen

een load balancer, selecteer Hallo toodelete netwerktaakverdeler gewenste tooremove. In Hallo *Load Balancer* blade, klik op **verwijderen** Hallo boven aan de blade Hallo. Selecteer **Ja** wanneer dit wordt gevraagd.

## <a name="next-steps"></a>Volgende stappen

[Aan de slag met het configureren van een interne load balancer](load-balancer-get-started-ilb-arm-cli.md)

[Een distributiemodus voor de load balancer configureren](load-balancer-distribution-mode.md)

[TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren](load-balancer-tcp-idle-timeout.md)
