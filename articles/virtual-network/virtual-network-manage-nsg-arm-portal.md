---
title: aaaManage nsg's met behulp van hello Azure-portal | Microsoft Docs
description: Meer informatie over hoe toomanage bestaande hello Azure-portal met nsg's.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5d55679d-57da-457c-97dc-1e1973909ee5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.openlocfilehash: ad9a4060bd81bae4597ad5a4f59622e10cd214cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-nsgs-using-hello-portal"></a>Nsg's met Hallo portal beheren

> [!div class="op_single_selector"]
> * [Portal](virtual-network-manage-nsg-arm-portal.md)
> * [PowerShell](virtual-network-manage-nsg-arm-ps.md)
> * [Azure-CLI](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md). In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van het klassieke implementatiemodel hello aanbeveelt gebruiken.
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a>Informatie ophalen
U kunt uw bestaande nsg's weergeven, regels voor een bestaande NSG ophalen en weten welke resources een NSG is gekoppeld aan.

### <a name="view-existing-nsgs"></a>Bestaande nsg's weergeven

tooview alle bestaande nsg's in een abonnement, volledige Hallo stappen te volgen:

1. Navigeer via een browser toohttp://portal.azure.com en, indien nodig, meld u aan met uw Azure-account.

2. Klik op **Bladeren >** > **Netwerkbeveiligingsgroepen**.

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. Controleer Hallo lijst met nsg's in Hallo **Netwerkbeveiligingsgroepen** blade.

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a>Nsg's weergeven in een resourcegroep

tooview hello lijst met nsg's in Hallo **RG NSG** resourcegroep, volledige Hallo stappen te volgen:

1. Klik op **resourcegroepen >** > **RG NSG** > **...** .

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. In de lijst met resources Hallo zoeken naar objecten Hallo NSG pictogram weergegeven zoals in Hallo **Resources** blade hieronder.

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a>Lijst met alle regels voor een NSG

tooview hello regels van een NSG met de naam **NSG-FrontEnd**, volledige Hallo volgende stappen:

1. Van Hallo **Netwerkbeveiligingsgroepen** blade of Hallo **Resources** blade hierboven, klikt u op **NSG-FrontEnd**.

2. In Hallo **instellingen** tabblad **inkomende beveiligingsregels**.

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. Hallo **inkomende beveiligingsregels** blade wordt weergegeven zoals hieronder wordt weergegeven.

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. In Hallo **instellingen** tabblad **uitgaande beveiligingsregels** toosee Hallo uitgaande regels.

    > [!NOTE]
    > Standaardregels tooview, klikt u op Hallo **regels standaard** pictogram Hallo boven aan het Hallo-blade waarmee de Hallo regels worden weergegeven.
    >

### <a name="view-nsgs-associations"></a>Nsg's koppelingen weergeven

tooview welke resources Hallo **NSG-FrontEnd** NSG is met, volledige Hallo stappen te volgen:

1. Van Hallo **Netwerkbeveiligingsgroepen** blade of Hallo **Resources** blade hierboven, klikt u op **NSG-FrontEnd**.

2. In Hallo **instellingen** tabblad **subnetten** tooview welke subnetten zijn toohello NSG die is gekoppeld.

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. In Hallo **instellingen** tabblad **netwerkinterfaces** tooview wat NIC's gekoppeld zijn toohello NSG.

## <a name="manage-rules"></a>Regels beheren
U kunt regels tooan bestaande NSG toevoegen, bestaande regels bewerken en regels te verwijderen.

### <a name="add-a-rule"></a>Een regel toevoegen
tooadd een regel waarmee **inkomende** verkeer tooport **443** van een machine toohello **NSG-FrontEnd** NSG, volledige Hallo stappen te volgen:

1. Van Hallo **Netwerkbeveiligingsgroepen** blade of Hallo **Resources** blade hierboven, klikt u op **NSG-FrontEnd**.
2. In Hallo **instellingen** tabblad **inkomende beveiligingsregels**.
3. In Hallo **inkomende beveiligingsregels** blade, klikt u op **toevoegen**. Klik op Hallo **de inkomende beveiligingsregel toevoegen** blade Hallo waarden doorvoeren, zoals hieronder wordt weergegeven en klik vervolgens op **OK**.

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    Let na enkele seconden op nieuwe regel in Hallo Hallo **inkomende beveiligingsregels** blade.

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a>Een regel wijzigen
toochange hello regel bovenstaande tooallow binnenkomend verkeer van Hallo **Internet** alleen en volledige Hallo stappen te volgen:

