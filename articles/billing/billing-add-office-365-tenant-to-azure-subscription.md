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
# <a name="associate-an-office-365-tenant-to-an-azure-subscription"></a><span data-ttu-id="a297d-103">Koppelen van een Office 365-tenant met een Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="a297d-103">Associate an Office 365 tenant to an Azure subscription</span></span>
<span data-ttu-id="a297d-104">Uw afzonderlijke Azure en Office 365-abonnementen koppelen zodat u toegang hebt tot de Office 365-tenant van uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a297d-104">Link your separate Azure and Office 365 subscriptions so that you can access the Office 365 tenant from your Azure subscription.</span></span> <span data-ttu-id="a297d-105">Als u wilt koppelen van uw abonnementen, aanmelden bij Azure met de administrator-account Azure-service, een map toevoegen en de organisatie Office 365-accounts toevoegen aan de Azure Active Directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="a297d-105">To link your subscriptions, sign in to Azure with the Azure service administrator account, add a directory, and add the Office 365 organizational accounts to the Azure Active Directory tenant.</span></span>

<span data-ttu-id="a297d-106">Als u wilt dat Office 365-abonnement voor gebruikers in uw Azure Active Directory-exemplaar of een Office 365-account, maar niet een Azure-account hebt, raadpleegt u [aanmelden voor Azure met Office 365-account](billing-use-existing-office-365-account-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="a297d-106">If you want an Office 365 subscription for users in your Azure Active Directory instance or you have an Office 365 account but not an Azure account, see [Sign up for Azure with Office 365 account](billing-use-existing-office-365-account-azure-subscription.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="a297d-107">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="a297d-107">Before you begin</span></span>
* <span data-ttu-id="a297d-108">U moet de referenties van de beheerder van de service Azure-abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="a297d-108">You must have the credentials of the Azure subscription service administrator.</span></span> <span data-ttu-id="a297d-109">Sommige van de stappen in dit artikel is niet mogelijk in medebeheerder accounts.</span><span class="sxs-lookup"><span data-stu-id="a297d-109">Co-administrator accounts can't do some of the steps in this article.</span></span> <span data-ttu-id="a297d-110">Zie het wijzigen van de servicebeheerder [toevoegen of wijzigen van de Azure-beheerdersrollen](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span><span class="sxs-lookup"><span data-stu-id="a297d-110">To change your service administrator, see [How to add or change Azure administrator roles](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span></span>
* <span data-ttu-id="a297d-111">U kunt de referenties van een globale beheerder van de Office 365-tenant moet hebben.</span><span class="sxs-lookup"><span data-stu-id="a297d-111">You must have the credentials of a global administrator of the Office 365 tenant.</span></span>
* <span data-ttu-id="a297d-112">Het e-mailadres van de servicebeheerder moet niet in de Office 365-tenant.</span><span class="sxs-lookup"><span data-stu-id="a297d-112">The email address of the service administrator must not be in the Office 365 tenant.</span></span>
* <span data-ttu-id="a297d-113">Het e-mailadres van de servicebeheerder moet niet overeenkomen met die van een globale beheerder van de Office 365-tenant.</span><span class="sxs-lookup"><span data-stu-id="a297d-113">The email address of the service administrator must not match that of any global administrator of the Office 365 tenant.</span></span>
* <span data-ttu-id="a297d-114">Als u een e-mailadres dat is zowel een Microsoft-account als een organisatie-account gebruikt, moet u tijdelijk de servicebeheerder van uw Azure-abonnement van de voor het gebruik van een andere Microsoft-account wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a297d-114">If you use an email address that is both a Microsoft account and an organizational account, temporarily change the service administrator of your Azure subscription to use another Microsoft account.</span></span> <span data-ttu-id="a297d-115">Kunt u een Microsoft-account op de [aanmeldingspagina voor Microsoft-account](https://signup.live.com/).</span><span class="sxs-lookup"><span data-stu-id="a297d-115">You can create a Microsoft account at the [Microsoft account signup page](https://signup.live.com/).</span></span>

## <a name="link-office-365-tenant-to-azure-subscription"></a><span data-ttu-id="a297d-116">Office 365-tenant voor koppeling met Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="a297d-116">Link Office 365 tenant to Azure subscription</span></span>
<span data-ttu-id="a297d-117">Om te koppelen van de Office 365-tenant met de Azure-abonnement, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="a297d-117">To associate the Office 365 tenant to the Azure subscription, follow these steps:</span></span>

### <a name="step-1-add-office-365-tenant-to-your-azure-subscription"></a><span data-ttu-id="a297d-118">Stap 1: Office 365-tenant toevoegen aan uw Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="a297d-118">Step 1: Add Office 365 tenant to your Azure subscription</span></span>

1. <span data-ttu-id="a297d-119">Aanmelden bij de [klassieke Azure-portal](https://manage.windowsazure.com/) met de beheerdersreferenties voor de service.</span><span class="sxs-lookup"><span data-stu-id="a297d-119">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) with the service administrator credentials.</span></span>

    ![Schermopname van Azure-aanmeldingspagina](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. <span data-ttu-id="a297d-121">Selecteer in het linkerdeelvenster **ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="a297d-121">In the left pane, select **ACTIVE DIRECTORY**.</span></span> <span data-ttu-id="a297d-122">Er mag niet de Office 365-tenant.</span><span class="sxs-lookup"><span data-stu-id="a297d-122">You shouldn't see the Office 365 tenant.</span></span> <span data-ttu-id="a297d-123">Als u deze ziet, gaat u naar [stap 2: de map die is gekoppeld aan het Azure-abonnement wijzigen](#Step2).</span><span class="sxs-lookup"><span data-stu-id="a297d-123">If you see it, skip to [Step 2: Change the directory associated with the Azure subscription](#Step2).</span></span>
   
   ![Schermopname van Active Directory-vermelding](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. <span data-ttu-id="a297d-125">Selecteer **nieuw** > **DIRECTORY** > **aangepast maken**.</span><span class="sxs-lookup"><span data-stu-id="a297d-125">Select **NEW** > **DIRECTORY** > **CUSTOM CREATE**.</span></span>
   
    ![Schermopname van Azure Active Directory aangepast maken](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. <span data-ttu-id="a297d-127">Op de **toevoegen directory** pagina onder **DIRECTORY**, selecteer **bestaande directory gebruiken**.</span><span class="sxs-lookup"><span data-stu-id="a297d-127">On the **Add directory** page, under **DIRECTORY**, select **Use existing directory**.</span></span> <span data-ttu-id="a297d-128">Selecteer vervolgens **ik ben klaar om te worden afgemeld**, en selecteer **Complete** ![voltooien pictogram](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="a297d-128">Then select **I am ready to be signed out now**, and select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Schermafbeelding van de 'Bestaande directory gebruiken'](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. <span data-ttu-id="a297d-130">Nadat u bent afgemeld, meldt u zich aan met de referenties van de globale beheerder van uw Office 365-tenant.</span><span class="sxs-lookup"><span data-stu-id="a297d-130">After you are signed out, sign in with the global administrator’s credentials of your Office 365 tenant.</span></span>
   
    ![Schermopname van Office 365-hoofdbeheerder aanmelden](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. <span data-ttu-id="a297d-132">Selecteer **gaan**.</span><span class="sxs-lookup"><span data-stu-id="a297d-132">Select **Continue**.</span></span>
   
    ![Schermopname van verificatie](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. <span data-ttu-id="a297d-134">Selecteer **nu afmelden**.</span><span class="sxs-lookup"><span data-stu-id="a297d-134">Select **Sign out now**.</span></span>
   
    ![Schermopname van afmelden](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. <span data-ttu-id="a297d-136">Aanmelden bij de [klassieke Azure-portal](https://manage.windowsazure.com/) met de beheerdersreferenties voor de service.</span><span class="sxs-lookup"><span data-stu-id="a297d-136">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) with the service administrator credentials.</span></span>
   
    ![Schermopname van Azure-aanmeldingspagina](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. <span data-ttu-id="a297d-138">U ziet uw Office 365-tenant in het dashboard.</span><span class="sxs-lookup"><span data-stu-id="a297d-138">You should see your Office 365 tenant in the dashboard.</span></span>
   
    ![Schermopname van dashboard](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <span data-ttu-id="a297d-140"><a name="Step2"></a>Stap 2: De map die is gekoppeld aan het Azure-abonnement wijzigen</span><span class="sxs-lookup"><span data-stu-id="a297d-140"><a name="Step2"></a>Step 2: Change the directory associated with the Azure subscription</span></span>
   
1. <span data-ttu-id="a297d-141">Selecteer **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="a297d-141">Select **Settings**.</span></span>
   
    ![Schermopname van Azure classic portal Instellingenpictogram](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. <span data-ttu-id="a297d-143">Selecteer uw Azure-abonnement en selecteer vervolgens **DIRECTORY bewerken**.</span><span class="sxs-lookup"><span data-stu-id="a297d-143">Select your Azure subscription, and then select **EDIT DIRECTORY**.</span></span>

    ![Schermopname van Azure-abonnement bewerken directory](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. <span data-ttu-id="a297d-145">Selecteer **volgende** ![volgende pictogram](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span><span class="sxs-lookup"><span data-stu-id="a297d-145">Select **Next** ![Next icon](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span></span>
   
    ![Schermopname van "Wijziging de bijbehorende map"](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. <span data-ttu-id="a297d-147">Bekijk de betrokken accounts.</span><span class="sxs-lookup"><span data-stu-id="a297d-147">Review the affected accounts.</span></span> <span data-ttu-id="a297d-148">Alle medebeheerders en [op rollen gebaseerde toegangsbeheer (RBAC)](../active-directory/role-based-access-control-configure.md) gebruikers met een toegewezen toegang tot in de bestaande resourcegroepen worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="a297d-148">All co-administrators and [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) users with assigned access in the existing resource groups are removed.</span></span> <span data-ttu-id="a297d-149">De waarschuwing die u ontvangt noemt alleen het verwijderen van medebeheerders.</span><span class="sxs-lookup"><span data-stu-id="a297d-149">The warning you receive only mentions the removal of co-administrators.</span></span>
      
    ![Schermafbeelding van de medebeheerder accounts moeten worden verwijderd.](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![Schermafbeelding van een voorbeeld van de gebruikersaccount moet worden verwijderd.](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. <span data-ttu-id="a297d-152">Selecteer **Complete** ![voltooien pictogram](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="a297d-152">Select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-to-the-azure-active-directory-tenant"></a><span data-ttu-id="a297d-153">Stap 3: Uw organisatie Office 365-accounts toevoegen als medebeheerders aan de Azure Active Directory-tenant</span><span class="sxs-lookup"><span data-stu-id="a297d-153">Step 3: Add your Office 365 organizational accounts as co-administrators to the Azure Active Directory tenant</span></span>
   
1. <span data-ttu-id="a297d-154">Selecteer de **beheerders** tabblad en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a297d-154">Select the **ADMINISTRATORS** tab, and then select **ADD**.</span></span>
   
    ![Tabblad beheerders van schermopname van Azure classic portal-instellingen](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. <span data-ttu-id="a297d-156">Een organisatie-account van uw Office 365-tenant, het Azure-abonnement selecteren, en selecteer vervolgens **Complete** ![voltooien pictogram](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="a297d-156">Enter an organizational account of your Office 365 tenant, select the Azure subscription, and then select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Schermopname van Azure toevoegen medebeheerder dialoogvenster](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. <span data-ttu-id="a297d-158">Ga terug naar de **beheerders** tabblad.</span><span class="sxs-lookup"><span data-stu-id="a297d-158">Go back to the **ADMINISTRATORS** tab.</span></span> <span data-ttu-id="a297d-159">U ziet het organisatie-account wordt weergegeven als medebeheerder.</span><span class="sxs-lookup"><span data-stu-id="a297d-159">You should see the organizational account displayed as co-administrator.</span></span>
   
    ![Schermafbeelding van tabblad beheerders](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  <span data-ttu-id="a297d-161">Toegang tot Azure met het account medebeheerder testen.</span><span class="sxs-lookup"><span data-stu-id="a297d-161">Test access to Azure with the co-administrator account.</span></span>
   
    <span data-ttu-id="a297d-162">a.</span><span class="sxs-lookup"><span data-stu-id="a297d-162">a.</span></span> <span data-ttu-id="a297d-163">Afmelden bij de klassieke Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a297d-163">Sign out of the Azure classic portal.</span></span>
   
    <span data-ttu-id="a297d-164">b.</span><span class="sxs-lookup"><span data-stu-id="a297d-164">b.</span></span> <span data-ttu-id="a297d-165">Open de [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a297d-165">Open the [Azure portal](https://portal.azure.com/).</span></span>
   
    <span data-ttu-id="a297d-166">c.</span><span class="sxs-lookup"><span data-stu-id="a297d-166">c.</span></span> <span data-ttu-id="a297d-167">Voer de referenties van de CO-beheerder en selecteer vervolgens **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="a297d-167">Enter the credentials of the co-administrator, and then select **Sign in**.</span></span>
   
    ![Schermopname van Azure-aanmeldingspagina](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a><span data-ttu-id="a297d-169">Hulp nodig?</span><span class="sxs-lookup"><span data-stu-id="a297d-169">Need help?</span></span> <span data-ttu-id="a297d-170">Neem contact op met ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="a297d-170">Contact support.</span></span>
<span data-ttu-id="a297d-171">Als u nog hulp nodig hebt, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) ophalen van uw probleem snel worden opgelost.</span><span class="sxs-lookup"><span data-stu-id="a297d-171">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>


