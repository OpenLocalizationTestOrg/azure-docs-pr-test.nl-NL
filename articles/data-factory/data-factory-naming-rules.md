---
title: aaaRules voor de naamgeving van Azure Data Factory-entiteiten | Microsoft Docs
description: Beschrijving van naamgevingsregels voor Data Factory-entiteiten.
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: bc5e801d-0b3b-48ec-9501-bb4146ea17f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 98c5fc5fc932b72b65894afad438b4dc321c8aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---naming-rules"></a><span data-ttu-id="223f9-103">Azure Data Factory - naamgevingsregels</span><span class="sxs-lookup"><span data-stu-id="223f9-103">Azure Data Factory - naming rules</span></span>
<span data-ttu-id="223f9-104">Hallo volgende tabel biedt naamgevingsregels voor Data Factory-artefacten.</span><span class="sxs-lookup"><span data-stu-id="223f9-104">hello following table provides naming rules for Data Factory artifacts.</span></span>

| <span data-ttu-id="223f9-105">Naam</span><span class="sxs-lookup"><span data-stu-id="223f9-105">Name</span></span> | <span data-ttu-id="223f9-106">Uniekheid van de naam</span><span class="sxs-lookup"><span data-stu-id="223f9-106">Name Uniqueness</span></span> | <span data-ttu-id="223f9-107">De validatie wordt gecontroleerd</span><span class="sxs-lookup"><span data-stu-id="223f9-107">Validation Checks</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="223f9-108">Data Factory</span><span class="sxs-lookup"><span data-stu-id="223f9-108">Data Factory</span></span> |<span data-ttu-id="223f9-109">Uniek zijn voor Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="223f9-109">Unique across Microsoft Azure.</span></span> <span data-ttu-id="223f9-110">Namen zijn niet hoofdlettergevoelig, dat wil zeggen, `MyDF` en `mydf` toohello verwijzen dezelfde gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="223f9-110">Names are case-insensitive, that is, `MyDF` and `mydf` refer toohello same data factory.</span></span> |<ul><li><span data-ttu-id="223f9-111">Elke gegevensfactory is gebonden tooexactly één Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="223f9-111">Each data factory is tied tooexactly one Azure subscription.</span></span></li><li><span data-ttu-id="223f9-112">Object-namen moeten beginnen met een letter of cijfer en mag alleen letters, cijfers en Hallo streepje (-) bevatten.</span><span class="sxs-lookup"><span data-stu-id="223f9-112">Object names must start with a letter or a number, and can contain only letters, numbers, and hello dash (-) character.</span></span></li><li><span data-ttu-id="223f9-113">Elk streepje (-) moet direct worden voorafgegaan en gevolgd door een letter of cijfer.</span><span class="sxs-lookup"><span data-stu-id="223f9-113">Every dash (-) character must be immediately preceded and followed by a letter or a number.</span></span> <span data-ttu-id="223f9-114">Twee opeenvolgende streepjes zijn in containernamen niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="223f9-114">Consecutive dashes are not permitted in container names.</span></span></li><li><span data-ttu-id="223f9-115">Naam mag 3-63 tekens lang zijn.</span><span class="sxs-lookup"><span data-stu-id="223f9-115">Name can be 3-63 characters long.</span></span></li></ul> |
| <span data-ttu-id="223f9-116">Gekoppelde Services/tabellen/pijplijnen</span><span class="sxs-lookup"><span data-stu-id="223f9-116">Linked Services/Tables/Pipelines</span></span> |<span data-ttu-id="223f9-117">Unieke met in een gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="223f9-117">Unique with in a data factory.</span></span> <span data-ttu-id="223f9-118">De namen zijn niet hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="223f9-118">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="223f9-119">Maximum aantal tekens in een tabelnaam: 260.</span><span class="sxs-lookup"><span data-stu-id="223f9-119">Maximum number of characters in a table name: 260.</span></span></li><li><span data-ttu-id="223f9-120">Objectnamen moeten beginnen met een letter, cijfer of een onderstrepingsteken (_).</span><span class="sxs-lookup"><span data-stu-id="223f9-120">Object names must start with a letter, number, or an underscore (_).</span></span></li><li><span data-ttu-id="223f9-121">Volgende tekens zijn niet toegestaan: '. ', '+ ','?', '/', ' < ', ' > "," * ","%","&",": ","\\"</span><span class="sxs-lookup"><span data-stu-id="223f9-121">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”, ”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |
| <span data-ttu-id="223f9-122">Resourcegroep</span><span class="sxs-lookup"><span data-stu-id="223f9-122">Resource Group</span></span> |<span data-ttu-id="223f9-123">Uniek zijn voor Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="223f9-123">Unique across Microsoft Azure.</span></span> <span data-ttu-id="223f9-124">De namen zijn niet hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="223f9-124">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="223f9-125">Maximum aantal tekens: 1000.</span><span class="sxs-lookup"><span data-stu-id="223f9-125">Maximum number of characters: 1000.</span></span></li><li><span data-ttu-id="223f9-126">Naam mag letters, cijfers en Hallo volgende tekens bevatten: '-', ' _ ',', 'en'. '</span><span class="sxs-lookup"><span data-stu-id="223f9-126">Name can contain letters, digits, and hello following characters: “-”, “_”, “,” and “.”</span></span></li></ul> |

