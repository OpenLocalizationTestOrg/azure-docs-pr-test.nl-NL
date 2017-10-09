---
title: gegevens in Azure Hadoop - Library Microsoft Avro - aaaSerialize | Microsoft Docs
description: Meer informatie over hoe tooserialize en deserialiseren van gegevens in Hadoop in HDInsight met Hallo Microsoft Avro Library toopersist toomemory, een database of een bestand.
keywords: avro, hadoop avro
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: c78dc20d-5d8d-4366-94ac-abbe89aaac58
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jgao
ms.custom: hdiseo17may2017
ms.openlocfilehash: f364f8e855a54c0fc160e9a106ec8d5b30c6db23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="serialize-data-in-hadoop-with-hello-microsoft-avro-library"></a><span data-ttu-id="5842c-104">Gegevens in Hadoop Hello Microsoft Avro Library serialiseren</span><span class="sxs-lookup"><span data-stu-id="5842c-104">Serialize data in Hadoop with hello Microsoft Avro Library</span></span>

>[!NOTE]
><span data-ttu-id="5842c-105">Hallo Avro SDK wordt niet langer ondersteund door Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5842c-105">hello Avro SDK is no longer supported by Microsoft.</span></span> <span data-ttu-id="5842c-106">Hallo-bibliotheek is open-source community ondersteund.</span><span class="sxs-lookup"><span data-stu-id="5842c-106">hello library is open source community supported.</span></span> <span data-ttu-id="5842c-107">Hallo-bronnen voor Hallo bibliotheek bevinden zich in [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span><span class="sxs-lookup"><span data-stu-id="5842c-107">hello sources for hello library are located in [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

<span data-ttu-id="5842c-108">Dit onderwerp wordt beschreven hoe toouse hello [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) tooserialize objecten en andere gegevens structuren in streams toopersist ze toomemory, een database of een bestand.</span><span class="sxs-lookup"><span data-stu-id="5842c-108">This topic shows how toouse hello [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) tooserialize objects and other data structures into streams toopersist them toomemory, a database, or a file.</span></span> <span data-ttu-id="5842c-109">U ziet ook hoe toodeserialize ze toorecover Hallo originele objecten.</span><span class="sxs-lookup"><span data-stu-id="5842c-109">It also shows how toodeserialize them toorecover hello original objects.</span></span>

[!INCLUDE [windows-only](../../includes/hdinsight-windows-only.md)]

## <a name="apache-avro"></a><span data-ttu-id="5842c-110">Apache Avro</span><span class="sxs-lookup"><span data-stu-id="5842c-110">Apache Avro</span></span>
<span data-ttu-id="5842c-111">Hallo <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implements Hallo systeem voor serialisatie Apache Avro voor Hallo Microsoft.NET-omgeving.</span><span class="sxs-lookup"><span data-stu-id="5842c-111">hello <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implements hello Apache Avro data serialization system for hello Microsoft.NET environment.</span></span> <span data-ttu-id="5842c-112">Apache Avro biedt een compacte binaire gegevens DIF-indeling voor serialisatie.</span><span class="sxs-lookup"><span data-stu-id="5842c-112">Apache Avro provides a compact binary data interchange format for serialization.</span></span> <span data-ttu-id="5842c-113">Hierbij <a href="http://www.json.org" target="_blank">JSON</a> toodefine een taal networkdirect-schema dat taalherkenning interoperabiliteit van talen.</span><span class="sxs-lookup"><span data-stu-id="5842c-113">It uses <a href="http://www.json.org" target="_blank">JSON</a> toodefine a language-agnostic schema that underwrites language interoperability.</span></span> <span data-ttu-id="5842c-114">Gegevens die zijn geserialiseerd in één taal kan worden gelezen in een andere.</span><span class="sxs-lookup"><span data-stu-id="5842c-114">Data serialized in one language can be read in another.</span></span> <span data-ttu-id="5842c-115">C, C++ C#, Java, PHP, Python en Ruby worden momenteel ondersteund.</span><span class="sxs-lookup"><span data-stu-id="5842c-115">Currently C, C++, C#, Java, PHP, Python, and Ruby are supported.</span></span> <span data-ttu-id="5842c-116">Gedetailleerde informatie over het Hallo-indeling vindt u in Hallo <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro-specificatie</a>.</span><span class="sxs-lookup"><span data-stu-id="5842c-116">Detailed information on hello format can be found in hello <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro Specification</a>.</span></span> 

>[!NOTE]
><span data-ttu-id="5842c-117">Hallo Microsoft Avro Library biedt geen ondersteuning voor Hallo externe procedureaanroepen (RPC's)-aanroepen deel van deze specificatie.</span><span class="sxs-lookup"><span data-stu-id="5842c-117">hello Microsoft Avro Library does not support hello remote procedure calls (RPCs) part of this specification.</span></span>
>

<span data-ttu-id="5842c-118">Hallo geserialiseerd representatie van een object in Hallo Avro-systeem bestaat uit twee delen: schema en de werkelijke waarde.</span><span class="sxs-lookup"><span data-stu-id="5842c-118">hello serialized representation of an object in hello Avro system consists of two parts: schema and actual value.</span></span> <span data-ttu-id="5842c-119">Hallo Avro-schema beschrijft Hallo taalonafhankelijke gegevensmodel van Hallo geserialiseerd gegevens met JSON.</span><span class="sxs-lookup"><span data-stu-id="5842c-119">hello Avro schema describes hello language-independent data model of hello serialized data with JSON.</span></span> <span data-ttu-id="5842c-120">Deze functionaliteit wordt weergegeven naast een binaire voorstelling van gegevens.</span><span class="sxs-lookup"><span data-stu-id="5842c-120">It is presented side by side with a binary representation of data.</span></span> <span data-ttu-id="5842c-121">Hallo-schema is gescheiden van de binaire voorstelling Hallo met staat elk object toobe geschreven met de overhead van geen per waarde, waardoor serialisatie snel en hello weergave kleine.</span><span class="sxs-lookup"><span data-stu-id="5842c-121">Having hello schema separate from hello binary representation permits each object toobe written with no per-value overheads, making serialization fast, and hello representation small.</span></span>

## <a name="hello-hadoop-scenario"></a><span data-ttu-id="5842c-122">Hallo Hadoop-scenario</span><span class="sxs-lookup"><span data-stu-id="5842c-122">hello Hadoop scenario</span></span>
<span data-ttu-id="5842c-123">Hallo Apache Avro serialisatie-indeling wordt veel gebruikt in Azure HDInsight en andere Apache Hadoop-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="5842c-123">hello Apache Avro serialization format is widely used in Azure HDInsight and other Apache Hadoop environments.</span></span> <span data-ttu-id="5842c-124">Avro biedt een handige manier toorepresent complexe gegevensstructuren binnen een Hadoop-MapReduce-taak.</span><span class="sxs-lookup"><span data-stu-id="5842c-124">Avro provides a convenient way toorepresent complex data structures within a Hadoop MapReduce job.</span></span> <span data-ttu-id="5842c-125">Hallo-indeling van het Avro-bestanden (Avro object container-bestand) is ontworpen toosupport Hallo gedistribueerde MapReduce-programmeermodel.</span><span class="sxs-lookup"><span data-stu-id="5842c-125">hello format of Avro files (Avro object container file) has been designed toosupport hello distributed MapReduce programming model.</span></span> <span data-ttu-id="5842c-126">Hallo belangrijke functie waarmee Hallo gedistribueerd is dat bestanden Hallo 'splittable' in de zin Hallo één kunt elk punt in een bestand en beginnen met lezen van een bepaald blok zijn.</span><span class="sxs-lookup"><span data-stu-id="5842c-126">hello key feature that enables hello distribution is that hello files are “splittable” in hello sense that one can seek any point in a file and start reading from a particular block.</span></span>

## <a name="serialization-in-avro-library"></a><span data-ttu-id="5842c-127">Serialisatie in de bibliotheek voor Avro</span><span class="sxs-lookup"><span data-stu-id="5842c-127">Serialization in Avro Library</span></span>
<span data-ttu-id="5842c-128">Hallo .NET-bibliotheek voor Avro ondersteunt serialiseren objecten op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="5842c-128">hello .NET Library for Avro supports two ways of serializing objects:</span></span>

* <span data-ttu-id="5842c-129">**Reflectie** -Hallo JSON-schema voor Hallo typen automatisch gebouwd van Hallo gegevens contract kenmerken van Hallo .NET typen toobe geserialiseerd.</span><span class="sxs-lookup"><span data-stu-id="5842c-129">**reflection** - hello JSON schema for hello types is automatically built from hello data contract attributes of hello .NET types toobe serialized.</span></span>
* <span data-ttu-id="5842c-130">**algemene record** -een JSON-schema expliciet is opgegeven in een record die wordt vertegenwoordigd door Hallo [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) wanneer er geen .NET-typen aanwezig toodescribe Hallo-schema voor Hallo gegevens toobe zijn klasse geserialiseerd.</span><span class="sxs-lookup"><span data-stu-id="5842c-130">**generic record** - A JSON schema is explicitly specified in a record represented by hello [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) class when no .NET types are present toodescribe hello schema for hello data toobe serialized.</span></span>

<span data-ttu-id="5842c-131">Hallo gegevensschema is bekend tooboth Hallo writer en lezer van de stroom hello, kan Hallo gegevens kunnen worden verzonden zonder dat het schema.</span><span class="sxs-lookup"><span data-stu-id="5842c-131">When hello data schema is known tooboth hello writer and reader of hello stream, hello data can be sent without its schema.</span></span> <span data-ttu-id="5842c-132">In gevallen dat wanneer een Avro-object container-bestand wordt gebruikt, Hallo schema wordt opgeslagen in Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="5842c-132">In cases when an Avro object container file is used, hello schema is stored within hello file.</span></span> <span data-ttu-id="5842c-133">Andere parameters, zoals Hallo codec gebruikt voor de compressie van gegevens kunnen worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="5842c-133">Other parameters, such as hello codec used for data compression, can be specified.</span></span> <span data-ttu-id="5842c-134">Deze scenario's zijn in meer detail beschreven en wordt geïllustreerd in de volgende codevoorbeelden Hallo:</span><span class="sxs-lookup"><span data-stu-id="5842c-134">These scenarios are outlined in more detail and illustrated in hello following code examples:</span></span>

## <a name="install-avro-library"></a><span data-ttu-id="5842c-135">Bibliotheek voor Avro installeren</span><span class="sxs-lookup"><span data-stu-id="5842c-135">Install Avro Library</span></span>
<span data-ttu-id="5842c-136">Hallo volgende is vereist voordat u Hallo bibliotheek installeert:</span><span class="sxs-lookup"><span data-stu-id="5842c-136">hello following are required before you install hello library:</span></span>

* <span data-ttu-id="5842c-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span><span class="sxs-lookup"><span data-stu-id="5842c-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span></span>
* <span data-ttu-id="5842c-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 of hoger)</span><span class="sxs-lookup"><span data-stu-id="5842c-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 or later)</span></span>

