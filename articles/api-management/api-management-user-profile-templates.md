---
title: Gebruiker profielsjablonen in Azure API Management | Microsoft Docs
description: Informatie over het aanpassen van de inhoud van het gebruikersprofiel pagina's in de ontwikkelaarsportal in Azure API Management.
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
ms.openlocfilehash: 9a11bd5800068a5725ab2f099043993bff0b28d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="user-profile-templates-in-azure-api-management"></a><span data-ttu-id="edf30-103">Gebruiker profielsjablonen in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="edf30-103">User profile templates in Azure API Management</span></span>
<span data-ttu-id="edf30-104">Azure API Management biedt de mogelijkheid voor het aanpassen van de inhoud van developer portal-pagina's met behulp van een set van sjablonen die hun inhoud configureren.</span><span class="sxs-lookup"><span data-stu-id="edf30-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="edf30-105">Met behulp van [DotLiquid](http://dotliquidmarkup.org/) syntaxis en de editor van uw keuze, zoals [DotLiquid voor ontwerpers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), en een opgegeven set gelokaliseerde [resources String](api-management-template-resources.md#strings), [Glyph-resources](api-management-template-resources.md#glyphs), en [pagina besturingselementen](api-management-page-controls.md), hebt u aanzienlijke flexibiliteit voor het configureren van de inhoud van de pagina's naar wens met behulp van deze sjablonen.</span><span class="sxs-lookup"><span data-stu-id="edf30-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="edf30-106">De sjablonen in deze sectie kunnen u de inhoud van de gebruiker profiel pagina's in de ontwikkelaarsportal aanpassen.</span><span class="sxs-lookup"><span data-stu-id="edf30-106">The templates in this section allow you to customize the content of the User profile pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="edf30-107">Profiel</span><span class="sxs-lookup"><span data-stu-id="edf30-107">Profile</span></span>](#Profile)  
  
