---
title: aaaSet up PowerShell toocreate een VM voor Hallo Marketplace | Microsoft Docs
description: "Instructies voor het instellen van Azure PowerShell en gebruiken als een optioneel proces toocreate VM-installatiekopieën toodeploy, stroom en verkopen op, hello Azure Marketplace"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e19d6cda-76df-4e42-be84-c9fe47a636db
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/04/2016
ms.author: hascipio
ms.openlocfilehash: cd2ebad7472248b8f921706e1a8c82d41f33b9cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-powershell-toocreate-an-offer-for-hello-azure-marketplace"></a>Azure PowerShell toocreate instellen met een aanbieding voor hello Azure Marketplace
Voor gedetailleerde informatie over het tooset van PowerShell in Azure, Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview). Een eenvoudige benadering is toouse Hallo certificaat methode, gedownload en importeert een certificaat nodig voor verificatie. Hallo tooobtain nodig van het certificaat, gebruikt u Hallo **Get-AzurePublishSettingsFile** cmdlet. Hallo-bestand opslaan wanneer u wordt gevraagd. tooimport hello certificaat in een PowerShell-sessie gebruik Hallo **importeren AzurePublishSettingsFile** cmdlet.

tooconfigure en store Hallo algemene Microsoft Azure-abonnement-instellingen voor Hallo PowerShell-sessie gebruiken Hallo **Set-AzureSubscription** en **Select-AzureSubscription** cmdlets:

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

de eerste opdracht Hallo koppelt een standaardopslagaccount aan Hallo-abonnement (nodig voor bepaalde bewerkingen van VM-inrichting).  Hallo maakt tweede Hallo abonnement Hallo huidige abonnement (herkend door andere cmdlets).

## <a name="see-also"></a>Zie ook
* [Aan de slag: hoe toopublish een aanbieding toohello Azure Marketplace](marketplace-publishing-getting-started.md)
* [Maken van de installatiekopie van een virtuele machine voor Hallo Marketplace](marketplace-publishing-vm-image-creation.md)

