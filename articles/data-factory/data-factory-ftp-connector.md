---
title: aaaMove gegevens van een FTP-server met behulp van Azure Data Factory | Microsoft Docs
description: Meer informatie over het toomove gegevens van een FTP-server met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: eea3bab0-a6e4-4045-ad44-9ce06229c718
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jingwang
ms.openlocfilehash: c707e29532b2a8a870603948cb6150ab857bd6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a><span data-ttu-id="4a02d-103">Gegevens verplaatsen van een FTP-server met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="4a02d-103">Move data from an FTP server by using Azure Data Factory</span></span>
<span data-ttu-id="4a02d-104">Dit artikel wordt uitgelegd hoe toouse hello kopieeractiviteit in Azure Data Factory toomove gegevens van een FTP-server.</span><span class="sxs-lookup"><span data-stu-id="4a02d-104">This article explains how toouse hello copy activity in Azure Data Factory toomove data from an FTP server.</span></span> <span data-ttu-id="4a02d-105">Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.</span><span class="sxs-lookup"><span data-stu-id="4a02d-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="4a02d-106">U kunt gegevens kopiëren van een FTP-server tooany ondersteund sink-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="4a02d-106">You can copy data from an FTP server tooany supported sink data store.</span></span> <span data-ttu-id="4a02d-107">Zie voor een lijst van gegevens winkels ondersteund zoals sinks door kopieeractiviteit hello, Hallo [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="4a02d-107">For a list of data stores supported as sinks by hello copy activity, see hello [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="4a02d-108">Data Factory ondersteunt momenteel alleen zwevend gegevens van een FTP-server tooother gegevens worden opgeslagen, maar niet verplaatsen van gegevens van andere gegevens worden opgeslagen tooan FTP-server.</span><span class="sxs-lookup"><span data-stu-id="4a02d-108">Data Factory currently supports only moving data from an FTP server tooother data stores, but not moving data from other data stores tooan FTP server.</span></span> <span data-ttu-id="4a02d-109">Deze ondersteuning biedt voor zowel on-premises en in de cloud van de FTP-servers.</span><span class="sxs-lookup"><span data-stu-id="4a02d-109">It supports both on-premises and cloud FTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="4a02d-110">Hallo kopieeractiviteit verwijdert Hallo-bronbestand niet nadat het is gekopieerde toohello bestemming.</span><span class="sxs-lookup"><span data-stu-id="4a02d-110">hello copy activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="4a02d-111">Als u toodelete Hallo-bronbestand na een geslaagde kopie moet, maakt u een aangepaste activiteit toodelete Hallo-bestand en Hallo activiteit in de pijplijn hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4a02d-111">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file, and use hello activity in hello pipeline.</span></span> 