<span data-ttu-id="5842c-139">Houd er rekening mee dat Hallo Newtonsoft.Json.dll afhankelijkheid wordt automatisch gedownload met de installatie Hallo Hallo Microsoft Avro Library.</span><span class="sxs-lookup"><span data-stu-id="5842c-139">Note that hello Newtonsoft.Json.dll dependency is downloaded automatically with hello installation of hello Microsoft Avro Library.</span></span> <span data-ttu-id="5842c-140">Hallo-procedure is opgegeven in de volgende sectie Hallo:</span><span class="sxs-lookup"><span data-stu-id="5842c-140">hello procedure is provided in hello following section:</span></span>

<span data-ttu-id="5842c-141">Hallo Microsoft Avro Library wordt gedistribueerd als een NuGet-pakket dat kan worden geïnstalleerd vanuit Visual Studio via Hallo procedure te volgen:</span><span class="sxs-lookup"><span data-stu-id="5842c-141">hello Microsoft Avro Library is distributed as a NuGet package that can be installed from Visual Studio via hello following procedure:</span></span>

1. <span data-ttu-id="5842c-142">Selecteer Hallo **Project** tabblad -> **NuGet-pakketten beheren...**</span><span class="sxs-lookup"><span data-stu-id="5842c-142">Select hello **Project** tab -> **Manage NuGet Packages...**</span></span>
2. <span data-ttu-id="5842c-143">Zoek naar 'Microsoft.Hadoop.Avro' in hello **Online zoeken** vak.</span><span class="sxs-lookup"><span data-stu-id="5842c-143">Search for "Microsoft.Hadoop.Avro" in hello **Search Online** box.</span></span>
3. <span data-ttu-id="5842c-144">Klik op Hallo **installeren** knop naast te**Avro-bibliotheek van Microsoft Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="5842c-144">Click hello **Install** button next too**Microsoft Azure HDInsight Avro Library**.</span></span>

<span data-ttu-id="5842c-145">Houd er rekening mee dat Hallo Newtonsoft.Json.dll (> = 6.0.4) afhankelijkheid ook automatisch wordt gedownload Hello Microsoft Avro Library.</span><span class="sxs-lookup"><span data-stu-id="5842c-145">Note that hello Newtonsoft.Json.dll (>=6.0.4) dependency is also downloaded automatically with hello Microsoft Avro Library.</span></span>

