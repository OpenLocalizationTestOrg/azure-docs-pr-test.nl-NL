---
title: Voorbeelden van Azure PowerShell - App Service | Microsoft Docs
description: Voorbeelden van Azure PowerShell - App Service
services: app-service
documentationcenter: app-service
author: syntaxc4
manager: erikre
editor: ggailey777
tags: azure-service-management
ms.assetid: b48d1137-8c04-46e0-b430-101e07d7e470
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 03/08/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 3254fdd57cfcd170f22374c1e3b058e6081d8e8e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-powershell-samples"></a><span data-ttu-id="adfa6-103">Voorbeelden van Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="adfa6-103">Azure PowerShell Samples</span></span>

<span data-ttu-id="adfa6-104">De volgende tabel bevat koppelingen naar bash-scripts die zijn gebouwd met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="adfa6-104">The following table includes links to bash scripts built using the Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="adfa6-105">**App maken**</span><span class="sxs-lookup"><span data-stu-id="adfa6-105">**Create app**</span></span>||
| [<span data-ttu-id="adfa6-106">Een web-app maken met de implementatie van GitHub</span><span class="sxs-lookup"><span data-stu-id="adfa6-106">Create a web app with deployment from GitHub</span></span>](./scripts/app-service-powershell-deploy-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="adfa6-107">Hiermee maakt u een Azure-web-app dat code vanuit GitHub haalt.</span><span class="sxs-lookup"><span data-stu-id="adfa6-107">Creates an Azure web app which pulls code from GitHub.</span></span> |
| [<span data-ttu-id="adfa6-108">Een web-app maken met doorlopende implementatie vanuit GitHub</span><span class="sxs-lookup"><span data-stu-id="adfa6-108">Create a web app with continuous deployment from GitHub</span></span>](./scripts/app-service-powershell-continuous-deployment-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="adfa6-109">Hiermee maakt u een Azure-web-app dat continu code vanuit GitHub implementeert.</span><span class="sxs-lookup"><span data-stu-id="adfa6-109">Creates an Azure web app which continuously deploys code from GitHub.</span></span> |
| [<span data-ttu-id="adfa6-110">Een web-app maken en implementeren van code met FTP</span><span class="sxs-lookup"><span data-stu-id="adfa6-110">Create a web app and deploy code with FTP</span></span>](./scripts/app-service-powershell-deploy-ftp.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="adfa6-111">Maakt een Azure-web-app en het uploaden van bestanden van een lokale map met FTP.</span><span class="sxs-lookup"><span data-stu-id="adfa6-111">Creates an Azure web app and upload files from a local directory using FTP.</span></span> |
| [<span data-ttu-id="adfa6-112">Een web-app maken en code implementeren vanuit een lokale Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="adfa6-112">Create a web app and deploy code from a local Git repository</span></span>](./scripts/app-service-powershell-deploy-local-git.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="adfa6-113">Een Azure-web-app maakt en configureert u code push van een lokale Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="adfa6-113">Creates an Azure web app and configures code push from a local Git repository.</span></span> |
| [<span data-ttu-id="adfa6-114">Een web-app maken en code implementeren in een faseringsomgeving</span><span class="sxs-lookup"><span data-stu-id="adfa6-114">Create a web app and deploy code to a staging environment</span></span>](./scripts/app-service-powershell-deploy-staging-environment.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="adfa6-115">Een Azure-web-app maakt met een implementatiesleuf voor het Faseren van codewijzigingen.</span><span class="sxs-lookup"><span data-stu-id="adfa6-115">Creates an Azure web app with a deployment slot for staging code changes.</span></span> |
|<span data-ttu-id="adfa6-116">**App configureren**</span><span class="sxs-lookup"><span data-stu-id="adfa6-116">**Configure app**</span></span>||
| [<span data-ttu-id="adfa6-117">Een aangepast domein aan een web-app toewijzen</span><span class="sxs-lookup"><span data-stu-id="adfa6-117">Map a custom domain to a web app</span></span>](./scripts/app-service-powershell-configure-custom-domain.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="adfa6-118">Een Azure-web-app maakt en wijst een aangepaste domeinnaam aan.</span><span class="sxs-lookup"><span data-stu-id="adfa6-118">Creates an Azure web app and maps a custom domain name to it.</span></span> |
| [<span data-ttu-id="adfa6-119">Een aangepaste SSL-certificaat binden aan een web-app</span><span class="sxs-lookup"><span data-stu-id="adfa6-119">Bind a custom SSL certificate to a web app</span></span>](./scripts/app-service-powershell-configure-ssl-certificate.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="adfa6-120">Een Azure-web-app maakt en koppelt het SSL-certificaat van een aangepaste domeinnaam aan deze.</span><span class="sxs-lookup"><span data-stu-id="adfa6-120">Creates an Azure web app and binds the SSL certificate of a custom domain name to it.</span></span> |
|<span data-ttu-id="adfa6-121">**Scale-app**</span><span class="sxs-lookup"><span data-stu-id="adfa6-121">**Scale app**</span></span>||
| [<span data-ttu-id="adfa6-122">Een web-app handmatig schalen</span><span class="sxs-lookup"><span data-stu-id="adfa6-122">Scale a web app manually</span></span>](./scripts/app-service-powershell-scale-manual.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="adfa6-123">Een Azure-web-app maakt en over 2 exemplaren op schaal.</span><span class="sxs-lookup"><span data-stu-id="adfa6-123">Creates an Azure web app and scales it across 2 instances.</span></span> |
| [<span data-ttu-id="adfa6-124">Een web-app wereldwijd schalen met een architectuur voor hoge beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="adfa6-124">Scale a web app worldwide with a high-availability architecture</span></span>](./scripts/app-service-powershell-scale-high-availability.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="adfa6-125">Maakt twee Azure-web-apps in twee verschillende geografische regio's en maakt u ze beschikbaar zijn via één eindpunt met behulp van Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="adfa6-125">Creates two Azure web apps in two different geographical regions and makes them available through a single endpoint using Azure Traffic Manager.</span></span> |
|<span data-ttu-id="adfa6-126">**App verbinden met resources**</span><span class="sxs-lookup"><span data-stu-id="adfa6-126">**Connect app to resources**</span></span>||
| [<span data-ttu-id="adfa6-127">Een WebApp verbinden met een SQL-Database</span><span class="sxs-lookup"><span data-stu-id="adfa6-127">Connect a web app to a SQL Database</span></span>](./scripts/app-service-powershell-connect-to-sql.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="adfa6-128">Hiermee maakt u een Azure-web-app en een SQL-database en vervolgens wordt de databaseverbindingsreeks toegevoegd aan de app-instellingen.</span><span class="sxs-lookup"><span data-stu-id="adfa6-128">Creates an Azure web app and a SQL database, then adds the database connection string to the app settings.</span></span> |
| [<span data-ttu-id="adfa6-129">Een web-app verbinden met een opslagaccount</span><span class="sxs-lookup"><span data-stu-id="adfa6-129">Connect a web app to a storage account</span></span>](./scripts/app-service-powershell-connect-to-storage.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="adfa6-130">Hiermee maakt u een Azure-web-app en een opslagaccount en vervolgens voegt u de verbindingsreeks voor opslag toe aan de app-instellingen.</span><span class="sxs-lookup"><span data-stu-id="adfa6-130">Creates an Azure web app and a storage account, then adds the storage connection string to the app settings.</span></span> |
|<span data-ttu-id="adfa6-131">**App controleren**</span><span class="sxs-lookup"><span data-stu-id="adfa6-131">**Monitor app**</span></span>||
| [<span data-ttu-id="adfa6-132">Een web-app bewaken met webserverlogboeken</span><span class="sxs-lookup"><span data-stu-id="adfa6-132">Monitor a web app with web server logs</span></span>](./scripts/app-service-powershell-monitor.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="adfa6-133">Een Azure-web-app maakt, schakelt logboekregistratie voor het en downloadt de logboeken naar uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="adfa6-133">Creates an Azure web app, enables logging for it, and downloads the logs to your local machine.</span></span> |
| | |
