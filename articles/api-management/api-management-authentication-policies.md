---
title: verificatiebeleid voor aaaAzure API Management | Microsoft Docs
description: Meer informatie over Hallo verificatiebeleid beschikbaar voor gebruik in Azure API Management.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 061702a7-3a78-472b-a54a-f3b1e332490d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: ce93cced66cb67520e97c7c15f3685bffb08e1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-authentication-policies"></a>API Management-beleidsregels voor verificatie
Dit onderwerp bevat een verwijzing voor Hallo API Management-beleidsregels te volgen. Zie voor meer informatie over het toevoegen en configureren van beleid [-beleid in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="AuthenticationPolicies"></a>Verificatiebeleid  
  
-   [Verificatie met Basic](api-management-authentication-policies.md#Basic) -verificatie met een back-endservice basisverificatie wordt gebruikt.  
  
-   [Verificatie met een clientcertificaat](api-management-authentication-policies.md#ClientCertificate) -verificatie met een back-endservice met behulp van clientcertificaten.  
  
##  <a name="Basic"></a>Verificatie met Basic  
 Gebruik Hallo `authentication-basic` beleid tooauthenticate met een back-endservice basisverificatie wordt gebruikt. Dit beleid effectief Hallo HTTP-autorisatie-header toohello waarde bijbehorende toohello referenties instellen in het Hallo-beleid.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a>Voorbeeld  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a>Elementen  
  
|Naam|Beschrijving|Vereist|  
|----------|-----------------|--------------|  
|verificatie-basis|Hoofdelement.|Ja|  
  
### <a name="attributes"></a>Kenmerken  
  
|Naam|Beschrijving|Vereist|Standaard|  
|----------|-----------------|--------------|-------------|  
|gebruikersnaam|Hiermee geeft u een gebruikersnaam Hallo Hallo Basic referentie.|Ja|N.v.t.|  
|wachtwoord|Hiermee geeft u Hallo-wachtwoord van Hallo Basic referentie.|Ja|N.v.t.|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomende  
  
-   **Beleid scopes:** API  
  
##  <a name="ClientCertificate"></a>Verificatie met een clientcertificaat  
 Gebruik Hallo `authentication-certificate` beleid tooauthenticate met een back-endservice clientcertificaat. Hallo-certificaat moet toobe [geïnstalleerd in API Management](http://go.microsoft.com/fwlink/?LinkID=511599) eerste en wordt geïdentificeerd door de vingerafdruk.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a>Voorbeeld  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a>Elementen  
  
|Naam|Beschrijving|Vereist|  
|----------|-----------------|--------------|  
|certificaat voor clientverificatie|Hoofdelement.|Ja|  
  
### <a name="attributes"></a>Kenmerken  
  
|Naam|Beschrijving|Vereist|Standaard|  
|----------|-----------------|--------------|-------------|  
|vingerafdruk|Hallo vingerafdruk Hallo clientcertificaat.|Ja|N.v.t.|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomende  
  
-   **Beleid scopes:** API  
  

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie werken met beleid [-beleid in API Management](api-management-howto-policies.md).  