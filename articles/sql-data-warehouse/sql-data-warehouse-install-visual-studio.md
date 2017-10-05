---
title: Visual Studio en SSDT voor SQL datawarehouse installeren | Microsoft Docs
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
ms.openlocfilehash: f7023b78c241a7bc8014276cd0bfa455165b42cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a><span data-ttu-id="f88cb-103">Visual Studio en SSDT voor SQL datawarehouse installeren</span><span class="sxs-lookup"><span data-stu-id="f88cb-103">Install Visual Studio and SSDT for SQL Data Warehouse</span></span>
<span data-ttu-id="f88cb-104">Voor het ontwikkelen van toepassingen voor SQL Data Warehouse, wordt u aangeraden de meest recente versie van Visual Studio met de meest recente versie van SQL Server Data Tools (SSDT).</span><span class="sxs-lookup"><span data-stu-id="f88cb-104">To develop applications for SQL Data Warehouse, we recommend using the most recent version of Visual Studio with the most recent version of SQL Server Data Tools (SSDT).</span></span>  <span data-ttu-id="f88cb-105">Visual Studio 2013 Update 5 met SSDT wordt ook ondersteund voor compatibiliteit met eerdere versies.</span><span class="sxs-lookup"><span data-stu-id="f88cb-105">Visual Studio 2013 Update 5 with SSDT is also supported for backward compatibility.</span></span>  

<span data-ttu-id="f88cb-106">Wanneer u Visual Studio met SSDT gebruikt, kunt u de SQL Server-objectverkenner gebruiken om tabellen, weergaven, opgeslagen procedures en nog veel meer objecten in de SQL Data Warehouse visueel te verkennen, en kunt u query's uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f88cb-106">Using Visual Studio with SSDT will allow you to use the SQL Server Object Explorer to visually explore tables, views, stored procedures and many more objects in your SQL Data Warehouse as well as run queries.</span></span>

> [!NOTE]
> <span data-ttu-id="f88cb-107">SQL Data Warehouse biedt nog geen ondersteuning voor Visual Studio-Database-projecten.</span><span class="sxs-lookup"><span data-stu-id="f88cb-107">SQL Data Warehouse does not yet support Visual Studio Database Projects.</span></span>  <span data-ttu-id="f88cb-108">Deze functie wordt in een toekomstige versie toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="f88cb-108">This feature will be added in a future version.</span></span>
> 
> 

## <a name="step-1-install-visual-studio"></a><span data-ttu-id="f88cb-109">Stap 1: Installeer Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f88cb-109">Step 1: Install Visual Studio</span></span>
<span data-ttu-id="f88cb-110">Volg deze koppelingen wilt downloaden en installeren van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f88cb-110">Follow these links to download and install Visual Studio.</span></span> <span data-ttu-id="f88cb-111">Als u al Visual Studio 2013 hebt of hoger is geïnstalleerd, kunt u doorgaan met stap 2, SSDT installeren.</span><span class="sxs-lookup"><span data-stu-id="f88cb-111">If you already have Visual Studio 2013 or later installed, you can skip to Step 2, install SSDT.</span></span>

1. <span data-ttu-id="f88cb-112">[Visual Studio downloaden][].</span><span class="sxs-lookup"><span data-stu-id="f88cb-112">[Download Visual Studio][].</span></span>
2. <span data-ttu-id="f88cb-113">Ga als volgt de [Visual Studio installeren] [ Installing Visual Studio] leiden op MSDN en kies de standaardconfiguraties.</span><span class="sxs-lookup"><span data-stu-id="f88cb-113">Follow the [Installing Visual Studio][Installing Visual Studio] guide on MSDN and choose the default configurations.</span></span>

## <a name="step-2-install-ssdt"></a><span data-ttu-id="f88cb-114">Stap 2: SSDT installeren</span><span class="sxs-lookup"><span data-stu-id="f88cb-114">Step 2: Install SSDT</span></span>
<span data-ttu-id="f88cb-115">Als u SSDT voor Visual Studio wilt installeren, voert u de volgende stappen uit om in Visual Studio op een SSDT-update te controleren.</span><span class="sxs-lookup"><span data-stu-id="f88cb-115">To install SSDT for Visual Studio simply check for an SSDT update from within Visual Studio by following these steps.</span></span>

1. <span data-ttu-id="f88cb-116">Klik in Visual Studio op **extra** / **uitbreidingen en Updates...**</span><span class="sxs-lookup"><span data-stu-id="f88cb-116">In Visual Studio click on **Tools** / **Extensions and Updates…**</span></span><span data-ttu-id="f88cb-117"> / **Updates**</span><span class="sxs-lookup"><span data-stu-id="f88cb-117"> / **Updates**</span></span>
2. <span data-ttu-id="f88cb-118">Selecteer **Product Updates** (Productupdates) en zoek naar **Microsoft SQL Server Update for database tooling** (Microsoft SQL Server Update voor databasehulpprogramma's)</span><span class="sxs-lookup"><span data-stu-id="f88cb-118">Select **Product Updates** and then look for **Microsoft SQL Server Update for database tooling**</span></span>

<span data-ttu-id="f88cb-119">Als er geen update wordt gevonden, hebt u de meest recente versie al geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="f88cb-119">If an update is not found, then you should have the latest version installed.</span></span>  <span data-ttu-id="f88cb-120">Als u wilt controleren of SSDT is geïnstalleerd, klikt u op **Help** / **About Microsoft Visual Studio** (Help > Info) en zoekt u in de lijst naar SQL Server Data Tools.</span><span class="sxs-lookup"><span data-stu-id="f88cb-120">To confirm SSDT is installed, click on **Help** / **About Microsoft Visual Studio** and look for SQL Server Data Tools in the list.</span></span>  <span data-ttu-id="f88cb-121">De meest recente versie van SSDT is 14.0.60525.0.</span><span class="sxs-lookup"><span data-stu-id="f88cb-121">The latest version of SSDT is 14.0.60525.0.</span></span>  <span data-ttu-id="f88cb-122">Als de optie voor het installeren van niet beschikbaar vanuit Visual Studio is, u kunt ook kunt u via de [SSDT downloaden] [ SSDT Download] pagina om te downloaden en SSDT handmatig installeren.</span><span class="sxs-lookup"><span data-stu-id="f88cb-122">If the option to install is not available from Visual Studio, alternatively you can visit the [SSDT Download][SSDT Download] page to download and install SSDT manually.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f88cb-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f88cb-123">Next steps</span></span>
<span data-ttu-id="f88cb-124">Nu dat u de nieuwste versie van SSDT hebt, bent u klaar om te [verbinding] [ connect] met uw SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f88cb-124">Now that you have the latest version of SSDT, you are ready to [connect][connect] to your SQL Data Warehouse.</span></span>

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
<span data-ttu-id="f88cb-125">[Visual Studio downloaden]: https://www.visualstudio.com/downloads/</span><span class="sxs-lookup"><span data-stu-id="f88cb-125">[Download Visual Studio]: https://www.visualstudio.com/downloads/</span></span>
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
