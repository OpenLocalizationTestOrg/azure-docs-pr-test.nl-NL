---
title: aaaMove-gegevens van de SFTP-server met behulp van Azure Data Factory | Microsoft Docs
description: Meer informatie over het toomove gegevens uit een on-premises of een cloud SFTP-server met behulp van Azure Data Factory.
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
ms.date: 06/05/2017
ms.author: jingwang
ms.openlocfilehash: b976289e2c1b1899634bb5565b375499077fa554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-sftp-server-using-azure-data-factory"></a><span data-ttu-id="d71f1-103">Gegevens verplaatsen van een SFTP-server met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d71f1-103">Move data from an SFTP server using Azure Data Factory</span></span>
<span data-ttu-id="d71f1-104">In dit artikel bevat een overzicht van hoe toouse hello Kopieeractiviteit in Azure Data Factory toomove gegevens uit een on-premises/cloudtoepassing SFTP server tooa gegevensarchief sink ondersteund.</span><span class="sxs-lookup"><span data-stu-id="d71f1-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises/cloud SFTP server tooa supported sink data store.</span></span> <span data-ttu-id="d71f1-105">In dit artikel is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel met daarin een algemeen overzicht van de verplaatsing van gegevens kopiëren-activiteit en Hallo lijst met gegevensarchieven ondersteund als bronnen/Put.</span><span class="sxs-lookup"><span data-stu-id="d71f1-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="d71f1-106">Data factory ondersteunt momenteel alleen verplaatsen van gegevens uit een SFTP server tooother-gegevens worden opgeslagen, maar niet voor het verplaatsen van gegevens van andere gegevens worden opgeslagen tooan SFTP-server.</span><span class="sxs-lookup"><span data-stu-id="d71f1-106">Data factory currently supports only moving data from an SFTP server tooother data stores, but not for moving data from other data stores tooan SFTP server.</span></span> <span data-ttu-id="d71f1-107">Deze ondersteuning biedt voor zowel on-premises en in de cloud SFTP-servers.</span><span class="sxs-lookup"><span data-stu-id="d71f1-107">It supports both on-premises and cloud SFTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="d71f1-108">Kopieeractiviteit worden Hallo-bronbestand niet verwijderd nadat het is gekopieerde toohello bestemming.</span><span class="sxs-lookup"><span data-stu-id="d71f1-108">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="d71f1-109">Als u toodelete Hallo-bronbestand na een geslaagde kopie moet, maakt u een aangepaste activiteit toodelete Hallo-bestand en Hallo activiteit in de pijplijn hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d71f1-109">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="d71f1-110">Ondersteunde scenario's en verificatietypen</span><span class="sxs-lookup"><span data-stu-id="d71f1-110">Supported scenarios and authentication types</span></span>
<span data-ttu-id="d71f1-111">U kunt deze gegevens SFTP connector toocopy uit **zowel cloud SFTP-servers en on-premises SFTP-servers**.</span><span class="sxs-lookup"><span data-stu-id="d71f1-111">You can use this SFTP connector toocopy data from **both cloud SFTP servers and on-premises SFTP servers**.</span></span> <span data-ttu-id="d71f1-112">**Basic** en **SshPublicKey** authenticatietypen worden ondersteund bij het verbinden van toohello SFTP-server.</span><span class="sxs-lookup"><span data-stu-id="d71f1-112">**Basic** and **SshPublicKey** authentication types are supported when connecting toohello SFTP server.</span></span>

<span data-ttu-id="d71f1-113">Als u gegevens uit een on-premises SFTP-server, moet u een Data Management Gateway installeren in Hallo lokale omgeving/Azure VM.</span><span class="sxs-lookup"><span data-stu-id="d71f1-113">When copying data from an on-premises SFTP server, you need install a Data Management Gateway in hello on-premises environment/Azure VM.</span></span> <span data-ttu-id="d71f1-114">Zie [Data Management Gateway](data-factory-data-management-gateway.md) voor meer informatie over het Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="d71f1-114">See [Data Management Gateway](data-factory-data-management-gateway.md) for details on hello gateway.</span></span> <span data-ttu-id="d71f1-115">Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor stapsgewijze instructies voor het Hallo-gateway instellen en gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d71f1-115">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway and using it.</span></span>

## <a name="getting-started"></a><span data-ttu-id="d71f1-116">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="d71f1-116">Getting started</span></span>
<span data-ttu-id="d71f1-117">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit een bron SFTP verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="d71f1-117">You can create a pipeline with a copy activity that moves data from an SFTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="d71f1-118">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="d71f1-118">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="d71f1-119">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="d71f1-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

