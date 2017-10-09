---
title: "aaaConfigure privé IP-adressen voor virtuele machines - Azure-portal | Microsoft Docs"
description: "Meer informatie over hoe tooconfigure privé IP-adressen voor virtuele machines met hello Azure-portal."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 11245645-357d-4358-9a14-dd78e367b494
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 474161303cdf8cb98e16ffd7cef6b74debdbc49a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-portal"></a>Privé IP-adressen voor een virtuele machine met behulp van hello Azure-portal configureren

> [!div class="op_single_selector"]
> * [Azure Portal](virtual-networks-static-private-ip-arm-pportal.md)
> * [PowerShell](virtual-networks-static-private-ip-arm-ps.md)
> * [Azure-CLI](virtual-networks-static-private-ip-arm-cli.md)
> * [Azure-portal (klassiek)](virtual-networks-static-private-ip-classic-pportal.md)
> * [PowerShell (klassiek)](virtual-networks-static-private-ip-classic-ps.md)
> * [Azure CLI (klassiek)](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel. U kunt ook [statisch privé IP-adres in het klassieke implementatiemodel Hallo beheren](virtual-networks-static-private-ip-classic-pportal.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

Hallo voorbeeld volgt verwacht een eenvoudige omgeving al gemaakt. Als u toorun Hallo stappen wilt zoals ze worden weergegeven in dit document, eerst bouwen Hallo testomgeving beschreven in [een vnet maken](virtual-networks-create-vnet-arm-pportal.md).

## <a name="how-toocreate-a-vm-for-testing-static-private-ip-addresses"></a>Hoe toocreate een virtuele machine voor het testen van statische privé-IP-adressen
U kunt een statisch privé IP-adres niet instellen tijdens het maken van een virtuele machine in de modus voor Resource Manager deployment Hallo Hallo via hello Azure-portal. U moet eerst Hallo VM maken, tehn stelt de privé IP-toobe statische.

een virtuele machine met de naam toocreate *DNS01* in Hallo *FrontEnd* subnet van een VNet met de naam *TestVNet*, volgt u onderstaande stappen voor Hallo.

1. Navigeer via een browser toohttp://portal.azure.com en, indien nodig, meld u aan met uw Azure-account.
2. Klik op **nieuw** > **Compute** > **Windows Server 2012 R2 Datacenter**, zoals u ziet dat Hallo **een implementatiemodelselecteren** lijst al staat **Resource Manager**, en klik vervolgens op **maken**, zoals in onderstaande afbeelding ziet Hallo.
   
    ![Virtuele machine maken in Azure-portal](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. In Hallo **basisbeginselen** blade Voer Hallo-naam van Hallo VM toobe gemaakt (*DNS01* in ons scenario), Hallo lokale administrator-account en wachtwoord, zoals weergegeven in onderstaande afbeelding ziet Hallo.
   
    ![Blade Grondbeginselen](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. Zorg ervoor dat Hallo **locatie** geselecteerd is *VS-midden*, klikt u vervolgens op **Selecteer een bestaande** onder **resourcegroep**, klikt u vervolgens op **Resourcegroep** opnieuw in en klik vervolgens op *TestRG*, en klik vervolgens op **OK**.
   
    ![Blade Grondbeginselen](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. In Hallo **een grootte kiezen** blade Selecteer **A1 standaard**, en klik vervolgens op **Selecteer**.
   
    ![Kies een blade grootte](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. In de **instellingen** blade, zorg ervoor dat Hallo volgende eigenschappen worden ingesteld met de onderstaande Hallo-waarden zijn ingesteld en klik vervolgens op **OK**.
   
    -**Storage-account**: *vnetstorage*
   
   * **Netwerk**: *TestVNet*
   * **Subnet**: *FrontEnd*
     
     ![Kies een blade grootte](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. In Hallo **samenvatting** blade, klikt u op **OK**. Kennisgeving Hallo tegel hieronder weergegeven in het dashboard.
   
    ![Virtuele machine maken in Azure-portal](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Hoe de gegevens voor een VM voor het adres van tooretrieve statische privé-IP
tooview Hallo statisch privé IP-adresgegevens voor Hallo VM gemaakt met de bovenstaande stappen voor Hallo Hallo onderstaande stappen uitvoeren.

1. Vanuit hello Azure Azure portal, klikt u op **door alles bladeren** > **virtuele machines** > **DNS01** > **alle instellingen** > **netwerkinterfaces** en klik vervolgens op Hallo alleen netwerkinterface vermeld.
   
    ![VM-tegel implementeren](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. In Hallo **netwerkinterface** blade, klikt u op **alle instellingen** > **IP-adressen** en kennisgeving Hallo **toewijzing** en **IP-adres** waarden.
   
    ![VM-tegel implementeren](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>Hoe tooadd een statische privé-IP adres tooan bestaande VM
een statisch privé IP-adres toohello VM gemaakt met behulp van Hallo de bovenstaande stappen tooadd Hallo volgende stappen:

1. Van Hallo **IP-adressen** blade hierboven, klikt u op **statische** onder **toewijzing**.
2. Type *192.168.1.101* voor **IP-adres**, en klik vervolgens op **opslaan**.
   
    ![Virtuele machine maken in Azure-portal](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> Als na het klikken op **opslaan** merkt u Hallo toewijzing nog steeds te ingesteld**dynamische**, betekent dit Hallo opgegeven IP-adres is al in gebruik. Probeer een ander IP-adres.
> 
> 

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Hoe tooremove een statisch privé IP-adres van een virtuele machine
tooremove Hallo statisch privé IP-adres van VM gemaakt, Hallo Hallo stap voltooien:

Van Hallo **IP-adressen** blade hierboven, klikt u op **dynamische** onder **toewijzing**, en klik vervolgens op **opslaan**.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [gereserveerde openbare IP-adres](virtual-networks-reserved-public-ip.md) adressen.
* Meer informatie over [instantieniveau openbare IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adressen.
* Raadpleeg Hallo [gereserveerde IP-REST-API's](https://msdn.microsoft.com/library/azure/dn722420.aspx).