<span data-ttu-id="5842c-146">Hallo Microsoft Avro Library broncode is beschikbaar op [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span><span class="sxs-lookup"><span data-stu-id="5842c-146">hello Microsoft Avro Library source code is available at [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

## <a name="compile-schemas-using-avro-library"></a><span data-ttu-id="5842c-147">Schema's met behulp van de bibliotheek voor Avro compileren</span><span class="sxs-lookup"><span data-stu-id="5842c-147">Compile schemas using Avro Library</span></span>
<span data-ttu-id="5842c-148">Hallo Microsoft Avro Library bevat een codegeneratie hulpprogramma waarmee het maken van C#-typen automatisch op basis van Hallo eerder JSON-schema is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="5842c-148">hello Microsoft Avro Library contains a code generation utility that allows creating C# types automatically based on hello previously defined JSON schema.</span></span> <span data-ttu-id="5842c-149">Hallo code generatie hulpprogramma niet is gedistribueerd als een binair uitvoerbaar bestand, maar kan eenvoudig worden opgebouwd via Hallo procedure te volgen:</span><span class="sxs-lookup"><span data-stu-id="5842c-149">hello code generation utility is not distributed as a binary executable, but can be easily built via hello following procedure:</span></span>

1. <span data-ttu-id="5842c-150">Hallo ZIP-bestand met de meest recente versie Hallo van broncode HDInsight SDK uit downloaden <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK voor Hadoop</a>.</span><span class="sxs-lookup"><span data-stu-id="5842c-150">Download hello .zip file with hello latest version of HDInsight SDK source code from <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK For Hadoop</a>.</span></span> <span data-ttu-id="5842c-151">(Klik op Hallo **downloaden** pictogram, niet Hallo **downloadt** tabblad.)</span><span class="sxs-lookup"><span data-stu-id="5842c-151">(Click hello **Download** icon, not hello **Downloads** tab.)</span></span>
2. <span data-ttu-id="5842c-152">Pak Hallo HDInsight SDK tooa map op de machine Hallo met .NET Framework 4 geïnstalleerd en toohello Internet verbonden voor het downloaden van de vereiste afhankelijkheid NuGet-pakketten.</span><span class="sxs-lookup"><span data-stu-id="5842c-152">Extract hello HDInsight SDK tooa directory on hello machine with .NET Framework 4 installed and connected toohello Internet for downloading necessary dependency NuGet packages.</span></span> <span data-ttu-id="5842c-153">Hieronder, gaan we ervan uit dat de broncode Hallo uitgepakte tooC:\SDK is.</span><span class="sxs-lookup"><span data-stu-id="5842c-153">Below, we assume that hello source code is extracted tooC:\SDK.</span></span>
3. <span data-ttu-id="5842c-154">Ga toohello map C:\SDK\src\Microsoft.Hadoop.Avro.Tools en build.bat uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5842c-154">Go toohello folder C:\SDK\src\Microsoft.Hadoop.Avro.Tools and run build.bat.</span></span> <span data-ttu-id="5842c-155">(Hallo bestandsaanroepen MSBuild van Hallo 32-bits distributie van Hallo .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="5842c-155">(hello file calls MSBuild from hello 32-bit distribution of hello .NET Framework.</span></span> <span data-ttu-id="5842c-156">Indien toouse Hallo 64-bits versie gewenst, bewerk build.bat, Hallo opmerkingen in Hallo-bestand te volgen.) Zorg ervoor dat Hallo build geslaagd.</span><span class="sxs-lookup"><span data-stu-id="5842c-156">If you would like toouse hello 64-bit version, edit build.bat, following hello comments inside hello file.) Ensure that hello build is successful.</span></span> <span data-ttu-id="5842c-157">(Op sommige systemen MSBuild kan leiden tot waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="5842c-157">(On some systems, MSBuild may produce warnings.</span></span> <span data-ttu-id="5842c-158">Deze waarschuwingen hebben geen invloed op Hallo hulpprogramma, zolang er geen fouten build zijn.)</span><span class="sxs-lookup"><span data-stu-id="5842c-158">These warnings do not affect hello utility as long as there are no build errors.)</span></span>
4. <span data-ttu-id="5842c-159">Hallo gecompileerd hulpprogramma bevindt zich in C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.</span><span class="sxs-lookup"><span data-stu-id="5842c-159">hello compiled utility is located in C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.</span></span>

<span data-ttu-id="5842c-160">tooget bekend bent met de opdrachtregelsyntaxis Hallo Hallo volgende opdracht uit Hallo map bevindt Hallo code generatie hulpprogramma uitvoeren:`Microsoft.Hadoop.Avro.Tools help /c:codegen`</span><span class="sxs-lookup"><span data-stu-id="5842c-160">tooget familiar with hello command-line syntax, execute hello following command from hello folder where hello code generation utility is located: `Microsoft.Hadoop.Avro.Tools help /c:codegen`</span></span>

<span data-ttu-id="5842c-161">tootest hello hulpprogramma, kunt u C#-klassen genereren van het Hallo JSON-schema voorbeeldbestand Hallo broncode voorzien.</span><span class="sxs-lookup"><span data-stu-id="5842c-161">tootest hello utility, you can generate C# classes from hello sample JSON schema file provided with hello source code.</span></span> <span data-ttu-id="5842c-162">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5842c-162">Execute hello following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:

<span data-ttu-id="5842c-163">Dit moet tooproduce twee C#-bestanden in de huidige map Hallo: SensorData.cs en Location.cs.</span><span class="sxs-lookup"><span data-stu-id="5842c-163">This is supposed tooproduce two C# files in hello current directory: SensorData.cs and Location.cs.</span></span>

<span data-ttu-id="5842c-164">toounderstand hello logica die Hallo code generatie hulpprogramma wordt gebruikt tijdens het converteren van typen tooC # Hallo JSON-schema, Zie Hallo bestand GenerationVerification.feature in C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.</span><span class="sxs-lookup"><span data-stu-id="5842c-164">toounderstand hello logic that hello code generation utility is using while converting hello JSON schema tooC# types, see hello file GenerationVerification.feature located in C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.</span></span>

<span data-ttu-id="5842c-165">Naamruimten worden opgehaald uit Hallo-JSON-schema met behulp van Hallo logica in factoren in de vorige alinea Hallo Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="5842c-165">Namespaces are extracted from hello JSON schema, using hello logic described in hello file mentioned in hello previous paragraph.</span></span> <span data-ttu-id="5842c-166">Naamruimten die worden opgehaald uit Hallo schema hebben voorrang op wat wordt geleverd bij Hallo/n parameter in opdrachtregel Hallo-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="5842c-166">Namespaces extracted from hello schema take precedence over whatever is provided with hello /n parameter in hello utility command line.</span></span> <span data-ttu-id="5842c-167">Als u toooverride Hallo naamruimten die zich in het Hallo-schema wilt, gebruikt u Hallo /nf parameter.</span><span class="sxs-lookup"><span data-stu-id="5842c-167">If you want toooverride hello namespaces contained within hello schema, use hello /nf parameter.</span></span> <span data-ttu-id="5842c-168">Bijvoorbeeld toochange alle naamruimten van Hallo SampleJSONSchema.avsc toomy.own.nspace, uitvoeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="5842c-168">For example, toochange all namespaces from hello SampleJSONSchema.avsc toomy.own.nspace, execute hello following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:. /nf:my.own.nspace

## <a name="about-hello-samples"></a><span data-ttu-id="5842c-169">Over het Hallo-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="5842c-169">About hello samples</span></span>
<span data-ttu-id="5842c-170">Zes voorbeelden vindt u in dit onderwerp ziet u verschillende scenario's die worden ondersteund door Hallo Microsoft Avro Library.</span><span class="sxs-lookup"><span data-stu-id="5842c-170">Six examples provided in this topic illustrate different scenarios supported by hello Microsoft Avro Library.</span></span> <span data-ttu-id="5842c-171">Hallo Microsoft Avro Library is ontworpen toowork met elke andere stroom.</span><span class="sxs-lookup"><span data-stu-id="5842c-171">hello Microsoft Avro Library is designed toowork with any stream.</span></span> <span data-ttu-id="5842c-172">In deze voorbeelden wordt gegevens gemanipuleerd via geheugen gegevensstromen in plaats van bestand streams of databases voor eenvoud en consistentie.</span><span class="sxs-lookup"><span data-stu-id="5842c-172">In these examples, data is manipulated via memory streams rather than file streams or databases for simplicity and consistency.</span></span> <span data-ttu-id="5842c-173">Hallo aanpak in een productieomgeving, is afhankelijk van de exacte scenariovereisten hello, gegevensbron en volume, prestaties beperkingen en andere factoren.</span><span class="sxs-lookup"><span data-stu-id="5842c-173">hello approach taken in a production environment depends on hello exact scenario requirements, data source and volume, performance constraints, and other factors.</span></span>

<span data-ttu-id="5842c-174">eerste twee voorbeelden kunt u zien hoe Hallo tooserialize en gegevens in geheugenbuffers stroom deserialiseren via reflectie en algemene records.</span><span class="sxs-lookup"><span data-stu-id="5842c-174">hello first two examples show how tooserialize and deserialize data into memory stream buffers by using reflection and generic records.</span></span> <span data-ttu-id="5842c-175">Hallo schema in beide gevallen wordt aangenomen dat toobe gedeeld tussen hello en schrijfprogramma out-of-band.</span><span class="sxs-lookup"><span data-stu-id="5842c-175">hello schema in these two cases is assumed toobe shared between hello readers and writers out-of-band.</span></span>

<span data-ttu-id="5842c-176">Hallo derde en vierde voorbeelden kunt u zien hoe tooserialize en deserialiseren van gegevens met behulp van Hallo Avro object containerbestanden.</span><span class="sxs-lookup"><span data-stu-id="5842c-176">hello third and fourth examples show how tooserialize and deserialize data by using hello Avro object container files.</span></span> <span data-ttu-id="5842c-177">Wanneer gegevens worden opgeslagen in een Avro-container-bestand, wordt het schema is altijd met het opgeslagen omdat Hallo schema moet worden gedeeld voor deserialisatie.</span><span class="sxs-lookup"><span data-stu-id="5842c-177">When data is stored in an Avro container file, its schema is always stored with it because hello schema must be shared for deserialization.</span></span>

<span data-ttu-id="5842c-178">Hallo voorbeeld waarin Hallo eerste vier voorbeelden kunnen worden gedownload vanuit Hallo <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Azure codevoorbeelden</a> site.</span><span class="sxs-lookup"><span data-stu-id="5842c-178">hello sample containing hello first four examples can be downloaded from hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="5842c-179">Hallo vijfde voorbeeld ziet u hoe een aangepaste compressiecodec voor Avro toouse containerbestanden object.</span><span class="sxs-lookup"><span data-stu-id="5842c-179">hello fifth example shows how toouse a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="5842c-180">Een voorbeeld van een met Hallo-code voor dit voorbeeld kan worden gedownload vanaf Hallo <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Azure codevoorbeelden</a> site.</span><span class="sxs-lookup"><span data-stu-id="5842c-180">A sample containing hello code for this example can be downloaded from hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="5842c-181">Hallo zesde voorbeeld toont hoe toouse Avro serialisatie tooupload gegevens tooAzure Blob storage en vervolgens te analyseren met behulp van Hive met een HDInsight (Hadoop)-cluster.</span><span class="sxs-lookup"><span data-stu-id="5842c-181">hello sixth sample shows how toouse Avro serialization tooupload data tooAzure Blob storage and then analyze it by using Hive with an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="5842c-182">Het kan worden gedownload vanaf Hallo <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Azure codevoorbeelden</a> site.</span><span class="sxs-lookup"><span data-stu-id="5842c-182">It can be downloaded from hello <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="5842c-183">Hier vindt u koppelingen toohello zes voorbeelden in Hallo onderwerp besproken:</span><span class="sxs-lookup"><span data-stu-id="5842c-183">Here are links toohello six samples discussed in hello topic:</span></span>

* <span data-ttu-id="5842c-184"><a href="#Scenario1">**Serialisatie met reflectie** </a> -Hallo JSON-schema voor typen toobe geserialiseerd automatisch gebouwd van Hallo gegevens contract kenmerken.</span><span class="sxs-lookup"><span data-stu-id="5842c-184"><a href="#Scenario1">**Serialization with reflection**</a> - hello JSON schema for types toobe serialized is automatically built from hello data contract attributes.</span></span>
* <span data-ttu-id="5842c-185"><a href="#Scenario2">**Serialisatie met algemene record** </a> -Hallo JSON-schema is expliciet worden opgegeven in een record wanneer er geen .NET-type beschikbaar voor reflectie is.</span><span class="sxs-lookup"><span data-stu-id="5842c-185"><a href="#Scenario2">**Serialization with generic record**</a> - hello JSON schema is explicitly specified in a record when no .NET type is available for reflection.</span></span>
* <span data-ttu-id="5842c-186"><a href="#Scenario3">**Gebruik van object containerbestanden met reflectie serialisatie** </a> -Hallo JSON-schema automatisch is gemaakt en gedeeld samen met de Hallo geserialiseerd gegevens via een Avro-object container-bestand.</span><span class="sxs-lookup"><span data-stu-id="5842c-186"><a href="#Scenario3">**Serialization using object container files with reflection**</a> - hello JSON schema is automatically built and shared together with hello serialized data via an Avro object container file.</span></span>
* <span data-ttu-id="5842c-187"><a href="#Scenario4">**Serialisatie in object containerbestanden met algemene record** </a> -Hallo JSON-schema expliciet is opgegeven voordat Hallo serialisatie en gedeeld samen met de Hallo gegevens via een Avro-object container-bestand.</span><span class="sxs-lookup"><span data-stu-id="5842c-187"><a href="#Scenario4">**Serialization using object container files with generic record**</a> - hello JSON schema is explicitly specified before hello serialization and shared together with hello data via an Avro object container file.</span></span>
* <span data-ttu-id="5842c-188"><a href="#Scenario5">**Gebruik van object containerbestanden met een aangepaste compressiecodec serialisatie** </a> -Hallo voorbeeld ziet u hoe een Avro toocreate containerbestand met een aangepaste .NET-implementatie van Hallo Deflate gegevens compressiecodec object.</span><span class="sxs-lookup"><span data-stu-id="5842c-188"><a href="#Scenario5">**Serialization using object container files with a custom compression codec**</a> - hello example shows how toocreate an Avro object container file with a customized .NET implementation of hello Deflate data compression codec.</span></span>
* <span data-ttu-id="5842c-189"><a href="#Scenario6">**Met behulp van Avro tooupload gegevens voor Microsoft Azure HDInsight-service Hallo** </a> -Hallo voorbeeld ziet u hoe de Avro-serialisatie samenwerkt met Hallo HDInsight-service.</span><span class="sxs-lookup"><span data-stu-id="5842c-189"><a href="#Scenario6">**Using Avro tooupload data for hello Microsoft Azure HDInsight service**</a> - hello example illustrates how Avro serialization interacts with hello HDInsight service.</span></span> <span data-ttu-id="5842c-190">Een actief Azure-abonnement en toegang tooan Azure HDInsight-cluster vereist toorun in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="5842c-190">An active Azure subscription and access tooan Azure HDInsight cluster are required toorun this example.</span></span>

## <span data-ttu-id="5842c-191"><a name="Scenario1"></a>Voorbeeld 1: Serialisatie met reflectie</span><span class="sxs-lookup"><span data-stu-id="5842c-191"><a name="Scenario1"></a>Sample 1: Serialization with reflection</span></span>
<span data-ttu-id="5842c-192">Hallo JSON-schema voor Hallo-typen kan worden automatisch gebouwd door Hallo Microsoft Avro Library via reflectie uit Hallo gegevens contract kenmerken van Hallo C#-objecten toobe geserialiseerd.</span><span class="sxs-lookup"><span data-stu-id="5842c-192">hello JSON schema for hello types can be automatically built by hello Microsoft Avro Library via reflection from hello data contract attributes of hello C# objects toobe serialized.</span></span> <span data-ttu-id="5842c-193">Hallo Microsoft Avro Library maakt een [ **IAvroSeralizer<T>**  ](http://msdn.microsoft.com/library/dn627341.aspx) tooidentify Hallo velden toobe geserialiseerd.</span><span class="sxs-lookup"><span data-stu-id="5842c-193">hello Microsoft Avro Library creates an [**IAvroSeralizer<T>**](http://msdn.microsoft.com/library/dn627341.aspx) tooidentify hello fields toobe serialized.</span></span>

<span data-ttu-id="5842c-194">In dit voorbeeld objecten (een **SensorData** klasse met een lid **locatie** struct) geserialiseerde tooa geheugenstroom zijn en deze stroom op zijn beurt wordt gedeserialiseerd.</span><span class="sxs-lookup"><span data-stu-id="5842c-194">In this example, objects (a **SensorData** class with a member **Location** struct) are serialized tooa memory stream, and this stream is in turn deserialized.</span></span> <span data-ttu-id="5842c-195">Hallo resultaat wordt vervolgens vergeleken toohello in eerste instantie tooconfirm die Hallo **SensorData** hersteld-object is identiek toohello oorspronkelijke.</span><span class="sxs-lookup"><span data-stu-id="5842c-195">hello result is then compared toohello initial instance tooconfirm that hello **SensorData** object recovered is identical toohello original.</span></span>

<span data-ttu-id="5842c-196">Hallo-schema in dit voorbeeld wordt uitgegaan van toobe gedeeld tussen hello en schrijfprogramma, dus containerindeling van Hallo Avro-object niet vereist is.</span><span class="sxs-lookup"><span data-stu-id="5842c-196">hello schema in this example is assumed toobe shared between hello readers and writers, so hello Avro object container format is not required.</span></span> <span data-ttu-id="5842c-197">Voor een voorbeeld van hoe tooserialize en deserialiseren van gegevens in geheugenbuffers via reflectie met containerindeling Hallo-object als Hallo schema moet worden gedeeld met Hallo gegevens, Zie <a href="#Scenario3">serialisatie in object containerbestanden met reflectie</a>.</span><span class="sxs-lookup"><span data-stu-id="5842c-197">For an example of how tooserialize and deserialize data into memory buffers by using reflection with hello object container format when hello schema must be shared with hello data, see <a href="#Scenario3">Serialization using object container files with reflection</a>.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serialize and deserialize sample data set represented as an object using reflection.
            //No explicit schema definition is required - schema of serialized objects is automatically built.
            public void SerializeDeserializeObjectUsingReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION\n");
                Console.WriteLine("Serializing Sample Data Set...");

                //Create a new AvroSerializer instance and specify a custom serialization strategy AvroDataContractResolver
                //for serializing only properties attributed with DataContract/DateMember
                var avroSerializer = AvroSerializer.Create<SensorData>();

                //Create a memory stream buffer
                using (var buffer = new MemoryStream())
                {
                    //Create a data set by using sample class and struct
                    var expected = new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } };

                    //Serialize hello data toohello specified stream
                    avroSerializer.Serialize(buffer, expected);


                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Deserialize data from hello stream and cast it toohello same type used for serialization
                    var actual = avroSerializer.Deserialize(buffer);

                    Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                    //Finally, verify that deserialized data matches hello original one
                    bool isEqual = this.Equal(expected, actual);

                    Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);

                }
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }



            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization toomemory using reflection
                Sample.SerializeDeserializeObjectUsingReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION
    //
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-2-serialization-with-a-generic-record"></a><span data-ttu-id="5842c-198">Voorbeeld 2: Serialisatie met algemene record</span><span class="sxs-lookup"><span data-stu-id="5842c-198">Sample 2: Serialization with a generic record</span></span>
<span data-ttu-id="5842c-199">Een JSON-schema kan expliciet worden opgegeven in een algemene record wanneer reflectie kan niet worden gebruikt omdat het Hallo-gegevens via .NET-klassen met een gegevenscontract kan niet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5842c-199">A JSON schema can be explicitly specified in a generic record when reflection cannot be used because hello data cannot be represented via .NET classes with a data contract.</span></span> <span data-ttu-id="5842c-200">Deze methode is langzamer dan met behulp van reflectie.</span><span class="sxs-lookup"><span data-stu-id="5842c-200">This method is slower than using reflection.</span></span> <span data-ttu-id="5842c-201">In dergelijke gevallen kan Hallo-schema voor Hallo gegevens ook worden dynamisch is, dat wil zeggen, niet bekend bij het compileren.</span><span class="sxs-lookup"><span data-stu-id="5842c-201">In such cases, hello schema for hello data may also be dynamic, that is, not known at compile time.</span></span> <span data-ttu-id="5842c-202">Gegevens weergegeven als door komma's gescheiden waarden (CSV)-bestanden waarvan het schema onbekend is totdat deze is omgezet toohello Avro-indeling tijdens de uitvoering is een voorbeeld van dit soort dynamische scenario.</span><span class="sxs-lookup"><span data-stu-id="5842c-202">Data represented as comma-separated values (CSV) files whose schema is unknown until it is transformed toohello Avro format at run time is an example of this sort of dynamic scenario.</span></span>

