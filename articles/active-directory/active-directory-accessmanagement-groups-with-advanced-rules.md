---
title: Vullen van groepen dynamisch op basis van in Azure Active Directory-objectkenmerken | Microsoft Docs
description: Hoe-aan de geavanceerde regels maken voor groepslidmaatschap inclusief regeloperators expressie en parameters ondersteunde.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 04813a42-d40a-48d6-ae96-15b7e5025884
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: curtand
ms.reviewer: rodejo
ms.openlocfilehash: b9b5ddf42958a2b4e241d0252101d979009e7dc0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="populate-groups-dynamically-based-on-object-attributes"></a>Vullen van groepen dynamisch op basis van kenmerken van het object
De klassieke Azure portal biedt u de mogelijkheid voor complexere op kenmerken gebaseerde dynamisch lidmaatschap voor groepen van Azure Active Directory (Azure AD).  

Wanneer alle kenmerken van een gebruiker of apparaat wijzigt, evalueert het systeem alle dynamische groep regels in een map om te controleren of de wijziging zou een groep toevoegt of verwijdert. Als een gebruiker of apparaat voldoet aan een regel voor een groep, worden ze toegevoegd als een lid van die groep. Als u niet langer voldoen aan de regel, worden ze verwijderd.

> [!NOTE]
> - U kunt een regel instellen voor dynamisch lidmaatschap voor beveiligingsgroepen of Office 365-groepen.
>
> - Dit onderdeel vereist een Azure AD Premium P1-licentie voor elk lid van de gebruiker toegevoegd aan ten minste één dynamische groep.
>
> - U kunt een dynamische groep voor apparaten of gebruikers maken, maar u een regel waarmee zowel gebruikersclaims als apparaatobjecten bevat kan niet maken.

> - Op dit moment is het niet mogelijk te maken van een groep apparaten op basis van die eigenaar is van de kenmerken van de gebruiker. Apparaat lidmaatschapsregels kunnen alleen verwijzen naar het onmiddellijke kenmerken van apparaatobjecten in de map.

