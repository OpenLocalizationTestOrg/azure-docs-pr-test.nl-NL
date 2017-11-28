---
title: Voor het verbinden met Azure Analysis Services is nodig clientbibliotheken | Microsoft Docs
description: Beschrijft de clientbibliotheken vereist is voor clienttoepassingen en hulpprogramma's om verbinding maken met Azure Analysis Services
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
ms.openlocfilehash: a96e7fe671dc051da35168fa7b49ecba53b4c4a5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="client-libraries-for-connecting-to-azure-analysis-services"></a><span data-ttu-id="6e171-103">Clientbibliotheken voor het verbinden met Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="6e171-103">Client libraries for connecting to Azure Analysis Services</span></span>

<span data-ttu-id="6e171-104">Clientbibliotheken zijn nodig voor client-toepassingen en hulpprogramma's die verbinding maken met Analysis Services-servers.</span><span class="sxs-lookup"><span data-stu-id="6e171-104">Client libraries are necessary for client applications and tools to connect to Analysis Services servers.</span></span> 

<span data-ttu-id="6e171-105">Analyseservices gebruikmaken van drie clientbibliotheken.</span><span class="sxs-lookup"><span data-stu-id="6e171-105">Analysis Services utilize three client libraries.</span></span> <span data-ttu-id="6e171-106">ADOMD.NET en Analysis Services Management Objects (AMO), zijn beheerde clientbibliotheken.</span><span class="sxs-lookup"><span data-stu-id="6e171-106">ADOMD.NET and Analysis Services Management Objects (AMO), are managed client libraries.</span></span> <span data-ttu-id="6e171-107">De Analysis Services OLE DB-provider (MSOLAP DLL) is een native clientbibliotheek.</span><span class="sxs-lookup"><span data-stu-id="6e171-107">The Analysis Services OLE DB provider (MSOLAP DLL) is a native client library.</span></span> <span data-ttu-id="6e171-108">Alle drie worden doorgaans geïnstalleerd op hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="6e171-108">Typically, all three are installed at the same time.</span></span> <span data-ttu-id="6e171-109">Azure Analysis Services is vereist voor de meest recente versies.</span><span class="sxs-lookup"><span data-stu-id="6e171-109">Azure Analysis Services requires the latest versions.</span></span> 

<span data-ttu-id="6e171-110">Microsoft-clienttoepassingen, zoals Power BI Desktop- en Excel installeren alle drie clientbibliotheken.</span><span class="sxs-lookup"><span data-stu-id="6e171-110">Microsoft client applications such as Power BI Desktop and Excel install all three client libraries.</span></span> <span data-ttu-id="6e171-111">Echter, afhankelijk van de versie of de frequentie van updates, clientbibliotheken mogelijk niet de meest recente versies die vereist zijn voor Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="6e171-111">However, depending on the version or frequency of updates, client libraries may not be the latest versions required by Azure Analysis Services.</span></span> <span data-ttu-id="6e171-112">Dit geldt ook voor aangepaste toepassingen of andere interfaces, zoals AsCmd, TOM en ADOMD.NET.</span><span class="sxs-lookup"><span data-stu-id="6e171-112">The same applies to custom applications or other interfaces such as AsCmd, TOM, ADOMD.NET.</span></span> <span data-ttu-id="6e171-113">Deze toepassingen moet handmatig installeren van de tapewisselaars.</span><span class="sxs-lookup"><span data-stu-id="6e171-113">These applications require manually installing the libraries.</span></span> <span data-ttu-id="6e171-114">De clientbibliotheken voor handmatige installatie zijn opgenomen in SQL Server featurepacks die als pakketten te distribueren.</span><span class="sxs-lookup"><span data-stu-id="6e171-114">The client libraries for manual installation are included in SQL Server feature packs as distributable packages.</span></span> <span data-ttu-id="6e171-115">Echter deze clientbibliotheken zijn gekoppeld aan de SQL Server-versie en mogelijk niet de nieuwste versie.</span><span class="sxs-lookup"><span data-stu-id="6e171-115">However, these client libraries are tied to the SQL Server version and may not be the latest.</span></span>  

<span data-ttu-id="6e171-116">Clientbibliotheken voor clientverbindingen zijn anders dan gegevensproviders waarmee verbinding wordt gemaakt van een Azure Analysis Services-server met een gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="6e171-116">Client libraries for client connections are different from data providers required to connect from an Azure Analysis Services server to a data source.</span></span> <span data-ttu-id="6e171-117">Zie voor meer informatie over datasource-verbindingen, [Datasource verbindingen](analysis-services-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="6e171-117">To learn more about datasource connections, see [Datasource connections](analysis-services-datasource.md).</span></span>

## <a name="download-the-latest-client-libraries"></a><span data-ttu-id="6e171-118">Download de meest recente clientbibliotheken</span><span class="sxs-lookup"><span data-stu-id="6e171-118">Download the latest client libraries</span></span>  
<span data-ttu-id="6e171-119">De volgende clientbibliotheken gebruiken als u in een productieomgeving en volledig vrijgegeven en ondersteunde versies vereist.</span><span class="sxs-lookup"><span data-stu-id="6e171-119">Use the following client libraries if you are in a production environment and require fully released and supported versions.</span></span>

[<span data-ttu-id="6e171-120">MSOLAP (amd64)</span><span class="sxs-lookup"><span data-stu-id="6e171-120">MSOLAP (amd64)</span></span>](https://go.microsoft.com/fwlink/?linkid=829576)</br><span data-ttu-id="6e171-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span><span class="sxs-lookup"><span data-stu-id="6e171-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span></span></br><span data-ttu-id="6e171-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span><span class="sxs-lookup"><span data-stu-id="6e171-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span></span></br><span data-ttu-id="6e171-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span><span class="sxs-lookup"><span data-stu-id="6e171-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="6e171-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6e171-124">Next steps</span></span>
<span data-ttu-id="6e171-125">[Verbinding maken met Excel](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="6e171-125">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
[<span data-ttu-id="6e171-126">Verbinden met Power BI</span><span class="sxs-lookup"><span data-stu-id="6e171-126">Connect with Power BI</span></span>](analysis-services-connect-pbi.md)
