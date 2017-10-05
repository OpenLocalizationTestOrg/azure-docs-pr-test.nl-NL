---
title: Implementatie van grote implementaties
description: Informatie over het implementeren van grote implementaties met de Azure-Toolkit voor Eclipse.
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
ms.openlocfilehash: e12e379e2b6727653e2377b1760c3745596a1e9c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deploying-large-deployments"></a>Implementatie van grote implementaties
Als uw implementatie te groot om te worden opgenomen in de standaard approot-map is, kunt u een resource voor lokale opslag gebruiken als de hoofdmap van de implementatie voor uw JDK en toepassingsservers.

## <a name="to-use-a-local-storage-resource-as-the-deployment-root-folder-for-large-deployments"></a>De bron van een lokale opslag gebruiken als de hoofdmap van de implementatie voor grote implementaties
1. Maak een nieuwe resource van de lokale opslag. De naam van de resource niet van belang. Storage-resources zijn gedefinieerd op het rolniveau van de. De snelste manier toegang krijgen tot het configuratiedialoogvenster van de lokale opslag, van waaruit u een nieuwe resource van de lokale opslag kunt maken is met behulp van de volgende stappen uit: met de rechtermuisknop op de rol in de **Projectverkenner** weergave (Vouw uw Azure-project knooppunt als de functie niet wordt weergegeven), klikt u op **Azure**, en klik vervolgens op **lokale opslag**. Binnen de **lokale opslag** dialoogvenster, klikt u op **toevoegen** voor het maken van een nieuwe resource van de lokale opslag.

2. Stel de gewenste grootte op ten minste 2048 MB (iets minder kan hetzelfde bestand grootte problemen veroorzaken zoals u zou optreden in de approot).

3. Zorg ervoor dat **opschonen van de inhoud wanneer de rolinstantie gerecycled wordt** is ingeschakeld; Dit helpt voorkomen dat opstartlogica van de implementatie worden uitgevoerd in conflicten met vooraf bestaande bestanden in de bron wanneer het rolexemplaar gerecycled.

4. Zorg ervoor dat de **omgevingsvariabele pad van de resource opslaan na implementatie** waarde is ingesteld op de tekenreeks **DEPLOYROOT**. Uw lokale opslag resource dialoogvenster ziet er ongeveer als volgt.

   ![][ic667943]

U kunt ook als u **DEPLOYROOT** als de *naam* van uw lokale resource en voer de automatisch gegenereerde naam van omgevingsvariabele wijzigingen (die wordt ingesteld op **DEPLOYROOT_ PAD** in dat geval), die voor uw toepassing ook zou werken.

Als u meer informatie over het maken van een resource voor lokale opslag kan worden gevonden op [eigenschappen van lokale opslag][Local storage properties].

## <a name="see-also"></a>Zie ook
[Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]

[Maken van een Hallo wereld-toepassing voor Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

[De installatie van de Azure Toolkit voor Eclipse][Installing the Azure Toolkit for Eclipse] 

Zie voor meer informatie over het gebruik van Azure met Java de [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
