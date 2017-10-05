---
title: Het oplossen van de automatische registratie van Azure AD-domein aangesloten computers voor downlevel-clients voor Windows | Microsoft Docs
description: Het oplossen van de automatische registratie van Azure AD-domein lid zijn van computers voor Windows downlevel-clients.
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
ms.openlocfilehash: a7c8ef4c59c53c21258f0c61963d8f994a3946ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-to-azure-ad-for-windows-down-level-clients"></a><span data-ttu-id="e27a5-103">Het oplossen van automatische registratie van domein computers toegevoegd aan Azure AD. voor Windows downlevel-clients</span><span class="sxs-lookup"><span data-stu-id="e27a5-103">Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients</span></span> 

<span data-ttu-id="e27a5-104">In dit onderwerp is alleen van toepassing op de volgende clients:</span><span class="sxs-lookup"><span data-stu-id="e27a5-104">This topic is applicable only to the following clients:</span></span> 

- <span data-ttu-id="e27a5-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="e27a5-105">Windows 7</span></span> 
- <span data-ttu-id="e27a5-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="e27a5-106">Windows 8.1</span></span> 
- <span data-ttu-id="e27a5-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="e27a5-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="e27a5-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="e27a5-108">Windows Server 2012</span></span> 
- <span data-ttu-id="e27a5-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="e27a5-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="e27a5-110">Zie voor Windows 10 of Windows Server 2016 [computers probleemoplossing automatische registratie van domein worden toegevoegd aan Azure AD. – Windows 10 en Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span><span class="sxs-lookup"><span data-stu-id="e27a5-110">For Windows 10 or Windows Server 2016, see [Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span></span>

<span data-ttu-id="e27a5-111">Dit onderwerp wordt ervan uitgegaan dat u hebt geconfigureerd automatische registratie van apparaten domein vermelde in dat wordt beschreven in [automatische registratie van Windows-domein-apparaten met Azure Active Directory configureren](active-directory-device-registration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e27a5-111">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md).</span></span>
 
<span data-ttu-id="e27a5-112">Dit onderwerp vindt u richtlijnen over het oplossen van problemen op te lossen.</span><span class="sxs-lookup"><span data-stu-id="e27a5-112">This topic provides you with troubleshooting guidance on how to resolve potential issues.</span></span>  
<span data-ttu-id="e27a5-113">Een aantal zaken om aan te geven voor geslaagde resultaten:</span><span class="sxs-lookup"><span data-stu-id="e27a5-113">Some things to note for successful outcomes:</span></span> 

- <span data-ttu-id="e27a5-114">Registratie van deze clients over Azure AD is per gebruiker/apparaat.</span><span class="sxs-lookup"><span data-stu-id="e27a5-114">Registration of these clients on Azure AD is per user/device.</span></span> <span data-ttu-id="e27a5-115">Als een voorbeeld: als jdoe en jharnett moet u zich bij dit apparaat aanmelden, de registratie van een afzonderlijke (DeviceID) wordt gemaakt voor elk van deze gebruikers in het tabblad gebruiker info.</span><span class="sxs-lookup"><span data-stu-id="e27a5-115">As an example: If jdoe and jharnett log in to this device, a separate registration (DeviceID) is created for each of these users in the USER info tab.</span></span>  

- <span data-ttu-id="e27a5-116">De registratie van deze clients buiten het vak is geconfigureerd om te proberen bij het aanmelden of vergrendelen/ontgrendelen en kan er 5 minuten vertraging dat dit met behulp van een Task Scheduler-taak wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="e27a5-116">Registration of these clients out of the box is configured to try at either logon or lock/unlock and there could be 5-minute delay that this is triggered using a Task Scheduler task.</span></span> 

- <span data-ttu-id="e27a5-117">Een opnieuw installeren van het besturingssysteem of een handmatige opheffen van de registratie en opnieuw te registreren, kan een nieuwe registratie maakt op Azure AD en resulteert in meerdere vermeldingen op het tabblad gebruikers gegevens in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e27a5-117">A re-install of the operating system or a manual un-register and re-register may create a new registration on Azure AD and will result in multiple entries under the USER info tab in the Azure portal.</span></span> 


## <a name="step-1-retrieve-the-registration-status"></a><span data-ttu-id="e27a5-118">Stap 1: De registratiestatus ophalen</span><span class="sxs-lookup"><span data-stu-id="e27a5-118">Step 1: Retrieve the registration status</span></span> 

<span data-ttu-id="e27a5-119">**De registratiestatus controleren:**</span><span class="sxs-lookup"><span data-stu-id="e27a5-119">**To verify the registration status:**</span></span>  

1. <span data-ttu-id="e27a5-120">Open de opdrachtprompt als beheerder</span><span class="sxs-lookup"><span data-stu-id="e27a5-120">Open the command prompt as an administrator</span></span> 

2. <span data-ttu-id="e27a5-121">Type`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span><span class="sxs-lookup"><span data-stu-id="e27a5-121">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="e27a5-122">Met deze opdracht geeft een dialoogvenster waarmee u meer informatie over de status van de join.</span><span class="sxs-lookup"><span data-stu-id="e27a5-122">This command displays a dialog box that provides you with more details about the join status.</span></span>

![Werkplekdeelname voor Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-the-registration-status"></a><span data-ttu-id="e27a5-124">Stap 2: De registratiestatus van de</span><span class="sxs-lookup"><span data-stu-id="e27a5-124">Step 2: Evaluate the registration status</span></span> 

<span data-ttu-id="e27a5-125">Als de join niet geslaagd is, biedt in het dialoogvenster u informatie over het probleem dat is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="e27a5-125">If the join was not successful, the dialog box provides you with details about the issue that has occured.</span></span>

<span data-ttu-id="e27a5-126">**De meest voorkomende problemen zijn:**</span><span class="sxs-lookup"><span data-stu-id="e27a5-126">**The most common issues are:**</span></span>

- <span data-ttu-id="e27a5-127">Een onjuist geconfigureerde AD FS of Azure AD</span><span class="sxs-lookup"><span data-stu-id="e27a5-127">A misconfigured AD FS or Azure AD</span></span>

    ![Werkplekdeelname voor Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="e27a5-129">U bent niet aangemeld op als een domeingebruiker</span><span class="sxs-lookup"><span data-stu-id="e27a5-129">You are not signed on as a domain user</span></span>

    ![Werkplekdeelname voor Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="e27a5-131">Een quotum is bereikt</span><span class="sxs-lookup"><span data-stu-id="e27a5-131">A quota has been reached</span></span>

    ![Werkplekdeelname voor Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="e27a5-133">De service reageert niet</span><span class="sxs-lookup"><span data-stu-id="e27a5-133">The service is not responding</span></span> 

    ![Werkplekdeelname voor Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="e27a5-135">U kunt ook de statusinformatie vinden in het gebeurtenislogboek onder **toepassingen en Services Log\Microsoft-Workplace Join**.</span><span class="sxs-lookup"><span data-stu-id="e27a5-135">You can also find the status information in the event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="e27a5-136">**De meest voorkomende oorzaken voor de registratie van een mislukte zijn:**</span><span class="sxs-lookup"><span data-stu-id="e27a5-136">**The most common causes for a failed registration are:**</span></span> 

- <span data-ttu-id="e27a5-137">Uw computer zich niet in het interne netwerk van de organisatie of een VPN zonder verbinding met een on-premises AD-domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="e27a5-137">Your computer is not on the organization’s internal network or a VPN without connection to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="e27a5-138">U bent aangemeld met een lokaal computeraccount op de computer.</span><span class="sxs-lookup"><span data-stu-id="e27a5-138">You are logged on to your computer with a local computer account.</span></span> 

- <span data-ttu-id="e27a5-139">Problemen met de configuratie van service:</span><span class="sxs-lookup"><span data-stu-id="e27a5-139">Service configuration issues:</span></span> 

  - <span data-ttu-id="e27a5-140">De federation-server is geconfigureerd voor ondersteuning van **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="e27a5-140">The federation server has been configured to support **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="e27a5-141">Er is geen Service Connection Point-object dat verwijst naar de domeinnaam van uw geverifieerde in Azure AD in het AD-forest waar de computer deel uitmaakt.</span><span class="sxs-lookup"><span data-stu-id="e27a5-141">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to.</span></span>

  - <span data-ttu-id="e27a5-142">Een gebruiker heeft de limiet van apparaten bereikt.</span><span class="sxs-lookup"><span data-stu-id="e27a5-142">A user has reached the limit of devices.</span></span> <span data-ttu-id="e27a5-143">Zie aan de slag met Azure Active Directory-apparaatregistratie.</span><span class="sxs-lookup"><span data-stu-id="e27a5-143">Please see Get Started with Azure Active Directory Device Registration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e27a5-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e27a5-144">Next steps</span></span>

<span data-ttu-id="e27a5-145">Zie voor meer informatie de [automatische apparaatregistratie Veelgestelde vragen](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="e27a5-145">For more information, see the [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
