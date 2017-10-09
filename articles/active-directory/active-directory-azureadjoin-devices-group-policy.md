---
title: aaaConnect domeinapparaten tooAzure AD voor Windows 10 optreedt | Microsoft Docs
description: Legt uit hoe beheerders bedrijfsnetwerk Groepsbeleid tooenable apparaten toobe toohello domein kunnen configureren.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2ff29f3e-5325-4f43-9baa-6ae8d6bad3e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 9766aa702352dea2ecad3a9a0bdf8d3286ee6d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-domain-joined-devices-tooazure-ad-for-windows-10-experiences"></a><span data-ttu-id="572aa-103">Verbinding maken met domein apparaten tooAzure AD voor Windows 10-ervaring</span><span class="sxs-lookup"><span data-stu-id="572aa-103">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>
<span data-ttu-id="572aa-104">Domeinlidmaatschap is Hallo traditionele manier organisaties hebben verbonden apparaten voor werk voor Hallo afgelopen 15 jaar en meer.</span><span class="sxs-lookup"><span data-stu-id="572aa-104">Domain join is hello traditional way organizations have connected devices for work for hello last 15 years and more.</span></span> <span data-ttu-id="572aa-105">Deze gebruikers toosign tootheir apparaten ingeschakeld met behulp van hun werk Windows Server Active Directory (Active Directory) of schoolaccounts en toegestane IT toofully deze apparaten te beheren.</span><span class="sxs-lookup"><span data-stu-id="572aa-105">It has enabled users toosign in tootheir devices by using their Windows Server Active Directory (Active Directory) work or school accounts and allowed IT toofully manage these devices.</span></span> <span data-ttu-id="572aa-106">Organisaties zijn gewoonlijk afhankelijk van de methoden tooprovision apparaten toousers imaging en System Center Configuration Manager (SCCM) of Groepsbeleid toomanage wordt meestal gebruikt ze.</span><span class="sxs-lookup"><span data-stu-id="572aa-106">Organizations typically rely on imaging methods tooprovision devices toousers and generally use System Center Configuration Manager (SCCM) or Group Policy toomanage them.</span></span>


<span data-ttu-id="572aa-107">Aan domein toevoegen in Windows 10 biedt Hallo volgende voordelen nadat u verbinding maakt met apparaten tooAzure Active Directory (Azure AD):</span><span class="sxs-lookup"><span data-stu-id="572aa-107">Domain join in Windows 10 provides you with hello following benefits after you connect devices tooAzure Active Directory (Azure AD):</span></span>

* <span data-ttu-id="572aa-108">Eenmalige aanmelding (SSO) tooAzure AD bronnen vanaf elke locatie</span><span class="sxs-lookup"><span data-stu-id="572aa-108">Single sign-on (SSO) tooAzure AD resources from anywhere</span></span>
* <span data-ttu-id="572aa-109">Toohello enterprise, Windows Store openen met behulp van werk of school accounts (Er is geen Microsoft-account vereist)</span><span class="sxs-lookup"><span data-stu-id="572aa-109">Access toohello enterprise Windows Store by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="572aa-110">Enterprise-compatibele zwervende gebruikersinstellingen op apparaten met werk of school accounts (Er is geen Microsoft-account vereist)</span><span class="sxs-lookup"><span data-stu-id="572aa-110">Enterprise-compliant roaming of user settings across devices by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="572aa-111">Sterke verificatie en handige aanmelden voor werk of school accounts met Windows Hello voor bedrijven en Windows Hello</span><span class="sxs-lookup"><span data-stu-id="572aa-111">Strong authentication and convenient sign-in for work or school accounts with Windows Hello for Business and Windows Hello</span></span>
* <span data-ttu-id="572aa-112">Mogelijkheid toorestrict toegang alleen toodevices die voldoen aan de organisatie-instellingen voor Groepsbeleid</span><span class="sxs-lookup"><span data-stu-id="572aa-112">Ability toorestrict access only toodevices that comply with organizational device Group Policy settings</span></span>

## <a name="prerequisites"></a><span data-ttu-id="572aa-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="572aa-113">Prerequisites</span></span>
<span data-ttu-id="572aa-114">Aan domein toevoegen blijft toobe nuttig.</span><span class="sxs-lookup"><span data-stu-id="572aa-114">Domain join continues toobe useful.</span></span> <span data-ttu-id="572aa-115">Echter tooget hello Azure AD voordelen van eenmalige aanmelding, zwervende instellingen met werk of schoolaccounts, en toegang tot de tooWindows opgeslagen met werk of school accounts, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="572aa-115">However, tooget hello Azure AD benefits of SSO, roaming of settings with work or school accounts, and access tooWindows Store with work or school accounts, you will need hello following:</span></span>

