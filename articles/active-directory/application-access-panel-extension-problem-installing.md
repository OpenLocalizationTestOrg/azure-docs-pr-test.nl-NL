---
title: Problemen bij het installeren van de toegang tot de toepassing van het deelvenster Browseruitbreiding | Microsoft Docs
description: Het oplossen van veelvoorkomende fouten aangetroffen bij het installeren van de uitbreiding voor toegang tot Configuratiescherm browser
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewer: japere
ms.openlocfilehash: 8b7327508633e33917d1fa9c1f35ed1bde5a26e1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="problem-installing-the-application-access-panel-browser-extension"></a><span data-ttu-id="08649-103">Problemen bij het installeren van de toegang tot de toepassing van het deelvenster Browseruitbreiding</span><span class="sxs-lookup"><span data-stu-id="08649-103">Problem installing the application access panel browser extension</span></span>

<span data-ttu-id="08649-104">Het Toegangspaneel is een portal op Internet waarmee een gebruiker met een account voor werk of school in Azure Active Directory (Azure AD) voor weergave in en start cloud-gebaseerde toepassingen die de Azure AD-beheerder heeft deze toegang verleend tot.</span><span class="sxs-lookup"><span data-stu-id="08649-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="08649-105">Een gebruiker met Azure AD-edities kunt ook gebruiken voor groepsbeheer met Self-service en app-mogelijkheden voor beheer via het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="08649-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="08649-106">Het Toegangspaneel is gescheiden van de Azure-portal en vereist geen gebruikers een Azure-abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="08649-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="08649-107">Als u wilt gebruiken op basis van wachtwoorden eenmalige aanmelding (SSO) in het deelvenster toegang, moet de extensie Toegangspaneel worden geïnstalleerd in de browser van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="08649-107">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="08649-108">Deze extensie wordt automatisch gedownload wanneer een gebruiker selecteert een toepassing die is geconfigureerd voor eenmalige aanmelding op basis van wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="08649-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="08649-109">Vergadering Browservereisten voor het toegangsvenster</span><span class="sxs-lookup"><span data-stu-id="08649-109">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="08649-110">Het toegangsvenster vereist een browser die JavaScript ondersteunt en CSS is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="08649-110">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="08649-111">Als u wilt gebruiken op basis van wachtwoorden eenmalige aanmelding (SSO) in het deelvenster toegang, moet de extensie Toegangspaneel worden geïnstalleerd in de browser van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="08649-111">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="08649-112">Deze extensie wordt automatisch gedownload wanneer een gebruiker selecteert een toepassing die is geconfigureerd voor eenmalige aanmelding op basis van wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="08649-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="08649-113">Voor eenmalige aanmelding op basis van wachtwoorden kunnen van de eindgebruiker browsers zijn:</span><span class="sxs-lookup"><span data-stu-id="08649-113">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="08649-114">Internet Explorer 8, 9, 10, 11--op Windows 7 of hoger</span><span class="sxs-lookup"><span data-stu-id="08649-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="08649-115">Rand verjaardagseditie van Windows 10 of hoger</span><span class="sxs-lookup"><span data-stu-id="08649-115">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="08649-116">Chrome--Op Windows 7 of hoger, en op Mac OS X of hoger</span><span class="sxs-lookup"><span data-stu-id="08649-116">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="08649-117">Firefox 26,0 of later--op Windows XP SP2 of hoger, en op Mac OS X 10,6 of hoger</span><span class="sxs-lookup"><span data-stu-id="08649-117">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="08649-118">Het installeren van de Browseruitbreiding toegang Configuratiescherm</span><span class="sxs-lookup"><span data-stu-id="08649-118">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="08649-119">Volg de onderstaande stappen voor het installeren van de Browseruitbreiding toegang Configuratiescherm:</span><span class="sxs-lookup"><span data-stu-id="08649-119">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="08649-120">Open de [Toegangspaneel](https://myapps.microsoft.com) in een van de ondersteunde browsers en meld u aan als een **gebruiker** in uw Azure AD.</span><span class="sxs-lookup"><span data-stu-id="08649-120">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="08649-121">Klik op een **wachtwoord SSO toepassing** in het deelvenster toegang.</span><span class="sxs-lookup"><span data-stu-id="08649-121">Click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="08649-122">Selecteer in het venster met de vraag om de software te installeren, **nu installeren**.</span><span class="sxs-lookup"><span data-stu-id="08649-122">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="08649-123">Op basis van uw browser u omgeleid naar de downloadkoppeling.</span><span class="sxs-lookup"><span data-stu-id="08649-123">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="08649-124">**Voeg** de uitbreiding van uw browser.</span><span class="sxs-lookup"><span data-stu-id="08649-124">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="08649-125">Als uw browser wordt gevraagd, selecteert u op een **inschakelen** of **toestaan** de extensie.</span><span class="sxs-lookup"><span data-stu-id="08649-125">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="08649-126">Nadat deze is geïnstalleerd, **opnieuw** uw browsersessie.</span><span class="sxs-lookup"><span data-stu-id="08649-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="08649-127">Meld u aan in het deelvenster toegang en zien als u kunt **starten** uw wachtwoord SSO-toepassingen</span><span class="sxs-lookup"><span data-stu-id="08649-127">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="08649-128">U kunt ook de uitbreiding voor Chrome en rand van de onderstaande directe koppelingen downloaden:</span><span class="sxs-lookup"><span data-stu-id="08649-128">You may also download the extension for Chrome and Edge from the direct links below:</span></span>

-   [<span data-ttu-id="08649-129">Uitbreiding van chrome toegang Configuratiescherm</span><span class="sxs-lookup"><span data-stu-id="08649-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="08649-130">Uitbreiding van de rand toegang Configuratiescherm</span><span class="sxs-lookup"><span data-stu-id="08649-130">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84) 

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="08649-131">Instellen van een groepsbeleid voor Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="08649-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="08649-132">U kunt een groepsbeleid waarmee u op afstand installeren van de extensie Toegangspaneel voor Internet Explorer op computers van uw gebruikers instellen.</span><span class="sxs-lookup"><span data-stu-id="08649-132">You can setup a group policy that allow you to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="08649-133">De vereisten zijn:</span><span class="sxs-lookup"><span data-stu-id="08649-133">The prerequisites include:</span></span>

-   <span data-ttu-id="08649-134">U hebt ingesteld [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), en u hebt uw gebruikers machines toegevoegd aan uw domein.</span><span class="sxs-lookup"><span data-stu-id="08649-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>

-   <span data-ttu-id="08649-135">U moet de machtiging 'Instellingen bewerken' voor het bewerken van het groepsbeleidsobject (GPO) hebben.</span><span class="sxs-lookup"><span data-stu-id="08649-135">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="08649-136">Standaard hebben leden van de volgende beveiligingsgroepen deze machtiging: Domeinadministrators, Ondernemingsadministrators en Maker Eigenaar Groepsbeleid.</span><span class="sxs-lookup"><span data-stu-id="08649-136">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="08649-137">[Meer informatie](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="08649-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="08649-138">Volg de zelfstudie [het implementeren van de uitbreiding van het Configuratiescherm toegang voor Internet Explorer met behulp van Groepsbeleid](active-directory-saas-ie-group-policy.md) voor stapsgewijze instructies voor het configureren van het Groepsbeleid en het implementeren voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="08649-138">Follow the tutorial [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md) for step by step instructions on how to configure the group policy and deploy it to users.</span></span>

## <a name="troubleshoot-the-access-panel-in-internet-explorer"></a><span data-ttu-id="08649-139">Problemen met het toegangsvenster in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="08649-139">Troubleshoot the Access Panel in Internet Explorer</span></span>

<span data-ttu-id="08649-140">Ga als volgt de [oplossen met de extensie van het Configuratiescherm toegang voor Internet Explorer](active-directory-saas-ie-troubleshooting.md) geleid voor toegang tot een diagnostische hulpprogramma's en stapsgewijze instructies over het configureren van de extensie voor IE.</span><span class="sxs-lookup"><span data-stu-id="08649-140">Follow the [Troubleshoot the Access Panel Extension for Internet Explorer](active-directory-saas-ie-troubleshooting.md) guide for access a diagnostics tool and step by step instructions on configuring the extension for IE.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="08649-141">Als bovenstaande stappen voor probleemoplossing het probleem niet oplossen</span><span class="sxs-lookup"><span data-stu-id="08649-141">If these troubleshooting steps do not resolve the issue</span></span>

<span data-ttu-id="08649-142">een ondersteuningsticket opent met de volgende informatie, indien beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="08649-142">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="08649-143">Correlatie fout-ID</span><span class="sxs-lookup"><span data-stu-id="08649-143">Correlation error ID</span></span>

-   <span data-ttu-id="08649-144">UPN (e-mailadres van de gebruiker)</span><span class="sxs-lookup"><span data-stu-id="08649-144">UPN (user email address)</span></span>

-   <span data-ttu-id="08649-145">TenantID</span><span class="sxs-lookup"><span data-stu-id="08649-145">TenantID</span></span>

-   <span data-ttu-id="08649-146">Browsertype</span><span class="sxs-lookup"><span data-stu-id="08649-146">Browser type</span></span>

-   <span data-ttu-id="08649-147">Tijdzone en de tijd/tijdsbestek tijdens fout optreedt</span><span class="sxs-lookup"><span data-stu-id="08649-147">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="08649-148">Fiddler traceringen</span><span class="sxs-lookup"><span data-stu-id="08649-148">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="08649-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="08649-149">Next steps</span></span>
[<span data-ttu-id="08649-150">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="08649-150">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
