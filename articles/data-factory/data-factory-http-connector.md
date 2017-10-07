---
title: gegevens van de bron van een HTTP - Azure aaaMove | Microsoft Docs
description: Meer informatie over hoe toomove uit een on-premises of in een cloud HTTP gegevensbron met behulp van Azure Data Factory.
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
ms.openlocfilehash: e39b9cbff870aef4be91938cacff39a2fd12d64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a><span data-ttu-id="b76dc-103">Gegevens verplaatsen van een HTTP-bron met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="b76dc-103">Move data from an HTTP source using Azure Data Factory</span></span>
<span data-ttu-id="b76dc-104">In dit artikel bevat een overzicht van hoe toouse hello Kopieeractiviteit in Azure Data Factory toomove gegevens uit een on-premises/cloudtoepassing HTTP-eindpunt tooa gegevensarchief sink ondersteund.</span><span class="sxs-lookup"><span data-stu-id="b76dc-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises/cloud HTTP endpoint tooa supported sink data store.</span></span> <span data-ttu-id="b76dc-105">In dit artikel is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel met daarin een algemeen overzicht van de verplaatsing van gegevens kopiëren-activiteit en Hallo lijst met gegevensarchieven ondersteund als bronnen/Put.</span><span class="sxs-lookup"><span data-stu-id="b76dc-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="b76dc-106">Data factory momenteel ondersteunt alleen het verplaatsen van gegevens van een HTTP tooother gegevensarchieven bron, maar niet verplaatsen van gegevens van andere gegevens worden opgeslagen tooan HTTP bestemming.</span><span class="sxs-lookup"><span data-stu-id="b76dc-106">Data factory currently supports only moving data from an HTTP source tooother data stores, but not moving data from other data stores tooan HTTP destination.</span></span>

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="b76dc-107">Ondersteunde scenario's en verificatietypen</span><span class="sxs-lookup"><span data-stu-id="b76dc-107">Supported scenarios and authentication types</span></span>
<span data-ttu-id="b76dc-108">U kunt deze gegevens HTTP connector tooretrieve uit **zowel cloud als on-premises HTTP/s-eindpunt** met behulp van HTTP **ophalen** of **POST** methode.</span><span class="sxs-lookup"><span data-stu-id="b76dc-108">You can use this HTTP connector tooretrieve data from **both cloud and on-premises HTTP/s endpoint** by using HTTP **GET** or **POST** method.</span></span> <span data-ttu-id="b76dc-109">Hallo verificatietypen volgende worden ondersteund: **anoniem**, **Basic**, **Digest**, **Windows**, en  **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="b76dc-109">hello following authentication types are supported: **Anonymous**, **Basic**, **Digest**, **Windows**, and **ClientCertificate**.</span></span> <span data-ttu-id="b76dc-110">Houd er rekening mee Hallo verschil tussen deze connector en Hallo [Web tabel connector](data-factory-web-table-connector.md) is: laatste Hallo gebruikte tooextract tabelinhoud van HTML-webpagina is.</span><span class="sxs-lookup"><span data-stu-id="b76dc-110">Note hello difference between this connector and hello [Web table connector](data-factory-web-table-connector.md) is: hello latter is used tooextract table content from web HTML page.</span></span>

<span data-ttu-id="b76dc-111">Bij het kopiëren van gegevens uit een lokale HTTP-eindpunt, moet u een Data Management Gateway installeren in Hallo lokale omgeving/Azure VM.</span><span class="sxs-lookup"><span data-stu-id="b76dc-111">When copying data from an on-premises HTTP endpoint, you need install a Data Management Gateway in hello on-premises environment/Azure VM.</span></span> <span data-ttu-id="b76dc-112">Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn artikel over Data Management Gateway en stapsgewijze instructies over het instellen van Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="b76dc-112">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="b76dc-113">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="b76dc-113">Getting started</span></span>
<span data-ttu-id="b76dc-114">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens van een HTTP-bron verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="b76dc-114">You can create a pipeline with a copy activity that moves data from an HTTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="b76dc-115">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="b76dc-115">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="b76dc-116">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="b76dc-116">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

