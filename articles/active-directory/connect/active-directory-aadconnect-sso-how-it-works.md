---
title: 'Azure AD Connect: Naadloze eenmalige aanmelding - werking | Microsoft Docs'
description: Dit artikel wordt beschreven hoe hello Azure Active Directory naadloze eenmalige aanmelding functie werkt.
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
ms.openlocfilehash: 17ce35b32832d241068ab878cf7aac42deab74ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a><span data-ttu-id="c3e92-104">Azure Active Directory naadloze eenmalige aanmelding: technische diepgaand</span><span class="sxs-lookup"><span data-stu-id="c3e92-104">Azure Active Directory Seamless Single Sign-On: Technical deep dive</span></span>

<span data-ttu-id="c3e92-105">In dit artikel biedt u technische gegevens in de werking van hello Azure Active Directory naadloze eenmalige aanmelding (SSO naadloze) functie.</span><span class="sxs-lookup"><span data-stu-id="c3e92-105">This article gives you technical details into how hello Azure Active Directory Seamless Single Sign-On (Seamless SSO) feature works.</span></span>

>[!IMPORTANT]
><span data-ttu-id="c3e92-106">Hallo naadloze SSO-functie is momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="c3e92-106">hello Seamless SSO feature is currently in preview.</span></span>

## <a name="how-does-seamless-sso-work"></a><span data-ttu-id="c3e92-107">Hoe werkt naadloze eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c3e92-107">How does Seamless SSO work?</span></span>

<span data-ttu-id="c3e92-108">Deze sectie heeft twee onderdelen tooit:</span><span class="sxs-lookup"><span data-stu-id="c3e92-108">This section has two parts tooit:</span></span>
1. <span data-ttu-id="c3e92-109">Hallo-instelling van Hallo naadloze SSO-functie.</span><span class="sxs-lookup"><span data-stu-id="c3e92-109">hello setup of hello Seamless SSO feature.</span></span>
2. <span data-ttu-id="c3e92-110">Hoe werkt een enkele gebruiker aanmelden transactie met naadloze eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c3e92-110">How a single user sign-in transaction works with Seamless SSO.</span></span>

### <a name="how-does-set-up-work"></a><span data-ttu-id="c3e92-111">Hoe werken instellen?</span><span class="sxs-lookup"><span data-stu-id="c3e92-111">How does set up work?</span></span>

