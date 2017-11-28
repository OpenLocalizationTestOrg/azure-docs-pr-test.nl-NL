---
title: Wat is het toegangsvenster in Azure Active Directory? | Microsoft Docs
description: Informatie over het gebruik van variaties van het toegangsvenster (webbrowser, Android-app, iPhone en iPad app) voor toegang tot SaaS-apps.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: c0252d01-7e6e-4f79-a70e-600479577dfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd9066c251188c0f18fe1a9403baa2beaeeb987c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-the-access-panel"></a><span data-ttu-id="56b64-104">Wat is het toegangsvenster?</span><span class="sxs-lookup"><span data-stu-id="56b64-104">What is the access panel?</span></span>

<span data-ttu-id="56b64-105">Het toegangspaneel is een webportal.</span><span class="sxs-lookup"><span data-stu-id="56b64-105">The access panel is a web-based portal.</span></span> <span data-ttu-id="56b64-106">Dit kan een gebruiker met een werk of schoolaccount in Azure Active Directory om te bekijken en cloud-gebaseerde toepassingen start een Azure AD-beheerder heeft deze toegang verleend tot.</span><span class="sxs-lookup"><span data-stu-id="56b64-106">It enables a user with a work or school account in Azure Active Directory to view and start cloud-based applications an Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="56b64-107">U kunt ook groepsbeheer met Self-service en app-mogelijkheden voor beheer via het toegangsvenster gebruiken.</span><span class="sxs-lookup"><span data-stu-id="56b64-107">You can also use self-service group and app management capabilities through the access panel.</span></span>

<span data-ttu-id="56b64-108">Het toegangspaneel is gescheiden van de Azure-portal en komt niet voor u om een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="56b64-108">The access panel is separate from the Azure portal and does not you to have an Azure subscription.</span></span>

![Toegangsvenster][1]

<span data-ttu-id="56b64-110">Het toegangsvenster kunt u enkele van uw profielinstellingen, inclusief de mogelijkheid om te bewerken:</span><span class="sxs-lookup"><span data-stu-id="56b64-110">The access panel enables you to edit some of your profile settings, including the ability to:</span></span>

- <span data-ttu-id="56b64-111">Wijzig het wachtwoord die zijn gekoppeld aan een account voor werk of school</span><span class="sxs-lookup"><span data-stu-id="56b64-111">Change the password associated with a work or school account</span></span>

- <span data-ttu-id="56b64-112">Bewerken van instellingen voor wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="56b64-112">Edit password reset settings</span></span>

- <span data-ttu-id="56b64-113">Bewerken en neem contact op met de prioriteit van instellingen in verband met multi-factor authentication (voor accounts die zijn vereist om deze te gebruiken door een beheerder)</span><span class="sxs-lookup"><span data-stu-id="56b64-113">Edit contact and preference settings related to multi-factor authentication (for accounts that have been required to use it by an administrator)</span></span>

- <span data-ttu-id="56b64-114">Account details, zoals gebruikers-ID, alternatieve e-mailadres en mobile en office telefoonnummers en apparaten bekijken</span><span class="sxs-lookup"><span data-stu-id="56b64-114">View account details, such as user ID, alternate email, and mobile and office phone numbers, and devices</span></span>

- <span data-ttu-id="56b64-115">Weergeven en cloud-gebaseerde toepassingen die de Azure AD-beheerder heeft deze toegang verleend tot starten.</span><span class="sxs-lookup"><span data-stu-id="56b64-115">View and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="56b64-116">Zie voor meer informatie over het toegangsvenster vanuit het perspectief van de gebruikers met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="56b64-116">For more information about the access panel from the users’ perspective, see Using the access panel.</span></span> 

