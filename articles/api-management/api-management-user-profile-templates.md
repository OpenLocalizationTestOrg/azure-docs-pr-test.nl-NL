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
# <a name="user-profile-templates-in-azure-api-management"></a><span data-ttu-id="4d8d9-103">Gebruiker profielsjablonen in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="4d8d9-103">User profile templates in Azure API Management</span></span>
<span data-ttu-id="4d8d9-104">Azure API Management biedt dat u Hallo mogelijkheid toocustomize Hallo inhoud van developer portal-pagina's met behulp van een set van sjablonen die hun inhoud configureren.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="4d8d9-105">Met behulp van [DotLiquid](http://dotliquidmarkup.org/) syntaxis en het Hallo-editor naar keuze, zoals [DotLiquid voor ontwerpers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), en een opgegeven set gelokaliseerde [resources String](api-management-template-resources.md#strings), [ De glyph-resources](api-management-template-resources.md#glyphs), en [pagina besturingselementen](api-management-page-controls.md), hebt u aanzienlijke flexibiliteit tooconfigure Hallo inhoud van het Hallo-pagina's naar wens met behulp van deze sjablonen.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="4d8d9-106">Hallo-sjablonen in deze sectie kunt u toocustomize Hallo inhoud van Hallo gebruiker profiel's in Hallo-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-106">hello templates in this section allow you toocustomize hello content of hello User profile pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="4d8d9-107">Profiel</span><span class="sxs-lookup"><span data-stu-id="4d8d9-107">Profile</span></span>](#Profile)  
  
