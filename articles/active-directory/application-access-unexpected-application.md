---
title: aaaUnexpected toepassing in de lijst met mijn toepassingen | Microsoft Docs
description: Hoe toosee alle toepassingen in uw tenant en u begrijpt hoe toepassingen worden weergegeven in de lijst met alle toepassingen onder bedrijfstoepassingen
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 2f974046b655bc36a05f002c56511a8a988cd01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-application-in-my-applications-list"></a><span data-ttu-id="92b88-103">Onverwachte toepassing in de lijst met mijn toepassingen</span><span class="sxs-lookup"><span data-stu-id="92b88-103">Unexpected application in my applications list</span></span>

<span data-ttu-id="92b88-104">In dit artikel kunt u toounderstand hoe toepassingen worden weergegeven in uw **alle toepassingen** lijst onder **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="92b88-104">This article help you toounderstand how applications appear in your **All Applications** list under **Enterprise Applications**.</span></span> 

## <a name="how-toosee-all-applications-in-your-tenant"></a><span data-ttu-id="92b88-105">Hoe toosee alle toepassingen in uw tenant</span><span class="sxs-lookup"><span data-stu-id="92b88-105">How toosee all applications in your tenant</span></span>

<span data-ttu-id="92b88-106">toosee alle toepassingen in uw tenant hello, moet u toouse hello **Filter** beheren tooshow **alle toepassingen** onder Hallo **alle toepassingen** lijst.</span><span class="sxs-lookup"><span data-stu-id="92b88-106">toosee all hello applications in your tenant, you need toouse hello **Filter** control tooshow **All Applications** under hello **All Applications** list.</span></span> <span data-ttu-id="92b88-107">toodo deze, Hallo stappen hieronder:</span><span class="sxs-lookup"><span data-stu-id="92b88-107">toodo this, follow hello steps below:</span></span>

1.  <span data-ttu-id="92b88-108">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="92b88-108">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="92b88-109">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="92b88-109">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="92b88-110">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="92b88-110">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="92b88-111">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="92b88-111">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="92b88-112">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="92b88-112">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="92b88-113">Klik op Hallo gebruik Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="92b88-113">click hello use hello **Filter** control at hello top of hello **All Applications List**.</span></span>

7.  <span data-ttu-id="92b88-114">Op Hallo **Filter** blade, set Hallo **weergeven** optie te**alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="92b88-114">On hello **Filter** blade, set hello **Show** option too**All Applications.**</span></span>

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a><span data-ttu-id="92b88-115">Waarom wordt er een specifieke toepassing weergegeven in de lijst met alle toepassingen?</span><span class="sxs-lookup"><span data-stu-id="92b88-115">Why does a specific application appear in my all applications list?</span></span>

<span data-ttu-id="92b88-116">Wanneer te gefilterd**alle toepassingen**, Hallo **alle toepassingen** **lijst** toont elk Service-Principal-object in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="92b88-116">When filtered too**All Applications**, hello **All Applications** **List** shows every Service Principal object in your tenant.</span></span> <span data-ttu-id="92b88-117">Service-Principal-objecten kunnen worden weergegeven in deze lijst op een verschillende manieren:</span><span class="sxs-lookup"><span data-stu-id="92b88-117">Service Principal objects can appear in this list in a various ways:</span></span>

1.  <span data-ttu-id="92b88-118">Wanneer u een toepassing van Hallo-toepassingsgalerie toevoegt, waaronder:</span><span class="sxs-lookup"><span data-stu-id="92b88-118">When you add any application from hello application gallery, including:</span></span>

   1. <span data-ttu-id="92b88-119">**Azure AD-galerie toepassingen** : een toepassing die vooraf geïntegreerde voor eenmalige aanmelding met Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="92b88-119">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

   2. <span data-ttu-id="92b88-120">**Application Proxy toepassingen** : een toepassing die wordt uitgevoerd in uw on-premises omgeving dat u wilt dat tooprovide beveiligde eenmalige aanmelding tooexternally.</span><span class="sxs-lookup"><span data-stu-id="92b88-120">**Application Proxy Applications** – An application running in your on-premises environment that you want tooprovide secure single-sign on tooexternally.</span></span>

   3. <span data-ttu-id="92b88-121">**Aangepaste ontwikkelde toepassingen** : een toepassing die uw organisatie wil toodevelop op Azure AD-ontwikkelplatform voor toepassing hello, maar die mogelijk niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="92b88-121">**Custom-developed Applications** – An application that your organization wishes toodevelop on hello Azure AD Application Development Platform, but that may not exist yet.</span></span>

   4. <span data-ttu-id="92b88-122">**Niet-galerie toepassingen** : Breng uw eigen toepassingen!</span><span class="sxs-lookup"><span data-stu-id="92b88-122">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="92b88-123">Een webkoppeling die u wilt dat alle toepassingen die een veld de gebruikersnaam en wachtwoord SAML of OpenID Connect-protocollen ondersteunt of ondersteunt SCIM die u wenst dat toointegrate voor eenmalige aanmelding met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92b88-123">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish toointegrate for single sign-on with Azure AD.</span></span>

