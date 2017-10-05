---
title: Gegevens verplaatsen van een HTTP-bron - Azure | Microsoft Docs
description: Meer informatie over het verplaatsen van gegevens uit een on-premises of een HTTP-bron van cloud met Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 3cc1bd293868b0bb093f617ac12e16c26780fc89
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a><span data-ttu-id="1905d-103">Gegevens verplaatsen van een HTTP-bron met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1905d-103">Move data from an HTTP source using Azure Data Factory</span></span>
<span data-ttu-id="1905d-104">In dit artikel bevat een overzicht van het gebruik van de Kopieeractiviteit in Azure Data Factory om gegevens te verplaatsen van een on-premises/cloudtoepassing HTTP-eindpunt met een ondersteunde sink-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="1905d-104">This article outlines how to use the Copy Activity in Azure Data Factory to move data from an on-premises/cloud HTTP endpoint to a supported sink data store.</span></span> <span data-ttu-id="1905d-105">In dit artikel is gebaseerd op de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel met daarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit en de lijst met gegevensarchieven ondersteund als bronnen/Put.</span><span class="sxs-lookup"><span data-stu-id="1905d-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and the list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="1905d-106">Data factory ondersteunt momenteel alleen zwevend gegevens van een HTTP-bron naar andere gegevensarchieven, maar niet verplaatsen van gegevens van andere gegevens worden opgeslagen op een HTTP-doel.</span><span class="sxs-lookup"><span data-stu-id="1905d-106">Data factory currently supports only moving data from an HTTP source to other data stores, but not moving data from other data stores to an HTTP destination.</span></span>

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="1905d-107">Ondersteunde scenario's en verificatietypen</span><span class="sxs-lookup"><span data-stu-id="1905d-107">Supported scenarios and authentication types</span></span>
<span data-ttu-id="1905d-108">U kunt deze connector HTTP-gegevens ophalen van **zowel cloud als on-premises HTTP/s-eindpunt** met behulp van HTTP **ophalen** of **POST** methode.</span><span class="sxs-lookup"><span data-stu-id="1905d-108">You can use this HTTP connector to retrieve data from **both cloud and on-premises HTTP/s endpoint** by using HTTP **GET** or **POST** method.</span></span> <span data-ttu-id="1905d-109">De volgende verificatietypen worden ondersteund: **anoniem**, **Basic**, **Digest**, **Windows**, en **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="1905d-109">The following authentication types are supported: **Anonymous**, **Basic**, **Digest**, **Windows**, and **ClientCertificate**.</span></span> <span data-ttu-id="1905d-110">Noteer het verschil tussen deze connector en de [Web tabel connector](data-factory-web-table-connector.md) is: de laatste tabelinhoud ophalen uit webpagina HTML wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1905d-110">Note the difference between this connector and the [Web table connector](data-factory-web-table-connector.md) is: the latter is used to extract table content from web HTML page.</span></span>

<span data-ttu-id="1905d-111">Bij het kopiëren van gegevens uit een lokale HTTP-eindpunt, moet u een Data Management Gateway installeren in de lokale omgeving/Azure VM.</span><span class="sxs-lookup"><span data-stu-id="1905d-111">When copying data from an on-premises HTTP endpoint, you need install a Data Management Gateway in the on-premises environment/Azure VM.</span></span> <span data-ttu-id="1905d-112">Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor meer informatie over Data Management Gateway en stapsgewijze instructies over het instellen van de gateway.</span><span class="sxs-lookup"><span data-stu-id="1905d-112">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="1905d-113">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="1905d-113">Getting started</span></span>
<span data-ttu-id="1905d-114">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens van een HTTP-bron verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="1905d-114">You can create a pipeline with a copy activity that moves data from an HTTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="1905d-115">De eenvoudigste manier om een pijplijn maken is met de **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="1905d-115">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="1905d-116">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met de wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="1905d-116">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

