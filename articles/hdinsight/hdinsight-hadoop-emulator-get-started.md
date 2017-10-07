---
title: met behulp van een Hadoop-sandbox - emulator - Azure HDInsight aaaLearn | Microsoft Docs
description: 'toostart leren over het gebruik van Hadoop-ecosysteem Hallo, u kunt een Hadoop-sandbox van Hortonworks instellen op een virtuele machine van Azure. '
keywords: hadoop-emulator, hadoop sandbox
editor: cgronlun
manager: jhubbard
services: hdinsight
author: nitinme
documentationcenter: 
tags: azure-portal
ms.assetid: 6ad5bb58-8215-4e3d-a07f-07fcd8839cc6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 91e74f0823fd02e9bb812155a7d09357a77b0736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a>Aan de slag met een sandbox met Hadoop, een emulator op een virtuele machine

Meer informatie over hoe tooinstall Hallo Hadoop sandbox van Hortonworks op een virtuele machine toolearn over Hallo Hadoop-ecosysteem. Hallo sandbox biedt een lokale ontwikkeling omgeving toolearn over Hadoop, Hadoop Distributed File System (HDFS) en de verzending van de taak. Wanneer u bekend met Hadoop bent, kunt u beginnen met Hadoop op Azure door het maken van een HDInsight-cluster. Zie voor meer informatie over hoe tooget aan de slag [aan de slag met Hadoop op HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).

## <a name="prerequisites"></a>Vereisten
* [Oracle VirtualBox](https://www.virtualbox.org/). Download en installeer deze via [hier](https://www.virtualbox.org/wiki/Downloads).



## <a name="download-and-install-hello-virtual-machine"></a>Download en installeer Hallo virtuele machine
1. Blader toohello [Hortonworks downloadt](http://hortonworks.com/downloads/#sandbox).

2. Klik op **downloaden voor VIRTUALBOX** toodownload Hallo nieuwste Hortonworks Sandbox op een virtuele machine. U bent na vragen aan gebruiker tooregister met Hortonworks voordat Hallo downloaden wordt gestart. Het duurt een tootwo uren toodownload, afhankelijk van de netwerksnelheid van uw.
   
    ![Afbeelding van de koppeling voor de Hortonworks Sandbox voor VirtualBox downloaden](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. Uit dezelfde webpagina hello, klikt u op Hallo **importeren op de virtuele vak** koppelen toodownload een PDF-bestand met de installatie-instructies voor het Hallo virtuele machine.

een oudere versie-sandbox HDP toodownload uitvouwen Hallo archief:

![Hortonworks sandbox-archief](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-hello-virtual-machine"></a>Hallo virtuele machine starten

1. Oracle VM VirtualBox openen.
2. Van Hallo **bestand** menu, klikt u op **importeren toestel**, en geef vervolgens Hallo Hortonworks sandbox-installatiekopie.
1. Selecteer Hallo Hortonworks Sandbox, klikt u op **Start**, en vervolgens **normaal Start**. Zodra opstartproces hello, Hallo virtuele machine is voltooid, wordt aanmelding instructies weergegeven.
   
    ![Normale starten](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. Open een webbrowser en navigeer toohello URL weergegeven (meestal http://127.0.0.1:8888).

## <a name="set-sandbox-passwords"></a>Sandbox-wachtwoorden instellen

1. Van Hallo **aan de slag** stap Hallo Hortonworks Sandbox pagina **weergave geavanceerde opties**. Hallo-informatie op deze pagina toolog in toohello sandbox via SSH gebruiken. Gebruik Hallo naam en wachtwoord opgegeven.
   
   > [!NOTE]
   > Als u geen een SSH-client is geïnstalleerd, kunt u web gebaseerde SSH op aangeboden door Hallo virtuele machine op Hallo **http://localhost:4200 /**.
   > 
   
    Hallo bent eerste keer dat u verbinding maken via SSH, u na vragen aan gebruiker toochange Hallo wachtwoord voor het hoofdaccount Hallo. Voer een nieuw wachtwoord dat u gebruiken wanneer u zich aanmeldt via SSH.

2. Nadat u bent aangemeld, Voer Hallo volgende opdracht:
   
        ambari-admin-password-reset
   
    Wanneer u wordt gevraagd, moet u een wachtwoord opgeven voor Hallo Ambari-beheeraccount. Dit wordt gebruikt wanneer u toegang Hallo Ambari-Webgebruikersinterface tot.

## <a name="use-hive-commands"></a>Hive-opdrachten gebruiken

1. Gebruik van een SSH-verbinding toohello-sandbox Hallo toostart Hallo Hive-opdrachtshell te volgen:
   
        hive
2. Zodra het Hallo-shell is gestart, gebruikt u Hallo tooview Hallo tabellen die worden geleverd met Hallo sandbox na:
   
        show tables;
3. Gebruik Hallo volgende tooretrieve 10 rijen uit Hallo `sample_07` tabel:
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over hoe toouse Visual Studio met Hallo Hortonworks Sandbox](hdinsight-hadoop-emulator-visual-studio.md)
* [Learning Hallo kabels Hallo Hortonworks Sandbox](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [Hadoop-zelfstudie - aan de slag met HDP](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

