---
title: aaaConstructing filtertekenreeksen voor Hallo tabel designer | Microsoft Docs
description: Tekenreeksen voor Hallo tabel designer maken
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a1a10ea1-687a-4ee1-a952-6b24c2fe1a22
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 48b38d27b97936064daa875e41881d51546bc11f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="constructing-filter-strings-for-hello-table-designer"></a><span data-ttu-id="0c694-103">Samenstellen van tekenreeksen voor Hallo tabelontwerp</span><span class="sxs-lookup"><span data-stu-id="0c694-103">Constructing Filter Strings for hello Table Designer</span></span>
## <a name="overview"></a><span data-ttu-id="0c694-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="0c694-104">Overview</span></span>
<span data-ttu-id="0c694-105">toofilter gegevens in een Azure-tabel die wordt weergegeven in Visual Studio Hallo **tabelontwerp**, u een filtertekenreeks in te stellen en voer deze in het filterveld Hallo.</span><span class="sxs-lookup"><span data-stu-id="0c694-105">toofilter data in an Azure table that is displayed in hello Visual Studio **Table Designer**, you construct a filter string and enter it into hello filter field.</span></span> <span data-ttu-id="0c694-106">Tekenreekssyntaxis wordt Hallo filter wordt gedefinieerd door Hallo WCF Data Services en vergelijkbare tooa SQL WHERE-component is, maar toohello tabel-service via een HTTP-aanvraag is verzonden.</span><span class="sxs-lookup"><span data-stu-id="0c694-106">hello filter string syntax is defined by hello WCF Data Services and is similar tooa SQL WHERE clause, but is sent toohello Table service via an HTTP request.</span></span> <span data-ttu-id="0c694-107">Hallo **tabelontwerp** ingangen Hallo juiste codering voor u in dat geval toofilter op een waarde van de gewenste eigenschap, u moet alleen Hallo eigenschapsnaam, vergelijkingsoperator, voor de vergelijkingsvoorwaarde, invoeren en eventueel Booleaanse operator in Hallo filteren veld.</span><span class="sxs-lookup"><span data-stu-id="0c694-107">hello **Table Designer** handles hello proper encoding for you, so toofilter on a desired property value, you need only enter hello property name, comparison operator, criteria value, and optionally, Boolean operator in hello filter field.</span></span> <span data-ttu-id="0c694-108">U hoeft geen tooinclude hello $filter query-optie zoals u zou doen als u een URL tooquery Hallo tabel via Hallo zijn construeren [Storage Services REST API-verwijzing](http://go.microsoft.com/fwlink/p/?LinkId=400447).</span><span class="sxs-lookup"><span data-stu-id="0c694-108">You do not need tooinclude hello $filter query option as you would if you were constructing a URL tooquery hello table via hello [Storage Services REST API Reference](http://go.microsoft.com/fwlink/p/?LinkId=400447).</span></span>

<span data-ttu-id="0c694-109">Hallo WCF Data Services zijn gebaseerd op Hallo [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData).</span><span class="sxs-lookup"><span data-stu-id="0c694-109">hello WCF Data Services are based on hello [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData).</span></span> <span data-ttu-id="0c694-110">Voor meer informatie over Hallo filter system query-optie (**$filter**), Zie Hallo [OData URI Conventions-specificatie](http://go.microsoft.com/fwlink/p/?LinkId=214806).</span><span class="sxs-lookup"><span data-stu-id="0c694-110">For details on hello filter system query option (**$filter**), see hello [OData URI Conventions specification](http://go.microsoft.com/fwlink/p/?LinkId=214806).</span></span>

## <a name="comparison-operators"></a><span data-ttu-id="0c694-111">Vergelijkingsoperators</span><span class="sxs-lookup"><span data-stu-id="0c694-111">Comparison Operators</span></span>
<span data-ttu-id="0c694-112">Hallo worden volgende logische operators ondersteund voor alle eigenschaptypen:</span><span class="sxs-lookup"><span data-stu-id="0c694-112">hello following logical operators are supported for all property types:</span></span>

| <span data-ttu-id="0c694-113">Logische operator</span><span class="sxs-lookup"><span data-stu-id="0c694-113">Logical operator</span></span> | <span data-ttu-id="0c694-114">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0c694-114">Description</span></span> | <span data-ttu-id="0c694-115">Voorbeeld filtertekenreeks</span><span class="sxs-lookup"><span data-stu-id="0c694-115">Example filter string</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0c694-116">EQ</span><span class="sxs-lookup"><span data-stu-id="0c694-116">eq</span></span> |<span data-ttu-id="0c694-117">Gelijk zijn aan</span><span class="sxs-lookup"><span data-stu-id="0c694-117">Equal</span></span> |<span data-ttu-id="0c694-118">Plaats-eq "Redmond"</span><span class="sxs-lookup"><span data-stu-id="0c694-118">City eq 'Redmond'</span></span> |
| <span data-ttu-id="0c694-119">gt</span><span class="sxs-lookup"><span data-stu-id="0c694-119">gt</span></span> |<span data-ttu-id="0c694-120">Groter dan</span><span class="sxs-lookup"><span data-stu-id="0c694-120">Greater than</span></span> |<span data-ttu-id="0c694-121">Prijs gt 20</span><span class="sxs-lookup"><span data-stu-id="0c694-121">Price gt 20</span></span> |
| <span data-ttu-id="0c694-122">ge</span><span class="sxs-lookup"><span data-stu-id="0c694-122">ge</span></span> |<span data-ttu-id="0c694-123">Groter dan of gelijk te</span><span class="sxs-lookup"><span data-stu-id="0c694-123">Greater than or equal too</span></span>|<span data-ttu-id="0c694-124">Prijs ge 10</span><span class="sxs-lookup"><span data-stu-id="0c694-124">Price ge 10</span></span> |
| <span data-ttu-id="0c694-125">lt</span><span class="sxs-lookup"><span data-stu-id="0c694-125">lt</span></span> |<span data-ttu-id="0c694-126">Kleiner dan</span><span class="sxs-lookup"><span data-stu-id="0c694-126">Less than</span></span> |<span data-ttu-id="0c694-127">Prijs lt 20</span><span class="sxs-lookup"><span data-stu-id="0c694-127">Price lt 20</span></span> |
| <span data-ttu-id="0c694-128">RP</span><span class="sxs-lookup"><span data-stu-id="0c694-128">le</span></span> |<span data-ttu-id="0c694-129">Kleiner dan of gelijk zijn</span><span class="sxs-lookup"><span data-stu-id="0c694-129">Less than or equal</span></span> |<span data-ttu-id="0c694-130">Prijs RP 100</span><span class="sxs-lookup"><span data-stu-id="0c694-130">Price le 100</span></span> |
| <span data-ttu-id="0c694-131">ne</span><span class="sxs-lookup"><span data-stu-id="0c694-131">ne</span></span> |<span data-ttu-id="0c694-132">Niet gelijk aan</span><span class="sxs-lookup"><span data-stu-id="0c694-132">Not equal</span></span> |<span data-ttu-id="0c694-133">Plaats ne 'Londen'</span><span class="sxs-lookup"><span data-stu-id="0c694-133">City ne 'London'</span></span> |
| <span data-ttu-id="0c694-134">en</span><span class="sxs-lookup"><span data-stu-id="0c694-134">and</span></span> |<span data-ttu-id="0c694-135">En</span><span class="sxs-lookup"><span data-stu-id="0c694-135">And</span></span> |<span data-ttu-id="0c694-136">Prijs RP 200 en prijs gt 3.5</span><span class="sxs-lookup"><span data-stu-id="0c694-136">Price le 200 and Price gt 3.5</span></span> |
| <span data-ttu-id="0c694-137">of</span><span class="sxs-lookup"><span data-stu-id="0c694-137">or</span></span> |<span data-ttu-id="0c694-138">of</span><span class="sxs-lookup"><span data-stu-id="0c694-138">Or</span></span> |<span data-ttu-id="0c694-139">Prijs RP 3.5 of prijs gt 200</span><span class="sxs-lookup"><span data-stu-id="0c694-139">Price le 3.5 or Price gt 200</span></span> |
| <span data-ttu-id="0c694-140">niet</span><span class="sxs-lookup"><span data-stu-id="0c694-140">not</span></span> |<span data-ttu-id="0c694-141">niet</span><span class="sxs-lookup"><span data-stu-id="0c694-141">Not</span></span> |<span data-ttu-id="0c694-142">niet isAvailable</span><span class="sxs-lookup"><span data-stu-id="0c694-142">not isAvailable</span></span> |

<span data-ttu-id="0c694-143">Bij het maken van een filtertekenreeks zijn hello volgende regels van belang:</span><span class="sxs-lookup"><span data-stu-id="0c694-143">When constructing a filter string, hello following rules are important:</span></span>

* <span data-ttu-id="0c694-144">Hallo logische operators toocompare een eigenschapswaarde tooa gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0c694-144">Use hello logical operators toocompare a property tooa value.</span></span> <span data-ttu-id="0c694-145">Houd er rekening mee dat het is niet mogelijk toocompare tooa dynamische waarde van een eigenschap; een-zijde van Hallo-expressie moet een constante zijn.</span><span class="sxs-lookup"><span data-stu-id="0c694-145">Note that it is not possible toocompare a property tooa dynamic value; one side of hello expression must be a constant.</span></span>
* <span data-ttu-id="0c694-146">Alle onderdelen van de filtertekenreeks Hallo zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="0c694-146">All parts of hello filter string are case-sensitive.</span></span>
* <span data-ttu-id="0c694-147">Hallo constante waarde moet van het Hallo hetzelfde gegevenstype als de eigenschap hello om Hallo filter tooreturn geldige resultaten.</span><span class="sxs-lookup"><span data-stu-id="0c694-147">hello constant value must be of hello same data type as hello property in order for hello filter tooreturn valid results.</span></span> <span data-ttu-id="0c694-148">Zie voor meer informatie over ondersteunde eigenschaptypen [Understanding Hallo Table Service Data Model](http://go.microsoft.com/fwlink/p/?LinkId=400448).</span><span class="sxs-lookup"><span data-stu-id="0c694-148">For more information about supported property types, see [Understanding hello Table Service Data Model](http://go.microsoft.com/fwlink/p/?LinkId=400448).</span></span>

## <a name="filtering-on-string-properties"></a><span data-ttu-id="0c694-149">Filteren op Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="0c694-149">Filtering on String Properties</span></span>
<span data-ttu-id="0c694-150">Wanneer u op Eigenschappen van een verbindingsreeks filtert, moet u Hallo tekenreeksconstante tussen enkele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="0c694-150">When you filter on string properties, enclose hello string constant in single quotation marks.</span></span>

<span data-ttu-id="0c694-151">Hallo voorbeeld filters op Hallo volgen **PartitionKey** en **RowKey** eigenschappen; extra niet-sleutelkenmerk eigenschappen kunnen ook worden toegevoegd toohello filtertekenreeks:</span><span class="sxs-lookup"><span data-stu-id="0c694-151">hello following example filters on hello **PartitionKey** and **RowKey** properties; additional non-key properties could also be added toohello filter string:</span></span>

    PartitionKey eq 'Partition1' and RowKey eq '00001'

<span data-ttu-id="0c694-152">U kunt haakjes elke filterexpressie, hoewel dit niet vereist is:</span><span class="sxs-lookup"><span data-stu-id="0c694-152">You can enclose each filter expression in parentheses, although it is not required:</span></span>

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

<span data-ttu-id="0c694-153">Houd er rekening mee dat Hallo tabel-service biedt geen ondersteuning voor query's met jokertekens en ze worden niet ondersteund in Hallo tabelontwerp ofwel.</span><span class="sxs-lookup"><span data-stu-id="0c694-153">Note that hello Table service does not support wildcard queries, and they are not supported in hello Table Designer either.</span></span> <span data-ttu-id="0c694-154">U kunt echter met behulp van vergelijkingsoperators op de gewenste voorvoegsel Hallo vergelijken van voorvoegsels uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="0c694-154">However, you can perform prefix matching by using comparison operators on hello desired prefix.</span></span> <span data-ttu-id="0c694-155">Hallo retourneert volgende voorbeeld entiteiten met een eigenschap LastName die begint met Hallo letter "A":</span><span class="sxs-lookup"><span data-stu-id="0c694-155">hello following example returns entities with a LastName property beginning with hello letter 'A':</span></span>

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a><span data-ttu-id="0c694-156">Filteren op numerieke eigenschappen</span><span class="sxs-lookup"><span data-stu-id="0c694-156">Filtering on Numeric Properties</span></span>
<span data-ttu-id="0c694-157">toofilter op een geheel getal of een getal met drijvende komma, geef Hallo zonder aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="0c694-157">toofilter on an integer or floating-point number, specify hello number without quotation marks.</span></span>

<span data-ttu-id="0c694-158">In dit voorbeeld retourneert alle entiteiten met een eigenschap Age waarvan de waarde groter dan 30 is:</span><span class="sxs-lookup"><span data-stu-id="0c694-158">This example returns all entities with an Age property whose value is greater than 30:</span></span>

    Age gt 30

<span data-ttu-id="0c694-159">In dit voorbeeld retourneert alle entiteiten met een tegoed eigenschap waarvan de waarde is kleiner dan of gelijk zijn aan too100.25:</span><span class="sxs-lookup"><span data-stu-id="0c694-159">This example returns all entities with an AmountDue property whose value is less than or equal too100.25:</span></span>

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a><span data-ttu-id="0c694-160">Filteren op Boole-eigenschappen</span><span class="sxs-lookup"><span data-stu-id="0c694-160">Filtering on Boolean Properties</span></span>
<span data-ttu-id="0c694-161">toofilter op een Boolean opgeven **true** of **false** zonder aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="0c694-161">toofilter on a Boolean value, specify **true** or **false** without quotation marks.</span></span>

<span data-ttu-id="0c694-162">Hallo volgende voorbeeld retourneert alle entiteiten waarbij Hallo IsActive eigenschap is ingesteld te**true**:</span><span class="sxs-lookup"><span data-stu-id="0c694-162">hello following example returns all entities where hello IsActive property is set too**true**:</span></span>

    IsActive eq true

<span data-ttu-id="0c694-163">U kunt ook deze filterexpressie zonder Hallo logische operator schrijven.</span><span class="sxs-lookup"><span data-stu-id="0c694-163">You can also write this filter expression without hello logical operator.</span></span> <span data-ttu-id="0c694-164">In Hallo voorbeeld te volgen, Hallo tabelservice geeft ook alle entiteiten waarbij IsActive is **true**:</span><span class="sxs-lookup"><span data-stu-id="0c694-164">In hello following example, hello Table service will also return all entities where IsActive is **true**:</span></span>

    IsActive

<span data-ttu-id="0c694-165">alle entiteiten waarbij IsActive False is, kunt u geen Hallo tooreturn operator:</span><span class="sxs-lookup"><span data-stu-id="0c694-165">tooreturn all entities where IsActive is false, you can use hello not operator:</span></span>

    not IsActive

## <a name="filtering-on-datetime-properties"></a><span data-ttu-id="0c694-166">Filteren op datum/tijd-eigenschappen</span><span class="sxs-lookup"><span data-stu-id="0c694-166">Filtering on DateTime Properties</span></span>
<span data-ttu-id="0c694-167">toofilter op een DateTime-waarde opgeven Hallo **datetime** sleutelwoord, gevolgd door Hallo datum/tijd constante in enkele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="0c694-167">toofilter on a DateTime value, specify hello **datetime** keyword, followed by hello date/time constant in single quotation marks.</span></span> <span data-ttu-id="0c694-168">Hallo datum/tijd constante moet in gecombineerde UTC-notatie, zoals beschreven in [eigenschapswaarden voor datum/tijd opmaken](http://go.microsoft.com/fwlink/p/?LinkId=400449).</span><span class="sxs-lookup"><span data-stu-id="0c694-168">hello date/time constant must be in combined UTC format, as described in [Formatting DateTime Property Values](http://go.microsoft.com/fwlink/p/?LinkId=400449).</span></span>

<span data-ttu-id="0c694-169">Hallo volgende voorbeeld retourneert entiteiten waarbij Hallo CustomerSince eigenschap is gelijk tooJuly 10, 2008:</span><span class="sxs-lookup"><span data-stu-id="0c694-169">hello following example returns entities where hello CustomerSince property is equal tooJuly 10, 2008:</span></span>

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
