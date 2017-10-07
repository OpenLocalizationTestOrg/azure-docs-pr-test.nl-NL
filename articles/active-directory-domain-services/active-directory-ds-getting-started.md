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
ms.date: 08/28/2017
ms.author: maheshu
ms.openlocfilehash: 79cbb21c4a50194f5ad8ca1a4a8493ee4a260a9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Azure Active Directory Domain Services met behulp van hello Azure-portal (Preview) inschakelen
Dit artikel laat zien hoe tooenable Azure Active Directory Domain Services (Azure AD DS) met behulp van hello Azure-portal.


Hallo toolaunch **inschakelen Azure AD Domain Services** wizard, volledige Hallo stappen te volgen:

1. Ga toohello [Azure-portal](https://portal.azure.com).
2. Klik in het linkerdeelvenster Hallo op **nieuw**.
3. In Hallo **nieuw** blade, type **domeinservices** in Hallo zoekbalk.

    ![Zoeken naar domeinservices](./media/getting-started/search-domain-services.png)

4. Klik op tooselect **Azure AD Domain Services** uit de lijst Hallo van zoeksuggesties. Op Hallo **Azure AD Domain Services** blade, klikt u op Hallo **maken** knop.

    ![Domain services-blade](./media/getting-started/domain-services-blade.png)

5. Hallo **inschakelen Azure AD Domain Services** wizard wordt gestart.


## <a name="task-1-configure-basic-settings"></a>Taak 1: basisinstellingen configureren
In Hallo **basisbeginselen** pagina van wizard hello, kunt u Hallo DNS-domeinnaam voor het beheerde domein Hallo opgeven. U kunt ook Hallo resourcegroep en Azure-locatie toowhich Hallo beheerd domein moet worden geïmplementeerd.

![Basisprincipes configureren](./media/getting-started/domain-services-blade-basics.png)

1. Kies Hallo **DNS-domeinnaam** voor uw beheerde domein.

   * Hallo standaarddomeinnaam van Hallo-map (met een **. onmicrosoft.com** achtervoegsel) standaard is opgegeven.

   * U kunt er ook voor typen in een aangepaste domeinnaam. In dit voorbeeld wordt de aangepaste domeinnaam Hallo is *contoso100.com*.

     > [!WARNING]
     > Hallo-voorvoegsel van de opgegeven domeinnaam (bijvoorbeeld *contoso100* in Hallo *contoso100.com* domeinnaam) moet 15 of minder tekens bevatten. U kunt een beheerd domein maken met een voorvoegsel langer is dan 15 tekens.
     >
     >

2. Zorg ervoor dat die Hallo DNS-domeinnaam die u hebt gekozen voor Hallo beheerd domein nog niet bestaat in het virtuele netwerk Hallo. Controleer in het bijzonder of:

   * U hebt al een domein met Hallo dezelfde DNS-domeinnaam op Hallo virtueel netwerk.

   * Hallo virtueel netwerk waar u van plan tooenable Hallo beheerd domein bent heeft een VPN-verbinding met uw on-premises netwerk. In dit scenario, zorg ervoor dat u hebt geen een domein met Hallo dezelfde DNS-domeinnaam op uw on-premises netwerk.

   * U hebt een bestaande cloudservice met die naam op Hallo virtueel netwerk.

3. Kies Hallo **type virtueel netwerk**. Standaard Hallo **Resource Manager** type virtueel netwerk dat is geselecteerd. Het wordt aangeraden om dit type virtueel netwerk gebruiken voor alle beheerde domeinen van een nieuw gemaakt.

4. Selecteer hello Azure **abonnement** waarin u wilt toocreate Hallo beheerd domein.

5. Selecteer Hallo **resourcegroep** moet deel uitmaken van toowhich Hallo beheerd domein. U kunt beide Hallo **nieuw** of **gebruik bestaande** opties tooselect Hallo-resourcegroep.

6. Kies hello Azure **locatie** aan welke Hallo beheerd domein moet worden gemaakt. Op Hallo **netwerk** pagina van wizard hello, ziet u alleen virtuele netwerken die deel uitmaken van toohello locatie die u hebt geselecteerd.

7. Wanneer u klaar bent, klikt u op **OK** toomove op toohello **netwerk** pagina van wizard Hallo.


## <a name="next-step"></a>Volgende stap
[Taak 2: De netwerkinstellingen configureren](active-directory-ds-getting-started-network.md)
