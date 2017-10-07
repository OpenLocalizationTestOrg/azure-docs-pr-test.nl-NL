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
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a><span data-ttu-id="9cff4-104">Aan de slag met een sandbox met Hadoop, een emulator op een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="9cff4-104">Get started with a Hadoop sandbox, an emulator on a virtual machine</span></span>

<span data-ttu-id="9cff4-105">Meer informatie over hoe tooinstall Hallo Hadoop sandbox van Hortonworks op een virtuele machine toolearn over Hallo Hadoop-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="9cff4-105">Learn how tooinstall hello Hadoop sandbox from Hortonworks on a virtual machine toolearn about hello Hadoop ecosystem.</span></span> <span data-ttu-id="9cff4-106">Hallo sandbox biedt een lokale ontwikkeling omgeving toolearn over Hadoop, Hadoop Distributed File System (HDFS) en de verzending van de taak.</span><span class="sxs-lookup"><span data-stu-id="9cff4-106">hello sandbox provides a local development environment toolearn about Hadoop, Hadoop Distributed File System (HDFS), and job submission.</span></span> <span data-ttu-id="9cff4-107">Wanneer u bekend met Hadoop bent, kunt u beginnen met Hadoop op Azure door het maken van een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9cff4-107">Once you are familiar with Hadoop, you can start using Hadoop on Azure by creating an HDInsight cluster.</span></span> <span data-ttu-id="9cff4-108">Zie voor meer informatie over hoe tooget aan de slag [aan de slag met Hadoop op HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9cff4-108">For more information on how tooget started, see [Get started with Hadoop on HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9cff4-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9cff4-109">Prerequisites</span></span>
* <span data-ttu-id="9cff4-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span><span class="sxs-lookup"><span data-stu-id="9cff4-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span></span> <span data-ttu-id="9cff4-111">Download en installeer deze via [hier](https://www.virtualbox.org/wiki/Downloads).</span><span class="sxs-lookup"><span data-stu-id="9cff4-111">Download and install it from [here](https://www.virtualbox.org/wiki/Downloads).</span></span>



## <a name="download-and-install-hello-virtual-machine"></a><span data-ttu-id="9cff4-112">Download en installeer Hallo virtuele machine</span><span class="sxs-lookup"><span data-stu-id="9cff4-112">Download and install hello virtual machine</span></span>
1. <span data-ttu-id="9cff4-113">Blader toohello [Hortonworks downloadt](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="9cff4-113">Browse toohello [Hortonworks downloads](http://hortonworks.com/downloads/#sandbox).</span></span>

2. <span data-ttu-id="9cff4-114">Klik op **downloaden voor VIRTUALBOX** toodownload Hallo nieuwste Hortonworks Sandbox op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="9cff4-114">Click **DOWNLOAD FOR VIRTUALBOX** toodownload hello latest Hortonworks Sandbox on a VM.</span></span> <span data-ttu-id="9cff4-115">U bent na vragen aan gebruiker tooregister met Hortonworks voordat Hallo downloaden wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="9cff4-115">You are prompted tooregister with Hortonworks before hello download begins.</span></span> <span data-ttu-id="9cff4-116">Het duurt een tootwo uren toodownload, afhankelijk van de netwerksnelheid van uw.</span><span class="sxs-lookup"><span data-stu-id="9cff4-116">It takes one tootwo hours toodownload depending on your network speed.</span></span>
   
    ![Afbeelding van de koppeling voor de Hortonworks Sandbox voor VirtualBox downloaden](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. <span data-ttu-id="9cff4-118">Uit dezelfde webpagina hello, klikt u op Hallo **importeren op de virtuele vak** koppelen toodownload een PDF-bestand met de installatie-instructies voor het Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="9cff4-118">From hello same web page, click hello **Import on Virtual Box** link toodownload a PDF containing installation instructions for hello virtual machine.</span></span>

<span data-ttu-id="9cff4-119">een oudere versie-sandbox HDP toodownload uitvouwen Hallo archief:</span><span class="sxs-lookup"><span data-stu-id="9cff4-119">toodownload an older HDP version sandbox, expand hello archive:</span></span>

![Hortonworks sandbox-archief](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-hello-virtual-machine"></a><span data-ttu-id="9cff4-121">Hallo virtuele machine starten</span><span class="sxs-lookup"><span data-stu-id="9cff4-121">Start hello virtual machine</span></span>

1. <span data-ttu-id="9cff4-122">Oracle VM VirtualBox openen.</span><span class="sxs-lookup"><span data-stu-id="9cff4-122">Open Oracle VM VirtualBox.</span></span>
2. <span data-ttu-id="9cff4-123">Van Hallo **bestand** menu, klikt u op **importeren toestel**, en geef vervolgens Hallo Hortonworks sandbox-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="9cff4-123">From hello **File** menu, click **Import Appliance**, and then specify hello Hortonworks Sandbox image.</span></span>
1. <span data-ttu-id="9cff4-124">Selecteer Hallo Hortonworks Sandbox, klikt u op **Start**, en vervolgens **normaal Start**.</span><span class="sxs-lookup"><span data-stu-id="9cff4-124">Select hello Hortonworks Sandbox, click **Start**, and then **Normal Start**.</span></span> <span data-ttu-id="9cff4-125">Zodra opstartproces hello, Hallo virtuele machine is voltooid, wordt aanmelding instructies weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9cff4-125">Once hello virtual machine has finished hello boot process, it displays login instructions.</span></span>
   
    ![Normale starten](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. <span data-ttu-id="9cff4-127">Open een webbrowser en navigeer toohello URL weergegeven (meestal http://127.0.0.1:8888).</span><span class="sxs-lookup"><span data-stu-id="9cff4-127">Open a web browser and navigate toohello URL displayed (usually http://127.0.0.1:8888).</span></span>

## <a name="set-sandbox-passwords"></a><span data-ttu-id="9cff4-128">Sandbox-wachtwoorden instellen</span><span class="sxs-lookup"><span data-stu-id="9cff4-128">Set Sandbox passwords</span></span>

1. <span data-ttu-id="9cff4-129">Van Hallo **aan de slag** stap Hallo Hortonworks Sandbox pagina **weergave geavanceerde opties**.</span><span class="sxs-lookup"><span data-stu-id="9cff4-129">From hello **get started** step of hello Hortonworks Sandbox page, select **View Advanced Options**.</span></span> <span data-ttu-id="9cff4-130">Hallo-informatie op deze pagina toolog in toohello sandbox via SSH gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9cff4-130">Use hello information on this page toolog in toohello sandbox using SSH.</span></span> <span data-ttu-id="9cff4-131">Gebruik Hallo naam en wachtwoord opgegeven.</span><span class="sxs-lookup"><span data-stu-id="9cff4-131">Use hello name and password provided.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9cff4-132">Als u geen een SSH-client is geïnstalleerd, kunt u web gebaseerde SSH op aangeboden door Hallo virtuele machine op Hallo **http://localhost:4200 /**.</span><span class="sxs-lookup"><span data-stu-id="9cff4-132">If you do not have an SSH client installed, you can use hello web-based SSH provided at by hello virtual machine at **http://localhost:4200/**.</span></span>
   > 
   
    <span data-ttu-id="9cff4-133">Hallo bent eerste keer dat u verbinding maken via SSH, u na vragen aan gebruiker toochange Hallo wachtwoord voor het hoofdaccount Hallo.</span><span class="sxs-lookup"><span data-stu-id="9cff4-133">hello first time you connect using SSH, you are prompted toochange hello password for hello root account.</span></span> <span data-ttu-id="9cff4-134">Voer een nieuw wachtwoord dat u gebruiken wanneer u zich aanmeldt via SSH.</span><span class="sxs-lookup"><span data-stu-id="9cff4-134">Enter a new password, which you use when you log in using SSH.</span></span>

2. <span data-ttu-id="9cff4-135">Nadat u bent aangemeld, Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="9cff4-135">Once logged in, enter hello following command:</span></span>
   
        ambari-admin-password-reset
   
    <span data-ttu-id="9cff4-136">Wanneer u wordt gevraagd, moet u een wachtwoord opgeven voor Hallo Ambari-beheeraccount.</span><span class="sxs-lookup"><span data-stu-id="9cff4-136">When prompted, provide a password for hello Ambari admin account.</span></span> <span data-ttu-id="9cff4-137">Dit wordt gebruikt wanneer u toegang Hallo Ambari-Webgebruikersinterface tot.</span><span class="sxs-lookup"><span data-stu-id="9cff4-137">This is used when you access hello Ambari Web UI.</span></span>

## <a name="use-hive-commands"></a><span data-ttu-id="9cff4-138">Hive-opdrachten gebruiken</span><span class="sxs-lookup"><span data-stu-id="9cff4-138">Use Hive commands</span></span>

1. <span data-ttu-id="9cff4-139">Gebruik van een SSH-verbinding toohello-sandbox Hallo toostart Hallo Hive-opdrachtshell te volgen:</span><span class="sxs-lookup"><span data-stu-id="9cff4-139">From an SSH connection toohello sandbox, use hello following command toostart hello Hive shell:</span></span>
   
        hive
2. <span data-ttu-id="9cff4-140">Zodra het Hallo-shell is gestart, gebruikt u Hallo tooview Hallo tabellen die worden geleverd met Hallo sandbox na:</span><span class="sxs-lookup"><span data-stu-id="9cff4-140">Once hello shell has started, use hello following tooview hello tables that are provided with hello sandbox:</span></span>
   
        show tables;
3. <span data-ttu-id="9cff4-141">Gebruik Hallo volgende tooretrieve 10 rijen uit Hallo `sample_07` tabel:</span><span class="sxs-lookup"><span data-stu-id="9cff4-141">Use hello following tooretrieve 10 rows from hello `sample_07` table:</span></span>
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a><span data-ttu-id="9cff4-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9cff4-142">Next steps</span></span>
* [<span data-ttu-id="9cff4-143">Meer informatie over hoe toouse Visual Studio met Hallo Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="9cff4-143">Learn how toouse Visual Studio with hello Hortonworks Sandbox</span></span>](hdinsight-hadoop-emulator-visual-studio.md)
* [<span data-ttu-id="9cff4-144">Learning Hallo kabels Hallo Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="9cff4-144">Learning hello ropes of hello Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="9cff4-145">Hadoop-zelfstudie - aan de slag met HDP</span><span class="sxs-lookup"><span data-stu-id="9cff4-145">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