2.  <span data-ttu-id="92b88-124">Wanneer zich aanmelden voor of aanmelden bij een 3<sup>rd</sup> of een toepassing die is geïntegreerd met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="92b88-124">When signing up for, or signing in to, a 3<sup>rd</sup> party application integrated with Azure Active Directory.</span></span> <span data-ttu-id="92b88-125">Een voorbeeld hiervan is [Smartsheet](https://app.smartsheet.com/b/home) of [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span><span class="sxs-lookup"><span data-stu-id="92b88-125">One example of this is [Smartsheet](https://app.smartsheet.com/b/home) or [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span></span>

3.  <span data-ttu-id="92b88-126">Wanneer u zich aanmelden voor of een licentie tooa gebruiker of groep tooa eerste toepassing van een leverancier toe te voegen, zoals [Microsoft Office 365](http://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="92b88-126">When signing up for, or adding a license tooa user or a group tooa first party application, like [Microsoft Office 365](http://products.office.com/).</span></span>

4.  <span data-ttu-id="92b88-127">Wanneer u de registratie van een nieuwe toepassing toevoegt door het maken van een toepassing die aangepaste zijn ontwikkeld met behulp van Hallo [toepassingsregister](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span><span class="sxs-lookup"><span data-stu-id="92b88-127">When you add a new application registration by creating a custom-developed application using hello [Application Registry](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span></span>

5.  <span data-ttu-id="92b88-128">Wanneer u de registratie van een nieuwe toepassing toevoegt door het maken van een toepassing die aangepaste zijn ontwikkeld met behulp van Hallo [V2.0-Portal voor registratie van toepassing](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span><span class="sxs-lookup"><span data-stu-id="92b88-128">When you add a new application registration by creating a custom-developed application using hello [V2.0 Application Registration Portal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span></span>

6.  <span data-ttu-id="92b88-129">Wanneer u een toepassing toevoegen u ontwikkelt met Visual Studio [ASP.net verificatiemethoden](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) of [verbonden Services](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).</span><span class="sxs-lookup"><span data-stu-id="92b88-129">When you add an application you’re developing using Visual Studio’s [ASP.net Authentication Methods](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) or [Connected Services](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).</span></span>

7.  <span data-ttu-id="92b88-130">Wanneer u een service principal-object met behulp van Hallo maakt [Azure AD PowerShell-Module](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="92b88-130">When you create a service principal object using hello [Azure AD PowerShell Module](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

8.  <span data-ttu-id="92b88-131">Wanneer u [tooan toepassing toestemming](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) als een beheerder toouse gegevens in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="92b88-131">When you [consent tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) as an administrator toouse data in your tenant.</span></span>

9.  <span data-ttu-id="92b88-132">Wanneer een [gebruiker hiermee akkoord gaat tooan toepassing](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toouse gegevens in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="92b88-132">When a [user consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toouse data in your tenant.</span></span>

10. <span data-ttu-id="92b88-133">Wanneer u bepaalde services waarmee gegevens worden opgeslagen in uw tenant inschakelen.</span><span class="sxs-lookup"><span data-stu-id="92b88-133">When you enable certain services that store data in your tenant.</span></span> <span data-ttu-id="92b88-134">Een voorbeeld hiervan is het wachtwoord opnieuw instellen, die is gemodelleerd als een service-principal toostore uw wachtwoord opnieuw instellen van beleid veilig.</span><span class="sxs-lookup"><span data-stu-id="92b88-134">One example of this is Password Reset, which is modeled as a service principal toostore your password reset policy securely.</span></span>

<span data-ttu-id="92b88-135">tooget meer informatie over hoe tooyour-directory worden toegevoegd in apps Lees [hoe en waarom toepassingen tooAzure AD zijn toegevoegd](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span><span class="sxs-lookup"><span data-stu-id="92b88-135">tooget more details on how apps are added tooyour directory, read [How and why applications are added tooAzure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span></span>

## <a name="i-want-tooremove-a-specific-users-or-groups-assignment-tooan-application"></a><span data-ttu-id="92b88-136">Ik wil tooremove dat een specifieke gebruiker of groep van toewijzing tooan toepassing</span><span class="sxs-lookup"><span data-stu-id="92b88-136">I want tooremove a specific user’s or group’s assignment tooan application</span></span>

<span data-ttu-id="92b88-137">een gebruiker of groep toewijzing tooan toepassing tooremove Hallo stappen in Hallo volgen [de toewijzing van een gebruiker of groep verwijderen uit een enterprise-app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) artikel.</span><span class="sxs-lookup"><span data-stu-id="92b88-137">tooremove a user or group assignment tooan application, follow hello steps listed in hello [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

## <a name="i-want-toodisable-all-access-tooan-application-for-every-user"></a><span data-ttu-id="92b88-138">Ik wil toodisable alle access tooan-toepassing voor elke gebruiker</span><span class="sxs-lookup"><span data-stu-id="92b88-138">I want toodisable all access tooan application for every user</span></span>

<span data-ttu-id="92b88-139">toodisable alle aanmeldingen tooan Gebruikerstoepassing, volg Hallo de stappen die worden vermeld in Hallo [gebruikersaanmeldingen een enterprise-App in Azure Active Directory uitschakelen](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) artikel.</span><span class="sxs-lookup"><span data-stu-id="92b88-139">toodisable all user sign-ins tooan application, follow hello steps listed in hello [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-toodelete-an-application-entirely"></a><span data-ttu-id="92b88-140">Ik wil dat een toepassing toodelete volledig</span><span class="sxs-lookup"><span data-stu-id="92b88-140">I want toodelete an application entirely</span></span>

<span data-ttu-id="92b88-141">te**verwijderen van een toepassing**, volgt u onderstaande instructies voor Hallo:</span><span class="sxs-lookup"><span data-stu-id="92b88-141">too**delete an application**, follow hello instructions below:</span></span>

1.  <span data-ttu-id="92b88-142">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="92b88-142">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="92b88-143">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="92b88-143">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="92b88-144">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="92b88-144">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="92b88-145">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="92b88-145">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="92b88-146">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="92b88-146">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="92b88-147">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="92b88-147">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="92b88-148">Selecteer de gewenste toodelete Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="92b88-148">Select hello application you want toodelete.</span></span>

7.  <span data-ttu-id="92b88-149">Nadat de toepassing hello wordt geladen, klikt u op **verwijderen** pictogram van Hallo bovenste toepassing **overzicht** blade.</span><span class="sxs-lookup"><span data-stu-id="92b88-149">Once hello application loads, click **Delete** icon from hello top application’s **Overview** blade.</span></span>

## <a name="i-want-toodisable-all-future-user-consent-operations-tooany-application"></a><span data-ttu-id="92b88-150">Ik wil toodisable alle toekomstige toestemming operations tooany-Gebruikerstoepassing</span><span class="sxs-lookup"><span data-stu-id="92b88-150">I want toodisable all future user consent operations tooany application</span></span>

<span data-ttu-id="92b88-151">Toestemming van de gebruiker uitschakelt voor uw hele directory voorkomen dat eindgebruikers van ermee akkoord dat tooany toepassing.</span><span class="sxs-lookup"><span data-stu-id="92b88-151">Disabling user consent for your entire directory prevent end users from consenting tooany application.</span></span> <span data-ttu-id="92b88-152">Beheerders kunnen nog steeds op behalves van de gebruiker toestemming.</span><span class="sxs-lookup"><span data-stu-id="92b88-152">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="92b88-153">toolearn meer informatie over de toepassing toestemming geven en waarom u kunt of wilt niet toodo, Lees [wat gebruikers- en toestemming van de beheerder](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span><span class="sxs-lookup"><span data-stu-id="92b88-153">toolearn more about application consent, and why you may or may not wish toodo this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="92b88-154">te**uitschakelen alle toekomstige gebruikers toestemming bewerkingen in uw hele directory**, volgt u onderstaande instructies voor Hallo:</span><span class="sxs-lookup"><span data-stu-id="92b88-154">too**disable all future user consent operations in your entire directory**, follow hello instructions below:</span></span>

1.  <span data-ttu-id="92b88-155">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="92b88-155">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="92b88-156">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="92b88-156">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="92b88-157">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="92b88-157">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="92b88-158">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="92b88-158">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="92b88-159">Klik op **gebruikersinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="92b88-159">click **User settings**.</span></span>

6.  <span data-ttu-id="92b88-160">Alle toekomstige gebruikers toestemming bewerkingen uitschakelen door Hallo instelling **gebruikers apps tooaccess kunnen toestaan hun gegevens** te schakelen**Nee** en klik op Hallo **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="92b88-160">Disable all future user consent operations by setting hello **Users can allow apps tooaccess their data** toggle too**No** and click hello **Save** button.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92b88-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="92b88-161">Next steps</span></span>
[<span data-ttu-id="92b88-162">Toepassingen beheren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="92b88-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