<span data-ttu-id="5842c-203">Dit voorbeeld ziet u hoe toocreate en gebruik een [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly Geef een JSON-schema, hoe toopopulate met Hallo gegevens en vervolgens het tooserialize en te deserialiseren.</span><span class="sxs-lookup"><span data-stu-id="5842c-203">This example shows how toocreate and use an [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly specify a JSON schema, how toopopulate it with hello data, and then how tooserialize and deserialize it.</span></span> <span data-ttu-id="5842c-204">Hallo resultaat wordt vervolgens vergeleken toohello initiële exemplaar tooconfirm die record hersteld Hallo identieke toohello oorspronkelijke is.</span><span class="sxs-lookup"><span data-stu-id="5842c-204">hello result is then compared toohello initial instance tooconfirm that hello record recovered is identical toohello original.</span></span>

<span data-ttu-id="5842c-205">Hallo-schema in dit voorbeeld wordt uitgegaan van toobe gedeeld tussen hello en schrijfprogramma, dus containerindeling van Hallo Avro-object niet vereist is.</span><span class="sxs-lookup"><span data-stu-id="5842c-205">hello schema in this example is assumed toobe shared between hello readers and writers, so hello Avro object container format is not required.</span></span> <span data-ttu-id="5842c-206">Voor een voorbeeld van hoe tooserialize en deserialiseren van gegevens in geheugenbuffers met behulp van een algemene record met Hallo object containerindeling wanneer Hallo schema toegevoegd aan gegevens Hallo geserialiseerd worden moet, Zie Hallo <a href="#Scenario4">serialisatie met objectcontainer bestanden met algemene record</a> voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="5842c-206">For an example of how tooserialize and deserialize data into memory buffers by using a generic record with hello object container format when hello schema must be included with hello serialized data, see hello <a href="#Scenario4">Serialization using object container files with generic record</a> example.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Linq;
    using System.Runtime.Serialization;
    using Microsoft.Hadoop.Avro.Container;
    using Microsoft.Hadoop.Avro.Schema;
    using Microsoft.Hadoop.Avro;

    //This class contains all methods demonstrating
    //hello usage of Microsoft Avro Library
    public class AvroSample
    {

        //Serialize and deserialize sample data set by using a generic record.
        //A generic record is a special class with hello schema explicitly defined in JSON.
        //All serialized data should be mapped toohello fields of hello generic record,
        //which in turn is then serialized.
        public void SerializeDeserializeObjectUsingGenericRecords()
        {
            Console.WriteLine("SERIALIZATION USING GENERIC RECORD\n");
            Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

            //Define hello schema in JSON
            const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

            //Create a generic serializer based on hello schema
            var serializer = AvroSerializer.CreateGeneric(Schema);
            var rootSchema = serializer.WriterSchema as RecordSchema;

            //Create a memory stream buffer
            using (var stream = new MemoryStream())
            {
                //Create a generic record toorepresent hello data
                dynamic location = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location.Floor = 1;
                location.Room = 243;

                dynamic expected = new AvroRecord(serializer.WriterSchema);
                expected.Location = location;
                expected.Value = new byte[] { 1, 2, 3, 4, 5 };

                Console.WriteLine("Serializing Sample Data Set...");

                //Serialize hello data
                serializer.Serialize(stream, expected);

                stream.Seek(0, SeekOrigin.Begin);

                Console.WriteLine("Deserializing Sample Data Set...");

                //Deserialize hello data into a generic record
                dynamic actual = serializer.Deserialize(stream);

                Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                //Finally, verify hello results
                bool isEqual = expected.Location.Floor.Equals(actual.Location.Floor);
                isEqual = isEqual && expected.Location.Room.Equals(actual.Location.Room);
                isEqual = isEqual && ((byte[])expected.Value).SequenceEqual((byte[])actual.Value);
                Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);
            }
        }

        static void Main()
        {

            string sectionDivider = "---------------------------------------- ";

            //Create an instance of AvroSample class and invoke methods
            //illustrating different serializing approaches
            AvroSample Sample = new AvroSample();

            //Serialization toomemory using generic record
            Sample.SerializeDeserializeObjectUsingGenericRecords();

            Console.WriteLine(sectionDivider);
            Console.WriteLine("Press any key tooexit.");
            Console.Read();
        }
    }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-3-serialization-using-object-container-files-and-serialization-with-reflection"></a><span data-ttu-id="5842c-207">Voorbeeld 3: Serialisatie object containerbestanden en serialisatie gebruiken met reflectie</span><span class="sxs-lookup"><span data-stu-id="5842c-207">Sample 3: Serialization using object container files and serialization with reflection</span></span>
<span data-ttu-id="5842c-208">In dit voorbeeld is vergelijkbaar toohello scenario in Hallo <a href="#Scenario1"> eerste voorbeeld</a>, waarbij Hallo schema impliciet met reflectie is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="5842c-208">This example is similar toohello scenario in hello <a href="#Scenario1"> first example</a>, where hello schema is implicitly specified with reflection.</span></span> <span data-ttu-id="5842c-209">Hallo verschil is dat u hier Hallo-schema niet bekend toohello lezer die deze deserializes toobe wordt verondersteld.</span><span class="sxs-lookup"><span data-stu-id="5842c-209">hello difference is that here, hello schema is not assumed toobe known toohello reader that deserializes it.</span></span> <span data-ttu-id="5842c-210">Hallo **SensorData** objecten toobe geserialiseerd en hun impliciet opgegeven schema worden opgeslagen in een Avro-object container-bestand dat wordt vertegenwoordigd door Hallo [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) de klasse.</span><span class="sxs-lookup"><span data-stu-id="5842c-210">hello **SensorData** objects toobe serialized and their implicitly specified schema are stored in an Avro object container file represented by hello [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span>

<span data-ttu-id="5842c-211">Hallo-gegevens is geserialiseerd in dit voorbeeld met [ **SequentialWriter<SensorData>**  ](http://msdn.microsoft.com/library/dn627340.aspx) en gedeserialiseerd met [ **SequentialReader<SensorData>** ](http://msdn.microsoft.com/library/dn627340.aspx).</span><span class="sxs-lookup"><span data-stu-id="5842c-211">hello data is serialized in this example with [**SequentialWriter<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx) and deserialized with [**SequentialReader<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx).</span></span> <span data-ttu-id="5842c-212">Hallo resultaat wordt vergeleken toohello initiële exemplaren tooensure identiteit.</span><span class="sxs-lookup"><span data-stu-id="5842c-212">hello result then is compared toohello initial instances tooensure identity.</span></span>

<span data-ttu-id="5842c-213">Hallo in Hallo gegevensobject containerbestand is gecomprimeerd via Hallo standaard [ **Deflate** ] [ deflate-100] compressiecodec van .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="5842c-213">hello data in hello object container file is compressed via hello default [**Deflate**][deflate-100] compression codec from .NET Framework 4.</span></span> <span data-ttu-id="5842c-214">Zie Hallo <a href="#Scenario5"> vijfde voorbeeld</a> in dit onderwerp toolearn hoe toouse een meer recente en hogere versie van Hallo [ **Deflate** ] [ deflate-110] compressie de codec is beschikbaar in .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="5842c-214">See hello <a href="#Scenario5"> fifth example</a> in this topic toolearn how toouse a more recent and superior version of hello [**Deflate**][deflate-110] compression codec available in .NET Framework 4.5.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes hello sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello Deflate codec.
            public void SerializeDeserializeUsingObjectContainersReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is compressed using hello Deflate codec.
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true)))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            bool isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual);
                            count++;
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-4-serialization-using-object-container-files-and-serialization-with-generic-record"></a><span data-ttu-id="5842c-215">Voorbeeld 4: Serialisatie object containerbestanden en serialisatie gebruiken met algemene record</span><span class="sxs-lookup"><span data-stu-id="5842c-215">Sample 4: Serialization using object container files and serialization with generic record</span></span>
<span data-ttu-id="5842c-216">In dit voorbeeld is vergelijkbaar toohello scenario in Hallo <a href="#Scenario2"> tweede voorbeeld</a>, waarbij Hallo schema expliciet is opgegeven met JSON.</span><span class="sxs-lookup"><span data-stu-id="5842c-216">This example is similar toohello scenario in hello <a href="#Scenario2"> second example</a>, where hello schema is explicitly specified with JSON.</span></span> <span data-ttu-id="5842c-217">Hallo verschil is dat u hier Hallo-schema niet bekend toohello lezer die deze deserializes toobe wordt verondersteld.</span><span class="sxs-lookup"><span data-stu-id="5842c-217">hello difference is that here, hello schema is not assumed toobe known toohello reader that deserializes it.</span></span>

