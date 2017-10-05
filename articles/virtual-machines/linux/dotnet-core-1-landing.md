---
title: Azure Linux virtuele Machine DotNet Core zelfstudie 1 | Microsoft Docs
description: Virtuele Machine van Azure DotNet belangrijkste zelfstudie
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b3652e86-0c44-4ac9-8cd1-27abdeaea4d4
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 928d90f4bee593f04a41254b5f37d9328e59e05e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="automating-application-deployments-to-linux-virtual-machines"></a>Implementaties van toepassingen voor virtuele Linux-Machines automatiseren 

Deze reeks vierdelige details implementeren en configureren van Azure-resource en toepassingen met behulp van Azure Resource Manager-sjablonen. In deze reeks een voorbeeldsjabloon wordt geïmplementeerd en de sjabloon voor de implementatie worden onderzocht. Het doel van deze reeks is dat u op de relatie tussen een Azure-resources, en geef een handen op de ervaring met de implementatie volledig geïntegreerde Azure Resource Manager-sjablonen. Dit document wordt ervan uitgegaan dat de op basisniveau kennis met Azure Resource Manager, voordat u begint in deze zelfstudie raken met de basisconcepten van Azure Resource Manager. 

## <a name="music-store-application"></a>Music store-toepassing
Het voorbeeld dat wordt gebruikt in deze reeks is een .net Core toepassing simuleren een dienst getoond. Deze toepassing kan worden geïmplementeerd op een Linux- of Windows virtueel-systeemtype, voorbeeld implementaties zijn gemaakt voor beide. De toepassing bevat een webtoepassing en een SQL-database. Voordat de artikelen in deze reeks wordt gelezen door de toepassing met behulp van de implementatie-knop gevonden op deze pagina te implementeren. Wanneer volledig is geïmplementeerd, wordt de architectuur van de toepassing / Azure ziet eruit als in het volgende diagram. 

De sjabloon muziek Store Resource Manager vindt u hier, [muziek Store Linux sjabloon](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db)

![Music Store-toepassing](./media/dotnet-core-1-landing/music-store.png)

Elk van deze onderdelen, waaronder de koppelen JSON-sjabloon wordt behandeld in de volgende vier artikelen.

* [**Toepassingsarchitectuur** ](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) : toepassingsonderdelen zoals websites en databases moeten worden gehost op Azure computerbronnen zoals virtuele machines en Azure SQL-databases. Dit document helpt bij de toewijzing rekencapaciteit nodig, naar Azure-resources en het implementeren van deze resources met een Azure Resource Manager-sjabloon. 
* [**Toegang en beveiliging** ](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) – bij het hosten van toepassingen in Azure, is het nodig zijn om te overwegen hoe de toepassing wordt geopend en hoe verschillende toegang tot de onderdelen van toepassingen elkaar. In dit document worden bieden en beveiliging van internettoegang tot een toepassing en tussen toepassingsonderdelen.
* [**Beschikbaarheid en schaal** ](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) – beschikbaarheid en schaal verwijzen naar de toepassingen de mogelijkheid om te blijven uitvoeren tijdens infrastructuuruitvaltijd en de mogelijkheid om te schalen rekenresources om te voldoen aan de vraag van de toepassing. Dit Documentdetails van de onderdelen die nodig zijn voor het implementeren van een taakverdeling en de maximaal beschikbare toepassingen.
* [**Toepassingsimplementatie** ](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) : wanneer het implementeren van toepassingen op Azure Virtual Machines, de methode waarmee de binaire bestanden van de toepassingen zijn geïnstalleerd op de virtuele Machine moet worden overwogen. In dit document worden automatiseren installatie van de toepassing met behulp van Azure virtuele Machine aangepast scriptextensies.

Het doel bij het ontwikkelen van Azure Resource Manager-sjablonen is voor het automatiseren van de implementatie van Azure-infrastructuur en de installatie en configuratie van alle toepassingen die wordt gehost op deze Azure-infrastructuur. Het uitvoeren van deze artikelen bevat een voorbeeld van deze ervaring.

## <a name="deploy-the-music-store-application"></a>De muziek store-toepassing implementeren
De muziek Store-toepassing kan worden geïmplementeerd met behulp van deze knop.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FMicrosoft%2Fdotnet-core-sample-templates%2Fmaster%2Fdotnet-core-music-linux%2Fazuredeploy.json" target="_blank"> <img src="http://azuredeploy.net/deploybutton.png"/>
</a>

De Azure Resource Manager-sjabloon vereist de volgende parameterwaarden.

| Parameternaam | Beschrijving |
| --- | --- |
| SSHKEYDATA |SSH-sleutelgegevens gebruikt om toegang aan de virtuele Machine te beveiligen. Zie voor meer informatie over het maken van een SSH-sleutelpaar [maken van SSH-sleutels voor virtuele Linux-machines in Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). |
| ADMINUSERNAME |De beheerdersgebruikersnaam die wordt gebruikt op de virtuele machine en de Azure SQL Database. |
| SQLADMINPASSWORD |Wachtwoord dat wordt gebruikt op de Azure SQL Database. |
| NUMBEROFINSTANCES |Het aantal virtuele machines worden gemaakt. Elk van deze virtuele machines host voor de webtoepassing muziek Store en al het verkeer gelijkmatig wordt verdeeld onder te brengen. |
| PUBLICIPADDRESSDNSNAME |Globaal unieke DNS-naam die is gekoppeld aan het openbare IP-adres. |

Wanneer de sjabloonimplementatie is voltooid, blader naar het openbare IP-adres met een internetbrowser. De .net Core muziek site worden weergegeven.

## <a name="next-steps"></a>Volgende stappen
<hr>

[Stap 1 - toepassingsarchitectuur met Azure Resource Manager-sjablonen](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Stap 2 - toegang en beveiliging in Azure Resource Manager-sjablonen](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Stap 3 - beschikbaarheid en schaal in Azure Resource Manager-sjablonen](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Stap 4: implementatie van de toepassing met Azure Resource Manager-sjablonen](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

