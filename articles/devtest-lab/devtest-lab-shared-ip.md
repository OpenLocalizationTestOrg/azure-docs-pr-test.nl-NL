---
title: aaaUnderstand gedeelde IP-adressen in Azure DevTest Labs | Microsoft Docs
description: Meer informatie over hoe Azure DevTest Labs gebruikmaakt van gedeelde IP-adressen toominimize Hallo openbare IP-adressen vereist tooaccess uw lab virtuele machines.
services: devtest-lab
documentationcenter: na
author: camsoper
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: casoper
ms.openlocfilehash: 8756410117a9d550d567d372174bf1ea96703c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a>Gedeelde IP-adressen in Azure DevTest Labs begrijpen

Azure DevTest Labs kunt lab VMs share Hallo hetzelfde openbare IP-adres toominimize Hallo aantal openbare IP-adressen vereist tooaccess uw afzonderlijke lab virtuele machines.  Dit artikel wordt beschreven hoe gedeelde IP-adressen werk en hun bijbehorende configuratie-opties.

## <a name="shared-ip-setting"></a>Gedeelde IP-instelling

Wanneer u een testomgeving maakt, bevindt het zich in een subnet van een virtueel netwerk.  Dit subnet is standaard gemaakt met **Schakel gedeelde openbare IP-adres** instellen te*Ja*.  Deze configuratie maakt een openbaar IP-adres voor het hele subnet Hallo.  Zie voor meer informatie over het configureren van virtuele netwerken en subnetten [configureren van een virtueel netwerk in Azure DevTest Labs](devtest-lab-configure-vnet.md).

![Nieuw lab-subnet](media/devtest-lab-shared-ip/lab-subnet.png)

Voor bestaande labs, kunt u deze optie inschakelen door het selecteren van **configuratie en het beleid > virtuele netwerken**. Vervolgens selecteert u een virtueel netwerk in Hallo lijst en kies **inschakelen gedeelde openbare IP-adres** voor een geselecteerde subnet. U kunt deze optie in een testomgeving ook uitschakelen als u niet dat tooshare een openbaar IP-adres in het lab virtuele machines wilt.

Alle virtuele machines in dit lab standaard toousing gemaakt van een gedeelde IP-adres.  Bij het maken van VM hello, deze instelling kan worden waargenomen in Hallo **geavanceerde instellingen** blade onder **IP-adresconfiguratie**.

![Nieuwe virtuele machine](media/devtest-lab-shared-ip/new-vm.png)

- **Gedeelde:** alle virtuele machines die zijn gemaakt als **gedeelde** in één resourcegroep (RG) worden geplaatst. Een enkel IP-adres is toegewezen voor die RG en alle virtuele machines in Hallo RG dat IP-adres wordt gebruikt.
- **Openbaar:** elke VM die u maakt een eigen IP-adres heeft en in een eigen resourcegroep wordt gemaakt.
- **Persoonlijk:** elke VM die u maakt een particuliere IP-adres gebruikt. U zich niet kunnen tooconnect toothis VM rechtstreeks vanuit Hallo internet met extern bureaublad.

Wanneer een virtuele machine met gedeelde IP ingeschakeld wordt toegevoegd toohello subnet, DevTest Labs automatisch voegt van Hallo VM tooa load balancer toe en wijst een TCP-poortnummer op Hallo openbare IP-adres, doorsturen toohello RDP-poort op Hallo VM.  

## <a name="using-hello-shared-ip"></a>Met behulp van Hallo gedeeld IP

- **Linux-gebruikers:** SSH toohello VM via Hallo IP-adres of FQDN-naam, gevolgd door een dubbelepunt, gevolgd door Hallo-poort. In onderstaande Hallo afbeelding, bijvoorbeeld adres Hallo RDP tooconnect toohello VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.

  ![Voorbeeld van de virtuele machine](media/devtest-lab-shared-ip/vm-info.png)

- **Windows-gebruikers:** Selecteer Hallo **Connect** in Azure portal toodownload Hallo vooraf geconfigureerde RDP-bestand en toegang tot Hallo VM.

## <a name="next-steps"></a>Volgende stappen

* [Labbeleidsregels definiëren in Azure DevTest Labs](devtest-lab-set-lab-policy.md)
* [Een virtueel netwerk configureren in Azure DevTest Labs](devtest-lab-configure-vnet.md)





