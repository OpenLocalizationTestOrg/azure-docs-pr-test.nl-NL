---
title: Domein apparaten verbinden met Azure AD voor Windows 10 optreedt | Microsoft Docs
description: Legt uit hoe beheerders Groepsbeleid zodat apparaten aan het domein met het bedrijfsnetwerk kunnen configureren.
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
ms.openlocfilehash: 9c91579d20bb84701f6d0b97d944728c84044adf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-domain-joined-devices-to-azure-ad-for-windows-10-experiences"></a><span data-ttu-id="26edc-103">Connect domain-joined devices to Azure AD for Windows 10 experiences (Engelstalig)</span><span class="sxs-lookup"><span data-stu-id="26edc-103">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>
<span data-ttu-id="26edc-104">Aan domein toevoegen is dat de traditionele manier organisaties hebben verbonden apparaten voor werk voor de afgelopen 15 jaar en meer.</span><span class="sxs-lookup"><span data-stu-id="26edc-104">Domain join is the traditional way organizations have connected devices for work for the last 15 years and more.</span></span> <span data-ttu-id="26edc-105">Gebruikers kunnen aanmelden met hun apparaten via hun werk Windows Server Active Directory (Active Directory)- of schoolaccounts ingeschakeld en toegestaan IT volledig deze apparaten te beheren.</span><span class="sxs-lookup"><span data-stu-id="26edc-105">It has enabled users to sign in to their devices by using their Windows Server Active Directory (Active Directory) work or school accounts and allowed IT to fully manage these devices.</span></span> <span data-ttu-id="26edc-106">Organisaties zijn gewoonlijk afhankelijk van de installatiekopieën methoden voor het inrichten van apparaten aan gebruikers en meestal System Center Configuration Manager (SCCM) of Groepsbeleid gebruiken om deze te beheren.</span><span class="sxs-lookup"><span data-stu-id="26edc-106">Organizations typically rely on imaging methods to provision devices to users and generally use System Center Configuration Manager (SCCM) or Group Policy to manage them.</span></span>


<span data-ttu-id="26edc-107">Aan domein toevoegen in Windows 10 biedt de volgende voordelen nadat u apparaten op Azure Active Directory (Azure AD aansluit):</span><span class="sxs-lookup"><span data-stu-id="26edc-107">Domain join in Windows 10 provides you with the following benefits after you connect devices to Azure Active Directory (Azure AD):</span></span>

* <span data-ttu-id="26edc-108">Eenmalige aanmelding (SSO) naar Azure AD-resources vanaf elke locatie</span><span class="sxs-lookup"><span data-stu-id="26edc-108">Single sign-on (SSO) to Azure AD resources from anywhere</span></span>
* <span data-ttu-id="26edc-109">Toegang tot de Windows Store-onderneming met werk of school accounts (Er is geen Microsoft-account vereist)</span><span class="sxs-lookup"><span data-stu-id="26edc-109">Access to the enterprise Windows Store by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="26edc-110">Enterprise-compatibele zwervende gebruikersinstellingen op apparaten met werk of school accounts (Er is geen Microsoft-account vereist)</span><span class="sxs-lookup"><span data-stu-id="26edc-110">Enterprise-compliant roaming of user settings across devices by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="26edc-111">Sterke verificatie en handige aanmelden voor werk of school accounts met Windows Hello voor bedrijven en Windows Hello</span><span class="sxs-lookup"><span data-stu-id="26edc-111">Strong authentication and convenient sign-in for work or school accounts with Windows Hello for Business and Windows Hello</span></span>
* <span data-ttu-id="26edc-112">Mogelijkheid toegang te beperken tot apparaten die aan de organisatie-instellingen voor Groepsbeleid voldoen</span><span class="sxs-lookup"><span data-stu-id="26edc-112">Ability to restrict access only to devices that comply with organizational device Group Policy settings</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26edc-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="26edc-113">Prerequisites</span></span>
<span data-ttu-id="26edc-114">Aan domein toevoegen blijft nuttig zijn.</span><span class="sxs-lookup"><span data-stu-id="26edc-114">Domain join continues to be useful.</span></span> <span data-ttu-id="26edc-115">Echter te krijgen van de Azure AD-voordelen van eenmalige aanmelding, zwervende instellingen met werk of schoolaccounts en toegang tot Windows Store met werk of school-accounts, moet u het volgende:</span><span class="sxs-lookup"><span data-stu-id="26edc-115">However, to get the Azure AD benefits of SSO, roaming of settings with work or school accounts, and access to Windows Store with work or school accounts, you will need the following:</span></span>

* <span data-ttu-id="26edc-116">Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="26edc-116">Azure AD subscription</span></span>
* <span data-ttu-id="26edc-117">Azure AD Connect uit te breiden de on-premises directory naar Azure AD</span><span class="sxs-lookup"><span data-stu-id="26edc-117">Azure AD Connect to extend the on-premises directory to Azure AD</span></span>
* <span data-ttu-id="26edc-118">Beleid dat is ingesteld op het domein apparaten verbinden met Azure AD</span><span class="sxs-lookup"><span data-stu-id="26edc-118">Policy that's set to connect domain-joined devices to Azure AD</span></span>
* <span data-ttu-id="26edc-119">Windows 10-build (build 10551 of nieuwer) voor apparaten</span><span class="sxs-lookup"><span data-stu-id="26edc-119">Windows 10 build (build 10551 or newer) for devices</span></span>

