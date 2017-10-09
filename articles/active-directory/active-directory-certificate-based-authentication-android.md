---
title: aaaAzure certificaat gebaseerde verificatie van Active Directory op Android | Microsoft Docs
description: Meer informatie over Hallo ondersteund scenario's en het Hallo-vereisten voor het configureren van verificatie op basis van certificaten in oplossingen met Android-apparaten
services: active-directory
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/28/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 148275fa3da610530c278fcd57e02e907f735d9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-android"></a><span data-ttu-id="5b927-103">Azure Active Directory gebaseerde verificatie voor Android</span><span class="sxs-lookup"><span data-stu-id="5b927-103">Azure Active Directory certificate-based authentication on Android</span></span>


<span data-ttu-id="5b927-104">Certificaat gebaseerde verificatie (CBA) kunt u toobe geverifieerd door Azure Active Directory met een clientcertificaat op een Windows-, Android of iOS-apparaat verbinding te maken met uw Exchange online-account in:</span><span class="sxs-lookup"><span data-stu-id="5b927-104">Certificate-based authentication (CBA) enables you toobe authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

* <span data-ttu-id="5b927-105">Mobiele Office-toepassingen zoals Microsoft Outlook en Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="5b927-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   
* <span data-ttu-id="5b927-106">Exchange ActiveSync (EAS)-clients</span><span class="sxs-lookup"><span data-stu-id="5b927-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="5b927-107">Configuratie van deze functie wordt voorkomen dat Hallo nodig tooenter een gebruikersnaam en wachtwoord combinatie in bepaalde e-mail en Microsoft Office-toepassingen op uw mobiele apparaat.</span><span class="sxs-lookup"><span data-stu-id="5b927-107">Configuring this feature eliminates hello need tooenter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="5b927-108">Dit onderwerp vindt u Hallo vereisten en Hallo ondersteund scenario's voor het configureren van CBA op een apparaat iOS(Android) voor gebruikers van tenants in Office 365 Enterprise, Business, Education, US Government, China en Duitsland plant.</span><span class="sxs-lookup"><span data-stu-id="5b927-108">This topic provides you with hello requirements and hello supported scenarios for configuring CBA on an iOS(Android) device for users of tenants in Office 365 Enterprise, Business, Education, US Government, China, and Germany plans.</span></span>



<span data-ttu-id="5b927-109">Deze functie is beschikbaar in preview in Office 365 US Government verdediging en Federal plannen.</span><span class="sxs-lookup"><span data-stu-id="5b927-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span></span>


## <a name="office-mobile-applications-support"></a><span data-ttu-id="5b927-110">Ondersteuning voor mobiele Office-toepassingen</span><span class="sxs-lookup"><span data-stu-id="5b927-110">Office mobile applications support</span></span>
| <span data-ttu-id="5b927-111">Apps</span><span class="sxs-lookup"><span data-stu-id="5b927-111">Apps</span></span> | <span data-ttu-id="5b927-112">Ondersteuning</span><span class="sxs-lookup"><span data-stu-id="5b927-112">Support</span></span> |
| --- | --- |
| <span data-ttu-id="5b927-113">Azure Information Protection-app</span><span class="sxs-lookup"><span data-stu-id="5b927-113">Azure Information Protection app</span></span> |![Selecteren][1] |
| <span data-ttu-id="5b927-115">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="5b927-115">Microsoft Teams</span></span> |![Selecteren][1] |
| <span data-ttu-id="5b927-117">OneNote</span><span class="sxs-lookup"><span data-stu-id="5b927-117">OneNote</span></span> |![Selecteren][1] |
| <span data-ttu-id="5b927-119">OneDrive</span><span class="sxs-lookup"><span data-stu-id="5b927-119">OneDrive</span></span> |![Selecteren][1] |
| <span data-ttu-id="5b927-121">Outlook</span><span class="sxs-lookup"><span data-stu-id="5b927-121">Outlook</span></span> |![Selecteren][1] |
| <span data-ttu-id="5b927-123">Mobiele apps van Power BI</span><span class="sxs-lookup"><span data-stu-id="5b927-123">Power BI mobile apps</span></span> |![Selecteren][1] |
| <span data-ttu-id="5b927-125">Skype voor bedrijven</span><span class="sxs-lookup"><span data-stu-id="5b927-125">Skype for Business</span></span> |![Selecteren][1] |
| <span data-ttu-id="5b927-127">Word / Excel / PowerPoint</span><span class="sxs-lookup"><span data-stu-id="5b927-127">Word / Excel / PowerPoint</span></span> |![Selecteren][1] |
| <span data-ttu-id="5b927-129">Yammer</span><span class="sxs-lookup"><span data-stu-id="5b927-129">Yammer</span></span> |![Selecteren][1] |


### <a name="implementation-requirements"></a><span data-ttu-id="5b927-131">Vereisten voor implementatie</span><span class="sxs-lookup"><span data-stu-id="5b927-131">Implementation requirements</span></span>

<span data-ttu-id="5b927-132">Hallo versie van besturingssysteem van het apparaat moet Android 5.0 (Lollipop) en hoger.</span><span class="sxs-lookup"><span data-stu-id="5b927-132">hello device OS version must be Android 5.0 (Lollipop) and above.</span></span> 