-   [<span data-ttu-id="edf30-108">Abonnementen</span><span class="sxs-lookup"><span data-stu-id="edf30-108">Subscriptions</span></span>](#Subscriptions)  
  
-   [<span data-ttu-id="edf30-109">Toepassingen</span><span class="sxs-lookup"><span data-stu-id="edf30-109">Applications</span></span>](#Applications)  
  
-   [<span data-ttu-id="edf30-110">Update-accountgegevens</span><span class="sxs-lookup"><span data-stu-id="edf30-110">Update account info</span></span>](#UpdateAccountInfo)  
  
> [!NOTE]
>  <span data-ttu-id="edf30-111">Standaard-voorbeeldsjablonen zijn opgenomen in de volgende documentatie, maar nog worden gewijzigd vanwege continu verbeteringen.</span><span class="sxs-lookup"><span data-stu-id="edf30-111">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="edf30-112">U kunt de live standaardsjablonen weergeven in de ontwikkelaarsportal door te navigeren naar de gewenste afzonderlijke sjablonen.</span><span class="sxs-lookup"><span data-stu-id="edf30-112">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="edf30-113">Zie voor meer informatie over het werken met sjablonen [het aanpassen van de API Management portal voor ontwikkelaars met behulp van sjablonen](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="edf30-113">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="edf30-114"><a name="Profile"></a>Profiel</span><span class="sxs-lookup"><span data-stu-id="edf30-114"><a name="Profile"></a> Profile</span></span>  
 <span data-ttu-id="edf30-115">De **profiel** sjabloon kunt u de Gebruikersprofielsectie van de pagina gebruikersprofiel in de ontwikkelaarsportal aanpassen.</span><span class="sxs-lookup"><span data-stu-id="edf30-115">The **profile** template allows you to customize the user profile section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="edf30-116">![Pagina gebruikersprofiel](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "APIM gebruikersprofiel pagina")</span><span class="sxs-lookup"><span data-stu-id="edf30-116">![User Profile Page](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "APIM User Profile Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="edf30-117">Standaardsjabloon</span><span class="sxs-lookup"><span data-stu-id="edf30-117">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="edf30-118">Besturingselementen</span><span class="sxs-lookup"><span data-stu-id="edf30-118">Controls</span></span>  
 <span data-ttu-id="edf30-119">Deze sjabloon kan geen gebruik [pagina besturingselementen](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="edf30-119">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="edf30-120">Gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="edf30-120">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="edf30-121">De [profiel](#Profile), [toepassingen](#Applications), en [abonnementen](#Subscriptions) sjablonen voor het gegevensmodel met dezelfde delen en ontvangen van dezelfde sjabloongegevens.</span><span class="sxs-lookup"><span data-stu-id="edf30-121">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="edf30-122">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="edf30-122">Property</span></span>|<span data-ttu-id="edf30-123">Type</span><span class="sxs-lookup"><span data-stu-id="edf30-123">Type</span></span>|<span data-ttu-id="edf30-124">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="edf30-124">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="edf30-125">Voornaam</span><span class="sxs-lookup"><span data-stu-id="edf30-125">firstName</span></span>|<span data-ttu-id="edf30-126">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="edf30-126">string</span></span>|<span data-ttu-id="edf30-127">De voornaam van de huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="edf30-127">First name of the current user.</span></span>|  
|<span data-ttu-id="edf30-128">Achternaam</span><span class="sxs-lookup"><span data-stu-id="edf30-128">lastName</span></span>|<span data-ttu-id="edf30-129">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="edf30-129">string</span></span>|<span data-ttu-id="edf30-130">De achternaam van de huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="edf30-130">Last name of the current user.</span></span>|  
|<span data-ttu-id="edf30-131">Bedrijfsnaam</span><span class="sxs-lookup"><span data-stu-id="edf30-131">companyName</span></span>|<span data-ttu-id="edf30-132">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="edf30-132">string</span></span>|<span data-ttu-id="edf30-133">De naam van het bedrijf van de huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="edf30-133">The company name of the current user.</span></span>|  
|<span data-ttu-id="edf30-134">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="edf30-134">addresserEmail</span></span>|<span data-ttu-id="edf30-135">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="edf30-135">string</span></span>|<span data-ttu-id="edf30-136">E-mailadres van de huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="edf30-136">Email address of the current user.</span></span>|  
|<span data-ttu-id="edf30-137">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="edf30-137">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="edf30-138">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="edf30-138">string</span></span>|<span data-ttu-id="edf30-139">Relatieve URL om analytics voor de huidige gebruiker weer te geven.</span><span class="sxs-lookup"><span data-stu-id="edf30-139">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="edf30-140">abonnementen</span><span class="sxs-lookup"><span data-stu-id="edf30-140">subscriptions</span></span>|<span data-ttu-id="edf30-141">Verzameling van [abonnement](api-management-template-data-model-reference.md#Subscription) entiteiten.</span><span class="sxs-lookup"><span data-stu-id="edf30-141">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="edf30-142">De abonnementen voor de huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="edf30-142">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="edf30-143">toepassingen</span><span class="sxs-lookup"><span data-stu-id="edf30-143">applications</span></span>|<span data-ttu-id="edf30-144">Verzameling van [toepassing](api-management-template-data-model-reference.md#Application) entiteiten.</span><span class="sxs-lookup"><span data-stu-id="edf30-144">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="edf30-145">De toepassingen van de huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="edf30-145">The applications of the current user.</span></span>|  
|<span data-ttu-id="edf30-146">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="edf30-146">changePasswordUrl</span></span>|<span data-ttu-id="edf30-147">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="edf30-147">string</span></span>|<span data-ttu-id="edf30-148">De relatieve URL van de huidige gebruiker-wachtwoord te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="edf30-148">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="edf30-149">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="edf30-149">changeNameOrEmailUrl</span></span>|<span data-ttu-id="edf30-150">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="edf30-150">string</span></span>|<span data-ttu-id="edf30-151">De relatieve URL moet de naam en e-mailadres voor de huidige gebruiker wijzigen.</span><span class="sxs-lookup"><span data-stu-id="edf30-151">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="edf30-152">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="edf30-152">canChangePassword</span></span>|<span data-ttu-id="edf30-153">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="edf30-153">boolean</span></span>|<span data-ttu-id="edf30-154">Hiermee wordt aangegeven of de huidige gebruiker hun wachtwoord kan wijzigen.</span><span class="sxs-lookup"><span data-stu-id="edf30-154">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="edf30-155">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="edf30-155">isSystemUser</span></span>|<span data-ttu-id="edf30-156">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="edf30-156">boolean</span></span>|<span data-ttu-id="edf30-157">Hiermee wordt aangegeven of de huidige gebruiker is lid van een van de ingebouwde [groepen](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="edf30-157">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="edf30-158">Voorbeeldgegevens voor sjabloon</span><span class="sxs-lookup"><span data-stu-id="edf30-158">Sample template data</span></span>  
  
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
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
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
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
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
  
##  <span data-ttu-id="edf30-159"><a name="Subscriptions"></a>Abonnementen</span><span class="sxs-lookup"><span data-stu-id="edf30-159"><a name="Subscriptions"></a> Subscriptions</span></span>  
 <span data-ttu-id="edf30-160">De **abonnementen** sjabloon kunt u het gedeelte Abonnementen van de pagina gebruikersprofiel in de ontwikkelaarsportal aanpassen.</span><span class="sxs-lookup"><span data-stu-id="edf30-160">The **Subscriptions** template allows you to customize the subscriptions section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="edf30-161">![Abonnement op de gebruikerspagina](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "APIM op de pagina gebruiker abonnement")</span><span class="sxs-lookup"><span data-stu-id="edf30-161">![User Subscription Page](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "APIM User Subscription Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="edf30-162">Standaardsjabloon</span><span class="sxs-lookup"><span data-stu-id="edf30-162">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="edf30-163">Besturingselementen</span><span class="sxs-lookup"><span data-stu-id="edf30-163">Controls</span></span>  
 <span data-ttu-id="edf30-164">Deze sjabloon kan gebruikt u de volgende [pagina besturingselementen](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="edf30-164">This template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="edf30-165">abonnement annuleren</span><span class="sxs-lookup"><span data-stu-id="edf30-165">subscription-cancel</span></span>](api-management-page-controls.md#subscription-cancel)  
  
### <a name="data-model"></a><span data-ttu-id="edf30-166">Gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="edf30-166">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="edf30-167">De [profiel](#Profile), [toepassingen](#Applications), en [abonnementen](#Subscriptions) sjablonen voor het gegevensmodel met dezelfde delen en ontvangen van dezelfde sjabloongegevens.</span><span class="sxs-lookup"><span data-stu-id="edf30-167">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="edf30-168">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="edf30-168">Property</span></span>|<span data-ttu-id="edf30-169">Type</span><span class="sxs-lookup"><span data-stu-id="edf30-169">Type</span></span>|<span data-ttu-id="edf30-170">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="edf30-170">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="edf30-171">Voornaam</span><span class="sxs-lookup"><span data-stu-id="edf30-171">firstName</span></span>|<span data-ttu-id="edf30-172">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="edf30-172">string</span></span>|<span data-ttu-id="edf30-173">De voornaam van de huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="edf30-173">First name of the current user.</span></span>|  
|<span data-ttu-id="edf30-174">Achternaam</span><span class="sxs-lookup"><span data-stu-id="edf30-174">lastName</span></span>|<span data-ttu-id="edf30-175">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="edf30-175">string</span></span>|<span data-ttu-id="edf30-176">De achternaam van de huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="edf30-176">Last name of the current user.</span></span>|  
|<span data-ttu-id="edf30-177">Bedrijfsnaam</span><span class="sxs-lookup"><span data-stu-id="edf30-177">companyName</span></span>|<span data-ttu-id="edf30-178">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="edf30-178">string</span></span>|<span data-ttu-id="edf30-179">De naam van het bedrijf van de huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="edf30-179">The company name of the current user.</span></span>|  
|<span data-ttu-id="edf30-180">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="edf30-180">addresserEmail</span></span>|<span data-ttu-id="edf30-181">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="edf30-181">string</span></span>|<span data-ttu-id="edf30-182">E-mailadres van de huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="edf30-182">Email address of the current user.</span></span>|  
|<span data-ttu-id="edf30-183">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="edf30-183">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="edf30-184">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="edf30-184">string</span></span>|<span data-ttu-id="edf30-185">Relatieve URL om analytics voor de huidige gebruiker weer te geven.</span><span class="sxs-lookup"><span data-stu-id="edf30-185">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="edf30-186">abonnementen</span><span class="sxs-lookup"><span data-stu-id="edf30-186">subscriptions</span></span>|<span data-ttu-id="edf30-187">Verzameling van [abonnement](api-management-template-data-model-reference.md#Subscription) entiteiten.</span><span class="sxs-lookup"><span data-stu-id="edf30-187">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="edf30-188">De abonnementen voor de huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="edf30-188">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="edf30-189">toepassingen</span><span class="sxs-lookup"><span data-stu-id="edf30-189">applications</span></span>|<span data-ttu-id="edf30-190">Verzameling van [toepassing](api-management-template-data-model-reference.md#Application) entiteiten.</span><span class="sxs-lookup"><span data-stu-id="edf30-190">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="edf30-191">De toepassingen van de huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="edf30-191">The applications of the current user.</span></span>|  
|<span data-ttu-id="edf30-192">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="edf30-192">changePasswordUrl</span></span>|<span data-ttu-id="edf30-193">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="edf30-193">string</span></span>|<span data-ttu-id="edf30-194">De relatieve URL van de huidige gebruiker-wachtwoord te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="edf30-194">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="edf30-195">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="edf30-195">changeNameOrEmailUrl</span></span>|<span data-ttu-id="edf30-196">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="edf30-196">string</span></span>|<span data-ttu-id="edf30-197">De relatieve URL moet de naam en e-mailadres voor de huidige gebruiker wijzigen.</span><span class="sxs-lookup"><span data-stu-id="edf30-197">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="edf30-198">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="edf30-198">canChangePassword</span></span>|<span data-ttu-id="edf30-199">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="edf30-199">boolean</span></span>|<span data-ttu-id="edf30-200">Hiermee wordt aangegeven of de huidige gebruiker hun wachtwoord kan wijzigen.</span><span class="sxs-lookup"><span data-stu-id="edf30-200">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="edf30-201">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="edf30-201">isSystemUser</span></span>|<span data-ttu-id="edf30-202">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="edf30-202">boolean</span></span>|<span data-ttu-id="edf30-203">Hiermee wordt aangegeven of de huidige gebruiker is lid van een van de ingebouwde [groepen](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="edf30-203">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="edf30-204">Voorbeeldgegevens voor sjabloon</span><span class="sxs-lookup"><span data-stu-id="edf30-204">Sample template data</span></span>  
  
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
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
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
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
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
  
##  <span data-ttu-id="edf30-205"><a name="Applications"></a>Toepassingen</span><span class="sxs-lookup"><span data-stu-id="edf30-205"><a name="Applications"></a> Applications</span></span>  
 <span data-ttu-id="edf30-206">De **toepassingen** sjabloon kunt u het gedeelte Abonnementen van de pagina gebruikersprofiel in de ontwikkelaarsportal aanpassen.</span><span class="sxs-lookup"><span data-stu-id="edf30-206">The **Applications** template allows you to customize the subscriptions section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="edf30-207">![Gebruiker toepassingen accountpagina](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "APIM gebruikersaccount pagina met toepassingen")</span><span class="sxs-lookup"><span data-stu-id="edf30-207">![User Account Applications Page](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "APIM User Account Applications Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="edf30-208">Standaardsjabloon</span><span class="sxs-lookup"><span data-stu-id="edf30-208">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="edf30-209">Besturingselementen</span><span class="sxs-lookup"><span data-stu-id="edf30-209">Controls</span></span>  
 <span data-ttu-id="edf30-210">Deze sjabloon kan gebruikt u de volgende [pagina besturingselementen](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="edf30-210">This template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="edf30-211">App-acties</span><span class="sxs-lookup"><span data-stu-id="edf30-211">app-actions</span></span>](api-management-page-controls.md#app-actions)  
  
### <a name="data-model"></a><span data-ttu-id="edf30-212">Gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="edf30-212">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="edf30-213">De [profiel](#Profile), [toepassingen](#Applications), en [abonnementen](#Subscriptions) sjablonen voor het gegevensmodel met dezelfde delen en ontvangen van dezelfde sjabloongegevens.</span><span class="sxs-lookup"><span data-stu-id="edf30-213">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="edf30-214">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="edf30-214">Property</span></span>|<span data-ttu-id="edf30-215">Type</span><span class="sxs-lookup"><span data-stu-id="edf30-215">Type</span></span>|<span data-ttu-id="edf30-216">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="edf30-216">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="edf30-217">Voornaam</span><span class="sxs-lookup"><span data-stu-id="edf30-217">firstName</span></span>|<span data-ttu-id="edf30-218">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="edf30-218">string</span></span>|<span data-ttu-id="edf30-219">De voornaam van de huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="edf30-219">First name of the current user.</span></span>|  
|<span data-ttu-id="edf30-220">Achternaam</span><span class="sxs-lookup"><span data-stu-id="edf30-220">lastName</span></span>|<span data-ttu-id="edf30-221">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="edf30-221">string</span></span>|<span data-ttu-id="edf30-222">De achternaam van de huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="edf30-222">Last name of the current user.</span></span>|  
|<span data-ttu-id="edf30-223">Bedrijfsnaam</span><span class="sxs-lookup"><span data-stu-id="edf30-223">companyName</span></span>|<span data-ttu-id="edf30-224">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="edf30-224">string</span></span>|<span data-ttu-id="edf30-225">De naam van het bedrijf van de huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="edf30-225">The company name of the current user.</span></span>|  
|<span data-ttu-id="edf30-226">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="edf30-226">addresserEmail</span></span>|<span data-ttu-id="edf30-227">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="edf30-227">string</span></span>|<span data-ttu-id="edf30-228">E-mailadres van de huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="edf30-228">Email address of the current user.</span></span>|  
|<span data-ttu-id="edf30-229">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="edf30-229">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="edf30-230">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="edf30-230">string</span></span>|<span data-ttu-id="edf30-231">Relatieve URL om analytics voor de huidige gebruiker weer te geven.</span><span class="sxs-lookup"><span data-stu-id="edf30-231">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="edf30-232">abonnementen</span><span class="sxs-lookup"><span data-stu-id="edf30-232">subscriptions</span></span>|<span data-ttu-id="edf30-233">Verzameling van [abonnement](api-management-template-data-model-reference.md#Subscription) entiteiten.</span><span class="sxs-lookup"><span data-stu-id="edf30-233">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="edf30-234">De abonnementen voor de huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="edf30-234">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="edf30-235">toepassingen</span><span class="sxs-lookup"><span data-stu-id="edf30-235">applications</span></span>|<span data-ttu-id="edf30-236">Verzameling van [toepassing](api-management-template-data-model-reference.md#Application) entiteiten.</span><span class="sxs-lookup"><span data-stu-id="edf30-236">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="edf30-237">De toepassingen van de huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="edf30-237">The applications of the current user.</span></span>|  
|<span data-ttu-id="edf30-238">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="edf30-238">changePasswordUrl</span></span>|<span data-ttu-id="edf30-239">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="edf30-239">string</span></span>|<span data-ttu-id="edf30-240">De relatieve URL van de huidige gebruiker-wachtwoord te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="edf30-240">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="edf30-241">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="edf30-241">changeNameOrEmailUrl</span></span>|<span data-ttu-id="edf30-242">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="edf30-242">string</span></span>|<span data-ttu-id="edf30-243">De relatieve URL moet de naam en e-mailadres voor de huidige gebruiker wijzigen.</span><span class="sxs-lookup"><span data-stu-id="edf30-243">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="edf30-244">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="edf30-244">canChangePassword</span></span>|<span data-ttu-id="edf30-245">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="edf30-245">boolean</span></span>|<span data-ttu-id="edf30-246">Hiermee wordt aangegeven of de huidige gebruiker hun wachtwoord kan wijzigen.</span><span class="sxs-lookup"><span data-stu-id="edf30-246">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="edf30-247">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="edf30-247">isSystemUser</span></span>|<span data-ttu-id="edf30-248">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="edf30-248">boolean</span></span>|<span data-ttu-id="edf30-249">Hiermee wordt aangegeven of de huidige gebruiker is lid van een van de ingebouwde [groepen](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="edf30-249">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="edf30-250">Voorbeeldgegevens voor sjabloon</span><span class="sxs-lookup"><span data-stu-id="edf30-250">Sample template data</span></span>  
  
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
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
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
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
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
  
##  <span data-ttu-id="edf30-251"><a name="UpdateAccountInfo"></a>Update-accountgegevens</span><span class="sxs-lookup"><span data-stu-id="edf30-251"><a name="UpdateAccountInfo"></a> Update account info</span></span>  
 <span data-ttu-id="edf30-252">De **Uodate accountgegevens** sjabloon kunt u voor het aanpassen van de **accountgegevens bijwerken** pagina in de portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="edf30-252">The **Uodate account info** template allows you to customize the **Update account information** page in the developer portal.</span></span>  
  
 <span data-ttu-id="edf30-253">![Info pagina Developer Portal sjablonen voor gebruikersaccounts](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "APIM Info pagina Developer Portal sjablonen voor gebruikersaccounts")</span><span class="sxs-lookup"><span data-stu-id="edf30-253">![User Account Info Page Developer Portal Templates](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "APIM User Account Info Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="edf30-254">Standaardsjabloon</span><span class="sxs-lookup"><span data-stu-id="edf30-254">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="edf30-255">Besturingselementen</span><span class="sxs-lookup"><span data-stu-id="edf30-255">Controls</span></span>  
 <span data-ttu-id="edf30-256">Deze sjabloon kan geen gebruik [pagina besturingselementen](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="edf30-256">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="edf30-257">Gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="edf30-257">Data model</span></span>  
 <span data-ttu-id="edf30-258">[Gebruikersaccountgegevens](api-management-template-data-model-reference.md#UserAccountInfo) entiteit.</span><span class="sxs-lookup"><span data-stu-id="edf30-258">[User account info](api-management-template-data-model-reference.md#UserAccountInfo) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="edf30-259">Voorbeeldgegevens voor sjabloon</span><span class="sxs-lookup"><span data-stu-id="edf30-259">Sample template data</span></span>  
  
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

## <a name="next-steps"></a><span data-ttu-id="edf30-260">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="edf30-260">Next steps</span></span>
<span data-ttu-id="edf30-261">Zie voor meer informatie over het werken met sjablonen [het aanpassen van de API Management portal voor ontwikkelaars met behulp van sjablonen](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="edf30-261">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>