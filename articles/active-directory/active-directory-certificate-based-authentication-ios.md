---
title: Azure Active Directory gebaseerde verificatie op iOS | Microsoft Docs
description: Meer informatie over de ondersteunde scenario's en de vereisten voor het configureren op certificaten gebaseerde verificatie in oplossingen met iOS-apparaten
services: active-directory
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: 26a6fc54-0153-44fb-b970-9b432c99e9f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: c781f3f054fad5c5092fed5058c932fd4e97cf35
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-ios"></a><span data-ttu-id="f5ded-103">Azure Active Directory gebaseerde verificatie op iOS</span><span class="sxs-lookup"><span data-stu-id="f5ded-103">Azure Active Directory certificate-based authentication on iOS</span></span>

<span data-ttu-id="f5ded-104">Certificaat gebaseerde verificatie (CBA) kunt u moeten worden geverifieerd door Azure Active Directory met een clientcertificaat op een Windows-, Android of iOS-apparaat verbinding te maken met uw Exchange online-account in:</span><span class="sxs-lookup"><span data-stu-id="f5ded-104">Certificate-based authentication (CBA) enables you to be authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

* <span data-ttu-id="f5ded-105">Mobiele Office-toepassingen zoals Microsoft Outlook en Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="f5ded-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   
* <span data-ttu-id="f5ded-106">Exchange ActiveSync (EAS)-clients</span><span class="sxs-lookup"><span data-stu-id="f5ded-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="f5ded-107">Configuratie van deze functie wordt voorkomen moet een combinatie van gebruikersnaam en wachtwoord invoeren in bepaalde e-mail en Microsoft Office-toepassingen op uw mobiele apparaat.</span><span class="sxs-lookup"><span data-stu-id="f5ded-107">Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="f5ded-108">Dit onderwerp vindt u de vereisten en de ondersteunde scenario's voor het configureren van CBA op een apparaat iOS(Android) voor gebruikers van tenants in Office 365 Enterprise, Business, Education, US Government, China en Duitsland plant.</span><span class="sxs-lookup"><span data-stu-id="f5ded-108">This topic provides you with the requirements and the supported scenarios for configuring CBA on an iOS(Android) device for users of tenants in Office 365 Enterprise, Business, Education, US Government, China, and Germany plans.</span></span>

<span data-ttu-id="f5ded-109">Deze functie is beschikbaar in preview in Office 365 US Government verdediging en Federal plannen.</span><span class="sxs-lookup"><span data-stu-id="f5ded-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span></span>




## <a name="office-mobile-applications-support"></a><span data-ttu-id="f5ded-110">Ondersteuning voor mobiele Office-toepassingen</span><span class="sxs-lookup"><span data-stu-id="f5ded-110">Office mobile applications support</span></span>

| <span data-ttu-id="f5ded-111">Apps</span><span class="sxs-lookup"><span data-stu-id="f5ded-111">Apps</span></span> | <span data-ttu-id="f5ded-112">Ondersteuning</span><span class="sxs-lookup"><span data-stu-id="f5ded-112">Support</span></span> |
| --- | --- |
| <span data-ttu-id="f5ded-113">Azure Information Protection-app</span><span class="sxs-lookup"><span data-stu-id="f5ded-113">Azure Information Protection app</span></span> |![Selecteren][1] |
| <span data-ttu-id="f5ded-115">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f5ded-115">Microsoft Teams</span></span> |![Selecteren][1] |
| <span data-ttu-id="f5ded-117">OneNote</span><span class="sxs-lookup"><span data-stu-id="f5ded-117">OneNote</span></span> |![Selecteren][1] |
| <span data-ttu-id="f5ded-119">OneDrive</span><span class="sxs-lookup"><span data-stu-id="f5ded-119">OneDrive</span></span> |![Selecteren][1] |
| <span data-ttu-id="f5ded-121">Outlook</span><span class="sxs-lookup"><span data-stu-id="f5ded-121">Outlook</span></span> |![Selecteren][1] |
| <span data-ttu-id="f5ded-123">Mobiele apps van Power BI</span><span class="sxs-lookup"><span data-stu-id="f5ded-123">Power BI mobile apps</span></span> |![Selecteren][1] |
| <span data-ttu-id="f5ded-125">Skype voor bedrijven</span><span class="sxs-lookup"><span data-stu-id="f5ded-125">Skype for Business</span></span> |![Selecteren][1] |
| <span data-ttu-id="f5ded-127">Word / Excel / PowerPoint</span><span class="sxs-lookup"><span data-stu-id="f5ded-127">Word / Excel / PowerPoint</span></span> |![Selecteren][1] |
| <span data-ttu-id="f5ded-129">Yammer</span><span class="sxs-lookup"><span data-stu-id="f5ded-129">Yammer</span></span> |![Selecteren][1] |


## <a name="requirements"></a><span data-ttu-id="f5ded-131">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f5ded-131">Requirements</span></span> 

<span data-ttu-id="f5ded-132">De versie van het besturingssysteem van het apparaat moet iOS 9 en hoger</span><span class="sxs-lookup"><span data-stu-id="f5ded-132">The device OS version must be iOS 9 and above</span></span> 

<span data-ttu-id="f5ded-133">Een federation-server moet worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="f5ded-133">A federation server must be configured.</span></span>  

