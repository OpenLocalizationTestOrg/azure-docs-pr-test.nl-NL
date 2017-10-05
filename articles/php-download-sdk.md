---
title: De Azure SDK voor PHP downloaden
description: Informatie over het downloaden en installeren van de Azure SDK voor PHP.
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
ms.openlocfilehash: fd3d28b133ef8e646f5c2f1c1127f654daa61b95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="download-the-azure-sdk-for-php"></a><span data-ttu-id="c87bf-103">De Azure SDK voor PHP downloaden</span><span class="sxs-lookup"><span data-stu-id="c87bf-103">Download the Azure SDK for PHP</span></span>
## <a name="overview"></a><span data-ttu-id="c87bf-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="c87bf-104">Overview</span></span>
<span data-ttu-id="c87bf-105">De Azure SDK voor PHP omvat onderdelen waarmee u kunt ontwikkelen, implementeren en beheren van PHP-toepassingen voor Azure.</span><span class="sxs-lookup"><span data-stu-id="c87bf-105">The Azure SDK for PHP includes components that allow you to develop, deploy, and manage PHP applications for Azure.</span></span> <span data-ttu-id="c87bf-106">De Azure SDK voor PHP bevat met name de volgende:</span><span class="sxs-lookup"><span data-stu-id="c87bf-106">Specifically, the Azure SDK for PHP includes the following:</span></span>

* <span data-ttu-id="c87bf-107">**De PHP-clientbibliotheken voor Azure**.</span><span class="sxs-lookup"><span data-stu-id="c87bf-107">**The PHP client libraries for Azure**.</span></span> <span data-ttu-id="c87bf-108">Deze klassenbibliotheken biedt een interface voor toegang tot Azure-functies, zoals services voor het beheer van gegevens en cloudservices.</span><span class="sxs-lookup"><span data-stu-id="c87bf-108">These class libraries provide an interface for accessing Azure features, such as data management services and cloud services.</span></span>  
* <span data-ttu-id="c87bf-109">**De Azure-opdrachtregelinterface voor Mac, Linux en Windows (Azure CLI)**.</span><span class="sxs-lookup"><span data-stu-id="c87bf-109">**The Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)**.</span></span> <span data-ttu-id="c87bf-110">Dit is een reeks opdrachten voor het implementeren en beheren van Azure-services, zoals Azure Websites en Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="c87bf-110">This is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="c87bf-111">Het werk van de Azure CLI op elk platform, inclusief Mac, Linux en Windows.</span><span class="sxs-lookup"><span data-stu-id="c87bf-111">The Azure CLI work on any platform, including Mac, Linux, and Windows.</span></span>
* <span data-ttu-id="c87bf-112">**Azure PowerShell (alleen Windows)**.</span><span class="sxs-lookup"><span data-stu-id="c87bf-112">**Azure PowerShell (Windows Only)**.</span></span> <span data-ttu-id="c87bf-113">Dit is een set PowerShell-cmdlets voor het implementeren en beheren van Azure-Services, zoals Cloudservices en virtuele Machines.</span><span class="sxs-lookup"><span data-stu-id="c87bf-113">This is a set of PowerShell cmdlets for deploying and managing Azure Services, such as Cloud Services and Virtual Machines.</span></span>
* <span data-ttu-id="c87bf-114">**De Azure Emulators (alleen Windows)**.</span><span class="sxs-lookup"><span data-stu-id="c87bf-114">**The Azure Emulators (Windows Only)**.</span></span> <span data-ttu-id="c87bf-115">De berekenings- en emulators zijn lokale emulators van cloudservices en -gegevens management services waarmee u een toepassing lokaal te testen.</span><span class="sxs-lookup"><span data-stu-id="c87bf-115">The compute and storage emulators are local emulators of cloud services and data management services that allow you to test an application locally.</span></span> <span data-ttu-id="c87bf-116">De Azure-Emulators alleen op Windows worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c87bf-116">The Azure Emulators run on Windows only.</span></span>

<span data-ttu-id="c87bf-117">De volgende secties wordt beschreven hoe downloaden en installeren van de onderdelen die hierboven worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="c87bf-117">The sections below describe how to download and install the components described above.</span></span>

<span data-ttu-id="c87bf-118">De instructies in dit onderwerp wordt ervan uitgegaan dat u hebt [PHP] [ install-php] geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="c87bf-118">The instructions in this topic assume that you have [PHP][install-php] installed.</span></span>

> [!NOTE]
> <span data-ttu-id="c87bf-119">U kunt PHP 5.5 of hoger de PHP-clientbibliotheken gebruiken voor Azure moet hebben.</span><span class="sxs-lookup"><span data-stu-id="c87bf-119">You must have PHP 5.5 or higher to use the PHP client libraries for Azure.</span></span>
> 
> 

## <a name="php-client-libraries-for-azure"></a><span data-ttu-id="c87bf-120">PHP-clientbibliotheken voor Azure</span><span class="sxs-lookup"><span data-stu-id="c87bf-120">PHP client libraries for Azure</span></span>
<span data-ttu-id="c87bf-121">De PHP-clientbibliotheken voor Azure biedt een interface voor toegang tot Azure-functies, zoals services voor het beheer van gegevens en in de cloud services, op een ander besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="c87bf-121">The PHP Client Libraries for Azure provide an interface for accessing Azure features, such as data management services and cloud services, from any operating system.</span></span> <span data-ttu-id="c87bf-122">Deze bibliotheken kunnen worden geïnstalleerd via de Composer.</span><span class="sxs-lookup"><span data-stu-id="c87bf-122">These libraries can be installed via the Composer.</span></span>

