---
title: aaaSingle tooapps aanmelding met Azure AD-toepassingsproxy | Microsoft Docs
description: Schakel eenmalige aanmelding voor uw gepubliceerde on-premises toepassingen met Azure AD-toepassingsproxy in hello Azure-portal.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5ff288d36163b74215677d9e34c93c985ac33d54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a><span data-ttu-id="58855-103">Wachtwoord voor eenmalige aanmelding met toepassingsproxy vaulting</span><span class="sxs-lookup"><span data-stu-id="58855-103">Password vaulting for single sign-on with Application Proxy</span></span>

<span data-ttu-id="58855-104">Azure Active Directory-toepassingsproxy helpt u bij de productiviteit door on-premises toepassingen publiceren zodat externe werknemers veilig toegang deze te tot verbeteren.</span><span class="sxs-lookup"><span data-stu-id="58855-104">Azure Active Directory Application Proxy helps you improve productivity by publishing on-premises applications so that remote employees can securely access them, too.</span></span> <span data-ttu-id="58855-105">In hello Azure-portal, kunt u ook eenmalige aanmelding (SSO) toothese apps instellen.</span><span class="sxs-lookup"><span data-stu-id="58855-105">In hello Azure portal, you can also set up single sign-on (SSO) toothese apps.</span></span> <span data-ttu-id="58855-106">Uw gebruikers hoeven alleen tooauthenticate met Azure AD en toegang te krijgen tot uw zakelijke toepassing zonder toosign in opnieuw.</span><span class="sxs-lookup"><span data-stu-id="58855-106">Your users only need tooauthenticate with Azure AD, and they can access your enterprise application without having toosign in again.</span></span>

<span data-ttu-id="58855-107">Toepassingsproxy ondersteunt verschillende [eenmalige aanmelding modi](application-proxy-sso-overview.md).</span><span class="sxs-lookup"><span data-stu-id="58855-107">Application Proxy supports several [single sign-on modes](application-proxy-sso-overview.md).</span></span> <span data-ttu-id="58855-108">Op basis van wachtwoorden eenmalige aanmelding is bedoeld voor toepassingen die gebruikmaken van een combinatie van gebruikersnaam en wachtwoord voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="58855-108">Password-based sign-on is intended for applications that use a username/password combination for authentication.</span></span> <span data-ttu-id="58855-109">Wanneer u op basis van wachtwoorden eenmalige aanmelding voor uw toepassing configureert, hebben uw gebruikers toosign in één keer toohello on-premises toepassing.</span><span class="sxs-lookup"><span data-stu-id="58855-109">When you configure password-based sign-on for your application, your users have toosign in toohello on-premises application once.</span></span> <span data-ttu-id="58855-110">Hierna is Azure Active Directory Hallo aanmelden informatie opslaat en automatisch biedt deze toepassing toohello wanneer uw gebruikers toegang op afstand.</span><span class="sxs-lookup"><span data-stu-id="58855-110">After that, Azure Active Directory stores hello sign-in information and automatically provides it toohello application when your users access it remotely.</span></span> 

<span data-ttu-id="58855-111">U moet al hebt gepubliceerd en uw app met toepassingsproxy getest.</span><span class="sxs-lookup"><span data-stu-id="58855-111">You should already have published and tested your app with Application Proxy.</span></span> <span data-ttu-id="58855-112">Als dit niet het geval is, volgt u de stappen Hallo in [toepassingen publiceren met Azure AD-toepassingsproxy](application-proxy-publish-azure-portal.md) vervolgens kun je hier.</span><span class="sxs-lookup"><span data-stu-id="58855-112">If not, follow hello steps in [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md) then come back here.</span></span> 

## <a name="set-up-password-vaulting-for-your-application"></a><span data-ttu-id="58855-113">Wachtwoord voor uw toepassing vaulting instellen</span><span class="sxs-lookup"><span data-stu-id="58855-113">Set up password vaulting for your application</span></span>