- <span data-ttu-id="56b64-117">Groepen zelf beheren.</span><span class="sxs-lookup"><span data-stu-id="56b64-117">Self-manage groups.</span></span> <span data-ttu-id="56b64-118">Meer specifiek, kan de beheerder maken en beheren van beveiligingsgroepen en aanvragen beveiligingsgroepen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56b64-118">More specifically, the administrator can create and manage security groups and request security group memberships in Azure AD.</span></span> <span data-ttu-id="56b64-119">Zie voor meer informatie [groepsbeheer met Self-service voor gebruikers in Azure AD](active-directory-accessmanagement-self-service-group-management.md) en [groepen beheren](active-directory-manage-groups.md).</span><span class="sxs-lookup"><span data-stu-id="56b64-119">For more information, see [Self-service group management for users in Azure AD](active-directory-accessmanagement-self-service-group-management.md) and [Manage your groups](active-directory-manage-groups.md).</span></span>




## <a name="accessing-the-access-panel"></a><span data-ttu-id="56b64-120">Toegang tot het toegangsvenster</span><span class="sxs-lookup"><span data-stu-id="56b64-120">Accessing the access panel</span></span>

<span data-ttu-id="56b64-121">U kunt toegang krijgen tot het toegangsvenster via de volgende URL in een webbrowser:`http://myapps.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="56b64-121">You can access the access panel by visiting the following URL in a web browser: `http://myapps.microsoft.com`</span></span>

<span data-ttu-id="56b64-122">Als u aangepaste huisstijl is geconfigureerd voor de aanmeldingspagina hebt, kunt u deze huisstijl door het domein van uw organisatie aan het einde van de URL toe te voegen kunt laden:`http://myapps.microsoft.com/<your domain>.com`</span><span class="sxs-lookup"><span data-stu-id="56b64-122">If you have custom branding configured for your sign-in page, you can load this branding by appending your organization’s domain to the end of the URL: `http://myapps.microsoft.com/<your domain>.com`</span></span>

<span data-ttu-id="56b64-123">In dit geval kunt u een actieve of een geverifieerde domeinnaam die is geconfigureerd in uw Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="56b64-123">In this case, you can use any active or verified domain name that has been configured in your Azure portal.</span></span>

![Wingtip Toys domeinnaam][2]  

<span data-ttu-id="56b64-125">U moet de URL voor alle gebruikers die zullen zich aanmelden bij toepassingen die zijn geïntegreerd met Azure AD te verdelen.</span><span class="sxs-lookup"><span data-stu-id="56b64-125">You need to distribute the URL to all users who will sign in to applications that are integrated with Azure AD.</span></span>

## <a name="authentication"></a><span data-ttu-id="56b64-126">Authentication</span><span class="sxs-lookup"><span data-stu-id="56b64-126">Authentication</span></span>

<span data-ttu-id="56b64-127">Bereiken van het toegangsvenster, moet u worden geverifieerd via een account voor werk of school in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56b64-127">To reach the access panel, you must be authenticated through a work or school account in Azure AD.</span></span> <span data-ttu-id="56b64-128">U kunt naar rechtstreeks Azure AD zijn geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="56b64-128">You can be authenticated to Azure AD directly.</span></span> <span data-ttu-id="56b64-129">U kunt ook als een organisatie heeft federation geconfigureerd met behulp van Active Directory Federation Services (AD FS) of andere technologieën, kan u worden geverifieerd door Windows Server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="56b64-129">Alternatively, if an organization has configured federation by using Active Directory Federation Services (AD FS) or other technologies, you can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="56b64-130">Als u een abonnement voor Azure of Office 365 hebt en u hebt gebruikt de Azure portal of een Office 365-toepassing, ziet u de lijst met toepassingen zonder aanmelden opnieuw.</span><span class="sxs-lookup"><span data-stu-id="56b64-130">If you have a subscription for Azure or Office 365 and you have been using the Azure portal or an Office 365 application, you can see the list of applications without signing-in again.</span></span> <span data-ttu-id="56b64-131">Als u niet bent geverifieerd u wordt gevraagd om aan te melden met behulp van de gebruikersnaam en het wachtwoord voor uw account in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56b64-131">If you are are not authenticated you are prompted to sign in by using the username and password for your account in Azure AD.</span></span> <span data-ttu-id="56b64-132">Als uw organisatie heeft federation geconfigureerd, is typt de gebruikersnaam voldoende.</span><span class="sxs-lookup"><span data-stu-id="56b64-132">If your organization has configured federation, typing the username is sufficient.</span></span>

