---
title: Verwante en gekoppelde resources in de tegel-galerie
description: Meer informatie over verwante en gekoppelde resources die worden weergegeven in de tegel-galerie van Azure preview portal.
services: azure-portal
documentationcenter: 
author: adamabdelhamed
manager: wpickett
editor: 
ms.assetid: dba96d29-f518-49c8-bfd2-f14cecb44cbf
ms.service: azure-portal
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2015
ms.author: adamab
ms.openlocfilehash: efa7bce26c2c4c153b083e0e34d689a11d27dd16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="related-and-linked-resources-in-the-tile-gallery"></a>Verwante en gekoppelde resources in de tegel-galerie
De tegel galerie kunt u tegels vinden voor een bepaalde bron- en sleep deze naar uw huidige blade. Met de tegel-galerie, kunt u beheerweergaven die resources omvatten. Voor een opgegeven resource bevatten de bijbehorende resources alle resources in de resourcegroep en alle resources die een koppeling naar of van de resource.

## <a name="linked-resources-in-resource-manager"></a>Gekoppelde resources in het Resource Manager
Koppelen is een functie van de Resource Manager.  Hiermee kunt u relaties tussen resources declareren, zelfs als ze zich niet in dezelfde resourcegroep. Koppelen, heeft geen invloed op de runtime van uw resources, niet van invloed op de facturering en niet van invloed op rollen gebaseerde toegang.  Het is gewoon een mechanisme die kunt u vertegenwoordigen relaties, zodat de hulpprogramma's als de tegel-galerie een geavanceerde beheermogelijkheden bieden kan optreden.  De hulpprogramma's kunnen de koppelingen die via de koppelingen API inspecteren en bieden aangepaste relatie management ook optreedt. 

## <a name="how-do-i-link-my-resources"></a>Hoe kan ik mijn resources koppelen?
Wanneer u resources via de portal of met het implementeren van een sjabloon via Azure PowerShell of Azure CLI maakt, worden automatisch koppelingen gemaakt voor enkele afhankelijke resources. U kunt ook programmatisch resources koppelen met behulp van de [gekoppelde Resources REST-API](/rest/api/resources/resourcelinks).

## <a name="next-steps"></a>Volgende stappen
* Als u een inleiding tot het schrijven van Resource Manager-sjablonen, Zie [sjablonen](../azure-resource-manager/resource-group-authoring-templates.md).
* Zie voor meer informatie over het werken met resourcegroepen gebruiken via de portal, [met behulp van de Azure-portal voor het beheren van uw Azure-resources](../azure-resource-manager/resource-group-portal.md).

