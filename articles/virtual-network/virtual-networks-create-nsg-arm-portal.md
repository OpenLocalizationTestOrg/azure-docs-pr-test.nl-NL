---
title: aaaManage-netwerkbeveiligingsgroepen - Azure-portal | Microsoft Docs
description: Meer informatie over hoe toomanage netwerkbeveiligingsgroepen met hello Azure-portal.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: faee5ac8-f4c4-4f97-ade5-197a37aad496
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 53fb29e60cbc2a535f6cf03e430d9e703e97b216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-portal"></a>Netwerkbeveiligingsgroepen met hello Azure-portal beheren

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel. U kunt ook [nsg's maken in het klassieke implementatiemodel Hallo](virtual-networks-create-nsg-classic-ps.md).

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

Hallo voorbeeld PowerShell onderstaande opdrachten verwacht een eenvoudige omgeving al gemaakt dat is gebaseerd op Hallo bovenstaande scenario. Als u toorun Hallo opdrachten wilt zoals ze worden weergegeven in dit document, moet u eerst Hallo testomgeving verder door de implementatie [deze sjabloon](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), klikt u op **tooAzure implementeren**, standaardparameterwaarden Hallo vervangen indien nodig, en volg de instructies in Hallo in Hallo portal. Hallo stappen hieronder gebruik **RG NSG** zoals Hallo-naam van Hallo resource groep Hallo-sjabloon is geïmplementeerd.

## <a name="create-hello-nsg-frontend-nsg"></a>Hallo NSG-FrontEnd NSG maken
Hallo toocreate **NSG-FrontEnd** NSG zoals weergegeven in de bovenstaande Hallo-scenario Hallo volgende stappen.

1. Navigeer via een browser toohttp://portal.azure.com en, indien nodig, meld u aan met uw Azure-account.
2. Klik op **Bladeren >** > **Netwerkbeveiligingsgroepen**.
   
    ![Azure portal - nsg 's](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. In Hallo **Netwerkbeveiligingsgroepen** blade, klikt u op **toevoegen**.
   
    ![Azure portal - nsg 's](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. In Hallo **netwerkbeveiligingsgroep maken** blade maken van een NSG met de naam *NSG-FrontEnd* in Hallo *RG NSG* resourcegroep en klik vervolgens op **maken**.
   
    ![Azure portal - nsg 's](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a>Regels maken in een bestaande NSG
toocreate regels in een bestaande NSG van hello Azure-portal stappen Hallo volgende.

1. Klik op **Bladeren >** > **Netwerkbeveiligingsgroepen**.
2. Klik in de lijst Hallo van nsg's, op **NSG-FrontEnd** > **beveiligingsregels voor binnenkomende verbindingen**
   
    ![Azure portal - NSG-FrontEnd](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. In de lijst met Hallo **inkomende beveiligingsregels**, klikt u op **toevoegen**.
   
    ![Azure-portal - regel toevoegen](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. In Hallo **de inkomende beveiligingsregel toevoegen** blade maken van een regel met naam *web regel* met de prioriteit van *200* toegang via *TCP* tooport *80* tooany VM vanaf elke bron en klik vervolgens op **OK**. U ziet dat de meeste van deze instellingen standaardwaarden al.
   
    ![Azure portal - instellingen van de regel](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. Na enkele seconden worden er nieuwe regel in het NSG Hallo Hallo.
   
    ![Azure portal - nieuwe regel](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. Herhaal stap too6 toocreate een inkomende regel met de naam *rdp-regel* met een prioriteit van *250* toegang via *TCP* tooport *3389* tooany VM van een andere bron.

## <a name="associate-hello-nsg-toohello-frontend-subnet"></a>Hallo NSG toohello FrontEnd subnet koppelen
1. Klik op **Bladeren >** > **resourcegroepen** > **RG NSG**.
2. In Hallo **RG NSG** blade, klikt u op **...**   >  **TestVNet**.
   
    ![Azure portal - TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. In Hallo **instellingen** blade, klikt u op **subnetten** > **FrontEnd** > **netwerkbeveiligingsgroep**  >  **NSG-FrontEnd**.
   
    ![Azure portal - subnetinstellingen](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. In Hallo **FrontEnd** blade, klikt u op **opslaan**.
   
    ![Azure portal - subnetinstellingen](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-hello-nsg-backend-nsg"></a>Hallo NSG-back-end NSG maken
Hallo toocreate **NSG-back-end** NSG en koppelt u deze toohello **back-end** subnet, Hallo stappen hieronder.

1. Hallo Herhaal de stappen in [maken Hallo NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) toocreate een NSG met de naam *NSG-back-end*
2. Hallo Herhaal de stappen in [regels maken in een bestaande NSG](#Create-rules-in-an-existing-NSG) toocreate hello **inkomende** regels in Hallo onderstaande tabel.
   
   | Regel voor binnenkomende verbindingen | Uitgaande regel |
   | --- | --- |
   | ![Azure portal - regel voor binnenkomende verbindingen](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Azure portal - uitgaande regel](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. Hallo Herhaal de stappen in [hello NSG toohello FrontEnd subnet koppelen](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate hello **NSG-back-end** NSG toohello **back-end** subnet.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[bestaande nsg's beheren](virtual-network-manage-nsg-arm-portal.md)
* [Logboekregistratie inschakelen](virtual-network-nsg-manage-log.md) voor nsg's.

