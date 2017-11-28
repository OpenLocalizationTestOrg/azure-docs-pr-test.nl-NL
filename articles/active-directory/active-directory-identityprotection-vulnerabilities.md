---
title: 'Beveiligingsproblemen die worden gedetecteerd door Azure Active Directory: Identity Protection | Microsoft Docs'
description: 'Overzicht van de beveiligingsproblemen die worden gedetecteerd door Azure Active Directory: Identity Protection.'
services: active-directory
keywords: beveiliging in Azure active directory-identiteit, cloud app discovery, het beheren van toepassingen, beveiliging, risico, risiconiveau, beveiligingsprobleem, beveiligingsbeleid
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92233a5b-cb34-4d28-88cc-d5d29c0f3256
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 364873ff54099a6123e40b12e819d1745751f285
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a><span data-ttu-id="ed07b-104">Beveiligingsproblemen die worden gedetecteerd door Azure Active Directory: Identity Protection</span><span class="sxs-lookup"><span data-stu-id="ed07b-104">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="ed07b-105">Zwakke plekken zijn zwakke punten in uw omgeving die door een aanvaller kan worden misbruikt.</span><span class="sxs-lookup"><span data-stu-id="ed07b-105">Vulnerabilities are weaknesses in your environment that can be exploited by an attacker.</span></span> <span data-ttu-id="ed07b-106">U wordt aangeraden dat u deze beveiligingslekken ter verbetering van de beveiligingsstatus van uw organisatie, en voorkomen dat aanvallers deze nu aanvalt.</span><span class="sxs-lookup"><span data-stu-id="ed07b-106">We recommend that you address these vulnerabilities to improve the security posture of your organization, and prevent attackers from exploiting them.</span></span>


