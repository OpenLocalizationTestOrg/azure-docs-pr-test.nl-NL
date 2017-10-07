---
title: Azure-portal met behulp aaaOpen poorten tooa VM Hallo | Microsoft Docs
description: Meer informatie over hoe tooopen een poort / maken van een eindpunt tooyour virtuele machine van Windows hello resource manager-implementatiemodel met in hello Azure Portal
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: f7cf0319-5ee7-435e-8f94-c484bf5ee6f1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: aba789c65254651899aa688f256fe616c3d0126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-tooa-virtual-machine-with-hello-azure-portal"></a>Hoe tooopen poorten tooa virtuele machine met hello Azure-portal
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a>Snelle opdrachten
U kunt ook [u deze stappen uitvoert met Azure PowerShell](nsg-quickstart-powershell.md).

Maak eerst de Netwerkbeveiligingsgroep. Selecteer een resourcegroep in Hallo-portal, kiest u **toevoegen**, zoekt en selecteert u **netwerkbeveiligingsgroep**:

![Een Netwerkbeveiligingsgroep toevoegen](./media/nsg-quickstart-portal/add-nsg.png)

Voer een naam voor de beveiligingsgroep van uw netwerk, selecteert u of een resourcegroep maken en selecteer een locatie. Selecteer **maken** wanneer voltooid:

![Een Netwerkbeveiligingsgroep maken](./media/nsg-quickstart-portal/create-nsg.png)

Selecteer uw nieuwe Netwerkbeveiligingsgroep. Selecteer 'Inkomende beveiligingsregels' en vervolgens Hallo **toevoegen** knop toocreate een regel:

![Een inkomende regel toevoegen](./media/nsg-quickstart-portal/add-inbound-rule.png)

Kies een gemeenschappelijke **Service** uit de vervolgkeuzelijst hello, zoals *HTTP*. U kunt ook selecteren *aangepaste* tooprovide een specifieke poort toouse. Indien gewenst, Hallo prioriteit of de naam wijzigen. Hallo prioriteit is van invloed op Hallo volgorde waarin regels worden toegepast - Hallo lagere Hallo numerieke waarde, hello eerdere Hallo-regel wordt toegepast. U kunt ook selecteren **Geavanceerd** Hallo boven aan dit scherm tooenter een specifiek bereik van IP-blok of poort, bijvoorbeeld de gegevensbron. Wanneer u klaar bent, selecteert u **OK** toocreate Hallo regel:

![Een inkomende regel maken](./media/nsg-quickstart-portal/create-inbound-rule.png)

De laatste stap is tooassociate groepeert u de netwerkbeveiliging van uw met een subnet of een specifieke netwerkinterface. Laten we Hallo Netwerkbeveiligingsgroep aan een subnet koppelen. Selecteer **subnetten**, en kies vervolgens **koppelen**:

![Een Netwerkbeveiligingsgroep aan een subnet koppelen](./media/nsg-quickstart-portal/associate-subnet.png)

Selecteer het virtuele netwerk en selecteer vervolgens de juiste subnet Hallo:

![Koppelen van een Netwerkbeveiligingsgroep aan een virtueel netwerk](./media/nsg-quickstart-portal/select-vnet-subnet.png)

U hebt nu een Netwerkbeveiligingsgroep gemaakt van een inkomende regel staat toe dat verkeer op poort 80 en die aan een subnet is gekoppeld gemaakt. Alle virtuele machines verbinding van toothat subnet zijn op poort 80 bereikbaar.

## <a name="more-information-on-network-security-groups"></a>Meer informatie over Netwerkbeveiligingsgroepen
Hallo-hier snelle opdrachten kunt u tooget up en wordt uitgevoerd met verkeer stromende tooyour VM. Netwerkbeveiligingsgroepen bieden veel handige functies en verfijning voor het beheren van toegang tot tooyour bronnen. U kunt meer lezen over [hier maken van een Netwerkbeveiligingsgroep en ACL regels](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).

Voor maximaal beschikbare webtoepassingen, moet u uw virtuele machines achter een Load Balancer van Azure plaatsen. Hallo-taakverdeling verkeer tooVMs, met een Netwerkbeveiligingsgroep waarmee wordt verkeer gefilterd. Zie voor meer informatie [hoe tooload saldo Linux virtuele machines in Azure toocreate een maximaal beschikbare toepassing](tutorial-load-balancer.md).

## <a name="next-steps"></a>Volgende stappen
In dit voorbeeld moet u een eenvoudige regel tooallow HTTP-verkeer gemaakt. Hier vindt u informatie over het maken van meer gedetailleerde omgevingen in Hallo artikelen te volgen:

* [Overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [Wat is een netwerkbeveiligingsgroep (NSG)?](../../virtual-network/virtual-networks-nsg.md)