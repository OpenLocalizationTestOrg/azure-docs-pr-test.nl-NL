---
title: verwijzing naar de Service Bus SQLFilter aaaAzure | Microsoft Docs
description: Gegevens over SQLFilter grammatica.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: ea49d42e343a6b324eb34c7831ff6be2855346e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sqlfilter-syntax"></a>SQLFilter syntaxis

Een *SqlFilter* is een exemplaar van Hallo [SqlFilter klasse](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), en geeft u een SQL-filter op basis van taal-expressie die wordt geëvalueerd op basis van een [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage). Een SqlFilter ondersteunt een subset van Hallo SQL-92 standaard.  
  
 Dit onderwerp bevat informatie over SqlFilter grammatica.  
  
```  
<predicate ::=  
      { NOT <predicate> }  
      | <predicate> AND <predicate>  
      | <predicate> OR <predicate>  
      | <expression> { = | <> | != | > | >= | < | <= } <expression>  
      | <property> IS [NOT] NULL  
      | <expression> [NOT] IN ( <expression> [, ...n] )  
      | <expression> [NOT] LIKE <pattern> [ESCAPE <escape_char>]  
      | EXISTS ( <property> )  
      | ( <predicate> )  
  
```  
  
```  
<expression> ::=  
      <constant>   
      | <function>  
      | <property>  
      | <expression> { + | - | * | / | % } <expression>  
      | { + | - } <expression>  
      | ( <expression> )  
  
```  
  
```  
<property> :=   
       [<scope> .] <property_name>  
  
```  
  
## <a name="arguments"></a>Argumenten  
  
-   `<scope>`is een optionele tekenreeks die aangeeft Hallo bereik van Hallo `<property_name>`. Geldige waarden zijn `sys` of `user`. Hallo `sys` waarde geeft aan dat systeem bereik waar `<property_name>` is de naam van een openbare eigenschap Hallo [BrokeredMessage klasse](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage). `user`bereik van de gebruiker geeft aan waar `<property_name>` is een sleutel van Hallo [BrokeredMessage klasse](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) woordenlijst. `user`in het bereik zijn Hallo standaardbereik als `<scope>` is niet opgegeven.  
  
## <a name="remarks"></a>Opmerkingen

Een poging tooaccess een niet-bestaande systeemeigenschap is een fout tijdens een poging een niet-bestaande tooaccess gebruiker-eigenschap geen fout is. In plaats daarvan wordt de eigenschap van een niet-bestaande intern geëvalueerd als een onbekende waarde. Een onbekende waarde behandeld speciaal tijdens de evaluatie van de operator.  
  
## <a name="propertyname"></a>kubuskenmerkbinding  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a>Argumenten  

 `<regular_identifier>`is een tekenreeks die wordt vertegenwoordigd door Hallo volgende reguliere expressie:  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
Deze grammatica betekent een tekenreeks die begint met een letter en wordt gevolgd door een of meer onderstrepingsteken/letter/cijfers.  
  
`[:IsLetter:]`betekent een Unicode-teken is aangemerkt als een Unicode-letter. `System.Char.IsLetter(c)`retourneert `true` als `c` is een Unicode-letter.  
  
`[:IsDigit:]`betekent een Unicode-teken is aangemerkt als een decimaal cijfer. `System.Char.IsDigit(c)`retourneert `true` als `c` een Unicode-teken.  
  
Een `<regular_identifier>` mag geen gereserveerd trefwoord.  
  
`<delimited_identifier>`is een tekenreeks die is ingesloten door horizontaal vierkante haken ([]). Een vierkant haakje sluiten wordt weergegeven als twee rechts vierkante haken. Hallo hieronder vindt u voorbeelden van `<delimited_identifier>`:  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
`<quoted_identifier>`is een tekenreeks die is ingesloten tussen dubbele aanhalingstekens. Dubbele aanhalingstekens in id wordt weergegeven als dubbele aanhalingstekens. Het is niet raadzaam toouse id's tussen aanhalingstekens omdat kunnen eenvoudig worden verward met een tekenreeksconstante. Gebruik indien mogelijk een gescheiden id. Hallo Hieronder volgt een voorbeeld van `<quoted_identifier>`:  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a>patroon  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a>Opmerkingen
  
`<pattern>`moet een expressie die wordt geëvalueerd als een tekenreeks zijn. Deze wordt gebruikt als een patroon voor Hallo zoals operator.      Hallo jokertekens volgende kan bevatten.  
  
-   `%`: Een tekenreeks van nul of meer tekens.  
  
-   `_`: Een enkel teken.  
  
## <a name="escapechar"></a>escape_char  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a>Opmerkingen  

`<escape_char>`moet een expressie die wordt geëvalueerd als een tekenreeks met lengte 1. Deze wordt gebruikt als een escape-teken voor Hallo zoals operator.  
  
 Bijvoorbeeld: `property LIKE 'ABC\%' ESCAPE '\'` overeenkomt met `ABC%` in plaats van een tekenreeks die met begint `ABC`.  
  
## <a name="constant"></a>constante  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a>Argumenten  
  
-   `<integer_constant>`is een reeks cijfers die niet tussen aanhalingstekens worden geplaatst en bevatten geen decimalen. Hallo-waarden worden opgeslagen als `System.Int64` intern en volg Hallo hetzelfde bereik.  
  
     Dit zijn voorbeelden van lange constanten:  
  
    ```  
    1894  
    2  
    ```  
  
