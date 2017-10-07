---
title: aaaUse hello Vertex Execution View in Data Lake Tools voor Visual Studio | Microsoft Docs
description: Meer informatie over hoe toouse Hallo Vertex Execution View tooexam Data Lake Analytics-taken.
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5366d852-e7d6-44cf-a88c-e9f52f15f7df
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/13/2016
ms.author: jgao
ms.openlocfilehash: fb54d2af8a32aa27a54ff50a73c1b4903677a21e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a>Hallo Vertex Execution View in Data Lake Tools voor Visual Studio gebruiken
Meer informatie over hoe toouse Hallo Vertex Execution View tooexam Data Lake Analytics-taken.

## <a name="prerequisites"></a>Vereisten

Moet u basiskennis van het gebruik van Data Lake Tools voor Visual Studio toodevelop U-SQL-script.  Zie [zelfstudie: U-SQL-scripts ontwikkelen met Data Lake Tools voor Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).

## <a name="open-hello-vertex-execution-view"></a>Hallo Vertex Execution View openen
Open een U-SQL-taak in de Data Lake Tools voor Visual Studio. Klik op **Vertex Execution View** in Hallo linkerbenedenhoek. Hebt u mogelijk na vragen aan gebruiker tooload profielen eerst en het kan even duren, afhankelijk van uw netwerkverbinding.

![Data Lake Analytics Tools Vertex Execution View](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a>Vertex Execution View begrijpen
Hallo Vertex Execution View bestaat uit drie delen:

![Data Lake Analytics Tools Vertex Execution View](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

Hallo **hoekpunt selector** op Hallo links kunt u hoekpunten selecteren door functies (zoals top 10 gegevens lezen, of kies fase). Een van de meest gebruikte Hallo-filters toosee Hallo is **hoekpunten op kritieke pad**. Hallo **kritieke pad** is Hallo langste keten van hoekpunten van een U-SQL-taak. Understanding Hallo kritieke pad is nuttig voor het optimaliseren van uw taken door te controleren welke hoekpunt duurt Hallo langste.
  
![Data Lake Analytics Tools Vertex Execution View](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

Hallo bovenste middelste deelvenster ziet u Hallo **verwerkingsstatus van alle Hallo hoekpunten**.
  
![Data Lake Analytics Tools Vertex Execution View](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

Hallo onder het middelste deelvenster ziet u informatie over elk hoekpunt:
* Procesnaam: naam van Hallo van Hallo hoekpunt exemplaar. Bestaat uit verschillende onderdelen in StageName | VertexName | VertexRunInstance. Hallo SV7_Split [62] .v1 hoekpunt staat bijvoorbeeld voor Hallo tweede exemplaar dat wordt uitgevoerd (.v1, index die begint bij 0) van hoekpunt getal 62 in fase SV7_Split.
* Totale gegevens lezen/schriftelijke: Hallo gegevens is gelezen of weggeschreven door dit hoekpunt.
* Status/afsluitstatus: Hallo eindstatus wanneer Hallo hoekpunt wordt beëindigd.
* Exit Code/mislukte Type: Hallo fout bij het Hallo hoekpunt is mislukt.
* Het maken van reden: Waarom Hallo hoekpunt is gemaakt.
* Resource latentie/proces latentie/PN wachtrij latentie: Hallo gebruikte tijd voor Hallo hoekpunt toowait voor resources, tooprocess gegevens en toostay in Hallo wachtrij.
* GUID van proces/Maker: GUID voor de huidige actieve hoekpunt Hallo of de maker.
* Versie: Hallo N de instantie van Hallo hoekpunt uitgevoerd (Hallo-systeem kunt plannen nieuwe exemplaren van een hoekpunt voor een groot aantal redenen, bijvoorbeeld failover compute redundantie, enz.)
* Versie wanneer gemaakt.
* Verwerken maken Start tijd/proces in de wachtrij geplaatst tijd/proces Start tijd/proces voltooid tijd: wanneer Hallo hoekpunt proces maken start; Wanneer Hallo hoekpunt proces wordt gestart tooqueue; Hallo wanneer bepaalde hoekpunt proces gestart; Wanneer hello bepaalde hoekpunt is voltooid.

## <a name="next-steps"></a>Volgende stappen
* toolog diagnostische informatie, Zie [toegang tot logboeken met diagnostische gegevens voor Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)
* Zie voor een complexere query toosee [websitelogboeken analyseren met Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).
* taakdetails tooview, Zie [gebruik taak Browser en weergave van de taak voor Azure Data lake Analytics-taken](data-lake-analytics-data-lake-tools-view-jobs.md)
