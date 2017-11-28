---
title: Apps publiceren met een Azure AD-toepassingsproxy | Microsoft Docs
description: Publiceer on-premises toepassingen naar de cloud met Azure AD-toepassingsproxy in de Azure portal.
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
ms.openlocfilehash: e00a939f2b20ab8e0a2ddf0ff91e59db440213ac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="07a48-103">Toepassingen publiceren met Azure AD-toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="07a48-103">Publish applications using Azure AD Application Proxy</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="07a48-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="07a48-104">Azure portal</span></span>](application-proxy-publish-azure-portal.md)
> * [<span data-ttu-id="07a48-105">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="07a48-105">Azure classic portal</span></span>](active-directory-application-proxy-publish.md)

<span data-ttu-id="07a48-106">Toepassingsproxy van Azure Active Directory (AD) kunt u ondersteuning voor externe werknemers door het publiceren van on-premises toepassingen via internet worden geopend.</span><span class="sxs-lookup"><span data-stu-id="07a48-106">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications to be accessed over the internet.</span></span> <span data-ttu-id="07a48-107">U kunt deze toepassingen via de Azure-portal voor beveiligde externe toegang van buiten uw netwerk publiceren.</span><span class="sxs-lookup"><span data-stu-id="07a48-107">You can publish these applications through the Azure portal to provide secure remote access from outside your network.</span></span>

<span data-ttu-id="07a48-108">Dit artikel begeleidt u bij de stappen voor het publiceren van een lokale app met toepassingsproxy.</span><span class="sxs-lookup"><span data-stu-id="07a48-108">This article walks you through the steps to publish an on-premises app with Application Proxy.</span></span> <span data-ttu-id="07a48-109">Nadat u dit artikel hebt voltooid, ziet u uw gebruikers die toegang tot uw app op afstand mogelijk.</span><span class="sxs-lookup"><span data-stu-id="07a48-109">After you complete this article, your users will be able to access your app remotely.</span></span> <span data-ttu-id="07a48-110">En u bent klaar om extra functies voor de toepassing zoals het eenmalige aanmelding, persoonlijke informatie en vereisten voor beveiliging te configureren.</span><span class="sxs-lookup"><span data-stu-id="07a48-110">And you'll be ready to configure extra features for the application like single sign-on, personalized information, and security requirements.</span></span>

