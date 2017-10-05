---
title: Sessie-affiniteit met de Azure-Toolkit voor Eclipse inschakelen
description: Informatie over het inschakelen van sessie-affiniteit met de Azure-Toolkit voor Eclipse.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 88c595ec-7d85-40bd-9078-8d6be7b3f0fa
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: ab8623d6f9751ed6d71d9a5b1c0d5e939c442862
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-session-affinity"></a>Sessie-affiniteit inschakelen
Binnen de Azure-werkset voor Eclipse, kunt u de affiniteit van HTTP-sessie of 'een tijdelijke sessies', voor uw functies inschakelen. De volgende afbeelding toont de **Load Balancing** eigenschappenvenster gebruikt voor het inschakelen van de functie van de affiniteit sessie:

![][ic719492]

## <a name="to-enable-session-affinity-for-your-role"></a>Sessie-affiniteit voor uw rol inschakelen
1. Met de rechtermuisknop op de rol in de Eclipse-Project Explorer, klikt u op **Azure**, en klik vervolgens op **Load Balancing**.

2. In de **eigenschappen WorkerRole1 Load Balancing** dialoogvenster:

   a. Controleer **inschakelen HTTP-sessie affiniteit (een tijdelijke sessies) voor deze rol.**

   b. Voor **invoer eindpunt te gebruiken**, selecteert u een invoereindpunt moet worden gebruikt, bijvoorbeeld **http (openbare: 80, persoonlijke: 8080)**. Uw toepassing, moet dit eindpunt gebruiken als de HTTP-eindpunt. U kunt meerdere eindpunten inschakelen voor uw rol, maar u kunt slechts één van deze ter ondersteuning van een tijdelijke sessies selecteren.

   c. Uw toepassing opnieuw bouwt.

Eenmaal is ingeschakeld, hebt u meer dan één rolexemplaar, blijven HTTP-aanvragen die afkomstig zijn van een bepaalde client wordt verwerkt door dezelfde rolinstantie.

De Eclipse-Toolkit maakt dit mogelijk door een speciale IIS-module Application Request Routing (ARR) in elk van uw rolinstanties installeren. ARR wordt omgeleid naar de juiste rolinstantie HTTP-aanvragen. De toolkit opnieuw automatisch geconfigureerd voor het geselecteerde eindpunt, zodat de binnenkomende HTTP-verkeer wordt eerst doorgestuurd naar de ARR-software. De toolkit maakt ook een nieuwe interne eindpunt die uw Java-server is geconfigureerd om te luisteren naar. Dit is het eindpunt dat wordt gebruikt door ARR de HTTP-verkeer naar de juiste instantie worden omgeleid. Op deze manier elke rolinstantie in uw implementatie meerdere exemplaren fungeert als omgekeerde proxy voor alle andere gevallen belden inschakelen van een tijdelijke sessies.

## <a name="notes-about-session-affinity"></a>Opmerkingen over de affiniteit van sessie
* Sessie-affiniteit werkt niet in de rekenemulator. De instellingen kunnen worden toegepast in de rekenemulator geen conflicten ontstaan met uw buildproces of compute-emulator worden uitgevoerd, maar de functie zelf werkt niet binnen de rekenemulator.

* Inschakelen van sessie-affiniteit leidt tot een toename van de hoeveelheid schijfruimte in beslag genomen door uw implementatie in Azure, zoals extra software worden gedownload en geïnstalleerd in uw rolinstanties wanneer uw service wordt gestart in de Azure-cloud.

* De tijd voor het initialiseren van elke rol zal langer duren.

* Een interne eindpunt, zoals hierboven vermeld, worden gebruikt als een rerouter verkeer wordt toegevoegd.


## <a name="see-also"></a>Zie ook
[Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]

[Maken van een Hallo wereld-toepassing voor Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

[De installatie van de Azure Toolkit voor Eclipse][Installing the Azure Toolkit for Eclipse] 

Zie voor meer informatie over het gebruik van Azure met Java de [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How to Maintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
