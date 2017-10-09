---
title: aaaPage sjablonen in Azure API Management | Microsoft Docs
description: Meer informatie over hoe toocustomize Hallo inhoud van developer portal-pagina's met behulp van een set van sjablonen in Azure API Management.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: e57df269-1019-4b74-b74d-53155b809d59
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 84bd971ad4bcacfdd36c2ebbe05b16063f2a547b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="page-templates-in-azure-api-management"></a><span data-ttu-id="5b388-103">Sjablonen in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="5b388-103">Page templates in Azure API Management</span></span>
<span data-ttu-id="5b388-104">Azure API Management biedt dat u Hallo mogelijkheid toocustomize Hallo inhoud van developer portal-pagina's met behulp van een set van sjablonen die hun inhoud configureren.</span><span class="sxs-lookup"><span data-stu-id="5b388-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="5b388-105">Met behulp van [DotLiquid](http://dotliquidmarkup.org/) syntaxis en het Hallo-editor naar keuze, zoals [DotLiquid voor ontwerpers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), en een opgegeven set gelokaliseerde [resources String](api-management-template-resources.md#strings), [ De glyph-resources](api-management-template-resources.md#glyphs), en [pagina besturingselementen](api-management-page-controls.md), hebt u aanzienlijke flexibiliteit tooconfigure Hallo inhoud van het Hallo-pagina's naar wens met behulp van deze sjablonen.</span><span class="sxs-lookup"><span data-stu-id="5b388-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="5b388-106">Hallo-sjablonen in deze sectie kunt u toocustomize Hallo inhoud van het Hallo-aanmelding in de aanmelding van en pagina's pagina niet vinden in Hallo-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="5b388-106">hello templates in this section allow you toocustomize hello content of hello sign in, sign up, and page not found pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="5b388-107">Aanmelden</span><span class="sxs-lookup"><span data-stu-id="5b388-107">Sign in</span></span>](#SignIn)  
  