* <span data-ttu-id="572aa-116">Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="572aa-116">Azure AD subscription</span></span>
* <span data-ttu-id="572aa-117">Azure AD Connect tooextend Hallo lokale directory tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="572aa-117">Azure AD Connect tooextend hello on-premises directory tooAzure AD</span></span>
* <span data-ttu-id="572aa-118">Beleid dat is ingesteld tooconnect domeinapparaten tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="572aa-118">Policy that's set tooconnect domain-joined devices tooAzure AD</span></span>
* <span data-ttu-id="572aa-119">Windows 10-build (build 10551 of nieuwer) voor apparaten</span><span class="sxs-lookup"><span data-stu-id="572aa-119">Windows 10 build (build 10551 or newer) for devices</span></span>

<span data-ttu-id="572aa-120">tooenable Windows Hello voor bedrijven en Windows Hello, moet u ook de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="572aa-120">tooenable Windows Hello for Business and Windows Hello, you will also need hello following:</span></span>

- <span data-ttu-id="572aa-121">**Openbare-sleutelinfrastructuur (PKI)** voor de gebruiker certificaten uitgifte.</span><span class="sxs-lookup"><span data-stu-id="572aa-121">**Public key infrastructure (PKI)** for user certificates issuance.</span></span>

- <span data-ttu-id="572aa-122">**System Center Configuration Manager Current Branch** -u moet tooinstall versie 1606 of hoger.</span><span class="sxs-lookup"><span data-stu-id="572aa-122">**System Center Configuration Manager Current Branch** - You need tooinstall version 1606 or better.</span></span>  
<span data-ttu-id="572aa-123">Zie voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="572aa-123">For more information, see:</span></span> 
    - [<span data-ttu-id="572aa-124">Documentatie voor System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="572aa-124">Documentation for System Center Configuration Manager</span></span>](https://technet.microsoft.com/library/mt346023.aspx)
    - [<span data-ttu-id="572aa-125">System Center Configuration Manager-teamblog</span><span class="sxs-lookup"><span data-stu-id="572aa-125">System Center Configuration Manager Team Blog</span></span>](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [<span data-ttu-id="572aa-126">Windows Hello voor bedrijven-instellingen in System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="572aa-126">Windows Hello for Business settings in System Center Configuration Manager</span></span>](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

<span data-ttu-id="572aa-127">U kunt doen als een implementatievereiste van alternatieve toohello PKI Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="572aa-127">As an alternative toohello PKI deployment requirement, you can do hello following:</span></span>

* <span data-ttu-id="572aa-128">Enkele domeincontrollers met Windows Server 2016 Active Directory Domain Services hebben.</span><span class="sxs-lookup"><span data-stu-id="572aa-128">Have a few domain controllers with Windows Server 2016 Active Directory Domain Services.</span></span>

<span data-ttu-id="572aa-129">tooenable voorwaardelijke toegang, kunt u instellingen voor Groepsbeleid waarmee toegang tot apparaten die lid zijn van toodomain met geen extra implementaties.</span><span class="sxs-lookup"><span data-stu-id="572aa-129">tooenable conditional access, you can create Group Policy settings that allow access toodomain-joined devices with no additional deployments.</span></span> <span data-ttu-id="572aa-130">toomanage toegangsbeheer op basis van naleving van Hallo-apparaat, moet u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="572aa-130">toomanage access control based on compliance of hello device, you will need hello following:</span></span>

* <span data-ttu-id="572aa-131">System Center Configuration Manager Current Branch (1606 of hoger) voor Windows Hello voor bedrijven-scenario 's</span><span class="sxs-lookup"><span data-stu-id="572aa-131">System Center Configuration Manager Current Branch (1606 or later) for Windows Hello for Business scenarios</span></span>

## <a name="deployment-instructions"></a><span data-ttu-id="572aa-132">Implementatie-instructies</span><span class="sxs-lookup"><span data-stu-id="572aa-132">Deployment instructions</span></span>

<span data-ttu-id="572aa-133">toodeploy, volg Hallo de stappen die worden vermeld in [hoe tooconfigure automatische registratie van Windows-domein apparaten met Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="572aa-133">toodeploy, follow hello steps listed in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

## <a name="next-step"></a><span data-ttu-id="572aa-134">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="572aa-134">Next step</span></span>
* [<span data-ttu-id="572aa-135">Windows 10 voor Hallo ondernemingen: manieren toouse apparaten for work.</span><span class="sxs-lookup"><span data-stu-id="572aa-135">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="572aa-136">Cloud-mogelijkheden tooWindows 10-apparaten via Azure Active Directory Join uitbreiden</span><span class="sxs-lookup"><span data-stu-id="572aa-136">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* <span data-ttu-id="572aa-137">[Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md) (Gebruiksscenario’s voor Azure AD Join)</span><span class="sxs-lookup"><span data-stu-id="572aa-137">[Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)</span></span>
* [<span data-ttu-id="572aa-138">Verbinding maken met domein apparaten tooAzure AD voor Windows 10-ervaring</span><span class="sxs-lookup"><span data-stu-id="572aa-138">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="572aa-139">Azure AD Join instellen</span><span class="sxs-lookup"><span data-stu-id="572aa-139">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

