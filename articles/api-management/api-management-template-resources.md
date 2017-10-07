---
title: API Management-sjabloonresources aaaAzure | Microsoft Docs
description: Meer informatie over Hallo typen resources beschikbaar voor gebruik in developer portal sjablonen in Azure API Management.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 51a1b4c6-a9fd-4524-9e0e-03a9800c3e94
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2221e3852986d485d13817b483e473dfe451d3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-template-resources"></a>Azure API Management-sjabloonresources
Azure API Management biedt de volgende typen resources voor gebruik in Hallo developer portal sjablonen Hallo.  
  
-   [Tekenreeksbronnen](#strings)  
  
-   [De glyph-resources](#glyphs)  
  
##  <a name="strings"></a>Tekenreeksbronnen  
 API Management biedt een uitgebreide reeks tekenreeksresources voor gebruik in Hallo-portal voor ontwikkelaars. Deze resources worden vertaald in alle Hallo talen wordt ondersteund door de API Management. Hallo standaardset sjablonen maakt gebruik van deze resources voor paginakopteksten, labels en de constante tekenreeksen die worden weergegeven in het Hallo-portal voor ontwikkelaars. toouse een string-bron in uw sjablonen bieden Hallo resource tekenreeks voorvoegsel gevolgd door de naam van de tekenreeks hello, zoals weergegeven in het volgende voorbeeld Hallo.  
  
```  
{% localized "Prefix|Name" %}  
  
```  
  
 Hallo volgende voorbeeld is van Hallo Product lijstsjabloon en geeft weer **producten** bovenaan Hallo Hallo pagina.  
  
```  
<h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>  
  
```  
  
 Raadpleeg toohello tabellen voor Hallo tekenreeksbronnen beschikbaar voor gebruik in uw developer portal sjablonen te volgen. Hallo-tabelnaam gebruiken als voorvoegsel Hallo Hallo tekenreeksbronnen in de tabel.  
  
-   [ApisStrings](#ApisStrings)  
  
-   [ApplicationListStrings](#ApplicationListStrings)  
  
-   [AppDetailsStrings](#AppDetailsStrings)  
  
-   [AppStrings](#AppStrings)  
  
-   [CommonResources](#CommonResources)  
  
-   [CommonStrings](#CommonStrings)  
  
-   [Documentatie](#Documentation)  
  
-   [ErrorPageStrings](#ErrorPageStrings)  
  
-   [IssuesStrings](#IssuesStrings)  
  
-   [NotFoundStrings](#NotFoundStrings)  
  
-   [ProductDetailsStrings](#ProductDetailsStrings)  
  
-   [ProductsStrings](#ProductsStrings)  
  
-   [ProviderInfoStrings](#ProviderInfoStrings)  
  
-   [SigninResources](#SigninResources)  
  
-   [SigninStrings](#SigninStrings)  
  
-   [SignupStrings](#SignupStrings)  
  
-   [SubscriptionListStrings](#SubscriptionListStrings)  
  
-   [SubscriptionStrings](#SubscriptionStrings)  
  
-   [UpdateProfileStrings](#UpdateProfileStrings)  
  
-   [Gebruikersprofiel](#UserProfile)  
  
###  <a name="ApisStrings"></a>ApisStrings  
  
|Naam|Tekst|  
|----------|----------|  
|PageTitleApis|API's|  
  
###  <a name="AppDetailsStrings"></a>AppDetailsStrings  
  
|Naam|Tekst|  
|----------|----------|  
|WebApplicationsDetailsTitle|Voorbeeld van de toepassing|  
|WebApplicationsRequirementsHeader|Vereisten|  
|WebApplicationsScreenshotAlt|schermopname|  
|WebApplicationsScreenshotsHeader|Schermafbeeldingen|  
  
###  <a name="ApplicationListStrings"></a>ApplicationListStrings  
  
|Naam|Tekst|  
|----------|----------|  
|WebDevelopersAppDeleteConfirmation|Weet u zeker dat u wilt dat tooremove toepassing?|  
|WebDevelopersAppNotPublished|Niet gepubliceerd|  
|WebDevelopersAppNotSubminted|Niet verzonden|  
|WebDevelopersAppTableCategoryHeader|Category|  
|WebDevelopersAppTableNameHeader|Naam|  
|WebDevelopersAppTableStateHeader|Status|  
|WebDevelopersEditLink|Bewerken|  
|WebDevelopersRegisterAppLink|Toepassing registreren|  
|WebDevelopersRemoveLink|Verwijderen|  
|WebDevelopersSubmitLink|Verzenden|  
|WebDevelopersYourApplicationsHeader|Uw toepassingen|  
  
###  <a name="AppStrings"></a>AppStrings  
  
|Naam|Tekst|  
|----------|----------|  
|WebApplicationsHeader|Toepassingen|  
  
###  <a name="CommonResources"></a>CommonResources  
  
|Naam|Tekst|  
|----------|----------|  
|NoItemsToDisplay|Er zijn geen resultaten gevonden.|  
|GeneralExceptionMessage|Er is niet juist. Het is mogelijk een tijdelijke fout of een fout. Probeer het opnieuw.|  
|GeneralJsonExceptionMessage|Er is niet juist. Het is mogelijk een tijdelijke fout of een fout. Controleer, Hallo pagina vernieuwen en probeer het opnieuw.|  
|ConfirmationMessageUnsavedChanges|Er zijn enkele niet-opgeslagen wijzigingen. Weet u zeker dat u wilt toocancel en Hallo wijzigingen negeren?|  
|AzureActiveDirectory|Azure Active Directory|  
|HttpLargeRequestMessage|HTTP-aanvraagtekst te groot.|  
  
###  <a name="CommonStrings"></a>CommonStrings  
  
|Naam|Tekst|  
|----------|----------|  
|ButtonLabelCancel|Annuleren|  
|ButtonLabelSave|Opslaan|  
|GeneralExceptionMessage|Er is niet juist. Het is mogelijk een tijdelijke fout of een fout. Probeer het opnieuw.|  
|NoItemsToDisplay|Er zijn geen items toodisplay.|  
|PagerButtonLabelFirst|Eerste|  
|PagerButtonLabelLast|laatste|  
|PagerButtonLabelNext|Volgende|  
|PagerButtonLabelPrevious|Vorig|  
|PagerLabelPageNOfM|Pagina {0} van {1}|  
|PasswordTooShort|Hallo wachtwoord is te kort|  
|EmailAsPassword|Gebruik uw e-mailadres niet als uw wachtwoord|  
|PasswordSameAsUserName|Uw wachtwoord mag niet uw gebruikersnaam bevatten.|  
|PasswordTwoCharacterClasses|Klassen voor verschillende tekensets gebruiken|  
|PasswordTooManyRepetitions|Te veel herhalingen|  
|PasswordSequenceFound|Uw wachtwoord bevat reeksen|  
|PagerLabelPageSize|Paginagrootte|  
|CurtainLabelLoading|Laden...|  
|TablePlaceholderNothingToDisplay|Er zijn geen gegevens voor geselecteerde Hallo periode en bereik|  
|ButtonLabelClose|Sluiten|  
  
###  <a name="Documentation"></a>Documentatie  
  
|Naam|Tekst|  
|----------|----------|  
|WebDocumentationInvalidHeaderErrorMessage|Ongeldige header {0}|  
|WebDocumentationInvalidRequestErrorMessage|Ongeldige aanvraag-URL|  
|TextboxLabelAccessToken|Toegangstoken *|  
|DropdownOptionPrimaryKeyFormat|Primaire-{0}|  
|DropdownOptionSecondaryKeyFormat|Secundaire-{0}|  
|WebDocumentationSubscriptionKeyText|De abonnementssleutel van uw|  
|WebDocumentationTemplatesAddHeaders|Vereiste HTTP-headers toevoegen|  
|WebDocumentationTemplatesBasicAuthSample|Basisverificatie-voorbeeld|  
|WebDocumentationTemplatesCurlForBasicAuth|voor basisverificatie gebruik:--gebruiker {username}: {wachtwoord}|  
|WebDocumentationTemplatesCurlValuesForPath|Geef waarden op voor de padparameters (weergegeven als {...}), uw abonnementssleutel en waarden voor queryparameters|  
|WebDocumentationTemplatesDeveloperKey|De abonnementssleutel van uw opgeven|  
|WebDocumentationTemplatesJavaApache|In dit voorbeeld gebruikt Hallo Apache HTTP-client van HTTP-onderdelen (http://hc.apache.org/httpcomponents-client-ga/)|  
|WebDocumentationTemplatesOptionalParams|Waarden opgeven voor optionele parameters, indien nodig|  
|WebDocumentationTemplatesPhpPackage|Dit voorbeeld gebruikt Hallo HTTP_Request2-pakket. (voor meer informatie: http://pear.php.net/package/HTTP_Request2)|  
|WebDocumentationTemplatesPythonValuesForPath|Geef waarden voor padparameters (weergegeven als {...}) en de hoofdtekst indien nodig|  
|WebDocumentationTemplatesRequestBody|Aanvraagtekst opgeven|  
|WebDocumentationTemplatesRequiredParams|Geef waarden op voor de volgende parameters Hallo|  
|WebDocumentationTemplatesValuesForPath|Geef waarden voor padparameters (weergegeven als {...})|  
|OAuth2AuthorizationEndpointDescription|Hallo autorisatie eindpunt gebruikte toointeract met Hallo resource-eigenaar is en verkrijgen van een machtiging grant.|  
|OAuth2AuthorizationEndpointName|Autorisatie-eindpunt|  
|OAuth2TokenEndpointDescription|Hallo-tokeneindpunt wordt gebruikt door Hallo client tooobtain een toegangstoken in de vorm van de machtiging verlenen of vernieuwen van tokens.|  
|OAuth2TokenEndpointName|-Tokeneindpunt|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_Description|< p\> Hallo client initieert Hallo stroom door Hallo resource eigenaar gebruikersagent toohello autorisatie eindpunt.  Hallo-client neemt de client-id, het aangevraagde bereik, de lokale status en een omleiding URI toowhich Hallo autorisatie-server stuurt Hallo gebruikersagent terug wanneer toegang wordt verleend (of geweigerd).     < /p\> < p\> Hallo autorisatie server verifieert de resource-eigenaar hello (via Hallo gebruikersagent) en vaststelt of Hallo resource-eigenaar verleent of weigert de aanvraag voor toegang tot Hallo-client.     < /p\> < p\> ervan uitgaande dat Hallo resource-eigenaar toegang verleent, Hallo autorisatie server Hallo gebruikersagent back toohello client met behulp van Hallo omleidings-URI opgegeven doorstuurt eerdere (Hallo aanvraag of tijdens clien t registratie).  Hallo omleidings-URI bevat een autorisatiecode en geen lokale status die eerder door Hallo client geleverd.     < /p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_ErrorDescription|< p\> als Hallo gebruiker Hallo toegangsaanvraag van weigert als Hallo-aanvraag ongeldig is, Hallo client ontvangt met Hallo parameters toevoegen op toohello omleiding te volgen: < /p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_Name|Autorisatieaanvraag|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_RequestDescription|< p\> clientapp Hallo Hallo gebruiker toohello autorisatie eindpunt in volgorde tooinitiate Hallo OAuth-proces moet verzenden.          Op Hallo autorisatie eindpunt, Hallo gebruiker wordt geverifieerd en vervolgens verleent of weigert access toohello-app.     < /p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_ResponseDescription|< p\> ervan uitgaande dat Hallo resource-eigenaar toegang verleent, autorisatie server Hallo gebruikersagent back toohello client met behulp van Hallo omleidings-URI opgegeven doorstuurt eerdere (Hallo aanvraag of tijdens de clientregistratie).  Hallo omleidings-URI bevat een autorisatiecode en geen lokale status die eerder door Hallo client geleverd. < /p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_Description|< p\> Hallo client vraagt een toegangstoken van Hallo autorisatie server'' s-tokeneindpunt door Hallo autorisatiecode ontvangen in de vorige stap Hallo.  Wanneer de aanvraag hello, verifieert Hallo-client met Hallo autorisatie-server.  Hallo-client bevat een Hallo omleiding URI die wordt gebruikt tooobtain Hallo autorisatiecode voor verificatie. < /p\> < p\> Hallo autorisatie server verifieert de client hello, valideert de autorisatiecode Hallo en zorgt ervoor dat Hallo omleidings-URI komt overeen met Hallo URI gebruikte tooredirect Hallo client ontvangen in stap (C).  Als geldig is, wordt Hallo autorisatie server reageert op een toegangstoken en desgewenst een vernieuwingstoken. < /p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_ErrorDescription|< p\> als clientverificatie Hallo-aanvraag is mislukt of ongeldig is, Hallo autorisatie server reageert met de statuscode van een HTTP-fout 400 (ongeldige aanvraag) (tenzij anders opgegeven) en omvat de volgende parameters met antwoord Hallo Hallo. < /p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_RequestDescription|< p\> Hallo client doet een aanvraag toohello token eindpunt door te sturen Hallo Hallo ' application/x-1-800-www-Dell-form-urlencoded' indeling met een tekencodering van UTF-8 in Hallo HTTP-aanvraag entiteitshoofdtekst parameters te volgen. < /p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_ResponseDescription|< p\> Hallo autorisatie server geeft een access-token en optionele vernieuwen en constructies Hallo antwoord door toe te voegen Hallo parameters toohello entiteitshoofdtekst van Hallo HTTP-antwoord met een 200 (OK)-statuscode te volgen. < /p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_Description|< p\> Hallo client verifieert met Hallo autorisatie-server en aanvragen van een toegangstoken van token Hallo-eindpunt. < /p\> < p\> Hallo autorisatie server verifieert de client hello en als geldig is, geeft u een toegangstoken. < /p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_ErrorDescription|< p\> als Hallo aanvraag clientverificatie is mislukt of ongeldig is Hallo autorisatie server reageert met een HTTP-fout 400 (ongeldige aanvraag)-statuscode (tenzij anders opgegeven) en omvat de volgende parameters met antwoord Hallo Hallo. < /p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_RequestDescription|< p\> Hallo client doet een aanvraag toohello token eindpunt door toe te voegen Hallo Hallo ' application/x-1-800-www-Dell-form-urlencoded' indeling met een tekencodering van UTF-8 in Hallo HTTP-aanvraag entiteitshoofdtekst parameters te volgen. < /p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_ResponseDescription|< p\> als Hallo-aanvraag voor toegang tot token geldig en geautoriseerde is Hallo autorisatie server problemen met een access-token en optionele vernieuwen en constructies Hallo antwoord door toe te voegen Hallo volgende parameters toohello entiteitshoofdtekst van Hallo HTTP antwoord met een statuscode van 200 (OK). < /p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_Description|< p\> Hallo client initieert Hallo stroom door de resource-eigenaar Hallo '' s gebruikersagent toohello autorisatie eindpunt.  Hallo-client neemt de client-id, het aangevraagde bereik, de lokale status en een omleiding URI toowhich Hallo autorisatie-server stuurt Hallo gebruikersagent terug wanneer toegang wordt verleend (of geweigerd). < /p\> < p\> Hallo autorisatie server verifieert de resource-eigenaar hello (via Hallo gebruikersagent) en vaststelt of Hallo resource-eigenaar verleent of Hallo client weigert '' s-toegangsaanvraag. < /p\> < p\> ervan uitgaande dat Hallo resource-eigenaar toegang verleent, Hallo autorisatie server Hallo gebruikersagent back toohello client Hallo omleiding URI die eerder is verkregen met doorstuurt.  Hallo omleidings-URI bevat toegangstoken Hallo Hallo URI-fragment. < /p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_ErrorDescription|< p\> als Hallo resource-eigenaar Hallo toegangsaanvraag toe of weigert als Hallo aanvraag om redenen dan een ontbrekende of ongeldige omleiding URI mislukt, Hallo autorisatie server informeert het Hallo-client door toe te voegen Hallo volgende parameters toohello fragme NT-onderdeel van het gebruik van Hallo omleiding URI Hallo ' application/x-1-800-www-Dell-form-urlencoded' indeling. < /p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_RequestDescription|< p\> clientapp Hallo Hallo gebruiker toohello autorisatie eindpunt in volgorde tooinitiate Hallo OAuth-proces moet verzenden.      Op Hallo autorisatie eindpunt, Hallo gebruiker wordt geverifieerd en vervolgens verleent of weigert access toohello-app. < /p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_ResponseDescription|< p\> als Hallo resource-eigenaar toegangsaanvraag hello verleent, Hallo autorisatie server een toegangstoken uitgeeft en toohello client door toe te voegen Hallo parameters toohello fragmentonderdeel van Hallo omleidings-URI te volgen levert Hallo met "a pplication/x-1-800-www-Dell-form-urlencoded'-notatie. < /p\>|  
|OAuth2Flow_ObtainAuthorization_AuthorizationCodeGrant_Description|Autorisatiecodestroom is geoptimaliseerd voor clients die geschikt is voor het onderhouden van Hallo vertrouwelijkheid van hun referenties (bijvoorbeeld server webtoepassingen geïmplementeerd met behulp van PHP, Java, Python, Ruby, ASP.NET, enz.).|  
|OAuth2Flow_ObtainAuthorization_AuthorizationCodeGrant_Name|Autorisatie Code verlenen|  
|OAuth2Flow_ObtainAuthorization_ClientCredentialsGrant_Description|Clientreferentiestroom is geschikt in gevallen waarbij Hallo-client (uw toepassing) toegang tot beveiligde toohello bronnen onder het beheer is aangevraagd. Hallo-client wordt beschouwd als een resource-eigenaar, zodat geen tussenkomst van de eindgebruiker is vereist.|  
|OAuth2Flow_ObtainAuthorization_ClientCredentialsGrant_Name|Client referenties verlenen|  
|OAuth2Flow_ObtainAuthorization_ImplicitGrant_Description|Impliciete stroom is geoptimaliseerd voor clients waarvoor niet van het onderhouden van Hallo vertrouwelijkheid van hun referenties bekende toooperate een bepaalde omleidings-URI. Deze clients zijn doorgaans geïmplementeerd in een browser met gebruik van een scripttaal zoals JavaScript.|  
|OAuth2Flow_ObtainAuthorization_ImplicitGrant_Name|Impliciete verlenen|  
|OAuth2Flow_ObtainAuthorization_ResourceOwnerPasswordCredentialsGrant_Description|Resource-eigenaar wachtwoord referentiestroom is geschikt in gevallen waarbij Hallo resource-eigenaar een vertrouwensrelatie met Hallo-client (uw toepassing), zoals besturingssysteem Hallo-apparaat of een toepassing met bijzondere rechten heeft. Deze stroom is geschikt voor clients die geschikt is voor het verkrijgen van Hallo resource-eigenaar van referenties (gebruikersnaam en wachtwoord, meestal met behulp van een interactief formulier).|  
|OAuth2Flow_ObtainAuthorization_ResourceOwnerPasswordCredentialsGrant_Name|De referenties van het wachtwoord voor resource-eigenaar verlenen|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_Description|< p\> Hallo resource-eigenaar biedt Hallo-client met de gebruikersnaam en wachtwoord. < /p\> < p\> Hallo client vraagt een toegangstoken van Hallo autorisatie server'' s-tokeneindpunt door Hallo referenties ontvangen van Hallo resource-eigenaar.  Wanneer de aanvraag hello, verifieert Hallo-client met Hallo autorisatie-server. < /p\> < p\> Hallo autorisatie server verifieert de client Hallo Hallo eigenaar bronreferenties valideert en als geldig is, geeft u een toegangstoken. < /p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_ErrorDescription|< p\> als Hallo aanvraag clientverificatie is mislukt of ongeldig is Hallo autorisatie server reageert met een HTTP-fout 400 (ongeldige aanvraag)-statuscode (tenzij anders opgegeven) en omvat de volgende parameters met antwoord Hallo Hallo. < /p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_RequestDescription|< p\> Hallo client doet een aanvraag toohello token eindpunt door toe te voegen Hallo Hallo ' application/x-1-800-www-Dell-form-urlencoded' indeling met een tekencodering van UTF-8 in Hallo HTTP-aanvraag entiteitshoofdtekst parameters te volgen. < /p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_ResponseDescription|< p\> als Hallo-aanvraag voor toegang tot token geldig en geautoriseerde is Hallo autorisatie server problemen met een access-token en optionele vernieuwen en constructies Hallo antwoord door toe te voegen Hallo parameters toohello entiteitshoofdtekst van Hallo HTTP respo na nse met een statuscode van 200 (OK). < /p\>|  
|OAuth2Step_AccessTokenRequest_Name|De tokenaanvraag toegang|  
|OAuth2Step_AuthorizationRequest_Name|Autorisatieaanvraag|  
|OAuth2AccessToken_AuthorizationCodeGrant_TokenResponse|VEREIST. Hallo-toegangstoken is uitgegeven door Hallo autorisatie-server.|  
|OAuth2AccessToken_ClientCredentialsGrant_TokenResponse|VEREIST. Hallo-toegangstoken is uitgegeven door Hallo autorisatie-server.|  
|OAuth2AccessToken_ImplicitGrant_AuthorizationResponse|VEREIST. Hallo-toegangstoken is uitgegeven door Hallo autorisatie-server.|  
|OAuth2AccessToken_ResourceOwnerPasswordCredentialsGrant_TokenResponse|VEREIST. Hallo-toegangstoken is uitgegeven door Hallo autorisatie-server.|  
|OAuth2ClientId_AuthorizationCodeGrant_AuthorizationRequest|VEREIST. Client-id.|  
|OAuth2ClientId_AuthorizationCodeGrant_TokenRequest|VEREIST als Hallo-client niet met Hallo autorisatie-server verifieert.|  
|OAuth2ClientId_ImplicitGrant_AuthorizationRequest|VEREIST. Hallo van client-id.|  
|OAuth2Code_AuthorizationCodeGrant_AuthorizationResponse|VEREIST. Hallo autorisatie-code is gegenereerd door Hallo autorisatie-server.|  
|OAuth2Code_AuthorizationCodeGrant_TokenRequest|VEREIST. Hallo autorisatiecode van Hallo autorisatie server ontvangen.|  
|OAuth2ErrorDescription_AuthorizationCodeGrant_AuthorizationErrorResponse|OPTIONEEL. Leesbare ASCII-tekst bieden aanvullende informatie.|  
|OAuth2ErrorDescription_AuthorizationCodeGrant_TokenErrorResponse|OPTIONEEL. Leesbare ASCII-tekst bieden aanvullende informatie.|  
|OAuth2ErrorDescription_ClientCredentialsGrant_TokenErrorResponse|OPTIONEEL. Leesbare ASCII-tekst bieden aanvullende informatie.|  
|OAuth2ErrorDescription_ImplicitGrant_AuthorizationErrorResponse|OPTIONEEL. Leesbare ASCII-tekst bieden aanvullende informatie.|  
|OAuth2ErrorDescription_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|OPTIONEEL. Leesbare ASCII-tekst bieden aanvullende informatie.|  
|OAuth2ErrorUri_AuthorizationCodeGrant_AuthorizationErrorResponse|OPTIONEEL. Een URI die een leesbare webpagina met informatie over de fout Hallo identificeren.|  
|OAuth2ErrorUri_AuthorizationCodeGrant_TokenErrorResponse|OPTIONEEL. Een URI die een leesbare webpagina met informatie over de fout Hallo identificeren.|  
|OAuth2ErrorUri_ClientCredentialsGrant_TokenErrorResponse|OPTIONEEL. Een URI die een leesbare webpagina met informatie over de fout Hallo identificeren.|  
|OAuth2ErrorUri_ImplicitGrant_AuthorizationErrorResponse|OPTIONEEL. Een URI die een leesbare webpagina met informatie over de fout Hallo identificeren.|  
|OAuth2ErrorUri_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|OPTIONEEL. Een URI die een leesbare webpagina met informatie over de fout Hallo identificeren.|  
|OAuth2Error_AuthorizationCodeGrant_AuthorizationErrorResponse|VEREIST. Een enkele ASCII-foutcode wordt gegeven van de volgende Hallo: invalid_request, unauthorized_client, access_denied, unsupported_response_type, invalid_scope, server_error, temporarily_unavailable.|  
|OAuth2Error_AuthorizationCodeGrant_TokenErrorResponse|VEREIST. Een enkele ASCII-foutcode wordt gegeven van de volgende Hallo: invalid_request, invalid_client, invalid_grant, unauthorized_client, unsupported_grant_type, invalid_scope.|  
|OAuth2Error_ClientCredentialsGrant_TokenErrorResponse|VEREIST. Een enkele ASCII-foutcode wordt gegeven van de volgende Hallo: invalid_request, invalid_client, invalid_grant, unauthorized_client, unsupported_grant_type, invalid_scope.|  
|OAuth2Error_ImplicitGrant_AuthorizationErrorResponse|VEREIST. Een enkele ASCII-foutcode wordt gegeven van de volgende Hallo: invalid_request, unauthorized_client, access_denied, unsupported_response_type, invalid_scope, server_error, temporarily_unavailable.|  
|OAuth2Error_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|VEREIST. Een enkele ASCII-foutcode wordt gegeven van de volgende Hallo: invalid_request, invalid_client, invalid_grant, unauthorized_client, unsupported_grant_type, invalid_scope.|  
|OAuth2ExpiresIn_AuthorizationCodeGrant_TokenResponse|AANBEVOLEN. Hallo levensduur in seconden van Hallo-toegangstoken.|  
|OAuth2ExpiresIn_ClientCredentialsGrant_TokenResponse|AANBEVOLEN. Hallo levensduur in seconden van Hallo-toegangstoken.|  
|OAuth2ExpiresIn_ImplicitGrant_AuthorizationResponse|AANBEVOLEN. Hallo levensduur in seconden van Hallo-toegangstoken.|  
|OAuth2ExpiresIn_ResourceOwnerPasswordCredentialsGrant_TokenResponse|AANBEVOLEN. Hallo levensduur in seconden van Hallo-toegangstoken.|  
|OAuth2GrantType_AuthorizationCodeGrant_TokenRequest|VEREIST. Waarde moet worden ingesteld te 'authorization_code'.|  
|OAuth2GrantType_ClientCredentialsGrant_TokenRequest|VEREIST. Waarde moet worden ingesteld te 'client_credentials'.|  
|OAuth2GrantType_ResourceOwnerPasswordCredentialsGrant_TokenRequest|VEREIST. Waarde moet worden ingesteld te 'password'.|  
|OAuth2Password_ResourceOwnerPasswordCredentialsGrant_TokenRequest|VEREIST. Hallo resource eigenaarswachtwoord.|  
|OAuth2RedirectUri_AuthorizationCodeGrant_AuthorizationRequest|OPTIONEEL. Hallo omleiding eindpunt URI moet een absolute URI zijn.|  
|OAuth2RedirectUri_AuthorizationCodeGrant_TokenRequest|VEREIST als de parameter 'redirect_uri' Hallo is opgenomen in Hallo autorisatieaanvraag en hun waarden identiek zijn.|  
|OAuth2RedirectUri_ImplicitGrant_AuthorizationRequest|OPTIONEEL. Hallo omleiding eindpunt URI moet een absolute URI zijn.|  
|OAuth2RefreshToken_AuthorizationCodeGrant_TokenResponse|OPTIONEEL. Hallo vernieuwingstoken, dat gebruikt tooobtain nieuwe toegangstokens worden kan.|  
|OAuth2RefreshToken_ClientCredentialsGrant_TokenResponse|OPTIONEEL. Hallo vernieuwingstoken, dat gebruikt tooobtain nieuwe toegangstokens worden kan.|  
|OAuth2RefreshToken_ResourceOwnerPasswordCredentialsGrant_TokenResponse|OPTIONEEL. Hallo vernieuwingstoken, dat gebruikt tooobtain nieuwe toegangstokens worden kan.|  
|OAuth2ResponseType_AuthorizationCodeGrant_AuthorizationRequest|VEREIST. Waarde moet worden ingesteld te 'code'.|  
|OAuth2ResponseType_ImplicitGrant_AuthorizationRequest|VEREIST. Waarde moet worden ingesteld als te 'token'.|  
|OAuth2Scope_AuthorizationCodeGrant_AuthorizationRequest|OPTIONEEL. Hallo-bereik van Hallo-toegangsaanvraag.|  
|OAuth2Scope_AuthorizationCodeGrant_TokenResponse|OPTIONEEL als identieke toohello bereik aangevraagd door de client Hallo; anders is vereist.|  
|OAuth2Scope_ClientCredentialsGrant_TokenRequest|OPTIONEEL. Hallo-bereik van Hallo-toegangsaanvraag.|  
|OAuth2Scope_ClientCredentialsGrant_TokenResponse|OPTIONEEL, indien identieke toohello bereik aangevraagd door de client Hallo; anders is vereist.|  
|OAuth2Scope_ImplicitGrant_AuthorizationRequest|OPTIONEEL. Hallo-bereik van Hallo-toegangsaanvraag.|  
|OAuth2Scope_ImplicitGrant_AuthorizationResponse|OPTIONEEL als identieke toohello bereik aangevraagd door de client Hallo; anders is vereist.|  
|OAuth2Scope_ResourceOwnerPasswordCredentialsGrant_TokenRequest|OPTIONEEL. Hallo-bereik van Hallo-toegangsaanvraag.|  
|OAuth2Scope_ResourceOwnerPasswordCredentialsGrant_TokenResponse|OPTIONEEL, indien identieke toohello bereik aangevraagd door de client Hallo; anders is vereist.|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationErrorResponse|Als de parameter 'state' hello aanwezig in de clientaanvraag autorisatie Hallo is vereist.  Hallo exacte waarde van Hallo client ontvangen.|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationRequest|AANBEVOLEN. Een ondoorzichtige waarde die wordt gebruikt door de status van de toomaintain tussen Hallo-aanvraag en callback Hallo.  Hallo autorisatie server omvat deze waarde wanneer Hallo gebruikersagent back toohello client omleiden.  Hallo-parameter moet worden gebruikt voor het voorkomen van aanvraagvervalsing op meerdere sites.|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationResponse|Als de parameter 'state' hello aanwezig in de clientaanvraag autorisatie Hallo is vereist.  Hallo exacte waarde van Hallo client ontvangen.|  
|OAuth2State_ImplicitGrant_AuthorizationErrorResponse|Als de parameter 'state' hello aanwezig in de clientaanvraag autorisatie Hallo is vereist.  Hallo exacte waarde van Hallo client ontvangen.|  
|OAuth2State_ImplicitGrant_AuthorizationRequest|AANBEVOLEN. Een ondoorzichtige waarde die wordt gebruikt door de status van de toomaintain tussen Hallo-aanvraag en callback Hallo.  Hallo autorisatie server omvat deze waarde wanneer Hallo gebruikersagent back toohello client omleiden.  Hallo-parameter moet worden gebruikt voor het voorkomen van aanvraagvervalsing op meerdere sites.|  
|OAuth2State_ImplicitGrant_AuthorizationResponse|Als de parameter 'state' hello aanwezig in de clientaanvraag autorisatie Hallo is vereist.  Hallo exacte waarde van Hallo client ontvangen.|  
|OAuth2TokenType_AuthorizationCodeGrant_TokenResponse|VEREIST. Hallo type Hallo token dat is uitgegeven.|  
|OAuth2TokenType_ClientCredentialsGrant_TokenResponse|VEREIST. Hallo type Hallo token dat is uitgegeven.|  
|OAuth2TokenType_ImplicitGrant_AuthorizationResponse|VEREIST. Hallo type Hallo token dat is uitgegeven.|  
|OAuth2TokenType_ResourceOwnerPasswordCredentialsGrant_TokenResponse|VEREIST. Hallo type Hallo token dat is uitgegeven.|  
|OAuth2UserName_ResourceOwnerPasswordCredentialsGrant_TokenRequest|VEREIST. Hallo resource eigenaar gebruikersnaam.|  
|OAuth2UnsupportedTokenType|Type token {0}' is geen supporetd.|  
|OAuth2InvalidState|Ongeldige reactie van de autorisatie-server|  
|OAuth2GrantType_AuthorizationCode|Autorisatiecode|  
|OAuth2GrantType_Implicit|Impliciete|  
|OAuth2GrantType_ClientCredentials|Clientreferenties|  
|OAuth2GrantType_ResourceOwnerPassword|Wachtwoord voor resource-eigenaar|  
|WebDocumentation302Code|302 gevonden|  
|WebDocumentation400Code|400 (ongeldige aanvraag)|  
|OAuth2SendingMethod_AuthHeader|Autorisatie-header|  
|OAuth2SendingMethod_QueryParam|Query-parameter|  
|OAuth2AuthorizationServerGeneralException|Er is een fout opgetreden bij het verlenen van toegang via {0}|  
|OAuth2AuthorizationServerCommunicationException|Een HTTP-verbinding tooauthorization-server kan niet worden gemaakt of het onverwacht is gesloten.|  
|WebDocumentationOAuth2GeneralErrorMessage|Er is een onverwachte fout opgetreden.|  
|AuthorizationServerCommunicationException|Autorisatie server communicatie uitzondering is opgetreden. Neem contact op met de beheerder.|  
|TextblockSubscriptionKeyHeaderDescription|Abonnementssleutel waarmee toegang toothis API. Gevonden in de < een href ='/ developer'\>profiel < /a\>.|  
|TextblockOAuthHeaderDescription|OAuth 2.0-toegangstoken is verkregen van < ik\>{0} < /i\>. Ondersteunde typen grant: < i\>{1} < /i\>.|  
|TextblockContentTypeHeaderDescription|Mediatype van Hallo hoofdtekst toohello API verzonden.|  
|ErrorMessageApiNotAccessible|Hallo API die u probeert toocall is op dit moment niet toegankelijk. Neem contact op met de Hallo API publisher < een href = "/ problemen"\>hier < /a\>.|  
|ErrorMessageApiTimedout|Hallo API die u probeert toocall duurt langer dan normaal tooget antwoord terug. Neem contact op met de Hallo API publisher < een href = "/ problemen"\>hier < /a\>.|  
|BadRequestParameterExpected|'parameter '{0}' wordt verwacht'|  
|TooltipTextDoubleClickToSelectAll|Dubbelklik in alle tooselect.|  
|TooltipTextHideRevealSecret|Weergeven/verbergen|  
|ButtonLinkOpenConsole|Probeer het nu|  
|SectionHeadingRequestBody|Aanvraagtekst|  
|SectionHeadingRequestParameters|Parameters van de aanvraag|  
|SectionHeadingRequestUrl|Aanvraag-URL|  
|SectionHeadingResponse|Antwoord|  
|SectionHeadingRequestHeaders|Aanvraagheaders|  
|FormLabelSubtextOptional|Optioneel|  
|SectionHeadingCodeSamples|Codevoorbeelden|  
|TextblockOpenidConnectHeaderDescription|OpenID Connect-id-token verkregen via < ik\>{0} < /i\>. Ondersteunde typen grant: < i\>{1} < /i\>.|  
  
###  <a name="ErrorPageStrings"></a>ErrorPageStrings  
  
|Naam|Tekst|  
|----------|----------|  
|LinkLabelBack|Terug|  
|LinkLabelHomePage|startpagina|  
|LinkLabelSendUsEmail|Stuur ons een e-mailbericht|  
|PageTitleError|Er is een probleem voor Hallo aangevraagde pagina|  
|TextblockPotentialCauseIntermittentIssue|Kan dit een onregelmatige data access-probleem dat al is.|  
|TextblockPotentialCauseOldLink|Hallo-koppeling die u hebt geklikt op mogelijk oude en geen punt toohello locatie meer te corrigeren.|  
|TextblockPotentialCauseTechnicalProblem|Mogelijk zijn er een technisch probleem aan onze kant.|  
|TextblockPotentialSolutionRefresh|Hallo probeer pagina te vernieuwen.|  
|TextblockPotentialSolutionStartOver|Beginnen van onze {0}.|  
|TextblockPotentialSolutionTryAgain|Ga {0} en probeer het Hallo-actie die u opnieuw uitgevoerd.|  
|TextReportProblem|{0} met een beschrijving van wat er mis ging en we kijken deze zo snel kunnen wij.|  
|TitlePotentialCause|Mogelijke oorzaak|  
|TitlePotentialSolution|Het is mogelijk slechts een tijdelijk probleem, enkele dingen tootry|  
  
###  <a name="IssuesStrings"></a>IssuesStrings  
  
|Naam|Tekst|  
|----------|----------|  
|WebIssuesIndexTitle|Problemen|  
|WebIssuesNoActiveSubscriptions|U hebt geen actieve abonnementen. In dat geval moet u toosubscribe in voor een product tooreport een probleem.|  
|WebIssuesNotSignin|U bent niet aangemeld. Voer de {0} tooreport een probleem of een opmerking posten.|  
|WebIssuesReportIssueButton|Probleem melden|  
|WebIssuesSignIn|aanmelden|  
|WebIssuesStatusReportedBy|Status: {0} &#124; Gemeld door {1}|  
  
###  <a name="NotFoundStrings"></a>NotFoundStrings  
  
|Naam|Tekst|  
|----------|----------|  
|LinkLabelHomePage|startpagina|  
|LinkLabelSendUsEmail|Stuur ons een e-mailbericht|  
|PageTitleNotFound|Helaas dat Hallo pagina die u zoekt niet vinden|  
|TextblockPotentialCauseMisspelledUrl|U verkeerd gespeld Hallo URL als u hebt getypt in.|  
|TextblockPotentialCauseOldLink|Hallo-koppeling die u hebt geklikt op mogelijk oude en geen punt toohello locatie meer te corrigeren.|  
|TextblockPotentialSolutionRetype|Probeer het opnieuw Hallo-URL.|  
|TextblockPotentialSolutionStartOver|Beginnen van onze {0}.|  
|TextReportProblem|{0} met een beschrijving van wat er mis ging en we kijken deze zo snel kunnen wij.|  
|TitlePotentialCause|Mogelijke oorzaak|  
|TitlePotentialSolution|Mogelijke oplossing|  
  
###  <a name="ProductDetailsStrings"></a>ProductDetailsStrings  
  
|Naam|Tekst|  
|----------|----------|  
|WebProductsAgreement|Abonneer u te {0} Product, ik ga akkoord toohello `<a data-toggle='modal' href='#legal-terms'\>Terms of Use</a\>`.|  
|WebProductsLegalTermsLink|Gebruiksvoorwaarden|  
|WebProductsSubscribeButton|Aanmelden|  
|WebProductsUsageLimitsHeader|Limieten voor Resourcegebruik|  
|WebProductsYouAreNotSubscribed|U bent geabonneerd toothis product.|  
|WebProductsYouRequestedSubscription|U hebt aangevraagd abonnement toothis product.|  
|ErrorYouNeedtoAgreeWithLegalTerms|U moet de gebruiksvoorwaarden toohello akkoord te gaan voordat u verder kunt gaan.|  
|ButtonLabelAddSubscription|Abonnement toevoegen|  
|LinkLabelChangeSubscriptionName|wijzigen|  
|ButtonLabelConfirm|Bevestigen|  
|TextblockMultipleSubscriptionsCount|U hebt {0} abonnementen toothis product:|  
|TextblockSingleSubscriptionsCount|U hebt {0} abonnement toothis product:|  
|TextblockSingleApisCount|Dit product bevat {0} API:|  
|TextblockMultipleApisCount|Dit product bevat {0} API's:|  
|TextblockHeaderSubscribe|Abonneren tooproduct|  
|TextblockSubscriptionDescription|Een nieuw abonnement worden gemaakt als volgt:|  
|TextblockSubscriptionLimitReached|Abonnementen limiet bereikt.|  
  
###  <a name="ProductsStrings"></a>ProductsStrings  
  
|Naam|Tekst|  
|----------|----------|  
|PageTitleProducts|Producten|  
  
###  <a name="ProviderInfoStrings"></a>ProviderInfoStrings  
  
|Naam|Tekst|  
|----------|----------|  
|TextboxExternalIdentitiesDisabled|Aanmelden is uitgeschakeld door beheerders Hallo Hallo momenteel.|  
|TextboxExternalIdentitiesSigninInvitation|U kunt ook aanmelden|  
|TextboxExternalIdentitiesSigninInvitationPrimary|Meld u aan met:|  
  
###  <a name="SigninResources"></a>SigninResources  
  
|Naam|Tekst|  
|----------|----------|  
|PrincipalNotFound|Principal is niet gevonden of de handtekening is ongeldig|  
|ErrorSsoAuthenticationFailed|SSO-verificatie is mislukt|  
|ErrorSsoAuthenticationFailedDetailed|Ongeldig token dat is opgegeven of de handtekening kan niet worden geverifieerd.|  
|ErrorSsoTokenInvalid|SSO-token is ongeldig|  
|ValidationErrorSpecificEmailAlreadyExists|E-mailadres {0}' is al geregistreerd|  
|ValidationErrorSpecificEmailInvalid|E-mailadres {0} is ongeldig|  
|ValidationErrorPasswordInvalid|Wachtwoord is ongeldig. Hallo-fouten te corrigeren en probeer het opnieuw.|  
|PropertyTooShort|{0} is te kort|  
|WebAuthenticationAddresserEmailInvalidErrorMessage|Ongeldig e-mailadres.|  
|ValidationMessageNewPasswordConfirmationRequired|Nieuw wachtwoord bevestigen|  
|ValidationErrorPasswordConfirmationRequired|Bevestig het wachtwoord is leeg|  
|WebAuthenticationEmailChangeNotice|Wijziging bevestigingsbericht is veel te op Hallo {0}. Volg de instructies in het tooconfirm uw nieuwe e-mailadres. Als Hallo e-mail niet heeft bereikt tooyour postvak in van Hallo binnen enkele minuten, controleert u de map Ongewenste e-mail.|  
|WebAuthenticationEmailChangeNoticeHeader|Uw e-wijzigingsaanvraag is met succes verwerkt|  
|WebAuthenticationEmailChangeNoticeTitle|Wijziging van het e-mailadres aangevraagd|  
|WebAuthenticationEmailHasBeenRevertedNotice|U e-mailadres is al aanwezig. Aanvraag is hersteld|  
|ValidationErrorEmailAlreadyExists|Er bestaat al een e-mailadres|  
|ValidationErrorEmailInvalid|Ongeldig e-mailadres|  
|TextboxLabelEmail|E-mail|  
|ValidationErrorEmailRequired|E-mailadres is vereist.|  
|WebAuthenticationErrorNoticeHeader|Fout|  
|WebAuthenticationFieldLengthErrorMessage|{0} moet een maximale lengte van {1}|  
|TextboxLabelEmailFirstName|Voornaam|  
|ValidationErrorFirstNameRequired|Voornaam is vereist.|  
|ValidationErrorFirstNameInvalid|Ongeldige voornaam|  
|NoticeInvalidInvitationToken|Houd er rekening mee dat bevestiging koppelingen slechts 48 uur geldig zijn. Als u nog steeds binnen deze periode, Controleer of dat de koppeling correct is. Als de koppeling is verlopen, klikt u vervolgens herhaalt Hallo-actie die u probeert tooconfirm.|  
|NoticeHeaderInvalidInvitationToken|Ongeldige uitnodiging token|  
|NoticeTitleInvalidInvitationToken|Bevestiging fout|  
|WebAuthenticationLastNameInvalidErrorMessage|Ongeldige achternaam|  
|TextboxLabelEmailLastName|Achternaam|  
|ValidationErrorLastNameRequired|Achternaam is vereist.|  
|WebAuthenticationLinkExpiredNotice|Bevestigingskoppeling tooyou verzonden is verlopen. `<a href={0}?token={1}>Resend confirmation email.</a\>`|  
|NoticePasswordResetLinkInvalidOrExpired|Uw wachtwoord opnieuw instellen van koppeling is ongeldig of verlopen.|  
|WebAuthenticationLinkExpiredNoticeTitle|Koppeling verzonden|  
|WebAuthenticationNewPasswordLabel|Nieuw wachtwoord|  
|ValidationMessageNewPasswordRequired|Nieuwe wachtwoord is vereist.|  
|TextboxLabelNotificationsSenderEmail|Meldingen afzender e|  
|TextboxLabelOrganizationName|Naam van de organisatie|  
|WebAuthenticationOrganizationRequiredErrorMessage|Naam van de organisatie is leeg|  
|WebAuthenticationPasswordChangedNotice|Uw wachtwoord is bijgewerkt|  
|WebAuthenticationPasswordChangedNoticeTitle|Wachtwoord wilt bijwerken|  
|WebAuthenticationPasswordCompareErrorMessage|Wachtwoorden komen niet overeen|  
|WebAuthenticationPasswordConfirmLabel|Wachtwoord bevestigen|  
|ValidationErrorPasswordInvalidDetailed|Wachtwoord is niet sterk genoeg.|  
|WebAuthenticationPasswordLabel|Wachtwoord|  
|ValidationErrorPasswordRequired|Wachtwoord is vereist.|  
|WebAuthenticationPasswordResetSendNotice|Wijziging wachtwoord bevestigingsbericht is veel te op Hallo {0}. Volg de instructies Hallo binnen Hallo e toocontinue uw wachtwoordwijziging.|  
|WebAuthenticationPasswordResetSendNoticeHeader|Uw aanvraag voor wachtwoordherstel is met succes verwerkt|  
|WebAuthenticationPasswordResetSendNoticeTitle|Wachtwoordherstel aangevraagd|  
|WebAuthenticationRequestNotFoundNotice|Aanvraag is niet gevonden|  
|WebAuthenticationSenderEmailRequiredErrorMessage|Meldingen afzender e-mail is leeg|  
|WebAuthenticationSigninPasswordLabel|Hallo wijzigen om te bevestigen dat een wachtwoord invoeren|  
|WebAuthenticationSignupConfirmNotice|Bevestiging per e-mail is onderweg te {0}. < br /\> Neem Volg de instructies in Hallo e-tooactivate uw account. < br /\> als Hallo e-mail niet heeft bereikt in je postvak in in Hallo binnen enkele minuten, controleert u de map Ongewenste e-mail.|  
|WebAuthenticationSignupConfirmNoticeHeader|Uw account is gemaakt|  
|WebAuthenticationSignupConfirmNoticeRepeatHeader|Registratie bevestigingsbericht is opnieuw verzonden|  
|WebAuthenticationSignupConfirmNoticeTitle|Account dat is gemaakt|  
|WebAuthenticationTokenRequiredErrorMessage|Token is leeg|  
|WebAuthenticationUserAlreadyRegisteredNotice|Het lijkt dat een gebruiker met dit e-mailadres is al geregistreerd in Hallo-systeem. Als u uw wachtwoord bent vergeten, kunt u proberen toorestore of neem contact op met het ondersteuningsteam.|  
|WebAuthenticationUserAlreadyRegisteredNoticeHeader|Gebruiker is al geregistreerd|  
|WebAuthenticationUserAlreadyRegisteredNoticeTitle|Al geregistreerd|  
|ButtonLabelChangePassword|Wachtwoord wijzigen|  
|ButtonLabelChangeAccountInfo|Informatie over de account wijzigen|  
|ButtonLabelCloseAccount|Account sluiten|  
|WebAuthenticationInvalidCaptchaErrorMessage|Ingevoerde tekst komt niet overeen met de tekst op Hallo-afbeelding. Probeer het opnieuw.|  
|ValidationErrorCredentialsInvalid|E-mailadres of wachtwoord is ongeldig. Hallo-fouten te corrigeren en probeer het opnieuw.|  
|WebAuthenticationRequestIsNotValid|Aanvraag is niet geldig|  
|WebAuthenticationUserIsNotConfirm|Bevestig uw inschrijving voordat u probeert toosign in.|  
|WebAuthenticationInvalidEmailFormated|E-mailadres is ongeldig: {0}|  
|WebAuthenticationUserNotFound|De gebruiker is niet gevonden|  
|WebAuthenticationTenantNotRegistered|Uw account hoort tooa Azure Active Directory-tenant die geen geautoriseerde tooaccess deze portal.|  
|WebAuthenticationAuthenticationFailed|Verificatie is mislukt.|  
|WebAuthenticationGooglePlusNotEnabled|Verificatie is mislukt. Of u gemachtigd toepassing hello en neem contact op met de Hallo beheerder toomake is zeker dat Google-verificatie juist geconfigureerd.|  
|ValidationErrorAllowedTenantIsRequired|Toegestane Tenant is vereist|  
|ValidationErrorTenantIsNotValid|Hello Azure Active Directory-tenant '{0}' is niet geldig.|  
|WebAuthenticationActiveDirectoryTitle|Azure Active Directory|  
|WebAuthenticationLoginUsingYourProvider|Meld u aan met uw account {0}|  
|WebAuthenticationUserLimitNotice|Deze service heeft Hallo kunt u het maximum aantal toegestane gebruikers bereikt. Neem `<a href="mailto:{0}"\>contact hello administrator</a\>` tooupgrade hun gebruikersregistratie-service en opnieuw in te schakelen.|  
|WebAuthenticationUserLimitNoticeHeader|Gebruikersregistratie uitgeschakeld|  
|WebAuthenticationUserLimitNoticeTitle|Gebruikersregistratie uitgeschakeld|  
|WebAuthenticationUserRegistrationDisabledNotice|De registratie van gebruikers is uitgeschakeld door Hallo beheerder. Meld u aan met externe id-provider.|  
|WebAuthenticationUserRegistrationDisabledNoticeHeader|Gebruikersregistratie uitgeschakeld|  
|WebAuthenticationUserRegistrationDisabledNoticeTitle|Gebruikersregistratie uitgeschakeld|  
|WebAuthenticationSignupPendingConfirmationNotice|Voordat we Hallo maken van uw account kunt voltooien moeten we tooverify uw e-mailadres. We hebben een e-mailbericht te verzonden {0}. Volg de instructies Hallo binnen Hallo e-tooactivate uw account. Als Hallo e-mail niet binnen Hallo binnen enkele minuten plaatsvinden, controleert u de map Ongewenste e-mail.|  
|WebAuthenticationSignupPendingConfirmationAccountFoundNotice|Er is een niet-bevestigde account aangetroffen voor Hallo e-mailadres {0}. toocomplete hello maken van uw account moet tooverify uw e-mailadres. We hebben een e-mailbericht te verzonden {0}. Volg de instructies Hallo binnen Hallo e-tooactivate uw account. Als Hallo e-mail niet binnen Hallo binnen enkele minuten plaatsvinden, Controleer of de map Ongewenste e-mail|  
|WebAuthenticationSignupConfirmationAlmostDone|Bijna klaar|  
|WebAuthenticationSignupConfirmationEmailSent|We hebben een e-mailbericht te verzonden {0}. Volg de instructies Hallo binnen Hallo e-tooactivate uw account. Als Hallo e-mail niet binnen Hallo binnen enkele minuten plaatsvinden, controleert u de map Ongewenste e-mail.|  
|WebAuthenticationEmailSentNotificationMessage|E-mail is verzonden te {0}|  
|WebAuthenticationNoAadTenantConfigured|Er is geen Azure Active Directory-tenant is geconfigureerd voor Hallo-service.|  
|CheckboxLabelUserRegistrationTermsConsentRequired|Ik ga akkoord toohello `<a data-toggle="modal" href="#" data-target="#terms"\>Terms of Use</a\>`.|  
|TextblockUserRegistrationTermsProvided|Raadpleeg`<a data-toggle="modal" href="#" data-target="#terms"\>Terms of Use.</a\>`|  
|DialogHeadingTermsOfUse|Gebruiksvoorwaarden|  
|ValidationMessageConsentNotAccepted|U moet de gebruiksvoorwaarden toohello akkoord te gaan voordat u verder kunt gaan.|  
  
###  <a name="SigninStrings"></a>SigninStrings  
  
|Naam|Tekst|  
|----------|----------|  
|WebAuthenticationForgotPassword|Wachtwoord vergeten?|  
|WebAuthenticationIfAdministrator|Als u een beheerder moet u zich aanmeldt `<a href="{0}"\>here</a\>`.|  
|WebAuthenticationNotAMember|Geen lid nog? `<a href="/signup"\>Sign up now</a\>`|  
|WebAuthenticationRemember|Mijn aanmeldingsgegevens onthouden op deze computer|  
|WebAuthenticationSigininWithPassword|Meld u aan met uw gebruikersnaam en wachtwoord|  
|WebAuthenticationSigninTitle|Aanmelden|  
|WebAuthenticationSignUpNow|Nu aanmelden|  
  
###  <a name="SignupStrings"></a>SignupStrings  
  
|Naam|Tekst|  
|----------|----------|  
|PageTitleSignup|Aanmelden|  
|WebAuthenticationAlreadyAMember|Bent u al lid?|  
|WebAuthenticationCreateNewAccount|Maak een nieuwe API Management-account|  
|WebAuthenticationSigninNow|Nu aanmelden|  
|ButtonLabelSignup|Aanmelden|  
  
###  <a name="SubscriptionListStrings"></a>SubscriptionListStrings  
  
|Naam|Tekst|  
|----------|----------|  
|SubscriptionCancelConfirmation|Weet u zeker dat u toocancel dit abonnement?|  
|SubscriptionRenewConfirmation|Weet u zeker dat u toorenew dit abonnement?|  
|WebDevelopersManageSubscriptions|Abonnementen beheren|  
|WebDevelopersPrimaryKey|Primaire sleutel|  
|WebDevelopersRegenerateLink|Opnieuw genereren|  
|WebDevelopersSecondaryKey|Secundaire sleutel|  
|ButtonLabelShowKey|Weergeven|  
|ButtonLabelRenewSubscription|Verlengen|  
|WebDevelopersSubscriptionReqested|Aangevraagd voor {0}|  
|WebDevelopersSubscriptionRequestedState|Aangevraagd|  
|WebDevelopersSubscriptionTableNameHeader|Naam|  
|WebDevelopersSubscriptionTableStateHeader|Status|  
|WebDevelopersUsageStatisticsLink|Analytics-rapporten|  
|WebDevelopersYourSubscriptions|Uw abonnementen|  
|SubscriptionPropertyLabelRequestedDate|Aangevraagde op|  
|SubscriptionPropertyLabelStartedDate|Begonnen op|  
|PageTitleRenameSubscription|Wijzig de naam van abonnement|  
|SubscriptionPropertyLabelName|De naam van abonnement|  
  
###  <a name="SubscriptionStrings"></a>SubscriptionStrings  
  
|Naam|Tekst|  
|----------|----------|  
|SectionHeadingCloseAccount|Tooclose Zoek uw account?|  
|PageTitleDeveloperProfile|Profiel|  
|ButtonLabelHideKey|Verbergen|  
|ButtonLabelRegenerateKey|Opnieuw genereren|  
|InformationMessageKeyWasRegenerated|Weet u zeker dat u tooregenerate deze sleutel?|  
|ButtonLabelShowKey|Weergeven|  
  
###  <a name="UpdateProfileStrings"></a>UpdateProfileStrings  
  
|Naam|Tekst|  
|----------|----------|  
|ButtonLabelUpdateProfile|Profiel bijwerken|  
|PageTitleUpdateProfile|Accountgegevens bijwerken|  
  
###  <a name="UserProfile"></a>Gebruikersprofiel  
  
|Naam|Tekst|  
|----------|----------|  
|ButtonLabelChangeAccountInfo|Informatie over de account wijzigen|  
|ButtonLabelChangePassword|Wachtwoord wijzigen|  
|ButtonLabelCloseAccount|Account sluiten|  
|TextboxLabelEmail|E-mail|  
|TextboxLabelEmailFirstName|Voornaam|  
|TextboxLabelEmailLastName|Achternaam|  
|TextboxLabelNotificationsSenderEmail|Meldingen afzender e|  
|TextboxLabelOrganizationName|Naam van de organisatie|  
|SubscriptionStateActive|Actief|  
|SubscriptionStateCancelled|Geannuleerd|  
|SubscriptionStateExpired|Verlopen|  
|SubscriptionStateRejected|Afgewezen|  
|SubscriptionStateRequested|Aangevraagd|  
|SubscriptionStateSuspended|Onderbroken|  
|DefaultSubscriptionNameTemplate|{0} (standaard)|  
|SubscriptionNameTemplate|Ontwikkelaars toegang #{0}|  
|TextboxLabelSubscriptionName|De naam van abonnement|  
|ValidationMessageSubscriptionNameRequired|De abonnementsnaam van het mag niet leeg zijn.|  
|ApiManagementUserLimitReached|Deze service heeft Hallo kunt u het maximum aantal toegestane gebruikers bereikt. Werk tooa hoger prijscategorie.|  
  
##  <a name="glyphs"></a>De glyph-resources  
 Developer-portal API Management-sjablonen kunt Hallo glyphs uit [Glyphicons van Bootstrap](http://getbootstrap.com/components/#glyphicons). Deze reeks glyphs bevat meer dan 250 glyphs in lettertype-indeling van Hallo [Glyphicon](http://glyphicons.com/) Halflings ingesteld. toouse een glyph van deze ingesteld, Hallo syntaxis gebruiken.  
  
```html  
<span class="glyphicon glyphicon-user">  
```  
  
 Zie voor een volledige lijst van glyphs Hallo [Glyphicons van Bootstrap](http://getbootstrap.com/components/#glyphicons).

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over het werken met sjablonen [hoe toocustomize API Management-portal voor ontwikkelaars met behulp van sjablonen Hallo](api-management-developer-portal-templates.md).