<span data-ttu-id="56b64-133">Wanneer u bent geverifieerd, kunt u communiceren met de toepassingen die de beheerder heeft geïntegreerd in de map.</span><span class="sxs-lookup"><span data-stu-id="56b64-133">When you are authenticated, you can interact with the applications that your administrator has integrated with the directory.</span></span> <span data-ttu-id="56b64-134">Zie voor meer informatie over toepassingen integreren met Azure AD, [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="56b64-134">To learn how to integrate applications with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="web-browser-requirements"></a><span data-ttu-id="56b64-135">Vereisten voor webbrowsers</span><span class="sxs-lookup"><span data-stu-id="56b64-135">Web browser requirements</span></span>

<span data-ttu-id="56b64-136">Ten minste het toegangsvenster vereist een browser die JavaScript ondersteunt en CSS is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="56b64-136">At a minimum, the access panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="56b64-137">Voor de gebruiker zijn aangemeld via op basis van wachtwoorden eenmalige aanmelding (SSO) aan toepassingen, moet de extensie van het Configuratiescherm toegang in uw browser worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="56b64-137">For the user to be signed in to applications through password-based single sign-on (SSO), the access panel extension must be installed in your browser.</span></span> <span data-ttu-id="56b64-138">De extensie wordt automatisch gedownload wanneer u een toepassing die is geconfigureerd voor eenmalige aanmelding op basis van wachtwoorden selecteert.</span><span class="sxs-lookup"><span data-stu-id="56b64-138">The extension is downloaded automatically when you select an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="56b64-139">De extensie van het Configuratiescherm toegang is momenteel beschikbaar voor Internet Explorer 8 en hoger, Microsoft Edge en Chrome Firefox browsers.</span><span class="sxs-lookup"><span data-stu-id="56b64-139">The access panel extension is currently available for Internet Explorer 8 and later, Edge, Chrome, and Firefox browsers.</span></span>

## <a name="mobile-app-support"></a><span data-ttu-id="56b64-140">Ondersteuning voor mobiele Apps</span><span class="sxs-lookup"><span data-stu-id="56b64-140">Mobile app support</span></span>

<span data-ttu-id="56b64-141">Het team van Azure Active Directory publiceert de mijn mobiele app van apps.</span><span class="sxs-lookup"><span data-stu-id="56b64-141">The Azure Active Directory team publishes the my apps mobile app.</span></span> <span data-ttu-id="56b64-142">Wanneer u de app installeert, kunt u zich aanmeldt bij de SSO-toepassingen op basis van wachtwoorden op iOS en Android-apparaten.</span><span class="sxs-lookup"><span data-stu-id="56b64-142">When you install the app, you can sign in to password-based SSO applications on iOS and Android devices.</span></span>

> [!NOTE]
> <span data-ttu-id="56b64-143">U kunt aanmelden bij toepassingen die ondersteuning bieden voor federatie met Azure AD (inclusief Salesforce, Google Apps, Dropbox, Box, Concur, Workday, Office 365 en meer dan 70 anderen) op vrijwel elke webbrowser op elk apparaat zonder een invoegtoepassing of mobiele app.</span><span class="sxs-lookup"><span data-stu-id="56b64-143">You can sign in to applications that support federation with Azure AD (including Salesforce, Google Apps, Dropbox, Box, Concur, Workday, Office 365, and more than 70 others) on virtually any web browser, on any device, without needing a plug-in or mobile app.</span></span> <span data-ttu-id="56b64-144">Alle andere [toegang tot Configuratiescherm ervaringen](https://myapps.microsoft.com/) ook hoeven niet de mijn mobiele app van apps moet worden gebruikt op een mobiel apparaat.</span><span class="sxs-lookup"><span data-stu-id="56b64-144">All other [access panel experiences](https://myapps.microsoft.com/) do also not require the my apps mobile app to be used on a mobile device.</span></span>
>
>

### <a name="my-apps-for-android"></a><span data-ttu-id="56b64-145">Mijn apps voor Android</span><span class="sxs-lookup"><span data-stu-id="56b64-145">My apps for Android</span></span>

<span data-ttu-id="56b64-146">Mijn apps voor Android wordt ondersteund op een Android-apparaat met Android versie 4.1 en hoger.</span><span class="sxs-lookup"><span data-stu-id="56b64-146">My apps for Android is supported on any Android device that is running Android version 4.1 and later.</span></span>  
<span data-ttu-id="56b64-147">Is beschikbaar in de [Google Play store](https://play.google.com/store/apps/details?id=com.microsoft.myapps).</span><span class="sxs-lookup"><span data-stu-id="56b64-147">It is available in the [Google Play store](https://play.google.com/store/apps/details?id=com.microsoft.myapps).</span></span>

![Mijn apps voor Android][3]   

### <a name="my-apps-for-iphone-and-ipad"></a><span data-ttu-id="56b64-149">Mijn apps voor iPhone en iPad</span><span class="sxs-lookup"><span data-stu-id="56b64-149">My apps for iPhone and iPad</span></span>

<span data-ttu-id="56b64-150">Mijn apps voor iOS wordt ondersteund op een iPhone of iPad met versie voor iOS 7 en hoger.</span><span class="sxs-lookup"><span data-stu-id="56b64-150">My apps for iOS is supported on any iPhone or iPad that is running iOS version 7 and later.</span></span>  
<span data-ttu-id="56b64-151">Is beschikbaar in de [Apple App Store](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8).</span><span class="sxs-lookup"><span data-stu-id="56b64-151">It is available in the [Apple App Store](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8).</span></span>

![Mijn apps voor iOS][4]    



## <a name="managed-browser-for-my-apps"></a><span data-ttu-id="56b64-153">Beheerde browser voor mijn apps</span><span class="sxs-lookup"><span data-stu-id="56b64-153">Managed browser for my apps</span></span>

<span data-ttu-id="56b64-154">Mijn apps is ook geïntegreerd in de Intune Managed Browser.</span><span class="sxs-lookup"><span data-stu-id="56b64-154">My apps is also integrated in the Intune Managed Browser.</span></span> <span data-ttu-id="56b64-155">De Intune Managed Browser voor iOS en Android-apparaten speelt een belangrijke rol om ervoor te zorgen dat de gegevens op mobiele apparaten beveiligd blijven.</span><span class="sxs-lookup"><span data-stu-id="56b64-155">The Intune Managed Browser for iOS and Android devices plays a key role in ensuring that data on mobile devices stays secure.</span></span> <span data-ttu-id="56b64-156">Hiermee kunt u veilig kunt weergeven en webpagina's die mogelijk bedrijfsgegevens bevatten en biedt een veilige websurfervaring.</span><span class="sxs-lookup"><span data-stu-id="56b64-156">It lets you safely view and navigate web pages that might contain company information, and provides a secure web-browsing experience.</span></span>  
<span data-ttu-id="56b64-157">U snel toegang tot mijn apps op uw startpagina van Managed Browser en in uw bladwijzers, zodat u minder klikken bereiken van elke toepassing die u wilt openen.</span><span class="sxs-lookup"><span data-stu-id="56b64-157">You find quick access to my apps on your Managed Browser homepage and in your bookmarks, giving you fewer clicks to reach any application you want to access.</span></span>

<span data-ttu-id="56b64-158">Is beschikbaar in de [Apple App Store](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) en [Google Play Store](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).</span><span class="sxs-lookup"><span data-stu-id="56b64-158">It is available in the [Apple App Store](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) and [Google Play Store](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).</span></span>

![Mananged browser voor mijn apps][5]    





## <a name="tips-for-testing-the-user-experience"></a><span data-ttu-id="56b64-160">Tips voor het testen van de gebruikerservaring</span><span class="sxs-lookup"><span data-stu-id="56b64-160">Tips for testing the user experience</span></span>

<span data-ttu-id="56b64-161">Als u een Azure-beheerder bent en u bent aangemeld bij de Azure-portal met behulp van een account in de directory, bent u automatisch aangemeld voor het toegangsvenster als uw huidige account gebruiken.</span><span class="sxs-lookup"><span data-stu-id="56b64-161">If you are an Azure administrator and you are signed in to the Azure portal by using an account in the directory, you are automatically signed in to the access panel as your current account.</span></span> <span data-ttu-id="56b64-162">In dit geval ziet u alle toepassingen die aan u zijn toegewezen.</span><span class="sxs-lookup"><span data-stu-id="56b64-162">In this case, you can see all applications that have been assigned to you.</span></span>

<span data-ttu-id="56b64-163">**Voor testen als een *verschillende* gebruikersaccount:**</span><span class="sxs-lookup"><span data-stu-id="56b64-163">**To test as a *different* user account:**</span></span>

1. <span data-ttu-id="56b64-164">Klik op het gebruikersmenu in de rechterbovenhoek van de Azure-portal of in het deelvenster toegang en selecteer vervolgens **Afmelden**.</span><span class="sxs-lookup"><span data-stu-id="56b64-164">Click the user menu in the upper-right corner of the Azure portal or the access panel, and then select **Sign Out**.</span></span> 
2. <span data-ttu-id="56b64-165">Ga naar de [toegangspaneel](http://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="56b64-165">Go to the [access panel](http://myapps.microsoft.com).</span></span>
3. <span data-ttu-id="56b64-166">Typ de gebruikersnaam en het wachtwoord voor het account in uw directory die u wilt testen op de aanmeldingspagina.</span><span class="sxs-lookup"><span data-stu-id="56b64-166">On the sign-in page, type the username and password for the account in your directory you want to test.</span></span>


## <a name="starting-applications"></a><span data-ttu-id="56b64-167">Starten van toepassingen</span><span class="sxs-lookup"><span data-stu-id="56b64-167">Starting applications</span></span>

<span data-ttu-id="56b64-168">Verschillende soorten toepassingen kunnen worden weergegeven in het deelvenster toegang.</span><span class="sxs-lookup"><span data-stu-id="56b64-168">Several types of applications can appear on the access panel.</span></span>

### <a name="office-365-applications"></a><span data-ttu-id="56b64-169">Office 365-toepassingen</span><span class="sxs-lookup"><span data-stu-id="56b64-169">Office 365 applications</span></span>

<span data-ttu-id="56b64-170">Als uw organisatie van Office 365-toepassingen gebruikmaakt en u een licentie voor Office 365-toepassingen worden weergegeven in het deelvenster toegang.</span><span class="sxs-lookup"><span data-stu-id="56b64-170">If your organization is using Office 365 applications and you are licensed for them, the Office 365 applications appear on your access panel.</span></span>

<span data-ttu-id="56b64-171">Als u op de tegel van een toepassing voor een Office 365-toepassing, wordt u omgeleid naar de toepassing en automatisch aangemeld.</span><span class="sxs-lookup"><span data-stu-id="56b64-171">When you click an application tile for an Office 365 application, you are redirected to the application and automatically signed in.</span></span>

### <a name="microsoft-and-third-party-applications-configured-with-federation-based-sso"></a><span data-ttu-id="56b64-172">Microsoft en derden toepassingen die zijn geconfigureerd op basis van een federatieve aanmelding bij</span><span class="sxs-lookup"><span data-stu-id="56b64-172">Microsoft and third-party applications configured with federation-based SSO</span></span>

<span data-ttu-id="56b64-173">Uw beheerder kan toepassingen toevoegen in de sectie Active Directory van de Azure-portal met de SSO-modus ingesteld op **Azure AD Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="56b64-173">Your administrator can add applications in the Active Directory section of the Azure portal with the SSO mode set to **Azure AD Single Sign-On**.</span></span> <span data-ttu-id="56b64-174">U kunt deze toepassingen alleen zien als de beheerder heeft u toegang tot de toepassingen expliciet verleend.</span><span class="sxs-lookup"><span data-stu-id="56b64-174">You can only see these applications if your administrator has explicitly granted you access to the applications.</span></span>

<span data-ttu-id="56b64-175">Als u op een tegel voor een van deze toepassingen, wordt u omgeleid en automatisch aangemeld bij de toepassing.</span><span class="sxs-lookup"><span data-stu-id="56b64-175">When you click a tile for one of these applications, you are redirected and automatically signed in to the application.</span></span>

### <a name="password-based-sso-without-identity-provisioning"></a><span data-ttu-id="56b64-176">Eenmalige aanmelding op basis van wachtwoorden zonder identiteit inrichten</span><span class="sxs-lookup"><span data-stu-id="56b64-176">Password-based SSO without identity provisioning</span></span>

<span data-ttu-id="56b64-177">Uw beheerder kan toepassingen toevoegen in de sectie Active Directory van de Azure-portal met de SSO-modus ingesteld op **op basis van wachtwoorden Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="56b64-177">Your administrator can add applications in the Active Directory section of the Azure portal with the SSO mode set to **Password-based Single Sign-On**.</span></span> <span data-ttu-id="56b64-178">Alle gebruikers in de map ziet alle toepassingen die zijn geconfigureerd in deze modus.</span><span class="sxs-lookup"><span data-stu-id="56b64-178">All users in the directory can see all applications that have been configured in this mode.</span></span>

<span data-ttu-id="56b64-179">De eerste keer u klikken op een tegel voor een van deze toepassingen u wordt gevraagd het wachtwoord SSO-invoegtoepassing voor Internet Explorer of Chrome installeren.</span><span class="sxs-lookup"><span data-stu-id="56b64-179">The first time, you click a tile for one of these applications, you are prompted to install the Password SSO plug-in for Internet Explorer or Chrome.</span></span> <span data-ttu-id="56b64-180">De installatie moet u mogelijk opnieuw opstarten van uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="56b64-180">The installation might require you to restart your web browser.</span></span> <span data-ttu-id="56b64-181">Wanneer u naar het toegangspaneel terugkeert en klikt u nogmaals op de tegel toepassing, wordt u gevraagd om een gebruikersnaam en wachtwoord voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="56b64-181">When you return to the access panel and click the application tile again, you are prompted for a username and password for the application.</span></span> <span data-ttu-id="56b64-182">Wanneer u uw gebruikersnaam en wachtwoord hebt ingevoerd, worden deze referenties veilig opgeslagen en gekoppeld aan uw account in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56b64-182">When you have entered your username and password, these credentials are securely stored and linked to your account in Azure AD.</span></span>

<span data-ttu-id="56b64-183">De volgende keer dat u op de tegel toepassing bent u automatisch aangemeld bij de toepassing.</span><span class="sxs-lookup"><span data-stu-id="56b64-183">The next time you click the application tile, you are automatically signed in to the application.</span></span>  
<span data-ttu-id="56b64-184">U hoeft niet te uw referenties opnieuw invoeren en of het wachtwoord SSO-invoegtoepassing installeren.</span><span class="sxs-lookup"><span data-stu-id="56b64-184">You don't have to enter your credentials again and or install the Password SSO plug-in.</span></span>

<span data-ttu-id="56b64-185">Als uw referenties in de derde partij doeltoepassing hebt gewijzigd, moet u ook de referenties die zijn opgeslagen in Azure AD bijwerken.</span><span class="sxs-lookup"><span data-stu-id="56b64-185">If your credentials have changed in the target third-party application, you must also update your credentials that are stored in Azure AD.</span></span> 

<span data-ttu-id="56b64-186">**Referenties bijwerken:**</span><span class="sxs-lookup"><span data-stu-id="56b64-186">**To update credentials:**</span></span>

1. <span data-ttu-id="56b64-187">Selecteer het pictogram op de tegel toepassing.</span><span class="sxs-lookup"><span data-stu-id="56b64-187">Select the icon on the application tile.</span></span>
2. <span data-ttu-id="56b64-188">Selecteer **referenties bijwerken** gebruikersnaam en wachtwoord voor de toepassing opnieuw in te voeren.</span><span class="sxs-lookup"><span data-stu-id="56b64-188">Select **update credentials** to reenter the username and password for the application.</span></span>


### <a name="password-based-sso-with-identity-provisioning"></a><span data-ttu-id="56b64-189">Eenmalige aanmelding op basis van wachtwoorden met het leveren van identiteit</span><span class="sxs-lookup"><span data-stu-id="56b64-189">Password-based SSO with identity provisioning</span></span>

<span data-ttu-id="56b64-190">Uw beheerder kan toevoegen toepassingen in de **Active Directory** sectie van de Azure-portal met de SSO-modus ingesteld op **op basis van wachtwoorden Single Sign-On**, samen met het inrichten van de identiteit.</span><span class="sxs-lookup"><span data-stu-id="56b64-190">Your administrator can add applications in the **Active Directory** section of the Azure portal with the SSO mode set to **Password-based Single Sign-On**, along with identity provisioning.</span></span>

<span data-ttu-id="56b64-191">De eerste keer gebruikt, u klikt op de tegel van een toepassing voor een van deze toepassingen, wordt u gevraagd voor het installeren van de **wachtwoord SSO-invoegtoepassing voor Internet Explorer of Chrome**.</span><span class="sxs-lookup"><span data-stu-id="56b64-191">The first time, you click an application tile for one of these applications, you are prompted to install the **Password SSO plug-in for Internet Explorer or Chrome**.</span></span> <span data-ttu-id="56b64-192">De installatie moet u mogelijk opnieuw opstarten van uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="56b64-192">The installation might require you to restart your web browser.</span></span>  
<span data-ttu-id="56b64-193">Wanneer u naar het toegangspaneel terugkeert en klikt u op de tegel toepassing opnieuw, bent u automatisch aangemeld bij de toepassing.</span><span class="sxs-lookup"><span data-stu-id="56b64-193">When you return to the access panel and click the application tile again, you are automatically signed in to the application.</span></span>

<span data-ttu-id="56b64-194">Sommige toepassingen moet u mogelijk uw wachtwoord op de eerste aanmeldingspagina te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="56b64-194">Some applications might require you to change your password on the first sign-in.</span></span> <span data-ttu-id="56b64-195">Als uw referenties in de derde partij doeltoepassing hebt gewijzigd, moet u ook de referenties die zijn opgeslagen in Azure AD bijwerken.</span><span class="sxs-lookup"><span data-stu-id="56b64-195">If your credentials have changed in the target third-party application, you must also update the credentials that are stored in Azure AD.</span></span> 

<span data-ttu-id="56b64-196">**Referenties bijwerken:**</span><span class="sxs-lookup"><span data-stu-id="56b64-196">**To update credentials:**</span></span>

1. <span data-ttu-id="56b64-197">Selecteer het pictogram op de tegel toepassing.</span><span class="sxs-lookup"><span data-stu-id="56b64-197">Select the icon on the application tile.</span></span>
2. <span data-ttu-id="56b64-198">Selecteer **referenties bijwerken** gebruikersnaam en wachtwoord voor de toepassing opnieuw in te voeren.</span><span class="sxs-lookup"><span data-stu-id="56b64-198">Select **update credentials** to reenter the username and password for the application.</span></span>


### <a name="application-with-existing-sso-solutions"></a><span data-ttu-id="56b64-199">Toepassing met bestaande oplossingen voor eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="56b64-199">Application with existing SSO solutions</span></span>

<span data-ttu-id="56b64-200">Voor meer informatie over het configureren van eenmalige aanmelding voor een toepassing de Azure portal biedt een derde optie, genaamd **bestaande Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="56b64-200">To configure SSO for an application, the Azure portal provides a third option called **Existing Single Sign-On**.</span></span> <span data-ttu-id="56b64-201">Deze optie kunt de beheerder om een koppeling maken naar een toepassing op en plaats deze in het deelvenster toegang voor geselecteerde gebruikers.</span><span class="sxs-lookup"><span data-stu-id="56b64-201">This option enables your administrator to create a link to an application and place it on the access panel for selected users.</span></span>

<span data-ttu-id="56b64-202">Bijvoorbeeld, als een toepassing is geconfigureerd om gebruikers te verifiëren met behulp van AD FS 2.0, uw beheerder kan gebruiken de **bestaande Single Sign-On** optie voor het maken van een koppeling in het deelvenster toegang.</span><span class="sxs-lookup"><span data-stu-id="56b64-202">For example, if an application is configured to authenticate users by using AD FS 2.0, your administrator can use the **Existing Single Sign-On** option to create a link to it on the access panel.</span></span> <span data-ttu-id="56b64-203">Wanneer u de koppeling opent, kunt u bent geverifieerd via AD FS 2.0 of een andere bestaande oplossing voor eenmalige aanmelding biedt voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="56b64-203">When you access the link, you are authenticated through AD FS 2.0 or whatever existing SSO solution the application provides.</span></span>


## <a name="next-steps"></a><span data-ttu-id="56b64-204">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="56b64-204">Next steps</span></span>

- <span data-ttu-id="56b64-205">Zie voor een lijst met alle onderwerpen met betrekking tot Toepassingsbeheer de [artikel index voor Toepassingsbeheer in Azure Active Directory](active-directory-apps-index.md).</span><span class="sxs-lookup"><span data-stu-id="56b64-205">To see a list of all topics that are related to application management, see the [article index for application management in Azure Active Directory](active-directory-apps-index.md).</span></span>
 
- <span data-ttu-id="56b64-206">Zie voor informatie over het integreren van een SaaS-app in Azure AD, de [lijst met zelfstudies over het integreren van SaaS-apps](active-directory-saas-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="56b64-206">To learn how to integrate a SaaS app into Azure AD, see the [list of tutorials on how to integrate SaaS apps](active-directory-saas-tutorial-list.md).</span></span>
 
- <span data-ttu-id="56b64-207">Zie voor meer informatie over het beheren van apps met Azure AD, de [Inleiding tot één aanmelding en beheren van app-toegang met Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="56b64-207">To learn more about managing apps with Azure AD, see the [introduction to single sign-on and managing app access with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>
 
- <span data-ttu-id="56b64-208">Zie voor meer informatie over gebruikers inrichten, [gebruikers inrichten en opheffen van inrichting tot SaaS-toepassingen automatiseren](active-directory-saas-app-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="56b64-208">To learn more about user provisioning, see [automate user provisioning and deprovisioning to SaaS applications](active-directory-saas-app-provisioning.md).</span></span>

<!--Image references-->
[1]: ./media/active-directory-saas-access-panel-introduction/01.png
[2]: ./media/active-directory-saas-access-panel-introduction/02.png
[3]: ./media/active-directory-saas-access-panel-introduction/03.png
[4]: ./media/active-directory-saas-access-panel-introduction/04.png
[5]: ./media/active-directory-saas-access-panel-introduction/05.png
