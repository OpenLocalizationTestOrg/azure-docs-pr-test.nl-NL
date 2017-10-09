---
title: aaaWriting expressies voor kenmerktoewijzingen in Azure Active Directory | Microsoft Docs
description: Meer informatie over hoe toouse expressie toewijzingen tootransform kenmerk waarden in een aanvaardbare indeling tijdens de geautomatiseerde inrichting van objecten van de SaaS-app in Azure Active Directory.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: b13c51cd-1bea-4e5e-9791-5d951a518943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: markvi
ms.openlocfilehash: caa0dd8144f6e5279a869e015ed75bd24169d585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="writing-expressions-for-attribute-mappings-in-azure-active-directory"></a>Expressies voor kenmerktoewijzingen schrijven in Azure Active Directory
Bij het configureren van inrichting tooa SaaS-toepassing is een expressie-toewijzing Hallo typen kenmerktoewijzingen die u kunt opgeven. Hiervoor moet u een script-achtige expressie waarmee u tootransform gegevens van uw gebruikers in de opmaak die meer geschikt is voor de SaaS-toepassing hello.

## <a name="syntax-overview"></a>Overzicht van de syntaxis
Hallo-syntaxis voor expressies voor kenmerktoewijzingen is doet denken aan van Visual Basic voor Applications (VBA)-functies.

* Hallo gehele expressie moet worden gedefinieerd in termen van functies, die bestaan uit een naam die wordt gevolgd door haakjes argumenten: <br>
  *Functienaam (<< argument 1 >>, <<argument N>>)*
* U kunt functies binnen elkaar nesten. Bijvoorbeeld: <br> *FunctionOne (FunctionTwo (<<argument1>>))*
* U kunt drie soorten argumenten doorgegeven aan functies:
  
  1. Kenmerken, die moeten worden tussen vierkante vierkante haken. Bijvoorbeeld: [attributeName]
  2. Tekenreeksconstanten moeten tussen dubbele aanhalingstekens worden geplaatst. Bijvoorbeeld: 'Verenigde Staten'
  3. Andere functies. Bijvoorbeeld: FunctionOne (<<argument1>>, FunctionTwo (<<argument2>>))
