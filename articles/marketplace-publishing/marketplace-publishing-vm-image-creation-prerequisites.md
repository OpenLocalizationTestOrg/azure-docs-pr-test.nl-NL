---
title: vereisten voor het maken van de installatiekopie van een virtuele machine voor hello Azure Marketplace aaaTechnical | Microsoft Docs
description: Hallo-vereisten voor het maken en implementeren van een virtuele machine installatiekopie toohello Azure Marketplace voor anderen begrijpen toopurchase.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 63c16966-0304-4b17-a715-368a0a5ccb2c
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: fcae4d9e052581e3c1dfe7962e6d50ec31040419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="technical-prerequisites-for-creating-a-virtual-machine-image-for-hello-azure-marketplace"></a>Technische vereisten voor het maken van de installatiekopie van een virtuele machine voor hello Azure Marketplace
Hallo-proces zorgvuldig door voordat u begint lees en begrijp waar en waarom elke stap wordt uitgevoerd. Zo veel mogelijk, u moet uw bedrijfsgegevens en andere gegevens voorbereiden, vereiste hulpprogramma's downloaden en/of technische onderdelen maken voordat u begint met Hallo-proces voor het maken van aanbieding. Deze items moeten worden van de hand van dit artikel.  

## <a name="download-needed-tools--applications"></a>Download de benodigde hulpprogramma's en toepassingen
Moet u de volgende items gereed is voordat u begint met Hallo Hallo hebben:

* Afhankelijk van het besturingssysteem die u ontwikkelt, installatie Hallo [Azure PowerShell-cmdlets](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) of [Linux opdrachtregelinterface hulpprogramma](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) van Hallo [Azure downloadt](https://azure.microsoft.com/downloads/) pagina.
* Azure Opslagverkenner van CodePlex installeren.
* Download en installeer Hallo certificeringsinstantie Test hulpprogramma voor Azure gecertificeerd:
  * [http://go.Microsoft.com/fwlink/?LinkId=526913](http://go.microsoft.com/fwlink/?LinkID=526913). U moet een computer met Windows toorun Hallo certificeringsinstantie hulpprogramma. Als u een computer op basis van Windows niet hebt, kunt u Hallo-hulpprogramma voor het gebruik van een VM op basis van Windows in Azure uitvoeren.

## <a name="platforms-supported"></a>Ondersteunde platforms
U kunt ontwikkelen op basis van een Azure-machines op Windows of Linux. Bepaalde elementen van Hallo publicatieproces--zoals het maken van een Azure-compatibele virtuele harde schijf (VHD)--Gebruik verschillende hulpprogramma's en stappen, afhankelijk van welk besturingssysteem u gebruikt:  

* Als u van Linux gebruikmaakt, raadpleeg dan toohello gedeelte 'Een Azure-compatibele-VHD maken (op basis van Linux)' Hallo [virtuele machine installatiekopie publishing handleiding](marketplace-publishing-vm-image-creation.md).
* Als u van Windows gebruikmaakt, raadpleeg dan toohello gedeelte 'Een Azure-compatibele-VHD maken (op Windows gebaseerd)' Hallo [virtuele machine installatiekopie publishing handleiding](marketplace-publishing-vm-image-creation.md).

> [!NOTE]
> U moet toegang tot tooa op basis van Windows machine:
> 
> * Hallo certificeringsinstantie validatiehulpprogramma uitvoeren.
> * Hallo VHD gedeeld access signature-URL voor Hallo VHD certificeringsinstantie indienen maken.
> 
> 

## <a name="develop-your-vhd"></a>Uw VHD ontwikkelen
U kunt Azure VHD's in Hallo cloud of on-premises ontwikkelen:

* Cloud-gebaseerde ontwikkeling betekent dat alle stappen van de ontwikkeling op afstand worden uitgevoerd op een VHD residente op Azure.
* Lokale ontwikkeling vereist downloaden van een VHD en ontwikkelen met behulp van on-premises infrastructuur. Hoewel dit mogelijk is raadzaam niet deze. Houd er rekening mee dat ontwikkelen voor Windows of SQL lokale vereist dat u toohave Hallo relevante lokale licentiecodes te gebruiken. U kan opnemen of installatie van SQL Server na het maken van een virtuele machine. Ook moet u uw aanbieding baseren op de installatiekopie van een goedgekeurde SQL vanaf hello Azure-portal. Als u toodevelop lokale besluit, moet u een aantal stappen anders dan als u in Hallo cloud ontwikkelt uitvoeren. U kunt relevante informatie vinden in [maken van een installatiekopie van een lokale virtuele machine](marketplace-publishing-vm-image-creation-on-premise.md).

[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
