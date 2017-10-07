---
title: aaaUse een Office 365-tenant met een Azure-abonnement | Microsoft Docs
description: Meer informatie over hoe een Office 365 tooadd directory (tenant) tooan Azure-abonnement.
services: 
documentationcenter: 
author: JiangChen79
manager: jlian
editor: 
tags: billing,top-support-issue
ms.assetid: cc9c57c6-7bfd-4dea-9027-c75ef3737589
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: cjiang
ms.openlocfilehash: e560370417bd074a7e37ceb7c60da45dbbbcf775
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="associate-an-office-365-tenant-tooan-azure-subscription"></a>Koppelen van een Office 365-tenant tooan Azure-abonnement
Uw afzonderlijke Azure en Office 365-abonnementen koppelen zodat u toegang hebt tot Hallo Office 365-tenant van uw Azure-abonnement. toolink uw abonnementen aanmelden tooAzure Hello administrator-account Azure-service, voegt u een map toe en Hallo Office 365 organisatieaccounts toohello Azure Active Directory-tenant.

Als u wilt dat Office 365-abonnement voor gebruikers in uw Azure Active Directory-exemplaar of een Office 365-account, maar niet een Azure-account hebt, raadpleegt u [aanmelden voor Azure met Office 365-account](billing-use-existing-office-365-account-azure-subscription.md). 

## <a name="before-you-begin"></a>Voordat u begint
* U moet referenties op Hallo van servicebeheerder voor hello Azure-abonnement hebben. Medebeheerder accounts niet sommige Hallo stappen in dit artikel. toochange de servicebeheerder Zie [hoe tooadd of wijzig Azure-beheerdersrollen](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).
* U moet de referenties van een globale beheerder van Office 365-tenant Hallo Hallo hebben.
* Hallo e-mailadres van de servicebeheerder Hallo mag geen in Hallo Office 365-tenant.
* Hallo e-mailadres van de servicebeheerder Hallo moet niet overeenkomen met die van een globale beheerder van Hallo Office 365-tenant.
* Als u een e-mailadres dat is zowel een Microsoft-account en een organisatieaccount, tijdelijk servicebeheerder Hallo van uw Azure-abonnement toouse een andere Microsoft-account wijzigen. U kunt een Microsoft-account maken op Hallo [aanmeldingspagina voor Microsoft-account](https://signup.live.com/).

## <a name="link-office-365-tenant-tooazure-subscription"></a>Office 365-tenant tooAzure abonnement koppelen
tooassociate hello Office 365-tenant toohello Azure-abonnement, als volgt te werk:

### <a name="step-1-add-office-365-tenant-tooyour-azure-subscription"></a>Stap 1: Office 365-tenant tooyour Azure-abonnement toevoegen

1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com/) met beheerdersreferenties Hallo-service.

    ![Schermopname van Azure-aanmeldingspagina](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. Selecteer in het linkerdeelvenster Hallo **ACTIVE DIRECTORY**. Er mag niet Hallo Office 365-tenant. Als u deze ziet, gaat u verder te[stap 2: de map Hallo wijzigen die zijn gekoppeld aan hello Azure-abonnement](#Step2).
   
   ![Schermopname van Active Directory-vermelding](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. Selecteer **nieuw** > **DIRECTORY** > **aangepast maken**.
   
    ![Schermopname van Azure Active Directory aangepast maken](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. Op Hallo **toevoegen directory** pagina onder **DIRECTORY**, selecteer **bestaande directory gebruiken**. Selecteer vervolgens **ik ben klaar toobe afgemeld**, en selecteer **Complete** ![voltooien pictogram](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).
   
    ![Schermafbeelding van de 'Bestaande directory gebruiken'](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. Nadat u bent afgemeld, meld u aan met referenties Hallo globale beheerder van uw Office 365-tenant.
   
    ![Schermopname van Office 365-hoofdbeheerder aanmelden](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. Selecteer **gaan**.
   
    ![Schermopname van verificatie](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. Selecteer **nu afmelden**.
   
    ![Schermopname van afmelden](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com/) met beheerdersreferenties Hallo-service.
   
    ![Schermopname van Azure-aanmeldingspagina](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. U ziet uw Office 365-tenant in Hallo-dashboard.
   
    ![Schermopname van dashboard](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <a name="Step2"></a>Stap 2: Hallo-map die is gekoppeld aan hello Azure-abonnement wijzigen
   
1. Selecteer **instellingen**.
   
    ![Schermopname van Azure classic portal Instellingenpictogram](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. Selecteer uw Azure-abonnement en selecteer vervolgens **DIRECTORY bewerken**.

    ![Schermopname van Azure-abonnement bewerken directory](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. Selecteer **volgende** ![volgende pictogram](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).
   
    ![Schermopname van het "Wijziging hello gekoppeld directory"](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. Bekijk Hallo van invloed op een accounts. Alle medebeheerders en [op rollen gebaseerde toegangsbeheer (RBAC)](../active-directory/role-based-access-control-configure.md) gebruikers toegewezen toegang in Hallo bestaande resourcegroepen worden verwijderd. Hallo waarschuwing verschijnt noemt alleen Hallo verwijderen van medebeheerders.
      
    ![Schermafbeelding van Hallo medebeheerder accounts toobe verwijderd.](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![Schermafbeelding van een voorbeeld van de gebruiker account toobe verwijderd.](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. Selecteer **Complete** ![voltooien pictogram](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-toohello-azure-active-directory-tenant"></a>Stap 3: Uw organisatie Office 365-accounts toevoegen als medebeheerders toohello Azure Active Directory-tenant
   
1. Selecteer Hallo **beheerders** tabblad en selecteer vervolgens **toevoegen**.
   
    ![Tabblad beheerders van schermopname van Azure classic portal-instellingen](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. Een organisatie-account van uw Office 365-tenant, hello Azure-abonnement selecteren, en selecteer vervolgens **Complete** ![voltooien pictogram](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).
   
    ![Schermopname van Azure toevoegen medebeheerder dialoogvenster](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. Ga terug toohello **beheerders** tabblad. U ziet Hallo organisatie-account wordt weergegeven als medebeheerder.
   
    ![Schermafbeelding van tabblad beheerders](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  Test toegang tooAzure met Hallo mede administrator-account.
   
    a. Meld u af bij Hallo klassieke Azure-portal.
   
    b. Open Hallo [Azure-portal](https://portal.azure.com/).
   
    c. Geef referenties op Hallo van Hallo medebeheerder en selecteer vervolgens **aanmelden**.
   
    ![Schermopname van Azure-aanmeldingspagina](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a>Hulp nodig? Neem contact op met ondersteuning.
Als u nog hulp nodig hebt, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget uw probleem snel worden opgelost.


