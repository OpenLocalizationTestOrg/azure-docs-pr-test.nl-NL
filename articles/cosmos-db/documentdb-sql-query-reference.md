---
title: 'Azure DB Cosmos DocumentDB API: SQL-syntaxis voor | Microsoft Docs'
description: Documentatie voor de taal van Azure Cosmos DB DocumentDB API SQL-query.
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: reference
ms.date: 06/13/2017
ms.author: mimig
ms.openlocfilehash: 63b2d20c74df4fd6173994ee1a727594ba8afba3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a><span data-ttu-id="288ad-103">Azure DB Cosmos DocumentDB API: Verwijzing naar SQL</span><span class="sxs-lookup"><span data-stu-id="288ad-103">Azure Cosmos DB DocumentDB API: SQL syntax reference</span></span>

<span data-ttu-id="288ad-104">De Azure-API voor DocumentDB Cosmos DB ondersteunt documentquery's die gebruikmaken van een bekende SQL (Structured Query Language) zoals grammatica via hiërarchische JSON-documenten zonder expliciet schema of het maken van secundaire indexen.</span><span class="sxs-lookup"><span data-stu-id="288ad-104">The Azure Cosmos DB DocumentDB API supports querying documents using a familiar SQL (Structured Query Language) like grammar over hierarchical JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> <span data-ttu-id="288ad-105">Dit onderwerp vindt u documentatie voor de DocumentDB API SQL query language reference.</span><span class="sxs-lookup"><span data-stu-id="288ad-105">This topic provides reference documentation for the DocumentDB API SQL query language.</span></span>

