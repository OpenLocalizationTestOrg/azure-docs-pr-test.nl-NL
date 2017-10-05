---
title: Onverwachte toepassing in de lijst met mijn toepassingen | Microsoft Docs
description: Hoe zien alle toepassingen in uw tenant en u begrijpt hoe toepassingen worden weergegeven in de lijst met alle toepassingen onder bedrijfstoepassingen
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
ms.openlocfilehash: 0f8136cb066fa6e3e4a8dd06e34b9f866e3916f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="unexpected-application-in-my-applications-list"></a><span data-ttu-id="ca5fc-103">Onverwachte toepassing in de lijst met mijn toepassingen</span><span class="sxs-lookup"><span data-stu-id="ca5fc-103">Unexpected application in my applications list</span></span>

<span data-ttu-id="ca5fc-104">In dit artikel helpen te begrijpen hoe toepassingen worden weergegeven in uw **alle toepassingen** lijst onder **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-104">This article help you to understand how applications appear in your **All Applications** list under **Enterprise Applications**.</span></span> 

## <a name="how-to-see-all-applications-in-your-tenant"></a><span data-ttu-id="ca5fc-105">Hoe ziet u alle toepassingen in uw tenant</span><span class="sxs-lookup"><span data-stu-id="ca5fc-105">How to see all applications in your tenant</span></span>

<span data-ttu-id="ca5fc-106">Overzicht van alle toepassingen in uw tenant, moet u gebruiken de **Filter** besturingselement om weer te geven **alle toepassingen** onder de **alle toepassingen** lijst.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-106">To see all the applications in your tenant, you need to use the **Filter** control to show **All Applications** under the **All Applications** list.</span></span> <span data-ttu-id="ca5fc-107">U doet dit door de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="ca5fc-107">To do this, follow the steps below:</span></span>

1.  <span data-ttu-id="ca5fc-108">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="ca5fc-108">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ca5fc-109">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-109">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ca5fc-110">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-110">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ca5fc-111">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-111">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ca5fc-112">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-112">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="ca5fc-113">Klik op het gebruik de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-113">click the use the **Filter** control at the top of the **All Applications List**.</span></span>

7.  <span data-ttu-id="ca5fc-114">Op de **Filter** blade ingesteld de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="ca5fc-114">On the **Filter** blade, set the **Show** option to **All Applications.**</span></span>

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a><span data-ttu-id="ca5fc-115">Waarom wordt er een specifieke toepassing weergegeven in de lijst met alle toepassingen?</span><span class="sxs-lookup"><span data-stu-id="ca5fc-115">Why does a specific application appear in my all applications list?</span></span>

<span data-ttu-id="ca5fc-116">Wanneer gefilterd op **alle toepassingen**, wordt de **alle toepassingen** **lijst** toont elk Service-Principal-object in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-116">When filtered to **All Applications**, the **All Applications** **List** shows every Service Principal object in your tenant.</span></span> <span data-ttu-id="ca5fc-117">Service-Principal-objecten kunnen worden weergegeven in deze lijst op een verschillende manieren:</span><span class="sxs-lookup"><span data-stu-id="ca5fc-117">Service Principal objects can appear in this list in a various ways:</span></span>

1.  <span data-ttu-id="ca5fc-118">Wanneer u een toepassing uit de galerie met toepassingen toevoegt, waaronder:</span><span class="sxs-lookup"><span data-stu-id="ca5fc-118">When you add any application from the application gallery, including:</span></span>

   1. <span data-ttu-id="ca5fc-119">**Azure AD-galerie toepassingen** : een toepassing die vooraf geïntegreerde voor eenmalige aanmelding met Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-119">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

   2. <span data-ttu-id="ca5fc-120">**Application Proxy toepassingen** : een toepassing die wordt uitgevoerd in uw on-premises omgeving die u wilt extern beveiligde eenmalige aanmelding op te geven.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-120">**Application Proxy Applications** – An application running in your on-premises environment that you want to provide secure single-sign on to externally.</span></span>

   3. <span data-ttu-id="ca5fc-121">**Aangepaste ontwikkelde toepassingen** : een toepassing die uw organisatie wil ontwikkelen op het Azure AD-toepassing ontwikkelplatform, maar die mogelijk niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-121">**Custom-developed Applications** – An application that your organization wishes to develop on the Azure AD Application Development Platform, but that may not exist yet.</span></span>

   4. <span data-ttu-id="ca5fc-122">**Niet-galerie toepassingen** : Breng uw eigen toepassingen!</span><span class="sxs-lookup"><span data-stu-id="ca5fc-122">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="ca5fc-123">Een webkoppeling die u wilt dat alle toepassingen die een veld de gebruikersnaam en wachtwoord SAML of OpenID Connect-protocollen ondersteunt of ondersteunt SCIM die u wilt integreren voor eenmalige aanmelding met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-123">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish to integrate for single sign-on with Azure AD.</span></span>

