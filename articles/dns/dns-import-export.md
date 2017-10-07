---
title: aaaImport en exporteren van een domeinzone tooAzure DNS met Azure CLI 1.0-bestand | Microsoft Docs
description: Meer informatie over hoe tooimport en een DNS-server exporteren bestand tooAzure DNS-zone met behulp van Azure CLI 1.0
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: f5797782-3005-4663-a488-ac0089809010
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 4c3163395e151e9934c730349b828c612491016f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-a-dns-zone-file-using-hello-azure-cli-10"></a><span data-ttu-id="1d3d1-103">Importeren en exporteren van een DNS-zonebestand met hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1d3d1-103">Import and export a DNS zone file using hello Azure CLI 1.0</span></span> 

<span data-ttu-id="1d3d1-104">In dit artikel leert u hoe tooimport en exporteren DNS-zone-bestanden voor het gebruik van Azure DNS hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-104">This article walks you through how tooimport and export DNS zone files for Azure DNS using hello Azure CLI 1.0.</span></span>

## <a name="introduction-toodns-zone-migration"></a><span data-ttu-id="1d3d1-105">Inleiding tooDNS zone migratie</span><span class="sxs-lookup"><span data-stu-id="1d3d1-105">Introduction tooDNS zone migration</span></span>

<span data-ttu-id="1d3d1-106">Een DNS-zonebestand is een tekstbestand met de details van elke record System DNS (Domain Name) in Hallo zone.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-106">A DNS zone file is a text file that contains details of every Domain Name System (DNS) record in hello zone.</span></span> <span data-ttu-id="1d3d1-107">Volgt een standaardindeling, waardoor het geschikt is voor de DNS-records overbrengen tussen DNS-systemen.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-107">It follows a standard format, making it suitable for transferring DNS records between DNS systems.</span></span> <span data-ttu-id="1d3d1-108">Met behulp van een zonebestand is een snelle, betrouwbare, en een handige manier tootransfer een DNS-zone van of naar Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-108">Using a zone file is a quick, reliable, and convenient way tootransfer a DNS zone into or out of Azure DNS.</span></span>

<span data-ttu-id="1d3d1-109">Azure DNS ondersteunt importeren en exporteren van de zone-bestanden met behulp van hello Azure-opdrachtregelinterface (CLI).</span><span class="sxs-lookup"><span data-stu-id="1d3d1-109">Azure DNS supports importing and exporting zone files by using hello Azure command-line interface (CLI).</span></span> <span data-ttu-id="1d3d1-110">Zone-bestand importeren is **niet** momenteel ondersteund via Azure PowerShell of hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-110">Zone file import is **not** currently supported via Azure PowerShell or hello Azure portal.</span></span>

