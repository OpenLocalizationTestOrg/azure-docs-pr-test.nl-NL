---
title: 'Azure AD Connect: Pass through-verificatie - Smart accountvergrendeling | Microsoft Docs'
description: Dit artikel wordt beschreven hoe Pass-through-verificatie voor Azure Active Directory (Azure AD) beveiligd met uw lokale accounts van wachtwoord beveiligingsaanvallen in Hallo cloud.
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
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: b02e315c3cc3eae00ca6408d735a416f34c2cdc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-smart-lockout"></a><span data-ttu-id="4a7eb-104">Pass-through-verificatie van Azure Active Directory: Smart accountvergrendeling</span><span class="sxs-lookup"><span data-stu-id="4a7eb-104">Azure Active Directory Pass-through Authentication: Smart Lockout</span></span>

## <a name="overview"></a><span data-ttu-id="4a7eb-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="4a7eb-105">Overview</span></span>

<span data-ttu-id="4a7eb-106">Azure AD biedt bescherming tegen beveiligingsaanvallen wachtwoord en voorkomt dat legitieme gebruikers hun Office 365 en SaaS-toepassingen wordt vergrendeld.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-106">Azure AD protects against brute force password attacks and prevents genuine users from being locked out of their Office 365 and SaaS applications.</span></span> <span data-ttu-id="4a7eb-107">Deze mogelijkheid, aangeroepen **Smart accountvergrendeling**, wordt ondersteund als u Pass-through-verificatie als uw contactmethode aanmelden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-107">This capability, called **Smart Lockout**, is supported when you use Pass-through Authentication as your sign-in method.</span></span> <span data-ttu-id="4a7eb-108">Smartcard-vergrendeling is standaard ingeschakeld voor alle tenants en beveiligt uw gebruikersaccounts alle Hallo tijd; Er is geen tooturn nodig op.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-108">Smart Lockout is enabled by default for all tenants and are protecting your user accounts all hello time; there is no need tooturn it on.</span></span>

<span data-ttu-id="4a7eb-109">Smart vergrendeling werkt door de mislukte aanmeldpogingen te houden en na een bepaalde **Blokkeringsdrempel**, te beginnen een **vergrendelingsduur**.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-109">Smart Lockout works by keeping track of failed sign-in attempts, and after a certain **Lockout Threshold**, starting a **Lockout Duration**.</span></span> <span data-ttu-id="4a7eb-110">Alle pogingen aanmelden van de aanvaller Hallo tijdens Hallo vergrendelingsduur worden geweigerd.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-110">Any sign-in attempts from hello attacker during hello Lockout Duration are rejected.</span></span> <span data-ttu-id="4a7eb-111">Als Hallo aanval blijft, aanmeldingspogingen Hallo daaropvolgende mislukte nadat Hallo vergrendelingsduur leiden tot een langere duur van de vergrendeling is beëindigd.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-111">If hello attack continues, hello subsequent failed sign-in attempts after hello Lockout Duration ends result in longer Lockout Durations.</span></span>

>[!NOTE]
><span data-ttu-id="4a7eb-112">Hallo standaard Blokkeringsdrempel is 10 mislukte pogingen en Hallo standaard die vergrendelingsduur is 60 seconden.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-112">hello default Lockout Threshold is 10 failed attempts, and hello default Lockout Duration is 60 seconds.</span></span>

<span data-ttu-id="4a7eb-113">Smart accountvergrendeling is ook onderscheid gemaakt tussen de aanmeldingen van legitieme gebruikers en tegen kwaadwillende personen en alleen vergrendeld Hallo aanvallers in de meeste gevallen.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-113">Smart Lockout also distinguishes between sign-ins from genuine users and from attackers and only locks out hello attackers in most cases.</span></span> <span data-ttu-id="4a7eb-114">Deze functionaliteit wordt voorkomen dat aanvallers met kwaadaardige bedoelingen accountvergrendeling legitieme gebruikers.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-114">This functionality prevents attackers from maliciously locking out genuine users.</span></span> <span data-ttu-id="4a7eb-115">We gebruiken uit het verleden aanmelden gedrag, apparaten en browsers en andere signalen toodistinguish tussen legitieme gebruikers en aanvallers van gebruikers.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-115">We use past sign-in behavior, users’ devices & browsers and other signals toodistinguish between genuine users and attackers.</span></span> <span data-ttu-id="4a7eb-116">We zijn voortdurend verbeteren van onze algoritmen.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-116">We are constantly improving our algorithms.</span></span>

