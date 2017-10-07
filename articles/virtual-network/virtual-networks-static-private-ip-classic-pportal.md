---
title: "aaaConfigure privé IP-adressen voor virtuele machines (klassiek) - Azure-portal | Microsoft Docs"
description: "Meer informatie over hoe tooconfigure privé IP-adressen voor virtuele machines (klassiek) met hello Azure-portal."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b8ef8367-58b2-42df-9f26-3269980950b8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: df4bfa6768fc9e66db89785b633ffdb0274dbc46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-portal"></a>Privé IP-adressen voor een virtuele machine (klassiek) met behulp van hello Azure-portal configureren

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

In dit artikel bevat informatie over Hallo klassieke implementatiemodel. U kunt ook [een statisch privé IP-adres in Hallo Resource Manager-implementatiemodel beheren](virtual-networks-static-private-ip-arm-pportal.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

Hallo voorbeeld volgt verwacht een eenvoudige omgeving al gemaakt. Als u toorun Hallo stappen wilt zoals ze worden weergegeven in dit document, eerst bouwen Hallo testomgeving beschreven in [een vnet maken](virtual-networks-create-vnet-classic-pportal.md).

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>Hoe toospecify een statisch privé IP-adres bij het maken van een virtuele machine
een virtuele machine met de naam toocreate *DNS01* in Hallo *FrontEnd* subnet van een VNet met de naam *TestVNet* met een statisch privé IP-adres van *192.168.1.101*, Volg onderstaande stappen voor Hallo:

1. Navigeer via een browser toohttp://portal.azure.com en, indien nodig, meld u aan met uw Azure-account.
2. Klik op **nieuw** > **Compute** > **Windows Server 2012 R2 Datacenter**, zoals u ziet dat Hallo **een implementatiemodelselecteren** lijst al staat **klassieke**, en klik vervolgens op **maken**.
   
    ![Virtuele machine maken in Azure-portal](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. In Hallo **VM maken** blade Voer Hallo-naam van Hallo VM toobe gemaakt (*DNS01* in ons scenario), Hallo lokale administrator-account en wachtwoord.
   
    ![Virtuele machine maken in Azure-portal](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. Klik op **optionele configuratie** > **netwerk** > **virtueel netwerk**, en klik vervolgens op **TestVNet**. Als **TestVNet** is niet beschikbaar is, zorg ervoor dat u gebruikmaakt van Hallo *VS-midden* locatie en het Hallo-testomgeving beschreven op Hallo begin van dit artikel hebt gemaakt.
   
    ![Virtuele machine maken in Azure-portal](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. In Hallo **netwerk** blade, zorg ervoor dat Hallo subnet geselecteerde is *FrontEnd*, klikt u vervolgens op **IP-adressen**onder **IP-adrestoewijzing** klikt u op **statische**, en voer vervolgens *192.168.1.101* voor **IP-adres** zoals hieronder wordt weergegeven.
   
    ![Virtuele machine maken in Azure-portal](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. Klik op **OK** in Hallo **IP-adressen** blade, klikt u vervolgens op **OK** in Hallo **netwerk** blade en klik op **OK**in Hallo **optionele configuratie** blade.
7. In Hallo **VM maken** blade, klikt u op **maken**. Kennisgeving Hallo tegel hieronder weergegeven in het dashboard.
   
    ![Virtuele machine maken in Azure-portal](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Hoe de gegevens voor een VM voor het adres van tooretrieve statische privé-IP
tooview Hallo statisch privé IP-adresgegevens voor Hallo VM gemaakt met de bovenstaande stappen voor Hallo Hallo onderstaande stappen uitvoeren.

1. Vanuit hello Azure Azure portal, klikt u op **door alles bladeren** > **virtuele machines (klassiek)** > **DNS01**  >   **Alle instellingen** > **IP-adressen** en Let op Hallo van IP-adrestoewijzing en IP-adres, zoals hieronder wordt weergegeven.
   
    ![Virtuele machine maken in Azure-portal](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Hoe tooremove een statisch privé IP-adres van een virtuele machine
tooremove Hallo statisch privé IP-adres van VM gemaakt, Hallo Hallo volgende stappen.

1. Van Hallo **IP-adressen** blade hierboven, klikt u op **dynamische** toohello rechts van **IP-adrestoewijzing**, klikt u vervolgens op **opslaan**, en vervolgens Klik op **Ja**.
   
    ![Virtuele machine maken in Azure-portal](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>Hoe tooadd een statische privé-IP adres tooan bestaande VM
een statisch privé IP-adres toohello VM gemaakt met behulp van Hallo de bovenstaande stappen tooadd Hallo volgende stappen:

1. Van Hallo **IP-adressen** blade hierboven, klikt u op **statische** toohello rechts van **IP-adrestoewijzing**.
2. Type *192.168.1.101* voor **IP-adres**, klikt u vervolgens op **opslaan**, en klik vervolgens op **Ja**.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [gereserveerde openbare IP-adres](virtual-networks-reserved-public-ip.md) adressen.
* Meer informatie over [instantieniveau openbare IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adressen.
* Raadpleeg Hallo [gereserveerde IP-REST-API's](https://msdn.microsoft.com/library/azure/dn722420.aspx).

