---
title: Eenheden per Azure-Database waarin wordt uitgelegd berekenen voor MySQL | Microsoft Docs
description: 'Azure DB voor MySQL: dit artikel wordt uitgelegd Hallo concepten van Compute-eenheden en wat er gebeurt wanneer uw werkbelasting bereikt Hallo maximum aantal eenheden berekenen.'
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 751b4fff2760e55565e2bc80d49db17a57397779
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="explaining-compute-units-in-azure-database-for-mysql"></a>In Azure MySQL-Database waarin wordt uitgelegd Compute-eenheden
In dit artikel wordt uitgelegd Hallo concept van Compute-eenheden en wat er gebeurt wanneer uw werkbelasting bereikt Hallo maximum aantal eenheden berekenen.

## <a name="what-are-compute-units"></a>Wat zijn eenheden berekenen?
COMPUTE eenheden zijn een meting van CPU-verwerking doorvoer die gegarandeerd toobe beschikbaar tooa één Azure-Database voor de MySQL-server. Een Compute-eenheid is een gecombineerde meting van CPU en geheugenbronnen. In het algemeen neer 50 Compute eenheden toohalf van een kern. 100 compute eenheden neer tooone core. 2000 compute eenheden neer tootwenty kernen van gegarandeerde verwerking doorvoer beschikbaar tooyour server.

Hallo hoeveelheid geheugen per eenheid Compute is geoptimaliseerd voor Hallo Basic en Standard Prijscategorieën. Hallo Compute eenheden verdubbeling doordat Hallo prestatieniveau gelijkstaat toodoubling Hallo set resource beschikbaar toothat één Azure-Database voor MySQL.

Bijvoorbeeld, biedt een 800 Compute standaardeenheden doorvoer van 8 x meer CPU en geheugen dan een 100 Compute standaardeenheden-configuratie. Echter, terwijl 100 Compute standaardeenheden bieden Hallo dezelfde CPU doorvoer vergeleken tooBasic 100 Compute eenheden, Hallo hoeveelheid geheugen die is vooraf geconfigureerd in de Standard-prijscategorie is dubbel Hallo hoeveelheid geheugen die is geconfigureerd voor Basic prijscategorie. Daarom biedt Standard-prijscategorie betere prestaties van de werkbelasting en lagere latentie mogelijk transactie dan Basic prijscategorie Hello die dezelfde Compute eenheden geselecteerd.

## <a name="how-can-i-determine-hello-number-of-compute-units-needed-for-my-workload"></a>Hoe kan ik zien van Hallo aantal Compute-eenheden voor de werkbelasting nodig?
Als u op zoek bent toomigrate een bestaande MySQL-server lokaal wordt uitgevoerd, of op een virtuele machine, kunt u het aantal eenheden Compute Hallo kunt bepalen door schatten hoeveel kernen van doorvoer van de verwerking van uw werkbelasting moet. 

Als uw bestaande on-premises of de server van de virtuele machine is momenteel gebruik van 4 kernen (zonder CPU hyperthread tellen) wordt eerst 400 Compute eenheden configureren voor uw Azure-Database voor de MySQL-server. COMPUTE eenheden kunnen worden dynamisch uitgebreid omhoog of omlaag, afhankelijk van de behoeften van uw werkbelasting met vrijwel geen uitvaltijd voor toepassingen. 

Monitor-grafiek Hallo metrische gegevens in Azure portal- of schrijfbewerking Azure CLI-opdrachten - toomeasure Hallo compute eenheden. Relevante meetgegevens toomonitor zijn Hallo eenheid Compute-percentage en Compute-eenheid limiet.

>[!IMPORTANT]
> Als u opslag IOP's niet volledig zijn gebruikt toohello maximum vinden, kunt u overwegen Hallo compute eenheden gebruik en bewaking. Hallo Compute eenheden verhogen mogelijk voor een hogere i/o-doorvoer door vermindering van het prestatieknelpunt Hallo vervaldatum toolimited CPU of geheugen.

## <a name="what-happens-when-i-hit-my-maximum-compute-units"></a>Wat gebeurt er wanneer ik mijn maximum aantal eenheden voor Compute bereikt?
Prestaties zijn kalibreren en tooprovide resources toorun beheerst de werkbelasting van de database van toohello max limieten voor Hallo geselecteerde prijscategorie en prestatieniveau. 

Als uw werkbelasting Hallo maximale limieten in ofwel Hallo Compute eenheden of ingerichte IOPS-limieten bereikt, kunt u tooutilize Hallo bronnen op de maximaal toegestane niveau Hallo blijven, maar uw query's zijn waarschijnlijk toosee verhoogd latenties. Deze limieten resulteren niet in fouten, maar in plaats daarvan een vertraging van de werkbelasting hello, tenzij Hallo vertraging wordt zo ernstig die query time-out. 

Als uw werkbelasting Hallo-bovengrenzen voor het aantal verbindingen bereikt, worden de expliciete fouten gegenereerd. Zie voor meer informatie over bronnen limieten [beperkingen in Azure-Database voor MySQL](concepts-limits.md).

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over het Prijscategorieën [Azure Database voor MySQL Prijscategorieën](./concepts-service-tiers.md).
