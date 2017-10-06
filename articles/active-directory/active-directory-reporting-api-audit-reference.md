---
title: controle van de Active Directory aaaAzure API-referentiemateriaal | Microsoft Docs
description: Hoe tooget Hello audit-API van Azure Active Directory gestart
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 44e46be8-09e5-4981-be2b-d474aaa92792
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5f33b62ede9be445f35704739e328580dc454368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-api-reference"></a>Azure Active Directory-audit API-referentiemateriaal
In dit onderwerp maakt deel uit van een verzameling van onderwerpen over hello Azure Active Directory rapportage-API.  
Rapportage van Azure AD biedt u een API waarmee u tooaccess controlegegevens met code of gerelateerde hulpprogramma's.
Hallo-bereik van dit onderwerp is tooprovide u met naslaginformatie over Hallo **audit API**.

Zie:

* [Controlelogboeken](active-directory-reporting-azure-portal.md#activity-reports) voor meer conceptuele informatie

* [Aan de slag met Azure Active Directory Reporting API Hallo](active-directory-reporting-api-getting-started.md) voor meer informatie over Hallo rapportage-API.


Voor:

- Veelgestelde vragen, Lees onze [Veelgestelde vragen](active-directory-reporting-faq.md) 

- Uitgeeft, neem [een ondersteuningsticket bestand](active-directory-troubleshooting-support-howto.md) 


## <a name="who-can-access-hello-data"></a>Wie toegang heeft tot Hallo gegevens?
* Gebruikers met de rol beheerder beveiliging of beveiliging Reader Hallo
* Globale beheerders
* Elke app die autorisatie tooaccess Hallo API is (app autorisatie worden instellingen slechts op basis van toestemming van de globale beheerder)

## <a name="prerequisites"></a>Vereisten
In de volgorde tooaccess in deze lijst via Hallo rapportage-API, moet u hebben:

* Een [Azure Active Directory gratis of betere edition](active-directory-editions.md)
* Voltooide Hallo [vereisten tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md). 

## <a name="accessing-hello-api"></a>Toegang tot Hallo-API
U kunt deze API voor installatie zonder toezicht benaderen via Hallo [grafiek Explorer](https://graphexplorer2.cloudapp.net) of programmatisch met bijvoorbeeld PowerShell. In de volgorde voor PowerShell toocorrectly interpreteren Hallo OData-filtersyntaxis gebruikt in AAD grafiek REST-aanroepen, moet u Hallo backtick (aka: ernstig accent) teken te 'escape' hello $-teken. Hallo backtick teken fungeert als [PowerShell van escape-teken](https://technet.microsoft.com/library/hh847755.aspx)PowerShell toodo zodat een letterlijke interpretatie van Hallo $-teken en te voorkomen dat deze als de naam van een PowerShell-variabele verwarrend (ie: $filter).

in dit onderwerp Hallo richt zich op Hallo grafiek Explorer. Zie voor een voorbeeld van PowerShell [PowerShell-script](active-directory-reporting-api-audit-samples.md#powershell-script).

## <a name="api-endpoint"></a>API-eindpunt
U kunt toegang tot deze API met behulp van Hallo URI te volgen:  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

Er is geen limiet voor het aantal records dat wordt geretourneerd door hello Azure AD audit-API (OData paginering met) Hallo.
Bekijk voor ondergrenzen voor de bewaarperiode op rapportagegegevens [bewaarbeleidsregels Reporting](active-directory-reporting-retention.md).

Deze aanroep retourneert Hallo gegevens in batches. Elke batch heeft maximaal 1000 records.  
tooget hello volgende batch van records, volgende Hallo-verbinding gebruiken. Hallo skiptoken informatie ophalen uit de eerste set Hallo van de geretourneerde records. Hallo skip-token worden achter Hallo Hallo resultatenset.  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a>Ondersteunde filters
U kunt kleiner Hallo aantal records dat wordt geretourneerd door een API-aanroep in de vorm van een filter.  
Voor aanmelden API worden gerelateerde gegevens, Hallo na filters ondersteund:

* **$top =\<aantal records toobe geretourneerd\>**  -toolimit Hallo aantal geretourneerde records. Dit is een dure bewerking. U moet dit filter niet gebruiken als u wilt dat tooreturn duizenden objecten.     
* **$filter =\<uw filterinstructie\>**  -toospecify op basis van ondersteunde filtervelden, registreert u het belangrijkst Hallo type Hallo

## <a name="supported-filter-fields-and-operators"></a>Ondersteunde filtervelden en -operators
toospecify hello type records die u belangrijk vindt, kunt u een filter-instructie die kan een bestand of een combinatie van Hallo na filtervelden bevatten:

* [ActiviteitDatum](#activitydate) -definieert een datum of datumbereik
* [categorie](#category) -Hallo categorie op het gewenste toofilter definieert.
* [activityStatus](#activitystatus) -definieert Hallo status van een activiteit
* [activityType](#activitytype) -definieert Hallo-type van een activiteit
* [activiteit](#activity) -Hallo activiteit definieert als tekenreeks  
* [naam van deacteur/](#actorname) -Hallo actor definieert in de vorm van de naam van de Hallo acteur van
* [acteur/objectid](#actorobjectid) -Hallo actor definieert in de vorm van de Hallo actor-ID   
* [acteur/upn](#actorupn) -Hallo actor definieert in de vorm van Hallo actor van principe (user Principal name) 
* [doelnaam/](#targetname) -Hallo doel in de vorm van de naam van de Hallo acteur van definieert
* [doel/objectid](#targetobjectid) -Hallo doel definieert in de vorm van Hallo-doel-ID  
* [doel/upn](#targetupn) -Hallo actor definieert in de vorm van Hallo actor van principe (user Principal name)   

- - -
### <a name="activitydate"></a>activityDate
**Operators ondersteund**: eq, ge RP, gt, lt

**Voorbeeld**:

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

**Opmerkingen bij de**:

DateTime-waarde moet in UTC-notatie

- - -
### <a name="category"></a>category

**Ondersteunde waarden**:

| Category                         | Waarde     |
| :--                              | ---       |
| Hoofddirectory                   | Directory |
| Self-service voor wachtwoordbeheer | SSPR      |
| Self-service voor groepsbeheer    | SSGM      |
| Account inrichten             | Sync      |
| Automatische wachtwoordoverschakeling      | Automatische wachtwoordoverschakeling |
| Identiteitsbeveiliging              | IdentityProtection |
| Uitgenodigde gebruikers                    | Uitgenodigde gebruikers |
| MIM-service                      | MIM-service |



**Operators ondersteund**: eq

**Voorbeeld**:

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a>ActivityStatus

**Ondersteunde waarden**:

| Activiteitsstatus | Waarde |
| :--             | ---   |
| Geslaagd         | 0     |
| Fout         | - 1   |

**Operators ondersteund**: eq

**Voorbeeld**:

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a>activityType
**Operators ondersteund**: eq

**Voorbeeld**:

    $filter=activityType eq 'User'    

**Opmerkingen bij de**:

hoofdlettergevoelig

- - -
### <a name="activity"></a>Activiteit
**Operators ondersteund**: eq, bevat, startsWith

**Voorbeeld**:

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

**Opmerkingen bij de**:

hoofdlettergevoelig

- - -
### <a name="actorname"></a>naam van de acteur /
**Operators ondersteund**: eq, bevat, startsWith

**Voorbeeld**:

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

**Opmerkingen bij de**:

Niet-hoofdlettergevoelige

- - -
### <a name="actorobjectid"></a>acteur/objectId
**Operators ondersteund**: eq

**Voorbeeld**:

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a>doelnaam /
**Operators ondersteund**: eq, bevat, startsWith

**Voorbeeld**:

    $filter=targets/any(t: t/name eq 'some name')    

**Opmerkingen bij de**:

Niet-hoofdlettergevoelige

- - -
### <a name="targetupn"></a>doel/upn
**Operators ondersteund**: eq, startsWith

**Voorbeeld**:

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

**Opmerkingen bij de**:

* Niet-hoofdlettergevoelige
* U moet tooadd Hallo volledige naamruimte tijdens het opvragen van Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity

- - -
### <a name="targetobjectid"></a>doel/objectId
**Operators ondersteund**: eq

**Voorbeeld**:

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a>acteur/upn
**Operators ondersteund**: eq, startsWith

**Voorbeeld**:

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

**Opmerkingen bij de**:

* Niet-hoofdlettergevoelige 
* U moet tooadd Hallo volledige naamruimte tijdens het opvragen van Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity

- - -
## <a name="next-steps"></a>Volgende stappen
* Wilt u toosee voorbeelden voor gefilterde systeemactiviteiten? Bekijk Hallo [voorbeelden van Azure Active Directory-audit API](active-directory-reporting-api-audit-samples.md).
* Wilt u meer informatie over reporting hello Azure AD-API tooknow? Zie [aan de slag met Azure Active Directory Reporting API Hallo](active-directory-reporting-api-getting-started.md).

