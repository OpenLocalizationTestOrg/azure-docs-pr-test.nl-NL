---
title: 'Azure AD Connect-synchronisatie: hoe toomanage hello Azure AD-serviceaccount | Microsoft Docs'
description: In dit onderwerp wordt beschreven hoe toorestore hello Azure AD-serviceaccount.
services: active-directory
keywords: AADSTS70002, AADSTS50054, hello hoe tooreset Hallo wachtwoord voor Azure AD Connect-synchronisatie Connector-serviceaccount
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 6077043a-27f1-4304-a44b-81dc46620f24
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e563518eae173de42a1d40bb5a76e63f29f9da42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomanage-hello-azure-ad-service-account"></a><span data-ttu-id="a6628-104">Azure AD Connect-synchronisatie: hoe toomanage hello Azure AD-serviceaccount</span><span class="sxs-lookup"><span data-stu-id="a6628-104">Azure AD Connect sync: How toomanage hello Azure AD service account</span></span>
<span data-ttu-id="a6628-105">Hallo-serviceaccount die wordt gebruikt door hello Azure AD-Connector moet toobe service gratis.</span><span class="sxs-lookup"><span data-stu-id="a6628-105">hello service account used by hello Azure AD Connector is supposed toobe service free.</span></span> <span data-ttu-id="a6628-106">Als u tooreset de referenties moet, wordt de in dit onderwerp voor u.</span><span class="sxs-lookup"><span data-stu-id="a6628-106">If you need tooreset its credentials, then this topic is for you.</span></span> <span data-ttu-id="a6628-107">Bijvoorbeeld, als een globale beheerder heeft door fout-wachtwoord opnieuw instellen Hallo Hallo serviceaccount met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a6628-107">For example, if a Global Administrator has by mistake reset hello password on hello service account using PowerShell.</span></span>

## <a name="reset-hello-credentials"></a><span data-ttu-id="a6628-108">Hallo referenties opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="a6628-108">Reset hello credentials</span></span>
<span data-ttu-id="a6628-109">Als het Hallo-serviceaccount is gedefinieerd op Hallo Azure AD-Connector geen contact met Azure AD vanwege problemen met tooauthentication, Hallo wachtwoord opnieuw kan worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a6628-109">If hello service account defined on hello Azure AD Connector cannot contact Azure AD due tooauthentication problems, hello password can be reset.</span></span>

1. <span data-ttu-id="a6628-110">Meld u aan toohello Azure AD Connect sync-server en start PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a6628-110">Sign in toohello Azure AD Connect sync server and start PowerShell.</span></span>
2. <span data-ttu-id="a6628-111">Voer `Add-ADSyncAADServiceAccount` uit.</span><span class="sxs-lookup"><span data-stu-id="a6628-111">Run `Add-ADSyncAADServiceAccount`.</span></span>  
   <span data-ttu-id="a6628-112">![PowerShell-cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span><span class="sxs-lookup"><span data-stu-id="a6628-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span></span>
3. <span data-ttu-id="a6628-113">Geef referenties op globale beheerder Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6628-113">Provide Azure AD Global admin credentials.</span></span>

<span data-ttu-id="a6628-114">Deze cmdlet Hallo wachtwoord voor serviceaccount Hallo opnieuw instellen en in Azure AD en in de synchronisatie-engine Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="a6628-114">This cmdlet resets hello password for hello service account and update it both in Azure AD and in hello sync engine.</span></span>

## <a name="known-issues-these-steps-can-solve"></a><span data-ttu-id="a6628-115">Bekende problemen met die deze stappen kunnen worden opgelost</span><span class="sxs-lookup"><span data-stu-id="a6628-115">Known issues these steps can solve</span></span>
<span data-ttu-id="a6628-116">Deze sectie is een lijst met fouten die zijn gerapporteerd door klanten die door een gebruikersreferenties instellen op Hallo Azure AD-serviceaccount zijn opgelost.</span><span class="sxs-lookup"><span data-stu-id="a6628-116">This section is a list of errors reported by customers that were fixed by a credentials reset on hello Azure AD service account.</span></span>

- - -
<span data-ttu-id="a6628-117">Gebeurtenis 6900</span><span class="sxs-lookup"><span data-stu-id="a6628-117">Event 6900</span></span>  
<span data-ttu-id="a6628-118">Hallo-server een onverwachte fout opgetreden tijdens het verwerken van een wijzigingsmelding wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="a6628-118">hello server encountered an unexpected error while processing a password change notification:</span></span>  
<span data-ttu-id="a6628-119">AADSTS70002: Fout bij valideren referenties.</span><span class="sxs-lookup"><span data-stu-id="a6628-119">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="a6628-120">AADSTS50054: Oude wachtwoord wordt gebruikt voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="a6628-120">AADSTS50054: Old password is used for authentication.</span></span>

- - -
<span data-ttu-id="a6628-121">Gebeurtenis 659</span><span class="sxs-lookup"><span data-stu-id="a6628-121">Event 659</span></span>  
<span data-ttu-id="a6628-122">Fout bij het ophalen van wachtwoord-beleidsconfiguratie synchronisatie.</span><span class="sxs-lookup"><span data-stu-id="a6628-122">Error while retrieving password policy sync configuration.</span></span> <span data-ttu-id="a6628-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span><span class="sxs-lookup"><span data-stu-id="a6628-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span></span>  
<span data-ttu-id="a6628-124">AADSTS70002: Fout bij valideren referenties.</span><span class="sxs-lookup"><span data-stu-id="a6628-124">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="a6628-125">AADSTS50054: Oude wachtwoord wordt gebruikt voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="a6628-125">AADSTS50054: Old password is used for authentication.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6628-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a6628-126">Next steps</span></span>
<span data-ttu-id="a6628-127">**Overzichtsonderwerpen**</span><span class="sxs-lookup"><span data-stu-id="a6628-127">**Overview topics**</span></span>

* [<span data-ttu-id="a6628-128">Azure AD Connect-synchronisatie: inzicht en synchronisatie aanpassen</span><span class="sxs-lookup"><span data-stu-id="a6628-128">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="a6628-129">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a6628-129">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