<span data-ttu-id="c87bf-123">Zie voor meer informatie over het gebruik van de PHP-clientbibliotheken voor Azure [het gebruik van de Blob-Service][blob-service], [het gebruik van de Tabelservice] [ table-service]en [het gebruik van de Queue-Service][queue-service].</span><span class="sxs-lookup"><span data-stu-id="c87bf-123">For information about how to use the PHP Client Libraries for Azure, see [How to Use the Blob Service][blob-service], [How to Use the Table Service][table-service] and [How to Use the Queue Service][queue-service].</span></span>

### <a name="install-via-composer"></a><span data-ttu-id="c87bf-124">Installeren via de Composer</span><span class="sxs-lookup"><span data-stu-id="c87bf-124">Install via Composer</span></span>
1. <span data-ttu-id="c87bf-125">[Installeer Git][install-git].</span><span class="sxs-lookup"><span data-stu-id="c87bf-125">[Install Git][install-git].</span></span>

    > [AZURE.NOTE] <span data-ttu-id="c87bf-126">In Windows moet u ook de uitvoerbare Git toevoegen aan de omgevingsvariabele PATH.</span><span class="sxs-lookup"><span data-stu-id="c87bf-126">On Windows, you will also need to add the Git executable to your PATH environment variable.</span></span>

1. <span data-ttu-id="c87bf-127">Maak een bestand met de naam **composer.json** in de hoofdmap van uw project en voeg de volgende code toe:</span><span class="sxs-lookup"><span data-stu-id="c87bf-127">Create a file named **composer.json** in the root of your project and add the following code to it:</span></span>
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. <span data-ttu-id="c87bf-128">Download  **[composer.phar] [ composer-phar]**  in de hoofdmap van uw project.</span><span class="sxs-lookup"><span data-stu-id="c87bf-128">Download **[composer.phar][composer-phar]** in your project root.</span></span>
3. <span data-ttu-id="c87bf-129">Open een opdrachtprompt en dit in de hoofdmap van uw project uitvoeren</span><span class="sxs-lookup"><span data-stu-id="c87bf-129">Open a command prompt and execute this in your project root</span></span>
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a><span data-ttu-id="c87bf-130">Azure PowerShell en Azure Emulators</span><span class="sxs-lookup"><span data-stu-id="c87bf-130">Azure PowerShell and Azure Emulators</span></span>
<span data-ttu-id="c87bf-131">Azure PowerShell is een set PowerShell-cmdlets voor het implementeren en beheren van Azure-Services (zoals Cloudservices en virtuele Machines).</span><span class="sxs-lookup"><span data-stu-id="c87bf-131">Azure PowerShell is a set of PowerShell cmdlets for deploying and managing Azure Services (such as Cloud Services and Virtual Machines).</span></span> <span data-ttu-id="c87bf-132">De Azure-Emulators zijn emulators van cloudservices en -gegevens management services waarmee u een toepassing lokaal te testen.</span><span class="sxs-lookup"><span data-stu-id="c87bf-132">The Azure Emulators are emulators of cloud services and data management services that allow you to test an application locally.</span></span> <span data-ttu-id="c87bf-133">Deze onderdelen worden ondersteund. alleen Windows.</span><span class="sxs-lookup"><span data-stu-id="c87bf-133">These components are supported Windows only.</span></span>

<span data-ttu-id="c87bf-134">De aanbevolen manier voor het installeren van Azure PowerShell en de Azure-emulator is met de [Microsoft Web Platform Installer][download-wpi].</span><span class="sxs-lookup"><span data-stu-id="c87bf-134">The recommended way to install Azure PowerShell and the Azure Emulators is to use the [Microsoft Web Platform Installer][download-wpi].</span></span> <span data-ttu-id="c87bf-135">Houd er rekening mee dat u ook kunt andere onderdelen van de ontwikkeling, zoals PHP, SQL Server, de Microsoft-Drivers voor SQL Server voor PHP en WebMatrix installeren.</span><span class="sxs-lookup"><span data-stu-id="c87bf-135">Note that you can also choose to install other development components, such as PHP, SQL Server, the Microsoft Drivers for SQL Server for PHP, and WebMatrix.</span></span>

<span data-ttu-id="c87bf-136">Zie voor meer informatie over het gebruik van Azure PowerShell [hoe Azure PowerShell gebruiken][powershell-tools].</span><span class="sxs-lookup"><span data-stu-id="c87bf-136">For information about how to use Azure PowerShell, see [How to Use Azure PowerShell][powershell-tools].</span></span>

## <a name="azure-cli"></a><span data-ttu-id="c87bf-137">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c87bf-137">Azure CLI</span></span>
<span data-ttu-id="c87bf-138">De Azure CLI is een reeks opdrachten voor het implementeren en beheren van Azure-services, zoals Azure Websites en Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="c87bf-138">The Azure CLI is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="c87bf-139">Zie voor meer informatie over het installeren van Azure CLI [Azure CLI installeren](cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c87bf-139">For information about installing Azure CLI, see [Install the Azure CLI](cli-install-nodejs.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c87bf-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c87bf-140">Next steps</span></span>
<span data-ttu-id="c87bf-141">Zie voor meer informatie de [PHP-ontwikkelaarscentrum](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="c87bf-141">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

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