<span data-ttu-id="5842c-218">Hallo testset gegevens verzameld in een lijst met [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) objecten via een expliciet gedefinieerde JSON-schema en vervolgens wordt opgeslagen in een container-bestand van het object dat wordt vertegenwoordigd door Hallo [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) klasse.</span><span class="sxs-lookup"><span data-stu-id="5842c-218">hello test data set is collected into a list of [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) objects via an explicitly defined JSON schema and then stored in an object container file represented by hello [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span> <span data-ttu-id="5842c-219">Dit containerbestand maakt een writer is gebruikte tooserialize Hallo gegevens, decomprimeren tooa geheugenstroom die wordt vervolgens tooa bestand opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="5842c-219">This container file creates a writer that is used tooserialize hello data, uncompressed, tooa memory stream that is then saved tooa file.</span></span> <span data-ttu-id="5842c-220">Hallo [ **Codec.Null** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) parameter die wordt gebruikt voor het maken van de lezer Hallo geeft aan dat deze gegevens niet worden gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="5842c-220">hello [**Codec.Null**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) parameter used for creating hello reader specifies that this data is not compressed.</span></span>

<span data-ttu-id="5842c-221">Hallo-gegevens worden vervolgens lezen uit het Hallo-bestand en gedeserialiseerd tot een verzameling van objecten.</span><span class="sxs-lookup"><span data-stu-id="5842c-221">hello data is then read from hello file and deserialized into a collection of objects.</span></span> <span data-ttu-id="5842c-222">Deze verzameling is de initiële lijst vergeleken toohello van Avro records tooconfirm dat ze identiek zijn.</span><span class="sxs-lookup"><span data-stu-id="5842c-222">This collection is compared toohello initial list of Avro records tooconfirm that they are identical.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro.Schema;
        using Microsoft.Hadoop.Avro;

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes a sample data set by using a generic record and Avro object container files.
            //Serialized data is not compressed.
            public void SerializeDeserializeUsingObjectContainersGenericRecord()
            {
                Console.WriteLine("SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleGenericRecordNullCodec.avro";

                Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

                //Define hello schema in JSON
                const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

                //Create a generic serializer based on hello schema
                var serializer = AvroSerializer.CreateGeneric(Schema);
                var rootSchema = serializer.WriterSchema as RecordSchema;

                //Create a generic record toorepresent hello data
                var testData = new List<AvroRecord>();

                dynamic expected1 = new AvroRecord(rootSchema);
                dynamic location1 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location1.Floor = 1;
                location1.Room = 243;
                expected1.Location = location1;
                expected1.Value = new byte[] { 1, 2, 3, 4, 5 };
                testData.Add(expected1);

                dynamic expected2 = new AvroRecord(rootSchema);
                dynamic location2 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location2.Floor = 1;
                location2.Room = 244;
                expected2.Location = location2;
                expected2.Value = new byte[] { 6, 7, 8, 9 };
                testData.Add(expected2);

                //Serializing and saving data toofile.
                //Create a MemoryStream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is not compressed (Null compression codec).
                    using (var writer = AvroContainer.CreateGenericWriter(Schema, buffer, Codec.Null))
                    {
                        using (var streamWriter = new SequentialWriter<object>(writer, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(streamWriter.Write);
                        }
                    }

                    Console.WriteLine("Saving serialized data toofile...");

                    //Save stream toofile
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing hello data.
                //Create a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = AvroContainer.CreateGenericReader(buffer))
                    {
                        using (var streamReader = new SequentialReader<object>(reader))
                        {
                            var results = streamReader.Objects;

                            Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                            //Finally, verify hello results
                            var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = (dynamic)serialized, actual = (dynamic)deserialized });
                            int count = 1;
                            foreach (var pair in pairs)
                            {
                                bool isEqual = pair.expected.Location.Floor.Equals(pair.actual.Location.Floor);
                                isEqual = isEqual && pair.expected.Location.Room.Equals(pair.actual.Location.Room);
                                isEqual = isEqual && ((byte[])pair.expected.Value).SequenceEqual((byte[])pair.actual.Value);
                                Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                                count++;
                            }
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using hello given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of hello AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using generic record tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersGenericRecord();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.




## <a name="sample-5-serialization-using-object-container-files-with-a-custom-compression-codec"></a><span data-ttu-id="5842c-223">Voorbeeld 5: Serialisatie object container-bestanden gebruiken in een aangepaste compressiecodec</span><span class="sxs-lookup"><span data-stu-id="5842c-223">Sample 5: Serialization using object container files with a custom compression codec</span></span>
<span data-ttu-id="5842c-224">Hallo vijfde voorbeeld ziet u hoe een aangepaste compressiecodec voor Avro toouse containerbestanden object.</span><span class="sxs-lookup"><span data-stu-id="5842c-224">hello fifth example shows how toouse a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="5842c-225">Een voorbeeld van een met Hallo-code voor dit voorbeeld kan worden gedownload vanaf Hallo [Azure codevoorbeelden](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) site.</span><span class="sxs-lookup"><span data-stu-id="5842c-225">A sample containing hello code for this example can be downloaded from hello [Azure code samples](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) site.</span></span>

<span data-ttu-id="5842c-226">Hallo [Avro-specificatie](http://avro.apache.org/docs/current/spec.html#Required+Codecs) kunt u informatie over het gebruik van een optionele compressiecodec (bovendien te**Null** en **Deflate** standaardwaarden).</span><span class="sxs-lookup"><span data-stu-id="5842c-226">hello [Avro Specification](http://avro.apache.org/docs/current/spec.html#Required+Codecs) allows usage of an optional compression codec (in addition too**Null** and **Deflate** defaults).</span></span> <span data-ttu-id="5842c-227">In dit voorbeeld wordt een nieuwe codec zoals Snappy niet implementeren (vermeld als een ondersteunde optionele codec in Hallo [Avro-specificatie](http://avro.apache.org/docs/current/spec.html#snappy)).</span><span class="sxs-lookup"><span data-stu-id="5842c-227">This example is not implementing a new codec such as Snappy (mentioned as a supported optional codec in hello [Avro Specification](http://avro.apache.org/docs/current/spec.html#snappy)).</span></span> <span data-ttu-id="5842c-228">Er wordt weergegeven hoe toouse .NET Framework 4.5-implementatie van Hallo Hallo [ **Deflate** ] [ deflate-110] codec een betere compressiealgoritme op basis van Hallo biedt[zlib](http://zlib.net/) compressiebibliotheek dan Hallo standaard .NET Framework 4-versie.</span><span class="sxs-lookup"><span data-stu-id="5842c-228">It shows how toouse hello .NET Framework 4.5 implementation of hello [**Deflate**][deflate-110] codec, which provides a better compression algorithm based on hello [zlib](http://zlib.net/) compression library than hello default .NET Framework 4 version.</span></span>

    //
    // This code needs toobe compiled with hello parameter Target Framework set as ".NET Framework 4.5"
    // tooensure hello desired implementation of hello Deflate compression algorithm is used.
    // Ensure your C# project is set up accordingly.
    //

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.IO;
        using System.IO.Compression;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        #region Defining objects for serialization
        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }
        #endregion

        #region Defining custom codec based on .NET Framework V.4.5 Deflate
        //Avro.NET codec class contains two methods,
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed),
        //which are hello key ones for data compression.
        //tooenable a custom codec, one needs tooimplement these methods for hello required codec.

        #region Defining Compression and Decompression Streams
        //DeflateStream (class from System.IO.Compression namespace that implements Deflate algorithm)
        //cannot be directly used for Avro because it does not support vital operations like Seek.
        //Thus one needs tooimplement two classes inherited from stream
        //(one for compressed and one for decompressed stream)
        //that use Deflate compression and implement all required features.
        internal sealed class CompressionStreamDeflate45 : Stream
        {
            private readonly Stream buffer;
            private DeflateStream compressionStream;

            public CompressionStreamDeflate45(Stream buffer)
            {
                Debug.Assert(buffer != null, "Buffer is not allowed toobe null.");

                this.compressionStream = new DeflateStream(buffer, CompressionLevel.Fastest, true);
                this.buffer = buffer;
            }

            public override bool CanRead
            {
                get { return this.buffer.CanRead; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return this.buffer.CanWrite; }
            }

            public override void Flush()
            {
                this.compressionStream.Close();
            }

            public override long Length
            {
                get { return this.buffer.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.buffer.Position;
                }

                set
                {
                    this.buffer.Position = value;
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.buffer.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                return this.buffer.Seek(offset, origin);
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                this.compressionStream.Write(buffer, offset, count);
            }

            protected override void Dispose(bool disposed)
            {
                base.Dispose(disposed);

                if (disposed)
                {
                    this.compressionStream.Dispose();
                    this.compressionStream = null;
                }
            }
        }

        internal sealed class DecompressionStreamDeflate45 : Stream
        {
            private readonly DeflateStream decompressed;

            public DecompressionStreamDeflate45(Stream compressed)
            {
                this.decompressed = new DeflateStream(compressed, CompressionMode.Decompress, true);
            }

            public override bool CanRead
            {
                get { return true; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return false; }
            }

            public override void Flush()
            {
                this.decompressed.Close();
            }

            public override long Length
            {
                get { return this.decompressed.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.decompressed.Position;
                }

                set
                {
                    throw new NotSupportedException();
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.decompressed.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                throw new NotSupportedException();
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                throw new NotSupportedException();
            }

            protected override void Dispose(bool disposing)
            {
                base.Dispose(disposing);

                if (disposing)
                {
                    this.decompressed.Dispose();
                }
            }
        }
        #endregion

        #region Define Codec
        //Define hello actual codec class containing hello required methods for manipulating streams:
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed).
        //Codec class uses classes for compressed and decompressed streams defined above.
        internal sealed class DeflateCodec45 : Codec
        {

            //We merely use different IMPLEMENTATIONS of Deflate, so CodecName remains "deflate"
            public static readonly string CodecName = "deflate";

            public DeflateCodec45()
                : base(CodecName)
            {
            }

            public override Stream GetCompressedStreamOver(Stream decompressed)
            {
                if (decompressed == null)
                {
                    throw new ArgumentNullException("decompressed");
                }

                return new CompressionStreamDeflate45(decompressed);
            }

            public override Stream GetDecompressedStreamOver(Stream compressed)
            {
                if (compressed == null)
                {
                    throw new ArgumentNullException("compressed");
                }

                return new DecompressionStreamDeflate45(compressed);
            }
        }
        #endregion

        #region Define modified Codec Factory
        //Define modified codec factory toobe used in hello reader.
        //It catches hello attempt toouse "Deflate" and provide  a custom codec.
        //For all other cases, it relies on hello base class (CodecFactory).
        internal sealed class CodecFactoryDeflate45 : CodecFactory
        {

            public override Codec Create(string codecName)
            {
                if (codecName == DeflateCodec45.CodecName)
                    return new DeflateCodec45();
                else
                    return base.Create(codecName);
            }
        }
        #endregion

        #endregion

        #region Sample Class with demonstration methods
        //This class contains methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello custom compression codec (Deflate of .NET Framework 4.5).
            //
            //This sample uses memory stream for all operations related tooserialization, deserialization and
            //object container manipulation, though file stream could be easily used.
            public void SerializeDeserializeUsingObjectContainersReflectionCustomCodec()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate45.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Here hello custom codec is introduced. For convenience, hello next commented code line shows how toouse built-in Deflate.
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, new DeflateCodec45()))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Because of SequentialReader<T> constructor signature, an AvroSerializerSettings instance is required
                    //when codec factory is explicitly specified.
                    //You may comment hello line below if you want toouse built-in Deflate (see next comment).
                    AvroSerializerSettings settings = new AvroSerializerSettings();

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    //Here hello custom codec factory is introduced.
                    //For convenience, hello next commented code line shows how toouse built-in Deflate
                    //(no explicit Codec Factory parameter is required in this case).
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var reader = new SequentialReader<SensorData>(AvroContainer.CreateReader<SensorData>(buffer, true)))
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true, settings, new CodecFactoryDeflate45())))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        bool isEqual;
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                            count++;
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }
        #endregion

            #region Helper Methods

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }
            #endregion

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection tooAvro object container file using custom codec
                Sample.SerializeDeserializeUsingObjectContainersReflectionCustomCodec();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    //For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.

