---
title: Opmerkingen bij de aaaRelease van Data Management Gateway | Microsoft Docs
description: Releaseopmerkingen voor Data Management Gateway-loop
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 14762e82-76d9-41c4-ba9f-14a54da29c36
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 3165d7537410a0531e0bb7f7fe584767f9155574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-data-management-gateway"></a><span data-ttu-id="d5ed1-103">Releaseopmerkingen voor Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="d5ed1-103">Release notes for Data Management Gateway</span></span>
<span data-ttu-id="d5ed1-104">Een van de uitdagingen Hallo voor moderne gegevensintegratie is toomove gegevens tooand van lokale toocloud.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-104">One of hello challenges for modern data integration is toomove data tooand from on-premises toocloud.</span></span> <span data-ttu-id="d5ed1-105">Data Factory maakt deze integratie met Data Management Gateway, een agent wordt dat u lokale tooenable hybride gegevensverplaatsing kunt installeren.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-105">Data Factory makes this integration with Data Management Gateway, which is an agent that you can install on-premises tooenable hybrid data movement.</span></span>

<span data-ttu-id="d5ed1-106">Zie de volgende artikelen voor meer informatie over Data Management Gateway Hallo en hoe toouse het:</span><span class="sxs-lookup"><span data-stu-id="d5ed1-106">See hello following articles for detailed information about Data Management Gateway and how toouse it:</span></span>

