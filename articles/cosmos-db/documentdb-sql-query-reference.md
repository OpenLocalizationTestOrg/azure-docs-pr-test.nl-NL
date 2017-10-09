---
<span data-ttu-id="c1b02-101">titel: aaa "Azure Cosmos DB DocumentDB-API: SQL-syntaxis | Microsoft Docs' Beschrijving: verwijzen naar de documentatie voor hello Azure Cosmos DB DocumentDB API SQL-querytaal.</span><span class="sxs-lookup"><span data-stu-id="c1b02-101">title: aaa"Azure Cosmos DB DocumentDB API: SQL syntax | Microsoft Docs" description: Reference documentation for hello Azure Cosmos DB DocumentDB API SQL query language.</span></span>
<span data-ttu-id="c1b02-102">Services: cosmos-db auteur: mimig1 manager: jhubbard-editor: mimig documentationcenter: ''</span><span class="sxs-lookup"><span data-stu-id="c1b02-102">services: cosmos-db author: mimig1 manager: jhubbard editor: mimig documentationcenter: ''</span></span>

<span data-ttu-id="c1b02-103">MS.AssetID: ms.service: cosmos-db ms.workload: data services ms.tgt_pltfrm: na ms.devlang: n.v.t. ms.topic: verwijzen naar ms.date: 13-06/2017 ms.author: mimig</span><span class="sxs-lookup"><span data-stu-id="c1b02-103">ms.assetid: ms.service: cosmos-db ms.workload: data-services ms.tgt_pltfrm: na ms.devlang: na ms.topic: reference ms.date: 06/13/2017 ms.author: mimig</span></span>

---

# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a><span data-ttu-id="c1b02-104">Azure DB Cosmos DocumentDB API: Verwijzing naar SQL</span><span class="sxs-lookup"><span data-stu-id="c1b02-104">Azure Cosmos DB DocumentDB API: SQL syntax reference</span></span>

<span data-ttu-id="c1b02-105">Hello Azure Cosmos DB DocumentDB API ondersteunt documentquery's die gebruikmaken van een bekende SQL (Structured Query Language) zoals grammatica via hiërarchische JSON-documenten zonder expliciet schema of het maken van secundaire indexen.</span><span class="sxs-lookup"><span data-stu-id="c1b02-105">hello Azure Cosmos DB DocumentDB API supports querying documents using a familiar SQL (Structured Query Language) like grammar over hierarchical JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> <span data-ttu-id="c1b02-106">Dit onderwerp bevat de naslagdocumentatie voor Hallo DocumentDB API SQL-querytaal.</span><span class="sxs-lookup"><span data-stu-id="c1b02-106">This topic provides reference documentation for hello DocumentDB API SQL query language.</span></span>

