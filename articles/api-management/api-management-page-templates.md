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
# <a name="page-templates-in-azure-api-management"></a>Sjablonen in Azure API Management
Azure API Management biedt dat u Hallo mogelijkheid toocustomize Hallo inhoud van developer portal-pagina's met behulp van een set van sjablonen die hun inhoud configureren. Met behulp van [DotLiquid](http://dotliquidmarkup.org/) syntaxis en het Hallo-editor naar keuze, zoals [DotLiquid voor ontwerpers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), en een opgegeven set gelokaliseerde [resources String](api-management-template-resources.md#strings), [ De glyph-resources](api-management-template-resources.md#glyphs), en [pagina besturingselementen](api-management-page-controls.md), hebt u aanzienlijke flexibiliteit tooconfigure Hallo inhoud van het Hallo-pagina's naar wens met behulp van deze sjablonen.  
  
 Hallo-sjablonen in deze sectie kunt u toocustomize Hallo inhoud van het Hallo-aanmelding in de aanmelding van en pagina's pagina niet vinden in Hallo-portal voor ontwikkelaars.  
  
-   [Aanmelden](#SignIn)  
  
-   [Aanmelden](#SignUp)  
  
-   [Pagina is niet gevonden](#PageNotFound)  
  
> [!NOTE]
>  Standaard-voorbeeldsjablonen zijn opgenomen in de volgende documentatie Hallo, maar onderwerp toochange vanwege toocontinuous verbeteringen zijn. U kunt Hallo live standaardsjablonen in Hallo developer-portal door te navigeren toohello gewenst afzonderlijke sjablonen weergeven. Zie voor meer informatie over het werken met sjablonen [hoe toocustomize API Management-portal voor ontwikkelaars met behulp van sjablonen Hallo](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
##  <a name="SignIn"></a>Aanmelden  
 Hallo **aanmelden** sjabloon kunt u toocustomize Hallo aanmelding op de pagina in het Hallo-portal voor ontwikkelaars.  
  
 ![Meld u aan de pagina](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "APIM aanmelden pagina Developer Portal-sjablonen")  
  
### <a name="default-template"></a>Standaardsjabloon  
  
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
  
### <a name="controls"></a>Besturingselementen  
 Deze sjabloon kunt Hallo volgende [pagina besturingselementen](api-management-page-controls.md).  
  
-   [Basic-aanmelding](api-management-page-controls.md#basic-signin)  
  
-   [providers](api-management-page-controls.md#providers)  
  
### <a name="data-model"></a>Gegevensmodel  
 [Gebruiker aanmelden](api-management-template-data-model-reference.md#UseSignIn) entiteit.  
  
### <a name="sample-template-data"></a>Voorbeeldgegevens voor sjabloon  
  
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
  
##  <a name="SignUp"></a>Aanmelden  
 Hallo **aanmelden** sjabloon kunt u registratiepagina toocustomize Hallo in Hallo-portal voor ontwikkelaars.  
  
 ![Aanmeldingspagina](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "APIM aanmelden pagina Developer Portal-sjablonen")  
  
### <a name="default-template"></a>Standaardsjabloon  
  
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
  
### <a name="controls"></a>Besturingselementen  
 Deze sjabloon kunt Hallo volgende [pagina besturingselementen](api-management-page-controls.md).  
  
-   [aanmelden](api-management-page-controls.md#sign-up)  
  
### <a name="data-model"></a>Gegevensmodel  
 [Gebruiker aanmelden](api-management-template-data-model-reference.md#UserSignUp) entiteit.  
  
### <a name="sample-template-data"></a>Voorbeeldgegevens voor sjabloon  
  
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
  
##  <a name="PageNotFound"></a>Pagina is niet gevonden  
 Hallo **pagina niet gevonden** sjabloon kunt u toocustomize Hallo pagina pagina niet gevonden in Hallo-portal voor ontwikkelaars.  
  
 ![Niet gevonden pagina](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "APIM niet gevonden pagina Developer Portal-sjablonen")  
  
### <a name="default-template"></a>Standaardsjabloon  
  
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
  
### <a name="controls"></a>Besturingselementen  
 Deze sjabloon kan geen gebruik [pagina besturingselementen](api-management-page-controls.md).  
  
### <a name="data-model"></a>Gegevensmodel  
  
|Eigenschap|Type|Beschrijving|  
|--------------|----------|-----------------|  
|referenceCode|Tekenreeks|De code gegenereerd als deze pagina wordt weergegeven als Hallo resultaat van een interne fout.|  
|Foutcode|Tekenreeks|De code gegenereerd als deze pagina wordt weergegeven als Hallo resultaat van een interne fout.|  
|emailBody|Tekenreeks|Tekst gegenereerd als deze pagina wordt weergegeven als resultaat van een interne fout Hallo van e-mail.|  
|requestedUrl|Tekenreeks|Hallo URL aangevraagd wanneer Hallo pagina is niet gevonden.|  
|referrerUrl|Tekenreeks|Hallo verwijzende URL toohello aangevraagde URL.|  
  
### <a name="sample-template-data"></a>Voorbeeldgegevens voor sjabloon  
  
```json  
{  
    "referenceCode": null,  
    "errorCode": null,  
    "emailBody": null,  
    "requestedUrl": "https://contoso5.portal.azure-api.net:443/NotFoundPage?startEditTemplate=NotFoundPage",  
    "referrerUrl": "https://contoso5.portal.azure-api.net/signup?startEditTemplate=SignUpTemplate"  
}  
```

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over het werken met sjablonen [hoe toocustomize API Management-portal voor ontwikkelaars met behulp van sjablonen Hallo](api-management-developer-portal-templates.md).
