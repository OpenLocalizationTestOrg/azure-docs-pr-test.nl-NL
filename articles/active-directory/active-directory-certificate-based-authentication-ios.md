---
title: aaaAzure certificaat gebaseerde verificatie van Active Directory voor iOS | Microsoft Docs
description: Meer informatie over Hallo ondersteund scenario's en het Hallo-vereisten voor het configureren van verificatie op basis van certificaten in oplossingen met iOS-apparaten
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
ms.openlocfilehash: 4486ff5239c2897b3bc187053f31d74807430301
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-ios"></a><span data-ttu-id="dc0e6-103">Azure Active Directory gebaseerde verificatie op iOS</span><span class="sxs-lookup"><span data-stu-id="dc0e6-103">Azure Active Directory certificate-based authentication on iOS</span></span>

<span data-ttu-id="dc0e6-104">Certificaat gebaseerde verificatie (CBA) kunt u toobe geverifieerd door Azure Active Directory met een clientcertificaat op een Windows-, Android of iOS-apparaat verbinding te maken met uw Exchange online-account in:</span><span class="sxs-lookup"><span data-stu-id="dc0e6-104">Certificate-based authentication (CBA) enables you toobe authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

* <span data-ttu-id="dc0e6-105">Mobiele Office-toepassingen zoals Microsoft Outlook en Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="dc0e6-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   
* <span data-ttu-id="dc0e6-106">Exchange ActiveSync (EAS)-clients</span><span class="sxs-lookup"><span data-stu-id="dc0e6-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="dc0e6-107">Configuratie van deze functie wordt voorkomen dat Hallo nodig tooenter een gebruikersnaam en wachtwoord combinatie in bepaalde e-mail en Microsoft Office-toepassingen op uw mobiele apparaat.</span><span class="sxs-lookup"><span data-stu-id="dc0e6-107">Configuring this feature eliminates hello need tooenter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="dc0e6-108">Dit onderwerp vindt u Hallo vereisten en Hallo ondersteund scenario's voor het configureren van CBA op een apparaat iOS(Android) voor gebruikers van tenants in Office 365 Enterprise, Business, Education, US Government, China en Duitsland plant.</span><span class="sxs-lookup"><span data-stu-id="dc0e6-108">This topic provides you with hello requirements and hello supported scenarios for configuring CBA on an iOS(Android) device for users of tenants in Office 365 Enterprise, Business, Education, US Government, China, and Germany plans.</span></span>

<span data-ttu-id="dc0e6-109">Deze functie is beschikbaar in preview in Office 365 US Government verdediging en Federal plannen.</span><span class="sxs-lookup"><span data-stu-id="dc0e6-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span></span>




## <a name="office-mobile-applications-support"></a><span data-ttu-id="dc0e6-110">Ondersteuning voor mobiele Office-toepassingen</span><span class="sxs-lookup"><span data-stu-id="dc0e6-110">Office mobile applications support</span></span>