<span data-ttu-id="1d3d1-111">Hello Azure CLI 1.0 is een platformoverschrijdende opdrachtregel-hulpprogramma gebruikt voor het beheer van Azure-services.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-111">hello Azure CLI 1.0 is a cross-platform command-line tool used for managing Azure services.</span></span> <span data-ttu-id="1d3d1-112">Is beschikbaar voor Windows, Mac en Linux platforms Hallo van Hallo [pagina Azure downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1d3d1-112">It is available for hello Windows, Mac, and Linux platforms from hello [Azure downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="1d3d1-113">Ondersteuning voor meerdere platforms is belangrijk voor importeren en exporteren van zonebestanden, omdat de meest voorkomende naam serversoftware Hallo [BINDEN](https://www.isc.org/downloads/bind/), doorgaans op Linux wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-113">Cross-platform support is important for importing and exporting zone files, because hello most common name server software, [BIND](https://www.isc.org/downloads/bind/), typically runs on Linux.</span></span>

> [!NOTE]
> <span data-ttu-id="1d3d1-114">Er zijn twee versies van hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-114">There are currently two versions of hello Azure CLI.</span></span> <span data-ttu-id="1d3d1-115">CLI1.0 is gebaseerd op Node.js en opdrachten die beginnen met 'azure' is.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-115">CLI1.0 is based on Node.js, and has commands beginning with "azure".</span></span>
> <span data-ttu-id="1d3d1-116">CLI2.0 is gebaseerd op Python en opdrachten die beginnen met 'az' heeft.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-116">CLI2.0 is based on Python and has commands beginning with "az".</span></span> <span data-ttu-id="1d3d1-117">Zone-bestand importeren in beide versies wordt ondersteund, wordt u aangeraden Hallo CLI1.0 opdrachten, zoals beschreven in deze pagina.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-117">While zone file import is supported in both versions, we recommend using hello CLI1.0 commands, as described in this page.</span></span>

## <a name="obtain-your-existing-dns-zone-file"></a><span data-ttu-id="1d3d1-118">Verkrijgen van uw bestaande DNS-zonebestand</span><span class="sxs-lookup"><span data-stu-id="1d3d1-118">Obtain your existing DNS zone file</span></span>

<span data-ttu-id="1d3d1-119">Voordat u een DNS-zone-bestand in Azure DNS importeren, moet u een kopie van het Hallo-zonebestand tooobtain.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-119">Before you import a DNS zone file into Azure DNS, you need tooobtain a copy of hello zone file.</span></span> <span data-ttu-id="1d3d1-120">Hallo-bron van dit bestand is afhankelijk van waar momenteel Hallo DNS-zone wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-120">hello source of this file depends on where hello DNS zone is currently hosted.</span></span>

* <span data-ttu-id="1d3d1-121">Als uw DNS-zone wordt gehost door een partner-service (zoals een domeinregistrar, specifieke DNS-hostingprovider of alternatieve cloudprovider), leveren die service DNS-zonebestand voor Hallo mogelijkheid toodownload Hallo.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-121">If your DNS zone is hosted by a partner service (such as a domain registrar, dedicated DNS hosting provider, or alternative cloud provider), that service should provide hello ability toodownload hello DNS zone file.</span></span>
* <span data-ttu-id="1d3d1-122">Als uw DNS-zone wordt gehost op Windows DNS, Hallo standaard wordt de map voor Hallo zonebestanden **%systemroot%\system32\dns**.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-122">If your DNS zone is hosted on Windows DNS, hello default folder for hello zone files is **%systemroot%\system32\dns**.</span></span> <span data-ttu-id="1d3d1-123">Hallo volledig pad tooeach zone-bestand bevat ook op Hallo **algemene** tabblad van Hallo DNS-console.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-123">hello full path tooeach zone file also shows on hello **General** tab of hello DNS console.</span></span>
* <span data-ttu-id="1d3d1-124">Als uw DNS-zone wordt gehost met behulp van BIND, Hallo-locatie van Hallo-zonebestand voor elke zone wordt opgegeven in het configuratiebestand voor BIND Hallo **named.conf**.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-124">If your DNS zone is hosted by using BIND, hello location of hello zone file for each zone is specified in hello BIND configuration file **named.conf**.</span></span>

> [!NOTE]
> <span data-ttu-id="1d3d1-125">Zone-bestanden die zijn gedownload van GoDaddy hebben een iets andere indeling.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-125">Zone files downloaded from GoDaddy have a slightly nonstandard format.</span></span> <span data-ttu-id="1d3d1-126">U moet toocorrect dit voordat u deze zonebestanden in Azure DNS importeren.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-126">You need toocorrect this before you import these zone files into Azure DNS.</span></span>
>
> <span data-ttu-id="1d3d1-127">DNS-namen in Hallo RDATA van elke DNS-record zijn opgegeven als FQDN-namen, maar ze niet beschikken over een afsluitende '. ' Dit betekent dat ze worden geïnterpreteerd door andere DNS-systemen als relatieve namen.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-127">DNS names in hello RDATA of each DNS record are specified as fully qualified names, but they don't have a terminating "." This means they are interpreted by other DNS systems as relative names.</span></span> <span data-ttu-id="1d3d1-128">U moet tooedit Hallo zone bestand tooappend Hallo beëindigd '. ' tootheir namen voordat u ze in Azure DNS importeren.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-128">You need tooedit hello zone file tooappend hello terminating "." tootheir names before you import them into Azure DNS.</span></span>
>
> <span data-ttu-id="1d3d1-129">Bijvoorbeeld, CNAME-record 'www 3600 IN CNAME contoso.com' hello te moet worden gewijzigd 'www 3600 IN CNAME contoso.com'.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-129">For example, hello CNAME record "www 3600 IN CNAME contoso.com" should be changed too"www 3600 IN CNAME contoso.com."</span></span>
> <span data-ttu-id="1d3d1-130">(met een afsluitende '. ').</span><span class="sxs-lookup"><span data-stu-id="1d3d1-130">(with a terminating ".").</span></span>

## <a name="import-a-dns-zone-file-into-azure-dns"></a><span data-ttu-id="1d3d1-131">Een DNS-zone-bestand importeren in Azure DNS</span><span class="sxs-lookup"><span data-stu-id="1d3d1-131">Import a DNS zone file into Azure DNS</span></span>

<span data-ttu-id="1d3d1-132">Maakt een nieuwe zone een zonebestand te importeren in Azure DNS, als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-132">Importing a zone file creates a new zone in Azure DNS if one does not already exist.</span></span> <span data-ttu-id="1d3d1-133">Als de zone Hallo al bestaat, moeten hello recordsets in Hallo zonebestand worden samengevoegd met de bestaande recordsets Hallo.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-133">If hello zone already exists, hello record sets in hello zone file must be merged with hello existing record sets.</span></span>

### <a name="merge-behavior"></a><span data-ttu-id="1d3d1-134">Samenvoegen van gedrag</span><span class="sxs-lookup"><span data-stu-id="1d3d1-134">Merge behavior</span></span>

* <span data-ttu-id="1d3d1-135">Standaard worden bestaande en nieuwe recordsets samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-135">By default, existing and new record sets are merged.</span></span> <span data-ttu-id="1d3d1-136">Identieke records binnen een samengevoegde Recordset zijn ongedaan gedupliceerde.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-136">Identical records within a merged record set are de-duplicated.</span></span>
* <span data-ttu-id="1d3d1-137">U kunt ook door op te geven Hallo `--force` optie, Hallo importeren proces vervangt bestaande recordsets met nieuwe recordsets.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-137">Alternatively, by specifying hello `--force` option, hello import process replaces existing record sets with new record sets.</span></span> <span data-ttu-id="1d3d1-138">Bestaande recordsets waarvoor geen overeenkomende recordset in de geïmporteerde zonebestand Hallo worden niet verwijderd.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-138">Existing record sets that do not have a corresponding record set in hello imported zone file are not be removed.</span></span>
* <span data-ttu-id="1d3d1-139">Als recordsets worden samengevoegd, wordt hello toolive TTL (time) van de bestaande recordsets gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-139">When record sets are merged, hello time toolive (TTL) of preexisting record sets is used.</span></span> <span data-ttu-id="1d3d1-140">Wanneer `--force` wordt gebruikt, Hallo TTL van de nieuwe recordset hello wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-140">When `--force` is used, hello TTL of hello new record set is used.</span></span>
* <span data-ttu-id="1d3d1-141">Parameters Authority (SOA) is gestart (behalve `host`) altijd onttrokken Hallo geïmporteerde zone-bestand, ongeacht of `--force` wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-141">Start of Authority (SOA) parameters (except `host`) are always taken from hello imported zone file, regardless of whether `--force` is used.</span></span> <span data-ttu-id="1d3d1-142">Op deze manier voor Hallo naamserverrecord ingesteld in het toppunt zone hello, hello TTL altijd overgenomen uit Hallo geïmporteerde zone-bestand.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-142">Similarly, for hello name server record set at hello zone apex, hello TTL is always taken from hello imported zone file.</span></span>
* <span data-ttu-id="1d3d1-143">Een geïmporteerde CNAME-record is geen vervanging voor een bestaande CNAME record met dezelfde naam tenzij Hallo Hallo `--force` parameter wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-143">An imported CNAME record does not replace an existing CNAME record with hello same name unless hello `--force` parameter is specified.</span></span>
* <span data-ttu-id="1d3d1-144">Als een conflict optreedt tussen een CNAME-record en een andere record Hallo dezelfde naam maar een ander type (ongeacht die is bestaande of nieuwe), Hallo bestaande record wordt bewaard.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-144">When a conflict arises between a CNAME record and another record of hello same name but different type (regardless of which is existing or new), hello existing record is retained.</span></span> <span data-ttu-id="1d3d1-145">Dit is onafhankelijk van het gebruik van Hallo `--force`.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-145">This is independent of hello use of `--force`.</span></span>

### <a name="additional-information-about-importing"></a><span data-ttu-id="1d3d1-146">Als u meer informatie over het importeren</span><span class="sxs-lookup"><span data-stu-id="1d3d1-146">Additional information about importing</span></span>

<span data-ttu-id="1d3d1-147">Hallo bieden opmerkingen bij de volgende aanvullende technische gegevens over Hallo zone importeren.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-147">hello following notes provide additional technical details about hello zone import process.</span></span>

* <span data-ttu-id="1d3d1-148">Hallo `$TTL` richtlijn is optioneel en wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-148">hello `$TTL` directive is optional, and it is supported.</span></span> <span data-ttu-id="1d3d1-149">Als er geen `$TTL` richtlijn krijgt, records zonder een expliciete TTL worden geïmporteerd tooa standaard TTL 3600 seconden instellen.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-149">When no `$TTL` directive is given, records without an explicit TTL are imported set tooa default TTL of 3600 seconds.</span></span> <span data-ttu-id="1d3d1-150">Wanneer twee registreert in hello dezelfde recordset Geef andere TTLs, Hallo lagere waarde wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-150">When two records in hello same record set specify different TTLs, hello lower value is used.</span></span>
* <span data-ttu-id="1d3d1-151">Hallo `$ORIGIN` richtlijn is optioneel en wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-151">hello `$ORIGIN` directive is optional, and it is supported.</span></span> <span data-ttu-id="1d3d1-152">Als er geen `$ORIGIN` is ingesteld, Hallo standaard gebruikte waarde is de zonenaam Hallo die is opgegeven op de opdrachtregel Hallo (plus hello wordt beëindigd '. ').</span><span class="sxs-lookup"><span data-stu-id="1d3d1-152">When no `$ORIGIN` is set, hello default value used is hello zone name as specified on hello command line (plus hello terminating ".").</span></span>
* <span data-ttu-id="1d3d1-153">Hallo `$INCLUDE` en `$GENERATE` richtlijnen worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-153">hello `$INCLUDE` and `$GENERATE` directives are not supported.</span></span>
* <span data-ttu-id="1d3d1-154">Deze typen worden ondersteund: A, AAAA, CNAME, MX, NS, SOA, SRV en TXT.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-154">These record types are supported: A, AAAA, CNAME, MX, NS, SOA, SRV, and TXT.</span></span>
* <span data-ttu-id="1d3d1-155">Hallo SOA-record wordt automatisch gemaakt door Azure DNS wanneer u een zone wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-155">hello SOA record is created automatically by Azure DNS when a zone is created.</span></span> <span data-ttu-id="1d3d1-156">Wanneer u een zonebestand importeert, alle SOA-parameters zijn afkomstig uit Hallo zonebestand *behalve* hello `host` parameter.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-156">When you import a zone file, all SOA parameters are taken from hello zone file *except* hello `host` parameter.</span></span> <span data-ttu-id="1d3d1-157">Hallo-waarde die door Azure DNS maakt gebruik van deze parameter.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-157">This parameter uses hello value provided by Azure DNS.</span></span> <span data-ttu-id="1d3d1-158">Dit is omdat deze parameter moet toohello de naam van de primaire server is verstrekt door Azure DNS verwijzen.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-158">This is because this parameter must refer toohello primary name server provided by Azure DNS.</span></span>
* <span data-ttu-id="1d3d1-159">Hallo naamserverrecord ingesteld in het toppunt Hallo zone wordt ook automatisch gemaakt door Azure DNS als Hallo zone wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-159">hello name server record set at hello zone apex is also created automatically by Azure DNS when hello zone is created.</span></span> <span data-ttu-id="1d3d1-160">Alleen is hello TTL van deze recordset geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-160">Only hello TTL of this record set is imported.</span></span> <span data-ttu-id="1d3d1-161">Deze records bevatten Hallo naamservernamen verstrekt door Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-161">These records contain hello name server names provided by Azure DNS.</span></span> <span data-ttu-id="1d3d1-162">Hallo gegevens niet wordt overschreven door de waarden in de geïmporteerde zonebestand Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-162">hello record data is not overwritten by hello values contained in hello imported zone file.</span></span>
* <span data-ttu-id="1d3d1-163">Azure DNS biedt ondersteuning voor slechts één tekenreeks TXT-records tijdens de openbare Preview.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-163">During Public Preview, Azure DNS supports only single-string TXT records.</span></span> <span data-ttu-id="1d3d1-164">Multistring TXT-records zijn aaneengeschakelde en afgekapte too255 tekens zijn.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-164">Multistring TXT records are be concatenated and truncated too255 characters.</span></span>

### <a name="cli-format-and-values"></a><span data-ttu-id="1d3d1-165">CLI-indeling en waarden</span><span class="sxs-lookup"><span data-stu-id="1d3d1-165">CLI format and values</span></span>

<span data-ttu-id="1d3d1-166">Hallo-indeling van hello Azure CLI opdracht tooimport een DNS-zone is:</span><span class="sxs-lookup"><span data-stu-id="1d3d1-166">hello format of hello Azure CLI command tooimport a DNS zone is:</span></span>

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="1d3d1-167">Waarden:</span><span class="sxs-lookup"><span data-stu-id="1d3d1-167">Values:</span></span>

* <span data-ttu-id="1d3d1-168">`<resource group>`Hallo naam van resourcegroep Hallo Hallo zone in Azure DNS is.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-168">`<resource group>` is hello name of hello resource group for hello zone in Azure DNS.</span></span>
* <span data-ttu-id="1d3d1-169">`<zone name>`Hallo-naam van Hallo zone is.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-169">`<zone name>` is hello name of hello zone.</span></span>
* <span data-ttu-id="1d3d1-170">`<zone file name>`Hallo padnaam van Hallo zone bestand toobe geïmporteerd is.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-170">`<zone file name>` is hello path/name of hello zone file toobe imported.</span></span>

<span data-ttu-id="1d3d1-171">Als een zone met deze naam niet in de resourcegroep hello bestaat, wordt deze voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-171">If a zone with this name does not exist in hello resource group, it is created for you.</span></span> <span data-ttu-id="1d3d1-172">Als hello zone al bestaat, worden hello geïmporteerde recordsets samengevoegd met bestaande recordsets.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-172">If hello zone already exists, hello imported record sets are merged with existing record sets.</span></span> <span data-ttu-id="1d3d1-173">toooverwrite hello bestaande recordsets, gebruik Hallo `--force` optie.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-173">toooverwrite hello existing record sets, use hello `--force` option.</span></span>

<span data-ttu-id="1d3d1-174">tooverify hello indeling van een zonebestand zonder het, gebruik Hallo daadwerkelijk geïmporteerd `--parse-only` optie.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-174">tooverify hello format of a zone file without actually importing it, use hello `--parse-only` option.</span></span>

### <a name="step-1-import-a-zone-file"></a><span data-ttu-id="1d3d1-175">Step 1.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-175">Step 1.</span></span> <span data-ttu-id="1d3d1-176">Een zonebestand importeren</span><span class="sxs-lookup"><span data-stu-id="1d3d1-176">Import a zone file</span></span>

<span data-ttu-id="1d3d1-177">een zonebestand voor Hallo zone tooimport **contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-177">tooimport a zone file for hello zone **contoso.com**.</span></span>

1. <span data-ttu-id="1d3d1-178">Meld u tooyour Azure-abonnement met behulp van hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-178">Sign in tooyour Azure subscription by using hello Azure CLI 1.0.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="1d3d1-179">Selecteer waar u toocreate uw nieuwe DNS-zone Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-179">Select hello subscription where you want toocreate your new DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="1d3d1-180">Azure DNS is een Azure Resource Manager alleen-lezen-service zodat hello Azure CLI uitgeschakeld tooResource Manager-modus zijn moet.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-180">Azure DNS is an Azure Resource Manager-only service, so hello Azure CLI must be switched tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="1d3d1-181">Voordat u hello Azure DNS-service gebruiken, moet u uw abonnement toouse hello Microsoft.Network-resourceprovider registreren.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-181">Before you use hello Azure DNS service, you must register your subscription toouse hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="1d3d1-182">(Dit is een eenmalige bewerking voor elk abonnement.)</span><span class="sxs-lookup"><span data-stu-id="1d3d1-182">(This is a one-time operation for each subscription.)</span></span>

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. <span data-ttu-id="1d3d1-183">Als u nog geen een hebt, moet u ook toocreate een Resource Manager-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-183">If you don't have one already, you also need toocreate a Resource Manager resource group.</span></span>

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. <span data-ttu-id="1d3d1-184">tooimport hello zone **contoso.com** uit bestand Hallo **contoso.com.txt** in een nieuwe DNS-zone in de resourcegroep Hallo **myresourcegroup**, Voer Hallo opdracht `azure network dns zone import`.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-184">tooimport hello zone **contoso.com** from hello file **contoso.com.txt** into a new DNS zone in hello resource group **myresourcegroup**, run hello command `azure network dns zone import`.</span></span><BR><span data-ttu-id="1d3d1-185">Met deze opdracht wordt geladen Hallo zone-bestand en het parseren.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-185">This command loads hello zone file and parse it.</span></span> <span data-ttu-id="1d3d1-186">Hallo-opdracht wordt een reeks opdrachten uitgevoerd op Hallo Azure DNS-service toocreate Hallo zone en alle Hallo recordsets in Hallo zone.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-186">hello command executes a series of commands on hello Azure DNS service toocreate hello zone and all hello record sets in hello zone.</span></span> <span data-ttu-id="1d3d1-187">Hallo opdracht rapporten voortgang in Hallo-consolevenster, samen met eventuele fouten of waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-187">hello command reports progress in hello console window, along with any errors or warnings.</span></span> <span data-ttu-id="1d3d1-188">Omdat recordsets zijn gemaakt in de reeks, duurt het enkele minuten tooimport een grote zone-bestand.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-188">Because record sets are created in series, it may take a few minutes tooimport a large zone file.</span></span>

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-hello-zone"></a><span data-ttu-id="1d3d1-189">Stap 2.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-189">Step 2.</span></span> <span data-ttu-id="1d3d1-190">Controleer of de zone Hallo</span><span class="sxs-lookup"><span data-stu-id="1d3d1-190">Verify hello zone</span></span>

<span data-ttu-id="1d3d1-191">tooverify hello DNS-zone nadat u Hallo-bestand importeren, kunt u een van de volgende methoden Hallo:</span><span class="sxs-lookup"><span data-stu-id="1d3d1-191">tooverify hello DNS zone after you import hello file, you can use any one of hello following methods:</span></span>

* <span data-ttu-id="1d3d1-192">U kunt Hallo records weergeven met behulp van hello Azure CLI-opdracht te volgen:</span><span class="sxs-lookup"><span data-stu-id="1d3d1-192">You can list hello records by using hello following Azure CLI command:</span></span>

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* <span data-ttu-id="1d3d1-193">U kunt Hallo records weergeven met behulp van PowerShell-cmdlet Hallo `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-193">You can list hello records by using hello PowerShell cmdlet `Get-AzureRmDnsRecordSet`.</span></span>
* <span data-ttu-id="1d3d1-194">U kunt `nslookup` tooverify naamomzetting voor Hallo records.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-194">You can use `nslookup` tooverify name resolution for hello records.</span></span> <span data-ttu-id="1d3d1-195">Omdat Hallo zone nog niet is toegewezen, moet u toospecify Hallo juiste Azure DNS-naamservers expliciet.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-195">Because hello zone isn't delegated yet, you need toospecify hello correct Azure DNS name servers explicitly.</span></span> <span data-ttu-id="1d3d1-196">Hallo volgende voorbeeld toont hoe tooretrieve hello naamservernamen toohello zone toegewezen.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-196">hello following sample shows how tooretrieve hello name server names assigned toohello zone.</span></span> <span data-ttu-id="1d3d1-197">IT ook ziet u hoe tooquery Hallo 'www' vastleggen met behulp van `nslookup`.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-197">IT also shows how tooquery hello "www" record by using `nslookup`.</span></span>

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up hello DNS Record Set "@" of type "NS"
        data:Id: /subscriptions/.../resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com/NS/@
        data:Name: @
        data:Type: Microsoft.Network/dnszones/NS
        data:Location: global
        data:TTL : 3600
        data:NS records
        data:Name server domain name : ns1-01.azure-dns.com
        data:Name server domain name : ns2-01.azure-dns.net
        data:Name server domain name : ns3-01.azure-dns.org
        data:Name server domain name : ns4-01.azure-dns.info
        data:
        info:network dns record-set show command OK

        C:\> nslookup www.contoso.com ns1-01.azure-dns.com

        Server: ns1-01.azure-dns.com
        Address:  40.90.4.1

        Name:www.contoso.com
        Addresses:  134.170.185.46
        134.170.188.221

### <a name="step-3-update-dns-delegation"></a><span data-ttu-id="1d3d1-198">Stap 3.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-198">Step 3.</span></span> <span data-ttu-id="1d3d1-199">DNS-delegering bijwerken</span><span class="sxs-lookup"><span data-stu-id="1d3d1-199">Update DNS delegation</span></span>

<span data-ttu-id="1d3d1-200">Nadat u hebt gecontroleerd dat Hallo zone correct is geïmporteerd, moet u tooupdate Hallo DNS-delegering toopoint toohello naamservers Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-200">After you have verified that hello zone has been imported correctly, you need tooupdate hello DNS delegation toopoint toohello Azure DNS name servers.</span></span> <span data-ttu-id="1d3d1-201">Zie voor meer informatie artikel Hallo [Hallo DNS-delegering bijwerken](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="1d3d1-201">For more information, see hello article [Update hello DNS delegation](dns-domain-delegation.md).</span></span>

## <a name="export-a-dns-zone-file-from-azure-dns"></a><span data-ttu-id="1d3d1-202">Een DNS-zone-bestand exporteren uit Azure DNS</span><span class="sxs-lookup"><span data-stu-id="1d3d1-202">Export a DNS zone file from Azure DNS</span></span>

<span data-ttu-id="1d3d1-203">Hallo-indeling van hello Azure CLI opdracht tooimport een DNS-zone is:</span><span class="sxs-lookup"><span data-stu-id="1d3d1-203">hello format of hello Azure CLI command tooimport a DNS zone is:</span></span>

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="1d3d1-204">Waarden:</span><span class="sxs-lookup"><span data-stu-id="1d3d1-204">Values:</span></span>

* <span data-ttu-id="1d3d1-205">`<resource group>`Hallo naam van resourcegroep Hallo Hallo zone in Azure DNS is.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-205">`<resource group>` is hello name of hello resource group for hello zone in Azure DNS.</span></span>
* <span data-ttu-id="1d3d1-206">`<zone name>`Hallo-naam van Hallo zone is.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-206">`<zone name>` is hello name of hello zone.</span></span>
* <span data-ttu-id="1d3d1-207">`<zone file name>`Hallo padnaam van Hallo zone bestand toobe geëxporteerd is.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-207">`<zone file name>` is hello path/name of hello zone file toobe exported.</span></span>

<span data-ttu-id="1d3d1-208">Zoals met Hallo zone importeren, moet u eerst toosign in, kiest u uw abonnement en configureer hello Azure CLI toouse Resource Manager-modus.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-208">As with hello zone import, you first need toosign in, choose your subscription, and configure hello Azure CLI toouse Resource Manager mode.</span></span>

### <a name="tooexport-a-zone-file"></a><span data-ttu-id="1d3d1-209">tooexport een zonebestand</span><span class="sxs-lookup"><span data-stu-id="1d3d1-209">tooexport a zone file</span></span>

1. <span data-ttu-id="1d3d1-210">Meld u tooyour Azure-abonnement met behulp van hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-210">Sign in tooyour Azure subscription by using hello Azure CLI.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="1d3d1-211">Selecteer waar u toocreate uw DNS-zone Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-211">Select hello subscription where you want toocreate your DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="1d3d1-212">Azure DNS is een Azure Resource Manager alleen-lezen-service.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-212">Azure DNS is an Azure Resource Manager-only service.</span></span> <span data-ttu-id="1d3d1-213">Hello Azure CLI moet geschakelde tooResource Manager-modus.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-213">hello Azure CLI must be switched tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="1d3d1-214">tooexport Hallo bestaande Azure DNS-zone **contoso.com** in de resourcegroep **myresourcegroup** toohello bestand **contoso.com.txt** (in Hallo huidige map), voert u `azure network dns zone export`.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-214">tooexport hello existing Azure DNS zone **contoso.com** in resource group **myresourcegroup** toohello file **contoso.com.txt** (in hello current folder), run `azure network dns zone export`.</span></span> <span data-ttu-id="1d3d1-215">Deze opdracht aanroepen hello Azure DNS-service tooenumerate recordsets in Hallo zone en Hallo resultaten tooa BIND-compatibele zone-bestand exporteren.</span><span class="sxs-lookup"><span data-stu-id="1d3d1-215">This command  calls hello Azure DNS service tooenumerate record sets in hello zone and export hello results tooa BIND-compatible zone file.</span></span>

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