<span data-ttu-id="288ad-106">Zie voor een overzicht van de DocumentDB API SQL-querytaal [SQL-query's voor Azure Cosmos DB DocumentDB API](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="288ad-106">For a walkthrough of the DocumentDB API SQL query language, see [SQL queries for Azure Cosmos DB DocumentDB API](documentdb-sql-query.md).</span></span>  
  
<span data-ttu-id="288ad-107">We nodigen ook u gaat u naar de [Query Playground](http://www.documentdb.com/sql/demo) kunt u proberen Azure Cosmos DB en SQL-query's uitvoeren op onze gegevensset.</span><span class="sxs-lookup"><span data-stu-id="288ad-107">We also invite you to visit the [Query Playground](http://www.documentdb.com/sql/demo) where you can try Azure Cosmos DB and run SQL queries against our dataset.</span></span>  
  
## <a name="select-query"></a><span data-ttu-id="288ad-108">SELECT-query</span><span class="sxs-lookup"><span data-stu-id="288ad-108">SELECT query</span></span>  
<span data-ttu-id="288ad-109">JSON-documenten opgehaald uit de database.</span><span class="sxs-lookup"><span data-stu-id="288ad-109">Retrieves JSON documents from the database.</span></span> <span data-ttu-id="288ad-110">Ondersteunt de evaluatie van de expressie, projecties, filteren en lid wordt.</span><span class="sxs-lookup"><span data-stu-id="288ad-110">Supports expression evaluation, projections, filtering and joins.</span></span>  <span data-ttu-id="288ad-111">De conventies voor de beschrijving van de SELECT-instructies zijn in een tabel in de sectie syntaxis overeenkomsten weergegeven.</span><span class="sxs-lookup"><span data-stu-id="288ad-111">The conventions used for describing the SELECT statements are tabulated in the Syntax conventions section.</span></span>  
  
<span data-ttu-id="288ad-112">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-112">**Syntax**</span></span>  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 <span data-ttu-id="288ad-113">**Opmerkingen**</span><span class="sxs-lookup"><span data-stu-id="288ad-113">**Remarks**</span></span>  
  
 <span data-ttu-id="288ad-114">Zie de volgende secties voor meer informatie op elke component:</span><span class="sxs-lookup"><span data-stu-id="288ad-114">See following sections for details on each clause:</span></span>  
  
-   [<span data-ttu-id="288ad-115">SELECT-component</span><span class="sxs-lookup"><span data-stu-id="288ad-115">SELECT clause</span></span>](#bk_select_query)  
  
-   [<span data-ttu-id="288ad-116">FROM-component</span><span class="sxs-lookup"><span data-stu-id="288ad-116">FROM clause</span></span>](#bk_from_clause)  
  
-   [<span data-ttu-id="288ad-117">WHERE-component</span><span class="sxs-lookup"><span data-stu-id="288ad-117">WHERE clause</span></span>](#bk_where_clause)  
  
-   [<span data-ttu-id="288ad-118">ORDER BY-component</span><span class="sxs-lookup"><span data-stu-id="288ad-118">ORDER BY clause</span></span>](#bk_orderby_clause)  
  
<span data-ttu-id="288ad-119">De componenten in de SELECT-instructie moeten worden besteld, zoals hierboven.</span><span class="sxs-lookup"><span data-stu-id="288ad-119">The clauses in the SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="288ad-120">Een van de optionele componenten kan worden weggelaten.</span><span class="sxs-lookup"><span data-stu-id="288ad-120">Any one of the optional clauses can be omitted.</span></span> <span data-ttu-id="288ad-121">Maar als optionele componenten worden gebruikt, moeten ze worden weergegeven in de juiste volgorde.</span><span class="sxs-lookup"><span data-stu-id="288ad-121">But when optional clauses are used, they must appear in the right order.</span></span>  
  
<span data-ttu-id="288ad-122">**Logische verwerkingsvolgorde van de SELECT-instructie**</span><span class="sxs-lookup"><span data-stu-id="288ad-122">**Logical Processing Order of the SELECT statement**</span></span>  
  
<span data-ttu-id="288ad-123">De volgorde waarin componenten worden verwerkt is:</span><span class="sxs-lookup"><span data-stu-id="288ad-123">The order in which clauses are processed is:</span></span>  

1.  [<span data-ttu-id="288ad-124">FROM-component</span><span class="sxs-lookup"><span data-stu-id="288ad-124">FROM clause</span></span>](#bk_from_clause)  
2.  [<span data-ttu-id="288ad-125">WHERE-component</span><span class="sxs-lookup"><span data-stu-id="288ad-125">WHERE clause</span></span>](#bk_where_clause)  
3.  [<span data-ttu-id="288ad-126">ORDER BY-component</span><span class="sxs-lookup"><span data-stu-id="288ad-126">ORDER BY clause</span></span>](#bk_orderby_clause)  
4.  [<span data-ttu-id="288ad-127">SELECT-component</span><span class="sxs-lookup"><span data-stu-id="288ad-127">SELECT clause</span></span>](#bk_select_query)  

<span data-ttu-id="288ad-128">Houd er rekening mee dat dit verschilt van de volgorde waarin ze worden weergegeven in de syntaxis.</span><span class="sxs-lookup"><span data-stu-id="288ad-128">Note that this is different from the order in which they appear in the syntax.</span></span> <span data-ttu-id="288ad-129">De volgorde is dat alle nieuwe symbolen die zijn geïntroduceerd in een component verwerkte zichtbaar zijn en kunnen worden gebruikt in de componenten die later wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="288ad-129">The ordering is such that all new symbols introduced by a processed clause are visible and can be used in clauses processed later.</span></span> <span data-ttu-id="288ad-130">Bijvoorbeeld, aliassen die zijn gedeclareerd in een FROM-component in, waarbij toegankelijk zijn en SELECT-component.</span><span class="sxs-lookup"><span data-stu-id="288ad-130">For instance, aliases declared in a FROM clause are accessible in WHERE and SELECT clauses.</span></span>  

<span data-ttu-id="288ad-131">**Spaties en -opmerkingen**</span><span class="sxs-lookup"><span data-stu-id="288ad-131">**Whitespace characters and comments**</span></span>  

<span data-ttu-id="288ad-132">Alle spatietekens die deel uitmaken van een tekenreeks tussen aanhalingstekens of aanhalingstekens id maken geen deel uit van de taal-grammatica en worden genegeerd tijdens het parseren.</span><span class="sxs-lookup"><span data-stu-id="288ad-132">All white space characters which are not part of a quoted string or quoted identifier are not part of the language grammar and are ignored during parsing.</span></span>  

<span data-ttu-id="288ad-133">De query language ondersteunt T-SQL-stijl opmerkingen zoals</span><span class="sxs-lookup"><span data-stu-id="288ad-133">The query language supports T-SQL style comments like</span></span>  

-   <span data-ttu-id="288ad-134">SQL-instructie`-- comment text [newline]`</span><span class="sxs-lookup"><span data-stu-id="288ad-134">SQL Statement `-- comment text [newline]`</span></span>  

<span data-ttu-id="288ad-135">Terwijl uit witruimte bestaat en -opmerkingen bevatten geen betekenis in de grammatica, moet het worden gebruikt voor het scheiden van tokens.</span><span class="sxs-lookup"><span data-stu-id="288ad-135">While whitespace characters and comments do not have any significance in the grammar, they must be used to separate tokens.</span></span> <span data-ttu-id="288ad-136">Bijvoorbeeld: `-1e5` is één nummer token, even`: – 1 e5` wordt een min token gevolgd door nummer 1 en id e5.</span><span class="sxs-lookup"><span data-stu-id="288ad-136">For instance: `-1e5` is a single number token, while`: – 1 e5` is a minus token followed by number 1 and identifier e5.</span></span>  

##  <span data-ttu-id="288ad-137"><a name="bk_select_query"></a>SELECT-component</span><span class="sxs-lookup"><span data-stu-id="288ad-137"><a name="bk_select_query"></a> SELECT clause</span></span>  
<span data-ttu-id="288ad-138">De componenten in de SELECT-instructie moeten worden besteld, zoals hierboven.</span><span class="sxs-lookup"><span data-stu-id="288ad-138">The clauses in the SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="288ad-139">Een van de optionele componenten kan worden weggelaten.</span><span class="sxs-lookup"><span data-stu-id="288ad-139">Any one of the optional clauses can be omitted.</span></span> <span data-ttu-id="288ad-140">Maar als optionele componenten worden gebruikt, moeten ze worden weergegeven in de juiste volgorde.</span><span class="sxs-lookup"><span data-stu-id="288ad-140">But when optional clauses are used, they must appear in the right order.</span></span>  

<span data-ttu-id="288ad-141">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-141">**Syntax**</span></span>  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 <span data-ttu-id="288ad-142">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-142">**Arguments**</span></span>  
  
 `<select_specification>`  
  
 <span data-ttu-id="288ad-143">Eigenschappen of -waarde worden geselecteerd voor de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-143">Properties or value to be selected for the result set.</span></span>  
  
 `'*'`  
  
<span data-ttu-id="288ad-144">Hiermee geeft u op dat de waarde zonder wijzigingen moet worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="288ad-144">Specifies that the value should be retrieved without making any changes.</span></span> <span data-ttu-id="288ad-145">Specifiek als de verwerkte waarde een object is, worden alle eigenschappen worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="288ad-145">Specifically if the processed value is an object, all properties will be retrieved.</span></span>  
  
 `<object_property_list>`  
  
<span data-ttu-id="288ad-146">Hiermee geeft u de lijst met eigenschappen worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="288ad-146">Specifies the list of properties to be retrieved.</span></span> <span data-ttu-id="288ad-147">Elke geretourneerde waarde is een object met de eigenschappen die zijn opgegeven.</span><span class="sxs-lookup"><span data-stu-id="288ad-147">Each returned value will be an object with the properties specified.</span></span>  
  
`VALUE`  
  
<span data-ttu-id="288ad-148">Geeft aan dat de JSON-waarde moet worden opgehaald in plaats van de volledige JSON-object.</span><span class="sxs-lookup"><span data-stu-id="288ad-148">Specifies that the JSON value should be retrieved instead of the complete JSON object.</span></span> <span data-ttu-id="288ad-149">Dit, in tegenstelling tot `<property_list>` loopt niet de verwachte waarde in een object.</span><span class="sxs-lookup"><span data-stu-id="288ad-149">This, unlike `<property_list>` does not wrap the projected value in an object.</span></span>  
  
`<scalar_expression>`  
  
<span data-ttu-id="288ad-150">De expressie voor de waarde moeten worden berekend.</span><span class="sxs-lookup"><span data-stu-id="288ad-150">Expression representing the value to be computed.</span></span> <span data-ttu-id="288ad-151">Zie [scalaire expressies](#bk_scalar_expressions) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="288ad-151">See [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
<span data-ttu-id="288ad-152">**Opmerkingen**</span><span class="sxs-lookup"><span data-stu-id="288ad-152">**Remarks**</span></span>  
  
<span data-ttu-id="288ad-153">De `SELECT *` syntaxis is alleen geldig als FROM-component precies één alias is gedeclareerd.</span><span class="sxs-lookup"><span data-stu-id="288ad-153">The `SELECT *` syntax is only valid if FROM clause has declared exactly one alias.</span></span> <span data-ttu-id="288ad-154">`SELECT *`biedt een identity-projectie handig is als er geen projectie is vereist.</span><span class="sxs-lookup"><span data-stu-id="288ad-154">`SELECT *` provides an identity projection, which can be useful if no projection is needed.</span></span> <span data-ttu-id="288ad-155">Selecteer * is alleen geldig als FROM-component is opgegeven en er slechts één invoer bron geïntroduceerd.</span><span class="sxs-lookup"><span data-stu-id="288ad-155">SELECT * is only valid if FROM clause is specified and introduced only a single input source.</span></span>  
  
<span data-ttu-id="288ad-156">Houd er rekening mee dat `SELECT <select_list>` en `SELECT *` 'syntactische suiker' zijn en u kunt ook kan worden uitgedrukt met behulp van eenvoudige SELECT-instructies zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="288ad-156">Note that `SELECT <select_list>` and `SELECT *` are "syntactic sugar" and can be alternatively expressed by using simple SELECT statements as shown below.</span></span>  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     <span data-ttu-id="288ad-157">is gelijk aan:</span><span class="sxs-lookup"><span data-stu-id="288ad-157">is equivalent to:</span></span>  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     <span data-ttu-id="288ad-158">is gelijk aan:</span><span class="sxs-lookup"><span data-stu-id="288ad-158">is equivalent to:</span></span>  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
<span data-ttu-id="288ad-159">**Zie ook**</span><span class="sxs-lookup"><span data-stu-id="288ad-159">**See Also**</span></span>  
  
[<span data-ttu-id="288ad-160">Scalaire expressies</span><span class="sxs-lookup"><span data-stu-id="288ad-160">Scalar expressions</span></span>](#bk_scalar_expressions)  
[<span data-ttu-id="288ad-161">SELECT-component</span><span class="sxs-lookup"><span data-stu-id="288ad-161">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="288ad-162"><a name="bk_from_clause"></a>FROM-component</span><span class="sxs-lookup"><span data-stu-id="288ad-162"><a name="bk_from_clause"></a> FROM clause</span></span>  
<span data-ttu-id="288ad-163">Hiermee geeft u de bron- of gekoppelde bronnen.</span><span class="sxs-lookup"><span data-stu-id="288ad-163">Specifies the source or joined sources.</span></span> <span data-ttu-id="288ad-164">De component FROM is optioneel.</span><span class="sxs-lookup"><span data-stu-id="288ad-164">The FROM clause is optional.</span></span> <span data-ttu-id="288ad-165">Als dat niet wordt opgegeven, andere componenten nog steeds uitgevoerd alsof FROM-component opgegeven één document.</span><span class="sxs-lookup"><span data-stu-id="288ad-165">If not specified, other clauses will still be executed as if FROM clause provided a single document.</span></span>  
  
<span data-ttu-id="288ad-166">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-166">**Syntax**</span></span>  
  
```  
FROM <from_specification>  
  
<from_specification> ::=   
        <from_source> {[ JOIN <from_source>][,...n]}  
  
<from_source> ::=   
          <collection_expression> [[AS] input_alias]  
        | input_alias IN <collection_expression>  
  
<collection_expression> ::=   
        ROOT   
     | collection_name  
     | input_alias  
     | <collection_expression> '.' property_name  
     | <collection_expression> '[' "property_name" | array_index ']'  
```  
  
<span data-ttu-id="288ad-167">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-167">**Arguments**</span></span>  
  
`<from_source>`  
  
<span data-ttu-id="288ad-168">Hiermee geeft u een gegevensbron met of zonder een alias.</span><span class="sxs-lookup"><span data-stu-id="288ad-168">Specifies a data source, with or without an alias.</span></span> <span data-ttu-id="288ad-169">Als alias niet opgegeven is, wordt deze afgeleid van de `<collection_expression>` met volgende regels:</span><span class="sxs-lookup"><span data-stu-id="288ad-169">If alias is not specified, it will be inferred from the `<collection_expression>` using following rules:</span></span>  
  
-   <span data-ttu-id="288ad-170">De expressie is een verzamelingnaam, wordt verzamelingnaam worden gebruikt als een alias.</span><span class="sxs-lookup"><span data-stu-id="288ad-170">If the expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
-   <span data-ttu-id="288ad-171">Als de expressie `<collection_expression>`, en vervolgens kubuskenmerkbinding en vervolgens kubuskenmerkbinding wordt gebruikt als alias.</span><span class="sxs-lookup"><span data-stu-id="288ad-171">If the expression is `<collection_expression>`, then property_name, then property_name will be used as an alias.</span></span> <span data-ttu-id="288ad-172">De expressie is een verzamelingnaam, wordt verzamelingnaam worden gebruikt als een alias.</span><span class="sxs-lookup"><span data-stu-id="288ad-172">If the expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
<span data-ttu-id="288ad-173">ALS IN DE`input_alias`</span><span class="sxs-lookup"><span data-stu-id="288ad-173">AS `input_alias`</span></span>  
  
<span data-ttu-id="288ad-174">Hiermee wordt aangegeven dat de `input_alias` is een set met waarden geretourneerd door de onderliggende verzamelingsexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-174">Specifies that the `input_alias` is a set of values returned by the underlying collection expression.</span></span>  
 
<span data-ttu-id="288ad-175">`input_alias`IN</span><span class="sxs-lookup"><span data-stu-id="288ad-175">`input_alias` IN</span></span>  
  
<span data-ttu-id="288ad-176">Hiermee wordt aangegeven dat de `input_alias` moet de set met waarden die zijn verkregen door iteratie van alle matrixelementen van elke matrix geretourneerd door de onderliggende verzamelingsexpressie vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="288ad-176">Specifies that the `input_alias` should represent the set of values obtained by iterating over all array elements of each array returned by the underlying collection expression.</span></span> <span data-ttu-id="288ad-177">Een waarde die is geretourneerd door de onderliggende verzamelingsexpressie is geen matrix wordt genegeerd.</span><span class="sxs-lookup"><span data-stu-id="288ad-177">Any value returned by underlying collection expression that is not an array is ignored.</span></span>  
  
`<collection_expression>`  
  
<span data-ttu-id="288ad-178">Hiermee geeft u de verzamelingsexpressie voor het ophalen van de documenten worden gebruikt in de.</span><span class="sxs-lookup"><span data-stu-id="288ad-178">Specifies the collection expression to be used to retrieve the documents.</span></span>  
  
`ROOT`  
  
<span data-ttu-id="288ad-179">Hiermee geeft u op dat document moet worden opgehaald van de standaardwaarde, momenteel verbonden verzameling.</span><span class="sxs-lookup"><span data-stu-id="288ad-179">Specifies that document should be retrieved from the default, currently connected collection.</span></span>  
  
`collection_name`  
  
<span data-ttu-id="288ad-180">Hiermee geeft u op dat document moet worden opgehaald uit de opgegeven verzameling.</span><span class="sxs-lookup"><span data-stu-id="288ad-180">Specifies that document should be retrieved from the provided collection.</span></span> <span data-ttu-id="288ad-181">De naam van de verzameling moet overeenkomen met de naam van de momenteel verbonden met verzameling.</span><span class="sxs-lookup"><span data-stu-id="288ad-181">The name of the collection must match the name of the collection currently connected to.</span></span>  
  
`input_alias`  
  
<span data-ttu-id="288ad-182">Hiermee geeft u op dat document moet worden opgehaald uit de andere bron gedefinieerd door de opgegeven alias.</span><span class="sxs-lookup"><span data-stu-id="288ad-182">Specifies that document should be retrieved from the other source defined by the provided alias.</span></span>  
  
`<collection_expression> '.' property_`  
  
<span data-ttu-id="288ad-183">Geeft aan dat document moet worden opgehaald door het openen van de `property_name` eigenschap of matrixindex matrixelement voor alle documenten die worden opgehaald door opgegeven verzamelingsexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-183">Specifies that document should be retrieved by accessing the `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
<span data-ttu-id="288ad-184">Geeft aan dat document moet worden opgehaald door het openen van de `property_name` eigenschap of matrixindex matrixelement voor alle documenten die worden opgehaald door opgegeven verzamelingsexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-184">Specifies that document should be retrieved by accessing the `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
<span data-ttu-id="288ad-185">**Opmerkingen**</span><span class="sxs-lookup"><span data-stu-id="288ad-185">**Remarks**</span></span>  
  
<span data-ttu-id="288ad-186">Alle aliassen verstrekt of afgeleid in de `<from_source>(`s) moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="288ad-186">All aliases provided or inferred in the `<from_source>(`s) must be unique.</span></span> <span data-ttu-id="288ad-187">De syntaxis van de `<collection_expression>.`kubuskenmerkbinding is hetzelfde als `<collection_expression>' ['"property_name"']'`.</span><span class="sxs-lookup"><span data-stu-id="288ad-187">The Syntax `<collection_expression>.`property_name is the same as `<collection_expression>' ['"property_name"']'`.</span></span> <span data-ttu-id="288ad-188">De syntaxis van de laatste kan echter worden gebruikt als een eigenschapsnaam een niet-id-tekens bevat.</span><span class="sxs-lookup"><span data-stu-id="288ad-188">However, the latter syntax can be used if a property name contains a non-identifier characters.</span></span>  
  
<span data-ttu-id="288ad-189">**Ontbrekende eigenschappen, ontbrekende matrixelementen, niet-gedefinieerde waarden verwerken**</span><span class="sxs-lookup"><span data-stu-id="288ad-189">**Missing properties, missing array elements, undefined values handling**</span></span>  
  
<span data-ttu-id="288ad-190">Als een verzamelingsexpressie voor een naar eigenschappen of matrixelementen en waarde niet bestaat, wordt die waarde genegeerd en niet verder worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="288ad-190">If a collection expression accesses properties or array elements and that value does not exist, that value will be ignored and not processed further.</span></span>  
  
<span data-ttu-id="288ad-191">**Verzameling expressie context scoping**</span><span class="sxs-lookup"><span data-stu-id="288ad-191">**Collection expression context scoping**</span></span>  
  
<span data-ttu-id="288ad-192">Een verzamelingsexpressie is mogelijk binnen het bereik van verzameling of binnen het bereik van document:</span><span class="sxs-lookup"><span data-stu-id="288ad-192">A collection expression may be collection-scoped or document-scoped:</span></span>  
  
-   <span data-ttu-id="288ad-193">Een expressie is verzameling-bereik, als de onderliggende gegevensbron van de verzamelingsexpressie ofwel ROOT is of `collection_name`.</span><span class="sxs-lookup"><span data-stu-id="288ad-193">An expression is collection-scoped, if the underlying source of the collection expression is either ROOT or `collection_name`.</span></span> <span data-ttu-id="288ad-194">Een dergelijke expressie vertegenwoordigt een verzameling van documenten die zijn opgehaald uit de verzameling rechtstreeks en is niet afhankelijk van de verwerking van andere expressies verzameling.</span><span class="sxs-lookup"><span data-stu-id="288ad-194">Such an expression represents a set of documents retrieved from the collection directly, and is not dependent on the processing of other collection expressions.</span></span>  
  
-   <span data-ttu-id="288ad-195">Een expressie is document-bereik, als de onderliggende gegevensbron van de verzamelingsexpressie `input_alias` geïntroduceerd eerder in de query.</span><span class="sxs-lookup"><span data-stu-id="288ad-195">An expression is document-scoped, if the underlying source of the collection expression is `input_alias` introduced earlier in the query.</span></span> <span data-ttu-id="288ad-196">Een dergelijke expressie vertegenwoordigt een verzameling van documenten die zijn verkregen door het evalueren van de verzamelingsexpressie in het bereik van de van elk document die horen bij de set die zijn gekoppeld aan de verzameling alias hebben.</span><span class="sxs-lookup"><span data-stu-id="288ad-196">Such an expression represents a set of documents obtained by evaluating the collection expression in the scope of each document belonging to the set associated with the aliased collection.</span></span>  <span data-ttu-id="288ad-197">De resulterende set worden een samenvoeging van die worden verkregen door de verzamelingsexpressie voor elk van de documenten in de onderliggende set te evalueren.</span><span class="sxs-lookup"><span data-stu-id="288ad-197">The resulting set will be a union of sets obtained by evaluating the collection expression for each of the documents in the underlying set.</span></span>  
  
<span data-ttu-id="288ad-198">**Joins**</span><span class="sxs-lookup"><span data-stu-id="288ad-198">**Joins**</span></span>  
  
<span data-ttu-id="288ad-199">In de huidige release ondersteunt Azure Cosmos DB inner joins.</span><span class="sxs-lookup"><span data-stu-id="288ad-199">In the current release, Azure Cosmos DB supports inner joins.</span></span> <span data-ttu-id="288ad-200">Er zijn extra join mechanismen toekomstige.</span><span class="sxs-lookup"><span data-stu-id="288ad-200">Additional join capabilities are forthcoming.</span></span>

<span data-ttu-id="288ad-201">Inner join resulteert in een volledige vectorproduct van de sets die deel uitmaken van de join.</span><span class="sxs-lookup"><span data-stu-id="288ad-201">Inner joins result in a complete cross product of the sets participating in the join.</span></span> <span data-ttu-id="288ad-202">Het resultaat van een join N manier is een set met tuples zijn N-element, waarbij elke waarde in de tuple is gekoppeld aan de alias instellen die deel uitmaken van de join en toegankelijk zijn voor het verwijzen naar deze alias in andere componenten.</span><span class="sxs-lookup"><span data-stu-id="288ad-202">The result of an N-way join is a set of N-element tuples, where each value in the tuple is associated with the aliased set participating in the join and can be accessed by referencing that alias in other clauses.</span></span>  
  
<span data-ttu-id="288ad-203">De evaluatie van de join, is afhankelijk van het bereik van de context van de deelnemende sets:</span><span class="sxs-lookup"><span data-stu-id="288ad-203">The evaluation of the join depends on the context scope of the participating sets:</span></span>  
  
-  <span data-ttu-id="288ad-204">Een join tussen verzamelingsset A en gericht op de verzameling ingesteld B, resulteert in een vectorproduct van alle elementen in sets A en B.</span><span class="sxs-lookup"><span data-stu-id="288ad-204">A join between collection-set A and collection-scoped set B, results in a cross product of all elements in sets A and B.</span></span>
  
-   <span data-ttu-id="288ad-205">Een koppeling tussen het paar A en binnen het bereik van document set B, resulteert in een samenvoeging van alle sets die zijn verkregen door het evalueren van binnen het bereik van document set B voor elk document van A. instellen</span><span class="sxs-lookup"><span data-stu-id="288ad-205">A join between set A and document-scoped set B, results in a union of all sets obtained by evaluating document-scoped set B for each document from set A.</span></span>  
  
 <span data-ttu-id="288ad-206">In de huidige release wordt maximaal één expressie gericht op de verzameling ondersteund door de queryprocessor.</span><span class="sxs-lookup"><span data-stu-id="288ad-206">In the current release, a maximum of one collection-scoped expression is supported by the query processor.</span></span>  
  
<span data-ttu-id="288ad-207">**Voorbeelden van joins:**</span><span class="sxs-lookup"><span data-stu-id="288ad-207">**Examples of joins:**</span></span>  
  
<span data-ttu-id="288ad-208">Bekijk de volgende FROM-component:`<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span><span class="sxs-lookup"><span data-stu-id="288ad-208">Let's look at the following FROM clause: `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span></span>  
  
 <span data-ttu-id="288ad-209">Elke bron definiëren, kunnen `input_alias1, input_alias2, …, input_aliasN`.</span><span class="sxs-lookup"><span data-stu-id="288ad-209">Let each source define `input_alias1, input_alias2, …, input_aliasN`.</span></span> <span data-ttu-id="288ad-210">Deze component FROM retourneert een set met N-tuples (tuple met N waarden).</span><span class="sxs-lookup"><span data-stu-id="288ad-210">This FROM clause returns a set of N-tuples (tuple with N values).</span></span> <span data-ttu-id="288ad-211">Elke tuple heeft geproduceerd door alle verzameling aliassen iteratie van hun respectieve sets waarden.</span><span class="sxs-lookup"><span data-stu-id="288ad-211">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span>  
  
<span data-ttu-id="288ad-212">*Voorbeeld 1, met 2 bronnen JOIN:*</span><span class="sxs-lookup"><span data-stu-id="288ad-212">*JOIN example 1, with 2 sources:*</span></span>  
  
- <span data-ttu-id="288ad-213">Laat `<from_source1>` verzameling bereik en de set {A, B, C} vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="288ad-213">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="288ad-214">Laat `<from_source2>` worden document binnen het bereik van verwijzende input_alias1 en vertegenwoordigen sets:</span><span class="sxs-lookup"><span data-stu-id="288ad-214">Let `<from_source2>` be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="288ad-215">{1, 2} voor`input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="288ad-215">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="288ad-216">{3} voor`input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="288ad-216">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="288ad-217">{4, 5} voor`input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="288ad-217">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="288ad-218">De component FROM `<from_source1> JOIN <from_source2>` leidt ertoe dat de volgende tuples:</span><span class="sxs-lookup"><span data-stu-id="288ad-218">The FROM clause `<from_source1> JOIN <from_source2>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="288ad-219">(`input_alias1, input_alias2`):</span><span class="sxs-lookup"><span data-stu-id="288ad-219">(`input_alias1, input_alias2`):</span></span>  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
<span data-ttu-id="288ad-220">*Voorbeeld 2, met 3 bronnen JOIN:*</span><span class="sxs-lookup"><span data-stu-id="288ad-220">*JOIN example 2, with 3 sources:*</span></span>  
  
- <span data-ttu-id="288ad-221">Laat `<from_source1>` verzameling bereik en de set {A, B, C} vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="288ad-221">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="288ad-222">Laat `<from_source2>` worden binnen het bereik van document verwijzen naar `input_alias1` sets omvatten:</span><span class="sxs-lookup"><span data-stu-id="288ad-222">Let `<from_source2>` be document-scoped referencing `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="288ad-223">{1, 2} voor`input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="288ad-223">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="288ad-224">{3} voor`input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="288ad-224">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="288ad-225">{4, 5} voor`input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="288ad-225">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="288ad-226">Laat `<from_source3>` worden binnen het bereik van document verwijzen naar `input_alias2` sets omvatten:</span><span class="sxs-lookup"><span data-stu-id="288ad-226">Let `<from_source3>` be document-scoped referencing `input_alias2` and represent sets:</span></span>  
  
    <span data-ttu-id="288ad-227">{100, 200} voor`input_alias2 = 1,`</span><span class="sxs-lookup"><span data-stu-id="288ad-227">{100, 200} for `input_alias2 = 1,`</span></span>  
  
    <span data-ttu-id="288ad-228">{300} voor`input_alias2 = 3,`</span><span class="sxs-lookup"><span data-stu-id="288ad-228">{300} for `input_alias2 = 3,`</span></span>  
  
- <span data-ttu-id="288ad-229">De component FROM `<from_source1> JOIN <from_source2> JOIN <from_source3>` leidt ertoe dat de volgende tuples:</span><span class="sxs-lookup"><span data-stu-id="288ad-229">The FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="288ad-230">(input_alias1, input_alias2, input_alias3):</span><span class="sxs-lookup"><span data-stu-id="288ad-230">(input_alias1, input_alias2, input_alias3):</span></span>  
  
    <span data-ttu-id="288ad-231">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span><span class="sxs-lookup"><span data-stu-id="288ad-231">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="288ad-232">Gebrek aan tuples voor andere waarden van `input_alias1`, `input_alias2`, waarvoor de `<from_source3>` heeft geen waarden retourneren.</span><span class="sxs-lookup"><span data-stu-id="288ad-232">Lack of tuples for other values of `input_alias1`, `input_alias2`, for which the `<from_source3>` did not return any values.</span></span>  
  
<span data-ttu-id="288ad-233">*Voorbeeld 3, met 3 bronnen JOIN:*</span><span class="sxs-lookup"><span data-stu-id="288ad-233">*JOIN example 3, with 3 sources:*</span></span>  
  
- <span data-ttu-id="288ad-234">Laat < from_source1 > worden gericht op de verzameling en vertegenwoordigen set {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="288ad-234">Let <from_source1> be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="288ad-235">Laat `<from_source1>` verzameling bereik en de set {A, B, C} vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="288ad-235">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="288ad-236">< From_source2 > verwijzende input_alias1 binnen het bereik van document zijn en stelt vertegenwoordigen, kunnen:</span><span class="sxs-lookup"><span data-stu-id="288ad-236">Let <from_source2> be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="288ad-237">{1, 2} voor`input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="288ad-237">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="288ad-238">{3} voor`input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="288ad-238">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="288ad-239">{4, 5} voor`input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="288ad-239">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="288ad-240">Laat `<from_source3>` moet binnen het bereik `input_alias1` sets omvatten:</span><span class="sxs-lookup"><span data-stu-id="288ad-240">Let `<from_source3>` be scoped to `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="288ad-241">{100, 200} voor`input_alias2 = A,`</span><span class="sxs-lookup"><span data-stu-id="288ad-241">{100, 200} for `input_alias2 = A,`</span></span>  
  
    <span data-ttu-id="288ad-242">{300} voor`input_alias2 = C,`</span><span class="sxs-lookup"><span data-stu-id="288ad-242">{300} for `input_alias2 = C,`</span></span>  
  
- <span data-ttu-id="288ad-243">De component FROM `<from_source1> JOIN <from_source2> JOIN <from_source3>` leidt ertoe dat de volgende tuples:</span><span class="sxs-lookup"><span data-stu-id="288ad-243">The FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="288ad-244">(`input_alias1, input_alias2, input_alias3`):</span><span class="sxs-lookup"><span data-stu-id="288ad-244">(`input_alias1, input_alias2, input_alias3`):</span></span>  
  
    <span data-ttu-id="288ad-245">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200), C, 4, 300, (C, 5, 300)</span><span class="sxs-lookup"><span data-stu-id="288ad-245">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="288ad-246">Dit resulteerde in vectorproduct tussen `<from_source2>` en `<from_source3>` omdat beide zijn gericht op hetzelfde `<from_source1>`.</span><span class="sxs-lookup"><span data-stu-id="288ad-246">This resulted in cross product between `<from_source2>` and `<from_source3>` because both are scoped to the same `<from_source1>`.</span></span>  <span data-ttu-id="288ad-247">Dit resulteerde in 4 (2 x 2) tuples met waarde A, 0 tuples met waarde B (1 x 0) en 2 (2 x 1) tuples met waarde C.</span><span class="sxs-lookup"><span data-stu-id="288ad-247">This resulted in 4 (2x2) tuples having value A, 0 tuples having value B (1x0) and 2 (2x1) tuples having value C.</span></span>  
  
<span data-ttu-id="288ad-248">**Zie ook**</span><span class="sxs-lookup"><span data-stu-id="288ad-248">**See also**</span></span>  
  
 [<span data-ttu-id="288ad-249">SELECT-component</span><span class="sxs-lookup"><span data-stu-id="288ad-249">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="288ad-250"><a name="bk_where_clause"></a>WHERE-component</span><span class="sxs-lookup"><span data-stu-id="288ad-250"><a name="bk_where_clause"></a> WHERE clause</span></span>  
 <span data-ttu-id="288ad-251">Hiermee geeft u het zoekcriterium voor de documenten die worden geretourneerd door de query.</span><span class="sxs-lookup"><span data-stu-id="288ad-251">Specifies the search condition for the documents returned by the query.</span></span>  
  
 <span data-ttu-id="288ad-252">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-252">**Syntax**</span></span>  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 <span data-ttu-id="288ad-253">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-253">**Arguments**</span></span>  
  
-   `<filter_condition>`  
  
     <span data-ttu-id="288ad-254">Geeft aan welke voorwaarde moet worden voldaan om de documenten die moeten worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="288ad-254">Specifies the condition to be met for the documents to be returned.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="288ad-255">De expressie voor de waarde moeten worden berekend.</span><span class="sxs-lookup"><span data-stu-id="288ad-255">Expression representing the value to be computed.</span></span> <span data-ttu-id="288ad-256">Zie de [scalaire expressies](#bk_scalar_expressions) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="288ad-256">See the [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
 <span data-ttu-id="288ad-257">**Opmerkingen**</span><span class="sxs-lookup"><span data-stu-id="288ad-257">**Remarks**</span></span>  
  
 <span data-ttu-id="288ad-258">Om het document moet worden geretourneerd van een expressie die is opgegeven als filter moet voorwaarde resulteren in waar.</span><span class="sxs-lookup"><span data-stu-id="288ad-258">In order for the document to be returned an expression specified as filter condition must evaluate to true.</span></span> <span data-ttu-id="288ad-259">Alleen Booleaanse waarde true voldoen aan de voorwaarde, een andere waarde: niet-gedefinieerde, null, false, getal, matrix of Object niet voldoen aan de voorwaarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-259">Only Boolean value true will satisfy the condition, any other value: undefined, null, false, Number, Array or Object will not satisfy the condition.</span></span>  
  
##  <span data-ttu-id="288ad-260"><a name="bk_orderby_clause"></a>ORDER BY-component</span><span class="sxs-lookup"><span data-stu-id="288ad-260"><a name="bk_orderby_clause"></a> ORDER BY clause</span></span>  
 <span data-ttu-id="288ad-261">Hiermee geeft u de sorteervolgorde voor de resultaten die door de query zijn geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="288ad-261">Specifies the sorting order for results returned by the query.</span></span>  
  
 <span data-ttu-id="288ad-262">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-262">**Syntax**</span></span>  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 <span data-ttu-id="288ad-263">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-263">**Arguments**</span></span>  
  
-   `<sort_specification>`  
  
     <span data-ttu-id="288ad-264">Hiermee geeft u een eigenschap of een expressie waarmee moet worden gesorteerd van de queryresultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-264">Specifies a property or expression on which to sort the query result set.</span></span> <span data-ttu-id="288ad-265">Een kolom sorteren kan worden opgegeven als een alias voor een naam of kolom.</span><span class="sxs-lookup"><span data-stu-id="288ad-265">A sort column can be specified as a name or column alias.</span></span>  
  
     <span data-ttu-id="288ad-266">Meerdere sortering-kolommen kunnen worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="288ad-266">Multiple sort columns can be specified.</span></span> <span data-ttu-id="288ad-267">Kolomnamen moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="288ad-267">Column names must be unique.</span></span> <span data-ttu-id="288ad-268">De volgorde van de kolommen sorteren in de component ORDER BY definieert de organisatie van de gesorteerde resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-268">The sequence of the sort columns in the ORDER BY clause defines the organization of the sorted result set.</span></span> <span data-ttu-id="288ad-269">Dat wil zeggen, de resultatenset is gesorteerd op de eerste eigenschap en vervolgens die geordende lijst is gesorteerd op de tweede eigenschap, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="288ad-269">That is, the result set is sorted by the first property and then that ordered list is sorted by the second property, and so on.</span></span>  
  
     <span data-ttu-id="288ad-270">De kolomnamen van de waarnaar wordt verwezen in de component ORDER BY moeten naar een kolom in de selectielijst of naar een kolom die is gedefinieerd in een tabel die is opgegeven in de component FROM zonder eventuele dubbelzinnigheden overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="288ad-270">The column names referenced in the ORDER BY clause must correspond to either a column in the select list or to a column defined in a table specified in the FROM clause without any ambiguities.</span></span>  
  
-   `<sort_expression>`  
  
     <span data-ttu-id="288ad-271">Hiermee geeft u een één eigenschap of een expressie waarmee moet worden gesorteerd van de queryresultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-271">Specifies a single property or expression on which to sort the query result set.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="288ad-272">Zie de [scalaire expressies](#bk_scalar_expressions) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="288ad-272">See the [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
-   `ASC | DESC`  
  
     <span data-ttu-id="288ad-273">Hiermee geeft u op dat de waarden in de opgegeven kolom in oplopende of aflopende volgorde moeten worden gesorteerd.</span><span class="sxs-lookup"><span data-stu-id="288ad-273">Specifies that the values in the specified column should be sorted in ascending or descending order.</span></span> <span data-ttu-id="288ad-274">ASC sorteren van de laagste waarde naar de hoogste waarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-274">ASC sorts from the lowest value to highest value.</span></span> <span data-ttu-id="288ad-275">DESC sorteren van hoogste waarde naar de laagste waarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-275">DESC sorts from highest value to lowest value.</span></span> <span data-ttu-id="288ad-276">ASC is de standaardsorteervolgorde.</span><span class="sxs-lookup"><span data-stu-id="288ad-276">ASC is the default sort order.</span></span> <span data-ttu-id="288ad-277">Null-waarden worden behandeld als de laagst mogelijke waarden.</span><span class="sxs-lookup"><span data-stu-id="288ad-277">Null values are treated as the lowest possible values.</span></span>  
  
 <span data-ttu-id="288ad-278">**Opmerkingen**</span><span class="sxs-lookup"><span data-stu-id="288ad-278">**Remarks**</span></span>  
  
 <span data-ttu-id="288ad-279">Terwijl de querygrammatica meerdere volgorde door eigenschappen ondersteunt, wordt de runtime van Azure DB die Cosmos-query ondersteunt alleen tegen één eigenschap, en alleen eigenschapnamen, dat wil zeggen, niet op berekende eigenschappen sorteren.</span><span class="sxs-lookup"><span data-stu-id="288ad-279">While the query grammar supports multiple order by properties, the Azure Cosmos DB query runtime supports sorting only against a single property, and only against property names, i.e., not against computed properties.</span></span> <span data-ttu-id="288ad-280">Sorteren is ook vereist dat het indexeringsbeleid een bereikindex voor de eigenschap en het opgegeven type met de maximale precisie bevat.</span><span class="sxs-lookup"><span data-stu-id="288ad-280">Sorting also requires that the indexing policy includes a range index for the property and the specified type, with the maximum precision.</span></span> <span data-ttu-id="288ad-281">Raadpleeg de indexering beleid-documentatie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="288ad-281">Refer to the indexing policy documentation for more details.</span></span>  
  
##  <span data-ttu-id="288ad-282"><a name="bk_scalar_expressions"></a>Scalaire expressies</span><span class="sxs-lookup"><span data-stu-id="288ad-282"><a name="bk_scalar_expressions"></a> Scalar expressions</span></span>  
 <span data-ttu-id="288ad-283">Een scalaire expressie die is een combinatie van de symbolen en operators die kunnen worden geëvalueerd om te verkrijgen van een enkele waarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-283">A scalar expression is a combination of symbols and operators that can be evaluated to obtain a single value.</span></span> <span data-ttu-id="288ad-284">Eenvoudige expressies kunnen bestaan constanten, eigenschap verwijzingen, matrix element verwijzingen, alias-verwijzingen of functieaanroepen.</span><span class="sxs-lookup"><span data-stu-id="288ad-284">Simple expressions can be constants, property references, array element references, alias references, or function calls.</span></span> <span data-ttu-id="288ad-285">Eenvoudige expressies kunnen worden gecombineerd tot complexe expressies met operators.</span><span class="sxs-lookup"><span data-stu-id="288ad-285">Simple expressions can be combined into complex expressions using operators.</span></span>  
  
 <span data-ttu-id="288ad-286">Zie voor informatie over welke scalaire expressie die u wellicht waarden, [constanten](#bk_constants) sectie.</span><span class="sxs-lookup"><span data-stu-id="288ad-286">For details on values which scalar expression may have, see [Constants](#bk_constants) section.</span></span>  
  
 <span data-ttu-id="288ad-287">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-287">**Syntax**</span></span>  
  
```  
<scalar_expression> ::=  
       <constant>   
     | input_alias   
     | parameter_name  
     | <scalar_expression>.property_name  
     | <scalar_expression>'['"property_name"|array_index']'  
     | unary_operator <scalar_expression>  
     | <scalar_expression> binary_operator <scalar_expression>    
     | <scalar_expression> ? <scalar_expression> : <scalar_expression>  
     | <scalar_function_expression>  
     | <create_object_expression>   
     | <create_array_expression>  
     | (<scalar_expression>)   
  
<scalar_function_expression> ::=  
        'udf.' Udf_scalar_function([<scalar_expression>][,…n])  
        | builtin_scalar_function([<scalar_expression>][,…n])  
  
<create_object_expression> ::=  
   '{' [{property_name | "property_name"} : <scalar_expression>][,…n] '}'  
  
<create_array_expression> ::=  
   '[' [<scalar_expression>][,…n] ']'  
  
```  
  
 <span data-ttu-id="288ad-288">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-288">**Arguments**</span></span>  
  
-   `<constant>`  
  
     <span data-ttu-id="288ad-289">Vertegenwoordigt een constante waarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-289">Represents a constant value.</span></span> <span data-ttu-id="288ad-290">Zie [constanten](#bk_constants) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="288ad-290">See [Constants](#bk_constants) section for details.</span></span>  
  
-   `input_alias`  
  
     <span data-ttu-id="288ad-291">Hiermee geeft u een waarde die is gedefinieerd door de `input_alias` geïntroduceerd in de `FROM` component.</span><span class="sxs-lookup"><span data-stu-id="288ad-291">Represents a value defined by the `input_alias` introduced in the `FROM` clause.</span></span>  
    <span data-ttu-id="288ad-292">Deze waarde kan niet worden gegarandeerd **niet-gedefinieerde** –**niet-gedefinieerde** waarden in de invoer worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="288ad-292">This value is guaranteed to not be **undefined** –**undefined** values in the input are skipped.</span></span>  
  
-   `<scalar_expression>.property_name`  
  
     <span data-ttu-id="288ad-293">Vertegenwoordigt een waarde van de eigenschap van een object.</span><span class="sxs-lookup"><span data-stu-id="288ad-293">Represents a value of the property of an object.</span></span> <span data-ttu-id="288ad-294">Als de eigenschap niet bestaat of eigenschap van een waarde die niet een object wordt verwezen, wordt de expressie resulteert in **niet-gedefinieerde** waarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-294">If the property does not exist or property is referenced on a value which is not an object, then the expression evaluates to **undefined** value.</span></span>  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     <span data-ttu-id="288ad-295">Hiermee geeft u een waarde van de eigenschap met de naam `property_name` of matrixelement met index `array_index` van een objectmatrix.</span><span class="sxs-lookup"><span data-stu-id="288ad-295">Represents a value of the property with name `property_name` or array element with index `array_index` of an object/array.</span></span> <span data-ttu-id="288ad-296">Als de eigenschap/matrixindex niet bestaat of de eigenschap/matrixindex op een waarde die niet een objectmatrix wordt verwezen, klikt u vervolgens resulteert de expressie in niet-gedefinieerde waarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-296">If the property/array index does not exist or the property/array index is referenced on a value which is not an object/array, then the expression evaluates to undefined value.</span></span>  
  
-   `unary_operator <scalar_expression>`  
  
     <span data-ttu-id="288ad-297">Vertegenwoordigt een operator die wordt toegepast op een enkele waarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-297">Represents an operator that is applied to a single value.</span></span> <span data-ttu-id="288ad-298">Zie [Operators](#bk_operators) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="288ad-298">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     <span data-ttu-id="288ad-299">Vertegenwoordigt een operator die wordt toegepast op twee waarden.</span><span class="sxs-lookup"><span data-stu-id="288ad-299">Represents an operator that is applied to two values.</span></span> <span data-ttu-id="288ad-300">Zie [Operators](#bk_operators) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="288ad-300">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_function_expression>`  
  
     <span data-ttu-id="288ad-301">Vertegenwoordigt een waarde die is gedefinieerd door een resultaat van een functieaanroep.</span><span class="sxs-lookup"><span data-stu-id="288ad-301">Represents a value defined by a result of a function call.</span></span>  
  
-   `udf_scalar_function`  
  
     <span data-ttu-id="288ad-302">Naam van de gebruiker gedefinieerde scalaire functie.</span><span class="sxs-lookup"><span data-stu-id="288ad-302">Name of the user defined scalar function.</span></span>  
  
-   `builtin_scalar_function`  
  
     <span data-ttu-id="288ad-303">De naam van de ingebouwde scalaire functie.</span><span class="sxs-lookup"><span data-stu-id="288ad-303">Name of the built-in scalar function.</span></span>  
  
-   `<create_object_expression>`  
  
     <span data-ttu-id="288ad-304">Hiermee geeft u een waarde die wordt verkregen door het maken van een nieuw object met de opgegeven eigenschappen en hun waarden.</span><span class="sxs-lookup"><span data-stu-id="288ad-304">Represents a value obtained by creating a new object with specified properties and their values.</span></span>  
  
-   `<create_array_expression>`  
  
     <span data-ttu-id="288ad-305">Hiermee geeft u een waarde die wordt verkregen door het maken van een nieuwe matrix met de opgegeven waarden als elementen</span><span class="sxs-lookup"><span data-stu-id="288ad-305">Represents a value obtained by creating a new array with specified values as elements</span></span>  
  
-   `parameter_name`  
  
     <span data-ttu-id="288ad-306">Vertegenwoordigt een waarde van de opgegeven parameternaam.</span><span class="sxs-lookup"><span data-stu-id="288ad-306">Represents a value of the specified parameter name.</span></span> <span data-ttu-id="288ad-307">Parameternamen moeten één @ hebben als het eerste teken.</span><span class="sxs-lookup"><span data-stu-id="288ad-307">Parameter names must have a single @ as the first character.</span></span>  
  
 <span data-ttu-id="288ad-308">**Opmerkingen**</span><span class="sxs-lookup"><span data-stu-id="288ad-308">**Remarks**</span></span>  
  
 <span data-ttu-id="288ad-309">Bij het aanroepen van een ingebouwde of de gebruiker gedefinieerde scalaire functie moeten alle argumenten worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="288ad-309">When calling a built-in or user defined scalar function all arguments must be defined.</span></span> <span data-ttu-id="288ad-310">Als een van de argumenten is gedefinieerd, wordt de functie wordt niet aangeroepen en wordt het resultaat is niet gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="288ad-310">If any of the arguments is undefined, the function will not be called and the result will be undefined.</span></span>  
  
 <span data-ttu-id="288ad-311">Bij het maken van een object, worden alle eigenschappen die niet-gedefinieerde waarde is toegewezen overgeslagen en niet is opgenomen in het gemaakte object.</span><span class="sxs-lookup"><span data-stu-id="288ad-311">When creating an object, any property that is assigned undefined value will be skipped and not included in the created object.</span></span>  
  
 <span data-ttu-id="288ad-312">Wanneer het maken van een matrix, maar een elementwaarde die is toegewezen **niet-gedefinieerde** waarde wordt overgeslagen en niet is opgenomen in het gemaakte object.</span><span class="sxs-lookup"><span data-stu-id="288ad-312">When creating an array, any element value that is assigned **undefined** value will be skipped and not included in the created object.</span></span> <span data-ttu-id="288ad-313">Hierdoor wordt het volgende gedefinieerde element de plaatsvindt zodanig dat de gemaakte matrix wordt niet hebt overgeslagen indexen.</span><span class="sxs-lookup"><span data-stu-id="288ad-313">This will cause the next defined element to take its place in such a way that the created array will not have skipped indexes.</span></span>  
  
##  <span data-ttu-id="288ad-314"><a name="bk_operators"></a>Operators</span><span class="sxs-lookup"><span data-stu-id="288ad-314"><a name="bk_operators"></a> Operators</span></span>  
 <span data-ttu-id="288ad-315">Deze sectie beschrijft de ondersteunde operators.</span><span class="sxs-lookup"><span data-stu-id="288ad-315">This section describes the supported operators.</span></span> <span data-ttu-id="288ad-316">Elke operator kan worden toegewezen aan één categorie.</span><span class="sxs-lookup"><span data-stu-id="288ad-316">Each operator can be assigned to exactly one category.</span></span>  
  
 <span data-ttu-id="288ad-317">Zie **Operator categorieën** tabel hieronder voor meer informatie met betrekking tot de verwerking van **niet-gedefinieerde** waarden, type-vereisten voor de invoerwaarden en verwerking van waarden met niet overeenkomende typen.</span><span class="sxs-lookup"><span data-stu-id="288ad-317">See **Operator categories** table below, for details regarding handling of **undefined** values, type requirements for input values and handling of values with not matching types.</span></span>  
  
 <span data-ttu-id="288ad-318">**Operator categorieën:**</span><span class="sxs-lookup"><span data-stu-id="288ad-318">**Operator categories:**</span></span>  
  
|<span data-ttu-id="288ad-319">**Categorie**</span><span class="sxs-lookup"><span data-stu-id="288ad-319">**Category**</span></span>|<span data-ttu-id="288ad-320">**Details**</span><span class="sxs-lookup"><span data-stu-id="288ad-320">**Details**</span></span>|  
|-|-|  
|<span data-ttu-id="288ad-321">**rekenkundige bewerking**</span><span class="sxs-lookup"><span data-stu-id="288ad-321">**arithmetic**</span></span>|<span data-ttu-id="288ad-322">Operator input(s) (s) worden verwacht.</span><span class="sxs-lookup"><span data-stu-id="288ad-322">Operator expects input(s) to be Number(s).</span></span> <span data-ttu-id="288ad-323">Uitvoer is ook een getal.</span><span class="sxs-lookup"><span data-stu-id="288ad-323">Output is also a Number.</span></span> <span data-ttu-id="288ad-324">Als een van de invoerwaarden **niet-gedefinieerde** of type dan het aantal vervolgens het resultaat is **niet-gedefinieerde**.</span><span class="sxs-lookup"><span data-stu-id="288ad-324">If any of the inputs is **undefined** or type other than Number then the result is **undefined**.</span></span>|  
|<span data-ttu-id="288ad-325">**Bitsgewijze**</span><span class="sxs-lookup"><span data-stu-id="288ad-325">**bitwise**</span></span>|<span data-ttu-id="288ad-326">Operator verwacht input(s) worden 32-bits geheel getal met teken (s).</span><span class="sxs-lookup"><span data-stu-id="288ad-326">Operator expects input(s) to be 32-bit signed integer Number(s).</span></span> <span data-ttu-id="288ad-327">Uitvoer is ook een 32-bits geheel getal.</span><span class="sxs-lookup"><span data-stu-id="288ad-327">Output is also 32-bit signed integer Number.</span></span><br /><br /> <span data-ttu-id="288ad-328">Een niet-integerwaarde worden afgerond.</span><span class="sxs-lookup"><span data-stu-id="288ad-328">Any non-integer value will be rounded.</span></span> <span data-ttu-id="288ad-329">Positieve waarde wordt afgerond, negatieve getallen naar boven afgerond.</span><span class="sxs-lookup"><span data-stu-id="288ad-329">Positive value will be rounded down, negative values rounded up.</span></span><br /><br /> <span data-ttu-id="288ad-330">Een willekeurige waarde die buiten het bereik voor 32-bits geheel getal wordt geconverteerd, door middel van de laatste 32-bits van de twee van bits.</span><span class="sxs-lookup"><span data-stu-id="288ad-330">Any value that is outside of the 32-bit integer range will be converted, by taking last 32-bits of its two's complement notation.</span></span><br /><br /> <span data-ttu-id="288ad-331">Als een van de invoerwaarden **niet-gedefinieerde** of andere dan getal, typ dan is het resultaat **niet-gedefinieerde**.</span><span class="sxs-lookup"><span data-stu-id="288ad-331">If any of the inputs is **undefined** or type other than Number, then the result is **undefined**.</span></span><br /><br /> <span data-ttu-id="288ad-332">**Opmerking:** het bovenstaande gedrag is compatibel met JavaScript bitsgewijze operator gedrag.</span><span class="sxs-lookup"><span data-stu-id="288ad-332">**Note:** The above behavior is compatible with JavaScript bitwise operator behavior.</span></span>|  
|<span data-ttu-id="288ad-333">**logische**</span><span class="sxs-lookup"><span data-stu-id="288ad-333">**logical**</span></span>|<span data-ttu-id="288ad-334">Operator input(s) Boolean(s) worden verwacht.</span><span class="sxs-lookup"><span data-stu-id="288ad-334">Operator expects input(s) to be Boolean(s).</span></span> <span data-ttu-id="288ad-335">Uitvoer is ook een Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-335">Output is also a Boolean.</span></span><br /><span data-ttu-id="288ad-336">Als een van de invoerwaarden **niet-gedefinieerde** of typ dan Boolean, wordt het resultaat **niet-gedefinieerde**.</span><span class="sxs-lookup"><span data-stu-id="288ad-336">If any of the inputs is **undefined** or type other than Boolean, then the result will be **undefined**.</span></span>|  
|<span data-ttu-id="288ad-337">**vergelijking**</span><span class="sxs-lookup"><span data-stu-id="288ad-337">**comparison**</span></span>|<span data-ttu-id="288ad-338">Operator verwacht input(s) hetzelfde type en niet worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="288ad-338">Operator expects input(s) to have the same type and not be undefined.</span></span> <span data-ttu-id="288ad-339">Uitvoer is een Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-339">Output is a Boolean.</span></span><br /><br /> <span data-ttu-id="288ad-340">Als een van de invoerwaarden **niet-gedefinieerde** of de invoerwaarden hebben verschillende typen en vervolgens het resultaat is **niet-gedefinieerde**.</span><span class="sxs-lookup"><span data-stu-id="288ad-340">If any of the inputs is **undefined** or the inputs have different types, then the result is **undefined**.</span></span><br /><br /> <span data-ttu-id="288ad-341">Zie **volgorde van waarden voor vergelijking** tabel voor waarde ordening details.</span><span class="sxs-lookup"><span data-stu-id="288ad-341">See **Ordering of values for comparison** table for value ordering details.</span></span>|  
|<span data-ttu-id="288ad-342">**tekenreeks**</span><span class="sxs-lookup"><span data-stu-id="288ad-342">**string**</span></span>|<span data-ttu-id="288ad-343">Operator input(s) meer worden verwacht.</span><span class="sxs-lookup"><span data-stu-id="288ad-343">Operator expects input(s) to be String(s).</span></span> <span data-ttu-id="288ad-344">Uitvoer is ook een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="288ad-344">Output is also a String.</span></span><br /><span data-ttu-id="288ad-345">Als een van de invoerwaarden **niet-gedefinieerde** of andere dan tekenreeks typen en vervolgens het resultaat is **niet-gedefinieerde**.</span><span class="sxs-lookup"><span data-stu-id="288ad-345">If any of the inputs is **undefined** or type other than String then the result is **undefined**.</span></span>|  
  
 <span data-ttu-id="288ad-346">**Unaire operators:**</span><span class="sxs-lookup"><span data-stu-id="288ad-346">**Unary operators:**</span></span>  
  
|<span data-ttu-id="288ad-347">**Naam**</span><span class="sxs-lookup"><span data-stu-id="288ad-347">**Name**</span></span>|<span data-ttu-id="288ad-348">**Operator**</span><span class="sxs-lookup"><span data-stu-id="288ad-348">**Operator**</span></span>|<span data-ttu-id="288ad-349">**Details**</span><span class="sxs-lookup"><span data-stu-id="288ad-349">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="288ad-350">**rekenkundige bewerking**</span><span class="sxs-lookup"><span data-stu-id="288ad-350">**arithmetic**</span></span>|+<br /><br /> -|<span data-ttu-id="288ad-351">Retourneert de waarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-351">Returns the number value.</span></span><br /><br /> <span data-ttu-id="288ad-352">Bitsgewijze onderhandeling.</span><span class="sxs-lookup"><span data-stu-id="288ad-352">Bitwise negation.</span></span> <span data-ttu-id="288ad-353">De numerieke waarde retourneert genegeerde.</span><span class="sxs-lookup"><span data-stu-id="288ad-353">Returns negated number value.</span></span>|  
|<span data-ttu-id="288ad-354">**Bitsgewijze**</span><span class="sxs-lookup"><span data-stu-id="288ad-354">**bitwise**</span></span>|~|<span data-ttu-id="288ad-355">Toepassingsgroepen de aanvulling.</span><span class="sxs-lookup"><span data-stu-id="288ad-355">Ones' complement.</span></span> <span data-ttu-id="288ad-356">Retourneert een reeks een numerieke waarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-356">Returns a complement of a number value.</span></span>|  
|<span data-ttu-id="288ad-357">**Logische**</span><span class="sxs-lookup"><span data-stu-id="288ad-357">**Logical**</span></span>|<span data-ttu-id="288ad-358">**NIET**</span><span class="sxs-lookup"><span data-stu-id="288ad-358">**NOT**</span></span>|<span data-ttu-id="288ad-359">Negatie.</span><span class="sxs-lookup"><span data-stu-id="288ad-359">Negation.</span></span> <span data-ttu-id="288ad-360">Retourneert genegeerde Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-360">Returns negated Boolean value.</span></span>|  
  
 <span data-ttu-id="288ad-361">**Binaire operators:**</span><span class="sxs-lookup"><span data-stu-id="288ad-361">**Binary operators:**</span></span>  
  
|<span data-ttu-id="288ad-362">**Naam**</span><span class="sxs-lookup"><span data-stu-id="288ad-362">**Name**</span></span>|<span data-ttu-id="288ad-363">**Operator**</span><span class="sxs-lookup"><span data-stu-id="288ad-363">**Operator**</span></span>|<span data-ttu-id="288ad-364">**Details**</span><span class="sxs-lookup"><span data-stu-id="288ad-364">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="288ad-365">**rekenkundige bewerking**</span><span class="sxs-lookup"><span data-stu-id="288ad-365">**arithmetic**</span></span>|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|<span data-ttu-id="288ad-366">Toevoeging.</span><span class="sxs-lookup"><span data-stu-id="288ad-366">Addition.</span></span><br /><br /> <span data-ttu-id="288ad-367">Aftrekken.</span><span class="sxs-lookup"><span data-stu-id="288ad-367">Subtraction.</span></span><br /><br /> <span data-ttu-id="288ad-368">Vermenigvuldigen.</span><span class="sxs-lookup"><span data-stu-id="288ad-368">Multiplication.</span></span><br /><br /> <span data-ttu-id="288ad-369">Deling.</span><span class="sxs-lookup"><span data-stu-id="288ad-369">Division.</span></span><br /><br /> <span data-ttu-id="288ad-370">Modulatie.</span><span class="sxs-lookup"><span data-stu-id="288ad-370">Modulation.</span></span>|  
|<span data-ttu-id="288ad-371">**Bitsgewijze**</span><span class="sxs-lookup"><span data-stu-id="288ad-371">**bitwise**</span></span>|<span data-ttu-id="288ad-372">&#124;</span><span class="sxs-lookup"><span data-stu-id="288ad-372">&#124;</span></span><br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|<span data-ttu-id="288ad-373">Bitsgewijze OR.</span><span class="sxs-lookup"><span data-stu-id="288ad-373">Bitwise OR.</span></span><br /><br /> <span data-ttu-id="288ad-374">Bitsgewijze AND.</span><span class="sxs-lookup"><span data-stu-id="288ad-374">Bitwise AND.</span></span><br /><br /> <span data-ttu-id="288ad-375">Bitsgewijze XOR.</span><span class="sxs-lookup"><span data-stu-id="288ad-375">Bitwise XOR.</span></span><br /><br /> <span data-ttu-id="288ad-376">Verschuiving naar links.</span><span class="sxs-lookup"><span data-stu-id="288ad-376">Left Shift.</span></span><br /><br /> <span data-ttu-id="288ad-377">Rechts verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="288ad-377">Right Shift.</span></span><br /><br /> <span data-ttu-id="288ad-378">Nul opvulling rechts verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="288ad-378">Zero-fill Right Shift.</span></span>|  
|<span data-ttu-id="288ad-379">**logische**</span><span class="sxs-lookup"><span data-stu-id="288ad-379">**logical**</span></span>|<span data-ttu-id="288ad-380">**EN**</span><span class="sxs-lookup"><span data-stu-id="288ad-380">**AND**</span></span><br /><br /> <span data-ttu-id="288ad-381">**OR**</span><span class="sxs-lookup"><span data-stu-id="288ad-381">**OR**</span></span>|<span data-ttu-id="288ad-382">Logische verbinding.</span><span class="sxs-lookup"><span data-stu-id="288ad-382">Logical conjunction.</span></span> <span data-ttu-id="288ad-383">Retourneert **true** als beide argumenten zijn **true**, retourneert **false** anders.</span><span class="sxs-lookup"><span data-stu-id="288ad-383">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="288ad-384">Logische verbinding.</span><span class="sxs-lookup"><span data-stu-id="288ad-384">Logical conjunction.</span></span> <span data-ttu-id="288ad-385">Retourneert **true** als beide argumenten zijn **true**, retourneert **false** anders.</span><span class="sxs-lookup"><span data-stu-id="288ad-385">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span>|  
|<span data-ttu-id="288ad-386">**vergelijking**</span><span class="sxs-lookup"><span data-stu-id="288ad-386">**comparison**</span></span>|**=**<br /><br /> <span data-ttu-id="288ad-387">**!=, <>**</span><span class="sxs-lookup"><span data-stu-id="288ad-387">**!=, <>**</span></span><br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> <span data-ttu-id="288ad-388">**??**</span><span class="sxs-lookup"><span data-stu-id="288ad-388">**??**</span></span>|<span data-ttu-id="288ad-389">Is gelijk aan.</span><span class="sxs-lookup"><span data-stu-id="288ad-389">Equals.</span></span> <span data-ttu-id="288ad-390">Retourneert **true** als argumenten gelijk zijn, retourneert **false** anders.</span><span class="sxs-lookup"><span data-stu-id="288ad-390">Returns **true** if arguments are equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="288ad-391">Niet gelijk aan.</span><span class="sxs-lookup"><span data-stu-id="288ad-391">Not equal to.</span></span> <span data-ttu-id="288ad-392">Retourneert **true** als argumenten niet gelijk zijn, retourneert **false** anders.</span><span class="sxs-lookup"><span data-stu-id="288ad-392">Returns **true** if arguments are not equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="288ad-393">Groter dan.</span><span class="sxs-lookup"><span data-stu-id="288ad-393">Greater Than.</span></span> <span data-ttu-id="288ad-394">Retourneert **true** als eerste argument groter dan het tweede is, retourneren **false** anders.</span><span class="sxs-lookup"><span data-stu-id="288ad-394">Returns **true** if first argument is greater than the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="288ad-395">Groter dan of gelijk zijn aan.</span><span class="sxs-lookup"><span data-stu-id="288ad-395">Greater Than or Equal To.</span></span> <span data-ttu-id="288ad-396">Retourneert **true** als eerste argument groter dan of gelijk aan het tweede is, geretourneerd **false** anders.</span><span class="sxs-lookup"><span data-stu-id="288ad-396">Returns **true** if first argument is greater than or equal to the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="288ad-397">Minder dan.</span><span class="sxs-lookup"><span data-stu-id="288ad-397">Less Than.</span></span> <span data-ttu-id="288ad-398">Retourneert **true** als eerste argument kleiner is dan de tweede één terugkeer **false** anders.</span><span class="sxs-lookup"><span data-stu-id="288ad-398">Returns **true** if first argument is less than the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="288ad-399">Kleiner dan of gelijk zijn aan.</span><span class="sxs-lookup"><span data-stu-id="288ad-399">Less Than or Equal To.</span></span> <span data-ttu-id="288ad-400">Retourneert **true** als eerste argument kleiner dan of gelijk zijn aan de tweede waarde is retourneren **false** anders.</span><span class="sxs-lookup"><span data-stu-id="288ad-400">Returns **true** if first argument is less than or equal to the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="288ad-401">Coalesce.</span><span class="sxs-lookup"><span data-stu-id="288ad-401">Coalesce.</span></span> <span data-ttu-id="288ad-402">Het tweede argument retourneert als het eerste argument is een **niet-gedefinieerde** waarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-402">Returns the second argument if the first argument is an **undefined** value.</span></span>|  
|<span data-ttu-id="288ad-403">**Tekenreeks**</span><span class="sxs-lookup"><span data-stu-id="288ad-403">**String**</span></span>|<span data-ttu-id="288ad-404">**&#124;&#124;**</span><span class="sxs-lookup"><span data-stu-id="288ad-404">**&#124;&#124;**</span></span>|<span data-ttu-id="288ad-405">Samenvoeging.</span><span class="sxs-lookup"><span data-stu-id="288ad-405">Concatenation.</span></span> <span data-ttu-id="288ad-406">Retourneert een samenvoeging van beide argumenten.</span><span class="sxs-lookup"><span data-stu-id="288ad-406">Returns a concatenation of both arguments.</span></span>|  
  
 <span data-ttu-id="288ad-407">**Ternair operators:**</span><span class="sxs-lookup"><span data-stu-id="288ad-407">**Ternary operators:**</span></span>  
  
|<span data-ttu-id="288ad-408">Ternaire operator</span><span class="sxs-lookup"><span data-stu-id="288ad-408">Ternary operator</span></span>|<span data-ttu-id="288ad-409">?</span><span class="sxs-lookup"><span data-stu-id="288ad-409">?</span></span>|<span data-ttu-id="288ad-410">Het tweede argument retourneert als het eerste argument wordt geëvalueerd naar **true**; anders het derde argument retourneren.</span><span class="sxs-lookup"><span data-stu-id="288ad-410">Returns the second argument if the first argument evaluates to **true**; return the third argument otherwise.</span></span>|  
|-|-|-|  
  
 <span data-ttu-id="288ad-411">**Ordening van waarden voor vergelijking**</span><span class="sxs-lookup"><span data-stu-id="288ad-411">**Ordering of values for comparison**</span></span>  
  
|<span data-ttu-id="288ad-412">**Type**</span><span class="sxs-lookup"><span data-stu-id="288ad-412">**Type**</span></span>|<span data-ttu-id="288ad-413">**De volgorde van de waarden**</span><span class="sxs-lookup"><span data-stu-id="288ad-413">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="288ad-414">**Niet-gedefinieerd**</span><span class="sxs-lookup"><span data-stu-id="288ad-414">**Undefined**</span></span>|<span data-ttu-id="288ad-415">Niet worden vergeleken.</span><span class="sxs-lookup"><span data-stu-id="288ad-415">Not comparable.</span></span>|  
|<span data-ttu-id="288ad-416">**Null**</span><span class="sxs-lookup"><span data-stu-id="288ad-416">**Null**</span></span>|<span data-ttu-id="288ad-417">Eén waarde: **null**</span><span class="sxs-lookup"><span data-stu-id="288ad-417">Single value: **null**</span></span>|  
|<span data-ttu-id="288ad-418">**Aantal**</span><span class="sxs-lookup"><span data-stu-id="288ad-418">**Number**</span></span>|<span data-ttu-id="288ad-419">Natuurlijke reëel getal.</span><span class="sxs-lookup"><span data-stu-id="288ad-419">Natural real number.</span></span><br /><br /> <span data-ttu-id="288ad-420">Negatieve oneindige waarde is kleiner dan andere numerieke waarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-420">Negative Infinity value is smaller than any other Number value.</span></span><br /><br /> <span data-ttu-id="288ad-421">Positieve oneindige waarde is groter dan andere numerieke waarde. **NaN** waarde kan niet worden vergeleken.</span><span class="sxs-lookup"><span data-stu-id="288ad-421">Positive Infinity value is larger than any other Number value.**NaN** value is not comparable.</span></span> <span data-ttu-id="288ad-422">Vergelijken met **NaN** leidt ertoe dat **niet-gedefinieerde** waarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-422">Comparing with **NaN** will result in **undefined** value.</span></span>|  
|<span data-ttu-id="288ad-423">**Tekenreeks**</span><span class="sxs-lookup"><span data-stu-id="288ad-423">**String**</span></span>|<span data-ttu-id="288ad-424">Lexicographical volgorde.</span><span class="sxs-lookup"><span data-stu-id="288ad-424">Lexicographical order.</span></span>|  
|<span data-ttu-id="288ad-425">**Matrix**</span><span class="sxs-lookup"><span data-stu-id="288ad-425">**Array**</span></span>|<span data-ttu-id="288ad-426">Er is geen ordening, maar billijke.</span><span class="sxs-lookup"><span data-stu-id="288ad-426">No ordering, but equitable.</span></span>|  
|<span data-ttu-id="288ad-427">**Object**</span><span class="sxs-lookup"><span data-stu-id="288ad-427">**Object**</span></span>|<span data-ttu-id="288ad-428">Er is geen ordening, maar billijke.</span><span class="sxs-lookup"><span data-stu-id="288ad-428">No ordering, but equitable.</span></span>|  
  
 <span data-ttu-id="288ad-429">**Opmerkingen**</span><span class="sxs-lookup"><span data-stu-id="288ad-429">**Remarks**</span></span>  
  
 <span data-ttu-id="288ad-430">In Azure Cosmos DB, worden de typen waarden vaak niet bekend totdat ze daadwerkelijk worden opgehaald uit de database.</span><span class="sxs-lookup"><span data-stu-id="288ad-430">In Azure Cosmos DB, the types of values are often not known until they are actually retrieved from the database.</span></span> <span data-ttu-id="288ad-431">Om efficiënt uitvoeren van query's te ondersteunen, hebben de meeste van de operators strikt type vereisten.</span><span class="sxs-lookup"><span data-stu-id="288ad-431">In order to support efficient execution of queries, most of the operators have strict type requirements.</span></span> <span data-ttu-id="288ad-432">Operators zelf voeren ook geen impliciete conversies.</span><span class="sxs-lookup"><span data-stu-id="288ad-432">Also operators by themselves do not perform implicit conversions.</span></span>  
  
 <span data-ttu-id="288ad-433">Dit betekent dat een query, zoals: Selecteer * van ROOT r waar r.Age = 21 retourneert alleen documenten met eigenschap leeftijd gelijk zijn aan het getal 21.</span><span class="sxs-lookup"><span data-stu-id="288ad-433">This means that a query like: SELECT * FROM ROOT r WHERE r.Age = 21 will only return documents with property Age equal to the number 21.</span></span> <span data-ttu-id="288ad-434">Documenten met leeftijd gelijk is aan de tekenreeks '21' of de tekenreeks '0021'-eigenschap wordt niet overeenkomen, als de expressie '21' = 21 naar niet-gedefinieerde evalueert.</span><span class="sxs-lookup"><span data-stu-id="288ad-434">Documents with property Age equal to the string "21" or the string "0021" will not match, as the expression "21" = 21 evaluates to undefined.</span></span> <span data-ttu-id="288ad-435">Hiermee kunt u een beter gebruik van indexen, omdat het opzoeken van een specifieke waarde (dat wil zeggen 21 number) is sneller dan zoeken naar oneindig aantal mogelijke overeenkomsten (dat wil zeggen getal 21 of tekenreeksen '21', '021', "21.0"...).</span><span class="sxs-lookup"><span data-stu-id="288ad-435">This allows for a better use of indexes, because the lookup of a specific value (i.e. number 21) is faster than search for indefinite number of potential matches (i.e. number 21 or strings "21", "021", "21.0" …).</span></span> <span data-ttu-id="288ad-436">Dit wijkt af van hoe JavaScript operators van waarden van verschillende typen evalueert.</span><span class="sxs-lookup"><span data-stu-id="288ad-436">This is different from how JavaScript evaluates operators on values of different types.</span></span>  
  
 <span data-ttu-id="288ad-437">**Matrices en objecten gelijkheid en het vergelijkingstype**</span><span class="sxs-lookup"><span data-stu-id="288ad-437">**Arrays and objects equality and comparison**</span></span>  
  
 <span data-ttu-id="288ad-438">Vergelijken van de matrix of Object waarden met bereik operators (>, > =, <, < =) leidt ertoe dat niet-gedefinieerde omdat er geen volgorde gedefinieerd op het Object of de matrix waarden.</span><span class="sxs-lookup"><span data-stu-id="288ad-438">Comparing of Array or Object values using range operators (>, >=, <, <=) will result in undefined as there is not order defined on Object or Array values.</span></span> <span data-ttu-id="288ad-439">Echter met gelijk-ongelijk operators (=,! =, <>) wordt ondersteund en waarden structureel's worden vergeleken.</span><span class="sxs-lookup"><span data-stu-id="288ad-439">However using equality/inequality operators (=, !=, <>) is supported and values will be compared structurally.</span></span>  
  
 <span data-ttu-id="288ad-440">Matrices zijn gelijk als beide matrices hetzelfde aantal elementen hebben en elementen op die overeenkomt met de posities ook gelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="288ad-440">Arrays are equal if both arrays have same number of elements and elements at matching positions are also equal.</span></span> <span data-ttu-id="288ad-441">Het resultaat van de vergelijking van de matrix is niet gedefinieerd als niet alle elementen resulteert in een paar vergelijken gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="288ad-441">If comparing any pair of elements results in undefined, the result of array comparison is undefined.</span></span>  
  
 <span data-ttu-id="288ad-442">Objecten zijn gelijk als beide objecten hebben dezelfde eigenschappen die zijn gedefinieerd, en als de waarden van eigenschappen die overeenkomt met ook gelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="288ad-442">Objects are equal if both objects have same properties defined, and if values of matching properties are also equal.</span></span> <span data-ttu-id="288ad-443">Als het vergelijken van elk paar eigenschap waarden resulteert in een niet-gedefinieerd, is het resultaat van de vergelijking object is niet gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="288ad-443">If comparing any pair of property values results in undefined, the result of object comparison is undefined.</span></span>  
  
##  <span data-ttu-id="288ad-444"><a name="bk_constants"></a>Constanten</span><span class="sxs-lookup"><span data-stu-id="288ad-444"><a name="bk_constants"></a> Constants</span></span>  
 <span data-ttu-id="288ad-445">Een constante, ook wel bekend als een letterlijke waarde of een scalaire waarde is een symbool dat de waarde van een specifieke gegevens vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="288ad-445">A constant, also known as a literal or a scalar value, is a symbol that represents a specific data value.</span></span> <span data-ttu-id="288ad-446">De indeling van een constante is afhankelijk van het gegevenstype van de waarde vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="288ad-446">The format of a constant depends on the data type of the value it represents.</span></span>  
  
 <span data-ttu-id="288ad-447">**Scalaire-gegevenstypen ondersteund:**</span><span class="sxs-lookup"><span data-stu-id="288ad-447">**Supported scalar data types:**</span></span>  
  
|<span data-ttu-id="288ad-448">**Type**</span><span class="sxs-lookup"><span data-stu-id="288ad-448">**Type**</span></span>|<span data-ttu-id="288ad-449">**De volgorde van de waarden**</span><span class="sxs-lookup"><span data-stu-id="288ad-449">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="288ad-450">**Niet-gedefinieerd**</span><span class="sxs-lookup"><span data-stu-id="288ad-450">**Undefined**</span></span>|<span data-ttu-id="288ad-451">Eén waarde: **niet gedefinieerd**</span><span class="sxs-lookup"><span data-stu-id="288ad-451">Single value: **undefined**</span></span>|  
|<span data-ttu-id="288ad-452">**Null**</span><span class="sxs-lookup"><span data-stu-id="288ad-452">**Null**</span></span>|<span data-ttu-id="288ad-453">Eén waarde: **null**</span><span class="sxs-lookup"><span data-stu-id="288ad-453">Single value: **null**</span></span>|  
|<span data-ttu-id="288ad-454">**Booleaanse waarde**</span><span class="sxs-lookup"><span data-stu-id="288ad-454">**Boolean**</span></span>|<span data-ttu-id="288ad-455">Waarden: **false**, **true**.</span><span class="sxs-lookup"><span data-stu-id="288ad-455">Values: **false**, **true**.</span></span>|  
|<span data-ttu-id="288ad-456">**Aantal**</span><span class="sxs-lookup"><span data-stu-id="288ad-456">**Number**</span></span>|<span data-ttu-id="288ad-457">Een getal met dubbele precisie drijvende komma IEEE-norm 754.</span><span class="sxs-lookup"><span data-stu-id="288ad-457">A double-precision floating-point number, IEEE 754 standard.</span></span>|  
|<span data-ttu-id="288ad-458">**Tekenreeks**</span><span class="sxs-lookup"><span data-stu-id="288ad-458">**String**</span></span>|<span data-ttu-id="288ad-459">Een reeks van nul of meer Unicode-tekens.</span><span class="sxs-lookup"><span data-stu-id="288ad-459">A sequence of zero or more Unicode characters.</span></span> <span data-ttu-id="288ad-460">Tekenreeksen moeten worden ingesloten in enkele of dubbele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="288ad-460">Strings must be enclosed in single or double quotes.</span></span>|  
|<span data-ttu-id="288ad-461">**Matrix**</span><span class="sxs-lookup"><span data-stu-id="288ad-461">**Array**</span></span>|<span data-ttu-id="288ad-462">Een reeks van nul of meer elementen.</span><span class="sxs-lookup"><span data-stu-id="288ad-462">A sequence of zero or more elements.</span></span> <span data-ttu-id="288ad-463">Elk element is een waarde van elk gegevenstype scalaire, behalve Undefined.</span><span class="sxs-lookup"><span data-stu-id="288ad-463">Each element can be a value of any scalar data type, except Undefined.</span></span>|  
|<span data-ttu-id="288ad-464">**Object**</span><span class="sxs-lookup"><span data-stu-id="288ad-464">**Object**</span></span>|<span data-ttu-id="288ad-465">Een niet-geordende reeks nul of meer naam/waarde-paren.</span><span class="sxs-lookup"><span data-stu-id="288ad-465">An unordered set of zero or more name/value pairs.</span></span> <span data-ttu-id="288ad-466">De naam van een Unicode-tekenreeks is, de waarde kan zijn van elk gegevenstype scalaire, behalve **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="288ad-466">Name is a Unicode string, value can be of any scalar data type, except **Undefined**.</span></span>|  
  
 <span data-ttu-id="288ad-467">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-467">**Syntax**</span></span>  
  
```  
<constant> ::=  
   <undefined_constant>  
     | <null_constant>   
     | <boolean_constant>   
     | <number_constant>   
     | <string_constant>   
     | <array_constant>   
     | <object_constant>   
  
<undefined_constant> ::= undefined  
  
<null_constant> ::= null  
  
<boolean_constant> ::= false | true  
  
<number_constant> ::= decimal_literal | hexadecimal_literal  
  
<string_constant> ::= string_literal  
  
<array_constant> ::=  
    '[' [<constant>][,...n] ']'  
  
<object_constant> ::=   
   '{' [{property_name | "property_name"} : <constant>][,...n] '}'  
  
```  
  
 <span data-ttu-id="288ad-468">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-468">**Arguments**</span></span>  
  
1.  `<undefined_constant>; undefined`  
  
     <span data-ttu-id="288ad-469">Geeft niet-gedefinieerde waarde van het type niet gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="288ad-469">Represents undefined value of type Undefined.</span></span>  
  
2.  `<null_constant>; null`  
  
     <span data-ttu-id="288ad-470">Hiermee geeft u **null** waarde van het type **Null**.</span><span class="sxs-lookup"><span data-stu-id="288ad-470">Represents **null** value of type **Null**.</span></span>  
  
3.  `<boolean_constant>`  
  
     <span data-ttu-id="288ad-471">Constante van het type Booleaans vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="288ad-471">Represents constant of type Boolean.</span></span>  
  
4.  `false`  
  
     <span data-ttu-id="288ad-472">Hiermee geeft u **false** waarde van het type Boole-waarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-472">Represents **false** value of type Boolean.</span></span>  
  
5.  `true`  
  
     <span data-ttu-id="288ad-473">Hiermee geeft u **true** waarde van het type Boole-waarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-473">Represents **true** value of type Boolean.</span></span>  
  
6.  `<number_constant>`  
  
     <span data-ttu-id="288ad-474">Hiermee geeft u een constante.</span><span class="sxs-lookup"><span data-stu-id="288ad-474">Represents a constant.</span></span>  
  
7.  `decimal_literal`  
  
     <span data-ttu-id="288ad-475">Decimale letterlijke waarden zijn getallen weergegeven met behulp van de decimale notatie of wetenschappelijke notatie.</span><span class="sxs-lookup"><span data-stu-id="288ad-475">Decimal literals are numbers represented using either decimal notation, or scientific notation.</span></span>  
  
8.  `hexadecimal_literal`  
  
     <span data-ttu-id="288ad-476">Hexadecimale letterlijke waarden zijn getallen weergegeven met behulp van het voorvoegsel '0 x' gevolgd door een of meer hexadecimale cijfers.</span><span class="sxs-lookup"><span data-stu-id="288ad-476">Hexadecimal literals are numbers represented using prefix '0x' followed by one or more hexadecimal digits.</span></span>  
  
9. `<string_constant>`  
  
     <span data-ttu-id="288ad-477">Hiermee geeft u een constante van het type String.</span><span class="sxs-lookup"><span data-stu-id="288ad-477">Represents a constant of type String.</span></span>  
  
10. `string _literal`  
  
     <span data-ttu-id="288ad-478">Letterlijke tekenreeks zijn vertegenwoordigd door een reeks van nul of meer Unicode-tekens of escapereeksen Unicode-tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="288ad-478">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="288ad-479">Letterlijke tekenreeks zijn ingesloten in enkele aanhalingstekens (apostrof: ') of dubbele aanhalingstekens (aanhalingsteken: ').</span><span class="sxs-lookup"><span data-stu-id="288ad-479">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span>  
  
 <span data-ttu-id="288ad-480">Volgende escapereeksen worden toegestaan:</span><span class="sxs-lookup"><span data-stu-id="288ad-480">Following escape sequences are allowed:</span></span>  
  
|<span data-ttu-id="288ad-481">**Escape-reeks**</span><span class="sxs-lookup"><span data-stu-id="288ad-481">**Escape sequence**</span></span>|<span data-ttu-id="288ad-482">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="288ad-482">**Description**</span></span>|<span data-ttu-id="288ad-483">**Unicode-teken**</span><span class="sxs-lookup"><span data-stu-id="288ad-483">**Unicode character**</span></span>|  
|-|-|-|  
|<span data-ttu-id="288ad-484">\\'</span><span class="sxs-lookup"><span data-stu-id="288ad-484">\\'</span></span>|<span data-ttu-id="288ad-485">enkel aanhalingsteken (')</span><span class="sxs-lookup"><span data-stu-id="288ad-485">apostrophe (')</span></span>|<span data-ttu-id="288ad-486">U + 0027</span><span class="sxs-lookup"><span data-stu-id="288ad-486">U+0027</span></span>|  
|<span data-ttu-id="288ad-487">\\"</span><span class="sxs-lookup"><span data-stu-id="288ad-487">\\"</span></span>|<span data-ttu-id="288ad-488">aanhalingsteken (")</span><span class="sxs-lookup"><span data-stu-id="288ad-488">quotation mark (")</span></span>|<span data-ttu-id="288ad-489">U + 0022</span><span class="sxs-lookup"><span data-stu-id="288ad-489">U+0022</span></span>|  
|\\\|<span data-ttu-id="288ad-490">omgekeerde schuine streep (\\)</span><span class="sxs-lookup"><span data-stu-id="288ad-490">reverse solidus (\\)</span></span>|<span data-ttu-id="288ad-491">U + 005C</span><span class="sxs-lookup"><span data-stu-id="288ad-491">U+005C</span></span>|  
|\\/|<span data-ttu-id="288ad-492">schuine streep (/)</span><span class="sxs-lookup"><span data-stu-id="288ad-492">solidus (/)</span></span>|<span data-ttu-id="288ad-493">U + 002F</span><span class="sxs-lookup"><span data-stu-id="288ad-493">U+002F</span></span>|  
|<span data-ttu-id="288ad-494">\ber</span><span class="sxs-lookup"><span data-stu-id="288ad-494">\b</span></span>|<span data-ttu-id="288ad-495">BACKSPACE</span><span class="sxs-lookup"><span data-stu-id="288ad-495">backspace</span></span>|<span data-ttu-id="288ad-496">U + 0008</span><span class="sxs-lookup"><span data-stu-id="288ad-496">U+0008</span></span>|  
|<span data-ttu-id="288ad-497">\f</span><span class="sxs-lookup"><span data-stu-id="288ad-497">\f</span></span>|<span data-ttu-id="288ad-498">formulier feed</span><span class="sxs-lookup"><span data-stu-id="288ad-498">form feed</span></span>|<span data-ttu-id="288ad-499">U + 000C</span><span class="sxs-lookup"><span data-stu-id="288ad-499">U+000C</span></span>|  
|\n|<span data-ttu-id="288ad-500">nieuwe regel</span><span class="sxs-lookup"><span data-stu-id="288ad-500">line feed</span></span>|<span data-ttu-id="288ad-501">U + 000A</span><span class="sxs-lookup"><span data-stu-id="288ad-501">U+000A</span></span>|  
|<span data-ttu-id="288ad-502">\r</span><span class="sxs-lookup"><span data-stu-id="288ad-502">\r</span></span>|<span data-ttu-id="288ad-503">regelterugloop</span><span class="sxs-lookup"><span data-stu-id="288ad-503">carriage return</span></span>|<span data-ttu-id="288ad-504">U + 000D</span><span class="sxs-lookup"><span data-stu-id="288ad-504">U+000D</span></span>|  
|<span data-ttu-id="288ad-505">\t</span><span class="sxs-lookup"><span data-stu-id="288ad-505">\t</span></span>|<span data-ttu-id="288ad-506">tabblad</span><span class="sxs-lookup"><span data-stu-id="288ad-506">tab</span></span>|<span data-ttu-id="288ad-507">U + 0009</span><span class="sxs-lookup"><span data-stu-id="288ad-507">U+0009</span></span>|  
|<span data-ttu-id="288ad-508">\uXXXX</span><span class="sxs-lookup"><span data-stu-id="288ad-508">\uXXXX</span></span>|<span data-ttu-id="288ad-509">Een Unicode-teken is gedefinieerd door 4 hexadecimale cijfers.</span><span class="sxs-lookup"><span data-stu-id="288ad-509">A Unicode character defined by 4 hexadecimal digits.</span></span>|<span data-ttu-id="288ad-510">U + XXXX</span><span class="sxs-lookup"><span data-stu-id="288ad-510">U+XXXX</span></span>|  
  
##  <span data-ttu-id="288ad-511"><a name="bk_query_perf_guidelines"></a>Richtlijnen voor query-prestaties</span><span class="sxs-lookup"><span data-stu-id="288ad-511"><a name="bk_query_perf_guidelines"></a> Query performance guidelines</span></span>  
 <span data-ttu-id="288ad-512">Om een query voor het efficiënt voor een grote verzameling worden uitgevoerd, moet deze filters die kunnen worden geleverd via een of meer indexen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="288ad-512">In order for a query to be executed efficiently for a large collection, it should use filters which can be served through one or more indexes.</span></span>  
  
 <span data-ttu-id="288ad-513">De volgende filters wordt voor het opzoeken van de index beschouwd:</span><span class="sxs-lookup"><span data-stu-id="288ad-513">The following filters will be considered for index lookup:</span></span>  
  
-   <span data-ttu-id="288ad-514">Gebruik gelijkheidsoperator (=) met een padexpressie document en een constante.</span><span class="sxs-lookup"><span data-stu-id="288ad-514">Use equality operator ( = ) with a document path expression and a constant.</span></span>  
  
-   <span data-ttu-id="288ad-515">Bereikoperatoren gebruiken (<, \<=, >, > =) met een padexpressie document en aantal constanten.</span><span class="sxs-lookup"><span data-stu-id="288ad-515">Use range operators (<, \<=, >, >=) with a document path expression and number constants.</span></span>  
  
-   <span data-ttu-id="288ad-516">Document padexpressie staat voor een expressie waarmee een constante pad in de documenten uit de verzameling database waarnaar wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="288ad-516">Document path expression stands for any expression which identifies a constant path in the documents from the referenced database collection.</span></span>  
  
 <span data-ttu-id="288ad-517">**Document padexpressie**</span><span class="sxs-lookup"><span data-stu-id="288ad-517">**Document path expression**</span></span>  
  
 <span data-ttu-id="288ad-518">Document padexpressies zijn expressies die een pad van de eigenschap of matrix indexeerfunctie beoordelaars via een document dat afkomstig is van de database verzameling documenten.</span><span class="sxs-lookup"><span data-stu-id="288ad-518">Document path expressions are expressions that a path of property or array indexer assessors over a document coming from database collection documents.</span></span> <span data-ttu-id="288ad-519">Dit pad kan worden gebruikt voor het identificeren van de locatie van de waarden waarnaar wordt verwezen in een filter rechtstreeks in de documenten in de database-verzameling.</span><span class="sxs-lookup"><span data-stu-id="288ad-519">This path can be used to identify the location of values referenced in a filter directly within the documents in the database collection.</span></span>  
  
 <span data-ttu-id="288ad-520">Voor een expressie die moet worden beschouwd als een document padexpressie, de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="288ad-520">For an expression to be considered a document path expression, it should:</span></span>  
  
1.  <span data-ttu-id="288ad-521">Verwijst rechtstreeks naar de hoofdmap van de verzameling.</span><span class="sxs-lookup"><span data-stu-id="288ad-521">Reference the collection root directly.</span></span>  
  
2.  <span data-ttu-id="288ad-522">Verwijzing naar eigenschap of constante matrix indexeerfunctie van sommige padexpressie document</span><span class="sxs-lookup"><span data-stu-id="288ad-522">Reference property or constant array indexer of some document path expression</span></span>  
  
3.  <span data-ttu-id="288ad-523">Verwijzen naar een alias die bepaalde padexpressie document vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="288ad-523">Reference an alias, which represents some document path expression.</span></span>  
  
     <span data-ttu-id="288ad-524">**Syntaxis conventies**</span><span class="sxs-lookup"><span data-stu-id="288ad-524">**Syntax conventions**</span></span>  
  
     <span data-ttu-id="288ad-525">De volgende tabel beschrijft de conventies gebruikt om te beschrijven syntaxis in de Quertytaal van de API-verwijzing.</span><span class="sxs-lookup"><span data-stu-id="288ad-525">The following table describes the conventions used to describe syntax in the DocumentDB API Query Language reference.</span></span>  
  
    |<span data-ttu-id="288ad-526">**Conventies**</span><span class="sxs-lookup"><span data-stu-id="288ad-526">**Convention**</span></span>|<span data-ttu-id="288ad-527">**Gebruikt voor**</span><span class="sxs-lookup"><span data-stu-id="288ad-527">**Used for**</span></span>|  
    |-|-|    
    |<span data-ttu-id="288ad-528">HOOFDLETTERS</span><span class="sxs-lookup"><span data-stu-id="288ad-528">UPPERCASE</span></span>|<span data-ttu-id="288ad-529">Niet-hoofdlettergevoelige trefwoorden.</span><span class="sxs-lookup"><span data-stu-id="288ad-529">Case-insensitive keywords.</span></span>|  
    |<span data-ttu-id="288ad-530">kleine letters</span><span class="sxs-lookup"><span data-stu-id="288ad-530">lowercase</span></span>|<span data-ttu-id="288ad-531">Trefwoorden hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="288ad-531">Case-sensitive keywords.</span></span>|  
    |<span data-ttu-id="288ad-532">\<nonterminal ></span><span class="sxs-lookup"><span data-stu-id="288ad-532">\<nonterminal></span></span>|<span data-ttu-id="288ad-533">Niet-eindigende, die is gedefinieerd afzonderlijk.</span><span class="sxs-lookup"><span data-stu-id="288ad-533">Nonterminal, defined separately.</span></span>|  
    |<span data-ttu-id="288ad-534">\<nonterminal >:: =</span><span class="sxs-lookup"><span data-stu-id="288ad-534">\<nonterminal> ::=</span></span>|<span data-ttu-id="288ad-535">De definitie van de syntaxis van de nonterminal.</span><span class="sxs-lookup"><span data-stu-id="288ad-535">Syntax definition of the nonterminal.</span></span>|  
    |<span data-ttu-id="288ad-536">other_terminal</span><span class="sxs-lookup"><span data-stu-id="288ad-536">other_terminal</span></span>|<span data-ttu-id="288ad-537">Terminal (token) in de woorden in detail beschreven.</span><span class="sxs-lookup"><span data-stu-id="288ad-537">Terminal (token), described in detail in words.</span></span>|  
    |<span data-ttu-id="288ad-538">ID</span><span class="sxs-lookup"><span data-stu-id="288ad-538">identifier</span></span>|<span data-ttu-id="288ad-539">ID.</span><span class="sxs-lookup"><span data-stu-id="288ad-539">Identifier.</span></span> <span data-ttu-id="288ad-540">Kan de volgende tekens bevatten: a-z A-Z 0-9 _First teken mag niet een cijfer.</span><span class="sxs-lookup"><span data-stu-id="288ad-540">Allows following characters only: a-z A-Z 0-9 _First character cannot be a digit.</span></span>|  
    |<span data-ttu-id="288ad-541">'tekenreeks'</span><span class="sxs-lookup"><span data-stu-id="288ad-541">"string"</span></span>|<span data-ttu-id="288ad-542">Tekenreeks tussen aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="288ad-542">Quoted string.</span></span> <span data-ttu-id="288ad-543">Hiermee kunt een geldige tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="288ad-543">Allows any valid string.</span></span> <span data-ttu-id="288ad-544">Zie de beschrijving van een string_literal.</span><span class="sxs-lookup"><span data-stu-id="288ad-544">See description of a string_literal.</span></span>|  
    |<span data-ttu-id="288ad-545">"symbool"</span><span class="sxs-lookup"><span data-stu-id="288ad-545">'symbol'</span></span>|<span data-ttu-id="288ad-546">Letterlijke symbool die deel uitmaakt van de syntaxis.</span><span class="sxs-lookup"><span data-stu-id="288ad-546">Literal symbol which is part of the syntax.</span></span>|  
    |<span data-ttu-id="288ad-547">&#124; (verticale balk)</span><span class="sxs-lookup"><span data-stu-id="288ad-547">&#124; (vertical bar)</span></span>|<span data-ttu-id="288ad-548">Alternatieven voor de syntaxis van de items.</span><span class="sxs-lookup"><span data-stu-id="288ad-548">Alternatives for syntax items.</span></span> <span data-ttu-id="288ad-549">U kunt slechts één van de items die zijn opgegeven.</span><span class="sxs-lookup"><span data-stu-id="288ad-549">You can use only one of the items specified.</span></span>|  
    |<span data-ttu-id="288ad-550">[] /(brackets)</span><span class="sxs-lookup"><span data-stu-id="288ad-550">[ ] /(brackets)</span></span>|<span data-ttu-id="288ad-551">Vierkante haken plaatst u een of meer optionele items.</span><span class="sxs-lookup"><span data-stu-id="288ad-551">Brackets enclose one or more optional items.</span></span>|  
    |<span data-ttu-id="288ad-552">[,.. .n]</span><span class="sxs-lookup"><span data-stu-id="288ad-552">[ ,...n ]</span></span>|<span data-ttu-id="288ad-553">Hiermee geeft u het vorige item kunt herhaalde n het aantal keren.</span><span class="sxs-lookup"><span data-stu-id="288ad-553">Indicates the preceding item can be repeated n number of times.</span></span> <span data-ttu-id="288ad-554">De exemplaren worden gescheiden door komma's.</span><span class="sxs-lookup"><span data-stu-id="288ad-554">The occurrences are separated by commas.</span></span>|  
    |<span data-ttu-id="288ad-555">[.. .n]</span><span class="sxs-lookup"><span data-stu-id="288ad-555">[ ...n ]</span></span>|<span data-ttu-id="288ad-556">Hiermee geeft u het vorige item kunt herhaalde n het aantal keren.</span><span class="sxs-lookup"><span data-stu-id="288ad-556">Indicates the preceding item can be repeated n number of times.</span></span> <span data-ttu-id="288ad-557">De exemplaren worden gescheiden door spaties.</span><span class="sxs-lookup"><span data-stu-id="288ad-557">The occurrences are separated by blanks.</span></span>|  
  
##  <span data-ttu-id="288ad-558"><a name="bk_built_in_functions"></a>Ingebouwde functies</span><span class="sxs-lookup"><span data-stu-id="288ad-558"><a name="bk_built_in_functions"></a> Built-in functions</span></span>  
 <span data-ttu-id="288ad-559">Azure Cosmos DB biedt veel ingebouwde SQL-functies.</span><span class="sxs-lookup"><span data-stu-id="288ad-559">Azure Cosmos DB provides many built-in SQL functions.</span></span> <span data-ttu-id="288ad-560">De categorieën van ingebouwde functies worden hieronder vermeld.</span><span class="sxs-lookup"><span data-stu-id="288ad-560">The categories of built-in functions are listed below.</span></span>  
  
|<span data-ttu-id="288ad-561">Functie</span><span class="sxs-lookup"><span data-stu-id="288ad-561">Function</span></span>|<span data-ttu-id="288ad-562">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="288ad-562">Description</span></span>|  
|--------------|-----------------|  
|[<span data-ttu-id="288ad-563">Wiskundige functies</span><span class="sxs-lookup"><span data-stu-id="288ad-563">Mathematical functions</span></span>](#bk_mathematical_functions)|<span data-ttu-id="288ad-564">De rekenkundige functies elke uitvoeren een berekening, meestal op basis van de invoerwaarden die zijn opgegeven als argumenten en een numerieke waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="288ad-564">The mathematical functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>|  
|[<span data-ttu-id="288ad-565">Controle van de functies van het type</span><span class="sxs-lookup"><span data-stu-id="288ad-565">Type checking functions</span></span>](#bk_type_checking_functions)|<span data-ttu-id="288ad-566">Het type controleren of functies kunnen u om te controleren van het type van een expressie in SQL-query's.</span><span class="sxs-lookup"><span data-stu-id="288ad-566">The type checking functions allow you to check the type of an expression within SQL queries.</span></span>|  
|[<span data-ttu-id="288ad-567">Tekenreeksfuncties</span><span class="sxs-lookup"><span data-stu-id="288ad-567">String functions</span></span>](#bk_string_functions)|<span data-ttu-id="288ad-568">De tekenreeksfuncties een bewerking uitvoeren op een tekenreekswaarde van de invoer en een tekenreeks, numerieke of Booleaanse waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="288ad-568">The string functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>|  
|[<span data-ttu-id="288ad-569">Matrixfuncties</span><span class="sxs-lookup"><span data-stu-id="288ad-569">Array functions</span></span>](#bk_array_functions)|<span data-ttu-id="288ad-570">De matrixfuncties uitvoeren voor een bewerking in een matrix invoerwaarde en keer terug numerieke, de waarde voor Boole-waarde of een matrix.</span><span class="sxs-lookup"><span data-stu-id="288ad-570">The array functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span>|  
|[<span data-ttu-id="288ad-571">Ruimtelijke functies</span><span class="sxs-lookup"><span data-stu-id="288ad-571">Spatial functions</span></span>](#bk_spatial_functions)|<span data-ttu-id="288ad-572">De ruimtelijke functies een bewerking uitvoeren op een invoerwaarde ruimtelijke object en een numeriek gegevenstype of Booleaanse waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="288ad-572">The spatial functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>|  
  
###  <span data-ttu-id="288ad-573"><a name="bk_mathematical_functions"></a>Wiskundige functies</span><span class="sxs-lookup"><span data-stu-id="288ad-573"><a name="bk_mathematical_functions"></a> Mathematical functions</span></span>  
 <span data-ttu-id="288ad-574">De volgende functies elke uitvoeren van een berekening, meestal op basis van de invoerwaarden die zijn opgegeven als argumenten en een numerieke waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="288ad-574">The following functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="288ad-575">ABS</span><span class="sxs-lookup"><span data-stu-id="288ad-575">ABS</span></span>](#bk_abs)|[<span data-ttu-id="288ad-576">BOOGCOS</span><span class="sxs-lookup"><span data-stu-id="288ad-576">ACOS</span></span>](#bk_acos)|[<span data-ttu-id="288ad-577">ASIN</span><span class="sxs-lookup"><span data-stu-id="288ad-577">ASIN</span></span>](#bk_asin)|  
|[<span data-ttu-id="288ad-578">BOOGTAN</span><span class="sxs-lookup"><span data-stu-id="288ad-578">ATAN</span></span>](#bk_atan)|[<span data-ttu-id="288ad-579">ATN2</span><span class="sxs-lookup"><span data-stu-id="288ad-579">ATN2</span></span>](#bk_atn2)|[<span data-ttu-id="288ad-580">MAXIMUM</span><span class="sxs-lookup"><span data-stu-id="288ad-580">CEILING</span></span>](#bk_ceiling)|  
|[<span data-ttu-id="288ad-581">CO 'S</span><span class="sxs-lookup"><span data-stu-id="288ad-581">COS</span></span>](#bk_cos)|[<span data-ttu-id="288ad-582">COT</span><span class="sxs-lookup"><span data-stu-id="288ad-582">COT</span></span>](#bk_cot)|[<span data-ttu-id="288ad-583">GRADEN</span><span class="sxs-lookup"><span data-stu-id="288ad-583">DEGREES</span></span>](#bk_degrees)|  
|[<span data-ttu-id="288ad-584">EXP</span><span class="sxs-lookup"><span data-stu-id="288ad-584">EXP</span></span>](#bk_exp)|[<span data-ttu-id="288ad-585">FLOOR</span><span class="sxs-lookup"><span data-stu-id="288ad-585">FLOOR</span></span>](#bk_floor)|[<span data-ttu-id="288ad-586">LOGBOEK</span><span class="sxs-lookup"><span data-stu-id="288ad-586">LOG</span></span>](#bk_log)|  
|[<span data-ttu-id="288ad-587">LOG10</span><span class="sxs-lookup"><span data-stu-id="288ad-587">LOG10</span></span>](#bk_log10)|[<span data-ttu-id="288ad-588">PI</span><span class="sxs-lookup"><span data-stu-id="288ad-588">PI</span></span>](#bk_pi)|[<span data-ttu-id="288ad-589">ENERGIEBEHEER</span><span class="sxs-lookup"><span data-stu-id="288ad-589">POWER</span></span>](#bk_power)|  
|[<span data-ttu-id="288ad-590">RADIALEN</span><span class="sxs-lookup"><span data-stu-id="288ad-590">RADIANS</span></span>](#bk_radians)|[<span data-ttu-id="288ad-591">AFRONDEN</span><span class="sxs-lookup"><span data-stu-id="288ad-591">ROUND</span></span>](#bk_round)|[<span data-ttu-id="288ad-592">SIN</span><span class="sxs-lookup"><span data-stu-id="288ad-592">SIN</span></span>](#bk_sin)|  
|[<span data-ttu-id="288ad-593">SQRT</span><span class="sxs-lookup"><span data-stu-id="288ad-593">SQRT</span></span>](#bk_sqrt)|[<span data-ttu-id="288ad-594">VIERKANTE</span><span class="sxs-lookup"><span data-stu-id="288ad-594">SQUARE</span></span>](#bk_square)|[<span data-ttu-id="288ad-595">AANMELDING</span><span class="sxs-lookup"><span data-stu-id="288ad-595">SIGN</span></span>](#bk_sign)|  
|[<span data-ttu-id="288ad-596">TAN</span><span class="sxs-lookup"><span data-stu-id="288ad-596">TAN</span></span>](#bk_tan)|[<span data-ttu-id="288ad-597">GEHEEL</span><span class="sxs-lookup"><span data-stu-id="288ad-597">TRUNC</span></span>](#bk_trunc)||  
  
####  <span data-ttu-id="288ad-598"><a name="bk_abs"></a>ABS</span><span class="sxs-lookup"><span data-stu-id="288ad-598"><a name="bk_abs"></a> ABS</span></span>  
 <span data-ttu-id="288ad-599">Retourneert de absolute (positieve) waarde van de opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-599">Returns the absolute (positive) value of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-600">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-600">**Syntax**</span></span>  
  
```  
ABS (<numeric_expression>)  
```  
  
 <span data-ttu-id="288ad-601">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-601">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="288ad-602">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-602">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-603">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-603">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-604">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-604">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-605">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-605">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-606">Het volgende voorbeeld toont de resultaten van het gebruik van de functie ABS op drie verschillende aantallen.</span><span class="sxs-lookup"><span data-stu-id="288ad-606">The following example shows the results of using the ABS function on three different numbers.</span></span>  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 <span data-ttu-id="288ad-607">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-607">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <span data-ttu-id="288ad-608"><a name="bk_acos"></a>BOOGCOS</span><span class="sxs-lookup"><span data-stu-id="288ad-608"><a name="bk_acos"></a> ACOS</span></span>  
 <span data-ttu-id="288ad-609">Retourneert de hoek in radialen, waarvan de cosinus de opgegeven numerieke expressie is. ook wel de boogcosinus genoemd.</span><span class="sxs-lookup"><span data-stu-id="288ad-609">Returns the angle, in radians, whose cosine is the specified numeric expression; also called arccosine.</span></span>  
  
 <span data-ttu-id="288ad-610">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-610">**Syntax**</span></span>  
  
```  
ACOS(<numeric_expression>)  
```  
  
 <span data-ttu-id="288ad-611">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-611">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="288ad-612">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-612">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-613">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-613">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-614">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-614">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-615">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-615">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-616">Het volgende voorbeeld retourneert de BOOGCOS van-1.</span><span class="sxs-lookup"><span data-stu-id="288ad-616">The following example returns the ACOS of -1.</span></span>  
  
```  
SELECT ACOS(-1)  
```  
  
 <span data-ttu-id="288ad-617">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-617">Here is the result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="288ad-618"><a name="bk_asin"></a>ASIN</span><span class="sxs-lookup"><span data-stu-id="288ad-618"><a name="bk_asin"></a> ASIN</span></span>  
 <span data-ttu-id="288ad-619">Retourneert de hoek in radialen, waarvan de sinus de opgegeven numerieke expressie is.</span><span class="sxs-lookup"><span data-stu-id="288ad-619">Returns the angle, in radians, whose sine is the specified numeric expression.</span></span> <span data-ttu-id="288ad-620">Dit wordt ook boogsinus genoemd.</span><span class="sxs-lookup"><span data-stu-id="288ad-620">This is also called arcsine.</span></span>  
  
 <span data-ttu-id="288ad-621">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-621">**Syntax**</span></span>  
  
```  
ASIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="288ad-622">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-622">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="288ad-623">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-623">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-624">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-624">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-625">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-625">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-626">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-626">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-627">Het volgende voorbeeld retourneert de ASIN van-1.</span><span class="sxs-lookup"><span data-stu-id="288ad-627">The following example returns the ASIN of -1.</span></span>  
  
```  
SELECT ASIN(-1)  
```  
  
 <span data-ttu-id="288ad-628">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-628">Here is the result set.</span></span>  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <span data-ttu-id="288ad-629"><a name="bk_atan"></a>BOOGTAN</span><span class="sxs-lookup"><span data-stu-id="288ad-629"><a name="bk_atan"></a> ATAN</span></span>  
 <span data-ttu-id="288ad-630">Retourneert de hoek in radialen, waarvan de tangens de opgegeven numerieke expressie is.</span><span class="sxs-lookup"><span data-stu-id="288ad-630">Returns the angle, in radians, whose tangent is the specified numeric expression.</span></span> <span data-ttu-id="288ad-631">Dit wordt ook arctangens genoemd.</span><span class="sxs-lookup"><span data-stu-id="288ad-631">This is also called arctangent.</span></span>  
  
 <span data-ttu-id="288ad-632">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-632">**Syntax**</span></span>  
  
```  
ATAN(<numeric_expression>)  
```  
  
 <span data-ttu-id="288ad-633">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-633">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="288ad-634">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-634">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-635">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-635">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-636">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-636">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-637">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-637">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-638">Het volgende voorbeeld retourneert de BOOGTAN van de opgegeven waarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-638">The following example returns the ATAN of the specified value.</span></span>  
  
```  
SELECT ATAN(-45.01)  
```  
  
 <span data-ttu-id="288ad-639">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-639">Here is the result set.</span></span>  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <span data-ttu-id="288ad-640"><a name="bk_atn2"></a>ATN2</span><span class="sxs-lookup"><span data-stu-id="288ad-640"><a name="bk_atn2"></a> ATN2</span></span>  
 <span data-ttu-id="288ad-641">Retourneert de hoofdsom van de arctangens van y / x, uitgedrukt in radialen.</span><span class="sxs-lookup"><span data-stu-id="288ad-641">Returns the principal value of the arc tangent of y/x, expressed in radians.</span></span>  
  
 <span data-ttu-id="288ad-642">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-642">**Syntax**</span></span>  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 <span data-ttu-id="288ad-643">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-643">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="288ad-644">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-644">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-645">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-645">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-646">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-646">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-647">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-647">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-648">Het volgende voorbeeld wordt de ATN2 voor het opgegeven berekend x en y onderdelen.</span><span class="sxs-lookup"><span data-stu-id="288ad-648">The following example calculates the ATN2 for the specified x and y components.</span></span>  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 <span data-ttu-id="288ad-649">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-649">Here is the result set.</span></span>  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <span data-ttu-id="288ad-650"><a name="bk_ceiling"></a>MAXIMUM</span><span class="sxs-lookup"><span data-stu-id="288ad-650"><a name="bk_ceiling"></a> CEILING</span></span>  
 <span data-ttu-id="288ad-651">Retourneert de kleinste waarde van geheel getal groter dan of gelijk zijn aan de opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-651">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-652">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-652">**Syntax**</span></span>  
  
```  
CEILING (<numeric_expression>)  
```  
  
 <span data-ttu-id="288ad-653">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-653">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="288ad-654">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-654">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-655">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-655">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-656">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-656">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-657">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-657">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-658">Het volgende voorbeeld toont een positieve numerieke, negatieve en nulwaarden met de functie CEILING.</span><span class="sxs-lookup"><span data-stu-id="288ad-658">The following example shows positive numeric, negative, and zero values with the CEILING function.</span></span>  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 <span data-ttu-id="288ad-659">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-659">Here is the result set.</span></span>  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <span data-ttu-id="288ad-660"><a name="bk_cos"></a>CO 'S</span><span class="sxs-lookup"><span data-stu-id="288ad-660"><a name="bk_cos"></a> COS</span></span>  
 <span data-ttu-id="288ad-661">Retourneert de trigonometrische cosinus van de opgegeven hoek in radialen in de opgegeven expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-661">Returns the trigonometric cosine of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="288ad-662">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-662">**Syntax**</span></span>  
  
```  
COS(<numeric_expression>)  
```  
  
 <span data-ttu-id="288ad-663">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-663">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="288ad-664">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-664">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-665">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-665">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-666">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-666">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-667">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-667">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-668">Het volgende voorbeeld berekent de Cosinus van de opgegeven hoek.</span><span class="sxs-lookup"><span data-stu-id="288ad-668">The following example calculates the COS of the specified angle.</span></span>  
  
```  
SELECT COS(14.78)  
```  
  
 <span data-ttu-id="288ad-669">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-669">Here is the result set.</span></span>  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <span data-ttu-id="288ad-670"><a name="bk_cot"></a>COT</span><span class="sxs-lookup"><span data-stu-id="288ad-670"><a name="bk_cot"></a> COT</span></span>  
 <span data-ttu-id="288ad-671">Retourneert de trigonometrische cotangens van de opgegeven hoek in radialen in het opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-671">Returns the trigonometric cotangent of the specified angle, in radians, in the specified numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-672">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-672">**Syntax**</span></span>  
  
```  
COT(<numeric_expression>)  
```  
  
 <span data-ttu-id="288ad-673">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-673">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="288ad-674">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-674">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-675">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-675">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-676">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-676">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-677">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-677">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-678">Het volgende voorbeeld berekent de COT van de opgegeven hoek.</span><span class="sxs-lookup"><span data-stu-id="288ad-678">The following example calculates the COT of the specified angle.</span></span>  
  
```  
SELECT COT(124.1332)  
```  
  
 <span data-ttu-id="288ad-679">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-679">Here is the result set.</span></span>  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <span data-ttu-id="288ad-680"><a name="bk_degrees"></a>GRADEN</span><span class="sxs-lookup"><span data-stu-id="288ad-680"><a name="bk_degrees"></a> DEGREES</span></span>  
 <span data-ttu-id="288ad-681">Retourneert de overeenkomstige hoek in graden voor een hoek aangeduid in radialen.</span><span class="sxs-lookup"><span data-stu-id="288ad-681">Returns the corresponding angle in degrees for an angle specified in radians.</span></span>  
  
 <span data-ttu-id="288ad-682">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-682">**Syntax**</span></span>  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 <span data-ttu-id="288ad-683">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-683">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="288ad-684">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-684">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-685">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-685">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-686">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-686">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-687">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-687">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-688">Het volgende voorbeeld retourneert het aantal graden in een hoek van PI/2 radialen.</span><span class="sxs-lookup"><span data-stu-id="288ad-688">The following example returns the number of degrees in an angle of PI/2 radians.</span></span>  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 <span data-ttu-id="288ad-689">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-689">Here is the result set.</span></span>  
  
```  
[{"$1": 90}]  
```  
  
####  <span data-ttu-id="288ad-690"><a name="bk_floor"></a>FLOOR</span><span class="sxs-lookup"><span data-stu-id="288ad-690"><a name="bk_floor"></a> FLOOR</span></span>  
 <span data-ttu-id="288ad-691">Retourneert het grootste gehele getal kleiner dan of gelijk zijn aan de opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-691">Returns the largest integer less than or equal to the specified numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-692">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-692">**Syntax**</span></span>  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 <span data-ttu-id="288ad-693">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-693">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="288ad-694">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-694">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-695">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-695">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-696">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-696">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-697">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-697">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-698">Het volgende voorbeeld toont een positieve numerieke, negatieve en nulwaarden met de functie FLOOR.</span><span class="sxs-lookup"><span data-stu-id="288ad-698">The following example shows positive numeric, negative, and zero values with the FLOOR function.</span></span>  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 <span data-ttu-id="288ad-699">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-699">Here is the result set.</span></span>  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <span data-ttu-id="288ad-700"><a name="bk_exp"></a>EXP</span><span class="sxs-lookup"><span data-stu-id="288ad-700"><a name="bk_exp"></a> EXP</span></span>  
 <span data-ttu-id="288ad-701">Berekent de exponentiële waarde van de opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-701">Returns the exponential value of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-702">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-702">**Syntax**</span></span>  
  
```  
EXP (<numeric_expression>)  
```  
  
 <span data-ttu-id="288ad-703">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-703">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="288ad-704">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-704">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-705">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-705">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-706">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-706">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-707">**Opmerkingen**</span><span class="sxs-lookup"><span data-stu-id="288ad-707">**Remarks**</span></span>  
  
 <span data-ttu-id="288ad-708">De constante **e** (2.718281...) de basis van de natuurlijke logaritme.</span><span class="sxs-lookup"><span data-stu-id="288ad-708">The constant **e** (2.718281…), is the base of natural logarithms.</span></span>  
  
 <span data-ttu-id="288ad-709">De exponent van een getal is de constante **e** tot de macht van het getal.</span><span class="sxs-lookup"><span data-stu-id="288ad-709">The exponent of a number is the constant **e** raised to the power of the number.</span></span> <span data-ttu-id="288ad-710">Bijvoorbeeld EXP(1.0) e = ^ 1.0 = 2.71828182845905 en EXP(10) e = ^ 10 = 22026.4657948067.</span><span class="sxs-lookup"><span data-stu-id="288ad-710">For example EXP(1.0) = e^1.0 = 2.71828182845905 and EXP(10) = e^10 = 22026.4657948067.</span></span>  
  
 <span data-ttu-id="288ad-711">De exponentiële waarde van de natuurlijke logaritme van een getal is het aantal zelf: EXP (LOGBOEKREGISTRATIE (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="288ad-711">The exponential of the natural logarithm of a number is the number itself: EXP (LOG (n)) = n.</span></span> <span data-ttu-id="288ad-712">En de natuurlijke logaritme van de exponentiële van een getal is het aantal zelf: logboek (EXP (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="288ad-712">And the natural logarithm of the exponential of a number is the number itself: LOG (EXP (n)) = n.</span></span>  
  
 <span data-ttu-id="288ad-713">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-713">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-714">Het volgende voorbeeld wordt een variabele gedeclareerd en berekent de exponentiële waarde van de opgegeven variabele (10).</span><span class="sxs-lookup"><span data-stu-id="288ad-714">The following example declares a variable and returns the exponential value of the specified variable (10).</span></span>  
  
```  
SELECT EXP(10)  
```  
  
 <span data-ttu-id="288ad-715">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-715">Here is the result set.</span></span>  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 <span data-ttu-id="288ad-716">Het volgende voorbeeld retourneert de exponentiële waarde van de natural logarithm van 20 en de natuurlijke logaritme van de exponentiële van 20.</span><span class="sxs-lookup"><span data-stu-id="288ad-716">The following example returns the exponential value of the natural logarithm of 20 and the natural logarithm of the exponential of 20.</span></span> <span data-ttu-id="288ad-717">Omdat deze functies inverse functies van elkaar zijn, is de retourwaarde voor drijvende punt math in beide gevallen afgeronde 20.</span><span class="sxs-lookup"><span data-stu-id="288ad-717">Because these functions are inverse functions of one another, the return value with rounding for floating point math in both cases is 20.</span></span>  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 <span data-ttu-id="288ad-718">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-718">Here is the result set.</span></span>  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <span data-ttu-id="288ad-719"><a name="bk_log"></a>LOGBOEK</span><span class="sxs-lookup"><span data-stu-id="288ad-719"><a name="bk_log"></a> LOG</span></span>  
 <span data-ttu-id="288ad-720">Retourneert de natuurlijke logaritme van de opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-720">Returns the natural logarithm of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-721">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-721">**Syntax**</span></span>  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 <span data-ttu-id="288ad-722">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-722">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="288ad-723">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-723">Is a numeric expression.</span></span>  
  
-   `base`  
  
     <span data-ttu-id="288ad-724">Optionele numerieke argument dat Hiermee stelt u de basis voor de logaritme.</span><span class="sxs-lookup"><span data-stu-id="288ad-724">Optional numeric argument that sets the base for the logarithm.</span></span>  
  
 <span data-ttu-id="288ad-725">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-725">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-726">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-726">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-727">**Opmerkingen**</span><span class="sxs-lookup"><span data-stu-id="288ad-727">**Remarks**</span></span>  
  
 <span data-ttu-id="288ad-728">Standaard retourneert LOG() de natuurlijke logaritme.</span><span class="sxs-lookup"><span data-stu-id="288ad-728">By default, LOG() returns the natural logarithm.</span></span> <span data-ttu-id="288ad-729">U kunt het grondtal van de logaritme met een andere waarde wijzigen met behulp van de optionele parameter basis.</span><span class="sxs-lookup"><span data-stu-id="288ad-729">You can change the base of the logarithm to another value by using the optional base parameter.</span></span>  
  
 <span data-ttu-id="288ad-730">De natuurlijke logaritme is de logaritme met het grondtal **e**, waarbij **e** is een constante irrational ongeveer gelijk aan 2.718281828.</span><span class="sxs-lookup"><span data-stu-id="288ad-730">The natural logarithm is the logarithm to the base **e**, where **e** is an irrational constant approximately equal to 2.718281828.</span></span>  
  
 <span data-ttu-id="288ad-731">De natuurlijke logaritme van de exponentiële van een getal is het aantal zelf: logboek (EXP (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="288ad-731">The natural logarithm of the exponential of a number is the number itself: LOG( EXP( n ) ) = n.</span></span> <span data-ttu-id="288ad-732">En de exponentiële waarde van de natuurlijke logaritme van een getal is het aantal zelf: EXP (LOGBOEKREGISTRATIE (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="288ad-732">And the exponential of the natural logarithm of a number is the number itself: EXP( LOG( n ) ) = n.</span></span>  
  
 <span data-ttu-id="288ad-733">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-733">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-734">Het volgende voorbeeld wordt een variabele gedeclareerd en retourneert de waarde van de logaritme van de opgegeven variabele (10).</span><span class="sxs-lookup"><span data-stu-id="288ad-734">The following example declares a variable and returns the logarithm value of the specified variable (10).</span></span>  
  
```  
SELECT LOG(10)  
```  
  
 <span data-ttu-id="288ad-735">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-735">Here is the result set.</span></span>  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 <span data-ttu-id="288ad-736">Het volgende voorbeeld wordt het logboek voor de exponent van een getal berekend.</span><span class="sxs-lookup"><span data-stu-id="288ad-736">The following example calculates the LOG for the exponent of a number.</span></span>  
  
```  
SELECT EXP(LOG(10))  
```  
  
 <span data-ttu-id="288ad-737">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-737">Here is the result set.</span></span>  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <span data-ttu-id="288ad-738"><a name="bk_log10"></a>LOG10</span><span class="sxs-lookup"><span data-stu-id="288ad-738"><a name="bk_log10"></a> LOG10</span></span>  
 <span data-ttu-id="288ad-739">Retourneert de logaritme met grondtal 10 van de opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-739">Returns the base-10 logarithm of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-740">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-740">**Syntax**</span></span>  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 <span data-ttu-id="288ad-741">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-741">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="288ad-742">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-742">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-743">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-743">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-744">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-744">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-745">**Opmerkingen**</span><span class="sxs-lookup"><span data-stu-id="288ad-745">**Remarks**</span></span>  
  
 <span data-ttu-id="288ad-746">De functies LOG10 en POWER zijn omgekeerd aan elkaar gerelateerd.</span><span class="sxs-lookup"><span data-stu-id="288ad-746">The LOG10 and POWER functions are inversely related to one another.</span></span> <span data-ttu-id="288ad-747">Bijvoorbeeld 10 ^ LOG10(n) = n.</span><span class="sxs-lookup"><span data-stu-id="288ad-747">For example, 10 ^ LOG10(n) = n.</span></span>  
  
 <span data-ttu-id="288ad-748">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-748">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-749">Het volgende voorbeeld wordt een variabele gedeclareerd en retourneert de waarde LOG10 van de opgegeven variabele (100).</span><span class="sxs-lookup"><span data-stu-id="288ad-749">The following example declares a variable and returns the LOG10 value of the specified variable (100).</span></span>  
  
```  
SELECT LOG10(100)  
```  
  
 <span data-ttu-id="288ad-750">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-750">Here is the result set.</span></span>  
  
```  
[{$1: 2}]  
```  
  
####  <span data-ttu-id="288ad-751"><a name="bk_pi"></a>PI</span><span class="sxs-lookup"><span data-stu-id="288ad-751"><a name="bk_pi"></a> PI</span></span>  
 <span data-ttu-id="288ad-752">Retourneert de constante waarde van PI.</span><span class="sxs-lookup"><span data-stu-id="288ad-752">Returns the constant value of PI.</span></span>  
  
 <span data-ttu-id="288ad-753">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-753">**Syntax**</span></span>  
  
```  
PI ()  
```  
  
 <span data-ttu-id="288ad-754">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-754">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="288ad-755">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-755">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-756">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-756">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-757">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-757">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-758">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-758">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-759">Het volgende voorbeeld retourneert de waarde van PI.</span><span class="sxs-lookup"><span data-stu-id="288ad-759">The following example returns the value of PI.</span></span>  
  
```  
SELECT PI()  
```  
  
 <span data-ttu-id="288ad-760">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-760">Here is the result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="288ad-761"><a name="bk_power"></a>ENERGIEBEHEER</span><span class="sxs-lookup"><span data-stu-id="288ad-761"><a name="bk_power"></a> POWER</span></span>  
 <span data-ttu-id="288ad-762">Retourneert de waarde van de opgegeven expressie voor de opgegeven macht.</span><span class="sxs-lookup"><span data-stu-id="288ad-762">Returns the value of the specified expression to the specified power.</span></span>  
  
 <span data-ttu-id="288ad-763">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-763">**Syntax**</span></span>  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 <span data-ttu-id="288ad-764">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-764">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="288ad-765">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-765">Is a numeric expression.</span></span>  
  
-   `y`  
  
     <span data-ttu-id="288ad-766">Is de macht waarnaar u wilt activeren `numeric_expression`.</span><span class="sxs-lookup"><span data-stu-id="288ad-766">Is the power to which to raise `numeric_expression`.</span></span>  
  
 <span data-ttu-id="288ad-767">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-767">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-768">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-768">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-769">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-769">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-770">Het volgende voorbeeld wordt een getal tot de macht 3 (de kubus van het getal) te verhogen.</span><span class="sxs-lookup"><span data-stu-id="288ad-770">The following example demonstrates raising a number to the power of 3 (the cube of the number).</span></span>  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 <span data-ttu-id="288ad-771">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-771">Here is the result set.</span></span>  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <span data-ttu-id="288ad-772"><a name="bk_radians"></a>RADIALEN</span><span class="sxs-lookup"><span data-stu-id="288ad-772"><a name="bk_radians"></a> RADIANS</span></span>  
 <span data-ttu-id="288ad-773">Retourneert radialen wanneer een numerieke expressie, in graden wordt ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="288ad-773">Returns radians when a numeric expression, in degrees, is entered.</span></span>  
  
 <span data-ttu-id="288ad-774">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-774">**Syntax**</span></span>  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 <span data-ttu-id="288ad-775">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-775">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="288ad-776">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-776">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-777">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-777">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-778">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-778">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-779">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-779">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-780">Het volgende voorbeeld duurt een paar hoeken als invoer en de bijbehorende Radiaal waarden retourneert.</span><span class="sxs-lookup"><span data-stu-id="288ad-780">The following example takes a few angles as input and returns their corresponding radian values.</span></span>  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 <span data-ttu-id="288ad-781">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-781">Here is the result set.</span></span>  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <span data-ttu-id="288ad-782"><a name="bk_round"></a>AFRONDEN</span><span class="sxs-lookup"><span data-stu-id="288ad-782"><a name="bk_round"></a> ROUND</span></span>  
 <span data-ttu-id="288ad-783">Retourneert een numerieke waarde, op het dichtstbijzijnde gehele getal afgerond.</span><span class="sxs-lookup"><span data-stu-id="288ad-783">Returns a numeric value, rounded to the closest integer value.</span></span>  
  
 <span data-ttu-id="288ad-784">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-784">**Syntax**</span></span>  
  
```  
ROUND(<numeric_expression>)  
```  
  
 <span data-ttu-id="288ad-785">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-785">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="288ad-786">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-786">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-787">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-787">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-788">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-788">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-789">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-789">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-790">Het volgende voorbeeld wordt de volgende positieve en negatieve getallen naar het dichtstbijzijnde gehele getal afgerond.</span><span class="sxs-lookup"><span data-stu-id="288ad-790">The following example rounds the following positive and negative numbers to the nearest integer.</span></span>  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 <span data-ttu-id="288ad-791">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-791">Here is the result set.</span></span>  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <span data-ttu-id="288ad-792"><a name="bk_sign"></a>AANMELDING</span><span class="sxs-lookup"><span data-stu-id="288ad-792"><a name="bk_sign"></a> SIGN</span></span>  
 <span data-ttu-id="288ad-793">Retourneert de positief (+ 1), nul (0) of minteken (-1) van de opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-793">Returns the positive (+1), zero (0), or negative (-1) sign of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-794">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-794">**Syntax**</span></span>  
  
```  
SIGN(<numeric_expression>)  
```  
  
 <span data-ttu-id="288ad-795">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-795">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="288ad-796">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-796">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-797">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-797">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-798">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-798">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-799">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-799">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-800">Het volgende voorbeeld retourneert de waarden van de aanmelding van de getallen van -2 op 2.</span><span class="sxs-lookup"><span data-stu-id="288ad-800">The following example returns the SIGN values of numbers from -2 to 2.</span></span>  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 <span data-ttu-id="288ad-801">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-801">Here is the result set.</span></span>  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <span data-ttu-id="288ad-802"><a name="bk_sin"></a>SIN</span><span class="sxs-lookup"><span data-stu-id="288ad-802"><a name="bk_sin"></a> SIN</span></span>  
 <span data-ttu-id="288ad-803">Retourneert de trigonometrische sinus van de opgegeven hoek in radialen in de opgegeven expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-803">Returns the trigonometric sine of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="288ad-804">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-804">**Syntax**</span></span>  
  
```  
SIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="288ad-805">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-805">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="288ad-806">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-806">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-807">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-807">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-808">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-808">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-809">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-809">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-810">Het volgende voorbeeld berekent de SINUS van de opgegeven hoek.</span><span class="sxs-lookup"><span data-stu-id="288ad-810">The following example calculates the SIN of the specified angle.</span></span>  
  
```  
SELECT SIN(45.175643)  
```  
  
 <span data-ttu-id="288ad-811">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-811">Here is the result set.</span></span>  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <span data-ttu-id="288ad-812"><a name="bk_sqrt"></a>SQRT</span><span class="sxs-lookup"><span data-stu-id="288ad-812"><a name="bk_sqrt"></a> SQRT</span></span>  
 <span data-ttu-id="288ad-813">Retourneert de vierkantswortel van de numerieke waarde die is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="288ad-813">Returns the square root of the specified numeric value.</span></span>  
  
 <span data-ttu-id="288ad-814">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-814">**Syntax**</span></span>  
  
```  
SQRT(<numeric_expression>)  
```  
  
 <span data-ttu-id="288ad-815">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-815">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="288ad-816">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-816">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-817">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-817">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-818">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-818">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-819">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-819">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-820">Het volgende voorbeeld retourneert de hoofdmappen kwadraat van getallen 1-3.</span><span class="sxs-lookup"><span data-stu-id="288ad-820">The following example returns the square roots of numbers 1-3.</span></span>  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 <span data-ttu-id="288ad-821">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-821">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <span data-ttu-id="288ad-822"><a name="bk_square"></a>VIERKANTE</span><span class="sxs-lookup"><span data-stu-id="288ad-822"><a name="bk_square"></a> SQUARE</span></span>  
 <span data-ttu-id="288ad-823">Retourneert het kwadraat van de numerieke waarde die is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="288ad-823">Returns the square of the specified numeric value.</span></span>  
  
 <span data-ttu-id="288ad-824">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-824">**Syntax**</span></span>  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 <span data-ttu-id="288ad-825">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-825">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="288ad-826">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-826">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-827">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-827">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-828">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-828">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-829">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-829">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-830">Het volgende voorbeeld retourneert de kwadraten van getallen 1-3.</span><span class="sxs-lookup"><span data-stu-id="288ad-830">The following example returns the squares of numbers 1-3.</span></span>  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 <span data-ttu-id="288ad-831">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-831">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <span data-ttu-id="288ad-832"><a name="bk_tan"></a>TAN</span><span class="sxs-lookup"><span data-stu-id="288ad-832"><a name="bk_tan"></a> TAN</span></span>  
 <span data-ttu-id="288ad-833">Retourneert de tangens van de opgegeven hoek in radialen in de opgegeven expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-833">Returns the tangent of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="288ad-834">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-834">**Syntax**</span></span>  
  
```  
TAN (<numeric_expression>)  
```  
  
 <span data-ttu-id="288ad-835">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-835">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="288ad-836">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-836">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-837">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-837">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-838">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-838">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-839">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-839">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-840">Het volgende voorbeeld wordt de tangens van PI () berekend / 2.</span><span class="sxs-lookup"><span data-stu-id="288ad-840">The following example calculates the tangent of PI()/2.</span></span>  
  
```  
SELECT TAN(PI()/2);  
```  
  
 <span data-ttu-id="288ad-841">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-841">Here is the result set.</span></span>  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <span data-ttu-id="288ad-842"><a name="bk_trunc"></a>GEHEEL</span><span class="sxs-lookup"><span data-stu-id="288ad-842"><a name="bk_trunc"></a> TRUNC</span></span>  
 <span data-ttu-id="288ad-843">Retourneert een numerieke waarde, afgekapt tot het dichtstbijzijnde gehele getal.</span><span class="sxs-lookup"><span data-stu-id="288ad-843">Returns a numeric value, truncated to the closest integer value.</span></span>  
  
 <span data-ttu-id="288ad-844">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-844">**Syntax**</span></span>  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 <span data-ttu-id="288ad-845">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-845">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="288ad-846">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-846">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-847">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-847">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-848">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-848">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-849">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-849">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-850">Het volgende voorbeeld wordt de volgende positieve en negatieve getallen naar het dichtstbijzijnde gehele getal afgekapt.</span><span class="sxs-lookup"><span data-stu-id="288ad-850">The following example truncates the following positive and negative numbers to the nearest integer value.</span></span>  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 <span data-ttu-id="288ad-851">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-851">Here is the result set.</span></span>  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <span data-ttu-id="288ad-852"><a name="bk_type_checking_functions"></a>Controle van de functies van het type</span><span class="sxs-lookup"><span data-stu-id="288ad-852"><a name="bk_type_checking_functions"></a> Type checking functions</span></span>  
 <span data-ttu-id="288ad-853">De volgende functies ondersteunen typecontrole tegen invoerwaarden en elk een Booleaanse waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="288ad-853">The following functions support type checking against input values, and each return a Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="288ad-854">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="288ad-854">IS_ARRAY</span></span>](#bk_is_array)|[<span data-ttu-id="288ad-855">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="288ad-855">IS_BOOL</span></span>](#bk_is_bool)|[<span data-ttu-id="288ad-856">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="288ad-856">IS_DEFINED</span></span>](#bk_is_defined)|  
|[<span data-ttu-id="288ad-857">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="288ad-857">IS_NULL</span></span>](#bk_is_null)|[<span data-ttu-id="288ad-858">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="288ad-858">IS_NUMBER</span></span>](#bk_is_number)|[<span data-ttu-id="288ad-859">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="288ad-859">IS_OBJECT</span></span>](#bk_is_object)|  
|[<span data-ttu-id="288ad-860">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="288ad-860">IS_PRIMITIVE</span></span>](#bk_is_primitive)|[<span data-ttu-id="288ad-861">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="288ad-861">IS_STRING</span></span>](#bk_is_string)||  
  
####  <span data-ttu-id="288ad-862"><a name="bk_is_array"></a>IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="288ad-862"><a name="bk_is_array"></a> IS_ARRAY</span></span>  
 <span data-ttu-id="288ad-863">Retourneert een Booleaanse waarde die aangeeft of het type van de opgegeven expressie een matrix is.</span><span class="sxs-lookup"><span data-stu-id="288ad-863">Returns a Boolean value indicating if the type of the specified expression is an array.</span></span>  
  
 <span data-ttu-id="288ad-864">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-864">**Syntax**</span></span>  
  
```  
IS_ARRAY(<expression>)  
```  
  
 <span data-ttu-id="288ad-865">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-865">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="288ad-866">Is geldige expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-866">Is any valid expression.</span></span>  
  
 <span data-ttu-id="288ad-867">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-867">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-868">Retourneert een Booleaanse expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-868">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="288ad-869">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-869">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-870">Het volgende voorbeeld controleert objecten van JSON Boolean, getal, string, null, object, matrix en niet-gedefinieerde typen met de functie IS_ARRAY.</span><span class="sxs-lookup"><span data-stu-id="288ad-870">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_ARRAY function.</span></span>  
  
```  
SELECT   
 IS_ARRAY(true),   
 IS_ARRAY(1),  
 IS_ARRAY("value"),  
 IS_ARRAY(null),  
 IS_ARRAY({prop: "value"}),   
 IS_ARRAY([1, 2, 3]),  
 IS_ARRAY({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="288ad-871">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-871">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <span data-ttu-id="288ad-872"><a name="bk_is_bool"></a>IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="288ad-872"><a name="bk_is_bool"></a> IS_BOOL</span></span>  
 <span data-ttu-id="288ad-873">Retourneert een Booleaanse waarde die aangeeft of het type van de opgegeven expressie een Booleaanse waarde is.</span><span class="sxs-lookup"><span data-stu-id="288ad-873">Returns a Boolean value indicating if the type of the specified expression is a Boolean.</span></span>  
  
 <span data-ttu-id="288ad-874">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-874">**Syntax**</span></span>  
  
```  
IS_BOOL(<expression>)  
```  
  
 <span data-ttu-id="288ad-875">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-875">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="288ad-876">Is geldige expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-876">Is any valid expression.</span></span>  
  
 <span data-ttu-id="288ad-877">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-877">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-878">Retourneert een Booleaanse expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-878">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="288ad-879">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-879">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-880">Het volgende voorbeeld controleert objecten van JSON Boolean, getal, string, null, object, matrix en niet-gedefinieerde typen met de functie IS_BOOL.</span><span class="sxs-lookup"><span data-stu-id="288ad-880">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_BOOL function.</span></span>  
  
```  
SELECT   
    IS_BOOL(true),   
    IS_BOOL(1),  
    IS_BOOL("value"),   
    IS_BOOL(null),  
    IS_BOOL({prop: "value"}),   
    IS_BOOL([1, 2, 3]),  
    IS_BOOL({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="288ad-881">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-881">Here is the result set.</span></span>  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="288ad-882"><a name="bk_is_defined"></a>IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="288ad-882"><a name="bk_is_defined"></a> IS_DEFINED</span></span>  
 <span data-ttu-id="288ad-883">Retourneert een Booleaanse waarde die aangeeft of de eigenschap een waarde is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="288ad-883">Returns a Boolean indicating if the property has been assigned a value.</span></span>  
  
 <span data-ttu-id="288ad-884">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-884">**Syntax**</span></span>  
  
```  
IS_DEFINED(<expression>)  
```  
  
 <span data-ttu-id="288ad-885">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-885">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="288ad-886">Is geldige expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-886">Is any valid expression.</span></span>  
  
 <span data-ttu-id="288ad-887">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-887">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-888">Retourneert een Booleaanse expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-888">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="288ad-889">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-889">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-890">Het volgende voorbeeld wordt gecontroleerd op de aanwezigheid van een eigenschap binnen het opgegeven JSON-document.</span><span class="sxs-lookup"><span data-stu-id="288ad-890">The following example checks for the presence of a property within the specified JSON document.</span></span> <span data-ttu-id="288ad-891">De eerste retourneert true omdat "a" aanwezig is, maar de tweede onwaar retourneert omdat "b" ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="288ad-891">The first returns true since "a" is present, but the second returns false since "b" is absent.</span></span>  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 <span data-ttu-id="288ad-892">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-892">Here is the result set.</span></span>  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <span data-ttu-id="288ad-893"><a name="bk_is_null"></a>IS_NULL</span><span class="sxs-lookup"><span data-stu-id="288ad-893"><a name="bk_is_null"></a> IS_NULL</span></span>  
 <span data-ttu-id="288ad-894">Retourneert een Booleaanse waarde die aangeeft of het type van de opgegeven expressie null is.</span><span class="sxs-lookup"><span data-stu-id="288ad-894">Returns a Boolean value indicating if the type of the specified expression is null.</span></span>  
  
 <span data-ttu-id="288ad-895">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-895">**Syntax**</span></span>  
  
```  
IS_NULL(<expression>)  
```  
  
 <span data-ttu-id="288ad-896">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-896">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="288ad-897">Is geldige expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-897">Is any valid expression.</span></span>  
  
 <span data-ttu-id="288ad-898">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-898">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-899">Retourneert een Booleaanse expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-899">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="288ad-900">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-900">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-901">Het volgende voorbeeld controleert objecten van JSON Boolean, getal, string, null, object, matrix en niet-gedefinieerde typen met de functie IS_NULL.</span><span class="sxs-lookup"><span data-stu-id="288ad-901">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_NULL function.</span></span>  
  
```  
SELECT   
    IS_NULL(true),   
    IS_NULL(1),  
    IS_NULL("value"),   
    IS_NULL(null),  
    IS_NULL({prop: "value"}),   
    IS_NULL([1, 2, 3]),  
    IS_NULL({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="288ad-902">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-902">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="288ad-903"><a name="bk_is_number"></a>IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="288ad-903"><a name="bk_is_number"></a> IS_NUMBER</span></span>  
 <span data-ttu-id="288ad-904">Retourneert een Booleaanse waarde die aangeeft of het type van de opgegeven expressie is van een getal.</span><span class="sxs-lookup"><span data-stu-id="288ad-904">Returns a Boolean value indicating if the type of the specified expression is a number.</span></span>  
  
 <span data-ttu-id="288ad-905">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-905">**Syntax**</span></span>  
  
```  
IS_NUMBER(<expression>)  
```  
  
 <span data-ttu-id="288ad-906">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-906">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="288ad-907">Is geldige expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-907">Is any valid expression.</span></span>  
  
 <span data-ttu-id="288ad-908">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-908">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-909">Retourneert een Booleaanse expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-909">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="288ad-910">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-910">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-911">Het volgende voorbeeld controleert objecten van JSON Boolean, getal, string, null, object, matrix en niet-gedefinieerde typen met de functie IS_NULL.</span><span class="sxs-lookup"><span data-stu-id="288ad-911">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_NULL function.</span></span>  
  
```  
SELECT   
    IS_NUMBER(true),   
    IS_NUMBER(1),  
    IS_NUMBER("value"),   
    IS_NUMBER(null),  
    IS_NUMBER({prop: "value"}),   
    IS_NUMBER([1, 2, 3]),  
    IS_NUMBER({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="288ad-912">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-912">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="288ad-913"><a name="bk_is_object"></a>IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="288ad-913"><a name="bk_is_object"></a> IS_OBJECT</span></span>  
 <span data-ttu-id="288ad-914">Retourneert een Booleaanse waarde die aangeeft of het type van de opgegeven expressie een JSON-object is.</span><span class="sxs-lookup"><span data-stu-id="288ad-914">Returns a Boolean value indicating if the type of the specified expression is a JSON object.</span></span>  
  
 <span data-ttu-id="288ad-915">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-915">**Syntax**</span></span>  
  
```  
IS_OBJECT(<expression>)  
```  
  
 <span data-ttu-id="288ad-916">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-916">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="288ad-917">Is geldige expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-917">Is any valid expression.</span></span>  
  
 <span data-ttu-id="288ad-918">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-918">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-919">Retourneert een Booleaanse expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-919">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="288ad-920">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-920">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-921">Het volgende voorbeeld controleert objecten van JSON Boolean, getal, string, null, object, matrix en niet-gedefinieerde typen met de functie IS_OBJECT.</span><span class="sxs-lookup"><span data-stu-id="288ad-921">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_OBJECT function.</span></span>  
  
```  
SELECT   
    IS_OBJECT(true),   
    IS_OBJECT(1),  
    IS_OBJECT("value"),   
    IS_OBJECT(null),  
    IS_OBJECT({prop: "value"}),   
    IS_OBJECT([1, 2, 3]),  
    IS_OBJECT({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="288ad-922">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-922">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <span data-ttu-id="288ad-923"><a name="bk_is_primitive"></a>IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="288ad-923"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span></span>  
 <span data-ttu-id="288ad-924">Retourneert een Booleaanse waarde die aangeeft of het type van de opgegeven expressie is van een primitief (string, Boolean, numerieke of null).</span><span class="sxs-lookup"><span data-stu-id="288ad-924">Returns a Boolean value indicating if the type of the specified expression is a primitive (string, Boolean, numeric or null).</span></span>  
  
 <span data-ttu-id="288ad-925">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-925">**Syntax**</span></span>  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 <span data-ttu-id="288ad-926">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-926">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="288ad-927">Is geldige expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-927">Is any valid expression.</span></span>  
  
 <span data-ttu-id="288ad-928">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-928">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-929">Retourneert een Booleaanse expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-929">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="288ad-930">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-930">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-931">Het volgende voorbeeld controleert objecten van JSON Boolean, getal, string, null, object, matrix en niet-gedefinieerde typen met de functie IS_PRIMITIVE.</span><span class="sxs-lookup"><span data-stu-id="288ad-931">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_PRIMITIVE function.</span></span>  
  
```  
SELECT   
           IS_PRIMITIVE(true),   
           IS_PRIMITIVE(1),  
           IS_PRIMITIVE("value"),   
           IS_PRIMITIVE(null),  
           IS_PRIMITIVE({prop: "value"}),   
           IS_PRIMITIVE([1, 2, 3]),  
           IS_PRIMITIVE({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="288ad-932">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-932">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <span data-ttu-id="288ad-933"><a name="bk_is_string"></a>IS_STRING</span><span class="sxs-lookup"><span data-stu-id="288ad-933"><a name="bk_is_string"></a> IS_STRING</span></span>  
 <span data-ttu-id="288ad-934">Retourneert een Booleaanse waarde die aangeeft of het type van de opgegeven expressie een tekenreeks is.</span><span class="sxs-lookup"><span data-stu-id="288ad-934">Returns a Boolean value indicating if the type of the specified expression is a string.</span></span>  
  
 <span data-ttu-id="288ad-935">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-935">**Syntax**</span></span>  
  
```  
IS_STRING(<expression>)  
```  
  
 <span data-ttu-id="288ad-936">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-936">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="288ad-937">Is geldige expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-937">Is any valid expression.</span></span>  
  
 <span data-ttu-id="288ad-938">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-938">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-939">Retourneert een Booleaanse expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-939">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="288ad-940">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-940">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-941">Het volgende voorbeeld controleert objecten van JSON Boolean, getal, string, null, object, matrix en niet-gedefinieerde typen met de functie IS_STRING.</span><span class="sxs-lookup"><span data-stu-id="288ad-941">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_STRING function.</span></span>  
  
```  
SELECT   
       IS_STRING(true),   
       IS_STRING(1),  
       IS_STRING("value"),   
       IS_STRING(null),  
       IS_STRING({prop: "value"}),   
       IS_STRING([1, 2, 3]),  
       IS_STRING({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="288ad-942">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-942">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <span data-ttu-id="288ad-943"><a name="bk_string_functions"></a>Tekenreeks-functies</span><span class="sxs-lookup"><span data-stu-id="288ad-943"><a name="bk_string_functions"></a> String functions</span></span>  
 <span data-ttu-id="288ad-944">De volgende scalaire functies een bewerking uitvoeren op een tekenreekswaarde van de invoer en een tekenreeks, numerieke of Booleaanse waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="288ad-944">The following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="288ad-945">CONCAT</span><span class="sxs-lookup"><span data-stu-id="288ad-945">CONCAT</span></span>](#bk_concat)|[<span data-ttu-id="288ad-946">BEVAT</span><span class="sxs-lookup"><span data-stu-id="288ad-946">CONTAINS</span></span>](#bk_contains)|[<span data-ttu-id="288ad-947">ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="288ad-947">ENDSWITH</span></span>](#bk_endswith)|  
|[<span data-ttu-id="288ad-948">INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="288ad-948">INDEX_OF</span></span>](#bk_index_of)|[<span data-ttu-id="288ad-949">LINKS</span><span class="sxs-lookup"><span data-stu-id="288ad-949">LEFT</span></span>](#bk_left)|[<span data-ttu-id="288ad-950">LENGTE</span><span class="sxs-lookup"><span data-stu-id="288ad-950">LENGTH</span></span>](#bk_length)|  
|[<span data-ttu-id="288ad-951">LAGERE</span><span class="sxs-lookup"><span data-stu-id="288ad-951">LOWER</span></span>](#bk_lower)|[<span data-ttu-id="288ad-952">LTRIM</span><span class="sxs-lookup"><span data-stu-id="288ad-952">LTRIM</span></span>](#bk_ltrim)|[<span data-ttu-id="288ad-953">VERVANGEN</span><span class="sxs-lookup"><span data-stu-id="288ad-953">REPLACE</span></span>](#bk_replace)|  
|[<span data-ttu-id="288ad-954">REPLICEREN</span><span class="sxs-lookup"><span data-stu-id="288ad-954">REPLICATE</span></span>](#bk_replicate)|[<span data-ttu-id="288ad-955">OMKEREN</span><span class="sxs-lookup"><span data-stu-id="288ad-955">REVERSE</span></span>](#bk_reverse)|[<span data-ttu-id="288ad-956">RECHTS</span><span class="sxs-lookup"><span data-stu-id="288ad-956">RIGHT</span></span>](#bk_right)|  
|[<span data-ttu-id="288ad-957">RTRIM</span><span class="sxs-lookup"><span data-stu-id="288ad-957">RTRIM</span></span>](#bk_rtrim)|[<span data-ttu-id="288ad-958">STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="288ad-958">STARTSWITH</span></span>](#bk_startswith)|[<span data-ttu-id="288ad-959">DE SUBTEKENREEKS</span><span class="sxs-lookup"><span data-stu-id="288ad-959">SUBSTRING</span></span>](#bk_substring)|  
|[<span data-ttu-id="288ad-960">BOVENSTE</span><span class="sxs-lookup"><span data-stu-id="288ad-960">UPPER</span></span>](#bk_upper)|||  
  
####  <span data-ttu-id="288ad-961"><a name="bk_concat"></a>CONCAT</span><span class="sxs-lookup"><span data-stu-id="288ad-961"><a name="bk_concat"></a> CONCAT</span></span>  
 <span data-ttu-id="288ad-962">Retourneert een tekenreeks die het resultaat van het samenvoegen van twee of meer tekenreekswaarden.</span><span class="sxs-lookup"><span data-stu-id="288ad-962">Returns a string that is the result of concatenating two or more string values.</span></span>  
  
 <span data-ttu-id="288ad-963">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-963">**Syntax**</span></span>  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 <span data-ttu-id="288ad-964">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-964">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="288ad-965">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-965">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="288ad-966">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-966">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-967">Retourneert een tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-967">Returns a string expression.</span></span>  
  
 <span data-ttu-id="288ad-968">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-968">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-969">Het volgende voorbeeld retourneert de samengevoegde tekenreeks van de opgegeven waarden.</span><span class="sxs-lookup"><span data-stu-id="288ad-969">The following example returns the concatenated string of the specified values.</span></span>  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 <span data-ttu-id="288ad-970">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-970">Here is the result set.</span></span>  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <span data-ttu-id="288ad-971"><a name="bk_contains"></a>BEVAT</span><span class="sxs-lookup"><span data-stu-id="288ad-971"><a name="bk_contains"></a> CONTAINS</span></span>  
 <span data-ttu-id="288ad-972">Retourneert een Boolean die aangeeft of de eerste expressie tekenreeks de tweede bevat.</span><span class="sxs-lookup"><span data-stu-id="288ad-972">Returns a Boolean indicating whether the first string expression contains the second.</span></span>  
  
 <span data-ttu-id="288ad-973">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-973">**Syntax**</span></span>  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="288ad-974">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-974">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="288ad-975">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-975">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="288ad-976">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-976">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-977">Retourneert een Booleaanse expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-977">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="288ad-978">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-978">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-979">Het volgende voorbeeld controleert als "abc" bevat "ab" en "d".</span><span class="sxs-lookup"><span data-stu-id="288ad-979">The following example checks if "abc" contains "ab" and contains "d".</span></span>  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 <span data-ttu-id="288ad-980">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-980">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="288ad-981"><a name="bk_endswith"></a>ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="288ad-981"><a name="bk_endswith"></a> ENDSWITH</span></span>  
 <span data-ttu-id="288ad-982">Retourneert een Boolean die aangeeft of de eerste tekenreeksexpressie eindigt op de tweede.</span><span class="sxs-lookup"><span data-stu-id="288ad-982">Returns a Boolean indicating whether the first string expression ends with the second.</span></span>  
  
 <span data-ttu-id="288ad-983">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-983">**Syntax**</span></span>  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="288ad-984">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-984">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="288ad-985">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-985">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="288ad-986">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-986">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-987">Retourneert een Booleaanse expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-987">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="288ad-988">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-988">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-989">Het volgende voorbeeld retourneert dat de "abc" eindigt op "b" en 'bc'.</span><span class="sxs-lookup"><span data-stu-id="288ad-989">The following example returns the "abc" ends with "b" and "bc".</span></span>  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 <span data-ttu-id="288ad-990">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-990">Here is the result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="288ad-991"><a name="bk_index_of"></a>INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="288ad-991"><a name="bk_index_of"></a> INDEX_OF</span></span>  
 <span data-ttu-id="288ad-992">Retourneert de beginpositie van het eerste exemplaar van de tweede tekenreeksexpressie binnen de eerste expressie in de opgegeven tekenreeks is of -1 als de tekenreeks is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="288ad-992">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span>  
  
 <span data-ttu-id="288ad-993">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-993">**Syntax**</span></span>  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="288ad-994">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-994">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="288ad-995">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-995">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="288ad-996">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-996">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-997">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-997">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-998">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-998">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-999">Het volgende voorbeeld wordt de index van verschillende subtekenreeksen binnen "abc".</span><span class="sxs-lookup"><span data-stu-id="288ad-999">The following example returns the index of various substrings inside "abc".</span></span>  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 <span data-ttu-id="288ad-1000">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-1000">Here is the result set.</span></span>  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <span data-ttu-id="288ad-1001"><a name="bk_left"></a>LINKS</span><span class="sxs-lookup"><span data-stu-id="288ad-1001"><a name="bk_left"></a> LEFT</span></span>  
 <span data-ttu-id="288ad-1002">Retourneert het linkergedeelte van een tekenreeks zijn met het opgegeven aantal tekens.</span><span class="sxs-lookup"><span data-stu-id="288ad-1002">Returns the left part of a string with the specified number of characters.</span></span>  
  
 <span data-ttu-id="288ad-1003">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-1003">**Syntax**</span></span>  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="288ad-1004">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-1004">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="288ad-1005">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1005">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="288ad-1006">Is geldige numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1006">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-1007">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-1007">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-1008">Retourneert een tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1008">Returns a string expression.</span></span>  
  
 <span data-ttu-id="288ad-1009">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-1009">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-1010">Het volgende voorbeeld wordt het linkergedeelte van "abc" voor verschillende lengtewaarden.</span><span class="sxs-lookup"><span data-stu-id="288ad-1010">The following example returns the left part of "abc" for various length values.</span></span>  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 <span data-ttu-id="288ad-1011">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-1011">Here is the result set.</span></span>  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <span data-ttu-id="288ad-1012"><a name="bk_length"></a>LENGTE</span><span class="sxs-lookup"><span data-stu-id="288ad-1012"><a name="bk_length"></a> LENGTH</span></span>  
 <span data-ttu-id="288ad-1013">Retourneert het aantal tekens van de opgegeven tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1013">Returns the number of characters of the specified string expression.</span></span>  
  
 <span data-ttu-id="288ad-1014">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-1014">**Syntax**</span></span>  
  
```  
LENGTH(<str_expr>)  
```  
  
 <span data-ttu-id="288ad-1015">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-1015">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="288ad-1016">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1016">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="288ad-1017">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-1017">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-1018">Retourneert een tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1018">Returns a string expression.</span></span>  
  
 <span data-ttu-id="288ad-1019">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-1019">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-1020">Het volgende voorbeeld retourneert de lengte van een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="288ad-1020">The following example returns the length of a string.</span></span>  
  
```  
SELECT LENGTH("abc")  
```  
  
 <span data-ttu-id="288ad-1021">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-1021">Here is the result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="288ad-1022"><a name="bk_lower"></a>LAGERE</span><span class="sxs-lookup"><span data-stu-id="288ad-1022"><a name="bk_lower"></a> LOWER</span></span>  
 <span data-ttu-id="288ad-1023">Retourneert een tekenreeksexpressie na hoofdletter gegevens converteren naar kleine letters.</span><span class="sxs-lookup"><span data-stu-id="288ad-1023">Returns a string expression after converting uppercase character data to lowercase.</span></span>  
  
 <span data-ttu-id="288ad-1024">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-1024">**Syntax**</span></span>  
  
```  
LOWER(<str_expr>)  
```  
  
 <span data-ttu-id="288ad-1025">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-1025">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="288ad-1026">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1026">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="288ad-1027">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-1027">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-1028">Retourneert een tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1028">Returns a string expression.</span></span>  
  
 <span data-ttu-id="288ad-1029">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-1029">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-1030">Het volgende voorbeeld laat zien hoe lager gebruiken in een query.</span><span class="sxs-lookup"><span data-stu-id="288ad-1030">The following example shows how to use LOWER in a query.</span></span>  
  
```  
SELECT LOWER("Abc")  
```  
  
 <span data-ttu-id="288ad-1031">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-1031">Here is the result set.</span></span>  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <span data-ttu-id="288ad-1032"><a name="bk_ltrim"></a>LTRIM</span><span class="sxs-lookup"><span data-stu-id="288ad-1032"><a name="bk_ltrim"></a> LTRIM</span></span>  
 <span data-ttu-id="288ad-1033">Retourneert een tekenreeksexpressie na het verwijderen van toonaangevende lege waarden.</span><span class="sxs-lookup"><span data-stu-id="288ad-1033">Returns a string expression after it removes leading blanks.</span></span>  
  
 <span data-ttu-id="288ad-1034">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-1034">**Syntax**</span></span>  
  
```  
LTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="288ad-1035">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-1035">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="288ad-1036">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1036">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="288ad-1037">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-1037">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-1038">Retourneert een tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1038">Returns a string expression.</span></span>  
  
 <span data-ttu-id="288ad-1039">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-1039">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-1040">Het volgende voorbeeld laat zien hoe LTRIM gebruiken binnen een query.</span><span class="sxs-lookup"><span data-stu-id="288ad-1040">The following example shows how to use LTRIM inside a query.</span></span>  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 <span data-ttu-id="288ad-1041">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-1041">Here is the result set.</span></span>  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <span data-ttu-id="288ad-1042"><a name="bk_replace"></a>VERVANGEN</span><span class="sxs-lookup"><span data-stu-id="288ad-1042"><a name="bk_replace"></a> REPLACE</span></span>  
 <span data-ttu-id="288ad-1043">Vervangt alle instanties van een opgegeven string-waarde met de waarde van een andere tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="288ad-1043">Replaces all occurrences of a specified string value with another string value.</span></span>  
  
 <span data-ttu-id="288ad-1044">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-1044">**Syntax**</span></span>  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="288ad-1045">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-1045">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="288ad-1046">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1046">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="288ad-1047">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-1047">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-1048">Retourneert een tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1048">Returns a string expression.</span></span>  
  
 <span data-ttu-id="288ad-1049">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-1049">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-1050">Het volgende voorbeeld ziet hoe u vervangen in een query.</span><span class="sxs-lookup"><span data-stu-id="288ad-1050">The following example shows how to use REPLACE in a query.</span></span>  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 <span data-ttu-id="288ad-1051">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-1051">Here is the result set.</span></span>  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <span data-ttu-id="288ad-1052"><a name="bk_replicate"></a>REPLICEREN</span><span class="sxs-lookup"><span data-stu-id="288ad-1052"><a name="bk_replicate"></a> REPLICATE</span></span>  
 <span data-ttu-id="288ad-1053">Herhaalt een string-waarde van een opgegeven aantal keren.</span><span class="sxs-lookup"><span data-stu-id="288ad-1053">Repeats a string value a specified number of times.</span></span>  
  
 <span data-ttu-id="288ad-1054">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-1054">**Syntax**</span></span>  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="288ad-1055">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-1055">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="288ad-1056">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1056">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="288ad-1057">Is geldige numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1057">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-1058">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-1058">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-1059">Retourneert een tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1059">Returns a string expression.</span></span>  
  
 <span data-ttu-id="288ad-1060">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-1060">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-1061">Het volgende voorbeeld ziet hoe u REPLICEREN in een query.</span><span class="sxs-lookup"><span data-stu-id="288ad-1061">The following example shows how to use REPLICATE in a query.</span></span>  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 <span data-ttu-id="288ad-1062">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-1062">Here is the result set.</span></span>  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <span data-ttu-id="288ad-1063"><a name="bk_reverse"></a>OMKEREN</span><span class="sxs-lookup"><span data-stu-id="288ad-1063"><a name="bk_reverse"></a> REVERSE</span></span>  
 <span data-ttu-id="288ad-1064">Retourneert de omgekeerde volgorde van een string-waarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-1064">Returns the reverse order of a string value.</span></span>  
  
 <span data-ttu-id="288ad-1065">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-1065">**Syntax**</span></span>  
  
```  
REVERSE(<str_expr>)  
```  
  
 <span data-ttu-id="288ad-1066">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-1066">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="288ad-1067">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1067">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="288ad-1068">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-1068">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-1069">Retourneert een tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1069">Returns a string expression.</span></span>  
  
 <span data-ttu-id="288ad-1070">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-1070">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-1071">Het volgende voorbeeld laat zien hoe REVERSE gebruiken in een query.</span><span class="sxs-lookup"><span data-stu-id="288ad-1071">The following example shows how to use REVERSE in a query.</span></span>  
  
```  
SELECT REVERSE("Abc")  
```  
  
 <span data-ttu-id="288ad-1072">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-1072">Here is the result set.</span></span>  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <span data-ttu-id="288ad-1073"><a name="bk_right"></a>RECHTS</span><span class="sxs-lookup"><span data-stu-id="288ad-1073"><a name="bk_right"></a> RIGHT</span></span>  
 <span data-ttu-id="288ad-1074">Retourneert de juiste deel van een tekenreeks zijn met het opgegeven aantal tekens.</span><span class="sxs-lookup"><span data-stu-id="288ad-1074">Returns the right part of a string with the specified number of characters.</span></span>  
  
 <span data-ttu-id="288ad-1075">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-1075">**Syntax**</span></span>  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="288ad-1076">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-1076">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="288ad-1077">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1077">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="288ad-1078">Is geldige numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1078">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-1079">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-1079">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-1080">Retourneert een tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1080">Returns a string expression.</span></span>  
  
 <span data-ttu-id="288ad-1081">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-1081">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-1082">Het volgende voorbeeld wordt het rechterdeel van "abc" voor verschillende lengtewaarden.</span><span class="sxs-lookup"><span data-stu-id="288ad-1082">The following example returns the right part of "abc" for various length values.</span></span>  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 <span data-ttu-id="288ad-1083">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-1083">Here is the result set.</span></span>  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <span data-ttu-id="288ad-1084"><a name="bk_rtrim"></a>RTRIM</span><span class="sxs-lookup"><span data-stu-id="288ad-1084"><a name="bk_rtrim"></a> RTRIM</span></span>  
 <span data-ttu-id="288ad-1085">Retourneert een tekenreeksexpressie na het afsluitende spaties verwijderen.</span><span class="sxs-lookup"><span data-stu-id="288ad-1085">Returns a string expression after it removes trailing blanks.</span></span>  
  
 <span data-ttu-id="288ad-1086">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-1086">**Syntax**</span></span>  
  
```  
RTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="288ad-1087">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-1087">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="288ad-1088">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1088">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="288ad-1089">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-1089">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-1090">Retourneert een tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1090">Returns a string expression.</span></span>  
  
 <span data-ttu-id="288ad-1091">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-1091">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-1092">Het volgende voorbeeld laat zien hoe RTRIM gebruiken binnen een query.</span><span class="sxs-lookup"><span data-stu-id="288ad-1092">The following example shows how to use RTRIM inside a query.</span></span>  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 <span data-ttu-id="288ad-1093">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-1093">Here is the result set.</span></span>  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <span data-ttu-id="288ad-1094"><a name="bk_startswith"></a>STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="288ad-1094"><a name="bk_startswith"></a> STARTSWITH</span></span>  
 <span data-ttu-id="288ad-1095">Retourneert een Boolean die aangeeft of de eerste expressie tekenreeks begint met het tweede.</span><span class="sxs-lookup"><span data-stu-id="288ad-1095">Returns a Boolean indicating whether the first string expression starts with the second.</span></span>  
  
 <span data-ttu-id="288ad-1096">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-1096">**Syntax**</span></span>  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="288ad-1097">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-1097">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="288ad-1098">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1098">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="288ad-1099">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-1099">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-1100">Retourneert een Booleaanse expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1100">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="288ad-1101">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-1101">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-1102">Het volgende voorbeeld wordt gecontroleerd of de tekenreeks "abc" met "b begint" en "a".</span><span class="sxs-lookup"><span data-stu-id="288ad-1102">The following example checks if the string "abc" begins with "b" and "a".</span></span>  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 <span data-ttu-id="288ad-1103">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-1103">Here is the result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="288ad-1104"><a name="bk_substring"></a>DE SUBTEKENREEKS</span><span class="sxs-lookup"><span data-stu-id="288ad-1104"><a name="bk_substring"></a> SUBSTRING</span></span>  
 <span data-ttu-id="288ad-1105">Retourneert deel van een tekenreeksexpressie die beginnen bij de op nul gebaseerde positie opgegeven teken en blijft de opgegeven lengte of het einde van de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="288ad-1105">Returns part of a string expression starting at the specified character zero-based position and continues to the specified length, or to the end of the string.</span></span>  
  
 <span data-ttu-id="288ad-1106">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-1106">**Syntax**</span></span>  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="288ad-1107">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-1107">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="288ad-1108">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1108">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="288ad-1109">Is geldige numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1109">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-1110">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-1110">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-1111">Retourneert een tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1111">Returns a string expression.</span></span>  
  
 <span data-ttu-id="288ad-1112">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-1112">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-1113">Het volgende voorbeeld retourneert de subtekenreeks van "abc" beginnen bij 1 en voor een lengte van 1 teken.</span><span class="sxs-lookup"><span data-stu-id="288ad-1113">The following example returns the substring of "abc" starting at 1 and for a length of 1 character.</span></span>  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 <span data-ttu-id="288ad-1114">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-1114">Here is the result set.</span></span>  
  
```  
[{"$1": "b"}]  
```  
  
####  <span data-ttu-id="288ad-1115"><a name="bk_upper"></a>BOVENSTE</span><span class="sxs-lookup"><span data-stu-id="288ad-1115"><a name="bk_upper"></a> UPPER</span></span>  
 <span data-ttu-id="288ad-1116">Retourneert een tekenreeksexpressie na kleine letter gegevens converteren naar hoofdletters.</span><span class="sxs-lookup"><span data-stu-id="288ad-1116">Returns a string expression after converting lowercase character data to uppercase.</span></span>  
  
 <span data-ttu-id="288ad-1117">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-1117">**Syntax**</span></span>  
  
```  
UPPER(<str_expr>)  
```  
  
 <span data-ttu-id="288ad-1118">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-1118">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="288ad-1119">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1119">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="288ad-1120">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-1120">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-1121">Retourneert een tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1121">Returns a string expression.</span></span>  
  
 <span data-ttu-id="288ad-1122">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-1122">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-1123">Het volgende voorbeeld ziet het gebruik van hoofdletters in een query</span><span class="sxs-lookup"><span data-stu-id="288ad-1123">The following example shows how to use UPPER in a query</span></span>  
  
```  
SELECT UPPER("Abc")  
```  
  
 <span data-ttu-id="288ad-1124">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-1124">Here is the result set.</span></span>  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <span data-ttu-id="288ad-1125"><a name="bk_array_functions"></a>Matrixfuncties</span><span class="sxs-lookup"><span data-stu-id="288ad-1125"><a name="bk_array_functions"></a> Array functions</span></span>  
 <span data-ttu-id="288ad-1126">De volgende scalaire functies uitvoeren van een bewerking op een matrix invoerwaarde en retourneren numerieke, Booleaanse waarde of een matrix van waarde</span><span class="sxs-lookup"><span data-stu-id="288ad-1126">The following scalar functions perform an operation on an array input value and return numeric, Boolean or array value</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="288ad-1127">ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="288ad-1127">ARRAY_CONCAT</span></span>](#bk_array_concat)|[<span data-ttu-id="288ad-1128">ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="288ad-1128">ARRAY_CONTAINS</span></span>](#bk_array_contains)|[<span data-ttu-id="288ad-1129">ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="288ad-1129">ARRAY_LENGTH</span></span>](#bk_array_length)|  
|[<span data-ttu-id="288ad-1130">ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="288ad-1130">ARRAY_SLICE</span></span>](#bk_array_slice)|||  
  
####  <span data-ttu-id="288ad-1131"><a name="bk_array_concat"></a>ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="288ad-1131"><a name="bk_array_concat"></a> ARRAY_CONCAT</span></span>  
 <span data-ttu-id="288ad-1132">Retourneert een matrix die het resultaat van het samenvoegen van twee of meer matrixwaarden.</span><span class="sxs-lookup"><span data-stu-id="288ad-1132">Returns an array that is the result of concatenating two or more array values.</span></span>  
  
 <span data-ttu-id="288ad-1133">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-1133">**Syntax**</span></span>  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 <span data-ttu-id="288ad-1134">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-1134">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="288ad-1135">Is geldige matrixexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1135">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="288ad-1136">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-1136">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-1137">Retourneert een matrixexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1137">Returns an array expression.</span></span>  
  
 <span data-ttu-id="288ad-1138">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-1138">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-1139">Het volgende voorbeeld hoe u voor het samenvoegen van twee matrices.</span><span class="sxs-lookup"><span data-stu-id="288ad-1139">The following example how to concatenate two arrays.</span></span>  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 <span data-ttu-id="288ad-1140">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-1140">Here is the result set.</span></span>  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <span data-ttu-id="288ad-1141"><a name="bk_array_contains"></a>ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="288ad-1141"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span></span>  
 <span data-ttu-id="288ad-1142">Retourneert een Booleaanse waarde die aangeeft of de matrix bevat met de opgegeven waarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-1142">Returns a Boolean indicating whether the array contains the specified value.</span></span>  
  
 <span data-ttu-id="288ad-1143">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-1143">**Syntax**</span></span>  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 <span data-ttu-id="288ad-1144">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-1144">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="288ad-1145">Is geldige matrixexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1145">Is any valid array expression.</span></span>  
  
-   `expr`  
  
     <span data-ttu-id="288ad-1146">Is geldige expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1146">Is any valid expression.</span></span>  
  
 <span data-ttu-id="288ad-1147">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-1147">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-1148">Retourneert een Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-1148">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="288ad-1149">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-1149">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-1150">Het volgende voorbeeld voor het lidmaatschap van een matrix met ARRAY_CONTAINS controleren.</span><span class="sxs-lookup"><span data-stu-id="288ad-1150">The following example how to check for membership in an array using ARRAY_CONTAINS.</span></span>  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 <span data-ttu-id="288ad-1151">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-1151">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="288ad-1152"><a name="bk_array_length"></a>ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="288ad-1152"><a name="bk_array_length"></a> ARRAY_LENGTH</span></span>  
 <span data-ttu-id="288ad-1153">Retourneert het aantal elementen van de opgegeven matrix-expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1153">Returns the number of elements of the specified array expression.</span></span>  
  
 <span data-ttu-id="288ad-1154">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-1154">**Syntax**</span></span>  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 <span data-ttu-id="288ad-1155">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-1155">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="288ad-1156">Is geldige matrixexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1156">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="288ad-1157">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-1157">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-1158">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1158">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-1159">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-1159">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-1160">Het volgende voorbeeld de lengte van een matrix met ARRAY_LENGTH krijgen.</span><span class="sxs-lookup"><span data-stu-id="288ad-1160">The following example how to get the length of an array using ARRAY_LENGTH.</span></span>  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 <span data-ttu-id="288ad-1161">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-1161">Here is the result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="288ad-1162"><a name="bk_array_slice"></a>ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="288ad-1162"><a name="bk_array_slice"></a> ARRAY_SLICE</span></span>  
 <span data-ttu-id="288ad-1163">Retourneert deel van een matrixexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1163">Returns part of an array expression.</span></span>
  
 <span data-ttu-id="288ad-1164">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-1164">**Syntax**</span></span>  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="288ad-1165">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-1165">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="288ad-1166">Is geldige matrixexpressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1166">Is any valid array expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="288ad-1167">Is geldige numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1167">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="288ad-1168">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-1168">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-1169">Retourneert een Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-1169">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="288ad-1170">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-1170">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-1171">Het volgende voorbeeld het ophalen van een deel van een matrix met ARRAY_SLICE.</span><span class="sxs-lookup"><span data-stu-id="288ad-1171">The following example how to get a part of an array using ARRAY_SLICE.</span></span>  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 <span data-ttu-id="288ad-1172">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-1172">Here is the result set.</span></span>  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <span data-ttu-id="288ad-1173"><a name="bk_spatial_functions"></a>Ruimtelijke functies</span><span class="sxs-lookup"><span data-stu-id="288ad-1173"><a name="bk_spatial_functions"></a> Spatial functions</span></span>  
 <span data-ttu-id="288ad-1174">De volgende scalaire functies een bewerking uitvoeren op een invoerwaarde ruimtelijke object en een numeriek gegevenstype of Booleaanse waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="288ad-1174">The following scalar functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="288ad-1175">ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="288ad-1175">ST_DISTANCE</span></span>](#bk_st_distance)|[<span data-ttu-id="288ad-1176">ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="288ad-1176">ST_WITHIN</span></span>](#bk_st_within)|[<span data-ttu-id="288ad-1177">ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="288ad-1177">ST_INTERSECTS</span></span>](#bk_st_intersects)|[<span data-ttu-id="288ad-1178">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="288ad-1178">ST_ISVALID</span></span>](#bk_st_isvalid)|  
|[<span data-ttu-id="288ad-1179">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="288ad-1179">ST_ISVALIDDETAILED</span></span>](#bk_st_isvaliddetailed)|||  
  
####  <span data-ttu-id="288ad-1180"><a name="bk_st_distance"></a>ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="288ad-1180"><a name="bk_st_distance"></a> ST_DISTANCE</span></span>  
 <span data-ttu-id="288ad-1181">Retourneert de afstand tussen de twee GeoJSON punt, Polygon of LineString expressies.</span><span class="sxs-lookup"><span data-stu-id="288ad-1181">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span>  
  
 <span data-ttu-id="288ad-1182">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-1182">**Syntax**</span></span>  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="288ad-1183">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-1183">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="288ad-1184">Is geldige expressie voor GeoJSON punt, Polygon of LineString-object.</span><span class="sxs-lookup"><span data-stu-id="288ad-1184">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="288ad-1185">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-1185">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-1186">Retourneert een numerieke expressie met de afstand.</span><span class="sxs-lookup"><span data-stu-id="288ad-1186">Returns a numeric expression containing the distance.</span></span> <span data-ttu-id="288ad-1187">Dit wordt uitgedrukt in meters voor de verwijzing van het systeem.</span><span class="sxs-lookup"><span data-stu-id="288ad-1187">This is expressed in meters for the default reference system.</span></span>  
  
 <span data-ttu-id="288ad-1188">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-1188">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-1189">Het volgende voorbeeld laat zien hoe alle familie documenten die binnen 30 km van de opgegeven locatie met de ingebouwde functie ST_DISTANCE retourneren.</span><span class="sxs-lookup"><span data-stu-id="288ad-1189">The following example shows how to return all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> <span data-ttu-id="288ad-1190">.</span><span class="sxs-lookup"><span data-stu-id="288ad-1190">.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 <span data-ttu-id="288ad-1191">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-1191">Here is the result set.</span></span>  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <span data-ttu-id="288ad-1192"><a name="bk_st_within"></a>ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="288ad-1192"><a name="bk_st_within"></a> ST_WITHIN</span></span>  
 <span data-ttu-id="288ad-1193">Retourneert een Booleaanse expressie die aangeeft of het GeoJSON-object opgegeven in het eerste argument (punt, Polygon of LineString) binnen het GeoJSON (punt, Polygon of LineString) in het tweede argument.</span><span class="sxs-lookup"><span data-stu-id="288ad-1193">Returns a Boolean expression indicating whether the GeoJSON object (Point, Polygon, or LineString) specified in the first argument is within the GeoJSON (Point, Polygon, or LineString) in the second argument.</span></span>  
  
 <span data-ttu-id="288ad-1194">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-1194">**Syntax**</span></span>  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="288ad-1195">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-1195">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="288ad-1196">Is geldige expressie voor GeoJSON punt, Polygon of LineString-object.</span><span class="sxs-lookup"><span data-stu-id="288ad-1196">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="288ad-1197">Is geldige expressie voor GeoJSON punt, Polygon of LineString-object.</span><span class="sxs-lookup"><span data-stu-id="288ad-1197">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="288ad-1198">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-1198">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-1199">Retourneert een Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-1199">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="288ad-1200">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-1200">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-1201">Het volgende voorbeeld laat zien hoe alle familie documenten binnen een veelhoek met ST_WITHIN vinden.</span><span class="sxs-lookup"><span data-stu-id="288ad-1201">The following example shows how to find all family documents within a polygon using ST_WITHIN.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="288ad-1202">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-1202">Here is the result set.</span></span>  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <span data-ttu-id="288ad-1203"><a name="bk_st_intersects"></a>ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="288ad-1203"><a name="bk_st_intersects"></a> ST_INTERSECTS</span></span>  
 <span data-ttu-id="288ad-1204">Retourneert een Booleaanse expressie die aangeeft of het GeoJSON-object opgegeven in het eerste argument (punt, Polygon of LineString) in de polygoonring GeoJSON (punt, Polygon of LineString) in het tweede argument.</span><span class="sxs-lookup"><span data-stu-id="288ad-1204">Returns a Boolean expression indicating whether the GeoJSON object (Point, Polygon, or LineString) specified in the first argument intersects the GeoJSON (Point, Polygon, or LineString) in the second argument.</span></span>  
  
 <span data-ttu-id="288ad-1205">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-1205">**Syntax**</span></span>  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="288ad-1206">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-1206">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="288ad-1207">Is geldige expressie voor GeoJSON punt, Polygon of LineString-object.</span><span class="sxs-lookup"><span data-stu-id="288ad-1207">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="288ad-1208">Is geldige expressie voor GeoJSON punt, Polygon of LineString-object.</span><span class="sxs-lookup"><span data-stu-id="288ad-1208">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="288ad-1209">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-1209">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-1210">Retourneert een Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-1210">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="288ad-1211">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-1211">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-1212">Het volgende voorbeeld laat zien hoe vinden alle gebieden die in de polygoonring met de opgegeven veelhoek.</span><span class="sxs-lookup"><span data-stu-id="288ad-1212">The following example shows how to find all areas that intersects with the given polygon.</span></span>  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="288ad-1213">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-1213">Here is the result set.</span></span>  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <span data-ttu-id="288ad-1214"><a name="bk_st_isvalid"></a>ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="288ad-1214"><a name="bk_st_isvalid"></a> ST_ISVALID</span></span>  
 <span data-ttu-id="288ad-1215">Retourneert een Booleaanse waarde die aangeeft of de opgegeven expressie voor GeoJSON punt, Polygon of LineString ongeldig is.</span><span class="sxs-lookup"><span data-stu-id="288ad-1215">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span>  
  
 <span data-ttu-id="288ad-1216">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-1216">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="288ad-1217">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-1217">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="288ad-1218">Is geldige GeoJSON punt, Polygon of LineString-expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1218">Is any valid GeoJSON Point, Polygon, or LineString expression.</span></span>  
  
 <span data-ttu-id="288ad-1219">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-1219">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-1220">Retourneert een Booleaanse expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1220">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="288ad-1221">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-1221">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-1222">Het volgende voorbeeld laat zien hoe controleren of een punt ST_VALID geldig is.</span><span class="sxs-lookup"><span data-stu-id="288ad-1222">The following example shows how to check if a point is valid using ST_VALID.</span></span>  
  
 <span data-ttu-id="288ad-1223">Dit punt heeft bijvoorbeeld een Breedtegraadwaarde die niet in het geldige waardenbereik [-90, 90], dus de query retourneert false.</span><span class="sxs-lookup"><span data-stu-id="288ad-1223">For example, this point has a latitude value that's not in the valid range of values [-90, 90], so the query returns false.</span></span>  
  
 <span data-ttu-id="288ad-1224">Voor multilinestring vereist de specificatie GeoJSON dat de opgegeven combinatie van laatste coördinaat moet hetzelfde zijn als de eerste pagina, voor het maken van een gesloten vorm.</span><span class="sxs-lookup"><span data-stu-id="288ad-1224">For polygons, the GeoJSON specification requires that the last coordinate pair provided should be the same as the first, to create a closed shape.</span></span> <span data-ttu-id="288ad-1225">Punten in een polygoon moeten worden opgegeven in rechtsom volgorde.</span><span class="sxs-lookup"><span data-stu-id="288ad-1225">Points within a polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="288ad-1226">Een polygoon die is opgegeven in rechtsom volgorde vertegenwoordigt de inverse van de regio binnen deze.</span><span class="sxs-lookup"><span data-stu-id="288ad-1226">A polygon specified in clockwise order represents the inverse of the region within it.</span></span>  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 <span data-ttu-id="288ad-1227">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-1227">Here is the result set.</span></span>  
  
```  
[{ "$1": false }]  
```  
  
####  <span data-ttu-id="288ad-1228"><a name="bk_st_isvaliddetailed"></a>ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="288ad-1228"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span></span>  
 <span data-ttu-id="288ad-1229">Retourneert een JSON-waarde met een Booleaanse waarde als de opgegeven expressie voor GeoJSON punt, Polygon of LineString is geldig, en als ongeldig, ook de reden als een string-waarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-1229">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span>  
  
 <span data-ttu-id="288ad-1230">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="288ad-1230">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="288ad-1231">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="288ad-1231">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="288ad-1232">Is geldige GeoJSON-punt of de veelhoek expressie.</span><span class="sxs-lookup"><span data-stu-id="288ad-1232">Is any valid GeoJSON point or polygon expression.</span></span>  
  
 <span data-ttu-id="288ad-1233">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="288ad-1233">**Return Types**</span></span>  
  
 <span data-ttu-id="288ad-1234">Retourneert een JSON-waarde met een Booleaanse waarde als de opgegeven GeoJSON-punt of de veelhoek expressie is geldig, en als ongeldig, ook de reden als een string-waarde.</span><span class="sxs-lookup"><span data-stu-id="288ad-1234">Returns a JSON value containing a Boolean value if the specified GeoJSON point or polygon expression is valid, and if invalid, additionally the reason as a string value.</span></span>  
  
 <span data-ttu-id="288ad-1235">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="288ad-1235">**Examples**</span></span>  
  
 <span data-ttu-id="288ad-1236">Het volgende voorbeeld geldigheid (met details) met behulp van ST_ISVALIDDETAILED controleren.</span><span class="sxs-lookup"><span data-stu-id="288ad-1236">The following example how to check validity (with details) using ST_ISVALIDDETAILED.</span></span>  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 <span data-ttu-id="288ad-1237">Hier volgt de resultatenset.</span><span class="sxs-lookup"><span data-stu-id="288ad-1237">Here is the result set.</span></span>  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "The Polygon input is not valid because the start and end points of the ring number 1 are not the same. Each ring of a polygon must have the same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a><span data-ttu-id="288ad-1238">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="288ad-1238">Next steps</span></span>  
 <span data-ttu-id="288ad-1239">[SQL-syntaxis en SQL-query voor Azure Cosmos-DB](documentdb-sql-query.md) </span><span class="sxs-lookup"><span data-stu-id="288ad-1239">[SQL syntax and SQL query for Azure Cosmos DB](documentdb-sql-query.md) </span></span>  
 [<span data-ttu-id="288ad-1240">Azure DB Cosmos-documentatie</span><span class="sxs-lookup"><span data-stu-id="288ad-1240">Azure Cosmos DB documentation</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
