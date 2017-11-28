---
title: aaaTroubleshooting hello automatische registratie van Azure AD-domein voor Windows downlevel-clients computers die lid zijn | Microsoft Docs
description: Het oplossen van problemen Hallo automatische registratie van Azure AD-domein lid zijn van computers voor Windows downlevel-clients.
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
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 84fe666576f13de09d1eaa5692517d45a4dbeebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad-for-windows-down-level-clients"></a><span data-ttu-id="0b9f9-103">Automatische registratie van domein het oplossen van problemen die lid zijn van computers tooAzure AD voor Windows downlevel-clients</span><span class="sxs-lookup"><span data-stu-id="0b9f9-103">Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients</span></span> 

<span data-ttu-id="0b9f9-104">In dit onderwerp is van toepassing alleen toohello volgende clients:</span><span class="sxs-lookup"><span data-stu-id="0b9f9-104">This topic is applicable only toohello following clients:</span></span> 

- <span data-ttu-id="0b9f9-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="0b9f9-105">Windows 7</span></span> 
- <span data-ttu-id="0b9f9-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="0b9f9-106">Windows 8.1</span></span> 
- <span data-ttu-id="0b9f9-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="0b9f9-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="0b9f9-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="0b9f9-108">Windows Server 2012</span></span> 
- <span data-ttu-id="0b9f9-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="0b9f9-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="0b9f9-110">Zie voor Windows 10 of Windows Server 2016 [automatische registratie van domein het oplossen van problemen die lid zijn van computers tooAzure AD – Windows 10 en Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span><span class="sxs-lookup"><span data-stu-id="0b9f9-110">For Windows 10 or Windows Server 2016, see [Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span></span>

<span data-ttu-id="0b9f9-111">Dit onderwerp wordt ervan uitgegaan dat u hebt geconfigureerd automatische registratie van apparaten domein vermelde in dat wordt beschreven in [hoe tooconfigure automatische registratie van Windows-domein apparaten met Azure Active Directory](active-directory-device-registration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0b9f9-111">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md).</span></span>
 
<span data-ttu-id="0b9f9-112">Dit onderwerp vindt u informatie over hoe tooresolve mogelijke problemen op te lossen.</span><span class="sxs-lookup"><span data-stu-id="0b9f9-112">This topic provides you with troubleshooting guidance on how tooresolve potential issues.</span></span>  
<span data-ttu-id="0b9f9-113">Een aantal dingen toonote voor geslaagde resultaten:</span><span class="sxs-lookup"><span data-stu-id="0b9f9-113">Some things toonote for successful outcomes:</span></span> 

- <span data-ttu-id="0b9f9-114">Registratie van deze clients over Azure AD is per gebruiker/apparaat.</span><span class="sxs-lookup"><span data-stu-id="0b9f9-114">Registration of these clients on Azure AD is per user/device.</span></span> <span data-ttu-id="0b9f9-115">Als een voorbeeld: als jdoe en jharnett wilt toothis apparaat aanmelden, de registratie van een afzonderlijke (apparaat-id) voor elk van deze gebruikers in het tabblad info van Hallo gebruiker is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0b9f9-115">As an example: If jdoe and jharnett log in toothis device, a separate registration (DeviceID) is created for each of these users in hello USER info tab.</span></span>  

- <span data-ttu-id="0b9f9-116">De registratie van deze clients out of box Hallo geconfigureerde tootry bij het aanmelden of vergrendelen/ontgrendelen is en kan er 5 minuten vertraging dat dit met behulp van een Task Scheduler-taak wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="0b9f9-116">Registration of these clients out of hello box is configured tootry at either logon or lock/unlock and there could be 5-minute delay that this is triggered using a Task Scheduler task.</span></span> 

- <span data-ttu-id="0b9f9-117">Een opnieuw installeren van het besturingssysteem hello of een handmatige opheffen van de registratie en opnieuw te registreren, kan een nieuwe registratie maakt op Azure AD en resulteert in meerdere vermeldingen Hallo gebruiker info tabblad in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="0b9f9-117">A re-install of hello operating system or a manual un-register and re-register may create a new registration on Azure AD and will result in multiple entries under hello USER info tab in hello Azure portal.</span></span> 


## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="0b9f9-118">Stap 1: De registratiestatus Hallo ophalen</span><span class="sxs-lookup"><span data-stu-id="0b9f9-118">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="0b9f9-119">**tooverify hello registratiestatus:**</span><span class="sxs-lookup"><span data-stu-id="0b9f9-119">**tooverify hello registration status:**</span></span>  

1. <span data-ttu-id="0b9f9-120">Open Hallo opdrachtprompt als beheerder</span><span class="sxs-lookup"><span data-stu-id="0b9f9-120">Open hello command prompt as an administrator</span></span> 

2. <span data-ttu-id="0b9f9-121">Type`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span><span class="sxs-lookup"><span data-stu-id="0b9f9-121">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="0b9f9-122">Met deze opdracht geeft een dialoogvenster waarmee u meer informatie over de status van Hallo join.</span><span class="sxs-lookup"><span data-stu-id="0b9f9-122">This command displays a dialog box that provides you with more details about hello join status.</span></span>

![Werkplekdeelname voor Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-registration-status"></a><span data-ttu-id="0b9f9-124">Stap 2: De registratiestatus Hallo</span><span class="sxs-lookup"><span data-stu-id="0b9f9-124">Step 2: Evaluate hello registration status</span></span> 

<span data-ttu-id="0b9f9-125">Als Hallo join niet geslaagd is, biedt Hallo dialoogvenster u meer informatie over Hallo probleem dat is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="0b9f9-125">If hello join was not successful, hello dialog box provides you with details about hello issue that has occured.</span></span>

<span data-ttu-id="0b9f9-126">**Hallo meest voorkomende problemen zijn:**</span><span class="sxs-lookup"><span data-stu-id="0b9f9-126">**hello most common issues are:**</span></span>

- <span data-ttu-id="0b9f9-127">Een onjuist geconfigureerde AD FS of Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b9f9-127">A misconfigured AD FS or Azure AD</span></span>

    ![Werkplekdeelname voor Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="0b9f9-129">U bent niet aangemeld op als een domeingebruiker</span><span class="sxs-lookup"><span data-stu-id="0b9f9-129">You are not signed on as a domain user</span></span>

    ![Werkplekdeelname voor Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="0b9f9-131">Een quotum is bereikt</span><span class="sxs-lookup"><span data-stu-id="0b9f9-131">A quota has been reached</span></span>

    ![Werkplekdeelname voor Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="0b9f9-133">Hallo-service reageert niet</span><span class="sxs-lookup"><span data-stu-id="0b9f9-133">hello service is not responding</span></span> 

    ![Werkplekdeelname voor Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="0b9f9-135">U kunt ook Hallo statusinformatie vinden in het gebeurtenislogboek Hallo onder **toepassingen en Services Log\Microsoft-Workplace Join**.</span><span class="sxs-lookup"><span data-stu-id="0b9f9-135">You can also find hello status information in hello event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="0b9f9-136">**Hallo meest voorkomende oorzaken van een mislukte inschrijving zijn:**</span><span class="sxs-lookup"><span data-stu-id="0b9f9-136">**hello most common causes for a failed registration are:**</span></span> 

- <span data-ttu-id="0b9f9-137">Uw computer is niet op het interne netwerk van de organisatie van de hello of een VPN zonder verbinding tooan lokale AD-domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="0b9f9-137">Your computer is not on hello organization’s internal network or a VPN without connection tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="0b9f9-138">U bent aangemeld op de computer tooyour met een lokaal computeraccount.</span><span class="sxs-lookup"><span data-stu-id="0b9f9-138">You are logged on tooyour computer with a local computer account.</span></span> 

- <span data-ttu-id="0b9f9-139">Problemen met de configuratie van service:</span><span class="sxs-lookup"><span data-stu-id="0b9f9-139">Service configuration issues:</span></span> 

  - <span data-ttu-id="0b9f9-140">Hallo federation-server is geconfigureerd toosupport **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="0b9f9-140">hello federation server has been configured toosupport **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="0b9f9-141">Er is geen Service Connection Point-object dat tooyour geverifieerde domeinnaam op beheerpunten in Azure AD in Hallo AD-forest waar Hallo computer behoort.</span><span class="sxs-lookup"><span data-stu-id="0b9f9-141">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to.</span></span>

  - <span data-ttu-id="0b9f9-142">Een gebruiker de Hallo heeft bereikt van apparaten.</span><span class="sxs-lookup"><span data-stu-id="0b9f9-142">A user has reached hello limit of devices.</span></span> <span data-ttu-id="0b9f9-143">Zie aan de slag met Azure Active Directory-apparaatregistratie.</span><span class="sxs-lookup"><span data-stu-id="0b9f9-143">Please see Get Started with Azure Active Directory Device Registration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b9f9-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0b9f9-144">Next steps</span></span>

<span data-ttu-id="0b9f9-145">Zie voor meer informatie, Hallo [automatische apparaatregistratie Veelgestelde vragen](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="0b9f9-145">For more information, see hello [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