2.  <span data-ttu-id="ca5fc-124">Wanneer zich aanmelden voor of aanmelden bij een 3<sup>rd</sup> of een toepassing die is geïntegreerd met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-124">When signing up for, or signing in to, a 3<sup>rd</sup> party application integrated with Azure Active Directory.</span></span> <span data-ttu-id="ca5fc-125">Een voorbeeld hiervan is [Smartsheet](https://app.smartsheet.com/b/home) of [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca5fc-125">One example of this is [Smartsheet](https://app.smartsheet.com/b/home) or [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span></span>

3.  <span data-ttu-id="ca5fc-126">Wanneer u zich aanmelden voor of een licentie toe te voegen aan een gebruiker of een groep aan een eerste toepassing van derden, zoals [Microsoft Office 365](http://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="ca5fc-126">When signing up for, or adding a license to a user or a group to a first party application, like [Microsoft Office 365](http://products.office.com/).</span></span>

4.  <span data-ttu-id="ca5fc-127">Wanneer u een nieuwe toepassingsregistratie toevoegen door het maken van een toepassing aangepaste ontwikkeld met de [toepassingsregister](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span><span class="sxs-lookup"><span data-stu-id="ca5fc-127">When you add a new application registration by creating a custom-developed application using the [Application Registry](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span></span>

5.  <span data-ttu-id="ca5fc-128">Wanneer u een nieuwe toepassingsregistratie toevoegen door het maken van een toepassing aangepaste ontwikkeld met de [V2.0-Portal voor registratie van toepassing](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span><span class="sxs-lookup"><span data-stu-id="ca5fc-128">When you add a new application registration by creating a custom-developed application using the [V2.0 Application Registration Portal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span></span>

6.  <span data-ttu-id="ca5fc-129">Wanneer u een toepassing toevoegen u ontwikkelt met Visual Studio [ASP.net verificatiemethoden](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) of [verbonden Services](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca5fc-129">When you add an application you’re developing using Visual Studio’s [ASP.net Authentication Methods](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) or [Connected Services](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).</span></span>

7.  <span data-ttu-id="ca5fc-130">Wanneer u maakt een service-principal-object met de [Azure AD PowerShell-Module](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="ca5fc-130">When you create a service principal object using the [Azure AD PowerShell Module](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

8.  <span data-ttu-id="ca5fc-131">Wanneer u [toestemming geeft om een toepassing te](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) als beheerder om gegevens te gebruiken in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-131">When you [consent to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) as an administrator to use data in your tenant.</span></span>

9.  <span data-ttu-id="ca5fc-132">Wanneer een [gebruiker hiermee akkoord gaat tot een toepassing](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) om gegevens te gebruiken in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-132">When a [user consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to use data in your tenant.</span></span>

10. <span data-ttu-id="ca5fc-133">Wanneer u bepaalde services waarmee gegevens worden opgeslagen in uw tenant inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-133">When you enable certain services that store data in your tenant.</span></span> <span data-ttu-id="ca5fc-134">Een voorbeeld hiervan is wachtwoord opnieuw instellen, die is gemodelleerd als een service-principal voor het opslaan van uw wachtwoord opnieuw instellen van beleid veilig.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-134">One example of this is Password Reset, which is modeled as a service principal to store your password reset policy securely.</span></span>

<span data-ttu-id="ca5fc-135">Als u meer informatie over hoe apps worden toegevoegd aan uw directory, lezen [hoe en waarom toepassingen worden toegevoegd aan Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span><span class="sxs-lookup"><span data-stu-id="ca5fc-135">To get more details on how apps are added to your directory, read [How and why applications are added to Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span></span>

## <a name="i-want-to-remove-a-specific-users-or-groups-assignment-to-an-application"></a><span data-ttu-id="ca5fc-136">Ik wil een specifieke gebruiker of groep van toewijzing aan een toepassing verwijderen</span><span class="sxs-lookup"><span data-stu-id="ca5fc-136">I want to remove a specific user’s or group’s assignment to an application</span></span>

<span data-ttu-id="ca5fc-137">Als u wilt verwijderen van een gebruiker of groepstoewijzing aan een toepassing, volg de stappen in de [de toewijzing van een gebruiker of groep verwijderen uit een enterprise-app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) artikel.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-137">To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

## <a name="i-want-to-disable-all-access-to-an-application-for-every-user"></a><span data-ttu-id="ca5fc-138">Ik wil alle toegang tot een toepassing voor elke gebruiker uitschakelen</span><span class="sxs-lookup"><span data-stu-id="ca5fc-138">I want to disable all access to an application for every user</span></span>

<span data-ttu-id="ca5fc-139">Schakel alle gebruikersaanmeldingen tot een toepassing die de stappen die worden vermeld in de [gebruikersaanmeldingen een enterprise-App in Azure Active Directory uitschakelen](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) artikel.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-139">To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-to-delete-an-application-entirely"></a><span data-ttu-id="ca5fc-140">Ik wil een toepassing volledig verwijderen</span><span class="sxs-lookup"><span data-stu-id="ca5fc-140">I want to delete an application entirely</span></span>

<span data-ttu-id="ca5fc-141">Naar **verwijderen van een toepassing**, volgt u onderstaande instructies:</span><span class="sxs-lookup"><span data-stu-id="ca5fc-141">To **delete an application**, follow the instructions below:</span></span>

1.  <span data-ttu-id="ca5fc-142">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="ca5fc-142">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ca5fc-143">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-143">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ca5fc-144">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-144">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ca5fc-145">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-145">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ca5fc-146">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-146">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="ca5fc-147">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="ca5fc-147">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="ca5fc-148">Selecteer de toepassing die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-148">Select the application you want to delete.</span></span>

7.  <span data-ttu-id="ca5fc-149">Nadat de toepassing wordt geladen, klikt u op **verwijderen** pictogram van de bovenste toepassing **overzicht** blade.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-149">Once the application loads, click **Delete** icon from the top application’s **Overview** blade.</span></span>

## <a name="i-want-to-disable-all-future-user-consent-operations-to-any-application"></a><span data-ttu-id="ca5fc-150">Ik wil alle bewerkingen van toekomstige gebruikers toestemming voor elke toepassing uitschakelen</span><span class="sxs-lookup"><span data-stu-id="ca5fc-150">I want to disable all future user consent operations to any application</span></span>

<span data-ttu-id="ca5fc-151">Toestemming van de gebruiker uitschakelt voor uw hele directory te voorkomen dat eindgebruikers ermee akkoord dat elke toepassing.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-151">Disabling user consent for your entire directory prevent end users from consenting to any application.</span></span> <span data-ttu-id="ca5fc-152">Beheerders kunnen nog steeds op behalves van de gebruiker toestemming.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-152">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="ca5fc-153">Meer informatie over de toepassing toestemming en waarom u niet wilt doen, of lezen [wat gebruikers- en toestemming van de beheerder](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span><span class="sxs-lookup"><span data-stu-id="ca5fc-153">To learn more about application consent, and why you may or may not wish to do this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="ca5fc-154">Naar **uitschakelen alle toekomstige gebruikers toestemming bewerkingen in uw hele directory**, volgt u onderstaande instructies:</span><span class="sxs-lookup"><span data-stu-id="ca5fc-154">To **disable all future user consent operations in your entire directory**, follow the instructions below:</span></span>

1.  <span data-ttu-id="ca5fc-155">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="ca5fc-155">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="ca5fc-156">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-156">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ca5fc-157">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-157">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ca5fc-158">Klik op **gebruikers en groepen** in het navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-158">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="ca5fc-159">Klik op **gebruikersinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-159">click **User settings**.</span></span>

6.  <span data-ttu-id="ca5fc-160">Alle toekomstige gebruikers toestemming bewerkingen uitschakelen door in te stellen de **gebruikers kunnen toestaan dat apps toegang tot hun gegevens** in-of uitschakelen op **Nee** en klik op de **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="ca5fc-160">Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca5fc-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ca5fc-161">Next steps</span></span>
[<span data-ttu-id="ca5fc-162">Toepassingen beheren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ca5fc-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