- <span data-ttu-id="d71f1-120">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="d71f1-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="d71f1-121">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="d71f1-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> <span data-ttu-id="d71f1-122">Zie voor JSON-toocopy gegevens van SFTP server tooAzure Blob Storage voorbeelden, [JSON-voorbeeld: gegevens kopiëren van SFTP server tooAzure blob](#json-example-copy-data-from-sftp-server-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="d71f1-122">For JSON samples toocopy data from SFTP server tooAzure Blob Storage, see [JSON Example: Copy data from SFTP server tooAzure blob](#json-example-copy-data-from-sftp-server-to-azure-blob) section of this article.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d71f1-123">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="d71f1-123">Linked service properties</span></span>
<span data-ttu-id="d71f1-124">Hallo volgende tabel biedt een beschrijving voor de JSON-elementen specifieke tooFTP gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="d71f1-124">hello following table provides description for JSON elements specific tooFTP linked service.</span></span>

| <span data-ttu-id="d71f1-125">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="d71f1-125">Property</span></span> | <span data-ttu-id="d71f1-126">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d71f1-126">Description</span></span> | <span data-ttu-id="d71f1-127">Vereist</span><span class="sxs-lookup"><span data-stu-id="d71f1-127">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d71f1-128">type</span><span class="sxs-lookup"><span data-stu-id="d71f1-128">type</span></span> | <span data-ttu-id="d71f1-129">de eigenschap type Hello te moet worden ingesteld`Sftp`.</span><span class="sxs-lookup"><span data-stu-id="d71f1-129">hello type property must be set too`Sftp`.</span></span> |<span data-ttu-id="d71f1-130">Ja</span><span class="sxs-lookup"><span data-stu-id="d71f1-130">Yes</span></span> |
| <span data-ttu-id="d71f1-131">host</span><span class="sxs-lookup"><span data-stu-id="d71f1-131">host</span></span> | <span data-ttu-id="d71f1-132">Naam of IP-adres van Hallo SFTP-server.</span><span class="sxs-lookup"><span data-stu-id="d71f1-132">Name or IP address of hello SFTP server.</span></span> |<span data-ttu-id="d71f1-133">Ja</span><span class="sxs-lookup"><span data-stu-id="d71f1-133">Yes</span></span> |
| <span data-ttu-id="d71f1-134">poort</span><span class="sxs-lookup"><span data-stu-id="d71f1-134">port</span></span> |<span data-ttu-id="d71f1-135">De poort op welke Hallo SFTP-server luistert.</span><span class="sxs-lookup"><span data-stu-id="d71f1-135">Port on which hello SFTP server is listening.</span></span> <span data-ttu-id="d71f1-136">de standaardwaarde Hallo is: 21</span><span class="sxs-lookup"><span data-stu-id="d71f1-136">hello default value is: 21</span></span> |<span data-ttu-id="d71f1-137">Nee</span><span class="sxs-lookup"><span data-stu-id="d71f1-137">No</span></span> |
| <span data-ttu-id="d71f1-138">authenticationType</span><span class="sxs-lookup"><span data-stu-id="d71f1-138">authenticationType</span></span> |<span data-ttu-id="d71f1-139">Geef het verificatietype.</span><span class="sxs-lookup"><span data-stu-id="d71f1-139">Specify authentication type.</span></span> <span data-ttu-id="d71f1-140">Toegestane waarden: **Basic**, **SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="d71f1-140">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="d71f1-141">Raadpleeg te[Using basisverificatie](#using-basic-authentication) en [met behulp van SSH openbare-sleutelauthenticatie](#using-ssh-public-key-authentication) respectievelijk secties over meer eigenschappen en voorbeelden van JSON.</span><span class="sxs-lookup"><span data-stu-id="d71f1-141">Refer too[Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="d71f1-142">Ja</span><span class="sxs-lookup"><span data-stu-id="d71f1-142">Yes</span></span> |
| <span data-ttu-id="d71f1-143">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="d71f1-143">skipHostKeyValidation</span></span> | <span data-ttu-id="d71f1-144">Geef op of tooskip sleutel validatie hosten.</span><span class="sxs-lookup"><span data-stu-id="d71f1-144">Specify whether tooskip host key validation.</span></span> | <span data-ttu-id="d71f1-145">Nee.</span><span class="sxs-lookup"><span data-stu-id="d71f1-145">No.</span></span> <span data-ttu-id="d71f1-146">standaardwaarde Hallo: false</span><span class="sxs-lookup"><span data-stu-id="d71f1-146">hello default value: false</span></span> |
| <span data-ttu-id="d71f1-147">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="d71f1-147">hostKeyFingerprint</span></span> | <span data-ttu-id="d71f1-148">Hallo-vingerafdruk van Hallo hostsleutel opgeven.</span><span class="sxs-lookup"><span data-stu-id="d71f1-148">Specify hello finger print of hello host key.</span></span> | <span data-ttu-id="d71f1-149">Ja als hello `skipHostKeyValidation` toofalse is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="d71f1-149">Yes if hello `skipHostKeyValidation` is set toofalse.</span></span>  |
| <span data-ttu-id="d71f1-150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d71f1-150">gatewayName</span></span> |<span data-ttu-id="d71f1-151">Naam van Hallo Data Management Gateway tooconnect tooan een on-premises SFTP-server.</span><span class="sxs-lookup"><span data-stu-id="d71f1-151">Name of hello Data Management Gateway tooconnect tooan on-premises SFTP server.</span></span> | <span data-ttu-id="d71f1-152">Ja als u kopiëren van gegevens uit een on-premises SFTP-server.</span><span class="sxs-lookup"><span data-stu-id="d71f1-152">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="d71f1-153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="d71f1-153">encryptedCredential</span></span> | <span data-ttu-id="d71f1-154">Versleutelde referentie tooaccess Hallo SFTP-server.</span><span class="sxs-lookup"><span data-stu-id="d71f1-154">Encrypted credential tooaccess hello SFTP server.</span></span> <span data-ttu-id="d71f1-155">Automatisch gegenereerd als u basisverificatie (gebruikersnaam en wachtwoord) of SshPublicKey verificatie (gebruikersnaam + pad naar de persoonlijke sleutel of inhoud) in kopiëren wizard of Hallo ClickOnce pop-up dialoogvenster opgeven.</span><span class="sxs-lookup"><span data-stu-id="d71f1-155">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="d71f1-156">Nee.</span><span class="sxs-lookup"><span data-stu-id="d71f1-156">No.</span></span> <span data-ttu-id="d71f1-157">Alleen van toepassing wanneer het kopiëren van gegevens uit een on-premises SFTP-server.</span><span class="sxs-lookup"><span data-stu-id="d71f1-157">Apply only when copying data from an on-premises SFTP server.</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="d71f1-158">Met behulp van basisverificatie</span><span class="sxs-lookup"><span data-stu-id="d71f1-158">Using basic authentication</span></span>

<span data-ttu-id="d71f1-159">Basisverificatie toouse ingesteld `authenticationType` als `Basic`, en geef de volgende eigenschappen afgezien van SFTP connector algemene die zijn geïntroduceerd in de laatste sectie Hallo HALLO hallo:</span><span class="sxs-lookup"><span data-stu-id="d71f1-159">toouse basic authentication, set `authenticationType` as `Basic`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="d71f1-160">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="d71f1-160">Property</span></span> | <span data-ttu-id="d71f1-161">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d71f1-161">Description</span></span> | <span data-ttu-id="d71f1-162">Vereist</span><span class="sxs-lookup"><span data-stu-id="d71f1-162">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d71f1-163">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="d71f1-163">username</span></span> | <span data-ttu-id="d71f1-164">Gebruiker met toegang toohello SFTP-server.</span><span class="sxs-lookup"><span data-stu-id="d71f1-164">User who has access toohello SFTP server.</span></span> |<span data-ttu-id="d71f1-165">Ja</span><span class="sxs-lookup"><span data-stu-id="d71f1-165">Yes</span></span> |
| <span data-ttu-id="d71f1-166">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="d71f1-166">password</span></span> | <span data-ttu-id="d71f1-167">Wachtwoord voor gebruiker hello (gebruikersnaam).</span><span class="sxs-lookup"><span data-stu-id="d71f1-167">Password for hello user (username).</span></span> | <span data-ttu-id="d71f1-168">Ja</span><span class="sxs-lookup"><span data-stu-id="d71f1-168">Yes</span></span> |

#### <a name="example-basic-authentication"></a><span data-ttu-id="d71f1-169">Voorbeeld: Basisverificatie</span><span class="sxs-lookup"><span data-stu-id="d71f1-169">Example: Basic authentication</span></span>
```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="d71f1-170">Voorbeeld: Basisverificatie met versleutelde referentie</span><span class="sxs-lookup"><span data-stu-id="d71f1-170">Example: Basic authentication with encrypted credential</span></span>

```JSON
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
      }
}
```

### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="d71f1-171">Met behulp van SSH-verificatie voor openbare sleutel</span><span class="sxs-lookup"><span data-stu-id="d71f1-171">Using SSH public key authentication</span></span>

<span data-ttu-id="d71f1-172">Stel toouse SSH openbare-sleutelauthenticatie, `authenticationType` als `SshPublicKey`, en geef de volgende eigenschappen afgezien van SFTP connector algemene die zijn geïntroduceerd in de laatste sectie Hallo HALLO hallo:</span><span class="sxs-lookup"><span data-stu-id="d71f1-172">toouse SSH public key authentication, set `authenticationType` as `SshPublicKey`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="d71f1-173">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="d71f1-173">Property</span></span> | <span data-ttu-id="d71f1-174">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d71f1-174">Description</span></span> | <span data-ttu-id="d71f1-175">Vereist</span><span class="sxs-lookup"><span data-stu-id="d71f1-175">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d71f1-176">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="d71f1-176">username</span></span> |<span data-ttu-id="d71f1-177">Gebruiker met toegang toohello SFTP-server</span><span class="sxs-lookup"><span data-stu-id="d71f1-177">User who has access toohello SFTP server</span></span> |<span data-ttu-id="d71f1-178">Ja</span><span class="sxs-lookup"><span data-stu-id="d71f1-178">Yes</span></span> |
| <span data-ttu-id="d71f1-179">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="d71f1-179">privateKeyPath</span></span> | <span data-ttu-id="d71f1-180">Geef het absolute pad toohello persoonlijke sleutelbestand dat gateway kunt openen.</span><span class="sxs-lookup"><span data-stu-id="d71f1-180">Specify absolute path toohello private key file that gateway can access.</span></span> | <span data-ttu-id="d71f1-181">Geef beide Hallo `privateKeyPath` of `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="d71f1-181">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="d71f1-182">Alleen van toepassing wanneer het kopiëren van gegevens uit een on-premises SFTP-server.</span><span class="sxs-lookup"><span data-stu-id="d71f1-182">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="d71f1-183">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="d71f1-183">privateKeyContent</span></span> | <span data-ttu-id="d71f1-184">Een geserialiseerde tekenreeks Hallo-inhoud met persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="d71f1-184">A serialized string of hello private key content.</span></span> <span data-ttu-id="d71f1-185">Hallo Wizard kopiëren kunt Hallo persoonlijke sleutelbestand lezen inhoud en extraheren Hallo persoonlijke sleutel automatisch.</span><span class="sxs-lookup"><span data-stu-id="d71f1-185">hello Copy Wizard can read hello private key file and extract hello private key content automatically.</span></span> <span data-ttu-id="d71f1-186">Als u van andere hulpprogramma/SDK gebruikmaakt, gebruikt u de Hallo privateKeyPath eigenschap.</span><span class="sxs-lookup"><span data-stu-id="d71f1-186">If you are using any other tool/SDK, use hello privateKeyPath property instead.</span></span> | <span data-ttu-id="d71f1-187">Geef beide Hallo `privateKeyPath` of `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="d71f1-187">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="d71f1-188">Wachtwoordzin</span><span class="sxs-lookup"><span data-stu-id="d71f1-188">passPhrase</span></span> | <span data-ttu-id="d71f1-189">Hallo pass woordgroep en het wachtwoord toodecrypt Hallo persoonlijke sleutel opgeven als Hallo-sleutelbestand is beveiligd met een wachtwoordzin.</span><span class="sxs-lookup"><span data-stu-id="d71f1-189">Specify hello pass phrase/password toodecrypt hello private key if hello key file is protected by a pass phrase.</span></span> | <span data-ttu-id="d71f1-190">Ja als Hallo-bestand met persoonlijke sleutel wordt beveiligd door een wachtwoordzin.</span><span class="sxs-lookup"><span data-stu-id="d71f1-190">Yes if hello private key file is protected by a pass phrase.</span></span> |

> [!NOTE]
> <span data-ttu-id="d71f1-191">SFTP-connector ondersteunen alleen OpenSSH-sleutel.</span><span class="sxs-lookup"><span data-stu-id="d71f1-191">SFTP connector only support OpenSSH key.</span></span> <span data-ttu-id="d71f1-192">Zorg ervoor dat uw sleutelbestand Hallo juiste indeling.</span><span class="sxs-lookup"><span data-stu-id="d71f1-192">Make sure your key file is in hello proper format.</span></span> <span data-ttu-id="d71f1-193">U kunt Putty hulpprogramma tooconvert uit ppk tooOpenSSH indeling gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d71f1-193">You can use Putty tool tooconvert from .ppk tooOpenSSH format.</span></span>

#### <a name="example-sshpublickey-authentication-using-private-key-filepath"></a><span data-ttu-id="d71f1-194">Voorbeeld: SshPublicKey verificatie met behulp van persoonlijke sleutels filePath</span><span class="sxs-lookup"><span data-stu-id="d71f1-194">Example: SshPublicKey authentication using private key filePath</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="d71f1-195">Voorbeeld: SshPublicKey verificatie met behulp van persoonlijke sleutels inhoud</span><span class="sxs-lookup"><span data-stu-id="d71f1-195">Example: SshPublicKey authentication using private key content</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="d71f1-196">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="d71f1-196">Dataset properties</span></span>
<span data-ttu-id="d71f1-197">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="d71f1-197">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="d71f1-198">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle typen van de gegevensset.</span><span class="sxs-lookup"><span data-stu-id="d71f1-198">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="d71f1-199">Hallo **typeProperties** sectie verschilt voor elk type dataset.</span><span class="sxs-lookup"><span data-stu-id="d71f1-199">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="d71f1-200">Het levert informatie die specifieke toohello gegevensset type.</span><span class="sxs-lookup"><span data-stu-id="d71f1-200">It provides information that is specific toohello dataset type.</span></span> <span data-ttu-id="d71f1-201">Hallo typeProperties sectie voor een gegevensset van het type **FileShare** dataset bevat Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="d71f1-201">hello typeProperties section for a dataset of type **FileShare** dataset has hello following properties:</span></span>

| <span data-ttu-id="d71f1-202">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="d71f1-202">Property</span></span> | <span data-ttu-id="d71f1-203">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d71f1-203">Description</span></span> | <span data-ttu-id="d71f1-204">Vereist</span><span class="sxs-lookup"><span data-stu-id="d71f1-204">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d71f1-205">folderPath</span><span class="sxs-lookup"><span data-stu-id="d71f1-205">folderPath</span></span> |<span data-ttu-id="d71f1-206">Submap pad toohello.</span><span class="sxs-lookup"><span data-stu-id="d71f1-206">Sub path toohello folder.</span></span> <span data-ttu-id="d71f1-207">Gebruik van escape-teken ' \ ' voor speciale tekens in Hallo-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="d71f1-207">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="d71f1-208">Zie [voorbeeld gekoppelde service en gegevensset definities](#sample-linked-service-and-dataset-definitions) voor voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="d71f1-208">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="d71f1-209">U kunt deze eigenschap combineren met **partitionBy** toohave mappaden op basis van het segment beginnen of eindigen-datums en tijden.</span><span class="sxs-lookup"><span data-stu-id="d71f1-209">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="d71f1-210">Ja</span><span class="sxs-lookup"><span data-stu-id="d71f1-210">Yes</span></span> |
| <span data-ttu-id="d71f1-211">fileName</span><span class="sxs-lookup"><span data-stu-id="d71f1-211">fileName</span></span> |<span data-ttu-id="d71f1-212">Hallo-naam van Hallo-bestand opgeven in Hallo **folderPath** als u wilt dat Hallo tabel toorefer tooa specifiek bestand in map Hallo.</span><span class="sxs-lookup"><span data-stu-id="d71f1-212">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="d71f1-213">Als u geen waarde voor deze eigenschap niet opgeeft, wijst Hallo tabel tooall bestanden in de map Hallo.</span><span class="sxs-lookup"><span data-stu-id="d71f1-213">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="d71f1-214">Wanneer fileName niet voor een uitvoergegevensset opgegeven is, zou Hallo van Hallo gegenereerd bestand in worden Hallo volgt deze indeling:</span><span class="sxs-lookup"><span data-stu-id="d71f1-214">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="d71f1-215">Gegevens. <Guid>.txt (voorbeeld: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="d71f1-215">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="d71f1-216">Nee</span><span class="sxs-lookup"><span data-stu-id="d71f1-216">No</span></span> |
| <span data-ttu-id="d71f1-217">fileFilter</span><span class="sxs-lookup"><span data-stu-id="d71f1-217">fileFilter</span></span> |<span data-ttu-id="d71f1-218">Geef dat een filter toobe tooselect gebruikt een subset van de bestanden in Hallo folderPath in plaats van alle bestanden.</span><span class="sxs-lookup"><span data-stu-id="d71f1-218">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="d71f1-219">Toegestane waarden zijn: `*` (meerdere tekens) en `?` (willekeurig teken).</span><span class="sxs-lookup"><span data-stu-id="d71f1-219">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="d71f1-220">Voorbeelden 1:`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="d71f1-220">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="d71f1-221">Voorbeeld 2:`"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="d71f1-221">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="d71f1-222">fileFilter geldt voor een invoergegevensset bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="d71f1-222">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="d71f1-223">Deze eigenschap wordt niet ondersteund met HDFS.</span><span class="sxs-lookup"><span data-stu-id="d71f1-223">This property is not supported with HDFS.</span></span> |<span data-ttu-id="d71f1-224">Nee</span><span class="sxs-lookup"><span data-stu-id="d71f1-224">No</span></span> |
| <span data-ttu-id="d71f1-225">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="d71f1-225">partitionedBy</span></span> |<span data-ttu-id="d71f1-226">partitionedBy mag gebruikte toospecify een dynamische folderPath bestandsnaam op van de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="d71f1-226">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="d71f1-227">Bijvoorbeeld, folderPath geparametriseerde voor elk uur van gegevens.</span><span class="sxs-lookup"><span data-stu-id="d71f1-227">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="d71f1-228">Nee</span><span class="sxs-lookup"><span data-stu-id="d71f1-228">No</span></span> |
| <span data-ttu-id="d71f1-229">Indeling</span><span class="sxs-lookup"><span data-stu-id="d71f1-229">format</span></span> | <span data-ttu-id="d71f1-230">Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="d71f1-230">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="d71f1-231">Set Hallo **type** eigenschap onder indeling tooone van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="d71f1-231">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="d71f1-232">Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties.</span><span class="sxs-lookup"><span data-stu-id="d71f1-232">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="d71f1-233">Als u wilt dat te**kopiëren van bestanden als-is** tussen bestandsgebaseerde winkels (binaire kopiëren) Hallo indeling sectie in beide definities invoer en uitvoer gegevensset overslaan.</span><span class="sxs-lookup"><span data-stu-id="d71f1-233">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="d71f1-234">Nee</span><span class="sxs-lookup"><span data-stu-id="d71f1-234">No</span></span> |
| <span data-ttu-id="d71f1-235">Compressie</span><span class="sxs-lookup"><span data-stu-id="d71f1-235">compression</span></span> | <span data-ttu-id="d71f1-236">Hallo-type en compressieniveau voor Hallo gegevens opgeven.</span><span class="sxs-lookup"><span data-stu-id="d71f1-236">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="d71f1-237">Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="d71f1-237">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="d71f1-238">Ondersteunde niveaus: **optimale** en **snelst**.</span><span class="sxs-lookup"><span data-stu-id="d71f1-238">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="d71f1-239">Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="d71f1-239">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="d71f1-240">Nee</span><span class="sxs-lookup"><span data-stu-id="d71f1-240">No</span></span> |
| <span data-ttu-id="d71f1-241">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="d71f1-241">useBinaryTransfer</span></span> |<span data-ttu-id="d71f1-242">Geef binaire overdrachtsmodus of gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d71f1-242">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="d71f1-243">De waarde True voor binaire modus en ONWAAR ASCII.</span><span class="sxs-lookup"><span data-stu-id="d71f1-243">True for binary mode and false ASCII.</span></span> <span data-ttu-id="d71f1-244">Standaardwaarde: True.</span><span class="sxs-lookup"><span data-stu-id="d71f1-244">Default value: True.</span></span> <span data-ttu-id="d71f1-245">Deze eigenschap kan alleen worden gebruikt wanneer de bijbehorende gekoppelde-servicetype is van het type: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="d71f1-245">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="d71f1-246">Nee</span><span class="sxs-lookup"><span data-stu-id="d71f1-246">No</span></span> |

> [!NOTE]
> <span data-ttu-id="d71f1-247">bestandsnaam en fileFilter worden niet gelijktijdig gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d71f1-247">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="d71f1-248">Gebruik de eigenschap partionedBy</span><span class="sxs-lookup"><span data-stu-id="d71f1-248">Using partionedBy property</span></span>
<span data-ttu-id="d71f1-249">Zoals vermeld in de vorige sectie hello, kunt u een dynamische folderPath, filename voor time series-gegevens met partitionedBy opgeven.</span><span class="sxs-lookup"><span data-stu-id="d71f1-249">As mentioned in hello previous section, you can specify a dynamic folderPath, filename for time series data with partitionedBy.</span></span> <span data-ttu-id="d71f1-250">U kunt dit doen met Hallo Data Factory-macro's en Hallo systeemvariabele SliceStart, SliceEnd die wijzen op Hallo logische periode voor een bepaalde gegevenssegment.</span><span class="sxs-lookup"><span data-stu-id="d71f1-250">You can do so with hello Data Factory macros and hello system variable SliceStart, SliceEnd that indicate hello logical time period for a given data slice.</span></span>

<span data-ttu-id="d71f1-251">toolearn over tijd reeks gegevenssets, planning en segmenten, Zie [gegevenssets maken](data-factory-create-datasets.md), [planning en uitvoering](data-factory-scheduling-and-execution.md), en [pijplijnen maken](data-factory-create-pipelines.md) artikelen.</span><span class="sxs-lookup"><span data-stu-id="d71f1-251">toolearn about time series datasets, scheduling, and slices, See [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="d71f1-252">Voorbeeld 1:</span><span class="sxs-lookup"><span data-stu-id="d71f1-252">Sample 1:</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="d71f1-253">In dit voorbeeld {segment} is vervangen door de waarde van de Hallo van Data Factory systeemvariabele SliceStart Hallo-indeling (YYYYMMDDHH) opgegeven.</span><span class="sxs-lookup"><span data-stu-id="d71f1-253">In this example {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="d71f1-254">Hallo SliceStart verwijst toostart tijd van Hallo segment.</span><span class="sxs-lookup"><span data-stu-id="d71f1-254">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="d71f1-255">Hallo folderPath verschilt voor elk segment.</span><span class="sxs-lookup"><span data-stu-id="d71f1-255">hello folderPath is different for each slice.</span></span> <span data-ttu-id="d71f1-256">Voorbeeld: wikidatagateway/wikisampledataout/2014100103 of wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="d71f1-256">Example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="d71f1-257">Voorbeeld 2:</span><span class="sxs-lookup"><span data-stu-id="d71f1-257">Sample 2:</span></span>

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
<span data-ttu-id="d71f1-258">In dit voorbeeld worden jaar, maand, dag en tijd van de SliceStart uitgepakt in verschillende variabelen die worden gebruikt door de eigenschappen voor folderPath en de bestandsnaam.</span><span class="sxs-lookup"><span data-stu-id="d71f1-258">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="d71f1-259">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="d71f1-259">Copy activity properties</span></span>
<span data-ttu-id="d71f1-260">Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="d71f1-260">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="d71f1-261">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en beleidsregels zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="d71f1-261">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="d71f1-262">Terwijl het Hallo-eigenschappen die beschikbaar zijn in Hallo typeProperties gedeelte van de activiteit Hallo variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="d71f1-262">Whereas, hello properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="d71f1-263">Voor de kopieeractiviteit, wordt Hallo type-eigenschappen variëren afhankelijk van Hallo soorten gegevensbronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="d71f1-263">For Copy activity, hello type properties vary depending on hello types of sources and sinks.</span></span>

[!INCLUDE [data-factory-file-system-source](../../includes/data-factory-file-system-source.md)]

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="d71f1-264">Ondersteunde indelingen voor bestands- en compressie</span><span class="sxs-lookup"><span data-stu-id="d71f1-264">Supported file and compression formats</span></span>
<span data-ttu-id="d71f1-265">Zie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d71f1-265">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-sftp-server-tooazure-blob"></a><span data-ttu-id="d71f1-266">JSON-voorbeeld: Gegevens kopiëren van SFTP server tooAzure blob</span><span class="sxs-lookup"><span data-stu-id="d71f1-266">JSON Example: Copy data from SFTP server tooAzure blob</span></span>
<span data-ttu-id="d71f1-267">Hallo volgende voorbeeld wordt een voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d71f1-267">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="d71f1-268">Ze geven weer hoe toocopy van SFTP gegevensbron tooAzure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="d71f1-268">They show how toocopy data from SFTP source tooAzure Blob Storage.</span></span> <span data-ttu-id="d71f1-269">Echter gegevens kunnen worden gekopieerd **rechtstreeks** uit een van de bronnen tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d71f1-269">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d71f1-270">Dit voorbeeld bevat JSON-fragmenten.</span><span class="sxs-lookup"><span data-stu-id="d71f1-270">This sample provides JSON snippets.</span></span> <span data-ttu-id="d71f1-271">Dit omvat geen stapsgewijze instructies voor het maken van de gegevensfactory Hallo.</span><span class="sxs-lookup"><span data-stu-id="d71f1-271">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="d71f1-272">Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor stapsgewijze instructies.</span><span class="sxs-lookup"><span data-stu-id="d71f1-272">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="d71f1-273">Hallo voorbeeld heeft Hallo data factory-entiteiten te volgen:</span><span class="sxs-lookup"><span data-stu-id="d71f1-273">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="d71f1-274">Een gekoppelde service van het type [sftp](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d71f1-274">A linked service of type [sftp](#linked-service-properties).</span></span>
* <span data-ttu-id="d71f1-275">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d71f1-275">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="d71f1-276">Invoer [gegevensset](data-factory-create-datasets.md) van het type [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d71f1-276">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="d71f1-277">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d71f1-277">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="d71f1-278">Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [FileSystemSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d71f1-278">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="d71f1-279">Hallo-voorbeeld worden gegevens gekopieerd van een SFTP server tooan Azure blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="d71f1-279">hello sample copies data from an SFTP server tooan Azure blob every hour.</span></span> <span data-ttu-id="d71f1-280">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="d71f1-280">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="d71f1-281">**Gekoppelde SFTP-service**</span><span class="sxs-lookup"><span data-stu-id="d71f1-281">**SFTP linked service**</span></span>

<span data-ttu-id="d71f1-282">In dit voorbeeld gebruikt de basisverificatie Hallo met gebruikersnaam en wachtwoord in tekst zonder opmaak.</span><span class="sxs-lookup"><span data-stu-id="d71f1-282">This example uses hello basic authentication with user name and password in plain text.</span></span> <span data-ttu-id="d71f1-283">U kunt ook een van de volgende manieren hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="d71f1-283">You can also use one of hello following ways:</span></span>

* <span data-ttu-id="d71f1-284">Basisverificatie met versleutelde referenties</span><span class="sxs-lookup"><span data-stu-id="d71f1-284">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="d71f1-285">SSH-verificatie voor openbare sleutel</span><span class="sxs-lookup"><span data-stu-id="d71f1-285">SSH public key authentication</span></span>

<span data-ttu-id="d71f1-286">Zie [FTP gekoppelde service](#linked-service-properties) sectie voor verschillende soorten verificatie die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d71f1-286">See [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON

{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "myuser",
            "password": "mypassword",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```