- <span data-ttu-id="1905d-117">U kunt ook de volgende hulpprogramma's gebruiken voor het maken van een pijplijn: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon**, **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="1905d-117">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="1905d-118">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies voor een pijplijn maken met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="1905d-118">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> <span data-ttu-id="1905d-119">Zie voor voorbeelden van JSON gegevens van HTTP-bron kopiëren naar Azure Blob Storage, [JSON voorbeelden](#json-examples) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="1905d-119">For JSON samples to copy data from HTTP source to Azure Blob Storage, see [JSON examples](#json-examples) section of this articles.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="1905d-120">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="1905d-120">Linked service properties</span></span>
<span data-ttu-id="1905d-121">De volgende tabel bevat de beschrijving voor JSON-elementen die specifiek zijn voor HTTP gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="1905d-121">The following table provides description for JSON elements specific to HTTP linked service.</span></span>

| <span data-ttu-id="1905d-122">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="1905d-122">Property</span></span> | <span data-ttu-id="1905d-123">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1905d-123">Description</span></span> | <span data-ttu-id="1905d-124">Vereist</span><span class="sxs-lookup"><span data-stu-id="1905d-124">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1905d-125">type</span><span class="sxs-lookup"><span data-stu-id="1905d-125">type</span></span> | <span data-ttu-id="1905d-126">De eigenschap type moet worden ingesteld op: `Http`.</span><span class="sxs-lookup"><span data-stu-id="1905d-126">The type property must be set to: `Http`.</span></span> | <span data-ttu-id="1905d-127">Ja</span><span class="sxs-lookup"><span data-stu-id="1905d-127">Yes</span></span> |
| <span data-ttu-id="1905d-128">URL</span><span class="sxs-lookup"><span data-stu-id="1905d-128">url</span></span> | <span data-ttu-id="1905d-129">Basis-URL voor de webserver</span><span class="sxs-lookup"><span data-stu-id="1905d-129">Base URL to the Web Server</span></span> | <span data-ttu-id="1905d-130">Ja</span><span class="sxs-lookup"><span data-stu-id="1905d-130">Yes</span></span> |
| <span data-ttu-id="1905d-131">authenticationType</span><span class="sxs-lookup"><span data-stu-id="1905d-131">authenticationType</span></span> | <span data-ttu-id="1905d-132">Hiermee geeft u het verificatietype.</span><span class="sxs-lookup"><span data-stu-id="1905d-132">Specifies the authentication type.</span></span> <span data-ttu-id="1905d-133">Toegestane waarden zijn: **anoniem**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="1905d-133">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="1905d-134">Raadpleeg de secties onder deze tabel over meer eigenschappen en voorbeelden voor deze verificatietypen JSON respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="1905d-134">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="1905d-135">Ja</span><span class="sxs-lookup"><span data-stu-id="1905d-135">Yes</span></span> |
| <span data-ttu-id="1905d-136">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="1905d-136">enableServerCertificateValidation</span></span> | <span data-ttu-id="1905d-137">Geef op of validatie van het servercertificaat SSL inschakelen als bron is een HTTPS-webserver</span><span class="sxs-lookup"><span data-stu-id="1905d-137">Specify whether to enable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="1905d-138">Nee, de standaardwaarde is true</span><span class="sxs-lookup"><span data-stu-id="1905d-138">No, default is true</span></span> |
| <span data-ttu-id="1905d-139">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1905d-139">gatewayName</span></span> | <span data-ttu-id="1905d-140">Naam van de Data Management Gateway verbinding maken met een lokale HTTP-bron.</span><span class="sxs-lookup"><span data-stu-id="1905d-140">Name of the Data Management Gateway to connect to an on-premises HTTP source.</span></span> | <span data-ttu-id="1905d-141">Ja als u gegevens kopiëren van een lokale HTTP-bron.</span><span class="sxs-lookup"><span data-stu-id="1905d-141">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="1905d-142">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="1905d-142">encryptedCredential</span></span> | <span data-ttu-id="1905d-143">Versleutelde referentie voor toegang tot het HTTP-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="1905d-143">Encrypted credential to access the HTTP endpoint.</span></span> <span data-ttu-id="1905d-144">Automatisch wordt gegenereerd wanneer u de verificatie-informatie in de wizard kopiëren of de ClickOnce-pop-dialoogvenster configureert.</span><span class="sxs-lookup"><span data-stu-id="1905d-144">Auto-generated when you configure the authentication information in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="1905d-145">Nee.</span><span class="sxs-lookup"><span data-stu-id="1905d-145">No.</span></span> <span data-ttu-id="1905d-146">Alleen van toepassing wanneer het kopiëren van gegevens uit een lokale HTTP-server.</span><span class="sxs-lookup"><span data-stu-id="1905d-146">Apply only when copying data from an on-premises HTTP server.</span></span> |

