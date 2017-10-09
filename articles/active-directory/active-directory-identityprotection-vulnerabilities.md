---
title: 'aaaVulnerabilities gedetecteerd door Azure Active Directory: Identity Protection | Microsoft Docs'
description: 'Overzicht van Hallo beveiligingsproblemen die worden gedetecteerd door Azure Active Directory: Identity Protection.'
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
ms.openlocfilehash: 5e1cb401f8b566a180eb46e3420a090bcfc66767
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a><span data-ttu-id="0990d-104">Beveiligingsproblemen die worden gedetecteerd door Azure Active Directory: Identity Protection</span><span class="sxs-lookup"><span data-stu-id="0990d-104">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="0990d-105">Zwakke plekken zijn zwakke punten in uw omgeving die door een aanvaller kan worden misbruikt.</span><span class="sxs-lookup"><span data-stu-id="0990d-105">Vulnerabilities are weaknesses in your environment that can be exploited by an attacker.</span></span> <span data-ttu-id="0990d-106">U wordt aangeraden deze beveiligingsproblemen tooimprove Hallo beveiligingsstatus van uw organisatie adres en voorkomen dat aanvallers deze nu aanvalt.</span><span class="sxs-lookup"><span data-stu-id="0990d-106">We recommend that you address these vulnerabilities tooimprove hello security posture of your organization, and prevent attackers from exploiting them.</span></span>


