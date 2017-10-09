---
title: activiteitenrapport aaaAzure Active Directory-aanmeldingspagina API-referentiemateriaal | Microsoft Docs
description: Naslaginformatie voor hello Azure Active Directory-aanmeldingspagina activiteitenrapport API
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ddcd9ae0-f6b7-4f13-a5e1-6cbf51a25634
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 8123f308a291503f2c61ac5de26696806c6402ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a>Azure Active Directory aanmeldingsactiviteiten rapport API-referentiemateriaal
In dit onderwerp maakt deel uit van een verzameling van onderwerpen over hello Azure Active Directory rapportage-API.  
Rapportage van Azure AD biedt u een API waarmee u kunt rapportgegevens voor tooaccess aanmeldingsactiviteiten met code of gerelateerde hulpprogramma's.
Hallo-bereik van dit onderwerp is tooprovide u met naslaginformatie over Hallo **aanmelden activiteit rapport API**.

Zie:

* [Aanmelden activiteiten](active-directory-reporting-azure-portal.md#activity-reports) voor meer conceptuele informatie
* [Aan de slag met Azure Active Directory Reporting API Hallo](active-directory-reporting-api-getting-started.md) voor meer informatie over Hallo rapportage-API.


## <a name="who-can-access-hello-api-data"></a>Wie toegang heeft tot Hallo API gegevens?
* Gebruikers- en Service-Principals Hallo beheerder beveiliging of beveiliging lezer rol
* Globale beheerders
* Elke app die autorisatie tooaccess Hallo API is (app autorisatie worden instellingen slechts op basis van toestemming van de globale beheerder)

tooconfigure toegang voor een tooaccess Toepassingsbeveiliging API's zoals signin-gebeurtenissen, gebruik Hallo PowerShell tooadd Hallo toepassingen Service-Principal te volgen in de rol van de lezer van de beveiliging Hallo

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a>Vereisten
in deze lijst via tooaccess Hallo reporting API, moet u hebben:

* Een [Azure Active Directory Premium P1 of P2 edition](active-directory-editions.md)
* Voltooide Hallo [vereisten tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md). 

## <a name="accessing-hello-api"></a>Toegang tot Hallo-API
U kunt deze API voor installatie zonder toezicht benaderen via Hallo [grafiek Explorer](https://graphexplorer2.cloudapp.net) of programmatisch met bijvoorbeeld PowerShell. In de volgorde voor PowerShell toocorrectly interpreteren Hallo OData-filtersyntaxis gebruikt in AAD grafiek REST-aanroepen, moet u Hallo backtick (aka: ernstig accent) teken te 'escape' hello $-teken. Hallo backtick teken fungeert als [PowerShell van escape-teken](https://technet.microsoft.com/library/hh847755.aspx)PowerShell toodo zodat een letterlijke interpretatie van Hallo $-teken en te voorkomen dat deze als de naam van een PowerShell-variabele verwarrend (ie: $filter).

in dit onderwerp Hallo richt zich op Hallo grafiek Explorer. Zie voor een voorbeeld van PowerShell [PowerShell-script](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).

## <a name="api-endpoint"></a>API-eindpunt
U kunt toegang tot deze API met behulp van Hallo basis-URI te volgen:  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



Vanwege toohello hoeveelheid gegevens die heeft deze API een limiet van 1 miljoen records geretourneerd. 

Deze aanroep retourneert Hallo gegevens in batches. Elke batch heeft maximaal 1000 records.  
tooget hello volgende batch van records, volgende Hallo-verbinding gebruiken. Hallo ophalen [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) informatie uit de eerste set Hallo van de geretourneerde records. Hallo skip-token worden achter Hallo Hallo resultatenset.  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a>Ondersteunde filters
U kunt kleiner Hallo aantal records dat wordt geretourneerd door een API-aanroep in de vorm van een filter.  
Voor aanmelden API worden gerelateerde gegevens, Hallo na filters ondersteund:

* **$top =\<aantal records toobe geretourneerd\>**  -toolimit Hallo aantal geretourneerde records. Dit is een dure bewerking. U moet dit filter niet gebruiken als u wilt dat tooreturn duizenden objecten.  
* **$filter =\<uw filterinstructie\>**  -toospecify op basis van ondersteunde filtervelden, registreert u het belangrijkst Hallo type Hallo

## <a name="supported-filter-fields-and-operators"></a>Ondersteunde filtervelden en -operators
toospecify hello type records die u belangrijk vindt, kunt u een filter-instructie die kan een bestand of een combinatie van Hallo na filtervelden bevatten:

* [signinDateTime](#signindatetime) -definieert een datum of datumbereik
* [userId](#userid) -definieert een specifieke gebruiker op basis van Hallo-gebruikers-ID.
* [userPrincipalName](#userprincipalname) -definieert van een specifieke gebruiker op basis van Hallo gebruiker UPN (User Principal Name)
* [appId](#appid) -ID van een specifieke app op basis van Hallo app definieert
* [appDisplayName](#appdisplayname) -definieert weergavenaam voor een specifieke app op basis van Hallo-app
* [loginStatus](#loginStatus) -definieert Hallo status van Hallo aanmeldingen (geslaagd / fout)

> [!NOTE]
> Wanneer u grafiek Explorer gebruikt, moet u Hallo toouse Hallo juist geldt voor elke letter filter-velden.
> 
> 

toonarrow u Hallo bereik van Hallo gegevens geretourneerd, kunt u combinaties van Hallo ondersteund filters en filtervelden maken. Bijvoorbeeld: hello volgende instructie retourneert Hallo bovenste 10 records tussen 1 juli 2016 en juli 6 2016:

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a>signinDateTime
**Operators ondersteund**: eq, ge RP, gt, lt

**Voorbeeld**:

Met behulp van een specifieke datum

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



Met behulp van een datumbereik    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


**Opmerkingen bij de**:

Hallo datetime-parameter moet zich bevinden in Hallo UTC-notatie 

- - -
### <a name="userid"></a>Gebruikers-id
**Operators ondersteund**: eq

**Voorbeeld**:

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

**Opmerkingen bij de**:

Hallo-waarde van de gebruikers-id is een string-waarde

- - -
### <a name="userprincipalname"></a>UserPrincipalName
**Operators ondersteund**: eq

**Voorbeeld**:

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


**Opmerkingen bij de**:

Hallo-waarde van userPrincipalName is de waarde van een tekenreeks

- - -
### <a name="appid"></a>AppId
**Operators ondersteund**: eq

**Voorbeeld**:

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



**Opmerkingen bij de**:

Hallo-waarde van de appId is een string-waarde

- - -
### <a name="appdisplayname"></a>appDisplayName
**Operators ondersteund**: eq

**Voorbeeld**:

    $filter=appDisplayName+eq+'Azure+Portal' 


**Opmerkingen bij de**:

Hallo-waarde van appDisplayName is een string-waarde

- - -
### <a name="loginstatus"></a>loginStatus
**Operators ondersteund**: eq

**Voorbeeld**:

    $filter=loginStatus+eq+'1'  


**Opmerkingen bij de**:

Er zijn twee opties voor Hallo loginStatus: 0 - geslaagd, 1 - fout

- - -
## <a name="next-steps"></a>Volgende stappen
* Wilt u toosee voorbeelden voor gefilterde activiteiten aanmelden? Bekijk Hallo [Azure Active Directory aanmeldingsactiviteiten rapport API samples](active-directory-reporting-api-sign-in-activity-samples.md).
* Wilt u meer informatie over reporting hello Azure AD-API tooknow? Zie [aan de slag met Azure Active Directory Reporting API Hallo](active-directory-reporting-api-getting-started.md).