<span data-ttu-id="1905d-147">Zie [gegevens verplaatsen tussen lokale bronnen en de cloud met Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) voor meer informatie over het instellen van referenties voor on-premises HTTP connector-gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="1905d-147">See [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for details about setting credentials for on-premises HTTP connector data source.</span></span>

### <a name="using-basic-digest-or-windows-authentication"></a><span data-ttu-id="1905d-148">Met behulp van basisverificatie, verificatiesamenvatting of Windows-verificatie</span><span class="sxs-lookup"><span data-stu-id="1905d-148">Using Basic, Digest, or Windows authentication</span></span>

<span data-ttu-id="1905d-149">Stel `authenticationType` als `Basic`, `Digest`, of `Windows`, en geef de volgende eigenschappen naast de HTTP-connector algemene resources die hierboven zijn geïntroduceerd:</span><span class="sxs-lookup"><span data-stu-id="1905d-149">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="1905d-150">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="1905d-150">Property</span></span> | <span data-ttu-id="1905d-151">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1905d-151">Description</span></span> | <span data-ttu-id="1905d-152">Vereist</span><span class="sxs-lookup"><span data-stu-id="1905d-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1905d-153">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="1905d-153">username</span></span> | <span data-ttu-id="1905d-154">Gebruikersnaam voor toegang tot het HTTP-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="1905d-154">Username to access the HTTP endpoint.</span></span> | <span data-ttu-id="1905d-155">Ja</span><span class="sxs-lookup"><span data-stu-id="1905d-155">Yes</span></span> |
| <span data-ttu-id="1905d-156">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="1905d-156">password</span></span> | <span data-ttu-id="1905d-157">Wachtwoord voor de gebruiker (gebruikersnaam).</span><span class="sxs-lookup"><span data-stu-id="1905d-157">Password for the user (username).</span></span> | <span data-ttu-id="1905d-158">Ja</span><span class="sxs-lookup"><span data-stu-id="1905d-158">Yes</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="1905d-159">Voorbeeld: met behulp van basisverificatie, verificatiesamenvatting of Windows-verificatie</span><span class="sxs-lookup"><span data-stu-id="1905d-159">Example: using Basic, Digest, or Windows authentication</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "basic",
            "url" : "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

### <a name="using-clientcertificate-authentication"></a><span data-ttu-id="1905d-160">ClientCertificate-verificatie</span><span class="sxs-lookup"><span data-stu-id="1905d-160">Using ClientCertificate authentication</span></span>

<span data-ttu-id="1905d-161">Met basisverificatie, stelt `authenticationType` als `ClientCertificate`, en geef de volgende eigenschappen naast de HTTP-connector algemene resources die hierboven zijn geïntroduceerd:</span><span class="sxs-lookup"><span data-stu-id="1905d-161">To use basic authentication, set `authenticationType` as `ClientCertificate`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="1905d-162">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="1905d-162">Property</span></span> | <span data-ttu-id="1905d-163">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1905d-163">Description</span></span> | <span data-ttu-id="1905d-164">Vereist</span><span class="sxs-lookup"><span data-stu-id="1905d-164">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1905d-165">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="1905d-165">embeddedCertData</span></span> | <span data-ttu-id="1905d-166">De Base64-gecodeerde inhoud van de binaire gegevens van het bestand (Personal Information Exchange (PFX).</span><span class="sxs-lookup"><span data-stu-id="1905d-166">The Base64-encoded contents of binary data of the Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="1905d-167">Geef ofwel de `embeddedCertData` of `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="1905d-167">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="1905d-168">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="1905d-168">certThumbprint</span></span> | <span data-ttu-id="1905d-169">De vingerafdruk van het certificaat dat is geïnstalleerd op de gatewaycomputer certificaatarchief.</span><span class="sxs-lookup"><span data-stu-id="1905d-169">The thumbprint of the certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="1905d-170">Alleen van toepassing wanneer het kopiëren van gegevens van een lokale HTTP-bron.</span><span class="sxs-lookup"><span data-stu-id="1905d-170">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="1905d-171">Geef ofwel de `embeddedCertData` of `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="1905d-171">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="1905d-172">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="1905d-172">password</span></span> | <span data-ttu-id="1905d-173">Het wachtwoord is gekoppeld aan het certificaat.</span><span class="sxs-lookup"><span data-stu-id="1905d-173">Password associated with the certificate.</span></span> | <span data-ttu-id="1905d-174">Nee</span><span class="sxs-lookup"><span data-stu-id="1905d-174">No</span></span> |

<span data-ttu-id="1905d-175">Als u `certThumbprint` voor verificatie en het certificaat in het persoonlijke archief van de lokale computer is geïnstalleerd, moet u de machtiging lezen voor de gateway-service:</span><span class="sxs-lookup"><span data-stu-id="1905d-175">If you use `certThumbprint` for authentication and the certificate is installed in the personal store of the local computer, you need to grant the read permission to the gateway service:</span></span>

1. <span data-ttu-id="1905d-176">Start Microsoft Management Console (MMC).</span><span class="sxs-lookup"><span data-stu-id="1905d-176">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="1905d-177">Voeg de **certificaten** -module die gericht is op de **lokale Computer**.</span><span class="sxs-lookup"><span data-stu-id="1905d-177">Add the **Certificates** snap-in that targets the **Local Computer**.</span></span>
2. <span data-ttu-id="1905d-178">Vouw **certificaten**, **persoonlijke**, en klik op **certificaten**.</span><span class="sxs-lookup"><span data-stu-id="1905d-178">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="1905d-179">Met de rechtermuisknop op het certificaat uit het persoonlijke archief en selecteer **alle taken**->**persoonlijke sleutels beheren...**</span><span class="sxs-lookup"><span data-stu-id="1905d-179">Right-click the certificate from the personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="1905d-180">Op de **beveiliging** tabblad, het toevoegen van het gebruikersaccount waaronder Data Management Gateway Host Service wordt uitgevoerd met leestoegang tot het certificaat.</span><span class="sxs-lookup"><span data-stu-id="1905d-180">On the **Security** tab, add the user account under which Data Management Gateway Host Service is running with the read access to the certificate.</span></span>  

#### <a name="example-using-client-certificate"></a><span data-ttu-id="1905d-181">Voorbeeld: met behulp van clientcertificaat</span><span class="sxs-lookup"><span data-stu-id="1905d-181">Example: using client certificate</span></span>
<span data-ttu-id="1905d-182">Deze gekoppelde service wordt uw gegevensfactory op een lokale HTTP-webserver.</span><span class="sxs-lookup"><span data-stu-id="1905d-182">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="1905d-183">Dit maakt gebruik van een clientcertificaat dat is geïnstalleerd op de machine met Data Management Gateway is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="1905d-183">It uses a client certificate that is installed on the machine with Data Management Gateway installed.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"

        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="1905d-184">Voorbeeld: clientcertificaat gebruiken in een bestand</span><span class="sxs-lookup"><span data-stu-id="1905d-184">Example: using client certificate in a file</span></span>
<span data-ttu-id="1905d-185">Deze gekoppelde service wordt uw gegevensfactory op een lokale HTTP-webserver.</span><span class="sxs-lookup"><span data-stu-id="1905d-185">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="1905d-186">Een certificaatbestand van de client op de machine wordt met Data Management Gateway is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="1905d-186">It uses a client certificate file on the machine with Data Management Gateway installed.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="1905d-187">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="1905d-187">Dataset properties</span></span>
<span data-ttu-id="1905d-188">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van de [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="1905d-188">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="1905d-189">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="1905d-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="1905d-190">De **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over de locatie van de gegevens in het gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="1905d-190">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="1905d-191">De typeProperties sectie voor de gegevensset van het type **Http** heeft de volgende eigenschappen</span><span class="sxs-lookup"><span data-stu-id="1905d-191">The typeProperties section for dataset of type **Http** has the following properties</span></span>

| <span data-ttu-id="1905d-192">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="1905d-192">Property</span></span> | <span data-ttu-id="1905d-193">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1905d-193">Description</span></span> | <span data-ttu-id="1905d-194">Vereist</span><span class="sxs-lookup"><span data-stu-id="1905d-194">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1905d-195">type</span><span class="sxs-lookup"><span data-stu-id="1905d-195">type</span></span> | <span data-ttu-id="1905d-196">Het type van de gegevensset zijn opgegeven.</span><span class="sxs-lookup"><span data-stu-id="1905d-196">Specified the type of the dataset.</span></span> <span data-ttu-id="1905d-197">moet worden ingesteld op `Http`.</span><span class="sxs-lookup"><span data-stu-id="1905d-197">must be set to `Http`.</span></span> | <span data-ttu-id="1905d-198">Ja</span><span class="sxs-lookup"><span data-stu-id="1905d-198">Yes</span></span> |
| <span data-ttu-id="1905d-199">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="1905d-199">relativeUrl</span></span> | <span data-ttu-id="1905d-200">Een relatieve URL naar de resource die de gegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="1905d-200">A relative URL to the resource that contains the data.</span></span> <span data-ttu-id="1905d-201">Als het pad niet wordt opgegeven, worden alleen de URL die is opgegeven in de definitie van de gekoppelde service wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1905d-201">When path is not specified, only the URL specified in the linked service definition is used.</span></span> <br><br> <span data-ttu-id="1905d-202">Kan de dynamische-URL, kunt u [Data Factory-functies en systeemvariabelen](data-factory-functions-variables.md), bijvoorbeeld 'relativeUrl': ' $$Text.Format ('/ Mijn/rapport? maand = {0:yyyy}-{0:MM} & fmt csv =', SliceStart) '.</span><span class="sxs-lookup"><span data-stu-id="1905d-202">To construct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), e.g. "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)".</span></span> | <span data-ttu-id="1905d-203">Nee</span><span class="sxs-lookup"><span data-stu-id="1905d-203">No</span></span> |
| <span data-ttu-id="1905d-204">requestMethod</span><span class="sxs-lookup"><span data-stu-id="1905d-204">requestMethod</span></span> | <span data-ttu-id="1905d-205">HTTP-methode.</span><span class="sxs-lookup"><span data-stu-id="1905d-205">Http method.</span></span> <span data-ttu-id="1905d-206">Toegestane waarden zijn **ophalen** of **POST**.</span><span class="sxs-lookup"><span data-stu-id="1905d-206">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="1905d-207">Nee.</span><span class="sxs-lookup"><span data-stu-id="1905d-207">No.</span></span> <span data-ttu-id="1905d-208">Standaard is `GET`.</span><span class="sxs-lookup"><span data-stu-id="1905d-208">Default is `GET`.</span></span> |
| <span data-ttu-id="1905d-209">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="1905d-209">additionalHeaders</span></span> | <span data-ttu-id="1905d-210">Aanvullende HTTP-aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="1905d-210">Additional HTTP request headers.</span></span> | <span data-ttu-id="1905d-211">Nee</span><span class="sxs-lookup"><span data-stu-id="1905d-211">No</span></span> |
| <span data-ttu-id="1905d-212">requestBody</span><span class="sxs-lookup"><span data-stu-id="1905d-212">requestBody</span></span> | <span data-ttu-id="1905d-213">Instantie voor HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="1905d-213">Body for HTTP request.</span></span> | <span data-ttu-id="1905d-214">Nee</span><span class="sxs-lookup"><span data-stu-id="1905d-214">No</span></span> |
| <span data-ttu-id="1905d-215">Indeling</span><span class="sxs-lookup"><span data-stu-id="1905d-215">format</span></span> | <span data-ttu-id="1905d-216">Als u gewoon wilt **gegevens ophalen van HTTP-eindpunt als-is** overslaan zonder deze parseren, deze instellingen.</span><span class="sxs-lookup"><span data-stu-id="1905d-216">If you want to simply **retrieve the data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="1905d-217">Als u de inhoud van het HTTP-antwoord geparseerd tijdens het kopiëren wilt, de volgende indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="1905d-217">If you want to parse the HTTP response content during copy, the following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="1905d-218">Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties.</span><span class="sxs-lookup"><span data-stu-id="1905d-218">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="1905d-219">Nee</span><span class="sxs-lookup"><span data-stu-id="1905d-219">No</span></span> |
| <span data-ttu-id="1905d-220">Compressie</span><span class="sxs-lookup"><span data-stu-id="1905d-220">compression</span></span> | <span data-ttu-id="1905d-221">Geef het type en de compressie van de gegevens.</span><span class="sxs-lookup"><span data-stu-id="1905d-221">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="1905d-222">Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="1905d-222">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="1905d-223">Ondersteunde niveaus: **optimale** en **snelst**.</span><span class="sxs-lookup"><span data-stu-id="1905d-223">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="1905d-224">Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="1905d-224">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="1905d-225">Nee</span><span class="sxs-lookup"><span data-stu-id="1905d-225">No</span></span> |

### <a name="example-using-the-get-default-method"></a><span data-ttu-id="1905d-226">Voorbeeld: met behulp van de methode GET (standaard)</span><span class="sxs-lookup"><span data-stu-id="1905d-226">Example: using the GET (default) method</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

### <a name="example-using-the-post-method"></a><span data-ttu-id="1905d-227">Voorbeeld: via de POST-methode</span><span class="sxs-lookup"><span data-stu-id="1905d-227">Example: using the POST method</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
           "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="1905d-228">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="1905d-228">Copy activity properties</span></span>
<span data-ttu-id="1905d-229">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van activiteiten van de [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="1905d-229">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="1905d-230">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="1905d-230">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="1905d-231">Eigenschappen die beschikbaar zijn in de **typeProperties** sectie van de activiteit aan de andere kant variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="1905d-231">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="1905d-232">Voor de kopieeractiviteit variëren ze, afhankelijk van de typen van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="1905d-232">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="1905d-233">Wanneer de bron is in de kopieerbewerking is momenteel van het type **HttpSource**, de volgende eigenschappen worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="1905d-233">Currently, when the source in copy activity is of type **HttpSource**, the following properties are supported.</span></span>

| <span data-ttu-id="1905d-234">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="1905d-234">Property</span></span> | <span data-ttu-id="1905d-235">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1905d-235">Description</span></span> | <span data-ttu-id="1905d-236">Vereist</span><span class="sxs-lookup"><span data-stu-id="1905d-236">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="1905d-237">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="1905d-237">httpRequestTimeout</span></span> | <span data-ttu-id="1905d-238">De time-out (TimeSpan) voor de HTTP-aanvragen reageert.</span><span class="sxs-lookup"><span data-stu-id="1905d-238">The timeout (TimeSpan) for the HTTP request to get a response.</span></span> <span data-ttu-id="1905d-239">De time-out is reageert niet op de time-out antwoordgegevens lezen.</span><span class="sxs-lookup"><span data-stu-id="1905d-239">It is the timeout to get a response, not the timeout to read response data.</span></span> | <span data-ttu-id="1905d-240">Nee.</span><span class="sxs-lookup"><span data-stu-id="1905d-240">No.</span></span> <span data-ttu-id="1905d-241">Standaardwaarde: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="1905d-241">Default value: 00:01:40</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="1905d-242">Ondersteunde indelingen voor bestands- en compressie</span><span class="sxs-lookup"><span data-stu-id="1905d-242">Supported file and compression formats</span></span>
<span data-ttu-id="1905d-243">Zie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1905d-243">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="1905d-244">JSON-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="1905d-244">JSON examples</span></span>
<span data-ttu-id="1905d-245">Het volgende voorbeeld leveren voorbeeld JSON definities die u kunt een pijplijn maken met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1905d-245">The following example provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="1905d-246">Ze laten zien hoe gegevens van HTTP-bron kopiëren naar Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="1905d-246">They show how to copy data from HTTP source to Azure Blob Storage.</span></span> <span data-ttu-id="1905d-247">Echter, de gegevens kunnen worden gekopieerd **rechtstreeks** uit een van de bronnen aan een van de PUT vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van de Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1905d-247">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-http-source-to-azure-blob-storage"></a><span data-ttu-id="1905d-248">Voorbeeld: Gegevens kopiëren van HTTP-bron naar Azure Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="1905d-248">Example: Copy data from HTTP source to Azure Blob Storage</span></span>
<span data-ttu-id="1905d-249">De Data Factory-oplossing voor dit voorbeeld bevat de volgende Data Factory-entiteiten:</span><span class="sxs-lookup"><span data-stu-id="1905d-249">The Data Factory solution for this sample contains the following Data Factory entities:</span></span>

1. <span data-ttu-id="1905d-250">Een gekoppelde service van het type [HTTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1905d-250">A linked service of type [HTTP](#linked-service-properties).</span></span>
2. <span data-ttu-id="1905d-251">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1905d-251">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="1905d-252">Invoer [gegevensset](data-factory-create-datasets.md) van het type [Http](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1905d-252">An input [dataset](data-factory-create-datasets.md) of type [Http](#dataset-properties).</span></span>
4. <span data-ttu-id="1905d-253">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1905d-253">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="1905d-254">Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [HttpSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1905d-254">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [HttpSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="1905d-255">Het voorbeeld worden gegevens gekopieerd van een HTTP-bron met een Azure-blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="1905d-255">The sample copies data from an HTTP source to an Azure blob every hour.</span></span> <span data-ttu-id="1905d-256">De JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na de voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="1905d-256">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="http-linked-service"></a><span data-ttu-id="1905d-257">Gekoppelde HTTP-service</span><span class="sxs-lookup"><span data-stu-id="1905d-257">HTTP linked service</span></span>
<span data-ttu-id="1905d-258">Dit voorbeeld wordt de HTTP-gekoppelde service met anonieme verificatie.</span><span class="sxs-lookup"><span data-stu-id="1905d-258">This example uses the HTTP linked service with anonymous authentication.</span></span> <span data-ttu-id="1905d-259">Zie [HTTP gekoppelde service](#linked-service-properties) sectie voor verschillende soorten verificatie die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1905d-259">See [HTTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="1905d-260">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="1905d-260">Azure Storage linked service</span></span>

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

### <a name="http-input-dataset"></a><span data-ttu-id="1905d-261">HTTP-invoergegevensset</span><span class="sxs-lookup"><span data-stu-id="1905d-261">HTTP input dataset</span></span>
<span data-ttu-id="1905d-262">Instelling **externe** naar **true** informeert de Data Factory-service dat de dataset extern is aan de gegevensfactory en niet wordt geproduceerd door een activiteit in de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="1905d-262">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}

```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="1905d-263">Azure Blob-uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="1905d-263">Azure Blob output dataset</span></span>

<span data-ttu-id="1905d-264">Gegevens worden geschreven naar een nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="1905d-264">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="1905d-265">Pijplijn met de kopieeractiviteit</span><span class="sxs-lookup"><span data-stu-id="1905d-265">Pipeline with Copy activity</span></span>

<span data-ttu-id="1905d-266">De pijplijn bevat een Kopieeractiviteit die is geconfigureerd voor gebruik van de invoer- en uitvoergegevenssets en elk uur is gepland.</span><span class="sxs-lookup"><span data-stu-id="1905d-266">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="1905d-267">In de pijplijn-JSON-definitie de **bron** type is ingesteld op **HttpSource** en **sink** type is ingesteld op **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="1905d-267">In the pipeline JSON definition, the **source** type is set to **HttpSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="1905d-268">Zie [HttpSource](#copy-activity-properties) voor de lijst met eigenschappen die door de HttpSource ondersteund.</span><span class="sxs-lookup"><span data-stu-id="1905d-268">See [HttpSource](#copy-activity-properties) for the list of properties supported by the HttpSource.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "HttpSourceToAzureBlob",
        "description": "Copy from an HTTP source to an Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "HttpSourceDataInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "HttpSource"
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
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```

> [!NOTE]
> <span data-ttu-id="1905d-269">Zie het toewijzen van kolommen uit de bron-gegevensset naar kolommen uit de dataset sink [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="1905d-269">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="1905d-270">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="1905d-270">Performance and Tuning</span></span>
<span data-ttu-id="1905d-271">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) voor meer informatie over de belangrijkste factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren om te optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="1905d-271">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
