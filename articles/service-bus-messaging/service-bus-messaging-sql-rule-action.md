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
# <a name="sqlruleaction-syntax"></a><span data-ttu-id="63051-103">SQLRuleAction syntaxis</span><span class="sxs-lookup"><span data-stu-id="63051-103">SQLRuleAction syntax</span></span>

<span data-ttu-id="63051-104">Een *SqlRuleAction* is een exemplaar van Hallo [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) klasse en vertegenwoordigt set acties die zijn geschreven in SQL-taal gebaseerd syntaxis die wordt uitgevoerd op een [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="63051-104">A *SqlRuleAction* is an instance of hello [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) class, and represents set of actions written in SQL-language based syntax that is performed against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span>   
  
<span data-ttu-id="63051-105">Dit onderwerp bevat informatie over Hallo SQL-grammatica voor regel in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="63051-105">This topic lists details about hello SQL rule action grammar.</span></span>  
  
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
  
## <a name="arguments"></a><span data-ttu-id="63051-106">Argumenten</span><span class="sxs-lookup"><span data-stu-id="63051-106">Arguments</span></span>  
  
-   <span data-ttu-id="63051-107">`<scope>`is een optionele tekenreeks die aangeeft Hallo bereik van Hallo `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="63051-107">`<scope>` is an optional string indicating hello scope of hello `<property_name>`.</span></span> <span data-ttu-id="63051-108">Geldige waarden zijn `sys` of `user`.</span><span class="sxs-lookup"><span data-stu-id="63051-108">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="63051-109">Hallo `sys` waarde geeft aan dat systeem bereik waar `<property_name>` is de naam van een openbare eigenschap Hallo [BrokeredMessage klasse](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="63051-109">hello `sys` value indicates system scope where `<property_name>` is a public property name of hello [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="63051-110">`user`bereik van de gebruiker geeft aan waar `<property_name>` is een sleutel van Hallo [BrokeredMessage klasse](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) woordenlijst.</span><span class="sxs-lookup"><span data-stu-id="63051-110">`user` indicates user scope where `<property_name>` is a key of hello [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="63051-111">`user`in het bereik zijn Hallo standaardbereik als `<scope>` is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="63051-111">`user` scope is hello default scope if `<scope>` is not specified.</span></span>  
  
### <a name="remarks"></a><span data-ttu-id="63051-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="63051-112">Remarks</span></span>  

<span data-ttu-id="63051-113">Een poging tooaccess een niet-bestaande systeemeigenschap is een fout tijdens een poging een niet-bestaande tooaccess gebruiker-eigenschap geen fout is.</span><span class="sxs-lookup"><span data-stu-id="63051-113">An attempt tooaccess a non-existent system property is an error, while an attempt tooaccess a non-existent user property is not an error.</span></span> <span data-ttu-id="63051-114">In plaats daarvan wordt de eigenschap van een niet-bestaande intern geëvalueerd als een onbekende waarde.</span><span class="sxs-lookup"><span data-stu-id="63051-114">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="63051-115">Een onbekende waarde behandeld speciaal tijdens de evaluatie van de operator.</span><span class="sxs-lookup"><span data-stu-id="63051-115">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="63051-116">kubuskenmerkbinding</span><span class="sxs-lookup"><span data-stu-id="63051-116">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="63051-117">Argumenten</span><span class="sxs-lookup"><span data-stu-id="63051-117">Arguments</span></span>  
 <span data-ttu-id="63051-118">`<regular_identifier>`is een tekenreeks die wordt vertegenwoordigd door Hallo volgende reguliere expressie:</span><span class="sxs-lookup"><span data-stu-id="63051-118">`<regular_identifier>` is a string represented by hello following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
 <span data-ttu-id="63051-119">Dit betekent dat een tekenreeks die begint met een letter en wordt gevolgd door een of meer onderstrepingsteken/letter/cijfers.</span><span class="sxs-lookup"><span data-stu-id="63051-119">This means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
 <span data-ttu-id="63051-120">`[:IsLetter:]`betekent een Unicode-teken is aangemerkt als een Unicode-letter.</span><span class="sxs-lookup"><span data-stu-id="63051-120">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="63051-121">`System.Char.IsLetter(c)`retourneert `true` als `c` is een Unicode-letter.</span><span class="sxs-lookup"><span data-stu-id="63051-121">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
 <span data-ttu-id="63051-122">`[:IsDigit:]`betekent een Unicode-teken is aangemerkt als een decimaal cijfer.</span><span class="sxs-lookup"><span data-stu-id="63051-122">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="63051-123">`System.Char.IsDigit(c)`retourneert `true` als `c` een Unicode-teken.</span><span class="sxs-lookup"><span data-stu-id="63051-123">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
 <span data-ttu-id="63051-124">Een `<regular_identifier>` mag geen gereserveerd trefwoord.</span><span class="sxs-lookup"><span data-stu-id="63051-124">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
 <span data-ttu-id="63051-125">`<delimited_identifier>`is een tekenreeks die is ingesloten door horizontaal vierkante haken ([]).</span><span class="sxs-lookup"><span data-stu-id="63051-125">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="63051-126">Een vierkant haakje sluiten wordt weergegeven als twee rechts vierkante haken.</span><span class="sxs-lookup"><span data-stu-id="63051-126">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="63051-127">Hallo hieronder vindt u voorbeelden van `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="63051-127">hello following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
 <span data-ttu-id="63051-128">`<quoted_identifier>`is een tekenreeks die is ingesloten tussen dubbele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="63051-128">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="63051-129">Dubbele aanhalingstekens in id wordt weergegeven als dubbele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="63051-129">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="63051-130">Het is niet raadzaam toouse id's tussen aanhalingstekens omdat kunnen eenvoudig worden verward met een tekenreeksconstante.</span><span class="sxs-lookup"><span data-stu-id="63051-130">It is not recommended toouse quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="63051-131">Gebruik indien mogelijk een gescheiden id.</span><span class="sxs-lookup"><span data-stu-id="63051-131">Use a delimited identifier if possible.</span></span> <span data-ttu-id="63051-132">Hallo Hieronder volgt een voorbeeld van `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="63051-132">hello following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="63051-133">patroon</span><span class="sxs-lookup"><span data-stu-id="63051-133">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="63051-134">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="63051-134">Remarks</span></span>
  
 <span data-ttu-id="63051-135">`<pattern>`moet een expressie die wordt geëvalueerd als een tekenreeks zijn.</span><span class="sxs-lookup"><span data-stu-id="63051-135">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="63051-136">Deze wordt gebruikt als een patroon voor Hallo zoals operator.</span><span class="sxs-lookup"><span data-stu-id="63051-136">It is used as a pattern for hello LIKE operator.</span></span>      <span data-ttu-id="63051-137">Hallo jokertekens volgende kan bevatten.</span><span class="sxs-lookup"><span data-stu-id="63051-137">It can contain hello following wildcard characters:</span></span>  
  
-   <span data-ttu-id="63051-138">`%`: Een tekenreeks van nul of meer tekens.</span><span class="sxs-lookup"><span data-stu-id="63051-138">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="63051-139">`_`: Een enkel teken.</span><span class="sxs-lookup"><span data-stu-id="63051-139">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="63051-140">escape_char</span><span class="sxs-lookup"><span data-stu-id="63051-140">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="63051-141">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="63051-141">Remarks</span></span>
  
 <span data-ttu-id="63051-142">`<escape_char>`moet een expressie die wordt geëvalueerd als een tekenreeks met lengte 1.</span><span class="sxs-lookup"><span data-stu-id="63051-142">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="63051-143">Deze wordt gebruikt als een escape-teken voor Hallo zoals operator.</span><span class="sxs-lookup"><span data-stu-id="63051-143">It is used as an escape character for hello LIKE operator.</span></span>  
  
 <span data-ttu-id="63051-144">Bijvoorbeeld: `property LIKE 'ABC\%' ESCAPE '\'` overeenkomt met `ABC%` in plaats van een tekenreeks die met begint `ABC`.</span><span class="sxs-lookup"><span data-stu-id="63051-144">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="63051-145">constante</span><span class="sxs-lookup"><span data-stu-id="63051-145">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="63051-146">Argumenten</span><span class="sxs-lookup"><span data-stu-id="63051-146">Arguments</span></span>  
  
-   <span data-ttu-id="63051-147">`<integer_constant>`is een reeks cijfers die niet tussen aanhalingstekens worden geplaatst en bevatten geen decimalen.</span><span class="sxs-lookup"><span data-stu-id="63051-147">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="63051-148">Hallo-waarden worden opgeslagen als `System.Int64` intern en volg Hallo hetzelfde bereik.</span><span class="sxs-lookup"><span data-stu-id="63051-148">hello values are stored as `System.Int64` internally, and follow hello same range.</span></span>  
  
     <span data-ttu-id="63051-149">Hallo hieronder vindt u voorbeelden van lange-constanten zijn:</span><span class="sxs-lookup"><span data-stu-id="63051-149">hello following are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="63051-150">`<decimal_constant>`is een reeks cijfers die niet tussen dubbele aanhalingstekens, en bevatten een decimaalteken.</span><span class="sxs-lookup"><span data-stu-id="63051-150">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="63051-151">Hallo-waarden worden opgeslagen als `System.Double` intern en volg Hallo hetzelfde bereik/precisie.</span><span class="sxs-lookup"><span data-stu-id="63051-151">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span>  
  
     <span data-ttu-id="63051-152">Dit nummer in een toekomstige versie worden opgeslagen in een andere gegevensbron type toosupport exacte aantal semantiek, zodat u niet verstandig Hallo feit Hallo onderliggende gegevenstype is `System.Double` voor `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="63051-152">In a future version, this number might be stored in a different data type toosupport exact number semantics, so you should not rely on hello fact hello underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="63051-153">Hallo-dit zijn voorbeelden van decimale constanten:</span><span class="sxs-lookup"><span data-stu-id="63051-153">hello following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="63051-154">`<approximate_number_constant>`is een aantal geschreven in wetenschappelijke notatie.</span><span class="sxs-lookup"><span data-stu-id="63051-154">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="63051-155">Hallo-waarden worden opgeslagen als `System.Double` intern en volg Hallo hetzelfde bereik/precisie.</span><span class="sxs-lookup"><span data-stu-id="63051-155">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span> <span data-ttu-id="63051-156">Hallo hieronder vindt u voorbeelden van het geschatte aantal constanten:</span><span class="sxs-lookup"><span data-stu-id="63051-156">hello following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="63051-157">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="63051-157">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="63051-158">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="63051-158">Remarks</span></span>
  
<span data-ttu-id="63051-159">Boole-constanten worden vertegenwoordigd door Hallo trefwoorden `TRUE` of `FALSE`.</span><span class="sxs-lookup"><span data-stu-id="63051-159">Boolean constants are represented by hello keywords `TRUE` or `FALSE`.</span></span> <span data-ttu-id="63051-160">Hallo-waarden worden opgeslagen als `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="63051-160">hello values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="63051-161">string_constant</span><span class="sxs-lookup"><span data-stu-id="63051-161">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="63051-162">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="63051-162">Remarks</span></span>
  
<span data-ttu-id="63051-163">Tekenreeksconstanten zijn ingesloten in enkele aanhalingstekens en geen geldige unicodetekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="63051-163">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="63051-164">Een enkel aanhalingsteken ingesloten in een tekenreeksconstante wordt vertegenwoordigd als twee enkele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="63051-164">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="63051-165">Functie</span><span class="sxs-lookup"><span data-stu-id="63051-165">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="63051-166">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="63051-166">Remarks</span></span>  

<span data-ttu-id="63051-167">Hallo `newid()` functie retourneert een **System.Guid** die worden gegenereerd door Hallo `System.Guid.NewGuid()` methode.</span><span class="sxs-lookup"><span data-stu-id="63051-167">hello `newid()` function returns a **System.Guid** generated by hello `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="63051-168">Hallo `property(name)` functie retourneert Hallo-waarde van Hallo-eigenschap waarnaar wordt verwezen door `name`.</span><span class="sxs-lookup"><span data-stu-id="63051-168">hello `property(name)` function returns hello value of hello property referenced by `name`.</span></span> <span data-ttu-id="63051-169">Hallo `name` waarde kan een geldige expressie die een string-waarde zijn.</span><span class="sxs-lookup"><span data-stu-id="63051-169">hello `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="63051-170">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="63051-170">Considerations</span></span>

- <span data-ttu-id="63051-171">Is de gebruikte toocreate een nieuwe eigenschap of update Hallo waarde van een bestaande eigenschap.</span><span class="sxs-lookup"><span data-stu-id="63051-171">SET is used toocreate a new property or update hello value of an existing property.</span></span>
- <span data-ttu-id="63051-172">VERWIJDEREN is gebruikte tooremove een eigenschap.</span><span class="sxs-lookup"><span data-stu-id="63051-172">REMOVE is used tooremove a property.</span></span>
- <span data-ttu-id="63051-173">SET voert impliciete conversie indien mogelijk wanneer Hallo Expressietype en bestaande eigenschapstype Hallo verschillen.</span><span class="sxs-lookup"><span data-stu-id="63051-173">SET performs implicit conversion if possible when hello expression type and hello existing property type are different.</span></span>
- <span data-ttu-id="63051-174">Actie mislukt als niet-bestaande Systeemeigenschappen zijn waarnaar wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="63051-174">Action fails if non-existent system properties were referenced.</span></span>
- <span data-ttu-id="63051-175">Actie mislukt niet als niet-bestaande gebruikerseigenschappen zijn waarnaar wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="63051-175">Action does not fail if non-existent user properties were referenced.</span></span>
- <span data-ttu-id="63051-176">Een eigenschap van een niet-bestaande wordt geëvalueerd als 'Onbekend' intern, volgende Hallo dezelfde semantiek als [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) bij het evalueren van operators.</span><span class="sxs-lookup"><span data-stu-id="63051-176">A non-existent user property is evaluated as "Unknown" internally, following hello same semantics as [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) when evaluating operators.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63051-177">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="63051-177">Next steps</span></span>

- [<span data-ttu-id="63051-178">SQLRuleAction klasse</span><span class="sxs-lookup"><span data-stu-id="63051-178">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)
- [<span data-ttu-id="63051-179">SQLFilter klasse</span><span class="sxs-lookup"><span data-stu-id="63051-179">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
