---
title: aaaAzure Service-eindpunten
description: Beschrijft hello Azure Service-eindpunt instellingen in hello Azure Toolkit voor Eclipse.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9c6125ec-7278-461e-b69c-ed56e844f742
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 357aa56409a894719077f2c8f302575c8ebb6883
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-endpoints"></a>Azure Service-eindpunten
Azure service-eindpunten die bepalen dat of uw toepassing geïmplementeerd tooand beheerd door Hallo globale Azure-platform wordt, door Azure worden beheerd door 21Vianet in China, of een persoonlijk die door Azure-platform. Hallo **Service-eindpunten** dialoogvenster kunt u toospecify die service-eindpunten die u wilt dat toouse. Hallo tooopen **Service-eindpunten** dialoogvenster in Eclipse, klikt u op **venster**, klikt u op **voorkeuren**, vouw **Azure**, en klik vervolgens op **Service-eindpunten**. Instelling Hallo **Active ingesteld** veld bepaalt welke Azure-service eindpunten wordt gebruikt voor hello Azure projecten in uw huidige werkruimte.

Hallo hieronder vindt u Hallo **Service-eindpunten** dialoogvenster.

![][ic719493]

## <a name="tooset-hello-service-endpoints"></a>tooset hello service-eindpunten
In Hallo **Service-eindpunten** dialoogvenster, nemen Hallo van de volgende activiteiten:

* Als u wilt dat toouse Hallo globale Azure-platform, van Hallo **Active ingesteld** vervolgkeuzelijst, selecteer **windowsazure.com** en klik op **OK**.

* Als u wilt dat Azure beheerd door 21Vianet in China, van Hallo toouse **Active ingesteld** vervolgkeuzelijst, selecteer **windowsazure.cn (China)** en klik op **OK**.

* Als u wilt dat toouse persoonlijke Azure-platform:

  1. Klik op **Bewerken**.

  2. Een dialoogvenster wordt geopend, waarin wordt gemeld dat Hallo **Service-eindpunten** dialoogvenster wordt gesloten en Hallo voorkeur sets bestand wordt geopend. Klik op **OK**.

  3. Hallo preferencesets.xml bestand, maak een nieuwe `preferenceset` element. Voor deze nieuwe element maken `name`, `blob`, `management`, `portalURL` en `publishsettings` kenmerken en waarden toevoegen voor hen die overeenkomen met tooyour persoonlijke Azure-platform. U kunt Hallo waarden opgegeven voor bestaande hello gebruiken `preferenceset` elementen als sjabloon. **Opmerking**: waarde gebruikt voor Hallo Hallo `blob` kenmerk Hallo tekst 'blob' hello URL moet bevatten.

  4. Opslaan en sluiten preferencesets.xml.

  5. Open Hallo **Service-eindpunten** dialoogvenster.

  6. Van Hallo **Active ingesteld** vervolgkeuzelijst, selecteer Hallo active instellen die u gemaakt en klik op **OK**.

  7. Als u uw persoonlijke Azure-platform hebt gemaakt `preferenceset` element, kunt u Hallo waarden toegewezen tooit wijzigen door te klikken op Hallo **bewerken** knop in Hallo **Services-eindpunt** dialoogvenster. U kunt ook meerdere persoonlijke Azure-platform maken `preferenceset` elementen, als u wenst.

## <a name="see-also"></a>Zie ook
[Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]

[Hello Azure Toolkit voor Eclipse installeren][Installing hello Azure Toolkit for Eclipse] 

[Maken van een Hallo wereld-toepassing voor Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
