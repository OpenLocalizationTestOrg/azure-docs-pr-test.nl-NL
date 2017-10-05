---
title: 'Azure AD Connect-synchronisatie: het wachtwoord voor de AD DS-account wijzigen | Microsoft Docs'
description: Dit document onderwerp beschrijft hoe u Azure AD Connect bijwerken nadat het wachtwoord van het AD DS-account wordt gewijzigd.
services: active-directory
keywords: AD DS-account, Active Directory-account, wachtwoord
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 14e16a238e60ecfeeb3cbf88c3922a79349dcc75
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="changing-the-ad-ds-account-password"></a><span data-ttu-id="73835-104">Het wachtwoord voor de AD DS-account wijzigen</span><span class="sxs-lookup"><span data-stu-id="73835-104">Changing the AD DS account password</span></span>
<span data-ttu-id="73835-105">De AD DS-account verwijst naar het gebruikersaccount dat door Azure AD Connect worden gebruikt om te communiceren met de lokale Active Directory.</span><span class="sxs-lookup"><span data-stu-id="73835-105">The AD DS account refers to the user account used by Azure AD Connect to communicate with on-premises Active Directory.</span></span> <span data-ttu-id="73835-106">Als u het wachtwoord van de AD DS-account wijzigt, moet u Azure AD Connect-synchronisatieservice bijwerken met het nieuwe wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="73835-106">If you change the password of the AD DS account, you must update Azure AD Connect Synchronization Service with the new password.</span></span> <span data-ttu-id="73835-107">Anders wordt de synchronisatie kan niet meer correct synchroniseren met de lokale Active Directory en de volgende fouten optreden:</span><span class="sxs-lookup"><span data-stu-id="73835-107">Otherwise, the Synchronization can no longer synchronize correctly with the on-premises Active Directory and you will encounter the following errors:</span></span>

* <span data-ttu-id="73835-108">In de bewerking Synchronization Service Manager, een importeren of exporteren met on-premises AD mislukt met **Nee-begin-referenties** fout.</span><span class="sxs-lookup"><span data-stu-id="73835-108">In the Synchronization Service Manager, any import or export operation with on-premises AD fails with **no-start-credentials** error.</span></span>

* <span data-ttu-id="73835-109">Onder Windows Logboeken, het logboek voor toepassingsgebeurtenissen bevat een fout opgetreden bij **gebeurtenis-ID 6000** en het bericht **'de beheeragent 'contoso.com' kan niet worden uitgevoerd omdat de referenties ongeldig zijn'**.</span><span class="sxs-lookup"><span data-stu-id="73835-109">Under Windows Event Viewer, the application event log contains an error with **Event ID 6000** and message **'The management agent "contoso.com" failed to run because the credentials were invalid'**.</span></span>


## <a name="how-to-update-the-synchronization-service-with-new-password-for-ad-ds-account"></a><span data-ttu-id="73835-110">Het bijwerken van de synchronisatieservice met een nieuw wachtwoord voor AD DS-account</span><span class="sxs-lookup"><span data-stu-id="73835-110">How to update the Synchronization Service with new password for AD DS account</span></span>
<span data-ttu-id="73835-111">De synchronisatieservice bijwerken met het nieuwe wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="73835-111">To update the Synchronization Service with the new password:</span></span>

1. <span data-ttu-id="73835-112">Synchronization Service Manager (START → Synchronization-Service) starten.</span><span class="sxs-lookup"><span data-stu-id="73835-112">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="73835-113">![Sync-Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="73835-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  

2. <span data-ttu-id="73835-114">Ga naar de **Connectors** tabblad.</span><span class="sxs-lookup"><span data-stu-id="73835-114">Go to the **Connectors** tab.</span></span>

3. <span data-ttu-id="73835-115">Selecteer de **AD-Connector** die overeenkomt met de AD DS-account waarvoor u het wachtwoord is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="73835-115">Select the **AD Connector** that corresponds to the AD DS account for which its password was changed.</span></span>

4. <span data-ttu-id="73835-116">Onder **acties**, selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="73835-116">Under **Actions**, select **Properties**.</span></span>

5. <span data-ttu-id="73835-117">Selecteer in het pop-updialoogvenster **verbinding maken met Active Directory-Forest**:</span><span class="sxs-lookup"><span data-stu-id="73835-117">In the pop-up dialog, select **Connect to Active Directory Forest**:</span></span>

6. <span data-ttu-id="73835-118">Voer het nieuwe wachtwoord van de AD DS-account in de **wachtwoord** textbox.</span><span class="sxs-lookup"><span data-stu-id="73835-118">Enter the new password of the AD DS account in the **Password** textbox.</span></span>

7. <span data-ttu-id="73835-119">Klik op **OK** naar het nieuwe wachtwoord opslaan en sluiten van een pop-upvenster.</span><span class="sxs-lookup"><span data-stu-id="73835-119">Click **OK** to save the new password and close the pop-up dialog.</span></span>

8. <span data-ttu-id="73835-120">Opnieuw opstarten van de Azure AD Connect onder Windows Service Control Manager-synchronisatieservice.</span><span class="sxs-lookup"><span data-stu-id="73835-120">Restart the Azure AD Connect Synchronization Service under Windows Service Control Manager.</span></span> <span data-ttu-id="73835-121">Dit is om ervoor te zorgen dat elke verwijzing naar het oude wachtwoord is verwijderd uit het cachegeheugen.</span><span class="sxs-lookup"><span data-stu-id="73835-121">This is to ensure that any reference to the old password is removed from the memory cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73835-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="73835-122">Next steps</span></span>
<span data-ttu-id="73835-123">**Overzichtsonderwerpen**</span><span class="sxs-lookup"><span data-stu-id="73835-123">**Overview topics**</span></span>

* [<span data-ttu-id="73835-124">Azure AD Connect-synchronisatie: inzicht en synchronisatie aanpassen</span><span class="sxs-lookup"><span data-stu-id="73835-124">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="73835-125">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="73835-125">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