-   [<span data-ttu-id="4d8d9-108">Abonnementen</span><span class="sxs-lookup"><span data-stu-id="4d8d9-108">Subscriptions</span></span>](#Subscriptions)  
  
-   [<span data-ttu-id="4d8d9-109">Toepassingen</span><span class="sxs-lookup"><span data-stu-id="4d8d9-109">Applications</span></span>](#Applications)  
  
-   [<span data-ttu-id="4d8d9-110">Update-accountgegevens</span><span class="sxs-lookup"><span data-stu-id="4d8d9-110">Update account info</span></span>](#UpdateAccountInfo)  
  
> [!NOTE]
>  <span data-ttu-id="4d8d9-111">Standaard-voorbeeldsjablonen zijn opgenomen in de volgende documentatie Hallo, maar onderwerp toochange vanwege toocontinuous verbeteringen zijn.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-111">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="4d8d9-112">U kunt Hallo live standaardsjablonen in Hallo developer-portal door te navigeren toohello gewenst afzonderlijke sjablonen weergeven.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-112">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="4d8d9-113">Zie voor meer informatie over het werken met sjablonen [hoe toocustomize API Management-portal voor ontwikkelaars met behulp van sjablonen Hallo](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="4d8d9-113">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="4d8d9-114"><a name="Profile"></a>Profiel</span><span class="sxs-lookup"><span data-stu-id="4d8d9-114"><a name="Profile"></a> Profile</span></span>  
 <span data-ttu-id="4d8d9-115">Hallo **profiel** sjabloon kunt u toocustomize Hallo Gebruikersprofielsectie Hallo van profielpagina van gebruiker in Hallo-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-115">hello **profile** template allows you toocustomize hello user profile section of hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="4d8d9-116">![Pagina gebruikersprofiel](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "APIM gebruikersprofiel pagina")</span><span class="sxs-lookup"><span data-stu-id="4d8d9-116">![User Profile Page](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "APIM User Profile Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="4d8d9-117">Standaardsjabloon</span><span class="sxs-lookup"><span data-stu-id="4d8d9-117">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="4d8d9-118">Besturingselementen</span><span class="sxs-lookup"><span data-stu-id="4d8d9-118">Controls</span></span>  
 <span data-ttu-id="4d8d9-119">Deze sjabloon kan geen gebruik [pagina besturingselementen](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="4d8d9-119">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="4d8d9-120">Gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="4d8d9-120">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="4d8d9-121">Hallo [profiel](#Profile), [toepassingen](#Applications), en [abonnementen](#Subscriptions) sjablonen Hallo dezelfde gegevens modelleren en Hallo ontvangen delen dezelfde sjabloongegevens.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-121">hello [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share hello same data model and receive hello same template data.</span></span>  
  
|<span data-ttu-id="4d8d9-122">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4d8d9-122">Property</span></span>|<span data-ttu-id="4d8d9-123">Type</span><span class="sxs-lookup"><span data-stu-id="4d8d9-123">Type</span></span>|<span data-ttu-id="4d8d9-124">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4d8d9-124">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="4d8d9-125">Voornaam</span><span class="sxs-lookup"><span data-stu-id="4d8d9-125">firstName</span></span>|<span data-ttu-id="4d8d9-126">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d8d9-126">string</span></span>|<span data-ttu-id="4d8d9-127">De voornaam van de huidige gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-127">First name of hello current user.</span></span>|  
|<span data-ttu-id="4d8d9-128">Achternaam</span><span class="sxs-lookup"><span data-stu-id="4d8d9-128">lastName</span></span>|<span data-ttu-id="4d8d9-129">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d8d9-129">string</span></span>|<span data-ttu-id="4d8d9-130">De achternaam van de huidige gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-130">Last name of hello current user.</span></span>|  
|<span data-ttu-id="4d8d9-131">Bedrijfsnaam</span><span class="sxs-lookup"><span data-stu-id="4d8d9-131">companyName</span></span>|<span data-ttu-id="4d8d9-132">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d8d9-132">string</span></span>|<span data-ttu-id="4d8d9-133">bedrijfsnaam van de huidige gebruiker Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-133">hello company name of hello current user.</span></span>|  
|<span data-ttu-id="4d8d9-134">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="4d8d9-134">addresserEmail</span></span>|<span data-ttu-id="4d8d9-135">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d8d9-135">string</span></span>|<span data-ttu-id="4d8d9-136">E-mailadres van de huidige gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-136">Email address of hello current user.</span></span>|  
|<span data-ttu-id="4d8d9-137">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="4d8d9-137">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="4d8d9-138">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d8d9-138">string</span></span>|<span data-ttu-id="4d8d9-139">Relatieve URL tooview analytics voor de huidige gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-139">Relative URL tooview analytics for hello current user.</span></span>|  
|<span data-ttu-id="4d8d9-140">abonnementen</span><span class="sxs-lookup"><span data-stu-id="4d8d9-140">subscriptions</span></span>|<span data-ttu-id="4d8d9-141">Verzameling van [abonnement](api-management-template-data-model-reference.md#Subscription) entiteiten.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-141">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="4d8d9-142">Hallo-abonnementen voor de huidige gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-142">hello subscriptions for hello current user.</span></span>|  
|<span data-ttu-id="4d8d9-143">toepassingen</span><span class="sxs-lookup"><span data-stu-id="4d8d9-143">applications</span></span>|<span data-ttu-id="4d8d9-144">Verzameling van [toepassing](api-management-template-data-model-reference.md#Application) entiteiten.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-144">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="4d8d9-145">Hallo-toepassingen van de huidige gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-145">hello applications of hello current user.</span></span>|  
|<span data-ttu-id="4d8d9-146">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="4d8d9-146">changePasswordUrl</span></span>|<span data-ttu-id="4d8d9-147">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d8d9-147">string</span></span>|<span data-ttu-id="4d8d9-148">Hallo relatieve URL toochange Hallo huidige wachtwoord van gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-148">hello relative URL toochange hello current user's password.</span></span>|  
|<span data-ttu-id="4d8d9-149">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="4d8d9-149">changeNameOrEmailUrl</span></span>|<span data-ttu-id="4d8d9-150">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d8d9-150">string</span></span>|<span data-ttu-id="4d8d9-151">relatieve URL toochange Hallo-naam en e-mailadres voor de huidige gebruiker Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-151">hello relative URL toochange hello name and email for hello current user.</span></span>|  
|<span data-ttu-id="4d8d9-152">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="4d8d9-152">canChangePassword</span></span>|<span data-ttu-id="4d8d9-153">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="4d8d9-153">boolean</span></span>|<span data-ttu-id="4d8d9-154">Hiermee wordt aangegeven of kan de huidige gebruiker Hallo hun wachtwoord wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-154">Whether hello current user can change their password.</span></span>|  
|<span data-ttu-id="4d8d9-155">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="4d8d9-155">isSystemUser</span></span>|<span data-ttu-id="4d8d9-156">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="4d8d9-156">boolean</span></span>|<span data-ttu-id="4d8d9-157">Of Hallo-huidige gebruiker lid is van een van de ingebouwde Hallo [groepen](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="4d8d9-157">Whether hello current user is a member of one of hello built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="4d8d9-158">Voorbeeldgegevens voor sjabloon</span><span class="sxs-lookup"><span data-stu-id="4d8d9-158">Sample template data</span></span>  
  
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
  
##  <span data-ttu-id="4d8d9-159"><a name="Subscriptions"></a>Abonnementen</span><span class="sxs-lookup"><span data-stu-id="4d8d9-159"><a name="Subscriptions"></a> Subscriptions</span></span>  
 <span data-ttu-id="4d8d9-160">Hallo **abonnementen** sjabloon kunt u toocustomize Hallo abonnementen sectie van Hallo pagina gebruikersprofiel in Hallo-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-160">hello **Subscriptions** template allows you toocustomize hello subscriptions section of hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="4d8d9-161">![Abonnement op de gebruikerspagina](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "APIM op de pagina gebruiker abonnement")</span><span class="sxs-lookup"><span data-stu-id="4d8d9-161">![User Subscription Page](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "APIM User Subscription Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="4d8d9-162">Standaardsjabloon</span><span class="sxs-lookup"><span data-stu-id="4d8d9-162">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="4d8d9-163">Besturingselementen</span><span class="sxs-lookup"><span data-stu-id="4d8d9-163">Controls</span></span>  
 <span data-ttu-id="4d8d9-164">Deze sjabloon kunt Hallo volgende [pagina besturingselementen](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="4d8d9-164">This template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="4d8d9-165">abonnement annuleren</span><span class="sxs-lookup"><span data-stu-id="4d8d9-165">subscription-cancel</span></span>](api-management-page-controls.md#subscription-cancel)  
  
### <a name="data-model"></a><span data-ttu-id="4d8d9-166">Gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="4d8d9-166">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="4d8d9-167">Hallo [profiel](#Profile), [toepassingen](#Applications), en [abonnementen](#Subscriptions) sjablonen Hallo dezelfde gegevens modelleren en Hallo ontvangen delen dezelfde sjabloongegevens.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-167">hello [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share hello same data model and receive hello same template data.</span></span>  
  
|<span data-ttu-id="4d8d9-168">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4d8d9-168">Property</span></span>|<span data-ttu-id="4d8d9-169">Type</span><span class="sxs-lookup"><span data-stu-id="4d8d9-169">Type</span></span>|<span data-ttu-id="4d8d9-170">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4d8d9-170">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="4d8d9-171">Voornaam</span><span class="sxs-lookup"><span data-stu-id="4d8d9-171">firstName</span></span>|<span data-ttu-id="4d8d9-172">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d8d9-172">string</span></span>|<span data-ttu-id="4d8d9-173">De voornaam van de huidige gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-173">First name of hello current user.</span></span>|  
|<span data-ttu-id="4d8d9-174">Achternaam</span><span class="sxs-lookup"><span data-stu-id="4d8d9-174">lastName</span></span>|<span data-ttu-id="4d8d9-175">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d8d9-175">string</span></span>|<span data-ttu-id="4d8d9-176">De achternaam van de huidige gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-176">Last name of hello current user.</span></span>|  
|<span data-ttu-id="4d8d9-177">Bedrijfsnaam</span><span class="sxs-lookup"><span data-stu-id="4d8d9-177">companyName</span></span>|<span data-ttu-id="4d8d9-178">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d8d9-178">string</span></span>|<span data-ttu-id="4d8d9-179">bedrijfsnaam van de huidige gebruiker Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-179">hello company name of hello current user.</span></span>|  
|<span data-ttu-id="4d8d9-180">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="4d8d9-180">addresserEmail</span></span>|<span data-ttu-id="4d8d9-181">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d8d9-181">string</span></span>|<span data-ttu-id="4d8d9-182">E-mailadres van de huidige gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-182">Email address of hello current user.</span></span>|  
|<span data-ttu-id="4d8d9-183">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="4d8d9-183">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="4d8d9-184">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d8d9-184">string</span></span>|<span data-ttu-id="4d8d9-185">Relatieve URL tooview analytics voor de huidige gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-185">Relative URL tooview analytics for hello current user.</span></span>|  
|<span data-ttu-id="4d8d9-186">abonnementen</span><span class="sxs-lookup"><span data-stu-id="4d8d9-186">subscriptions</span></span>|<span data-ttu-id="4d8d9-187">Verzameling van [abonnement](api-management-template-data-model-reference.md#Subscription) entiteiten.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-187">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="4d8d9-188">Hallo-abonnementen voor de huidige gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-188">hello subscriptions for hello current user.</span></span>|  
|<span data-ttu-id="4d8d9-189">toepassingen</span><span class="sxs-lookup"><span data-stu-id="4d8d9-189">applications</span></span>|<span data-ttu-id="4d8d9-190">Verzameling van [toepassing](api-management-template-data-model-reference.md#Application) entiteiten.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-190">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="4d8d9-191">Hallo-toepassingen van de huidige gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-191">hello applications of hello current user.</span></span>|  
|<span data-ttu-id="4d8d9-192">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="4d8d9-192">changePasswordUrl</span></span>|<span data-ttu-id="4d8d9-193">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d8d9-193">string</span></span>|<span data-ttu-id="4d8d9-194">Hallo relatieve URL toochange Hallo huidige wachtwoord van gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-194">hello relative URL toochange hello current user's password.</span></span>|  
|<span data-ttu-id="4d8d9-195">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="4d8d9-195">changeNameOrEmailUrl</span></span>|<span data-ttu-id="4d8d9-196">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d8d9-196">string</span></span>|<span data-ttu-id="4d8d9-197">relatieve URL toochange Hallo-naam en e-mailadres voor de huidige gebruiker Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-197">hello relative URL toochange hello name and email for hello current user.</span></span>|  
|<span data-ttu-id="4d8d9-198">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="4d8d9-198">canChangePassword</span></span>|<span data-ttu-id="4d8d9-199">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="4d8d9-199">boolean</span></span>|<span data-ttu-id="4d8d9-200">Hiermee wordt aangegeven of kan de huidige gebruiker Hallo hun wachtwoord wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-200">Whether hello current user can change their password.</span></span>|  
|<span data-ttu-id="4d8d9-201">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="4d8d9-201">isSystemUser</span></span>|<span data-ttu-id="4d8d9-202">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="4d8d9-202">boolean</span></span>|<span data-ttu-id="4d8d9-203">Of Hallo-huidige gebruiker lid is van een van de ingebouwde Hallo [groepen](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="4d8d9-203">Whether hello current user is a member of one of hello built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="4d8d9-204">Voorbeeldgegevens voor sjabloon</span><span class="sxs-lookup"><span data-stu-id="4d8d9-204">Sample template data</span></span>  
  
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
  
##  <span data-ttu-id="4d8d9-205"><a name="Applications"></a>Toepassingen</span><span class="sxs-lookup"><span data-stu-id="4d8d9-205"><a name="Applications"></a> Applications</span></span>  
 <span data-ttu-id="4d8d9-206">Hallo **toepassingen** sjabloon kunt u toocustomize Hallo abonnementen sectie van Hallo pagina gebruikersprofiel in Hallo-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-206">hello **Applications** template allows you toocustomize hello subscriptions section of hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="4d8d9-207">![Gebruiker toepassingen accountpagina](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "APIM gebruikersaccount pagina met toepassingen")</span><span class="sxs-lookup"><span data-stu-id="4d8d9-207">![User Account Applications Page](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "APIM User Account Applications Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="4d8d9-208">Standaardsjabloon</span><span class="sxs-lookup"><span data-stu-id="4d8d9-208">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="4d8d9-209">Besturingselementen</span><span class="sxs-lookup"><span data-stu-id="4d8d9-209">Controls</span></span>  
 <span data-ttu-id="4d8d9-210">Deze sjabloon kunt Hallo volgende [pagina besturingselementen](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="4d8d9-210">This template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="4d8d9-211">App-acties</span><span class="sxs-lookup"><span data-stu-id="4d8d9-211">app-actions</span></span>](api-management-page-controls.md#app-actions)  
  
### <a name="data-model"></a><span data-ttu-id="4d8d9-212">Gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="4d8d9-212">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="4d8d9-213">Hallo [profiel](#Profile), [toepassingen](#Applications), en [abonnementen](#Subscriptions) sjablonen Hallo dezelfde gegevens modelleren en Hallo ontvangen delen dezelfde sjabloongegevens.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-213">hello [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share hello same data model and receive hello same template data.</span></span>  
  
|<span data-ttu-id="4d8d9-214">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4d8d9-214">Property</span></span>|<span data-ttu-id="4d8d9-215">Type</span><span class="sxs-lookup"><span data-stu-id="4d8d9-215">Type</span></span>|<span data-ttu-id="4d8d9-216">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4d8d9-216">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="4d8d9-217">Voornaam</span><span class="sxs-lookup"><span data-stu-id="4d8d9-217">firstName</span></span>|<span data-ttu-id="4d8d9-218">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d8d9-218">string</span></span>|<span data-ttu-id="4d8d9-219">De voornaam van de huidige gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-219">First name of hello current user.</span></span>|  
|<span data-ttu-id="4d8d9-220">Achternaam</span><span class="sxs-lookup"><span data-stu-id="4d8d9-220">lastName</span></span>|<span data-ttu-id="4d8d9-221">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d8d9-221">string</span></span>|<span data-ttu-id="4d8d9-222">De achternaam van de huidige gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-222">Last name of hello current user.</span></span>|  
|<span data-ttu-id="4d8d9-223">Bedrijfsnaam</span><span class="sxs-lookup"><span data-stu-id="4d8d9-223">companyName</span></span>|<span data-ttu-id="4d8d9-224">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d8d9-224">string</span></span>|<span data-ttu-id="4d8d9-225">bedrijfsnaam van de huidige gebruiker Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-225">hello company name of hello current user.</span></span>|  
|<span data-ttu-id="4d8d9-226">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="4d8d9-226">addresserEmail</span></span>|<span data-ttu-id="4d8d9-227">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d8d9-227">string</span></span>|<span data-ttu-id="4d8d9-228">E-mailadres van de huidige gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-228">Email address of hello current user.</span></span>|  
|<span data-ttu-id="4d8d9-229">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="4d8d9-229">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="4d8d9-230">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d8d9-230">string</span></span>|<span data-ttu-id="4d8d9-231">Relatieve URL tooview analytics voor de huidige gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-231">Relative URL tooview analytics for hello current user.</span></span>|  
|<span data-ttu-id="4d8d9-232">abonnementen</span><span class="sxs-lookup"><span data-stu-id="4d8d9-232">subscriptions</span></span>|<span data-ttu-id="4d8d9-233">Verzameling van [abonnement](api-management-template-data-model-reference.md#Subscription) entiteiten.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-233">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="4d8d9-234">Hallo-abonnementen voor de huidige gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-234">hello subscriptions for hello current user.</span></span>|  
|<span data-ttu-id="4d8d9-235">toepassingen</span><span class="sxs-lookup"><span data-stu-id="4d8d9-235">applications</span></span>|<span data-ttu-id="4d8d9-236">Verzameling van [toepassing](api-management-template-data-model-reference.md#Application) entiteiten.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-236">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="4d8d9-237">Hallo-toepassingen van de huidige gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-237">hello applications of hello current user.</span></span>|  
|<span data-ttu-id="4d8d9-238">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="4d8d9-238">changePasswordUrl</span></span>|<span data-ttu-id="4d8d9-239">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d8d9-239">string</span></span>|<span data-ttu-id="4d8d9-240">Hallo relatieve URL toochange Hallo huidige wachtwoord van gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-240">hello relative URL toochange hello current user's password.</span></span>|  
|<span data-ttu-id="4d8d9-241">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="4d8d9-241">changeNameOrEmailUrl</span></span>|<span data-ttu-id="4d8d9-242">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d8d9-242">string</span></span>|<span data-ttu-id="4d8d9-243">relatieve URL toochange Hallo-naam en e-mailadres voor de huidige gebruiker Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-243">hello relative URL toochange hello name and email for hello current user.</span></span>|  
|<span data-ttu-id="4d8d9-244">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="4d8d9-244">canChangePassword</span></span>|<span data-ttu-id="4d8d9-245">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="4d8d9-245">boolean</span></span>|<span data-ttu-id="4d8d9-246">Hiermee wordt aangegeven of kan de huidige gebruiker Hallo hun wachtwoord wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-246">Whether hello current user can change their password.</span></span>|  
|<span data-ttu-id="4d8d9-247">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="4d8d9-247">isSystemUser</span></span>|<span data-ttu-id="4d8d9-248">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="4d8d9-248">boolean</span></span>|<span data-ttu-id="4d8d9-249">Of Hallo-huidige gebruiker lid is van een van de ingebouwde Hallo [groepen](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="4d8d9-249">Whether hello current user is a member of one of hello built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="4d8d9-250">Voorbeeldgegevens voor sjabloon</span><span class="sxs-lookup"><span data-stu-id="4d8d9-250">Sample template data</span></span>  
  
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
  
##  <span data-ttu-id="4d8d9-251"><a name="UpdateAccountInfo"></a>Update-accountgegevens</span><span class="sxs-lookup"><span data-stu-id="4d8d9-251"><a name="UpdateAccountInfo"></a> Update account info</span></span>  
 <span data-ttu-id="4d8d9-252">Hallo **Uodate accountgegevens** sjabloon kunt u toocustomize hello **accountgegevens bijwerken** pagina in het Hallo-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-252">hello **Uodate account info** template allows you toocustomize hello **Update account information** page in hello developer portal.</span></span>  
  
 <span data-ttu-id="4d8d9-253">![Info pagina Developer Portal sjablonen voor gebruikersaccounts](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "APIM Info pagina Developer Portal sjablonen voor gebruikersaccounts")</span><span class="sxs-lookup"><span data-stu-id="4d8d9-253">![User Account Info Page Developer Portal Templates](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "APIM User Account Info Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="4d8d9-254">Standaardsjabloon</span><span class="sxs-lookup"><span data-stu-id="4d8d9-254">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="4d8d9-255">Besturingselementen</span><span class="sxs-lookup"><span data-stu-id="4d8d9-255">Controls</span></span>  
 <span data-ttu-id="4d8d9-256">Deze sjabloon kan geen gebruik [pagina besturingselementen](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="4d8d9-256">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="4d8d9-257">Gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="4d8d9-257">Data model</span></span>  
 <span data-ttu-id="4d8d9-258">[Gebruikersaccountgegevens](api-management-template-data-model-reference.md#UserAccountInfo) entiteit.</span><span class="sxs-lookup"><span data-stu-id="4d8d9-258">[User account info](api-management-template-data-model-reference.md#UserAccountInfo) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="4d8d9-259">Voorbeeldgegevens voor sjabloon</span><span class="sxs-lookup"><span data-stu-id="4d8d9-259">Sample template data</span></span>  
  
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

## <a name="next-steps"></a><span data-ttu-id="4d8d9-260">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4d8d9-260">Next steps</span></span>
<span data-ttu-id="4d8d9-261">Zie voor meer informatie over het werken met sjablonen [hoe toocustomize API Management-portal voor ontwikkelaars met behulp van sjablonen Hallo](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="4d8d9-261">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
