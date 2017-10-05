---
title: Gegevens verplaatsen van een FTP-server met behulp van Azure Data Factory | Microsoft Docs
description: Meer informatie over het verplaatsen van gegevens van een FTP-server met behulp van Azure Data Factory.
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
ms.openlocfilehash: f8f31f3a2ee02c964737dd32145499f3dcfd0624
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a><span data-ttu-id="1b8cf-103">Gegevens verplaatsen van een FTP-server met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1b8cf-103">Move data from an FTP server by using Azure Data Factory</span></span>
<span data-ttu-id="1b8cf-104">Dit artikel wordt uitgelegd hoe u de kopieeractiviteit in Azure Data Factory om gegevens te verplaatsen van een FTP-server.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-104">This article explains how to use the copy activity in Azure Data Factory to move data from an FTP server.</span></span> <span data-ttu-id="1b8cf-105">Dit is gebaseerd op de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, hetgeen een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit toont.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="1b8cf-106">U kunt gegevens uit een FTP-server kopiëren naar een ondersteunde sink-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-106">You can copy data from an FTP server to any supported sink data store.</span></span> <span data-ttu-id="1b8cf-107">Zie voor een lijst met gegevensarchieven als PUT wordt ondersteund door de kopieeractiviteit, de [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-107">For a list of data stores supported as sinks by the copy activity, see the [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="1b8cf-108">Data Factory ondersteunt momenteel alleen zwevend gegevens van een FTP-server naar andere gegevensarchieven, maar niet verplaatsen van gegevens van andere gegevens worden opgeslagen met een FTP-server.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-108">Data Factory currently supports only moving data from an FTP server to other data stores, but not moving data from other data stores to an FTP server.</span></span> <span data-ttu-id="1b8cf-109">Deze ondersteuning biedt voor zowel on-premises en in de cloud van de FTP-servers.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-109">It supports both on-premises and cloud FTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="1b8cf-110">De kopieeractiviteit verwijdert het bronbestand niet nadat deze is gekopieerd naar de bestemming.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-110">The copy activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="1b8cf-111">Als u verwijderen van het bronbestand na een geslaagde kopie wilt, maakt u een aangepaste activiteit voor het verwijderen van het bestand en gebruikt u de activiteit in de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-111">If you need to delete the source file after a successful copy, create a custom activity to delete the file, and use the activity in the pipeline.</span></span> 

## <a name="enable-connectivity"></a><span data-ttu-id="1b8cf-112">Connectiviteit inschakelen</span><span class="sxs-lookup"><span data-stu-id="1b8cf-112">Enable connectivity</span></span>
<span data-ttu-id="1b8cf-113">Als u overstapt gegevens uit een **lokale** FTP-server aan een cloud gegevens opslaan (bijvoorbeeld naar Azure Blob-opslag), installeren en gebruiken van Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-113">If you are moving data from an **on-premises** FTP server to a cloud data store (for example, to Azure Blob storage), install and use Data Management Gateway.</span></span> <span data-ttu-id="1b8cf-114">Data Management Gateway is een clientagent die is geïnstalleerd op uw on-premises machine en cloudservices voor verbinding met een on-premises resource maakt.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-114">The Data Management Gateway is a client agent that is installed on your on-premises machine, and it allows cloud services to connect to an on-premises resource.</span></span> <span data-ttu-id="1b8cf-115">Zie voor meer informatie [Data Management Gateway](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="1b8cf-115">For details, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="1b8cf-116">Voor stapsgewijze instructies voor het instellen de gateway boven en gebruik, Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="1b8cf-116">For step-by-step instructions on setting up the gateway and using it, see [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="1b8cf-117">U kunt de gateway verbinding maken met een FTP-server, zelfs als de server zich op een Azure-infrastructuur als een dienst (IaaS) virtuele machine (VM).</span><span class="sxs-lookup"><span data-stu-id="1b8cf-117">You use the gateway to connect to an FTP server, even if the server is on an Azure infrastructure as a service (IaaS) virtual machine (VM).</span></span>

<span data-ttu-id="1b8cf-118">Het is mogelijk voor het installeren van de gateway op de lokale machine of de IaaS VM als de FTP-server.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-118">It is possible to install the gateway on the same on-premises machine or IaaS VM as the FTP server.</span></span> <span data-ttu-id="1b8cf-119">We raden echter aan dat u de gateway installeren op een afzonderlijke computer of op IaaS VM om bronconflicten te voorkomen, en voor betere prestaties.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-119">However, we recommend that you install the gateway on a separate machine or IaaS VM to avoid resource contention, and for better performance.</span></span> <span data-ttu-id="1b8cf-120">Wanneer u de gateway op een afzonderlijke computer installeert, is de machine moet toegang hebben tot de FTP-server.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-120">When you install the gateway on a separate machine, the machine should be able to access the FTP server.</span></span>

## <a name="get-started"></a><span data-ttu-id="1b8cf-121">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="1b8cf-121">Get started</span></span>
<span data-ttu-id="1b8cf-122">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens van een FTP-bron verplaatst met behulp van verschillende hulpprogramma's of API's.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-122">You can create a pipeline with a copy activity that moves data from an FTP source by using different tools or APIs.</span></span>

<span data-ttu-id="1b8cf-123">De eenvoudigste manier om een pijplijn maken is met de **Data Factory-Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-123">The easiest way to create a pipeline is to use the **Data Factory Copy Wizard**.</span></span> <span data-ttu-id="1b8cf-124">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough.</span></span>

<span data-ttu-id="1b8cf-125">U kunt ook de volgende hulpprogramma's gebruiken voor het maken van een pijplijn: **Azure-portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager-sjabloon**, **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="1b8cf-126">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies voor een pijplijn maken met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="1b8cf-127">Of u de hulpprogramma's of API's gebruiken, moet u de volgende stappen voor het maken van een pijplijn die de gegevens vanuit een brongegevensarchief naar een gegevensarchief sink verplaatst uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="1b8cf-127">Whether you use the tools or APIs, perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="1b8cf-128">Maak **gekoppelde services** slaat om invoer- en gegevens te koppelen aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-128">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="1b8cf-129">Maak **gegevenssets** vertegenwoordigt de invoer- en -gegevens voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-129">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="1b8cf-130">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="1b8cf-131">Wanneer u de wizard gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="1b8cf-132">Wanneer u hulpprogramma's of API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van de JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-132">When you use tools or APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="1b8cf-133">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die worden gebruikt om gegevens te kopiëren van een FTP-gegevensarchief de [JSON-voorbeeld: gegevens kopiëren van de FTP-server naar Azure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from an FTP data store, see the [JSON example: Copy data from FTP server to Azure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="1b8cf-134">Zie voor meer informatie over ondersteunde indelingen voor de bestands- en compressie te gebruiken, [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="1b8cf-134">For details about supported file and compression formats to use, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="1b8cf-135">De volgende secties bevatten informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van Data Factory-entiteiten die specifiek voor FTP.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-135">The following sections provide details about JSON properties that are used to define Data Factory entities specific to FTP.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="1b8cf-136">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="1b8cf-136">Linked service properties</span></span>
<span data-ttu-id="1b8cf-137">De volgende tabel beschrijft de JSON-elementen die specifiek zijn voor een FTP-gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-137">The following table describes JSON elements specific to an FTP linked service.</span></span>

| <span data-ttu-id="1b8cf-138">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="1b8cf-138">Property</span></span> | <span data-ttu-id="1b8cf-139">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1b8cf-139">Description</span></span> | <span data-ttu-id="1b8cf-140">Vereist</span><span class="sxs-lookup"><span data-stu-id="1b8cf-140">Required</span></span> | <span data-ttu-id="1b8cf-141">Standaard</span><span class="sxs-lookup"><span data-stu-id="1b8cf-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1b8cf-142">type</span><span class="sxs-lookup"><span data-stu-id="1b8cf-142">type</span></span> |<span data-ttu-id="1b8cf-143">Stel dit in op FtpServer.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-143">Set this to FtpServer.</span></span> |<span data-ttu-id="1b8cf-144">Ja</span><span class="sxs-lookup"><span data-stu-id="1b8cf-144">Yes</span></span> |&nbsp; |
| <span data-ttu-id="1b8cf-145">host</span><span class="sxs-lookup"><span data-stu-id="1b8cf-145">host</span></span> |<span data-ttu-id="1b8cf-146">Geef de naam of IP-adres van de FTP-server.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-146">Specify the name or IP address of the FTP server.</span></span> |<span data-ttu-id="1b8cf-147">Ja</span><span class="sxs-lookup"><span data-stu-id="1b8cf-147">Yes</span></span> |&nbsp; |
| <span data-ttu-id="1b8cf-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="1b8cf-148">authenticationType</span></span> |<span data-ttu-id="1b8cf-149">Geef het verificatietype.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-149">Specify the authentication type.</span></span> |<span data-ttu-id="1b8cf-150">Ja</span><span class="sxs-lookup"><span data-stu-id="1b8cf-150">Yes</span></span> |<span data-ttu-id="1b8cf-151">Basic, anonieme</span><span class="sxs-lookup"><span data-stu-id="1b8cf-151">Basic, Anonymous</span></span> |
| <span data-ttu-id="1b8cf-152">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="1b8cf-152">username</span></span> |<span data-ttu-id="1b8cf-153">De gebruiker die toegang tot de FTP-server heeft opgeven.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-153">Specify the user who has access to the FTP server.</span></span> |<span data-ttu-id="1b8cf-154">Nee</span><span class="sxs-lookup"><span data-stu-id="1b8cf-154">No</span></span> |&nbsp; |
| <span data-ttu-id="1b8cf-155">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="1b8cf-155">password</span></span> |<span data-ttu-id="1b8cf-156">Geef het wachtwoord voor de gebruiker (gebruikersnaam).</span><span class="sxs-lookup"><span data-stu-id="1b8cf-156">Specify the password for the user (username).</span></span> |<span data-ttu-id="1b8cf-157">Nee</span><span class="sxs-lookup"><span data-stu-id="1b8cf-157">No</span></span> |&nbsp; |
| <span data-ttu-id="1b8cf-158">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="1b8cf-158">encryptedCredential</span></span> |<span data-ttu-id="1b8cf-159">Geef de versleutelde referenties voor toegang tot de FTP-server.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-159">Specify the encrypted credential to access the FTP server.</span></span> |<span data-ttu-id="1b8cf-160">Nee</span><span class="sxs-lookup"><span data-stu-id="1b8cf-160">No</span></span> |&nbsp; |
| <span data-ttu-id="1b8cf-161">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1b8cf-161">gatewayName</span></span> |<span data-ttu-id="1b8cf-162">Geef de naam van de gateway in Data Management Gateway verbinding maken met een on-premises FTP-server.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-162">Specify the name of the gateway in Data Management Gateway to connect to an on-premises FTP server.</span></span> |<span data-ttu-id="1b8cf-163">Nee</span><span class="sxs-lookup"><span data-stu-id="1b8cf-163">No</span></span> |&nbsp; |
| <span data-ttu-id="1b8cf-164">poort</span><span class="sxs-lookup"><span data-stu-id="1b8cf-164">port</span></span> |<span data-ttu-id="1b8cf-165">Geef de poort waarop de FTP-server luistert.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-165">Specify the port on which the FTP server is listening.</span></span> |<span data-ttu-id="1b8cf-166">Nee</span><span class="sxs-lookup"><span data-stu-id="1b8cf-166">No</span></span> |<span data-ttu-id="1b8cf-167">21</span><span class="sxs-lookup"><span data-stu-id="1b8cf-167">21</span></span> |
| <span data-ttu-id="1b8cf-168">enableSsl</span><span class="sxs-lookup"><span data-stu-id="1b8cf-168">enableSsl</span></span> |<span data-ttu-id="1b8cf-169">Geef op of FTP gebruiken via een SSL/TLS-kanaal.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-169">Specify whether to use FTP over an SSL/TLS channel.</span></span> |<span data-ttu-id="1b8cf-170">Nee</span><span class="sxs-lookup"><span data-stu-id="1b8cf-170">No</span></span> |<span data-ttu-id="1b8cf-171">De waarde True</span><span class="sxs-lookup"><span data-stu-id="1b8cf-171">true</span></span> |
| <span data-ttu-id="1b8cf-172">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="1b8cf-172">enableServerCertificateValidation</span></span> |<span data-ttu-id="1b8cf-173">Geef op of validatie van het servercertificaat SSL inschakelen wanneer u FTP via SSL/TLS-kanaal.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-173">Specify whether to enable server SSL certificate validation when you are using FTP over SSL/TLS channel.</span></span> |<span data-ttu-id="1b8cf-174">Nee</span><span class="sxs-lookup"><span data-stu-id="1b8cf-174">No</span></span> |<span data-ttu-id="1b8cf-175">De waarde True</span><span class="sxs-lookup"><span data-stu-id="1b8cf-175">true</span></span> |

### <a name="use-anonymous-authentication"></a><span data-ttu-id="1b8cf-176">Gebruik anonieme verificatie</span><span class="sxs-lookup"><span data-stu-id="1b8cf-176">Use Anonymous authentication</span></span>

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

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="1b8cf-177">Gebruik van gebruikersnaam en wachtwoord voor basisverificatie in tekst zonder opmaak</span><span class="sxs-lookup"><span data-stu-id="1b8cf-177">Use username and password in plain text for basic authentication</span></span>

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

### <a name="use-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="1b8cf-178">Gebruik poort, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="1b8cf-178">Use port, enableSsl, enableServerCertificateValidation</span></span>

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

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="1b8cf-179">EncryptedCredential gebruiken voor verificatie en gateway</span><span class="sxs-lookup"><span data-stu-id="1b8cf-179">Use encryptedCredential for authentication and gateway</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="1b8cf-180">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="1b8cf-180">Dataset properties</span></span>
<span data-ttu-id="1b8cf-181">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets [gegevenssets maken](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="1b8cf-181">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="1b8cf-182">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle typen van de gegevensset.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-182">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="1b8cf-183">De **typeProperties** sectie verschilt voor elk type dataset.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-183">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="1b8cf-184">Het levert informatie die specifiek is voor het type dataset.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-184">It provides information that is specific to the dataset type.</span></span> <span data-ttu-id="1b8cf-185">De **typeProperties** sectie voor een gegevensset van het type **FileShare** heeft de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="1b8cf-185">The **typeProperties** section for a dataset of type **FileShare** has the following properties:</span></span>

| <span data-ttu-id="1b8cf-186">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="1b8cf-186">Property</span></span> | <span data-ttu-id="1b8cf-187">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1b8cf-187">Description</span></span> | <span data-ttu-id="1b8cf-188">Vereist</span><span class="sxs-lookup"><span data-stu-id="1b8cf-188">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1b8cf-189">folderPath</span><span class="sxs-lookup"><span data-stu-id="1b8cf-189">folderPath</span></span> |<span data-ttu-id="1b8cf-190">Subpad naar de map.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-190">Subpath to the folder.</span></span> <span data-ttu-id="1b8cf-191">Gebruik van escape-teken ' \ ' voor speciale tekens in de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-191">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="1b8cf-192">Zie [voorbeeld gekoppelde service en gegevensset definities](#sample-linked-service-and-dataset-definitions) voor voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-192">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="1b8cf-193">U kunt deze eigenschap combineren met **partitionBy** mappaden op basis van het segment start en eindtijden datum.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-193">You can combine this property with **partitionBy** to have folder paths based on slice start and end date-times.</span></span> |<span data-ttu-id="1b8cf-194">Ja</span><span class="sxs-lookup"><span data-stu-id="1b8cf-194">Yes</span></span> |
| <span data-ttu-id="1b8cf-195">fileName</span><span class="sxs-lookup"><span data-stu-id="1b8cf-195">fileName</span></span> |<span data-ttu-id="1b8cf-196">Geef de naam van het bestand in de **folderPath** als u wilt dat de tabel om te verwijzen naar een bepaald bestand in de map.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-196">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="1b8cf-197">Als u geen waarde voor deze eigenschap niet opgeeft, wordt de tabel verwijst naar alle bestanden in de map.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-197">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="1b8cf-198">Wanneer **fileName** is niet opgegeven voor een uitvoergegevensset, de naam van het gegenereerde bestand is in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="1b8cf-198">When **fileName** is not specified for an output dataset, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="1b8cf-199">Gegevens. <Guid>.txt (voorbeeld: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="1b8cf-199">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="1b8cf-200">Nee</span><span class="sxs-lookup"><span data-stu-id="1b8cf-200">No</span></span> |
| <span data-ttu-id="1b8cf-201">fileFilter</span><span class="sxs-lookup"><span data-stu-id="1b8cf-201">fileFilter</span></span> |<span data-ttu-id="1b8cf-202">Geef een filter om te worden gebruikt voor het selecteren van een subset van de bestanden in de **folderPath**, in plaats van alle bestanden.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-202">Specify a filter to be used to select a subset of files in the **folderPath**, rather than all files.</span></span><br/><br/><span data-ttu-id="1b8cf-203">Toegestane waarden zijn: `*` (meerdere tekens) en `?` (willekeurig teken).</span><span class="sxs-lookup"><span data-stu-id="1b8cf-203">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="1b8cf-204">Voorbeeld 1:`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="1b8cf-204">Example 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="1b8cf-205">Voorbeeld 2:`"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="1b8cf-205">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="1b8cf-206">**fileFilter** is van toepassing op een bestandsshare-invoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-206">**fileFilter** is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="1b8cf-207">Deze eigenschap wordt niet ondersteund met Hadoop Distributed File System (HDFS).</span><span class="sxs-lookup"><span data-stu-id="1b8cf-207">This property is not supported with Hadoop Distributed File System (HDFS).</span></span> |<span data-ttu-id="1b8cf-208">Nee</span><span class="sxs-lookup"><span data-stu-id="1b8cf-208">No</span></span> |
| <span data-ttu-id="1b8cf-209">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="1b8cf-209">partitionedBy</span></span> |<span data-ttu-id="1b8cf-210">Hiermee geeft u een dynamische **folderPath** en **fileName** voor tijd reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-210">Used to specify a dynamic **folderPath** and **fileName** for time series data.</span></span> <span data-ttu-id="1b8cf-211">Bijvoorbeeld, kunt u een **folderPath** met parameters die voor elk uur van gegevens.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-211">For example, you can specify a **folderPath** that is parameterized for every hour of data.</span></span> |<span data-ttu-id="1b8cf-212">Nee</span><span class="sxs-lookup"><span data-stu-id="1b8cf-212">No</span></span> |
| <span data-ttu-id="1b8cf-213">Indeling</span><span class="sxs-lookup"><span data-stu-id="1b8cf-213">format</span></span> | <span data-ttu-id="1b8cf-214">De volgende indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-214">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="1b8cf-215">Stel de **type** eigenschap onder indeling op een van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-215">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="1b8cf-216">Zie voor meer informatie de [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-216">For more information, see the [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="1b8cf-217">Als u wilt kopiëren van bestanden, omdat ze tussen winkels op basis van bestanden (binaire kopiëren), slaat u de sectie indeling in de definities van beide invoer en uitvoer gegevensset.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-217">If you want to copy files as they are between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="1b8cf-218">Nee</span><span class="sxs-lookup"><span data-stu-id="1b8cf-218">No</span></span> |
| <span data-ttu-id="1b8cf-219">Compressie</span><span class="sxs-lookup"><span data-stu-id="1b8cf-219">compression</span></span> | <span data-ttu-id="1b8cf-220">Geef het type en de compressie van de gegevens.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-220">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="1b8cf-221">Ondersteunde typen zijn **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**, en ondersteunde niveaus zijn **optimale** en **snelst**.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-221">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**, and supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="1b8cf-222">Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="1b8cf-222">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="1b8cf-223">Nee</span><span class="sxs-lookup"><span data-stu-id="1b8cf-223">No</span></span> |
| <span data-ttu-id="1b8cf-224">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="1b8cf-224">useBinaryTransfer</span></span> |<span data-ttu-id="1b8cf-225">Geef op of de binaire overdrachtsmodus gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-225">Specify whether to use the binary transfer mode.</span></span> <span data-ttu-id="1b8cf-226">De waarden zijn true zijn voor binaire modus (dit is de standaardwaarde) en false voor ASCII.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-226">The values are true for binary mode (this is the default value), and false for ASCII.</span></span> <span data-ttu-id="1b8cf-227">Deze eigenschap kan alleen worden gebruikt als het type van de bijbehorende gekoppelde service van het type: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-227">This property can only be used when the associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="1b8cf-228">Nee</span><span class="sxs-lookup"><span data-stu-id="1b8cf-228">No</span></span> |

> [!NOTE]
> <span data-ttu-id="1b8cf-229">**Bestandsnaam** en **fileFilter** niet gelijktijdig worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-229">**fileName** and **fileFilter** cannot be used simultaneously.</span></span>

### <a name="use-the-partionedby-property"></a><span data-ttu-id="1b8cf-230">Gebruik de eigenschap partionedBy</span><span class="sxs-lookup"><span data-stu-id="1b8cf-230">Use the partionedBy property</span></span>
<span data-ttu-id="1b8cf-231">Zoals vermeld in de vorige sectie, kunt u een dynamische **folderPath** en **fileName** voor time series-gegevens met de **partitionedBy** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-231">As mentioned in the previous section, you can specify a dynamic **folderPath** and **fileName** for time series data with the **partitionedBy** property.</span></span>

<span data-ttu-id="1b8cf-232">Zie voor meer informatie over tijd reeks gegevenssets, planning en segmenten, [gegevenssets maken](data-factory-create-datasets.md), [planning en uitvoering](data-factory-scheduling-and-execution.md), en [pijplijnen maken](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="1b8cf-232">To learn about time series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="1b8cf-233">Voorbeeld 1</span><span class="sxs-lookup"><span data-stu-id="1b8cf-233">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="1b8cf-234">In dit voorbeeld {segment} is vervangen door de waarde van de Data Factory systeemvariabele SliceStart, in de opgegeven indeling (YYYYMMDDHH).</span><span class="sxs-lookup"><span data-stu-id="1b8cf-234">In this example, {Slice} is replaced with the value of Data Factory system variable SliceStart, in the format specified (YYYYMMDDHH).</span></span> <span data-ttu-id="1b8cf-235">De SliceStart verwijst voor het starten van de tijd van het segment.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-235">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="1b8cf-236">Het mappad verschilt voor elk segment.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-236">The folder path is different for each slice.</span></span> <span data-ttu-id="1b8cf-237">(Bijvoorbeeld wikidatagateway/wikisampledataout/2014100103 of wikidatagateway/wikisampledataout/2014100104.)</span><span class="sxs-lookup"><span data-stu-id="1b8cf-237">(For example, wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.)</span></span>

#### <a name="sample-2"></a><span data-ttu-id="1b8cf-238">Voorbeeld 2</span><span class="sxs-lookup"><span data-stu-id="1b8cf-238">Sample 2</span></span>

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
<span data-ttu-id="1b8cf-239">In dit voorbeeld wordt het jaar, maand, dag en tijd van de SliceStart worden uitgepakt in verschillende variabelen die worden gebruikt door de **folderPath** en **fileName** eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-239">In this example, the year, month, day, and time of SliceStart are extracted into separate variables that are used by the **folderPath** and **fileName** properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="1b8cf-240">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="1b8cf-240">Copy activity properties</span></span>
<span data-ttu-id="1b8cf-241">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van activiteiten [pijplijnen maken](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="1b8cf-241">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="1b8cf-242">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en beleidsregels zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-242">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="1b8cf-243">Eigenschappen die beschikbaar zijn in de **typeProperties** sectie van de activiteit aan de andere kant variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-243">Properties available in the **typeProperties** section of the activity, on the other hand, vary with each activity type.</span></span> <span data-ttu-id="1b8cf-244">Voor de kopieeractiviteit wordt de type-eigenschappen variëren afhankelijk van de typen van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-244">For the copy activity, the type properties vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="1b8cf-245">In de kopieeractiviteit, wanneer de bron van het type **FileSystemSource**, de volgende eigenschap is beschikbaar in **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="1b8cf-245">In copy activity, when the source is of type **FileSystemSource**, the following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="1b8cf-246">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="1b8cf-246">Property</span></span> | <span data-ttu-id="1b8cf-247">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1b8cf-247">Description</span></span> | <span data-ttu-id="1b8cf-248">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="1b8cf-248">Allowed values</span></span> | <span data-ttu-id="1b8cf-249">Vereist</span><span class="sxs-lookup"><span data-stu-id="1b8cf-249">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1b8cf-250">Recursieve</span><span class="sxs-lookup"><span data-stu-id="1b8cf-250">recursive</span></span> |<span data-ttu-id="1b8cf-251">Hiermee wordt aangegeven of de gegevens recursief is gelezen uit de submappen, of alleen uit de opgegeven map.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-251">Indicates whether the data is read recursively from the subfolders, or only from the specified folder.</span></span> |<span data-ttu-id="1b8cf-252">True, False (standaard)</span><span class="sxs-lookup"><span data-stu-id="1b8cf-252">True, False (default)</span></span> |<span data-ttu-id="1b8cf-253">Nee</span><span class="sxs-lookup"><span data-stu-id="1b8cf-253">No</span></span> |

## <a name="json-example-copy-data-from-ftp-server-to-azure-blob"></a><span data-ttu-id="1b8cf-254">JSON-voorbeeld: gegevens kopiëren van de FTP-server naar Azure Blob</span><span class="sxs-lookup"><span data-stu-id="1b8cf-254">JSON example: Copy data from FTP server to Azure Blob</span></span>
<span data-ttu-id="1b8cf-255">Dit voorbeeld laat zien hoe gegevens kopiëren van een FTP-server naar Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-255">This sample shows how to copy data from an FTP server to Azure Blob storage.</span></span> <span data-ttu-id="1b8cf-256">Echter gegevens kunnen worden gekopieerd naar een van de PUT vermeld in de [ondersteunde gegevensarchieven en indelingen](data-factory-data-movement-activities.md#supported-data-stores-and-formats), met behulp van de kopieeractiviteit in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-256">However, data can be copied directly to any of the sinks stated in the [supported data stores and formats](data-factory-data-movement-activities.md#supported-data-stores-and-formats), by using the copy activity in Data Factory.</span></span>  

<span data-ttu-id="1b8cf-257">De volgende voorbeelden geven voorbeeld JSON definities die u een pijplijn maken kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), of [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="1b8cf-257">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span></span>

* <span data-ttu-id="1b8cf-258">Een gekoppelde service van het type [FtpServer](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="1b8cf-258">A linked service of type [FtpServer](#linked-service-properties)</span></span>
* <span data-ttu-id="1b8cf-259">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="1b8cf-259">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="1b8cf-260">Invoer [gegevensset](data-factory-create-datasets.md) van het type [bestandsshare](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="1b8cf-260">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties)</span></span>
* <span data-ttu-id="1b8cf-261">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="1b8cf-261">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="1b8cf-262">Een [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [FileSystemSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="1b8cf-262">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="1b8cf-263">Het voorbeeld kopieert gegevens van een FTP-server naar een Azure-blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-263">The sample copies data from an FTP server to an Azure blob every hour.</span></span> <span data-ttu-id="1b8cf-264">De JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na de voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-264">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="ftp-linked-service"></a><span data-ttu-id="1b8cf-265">Gekoppelde FTP-service</span><span class="sxs-lookup"><span data-stu-id="1b8cf-265">FTP linked service</span></span>

<span data-ttu-id="1b8cf-266">Basisverificatie, wordt dit voorbeeld met de gebruikersnaam en wachtwoord in tekst zonder opmaak.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-266">This example uses basic authentication, with the user name and password in plain text.</span></span> <span data-ttu-id="1b8cf-267">U kunt ook een van de volgende manieren gebruiken:</span><span class="sxs-lookup"><span data-stu-id="1b8cf-267">You can also use one of the following ways:</span></span>

* <span data-ttu-id="1b8cf-268">Anonieme verificatie</span><span class="sxs-lookup"><span data-stu-id="1b8cf-268">Anonymous authentication</span></span>
* <span data-ttu-id="1b8cf-269">Basisverificatie met versleutelde referenties</span><span class="sxs-lookup"><span data-stu-id="1b8cf-269">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="1b8cf-270">FTP via SSL/TLS (FTPS)</span><span class="sxs-lookup"><span data-stu-id="1b8cf-270">FTP over SSL/TLS (FTPS)</span></span>

<span data-ttu-id="1b8cf-271">Zie de [FTP gekoppelde service](#linked-service-properties) sectie voor verschillende soorten verificatie die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-271">See the [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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
### <a name="azure-storage-linked-service"></a><span data-ttu-id="1b8cf-272">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="1b8cf-272">Azure Storage linked service</span></span>

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
### <a name="ftp-input-dataset"></a><span data-ttu-id="1b8cf-273">FTP-invoergegevensset</span><span class="sxs-lookup"><span data-stu-id="1b8cf-273">FTP input dataset</span></span>

<span data-ttu-id="1b8cf-274">Deze gegevensset verwijst naar de FTP-map `mysharedfolder` en de bestandsnaam `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-274">This dataset refers to the FTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="1b8cf-275">De pijplijn kopieert het bestand naar de bestemming.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-275">The pipeline copies the file to the destination.</span></span>

<span data-ttu-id="1b8cf-276">Instelling **externe** naar **true** informeert de Data Factory-service in de gegevensset extern is aan de gegevensfactory en niet wordt geproduceerd door een activiteit in de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-276">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory, and is not produced by an activity in the data factory.</span></span>

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

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="1b8cf-277">Azure Blob-uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="1b8cf-277">Azure Blob output dataset</span></span>

<span data-ttu-id="1b8cf-278">Gegevens worden geschreven naar een nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="1b8cf-278">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="1b8cf-279">Het pad naar de blob wordt dynamisch geëvalueerd op basis van de begintijd van het segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-279">The folder path for the blob is dynamically evaluated, based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="1b8cf-280">Het mappad maakt gebruik van het jaar, maand, dag en uur delen van de begintijd.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-280">The folder path uses the year, month, day, and hours parts of the start time.</span></span>

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


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a><span data-ttu-id="1b8cf-281">Een kopieeractiviteit in een pijplijn met systeem bron- en blob bestandssink</span><span class="sxs-lookup"><span data-stu-id="1b8cf-281">A copy activity in a pipeline with file system source and blob sink</span></span>

<span data-ttu-id="1b8cf-282">De pijplijn bevat een kopieeractiviteit die is geconfigureerd voor gebruik van de invoer- en uitvoergegevenssets en elk uur is gepland.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-282">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="1b8cf-283">In de pijplijn-JSON-definitie de **bron** type is ingesteld op **FileSystemSource**, en de **sink** type is ingesteld op **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="1b8cf-283">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and the **sink** type is set to **BlobSink**.</span></span>

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
> <span data-ttu-id="1b8cf-284">Zie het toewijzen van kolommen uit de bron-gegevensset naar kolommen uit de dataset sink [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="1b8cf-284">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b8cf-285">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1b8cf-285">Next steps</span></span>
<span data-ttu-id="1b8cf-286">Zie de volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="1b8cf-286">See the following articles:</span></span>

* <span data-ttu-id="1b8cf-287">Zie voor meer informatie over de belangrijkste factoren die prestaties impact van gegevensverplaatsing (kopieeractiviteit) in de Data Factory en verschillende manieren om te optimaliseren, de [activiteit prestaties en prestatieafstemming handleiding kopiëren](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="1b8cf-287">To learn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways to optimize it, see the [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="1b8cf-288">Zie voor stapsgewijze instructies voor het maken van een pijplijn met een kopieeractiviteit de [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="1b8cf-288">For step-by-step instructions for creating a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