-   [<span data-ttu-id="5b388-108">Aanmelden</span><span class="sxs-lookup"><span data-stu-id="5b388-108">Sign up</span></span>](#SignUp)  
  
-   [<span data-ttu-id="5b388-109">Pagina is niet gevonden</span><span class="sxs-lookup"><span data-stu-id="5b388-109">Page not found</span></span>](#PageNotFound)  
  
> [!NOTE]
>  <span data-ttu-id="5b388-110">Standaard-voorbeeldsjablonen zijn opgenomen in de volgende documentatie Hallo, maar onderwerp toochange vanwege toocontinuous verbeteringen zijn.</span><span class="sxs-lookup"><span data-stu-id="5b388-110">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="5b388-111">U kunt Hallo live standaardsjablonen in Hallo developer-portal door te navigeren toohello gewenst afzonderlijke sjablonen weergeven.</span><span class="sxs-lookup"><span data-stu-id="5b388-111">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="5b388-112">Zie voor meer informatie over het werken met sjablonen [hoe toocustomize API Management-portal voor ontwikkelaars met behulp van sjablonen Hallo](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="5b388-112">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="5b388-113"><a name="SignIn"></a>Aanmelden</span><span class="sxs-lookup"><span data-stu-id="5b388-113"><a name="SignIn"></a> Sign in</span></span>  
 <span data-ttu-id="5b388-114">Hallo **aanmelden** sjabloon kunt u toocustomize Hallo aanmelding op de pagina in het Hallo-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="5b388-114">hello **sign in** template allows you toocustomize hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="5b388-115">![Meld u aan de pagina](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "APIM aanmelden pagina Developer Portal-sjablonen")</span><span class="sxs-lookup"><span data-stu-id="5b388-115">![Sign In Page](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "APIM Sign In Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="5b388-116">Standaardsjabloon</span><span class="sxs-lookup"><span data-stu-id="5b388-116">Default template</span></span>  
  
```xml  
<h2 class="text-center">{% localized "SigninStrings|WebAuthenticationSigninTitle" %}</h2>  
{% if registrationEnabled == true %}  
<p class="text-center">{% localized "SigninStrings|WebAuthenticationNotAMember" %}</p>  
{% endif %}  
  
<div class="row center-block ap-idp-container">  
  <div class="col-md-6">  
    {% if registrationEnabled == true %}  
        <p>{% localized "SigninStrings|WebAuthenticationSigininWithPassword" %}</p>  
    <basic-SignIn></basic-SignIn>  
    {% endif %}  
  </div>  
  
    {% if registrationEnabled != true and providers.size == 0 %}  
        {% localized "ProviderInfoStrings|TextboxExternalIdentitiesDisabled" %}  
  {% else %}  
        {% if providers.size > 0 %}  
      <div class="col-md-6">  
            <div class="providers-list">  
                <p class="text-left">  
                {% if registrationEnabled == true %}  
                    {% localized "ProviderInfoStrings|TextboxExternalIdentitiesSigninInvitation" %}  
                {% else %}  
                    {% localized "ProviderInfoStrings|TextboxExternalIdentitiesSigninInvitationPrimary" %}  
                {% endif %}  
                </p>  
        <providers></providers>  
            </div>  
    </div>  
        {% endif %}  
    {% endif %}  
  
  {% if userRegistrationTermsEnabled == true %}  
    <div class="col-md-6">  
        <div id="terms" class="modal" role="dialog" tabindex="-1">  
            <div class="modal-dialog">  
                <div class="modal-content">  
                    <div class="modal-header">  
                        <h4 class="modal-title">{% localized "SigninResources|DialogHeadingTermsOfUse" %}</h4>  
                    </div>  
                    <div class="modal-body break-all">{{userRegistrationTerms}}</div>  
                    <div class="modal-footer">  
                        <button type="button" class="btn btn-default" data-dismiss="modal">{% localized "CommonStrings|ButtonLabelClose" %}</button>  
                    </div>  
                </div>  
            </div>  
        </div>  
        <p>{% localized "SigninResources|TextblockUserRegistrationTermsProvided" %}</p>  
    </div>  
    {% endif %}  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="5b388-117">Besturingselementen</span><span class="sxs-lookup"><span data-stu-id="5b388-117">Controls</span></span>  
 <span data-ttu-id="5b388-118">Deze sjabloon kunt Hallo volgende [pagina besturingselementen](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="5b388-118">This template may  use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="5b388-119">Basic-aanmelding</span><span class="sxs-lookup"><span data-stu-id="5b388-119">basic-signin</span></span>](api-management-page-controls.md#basic-signin)  
  
-   [<span data-ttu-id="5b388-120">providers</span><span class="sxs-lookup"><span data-stu-id="5b388-120">providers</span></span>](api-management-page-controls.md#providers)  
  
### <a name="data-model"></a><span data-ttu-id="5b388-121">Gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="5b388-121">Data model</span></span>  
 <span data-ttu-id="5b388-122">[Gebruiker aanmelden](api-management-template-data-model-reference.md#UseSignIn) entiteit.</span><span class="sxs-lookup"><span data-stu-id="5b388-122">[User sign in](api-management-template-data-model-reference.md#UseSignIn) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="5b388-123">Voorbeeldgegevens voor sjabloon</span><span class="sxs-lookup"><span data-stu-id="5b388-123">Sample template data</span></span>  
  
```json  
{  
    "Email": null,  
    "Password": null,  
    "ReturnUrl": null,  
    "RememberMe": false,  
    "RegistrationEnabled": true,  
    "DelegationEnabled": false,  
    "DelegationUrl": null,  
    "SsoSignUpUrl": null,  
    "AuxServiceUrl": "https://manage.windowsazure.com/#Workspaces/ApiManagementExtension/service/contoso5/dashboard",  
    "Providers": [  
        {  
            "Properties": {  
                "AuthenticationType": "Aad",  
                "Caption": "Azure Active Directory"  
            },  
            "AuthenticationType": "Aad",  
            "Caption": "Azure Active Directory"  
        }  
    ],  
    "UserRegistrationTerms": null,  
    "UserRegistrationTermsEnabled": false  
}  
```  
  
##  <span data-ttu-id="5b388-124"><a name="SignUp"></a>Aanmelden</span><span class="sxs-lookup"><span data-stu-id="5b388-124"><a name="SignUp"></a> Sign up</span></span>  
 <span data-ttu-id="5b388-125">Hallo **aanmelden** sjabloon kunt u registratiepagina toocustomize Hallo in Hallo-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="5b388-125">hello **sign up** template allows you toocustomize hello sign up page in hello developer portal.</span></span>  
  
 <span data-ttu-id="5b388-126">![Aanmeldingspagina](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "APIM aanmelden pagina Developer Portal-sjablonen")</span><span class="sxs-lookup"><span data-stu-id="5b388-126">![Sign Up Page](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "APIM Sign Up Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="5b388-127">Standaardsjabloon</span><span class="sxs-lookup"><span data-stu-id="5b388-127">Default template</span></span>  
  
```xml  
<h2 class="text-center">{% localized "SignupStrings|PageTitleSignup" %}</h2>  
<p class="text-center">  
  {% localized "SignupStrings|WebAuthenticationAlreadyAMember" %} <a href="/signin">{% localized "SignupStrings|WebAuthenticationSigninNow" %}</a>  
</p>  
  
<div class="row center-block ap-idp-container">  
  <div class="col-md-6">  
    <p>{% localized "SignupStrings|WebAuthenticationCreateNewAccount" %}</p>  
    <sign-up></sign-up>  
  </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="5b388-128">Besturingselementen</span><span class="sxs-lookup"><span data-stu-id="5b388-128">Controls</span></span>  
 <span data-ttu-id="5b388-129">Deze sjabloon kunt Hallo volgende [pagina besturingselementen](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="5b388-129">This template may  use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="5b388-130">aanmelden</span><span class="sxs-lookup"><span data-stu-id="5b388-130">sign-up</span></span>](api-management-page-controls.md#sign-up)  
  
### <a name="data-model"></a><span data-ttu-id="5b388-131">Gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="5b388-131">Data model</span></span>  
 <span data-ttu-id="5b388-132">[Gebruiker aanmelden](api-management-template-data-model-reference.md#UserSignUp) entiteit.</span><span class="sxs-lookup"><span data-stu-id="5b388-132">[User sign up](api-management-template-data-model-reference.md#UserSignUp) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="5b388-133">Voorbeeldgegevens voor sjabloon</span><span class="sxs-lookup"><span data-stu-id="5b388-133">Sample template data</span></span>  
  
```json  
{  
    "PasswordConfirm": null,  
    "Password": null,  
    "PasswordVerdictLevel": 0,  
    "UserRegistrationTerms": null,  
    "UserRegistrationTermsOptions": 0,  
    "ConsentAccepted": false,  
    "Email": null,  
    "FirstName": null,  
    "LastName": null,  
    "UserData": null,  
    "NameIdentifier": null,  
    "ProviderName": null  
}  
```  
  
##  <span data-ttu-id="5b388-134"><a name="PageNotFound"></a>Pagina is niet gevonden</span><span class="sxs-lookup"><span data-stu-id="5b388-134"><a name="PageNotFound"></a> Page not found</span></span>  
 <span data-ttu-id="5b388-135">Hallo **pagina niet gevonden** sjabloon kunt u toocustomize Hallo pagina pagina niet gevonden in Hallo-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="5b388-135">hello **page not found** template allows you toocustomize hello page not found page in hello developer portal.</span></span>  
  
 <span data-ttu-id="5b388-136">![Niet gevonden pagina](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "APIM niet gevonden pagina Developer Portal-sjablonen")</span><span class="sxs-lookup"><span data-stu-id="5b388-136">![Not Found Page](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "APIM Not Found Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="5b388-137">Standaardsjabloon</span><span class="sxs-lookup"><span data-stu-id="5b388-137">Default template</span></span>  
  
```xml  
<h2>{% localized "NotFoundStrings|PageTitleNotFound" %}</h2>  
  
<h3>{% localized "NotFoundStrings|TitlePotentialCause" %}</h3>  
<ul>  
  <li>{% localized "NotFoundStrings|TextblockPotentialCauseOldLink" %}</li>  
  <li>{% localized "NotFoundStrings|TextblockPotentialCauseMisspelledUrl" %}</li>  
</ul>  
  
<h3>{% localized "NotFoundStrings|TitlePotentialSolution" %}</h3>  
<ul>  
  <li>{% localized "NotFoundStrings|TextblockPotentialSolutionRetype" %}</li>  
  <li>  
    {% capture textPotentialSolutionStartOver %}{% localized "NotFoundStrings|TextblockPotentialSolutionStartOver" %}{% endcapture %}  
    {% capture homeLink %}<a href="/">{% localized "NotFoundStrings|LinkLabelHomePage" %}</a>{% endcapture %}  
    {% assign replaceString = '{0}' %}  
  
    {{ textPotentialSolutionStartOver | replace : replaceString, homeLink }}  
  </li>  
</ul>  
  
<p>  
  {% capture textReportProblem %}{% localized "NotFoundStrings|TextReportProblem" %}{% endcapture %}  
  {% capture emailLink %}<a href="mailto:apimgmt@microsoft.com" target="_self" title="API Management Support">{% localized "NotFoundStrings|LinkLabelSendUsEmail" %}</a>{% endcapture %}  
  {% assign replaceString = '{0}' %}  
  
  {{ textReportProblem | replace : replaceString, emailLink }}  
</p>  
```  
  
### <a name="controls"></a><span data-ttu-id="5b388-138">Besturingselementen</span><span class="sxs-lookup"><span data-stu-id="5b388-138">Controls</span></span>  
 <span data-ttu-id="5b388-139">Deze sjabloon kan geen gebruik [pagina besturingselementen](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="5b388-139">This template may  not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="5b388-140">Gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="5b388-140">Data model</span></span>  
  
|<span data-ttu-id="5b388-141">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="5b388-141">Property</span></span>|<span data-ttu-id="5b388-142">Type</span><span class="sxs-lookup"><span data-stu-id="5b388-142">Type</span></span>|<span data-ttu-id="5b388-143">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5b388-143">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="5b388-144">referenceCode</span><span class="sxs-lookup"><span data-stu-id="5b388-144">referenceCode</span></span>|<span data-ttu-id="5b388-145">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="5b388-145">string</span></span>|<span data-ttu-id="5b388-146">De code gegenereerd als deze pagina wordt weergegeven als Hallo resultaat van een interne fout.</span><span class="sxs-lookup"><span data-stu-id="5b388-146">Code generated if this page was displayed as hello result of an internal error.</span></span>|  
|<span data-ttu-id="5b388-147">Foutcode</span><span class="sxs-lookup"><span data-stu-id="5b388-147">errorCode</span></span>|<span data-ttu-id="5b388-148">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="5b388-148">string</span></span>|<span data-ttu-id="5b388-149">De code gegenereerd als deze pagina wordt weergegeven als Hallo resultaat van een interne fout.</span><span class="sxs-lookup"><span data-stu-id="5b388-149">Code generated if this page was displayed as hello result of an internal error.</span></span>|  
|<span data-ttu-id="5b388-150">emailBody</span><span class="sxs-lookup"><span data-stu-id="5b388-150">emailBody</span></span>|<span data-ttu-id="5b388-151">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="5b388-151">string</span></span>|<span data-ttu-id="5b388-152">Tekst gegenereerd als deze pagina wordt weergegeven als resultaat van een interne fout Hallo van e-mail.</span><span class="sxs-lookup"><span data-stu-id="5b388-152">Email body generated if this page was displayed as hello result of an internal error.</span></span>|  
|<span data-ttu-id="5b388-153">requestedUrl</span><span class="sxs-lookup"><span data-stu-id="5b388-153">requestedUrl</span></span>|<span data-ttu-id="5b388-154">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="5b388-154">string</span></span>|<span data-ttu-id="5b388-155">Hallo URL aangevraagd wanneer Hallo pagina is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="5b388-155">hello URL requested when hello page was not found.</span></span>|  
|<span data-ttu-id="5b388-156">referrerUrl</span><span class="sxs-lookup"><span data-stu-id="5b388-156">referrerUrl</span></span>|<span data-ttu-id="5b388-157">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="5b388-157">string</span></span>|<span data-ttu-id="5b388-158">Hallo verwijzende URL toohello aangevraagde URL.</span><span class="sxs-lookup"><span data-stu-id="5b388-158">hello referrer URL toohello requested URL.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="5b388-159">Voorbeeldgegevens voor sjabloon</span><span class="sxs-lookup"><span data-stu-id="5b388-159">Sample template data</span></span>  
  
```json  
{  
    "referenceCode": null,  
    "errorCode": null,  
    "emailBody": null,  
    "requestedUrl": "https://contoso5.portal.azure-api.net:443/NotFoundPage?startEditTemplate=NotFoundPage",  
    "referrerUrl": "https://contoso5.portal.azure-api.net/signup?startEditTemplate=SignUpTemplate"  
}  
```

## <a name="next-steps"></a><span data-ttu-id="5b388-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5b388-160">Next steps</span></span>
<span data-ttu-id="5b388-161">Zie voor meer informatie over het werken met sjablonen [hoe toocustomize API Management-portal voor ontwikkelaars met behulp van sjablonen Hallo](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5b388-161">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