<span data-ttu-id="07a48-111">Als u geen ervaring met toepassingsproxy, meer informatie over deze functie in het artikel [het verstrekken van veilige externe toegang tot on-premises toepassingen](active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="07a48-111">If you're new to Application Proxy, learn more about this feature with the article [How to provide secure remote access to on-premises applications](active-directory-application-proxy-get-started.md).</span></span>


## <a name="publish-an-on-premises-app-for-remote-access"></a><span data-ttu-id="07a48-112">Publiceren van een lokale app voor externe toegang</span><span class="sxs-lookup"><span data-stu-id="07a48-112">Publish an on-premises app for remote access</span></span>

<span data-ttu-id="07a48-113">Volg deze stappen voor het publiceren van uw apps met Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="07a48-113">Follow these steps to publish your apps with Application Proxy.</span></span> <span data-ttu-id="07a48-114">Als u dit nog niet hebt al gedownload en een connector voor uw organisatie hebt geconfigureerd, gaat u naar [aan de slag met Application Proxy en installeer de connector](active-directory-application-proxy-enable.md) eerste, en vervolgens uw app te publiceren.</span><span class="sxs-lookup"><span data-stu-id="07a48-114">If you haven't already downloaded and configured a connector for your organization, go to [Get started with Application Proxy and install the connector](active-directory-application-proxy-enable.md) first, and then publish your app.</span></span>

> [!TIP]
> <span data-ttu-id="07a48-115">Als u voor de eerste keer uit toepassingsproxy test, kiest u een toepassing die ingesteld voor verificatie op basis van wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="07a48-115">If you're testing out Application Proxy for the first time, choose an application that's set up for password-based authentication.</span></span> <span data-ttu-id="07a48-116">Toepassingsproxy biedt ondersteuning voor andere soorten authenticatie, maar apps op basis van wachtwoorden zijn het eenvoudigst te laten snel gebruiksklaar.</span><span class="sxs-lookup"><span data-stu-id="07a48-116">Application Proxy supports other types of authentication, but password-based apps are the easiest to get up and running quickly.</span></span> 

1. <span data-ttu-id="07a48-117">Meld u aan als een beheerder in de [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="07a48-117">Sign in as an administrator in the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="07a48-118">Selecteer **Azure Active Directory** > **bedrijfstoepassingen** > **nieuwe toepassing**.</span><span class="sxs-lookup"><span data-stu-id="07a48-118">Select **Azure Active Directory** > **Enterprise applications** > **New application**.</span></span>

  ![Een zakelijke toepassing toevoegen](./media/application-proxy-publish-azure-portal/add-app.png)

3. <span data-ttu-id="07a48-120">Selecteer **alle**, selecteer daarna **On-premises toepassing**.</span><span class="sxs-lookup"><span data-stu-id="07a48-120">Select **All**, then select **On-premises application**.</span></span>  

  ![Uw eigen toepassing toevoegen](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. <span data-ttu-id="07a48-122">Geef de volgende informatie over de toepassing op:</span><span class="sxs-lookup"><span data-stu-id="07a48-122">Provide the following information about your application:</span></span>

   - <span data-ttu-id="07a48-123">**Naam**: de naam van de toepassing die wordt weergegeven in het deelvenster toegang en in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="07a48-123">**Name**: The name of the application that will appear on the access panel and in the Azure portal.</span></span> 

   - <span data-ttu-id="07a48-124">**Interne URL**: de URL die u gebruikt voor toegang tot de toepassing uit binnen uw particuliere netwerk.</span><span class="sxs-lookup"><span data-stu-id="07a48-124">**Internal URL**: The URL that you use to access the application from inside your private network.</span></span> <span data-ttu-id="07a48-125">U kunt voor het publiceren een specifiek pad opgeven op de back-endserver, terwijl de rest van de server ongepubliceerd blijft.</span><span class="sxs-lookup"><span data-stu-id="07a48-125">You can provide a specific path on the backend server to publish, while the rest of the server is unpublished.</span></span> <span data-ttu-id="07a48-126">U kunt op deze manier kunnen verschillende sites op dezelfde server als verschillende apps publiceren en elk een eigen naam en toegangsregels geven.</span><span class="sxs-lookup"><span data-stu-id="07a48-126">In this way, you can publish different sites on the same server as different apps, and give each one its own name and access rules.</span></span>

     > [!TIP]
     > <span data-ttu-id="07a48-127">Als u een pad publiceert, moet u ervoor zorgen dat dit alle benodigde installatiekopieën, scripts en opmaakmodellen voor uw toepassing bevat.</span><span class="sxs-lookup"><span data-stu-id="07a48-127">If you publish a path, make sure that it includes all the necessary images, scripts, and style sheets for your application.</span></span> <span data-ttu-id="07a48-128">Als uw app zich bijvoorbeeld bevindt op het pad https://uwapp/app en gebruikmaakt van installatiekopieën op https://uwapp/media, moet u https://uwapp/ publiceren als het pad.</span><span class="sxs-lookup"><span data-stu-id="07a48-128">For example, if your app is at https://yourapp/app and uses images located at https://yourapp/media, then you should publish https://yourapp/ as the path.</span></span> <span data-ttu-id="07a48-129">Deze interne URL hoeft niet te worden van de startpagina van die uw gebruikers te zien.</span><span class="sxs-lookup"><span data-stu-id="07a48-129">This internal URL doesn't have to be the landing page your users see.</span></span> <span data-ttu-id="07a48-130">Zie voor meer informatie [instellen van een aangepaste startpagina van gepubliceerde apps](application-proxy-office365-app-launcher.md).</span><span class="sxs-lookup"><span data-stu-id="07a48-130">For more information, see [Set a custom home page for published apps](application-proxy-office365-app-launcher.md).</span></span>

   - <span data-ttu-id="07a48-131">**Externe URL**: het adres uw gebruikers gaat naar om toegang tot de app van buiten uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="07a48-131">**External URL**: The address your users will go to in order to access the app from outside your network.</span></span> <span data-ttu-id="07a48-132">Als u niet wilt gebruiken van het standaarddomein toepassingsproxy, leest u over [aangepaste domeinen in Azure AD-toepassingsproxy](active-directory-application-proxy-custom-domains.md).</span><span class="sxs-lookup"><span data-stu-id="07a48-132">If you don't want to use the default Application Proxy domain, read about [custom domains in Azure AD Application Proxy](active-directory-application-proxy-custom-domains.md).</span></span>
   - <span data-ttu-id="07a48-133">**Verificatie vooraf**: hoe Application Proxy gebruikers worden geverifieerd voordat ze toegang geven tot uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="07a48-133">**Pre Authentication**: How Application Proxy verifies users before giving them access to your application.</span></span> 

     - <span data-ttu-id="07a48-134">Azure Active Directory: de gebruikers worden omgeleid met de toepassingsproxy zodat zij zich kunnen aanmelden met Azure AD. Hierbij worden hun machtigingen geverifieerd voor de directory en de toepassing.</span><span class="sxs-lookup"><span data-stu-id="07a48-134">Azure Active Directory: Application Proxy redirects users to sign in with Azure AD, which authenticates their permissions for the directory and application.</span></span> <span data-ttu-id="07a48-135">We raden deze optie als de standaardconfiguratie, zodat u van Azure AD-beveiligingsfuncties zoals voorwaardelijke toegang en multi-factor Authentication profiteren kunt.</span><span class="sxs-lookup"><span data-stu-id="07a48-135">We recommend keeping this option as the default, so that you can take advantage of Azure AD security features like conditional access and Multi-Factor Authentication.</span></span>
     - <span data-ttu-id="07a48-136">Passthrough: Gebruikers hebben geen worden geverifieerd bij Azure Active Directory om toegang tot de toepassing.</span><span class="sxs-lookup"><span data-stu-id="07a48-136">Passthrough: Users don't have to authenticate against Azure Active Directory to access the application.</span></span> <span data-ttu-id="07a48-137">U kunt nog steeds verificatievereisten op de back-end instellen.</span><span class="sxs-lookup"><span data-stu-id="07a48-137">You can still set up authentication requirements on the backend.</span></span>
   - <span data-ttu-id="07a48-138">**Connector-groep**: Connectors verwerken van de externe toegang tot uw toepassing en connector groepeert u indelen connectors en apps per regio, netwerk of doel help.</span><span class="sxs-lookup"><span data-stu-id="07a48-138">**Connector Group**: Connectors process the remote access to your application, and connector groups help you organize connectors and apps by region, network, or purpose.</span></span> <span data-ttu-id="07a48-139">Als u een connector groepen die zijn gemaakt nog niet hebt, uw app is toegewezen aan **standaard**.</span><span class="sxs-lookup"><span data-stu-id="07a48-139">If you don't have any connector groups created yet, your app is assigned to **Default**.</span></span>

   ![Uw toepassing configureren](./media/application-proxy-publish-azure-portal/configure-app.png)
5. <span data-ttu-id="07a48-141">Indien nodig, extra instellingen configureren.</span><span class="sxs-lookup"><span data-stu-id="07a48-141">If necessary, configure additional settings.</span></span> <span data-ttu-id="07a48-142">Voor de meeste toepassingen, moet u deze instellingen behouden de standaardwaarden hebben.</span><span class="sxs-lookup"><span data-stu-id="07a48-142">For most applications, you should keep these settings in their default states.</span></span> 
   - <span data-ttu-id="07a48-143">**Back-end toepassing time-out**: deze waarde instelt op **lang** alleen als uw toepassing traag is om te verifiëren en verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="07a48-143">**Backend Application Timeout**: Set this value to **Long** only if your application is slow to authenticate and connect.</span></span> 
   - <span data-ttu-id="07a48-144">**URL's in de Headers vertalen**: deze waarde als behouden **Ja** tenzij uw toepassing de oorspronkelijke host-header in de verificatieaanvraag vereist.</span><span class="sxs-lookup"><span data-stu-id="07a48-144">**Translate URLs in Headers**: Keep this value as **Yes** unless your application required the original host header in the authentication request.</span></span>
   - <span data-ttu-id="07a48-145">**URL's in de hoofdtekst van de toepassing te vertalen**: deze waarde als behouden **Nee** tenzij u hardcoded HTML-koppelingen naar andere on-premises toepassingen hebben en geen aangepaste domeinen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="07a48-145">**Translate URLs in Application Body**: Keep this value as **No** unless you have hardcoded HTML links to other on-premises applications, and don't use custom domains.</span></span> <span data-ttu-id="07a48-146">Zie voor meer informatie [koppelen vertaling met toepassingsproxy](application-proxy-link-translation.md).</span><span class="sxs-lookup"><span data-stu-id="07a48-146">For more information, see [Link translation with Application Proxy](application-proxy-link-translation.md).</span></span>
   
   ![Uw toepassing configureren](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. <span data-ttu-id="07a48-148">Selecteer **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="07a48-148">Select **Add**.</span></span>


## <a name="add-a-test-user"></a><span data-ttu-id="07a48-149">Een testgebruiker toevoegen</span><span class="sxs-lookup"><span data-stu-id="07a48-149">Add a test user</span></span> 

<span data-ttu-id="07a48-150">Als u wilt testen dat uw app correct is gepubliceerd, moet u een test-gebruikersaccount toevoegen.</span><span class="sxs-lookup"><span data-stu-id="07a48-150">To test that your app was published correctly, add a test user account.</span></span> <span data-ttu-id="07a48-151">Controleer of dit account heeft al machtigingen voor toegang tot de app uit binnen het bedrijfsnetwerk.</span><span class="sxs-lookup"><span data-stu-id="07a48-151">Verify that this account already has permissions to access the app from inside the corporate network.</span></span>

1. <span data-ttu-id="07a48-152">Selecteer terug op de blade snel starten **een gebruiker toewijzen voor het testen van**.</span><span class="sxs-lookup"><span data-stu-id="07a48-152">Back on the Quick start blade, select **Assign a user for testing**.</span></span>

  ![Een gebruiker toewijzen voor het testen](./media/application-proxy-publish-azure-portal/assign-user.png)

2. <span data-ttu-id="07a48-154">Selecteer op de gebruikers en groepen blade **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="07a48-154">On the Users and groups blade, select **Add**.</span></span>

  ![Een gebruiker of groep toevoegen](./media/application-proxy-publish-azure-portal/add-user.png)

3. <span data-ttu-id="07a48-156">Selecteer op het tabblad van de toewijzing toevoegen **gebruikers en groepen** kies vervolgens het account dat u wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="07a48-156">On the Add assignment blade, select **Users and groups** then choose the account you want to add.</span></span> 
4. <span data-ttu-id="07a48-157">Selecteer **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="07a48-157">Select **Assign**.</span></span>

## <a name="test-your-published-app"></a><span data-ttu-id="07a48-158">Uw gepubliceerde app testen</span><span class="sxs-lookup"><span data-stu-id="07a48-158">Test your published app</span></span>

<span data-ttu-id="07a48-159">Navigeer naar de externe URL die u hebt geconfigureerd tijdens de stap voor publiceren in uw browser.</span><span class="sxs-lookup"><span data-stu-id="07a48-159">In your browser, navigate to the external URL that you configured during the publish step.</span></span> <span data-ttu-id="07a48-160">U moet het startscherm Zie en kunnen aanmelden met de testaccount die u instelt.</span><span class="sxs-lookup"><span data-stu-id="07a48-160">You should see the start screen, and be able to sign in with the test account you set up.</span></span>

![Uw gepubliceerde app testen](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a><span data-ttu-id="07a48-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="07a48-162">Next steps</span></span>
- <span data-ttu-id="07a48-163">[Downloaden van connectors](active-directory-application-proxy-enable.md) en [connector groepen maken](active-directory-application-proxy-connectors-azure-portal.md) voor het publiceren van toepassingen op afzonderlijke netwerken en locaties.</span><span class="sxs-lookup"><span data-stu-id="07a48-163">[Download connectors](active-directory-application-proxy-enable.md) and [create connector groups](active-directory-application-proxy-connectors-azure-portal.md) to publish applications on separate networks and locations.</span></span>

- <span data-ttu-id="07a48-164">[Instellen van eenmalige aanmelding](application-proxy-sso-azure-portal.md) voor uw zojuist gepubliceerde app</span><span class="sxs-lookup"><span data-stu-id="07a48-164">[Set up single sign-on](application-proxy-sso-azure-portal.md) for your newly published app</span></span>
