---
title: aaa "profielsjablonen van de gebruiker in Azure API Management | Microsoft Docs'
description: Meer informatie over hoe toocustomize Hallo inhoud van het gebruikersprofiel Hallo-pagina's in Azure API Management Hallo developer-Portal.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2e3b73ef-d223-44fe-9280-c3af3fd4a030
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: c8f153b310221164809acf58e4af236928ceb41d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="user-profile-templates-in-azure-api-management"></a>Gebruiker profielsjablonen in Azure API Management
Azure API Management biedt dat u Hallo mogelijkheid toocustomize Hallo inhoud van developer portal-pagina's met behulp van een set van sjablonen die hun inhoud configureren. Met behulp van [DotLiquid](http://dotliquidmarkup.org/) syntaxis en het Hallo-editor naar keuze, zoals [DotLiquid voor ontwerpers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), en een opgegeven set gelokaliseerde [resources String](api-management-template-resources.md#strings), [ De glyph-resources](api-management-template-resources.md#glyphs), en [pagina besturingselementen](api-management-page-controls.md), hebt u aanzienlijke flexibiliteit tooconfigure Hallo inhoud van het Hallo-pagina's naar wens met behulp van deze sjablonen.  
  
 Hallo-sjablonen in deze sectie kunt u toocustomize Hallo inhoud van Hallo gebruiker profiel's in Hallo-portal voor ontwikkelaars.  
  
