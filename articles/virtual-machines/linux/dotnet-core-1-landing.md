---
title: aaaAzure Linux virtuele Machine DotNet Core zelfstudie 1 | Microsoft Docs
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
ms.openlocfilehash: 7e6f047197336de1e93c50413b6eabb718230bc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automating-application-deployments-toolinux-virtual-machines"></a>Automatisering van toepassing implementaties tooLinux virtuele Machines 

Deze reeks vierdelige details implementeren en configureren van Azure-resource en toepassingen met behulp van Azure Resource Manager-sjablonen. In deze reeks een voorbeeldsjabloon is geïmplementeerd en Hallo implementatiesjabloon onderzocht. Hallo-doel van deze reeks is tooeducate op Hallo relatie tussen Azure-resources en tooprovide handen op ervaring met de implementatie volledig geïntegreerde Azure Resource Manager-sjablonen. Dit document wordt ervan uitgegaan dat de op basisniveau kennis met Azure Resource Manager, voordat u begint in deze zelfstudie raken met de basisconcepten van Azure Resource Manager. 

## <a name="music-store-application"></a>Music store-toepassing
Hallo voorbeeld gebruikt in deze reeks is een .net Core toepassing simuleren een dienst getoond. Deze toepassing kan worden geïmplementeerd tooeither een Linux- of Windows virtuele-systeem voorbeeld voor beide implementaties zijn gemaakt. Hallo toepassing beschikt over een webtoepassing en een SQL-database. Voordat Hallo artikelen in deze reeks wordt gelezen door Hallo-toepassing met behulp van Hallo implementatie knop gevonden op deze pagina te implementeren. Wanneer volledig is geïmplementeerd, eruit hello toepassing / Azure architectuur Hallo volgende diagram. 

Hallo muziek Store Resource Manager-sjabloon vindt u hier, [muziek Store Linux sjabloon](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db)

![Music Store-toepassing](./media/dotnet-core-1-landing/music-store.png)

Elk van deze onderdelen, met inbegrip van Hallo sjabloon JSON wordt behandeld in de volgende vier artikelen Hallo koppelen.

* [**Toepassingsarchitectuur** ](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) : toepassingsonderdelen zoals websites en databases moeten toobe gehost op Azure computerbronnen zoals virtuele machines en Azure SQL-databases. Dit document wordt uitgelegd toewijzing rekencapaciteit nodig, tooAzure resources en implementeren van deze resources met een Azure Resource Manager-sjabloon. 
* [**Toegang en beveiliging** ](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) – wanneer toepassingen in Azure hosten, is het nodig tooconsider hoe Hallo toepassing wordt geopend en hoe de andere toepassingsonderdelen toegang tot elkaar. In dit document worden bieden en beveiliging van internet toegang tooan toepassing en access tussen toepassingsonderdelen.
* [**Beschikbaarheid en schaal** ](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) : beschikbaarheid en schaal verwijzen toohello toepassingen de mogelijkheid toostay uitvoeren tijdens infrastructuuruitvaltijd en Hallo mogelijkheid tooscale compute resources toomeet toepassing vraag. Dit document details Hallo onderdelen nodig toodeploy een met gelijke taakverdeling en maximaal beschikbare toepassingen.
* [**Toepassingsimplementatie** ](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) : wanneer het implementeren van toepassingen op Azure Virtual Machines, door welke Hallo binaire bestanden van toepassingen zijn geïnstalleerd op virtuele Machine Hallo Hallo-methode moet worden overwogen. In dit document worden automatiseren installatie van de toepassing met behulp van Azure virtuele Machine aangepast scriptextensies.

Hallo doel bij het ontwikkelen van Azure Resource Manager-sjablonen is tooautomate Hallo implementatie van Azure-infrastructuur en Hallo-installatie en configuratie van alle toepassingen die wordt gehost op deze Azure-infrastructuur. Het uitvoeren van deze artikelen bevat een voorbeeld van deze ervaring.

## <a name="deploy-hello-music-store-application"></a>Hallo muziek store-App implementeren
Hallo muziek Store-toepassing kan worden geïmplementeerd met behulp van deze knop.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FMicrosoft%2Fdotnet-core-sample-templates%2Fmaster%2Fdotnet-core-music-linux%2Fazuredeploy.json" target="_blank"> <img src="http://azuredeploy.net/deploybutton.png"/>
</a>

Hello Azure Resource Manager-sjabloon vereist Hallo parameterwaarden te volgen.

| Parameternaam | Beschrijving |
| --- | --- |
| SSHKEYDATA |SSH-sleutel gegevens gebruikt toosecure toegang toohello virtuele Machine. Zie voor meer informatie over het maken van een SSH-sleutelpaar [maken van SSH-sleutels voor virtuele Linux-machines in Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). |
| ADMINUSERNAME |De beheerdersgebruikersnaam die wordt gebruikt op Hallo virtuele machine en hello Azure SQL Database. |
| SQLADMINPASSWORD |Wachtwoord dat wordt gebruikt op Hallo Azure SQL Database. |
| NUMBEROFINSTANCES |Hallo aantal virtuele machines toobe gemaakt. Elk van deze webtoepassing voor virtuele machines host Hallo muziek Store en alle verkeer gelijkmatig wordt verdeeld onder te brengen. |
| PUBLICIPADDRESSDNSNAME |Globaal unieke DNS-naam die is gekoppeld aan Hallo openbare IP-adres. |

Wanneer de sjabloonimplementatie Hallo is voltooid, bladert u toohello openbare IP-adres met een internetbrowser. Hallo .net Core muziek site worden weergegeven.

## <a name="next-steps"></a>Volgende stappen
<hr>

[Stap 1 - toepassingsarchitectuur met Azure Resource Manager-sjablonen](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Stap 2 - toegang en beveiliging in Azure Resource Manager-sjablonen](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Stap 3 - beschikbaarheid en schaal in Azure Resource Manager-sjablonen](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Stap 4: implementatie van de toepassing met Azure Resource Manager-sjablonen](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

