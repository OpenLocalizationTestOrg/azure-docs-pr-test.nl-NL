---
title: aaaConfigure een virtueel netwerk in Azure DevTest Labs | Microsoft Docs
description: Meer informatie over hoe tooconfigure een bestaand virtueel netwerk en subnet, en deze gebruiken in een virtuele machine met Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 6cda99c2-b87e-4047-90a0-5df10d8e9e14
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: a11ce8315e3c540e44aeacc9c5ee3dde014d4621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a>Een virtueel netwerk configureren in Azure DevTest Labs
Zoals wordt beschreven in artikel Hallo [toevoegen van een VM met artefacten tooa lab](devtest-lab-add-vm-with-artifacts.md), wanneer u een virtuele machine in een testomgeving maken kunt u een geconfigureerde virtueel netwerk. Een scenario om dit te doen is als u tooaccess moet uw corpnet-bronnen van uw virtuele machines met virtuele netwerk dat is geconfigureerd met ExpressRoute of site-naar-site VPN Hallo. Hallo volgende secties laten zien hoe tooadd uw bestaande virtuele netwerk in een testomgeving virtuele-netwerkinstellingen zodat deze beschikbaar toochoose bij het maken van virtuele machines.

## <a name="configure-a-virtual-network-for-a-lab-using-hello-azure-portal"></a>Een virtueel netwerk voor een testomgeving met hello Azure-portal configureren
Hallo volgende stappen maakt u een bestaande virtuele netwerk (en subnet) tooa testomgeving toe te voegen zodat deze kan worden gebruikt bij het maken van een virtuele machine in Hallo dezelfde lab. 

1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.
3. Selecteer de gewenste lab Hallo in lijst Hallo van labs. 
4. Selecteer op Hallo van labblade, **configuratie**.
5. Op de Hallo lab **configuratie** blade Selecteer **virtuele netwerken**.
6. Op Hallo **virtuele netwerken** blade ziet u een lijst met virtuele netwerken die zijn geconfigureerd voor het huidige lab hello, evenals Hallo standaard virtueel netwerk dat is gemaakt voor uw testomgeving. 
7. Selecteer **+ toevoegen**.
   
    ![Een bestaand virtueel netwerk tooyour lab toevoegen](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. Op Hallo **virtueel netwerk** blade Selecteer **[Selecteer virtueel netwerk]**.
   
    ![Selecteer een bestaand virtueel netwerk](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. Op Hallo **virtueel netwerk kiezen** blade, selecteer Hallo gewenste virtueel netwerk. Hallo blade ziet u alle Hallo virtuele netwerken die zijn onder Hallo dezelfde regio in Hallo-abonnement als Hallo lab.  
10. Na het selecteren van een virtueel netwerk, keert u terug toohello **virtueel netwerk** klikt u op Hallo subnet in de lijst Hallo HALLO hallo blade onderaan in.

    ![Subnetlijst met](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    Hallo Lab Subnet blade wordt weergegeven.

    ![Subnet labblade](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. Geef een **labsubnetnaam**.
12. tooallow een subnet toobe gebruikt in een lab maken van de VM, selecteer **gebruik bij het maken van de virtuele machine**.
13. tooenable een [openbaar IP-adres gedeeld](devtest-lab-shared-ip.md), selecteer **Schakel gedeelde openbare IP-adres**.
14. Selecteer tooallow openbare IP-adressen in een subnet **openbare IP-maken toestaan**.
15. In Hallo **maximum aantal virtuele machines per gebruiker** veld Hallo maximum aantal virtuele machines per gebruiker voor elk subnet. Als u wilt dat een onbeperkt aantal virtuele machines, laat u dit veld leeg.
16. Selecteer **OK** tooclose Hallo Lab Subnet blade.
17. Selecteer **opslaan** tooclose Hallo virtuele netwerkblade.
18. Nu dat hello virtueel netwerk is geconfigureerd, kan worden geselecteerd bij het maken van een virtuele machine. 
    toosee hoe toocreate een virtuele machine en geef een virtueel netwerk, raadpleeg dan toohello artikel [toevoegen van een VM met artefacten tooa lab](devtest-lab-add-vm-with-artifacts.md). 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Volgende stappen
Nadat u hebt toegevoegd Hallo gewenst virtueel netwerk tooyour lab, Hallo volgende stap is te[toevoegen van een VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).

