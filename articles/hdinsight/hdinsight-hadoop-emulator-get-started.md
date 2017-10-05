---
title: Meer informatie over met behulp van een Hadoop-sandbox - emulator - Azure HDInsight | Microsoft Docs
description: 'Als u wilt weten over het gebruik van het Hadoop-ecosysteem, kunt u instellen een sandbox met Hadoop van Hortonworks op een virtuele machine van Azure. '
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
ms.openlocfilehash: b701879464205860edd1c097651b532f87bae388
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a><span data-ttu-id="92961-104">Aan de slag met een sandbox met Hadoop, een emulator op een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="92961-104">Get started with a Hadoop sandbox, an emulator on a virtual machine</span></span>

<span data-ttu-id="92961-105">Informatie over het installeren van de sandbox Hadoop vanaf Hortonworks op een virtuele machine voor meer informatie over het Hadoop-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="92961-105">Learn how to install the Hadoop sandbox from Hortonworks on a virtual machine to learn about the Hadoop ecosystem.</span></span> <span data-ttu-id="92961-106">De sandbox biedt een lokale ontwikkelingsomgeving voor meer informatie over Hadoop, Hadoop Distributed File System (HDFS) en de verzending van de taak.</span><span class="sxs-lookup"><span data-stu-id="92961-106">The sandbox provides a local development environment to learn about Hadoop, Hadoop Distributed File System (HDFS), and job submission.</span></span> <span data-ttu-id="92961-107">Wanneer u bekend met Hadoop bent, kunt u beginnen met Hadoop op Azure door het maken van een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="92961-107">Once you are familiar with Hadoop, you can start using Hadoop on Azure by creating an HDInsight cluster.</span></span> <span data-ttu-id="92961-108">Zie voor meer informatie over het aan de slag [aan de slag met Hadoop op HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="92961-108">For more information on how to get started, see [Get started with Hadoop on HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92961-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="92961-109">Prerequisites</span></span>
* <span data-ttu-id="92961-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span><span class="sxs-lookup"><span data-stu-id="92961-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span></span> <span data-ttu-id="92961-111">Download en installeer deze via [hier](https://www.virtualbox.org/wiki/Downloads).</span><span class="sxs-lookup"><span data-stu-id="92961-111">Download and install it from [here](https://www.virtualbox.org/wiki/Downloads).</span></span>



## <a name="download-and-install-the-virtual-machine"></a><span data-ttu-id="92961-112">Download en installeer de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="92961-112">Download and install the virtual machine</span></span>
1. <span data-ttu-id="92961-113">Blader naar de [Hortonworks downloadt](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="92961-113">Browse to the [Hortonworks downloads](http://hortonworks.com/downloads/#sandbox).</span></span>

2. <span data-ttu-id="92961-114">Klik op **downloaden voor VIRTUALBOX** voor het downloaden van de meest recente Hortonworks Sandbox op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="92961-114">Click **DOWNLOAD FOR VIRTUALBOX** to download the latest Hortonworks Sandbox on a VM.</span></span> <span data-ttu-id="92961-115">U wordt gevraagd om te registreren met Hortonworks voordat de download wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="92961-115">You are prompted to register with Hortonworks before the download begins.</span></span> <span data-ttu-id="92961-116">Het duurt een tot twee uur om te downloaden, afhankelijk van de netwerksnelheid van uw.</span><span class="sxs-lookup"><span data-stu-id="92961-116">It takes one to two hours to download depending on your network speed.</span></span>
   
    ![Afbeelding van de koppeling voor de Hortonworks Sandbox voor VirtualBox downloaden](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. <span data-ttu-id="92961-118">Van dezelfde pagina, klikt u op de **importeren op de virtuele vak** koppeling voor het downloaden van een PDF-bestand met de installatie-instructies voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="92961-118">From the same web page, click the **Import on Virtual Box** link to download a PDF containing installation instructions for the virtual machine.</span></span>

<span data-ttu-id="92961-119">Vouw het archief voor het downloaden van een oudere versie sandbox voor HDP:</span><span class="sxs-lookup"><span data-stu-id="92961-119">To download an older HDP version sandbox, expand the archive:</span></span>

![Hortonworks sandbox-archief](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-the-virtual-machine"></a><span data-ttu-id="92961-121">De virtuele machine starten</span><span class="sxs-lookup"><span data-stu-id="92961-121">Start the virtual machine</span></span>

1. <span data-ttu-id="92961-122">Oracle VM VirtualBox openen.</span><span class="sxs-lookup"><span data-stu-id="92961-122">Open Oracle VM VirtualBox.</span></span>
2. <span data-ttu-id="92961-123">Van de **bestand** menu, klikt u op **importeren toestel**, en geef vervolgens de installatiekopie van het Hortonworks Sandbox.</span><span class="sxs-lookup"><span data-stu-id="92961-123">From the **File** menu, click **Import Appliance**, and then specify the Hortonworks Sandbox image.</span></span>
1. <span data-ttu-id="92961-124">Selecteer de Hortonworks Sandbox, klik op **Start**, en vervolgens **normaal Start**.</span><span class="sxs-lookup"><span data-stu-id="92961-124">Select the Hortonworks Sandbox, click **Start**, and then **Normal Start**.</span></span> <span data-ttu-id="92961-125">Zodra het opstarten van de virtuele machine is voltooid, wordt de aanmelding instructies weergegeven.</span><span class="sxs-lookup"><span data-stu-id="92961-125">Once the virtual machine has finished the boot process, it displays login instructions.</span></span>
   
    ![Normale starten](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. <span data-ttu-id="92961-127">Open een webbrowser en navigeer naar de URL weergegeven (meestal http://127.0.0.1:8888).</span><span class="sxs-lookup"><span data-stu-id="92961-127">Open a web browser and navigate to the URL displayed (usually http://127.0.0.1:8888).</span></span>

## <a name="set-sandbox-passwords"></a><span data-ttu-id="92961-128">Sandbox-wachtwoorden instellen</span><span class="sxs-lookup"><span data-stu-id="92961-128">Set Sandbox passwords</span></span>

1. <span data-ttu-id="92961-129">Van de **aan de slag** stap van de Hortonworks Sandbox pagina **weergave geavanceerde opties**.</span><span class="sxs-lookup"><span data-stu-id="92961-129">From the **get started** step of the Hortonworks Sandbox page, select **View Advanced Options**.</span></span> <span data-ttu-id="92961-130">Gebruik de informatie op deze pagina aanmelden bij de sandbox via SSH.</span><span class="sxs-lookup"><span data-stu-id="92961-130">Use the information on this page to log in to the sandbox using SSH.</span></span> <span data-ttu-id="92961-131">Gebruik de naam en wachtwoord opgegeven.</span><span class="sxs-lookup"><span data-stu-id="92961-131">Use the name and password provided.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="92961-132">Als u een SSH-client is geïnstalleerd niet hebt, kunt u het web gebaseerde SSH op aangeboden door de virtuele machine op **http://localhost:4200 /**.</span><span class="sxs-lookup"><span data-stu-id="92961-132">If you do not have an SSH client installed, you can use the web-based SSH provided at by the virtual machine at **http://localhost:4200/**.</span></span>
   > 
   
    <span data-ttu-id="92961-133">De eerste keer dat u verbinding maken via SSH, wordt u gevraagd het wachtwoord voor het root-account te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="92961-133">The first time you connect using SSH, you are prompted to change the password for the root account.</span></span> <span data-ttu-id="92961-134">Voer een nieuw wachtwoord dat u gebruiken wanneer u zich aanmeldt via SSH.</span><span class="sxs-lookup"><span data-stu-id="92961-134">Enter a new password, which you use when you log in using SSH.</span></span>

2. <span data-ttu-id="92961-135">Nadat u bent aangemeld, voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="92961-135">Once logged in, enter the following command:</span></span>
   
        ambari-admin-password-reset
   
    <span data-ttu-id="92961-136">Wanneer u wordt gevraagd, moet u een wachtwoord opgeven voor de Ambari-beheeraccount.</span><span class="sxs-lookup"><span data-stu-id="92961-136">When prompted, provide a password for the Ambari admin account.</span></span> <span data-ttu-id="92961-137">Dit wordt gebruikt wanneer u toegang de Ambari-Webgebruikersinterface tot.</span><span class="sxs-lookup"><span data-stu-id="92961-137">This is used when you access the Ambari Web UI.</span></span>

## <a name="use-hive-commands"></a><span data-ttu-id="92961-138">Hive-opdrachten gebruiken</span><span class="sxs-lookup"><span data-stu-id="92961-138">Use Hive commands</span></span>

1. <span data-ttu-id="92961-139">Gebruik de volgende opdracht de Hive-shell starten van een SSH-verbinding aan de sandbox:</span><span class="sxs-lookup"><span data-stu-id="92961-139">From an SSH connection to the sandbox, use the following command to start the Hive shell:</span></span>
   
        hive
2. <span data-ttu-id="92961-140">Nadat de shell is gestart, gebruikt u de volgende om de tabellen die worden geleverd aan de sandbox weer te geven:</span><span class="sxs-lookup"><span data-stu-id="92961-140">Once the shell has started, use the following to view the tables that are provided with the sandbox:</span></span>
   
        show tables;
3. <span data-ttu-id="92961-141">Gebruik de volgende voor het ophalen van 10 rijen uit de `sample_07` tabel:</span><span class="sxs-lookup"><span data-stu-id="92961-141">Use the following to retrieve 10 rows from the `sample_07` table:</span></span>
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a><span data-ttu-id="92961-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="92961-142">Next steps</span></span>
* [<span data-ttu-id="92961-143">Informatie over het gebruik van Visual Studio met de Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="92961-143">Learn how to use Visual Studio with the Hortonworks Sandbox</span></span>](hdinsight-hadoop-emulator-visual-studio.md)
* [<span data-ttu-id="92961-144">De kabels van de Hortonworks Sandbox leren</span><span class="sxs-lookup"><span data-stu-id="92961-144">Learning the ropes of the Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="92961-145">Hadoop-zelfstudie - aan de slag met HDP</span><span class="sxs-lookup"><span data-stu-id="92961-145">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