1. <span data-ttu-id="58855-114">Meld u aan toohello [Azure-portal](https://portal.azure.com) als beheerder.</span><span class="sxs-lookup"><span data-stu-id="58855-114">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="58855-115">Selecteer **Azure Active Directory** > **bedrijfstoepassingen** > **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="58855-115">Select **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="58855-116">Selecteer in Hallo lijst Hallo-app die u wilt dat tooset up met eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="58855-116">From hello list, select hello app that you want tooset up with SSO.</span></span>  
4. <span data-ttu-id="58855-117">Selecteer **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="58855-117">Select **Single sign-on**.</span></span>

   ![Schakel eenmalige aanmelding](./media/application-proxy-sso-azure-portal/select-sso.png)

5. <span data-ttu-id="58855-119">Kies bij Hallo SSO-modus **op basis van wachtwoorden aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="58855-119">For hello SSO mode, choose **Password-based Sign-on**.</span></span>
6. <span data-ttu-id="58855-120">Voor Hallo aanmeldings-URL, Hallo URL opgeven voor Hallo pagina waar gebruikers hun gebruikersnaam en wachtwoord toosign in tooyour app buiten het bedrijfsnetwerk Hallo invoeren.</span><span class="sxs-lookup"><span data-stu-id="58855-120">For hello Sign-on URL, enter hello URL for hello page where users enter their username and password toosign in tooyour app outside of hello corporate network.</span></span> <span data-ttu-id="58855-121">Kan dit Hallo externe URL die u hebt gemaakt toen u Hallo-app via toepassingsproxy gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="58855-121">This may be hello External URL that you created when you published hello app through Application Proxy.</span></span> 

   ![Kiezen op basis van wachtwoorden eenmalige aanmelding en voer de URL](./media/application-proxy-sso-azure-portal/password-sso.png)

7. <span data-ttu-id="58855-123">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="58855-123">Select **Save**.</span></span>

<!-- Need toorepro?
7. hello page should tell you that a sign-in form was successfully detected at hello provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow hello instructions toopoint out where hello sign-in credentials go. 
-->

## <a name="test-your-app"></a><span data-ttu-id="58855-124">Uw app testen</span><span class="sxs-lookup"><span data-stu-id="58855-124">Test your app</span></span>

<span data-ttu-id="58855-125">Ga tooexternal-URL die u hebt geconfigureerd voor externe toegang tooyour toepassing.</span><span class="sxs-lookup"><span data-stu-id="58855-125">Go tooexternal URL that you configured for remote access tooyour application.</span></span> <span data-ttu-id="58855-126">Aanmelden met uw referenties voor die app (of het Hallo-referenties voor een testaccount dat u toegang hebt ingesteld).</span><span class="sxs-lookup"><span data-stu-id="58855-126">Sign in with your credentials for that app (or hello credentials for a test account that you set up with access).</span></span> <span data-ttu-id="58855-127">Zodra u zich is aanmeldt, moet u kunnen tooleave Hallo app en keert u terug zonder uw referenties opnieuw invoeren.</span><span class="sxs-lookup"><span data-stu-id="58855-127">Once you sign in successfully, you should be able tooleave hello app and come back without entering your credentials again.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="58855-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="58855-128">Next steps</span></span>

- <span data-ttu-id="58855-129">Meer informatie over andere manieren tooimplement [eenmalige aanmelding met toepassingsproxy](application-proxy-sso-overview.md)</span><span class="sxs-lookup"><span data-stu-id="58855-129">Read about other ways tooimplement [Single sign-on with Application Proxy](application-proxy-sso-overview.md)</span></span>
- <span data-ttu-id="58855-130">Meer informatie over [beveiligingsoverwegingen voor toegang tot apps op afstand met Azure AD-toepassingsproxy](application-proxy-security-considerations.md)</span><span class="sxs-lookup"><span data-stu-id="58855-130">Learn about [Security considerations for accessing apps remotely with Azure AD Application Proxy](application-proxy-security-considerations.md)</span></span>