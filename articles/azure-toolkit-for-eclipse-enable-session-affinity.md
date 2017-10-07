---
title: Sessie-affiniteit met behulp van aaaEnable Hallo Azure Toolkit voor Eclipse
description: Meer informatie over hoe Azure-Toolkit voor Eclipse tooenable sessie affiniteit met Hallo.
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
ms.openlocfilehash: 523e728c58bda95e7af4b242e831694eb6d75cb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-session-affinity"></a>Sessie-affiniteit inschakelen
Binnen hello Azure Toolkit voor Eclipse, kunt u de affiniteit van HTTP-sessie of 'een tijdelijke sessies', voor uw rollen inschakelen. Hallo volgende afbeelding toont Hallo **Load Balancing** eigenschappen dialoogvenster gebruikt tooenable Hallo sessie affiniteit functie:

![][ic719492]

## <a name="tooenable-session-affinity-for-your-role"></a>sessie-affiniteit tooenable voor uw rol
1. Met de rechtermuisknop op het Hallo-rol in de Eclipse-Project Explorer, klikt u op **Azure**, en klik vervolgens op **Load Balancing**.

2. In Hallo **eigenschappen WorkerRole1 Load Balancing** dialoogvenster:

   a. Controleer **inschakelen HTTP-sessie affiniteit (een tijdelijke sessies) voor deze rol.**

   b. Voor **invoer eindpunt toouse**, selecteert u bijvoorbeeld een toouse invoereindpunt **http (openbare: 80, persoonlijke: 8080)**. Uw toepassing, moet dit eindpunt gebruiken als de HTTP-eindpunt. U kunt meerdere eindpunten inschakelen voor uw rol, maar kunt u slechts één van deze toosupport een tijdelijke sessies.

   c. Uw toepassing opnieuw bouwt.

Eenmaal is ingeschakeld, hebt u meer dan één rolexemplaar, HTTP-aanvragen die afkomstig zijn van een bepaalde client blijft wordt verwerkt door Hallo dezelfde rolinstantie.

Hallo Eclipse Toolkit maakt dit mogelijk door een speciale IIS-module Application Request Routing (ARR) in elk van uw rolinstanties installeren. ARR wordt omgeleid toohello juiste rolinstantie voor HTTP-aanvragen. Hallo toolkit automatisch geselecteerd Hallo eindpunt opnieuw geconfigureerd zodat de binnenkomende HTTP-verkeer Hallo eerste gerouteerde toohello ARR software. Hallo toolkit maakt ook een nieuwe interne eindpunt dat uw Java-server is geconfigureerd toolisten aan. Hallo eindpunt dat wordt gebruikt door ARR tooreroute Hallo HTTP-verkeer toohello geschikte rolexemplaar is. Op deze manier fungeert elke rolinstantie in uw implementatie meerdere exemplaren als omgekeerde proxy voor alle andere exemplaren Hallo inschakelen van een tijdelijke sessies.

## <a name="notes-about-session-affinity"></a>Opmerkingen over de affiniteit van sessie
* Sessie-affiniteit werkt niet in Hallo rekenemulator. Hallo-instellingen kunnen worden toegepast in de rekenemulator Hallo geen conflicten ontstaan met uw buildproces of compute-emulator worden uitgevoerd, maar Hallo zelf functie werkt niet binnen het Hallo-rekenemulator.

* Inschakelen van sessie-affiniteit leidt tot een toename van Hallo en de hoeveelheid schijfruimte in beslag genomen door uw implementatie in Azure, zoals aanvullende software wordt gedownload en geïnstalleerd in uw rolinstanties wanneer uw service wordt gestart in hello Azure-cloud.

* Hallo tijd tooinitialize die elke rol zal langer duren.

* Interne eindpunt, toofunction als een rerouter verkeer zoals hierboven vermeld, worden toegevoegd.


## <a name="see-also"></a>Zie ook
[Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]

[Maken van een Hallo wereld-toepassing voor Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Hello Azure Toolkit voor Eclipse installeren][Installing hello Azure Toolkit for Eclipse] 

Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How tooMaintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
