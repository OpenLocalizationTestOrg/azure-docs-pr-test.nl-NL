---
title: aaaMultiple IP-adressen voor virtuele machines in Azure - Portal | Microsoft Docs
description: Meer informatie over hoe tooassign meerdere IP-adressen tooa virtuele machine met Azure-portal Hallo | Resource Manager.
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 3a8cae97-3bed-430d-91b3-274696d91e34
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/30/2016
ms.author: annahar
ms.openlocfilehash: 34075766ac68c8de38c258a4d70e35881f28bb0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-portal"></a>Meerdere IP-adressen toovirtual machines hello Azure-portal met toewijzen

>[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]
>
Dit artikel wordt uitgelegd hoe een virtuele machine (VM) via hello Azure Resource Manager deployment model met behulp van toocreate hello Azure-portal. Meerdere IP-adressen kunnen niet worden toegewezen als tooresources via de klassieke implementatiemodel Hallo is gemaakt. meer informatie over Azure-implementatiemodellen, Hallo lezen toolearn [begrijpen implementatiemodellen](../resource-manager-deployment-model.md) artikel.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Een virtuele machine maken met meerdere IP-adressen

Als u een virtuele machine met meerdere IP-adressen of een statisch privé IP-adres toocreate wilt, moet u deze met PowerShell of Azure CLI Hallo maken. Klik op Hallo PowerShell of CLI opties Hallo boven aan dit artikel toolearn hoe. U kunt een virtuele machine maken met één dynamische particuliere IP-adres en (optioneel) op één openbaar IP-adres met Hallo-portal door Hallo stappen in Hallo [maken van een virtuele machine van Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md) of [maken van een Linux-VM](../virtual-machines/linux/quick-create-portal.md) artikelen. Nadat u Hallo VM gemaakt, kunt u Hallo IP-adrestype van dynamische toostatic wijzigen en toevoegen van extra IP-adressen met Hallo-portal door stap in Hallo [toevoegen IP-adressen tooa VM](#add) sectie van dit artikel.

## <a name="add"></a>IP-adressen tooa VM toevoegen

U kunt persoonlijke en openbare IP-adressen tooa NIC toevoegen via Hallo stappen volgen. Hallo voorbeelden in de volgende secties Hallo wordt ervan uitgegaan dat er al een virtuele machine met Hallo drie IP-configuraties beschreven in Hallo [scenario](#Scenario) in dit artikel, maar het is niet vereist dat u doen.

### <a name="coreadd"></a>Core stappen

1. Blader toohello Azure-portal op https://portal.azure.com en meld u in de App, indien nodig.
2. Klik in de portal Hallo op **meer services** > type *virtuele machines* in het filtervak Hallo en klik vervolgens op **virtuele machines**.
3. In Hallo **virtuele machines** blade, klikt u op Hallo VM die u wilt dat tooadd IP-adressen aan. Klik op **netwerkinterfaces** op Hallo virtuele machineblade die wordt weergegeven en selecteer vervolgens Hallo netwerk interface die u wilt dat tooadd Hallo IP-adressen aan. In voorbeeld Hallo in Hallo volgende afbeelding, Hallo NIC met de naam *myNIC* van Hallo VM met de naam *myVM* is ingeschakeld:

    ![Netwerkinterface](./media/virtual-network-multiple-ip-addresses-portal/figure1.png)

4. Hallo blade die wordt weergegeven voor Hallo NIC die u hebt geselecteerd, klikt u op **IP-configuraties**.

Volledige Hallo stappen in een van Hallo secties die volgen, op basis van Hallo type IP-adres wilt u tooadd.

### <a name="add-a-private-ip-address"></a>**Een persoonlijke IP-adres toevoegen**

Voer Hallo tooadd stappen een nieuwe persoonlijke IP-adres te volgen:

1. Volledige Hallo stappen voor het Hallo [Core stappen](#coreadd) sectie van dit artikel.
2. Klik op **Add**. In Hallo **toevoegen IP-configuratie** blade die wordt weergegeven, maak een IP-configuratie met de naam *IPConfig 4* met *10.0.0.7* als een *statische* privé-IP adres en klik vervolgens op **OK**.

    > [!NOTE]
    > Wanneer u een statisch IP-adres toevoegt, moet u op Hallo subnet Hallo die NIC is verbonden met een ongebruikte en een geldig adres opgeven. Als u Hallo-adres niet beschikbaar is, Hallo portal een X voor Hallo IP-adres wordt weergegeven en moet u tooselect een ander.

3. Wanneer u op OK klikt, Hallo blade wordt gesloten en ziet u Hallo nieuwe IP-configuratie weergegeven. Klik op **OK** tooclose hello **toevoegen IP-configuratie** blade.
4. U kunt klikken op **toevoegen** tooadd extra IP-configuraties of sluit alle geopende blades toofinish toe te voegen IP-adressen.
5. Toevoegen Hallo privé-IP-adressen toohello VM besturingssysteem via Hallo stappen voor het besturingssysteem in Hallo [toevoegen IP-adressen tooa VM besturingssysteem](#os-config) sectie van dit artikel.

### <a name="add-a-public-ip-address"></a>Een openbaar IP-adres toevoegen

Een openbaar IP-adres wordt toegevoegd door een openbare IP-adres resource tooeither koppelen van een nieuwe IP-configuratie of een bestaande IP-configuratie.

> [!NOTE]
> Openbare IP-adressen hebben een nominaal kosten. meer over IP-prijzen toolearn lezen Hallo [IP-adres prijzen](https://azure.microsoft.com/pricing/details/ip-addresses) pagina. Er is een limiet toohello aantal openbare IP-adressen die kunnen worden gebruikt in een abonnement. meer informatie over het Hallo-limieten, Hallo lezen toolearn [Azure beperkt](../azure-subscription-service-limits.md#networking-limits) artikel.
> 

### <a name="create-public-ip"></a>Een openbare IP-adres-resource maken

Een openbaar IP-adres is een instelling voor de bron van een openbare IP-adres. Als u hebt een openbare IP-adres resource die geen momenteel gekoppeld tooan IP-configuratie die u wilt tooassociate tooan IP-configuratie overslaan Hallo stappen te volgen en Hallo stappen uitvoeren in een van Hallo secties die volgen, die u nodig hebt. Als u een beschikbare resource voor openbare IP-adres niet hebt, voert u Hallo stappen toocreate een volgende:

1. Blader toohello Azure-portal op https://portal.azure.com en meld u in de App, indien nodig.
3. Klik in de portal Hallo op **nieuw** > **Networking** > **openbaar IP-adres**.
4. In Hallo **openbare IP-adres maken** blade die wordt weergegeven, voer een **naam**, selecteer een **IP-adrestoewijzing** type, een **abonnement**, een **Resourcegroep**, en een **locatie**, klikt u vervolgens op **maken**, zoals weergegeven in de volgende afbeelding Hallo:

    ![Een openbare IP-adres-resource maken](./media/virtual-network-multiple-ip-addresses-portal/figure5.png)

5. Volledige Hallo stappen in een van de Hallo secties tooassociate Hallo openbare IP-resource tooan IP-adresconfiguratie.

#### <a name="associate-hello-public-ip-address-resource-tooa-new-ip-configuration"></a>Hallo openbare IP-resource tooa nieuwe IP-adresconfiguratie koppelen

1. Volledige Hallo stappen voor het Hallo [Core stappen](#coreadd) sectie van dit artikel.
2. Klik op **Add**. In Hallo **toevoegen IP-configuratie** blade die wordt weergegeven, maak een IP-configuratie met de naam *IPConfig 4*. Hallo inschakelen **openbaar IP-adres** en selecteert u een bestaande, beschikbare openbare IP-adres resource in Hallo **openbare IP-adres kiezen** blade die wordt weergegeven.

    Nadat u Hallo openbare IP-adres resource hebt geselecteerd, klikt u op **OK** en Hallo blade wordt gesloten. Als u een bestaand openbaar IP-adres niet hebt, kunt u een door de stappen in Hallo Hallo [maken van een openbare IP-adres resource](#create-public-ip) sectie van dit artikel. 

3. Bekijk Hallo nieuwe IP-configuratie. Hoewel een particulier IP-adres is niet expliciet toegewezen, is een automatisch toohello IP-configuratie, toegewezen, omdat alle IP-configuraties moeten een particulier IP-adres hebben.
4. U kunt klikken op **toevoegen** tooadd extra IP-configuraties of sluit alle geopende blades toofinish toe te voegen IP-adressen.
5. Hallo persoonlijke IP-adres toohello VM besturingssysteem toevoegen via Hallo stappen voor het besturingssysteem in Hallo [toevoegen IP-adressen tooa VM besturingssysteem](#os-config) sectie van dit artikel. Voeg geen Hallo openbare IP-adres toohello besturingssysteem.

#### <a name="associate-hello-public-ip-address-resource-tooan-existing-ip-configuration"></a>Hallo openbare IP-resource tooan bestaande IP-adresconfiguratie koppelen

1. Volledige Hallo stappen voor het Hallo [Core stappen](#coreadd) sectie van dit artikel.
2. Klik op Hallo IP-configuratie die u tooadd Hallo openbare IP-adresbron wilt.
3. Hallo IPConfig blade die wordt weergegeven, klikt u op **IP-adres**.
4. In Hallo **openbare IP-adres kiezen** blade die wordt weergegeven, selecteert u een openbaar IP-adres.
5. Klik op **opslaan** en Hallo blades worden gesloten. Als u een bestaand openbaar IP-adres niet hebt, kunt u een door de stappen in Hallo Hallo [maken van een openbare IP-adres resource](#create-public-ip) sectie van dit artikel.
3. Bekijk Hallo nieuwe IP-configuratie.
4. U kunt klikken op **toevoegen** tooadd extra IP-configuraties of sluit alle geopende blades toofinish toe te voegen IP-adressen. Voeg geen Hallo openbare IP-adres toohello besturingssysteem.


[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
