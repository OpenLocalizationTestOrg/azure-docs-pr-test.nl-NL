---
title: Importeren en exporteren van een domein zonebestand naar Azure DNS met Azure CLI 1.0 | Microsoft Docs
description: Meer informatie over het importeren en exporteren van een DNS-zone-bestand naar Azure DNS met behulp van Azure CLI 1.0
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
ms.openlocfilehash: d6d3fa7aa0e8b2462b3a6b4b66d3d87ab5535314
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="import-and-export-a-dns-zone-file-using-the-azure-cli-10"></a><span data-ttu-id="0bc77-103">Importeren en exporteren van een DNS-zone-bestand met de Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0bc77-103">Import and export a DNS zone file using the Azure CLI 1.0</span></span> 

<span data-ttu-id="0bc77-104">Dit artikel begeleidt u bij het importeren en exporteren van DNS-zone-bestanden voor Azure DNS met de Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="0bc77-104">This article walks you through how to import and export DNS zone files for Azure DNS using the Azure CLI 1.0.</span></span>

## <a name="introduction-to-dns-zone-migration"></a><span data-ttu-id="0bc77-105">Inleiding tot DNS-zone-migratie</span><span class="sxs-lookup"><span data-stu-id="0bc77-105">Introduction to DNS zone migration</span></span>

<span data-ttu-id="0bc77-106">Een DNS-zonebestand is een tekstbestand met de details van elke record System DNS (Domain Name) in de zone.</span><span class="sxs-lookup"><span data-stu-id="0bc77-106">A DNS zone file is a text file that contains details of every Domain Name System (DNS) record in the zone.</span></span> <span data-ttu-id="0bc77-107">Volgt een standaardindeling, waardoor het geschikt is voor de DNS-records overbrengen tussen DNS-systemen.</span><span class="sxs-lookup"><span data-stu-id="0bc77-107">It follows a standard format, making it suitable for transferring DNS records between DNS systems.</span></span> <span data-ttu-id="0bc77-108">Met behulp van een zonebestand is een snelle, betrouwbare en handige manier om over te dragen van een DNS-zone van of naar Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="0bc77-108">Using a zone file is a quick, reliable, and convenient way to transfer a DNS zone into or out of Azure DNS.</span></span>

<span data-ttu-id="0bc77-109">Azure DNS ondersteunt importeren en exporteren van de zone-bestanden met behulp van de Azure-opdrachtregelinterface (CLI).</span><span class="sxs-lookup"><span data-stu-id="0bc77-109">Azure DNS supports importing and exporting zone files by using the Azure command-line interface (CLI).</span></span> <span data-ttu-id="0bc77-110">Zone-bestand importeren is **niet** momenteel ondersteund via Azure PowerShell of Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0bc77-110">Zone file import is **not** currently supported via Azure PowerShell or the Azure portal.</span></span>

