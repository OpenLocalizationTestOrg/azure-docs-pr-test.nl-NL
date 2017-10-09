---
title: aaaPublish apps met Azure AD-toepassingsproxy | Microsoft Docs
description: Lokale toepassingen toohello cloud met Azure AD-toepassingsproxy in hello Azure-portal publiceren.
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
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ed5458467fb7d4376f65a222f1ba5f23cfdfc57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="61694-103">Toepassingen publiceren met Azure AD-toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="61694-103">Publish applications using Azure AD Application Proxy</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="61694-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="61694-104">Azure portal</span></span>](application-proxy-publish-azure-portal.md)
> * [<span data-ttu-id="61694-105">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="61694-105">Azure classic portal</span></span>](active-directory-application-proxy-publish.md)

<span data-ttu-id="61694-106">Toepassingsproxy van Azure Active Directory (AD) kunt u ondersteuning voor externe werknemers door het publiceren van lokale toepassingen toobe toegankelijk is via Hallo internet.</span><span class="sxs-lookup"><span data-stu-id="61694-106">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications toobe accessed over hello internet.</span></span> <span data-ttu-id="61694-107">U kunt deze u toepassingen publiceert via hello Azure portal tooprovide veilige externe toegang van buiten uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="61694-107">You can publish these applications through hello Azure portal tooprovide secure remote access from outside your network.</span></span>

<span data-ttu-id="61694-108">Dit artikel begeleidt u bij Hallo stappen toopublish een lokale app met toepassingsproxy.</span><span class="sxs-lookup"><span data-stu-id="61694-108">This article walks you through hello steps toopublish an on-premises app with Application Proxy.</span></span> <span data-ttu-id="61694-109">Nadat u dit artikel hebt voltooid, uw gebruikers zullen worden tooaccess kunnen uw app op afstand.</span><span class="sxs-lookup"><span data-stu-id="61694-109">After you complete this article, your users will be able tooaccess your app remotely.</span></span> <span data-ttu-id="61694-110">En u bent klaar tooconfigure extra functies voor de toepassing hello zoals eenmalige aanmelding, persoonlijke gegevens en beveiligingsvereisten.</span><span class="sxs-lookup"><span data-stu-id="61694-110">And you'll be ready tooconfigure extra features for hello application like single sign-on, personalized information, and security requirements.</span></span>

