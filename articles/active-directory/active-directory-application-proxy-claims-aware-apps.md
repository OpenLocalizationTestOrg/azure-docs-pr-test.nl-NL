---
title: aaaClaims-compatibele apps - toepassingsproxy van Azure AD | Microsoft Docs
description: Hoe toopublish een on-premises ASP.NET-toepassingen die AD FS-claims voor veilige externe toegang door uw gebruikers te accepteren.
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
ms.openlocfilehash: 7be633225de700226c7c94815eb91b3de2b61cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a><span data-ttu-id="5b141-103">Werken met claimbewuste toepassingen in de toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="5b141-103">Working with claims-aware apps in Application Proxy</span></span>
<span data-ttu-id="5b141-104">[Claims-compatibele apps](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) een omleiding toohello Security Token Service (STS) uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5b141-104">[Claims-aware apps](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) perform a redirection toohello Security Token Service (STS).</span></span> <span data-ttu-id="5b141-105">Hallo STS vraagt om de referenties van gebruiker Hallo voor een token en stuurt vervolgens door Hallo-Gebruikerstoepassing toohello.</span><span class="sxs-lookup"><span data-stu-id="5b141-105">hello STS requests credentials from hello user in exchange for a token and then redirects hello user toohello application.</span></span> <span data-ttu-id="5b141-106">Er zijn enkele manieren tooenable toepassingsproxy toowork met deze omleidingen.</span><span class="sxs-lookup"><span data-stu-id="5b141-106">There are a few ways tooenable Application Proxy toowork with these redirects.</span></span> <span data-ttu-id="5b141-107">Gebruik dit artikel tooconfigure uw implementatie voor claims-compatibele apps.</span><span class="sxs-lookup"><span data-stu-id="5b141-107">Use this article tooconfigure your deployment for claims-aware apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5b141-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5b141-108">Prerequisites</span></span>
<span data-ttu-id="5b141-109">Zorg ervoor dat Hallo STS die Hallo claimbewuste app leidt toois beschikbaar buiten uw on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="5b141-109">Make sure that hello STS that hello claims-aware app redirects toois available outside of your on-premises network.</span></span> <span data-ttu-id="5b141-110">U kunt Hallo STS beschikbaar maken door het beschikbaar te maken via een proxy of door ze buiten verbindingen.</span><span class="sxs-lookup"><span data-stu-id="5b141-110">You can make hello STS available by exposing it through a proxy or by allowing outside connections.</span></span> 

## <a name="publish-your-application"></a><span data-ttu-id="5b141-111">Uw toepassing publiceren</span><span class="sxs-lookup"><span data-stu-id="5b141-111">Publish your application</span></span>

