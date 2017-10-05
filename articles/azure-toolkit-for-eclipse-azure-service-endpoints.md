---
title: Azure Service-eindpunten
description: Beschrijft de instellingen van Azure Service-eindpunt in de Azure-werkset voor Eclipse.
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
ms.openlocfilehash: 6059c292c2687f1bf3d9be04c03aaaaf6adde945
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-service-endpoints"></a>Azure Service-eindpunten
Azure service-eindpunten die bepalen dat of uw toepassing is geïmplementeerd en beheerd door de globale Azure-platform, door Azure worden beheerd door 21Vianet in China, of een persoonlijk die door Azure-platform. De **Service-eindpunten** dialoogvenster kunt u opgeven welke service-eindpunten die u wilt gebruiken. Openen van de **Service-eindpunten** dialoogvenster in Eclipse, klikt u op **venster**, klikt u op **voorkeuren**, vouw **Azure**, en klik vervolgens op  **Service-eindpunten**. Instellen van de **Active ingesteld** veld bepaalt welke Azure-service-eindpunten wordt gebruikt voor de Azure-projecten in uw huidige werkruimte.

Het volgende bevat de **Service-eindpunten** dialoogvenster.

![][ic719493]

## <a name="to-set-the-service-endpoints"></a>Instellen van de service-eindpunten
In de **Service-eindpunten** dialoogvenster, voer een van de volgende acties:

* Als u gebruiken van de globale Azure-platform wilt, van de **Active ingesteld** vervolgkeuzelijst, selecteer **windowsazure.com** en klik op **OK**.

* Als u gebruiken van Azure die worden beheerd door 21Vianet in China wilt, uit de **Active ingesteld** vervolgkeuzelijst, selecteer **windowsazure.cn (China)** en klik op **OK**.

* Als u gebruiken een persoonlijke Azure-platform wilt:

  1. Klik op **Bewerken**.

  2. Een dialoogvenster wordt geopend, waarin wordt gemeld dat de **Service-eindpunten** dialoogvenster wordt gesloten en de voorkeur sets-bestand wordt geopend. Klik op **OK**.

  3. Maak een nieuwe in het bestand preferencesets.xml `preferenceset` element. Voor deze nieuwe element maken `name`, `blob`, `management`, `portalURL` en `publishsettings` kenmerken en waarden toevoegen voor hen die overeenkomen met uw persoonlijke Azure-platform. U kunt de waarden voor de bestaande `preferenceset` elementen als sjabloon. **Opmerking**: de waarde voor de `blob` kenmerk moet de tekst 'blob' in de URL bevatten.

  4. Opslaan en sluiten preferencesets.xml.

  5. Open de **Service-eindpunten** dialoogvenster.

  6. Van de **Active ingesteld** vervolgkeuzelijst, selecteer de actieve instellen die u gemaakt en klik op **OK**.

  7. Als u uw persoonlijke Azure-platform hebt gemaakt `preferenceset` element, kunt u de waarden die zijn toegewezen door te klikken op de **bewerken** knop in de **Services-eindpunt** dialoogvenster. U kunt ook meerdere persoonlijke Azure-platform maken `preferenceset` elementen, als u wenst.

## <a name="see-also"></a>Zie ook
[Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]

[De installatie van de Azure Toolkit voor Eclipse][Installing the Azure Toolkit for Eclipse] 

[Maken van een Hallo wereld-toepassing voor Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

Zie voor meer informatie over het gebruik van Azure met Java de [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
