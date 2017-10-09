---
title: Virtuele Machines van Azure Data wetenschappelijke als IPython Notebook Servers aaaProvision | Microsoft Docs
description: Instellen van een Data wetenschappelijke virtuele Machine als een Server van de Notebook IPython met ondersteunende hulpprogramma's.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 95e1fa87-794a-4d03-80a4-af4f3f3ac31e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev
ms.openlocfilehash: 7c0abcbcb822918332f76a9f16690a72b90f4b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="provision-azure-data-science-virtual-machines-as-ipython-notebook-servers"></a>Azure Data wetenschappelijke virtuele Machines inrichten als IPython Notebook Servers
Instructies zijn opgegeven hier die wordt beschreven hoe tooset van een virtuele machine van Azure en een virtuele machine in Azure met SQL-Service als de laptop IPython servers. Hallo Windows virtuele machine is geconfigureerd met ondersteunende hulpprogramma's zoals IPython laptop, Azure Storage Explorer en AzCopy, evenals andere hulpprogramma's die handig voor gegevens wetenschappelijke projecten zijn. Azure Storage Explorer en AzCopy, bijvoorbeeld bieden handige manieren tooupload gegevensopslag tooAzure van uw lokale computer of toodownload het tooyour lokale computer uit de opslag. 

Dit menu koppelingen tootopics waarin wordt beschreven hoe tooset up Hallo verschillende gegevens wetenschappelijke omgevingen gebruikt door Hallo [Team gegevens wetenschap proces (TDSP)](data-science-process-overview.md).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

Verschillende soorten virtuele Azure-machines kunnen worden ingericht en geconfigureerd toobe gebruikt als onderdeel van een cloud-gebaseerde gegevens wetenschap-omgeving. Hallo beslissing over welke versie van de virtuele machine toouse afhankelijk van het Hallo-type en de hoeveelheid gegevens toobe is gemodelleerd met machine learning en Hallo doellocatie voor dat de gegevens in de cloud Hallo. 

* Zie voor instructies over Hallo vragen tooconsider wanneer deze beslissing, [van plan bent uw Azure Machine Learning gegevens wetenschappelijke omgeving](machine-learning-data-science-plan-your-environment.md). 
* Zie voor een catalogus van een aantal Hallo-scenario's die u tegenkomen kunt bij het uitvoeren van geavanceerde analyses [scenario's voor geavanceerde analyses proces en de technologie in Azure Machine Learning Hallo](machine-learning-data-science-plan-sample-scenarios.md)

Twee sets met instructies zijn beschikbaar:

* [Instellen van Azure een virtuele machine als een server IPython Notebook voor geavanceerde analyses](machine-learning-data-science-setup-virtual-machine.md) ziet u hoe tooprovision een virtuele machine van Azure met IPython laptops en andere hulpprogramma's voor gegevenswetenschap toodo gebruikt voor gevallen waarin een vorm van dan SQL Azure-opslag kan worden gebruikt toostore Hallo gegevens.
* [Instellen van een virtuele machine van Azure SQL-Server als een server IPython Notebook voor geavanceerde analyses](machine-learning-data-science-setup-sql-server-virtual-machine.md) ziet u hoe tooprovision een virtuele machine van Azure SQL-Server met IPython laptops en andere hulpprogramma's voor gegevenswetenschap toodo gebruikt voor gevallen waarin een SQL-database kan worden gebruikt toostore Hallo gegevens.

Zodra de ingericht en geconfigureerd, is deze virtuele machines zijn gereed voor gebruik als IPython Notebook servers voor Hallo exploratie en verwerking van gegevens, en voor andere taken die nodig zijn in combinatie met Azure Machine Learning en Hallo Team gegevens wetenschap proces (TDSP). Hello zijn de volgende stappen in Hallo gegevens wetenschap proces toegewezen in Hallo [TDSP leertraject](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) en bevatten mogelijk stappen die gegevens in SQL Server of HDInsight, verwerken en het voorbeeld ter voorbereiding van het leren van gegevens met Azure Hallo verplaatsen Machine Learning.

> [!NOTE]
> Virtuele Machines in Azure worden berekend als **Betaal alleen voor wat u**. tooensure die u niet worden kosten in rekening gebracht wanneer de virtuele machine niet wordt gebruikt, heeft de toobe hello **gestopt (Deallocated)** status van Hallo [klassieke Azure-Portal](http://manage.windowsazure.com/). Voor stapsgewijze instructies of hoe toodeallocate u virtuele machine, Zie [afsluiten en toewijzing van de virtuele machine als deze niet in gebruik](machine-learning-data-science-setup-virtual-machine.md#shutdown)
> 
> 