* Voor tekenreeksconstanten, als u een backslash (\) of een aanhalingsteken (") in Hallo tekenreeks, moet moet deze worden voorafgegaan door Hallo backslash (\)-symbool. Bijvoorbeeld: ' Bedrijfsnaam: \"Contoso\"'

## <a name="list-of-functions"></a>Lijst met functies
[Append](#append) &nbsp; &nbsp; &nbsp; &nbsp; [FormatDateTime](#formatdatetime) &nbsp; &nbsp; &nbsp; &nbsp; [koppelen](#join) &nbsp; &nbsp; &nbsp; &nbsp; [Mid](#mid) &nbsp; &nbsp; &nbsp; &nbsp; [niet](#not) &nbsp; &nbsp; &nbsp; &nbsp; [Vervangen](#replace) &nbsp; &nbsp; &nbsp; &nbsp; [StripSpaces](#stripspaces) &nbsp; &nbsp; &nbsp; &nbsp; [Switch](#switch)

- - -
### <a name="append"></a>Toevoegen
**Functie:**<br> Append(Source, suffix)

**Beschrijving:**<br> Neemt een tekenreekswaarde bron en Hallo achtervoegsel toohello eind toegevoegd.

**Parameters:**<br> 

| Naam | Vereiste / herhalende | Type | Opmerkingen |
| --- | --- | --- | --- |
| **bron** |Vereist |Tekenreeks |Meestal de naam van kenmerk van het bronobject Hallo Hallo |
| **achtervoegsel** |Vereist |Tekenreeks |Hallo-tekenreeks die u wilt dat tooappend toohello einde van de bron-Hallo-waarde. |

- - -
### <a name="formatdatetime"></a>formatDateTime
**Functie:**<br> FormatDateTime (bron, inputFormat, outputFormat)

**Beschrijving:**<br> Een tekenreeks van de datum van de ene indeling en converteert naar een andere indeling.

**Parameters:**<br> 

| Naam | Vereiste / herhalende | Type | Opmerkingen |
| --- | --- | --- | --- |
| **bron** |Vereist |Tekenreeks |Meestal naam van kenmerk Hallo van Hallo bronobject. |
| **inputFormat** |Vereist |Tekenreeks |Verwachte notatie voor de bron-Hallo-waarde. Zie voor ondersteunde indelingen [http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx](http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx). |
| **outputFormat** |Vereist |Tekenreeks |Indeling van Hallo uitvoer datum. |

- - -
### <a name="join"></a>Koppelen
**Functie:**<br> Join (scheidingsteken, bron1, bron2,...)

**Beschrijving:**<br> Join() is vergelijkbaar tooAppend(), behalve dat deze meerdere kunt combineren **bron** tekenreeks waarden in één tekenreeks en elke waarde worden gescheiden door een **scheidingsteken** tekenreeks.

Als een van de bron-waarden Hallo een kenmerk met meerdere waarden is, worden elke waarde in kenmerk waarde van het lid samen, gescheiden Hallo scheidingsteken.

**Parameters:**<br> 

| Naam | Vereiste / herhalende | Type | Opmerkingen |
| --- | --- | --- | --- |
| **scheidingsteken** |Vereist |Tekenreeks |Tekenreeks gebruikt tooseparate bronwaarden wanneer ze worden samengevoegd tot één tekenreeks. Kan ' ' als er geen scheidingsteken vereist is. |
| ** bron1... bronN ** |Vereiste, variabele-aantal keren |Tekenreeks |Tekenreeks waarden toobe zijn samengevoegd. |

- - -
### <a name="mid"></a>Mid
**Functie:**<br> Mid (bron, start, lengte)

**Beschrijving:**<br> Retourneert een subtekenreeks van Hallo bronwaarde. Een subtekenreeks is een tekenreeks zijn met slechts enkele Hallo tekens uit de brontekenreeks Hallo.

**Parameters:**<br> 

| Naam | Vereiste / herhalende | Type | Opmerkingen |
| --- | --- | --- | --- |
| **bron** |Vereist |Tekenreeks |Meestal de naam van het Hallo-kenmerk. |
| **start** |Vereist |geheel getal |De index in Hallo **bron** tekenreeks waar subtekenreeks moet beginnen. Eerste teken in Hallo tekenreeks heeft de index van 1, tweede teken wordt index 2 hebben, enzovoort. |
| **lengte** |Vereist |geheel getal |Lengte van Hallo substring. Als de lengte buiten Hallo eindigt **bron** tekenreeks, functie substring van resultaat **start** index tot het einde van **bron** tekenreeks. |

- - -
### <a name="not"></a>niet
**Functie:**<br> NOT(Source)

**Beschrijving:**<br> Spiegelingen Hallo Booleaanse waarde Hallo **bron**. Als **bron** waarde is '*True*', retourneert '*False*'. Anders retourneert '*True*'.

**Parameters:**<br> 

| Naam | Vereiste / herhalende | Type | Opmerkingen |
| --- | --- | --- | --- |
| **bron** |Vereist |Booleaanse tekenreeks |Verwacht **bron** waarden zijn 'True' of 'False'... |

- - -
### <a name="replace"></a>Vervangen
**Functie:**<br> ObsoleteReplace (bron, oldValue, regexPattern, regexGroupName, vervangende waarde, replacementAttributeName, sjabloon)

**Beschrijving:**<br>
Vervangt waarden binnen een tekenreeks. Het werkt anders, afhankelijk van de opgegeven Hallo-parameters:

* Wanneer **oldValue** en **vervangende waarde** zijn beschikbaar:
  
  * Alle instanties van oldValue in Hallo bron vervangen door de vervangende waarde
* Wanneer **oldValue** en **sjabloon** zijn beschikbaar:
  
  * Vervangt alle instanties van Hallo **oldValue** in Hallo **sjabloon** Hello **bron** waarde
* Wanneer **oldValueRegexPattern**, **oldValueRegexGroupName**, **vervangende waarde** zijn beschikbaar:
  
  * Vervangt alle waarden die overeenkomen met oldValueRegexPattern in Hallo brontekenreeks met vervangende waarde
* Wanneer **oldValueRegexPattern**, **oldValueRegexGroupName**, **replacementPropertyName** zijn beschikbaar:
  
  * Als **bron** waarde heeft, **bron** wordt geretourneerd
  * Als **bron** heeft geen waarde, gebruikt de **oldValueRegexPattern** en **oldValueRegexGroupName** tooextract vervangende waarde van eigenschap met de Hallo  **replacementPropertyName**. Vervangende waarde wordt geretourneerd als resultaat Hallo

**Parameters:**<br> 

| Naam | Vereiste / herhalende | Type | Opmerkingen |
| --- | --- | --- | --- |
| **bron** |Vereist |Tekenreeks |Meestal naam van kenmerk Hallo van Hallo bronobject. |
| **oldValue** |Optioneel |Tekenreeks |Waarde vervangen toobe **bron** of **sjabloon**. |
| **regexPattern** |Optioneel |Tekenreeks |Regex-patroon voor Hallo waarde toobe vervangen **bron**. Of, als replacementPropertyName wordt gebruikt, tooextract waarde van de vervangende eigenschap patroon. |
| **regexGroupName** |Optioneel |Tekenreeks |Naam van de groep Hallo binnen **regexPattern**. Alleen wanneer replacementPropertyName wordt gebruikt, wordt er Haal de waarde van deze groep als vervangende waarde van eigenschap vervanging. |
| **vervangende waarde** |Optioneel |Tekenreeks |Nieuwe waarde tooreplace oude met. |
| **replacementAttributeName** |Optioneel |Tekenreeks |Naam van Hallo kenmerk toobe gebruikt voor de vervangende waarde wanneer de bron heeft geen waarde. |
| **sjabloon** |Optioneel |Tekenreeks |Wanneer **sjabloon** waarde wordt opgegeven, gaan we voor **oldValue** binnen Hallo sjabloon en vervang deze door de bronwaarde. |

- - -
### <a name="stripspaces"></a>StripSpaces
**Functie:**<br> StripSpaces(source)

**Beschrijving:**<br> Verwijdert alle spaties ("") tekens bevatten uit Hallo brontekenreeks.

**Parameters:**<br> 

| Naam | Vereiste / herhalende | Type | Opmerkingen |
| --- | --- | --- | --- |
| **bron** |Vereist |Tekenreeks |**bron** tooupdate waarde. |

- - -
### <a name="switch"></a>Switch
**Functie:**<br> Switch (bron, defaultValue, key1, value1, key2, waarde2,...)

**Beschrijving:**<br> Wanneer **bron** waarde komt overeen met een **sleutel**, retourneert **waarde** voor die **sleutel**. Als **bron** waarde komt niet overeen met alle sleutels, retourneert **defaultValue**.  **Sleutel** en **waarde** parameters moeten altijd komen in paren worden gebruikt. Hallo functie verwacht altijd een even aantal parameters.

**Parameters:**<br> 

| Naam | Vereiste / herhalende | Type | Opmerkingen |
| --- | --- | --- | --- |
| **bron** |Vereist |Tekenreeks |**Bron** tooupdate waarde. |
| **Standaardwaarde** |Optioneel |Tekenreeks |Standaard waarde toobe gebruikt als bron komt niet overeen met alle sleutels. Lege tekenreeks (""). |
| **sleutel** |Vereist |Tekenreeks |**Sleutel** toocompare **bron** waarde met. |
| **waarde** |Vereist |Tekenreeks |Vervangende waarde voor Hallo **bron** overeenkomende Hallo-sleutel. |

## <a name="examples"></a>Voorbeelden
### <a name="strip-known-domain-name"></a>Strook bekende domeinnaam
U moet toostrip een bekende domeinnaam van tooobtain van de e-mailadres van een gebruiker een gebruikersnaam. <br>
Bijvoorbeeld als Hallo domein 'contoso.com' is, kan u Hallo expressie te volgen:

**Expressie:** <br>
`Replace([mail], "@contoso.com", , ,"", ,)`

**Voorbeeld van invoer / uitvoer:** <br>

* **INVOER** (e-mail): 'john.doe@contoso.com'
* **UITVOER**: 'john.doe'

### <a name="append-constant-suffix-toouser-name"></a>Constante achtervoegsel toouser naam toevoegen
Als u van een Sandbox met Salesforce gebruikmaakt, moet u mogelijk een extra achtervoegsels tooall tooappend uw gebruikersnamen voordat deze worden gesynchroniseerd.

**Expressie:** <br>
`Append([userPrincipalName], ".test"))`

**I/o-voorbeeld:** <br>

* **INVOER**: (userPrincipalName): 'John.Doe@contoso.com'
* **UITVOER**: 'John.Doe@contoso.com.test'

### <a name="generate-user-alias-by-concatenating-parts-of-first-and-last-name"></a>Gebruikersalias genereren met cookievalidatie delen van de voornaam en achternaam
Een gebruikersalias toogenerate moet u eerst 3 letters van de voornaam van de gebruiker en de eerste 5 letters van de achternaam van de gebruiker.

**Expressie:** <br>
`Append(Mid([givenName], 1, 3), Mid([surname], 1, 5))`

**I/o-voorbeeld:** <br>

* **INVOER** (givenName): "Jan"
* **INVOER** (voornaam): 'De Vries'
* **UITVOER**: 'JohDoe'

### <a name="output-date-as-a-string-in-a-certain-format"></a>Uitvoerdatum als een tekenreeks in een bepaalde indeling
Wilt u toosend datums tooa SaaS-toepassing in een bepaalde indeling. <br>
U wilt bijvoorbeeld tooformat datums voor ServiceNow.

**Expressie:** <br>

`FormatDateTime([extensionAttribute1], "yyyyMMddHHmmss.fZ", "yyyy-MM-dd")`

**I/o-voorbeeld:**

* **INVOER** (extensionAttribute1): '20150123105347.1Z'
* **UITVOER**: '2015-01-23'

### <a name="replace-a-value-based-on-predefined-set-of-options"></a>Een waarde op basis van vooraf gedefinieerde set opties vervangen
U moet het Hallo-tijdzone toodefine van Hallo-gebruiker op basis van Hallo status code opgeslagen in Azure AD. <br>
Als Hallo status code komt niet met de Hallo vooraf gedefinieerde opties overeen, gebruikt u de standaardwaarde van 'Australië/Sydney'.

**Expressie:** <br>

`Switch([state], "Australia/Sydney", "NSW", "Australia/Sydney","QLD", "Australia/Brisbane", "SA", "Australia/Adelaide")`

**I/o-voorbeeld:**

* **INVOER** (status): 'QLD'
* **UITVOER**: ' Australië/Brisbane'

## <a name="related-articles"></a>Verwante artikelen
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
* [Gebruiker inrichten/Deprovisioning tooSaaS Apps automatiseren](active-directory-saas-app-provisioning.md)
* [Kenmerktoewijzingen voor gebruikers inrichten aanpassen](active-directory-saas-customizing-attribute-mappings.md)
* [Bereikfilters voor gebruikers inrichten](active-directory-saas-scoping-filters.md)
* [Met behulp van SCIM tooenable automatische inrichting van gebruikers en groepen van Azure Active Directory-tooapplications](active-directory-scim-provisioning.md)
* [Meldingen inrichten van een account](active-directory-saas-account-provisioning-notifications.md)
* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps](active-directory-saas-tutorial-list.md)