-   [Profiel](#Profile)  
  
-   [Abonnementen](#Subscriptions)  
  
-   [Toepassingen](#Applications)  
  
-   [Update-accountgegevens](#UpdateAccountInfo)  
  
> [!NOTE]
>  Standaard-voorbeeldsjablonen zijn opgenomen in de volgende documentatie Hallo, maar onderwerp toochange vanwege toocontinuous verbeteringen zijn. U kunt Hallo live standaardsjablonen in Hallo developer-portal door te navigeren toohello gewenst afzonderlijke sjablonen weergeven. Zie voor meer informatie over het werken met sjablonen [hoe toocustomize API Management-portal voor ontwikkelaars met behulp van sjablonen Hallo](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
##  <a name="Profile"></a>Profiel  
 Hallo **profiel** sjabloon kunt u toocustomize Hallo Gebruikersprofielsectie Hallo van profielpagina van gebruiker in Hallo-portal voor ontwikkelaars.  
  
 ![Pagina gebruikersprofiel](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "APIM gebruikersprofiel pagina")  
  
### <a name="default-template"></a>Standaardsjabloon  
  
```xml  
<div class="pull-right">  
  {% if canChangePassword == true %}  
  <a class="btn btn-default" id="ChangePassword" role="button" href="{{changePasswordUrl}}">{% localized "UserProfile|ButtonLabelChangePassword" %}</a>  
  {% endif %}  
  <a id="changeAccountInfo" href="{{changeNameOrEmailUrl}}" class="btn btn-default">  
    <span class="glyphicon glyphicon-user"></span>  
    <span>{% localized "UserProfile|ButtonLabelChangeAccountInfo" %}</span>  
  </a>  
</div>  
<h2>{% localized "SubscriptionStrings|PageTitleDeveloperProfile" %}</h2>  
<div class="container-fluid">  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="Email">{% localized "UserProfile|TextboxLabelEmail" %}</label>  
    </div>  
    <div class="col-sm-9" id="Email">{{email}}</div>  
  </div>  
  
  {% if isSystemUser != true %}  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="FirstName">{% localized "UserProfile|TextboxLabelEmailFirstName" %}</label>  
    </div>  
    <div class="col-sm-9" id="FirstName">{{FirstName}}</div>  
  </div>  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="LastName">{% localized "UserProfile|TextboxLabelEmailLastName" %}</label>  
    </div>  
    <div class="col-sm-9" id="LastName">{{LastName}}</div>  
  </div>  
  {% else %}  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="CompanyName">{% localized "UserProfile|TextboxLabelOrganizationName" %}</label>  
    </div>  
    <div class="col-sm-9" id="CompanyName">{{CompanyName}}</div>  
  </div>  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="AddresserEmail">{% localized "UserProfile|TextboxLabelNotificationsSenderEmail" %}</label>  
    </div>  
    <div class="col-sm-9" id="AddresserEmail">{{AddresserEmail}}</div>  
  </div>  
  {% endif %}  
  
</div>  
```  
  
### <a name="controls"></a>Besturingselementen  
 Deze sjabloon kan geen gebruik [pagina besturingselementen](api-management-page-controls.md).  
  
### <a name="data-model"></a>Gegevensmodel  
  
> [!NOTE]
>  Hallo [profiel](#Profile), [toepassingen](#Applications), en [abonnementen](#Subscriptions) sjablonen Hallo dezelfde gegevens modelleren en Hallo ontvangen delen dezelfde sjabloongegevens.  
  
|Eigenschap|Type|Beschrijving|  
|--------------|----------|-----------------|  
|Voornaam|Tekenreeks|De voornaam van de huidige gebruiker Hallo.|  
|Achternaam|Tekenreeks|De achternaam van de huidige gebruiker Hallo.|  
|Bedrijfsnaam|Tekenreeks|bedrijfsnaam van de huidige gebruiker Hallo Hallo.|  
|addresserEmail|Tekenreeks|E-mailadres van de huidige gebruiker Hallo.|  
|developersUsageStatisticsLinkk|Tekenreeks|Relatieve URL tooview analytics voor de huidige gebruiker Hallo.|  
|abonnementen|Verzameling van [abonnement](api-management-template-data-model-reference.md#Subscription) entiteiten.|Hallo-abonnementen voor de huidige gebruiker Hallo.|  
|toepassingen|Verzameling van [toepassing](api-management-template-data-model-reference.md#Application) entiteiten.|Hallo-toepassingen van de huidige gebruiker Hallo.|  
|changePasswordUrl|Tekenreeks|Hallo relatieve URL toochange Hallo huidige wachtwoord van gebruiker.|  
|changeNameOrEmailUrl|Tekenreeks|relatieve URL toochange Hallo-naam en e-mailadres voor de huidige gebruiker Hallo Hallo.|  
|canChangePassword|Booleaanse waarde|Hiermee wordt aangegeven of kan de huidige gebruiker Hallo hun wachtwoord wijzigen.|  
|isSystemUser|Booleaanse waarde|Of Hallo-huidige gebruiker lid is van een van de ingebouwde Hallo [groepen](api-management-key-concepts.md#groups).|  
  
### <a name="sample-template-data"></a>Voorbeeldgegevens voor sjabloon  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <a name="Subscriptions"></a>Abonnementen  
 Hallo **abonnementen** sjabloon kunt u toocustomize Hallo abonnementen sectie van Hallo pagina gebruikersprofiel in Hallo-portal voor ontwikkelaars.  
  
 ![Abonnement op de gebruikerspagina](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "APIM op de pagina gebruiker abonnement")  
  
### <a name="default-template"></a>Standaardsjabloon  
  
```xml  
<div class="ap-account-subscriptions">  
  <a href="{{developersUsageStatisticsLink}}" id="UsageStatistics" class="btn btn-default pull-right">  
    <span class="glyphicon glyphicon-stats"></span>  
    <span>{% localized "SubscriptionListStrings|WebDevelopersUsageStatisticsLink" %}</span>  
  </a>  
  
  <h2>{% localized "SubscriptionListStrings|WebDevelopersYourSubscriptions" %}</h2>  
  
  <table class="table">  
    <thead>  
      <tr>  
        <th>Subscription details</th>  
        <th>Product</th>  
        <th>{% localized "SubscriptionListStrings|WebDevelopersSubscriptionTableStateHeader" %}</th>  
        <th>Action</th>  
      </tr>  
    </thead>  
    <tbody>  
      {% if subscriptions.size == 0 %}  
      <tr>  
        <td class="text-center" colspan="4">  
          {% localized "CommonResources|NoItemsToDisplay" %}  
        </td>  
      </tr>  
      {% else %}  
      {% for subscription in subscriptions %}  
      <tr id="{{subscription.id}}" {% if subscription.hasExpired %} class="expired" {% endif %}>  
        <td>  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelName" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.displayName }}  
            </div>  
            <div class="col-lg-2">  
              <a class="btn-link" href="/Subscriptions/{{subscription.id}}/Rename">Rename</a>  
            </div>  
            <div class="clearfix"></div>  
          </div>  
          {% if subscription.isAwaitingApproval %}  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelRequestedDate" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.createdDate | date:"MM/dd/yyyy" }}  
            </div>  
          </div>  
          {% else %}  
          {% if subscription.isRejected == false %}  
          {% if subscription.startDate %}  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelStartedDate" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.startDate | date:"MM/dd/yyyy" }}  
            </div>  
          </div>  
          {% endif %}  
  
          <!-- ko with: Developers.Account.Root.account.key('{{subscription.primaryKey}}', '{{subscription.id}}', true) -->  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|WebDevelopersPrimaryKey" %}</label>  
            <div class="col-lg-6">  
              <code data-bind="text: $data.displayKey()" id="primary_{{subscription.id}}"></code>  
            </div>  
            <div class="col-lg-2">  
              <!-- ko if: !requestInProgress() -->  
              <div class="nowrap">  
                <a href="#" class="btn-link" id="togglePrimary_{{subscription.id}}" data-bind="click: toggleKeyDisplay, text: toggleKeyLabel"></a>  
                |  
                <a href="#" class="btn-link" id="regeneratePrimary_{{subscription.id}}" data-bind="click: regenerateKey, text: regenerateKeyLabel"></a>  
              </div>  
              <!-- /ko -->  
              <!-- ko if: requestInProgress() -->  
              <div class="progress progress-striped active">  
                <div class="progress-bar" role="progressbar" aria-valuenow="100" aria-valuemin="0" aria-valuemax="100" style="width: 100%">  
                  <span class="sr-only"></span>  
                </div>  
              </div>  
              <!-- /ko -->  
            </div>  
            <div class="clearfix"></div>  
          </div>  
          <!-- /ko -->  
          <!-- ko with: Developers.Account.Root.account.key('{{subscription.secondaryKey}}', '{{subscription.id}}', false) -->  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|WebDevelopersSecondaryKey" %}</label>  
            <div class="col-lg-6">  
              <code data-bind="text: $data.displayKey()" id="secondary_{{subscription.id}}"></code>  
            </div>  
            <div class="col-lg-2">  
              <div class="nowrap">  
                <a href="#" class="btn-link" id="toggleSecondary_{{subscription.id}}" data-bind="click: toggleKeyDisplay, text: toggleKeyLabel">{% localized "SubscriptionListStrings|ButtonLabelShowKey" %}</a>  
                |  
                <a href="#" class="btn-link" id="regenerateSecondary_{{subscription.id}}" data-bind="click: regenerateKey, text: regenerateKeyLabel">{% localized "SubscriptionListStrings|WebDevelopersRegenerateLink" %}</a>  
              </div>  
            </div>  
            <div class="clearfix"> </div>  
          </div>  
          <!-- /ko -->  
          {% endif %}  
          {% endif %}  
        </td>  
        <td>  
          <a href="{{subscription.productDetailsUrl}}">{{subscription.productTitle}}</a>  
        </td>  
        <td>  
          <strong>  
            {{subscription.state}}  
          </strong>  
        </td>  
        <td>  
          <div class="nowrap">  
            {% if subscription.canBeCancelled %}  
            <subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }"></subscription-cancel>  
            {% endif %}  
          </div>  
        </td>  
      </tr>  
      {% endfor %}  
      {% endif %}  
    </tbody>  
  </table>  
</div>  
```  
  
### <a name="controls"></a>Besturingselementen  
 Deze sjabloon kunt Hallo volgende [pagina besturingselementen](api-management-page-controls.md).  
  
-   [abonnement annuleren](api-management-page-controls.md#subscription-cancel)  
  
### <a name="data-model"></a>Gegevensmodel  
  
> [!NOTE]
>  Hallo [profiel](#Profile), [toepassingen](#Applications), en [abonnementen](#Subscriptions) sjablonen Hallo dezelfde gegevens modelleren en Hallo ontvangen delen dezelfde sjabloongegevens.  
  
|Eigenschap|Type|Beschrijving|  
|--------------|----------|-----------------|  
|Voornaam|Tekenreeks|De voornaam van de huidige gebruiker Hallo.|  
|Achternaam|Tekenreeks|De achternaam van de huidige gebruiker Hallo.|  
|Bedrijfsnaam|Tekenreeks|bedrijfsnaam van de huidige gebruiker Hallo Hallo.|  
|addresserEmail|Tekenreeks|E-mailadres van de huidige gebruiker Hallo.|  
|developersUsageStatisticsLinkk|Tekenreeks|Relatieve URL tooview analytics voor de huidige gebruiker Hallo.|  
|abonnementen|Verzameling van [abonnement](api-management-template-data-model-reference.md#Subscription) entiteiten.|Hallo-abonnementen voor de huidige gebruiker Hallo.|  
|toepassingen|Verzameling van [toepassing](api-management-template-data-model-reference.md#Application) entiteiten.|Hallo-toepassingen van de huidige gebruiker Hallo.|  
|changePasswordUrl|Tekenreeks|Hallo relatieve URL toochange Hallo huidige wachtwoord van gebruiker.|  
|changeNameOrEmailUrl|Tekenreeks|relatieve URL toochange Hallo-naam en e-mailadres voor de huidige gebruiker Hallo Hallo.|  
|canChangePassword|Booleaanse waarde|Hiermee wordt aangegeven of kan de huidige gebruiker Hallo hun wachtwoord wijzigen.|  
|isSystemUser|Booleaanse waarde|Of Hallo-huidige gebruiker lid is van een van de ingebouwde Hallo [groepen](api-management-key-concepts.md#groups).|  
  
### <a name="sample-template-data"></a>Voorbeeldgegevens voor sjabloon  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <a name="Applications"></a>Toepassingen  
 Hallo **toepassingen** sjabloon kunt u toocustomize Hallo abonnementen sectie van Hallo pagina gebruikersprofiel in Hallo-portal voor ontwikkelaars.  
  
 ![Gebruiker toepassingen accountpagina](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "APIM gebruikersaccount pagina met toepassingen")  
  
### <a name="default-template"></a>Standaardsjabloon  
  
```xml  
<div class="ap-account-applications">  
  <a id="RegisterApplication" href="/Developer/Applications/Register" class="btn btn-success pull-right">  
    <span class="glyphicon glyphicon-plus"></span>  
    <span>{% localized "ApplicationListStrings|WebDevelopersRegisterAppLink" %}</span>  
  </a>  
  <h2>{% localized "ApplicationListStrings|WebDevelopersYourApplicationsHeader" %}</h2>  
  
  <table class="table">  
    <thead>  
      <tr>  
        <th class="col-md-8">{% localized "ApplicationListStrings|WebDevelopersAppTableNameHeader" %}</th>  
        <th class="col-md-2">{% localized "ApplicationListStrings|WebDevelopersAppTableCategoryHeader" %}</th>  
        <th class="col-md-2" colspan="2">{% localized "ApplicationListStrings|WebDevelopersAppTableStateHeader" %}</th>  
      </tr>  
    </thead>  
    <tbody>  
  
      {% if applications.size == 0 %}  
  
      <tr>  
        <td class="col-md-12 text-center" colspan="4">  
          {% localized "CommonResources|NoItemsToDisplay" %}  
        </td>  
      </tr>  
  
      {% else %}  
  
      {% for app in applications %}  
      <tr>  
        <td class="col-md-8">  
          {{app.title}}  
        </td>  
        <td class="col-md-2">  
          {{app.categoryName}}  
        </td>  
        <td class="col-md-2">  
          <strong>  
            {% case app.state %}  
            {% when ApplicationStateModel.Registered %}  
            {% localized "ApplicationListStrings|WebDevelopersAppNotSubminted" %}  
  
            {% when ApplicationStateModel.Unpublished %}  
            {% localized "ApplicationListStrings|WebDevelopersAppNotPublished" %}  
  
            {% else %}  
            {{ app.state }}  
            {% endcase %}  
          </strong>  
        </td>  
        <td class="col-md-1">  
          <div class="nowrap">  
            {% if app.state != ApplicationStateModel.Submitted and app.state != ApplicationStateModel.Published %}  
            <app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
            {% endif %}  
          </div>  
        </td>  
      </tr>  
      {% endfor %}  
  
      {% endif %}  
    </tbody>  
  </table>  
</div>  
```  
  
### <a name="controls"></a>Besturingselementen  
 Deze sjabloon kunt Hallo volgende [pagina besturingselementen](api-management-page-controls.md).  
  
-   [App-acties](api-management-page-controls.md#app-actions)  
  
### <a name="data-model"></a>Gegevensmodel  
  
> [!NOTE]
>  Hallo [profiel](#Profile), [toepassingen](#Applications), en [abonnementen](#Subscriptions) sjablonen Hallo dezelfde gegevens modelleren en Hallo ontvangen delen dezelfde sjabloongegevens.  
  
|Eigenschap|Type|Beschrijving|  
|--------------|----------|-----------------|  
|Voornaam|Tekenreeks|De voornaam van de huidige gebruiker Hallo.|  
|Achternaam|Tekenreeks|De achternaam van de huidige gebruiker Hallo.|  
|Bedrijfsnaam|Tekenreeks|bedrijfsnaam van de huidige gebruiker Hallo Hallo.|  
|addresserEmail|Tekenreeks|E-mailadres van de huidige gebruiker Hallo.|  
|developersUsageStatisticsLinkk|Tekenreeks|Relatieve URL tooview analytics voor de huidige gebruiker Hallo.|  
|abonnementen|Verzameling van [abonnement](api-management-template-data-model-reference.md#Subscription) entiteiten.|Hallo-abonnementen voor de huidige gebruiker Hallo.|  
|toepassingen|Verzameling van [toepassing](api-management-template-data-model-reference.md#Application) entiteiten.|Hallo-toepassingen van de huidige gebruiker Hallo.|  
|changePasswordUrl|Tekenreeks|Hallo relatieve URL toochange Hallo huidige wachtwoord van gebruiker.|  
|changeNameOrEmailUrl|Tekenreeks|relatieve URL toochange Hallo-naam en e-mailadres voor de huidige gebruiker Hallo Hallo.|  
|canChangePassword|Booleaanse waarde|Hiermee wordt aangegeven of kan de huidige gebruiker Hallo hun wachtwoord wijzigen.|  
|isSystemUser|Booleaanse waarde|Of Hallo-huidige gebruiker lid is van een van de ingebouwde Hallo [groepen](api-management-key-concepts.md#groups).|  
  
### <a name="sample-template-data"></a>Voorbeeldgegevens voor sjabloon  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <a name="UpdateAccountInfo"></a>Update-accountgegevens  
 Hallo **Uodate accountgegevens** sjabloon kunt u toocustomize hello **accountgegevens bijwerken** pagina in het Hallo-portal voor ontwikkelaars.  
  
 ![Info pagina Developer Portal sjablonen voor gebruikersaccounts](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "APIM Info pagina Developer Portal sjablonen voor gebruikersaccounts")  
  
### <a name="default-template"></a>Standaardsjabloon  
  
```xml  
<div class="row">  
  <div class="col-sm-6 col-md-6">  
    <div class="form-group">  
      <label for="Email">{% localized "SigninResources|TextboxLabelEmail" %}</label>  
      <input autofocus="autofocus" class="form-control" id="Email" name="Email" type="text" value="{{email}}">  
    </div>  
    <div class="form-group">  
      <label for="FirstName">{% localized "SigninResources|TextboxLabelEmailFirstName" %}</label>  
      <input class="form-control" id="FirstName" name="FirstName" type="text" value="{{firstName}}">  
    </div>  
    <div class="form-group">  
      <label for="LastName">{% localized "SigninResources|TextboxLabelEmailLastName" %}</label>  
      <input class="form-control" id="LastName" name="LastName" type="text" value="{{lastName}}">  
    </div>  
    <div class="form-group">  
      <label for="Password">{% localized "SigninResources|WebAuthenticationSigninPasswordLabel" %}</label>  
      <input class="form-control" id="Password" name="Password" type="password">  
    </div>  
  </div>  
</div>  
  
<button type="submit" class="btn btn-primary" id="UpdateProfile">  
  {% localized "UpdateProfileStrings|ButtonLabelUpdateProfile" %}  
</button>  
<a class="btn btn-default" href="/developer" role="button">  
  {% localized "CommonStrings|ButtonLabelCancel" %}  
</a>  
```  
  
### <a name="controls"></a>Besturingselementen  
 Deze sjabloon kan geen gebruik [pagina besturingselementen](api-management-page-controls.md).  
  
### <a name="data-model"></a>Gegevensmodel  
 [Gebruikersaccountgegevens](api-management-template-data-model-reference.md#UserAccountInfo) entiteit.  
  
### <a name="sample-template-data"></a>Voorbeeldgegevens voor sjabloon  
  
```json  
{  
    "FirstName": "Administrator",  
    "LastName": "",  
    "Email": "admin@live.com",  
    "Password": null,  
    "NameIdentifier": null,  
    "ProviderName": null,  
    "IsBasicAccount": false  
}  
```

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over het werken met sjablonen [hoe toocustomize API Management-portal voor ontwikkelaars met behulp van sjablonen Hallo](api-management-developer-portal-templates.md).