<span data-ttu-id="c3e92-112">Naadloze eenmalige aanmelding is ingeschakeld via Azure AD Connect zoals [hier](active-directory-aadconnect-sso-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="c3e92-112">Seamless SSO is enabled using Azure AD Connect as shown [here](active-directory-aadconnect-sso-quick-start.md).</span></span> <span data-ttu-id="c3e92-113">Tijdens het inschakelen van de functie Hallo optreden Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c3e92-113">While enabling hello feature, hello following steps occur:</span></span>
- <span data-ttu-id="c3e92-114">Een account met de naam `AZUREADSSOACCT` (geeft Azure AD) is gemaakt in uw on-premises Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="c3e92-114">A computer account named `AZUREADSSOACCT` (which represents Azure AD) is created in your on-premises Active Directory (AD).</span></span>
- <span data-ttu-id="c3e92-115">Hallo computeraccount Kerberos ontsleutelingssleutel wordt veilig worden gedeeld met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3e92-115">hello computer account's Kerberos decryption key is shared securely with Azure AD.</span></span>
- <span data-ttu-id="c3e92-116">Twee Kerberos-SPN-namen (SPN's) gemaakt bovendien twee URL's voor een toorepresent die worden gebruikt tijdens het aanmelden van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3e92-116">In addition, two Kerberos service principal names (SPNs) are created toorepresent two URLs that are used during Azure AD sign-in.</span></span>

>[!NOTE]
> <span data-ttu-id="c3e92-117">Hallo-computeraccount en Hallo Kerberos-SPN's worden gemaakt in elk AD-forest u tooAzure AD synchroniseren (met behulp van Azure AD Connect) en gebruikers voor wie u wilt dat naadloze eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c3e92-117">hello computer account and hello Kerberos SPNs are created in each AD forest you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want Seamless SSO.</span></span> <span data-ttu-id="c3e92-118">Hallo verplaatsen `AZUREADSSOACCT` computer account tooan organisatie-eenheid (OE) waar de computeraccounts van andere opgeslagen tooensure die wordt beheerd zijn in dezelfde Hallo manier en is niet verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c3e92-118">Move hello `AZUREADSSOACCT` computer account tooan Organization Unit (OU) where other computer accounts are stored tooensure that it is managed in hello same way and is not deleted.</span></span>

>[!IMPORTANT]
><span data-ttu-id="c3e92-119">Ten zeerste aangeraden dat u [overschakelen Hallo Kerberos ontsleutelingssleutel](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) Hallo `AZUREADSSOACCT` computeraccount ten minste elke 30 dagen.</span><span class="sxs-lookup"><span data-stu-id="c3e92-119">We highly recommend that you [roll over hello Kerberos decryption key](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) of hello `AZUREADSSOACCT` computer account at least every 30 days.</span></span>

### <a name="how-does-sign-in-with-seamless-sso-work"></a><span data-ttu-id="c3e92-120">Hoe aanmelden met naadloze eenmalige aanmelding werk?</span><span class="sxs-lookup"><span data-stu-id="c3e92-120">How does sign-in with Seamless SSO work?</span></span>

<span data-ttu-id="c3e92-121">Zodra het Hallo-installatie is voltooid, werkt naadloos SSO Hallo dezelfde manier als andere aanmelden die gebruikmaakt van geïntegreerde Windows-verificatie (IWA).</span><span class="sxs-lookup"><span data-stu-id="c3e92-121">Once hello set-up is complete, Seamless SSO works hello same way as any other sign-in that uses Integrated Windows Authentication (IWA).</span></span> <span data-ttu-id="c3e92-122">Hallo-stroom is als volgt:</span><span class="sxs-lookup"><span data-stu-id="c3e92-122">hello flow is as follows:</span></span>

1. <span data-ttu-id="c3e92-123">Hallo gebruiker probeert een toepassing tooaccess (bijvoorbeeld Hallo Outlook Web App - https://outlook.office365.com/owa/) van een domein, zakelijke apparaat binnen uw bedrijfsnetwerk.</span><span class="sxs-lookup"><span data-stu-id="c3e92-123">hello user tries tooaccess an application (for example, hello Outlook Web App - https://outlook.office365.com/owa/) from a domain-joined corporate device inside your corporate network.</span></span>
2. <span data-ttu-id="c3e92-124">Als het Hallo-gebruiker is niet al aangemeld, is Hallo gebruiker omgeleide toohello Azure AD-aanmeldingspagina.</span><span class="sxs-lookup"><span data-stu-id="c3e92-124">If hello user is not already signed in, hello user is redirected toohello Azure AD sign-in page.</span></span>

  >[!NOTE]
  ><span data-ttu-id="c3e92-125">Als hello Azure AD-aanmelden-aanvraag bevat een `domain_hint` (identificeren uw tenant - bijvoorbeeld, contoso.onmicrosoft.com) of `login_hint` (Hallo gebruiker - bijvoorbeeld identificeren user@contoso.onmicrosoft.com of user@contoso.com) parameter en klik vervolgens stap 2 wordt overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="c3e92-125">If hello Azure AD sign-in request includes a `domain_hint` (identifying your tenant- for example, contoso.onmicrosoft.com) or `login_hint` (identifying hello user - for example, user@contoso.onmicrosoft.com or user@contoso.com) parameter, then step 2 is skipped.</span></span>

3. <span data-ttu-id="c3e92-126">Hallo gebruikerstypen in hun gebruikersnaam in de aanmeldingspagina hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3e92-126">hello user types in their user name into hello Azure AD sign-in page.</span></span>
4. <span data-ttu-id="c3e92-127">Als u JavaScript in Hallo achtergrond, uitdagingen Azure AD Hallo browser via een 401 onbevoegde antwoord tooprovide een Kerberos-ticket.</span><span class="sxs-lookup"><span data-stu-id="c3e92-127">Using JavaScript in hello background, Azure AD challenges hello browser, via a 401 Unauthorized response, tooprovide a Kerberos ticket.</span></span>
5. <span data-ttu-id="c3e92-128">Hallo-browser op hun beurt vraagt een ticket uit Active Directory voor Hallo `AZUREADSSOACCT` computeraccount (die staat voor Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c3e92-128">hello browser, in turn, requests a ticket from Active Directory for hello `AZUREADSSOACCT` computer account (which represents Azure AD).</span></span>
6. <span data-ttu-id="c3e92-129">Active Directory Hallo computeraccount zoekt en retourneert een Kerberos-ticket toohello browser versleuteld met Hallo computeraccount geheim.</span><span class="sxs-lookup"><span data-stu-id="c3e92-129">Active Directory locates hello computer account and returns a Kerberos ticket toohello browser encrypted with hello computer account's secret.</span></span>
7. <span data-ttu-id="c3e92-130">Hallo browser stuurt Hallo Kerberos-ticket die is verkregen van Active Directory tooAzure AD (op een van de Hallo [Azure AD-URL's van de browser toohello Intranet-beveiligingszone-instellingen hebt toegevoegd](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span><span class="sxs-lookup"><span data-stu-id="c3e92-130">hello browser forwards hello Kerberos ticket it acquired from Active Directory tooAzure AD (on one of hello [Azure AD URLs previously added toohello browser's Intranet zone settings](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span></span>
8. <span data-ttu-id="c3e92-131">Azure AD ontsleuteld Hallo Kerberos-ticket, waaronder Hallo identiteit van Hallo gebruiker is aangemeld bij bedrijfsapparaten Hallo Hallo eerder gebruikte gedeelde sleutel.</span><span class="sxs-lookup"><span data-stu-id="c3e92-131">Azure AD decrypts hello Kerberos ticket, which includes hello identity of hello user signed into hello corporate device, using hello previously shared key.</span></span>
9. <span data-ttu-id="c3e92-132">Na evaluatie, is Azure AD retourneert een token terug toohello toepassing of vraagt Hallo gebruiker tooperform aanvullende bewijzen, zoals multi-factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="c3e92-132">After evaluation, Azure AD either returns a token back toohello application or asks hello user tooperform additional proofs, such as Multi-Factor Authentication.</span></span>
10. <span data-ttu-id="c3e92-133">Als Hallo gebruiker aanmelden geslaagd is, is Hallo gebruiker kunnen tooaccess Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c3e92-133">If hello user sign-in is successful, hello user is able tooaccess hello application.</span></span>

<span data-ttu-id="c3e92-134">Hallo volgende diagram ziet u alle onderdelen van Hallo en Hallo stappen die nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="c3e92-134">hello following diagram illustrates all hello components and hello steps involved.</span></span>

![Naadloze eenmalige aanmelding](./media/active-directory-aadconnect-sso/sso2.png)

<span data-ttu-id="c3e92-136">Naadloze eenmalige aanmelding is opportunistisch, wat betekent dat als het mislukt, de aanmeldingservaring Hallo terugvalt tooits reguliere gedrag - eenledige, Hallo gebruiker moet tooenter hun toosign wachtwoord in.</span><span class="sxs-lookup"><span data-stu-id="c3e92-136">Seamless SSO is opportunistic, which means if it fails, hello sign-in experience falls back tooits regular behavior - i.e, hello user needs tooenter their password toosign in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3e92-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c3e92-137">Next steps</span></span>

- <span data-ttu-id="c3e92-138">[**Snel starten** ](active-directory-aadconnect-sso-quick-start.md) - laten en Azure AD naadloze eenmalige aanmelding wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c3e92-138">[**Quick Start**](active-directory-aadconnect-sso-quick-start.md) - Get up and running Azure AD Seamless SSO.</span></span>
- <span data-ttu-id="c3e92-139">[**Veelgestelde vragen** ](active-directory-aadconnect-sso-faq.md) -toofrequently vragen worden beantwoord.</span><span class="sxs-lookup"><span data-stu-id="c3e92-139">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="c3e92-140">[**Problemen met** ](active-directory-aadconnect-troubleshoot-sso.md) -informatie over hoe tooresolve algemene problemen met een Hallo-functie.</span><span class="sxs-lookup"><span data-stu-id="c3e92-140">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="c3e92-141">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - voor de nieuwe functieaanvragen indienen.</span><span class="sxs-lookup"><span data-stu-id="c3e92-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