-   `<decimal_constant>`is een reeks cijfers die niet tussen dubbele aanhalingstekens, en bevatten een decimaalteken. Hallo-waarden worden opgeslagen als `System.Double` intern en volg Hallo hetzelfde bereik/precisie.  
  
     Dit nummer in een toekomstige versie worden opgeslagen in een andere gegevensbron type toosupport exacte aantal semantiek, zodat u niet verstandig Hallo feit Hallo onderliggende gegevenstype is `System.Double` voor `<decimal_constant>`.  
  
     Hallo-dit zijn voorbeelden van decimale constanten:  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   `<approximate_number_constant>`is een aantal geschreven in wetenschappelijke notatie. Hallo-waarden worden opgeslagen als `System.Double` intern en volg Hallo hetzelfde bereik/precisie. Hallo hieronder vindt u voorbeelden van het geschatte aantal constanten:  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a>boolean_constant  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a>Opmerkingen  

Boole-constanten worden vertegenwoordigd door Hallo trefwoorden **TRUE** of **FALSE**. Hallo-waarden worden opgeslagen als `System.Boolean`.  
  
## <a name="stringconstant"></a>string_constant  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a>Opmerkingen  

Tekenreeksconstanten zijn ingesloten in enkele aanhalingstekens en geen geldige unicodetekens bevatten. Een enkel aanhalingsteken ingesloten in een tekenreeksconstante wordt vertegenwoordigd als twee enkele aanhalingstekens.  
  
## <a name="function"></a>Functie  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a>Opmerkingen
  
Hallo `newid()` functie retourneert een **System.Guid** die worden gegenereerd door Hallo `System.Guid.NewGuid()` methode.  
  
Hallo `property(name)` functie retourneert Hallo-waarde van Hallo-eigenschap waarnaar wordt verwezen door `name`. Hallo `name` waarde kan een geldige expressie die een string-waarde zijn.  
  
## <a name="considerations"></a>Overwegingen
  
Houd rekening met de volgende Hallo [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantiek:  
  
-   De namen van eigenschappen zijn niet hoofdlettergevoelig.  
  
-   Operators Volg C# impliciete conversie semantiek indien mogelijk.  
  
-   Systeem zijn openbare eigenschappen beschikbaar zijn in [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) exemplaren.  
  
    Houd rekening met de volgende Hallo `IS [NOT] NULL` semantiek:  
  
    -   `property IS NULL`wordt geëvalueerd als `true` als beide Hallo-eigenschap niet bestaat of de waarde van eigenschap Hallo `null`.  
  
### <a name="property-evaluation-semantics"></a>Eigenschap evaluatie semantiek  
  
-   Een poging tooevaluate een niet-bestaande systeemeigenschap genereert een [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) uitzondering.  
  
-   Een eigenschap die niet intern wordt geëvalueerd als **onbekende**.  
  
 Onbekende evaluatie in rekenkundige operatoren:  
  
-   Voor binaire operators als een Hallo links en/of rechts van operanden wordt geëvalueerd als **onbekende**, dan is Hallo resultaat **onbekende**.  
  
-   Voor unaire operators, als een operand wordt geëvalueerd als **onbekende**, dan is Hallo resultaat **onbekende**.  
  
 Onbekende evaluatie in binaire vergelijkingsoperators:  
  
-   Als een Hallo links en/of rechts van operanden wordt geëvalueerd als **onbekende**, dan is Hallo resultaat **onbekende**.  
  
 Onbekende evaluatie in `[NOT] LIKE`:  
  
-   Als een operand wordt geëvalueerd als **onbekende**, dan is Hallo resultaat **onbekende**.  
  
 Onbekende evaluatie in `[NOT] IN`:  
  
-   Als de linkeroperand hello wordt geëvalueerd als **onbekende**, dan is Hallo resultaat **onbekende**.  
  
 Onbekende evaluatie in **en** operator:  
  
```  
+---+---+---+---+  
|AND| T | F | U |  
+---+---+---+---+  
| T | T | F | U |  
+---+---+---+---+  
| F | F | F | F |  
+---+---+---+---+  
| U | U | F | U |  
+---+---+---+---+  
```  
  
 Onbekende evaluatie in **of** operator:  
  
```  
+---+---+---+---+  
|OR | T | F | U |  
+---+---+---+---+  
| T | T | T | T |  
+---+---+---+---+  
| F | T | F | U |  
+---+---+---+---+  
| U | T | U | U |  
+---+---+---+---+  
```  
  
### <a name="operator-binding-semantics"></a>Operator binding semantiek
  
-   Vergelijkingsoperators zoals `>`, `>=`, `<`, `<=`, `!=`, en `=` Volg dezelfde Hallo-semantiek als Hallo C#-operator in gegevens binding Typ aanbiedingen en impliciete conversies.  
  
-   Rekenkundige operatoren zoals `+`, `-`, `*`, `/`, en `%` Volg dezelfde Hallo-semantiek als Hallo C#-operator in gegevens binding Typ aanbiedingen en impliciete conversies.

## <a name="next-steps"></a>Volgende stappen

- [SQLFilter klasse](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [SQLRuleAction klasse](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)