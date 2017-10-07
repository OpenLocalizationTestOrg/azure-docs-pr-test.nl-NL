---
title: de beveiligingsconfiguratie aaaSplit samenvoegen | Microsoft Docs
description: Instellen van x409 certificaten voor versleuteling
metakeywords: Elastic Database certificates security
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: f9e89c57-61a0-484f-b787-82dae2349cb6
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 511c04be0598d8a0889aa3e3fcf02be0bf0e96cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="split-merge-security-configuration"></a><span data-ttu-id="63a48-103">Gesplitste samenvoegen Beveiligingsconfiguratie</span><span class="sxs-lookup"><span data-stu-id="63a48-103">Split-merge security configuration</span></span>
<span data-ttu-id="63a48-104">toouse hello gesplitste/Merge-service, moet u goed beveiliging configureren.</span><span class="sxs-lookup"><span data-stu-id="63a48-104">toouse hello Split/Merge service, you must correctly configure security.</span></span> <span data-ttu-id="63a48-105">Hallo-service maakt deel uit van Hallo elastisch schalen functie van Microsoft Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="63a48-105">hello service is part of hello Elastic Scale feature of Microsoft Azure SQL Database.</span></span> <span data-ttu-id="63a48-106">Zie voor meer informatie [elastische Scale splitsen en Merge-zelfstudie](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="63a48-106">For more information, see [Elastic Scale Split and Merge Service Tutorial](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span></span>

## <a name="configuring-certificates"></a><span data-ttu-id="63a48-107">Configureren van certificaten</span><span class="sxs-lookup"><span data-stu-id="63a48-107">Configuring certificates</span></span>
<span data-ttu-id="63a48-108">Certificaten worden op twee manieren geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="63a48-108">Certificates are configured in two ways.</span></span> 

1. [<span data-ttu-id="63a48-109">tooConfigure hello SSL-certificaat</span><span class="sxs-lookup"><span data-stu-id="63a48-109">tooConfigure hello SSL Certificate</span></span>](#to-configure-the-ssl-certificate)
2. [<span data-ttu-id="63a48-110">tooConfigure clientcertificaten</span><span class="sxs-lookup"><span data-stu-id="63a48-110">tooConfigure Client Certificates</span></span>](#to-configure-client-certificates) 

## <a name="tooobtain-certificates"></a><span data-ttu-id="63a48-111">tooobtain certificaten</span><span class="sxs-lookup"><span data-stu-id="63a48-111">tooobtain certificates</span></span>
<span data-ttu-id="63a48-112">Certificaten kunnen worden opgehaald van openbare certificeringsinstanties (CA's) of van Hallo [Windows certificaatservice](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span><span class="sxs-lookup"><span data-stu-id="63a48-112">Certificates can be obtained from public Certificate Authorities (CAs) or from hello [Windows Certificate Service](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span></span> <span data-ttu-id="63a48-113">Dit zijn Hallo voorkeur methoden tooobtain certificaten.</span><span class="sxs-lookup"><span data-stu-id="63a48-113">These are hello preferred methods tooobtain certificates.</span></span>

<span data-ttu-id="63a48-114">Als u deze opties niet beschikbaar zijn, kunt u genereren **zelfondertekende certificaten**.</span><span class="sxs-lookup"><span data-stu-id="63a48-114">If those options are not available, you can generate **self-signed certificates**.</span></span>

## <a name="tools-toogenerate-certificates"></a><span data-ttu-id="63a48-115">Hulpprogramma's voor toogenerate certificaten</span><span class="sxs-lookup"><span data-stu-id="63a48-115">Tools toogenerate certificates</span></span>
* [<span data-ttu-id="63a48-116">MakeCert.exe</span><span class="sxs-lookup"><span data-stu-id="63a48-116">makecert.exe</span></span>](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [<span data-ttu-id="63a48-117">pvk2pfx.exe</span><span class="sxs-lookup"><span data-stu-id="63a48-117">pvk2pfx.exe</span></span>](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="toorun-hello-tools"></a><span data-ttu-id="63a48-118">toorun Hallo-hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="63a48-118">toorun hello tools</span></span>
* <span data-ttu-id="63a48-119">Zie van ontwikkelaars vanaf de opdrachtprompt voor Visual Studios [Visual Studio-opdrachtprompt](http://msdn.microsoft.com/library/ms229859.aspx)</span><span class="sxs-lookup"><span data-stu-id="63a48-119">From a Developer Command Prompt for Visual Studios, see [Visual Studio Command Prompt](http://msdn.microsoft.com/library/ms229859.aspx)</span></span> 
  
    <span data-ttu-id="63a48-120">Als u hebt geïnstalleerd, gaat u naar:</span><span class="sxs-lookup"><span data-stu-id="63a48-120">If installed, go to:</span></span>
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* <span data-ttu-id="63a48-121">Ophalen van Hallo WDK van [Windows 8.1: Download kits en hulpprogramma's](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span><span class="sxs-lookup"><span data-stu-id="63a48-121">Get hello WDK from [Windows 8.1: Download kits and tools](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span></span>

## <a name="tooconfigure-hello-ssl-certificate"></a><span data-ttu-id="63a48-122">tooconfigure hello SSL-certificaat</span><span class="sxs-lookup"><span data-stu-id="63a48-122">tooconfigure hello SSL certificate</span></span>
<span data-ttu-id="63a48-123">Een SSL-certificaat is vereist tooencrypt Hallo communicatie en Hallo server verifiëren.</span><span class="sxs-lookup"><span data-stu-id="63a48-123">A SSL certificate is required tooencrypt hello communication and authenticate hello server.</span></span> <span data-ttu-id="63a48-124">Kies Hallo meest toepasselijke van Hallo drie scenario's hieronder en alle bijbehorende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="63a48-124">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="63a48-125">Een nieuw zelfondertekend certificaat maken</span><span class="sxs-lookup"><span data-stu-id="63a48-125">Create a new self-signed certificate</span></span>
1. [<span data-ttu-id="63a48-126">Een zelfondertekend certificaat maken</span><span class="sxs-lookup"><span data-stu-id="63a48-126">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="63a48-127">PFX-bestand voor zelfondertekende SSL-certificaat maken</span><span class="sxs-lookup"><span data-stu-id="63a48-127">Create PFX file for Self-Signed SSL Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="63a48-128">SSL-certificaat tooCloud Service uploaden</span><span class="sxs-lookup"><span data-stu-id="63a48-128">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
4. [<span data-ttu-id="63a48-129">SSL-certificaat in het configuratiebestand van de Service bijwerken</span><span class="sxs-lookup"><span data-stu-id="63a48-129">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)
5. [<span data-ttu-id="63a48-130">SSL-certificeringsinstantie importeren</span><span class="sxs-lookup"><span data-stu-id="63a48-130">Import SSL Certification Authority</span></span>](#import-ssl-certification-authority)

### <a name="toouse-an-existing-certificate-from-hello-certificate-store"></a><span data-ttu-id="63a48-131">toouse een bestaand certificaat van Hallo certificaat opslaan</span><span class="sxs-lookup"><span data-stu-id="63a48-131">toouse an existing certificate from hello certificate store</span></span>
1. [<span data-ttu-id="63a48-132">SSL-certificaat exporteren uit het certificaatarchief</span><span class="sxs-lookup"><span data-stu-id="63a48-132">Export SSL Certificate From Certificate Store</span></span>](#export-ssl-certificate-from-certificate-store)
2. [<span data-ttu-id="63a48-133">SSL-certificaat tooCloud Service uploaden</span><span class="sxs-lookup"><span data-stu-id="63a48-133">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
3. [<span data-ttu-id="63a48-134">SSL-certificaat in het configuratiebestand van de Service bijwerken</span><span class="sxs-lookup"><span data-stu-id="63a48-134">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

### <a name="toouse-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="63a48-135">toouse een bestaand certificaat in een PFX-bestand</span><span class="sxs-lookup"><span data-stu-id="63a48-135">toouse an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="63a48-136">SSL-certificaat tooCloud Service uploaden</span><span class="sxs-lookup"><span data-stu-id="63a48-136">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
2. [<span data-ttu-id="63a48-137">SSL-certificaat in het configuratiebestand van de Service bijwerken</span><span class="sxs-lookup"><span data-stu-id="63a48-137">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

## <a name="tooconfigure-client-certificates"></a><span data-ttu-id="63a48-138">clientcertificaten tooconfigure</span><span class="sxs-lookup"><span data-stu-id="63a48-138">tooconfigure client certificates</span></span>
<span data-ttu-id="63a48-139">Clientcertificaten vereist zijn in de volgorde tooauthenticate aanvragen toohello service.</span><span class="sxs-lookup"><span data-stu-id="63a48-139">Client certificates are required in order tooauthenticate requests toohello service.</span></span> <span data-ttu-id="63a48-140">Kies Hallo meest toepasselijke van Hallo drie scenario's hieronder en alle bijbehorende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="63a48-140">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="turn-off-client-certificates"></a><span data-ttu-id="63a48-141">Clientcertificaten uitschakelen</span><span class="sxs-lookup"><span data-stu-id="63a48-141">Turn off client certificates</span></span>
1. [<span data-ttu-id="63a48-142">Op basis van certificaten clientverificatie uitschakelen</span><span class="sxs-lookup"><span data-stu-id="63a48-142">Turn Off Client Certificate-Based Authentication</span></span>](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a><span data-ttu-id="63a48-143">Nieuwe zelfondertekende certificaten uitgeven</span><span class="sxs-lookup"><span data-stu-id="63a48-143">Issue new self-signed client certificates</span></span>
1. [<span data-ttu-id="63a48-144">Een zelfondertekend certificeringsinstantie maken</span><span class="sxs-lookup"><span data-stu-id="63a48-144">Create a Self-Signed Certification Authority</span></span>](#create-a-self-signed-certification-authority)
2. [<span data-ttu-id="63a48-145">CA-certificaat tooCloud Service uploaden</span><span class="sxs-lookup"><span data-stu-id="63a48-145">Upload CA Certificate tooCloud Service</span></span>](#upload-ca-certificate-to-cloud-service)
3. [<span data-ttu-id="63a48-146">CA-certificaat in het configuratiebestand van de Service bijwerken</span><span class="sxs-lookup"><span data-stu-id="63a48-146">Update CA Certificate in Service Configuration File</span></span>](#update-ca-certificate-in-service-configuration-file)
4. [<span data-ttu-id="63a48-147">Clientcertificaten uitgeven</span><span class="sxs-lookup"><span data-stu-id="63a48-147">Issue Client Certificates</span></span>](#issue-client-certificates)
5. [<span data-ttu-id="63a48-148">PFX-bestanden maken voor clientcertificaten</span><span class="sxs-lookup"><span data-stu-id="63a48-148">Create PFX files for Client Certificates</span></span>](#create-pfx-files-for-client-certificates)
6. [<span data-ttu-id="63a48-149">Client-certificaat importeren</span><span class="sxs-lookup"><span data-stu-id="63a48-149">Import Client Certificate</span></span>](#Import-Client-Certificate)
7. [<span data-ttu-id="63a48-150">Certificaatvingerafdrukken Client kopiëren</span><span class="sxs-lookup"><span data-stu-id="63a48-150">Copy Client Certificate Thumbprints</span></span>](#copy-client-certificate-thumbprints)
8. [<span data-ttu-id="63a48-151">Clients toegestaan in Hallo serviceconfiguratiebestand configureren</span><span class="sxs-lookup"><span data-stu-id="63a48-151">Configure Allowed Clients in hello Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a><span data-ttu-id="63a48-152">Bestaande clientcertificaten gebruiken</span><span class="sxs-lookup"><span data-stu-id="63a48-152">Use existing client certificates</span></span>
1. [<span data-ttu-id="63a48-153">Vinden van openbare sleutel van CA</span><span class="sxs-lookup"><span data-stu-id="63a48-153">Find CA Public Key</span></span>](#find-ca-public-key)
2. [<span data-ttu-id="63a48-154">CA-certificaat tooCloud Service uploaden</span><span class="sxs-lookup"><span data-stu-id="63a48-154">Upload CA Certificate tooCloud Service</span></span>](#Upload-CA-certificate-to-cloud-service)
3. [<span data-ttu-id="63a48-155">CA-certificaat in het configuratiebestand van de Service bijwerken</span><span class="sxs-lookup"><span data-stu-id="63a48-155">Update CA Certificate in Service Configuration File</span></span>](#Update-CA-Certificate-in-Service-Configuration-File)
4. [<span data-ttu-id="63a48-156">Certificaatvingerafdrukken Client kopiëren</span><span class="sxs-lookup"><span data-stu-id="63a48-156">Copy Client Certificate Thumbprints</span></span>](#Copy-Client-Certificate-Thumbprints)
5. [<span data-ttu-id="63a48-157">Clients toegestaan in Hallo serviceconfiguratiebestand configureren</span><span class="sxs-lookup"><span data-stu-id="63a48-157">Configure Allowed Clients in hello Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)
6. [<span data-ttu-id="63a48-158">Controle van certificaatintrekking Client configureren</span><span class="sxs-lookup"><span data-stu-id="63a48-158">Configure Client Certificate Revocation Check</span></span>](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a><span data-ttu-id="63a48-159">Toegestane IP-adressen</span><span class="sxs-lookup"><span data-stu-id="63a48-159">Allowed IP addresses</span></span>
<span data-ttu-id="63a48-160">Toegang toohello service-eindpunten kunnen beperkte toospecific bereiken van IP-adressen zijn.</span><span class="sxs-lookup"><span data-stu-id="63a48-160">Access toohello service endpoints can be restricted toospecific ranges of IP addresses.</span></span>

## <a name="tooconfigure-encryption-for-hello-store"></a><span data-ttu-id="63a48-161">versleuteling voor Hallo store tooconfigure</span><span class="sxs-lookup"><span data-stu-id="63a48-161">tooconfigure encryption for hello store</span></span>
<span data-ttu-id="63a48-162">Een certificaat is vereist tooencrypt Hallo referenties die zijn opgeslagen in Hallo metagegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="63a48-162">A certificate is required tooencrypt hello credentials that are stored in hello metadata store.</span></span> <span data-ttu-id="63a48-163">Kies Hallo meest toepasselijke van Hallo drie scenario's hieronder en alle bijbehorende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="63a48-163">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="use-a-new-self-signed-certificate"></a><span data-ttu-id="63a48-164">Een nieuw zelfondertekend certificaat gebruiken</span><span class="sxs-lookup"><span data-stu-id="63a48-164">Use a new self-signed certificate</span></span>
1. [<span data-ttu-id="63a48-165">Een zelfondertekend certificaat maken</span><span class="sxs-lookup"><span data-stu-id="63a48-165">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="63a48-166">PFX-bestand voor het versleutelingscertificaat zelfondertekend maken</span><span class="sxs-lookup"><span data-stu-id="63a48-166">Create PFX file for Self-Signed Encryption Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="63a48-167">Versleutelingscertificaat tooCloud Service uploaden</span><span class="sxs-lookup"><span data-stu-id="63a48-167">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
4. [<span data-ttu-id="63a48-168">Versleutelingscertificaat in het configuratiebestand van de Service bijwerken</span><span class="sxs-lookup"><span data-stu-id="63a48-168">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-hello-certificate-store"></a><span data-ttu-id="63a48-169">Een bestaand certificaat uit het certificaatarchief hello gebruiken</span><span class="sxs-lookup"><span data-stu-id="63a48-169">Use an existing certificate from hello certificate store</span></span>
1. [<span data-ttu-id="63a48-170">Versleutelingscertificaat exporteren uit het certificaatarchief</span><span class="sxs-lookup"><span data-stu-id="63a48-170">Export Encryption Certificate From Certificate Store</span></span>](#export-encryption-certificate-from-certificate-store)
2. [<span data-ttu-id="63a48-171">Versleutelingscertificaat tooCloud Service uploaden</span><span class="sxs-lookup"><span data-stu-id="63a48-171">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
3. [<span data-ttu-id="63a48-172">Versleutelingscertificaat in het configuratiebestand van de Service bijwerken</span><span class="sxs-lookup"><span data-stu-id="63a48-172">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="63a48-173">Een bestaand certificaat gebruiken in een PFX-bestand</span><span class="sxs-lookup"><span data-stu-id="63a48-173">Use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="63a48-174">Versleutelingscertificaat tooCloud Service uploaden</span><span class="sxs-lookup"><span data-stu-id="63a48-174">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
2. [<span data-ttu-id="63a48-175">Versleutelingscertificaat in het configuratiebestand van de Service bijwerken</span><span class="sxs-lookup"><span data-stu-id="63a48-175">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

## <a name="hello-default-configuration"></a><span data-ttu-id="63a48-176">Hallo standaardconfiguratie</span><span class="sxs-lookup"><span data-stu-id="63a48-176">hello default configuration</span></span>
<span data-ttu-id="63a48-177">Hallo standaardconfiguratie weigert u alle toegang toohello HTTP-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="63a48-177">hello default configuration denies all access toohello HTTP endpoint.</span></span> <span data-ttu-id="63a48-178">Dit is Hallo aanbevolen instelling, aangezien Hallo aanvragen toothese eindpunten gevoelige informatie, zoals databasereferenties mag uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="63a48-178">This is hello recommended setting, since hello requests toothese endpoints may carry sensitive information like database credentials.</span></span>
<span data-ttu-id="63a48-179">Hallo standaardconfiguratie kunt alle toegang toohello HTTPS-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="63a48-179">hello default configuration allows all access toohello HTTPS endpoint.</span></span> <span data-ttu-id="63a48-180">Deze instelling kan verder worden beperkt.</span><span class="sxs-lookup"><span data-stu-id="63a48-180">This setting may be restricted further.</span></span>

### <a name="changing-hello-configuration"></a><span data-ttu-id="63a48-181">Hallo-configuratie wijzigen</span><span class="sxs-lookup"><span data-stu-id="63a48-181">Changing hello Configuration</span></span>
<span data-ttu-id="63a48-182">Hallo groep toegangscontroleregels die van toepassing zijn tooand-eindpunt is geconfigureerd in Hallo  **<EndpointAcls>**  sectie in Hallo **serviceconfiguratiebestand**.</span><span class="sxs-lookup"><span data-stu-id="63a48-182">hello group of access control rules that apply tooand endpoint are configured in hello **<EndpointAcls>** section in hello **service configuration file**.</span></span>

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

<span data-ttu-id="63a48-183">Hallo-regels in een besturingselement toegangsgroep zijn geconfigureerd in een <AccessControl name=""> gedeelte van configuratiebestand Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="63a48-183">hello rules in an access control group are configured in a <AccessControl name=""> section of hello service configuration file.</span></span> 

<span data-ttu-id="63a48-184">Hallo-indeling wordt uitgelegd in de documentatie voor Network Access Control Lists.</span><span class="sxs-lookup"><span data-stu-id="63a48-184">hello format is explained in Network Access Control Lists documentation.</span></span>
<span data-ttu-id="63a48-185">Bijvoorbeeld: tooallow alleen IP-adressen in Hallo bereik 100.100.0.0 too100.100.255.255 tooaccess Hallo HTTPS-eindpunt, Hallo regels eruit als volgt:</span><span class="sxs-lookup"><span data-stu-id="63a48-185">For example, tooallow only IPs in hello range 100.100.0.0 too100.100.255.255 tooaccess hello HTTPS endpoint, hello rules would look like this:</span></span>

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a><span data-ttu-id="63a48-186">Denial of service te voorkomen</span><span class="sxs-lookup"><span data-stu-id="63a48-186">Denial of service prevention</span></span>
<span data-ttu-id="63a48-187">Er zijn twee verschillende mechanismen toodetect ondersteund en Denial of Service-aanvallen te voorkomen:</span><span class="sxs-lookup"><span data-stu-id="63a48-187">There are two different mechanisms supported toodetect and prevent Denial of Service attacks:</span></span>

* <span data-ttu-id="63a48-188">Beperk het aantal gelijktijdige aanvragen per externe host (standaard uitgeschakeld)</span><span class="sxs-lookup"><span data-stu-id="63a48-188">Restrict number of concurrent requests per remote host (off by default)</span></span>
* <span data-ttu-id="63a48-189">Snelheid van toegang per externe host beperken (op standaard)</span><span class="sxs-lookup"><span data-stu-id="63a48-189">Restrict rate of access per remote host (on by default)</span></span>

<span data-ttu-id="63a48-190">Deze zijn gebaseerd op Hallo functies verder beschreven in de dynamische IP-beveiliging in IIS.</span><span class="sxs-lookup"><span data-stu-id="63a48-190">These are based on hello features further documented in Dynamic IP Security in IIS.</span></span> <span data-ttu-id="63a48-191">Wanneer deze configuratie wijzigen pas op Hallo volgende factoren:</span><span class="sxs-lookup"><span data-stu-id="63a48-191">When changing this configuration beware of hello following factors:</span></span>

* <span data-ttu-id="63a48-192">Hallo-gedrag van proxy's en apparaten via Hallo externe hostinformatie Network Address Translation</span><span class="sxs-lookup"><span data-stu-id="63a48-192">hello behavior of proxies and Network Address Translation devices over hello remote host information</span></span>
* <span data-ttu-id="63a48-193">Elke aanvraag tooany resource in de Webrol hello wordt beschouwd als (bijvoorbeeld bij het laden van scripts, afbeeldingen, enzovoort)</span><span class="sxs-lookup"><span data-stu-id="63a48-193">Each request tooany resource in hello web role is considered (e.g. loading scripts, images, etc)</span></span>

## <a name="restricting-number-of-concurrent-accesses"></a><span data-ttu-id="63a48-194">Het aantal gelijktijdige toegang beperken</span><span class="sxs-lookup"><span data-stu-id="63a48-194">Restricting number of concurrent accesses</span></span>
<span data-ttu-id="63a48-195">Hallo-instellingen voor het configureren van dit probleem zijn:</span><span class="sxs-lookup"><span data-stu-id="63a48-195">hello settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

<span data-ttu-id="63a48-196">DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable deze beveiliging wijzigen.</span><span class="sxs-lookup"><span data-stu-id="63a48-196">Change DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable this protection.</span></span>

## <a name="restricting-rate-of-access"></a><span data-ttu-id="63a48-197">Snelheid van de toegang beperken</span><span class="sxs-lookup"><span data-stu-id="63a48-197">Restricting rate of access</span></span>
<span data-ttu-id="63a48-198">Hallo-instellingen voor het configureren van dit probleem zijn:</span><span class="sxs-lookup"><span data-stu-id="63a48-198">hello settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-hello-response-tooa-denied-request"></a><span data-ttu-id="63a48-199">Hallo antwoord tooa configureren aanvraag geweigerd</span><span class="sxs-lookup"><span data-stu-id="63a48-199">Configuring hello response tooa denied request</span></span>
<span data-ttu-id="63a48-200">Hallo configureert volgende instelling Hallo antwoord tooa aanvraag geweigerd:</span><span class="sxs-lookup"><span data-stu-id="63a48-200">hello following setting configures hello response tooa denied request:</span></span>

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
<span data-ttu-id="63a48-201">Raadpleeg de documentatie toohello voor dynamische IP-beveiliging in IIS voor andere ondersteunde waarden.</span><span class="sxs-lookup"><span data-stu-id="63a48-201">Refer toohello documentation for Dynamic IP Security in IIS for other supported values.</span></span>

## <a name="operations-for-configuring-service-certificates"></a><span data-ttu-id="63a48-202">Bewerkingen voor het configureren van servicecertificaten</span><span class="sxs-lookup"><span data-stu-id="63a48-202">Operations for configuring service certificates</span></span>
<span data-ttu-id="63a48-203">Dit onderwerp is alleen ter informatie.</span><span class="sxs-lookup"><span data-stu-id="63a48-203">This topic is for reference only.</span></span> <span data-ttu-id="63a48-204">Volg de configuratiestappen Hallo die worden beschreven in:</span><span class="sxs-lookup"><span data-stu-id="63a48-204">Please follow hello configuration steps outlined in:</span></span>

* <span data-ttu-id="63a48-205">Hallo SSL-certificaat configureren</span><span class="sxs-lookup"><span data-stu-id="63a48-205">Configure hello SSL certificate</span></span>
* <span data-ttu-id="63a48-206">Clientcertificaten configureren</span><span class="sxs-lookup"><span data-stu-id="63a48-206">Configure client certificates</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="63a48-207">Een zelfondertekend certificaat maken</span><span class="sxs-lookup"><span data-stu-id="63a48-207">Create a self-signed certificate</span></span>
<span data-ttu-id="63a48-208">Uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="63a48-208">Execute:</span></span>

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

<span data-ttu-id="63a48-209">toocustomize:</span><span class="sxs-lookup"><span data-stu-id="63a48-209">toocustomize:</span></span>

* <span data-ttu-id="63a48-210">-n met Hallo service-URL.</span><span class="sxs-lookup"><span data-stu-id="63a48-210">-n with hello service URL.</span></span> <span data-ttu-id="63a48-211">Jokertekens ("CN = * .cloudapp .net ') en alternatieve namen (CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net') worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="63a48-211">Wildcards ("CN=*.cloudapp.net") and alternative names ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") are supported.</span></span>
* <span data-ttu-id="63a48-212">-e met Hallo certificaat verloopt een sterk wachtwoord maken en geef hem wanneer u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="63a48-212">-e with hello certificate expiration date Create a strong password and specify it when prompted.</span></span>

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a><span data-ttu-id="63a48-213">PFX-bestand voor zelf-ondertekend SSL-certificaat maken</span><span class="sxs-lookup"><span data-stu-id="63a48-213">Create PFX file for self-signed SSL certificate</span></span>
<span data-ttu-id="63a48-214">Uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="63a48-214">Execute:</span></span>

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

<span data-ttu-id="63a48-215">Wachtwoord invoeren en exporteer het certificaat met deze opties:</span><span class="sxs-lookup"><span data-stu-id="63a48-215">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="63a48-216">Ja, Hallo persoonlijke sleutel exporteren</span><span class="sxs-lookup"><span data-stu-id="63a48-216">Yes, export hello private key</span></span>
* <span data-ttu-id="63a48-217">Alle uitgebreide eigenschappen exporteren</span><span class="sxs-lookup"><span data-stu-id="63a48-217">Export all extended properties</span></span>

## <a name="export-ssl-certificate-from-certificate-store"></a><span data-ttu-id="63a48-218">SSL-certificaat exporteren uit het certificaatarchief</span><span class="sxs-lookup"><span data-stu-id="63a48-218">Export SSL certificate from certificate store</span></span>
* <span data-ttu-id="63a48-219">Certificaat zoeken</span><span class="sxs-lookup"><span data-stu-id="63a48-219">Find certificate</span></span>
* <span data-ttu-id="63a48-220">Klik op Acties -> alle taken -> exporteren...</span><span class="sxs-lookup"><span data-stu-id="63a48-220">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="63a48-221">Exporteer het certificaat in een. PFX-bestand met deze opties:</span><span class="sxs-lookup"><span data-stu-id="63a48-221">Export certificate into a .PFX file with these options:</span></span>
  * <span data-ttu-id="63a48-222">Ja, Hallo persoonlijke sleutel exporteren</span><span class="sxs-lookup"><span data-stu-id="63a48-222">Yes, export hello private key</span></span>
  * <span data-ttu-id="63a48-223">Indien mogelijk exporteren met alle certificaten in het certificeringspad Hallo * alle uitgebreide eigenschappen exporteren</span><span class="sxs-lookup"><span data-stu-id="63a48-223">Include all certificates in hello certification path if possible *Export all extended properties</span></span>

## <a name="upload-ssl-certificate-toocloud-service"></a><span data-ttu-id="63a48-224">SSL-certificaat toocloud service uploaden</span><span class="sxs-lookup"><span data-stu-id="63a48-224">Upload SSL certificate toocloud service</span></span>
<span data-ttu-id="63a48-225">Upload het certificaat met de Hallo bestaande of gegenereerd. PFX-bestand met de Hallo SSL-sleutelpaar:</span><span class="sxs-lookup"><span data-stu-id="63a48-225">Upload certificate with hello existing or generated .PFX file with hello SSL key pair:</span></span>

* <span data-ttu-id="63a48-226">Hallo-wachtwoord beveiligt persoonlijke sleutelgegevens Hallo invoeren</span><span class="sxs-lookup"><span data-stu-id="63a48-226">Enter hello password protecting hello private key information</span></span>

## <a name="update-ssl-certificate-in-service-configuration-file"></a><span data-ttu-id="63a48-227">SSL-certificaat in het configuratiebestand van de service bijwerken</span><span class="sxs-lookup"><span data-stu-id="63a48-227">Update SSL certificate in service configuration file</span></span>
<span data-ttu-id="63a48-228">Update Hallo vingerafdrukwaarde van de volgende instelling in het serviceconfiguratiebestand met de vingerafdruk van certificaat Hallo HALLO hallo Hallo geüpload toohello cloudservice:</span><span class="sxs-lookup"><span data-stu-id="63a48-228">Update hello thumbprint value of hello following setting in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a><span data-ttu-id="63a48-229">SSL-certificeringsinstantie importeren</span><span class="sxs-lookup"><span data-stu-id="63a48-229">Import SSL certification authority</span></span>
<span data-ttu-id="63a48-230">Volg deze stappen in alle account/machine die communiceert met de Hallo-service:</span><span class="sxs-lookup"><span data-stu-id="63a48-230">Follow these steps in all account/machine that will communicate with hello service:</span></span>

* <span data-ttu-id="63a48-231">Dubbelklik op Hallo. CER-bestand in Windows Verkenner</span><span class="sxs-lookup"><span data-stu-id="63a48-231">Double-click hello .CER file in Windows Explorer</span></span>
* <span data-ttu-id="63a48-232">Klik in het dialoogvenster certificaat Hallo certificaat installeren...</span><span class="sxs-lookup"><span data-stu-id="63a48-232">In hello Certificate dialog, click Install Certificate…</span></span>
* <span data-ttu-id="63a48-233">Certificaat importeren in Hallo die Trusted Root Certification Authorities opslaan</span><span class="sxs-lookup"><span data-stu-id="63a48-233">Import certificate into hello Trusted Root Certification Authorities store</span></span>

## <a name="turn-off-client-certificate-based-authentication"></a><span data-ttu-id="63a48-234">Op basis van certificaten clientverificatie uitschakelen</span><span class="sxs-lookup"><span data-stu-id="63a48-234">Turn off client certificate-based authentication</span></span>
<span data-ttu-id="63a48-235">Alleen op basis van certificaten clientverificatie wordt ondersteund en u dit uitschakelt wilt toestaan voor openbare toegang toohello service-eindpunten, tenzij andere beveiligingsmechanismen geïmplementeerd (zoals Microsoft Azure Virtual Network) zijn.</span><span class="sxs-lookup"><span data-stu-id="63a48-235">Only client certificate-based authentication is supported and disabling it will allow for public access toohello service endpoints, unless other mechanisms are in place (e.g. Microsoft Azure Virtual Network).</span></span>

<span data-ttu-id="63a48-236">Deze instellingen toofalse in functie van Hallo service configuration file tooturn Hallo wijzigen uitschakelen:</span><span class="sxs-lookup"><span data-stu-id="63a48-236">Change these settings toofalse in hello service configuration file tooturn hello feature off:</span></span>

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

<span data-ttu-id="63a48-237">Kopieer vervolgens Hallo die dezelfde vingerafdruk als Hallo SSL-certificaat in de instelling voor Hallo CA-certificaat:</span><span class="sxs-lookup"><span data-stu-id="63a48-237">Then, copy hello same thumbprint as hello SSL certificate in hello CA certificate setting:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a><span data-ttu-id="63a48-238">Een zelfondertekend certificeringsinstantie maken</span><span class="sxs-lookup"><span data-stu-id="63a48-238">Create a self-signed certification authority</span></span>
<span data-ttu-id="63a48-239">Hallo te volgen stappen toocreate een zelfondertekend certificaat tooact als een certificeringsinstantie worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="63a48-239">Execute hello following steps toocreate a self-signed certificate tooact as a Certification Authority:</span></span>

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

<span data-ttu-id="63a48-240">toocustomize deze</span><span class="sxs-lookup"><span data-stu-id="63a48-240">toocustomize it</span></span>

* <span data-ttu-id="63a48-241">-e met Hallo certificeringsinstantie vervaldatum</span><span class="sxs-lookup"><span data-stu-id="63a48-241">-e with hello certification expiration date</span></span>

## <a name="find-ca-public-key"></a><span data-ttu-id="63a48-242">Vinden van openbare sleutel van CA</span><span class="sxs-lookup"><span data-stu-id="63a48-242">Find CA public key</span></span>
<span data-ttu-id="63a48-243">Alle clientcertificaten zijn uitgegeven door een certificeringsinstantie wordt vertrouwd door het Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="63a48-243">All client certificates must have been issued by a Certification Authority trusted by hello service.</span></span> <span data-ttu-id="63a48-244">Vinden Hallo openbare sleutel toohello certificeringsinstantie die certificaten Hallo client die toobe worden gebruikt voor verificatie in volgorde tooupload het toohello-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="63a48-244">Find hello public key toohello Certification Authority that issued hello client certificates that are going toobe used for authentication in order tooupload it toohello cloud service.</span></span>

<span data-ttu-id="63a48-245">Als Hallo-bestand met de openbare sleutel Hallo niet beschikbaar is, uit het certificaatarchief Hallo exporteren:</span><span class="sxs-lookup"><span data-stu-id="63a48-245">If hello file with hello public key is not available, export it from hello certificate store:</span></span>

* <span data-ttu-id="63a48-246">Certificaat zoeken</span><span class="sxs-lookup"><span data-stu-id="63a48-246">Find certificate</span></span>
  * <span data-ttu-id="63a48-247">Zoeken naar een clientcertificaat dat is uitgegeven door Hallo dezelfde certificeringsinstantie (CA)</span><span class="sxs-lookup"><span data-stu-id="63a48-247">Search for a client certificate issued by hello same Certification Authority</span></span>
* <span data-ttu-id="63a48-248">Dubbelklik op Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="63a48-248">Double-click hello certificate.</span></span>
* <span data-ttu-id="63a48-249">Selecteer Hallo certificeringspad tabblad in het dialoogvenster voor Hallo-certificaat.</span><span class="sxs-lookup"><span data-stu-id="63a48-249">Select hello Certification Path tab in hello Certificate dialog.</span></span>
* <span data-ttu-id="63a48-250">Dubbelklik op Hallo CA vermelding in het Hallo-pad.</span><span class="sxs-lookup"><span data-stu-id="63a48-250">Double-click hello CA entry in hello path.</span></span>
* <span data-ttu-id="63a48-251">Notities van de certificaateigenschappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="63a48-251">Take notes of hello certificate properties.</span></span>
* <span data-ttu-id="63a48-252">Sluit Hallo **certificaat** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="63a48-252">Close hello **Certificate** dialog.</span></span>
* <span data-ttu-id="63a48-253">Certificaat zoeken</span><span class="sxs-lookup"><span data-stu-id="63a48-253">Find certificate</span></span>
  * <span data-ttu-id="63a48-254">Zoeken naar Hallo CA die hierboven vermeld.</span><span class="sxs-lookup"><span data-stu-id="63a48-254">Search for hello CA noted above.</span></span>
* <span data-ttu-id="63a48-255">Klik op Acties -> alle taken -> exporteren...</span><span class="sxs-lookup"><span data-stu-id="63a48-255">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="63a48-256">Exporteer het certificaat in een. CER met deze opties:</span><span class="sxs-lookup"><span data-stu-id="63a48-256">Export certificate into a .CER with these options:</span></span>
  * <span data-ttu-id="63a48-257">**Nee, Hallo persoonlijke sleutel niet exporteren**</span><span class="sxs-lookup"><span data-stu-id="63a48-257">**No, do not export hello private key**</span></span>
  * <span data-ttu-id="63a48-258">Indien mogelijk exporteren met alle certificaten in het certificeringspad Hallo.</span><span class="sxs-lookup"><span data-stu-id="63a48-258">Include all certificates in hello certification path if possible.</span></span>
  * <span data-ttu-id="63a48-259">Alle uitgebreide eigenschappen exporteren.</span><span class="sxs-lookup"><span data-stu-id="63a48-259">Export all extended properties.</span></span>

## <a name="upload-ca-certificate-toocloud-service"></a><span data-ttu-id="63a48-260">Uploaden van de CA-certificaat toocloud-service</span><span class="sxs-lookup"><span data-stu-id="63a48-260">Upload CA certificate toocloud service</span></span>
<span data-ttu-id="63a48-261">Upload het certificaat met de Hallo bestaande of gegenereerd. CER-bestand met de openbare sleutel Hallo CA.</span><span class="sxs-lookup"><span data-stu-id="63a48-261">Upload certificate with hello existing or generated .CER file with hello CA public key.</span></span>

## <a name="update-ca-certificate-in-service-configuration-file"></a><span data-ttu-id="63a48-262">Update-CA-certificaat in het configuratiebestand van de service</span><span class="sxs-lookup"><span data-stu-id="63a48-262">Update CA certificate in service configuration file</span></span>
<span data-ttu-id="63a48-263">Update Hallo vingerafdrukwaarde van de volgende instelling in het serviceconfiguratiebestand met de vingerafdruk van certificaat Hallo HALLO hallo Hallo geüpload toohello cloudservice:</span><span class="sxs-lookup"><span data-stu-id="63a48-263">Update hello thumbprint value of hello following setting in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

<span data-ttu-id="63a48-264">Werk de waarde Hallo Hallo na instellen met Hallo dezelfde vingerafdruk:</span><span class="sxs-lookup"><span data-stu-id="63a48-264">Update hello value of hello following setting with hello same thumbprint:</span></span>

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a><span data-ttu-id="63a48-265">Clientcertificaten uitgeven</span><span class="sxs-lookup"><span data-stu-id="63a48-265">Issue client certificates</span></span>
<span data-ttu-id="63a48-266">Elke afzonderlijke geautoriseerde tooaccess Hallo-service moet een certificaat uitgegeven voor his/hers exclusieve gebruik hebben en eigenaar his/hers tooprotect sterk wachtwoord van de persoonlijke sleutel moet kiezen.</span><span class="sxs-lookup"><span data-stu-id="63a48-266">Each individual authorized tooaccess hello service should have a client certificate issued for his/hers exclusive use and should choose his/hers own strong password tooprotect its private key.</span></span> 

<span data-ttu-id="63a48-267">Hallo stappen te volgen moet worden uitgevoerd in Hallo dezelfde machine waar Hallo zelfondertekend CA-certificaat is gegenereerd en worden opgeslagen:</span><span class="sxs-lookup"><span data-stu-id="63a48-267">hello following steps must be executed in hello same machine where hello self-signed CA certificate was generated and stored:</span></span>

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

<span data-ttu-id="63a48-268">Aanpassen:</span><span class="sxs-lookup"><span data-stu-id="63a48-268">Customizing:</span></span>

* <span data-ttu-id="63a48-269">-n met een ID voor toohello-client die met dit certificaat wordt geverifieerd</span><span class="sxs-lookup"><span data-stu-id="63a48-269">-n with an ID for toohello client that will be authenticated with this certificate</span></span>
* <span data-ttu-id="63a48-270">-e met Hallo certificaat verloopt</span><span class="sxs-lookup"><span data-stu-id="63a48-270">-e with hello certificate expiration date</span></span>
* <span data-ttu-id="63a48-271">MyID.pvk en MyID.cer met unieke bestandsnamen voor dit clientcertificaat</span><span class="sxs-lookup"><span data-stu-id="63a48-271">MyID.pvk and MyID.cer with unique filenames for this client certificate</span></span>

<span data-ttu-id="63a48-272">Met deze opdracht gevraagd een wachtwoord toobe gemaakt en vervolgens één keer worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="63a48-272">This command will prompt for a password toobe created and then used once.</span></span> <span data-ttu-id="63a48-273">Gebruik een sterk wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="63a48-273">Use a strong password.</span></span>

## <a name="create-pfx-files-for-client-certificates"></a><span data-ttu-id="63a48-274">PFX-bestanden voor client-certificaten maken</span><span class="sxs-lookup"><span data-stu-id="63a48-274">Create PFX files for client certificates</span></span>
<span data-ttu-id="63a48-275">Voor elk certificaat gegenereerde client uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="63a48-275">For each generated client certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="63a48-276">Aanpassen:</span><span class="sxs-lookup"><span data-stu-id="63a48-276">Customizing:</span></span>

    MyID.pvk and MyID.cer with hello filename for hello client certificate

<span data-ttu-id="63a48-277">Wachtwoord invoeren en exporteer het certificaat met deze opties:</span><span class="sxs-lookup"><span data-stu-id="63a48-277">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="63a48-278">Ja, Hallo persoonlijke sleutel exporteren</span><span class="sxs-lookup"><span data-stu-id="63a48-278">Yes, export hello private key</span></span>
* <span data-ttu-id="63a48-279">Alle uitgebreide eigenschappen exporteren</span><span class="sxs-lookup"><span data-stu-id="63a48-279">Export all extended properties</span></span>
* <span data-ttu-id="63a48-280">Hallo afzonderlijke toowhom die dit certificaat wordt uitgegeven moet Hallo export wachtwoord kiezen</span><span class="sxs-lookup"><span data-stu-id="63a48-280">hello individual toowhom this certificate is being issued should choose hello export password</span></span>

## <a name="import-client-certificate"></a><span data-ttu-id="63a48-281">Client-certificaat importeren</span><span class="sxs-lookup"><span data-stu-id="63a48-281">Import client certificate</span></span>
<span data-ttu-id="63a48-282">Elke gebruiker voor wie een clientcertificaat is uitgegeven Hallo-sleutelparen moet importeren in Hallo machines gebruikt hij toocommunicate met Hallo-service:</span><span class="sxs-lookup"><span data-stu-id="63a48-282">Each individual for whom a client certificate has been issued should import hello key pair in hello machines he/she will use toocommunicate with hello service:</span></span>

* <span data-ttu-id="63a48-283">Dubbelklik op Hallo. PFX-bestand in Windows Verkenner</span><span class="sxs-lookup"><span data-stu-id="63a48-283">Double-click hello .PFX file in Windows Explorer</span></span>
* <span data-ttu-id="63a48-284">Certificaat importeren in het persoonlijk archief met ten minste deze optie Hallo:</span><span class="sxs-lookup"><span data-stu-id="63a48-284">Import certificate into hello Personal store with at least this option:</span></span>
  * <span data-ttu-id="63a48-285">Alle uitgebreide eigenschappen ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="63a48-285">Include all extended properties checked</span></span>

## <a name="copy-client-certificate-thumbprints"></a><span data-ttu-id="63a48-286">Certificaatvingerafdrukken client kopiëren</span><span class="sxs-lookup"><span data-stu-id="63a48-286">Copy client certificate thumbprints</span></span>
<span data-ttu-id="63a48-287">Elke gebruiker voor wie een clientcertificaat is uitgegeven moet deze stappen in volgorde tooobtain Hallo vingerafdruk van his/hers certificaat dat wordt toegevoegd toohello serviceconfiguratiebestand:</span><span class="sxs-lookup"><span data-stu-id="63a48-287">Each individual for whom a client certificate has been issued must follow these steps in order tooobtain hello thumbprint of his/hers certificate which will be added toohello service configuration file:</span></span>

* <span data-ttu-id="63a48-288">Certmgr.exe uitvoeren</span><span class="sxs-lookup"><span data-stu-id="63a48-288">Run certmgr.exe</span></span>
* <span data-ttu-id="63a48-289">Selecteer Hallo persoonlijke tabblad</span><span class="sxs-lookup"><span data-stu-id="63a48-289">Select hello Personal tab</span></span>
* <span data-ttu-id="63a48-290">Dubbelklik op Hallo clientcertificaat toobe gebruikt voor verificatie</span><span class="sxs-lookup"><span data-stu-id="63a48-290">Double-click hello client certificate toobe used for authentication</span></span>
* <span data-ttu-id="63a48-291">Selecteer in het dialoogvenster Hallo certificaat dat wordt geopend, Hallo tabblad met Details</span><span class="sxs-lookup"><span data-stu-id="63a48-291">In hello Certificate dialog that opens, select hello Details tab</span></span>
* <span data-ttu-id="63a48-292">Controleer of dat weergeven alle wordt weergegeven</span><span class="sxs-lookup"><span data-stu-id="63a48-292">Make sure Show is displaying All</span></span>
* <span data-ttu-id="63a48-293">Selecteer Hallo veld met de naam van de vingerafdruk in Hallo lijst</span><span class="sxs-lookup"><span data-stu-id="63a48-293">Select hello field named Thumbprint in hello list</span></span>
* <span data-ttu-id="63a48-294">Hallo-waarde van de vingerafdruk van het Hallo kopiëren ** verwijderen van niet-zichtbare Unicode-tekens voor de eerste cijfer Hallo ** verwijdert alle spaties</span><span class="sxs-lookup"><span data-stu-id="63a48-294">Copy hello value of hello thumbprint ** Delete non-visible Unicode characters in front of hello first digit ** Delete all spaces</span></span>

## <a name="configure-allowed-clients-in-hello-service-configuration-file"></a><span data-ttu-id="63a48-295">Toegestane clients in het serviceconfiguratiebestand Hallo configureren</span><span class="sxs-lookup"><span data-stu-id="63a48-295">Configure Allowed clients in hello service configuration file</span></span>
<span data-ttu-id="63a48-296">Hallo-waarde van de volgende instelling in het serviceconfiguratiebestand een door komma's gescheiden lijst met vingerafdrukken Hallo van clientcertificaten Hallo toegestaan toohello-access-service Hallo Hallo bijwerken:</span><span class="sxs-lookup"><span data-stu-id="63a48-296">Update hello value of hello following setting in hello service configuration file with a comma-separated list of hello thumbprints of hello client certificates allowed access toohello service:</span></span>

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a><span data-ttu-id="63a48-297">Controle van certificaatintrekking client configureren</span><span class="sxs-lookup"><span data-stu-id="63a48-297">Configure client certificate revocation check</span></span>
<span data-ttu-id="63a48-298">de standaardinstelling Hallo controleert niet Hello certificeringsinstantie (CA) voor de clientstatus certificaat intrekken.</span><span class="sxs-lookup"><span data-stu-id="63a48-298">hello default setting does not check with hello Certification Authority for client certificate revocation status.</span></span> <span data-ttu-id="63a48-299">tooturn op Hallo controleert, als certificeringsinstantie (CA) die clientcertificaten Hallo afgegeven Hallo ondersteunt deze controles, Hallo instelling na met een van Hallo-waarden die zijn gedefinieerd in Hallo X509RevocationMode opsomming wijzigen:</span><span class="sxs-lookup"><span data-stu-id="63a48-299">tooturn on hello checks, if hello Certification Authority which issued hello client certificates supports such checks, change hello following setting with one of hello values defined in hello X509RevocationMode Enumeration:</span></span>

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a><span data-ttu-id="63a48-300">PFX-bestand voor zelfondertekende versleutelingscertificaten maken</span><span class="sxs-lookup"><span data-stu-id="63a48-300">Create PFX file for self-signed encryption certificates</span></span>
<span data-ttu-id="63a48-301">Voor een versleutelingscertificaat uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="63a48-301">For an encryption certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="63a48-302">Aanpassen:</span><span class="sxs-lookup"><span data-stu-id="63a48-302">Customizing:</span></span>

    MyID.pvk and MyID.cer with hello filename for hello encryption certificate

<span data-ttu-id="63a48-303">Wachtwoord invoeren en exporteer het certificaat met deze opties:</span><span class="sxs-lookup"><span data-stu-id="63a48-303">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="63a48-304">Ja, Hallo persoonlijke sleutel exporteren</span><span class="sxs-lookup"><span data-stu-id="63a48-304">Yes, export hello private key</span></span>
* <span data-ttu-id="63a48-305">Alle uitgebreide eigenschappen exporteren</span><span class="sxs-lookup"><span data-stu-id="63a48-305">Export all extended properties</span></span>
* <span data-ttu-id="63a48-306">U moet Hallo wachtwoord tijdens het uploaden van Hallo certificate toohello cloud-service.</span><span class="sxs-lookup"><span data-stu-id="63a48-306">You will need hello password when uploading hello certificate toohello cloud service.</span></span>

## <a name="export-encryption-certificate-from-certificate-store"></a><span data-ttu-id="63a48-307">Versleutelingscertificaat exporteren uit het certificaatarchief</span><span class="sxs-lookup"><span data-stu-id="63a48-307">Export encryption certificate from certificate store</span></span>
* <span data-ttu-id="63a48-308">Certificaat zoeken</span><span class="sxs-lookup"><span data-stu-id="63a48-308">Find certificate</span></span>
* <span data-ttu-id="63a48-309">Klik op Acties -> alle taken -> exporteren...</span><span class="sxs-lookup"><span data-stu-id="63a48-309">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="63a48-310">Exporteer het certificaat in een. PFX-bestand met deze opties:</span><span class="sxs-lookup"><span data-stu-id="63a48-310">Export certificate into a .PFX file with these options:</span></span> 
  * <span data-ttu-id="63a48-311">Ja, Hallo persoonlijke sleutel exporteren</span><span class="sxs-lookup"><span data-stu-id="63a48-311">Yes, export hello private key</span></span>
  * <span data-ttu-id="63a48-312">Indien mogelijk exporteren met alle certificaten in het certificeringspad Hallo</span><span class="sxs-lookup"><span data-stu-id="63a48-312">Include all certificates in hello certification path if possible</span></span> 
* <span data-ttu-id="63a48-313">Alle uitgebreide eigenschappen exporteren</span><span class="sxs-lookup"><span data-stu-id="63a48-313">Export all extended properties</span></span>

## <a name="upload-encryption-certificate-toocloud-service"></a><span data-ttu-id="63a48-314">Uploaden van de certificaatservice toocloud versleuteling</span><span class="sxs-lookup"><span data-stu-id="63a48-314">Upload encryption certificate toocloud service</span></span>
<span data-ttu-id="63a48-315">Upload het certificaat met de Hallo bestaande of gegenereerd. PFX-bestand met de Hallo versleuteling sleutelpaar:</span><span class="sxs-lookup"><span data-stu-id="63a48-315">Upload certificate with hello existing or generated .PFX file with hello encryption key pair:</span></span>

* <span data-ttu-id="63a48-316">Hallo-wachtwoord beveiligt persoonlijke sleutelgegevens Hallo invoeren</span><span class="sxs-lookup"><span data-stu-id="63a48-316">Enter hello password protecting hello private key information</span></span>

## <a name="update-encryption-certificate-in-service-configuration-file"></a><span data-ttu-id="63a48-317">Versleutelingscertificaat in het configuratiebestand van de service bijwerken</span><span class="sxs-lookup"><span data-stu-id="63a48-317">Update encryption certificate in service configuration file</span></span>
<span data-ttu-id="63a48-318">Update Hallo vingerafdrukwaarde van de volgende instellingen in het serviceconfiguratiebestand met de vingerafdruk van certificaat Hallo Hallo HALLO hallo geüpload toohello cloudservice:</span><span class="sxs-lookup"><span data-stu-id="63a48-318">Update hello thumbprint value of hello following settings in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a><span data-ttu-id="63a48-319">Algemene bewerkingen van het certificaat</span><span class="sxs-lookup"><span data-stu-id="63a48-319">Common certificate operations</span></span>
* <span data-ttu-id="63a48-320">Hallo SSL-certificaat configureren</span><span class="sxs-lookup"><span data-stu-id="63a48-320">Configure hello SSL certificate</span></span>
* <span data-ttu-id="63a48-321">Clientcertificaten configureren</span><span class="sxs-lookup"><span data-stu-id="63a48-321">Configure client certificates</span></span>

## <a name="find-certificate"></a><span data-ttu-id="63a48-322">Certificaat zoeken</span><span class="sxs-lookup"><span data-stu-id="63a48-322">Find certificate</span></span>
<span data-ttu-id="63a48-323">Volg deze stappen:</span><span class="sxs-lookup"><span data-stu-id="63a48-323">Follow these steps:</span></span>

1. <span data-ttu-id="63a48-324">Mmc.exe worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="63a48-324">Run mmc.exe.</span></span>
2. <span data-ttu-id="63a48-325">File -> module toevoegen/verwijderen...</span><span class="sxs-lookup"><span data-stu-id="63a48-325">File -> Add/Remove Snap-in…</span></span>
3. <span data-ttu-id="63a48-326">Selecteer **certificaten**.</span><span class="sxs-lookup"><span data-stu-id="63a48-326">Select **Certificates**.</span></span>
4. <span data-ttu-id="63a48-327">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="63a48-327">Click **Add**.</span></span>
5. <span data-ttu-id="63a48-328">Hallo certificaat store locatie kiezen.</span><span class="sxs-lookup"><span data-stu-id="63a48-328">Choose hello certificate store location.</span></span>
6. <span data-ttu-id="63a48-329">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="63a48-329">Click **Finish**.</span></span>
7. <span data-ttu-id="63a48-330">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="63a48-330">Click **OK**.</span></span>
8. <span data-ttu-id="63a48-331">Vouw **certificaten**.</span><span class="sxs-lookup"><span data-stu-id="63a48-331">Expand **Certificates**.</span></span>
9. <span data-ttu-id="63a48-332">Vouw Hallo certificaat store.</span><span class="sxs-lookup"><span data-stu-id="63a48-332">Expand hello certificate store node.</span></span>
10. <span data-ttu-id="63a48-333">Vouw Hallo certificaat onderliggend knooppunt.</span><span class="sxs-lookup"><span data-stu-id="63a48-333">Expand hello Certificate child node.</span></span>
11. <span data-ttu-id="63a48-334">Selecteer een certificaat in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="63a48-334">Select a certificate in hello list.</span></span>

## <a name="export-certificate"></a><span data-ttu-id="63a48-335">Certificaat exporteren</span><span class="sxs-lookup"><span data-stu-id="63a48-335">Export certificate</span></span>
<span data-ttu-id="63a48-336">In Hallo **Wizard Certificaat exporteren**:</span><span class="sxs-lookup"><span data-stu-id="63a48-336">In hello **Certificate Export Wizard**:</span></span>

1. <span data-ttu-id="63a48-337">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="63a48-337">Click **Next**.</span></span>
2. <span data-ttu-id="63a48-338">Selecteer **Ja**, klikt u vervolgens **Export Hallo persoonlijke sleutel**.</span><span class="sxs-lookup"><span data-stu-id="63a48-338">Select **Yes**, then **Export hello private key**.</span></span>
3. <span data-ttu-id="63a48-339">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="63a48-339">Click **Next**.</span></span>
4. <span data-ttu-id="63a48-340">Selecteer Hallo gewenste uitvoer-bestandsindeling.</span><span class="sxs-lookup"><span data-stu-id="63a48-340">Select hello desired output file format.</span></span>
5. <span data-ttu-id="63a48-341">Selectievakje Hallo gewenste opties.</span><span class="sxs-lookup"><span data-stu-id="63a48-341">Check hello desired options.</span></span>
6. <span data-ttu-id="63a48-342">Controleer **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="63a48-342">Check **Password**.</span></span>
7. <span data-ttu-id="63a48-343">Voer een sterk wachtwoord in en Bevestig het.</span><span class="sxs-lookup"><span data-stu-id="63a48-343">Enter a strong password and confirm it.</span></span>
8. <span data-ttu-id="63a48-344">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="63a48-344">Click **Next**.</span></span>
9. <span data-ttu-id="63a48-345">Typ of blader een bestandsnaam waar toostore certificaat Hallo (gebruik een. PFX-extensie).</span><span class="sxs-lookup"><span data-stu-id="63a48-345">Type or browse a filename where toostore hello certificate (use a .PFX extension).</span></span>
10. <span data-ttu-id="63a48-346">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="63a48-346">Click **Next**.</span></span>
11. <span data-ttu-id="63a48-347">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="63a48-347">Click **Finish**.</span></span>
12. <span data-ttu-id="63a48-348">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="63a48-348">Click **OK**.</span></span>

## <a name="import-certificate"></a><span data-ttu-id="63a48-349">Certificaat importeren</span><span class="sxs-lookup"><span data-stu-id="63a48-349">Import certificate</span></span>
<span data-ttu-id="63a48-350">Hallo in de Wizard Certificaat importeren:</span><span class="sxs-lookup"><span data-stu-id="63a48-350">In hello Certificate Import Wizard:</span></span>

1. <span data-ttu-id="63a48-351">Selecteer Hallo opslaglocatie.</span><span class="sxs-lookup"><span data-stu-id="63a48-351">Select hello store location.</span></span>
   
   * <span data-ttu-id="63a48-352">Selecteer **huidige gebruiker** als alleen de processen die worden uitgevoerd onder de huidige gebruiker heeft toegang tot Hallo-service</span><span class="sxs-lookup"><span data-stu-id="63a48-352">Select **Current User** if only processes running under current user will access hello service</span></span>
   * <span data-ttu-id="63a48-353">Selecteer **lokale Machine** als andere processen in deze computer toegang Hallo-service tot heeft</span><span class="sxs-lookup"><span data-stu-id="63a48-353">Select **Local Machine** if other processes in this computer will access hello service</span></span>
2. <span data-ttu-id="63a48-354">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="63a48-354">Click **Next**.</span></span>
3. <span data-ttu-id="63a48-355">Als importeren uit een bestand, controleert u het bestandspad Hallo.</span><span class="sxs-lookup"><span data-stu-id="63a48-355">If importing from a file, confirm hello file path.</span></span>
4. <span data-ttu-id="63a48-356">Als u deze importeert een. PFX-bestand:</span><span class="sxs-lookup"><span data-stu-id="63a48-356">If importing a .PFX file:</span></span>
   1. <span data-ttu-id="63a48-357">Bescherming van persoonlijke sleutel Hallo Hallo-wachtwoord invoeren</span><span class="sxs-lookup"><span data-stu-id="63a48-357">Enter hello password protecting hello private key</span></span>
   2. <span data-ttu-id="63a48-358">Selecteer opties voor importeren</span><span class="sxs-lookup"><span data-stu-id="63a48-358">Select import options</span></span>
5. <span data-ttu-id="63a48-359">Selecteer "Locatie" certificaten in Hallo na store</span><span class="sxs-lookup"><span data-stu-id="63a48-359">Select "Place" certificates in hello following store</span></span>
6. <span data-ttu-id="63a48-360">Klik op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="63a48-360">Click **Browse**.</span></span>
7. <span data-ttu-id="63a48-361">Selecteer de gewenste winkel Hallo.</span><span class="sxs-lookup"><span data-stu-id="63a48-361">Select hello desired store.</span></span>
8. <span data-ttu-id="63a48-362">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="63a48-362">Click **Finish**.</span></span>
   
   * <span data-ttu-id="63a48-363">Als Hallo vertrouwde basiscertificeringsinstanties hebt gekozen, klikt u op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="63a48-363">If hello Trusted Root Certification Authority store was chosen, click **Yes**.</span></span>
9. <span data-ttu-id="63a48-364">Klik op **OK** op alle vensters van het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="63a48-364">Click **OK** on all dialog windows.</span></span>

## <a name="upload-certificate"></a><span data-ttu-id="63a48-365">Certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="63a48-365">Upload certificate</span></span>
<span data-ttu-id="63a48-366">In Hallo [Azure Portal](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="63a48-366">In hello [Azure Portal](https://portal.azure.com/)</span></span>

1. <span data-ttu-id="63a48-367">Selecteer **Cloudservices**.</span><span class="sxs-lookup"><span data-stu-id="63a48-367">Select **Cloud Services**.</span></span>
2. <span data-ttu-id="63a48-368">Hallo-cloudservice selecteren.</span><span class="sxs-lookup"><span data-stu-id="63a48-368">Select hello cloud service.</span></span>
3. <span data-ttu-id="63a48-369">Klik op het bovenste menu Hallo **certificaten**.</span><span class="sxs-lookup"><span data-stu-id="63a48-369">On hello top menu, click **Certificates**.</span></span>
4. <span data-ttu-id="63a48-370">Klik op de balk onderaan hello, **uploaden**.</span><span class="sxs-lookup"><span data-stu-id="63a48-370">On hello bottom bar, click **Upload**.</span></span>
5. <span data-ttu-id="63a48-371">Hallo-certificaatbestand selecteren.</span><span class="sxs-lookup"><span data-stu-id="63a48-371">Select hello certificate file.</span></span>
6. <span data-ttu-id="63a48-372">Als het is een. PFX-bestand, Hallo wachtwoord invoeren voor de persoonlijke sleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="63a48-372">If it is a .PFX file, enter hello password for hello private key.</span></span>
7. <span data-ttu-id="63a48-373">Als voltooid, kopiëren van de certificaatvingerafdruk Hallo van Hallo nieuw item in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="63a48-373">Once completed, copy hello certificate thumbprint from hello new entry in hello list.</span></span>

## <a name="other-security-considerations"></a><span data-ttu-id="63a48-374">Andere beveiligingsoverwegingen</span><span class="sxs-lookup"><span data-stu-id="63a48-374">Other security considerations</span></span>
<span data-ttu-id="63a48-375">Hallo SSL-instellingen in dit document beschreven versleutelen van communicatie tussen het Hallo-service en de clients wanneer Hallo HTTPS-eindpunt wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="63a48-375">hello SSL settings described in this document encrypt communication between hello service and its clients when hello HTTPS endpoint is used.</span></span> <span data-ttu-id="63a48-376">Dit is belangrijk omdat de referenties voor toegang tot de database en mogelijk andere vertrouwelijke informatie zijn opgenomen in het Hallo-communicatie.</span><span class="sxs-lookup"><span data-stu-id="63a48-376">This is important since credentials for database access and potentially other sensitive information are contained in hello communication.</span></span> <span data-ttu-id="63a48-377">Let echter op Hallo service interne status, inclusief referenties, in de interne tabellen in Hallo Microsoft Azure SQL database die u hebt opgegeven voor de metagegevensopslag van in uw Microsoft Azure-abonnement zich blijft voordoen.</span><span class="sxs-lookup"><span data-stu-id="63a48-377">Note, however, that hello service persists internal status, including credentials, in its internal tables in hello Microsoft Azure SQL database that you have provided for metadata storage in your Microsoft Azure subscription.</span></span> <span data-ttu-id="63a48-378">Deze database is gedefinieerd als onderdeel van de volgende instelling in uw serviceconfiguratiebestand hello (. CSCFG-bestand):</span><span class="sxs-lookup"><span data-stu-id="63a48-378">That database was defined as part of hello following setting in your service configuration file (.CSCFG file):</span></span> 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

<span data-ttu-id="63a48-379">In deze database opgeslagen referenties zijn versleuteld.</span><span class="sxs-lookup"><span data-stu-id="63a48-379">Credentials stored in this database are encrypted.</span></span> <span data-ttu-id="63a48-380">Echter als een best practice voor zorgen dat de web- en werkrollen rollen van uw service-implementaties up toodate blijven en veilig zijn als ze beide toegang toohello metagegevens database en het Hallo-certificaat gebruikt voor versleuteling en ontsleuteling van opgeslagen referenties hebben.</span><span class="sxs-lookup"><span data-stu-id="63a48-380">However, as a best practice, ensure that both web and worker roles of your service deployments are kept up toodate and secure as they both have access toohello metadata database and hello certificate used for encryption and decryption of stored credentials.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