| <span data-ttu-id="dc0e6-111">Apps</span><span class="sxs-lookup"><span data-stu-id="dc0e6-111">Apps</span></span> | <span data-ttu-id="dc0e6-112">Ondersteuning</span><span class="sxs-lookup"><span data-stu-id="dc0e6-112">Support</span></span> |
| --- | --- |
| <span data-ttu-id="dc0e6-113">Azure Information Protection-app</span><span class="sxs-lookup"><span data-stu-id="dc0e6-113">Azure Information Protection app</span></span> |![Selecteren][1] |
| <span data-ttu-id="dc0e6-115">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="dc0e6-115">Microsoft Teams</span></span> |![Selecteren][1] |
| <span data-ttu-id="dc0e6-117">OneNote</span><span class="sxs-lookup"><span data-stu-id="dc0e6-117">OneNote</span></span> |![Selecteren][1] |
| <span data-ttu-id="dc0e6-119">OneDrive</span><span class="sxs-lookup"><span data-stu-id="dc0e6-119">OneDrive</span></span> |![Selecteren][1] |
| <span data-ttu-id="dc0e6-121">Outlook</span><span class="sxs-lookup"><span data-stu-id="dc0e6-121">Outlook</span></span> |![Selecteren][1] |
| <span data-ttu-id="dc0e6-123">Mobiele apps van Power BI</span><span class="sxs-lookup"><span data-stu-id="dc0e6-123">Power BI mobile apps</span></span> |![Selecteren][1] |
| <span data-ttu-id="dc0e6-125">Skype voor bedrijven</span><span class="sxs-lookup"><span data-stu-id="dc0e6-125">Skype for Business</span></span> |![Selecteren][1] |
| <span data-ttu-id="dc0e6-127">Word / Excel / PowerPoint</span><span class="sxs-lookup"><span data-stu-id="dc0e6-127">Word / Excel / PowerPoint</span></span> |![Selecteren][1] |
| <span data-ttu-id="dc0e6-129">Yammer</span><span class="sxs-lookup"><span data-stu-id="dc0e6-129">Yammer</span></span> |![Selecteren][1] |


## <a name="requirements"></a><span data-ttu-id="dc0e6-131">Vereisten</span><span class="sxs-lookup"><span data-stu-id="dc0e6-131">Requirements</span></span> 

<span data-ttu-id="dc0e6-132">Hallo versie van besturingssysteem van het apparaat moet iOS 9 en hoger</span><span class="sxs-lookup"><span data-stu-id="dc0e6-132">hello device OS version must be iOS 9 and above</span></span> 

<span data-ttu-id="dc0e6-133">Een federation-server moet worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="dc0e6-133">A federation server must be configured.</span></span>  

<span data-ttu-id="dc0e6-134">Microsoft Authenticator is vereist voor de Office-toepassingen op iOS.</span><span class="sxs-lookup"><span data-stu-id="dc0e6-134">Microsoft Authenticator is required for Office applications on iOS.</span></span>  

<span data-ttu-id="dc0e6-135">Voor Azure Active Directory toorevoke een clientcertificaat bevatten Hallo AD FS-token Hallo claims te volgen:</span><span class="sxs-lookup"><span data-stu-id="dc0e6-135">For Azure Active Directory toorevoke a client certificate, hello ADFS token must have hello following claims:</span></span>  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  <span data-ttu-id="dc0e6-136">(serienummer van het clientcertificaat Hallo Hallo)</span><span class="sxs-lookup"><span data-stu-id="dc0e6-136">(hello serial number of hello client certificate)</span></span> 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  <span data-ttu-id="dc0e6-137">(Hallo tekenreeks voor de verlener van het clientcertificaat Hallo Hallo)</span><span class="sxs-lookup"><span data-stu-id="dc0e6-137">(hello string for hello issuer of hello client certificate)</span></span> 

<span data-ttu-id="dc0e6-138">Azure Active Directory toegevoegd deze claimtoken voor het vernieuwen van toohello als ze beschikbaar in AD FS-token van het hello (of andere SAML-token zijn).</span><span class="sxs-lookup"><span data-stu-id="dc0e6-138">Azure Active Directory adds these claims toohello refresh token if they are available in hello ADFS token (or any other SAML token).</span></span> <span data-ttu-id="dc0e6-139">Wanneer het vernieuwingstoken Hallo toobe gevalideerd moet, is deze informatie gebruikte toocheck Hallo intrekken.</span><span class="sxs-lookup"><span data-stu-id="dc0e6-139">When hello refresh token needs toobe validated, this information is used toocheck hello revocation.</span></span> 

<span data-ttu-id="dc0e6-140">Als een best practice moet u Hallo ADFS foutpagina's bijwerken met de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="dc0e6-140">As a best practice, you should update hello ADFS error pages with hello following:</span></span>

