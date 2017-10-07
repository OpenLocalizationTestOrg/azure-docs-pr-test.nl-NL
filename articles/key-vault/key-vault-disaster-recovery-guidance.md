---
title: aaaWhat toodo in Hallo-gebeurtenis van een onderbreking van de Azure-service die gevolgen heeft voor Azure Sleutelkluis | Microsoft Docs
description: Meer informatie over welke toodo in Hallo-gebeurtenis van een onderbreking van de Azure-service die gevolgen heeft voor Azure Sleutelkluis.
services: key-vault
documentationcenter: 
author: adamglick
manager: mbaldwin
editor: 
ms.assetid: 19a9af63-3032-447b-9d1a-b0125f384edb
ms.service: key-vault
ms.workload: key-vault
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: sumedhb;aglick
ms.openlocfilehash: 88eec82ada401a28323b3eea126168185ba4cdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a>Azure Sleutelkluis beschikbaarheid en redundantie
Azure Sleutelkluis is uitgerust met meerdere lagen van redundantie toomake u ervoor zorgen dat uw sleutels en geheimen toepassing tooyour beschikbaar blijven zelfs als afzonderlijke onderdelen van Hallo-service is mislukt.

Hallo inhoud van uw sleutelkluis wordt gerepliceerd binnen Hallo regio en de secundaire regio tooa ten minste 150 mijl verwijderd, maar binnen Hallo hetzelfde Geografie. Dit onderhoudt gebied van duurzaamheid van uw sleutels en geheimen. Zie Hallo [Azure regio's gekoppeld](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) document voor meer informatie over specifieke regio-paren.

Als afzonderlijke onderdelen in de sleutelkluis-service Hallo mislukken, stap alternatieve onderdelen binnen Hallo regio in tooserve uw aanvraag toomake ervoor dat er geen verslechtering van de functionaliteit. U hoeft geen tootake elke actie tootrigger dit. Dit gebeurt automatisch en transparant tooyou zijn.

In Hallo zeldzame geval dat een volledige Azure-regio niet beschikbaar is, Hallo-aanvragen die u van Azure Sleutelkluis in deze regio aanbrengt automatisch doorgestuurd (*failover*) tooa secundaire regio. Wanneer de primaire regio Hallo weer beschikbaar is, aanvragen terug doorgestuurd (*kan niet terug*) toohello primaire regio. Opnieuw, u hoeft niet tootake geen actie omdat dit automatisch gebeurt.

Er zijn enkele aanvullende opmerkingen toobe op de hoogte van:

* In geval van een failover regio Hallo duurt enkele minuten duren voordat Hallo service toofail via. Aanvragen die afkomstig zijn gedurende deze tijd mislukken totdat de Hallo failover is voltooid.
* Nadat een failover voltooid is, wordt de sleutelkluis in de modus alleen-lezen is. Aanvragen die worden ondersteund in deze modus zijn:
  * Lijst sleutelkluizen
  * Eigenschappen van sleutelkluizen opgehaald
  * Lijst met geheimen
  * Ophalen van geheimen
  * Lijst met sleutels
  * (Eigenschappen van)-sleutels ophalen
  * Versleutelen
  * Ontsleutelen
  * Tekstterugloop
  * Uitpakken
  * Verifiëren
  * Aanmelding
  * Back-up
* Na een failover terug mislukte is, alle aanvraagtypen (inclusief lezen *en* schrijfaanvragen) beschikbaar zijn.

