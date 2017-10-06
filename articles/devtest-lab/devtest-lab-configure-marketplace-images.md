---
title: instellingen voor de aaaConfigure Azure Marketplace-installatiekopie in Azure DevTest Labs | Microsoft Docs
description: "Configureren welke Azure Marketplace-installatiekopieën kunnen worden gebruikt bij het maken van een virtuele machine in Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 804c6af2-17e9-4320-af3a-f454bd398379
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: bb4b7f1c0cbe967bee724f7ee20f64f8c4ea58ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a>Configureren van instellingen voor Azure Marketplace-installatiekopie in Azure DevTest Labs
DevTest Labs ondersteunt maken virtuele machines op basis van Azure Marketplace-installatiekopieën, afhankelijk van hoe u Azure Marketplace-installatiekopieën toobe gebruikt in uw lab hebt geconfigureerd. Dit artikel ziet u hoe toospecify die, indien aanwezig, Azure Marketplace-installatiekopieën kunnen worden gebruikt bij het maken van virtuele machines in een testomgeving. Dit zorgt ervoor dat uw team alleen toegang toohello Marketplace-installatiekopieën die ze nodig heeft. 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a>Selecteer welke Azure Marketplace-installatiekopieën zijn toegestaan bij het maken van een virtuele machine
1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.
3. Selecteer de gewenste lab Hallo in lijst Hallo van labs. 
4. Selecteer op Hallo van labblade, **configuratie en het beleid**.
5. Op het lab **configuratie en het beleid** blade onder **basissen voor virtuele Machine**, selecteer **Marketplace-installatiekopieën**.
6. Geef op of u wilt dat alle Hallo gekwalificeerde Azure Marketplace-installatiekopieën toobe beschikbaar voor gebruik als basis van een nieuwe virtuele machine. Als u selecteert **Ja**, klikt u vervolgens alle hello Azure Marketplace-installatiekopieën die voldoen aan alle volgende criteria Hallo zijn toegestaan in Hallo lab:
   
   * Hallo-installatiekopie wordt gemaakt van één VM **en**
   * Hallo installatiekopie maakt gebruik van Azure Resource Manager tooprovision virtuele machines, **en**
   * Hallo installatiekopie vereist geen extra licentieabonnement aanschaffen
     
    Als u geen afbeeldingen toobe toegestaan wilt, of u wilt dat toospecify welke afbeeldingen kunnen worden gebruikt, selecteert u **Nee**.
     
     ![Optie tooallow alle Marketplace-installatiekopieën toobe gebruikt als basis installatiekopieën voor virtuele machines](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. Als u selecteert **Nee** toohello vorige stap, hello **toegestane installatiekopieën/Selecteer alle** selectievakje is ingeschakeld. 
   U kunt gebruik deze optie samen met de Hallo zoeken vak tooquickly selecteren of selectie van alle Hallo items weergegeven in de lijst Hallo opheffen.
   * Selecteer hello Azure Marketplace-installatiekopieën gewenste tooallow voor het maken van de virtuele machine afzonderlijk door het bijbehorende selectievakje van elke installatiekopie.
   * Selecteer niets uit de lijst Hallo als u niet tooallow alle Azure Marketplace-installatiekopieën toobe gebruikt in Hallo lab wilt.
   
    ![U kunt opgeven welke Azure Marketplace-installatiekopieën kunnen worden gebruikt als basis van installatiekopieën voor virtuele machines](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Volgende stappen
Wanneer u de manier waarop Azure Marketplace-installatiekopieën zijn toegestaan bij het maken van een virtuele machine hebt geconfigureerd, Hallo volgende stap is te[toevoegen van een VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).

