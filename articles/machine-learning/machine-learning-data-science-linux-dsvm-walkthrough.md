---
title: aaaData wetenschappelijke op Hallo Linux gegevens wetenschappelijke virtuele Machine | Microsoft Docs
description: Hoe tooperform enkele algemene gegevenswetenschap taken Hello Linux gegevens wetenschappelijke VM.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 34ef0b10-9270-474f-8800-eecb183bbce4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev;paulsh
ms.openlocfilehash: 78764825f2e834fa4ddb7fdc2f59418dbe736e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-on-hello-linux-data-science-virtual-machine"></a><span data-ttu-id="73d4f-103">Gegevenswetenschap op Hallo Linux gegevens wetenschappelijke virtuele Machine</span><span class="sxs-lookup"><span data-stu-id="73d4f-103">Data science on hello Linux Data Science Virtual Machine</span></span>
<span data-ttu-id="73d4f-104">Dit overzicht toont u hoe tooperform enkele algemene gegevenswetenschap taken Hello Linux gegevens wetenschappelijke VM.</span><span class="sxs-lookup"><span data-stu-id="73d4f-104">This walkthrough shows you how tooperform several common data science tasks with hello Linux Data Science VM.</span></span> <span data-ttu-id="73d4f-105">Hallo Linux gegevens wetenschappelijke virtuele Machine (DSVM) is beschikbaar in Azure die vooraf worden geïnstalleerd met een verzameling hulpprogramma's die doorgaans gebruikt voor gegevensanalyse en machine learning op de installatiekopie van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="73d4f-105">hello Linux Data Science Virtual Machine (DSVM) is a virtual machine image available on Azure that is pre-installed with a collection of tools commonly used for data analytics and machine learning.</span></span> <span data-ttu-id="73d4f-106">Hallo belangrijke software-onderdelen worden gespecificeerd in Hallo [inrichten Hallo Linux gegevens wetenschappelijke virtuele Machine](machine-learning-data-science-linux-dsvm-intro.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="73d4f-106">hello key software components are itemized in hello [Provision hello Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md) topic.</span></span> <span data-ttu-id="73d4f-107">Hallo VM-installatiekopie maakt het eenvoudig tooget gestart tijdens het doorzoeken van wetenschappelijke gegevens in minuten, zonder tooinstall en elk van de hulpprogramma's voor Hallo afzonderlijk configureren.</span><span class="sxs-lookup"><span data-stu-id="73d4f-107">hello VM image makes it easy tooget started doing data science in minutes, without having tooinstall and configure each of hello tools individually.</span></span> <span data-ttu-id="73d4f-108">U kunt eenvoudig opschalen Hallo VM, indien nodig en stop de toepassing als deze niet in gebruik.</span><span class="sxs-lookup"><span data-stu-id="73d4f-108">You can easily scale up hello VM, if needed, and stop it when not in use.</span></span> <span data-ttu-id="73d4f-109">Deze resource wordt dus elastische en betaalbare.</span><span class="sxs-lookup"><span data-stu-id="73d4f-109">So this resource is both elastic and cost-efficient.</span></span>

