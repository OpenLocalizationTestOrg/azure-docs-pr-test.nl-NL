---
title: 'Azure Active Directory Domain Services: De Azure AD-DC-beheerdersgroep maken | Microsoft Docs'
description: Azure Active Directory Domain Services inschakelen met behulp van de klassieke Azure-portal
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
ms.openlocfilehash: 5ed0125e05928cf0f6d9941e099b433ecb46e6e2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-classic-portal"></a>Azure Active Directory Domain Services inschakelen met behulp van de klassieke Azure-portal
In dit artikel wordt beschreven en wordt begeleid bij de configuratietaken die vereist zijn voor u inschakelen van Azure Active Directory Domain Services (Azure AD DS) voor uw tenant van Azure Active Directory (Azure AD).

> [!NOTE]
> [**Probeer de nieuwe portal (preview) Azure-ervaring in plaats daarvan**](active-directory-ds-getting-started.md). 
>

## <a name="task-1-create-the-azure-ad-dc-administrators-group"></a>Taak 1: de Azure AD-DC-beheerdersgroep maken
De eerste taak is het maken van een beheergroep in uw Azure AD-tenant. Deze speciale beheerdersgroep heet *AAD DC beheerders*. Leden van deze groep worden verleend beheerdersmachtigingen op de computers die zijn met het domein is gekoppeld aan het Azure Active Directory Domain Services beheerd domein. Op de machines domein, wordt deze groep toegevoegd aan de groep administrators. Leden van deze groep kunnen ook extern bureaublad gebruiken extern verbinding maken met domein-machines.  

> [!NOTE]
> U bent niet gemachtigd domeinbeheerder of ondernemingsbeheerder op het beheerde domein die u hebt gemaakt met behulp van Azure Active Directory Domain Services. Op de beheerde domeinen, worden deze machtigingen zijn gereserveerd door de service en zijn niet beschikbaar gesteld aan gebruikers van de tenant. Echter kunt u de speciale beheergroep gemaakt in deze taak voor de configuratie kunt u sommige bevoorrechte bewerkingen uitvoeren. Deze bewerkingen zijn computers toevoegen aan het domein en Groepsbeleid configureren die deel uitmaken van de beheergroep op domein-machines.
>

In deze configuratietaak maken van de beheergroep en een of meer gebruikers in uw directory toevoegen aan de groep. Voor het maken van de beheergroep voor Azure Active Directory Domain Services, het volgende doen:

1. Ga naar de [klassieke Azure-portal](https://manage.windowsazure.com).
2. Selecteer de knop **Active Directory** in het linkerdeelvenster.
3. Selecteer de Azure AD-tenant (directory) waarvoor u wilt inschakelen van Azure Active Directory Domain Services. U kunt slechts één domein voor elke Azure AD-directory maken.

    ![Azure AD-directory selecteren](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. Op de **preview directory** pagina, klikt u op de **groepen** tabblad.
5. U voegt een groep toe aan uw Azure AD-tenant in het taakvenster onder aan het venster **groep toevoegen**.

    ![De knop groep toevoegen](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. In de **groep toevoegen** dialoogvenster vak, maakt u een groep met de naam **AAD DC beheerders**, en stel vervolgens **groepstype** naar **beveiliging**.

   > [!WARNING]
   > Voor toegang binnen uw Azure Active Directory Domain Services beheerd domein, een groep te maken met deze naam.
   >
   >

    ![Het dialoogvenster groep toevoegen](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. In de **beschrijving** vak, voer een beschrijving in waarmee anderen om te begrijpen dat deze codegroep beheerdersmachtigingen binnen Azure Active Directory Domain Services.
8. Nadat u de groep hebt gemaakt, klikt u op de naam van de groep om de eigenschappen ervan weer te geven.
9. U kunt gebruikers toevoegen als leden van de groep aan de onderkant van het venster op de **leden toevoegen** knop.

    ![Knop voor leden van groep toevoegen](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. In de **leden toevoegen** dialoogvenster Selecteer de gebruikers die u moeten lid zijn van deze groep en klik vervolgens op het vinkje in de rechterbenedenhoek.

    ![Gebruikers toevoegen aan de groep administrators](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a>Volgende stap
[Taak 2: Maak of Selecteer een Azure-netwerk](active-directory-ds-getting-started-vnet.md)