## <a name="to-create-an-advanced-rule"></a>Geavanceerde regels maken
1. In de [klassieke Azure-portal](https://manage.windowsazure.com), selecteer **Active Directory**, en open vervolgens de directory van uw organisatie.
2. Selecteer de **groepen** tabblad en open vervolgens de groep die u wilt bewerken.
3. Selecteer de **configureren** tabblad de **geavanceerde regel** optie en voer vervolgens de geavanceerde regel in het tekstvak.

## <a name="constructing-the-body-of-an-advanced-rule"></a>De hoofdtekst van een geavanceerde regel maken
De geavanceerde regel die u voor de dynamisch lidmaatschap voor groepen kunt maken is in wezen een binaire expressie die bestaat uit drie delen en resulteert in een uitkomst true of false. Er zijn drie delen:

* Links parameter
* Binaire operator
* Juiste constante

Een volledige geavanceerde regel ziet er ongeveer als volgt: (leftParameter binaryOperator 'RightConstant'), waarbij het openen en sluithaakje zijn vereist voor de hele binaire expressie, dubbele aanhalingstekens zijn vereist voor de juiste constante en de syntaxis voor de parameter links user.property. Een geavanceerde regel kan bestaan uit meer dan één binaire expressies gescheiden door- en- of en - niet logische operators.
Hier volgen enkele voorbeelden van een correct samengestelde geavanceerde regel:

* (user.department - eq 'Verkoop')- of (user.department - eq "Marketing")
* (user.department - eq 'Verkoop')- en - not (user.jobTitle-bevat 'SDE')

Zie de volgende secties voor de volledige lijst van ondersteunde parameters en regeloperators expressie.


Houd er rekening mee dat de eigenschap moet worden voorafgegaan door het juiste object-type: gebruiker of apparaat.
De onderstaande regel wordt de validatie mislukt: e-– ne null

De juiste regel zou zijn:

User.mail – ne null

De totale lengte van de hoofdtekst van de geavanceerde regel kan niet groter zijn dan 2048 tekens bestaan.

> [!NOTE]
> De tekenreeks en de regex-bewerkingen zijn niet hoofdlettergevoelig.
> Tekenreeksen met aanhalingstekens ' moet worden voorafgegaan met ' teken bijvoorbeeld user.department - eq \`'Verkoop'.
> Gebruik alleen aanhalingstekens voor type tekenreekswaarden en gebruiken alleen Engels aanhalingstekens.
>
>

## <a name="supported-expression-rule-operators"></a>Ondersteunde expressie regeloperators
De volgende tabel bevat de operators voor de regel ondersteund expression en hun syntaxis moet worden gebruikt in de hoofdtekst van de geavanceerde regel:

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

Alle Operators worden hieronder weergegeven per prioriteitsvolgorde van lagere naar hoger, operator in dezelfde regel bevinden zich in dezelfde prioriteit-een - all - of - en - niet - eq - ne - startsWith - notStartsWith-- notContains bevat-overeenkomen met – notMatch-in - notIn

Alle operators kunnen worden gebruikt met of zonder koppelteken voorvoegsel.

Houd er rekening mee dat haakje niet altijd nodig zijn, moet u alleen haakje toevoegen wanneer voorrang voldoet niet aan uw vereisten bijvoorbeeld:

   User.Department-eq 'Marketing –' en 'VS' user.country – eq

is gelijk aan:

   (user.department – eq 'Marketing') – en (user.country-eq "VS")

## <a name="using-the--in-and--notin-operators"></a>Met behulp van de - In en notIn - operators

Als u wilt vergelijken van de waarde van een gebruikerskenmerk tegen een aantal verschillende waarden kunt u de - In of notIn - operators. Hier volgt een voorbeeld met behulp van de - In-operator:

    user.department -In [ "50001", "50002", "50003", “50005”, “50006”, “50007”, “50008”, “50016”, “50020”, “50024”, “50038”, “50039”, “51100” ]

Let op het gebruik van de ' [' en '] ' aan het begin en einde van de lijst met waarden. Deze voorwaarde wordt geëvalueerd als waar de waarde van user.department gelijk is aan een van de waarden in de lijst.

## <a name="query-error-remediation"></a>Herstel voor query-fout
De volgende tabel geeft een lijst van mogelijke fouten opgespoord en hoe deze corrigeren die zich voordoen

| Parserfout-query | Fout-gebruik | Gecorrigeerde syntaxis |
| --- | --- | --- |
| Fout: Kenmerk wordt niet ondersteund. |(user.invalidProperty - eq 'Value') |(user.department - eq '' waarde '')<br/>De eigenschap moet overeenkomen met een van de [eigenschappenlijst ondersteund](#supported-properties). |
| Fout: De Operator wordt niet ondersteund op kenmerk. |(user.accountEnabled-bevat true) |(user.accountEnabled - eq waar)<br/>De eigenschap is van het type boolean. De ondersteunde operators (-eq of - ne) op boolean-type in de bovenstaande lijst. |
| Fout: Fout bij schemacompilatie opvragen. |(user.department - eq 'Verkoop')- en (user.department - eq "Marketing') (user.userPrincipalName-match ' *@domain.ext') |(user.department - eq 'Verkoop')- en (user.department - eq "Marketing")<br/>Logische operator moet overeenkomen met een van de bovenstaande lijst van ondersteunde eigenschappen. (user.userPrincipalName-overeenkomen met '. *@domain.ext') of (user.userPrincipalName-overeenkomen met '@domain.ext$') fout in de reguliere expressie. |
| Fout: Binaire expressie is geen juiste indeling. |(user.department – eq 'Verkoop') (user.department - eq 'Verkoop') (user.department-eq 'Verkoop') |(user.accountEnabled - eq true)- en (user.userPrincipalName-bevat 'alias@domain')<br/>Query heeft meerdere fouten. Haakje niet op de juiste plaats. |
| Fout: Er is een onbekende fout opgetreden tijdens het instellen van dynamische lidmaatschappen. |(user.accountEnabled - eq "True" en user.userPrincipalName-bevat 'alias@domain') |(user.accountEnabled - eq true)- en (user.userPrincipalName-bevat 'alias@domain')<br/>Query heeft meerdere fouten. Haakje niet op de juiste plaats. |

## <a name="supported-properties"></a>Ondersteunde eigenschappen
Hier volgen de gebruikersgegevens die u in de geavanceerde regel gebruiken kunt:

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
| E-mail |Een string-waarde of $null (SMTP-adres van de gebruiker) |(user.mail - eq '' waarde '') |
| mailNickName |De waarde van een tekenreeks (mailalias van de gebruiker) |(user.mailNickName - eq '' waarde '') |
| mobiele |Een string-waarde of $null |(user.mobile - eq '' waarde '') |
| object-id |GUID van het gebruikersobject |(user.objectId - eq '1111111-1111-1111-1111-111111111111') |
| onPremisesSecurityIdentifier | On-premises beveiligings-id (SID) voor gebruikers die zijn gesynchroniseerd van on-premises naar de cloud. |(user.onPremisesSecurityIdentifier - eq "S-1-1-11-1111111111-1111111111-1111111111-1111111") |
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

* -een (voldaan wanneer ten minste één item in de verzameling komt overeen met de voorwaarde)
* -alle (voldaan wanneer alle objecten in de verzameling die overeenkomen met de voorwaarde)

| Eigenschappen | Waarden | Gebruik |
| --- | --- | --- |
| assignedPlans |Elk object in de verzameling beschrijft de tekenreekseigenschappen van de volgende: capabilityStatus, service, servicePlanId |user.assignedPlans-eventuele (assignedPlan.servicePlanId - eq 'efb87545-963c-4e0d-99df-69c6916d9eb0'- en assignedPlan.capabilityStatus - eq "Ingeschakeld") |

Eigenschappen van meerdere waarden zijn verzamelingen van objecten van hetzelfde type. U kunt - eventuele en -alle operators respectievelijk een voorwaarde op een of meer van de items in de verzameling toepassen. Bijvoorbeeld:

assignedPlans is een eigenschap met meerdere waarden met een lijst met alle service-abonnementen aan de gebruiker toegewezen. De expressie wordt Selecteer onder gebruikers die de Exchange Online (Plan 2) service-abonnement dat ook in de ingeschakelde status hebben:

```
user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled")
```

(De Guid-id identificeert het Exchange Online (Plan 2) service-abonnement.)

> [!NOTE]
> Dit is handig als u wilt dat voor het identificeren van alle gebruikers van wie een Office 365 (of andere Microsoft Online Services) mogelijkheid is ingeschakeld, bijvoorbeeld doel te definiëren met een bepaalde set van beleidsregels.

De volgende expressie selecteert alle gebruikers die beschikken over een service-abonnement dat is gekoppeld aan de Intune-service (aangeduid met de naam van de service "SCO"):
```
user.assignedPlans -any (assignedPlan.service -eq "SCO" -and assignedPlan.capabilityStatus -eq "Enabled")
```

## <a name="use-of-null-values"></a>Gebruik van Null-waarden

Geef een null-waarde in een regel, kunt u 'null' of $null. Voorbeeld:

   User.mail – ne null is gelijk aan user.mail – ne $null

## <a name="extension-attributes-and-custom-attributes"></a>Extensie-kenmerken en aangepaste kenmerken
Uitbreidingskenmerken en aangepaste kenmerken worden ondersteund in de regels voor dynamisch lidmaatschap.

Uitbreidingskenmerken vanuit het lokale Windows Server AD worden gesynchroniseerd en nemen de indeling van 'ExtensionAttributeX', waarbij X gelijk is aan 1 en 15 vallen.
Een voorbeeld van een regel die gebruikmaakt van een kenmerk toestelnummer

(user.extensionAttribute15 - eq "Marketing")

Aangepaste kenmerken worden gesynchroniseerd vanuit de lokale Windows Server AD of vanuit een verbonden SaaS-toepassing en de indeling van ' user.extension_[GUID]\__ [kenmerk] ', waarbij [GUID] is de unieke id in van AAD voor de toepassing die het kenmerk in Add hebt gemaakt en [kenmerk] de naam van het kenmerk, is zoals deze is gemaakt.
Een voorbeeld van een regel die gebruikmaakt van een aangepast kenmerk is

User.extension_c272a57b722d4eb29bfe327874ae79cb__OfficeNumber  

De naam van aangepast kenmerk kan worden gevonden in de map een query uitgevoerd op een gebruiker het kenmerk grafiek Verkenner en zoeken naar de naam van het kenmerk.

## <a name="direct-reports-rule"></a>De regel 'Directe ondergeschikten'
U kunt een groep met alle directe ondergeschikten van een manager maken. Wanneer de manager directe ondergeschikten in de toekomst wijzigt, wordt het lidmaatschap van de groep automatisch aangepast.

> [!NOTE]
> 1. Voor de regel werkt, controleert u of de **ID Manager** eigenschap correct is ingesteld op gebruikers in uw tenant. U kunt de huidige waarde voor een gebruiker controleren op hun **tabblad profiel**.
> 2. Deze regel ondersteunt alleen **direct** rapporten. Het is momenteel niet mogelijk een groep maken voor een geneste hiërarchie, bijvoorbeeld een groep met directe ondergeschikten en hun rapporten.

**De groep configureren**

1. Volg de stappen 1-5 van sectie [voor het maken van de geavanceerde regel](#to-create-the-advanced-rule), en selecteer een **lidmaatschapstype** van **dynamische gebruiker**.
2. Op de **dynamische lidmaatschapsregels** blade invoeren van de regel met de volgende syntaxis:

    *Directe ondergeschikten voor "{obectID_of_manager}"*

    Een voorbeeld van een geldige regel:
```
                    Direct Reports for "62e19b97-8b3d-4d4a-a106-4ce66896a863"
```
    where “62e19b97-8b3d-4d4a-a106-4ce66896a863” is the objectID of the manager. The object ID can be found on manager's **Profile tab**.
3. Na het opslaan van de regel, worden alle gebruikers met de opgegeven waarde voor de ID van de Manager worden toegevoegd aan de groep.

## <a name="using-attributes-to-create-rules-for-device-objects"></a>Kenmerken gebruiken voor het maken van regels voor apparaatobjecten
U kunt ook een regel die u apparaatobjecten voor lidmaatschap in een groep selecteert maken. De volgende kenmerken van de apparaten kunnen worden gebruikt:

| Eigenschappen              | Toegestane waarden                  | Gebruik                                                       |
|-------------------------|---------------------------------|-------------------------------------------------------------|
| accountEnabled          | de waarde True, false                      | (device.accountEnabled - eq waar)                            |
| Weergavenaam             | Waarde van een tekenreeks                | (device.displayName - eq 'Rob Iphone')                       |
| DeviceOSType            | Waarde van een tekenreeks                | (device.deviceOSType - eq 'IOS')                             |
| DeviceOSVersion         | Waarde van een tekenreeks                | (apparaat. OSVersion - eq '9.1')                                |
| deviceCategory          | Waarde van een tekenreeks                | (device.deviceCategory - eq "")                              |
| DeviceManufacturer      | Waarde van een tekenreeks                | (device.deviceManufacturer - eq "Microsoft")                 |
| DeviceModel             | Waarde van een tekenreeks                | (device.deviceModel - eq "IPhone 7 +")                        |
| deviceOwnership         | Waarde van een tekenreeks                | (device.deviceOwnership - eq "")                             |
| Domeinnaam              | Waarde van een tekenreeks                | (device.domainName - eq 'contoso.com')                       |
| enrollmentProfileName   | Waarde van een tekenreeks                | (device.enrollmentProfileName - eq "")                       |
| isRooted                | de waarde True, false                      | (device.deviceOSType - eq waar)                              |
| managementType          | Waarde van een tekenreeks                | (device.managementType - eq "")                              |
| OrganizationalUnit      | Waarde van een tekenreeks                | (device.organizationalUnit - eq "")                          |
| deviceId                | een geldig apparaat-id                | (device.deviceId - eq "d4fe7726-5966-431c-b3b8-cddc8fdb717d") |
| object-id                | een geldige AAD objectId            | (device.objectId - eq "76ad43c9-32c5-45e8-a272-7b58b58f596d") |

> [!NOTE]
> Deze regels van het apparaat kunnen niet worden gemaakt met behulp van de vervolgkeuzelijst 'eenvoudige regel' in de klassieke Azure portal.
>
>

## <a name="next-steps"></a>Volgende stappen
Deze artikelen bevatten aanvullende informatie over Azure Active Directory.

* [Het oplossen van problemen dynamisch lidmaatschap voor groepen](active-directory-accessmanagement-troubleshooting.md)
* [Managing access to resources with Azure Active Directory groups](active-directory-manage-groups.md) (Toegang tot resources beheren met Azure Active Directory-groepen)
* [Azure Active Directory cmdlets for configuring group settings](active-directory-accessmanagement-groups-settings-cmdlets.md) (Azure Active Directory-cmdlets voor het configureren van groepsinstellingen)
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)