* <span data-ttu-id="dc0e6-141">Hallo vereiste voor het installeren van Microsoft Authenticator Hallo op iOS</span><span class="sxs-lookup"><span data-stu-id="dc0e6-141">hello requirement for installing hello Microsoft Authenticator on iOS</span></span>
* <span data-ttu-id="dc0e6-142">Instructies voor het tooget een gebruikerscertificaat.</span><span class="sxs-lookup"><span data-stu-id="dc0e6-142">Instructions on how tooget a user certificate.</span></span> 

<span data-ttu-id="dc0e6-143">Zie voor meer informatie [Hallo Sign in AD FS's aanpassen](https://technet.microsoft.com/library/dn280950.aspx).</span><span class="sxs-lookup"><span data-stu-id="dc0e6-143">For more details, see [Customizing hello AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span></span>

<span data-ttu-id="dc0e6-144">Sommige Office-apps (met moderne verificatie is ingeschakeld) verzenden '*prompt = aanmelding*' tooAzure AD in de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="dc0e6-144">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ tooAzure AD in their request.</span></span> <span data-ttu-id="dc0e6-145">Standaard Azure AD zet dit in Hallo aanvraag tooADFS te '*wauth = usernamepassworduri*' (vraagt ADFS toodo U/P auth) en '*wfresh = 0*' (vraagt ADFS tooignore SSO-status en voer een nieuwe verificatie) .</span><span class="sxs-lookup"><span data-stu-id="dc0e6-145">By default, Azure AD translates this in hello request tooADFS too‘*wauth=usernamepassworduri*’ (asks ADFS toodo U/P auth) and ‘*wfresh=0*’ (asks ADFS tooignore SSO state and do a fresh authentication).</span></span> <span data-ttu-id="dc0e6-146">Als u wilt dat tooenable op certificaten gebaseerde verificatie voor deze apps, moet u toomodify Hallo standaardgedrag Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc0e6-146">If you want tooenable certificate-based authentication for these apps, you need toomodify hello default Azure AD behavior.</span></span> <span data-ttu-id="dc0e6-147">NET set Hallo '*PromptLoginBehavior*' in de federatieve domeininstellingen te '*uitgeschakelde*'.</span><span class="sxs-lookup"><span data-stu-id="dc0e6-147">Just set hello ‘*PromptLoginBehavior*’ in your federated domain settings too‘*Disabled*‘.</span></span> <span data-ttu-id="dc0e6-148">U kunt Hallo [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet tooperform deze taak:</span><span class="sxs-lookup"><span data-stu-id="dc0e6-148">You can use hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet tooperform this task:</span></span>

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`
  

## <a name="exchange-activesync-clients-support"></a><span data-ttu-id="dc0e6-149">Ondersteuning voor Exchange ActiveSync-clients</span><span class="sxs-lookup"><span data-stu-id="dc0e6-149">Exchange ActiveSync clients support</span></span>
<span data-ttu-id="dc0e6-150">In iOS 9 of hoger, wordt Hallo systeemeigen iOS-e-mailclient ondersteund.</span><span class="sxs-lookup"><span data-stu-id="dc0e6-150">On iOS 9 or later, hello native iOS mail client is supported.</span></span> <span data-ttu-id="dc0e6-151">Voor alle andere toepassingen Exchange ActiveSync toodetermine als deze functie wordt ondersteund, contact op met de ontwikkelaar van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="dc0e6-151">For all other Exchange ActiveSync applications, toodetermine if this feature is supported, contact your application developer.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="dc0e6-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dc0e6-152">Next steps</span></span>

<span data-ttu-id="dc0e6-153">Als u tooconfigure certificaat gebaseerde verificatie in uw omgeving wilt, Zie [aan de slag met verificatie op basis van certificaten op Android](active-directory-certificate-based-authentication-get-started.md) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="dc0e6-153">If you want tooconfigure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) for instructions.</span></span>


<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-ios/ic195031.png
