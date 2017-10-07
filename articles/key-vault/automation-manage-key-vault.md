---
title: aaaManage Azure Key Vault met behulp van Azure Automation | Microsoft Docs
description: Meer informatie over hoe hello Azure Automation-service gebruikte toomanage Azure Key Vault kan zijn.
services: Key-Vault, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 4e780762-19b6-4ca6-b894-ebb44c538f35
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte;csand
ms.openlocfilehash: 7f46ecc1206a96e8aeb1d086285461cb5b205472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a>Het beheren van Azure Sleutelkluis met behulp van Azure Automation
Deze handleiding vindt u toohello Azure Automation-service en hoe het kan gebruikte toosimplify beheer van uw sleutels en geheimen in Azure Sleutelkluis.

## <a name="what-is-azure-automation"></a>Wat is Azure Automation?
[Azure Automation](../automation/automation-intro.md) is een Azure-service voor het vereenvoudigen van beheer door automatisering van bedrijfsprocessen en configuratie van de gewenste status. Met behulp van Azure Automation, kunnen handmatige, herhaalde langlopende en foutgevoelige-taken worden geautomatiseerd tooincrease betrouwbaarheid, efficiëntie en een tijd toovalue voor uw organisatie.

Azure Automation biedt een engine voor het uitvoeren van uiterst betrouwbare, maximaal beschikbare workflow die schaalbaar toomeet uw behoeften. In Azure Automation kunnen processen worden gestarte handmatig, door systemen van derden 3rd of met regelmatige tussenpozen zodat taken gebeuren precies wanneer deze nodig is.

Operationele overhead verminderen en vrijmaken IT en DevOps personeel toofocus op het werk dat bedrijfswaarde door te verplaatsen van uw cloud management taken toobe voegt automatisch uitgevoerd door Azure Automation.

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a>Hoe kan Azure Automation helpen beheren van Azure Sleutelkluis?
Sleutelkluis in Azure Automation kunnen worden beheerd met behulp van Hallo [AzureRM Sleutelkluis-cmdlets](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) en [Azure Classic Sleutelkluis-cmdlets](https://msdn.microsoft.com/library/azure/dn868052.aspx). Hallo Azure-module voor het beheren van klassieke Sleutelkluis beschikbaar automatisch in Azure Automation is en u kunt importeren Hallo [AzureRM KeyVault-module](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) in Azure Automation, zodat u veel van uw Sleutelkluis-beheer kan uitvoeren taken in het Hallo-service. U kunt deze cmdlets in Azure Automation met Hallo-cmdlets voor andere Azure-services, complexe taken tooautomate ook koppelen in Azure-services en 3e systemen van derden.

Met hello Azure Sleutelkluis-cmdlets kunt u deze taken onder andere uitvoeren: 

* Maken en configureren van een sleutelkluis
* Maken of importeren van een sleutel
* Maken of bijwerken van een geheim
* Kenmerken van een sleutel bijwerken
* Een sleutel of geheim ophalen
* Een sleutel of geheim verwijderen

Hier volgen enkele voorbeelden van het gebruik van PowerShell toomanage Sleutelkluis:  

* [Azure Sleutelkluis - stap voor stap](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [Installeren en configureren van een Azure Sleutelkluis](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a>Volgende stappen
Nu u Hallo basisbeginselen van Azure Automation en hoe deze kan worden gebruikt toomanage Azure Sleutelkluis hebt geleerd, volgt u deze koppelingen toolearn meer informatie over Azure Automation.

* Zie hello Azure Automation [zelfstudie aan de slag](../automation/automation-first-runbook-graphical.md).
* Zie Hallo [Azure Key Vault PowerShell-scripts](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).

