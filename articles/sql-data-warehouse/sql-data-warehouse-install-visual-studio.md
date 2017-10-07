---
title: aaaInstall Visual Studio en SSDT voor SQL Data Warehouse | Microsoft Docs
description: Visual Studio en SQL Server Development Tools (SSDT) voor Azure SQL Data Warehouse installeren
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 0ed9b406-9b42-4fe6-b963-fe0a5b48aac1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 03/30/2017
ms.author: anvang;barbkess
ms.openlocfilehash: cf49c13d5cab598ed127f5702c04168b62ede0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a><span data-ttu-id="9d907-103">Visual Studio en SSDT voor SQL datawarehouse installeren</span><span class="sxs-lookup"><span data-stu-id="9d907-103">Install Visual Studio and SSDT for SQL Data Warehouse</span></span>
<span data-ttu-id="9d907-104">toodevelop toepassingen voor SQL Data Warehouse, wordt u aangeraden meest recente versie van Visual Studio Hallo Hallo meest recente versie van SQL Server Data Tools (SSDT).</span><span class="sxs-lookup"><span data-stu-id="9d907-104">toodevelop applications for SQL Data Warehouse, we recommend using hello most recent version of Visual Studio with hello most recent version of SQL Server Data Tools (SSDT).</span></span>  <span data-ttu-id="9d907-105">Visual Studio 2013 Update 5 met SSDT wordt ook ondersteund voor compatibiliteit met eerdere versies.</span><span class="sxs-lookup"><span data-stu-id="9d907-105">Visual Studio 2013 Update 5 with SSDT is also supported for backward compatibility.</span></span>  

<span data-ttu-id="9d907-106">Met Visual Studio met SSDT kunt u toouse Hallo SQL Server Object Explorer toovisually verkennen tabellen, weergaven, opgeslagen procedures en veel meer objecten in uw SQL Data Warehouse, evenals een query's uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="9d907-106">Using Visual Studio with SSDT will allow you toouse hello SQL Server Object Explorer toovisually explore tables, views, stored procedures and many more objects in your SQL Data Warehouse as well as run queries.</span></span>

> [!NOTE]
> <span data-ttu-id="9d907-107">SQL Data Warehouse biedt nog geen ondersteuning voor Visual Studio-Database-projecten.</span><span class="sxs-lookup"><span data-stu-id="9d907-107">SQL Data Warehouse does not yet support Visual Studio Database Projects.</span></span>  <span data-ttu-id="9d907-108">Deze functie wordt in een toekomstige versie toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="9d907-108">This feature will be added in a future version.</span></span>
> 
> 

## <a name="step-1-install-visual-studio"></a><span data-ttu-id="9d907-109">Stap 1: Installeer Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9d907-109">Step 1: Install Visual Studio</span></span>
<span data-ttu-id="9d907-110">Volg deze koppelingen toodownload en installeer Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9d907-110">Follow these links toodownload and install Visual Studio.</span></span> <span data-ttu-id="9d907-111">Als u al hebt Visual Studio 2013 of hoger is geïnstalleerd, kunt u overslaan tooStep 2, SSDT installeren.</span><span class="sxs-lookup"><span data-stu-id="9d907-111">If you already have Visual Studio 2013 or later installed, you can skip tooStep 2, install SSDT.</span></span>

1. <span data-ttu-id="9d907-112">[Visual Studio downloaden][].</span><span class="sxs-lookup"><span data-stu-id="9d907-112">[Download Visual Studio][].</span></span>
2. <span data-ttu-id="9d907-113">Ga als volgt Hallo [Visual Studio installeren] [ Installing Visual Studio] leiden op MSDN en kies de standaardconfiguraties Hallo.</span><span class="sxs-lookup"><span data-stu-id="9d907-113">Follow hello [Installing Visual Studio][Installing Visual Studio] guide on MSDN and choose hello default configurations.</span></span>

## <a name="step-2-install-ssdt"></a><span data-ttu-id="9d907-114">Stap 2: SSDT installeren</span><span class="sxs-lookup"><span data-stu-id="9d907-114">Step 2: Install SSDT</span></span>
<span data-ttu-id="9d907-115">tooinstall SSDT voor Visual Studio kunt u controleren voor een SSDT-update van Visual Studio met de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="9d907-115">tooinstall SSDT for Visual Studio simply check for an SSDT update from within Visual Studio by following these steps.</span></span>

1. <span data-ttu-id="9d907-116">Klik in Visual Studio op **extra** / **uitbreidingen en Updates...**</span><span class="sxs-lookup"><span data-stu-id="9d907-116">In Visual Studio click on **Tools** / **Extensions and Updates…**</span></span><span data-ttu-id="9d907-117"> / **Updates**</span><span class="sxs-lookup"><span data-stu-id="9d907-117"> / **Updates**</span></span>
2. <span data-ttu-id="9d907-118">Selecteer **Product Updates** (Productupdates) en zoek naar **Microsoft SQL Server Update for database tooling** (Microsoft SQL Server Update voor databasehulpprogramma's)</span><span class="sxs-lookup"><span data-stu-id="9d907-118">Select **Product Updates** and then look for **Microsoft SQL Server Update for database tooling**</span></span>

<span data-ttu-id="9d907-119">Als een update niet wordt gevonden, moet u de meest recente versie Hallo geïnstalleerd hebben.</span><span class="sxs-lookup"><span data-stu-id="9d907-119">If an update is not found, then you should have hello latest version installed.</span></span>  <span data-ttu-id="9d907-120">tooconfirm SSDT is geïnstalleerd, klikt u op **Help** / **About Microsoft Visual Studio** en zoek naar SQL Server Data Tools in Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="9d907-120">tooconfirm SSDT is installed, click on **Help** / **About Microsoft Visual Studio** and look for SQL Server Data Tools in hello list.</span></span>  <span data-ttu-id="9d907-121">Hallo meest recente versie van SSDT is 14.0.60525.0.</span><span class="sxs-lookup"><span data-stu-id="9d907-121">hello latest version of SSDT is 14.0.60525.0.</span></span>  <span data-ttu-id="9d907-122">Als Hallo optie tooinstall niet beschikbaar vanuit Visual Studio is, u kunt ook kunt u bezoeken Hallo [SSDT downloaden] [ SSDT Download] toodownload pagina en SSDT handmatig installeren.</span><span class="sxs-lookup"><span data-stu-id="9d907-122">If hello option tooinstall is not available from Visual Studio, alternatively you can visit hello [SSDT Download][SSDT Download] page toodownload and install SSDT manually.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d907-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9d907-123">Next steps</span></span>
<span data-ttu-id="9d907-124">Nu dat u hebt de nieuwste versie van SSDT hello, bent u klaar te[verbinding] [ connect] tooyour SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9d907-124">Now that you have hello latest version of SSDT, you are ready too[connect][connect] tooyour SQL Data Warehouse.</span></span>

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
[Visual Studio downloaden]: https://www.visualstudio.com/downloads/
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
