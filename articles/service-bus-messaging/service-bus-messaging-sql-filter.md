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
# <a name="sqlfilter-syntax"></a><span data-ttu-id="cdf1d-103">SQLFilter syntaxis</span><span class="sxs-lookup"><span data-stu-id="cdf1d-103">SQLFilter syntax</span></span>

<span data-ttu-id="cdf1d-104">Een *SqlFilter* is een exemplaar van Hallo [SqlFilter klasse](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), en geeft u een SQL-filter op basis van taal-expressie die wordt geëvalueerd op basis van een [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="cdf1d-104">A *SqlFilter* is an instance of hello [SqlFilter class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), and represents a SQL language-based filter expression that is evaluated against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="cdf1d-105">Een SqlFilter ondersteunt een subset van Hallo SQL-92 standaard.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-105">A SqlFilter supports a subset of hello SQL-92 standard.</span></span>  
  
 <span data-ttu-id="cdf1d-106">Dit onderwerp bevat informatie over SqlFilter grammatica.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-106">This topic lists details about SqlFilter grammar.</span></span>  
  
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
  
## <a name="arguments"></a><span data-ttu-id="cdf1d-107">Argumenten</span><span class="sxs-lookup"><span data-stu-id="cdf1d-107">Arguments</span></span>  
  
-   <span data-ttu-id="cdf1d-108">`<scope>`is een optionele tekenreeks die aangeeft Hallo bereik van Hallo `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-108">`<scope>` is an optional string indicating hello scope of hello `<property_name>`.</span></span> <span data-ttu-id="cdf1d-109">Geldige waarden zijn `sys` of `user`.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-109">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="cdf1d-110">Hallo `sys` waarde geeft aan dat systeem bereik waar `<property_name>` is de naam van een openbare eigenschap Hallo [BrokeredMessage klasse](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="cdf1d-110">hello `sys` value indicates system scope where `<property_name>` is a public property name of hello [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="cdf1d-111">`user`bereik van de gebruiker geeft aan waar `<property_name>` is een sleutel van Hallo [BrokeredMessage klasse](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) woordenlijst.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-111">`user` indicates user scope where `<property_name>` is a key of hello [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="cdf1d-112">`user`in het bereik zijn Hallo standaardbereik als `<scope>` is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-112">`user` scope is hello default scope if `<scope>` is not specified.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="cdf1d-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="cdf1d-113">Remarks</span></span>

<span data-ttu-id="cdf1d-114">Een poging tooaccess een niet-bestaande systeemeigenschap is een fout tijdens een poging een niet-bestaande tooaccess gebruiker-eigenschap geen fout is.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-114">An attempt tooaccess a non-existent system property is an error, while an attempt tooaccess a non-existent user property is not an error.</span></span> <span data-ttu-id="cdf1d-115">In plaats daarvan wordt de eigenschap van een niet-bestaande intern geëvalueerd als een onbekende waarde.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-115">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="cdf1d-116">Een onbekende waarde behandeld speciaal tijdens de evaluatie van de operator.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-116">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="cdf1d-117">kubuskenmerkbinding</span><span class="sxs-lookup"><span data-stu-id="cdf1d-117">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="cdf1d-118">Argumenten</span><span class="sxs-lookup"><span data-stu-id="cdf1d-118">Arguments</span></span>  

 <span data-ttu-id="cdf1d-119">`<regular_identifier>`is een tekenreeks die wordt vertegenwoordigd door Hallo volgende reguliere expressie:</span><span class="sxs-lookup"><span data-stu-id="cdf1d-119">`<regular_identifier>` is a string represented by hello following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
<span data-ttu-id="cdf1d-120">Deze grammatica betekent een tekenreeks die begint met een letter en wordt gevolgd door een of meer onderstrepingsteken/letter/cijfers.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-120">This grammar means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
<span data-ttu-id="cdf1d-121">`[:IsLetter:]`betekent een Unicode-teken is aangemerkt als een Unicode-letter.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-121">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="cdf1d-122">`System.Char.IsLetter(c)`retourneert `true` als `c` is een Unicode-letter.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-122">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
<span data-ttu-id="cdf1d-123">`[:IsDigit:]`betekent een Unicode-teken is aangemerkt als een decimaal cijfer.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-123">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="cdf1d-124">`System.Char.IsDigit(c)`retourneert `true` als `c` een Unicode-teken.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-124">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
<span data-ttu-id="cdf1d-125">Een `<regular_identifier>` mag geen gereserveerd trefwoord.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-125">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
<span data-ttu-id="cdf1d-126">`<delimited_identifier>`is een tekenreeks die is ingesloten door horizontaal vierkante haken ([]).</span><span class="sxs-lookup"><span data-stu-id="cdf1d-126">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="cdf1d-127">Een vierkant haakje sluiten wordt weergegeven als twee rechts vierkante haken.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-127">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="cdf1d-128">Hallo hieronder vindt u voorbeelden van `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="cdf1d-128">hello following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
<span data-ttu-id="cdf1d-129">`<quoted_identifier>`is een tekenreeks die is ingesloten tussen dubbele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-129">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="cdf1d-130">Dubbele aanhalingstekens in id wordt weergegeven als dubbele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-130">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="cdf1d-131">Het is niet raadzaam toouse id's tussen aanhalingstekens omdat kunnen eenvoudig worden verward met een tekenreeksconstante.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-131">It is not recommended toouse quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="cdf1d-132">Gebruik indien mogelijk een gescheiden id.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-132">Use a delimited identifier if possible.</span></span> <span data-ttu-id="cdf1d-133">Hallo Hieronder volgt een voorbeeld van `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="cdf1d-133">hello following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="cdf1d-134">patroon</span><span class="sxs-lookup"><span data-stu-id="cdf1d-134">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="cdf1d-135">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="cdf1d-135">Remarks</span></span>
  
<span data-ttu-id="cdf1d-136">`<pattern>`moet een expressie die wordt geëvalueerd als een tekenreeks zijn.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-136">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="cdf1d-137">Deze wordt gebruikt als een patroon voor Hallo zoals operator.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-137">It is used as a pattern for hello LIKE operator.</span></span>      <span data-ttu-id="cdf1d-138">Hallo jokertekens volgende kan bevatten.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-138">It can contain hello following wildcard characters:</span></span>  
  
-   <span data-ttu-id="cdf1d-139">`%`: Een tekenreeks van nul of meer tekens.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-139">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="cdf1d-140">`_`: Een enkel teken.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-140">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="cdf1d-141">escape_char</span><span class="sxs-lookup"><span data-stu-id="cdf1d-141">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="cdf1d-142">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="cdf1d-142">Remarks</span></span>  

<span data-ttu-id="cdf1d-143">`<escape_char>`moet een expressie die wordt geëvalueerd als een tekenreeks met lengte 1.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-143">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="cdf1d-144">Deze wordt gebruikt als een escape-teken voor Hallo zoals operator.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-144">It is used as an escape character for hello LIKE operator.</span></span>  
  
 <span data-ttu-id="cdf1d-145">Bijvoorbeeld: `property LIKE 'ABC\%' ESCAPE '\'` overeenkomt met `ABC%` in plaats van een tekenreeks die met begint `ABC`.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-145">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="cdf1d-146">constante</span><span class="sxs-lookup"><span data-stu-id="cdf1d-146">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="cdf1d-147">Argumenten</span><span class="sxs-lookup"><span data-stu-id="cdf1d-147">Arguments</span></span>  
  
-   <span data-ttu-id="cdf1d-148">`<integer_constant>`is een reeks cijfers die niet tussen aanhalingstekens worden geplaatst en bevatten geen decimalen.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-148">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="cdf1d-149">Hallo-waarden worden opgeslagen als `System.Int64` intern en volg Hallo hetzelfde bereik.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-149">hello values are stored as `System.Int64` internally, and follow hello same range.</span></span>  
  
     <span data-ttu-id="cdf1d-150">Dit zijn voorbeelden van lange constanten:</span><span class="sxs-lookup"><span data-stu-id="cdf1d-150">These are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="cdf1d-151">`<decimal_constant>`is een reeks cijfers die niet tussen dubbele aanhalingstekens, en bevatten een decimaalteken.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-151">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="cdf1d-152">Hallo-waarden worden opgeslagen als `System.Double` intern en volg Hallo hetzelfde bereik/precisie.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-152">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span>  
  
     <span data-ttu-id="cdf1d-153">Dit nummer in een toekomstige versie worden opgeslagen in een andere gegevensbron type toosupport exacte aantal semantiek, zodat u niet verstandig Hallo feit Hallo onderliggende gegevenstype is `System.Double` voor `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-153">In a future version, this number might be stored in a different data type toosupport exact number semantics, so you should not rely on hello fact hello underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="cdf1d-154">Hallo-dit zijn voorbeelden van decimale constanten:</span><span class="sxs-lookup"><span data-stu-id="cdf1d-154">hello following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="cdf1d-155">`<approximate_number_constant>`is een aantal geschreven in wetenschappelijke notatie.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-155">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="cdf1d-156">Hallo-waarden worden opgeslagen als `System.Double` intern en volg Hallo hetzelfde bereik/precisie.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-156">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span> <span data-ttu-id="cdf1d-157">Hallo hieronder vindt u voorbeelden van het geschatte aantal constanten:</span><span class="sxs-lookup"><span data-stu-id="cdf1d-157">hello following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="cdf1d-158">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="cdf1d-158">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="cdf1d-159">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="cdf1d-159">Remarks</span></span>  

<span data-ttu-id="cdf1d-160">Boole-constanten worden vertegenwoordigd door Hallo trefwoorden **TRUE** of **FALSE**.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-160">Boolean constants are represented by hello keywords **TRUE** or **FALSE**.</span></span> <span data-ttu-id="cdf1d-161">Hallo-waarden worden opgeslagen als `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-161">hello values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="cdf1d-162">string_constant</span><span class="sxs-lookup"><span data-stu-id="cdf1d-162">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="cdf1d-163">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="cdf1d-163">Remarks</span></span>  

<span data-ttu-id="cdf1d-164">Tekenreeksconstanten zijn ingesloten in enkele aanhalingstekens en geen geldige unicodetekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-164">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="cdf1d-165">Een enkel aanhalingsteken ingesloten in een tekenreeksconstante wordt vertegenwoordigd als twee enkele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-165">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="cdf1d-166">Functie</span><span class="sxs-lookup"><span data-stu-id="cdf1d-166">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="cdf1d-167">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="cdf1d-167">Remarks</span></span>
  
<span data-ttu-id="cdf1d-168">Hallo `newid()` functie retourneert een **System.Guid** die worden gegenereerd door Hallo `System.Guid.NewGuid()` methode.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-168">hello `newid()` function returns a **System.Guid** generated by hello `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="cdf1d-169">Hallo `property(name)` functie retourneert Hallo-waarde van Hallo-eigenschap waarnaar wordt verwezen door `name`.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-169">hello `property(name)` function returns hello value of hello property referenced by `name`.</span></span> <span data-ttu-id="cdf1d-170">Hallo `name` waarde kan een geldige expressie die een string-waarde zijn.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-170">hello `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="cdf1d-171">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="cdf1d-171">Considerations</span></span>
  
<span data-ttu-id="cdf1d-172">Houd rekening met de volgende Hallo [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantiek:</span><span class="sxs-lookup"><span data-stu-id="cdf1d-172">Consider hello following [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantics:</span></span>  
  
-   <span data-ttu-id="cdf1d-173">De namen van eigenschappen zijn niet hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-173">Property names are case-insensitive.</span></span>  
  
-   <span data-ttu-id="cdf1d-174">Operators Volg C# impliciete conversie semantiek indien mogelijk.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-174">Operators follow C# implicit conversion semantics whenever possible.</span></span>  
  
-   <span data-ttu-id="cdf1d-175">Systeem zijn openbare eigenschappen beschikbaar zijn in [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) exemplaren.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-175">System properties are public properties exposed in [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) instances.</span></span>  
  
    <span data-ttu-id="cdf1d-176">Houd rekening met de volgende Hallo `IS [NOT] NULL` semantiek:</span><span class="sxs-lookup"><span data-stu-id="cdf1d-176">Consider hello following `IS [NOT] NULL` semantics:</span></span>  
  
    -   <span data-ttu-id="cdf1d-177">`property IS NULL`wordt geëvalueerd als `true` als beide Hallo-eigenschap niet bestaat of de waarde van eigenschap Hallo `null`.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-177">`property IS NULL` is evaluated as `true` if either hello property doesn't exist or hello property's value is `null`.</span></span>  
  
### <a name="property-evaluation-semantics"></a><span data-ttu-id="cdf1d-178">Eigenschap evaluatie semantiek</span><span class="sxs-lookup"><span data-stu-id="cdf1d-178">Property evaluation semantics</span></span>  
  
-   <span data-ttu-id="cdf1d-179">Een poging tooevaluate een niet-bestaande systeemeigenschap genereert een [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) uitzondering.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-179">An attempt tooevaluate a non-existent system property throws a [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) exception.</span></span>  
  
-   <span data-ttu-id="cdf1d-180">Een eigenschap die niet intern wordt geëvalueerd als **onbekende**.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-180">A property that does not exist is internally evaluated as **unknown**.</span></span>  
  
 <span data-ttu-id="cdf1d-181">Onbekende evaluatie in rekenkundige operatoren:</span><span class="sxs-lookup"><span data-stu-id="cdf1d-181">Unknown evaluation in arithmetic operators:</span></span>  
  
-   <span data-ttu-id="cdf1d-182">Voor binaire operators als een Hallo links en/of rechts van operanden wordt geëvalueerd als **onbekende**, dan is Hallo resultaat **onbekende**.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-182">For binary operators, if either hello left and/or right side of operands is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
-   <span data-ttu-id="cdf1d-183">Voor unaire operators, als een operand wordt geëvalueerd als **onbekende**, dan is Hallo resultaat **onbekende**.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-183">For unary operators, if an operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="cdf1d-184">Onbekende evaluatie in binaire vergelijkingsoperators:</span><span class="sxs-lookup"><span data-stu-id="cdf1d-184">Unknown evaluation in binary comparison operators:</span></span>  
  
-   <span data-ttu-id="cdf1d-185">Als een Hallo links en/of rechts van operanden wordt geëvalueerd als **onbekende**, dan is Hallo resultaat **onbekende**.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-185">If either hello left and/or right side of operands is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="cdf1d-186">Onbekende evaluatie in `[NOT] LIKE`:</span><span class="sxs-lookup"><span data-stu-id="cdf1d-186">Unknown evaluation in `[NOT] LIKE`:</span></span>  
  
-   <span data-ttu-id="cdf1d-187">Als een operand wordt geëvalueerd als **onbekende**, dan is Hallo resultaat **onbekende**.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-187">If any operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="cdf1d-188">Onbekende evaluatie in `[NOT] IN`:</span><span class="sxs-lookup"><span data-stu-id="cdf1d-188">Unknown evaluation in `[NOT] IN`:</span></span>  
  
-   <span data-ttu-id="cdf1d-189">Als de linkeroperand hello wordt geëvalueerd als **onbekende**, dan is Hallo resultaat **onbekende**.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-189">If hello left operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="cdf1d-190">Onbekende evaluatie in **en** operator:</span><span class="sxs-lookup"><span data-stu-id="cdf1d-190">Unknown evaluation in **AND** operator:</span></span>  
  
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
  
 <span data-ttu-id="cdf1d-191">Onbekende evaluatie in **of** operator:</span><span class="sxs-lookup"><span data-stu-id="cdf1d-191">Unknown evaluation in **OR** operator:</span></span>  
  
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
  
### <a name="operator-binding-semantics"></a><span data-ttu-id="cdf1d-192">Operator binding semantiek</span><span class="sxs-lookup"><span data-stu-id="cdf1d-192">Operator binding semantics</span></span>
  
-   <span data-ttu-id="cdf1d-193">Vergelijkingsoperators zoals `>`, `>=`, `<`, `<=`, `!=`, en `=` Volg dezelfde Hallo-semantiek als Hallo C#-operator in gegevens binding Typ aanbiedingen en impliciete conversies.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-193">Comparison operators such as `>`, `>=`, `<`, `<=`, `!=`, and `=` follow hello same semantics as hello C# operator binding in data type promotions and implicit conversions.</span></span>  
  
-   <span data-ttu-id="cdf1d-194">Rekenkundige operatoren zoals `+`, `-`, `*`, `/`, en `%` Volg dezelfde Hallo-semantiek als Hallo C#-operator in gegevens binding Typ aanbiedingen en impliciete conversies.</span><span class="sxs-lookup"><span data-stu-id="cdf1d-194">Arithmetic operators such as `+`, `-`, `*`, `/`, and `%` follow hello same semantics as hello C# operator binding in data type promotions and implicit conversions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdf1d-195">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cdf1d-195">Next steps</span></span>

- [<span data-ttu-id="cdf1d-196">SQLFilter klasse</span><span class="sxs-lookup"><span data-stu-id="cdf1d-196">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [<span data-ttu-id="cdf1d-197">SQLRuleAction klasse</span><span class="sxs-lookup"><span data-stu-id="cdf1d-197">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)