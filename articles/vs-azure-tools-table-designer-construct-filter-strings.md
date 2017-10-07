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
# <a name="constructing-filter-strings-for-hello-table-designer"></a>Samenstellen van tekenreeksen voor Hallo tabelontwerp
## <a name="overview"></a>Overzicht
toofilter gegevens in een Azure-tabel die wordt weergegeven in Visual Studio Hallo **tabelontwerp**, u een filtertekenreeks in te stellen en voer deze in het filterveld Hallo. Tekenreekssyntaxis wordt Hallo filter wordt gedefinieerd door Hallo WCF Data Services en vergelijkbare tooa SQL WHERE-component is, maar toohello tabel-service via een HTTP-aanvraag is verzonden. Hallo **tabelontwerp** ingangen Hallo juiste codering voor u in dat geval toofilter op een waarde van de gewenste eigenschap, u moet alleen Hallo eigenschapsnaam, vergelijkingsoperator, voor de vergelijkingsvoorwaarde, invoeren en eventueel Booleaanse operator in Hallo filteren veld. U hoeft geen tooinclude hello $filter query-optie zoals u zou doen als u een URL tooquery Hallo tabel via Hallo zijn construeren [Storage Services REST API-verwijzing](http://go.microsoft.com/fwlink/p/?LinkId=400447).

Hallo WCF Data Services zijn gebaseerd op Hallo [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData). Voor meer informatie over Hallo filter system query-optie (**$filter**), Zie Hallo [OData URI Conventions-specificatie](http://go.microsoft.com/fwlink/p/?LinkId=214806).

## <a name="comparison-operators"></a>Vergelijkingsoperators
Hallo worden volgende logische operators ondersteund voor alle eigenschaptypen:

| Logische operator | Beschrijving | Voorbeeld filtertekenreeks |
| --- | --- | --- |
| EQ |Gelijk zijn aan |Plaats-eq "Redmond" |
| gt |Groter dan |Prijs gt 20 |
| ge |Groter dan of gelijk te|Prijs ge 10 |
| lt |Kleiner dan |Prijs lt 20 |
| RP |Kleiner dan of gelijk zijn |Prijs RP 100 |
| ne |Niet gelijk aan |Plaats ne 'Londen' |
| en |En |Prijs RP 200 en prijs gt 3.5 |
| of |of |Prijs RP 3.5 of prijs gt 200 |
| niet |niet |niet isAvailable |

Bij het maken van een filtertekenreeks zijn hello volgende regels van belang:

* Hallo logische operators toocompare een eigenschapswaarde tooa gebruiken. Houd er rekening mee dat het is niet mogelijk toocompare tooa dynamische waarde van een eigenschap; een-zijde van Hallo-expressie moet een constante zijn.
* Alle onderdelen van de filtertekenreeks Hallo zijn hoofdlettergevoelig.
* Hallo constante waarde moet van het Hallo hetzelfde gegevenstype als de eigenschap hello om Hallo filter tooreturn geldige resultaten. Zie voor meer informatie over ondersteunde eigenschaptypen [Understanding Hallo Table Service Data Model](http://go.microsoft.com/fwlink/p/?LinkId=400448).

## <a name="filtering-on-string-properties"></a>Filteren op Eigenschappen
Wanneer u op Eigenschappen van een verbindingsreeks filtert, moet u Hallo tekenreeksconstante tussen enkele aanhalingstekens.

Hallo voorbeeld filters op Hallo volgen **PartitionKey** en **RowKey** eigenschappen; extra niet-sleutelkenmerk eigenschappen kunnen ook worden toegevoegd toohello filtertekenreeks:

    PartitionKey eq 'Partition1' and RowKey eq '00001'

U kunt haakjes elke filterexpressie, hoewel dit niet vereist is:

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

Houd er rekening mee dat Hallo tabel-service biedt geen ondersteuning voor query's met jokertekens en ze worden niet ondersteund in Hallo tabelontwerp ofwel. U kunt echter met behulp van vergelijkingsoperators op de gewenste voorvoegsel Hallo vergelijken van voorvoegsels uitvoeren. Hallo retourneert volgende voorbeeld entiteiten met een eigenschap LastName die begint met Hallo letter "A":

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a>Filteren op numerieke eigenschappen
toofilter op een geheel getal of een getal met drijvende komma, geef Hallo zonder aanhalingstekens.

In dit voorbeeld retourneert alle entiteiten met een eigenschap Age waarvan de waarde groter dan 30 is:

    Age gt 30

In dit voorbeeld retourneert alle entiteiten met een tegoed eigenschap waarvan de waarde is kleiner dan of gelijk zijn aan too100.25:

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a>Filteren op Boole-eigenschappen
toofilter op een Boolean opgeven **true** of **false** zonder aanhalingstekens.

Hallo volgende voorbeeld retourneert alle entiteiten waarbij Hallo IsActive eigenschap is ingesteld te**true**:

    IsActive eq true

U kunt ook deze filterexpressie zonder Hallo logische operator schrijven. In Hallo voorbeeld te volgen, Hallo tabelservice geeft ook alle entiteiten waarbij IsActive is **true**:

    IsActive

alle entiteiten waarbij IsActive False is, kunt u geen Hallo tooreturn operator:

    not IsActive

## <a name="filtering-on-datetime-properties"></a>Filteren op datum/tijd-eigenschappen
toofilter op een DateTime-waarde opgeven Hallo **datetime** sleutelwoord, gevolgd door Hallo datum/tijd constante in enkele aanhalingstekens. Hallo datum/tijd constante moet in gecombineerde UTC-notatie, zoals beschreven in [eigenschapswaarden voor datum/tijd opmaken](http://go.microsoft.com/fwlink/p/?LinkId=400449).

Hallo volgende voorbeeld retourneert entiteiten waarbij Hallo CustomerSince eigenschap is gelijk tooJuly 10, 2008:

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