<span data-ttu-id="ed07b-107">![beveiligingsproblemen](./media/active-directory-identityprotection-vulnerabilities/101.png "beveiligingsproblemen")</span><span class="sxs-lookup"><span data-stu-id="ed07b-107">![vulnerabilities](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilities")</span></span>



<span data-ttu-id="ed07b-108">De volgende secties bieden u een overzicht van de kwetsbaarheden die zijn gerapporteerd door Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="ed07b-108">The following sections provide you with an overview of the vulnerabilities reported by Identity Protection.</span></span>

## <a name="multi-factor-authentication-registration-not-configured"></a><span data-ttu-id="ed07b-109">Multi-factor authentication-registratie niet geconfigureerd</span><span class="sxs-lookup"><span data-stu-id="ed07b-109">Multi-factor authentication registration not configured</span></span>
<span data-ttu-id="ed07b-110">Deze kwetsbaarheid helpt u bij de implementatie van Azure multi-factor Authentication in uw organisatie beheren.</span><span class="sxs-lookup"><span data-stu-id="ed07b-110">This vulnerability helps you control the deployment of Azure Multi-Factor Authentication in your organization.</span></span> 

<span data-ttu-id="ed07b-111">Azure multi-factor authentication-Server biedt een tweede beveiligingslaag voor verificatie van gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ed07b-111">Azure multi-factor authentication provides a second layer of security to user authentication.</span></span> <span data-ttu-id="ed07b-112">Deze u toegang tot gegevens en toepassingen beveiligt en te voldoen aan de behoeften van de gebruiker voor een eenvoudig proces aanmelden.</span><span class="sxs-lookup"><span data-stu-id="ed07b-112">It helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="ed07b-113">Sterke verificatie via een bereik van eenvoudige verificatie-opties levert: telefoonoproep, tekstbericht of mobiele app melding of verificatie van code en 3rd party OATH-tokens.</span><span class="sxs-lookup"><span data-stu-id="ed07b-113">It delivers strong authentication via a range of easy verification options—phone call, text message, or mobile app notification or verification code and 3rd party OATH tokens.</span></span>

<span data-ttu-id="ed07b-114">Het is raadzaam dat u Azure multi-factor Authentication voor gebruikersaanmelding nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="ed07b-114">We recommend that you require Azure Multi-Factor Authentication for user sign-ins.</span></span> <span data-ttu-id="ed07b-115">Multi-factorauthenticatie speelt een belangrijke rol in de beleidsregels voor voorwaardelijke toegang op basis van risico's beschikbaar via Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="ed07b-115">Multi-factor authentication plays a key role in risk-based conditional access policies available through Identity Protection.</span></span>

<span data-ttu-id="ed07b-116">Zie voor meer informatie [wat is Azure multi-factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ed07b-116">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

## <a name="unmanaged-cloud-apps"></a><span data-ttu-id="ed07b-117">Niet-beheerde cloud-apps</span><span class="sxs-lookup"><span data-stu-id="ed07b-117">Unmanaged cloud apps</span></span>
<span data-ttu-id="ed07b-118">Deze kwetsbaarheid helpt u identificeren onbeheerde cloud-apps in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="ed07b-118">This vulnerability helps you identify unmanaged cloud apps in your organization.</span></span>

<span data-ttu-id="ed07b-119">In moderne ondernemingen zijn IT-afdelingen vaak niet op de hoogte van alle cloud-toepassingen die van gebruikers in hun organisatie gebruikmaken voor hun werk.</span><span class="sxs-lookup"><span data-stu-id="ed07b-119">In modern enterprises, IT departments are often unaware of all the cloud applications that users in their organization are using to do their work.</span></span> <span data-ttu-id="ed07b-120">Het is gemakkelijk om te zien waarom beheerders zou twijfels hebt over niet-geautoriseerde toegang tot zakelijke gegevens, mogelijk gegevenslekken en andere beveiligingsrisico's.</span><span class="sxs-lookup"><span data-stu-id="ed07b-120">It is easy to see why administrators would have concerns about unauthorized access to corporate data, possible data leakage and other security risks.</span></span> 

<span data-ttu-id="ed07b-121">We raden aan uw organisatie te implementeren Cloud App Discovery voor het detecteren van niet-beheerde cloud-toepassingen en voor het beheren van deze toepassingen met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ed07b-121">We recommend that your organization deploy Cloud App Discovery to discover unmanaged cloud applications, and to manage these applications using Azure Active Directory.</span></span>

<span data-ttu-id="ed07b-122">Zie voor meer informatie [zoeken naar niet-beheerde cloud-toepassingen met Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ed07b-122">For more details, see [Finding unmanaged cloud applications with Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>

## <a name="security-alerts-from-privileged-identity-management"></a><span data-ttu-id="ed07b-123">Beveiligingswaarschuwingen van Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="ed07b-123">Security Alerts from Privileged Identity Management</span></span>
<span data-ttu-id="ed07b-124">Deze kwetsbaarheid helpt u bij het opsporen en oplossen van waarschuwingen over bevoegde identiteiten in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="ed07b-124">This vulnerability helps you discover and resolve alerts about privileged identities in your organization.</span></span>  

<span data-ttu-id="ed07b-125">Als u wilt dat gebruikers kunnen bevoorrechte bewerkingen uitvoeren, moeten organisaties gebruikers tijdelijke of permanente bevoegde om toegang te verlenen in Azure AD, Azure of Office 365-bronnen of andere SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="ed07b-125">To enable users to carry out privileged operations, organizations need to grant users temporary or permanent privileged access in Azure AD, Azure or Office 365 resources, or other SaaS apps.</span></span> <span data-ttu-id="ed07b-126">Elk van deze bevoegde gebruikers verhoogt de kwetsbaarheid van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="ed07b-126">Each of these privileged users increases the attack surface of your organization.</span></span> <span data-ttu-id="ed07b-127">Deze kwetsbaarheid kunt u gebruikers identificeren met onnodige bevoegdheden gebruiken en onderneem gepaste actie te verlagen of elimineren het risico dat ze vormen.</span><span class="sxs-lookup"><span data-stu-id="ed07b-127">This vulnerability helps you identify users with unnecessary privileged access, and take appropriate action to reduce or eliminate the risk they pose.</span></span> 

<span data-ttu-id="ed07b-128">Het is raadzaam om uw organisatie gebruikmaakt van Azure AD Privileged Identity Management te beheren, beheren en bewaken bevoegde identiteiten en toegang krijgen tot bronnen in Azure AD, evenals andere Microsoft online services zoals Office 365 of Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="ed07b-128">We recommend that your organization uses Azure AD Privileged Identity Management to manage, control, and monitor privileged identities and their access to resources in Azure AD as well as other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="ed07b-129">Zie voor meer informatie [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ed07b-129">For more details, see [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="see-also"></a><span data-ttu-id="ed07b-130">Zie ook</span><span class="sxs-lookup"><span data-stu-id="ed07b-130">See also</span></span>
* [<span data-ttu-id="ed07b-131">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="ed07b-131">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