<span data-ttu-id="0bc77-111">De Azure CLI 1.0 is een platformoverschrijdende-opdrachtregelprogramma voor het beheer van Azure-services.</span><span class="sxs-lookup"><span data-stu-id="0bc77-111">The Azure CLI 1.0 is a cross-platform command-line tool used for managing Azure services.</span></span> <span data-ttu-id="0bc77-112">Is beschikbaar voor Windows, Mac en Linux-platforms van de [pagina Azure downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="0bc77-112">It is available for the Windows, Mac, and Linux platforms from the [Azure downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="0bc77-113">Ondersteuning voor meerdere platforms is belangrijk voor importeren en exporteren van zonebestanden, aangezien de meest voorkomende naam serversoftware [BINDEN](https://www.isc.org/downloads/bind/), doorgaans op Linux wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0bc77-113">Cross-platform support is important for importing and exporting zone files, because the most common name server software, [BIND](https://www.isc.org/downloads/bind/), typically runs on Linux.</span></span>

> [!NOTE]
> <span data-ttu-id="0bc77-114">Er zijn twee versies van de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="0bc77-114">There are currently two versions of the Azure CLI.</span></span> <span data-ttu-id="0bc77-115">CLI1.0 is gebaseerd op Node.js en opdrachten die beginnen met 'azure' is.</span><span class="sxs-lookup"><span data-stu-id="0bc77-115">CLI1.0 is based on Node.js, and has commands beginning with "azure".</span></span>
> <span data-ttu-id="0bc77-116">CLI2.0 is gebaseerd op Python en opdrachten die beginnen met 'az' heeft.</span><span class="sxs-lookup"><span data-stu-id="0bc77-116">CLI2.0 is based on Python and has commands beginning with "az".</span></span> <span data-ttu-id="0bc77-117">Zone-bestand importeren in beide versies wordt ondersteund, wordt u aangeraden de opdrachten CLI1.0, zoals beschreven in deze pagina.</span><span class="sxs-lookup"><span data-stu-id="0bc77-117">While zone file import is supported in both versions, we recommend using the CLI1.0 commands, as described in this page.</span></span>

## <a name="obtain-your-existing-dns-zone-file"></a><span data-ttu-id="0bc77-118">Verkrijgen van uw bestaande DNS-zonebestand</span><span class="sxs-lookup"><span data-stu-id="0bc77-118">Obtain your existing DNS zone file</span></span>

<span data-ttu-id="0bc77-119">Voordat u een DNS-zone-bestand in Azure DNS importeren, moet u een exemplaar van de zonebestand.</span><span class="sxs-lookup"><span data-stu-id="0bc77-119">Before you import a DNS zone file into Azure DNS, you need to obtain a copy of the zone file.</span></span> <span data-ttu-id="0bc77-120">De bron van dit bestand is afhankelijk van waar de DNS-zone momenteel wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="0bc77-120">The source of this file depends on where the DNS zone is currently hosted.</span></span>

* <span data-ttu-id="0bc77-121">Als uw DNS-zone wordt gehost door een partner-service (zoals een domeinregistrar, specifieke DNS-hostingprovider of alternatieve cloudprovider), leveren of de service de mogelijkheid voor het downloaden van het DNS-zonebestand.</span><span class="sxs-lookup"><span data-stu-id="0bc77-121">If your DNS zone is hosted by a partner service (such as a domain registrar, dedicated DNS hosting provider, or alternative cloud provider), that service should provide the ability to download the DNS zone file.</span></span>
* <span data-ttu-id="0bc77-122">Als uw DNS-zone wordt gehost op Windows DNS, de standaardmap voor de zonebestanden is **%systemroot%\system32\dns**.</span><span class="sxs-lookup"><span data-stu-id="0bc77-122">If your DNS zone is hosted on Windows DNS, the default folder for the zone files is **%systemroot%\system32\dns**.</span></span> <span data-ttu-id="0bc77-123">Het volledige pad naar het bestand voor elke zone wordt ook weergegeven op de **algemene** tabblad van de DNS-console.</span><span class="sxs-lookup"><span data-stu-id="0bc77-123">The full path to each zone file also shows on the **General** tab of the DNS console.</span></span>
* <span data-ttu-id="0bc77-124">Als uw DNS-zone wordt gehost met behulp van BIND, de locatie van de zonebestand voor elke zone die is opgegeven in het configuratiebestand BIND **named.conf**.</span><span class="sxs-lookup"><span data-stu-id="0bc77-124">If your DNS zone is hosted by using BIND, the location of the zone file for each zone is specified in the BIND configuration file **named.conf**.</span></span>

> [!NOTE]
> <span data-ttu-id="0bc77-125">Zone-bestanden die zijn gedownload van GoDaddy hebben een iets andere indeling.</span><span class="sxs-lookup"><span data-stu-id="0bc77-125">Zone files downloaded from GoDaddy have a slightly nonstandard format.</span></span> <span data-ttu-id="0bc77-126">U moet deze corrigeren voordat u deze zonebestanden in Azure DNS importeren.</span><span class="sxs-lookup"><span data-stu-id="0bc77-126">You need to correct this before you import these zone files into Azure DNS.</span></span>
>
> <span data-ttu-id="0bc77-127">DNS-namen in het RDATA van elke DNS-record zijn opgegeven als FQDN-namen, maar ze niet beschikken over een afsluitende '. ' Dit betekent dat ze worden geïnterpreteerd door andere DNS-systemen als relatieve namen.</span><span class="sxs-lookup"><span data-stu-id="0bc77-127">DNS names in the RDATA of each DNS record are specified as fully qualified names, but they don't have a terminating "." This means they are interpreted by other DNS systems as relative names.</span></span> <span data-ttu-id="0bc77-128">U moet het zonebestand om toe te voegen de afsluitende bewerken '. ' voor hun namen voordat u ze in Azure DNS importeren.</span><span class="sxs-lookup"><span data-stu-id="0bc77-128">You need to edit the zone file to append the terminating "." to their names before you import them into Azure DNS.</span></span>
>
> <span data-ttu-id="0bc77-129">Bijvoorbeeld, moet de CNAME-record 'www 3600 IN CNAME contoso.com' worden gewijzigd in 'www 3600 IN CNAME contoso.com.'</span><span class="sxs-lookup"><span data-stu-id="0bc77-129">For example, the CNAME record "www 3600 IN CNAME contoso.com" should be changed to "www 3600 IN CNAME contoso.com."</span></span>
> <span data-ttu-id="0bc77-130">(met een afsluitende '. ').</span><span class="sxs-lookup"><span data-stu-id="0bc77-130">(with a terminating ".").</span></span>

## <a name="import-a-dns-zone-file-into-azure-dns"></a><span data-ttu-id="0bc77-131">Een DNS-zone-bestand importeren in Azure DNS</span><span class="sxs-lookup"><span data-stu-id="0bc77-131">Import a DNS zone file into Azure DNS</span></span>

<span data-ttu-id="0bc77-132">Maakt een nieuwe zone een zonebestand te importeren in Azure DNS, als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="0bc77-132">Importing a zone file creates a new zone in Azure DNS if one does not already exist.</span></span> <span data-ttu-id="0bc77-133">Als de zone al bestaat, moeten de recordsets in de zonebestand met de bestaande recordsets worden samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="0bc77-133">If the zone already exists, the record sets in the zone file must be merged with the existing record sets.</span></span>

### <a name="merge-behavior"></a><span data-ttu-id="0bc77-134">Samenvoegen van gedrag</span><span class="sxs-lookup"><span data-stu-id="0bc77-134">Merge behavior</span></span>

* <span data-ttu-id="0bc77-135">Standaard worden bestaande en nieuwe recordsets samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="0bc77-135">By default, existing and new record sets are merged.</span></span> <span data-ttu-id="0bc77-136">Identieke records binnen een samengevoegde Recordset zijn ongedaan gedupliceerde.</span><span class="sxs-lookup"><span data-stu-id="0bc77-136">Identical records within a merged record set are de-duplicated.</span></span>
* <span data-ttu-id="0bc77-137">U kunt ook door te geven de `--force` optie, de import-proces vervangt bestaande recordsets met nieuwe recordsets.</span><span class="sxs-lookup"><span data-stu-id="0bc77-137">Alternatively, by specifying the `--force` option, the import process replaces existing record sets with new record sets.</span></span> <span data-ttu-id="0bc77-138">Bestaande recordsets waarvoor geen overeenkomende recordset in de geïmporteerde zonebestand worden niet verwijderd.</span><span class="sxs-lookup"><span data-stu-id="0bc77-138">Existing record sets that do not have a corresponding record set in the imported zone file are not be removed.</span></span>
* <span data-ttu-id="0bc77-139">Als recordsets worden samengevoegd, wordt de tijd van de bestaande recordsets live (TTL) gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0bc77-139">When record sets are merged, the time to live (TTL) of preexisting record sets is used.</span></span> <span data-ttu-id="0bc77-140">Wanneer `--force` wordt gebruikt, wordt de TTL-waarde van de nieuwe recordset gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0bc77-140">When `--force` is used, the TTL of the new record set is used.</span></span>
* <span data-ttu-id="0bc77-141">Parameters Authority (SOA) is gestart (behalve `host`) altijd worden overgenomen uit het zonebestand geïmporteerde, ongeacht of `--force` wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0bc77-141">Start of Authority (SOA) parameters (except `host`) are always taken from the imported zone file, regardless of whether `--force` is used.</span></span> <span data-ttu-id="0bc77-142">Op deze manier voor de naamserverrecord ingesteld in het toppunt van de zone, is de TTL-waarde altijd overgenomen uit het geïmporteerde zonebestand.</span><span class="sxs-lookup"><span data-stu-id="0bc77-142">Similarly, for the name server record set at the zone apex, the TTL is always taken from the imported zone file.</span></span>
* <span data-ttu-id="0bc77-143">Een geïmporteerde CNAME-record is geen vervanging voor een bestaande CNAME-record met dezelfde naam als de `--force` parameter wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="0bc77-143">An imported CNAME record does not replace an existing CNAME record with the same name unless the `--force` parameter is specified.</span></span>
* <span data-ttu-id="0bc77-144">Als er ontstaat een conflict tussen een CNAME-record en een andere record met dezelfde naam maar met een ander type (ongeacht die is bestaande of nieuwe), wordt de bestaande blijven behouden.</span><span class="sxs-lookup"><span data-stu-id="0bc77-144">When a conflict arises between a CNAME record and another record of the same name but different type (regardless of which is existing or new), the existing record is retained.</span></span> <span data-ttu-id="0bc77-145">Dit is onafhankelijk van het gebruik van `--force`.</span><span class="sxs-lookup"><span data-stu-id="0bc77-145">This is independent of the use of `--force`.</span></span>

### <a name="additional-information-about-importing"></a><span data-ttu-id="0bc77-146">Als u meer informatie over het importeren</span><span class="sxs-lookup"><span data-stu-id="0bc77-146">Additional information about importing</span></span>

<span data-ttu-id="0bc77-147">De volgende opmerkingen bieden aanvullende technische gegevens over de zone importeren.</span><span class="sxs-lookup"><span data-stu-id="0bc77-147">The following notes provide additional technical details about the zone import process.</span></span>

* <span data-ttu-id="0bc77-148">De `$TTL` richtlijn is optioneel en wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="0bc77-148">The `$TTL` directive is optional, and it is supported.</span></span> <span data-ttu-id="0bc77-149">Als er geen `$TTL` richtlijn krijgt, records zonder een expliciete TTL geïmporteerde is ingesteld op een standaard-TTL van 3600 seconden zijn.</span><span class="sxs-lookup"><span data-stu-id="0bc77-149">When no `$TTL` directive is given, records without an explicit TTL are imported set to a default TTL of 3600 seconds.</span></span> <span data-ttu-id="0bc77-150">Wanneer twee records in de dezelfde recordset verschillende TTLs opgeeft, wordt de lagere waarde gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0bc77-150">When two records in the same record set specify different TTLs, the lower value is used.</span></span>
* <span data-ttu-id="0bc77-151">De `$ORIGIN` richtlijn is optioneel en wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="0bc77-151">The `$ORIGIN` directive is optional, and it is supported.</span></span> <span data-ttu-id="0bc77-152">Als er geen `$ORIGIN` is ingesteld, de standaardwaarde gebruikt, is de naam van de zone die is opgegeven op de opdrachtregel (plus de afsluitende '. ').</span><span class="sxs-lookup"><span data-stu-id="0bc77-152">When no `$ORIGIN` is set, the default value used is the zone name as specified on the command line (plus the terminating ".").</span></span>
* <span data-ttu-id="0bc77-153">De `$INCLUDE` en `$GENERATE` richtlijnen worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="0bc77-153">The `$INCLUDE` and `$GENERATE` directives are not supported.</span></span>
* <span data-ttu-id="0bc77-154">Deze typen worden ondersteund: A, AAAA, CNAME, MX, NS, SOA, SRV en TXT.</span><span class="sxs-lookup"><span data-stu-id="0bc77-154">These record types are supported: A, AAAA, CNAME, MX, NS, SOA, SRV, and TXT.</span></span>
* <span data-ttu-id="0bc77-155">De SOA-record wordt automatisch gemaakt door Azure DNS wanneer u een zone wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0bc77-155">The SOA record is created automatically by Azure DNS when a zone is created.</span></span> <span data-ttu-id="0bc77-156">Wanneer u een zonebestand importeert, alle SOA-parameters zijn overgenomen uit het zonebestand *behalve* de `host` parameter.</span><span class="sxs-lookup"><span data-stu-id="0bc77-156">When you import a zone file, all SOA parameters are taken from the zone file *except* the `host` parameter.</span></span> <span data-ttu-id="0bc77-157">De waarde die is verstrekt door Azure DNS maakt gebruik van deze parameter.</span><span class="sxs-lookup"><span data-stu-id="0bc77-157">This parameter uses the value provided by Azure DNS.</span></span> <span data-ttu-id="0bc77-158">Dit is omdat deze parameter naar de server de primaire naam van de Azure DNS verwijzen moet.</span><span class="sxs-lookup"><span data-stu-id="0bc77-158">This is because this parameter must refer to the primary name server provided by Azure DNS.</span></span>
* <span data-ttu-id="0bc77-159">De naamserverrecord ingesteld in het toppunt van de zone wordt ook automatisch gemaakt door Azure DNS wanneer de zone wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0bc77-159">The name server record set at the zone apex is also created automatically by Azure DNS when the zone is created.</span></span> <span data-ttu-id="0bc77-160">Alleen de TTL van deze recordset is geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="0bc77-160">Only the TTL of this record set is imported.</span></span> <span data-ttu-id="0bc77-161">Deze records bevatten de servernamen verstrekt door Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="0bc77-161">These records contain the name server names provided by Azure DNS.</span></span> <span data-ttu-id="0bc77-162">De gegevens van de record is niet overschreven door de waarden in de geïmporteerde zone-bestand.</span><span class="sxs-lookup"><span data-stu-id="0bc77-162">The record data is not overwritten by the values contained in the imported zone file.</span></span>
* <span data-ttu-id="0bc77-163">Azure DNS biedt ondersteuning voor slechts één tekenreeks TXT-records tijdens de openbare Preview.</span><span class="sxs-lookup"><span data-stu-id="0bc77-163">During Public Preview, Azure DNS supports only single-string TXT records.</span></span> <span data-ttu-id="0bc77-164">Multistring TXT-records zijn worden samengevoegd en afgekapt tot 255 tekens.</span><span class="sxs-lookup"><span data-stu-id="0bc77-164">Multistring TXT records are be concatenated and truncated to 255 characters.</span></span>

### <a name="cli-format-and-values"></a><span data-ttu-id="0bc77-165">CLI-indeling en waarden</span><span class="sxs-lookup"><span data-stu-id="0bc77-165">CLI format and values</span></span>

<span data-ttu-id="0bc77-166">De indeling van de Azure CLI-opdracht voor het importeren van een DNS-zone is:</span><span class="sxs-lookup"><span data-stu-id="0bc77-166">The format of the Azure CLI command to import a DNS zone is:</span></span>

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="0bc77-167">Waarden:</span><span class="sxs-lookup"><span data-stu-id="0bc77-167">Values:</span></span>

* <span data-ttu-id="0bc77-168">`<resource group>`is de naam van de resourcegroep voor de zone in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="0bc77-168">`<resource group>` is the name of the resource group for the zone in Azure DNS.</span></span>
* <span data-ttu-id="0bc77-169">`<zone name>`is de naam van de zone.</span><span class="sxs-lookup"><span data-stu-id="0bc77-169">`<zone name>` is the name of the zone.</span></span>
* <span data-ttu-id="0bc77-170">`<zone file name>`is de padnaam van het zonebestand moet worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="0bc77-170">`<zone file name>` is the path/name of the zone file to be imported.</span></span>

<span data-ttu-id="0bc77-171">Als een zone met deze naam niet in de resourcegroep bestaat, wordt deze voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0bc77-171">If a zone with this name does not exist in the resource group, it is created for you.</span></span> <span data-ttu-id="0bc77-172">Als de zone al bestaat, wordt de geïmporteerde recordsets worden samengevoegd met bestaande recordsets.</span><span class="sxs-lookup"><span data-stu-id="0bc77-172">If the zone already exists, the imported record sets are merged with existing record sets.</span></span> <span data-ttu-id="0bc77-173">Voor het overschrijven van de bestaande recordsets, gebruiken de `--force` optie.</span><span class="sxs-lookup"><span data-stu-id="0bc77-173">To overwrite the existing record sets, use the `--force` option.</span></span>

<span data-ttu-id="0bc77-174">Om te controleren of de indeling van een zonebestand zonder het geïmporteerd, gebruiken de `--parse-only` optie.</span><span class="sxs-lookup"><span data-stu-id="0bc77-174">To verify the format of a zone file without actually importing it, use the `--parse-only` option.</span></span>

### <a name="step-1-import-a-zone-file"></a><span data-ttu-id="0bc77-175">Step 1.</span><span class="sxs-lookup"><span data-stu-id="0bc77-175">Step 1.</span></span> <span data-ttu-id="0bc77-176">Een zonebestand importeren</span><span class="sxs-lookup"><span data-stu-id="0bc77-176">Import a zone file</span></span>

<span data-ttu-id="0bc77-177">Voor het importeren van een zonebestand voor de zone **contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="0bc77-177">To import a zone file for the zone **contoso.com**.</span></span>

1. <span data-ttu-id="0bc77-178">Aanmelden bij uw Azure-abonnement met behulp van de Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="0bc77-178">Sign in to your Azure subscription by using the Azure CLI 1.0.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="0bc77-179">Selecteer het abonnement waar u uw nieuwe DNS-zone maken.</span><span class="sxs-lookup"><span data-stu-id="0bc77-179">Select the subscription where you want to create your new DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="0bc77-180">Azure DNS is een Azure Resource Manager alleen-lezen-service zodat de Azure CLI moet worden overgeschakeld naar de modus Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0bc77-180">Azure DNS is an Azure Resource Manager-only service, so the Azure CLI must be switched to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="0bc77-181">Voordat u de Azure DNS-service gebruiken, moet u uw abonnement voor het gebruik van de Microsoft.Network-resourceprovider registreren.</span><span class="sxs-lookup"><span data-stu-id="0bc77-181">Before you use the Azure DNS service, you must register your subscription to use the Microsoft.Network resource provider.</span></span> <span data-ttu-id="0bc77-182">(Dit is een eenmalige bewerking voor elk abonnement.)</span><span class="sxs-lookup"><span data-stu-id="0bc77-182">(This is a one-time operation for each subscription.)</span></span>

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. <span data-ttu-id="0bc77-183">Als u nog geen een hebt, moet u ook een Resource Manager-resourcegroep maken.</span><span class="sxs-lookup"><span data-stu-id="0bc77-183">If you don't have one already, you also need to create a Resource Manager resource group.</span></span>

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. <span data-ttu-id="0bc77-184">Voor het importeren van de zone **contoso.com** uit het bestand **contoso.com.txt** in een nieuwe DNS-zone in de resourcegroep **myresourcegroup**, voert u de opdracht `azure network dns zone import`.</span><span class="sxs-lookup"><span data-stu-id="0bc77-184">To import the zone **contoso.com** from the file **contoso.com.txt** into a new DNS zone in the resource group **myresourcegroup**, run the command `azure network dns zone import`.</span></span><BR><span data-ttu-id="0bc77-185">Deze opdracht wordt geladen van bestand voor de zone en het parseren.</span><span class="sxs-lookup"><span data-stu-id="0bc77-185">This command loads the zone file and parse it.</span></span> <span data-ttu-id="0bc77-186">De opdracht wordt een reeks opdrachten uitgevoerd op de Azure DNS-service voor het maken van de zone en alle recordsets in de zone.</span><span class="sxs-lookup"><span data-stu-id="0bc77-186">The command executes a series of commands on the Azure DNS service to create the zone and all the record sets in the zone.</span></span> <span data-ttu-id="0bc77-187">De opdracht wordt uitgevoerd in het consolevenster, samen met eventuele fouten of waarschuwingen gemeld.</span><span class="sxs-lookup"><span data-stu-id="0bc77-187">The command reports progress in the console window, along with any errors or warnings.</span></span> <span data-ttu-id="0bc77-188">Omdat recordsets zijn gemaakt in de reeks, duurt een paar minuten een grote zone-bestand importeren.</span><span class="sxs-lookup"><span data-stu-id="0bc77-188">Because record sets are created in series, it may take a few minutes to import a large zone file.</span></span>

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-the-zone"></a><span data-ttu-id="0bc77-189">Stap 2.</span><span class="sxs-lookup"><span data-stu-id="0bc77-189">Step 2.</span></span> <span data-ttu-id="0bc77-190">Controleer of de zone</span><span class="sxs-lookup"><span data-stu-id="0bc77-190">Verify the zone</span></span>

<span data-ttu-id="0bc77-191">Om te controleren of de DNS-zone nadat u het bestand importeert, kunt u een van de volgende methoden gebruiken:</span><span class="sxs-lookup"><span data-stu-id="0bc77-191">To verify the DNS zone after you import the file, you can use any one of the following methods:</span></span>

* <span data-ttu-id="0bc77-192">U kunt de records weergeven met behulp van de volgende Azure CLI-opdracht:</span><span class="sxs-lookup"><span data-stu-id="0bc77-192">You can list the records by using the following Azure CLI command:</span></span>

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* <span data-ttu-id="0bc77-193">U kunt de records weergeven met behulp van de PowerShell-cmdlet `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="0bc77-193">You can list the records by using the PowerShell cmdlet `Get-AzureRmDnsRecordSet`.</span></span>
* <span data-ttu-id="0bc77-194">U kunt `nslookup` om te controleren of de naamomzetting voor de records.</span><span class="sxs-lookup"><span data-stu-id="0bc77-194">You can use `nslookup` to verify name resolution for the records.</span></span> <span data-ttu-id="0bc77-195">Omdat de zone nog niet is toegewezen, moet u de juiste Azure DNS-naamservers expliciet opgeven.</span><span class="sxs-lookup"><span data-stu-id="0bc77-195">Because the zone isn't delegated yet, you need to specify the correct Azure DNS name servers explicitly.</span></span> <span data-ttu-id="0bc77-196">Het volgende voorbeeld laat zien hoe de servernamen toegewezen aan de zone worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="0bc77-196">The following sample shows how to retrieve the name server names assigned to the zone.</span></span> <span data-ttu-id="0bc77-197">IT ook wordt uitgelegd hoe u de www-record met behulp van een query `nslookup`.</span><span class="sxs-lookup"><span data-stu-id="0bc77-197">IT also shows how to query the "www" record by using `nslookup`.</span></span>

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up the DNS Record Set "@" of type "NS"
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

### <a name="step-3-update-dns-delegation"></a><span data-ttu-id="0bc77-198">Stap 3.</span><span class="sxs-lookup"><span data-stu-id="0bc77-198">Step 3.</span></span> <span data-ttu-id="0bc77-199">DNS-delegering bijwerken</span><span class="sxs-lookup"><span data-stu-id="0bc77-199">Update DNS delegation</span></span>

<span data-ttu-id="0bc77-200">Nadat u hebt gecontroleerd of de zone correct zijn geïmporteerd, moet u de DNS-delegering om te verwijzen naar de Azure DNS-naamservers bijwerken.</span><span class="sxs-lookup"><span data-stu-id="0bc77-200">After you have verified that the zone has been imported correctly, you need to update the DNS delegation to point to the Azure DNS name servers.</span></span> <span data-ttu-id="0bc77-201">Zie voor meer informatie het artikel [de DNS-delegering bijwerken](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="0bc77-201">For more information, see the article [Update the DNS delegation](dns-domain-delegation.md).</span></span>

## <a name="export-a-dns-zone-file-from-azure-dns"></a><span data-ttu-id="0bc77-202">Een DNS-zone-bestand exporteren uit Azure DNS</span><span class="sxs-lookup"><span data-stu-id="0bc77-202">Export a DNS zone file from Azure DNS</span></span>

<span data-ttu-id="0bc77-203">De indeling van de Azure CLI-opdracht voor het importeren van een DNS-zone is:</span><span class="sxs-lookup"><span data-stu-id="0bc77-203">The format of the Azure CLI command to import a DNS zone is:</span></span>

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="0bc77-204">Waarden:</span><span class="sxs-lookup"><span data-stu-id="0bc77-204">Values:</span></span>

* <span data-ttu-id="0bc77-205">`<resource group>`is de naam van de resourcegroep voor de zone in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="0bc77-205">`<resource group>` is the name of the resource group for the zone in Azure DNS.</span></span>
* <span data-ttu-id="0bc77-206">`<zone name>`is de naam van de zone.</span><span class="sxs-lookup"><span data-stu-id="0bc77-206">`<zone name>` is the name of the zone.</span></span>
* <span data-ttu-id="0bc77-207">`<zone file name>`is de padnaam van het zonebestand moet worden geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="0bc77-207">`<zone file name>` is the path/name of the zone file to be exported.</span></span>

<span data-ttu-id="0bc77-208">Als met de import zone moet u eerst aanmelden, kiest u uw abonnement en configureren van de Azure CLI voor het gebruik van Resource Manager-modus.</span><span class="sxs-lookup"><span data-stu-id="0bc77-208">As with the zone import, you first need to sign in, choose your subscription, and configure the Azure CLI to use Resource Manager mode.</span></span>

### <a name="to-export-a-zone-file"></a><span data-ttu-id="0bc77-209">Een zonebestand exporteren</span><span class="sxs-lookup"><span data-stu-id="0bc77-209">To export a zone file</span></span>

1. <span data-ttu-id="0bc77-210">Aanmelden bij uw Azure-abonnement met behulp van de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="0bc77-210">Sign in to your Azure subscription by using the Azure CLI.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="0bc77-211">Selecteer het abonnement waarbij u wilt maken van uw DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="0bc77-211">Select the subscription where you want to create your DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="0bc77-212">Azure DNS is een Azure Resource Manager alleen-lezen-service.</span><span class="sxs-lookup"><span data-stu-id="0bc77-212">Azure DNS is an Azure Resource Manager-only service.</span></span> <span data-ttu-id="0bc77-213">De Azure CLI moet worden overgeschakeld naar de modus Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0bc77-213">The Azure CLI must be switched to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="0bc77-214">Exporteren van de bestaande Azure DNS-zone **contoso.com** in de resourcegroep **myresourcegroup** naar het bestand **contoso.com.txt** (in de huidige map), voert u `azure network dns zone export`.</span><span class="sxs-lookup"><span data-stu-id="0bc77-214">To export the existing Azure DNS zone **contoso.com** in resource group **myresourcegroup** to the file **contoso.com.txt** (in the current folder), run `azure network dns zone export`.</span></span> <span data-ttu-id="0bc77-215">Met deze opdracht roept de service Azure DNS-recordsets in de zone inventariseren en de resultaten exporteren naar een zone BIND-compatibel bestand.</span><span class="sxs-lookup"><span data-stu-id="0bc77-215">This command  calls the Azure DNS service to enumerate record sets in the zone and export the results to a BIND-compatible zone file.</span></span>

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
