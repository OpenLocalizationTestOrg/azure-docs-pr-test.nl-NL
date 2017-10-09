---
title: 'Azure Active Directory Domain Services: DC-beheerdersgroep hello Azure AD maken | Microsoft Docs'
description: Azure Active Directory Domain Services met behulp van de klassieke Azure-portal Hallo inschakelen
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
ms.date: 07/13/2017
ms.author: maheshu
ms.openlocfilehash: d629ab9632ef6a45b549630999ff9a122d60c040
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a>Azure Active Directory Domain Services met behulp van de klassieke Azure-portal Hallo inschakelen
In dit artikel wordt beschreven en wordt begeleid Hallo configuratietaken die vereist voor u tooenable Azure Active Directory Domain Services (Azure AD DS) voor uw tenant van Azure Active Directory (Azure AD zijn).

> [!NOTE]
> [**Probeer in plaats daarvan het Hallo nieuwe (preview) Azure portal ervaring**](active-directory-ds-getting-started.md). 
>

## <a name="task-1-create-hello-azure-ad-dc-administrators-group"></a>Taak 1: Maak hello Azure AD DC-beheerdersgroep
de eerste taak Hallo is toocreate een beheergroep in uw Azure AD-tenant. Deze speciale beheerdersgroep heet *AAD DC beheerders*. Leden van deze groep worden beheerdersmachtigingen op de computers die lid zijn van een domein toohello Azure Active Directory Domain Services beheerd domein zijn verleend. Deze groep wordt de groep administrators toohello toegevoegd op domein machines. Leden van deze groep kunnen ook op afstand toodomain die lid zijn van computers met extern bureaublad tooconnect gebruiken.  

> [!NOTE]
> U bent niet gemachtigd domeinbeheerder of ondernemingsbeheerder op Hallo beheerde domein dat u hebt gemaakt met behulp van Azure Active Directory Domain Services. Op de beheerde domeinen deze machtigingen zijn gereserveerd door het Hallo-service en zijn niet beschikbaar toousers binnen Hallo-tenant. U kunt echter gebruiken Hallo speciale beheergroep gemaakt in deze configuratie taak tooperform bevoegde enkele bewerkingen. Deze bewerkingen behoren lid te worden computers toohello domein, die deel uitmaken van de beheergroep toohello op machines domein en het configureren van Groepsbeleid.
>

In deze configuratietaak Hallo beheergroep maken en toevoegen van een of meer gebruikers in uw directory toohello-groep. toocreate Hallo-beheergroep van Azure Active Directory Domain Services, Hallo te volgen:

1. Ga toohello [klassieke Azure-portal](https://manage.windowsazure.com).
2. Selecteer in het linkerdeelvenster Hallo Hallo **Active Directory** knop.
3. Hello Azure AD-tenant (directory) dat waarvoor u tooenable Azure Active Directory Domain Services wilt selecteren. U kunt slechts één domein voor elke Azure AD-directory maken.

    ![Azure AD-directory selecteren](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. Op Hallo **preview directory** pagina, klikt u op Hallo **groepen** tabblad.
5. Klik op tooadd een groep tooyour Azure AD-tenant, in het taakvenster Hallo HALLO hallo venster onderaan in **groep toevoegen**.

    ![knop Hallo-groep toevoegen](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. In Hallo **groep toevoegen** dialoogvenster vak, maakt u een groep met de naam **AAD DC beheerders**, en stel vervolgens **groepstype** te**beveiliging**.

   > [!WARNING]
   > tooenable toegang in uw Azure Active Directory Domain Services beheerd domein, een groep maken met deze naam.
   >
   >

    ![dialoogvenster Hallo-groep toevoegen](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. In Hallo **beschrijving** vak, voer een beschrijving in waarmee anderen toounderstand deze codegroep beheerdersmachtigingen binnen Azure Active Directory Domain Services.
8. Nadat u Hallo groep hebt gemaakt, klikt u de eigenschappen op Hallo groep naam tooview.
9. tooadd gebruikers als leden van de groep hello, onderaan Hallo Hallo-venster, klikt u op Hallo **leden toevoegen** knop.

    ![Knop voor leden van groep toevoegen](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. In Hallo **leden toevoegen** in het dialoogvenster selecteert Hallo-gebruikers die moeten worden leden van deze groep en klik vervolgens op het vinkje Hallo op Hallo rechtsonder.

    ![Tooadministrators gebruikersgroep toevoegen](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a>Volgende stap
[Taak 2: Maak of Selecteer een Azure-netwerk](active-directory-ds-getting-started-vnet.md)
