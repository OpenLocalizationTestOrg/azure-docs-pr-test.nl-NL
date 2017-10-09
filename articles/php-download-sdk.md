---
title: aaaDownload hello Azure SDK voor PHP
description: Meer informatie over hoe toodownload en installeer hello Azure SDK voor PHP.
documentationcenter: php
services: app-service\web
author: allclark
manager: douge
editor: 
ms.assetid: bac355ac-4c25-42f4-8273-c5112eafa8d4
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 06/01/2016
ms.author: allclark;yaqiyang
ms.openlocfilehash: 94f56fc4f91bb175c08b9f7a43cb221c827694a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-azure-sdk-for-php"></a><span data-ttu-id="e27dd-103">Hello Azure SDK voor PHP downloaden</span><span class="sxs-lookup"><span data-stu-id="e27dd-103">Download hello Azure SDK for PHP</span></span>
## <a name="overview"></a><span data-ttu-id="e27dd-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="e27dd-104">Overview</span></span>
<span data-ttu-id="e27dd-105">Hello Azure SDK voor PHP omvat onderdelen waarmee u toodevelop, implementeren en beheren van PHP-toepassingen voor Azure.</span><span class="sxs-lookup"><span data-stu-id="e27dd-105">hello Azure SDK for PHP includes components that allow you toodevelop, deploy, and manage PHP applications for Azure.</span></span> <span data-ttu-id="e27dd-106">Hello Azure SDK voor PHP bevat met name de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="e27dd-106">Specifically, hello Azure SDK for PHP includes hello following:</span></span>

* <span data-ttu-id="e27dd-107">**PHP-clientbibliotheken voor Azure Hallo**.</span><span class="sxs-lookup"><span data-stu-id="e27dd-107">**hello PHP client libraries for Azure**.</span></span> <span data-ttu-id="e27dd-108">Deze klassenbibliotheken biedt een interface voor toegang tot Azure-functies, zoals services voor het beheer van gegevens en cloudservices.</span><span class="sxs-lookup"><span data-stu-id="e27dd-108">These class libraries provide an interface for accessing Azure features, such as data management services and cloud services.</span></span>  
* <span data-ttu-id="e27dd-109">**Hello Azure-opdrachtregelinterface voor Mac, Linux en Windows (Azure CLI)**.</span><span class="sxs-lookup"><span data-stu-id="e27dd-109">**hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)**.</span></span> <span data-ttu-id="e27dd-110">Dit is een reeks opdrachten voor het implementeren en beheren van Azure-services, zoals Azure Websites en Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="e27dd-110">This is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="e27dd-111">Hallo werk op elk platform, inclusief Mac, Linux en Windows Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e27dd-111">hello Azure CLI work on any platform, including Mac, Linux, and Windows.</span></span>
* <span data-ttu-id="e27dd-112">**Azure PowerShell (alleen Windows)**.</span><span class="sxs-lookup"><span data-stu-id="e27dd-112">**Azure PowerShell (Windows Only)**.</span></span> <span data-ttu-id="e27dd-113">Dit is een set PowerShell-cmdlets voor het implementeren en beheren van Azure-Services, zoals Cloudservices en virtuele Machines.</span><span class="sxs-lookup"><span data-stu-id="e27dd-113">This is a set of PowerShell cmdlets for deploying and managing Azure Services, such as Cloud Services and Virtual Machines.</span></span>
* <span data-ttu-id="e27dd-114">**Hallo (alleen Windows) Azure Emulators**.</span><span class="sxs-lookup"><span data-stu-id="e27dd-114">**hello Azure Emulators (Windows Only)**.</span></span> <span data-ttu-id="e27dd-115">Hallo berekeningen en opslag emulators zijn lokale emulators van cloudservices en -gegevens management services waarmee u een toepassing lokaal tootest.</span><span class="sxs-lookup"><span data-stu-id="e27dd-115">hello compute and storage emulators are local emulators of cloud services and data management services that allow you tootest an application locally.</span></span> <span data-ttu-id="e27dd-116">Hello Azure Emulators alleen op Windows worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e27dd-116">hello Azure Emulators run on Windows only.</span></span>