<span data-ttu-id="d71f1-287">**Een gekoppelde Azure Storage-service**</span><span class="sxs-lookup"><span data-stu-id="d71f1-287">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="d71f1-288">**Invoergegevensset SFTP**</span><span class="sxs-lookup"><span data-stu-id="d71f1-288">**SFTP input dataset**</span></span>

<span data-ttu-id="d71f1-289">Deze gegevensset verwijst toohello SFTP map `mysharedfolder` en de bestandsnaam `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="d71f1-289">This dataset refers toohello SFTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="d71f1-290">Hallo pijplijn kopieert Hallo toohello bestemming.</span><span class="sxs-lookup"><span data-stu-id="d71f1-290">hello pipeline copies hello file toohello destination.</span></span>

<span data-ttu-id="d71f1-291">Instelling 'extern': 'true' informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="d71f1-291">Setting "external": "true" informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "SFTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "SftpLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="d71f1-292">**Azure Blob-uitvoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="d71f1-292">**Azure Blob output dataset**</span></span>

<span data-ttu-id="d71f1-293">Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="d71f1-293">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d71f1-294">pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="d71f1-294">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="d71f1-295">Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d71f1-295">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="d71f1-296">**Pijplijn met de kopieeractiviteit**</span><span class="sxs-lookup"><span data-stu-id="d71f1-296">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="d71f1-297">Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="d71f1-297">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="d71f1-298">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**FileSystemSource** en **sink** type is ingesteld, te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="d71f1-298">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource** and **sink** type is set too**BlobSink**.</span></span>

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
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
        "start": "2017-02-20T18:00:00Z",
        "end": "2017-02-20T19:00:00Z"
    }
}
```

## <a name="performance-and-tuning"></a><span data-ttu-id="d71f1-299">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="d71f1-299">Performance and Tuning</span></span>
<span data-ttu-id="d71f1-300">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.</span><span class="sxs-lookup"><span data-stu-id="d71f1-300">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d71f1-301">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d71f1-301">Next Steps</span></span>
<span data-ttu-id="d71f1-302">Zie Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d71f1-302">See hello following articles:</span></span>

* <span data-ttu-id="d71f1-303">[Zelfstudie voor kopiëren-activiteit](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies voor het maken van een pijplijn met een Kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="d71f1-303">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
