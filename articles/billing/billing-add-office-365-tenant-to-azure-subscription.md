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
# <a name="associate-an-office-365-tenant-tooan-azure-subscription"></a><span data-ttu-id="4dadc-103">Koppelen van een Office 365-tenant tooan Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="4dadc-103">Associate an Office 365 tenant tooan Azure subscription</span></span>
<span data-ttu-id="4dadc-104">Uw afzonderlijke Azure en Office 365-abonnementen koppelen zodat u toegang hebt tot Hallo Office 365-tenant van uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="4dadc-104">Link your separate Azure and Office 365 subscriptions so that you can access hello Office 365 tenant from your Azure subscription.</span></span> <span data-ttu-id="4dadc-105">toolink uw abonnementen aanmelden tooAzure Hello administrator-account Azure-service, voegt u een map toe en Hallo Office 365 organisatieaccounts toohello Azure Active Directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="4dadc-105">toolink your subscriptions, sign in tooAzure with hello Azure service administrator account, add a directory, and add hello Office 365 organizational accounts toohello Azure Active Directory tenant.</span></span>

<span data-ttu-id="4dadc-106">Als u wilt dat Office 365-abonnement voor gebruikers in uw Azure Active Directory-exemplaar of een Office 365-account, maar niet een Azure-account hebt, raadpleegt u [aanmelden voor Azure met Office 365-account](billing-use-existing-office-365-account-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="4dadc-106">If you want an Office 365 subscription for users in your Azure Active Directory instance or you have an Office 365 account but not an Azure account, see [Sign up for Azure with Office 365 account](billing-use-existing-office-365-account-azure-subscription.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="4dadc-107">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="4dadc-107">Before you begin</span></span>
* <span data-ttu-id="4dadc-108">U moet referenties op Hallo van servicebeheerder voor hello Azure-abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="4dadc-108">You must have hello credentials of hello Azure subscription service administrator.</span></span> <span data-ttu-id="4dadc-109">Medebeheerder accounts niet sommige Hallo stappen in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="4dadc-109">Co-administrator accounts can't do some of hello steps in this article.</span></span> <span data-ttu-id="4dadc-110">toochange de servicebeheerder Zie [hoe tooadd of wijzig Azure-beheerdersrollen](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span><span class="sxs-lookup"><span data-stu-id="4dadc-110">toochange your service administrator, see [How tooadd or change Azure administrator roles](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span></span>
* <span data-ttu-id="4dadc-111">U moet de referenties van een globale beheerder van Office 365-tenant Hallo Hallo hebben.</span><span class="sxs-lookup"><span data-stu-id="4dadc-111">You must have hello credentials of a global administrator of hello Office 365 tenant.</span></span>
* <span data-ttu-id="4dadc-112">Hallo e-mailadres van de servicebeheerder Hallo mag geen in Hallo Office 365-tenant.</span><span class="sxs-lookup"><span data-stu-id="4dadc-112">hello email address of hello service administrator must not be in hello Office 365 tenant.</span></span>
* <span data-ttu-id="4dadc-113">Hallo e-mailadres van de servicebeheerder Hallo moet niet overeenkomen met die van een globale beheerder van Hallo Office 365-tenant.</span><span class="sxs-lookup"><span data-stu-id="4dadc-113">hello email address of hello service administrator must not match that of any global administrator of hello Office 365 tenant.</span></span>
* <span data-ttu-id="4dadc-114">Als u een e-mailadres dat is zowel een Microsoft-account en een organisatieaccount, tijdelijk servicebeheerder Hallo van uw Azure-abonnement toouse een andere Microsoft-account wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4dadc-114">If you use an email address that is both a Microsoft account and an organizational account, temporarily change hello service administrator of your Azure subscription toouse another Microsoft account.</span></span> <span data-ttu-id="4dadc-115">U kunt een Microsoft-account maken op Hallo [aanmeldingspagina voor Microsoft-account](https://signup.live.com/).</span><span class="sxs-lookup"><span data-stu-id="4dadc-115">You can create a Microsoft account at hello [Microsoft account signup page](https://signup.live.com/).</span></span>

## <a name="link-office-365-tenant-tooazure-subscription"></a><span data-ttu-id="4dadc-116">Office 365-tenant tooAzure abonnement koppelen</span><span class="sxs-lookup"><span data-stu-id="4dadc-116">Link Office 365 tenant tooAzure subscription</span></span>
<span data-ttu-id="4dadc-117">tooassociate hello Office 365-tenant toohello Azure-abonnement, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="4dadc-117">tooassociate hello Office 365 tenant toohello Azure subscription, follow these steps:</span></span>

### <a name="step-1-add-office-365-tenant-tooyour-azure-subscription"></a><span data-ttu-id="4dadc-118">Stap 1: Office 365-tenant tooyour Azure-abonnement toevoegen</span><span class="sxs-lookup"><span data-stu-id="4dadc-118">Step 1: Add Office 365 tenant tooyour Azure subscription</span></span>

1. <span data-ttu-id="4dadc-119">Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com/) met beheerdersreferenties Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="4dadc-119">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with hello service administrator credentials.</span></span>

    ![Schermopname van Azure-aanmeldingspagina](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. <span data-ttu-id="4dadc-121">Selecteer in het linkerdeelvenster Hallo **ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="4dadc-121">In hello left pane, select **ACTIVE DIRECTORY**.</span></span> <span data-ttu-id="4dadc-122">Er mag niet Hallo Office 365-tenant.</span><span class="sxs-lookup"><span data-stu-id="4dadc-122">You shouldn't see hello Office 365 tenant.</span></span> <span data-ttu-id="4dadc-123">Als u deze ziet, gaat u verder te[stap 2: de map Hallo wijzigen die zijn gekoppeld aan hello Azure-abonnement](#Step2).</span><span class="sxs-lookup"><span data-stu-id="4dadc-123">If you see it, skip too[Step 2: Change hello directory associated with hello Azure subscription](#Step2).</span></span>
   
   ![Schermopname van Active Directory-vermelding](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. <span data-ttu-id="4dadc-125">Selecteer **nieuw** > **DIRECTORY** > **aangepast maken**.</span><span class="sxs-lookup"><span data-stu-id="4dadc-125">Select **NEW** > **DIRECTORY** > **CUSTOM CREATE**.</span></span>
   
    ![Schermopname van Azure Active Directory aangepast maken](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. <span data-ttu-id="4dadc-127">Op Hallo **toevoegen directory** pagina onder **DIRECTORY**, selecteer **bestaande directory gebruiken**.</span><span class="sxs-lookup"><span data-stu-id="4dadc-127">On hello **Add directory** page, under **DIRECTORY**, select **Use existing directory**.</span></span> <span data-ttu-id="4dadc-128">Selecteer vervolgens **ik ben klaar toobe afgemeld**, en selecteer **Complete** ![voltooien pictogram](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="4dadc-128">Then select **I am ready toobe signed out now**, and select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Schermafbeelding van de 'Bestaande directory gebruiken'](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. <span data-ttu-id="4dadc-130">Nadat u bent afgemeld, meld u aan met referenties Hallo globale beheerder van uw Office 365-tenant.</span><span class="sxs-lookup"><span data-stu-id="4dadc-130">After you are signed out, sign in with hello global administrator’s credentials of your Office 365 tenant.</span></span>
   
    ![Schermopname van Office 365-hoofdbeheerder aanmelden](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. <span data-ttu-id="4dadc-132">Selecteer **gaan**.</span><span class="sxs-lookup"><span data-stu-id="4dadc-132">Select **Continue**.</span></span>
   
    ![Schermopname van verificatie](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. <span data-ttu-id="4dadc-134">Selecteer **nu afmelden**.</span><span class="sxs-lookup"><span data-stu-id="4dadc-134">Select **Sign out now**.</span></span>
   
    ![Schermopname van afmelden](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. <span data-ttu-id="4dadc-136">Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com/) met beheerdersreferenties Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="4dadc-136">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with hello service administrator credentials.</span></span>
   
    ![Schermopname van Azure-aanmeldingspagina](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. <span data-ttu-id="4dadc-138">U ziet uw Office 365-tenant in Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="4dadc-138">You should see your Office 365 tenant in hello dashboard.</span></span>
   
    ![Schermopname van dashboard](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <span data-ttu-id="4dadc-140"><a name="Step2"></a>Stap 2: Hallo-map die is gekoppeld aan hello Azure-abonnement wijzigen</span><span class="sxs-lookup"><span data-stu-id="4dadc-140"><a name="Step2"></a>Step 2: Change hello directory associated with hello Azure subscription</span></span>
   
1. <span data-ttu-id="4dadc-141">Selecteer **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="4dadc-141">Select **Settings**.</span></span>
   
    ![Schermopname van Azure classic portal Instellingenpictogram](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. <span data-ttu-id="4dadc-143">Selecteer uw Azure-abonnement en selecteer vervolgens **DIRECTORY bewerken**.</span><span class="sxs-lookup"><span data-stu-id="4dadc-143">Select your Azure subscription, and then select **EDIT DIRECTORY**.</span></span>

    ![Schermopname van Azure-abonnement bewerken directory](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. <span data-ttu-id="4dadc-145">Selecteer **volgende** ![volgende pictogram](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span><span class="sxs-lookup"><span data-stu-id="4dadc-145">Select **Next** ![Next icon](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span></span>
   
    ![Schermopname van het "Wijziging hello gekoppeld directory"](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. <span data-ttu-id="4dadc-147">Bekijk Hallo van invloed op een accounts.</span><span class="sxs-lookup"><span data-stu-id="4dadc-147">Review hello affected accounts.</span></span> <span data-ttu-id="4dadc-148">Alle medebeheerders en [op rollen gebaseerde toegangsbeheer (RBAC)](../active-directory/role-based-access-control-configure.md) gebruikers toegewezen toegang in Hallo bestaande resourcegroepen worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="4dadc-148">All co-administrators and [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) users with assigned access in hello existing resource groups are removed.</span></span> <span data-ttu-id="4dadc-149">Hallo waarschuwing verschijnt noemt alleen Hallo verwijderen van medebeheerders.</span><span class="sxs-lookup"><span data-stu-id="4dadc-149">hello warning you receive only mentions hello removal of co-administrators.</span></span>
      
    ![Schermafbeelding van Hallo medebeheerder accounts toobe verwijderd.](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![Schermafbeelding van een voorbeeld van de gebruiker account toobe verwijderd.](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. <span data-ttu-id="4dadc-152">Selecteer **Complete** ![voltooien pictogram](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="4dadc-152">Select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-toohello-azure-active-directory-tenant"></a><span data-ttu-id="4dadc-153">Stap 3: Uw organisatie Office 365-accounts toevoegen als medebeheerders toohello Azure Active Directory-tenant</span><span class="sxs-lookup"><span data-stu-id="4dadc-153">Step 3: Add your Office 365 organizational accounts as co-administrators toohello Azure Active Directory tenant</span></span>
   
1. <span data-ttu-id="4dadc-154">Selecteer Hallo **beheerders** tabblad en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4dadc-154">Select hello **ADMINISTRATORS** tab, and then select **ADD**.</span></span>
   
    ![Tabblad beheerders van schermopname van Azure classic portal-instellingen](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. <span data-ttu-id="4dadc-156">Een organisatie-account van uw Office 365-tenant, hello Azure-abonnement selecteren, en selecteer vervolgens **Complete** ![voltooien pictogram](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="4dadc-156">Enter an organizational account of your Office 365 tenant, select hello Azure subscription, and then select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Schermopname van Azure toevoegen medebeheerder dialoogvenster](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. <span data-ttu-id="4dadc-158">Ga terug toohello **beheerders** tabblad. U ziet Hallo organisatie-account wordt weergegeven als medebeheerder.</span><span class="sxs-lookup"><span data-stu-id="4dadc-158">Go back toohello **ADMINISTRATORS** tab. You should see hello organizational account displayed as co-administrator.</span></span>
   
    ![Schermafbeelding van tabblad beheerders](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  <span data-ttu-id="4dadc-160">Test toegang tooAzure met Hallo mede administrator-account.</span><span class="sxs-lookup"><span data-stu-id="4dadc-160">Test access tooAzure with hello co-administrator account.</span></span>
   
    <span data-ttu-id="4dadc-161">a.</span><span class="sxs-lookup"><span data-stu-id="4dadc-161">a.</span></span> <span data-ttu-id="4dadc-162">Meld u af bij Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4dadc-162">Sign out of hello Azure classic portal.</span></span>
   
    <span data-ttu-id="4dadc-163">b.</span><span class="sxs-lookup"><span data-stu-id="4dadc-163">b.</span></span> <span data-ttu-id="4dadc-164">Open Hallo [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4dadc-164">Open hello [Azure portal](https://portal.azure.com/).</span></span>
   
    <span data-ttu-id="4dadc-165">c.</span><span class="sxs-lookup"><span data-stu-id="4dadc-165">c.</span></span> <span data-ttu-id="4dadc-166">Geef referenties op Hallo van Hallo medebeheerder en selecteer vervolgens **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="4dadc-166">Enter hello credentials of hello co-administrator, and then select **Sign in**.</span></span>
   
    ![Schermopname van Azure-aanmeldingspagina](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a><span data-ttu-id="4dadc-168">Hulp nodig?</span><span class="sxs-lookup"><span data-stu-id="4dadc-168">Need help?</span></span> <span data-ttu-id="4dadc-169">Neem contact op met ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="4dadc-169">Contact support.</span></span>
<span data-ttu-id="4dadc-170">Als u nog hulp nodig hebt, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget uw probleem snel worden opgelost.</span><span class="sxs-lookup"><span data-stu-id="4dadc-170">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>


