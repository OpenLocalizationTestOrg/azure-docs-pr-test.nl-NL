---
title: 'Azure AD Connect: Naadloze eenmalige aanmelding - werking | Microsoft Docs'
description: Dit artikel wordt beschreven hoe de functie Azure Active Directory naadloze eenmalige aanmelding werkt.
services: active-directory
keywords: Wat is Azure AD Connect, installeer Active Directory onderdelen vereist voor Azure AD, SSO, Single Sign-on
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: f0bcbdb03fbb70ff91ac3a56974a88eb1b26c245
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a><span data-ttu-id="eb648-104">Azure Active Directory naadloze eenmalige aanmelding: technische diepgaand</span><span class="sxs-lookup"><span data-stu-id="eb648-104">Azure Active Directory Seamless Single Sign-On: Technical deep dive</span></span>

<span data-ttu-id="eb648-105">In dit artikel biedt u technische gegevens in de werking van de functie Azure Active Directory naadloze eenmalige aanmelding (SSO naadloze).</span><span class="sxs-lookup"><span data-stu-id="eb648-105">This article gives you technical details into how the Azure Active Directory Seamless Single Sign-On (Seamless SSO) feature works.</span></span>

>[!IMPORTANT]
><span data-ttu-id="eb648-106">De functie naadloze eenmalige aanmelding is momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="eb648-106">The Seamless SSO feature is currently in preview.</span></span>

## <a name="how-does-seamless-sso-work"></a><span data-ttu-id="eb648-107">Hoe werkt naadloze eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="eb648-107">How does Seamless SSO work?</span></span>

<span data-ttu-id="eb648-108">Deze sectie heeft twee delen:</span><span class="sxs-lookup"><span data-stu-id="eb648-108">This section has two parts to it:</span></span>
1. <span data-ttu-id="eb648-109">De installatie van de functie naadloze eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="eb648-109">The setup of the Seamless SSO feature.</span></span>
2. <span data-ttu-id="eb648-110">Hoe werkt een enkele gebruiker aanmelden transactie met naadloze eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="eb648-110">How a single user sign-in transaction works with Seamless SSO.</span></span>

### <a name="how-does-set-up-work"></a><span data-ttu-id="eb648-111">Hoe werken instellen?</span><span class="sxs-lookup"><span data-stu-id="eb648-111">How does set up work?</span></span>

