---
title: op basis van aaaAttribute dynamisch groepslidmaatschap in Azure Active Directory | Microsoft Docs
description: Hoe toocreate geavanceerde regels voor dynamische groepslidmaatschap, inclusief ondersteunde expressie regeloperators en parameters.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: fb434cc2-9a91-4ebf-9753-dd81e289787e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8cd06ed70433eff65401c67d7351d5dcc12a9dd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-attribute-based-rules-for-dynamic-group-membership-in-azure-active-directory"></a>Op kenmerken gebaseerde regels maken voor dynamisch lidmaatschap in Azure Active Directory
In Azure Active Directory (Azure AD), kunt u geavanceerde regels tooenable complexe op kenmerken gebaseerde dynamisch lidmaatschap voor groepen maken. Dit artikel wordt uitgelegd Hallo kenmerken en syntaxis toocreate dynamische lidmaatschapsregels voor gebruikers of apparaten.

Wanneer geen kenmerken van een gebruiker of apparaat Hallo systeem alle dynamische groep regels in een directory toosee evalueert als Hallo wijziging zou activeert wordt een groep toegevoegd of verwijderd. Als een gebruiker of apparaat voldoet aan een regel voor een groep, worden ze toegevoegd als een lid van die groep. Als ze voldoen aan het niet langer Hallo regel, worden ze verwijderd.

> [!NOTE]
> - U kunt een regel instellen voor dynamisch lidmaatschap voor beveiligingsgroepen of Office 365-groepen.
>
> - Deze functie moet een licentie voor Azure AD Premium-P1 voor elke gebruiker lid toegevoegde tooat minimaal één dynamische groep.
>
> - U kunt een dynamische groep voor apparaten of gebruikers maken, maar u een regel waarmee zowel gebruikersclaims als apparaatobjecten bevat kan niet maken.

> - Hallo momenteel is het niet mogelijk toocreate een apparaatgroep op basis van het die eigenaar is van de kenmerken van de gebruiker. Apparaat lidmaatschapsregels kunnen alleen onmiddellijke verwijzingskenmerken van apparaatobjecten in Hallo-directory.