<span data-ttu-id="61694-111">Als u nieuwe tooApplication Proxy, meer informatie over deze functie met Hallo artikel [hoe tooprovide veilige externe toegang tot het tooon-premises toepassingen](active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="61694-111">If you're new tooApplication Proxy, learn more about this feature with hello article [How tooprovide secure remote access tooon-premises applications](active-directory-application-proxy-get-started.md).</span></span>


## <a name="publish-an-on-premises-app-for-remote-access"></a><span data-ttu-id="61694-112">Publiceren van een lokale app voor externe toegang</span><span class="sxs-lookup"><span data-stu-id="61694-112">Publish an on-premises app for remote access</span></span>

<span data-ttu-id="61694-113">Volg deze stappen toopublish uw apps met Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="61694-113">Follow these steps toopublish your apps with Application Proxy.</span></span> <span data-ttu-id="61694-114">Als u dit nog niet hebt al gedownload en een connector voor uw organisatie hebt geconfigureerd, gaat u verder te[aan de slag met Application Proxy en het Hallo-connector installeert](active-directory-application-proxy-enable.md) eerste, en vervolgens uw app te publiceren.</span><span class="sxs-lookup"><span data-stu-id="61694-114">If you haven't already downloaded and configured a connector for your organization, go too[Get started with Application Proxy and install hello connector](active-directory-application-proxy-enable.md) first, and then publish your app.</span></span>

> [!TIP]
> <span data-ttu-id="61694-115">Als u uit toepassingsproxy voor Hallo eerst test, kiest u een toepassing die ingesteld voor verificatie op basis van wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="61694-115">If you're testing out Application Proxy for hello first time, choose an application that's set up for password-based authentication.</span></span> <span data-ttu-id="61694-116">Toepassingsproxy biedt ondersteuning voor andere soorten authenticatie, maar apps op basis van wachtwoorden Hallo eenvoudigste tooget up snel gebruiksklaar zijn.</span><span class="sxs-lookup"><span data-stu-id="61694-116">Application Proxy supports other types of authentication, but password-based apps are hello easiest tooget up and running quickly.</span></span> 

1. <span data-ttu-id="61694-117">Meld u aan als een beheerder in Hallo [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="61694-117">Sign in as an administrator in hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="61694-118">Selecteer **Azure Active Directory** > **bedrijfstoepassingen** > **nieuwe toepassing**.</span><span class="sxs-lookup"><span data-stu-id="61694-118">Select **Azure Active Directory** > **Enterprise applications** > **New application**.</span></span>

  ![Een zakelijke toepassing toevoegen](./media/application-proxy-publish-azure-portal/add-app.png)

3. <span data-ttu-id="61694-120">Selecteer **alle**, selecteer daarna **On-premises toepassing**.</span><span class="sxs-lookup"><span data-stu-id="61694-120">Select **All**, then select **On-premises application**.</span></span>  

  ![Uw eigen toepassing toevoegen](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. <span data-ttu-id="61694-122">Bieden de volgende informatie over uw toepassing hello:</span><span class="sxs-lookup"><span data-stu-id="61694-122">Provide hello following information about your application:</span></span>

   - <span data-ttu-id="61694-123">**Naam**: Hallo-naam van Hallo-toepassing die wordt weergegeven op het toegangsvenster hello en in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="61694-123">**Name**: hello name of hello application that will appear on hello access panel and in hello Azure portal.</span></span> 

   - <span data-ttu-id="61694-124">**Interne URL**: Hallo URL die u de toepassing hello tooaccess van binnen uw particuliere netwerk gebruikt.</span><span class="sxs-lookup"><span data-stu-id="61694-124">**Internal URL**: hello URL that you use tooaccess hello application from inside your private network.</span></span> <span data-ttu-id="61694-125">U kunt een specifiek pad opgeven op Hallo back-end server toopublish terwijl Hallo overige Hallo-server niet gepubliceerd is.</span><span class="sxs-lookup"><span data-stu-id="61694-125">You can provide a specific path on hello backend server toopublish, while hello rest of hello server is unpublished.</span></span> <span data-ttu-id="61694-126">Op deze manier kunt u verschillende sites publiceren op dezelfde server als verschillende apps Hallo en elk een eigen naam en toegangsregels geven.</span><span class="sxs-lookup"><span data-stu-id="61694-126">In this way, you can publish different sites on hello same server as different apps, and give each one its own name and access rules.</span></span>

     > [!TIP]
     > <span data-ttu-id="61694-127">Als u een pad publiceert, ervoor zorgen dat deze alle benodigde Hallo-installatiekopieën, scripts en StyleSheets voor uw toepassing bevat.</span><span class="sxs-lookup"><span data-stu-id="61694-127">If you publish a path, make sure that it includes all hello necessary images, scripts, and style sheets for your application.</span></span> <span data-ttu-id="61694-128">Bijvoorbeeld, als uw app op https://yourapp/app is en zich bevindt op https://yourapp/media installatiekopieën gebruikt, moet vervolgens u publiceren https://yourapp/ als Hallo-pad.</span><span class="sxs-lookup"><span data-stu-id="61694-128">For example, if your app is at https://yourapp/app and uses images located at https://yourapp/media, then you should publish https://yourapp/ as hello path.</span></span> <span data-ttu-id="61694-129">Deze interne URL geen toobe Hallo-startpagina die uw gebruikers te zien.</span><span class="sxs-lookup"><span data-stu-id="61694-129">This internal URL doesn't have toobe hello landing page your users see.</span></span> <span data-ttu-id="61694-130">Zie voor meer informatie [instellen van een aangepaste startpagina van gepubliceerde apps](application-proxy-office365-app-launcher.md).</span><span class="sxs-lookup"><span data-stu-id="61694-130">For more information, see [Set a custom home page for published apps](application-proxy-office365-app-launcher.md).</span></span>

   - <span data-ttu-id="61694-131">**Externe URL**: Hallo adres uw gebruikers gaan tooin volgorde tooaccess Hallo-app van buiten uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="61694-131">**External URL**: hello address your users will go tooin order tooaccess hello app from outside your network.</span></span> <span data-ttu-id="61694-132">Als u niet dat toouse Hallo standaarddomein toepassingsproxy wilt, leest u over [aangepaste domeinen in Azure AD-toepassingsproxy](active-directory-application-proxy-custom-domains.md).</span><span class="sxs-lookup"><span data-stu-id="61694-132">If you don't want toouse hello default Application Proxy domain, read about [custom domains in Azure AD Application Proxy](active-directory-application-proxy-custom-domains.md).</span></span>
   - <span data-ttu-id="61694-133">**Verificatie vooraf**: hoe Application Proxy gebruikers worden geverifieerd voordat ze deze toegang tooyour application te geven.</span><span class="sxs-lookup"><span data-stu-id="61694-133">**Pre Authentication**: How Application Proxy verifies users before giving them access tooyour application.</span></span> 

     - <span data-ttu-id="61694-134">Azure Active Directory: Gebruikers toosign met Azure AD dat hun machtigingen geverifieerd voor Hallo directory en de toepassing wordt doorgestuurd door Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="61694-134">Azure Active Directory: Application Proxy redirects users toosign in with Azure AD, which authenticates their permissions for hello directory and application.</span></span> <span data-ttu-id="61694-135">We raden deze optie als de standaard hello, zodat u van Azure AD-beveiligingsfuncties zoals voorwaardelijke toegang en multi-factor Authentication profiteren kunt.</span><span class="sxs-lookup"><span data-stu-id="61694-135">We recommend keeping this option as hello default, so that you can take advantage of Azure AD security features like conditional access and Multi-Factor Authentication.</span></span>
     - <span data-ttu-id="61694-136">Passthrough: Gebruikers hebben geen tooauthenticate voor Azure Active Directory tooaccess Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="61694-136">Passthrough: Users don't have tooauthenticate against Azure Active Directory tooaccess hello application.</span></span> <span data-ttu-id="61694-137">U kunt nog steeds verificatievereisten op Hallo back-end instellen.</span><span class="sxs-lookup"><span data-stu-id="61694-137">You can still set up authentication requirements on hello backend.</span></span>
   - <span data-ttu-id="61694-138">**Connector-groep**: Connectors proces Hallo RAS tooyour toepassings- en connector groepen te ordenen connectors en apps per regio, netwerk of doel.</span><span class="sxs-lookup"><span data-stu-id="61694-138">**Connector Group**: Connectors process hello remote access tooyour application, and connector groups help you organize connectors and apps by region, network, or purpose.</span></span> <span data-ttu-id="61694-139">Als u een connector groepen die zijn gemaakt nog niet hebt, uw app te toegewezen**standaard**.</span><span class="sxs-lookup"><span data-stu-id="61694-139">If you don't have any connector groups created yet, your app is assigned too**Default**.</span></span>

   ![Uw toepassing configureren](./media/application-proxy-publish-azure-portal/configure-app.png)
5. <span data-ttu-id="61694-141">Indien nodig, extra instellingen configureren.</span><span class="sxs-lookup"><span data-stu-id="61694-141">If necessary, configure additional settings.</span></span> <span data-ttu-id="61694-142">Voor de meeste toepassingen, moet u deze instellingen behouden de standaardwaarden hebben.</span><span class="sxs-lookup"><span data-stu-id="61694-142">For most applications, you should keep these settings in their default states.</span></span> 
   - <span data-ttu-id="61694-143">**Back-end toepassing time-out**: Stel deze waarde te**lang** alleen als uw toepassing is tooauthenticate vertragen en verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="61694-143">**Backend Application Timeout**: Set this value too**Long** only if your application is slow tooauthenticate and connect.</span></span> 
   - <span data-ttu-id="61694-144">**URL's in de Headers vertalen**: deze waarde als behouden **Ja** tenzij uw toepassing hello oorspronkelijke host-header in de verificatieaanvraag Hallo vereist.</span><span class="sxs-lookup"><span data-stu-id="61694-144">**Translate URLs in Headers**: Keep this value as **Yes** unless your application required hello original host header in hello authentication request.</span></span>
   - <span data-ttu-id="61694-145">**URL's in de hoofdtekst van de toepassing te vertalen**: deze waarde als behouden **Nee** tenzij u hardcoded HTML koppelingen tooother on-premises toepassingen hebben en geen aangepaste domeinen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="61694-145">**Translate URLs in Application Body**: Keep this value as **No** unless you have hardcoded HTML links tooother on-premises applications, and don't use custom domains.</span></span> <span data-ttu-id="61694-146">Zie voor meer informatie [koppelen vertaling met toepassingsproxy](application-proxy-link-translation.md).</span><span class="sxs-lookup"><span data-stu-id="61694-146">For more information, see [Link translation with Application Proxy](application-proxy-link-translation.md).</span></span>
   
   ![Uw toepassing configureren](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. <span data-ttu-id="61694-148">Selecteer **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="61694-148">Select **Add**.</span></span>


## <a name="add-a-test-user"></a><span data-ttu-id="61694-149">Een testgebruiker toevoegen</span><span class="sxs-lookup"><span data-stu-id="61694-149">Add a test user</span></span> 

<span data-ttu-id="61694-150">tootest dat uw app correct is gepubliceerd een test-gebruikersaccount toevoegen.</span><span class="sxs-lookup"><span data-stu-id="61694-150">tootest that your app was published correctly, add a test user account.</span></span> <span data-ttu-id="61694-151">Controleer of dit account heeft al machtigingen tooaccess Hallo-app uit binnen het bedrijfsnetwerk Hallo.</span><span class="sxs-lookup"><span data-stu-id="61694-151">Verify that this account already has permissions tooaccess hello app from inside hello corporate network.</span></span>

1. <span data-ttu-id="61694-152">Selecteer terug op de blade snel starten Hallo **een gebruiker toewijzen voor het testen van**.</span><span class="sxs-lookup"><span data-stu-id="61694-152">Back on hello Quick start blade, select **Assign a user for testing**.</span></span>

  ![Een gebruiker toewijzen voor het testen](./media/application-proxy-publish-azure-portal/assign-user.png)

2. <span data-ttu-id="61694-154">Selecteer op het Hallo-gebruikers en groepen blade, **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="61694-154">On hello Users and groups blade, select **Add**.</span></span>

  ![Een gebruiker of groep toevoegen](./media/application-proxy-publish-azure-portal/add-user.png)

3. <span data-ttu-id="61694-156">Selecteer op het tabblad van het Hallo toevoegen toewijzing **gebruikers en groepen** kies vervolgens de gewenste tooadd Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="61694-156">On hello Add assignment blade, select **Users and groups** then choose hello account you want tooadd.</span></span> 
4. <span data-ttu-id="61694-157">Selecteer **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="61694-157">Select **Assign**.</span></span>

## <a name="test-your-published-app"></a><span data-ttu-id="61694-158">Uw gepubliceerde app testen</span><span class="sxs-lookup"><span data-stu-id="61694-158">Test your published app</span></span>

<span data-ttu-id="61694-159">Navigeer in uw browser toohello externe URL die u hebt geconfigureerd tijdens het Hallo stap publiceren.</span><span class="sxs-lookup"><span data-stu-id="61694-159">In your browser, navigate toohello external URL that you configured during hello publish step.</span></span> <span data-ttu-id="61694-160">U ziet het startscherm Hallo en kunnen toosign worden met Hallo testaccount instellen van.</span><span class="sxs-lookup"><span data-stu-id="61694-160">You should see hello start screen, and be able toosign in with hello test account you set up.</span></span>

![Uw gepubliceerde app testen](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a><span data-ttu-id="61694-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="61694-162">Next steps</span></span>
- <span data-ttu-id="61694-163">[Downloaden van connectors](active-directory-application-proxy-enable.md) en [connector groepen maken](active-directory-application-proxy-connectors-azure-portal.md) toopublish toepassingen op afzonderlijke netwerken en locaties.</span><span class="sxs-lookup"><span data-stu-id="61694-163">[Download connectors](active-directory-application-proxy-enable.md) and [create connector groups](active-directory-application-proxy-connectors-azure-portal.md) toopublish applications on separate networks and locations.</span></span>

- <span data-ttu-id="61694-164">[Instellen van eenmalige aanmelding](application-proxy-sso-azure-portal.md) voor uw zojuist gepubliceerde app</span><span class="sxs-lookup"><span data-stu-id="61694-164">[Set up single sign-on](application-proxy-sso-azure-portal.md) for your newly published app</span></span>
