---
title: 'Azure AD Connect: Pass through-verificatie - hoe het werkt? | Microsoft Docs'
description: In dit artikel wordt beschreven hoe de Azure Active Directory Pass-through-verificatie werkt.
services: active-directory
keywords: Azure AD Connect Pass through-verificatie, install Active Directory onderdelen vereist voor Azure AD, SSO, Single Sign-on
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: ffcebee572a9ba2840e81250651dea45599d65d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a><span data-ttu-id="af223-105">Azure Active Directory Pass-through-verificatie: Technische diepgaand</span><span class="sxs-lookup"><span data-stu-id="af223-105">Azure Active Directory Pass-through Authentication: Technical deep dive</span></span>

>[!IMPORTANT]
><span data-ttu-id="af223-106">Azure AD Pass-through-verificatie is momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="af223-106">Azure AD Pass-through Authentication is currently in preview.</span></span> 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a><span data-ttu-id="af223-107">Hoe werkt Azure Active Directory Pass-through-verificatie?</span><span class="sxs-lookup"><span data-stu-id="af223-107">How does Azure Active Directory Pass-through Authentication work?</span></span>

<span data-ttu-id="af223-108">Wanneer een gebruiker probeert toosign in een toepassing die wordt beveiligd door Azure Active Directory (Azure AD) en Hallo als Pass through-verificatie is ingeschakeld op Hallo-tenant, worden de volgende stappen plaats:</span><span class="sxs-lookup"><span data-stu-id="af223-108">When a user attempts toosign into an application secured by Azure Active Directory (Azure AD), and if Pass-through Authentication is enabled on hello tenant, hello following steps occur:</span></span>