## <a name="sample-6-using-avro-tooupload-data-for-hello-microsoft-azure-hdinsight-service"></a><span data-ttu-id="5842c-229">Voorbeeld 6: Met behulp van Avro tooupload gegevens voor Hallo Microsoft Azure HDInsight-service</span><span class="sxs-lookup"><span data-stu-id="5842c-229">Sample 6: Using Avro tooupload data for hello Microsoft Azure HDInsight service</span></span>
<span data-ttu-id="5842c-230">Hallo zesde voorbeeld ziet u enkele programming technieken gerelateerde toointeracting met hello Azure HDInsight-service.</span><span class="sxs-lookup"><span data-stu-id="5842c-230">hello sixth example illustrates some programming techniques related toointeracting with hello Azure HDInsight service.</span></span> <span data-ttu-id="5842c-231">Een voorbeeld van een met Hallo-code voor dit voorbeeld kan worden gedownload vanaf Hallo [Azure codevoorbeelden](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) site.</span><span class="sxs-lookup"><span data-stu-id="5842c-231">A sample containing hello code for this example can be downloaded from hello [Azure code samples](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) site.</span></span>

<span data-ttu-id="5842c-232">Hallo voorbeeld Hallo volgende taken:</span><span class="sxs-lookup"><span data-stu-id="5842c-232">hello sample does hello following tasks:</span></span>

