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
ms.openlocfilehash: 4b6da997f44860dccb2aa2571ce099ab2d0231f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-password-synchronization-to-azure-active-directory-domain-services"></a><span data-ttu-id="cf575-103">Wachtwoordsynchronisatie inschakelen voor Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="cf575-103">Enable password synchronization to Azure Active Directory Domain Services</span></span>
<span data-ttu-id="cf575-104">Tijdens de vorige taken hebt u Azure Active Directory Domain Services ingeschakeld voor uw Azure Active Directory-tenant (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cf575-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="cf575-105">De volgende taak bestaat uit het inschakelen dat referentie-hashes voor NTLM- (NT LAN Manager) en Kerberos-verificatie moeten worden gesynchroniseerd met Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="cf575-105">The next task is to enable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication to Azure AD Domain Services.</span></span> <span data-ttu-id="cf575-106">Wanneer u de referentiesynchronisatie hebt ingesteld, kunnen gebruikers zich bij het beheerde domein aanmelden met hun zakelijke referenties.</span><span class="sxs-lookup"><span data-stu-id="cf575-106">After you've set up credential synchronization, users can sign in to the managed domain with their corporate credentials.</span></span>

<span data-ttu-id="cf575-107">De vereiste stappen voor gebruikersaccounts in de cloud en gebruikersaccounts die worden gesynchroniseerd vanuit uw on-premises map met Azure AD Connect, verschillen.</span><span class="sxs-lookup"><span data-stu-id="cf575-107">The steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span>  <span data-ttu-id="cf575-108">Als uw Azure AD-tenant een combinatie van heeft van cloudgebruikers en gebruikers van uw on-premises AD, moet u beide stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="cf575-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need to perform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="cf575-109">**Cloudgebruikersaccounts**: [synchroniseer de wachtwoorden voor cloudgebruikersaccounts met uw beheerde domein](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="cf575-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts to your managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="cf575-110">**On-premises gebruikersaccounts**: [synchroniseer de wachtwoorden voor gebruikersaccounts die zijn gesynchroniseerd vanuit uw on-premises AD met uw beheerde domein](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="cf575-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD to your managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-to-your-managed-domain-for-cloud-only-user-accounts"></a><span data-ttu-id="cf575-111">Taak 5: wachtwoordsynchronisatie met uw beheerde domein voor cloudgebruikersaccounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="cf575-111">Task 5: enable password synchronization to your managed domain for cloud-only user accounts</span></span>
<span data-ttu-id="cf575-112">Voor de verificatie van gebruikers in het beheerde domein heeft Azure Active Directory Domain Services referentie-hashes nodig in een indeling die geschikt is voor NTLM- en Kerberos-verificatie.</span><span class="sxs-lookup"><span data-stu-id="cf575-112">To authenticate users on the managed domain, Azure Active Directory Domain Services needs credential hashes in a format that's suitable for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="cf575-113">Totdat u Azure Active Directory Domain Services voor uw tenant inschakelt, maakt of bewaart Azure AD geen referentie-hashes in de vereiste indeling voor NTLM- of Kerberos-verificatie.</span><span class="sxs-lookup"><span data-stu-id="cf575-113">Azure AD does not generate or store credential hashes in the format that's required for NTLM or Kerberos authentication, until you enable Azure Active Directory Domain Services for your tenant.</span></span> <span data-ttu-id="cf575-114">Om veiligheidsredenen slaat Azure AD ook geen wachtwoorden op in niet-gecodeerde vorm.</span><span class="sxs-lookup"><span data-stu-id="cf575-114">For obvious security reasons, Azure AD also does not store any password credentials in clear-text form.</span></span> <span data-ttu-id="cf575-115">Azure AD biedt daarom geen manier voor het automatisch genereren van deze NTLM- of Kerberos-referentie-hashes op basis van bestaande referenties van gebruikers.</span><span class="sxs-lookup"><span data-stu-id="cf575-115">Therefore, Azure AD does not have a way to automatically generate these NTLM or Kerberos credential hashes based on users' existing credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="cf575-116">Als uw organisatie gebruikersaccounts in de cloud heeft, moeten gebruikers die Azure Active Directory Domain Services willen gebruiken, hun wachtwoord wijzigen.</span><span class="sxs-lookup"><span data-stu-id="cf575-116">If your organization has cloud-only user accounts, users who need to use Azure Active Directory Domain Services must change their passwords.</span></span> <span data-ttu-id="cf575-117">Een cloudgebruikersaccount is een account dat is gemaakt in uw Azure AD-directory via de Azure portal of Azure AD PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="cf575-117">A cloud-only user account is an account that was created in your Azure AD directory using either the Azure portal or Azure AD PowerShell cmdlets.</span></span> <span data-ttu-id="cf575-118">Deze gebruikersaccounts zijn niet gesynchroniseerd vanuit een on-premises map.</span><span class="sxs-lookup"><span data-stu-id="cf575-118">Such user accounts aren't synchronized from an on-premises directory.</span></span>
>
>

<span data-ttu-id="cf575-119">Door deze wachtwoordwijziging worden de referentie-hashes die door Azure Active Directory Domain Services zijn vereist voor Kerberos- en NTLM-verificatie, gegenereerd in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf575-119">This password change process causes the credential hashes that are required by Azure Active Directory Domain Services for Kerberos and NTLM authentication to be generated in Azure AD.</span></span> <span data-ttu-id="cf575-120">U kunt wachtwoorden laten verlopen voor alle gebruikers in de tenant die Azure Active Directory Domain Services moeten gebruiken of aan de gebruikers doorgeven dat ze hun wachtwoord moeten wijzigen.</span><span class="sxs-lookup"><span data-stu-id="cf575-120">You can either expire the passwords for all users in the tenant who need to use Azure Active Directory Domain Services or instruct them to change their passwords.</span></span>

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a><span data-ttu-id="cf575-121">Het genereren van hashes voor NTLM- en Kerberos-referenties inschakelen voor een cloudgebruikersaccount</span><span class="sxs-lookup"><span data-stu-id="cf575-121">Enable NTLM and Kerberos credential hash generation for a cloud-only user account</span></span>
<span data-ttu-id="cf575-122">Hier vindt u de instructies voor het wijzigen van het wachtwoord die u moet doorgeven aan gebruikers:</span><span class="sxs-lookup"><span data-stu-id="cf575-122">Here are the instructions you need to provide users, so they can change their passwords:</span></span>

1. <span data-ttu-id="cf575-123">Ga naar de pagina [Azure AD-toegangsvenster](http://myapps.microsoft.com) voor uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="cf575-123">Go to the [Azure AD Access Panel](http://myapps.microsoft.com) page for your organization.</span></span>

    ![Open het deelvenster Azure AD Access](./media/active-directory-domain-services-getting-started/access-panel.png)

2. <span data-ttu-id="cf575-125">In de rechterbovenhoek klikt u op uw naam en selecteert u **Profiel** in het menu.</span><span class="sxs-lookup"><span data-stu-id="cf575-125">In the top right corner, click on your name and select **Profile** from the menu.</span></span>

    ![Selecteer het profiel](./media/active-directory-domain-services-getting-started/select-profile.png)

3. <span data-ttu-id="cf575-127">Op de pagina **Profiel** klikt u op **Wachtwoord wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="cf575-127">On the **Profile** page, click on **Change password**.</span></span>

    ![Klik op 'Wachtwoord wijzigen'](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > <span data-ttu-id="cf575-129">Als u de optie **Wachtwoord wijzigen** niet ziet in het venster Toegangsvenster, controleert u of uw organisatie [Wachtwoordbeheer in Azure AD](../active-directory/active-directory-passwords-getting-started.md) heeft geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="cf575-129">If the **Change password** option is not displayed in the Access Panel window, ensure that your organization has configured [password management in Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span></span>
   >
   >
4. <span data-ttu-id="cf575-130">Op de pagina **Wachtwoord wijzigen** typt u uw bestaande (oude) wachtwoord, typt u een nieuw wachtwoord en bevestigt u dit.</span><span class="sxs-lookup"><span data-stu-id="cf575-130">On the **change password** page, type your existing (old) password, type a new password, and then confirm it.</span></span>

    ![Maak een virtueel netwerk voor Azure AD Domain Services.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. <span data-ttu-id="cf575-132">Klik op **Verzenden**.</span><span class="sxs-lookup"><span data-stu-id="cf575-132">Click **submit**.</span></span>

<span data-ttu-id="cf575-133">Een paar minuten nadat u uw wachtwoord hebt gewijzigd, kunt u het nieuwe wachtwoord gebruiken in Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="cf575-133">A few minutes after you have changed your password, the new password is usable in Azure Active Directory Domain Services.</span></span> <span data-ttu-id="cf575-134">Na ongeveer 20 minuten kunt u zich met uw gewijzigde wachtwoord aanmelden bij computers die zijn gekoppeld aan het beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="cf575-134">After a few more minutes (typically, about 20 minutes), you can sign in to computers that are joined to the managed domain by using the newly changed password.</span></span>

## <a name="related-content"></a><span data-ttu-id="cf575-135">Gerelateerde inhoud</span><span class="sxs-lookup"><span data-stu-id="cf575-135">Related Content</span></span>
* [<span data-ttu-id="cf575-136">Uw eigen wachtwoord bijwerken</span><span class="sxs-lookup"><span data-stu-id="cf575-136">How to update your own password</span></span>](../active-directory/active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="cf575-137">Aan de slag met wachtwoordbeheer in Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf575-137">Getting started with Password Management in Azure AD</span></span>](../active-directory/active-directory-passwords-getting-started.md)
* [<span data-ttu-id="cf575-138">Wachtwoordsynchronisatie met Azure Active Directory Domain Services inschakelen voor een gesynchroniseerde Azure AD-tenant</span><span class="sxs-lookup"><span data-stu-id="cf575-138">Enable password synchronization to Azure Active Directory Domain Services for a synced Azure AD tenant</span></span>](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [<span data-ttu-id="cf575-139">Een beheerd domein van Azure Active Directory Domain Services beheren</span><span class="sxs-lookup"><span data-stu-id="cf575-139">Administer an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="cf575-140">Een virtuele Windows-computer toevoegen aan een beheerd domein van Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="cf575-140">Join a Windows virtual machine to an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="cf575-141">Een virtuele Red Hat Enterprise Linux-computer toevoegen aan een beheerd domein van Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="cf575-141">Join a Red Hat Enterprise Linux virtual machine to an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