## <a name="enable-connectivity"></a><span data-ttu-id="4a02d-112">Connectiviteit inschakelen</span><span class="sxs-lookup"><span data-stu-id="4a02d-112">Enable connectivity</span></span>
<span data-ttu-id="4a02d-113">Als u overstapt gegevens uit een **lokale** FTP-server tooa cloud-gegevensarchief (bijvoorbeeld tooAzure Blob-opslag), installeren en gebruiken van Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="4a02d-113">If you are moving data from an **on-premises** FTP server tooa cloud data store (for example, tooAzure Blob storage), install and use Data Management Gateway.</span></span> <span data-ttu-id="4a02d-114">Hallo Data Management Gateway is een clientagent die op uw on-premises machine is geïnstalleerd en kunt u cloud services tooconnect tooan lokale resource.</span><span class="sxs-lookup"><span data-stu-id="4a02d-114">hello Data Management Gateway is a client agent that is installed on your on-premises machine, and it allows cloud services tooconnect tooan on-premises resource.</span></span> <span data-ttu-id="4a02d-115">Zie voor meer informatie [Data Management Gateway](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="4a02d-115">For details, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="4a02d-116">Zie voor stapsgewijze instructies voor het Hallo-gateway instellen en gebruiken deze [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="4a02d-116">For step-by-step instructions on setting up hello gateway and using it, see [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="4a02d-117">U Hallo gateway tooconnect tooan FTP-server, zelfs als het Hallo-server zich op een Azure-infrastructuur als een dienst (IaaS) virtuele machine (VM).</span><span class="sxs-lookup"><span data-stu-id="4a02d-117">You use hello gateway tooconnect tooan FTP server, even if hello server is on an Azure infrastructure as a service (IaaS) virtual machine (VM).</span></span>

<span data-ttu-id="4a02d-118">Het is mogelijk tooinstall Hallo gateway op Hallo dezelfde lokale machine of IaaS VM zoals Hallo FTP-server.</span><span class="sxs-lookup"><span data-stu-id="4a02d-118">It is possible tooinstall hello gateway on hello same on-premises machine or IaaS VM as hello FTP server.</span></span> <span data-ttu-id="4a02d-119">We raden echter aan dat u Hallo-gateway op een afzonderlijke computer of op IaaS VM tooavoid bronconflicten en voor betere prestaties installeert.</span><span class="sxs-lookup"><span data-stu-id="4a02d-119">However, we recommend that you install hello gateway on a separate machine or IaaS VM tooavoid resource contention, and for better performance.</span></span> <span data-ttu-id="4a02d-120">Wanneer u Hallo-gateway op een afzonderlijke computer installeert, is het Hallo-machine moeten kunnen tooaccess Hallo FTP-server.</span><span class="sxs-lookup"><span data-stu-id="4a02d-120">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello FTP server.</span></span>

## <a name="get-started"></a><span data-ttu-id="4a02d-121">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="4a02d-121">Get started</span></span>
<span data-ttu-id="4a02d-122">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens van een FTP-bron verplaatst met behulp van verschillende hulpprogramma's of API's.</span><span class="sxs-lookup"><span data-stu-id="4a02d-122">You can create a pipeline with a copy activity that moves data from an FTP source by using different tools or APIs.</span></span>

<span data-ttu-id="4a02d-123">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Data Factory-Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="4a02d-123">hello easiest way toocreate a pipeline is toouse hello **Data Factory Copy Wizard**.</span></span> <span data-ttu-id="4a02d-124">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht.</span><span class="sxs-lookup"><span data-stu-id="4a02d-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough.</span></span>

<span data-ttu-id="4a02d-125">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager-sjabloon**, **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="4a02d-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="4a02d-126">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="4a02d-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="4a02d-127">Of u Hallo-hulpprogramma's of API's gebruiken, voert u hello te volgen stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan:</span><span class="sxs-lookup"><span data-stu-id="4a02d-127">Whether you use hello tools or APIs, perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="4a02d-128">Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="4a02d-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="4a02d-129">Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="4a02d-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="4a02d-130">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="4a02d-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="4a02d-131">Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4a02d-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="4a02d-132">Wanneer u hulpprogramma's of API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="4a02d-132">When you use tools or APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="4a02d-133">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van een FTP-gegevensarchief zijn Hallo [JSON-voorbeeld: gegevens kopiëren van FTP-server tooAzure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="4a02d-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an FTP data store, see hello [JSON example: Copy data from FTP server tooAzure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="4a02d-134">Zie voor meer informatie over ondersteunde bestands- en compressie indelingen toouse [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="4a02d-134">For details about supported file and compression formats toouse, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="4a02d-135">Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooFTP zijn.</span><span class="sxs-lookup"><span data-stu-id="4a02d-135">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooFTP.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="4a02d-136">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="4a02d-136">Linked service properties</span></span>
<span data-ttu-id="4a02d-137">Hallo volgende tabel beschrijft de JSON-elementen specifieke tooan gekoppeld FTP-service.</span><span class="sxs-lookup"><span data-stu-id="4a02d-137">hello following table describes JSON elements specific tooan FTP linked service.</span></span>

| <span data-ttu-id="4a02d-138">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4a02d-138">Property</span></span> | <span data-ttu-id="4a02d-139">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4a02d-139">Description</span></span> | <span data-ttu-id="4a02d-140">Vereist</span><span class="sxs-lookup"><span data-stu-id="4a02d-140">Required</span></span> | <span data-ttu-id="4a02d-141">Standaard</span><span class="sxs-lookup"><span data-stu-id="4a02d-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4a02d-142">type</span><span class="sxs-lookup"><span data-stu-id="4a02d-142">type</span></span> |<span data-ttu-id="4a02d-143">Deze tooFtpServer ingesteld.</span><span class="sxs-lookup"><span data-stu-id="4a02d-143">Set this tooFtpServer.</span></span> |<span data-ttu-id="4a02d-144">Ja</span><span class="sxs-lookup"><span data-stu-id="4a02d-144">Yes</span></span> |&nbsp; |
| <span data-ttu-id="4a02d-145">host</span><span class="sxs-lookup"><span data-stu-id="4a02d-145">host</span></span> |<span data-ttu-id="4a02d-146">Hallo-naam of IP-adres van Hallo FTP-server opgeven.</span><span class="sxs-lookup"><span data-stu-id="4a02d-146">Specify hello name or IP address of hello FTP server.</span></span> |<span data-ttu-id="4a02d-147">Ja</span><span class="sxs-lookup"><span data-stu-id="4a02d-147">Yes</span></span> |&nbsp; |
| <span data-ttu-id="4a02d-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="4a02d-148">authenticationType</span></span> |<span data-ttu-id="4a02d-149">Hallo verificatietype opgeven.</span><span class="sxs-lookup"><span data-stu-id="4a02d-149">Specify hello authentication type.</span></span> |<span data-ttu-id="4a02d-150">Ja</span><span class="sxs-lookup"><span data-stu-id="4a02d-150">Yes</span></span> |<span data-ttu-id="4a02d-151">Basic, anonieme</span><span class="sxs-lookup"><span data-stu-id="4a02d-151">Basic, Anonymous</span></span> |
| <span data-ttu-id="4a02d-152">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="4a02d-152">username</span></span> |<span data-ttu-id="4a02d-153">Hallo-gebruiker met toegang toohello FTP-server opgeven.</span><span class="sxs-lookup"><span data-stu-id="4a02d-153">Specify hello user who has access toohello FTP server.</span></span> |<span data-ttu-id="4a02d-154">Nee</span><span class="sxs-lookup"><span data-stu-id="4a02d-154">No</span></span> |&nbsp; |
| <span data-ttu-id="4a02d-155">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="4a02d-155">password</span></span> |<span data-ttu-id="4a02d-156">Hallo-wachtwoord voor gebruiker hello (gebruikersnaam) opgeven.</span><span class="sxs-lookup"><span data-stu-id="4a02d-156">Specify hello password for hello user (username).</span></span> |<span data-ttu-id="4a02d-157">Nee</span><span class="sxs-lookup"><span data-stu-id="4a02d-157">No</span></span> |&nbsp; |
| <span data-ttu-id="4a02d-158">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="4a02d-158">encryptedCredential</span></span> |<span data-ttu-id="4a02d-159">Hallo versleutelde referentie tooaccess Hallo FTP-server opgeven.</span><span class="sxs-lookup"><span data-stu-id="4a02d-159">Specify hello encrypted credential tooaccess hello FTP server.</span></span> |<span data-ttu-id="4a02d-160">Nee</span><span class="sxs-lookup"><span data-stu-id="4a02d-160">No</span></span> |&nbsp; |
| <span data-ttu-id="4a02d-161">gatewayName</span><span class="sxs-lookup"><span data-stu-id="4a02d-161">gatewayName</span></span> |<span data-ttu-id="4a02d-162">Hallo naam opgeven van Hallo gateway in Data Management Gateway tooconnect tooan lokale FTP-server.</span><span class="sxs-lookup"><span data-stu-id="4a02d-162">Specify hello name of hello gateway in Data Management Gateway tooconnect tooan on-premises FTP server.</span></span> |<span data-ttu-id="4a02d-163">Nee</span><span class="sxs-lookup"><span data-stu-id="4a02d-163">No</span></span> |&nbsp; |
| <span data-ttu-id="4a02d-164">poort</span><span class="sxs-lookup"><span data-stu-id="4a02d-164">port</span></span> |<span data-ttu-id="4a02d-165">Geef op welke Hallo FTP-server luistert Hallo-poort.</span><span class="sxs-lookup"><span data-stu-id="4a02d-165">Specify hello port on which hello FTP server is listening.</span></span> |<span data-ttu-id="4a02d-166">Nee</span><span class="sxs-lookup"><span data-stu-id="4a02d-166">No</span></span> |<span data-ttu-id="4a02d-167">21</span><span class="sxs-lookup"><span data-stu-id="4a02d-167">21</span></span> |
| <span data-ttu-id="4a02d-168">enableSsl</span><span class="sxs-lookup"><span data-stu-id="4a02d-168">enableSsl</span></span> |<span data-ttu-id="4a02d-169">Geef op of toouse FTP via een SSL/TLS-kanaal.</span><span class="sxs-lookup"><span data-stu-id="4a02d-169">Specify whether toouse FTP over an SSL/TLS channel.</span></span> |<span data-ttu-id="4a02d-170">Nee</span><span class="sxs-lookup"><span data-stu-id="4a02d-170">No</span></span> |<span data-ttu-id="4a02d-171">De waarde True</span><span class="sxs-lookup"><span data-stu-id="4a02d-171">true</span></span> |
| <span data-ttu-id="4a02d-172">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="4a02d-172">enableServerCertificateValidation</span></span> |<span data-ttu-id="4a02d-173">Geef op of tooenable server SSL certificaatcontrole wanneer u FTP via SSL/TLS-kanaal.</span><span class="sxs-lookup"><span data-stu-id="4a02d-173">Specify whether tooenable server SSL certificate validation when you are using FTP over SSL/TLS channel.</span></span> |<span data-ttu-id="4a02d-174">Nee</span><span class="sxs-lookup"><span data-stu-id="4a02d-174">No</span></span> |<span data-ttu-id="4a02d-175">De waarde True</span><span class="sxs-lookup"><span data-stu-id="4a02d-175">true</span></span> |

### <a name="use-anonymous-authentication"></a><span data-ttu-id="4a02d-176">Gebruik anonieme verificatie</span><span class="sxs-lookup"><span data-stu-id="4a02d-176">Use Anonymous authentication</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {        
            "authenticationType": "Anonymous",
              "host": "myftpserver.com"
        }
    }
}
```

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="4a02d-177">Gebruik van gebruikersnaam en wachtwoord voor basisverificatie in tekst zonder opmaak</span><span class="sxs-lookup"><span data-stu-id="4a02d-177">Use username and password in plain text for basic authentication</span></span>

```JSON
{
    "name": "FTPLinkedService",
      "properties": {
    "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
      }
}
```

### <a name="use-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="4a02d-178">Gebruik poort, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="4a02d-178">Use port, enableSsl, enableServerCertificateValidation</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="4a02d-179">EncryptedCredential gebruiken voor verificatie en gateway</span><span class="sxs-lookup"><span data-stu-id="4a02d-179">Use encryptedCredential for authentication and gateway</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "mygateway"
        }
      }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="4a02d-180">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="4a02d-180">Dataset properties</span></span>
<span data-ttu-id="4a02d-181">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets [gegevenssets maken](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="4a02d-181">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="4a02d-182">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle typen van de gegevensset.</span><span class="sxs-lookup"><span data-stu-id="4a02d-182">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="4a02d-183">Hallo **typeProperties** sectie verschilt voor elk type dataset.</span><span class="sxs-lookup"><span data-stu-id="4a02d-183">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="4a02d-184">Het levert informatie die specifieke toohello gegevensset type.</span><span class="sxs-lookup"><span data-stu-id="4a02d-184">It provides information that is specific toohello dataset type.</span></span> <span data-ttu-id="4a02d-185">Hallo **typeProperties** sectie voor een gegevensset van het type **FileShare** heeft Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="4a02d-185">hello **typeProperties** section for a dataset of type **FileShare** has hello following properties:</span></span>

| <span data-ttu-id="4a02d-186">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4a02d-186">Property</span></span> | <span data-ttu-id="4a02d-187">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4a02d-187">Description</span></span> | <span data-ttu-id="4a02d-188">Vereist</span><span class="sxs-lookup"><span data-stu-id="4a02d-188">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4a02d-189">folderPath</span><span class="sxs-lookup"><span data-stu-id="4a02d-189">folderPath</span></span> |<span data-ttu-id="4a02d-190">Subpad toohello map.</span><span class="sxs-lookup"><span data-stu-id="4a02d-190">Subpath toohello folder.</span></span> <span data-ttu-id="4a02d-191">Gebruik van escape-teken ' \ ' voor speciale tekens in Hallo-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="4a02d-191">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="4a02d-192">Zie [voorbeeld gekoppelde service en gegevensset definities](#sample-linked-service-and-dataset-definitions) voor voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="4a02d-192">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="4a02d-193">U kunt deze eigenschap combineren met **partitionBy** toohave mappaden op basis van het segment beginnen en eindigen datums en tijden.</span><span class="sxs-lookup"><span data-stu-id="4a02d-193">You can combine this property with **partitionBy** toohave folder paths based on slice start and end date-times.</span></span> |<span data-ttu-id="4a02d-194">Ja</span><span class="sxs-lookup"><span data-stu-id="4a02d-194">Yes</span></span> |
| <span data-ttu-id="4a02d-195">fileName</span><span class="sxs-lookup"><span data-stu-id="4a02d-195">fileName</span></span> |<span data-ttu-id="4a02d-196">Hallo-naam van Hallo-bestand opgeven in Hallo **folderPath** als u wilt dat Hallo tabel toorefer tooa specifiek bestand in map Hallo.</span><span class="sxs-lookup"><span data-stu-id="4a02d-196">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="4a02d-197">Als u geen waarde voor deze eigenschap niet opgeeft, wijst Hallo tabel tooall bestanden in de map Hallo.</span><span class="sxs-lookup"><span data-stu-id="4a02d-197">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="4a02d-198">Wanneer **fileName** is niet opgegeven voor een uitvoergegevensset Hallo-naam van Hallo gegenereerd bestand is in de volgende indeling Hallo:</span><span class="sxs-lookup"><span data-stu-id="4a02d-198">When **fileName** is not specified for an output dataset, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="4a02d-199">Gegevens. <Guid>.txt (voorbeeld: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="4a02d-199">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="4a02d-200">Nee</span><span class="sxs-lookup"><span data-stu-id="4a02d-200">No</span></span> |
| <span data-ttu-id="4a02d-201">fileFilter</span><span class="sxs-lookup"><span data-stu-id="4a02d-201">fileFilter</span></span> |<span data-ttu-id="4a02d-202">Geef een filter toobe gebruikt tooselect een subset van de bestanden in Hallo **folderPath**, in plaats van alle bestanden.</span><span class="sxs-lookup"><span data-stu-id="4a02d-202">Specify a filter toobe used tooselect a subset of files in hello **folderPath**, rather than all files.</span></span><br/><br/><span data-ttu-id="4a02d-203">Toegestane waarden zijn: `*` (meerdere tekens) en `?` (willekeurig teken).</span><span class="sxs-lookup"><span data-stu-id="4a02d-203">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="4a02d-204">Voorbeeld 1:`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="4a02d-204">Example 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="4a02d-205">Voorbeeld 2:`"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="4a02d-205">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="4a02d-206">**fileFilter** is van toepassing op een bestandsshare-invoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="4a02d-206">**fileFilter** is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="4a02d-207">Deze eigenschap wordt niet ondersteund met Hadoop Distributed File System (HDFS).</span><span class="sxs-lookup"><span data-stu-id="4a02d-207">This property is not supported with Hadoop Distributed File System (HDFS).</span></span> |<span data-ttu-id="4a02d-208">Nee</span><span class="sxs-lookup"><span data-stu-id="4a02d-208">No</span></span> |
| <span data-ttu-id="4a02d-209">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="4a02d-209">partitionedBy</span></span> |<span data-ttu-id="4a02d-210">Gebruikt een dynamische toospecify **folderPath** en **fileName** voor tijd reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="4a02d-210">Used toospecify a dynamic **folderPath** and **fileName** for time series data.</span></span> <span data-ttu-id="4a02d-211">Bijvoorbeeld, kunt u een **folderPath** met parameters die voor elk uur van gegevens.</span><span class="sxs-lookup"><span data-stu-id="4a02d-211">For example, you can specify a **folderPath** that is parameterized for every hour of data.</span></span> |<span data-ttu-id="4a02d-212">Nee</span><span class="sxs-lookup"><span data-stu-id="4a02d-212">No</span></span> |
| <span data-ttu-id="4a02d-213">Indeling</span><span class="sxs-lookup"><span data-stu-id="4a02d-213">format</span></span> | <span data-ttu-id="4a02d-214">Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="4a02d-214">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="4a02d-215">Set Hallo **type** eigenschap onder indeling tooone van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="4a02d-215">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="4a02d-216">Zie voor meer informatie, Hallo [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren-indeling ](data-factory-supported-file-and-compression-formats.md#parquet-format) secties.</span><span class="sxs-lookup"><span data-stu-id="4a02d-216">For more information, see hello [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="4a02d-217">Als u wilt toocopy bestanden zoals ze tussen winkels op basis van bestanden (binaire kopiëren zijn), moet u Hallo indeling sectie in beide definities invoer en uitvoer gegevensset overslaan.</span><span class="sxs-lookup"><span data-stu-id="4a02d-217">If you want toocopy files as they are between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="4a02d-218">Nee</span><span class="sxs-lookup"><span data-stu-id="4a02d-218">No</span></span> |
| <span data-ttu-id="4a02d-219">Compressie</span><span class="sxs-lookup"><span data-stu-id="4a02d-219">compression</span></span> | <span data-ttu-id="4a02d-220">Hallo-type en compressieniveau voor Hallo gegevens opgeven.</span><span class="sxs-lookup"><span data-stu-id="4a02d-220">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="4a02d-221">Ondersteunde typen zijn **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**, en ondersteunde niveaus zijn **optimale** en **snelst**.</span><span class="sxs-lookup"><span data-stu-id="4a02d-221">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**, and supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="4a02d-222">Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="4a02d-222">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="4a02d-223">Nee</span><span class="sxs-lookup"><span data-stu-id="4a02d-223">No</span></span> |
| <span data-ttu-id="4a02d-224">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="4a02d-224">useBinaryTransfer</span></span> |<span data-ttu-id="4a02d-225">Geef op of overdrachtsmodus toouse Hallo binary.</span><span class="sxs-lookup"><span data-stu-id="4a02d-225">Specify whether toouse hello binary transfer mode.</span></span> <span data-ttu-id="4a02d-226">Hallo-waarden zijn true zijn voor binaire modus (dit is de standaardwaarde Hallo) en false voor ASCII.</span><span class="sxs-lookup"><span data-stu-id="4a02d-226">hello values are true for binary mode (this is hello default value), and false for ASCII.</span></span> <span data-ttu-id="4a02d-227">Deze eigenschap kan alleen worden gebruikt wanneer hello type bijbehorende gekoppelde service type: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="4a02d-227">This property can only be used when hello associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="4a02d-228">Nee</span><span class="sxs-lookup"><span data-stu-id="4a02d-228">No</span></span> |

> [!NOTE]
> <span data-ttu-id="4a02d-229">**Bestandsnaam** en **fileFilter** niet gelijktijdig worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4a02d-229">**fileName** and **fileFilter** cannot be used simultaneously.</span></span>

### <a name="use-hello-partionedby-property"></a><span data-ttu-id="4a02d-230">Hallo partionedBy eigenschap gebruiken</span><span class="sxs-lookup"><span data-stu-id="4a02d-230">Use hello partionedBy property</span></span>
<span data-ttu-id="4a02d-231">Zoals vermeld in de vorige sectie hello, kunt u een dynamische **folderPath** en **fileName** voor tijd reeksgegevens Hello **partitionedBy** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="4a02d-231">As mentioned in hello previous section, you can specify a dynamic **folderPath** and **fileName** for time series data with hello **partitionedBy** property.</span></span>

<span data-ttu-id="4a02d-232">toolearn over tijd reeks gegevenssets, planning en segmenten, Zie [gegevenssets maken](data-factory-create-datasets.md), [planning en uitvoering](data-factory-scheduling-and-execution.md), en [pijplijnen maken](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="4a02d-232">toolearn about time series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="4a02d-233">Voorbeeld 1</span><span class="sxs-lookup"><span data-stu-id="4a02d-233">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="4a02d-234">In dit voorbeeld {segment} is vervangen door de waarde van de Data Factory systeemvariabele SliceStart hello, in Hallo opmaken opgegeven (YYYYMMDDHH).</span><span class="sxs-lookup"><span data-stu-id="4a02d-234">In this example, {Slice} is replaced with hello value of Data Factory system variable SliceStart, in hello format specified (YYYYMMDDHH).</span></span> <span data-ttu-id="4a02d-235">Hallo SliceStart verwijst toostart tijd van Hallo segment.</span><span class="sxs-lookup"><span data-stu-id="4a02d-235">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="4a02d-236">Hallo mappad verschilt voor elk segment.</span><span class="sxs-lookup"><span data-stu-id="4a02d-236">hello folder path is different for each slice.</span></span> <span data-ttu-id="4a02d-237">(Bijvoorbeeld wikidatagateway/wikisampledataout/2014100103 of wikidatagateway/wikisampledataout/2014100104.)</span><span class="sxs-lookup"><span data-stu-id="4a02d-237">(For example, wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.)</span></span>

#### <a name="sample-2"></a><span data-ttu-id="4a02d-238">Voorbeeld 2</span><span class="sxs-lookup"><span data-stu-id="4a02d-238">Sample 2</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
<span data-ttu-id="4a02d-239">In dit voorbeeld Hallo jaar, maand, dag en tijd van de SliceStart worden uitgepakt in verschillende variabelen die worden gebruikt door Hallo **folderPath** en **fileName** eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="4a02d-239">In this example, hello year, month, day, and time of SliceStart are extracted into separate variables that are used by hello **folderPath** and **fileName** properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="4a02d-240">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="4a02d-240">Copy activity properties</span></span>
<span data-ttu-id="4a02d-241">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van activiteiten [pijplijnen maken](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="4a02d-241">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="4a02d-242">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en beleidsregels zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="4a02d-242">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="4a02d-243">Eigenschappen die beschikbaar zijn in Hallo **typeProperties** sectie van de activiteit op Hallo Hallo daarentegen, variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="4a02d-243">Properties available in hello **typeProperties** section of hello activity, on hello other hand, vary with each activity type.</span></span> <span data-ttu-id="4a02d-244">Voor de kopieeractiviteit hello afhankelijk Hallo type-eigenschappen Hallo soorten gegevensbronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="4a02d-244">For hello copy activity, hello type properties vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="4a02d-245">In de kopieerbewerking wanneer Hallo bron van het type **FileSystemSource**, Hallo eigenschap na is beschikbaar in **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="4a02d-245">In copy activity, when hello source is of type **FileSystemSource**, hello following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="4a02d-246">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4a02d-246">Property</span></span> | <span data-ttu-id="4a02d-247">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4a02d-247">Description</span></span> | <span data-ttu-id="4a02d-248">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="4a02d-248">Allowed values</span></span> | <span data-ttu-id="4a02d-249">Vereist</span><span class="sxs-lookup"><span data-stu-id="4a02d-249">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4a02d-250">Recursieve</span><span class="sxs-lookup"><span data-stu-id="4a02d-250">recursive</span></span> |<span data-ttu-id="4a02d-251">Hiermee wordt aangegeven of gegevens Hallo recursief is gelezen vanuit Hallo submappen of alleen vanuit de opgegeven map Hallo.</span><span class="sxs-lookup"><span data-stu-id="4a02d-251">Indicates whether hello data is read recursively from hello subfolders, or only from hello specified folder.</span></span> |<span data-ttu-id="4a02d-252">True, False (standaard)</span><span class="sxs-lookup"><span data-stu-id="4a02d-252">True, False (default)</span></span> |<span data-ttu-id="4a02d-253">Nee</span><span class="sxs-lookup"><span data-stu-id="4a02d-253">No</span></span> |

## <a name="json-example-copy-data-from-ftp-server-tooazure-blob"></a><span data-ttu-id="4a02d-254">JSON-voorbeeld: gegevens kopiëren van de FTP-server tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="4a02d-254">JSON example: Copy data from FTP server tooAzure Blob</span></span>
<span data-ttu-id="4a02d-255">In dit voorbeeld laat zien hoe toocopy gegevens van een FTP-server tooAzure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="4a02d-255">This sample shows how toocopy data from an FTP server tooAzure Blob storage.</span></span> <span data-ttu-id="4a02d-256">Echter gegevens kunnen worden gekopieerd direct tooany Hallo sinks vermelde in Hallo [ondersteunde gegevensarchieven en indelingen](data-factory-data-movement-activities.md#supported-data-stores-and-formats), met behulp van de kopieeractiviteit Hallo in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4a02d-256">However, data can be copied directly tooany of hello sinks stated in hello [supported data stores and formats](data-factory-data-movement-activities.md#supported-data-stores-and-formats), by using hello copy activity in Data Factory.</span></span>  

<span data-ttu-id="4a02d-257">Hallo volgende voorbeelden geven voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), of [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="4a02d-257">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span></span>

* <span data-ttu-id="4a02d-258">Een gekoppelde service van het type [FtpServer](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="4a02d-258">A linked service of type [FtpServer](#linked-service-properties)</span></span>
* <span data-ttu-id="4a02d-259">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="4a02d-259">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="4a02d-260">Invoer [gegevensset](data-factory-create-datasets.md) van het type [bestandsshare](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="4a02d-260">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties)</span></span>
* <span data-ttu-id="4a02d-261">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="4a02d-261">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="4a02d-262">Een [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [FileSystemSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="4a02d-262">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="4a02d-263">Hallo-voorbeeld worden gegevens gekopieerd van een FTP-server tooan Azure blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="4a02d-263">hello sample copies data from an FTP server tooan Azure blob every hour.</span></span> <span data-ttu-id="4a02d-264">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="4a02d-264">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="ftp-linked-service"></a><span data-ttu-id="4a02d-265">Gekoppelde FTP-service</span><span class="sxs-lookup"><span data-stu-id="4a02d-265">FTP linked service</span></span>

<span data-ttu-id="4a02d-266">Basisverificatie, wordt dit voorbeeld met het Hallo-gebruikersnaam en wachtwoord in tekst zonder opmaak.</span><span class="sxs-lookup"><span data-stu-id="4a02d-266">This example uses basic authentication, with hello user name and password in plain text.</span></span> <span data-ttu-id="4a02d-267">U kunt ook een van de volgende manieren hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="4a02d-267">You can also use one of hello following ways:</span></span>

* <span data-ttu-id="4a02d-268">Anonieme verificatie</span><span class="sxs-lookup"><span data-stu-id="4a02d-268">Anonymous authentication</span></span>
* <span data-ttu-id="4a02d-269">Basisverificatie met versleutelde referenties</span><span class="sxs-lookup"><span data-stu-id="4a02d-269">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="4a02d-270">FTP via SSL/TLS (FTPS)</span><span class="sxs-lookup"><span data-stu-id="4a02d-270">FTP over SSL/TLS (FTPS)</span></span>

<span data-ttu-id="4a02d-271">Zie Hallo [FTP gekoppelde service](#linked-service-properties) sectie voor verschillende soorten verificatie die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4a02d-271">See hello [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
    "type": "FtpServer",
    "typeProperties": {
        "host": "myftpserver.com",           
        "authenticationType": "Basic",
        "username": "Admin",
        "password": "123456"
    }
  }
}
```
### <a name="azure-storage-linked-service"></a><span data-ttu-id="4a02d-272">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="4a02d-272">Azure Storage linked service</span></span>

```JSON
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
### <a name="ftp-input-dataset"></a><span data-ttu-id="4a02d-273">FTP-invoergegevensset</span><span class="sxs-lookup"><span data-stu-id="4a02d-273">FTP input dataset</span></span>

<span data-ttu-id="4a02d-274">Deze gegevensset verwijst toohello FTP-map `mysharedfolder` en de bestandsnaam `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="4a02d-274">This dataset refers toohello FTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="4a02d-275">Hallo pijplijn kopieert Hallo toohello bestemming.</span><span class="sxs-lookup"><span data-stu-id="4a02d-275">hello pipeline copies hello file toohello destination.</span></span>

<span data-ttu-id="4a02d-276">Instelling **externe** te**true** informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet wordt geproduceerd door een activiteit in de gegevensfactory Hallo.</span><span class="sxs-lookup"><span data-stu-id="4a02d-276">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory, and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "FTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "FTPLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv",
      "useBinaryTransfer": true
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="4a02d-277">Azure Blob-uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="4a02d-277">Azure Blob output dataset</span></span>

<span data-ttu-id="4a02d-278">Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="4a02d-278">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="4a02d-279">Hallo mappad voor Hallo blob wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="4a02d-279">hello folder path for hello blob is dynamically evaluated, based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="4a02d-280">mappad Hallo Hallo jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4a02d-280">hello folder path uses hello year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/ftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a><span data-ttu-id="4a02d-281">Een kopieeractiviteit in een pijplijn met systeem bron- en blob bestandssink</span><span class="sxs-lookup"><span data-stu-id="4a02d-281">A copy activity in a pipeline with file system source and blob sink</span></span>

<span data-ttu-id="4a02d-282">Hallo pijplijn bevat een kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="4a02d-282">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="4a02d-283">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**FileSystemSource**, en Hallo **sink** type is ingesteld, te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="4a02d-283">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and hello **sink** type is set too**BlobSink**.</span></span>

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00Z",
        "end": "2016-08-24T19:00:00Z"
    }
}
```
> [!NOTE]
> <span data-ttu-id="4a02d-284">toomap kolommen uit de bron gegevensset toocolumns uit sink gegevensset, Zie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="4a02d-284">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a02d-285">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4a02d-285">Next steps</span></span>
<span data-ttu-id="4a02d-286">Zie Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4a02d-286">See hello following articles:</span></span>

* <span data-ttu-id="4a02d-287">toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (kopieeractiviteit) in Gegevensfactory en verschillende manieren toooptimize, Zie Hallo [activiteit prestaties en prestatieafstemming handleiding kopiëren](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="4a02d-287">toolearn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways toooptimize it, see hello [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="4a02d-288">Zie voor stapsgewijze instructies voor het maken van een pijplijn met een kopieeractiviteit hello [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="4a02d-288">For step-by-step instructions for creating a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