<span data-ttu-id="4a7eb-117">Omdat Pass through-verificatie stuurt wachtwoord validatie aanvragen naar uw lokale Active Directory (AD), moet u tooprevent aanvallers van uw gebruikers AD-accounts worden vergrendeld.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-117">Because Pass-through Authentication forwards password validation requests onto your on-premises Active Directory (AD), you need tooprevent attackers from locking out your users’ AD accounts.</span></span> <span data-ttu-id="4a7eb-118">Omdat u uw eigen beleid AD accountvergrendeling hebt (met name [ **Accountvergrendelingsdrempel** ](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) en [ **beleid voor opnieuw instellen Account Lockout teller na** ](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), moet u de Blokkeringsdrempel tooconfigure Azure AD en vergrendelingsduur waarden op de juiste wijze toofilter uit aanvallen in Hallo cloud voordat ze bereiken met uw on-premises AD.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-118">Since you have your own AD Account Lockout policies (specifically, [**Account Lockout Threshold**](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) and [**Reset Account Lockout Counter After policies**](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), you need tooconfigure Azure AD’s Lockout Threshold and Lockout Duration values appropriately toofilter out attacks in hello cloud before they reach your on-premises AD.</span></span>

>[!NOTE]
><span data-ttu-id="4a7eb-119">Hallo Smart accountvergrendeling is gratis en is _op_ standaard voor alle klanten.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-119">hello Smart Lockout feature is free and is _on_ by default for all customers.</span></span> <span data-ttu-id="4a7eb-120">Wijzigen van de Blokkeringsdrempel en de vergrendelingsduur waarden Graph API met Azure AD heeft uw tenant toohave ten minste één Azure AD Premium P2-licentie nodig.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-120">However, modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API needs your tenant toohave at least one Azure AD Premium P2 license.</span></span> <span data-ttu-id="4a7eb-121">U hoeft niet met een licentie voor Azure AD Premium-P2 _per gebruiker_ tooget Hallo Smart accountvergrendeling met Pass through-verificatie.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-121">You don't need an Azure AD Premium P2 license _per user_ tooget hello Smart Lockout feature with Pass-through Authentication.</span></span>

<span data-ttu-id="4a7eb-122">tooensure dat uw gebruikers on-premises AD-accounts zijn beveiligd, moet u tooensure die:</span><span class="sxs-lookup"><span data-stu-id="4a7eb-122">tooensure that your users’ on-premises AD accounts are well protected, you need tooensure that:</span></span>

1.  <span data-ttu-id="4a7eb-123">Azure AD-Blokkeringsdrempel is _minder_ dan de drempelwaarde voor vergrendeling van AD-Account.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-123">Azure AD’s Lockout Threshold is _less_ than AD’s Account Lockout Threshold.</span></span> <span data-ttu-id="4a7eb-124">Wij raden Hallo waarden in te stellen zodat AD van Accountvergrendelingsdrempel ten minste twee is of drie keer Blokkeringsdrempel Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-124">We recommend that you set hello values such that AD’s Account Lockout Threshold is at least two or three times Azure AD’s Lockout Threshold.</span></span>
2.  <span data-ttu-id="4a7eb-125">Azure AD-vergrendelingsduur (weergegeven in seconden) is _langer_ dan van AD opnieuw Account Lockout teller na (weergegeven in minuten).</span><span class="sxs-lookup"><span data-stu-id="4a7eb-125">Azure AD’s Lockout Duration (represented in seconds) is _longer_ than AD’s Reset Account Lockout Counter After (represented in minutes).</span></span>

## <a name="verify-your-ad-account-lockout-policies"></a><span data-ttu-id="4a7eb-126">Controleer of uw AD-accountvergrendeling-beleid</span><span class="sxs-lookup"><span data-stu-id="4a7eb-126">Verify your AD Account Lockout policies</span></span>

<span data-ttu-id="4a7eb-127">Hallo instructies tooverify na een accountvergrendeling AD-beleid gebruiken:</span><span class="sxs-lookup"><span data-stu-id="4a7eb-127">Use hello following instructions tooverify your AD Account Lockout policies:</span></span>

1.  <span data-ttu-id="4a7eb-128">Open het Hallo Group Policy Management-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-128">Open hello Group Policy Management tool.</span></span>
2.  <span data-ttu-id="4a7eb-129">Hallo Groepsbeleid bewerken die is toegepast tooall gebruikers, bijvoorbeeld Hallo standaarddomeinbeleid.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-129">Edit hello group policy that is applied tooall users, for example, hello Default Domain Policy.</span></span>
3.  <span data-ttu-id="4a7eb-130">Navigeer tooComputer Computerconfiguratie\Beleid\Windows Settings\Security Instellingen\beveiligingsinstellingen\accountbeleid\accountvergrendelingsbeleid.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-130">Navigate tooComputer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Account Lockout Policy.</span></span>
4.  <span data-ttu-id="4a7eb-131">Controleer of uw Accountvergrendelingsdrempel en stellen Account Lockout teller na waarden.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-131">Verify your Account Lockout Threshold and Reset Account Lockout Counter After values.</span></span>

![AD accountvergrendeling beleid](./media/active-directory-aadconnect-pass-through-authentication/pta5.png)

## <a name="use-hello-graph-api-toomanage-your-tenants-smart-lockout-values"></a><span data-ttu-id="4a7eb-133">Hallo Graph API toomanage van uw tenant Smart accountvergrendeling waarden gebruiken</span><span class="sxs-lookup"><span data-stu-id="4a7eb-133">Use hello Graph API toomanage your tenant’s Smart Lockout values</span></span>

>[!IMPORTANT]
><span data-ttu-id="4a7eb-134">Wijzigen van de Blokkeringsdrempel en de vergrendelingsduur waarden Graph API met Azure AD is een Azure AD Premium P2-functie.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-134">Modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API is an Azure AD Premium P2 feature.</span></span> <span data-ttu-id="4a7eb-135">Ook moet u toobe een globale beheerder zijn op uw tenant.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-135">It also needs you toobe a Global Administrator on your tenant.</span></span>

<span data-ttu-id="4a7eb-136">U kunt [grafiek Explorer](https://developer.microsoft.com/graph/graph-explorer) tooread, ingesteld en Azure AD Smart accountvergrendeling waarden bijwerken.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-136">You can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) tooread, set, and update Azure AD’s Smart Lockout values.</span></span> <span data-ttu-id="4a7eb-137">Maar u kunt deze bewerkingen ook programmatisch doen.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-137">But you can also do these operations programmatically.</span></span>

### <a name="read-smart-lockout-values"></a><span data-ttu-id="4a7eb-138">Waarden van de smartcard accountvergrendeling lezen</span><span class="sxs-lookup"><span data-stu-id="4a7eb-138">Read Smart Lockout values</span></span>

<span data-ttu-id="4a7eb-139">Volg deze stappen tooread van uw tenant Smart accountvergrendeling waarden:</span><span class="sxs-lookup"><span data-stu-id="4a7eb-139">Follow these steps tooread your tenant’s Smart Lockout values:</span></span>

1. <span data-ttu-id="4a7eb-140">Meld u aan bij de grafiek Explorer als globale beheerder van uw tenant.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-140">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="4a7eb-141">Als u wordt gevraagd, aangevraagde toegang verlenen voor Hallo machtigingen.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-141">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="4a7eb-142">Klik op 'Machtigingen wijzigen' en selecteer Hallo 'Directory.ReadWrite.All' machtiging.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-142">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="4a7eb-143">Hallo Graph API-aanvraag als volgt configureren: Stel de versie te "BÈTAVERSIE" aanvraagtype te 'ophalen' en de URL te`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-143">Configure hello Graph API request as follows: Set version too“BETA”, request type too“GET” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="4a7eb-144">Klikt u op 'Query uitvoeren' toosee van uw tenant Smart accountvergrendeling waarden.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-144">Click "Run Query" toosee your tenant's Smart Lockout values.</span></span> <span data-ttu-id="4a7eb-145">Als u waarden voor uw tenant voordat dit nog niet hebt ingesteld, ziet u een lege set.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-145">If you haven't set your tenant's values before, you see an empty set.</span></span>

### <a name="set-smart-lockout-values"></a><span data-ttu-id="4a7eb-146">Smart accountvergrendeling waarden instellen</span><span class="sxs-lookup"><span data-stu-id="4a7eb-146">Set Smart Lockout values</span></span>

<span data-ttu-id="4a7eb-147">Volg deze stappen tooset van uw tenant Smart accountvergrendeling waarden (voor Hallo alleen de eerste keer):</span><span class="sxs-lookup"><span data-stu-id="4a7eb-147">Follow these steps tooset your tenant’s Smart Lockout values (for hello first time only):</span></span>

1. <span data-ttu-id="4a7eb-148">Meld u aan bij de grafiek Explorer als globale beheerder van uw tenant.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-148">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="4a7eb-149">Als u wordt gevraagd, aangevraagde toegang verlenen voor Hallo machtigingen.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-149">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="4a7eb-150">Klik op 'Machtigingen wijzigen' en selecteer Hallo 'Directory.ReadWrite.All' machtiging.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-150">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="4a7eb-151">Hallo Graph API-aanvraag als volgt configureren: Stel de versie te "BÈTAVERSIE" aanvraagtype te 'posten' en de URL te`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-151">Configure hello Graph API request as follows: Set version too“BETA”, request type too“POST” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="4a7eb-152">Kopieer en plak de volgende JSON-aanvraag naar Hallo 'Aanvraag hoofdtekst' veld Hallo.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-152">Copy and paste hello following JSON request into hello "Request Body" field.</span></span> <span data-ttu-id="4a7eb-153">Hallo Smart accountvergrendeling waarden waar nodig wijzigen en gebruiken van een willekeurige GUID voor `templateId`.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-153">Change hello Smart Lockout values as appropriate and use a random GUID for `templateId`.</span></span>
5. <span data-ttu-id="4a7eb-154">Klikt u op 'Query uitvoeren' tooset van uw tenant Smart accountvergrendeling waarden.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-154">Click "Run Query" tooset your tenant's Smart Lockout values.</span></span>

```
{
  "templateId": "5cf42378-d67d-4f36-ba46-e8b86229381d",
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "300"
    },
    {
      "name": "LockoutThreshold",
      "value": "5"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

>[!NOTE]
><span data-ttu-id="4a7eb-155">Als u deze niet gebruikt, kunt u Hallo laten **BannedPasswordList** en **EnableBannedPasswordCheck** waarden als leeg ("") en 'false' respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-155">If you are not using them, you can leave hello **BannedPasswordList** and **EnableBannedPasswordCheck** values as empty ("") and "false" respectively.</span></span>

<span data-ttu-id="4a7eb-156">Controleer of u van uw tenant Smart accountvergrendeling waarden correct hebt ingesteld [deze stappen](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="4a7eb-156">Verify that you have set your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

### <a name="update-smart-lockout-values"></a><span data-ttu-id="4a7eb-157">Smart accountvergrendeling waarden bijwerken</span><span class="sxs-lookup"><span data-stu-id="4a7eb-157">Update Smart Lockout values</span></span>

<span data-ttu-id="4a7eb-158">Volg deze stappen tooupdate van uw tenant Smart accountvergrendeling waarden (als u deze voordat u al hebt ingesteld):</span><span class="sxs-lookup"><span data-stu-id="4a7eb-158">Follow these steps tooupdate your tenant’s Smart Lockout values (if you have already set them before):</span></span>

1. <span data-ttu-id="4a7eb-159">Meld u aan bij de grafiek Explorer als globale beheerder van uw tenant.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-159">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="4a7eb-160">Als u wordt gevraagd, aangevraagde toegang verlenen voor Hallo machtigingen.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-160">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="4a7eb-161">Klik op 'Machtigingen wijzigen' en selecteer Hallo 'Directory.ReadWrite.All' machtiging.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-161">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="4a7eb-162">[Volg deze stappen tooread van uw tenant Smart accountvergrendeling waarden](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="4a7eb-162">[Follow these steps tooread your tenant's Smart Lockout values](#read-smart-lockout-values).</span></span> <span data-ttu-id="4a7eb-163">Kopiëren Hallo `id` waarde (GUID) van het Hallo-item met 'weergavenaam' als 'PasswordRuleSettings'.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-163">Copy hello `id` value (a GUID) of hello item with "displayName" as "PasswordRuleSettings".</span></span>
4. <span data-ttu-id="4a7eb-164">Hallo Graph API-aanvraag als volgt configureren: Stel de versie te "BÈTAVERSIE" aanvraagtype te 'PATCH' en de URL te`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` -gebruiken Hallo GUID vanaf stap 3 voor `<id>`.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-164">Configure hello Graph API request as follows: Set version too“BETA”, request type too“PATCH” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` - use hello GUID from Step 3 for `<id>`.</span></span>
5. <span data-ttu-id="4a7eb-165">Kopieer en plak de volgende JSON-aanvraag naar Hallo 'Aanvraag hoofdtekst' veld Hallo.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-165">Copy and paste hello following JSON request into hello "Request Body" field.</span></span> <span data-ttu-id="4a7eb-166">Hallo Smart accountvergrendeling waarden zo nodig wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-166">Change hello Smart Lockout values as appropriate.</span></span>
6. <span data-ttu-id="4a7eb-167">Klikt u op 'Query uitvoeren' tooupdate van uw tenant Smart accountvergrendeling waarden.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-167">Click "Run Query" tooupdate your tenant's Smart Lockout values.</span></span>

```
{
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "30"
    },
    {
      "name": "LockoutThreshold",
      "value": "4"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

<span data-ttu-id="4a7eb-168">Controleer of u hebt uw tenant Smart accountvergrendeling waarden correct met bijgewerkt [deze stappen](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="4a7eb-168">Verify that you have updated your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a7eb-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4a7eb-169">Next steps</span></span>
- <span data-ttu-id="4a7eb-170">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - voor de nieuwe functieaanvragen indienen.</span><span class="sxs-lookup"><span data-stu-id="4a7eb-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
