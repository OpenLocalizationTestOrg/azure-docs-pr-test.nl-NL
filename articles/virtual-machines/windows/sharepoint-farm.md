---
title: aaaCreate SharePoint serverfarms in Azure | Microsoft Docs
description: Een nieuwe SharePoint 2013 of SharePoint 2016-farm snel maken in Azure met behulp van hello Azure portal marketplace.
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 89b124da-019d-4179-86dd-ad418d05a4f2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d71c7177d9b99cf377bab767342508007285b452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-sharepoint-server-farms-using-hello-azure-portal-marketplace"></a>SharePoint server-farms met hello Azure portal marketplace maken

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a>SharePoint 2013-farms
Met Microsoft Azure portal-marketplace hello, kunt u snel vooraf geconfigureerde SharePoint Server 2013-farms maken. Hiermee kunt u veel tijd als u een SharePoint-farm basis of hoge beschikbaarheid nodig hebt voor een omgeving met ontwikkelen en testen of opslaan als u SharePoint Server 2013 als een samenwerkingsoplossing voor voor uw organisatie.

> [!NOTE]
> Hallo **SharePoint-serverfarm** item in hello Azure Marketplace van hello Azure-portal is verwijderd. Het is vervangen door hello **SharePoint 2013 niet - HA-Farm** en **SharePoint 2013-Farm is HA** items.
>
>

Hallo basic SharePoint-farm bestaat uit drie virtuele machines in deze configuratie.

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

U kunt deze farmconfiguratie gebruiken voor een eenvoudig instellen voor het ontwikkelen van de SharePoint-app of uw eerst evaluatieversie van SharePoint 2013.

toocreate hello basic () SharePoint farm met drie servers:

1. Klik op [hier](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).
2. Klik op **implementeren**.
3. Op Hallo **SharePoint 2013 niet - HA-Farm** deelvenster, klikt u op **maken**.
4. Instellingen opgeven op Hallo stappen Hallo **maken SharePoint 2013 niet - HA-Farm** deelvenster en klik vervolgens op **maken**.

Hallo hoge beschikbaarheid SharePoint-farm bestaat uit negen virtuele machines in deze configuratie.

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

U kunt deze farm configuratie tootest hogere client belasting, hoge beschikbaarheid van Hallo externe SharePoint-site en SQL Server AlwaysOn-beschikbaarheidsgroepen gebruiken voor een SharePoint-farm. U kunt deze configuratie ook gebruiken voor ontwikkeling van apps in SharePoint in een omgeving met hoge beschikbaarheid.

toocreate hello hoge beschikbaarheid (9-server) SharePoint-farm:

1. Klik op [hier](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).
2. Klik op **implementeren**.
3. Op Hallo **SharePoint 2013-Farm is HA** deelvenster, klikt u op **maken**.
4. Instellingen opgeven op Hallo zeven stappen Hallo **maken SharePoint 2013 HA-Farm** deelvenster en klik vervolgens op **maken**.

> [!NOTE]
> U kunt geen Hallo maken **SharePoint 2013 niet - HA-Farm** of **SharePoint 2013-Farm is HA** met een gratis proefversie van Azure.
>
>

Hello Azure-portal maakt zowel deze farms in een virtueel netwerk met een internetgerichte webserver aanwezigheid alleen in de cloud. Er is geen site-naar-site VPN- of ExpressRoute-verbinding back tooyour organisatienetwerk.

> [!NOTE]
> Als u Hallo basic maakt of hello Azure-portal met hoge beschikbaarheid SharePoint-farms, u kunt een bestaande resourcegroep niet opgeven. Deze bedrijven toowork om deze beperking, maken met Azure PowerShell. Zie voor meer informatie [farms van SharePoint 2013 maken ontwikkelen en testen met Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).
>
>

## <a name="sharepoint-2016-farms"></a>SharePoint 2016-farms
Zie [in dit artikel](https://technet.microsoft.com/library/mt723354.aspx) voor Hallo instructies toobuild Hallo na één server SharePoint Server 2016-farm.

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-hello-sharepoint-farms"></a>Het beheer van SharePoint-farms Hallo
U kunt servers Hallo van deze bedrijven via Extern bureaublad-verbindingen kunt beheren. Zie voor meer informatie [toohello virtuele machine aanmelden](quick-create-portal.md#connect-to-virtual-machine).

Hallo Centraal beheer van SharePoint-site, kunt u Mijn sites, SharePoint-toepassingen en andere functionaliteit configureren. Zie voor meer informatie [SharePoint configureren](http://technet.microsoft.com/library/ee836142.aspx).

## <a name="next-steps"></a>Volgende stappen
* Aanvullende detecteren [SharePoint configuraties](https://technet.microsoft.com/library/dn635309.aspx) in Azure-infrastructuurservices.