<span data-ttu-id="eb648-112">Naadloze eenmalige aanmelding is ingeschakeld via Azure AD Connect zoals [hier](active-directory-aadconnect-sso-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="eb648-112">Seamless SSO is enabled using Azure AD Connect as shown [here](active-directory-aadconnect-sso-quick-start.md).</span></span> <span data-ttu-id="eb648-113">Tijdens het inschakelen van de functie, plaats de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="eb648-113">While enabling the feature, the following steps occur:</span></span>
- <span data-ttu-id="eb648-114">Een account met de naam `AZUREADSSOACCT` (geeft Azure AD) is gemaakt in uw on-premises Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="eb648-114">A computer account named `AZUREADSSOACCT` (which represents Azure AD) is created in your on-premises Active Directory (AD).</span></span>
- <span data-ttu-id="eb648-115">Het computeraccount Kerberos ontsleutelingssleutel wordt veilig worden gedeeld met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb648-115">The computer account's Kerberos decryption key is shared securely with Azure AD.</span></span>
- <span data-ttu-id="eb648-116">Bovendien worden twee Kerberos-SPN-namen (SPN's) gemaakt ter vertegenwoordiging van twee URL's die worden gebruikt tijdens het aanmelden van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb648-116">In addition, two Kerberos service principal names (SPNs) are created to represent two URLs that are used during Azure AD sign-in.</span></span>

>[!NOTE]
> <span data-ttu-id="eb648-117">Het computeraccount en de Kerberos-SPN's worden gemaakt in elk AD-forest u synchroniseren met Azure AD (met behulp van Azure AD Connect) en gebruikers voor wie u wilt dat naadloze eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="eb648-117">The computer account and the Kerberos SPNs are created in each AD forest you synchronize to Azure AD (using Azure AD Connect) and for whose users you want Seamless SSO.</span></span> <span data-ttu-id="eb648-118">Verplaats de `AZUREADSSOACCT` computeraccount aan een organisatie-eenheid (OE) waar de computeraccounts van andere worden opgeslagen om ervoor te zorgen dat het op dezelfde manier wordt beheerd en wordt niet verwijderd.</span><span class="sxs-lookup"><span data-stu-id="eb648-118">Move the `AZUREADSSOACCT` computer account to an Organization Unit (OU) where other computer accounts are stored to ensure that it is managed in the same way and is not deleted.</span></span>

>[!IMPORTANT]
><span data-ttu-id="eb648-119">Ten zeerste aangeraden dat u [Beweeg de muis over de ontsleutelingssleutel Kerberos](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) van de `AZUREADSSOACCT` computeraccount ten minste elke 30 dagen.</span><span class="sxs-lookup"><span data-stu-id="eb648-119">We highly recommend that you [roll over the Kerberos decryption key](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) of the `AZUREADSSOACCT` computer account at least every 30 days.</span></span>

### <a name="how-does-sign-in-with-seamless-sso-work"></a><span data-ttu-id="eb648-120">Hoe aanmelden met naadloze eenmalige aanmelding werk?</span><span class="sxs-lookup"><span data-stu-id="eb648-120">How does sign-in with Seamless SSO work?</span></span>

<span data-ttu-id="eb648-121">Zodra de installatie voltooid is, werkt naadloze eenmalige aanmelding op dezelfde manier als elke andere aanmelden die gebruikmaakt van geïntegreerde Windows-verificatie (IWA).</span><span class="sxs-lookup"><span data-stu-id="eb648-121">Once the set-up is complete, Seamless SSO works the same way as any other sign-in that uses Integrated Windows Authentication (IWA).</span></span> <span data-ttu-id="eb648-122">De stroom is als volgt:</span><span class="sxs-lookup"><span data-stu-id="eb648-122">The flow is as follows:</span></span>

1. <span data-ttu-id="eb648-123">De gebruiker probeert te krijgen tot een toepassing (bijvoorbeeld de Outlook Web App - https://outlook.office365.com/owa/) van een domein, zakelijke apparaat binnen uw bedrijfsnetwerk.</span><span class="sxs-lookup"><span data-stu-id="eb648-123">The user tries to access an application (for example, the Outlook Web App - https://outlook.office365.com/owa/) from a domain-joined corporate device inside your corporate network.</span></span>
2. <span data-ttu-id="eb648-124">Als de gebruiker niet is al aangemeld, wordt de gebruiker omgeleid naar de aanmeldingspagina van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb648-124">If the user is not already signed in, the user is redirected to the Azure AD sign-in page.</span></span>

  >[!NOTE]
  ><span data-ttu-id="eb648-125">Als de Azure AD-in de aanvraag bevat een `domain_hint` (identificeren uw tenant - bijvoorbeeld, contoso.onmicrosoft.com) of `login_hint` (identificatie van de gebruiker - bijvoorbeeld user@contoso.onmicrosoft.com of user@contoso.com) parameter en klik vervolgens stap 2 wordt overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="eb648-125">If the Azure AD sign-in request includes a `domain_hint` (identifying your tenant- for example, contoso.onmicrosoft.com) or `login_hint` (identifying the user - for example, user@contoso.onmicrosoft.com or user@contoso.com) parameter, then step 2 is skipped.</span></span>

3. <span data-ttu-id="eb648-126">De gebruiker typt de naam van de gebruiker naar de aanmeldingspagina van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb648-126">The user types in their user name into the Azure AD sign-in page.</span></span>
4. <span data-ttu-id="eb648-127">Voor informatie over het gebruik van JavaScript in de achtergrond van de uitdagingen Azure AD van de browser, via een 401-niet-geautoriseerde respons, zodat een Kerberos-ticket.</span><span class="sxs-lookup"><span data-stu-id="eb648-127">Using JavaScript in the background, Azure AD challenges the browser, via a 401 Unauthorized response, to provide a Kerberos ticket.</span></span>
5. <span data-ttu-id="eb648-128">Op zijn beurt vraagt de browser een ticket van Active Directory voor de `AZUREADSSOACCT` computeraccount (die staat voor Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eb648-128">The browser, in turn, requests a ticket from Active Directory for the `AZUREADSSOACCT` computer account (which represents Azure AD).</span></span>
6. <span data-ttu-id="eb648-129">Active Directory wordt gezocht naar de computeraccount en retourneert een Kerberos-ticket en de browser die is versleuteld met het computeraccount geheim.</span><span class="sxs-lookup"><span data-stu-id="eb648-129">Active Directory locates the computer account and returns a Kerberos ticket to the browser encrypted with the computer account's secret.</span></span>
7. <span data-ttu-id="eb648-130">De browser stuurt het Kerberos-ticket die is verkregen van Active Directory naar Azure AD (op een van de [Azure AD-URL's eerder zijn toegevoegd aan de browser Intranet-beveiligingszone-instellingen](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span><span class="sxs-lookup"><span data-stu-id="eb648-130">The browser forwards the Kerberos ticket it acquired from Active Directory to Azure AD (on one of the [Azure AD URLs previously added to the browser's Intranet zone settings](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span></span>
8. <span data-ttu-id="eb648-131">Azure AD ontsleutelt het Kerberos-ticket, waaronder de identiteit van de gebruiker aangemeld bij het bedrijfsapparaat met de eerder gedeelde sleutel.</span><span class="sxs-lookup"><span data-stu-id="eb648-131">Azure AD decrypts the Kerberos ticket, which includes the identity of the user signed into the corporate device, using the previously shared key.</span></span>
9. <span data-ttu-id="eb648-132">Na evaluatie, is Azure AD retourneert een token terug naar de toepassing of de gebruiker extra bewijzen, zoals multi-factor Authentication uitvoeren wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="eb648-132">After evaluation, Azure AD either returns a token back to the application or asks the user to perform additional proofs, such as Multi-Factor Authentication.</span></span>
10. <span data-ttu-id="eb648-133">Als de gebruiker aanmelden geslaagd is, wordt de gebruiker toegang tot de toepassing is.</span><span class="sxs-lookup"><span data-stu-id="eb648-133">If the user sign-in is successful, the user is able to access the application.</span></span>

<span data-ttu-id="eb648-134">Het volgende diagram illustreert de onderdelen en de vereiste stappen.</span><span class="sxs-lookup"><span data-stu-id="eb648-134">The following diagram illustrates all the components and the steps involved.</span></span>

![Naadloze eenmalige aanmelding](./media/active-directory-aadconnect-sso/sso2.png)

<span data-ttu-id="eb648-136">Naadloze eenmalige aanmelding is opportunistisch, dat als dit mislukt, de aanmeldingservaring terugvalt op het normale gedrag - eenledige, de gebruiker moet invoeren van hun wachtwoord aan te melden.</span><span class="sxs-lookup"><span data-stu-id="eb648-136">Seamless SSO is opportunistic, which means if it fails, the sign-in experience falls back to its regular behavior - i.e, the user needs to enter their password to sign in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb648-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="eb648-137">Next steps</span></span>

- <span data-ttu-id="eb648-138">[**Snel starten** ](active-directory-aadconnect-sso-quick-start.md) - laten en Azure AD naadloze eenmalige aanmelding wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="eb648-138">[**Quick Start**](active-directory-aadconnect-sso-quick-start.md) - Get up and running Azure AD Seamless SSO.</span></span>
- <span data-ttu-id="eb648-139">[**Veelgestelde vragen** ](active-directory-aadconnect-sso-faq.md) -antwoorden op veelgestelde vragen.</span><span class="sxs-lookup"><span data-stu-id="eb648-139">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="eb648-140">[**Problemen met** ](active-directory-aadconnect-troubleshoot-sso.md) -informatie over het oplossen van veelvoorkomende problemen met de functie.</span><span class="sxs-lookup"><span data-stu-id="eb648-140">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="eb648-141">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - voor de nieuwe functieaanvragen indienen.</span><span class="sxs-lookup"><span data-stu-id="eb648-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