<span data-ttu-id="e27dd-117">Hallo in de volgende secties wordt beschreven hoe toodownload en installeer Hallo onderdelen die hierboven worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="e27dd-117">hello sections below describe how toodownload and install hello components described above.</span></span>

<span data-ttu-id="e27dd-118">Hallo instructies in dit onderwerp wordt ervan uitgegaan dat u hebt [PHP] [ install-php] geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="e27dd-118">hello instructions in this topic assume that you have [PHP][install-php] installed.</span></span>

> [!NOTE]
> <span data-ttu-id="e27dd-119">U moet PHP 5.5 of hoger toouse Hallo PHP-clientbibliotheken voor Azure hebben.</span><span class="sxs-lookup"><span data-stu-id="e27dd-119">You must have PHP 5.5 or higher toouse hello PHP client libraries for Azure.</span></span>
> 
> 

## <a name="php-client-libraries-for-azure"></a><span data-ttu-id="e27dd-120">PHP-clientbibliotheken voor Azure</span><span class="sxs-lookup"><span data-stu-id="e27dd-120">PHP client libraries for Azure</span></span>
<span data-ttu-id="e27dd-121">Hallo PHP-clientbibliotheken voor Azure biedt een interface voor toegang tot Azure-functies, zoals services voor het beheer van gegevens en in de cloud services, op een ander besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="e27dd-121">hello PHP Client Libraries for Azure provide an interface for accessing Azure features, such as data management services and cloud services, from any operating system.</span></span> <span data-ttu-id="e27dd-122">Deze bibliotheken kunnen worden geïnstalleerd via Hallo Composer.</span><span class="sxs-lookup"><span data-stu-id="e27dd-122">These libraries can be installed via hello Composer.</span></span>

<span data-ttu-id="e27dd-123">Zie voor meer informatie over hoe toouse PHP-clientbibliotheken voor Azure Hallo [hoe tooUse Blob-Service Hallo][blob-service], [hoe tooUse Tabelservice Hallo] [ table-service] en [hoe tooUse Queue-Service Hallo][queue-service].</span><span class="sxs-lookup"><span data-stu-id="e27dd-123">For information about how toouse hello PHP Client Libraries for Azure, see [How tooUse hello Blob Service][blob-service], [How tooUse hello Table Service][table-service] and [How tooUse hello Queue Service][queue-service].</span></span>

### <a name="install-via-composer"></a><span data-ttu-id="e27dd-124">Installeren via de Composer</span><span class="sxs-lookup"><span data-stu-id="e27dd-124">Install via Composer</span></span>
1. <span data-ttu-id="e27dd-125">[Installeer Git][install-git].</span><span class="sxs-lookup"><span data-stu-id="e27dd-125">[Install Git][install-git].</span></span>

    > [AZURE.NOTE] <span data-ttu-id="e27dd-126">Op Windows moet u ook tooadd Hallo Git uitvoerbare tooyour pad-omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="e27dd-126">On Windows, you will also need tooadd hello Git executable tooyour PATH environment variable.</span></span>