1. <span data-ttu-id="5b141-112">Publiceer de toepassing op basis van toohello instructies die worden beschreven [publiceren van toepassingen met toepassingsproxy](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5b141-112">Publish your application according toohello instructions described in [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span></span>
2. <span data-ttu-id="5b141-113">Navigeer toohello toepassingspagina in Hallo portal en selecteert u een **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="5b141-113">Navigate toohello application page in hello portal and select **Single sign-on**.</span></span>
3. <span data-ttu-id="5b141-114">Als u hebt gekozen **Azure Active Directory** als uw **pre-authenticatie methode**, selecteer **Azure AD eenmalige aanmelding uitgeschakeld** als uw **intern Verificatiemethode**.</span><span class="sxs-lookup"><span data-stu-id="5b141-114">If you chose **Azure Active Directory** as your **Preauthentication Method**, select **Azure AD single sign-on disabled** as your **Internal Authentication Method**.</span></span> <span data-ttu-id="5b141-115">Als u hebt gekozen **Passthrough** als uw **pre-authenticatie methode**, hoeft u niet toochange alles.</span><span class="sxs-lookup"><span data-stu-id="5b141-115">If you chose **Passthrough** as your **Preauthentication Method**, you don't need toochange anything.</span></span>

## <a name="configure-adfs"></a><span data-ttu-id="5b141-116">AD FS configureren</span><span class="sxs-lookup"><span data-stu-id="5b141-116">Configure ADFS</span></span>

<span data-ttu-id="5b141-117">U kunt AD FS voor claims-compatibele apps op twee manieren configureren.</span><span class="sxs-lookup"><span data-stu-id="5b141-117">You can configure ADFS for claims-aware apps in one of two ways.</span></span> <span data-ttu-id="5b141-118">Hallo wordt eerst met behulp van aangepaste domeinen.</span><span class="sxs-lookup"><span data-stu-id="5b141-118">hello first is by using custom domains.</span></span> <span data-ttu-id="5b141-119">Hallo is het tweede met WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="5b141-119">hello second is with WS-Federation.</span></span> 

### <a name="option-1-custom-domains"></a><span data-ttu-id="5b141-120">Optie 1: Aangepaste domeinen</span><span class="sxs-lookup"><span data-stu-id="5b141-120">Option 1: Custom domains</span></span>

<span data-ttu-id="5b141-121">Als alle Hallo interne URL's voor uw toepassingen volledig gekwalificeerde zijn domeinnamen (FQDN's), dan kunt u configureren [aangepaste domeinen](active-directory-application-proxy-custom-domains.md) voor uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="5b141-121">If all hello internal URLs for your applications are fully qualified domain names (FQDNs), then you can configure [custom domains](active-directory-application-proxy-custom-domains.md) for your applications.</span></span> <span data-ttu-id="5b141-122">Gebruik Hallo aangepaste domeinen toocreate externe URL's die zijn hetzelfde als de interne URL's Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="5b141-122">Use hello custom domains toocreate external URLs that are hello same as hello internal URLs.</span></span> <span data-ttu-id="5b141-123">Als de externe URL's die overeenkomen met uw interne URL's, werken Hallo STS omleidingen of uw gebruikers on-premises of extern zijn.</span><span class="sxs-lookup"><span data-stu-id="5b141-123">When your external URLs match your internal URLs, then hello STS redirections work whether your users are on-premises or remote.</span></span> 

### <a name="option-2-ws-federation"></a><span data-ttu-id="5b141-124">Optie 2: WS-Federation</span><span class="sxs-lookup"><span data-stu-id="5b141-124">Option 2: WS-Federation</span></span>

1. <span data-ttu-id="5b141-125">Open AD FS-beheer.</span><span class="sxs-lookup"><span data-stu-id="5b141-125">Open ADFS Management.</span></span>
2. <span data-ttu-id="5b141-126">Ga te**Relying Party-vertrouwensrelaties**, met de rechtermuisknop op het Hallo-app die u met toepassingsproxy publiceren wilt en kiest u **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="5b141-126">Go too**Relying Party Trusts**, right-click on hello app you are publishing with Application Proxy, and choose **Properties**.</span></span>  

   ![Relying Party-vertrouwensrelaties met de rechtermuisknop op de naam van de app - schermafbeelding](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. <span data-ttu-id="5b141-128">Op Hallo **eindpunten** tabblad onder **eindpunttype**, selecteer **WS-Federation**.</span><span class="sxs-lookup"><span data-stu-id="5b141-128">On hello **Endpoints** tab, under **Endpoint type**, select **WS-Federation**.</span></span>
4. <span data-ttu-id="5b141-129">Onder **vertrouwde URL**, Voer Hallo-URL die u hebt ingevoerd in Hallo toepassingsproxy onder **externe URL** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="5b141-129">Under **Trusted URL**, enter hello URL you entered in hello Application Proxy under **External URL** and click **OK**.</span></span>  

   ![Toevoegen van een eindpunt - waarde vertrouwde URL - schermafbeelding](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a><span data-ttu-id="5b141-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5b141-131">Next steps</span></span>
* <span data-ttu-id="5b141-132">[Schakel eenmalige aanmelding op](application-proxy-sso-overview.md) voor toepassingen die niet claimbewuste</span><span class="sxs-lookup"><span data-stu-id="5b141-132">[Enable single-sign on](application-proxy-sso-overview.md) for applications that aren't claims-aware</span></span>
* [<span data-ttu-id="5b141-133">Native client-apps toointeract met proxy toepassingen inschakelen</span><span class="sxs-lookup"><span data-stu-id="5b141-133">Enable native client apps toointeract with proxy applications</span></span>](active-directory-application-proxy-native-client.md)