1. Van Hallo **Netwerkbeveiligingsgroepen** blade of Hallo **Resources** blade hierboven, klikt u op **NSG-FrontEnd**.
2. In Hallo **instellingen** en klik op Hallo regel die eerder is gemaakt.
3. In Hallo **toestaan https** blade, wijziging Hallo **bron** eigenschap zoals hieronder wordt weergegeven en klik vervolgens op **opslaan**.

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a>Een regel verwijderen

toodelete hello regel hierboven gemaakte, volledige Hallo stappen te volgen:

1. Van Hallo **Netwerkbeveiligingsgroepen** blade of Hallo **Resources** blade hierboven, klikt u op **NSG-FrontEnd**.
2. In Hallo **instellingen** en klik op Hallo regel die eerder is gemaakt.
3. In Hallo **toestaan https** blade, klikt u op **verwijderen**, en klik vervolgens op **Ja**.

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a>Koppelingen beheren
U kunt een NSG toosubnets en NIC's kunt koppelen. U kunt ook een NSG van elke bron die deze gekoppeld ontkoppelen.

### <a name="associate-an-nsg-tooa-nic"></a>Een NSG tooa NIC koppelen
Hallo tooassociate **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, volledige Hallo stappen te volgen:

1. Van Hallo **Netwerkbeveiligingsgroepen** blade of Hallo **Resources** blade hierboven, klikt u op **NSG-FrontEnd**.
2. In Hallo **instellingen** tabblad **netwerkinterfaces** > **koppelen** > **TestNICWeb1**.

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a>Een NSG van een NIC ontkoppelen

Hallo toodissociate **NSG-FrontEnd** NSG van Hallo **TestNICWeb1** NIC, volledige Hallo stappen te volgen:

1. Hallo Azure-portal, klik op **resourcegroepen >** > **RG NSG** > **...**   >  **TestNICWeb1**.

2. In Hallo **TestNICWeb1** blade, klikt u op **beveiliging wijzigen...**   >  **Geen**.

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> U kunt ook deze blade tooassociate Hallo NIC tooany bestaande NSG gebruiken.
>

### <a name="dissociate-an-nsg-from-a-subnet"></a>Een NSG van een subnet ontkoppelen

Hallo toodissociate **NSG-FrontEnd** NSG van Hallo **FrontEnd** subnet, volledige Hallo stappen te volgen:

1. Hallo Azure-portal, klik op **resourcegroepen >** > **RG NSG** > **...**   >  **TestVNet**.

2. In Hallo **instellingen** blade, klikt u op **subnetten** > **FrontEnd** > **netwerkbeveiligingsgroep**  >  **Geen**.

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. In Hallo **FrontEnd** blade, klikt u op **opslaan**.

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-tooa-subnet"></a>Een NSG tooa subnet koppelen

Hallo tooassociate **NSG-FrontEnd** NSG toohello **FronEnd** opnieuw subnet, volledige Hallo stappen te volgen:

1. Hallo Azure-portal, klik op **resourcegroepen >** > **RG NSG** > **...**   >  **TestVNet**.
2. In Hallo **instellingen** blade, klikt u op **subnetten** > **FrontEnd** > **netwerkbeveiligingsgroep**  >  **NSG-FrontEnd**.
3. In Hallo **FrontEnd** blade, klikt u op **opslaan**.

> [!NOTE]
> U kunt ook een subnet van de NSG tooa uit thh NSG van koppelen **instellingen** blade.
>

## <a name="delete-an-nsg"></a>Een NSG verwijderen
U kunt een NSG alleen verwijderen als het tooany resource niet is gekoppeld. toodelete een NSG, volledige Hallo volgende stappen uit:.

1. Hallo Azure-portal, klik op **resourcegroepen >** > **RG NSG** > **...**   >  **NSG-FrontEnd**.
2. In Hallo **instellingen** blade, klikt u op **netwerkinterfaces**.
3. Als er NIC's die worden vermeld, klikt u op Hallo NIC en volgt u stap 2 in [ontkoppelen van een NSG van een NIC](#Dissociate-an-NSG-from-a-NIC).
4. Herhaal stap 3 voor elke NIC.
5. In Hallo **instellingen** blade, klikt u op **subnetten**.
6. Als er subnetten die worden vermeld, klikt u op Hallo subnet en volg de stappen 2 en 3 in [een NSG van een subnet ontkoppelen](#Dissociate-an-NSG-from-a-subnet).
7. Toohello links schuift **NSG-FrontEnd** blade, klikt u vervolgens op **verwijderen** > **Ja**.

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a>Volgende stappen
* [Logboekregistratie inschakelen](virtual-network-nsg-manage-log.md) voor nsg's.
