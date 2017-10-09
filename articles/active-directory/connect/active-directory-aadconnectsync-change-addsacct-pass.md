---
title: 'Azure AD Connect-synchronisatie: veranderende Hallo AD DS-accountwachtwoord | Microsoft Docs'
description: Dit document onderwerp beschrijft hoe tooupdate Azure AD Connect na het wachtwoord op Hallo van Hallo AD DS-account wordt gewijzigd.
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
ms.openlocfilehash: 2707c9246446612f8d083ecde876b3b4fb2435ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-ad-ds-account-password"></a><span data-ttu-id="a29fa-104">Hallo AD DS accountwachtwoord wijzigen</span><span class="sxs-lookup"><span data-stu-id="a29fa-104">Changing hello AD DS account password</span></span>
<span data-ttu-id="a29fa-105">Hallo AD DS-account verwijst toohello gebruikersaccount gebruikt door Azure AD Connect toocommunicate met lokale Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a29fa-105">hello AD DS account refers toohello user account used by Azure AD Connect toocommunicate with on-premises Active Directory.</span></span> <span data-ttu-id="a29fa-106">Als u een wachtwoord op Hallo van Hallo AD DS-account wijzigt, moet u Azure AD Connect-synchronisatieservice bijwerken met het nieuwe wachtwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="a29fa-106">If you change hello password of hello AD DS account, you must update Azure AD Connect Synchronization Service with hello new password.</span></span> <span data-ttu-id="a29fa-107">Anders Hallo die synchronisatie niet meer correct met Hallo synchroniseren kan on-premises Active Directory en u tegenkomt Hallo volgende fouten:</span><span class="sxs-lookup"><span data-stu-id="a29fa-107">Otherwise, hello Synchronization can no longer synchronize correctly with hello on-premises Active Directory and you will encounter hello following errors:</span></span>

* <span data-ttu-id="a29fa-108">In Hallo Synchronization Service Manager, een importeren of exporteren bewerking met de lokale AD mislukt **Nee-begin-referenties** fout.</span><span class="sxs-lookup"><span data-stu-id="a29fa-108">In hello Synchronization Service Manager, any import or export operation with on-premises AD fails with **no-start-credentials** error.</span></span>

* <span data-ttu-id="a29fa-109">Onder de functie Logboeken van Windows hello toepassingslogboek bevat een fout opgetreden bij **gebeurtenis-ID 6000** en het bericht **'hello beheeragent 'contoso.com' mislukte toorun omdat Hallo referenties ongeldig zijn'** .</span><span class="sxs-lookup"><span data-stu-id="a29fa-109">Under Windows Event Viewer, hello application event log contains an error with **Event ID 6000** and message **'hello management agent "contoso.com" failed toorun because hello credentials were invalid'**.</span></span>


## <a name="how-tooupdate-hello-synchronization-service-with-new-password-for-ad-ds-account"></a><span data-ttu-id="a29fa-110">Hoe tooupdate synchronisatieservice Hallo met een nieuw wachtwoord voor AD DS-account</span><span class="sxs-lookup"><span data-stu-id="a29fa-110">How tooupdate hello Synchronization Service with new password for AD DS account</span></span>
<span data-ttu-id="a29fa-111">tooupdate hello Synchronization Service met het nieuwe wachtwoord Hallo:</span><span class="sxs-lookup"><span data-stu-id="a29fa-111">tooupdate hello Synchronization Service with hello new password:</span></span>

1. <span data-ttu-id="a29fa-112">Hallo Synchronization Service Manager (START → Synchronization Service) starten.</span><span class="sxs-lookup"><span data-stu-id="a29fa-112">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="a29fa-113">![Sync-Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="a29fa-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  

2. <span data-ttu-id="a29fa-114">Ga toohello **Connectors** tabblad.</span><span class="sxs-lookup"><span data-stu-id="a29fa-114">Go toohello **Connectors** tab.</span></span>

3. <span data-ttu-id="a29fa-115">Selecteer Hallo **AD-Connector** die overeenkomt met toohello AD DS-account waarvoor u het wachtwoord is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="a29fa-115">Select hello **AD Connector** that corresponds toohello AD DS account for which its password was changed.</span></span>

4. <span data-ttu-id="a29fa-116">Onder **acties**, selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="a29fa-116">Under **Actions**, select **Properties**.</span></span>

5. <span data-ttu-id="a29fa-117">Selecteer in het pop-upvenster hello, **tooActive Directory-Forest verbinding**:</span><span class="sxs-lookup"><span data-stu-id="a29fa-117">In hello pop-up dialog, select **Connect tooActive Directory Forest**:</span></span>

6. <span data-ttu-id="a29fa-118">Geef de nieuwe wachtwoord Hallo van Hallo AD DS-account in Hallo **wachtwoord** textbox.</span><span class="sxs-lookup"><span data-stu-id="a29fa-118">Enter hello new password of hello AD DS account in hello **Password** textbox.</span></span>

7. <span data-ttu-id="a29fa-119">Klik op **OK** toosave Hallo nieuw wachtwoord en sluiten Hallo pop-upvenster.</span><span class="sxs-lookup"><span data-stu-id="a29fa-119">Click **OK** toosave hello new password and close hello pop-up dialog.</span></span>

8. <span data-ttu-id="a29fa-120">Opnieuw opstarten hello Azure AD Connect-synchronisatieservice onder Windows Service Control Manager.</span><span class="sxs-lookup"><span data-stu-id="a29fa-120">Restart hello Azure AD Connect Synchronization Service under Windows Service Control Manager.</span></span> <span data-ttu-id="a29fa-121">Dit is tooensure die een verwijzing toohello oude wachtwoord is verwijderd uit cachegeheugen Hallo.</span><span class="sxs-lookup"><span data-stu-id="a29fa-121">This is tooensure that any reference toohello old password is removed from hello memory cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a29fa-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a29fa-122">Next steps</span></span>
<span data-ttu-id="a29fa-123">**Overzichtsonderwerpen**</span><span class="sxs-lookup"><span data-stu-id="a29fa-123">**Overview topics**</span></span>

* [<span data-ttu-id="a29fa-124">Azure AD Connect-synchronisatie: inzicht en synchronisatie aanpassen</span><span class="sxs-lookup"><span data-stu-id="a29fa-124">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="a29fa-125">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a29fa-125">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