* <span data-ttu-id="5842c-233">Maakt verbinding tooan bestaand HDInsight-service-cluster.</span><span class="sxs-lookup"><span data-stu-id="5842c-233">Connects tooan existing HDInsight service cluster.</span></span>
* <span data-ttu-id="5842c-234">Meerdere CSV-bestanden serialiseert en uploadt Hallo resultaat tooAzure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="5842c-234">Serializes several CSV files and uploads hello result tooAzure Blob storage.</span></span> <span data-ttu-id="5842c-235">(Hallo CSV-bestanden samen met de Hallo voorbeeld zijn gedistribueerd en vertegenwoordigen een uitpakken uit bijlage aandelen historische gegevens worden verspreid door [Infochimps](http://www.infochimps.com/) Hallo gedurende 1970 2010.</span><span class="sxs-lookup"><span data-stu-id="5842c-235">(hello CSV files are distributed together with hello sample and represent an extract from AMEX Stock historical data distributed by [Infochimps](http://www.infochimps.com/) for hello period 1970-2010.</span></span> <span data-ttu-id="5842c-236">Hallo voorbeeld leest gegevens uit een CSV-bestand, converteert Hallo records tooinstances Hallo **Stock** klasse en serialiseert u ze via reflectie.</span><span class="sxs-lookup"><span data-stu-id="5842c-236">hello sample reads CSV file data, converts hello records tooinstances of hello **Stock** class, and then serializes them by using reflection.</span></span> <span data-ttu-id="5842c-237">Voorraad typedefinitie wordt gemaakt van een JSON-schema via Hallo Microsoft Avro Library code generatie hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="5842c-237">Stock type definition is created from a JSON schema via hello Microsoft Avro Library code generation utility.</span></span>
* <span data-ttu-id="5842c-238">Maakt een nieuwe externe tabel aangeroepen **voorraden** in Hive, en koppelt u deze toohello gegevens geüpload in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="5842c-238">Creates a new external table called **Stocks** in Hive, and links it toohello data uploaded in hello previous step.</span></span>
* <span data-ttu-id="5842c-239">Een query uitvoert met behulp van Hive via Hallo **voorraden** tabel.</span><span class="sxs-lookup"><span data-stu-id="5842c-239">Executes a query by using Hive over hello **Stocks** table.</span></span>

<span data-ttu-id="5842c-240">Hallo voorbeeld voert bovendien een procedure opschonen voor en na het uitvoeren van belangrijke bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="5842c-240">In addition, hello sample performs a clean-up procedure before and after performing major operations.</span></span> <span data-ttu-id="5842c-241">Tijdens het Hallo opschonen, alle Hallo betrekking Azure Blob-gegevens en mappen worden verwijderd en Hallo Hive-tabel is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="5842c-241">During hello clean-up, all of hello related Azure Blob data and folders are removed, and hello Hive table is dropped.</span></span> <span data-ttu-id="5842c-242">U kunt ook Hallo opschonen procedure vanaf Hallo voorbeeldopdrachtregel aanroepen.</span><span class="sxs-lookup"><span data-stu-id="5842c-242">You can also invoke hello clean-up procedure from hello sample command line.</span></span>

<span data-ttu-id="5842c-243">Hallo voorbeeld heeft Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="5842c-243">hello sample has hello following prerequisites:</span></span>

* <span data-ttu-id="5842c-244">Een actief Microsoft Azure-abonnement en de abonnement-ID.</span><span class="sxs-lookup"><span data-stu-id="5842c-244">An active Microsoft Azure subscription and its subscription ID.</span></span>
* <span data-ttu-id="5842c-245">Een beheercertificaat voor Hallo-abonnement met de bijbehorende persoonlijke sleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="5842c-245">A management certificate for hello subscription with hello corresponding private key.</span></span> <span data-ttu-id="5842c-246">Hallo-certificaat moet worden geïnstalleerd in Hallo huidige gebruiker persoonlijke opslag op Hallo gebruikt machine toorun Hallo voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="5842c-246">hello certificate should be installed in hello current user private storage on hello machine used toorun hello sample.</span></span>
* <span data-ttu-id="5842c-247">Een actief HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="5842c-247">An active HDInsight cluster.</span></span>
* <span data-ttu-id="5842c-248">Een Azure Storage-account gekoppeld toohello HDInsight-cluster van de vorige vereiste Hallo samen met de Hallo bijbehorende primaire of secundaire toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="5842c-248">An Azure Storage account linked toohello HDInsight cluster from hello previous prerequisite, together with hello corresponding primary, or secondary access key.</span></span>

<span data-ttu-id="5842c-249">Alle informatie Hallo van Hallo vereisten moet worden ingevoerd toohello voorbeeldconfiguratiebestand voordat Hallo voorbeeld wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5842c-249">All of hello information from hello prerequisites should be entered toohello sample configuration file before hello sample is run.</span></span> <span data-ttu-id="5842c-250">Er zijn twee manieren toodo het:</span><span class="sxs-lookup"><span data-stu-id="5842c-250">There are two possible ways toodo it:</span></span>

* <span data-ttu-id="5842c-251">Hallo app.config-bestand in de hoofdmap Hallo-voorbeeld bewerken en vervolgens Hallo-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="5842c-251">Edit hello app.config file in hello sample root directory and then build hello sample</span></span>
* <span data-ttu-id="5842c-252">Hallo voorbeeld eerst te bouwen en bewerk vervolgens AvroHDISample.exe.config in Hallo build directory</span><span class="sxs-lookup"><span data-stu-id="5842c-252">First build hello sample, and then edit AvroHDISample.exe.config in hello build directory</span></span>

<span data-ttu-id="5842c-253">In beide gevallen moeten alle bewerkingen worden uitgevoerd in Hallo  **<appSettings>**  gedeelte instellingen.</span><span class="sxs-lookup"><span data-stu-id="5842c-253">In both cases, all edits should be done in hello **<appSettings>** settings section.</span></span> <span data-ttu-id="5842c-254">Ga als volgt Hallo opmerkingen in Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="5842c-254">Follow hello comments in hello file.</span></span>
<span data-ttu-id="5842c-255">Hallo wordt voorbeeld uitgevoerd vanaf de opdrachtregel Hallo door het uitvoeren van de volgende opdracht (waarbij hello ZIP-bestand met Hallo voorbeeld wordt uitgegaan van een toobe uitgepakt tooC:\AvroHDISample; als anders gebruik Hallo relevante bestandspad) Hallo:</span><span class="sxs-lookup"><span data-stu-id="5842c-255">hello sample is run from hello command line by executing hello following command (where hello .zip file with hello sample was assumed toobe extracted tooC:\AvroHDISample; if otherwise, use hello relevant file path):</span></span>

    AvroHDISample run C:\AvroHDISample\Data

<span data-ttu-id="5842c-256">tooclean Hallo-cluster, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5842c-256">tooclean up hello cluster, run hello following command:</span></span>

    AvroHDISample clean

[deflate-100]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.100).aspx
[deflate-110]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.110).aspx