<span data-ttu-id="f5ded-134">Microsoft Authenticator is vereist voor de Office-toepassingen op iOS.</span><span class="sxs-lookup"><span data-stu-id="f5ded-134">Microsoft Authenticator is required for Office applications on iOS.</span></span>  

<span data-ttu-id="f5ded-135">Voor Azure Active Directory voor het intrekken van een clientcertificaat, moet het AD FS-token hebben de volgende claims:</span><span class="sxs-lookup"><span data-stu-id="f5ded-135">For Azure Active Directory to revoke a client certificate, the ADFS token must have the following claims:</span></span>  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  <span data-ttu-id="f5ded-136">(Het serienummer van het clientcertificaat)</span><span class="sxs-lookup"><span data-stu-id="f5ded-136">(The serial number of the client certificate)</span></span> 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  <span data-ttu-id="f5ded-137">(De tekenreeks voor de verlener van het clientcertificaat)</span><span class="sxs-lookup"><span data-stu-id="f5ded-137">(The string for the issuer of the client certificate)</span></span> 

<span data-ttu-id="f5ded-138">Azure Active Directory toegevoegd deze claims naar het vernieuwingstoken als ze beschikbaar in de AD FS-token (of andere SAML-token zijn).</span><span class="sxs-lookup"><span data-stu-id="f5ded-138">Azure Active Directory adds these claims to the refresh token if they are available in the ADFS token (or any other SAML token).</span></span> <span data-ttu-id="f5ded-139">Wanneer het vernieuwingstoken dat worden gevalideerd moet, wordt deze informatie wordt gebruikt om te controleren van de intrekking.</span><span class="sxs-lookup"><span data-stu-id="f5ded-139">When the refresh token needs to be validated, this information is used to check the revocation.</span></span> 

<span data-ttu-id="f5ded-140">Als een best practice moet u de AD FS-foutpagina's bijwerken met de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="f5ded-140">As a best practice, you should update the ADFS error pages with the following:</span></span>

* <span data-ttu-id="f5ded-141">De vereiste voor het installeren van de Microsoft-Authenticator op iOS</span><span class="sxs-lookup"><span data-stu-id="f5ded-141">The requirement for installing the Microsoft Authenticator on iOS</span></span>
* <span data-ttu-id="f5ded-142">Instructies voor het ophalen van het certificaat van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f5ded-142">Instructions on how to get a user certificate.</span></span> 

<span data-ttu-id="f5ded-143">Zie voor meer informatie [aanpassen van de AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span><span class="sxs-lookup"><span data-stu-id="f5ded-143">For more details, see [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span></span>

<span data-ttu-id="f5ded-144">Sommige Office-apps (met moderne verificatie is ingeschakeld) verzenden '*prompt = aanmelding*' naar Azure AD in de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="f5ded-144">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ to Azure AD in their request.</span></span> <span data-ttu-id="f5ded-145">Standaard Azure AD zet dit in de aanvraag voor ADFS naar '*wauth = usernamepassworduri*' (AD FS wilt U/P auth vragen) en '*wfresh = 0*' (vraagt ADFS te negeren van SSO-status en een nieuwe verificatie).</span><span class="sxs-lookup"><span data-stu-id="f5ded-145">By default, Azure AD translates this in the request to ADFS to ‘*wauth=usernamepassworduri*’ (asks ADFS to do U/P auth) and ‘*wfresh=0*’ (asks ADFS to ignore SSO state and do a fresh authentication).</span></span> <span data-ttu-id="f5ded-146">Als u verificatie inschakelen op basis van certificaten voor deze apps wilt, moet u het standaardgedrag voor Azure AD te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f5ded-146">If you want to enable certificate-based authentication for these apps, you need to modify the default Azure AD behavior.</span></span> <span data-ttu-id="f5ded-147">Stelt u de '*PromptLoginBehavior*'in de instellingen van het federatieve domein naar'*uitgeschakelde*'.</span><span class="sxs-lookup"><span data-stu-id="f5ded-147">Just set the ‘*PromptLoginBehavior*’ in your federated domain settings to ‘*Disabled*‘.</span></span> <span data-ttu-id="f5ded-148">U kunt de [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet deze taak uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="f5ded-148">You can use the [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet to perform this task:</span></span>

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`
  

## <a name="exchange-activesync-clients-support"></a><span data-ttu-id="f5ded-149">Ondersteuning voor Exchange ActiveSync-clients</span><span class="sxs-lookup"><span data-stu-id="f5ded-149">Exchange ActiveSync clients support</span></span>
<span data-ttu-id="f5ded-150">In iOS 9 of hoger, wordt de systeemeigen iOS-e-mailclient ondersteund.</span><span class="sxs-lookup"><span data-stu-id="f5ded-150">On iOS 9 or later, the native iOS mail client is supported.</span></span> <span data-ttu-id="f5ded-151">Voor alle andere Exchange ActiveSync-toepassingen om te bepalen of deze functie wordt ondersteund, contact op met de ontwikkelaar van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="f5ded-151">For all other Exchange ActiveSync applications, to determine if this feature is supported, contact your application developer.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="f5ded-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f5ded-152">Next steps</span></span>

<span data-ttu-id="f5ded-153">Als u verificatie configureren op basis van certificaten in uw omgeving wilt, Zie [aan de slag met verificatie op basis van certificaten op Android](active-directory-certificate-based-authentication-get-started.md) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="f5ded-153">If you want to configure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) for instructions.</span></span>


<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-ios/ic195031.png
