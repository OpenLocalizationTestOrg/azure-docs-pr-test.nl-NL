---
title: Claims-compatibele apps - Azure AD-toepassingsproxy | Microsoft Docs
description: Het publiceren van on-premises ASP.NET-toepassingen die AD FS-claims voor veilige externe toegang door uw gebruikers te accepteren.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 91e6211b-fe6a-42c6-bdb3-1fff0312db15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 5784222608b01509fc4ff84b1a8792cbcfea89e6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a><span data-ttu-id="4d71c-103">Werken met claimbewuste toepassingen in de toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="4d71c-103">Working with claims-aware apps in Application Proxy</span></span>
<span data-ttu-id="4d71c-104">[Claims-compatibele apps](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) een omleiding naar de Security Token Service (STS) uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="4d71c-104">[Claims-aware apps](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) perform a redirection to the Security Token Service (STS).</span></span> <span data-ttu-id="4d71c-105">De STS vraagt om de referenties van de gebruiker voor een token en stuurt vervolgens door de gebruiker naar de toepassing.</span><span class="sxs-lookup"><span data-stu-id="4d71c-105">The STS requests credentials from the user in exchange for a token and then redirects the user to the application.</span></span> <span data-ttu-id="4d71c-106">Er zijn een aantal manieren Application Proxy voor gebruik met deze omleidingen in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="4d71c-106">There are a few ways to enable Application Proxy to work with these redirects.</span></span> <span data-ttu-id="4d71c-107">Gebruik dit artikel voor het configureren van uw implementatie van claims-compatibele apps.</span><span class="sxs-lookup"><span data-stu-id="4d71c-107">Use this article to configure your deployment for claims-aware apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4d71c-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4d71c-108">Prerequisites</span></span>
<span data-ttu-id="4d71c-109">Zorg ervoor dat de STS die de claimbewuste app wordt omgeleid naar uw on-premises netwerk beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="4d71c-109">Make sure that the STS that the claims-aware app redirects to is available outside of your on-premises network.</span></span> <span data-ttu-id="4d71c-110">U kunt de STS beschikbaar maken door het beschikbaar te maken via een proxy of door externe verbindingen toestaan.</span><span class="sxs-lookup"><span data-stu-id="4d71c-110">You can make the STS available by exposing it through a proxy or by allowing outside connections.</span></span> 

## <a name="publish-your-application"></a><span data-ttu-id="4d71c-111">Uw toepassing publiceren</span><span class="sxs-lookup"><span data-stu-id="4d71c-111">Publish your application</span></span>