## <a name="toocreate-an-advanced-rule"></a>een geavanceerde regel toocreate
1. Meld u aan toohello [Azure AD-beheercentrum](https://aad.portal.azure.com) met een account dat is een globale beheerder of de beheerder van een gebruiker.
2. Selecteer **gebruikers en groepen**.
3. Selecteer **alle groepen**.

   ![Openen Hallo groepen blade](./media/active-directory-groups-dynamic-membership-azure-portal/view-groups-blade.png)
4. In **alle groepen**, selecteer **nieuwe groep**.

   ![Nieuwe groep toevoegen](./media/active-directory-groups-dynamic-membership-azure-portal/add-group-type.png)
5. Op Hallo **groep** blade een naam en beschrijving voor de nieuwe groep Hallo opgeven. Selecteer een **lidmaatschapstype** van een van beide **dynamische gebruiker** of **dynamische apparaat**, afhankelijk van of u wilt toocreate een regel voor gebruikers of apparaten en selecteer vervolgens **Toevoegen dynamische query**. Zie voor Hallo kenmerken voor apparaat-regels gebruikt, [met kenmerken toocreate regels voor apparaatobjecten](#using-attributes-to-create-rules-for-device-objects).

   ![Van dynamische lidmaatschapsregel toevoegen](./media/active-directory-groups-dynamic-membership-azure-portal/add-dynamic-group-rule.png)
6. Op Hallo **dynamische lidmaatschapsregels** blade invoeren van de regel in Hallo **toevoegen dynamisch lidmaatschap geavanceerde regel** vak en selecteer vervolgens drukt u op Enter **maken** Hallo onderaan in Hallo-blade.
7. Selecteer **maken** op Hallo **groep** blade toocreate Hallo groep.

## <a name="constructing-hello-body-of-an-advanced-rule"></a>Hallo-hoofdtekst van een geavanceerde regel maken
Hallo geavanceerde regel die u voor Hallo dynamisch lidmaatschap voor groepen kunt maken is in wezen een binaire expressie die bestaat uit drie delen en resulteert in een uitkomst true of false. Er zijn drie delen Hallo:

* Links parameter
* Binaire operator
* Juiste constante

Een volledige geavanceerde regel eruitziet vergelijkbare toothis: (leftParameter binaryOperator 'RightConstant'), waarbij Hallo openen en haakje-sluiten optioneel voor de gehele binaire expressie Hallo zijn, dubbele aanhalingstekens zijn optioneel, alleen vereist voor de juiste Hallo constante wanneer deze tekenreeks en Hallo-syntaxis voor de linker Hallo-parameter is user.property. Een geavanceerde regel kan bestaan uit meer dan één binaire expressies door Hallo gescheiden- en- of en - niet logische operators.

Hallo hieronder vindt u voorbeelden van een correct samengestelde geavanceerde regel:
```
(user.department -eq "Sales") -or (user.department -eq "Marketing")
(user.department -eq "Sales") -and -not (user.jobTitle -contains "SDE")
```
Zie de volgende secties voor Hallo volledige lijst met ondersteunde parameters en regeloperators expressie. Zie voor Hallo kenmerken voor apparaat-regels gebruikt, [met kenmerken toocreate regels voor apparaatobjecten](#using-attributes-to-create-rules-for-device-objects).

Hallo totale lengte van Hallo hoofdtekst van de geavanceerde regel kan niet groter zijn dan 2048 tekens bestaan.

> [!NOTE]
> De tekenreeks en de regex-bewerkingen zijn niet hoofdlettergevoelig. U kunt ook een Null-controles, met behulp van $null als een constante bijvoorbeeld, user.department - eq $null uitvoeren.
> Tekenreeksen met aanhalingstekens ' moet worden voorafgegaan met ' teken bijvoorbeeld user.department - eq \`'Verkoop'.

## <a name="supported-expression-rule-operators"></a>Ondersteunde expressie regeloperators
Hallo volgende tabel bevat alle Hallo ondersteund expression regeloperators en hun syntaxis toobe gebruikt in de hoofdtekst Hallo Hallo geavanceerde regel:

| Operator | Syntaxis |
| --- | --- |
| Niet gelijk aan |-ne |
| is gelijk aan |-eq |
| Niet begint met |-notStartsWith |
| Begint met |-startsWith |
| Bevat niet |-notContains |
| Contains |-bevat |
| Komt niet overeen met |-notMatch |
| Overeenkomst |-overeen met |
| in | -in |
| Niet In | -notIn |

## <a name="operator-precedence"></a>Operatoren

Hieronder vindt u alle Operators per prioriteitsvolgorde van lagere toohigher. Operators op dezelfde regel zijn in dezelfde prioriteit:
````
-any -all
-or
-and
-not
-eq -ne -startsWith -notStartsWith -contains -notContains -match –notMatch -in -notIn
````
Alle operators kunnen worden gebruikt met of zonder Hallo koppelteken voorvoegsel. Haakjes zijn alleen nodig wanneer voorrang voldoet niet aan uw vereisten.
Bijvoorbeeld:
```
   user.department –eq "Marketing" –and user.country –eq "US"
```
is gelijk aan:
```
   (user.department –eq "Marketing") –and (user.country –eq "US")
```
## <a name="using-hello--in-and--notin-operators"></a>Met behulp van Hallo - In en notIn - operators

Als u wilt dat toocompare Hallo waarde van een gebruikerskenmerk op basis van een aantal verschillende waarden kunt u Hallo - In of notIn - operators. Hier volgt een voorbeeld met behulp van Hallo - In-operator:
```
    user.department -In [ "50001", "50002", "50003", “50005”, “50006”, “50007”, “50008”, “50016”, “50020”, “50024”, “50038”, “50039”, “51100” ]
```
Let op Hallo gebruik van Hallo ' [' en '] ' aan Hallo begin en einde van Hallo lijst met waarden. Deze voorwaarde wordt geëvalueerd tooTrue van Hallo-waarde van user.department gelijk is aan een van waarden in de lijst Hallo Hallo.


## <a name="query-error-remediation"></a>Herstel voor query-fout
Hallo volgende tabel geeft een lijst van mogelijke fouten opgespoord en hoe toocorrect indien ze optreden

| Parserfout-query | Fout-gebruik | Gecorrigeerde syntaxis |
| --- | --- | --- |
| Fout: Kenmerk wordt niet ondersteund. |(user.invalidProperty - eq 'Value') |(user.department - eq '' waarde '')<br/>De eigenschap moet overeenkomen met die van Hallo [eigenschappenlijst ondersteund](#supported-properties). |
| Fout: De Operator wordt niet ondersteund op kenmerk. |(user.accountEnabled-bevat true) |(user.accountEnabled - eq waar)<br/>De eigenschap is van het type boolean. Hallo ondersteund operatoren gebruiken (-eq of - ne) op boolean-type van Hallo bovenstaande lijst. |
| Fout: Fout bij schemacompilatie opvragen. |(user.department - eq 'Verkoop')- en (user.department - eq "Marketing') (user.userPrincipalName-match ' *@domain.ext') |(user.department - eq 'Verkoop')- en (user.department - eq "Marketing")<br/>Logische operator moet overeenkomen met een van bovenstaande Hallo ondersteund eigenschappenlijst. (user.userPrincipalName-overeenkomen met '. *@domain.ext') of (user.userPrincipalName-overeenkomen met '@domain.ext$') fout in de reguliere expressie. |
| Fout: Binaire expressie is geen juiste indeling. |(user.department – eq 'Verkoop') (user.department - eq 'Verkoop') (user.department-eq 'Verkoop') |(user.accountEnabled - eq true)- en (user.userPrincipalName-bevat 'alias@domain')<br/>Query heeft meerdere fouten. Haakje niet op de juiste plaats. |
| Fout: Er is een onbekende fout opgetreden tijdens het instellen van dynamische lidmaatschappen. |(user.accountEnabled - eq "True" en user.userPrincipalName-bevat 'alias@domain') |(user.accountEnabled - eq true)- en (user.userPrincipalName-bevat 'alias@domain')<br/>Query heeft meerdere fouten. Haakje niet op de juiste plaats. |

## <a name="supported-properties"></a>Ondersteunde eigenschappen
Hallo hieronder vindt u alle eigenschappen van de Hallo gebruiker die u in de geavanceerde regel gebruiken kunt:

### <a name="properties-of-type-boolean"></a>Eigenschappen van het type boolean
Toegestane operators

* -eq
* -ne

| Eigenschappen | Toegestane waarden | Gebruik |
| --- | --- | --- |
| accountEnabled |de waarde True, false |user.accountEnabled - eq true |
| DirSyncEnabled |de waarde True, false |user.dirSyncEnabled - eq true |

### <a name="properties-of-type-string"></a>Eigenschappen van het type tekenreeks
Toegestane operators

* -eq
* -ne
* -notStartsWith
* -StartsWith
* -bevat
* -notContains
* -overeen met
* -notMatch
* -in
* -notIn

| Eigenschappen | Toegestane waarden | Gebruik |
| --- | --- | --- |
| city |Een string-waarde of $null |(user.city - eq '' waarde '') |
| Land |Een string-waarde of $null |(user.country - eq '' waarde '') |
| Bedrijfsnaam | Een string-waarde of $null | (user.companyName - eq '' waarde '') |
| Afdeling |Een string-waarde of $null |(user.department - eq '' waarde '') |
| Weergavenaam |Waarde van een tekenreeks |(user.displayName - eq '' waarde '') |
| facsimileTelephoneNumber |Een string-waarde of $null |(user.facsimileTelephoneNumber - eq '' waarde '') |
| Voornaam |Een string-waarde of $null |(user.givenName - eq '' waarde '') |
| Functie |Een string-waarde of $null |(user.jobTitle - eq '' waarde '') |
| E-mail |Een string-waarde of $null (SMTP-adres van de gebruiker Hallo) |(user.mail - eq '' waarde '') |
| mailNickName |De waarde van een tekenreeks (mailalias van de gebruiker Hallo) |(user.mailNickName - eq '' waarde '') |
| mobiele |Een string-waarde of $null |(user.mobile - eq '' waarde '') |
| object-id |GUID van het gebruikersobject Hallo |(user.objectId - eq '1111111-1111-1111-1111-111111111111') |
| onPremisesSecurityIdentifier | Lokale beveiligings-id (SID) voor gebruikers die zijn gesynchroniseerd met lokale toohello cloud. |(user.onPremisesSecurityIdentifier - eq "S-1-1-11-1111111111-1111111111-1111111111-1111111") |
| passwordPolicies |Geen DisableStrongPassword DisablePasswordExpiration DisablePasswordExpiration, DisableStrongPassword |(user.passwordPolicies - eq "DisableStrongPassword") |
| physicalDeliveryOfficeName |Een string-waarde of $null |(user.physicalDeliveryOfficeName - eq '' waarde '') |
| Postcode |Een string-waarde of $null |(user.postalCode - eq '' waarde '') |
| preferredLanguage |ISO 639-1-code |(user.preferredLanguage - eq 'en-US') |
| sipProxyAddress |Een string-waarde of $null |(user.sipProxyAddress - eq '' waarde '') |
| state |Een string-waarde of $null |(user.state - eq '' waarde '') |
| StreetAddress |Een string-waarde of $null |(user.streetAddress - eq '' waarde '') |
| Achternaam |Een string-waarde of $null |(user.surname - eq '' waarde '') |
| telephoneNumber |Een string-waarde of $null |(user.telephoneNumber - eq '' waarde '') |
| usageLocation |Twee letters landcode |(user.usageLocation - eq "VS") |
| UserPrincipalName |Waarde van een tekenreeks |(user.userPrincipalName - eq "alias@domain") |
| UserType |lid Gast $null |(user.userType - eq 'Lid') |

### <a name="properties-of-type-string-collection"></a>Eigenschappen van het type tekenreeks-verzameling
Toegestane operators

* -bevat
* -notContains

| Eigenschappen | Toegestane waarden | Gebruik |
| --- | --- | --- |
| otherMails |Waarde van een tekenreeks |(user.otherMails-bevat 'alias@domain') |
| proxyAddresses |SMTP: alias@domain smtp:alias@domain |(user.proxyAddresses-bevat ' SMTP: alias@domain") |

## <a name="multi-value-properties"></a>Eigenschappen van meerdere waarden
Toegestane operators

* -een (tevreden wanneer ten minste één item in de verzameling Hallo overeenkomt met de Hallo voorwaarde)
* -alle (voldaan wanneer alle items in de verzameling Hallo overeenkomen met de voorwaarde van de Hallo)

| Eigenschappen | Waarden | Gebruik |
| --- | --- | --- |
| assignedPlans |Elk object in de verzameling Hallo beschrijft de volgende tekenreekseigenschappen Hallo: capabilityStatus, service, servicePlanId |user.assignedPlans-eventuele (assignedPlan.servicePlanId - eq 'efb87545-963c-4e0d-99df-69c6916d9eb0'- en assignedPlan.capabilityStatus - eq "Ingeschakeld") |

Eigenschappen van meerdere waarden zijn verzamelingen van objecten van het Hallo hetzelfde type. U kunt - eventuele en -alle operators tooapply een voorwaarde tooone of alle Hallo items in de verzameling hello, respectievelijk. Bijvoorbeeld:

assignedPlans is een eigenschap met meerdere waarden met een lijst met alle service-abonnementen toohello gebruiker toegewezen. gebruikers die beschikken over Hallo Exchange Online (Plan 2) service-abonnement dat ook in de ingeschakelde status selecteert Hallo hieronder expressie:

```
user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled")
```

(Guid-id Hallo identificeert Hallo Exchange Online (Plan 2) service-abonnement.)

> [!NOTE]
> Dit is handig als u wilt dat tooidentify alle gebruikers voor wie een Office 365 (of andere Microsoft Online Services) mogelijkheid is ingeschakeld, voor het voorbeeld tootarget ze met een bepaalde set van beleidsregels.

Hallo selecteert volgende expressie alle gebruikers die beschikken over een service-abonnement dat is gekoppeld aan Hallo Intune-service (aangeduid met de naam van de service "SCO"):
```
user.assignedPlans -any (assignedPlan.service -eq "SCO" -and assignedPlan.capabilityStatus -eq "Enabled")
```

## <a name="use-of-null-values"></a>Gebruik van Null-waarden

toospecify een null-waarde in een regel, kunt u 'null' of $null gebruiken. Voorbeeld:
```
   user.mail –ne null
```
is gelijk aan
```
   user.mail –ne $null
   ```

## <a name="extension-attributes-and-custom-attributes"></a>Extensie-kenmerken en aangepaste kenmerken
Uitbreidingskenmerken en aangepaste kenmerken worden ondersteund in de regels voor dynamisch lidmaatschap.

Uitbreidingskenmerken vanuit het lokale Windows Server AD worden gesynchroniseerd en voer de Hallo-indeling van 'ExtensionAttributeX', waarbij X gelijk is aan 1 en 15 vallen.
Een voorbeeld van een regel die gebruikmaakt van een kenmerk toestelnummer
```
(user.extensionAttribute15 -eq "Marketing")
```
Aangepaste kenmerken worden gesynchroniseerd vanuit de lokale Windows Server AD of vanuit een verbonden SaaS-toepassing en Hallo Hallo indeling van ' user.extension_[GUID]\__ [kenmerk] ', waarbij [GUID] Hallo unieke id in van AAD voor de toepassing hello die gemaakte Hallo-kenmerk in AAD en [kenmerk] is Hallo-naam van kenmerk Hallo wanneer deze is gemaakt.
Een voorbeeld van een regel die gebruikmaakt van een aangepast kenmerk is
```
user.extension_c272a57b722d4eb29bfe327874ae79cb__OfficeNumber  
```
Hallo naam van aangepast kenmerk kan worden gevonden in Hallo map door het opvragen van een gebruiker het kenmerk grafiek Verkenner en zoeken naar Hallo kenmerknaam.

## <a name="direct-reports-rule"></a>De regel 'Directe ondergeschikten'
U kunt een groep met alle directe ondergeschikten van een manager maken. Wanneer het Hallo-beheer directe ondergeschikten in toekomstige Hallo wijzigt, wordt Hallo groepslidmaatschap automatisch aangepast.

> [!NOTE]
> 1. Zorg ervoor Hallo Hallo regel toowork, **ID Manager** eigenschap correct is ingesteld op gebruikers in uw tenant. U kunt de huidige waarde voor een gebruiker Hallo controleren op hun **tabblad profiel**.
> 2. Deze regel ondersteunt alleen **direct** rapporten. Het is momenteel niet mogelijk toocreate een groep voor een geneste hiërarchie, bijvoorbeeld een groep met directe ondergeschikten en hun rapporten.

**tooconfigure hello groep**

1. Volg de stappen 1-5 van sectie [toocreate Hallo geavanceerde regel](#to-create-the-advanced-rule), en selecteer een **lidmaatschapstype** van **dynamische gebruiker**.
2. Op Hallo **dynamische lidmaatschapsregels** blade Hallo regel invoeren met Hallo de volgende syntaxis:

    *Directe ondergeschikten voor "{obectID_of_manager}"*

    Een voorbeeld van een geldige regel:
```
                    Direct Reports for "62e19b97-8b3d-4d4a-a106-4ce66896a863"
```
    where “62e19b97-8b3d-4d4a-a106-4ce66896a863” is hello objectID of hello manager. hello object ID can be found on manager's **Profile tab**.
3. Na het opslaan van Hallo regel moeten alle gebruikers met Hallo opgegeven Manager id-waarde toohello groep worden toegevoegd.

## <a name="using-attributes-toocreate-rules-for-device-objects"></a>Met behulp van kenmerken toocreate regels voor apparaatobjecten
U kunt ook een regel die u apparaatobjecten voor lidmaatschap in een groep selecteert maken. Hallo apparaatkenmerken volgende kan worden gebruikt.

 Apparaatkenmerk  | Waarden | Voorbeeld
 ----- | ----- | ----------------
 accountEnabled | de waarde True, false | (device.accountEnabled - eq waar)
 Weergavenaam | Waarde van een tekenreeks |(device.displayName - eq 'Rob Iphone')
 DeviceOSType | Waarde van een tekenreeks | (device.deviceOSType - eq 'IOS')
 DeviceOSVersion | Waarde van een tekenreeks | (apparaat. OSVersion - eq '9.1')
 deviceCategory | een geldige apparaatnaam categorie | (device.deviceCategory - eq "BYOD")
 DeviceManufacturer | Waarde van een tekenreeks | (device.deviceManufacturer - eq 'Samsung')
 DeviceModel | Waarde van een tekenreeks | (device.deviceModel - eq "iPad lucht")
 deviceOwnership | Persoonlijk, bedrijf | (device.deviceOwnership - eq "Bedrijf")
 Domeinnaam | Waarde van een tekenreeks | (device.domainName - eq 'contoso.com')
 enrollmentProfileName | De naam van het Inschrijvingsprofiel voor apparaten van Apple | (device.enrollmentProfileName - eq 'DEP iPhones')
 isRooted | de waarde True, false | (device.isRooted - eq waar)
 managementType | MDM (voor mobiele apparaten)<br>PC (voor computers die worden beheerd door Intune-PC-agent Hallo) | (device.managementType - eq 'MDM')
 OrganizationalUnit | de waarde van een tekenreeks die overeenkomt met de Hallo-naam van de organisatie-eenheid Hallo ingesteld door een lokale Active Directory | (device.organizationalUnit - eq "VS-pc's")
 deviceId | een geldige Azure AD-apparaat-ID | (device.deviceId - eq "d4fe7726-5966-431c-b3b8-cddc8fdb717d")
 object-id | een geldige Azure AD-object-ID |  (device.objectId - eq 76ad43c9-32c5-45e8-a272-7b58b58f596d')




## <a name="next-steps"></a>Volgende stappen
Deze artikelen bevatten aanvullende informatie over groepen in Azure Active Directory.

* [Zie de bestaande groepen](active-directory-groups-view-azure-portal.md)
* [Een nieuwe groep maken en leden toe te voegen](active-directory-groups-create-azure-portal.md)
* [Instellingen van een groep beheren](active-directory-groups-settings-azure-portal.md)
* [Lidmaatschap van een groep beheren](active-directory-groups-membership-azure-portal.md)
* [Dynamische regels voor gebruikers in een groep beheren](active-directory-groups-dynamic-membership-azure-portal.md)