1. <span data-ttu-id="af223-109">Hallo gebruiker probeert een toepassing tooaccess (bijvoorbeeld Hallo Outlook Web App - https://outlook.office365.com/owa/).</span><span class="sxs-lookup"><span data-stu-id="af223-109">hello user tries tooaccess an application (for example, hello Outlook Web App - https://outlook.office365.com/owa/).</span></span>
2. <span data-ttu-id="af223-110">Als het Hallo-gebruiker is niet al aangemeld, is Hallo gebruiker omgeleide toohello Azure AD-aanmeldingspagina.</span><span class="sxs-lookup"><span data-stu-id="af223-110">If hello user is not already signed in, hello user is redirected toohello Azure AD sign-in page.</span></span>
3. <span data-ttu-id="af223-111">Hallo gebruiker voert hun gebruikersnaam en wachtwoord in hello Azure AD-aanmeldingspagina en klikt op 'Aanmelden' Hallo-knop.</span><span class="sxs-lookup"><span data-stu-id="af223-111">hello user enters their username and password into hello Azure AD sign-in page and clicks hello "Sign in" button.</span></span>
4. <span data-ttu-id="af223-112">Azure AD, op de ontvangst van Hallo aanmelden aanvraag wordt Hallo-gebruikersnaam en wachtwoord (versleuteld met een openbare sleutel) op een wachtrij geplaatst.</span><span class="sxs-lookup"><span data-stu-id="af223-112">Azure AD, on receiving hello sign-in request, places hello username and password (encrypted  using a public key) on a queue.</span></span>
5. <span data-ttu-id="af223-113">Een Pass through-verificatie op lokale agent een toohello aanroep van de uitgaande wachtrij maakt en haalt Hallo gebruikersnaam en het versleutelde wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="af223-113">An on-premises Pass-through Authentication agent makes an outbound call toohello queue and retrieves hello username and encrypted password.</span></span>
6. <span data-ttu-id="af223-114">Hallo agent ontsleutelt Hallo-wachtwoord met behulp van de persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="af223-114">hello agent decrypts hello password using its private key.</span></span>
7. <span data-ttu-id="af223-115">Hallo-agent controleert vervolgens Hallo gebruikersnaam en wachtwoord op basis van Active Directory met standaard Windows-API's (een vergelijkbaar mechanisme toowhat wordt gebruikt door Active Directory Federation Services).</span><span class="sxs-lookup"><span data-stu-id="af223-115">hello agent then validates hello username and password against Active Directory using standard Windows APIs (a similar mechanism toowhat is used by Active Directory Federation Services).</span></span> <span data-ttu-id="af223-116">Hallo gebruikersnaam mag de standaardgebruikersnaam van beide Hallo lokale (meestal `userPrincipalName`) of een ander kenmerk in Azure AD Connect geconfigureerd (ook wel `Alternate ID`).</span><span class="sxs-lookup"><span data-stu-id="af223-116">hello username can be either hello on-premises default username (usually `userPrincipalName`) or another attribute configured in Azure AD Connect (known as `Alternate ID`).</span></span>
8. <span data-ttu-id="af223-117">Hallo lokale Active Directory domeincontroller (DC) en vervolgens wordt Hallo aanvraag geëvalueerd en retourneert de juiste reactie Hallo (geslaagd, mislukt, wachtwoord verlopen of gebruiker vergrendeld) toohello agent.</span><span class="sxs-lookup"><span data-stu-id="af223-117">hello on-premises Active Directory Domain Controller (DC) then evaluates hello request and returns hello appropriate response (success, failure, password expired or user locked out) toohello agent.</span></span>
9. <span data-ttu-id="af223-118">Hallo-agent wordt op zijn beurt dit antwoord back tooAzure AD retourneert.</span><span class="sxs-lookup"><span data-stu-id="af223-118">hello agent, in turn, returns this response back tooAzure AD.</span></span>
10. <span data-ttu-id="af223-119">Azure AD evalueert antwoord Hallo en gebruiker toohello reageert - bijvoorbeeld deze zich aanmeldt Hallo gebruiker direct of aanvragen voor multi-factor Authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="af223-119">Azure AD evaluates hello response and responds toohello user as appropriate - for example, it either signs hello user in immediately or requests for Multi-Factor Authentication (MFA).</span></span>
11. <span data-ttu-id="af223-120">Als Hallo gebruiker aanmelden geslaagd is, is Hallo gebruiker kunnen tooaccess Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="af223-120">If hello user sign-in is successful, hello user is able tooaccess hello application.</span></span>

<span data-ttu-id="af223-121">Hallo volgende diagram ziet u alle onderdelen van Hallo en Hallo stappen die nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="af223-121">hello following diagram illustrates all hello components and hello steps involved.</span></span>

![Pass-through-verificatie](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a><span data-ttu-id="af223-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="af223-123">Next steps</span></span>
- <span data-ttu-id="af223-124">[**Huidige beperkingen** ](active-directory-aadconnect-pass-through-authentication-current-limitations.md) -met deze functie is momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="af223-124">[**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - This feature is currently in preview.</span></span> <span data-ttu-id="af223-125">Informatie over welke scenario's worden ondersteund en welke niet.</span><span class="sxs-lookup"><span data-stu-id="af223-125">Learn which scenarios are supported and which ones are not.</span></span>
- <span data-ttu-id="af223-126">[**Snel starten** ](active-directory-aadconnect-pass-through-authentication-quick-start.md) - laten en Azure AD Pass-through-verificatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="af223-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="af223-127">[**Veelgestelde vragen** ](active-directory-aadconnect-pass-through-authentication-faq.md) -toofrequently vragen worden beantwoord.</span><span class="sxs-lookup"><span data-stu-id="af223-127">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="af223-128">[**Problemen met** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -informatie over hoe tooresolve algemene problemen met een Hallo-functie.</span><span class="sxs-lookup"><span data-stu-id="af223-128">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="af223-129">[**Azure AD naadloze eenmalige aanmelding** ](active-directory-aadconnect-sso.md) -meer informatie over deze aanvullende functie.</span><span class="sxs-lookup"><span data-stu-id="af223-129">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="af223-130">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - voor de nieuwe functieaanvragen indienen.</span><span class="sxs-lookup"><span data-stu-id="af223-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
