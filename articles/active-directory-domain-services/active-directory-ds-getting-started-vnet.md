---
title: 'Azure Active Directory Domain Services: een virtueel netwerk maken of selecteren | Microsoft Docs'
description: Azure Active Directory Domain Services met behulp van de klassieke Azure-portal Hallo inschakelen
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 13ab1608-e3d8-40de-9f7b-9b5b42199af4
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 212c741b20e846742d94f70342c4263ce8984153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a>Een virtueel netwerk voor Azure Active Directory Domain Services maken of selecteren
## <a name="before-you-begin"></a>Voordat u begint
Raadpleeg te[netwerken overwegingen voor Azure Active Directory Domain Services](active-directory-ds-networking.md).

## <a name="task-2-create-an-azure-virtual-network"></a>Taak 2: een virtueel netwerk van Azure maken
de volgende configuratietaak Hallo toocreate is een Azure-netwerk en een subnet binnen het. U schakelt Azure Active Directory Domain Services in dit subnet binnen uw virtuele netwerk in. Als u een bestaand virtueel netwerk dat u liever toouse hebt, kunt u deze stap overslaan.

> [!NOTE]
> Zorg ervoor dat Hallo virtuele Azure-netwerk u maakt of kies toouse met Azure Active Directory Domain Services behoort tooan Azure-regio die wordt ondersteund door Azure Active Directory Domain Services. tooascertain Hallo Azure-regio's waarin Azure Active Directory Domain Services beschikbaar is, Zie [Azure-services per regio](https://azure.microsoft.com/regions/#services/).
>
>Noteer de naam Hallo van Hallo virtueel netwerk tooensure dat u de juiste virtuele netwerk Hallo selecteert wanneer u Azure Active Directory Domain Services in een volgende configuratiestap inschakelen.


toocreate een Azure-netwerk waarin u wilt dat tooenable Azure Active Directory Domain Services, volgt u deze configuratie-instructies:

1. Ga toohello [klassieke Azure-portal](https://manage.windowsazure.com).
2. Selecteer in het linkerdeelvenster Hallo **netwerken**.

    ![Knooppunt Netwerken](./media/active-directory-domain-services-getting-started/networks-node.png)  
    Hallo **virtuele netwerken** venster wordt geopend.
3. Klik in het taakvenster Hallo HALLO hallo venster onderaan in op **nieuw**.

    ![Venster Virtuele netwerken](./media/active-directory-domain-services-getting-started/virtual-networks.png)
4. Klik op **Netwerkservices** en selecteer **Virtueel netwerk**.

    ![Virtueel netwerk - Snel maken](./media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. toocreate een virtueel netwerk, klikt u op **snelle invoer**.

6. Geef een **naam** voor uw virtuele netwerk en overweeg Hallo volgende manier:
    * U kunt tooconfigure **adresruimte** of **Maximum aantal VM's** voor dit netwerk.
    * U kunt laten Hallo **DNS-server** instellen als de **geen** nu. Nadat u Azure Active Directory Domain Services hebt ingeschakeld, kunt u de instelling Hallo bijwerken.
7. In Hallo **locatie** vervolgkeuzelijst, selecteert u een ondersteunde Azure-regio.  
    tooascertain Hallo Azure-regio's waarin Azure Active Directory Domain Services beschikbaar is, Zie [Azure-services per regio](https://azure.microsoft.com/regions/#services/).
8. toocreate uw virtuele netwerk, klikt u op **een virtueel netwerk maken**.

    ![Een virtueel netwerk voor Azure Active Directory Domain Services maken](./media/active-directory-domain-services-getting-started/create-vnet.png)
9. Nadat u een virtueel netwerk hebt gemaakt, selecteert u de naam van het virtuele netwerk Hallo Hallo en klik vervolgens op Hallo **configureren** tabblad.

    ![Een subnet maken](./media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. Onder **adresruimten voor virtueel netwerk**, klikt u op **subnet toevoegen**, en geef vervolgens een subnet met de naam van de Hallo **AaddsSubnet**.

    ![Een subnet voor Azure Active Directory Domain Services maken](./media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. toocreate Hallo subnet, klikt u op **opslaan**.


## <a name="next-step"></a>Volgende stap
[Taak 3: Azure Active Directory Domain Services inschakelen](active-directory-ds-getting-started-enableaadds.md)
