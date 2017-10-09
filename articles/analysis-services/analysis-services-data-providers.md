---
title: aaaClient bibliotheken die vereist zijn voor het verbinden van tooAzure Analysis Services | Microsoft Docs
description: Beschrijft de clientbibliotheken vereist is voor client toepassingen en hulpprogramma's tooconnect Azure Analysis Services
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 74ba5c05ba76c6587c5aed38f200a1ba469aa4f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="client-libraries-for-connecting-tooazure-analysis-services"></a><span data-ttu-id="6d637-103">Clientbibliotheken voor het verbinden van tooAzure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="6d637-103">Client libraries for connecting tooAzure Analysis Services</span></span>

<span data-ttu-id="6d637-104">Clientbibliotheken zijn nodig voor client-toepassingen en hulpprogramma's tooconnect tooAnalysis Services-servers.</span><span class="sxs-lookup"><span data-stu-id="6d637-104">Client libraries are necessary for client applications and tools tooconnect tooAnalysis Services servers.</span></span> 

<span data-ttu-id="6d637-105">Analyseservices gebruikmaken van drie clientbibliotheken.</span><span class="sxs-lookup"><span data-stu-id="6d637-105">Analysis Services utilize three client libraries.</span></span> <span data-ttu-id="6d637-106">ADOMD.NET en Analysis Services Management Objects (AMO), zijn beheerde clientbibliotheken.</span><span class="sxs-lookup"><span data-stu-id="6d637-106">ADOMD.NET and Analysis Services Management Objects (AMO), are managed client libraries.</span></span> <span data-ttu-id="6d637-107">Hallo Analysis Services OLE DB-provider (MSOLAP DLL) is een native clientbibliotheek.</span><span class="sxs-lookup"><span data-stu-id="6d637-107">hello Analysis Services OLE DB provider (MSOLAP DLL) is a native client library.</span></span> <span data-ttu-id="6d637-108">Normaal gesproken alle drie worden geïnstalleerd op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="6d637-108">Typically, all three are installed at hello same time.</span></span> <span data-ttu-id="6d637-109">Azure Analysis Services is de meest recente versies Hallo vereist.</span><span class="sxs-lookup"><span data-stu-id="6d637-109">Azure Analysis Services requires hello latest versions.</span></span> 

<span data-ttu-id="6d637-110">Microsoft-clienttoepassingen, zoals Power BI Desktop- en Excel installeren alle drie clientbibliotheken.</span><span class="sxs-lookup"><span data-stu-id="6d637-110">Microsoft client applications such as Power BI Desktop and Excel install all three client libraries.</span></span> <span data-ttu-id="6d637-111">Echter, afhankelijk van het Hallo-versie of -frequentie van updates, clientbibliotheken mogelijk niet de nieuwste versies Hallo vereist door Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="6d637-111">However, depending on hello version or frequency of updates, client libraries may not be hello latest versions required by Azure Analysis Services.</span></span> <span data-ttu-id="6d637-112">Hallo geldt toocustom toepassingen of andere interfaces zoals AsCmd, aangepaste, ADOMD.NET.</span><span class="sxs-lookup"><span data-stu-id="6d637-112">hello same applies toocustom applications or other interfaces such as AsCmd, TOM, ADOMD.NET.</span></span> <span data-ttu-id="6d637-113">Deze toepassingen vereisen Hallo tapewisselaars handmatig te installeren.</span><span class="sxs-lookup"><span data-stu-id="6d637-113">These applications require manually installing hello libraries.</span></span> <span data-ttu-id="6d637-114">Hallo-clientbibliotheken voor handmatige installatie zijn opgenomen in SQL Server featurepacks die als pakketten te distribueren.</span><span class="sxs-lookup"><span data-stu-id="6d637-114">hello client libraries for manual installation are included in SQL Server feature packs as distributable packages.</span></span> <span data-ttu-id="6d637-115">Deze clientbibliotheken zijn echter gebonden toohello SQL Server-versie en zijn mogelijk niet Hallo meest recente.</span><span class="sxs-lookup"><span data-stu-id="6d637-115">However, these client libraries are tied toohello SQL Server version and may not be hello latest.</span></span>  

<span data-ttu-id="6d637-116">Clientbibliotheken voor clientverbindingen zijn anders dan data providers vereist tooconnect uit een Azure Analysis Services server tooa-gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="6d637-116">Client libraries for client connections are different from data providers required tooconnect from an Azure Analysis Services server tooa data source.</span></span> <span data-ttu-id="6d637-117">toolearn meer informatie over de datasource-verbindingen, Zie [Datasource verbindingen](analysis-services-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="6d637-117">toolearn more about datasource connections, see [Datasource connections](analysis-services-datasource.md).</span></span>

## <a name="download-hello-latest-client-libraries"></a><span data-ttu-id="6d637-118">Download de meest recente clientbibliotheken Hallo</span><span class="sxs-lookup"><span data-stu-id="6d637-118">Download hello latest client libraries</span></span>  
<span data-ttu-id="6d637-119">Gebruik Hallo clientbibliotheken volgen als u in een productieomgeving en volledig vrijgegeven en ondersteunde versies vereist.</span><span class="sxs-lookup"><span data-stu-id="6d637-119">Use hello following client libraries if you are in a production environment and require fully released and supported versions.</span></span>

[<span data-ttu-id="6d637-120">MSOLAP (amd64)</span><span class="sxs-lookup"><span data-stu-id="6d637-120">MSOLAP (amd64)</span></span>](https://go.microsoft.com/fwlink/?linkid=829576)</br><span data-ttu-id="6d637-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span><span class="sxs-lookup"><span data-stu-id="6d637-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span></span></br><span data-ttu-id="6d637-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span><span class="sxs-lookup"><span data-stu-id="6d637-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span></span></br><span data-ttu-id="6d637-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span><span class="sxs-lookup"><span data-stu-id="6d637-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="6d637-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6d637-124">Next steps</span></span>
<span data-ttu-id="6d637-125">[Verbinding maken met Excel](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="6d637-125">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
[<span data-ttu-id="6d637-126">Verbinden met Power BI</span><span class="sxs-lookup"><span data-stu-id="6d637-126">Connect with Power BI</span></span>](analysis-services-connect-pbi.md)