*  [<span data-ttu-id="d5ed1-107">Gegevensbeheergateway</span><span class="sxs-lookup"><span data-stu-id="d5ed1-107">Data Management Gateway</span></span>](data-factory-data-management-gateway.md)
*  [<span data-ttu-id="d5ed1-108">Gegevens verplaatsen tussen on-premises en in de cloud met Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d5ed1-108">Move data between on-premises and cloud using Azure Data Factory</span></span>](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version-21063477"></a><span data-ttu-id="d5ed1-109">HUIDIGE VERSIE (2.10.6347.7)</span><span class="sxs-lookup"><span data-stu-id="d5ed1-109">CURRENT VERSION (2.10.6347.7)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="d5ed1-110">Verbeteringen-</span><span class="sxs-lookup"><span data-stu-id="d5ed1-110">Enhancements-</span></span>
- <span data-ttu-id="d5ed1-111">U kunt toevoegen DNS-vermeldingen toowhitelist servicebus in plaats van door alle Azure-IP-adressen van uw firewall (indien nodig).</span><span class="sxs-lookup"><span data-stu-id="d5ed1-111">You can add DNS entries toowhitelist service bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="d5ed1-112">U kunt de respectieve DNS-vermelding vinden op Azure-portal (Data Factory -> 'Maken en implementeren' -> 'Gateways'-'serviceUrls' (in JSON) ></span><span class="sxs-lookup"><span data-stu-id="d5ed1-112">You can find respective DNS entry on Azure portal (Data Factory -> ‘Author and Deploy’ -> ‘Gateways’ -> "serviceUrls" (in JSON)</span></span>
- <span data-ttu-id="d5ed1-113">HDFS-connector ondersteunt nu zelfondertekend certificaat met openbare doordat u SSL-validatie overslaat.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-113">HDFS connector now supports self-signed public certificate by letting you skip SSL validation.</span></span>
- <span data-ttu-id="d5ed1-114">Vaste: Probleem met de gateway tijdens het bijwerken (vervaldatum tooclock tijdverschil)</span><span class="sxs-lookup"><span data-stu-id="d5ed1-114">Fixed: Issue with gateway offline during update (due tooclock skew)</span></span>



## <a name="earlier-versions"></a><span data-ttu-id="d5ed1-115">Eerdere versies</span><span class="sxs-lookup"><span data-stu-id="d5ed1-115">Earlier versions</span></span>

## <a name="2963132"></a><span data-ttu-id="d5ed1-116">2.9.6313.2</span><span class="sxs-lookup"><span data-stu-id="d5ed1-116">2.9.6313.2</span></span>
### <a name="enhancements-"></a><span data-ttu-id="d5ed1-117">Verbeteringen-</span><span class="sxs-lookup"><span data-stu-id="d5ed1-117">Enhancements-</span></span>
-   <span data-ttu-id="d5ed1-118">U kunt toevoegen DNS-vermeldingen toowhitelist Service Bus in plaats van door alle Azure-IP-adressen van uw firewall (indien nodig).</span><span class="sxs-lookup"><span data-stu-id="d5ed1-118">You can add DNS entries toowhitelist Service Bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="d5ed1-119">Hier voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-119">More details here.</span></span>
-   <span data-ttu-id="d5ed1-120">U kunt nu gegevens uit een enkele blok-blob van too4.75 TB, namelijk Hallo maximaal ondersteunde grootte van blok-blob kopiëren.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-120">You can now copy data to/from a single block blob up too4.75 TB, which is hello max supported size of block blob.</span></span> <span data-ttu-id="d5ed1-121">(eerdere limiet was 195 GB).</span><span class="sxs-lookup"><span data-stu-id="d5ed1-121">(earlier limit was 195 GB).</span></span>
-   <span data-ttu-id="d5ed1-122">Vaste: Onvoldoende geheugen-probleem tijdens ritsen enkele kleine bestanden tijdens de kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-122">Fixed: Out of memory issue while unzipping several small files during copy activity.</span></span>
-   <span data-ttu-id="d5ed1-123">Vaste: Index valt buiten het bereik probleem tijdens het kopiëren van het Document DB tooan on-premises SQL Server met de functie idempotency.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-123">Fixed: Index out of range issue while copying from Document DB tooan on-premises SQL Server with idempotency feature.</span></span>
-   <span data-ttu-id="d5ed1-124">Vaste: SQL-script voor opschoning werkt niet met lokale SQL Server van de Wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-124">Fixed: SQL cleanup script doesn't work with on-premises SQL Server from Copy Wizard.</span></span>
-   <span data-ttu-id="d5ed1-125">Vaste: Kolomnaam met ruimte aan Hallo einde werkt niet in de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-125">Fixed: Column name with space at hello end does not work in copy activity.</span></span>

## <a name="28662833"></a><span data-ttu-id="d5ed1-126">2.8.66283.3</span><span class="sxs-lookup"><span data-stu-id="d5ed1-126">2.8.66283.3</span></span>
### <a name="enhancements-"></a><span data-ttu-id="d5ed1-127">Verbeteringen-</span><span class="sxs-lookup"><span data-stu-id="d5ed1-127">Enhancements-</span></span>
- <span data-ttu-id="d5ed1-128">Vaste: Probleem met de referenties op de computer opnieuw is opgestart gateway ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-128">Fixed: Issue with missing credentials on gateway machine reboot.</span></span>
- <span data-ttu-id="d5ed1-129">Vaste: Probleem met de registratie tijdens gateway herstellen met behulp van een back-upbestand.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-129">Fixed: Issue with registration during gateway restore using a backup file.</span></span>


## <a name="2762401"></a><span data-ttu-id="d5ed1-130">2.7.6240.1</span><span class="sxs-lookup"><span data-stu-id="d5ed1-130">2.7.6240.1</span></span>
### <a name="enhancements-"></a><span data-ttu-id="d5ed1-131">Verbeteringen-</span><span class="sxs-lookup"><span data-stu-id="d5ed1-131">Enhancements-</span></span>
- <span data-ttu-id="d5ed1-132">Vaste: Onjuiste leesbewerking van de decimale null-waarde van Oracle als bron.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-132">Fixed: Incorrect read of Decimal null value from Oracle as source.</span></span>

## <a name="2661922"></a><span data-ttu-id="d5ed1-133">2.6.6192.2</span><span class="sxs-lookup"><span data-stu-id="d5ed1-133">2.6.6192.2</span></span>
### <a name="whats-new"></a><span data-ttu-id="d5ed1-134">Nieuwe functies</span><span class="sxs-lookup"><span data-stu-id="d5ed1-134">What’s new</span></span>
- <span data-ttu-id="d5ed1-135">Klanten kunnen feedback op gateway registreren ervaring.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-135">Customers can provide feedback on gateway registering experience.</span></span>
- <span data-ttu-id="d5ed1-136">Ondersteuning voor een nieuwe compressie-indeling: ZIP (Deflate)</span><span class="sxs-lookup"><span data-stu-id="d5ed1-136">Support a new compression format: ZIP (Deflate)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="d5ed1-137">Verbeteringen-</span><span class="sxs-lookup"><span data-stu-id="d5ed1-137">Enhancements-</span></span>
- <span data-ttu-id="d5ed1-138">Prestatieverbeteringen voor Oracle opvangen, HDFS-bron.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-138">Performance improvement for Oracle Sink, HDFS source.</span></span>
- <span data-ttu-id="d5ed1-139">Fout-oplossing voor gateway automatisch bijwerken, gateway parallelle verwerking van capaciteit.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-139">Bug fix for gateway auto update, gateway parallel processing capacity.</span></span>


## <a name="2561641"></a><span data-ttu-id="d5ed1-140">2.5.6164.1</span><span class="sxs-lookup"><span data-stu-id="d5ed1-140">2.5.6164.1</span></span>
### <a name="enhancements"></a><span data-ttu-id="d5ed1-141">Verbeteringen</span><span class="sxs-lookup"><span data-stu-id="d5ed1-141">Enhancements</span></span>
- <span data-ttu-id="d5ed1-142">Betere en krachtigere Gateway registratie ervaring-nu kunt u de voortgangsstatus tijdens Hallo Gateway registratieproces, waardoor Hallo registratie ervaren responsievere bijhouden.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-142">Improved and more robust Gateway registration experience- Now you can track progress status during hello Gateway registration process, which makes hello registration experience more responsive.</span></span>
- <span data-ttu-id="d5ed1-143">Verbetering van de Gateway herstellen proces - u kunt nog steeds gateway herstellen, zelfs als er geen back-upbestand van Hallo gateway met deze update.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-143">Improvement in Gateway Restore Process- You can still recover gateway even if you do not have hello gateway backup file with this update.</span></span> <span data-ttu-id="d5ed1-144">Dit moet u tooreset gekoppelde Service referenties in Portal.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-144">This would require you tooreset Linked Service credentials in Portal.</span></span>
- <span data-ttu-id="d5ed1-145">Fout te herstellen.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-145">Bug fix.</span></span>

## <a name="2461511"></a><span data-ttu-id="d5ed1-146">2.4.6151.1</span><span class="sxs-lookup"><span data-stu-id="d5ed1-146">2.4.6151.1</span></span>

### <a name="whats-new"></a><span data-ttu-id="d5ed1-147">Nieuwe functies</span><span class="sxs-lookup"><span data-stu-id="d5ed1-147">What’s new</span></span>

- <span data-ttu-id="d5ed1-148">U kunt nu de referenties voor gegevensbron lokaal opslaan.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-148">You can now store data source credentials locally.</span></span> <span data-ttu-id="d5ed1-149">Hallo-referenties zijn versleuteld.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-149">hello credentials are encrypted.</span></span> <span data-ttu-id="d5ed1-150">referenties voor gegevensbron Hallo kunnen worden hersteld en teruggezet met behulp van back-upbestand Hallo die kan worden geëxporteerd uit een bestaande Gateway, alle lokale Hallo.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-150">hello data source credentials can be recovered and restored using hello backup file that can be exported from hello existing Gateway, all on-premises.</span></span>

### <a name="enhancements-"></a><span data-ttu-id="d5ed1-151">Verbeteringen-</span><span class="sxs-lookup"><span data-stu-id="d5ed1-151">Enhancements-</span></span>

- <span data-ttu-id="d5ed1-152">Betere en krachtigere Gateway registratie ervaring.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-152">Improved and more robust Gateway registration experience.</span></span>
- <span data-ttu-id="d5ed1-153">Ondersteuning voor automatische detectie van QuoteChar configuratie voor tekst zonder opmaak in de wizard kopiëren en Hallo verbeteren de algemene indeling nauwkeurigheid van de detectie.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-153">Support auto detection of QuoteChar configuration for Text format in copy wizard, and improve hello overall format detection accuracy.</span></span>

## <a name="2361002"></a><span data-ttu-id="d5ed1-154">2.3.6100.2</span><span class="sxs-lookup"><span data-stu-id="d5ed1-154">2.3.6100.2</span></span>

- <span data-ttu-id="d5ed1-155">Ondersteuning voor firstRowAsHeader en SkipLineCount automatische detectie in de wizard kopiëren voor tekstbestanden in on-premises bestandssysteem en HDFS.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-155">Support firstRowAsHeader and SkipLineCount auto detection in copy wizard for text files in on-premises File system and HDFS.</span></span>
- <span data-ttu-id="d5ed1-156">Hallo stabiliteit van de netwerkverbinding tussen de gateway en Service Bus verbeteren</span><span class="sxs-lookup"><span data-stu-id="d5ed1-156">Enhance hello stability of network connection between gateway and Service Bus</span></span>
- <span data-ttu-id="d5ed1-157">Een aantal problemen opgelost</span><span class="sxs-lookup"><span data-stu-id="d5ed1-157">A few bug fixes</span></span>


## <a name="2260721"></a><span data-ttu-id="d5ed1-158">2.2.6072.1</span><span class="sxs-lookup"><span data-stu-id="d5ed1-158">2.2.6072.1</span></span>

*  <span data-ttu-id="d5ed1-159">Ondersteunt het instellen van HTTP-proxy voor het gebruik van de gateway Hallo Hallo Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-159">Supports setting HTTP proxy for hello gateway using hello Gateway Configuration Manager.</span></span> <span data-ttu-id="d5ed1-160">Als geconfigureerd, zijn Azure Blob, Azure Table Azure Data Lake en Document DB toegankelijk via HTTP-proxy.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-160">If configured, Azure Blob, Azure Table, Azure Data Lake, and Document DB are accessed through HTTP proxy.</span></span>
*  <span data-ttu-id="d5ed1-161">Ondersteunt header verwerking voor TextFormat bij het kopiëren van gegevens uit / tooAzure Blob, Azure Data Lake Store on-premises bestandssysteem en lokale HDFS.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-161">Supports header handling for TextFormat when copying data from/tooAzure Blob, Azure Data Lake Store, on-premises File System, and on-premises HDFS.</span></span>
*  <span data-ttu-id="d5ed1-162">Ondersteunt het kopiëren van gegevens van toevoeg-blobs en pagina-Blob samen met de Hallo al ondersteund blok-Blob.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-162">Supports copying data from Append Blob and Page Blob along with hello already supported Block Blob.</span></span>
*  <span data-ttu-id="d5ed1-163">Introduceert een nieuwe gatewaystatus **Online (beperkt)**, wat aangeeft dat de belangrijkste functionaliteit van die Hallo van Hallo gateway werkt, behalve Hallo interactieve bewerking ondersteuning voor de Wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-163">Introduces a new gateway status **Online (Limited)**, which indicates that hello main functionality of hello gateway works except hello interactive operation support for Copy Wizard.</span></span>
*  <span data-ttu-id="d5ed1-164">Hallo robuustheid van gateway registreren met behulp van de registratiesleutel verbetert.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-164">Enhances hello robustness of gateway registration using registration key.</span></span>

## <a name="216040"></a><span data-ttu-id="d5ed1-165">2.1.6040.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-165">2.1.6040.</span></span>

*  <span data-ttu-id="d5ed1-166">DB2-stuurprogramma is nu opgenomen in Hallo gateway-installatiepakket.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-166">DB2 driver is included in hello gateway installation package now.</span></span> <span data-ttu-id="d5ed1-167">U hoeft geen tooinstall deze afzonderlijk.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-167">You do not need tooinstall it separately.</span></span>
*  <span data-ttu-id="d5ed1-168">DB2-stuurprogramma ondersteunt nu z-/ OS en DB2 voor ik (AS / 400) samen met de Hallo platformen die al worden ondersteund (Linux-, Unix- en Windows).</span><span class="sxs-lookup"><span data-stu-id="d5ed1-168">DB2 driver now supports z/OS and DB2 for i (AS/400) along with hello platforms already supported (Linux, Unix, and Windows).</span></span>
*  <span data-ttu-id="d5ed1-169">Ondersteunt het gebruik van Azure DB die Cosmos als een bron of bestemming voor on-premises gegevensopslagexemplaren</span><span class="sxs-lookup"><span data-stu-id="d5ed1-169">Supports using Azure Cosmos DB as a source or destination for on-premises data stores</span></span>
*  <span data-ttu-id="d5ed1-170">Ondersteunt het kopiëren van gegevens uit/toocold/hot blob-opslag samen met de Hallo al ondersteund algemeen opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-170">Supports copying data from/toocold/hot blob storage along with hello already supported general-purpose storage account.</span></span>
*  <span data-ttu-id="d5ed1-171">Hiermee kunt u tooconnect tooon-premises SQL Server via de gateway met machtigingen voor externe aanmelding.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-171">Allows you tooconnect tooon-premises SQL Server via gateway with remote login privileges.</span></span>  

## <a name="2060131"></a><span data-ttu-id="d5ed1-172">2.0.6013.1</span><span class="sxs-lookup"><span data-stu-id="d5ed1-172">2.0.6013.1</span></span>

*  <span data-ttu-id="d5ed1-173">Hallo taalcultuur/toobe die tijdens de handmatige installatie door een gateway gebruikt, kunt u selecteren.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-173">You can select hello language/culture toobe used by a gateway during manual installation.</span></span>

*  <span data-ttu-id="d5ed1-174">Wanneer de gateway werkt niet zoals verwacht, kunt u toosend gateway-logboeken van de afgelopen zeven dagen tooMicrosoft toofacilitate probleemoplossing van Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-174">When gateway does not work as expected, you can choose toosend gateway logs of last seven days tooMicrosoft toofacilitate troubleshooting of hello issue.</span></span> <span data-ttu-id="d5ed1-175">Als de gateway is niet verbonden toohello-cloudservice, kunt u kiezen toosave en archiveren van gateway-Logboeken.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-175">If gateway is not connected toohello cloud service, you can choose toosave and archive gateway logs.</span></span>  

*  <span data-ttu-id="d5ed1-176">Verbeteringen in de gebruikersinterface voor gateway configuration manager:</span><span class="sxs-lookup"><span data-stu-id="d5ed1-176">User interface improvements for gateway configuration manager:</span></span>

    *  <span data-ttu-id="d5ed1-177">Status van gateway meer zichtbaar maken op het tabblad Hallo-start.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-177">Make gateway status more visible on hello Home tab.</span></span>

    *  <span data-ttu-id="d5ed1-178">Ingedeeld en vereenvoudigd besturingselementen.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-178">Reorganized and simplified controls.</span></span>

    *  <span data-ttu-id="d5ed1-179">U kunt gegevens kopiëren van een opslagruimte met Hallo [voorbeeldfunctie code gratis exemplaar](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="d5ed1-179">You can copy data from a storage using hello [code-free copy preview tool](data-factory-copy-data-wizard-tutorial.md).</span></span> <span data-ttu-id="d5ed1-180">Zie [kopie gefaseerde](data-factory-copy-activity-performance.md#staged-copy) voor meer informatie over deze functie in het algemeen.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-180">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details about this feature in general.</span></span>
*  <span data-ttu-id="d5ed1-181">U kunt Data Management Gateway tooingress gegevens direct vanuit een on-premises SQL Server database in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-181">You can use Data Management Gateway tooingress data directly from an on-premises SQL Server database into Azure Machine Learning.</span></span>

*  <span data-ttu-id="d5ed1-182">Verbeterde prestaties</span><span class="sxs-lookup"><span data-stu-id="d5ed1-182">Performance improvements</span></span>

    * <span data-ttu-id="d5ed1-183">De prestaties weergeven/Preview-schemaversie op basis van SQL Server in code gratis exemplaar voorbeeldfunctie verbeteren.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-183">Improve performance on viewing Schema/Preview against SQL Server in code-free copy preview tool.</span></span>

## <a name="11259531"></a><span data-ttu-id="d5ed1-184">1.12.5953.1</span><span class="sxs-lookup"><span data-stu-id="d5ed1-184">1.12.5953.1</span></span>

*  <span data-ttu-id="d5ed1-185">Oplossingen voor problemen</span><span class="sxs-lookup"><span data-stu-id="d5ed1-185">Bug fixes</span></span>

## <a name="11159181"></a><span data-ttu-id="d5ed1-186">1.11.5918.1</span><span class="sxs-lookup"><span data-stu-id="d5ed1-186">1.11.5918.1</span></span>

*  <span data-ttu-id="d5ed1-187">Maximale grootte van het logboek voor systeemgebeurtenissen Hallo-gateway is verhoogd van 1 MB too40 MB.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-187">Maximum size of hello gateway event log has been increased from 1 MB too40 MB.</span></span>

*  <span data-ttu-id="d5ed1-188">Een dialoogvenster Beveiligingswaarschuwing wordt weergegeven als een herstart nodig is tijdens de gateway automatisch bijwerken.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-188">A warning dialog is displayed in case a restart is needed during gateway auto-update.</span></span> <span data-ttu-id="d5ed1-189">U kunt toorestart rechts vervolgens of hoger.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-189">You can choose toorestart right then or later.</span></span>

*  <span data-ttu-id="d5ed1-190">Als automatische updates is mislukt, probeert installatieprogramma van de gateway opnieuw automatische updates drie keer op maximum.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-190">In case auto-update fails, gateway installer retries auto-updating three times at maximum.</span></span>

*  <span data-ttu-id="d5ed1-191">Verbeterde prestaties</span><span class="sxs-lookup"><span data-stu-id="d5ed1-191">Performance improvements</span></span>

    * <span data-ttu-id="d5ed1-192">De prestaties voor het laden van grote tabellen van de lokale server in een scenario zonder code kopiëren verbeteren.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-192">Improve performance for loading large tables from on-premises server in code-free copy scenario.</span></span>

*  <span data-ttu-id="d5ed1-193">Oplossingen voor problemen</span><span class="sxs-lookup"><span data-stu-id="d5ed1-193">Bug fixes</span></span>

## <a name="11058921"></a><span data-ttu-id="d5ed1-194">1.10.5892.1</span><span class="sxs-lookup"><span data-stu-id="d5ed1-194">1.10.5892.1</span></span>

*  <span data-ttu-id="d5ed1-195">Verbeterde prestaties</span><span class="sxs-lookup"><span data-stu-id="d5ed1-195">Performance improvements</span></span>

*  <span data-ttu-id="d5ed1-196">Oplossingen voor problemen</span><span class="sxs-lookup"><span data-stu-id="d5ed1-196">Bug fixes</span></span>

## <a name="1958652"></a><span data-ttu-id="d5ed1-197">1.9.5865.2</span><span class="sxs-lookup"><span data-stu-id="d5ed1-197">1.9.5865.2</span></span>

*  <span data-ttu-id="d5ed1-198">Nul mogelijkheid touch automatische update</span><span class="sxs-lookup"><span data-stu-id="d5ed1-198">Zero touch auto update capability</span></span>
*  <span data-ttu-id="d5ed1-199">Pictogram in systeemvak voor nieuwe met statusindicatoren gateway</span><span class="sxs-lookup"><span data-stu-id="d5ed1-199">New tray icon with gateway status indicators</span></span>
*  <span data-ttu-id="d5ed1-200">De mogelijkheid te 'bijwerken nu' Hallo-client</span><span class="sxs-lookup"><span data-stu-id="d5ed1-200">Ability too“Update now” from hello client</span></span>
*  <span data-ttu-id="d5ed1-201">Tijd van de mogelijkheid tooset update plannen</span><span class="sxs-lookup"><span data-stu-id="d5ed1-201">Ability tooset update schedule time</span></span>
*  <span data-ttu-id="d5ed1-202">PowerShell-script voor het uitschakelen van automatische updates in-of uitschakelen</span><span class="sxs-lookup"><span data-stu-id="d5ed1-202">PowerShell script for toggling auto-update on/off</span></span>
*  <span data-ttu-id="d5ed1-203">Ondersteuning voor JSON-indeling</span><span class="sxs-lookup"><span data-stu-id="d5ed1-203">Support for JSON format</span></span>  
*  <span data-ttu-id="d5ed1-204">Verbeterde prestaties</span><span class="sxs-lookup"><span data-stu-id="d5ed1-204">Performance improvements</span></span>
*  <span data-ttu-id="d5ed1-205">Oplossingen voor problemen</span><span class="sxs-lookup"><span data-stu-id="d5ed1-205">Bug fixes</span></span>

## <a name="1858221"></a><span data-ttu-id="d5ed1-206">1.8.5822.1</span><span class="sxs-lookup"><span data-stu-id="d5ed1-206">1.8.5822.1</span></span>

*  <span data-ttu-id="d5ed1-207">Probleemoplossing-ervaring te verbeteren</span><span class="sxs-lookup"><span data-stu-id="d5ed1-207">Improve troubleshooting experience</span></span>
*  <span data-ttu-id="d5ed1-208">Verbeterde prestaties</span><span class="sxs-lookup"><span data-stu-id="d5ed1-208">Performance improvements</span></span>
*  <span data-ttu-id="d5ed1-209">Oplossingen voor problemen</span><span class="sxs-lookup"><span data-stu-id="d5ed1-209">Bug fixes</span></span>

### <a name="1757951"></a><span data-ttu-id="d5ed1-210">1.7.5795.1</span><span class="sxs-lookup"><span data-stu-id="d5ed1-210">1.7.5795.1</span></span>

*  <span data-ttu-id="d5ed1-211">Verbeterde prestaties</span><span class="sxs-lookup"><span data-stu-id="d5ed1-211">Performance improvements</span></span>
*  <span data-ttu-id="d5ed1-212">Oplossingen voor problemen</span><span class="sxs-lookup"><span data-stu-id="d5ed1-212">Bug fixes</span></span>

### <a name="1757641"></a><span data-ttu-id="d5ed1-213">1.7.5764.1</span><span class="sxs-lookup"><span data-stu-id="d5ed1-213">1.7.5764.1</span></span>

*  <span data-ttu-id="d5ed1-214">Verbeterde prestaties</span><span class="sxs-lookup"><span data-stu-id="d5ed1-214">Performance improvements</span></span>
*  <span data-ttu-id="d5ed1-215">Oplossingen voor problemen</span><span class="sxs-lookup"><span data-stu-id="d5ed1-215">Bug fixes</span></span>

### <a name="1657351"></a><span data-ttu-id="d5ed1-216">1.6.5735.1</span><span class="sxs-lookup"><span data-stu-id="d5ed1-216">1.6.5735.1</span></span>

*  <span data-ttu-id="d5ed1-217">Ondersteuning voor on-premises HDFS bron/Sink</span><span class="sxs-lookup"><span data-stu-id="d5ed1-217">Support on-premises HDFS Source/Sink</span></span>
*  <span data-ttu-id="d5ed1-218">Verbeterde prestaties</span><span class="sxs-lookup"><span data-stu-id="d5ed1-218">Performance improvements</span></span>
*  <span data-ttu-id="d5ed1-219">Oplossingen voor problemen</span><span class="sxs-lookup"><span data-stu-id="d5ed1-219">Bug fixes</span></span>

### <a name="1656961"></a><span data-ttu-id="d5ed1-220">1.6.5696.1</span><span class="sxs-lookup"><span data-stu-id="d5ed1-220">1.6.5696.1</span></span>

*  <span data-ttu-id="d5ed1-221">Verbeterde prestaties</span><span class="sxs-lookup"><span data-stu-id="d5ed1-221">Performance improvements</span></span>
*  <span data-ttu-id="d5ed1-222">Oplossingen voor problemen</span><span class="sxs-lookup"><span data-stu-id="d5ed1-222">Bug fixes</span></span>

### <a name="1656761"></a><span data-ttu-id="d5ed1-223">1.6.5676.1</span><span class="sxs-lookup"><span data-stu-id="d5ed1-223">1.6.5676.1</span></span>

*  <span data-ttu-id="d5ed1-224">Diagnostische hulpprogramma's voor ondersteuning in Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="d5ed1-224">Support diagnostic tools on Configuration Manager</span></span>
*  <span data-ttu-id="d5ed1-225">De tabelkolommen ondersteuning voor gegevensbronnen voor Azure Data Factory in tabelvorm</span><span class="sxs-lookup"><span data-stu-id="d5ed1-225">Support table columns for tabular data sources for Azure Data Factory</span></span>
*  <span data-ttu-id="d5ed1-226">Ondersteuning voor SQL DW voor Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d5ed1-226">Support SQL DW for Azure Data Factory</span></span>
*  <span data-ttu-id="d5ed1-227">Reclusive in BlobSource en FileSource ondersteuning voor Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d5ed1-227">Support Reclusive in BlobSource and FileSource for Azure Data Factory</span></span>
*  <span data-ttu-id="d5ed1-228">Ondersteuning voor CopyBehavior – MergeFiles PreserveHierarchy en FlattenHierarchy in BlobSink en FileSink met binaire kopie voor Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d5ed1-228">Support CopyBehavior – MergeFiles, PreserveHierarchy, and FlattenHierarchy in BlobSink and FileSink with Binary Copy for Azure Data Factory</span></span>
*  <span data-ttu-id="d5ed1-229">Ondersteuning voor Kopieeractiviteit rapportage voor Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d5ed1-229">Support Copy Activity reporting progress for Azure Data Factory</span></span>
*  <span data-ttu-id="d5ed1-230">Ondersteuning voor bron connectiviteit gegevensvalidatie voor Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d5ed1-230">Support Data Source Connectivity Validation for Azure Data Factory</span></span>
*  <span data-ttu-id="d5ed1-231">Oplossingen voor problemen</span><span class="sxs-lookup"><span data-stu-id="d5ed1-231">Bug fixes</span></span>

### <a name="1656721"></a><span data-ttu-id="d5ed1-232">1.6.5672.1</span><span class="sxs-lookup"><span data-stu-id="d5ed1-232">1.6.5672.1</span></span>

*  <span data-ttu-id="d5ed1-233">Naam van de tabel ondersteuning voor ODBC-gegevensbron voor Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d5ed1-233">Support table name for ODBC data source for Azure Data Factory</span></span>
*  <span data-ttu-id="d5ed1-234">Verbeterde prestaties</span><span class="sxs-lookup"><span data-stu-id="d5ed1-234">Performance improvements</span></span>
*  <span data-ttu-id="d5ed1-235">Oplossingen voor problemen</span><span class="sxs-lookup"><span data-stu-id="d5ed1-235">Bug fixes</span></span>

### <a name="1656581"></a><span data-ttu-id="d5ed1-236">1.6.5658.1</span><span class="sxs-lookup"><span data-stu-id="d5ed1-236">1.6.5658.1</span></span>

*  <span data-ttu-id="d5ed1-237">Ondersteuningsbestand van de Sink voor Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d5ed1-237">Support File Sink for Azure Data Factory</span></span>
*  <span data-ttu-id="d5ed1-238">Ondersteuning voor het behouden van hiërarchie in binaire kopie voor Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d5ed1-238">Support preserving hierarchy in binary copy for Azure Data Factory</span></span>
*  <span data-ttu-id="d5ed1-239">Kopiëren activiteit Idempotency ondersteuning voor Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d5ed1-239">Support Copy Activity Idempotency for Azure Data Factory</span></span>
*  <span data-ttu-id="d5ed1-240">Oplossingen voor problemen</span><span class="sxs-lookup"><span data-stu-id="d5ed1-240">Bug fixes</span></span>

### <a name="1656401"></a><span data-ttu-id="d5ed1-241">1.6.5640.1</span><span class="sxs-lookup"><span data-stu-id="d5ed1-241">1.6.5640.1</span></span>

*  <span data-ttu-id="d5ed1-242">Ondersteuning voor 3 meer gegevensbronnen voor Azure Data Factory (ODBC, OData, HDFS)</span><span class="sxs-lookup"><span data-stu-id="d5ed1-242">Support 3 more data sources for Azure Data Factory (ODBC, OData, HDFS)</span></span>
*  <span data-ttu-id="d5ed1-243">Aanhalingsteken in CSV-parser ondersteuning voor Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d5ed1-243">Support quote character in csv parser for Azure Data Factory</span></span>
*  <span data-ttu-id="d5ed1-244">Compressieondersteuning (BZip2)</span><span class="sxs-lookup"><span data-stu-id="d5ed1-244">Compression support (BZip2)</span></span>
*  <span data-ttu-id="d5ed1-245">Oplossingen voor problemen</span><span class="sxs-lookup"><span data-stu-id="d5ed1-245">Bug fixes</span></span>

### <a name="1556121"></a><span data-ttu-id="d5ed1-246">1.5.5612.1</span><span class="sxs-lookup"><span data-stu-id="d5ed1-246">1.5.5612.1</span></span>

*  <span data-ttu-id="d5ed1-247">Ondersteuning voor relationele databases van vijf voor Azure Data Factory (MySQL, PostgreSQL DB2, Teradata en Sybase)</span><span class="sxs-lookup"><span data-stu-id="d5ed1-247">Support five relational databases for Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata, and Sybase)</span></span>
*  <span data-ttu-id="d5ed1-248">Compressieondersteuning (Gzip en Deflate)</span><span class="sxs-lookup"><span data-stu-id="d5ed1-248">Compression support (Gzip and Deflate)</span></span>
*  <span data-ttu-id="d5ed1-249">Verbeterde prestaties</span><span class="sxs-lookup"><span data-stu-id="d5ed1-249">Performance improvements</span></span>
*  <span data-ttu-id="d5ed1-250">Oplossingen voor problemen</span><span class="sxs-lookup"><span data-stu-id="d5ed1-250">Bug fixes</span></span>

### <a name="1455491"></a><span data-ttu-id="d5ed1-251">1.4.5549.1</span><span class="sxs-lookup"><span data-stu-id="d5ed1-251">1.4.5549.1</span></span>

*  <span data-ttu-id="d5ed1-252">Oracle data source-ondersteuning voor Azure Data Factory toevoegen</span><span class="sxs-lookup"><span data-stu-id="d5ed1-252">Add Oracle data source support for Azure Data Factory</span></span>
*  <span data-ttu-id="d5ed1-253">Verbeterde prestaties</span><span class="sxs-lookup"><span data-stu-id="d5ed1-253">Performance improvements</span></span>
*  <span data-ttu-id="d5ed1-254">Oplossingen voor problemen</span><span class="sxs-lookup"><span data-stu-id="d5ed1-254">Bug fixes</span></span>

### <a name="1454921"></a><span data-ttu-id="d5ed1-255">1.4.5492.1</span><span class="sxs-lookup"><span data-stu-id="d5ed1-255">1.4.5492.1</span></span>

*  <span data-ttu-id="d5ed1-256">Unified binair die ondersteuning biedt voor zowel Microsoft Azure Data Factory als Power BI voor Office 365-services</span><span class="sxs-lookup"><span data-stu-id="d5ed1-256">Unified binary that supports both Microsoft Azure Data Factory and Office 365 Power BI services</span></span>
*  <span data-ttu-id="d5ed1-257">Verfijnen Hallo Configuratiegebruikersinterface en registratie-proces</span><span class="sxs-lookup"><span data-stu-id="d5ed1-257">Refine hello Configuration UI and registration process</span></span>
*  <span data-ttu-id="d5ed1-258">Azure Data Factory – Azure inkomende en uitgaande ondersteuning voor SQL Server-gegevensbron</span><span class="sxs-lookup"><span data-stu-id="d5ed1-258">Azure Data Factory – Azure Ingress and Egress support for SQL Server data source</span></span>

### <a name="1253031"></a><span data-ttu-id="d5ed1-259">1.2.5303.1</span><span class="sxs-lookup"><span data-stu-id="d5ed1-259">1.2.5303.1</span></span>

*  <span data-ttu-id="d5ed1-260">Los time-out probleem toosupport meer tijdrovend gegevensbronverbindingen.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-260">Fix timeout issue toosupport more time-consuming data source connections.</span></span>

### <a name="1155268"></a><span data-ttu-id="d5ed1-261">1.1.5526.8</span><span class="sxs-lookup"><span data-stu-id="d5ed1-261">1.1.5526.8</span></span>

*  <span data-ttu-id="d5ed1-262">.NET Framework 4.5.1 is vereist als een vereiste tijdens de installatie.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-262">Requires .NET Framework 4.5.1 as a prerequisite during setup.</span></span>

### <a name="1051442"></a><span data-ttu-id="d5ed1-263">1.0.5144.2</span><span class="sxs-lookup"><span data-stu-id="d5ed1-263">1.0.5144.2</span></span>

*  <span data-ttu-id="d5ed1-264">Er zijn geen wijzigingen die invloed hebben op Azure Data Factory-scenario's.</span><span class="sxs-lookup"><span data-stu-id="d5ed1-264">No changes that affect Azure Data Factory scenarios.</span></span>
