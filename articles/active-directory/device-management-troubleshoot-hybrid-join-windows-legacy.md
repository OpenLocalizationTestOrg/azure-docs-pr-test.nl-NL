---
title: aaaTroubleshooting hybride Azure Active Directory die lid zijn van de downlevel-apparaten | Microsoft Docs
description: Het oplossen van hybride Azure Active Directory die lid zijn van downlevel-apparaten.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: edd56b89579fac6b427732902284ad9c568b87b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-down-level-devices"></a><span data-ttu-id="b8d67-103">Het oplossen van hybride Azure Active Directory die lid zijn van downlevel-apparaten</span><span class="sxs-lookup"><span data-stu-id="b8d67-103">Troubleshooting hybrid Azure Active Directory joined down-level devices</span></span> 

<span data-ttu-id="b8d67-104">In dit onderwerp is van toepassing alleen toohello apparaten te volgen:</span><span class="sxs-lookup"><span data-stu-id="b8d67-104">This topic is applicable only toohello following devices:</span></span> 

- <span data-ttu-id="b8d67-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="b8d67-105">Windows 7</span></span> 
- <span data-ttu-id="b8d67-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="b8d67-106">Windows 8.1</span></span> 
- <span data-ttu-id="b8d67-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="b8d67-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="b8d67-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="b8d67-108">Windows Server 2012</span></span> 
- <span data-ttu-id="b8d67-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="b8d67-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="b8d67-110">Zie voor Windows 10 of Windows Server 2016 [probleemoplossing hybride Azure Active Directory die lid zijn van apparaten met Windows 10 en Windows Server 2016](device-management-troubleshoot-hybrid-join-windows-current.md).</span><span class="sxs-lookup"><span data-stu-id="b8d67-110">For Windows 10 or Windows Server 2016, see [Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices](device-management-troubleshoot-hybrid-join-windows-current.md).</span></span>

<span data-ttu-id="b8d67-111">Dit onderwerp wordt ervan uitgegaan dat u hebt [geconfigureerde hybride Azure Active Directory die lid zijn van de apparaten](device-management-hybrid-azuread-joined-devices-setup.md) toosupport Hallo volgen scenario's:</span><span class="sxs-lookup"><span data-stu-id="b8d67-111">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello following scenarios:</span></span>

- <span data-ttu-id="b8d67-112">Voorwaardelijke toegang op basis van apparaten</span><span class="sxs-lookup"><span data-stu-id="b8d67-112">Device-based conditional access</span></span>

- [<span data-ttu-id="b8d67-113">Enterprise-instellingen voor roaming</span><span class="sxs-lookup"><span data-stu-id="b8d67-113">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="b8d67-114">Windows Hello voor Bedrijven</span><span class="sxs-lookup"><span data-stu-id="b8d67-114">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md) 





<span data-ttu-id="b8d67-115">Dit onderwerp vindt u informatie over hoe tooresolve mogelijke problemen op te lossen.</span><span class="sxs-lookup"><span data-stu-id="b8d67-115">This topic provides you with troubleshooting guidance on how tooresolve potential issues.</span></span>  

<span data-ttu-id="b8d67-116">**Wat u moet weten:**</span><span class="sxs-lookup"><span data-stu-id="b8d67-116">**What you should know:**</span></span> 

- <span data-ttu-id="b8d67-117">maximum aantal apparaten per gebruiker Hallo is apparaatgerichte.</span><span class="sxs-lookup"><span data-stu-id="b8d67-117">hello maximum number of devices per user is device-centric.</span></span> <span data-ttu-id="b8d67-118">Bijvoorbeeld, als *jdoe* en *jharnett* tooa aanmelden apparaat, de registratie van een afzonderlijke (DeviceID) wordt gemaakt voor elk van deze in Hallo **gebruiker** tabblad info.</span><span class="sxs-lookup"><span data-stu-id="b8d67-118">For example, if *jdoe* and *jharnett* sign-in tooa device, a separate registration (DeviceID) is created for each of them in hello **USER** info tab.</span></span>  

- <span data-ttu-id="b8d67-119">Hallo initiële registratie / join is van de apparaten geconfigureerde tooperform een poging gedaan bij het aanmelden of vergrendelen / ontgrendelen.</span><span class="sxs-lookup"><span data-stu-id="b8d67-119">hello initial registration / join of devices is configured tooperform an attempt at either logon or lock / unlock.</span></span> <span data-ttu-id="b8d67-120">Er zijn 5 minuten vertraging geactiveerd door een scheduler-taak.</span><span class="sxs-lookup"><span data-stu-id="b8d67-120">There could be 5-minute delay triggered by a task scheduler task.</span></span> 

- <span data-ttu-id="b8d67-121">Opnieuw installeren van Hallo-besturingssysteem of een handmatige unregister en opnieuw te registreren kunnen een nieuwe registratie maakt op Azure AD en resulteert in meerdere vermeldingen Hallo gebruiker info tabblad in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b8d67-121">A reinstall of hello operating system or a manual unregister and re-register may create a new registration on Azure AD and results in multiple entries under hello USER info tab in hello Azure portal.</span></span> 


## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="b8d67-122">Stap 1: De registratiestatus Hallo ophalen</span><span class="sxs-lookup"><span data-stu-id="b8d67-122">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="b8d67-123">**tooverify hello registratiestatus:**</span><span class="sxs-lookup"><span data-stu-id="b8d67-123">**tooverify hello registration status:**</span></span>  

1. <span data-ttu-id="b8d67-124">Open Hallo opdrachtprompt als beheerder</span><span class="sxs-lookup"><span data-stu-id="b8d67-124">Open hello command prompt as an administrator</span></span> 

2. <span data-ttu-id="b8d67-125">Type`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span><span class="sxs-lookup"><span data-stu-id="b8d67-125">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="b8d67-126">Met deze opdracht geeft een dialoogvenster waarmee u meer informatie over de status van Hallo join.</span><span class="sxs-lookup"><span data-stu-id="b8d67-126">This command displays a dialog box that provides you with more details about hello join status.</span></span>

![Werkplekdeelname voor Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-hybrid-azure-ad-join-status"></a><span data-ttu-id="b8d67-128">Stap 2: De Hallo hybride Azure AD join-status</span><span class="sxs-lookup"><span data-stu-id="b8d67-128">Step 2: Evaluate hello hybrid Azure AD join status</span></span> 

<span data-ttu-id="b8d67-129">Als Hallo hybride Azure AD join niet geslaagd is, biedt Hallo dialoogvenster u meer informatie over Hallo probleem dat is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="b8d67-129">If hello hybrid Azure AD join was not successful, hello dialog box provides you with details about hello issue that has occurred.</span></span>

<span data-ttu-id="b8d67-130">**Hallo meest voorkomende problemen zijn:**</span><span class="sxs-lookup"><span data-stu-id="b8d67-130">**hello most common issues are:**</span></span>

- <span data-ttu-id="b8d67-131">Een onjuist geconfigureerde AD FS of Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8d67-131">A misconfigured AD FS or Azure AD</span></span>

    ![Werkplekdeelname voor Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="b8d67-133">U bent niet aangemeld op als een domeingebruiker</span><span class="sxs-lookup"><span data-stu-id="b8d67-133">You are not signed on as a domain user</span></span>

    ![Werkplekdeelname voor Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="b8d67-135">Een quotum is bereikt</span><span class="sxs-lookup"><span data-stu-id="b8d67-135">A quota has been reached</span></span>

    ![Werkplekdeelname voor Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="b8d67-137">Hallo-service reageert niet</span><span class="sxs-lookup"><span data-stu-id="b8d67-137">hello service is not responding</span></span> 

    ![Werkplekdeelname voor Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="b8d67-139">U kunt ook Hallo statusinformatie vinden in het gebeurtenislogboek Hallo onder **toepassingen en Services Log\Microsoft-Workplace Join**.</span><span class="sxs-lookup"><span data-stu-id="b8d67-139">You can also find hello status information in hello event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="b8d67-140">**Hallo meest voorkomende oorzaken van een mislukte hybride Azure AD join zijn:**</span><span class="sxs-lookup"><span data-stu-id="b8d67-140">**hello most common causes for a failed hybrid Azure AD join are:**</span></span> 

- <span data-ttu-id="b8d67-141">Uw computer is niet op het interne netwerk van de organisatie van de hello of een VPN zonder verbinding tooan lokale AD-domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="b8d67-141">Your computer is not on hello organization’s internal network or a VPN without connection tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="b8d67-142">U bent aangemeld op de computer tooyour met een lokaal computeraccount.</span><span class="sxs-lookup"><span data-stu-id="b8d67-142">You are logged on tooyour computer with a local computer account.</span></span> 

- <span data-ttu-id="b8d67-143">Problemen met de configuratie van service:</span><span class="sxs-lookup"><span data-stu-id="b8d67-143">Service configuration issues:</span></span> 

  - <span data-ttu-id="b8d67-144">Hallo federation-server is geconfigureerd toosupport **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="b8d67-144">hello federation server has been configured toosupport **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="b8d67-145">Er is geen Service Connection Point-object dat tooyour geverifieerde domeinnaam op beheerpunten in Azure AD in Hallo AD-forest waar Hallo computer behoort.</span><span class="sxs-lookup"><span data-stu-id="b8d67-145">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to.</span></span>

  - <span data-ttu-id="b8d67-146">Een gebruiker de Hallo heeft bereikt van apparaten.</span><span class="sxs-lookup"><span data-stu-id="b8d67-146">A user has reached hello limit of devices.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b8d67-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b8d67-147">Next steps</span></span>

<span data-ttu-id="b8d67-148">Bekijk voor vragen Hallo [Apparaatbeheer Veelgestelde vragen](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="b8d67-148">For questions, see hello [device management FAQ](device-management-faq.md)</span></span>  
