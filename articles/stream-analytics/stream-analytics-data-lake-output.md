---
title: aaaStream Analytics Data Lake Store uitvoer | Microsoft Docs
description: Configuratie van verificatie en autorisatie van een Azure Data Lake Store in een Stream Analytics-taak
keywords: 
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ea5baafa-0054-4c70-973a-6a3a8c6eaffc
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 183cf51edb2e49ac3e42257e67a8077b95777258
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-data-lake-store-output"></a><span data-ttu-id="ca542-103">Stream Analytics Data Lake Store-uitvoer</span><span class="sxs-lookup"><span data-stu-id="ca542-103">Stream Analytics Data Lake Store output</span></span>
<span data-ttu-id="ca542-104">Stream Analytics-taken ondersteunen verschillende uitvoermethoden, een wordt een [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span><span class="sxs-lookup"><span data-stu-id="ca542-104">Stream Analytics jobs support several output methods, one being an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span></span> <span data-ttu-id="ca542-105">Azure Data Lake Store is een ondernemingsbrede opslagplaats op hyperschaal voor analytische workloads van big data.</span><span class="sxs-lookup"><span data-stu-id="ca542-105">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="ca542-106">Data Lake Store kunt u toostore gegevens van elke grootte, type en opnamesnelheid snelheid voor operationele en experimentele analyses.</span><span class="sxs-lookup"><span data-stu-id="ca542-106">Data Lake Store enables you toostore data of any size, type and ingestion speed for operational and exploratory analytics.</span></span>

## <a name="authorize-a-data-lake-store-account"></a><span data-ttu-id="ca542-107">Een Data Lake Store-account toestaan</span><span class="sxs-lookup"><span data-stu-id="ca542-107">Authorize a Data Lake Store account</span></span>
1. <span data-ttu-id="ca542-108">Wanneer Data Lake Store als uitvoer in hello Azure-portal is geselecteerd, wordt u gevraagd tooauthorize gebruik van uw bestaande Data Lake Store of toorequest access toohello Data Lake Store via Hallo klassieke Portal.</span><span class="sxs-lookup"><span data-stu-id="ca542-108">When Data Lake Store is selected as an output in hello Azure portal, you will be prompted tooauthorize use of your existing Data Lake Store or toorequest access toohello Data Lake Store via hello Classic Portal.</span></span>
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. <span data-ttu-id="ca542-109">Als u al hebt tooData Lake Store, klik op 'Nu autoriseren' en gedurende een korte periode een pagina wordt weergegeven dat aangeeft 'Omleidt tooauthorization'.</span><span class="sxs-lookup"><span data-stu-id="ca542-109">If you already have access tooData Lake Store, click “Authorize Now” and for a brief time a page will pop up indicating “Redirecting tooauthorization”.</span></span> <span data-ttu-id="ca542-110">Hallo pagina automatisch wordt gesloten en u krijgt Hallo pagina waarmee u tooconfigure Hallo Data Lake Store-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="ca542-110">hello page will automatically close and you will be presented with hello page that would allow you tooconfigure hello Data Lake Store output.</span></span>

<span data-ttu-id="ca542-111">Als u niet hebt aangemeld voor Data Lake Store, kunt u volgen Hallo 'Nu aanmelden' koppeling tooinitiate Hallo aanvraag of volg Hallo [gestart instructies](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ca542-111">If you have not signed up for Data Lake Store, you can follow hello “Sign up now” link tooinitiate hello request, or follow hello [get started instructions](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="configure-hello-data-lake-store-output-properties"></a><span data-ttu-id="ca542-112">Hallo Data Lake Store uitvoereigenschappen configureren</span><span class="sxs-lookup"><span data-stu-id="ca542-112">Configure hello Data Lake Store output properties</span></span>
<span data-ttu-id="ca542-113">Zodra u Hallo geverifieerde Data Lake Store-account hebt, kunt u Hallo eigenschappen configureren voor de uitvoer van uw Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ca542-113">Once you have hello Data Lake Store account authenticated, you can configure hello properties for your Data Lake Store output.</span></span> <span data-ttu-id="ca542-114">Hallo onderstaande tabel is Hallo lijst met namen van eigenschappen en hun beschrijving tooconfigure uitvoer van uw Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ca542-114">hello table below is hello list of property names and their description tooconfigure your Data Lake Store output.</span></span>

<table>
<tbody>
<tr>
<td><span data-ttu-id="ca542-115"><B>DE NAAM VAN EIGENSCHAP</B></span><span class="sxs-lookup"><span data-stu-id="ca542-115"><B>PROPERTY NAME</B></span></span></td>
<td><span data-ttu-id="ca542-116"><B>BESCHRIJVING</B></span><span class="sxs-lookup"><span data-stu-id="ca542-116"><B>DESCRIPTION</B></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ca542-117">Uitvoeraliassen</span><span class="sxs-lookup"><span data-stu-id="ca542-117">Output Alias</span></span></td>
<td><span data-ttu-id="ca542-118">Dit is een beschrijvende naam die is gebruikt in query's toodirect Hallo query uitvoer toothis Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ca542-118">This is a friendly name used in queries toodirect hello query output toothis Data Lake Store.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ca542-119">Data Lake Store-Account</span><span class="sxs-lookup"><span data-stu-id="ca542-119">Data Lake Store Account</span></span></td>
<td><span data-ttu-id="ca542-120">Hallo-naam van Hallo storage-account waarin u de uitvoer wilt verzenden.</span><span class="sxs-lookup"><span data-stu-id="ca542-120">hello name of hello storage account where you are sending your output.</span></span> <span data-ttu-id="ca542-121">Er verschijnt een lijst met Hallo aangemelde gebruiker toegang tot de heeft Data Lake Store-accounts.</span><span class="sxs-lookup"><span data-stu-id="ca542-121">You will be presented with a list of Data Lake Store accounts  hello logged in user has access to.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ca542-122">Pad voorvoegsel patroon [<I>optionele</I>]</span><span class="sxs-lookup"><span data-stu-id="ca542-122">Path Prefix Pattern [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="ca542-123">Hallo bestand pad gebruikt toowrite uw bestanden binnen Hallo Data Lake Store-Account opgegeven.</span><span class="sxs-lookup"><span data-stu-id="ca542-123">hello file path used toowrite your files within hello specified Data Lake Store Account.</span></span> <BR><span data-ttu-id="ca542-124">{date} {time}</span><span class="sxs-lookup"><span data-stu-id="ca542-124">{date}, {time}</span></span><BR><span data-ttu-id="ca542-125">Voorbeeld 1: Map1/logs / {date} / {time}</span><span class="sxs-lookup"><span data-stu-id="ca542-125">Example 1: folder1/logs/{date}/{time}</span></span><BR><span data-ttu-id="ca542-126">Voorbeeld 2: Map1/logs / {date}</span><span class="sxs-lookup"><span data-stu-id="ca542-126">Example 2: folder1/logs/{date}</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ca542-127">Datum notatie [<I>optionele</I>]</span><span class="sxs-lookup"><span data-stu-id="ca542-127">Date Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="ca542-128">Als Hallo datum token in Hallo voorvoegsel pad wordt gebruikt, kunt u Hallo datumnotatie waarin de bestanden zijn ingedeeld.</span><span class="sxs-lookup"><span data-stu-id="ca542-128">If hello date token is used in hello prefix path, you can select hello date format in which your files are organized.</span></span> <span data-ttu-id="ca542-129">Voorbeeld: Jjjj/MM/DD</span><span class="sxs-lookup"><span data-stu-id="ca542-129">Example: YYYY/MM/DD</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ca542-130">Tijdnotatie [<I>optionele</I>]</span><span class="sxs-lookup"><span data-stu-id="ca542-130">Time Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="ca542-131">Als Hallo tijd token in Hallo voorvoegsel pad wordt gebruikt, geeft u de tijdnotatie Hallo waarin de bestanden zijn ingedeeld.</span><span class="sxs-lookup"><span data-stu-id="ca542-131">If hello time token is used in hello prefix path, specify hello time format in which your files are organized.</span></span> <span data-ttu-id="ca542-132">Hallo alleen ondersteunde waarde is momenteel HH.</span><span class="sxs-lookup"><span data-stu-id="ca542-132">Currently hello only supported value is HH.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ca542-133">Gebeurtenis serialisatie-indeling</span><span class="sxs-lookup"><span data-stu-id="ca542-133">Event Serialization Format</span></span></td>
<td><span data-ttu-id="ca542-134">Serialisatie-indeling voor uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="ca542-134">Serialization format for output data.</span></span> <span data-ttu-id="ca542-135">JSON, CSV en Avro worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="ca542-135">JSON, CSV, and Avro are supported.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ca542-136">Encoding</span><span class="sxs-lookup"><span data-stu-id="ca542-136">Encoding</span></span></td>
<td><span data-ttu-id="ca542-137">Als CSV- of JSON-indeling, moet een codering worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="ca542-137">If CSV or JSON format, an encoding must be specified.</span></span> <span data-ttu-id="ca542-138">UTF-8 wordt de coderingsindeling Hallo alleen ondersteund op dit moment.</span><span class="sxs-lookup"><span data-stu-id="ca542-138">UTF-8 is hello only supported encoding format at this time.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ca542-139">Scheidingsteken</span><span class="sxs-lookup"><span data-stu-id="ca542-139">Delimiter</span></span></td>
<td><span data-ttu-id="ca542-140">Alleen van toepassing voor CSV-serialisatie.</span><span class="sxs-lookup"><span data-stu-id="ca542-140">Only applicable for CSV serialization.</span></span> <span data-ttu-id="ca542-141">Stream Analytics ondersteunt een aantal algemene scheidingstekens voor het serialiseren van CSV-gegevens.</span><span class="sxs-lookup"><span data-stu-id="ca542-141">Stream Analytics supports a number of common delimiters for serializing CSV data.</span></span> <span data-ttu-id="ca542-142">Ondersteunde waarden zijn komma, puntkomma, spatie, tab en de verticale balk.</span><span class="sxs-lookup"><span data-stu-id="ca542-142">Supported values are comma, semicolon, space, tab and vertical bar.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ca542-143">Indeling</span><span class="sxs-lookup"><span data-stu-id="ca542-143">Format</span></span></td>
<td><span data-ttu-id="ca542-144">Alleen van toepassing op JSON-serialisatie.</span><span class="sxs-lookup"><span data-stu-id="ca542-144">Only applicable for JSON serialization.</span></span> <span data-ttu-id="ca542-145">Lijn gescheiden geeft aan dat Hallo uitvoer wordt ingedeeld door elk JSON-object dat is gescheiden door een nieuwe regel.</span><span class="sxs-lookup"><span data-stu-id="ca542-145">Line separated specifies that hello output will be formatted by having each JSON object separated by a new line.</span></span> <span data-ttu-id="ca542-146">Matrix geeft aan dat Hallo uitvoer wordt ingedeeld als een matrix met JSON-objecten.</span><span class="sxs-lookup"><span data-stu-id="ca542-146">Array specifies that hello output will be formatted as an array of JSON objects.</span></span></td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a><span data-ttu-id="ca542-147">Vernieuwen van Data Lake Store-autorisatie</span><span class="sxs-lookup"><span data-stu-id="ca542-147">Renew Data Lake Store Authorization</span></span>
<span data-ttu-id="ca542-148">Er is momenteel een beperking waarin Hallo-verificatietoken toobe handmatig moeten worden vernieuwd om de 90 dagen voor alle taken met Data Lake Store-uitvoer moet.</span><span class="sxs-lookup"><span data-stu-id="ca542-148">Currently, there is a limitation where hello authentication token needs toobe manually refreshed every 90 days for all jobs with Data Lake Store output.</span></span> <span data-ttu-id="ca542-149">U moet ook toore-verificatie van uw Data Lake Store-account als u uw wachtwoord is gewijzigd sinds de taak is gemaakt of laatst geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="ca542-149">You will also need toore-authenticate your Data Lake Store account if you have changed your password since your job was created or last authenticated.</span></span> <span data-ttu-id="ca542-150">Een symptoom zijn van dit probleem is geen taakuitvoer en een fout in Hallo Bewerkingslogboeken nodig voor nieuwe autorisatie waarmee wordt aangegeven.</span><span class="sxs-lookup"><span data-stu-id="ca542-150">A symptom of this issue is no job output and an error in hello Operation Logs indicating need for re-authorization.</span></span>

<span data-ttu-id="ca542-151">tooresolve dit probleem op door de actieve taak stoppen en ga tooyour Data Lake Store-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="ca542-151">tooresolve this issue, stop your running job and go tooyour Data Lake Store output.</span></span> <span data-ttu-id="ca542-152">Klik op de koppeling 'Vernieuwen autorisatie' hello en gedurende een korte periode een pagina wordt weergegeven dat aangeeft 'Omleidt tooauthorization..'.</span><span class="sxs-lookup"><span data-stu-id="ca542-152">Click hello “Renew authorization” link, and for a brief time a page will pop up indicating “Redirecting tooauthorization..”.</span></span> <span data-ttu-id="ca542-153">Hallo-pagina wordt automatisch gesloten en als dit lukt, wordt aangegeven 'Autorisatie is vernieuwd'.</span><span class="sxs-lookup"><span data-stu-id="ca542-153">hello page will automatically close and if successful, will indicate “Authorization has been successfully renewed”.</span></span> <span data-ttu-id="ca542-154">U moet tooclick 'Opgeslagen' Hallo Hallo pagina onderaan in, en kan worden voortgezet door de taak in de laatste tijd geëindigd tooavoid gegevensverlies Hallo opnieuw te starten.</span><span class="sxs-lookup"><span data-stu-id="ca542-154">You then need tooclick “Save” at hello bottom of hello page, and can proceed by restarting your job from hello Last Stopped Time tooavoid data loss.</span></span>

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