1. <span data-ttu-id="4d71c-112">Uw toepassing volgens de instructies die worden beschreven publiceren [publiceren van toepassingen met toepassingsproxy](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4d71c-112">Publish your application according to the instructions described in [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span></span>
2. <span data-ttu-id="4d71c-113">Navigeer naar de toepassingspagina in de portal en selecteer **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="4d71c-113">Navigate to the application page in the portal and select **Single sign-on**.</span></span>
3. <span data-ttu-id="4d71c-114">Als u hebt gekozen **Azure Active Directory** als uw **pre-authenticatie methode**, selecteer **Azure AD eenmalige aanmelding uitgeschakeld** als uw **intern Verificatiemethode**.</span><span class="sxs-lookup"><span data-stu-id="4d71c-114">If you chose **Azure Active Directory** as your **Preauthentication Method**, select **Azure AD single sign-on disabled** as your **Internal Authentication Method**.</span></span> <span data-ttu-id="4d71c-115">Als u hebt gekozen **Passthrough** als uw **pre-authenticatie methode**, u hoeft niet te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4d71c-115">If you chose **Passthrough** as your **Preauthentication Method**, you don't need to change anything.</span></span>

## <a name="configure-adfs"></a><span data-ttu-id="4d71c-116">AD FS configureren</span><span class="sxs-lookup"><span data-stu-id="4d71c-116">Configure ADFS</span></span>

<span data-ttu-id="4d71c-117">U kunt AD FS voor claims-compatibele apps op twee manieren configureren.</span><span class="sxs-lookup"><span data-stu-id="4d71c-117">You can configure ADFS for claims-aware apps in one of two ways.</span></span> <span data-ttu-id="4d71c-118">De eerste is met behulp van aangepaste domeinen.</span><span class="sxs-lookup"><span data-stu-id="4d71c-118">The first is by using custom domains.</span></span> <span data-ttu-id="4d71c-119">De tweede is met WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="4d71c-119">The second is with WS-Federation.</span></span> 

### <a name="option-1-custom-domains"></a><span data-ttu-id="4d71c-120">Optie 1: Aangepaste domeinen</span><span class="sxs-lookup"><span data-stu-id="4d71c-120">Option 1: Custom domains</span></span>

<span data-ttu-id="4d71c-121">Als alle de interne URL's voor uw toepassingen volledig zijn gekwalificeerde domeinnamen (FQDN's), dan kunt u configureren [aangepaste domeinen](active-directory-application-proxy-custom-domains.md) voor uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="4d71c-121">If all the internal URLs for your applications are fully qualified domain names (FQDNs), then you can configure [custom domains](active-directory-application-proxy-custom-domains.md) for your applications.</span></span> <span data-ttu-id="4d71c-122">Gebruik de aangepaste domeinen te maken van de externe URL's die hetzelfde als de interne URL's zijn.</span><span class="sxs-lookup"><span data-stu-id="4d71c-122">Use the custom domains to create external URLs that are the same as the internal URLs.</span></span> <span data-ttu-id="4d71c-123">Als de externe URL's die overeenkomen met uw interne URL's, werken de STS-omleidingen of uw gebruikers on-premises of extern zijn.</span><span class="sxs-lookup"><span data-stu-id="4d71c-123">When your external URLs match your internal URLs, then the STS redirections work whether your users are on-premises or remote.</span></span> 

### <a name="option-2-ws-federation"></a><span data-ttu-id="4d71c-124">Optie 2: WS-Federation</span><span class="sxs-lookup"><span data-stu-id="4d71c-124">Option 2: WS-Federation</span></span>

1. <span data-ttu-id="4d71c-125">Open AD FS-beheer.</span><span class="sxs-lookup"><span data-stu-id="4d71c-125">Open ADFS Management.</span></span>
2. <span data-ttu-id="4d71c-126">Ga naar **Relying Party-vertrouwensrelaties**, met de rechtermuisknop op de app die u met toepassingsproxy publiceren wilt en kiest u **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="4d71c-126">Go to **Relying Party Trusts**, right-click on the app you are publishing with Application Proxy, and choose **Properties**.</span></span>  

   ![Relying Party-vertrouwensrelaties met de rechtermuisknop op de naam van de app - schermafbeelding](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. <span data-ttu-id="4d71c-128">Op de **eindpunten** tabblad onder **eindpunttype**, selecteer **WS-Federation**.</span><span class="sxs-lookup"><span data-stu-id="4d71c-128">On the **Endpoints** tab, under **Endpoint type**, select **WS-Federation**.</span></span>
4. <span data-ttu-id="4d71c-129">Onder **vertrouwde URL**, voert u de URL die u hebt ingevoerd in de toepassingsproxy onder **externe URL** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4d71c-129">Under **Trusted URL**, enter the URL you entered in the Application Proxy under **External URL** and click **OK**.</span></span>  

   ![Toevoegen van een eindpunt - waarde vertrouwde URL - schermafbeelding](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a><span data-ttu-id="4d71c-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4d71c-131">Next steps</span></span>
* <span data-ttu-id="4d71c-132">[Schakel eenmalige aanmelding op](application-proxy-sso-overview.md) voor toepassingen die niet claimbewuste</span><span class="sxs-lookup"><span data-stu-id="4d71c-132">[Enable single-sign on](application-proxy-sso-overview.md) for applications that aren't claims-aware</span></span>
* [<span data-ttu-id="4d71c-133">Native ClientApps om te communiceren met de proxy-toepassingen inschakelen</span><span class="sxs-lookup"><span data-stu-id="4d71c-133">Enable native client apps to interact with proxy applications</span></span>](active-directory-application-proxy-native-client.md)