- <span data-ttu-id="b76dc-117">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="b76dc-117">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="b76dc-118">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="b76dc-118">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> <span data-ttu-id="b76dc-119">Zie voor JSON-toocopy gegevens uit de HTTP-bron tooAzure Blob Storage voorbeelden, [JSON voorbeelden](#json-examples) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="b76dc-119">For JSON samples toocopy data from HTTP source tooAzure Blob Storage, see [JSON examples](#json-examples) section of this articles.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="b76dc-120">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="b76dc-120">Linked service properties</span></span>
<span data-ttu-id="b76dc-121">Hallo volgende tabel biedt een beschrijving voor de JSON-elementen specifieke tooHTTP gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="b76dc-121">hello following table provides description for JSON elements specific tooHTTP linked service.</span></span>

| <span data-ttu-id="b76dc-122">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="b76dc-122">Property</span></span> | <span data-ttu-id="b76dc-123">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b76dc-123">Description</span></span> | <span data-ttu-id="b76dc-124">Vereist</span><span class="sxs-lookup"><span data-stu-id="b76dc-124">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b76dc-125">type</span><span class="sxs-lookup"><span data-stu-id="b76dc-125">type</span></span> | <span data-ttu-id="b76dc-126">Hallo type eigenschap moet worden ingesteld op: `Http`.</span><span class="sxs-lookup"><span data-stu-id="b76dc-126">hello type property must be set to: `Http`.</span></span> | <span data-ttu-id="b76dc-127">Ja</span><span class="sxs-lookup"><span data-stu-id="b76dc-127">Yes</span></span> |
| <span data-ttu-id="b76dc-128">URL</span><span class="sxs-lookup"><span data-stu-id="b76dc-128">url</span></span> | <span data-ttu-id="b76dc-129">Basis-URL toohello webserver</span><span class="sxs-lookup"><span data-stu-id="b76dc-129">Base URL toohello Web Server</span></span> | <span data-ttu-id="b76dc-130">Ja</span><span class="sxs-lookup"><span data-stu-id="b76dc-130">Yes</span></span> |
| <span data-ttu-id="b76dc-131">authenticationType</span><span class="sxs-lookup"><span data-stu-id="b76dc-131">authenticationType</span></span> | <span data-ttu-id="b76dc-132">Hiermee geeft u het verificatietype Hallo.</span><span class="sxs-lookup"><span data-stu-id="b76dc-132">Specifies hello authentication type.</span></span> <span data-ttu-id="b76dc-133">Toegestane waarden zijn: **anoniem**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="b76dc-133">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="b76dc-134">Raadpleeg toosections onder deze tabel over meer eigenschappen en voorbeelden van JSON respectievelijk voor deze verificatietypen.</span><span class="sxs-lookup"><span data-stu-id="b76dc-134">Refer toosections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="b76dc-135">Ja</span><span class="sxs-lookup"><span data-stu-id="b76dc-135">Yes</span></span> |
| <span data-ttu-id="b76dc-136">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="b76dc-136">enableServerCertificateValidation</span></span> | <span data-ttu-id="b76dc-137">Opgeven of tooenable server SSL certificaatcontrole als bron is een HTTPS-webserver</span><span class="sxs-lookup"><span data-stu-id="b76dc-137">Specify whether tooenable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="b76dc-138">Nee, de standaardwaarde is true</span><span class="sxs-lookup"><span data-stu-id="b76dc-138">No, default is true</span></span> |
| <span data-ttu-id="b76dc-139">gatewayName</span><span class="sxs-lookup"><span data-stu-id="b76dc-139">gatewayName</span></span> | <span data-ttu-id="b76dc-140">Naam van Hallo Data Management Gateway tooconnect tooan lokale HTTP-bron.</span><span class="sxs-lookup"><span data-stu-id="b76dc-140">Name of hello Data Management Gateway tooconnect tooan on-premises HTTP source.</span></span> | <span data-ttu-id="b76dc-141">Ja als u gegevens kopiëren van een lokale HTTP-bron.</span><span class="sxs-lookup"><span data-stu-id="b76dc-141">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="b76dc-142">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="b76dc-142">encryptedCredential</span></span> | <span data-ttu-id="b76dc-143">Versleutelde referentie tooaccess Hallo HTTP-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="b76dc-143">Encrypted credential tooaccess hello HTTP endpoint.</span></span> <span data-ttu-id="b76dc-144">Automatisch wordt gegenereerd wanneer u Hallo verificatiegegevens in kopiëren wizard of Hallo ClickOnce pop-up dialoogvenster configureert.</span><span class="sxs-lookup"><span data-stu-id="b76dc-144">Auto-generated when you configure hello authentication information in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="b76dc-145">Nee.</span><span class="sxs-lookup"><span data-stu-id="b76dc-145">No.</span></span> <span data-ttu-id="b76dc-146">Alleen van toepassing wanneer het kopiëren van gegevens uit een lokale HTTP-server.</span><span class="sxs-lookup"><span data-stu-id="b76dc-146">Apply only when copying data from an on-premises HTTP server.</span></span> |

<span data-ttu-id="b76dc-147">Zie [gegevens verplaatsen tussen lokale bronnen en Hallo cloud met Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) voor meer informatie over het instellen van referenties voor on-premises HTTP connector-gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="b76dc-147">See [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for details about setting credentials for on-premises HTTP connector data source.</span></span>

### <a name="using-basic-digest-or-windows-authentication"></a><span data-ttu-id="b76dc-148">Met behulp van basisverificatie, verificatiesamenvatting of Windows-verificatie</span><span class="sxs-lookup"><span data-stu-id="b76dc-148">Using Basic, Digest, or Windows authentication</span></span>

<span data-ttu-id="b76dc-149">Stel `authenticationType` als `Basic`, `Digest`, of `Windows`, en geef de volgende eigenschappen afgezien van HTTP-connector algemene werden geïntroduceerd hierboven Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="b76dc-149">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="b76dc-150">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="b76dc-150">Property</span></span> | <span data-ttu-id="b76dc-151">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b76dc-151">Description</span></span> | <span data-ttu-id="b76dc-152">Vereist</span><span class="sxs-lookup"><span data-stu-id="b76dc-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b76dc-153">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="b76dc-153">username</span></span> | <span data-ttu-id="b76dc-154">Gebruikersnaam tooaccess Hallo HTTP-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="b76dc-154">Username tooaccess hello HTTP endpoint.</span></span> | <span data-ttu-id="b76dc-155">Ja</span><span class="sxs-lookup"><span data-stu-id="b76dc-155">Yes</span></span> |
| <span data-ttu-id="b76dc-156">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="b76dc-156">password</span></span> | <span data-ttu-id="b76dc-157">Wachtwoord voor gebruiker hello (gebruikersnaam).</span><span class="sxs-lookup"><span data-stu-id="b76dc-157">Password for hello user (username).</span></span> | <span data-ttu-id="b76dc-158">Ja</span><span class="sxs-lookup"><span data-stu-id="b76dc-158">Yes</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="b76dc-159">Voorbeeld: met behulp van basisverificatie, verificatiesamenvatting of Windows-verificatie</span><span class="sxs-lookup"><span data-stu-id="b76dc-159">Example: using Basic, Digest, or Windows authentication</span></span>

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

### <a name="using-clientcertificate-authentication"></a><span data-ttu-id="b76dc-160">ClientCertificate-verificatie</span><span class="sxs-lookup"><span data-stu-id="b76dc-160">Using ClientCertificate authentication</span></span>

<span data-ttu-id="b76dc-161">Basisverificatie toouse ingesteld `authenticationType` als `ClientCertificate`, en geef de volgende eigenschappen afgezien van HTTP-connector algemene werden geïntroduceerd hierboven Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="b76dc-161">toouse basic authentication, set `authenticationType` as `ClientCertificate`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="b76dc-162">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="b76dc-162">Property</span></span> | <span data-ttu-id="b76dc-163">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b76dc-163">Description</span></span> | <span data-ttu-id="b76dc-164">Vereist</span><span class="sxs-lookup"><span data-stu-id="b76dc-164">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b76dc-165">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="b76dc-165">embeddedCertData</span></span> | <span data-ttu-id="b76dc-166">Hallo Base64-gecodeerde inhoud van de binaire gegevens van Hallo Personal Information Exchange (PFX)-bestand.</span><span class="sxs-lookup"><span data-stu-id="b76dc-166">hello Base64-encoded contents of binary data of hello Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="b76dc-167">Geef beide Hallo `embeddedCertData` of `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="b76dc-167">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="b76dc-168">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="b76dc-168">certThumbprint</span></span> | <span data-ttu-id="b76dc-169">Hallo vingerafdruk van certificaat Hallo die is geïnstalleerd op de gatewaycomputer certificaatarchief.</span><span class="sxs-lookup"><span data-stu-id="b76dc-169">hello thumbprint of hello certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="b76dc-170">Alleen van toepassing wanneer het kopiëren van gegevens van een lokale HTTP-bron.</span><span class="sxs-lookup"><span data-stu-id="b76dc-170">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="b76dc-171">Geef beide Hallo `embeddedCertData` of `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="b76dc-171">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="b76dc-172">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="b76dc-172">password</span></span> | <span data-ttu-id="b76dc-173">Het wachtwoord die zijn gekoppeld aan het Hallo-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b76dc-173">Password associated with hello certificate.</span></span> | <span data-ttu-id="b76dc-174">Nee</span><span class="sxs-lookup"><span data-stu-id="b76dc-174">No</span></span> |

<span data-ttu-id="b76dc-175">Als u `certThumbprint` voor verificatie en Hallo-certificaat is geïnstalleerd in het persoonlijke archief van de lokale computer Hallo hello, moet u toogrant Hallo leesmachtiging toohello gateway-service:</span><span class="sxs-lookup"><span data-stu-id="b76dc-175">If you use `certThumbprint` for authentication and hello certificate is installed in hello personal store of hello local computer, you need toogrant hello read permission toohello gateway service:</span></span>

1. <span data-ttu-id="b76dc-176">Start Microsoft Management Console (MMC).</span><span class="sxs-lookup"><span data-stu-id="b76dc-176">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="b76dc-177">Hallo toevoegen **certificaten** -module die Hallo doelen **lokale Computer**.</span><span class="sxs-lookup"><span data-stu-id="b76dc-177">Add hello **Certificates** snap-in that targets hello **Local Computer**.</span></span>
2. <span data-ttu-id="b76dc-178">Vouw **certificaten**, **persoonlijke**, en klik op **certificaten**.</span><span class="sxs-lookup"><span data-stu-id="b76dc-178">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="b76dc-179">Met de rechtermuisknop op het Hallo-certificaat uit het persoonlijke archief Hallo en selecteer **alle taken**->**persoonlijke sleutels beheren...**</span><span class="sxs-lookup"><span data-stu-id="b76dc-179">Right-click hello certificate from hello personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="b76dc-180">Op Hallo **beveiliging** tabblad, waaronder Data Management Gateway Host Service wordt uitgevoerd met Hallo leestoegang toohello certificaat Hallo-gebruikersaccount toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b76dc-180">On hello **Security** tab, add hello user account under which Data Management Gateway Host Service is running with hello read access toohello certificate.</span></span>  

#### <a name="example-using-client-certificate"></a><span data-ttu-id="b76dc-181">Voorbeeld: met behulp van clientcertificaat</span><span class="sxs-lookup"><span data-stu-id="b76dc-181">Example: using client certificate</span></span>
<span data-ttu-id="b76dc-182">Deze gekoppelde service wordt uw data factory tooan lokale HTTP-webserver.</span><span class="sxs-lookup"><span data-stu-id="b76dc-182">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="b76dc-183">Dit maakt gebruik van een clientcertificaat dat is geïnstalleerd op machine Hallo met Data Management Gateway is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b76dc-183">It uses a client certificate that is installed on hello machine with Data Management Gateway installed.</span></span>

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

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="b76dc-184">Voorbeeld: clientcertificaat gebruiken in een bestand</span><span class="sxs-lookup"><span data-stu-id="b76dc-184">Example: using client certificate in a file</span></span>
<span data-ttu-id="b76dc-185">Deze gekoppelde service wordt uw data factory tooan lokale HTTP-webserver.</span><span class="sxs-lookup"><span data-stu-id="b76dc-185">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="b76dc-186">Een certificaatbestand op Hallo machine wordt met Data Management Gateway is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b76dc-186">It uses a client certificate file on hello machine with Data Management Gateway installed.</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="b76dc-187">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="b76dc-187">Dataset properties</span></span>
<span data-ttu-id="b76dc-188">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="b76dc-188">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="b76dc-189">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="b76dc-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="b76dc-190">Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="b76dc-190">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="b76dc-191">Hallo typeProperties sectie voor de gegevensset van het type **Http** heeft de volgende eigenschappen Hallo</span><span class="sxs-lookup"><span data-stu-id="b76dc-191">hello typeProperties section for dataset of type **Http** has hello following properties</span></span>

| <span data-ttu-id="b76dc-192">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="b76dc-192">Property</span></span> | <span data-ttu-id="b76dc-193">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b76dc-193">Description</span></span> | <span data-ttu-id="b76dc-194">Vereist</span><span class="sxs-lookup"><span data-stu-id="b76dc-194">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="b76dc-195">type</span><span class="sxs-lookup"><span data-stu-id="b76dc-195">type</span></span> | <span data-ttu-id="b76dc-196">Hallo Hallo gegevensset type opgegeven.</span><span class="sxs-lookup"><span data-stu-id="b76dc-196">Specified hello type of hello dataset.</span></span> <span data-ttu-id="b76dc-197">te moet worden ingesteld`Http`.</span><span class="sxs-lookup"><span data-stu-id="b76dc-197">must be set too`Http`.</span></span> | <span data-ttu-id="b76dc-198">Ja</span><span class="sxs-lookup"><span data-stu-id="b76dc-198">Yes</span></span> |
| <span data-ttu-id="b76dc-199">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="b76dc-199">relativeUrl</span></span> | <span data-ttu-id="b76dc-200">Een relatieve URL toohello-bron die Hallo gegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="b76dc-200">A relative URL toohello resource that contains hello data.</span></span> <span data-ttu-id="b76dc-201">Wanneer het pad niet wordt opgegeven, wordt alleen Hallo URL die is opgegeven in de servicedefinitie Hallo gekoppeld gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b76dc-201">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> <br><br> <span data-ttu-id="b76dc-202">dynamische tooconstruct-URL, kunt u [Data Factory-functies en systeemvariabelen](data-factory-functions-variables.md), bijvoorbeeld 'relativeUrl': ' $$Text.Format ('/ Mijn/rapport? maand = {0:yyyy}-{0:MM} & fmt csv =', SliceStart) '.</span><span class="sxs-lookup"><span data-stu-id="b76dc-202">tooconstruct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), e.g. "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)".</span></span> | <span data-ttu-id="b76dc-203">Nee</span><span class="sxs-lookup"><span data-stu-id="b76dc-203">No</span></span> |
| <span data-ttu-id="b76dc-204">requestMethod</span><span class="sxs-lookup"><span data-stu-id="b76dc-204">requestMethod</span></span> | <span data-ttu-id="b76dc-205">HTTP-methode.</span><span class="sxs-lookup"><span data-stu-id="b76dc-205">Http method.</span></span> <span data-ttu-id="b76dc-206">Toegestane waarden zijn **ophalen** of **POST**.</span><span class="sxs-lookup"><span data-stu-id="b76dc-206">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="b76dc-207">Nee.</span><span class="sxs-lookup"><span data-stu-id="b76dc-207">No.</span></span> <span data-ttu-id="b76dc-208">Standaard is `GET`.</span><span class="sxs-lookup"><span data-stu-id="b76dc-208">Default is `GET`.</span></span> |
| <span data-ttu-id="b76dc-209">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="b76dc-209">additionalHeaders</span></span> | <span data-ttu-id="b76dc-210">Aanvullende HTTP-aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="b76dc-210">Additional HTTP request headers.</span></span> | <span data-ttu-id="b76dc-211">Nee</span><span class="sxs-lookup"><span data-stu-id="b76dc-211">No</span></span> |
| <span data-ttu-id="b76dc-212">requestBody</span><span class="sxs-lookup"><span data-stu-id="b76dc-212">requestBody</span></span> | <span data-ttu-id="b76dc-213">Instantie voor HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="b76dc-213">Body for HTTP request.</span></span> | <span data-ttu-id="b76dc-214">Nee</span><span class="sxs-lookup"><span data-stu-id="b76dc-214">No</span></span> |
| <span data-ttu-id="b76dc-215">Indeling</span><span class="sxs-lookup"><span data-stu-id="b76dc-215">format</span></span> | <span data-ttu-id="b76dc-216">Als u wilt dat toosimply **Hallo-gegevens ophalen van HTTP-eindpunt als-is** overslaan zonder deze parseren, deze instellingen.</span><span class="sxs-lookup"><span data-stu-id="b76dc-216">If you want toosimply **retrieve hello data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="b76dc-217">Als u tooparse Hallo HTTP-antwoord inhoud tijdens het kopiëren wilt, Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="b76dc-217">If you want tooparse hello HTTP response content during copy, hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="b76dc-218">Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties.</span><span class="sxs-lookup"><span data-stu-id="b76dc-218">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="b76dc-219">Nee</span><span class="sxs-lookup"><span data-stu-id="b76dc-219">No</span></span> |
| <span data-ttu-id="b76dc-220">Compressie</span><span class="sxs-lookup"><span data-stu-id="b76dc-220">compression</span></span> | <span data-ttu-id="b76dc-221">Hallo-type en compressieniveau voor Hallo gegevens opgeven.</span><span class="sxs-lookup"><span data-stu-id="b76dc-221">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="b76dc-222">Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="b76dc-222">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="b76dc-223">Ondersteunde niveaus: **optimale** en **snelst**.</span><span class="sxs-lookup"><span data-stu-id="b76dc-223">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="b76dc-224">Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="b76dc-224">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="b76dc-225">Nee</span><span class="sxs-lookup"><span data-stu-id="b76dc-225">No</span></span> |

### <a name="example-using-hello-get-default-method"></a><span data-ttu-id="b76dc-226">Voorbeeld: via Hallo GET (standaard)-methode</span><span class="sxs-lookup"><span data-stu-id="b76dc-226">Example: using hello GET (default) method</span></span>

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

### <a name="example-using-hello-post-method"></a><span data-ttu-id="b76dc-227">Voorbeeld: via Hallo POST-methode</span><span class="sxs-lookup"><span data-stu-id="b76dc-227">Example: using hello POST method</span></span>

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

## <a name="copy-activity-properties"></a><span data-ttu-id="b76dc-228">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="b76dc-228">Copy activity properties</span></span>
<span data-ttu-id="b76dc-229">Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="b76dc-229">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="b76dc-230">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="b76dc-230">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="b76dc-231">Eigenschappen die beschikbaar zijn in Hallo **typeProperties** sectie Hallo-activiteit op Hallo daarentegen variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="b76dc-231">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="b76dc-232">Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="b76dc-232">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="b76dc-233">Op dit moment wanneer Hallo-bron in de kopieerbewerking is van het type **HttpSource**, Hallo volgende eigenschappen worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="b76dc-233">Currently, when hello source in copy activity is of type **HttpSource**, hello following properties are supported.</span></span>

| <span data-ttu-id="b76dc-234">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="b76dc-234">Property</span></span> | <span data-ttu-id="b76dc-235">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b76dc-235">Description</span></span> | <span data-ttu-id="b76dc-236">Vereist</span><span class="sxs-lookup"><span data-stu-id="b76dc-236">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="b76dc-237">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="b76dc-237">httpRequestTimeout</span></span> | <span data-ttu-id="b76dc-238">Hallo-out (TimeSpan) voor Hallo HTTP-aanvraag tooget een antwoord.</span><span class="sxs-lookup"><span data-stu-id="b76dc-238">hello timeout (TimeSpan) for hello HTTP request tooget a response.</span></span> <span data-ttu-id="b76dc-239">Hallo time-out tooget een antwoord niet Hallo time-out tooread antwoordgegevens is.</span><span class="sxs-lookup"><span data-stu-id="b76dc-239">It is hello timeout tooget a response, not hello timeout tooread response data.</span></span> | <span data-ttu-id="b76dc-240">Nee.</span><span class="sxs-lookup"><span data-stu-id="b76dc-240">No.</span></span> <span data-ttu-id="b76dc-241">Standaardwaarde: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="b76dc-241">Default value: 00:01:40</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="b76dc-242">Ondersteunde indelingen voor bestands- en compressie</span><span class="sxs-lookup"><span data-stu-id="b76dc-242">Supported file and compression formats</span></span>
<span data-ttu-id="b76dc-243">Zie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b76dc-243">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="b76dc-244">JSON-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="b76dc-244">JSON examples</span></span>
<span data-ttu-id="b76dc-245">Hallo volgt voorbeeld JSON definities bieden dat u een pijplijn toocreate gebruiken met behulp van kunt [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b76dc-245">hello following example provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="b76dc-246">Ze geven weer hoe toocopy van HTTP gegevensbron tooAzure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="b76dc-246">They show how toocopy data from HTTP source tooAzure Blob Storage.</span></span> <span data-ttu-id="b76dc-247">Echter gegevens kunnen worden gekopieerd **rechtstreeks** uit een van de bronnen tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b76dc-247">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-http-source-tooazure-blob-storage"></a><span data-ttu-id="b76dc-248">Voorbeeld: Gegevens kopiëren van de HTTP-bron tooAzure Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="b76dc-248">Example: Copy data from HTTP source tooAzure Blob Storage</span></span>
<span data-ttu-id="b76dc-249">Hallo Data Factory-oplossing voor dit voorbeeld bevat Hallo Data Factory-entiteiten te volgen:</span><span class="sxs-lookup"><span data-stu-id="b76dc-249">hello Data Factory solution for this sample contains hello following Data Factory entities:</span></span>

1. <span data-ttu-id="b76dc-250">Een gekoppelde service van het type [HTTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b76dc-250">A linked service of type [HTTP](#linked-service-properties).</span></span>
2. <span data-ttu-id="b76dc-251">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b76dc-251">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="b76dc-252">Invoer [gegevensset](data-factory-create-datasets.md) van het type [Http](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b76dc-252">An input [dataset](data-factory-create-datasets.md) of type [Http](#dataset-properties).</span></span>
4. <span data-ttu-id="b76dc-253">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b76dc-253">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="b76dc-254">Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [HttpSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="b76dc-254">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [HttpSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="b76dc-255">Hallo-voorbeeld worden gegevens gekopieerd van een HTTP-bron tooan Azure blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="b76dc-255">hello sample copies data from an HTTP source tooan Azure blob every hour.</span></span> <span data-ttu-id="b76dc-256">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="b76dc-256">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="http-linked-service"></a><span data-ttu-id="b76dc-257">Gekoppelde HTTP-service</span><span class="sxs-lookup"><span data-stu-id="b76dc-257">HTTP linked service</span></span>
<span data-ttu-id="b76dc-258">In dit voorbeeld maakt gebruik van HTTP Hallo gekoppelde service met anonieme verificatie.</span><span class="sxs-lookup"><span data-stu-id="b76dc-258">This example uses hello HTTP linked service with anonymous authentication.</span></span> <span data-ttu-id="b76dc-259">Zie [HTTP gekoppelde service](#linked-service-properties) sectie voor verschillende soorten verificatie die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b76dc-259">See [HTTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="b76dc-260">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="b76dc-260">Azure Storage linked service</span></span>

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

### <a name="http-input-dataset"></a><span data-ttu-id="b76dc-261">HTTP-invoergegevensset</span><span class="sxs-lookup"><span data-stu-id="b76dc-261">HTTP input dataset</span></span>
<span data-ttu-id="b76dc-262">Instelling **externe** te**true** informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="b76dc-262">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="b76dc-263">Azure Blob-uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="b76dc-263">Azure Blob output dataset</span></span>

<span data-ttu-id="b76dc-264">Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="b76dc-264">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

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

### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="b76dc-265">Pijplijn met de kopieeractiviteit</span><span class="sxs-lookup"><span data-stu-id="b76dc-265">Pipeline with Copy activity</span></span>

<span data-ttu-id="b76dc-266">Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="b76dc-266">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="b76dc-267">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**HttpSource** en **sink** type is ingesteld, te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="b76dc-267">In hello pipeline JSON definition, hello **source** type is set too**HttpSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="b76dc-268">Zie [HttpSource](#copy-activity-properties) voor Hallo lijst met eigenschappen die ondersteund worden door Hallo HttpSource.</span><span class="sxs-lookup"><span data-stu-id="b76dc-268">See [HttpSource](#copy-activity-properties) for hello list of properties supported by hello HttpSource.</span></span>

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
        "description": "Copy from an HTTP source tooan Azure blob",
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
> <span data-ttu-id="b76dc-269">toomap kolommen uit de bron gegevensset toocolumns uit sink gegevensset, Zie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="b76dc-269">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="b76dc-270">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="b76dc-270">Performance and Tuning</span></span>
<span data-ttu-id="b76dc-271">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.</span><span class="sxs-lookup"><span data-stu-id="b76dc-271">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
