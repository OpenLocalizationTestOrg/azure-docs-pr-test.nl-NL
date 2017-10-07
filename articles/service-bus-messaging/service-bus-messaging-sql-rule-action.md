---
title: verwijzing naar de aaaSQLRuleAction in Azure | Microsoft Docs
description: Gegevens over SQLRuleAction grammatica.
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
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 8ef281f942847bcc535b83a5ffb30d03539734f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sqlruleaction-syntax"></a>SQLRuleAction syntaxis

Een *SqlRuleAction* is een exemplaar van Hallo [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) klasse en vertegenwoordigt set acties die zijn geschreven in SQL-taal gebaseerd syntaxis die wordt uitgevoerd op een [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).   
  
Dit onderwerp bevat informatie over Hallo SQL-grammatica voor regel in te grijpen.  
  
```  
<statements> ::=
    <statement> [, ...n]  
  
```  
  
```  
<statement> ::=
    <action> [;]
    Remarks
    -------
    Semicolon is optional.  
  
```  
  
```  
<action> ::=
    SET <property> = <expression>
    REMOVE <property>  
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
  
### <a name="remarks"></a>Opmerkingen  

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
  
 Dit betekent dat een tekenreeks die begint met een letter en wordt gevolgd door een of meer onderstrepingsteken/letter/cijfers.  
  
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
  
     Hallo hieronder vindt u voorbeelden van lange-constanten zijn:  
  
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
  
Boole-constanten worden vertegenwoordigd door Hallo trefwoorden `TRUE` of `FALSE`. Hallo-waarden worden opgeslagen als `System.Boolean`.  
  
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

- Is de gebruikte toocreate een nieuwe eigenschap of update Hallo waarde van een bestaande eigenschap.
- VERWIJDEREN is gebruikte tooremove een eigenschap.
- SET voert impliciete conversie indien mogelijk wanneer Hallo Expressietype en bestaande eigenschapstype Hallo verschillen.
- Actie mislukt als niet-bestaande Systeemeigenschappen zijn waarnaar wordt verwezen.
- Actie mislukt niet als niet-bestaande gebruikerseigenschappen zijn waarnaar wordt verwezen.
- Een eigenschap van een niet-bestaande wordt geëvalueerd als 'Onbekend' intern, volgende Hallo dezelfde semantiek als [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) bij het evalueren van operators.

## <a name="next-steps"></a>Volgende stappen

- [SQLRuleAction klasse](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)
- [SQLFilter klasse](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