<span data-ttu-id="5b927-133">Een federation-server moet worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="5b927-133">A federation server must be configured.</span></span>  

<span data-ttu-id="5b927-134">Voor Azure Active Directory toorevoke een clientcertificaat bevatten Hallo AD FS-token Hallo claims te volgen:</span><span class="sxs-lookup"><span data-stu-id="5b927-134">For Azure Active Directory toorevoke a client certificate, hello ADFS token must have hello following claims:</span></span>  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  <span data-ttu-id="5b927-135">(serienummer van het clientcertificaat Hallo Hallo)</span><span class="sxs-lookup"><span data-stu-id="5b927-135">(hello serial number of hello client certificate)</span></span> 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  <span data-ttu-id="5b927-136">(Hallo tekenreeks voor de verlener van het clientcertificaat Hallo Hallo)</span><span class="sxs-lookup"><span data-stu-id="5b927-136">(hello string for hello issuer of hello client certificate)</span></span> 

<span data-ttu-id="5b927-137">Azure Active Directory toegevoegd deze claimtoken voor het vernieuwen van toohello als ze beschikbaar in AD FS-token van het hello (of andere SAML-token zijn).</span><span class="sxs-lookup"><span data-stu-id="5b927-137">Azure Active Directory adds these claims toohello refresh token if they are available in hello ADFS token (or any other SAML token).</span></span> <span data-ttu-id="5b927-138">Wanneer het vernieuwingstoken Hallo toobe gevalideerd moet, is deze informatie gebruikte toocheck Hallo intrekken.</span><span class="sxs-lookup"><span data-stu-id="5b927-138">When hello refresh token needs toobe validated, this information is used toocheck hello revocation.</span></span> 

<span data-ttu-id="5b927-139">Als een best practice moet u Hallo ADFS foutpagina's bijwerken met instructies voor het tooget een gebruikerscertificaat.</span><span class="sxs-lookup"><span data-stu-id="5b927-139">As a best practice, you should update hello ADFS error pages with instructions on how tooget a user certificate.</span></span>  
<span data-ttu-id="5b927-140">Zie voor meer informatie [Hallo Sign in AD FS's aanpassen](https://technet.microsoft.com/library/dn280950.aspx).</span><span class="sxs-lookup"><span data-stu-id="5b927-140">For more details, see [Customizing hello AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span></span>  

<span data-ttu-id="5b927-141">Sommige Office-apps (met moderne verificatie is ingeschakeld) verzenden '*prompt = aanmelding*' tooAzure AD in de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="5b927-141">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ tooAzure AD in their request.</span></span> <span data-ttu-id="5b927-142">Standaard Azure AD zet dit in Hallo aanvraag tooADFS te '*wauth = usernamepassworduri*' (vraagt ADFS toodo U/P auth) en '*wfresh = 0*' (vraagt ADFS tooignore SSO-status en voer een nieuwe verificatie) .</span><span class="sxs-lookup"><span data-stu-id="5b927-142">By default, Azure AD translates this in hello request tooADFS too‘*wauth=usernamepassworduri*’ (asks ADFS toodo U/P auth) and ‘*wfresh=0*’ (asks ADFS tooignore SSO state and do a fresh authentication).</span></span> <span data-ttu-id="5b927-143">Als u wilt dat tooenable op certificaten gebaseerde verificatie voor deze apps, moet u toomodify Hallo standaardgedrag Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b927-143">If you want tooenable certificate-based authentication for these apps, you need toomodify hello default Azure AD behavior.</span></span> <span data-ttu-id="5b927-144">NET set Hallo '*PromptLoginBehavior*' in de federatieve domeininstellingen te '*uitgeschakelde*'.</span><span class="sxs-lookup"><span data-stu-id="5b927-144">Just set hello ‘*PromptLoginBehavior*’ in your federated domain settings too‘*Disabled*‘.</span></span> <span data-ttu-id="5b927-145">U kunt Hallo [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet tooperform deze taak:</span><span class="sxs-lookup"><span data-stu-id="5b927-145">You can use hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet tooperform this task:</span></span>

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`



## <a name="exchange-activesync-clients-support"></a><span data-ttu-id="5b927-146">Ondersteuning voor Exchange ActiveSync-clients</span><span class="sxs-lookup"><span data-stu-id="5b927-146">Exchange ActiveSync clients support</span></span>
<span data-ttu-id="5b927-147">Bepaalde Exchange ActiveSync-toepassingen (Lollipop) voor Android 5.0 of hoger worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="5b927-147">Certain Exchange ActiveSync applications on Android 5.0 (Lollipop) or later are supported.</span></span> <span data-ttu-id="5b927-148">toodetermine als deze functie biedt ondersteuning voor de e-mailtoepassing Neem contact op met de ontwikkelaar van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="5b927-148">toodetermine if your email application does support this feature, please contact your application developer.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="5b927-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5b927-149">Next steps</span></span>

<span data-ttu-id="5b927-150">Als u tooconfigure certificaat gebaseerde verificatie in uw omgeving wilt, Zie [aan de slag met verificatie op basis van certificaten op Android](active-directory-certificate-based-authentication-get-started.md) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="5b927-150">If you want tooconfigure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) for instructions.</span></span>

<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-android/ic195031.png