<span data-ttu-id="73d4f-110">Hallo gegevens wetenschappelijke taken gedemonstreerd in dit overzicht stappen Hallo die worden beschreven in Hallo [Team gegevens wetenschap proces](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span><span class="sxs-lookup"><span data-stu-id="73d4f-110">hello data science tasks demonstrated in this walkthrough follow hello steps outlined in hello [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span></span> <span data-ttu-id="73d4f-111">Deze procedure biedt een systematisch toodata wetenschappelijke waarmee teams van gegevenswetenschappers tooeffectively via Hallo levenscyclus van het bouwen van intelligente toepassingen samenwerken.</span><span class="sxs-lookup"><span data-stu-id="73d4f-111">This process provides a systematic approach toodata science that enables teams of data scientists tooeffectively collaborate over hello lifecycle of building intelligent applications.</span></span> <span data-ttu-id="73d4f-112">Hallo gegevens wetenschap proces biedt ook een iteratieve framework voor gegevenswetenschap die kan worden gevolgd door een persoon.</span><span class="sxs-lookup"><span data-stu-id="73d4f-112">hello data science process also provides an iterative framework for data science that can be followed by an individual.</span></span>

<span data-ttu-id="73d4f-113">Analyseren we Hallo [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) gegevensset in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="73d4f-113">We analyze hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset in this walkthrough.</span></span> <span data-ttu-id="73d4f-114">Dit is een set van e-mailberichten die zijn gemarkeerd als spam of ham (wat betekent dat ze zijn geen spam), en het bevat ook een aantal statistieken Hallo inhoud van het Hallo-e-mailberichten.</span><span class="sxs-lookup"><span data-stu-id="73d4f-114">This is a set of emails that are marked as either spam or ham (meaning they are not spam), and also contains some statistics on hello content of hello emails.</span></span> <span data-ttu-id="73d4f-115">Hallo statistieken opgenomen worden besproken in Hallo naast maar één sectie.</span><span class="sxs-lookup"><span data-stu-id="73d4f-115">hello statistics included are discussed in hello next but one section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73d4f-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="73d4f-116">Prerequisites</span></span>
<span data-ttu-id="73d4f-117">Voordat u een virtuele Machine voor Linux gegevens wetenschappelijke gebruiken kunt, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="73d4f-117">Before you can use a Linux Data Science Virtual Machine, you must have hello following:</span></span>

* <span data-ttu-id="73d4f-118">Een **Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="73d4f-118">An **Azure subscription**.</span></span> <span data-ttu-id="73d4f-119">Als u nog geen een, Zie [maken van uw gratis Azure-account vandaag](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="73d4f-119">If you do not already have one, see [Create your free Azure account today](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="73d4f-120">Een [ **gegevenswetenschap Linux VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span><span class="sxs-lookup"><span data-stu-id="73d4f-120">A [**Linux data science VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span></span> <span data-ttu-id="73d4f-121">Zie voor meer informatie over het inrichten van deze virtuele machine [inrichten Hallo Linux gegevens wetenschappelijke virtuele Machine](machine-learning-data-science-linux-dsvm-intro.md).</span><span class="sxs-lookup"><span data-stu-id="73d4f-121">For information on provisioning this VM, see [Provision hello Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md).</span></span>
* <span data-ttu-id="73d4f-122">[X2Go](http://wiki.x2go.org/doku.php) geïnstalleerd op uw computer en een XFCE-sessie hebt geopend.</span><span class="sxs-lookup"><span data-stu-id="73d4f-122">[X2Go](http://wiki.x2go.org/doku.php) installed on your computer and opened an XFCE session.</span></span> <span data-ttu-id="73d4f-123">Voor informatie over het installeren en configureren van een **X2Go client**, Zie [installeren en configureren van de client X2Go](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span><span class="sxs-lookup"><span data-stu-id="73d4f-123">For information on installing and configuring an **X2Go client**, see [Installing and configuring X2Go client](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span></span> 
* <span data-ttu-id="73d4f-124">Een **AzureML account**.</span><span class="sxs-lookup"><span data-stu-id="73d4f-124">An **AzureML account**.</span></span> <span data-ttu-id="73d4f-125">Als u nog geen hebt, zich aanmelden voor een nieuw wachtwoord op Hallo [AzureML-startpagina](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="73d4f-125">If you don't already have one, sign up for new one at hello [AzureML homepage](https://studio.azureml.net/).</span></span> <span data-ttu-id="73d4f-126">Er is een gratis gebruik laag toohelp die u aan de slag.</span><span class="sxs-lookup"><span data-stu-id="73d4f-126">There is a free usage tier toohelp you get started.</span></span>

## <a name="download-hello-spambase-dataset"></a><span data-ttu-id="73d4f-127">Hallo spambase gegevensset downloaden</span><span class="sxs-lookup"><span data-stu-id="73d4f-127">Download hello spambase dataset</span></span>
<span data-ttu-id="73d4f-128">Hallo [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) gegevensset is een relatief klein set gegevens die alleen 4601 voorbeelden bevat.</span><span class="sxs-lookup"><span data-stu-id="73d4f-128">hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset is a relatively small set of data that contains only 4601 examples.</span></span> <span data-ttu-id="73d4f-129">Dit is een handige grootte toouse wanneer dat sommige van de belangrijkste functies van de Hallo Hallo gegevens wetenschappelijke VM zoals deze houdt Hallo resourcevereisten matige te demonstreren.</span><span class="sxs-lookup"><span data-stu-id="73d4f-129">This is a convenient size toouse when demonstrating that some of hello key features of hello Data Science VM as it keeps hello resource requirements modest.</span></span>

> [!NOTE]
> <span data-ttu-id="73d4f-130">In dit scenario is gemaakt op een D2 v2-formaat Linux gegevens wetenschappelijke virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="73d4f-130">This walkthrough was created on a D2 v2-sized Linux Data Science Virtual Machine.</span></span> <span data-ttu-id="73d4f-131">Deze grootte DSVM kan afhandelen Hallo procedures in dit scenario is.</span><span class="sxs-lookup"><span data-stu-id="73d4f-131">This size DSVM is capable of handling hello procedures in this walkthrough.</span></span>
>
>

<span data-ttu-id="73d4f-132">Als u meer opslagruimte nodig hebt, kunt u extra schijven maken en deze tooyour VM koppelt.</span><span class="sxs-lookup"><span data-stu-id="73d4f-132">If you need more storage space, you can create additional disks and attach them tooyour VM.</span></span> <span data-ttu-id="73d4f-133">Deze schijven gebruiken een permanente Azure-opslag, zodat hun gegevens behouden blijven zelfs wanneer het Hallo-server is ingericht vanwege tooresizing of wordt afgesloten.</span><span class="sxs-lookup"><span data-stu-id="73d4f-133">These disks use persistent Azure storage, so their data is preserved even when hello server is reprovisioned due tooresizing or is shut down.</span></span> <span data-ttu-id="73d4f-134">tooadd een schijf en koppelt u dit tooyour VM, volg de instructies in Hallo [toevoegen van een schijf tooa Linux VM](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="73d4f-134">tooadd a disk and attach it tooyour VM, follow hello instructions in [Add a disk tooa Linux VM](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="73d4f-135">Deze stappen hello Azure-opdrachtregelinterface (Azure CLI), die al is geïnstalleerd op Hallo DSVM gebruiken.</span><span class="sxs-lookup"><span data-stu-id="73d4f-135">These steps use hello Azure Command-Line Interface (Azure CLI), which is already installed on hello DSVM.</span></span> <span data-ttu-id="73d4f-136">Deze procedures is dus mogelijk volledig uit Hallo VM zelf.</span><span class="sxs-lookup"><span data-stu-id="73d4f-136">So these procedures can be done entirely from hello VM itself.</span></span> <span data-ttu-id="73d4f-137">Een andere optie tooincrease opslag is toouse [Azure files](../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="73d4f-137">Another option tooincrease storage is toouse [Azure files](../storage/files/storage-how-to-use-files-linux.md).</span></span>

<span data-ttu-id="73d4f-138">toodownload hello gegevens, open een terminalvenster en voer deze opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="73d4f-138">toodownload hello data, open a terminal window and run this command:</span></span>

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

<span data-ttu-id="73d4f-139">het gedownloade bestand Hallo niet hebben een veldnamenrij, dus we maken een ander bestand dat u beschikt over een koptekst.</span><span class="sxs-lookup"><span data-stu-id="73d4f-139">hello downloaded file does not have a header row, so let's create another file that does have a header.</span></span> <span data-ttu-id="73d4f-140">Voer deze opdracht toocreate een bestand met de juiste kopteksten Hallo:</span><span class="sxs-lookup"><span data-stu-id="73d4f-140">Run this command toocreate a file with hello appropriate headers:</span></span>

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

<span data-ttu-id="73d4f-141">Vervolgens samenvoegen van Hallo twee bestanden samen met de Hallo-opdracht:</span><span class="sxs-lookup"><span data-stu-id="73d4f-141">Then concatenate hello two files together with hello command:</span></span>

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

<span data-ttu-id="73d4f-142">Hallo gegevensset heeft verschillende typen statistieken op elk e-mailbericht:</span><span class="sxs-lookup"><span data-stu-id="73d4f-142">hello dataset has several types of statistics on each email:</span></span>

* <span data-ttu-id="73d4f-143">Kolommen, zoals ***word\_freq\_WORD*** geven Hallo percentage woorden in Hallo e-mail die overeenkomen met *WORD*.</span><span class="sxs-lookup"><span data-stu-id="73d4f-143">Columns like ***word\_freq\_WORD*** indicate hello percentage of words in hello email that match *WORD*.</span></span> <span data-ttu-id="73d4f-144">Bijvoorbeeld, als *word\_freq\_zorg* is 1, wordt 1% van alle woorden in Hallo e-mailbericht zijn *zorg*.</span><span class="sxs-lookup"><span data-stu-id="73d4f-144">For example, if *word\_freq\_make* is 1, then 1% of all words in hello email were *make*.</span></span>
* <span data-ttu-id="73d4f-145">Kolommen, zoals ***char\_freq\_CHAR*** geven Hallo percentage van alle tekens in Hallo e-mailbericht zijn *CHAR*.</span><span class="sxs-lookup"><span data-stu-id="73d4f-145">Columns like ***char\_freq\_CHAR*** indicate hello percentage of all characters in hello email that were *CHAR*.</span></span>
* <span data-ttu-id="73d4f-146">***kapitaal\_uitvoeren\_lengte\_langste*** is Hallo langste lengte van een reeks van hoofdletters.</span><span class="sxs-lookup"><span data-stu-id="73d4f-146">***capital\_run\_length\_longest*** is hello longest length of a sequence of capital letters.</span></span>
* <span data-ttu-id="73d4f-147">***kapitaal\_uitvoeren\_lengte\_gemiddelde*** Hallo gemiddelde duur van alle reeksen hoofdletters is.</span><span class="sxs-lookup"><span data-stu-id="73d4f-147">***capital\_run\_length\_average*** is hello average length of all sequences of capital letters.</span></span>
* <span data-ttu-id="73d4f-148">***kapitaal\_uitvoeren\_lengte\_totale*** Hallo totale lengte van alle reeksen hoofdletters is.</span><span class="sxs-lookup"><span data-stu-id="73d4f-148">***capital\_run\_length\_total*** is hello total length of all sequences of capital letters.</span></span>
* <span data-ttu-id="73d4f-149">***spam*** geeft aan of e-mail hello wordt beschouwd als spam of niet (1 = spam, 0 = niet spam).</span><span class="sxs-lookup"><span data-stu-id="73d4f-149">***spam*** indicates whether hello email was considered spam or not (1 = spam, 0 = not spam).</span></span>

## <a name="explore-hello-dataset-with-microsoft-r-open"></a><span data-ttu-id="73d4f-150">Hallo gegevensset met Microsoft R Open verkennen</span><span class="sxs-lookup"><span data-stu-id="73d4f-150">Explore hello dataset with Microsoft R Open</span></span>
<span data-ttu-id="73d4f-151">Laten we Hallo gegevens controleren en voer enkele eenvoudige machine learning R. Hello gegevens wetenschappelijke VM wordt geleverd met [Microsoft R Open](https://mran.revolutionanalytics.com/open/) vooraf zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="73d4f-151">Let's examine hello data and do some basic machine learning with R. hello Data Science VM comes with [Microsoft R Open](https://mran.revolutionanalytics.com/open/) pre-installed.</span></span> <span data-ttu-id="73d4f-152">Hallo bieden multithreaded math bibliotheken in deze versie van R betere prestaties dan in verschillende versies met één thread.</span><span class="sxs-lookup"><span data-stu-id="73d4f-152">hello multithreaded math libraries in this version of R offer better performance than various single-threaded versions.</span></span> <span data-ttu-id="73d4f-153">Microsoft R Open biedt ook reproduceerbaarheid met behulp van een momentopname van Hallo CRAN pakket opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="73d4f-153">Microsoft R Open also provides reproducibility by using a snapshot of hello CRAN package repository.</span></span>

<span data-ttu-id="73d4f-154">tooget kopieën van Hallo codevoorbeelden in dit scenario, kloon Hallo gebruikt **Azure-Machine-Learning--Gegevenswetenschap** opslagplaats met git, dat vooraf is geïnstalleerd op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="73d4f-154">tooget copies of hello code samples used in this walkthrough, clone hello **Azure-Machine-Learning-Data-Science** repository using git, which is pre-installed on hello VM.</span></span> <span data-ttu-id="73d4f-155">Voer vanaf Hallo git-opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="73d4f-155">From hello git command line, run:</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="73d4f-156">Open een terminalvenster en een nieuwe R-sessie starten met Hallo R interactieve console.</span><span class="sxs-lookup"><span data-stu-id="73d4f-156">Open a terminal window and start a new R session with hello R interactive console.</span></span>

> [!NOTE]
> <span data-ttu-id="73d4f-157">U kunt ook RStudio gebruiken voor Hallo procedures te volgen.</span><span class="sxs-lookup"><span data-stu-id="73d4f-157">You can also use RStudio for hello following procedures.</span></span> <span data-ttu-id="73d4f-158">tooinstall RStudio, geef dan deze opdracht in een terminal:`./Desktop/DSVM\ tools/installRStudio.sh`</span><span class="sxs-lookup"><span data-stu-id="73d4f-158">tooinstall RStudio, execute this command at a terminal: `./Desktop/DSVM\ tools/installRStudio.sh`</span></span>
>
>

<span data-ttu-id="73d4f-159">tooimport hello gegevens en stelt u de omgeving hello, uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="73d4f-159">tooimport hello data and set up hello environment, run:</span></span>

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

<span data-ttu-id="73d4f-160">toosee samenvattende statistieken over elke kolom:</span><span class="sxs-lookup"><span data-stu-id="73d4f-160">toosee summary statistics about each column:</span></span>

    summary(data)

<span data-ttu-id="73d4f-161">Voor een andere weergave van Hallo gegevens:</span><span class="sxs-lookup"><span data-stu-id="73d4f-161">For a different view of hello data:</span></span>

    str(data)

<span data-ttu-id="73d4f-162">Dit toont u type van elke variabele Hallo en Hallo eerst enkele waarden in Hallo gegevensset.</span><span class="sxs-lookup"><span data-stu-id="73d4f-162">This shows you hello type of each variable and hello first few values in hello dataset.</span></span>

<span data-ttu-id="73d4f-163">Hallo *spam* kolom als een geheel getal is gelezen, maar het is daadwerkelijk een categorische variabele (of factor).</span><span class="sxs-lookup"><span data-stu-id="73d4f-163">hello *spam* column was read as an integer, but it's actually a categorical variable (or factor).</span></span> <span data-ttu-id="73d4f-164">tooset het type:</span><span class="sxs-lookup"><span data-stu-id="73d4f-164">tooset its type:</span></span>

    data$spam <- as.factor(data$spam)

<span data-ttu-id="73d4f-165">toodo sommige experimentele analyses, gebruik Hallo [ggplot2](http://ggplot2.org/) inpakken, een populaire grafische-bibliotheek voor R dat al is geïnstalleerd op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="73d4f-165">toodo some exploratory analysis, use hello [ggplot2](http://ggplot2.org/) package, a popular graphing library for R that is already installed on hello VM.</span></span> <span data-ttu-id="73d4f-166">Opmerking van Hallo samenvattingsgegevens dat eerder is weergegeven, dat we samenvattende statistieken op Hallo frequentie van Hallo uitroepteken teken hebben.</span><span class="sxs-lookup"><span data-stu-id="73d4f-166">Note, from hello summary data displayed earlier, that we have summary statistics on hello frequency of hello exclamation mark character.</span></span> <span data-ttu-id="73d4f-167">Laten we deze frequenties hier tekenen Hello volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="73d4f-167">Let's plot those frequencies here with hello following commands:</span></span>

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="73d4f-168">Aangezien Hallo nul balk Hallo tekent scheeftrekken wordt, gaan we deze verwijderen uit:</span><span class="sxs-lookup"><span data-stu-id="73d4f-168">Since hello zero bar is skewing hello plot, let's get rid of it:</span></span>

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="73d4f-169">Er is een niet-triviale dichtheid dan 1, waarin u geïnteresseerd.</span><span class="sxs-lookup"><span data-stu-id="73d4f-169">There is a non-trivial density above 1 that looks interesting.</span></span> <span data-ttu-id="73d4f-170">Bekijk alleen die gegevens in:</span><span class="sxs-lookup"><span data-stu-id="73d4f-170">Let's look at just that data:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="73d4f-171">Vervolgens splitsen door spam tegenover ham:</span><span class="sxs-lookup"><span data-stu-id="73d4f-171">Then split it by spam vs ham:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

<span data-ttu-id="73d4f-172">Deze voorbeelden moeten u in staat stellen toomake vergelijkbare curve van Hallo andere kolommen tooexplore Hallo in deze gegevens.</span><span class="sxs-lookup"><span data-stu-id="73d4f-172">These examples should enable you toomake similar plots of hello other columns tooexplore hello data contained in them.</span></span>

## <a name="train-and-test-an-ml-model"></a><span data-ttu-id="73d4f-173">Trainen en te testen ML-model</span><span class="sxs-lookup"><span data-stu-id="73d4f-173">Train and test an ML model</span></span>
<span data-ttu-id="73d4f-174">Nu gaan we trein een aantal machine learning tooclassify Hallo e-mailberichten in Hallo gegevensset modellen bevat een span of ham.</span><span class="sxs-lookup"><span data-stu-id="73d4f-174">Now let's train a couple of machine learning models tooclassify hello emails in hello dataset as containing either span or ham.</span></span> <span data-ttu-id="73d4f-175">We een decision tree-model en een willekeurige forest-model in deze sectie trainen en vervolgens de juistheid van hun voorspellingen.</span><span class="sxs-lookup"><span data-stu-id="73d4f-175">We train a decision tree model and a random forest model in this section and then test their accuracy of their predictions.</span></span>

> [!NOTE]
> <span data-ttu-id="73d4f-176">Hallo rpart (recursieve partitioneren en Regressiestructuren)-pakket gebruikt in de volgende code Hallo is al geïnstalleerd op Hallo gegevens wetenschappelijke VM.</span><span class="sxs-lookup"><span data-stu-id="73d4f-176">hello rpart (Recursive Partitioning and Regression Trees) package used in hello following code is already installed on hello Data Science VM.</span></span>
>
>

<span data-ttu-id="73d4f-177">Eerst laten we Hallo gegevensset splitsen in trainings- en testset sets:</span><span class="sxs-lookup"><span data-stu-id="73d4f-177">First, let's split hello dataset into training and test sets:</span></span>

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

<span data-ttu-id="73d4f-178">En maak vervolgens een decision tree tooclassify Hallo e-mailberichten.</span><span class="sxs-lookup"><span data-stu-id="73d4f-178">And then create a decision tree tooclassify hello emails.</span></span>

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

<span data-ttu-id="73d4f-179">Hier volgt Hallo resultaat:</span><span class="sxs-lookup"><span data-stu-id="73d4f-179">Here is hello result:</span></span>

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

<span data-ttu-id="73d4f-181">hoe goed worden uitgevoerd op Hallo training toodetermine ingesteld, Hallo volgende code gebruiken:</span><span class="sxs-lookup"><span data-stu-id="73d4f-181">toodetermine how well it performs on hello training set, use hello following code:</span></span>

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="73d4f-182">toodetermine hoe goed worden uitgevoerd op Hallo testset:</span><span class="sxs-lookup"><span data-stu-id="73d4f-182">toodetermine how well it performs on hello test set:</span></span>

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="73d4f-183">U kunt ook gaan we een willekeurige forest-model.</span><span class="sxs-lookup"><span data-stu-id="73d4f-183">Let's also try a random forest model.</span></span> <span data-ttu-id="73d4f-184">Willekeurige forests tal van beslissingsstructuren trainen en uitvoer van een klasse die Hallo-modus van Hallo classificaties uit alle Hallo afzonderlijke beslissingsstructuren.</span><span class="sxs-lookup"><span data-stu-id="73d4f-184">Random forests train a multitude of decision trees and output a class that is hello mode of hello classifications from all of hello individual decision trees.</span></span> <span data-ttu-id="73d4f-185">Ze bieden een krachtigere machine learning-benadering als voor de neiging Hallo van een decision tree model toooverfit een gegevensset training worden gecorrigeerd.</span><span class="sxs-lookup"><span data-stu-id="73d4f-185">They provide a more powerful machine learning approach as they correct for hello tendency of a decision tree model toooverfit a training dataset.</span></span>

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-tooazure-ml"></a><span data-ttu-id="73d4f-186">Een model tooAzure ML implementeren</span><span class="sxs-lookup"><span data-stu-id="73d4f-186">Deploy a model tooAzure ML</span></span>
<span data-ttu-id="73d4f-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) is een cloudservice die maakt het eenvoudig toobuild en implementeren van predictive analytics-modellen.</span><span class="sxs-lookup"><span data-stu-id="73d4f-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) is a cloud service that makes it easy toobuild and deploy predictive analytics models.</span></span> <span data-ttu-id="73d4f-188">Een van de Hallo nice functies van AzureML is de mogelijkheid toopublish R functioneren als een webservice.</span><span class="sxs-lookup"><span data-stu-id="73d4f-188">One of hello nice features of AzureML is its ability toopublish any R function as a web service.</span></span> <span data-ttu-id="73d4f-189">Hallo AzureML-R-pakket maakt implementatie eenvoudig toodo vanaf onze R-sessie op Hallo DSVM.</span><span class="sxs-lookup"><span data-stu-id="73d4f-189">hello AzureML R package makes deployment easy toodo right from our R session on hello DSVM.</span></span>

<span data-ttu-id="73d4f-190">toodeploy hello besluit structuur code uit de vorige sectie hello, moet u toosign in tooAzure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="73d4f-190">toodeploy hello decision tree code from hello previous section, you need toosign in tooAzure Machine Learning Studio.</span></span> <span data-ttu-id="73d4f-191">U moet uw werkruimte-ID en een token toosign autorisatie in.</span><span class="sxs-lookup"><span data-stu-id="73d4f-191">You need your workspace ID and an authorization token toosign in.</span></span> <span data-ttu-id="73d4f-192">toofind deze waarden en geïnitialiseerd Hallo AzureML variabelen met hen:</span><span class="sxs-lookup"><span data-stu-id="73d4f-192">toofind these values and initialize hello AzureML variables with them:</span></span>

<span data-ttu-id="73d4f-193">Selecteer **instellingen** Hallo links menu.</span><span class="sxs-lookup"><span data-stu-id="73d4f-193">Select **Settings** on hello left-hand menu.</span></span> <span data-ttu-id="73d4f-194">Opmerking uw **WERKRUIMTE-ID**.</span><span class="sxs-lookup"><span data-stu-id="73d4f-194">Note your **WORKSPACE ID**.</span></span> <span data-ttu-id="73d4f-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span><span class="sxs-lookup"><span data-stu-id="73d4f-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span></span>

<span data-ttu-id="73d4f-196">Selecteer **autorisatie Tokens** uit Hallo overhead menu en Opmerking uw **primaire autorisatie Token**.![ 3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span><span class="sxs-lookup"><span data-stu-id="73d4f-196">Select **Authorization Tokens** from hello overhead menu and note your **Primary Authorization Token**.![3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span></span>

<span data-ttu-id="73d4f-197">Load Hallo **AzureML** van het pakket en stelt u waarden van variabelen Hallo met uw token en werkruimte-ID in uw R-sessie op Hallo DSVM:</span><span class="sxs-lookup"><span data-stu-id="73d4f-197">Load hello **AzureML** package and then set values of hello variables with your token and workspace ID in your R session on hello DSVM:</span></span>

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


<span data-ttu-id="73d4f-198">Laten we vereenvoudigen Hallo model toomake deze demonstratie eenvoudiger tooimplement.</span><span class="sxs-lookup"><span data-stu-id="73d4f-198">Let's simplify hello model toomake this demonstration easier tooimplement.</span></span> <span data-ttu-id="73d4f-199">Kies Hallo drie variabelen in Hallo besluit dichtstbijzijnde toohello hoofddomeinstructuur en bouwen van een nieuwe boomstructuur met behulp van alleen die drie variabelen:</span><span class="sxs-lookup"><span data-stu-id="73d4f-199">Pick hello three variables in hello decision tree closest toohello root and build a new tree using just those three variables:</span></span>

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

<span data-ttu-id="73d4f-200">Moet een voorspellingsfunctie waarmee Hallo functies als invoer en retourneert Hallo voorspelde waarden:</span><span class="sxs-lookup"><span data-stu-id="73d4f-200">We need a prediction function that takes hello features as an input and returns hello predicted values:</span></span>

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

<span data-ttu-id="73d4f-201">Hallo predictSpam functie tooAzureML met Hallo publiceren **publishWebService** functie:</span><span class="sxs-lookup"><span data-stu-id="73d4f-201">Publish hello predictSpam function tooAzureML using hello **publishWebService** function:</span></span>

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

<span data-ttu-id="73d4f-202">Deze functie omvat Hallo **predictSpam** werkt, maakt u een webservice die met de naam **spamWebService** gedefinieerd met in- en uitgangen en retourneert informatie over nieuwe Hallo-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="73d4f-202">This function takes hello **predictSpam** function, creates a web service named **spamWebService** with defined inputs and outputs, and returns information about hello new endpoint.</span></span>

<span data-ttu-id="73d4f-203">Details weergeven van Hallo gepubliceerd webservice, inclusief de API-eindpunt en toegangssleutels met Hallo-opdracht:</span><span class="sxs-lookup"><span data-stu-id="73d4f-203">View details of hello published web service, including its API endpoint and access keys with hello command:</span></span>

    spamWebService[[2]]

<span data-ttu-id="73d4f-204">tootry het uit op de eerste 10 rijen van testset Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="73d4f-204">tootry it out on hello first 10 rows of hello test set:</span></span>

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a><span data-ttu-id="73d4f-205">Andere hulpprogramma's gebruiken</span><span class="sxs-lookup"><span data-stu-id="73d4f-205">Use other tools available</span></span>
<span data-ttu-id="73d4f-206">Hallo resterende secties ziet u hoe toouse sommige Hallo-hulpprogramma's geïnstalleerd op Hallo Linux gegevens wetenschappelijke VM. Hier volgt de lijst Hallo van hulpprogramma's beschreven:</span><span class="sxs-lookup"><span data-stu-id="73d4f-206">hello remaining sections show how toouse some of hello tools installed on hello Linux Data Science VM.Here is hello list of tools discussed:</span></span>

* <span data-ttu-id="73d4f-207">XGBoost</span><span class="sxs-lookup"><span data-stu-id="73d4f-207">XGBoost</span></span>
* <span data-ttu-id="73d4f-208">Python</span><span class="sxs-lookup"><span data-stu-id="73d4f-208">Python</span></span>
* <span data-ttu-id="73d4f-209">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="73d4f-209">Jupyterhub</span></span>
* <span data-ttu-id="73d4f-210">Rammelaar</span><span class="sxs-lookup"><span data-stu-id="73d4f-210">Rattle</span></span>
* <span data-ttu-id="73d4f-211">PostgreSQL & Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="73d4f-211">PostgreSQL & Squirrel SQL</span></span>
* <span data-ttu-id="73d4f-212">SQL Server-datawarehouse</span><span class="sxs-lookup"><span data-stu-id="73d4f-212">SQL Server Data Warehouse</span></span>

## <a name="xgboost"></a><span data-ttu-id="73d4f-213">XGBoost</span><span class="sxs-lookup"><span data-stu-id="73d4f-213">XGBoost</span></span>
<span data-ttu-id="73d4f-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) is een hulpprogramma waarmee een snelle en nauwkeurige gestimuleerd structuur-implementatie.</span><span class="sxs-lookup"><span data-stu-id="73d4f-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) is a tool that provides a fast and accurate boosted tree implementation.</span></span>

    require(xgboost)
    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

    bst <- xgboost(data = data.matrix(trainSet[,0:57]), label = trainSet$spam, nthread = 2, nrounds = 2, objective = "binary:logistic")

    pred <- predict(bst, data.matrix(testSet[, 0:57]))
    accuracy <- 1.0 - mean(as.numeric(pred > 0.5) != testSet$spam)
    print(paste("test accuracy = ", accuracy))

<span data-ttu-id="73d4f-215">XGBoost kunnen ook aanroepen vanuit python of een opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="73d4f-215">XGBoost can also call from python or a command line.</span></span>

## <a name="python"></a><span data-ttu-id="73d4f-216">Python</span><span class="sxs-lookup"><span data-stu-id="73d4f-216">Python</span></span>
<span data-ttu-id="73d4f-217">Voor de ontwikkeling met behulp van Python, zijn distributies van Hallo Anaconda Python 2.7 en 3.5 geïnstalleerd in Hallo DSVM.</span><span class="sxs-lookup"><span data-stu-id="73d4f-217">For development using Python, hello Anaconda Python distributions 2.7 and 3.5 have been installed in hello DSVM.</span></span>

> [!NOTE]
> <span data-ttu-id="73d4f-218">Hallo Anaconda distributie omvat [Condas](http://conda.pydata.org/docs/index.html), die mag gebruikte toocreate aangepaste omgevingen voor Python die verschillende versies en/of de pakketten die in deze geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="73d4f-218">hello Anaconda distribution includes [Condas](http://conda.pydata.org/docs/index.html), which can be used toocreate custom environments for Python that have different versions and/or packages installed in them.</span></span>
>
>

<span data-ttu-id="73d4f-219">We lezen in een aantal Hallo spambase gegevensset en Hallo e-mailberichten classificeren met ondersteuning voor virtuele machines vector in scikit-informatie:</span><span class="sxs-lookup"><span data-stu-id="73d4f-219">Let's read in some of hello spambase dataset and classify hello emails with support vector machines in scikit-learn:</span></span>

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="73d4f-220">toomake voorspellingen:</span><span class="sxs-lookup"><span data-stu-id="73d4f-220">toomake predictions:</span></span>

    clf.predict(X.ix[0:20, :])

<span data-ttu-id="73d4f-221">tooshow hoe toopublish een eindpunt voor met AzureML, gaan we maken een eenvoudigere model Hallo drie variabelen als toen we Hallo R model eerder hebt gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="73d4f-221">tooshow how toopublish an AzureML endpoint, let's make a simpler model hello three variables as we did when we published hello R model previously.</span></span>

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="73d4f-222">toopublish hello model tooAzureML:</span><span class="sxs-lookup"><span data-stu-id="73d4f-222">toopublish hello model tooAzureML:</span></span>

    # Publish hello model.
    workspace_id = "<workspace-id>"
    workspace_token = "<workspace-token>"
    from azureml import services
    @services.publish(workspace_id, workspace_token)
    @services.types(char_freq_dollar = float, word_freq_remove = float, word_freq_hp = float)
    @services.returns(int) # 0 or 1
    def predictSpam(char_freq_dollar, word_freq_remove, word_freq_hp):
        inputArray = [char_freq_dollar, word_freq_remove, word_freq_hp]
        return clf.predict(inputArray)

    # Get some info about hello resulting model.
    predictSpam.service.url
    predictSpam.service.api_key

    # Call hello model
    predictSpam.service(1, 1, 1)

> [!NOTE]
> <span data-ttu-id="73d4f-223">Dit is alleen beschikbaar voor python 2.7 en nog niet wordt ondersteund op 3.5.</span><span class="sxs-lookup"><span data-stu-id="73d4f-223">This is only available for python 2.7 and is not yet supported on 3.5.</span></span> <span data-ttu-id="73d4f-224">Voer met **/anaconda/bin/python2.7**.</span><span class="sxs-lookup"><span data-stu-id="73d4f-224">Run with **/anaconda/bin/python2.7**.</span></span>
>
>

## <a name="jupyterhub"></a><span data-ttu-id="73d4f-225">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="73d4f-225">Jupyterhub</span></span>
<span data-ttu-id="73d4f-226">Hallo Anaconda distributie in Hallo DSVM wordt geleverd met een Jupyter-notebook, een omgeving met meerdere platforms tooshare Python, R of Julia code en analyse.</span><span class="sxs-lookup"><span data-stu-id="73d4f-226">hello Anaconda distribution in hello DSVM comes with a Jupyter notebook, a cross-platform environment tooshare Python, R, or Julia code and analysis.</span></span> <span data-ttu-id="73d4f-227">Hallo Jupyter-notebook toegankelijk is via JupyterHub.</span><span class="sxs-lookup"><span data-stu-id="73d4f-227">hello Jupyter notebook is accessed through JupyterHub.</span></span> <span data-ttu-id="73d4f-228">U zich aanmelden met uw lokale Linux-gebruikersnaam en wachtwoord op ***https://\<VM DNS-naam of IP-adres\>: 8000 /***.</span><span class="sxs-lookup"><span data-stu-id="73d4f-228">You sign in using your local Linux user name and password at ***https://\<VM DNS name or IP Address\>:8000/***.</span></span> <span data-ttu-id="73d4f-229">Alle configuratiebestanden voor JupyterHub zijn gevonden in map **/etc/jupyterhub**.</span><span class="sxs-lookup"><span data-stu-id="73d4f-229">All configuration files for JupyterHub are found in directory **/etc/jupyterhub**.</span></span>

<span data-ttu-id="73d4f-230">Verschillende voorbeeldquery notitieblokken zijn al geïnstalleerd op Hallo VM:</span><span class="sxs-lookup"><span data-stu-id="73d4f-230">Several sample notebooks are already installed on hello VM:</span></span>

* <span data-ttu-id="73d4f-231">Zie Hallo [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) voor een voorbeeld Python-notebook.</span><span class="sxs-lookup"><span data-stu-id="73d4f-231">See hello [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) for a sample Python notebook.</span></span>
* <span data-ttu-id="73d4f-232">Zie [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) voor een voorbeeld van een **R** notebook.</span><span class="sxs-lookup"><span data-stu-id="73d4f-232">See [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) for a sample **R** notebook.</span></span>
* <span data-ttu-id="73d4f-233">Zie Hallo [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) voor een ander voorbeeld **Python** notebook.</span><span class="sxs-lookup"><span data-stu-id="73d4f-233">See hello [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) for another sample **Python** notebook.</span></span>

> [!NOTE]
> <span data-ttu-id="73d4f-234">Hallo Julia taal is ook beschikbaar via de opdrachtregel Hallo op Hallo Linux gegevens wetenschappelijke VM.</span><span class="sxs-lookup"><span data-stu-id="73d4f-234">hello Julia language is also available from hello command line on hello Linux Data Science VM.</span></span>
>
>

## <a name="rattle"></a><span data-ttu-id="73d4f-235">Rammelaar</span><span class="sxs-lookup"><span data-stu-id="73d4f-235">Rattle</span></span>
<span data-ttu-id="73d4f-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (R analytische hulpprogramma tooLearn eenvoudig hello) is een grafisch hulpprogramma R voor gegevensanalyse.</span><span class="sxs-lookup"><span data-stu-id="73d4f-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (hello R Analytical Tool tooLearn Easily) is a graphical R tool for data mining.</span></span> <span data-ttu-id="73d4f-237">Heeft een intuïtieve interface waarmee u eenvoudig tooload kunt, verkennen, en gegevens transformeren en bouwen en evalueren van modellen.</span><span class="sxs-lookup"><span data-stu-id="73d4f-237">It has an intuitive interface that makes it easy tooload, explore, and transform data and build and evaluate models.</span></span>  <span data-ttu-id="73d4f-238">Hallo artikel [Rattle: A Data Mining GUI voor R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) biedt een overzicht over de functies.</span><span class="sxs-lookup"><span data-stu-id="73d4f-238">hello article [Rattle: A Data Mining GUI for R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) provides a walkthrough that demonstrates its features.</span></span>

<span data-ttu-id="73d4f-239">Installeren en start Rammelaar Hello volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="73d4f-239">Install and start Rattle with hello following commands:</span></span>

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> <span data-ttu-id="73d4f-240">De installatie is niet vereist op Hallo DSVM.</span><span class="sxs-lookup"><span data-stu-id="73d4f-240">Installation is not required on hello DSVM.</span></span> <span data-ttu-id="73d4f-241">Maar Rammelaar wordt u mogelijk gevraagd extra pakketten tooinstall wanneer deze wordt geladen.</span><span class="sxs-lookup"><span data-stu-id="73d4f-241">But Rattle may prompt you tooinstall additional packages when it loads.</span></span>
>
>

<span data-ttu-id="73d4f-242">Rammelaar maakt gebruik van een tabblad-gebaseerde interface.</span><span class="sxs-lookup"><span data-stu-id="73d4f-242">Rattle uses a tab-based interface.</span></span> <span data-ttu-id="73d4f-243">De meeste Hallo tabbladen overeenkomen toosteps in Hallo [gegevens wetenschap proces](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), zoals het laden van gegevens of het verkennen.</span><span class="sxs-lookup"><span data-stu-id="73d4f-243">Most of hello tabs correspond toosteps in hello [Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), like loading data or exploring it.</span></span> <span data-ttu-id="73d4f-244">Hallo gegevens wetenschap proces loopt van links tooright via Hallo tabbladen.</span><span class="sxs-lookup"><span data-stu-id="73d4f-244">hello data science process flows from left tooright through hello tabs.</span></span> <span data-ttu-id="73d4f-245">Maar Hallo laatste tabblad bevat een logboek van Hallo R-opdrachten door Rammelaar worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="73d4f-245">But hello last tab contains a log of hello R commands run by Rattle.</span></span>

<span data-ttu-id="73d4f-246">tooload en Hallo gegevensset configureren:</span><span class="sxs-lookup"><span data-stu-id="73d4f-246">tooload and configure hello dataset:</span></span>

* <span data-ttu-id="73d4f-247">tooload Hallo-bestand, selecteer Hallo **gegevens** tabblad vervolgens</span><span class="sxs-lookup"><span data-stu-id="73d4f-247">tooload hello file, select hello **Data** tab, then</span></span>
* <span data-ttu-id="73d4f-248">Kies Hallo selector volgende te**Filename** en kies **spambaseHeaders.data**.</span><span class="sxs-lookup"><span data-stu-id="73d4f-248">Choose hello selector next too**Filename** and choose **spambaseHeaders.data**.</span></span>
* <span data-ttu-id="73d4f-249">tooload Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="73d4f-249">tooload hello file.</span></span> <span data-ttu-id="73d4f-250">Selecteer **Execute** in Hallo bovenste rij knoppen.</span><span class="sxs-lookup"><span data-stu-id="73d4f-250">select **Execute** in hello top row of buttons.</span></span> <span data-ttu-id="73d4f-251">U ziet een overzicht van elke kolom, met inbegrip van het geïdentificeerde gegevenstype, of u nu invoer, een doel of andere type variabele en het aantal unieke waarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="73d4f-251">You should see a summary of each column, including its identified data type, whether it's an input, a target, or other type of variable, and hello number of unique values.</span></span>
* <span data-ttu-id="73d4f-252">Rammelaar geconstateerd correct Hallo **spam** kolom als Hallo doel.</span><span class="sxs-lookup"><span data-stu-id="73d4f-252">Rattle has correctly identified hello **spam** column as hello target.</span></span> <span data-ttu-id="73d4f-253">Selecteer Hallo spam kolom en vervolgens set Hallo **gegevens doeltype** te**Categoric**.</span><span class="sxs-lookup"><span data-stu-id="73d4f-253">Select hello spam column, then set hello **Target Data Type** too**Categoric**.</span></span>

<span data-ttu-id="73d4f-254">tooexplore hello gegevens:</span><span class="sxs-lookup"><span data-stu-id="73d4f-254">tooexplore hello data:</span></span>

* <span data-ttu-id="73d4f-255">Selecteer Hallo **verkennen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="73d4f-255">Select hello **Explore** tab.</span></span>
* <span data-ttu-id="73d4f-256">Klik op **samenvatting**, klikt u vervolgens **Execute**, toosee enige informatie over de typen Hallo-variabelen en sommige samenvattende statistieken.</span><span class="sxs-lookup"><span data-stu-id="73d4f-256">Click **Summary**, then **Execute**, toosee some information about hello variable types and some summary statistics.</span></span>
* <span data-ttu-id="73d4f-257">tooview andere soorten statistieken over elke variabele, selecteer andere opties zoals **Beschrijf** of **basisbeginselen**.</span><span class="sxs-lookup"><span data-stu-id="73d4f-257">tooview other types of statistics about each variable, select other options like **Describe** or **Basics**.</span></span>

<span data-ttu-id="73d4f-258">Hallo **verkennen** tabblad kunt u ook toogenerate veel begrijpelijke manier mee worden uitgezet.</span><span class="sxs-lookup"><span data-stu-id="73d4f-258">hello **Explore** tab also allows you toogenerate many insightful plots.</span></span> <span data-ttu-id="73d4f-259">een histogram van Hallo gegevens tooplot:</span><span class="sxs-lookup"><span data-stu-id="73d4f-259">tooplot a histogram of hello data:</span></span>

* <span data-ttu-id="73d4f-260">Selecteer **distributies**.</span><span class="sxs-lookup"><span data-stu-id="73d4f-260">Select **Distributions**.</span></span>
* <span data-ttu-id="73d4f-261">Controleer **Histogram** voor **word_freq_remove** en **word_freq_you**.</span><span class="sxs-lookup"><span data-stu-id="73d4f-261">Check **Histogram** for **word_freq_remove** and **word_freq_you**.</span></span>
* <span data-ttu-id="73d4f-262">Selecteer **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="73d4f-262">Select **Execute**.</span></span> <span data-ttu-id="73d4f-263">U ziet dat beide dichtheid worden uitgezet in een grafiekvenster van één wanneer het duidelijk is dat Hallo woord "u" vaker wordt weergegeven in e-mailberichten dan 'verwijderen'.</span><span class="sxs-lookup"><span data-stu-id="73d4f-263">You should see both density plots in a single graph window, where it is clear that hello word "you" appears much more frequently in emails than "remove".</span></span>

<span data-ttu-id="73d4f-264">Er zijn ook Hallo correlatie waarnemingspunten interessante.</span><span class="sxs-lookup"><span data-stu-id="73d4f-264">hello Correlation plots are also interesting.</span></span> <span data-ttu-id="73d4f-265">toocreate een:</span><span class="sxs-lookup"><span data-stu-id="73d4f-265">toocreate one:</span></span>

* <span data-ttu-id="73d4f-266">Kies **correlatie** als Hallo **Type**, klikt u vervolgens</span><span class="sxs-lookup"><span data-stu-id="73d4f-266">Choose **Correlation** as hello **Type**, then</span></span>
* <span data-ttu-id="73d4f-267">Selecteer **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="73d4f-267">Select **Execute**.</span></span>
* <span data-ttu-id="73d4f-268">Rammelaar waarschuwt u raadt maximaal 40 variabelen.</span><span class="sxs-lookup"><span data-stu-id="73d4f-268">Rattle warns you that it recommends a maximum of 40 variables.</span></span> <span data-ttu-id="73d4f-269">Selecteer **Ja** tooview Hallo tekent.</span><span class="sxs-lookup"><span data-stu-id="73d4f-269">Select **Yes** tooview hello plot.</span></span>

<span data-ttu-id="73d4f-270">Er zijn enkele interessante correlaties die afkomstig van zijn: 'technologie' sterk te worden gecorreleerd 'HP' en 'labs' voor het voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="73d4f-270">There are some interesting correlations that come up: "technology" is strongly correlated too"HP" and "labs", for example.</span></span> <span data-ttu-id="73d4f-271">Dit wordt ook sterk gecorreleerd te '650', omdat het netnummer Hallo van Hallo gegevensset donors 650.</span><span class="sxs-lookup"><span data-stu-id="73d4f-271">It is also strongly correlated too"650", because hello area code of hello dataset donors is 650.</span></span>

<span data-ttu-id="73d4f-272">Hallo numerieke waarden voor Hallo correlaties tussen woorden zijn beschikbaar in Hallo verkennen venster.</span><span class="sxs-lookup"><span data-stu-id="73d4f-272">hello numeric values for hello correlations between words are available in hello Explore window.</span></span> <span data-ttu-id="73d4f-273">Het is interessant toonote, bijvoorbeeld 'technologie' op de negatieve worden gecorreleerd met "uw" en 'geld'.</span><span class="sxs-lookup"><span data-stu-id="73d4f-273">It is interesting toonote, for example, that "technology" is negatively correlated with "your" and "money".</span></span>

<span data-ttu-id="73d4f-274">Rammelaar kunt Hallo gegevensset toohandle transformeren enkele veelvoorkomende problemen.</span><span class="sxs-lookup"><span data-stu-id="73d4f-274">Rattle can transform hello dataset toohandle some common issues.</span></span> <span data-ttu-id="73d4f-275">Bijvoorbeeld, u kunt functies toorescale, rekenen ontbrekende waarden, uitschieters verwerken en variabelen of opmerkingen met ontbrekende gegevens verwijderen.</span><span class="sxs-lookup"><span data-stu-id="73d4f-275">For example, it allows you toorescale features, impute missing values, handle outliers, and remove variables or observations with missing data.</span></span> <span data-ttu-id="73d4f-276">Rammelaar kunt ook regels van de koppeling tussen opmerkingen en/of variabelen identificeren.</span><span class="sxs-lookup"><span data-stu-id="73d4f-276">Rattle can also identify association rules between observations and/or variables.</span></span> <span data-ttu-id="73d4f-277">Deze tabbladen zijn buiten het bereik van deze Introductie.</span><span class="sxs-lookup"><span data-stu-id="73d4f-277">These tabs are out of scope for this introductory walkthrough.</span></span>

<span data-ttu-id="73d4f-278">Rammelaar kunt ook cluster analyse uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="73d4f-278">Rattle can also perform cluster analysis.</span></span> <span data-ttu-id="73d4f-279">Laten we enkele functies toomake Hallo uitvoer eenvoudiger tooread uitsluiten.</span><span class="sxs-lookup"><span data-stu-id="73d4f-279">Let's exclude some features toomake hello output easier tooread.</span></span> <span data-ttu-id="73d4f-280">Op Hallo **gegevens** Kies **negeren** volgende tooeach van Hallo variabelen behalve deze tien items:</span><span class="sxs-lookup"><span data-stu-id="73d4f-280">On hello **Data** tab, choose **Ignore** next tooeach of hello variables except these ten items:</span></span>

* <span data-ttu-id="73d4f-281">word_freq_hp</span><span class="sxs-lookup"><span data-stu-id="73d4f-281">word_freq_hp</span></span>
* <span data-ttu-id="73d4f-282">word_freq_technology</span><span class="sxs-lookup"><span data-stu-id="73d4f-282">word_freq_technology</span></span>
* <span data-ttu-id="73d4f-283">word_freq_george</span><span class="sxs-lookup"><span data-stu-id="73d4f-283">word_freq_george</span></span>
* <span data-ttu-id="73d4f-284">word_freq_remove</span><span class="sxs-lookup"><span data-stu-id="73d4f-284">word_freq_remove</span></span>
* <span data-ttu-id="73d4f-285">word_freq_your</span><span class="sxs-lookup"><span data-stu-id="73d4f-285">word_freq_your</span></span>
* <span data-ttu-id="73d4f-286">word_freq_dollar</span><span class="sxs-lookup"><span data-stu-id="73d4f-286">word_freq_dollar</span></span>
* <span data-ttu-id="73d4f-287">word_freq_money</span><span class="sxs-lookup"><span data-stu-id="73d4f-287">word_freq_money</span></span>
* <span data-ttu-id="73d4f-288">capital_run_length_longest</span><span class="sxs-lookup"><span data-stu-id="73d4f-288">capital_run_length_longest</span></span>
* <span data-ttu-id="73d4f-289">word_freq_business</span><span class="sxs-lookup"><span data-stu-id="73d4f-289">word_freq_business</span></span>
* <span data-ttu-id="73d4f-290">ongewenste e-mail</span><span class="sxs-lookup"><span data-stu-id="73d4f-290">spam</span></span>

<span data-ttu-id="73d4f-291">Vervolgens gaat u terug toohello **Cluster** Kies **KMeans**, en set Hallo *aantal clusters* too4.</span><span class="sxs-lookup"><span data-stu-id="73d4f-291">Then go back toohello **Cluster** tab, choose **KMeans**, and set hello *Number of clusters* too4.</span></span> <span data-ttu-id="73d4f-292">Vervolgens **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="73d4f-292">Then **Execute**.</span></span> <span data-ttu-id="73d4f-293">Hallo resultaten worden weergegeven in het uitvoervenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="73d4f-293">hello results are displayed in hello output window.</span></span> <span data-ttu-id="73d4f-294">Een cluster met hoge frequentie van 'george' en 'hp' heeft en is waarschijnlijk een legitieme zakelijke-e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="73d4f-294">One cluster has high frequency of "george" and "hp" and is probably a legitimate business email.</span></span>

<span data-ttu-id="73d4f-295">een eenvoudige decision tree machine learning-model toobuild:</span><span class="sxs-lookup"><span data-stu-id="73d4f-295">toobuild a simple decision tree machine learning model:</span></span>

* <span data-ttu-id="73d4f-296">Selecteer Hallo **Model** tabblad</span><span class="sxs-lookup"><span data-stu-id="73d4f-296">Select hello **Model** tab,</span></span>
* <span data-ttu-id="73d4f-297">Kies **structuur** als Hallo **Type**.</span><span class="sxs-lookup"><span data-stu-id="73d4f-297">Choose **Tree** as hello **Type**.</span></span>
* <span data-ttu-id="73d4f-298">Selecteer **Execute** toodisplay Hallo structuur in tekstvorm in Hallo venster uitvoer.</span><span class="sxs-lookup"><span data-stu-id="73d4f-298">Select **Execute** toodisplay hello tree in text form in hello output window.</span></span>
* <span data-ttu-id="73d4f-299">Selecteer Hallo **tekenen** knop tooview een grafische versie.</span><span class="sxs-lookup"><span data-stu-id="73d4f-299">Select hello **Draw** button tooview a graphical version.</span></span> <span data-ttu-id="73d4f-300">Dit lijkt vergelijkbaar toohello structuur we verkregen eerder met behulp van *rpart*.</span><span class="sxs-lookup"><span data-stu-id="73d4f-300">This looks quite similar toohello tree we obtained earlier using *rpart*.</span></span>

<span data-ttu-id="73d4f-301">Een van de Hallo nice functies van Rammelaar is de mogelijkheid toorun enkele machine learning-methoden en ze snel te evalueren.</span><span class="sxs-lookup"><span data-stu-id="73d4f-301">One of hello nice features of Rattle is its ability toorun several machine learning methods and quickly evaluate them.</span></span> <span data-ttu-id="73d4f-302">Hier volgt Hallo procedure:</span><span class="sxs-lookup"><span data-stu-id="73d4f-302">Here is hello procedure:</span></span>

* <span data-ttu-id="73d4f-303">Kies **alle** voor Hallo **Type**.</span><span class="sxs-lookup"><span data-stu-id="73d4f-303">Choose **All** for hello **Type**.</span></span>
* <span data-ttu-id="73d4f-304">Selecteer **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="73d4f-304">Select **Execute**.</span></span>
* <span data-ttu-id="73d4f-305">Na voltooiing klikt u op enkel **Type**, bijvoorbeeld **SVM**, en Hallo resultaten te bekijken.</span><span class="sxs-lookup"><span data-stu-id="73d4f-305">After it finishes you can click any single **Type**, like **SVM**, and view hello results.</span></span>
* <span data-ttu-id="73d4f-306">U kunt ook Hallo prestaties van modellen op Hallo validatie ingesteld met Hallo Hallo vergelijken **Evaluate** tabblad. Bijvoorbeeld, Hallo **fout Matrix** selectie ziet u Hallo verwarring matrix, algemene fout en gemiddelde klasse fout voor elk model op Hallo validatie set.</span><span class="sxs-lookup"><span data-stu-id="73d4f-306">You can also compare hello performance of hello models on hello validation set using hello **Evaluate** tab. For example, hello **Error Matrix** selection shows you hello confusion matrix, overall error, and averaged class error for each model on hello validation set.</span></span>
* <span data-ttu-id="73d4f-307">U kunt ook tekenen ROC-curve, analyse van de gevoeligheid en andere soorten model evaluaties doen.</span><span class="sxs-lookup"><span data-stu-id="73d4f-307">You can also plot ROC curves, perform sensitivity analysis, and do other types of model evaluations.</span></span>

<span data-ttu-id="73d4f-308">Wanneer u klaar bent voor het bouwen van modellen, selecteren Hallo **logboek** tabblad tooview Hallo R code uitvoeren met Rammelaar tijdens uw sessie.</span><span class="sxs-lookup"><span data-stu-id="73d4f-308">Once you're finished building models, select hello **Log** tab tooview hello R code run by Rattle during your session.</span></span> <span data-ttu-id="73d4f-309">U kunt selecteren Hallo **exporteren** knop toosave deze.</span><span class="sxs-lookup"><span data-stu-id="73d4f-309">You can select hello **Export** button toosave it.</span></span>

> [!NOTE]
> <span data-ttu-id="73d4f-310">Er is een fout in de huidige release van Rammelaar.</span><span class="sxs-lookup"><span data-stu-id="73d4f-310">There is a bug in current release of Rattle.</span></span> <span data-ttu-id="73d4f-311">toomodify Hallo script of gebruik het toorepeat stappen van de hoger, moet u een teken # vóór * exporteren... dit logboek * in de tekst hello van Hallo logboek.</span><span class="sxs-lookup"><span data-stu-id="73d4f-311">toomodify hello script or use it toorepeat your steps later, you must insert a # character in front of *Export this log ... * in hello text of hello log.</span></span>
>
>

## <a name="postgresql--squirrel-sql"></a><span data-ttu-id="73d4f-312">PostgreSQL & Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="73d4f-312">PostgreSQL & Squirrel SQL</span></span>
<span data-ttu-id="73d4f-313">Hallo DSVM wordt geleverd met PostgreSQL geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="73d4f-313">hello DSVM comes with PostgreSQL installed.</span></span> <span data-ttu-id="73d4f-314">PostgreSQL is een geavanceerde, open-source relationele database.</span><span class="sxs-lookup"><span data-stu-id="73d4f-314">PostgreSQL is a sophisticated, open-source relational database.</span></span> <span data-ttu-id="73d4f-315">Deze sectie wordt beschreven hoe tooload onze gegevensset in PostgreSQL spam en deze vervolgens een query.</span><span class="sxs-lookup"><span data-stu-id="73d4f-315">This section shows how tooload our spam dataset into PostgreSQL and then query it.</span></span>

<span data-ttu-id="73d4f-316">Voordat u Hallo gegevens laden kunt, moet u tooallow wachtwoordverificatie van Hallo localhost.</span><span class="sxs-lookup"><span data-stu-id="73d4f-316">Before you can load hello data, you need tooallow password authentication from hello localhost.</span></span> <span data-ttu-id="73d4f-317">Bij een opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="73d4f-317">At a command prompt:</span></span>

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

<span data-ttu-id="73d4f-318">Aan de onderkant Hallo van configuratiebestand Hallo zijn verschillende regels die in details Hallo verbindingen toegestaan:</span><span class="sxs-lookup"><span data-stu-id="73d4f-318">Near hello bottom of hello config file are several lines that detail hello allowed connections:</span></span>

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

<span data-ttu-id="73d4f-319">Wijzig Hallo 'IPv4 lokale verbindingen' regel toouse md5 in plaats van ident, zodat we kunt aanmelden met een gebruikersnaam en wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="73d4f-319">Change hello "IPv4 local connections" line toouse md5 instead of ident, so we can log in using a username and password:</span></span>

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

<span data-ttu-id="73d4f-320">En Hallo postgres service opnieuw starten:</span><span class="sxs-lookup"><span data-stu-id="73d4f-320">And restart hello postgres service:</span></span>

    sudo systemctl restart postgresql

<span data-ttu-id="73d4f-321">toolaunch psql, een interactief terminal voor PostgreSQL als gebruiker met ingebouwde postgres Hallo Voer Hallo volgende opdracht vanaf een opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="73d4f-321">toolaunch psql, an interactive terminal for PostgreSQL, as hello built-in postgres user, run hello following command from a prompt:</span></span>

    sudo -u postgres psql

<span data-ttu-id="73d4f-322">Een nieuw gebruikersaccount maken, met behulp van dezelfde gebruikersnaam Hallo als u momenteel bent aangemeld als account voor Linux Hallo en wijs hieraan een wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="73d4f-322">Create a new user account, using hello same username as hello Linux account you're currently logged in as, and give it a password:</span></span>

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

<span data-ttu-id="73d4f-323">Meld u vervolgens in toopsql als uw gebruikers:</span><span class="sxs-lookup"><span data-stu-id="73d4f-323">Then log in toopsql as your user:</span></span>

    psql

<span data-ttu-id="73d4f-324">En Hallo gegevens importeren in een nieuwe database:</span><span class="sxs-lookup"><span data-stu-id="73d4f-324">And import hello data into a new database:</span></span>

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

<span data-ttu-id="73d4f-325">Nu gaan we Hallo gegevens verkennen en uitvoeren van sommige query's met behulp van **Squirrel SQL**, een grafisch hulpprogramma waarmee u communiceren met databases via een JDBC-stuurprogramma.</span><span class="sxs-lookup"><span data-stu-id="73d4f-325">Now, let's explore hello data and run some queries using **Squirrel SQL**, a graphical tool that lets you interact with databases via a JDBC driver.</span></span>

<span data-ttu-id="73d4f-326">tooget gestart, start SQL Squirrel in Hallo toepassingen menu.</span><span class="sxs-lookup"><span data-stu-id="73d4f-326">tooget started, launch Squirrel SQL from hello Applications menu.</span></span> <span data-ttu-id="73d4f-327">tooset van Hallo stuurprogramma:</span><span class="sxs-lookup"><span data-stu-id="73d4f-327">tooset up hello driver:</span></span>

* <span data-ttu-id="73d4f-328">Selecteer **Windows**, klikt u vervolgens **stuurprogramma's weergeven**.</span><span class="sxs-lookup"><span data-stu-id="73d4f-328">Select **Windows**, then **View Drivers**.</span></span>
* <span data-ttu-id="73d4f-329">Met de rechtermuisknop op **PostgreSQL** en selecteer **stuurprogramma wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="73d4f-329">Right-click on **PostgreSQL** and select **Modify Driver**.</span></span>
* <span data-ttu-id="73d4f-330">Selecteer **Extra klasse pad**, klikt u vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="73d4f-330">Select **Extra Class Path**, then **Add**.</span></span>
* <span data-ttu-id="73d4f-331">Voer ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** voor Hallo **bestandsnaam** en</span><span class="sxs-lookup"><span data-stu-id="73d4f-331">Enter ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** for hello **File Name** and</span></span>
* <span data-ttu-id="73d4f-332">Selecteer **Open**.</span><span class="sxs-lookup"><span data-stu-id="73d4f-332">Select **Open**.</span></span>
* <span data-ttu-id="73d4f-333">Lijst met stuurprogramma's kiezen en selecteer vervolgens **org.postgresql.Driver** in **klassenaam**, en selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="73d4f-333">Choose List Drivers, then select **org.postgresql.Driver** in **Class Name**, and select **OK**.</span></span>

<span data-ttu-id="73d4f-334">tooset hello verbinding toohello lokale server:</span><span class="sxs-lookup"><span data-stu-id="73d4f-334">tooset up hello connection toohello local server:</span></span>

* <span data-ttu-id="73d4f-335">Selecteer **Windows**, klikt u vervolgens **aliassen weergeven.**</span><span class="sxs-lookup"><span data-stu-id="73d4f-335">Select **Windows**, then **View Aliases.**</span></span>
* <span data-ttu-id="73d4f-336">Kies Hallo  **+**  toomake knop een nieuwe alias.</span><span class="sxs-lookup"><span data-stu-id="73d4f-336">Choose hello **+** button toomake a new alias.</span></span>
* <span data-ttu-id="73d4f-337">Naam *Spam database*, kies **PostgreSQL** in Hallo **stuurprogramma** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="73d4f-337">Name it *Spam database*, choose **PostgreSQL** in hello **Driver** drop-down.</span></span>
* <span data-ttu-id="73d4f-338">Hallo-URL te instellen*jdbc:postgresql://localhost/spam*.</span><span class="sxs-lookup"><span data-stu-id="73d4f-338">Set hello URL too*jdbc:postgresql://localhost/spam*.</span></span>
* <span data-ttu-id="73d4f-339">Voer uw *gebruikersnaam* en *wachtwoord*.</span><span class="sxs-lookup"><span data-stu-id="73d4f-339">Enter your *username* and *password*.</span></span>
* <span data-ttu-id="73d4f-340">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="73d4f-340">Click **OK**.</span></span>
* <span data-ttu-id="73d4f-341">Hallo tooopen **verbinding** venster, dubbelklikt u op Hallo ***Spam database*** alias.</span><span class="sxs-lookup"><span data-stu-id="73d4f-341">tooopen hello **Connection** window, double-click hello ***Spam database*** alias.</span></span>
* <span data-ttu-id="73d4f-342">Selecteer **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="73d4f-342">Select **Connect**.</span></span>

<span data-ttu-id="73d4f-343">toorun sommige query's:</span><span class="sxs-lookup"><span data-stu-id="73d4f-343">toorun some queries:</span></span>

* <span data-ttu-id="73d4f-344">Selecteer Hallo **SQL** tabblad.</span><span class="sxs-lookup"><span data-stu-id="73d4f-344">Select hello **SQL** tab.</span></span>
* <span data-ttu-id="73d4f-345">Voer een eenvoudige query zoals `SELECT * from data;` in Hallo query tekstvak bovenaan Hallo Hallo SQL tabblad.</span><span class="sxs-lookup"><span data-stu-id="73d4f-345">Enter a simple query such as `SELECT * from data;` in hello query textbox at hello top of hello SQL tab.</span></span>
* <span data-ttu-id="73d4f-346">Druk op **Ctrl + Enter** toorun deze.</span><span class="sxs-lookup"><span data-stu-id="73d4f-346">Press **Ctrl-Enter** toorun it.</span></span> <span data-ttu-id="73d4f-347">Standaard Squirrel SQL Hallo eerste 100 rijen geretourneerd uit uw query.</span><span class="sxs-lookup"><span data-stu-id="73d4f-347">By default Squirrel SQL returns hello first 100 rows from your query.</span></span>

<span data-ttu-id="73d4f-348">Er zijn veel meer query's die u tooexplore deze gegevens kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="73d4f-348">There are many more queries you could run tooexplore this data.</span></span> <span data-ttu-id="73d4f-349">Hoe werkt bijvoorbeeld Hallo frequentie van Hallo word *maken* verschillen tussen spam en ham?</span><span class="sxs-lookup"><span data-stu-id="73d4f-349">For example, how does hello frequency of hello word *make* differ between spam and ham?</span></span>

    SELECT avg(word_freq_make), spam from data group by spam;

<span data-ttu-id="73d4f-350">Of wat Hallo kenmerken van e-mailbericht dat vaak bevatten *3d*?</span><span class="sxs-lookup"><span data-stu-id="73d4f-350">Or what are hello characteristics of email that frequently contain *3d*?</span></span>

    SELECT * from data order by word_freq_3d desc;

<span data-ttu-id="73d4f-351">De meeste e-mailberichten waarvoor een hoge exemplaar van *3d* zijn blijkbaar spam, zodat het mogelijk een handige functie voor het bouwen van een Voorspellend model tooclassify Hallo e-mailberichten.</span><span class="sxs-lookup"><span data-stu-id="73d4f-351">Most emails that have a high occurrence of *3d* are apparently spam, so it could be a useful feature for building a predictive model tooclassify hello emails.</span></span>

<span data-ttu-id="73d4f-352">Indien u tooperform machine learning met gegevens die zijn opgeslagen in een PostgreSQL-database wenste, kunt u overwegen [MADlib](http://madlib.incubator.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="73d4f-352">If you wanted tooperform machine learning with data stored in a PostgreSQL database, consider using [MADlib](http://madlib.incubator.apache.org/).</span></span>

## <a name="sql-server-data-warehouse"></a><span data-ttu-id="73d4f-353">SQL Server-datawarehouse</span><span class="sxs-lookup"><span data-stu-id="73d4f-353">SQL Server Data Warehouse</span></span>
<span data-ttu-id="73d4f-354">Azure SQL Data Warehouse is een schaalbare clouddatabase die geschikt is voor het verwerken van grote hoeveelheden relationele en/of niet-relationele gegevens.</span><span class="sxs-lookup"><span data-stu-id="73d4f-354">Azure SQL Data Warehouse is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span> <span data-ttu-id="73d4f-355">Zie voor meer informatie [wat is Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="73d4f-355">For more information, see [What is Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span></span>

<span data-ttu-id="73d4f-356">tooconnect toohello datawarehouse op en Hallo tabel maken uitvoeren Hallo volgende opdracht uit vanaf een opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="73d4f-356">tooconnect toohello data warehouse and create hello table, run hello following command from a command prompt:</span></span>

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

<span data-ttu-id="73d4f-357">Klik op Hallo sqlcmd-opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="73d4f-357">Then at hello sqlcmd prompt:</span></span>

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

<span data-ttu-id="73d4f-358">Gegevens kopiëren met bcp:</span><span class="sxs-lookup"><span data-stu-id="73d4f-358">Copy data with bcp:</span></span>

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> <span data-ttu-id="73d4f-359">Hallo regeleinden in het gedownloade bestand Hallo zijn Windows-stijl, maar bcp verwacht UNIX-stijl, dus we er tootell bcp dat met moeten - r-vlag Hallo.</span><span class="sxs-lookup"><span data-stu-id="73d4f-359">hello line endings in hello downloaded file are Windows-style, but bcp expects UNIX-style, so we need tootell bcp that with hello -r flag.</span></span>
>
>

<span data-ttu-id="73d4f-360">En de query met sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="73d4f-360">And query with sqlcmd:</span></span>

    select top 10 spam, char_freq_dollar from spam;
    GO

<span data-ttu-id="73d4f-361">U kunt ook een query met Squirrel SQL.</span><span class="sxs-lookup"><span data-stu-id="73d4f-361">You could also query with Squirrel SQL.</span></span> <span data-ttu-id="73d4f-362">Uitvoeren van gelijksoortige stappen voor PostgreSQL, met behulp van Hallo Microsoft MSSQL Server JDBC-stuurprogramma, die kan worden gevonden in ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span><span class="sxs-lookup"><span data-stu-id="73d4f-362">Follow similar steps for PostgreSQL, using hello Microsoft MSSQL Server JDBC Driver, which can be found in ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73d4f-363">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="73d4f-363">Next steps</span></span>
<span data-ttu-id="73d4f-364">Zie voor een overzicht van onderwerpen die helpt u bij het Hallo-taken die Hallo Gegevenswetenschap proces in Azure omvatten, [Team gegevens wetenschap proces](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="73d4f-364">For an overview of topics that walk you through hello tasks that comprise hello Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="73d4f-365">Zie voor een beschrijving van andere scenario's voor end-to-end die laten Hallo stappen in Hallo Team gegevens wetenschappelijke processen voor specifieke scenario's zien [Team gegevens wetenschap proces scenario's](data-science-process-walkthroughs.md).</span><span class="sxs-lookup"><span data-stu-id="73d4f-365">For a description of other end-to-end walkthroughs that demonstrate hello steps in hello Team Data Science Process for specific scenarios, see [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md).</span></span> <span data-ttu-id="73d4f-366">Hallo-scenario's ook laten zien hoe toocombine cloud en on-premises hulpprogramma's en services in een werkstroom of pijplijn toocreate een intelligente toepassing.</span><span class="sxs-lookup"><span data-stu-id="73d4f-366">hello walkthroughs also illustrate how toocombine cloud and on-premises tools and services into a workflow or pipeline toocreate an intelligent application.</span></span>
