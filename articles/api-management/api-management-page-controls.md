---
title: aaaAzure API Management paginabesturingselementen | Microsoft Docs
description: Meer informatie over Hallo paginabesturingselementen beschikbaar voor gebruik in developer portal sjablonen in Azure API Management.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 03e0ac8d-64ff-4e9a-b029-d7be14fb31e3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 1a16a6fce197c0a2e14807ac21e81a9a73b515b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-page-controls"></a>Azure API Management-paginabesturingselementen
Azure API Management biedt Hallo besturingselementen voor gebruik in Hallo developer portal sjablonen te volgen.  
  
 toouse een besturingselement op Hallo gewenste locatie plaatst in Hallo developer portal sjabloon. Sommige besturingselementen, zoals Hallo [acties voor app](#app-actions) bepalen, parameters hebben, zoals wordt weergegeven in Hallo voorbeeld te volgen.  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 Hallo-waarden voor Hallo parameters worden doorgegeven in als onderdeel van het gegevensmodel Hallo voor Hallo-sjabloon. In de meeste gevallen kunt u gewoon plakken Hallo opgegeven voorbeeld voor elk besturingselement voor het toowork correct. U ziet voor meer informatie over de parameterwaarden Hallo Hallo gegevenssectie model voor elke sjabloon waarin een besturingselement kan worden gebruikt.  
  
 Zie voor meer informatie over het werken met sjablonen [hoe toocustomize API Management-portal voor ontwikkelaars met behulp van sjablonen Hallo](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
## <a name="developer-portal-template-page-controls"></a>Paginabesturingselementen voor ontwikkelaars sjabloon  
  
-   [App-acties](#app-actions)  
  
-   [Basic-aanmelding](#basic-signin)  
  
-   [besturingselement voor paginering](#paging-control)  
  
-   [providers](#providers)  
  
-   [besturingselement voor zoeken](#search-control)  
  
-   [aanmelden](#sign-up)  
  
-   [abonneren knop](#subscribe-button)  
  
-   [abonnement annuleren](#subscription-cancel)  
  
##  <a name="app-actions"></a>App-acties  
 Hallo `app-actions` beheer biedt een gebruikersinterface voor interactie met toepassingen op Hallo pagina gebruikersprofiel in Hallo-portal voor ontwikkelaars.  
  
 ![App- &#45; acties besturingselement](./media/api-management-page-controls/APIM-app-actions-control.png "APIM acties voor app beheer")  
  
### <a name="usage"></a>Gebruik  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a>Parameters  
  
|Parameter|Beschrijving|  
|---------------|-----------------|  
|AppId|Hallo-id van de toepassing hello.|  
  
### <a name="developer-portal-templates"></a>Developer portal-sjablonen  
 Hallo `app-actions` besturingselement kan worden gebruikt in Hallo developer portal-sjablonen te volgen.  
  
-   [Toepassingen](api-management-user-profile-templates.md#Applications)  
  
##  <a name="basic-signin"></a>Basic-aanmelding  
 Hallo `basic-signin` beheer biedt een controle voor verzamelen gebruiker aanmelden informatie in Hallo pagina in de ontwikkelaarsportal Hallo aanmelden.  
  
 ![Basic &#45; signin-besturingselement](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic signin-besturingselement")  
  
### <a name="usage"></a>Gebruik  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a>Parameters  
 Geen.  
  
### <a name="developer-portal-templates"></a>Developer portal-sjablonen  
 Hallo `basic-signin` besturingselement kan worden gebruikt in Hallo developer portal-sjablonen te volgen.  
  
-   [Aanmelden](api-management-page-templates.md#SignIn)  
  
##  <a name="paging-control"></a>besturingselement voor paginering  
 Hallo `paging-control` biedt pagineringsfunctionaliteit moet worden ingeschakeld op developer portal-pagina's die een lijst met items weergeven.  
  
 ![besturingselement van het wisselbestand](./media/api-management-page-controls/APIM-paging-control.png "APIM paginering besturingselement")  
  
### <a name="usage"></a>Gebruik  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a>Parameters  
 Geen.  
  
### <a name="developer-portal-templates"></a>Developer portal-sjablonen  
 Hallo `paging-control` besturingselement kan worden gebruikt in Hallo developer portal-sjablonen te volgen.  
  
-   [API-lijst](api-management-api-templates.md#APIList)  
  
-   [Lijst met kwesties](api-management-issue-templates.md#IssueList)  
  
-   [Lijst met producten](api-management-product-templates.md#ProductList)  
  
##  <a name="providers"></a>providers  
 Hallo `providers` beheer biedt een controle voor selectie van verificatieproviders in Hallo aanmeldingspagina in Hallo-portal voor ontwikkelaars.  
  
 ![providers besturingselement](./media/api-management-page-controls/APIM-providers-control.png "APIM providers besturingselement")  
  
### <a name="usage"></a>Gebruik  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a>Parameters  
 Geen.  
  
### <a name="developer-portal-templates"></a>Developer portal-sjablonen  
 Hallo `providers` besturingselement kan worden gebruikt in Hallo developer portal-sjablonen te volgen.  
  
-   [Aanmelden](api-management-page-templates.md#SignIn)  
  
##  <a name="search-control"></a>besturingselement voor zoeken  
 Hallo `search-control` biedt functionaliteit voor het zoeken op developer portal-pagina's die een lijst met items weergeven.  
  
 ![besturingselement zoeken](./media/api-management-page-controls/APIM-search-control.png "APIM zoekbesturing")  
  
### <a name="usage"></a>Gebruik  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a>Parameters  
 Geen.  
  
### <a name="developer-portal-templates"></a>Developer portal-sjablonen  
 Hallo `search-control` besturingselement kan worden gebruikt in Hallo developer portal-sjablonen te volgen.  
  
-   [API-lijst](api-management-api-templates.md#APIList)  
  
-   [Lijst met producten](api-management-product-templates.md#ProductList)  
  
##  <a name="sign-up"></a>aanmelden  
 Hallo `sign-up` control biedt een besturingselement voor het verzamelen van gebruikersprofielgegevens in Hallo registratiepagina in Hallo-portal voor ontwikkelaars.  
  
 ![aanmelding &#45; besturingselement up](./media/api-management-page-controls/APIM-sign-up-control.png "APIM aanmelding besturingselement")  
  
### <a name="usage"></a>Gebruik  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a>Parameters  
 Geen.  
  
### <a name="developer-portal-templates"></a>Developer portal-sjablonen  
 Hallo `sign-up` besturingselement kan worden gebruikt in Hallo developer portal-sjablonen te volgen.  
  
-   [Aanmelden](api-management-page-templates.md#SignUp)  
  
##  <a name="subscribe-button"></a>abonneren knop  
 Hallo `subscribe-button` biedt een controle voor een gebruiker tooa product abonneren.  
  
 ![abonneren &#45; knopbesturingselement](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM abonneren knopbesturingselement")  
  
### <a name="usage"></a>Gebruik  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a>Parameters  
 Geen.  
  
### <a name="developer-portal-templates"></a>Developer portal-sjablonen  
 Hallo `subscribe-button` besturingselement kan worden gebruikt in Hallo developer portal-sjablonen te volgen.  
  
-   [Product](api-management-product-templates.md#Product)  
  
##  <a name="subscription-cancel"></a>abonnement annuleren  
 Hallo `subscription-cancel` control biedt een besturingselement voor het annuleren van een abonnement tooa product Hallo pagina gebruikersprofiel in Hallo-portal voor ontwikkelaars.  
  
 ![abonnement &#45; besturing annuleren](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM abonnement annuleren besturingselement")  
  
### <a name="usage"></a>Gebruik  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a>Parameters  
  
|Parameter|Beschrijving|  
|---------------|-----------------|  
|subscriptionId|Hallo-id van Hallo abonnement toocancel.|  
|cancelUrl|Hallo abonnement annuleren URL.|  
  
### <a name="developer-portal-templates"></a>Developer portal-sjablonen  
 Hallo `subscription-cancel` besturingselement kan worden gebruikt in Hallo developer portal-sjablonen te volgen.  
  
-   [Product](api-management-product-templates.md#Product)

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over het werken met sjablonen [hoe toocustomize API Management-portal voor ontwikkelaars met behulp van sjablonen Hallo](api-management-developer-portal-templates.md).