<span data-ttu-id="0990d-107">![beveiligingsproblemen](./media/active-directory-identityprotection-vulnerabilities/101.png "beveiligingsproblemen")</span><span class="sxs-lookup"><span data-stu-id="0990d-107">![vulnerabilities](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilities")</span></span>



<span data-ttu-id="0990d-108">Hallo volgende secties vindt u een overzicht van Hallo zwakke plekken die zijn gerapporteerd door Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="0990d-108">hello following sections provide you with an overview of hello vulnerabilities reported by Identity Protection.</span></span>

## <a name="multi-factor-authentication-registration-not-configured"></a><span data-ttu-id="0990d-109">Multi-factor authentication-registratie niet geconfigureerd</span><span class="sxs-lookup"><span data-stu-id="0990d-109">Multi-factor authentication registration not configured</span></span>
<span data-ttu-id="0990d-110">Deze kwetsbaarheid helpt u bij Hallo-implementatie van Azure multi-factor Authentication in uw organisatie beheren.</span><span class="sxs-lookup"><span data-stu-id="0990d-110">This vulnerability helps you control hello deployment of Azure Multi-Factor Authentication in your organization.</span></span> 

<span data-ttu-id="0990d-111">Azure multi-factor authentication-Server biedt een tweede beveiligingslaag toouser beveiligingsverificatie.</span><span class="sxs-lookup"><span data-stu-id="0990d-111">Azure multi-factor authentication provides a second layer of security toouser authentication.</span></span> <span data-ttu-id="0990d-112">Het helpt beveiliging toegang toodata en toepassingen en te voldoen aan de behoeften van de gebruiker voor een eenvoudig proces aanmelden.</span><span class="sxs-lookup"><span data-stu-id="0990d-112">It helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="0990d-113">Sterke verificatie via een bereik van eenvoudige verificatie-opties levert: telefoonoproep, tekstbericht of mobiele app melding of verificatie van code en 3rd party OATH-tokens.</span><span class="sxs-lookup"><span data-stu-id="0990d-113">It delivers strong authentication via a range of easy verification options—phone call, text message, or mobile app notification or verification code and 3rd party OATH tokens.</span></span>

<span data-ttu-id="0990d-114">Het is raadzaam dat u Azure multi-factor Authentication voor gebruikersaanmelding nodig hebt. Multi-factorauthenticatie speelt een belangrijke rol in de beleidsregels voor voorwaardelijke toegang op basis van risico's beschikbaar via Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="0990d-114">We recommend that you require Azure Multi-Factor Authentication for user sign-ins. Multi-factor authentication plays a key role in risk-based conditional access policies available through Identity Protection.</span></span>

<span data-ttu-id="0990d-115">Zie voor meer informatie [wat is Azure multi-factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="0990d-115">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

## <a name="unmanaged-cloud-apps"></a><span data-ttu-id="0990d-116">Niet-beheerde cloud-apps</span><span class="sxs-lookup"><span data-stu-id="0990d-116">Unmanaged cloud apps</span></span>
<span data-ttu-id="0990d-117">Deze kwetsbaarheid helpt u identificeren onbeheerde cloud-apps in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="0990d-117">This vulnerability helps you identify unmanaged cloud apps in your organization.</span></span>

<span data-ttu-id="0990d-118">In moderne ondernemingen zijn IT-afdelingen vaak niet op de hoogte van alle Hallo cloud-toepassingen dat gebruikers in hun organisatie toodo hun werk gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0990d-118">In modern enterprises, IT departments are often unaware of all hello cloud applications that users in their organization are using toodo their work.</span></span> <span data-ttu-id="0990d-119">Het is gemakkelijk toosee waarom beheerders twijfels over onbevoegde toegang toocorporate gegevens, mogelijk gegevenslekken en andere beveiligingsrisico's hebt zou.</span><span class="sxs-lookup"><span data-stu-id="0990d-119">It is easy toosee why administrators would have concerns about unauthorized access toocorporate data, possible data leakage and other security risks.</span></span> 

<span data-ttu-id="0990d-120">We raden aan dat uw organisatie implementeren Cloud App Discovery toodiscover zonder begeleiding cloud-toepassingen en toomanage deze toepassingen met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0990d-120">We recommend that your organization deploy Cloud App Discovery toodiscover unmanaged cloud applications, and toomanage these applications using Azure Active Directory.</span></span>

<span data-ttu-id="0990d-121">Zie voor meer informatie [zoeken naar niet-beheerde cloud-toepassingen met Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0990d-121">For more details, see [Finding unmanaged cloud applications with Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>

## <a name="security-alerts-from-privileged-identity-management"></a><span data-ttu-id="0990d-122">Beveiligingswaarschuwingen van Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="0990d-122">Security Alerts from Privileged Identity Management</span></span>
<span data-ttu-id="0990d-123">Deze kwetsbaarheid helpt u bij het opsporen en oplossen van waarschuwingen over bevoegde identiteiten in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="0990d-123">This vulnerability helps you discover and resolve alerts about privileged identities in your organization.</span></span>  

<span data-ttu-id="0990d-124">tooenable gebruikers toocarry bevoorrechte bewerkingen, moeten organisaties toogrant gebruikers tijdelijke of permanente bevoegde toegang in Azure AD, Azure of Office 365-bronnen of andere SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="0990d-124">tooenable users toocarry out privileged operations, organizations need toogrant users temporary or permanent privileged access in Azure AD, Azure or Office 365 resources, or other SaaS apps.</span></span> <span data-ttu-id="0990d-125">Elk van deze kwetsbaarheid bevoegde gebruikers toeneemt Hallo van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="0990d-125">Each of these privileged users increases hello attack surface of your organization.</span></span> <span data-ttu-id="0990d-126">Deze kwetsbaarheid kunt u gebruikers identificeren met onnodige bevoorrechte toegang, en tooreduce passende maatregelen nemen of elimineren Hallo risico die ze vormen.</span><span class="sxs-lookup"><span data-stu-id="0990d-126">This vulnerability helps you identify users with unnecessary privileged access, and take appropriate action tooreduce or eliminate hello risk they pose.</span></span> 

<span data-ttu-id="0990d-127">We raden aan dat uw organisatie gebruikmaakt van Azure AD Privileged Identity Management toomanage, beheren en monitor bevoegde identiteiten en hun access tooresources in Azure AD, alsmede andere Microsoft online services zoals Office 365 of Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="0990d-127">We recommend that your organization uses Azure AD Privileged Identity Management toomanage, control, and monitor privileged identities and their access tooresources in Azure AD as well as other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="0990d-128">Zie voor meer informatie [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0990d-128">For more details, see [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="see-also"></a><span data-ttu-id="0990d-129">Zie ook</span><span class="sxs-lookup"><span data-stu-id="0990d-129">See also</span></span>
* [<span data-ttu-id="0990d-130">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="0990d-130">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

