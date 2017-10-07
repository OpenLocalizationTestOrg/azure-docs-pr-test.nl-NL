---
title: aaaDeploying grote implementaties
description: Meer informatie over hoe toodeploy grote implementaties met behulp van Azure Toolkit voor Eclipse Hallo.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6b1d2a7a5e49c78154fc856a221e64ca8dcfbe9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-large-deployments"></a>Implementatie van grote implementaties
Als uw implementatie te groot toobe opgenomen in de standaardmap approot hello is, kunt u een resource voor lokale opslag gebruiken als hoofdmap Hallo-implementatie voor uw JDK en toepassingsservers.

## <a name="toouse-a-local-storage-resource-as-hello-deployment-root-folder-for-large-deployments"></a>toouse een resource lokale opslag als Hallo implementatie-hoofdmap voor grote implementaties
1. Maak een nieuwe resource van de lokale opslag. Hallo-naam van Hallo resource maakt niet uit. Storage-resources zijn gedefinieerd op Hallo rolniveau. Hallo snelste manier tooaccess Hallo lokale opslag configuratiedialoogvenster, van waaruit u een nieuwe resource van de lokale opslag kunt maken, is via Hallo stappen te volgen: klik met de rechtermuisknop Hallo rol in Hallo **Projectverkenner** weergave (Vouw uw Azure-projectknooppunt als er geen rol Hallo), klikt u op **Azure**, en klik vervolgens op **lokale opslag**. Binnen Hallo **lokale opslag** dialoogvenster, klikt u op **toevoegen** toocreate een nieuwe resource van de lokale opslag.

2. Set Hallo gewenst grootte tooat minimaal 2048 MB (iets minder kan Hallo hetzelfde bestand grootte problemen veroorzaken zoals u zou optreden in Hallo approot).

3. Zorg ervoor dat **opschonen Hallo inhoud wanneer Hallo rolinstantie gerecycled wordt** is ingeschakeld; Dit helpt voorkomen dat opstartlogica Hallo-implementatie worden uitgevoerd in conflicten met vooraf bestaande bestanden in de resource Hallo wanneer Hallo rol exemplaar wordt gerecycled.

4. Zorg ervoor dat Hallo **omgeving variabele opslaan van de bron-mappad Hallo na implementatie** waarde is ingesteld toohello tekenreeks **DEPLOYROOT**. Uw lokale opslag resource dialoogvenster ziet er vergelijkbare toohello volgende.

   ![][ic667943]

U kunt ook als u **DEPLOYROOT** als Hallo *naam* van uw lokale resource en u Hallo automatisch gegenereerde naam van omgevingsvariabele niet wijzigen (die te worden ingesteld **DEPLOYROOT_PATH** in dat geval), die voor uw toepassing ook zou werken.

Als u meer informatie over het maken van een resource voor lokale opslag kan worden gevonden op [eigenschappen van lokale opslag][Local storage properties].

## <a name="see-also"></a>Zie ook
[Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]

[Maken van een Hallo wereld-toepassing voor Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Hello Azure Toolkit voor Eclipse installeren][Installing hello Azure Toolkit for Eclipse] 

Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
