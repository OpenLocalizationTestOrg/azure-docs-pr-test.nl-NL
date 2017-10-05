---
title: Verwijzing naar de SQLRuleAction in Azure | Microsoft Docs
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
ms.openlocfilehash: 7379b7f58563675f28d77928d933c0d9c7992e71
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="sqlruleaction-syntax"></a><span data-ttu-id="bc04f-103">SQLRuleAction syntaxis</span><span class="sxs-lookup"><span data-stu-id="bc04f-103">SQLRuleAction syntax</span></span>

<span data-ttu-id="bc04f-104">Een *SqlRuleAction* is een exemplaar van de [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) klasse en vertegenwoordigt set acties die zijn geschreven in SQL-taal gebaseerd syntaxis die wordt uitgevoerd op een [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="bc04f-104">A *SqlRuleAction* is an instance of the [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) class, and represents set of actions written in SQL-language based syntax that is performed against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span>   
  
<span data-ttu-id="bc04f-105">Dit onderwerp bevat informatie over de SQL-grammatica regel in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="bc04f-105">This topic lists details about the SQL rule action grammar.</span></span>  
  
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
  
## <a name="arguments"></a><span data-ttu-id="bc04f-106">Argumenten</span><span class="sxs-lookup"><span data-stu-id="bc04f-106">Arguments</span></span>  
  
-   <span data-ttu-id="bc04f-107">`<scope>`is een optionele tekenreeks die aangeeft van het bereik van de `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="bc04f-107">`<scope>` is an optional string indicating the scope of the `<property_name>`.</span></span> <span data-ttu-id="bc04f-108">Geldige waarden zijn `sys` of `user`.</span><span class="sxs-lookup"><span data-stu-id="bc04f-108">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="bc04f-109">De `sys` waarde geeft aan dat systeem bereik waar `<property_name>` is de naam van een openbare eigenschap van de [BrokeredMessage klasse](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="bc04f-109">The `sys` value indicates system scope where `<property_name>` is a public property name of the [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="bc04f-110">`user`bereik van de gebruiker geeft aan waar `<property_name>` is een sleutel van de [BrokeredMessage klasse](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) woordenlijst.</span><span class="sxs-lookup"><span data-stu-id="bc04f-110">`user` indicates user scope where `<property_name>` is a key of the [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="bc04f-111">`user`bereik is het standaardbereik als `<scope>` is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="bc04f-111">`user` scope is the default scope if `<scope>` is not specified.</span></span>  
  
### <a name="remarks"></a><span data-ttu-id="bc04f-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="bc04f-112">Remarks</span></span>  

<span data-ttu-id="bc04f-113">Een poging tot toegang tot een niet-bestaande systeemeigenschap is een fout tijdens een poging tot toegang tot een niet-bestaande gebruikerseigenschap geen fout is.</span><span class="sxs-lookup"><span data-stu-id="bc04f-113">An attempt to access a non-existent system property is an error, while an attempt to access a non-existent user property is not an error.</span></span> <span data-ttu-id="bc04f-114">In plaats daarvan wordt de eigenschap van een niet-bestaande intern geëvalueerd als een onbekende waarde.</span><span class="sxs-lookup"><span data-stu-id="bc04f-114">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="bc04f-115">Een onbekende waarde behandeld speciaal tijdens de evaluatie van de operator.</span><span class="sxs-lookup"><span data-stu-id="bc04f-115">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="bc04f-116">kubuskenmerkbinding</span><span class="sxs-lookup"><span data-stu-id="bc04f-116">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="bc04f-117">Argumenten</span><span class="sxs-lookup"><span data-stu-id="bc04f-117">Arguments</span></span>  
 <span data-ttu-id="bc04f-118">`<regular_identifier>`een tekenreeks is vertegenwoordigd door de volgende reguliere expressie:</span><span class="sxs-lookup"><span data-stu-id="bc04f-118">`<regular_identifier>` is a string represented by the following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
 <span data-ttu-id="bc04f-119">Dit betekent dat een tekenreeks die begint met een letter en wordt gevolgd door een of meer onderstrepingsteken/letter/cijfers.</span><span class="sxs-lookup"><span data-stu-id="bc04f-119">This means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
 <span data-ttu-id="bc04f-120">`[:IsLetter:]`betekent een Unicode-teken is aangemerkt als een Unicode-letter.</span><span class="sxs-lookup"><span data-stu-id="bc04f-120">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="bc04f-121">`System.Char.IsLetter(c)`retourneert `true` als `c` is een Unicode-letter.</span><span class="sxs-lookup"><span data-stu-id="bc04f-121">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
 <span data-ttu-id="bc04f-122">`[:IsDigit:]`betekent een Unicode-teken is aangemerkt als een decimaal cijfer.</span><span class="sxs-lookup"><span data-stu-id="bc04f-122">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="bc04f-123">`System.Char.IsDigit(c)`retourneert `true` als `c` een Unicode-teken.</span><span class="sxs-lookup"><span data-stu-id="bc04f-123">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
 <span data-ttu-id="bc04f-124">Een `<regular_identifier>` mag geen gereserveerd trefwoord.</span><span class="sxs-lookup"><span data-stu-id="bc04f-124">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
 <span data-ttu-id="bc04f-125">`<delimited_identifier>`is een tekenreeks die is ingesloten door horizontaal vierkante haken ([]).</span><span class="sxs-lookup"><span data-stu-id="bc04f-125">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="bc04f-126">Een vierkant haakje sluiten wordt weergegeven als twee rechts vierkante haken.</span><span class="sxs-lookup"><span data-stu-id="bc04f-126">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="bc04f-127">Hieronder vindt u voorbeelden van `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="bc04f-127">The following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
 <span data-ttu-id="bc04f-128">`<quoted_identifier>`is een tekenreeks die is ingesloten tussen dubbele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="bc04f-128">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="bc04f-129">Dubbele aanhalingstekens in id wordt weergegeven als dubbele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="bc04f-129">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="bc04f-130">Dit wordt niet aanbevolen voor id's tussen aanhalingstekens omdat kunnen eenvoudig worden verward met een tekenreeksconstante.</span><span class="sxs-lookup"><span data-stu-id="bc04f-130">It is not recommended to use quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="bc04f-131">Gebruik indien mogelijk een gescheiden id.</span><span class="sxs-lookup"><span data-stu-id="bc04f-131">Use a delimited identifier if possible.</span></span> <span data-ttu-id="bc04f-132">Hieronder volgt een voorbeeld van `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="bc04f-132">The following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="bc04f-133">patroon</span><span class="sxs-lookup"><span data-stu-id="bc04f-133">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="bc04f-134">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="bc04f-134">Remarks</span></span>
  
 <span data-ttu-id="bc04f-135">`<pattern>`moet een expressie die wordt geëvalueerd als een tekenreeks zijn.</span><span class="sxs-lookup"><span data-stu-id="bc04f-135">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="bc04f-136">Deze wordt gebruikt als een patroon voor de LIKE-operator.</span><span class="sxs-lookup"><span data-stu-id="bc04f-136">It is used as a pattern for the LIKE operator.</span></span>      <span data-ttu-id="bc04f-137">Dit kan de volgende tekens bevatten:</span><span class="sxs-lookup"><span data-stu-id="bc04f-137">It can contain the following wildcard characters:</span></span>  
  
-   <span data-ttu-id="bc04f-138">`%`: Een tekenreeks van nul of meer tekens.</span><span class="sxs-lookup"><span data-stu-id="bc04f-138">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="bc04f-139">`_`: Een enkel teken.</span><span class="sxs-lookup"><span data-stu-id="bc04f-139">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="bc04f-140">escape_char</span><span class="sxs-lookup"><span data-stu-id="bc04f-140">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="bc04f-141">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="bc04f-141">Remarks</span></span>
  
 <span data-ttu-id="bc04f-142">`<escape_char>`moet een expressie die wordt geëvalueerd als een tekenreeks met lengte 1.</span><span class="sxs-lookup"><span data-stu-id="bc04f-142">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="bc04f-143">Deze wordt gebruikt als een escape-teken voor de LIKE-operator.</span><span class="sxs-lookup"><span data-stu-id="bc04f-143">It is used as an escape character for the LIKE operator.</span></span>  
  
 <span data-ttu-id="bc04f-144">Bijvoorbeeld: `property LIKE 'ABC\%' ESCAPE '\'` overeenkomt met `ABC%` in plaats van een tekenreeks die met begint `ABC`.</span><span class="sxs-lookup"><span data-stu-id="bc04f-144">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="bc04f-145">constante</span><span class="sxs-lookup"><span data-stu-id="bc04f-145">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="bc04f-146">Argumenten</span><span class="sxs-lookup"><span data-stu-id="bc04f-146">Arguments</span></span>  
  
-   <span data-ttu-id="bc04f-147">`<integer_constant>`is een reeks cijfers die niet tussen aanhalingstekens worden geplaatst en bevatten geen decimalen.</span><span class="sxs-lookup"><span data-stu-id="bc04f-147">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="bc04f-148">De waarden worden opgeslagen als `System.Int64` intern en doe hetzelfde bereik.</span><span class="sxs-lookup"><span data-stu-id="bc04f-148">The values are stored as `System.Int64` internally, and follow the same range.</span></span>  
  
     <span data-ttu-id="bc04f-149">Hier volgen enkele voorbeelden van lange-constanten zijn:</span><span class="sxs-lookup"><span data-stu-id="bc04f-149">The following are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="bc04f-150">`<decimal_constant>`is een reeks cijfers die niet tussen dubbele aanhalingstekens, en bevatten een decimaalteken.</span><span class="sxs-lookup"><span data-stu-id="bc04f-150">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="bc04f-151">De waarden worden opgeslagen als `System.Double` intern, en volgt u de hetzelfde bereik/precisie.</span><span class="sxs-lookup"><span data-stu-id="bc04f-151">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span>  
  
     <span data-ttu-id="bc04f-152">Dit nummer in een toekomstige versie worden opgeslagen in een ander gegevenstype voor de ondersteuning van exacte aantal semantiek, dus u dient niet te vertrouwen op het feit de onderliggende gegevenstype is `System.Double` voor `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="bc04f-152">In a future version, this number might be stored in a different data type to support exact number semantics, so you should not rely on the fact the underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="bc04f-153">Hier volgen enkele voorbeelden van decimal-constanten zijn:</span><span class="sxs-lookup"><span data-stu-id="bc04f-153">The following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="bc04f-154">`<approximate_number_constant>`is een aantal geschreven in wetenschappelijke notatie.</span><span class="sxs-lookup"><span data-stu-id="bc04f-154">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="bc04f-155">De waarden worden opgeslagen als `System.Double` intern, en volgt u de hetzelfde bereik/precisie.</span><span class="sxs-lookup"><span data-stu-id="bc04f-155">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span> <span data-ttu-id="bc04f-156">Hier volgen enkele voorbeelden van het geschatte aantal constanten:</span><span class="sxs-lookup"><span data-stu-id="bc04f-156">The following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="bc04f-157">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="bc04f-157">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="bc04f-158">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="bc04f-158">Remarks</span></span>
  
<span data-ttu-id="bc04f-159">Boole-constanten worden vertegenwoordigd door de trefwoorden `TRUE` of `FALSE`.</span><span class="sxs-lookup"><span data-stu-id="bc04f-159">Boolean constants are represented by the keywords `TRUE` or `FALSE`.</span></span> <span data-ttu-id="bc04f-160">De waarden worden opgeslagen als `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="bc04f-160">The values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="bc04f-161">string_constant</span><span class="sxs-lookup"><span data-stu-id="bc04f-161">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="bc04f-162">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="bc04f-162">Remarks</span></span>
  
<span data-ttu-id="bc04f-163">Tekenreeksconstanten zijn ingesloten in enkele aanhalingstekens en geen geldige unicodetekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="bc04f-163">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="bc04f-164">Een enkel aanhalingsteken ingesloten in een tekenreeksconstante wordt vertegenwoordigd als twee enkele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="bc04f-164">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="bc04f-165">Functie</span><span class="sxs-lookup"><span data-stu-id="bc04f-165">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="bc04f-166">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="bc04f-166">Remarks</span></span>  

<span data-ttu-id="bc04f-167">De `newid()` functie retourneert een **System.Guid** die worden gegenereerd door de `System.Guid.NewGuid()` methode.</span><span class="sxs-lookup"><span data-stu-id="bc04f-167">The `newid()` function returns a **System.Guid** generated by the `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="bc04f-168">De `property(name)` functie retourneert de waarde van de eigenschap waarnaar wordt verwezen door `name`.</span><span class="sxs-lookup"><span data-stu-id="bc04f-168">The `property(name)` function returns the value of the property referenced by `name`.</span></span> <span data-ttu-id="bc04f-169">De `name` waarde kan een geldige expressie die een string-waarde zijn.</span><span class="sxs-lookup"><span data-stu-id="bc04f-169">The `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="bc04f-170">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="bc04f-170">Considerations</span></span>

- <span data-ttu-id="bc04f-171">Een nieuwe eigenschap maken of bijwerken van de waarde van een bestaande eigenschap worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bc04f-171">SET is used to create a new property or update the value of an existing property.</span></span>
- <span data-ttu-id="bc04f-172">VERWIJDEREN wordt gebruikt om een eigenschap te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="bc04f-172">REMOVE is used to remove a property.</span></span>
- <span data-ttu-id="bc04f-173">SET voert impliciete conversie indien mogelijk wanneer het Expressietype en het bestaande eigenschapstype verschillen.</span><span class="sxs-lookup"><span data-stu-id="bc04f-173">SET performs implicit conversion if possible when the expression type and the existing property type are different.</span></span>
- <span data-ttu-id="bc04f-174">Actie mislukt als niet-bestaande Systeemeigenschappen zijn waarnaar wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="bc04f-174">Action fails if non-existent system properties were referenced.</span></span>
- <span data-ttu-id="bc04f-175">Actie mislukt niet als niet-bestaande gebruikerseigenschappen zijn waarnaar wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="bc04f-175">Action does not fail if non-existent user properties were referenced.</span></span>
- <span data-ttu-id="bc04f-176">Een eigenschap van een niet-bestaande wordt geëvalueerd als 'Onbekend' intern, volgt dezelfde heeft als [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) bij het evalueren van operators.</span><span class="sxs-lookup"><span data-stu-id="bc04f-176">A non-existent user property is evaluated as "Unknown" internally, following the same semantics as [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) when evaluating operators.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc04f-177">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bc04f-177">Next steps</span></span>

- [<span data-ttu-id="bc04f-178">SQLRuleAction klasse</span><span class="sxs-lookup"><span data-stu-id="bc04f-178">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)
- [<span data-ttu-id="bc04f-179">SQLFilter klasse</span><span class="sxs-lookup"><span data-stu-id="bc04f-179">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
