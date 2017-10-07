---
title: aaa "Azure Batch-taakgebeurtenis start | Microsoft Docs'
description: Naslaginformatie voor Batch-taak start gebeurtenis.
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 2cb066be1578741125e9081a84a2b7c74dc8356a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="task-start-event"></a>Gebeurtenissen voor het starten van taak

 Deze gebeurtenis wordt verzonden als een taak is gepland toostart op een rekenknooppunt door Hallo scheduler. Houd er rekening mee dat als Hallo-taak wordt later opnieuw of opnieuw deze gebeurtenis wordt worden verzonden opnieuw voor hello dezelfde taak, maar Hallo aantal nieuwe pogingen en besturingssysteemversie van de taak wordt dienovereenkomstig bijgewerkt.


 Hallo ziet volgende voorbeeld Hallo-hoofdtekst van een taak start-gebeurtenis.

```
{
    "jobId": "job-0000000001",
    "id": "task-5",
    "taskType": "User",
    "systemTaskVersion": 0,
    "nodeInfo": {
        "poolId": "pool-001",
        "nodeId": "tvm-257509324_1-20160908t162728z"
    },
    "multiInstanceSettings": {
        "numberOfInstances": 1
    },
    "constraints": {
        "maxTaskRetryCount": 2
    },
    "executionInfo": {
        "retryCount": 0
    }
}
```

|Elementnaam|Type|Opmerkingen|
|------------------|----------|-----------|
|JobId|Tekenreeks|Hallo-id van Hallo-taak met taak Hallo.|
|id|Tekenreeks|Hallo-id van Hallo-taak.|
|taskType|Tekenreeks|Hallo type Hallo-taak. Dit kan worden 'Taakbeheer heeft, die aangeeft dat het een jobbeheertaak of gebruiker is niet een jobbeheertaak aangeeft.|
|systemTaskVersion|Int32|Dit is interne Hallo nieuwe pogingen voor een taak. Intern Hallo Batch-service kan opnieuw proberen van een taak tooaccount voor tijdelijke problemen. Deze problemen kunnen interne planning fouten of pogingen toorecover uit rekenknooppunten opnemen in een verkeerde status.|
|[nodeInfo](#nodeInfo)|Complex Type|Bevat informatie over het Hallo-rekenknooppunt op welke Hallo taak is uitgevoerd.|
|[multiInstanceSettings](#multiInstanceSettings)|Complex Type|Hiermee geeft u dat die taak Hallo taak met meerdere instanties vereisen van meerdere rekenknooppunten is.  Zie [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) voor meer informatie.|
|[beperkingen](#constraints)|Complex Type|Hallo uitvoering beperkingen toothis taak.|
|[executionInfo](#executionInfo)|Complex Type|Bevat informatie over Hallo uitvoering van Hallo-taak.|

###  <a name="nodeInfo"></a>nodeInfo

|Elementnaam|Type|Opmerkingen|
|------------------|----------|-----------|
|poolId|Tekenreeks|Hallo-id van Hallo-pool op welke Hallo taak is uitgevoerd.|
|nodeId|Tekenreeks|Hallo-id van Hallo-knooppunt op welke Hallo taak is uitgevoerd.|

###  <a name="multiInstanceSettings"></a>multiInstanceSettings

|Elementnaam|Type|Opmerkingen|
|------------------|----------|-----------|
|numberOfInstances|int|Hallo aantal rekenknooppunten door Hallo taak vereist.|

###  <a name="constraints"></a>beperkingen

|Elementnaam|Type|Opmerkingen|
|------------------|----------|-----------|
|maxTaskRetryCount|Int32|Hallo maximum aantal keren Hallo taak kan opnieuw worden uitgevoerd. Hallo Batch-service probeert een taak opnieuw als de afsluitcode gelijk aan nul is.<br /><br /> Houd er rekening mee dat deze waarde specifiek het aantal nieuwe pogingen Hallo bepaalt. Hallo Batch-service eenmaal probeert Hallo taak en probeer vervolgens up toothis limiet. Bijvoorbeeld, als Hallo maximale aantal pogingen 3 is, Batch wordt geprobeerd een taak too4 tijden (een initiële probeer en 3 nieuwe pogingen).<br /><br /> Als Hallo maximale aantal nieuwe pogingen 0 is, probeert Hallo Batch-service niet taken opnieuw.<br /><br /> Als Hallo maximale aantal pogingen -1 is, probeert Hallo Batch-service opnieuw taken zonder limiet.<br /><br /> Hallo-standaardwaarde is 0 (geen herhaalde pogingen).|

###  <a name="executionInfo"></a>executionInfo

|Elementnaam|Type|Opmerkingen|
|------------------|----------|-----------|
|retryCount|Int32|Hallo aantal keren Hallo taak door Hallo Batch-service opnieuw is geprobeerd. Hallo-taak wordt herhaald als deze wordt afgesloten met een andere waarde dan nul afsluitcode up toohello opgegeven MaxTaskRetryCount|
