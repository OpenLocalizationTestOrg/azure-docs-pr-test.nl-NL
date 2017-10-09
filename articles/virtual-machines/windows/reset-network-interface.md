---
title: aaaHow tooreset netwerkinterface voor virtuele machine van Windows Azure | Microsoft Docs
description: Toont hoe tooreset netwerkinterface voor virtuele machine van Windows Azure
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: genli
ms.openlocfilehash: 1b653820927ef4c3bb8f384a7e752846a8be3da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-network-interface-for-azure-windows-vm"></a>Hoe tooreset netwerkinterface voor virtuele machine van Windows Azure 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

U kan geen verbinding maken tooMicrosoft Azure Windows virtuele Machine (VM) nadat u uitschakelen dat standaard Hallo Network Interface (NIC) of handmatig een statisch IP-adres ingesteld voor Hallo NIC. Dit artikel laat zien hoe tooreset netwerkinterface Hallo voor de virtuele Windows Azure, die Hallo verbinding met extern probleem wordt opgelost.

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a>Netwerkinterface opnieuw instellen

### <a name="for-classic-vms"></a>Voor klassieke virtuele machines

tooreset network interface, als volgt te werk:

1.  Ga toohello [Azure-portal]( https://ms.portal.azure.com).
2.  Selecteer **virtuele Machines (klassiek)**.
3.  Selecteer Hallo van invloed op een virtuele Machine.
4.  Selecteer **IP-adressen**.
5.  Als hello **particuliere IP-toewijzing** is niet **statische**, ook wijzigen**statische**.
6.  Wijziging Hallo **IP-adres** tooanother IP-adres dat beschikbaar is in Hallo Subnet.
7.  Schakel opslaan.
8.  Hallo virtuele machine wordt opnieuw opgestart tooinitialize Hallo nieuwe NIC toohello systeem.
9.  Probeer tooRDP tooyour machine. Als dit lukt, kunt u particuliere IP-adres back toohello oorspronkelijke Hallo kunt wijzigen als u wilt. Anders kunt u deze. 

### <a name="for-vms-deployed-in-resource-group-model"></a>Virtuele machines die worden geïmplementeerd in de groep resourcemodel

1.  Ga toohello [Azure-portal]( https://ms.portal.azure.com).
2.  Selecteer Hallo van invloed op een virtuele Machine.
3.  Selecteer **netwerkinterfaces**.
4.  Hallo netwerkinterface die is gekoppeld aan de computer selecteren
5.  Selecteer **IP-configuraties**.
6.  Selecteer Hallo IP-adres. 
7.  Als hello **particuliere IP-toewijzing** is niet **statische**, ook wijzigen**statische**.
8.  Wijziging Hallo **IP-adres** tooanother IP-adres dat beschikbaar is in Hallo Subnet.
9. Hallo virtuele machine wordt opnieuw opgestart tooinitialize Hallo nieuwe NIC toohello systeem.
10. Probeer tooRDP tooyour machine. Als dit lukt, kunt u particuliere IP-adres back toohello oorspronkelijke Hallo kunt wijzigen als u wilt. Anders kunt u deze. 

## <a name="delete-hello-unavailable-nics"></a>Verwijder Hallo niet beschikbaar NIC's
Nadat u extern bureaublad toohello machine kunt, moet u Hallo oude NIC's tooavoid Hallo potentieel probleem verwijderen:

1.  Open Apparaatbeheer.
2.  Selecteer **weergave** > **verborgen apparaten**.
3.  Selecteer **netwerkadapters**. 
4.  Controleer of er met de naam als 'Microsoft Hyper-V-netwerkadapter' Hallo-adapters.
5.  U ziet mogelijk een niet beschikbaar-adapter die is niet beschikbaar. Hallo-adapter met de rechtermuisknop en selecteer vervolgens verwijderen.

    ![Hallo-afbeelding van Hallo NIC](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > Verwijder alleen Hallo-niet beschikbaar-adapters die Hallo-naam 'Microsoft Hyper-V-netwerkadapter' hebben. Als u een van de Hallo andere verborgen adapters verwijdert, kan dit ertoe leiden dat andere problemen.
    >
    >

6.  Alle niet beschikbaar adapter moet nu uit van uw systeem worden gewist.