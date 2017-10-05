---
title: Gebruik een Office 365-tenant met een Azure-abonnement | Microsoft Docs
description: Informatie over het toevoegen van een Office 365-directory (tenant) aan een Azure-abonnement.
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
ms.openlocfilehash: 7affb4a83cdb8ababef60e786a3c824e7477ed68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="associate-an-office-365-tenant-to-an-azure-subscription"></a>Koppelen van een Office 365-tenant met een Azure-abonnement
Uw afzonderlijke Azure en Office 365-abonnementen koppelen zodat u toegang hebt tot de Office 365-tenant van uw Azure-abonnement. Als u wilt koppelen van uw abonnementen, aanmelden bij Azure met de administrator-account Azure-service, een map toevoegen en de organisatie Office 365-accounts toevoegen aan de Azure Active Directory-tenant.

Als u wilt dat Office 365-abonnement voor gebruikers in uw Azure Active Directory-exemplaar of een Office 365-account, maar niet een Azure-account hebt, raadpleegt u [aanmelden voor Azure met Office 365-account](billing-use-existing-office-365-account-azure-subscription.md). 

## <a name="before-you-begin"></a>Voordat u begint
* U moet de referenties van de beheerder van de service Azure-abonnement hebben. Sommige van de stappen in dit artikel is niet mogelijk in medebeheerder accounts. Zie het wijzigen van de servicebeheerder [toevoegen of wijzigen van de Azure-beheerdersrollen](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).
* U kunt de referenties van een globale beheerder van de Office 365-tenant moet hebben.
* Het e-mailadres van de servicebeheerder moet niet in de Office 365-tenant.
* Het e-mailadres van de servicebeheerder moet niet overeenkomen met die van een globale beheerder van de Office 365-tenant.
* Als u een e-mailadres dat is zowel een Microsoft-account als een organisatie-account gebruikt, moet u tijdelijk de servicebeheerder van uw Azure-abonnement van de voor het gebruik van een andere Microsoft-account wijzigen. Kunt u een Microsoft-account op de [aanmeldingspagina voor Microsoft-account](https://signup.live.com/).

## <a name="link-office-365-tenant-to-azure-subscription"></a>Office 365-tenant voor koppeling met Azure-abonnement
Om te koppelen van de Office 365-tenant met de Azure-abonnement, de volgende stappen uit:

### <a name="step-1-add-office-365-tenant-to-your-azure-subscription"></a>Stap 1: Office 365-tenant toevoegen aan uw Azure-abonnement

1. Aanmelden bij de [klassieke Azure-portal](https://manage.windowsazure.com/) met de beheerdersreferenties voor de service.

    ![Schermopname van Azure-aanmeldingspagina](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. Selecteer in het linkerdeelvenster **ACTIVE DIRECTORY**. Er mag niet de Office 365-tenant. Als u deze ziet, gaat u naar [stap 2: de map die is gekoppeld aan het Azure-abonnement wijzigen](#Step2).
   
   ![Schermopname van Active Directory-vermelding](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. Selecteer **nieuw** > **DIRECTORY** > **aangepast maken**.
   
    ![Schermopname van Azure Active Directory aangepast maken](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. Op de **toevoegen directory** pagina onder **DIRECTORY**, selecteer **bestaande directory gebruiken**. Selecteer vervolgens **ik ben klaar om te worden afgemeld**, en selecteer **Complete** ![voltooien pictogram](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).
   
    ![Schermafbeelding van de 'Bestaande directory gebruiken'](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. Nadat u bent afgemeld, meldt u zich aan met de referenties van de globale beheerder van uw Office 365-tenant.
   
    ![Schermopname van Office 365-hoofdbeheerder aanmelden](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. Selecteer **gaan**.
   
    ![Schermopname van verificatie](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. Selecteer **nu afmelden**.
   
    ![Schermopname van afmelden](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. Aanmelden bij de [klassieke Azure-portal](https://manage.windowsazure.com/) met de beheerdersreferenties voor de service.
   
    ![Schermopname van Azure-aanmeldingspagina](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. U ziet uw Office 365-tenant in het dashboard.
   
    ![Schermopname van dashboard](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <a name="Step2"></a>Stap 2: De map die is gekoppeld aan het Azure-abonnement wijzigen
   
1. Selecteer **instellingen**.
   
    ![Schermopname van Azure classic portal Instellingenpictogram](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. Selecteer uw Azure-abonnement en selecteer vervolgens **DIRECTORY bewerken**.

    ![Schermopname van Azure-abonnement bewerken directory](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. Selecteer **volgende** ![volgende pictogram](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).
   
    ![Schermopname van "Wijziging de bijbehorende map"](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. Bekijk de betrokken accounts. Alle medebeheerders en [op rollen gebaseerde toegangsbeheer (RBAC)](../active-directory/role-based-access-control-configure.md) gebruikers met een toegewezen toegang tot in de bestaande resourcegroepen worden verwijderd. De waarschuwing die u ontvangt noemt alleen het verwijderen van medebeheerders.
      
    ![Schermafbeelding van de medebeheerder accounts moeten worden verwijderd.](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![Schermafbeelding van een voorbeeld van de gebruikersaccount moet worden verwijderd.](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. Selecteer **Complete** ![voltooien pictogram](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-to-the-azure-active-directory-tenant"></a>Stap 3: Uw organisatie Office 365-accounts toevoegen als medebeheerders aan de Azure Active Directory-tenant
   
1. Selecteer de **beheerders** tabblad en selecteer vervolgens **toevoegen**.
   
    ![Tabblad beheerders van schermopname van Azure classic portal-instellingen](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. Een organisatie-account van uw Office 365-tenant, het Azure-abonnement selecteren, en selecteer vervolgens **Complete** ![voltooien pictogram](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).
   
    ![Schermopname van Azure toevoegen medebeheerder dialoogvenster](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. Ga terug naar de **beheerders** tabblad. U ziet het organisatie-account wordt weergegeven als medebeheerder.
   
    ![Schermafbeelding van tabblad beheerders](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  Toegang tot Azure met het account medebeheerder testen.
   
    a. Afmelden bij de klassieke Azure portal.
   
    b. Open de [Azure Portal](https://portal.azure.com/).
   
    c. Voer de referenties van de CO-beheerder en selecteer vervolgens **aanmelden**.
   
    ![Schermopname van Azure-aanmeldingspagina](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a>Hulp nodig? Neem contact op met ondersteuning.
Als u nog hulp nodig hebt, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) ophalen van uw probleem snel worden opgelost.


