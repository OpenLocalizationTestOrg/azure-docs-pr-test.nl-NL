---
title: Eenmalige aanmelding voor apps met Azure AD-toepassingsproxy | Microsoft Docs
description: "Schakel één aanmelding voor uw gepubliceerde on-premises toepassingen met Azure AD-toepassingsproxy in de Azure portal."
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
ms.openlocfilehash: 9ddc0c1bd5f2cbb24f6761cfd041b820ee6464b8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a><span data-ttu-id="14182-103">Wachtwoord voor eenmalige aanmelding met toepassingsproxy vaulting</span><span class="sxs-lookup"><span data-stu-id="14182-103">Password vaulting for single sign-on with Application Proxy</span></span>

<span data-ttu-id="14182-104">Azure Active Directory-toepassingsproxy helpt u bij de productiviteit door on-premises toepassingen publiceren zodat externe werknemers veilig toegang deze te tot verbeteren.</span><span class="sxs-lookup"><span data-stu-id="14182-104">Azure Active Directory Application Proxy helps you improve productivity by publishing on-premises applications so that remote employees can securely access them, too.</span></span> <span data-ttu-id="14182-105">In de Azure-portal kunt u ook instellen van eenmalige aanmelding (SSO) op deze apps.</span><span class="sxs-lookup"><span data-stu-id="14182-105">In the Azure portal, you can also set up single sign-on (SSO) to these apps.</span></span> <span data-ttu-id="14182-106">Uw gebruikers alleen vereist voor verificatie met Azure AD en toegang te krijgen tot uw zakelijke toepassing zonder opnieuw aanmelden.</span><span class="sxs-lookup"><span data-stu-id="14182-106">Your users only need to authenticate with Azure AD, and they can access your enterprise application without having to sign in again.</span></span>

<span data-ttu-id="14182-107">Toepassingsproxy ondersteunt verschillende [eenmalige aanmelding modi](application-proxy-sso-overview.md).</span><span class="sxs-lookup"><span data-stu-id="14182-107">Application Proxy supports several [single sign-on modes](application-proxy-sso-overview.md).</span></span> <span data-ttu-id="14182-108">Op basis van wachtwoorden eenmalige aanmelding is bedoeld voor toepassingen die gebruikmaken van een combinatie van gebruikersnaam en wachtwoord voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="14182-108">Password-based sign-on is intended for applications that use a username/password combination for authentication.</span></span> <span data-ttu-id="14182-109">Wanneer u op basis van wachtwoorden eenmalige aanmelding voor uw toepassing configureert, wordt uw gebruikers aan te melden bij de on-premises toepassing eenmaal hebben.</span><span class="sxs-lookup"><span data-stu-id="14182-109">When you configure password-based sign-on for your application, your users have to sign in to the on-premises application once.</span></span> <span data-ttu-id="14182-110">Hierna is Azure Active Directory de gegevens worden opgeslagen en automatisch aan de toepassing te biedt wanneer uw gebruikers toegang op afstand.</span><span class="sxs-lookup"><span data-stu-id="14182-110">After that, Azure Active Directory stores the sign-in information and automatically provides it to the application when your users access it remotely.</span></span> 

<span data-ttu-id="14182-111">U moet al hebt gepubliceerd en uw app met toepassingsproxy getest.</span><span class="sxs-lookup"><span data-stu-id="14182-111">You should already have published and tested your app with Application Proxy.</span></span> <span data-ttu-id="14182-112">Als dit niet het geval is, volg de stappen in [toepassingen publiceren met Azure AD-toepassingsproxy](application-proxy-publish-azure-portal.md) vervolgens kun je hier.</span><span class="sxs-lookup"><span data-stu-id="14182-112">If not, follow the steps in [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md) then come back here.</span></span> 

