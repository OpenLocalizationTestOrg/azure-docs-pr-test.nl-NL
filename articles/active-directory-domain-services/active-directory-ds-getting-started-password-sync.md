---
title: 'Azure Active Directory Domain Services: wachtwoordsynchronisatie inschakelen | Microsoft Docs'
description: Aan de slag met Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 5a32a0df-a3ca-4ebe-b980-91f58f8030fc
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 8e073df9de2996f5ad159dda746881c014ea3d66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a><span data-ttu-id="9675b-103">Wachtwoord synchronisatie tooAzure Active Directory Domain Services inschakelen</span><span class="sxs-lookup"><span data-stu-id="9675b-103">Enable password synchronization tooAzure Active Directory Domain Services</span></span>
<span data-ttu-id="9675b-104">Tijdens de vorige taken hebt u Azure Active Directory Domain Services ingeschakeld voor uw Azure Active Directory-tenant (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9675b-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="9675b-105">de volgende taak Hallo is tooenable synchronisatie van referentie-hashes die vereist zijn voor NT LAN Manager (NTLM) en Kerberos-verificatie tooAzure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="9675b-105">hello next task is tooenable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication tooAzure AD Domain Services.</span></span> <span data-ttu-id="9675b-106">Nadat u een referentie-synchronisatie hebt ingesteld, kunnen gebruikers zich aanmelden in toohello beheerde domein met hun bedrijfsreferenties.</span><span class="sxs-lookup"><span data-stu-id="9675b-106">After you've set up credential synchronization, users can sign in toohello managed domain with their corporate credentials.</span></span>

<span data-ttu-id="9675b-107">Hallo stappen die nodig zijn verschillend voor de gebruiker alleen in de cloud accounts tegenover gebruikersaccounts die worden gesynchroniseerd vanuit uw lokale directory met Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="9675b-107">hello steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span>  <span data-ttu-id="9675b-108">Als uw Azure AD-tenant een combinatie van heeft cloud alleen gebruikers en gebruikers van uw on-premises AD, moet u tooperform na beide stappen.</span><span class="sxs-lookup"><span data-stu-id="9675b-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need tooperform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="9675b-109">**Alleen in de cloud gebruikersaccounts**: [wachtwoorden synchroniseren voor alleen in de cloud gebruikersaccounts tooyour beheerd domein](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="9675b-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts tooyour managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="9675b-110">**Lokale gebruikersaccounts**: [wachtwoorden synchroniseren voor gebruikersaccounts die zijn gesynchroniseerd vanuit uw on-premises AD tooyour beheerd domein](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="9675b-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD tooyour managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-cloud-only-user-accounts"></a><span data-ttu-id="9675b-111">Taak 5: wachtwoord synchronisatie tooyour beheerd domein voor gebruikersaccounts die alleen in de cloud inschakelen</span><span class="sxs-lookup"><span data-stu-id="9675b-111">Task 5: enable password synchronization tooyour managed domain for cloud-only user accounts</span></span>
<span data-ttu-id="9675b-112">gebruikers op Hallo tooauthenticate beheerd domein, Azure Active Directory Domain Services moet referentie-hashes in een indeling die geschikt is voor NTLM en Kerberos-verificatie.</span><span class="sxs-lookup"><span data-stu-id="9675b-112">tooauthenticate users on hello managed domain, Azure Active Directory Domain Services needs credential hashes in a format that's suitable for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="9675b-113">Azure AD niet genereren of opslaan van de referentie-hashes Hallo-indeling die is vereist voor NTLM of Kerberos-verificatie, totdat u Azure Active Directory Domain Services voor uw tenant inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9675b-113">Azure AD does not generate or store credential hashes in hello format that's required for NTLM or Kerberos authentication, until you enable Azure Active Directory Domain Services for your tenant.</span></span> <span data-ttu-id="9675b-114">Om veiligheidsredenen slaat Azure AD ook geen wachtwoorden op in niet-gecodeerde vorm.</span><span class="sxs-lookup"><span data-stu-id="9675b-114">For obvious security reasons, Azure AD also does not store any password credentials in clear-text form.</span></span> <span data-ttu-id="9675b-115">Azure AD heeft dus geen een manier tooautomatically deze op basis van bestaande referenties van gebruikers NTLM of Kerberos-referentie-hashes te genereren.</span><span class="sxs-lookup"><span data-stu-id="9675b-115">Therefore, Azure AD does not have a way tooautomatically generate these NTLM or Kerberos credential hashes based on users' existing credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="9675b-116">Als uw organisatie alleen in de cloud gebruikersaccounts heeft, kunnen gebruikers hoeven toouse Azure Active Directory Domain Services hun wachtwoord moeten wijzigen.</span><span class="sxs-lookup"><span data-stu-id="9675b-116">If your organization has cloud-only user accounts, users who need toouse Azure Active Directory Domain Services must change their passwords.</span></span> <span data-ttu-id="9675b-117">Een alleen-gebruikersaccount is een account dat is gemaakt in uw Azure AD-directory hello Azure-portal of Azure AD PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="9675b-117">A cloud-only user account is an account that was created in your Azure AD directory using either hello Azure portal or Azure AD PowerShell cmdlets.</span></span> <span data-ttu-id="9675b-118">Deze gebruikersaccounts zijn niet gesynchroniseerd vanuit een on-premises map.</span><span class="sxs-lookup"><span data-stu-id="9675b-118">Such user accounts aren't synchronized from an on-premises directory.</span></span>
>
>

<span data-ttu-id="9675b-119">Deze wachtwoordwijziging worden Hallo referentie hashes die voor Azure Active Directory Domain Services voor Kerberos en NTLM-verificatie toobe gegenereerd in Azure AD vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="9675b-119">This password change process causes hello credential hashes that are required by Azure Active Directory Domain Services for Kerberos and NTLM authentication toobe generated in Azure AD.</span></span> <span data-ttu-id="9675b-120">U kunt wachtwoorden laten verlopen Hallo voor alle gebruikers in Hallo tenant die toouse Azure Active Directory Domain Services moeten of ze toochange moeten hun wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="9675b-120">You can either expire hello passwords for all users in hello tenant who need toouse Azure Active Directory Domain Services or instruct them toochange their passwords.</span></span>

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a><span data-ttu-id="9675b-121">Het genereren van hashes voor NTLM- en Kerberos-referenties inschakelen voor een cloudgebruikersaccount</span><span class="sxs-lookup"><span data-stu-id="9675b-121">Enable NTLM and Kerberos credential hash generation for a cloud-only user account</span></span>
<span data-ttu-id="9675b-122">Hier volgen Hallo instructies, moet u tooprovide gebruikers, zodat ze kunnen hun wachtwoord wijzigen:</span><span class="sxs-lookup"><span data-stu-id="9675b-122">Here are hello instructions you need tooprovide users, so they can change their passwords:</span></span>

1. <span data-ttu-id="9675b-123">Ga toohello [Azure AD-Toegangsvenster](http://myapps.microsoft.com) pagina voor uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="9675b-123">Go toohello [Azure AD Access Panel](http://myapps.microsoft.com) page for your organization.</span></span>

    ![Hello Azure AD-Toegangsvenster starten](./media/active-directory-domain-services-getting-started/access-panel.png)

2. <span data-ttu-id="9675b-125">Klik op de naam van uw in Hallo rechterbovenhoek, en selecteer **profiel** in Hallo-menu.</span><span class="sxs-lookup"><span data-stu-id="9675b-125">In hello top right corner, click on your name and select **Profile** from hello menu.</span></span>

    ![Selecteer het profiel](./media/active-directory-domain-services-getting-started/select-profile.png)

3. <span data-ttu-id="9675b-127">Op Hallo **profiel** pagina, klikt u op **wachtwoord wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="9675b-127">On hello **Profile** page, click on **Change password**.</span></span>

    ![Klik op 'Wachtwoord wijzigen'](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > <span data-ttu-id="9675b-129">Als hello **wachtwoord wijzigen** optie niet wordt weergegeven in Hallo Toegangsvenster venster, zorg ervoor dat uw organisatie heeft geconfigureerd [in Azure AD-wachtwoordbeheer](../active-directory/active-directory-passwords-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="9675b-129">If hello **Change password** option is not displayed in hello Access Panel window, ensure that your organization has configured [password management in Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span></span>
   >
   >
4. <span data-ttu-id="9675b-130">Op Hallo **wachtwoord wijzigen** pagina, typt u uw bestaande (oude) wachtwoord, typt u een nieuw wachtwoord en Bevestig het.</span><span class="sxs-lookup"><span data-stu-id="9675b-130">On hello **change password** page, type your existing (old) password, type a new password, and then confirm it.</span></span>

    ![Maak een virtueel netwerk voor Azure AD Domain Services.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. <span data-ttu-id="9675b-132">Klik op **Verzenden**.</span><span class="sxs-lookup"><span data-stu-id="9675b-132">Click **submit**.</span></span>

<span data-ttu-id="9675b-133">Een paar minuten nadat u uw wachtwoord hebt gewijzigd is Hallo nieuwe wachtwoord gebruikt in Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="9675b-133">A few minutes after you have changed your password, hello new password is usable in Azure Active Directory Domain Services.</span></span> <span data-ttu-id="9675b-134">Na enkele minuten (meestal ongeveer 20 minuten), kunt u toocomputers die gekoppeld toohello beheerd domein zijn via Hallo zojuist gewijzigd wachtwoord aanmelden.</span><span class="sxs-lookup"><span data-stu-id="9675b-134">After a few more minutes (typically, about 20 minutes), you can sign in toocomputers that are joined toohello managed domain by using hello newly changed password.</span></span>

## <a name="related-content"></a><span data-ttu-id="9675b-135">Gerelateerde inhoud</span><span class="sxs-lookup"><span data-stu-id="9675b-135">Related Content</span></span>
* [<span data-ttu-id="9675b-136">Hoe tooupdate uw eigen wachtwoord</span><span class="sxs-lookup"><span data-stu-id="9675b-136">How tooupdate your own password</span></span>](../active-directory/active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="9675b-137">Aan de slag met wachtwoordbeheer in Azure AD</span><span class="sxs-lookup"><span data-stu-id="9675b-137">Getting started with Password Management in Azure AD</span></span>](../active-directory/active-directory-passwords-getting-started.md)
* [<span data-ttu-id="9675b-138">Wachtwoordsynchronisatie inschakelen tooAzure Active Directory Domain Services voor een gesynchroniseerde Azure AD-tenant</span><span class="sxs-lookup"><span data-stu-id="9675b-138">Enable password synchronization tooAzure Active Directory Domain Services for a synced Azure AD tenant</span></span>](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [<span data-ttu-id="9675b-139">Een beheerd domein van Azure Active Directory Domain Services beheren</span><span class="sxs-lookup"><span data-stu-id="9675b-139">Administer an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="9675b-140">Lid worden van een Windows virtuele machine tooan Azure Active Directory Domain Services beheerd domein</span><span class="sxs-lookup"><span data-stu-id="9675b-140">Join a Windows virtual machine tooan Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="9675b-141">Lid worden van een Red Hat Enterprise Linux virtuele machine tooan Azure Active Directory Domain Services beheerd domein</span><span class="sxs-lookup"><span data-stu-id="9675b-141">Join a Red Hat Enterprise Linux virtual machine tooan Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