<span data-ttu-id="26edc-120">Schakel Windows Hello voor bedrijven en Windows Hello door u ook het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="26edc-120">To enable Windows Hello for Business and Windows Hello, you will also need the following:</span></span>

- <span data-ttu-id="26edc-121">**Openbare-sleutelinfrastructuur (PKI)** voor de gebruiker certificaten uitgifte.</span><span class="sxs-lookup"><span data-stu-id="26edc-121">**Public key infrastructure (PKI)** for user certificates issuance.</span></span>

- <span data-ttu-id="26edc-122">**System Center Configuration Manager Current Branch** -u moet versie 1606 of hoger installeren.</span><span class="sxs-lookup"><span data-stu-id="26edc-122">**System Center Configuration Manager Current Branch** - You need to install version 1606 or better.</span></span>  
<span data-ttu-id="26edc-123">Zie voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="26edc-123">For more information, see:</span></span> 
    - [<span data-ttu-id="26edc-124">Documentatie voor System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="26edc-124">Documentation for System Center Configuration Manager</span></span>](https://technet.microsoft.com/library/mt346023.aspx)
    - [<span data-ttu-id="26edc-125">System Center Configuration Manager-teamblog</span><span class="sxs-lookup"><span data-stu-id="26edc-125">System Center Configuration Manager Team Blog</span></span>](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [<span data-ttu-id="26edc-126">Windows Hello voor bedrijven-instellingen in System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="26edc-126">Windows Hello for Business settings in System Center Configuration Manager</span></span>](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

<span data-ttu-id="26edc-127">Als alternatief voor de vereiste PKI-implementatie kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="26edc-127">As an alternative to the PKI deployment requirement, you can do the following:</span></span>

* <span data-ttu-id="26edc-128">Enkele domeincontrollers met Windows Server 2016 Active Directory Domain Services hebben.</span><span class="sxs-lookup"><span data-stu-id="26edc-128">Have a few domain controllers with Windows Server 2016 Active Directory Domain Services.</span></span>

<span data-ttu-id="26edc-129">U kunt instellingen voor Groepsbeleid die toegang tot de domein-apparaten met geen extra implementaties geven maken voor het inschakelen van voorwaardelijke toegang.</span><span class="sxs-lookup"><span data-stu-id="26edc-129">To enable conditional access, you can create Group Policy settings that allow access to domain-joined devices with no additional deployments.</span></span> <span data-ttu-id="26edc-130">Voor het beheren van toegangsbeheer op basis van naleving van het apparaat, moet u het volgende:</span><span class="sxs-lookup"><span data-stu-id="26edc-130">To manage access control based on compliance of the device, you will need the following:</span></span>

* <span data-ttu-id="26edc-131">System Center Configuration Manager Current Branch (1606 of hoger) voor Windows Hello voor bedrijven-scenario 's</span><span class="sxs-lookup"><span data-stu-id="26edc-131">System Center Configuration Manager Current Branch (1606 or later) for Windows Hello for Business scenarios</span></span>

## <a name="deployment-instructions"></a><span data-ttu-id="26edc-132">Implementatie-instructies</span><span class="sxs-lookup"><span data-stu-id="26edc-132">Deployment instructions</span></span>

<span data-ttu-id="26edc-133">Volg de stappen in voor het implementeren [automatische registratie van Windows-domein-apparaten met Azure Active Directory configureren](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="26edc-133">To deploy, follow the steps listed in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

## <a name="next-step"></a><span data-ttu-id="26edc-134">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="26edc-134">Next step</span></span>
* <span data-ttu-id="26edc-135">[Windows 10 for the enterprise: Ways to use devices for work](active-directory-azureadjoin-windows10-devices-overview.md) (Windows 10 voor de onderneming: manieren om apparaten voor werk te gebruiken)</span><span class="sxs-lookup"><span data-stu-id="26edc-135">[Windows 10 for the enterprise: Ways to use devices for work](active-directory-azureadjoin-windows10-devices-overview.md)</span></span>
* <span data-ttu-id="26edc-136">[Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md) (Cloudmogelijkheden uitbreiden naar Windows 10-apparaten met behulp van Azure Active Directory Join)</span><span class="sxs-lookup"><span data-stu-id="26edc-136">[Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)</span></span>
* <span data-ttu-id="26edc-137">[Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md) (Gebruiksscenario’s voor Azure AD Join)</span><span class="sxs-lookup"><span data-stu-id="26edc-137">[Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)</span></span>
* <span data-ttu-id="26edc-138">[Connect domain-joined devices to Azure AD for Windows 10 experiences](active-directory-azureadjoin-devices-group-policy.md) (Apparaten die lid zijn van een domein verbinden met Azure AD voor Windows 10-ervaringen)</span><span class="sxs-lookup"><span data-stu-id="26edc-138">[Connect domain-joined devices to Azure AD for Windows 10 experiences](active-directory-azureadjoin-devices-group-policy.md)</span></span>
* [<span data-ttu-id="26edc-139">Azure AD Join instellen</span><span class="sxs-lookup"><span data-stu-id="26edc-139">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

