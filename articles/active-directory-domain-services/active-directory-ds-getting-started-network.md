---
title: 'Azure Active Directory Domain Services: Aan de slag | Microsoft Docs'
description: Azure Active Directory Domain Services met behulp van hello Azure-portal (Preview) inschakelen
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 7695dabb11df8d9dcfdac24996edf021af2e7f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Azure Active Directory Domain Services met behulp van hello Azure-portal (Preview) inschakelen


## <a name="before-you-begin"></a>Voordat u begint
Raadpleeg te[netwerken overwegingen voor Azure Active Directory Domain Services](active-directory-ds-networking.md).


## <a name="task-2-configure-network-settings"></a>Taak 2: netwerkinstellingen configureren
de volgende configuratietaak Hallo toocreate is een Azure-netwerk en een specifieke subnet in het. U schakelt Azure Active Directory Domain Services in dit subnet binnen uw virtuele netwerk in. U kunt ook kiezen een bestaand virtueel netwerk en subnet binnen het Hallo-specifieke maken.

1. Klik op **virtueel netwerk** tooselect een virtueel netwerk.
2. Op Hallo **virtueel netwerk kiezen** blade ziet u alle bestaande virtuele netwerken. U ziet alleen Hallo virtuele netwerken die deel uitmaken van de resourcegroep toohello en Azure-locatie die u hebt geselecteerd op Hallo **basisbeginselen** wizardpagina.

3. Kies Hallo virtuele netwerk waarin Azure AD Domain Services moeten worden ingeschakeld. Klik op **nieuw**, als u liever toocreate een nieuw virtueel netwerk. We raden met behulp van een toegewezen subnet voor Azure AD Domain Services. Als u een bestaand virtueel netwerk kiezen [Maak een toegewezen subnet met Hallo virtuele netwerken extensie](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) en selecteer vervolgens dat subnet. 

    ![Virtueel netwerk kiezen](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. Klik op **Subnet** toopick Hallo specifieke subnet in dit virtuele netwerk, in welke tooenable uw nieuwe beheerd domein. In Hallo **subnet maken** blade Geef een naam voor het Hallo-subnet en klik op **OK** wanneer u klaar bent. Bijvoorbeeld, een subnet maken met de naam van de Hallo DomainServices, zodat u gemakkelijk voor andere beheerders toounderstand wat binnen Hallo subnet is geïmplementeerd.

    ![Subnet binnen Hallo virtueel netwerk kiezen](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > **Richtlijnen voor het selecteren van een subnet**
  > 1. Gebruik een toegewezen subnet voor Azure AD Domain Services. Implementeer geen eventuele andere virtuele machines toothis-subnet. Deze configuratie kunt u tooconfigure netwerkbeveiligingsgroepen (nsg's) voor uw werkbelastingen/virtuele machines zonder te verstoren uw beheerde domein. Zie voor meer informatie [networking overwegingen voor Azure Active Directory Domain Services](active-directory-ds-networking.md).
  2. Selecteer Hallo gatewaysubnet voor het implementeren van Azure AD Domain Services niet omdat het is niet een ondersteunde configuratie.
  3. Zorg ervoor dat u hebt geselecteerd Hallo-subnet heeft voldoende beschikbare-adresruimte - ten minste 3-5 beschikbare IP-adressen.
  >

5. Wanneer u klaar bent, klikt u op **OK** toomove op toohello **beheerdersgroep** pagina van wizard Hallo.


## <a name="next-step"></a>Volgende stap
[Taak 3: Configureer beheergroep en Azure AD Domain Services inschakelen](active-directory-ds-getting-started-admingroup.md)