## <a name="set-up-password-vaulting-for-your-application"></a><span data-ttu-id="14182-113">Wachtwoord voor uw toepassing vaulting instellen</span><span class="sxs-lookup"><span data-stu-id="14182-113">Set up password vaulting for your application</span></span>

1. <span data-ttu-id="14182-114">Meld u als beheerder aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="14182-114">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="14182-115">Selecteer **Azure Active Directory** > **bedrijfstoepassingen** > **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="14182-115">Select **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="14182-116">Selecteer de app die u wilt instellen met eenmalige aanmelding in de lijst.</span><span class="sxs-lookup"><span data-stu-id="14182-116">From the list, select the app that you want to set up with SSO.</span></span>  
4. <span data-ttu-id="14182-117">Selecteer **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="14182-117">Select **Single sign-on**.</span></span>

   ![Schakel eenmalige aanmelding](./media/application-proxy-sso-azure-portal/select-sso.png)

5. <span data-ttu-id="14182-119">Kies voor de modus SSO **op basis van wachtwoorden aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="14182-119">For the SSO mode, choose **Password-based Sign-on**.</span></span>
6. <span data-ttu-id="14182-120">Voer de URL voor de URL eenmalige aanmelding voor de pagina waar gebruikers hun gebruikersnaam en wachtwoord aanmelden bij uw app buiten het bedrijfsnetwerk invoeren.</span><span class="sxs-lookup"><span data-stu-id="14182-120">For the Sign-on URL, enter the URL for the page where users enter their username and password to sign in to your app outside of the corporate network.</span></span> <span data-ttu-id="14182-121">Dit kan zijn dat de externe URL die u hebt gemaakt toen u de app via toepassingsproxy hebt gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="14182-121">This may be the External URL that you created when you published the app through Application Proxy.</span></span> 

   ![Kiezen op basis van wachtwoorden eenmalige aanmelding en voer de URL](./media/application-proxy-sso-azure-portal/password-sso.png)

7. <span data-ttu-id="14182-123">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="14182-123">Select **Save**.</span></span>

<!-- Need to repro?
7. The page should tell you that a sign-in form was successfully detected at the provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow the instructions to point out where the sign-in credentials go. 
-->

## <a name="test-your-app"></a><span data-ttu-id="14182-124">Uw app testen</span><span class="sxs-lookup"><span data-stu-id="14182-124">Test your app</span></span>

<span data-ttu-id="14182-125">Ga naar de externe URL die u hebt geconfigureerd voor externe toegang tot uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="14182-125">Go to external URL that you configured for remote access to your application.</span></span> <span data-ttu-id="14182-126">Aanmelden met uw referenties voor die app (of de referenties voor een testaccount dat u toegang hebt ingesteld).</span><span class="sxs-lookup"><span data-stu-id="14182-126">Sign in with your credentials for that app (or the credentials for a test account that you set up with access).</span></span> <span data-ttu-id="14182-127">Zodra u zich is aanmeldt, kunt u moet de app laat en keert u terug zonder uw referenties opnieuw invoeren.</span><span class="sxs-lookup"><span data-stu-id="14182-127">Once you sign in successfully, you should be able to leave the app and come back without entering your credentials again.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="14182-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="14182-128">Next steps</span></span>

- <span data-ttu-id="14182-129">Meer informatie over andere manieren om te implementeren [eenmalige aanmelding met toepassingsproxy](application-proxy-sso-overview.md)</span><span class="sxs-lookup"><span data-stu-id="14182-129">Read about other ways to implement [Single sign-on with Application Proxy](application-proxy-sso-overview.md)</span></span>
- <span data-ttu-id="14182-130">Meer informatie over [beveiligingsoverwegingen voor toegang tot apps op afstand met Azure AD-toepassingsproxy](application-proxy-security-considerations.md)</span><span class="sxs-lookup"><span data-stu-id="14182-130">Learn about [Security considerations for accessing apps remotely with Azure AD Application Proxy](application-proxy-security-considerations.md)</span></span>