1. <span data-ttu-id="e27dd-127">Maak een bestand met de naam **composer.json** in Hallo hoofdmap van uw project en voeg Hallo code tooit te volgen:</span><span class="sxs-lookup"><span data-stu-id="e27dd-127">Create a file named **composer.json** in hello root of your project and add hello following code tooit:</span></span>
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. <span data-ttu-id="e27dd-128">Download  **[composer.phar] [ composer-phar]**  in de hoofdmap van uw project.</span><span class="sxs-lookup"><span data-stu-id="e27dd-128">Download **[composer.phar][composer-phar]** in your project root.</span></span>
3. <span data-ttu-id="e27dd-129">Open een opdrachtprompt en dit in de hoofdmap van uw project uitvoeren</span><span class="sxs-lookup"><span data-stu-id="e27dd-129">Open a command prompt and execute this in your project root</span></span>
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a><span data-ttu-id="e27dd-130">Azure PowerShell en Azure Emulators</span><span class="sxs-lookup"><span data-stu-id="e27dd-130">Azure PowerShell and Azure Emulators</span></span>
<span data-ttu-id="e27dd-131">Azure PowerShell is een set PowerShell-cmdlets voor het implementeren en beheren van Azure-Services (zoals Cloudservices en virtuele Machines).</span><span class="sxs-lookup"><span data-stu-id="e27dd-131">Azure PowerShell is a set of PowerShell cmdlets for deploying and managing Azure Services (such as Cloud Services and Virtual Machines).</span></span> <span data-ttu-id="e27dd-132">Hello Azure Emulators zijn emulators van cloudservices en -gegevens management services waarmee u een toepassing lokaal tootest.</span><span class="sxs-lookup"><span data-stu-id="e27dd-132">hello Azure Emulators are emulators of cloud services and data management services that allow you tootest an application locally.</span></span> <span data-ttu-id="e27dd-133">Deze onderdelen worden ondersteund. alleen Windows.</span><span class="sxs-lookup"><span data-stu-id="e27dd-133">These components are supported Windows only.</span></span>

<span data-ttu-id="e27dd-134">Hallo aanbevolen manier tooinstall Azure PowerShell en hello Azure Emulators is toouse hello [Microsoft Web Platform Installer][download-wpi].</span><span class="sxs-lookup"><span data-stu-id="e27dd-134">hello recommended way tooinstall Azure PowerShell and hello Azure Emulators is toouse hello [Microsoft Web Platform Installer][download-wpi].</span></span> <span data-ttu-id="e27dd-135">Houd er rekening mee dat u ook tooinstall andere onderdelen van de ontwikkeling, zoals PHP, SQL Server, Microsoft-Drivers Hallo voor SQL Server voor PHP en WebMatrix kunt.</span><span class="sxs-lookup"><span data-stu-id="e27dd-135">Note that you can also choose tooinstall other development components, such as PHP, SQL Server, hello Microsoft Drivers for SQL Server for PHP, and WebMatrix.</span></span>

<span data-ttu-id="e27dd-136">Voor informatie over het toouse Azure PowerShell, Zie [hoe tooUse Azure PowerShell][powershell-tools].</span><span class="sxs-lookup"><span data-stu-id="e27dd-136">For information about how toouse Azure PowerShell, see [How tooUse Azure PowerShell][powershell-tools].</span></span>

## <a name="azure-cli"></a><span data-ttu-id="e27dd-137">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e27dd-137">Azure CLI</span></span>
<span data-ttu-id="e27dd-138">Hello Azure CLI is een reeks opdrachten voor het implementeren en beheren van Azure-services, zoals Azure Websites en Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="e27dd-138">hello Azure CLI is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="e27dd-139">Zie voor meer informatie over het installeren van Azure CLI [installeren hello Azure CLI](cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e27dd-139">For information about installing Azure CLI, see [Install hello Azure CLI](cli-install-nodejs.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e27dd-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e27dd-140">Next steps</span></span>
<span data-ttu-id="e27dd-141">Zie voor meer informatie, Hallo [PHP-ontwikkelaarscentrum](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="e27dd-141">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[composer-github]: https://github.com/composer/composer
[composer-phar]: http://getcomposer.org/composer.phar
[nodejs-org]: http://nodejs.org/
[install-node-linux]: https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager
[download-wpi]: http://go.microsoft.com/fwlink/?LinkId=253447
[mac-installer]: http://go.microsoft.com/fwlink/?LinkId=252249
[blob-service]: http://go.microsoft.com/fwlink/?LinkId=252714
[table-service]: http://go.microsoft.com/fwlink/?LinkId=252715
[queue-service]: http://go.microsoft.com/fwlink/?LinkId=252716
[azure cli]: http://go.microsoft.com/fwlink/?LinkId=252717
[powershell-tools]: http://go.microsoft.com/fwlink/?LinkId=252718
[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