<span data-ttu-id="c1b02-107">Zie voor een overzicht van Hallo DocumentDB API SQL-querytaal [SQL-query's voor Azure Cosmos DB DocumentDB API](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="c1b02-107">For a walkthrough of hello DocumentDB API SQL query language, see [SQL queries for Azure Cosmos DB DocumentDB API](documentdb-sql-query.md).</span></span>  
  
<span data-ttu-id="c1b02-108">We ook nodigen u toovisit hello [Query Playground](http://www.documentdb.com/sql/demo) kunt u proberen Azure Cosmos DB en SQL-query's uitvoeren op onze gegevensset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-108">We also invite you toovisit hello [Query Playground](http://www.documentdb.com/sql/demo) where you can try Azure Cosmos DB and run SQL queries against our dataset.</span></span>  
  
## <a name="select-query"></a><span data-ttu-id="c1b02-109">SELECT-query</span><span class="sxs-lookup"><span data-stu-id="c1b02-109">SELECT query</span></span>  
<span data-ttu-id="c1b02-110">Haalt de JSON-documenten uit Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="c1b02-110">Retrieves JSON documents from hello database.</span></span> <span data-ttu-id="c1b02-111">Ondersteunt de evaluatie van de expressie, projecties, filteren en lid wordt.</span><span class="sxs-lookup"><span data-stu-id="c1b02-111">Supports expression evaluation, projections, filtering and joins.</span></span>  <span data-ttu-id="c1b02-112">Hallo syntaxis conventies sectie geeft een tabelindeling van Hallo conventies voor het beschrijven van Hallo SELECT-instructies.</span><span class="sxs-lookup"><span data-stu-id="c1b02-112">hello conventions used for describing hello SELECT statements are tabulated in hello Syntax conventions section.</span></span>  
  
<span data-ttu-id="c1b02-113">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-113">**Syntax**</span></span>  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 <span data-ttu-id="c1b02-114">**Opmerkingen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-114">**Remarks**</span></span>  
  
 <span data-ttu-id="c1b02-115">Zie de volgende secties voor meer informatie op elke component:</span><span class="sxs-lookup"><span data-stu-id="c1b02-115">See following sections for details on each clause:</span></span>  
  
-   [<span data-ttu-id="c1b02-116">SELECT-component</span><span class="sxs-lookup"><span data-stu-id="c1b02-116">SELECT clause</span></span>](#bk_select_query)  
  
-   [<span data-ttu-id="c1b02-117">FROM-component</span><span class="sxs-lookup"><span data-stu-id="c1b02-117">FROM clause</span></span>](#bk_from_clause)  
  
-   [<span data-ttu-id="c1b02-118">WHERE-component</span><span class="sxs-lookup"><span data-stu-id="c1b02-118">WHERE clause</span></span>](#bk_where_clause)  
  
-   [<span data-ttu-id="c1b02-119">ORDER BY-component</span><span class="sxs-lookup"><span data-stu-id="c1b02-119">ORDER BY clause</span></span>](#bk_orderby_clause)  
  
<span data-ttu-id="c1b02-120">Hallo-componenten in Hallo SELECT-instructie moeten worden besteld, zoals hierboven.</span><span class="sxs-lookup"><span data-stu-id="c1b02-120">hello clauses in hello SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="c1b02-121">Een van de optionele componenten Hallo kan worden weggelaten.</span><span class="sxs-lookup"><span data-stu-id="c1b02-121">Any one of hello optional clauses can be omitted.</span></span> <span data-ttu-id="c1b02-122">Maar als optionele componenten worden gebruikt, moeten ze worden weergegeven in de juiste volgorde Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1b02-122">But when optional clauses are used, they must appear in hello right order.</span></span>  
  
<span data-ttu-id="c1b02-123">**Logische verwerkingsvolgorde Hallo SELECT-instructie**</span><span class="sxs-lookup"><span data-stu-id="c1b02-123">**Logical Processing Order of hello SELECT statement**</span></span>  
  
<span data-ttu-id="c1b02-124">Hallo in welke volgorde componenten zijn verwerkt is:</span><span class="sxs-lookup"><span data-stu-id="c1b02-124">hello order in which clauses are processed is:</span></span>  

1.  [<span data-ttu-id="c1b02-125">FROM-component</span><span class="sxs-lookup"><span data-stu-id="c1b02-125">FROM clause</span></span>](#bk_from_clause)  
2.  [<span data-ttu-id="c1b02-126">WHERE-component</span><span class="sxs-lookup"><span data-stu-id="c1b02-126">WHERE clause</span></span>](#bk_where_clause)  
3.  [<span data-ttu-id="c1b02-127">ORDER BY-component</span><span class="sxs-lookup"><span data-stu-id="c1b02-127">ORDER BY clause</span></span>](#bk_orderby_clause)  
4.  [<span data-ttu-id="c1b02-128">SELECT-component</span><span class="sxs-lookup"><span data-stu-id="c1b02-128">SELECT clause</span></span>](#bk_select_query)  

<span data-ttu-id="c1b02-129">Houd er rekening mee dat dit verschilt van Hallo volgorde waarin ze worden weergegeven in het Hallo-syntaxis.</span><span class="sxs-lookup"><span data-stu-id="c1b02-129">Note that this is different from hello order in which they appear in hello syntax.</span></span> <span data-ttu-id="c1b02-130">Hallo ordening is dat alle nieuwe symbolen die zijn geïntroduceerd in een component verwerkte zichtbaar zijn en kunnen worden gebruikt in de componenten die later wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="c1b02-130">hello ordering is such that all new symbols introduced by a processed clause are visible and can be used in clauses processed later.</span></span> <span data-ttu-id="c1b02-131">Bijvoorbeeld, aliassen die zijn gedeclareerd in een FROM-component in, waarbij toegankelijk zijn en SELECT-component.</span><span class="sxs-lookup"><span data-stu-id="c1b02-131">For instance, aliases declared in a FROM clause are accessible in WHERE and SELECT clauses.</span></span>  

<span data-ttu-id="c1b02-132">**Spaties en -opmerkingen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-132">**Whitespace characters and comments**</span></span>  

<span data-ttu-id="c1b02-133">Alle spatietekens die deel uitmaken van een tekenreeks tussen aanhalingstekens of aanhalingstekens id maken geen deel uit van Hallo taal grammatica en worden genegeerd tijdens het parseren.</span><span class="sxs-lookup"><span data-stu-id="c1b02-133">All white space characters which are not part of a quoted string or quoted identifier are not part of hello language grammar and are ignored during parsing.</span></span>  

<span data-ttu-id="c1b02-134">Hallo-querytaal biedt ondersteuning voor T-SQL-stijl opmerkingen zoals</span><span class="sxs-lookup"><span data-stu-id="c1b02-134">hello query language supports T-SQL style comments like</span></span>  

-   <span data-ttu-id="c1b02-135">SQL-instructie`-- comment text [newline]`</span><span class="sxs-lookup"><span data-stu-id="c1b02-135">SQL Statement `-- comment text [newline]`</span></span>  

<span data-ttu-id="c1b02-136">Terwijl uit witruimte bestaat en -opmerkingen niet alle significante in grammatica hello zijn, moeten ze gebruikte tooseparate tokens zijn.</span><span class="sxs-lookup"><span data-stu-id="c1b02-136">While whitespace characters and comments do not have any significance in hello grammar, they must be used tooseparate tokens.</span></span> <span data-ttu-id="c1b02-137">Bijvoorbeeld: `-1e5` is één nummer token, even`: – 1 e5` wordt een min token gevolgd door nummer 1 en id e5.</span><span class="sxs-lookup"><span data-stu-id="c1b02-137">For instance: `-1e5` is a single number token, while`: – 1 e5` is a minus token followed by number 1 and identifier e5.</span></span>  

##  <span data-ttu-id="c1b02-138"><a name="bk_select_query"></a>SELECT-component</span><span class="sxs-lookup"><span data-stu-id="c1b02-138"><a name="bk_select_query"></a> SELECT clause</span></span>  
<span data-ttu-id="c1b02-139">Hallo-componenten in Hallo SELECT-instructie moeten worden besteld, zoals hierboven.</span><span class="sxs-lookup"><span data-stu-id="c1b02-139">hello clauses in hello SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="c1b02-140">Een van de optionele componenten Hallo kan worden weggelaten.</span><span class="sxs-lookup"><span data-stu-id="c1b02-140">Any one of hello optional clauses can be omitted.</span></span> <span data-ttu-id="c1b02-141">Maar als optionele componenten worden gebruikt, moeten ze worden weergegeven in de juiste volgorde Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1b02-141">But when optional clauses are used, they must appear in hello right order.</span></span>  

<span data-ttu-id="c1b02-142">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-142">**Syntax**</span></span>  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 <span data-ttu-id="c1b02-143">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-143">**Arguments**</span></span>  
  
 `<select_specification>`  
  
 <span data-ttu-id="c1b02-144">Eigenschappen of waarde toobe geselecteerd voor Hallo resultaat ingesteld.</span><span class="sxs-lookup"><span data-stu-id="c1b02-144">Properties or value toobe selected for hello result set.</span></span>  
  
 `'*'`  
  
<span data-ttu-id="c1b02-145">Hiermee geeft u op dat Hallo waarde zonder wijzigingen moet worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="c1b02-145">Specifies that hello value should be retrieved without making any changes.</span></span> <span data-ttu-id="c1b02-146">Specifiek als Hallo verwerkt waarde een object is, worden alle eigenschappen worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="c1b02-146">Specifically if hello processed value is an object, all properties will be retrieved.</span></span>  
  
 `<object_property_list>`  
  
<span data-ttu-id="c1b02-147">Hiermee geeft lijst op Hallo van eigenschappen toobe opgehaald.</span><span class="sxs-lookup"><span data-stu-id="c1b02-147">Specifies hello list of properties toobe retrieved.</span></span> <span data-ttu-id="c1b02-148">Elke geretourneerde waarde is een object met Hallo eigenschappen opgegeven.</span><span class="sxs-lookup"><span data-stu-id="c1b02-148">Each returned value will be an object with hello properties specified.</span></span>  
  
`VALUE`  
  
<span data-ttu-id="c1b02-149">Hiermee geeft u op dat Hallo JSON-waarde moet worden opgehaald in plaats van Hallo voltooid JSON-object.</span><span class="sxs-lookup"><span data-stu-id="c1b02-149">Specifies that hello JSON value should be retrieved instead of hello complete JSON object.</span></span> <span data-ttu-id="c1b02-150">Dit, in tegenstelling tot `<property_list>` loopt Hallo geprojecteerd waarde niet in een object.</span><span class="sxs-lookup"><span data-stu-id="c1b02-150">This, unlike `<property_list>` does not wrap hello projected value in an object.</span></span>  
  
`<scalar_expression>`  
  
<span data-ttu-id="c1b02-151">Expressie die aangeeft Hallo waarde toobe berekend.</span><span class="sxs-lookup"><span data-stu-id="c1b02-151">Expression representing hello value toobe computed.</span></span> <span data-ttu-id="c1b02-152">Zie [scalaire expressies](#bk_scalar_expressions) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-152">See [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
<span data-ttu-id="c1b02-153">**Opmerkingen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-153">**Remarks**</span></span>  
  
<span data-ttu-id="c1b02-154">Hallo `SELECT *` syntaxis is alleen geldig als FROM-component precies één alias is gedeclareerd.</span><span class="sxs-lookup"><span data-stu-id="c1b02-154">hello `SELECT *` syntax is only valid if FROM clause has declared exactly one alias.</span></span> <span data-ttu-id="c1b02-155">`SELECT *`biedt een identity-projectie handig is als er geen projectie is vereist.</span><span class="sxs-lookup"><span data-stu-id="c1b02-155">`SELECT *` provides an identity projection, which can be useful if no projection is needed.</span></span> <span data-ttu-id="c1b02-156">Selecteer * is alleen geldig als FROM-component is opgegeven en er slechts één invoer bron geïntroduceerd.</span><span class="sxs-lookup"><span data-stu-id="c1b02-156">SELECT * is only valid if FROM clause is specified and introduced only a single input source.</span></span>  
  
<span data-ttu-id="c1b02-157">Houd er rekening mee dat `SELECT <select_list>` en `SELECT *` 'syntactische suiker' zijn en u kunt ook kan worden uitgedrukt met behulp van eenvoudige SELECT-instructies zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c1b02-157">Note that `SELECT <select_list>` and `SELECT *` are "syntactic sugar" and can be alternatively expressed by using simple SELECT statements as shown below.</span></span>  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     <span data-ttu-id="c1b02-158">is gelijk aan:</span><span class="sxs-lookup"><span data-stu-id="c1b02-158">is equivalent to:</span></span>  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     <span data-ttu-id="c1b02-159">is gelijk aan:</span><span class="sxs-lookup"><span data-stu-id="c1b02-159">is equivalent to:</span></span>  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
<span data-ttu-id="c1b02-160">**Zie ook**</span><span class="sxs-lookup"><span data-stu-id="c1b02-160">**See Also**</span></span>  
  
[<span data-ttu-id="c1b02-161">Scalaire expressies</span><span class="sxs-lookup"><span data-stu-id="c1b02-161">Scalar expressions</span></span>](#bk_scalar_expressions)  
[<span data-ttu-id="c1b02-162">SELECT-component</span><span class="sxs-lookup"><span data-stu-id="c1b02-162">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="c1b02-163"><a name="bk_from_clause"></a>FROM-component</span><span class="sxs-lookup"><span data-stu-id="c1b02-163"><a name="bk_from_clause"></a> FROM clause</span></span>  
<span data-ttu-id="c1b02-164">Hiermee geeft u op Hallo bron of gekoppelde bronnen.</span><span class="sxs-lookup"><span data-stu-id="c1b02-164">Specifies hello source or joined sources.</span></span> <span data-ttu-id="c1b02-165">Hallo FROM-component is optioneel.</span><span class="sxs-lookup"><span data-stu-id="c1b02-165">hello FROM clause is optional.</span></span> <span data-ttu-id="c1b02-166">Als dat niet wordt opgegeven, andere componenten nog steeds uitgevoerd alsof FROM-component opgegeven één document.</span><span class="sxs-lookup"><span data-stu-id="c1b02-166">If not specified, other clauses will still be executed as if FROM clause provided a single document.</span></span>  
  
<span data-ttu-id="c1b02-167">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-167">**Syntax**</span></span>  
  
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
  
<span data-ttu-id="c1b02-168">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-168">**Arguments**</span></span>  
  
`<from_source>`  
  
<span data-ttu-id="c1b02-169">Hiermee geeft u een gegevensbron met of zonder een alias.</span><span class="sxs-lookup"><span data-stu-id="c1b02-169">Specifies a data source, with or without an alias.</span></span> <span data-ttu-id="c1b02-170">Als alias niet opgegeven is, wordt deze worden afgeleid van Hallo `<collection_expression>` met volgende regels:</span><span class="sxs-lookup"><span data-stu-id="c1b02-170">If alias is not specified, it will be inferred from hello `<collection_expression>` using following rules:</span></span>  
  
-   <span data-ttu-id="c1b02-171">Hallo-expressie is een verzamelingnaam, wordt verzamelingnaam worden gebruikt als een alias.</span><span class="sxs-lookup"><span data-stu-id="c1b02-171">If hello expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
-   <span data-ttu-id="c1b02-172">Als de expressie Hallo `<collection_expression>`, en vervolgens kubuskenmerkbinding en vervolgens kubuskenmerkbinding wordt gebruikt als alias.</span><span class="sxs-lookup"><span data-stu-id="c1b02-172">If hello expression is `<collection_expression>`, then property_name, then property_name will be used as an alias.</span></span> <span data-ttu-id="c1b02-173">Hallo-expressie is een verzamelingnaam, wordt verzamelingnaam worden gebruikt als een alias.</span><span class="sxs-lookup"><span data-stu-id="c1b02-173">If hello expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
<span data-ttu-id="c1b02-174">ALS IN DE`input_alias`</span><span class="sxs-lookup"><span data-stu-id="c1b02-174">AS `input_alias`</span></span>  
  
<span data-ttu-id="c1b02-175">Hiermee geeft u op dat Hallo `input_alias` is een set met waarden geretourneerd door Hallo onderliggende verzamelingsexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-175">Specifies that hello `input_alias` is a set of values returned by hello underlying collection expression.</span></span>  
 
<span data-ttu-id="c1b02-176">`input_alias`IN</span><span class="sxs-lookup"><span data-stu-id="c1b02-176">`input_alias` IN</span></span>  
  
<span data-ttu-id="c1b02-177">Hiermee geeft u op dat Hallo `input_alias` Hallo verzameling waarden die zijn verkregen door iteratie van alle matrixelementen van elke matrix geretourneerd door de onderliggende verzamelingsexpressie Hallo moet vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="c1b02-177">Specifies that hello `input_alias` should represent hello set of values obtained by iterating over all array elements of each array returned by hello underlying collection expression.</span></span> <span data-ttu-id="c1b02-178">Een waarde die is geretourneerd door de onderliggende verzamelingsexpressie is geen matrix wordt genegeerd.</span><span class="sxs-lookup"><span data-stu-id="c1b02-178">Any value returned by underlying collection expression that is not an array is ignored.</span></span>  
  
`<collection_expression>`  
  
<span data-ttu-id="c1b02-179">Hiermee geeft u op Hallo verzameling expressie toobe gebruikte tooretrieve Hallo documenten.</span><span class="sxs-lookup"><span data-stu-id="c1b02-179">Specifies hello collection expression toobe used tooretrieve hello documents.</span></span>  
  
`ROOT`  
  
<span data-ttu-id="c1b02-180">Hiermee geeft u op dat document uit de momenteel verbonden verzameling Hallo standaard moet worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="c1b02-180">Specifies that document should be retrieved from hello default, currently connected collection.</span></span>  
  
`collection_name`  
  
<span data-ttu-id="c1b02-181">Hiermee geeft u op dat document moet worden opgehaald uit de verzameling Hallo opgegeven.</span><span class="sxs-lookup"><span data-stu-id="c1b02-181">Specifies that document should be retrieved from hello provided collection.</span></span> <span data-ttu-id="c1b02-182">Hallo-naam van verzameling op Hallo moet overeenkomen met de Hallo-naam van verzameling op Hallo momenteel verbonden.</span><span class="sxs-lookup"><span data-stu-id="c1b02-182">hello name of hello collection must match hello name of hello collection currently connected to.</span></span>  
  
`input_alias`  
  
<span data-ttu-id="c1b02-183">Geeft aan dat document moet worden opgehaald uit Hallo andere bron gedefinieerd door Hallo opgegeven alias.</span><span class="sxs-lookup"><span data-stu-id="c1b02-183">Specifies that document should be retrieved from hello other source defined by hello provided alias.</span></span>  
  
`<collection_expression> '.' property_`  
  
<span data-ttu-id="c1b02-184">Geeft aan dat document moet worden opgehaald door het openen van Hallo `property_name` eigenschap of matrixindex matrixelement voor alle documenten die worden opgehaald door opgegeven verzamelingsexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-184">Specifies that document should be retrieved by accessing hello `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
<span data-ttu-id="c1b02-185">Geeft aan dat document moet worden opgehaald door het openen van Hallo `property_name` eigenschap of matrixindex matrixelement voor alle documenten die worden opgehaald door opgegeven verzamelingsexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-185">Specifies that document should be retrieved by accessing hello `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
<span data-ttu-id="c1b02-186">**Opmerkingen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-186">**Remarks**</span></span>  
  
<span data-ttu-id="c1b02-187">Alle aliassen verstrekt of afgeleid in Hallo `<from_source>(`s) moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="c1b02-187">All aliases provided or inferred in hello `<from_source>(`s) must be unique.</span></span> <span data-ttu-id="c1b02-188">Hallo syntaxis `<collection_expression>.`kubuskenmerkbinding is gelijk aan Hallo `<collection_expression>' ['"property_name"']'`.</span><span class="sxs-lookup"><span data-stu-id="c1b02-188">hello Syntax `<collection_expression>.`property_name is hello same as `<collection_expression>' ['"property_name"']'`.</span></span> <span data-ttu-id="c1b02-189">Hallo laatstgenoemde syntaxis kan echter worden gebruikt als een eigenschapsnaam een niet-id-tekens bevat.</span><span class="sxs-lookup"><span data-stu-id="c1b02-189">However, hello latter syntax can be used if a property name contains a non-identifier characters.</span></span>  
  
<span data-ttu-id="c1b02-190">**Ontbrekende eigenschappen, ontbrekende matrixelementen, niet-gedefinieerde waarden verwerken**</span><span class="sxs-lookup"><span data-stu-id="c1b02-190">**Missing properties, missing array elements, undefined values handling**</span></span>  
  
<span data-ttu-id="c1b02-191">Als een verzamelingsexpressie voor een naar eigenschappen of matrixelementen en waarde niet bestaat, wordt die waarde genegeerd en niet verder worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="c1b02-191">If a collection expression accesses properties or array elements and that value does not exist, that value will be ignored and not processed further.</span></span>  
  
<span data-ttu-id="c1b02-192">**Verzameling expressie context scoping**</span><span class="sxs-lookup"><span data-stu-id="c1b02-192">**Collection expression context scoping**</span></span>  
  
<span data-ttu-id="c1b02-193">Een verzamelingsexpressie is mogelijk binnen het bereik van verzameling of binnen het bereik van document:</span><span class="sxs-lookup"><span data-stu-id="c1b02-193">A collection expression may be collection-scoped or document-scoped:</span></span>  
  
-   <span data-ttu-id="c1b02-194">Een expressie is gericht op de verzameling, als hello onderliggende gegevensbron Hallo verzamelingsexpressie beide ROOT of `collection_name`.</span><span class="sxs-lookup"><span data-stu-id="c1b02-194">An expression is collection-scoped, if hello underlying source of hello collection expression is either ROOT or `collection_name`.</span></span> <span data-ttu-id="c1b02-195">Een dergelijke expressie vertegenwoordigt een verzameling van documenten die zijn opgehaald uit de verzameling Hallo rechtstreeks en is niet afhankelijk van het Hallo-verwerking van andere expressies verzameling.</span><span class="sxs-lookup"><span data-stu-id="c1b02-195">Such an expression represents a set of documents retrieved from hello collection directly, and is not dependent on hello processing of other collection expressions.</span></span>  
  
-   <span data-ttu-id="c1b02-196">Een expressie is binnen het bereik van document, als hello onderliggende gegevensbron Hallo verzamelingsexpressie `input_alias` geïntroduceerd eerder in het Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="c1b02-196">An expression is document-scoped, if hello underlying source of hello collection expression is `input_alias` introduced earlier in hello query.</span></span> <span data-ttu-id="c1b02-197">Een dergelijke expressie vertegenwoordigt een verzameling van documenten die zijn verkregen door het evalueren van Hallo verzamelingsexpressie in Hallo bereik van elk document die behoren toohello set Hallo alias verzameling gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="c1b02-197">Such an expression represents a set of documents obtained by evaluating hello collection expression in hello scope of each document belonging toohello set associated with hello aliased collection.</span></span>  <span data-ttu-id="c1b02-198">de resulterende set Hallo worden een samenvoeging van die worden verkregen door Hallo verzamelingsexpressie voor elke Hallo documenten in Hallo onderliggende set te evalueren.</span><span class="sxs-lookup"><span data-stu-id="c1b02-198">hello resulting set will be a union of sets obtained by evaluating hello collection expression for each of hello documents in hello underlying set.</span></span>  
  
<span data-ttu-id="c1b02-199">**Joins**</span><span class="sxs-lookup"><span data-stu-id="c1b02-199">**Joins**</span></span>  
  
<span data-ttu-id="c1b02-200">In de huidige release Hallo ondersteunt Azure Cosmos DB inner joins.</span><span class="sxs-lookup"><span data-stu-id="c1b02-200">In hello current release, Azure Cosmos DB supports inner joins.</span></span> <span data-ttu-id="c1b02-201">Er zijn extra join mechanismen toekomstige.</span><span class="sxs-lookup"><span data-stu-id="c1b02-201">Additional join capabilities are forthcoming.</span></span>

<span data-ttu-id="c1b02-202">Inner join in een volledige vectorproduct Hallo resultatensets die deel uitmaken van Hallo join.</span><span class="sxs-lookup"><span data-stu-id="c1b02-202">Inner joins result in a complete cross product of hello sets participating in hello join.</span></span> <span data-ttu-id="c1b02-203">Hallo-resultaat van een join N manier is een set met tuples zijn N-element, waarbij elke waarde in het Hallo-tuple is gekoppeld aan het Hallo-alias instellen die deel Hallo join en toegankelijk zijn voor het verwijzen naar deze alias in andere componenten.</span><span class="sxs-lookup"><span data-stu-id="c1b02-203">hello result of an N-way join is a set of N-element tuples, where each value in hello tuple is associated with hello aliased set participating in hello join and can be accessed by referencing that alias in other clauses.</span></span>  
  
<span data-ttu-id="c1b02-204">Hallo-evaluatie van Hallo join, is afhankelijk van Hallo context bereik van Hallo deelnemende sets:</span><span class="sxs-lookup"><span data-stu-id="c1b02-204">hello evaluation of hello join depends on hello context scope of hello participating sets:</span></span>  
  
-  <span data-ttu-id="c1b02-205">Een join tussen verzamelingsset A en gericht op de verzameling ingesteld B, resulteert in een vectorproduct van alle elementen in sets A en B.</span><span class="sxs-lookup"><span data-stu-id="c1b02-205">A join between collection-set A and collection-scoped set B, results in a cross product of all elements in sets A and B.</span></span>
  
-   <span data-ttu-id="c1b02-206">Een koppeling tussen het paar A en binnen het bereik van document set B, resulteert in een samenvoeging van alle sets die zijn verkregen door het evalueren van binnen het bereik van document set B voor elk document van A. instellen</span><span class="sxs-lookup"><span data-stu-id="c1b02-206">A join between set A and document-scoped set B, results in a union of all sets obtained by evaluating document-scoped set B for each document from set A.</span></span>  
  
 <span data-ttu-id="c1b02-207">In de huidige release Hallo wordt maximaal één expressie gericht op de verzameling ondersteund door de queryprocessor Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1b02-207">In hello current release, a maximum of one collection-scoped expression is supported by hello query processor.</span></span>  
  
<span data-ttu-id="c1b02-208">**Voorbeelden van joins:**</span><span class="sxs-lookup"><span data-stu-id="c1b02-208">**Examples of joins:**</span></span>  
  
<span data-ttu-id="c1b02-209">Bekijk hello FROM-component te volgen:`<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span><span class="sxs-lookup"><span data-stu-id="c1b02-209">Let's look at hello following FROM clause: `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span></span>  
  
 <span data-ttu-id="c1b02-210">Elke bron definiëren, kunnen `input_alias1, input_alias2, …, input_aliasN`.</span><span class="sxs-lookup"><span data-stu-id="c1b02-210">Let each source define `input_alias1, input_alias2, …, input_aliasN`.</span></span> <span data-ttu-id="c1b02-211">Deze component FROM retourneert een set met N-tuples (tuple met N waarden).</span><span class="sxs-lookup"><span data-stu-id="c1b02-211">This FROM clause returns a set of N-tuples (tuple with N values).</span></span> <span data-ttu-id="c1b02-212">Elke tuple heeft geproduceerd door alle verzameling aliassen iteratie van hun respectieve sets waarden.</span><span class="sxs-lookup"><span data-stu-id="c1b02-212">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span>  
  
<span data-ttu-id="c1b02-213">*Voorbeeld 1, met 2 bronnen JOIN:*</span><span class="sxs-lookup"><span data-stu-id="c1b02-213">*JOIN example 1, with 2 sources:*</span></span>  
  
- <span data-ttu-id="c1b02-214">Laat `<from_source1>` verzameling bereik en de set {A, B, C} vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="c1b02-214">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="c1b02-215">Laat `<from_source2>` worden document binnen het bereik van verwijzende input_alias1 en vertegenwoordigen sets:</span><span class="sxs-lookup"><span data-stu-id="c1b02-215">Let `<from_source2>` be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="c1b02-216">{1, 2} voor`input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="c1b02-216">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="c1b02-217">{3} voor`input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="c1b02-217">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="c1b02-218">{4, 5} voor`input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="c1b02-218">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="c1b02-219">Hallo FROM-component `<from_source1> JOIN <from_source2>` leidt ertoe dat Hallo tuples te volgen:</span><span class="sxs-lookup"><span data-stu-id="c1b02-219">hello FROM clause `<from_source1> JOIN <from_source2>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="c1b02-220">(`input_alias1, input_alias2`):</span><span class="sxs-lookup"><span data-stu-id="c1b02-220">(`input_alias1, input_alias2`):</span></span>  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
<span data-ttu-id="c1b02-221">*Voorbeeld 2, met 3 bronnen JOIN:*</span><span class="sxs-lookup"><span data-stu-id="c1b02-221">*JOIN example 2, with 3 sources:*</span></span>  
  
- <span data-ttu-id="c1b02-222">Laat `<from_source1>` verzameling bereik en de set {A, B, C} vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="c1b02-222">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="c1b02-223">Laat `<from_source2>` worden binnen het bereik van document verwijzen naar `input_alias1` sets omvatten:</span><span class="sxs-lookup"><span data-stu-id="c1b02-223">Let `<from_source2>` be document-scoped referencing `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="c1b02-224">{1, 2} voor`input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="c1b02-224">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="c1b02-225">{3} voor`input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="c1b02-225">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="c1b02-226">{4, 5} voor`input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="c1b02-226">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="c1b02-227">Laat `<from_source3>` worden binnen het bereik van document verwijzen naar `input_alias2` sets omvatten:</span><span class="sxs-lookup"><span data-stu-id="c1b02-227">Let `<from_source3>` be document-scoped referencing `input_alias2` and represent sets:</span></span>  
  
    <span data-ttu-id="c1b02-228">{100, 200} voor`input_alias2 = 1,`</span><span class="sxs-lookup"><span data-stu-id="c1b02-228">{100, 200} for `input_alias2 = 1,`</span></span>  
  
    <span data-ttu-id="c1b02-229">{300} voor`input_alias2 = 3,`</span><span class="sxs-lookup"><span data-stu-id="c1b02-229">{300} for `input_alias2 = 3,`</span></span>  
  
- <span data-ttu-id="c1b02-230">Hallo FROM-component `<from_source1> JOIN <from_source2> JOIN <from_source3>` leidt ertoe dat Hallo tuples te volgen:</span><span class="sxs-lookup"><span data-stu-id="c1b02-230">hello FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="c1b02-231">(input_alias1, input_alias2, input_alias3):</span><span class="sxs-lookup"><span data-stu-id="c1b02-231">(input_alias1, input_alias2, input_alias3):</span></span>  
  
    <span data-ttu-id="c1b02-232">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span><span class="sxs-lookup"><span data-stu-id="c1b02-232">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="c1b02-233">Gebrek aan tuples voor andere waarden van `input_alias1`, `input_alias2`, voor welke Hallo `<from_source3>` heeft geen waarden retourneren.</span><span class="sxs-lookup"><span data-stu-id="c1b02-233">Lack of tuples for other values of `input_alias1`, `input_alias2`, for which hello `<from_source3>` did not return any values.</span></span>  
  
<span data-ttu-id="c1b02-234">*Voorbeeld 3, met 3 bronnen JOIN:*</span><span class="sxs-lookup"><span data-stu-id="c1b02-234">*JOIN example 3, with 3 sources:*</span></span>  
  
- <span data-ttu-id="c1b02-235">Laat < from_source1 > worden gericht op de verzameling en vertegenwoordigen set {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="c1b02-235">Let <from_source1> be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="c1b02-236">Laat `<from_source1>` verzameling bereik en de set {A, B, C} vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="c1b02-236">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="c1b02-237">< From_source2 > verwijzende input_alias1 binnen het bereik van document zijn en stelt vertegenwoordigen, kunnen:</span><span class="sxs-lookup"><span data-stu-id="c1b02-237">Let <from_source2> be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="c1b02-238">{1, 2} voor`input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="c1b02-238">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="c1b02-239">{3} voor`input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="c1b02-239">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="c1b02-240">{4, 5} voor`input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="c1b02-240">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="c1b02-241">Laat `<from_source3>` moet binnen het bereik te`input_alias1` sets omvatten:</span><span class="sxs-lookup"><span data-stu-id="c1b02-241">Let `<from_source3>` be scoped too`input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="c1b02-242">{100, 200} voor`input_alias2 = A,`</span><span class="sxs-lookup"><span data-stu-id="c1b02-242">{100, 200} for `input_alias2 = A,`</span></span>  
  
    <span data-ttu-id="c1b02-243">{300} voor`input_alias2 = C,`</span><span class="sxs-lookup"><span data-stu-id="c1b02-243">{300} for `input_alias2 = C,`</span></span>  
  
- <span data-ttu-id="c1b02-244">Hallo FROM-component `<from_source1> JOIN <from_source2> JOIN <from_source3>` leidt ertoe dat Hallo tuples te volgen:</span><span class="sxs-lookup"><span data-stu-id="c1b02-244">hello FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="c1b02-245">(`input_alias1, input_alias2, input_alias3`):</span><span class="sxs-lookup"><span data-stu-id="c1b02-245">(`input_alias1, input_alias2, input_alias3`):</span></span>  
  
    <span data-ttu-id="c1b02-246">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200), C, 4, 300, (C, 5, 300)</span><span class="sxs-lookup"><span data-stu-id="c1b02-246">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="c1b02-247">Dit resulteerde in vectorproduct tussen `<from_source2>` en `<from_source3>` omdat beide bereik toohello dezelfde `<from_source1>`.</span><span class="sxs-lookup"><span data-stu-id="c1b02-247">This resulted in cross product between `<from_source2>` and `<from_source3>` because both are scoped toohello same `<from_source1>`.</span></span>  <span data-ttu-id="c1b02-248">Dit resulteerde in 4 (2 x 2) tuples met waarde A, 0 tuples met waarde B (1 x 0) en 2 (2 x 1) tuples met waarde C.</span><span class="sxs-lookup"><span data-stu-id="c1b02-248">This resulted in 4 (2x2) tuples having value A, 0 tuples having value B (1x0) and 2 (2x1) tuples having value C.</span></span>  
  
<span data-ttu-id="c1b02-249">**Zie ook**</span><span class="sxs-lookup"><span data-stu-id="c1b02-249">**See also**</span></span>  
  
 [<span data-ttu-id="c1b02-250">SELECT-component</span><span class="sxs-lookup"><span data-stu-id="c1b02-250">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="c1b02-251"><a name="bk_where_clause"></a>WHERE-component</span><span class="sxs-lookup"><span data-stu-id="c1b02-251"><a name="bk_where_clause"></a> WHERE clause</span></span>  
 <span data-ttu-id="c1b02-252">Hiermee geeft u Hallo zoekcriterium voor Hallo documenten die worden geretourneerd door Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="c1b02-252">Specifies hello search condition for hello documents returned by hello query.</span></span>  
  
 <span data-ttu-id="c1b02-253">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-253">**Syntax**</span></span>  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 <span data-ttu-id="c1b02-254">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-254">**Arguments**</span></span>  
  
-   `<filter_condition>`  
  
     <span data-ttu-id="c1b02-255">Hiermee geeft u Hallo voorwaarde toobe voldaan voor Hallo documenten toobe geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="c1b02-255">Specifies hello condition toobe met for hello documents toobe returned.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="c1b02-256">Expressie die aangeeft Hallo waarde toobe berekend.</span><span class="sxs-lookup"><span data-stu-id="c1b02-256">Expression representing hello value toobe computed.</span></span> <span data-ttu-id="c1b02-257">Zie Hallo [scalaire expressies](#bk_scalar_expressions) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-257">See hello [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
 <span data-ttu-id="c1b02-258">**Opmerkingen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-258">**Remarks**</span></span>  
  
 <span data-ttu-id="c1b02-259">Opdat Hallo geretourneerd document toobe een expressie die is opgegeven als filtervoorwaarde tootrue moet worden geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="c1b02-259">In order for hello document toobe returned an expression specified as filter condition must evaluate tootrue.</span></span> <span data-ttu-id="c1b02-260">Alleen Booleaanse waarde true voldoen aan Hallo voorwaarde, een andere waarde: niet-gedefinieerde, null, false, getal, matrix of Object niet voldoen aan Hallo voorwaarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-260">Only Boolean value true will satisfy hello condition, any other value: undefined, null, false, Number, Array or Object will not satisfy hello condition.</span></span>  
  
##  <span data-ttu-id="c1b02-261"><a name="bk_orderby_clause"></a>ORDER BY-component</span><span class="sxs-lookup"><span data-stu-id="c1b02-261"><a name="bk_orderby_clause"></a> ORDER BY clause</span></span>  
 <span data-ttu-id="c1b02-262">Hiermee geeft u Hallo sorteervolgorde voor de resultaten van Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="c1b02-262">Specifies hello sorting order for results returned by hello query.</span></span>  
  
 <span data-ttu-id="c1b02-263">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-263">**Syntax**</span></span>  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 <span data-ttu-id="c1b02-264">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-264">**Arguments**</span></span>  
  
-   `<sort_specification>`  
  
     <span data-ttu-id="c1b02-265">Hiermee geeft u een eigenschap of een expressie waarop toosort Hallo queryresultaatset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-265">Specifies a property or expression on which toosort hello query result set.</span></span> <span data-ttu-id="c1b02-266">Een kolom sorteren kan worden opgegeven als een alias voor een naam of kolom.</span><span class="sxs-lookup"><span data-stu-id="c1b02-266">A sort column can be specified as a name or column alias.</span></span>  
  
     <span data-ttu-id="c1b02-267">Meerdere sortering-kolommen kunnen worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="c1b02-267">Multiple sort columns can be specified.</span></span> <span data-ttu-id="c1b02-268">Kolomnamen moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="c1b02-268">Column names must be unique.</span></span> <span data-ttu-id="c1b02-269">Hallo Hallo sorteren kolommen in component ORDER BY Hallo reeks definieert Hallo organisatie van de resultaatset Hallo gesorteerd.</span><span class="sxs-lookup"><span data-stu-id="c1b02-269">hello sequence of hello sort columns in hello ORDER BY clause defines hello organization of hello sorted result set.</span></span> <span data-ttu-id="c1b02-270">Dat wil zeggen, Hallo resultatenset is gesorteerd op de eerste eigenschap Hallo en vervolgens die geordende lijst is gesorteerd op de tweede eigenschap hello, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="c1b02-270">That is, hello result set is sorted by hello first property and then that ordered list is sorted by hello second property, and so on.</span></span>  
  
     <span data-ttu-id="c1b02-271">Hallo kolomnamen waarnaar wordt verwezen in de component ORDER BY Hallo moeten overeenkomen met een kolom in Hallo lijst of tooa kolom gedefinieerd in een tabel die is opgegeven in de FROM-component Hallo zonder eventuele dubbelzinnigheden selecteren tooeither.</span><span class="sxs-lookup"><span data-stu-id="c1b02-271">hello column names referenced in hello ORDER BY clause must correspond tooeither a column in hello select list or tooa column defined in a table specified in hello FROM clause without any ambiguities.</span></span>  
  
-   `<sort_expression>`  
  
     <span data-ttu-id="c1b02-272">Hiermee geeft u een één eigenschap of een expressie op welke queryresultaatset Hallo toosort.</span><span class="sxs-lookup"><span data-stu-id="c1b02-272">Specifies a single property or expression on which toosort hello query result set.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="c1b02-273">Zie Hallo [scalaire expressies](#bk_scalar_expressions) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-273">See hello [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
-   `ASC | DESC`  
  
     <span data-ttu-id="c1b02-274">Hiermee geeft u op dat Hallo waarden in de opgegeven kolom Hallo in oplopende of aflopende volgorde moeten worden gesorteerd.</span><span class="sxs-lookup"><span data-stu-id="c1b02-274">Specifies that hello values in hello specified column should be sorted in ascending or descending order.</span></span> <span data-ttu-id="c1b02-275">ASC sorteert van Hallo laagste waarde toohighest waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-275">ASC sorts from hello lowest value toohighest value.</span></span> <span data-ttu-id="c1b02-276">DESC sorteren van hoogste waarde toolowest waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-276">DESC sorts from highest value toolowest value.</span></span> <span data-ttu-id="c1b02-277">ASC is Hallo standaardsorteervolgorde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-277">ASC is hello default sort order.</span></span> <span data-ttu-id="c1b02-278">Null-waarden worden behandeld als Hallo laagst mogelijke waarden.</span><span class="sxs-lookup"><span data-stu-id="c1b02-278">Null values are treated as hello lowest possible values.</span></span>  
  
 <span data-ttu-id="c1b02-279">**Opmerkingen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-279">**Remarks**</span></span>  
  
 <span data-ttu-id="c1b02-280">Tijdens het Hallo-querygrammatica ondersteunt meerdere volgorde door eigenschappen, ondersteunt hello Azure Cosmos DB query runtime alleen tegen één eigenschap, en alleen eigenschapnamen, dat wil zeggen, niet op berekende eigenschappen sorteren.</span><span class="sxs-lookup"><span data-stu-id="c1b02-280">While hello query grammar supports multiple order by properties, hello Azure Cosmos DB query runtime supports sorting only against a single property, and only against property names, i.e., not against computed properties.</span></span> <span data-ttu-id="c1b02-281">Sorteren is ook vereist dat Hallo indexeren beleid bevat een bereikindex voor de eigenschap Hallo en Hallo opgegeven type, met Hallo maximumprecisie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-281">Sorting also requires that hello indexing policy includes a range index for hello property and hello specified type, with hello maximum precision.</span></span> <span data-ttu-id="c1b02-282">Raadpleeg toohello indexeren beleid-documentatie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-282">Refer toohello indexing policy documentation for more details.</span></span>  
  
##  <span data-ttu-id="c1b02-283"><a name="bk_scalar_expressions"></a>Scalaire expressies</span><span class="sxs-lookup"><span data-stu-id="c1b02-283"><a name="bk_scalar_expressions"></a> Scalar expressions</span></span>  
 <span data-ttu-id="c1b02-284">Een scalaire expressie die is een combinatie van symbolen en operators die kunnen worden geëvalueerd tooobtain één waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-284">A scalar expression is a combination of symbols and operators that can be evaluated tooobtain a single value.</span></span> <span data-ttu-id="c1b02-285">Eenvoudige expressies kunnen bestaan constanten, eigenschap verwijzingen, matrix element verwijzingen, alias-verwijzingen of functieaanroepen.</span><span class="sxs-lookup"><span data-stu-id="c1b02-285">Simple expressions can be constants, property references, array element references, alias references, or function calls.</span></span> <span data-ttu-id="c1b02-286">Eenvoudige expressies kunnen worden gecombineerd tot complexe expressies met operators.</span><span class="sxs-lookup"><span data-stu-id="c1b02-286">Simple expressions can be combined into complex expressions using operators.</span></span>  
  
 <span data-ttu-id="c1b02-287">Zie voor informatie over welke scalaire expressie die u wellicht waarden, [constanten](#bk_constants) sectie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-287">For details on values which scalar expression may have, see [Constants](#bk_constants) section.</span></span>  
  
 <span data-ttu-id="c1b02-288">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-288">**Syntax**</span></span>  
  
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
  
 <span data-ttu-id="c1b02-289">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-289">**Arguments**</span></span>  
  
-   `<constant>`  
  
     <span data-ttu-id="c1b02-290">Vertegenwoordigt een constante waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-290">Represents a constant value.</span></span> <span data-ttu-id="c1b02-291">Zie [constanten](#bk_constants) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-291">See [Constants](#bk_constants) section for details.</span></span>  
  
-   `input_alias`  
  
     <span data-ttu-id="c1b02-292">Hiermee geeft u een waarde die is gedefinieerd door Hallo `input_alias` geïntroduceerd in Hallo `FROM` component.</span><span class="sxs-lookup"><span data-stu-id="c1b02-292">Represents a value defined by hello `input_alias` introduced in hello `FROM` clause.</span></span>  
    <span data-ttu-id="c1b02-293">Deze waarde is gegarandeerd toonot worden **niet-gedefinieerde** –**niet-gedefinieerde** waarden in de Hallo invoer worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="c1b02-293">This value is guaranteed toonot be **undefined** –**undefined** values in hello input are skipped.</span></span>  
  
-   `<scalar_expression>.property_name`  
  
     <span data-ttu-id="c1b02-294">Vertegenwoordigt een waarde van Hallo-eigenschap van een object.</span><span class="sxs-lookup"><span data-stu-id="c1b02-294">Represents a value of hello property of an object.</span></span> <span data-ttu-id="c1b02-295">Als Hallo-eigenschap niet bestaat of eigenschap van een waarde die niet een object wordt verwezen, Hallo expressie evalueert vervolgens te**niet-gedefinieerde** waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-295">If hello property does not exist or property is referenced on a value which is not an object, then hello expression evaluates too**undefined** value.</span></span>  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     <span data-ttu-id="c1b02-296">Vertegenwoordigt een waarde van eigenschap met de naam Hallo `property_name` of matrixelement met index `array_index` van een objectmatrix.</span><span class="sxs-lookup"><span data-stu-id="c1b02-296">Represents a value of hello property with name `property_name` or array element with index `array_index` of an object/array.</span></span> <span data-ttu-id="c1b02-297">Als Hallo eigenschappenmatrix/index niet bestaat of Hallo eigenschappenmatrix/index op een waarde die niet een objectmatrix wordt verwezen, evalueert Hallo expressie tooundefined waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-297">If hello property/array index does not exist or hello property/array index is referenced on a value which is not an object/array, then hello expression evaluates tooundefined value.</span></span>  
  
-   `unary_operator <scalar_expression>`  
  
     <span data-ttu-id="c1b02-298">Vertegenwoordigt een operator die wordt toegepast tooa één waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-298">Represents an operator that is applied tooa single value.</span></span> <span data-ttu-id="c1b02-299">Zie [Operators](#bk_operators) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-299">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     <span data-ttu-id="c1b02-300">Een operator die is toegepast tootwo waarden vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="c1b02-300">Represents an operator that is applied tootwo values.</span></span> <span data-ttu-id="c1b02-301">Zie [Operators](#bk_operators) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-301">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_function_expression>`  
  
     <span data-ttu-id="c1b02-302">Vertegenwoordigt een waarde die is gedefinieerd door een resultaat van een functieaanroep.</span><span class="sxs-lookup"><span data-stu-id="c1b02-302">Represents a value defined by a result of a function call.</span></span>  
  
-   `udf_scalar_function`  
  
     <span data-ttu-id="c1b02-303">Naam van de gebruiker Hallo scalaire functie gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="c1b02-303">Name of hello user defined scalar function.</span></span>  
  
-   `builtin_scalar_function`  
  
     <span data-ttu-id="c1b02-304">Naam van de ingebouwde scalaire functie Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1b02-304">Name of hello built-in scalar function.</span></span>  
  
-   `<create_object_expression>`  
  
     <span data-ttu-id="c1b02-305">Hiermee geeft u een waarde die wordt verkregen door het maken van een nieuw object met de opgegeven eigenschappen en hun waarden.</span><span class="sxs-lookup"><span data-stu-id="c1b02-305">Represents a value obtained by creating a new object with specified properties and their values.</span></span>  
  
-   `<create_array_expression>`  
  
     <span data-ttu-id="c1b02-306">Hiermee geeft u een waarde die wordt verkregen door het maken van een nieuwe matrix met de opgegeven waarden als elementen</span><span class="sxs-lookup"><span data-stu-id="c1b02-306">Represents a value obtained by creating a new array with specified values as elements</span></span>  
  
-   `parameter_name`  
  
     <span data-ttu-id="c1b02-307">Vertegenwoordigt een waarde van de opgegeven parameternaam Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1b02-307">Represents a value of hello specified parameter name.</span></span> <span data-ttu-id="c1b02-308">Parameternamen moeten één @ hebben als eerste teken Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1b02-308">Parameter names must have a single @ as hello first character.</span></span>  
  
 <span data-ttu-id="c1b02-309">**Opmerkingen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-309">**Remarks**</span></span>  
  
 <span data-ttu-id="c1b02-310">Bij het aanroepen van een ingebouwde of de gebruiker gedefinieerde scalaire functie moeten alle argumenten worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="c1b02-310">When calling a built-in or user defined scalar function all arguments must be defined.</span></span> <span data-ttu-id="c1b02-311">Als een van de argumenten Hallo is gedefinieerd, Hallo-functie wordt niet aangeroepen en Hallo resultaat is niet gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="c1b02-311">If any of hello arguments is undefined, hello function will not be called and hello result will be undefined.</span></span>  
  
 <span data-ttu-id="c1b02-312">Bij het maken van een object, worden alle eigenschappen die niet-gedefinieerde waarde is toegewezen overgeslagen en niet is opgenomen in het Hallo-object gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c1b02-312">When creating an object, any property that is assigned undefined value will be skipped and not included in hello created object.</span></span>  
  
 <span data-ttu-id="c1b02-313">Wanneer het maken van een matrix, maar een elementwaarde die is toegewezen **niet-gedefinieerde** waarde wordt overgeslagen en niet is opgenomen in object Hallo gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c1b02-313">When creating an array, any element value that is assigned **undefined** value will be skipped and not included in hello created object.</span></span> <span data-ttu-id="c1b02-314">Hierdoor wordt vervolgens gedefinieerd Hallo element tootake plaats zodanig dat matrix Hallo gemaakt wordt niet hebt overgeslagen indexen.</span><span class="sxs-lookup"><span data-stu-id="c1b02-314">This will cause hello next defined element tootake its place in such a way that hello created array will not have skipped indexes.</span></span>  
  
##  <span data-ttu-id="c1b02-315"><a name="bk_operators"></a>Operators</span><span class="sxs-lookup"><span data-stu-id="c1b02-315"><a name="bk_operators"></a> Operators</span></span>  
 <span data-ttu-id="c1b02-316">Deze sectie beschrijft operators Hallo ondersteund.</span><span class="sxs-lookup"><span data-stu-id="c1b02-316">This section describes hello supported operators.</span></span> <span data-ttu-id="c1b02-317">Elke operator kan worden toegewezen tooexactly één categorie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-317">Each operator can be assigned tooexactly one category.</span></span>  
  
 <span data-ttu-id="c1b02-318">Zie **Operator categorieën** tabel hieronder voor meer informatie met betrekking tot de verwerking van **niet-gedefinieerde** waarden, type-vereisten voor de invoerwaarden en verwerking van waarden met niet overeenkomende typen.</span><span class="sxs-lookup"><span data-stu-id="c1b02-318">See **Operator categories** table below, for details regarding handling of **undefined** values, type requirements for input values and handling of values with not matching types.</span></span>  
  
 <span data-ttu-id="c1b02-319">**Operator categorieën:**</span><span class="sxs-lookup"><span data-stu-id="c1b02-319">**Operator categories:**</span></span>  
  
|<span data-ttu-id="c1b02-320">**Categorie**</span><span class="sxs-lookup"><span data-stu-id="c1b02-320">**Category**</span></span>|<span data-ttu-id="c1b02-321">**Details**</span><span class="sxs-lookup"><span data-stu-id="c1b02-321">**Details**</span></span>|  
|-|-|  
|<span data-ttu-id="c1b02-322">**rekenkundige bewerking**</span><span class="sxs-lookup"><span data-stu-id="c1b02-322">**arithmetic**</span></span>|<span data-ttu-id="c1b02-323">Operator verwacht input(s) toobe (s).</span><span class="sxs-lookup"><span data-stu-id="c1b02-323">Operator expects input(s) toobe Number(s).</span></span> <span data-ttu-id="c1b02-324">Uitvoer is ook een getal.</span><span class="sxs-lookup"><span data-stu-id="c1b02-324">Output is also a Number.</span></span> <span data-ttu-id="c1b02-325">Als een van de invoerwaarden Hallo **niet-gedefinieerde** of type dan het aantal vervolgens Hallo resultaat is **niet-gedefinieerde**.</span><span class="sxs-lookup"><span data-stu-id="c1b02-325">If any of hello inputs is **undefined** or type other than Number then hello result is **undefined**.</span></span>|  
|<span data-ttu-id="c1b02-326">**Bitsgewijze**</span><span class="sxs-lookup"><span data-stu-id="c1b02-326">**bitwise**</span></span>|<span data-ttu-id="c1b02-327">Operator verwacht input(s) toobe 32-bits geheel getal met teken (s).</span><span class="sxs-lookup"><span data-stu-id="c1b02-327">Operator expects input(s) toobe 32-bit signed integer Number(s).</span></span> <span data-ttu-id="c1b02-328">Uitvoer is ook een 32-bits geheel getal.</span><span class="sxs-lookup"><span data-stu-id="c1b02-328">Output is also 32-bit signed integer Number.</span></span><br /><br /> <span data-ttu-id="c1b02-329">Een niet-integerwaarde worden afgerond.</span><span class="sxs-lookup"><span data-stu-id="c1b02-329">Any non-integer value will be rounded.</span></span> <span data-ttu-id="c1b02-330">Positieve waarde wordt afgerond, negatieve getallen naar boven afgerond.</span><span class="sxs-lookup"><span data-stu-id="c1b02-330">Positive value will be rounded down, negative values rounded up.</span></span><br /><br /> <span data-ttu-id="c1b02-331">Een waarde die buiten het bereik van Hallo 32-bits geheel getal wordt geconverteerd, door te nemen van de laatste 32-bits van de twee van bits.</span><span class="sxs-lookup"><span data-stu-id="c1b02-331">Any value that is outside of hello 32-bit integer range will be converted, by taking last 32-bits of its two's complement notation.</span></span><br /><br /> <span data-ttu-id="c1b02-332">Als een van de invoerwaarden Hallo **niet-gedefinieerde** of andere dan getal, typt u vervolgens Hallo resultaat is **niet-gedefinieerde**.</span><span class="sxs-lookup"><span data-stu-id="c1b02-332">If any of hello inputs is **undefined** or type other than Number, then hello result is **undefined**.</span></span><br /><br /> <span data-ttu-id="c1b02-333">**Opmerking:** Hallo hierboven gedrag is compatibel met JavaScript bitsgewijze operator gedrag.</span><span class="sxs-lookup"><span data-stu-id="c1b02-333">**Note:** hello above behavior is compatible with JavaScript bitwise operator behavior.</span></span>|  
|<span data-ttu-id="c1b02-334">**logische**</span><span class="sxs-lookup"><span data-stu-id="c1b02-334">**logical**</span></span>|<span data-ttu-id="c1b02-335">Operator verwacht input(s) toobe Boolean(s).</span><span class="sxs-lookup"><span data-stu-id="c1b02-335">Operator expects input(s) toobe Boolean(s).</span></span> <span data-ttu-id="c1b02-336">Uitvoer is ook een Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-336">Output is also a Boolean.</span></span><br /><span data-ttu-id="c1b02-337">Als een van de invoerwaarden Hallo **niet-gedefinieerde** of andere dan Boolean, typ wordt Hallo resultaat **niet-gedefinieerde**.</span><span class="sxs-lookup"><span data-stu-id="c1b02-337">If any of hello inputs is **undefined** or type other than Boolean, then hello result will be **undefined**.</span></span>|  
|<span data-ttu-id="c1b02-338">**vergelijking**</span><span class="sxs-lookup"><span data-stu-id="c1b02-338">**comparison**</span></span>|<span data-ttu-id="c1b02-339">Operator verwacht input(s) toohave Hallo dezelfde typt en niet worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="c1b02-339">Operator expects input(s) toohave hello same type and not be undefined.</span></span> <span data-ttu-id="c1b02-340">Uitvoer is een Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-340">Output is a Boolean.</span></span><br /><br /> <span data-ttu-id="c1b02-341">Als een van de invoerwaarden Hallo **niet-gedefinieerde** of Hallo-invoer hebben verschillende typen en vervolgens Hallo resultaat is **niet-gedefinieerde**.</span><span class="sxs-lookup"><span data-stu-id="c1b02-341">If any of hello inputs is **undefined** or hello inputs have different types, then hello result is **undefined**.</span></span><br /><br /> <span data-ttu-id="c1b02-342">Zie **volgorde van waarden voor vergelijking** tabel voor waarde ordening details.</span><span class="sxs-lookup"><span data-stu-id="c1b02-342">See **Ordering of values for comparison** table for value ordering details.</span></span>|  
|<span data-ttu-id="c1b02-343">**tekenreeks**</span><span class="sxs-lookup"><span data-stu-id="c1b02-343">**string**</span></span>|<span data-ttu-id="c1b02-344">Operator verwacht input(s) toobe meer.</span><span class="sxs-lookup"><span data-stu-id="c1b02-344">Operator expects input(s) toobe String(s).</span></span> <span data-ttu-id="c1b02-345">Uitvoer is ook een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="c1b02-345">Output is also a String.</span></span><br /><span data-ttu-id="c1b02-346">Als een van de invoerwaarden Hallo **niet-gedefinieerde** of type heeft dan tekenreeks vervolgens Hallo resultaat is **niet-gedefinieerde**.</span><span class="sxs-lookup"><span data-stu-id="c1b02-346">If any of hello inputs is **undefined** or type other than String then hello result is **undefined**.</span></span>|  
  
 <span data-ttu-id="c1b02-347">**Unaire operators:**</span><span class="sxs-lookup"><span data-stu-id="c1b02-347">**Unary operators:**</span></span>  
  
|<span data-ttu-id="c1b02-348">**Naam**</span><span class="sxs-lookup"><span data-stu-id="c1b02-348">**Name**</span></span>|<span data-ttu-id="c1b02-349">**Operator**</span><span class="sxs-lookup"><span data-stu-id="c1b02-349">**Operator**</span></span>|<span data-ttu-id="c1b02-350">**Details**</span><span class="sxs-lookup"><span data-stu-id="c1b02-350">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="c1b02-351">**rekenkundige bewerking**</span><span class="sxs-lookup"><span data-stu-id="c1b02-351">**arithmetic**</span></span>|+<br /><br /> -|<span data-ttu-id="c1b02-352">Hallo getal-waarde als resultaat gegeven.</span><span class="sxs-lookup"><span data-stu-id="c1b02-352">Returns hello number value.</span></span><br /><br /> <span data-ttu-id="c1b02-353">Bitsgewijze onderhandeling.</span><span class="sxs-lookup"><span data-stu-id="c1b02-353">Bitwise negation.</span></span> <span data-ttu-id="c1b02-354">De numerieke waarde retourneert genegeerde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-354">Returns negated number value.</span></span>|  
|<span data-ttu-id="c1b02-355">**Bitsgewijze**</span><span class="sxs-lookup"><span data-stu-id="c1b02-355">**bitwise**</span></span>|~|<span data-ttu-id="c1b02-356">Toepassingsgroepen de aanvulling.</span><span class="sxs-lookup"><span data-stu-id="c1b02-356">Ones' complement.</span></span> <span data-ttu-id="c1b02-357">Retourneert een reeks een numerieke waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-357">Returns a complement of a number value.</span></span>|  
|<span data-ttu-id="c1b02-358">**Logische**</span><span class="sxs-lookup"><span data-stu-id="c1b02-358">**Logical**</span></span>|<span data-ttu-id="c1b02-359">**NIET**</span><span class="sxs-lookup"><span data-stu-id="c1b02-359">**NOT**</span></span>|<span data-ttu-id="c1b02-360">Negatie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-360">Negation.</span></span> <span data-ttu-id="c1b02-361">Retourneert genegeerde Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-361">Returns negated Boolean value.</span></span>|  
  
 <span data-ttu-id="c1b02-362">**Binaire operators:**</span><span class="sxs-lookup"><span data-stu-id="c1b02-362">**Binary operators:**</span></span>  
  
|<span data-ttu-id="c1b02-363">**Naam**</span><span class="sxs-lookup"><span data-stu-id="c1b02-363">**Name**</span></span>|<span data-ttu-id="c1b02-364">**Operator**</span><span class="sxs-lookup"><span data-stu-id="c1b02-364">**Operator**</span></span>|<span data-ttu-id="c1b02-365">**Details**</span><span class="sxs-lookup"><span data-stu-id="c1b02-365">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="c1b02-366">**rekenkundige bewerking**</span><span class="sxs-lookup"><span data-stu-id="c1b02-366">**arithmetic**</span></span>|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|<span data-ttu-id="c1b02-367">Toevoeging.</span><span class="sxs-lookup"><span data-stu-id="c1b02-367">Addition.</span></span><br /><br /> <span data-ttu-id="c1b02-368">Aftrekken.</span><span class="sxs-lookup"><span data-stu-id="c1b02-368">Subtraction.</span></span><br /><br /> <span data-ttu-id="c1b02-369">Vermenigvuldigen.</span><span class="sxs-lookup"><span data-stu-id="c1b02-369">Multiplication.</span></span><br /><br /> <span data-ttu-id="c1b02-370">Deling.</span><span class="sxs-lookup"><span data-stu-id="c1b02-370">Division.</span></span><br /><br /> <span data-ttu-id="c1b02-371">Modulatie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-371">Modulation.</span></span>|  
|<span data-ttu-id="c1b02-372">**Bitsgewijze**</span><span class="sxs-lookup"><span data-stu-id="c1b02-372">**bitwise**</span></span>|<span data-ttu-id="c1b02-373">&#124;</span><span class="sxs-lookup"><span data-stu-id="c1b02-373">&#124;</span></span><br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|<span data-ttu-id="c1b02-374">Bitsgewijze OR.</span><span class="sxs-lookup"><span data-stu-id="c1b02-374">Bitwise OR.</span></span><br /><br /> <span data-ttu-id="c1b02-375">Bitsgewijze AND.</span><span class="sxs-lookup"><span data-stu-id="c1b02-375">Bitwise AND.</span></span><br /><br /> <span data-ttu-id="c1b02-376">Bitsgewijze XOR.</span><span class="sxs-lookup"><span data-stu-id="c1b02-376">Bitwise XOR.</span></span><br /><br /> <span data-ttu-id="c1b02-377">Verschuiving naar links.</span><span class="sxs-lookup"><span data-stu-id="c1b02-377">Left Shift.</span></span><br /><br /> <span data-ttu-id="c1b02-378">Rechts verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="c1b02-378">Right Shift.</span></span><br /><br /> <span data-ttu-id="c1b02-379">Nul opvulling rechts verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="c1b02-379">Zero-fill Right Shift.</span></span>|  
|<span data-ttu-id="c1b02-380">**logische**</span><span class="sxs-lookup"><span data-stu-id="c1b02-380">**logical**</span></span>|<span data-ttu-id="c1b02-381">**EN**</span><span class="sxs-lookup"><span data-stu-id="c1b02-381">**AND**</span></span><br /><br /> <span data-ttu-id="c1b02-382">**OR**</span><span class="sxs-lookup"><span data-stu-id="c1b02-382">**OR**</span></span>|<span data-ttu-id="c1b02-383">Logische verbinding.</span><span class="sxs-lookup"><span data-stu-id="c1b02-383">Logical conjunction.</span></span> <span data-ttu-id="c1b02-384">Retourneert **true** als beide argumenten zijn **true**, retourneert **false** anders.</span><span class="sxs-lookup"><span data-stu-id="c1b02-384">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="c1b02-385">Logische verbinding.</span><span class="sxs-lookup"><span data-stu-id="c1b02-385">Logical conjunction.</span></span> <span data-ttu-id="c1b02-386">Retourneert **true** als beide argumenten zijn **true**, retourneert **false** anders.</span><span class="sxs-lookup"><span data-stu-id="c1b02-386">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span>|  
|<span data-ttu-id="c1b02-387">**vergelijking**</span><span class="sxs-lookup"><span data-stu-id="c1b02-387">**comparison**</span></span>|**=**<br /><br /> <span data-ttu-id="c1b02-388">**!=, <>**</span><span class="sxs-lookup"><span data-stu-id="c1b02-388">**!=, <>**</span></span><br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> <span data-ttu-id="c1b02-389">**??**</span><span class="sxs-lookup"><span data-stu-id="c1b02-389">**??**</span></span>|<span data-ttu-id="c1b02-390">Is gelijk aan.</span><span class="sxs-lookup"><span data-stu-id="c1b02-390">Equals.</span></span> <span data-ttu-id="c1b02-391">Retourneert **true** als argumenten gelijk zijn, retourneert **false** anders.</span><span class="sxs-lookup"><span data-stu-id="c1b02-391">Returns **true** if arguments are equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="c1b02-392">Niet gelijk aan.</span><span class="sxs-lookup"><span data-stu-id="c1b02-392">Not equal to.</span></span> <span data-ttu-id="c1b02-393">Retourneert **true** als argumenten niet gelijk zijn, retourneert **false** anders.</span><span class="sxs-lookup"><span data-stu-id="c1b02-393">Returns **true** if arguments are not equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="c1b02-394">Groter dan.</span><span class="sxs-lookup"><span data-stu-id="c1b02-394">Greater Than.</span></span> <span data-ttu-id="c1b02-395">Retourneert **true** als eerste argument groter is dan de tweede hello, retourneren **false** anders.</span><span class="sxs-lookup"><span data-stu-id="c1b02-395">Returns **true** if first argument is greater than hello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="c1b02-396">Groter dan of gelijk zijn aan.</span><span class="sxs-lookup"><span data-stu-id="c1b02-396">Greater Than or Equal To.</span></span> <span data-ttu-id="c1b02-397">Retourneert **true** als eerste argument is groter dan of gelijk zijn aan toohello tweede, retourneren **false** anders.</span><span class="sxs-lookup"><span data-stu-id="c1b02-397">Returns **true** if first argument is greater than or equal toohello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="c1b02-398">Minder dan.</span><span class="sxs-lookup"><span data-stu-id="c1b02-398">Less Than.</span></span> <span data-ttu-id="c1b02-399">Retourneert **true** als eerste argument lager is dan het tweede hello, geretourneerd **false** anders.</span><span class="sxs-lookup"><span data-stu-id="c1b02-399">Returns **true** if first argument is less than hello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="c1b02-400">Kleiner dan of gelijk zijn aan.</span><span class="sxs-lookup"><span data-stu-id="c1b02-400">Less Than or Equal To.</span></span> <span data-ttu-id="c1b02-401">Retourneert **true** als eerste argument kleiner dan of gelijk is toohello tweede een return **false** anders.</span><span class="sxs-lookup"><span data-stu-id="c1b02-401">Returns **true** if first argument is less than or equal toohello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="c1b02-402">Coalesce.</span><span class="sxs-lookup"><span data-stu-id="c1b02-402">Coalesce.</span></span> <span data-ttu-id="c1b02-403">Retourneert Hallo tweede argument als eerste argument Hallo een **niet-gedefinieerde** waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-403">Returns hello second argument if hello first argument is an **undefined** value.</span></span>|  
|<span data-ttu-id="c1b02-404">**Tekenreeks**</span><span class="sxs-lookup"><span data-stu-id="c1b02-404">**String**</span></span>|<span data-ttu-id="c1b02-405">**&#124;&#124;**</span><span class="sxs-lookup"><span data-stu-id="c1b02-405">**&#124;&#124;**</span></span>|<span data-ttu-id="c1b02-406">Samenvoeging.</span><span class="sxs-lookup"><span data-stu-id="c1b02-406">Concatenation.</span></span> <span data-ttu-id="c1b02-407">Retourneert een samenvoeging van beide argumenten.</span><span class="sxs-lookup"><span data-stu-id="c1b02-407">Returns a concatenation of both arguments.</span></span>|  
  
 <span data-ttu-id="c1b02-408">**Ternair operators:**</span><span class="sxs-lookup"><span data-stu-id="c1b02-408">**Ternary operators:**</span></span>  
  
|<span data-ttu-id="c1b02-409">Ternaire operator</span><span class="sxs-lookup"><span data-stu-id="c1b02-409">Ternary operator</span></span>|<span data-ttu-id="c1b02-410">?</span><span class="sxs-lookup"><span data-stu-id="c1b02-410">?</span></span>|<span data-ttu-id="c1b02-411">Retourneert Hallo tweede argument als eerste argument Hallo te evalueert**true**; anders Hallo derde argument retourneren.</span><span class="sxs-lookup"><span data-stu-id="c1b02-411">Returns hello second argument if hello first argument evaluates too**true**; return hello third argument otherwise.</span></span>|  
|-|-|-|  
  
 <span data-ttu-id="c1b02-412">**Ordening van waarden voor vergelijking**</span><span class="sxs-lookup"><span data-stu-id="c1b02-412">**Ordering of values for comparison**</span></span>  
  
|<span data-ttu-id="c1b02-413">**Type**</span><span class="sxs-lookup"><span data-stu-id="c1b02-413">**Type**</span></span>|<span data-ttu-id="c1b02-414">**De volgorde van de waarden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-414">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="c1b02-415">**Niet-gedefinieerd**</span><span class="sxs-lookup"><span data-stu-id="c1b02-415">**Undefined**</span></span>|<span data-ttu-id="c1b02-416">Niet worden vergeleken.</span><span class="sxs-lookup"><span data-stu-id="c1b02-416">Not comparable.</span></span>|  
|<span data-ttu-id="c1b02-417">**Null**</span><span class="sxs-lookup"><span data-stu-id="c1b02-417">**Null**</span></span>|<span data-ttu-id="c1b02-418">Eén waarde: **null**</span><span class="sxs-lookup"><span data-stu-id="c1b02-418">Single value: **null**</span></span>|  
|<span data-ttu-id="c1b02-419">**Aantal**</span><span class="sxs-lookup"><span data-stu-id="c1b02-419">**Number**</span></span>|<span data-ttu-id="c1b02-420">Natuurlijke reëel getal.</span><span class="sxs-lookup"><span data-stu-id="c1b02-420">Natural real number.</span></span><br /><br /> <span data-ttu-id="c1b02-421">Negatieve oneindige waarde is kleiner dan andere numerieke waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-421">Negative Infinity value is smaller than any other Number value.</span></span><br /><br /> <span data-ttu-id="c1b02-422">Positieve oneindige waarde is groter dan andere numerieke waarde. **NaN** waarde kan niet worden vergeleken.</span><span class="sxs-lookup"><span data-stu-id="c1b02-422">Positive Infinity value is larger than any other Number value.**NaN** value is not comparable.</span></span> <span data-ttu-id="c1b02-423">Vergelijken met **NaN** leidt ertoe dat **niet-gedefinieerde** waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-423">Comparing with **NaN** will result in **undefined** value.</span></span>|  
|<span data-ttu-id="c1b02-424">**Tekenreeks**</span><span class="sxs-lookup"><span data-stu-id="c1b02-424">**String**</span></span>|<span data-ttu-id="c1b02-425">Lexicographical volgorde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-425">Lexicographical order.</span></span>|  
|<span data-ttu-id="c1b02-426">**Matrix**</span><span class="sxs-lookup"><span data-stu-id="c1b02-426">**Array**</span></span>|<span data-ttu-id="c1b02-427">Er is geen ordening, maar billijke.</span><span class="sxs-lookup"><span data-stu-id="c1b02-427">No ordering, but equitable.</span></span>|  
|<span data-ttu-id="c1b02-428">**Object**</span><span class="sxs-lookup"><span data-stu-id="c1b02-428">**Object**</span></span>|<span data-ttu-id="c1b02-429">Er is geen ordening, maar billijke.</span><span class="sxs-lookup"><span data-stu-id="c1b02-429">No ordering, but equitable.</span></span>|  
  
 <span data-ttu-id="c1b02-430">**Opmerkingen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-430">**Remarks**</span></span>  
  
 <span data-ttu-id="c1b02-431">In Azure Cosmos DB Hallo typen waarden vaak niet bekend zijn totdat ze daadwerkelijk worden opgehaald uit Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="c1b02-431">In Azure Cosmos DB, hello types of values are often not known until they are actually retrieved from hello database.</span></span> <span data-ttu-id="c1b02-432">In volgorde toosupport efficiënte uitvoering van query's hebben de meeste Hallo operators strikt type vereisten.</span><span class="sxs-lookup"><span data-stu-id="c1b02-432">In order toosupport efficient execution of queries, most of hello operators have strict type requirements.</span></span> <span data-ttu-id="c1b02-433">Operators zelf voeren ook geen impliciete conversies.</span><span class="sxs-lookup"><span data-stu-id="c1b02-433">Also operators by themselves do not perform implicit conversions.</span></span>  
  
 <span data-ttu-id="c1b02-434">Dit betekent dat een query, zoals: Selecteer * van ROOT r waar r.Age = 21 retourneert alleen documenten met leeftijd gelijk toohello getal 21-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="c1b02-434">This means that a query like: SELECT * FROM ROOT r WHERE r.Age = 21 will only return documents with property Age equal toohello number 21.</span></span> <span data-ttu-id="c1b02-435">Documenten met de eigenschap leeftijd gelijk toohello tekenreeks '21' of Hallo tekenreeks '0021' wordt niet overeenkomen, als Hallo expressie '21' = 21 tooundefined evalueert.</span><span class="sxs-lookup"><span data-stu-id="c1b02-435">Documents with property Age equal toohello string "21" or hello string "0021" will not match, as hello expression "21" = 21 evaluates tooundefined.</span></span> <span data-ttu-id="c1b02-436">Hiermee kunt u een beter gebruik van indexen, omdat Hallo opzoeken van een specifieke waarde (dat wil zeggen 21 number) is sneller dan zoeken naar oneindig aantal mogelijke overeenkomsten (dat wil zeggen getal 21 of tekenreeksen '21', '021', "21.0"...).</span><span class="sxs-lookup"><span data-stu-id="c1b02-436">This allows for a better use of indexes, because hello lookup of a specific value (i.e. number 21) is faster than search for indefinite number of potential matches (i.e. number 21 or strings "21", "021", "21.0" …).</span></span> <span data-ttu-id="c1b02-437">Dit wijkt af van hoe JavaScript operators van waarden van verschillende typen evalueert.</span><span class="sxs-lookup"><span data-stu-id="c1b02-437">This is different from how JavaScript evaluates operators on values of different types.</span></span>  
  
 <span data-ttu-id="c1b02-438">**Matrices en objecten gelijkheid en het vergelijkingstype**</span><span class="sxs-lookup"><span data-stu-id="c1b02-438">**Arrays and objects equality and comparison**</span></span>  
  
 <span data-ttu-id="c1b02-439">Vergelijken van de matrix of Object waarden met bereik operators (>, > =, <, < =) leidt ertoe dat niet-gedefinieerde omdat er geen volgorde gedefinieerd op het Object of de matrix waarden.</span><span class="sxs-lookup"><span data-stu-id="c1b02-439">Comparing of Array or Object values using range operators (>, >=, <, <=) will result in undefined as there is not order defined on Object or Array values.</span></span> <span data-ttu-id="c1b02-440">Echter met gelijk-ongelijk operators (=,! =, <>) wordt ondersteund en waarden structureel's worden vergeleken.</span><span class="sxs-lookup"><span data-stu-id="c1b02-440">However using equality/inequality operators (=, !=, <>) is supported and values will be compared structurally.</span></span>  
  
 <span data-ttu-id="c1b02-441">Matrices zijn gelijk als beide matrices hetzelfde aantal elementen hebben en elementen op die overeenkomt met de posities ook gelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="c1b02-441">Arrays are equal if both arrays have same number of elements and elements at matching positions are also equal.</span></span> <span data-ttu-id="c1b02-442">Als een combinatie van elementen vergelijken in een niet-gedefinieerde, Hallo resultaat van de vergelijking van de matrix resulteert is niet gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="c1b02-442">If comparing any pair of elements results in undefined, hello result of array comparison is undefined.</span></span>  
  
 <span data-ttu-id="c1b02-443">Objecten zijn gelijk als beide objecten hebben dezelfde eigenschappen die zijn gedefinieerd, en als de waarden van eigenschappen die overeenkomt met ook gelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="c1b02-443">Objects are equal if both objects have same properties defined, and if values of matching properties are also equal.</span></span> <span data-ttu-id="c1b02-444">Als elk paar eigenschapswaarden vergelijken in een niet-gedefinieerde, Hallo resultaat van het object vergelijking resulteert is niet gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="c1b02-444">If comparing any pair of property values results in undefined, hello result of object comparison is undefined.</span></span>  
  
##  <span data-ttu-id="c1b02-445"><a name="bk_constants"></a>Constanten</span><span class="sxs-lookup"><span data-stu-id="c1b02-445"><a name="bk_constants"></a> Constants</span></span>  
 <span data-ttu-id="c1b02-446">Een constante, ook wel bekend als een letterlijke waarde of een scalaire waarde is een symbool dat de waarde van een specifieke gegevens vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="c1b02-446">A constant, also known as a literal or a scalar value, is a symbol that represents a specific data value.</span></span> <span data-ttu-id="c1b02-447">Hallo-indeling van een constante is afhankelijk van Hallo-gegevenstype van Hallo-waarde vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="c1b02-447">hello format of a constant depends on hello data type of hello value it represents.</span></span>  
  
 <span data-ttu-id="c1b02-448">**Scalaire-gegevenstypen ondersteund:**</span><span class="sxs-lookup"><span data-stu-id="c1b02-448">**Supported scalar data types:**</span></span>  
  
|<span data-ttu-id="c1b02-449">**Type**</span><span class="sxs-lookup"><span data-stu-id="c1b02-449">**Type**</span></span>|<span data-ttu-id="c1b02-450">**De volgorde van de waarden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-450">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="c1b02-451">**Niet-gedefinieerd**</span><span class="sxs-lookup"><span data-stu-id="c1b02-451">**Undefined**</span></span>|<span data-ttu-id="c1b02-452">Eén waarde: **niet gedefinieerd**</span><span class="sxs-lookup"><span data-stu-id="c1b02-452">Single value: **undefined**</span></span>|  
|<span data-ttu-id="c1b02-453">**Null**</span><span class="sxs-lookup"><span data-stu-id="c1b02-453">**Null**</span></span>|<span data-ttu-id="c1b02-454">Eén waarde: **null**</span><span class="sxs-lookup"><span data-stu-id="c1b02-454">Single value: **null**</span></span>|  
|<span data-ttu-id="c1b02-455">**Booleaanse waarde**</span><span class="sxs-lookup"><span data-stu-id="c1b02-455">**Boolean**</span></span>|<span data-ttu-id="c1b02-456">Waarden: **false**, **true**.</span><span class="sxs-lookup"><span data-stu-id="c1b02-456">Values: **false**, **true**.</span></span>|  
|<span data-ttu-id="c1b02-457">**Aantal**</span><span class="sxs-lookup"><span data-stu-id="c1b02-457">**Number**</span></span>|<span data-ttu-id="c1b02-458">Een getal met dubbele precisie drijvende komma IEEE-norm 754.</span><span class="sxs-lookup"><span data-stu-id="c1b02-458">A double-precision floating-point number, IEEE 754 standard.</span></span>|  
|<span data-ttu-id="c1b02-459">**Tekenreeks**</span><span class="sxs-lookup"><span data-stu-id="c1b02-459">**String**</span></span>|<span data-ttu-id="c1b02-460">Een reeks van nul of meer Unicode-tekens.</span><span class="sxs-lookup"><span data-stu-id="c1b02-460">A sequence of zero or more Unicode characters.</span></span> <span data-ttu-id="c1b02-461">Tekenreeksen moeten worden ingesloten in enkele of dubbele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="c1b02-461">Strings must be enclosed in single or double quotes.</span></span>|  
|<span data-ttu-id="c1b02-462">**Matrix**</span><span class="sxs-lookup"><span data-stu-id="c1b02-462">**Array**</span></span>|<span data-ttu-id="c1b02-463">Een reeks van nul of meer elementen.</span><span class="sxs-lookup"><span data-stu-id="c1b02-463">A sequence of zero or more elements.</span></span> <span data-ttu-id="c1b02-464">Elk element is een waarde van elk gegevenstype scalaire, behalve Undefined.</span><span class="sxs-lookup"><span data-stu-id="c1b02-464">Each element can be a value of any scalar data type, except Undefined.</span></span>|  
|<span data-ttu-id="c1b02-465">**Object**</span><span class="sxs-lookup"><span data-stu-id="c1b02-465">**Object**</span></span>|<span data-ttu-id="c1b02-466">Een niet-geordende reeks nul of meer naam/waarde-paren.</span><span class="sxs-lookup"><span data-stu-id="c1b02-466">An unordered set of zero or more name/value pairs.</span></span> <span data-ttu-id="c1b02-467">De naam van een Unicode-tekenreeks is, de waarde kan zijn van elk gegevenstype scalaire, behalve **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="c1b02-467">Name is a Unicode string, value can be of any scalar data type, except **Undefined**.</span></span>|  
  
 <span data-ttu-id="c1b02-468">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-468">**Syntax**</span></span>  
  
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
  
 <span data-ttu-id="c1b02-469">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-469">**Arguments**</span></span>  
  
1.  `<undefined_constant>; undefined`  
  
     <span data-ttu-id="c1b02-470">Geeft niet-gedefinieerde waarde van het type niet gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="c1b02-470">Represents undefined value of type Undefined.</span></span>  
  
2.  `<null_constant>; null`  
  
     <span data-ttu-id="c1b02-471">Hiermee geeft u **null** waarde van het type **Null**.</span><span class="sxs-lookup"><span data-stu-id="c1b02-471">Represents **null** value of type **Null**.</span></span>  
  
3.  `<boolean_constant>`  
  
     <span data-ttu-id="c1b02-472">Constante van het type Booleaans vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="c1b02-472">Represents constant of type Boolean.</span></span>  
  
4.  `false`  
  
     <span data-ttu-id="c1b02-473">Hiermee geeft u **false** waarde van het type Boole-waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-473">Represents **false** value of type Boolean.</span></span>  
  
5.  `true`  
  
     <span data-ttu-id="c1b02-474">Hiermee geeft u **true** waarde van het type Boole-waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-474">Represents **true** value of type Boolean.</span></span>  
  
6.  `<number_constant>`  
  
     <span data-ttu-id="c1b02-475">Hiermee geeft u een constante.</span><span class="sxs-lookup"><span data-stu-id="c1b02-475">Represents a constant.</span></span>  
  
7.  `decimal_literal`  
  
     <span data-ttu-id="c1b02-476">Decimale letterlijke waarden zijn getallen weergegeven met behulp van de decimale notatie of wetenschappelijke notatie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-476">Decimal literals are numbers represented using either decimal notation, or scientific notation.</span></span>  
  
8.  `hexadecimal_literal`  
  
     <span data-ttu-id="c1b02-477">Hexadecimale letterlijke waarden zijn getallen weergegeven met behulp van het voorvoegsel '0 x' gevolgd door een of meer hexadecimale cijfers.</span><span class="sxs-lookup"><span data-stu-id="c1b02-477">Hexadecimal literals are numbers represented using prefix '0x' followed by one or more hexadecimal digits.</span></span>  
  
9. `<string_constant>`  
  
     <span data-ttu-id="c1b02-478">Hiermee geeft u een constante van het type String.</span><span class="sxs-lookup"><span data-stu-id="c1b02-478">Represents a constant of type String.</span></span>  
  
10. `string _literal`  
  
     <span data-ttu-id="c1b02-479">Letterlijke tekenreeks zijn vertegenwoordigd door een reeks van nul of meer Unicode-tekens of escapereeksen Unicode-tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="c1b02-479">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="c1b02-480">Letterlijke tekenreeks zijn ingesloten in enkele aanhalingstekens (apostrof: ') of dubbele aanhalingstekens (aanhalingsteken: ').</span><span class="sxs-lookup"><span data-stu-id="c1b02-480">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span>  
  
 <span data-ttu-id="c1b02-481">Volgende escapereeksen worden toegestaan:</span><span class="sxs-lookup"><span data-stu-id="c1b02-481">Following escape sequences are allowed:</span></span>  
  
|<span data-ttu-id="c1b02-482">**Escape-reeks**</span><span class="sxs-lookup"><span data-stu-id="c1b02-482">**Escape sequence**</span></span>|<span data-ttu-id="c1b02-483">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="c1b02-483">**Description**</span></span>|<span data-ttu-id="c1b02-484">**Unicode-teken**</span><span class="sxs-lookup"><span data-stu-id="c1b02-484">**Unicode character**</span></span>|  
|-|-|-|  
|<span data-ttu-id="c1b02-485">\\'</span><span class="sxs-lookup"><span data-stu-id="c1b02-485">\\'</span></span>|<span data-ttu-id="c1b02-486">enkel aanhalingsteken (')</span><span class="sxs-lookup"><span data-stu-id="c1b02-486">apostrophe (')</span></span>|<span data-ttu-id="c1b02-487">U + 0027</span><span class="sxs-lookup"><span data-stu-id="c1b02-487">U+0027</span></span>|  
|<span data-ttu-id="c1b02-488">\\"</span><span class="sxs-lookup"><span data-stu-id="c1b02-488">\\"</span></span>|<span data-ttu-id="c1b02-489">aanhalingsteken (")</span><span class="sxs-lookup"><span data-stu-id="c1b02-489">quotation mark (")</span></span>|<span data-ttu-id="c1b02-490">U + 0022</span><span class="sxs-lookup"><span data-stu-id="c1b02-490">U+0022</span></span>|  
|\\\|<span data-ttu-id="c1b02-491">omgekeerde schuine streep (\\)</span><span class="sxs-lookup"><span data-stu-id="c1b02-491">reverse solidus (\\)</span></span>|<span data-ttu-id="c1b02-492">U + 005C</span><span class="sxs-lookup"><span data-stu-id="c1b02-492">U+005C</span></span>|  
|\\/|<span data-ttu-id="c1b02-493">schuine streep (/)</span><span class="sxs-lookup"><span data-stu-id="c1b02-493">solidus (/)</span></span>|<span data-ttu-id="c1b02-494">U + 002F</span><span class="sxs-lookup"><span data-stu-id="c1b02-494">U+002F</span></span>|  
|<span data-ttu-id="c1b02-495">\ber</span><span class="sxs-lookup"><span data-stu-id="c1b02-495">\b</span></span>|<span data-ttu-id="c1b02-496">BACKSPACE</span><span class="sxs-lookup"><span data-stu-id="c1b02-496">backspace</span></span>|<span data-ttu-id="c1b02-497">U + 0008</span><span class="sxs-lookup"><span data-stu-id="c1b02-497">U+0008</span></span>|  
|<span data-ttu-id="c1b02-498">\f</span><span class="sxs-lookup"><span data-stu-id="c1b02-498">\f</span></span>|<span data-ttu-id="c1b02-499">formulier feed</span><span class="sxs-lookup"><span data-stu-id="c1b02-499">form feed</span></span>|<span data-ttu-id="c1b02-500">U + 000C</span><span class="sxs-lookup"><span data-stu-id="c1b02-500">U+000C</span></span>|  
|\n|<span data-ttu-id="c1b02-501">nieuwe regel</span><span class="sxs-lookup"><span data-stu-id="c1b02-501">line feed</span></span>|<span data-ttu-id="c1b02-502">U + 000A</span><span class="sxs-lookup"><span data-stu-id="c1b02-502">U+000A</span></span>|  
|<span data-ttu-id="c1b02-503">\r</span><span class="sxs-lookup"><span data-stu-id="c1b02-503">\r</span></span>|<span data-ttu-id="c1b02-504">regelterugloop</span><span class="sxs-lookup"><span data-stu-id="c1b02-504">carriage return</span></span>|<span data-ttu-id="c1b02-505">U + 000D</span><span class="sxs-lookup"><span data-stu-id="c1b02-505">U+000D</span></span>|  
|<span data-ttu-id="c1b02-506">\t</span><span class="sxs-lookup"><span data-stu-id="c1b02-506">\t</span></span>|<span data-ttu-id="c1b02-507">tabblad</span><span class="sxs-lookup"><span data-stu-id="c1b02-507">tab</span></span>|<span data-ttu-id="c1b02-508">U + 0009</span><span class="sxs-lookup"><span data-stu-id="c1b02-508">U+0009</span></span>|  
|<span data-ttu-id="c1b02-509">\uXXXX</span><span class="sxs-lookup"><span data-stu-id="c1b02-509">\uXXXX</span></span>|<span data-ttu-id="c1b02-510">Een Unicode-teken is gedefinieerd door 4 hexadecimale cijfers.</span><span class="sxs-lookup"><span data-stu-id="c1b02-510">A Unicode character defined by 4 hexadecimal digits.</span></span>|<span data-ttu-id="c1b02-511">U + XXXX</span><span class="sxs-lookup"><span data-stu-id="c1b02-511">U+XXXX</span></span>|  
  
##  <span data-ttu-id="c1b02-512"><a name="bk_query_perf_guidelines"></a>Richtlijnen voor query-prestaties</span><span class="sxs-lookup"><span data-stu-id="c1b02-512"><a name="bk_query_perf_guidelines"></a> Query performance guidelines</span></span>  
 <span data-ttu-id="c1b02-513">Om een query toobe efficiënt voor een grote verzameling wordt uitgevoerd, moet deze filters die kunnen worden geleverd via een of meer indexen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c1b02-513">In order for a query toobe executed efficiently for a large collection, it should use filters which can be served through one or more indexes.</span></span>  
  
 <span data-ttu-id="c1b02-514">Hallo na filters wordt voor het opzoeken van de index beschouwd:</span><span class="sxs-lookup"><span data-stu-id="c1b02-514">hello following filters will be considered for index lookup:</span></span>  
  
-   <span data-ttu-id="c1b02-515">Gebruik gelijkheidsoperator (=) met een padexpressie document en een constante.</span><span class="sxs-lookup"><span data-stu-id="c1b02-515">Use equality operator ( = ) with a document path expression and a constant.</span></span>  
  
-   <span data-ttu-id="c1b02-516">Bereikoperatoren gebruiken (<, \<=, >, > =) met een padexpressie document en aantal constanten.</span><span class="sxs-lookup"><span data-stu-id="c1b02-516">Use range operators (<, \<=, >, >=) with a document path expression and number constants.</span></span>  
  
-   <span data-ttu-id="c1b02-517">Document padexpressie staat voor een expressie waarmee een constante pad in Hallo documenten uit de database-collectie Hallo waarnaar wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="c1b02-517">Document path expression stands for any expression which identifies a constant path in hello documents from hello referenced database collection.</span></span>  
  
 <span data-ttu-id="c1b02-518">**Document padexpressie**</span><span class="sxs-lookup"><span data-stu-id="c1b02-518">**Document path expression**</span></span>  
  
 <span data-ttu-id="c1b02-519">Document padexpressies zijn expressies die een pad van de eigenschap of matrix indexeerfunctie beoordelaars via een document dat afkomstig is van de database verzameling documenten.</span><span class="sxs-lookup"><span data-stu-id="c1b02-519">Document path expressions are expressions that a path of property or array indexer assessors over a document coming from database collection documents.</span></span> <span data-ttu-id="c1b02-520">Dit pad mag gebruikte tooidentify Hallo locatie waarnaar wordt verwezen in een filter rechtstreeks in het Hallo-documenten in Hallo database verzameling waarden.</span><span class="sxs-lookup"><span data-stu-id="c1b02-520">This path can be used tooidentify hello location of values referenced in a filter directly within hello documents in hello database collection.</span></span>  
  
 <span data-ttu-id="c1b02-521">Voor een expressie toobe beschouwd als een document padexpressie, de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="c1b02-521">For an expression toobe considered a document path expression, it should:</span></span>  
  
1.  <span data-ttu-id="c1b02-522">Verwijzing Hallo verzameling root rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="c1b02-522">Reference hello collection root directly.</span></span>  
  
2.  <span data-ttu-id="c1b02-523">Verwijzing naar eigenschap of constante matrix indexeerfunctie van sommige padexpressie document</span><span class="sxs-lookup"><span data-stu-id="c1b02-523">Reference property or constant array indexer of some document path expression</span></span>  
  
3.  <span data-ttu-id="c1b02-524">Verwijzen naar een alias die bepaalde padexpressie document vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="c1b02-524">Reference an alias, which represents some document path expression.</span></span>  
  
     <span data-ttu-id="c1b02-525">**Syntaxis conventies**</span><span class="sxs-lookup"><span data-stu-id="c1b02-525">**Syntax conventions**</span></span>  
  
     <span data-ttu-id="c1b02-526">Hallo volgende tabel beschrijft Hallo conventies toodescribe syntaxis in Hallo Quertytaal API-verwijzing.</span><span class="sxs-lookup"><span data-stu-id="c1b02-526">hello following table describes hello conventions used toodescribe syntax in hello DocumentDB API Query Language reference.</span></span>  
  
    |<span data-ttu-id="c1b02-527">**Conventies**</span><span class="sxs-lookup"><span data-stu-id="c1b02-527">**Convention**</span></span>|<span data-ttu-id="c1b02-528">**Gebruikt voor**</span><span class="sxs-lookup"><span data-stu-id="c1b02-528">**Used for**</span></span>|  
    |-|-|    
    |<span data-ttu-id="c1b02-529">HOOFDLETTERS</span><span class="sxs-lookup"><span data-stu-id="c1b02-529">UPPERCASE</span></span>|<span data-ttu-id="c1b02-530">Niet-hoofdlettergevoelige trefwoorden.</span><span class="sxs-lookup"><span data-stu-id="c1b02-530">Case-insensitive keywords.</span></span>|  
    |<span data-ttu-id="c1b02-531">kleine letters</span><span class="sxs-lookup"><span data-stu-id="c1b02-531">lowercase</span></span>|<span data-ttu-id="c1b02-532">Trefwoorden hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="c1b02-532">Case-sensitive keywords.</span></span>|  
    |<span data-ttu-id="c1b02-533">\<nonterminal ></span><span class="sxs-lookup"><span data-stu-id="c1b02-533">\<nonterminal></span></span>|<span data-ttu-id="c1b02-534">Niet-eindigende, die is gedefinieerd afzonderlijk.</span><span class="sxs-lookup"><span data-stu-id="c1b02-534">Nonterminal, defined separately.</span></span>|  
    |<span data-ttu-id="c1b02-535">\<nonterminal >:: =</span><span class="sxs-lookup"><span data-stu-id="c1b02-535">\<nonterminal> ::=</span></span>|<span data-ttu-id="c1b02-536">De definitie van de syntaxis van Hallo nonterminal.</span><span class="sxs-lookup"><span data-stu-id="c1b02-536">Syntax definition of hello nonterminal.</span></span>|  
    |<span data-ttu-id="c1b02-537">other_terminal</span><span class="sxs-lookup"><span data-stu-id="c1b02-537">other_terminal</span></span>|<span data-ttu-id="c1b02-538">Terminal (token) in de woorden in detail beschreven.</span><span class="sxs-lookup"><span data-stu-id="c1b02-538">Terminal (token), described in detail in words.</span></span>|  
    |<span data-ttu-id="c1b02-539">ID</span><span class="sxs-lookup"><span data-stu-id="c1b02-539">identifier</span></span>|<span data-ttu-id="c1b02-540">ID.</span><span class="sxs-lookup"><span data-stu-id="c1b02-540">Identifier.</span></span> <span data-ttu-id="c1b02-541">Kan de volgende tekens bevatten: a-z A-Z 0-9 _First teken mag niet een cijfer.</span><span class="sxs-lookup"><span data-stu-id="c1b02-541">Allows following characters only: a-z A-Z 0-9 _First character cannot be a digit.</span></span>|  
    |<span data-ttu-id="c1b02-542">'tekenreeks'</span><span class="sxs-lookup"><span data-stu-id="c1b02-542">"string"</span></span>|<span data-ttu-id="c1b02-543">Tekenreeks tussen aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="c1b02-543">Quoted string.</span></span> <span data-ttu-id="c1b02-544">Hiermee kunt een geldige tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="c1b02-544">Allows any valid string.</span></span> <span data-ttu-id="c1b02-545">Zie de beschrijving van een string_literal.</span><span class="sxs-lookup"><span data-stu-id="c1b02-545">See description of a string_literal.</span></span>|  
    |<span data-ttu-id="c1b02-546">"symbool"</span><span class="sxs-lookup"><span data-stu-id="c1b02-546">'symbol'</span></span>|<span data-ttu-id="c1b02-547">Letterlijke symbool die deel uitmaakt van het Hallo-syntaxis.</span><span class="sxs-lookup"><span data-stu-id="c1b02-547">Literal symbol which is part of hello syntax.</span></span>|  
    |<span data-ttu-id="c1b02-548">&#124; (verticale balk)</span><span class="sxs-lookup"><span data-stu-id="c1b02-548">&#124; (vertical bar)</span></span>|<span data-ttu-id="c1b02-549">Alternatieven voor de syntaxis van de items.</span><span class="sxs-lookup"><span data-stu-id="c1b02-549">Alternatives for syntax items.</span></span> <span data-ttu-id="c1b02-550">U kunt slechts één van de opgegeven Hallo-items.</span><span class="sxs-lookup"><span data-stu-id="c1b02-550">You can use only one of hello items specified.</span></span>|  
    |<span data-ttu-id="c1b02-551">[] /(brackets)</span><span class="sxs-lookup"><span data-stu-id="c1b02-551">[ ] /(brackets)</span></span>|<span data-ttu-id="c1b02-552">Vierkante haken plaatst u een of meer optionele items.</span><span class="sxs-lookup"><span data-stu-id="c1b02-552">Brackets enclose one or more optional items.</span></span>|  
    |<span data-ttu-id="c1b02-553">[,.. .n]</span><span class="sxs-lookup"><span data-stu-id="c1b02-553">[ ,...n ]</span></span>|<span data-ttu-id="c1b02-554">Geeft aan Hallo voorgaande item herhaalde n het aantal keren dat kan worden.</span><span class="sxs-lookup"><span data-stu-id="c1b02-554">Indicates hello preceding item can be repeated n number of times.</span></span> <span data-ttu-id="c1b02-555">Hallo-instanties worden gescheiden door komma's.</span><span class="sxs-lookup"><span data-stu-id="c1b02-555">hello occurrences are separated by commas.</span></span>|  
    |<span data-ttu-id="c1b02-556">[.. .n]</span><span class="sxs-lookup"><span data-stu-id="c1b02-556">[ ...n ]</span></span>|<span data-ttu-id="c1b02-557">Geeft aan Hallo voorgaande item herhaalde n het aantal keren dat kan worden.</span><span class="sxs-lookup"><span data-stu-id="c1b02-557">Indicates hello preceding item can be repeated n number of times.</span></span> <span data-ttu-id="c1b02-558">Hallo-instanties worden gescheiden door spaties.</span><span class="sxs-lookup"><span data-stu-id="c1b02-558">hello occurrences are separated by blanks.</span></span>|  
  
##  <span data-ttu-id="c1b02-559"><a name="bk_built_in_functions"></a>Ingebouwde functies</span><span class="sxs-lookup"><span data-stu-id="c1b02-559"><a name="bk_built_in_functions"></a> Built-in functions</span></span>  
 <span data-ttu-id="c1b02-560">Azure Cosmos DB biedt veel ingebouwde SQL-functies.</span><span class="sxs-lookup"><span data-stu-id="c1b02-560">Azure Cosmos DB provides many built-in SQL functions.</span></span> <span data-ttu-id="c1b02-561">Hallo categorieën van ingebouwde functies worden hieronder vermeld.</span><span class="sxs-lookup"><span data-stu-id="c1b02-561">hello categories of built-in functions are listed below.</span></span>  
  
|<span data-ttu-id="c1b02-562">Functie</span><span class="sxs-lookup"><span data-stu-id="c1b02-562">Function</span></span>|<span data-ttu-id="c1b02-563">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c1b02-563">Description</span></span>|  
|--------------|-----------------|  
|[<span data-ttu-id="c1b02-564">Wiskundige functies</span><span class="sxs-lookup"><span data-stu-id="c1b02-564">Mathematical functions</span></span>](#bk_mathematical_functions)|<span data-ttu-id="c1b02-565">Hallo wiskundige functies elke uitvoeren van een berekening, meestal op basis van de invoerwaarden die zijn opgegeven als argumenten en een numerieke waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="c1b02-565">hello mathematical functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>|  
|[<span data-ttu-id="c1b02-566">Controle van de functies van het type</span><span class="sxs-lookup"><span data-stu-id="c1b02-566">Type checking functions</span></span>](#bk_type_checking_functions)|<span data-ttu-id="c1b02-567">Hallo type controleren of functies kunnen u toocheck Hallo-type van een expressie in SQL-query's.</span><span class="sxs-lookup"><span data-stu-id="c1b02-567">hello type checking functions allow you toocheck hello type of an expression within SQL queries.</span></span>|  
|[<span data-ttu-id="c1b02-568">Tekenreeksfuncties</span><span class="sxs-lookup"><span data-stu-id="c1b02-568">String functions</span></span>](#bk_string_functions)|<span data-ttu-id="c1b02-569">Hallo tekenreeksfuncties een bewerking uitvoeren op een tekenreekswaarde van de invoer en een tekenreeks, numerieke of Booleaanse waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="c1b02-569">hello string functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>|  
|[<span data-ttu-id="c1b02-570">Matrixfuncties</span><span class="sxs-lookup"><span data-stu-id="c1b02-570">Array functions</span></span>](#bk_array_functions)|<span data-ttu-id="c1b02-571">Hallo matrixfuncties uitvoeren voor een bewerking in een matrix invoerwaarde en keer terug numerieke, de waarde voor Boole-waarde of een matrix.</span><span class="sxs-lookup"><span data-stu-id="c1b02-571">hello array functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span>|  
|[<span data-ttu-id="c1b02-572">Ruimtelijke functies</span><span class="sxs-lookup"><span data-stu-id="c1b02-572">Spatial functions</span></span>](#bk_spatial_functions)|<span data-ttu-id="c1b02-573">Hallo ruimtelijke functies een bewerking uitvoeren op een invoerwaarde ruimtelijke object en een numeriek gegevenstype of Booleaanse waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="c1b02-573">hello spatial functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>|  
  
###  <span data-ttu-id="c1b02-574"><a name="bk_mathematical_functions"></a>Wiskundige functies</span><span class="sxs-lookup"><span data-stu-id="c1b02-574"><a name="bk_mathematical_functions"></a> Mathematical functions</span></span>  
 <span data-ttu-id="c1b02-575">Hallo volgende functies een berekening uitgevoerd, meestal op basis van de invoerwaarden die zijn opgegeven als argumenten en een numerieke waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="c1b02-575">hello following functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="c1b02-576">ABS</span><span class="sxs-lookup"><span data-stu-id="c1b02-576">ABS</span></span>](#bk_abs)|[<span data-ttu-id="c1b02-577">BOOGCOS</span><span class="sxs-lookup"><span data-stu-id="c1b02-577">ACOS</span></span>](#bk_acos)|[<span data-ttu-id="c1b02-578">ASIN</span><span class="sxs-lookup"><span data-stu-id="c1b02-578">ASIN</span></span>](#bk_asin)|  
|[<span data-ttu-id="c1b02-579">BOOGTAN</span><span class="sxs-lookup"><span data-stu-id="c1b02-579">ATAN</span></span>](#bk_atan)|[<span data-ttu-id="c1b02-580">ATN2</span><span class="sxs-lookup"><span data-stu-id="c1b02-580">ATN2</span></span>](#bk_atn2)|[<span data-ttu-id="c1b02-581">MAXIMUM</span><span class="sxs-lookup"><span data-stu-id="c1b02-581">CEILING</span></span>](#bk_ceiling)|  
|[<span data-ttu-id="c1b02-582">CO 'S</span><span class="sxs-lookup"><span data-stu-id="c1b02-582">COS</span></span>](#bk_cos)|[<span data-ttu-id="c1b02-583">COT</span><span class="sxs-lookup"><span data-stu-id="c1b02-583">COT</span></span>](#bk_cot)|[<span data-ttu-id="c1b02-584">GRADEN</span><span class="sxs-lookup"><span data-stu-id="c1b02-584">DEGREES</span></span>](#bk_degrees)|  
|[<span data-ttu-id="c1b02-585">EXP</span><span class="sxs-lookup"><span data-stu-id="c1b02-585">EXP</span></span>](#bk_exp)|[<span data-ttu-id="c1b02-586">FLOOR</span><span class="sxs-lookup"><span data-stu-id="c1b02-586">FLOOR</span></span>](#bk_floor)|[<span data-ttu-id="c1b02-587">LOGBOEK</span><span class="sxs-lookup"><span data-stu-id="c1b02-587">LOG</span></span>](#bk_log)|  
|[<span data-ttu-id="c1b02-588">LOG10</span><span class="sxs-lookup"><span data-stu-id="c1b02-588">LOG10</span></span>](#bk_log10)|[<span data-ttu-id="c1b02-589">PI</span><span class="sxs-lookup"><span data-stu-id="c1b02-589">PI</span></span>](#bk_pi)|[<span data-ttu-id="c1b02-590">ENERGIEBEHEER</span><span class="sxs-lookup"><span data-stu-id="c1b02-590">POWER</span></span>](#bk_power)|  
|[<span data-ttu-id="c1b02-591">RADIALEN</span><span class="sxs-lookup"><span data-stu-id="c1b02-591">RADIANS</span></span>](#bk_radians)|[<span data-ttu-id="c1b02-592">AFRONDEN</span><span class="sxs-lookup"><span data-stu-id="c1b02-592">ROUND</span></span>](#bk_round)|[<span data-ttu-id="c1b02-593">SIN</span><span class="sxs-lookup"><span data-stu-id="c1b02-593">SIN</span></span>](#bk_sin)|  
|[<span data-ttu-id="c1b02-594">SQRT</span><span class="sxs-lookup"><span data-stu-id="c1b02-594">SQRT</span></span>](#bk_sqrt)|[<span data-ttu-id="c1b02-595">VIERKANTE</span><span class="sxs-lookup"><span data-stu-id="c1b02-595">SQUARE</span></span>](#bk_square)|[<span data-ttu-id="c1b02-596">AANMELDING</span><span class="sxs-lookup"><span data-stu-id="c1b02-596">SIGN</span></span>](#bk_sign)|  
|[<span data-ttu-id="c1b02-597">TAN</span><span class="sxs-lookup"><span data-stu-id="c1b02-597">TAN</span></span>](#bk_tan)|[<span data-ttu-id="c1b02-598">GEHEEL</span><span class="sxs-lookup"><span data-stu-id="c1b02-598">TRUNC</span></span>](#bk_trunc)||  
  
####  <span data-ttu-id="c1b02-599"><a name="bk_abs"></a>ABS</span><span class="sxs-lookup"><span data-stu-id="c1b02-599"><a name="bk_abs"></a> ABS</span></span>  
 <span data-ttu-id="c1b02-600">Retourneert Hallo absolute (positieve) waarde Hallo opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-600">Returns hello absolute (positive) value of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-601">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-601">**Syntax**</span></span>  
  
```  
ABS (<numeric_expression>)  
```  
  
 <span data-ttu-id="c1b02-602">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-602">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="c1b02-603">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-603">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-604">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-604">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-605">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-605">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-606">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-606">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-607">Hallo ziet volgende voorbeeld Hallo resultaten van het gebruik van de functie ABS Hallo op drie verschillende aantallen.</span><span class="sxs-lookup"><span data-stu-id="c1b02-607">hello following example shows hello results of using hello ABS function on three different numbers.</span></span>  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 <span data-ttu-id="c1b02-608">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-608">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <span data-ttu-id="c1b02-609"><a name="bk_acos"></a>BOOGCOS</span><span class="sxs-lookup"><span data-stu-id="c1b02-609"><a name="bk_acos"></a> ACOS</span></span>  
 <span data-ttu-id="c1b02-610">Retourneert Hallo hoek in radialen, waarvan de cosinus is Hallo opgegeven numerieke expressie. ook wel de boogcosinus genoemd.</span><span class="sxs-lookup"><span data-stu-id="c1b02-610">Returns hello angle, in radians, whose cosine is hello specified numeric expression; also called arccosine.</span></span>  
  
 <span data-ttu-id="c1b02-611">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-611">**Syntax**</span></span>  
  
```  
ACOS(<numeric_expression>)  
```  
  
 <span data-ttu-id="c1b02-612">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-612">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="c1b02-613">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-613">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-614">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-614">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-615">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-615">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-616">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-616">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-617">Hallo retourneert volgende voorbeeld Hallo BOOGCOS van-1.</span><span class="sxs-lookup"><span data-stu-id="c1b02-617">hello following example returns hello ACOS of -1.</span></span>  
  
```  
SELECT ACOS(-1)  
```  
  
 <span data-ttu-id="c1b02-618">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-618">Here is hello result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="c1b02-619"><a name="bk_asin"></a>ASIN</span><span class="sxs-lookup"><span data-stu-id="c1b02-619"><a name="bk_asin"></a> ASIN</span></span>  
 <span data-ttu-id="c1b02-620">Retourneert Hallo hoek in radialen, waarvan de sinus Hallo is opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-620">Returns hello angle, in radians, whose sine is hello specified numeric expression.</span></span> <span data-ttu-id="c1b02-621">Dit wordt ook boogsinus genoemd.</span><span class="sxs-lookup"><span data-stu-id="c1b02-621">This is also called arcsine.</span></span>  
  
 <span data-ttu-id="c1b02-622">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-622">**Syntax**</span></span>  
  
```  
ASIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="c1b02-623">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-623">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="c1b02-624">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-624">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-625">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-625">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-626">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-626">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-627">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-627">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-628">Hallo retourneert volgende voorbeeld Hallo ASIN van-1.</span><span class="sxs-lookup"><span data-stu-id="c1b02-628">hello following example returns hello ASIN of -1.</span></span>  
  
```  
SELECT ASIN(-1)  
```  
  
 <span data-ttu-id="c1b02-629">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-629">Here is hello result set.</span></span>  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <span data-ttu-id="c1b02-630"><a name="bk_atan"></a>BOOGTAN</span><span class="sxs-lookup"><span data-stu-id="c1b02-630"><a name="bk_atan"></a> ATAN</span></span>  
 <span data-ttu-id="c1b02-631">Retourneert Hallo hoek in radialen, waarvan de tangens Hallo is opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-631">Returns hello angle, in radians, whose tangent is hello specified numeric expression.</span></span> <span data-ttu-id="c1b02-632">Dit wordt ook arctangens genoemd.</span><span class="sxs-lookup"><span data-stu-id="c1b02-632">This is also called arctangent.</span></span>  
  
 <span data-ttu-id="c1b02-633">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-633">**Syntax**</span></span>  
  
```  
ATAN(<numeric_expression>)  
```  
  
 <span data-ttu-id="c1b02-634">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-634">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="c1b02-635">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-635">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-636">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-636">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-637">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-637">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-638">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-638">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-639">Hallo volgende voorbeeld retourneert Hallo BOOGTAN Hallo waarde opgegeven.</span><span class="sxs-lookup"><span data-stu-id="c1b02-639">hello following example returns hello ATAN of hello specified value.</span></span>  
  
```  
SELECT ATAN(-45.01)  
```  
  
 <span data-ttu-id="c1b02-640">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-640">Here is hello result set.</span></span>  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <span data-ttu-id="c1b02-641"><a name="bk_atn2"></a>ATN2</span><span class="sxs-lookup"><span data-stu-id="c1b02-641"><a name="bk_atn2"></a> ATN2</span></span>  
 <span data-ttu-id="c1b02-642">Retourneert de hoofdsom Hallo van Hallo arctangens van y / x, uitgedrukt in radialen.</span><span class="sxs-lookup"><span data-stu-id="c1b02-642">Returns hello principal value of hello arc tangent of y/x, expressed in radians.</span></span>  
  
 <span data-ttu-id="c1b02-643">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-643">**Syntax**</span></span>  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 <span data-ttu-id="c1b02-644">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-644">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="c1b02-645">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-645">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-646">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-646">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-647">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-647">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-648">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-648">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-649">Hallo volgende voorbeeld wordt berekend Hallo ATN2 voor Hallo opgegeven x en y onderdelen.</span><span class="sxs-lookup"><span data-stu-id="c1b02-649">hello following example calculates hello ATN2 for hello specified x and y components.</span></span>  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 <span data-ttu-id="c1b02-650">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-650">Here is hello result set.</span></span>  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <span data-ttu-id="c1b02-651"><a name="bk_ceiling"></a>MAXIMUM</span><span class="sxs-lookup"><span data-stu-id="c1b02-651"><a name="bk_ceiling"></a> CEILING</span></span>  
 <span data-ttu-id="c1b02-652">Retourneert Hallo kleinste geheel getal groter dan of gelijk zijn aan om Hallo opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-652">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-653">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-653">**Syntax**</span></span>  
  
```  
CEILING (<numeric_expression>)  
```  
  
 <span data-ttu-id="c1b02-654">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-654">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="c1b02-655">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-655">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-656">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-656">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-657">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-657">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-658">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-658">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-659">Hallo volgende voorbeeld toont positieve numerieke negatief, en nulwaarden met Hallo functie CEILING.</span><span class="sxs-lookup"><span data-stu-id="c1b02-659">hello following example shows positive numeric, negative, and zero values with hello CEILING function.</span></span>  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 <span data-ttu-id="c1b02-660">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-660">Here is hello result set.</span></span>  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <span data-ttu-id="c1b02-661"><a name="bk_cos"></a>CO 'S</span><span class="sxs-lookup"><span data-stu-id="c1b02-661"><a name="bk_cos"></a> COS</span></span>  
 <span data-ttu-id="c1b02-662">Retourneert Hallo trigonometrische cosinus van Hallo hoek aangeduid in radialen, in Hallo opgegeven expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-662">Returns hello trigonometric cosine of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="c1b02-663">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-663">**Syntax**</span></span>  
  
```  
COS(<numeric_expression>)  
```  
  
 <span data-ttu-id="c1b02-664">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-664">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="c1b02-665">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-665">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-666">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-666">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-667">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-667">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-668">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-668">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-669">Hallo volgt berekent Hallo CO Hallo opgegeven hoek.</span><span class="sxs-lookup"><span data-stu-id="c1b02-669">hello following example calculates hello COS of hello specified angle.</span></span>  
  
```  
SELECT COS(14.78)  
```  
  
 <span data-ttu-id="c1b02-670">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-670">Here is hello result set.</span></span>  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <span data-ttu-id="c1b02-671"><a name="bk_cot"></a>COT</span><span class="sxs-lookup"><span data-stu-id="c1b02-671"><a name="bk_cot"></a> COT</span></span>  
 <span data-ttu-id="c1b02-672">Retourneert Hallo trigonometrische cotangens van Hallo hoek aangeduid in radialen, opgegeven in Hallo numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-672">Returns hello trigonometric cotangent of hello specified angle, in radians, in hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-673">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-673">**Syntax**</span></span>  
  
```  
COT(<numeric_expression>)  
```  
  
 <span data-ttu-id="c1b02-674">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-674">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="c1b02-675">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-675">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-676">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-676">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-677">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-677">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-678">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-678">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-679">Hallo volgt berekent Hallo COT van Hallo opgegeven hoek.</span><span class="sxs-lookup"><span data-stu-id="c1b02-679">hello following example calculates hello COT of hello specified angle.</span></span>  
  
```  
SELECT COT(124.1332)  
```  
  
 <span data-ttu-id="c1b02-680">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-680">Here is hello result set.</span></span>  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <span data-ttu-id="c1b02-681"><a name="bk_degrees"></a>GRADEN</span><span class="sxs-lookup"><span data-stu-id="c1b02-681"><a name="bk_degrees"></a> DEGREES</span></span>  
 <span data-ttu-id="c1b02-682">Retourneert Hallo bijbehorende hoek in graden voor een hoek aangeduid in radialen.</span><span class="sxs-lookup"><span data-stu-id="c1b02-682">Returns hello corresponding angle in degrees for an angle specified in radians.</span></span>  
  
 <span data-ttu-id="c1b02-683">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-683">**Syntax**</span></span>  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 <span data-ttu-id="c1b02-684">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-684">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="c1b02-685">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-685">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-686">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-686">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-687">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-687">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-688">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-688">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-689">Hallo volgende voorbeeld wordt het aantal graden Hallo in een hoek van radialen PI/2.</span><span class="sxs-lookup"><span data-stu-id="c1b02-689">hello following example returns hello number of degrees in an angle of PI/2 radians.</span></span>  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 <span data-ttu-id="c1b02-690">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-690">Here is hello result set.</span></span>  
  
```  
[{"$1": 90}]  
```  
  
####  <span data-ttu-id="c1b02-691"><a name="bk_floor"></a>FLOOR</span><span class="sxs-lookup"><span data-stu-id="c1b02-691"><a name="bk_floor"></a> FLOOR</span></span>  
 <span data-ttu-id="c1b02-692">Retourneert de grootste integer Hallo kleiner dan of gelijk toohello numerieke expressie opgegeven.</span><span class="sxs-lookup"><span data-stu-id="c1b02-692">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-693">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-693">**Syntax**</span></span>  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 <span data-ttu-id="c1b02-694">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-694">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="c1b02-695">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-695">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-696">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-696">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-697">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-697">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-698">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-698">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-699">Hallo volgende voorbeeld toont positieve numerieke negatief, en nulwaarden met Hallo functie FLOOR.</span><span class="sxs-lookup"><span data-stu-id="c1b02-699">hello following example shows positive numeric, negative, and zero values with hello FLOOR function.</span></span>  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 <span data-ttu-id="c1b02-700">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-700">Here is hello result set.</span></span>  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <span data-ttu-id="c1b02-701"><a name="bk_exp"></a>EXP</span><span class="sxs-lookup"><span data-stu-id="c1b02-701"><a name="bk_exp"></a> EXP</span></span>  
 <span data-ttu-id="c1b02-702">Retourneert Hallo exponentiële waarde Hallo opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-702">Returns hello exponential value of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-703">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-703">**Syntax**</span></span>  
  
```  
EXP (<numeric_expression>)  
```  
  
 <span data-ttu-id="c1b02-704">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-704">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="c1b02-705">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-705">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-706">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-706">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-707">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-707">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-708">**Opmerkingen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-708">**Remarks**</span></span>  
  
 <span data-ttu-id="c1b02-709">Hallo constante **e** (2.718281...) is Hallo grondtal van de natuurlijke logaritme.</span><span class="sxs-lookup"><span data-stu-id="c1b02-709">hello constant **e** (2.718281…), is hello base of natural logarithms.</span></span>  
  
 <span data-ttu-id="c1b02-710">Hallo exponent van een getal is Hallo constante **e** toohello macht van Hallo getal gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="c1b02-710">hello exponent of a number is hello constant **e** raised toohello power of hello number.</span></span> <span data-ttu-id="c1b02-711">Bijvoorbeeld EXP(1.0) e = ^ 1.0 = 2.71828182845905 en EXP(10) e = ^ 10 = 22026.4657948067.</span><span class="sxs-lookup"><span data-stu-id="c1b02-711">For example EXP(1.0) = e^1.0 = 2.71828182845905 and EXP(10) = e^10 = 22026.4657948067.</span></span>  
  
 <span data-ttu-id="c1b02-712">Hallo exponentiële van Hallo natuurlijke logaritme van een getal is Hallo getal zichzelf: EXP (LOGBOEKREGISTRATIE (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="c1b02-712">hello exponential of hello natural logarithm of a number is hello number itself: EXP (LOG (n)) = n.</span></span> <span data-ttu-id="c1b02-713">En Hallo natuurlijke logaritme van een getal exponentiële Hallo Hallo getal zichzelf: logboek (EXP (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="c1b02-713">And hello natural logarithm of hello exponential of a number is hello number itself: LOG (EXP (n)) = n.</span></span>  
  
 <span data-ttu-id="c1b02-714">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-714">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-715">Hallo volgende voorbeeld wordt een variabele gedeclareerd en retourneert Hallo exponentiële waarde van Hallo opgegeven variabele (10).</span><span class="sxs-lookup"><span data-stu-id="c1b02-715">hello following example declares a variable and returns hello exponential value of hello specified variable (10).</span></span>  
  
```  
SELECT EXP(10)  
```  
  
 <span data-ttu-id="c1b02-716">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-716">Here is hello result set.</span></span>  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 <span data-ttu-id="c1b02-717">Hallo retourneert volgende voorbeeld Hallo exponentiële waarde van Hallo natuurlijke logaritme van 20 en Hallo natuurlijke logaritme van Hallo exponentiële van 20.</span><span class="sxs-lookup"><span data-stu-id="c1b02-717">hello following example returns hello exponential value of hello natural logarithm of 20 and hello natural logarithm of hello exponential of 20.</span></span> <span data-ttu-id="c1b02-718">Omdat deze functies inverse functies van elkaar, Hallo retourwaarde zijn afgeronde voor drijvende komma berekening in beide gevallen is 20.</span><span class="sxs-lookup"><span data-stu-id="c1b02-718">Because these functions are inverse functions of one another, hello return value with rounding for floating point math in both cases is 20.</span></span>  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 <span data-ttu-id="c1b02-719">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-719">Here is hello result set.</span></span>  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <span data-ttu-id="c1b02-720"><a name="bk_log"></a>LOGBOEK</span><span class="sxs-lookup"><span data-stu-id="c1b02-720"><a name="bk_log"></a> LOG</span></span>  
 <span data-ttu-id="c1b02-721">Retourneert Hallo natuurlijke logaritme van Hallo opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-721">Returns hello natural logarithm of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-722">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-722">**Syntax**</span></span>  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 <span data-ttu-id="c1b02-723">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-723">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="c1b02-724">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-724">Is a numeric expression.</span></span>  
  
-   `base`  
  
     <span data-ttu-id="c1b02-725">Optionele numerieke argument dat Hallo voor Hallo logaritme ingesteld.</span><span class="sxs-lookup"><span data-stu-id="c1b02-725">Optional numeric argument that sets hello base for hello logarithm.</span></span>  
  
 <span data-ttu-id="c1b02-726">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-726">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-727">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-727">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-728">**Opmerkingen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-728">**Remarks**</span></span>  
  
 <span data-ttu-id="c1b02-729">Standaard retourneert LOG() Hallo natuurlijke logaritme.</span><span class="sxs-lookup"><span data-stu-id="c1b02-729">By default, LOG() returns hello natural logarithm.</span></span> <span data-ttu-id="c1b02-730">U kunt Hallo base Hallo logaritme tooanother waarde wijzigen met behulp van Hallo optionele base-parameter.</span><span class="sxs-lookup"><span data-stu-id="c1b02-730">You can change hello base of hello logarithm tooanother value by using hello optional base parameter.</span></span>  
  
 <span data-ttu-id="c1b02-731">Hallo natuurlijke logaritme is Hallo logaritme toohello base **e**, waarbij **e** een irrational constante ongeveer gelijk too2.718281828 is.</span><span class="sxs-lookup"><span data-stu-id="c1b02-731">hello natural logarithm is hello logarithm toohello base **e**, where **e** is an irrational constant approximately equal too2.718281828.</span></span>  
  
 <span data-ttu-id="c1b02-732">Hallo natuurlijke logaritme van Hallo exponentiële van een getal is Hallo getal zichzelf: logboek (EXP (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="c1b02-732">hello natural logarithm of hello exponential of a number is hello number itself: LOG( EXP( n ) ) = n.</span></span> <span data-ttu-id="c1b02-733">En exponentiële van Hallo natuurlijke logaritme van een getal Hallo Hallo getal zichzelf: EXP (LOGBOEKREGISTRATIE (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="c1b02-733">And hello exponential of hello natural logarithm of a number is hello number itself: EXP( LOG( n ) ) = n.</span></span>  
  
 <span data-ttu-id="c1b02-734">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-734">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-735">Hallo volgende voorbeeld wordt een variabele gedeclareerd en retourneert Hallo logaritme waarde van Hallo opgegeven variabele (10).</span><span class="sxs-lookup"><span data-stu-id="c1b02-735">hello following example declares a variable and returns hello logarithm value of hello specified variable (10).</span></span>  
  
```  
SELECT LOG(10)  
```  
  
 <span data-ttu-id="c1b02-736">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-736">Here is hello result set.</span></span>  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 <span data-ttu-id="c1b02-737">Hallo volgende voorbeeld wordt berekend Hallo logboek voor Hallo exponent van een getal.</span><span class="sxs-lookup"><span data-stu-id="c1b02-737">hello following example calculates hello LOG for hello exponent of a number.</span></span>  
  
```  
SELECT EXP(LOG(10))  
```  
  
 <span data-ttu-id="c1b02-738">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-738">Here is hello result set.</span></span>  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <span data-ttu-id="c1b02-739"><a name="bk_log10"></a>LOG10</span><span class="sxs-lookup"><span data-stu-id="c1b02-739"><a name="bk_log10"></a> LOG10</span></span>  
 <span data-ttu-id="c1b02-740">Retourneert Hallo logaritme met grondtal 10 van Hallo opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-740">Returns hello base-10 logarithm of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-741">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-741">**Syntax**</span></span>  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 <span data-ttu-id="c1b02-742">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-742">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="c1b02-743">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-743">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-744">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-744">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-745">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-745">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-746">**Opmerkingen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-746">**Remarks**</span></span>  
  
 <span data-ttu-id="c1b02-747">Hallo LOG10 en functies van POWER worden omgekeerd gerelateerde tooone een andere.</span><span class="sxs-lookup"><span data-stu-id="c1b02-747">hello LOG10 and POWER functions are inversely related tooone another.</span></span> <span data-ttu-id="c1b02-748">Bijvoorbeeld 10 ^ LOG10(n) = n.</span><span class="sxs-lookup"><span data-stu-id="c1b02-748">For example, 10 ^ LOG10(n) = n.</span></span>  
  
 <span data-ttu-id="c1b02-749">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-749">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-750">Hallo volgende voorbeeld wordt een variabele gedeclareerd en retourneert Hallo LOG10 waarde van Hallo opgegeven variabele (100).</span><span class="sxs-lookup"><span data-stu-id="c1b02-750">hello following example declares a variable and returns hello LOG10 value of hello specified variable (100).</span></span>  
  
```  
SELECT LOG10(100)  
```  
  
 <span data-ttu-id="c1b02-751">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-751">Here is hello result set.</span></span>  
  
```  
[{$1: 2}]  
```  
  
####  <span data-ttu-id="c1b02-752"><a name="bk_pi"></a>PI</span><span class="sxs-lookup"><span data-stu-id="c1b02-752"><a name="bk_pi"></a> PI</span></span>  
 <span data-ttu-id="c1b02-753">Retourneert Hallo constante waarde van PI.</span><span class="sxs-lookup"><span data-stu-id="c1b02-753">Returns hello constant value of PI.</span></span>  
  
 <span data-ttu-id="c1b02-754">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-754">**Syntax**</span></span>  
  
```  
PI ()  
```  
  
 <span data-ttu-id="c1b02-755">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-755">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="c1b02-756">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-756">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-757">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-757">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-758">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-758">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-759">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-759">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-760">Hallo retourneert volgende voorbeeld Hallo-waarde van PI.</span><span class="sxs-lookup"><span data-stu-id="c1b02-760">hello following example returns hello value of PI.</span></span>  
  
```  
SELECT PI()  
```  
  
 <span data-ttu-id="c1b02-761">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-761">Here is hello result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="c1b02-762"><a name="bk_power"></a>ENERGIEBEHEER</span><span class="sxs-lookup"><span data-stu-id="c1b02-762"><a name="bk_power"></a> POWER</span></span>  
 <span data-ttu-id="c1b02-763">Retourneert de waarde van de opgegeven Hallo Hallo expressie toohello opgegeven macht.</span><span class="sxs-lookup"><span data-stu-id="c1b02-763">Returns hello value of hello specified expression toohello specified power.</span></span>  
  
 <span data-ttu-id="c1b02-764">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-764">**Syntax**</span></span>  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 <span data-ttu-id="c1b02-765">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-765">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="c1b02-766">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-766">Is a numeric expression.</span></span>  
  
-   `y`  
  
     <span data-ttu-id="c1b02-767">Hallo power toowhich tooraise is `numeric_expression`.</span><span class="sxs-lookup"><span data-stu-id="c1b02-767">Is hello power toowhich tooraise `numeric_expression`.</span></span>  
  
 <span data-ttu-id="c1b02-768">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-768">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-769">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-769">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-770">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-770">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-771">Hallo volgende voorbeeld laat zien verhogen van een aantal toohello macht 3 (Hallo kubus van Hallo getal).</span><span class="sxs-lookup"><span data-stu-id="c1b02-771">hello following example demonstrates raising a number toohello power of 3 (hello cube of hello number).</span></span>  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 <span data-ttu-id="c1b02-772">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-772">Here is hello result set.</span></span>  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <span data-ttu-id="c1b02-773"><a name="bk_radians"></a>RADIALEN</span><span class="sxs-lookup"><span data-stu-id="c1b02-773"><a name="bk_radians"></a> RADIANS</span></span>  
 <span data-ttu-id="c1b02-774">Retourneert radialen wanneer een numerieke expressie, in graden wordt ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="c1b02-774">Returns radians when a numeric expression, in degrees, is entered.</span></span>  
  
 <span data-ttu-id="c1b02-775">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-775">**Syntax**</span></span>  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 <span data-ttu-id="c1b02-776">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-776">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="c1b02-777">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-777">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-778">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-778">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-779">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-779">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-780">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-780">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-781">Hallo volgende voorbeeld duurt enkele hoeken als invoer en de bijbehorende Radiaal waarden retourneert.</span><span class="sxs-lookup"><span data-stu-id="c1b02-781">hello following example takes a few angles as input and returns their corresponding radian values.</span></span>  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 <span data-ttu-id="c1b02-782">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-782">Here is hello result set.</span></span>  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <span data-ttu-id="c1b02-783"><a name="bk_round"></a>AFRONDEN</span><span class="sxs-lookup"><span data-stu-id="c1b02-783"><a name="bk_round"></a> ROUND</span></span>  
 <span data-ttu-id="c1b02-784">Retourneert een numerieke waarde afgeronde toohello dichtstbijzijnde integer-waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-784">Returns a numeric value, rounded toohello closest integer value.</span></span>  
  
 <span data-ttu-id="c1b02-785">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-785">**Syntax**</span></span>  
  
```  
ROUND(<numeric_expression>)  
```  
  
 <span data-ttu-id="c1b02-786">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-786">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="c1b02-787">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-787">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-788">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-788">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-789">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-789">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-790">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-790">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-791">Hallo volgende voorbeeld wordt afgerond Hallo positieve en negatieve getallen toohello dichtstbijzijnde integer te volgen.</span><span class="sxs-lookup"><span data-stu-id="c1b02-791">hello following example rounds hello following positive and negative numbers toohello nearest integer.</span></span>  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 <span data-ttu-id="c1b02-792">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-792">Here is hello result set.</span></span>  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <span data-ttu-id="c1b02-793"><a name="bk_sign"></a>AANMELDING</span><span class="sxs-lookup"><span data-stu-id="c1b02-793"><a name="bk_sign"></a> SIGN</span></span>  
 <span data-ttu-id="c1b02-794">Retourneert Hallo positieve (+ 1), nul (0) of minteken (-1) Hallo opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-794">Returns hello positive (+1), zero (0), or negative (-1) sign of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-795">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-795">**Syntax**</span></span>  
  
```  
SIGN(<numeric_expression>)  
```  
  
 <span data-ttu-id="c1b02-796">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-796">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="c1b02-797">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-797">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-798">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-798">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-799">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-799">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-800">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-800">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-801">Hallo volgende voorbeeld wordt Hallo aanmelding waarden van de getallen uit too2-2.</span><span class="sxs-lookup"><span data-stu-id="c1b02-801">hello following example returns hello SIGN values of numbers from -2 too2.</span></span>  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 <span data-ttu-id="c1b02-802">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-802">Here is hello result set.</span></span>  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <span data-ttu-id="c1b02-803"><a name="bk_sin"></a>SIN</span><span class="sxs-lookup"><span data-stu-id="c1b02-803"><a name="bk_sin"></a> SIN</span></span>  
 <span data-ttu-id="c1b02-804">Retourneert Hallo trigonometrische sinus van Hallo hoek aangeduid in radialen, in Hallo opgegeven expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-804">Returns hello trigonometric sine of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="c1b02-805">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-805">**Syntax**</span></span>  
  
```  
SIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="c1b02-806">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-806">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="c1b02-807">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-807">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-808">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-808">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-809">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-809">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-810">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-810">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-811">Hallo voorbeeld te volgen berekent Hallo SIN van Hallo opgegeven hoek.</span><span class="sxs-lookup"><span data-stu-id="c1b02-811">hello following example calculates hello SIN of hello specified angle.</span></span>  
  
```  
SELECT SIN(45.175643)  
```  
  
 <span data-ttu-id="c1b02-812">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-812">Here is hello result set.</span></span>  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <span data-ttu-id="c1b02-813"><a name="bk_sqrt"></a>SQRT</span><span class="sxs-lookup"><span data-stu-id="c1b02-813"><a name="bk_sqrt"></a> SQRT</span></span>  
 <span data-ttu-id="c1b02-814">Retourneert de vierkantswortel van Hallo Hallo opgegeven numerieke waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-814">Returns hello square root of hello specified numeric value.</span></span>  
  
 <span data-ttu-id="c1b02-815">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-815">**Syntax**</span></span>  
  
```  
SQRT(<numeric_expression>)  
```  
  
 <span data-ttu-id="c1b02-816">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-816">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="c1b02-817">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-817">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-818">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-818">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-819">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-819">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-820">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-820">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-821">Hallo retourneert volgende voorbeeld Hallo vierkante roots van de getallen 1-3.</span><span class="sxs-lookup"><span data-stu-id="c1b02-821">hello following example returns hello square roots of numbers 1-3.</span></span>  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 <span data-ttu-id="c1b02-822">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-822">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <span data-ttu-id="c1b02-823"><a name="bk_square"></a>VIERKANTE</span><span class="sxs-lookup"><span data-stu-id="c1b02-823"><a name="bk_square"></a> SQUARE</span></span>  
 <span data-ttu-id="c1b02-824">Retourneert Hallo vierkante Hallo opgegeven numerieke waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-824">Returns hello square of hello specified numeric value.</span></span>  
  
 <span data-ttu-id="c1b02-825">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-825">**Syntax**</span></span>  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 <span data-ttu-id="c1b02-826">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-826">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="c1b02-827">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-827">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-828">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-828">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-829">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-829">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-830">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-830">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-831">Hallo wordt volgende voorbeeld de kwadraten Hallo van getallen 1-3.</span><span class="sxs-lookup"><span data-stu-id="c1b02-831">hello following example returns hello squares of numbers 1-3.</span></span>  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 <span data-ttu-id="c1b02-832">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-832">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <span data-ttu-id="c1b02-833"><a name="bk_tan"></a>TAN</span><span class="sxs-lookup"><span data-stu-id="c1b02-833"><a name="bk_tan"></a> TAN</span></span>  
 <span data-ttu-id="c1b02-834">Retourneert de tangens Hallo Hallo hoek aangeduid in radialen, in Hallo opgegeven expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-834">Returns hello tangent of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="c1b02-835">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-835">**Syntax**</span></span>  
  
```  
TAN (<numeric_expression>)  
```  
  
 <span data-ttu-id="c1b02-836">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-836">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="c1b02-837">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-837">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-838">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-838">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-839">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-839">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-840">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-840">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-841">Hallo volgende voorbeeld wordt berekend Hallo tangens van PI () / 2.</span><span class="sxs-lookup"><span data-stu-id="c1b02-841">hello following example calculates hello tangent of PI()/2.</span></span>  
  
```  
SELECT TAN(PI()/2);  
```  
  
 <span data-ttu-id="c1b02-842">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-842">Here is hello result set.</span></span>  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <span data-ttu-id="c1b02-843"><a name="bk_trunc"></a>GEHEEL</span><span class="sxs-lookup"><span data-stu-id="c1b02-843"><a name="bk_trunc"></a> TRUNC</span></span>  
 <span data-ttu-id="c1b02-844">Retourneert een numerieke waarde ingekorte toohello dichtstbijzijnde integer-waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-844">Returns a numeric value, truncated toohello closest integer value.</span></span>  
  
 <span data-ttu-id="c1b02-845">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-845">**Syntax**</span></span>  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 <span data-ttu-id="c1b02-846">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-846">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="c1b02-847">Is een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-847">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-848">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-848">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-849">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-849">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-850">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-850">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-851">Hallo volgende voorbeeld wordt afgekapt Hallo positieve en negatieve getallen toohello dichtstbijzijnde integerwaarde te volgen.</span><span class="sxs-lookup"><span data-stu-id="c1b02-851">hello following example truncates hello following positive and negative numbers toohello nearest integer value.</span></span>  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 <span data-ttu-id="c1b02-852">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-852">Here is hello result set.</span></span>  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <span data-ttu-id="c1b02-853"><a name="bk_type_checking_functions"></a>Controle van de functies van het type</span><span class="sxs-lookup"><span data-stu-id="c1b02-853"><a name="bk_type_checking_functions"></a> Type checking functions</span></span>  
 <span data-ttu-id="c1b02-854">Hallo volgende functies ondersteunen typecontrole tegen invoerwaarden en elk een Booleaanse waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="c1b02-854">hello following functions support type checking against input values, and each return a Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="c1b02-855">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="c1b02-855">IS_ARRAY</span></span>](#bk_is_array)|[<span data-ttu-id="c1b02-856">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="c1b02-856">IS_BOOL</span></span>](#bk_is_bool)|[<span data-ttu-id="c1b02-857">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="c1b02-857">IS_DEFINED</span></span>](#bk_is_defined)|  
|[<span data-ttu-id="c1b02-858">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="c1b02-858">IS_NULL</span></span>](#bk_is_null)|[<span data-ttu-id="c1b02-859">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="c1b02-859">IS_NUMBER</span></span>](#bk_is_number)|[<span data-ttu-id="c1b02-860">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="c1b02-860">IS_OBJECT</span></span>](#bk_is_object)|  
|[<span data-ttu-id="c1b02-861">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="c1b02-861">IS_PRIMITIVE</span></span>](#bk_is_primitive)|[<span data-ttu-id="c1b02-862">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="c1b02-862">IS_STRING</span></span>](#bk_is_string)||  
  
####  <span data-ttu-id="c1b02-863"><a name="bk_is_array"></a>IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="c1b02-863"><a name="bk_is_array"></a> IS_ARRAY</span></span>  
 <span data-ttu-id="c1b02-864">Retourneert een Booleaanse waarde die aangeeft als Hallo type Hallo expressie opgegeven is een matrix.</span><span class="sxs-lookup"><span data-stu-id="c1b02-864">Returns a Boolean value indicating if hello type of hello specified expression is an array.</span></span>  
  
 <span data-ttu-id="c1b02-865">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-865">**Syntax**</span></span>  
  
```  
IS_ARRAY(<expression>)  
```  
  
 <span data-ttu-id="c1b02-866">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-866">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="c1b02-867">Is geldige expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-867">Is any valid expression.</span></span>  
  
 <span data-ttu-id="c1b02-868">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-868">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-869">Retourneert een Booleaanse expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-869">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="c1b02-870">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-870">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-871">Hallo volgende voorbeeld wordt gecontroleerd objecten van JSON Boolean, getal, string, null, object, matrix en niet-gedefinieerde typen met behulp van Hallo IS_ARRAY-functie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-871">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_ARRAY function.</span></span>  
  
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
  
 <span data-ttu-id="c1b02-872">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-872">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <span data-ttu-id="c1b02-873"><a name="bk_is_bool"></a>IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="c1b02-873"><a name="bk_is_bool"></a> IS_BOOL</span></span>  
 <span data-ttu-id="c1b02-874">Retourneert een Booleaanse waarde die aangeeft als Hallo type Hallo expressie opgegeven is een Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-874">Returns a Boolean value indicating if hello type of hello specified expression is a Boolean.</span></span>  
  
 <span data-ttu-id="c1b02-875">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-875">**Syntax**</span></span>  
  
```  
IS_BOOL(<expression>)  
```  
  
 <span data-ttu-id="c1b02-876">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-876">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="c1b02-877">Is geldige expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-877">Is any valid expression.</span></span>  
  
 <span data-ttu-id="c1b02-878">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-878">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-879">Retourneert een Booleaanse expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-879">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="c1b02-880">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-880">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-881">Hallo volgende voorbeeld wordt gecontroleerd objecten van JSON Boolean, getal, string, null, object, matrix en niet-gedefinieerde typen met behulp van Hallo IS_BOOL-functie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-881">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_BOOL function.</span></span>  
  
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
  
 <span data-ttu-id="c1b02-882">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-882">Here is hello result set.</span></span>  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="c1b02-883"><a name="bk_is_defined"></a>IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="c1b02-883"><a name="bk_is_defined"></a> IS_DEFINED</span></span>  
 <span data-ttu-id="c1b02-884">Retourneert een Booleaanse waarde die aangeeft of Hallo eigenschap een waarde is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="c1b02-884">Returns a Boolean indicating if hello property has been assigned a value.</span></span>  
  
 <span data-ttu-id="c1b02-885">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-885">**Syntax**</span></span>  
  
```  
IS_DEFINED(<expression>)  
```  
  
 <span data-ttu-id="c1b02-886">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-886">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="c1b02-887">Is geldige expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-887">Is any valid expression.</span></span>  
  
 <span data-ttu-id="c1b02-888">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-888">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-889">Retourneert een Booleaanse expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-889">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="c1b02-890">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-890">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-891">voorbeeld-controles voor de aanwezigheid van een eigenschap binnen Hallo HALLO hallo opgegeven JSON-document.</span><span class="sxs-lookup"><span data-stu-id="c1b02-891">hello following example checks for hello presence of a property within hello specified JSON document.</span></span> <span data-ttu-id="c1b02-892">Hallo eerst ' true ' geretourneerd omdat "a" aanwezig is, maar Hallo tweede onwaar retourneert omdat "b" ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="c1b02-892">hello first returns true since "a" is present, but hello second returns false since "b" is absent.</span></span>  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 <span data-ttu-id="c1b02-893">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-893">Here is hello result set.</span></span>  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <span data-ttu-id="c1b02-894"><a name="bk_is_null"></a>IS_NULL</span><span class="sxs-lookup"><span data-stu-id="c1b02-894"><a name="bk_is_null"></a> IS_NULL</span></span>  
 <span data-ttu-id="c1b02-895">Retourneert een Booleaanse waarde die aangeeft als Hallo type Hallo expressie opgegeven is null.</span><span class="sxs-lookup"><span data-stu-id="c1b02-895">Returns a Boolean value indicating if hello type of hello specified expression is null.</span></span>  
  
 <span data-ttu-id="c1b02-896">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-896">**Syntax**</span></span>  
  
```  
IS_NULL(<expression>)  
```  
  
 <span data-ttu-id="c1b02-897">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-897">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="c1b02-898">Is geldige expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-898">Is any valid expression.</span></span>  
  
 <span data-ttu-id="c1b02-899">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-899">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-900">Retourneert een Booleaanse expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-900">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="c1b02-901">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-901">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-902">Hallo volgende voorbeeld wordt gecontroleerd objecten van JSON Boolean, getal, string, null, object, matrix en niet-gedefinieerde typen met behulp van Hallo IS_NULL-functie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-902">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_NULL function.</span></span>  
  
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
  
 <span data-ttu-id="c1b02-903">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-903">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="c1b02-904"><a name="bk_is_number"></a>IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="c1b02-904"><a name="bk_is_number"></a> IS_NUMBER</span></span>  
 <span data-ttu-id="c1b02-905">Retourneert een Booleaanse waarde die aangeeft als Hallo type Hallo expressie opgegeven is een getal.</span><span class="sxs-lookup"><span data-stu-id="c1b02-905">Returns a Boolean value indicating if hello type of hello specified expression is a number.</span></span>  
  
 <span data-ttu-id="c1b02-906">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-906">**Syntax**</span></span>  
  
```  
IS_NUMBER(<expression>)  
```  
  
 <span data-ttu-id="c1b02-907">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-907">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="c1b02-908">Is geldige expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-908">Is any valid expression.</span></span>  
  
 <span data-ttu-id="c1b02-909">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-909">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-910">Retourneert een Booleaanse expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-910">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="c1b02-911">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-911">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-912">Hallo volgende voorbeeld wordt gecontroleerd objecten van JSON Boolean, getal, string, null, object, matrix en niet-gedefinieerde typen met behulp van Hallo IS_NULL-functie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-912">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_NULL function.</span></span>  
  
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
  
 <span data-ttu-id="c1b02-913">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-913">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="c1b02-914"><a name="bk_is_object"></a>IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="c1b02-914"><a name="bk_is_object"></a> IS_OBJECT</span></span>  
 <span data-ttu-id="c1b02-915">Retourneert een Booleaanse waarde die aangeeft als Hallo type Hallo expressie opgegeven is een JSON-object.</span><span class="sxs-lookup"><span data-stu-id="c1b02-915">Returns a Boolean value indicating if hello type of hello specified expression is a JSON object.</span></span>  
  
 <span data-ttu-id="c1b02-916">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-916">**Syntax**</span></span>  
  
```  
IS_OBJECT(<expression>)  
```  
  
 <span data-ttu-id="c1b02-917">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-917">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="c1b02-918">Is geldige expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-918">Is any valid expression.</span></span>  
  
 <span data-ttu-id="c1b02-919">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-919">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-920">Retourneert een Booleaanse expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-920">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="c1b02-921">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-921">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-922">Hallo volgende voorbeeld wordt gecontroleerd objecten van JSON Boolean, getal, string, null, object, matrix en niet-gedefinieerde typen met behulp van Hallo IS_OBJECT-functie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-922">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_OBJECT function.</span></span>  
  
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
  
 <span data-ttu-id="c1b02-923">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-923">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <span data-ttu-id="c1b02-924"><a name="bk_is_primitive"></a>IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="c1b02-924"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span></span>  
 <span data-ttu-id="c1b02-925">Retourneert een Booleaanse waarde waarmee wordt aangegeven als Hallo type Hallo opgegeven expressie is een primitief (string, Boolean, numerieke of null).</span><span class="sxs-lookup"><span data-stu-id="c1b02-925">Returns a Boolean value indicating if hello type of hello specified expression is a primitive (string, Boolean, numeric or null).</span></span>  
  
 <span data-ttu-id="c1b02-926">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-926">**Syntax**</span></span>  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 <span data-ttu-id="c1b02-927">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-927">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="c1b02-928">Is geldige expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-928">Is any valid expression.</span></span>  
  
 <span data-ttu-id="c1b02-929">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-929">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-930">Retourneert een Booleaanse expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-930">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="c1b02-931">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-931">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-932">Hallo volgende voorbeeld wordt gecontroleerd objecten van JSON Boolean, getal, string, null, object, matrix en niet-gedefinieerde typen met behulp van Hallo IS_PRIMITIVE-functie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-932">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_PRIMITIVE function.</span></span>  
  
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
  
 <span data-ttu-id="c1b02-933">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-933">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <span data-ttu-id="c1b02-934"><a name="bk_is_string"></a>IS_STRING</span><span class="sxs-lookup"><span data-stu-id="c1b02-934"><a name="bk_is_string"></a> IS_STRING</span></span>  
 <span data-ttu-id="c1b02-935">Retourneert een Booleaanse waarde die aangeeft als Hallo type Hallo expressie opgegeven is een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="c1b02-935">Returns a Boolean value indicating if hello type of hello specified expression is a string.</span></span>  
  
 <span data-ttu-id="c1b02-936">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-936">**Syntax**</span></span>  
  
```  
IS_STRING(<expression>)  
```  
  
 <span data-ttu-id="c1b02-937">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-937">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="c1b02-938">Is geldige expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-938">Is any valid expression.</span></span>  
  
 <span data-ttu-id="c1b02-939">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-939">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-940">Retourneert een Booleaanse expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-940">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="c1b02-941">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-941">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-942">Hallo volgende voorbeeld wordt gecontroleerd objecten van JSON Boolean, getal, string, null, object, matrix en niet-gedefinieerde typen met behulp van Hallo IS_STRING-functie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-942">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_STRING function.</span></span>  
  
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
  
 <span data-ttu-id="c1b02-943">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-943">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <span data-ttu-id="c1b02-944"><a name="bk_string_functions"></a>Tekenreeks-functies</span><span class="sxs-lookup"><span data-stu-id="c1b02-944"><a name="bk_string_functions"></a> String functions</span></span>  
 <span data-ttu-id="c1b02-945">Hallo volgende scalaire functies een bewerking uitvoeren op een tekenreekswaarde van de invoer en een tekenreeks, numerieke of Booleaanse waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="c1b02-945">hello following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="c1b02-946">CONCAT</span><span class="sxs-lookup"><span data-stu-id="c1b02-946">CONCAT</span></span>](#bk_concat)|[<span data-ttu-id="c1b02-947">BEVAT</span><span class="sxs-lookup"><span data-stu-id="c1b02-947">CONTAINS</span></span>](#bk_contains)|[<span data-ttu-id="c1b02-948">ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="c1b02-948">ENDSWITH</span></span>](#bk_endswith)|  
|[<span data-ttu-id="c1b02-949">INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="c1b02-949">INDEX_OF</span></span>](#bk_index_of)|[<span data-ttu-id="c1b02-950">LINKS</span><span class="sxs-lookup"><span data-stu-id="c1b02-950">LEFT</span></span>](#bk_left)|[<span data-ttu-id="c1b02-951">LENGTE</span><span class="sxs-lookup"><span data-stu-id="c1b02-951">LENGTH</span></span>](#bk_length)|  
|[<span data-ttu-id="c1b02-952">LAGERE</span><span class="sxs-lookup"><span data-stu-id="c1b02-952">LOWER</span></span>](#bk_lower)|[<span data-ttu-id="c1b02-953">LTRIM</span><span class="sxs-lookup"><span data-stu-id="c1b02-953">LTRIM</span></span>](#bk_ltrim)|[<span data-ttu-id="c1b02-954">VERVANGEN</span><span class="sxs-lookup"><span data-stu-id="c1b02-954">REPLACE</span></span>](#bk_replace)|  
|[<span data-ttu-id="c1b02-955">REPLICEREN</span><span class="sxs-lookup"><span data-stu-id="c1b02-955">REPLICATE</span></span>](#bk_replicate)|[<span data-ttu-id="c1b02-956">OMKEREN</span><span class="sxs-lookup"><span data-stu-id="c1b02-956">REVERSE</span></span>](#bk_reverse)|[<span data-ttu-id="c1b02-957">RECHTS</span><span class="sxs-lookup"><span data-stu-id="c1b02-957">RIGHT</span></span>](#bk_right)|  
|[<span data-ttu-id="c1b02-958">RTRIM</span><span class="sxs-lookup"><span data-stu-id="c1b02-958">RTRIM</span></span>](#bk_rtrim)|[<span data-ttu-id="c1b02-959">STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="c1b02-959">STARTSWITH</span></span>](#bk_startswith)|[<span data-ttu-id="c1b02-960">DE SUBTEKENREEKS</span><span class="sxs-lookup"><span data-stu-id="c1b02-960">SUBSTRING</span></span>](#bk_substring)|  
|[<span data-ttu-id="c1b02-961">BOVENSTE</span><span class="sxs-lookup"><span data-stu-id="c1b02-961">UPPER</span></span>](#bk_upper)|||  
  
####  <span data-ttu-id="c1b02-962"><a name="bk_concat"></a>CONCAT</span><span class="sxs-lookup"><span data-stu-id="c1b02-962"><a name="bk_concat"></a> CONCAT</span></span>  
 <span data-ttu-id="c1b02-963">Retourneert een tekenreeks die Hallo resultaat is van het samenvoegen van twee of meer tekenreekswaarden.</span><span class="sxs-lookup"><span data-stu-id="c1b02-963">Returns a string that is hello result of concatenating two or more string values.</span></span>  
  
 <span data-ttu-id="c1b02-964">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-964">**Syntax**</span></span>  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 <span data-ttu-id="c1b02-965">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-965">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="c1b02-966">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-966">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="c1b02-967">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-967">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-968">Retourneert een tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-968">Returns a string expression.</span></span>  
  
 <span data-ttu-id="c1b02-969">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-969">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-970">Hallo volgende voorbeeld retourneert Hallo samengevoegd tekenreeks Hallo opgegeven waarden.</span><span class="sxs-lookup"><span data-stu-id="c1b02-970">hello following example returns hello concatenated string of hello specified values.</span></span>  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 <span data-ttu-id="c1b02-971">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-971">Here is hello result set.</span></span>  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <span data-ttu-id="c1b02-972"><a name="bk_contains"></a>BEVAT</span><span class="sxs-lookup"><span data-stu-id="c1b02-972"><a name="bk_contains"></a> CONTAINS</span></span>  
 <span data-ttu-id="c1b02-973">Retourneert een Booleaanse waarde die aangeeft of de eerste tekenreeksexpressie Hallo Hallo op de tweede bevat.</span><span class="sxs-lookup"><span data-stu-id="c1b02-973">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span>  
  
 <span data-ttu-id="c1b02-974">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-974">**Syntax**</span></span>  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="c1b02-975">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-975">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="c1b02-976">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-976">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="c1b02-977">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-977">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-978">Retourneert een Booleaanse expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-978">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="c1b02-979">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-979">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-980">Hallo volgende voorbeeld wordt gecontroleerd als "abc" bevat "ab" en "d".</span><span class="sxs-lookup"><span data-stu-id="c1b02-980">hello following example checks if "abc" contains "ab" and contains "d".</span></span>  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 <span data-ttu-id="c1b02-981">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-981">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="c1b02-982"><a name="bk_endswith"></a>ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="c1b02-982"><a name="bk_endswith"></a> ENDSWITH</span></span>  
 <span data-ttu-id="c1b02-983">Retourneert een Booleaanse waarde die aangeeft of de eerste tekenreeksexpressie Hallo Hallo tweede eindigt.</span><span class="sxs-lookup"><span data-stu-id="c1b02-983">Returns a Boolean indicating whether hello first string expression ends with hello second.</span></span>  
  
 <span data-ttu-id="c1b02-984">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-984">**Syntax**</span></span>  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="c1b02-985">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-985">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="c1b02-986">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-986">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="c1b02-987">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-987">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-988">Retourneert een Booleaanse expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-988">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="c1b02-989">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-989">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-990">Hallo retourneert volgende voorbeeld Hallo "abc" op "b" en 'bc eindigt'.</span><span class="sxs-lookup"><span data-stu-id="c1b02-990">hello following example returns hello "abc" ends with "b" and "bc".</span></span>  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 <span data-ttu-id="c1b02-991">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-991">Here is hello result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="c1b02-992"><a name="bk_index_of"></a>INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="c1b02-992"><a name="bk_index_of"></a> INDEX_OF</span></span>  
 <span data-ttu-id="c1b02-993">Retourneert Hallo beginpositie van de eerste instantie Hallo van tweede tekenreeksexpressie Hallo binnen Hallo eerste opgegeven tekenreeksexpressie of -1 als het Hallo-tekenreeks is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="c1b02-993">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span>  
  
 <span data-ttu-id="c1b02-994">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-994">**Syntax**</span></span>  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="c1b02-995">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-995">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="c1b02-996">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-996">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="c1b02-997">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-997">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-998">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-998">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-999">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-999">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-1000">Hallo wordt volgende voorbeeld de index Hallo van verschillende subtekenreeksen binnen "abc".</span><span class="sxs-lookup"><span data-stu-id="c1b02-1000">hello following example returns hello index of various substrings inside "abc".</span></span>  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 <span data-ttu-id="c1b02-1001">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1001">Here is hello result set.</span></span>  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <span data-ttu-id="c1b02-1002"><a name="bk_left"></a>LINKS</span><span class="sxs-lookup"><span data-stu-id="c1b02-1002"><a name="bk_left"></a> LEFT</span></span>  
 <span data-ttu-id="c1b02-1003">Retourneert het linkergedeelte van een tekenreeks Hallo Hello opgegeven aantal tekens.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1003">Returns hello left part of a string with hello specified number of characters.</span></span>  
  
 <span data-ttu-id="c1b02-1004">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1004">**Syntax**</span></span>  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="c1b02-1005">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1005">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="c1b02-1006">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1006">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="c1b02-1007">Is geldige numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1007">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-1008">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1008">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-1009">Retourneert een tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1009">Returns a string expression.</span></span>  
  
 <span data-ttu-id="c1b02-1010">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1010">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-1011">Hallo volgende voorbeeld retourneert Hallo links onderdeel van "abc" voor waarden van verschillende lengte.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1011">hello following example returns hello left part of "abc" for various length values.</span></span>  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 <span data-ttu-id="c1b02-1012">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1012">Here is hello result set.</span></span>  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <span data-ttu-id="c1b02-1013"><a name="bk_length"></a>LENGTE</span><span class="sxs-lookup"><span data-stu-id="c1b02-1013"><a name="bk_length"></a> LENGTH</span></span>  
 <span data-ttu-id="c1b02-1014">Retourneert Hallo aantal tekens Hallo opgegeven tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1014">Returns hello number of characters of hello specified string expression.</span></span>  
  
 <span data-ttu-id="c1b02-1015">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1015">**Syntax**</span></span>  
  
```  
LENGTH(<str_expr>)  
```  
  
 <span data-ttu-id="c1b02-1016">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1016">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="c1b02-1017">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1017">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="c1b02-1018">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1018">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-1019">Retourneert een tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1019">Returns a string expression.</span></span>  
  
 <span data-ttu-id="c1b02-1020">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1020">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-1021">Hallo retourneert volgende voorbeeld Hallo lengte van een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1021">hello following example returns hello length of a string.</span></span>  
  
```  
SELECT LENGTH("abc")  
```  
  
 <span data-ttu-id="c1b02-1022">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1022">Here is hello result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="c1b02-1023"><a name="bk_lower"></a>LAGERE</span><span class="sxs-lookup"><span data-stu-id="c1b02-1023"><a name="bk_lower"></a> LOWER</span></span>  
 <span data-ttu-id="c1b02-1024">Retourneert een tekenreeksexpressie na hoofdletter gegevens toolowercase converteren.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1024">Returns a string expression after converting uppercase character data toolowercase.</span></span>  
  
 <span data-ttu-id="c1b02-1025">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1025">**Syntax**</span></span>  
  
```  
LOWER(<str_expr>)  
```  
  
 <span data-ttu-id="c1b02-1026">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1026">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="c1b02-1027">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1027">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="c1b02-1028">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1028">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-1029">Retourneert een tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1029">Returns a string expression.</span></span>  
  
 <span data-ttu-id="c1b02-1030">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1030">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-1031">Hallo volgende voorbeeld wordt getoond hoe toouse lager in een query.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1031">hello following example shows how toouse LOWER in a query.</span></span>  
  
```  
SELECT LOWER("Abc")  
```  
  
 <span data-ttu-id="c1b02-1032">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1032">Here is hello result set.</span></span>  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <span data-ttu-id="c1b02-1033"><a name="bk_ltrim"></a>LTRIM</span><span class="sxs-lookup"><span data-stu-id="c1b02-1033"><a name="bk_ltrim"></a> LTRIM</span></span>  
 <span data-ttu-id="c1b02-1034">Retourneert een tekenreeksexpressie na het verwijderen van toonaangevende lege waarden.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1034">Returns a string expression after it removes leading blanks.</span></span>  
  
 <span data-ttu-id="c1b02-1035">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1035">**Syntax**</span></span>  
  
```  
LTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="c1b02-1036">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1036">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="c1b02-1037">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1037">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="c1b02-1038">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1038">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-1039">Retourneert een tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1039">Returns a string expression.</span></span>  
  
 <span data-ttu-id="c1b02-1040">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1040">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-1041">Hallo volgende voorbeeld wordt getoond hoe toouse LTRIM binnen een query.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1041">hello following example shows how toouse LTRIM inside a query.</span></span>  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 <span data-ttu-id="c1b02-1042">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1042">Here is hello result set.</span></span>  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <span data-ttu-id="c1b02-1043"><a name="bk_replace"></a>VERVANGEN</span><span class="sxs-lookup"><span data-stu-id="c1b02-1043"><a name="bk_replace"></a> REPLACE</span></span>  
 <span data-ttu-id="c1b02-1044">Vervangt alle instanties van een opgegeven string-waarde met de waarde van een andere tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1044">Replaces all occurrences of a specified string value with another string value.</span></span>  
  
 <span data-ttu-id="c1b02-1045">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1045">**Syntax**</span></span>  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="c1b02-1046">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1046">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="c1b02-1047">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1047">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="c1b02-1048">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1048">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-1049">Retourneert een tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1049">Returns a string expression.</span></span>  
  
 <span data-ttu-id="c1b02-1050">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1050">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-1051">Hallo volgende voorbeeld ziet u hoe toouse vervangen in een query.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1051">hello following example shows how toouse REPLACE in a query.</span></span>  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 <span data-ttu-id="c1b02-1052">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1052">Here is hello result set.</span></span>  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <span data-ttu-id="c1b02-1053"><a name="bk_replicate"></a>REPLICEREN</span><span class="sxs-lookup"><span data-stu-id="c1b02-1053"><a name="bk_replicate"></a> REPLICATE</span></span>  
 <span data-ttu-id="c1b02-1054">Herhaalt een string-waarde van een opgegeven aantal keren.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1054">Repeats a string value a specified number of times.</span></span>  
  
 <span data-ttu-id="c1b02-1055">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1055">**Syntax**</span></span>  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="c1b02-1056">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1056">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="c1b02-1057">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1057">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="c1b02-1058">Is geldige numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1058">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-1059">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1059">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-1060">Retourneert een tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1060">Returns a string expression.</span></span>  
  
 <span data-ttu-id="c1b02-1061">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1061">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-1062">Hallo volgende voorbeeld ziet u hoe toouse REPLICEREN in een query.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1062">hello following example shows how toouse REPLICATE in a query.</span></span>  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 <span data-ttu-id="c1b02-1063">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1063">Here is hello result set.</span></span>  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <span data-ttu-id="c1b02-1064"><a name="bk_reverse"></a>OMKEREN</span><span class="sxs-lookup"><span data-stu-id="c1b02-1064"><a name="bk_reverse"></a> REVERSE</span></span>  
 <span data-ttu-id="c1b02-1065">Retourneert de omgekeerde volgorde Hallo van een string-waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1065">Returns hello reverse order of a string value.</span></span>  
  
 <span data-ttu-id="c1b02-1066">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1066">**Syntax**</span></span>  
  
```  
REVERSE(<str_expr>)  
```  
  
 <span data-ttu-id="c1b02-1067">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1067">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="c1b02-1068">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1068">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="c1b02-1069">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1069">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-1070">Retourneert een tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1070">Returns a string expression.</span></span>  
  
 <span data-ttu-id="c1b02-1071">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1071">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-1072">Hallo volgende voorbeeld ziet u hoe toouse REVERSE in een query.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1072">hello following example shows how toouse REVERSE in a query.</span></span>  
  
```  
SELECT REVERSE("Abc")  
```  
  
 <span data-ttu-id="c1b02-1073">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1073">Here is hello result set.</span></span>  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <span data-ttu-id="c1b02-1074"><a name="bk_right"></a>RECHTS</span><span class="sxs-lookup"><span data-stu-id="c1b02-1074"><a name="bk_right"></a> RIGHT</span></span>  
 <span data-ttu-id="c1b02-1075">Hallo rechts deel uit van een tekenreeks retourneert Hello opgegeven aantal tekens.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1075">Returns hello right part of a string with hello specified number of characters.</span></span>  
  
 <span data-ttu-id="c1b02-1076">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1076">**Syntax**</span></span>  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="c1b02-1077">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1077">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="c1b02-1078">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1078">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="c1b02-1079">Is geldige numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1079">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-1080">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1080">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-1081">Retourneert een tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1081">Returns a string expression.</span></span>  
  
 <span data-ttu-id="c1b02-1082">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1082">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-1083">Hello wordt volgende voorbeeld het rechterdeel Hallo van "abc" voor verschillende lengtewaarden.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1083">hello following example returns hello right part of "abc" for various length values.</span></span>  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 <span data-ttu-id="c1b02-1084">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1084">Here is hello result set.</span></span>  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <span data-ttu-id="c1b02-1085"><a name="bk_rtrim"></a>RTRIM</span><span class="sxs-lookup"><span data-stu-id="c1b02-1085"><a name="bk_rtrim"></a> RTRIM</span></span>  
 <span data-ttu-id="c1b02-1086">Retourneert een tekenreeksexpressie na het afsluitende spaties verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1086">Returns a string expression after it removes trailing blanks.</span></span>  
  
 <span data-ttu-id="c1b02-1087">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1087">**Syntax**</span></span>  
  
```  
RTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="c1b02-1088">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1088">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="c1b02-1089">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1089">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="c1b02-1090">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1090">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-1091">Retourneert een tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1091">Returns a string expression.</span></span>  
  
 <span data-ttu-id="c1b02-1092">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1092">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-1093">Hallo volgende voorbeeld wordt getoond hoe toouse RTRIM binnen een query.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1093">hello following example shows how toouse RTRIM inside a query.</span></span>  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 <span data-ttu-id="c1b02-1094">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1094">Here is hello result set.</span></span>  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <span data-ttu-id="c1b02-1095"><a name="bk_startswith"></a>STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="c1b02-1095"><a name="bk_startswith"></a> STARTSWITH</span></span>  
 <span data-ttu-id="c1b02-1096">Retourneert een Booleaanse waarde die aangeeft of de eerste tekenreeksexpressie Hallo op de tweede met de Hallo begint.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1096">Returns a Boolean indicating whether hello first string expression starts with hello second.</span></span>  
  
 <span data-ttu-id="c1b02-1097">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1097">**Syntax**</span></span>  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="c1b02-1098">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1098">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="c1b02-1099">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1099">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="c1b02-1100">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1100">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-1101">Retourneert een Booleaanse expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1101">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="c1b02-1102">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1102">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-1103">Hallo volgende voorbeeld controleert of hello string "abc" begint met "b" en "a".</span><span class="sxs-lookup"><span data-stu-id="c1b02-1103">hello following example checks if hello string "abc" begins with "b" and "a".</span></span>  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 <span data-ttu-id="c1b02-1104">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1104">Here is hello result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="c1b02-1105"><a name="bk_substring"></a>DE SUBTEKENREEKS</span><span class="sxs-lookup"><span data-stu-id="c1b02-1105"><a name="bk_substring"></a> SUBSTRING</span></span>  
 <span data-ttu-id="c1b02-1106">Retourneert deel uit van een tekenreeksexpressie die begint bij Hallo opgegeven teken op nul gebaseerde positie en blijft toohello opgegeven lengte of toohello einde van de Hallo-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1106">Returns part of a string expression starting at hello specified character zero-based position and continues toohello specified length, or toohello end of hello string.</span></span>  
  
 <span data-ttu-id="c1b02-1107">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1107">**Syntax**</span></span>  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="c1b02-1108">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1108">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="c1b02-1109">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1109">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="c1b02-1110">Is geldige numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1110">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-1111">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1111">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-1112">Retourneert een tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1112">Returns a string expression.</span></span>  
  
 <span data-ttu-id="c1b02-1113">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1113">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-1114">Hallo retourneert volgende voorbeeld Hallo subtekenreeks van "abc" beginnen bij 1 en voor een lengte van 1 teken.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1114">hello following example returns hello substring of "abc" starting at 1 and for a length of 1 character.</span></span>  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 <span data-ttu-id="c1b02-1115">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1115">Here is hello result set.</span></span>  
  
```  
[{"$1": "b"}]  
```  
  
####  <span data-ttu-id="c1b02-1116"><a name="bk_upper"></a>BOVENSTE</span><span class="sxs-lookup"><span data-stu-id="c1b02-1116"><a name="bk_upper"></a> UPPER</span></span>  
 <span data-ttu-id="c1b02-1117">Retourneert een tekenreeksexpressie na kleine letter gegevens toouppercase converteren.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1117">Returns a string expression after converting lowercase character data toouppercase.</span></span>  
  
 <span data-ttu-id="c1b02-1118">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1118">**Syntax**</span></span>  
  
```  
UPPER(<str_expr>)  
```  
  
 <span data-ttu-id="c1b02-1119">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1119">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="c1b02-1120">Is geldige tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1120">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="c1b02-1121">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1121">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-1122">Retourneert een tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1122">Returns a string expression.</span></span>  
  
 <span data-ttu-id="c1b02-1123">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1123">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-1124">Hallo volgende voorbeeld wordt getoond hoe toouse hoofdletters in een query</span><span class="sxs-lookup"><span data-stu-id="c1b02-1124">hello following example shows how toouse UPPER in a query</span></span>  
  
```  
SELECT UPPER("Abc")  
```  
  
 <span data-ttu-id="c1b02-1125">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1125">Here is hello result set.</span></span>  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <span data-ttu-id="c1b02-1126"><a name="bk_array_functions"></a>Matrixfuncties</span><span class="sxs-lookup"><span data-stu-id="c1b02-1126"><a name="bk_array_functions"></a> Array functions</span></span>  
 <span data-ttu-id="c1b02-1127">Hallo scalaire functies na een bewerking uitvoeren op een matrix invoerwaarde en retourneren numerieke, Booleaanse waarde of een matrix van waarde</span><span class="sxs-lookup"><span data-stu-id="c1b02-1127">hello following scalar functions perform an operation on an array input value and return numeric, Boolean or array value</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="c1b02-1128">ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="c1b02-1128">ARRAY_CONCAT</span></span>](#bk_array_concat)|[<span data-ttu-id="c1b02-1129">ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="c1b02-1129">ARRAY_CONTAINS</span></span>](#bk_array_contains)|[<span data-ttu-id="c1b02-1130">ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="c1b02-1130">ARRAY_LENGTH</span></span>](#bk_array_length)|  
|[<span data-ttu-id="c1b02-1131">ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="c1b02-1131">ARRAY_SLICE</span></span>](#bk_array_slice)|||  
  
####  <span data-ttu-id="c1b02-1132"><a name="bk_array_concat"></a>ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="c1b02-1132"><a name="bk_array_concat"></a> ARRAY_CONCAT</span></span>  
 <span data-ttu-id="c1b02-1133">Retourneert een matrix die Hallo resultaat is van het samenvoegen van twee of meer matrixwaarden.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1133">Returns an array that is hello result of concatenating two or more array values.</span></span>  
  
 <span data-ttu-id="c1b02-1134">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1134">**Syntax**</span></span>  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 <span data-ttu-id="c1b02-1135">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1135">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="c1b02-1136">Is geldige matrixexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1136">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="c1b02-1137">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1137">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-1138">Retourneert een matrixexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1138">Returns an array expression.</span></span>  
  
 <span data-ttu-id="c1b02-1139">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1139">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-1140">Hallo volgende voorbeeld hoe tooconcatenate twee matrices.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1140">hello following example how tooconcatenate two arrays.</span></span>  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 <span data-ttu-id="c1b02-1141">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1141">Here is hello result set.</span></span>  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <span data-ttu-id="c1b02-1142"><a name="bk_array_contains"></a>ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="c1b02-1142"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span></span>  
 <span data-ttu-id="c1b02-1143">Retourneert een Booleaanse waarde die aangeeft of de matrix Hallo Hallo bevat een waarde opgegeven.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1143">Returns a Boolean indicating whether hello array contains hello specified value.</span></span>  
  
 <span data-ttu-id="c1b02-1144">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1144">**Syntax**</span></span>  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 <span data-ttu-id="c1b02-1145">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1145">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="c1b02-1146">Is geldige matrixexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1146">Is any valid array expression.</span></span>  
  
-   `expr`  
  
     <span data-ttu-id="c1b02-1147">Is geldige expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1147">Is any valid expression.</span></span>  
  
 <span data-ttu-id="c1b02-1148">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1148">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-1149">Retourneert een Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1149">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="c1b02-1150">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1150">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-1151">Hallo volgt hoe toocheck voor lidmaatschap in een matrix met ARRAY_CONTAINS.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1151">hello following example how toocheck for membership in an array using ARRAY_CONTAINS.</span></span>  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 <span data-ttu-id="c1b02-1152">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1152">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="c1b02-1153"><a name="bk_array_length"></a>ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="c1b02-1153"><a name="bk_array_length"></a> ARRAY_LENGTH</span></span>  
 <span data-ttu-id="c1b02-1154">Retourneert Hallo aantal elementen Hallo matrixexpressie opgegeven.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1154">Returns hello number of elements of hello specified array expression.</span></span>  
  
 <span data-ttu-id="c1b02-1155">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1155">**Syntax**</span></span>  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 <span data-ttu-id="c1b02-1156">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1156">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="c1b02-1157">Is geldige matrixexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1157">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="c1b02-1158">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1158">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-1159">Retourneert een numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1159">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-1160">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1160">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-1161">Hallo volgende voorbeeld hoe tooget lengte van een matrix met ARRAY_LENGTH Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1161">hello following example how tooget hello length of an array using ARRAY_LENGTH.</span></span>  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 <span data-ttu-id="c1b02-1162">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1162">Here is hello result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="c1b02-1163"><a name="bk_array_slice"></a>ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="c1b02-1163"><a name="bk_array_slice"></a> ARRAY_SLICE</span></span>  
 <span data-ttu-id="c1b02-1164">Retourneert deel van een matrixexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1164">Returns part of an array expression.</span></span>
  
 <span data-ttu-id="c1b02-1165">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1165">**Syntax**</span></span>  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="c1b02-1166">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1166">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="c1b02-1167">Is geldige matrixexpressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1167">Is any valid array expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="c1b02-1168">Is geldige numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1168">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="c1b02-1169">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1169">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-1170">Retourneert een Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1170">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="c1b02-1171">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1171">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-1172">Hallo volgt hoe tooget deel uit van een matrix met ARRAY_SLICE.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1172">hello following example how tooget a part of an array using ARRAY_SLICE.</span></span>  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 <span data-ttu-id="c1b02-1173">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1173">Here is hello result set.</span></span>  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <span data-ttu-id="c1b02-1174"><a name="bk_spatial_functions"></a>Ruimtelijke functies</span><span class="sxs-lookup"><span data-stu-id="c1b02-1174"><a name="bk_spatial_functions"></a> Spatial functions</span></span>  
 <span data-ttu-id="c1b02-1175">Hallo volgende scalaire functies een bewerking uitvoeren op een invoerwaarde ruimtelijke object en een numeriek gegevenstype of Booleaanse waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1175">hello following scalar functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="c1b02-1176">ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="c1b02-1176">ST_DISTANCE</span></span>](#bk_st_distance)|[<span data-ttu-id="c1b02-1177">ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="c1b02-1177">ST_WITHIN</span></span>](#bk_st_within)|[<span data-ttu-id="c1b02-1178">ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="c1b02-1178">ST_INTERSECTS</span></span>](#bk_st_intersects)|[<span data-ttu-id="c1b02-1179">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="c1b02-1179">ST_ISVALID</span></span>](#bk_st_isvalid)|  
|[<span data-ttu-id="c1b02-1180">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="c1b02-1180">ST_ISVALIDDETAILED</span></span>](#bk_st_isvaliddetailed)|||  
  
####  <span data-ttu-id="c1b02-1181"><a name="bk_st_distance"></a>ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="c1b02-1181"><a name="bk_st_distance"></a> ST_DISTANCE</span></span>  
 <span data-ttu-id="c1b02-1182">Retourneert Hallo afstand tussen twee Hallo GeoJSON punt, Polygon of LineString expressies.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1182">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span>  
  
 <span data-ttu-id="c1b02-1183">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1183">**Syntax**</span></span>  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="c1b02-1184">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1184">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="c1b02-1185">Is geldige expressie voor GeoJSON punt, Polygon of LineString-object.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1185">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="c1b02-1186">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1186">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-1187">Retourneert een numerieke expressie met Hallo afstand.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1187">Returns a numeric expression containing hello distance.</span></span> <span data-ttu-id="c1b02-1188">Dit wordt uitgedrukt in meters voor referentiesysteem Hallo-standaard.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1188">This is expressed in meters for hello default reference system.</span></span>  
  
 <span data-ttu-id="c1b02-1189">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1189">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-1190">Hallo volgende voorbeeld wordt getoond hoe tooreturn alle familie documenten die binnen 30 km Hallo locatie met Hallo de ingebouwde functie ST_DISTANCE opgegeven.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1190">hello following example shows how tooreturn all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> <span data-ttu-id="c1b02-1191">.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1191">.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 <span data-ttu-id="c1b02-1192">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1192">Here is hello result set.</span></span>  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <span data-ttu-id="c1b02-1193"><a name="bk_st_within"></a>ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="c1b02-1193"><a name="bk_st_within"></a> ST_WITHIN</span></span>  
 <span data-ttu-id="c1b02-1194">Retourneert een Booleaanse expressie Hallo GeoJSON (punt, Polygon of LineString) opgegeven object in het eerste argument Hallo is binnen Hallo GeoJSON (punt, Polygon of LineString) in het tweede argument Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1194">Returns a Boolean expression indicating whether hello GeoJSON object (Point, Polygon, or LineString) specified in hello first argument is within hello GeoJSON (Point, Polygon, or LineString) in hello second argument.</span></span>  
  
 <span data-ttu-id="c1b02-1195">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1195">**Syntax**</span></span>  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="c1b02-1196">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1196">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="c1b02-1197">Is geldige expressie voor GeoJSON punt, Polygon of LineString-object.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1197">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="c1b02-1198">Is geldige expressie voor GeoJSON punt, Polygon of LineString-object.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1198">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="c1b02-1199">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1199">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-1200">Retourneert een Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1200">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="c1b02-1201">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1201">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-1202">Hallo volgende voorbeeld ziet u hoe toofind alle familie documenten binnen een veelhoek met ST_WITHIN.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1202">hello following example shows how toofind all family documents within a polygon using ST_WITHIN.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="c1b02-1203">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1203">Here is hello result set.</span></span>  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <span data-ttu-id="c1b02-1204"><a name="bk_st_intersects"></a>ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="c1b02-1204"><a name="bk_st_intersects"></a> ST_INTERSECTS</span></span>  
 <span data-ttu-id="c1b02-1205">Retourneert een Booleaanse expressie waarmee wordt aangegeven of de Hallo GeoJSON object (punt, Polygon of LineString) opgegeven in het eerste argument Hallo Hallo GeoJSON (punt, Polygon of LineString) in het tweede argument Hallo polygoonring.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1205">Returns a Boolean expression indicating whether hello GeoJSON object (Point, Polygon, or LineString) specified in hello first argument intersects hello GeoJSON (Point, Polygon, or LineString) in hello second argument.</span></span>  
  
 <span data-ttu-id="c1b02-1206">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1206">**Syntax**</span></span>  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="c1b02-1207">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1207">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="c1b02-1208">Is geldige expressie voor GeoJSON punt, Polygon of LineString-object.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1208">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="c1b02-1209">Is geldige expressie voor GeoJSON punt, Polygon of LineString-object.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1209">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="c1b02-1210">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1210">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-1211">Retourneert een Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1211">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="c1b02-1212">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1212">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-1213">Hallo volgende voorbeeld wordt getoond hoe toofind alle gebieden die in de polygoonring met Hallo gegeven veelhoek.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1213">hello following example shows how toofind all areas that intersects with hello given polygon.</span></span>  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="c1b02-1214">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1214">Here is hello result set.</span></span>  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <span data-ttu-id="c1b02-1215"><a name="bk_st_isvalid"></a>ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="c1b02-1215"><a name="bk_st_isvalid"></a> ST_ISVALID</span></span>  
 <span data-ttu-id="c1b02-1216">Retourneert een Booleaanse waarde die aangeeft of Hallo opgegeven GeoJSON punt, Polygon of LineString expressie is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1216">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span>  
  
 <span data-ttu-id="c1b02-1217">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1217">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="c1b02-1218">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1218">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="c1b02-1219">Is geldige GeoJSON punt, Polygon of LineString-expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1219">Is any valid GeoJSON Point, Polygon, or LineString expression.</span></span>  
  
 <span data-ttu-id="c1b02-1220">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1220">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-1221">Retourneert een Booleaanse expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1221">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="c1b02-1222">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1222">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-1223">Hallo volgende voorbeeld wordt getoond hoe toocheck als een punt ST_VALID geldig is.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1223">hello following example shows how toocheck if a point is valid using ST_VALID.</span></span>  
  
 <span data-ttu-id="c1b02-1224">Dit punt heeft bijvoorbeeld een Breedtegraadwaarde die niet in Hallo geldig waardenbereik [-90, 90], dus Hallo query retourneert false.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1224">For example, this point has a latitude value that's not in hello valid range of values [-90, 90], so hello query returns false.</span></span>  
  
 <span data-ttu-id="c1b02-1225">Voor multilinestring, Hallo GeoJSON specificatie moet Hallo laatste coördinaat paar opgegeven Hallo dezelfde als de eerste, toocreate Hallo een gesloten vorm.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1225">For polygons, hello GeoJSON specification requires that hello last coordinate pair provided should be hello same as hello first, toocreate a closed shape.</span></span> <span data-ttu-id="c1b02-1226">Punten in een polygoon moeten worden opgegeven in rechtsom volgorde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1226">Points within a polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="c1b02-1227">Een veelhoek in rechtsom order opgegeven vertegenwoordigt Hallo inverse van Hallo regio erin.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1227">A polygon specified in clockwise order represents hello inverse of hello region within it.</span></span>  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 <span data-ttu-id="c1b02-1228">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1228">Here is hello result set.</span></span>  
  
```  
[{ "$1": false }]  
```  
  
####  <span data-ttu-id="c1b02-1229"><a name="bk_st_isvaliddetailed"></a>ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="c1b02-1229"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span></span>  
 <span data-ttu-id="c1b02-1230">Retourneert een JSON-waarde met een Boolean-waarde als Hallo GeoJSON punt, Polygon of LineString expressie opgegeven geldig is en als ongeldig, bovendien Hallo reden als een string-waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1230">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span>  
  
 <span data-ttu-id="c1b02-1231">**Syntaxis**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1231">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="c1b02-1232">**Argumenten**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1232">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="c1b02-1233">Is geldige GeoJSON-punt of de veelhoek expressie.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1233">Is any valid GeoJSON point or polygon expression.</span></span>  
  
 <span data-ttu-id="c1b02-1234">**Retourtypen**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1234">**Return Types**</span></span>  
  
 <span data-ttu-id="c1b02-1235">Retourneert een JSON-waarde met een Boolean-waarde als Hallo GeoJSON punt opgegeven of veelhoek expressie geldig is en als ongeldig, bovendien Hallo reden als een string-waarde.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1235">Returns a JSON value containing a Boolean value if hello specified GeoJSON point or polygon expression is valid, and if invalid, additionally hello reason as a string value.</span></span>  
  
 <span data-ttu-id="c1b02-1236">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="c1b02-1236">**Examples**</span></span>  
  
 <span data-ttu-id="c1b02-1237">Hallo volgt hoe geldigheid van de toocheck (met details) met behulp van ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1237">hello following example how toocheck validity (with details) using ST_ISVALIDDETAILED.</span></span>  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 <span data-ttu-id="c1b02-1238">Hier volgt Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="c1b02-1238">Here is hello result set.</span></span>  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a polygon must have hello same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a><span data-ttu-id="c1b02-1239">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c1b02-1239">Next steps</span></span>  
 <span data-ttu-id="c1b02-1240">[SQL-syntaxis en SQL-query voor Azure Cosmos-DB](documentdb-sql-query.md) </span><span class="sxs-lookup"><span data-stu-id="c1b02-1240">[SQL syntax and SQL query for Azure Cosmos DB](documentdb-sql-query.md) </span></span>  
 [<span data-ttu-id="c1b02-1241">Azure DB Cosmos-documentatie</span><span class="sxs-lookup"><span data-stu-id="c1b02-1241">Azure Cosmos DB documentation</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
