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
# <a name="download-hello-azure-sdk-for-php"></a>Hello Azure SDK voor PHP downloaden
## <a name="overview"></a>Overzicht
Hello Azure SDK voor PHP omvat onderdelen waarmee u toodevelop, implementeren en beheren van PHP-toepassingen voor Azure. Hello Azure SDK voor PHP bevat met name de volgende Hallo:

* **PHP-clientbibliotheken voor Azure Hallo**. Deze klassenbibliotheken biedt een interface voor toegang tot Azure-functies, zoals services voor het beheer van gegevens en cloudservices.  
* **Hello Azure-opdrachtregelinterface voor Mac, Linux en Windows (Azure CLI)**. Dit is een reeks opdrachten voor het implementeren en beheren van Azure-services, zoals Azure Websites en Azure Virtual Machines. Hallo werk op elk platform, inclusief Mac, Linux en Windows Azure CLI.
* **Azure PowerShell (alleen Windows)**. Dit is een set PowerShell-cmdlets voor het implementeren en beheren van Azure-Services, zoals Cloudservices en virtuele Machines.
* **Hallo (alleen Windows) Azure Emulators**. Hallo berekeningen en opslag emulators zijn lokale emulators van cloudservices en -gegevens management services waarmee u een toepassing lokaal tootest. Hello Azure Emulators alleen op Windows worden uitgevoerd.

Hallo in de volgende secties wordt beschreven hoe toodownload en installeer Hallo onderdelen die hierboven worden beschreven.

Hallo instructies in dit onderwerp wordt ervan uitgegaan dat u hebt [PHP] [ install-php] geïnstalleerd.

> [!NOTE]
> U moet PHP 5.5 of hoger toouse Hallo PHP-clientbibliotheken voor Azure hebben.
> 
> 

## <a name="php-client-libraries-for-azure"></a>PHP-clientbibliotheken voor Azure
Hallo PHP-clientbibliotheken voor Azure biedt een interface voor toegang tot Azure-functies, zoals services voor het beheer van gegevens en in de cloud services, op een ander besturingssysteem. Deze bibliotheken kunnen worden geïnstalleerd via Hallo Composer.

Zie voor meer informatie over hoe toouse PHP-clientbibliotheken voor Azure Hallo [hoe tooUse Blob-Service Hallo][blob-service], [hoe tooUse Tabelservice Hallo] [ table-service] en [hoe tooUse Queue-Service Hallo][queue-service].

### <a name="install-via-composer"></a>Installeren via de Composer
1. [Installeer Git][install-git].

    > [AZURE.NOTE] Op Windows moet u ook tooadd Hallo Git uitvoerbare tooyour pad-omgevingsvariabele.

1. Maak een bestand met de naam **composer.json** in Hallo hoofdmap van uw project en voeg Hallo code tooit te volgen:
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. Download  **[composer.phar] [ composer-phar]**  in de hoofdmap van uw project.
3. Open een opdrachtprompt en dit in de hoofdmap van uw project uitvoeren
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a>Azure PowerShell en Azure Emulators
Azure PowerShell is een set PowerShell-cmdlets voor het implementeren en beheren van Azure-Services (zoals Cloudservices en virtuele Machines). Hello Azure Emulators zijn emulators van cloudservices en -gegevens management services waarmee u een toepassing lokaal tootest. Deze onderdelen worden ondersteund. alleen Windows.

Hallo aanbevolen manier tooinstall Azure PowerShell en hello Azure Emulators is toouse hello [Microsoft Web Platform Installer][download-wpi]. Houd er rekening mee dat u ook tooinstall andere onderdelen van de ontwikkeling, zoals PHP, SQL Server, Microsoft-Drivers Hallo voor SQL Server voor PHP en WebMatrix kunt.

Voor informatie over het toouse Azure PowerShell, Zie [hoe tooUse Azure PowerShell][powershell-tools].

## <a name="azure-cli"></a>Azure CLI
Hello Azure CLI is een reeks opdrachten voor het implementeren en beheren van Azure-services, zoals Azure Websites en Azure Virtual Machines. Zie voor meer informatie over het installeren van Azure CLI [installeren hello Azure CLI](cli-install-nodejs.md).

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie, Hallo [PHP-ontwikkelaarscentrum](/develop/php/).

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
