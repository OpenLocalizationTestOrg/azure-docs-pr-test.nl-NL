---
title: 'Azure AD Connect-synchronisatie: functieverwijzing | Microsoft Docs'
description: Verwijzing van expressies declaratieve inrichting in Azure AD Connect-synchronisatie.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 4f525ca0-be0e-4a2e-8da1-09b6b567ed5f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: fbe0df856ca2efda965650fb85c7e831a0be32c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a><span data-ttu-id="b316a-103">Azure AD Connect-synchronisatie: functieverwijzing</span><span class="sxs-lookup"><span data-stu-id="b316a-103">Azure AD Connect sync: Functions Reference</span></span>
<span data-ttu-id="b316a-104">In Azure AD Connect zijn functies gebruikte toomanipulate een kenmerkwaarde tijdens de synchronisatie.</span><span class="sxs-lookup"><span data-stu-id="b316a-104">In Azure AD Connect, functions are used toomanipulate an attribute value during synchronization.</span></span>  
<span data-ttu-id="b316a-105">Hallo syntaxis van Hallo functies wordt uitgedrukt met Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="b316a-105">hello Syntax of hello functions is expressed using hello following format:</span></span>  
`<output type> FunctionName(<input type> <position name>, ..)`

<span data-ttu-id="b316a-106">Als een functie is overbelast en meerdere syntaxes accepteert, worden alle geldige syntaxis vermeld.</span><span class="sxs-lookup"><span data-stu-id="b316a-106">If a function is overloaded and accepts multiple syntaxes, all valid syntaxes are listed.</span></span>  
<span data-ttu-id="b316a-107">Hallo-functies zijn sterk getypeerd en ze controleren dat het Hallo-type komt overeen met Hallo beschreven type doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="b316a-107">hello functions are strongly typed and they verify that hello type passed in matches hello documented type.</span></span>  
<span data-ttu-id="b316a-108">Als het Hallo-type komt niet overeen, wordt een fout gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-108">If hello type does not match, an error is thrown.</span></span>

<span data-ttu-id="b316a-109">Hallo-typen worden uitgedrukt Hello de volgende syntaxis:</span><span class="sxs-lookup"><span data-stu-id="b316a-109">hello types are expressed with hello following syntax:</span></span>

* <span data-ttu-id="b316a-110">**opslaglocatie** – binaire</span><span class="sxs-lookup"><span data-stu-id="b316a-110">**bin** – Binary</span></span>
* <span data-ttu-id="b316a-111">**BOOL** – Booleaanse</span><span class="sxs-lookup"><span data-stu-id="b316a-111">**bool** – Boolean</span></span>
* <span data-ttu-id="b316a-112">**DT** – UTC-datum/tijd</span><span class="sxs-lookup"><span data-stu-id="b316a-112">**dt** – UTC Date/Time</span></span>
* <span data-ttu-id="b316a-113">**Enum** – opsomming van de bekende constanten</span><span class="sxs-lookup"><span data-stu-id="b316a-113">**enum** – Enumeration of known constants</span></span>
* <span data-ttu-id="b316a-114">**EXP** – expressie verwacht tooevaluate tooa Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="b316a-114">**exp** – Expression, which is expected tooevaluate tooa Boolean</span></span>
* <span data-ttu-id="b316a-115">**mvbin** – meerwaardige binaire</span><span class="sxs-lookup"><span data-stu-id="b316a-115">**mvbin** – Multi-Valued Binary</span></span>
* <span data-ttu-id="b316a-116">**mvstr** – meerwaardige tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b316a-116">**mvstr** – Multi-Valued String</span></span>
* <span data-ttu-id="b316a-117">**mvref** – meerwaardige verwijzing</span><span class="sxs-lookup"><span data-stu-id="b316a-117">**mvref** – Multi-Valued Reference</span></span>
* <span data-ttu-id="b316a-118">**NUM** – numerieke</span><span class="sxs-lookup"><span data-stu-id="b316a-118">**num** – Numeric</span></span>
* <span data-ttu-id="b316a-119">**REF** : verwijzing</span><span class="sxs-lookup"><span data-stu-id="b316a-119">**ref** – Reference</span></span>
* <span data-ttu-id="b316a-120">**Str** – tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b316a-120">**str** – String</span></span>
* <span data-ttu-id="b316a-121">**VAR** : een variant van (bijna) alle andere type</span><span class="sxs-lookup"><span data-stu-id="b316a-121">**var** – A variant of (almost) any other type</span></span>
* <span data-ttu-id="b316a-122">**VOID** – geen waarde als resultaat</span><span class="sxs-lookup"><span data-stu-id="b316a-122">**void** – doesn’t return a value</span></span>

<span data-ttu-id="b316a-123">functies met typen Hallo Hallo **mvbin**, **mvstr**, en **mvref** kunt werken alleen op kenmerken met meerdere waarden.</span><span class="sxs-lookup"><span data-stu-id="b316a-123">hello functions with hello types **mvbin**, **mvstr**, and **mvref** can only work on multi-valued attributes.</span></span> <span data-ttu-id="b316a-124">Functies met **bin**, **str**, en **ref** werk op de kenmerken van zowel één waarde en meerdere waarden.</span><span class="sxs-lookup"><span data-stu-id="b316a-124">Functions with **bin**, **str**, and **ref** work on both single-valued and multi-valued attributes.</span></span>

## <a name="functions-reference"></a><span data-ttu-id="b316a-125">Functieverwijzing</span><span class="sxs-lookup"><span data-stu-id="b316a-125">Functions Reference</span></span>
| <span data-ttu-id="b316a-126">Lijst met functies</span><span class="sxs-lookup"><span data-stu-id="b316a-126">List of functions</span></span> |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="b316a-127">**Certificaat**</span><span class="sxs-lookup"><span data-stu-id="b316a-127">**Certificate**</span></span> | | | | |
| [<span data-ttu-id="b316a-128">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="b316a-128">CertExtensionOids</span></span>](#certextensionoids) |[<span data-ttu-id="b316a-129">CertFormat</span><span class="sxs-lookup"><span data-stu-id="b316a-129">CertFormat</span></span>](#certformat) |[<span data-ttu-id="b316a-130">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="b316a-130">CertFriendlyName</span></span>](#certfriendlyname) |[<span data-ttu-id="b316a-131">CertHashString</span><span class="sxs-lookup"><span data-stu-id="b316a-131">CertHashString</span></span>](#certhashstring) | |
| [<span data-ttu-id="b316a-132">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="b316a-132">CertIssuer</span></span>](#certissuer) |[<span data-ttu-id="b316a-133">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="b316a-133">CertIssuerDN</span></span>](#certissuerdn) |[<span data-ttu-id="b316a-134">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="b316a-134">CertIssuerOid</span></span>](#certissueroid) |[<span data-ttu-id="b316a-135">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="b316a-135">CertKeyAlgorithm</span></span>](#certkeyalgorithm) | |
| [<span data-ttu-id="b316a-136">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="b316a-136">CertKeyAlgorithmParams</span></span>](#certkeyalgorithmparams) |[<span data-ttu-id="b316a-137">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="b316a-137">CertNameInfo</span></span>](#certnameinfo) |[<span data-ttu-id="b316a-138">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="b316a-138">CertNotAfter</span></span>](#certnotafter) |[<span data-ttu-id="b316a-139">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="b316a-139">CertNotBefore</span></span>](#certnotbefore) | |
| [<span data-ttu-id="b316a-140">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="b316a-140">CertPublicKeyOid</span></span>](#certpublickeyoid) |[<span data-ttu-id="b316a-141">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="b316a-141">CertPublicKeyParametersOid</span></span>](#certpublickeyparametersoid) |[<span data-ttu-id="b316a-142">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="b316a-142">CertSerialNumber</span></span>](#certserialnumber) |[<span data-ttu-id="b316a-143">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="b316a-143">CertSignatureAlgorithmOid</span></span>](#certsignaturealgorithmoid) | |
| [<span data-ttu-id="b316a-144">CertSubject</span><span class="sxs-lookup"><span data-stu-id="b316a-144">CertSubject</span></span>](#certsubject) |[<span data-ttu-id="b316a-145">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="b316a-145">CertSubjectNameDN</span></span>](#certsubjectnamedn) |[<span data-ttu-id="b316a-146">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="b316a-146">CertSubjectNameOid</span></span>](#certsubjectnameoid) |[<span data-ttu-id="b316a-147">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="b316a-147">CertThumbprint</span></span>](#certthumbprint) | |
[<span data-ttu-id="b316a-148">CertVersion</span><span class="sxs-lookup"><span data-stu-id="b316a-148"> CertVersion</span></span>](#certversion) |[<span data-ttu-id="b316a-149">IsCert</span><span class="sxs-lookup"><span data-stu-id="b316a-149">IsCert</span></span>](#iscert) | | | |
| <span data-ttu-id="b316a-150">**Conversie**</span><span class="sxs-lookup"><span data-stu-id="b316a-150">**Conversion**</span></span> | | | | |
| [<span data-ttu-id="b316a-151">CBool</span><span class="sxs-lookup"><span data-stu-id="b316a-151">CBool</span></span>](#cbool) |[<span data-ttu-id="b316a-152">CDate</span><span class="sxs-lookup"><span data-stu-id="b316a-152">CDate</span></span>](#cdate) |[<span data-ttu-id="b316a-153">CGuid</span><span class="sxs-lookup"><span data-stu-id="b316a-153">CGuid</span></span>](#cguid) |[<span data-ttu-id="b316a-154">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="b316a-154">ConvertFromBase64</span></span>](#convertfrombase64) | |
| [<span data-ttu-id="b316a-155">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="b316a-155">ConvertToBase64</span></span>](#converttobase64) |[<span data-ttu-id="b316a-156">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="b316a-156">ConvertFromUTF8Hex</span></span>](#convertfromutf8hex) |[<span data-ttu-id="b316a-157">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="b316a-157">ConvertToUTF8Hex</span></span>](#converttoutf8hex) |[<span data-ttu-id="b316a-158">CNum</span><span class="sxs-lookup"><span data-stu-id="b316a-158">CNum</span></span>](#cnum) | |
| [<span data-ttu-id="b316a-159">CRef</span><span class="sxs-lookup"><span data-stu-id="b316a-159">CRef</span></span>](#cref) |[<span data-ttu-id="b316a-160">CStr</span><span class="sxs-lookup"><span data-stu-id="b316a-160">CStr</span></span>](#cstr) |[<span data-ttu-id="b316a-161">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="b316a-161">StringFromGuid</span></span>](#StringFromGuid) |[<span data-ttu-id="b316a-162">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="b316a-162">StringFromSid</span></span>](#stringfromsid) | |
| <span data-ttu-id="b316a-163">**Datum / tijd**</span><span class="sxs-lookup"><span data-stu-id="b316a-163">**Date / Time**</span></span> | | | | |
| [<span data-ttu-id="b316a-164">DateAdd</span><span class="sxs-lookup"><span data-stu-id="b316a-164">DateAdd</span></span>](#dateadd) |[<span data-ttu-id="b316a-165">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="b316a-165">DateFromNum</span></span>](#datefromnum) |[<span data-ttu-id="b316a-166">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="b316a-166">FormatDateTime</span></span>](#formatdatetime) |[<span data-ttu-id="b316a-167">Nu</span><span class="sxs-lookup"><span data-stu-id="b316a-167">Now</span></span>](#now) | |
| [<span data-ttu-id="b316a-168">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="b316a-168">NumFromDate</span></span>](#numfromdate) | | | | |
| <span data-ttu-id="b316a-169">**Directory**</span><span class="sxs-lookup"><span data-stu-id="b316a-169">**Directory**</span></span> | | | | |
| [<span data-ttu-id="b316a-170">DNComponent</span><span class="sxs-lookup"><span data-stu-id="b316a-170">DNComponent</span></span>](#dncomponent) |[<span data-ttu-id="b316a-171">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="b316a-171">DNComponentRev</span></span>](#dncomponentrev) |[<span data-ttu-id="b316a-172">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="b316a-172">EscapeDNComponent</span></span>](#escapedncomponent) | | |
| <span data-ttu-id="b316a-173">**Evaluatie**</span><span class="sxs-lookup"><span data-stu-id="b316a-173">**Evaluation**</span></span> | | | | |
| [<span data-ttu-id="b316a-174">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="b316a-174">IsBitSet</span></span>](#isbitset) |[<span data-ttu-id="b316a-175">IsDate</span><span class="sxs-lookup"><span data-stu-id="b316a-175">IsDate</span></span>](#isdate) |[<span data-ttu-id="b316a-176">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="b316a-176">IsEmpty</span></span>](#isempty) |[<span data-ttu-id="b316a-177">IsGuid</span><span class="sxs-lookup"><span data-stu-id="b316a-177">IsGuid</span></span>](#isguid) | |
| [<span data-ttu-id="b316a-178">IsNull</span><span class="sxs-lookup"><span data-stu-id="b316a-178">IsNull</span></span>](#isnull) |[<span data-ttu-id="b316a-179">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="b316a-179">IsNullOrEmpty</span></span>](#isnullorempty) |[<span data-ttu-id="b316a-180">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="b316a-180">IsNumeric</span></span>](#isnumeric) |[<span data-ttu-id="b316a-181">IsPresent</span><span class="sxs-lookup"><span data-stu-id="b316a-181">IsPresent</span></span>](#ispresent) | |
| [<span data-ttu-id="b316a-182">IsString</span><span class="sxs-lookup"><span data-stu-id="b316a-182">IsString</span></span>](#isstring) | | | | |
| <span data-ttu-id="b316a-183">**Math**</span><span class="sxs-lookup"><span data-stu-id="b316a-183">**Math**</span></span> | | | | |
| [<span data-ttu-id="b316a-184">BitAnd</span><span class="sxs-lookup"><span data-stu-id="b316a-184">BitAnd</span></span>](#bitand) |[<span data-ttu-id="b316a-185">BitOr</span><span class="sxs-lookup"><span data-stu-id="b316a-185">BitOr</span></span>](#bitor) |[<span data-ttu-id="b316a-186">RandomNum</span><span class="sxs-lookup"><span data-stu-id="b316a-186">RandomNum</span></span>](#randomnum) | | |
| <span data-ttu-id="b316a-187">**Met meerdere waarden**</span><span class="sxs-lookup"><span data-stu-id="b316a-187">**Multi-valued**</span></span> | | | | |
| [<span data-ttu-id="b316a-188">Bevat</span><span class="sxs-lookup"><span data-stu-id="b316a-188">Contains</span></span>](#contains) |[<span data-ttu-id="b316a-189">Aantal</span><span class="sxs-lookup"><span data-stu-id="b316a-189">Count</span></span>](#count) |[<span data-ttu-id="b316a-190">Item</span><span class="sxs-lookup"><span data-stu-id="b316a-190">Item</span></span>](#item) |[<span data-ttu-id="b316a-191">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="b316a-191">ItemOrNull</span></span>](#itemornull) | |
| [<span data-ttu-id="b316a-192">Koppelen</span><span class="sxs-lookup"><span data-stu-id="b316a-192">Join</span></span>](#join) |[<span data-ttu-id="b316a-193">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="b316a-193">RemoveDuplicates</span></span>](#removeduplicates) |[<span data-ttu-id="b316a-194">Splitsen</span><span class="sxs-lookup"><span data-stu-id="b316a-194">Split</span></span>](#split) | | |
| <span data-ttu-id="b316a-195">**Programma-overdracht**</span><span class="sxs-lookup"><span data-stu-id="b316a-195">**Program Flow**</span></span> | | | | |
| [<span data-ttu-id="b316a-196">Fout</span><span class="sxs-lookup"><span data-stu-id="b316a-196">Error</span></span>](#error) |[<span data-ttu-id="b316a-197">IIF</span><span class="sxs-lookup"><span data-stu-id="b316a-197">IIF</span></span>](#iif) |[<span data-ttu-id="b316a-198">Selecteren</span><span class="sxs-lookup"><span data-stu-id="b316a-198">Select</span></span>](#select) |[<span data-ttu-id="b316a-199">Switch</span><span class="sxs-lookup"><span data-stu-id="b316a-199">Switch</span></span>](#switch) | |
| [<span data-ttu-id="b316a-200">Waar</span><span class="sxs-lookup"><span data-stu-id="b316a-200">Where</span></span>](#where) |[<span data-ttu-id="b316a-201">Met</span><span class="sxs-lookup"><span data-stu-id="b316a-201">With</span></span>](#with) | | | |
| <span data-ttu-id="b316a-202">**Tekst**</span><span class="sxs-lookup"><span data-stu-id="b316a-202">**Text**</span></span> | | | | |
| [<span data-ttu-id="b316a-203">GUID</span><span class="sxs-lookup"><span data-stu-id="b316a-203">GUID</span></span>](#guid) |[<span data-ttu-id="b316a-204">InStr</span><span class="sxs-lookup"><span data-stu-id="b316a-204">InStr</span></span>](#instr) |[<span data-ttu-id="b316a-205">InStrRev</span><span class="sxs-lookup"><span data-stu-id="b316a-205">InStrRev</span></span>](#instrrev) |[<span data-ttu-id="b316a-206">LCase</span><span class="sxs-lookup"><span data-stu-id="b316a-206">LCase</span></span>](#lcase) | |
| [<span data-ttu-id="b316a-207">Links</span><span class="sxs-lookup"><span data-stu-id="b316a-207">Left</span></span>](#left) |[<span data-ttu-id="b316a-208">Len</span><span class="sxs-lookup"><span data-stu-id="b316a-208">Len</span></span>](#len) |[<span data-ttu-id="b316a-209">LTrim</span><span class="sxs-lookup"><span data-stu-id="b316a-209">LTrim</span></span>](#ltrim) |[<span data-ttu-id="b316a-210">Mid</span><span class="sxs-lookup"><span data-stu-id="b316a-210">Mid</span></span>](#mid) | |
| [<span data-ttu-id="b316a-211">PadLeft</span><span class="sxs-lookup"><span data-stu-id="b316a-211">PadLeft</span></span>](#padleft) |[<span data-ttu-id="b316a-212">PadRight</span><span class="sxs-lookup"><span data-stu-id="b316a-212">PadRight</span></span>](#padright) |[<span data-ttu-id="b316a-213">PCase</span><span class="sxs-lookup"><span data-stu-id="b316a-213">PCase</span></span>](#pcase) |[<span data-ttu-id="b316a-214">Vervangen</span><span class="sxs-lookup"><span data-stu-id="b316a-214">Replace</span></span>](#replace) | |
| [<span data-ttu-id="b316a-215">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="b316a-215">ReplaceChars</span></span>](#replacechars) |[<span data-ttu-id="b316a-216">Rechts</span><span class="sxs-lookup"><span data-stu-id="b316a-216">Right</span></span>](#right) |[<span data-ttu-id="b316a-217">RTrim</span><span class="sxs-lookup"><span data-stu-id="b316a-217">RTrim</span></span>](#rtrim) |[<span data-ttu-id="b316a-218">Trim</span><span class="sxs-lookup"><span data-stu-id="b316a-218">Trim</span></span>](#trim) | |
| [<span data-ttu-id="b316a-219">UCase</span><span class="sxs-lookup"><span data-stu-id="b316a-219">UCase</span></span>](#ucase) |[<span data-ttu-id="b316a-220">Word</span><span class="sxs-lookup"><span data-stu-id="b316a-220">Word</span></span>](#word) | | | |

- - -
### <a name="bitand"></a><span data-ttu-id="b316a-221">BitAnd</span><span class="sxs-lookup"><span data-stu-id="b316a-221">BitAnd</span></span>
<span data-ttu-id="b316a-222">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-222">**Description:**</span></span>  
<span data-ttu-id="b316a-223">Hallo functie BitAnd wordt opgegeven bits ingesteld op een waarde.</span><span class="sxs-lookup"><span data-stu-id="b316a-223">hello BitAnd function sets specified bits on a value.</span></span>

<span data-ttu-id="b316a-224">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-224">**Syntax:**</span></span>  
`num BitAnd(num value1, num value2)`

* <span data-ttu-id="b316a-225">Value1, value2: numerieke waarden die functiesleutels samen moeten worden</span><span class="sxs-lookup"><span data-stu-id="b316a-225">value1, value2: numeric values that should be AND’ed together</span></span>

<span data-ttu-id="b316a-226">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-226">**Remarks:**</span></span>  
<span data-ttu-id="b316a-227">Deze functie worden geconverteerd van beide parameters toohello binaire voorstelling en iets op:</span><span class="sxs-lookup"><span data-stu-id="b316a-227">This function converts both parameters toohello binary representation and sets a bit to:</span></span>

* <span data-ttu-id="b316a-228">0 - als een of beide van de bijbehorende bits in Hallo *masker* en *vlag* 0 zijn</span><span class="sxs-lookup"><span data-stu-id="b316a-228">0 - if one or both of hello corresponding bits in *mask* and *flag* are 0</span></span>
* <span data-ttu-id="b316a-229">1 - als de bijbehorende bits Hallo 1 zijn.</span><span class="sxs-lookup"><span data-stu-id="b316a-229">1 - if both of hello corresponding bits are 1.</span></span>

<span data-ttu-id="b316a-230">Met andere woorden, resultaat het 0 in alle gevallen, behalve wanneer de bijbehorende bits Hallo van beide parameters 1.</span><span class="sxs-lookup"><span data-stu-id="b316a-230">In other words, it returns 0 in all cases except when hello corresponding bits of both parameters are 1.</span></span>

<span data-ttu-id="b316a-231">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-231">**Example:**</span></span>  
`BitAnd(&HF, &HF7)`  
<span data-ttu-id="b316a-232">Retourneert 7 omdat hexadecimale 'F' en 'F7' toothis waarde evalueren.</span><span class="sxs-lookup"><span data-stu-id="b316a-232">Returns 7 because hexadecimal "F" AND "F7" evaluate toothis value.</span></span>

- - -
### <a name="bitor"></a><span data-ttu-id="b316a-233">BitOr</span><span class="sxs-lookup"><span data-stu-id="b316a-233">BitOr</span></span>
<span data-ttu-id="b316a-234">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-234">**Description:**</span></span>  
<span data-ttu-id="b316a-235">Hallo functie BitOr wordt opgegeven bits ingesteld op een waarde.</span><span class="sxs-lookup"><span data-stu-id="b316a-235">hello BitOr function sets specified bits on a value.</span></span>

<span data-ttu-id="b316a-236">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-236">**Syntax:**</span></span>  
`num BitOr(num value1, num value2)`

* <span data-ttu-id="b316a-237">Value1, value2: numerieke waarden die samen worden moeten</span><span class="sxs-lookup"><span data-stu-id="b316a-237">value1, value2: numeric values that should be OR’ed together</span></span>

<span data-ttu-id="b316a-238">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-238">**Remarks:**</span></span>  
<span data-ttu-id="b316a-239">Deze functie converteert beide parameters toohello binaire voorstelling en een too1 bits ingesteld als een of beide van de bijbehorende bits Hallo in masker en markering 1 en too0 zijn als de bijbehorende bits Hallo 0 zijn.</span><span class="sxs-lookup"><span data-stu-id="b316a-239">This function converts both parameters toohello binary representation and sets a bit too1 if one or both of hello corresponding bits in mask and flag are 1, and too0 if both of hello corresponding bits are 0.</span></span> <span data-ttu-id="b316a-240">Met andere woorden, retourneert 1 in alle gevallen behalve wanneer de bijbehorende bits Hallo van beide parameters 0.</span><span class="sxs-lookup"><span data-stu-id="b316a-240">In other words, it returns 1 in all cases except where hello corresponding bits of both parameters are 0.</span></span>

- - -
### <a name="cbool"></a><span data-ttu-id="b316a-241">CBool</span><span class="sxs-lookup"><span data-stu-id="b316a-241">CBool</span></span>
<span data-ttu-id="b316a-242">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-242">**Description:**</span></span>  
<span data-ttu-id="b316a-243">Hallo CBool functie retourneert een Booleaanse waarde die is gebaseerd op Hallo geëvalueerd expressie</span><span class="sxs-lookup"><span data-stu-id="b316a-243">hello CBool function returns a Boolean based on hello evaluated expression</span></span>

<span data-ttu-id="b316a-244">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-244">**Syntax:**</span></span>  
`bool CBool(exp Expression)`

<span data-ttu-id="b316a-245">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-245">**Remarks:**</span></span>  
<span data-ttu-id="b316a-246">Als Hallo expressie tooa andere waarde dan nul, resulteert en True CBool retourneert, anders wordt onwaar.</span><span class="sxs-lookup"><span data-stu-id="b316a-246">If hello expression evaluates tooa nonzero value, then CBool returns True, else it returns False.</span></span>

<span data-ttu-id="b316a-247">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-247">**Example:**</span></span>  
`CBool([attrib1] = [attrib2])`  

<span data-ttu-id="b316a-248">Retourneert waar als beide kenmerken hebben dezelfde waarde Hallo.</span><span class="sxs-lookup"><span data-stu-id="b316a-248">Returns True if both attributes have hello same value.</span></span>

- - -
### <a name="cdate"></a><span data-ttu-id="b316a-249">CDate</span><span class="sxs-lookup"><span data-stu-id="b316a-249">CDate</span></span>
<span data-ttu-id="b316a-250">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-250">**Description:**</span></span>  
<span data-ttu-id="b316a-251">Hallo functie CDate retourneert een UTC datetime-waarde van een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b316a-251">hello CDate function returns a UTC DateTime from a string.</span></span> <span data-ttu-id="b316a-252">Datum/tijd is niet een systeemeigen kenmerktype synchroon maar wordt gebruikt door een aantal functies.</span><span class="sxs-lookup"><span data-stu-id="b316a-252">DateTime is not a native attribute type in Sync but is used by some functions.</span></span>

<span data-ttu-id="b316a-253">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-253">**Syntax:**</span></span>  
`dt CDate(str value)`

* <span data-ttu-id="b316a-254">Waarde: Een tekenreeks met een datum, tijd en eventueel tijdzone</span><span class="sxs-lookup"><span data-stu-id="b316a-254">Value: A string with a date, time, and optionally time zone</span></span>

<span data-ttu-id="b316a-255">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-255">**Remarks:**</span></span>  
<span data-ttu-id="b316a-256">Hallo geretourneerde tekenreeks is altijd ingesteld op UTC.</span><span class="sxs-lookup"><span data-stu-id="b316a-256">hello returned string is always in UTC.</span></span>

<span data-ttu-id="b316a-257">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-257">**Example:**</span></span>  
`CDate([employeeStartTime])`  
<span data-ttu-id="b316a-258">Retourneert een datum-/ op basis van de begintijd van de werknemer Hallo</span><span class="sxs-lookup"><span data-stu-id="b316a-258">Returns a DateTime based on hello employee’s start time</span></span>

`CDate("2013-01-10 4:00 PM -8")`  
<span data-ttu-id="b316a-259">Retourneert een DateTime-waarde die aangeeft ' 2013-01-11-12:00 AM '</span><span class="sxs-lookup"><span data-stu-id="b316a-259">Returns a DateTime representing "2013-01-11 12:00 AM"</span></span>








- - -
### <a name="certextensionoids"></a><span data-ttu-id="b316a-260">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="b316a-260">CertExtensionOids</span></span>
<span data-ttu-id="b316a-261">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-261">**Description:**</span></span>  
<span data-ttu-id="b316a-262">Retourneert Hallo Oid-waarden van alle Hallo kritieke uitbreidingen van een certificaatobject.</span><span class="sxs-lookup"><span data-stu-id="b316a-262">Returns hello Oid values of all hello critical extensions of a certificate object.</span></span>

<span data-ttu-id="b316a-263">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-263">**Syntax:**</span></span>  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   <span data-ttu-id="b316a-264">certificateRawData: Byte matrix representatie van een X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-264">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="b316a-265">Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.</span><span class="sxs-lookup"><span data-stu-id="b316a-265">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certformat"></a><span data-ttu-id="b316a-266">CertFormat</span><span class="sxs-lookup"><span data-stu-id="b316a-266">CertFormat</span></span>
<span data-ttu-id="b316a-267">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-267">**Description:**</span></span>  
<span data-ttu-id="b316a-268">Retourneert Hallo naam van het Hallo-indeling van deze X.509v3-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-268">Returns hello name of hello format of this X.509v3 certificate.</span></span>

<span data-ttu-id="b316a-269">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-269">**Syntax:**</span></span>  
`str CertFormat(binary certificateRawData)`  
*   <span data-ttu-id="b316a-270">certificateRawData: Byte matrix representatie van een X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-270">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="b316a-271">Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.</span><span class="sxs-lookup"><span data-stu-id="b316a-271">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certfriendlyname"></a><span data-ttu-id="b316a-272">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="b316a-272">CertFriendlyName</span></span>
<span data-ttu-id="b316a-273">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-273">**Description:**</span></span>  
<span data-ttu-id="b316a-274">Retourneert Hallo alias voor een certificaat dat is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="b316a-274">Returns hello associated alias for a certificate.</span></span>

<span data-ttu-id="b316a-275">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-275">**Syntax:**</span></span>  
`str CertFriendlyName(binary certificateRawData)`  
*   <span data-ttu-id="b316a-276">certificateRawData: Byte matrix representatie van een X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-276">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="b316a-277">Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.</span><span class="sxs-lookup"><span data-stu-id="b316a-277">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certhashstring"></a><span data-ttu-id="b316a-278">CertHashString</span><span class="sxs-lookup"><span data-stu-id="b316a-278">CertHashString</span></span>
<span data-ttu-id="b316a-279">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-279">**Description:**</span></span>  
<span data-ttu-id="b316a-280">Retourneert Hallo SHA1-hash-waarde voor Hallo X.509v3-certificaat als hexadecimale tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b316a-280">Returns hello SHA1 hash value for hello X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="b316a-281">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-281">**Syntax:**</span></span>  
`str CertHashString(binary certificateRawData)`  
*   <span data-ttu-id="b316a-282">certificateRawData: Byte matrix representatie van een X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-282">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="b316a-283">Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.</span><span class="sxs-lookup"><span data-stu-id="b316a-283">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuer"></a><span data-ttu-id="b316a-284">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="b316a-284">CertIssuer</span></span>
<span data-ttu-id="b316a-285">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-285">**Description:**</span></span>  
<span data-ttu-id="b316a-286">Retourneert Hallo naam van certificeringsinstantie Hallo die Hallo X.509v3-certificaat heeft uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="b316a-286">Returns hello name of hello certificate authority that issued hello X.509v3 certificate.</span></span>

<span data-ttu-id="b316a-287">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-287">**Syntax:**</span></span>  
`str CertIssuer(binary certificateRawData)`  
*   <span data-ttu-id="b316a-288">certificateRawData: Byte matrix representatie van een X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-288">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="b316a-289">Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.</span><span class="sxs-lookup"><span data-stu-id="b316a-289">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuerdn"></a><span data-ttu-id="b316a-290">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="b316a-290">CertIssuerDN</span></span>
<span data-ttu-id="b316a-291">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-291">**Description:**</span></span>  
<span data-ttu-id="b316a-292">Retourneert Hallo DN-naam van de certificaatverlener Hallo.</span><span class="sxs-lookup"><span data-stu-id="b316a-292">Returns hello distinguished name of hello certificate issuer.</span></span>

<span data-ttu-id="b316a-293">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-293">**Syntax:**</span></span>  
`str CertIssuerDN(binary certificateRawData)`  
*   <span data-ttu-id="b316a-294">certificateRawData: Byte matrix representatie van een X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-294">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="b316a-295">Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.</span><span class="sxs-lookup"><span data-stu-id="b316a-295">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissueroid"></a><span data-ttu-id="b316a-296">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="b316a-296">CertIssuerOid</span></span>
<span data-ttu-id="b316a-297">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-297">**Description:**</span></span>  
<span data-ttu-id="b316a-298">Retourneert Hallo Oid Hallo van verlener van certificaten.</span><span class="sxs-lookup"><span data-stu-id="b316a-298">Returns hello Oid of hello certificate issuer.</span></span>

<span data-ttu-id="b316a-299">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-299">**Syntax:**</span></span>  
`str CertIssuerOid(binary certificateRawData)`  
*   <span data-ttu-id="b316a-300">certificateRawData: Byte matrix representatie van een X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-300">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="b316a-301">Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.</span><span class="sxs-lookup"><span data-stu-id="b316a-301">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithm"></a><span data-ttu-id="b316a-302">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="b316a-302">CertKeyAlgorithm</span></span>
<span data-ttu-id="b316a-303">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-303">**Description:**</span></span>  
<span data-ttu-id="b316a-304">Retourneert Hallo sleutelalgoritme informatie voor deze X.509v3-certificaat als een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b316a-304">Returns hello key algorithm information for this X.509v3 certificate as a string.</span></span>

<span data-ttu-id="b316a-305">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-305">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="b316a-306">certificateRawData: Byte matrix representatie van een X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-306">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="b316a-307">Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.</span><span class="sxs-lookup"><span data-stu-id="b316a-307">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithmparams"></a><span data-ttu-id="b316a-308">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="b316a-308">CertKeyAlgorithmParams</span></span>
<span data-ttu-id="b316a-309">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-309">**Description:**</span></span>  
<span data-ttu-id="b316a-310">Retourneert een hexadecimale tekenreeks Hallo sleutelalgoritme parameters voor Hallo X.509v3-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-310">Returns hello key algorithm parameters for hello X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="b316a-311">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-311">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="b316a-312">certificateRawData: Byte matrix representatie van een X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-312">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="b316a-313">Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.</span><span class="sxs-lookup"><span data-stu-id="b316a-313">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnameinfo"></a><span data-ttu-id="b316a-314">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="b316a-314">CertNameInfo</span></span>
<span data-ttu-id="b316a-315">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-315">**Description:**</span></span>  
<span data-ttu-id="b316a-316">Retourneert Hallo onderwerp en de verlener namen van een certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-316">Returns hello subject and issuer names from a certificate.</span></span>

<span data-ttu-id="b316a-317">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-317">**Syntax:**</span></span>  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   <span data-ttu-id="b316a-318">certificateRawData: Byte matrix representatie van een X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-318">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="b316a-319">Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.</span><span class="sxs-lookup"><span data-stu-id="b316a-319">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
*   <span data-ttu-id="b316a-320">X509NameType: hello X509NameType waarde voor Hallo onderwerp.</span><span class="sxs-lookup"><span data-stu-id="b316a-320">X509NameType: hello X509NameType value for hello subject.</span></span>
*   <span data-ttu-id="b316a-321">includesIssuerName: true tooinclude Hallo certificaatverlener; anders wordt onwaar.</span><span class="sxs-lookup"><span data-stu-id="b316a-321">includesIssuerName: true tooinclude hello issuer name; otherwise, false.</span></span>

- - -
### <a name="certnotafter"></a><span data-ttu-id="b316a-322">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="b316a-322">CertNotAfter</span></span>
<span data-ttu-id="b316a-323">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-323">**Description:**</span></span>  
<span data-ttu-id="b316a-324">Retourneert Hallo datum in plaatselijke tijd waarna een certificaat niet meer geldig is.</span><span class="sxs-lookup"><span data-stu-id="b316a-324">Returns hello date in local time after which a certificate is no longer valid.</span></span>

<span data-ttu-id="b316a-325">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-325">**Syntax:**</span></span>  
`dt CertNotAfter(binary certificateRawData)`  
*   <span data-ttu-id="b316a-326">certificateRawData: Byte matrix representatie van een X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-326">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="b316a-327">Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.</span><span class="sxs-lookup"><span data-stu-id="b316a-327">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnotbefore"></a><span data-ttu-id="b316a-328">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="b316a-328">CertNotBefore</span></span>
<span data-ttu-id="b316a-329">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-329">**Description:**</span></span>  
<span data-ttu-id="b316a-330">Retourneert Hallo datum in plaatselijke tijd waarop een certificaat geldig wordt.</span><span class="sxs-lookup"><span data-stu-id="b316a-330">Returns hello date in local time on which a certificate becomes valid.</span></span>

<span data-ttu-id="b316a-331">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-331">**Syntax:**</span></span>  
`dt CertNotBefore(binary certificateRawData)`  
*   <span data-ttu-id="b316a-332">certificateRawData: Byte matrix representatie van een X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-332">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="b316a-333">Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.</span><span class="sxs-lookup"><span data-stu-id="b316a-333">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyoid"></a><span data-ttu-id="b316a-334">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="b316a-334">CertPublicKeyOid</span></span>
<span data-ttu-id="b316a-335">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-335">**Description:**</span></span>  
<span data-ttu-id="b316a-336">Retourneert Hallo Oid van de openbare sleutel Hallo voor Hallo X.509v3-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-336">Returns hello Oid of hello public key for hello X.509v3 certificate.</span></span>

<span data-ttu-id="b316a-337">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-337">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="b316a-338">certificateRawData: Byte matrix representatie van een X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-338">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="b316a-339">Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.</span><span class="sxs-lookup"><span data-stu-id="b316a-339">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyparametersoid"></a><span data-ttu-id="b316a-340">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="b316a-340">CertPublicKeyParametersOid</span></span>
<span data-ttu-id="b316a-341">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-341">**Description:**</span></span>  
<span data-ttu-id="b316a-342">Retourneert Hallo Oid van Hallo openbare sleutel parameters voor Hallo X.509v3-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-342">Returns hello Oid of hello public key parameters for hello X.509v3 certificate.</span></span>

<span data-ttu-id="b316a-343">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-343">**Syntax:**</span></span>  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   <span data-ttu-id="b316a-344">certificateRawData: Byte matrix representatie van een X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-344">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="b316a-345">Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.</span><span class="sxs-lookup"><span data-stu-id="b316a-345">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certserialnumber"></a><span data-ttu-id="b316a-346">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="b316a-346">CertSerialNumber</span></span>
<span data-ttu-id="b316a-347">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-347">**Description:**</span></span>  
<span data-ttu-id="b316a-348">Retourneert het serienummer Hallo van Hallo X.509v3-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-348">Returns hello serial number of hello X.509v3 certificate.</span></span>

<span data-ttu-id="b316a-349">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-349">**Syntax:**</span></span>  
`str CertSerialNumber(binary certificateRawData)`  
*   <span data-ttu-id="b316a-350">certificateRawData: Byte matrix representatie van een X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-350">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="b316a-351">Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.</span><span class="sxs-lookup"><span data-stu-id="b316a-351">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsignaturealgorithmoid"></a><span data-ttu-id="b316a-352">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="b316a-352">CertSignatureAlgorithmOid</span></span>
<span data-ttu-id="b316a-353">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-353">**Description:**</span></span>  
<span data-ttu-id="b316a-354">Retourneert Hallo Oid van Hallo algoritme toocreate Hallo handtekening van een certificaat gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b316a-354">Returns hello Oid of hello algorithm used toocreate hello signature of a certificate.</span></span>

<span data-ttu-id="b316a-355">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-355">**Syntax:**</span></span>  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   <span data-ttu-id="b316a-356">certificateRawData: Byte matrix representatie van een X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-356">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="b316a-357">Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.</span><span class="sxs-lookup"><span data-stu-id="b316a-357">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubject"></a><span data-ttu-id="b316a-358">CertSubject</span><span class="sxs-lookup"><span data-stu-id="b316a-358">CertSubject</span></span>
<span data-ttu-id="b316a-359">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-359">**Description:**</span></span>  
<span data-ttu-id="b316a-360">Opgehaald Hallo onderwerp DN-naam van een certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-360">Gets hello subject distinguished name from a certificate.</span></span>

<span data-ttu-id="b316a-361">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-361">**Syntax:**</span></span>  
`str CertSubject(binary certificateRawData)`  
*   <span data-ttu-id="b316a-362">certificateRawData: Byte matrix representatie van een X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-362">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="b316a-363">Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.</span><span class="sxs-lookup"><span data-stu-id="b316a-363">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnamedn"></a><span data-ttu-id="b316a-364">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="b316a-364">CertSubjectNameDN</span></span>
<span data-ttu-id="b316a-365">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-365">**Description:**</span></span>  
<span data-ttu-id="b316a-366">Retourneert Hallo onderwerp DN-naam van een certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-366">Returns hello subject distinguished name from a certificate.</span></span>

<span data-ttu-id="b316a-367">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-367">**Syntax:**</span></span>  
`str CertSubjectNameDN(binary certificateRawData)`  
*   <span data-ttu-id="b316a-368">certificateRawData: Byte matrix representatie van een X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-368">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="b316a-369">Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.</span><span class="sxs-lookup"><span data-stu-id="b316a-369">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnameoid"></a><span data-ttu-id="b316a-370">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="b316a-370">CertSubjectNameOid</span></span>
<span data-ttu-id="b316a-371">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-371">**Description:**</span></span>  
<span data-ttu-id="b316a-372">Retourneert Hallo Oid van Hallo onderwerp de naam van een certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-372">Returns hello Oid of hello subject name from a certificate.</span></span>

<span data-ttu-id="b316a-373">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-373">**Syntax:**</span></span>  
`str CertSubjectNameOid(binary certificateRawData)`  
*   <span data-ttu-id="b316a-374">certificateRawData: Byte matrix representatie van een X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-374">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="b316a-375">Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.</span><span class="sxs-lookup"><span data-stu-id="b316a-375">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certthumbprint"></a><span data-ttu-id="b316a-376">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="b316a-376">CertThumbprint</span></span>
<span data-ttu-id="b316a-377">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-377">**Description:**</span></span>  
<span data-ttu-id="b316a-378">Retourneert Hallo vingerafdruk van een certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-378">Returns hello thumbprint of a certificate.</span></span>

<span data-ttu-id="b316a-379">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-379">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="b316a-380">certificateRawData: Byte matrix representatie van een X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-380">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="b316a-381">Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.</span><span class="sxs-lookup"><span data-stu-id="b316a-381">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certversion"></a><span data-ttu-id="b316a-382">CertVersion</span><span class="sxs-lookup"><span data-stu-id="b316a-382">CertVersion</span></span>
<span data-ttu-id="b316a-383">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-383">**Description:**</span></span>  
<span data-ttu-id="b316a-384">Retourneert Hallo versie van het X.509-indeling van een certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-384">Returns hello X.509 format version of a certificate.</span></span>

<span data-ttu-id="b316a-385">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-385">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="b316a-386">certificateRawData: Byte matrix representatie van een X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-386">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="b316a-387">Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.</span><span class="sxs-lookup"><span data-stu-id="b316a-387">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="cguid"></a><span data-ttu-id="b316a-388">CGuid</span><span class="sxs-lookup"><span data-stu-id="b316a-388">CGuid</span></span>
<span data-ttu-id="b316a-389">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-389">**Description:**</span></span>  
<span data-ttu-id="b316a-390">Hallo CGuid functie converteert Hallo tekenreeksweergave van een binaire voorstelling van GUID tooits.</span><span class="sxs-lookup"><span data-stu-id="b316a-390">hello CGuid function converts hello string representation of a GUID tooits binary representation.</span></span>

<span data-ttu-id="b316a-391">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-391">**Syntax:**</span></span>  
`bin CGuid(str GUID)`

* <span data-ttu-id="b316a-392">Een tekenreeks in dit patroon worden opgemaakt: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx of {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="b316a-392">A String formatted in this pattern: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

- - -
### <a name="contains"></a><span data-ttu-id="b316a-393">Contains</span><span class="sxs-lookup"><span data-stu-id="b316a-393">Contains</span></span>
<span data-ttu-id="b316a-394">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-394">**Description:**</span></span>  
<span data-ttu-id="b316a-395">Hallo bevat functie zoekt een tekenreeks binnen een kenmerk met meerdere waarden</span><span class="sxs-lookup"><span data-stu-id="b316a-395">hello Contains function finds a string inside a multi-valued attribute</span></span>

<span data-ttu-id="b316a-396">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-396">**Syntax:**</span></span>  
<span data-ttu-id="b316a-397">`num Contains (mvstring attribute, str search)`-hoofdlettergevoelig</span><span class="sxs-lookup"><span data-stu-id="b316a-397">`num Contains (mvstring attribute, str search)` - case-sensitive</span></span>  
`num Contains (mvstring attribute, str search, enum Casetype)`  
<span data-ttu-id="b316a-398">`num Contains (mvref attribute, str search)`-hoofdlettergevoelig</span><span class="sxs-lookup"><span data-stu-id="b316a-398">`num Contains (mvref attribute, str search)` - case-sensitive</span></span>

* <span data-ttu-id="b316a-399">kenmerk: Hallo kenmerk met meerdere waarden toosearch.</span><span class="sxs-lookup"><span data-stu-id="b316a-399">attribute: hello multi-valued attribute toosearch.</span></span>
* <span data-ttu-id="b316a-400">zoeken: string toofind in Hallo-kenmerk.</span><span class="sxs-lookup"><span data-stu-id="b316a-400">search: string toofind in hello attribute.</span></span>
* <span data-ttu-id="b316a-401">Casetype: CaseInsensitive of CaseSensitive.</span><span class="sxs-lookup"><span data-stu-id="b316a-401">Casetype: CaseInsensitive or CaseSensitive.</span></span>

<span data-ttu-id="b316a-402">Retourneert index in een kenmerk met meerdere waarden Hallo waar Hallo-tekenreeks is gevonden.</span><span class="sxs-lookup"><span data-stu-id="b316a-402">Returns index in hello multi-valued attribute where hello string was found.</span></span> <span data-ttu-id="b316a-403">0 wordt geretourneerd als het Hallo-tekenreeks is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="b316a-403">0 is returned if hello string is not found.</span></span>

<span data-ttu-id="b316a-404">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-404">**Remarks:**</span></span>  
<span data-ttu-id="b316a-405">Voor tekenreekskenmerken met meerdere waarden Hallo gezocht subtekenreeksen in Hallo waarden.</span><span class="sxs-lookup"><span data-stu-id="b316a-405">For multi-valued string attributes, hello search finds substrings in hello values.</span></span>  
<span data-ttu-id="b316a-406">Voor verwijzingskenmerken moet hello gezochte tekenreeks exact overeenkomen Hallo waarde toobe beschouwd als een overeenkomst.</span><span class="sxs-lookup"><span data-stu-id="b316a-406">For reference attributes, hello searched string must exactly match hello value toobe considered a match.</span></span>

<span data-ttu-id="b316a-407">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-407">**Example:**</span></span>  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
<span data-ttu-id="b316a-408">Als Hallo proxyAddresses kenmerk een primaire e-mailadres heeft (aangeduid door hoofdletters ' SMTP: '), Ga daarna terug Hallo proxyAddress kenmerk, anders retourneren een foutmelding.</span><span class="sxs-lookup"><span data-stu-id="b316a-408">If hello proxyAddresses attribute has a primary email address (indicated by uppercase "SMTP:"), then return hello proxyAddress attribute, else return an error.</span></span>

- - -
### <a name="convertfrombase64"></a><span data-ttu-id="b316a-409">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="b316a-409">ConvertFromBase64</span></span>
<span data-ttu-id="b316a-410">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-410">**Description:**</span></span>  
<span data-ttu-id="b316a-411">Hallo ConvertFromBase64 functie converteert Hallo base64-gecodeerde waarde tooa reguliere tekenreeks opgegeven.</span><span class="sxs-lookup"><span data-stu-id="b316a-411">hello ConvertFromBase64 function converts hello specified base64 encoded value tooa regular string.</span></span>

<span data-ttu-id="b316a-412">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-412">**Syntax:**</span></span>  
<span data-ttu-id="b316a-413">`str ConvertFromBase64(str source)`-wordt ervan uitgegaan dat Unicode voor codering</span><span class="sxs-lookup"><span data-stu-id="b316a-413">`str ConvertFromBase64(str source)` - assumes Unicode for encoding</span></span>  
`str ConvertFromBase64(str source, enum Encoding)`

* <span data-ttu-id="b316a-414">bron: Base64-gecodeerde tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b316a-414">source: Base64 encoded string</span></span>  
* <span data-ttu-id="b316a-415">-Codering: Unicode, ASCII, UTF8</span><span class="sxs-lookup"><span data-stu-id="b316a-415">Encoding: Unicode, ASCII, UTF8</span></span>

<span data-ttu-id="b316a-416">**Voorbeeld**</span><span class="sxs-lookup"><span data-stu-id="b316a-416">**Example**</span></span>  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

<span data-ttu-id="b316a-417">Beide voorbeelden retourneren '*Hello world!*'</span><span class="sxs-lookup"><span data-stu-id="b316a-417">Both examples return "*Hello world!*"</span></span>

- - -
### <a name="convertfromutf8hex"></a><span data-ttu-id="b316a-418">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="b316a-418">ConvertFromUTF8Hex</span></span>
<span data-ttu-id="b316a-419">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-419">**Description:**</span></span>  
<span data-ttu-id="b316a-420">Hallo ConvertFromUTF8Hex functie converteert Hallo UTF8 hexadecimaal gecodeerde waarde tooa tekenreeks opgegeven.</span><span class="sxs-lookup"><span data-stu-id="b316a-420">hello ConvertFromUTF8Hex function converts hello specified UTF8 Hex encoded value tooa string.</span></span>

<span data-ttu-id="b316a-421">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-421">**Syntax:**</span></span>  
`str ConvertFromUTF8Hex(str source)`

* <span data-ttu-id="b316a-422">bron: UTF8 2-bytes gecodeerde String</span><span class="sxs-lookup"><span data-stu-id="b316a-422">source: UTF8 2-byte encoded sting</span></span>

<span data-ttu-id="b316a-423">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-423">**Remarks:**</span></span>  
<span data-ttu-id="b316a-424">Hallo verschil tussen deze functie en ConvertFromBase64([],UTF8) in die resulteren Hallo is beschrijvende voor Hallo DN-kenmerk.</span><span class="sxs-lookup"><span data-stu-id="b316a-424">hello difference between this function and ConvertFromBase64([],UTF8) in that hello result is friendly for hello DN attribute.</span></span>  
<span data-ttu-id="b316a-425">Deze indeling wordt gebruikt door Azure Active Directory als de DN-naam.</span><span class="sxs-lookup"><span data-stu-id="b316a-425">This format is used by Azure Active Directory as DN.</span></span>

<span data-ttu-id="b316a-426">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-426">**Example:**</span></span>  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
<span data-ttu-id="b316a-427">Retourneert '*Hello world!*'</span><span class="sxs-lookup"><span data-stu-id="b316a-427">Returns "*Hello world!*"</span></span>

- - -
### <a name="converttobase64"></a><span data-ttu-id="b316a-428">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="b316a-428">ConvertToBase64</span></span>
<span data-ttu-id="b316a-429">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-429">**Description:**</span></span>  
<span data-ttu-id="b316a-430">Hallo ConvertToBase64 functie zet een tekenreeks tooa Unicode base64-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b316a-430">hello ConvertToBase64 function converts a string tooa Unicode base64 string.</span></span>  
<span data-ttu-id="b316a-431">Converteert Hallo-waarde van een matrix van gehele getallen tooits gelijkwaardige tekenreeksweergave die is gecodeerd met base 64-cijfers.</span><span class="sxs-lookup"><span data-stu-id="b316a-431">Converts hello value of an array of integers tooits equivalent string representation that is encoded with base-64 digits.</span></span>

<span data-ttu-id="b316a-432">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-432">**Syntax:**</span></span>  
`str ConvertToBase64(str source)`

<span data-ttu-id="b316a-433">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-433">**Example:**</span></span>  
`ConvertToBase64("Hello world!")`  
<span data-ttu-id="b316a-434">Retourneert 'SABlAGwAbABvACAAdwBvAHIAbABkACEA'</span><span class="sxs-lookup"><span data-stu-id="b316a-434">Returns "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span></span>

- - -
### <a name="converttoutf8hex"></a><span data-ttu-id="b316a-435">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="b316a-435">ConvertToUTF8Hex</span></span>
<span data-ttu-id="b316a-436">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-436">**Description:**</span></span>  
<span data-ttu-id="b316a-437">Hallo ConvertToUTF8Hex functie zet een tekenreeks tooa UTF8 hexadecimaal gecodeerde waarde.</span><span class="sxs-lookup"><span data-stu-id="b316a-437">hello ConvertToUTF8Hex function converts a string tooa UTF8 Hex encoded value.</span></span>

<span data-ttu-id="b316a-438">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-438">**Syntax:**</span></span>  
`str ConvertToUTF8Hex(str source)`

<span data-ttu-id="b316a-439">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-439">**Remarks:**</span></span>  
<span data-ttu-id="b316a-440">Hallo de indeling van de uitvoer van deze functie wordt gebruikt door Azure Active Directory als de indeling van het kenmerk DN-naam.</span><span class="sxs-lookup"><span data-stu-id="b316a-440">hello output format of this function is used by Azure Active Directory as DN attribute format.</span></span>

<span data-ttu-id="b316a-441">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-441">**Example:**</span></span>  
`ConvertToUTF8Hex("Hello world!")`  
<span data-ttu-id="b316a-442">Retourneert 48656C6C6F20776F726C6421</span><span class="sxs-lookup"><span data-stu-id="b316a-442">Returns 48656C6C6F20776F726C6421</span></span>

- - -
### <a name="count"></a><span data-ttu-id="b316a-443">Count</span><span class="sxs-lookup"><span data-stu-id="b316a-443">Count</span></span>
<span data-ttu-id="b316a-444">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-444">**Description:**</span></span>  
<span data-ttu-id="b316a-445">Hallo functie Count retourneert Hallo aantal elementen in een kenmerk met meerdere waarden</span><span class="sxs-lookup"><span data-stu-id="b316a-445">hello Count function returns hello number of elements in a multi-valued attribute</span></span>

<span data-ttu-id="b316a-446">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-446">**Syntax:**</span></span>  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a><span data-ttu-id="b316a-447">CNum</span><span class="sxs-lookup"><span data-stu-id="b316a-447">CNum</span></span>
<span data-ttu-id="b316a-448">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-448">**Description:**</span></span>  
<span data-ttu-id="b316a-449">Hallo CNum functie een tekenreeks en retourneert een numeriek gegevenstype.</span><span class="sxs-lookup"><span data-stu-id="b316a-449">hello CNum function takes a string and returns a numeric data type.</span></span>

<span data-ttu-id="b316a-450">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-450">**Syntax:**</span></span>  
`num CNum(str value)`

- - -
### <a name="cref"></a><span data-ttu-id="b316a-451">CRef</span><span class="sxs-lookup"><span data-stu-id="b316a-451">CRef</span></span>
<span data-ttu-id="b316a-452">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-452">**Description:**</span></span>  
<span data-ttu-id="b316a-453">Zet een tekenreeks tooa-verwijzingskenmerk</span><span class="sxs-lookup"><span data-stu-id="b316a-453">Converts a string tooa reference attribute</span></span>

<span data-ttu-id="b316a-454">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-454">**Syntax:**</span></span>  
`ref CRef(str value)`

<span data-ttu-id="b316a-455">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-455">**Example:**</span></span>  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a><span data-ttu-id="b316a-456">CStr</span><span class="sxs-lookup"><span data-stu-id="b316a-456">CStr</span></span>
<span data-ttu-id="b316a-457">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-457">**Description:**</span></span>  
<span data-ttu-id="b316a-458">Hallo CStr functie converteert tooa tekenreeksgegevenstype.</span><span class="sxs-lookup"><span data-stu-id="b316a-458">hello CStr function converts tooa string data type.</span></span>

<span data-ttu-id="b316a-459">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-459">**Syntax:**</span></span>  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* <span data-ttu-id="b316a-460">waarde: een numerieke waarde, verwijzingskenmerk of Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="b316a-460">value: Can be a numeric value, reference attribute, or Boolean.</span></span>

<span data-ttu-id="b316a-461">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-461">**Example:**</span></span>  
`CStr([dn])`  
<span data-ttu-id="b316a-462">Kan retourneren "cn = Jan, dc = contoso, dc = com"</span><span class="sxs-lookup"><span data-stu-id="b316a-462">Could return "cn=Joe,dc=contoso,dc=com"</span></span>

- - -
### <a name="dateadd"></a><span data-ttu-id="b316a-463">DateAdd</span><span class="sxs-lookup"><span data-stu-id="b316a-463">DateAdd</span></span>
<span data-ttu-id="b316a-464">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-464">**Description:**</span></span>  
<span data-ttu-id="b316a-465">Retourneert een datum met een datum toowhich die een opgegeven tijdsinterval is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="b316a-465">Returns a Date containing a date toowhich a specified time interval has been added.</span></span>

<span data-ttu-id="b316a-466">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-466">**Syntax:**</span></span>  
`dt DateAdd(str interval, num value, dt date)`

* <span data-ttu-id="b316a-467">interval: tekenreeksexpressie die Hallo tijdsinterval tooadd gewenste.</span><span class="sxs-lookup"><span data-stu-id="b316a-467">interval: String expression that is hello interval of time you want tooadd.</span></span> <span data-ttu-id="b316a-468">Hallo-tekenreeks moet een van de Hallo volgende waarden hebben:</span><span class="sxs-lookup"><span data-stu-id="b316a-468">hello string must have one of hello following values:</span></span>
  * <span data-ttu-id="b316a-469">JJJJ jaar</span><span class="sxs-lookup"><span data-stu-id="b316a-469">yyyy Year</span></span>
  * <span data-ttu-id="b316a-470">q kwartaal</span><span class="sxs-lookup"><span data-stu-id="b316a-470">q Quarter</span></span>
  * <span data-ttu-id="b316a-471">m maand</span><span class="sxs-lookup"><span data-stu-id="b316a-471">m Month</span></span>
  * <span data-ttu-id="b316a-472">y-dag van jaar</span><span class="sxs-lookup"><span data-stu-id="b316a-472">y Day of year</span></span>
  * <span data-ttu-id="b316a-473">d dag</span><span class="sxs-lookup"><span data-stu-id="b316a-473">d Day</span></span>
  * <span data-ttu-id="b316a-474">w weekdag</span><span class="sxs-lookup"><span data-stu-id="b316a-474">w Weekday</span></span>
  * <span data-ttu-id="b316a-475">ww Week</span><span class="sxs-lookup"><span data-stu-id="b316a-475">ww Week</span></span>
  * <span data-ttu-id="b316a-476">h uur</span><span class="sxs-lookup"><span data-stu-id="b316a-476">h Hour</span></span>
  * <span data-ttu-id="b316a-477">n minuut</span><span class="sxs-lookup"><span data-stu-id="b316a-477">n Minute</span></span>
  * <span data-ttu-id="b316a-478">s tweede</span><span class="sxs-lookup"><span data-stu-id="b316a-478">s Second</span></span>
* <span data-ttu-id="b316a-479">waarde: Hallo aantal eenheden dat u wilt dat tooadd.</span><span class="sxs-lookup"><span data-stu-id="b316a-479">value: hello number of units you want tooadd.</span></span> <span data-ttu-id="b316a-480">Kan een positieve waarde (tooget datums in toekomstige Hallo) of negatief (tooget datums in de afgelopen Hallo).</span><span class="sxs-lookup"><span data-stu-id="b316a-480">It can be positive (tooget dates in hello future) or negative (tooget dates in hello past).</span></span>
* <span data-ttu-id="b316a-481">datum: DateTime die toowhich Hallo datuminterval is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="b316a-481">date: DateTime representing date toowhich hello interval is added.</span></span>

<span data-ttu-id="b316a-482">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-482">**Example:**</span></span>  
`DateAdd("m", 3, CDate("2001-01-01"))`  
<span data-ttu-id="b316a-483">Drie maanden worden toegevoegd en retourneert een datetime-waarde die aangeeft '2001-04-01'.</span><span class="sxs-lookup"><span data-stu-id="b316a-483">Adds 3 months and returns a DateTime representing "2001-04-01".</span></span>

- - -
### <a name="datefromnum"></a><span data-ttu-id="b316a-484">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="b316a-484">DateFromNum</span></span>
<span data-ttu-id="b316a-485">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-485">**Description:**</span></span>  
<span data-ttu-id="b316a-486">Hallo DateFromNum functie converteert een waarde in de AD-datum notatie tooa DateTime-type.</span><span class="sxs-lookup"><span data-stu-id="b316a-486">hello DateFromNum function converts a value in AD’s date format tooa DateTime type.</span></span>

<span data-ttu-id="b316a-487">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-487">**Syntax:**</span></span>  
`dt DateFromNum(num value)`

<span data-ttu-id="b316a-488">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-488">**Example:**</span></span>  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
<span data-ttu-id="b316a-489">Retourneert een datetime-waarde die aangeeft 01-01-2012 23:00:00 uur</span><span class="sxs-lookup"><span data-stu-id="b316a-489">Returns a DateTime representing 2012-01-01 23:00:00</span></span>

- - -
### <a name="dncomponent"></a><span data-ttu-id="b316a-490">DNComponent</span><span class="sxs-lookup"><span data-stu-id="b316a-490">DNComponent</span></span>
<span data-ttu-id="b316a-491">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-491">**Description:**</span></span>  
<span data-ttu-id="b316a-492">Hallo DNComponent functie retourneert Hallo-waarde van een opgegeven DN-onderdeel van links.</span><span class="sxs-lookup"><span data-stu-id="b316a-492">hello DNComponent function returns hello value of a specified DN component going from left.</span></span>

<span data-ttu-id="b316a-493">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-493">**Syntax:**</span></span>  
`str DNComponent(ref dn, num ComponentNumber)`

* <span data-ttu-id="b316a-494">DN-naam: Hallo verwijzing kenmerk toointerpret</span><span class="sxs-lookup"><span data-stu-id="b316a-494">dn: hello reference attribute toointerpret</span></span>
* <span data-ttu-id="b316a-495">ComponentNumber: hello onderdeel in Hallo DN tooreturn</span><span class="sxs-lookup"><span data-stu-id="b316a-495">ComponentNumber: hello component in hello DN tooreturn</span></span>

<span data-ttu-id="b316a-496">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-496">**Example:**</span></span>  
`DNComponent([dn],1)`  
<span data-ttu-id="b316a-497">Als een DN-naam is "cn Kees, ou = =..., ' Jan wordt</span><span class="sxs-lookup"><span data-stu-id="b316a-497">If dn is "cn=Joe,ou=…," it returns Joe</span></span>

- - -
### <a name="dncomponentrev"></a><span data-ttu-id="b316a-498">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="b316a-498">DNComponentRev</span></span>
<span data-ttu-id="b316a-499">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-499">**Description:**</span></span>  
<span data-ttu-id="b316a-500">Hallo DNComponentRev functie retourneert Hallo-waarde van een opgegeven DN-onderdeel van rechts (Hallo end).</span><span class="sxs-lookup"><span data-stu-id="b316a-500">hello DNComponentRev function returns hello value of a specified DN component going from right (hello end).</span></span>

<span data-ttu-id="b316a-501">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-501">**Syntax:**</span></span>  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* <span data-ttu-id="b316a-502">DN-naam: Hallo verwijzing kenmerk toointerpret</span><span class="sxs-lookup"><span data-stu-id="b316a-502">dn: hello reference attribute toointerpret</span></span>
* <span data-ttu-id="b316a-503">ComponentNumber - hello onderdeel in Hallo DN tooreturn</span><span class="sxs-lookup"><span data-stu-id="b316a-503">ComponentNumber - hello component in hello DN tooreturn</span></span>
* <span data-ttu-id="b316a-504">-Opties: DC-alle onderdelen met negeren ' dc = "</span><span class="sxs-lookup"><span data-stu-id="b316a-504">Options: DC – Ignore all components with "dc="</span></span>

<span data-ttu-id="b316a-505">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-505">**Example:**</span></span>  
<span data-ttu-id="b316a-506">Als een DN-naam is "cn Kees, ou = Atlanta, ou = GA, ou = = US, dc = contoso, dc = com" vervolgens</span><span class="sxs-lookup"><span data-stu-id="b316a-506">If dn is "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com" then</span></span>  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
<span data-ttu-id="b316a-507">Beide retourneren ons.</span><span class="sxs-lookup"><span data-stu-id="b316a-507">Both return US.</span></span>

- - -
### <a name="error"></a><span data-ttu-id="b316a-508">Fout</span><span class="sxs-lookup"><span data-stu-id="b316a-508">Error</span></span>
<span data-ttu-id="b316a-509">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-509">**Description:**</span></span>  
<span data-ttu-id="b316a-510">Hallo functie Error is gebruikte tooreturn een aangepaste fout.</span><span class="sxs-lookup"><span data-stu-id="b316a-510">hello Error function is used tooreturn a custom error.</span></span>

<span data-ttu-id="b316a-511">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-511">**Syntax:**</span></span>  
`void Error(str ErrorMessage)`

<span data-ttu-id="b316a-512">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-512">**Example:**</span></span>  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
<span data-ttu-id="b316a-513">Als Hallo attribuut accountName niet aanwezig is, genereert u een fout op Hallo-object.</span><span class="sxs-lookup"><span data-stu-id="b316a-513">If hello attribute accountName is not present, throw an error on hello object.</span></span>

- - -
### <a name="escapedncomponent"></a><span data-ttu-id="b316a-514">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="b316a-514">EscapeDNComponent</span></span>
<span data-ttu-id="b316a-515">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-515">**Description:**</span></span>  
<span data-ttu-id="b316a-516">Hallo EscapeDNComponent functie duurt één onderdeel van een DN-naam en verlaat u zodat deze kan worden weergegeven in LDAP.</span><span class="sxs-lookup"><span data-stu-id="b316a-516">hello EscapeDNComponent function takes one component of a DN and escapes it so it can be represented in LDAP.</span></span>

<span data-ttu-id="b316a-517">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-517">**Syntax:**</span></span>  
`str EscapeDNComponent(str value)`

<span data-ttu-id="b316a-518">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-518">**Example:**</span></span>  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
<span data-ttu-id="b316a-519">Weet u zeker Hallo object kan worden gemaakt in een LDAP-adreslijst, zelfs wanneer Hallo displayName kenmerk tekens bevat die moeten worden voorafgegaan in LDAP.</span><span class="sxs-lookup"><span data-stu-id="b316a-519">Makes sure hello object can be created in an LDAP directory even if hello displayName attribute has characters that must be escaped in LDAP.</span></span>

- - -
### <a name="formatdatetime"></a><span data-ttu-id="b316a-520">formatDateTime</span><span class="sxs-lookup"><span data-stu-id="b316a-520">FormatDateTime</span></span>
<span data-ttu-id="b316a-521">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-521">**Description:**</span></span>  
<span data-ttu-id="b316a-522">Hallo FormatDateTime functie is gebruikte tooformat DateTime tooa tekenreeks met de opgegeven notatie</span><span class="sxs-lookup"><span data-stu-id="b316a-522">hello FormatDateTime function is used tooformat a DateTime tooa string with a specified format</span></span>

<span data-ttu-id="b316a-523">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-523">**Syntax:**</span></span>  
`str FormatDateTime(dt value, str format)`

* <span data-ttu-id="b316a-524">waarde: een waarde in Hallo datum-/ tijdindeling</span><span class="sxs-lookup"><span data-stu-id="b316a-524">value: a value in hello DateTime format</span></span>
* <span data-ttu-id="b316a-525">indeling: een Hallo indeling tooconvert naar type string.</span><span class="sxs-lookup"><span data-stu-id="b316a-525">format: a string representing hello format tooconvert to.</span></span>

<span data-ttu-id="b316a-526">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-526">**Remarks:**</span></span>  
<span data-ttu-id="b316a-527">Hallo mogelijke waarden voor Hallo indeling u hier vindt: [door de gebruiker gedefinieerde datum-/ tijdnotaties (functie Format)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span><span class="sxs-lookup"><span data-stu-id="b316a-527">hello possible values for hello format can be found here: [User-Defined Date/Time Formats (Format Function)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span></span>

<span data-ttu-id="b316a-528">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-528">**Example:**</span></span>  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
<span data-ttu-id="b316a-529">De resultaten in '2007-12-25'.</span><span class="sxs-lookup"><span data-stu-id="b316a-529">Results in "2007-12-25".</span></span>

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
<span data-ttu-id="b316a-530">Kan leiden tot '20140905081453.0Z'</span><span class="sxs-lookup"><span data-stu-id="b316a-530">Can result in "20140905081453.0Z"</span></span>

- - -
### <a name="guid"></a><span data-ttu-id="b316a-531">GUID</span><span class="sxs-lookup"><span data-stu-id="b316a-531">GUID</span></span>
<span data-ttu-id="b316a-532">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-532">**Description:**</span></span>  
<span data-ttu-id="b316a-533">Hallo functie GUID genereert een nieuwe willekeurige GUID</span><span class="sxs-lookup"><span data-stu-id="b316a-533">hello function GUID generates a new random GUID</span></span>

<span data-ttu-id="b316a-534">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-534">**Syntax:**</span></span>  
`str GUID()`

- - -
### <a name="iif"></a><span data-ttu-id="b316a-535">IIF</span><span class="sxs-lookup"><span data-stu-id="b316a-535">IIF</span></span>
<span data-ttu-id="b316a-536">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-536">**Description:**</span></span>  
<span data-ttu-id="b316a-537">Hallo functie IIF retourneert een van de mogelijke waarden op basis van een opgegeven voorwaarde.</span><span class="sxs-lookup"><span data-stu-id="b316a-537">hello IIF function returns one of a set of possible values based on a specified condition.</span></span>

<span data-ttu-id="b316a-538">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-538">**Syntax:**</span></span>  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* <span data-ttu-id="b316a-539">voorwaarde: een waarde of expressie die kan worden geëvalueerd tootrue of ONWAAR.</span><span class="sxs-lookup"><span data-stu-id="b316a-539">condition: any value or expression that can be evaluated tootrue or false.</span></span>
* <span data-ttu-id="b316a-540">waardeindienwaar: als Hallo voorwaarde wordt geëvalueerd tootrue, Hallo waarde geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-540">valueIfTrue: If hello condition evaluates tootrue, hello returned value.</span></span>
* <span data-ttu-id="b316a-541">WaardeAlsOnwaar: als Hallo voorwaarde wordt geëvalueerd toofalse, Hallo waarde geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-541">valueIfFalse: If hello condition evaluates toofalse, hello returned value.</span></span>

<span data-ttu-id="b316a-542">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-542">**Example:**</span></span>  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 <span data-ttu-id="b316a-543">Als Hallo gebruiker een intern is, retourneert de alias van een gebruiker met 't-' hello toegevoegd toohello begin van deze anders retourneert Hallo gebruikersalias is.</span><span class="sxs-lookup"><span data-stu-id="b316a-543">If hello user is an intern, returns hello alias of a user with "t-" added toohello beginning of it, else returns hello user’s alias as is.</span></span>

- - -
### <a name="instr"></a><span data-ttu-id="b316a-544">InStr</span><span class="sxs-lookup"><span data-stu-id="b316a-544">InStr</span></span>
<span data-ttu-id="b316a-545">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-545">**Description:**</span></span>  
<span data-ttu-id="b316a-546">Hallo functie InStr Hallo eerste exemplaar van een subtekenreeks wordt gevonden in een tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b316a-546">hello InStr function finds hello first occurrence of a substring in a string</span></span>

<span data-ttu-id="b316a-547">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-547">**Syntax:**</span></span>  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* <span data-ttu-id="b316a-548">reekscontroleren: string toobe doorzocht</span><span class="sxs-lookup"><span data-stu-id="b316a-548">stringcheck: string toobe searched</span></span>
* <span data-ttu-id="b316a-549">reeksvergelijken: string toobe gevonden</span><span class="sxs-lookup"><span data-stu-id="b316a-549">stringmatch: string toobe found</span></span>
* <span data-ttu-id="b316a-550">Start: positie toofind Hallo subtekenreeks wordt gestart</span><span class="sxs-lookup"><span data-stu-id="b316a-550">start: starting position toofind hello substring</span></span>
* <span data-ttu-id="b316a-551">Vergelijk: vbTextCompare of vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="b316a-551">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="b316a-552">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-552">**Remarks:**</span></span>  
<span data-ttu-id="b316a-553">Retourneert Hallo positie waar Hallo subtekenreeks is gevonden, of 0 als niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="b316a-553">Returns hello position where hello substring was found or 0 if not found.</span></span>

<span data-ttu-id="b316a-554">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-554">**Example:**</span></span>  
`InStr("hello quick brown fox","quick")`  
<span data-ttu-id="b316a-555">Evalues too5</span><span class="sxs-lookup"><span data-stu-id="b316a-555">Evalues too5</span></span>

`InStr("repEated","e",3,vbBinaryCompare)`  
<span data-ttu-id="b316a-556">Evalueert too7</span><span class="sxs-lookup"><span data-stu-id="b316a-556">Evaluates too7</span></span>

- - -
### <a name="instrrev"></a><span data-ttu-id="b316a-557">InStrRev</span><span class="sxs-lookup"><span data-stu-id="b316a-557">InStrRev</span></span>
<span data-ttu-id="b316a-558">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-558">**Description:**</span></span>  
<span data-ttu-id="b316a-559">Hallo functie InStrRev Hallo laatste exemplaar van een subtekenreeks wordt gevonden in een tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b316a-559">hello InStrRev function finds hello last occurrence of a substring in a string</span></span>

<span data-ttu-id="b316a-560">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-560">**Syntax:**</span></span>  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* <span data-ttu-id="b316a-561">reekscontroleren: string toobe doorzocht</span><span class="sxs-lookup"><span data-stu-id="b316a-561">stringcheck: string toobe searched</span></span>
* <span data-ttu-id="b316a-562">reeksvergelijken: string toobe gevonden</span><span class="sxs-lookup"><span data-stu-id="b316a-562">stringmatch: string toobe found</span></span>
* <span data-ttu-id="b316a-563">Start: positie toofind Hallo subtekenreeks wordt gestart</span><span class="sxs-lookup"><span data-stu-id="b316a-563">start: starting position toofind hello substring</span></span>
* <span data-ttu-id="b316a-564">Vergelijk: vbTextCompare of vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="b316a-564">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="b316a-565">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-565">**Remarks:**</span></span>  
<span data-ttu-id="b316a-566">Retourneert Hallo positie waar Hallo subtekenreeks is gevonden, of 0 als niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="b316a-566">Returns hello position where hello substring was found or 0 if not found.</span></span>

<span data-ttu-id="b316a-567">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-567">**Example:**</span></span>  
`InStrRev("abbcdbbbef","bb")`  
<span data-ttu-id="b316a-568">Retourneert 7</span><span class="sxs-lookup"><span data-stu-id="b316a-568">Returns 7</span></span>

- - -
### <a name="isbitset"></a><span data-ttu-id="b316a-569">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="b316a-569">IsBitSet</span></span>
<span data-ttu-id="b316a-570">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-570">**Description:**</span></span>  
<span data-ttu-id="b316a-571">Hallo-functie IsBitSet netwerktests als een bit is ingesteld of niet</span><span class="sxs-lookup"><span data-stu-id="b316a-571">hello function IsBitSet Tests if a bit is set or not</span></span>

<span data-ttu-id="b316a-572">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-572">**Syntax:**</span></span>  
`bool IsBitSet(num value, num flag)`

* <span data-ttu-id="b316a-573">waarde: een numerieke waarde die is evaluated.flag: een numerieke waarde die Hallo is bit toobe geëvalueerd</span><span class="sxs-lookup"><span data-stu-id="b316a-573">value: a numeric value that is evaluated.flag: a numeric value that has hello bit toobe evaluated</span></span>

<span data-ttu-id="b316a-574">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-574">**Example:**</span></span>  
`IsBitSet(&HF,4)`  
<span data-ttu-id="b316a-575">Retourneert True als omdat "4"-bit is ingesteld in Hallo hexadecimale waarde 'F'</span><span class="sxs-lookup"><span data-stu-id="b316a-575">Returns True because bit "4" is set in hello hexadecimal value "F"</span></span>

- - -
### <a name="isdate"></a><span data-ttu-id="b316a-576">IsDate</span><span class="sxs-lookup"><span data-stu-id="b316a-576">IsDate</span></span>
<span data-ttu-id="b316a-577">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-577">**Description:**</span></span>  
<span data-ttu-id="b316a-578">Als het Hallo-expressie kan worden geëvalueerd als een DateTime-type vervolgens Hallo functie IsDate tooTrue evalueert.</span><span class="sxs-lookup"><span data-stu-id="b316a-578">If hello expression can be evaluates as a DateTime type, then hello IsDate function evaluates tooTrue.</span></span>

<span data-ttu-id="b316a-579">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-579">**Syntax:**</span></span>  
`bool IsDate(var Expression)`

<span data-ttu-id="b316a-580">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-580">**Remarks:**</span></span>  
<span data-ttu-id="b316a-581">Toodetermine gebruikt als CDate() uitgevoerd worden kan.</span><span class="sxs-lookup"><span data-stu-id="b316a-581">Used toodetermine if CDate() can be successful.</span></span>

- - -
### <a name="iscert"></a><span data-ttu-id="b316a-582">IsCert</span><span class="sxs-lookup"><span data-stu-id="b316a-582">IsCert</span></span>
<span data-ttu-id="b316a-583">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-583">**Description:**</span></span>  
<span data-ttu-id="b316a-584">Retourneert waar als Hallo onbewerkte gegevens kunnen worden geserialiseerd in .NET X509Certificate2 certificaat-object.</span><span class="sxs-lookup"><span data-stu-id="b316a-584">Returns true if hello raw data can be serialized into .NET X509Certificate2 certificate object.</span></span>

<span data-ttu-id="b316a-585">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-585">**Syntax:**</span></span>  
`bool CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="b316a-586">certificateRawData: Byte matrix representatie van een X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b316a-586">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="b316a-587">Hallo-byte-matrix mag binair (DER), gecodeerd of Base64-gecodeerd x.509-gegevens.</span><span class="sxs-lookup"><span data-stu-id="b316a-587">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
- - -
### <a name="isempty"></a><span data-ttu-id="b316a-588">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="b316a-588">IsEmpty</span></span>
<span data-ttu-id="b316a-589">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-589">**Description:**</span></span>  
<span data-ttu-id="b316a-590">Als Hallo kenmerk aanwezig is in Hallo CS of MV maar tooan lege tekenreeks evalueert, evalueert de functie IsEmpty Hallo tooTrue.</span><span class="sxs-lookup"><span data-stu-id="b316a-590">If hello attribute is present in hello CS or MV but evaluates tooan empty string, then hello IsEmpty function evaluates tooTrue.</span></span>

<span data-ttu-id="b316a-591">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-591">**Syntax:**</span></span>  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a><span data-ttu-id="b316a-592">IsGuid</span><span class="sxs-lookup"><span data-stu-id="b316a-592">IsGuid</span></span>
<span data-ttu-id="b316a-593">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-593">**Description:**</span></span>  
<span data-ttu-id="b316a-594">Als het Hallo-tekenreeks kan worden geconverteerd tooa GUID, geëvalueerd Hallo IsGuid functie tootrue.</span><span class="sxs-lookup"><span data-stu-id="b316a-594">If hello string could be converted tooa GUID, then hello IsGuid function evaluated tootrue.</span></span>

<span data-ttu-id="b316a-595">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-595">**Syntax:**</span></span>  
`bool IsGuid(str GUID)`

<span data-ttu-id="b316a-596">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-596">**Remarks:**</span></span>  
<span data-ttu-id="b316a-597">Een GUID is gedefinieerd als een tekenreeks die een van deze patronen te volgen: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx of {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="b316a-597">A GUID is defined as a string following one of these patterns: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

<span data-ttu-id="b316a-598">Toodetermine gebruikt als CGuid() uitgevoerd worden kan.</span><span class="sxs-lookup"><span data-stu-id="b316a-598">Used toodetermine if CGuid() can be successful.</span></span>

<span data-ttu-id="b316a-599">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-599">**Example:**</span></span>  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
<span data-ttu-id="b316a-600">Als Hallo StrAttribute heeft een GUID-indeling, een binaire voorstelling retourneren, anders een Null geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-600">If hello StrAttribute has a GUID format, return a binary representation, otherwise return a Null.</span></span>

- - -
### <a name="isnull"></a><span data-ttu-id="b316a-601">IsNull</span><span class="sxs-lookup"><span data-stu-id="b316a-601">IsNull</span></span>
<span data-ttu-id="b316a-602">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-602">**Description:**</span></span>  
<span data-ttu-id="b316a-603">Als Hallo expressie tooNull resulteert, klikt u vervolgens de functie IsNull Hallo true ' geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-603">If hello expression evaluates tooNull, then hello IsNull function returns true.</span></span>

<span data-ttu-id="b316a-604">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-604">**Syntax:**</span></span>  
`bool IsNull(var Expression)`

<span data-ttu-id="b316a-605">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-605">**Remarks:**</span></span>  
<span data-ttu-id="b316a-606">Voor een kenmerk wordt een null-waarde uitgedrukt door Hallo afwezigheid van Hallo-kenmerk.</span><span class="sxs-lookup"><span data-stu-id="b316a-606">For an attribute, a Null is expressed by hello absence of hello attribute.</span></span>

<span data-ttu-id="b316a-607">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-607">**Example:**</span></span>  
`IsNull([displayName])`  
<span data-ttu-id="b316a-608">Retourneert True als het Hallo-kenmerk is niet aanwezig in Hallo CS of MV.</span><span class="sxs-lookup"><span data-stu-id="b316a-608">Returns True if hello attribute is not present in hello CS or MV.</span></span>

- - -
### <a name="isnullorempty"></a><span data-ttu-id="b316a-609">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="b316a-609">IsNullOrEmpty</span></span>
<span data-ttu-id="b316a-610">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-610">**Description:**</span></span>  
<span data-ttu-id="b316a-611">Als het Hallo-expressie is null of een lege tekenreeks, zijn Hallo IsNullOrEmpty functie retourneert true.</span><span class="sxs-lookup"><span data-stu-id="b316a-611">If hello expression is null or an empty string, then hello IsNullOrEmpty function returns true.</span></span>

<span data-ttu-id="b316a-612">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-612">**Syntax:**</span></span>  
`bool IsNullOrEmpty(var Expression)`

<span data-ttu-id="b316a-613">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-613">**Remarks:**</span></span>  
<span data-ttu-id="b316a-614">Voor een kenmerk, zou dit tooTrue evalueren of het Hallo-kenmerk ontbreekt of is aanwezig, maar is een lege tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b316a-614">For an attribute, this would evaluate tooTrue if hello attribute is absent or is present but is an empty string.</span></span>  
<span data-ttu-id="b316a-615">Hallo inverse van deze functie heet IsPresent.</span><span class="sxs-lookup"><span data-stu-id="b316a-615">hello inverse of this function is named IsPresent.</span></span>

<span data-ttu-id="b316a-616">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-616">**Example:**</span></span>  
`IsNullOrEmpty([displayName])`  
<span data-ttu-id="b316a-617">Retourneert True als het Hallo-kenmerk is niet aanwezig of is een lege tekenreeks in Hallo CS of MV.</span><span class="sxs-lookup"><span data-stu-id="b316a-617">Returns True if hello attribute is not present or is an empty string in hello CS or MV.</span></span>

- - -
### <a name="isnumeric"></a><span data-ttu-id="b316a-618">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="b316a-618">IsNumeric</span></span>
<span data-ttu-id="b316a-619">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-619">**Description:**</span></span>  
<span data-ttu-id="b316a-620">Hallo IsNumeric functie retourneert een Booleaanse waarde die aangeeft of een expressie kan worden geëvalueerd als een type.</span><span class="sxs-lookup"><span data-stu-id="b316a-620">hello IsNumeric function returns a Boolean value indicating whether an expression can be evaluated as a number type.</span></span>

<span data-ttu-id="b316a-621">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-621">**Syntax:**</span></span>  
`bool IsNumeric(var Expression)`

<span data-ttu-id="b316a-622">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-622">**Remarks:**</span></span>  
<span data-ttu-id="b316a-623">Toodetermine gebruikt als CNum() geslaagde tooparse Hallo expressie kan worden.</span><span class="sxs-lookup"><span data-stu-id="b316a-623">Used toodetermine if CNum() can be successful tooparse hello expression.</span></span>

- - -
### <a name="isstring"></a><span data-ttu-id="b316a-624">IsString</span><span class="sxs-lookup"><span data-stu-id="b316a-624">IsString</span></span>
<span data-ttu-id="b316a-625">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-625">**Description:**</span></span>  
<span data-ttu-id="b316a-626">Als het Hallo-expressie kan worden geëvalueerd tooa tekenreekstype, vervolgens Hallo IsString functie tooTrue evalueert.</span><span class="sxs-lookup"><span data-stu-id="b316a-626">If hello expression can be evaluated tooa string type, then hello IsString function evaluates tooTrue.</span></span>

<span data-ttu-id="b316a-627">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-627">**Syntax:**</span></span>  
`bool IsString(var expression)`

<span data-ttu-id="b316a-628">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-628">**Remarks:**</span></span>  
<span data-ttu-id="b316a-629">Toodetermine gebruikt als CStr() geslaagde tooparse Hallo expressie kan worden.</span><span class="sxs-lookup"><span data-stu-id="b316a-629">Used toodetermine if CStr() can be successful tooparse hello expression.</span></span>

- - -
### <a name="ispresent"></a><span data-ttu-id="b316a-630">IsPresent</span><span class="sxs-lookup"><span data-stu-id="b316a-630">IsPresent</span></span>
<span data-ttu-id="b316a-631">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-631">**Description:**</span></span>  
<span data-ttu-id="b316a-632">Als Hallo expressie tooa tekenreeks die niet Null is en is niet leeg resulteert, Hallo vervolgens IsPresent functie ' true ' geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-632">If hello expression evaluates tooa string that is not Null and is not empty, then hello IsPresent function returns true.</span></span>

<span data-ttu-id="b316a-633">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-633">**Syntax:**</span></span>  
`bool IsPresent(var expression)`

<span data-ttu-id="b316a-634">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-634">**Remarks:**</span></span>  
<span data-ttu-id="b316a-635">Hallo inverse van deze functie heet IsNullOrEmpty.</span><span class="sxs-lookup"><span data-stu-id="b316a-635">hello inverse of this function is named IsNullOrEmpty.</span></span>

<span data-ttu-id="b316a-636">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-636">**Example:**</span></span>  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a><span data-ttu-id="b316a-637">Item</span><span class="sxs-lookup"><span data-stu-id="b316a-637">Item</span></span>
<span data-ttu-id="b316a-638">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-638">**Description:**</span></span>  
<span data-ttu-id="b316a-639">Hallo functie Item retourneert één item van een tekenreeks/kenmerk met meerdere waarden.</span><span class="sxs-lookup"><span data-stu-id="b316a-639">hello Item function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="b316a-640">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-640">**Syntax:**</span></span>  
`var Item(mvstr attribute, num index)`

* <span data-ttu-id="b316a-641">kenmerk: kenmerk met meerdere waarden</span><span class="sxs-lookup"><span data-stu-id="b316a-641">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="b316a-642">index: item van de index tooan in Hallo meerwaardige tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b316a-642">index: index tooan item in hello multi-valued string.</span></span>

<span data-ttu-id="b316a-643">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-643">**Remarks:**</span></span>  
<span data-ttu-id="b316a-644">Hallo functie Item is nuttig in combinatie met de Hallo bevat de functie sinds de laatste functie Hallo retourneert Hallo index tooan item in een kenmerk met meerdere waarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="b316a-644">hello Item function is useful together with hello Contains function since hello latter function returns hello index tooan item in hello multi-valued attribute.</span></span>

<span data-ttu-id="b316a-645">Genereert een fout als de index valt buiten het bereik.</span><span class="sxs-lookup"><span data-stu-id="b316a-645">Throws an error if index is out of bounds.</span></span>

<span data-ttu-id="b316a-646">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-646">**Example:**</span></span>  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
<span data-ttu-id="b316a-647">Retourneert Hallo primaire e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="b316a-647">Returns hello primary email address.</span></span>

- - -
### <a name="itemornull"></a><span data-ttu-id="b316a-648">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="b316a-648">ItemOrNull</span></span>
<span data-ttu-id="b316a-649">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-649">**Description:**</span></span>  
<span data-ttu-id="b316a-650">Hallo ItemOrNull functie retourneert één item van een tekenreeks/kenmerk met meerdere waarden.</span><span class="sxs-lookup"><span data-stu-id="b316a-650">hello ItemOrNull function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="b316a-651">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-651">**Syntax:**</span></span>  
`var ItemOrNull(mvstr attribute, num index)`

* <span data-ttu-id="b316a-652">kenmerk: kenmerk met meerdere waarden</span><span class="sxs-lookup"><span data-stu-id="b316a-652">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="b316a-653">index: item van de index tooan in Hallo meerwaardige tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b316a-653">index: index tooan item in hello multi-valued string.</span></span>

<span data-ttu-id="b316a-654">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-654">**Remarks:**</span></span>  
<span data-ttu-id="b316a-655">Hallo ItemOrNull-functie is handig samen met de Hallo bevat de functie sinds de laatste functie Hallo retourneert Hallo index tooan item in een kenmerk met meerdere waarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="b316a-655">hello ItemOrNull function is useful together with hello Contains function since hello latter function returns hello index tooan item in hello multi-valued attribute.</span></span>

<span data-ttu-id="b316a-656">Als de index valt buiten het bereik, retourneert een Null-waarde.</span><span class="sxs-lookup"><span data-stu-id="b316a-656">If index is out of bounds, then returns a Null value.</span></span>

- - -
### <a name="join"></a><span data-ttu-id="b316a-657">Koppelen</span><span class="sxs-lookup"><span data-stu-id="b316a-657">Join</span></span>
<span data-ttu-id="b316a-658">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-658">**Description:**</span></span>  
<span data-ttu-id="b316a-659">Hallo Join-functie een tekenreeks met meerdere waarden en retourneert een tekenreeks met één waarde met opgegeven scheidingsteken ingevoegd tussen de verschillende items.</span><span class="sxs-lookup"><span data-stu-id="b316a-659">hello Join function takes a multi-valued string and returns a single-valued string with specified separator inserted between each item.</span></span>

<span data-ttu-id="b316a-660">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-660">**Syntax:**</span></span>  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* <span data-ttu-id="b316a-661">kenmerk: kenmerk met meerdere waarden die toobe die lid zijn van tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="b316a-661">attribute: Multi-valued attribute containing strings toobe joined.</span></span>
* <span data-ttu-id="b316a-662">scheidingsteken: een tekenreeks, gebruikte tooseparate Hallo subtekenreeksen in Hallo tekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-662">delimiter: Any string, used tooseparate hello substrings in hello returned string.</span></span> <span data-ttu-id="b316a-663">Als u dit weglaat, Hallo spatie ("") wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b316a-663">If omitted, hello space character (" ") is used.</span></span> <span data-ttu-id="b316a-664">Als scheidingsteken een tekenreeks met lengte nul is ("") of niets, alle items in de lijst Hallo worden samengevoegd met zonder scheidingstekens.</span><span class="sxs-lookup"><span data-stu-id="b316a-664">If Delimiter is a zero-length string ("") or Nothing, all items in hello list are concatenated with no delimiters.</span></span>

<span data-ttu-id="b316a-665">**Opmerkingen**</span><span class="sxs-lookup"><span data-stu-id="b316a-665">**Remarks**</span></span>  
<span data-ttu-id="b316a-666">Er is een pariteit tussen Hallo Join en Split-functies.</span><span class="sxs-lookup"><span data-stu-id="b316a-666">There is parity between hello Join and Split functions.</span></span> <span data-ttu-id="b316a-667">Hallo Join-functie wordt een matrix met tekenreeksen en koppelt deze met een scheidingsteken tekenreeks, tooreturn één tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b316a-667">hello Join function takes an array of strings and joins them using a delimiter string, tooreturn a single string.</span></span> <span data-ttu-id="b316a-668">Hallo gesplitste functie een tekenreeks en afscheiding op Hallo scheidingsteken, tooreturn een matrix met tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="b316a-668">hello Split function takes a string and separates it at hello delimiter, tooreturn an array of strings.</span></span> <span data-ttu-id="b316a-669">Een belangrijk verschil is echter dat Join tekenreeksen met een willekeurige tekenreeks scheidingsteken kunt samenvoegen, gesplitste kunt alleen tekenreeksen met behulp van een enkel teken scheidingsteken scheiden.</span><span class="sxs-lookup"><span data-stu-id="b316a-669">However, a key difference is that Join can concatenate strings with any delimiter string, Split can only separate strings using a single character delimiter.</span></span>

<span data-ttu-id="b316a-670">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-670">**Example:**</span></span>  
`Join([proxyAddresses],",")`  
<span data-ttu-id="b316a-671">Kan retourneren: 'SMTP:john.doe@contoso.com,smtp:jd@contoso.com'</span><span class="sxs-lookup"><span data-stu-id="b316a-671">Could return: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span></span>

- - -
### <a name="lcase"></a><span data-ttu-id="b316a-672">LCase</span><span class="sxs-lookup"><span data-stu-id="b316a-672">LCase</span></span>
<span data-ttu-id="b316a-673">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-673">**Description:**</span></span>  
<span data-ttu-id="b316a-674">Hallo LCase van converteert alle tekens in een tekenreeks toolower geval.</span><span class="sxs-lookup"><span data-stu-id="b316a-674">hello LCase function converts all characters in a string toolower case.</span></span>

<span data-ttu-id="b316a-675">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-675">**Syntax:**</span></span>  
`str LCase(str value)`

<span data-ttu-id="b316a-676">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-676">**Example:**</span></span>  
`LCase("TeSt")`  
<span data-ttu-id="b316a-677">Retourneert 'test'.</span><span class="sxs-lookup"><span data-stu-id="b316a-677">Returns "test".</span></span>

- - -
### <a name="left"></a><span data-ttu-id="b316a-678">Links</span><span class="sxs-lookup"><span data-stu-id="b316a-678">Left</span></span>
<span data-ttu-id="b316a-679">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-679">**Description:**</span></span>  
<span data-ttu-id="b316a-680">Hallo links functie retourneert een opgegeven aantal tekens vanaf de linkerkant Hallo van een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b316a-680">hello Left function returns a specified number of characters from hello left of a string.</span></span>

<span data-ttu-id="b316a-681">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-681">**Syntax:**</span></span>  
`str Left(str string, num NumChars)`

* <span data-ttu-id="b316a-682">tekenreeks: Hallo tekenreeks tooreturn tekens bevatten uit</span><span class="sxs-lookup"><span data-stu-id="b316a-682">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="b316a-683">NumChars: een getal dat aangeeft Hallo aantal tekens tooreturn vanaf hello (links) van een tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b316a-683">NumChars: a number identifying hello number of characters tooreturn from hello beginning (left) of string</span></span>

<span data-ttu-id="b316a-684">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-684">**Remarks:**</span></span>  
<span data-ttu-id="b316a-685">Een tekenreeks met Hallo eerste numChars tekens in de tekenreeks:</span><span class="sxs-lookup"><span data-stu-id="b316a-685">A string containing hello first numChars characters in string:</span></span>

* <span data-ttu-id="b316a-686">Als numChars = 0, lege tekenreeks retourneren.</span><span class="sxs-lookup"><span data-stu-id="b316a-686">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="b316a-687">Als numChars < 0, invoerreeks retourneren.</span><span class="sxs-lookup"><span data-stu-id="b316a-687">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="b316a-688">Als de tekenreeks is null, leeg tekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-688">If string is null, return empty string.</span></span>

<span data-ttu-id="b316a-689">Als de tekenreeks bevat minder tekens dan Hallo getal dat is opgegeven in numChars, wordt een tekenreeks identieke toostring (d.w.z., met alle tekens in parameter 1) geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-689">If string contains fewer characters than hello number specified in numChars, a string identical toostring (that is, containing all characters in parameter 1) is returned.</span></span>

<span data-ttu-id="b316a-690">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-690">**Example:**</span></span>  
`Left("John Doe", 3)`  
<span data-ttu-id="b316a-691">Retourneert 'Joh'.</span><span class="sxs-lookup"><span data-stu-id="b316a-691">Returns "Joh".</span></span>

- - -
### <a name="len"></a><span data-ttu-id="b316a-692">Len</span><span class="sxs-lookup"><span data-stu-id="b316a-692">Len</span></span>
<span data-ttu-id="b316a-693">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-693">**Description:**</span></span>  
<span data-ttu-id="b316a-694">Hallo functie Len retourneert het aantal tekens in een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b316a-694">hello Len function returns number of characters in a string.</span></span>

<span data-ttu-id="b316a-695">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-695">**Syntax:**</span></span>  
`num Len(str value)`

<span data-ttu-id="b316a-696">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-696">**Example:**</span></span>  
`Len("John Doe")`  
<span data-ttu-id="b316a-697">Retourneert 8</span><span class="sxs-lookup"><span data-stu-id="b316a-697">Returns 8</span></span>

- - -
### <a name="ltrim"></a><span data-ttu-id="b316a-698">LTrim</span><span class="sxs-lookup"><span data-stu-id="b316a-698">LTrim</span></span>
<span data-ttu-id="b316a-699">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-699">**Description:**</span></span>  
<span data-ttu-id="b316a-700">Hallo LTrim functie verwijdert voorloopspaties wit uit een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b316a-700">hello LTrim function removes leading white spaces from a string.</span></span>

<span data-ttu-id="b316a-701">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-701">**Syntax:**</span></span>  
`str LTrim(str value)`

<span data-ttu-id="b316a-702">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-702">**Example:**</span></span>  
`LTrim(" Test ")`  
<span data-ttu-id="b316a-703">Retourneert 'Test'</span><span class="sxs-lookup"><span data-stu-id="b316a-703">Returns "Test "</span></span>

- - -
### <a name="mid"></a><span data-ttu-id="b316a-704">Mid</span><span class="sxs-lookup"><span data-stu-id="b316a-704">Mid</span></span>
<span data-ttu-id="b316a-705">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-705">**Description:**</span></span>  
<span data-ttu-id="b316a-706">Hallo Mid functie retourneert een opgegeven aantal tekens van een opgegeven positie in een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b316a-706">hello Mid function returns a specified number of characters from a specified position in a string.</span></span>

<span data-ttu-id="b316a-707">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-707">**Syntax:**</span></span>  
`str Mid(str string, num start, num NumChars)`

* <span data-ttu-id="b316a-708">tekenreeks: Hallo tekenreeks tooreturn tekens bevatten uit</span><span class="sxs-lookup"><span data-stu-id="b316a-708">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="b316a-709">Start: een getal dat aangeeft Hallo beginpositie in tekenreeks tooreturn tekens bevatten uit</span><span class="sxs-lookup"><span data-stu-id="b316a-709">start: a number identifying hello starting position in string tooreturn characters from</span></span>
* <span data-ttu-id="b316a-710">NumChars: een getal dat aangeeft Hallo aantal tooreturn tekens vanaf positie in de tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b316a-710">NumChars: a number identifying hello number of characters tooreturn from position in string</span></span>

<span data-ttu-id="b316a-711">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-711">**Remarks:**</span></span>  
<span data-ttu-id="b316a-712">Retour numChars tekens vanaf positie start in de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b316a-712">Return numChars characters starting from position start in string.</span></span>  
<span data-ttu-id="b316a-713">Een tekenreeks met numChars tekens vanaf het begin van de positie in de tekenreeks:</span><span class="sxs-lookup"><span data-stu-id="b316a-713">A string containing numChars characters from position start in string:</span></span>

* <span data-ttu-id="b316a-714">Als numChars = 0, lege tekenreeks retourneren.</span><span class="sxs-lookup"><span data-stu-id="b316a-714">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="b316a-715">Als numChars < 0, invoerreeks retourneren.</span><span class="sxs-lookup"><span data-stu-id="b316a-715">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="b316a-716">Als start > Hallo lengte van tekenreeks, invoerreeks retourneren.</span><span class="sxs-lookup"><span data-stu-id="b316a-716">If start > hello length of string, return input string.</span></span>
* <span data-ttu-id="b316a-717">Als starten < = 0, invoer-tekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-717">If start <= 0, return input string.</span></span>
* <span data-ttu-id="b316a-718">Als de tekenreeks is null, leeg tekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-718">If string is null, return empty string.</span></span>

<span data-ttu-id="b316a-719">Als er niet numChar tekens worden resterend in de tekenreeks van positie-begin zoveel tekens mogelijk geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-719">If there are not numChar characters remaining in string from position start, as many characters as possible are returned.</span></span>

<span data-ttu-id="b316a-720">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-720">**Example:**</span></span>  
`Mid("John Doe", 3, 5)`  
<span data-ttu-id="b316a-721">Retourneert 'hn komen'.</span><span class="sxs-lookup"><span data-stu-id="b316a-721">Returns "hn Do".</span></span>

`Mid("John Doe", 6, 999)`  
<span data-ttu-id="b316a-722">Retourneert 'De Vries'</span><span class="sxs-lookup"><span data-stu-id="b316a-722">Returns "Doe"</span></span>

- - -
### <a name="now"></a><span data-ttu-id="b316a-723">Nu</span><span class="sxs-lookup"><span data-stu-id="b316a-723">Now</span></span>
<span data-ttu-id="b316a-724">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-724">**Description:**</span></span>  
<span data-ttu-id="b316a-725">Hallo nu retourneert functie een datum/tijd Hallo huidige datum en tijd opgeven op basis van tooyour systeemdatum en -tijd.</span><span class="sxs-lookup"><span data-stu-id="b316a-725">hello Now function returns a DateTime specifying hello current date and time, according tooyour computer's system date and time.</span></span>

<span data-ttu-id="b316a-726">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-726">**Syntax:**</span></span>  
`dt Now()`

- - -
### <a name="numfromdate"></a><span data-ttu-id="b316a-727">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="b316a-727">NumFromDate</span></span>
<span data-ttu-id="b316a-728">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-728">**Description:**</span></span>  
<span data-ttu-id="b316a-729">Hallo NumFromDate functie retourneert een datum in de datumnotatie van AD.</span><span class="sxs-lookup"><span data-stu-id="b316a-729">hello NumFromDate function returns a date in AD’s date format.</span></span>

<span data-ttu-id="b316a-730">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-730">**Syntax:**</span></span>  
`num NumFromDate(dt value)`

<span data-ttu-id="b316a-731">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-731">**Example:**</span></span>  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
<span data-ttu-id="b316a-732">Retourneert 129699324000000000</span><span class="sxs-lookup"><span data-stu-id="b316a-732">Returns 129699324000000000</span></span>

- - -
### <a name="padleft"></a><span data-ttu-id="b316a-733">PadLeft</span><span class="sxs-lookup"><span data-stu-id="b316a-733">PadLeft</span></span>
<span data-ttu-id="b316a-734">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-734">**Description:**</span></span>  
<span data-ttu-id="b316a-735">Hallo PadLeft links pad functie een tekenreeks tooa opgegeven met behulp van een opgegeven opvulteken lengte.</span><span class="sxs-lookup"><span data-stu-id="b316a-735">hello PadLeft function left-pads a string tooa specified length using a provided padding character.</span></span>

<span data-ttu-id="b316a-736">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-736">**Syntax:**</span></span>  
`str PadLeft(str string, num length, str padCharacter)`

* <span data-ttu-id="b316a-737">tekenreeks: Hallo toopad tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b316a-737">string: hello string toopad.</span></span>
* <span data-ttu-id="b316a-738">lengte: een geheel getal dat Hallo gewenste lengte van tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b316a-738">length: An integer representing hello desired length of string.</span></span>
* <span data-ttu-id="b316a-739">padCharacter: een tekenreeks die bestaat uit een enkel teken toouse als Hallo pad teken</span><span class="sxs-lookup"><span data-stu-id="b316a-739">padCharacter: A string consisting of a single character toouse as hello pad character</span></span>

<span data-ttu-id="b316a-740">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-740">**Remarks:**</span></span>

* <span data-ttu-id="b316a-741">Als het Hallo-lengte van tekenreeks is kleiner dan de lengte, vervolgens is padCharacter herhaaldelijk toegevoegde toohello begin (links) van een tekenreeks totdat er een gelijk toolength lengte.</span><span class="sxs-lookup"><span data-stu-id="b316a-741">If hello length of string is less than length, then padCharacter is repeatedly appended toohello beginning (left) of string until it has a length equal toolength.</span></span>
* <span data-ttu-id="b316a-742">padCharacter mag een spatie, maar dit kan een null-waarde niet.</span><span class="sxs-lookup"><span data-stu-id="b316a-742">PadCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="b316a-743">Als Hallo lengte van tekenreeks gelijk tooor groter dan lengte is, wordt de tekenreeks ongewijzigd geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-743">If hello length of string is equal tooor greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="b316a-744">Als de tekenreeks een lengte groter dan of gelijk zijn toolength heeft, wordt een identieke toostring tekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-744">If string has a length greater than or equal toolength, a string identical toostring is returned.</span></span>
* <span data-ttu-id="b316a-745">Als het Hallo-lengte van tekenreeks is kleiner dan de lengte, gewenst een nieuwe reeks Hallo lengte wordt geretourneerd met tekenreeks die is opgevuld met een padCharacter.</span><span class="sxs-lookup"><span data-stu-id="b316a-745">If hello length of string is less than length, then a new string of hello desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="b316a-746">Als de tekenreeks is null, Hallo een lege tekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-746">If string is null, hello function returns an empty string.</span></span>

<span data-ttu-id="b316a-747">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-747">**Example:**</span></span>  
`PadLeft("User", 10, "0")`  
<span data-ttu-id="b316a-748">Retourneert '000000User'.</span><span class="sxs-lookup"><span data-stu-id="b316a-748">Returns "000000User".</span></span>

- - -
### <a name="padright"></a><span data-ttu-id="b316a-749">PadRight</span><span class="sxs-lookup"><span data-stu-id="b316a-749">PadRight</span></span>
<span data-ttu-id="b316a-750">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-750">**Description:**</span></span>  
<span data-ttu-id="b316a-751">Hallo PadRight rechts pad functie een tekenreeks tooa opgegeven met behulp van een opgegeven opvulteken lengte.</span><span class="sxs-lookup"><span data-stu-id="b316a-751">hello PadRight function right-pads a string tooa specified length using a provided padding character.</span></span>

<span data-ttu-id="b316a-752">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-752">**Syntax:**</span></span>  
`str PadRight(str string, num length, str padCharacter)`

* <span data-ttu-id="b316a-753">tekenreeks: Hallo toopad tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b316a-753">string: hello string toopad.</span></span>
* <span data-ttu-id="b316a-754">lengte: een geheel getal dat Hallo gewenste lengte van tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b316a-754">length: An integer representing hello desired length of string.</span></span>
* <span data-ttu-id="b316a-755">padCharacter: een tekenreeks die bestaat uit een enkel teken toouse als Hallo pad teken</span><span class="sxs-lookup"><span data-stu-id="b316a-755">padCharacter: A string consisting of a single character toouse as hello pad character</span></span>

<span data-ttu-id="b316a-756">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-756">**Remarks:**</span></span>

* <span data-ttu-id="b316a-757">Als het Hallo-lengte van tekenreeks is kleiner dan de lengte, wordt padCharacter herhaaldelijk toegevoegde toohello einde (rechts) van de tekenreeks totdat er een gelijk toolength lengte.</span><span class="sxs-lookup"><span data-stu-id="b316a-757">If hello length of string is less than length, then padCharacter is repeatedly appended toohello end (right) of string until it has a length equal toolength.</span></span>
* <span data-ttu-id="b316a-758">padCharacter mag een spatie, maar dit kan een null-waarde niet.</span><span class="sxs-lookup"><span data-stu-id="b316a-758">padCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="b316a-759">Als Hallo lengte van tekenreeks gelijk tooor groter dan lengte is, wordt de tekenreeks ongewijzigd geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-759">If hello length of string is equal tooor greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="b316a-760">Als de tekenreeks een lengte groter dan of gelijk zijn toolength heeft, wordt een identieke toostring tekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-760">If string has a length greater than or equal toolength, a string identical toostring is returned.</span></span>
* <span data-ttu-id="b316a-761">Als het Hallo-lengte van tekenreeks is kleiner dan de lengte, gewenst een nieuwe reeks Hallo lengte wordt geretourneerd met tekenreeks die is opgevuld met een padCharacter.</span><span class="sxs-lookup"><span data-stu-id="b316a-761">If hello length of string is less than length, then a new string of hello desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="b316a-762">Als de tekenreeks is null, Hallo een lege tekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-762">If string is null, hello function returns an empty string.</span></span>

<span data-ttu-id="b316a-763">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-763">**Example:**</span></span>  
`PadRight("User", 10, "0")`  
<span data-ttu-id="b316a-764">Retourneert 'User000000'.</span><span class="sxs-lookup"><span data-stu-id="b316a-764">Returns "User000000".</span></span>

- - -
### <a name="pcase"></a><span data-ttu-id="b316a-765">PCase</span><span class="sxs-lookup"><span data-stu-id="b316a-765">PCase</span></span>
<span data-ttu-id="b316a-766">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-766">**Description:**</span></span>  
<span data-ttu-id="b316a-767">Hallo PCase functie converteert Hallo eerste teken van elk woord door spaties gescheiden in een tekenreeks tooupper-aanvraag en alle overige tekens worden geconverteerd toolower geval.</span><span class="sxs-lookup"><span data-stu-id="b316a-767">hello PCase function converts hello first character of each space delimited word in a string tooupper case, and all other characters are converted toolower case.</span></span>

<span data-ttu-id="b316a-768">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-768">**Syntax:**</span></span>  
`String PCase(string)`

<span data-ttu-id="b316a-769">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-769">**Remarks:**</span></span>

* <span data-ttu-id="b316a-770">Deze functie biedt momenteel geen juiste hoofdlettergebruik tooconvert een woord dat is volledig hoofdletters, zoals een acroniem.</span><span class="sxs-lookup"><span data-stu-id="b316a-770">This function does not currently provide proper casing tooconvert a word that is entirely uppercase, such as an acronym.</span></span>

<span data-ttu-id="b316a-771">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-771">**Example:**</span></span>  
`PCase("TEsT")`  
<span data-ttu-id="b316a-772">Retourneert 'Test'.</span><span class="sxs-lookup"><span data-stu-id="b316a-772">Returns "Test".</span></span>

`PCase(LCase("TEST"))`  
<span data-ttu-id="b316a-773">Retourneert 'Test'</span><span class="sxs-lookup"><span data-stu-id="b316a-773">Returns "Test"</span></span>

- - -
### <a name="randomnum"></a><span data-ttu-id="b316a-774">RandomNum</span><span class="sxs-lookup"><span data-stu-id="b316a-774">RandomNum</span></span>
<span data-ttu-id="b316a-775">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-775">**Description:**</span></span>  
<span data-ttu-id="b316a-776">Hallo RandomNum functie retourneert een willekeurig getal tussen een opgegeven interval.</span><span class="sxs-lookup"><span data-stu-id="b316a-776">hello RandomNum function returns a random number between a specified interval.</span></span>

<span data-ttu-id="b316a-777">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-777">**Syntax:**</span></span>  
`num RandomNum(num start, num end)`

* <span data-ttu-id="b316a-778">Start: een getal identificerende Hallo ondergrens van Hallo willekeurige waarde toogenerate</span><span class="sxs-lookup"><span data-stu-id="b316a-778">start: a number identifying hello lower limit of hello random value toogenerate</span></span>
* <span data-ttu-id="b316a-779">end: een getal identificerende Hallo bovengrens van Hallo willekeurige waarde toogenerate</span><span class="sxs-lookup"><span data-stu-id="b316a-779">end: a number identifying hello upper limit of hello random value toogenerate</span></span>

<span data-ttu-id="b316a-780">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-780">**Example:**</span></span>  
`Random(100,999)`  
<span data-ttu-id="b316a-781">734 kunnen worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-781">Can return 734.</span></span>

- - -
### <a name="removeduplicates"></a><span data-ttu-id="b316a-782">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="b316a-782">RemoveDuplicates</span></span>
<span data-ttu-id="b316a-783">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-783">**Description:**</span></span>  
<span data-ttu-id="b316a-784">Hallo RemoveDuplicates functie een tekenreeks met meerdere waarden en zorg ervoor dat elke waarde uniek is.</span><span class="sxs-lookup"><span data-stu-id="b316a-784">hello RemoveDuplicates function takes a multi-valued string and make sure each value is unique.</span></span>

<span data-ttu-id="b316a-785">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-785">**Syntax:**</span></span>  
`mvstr RemoveDuplicates(mvstr attribute)`

<span data-ttu-id="b316a-786">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-786">**Example:**</span></span>  
`RemoveDuplicates([proxyAddresses])`  
<span data-ttu-id="b316a-787">Retourneert een kenmerk opgeschoonde proxyAddress waar alle dubbele waarden zijn verwijderd.</span><span class="sxs-lookup"><span data-stu-id="b316a-787">Returns a sanitized proxyAddress attribute where all duplicate values have been removed.</span></span>

- - -
### <a name="replace"></a><span data-ttu-id="b316a-788">Vervangen</span><span class="sxs-lookup"><span data-stu-id="b316a-788">Replace</span></span>
<span data-ttu-id="b316a-789">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-789">**Description:**</span></span>  
<span data-ttu-id="b316a-790">Hallo functie vervangen vervangt alle instanties van een tekenreeks-tekenreeks tooanother.</span><span class="sxs-lookup"><span data-stu-id="b316a-790">hello Replace function replaces all occurrences of a string tooanother string.</span></span>

<span data-ttu-id="b316a-791">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-791">**Syntax:**</span></span>  
`str Replace(str string, str OldValue, str NewValue)`

* <span data-ttu-id="b316a-792">tekenreeks: een tekenreeks tooreplace in waarden.</span><span class="sxs-lookup"><span data-stu-id="b316a-792">string: A string tooreplace values in.</span></span>
* <span data-ttu-id="b316a-793">OldValue: Hallo tekenreeks toosearch voor en tooreplace.</span><span class="sxs-lookup"><span data-stu-id="b316a-793">OldValue: hello string toosearch for and tooreplace.</span></span>
* <span data-ttu-id="b316a-794">NewValue: Hallo tooreplace naar tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b316a-794">NewValue: hello string tooreplace to.</span></span>

<span data-ttu-id="b316a-795">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-795">**Remarks:**</span></span>  
<span data-ttu-id="b316a-796">Hallo functie herkent Hallo speciale monikers te volgen:</span><span class="sxs-lookup"><span data-stu-id="b316a-796">hello function recognizes hello following special monikers:</span></span>

* <span data-ttu-id="b316a-797">\n – nieuwe regel</span><span class="sxs-lookup"><span data-stu-id="b316a-797">\n – New Line</span></span>
* <span data-ttu-id="b316a-798">\r – regelterugloop</span><span class="sxs-lookup"><span data-stu-id="b316a-798">\r – Carriage Return</span></span>
* <span data-ttu-id="b316a-799">\t – tabblad</span><span class="sxs-lookup"><span data-stu-id="b316a-799">\t – Tab</span></span>

<span data-ttu-id="b316a-800">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-800">**Example:**</span></span>  
`Replace([address],"\r\n",", ")`  
<span data-ttu-id="b316a-801">CRLF vervangt door een komma en een spatie en kan leiden te "One Microsoft manier, Redmond, WA, VS"</span><span class="sxs-lookup"><span data-stu-id="b316a-801">Replaces CRLF with a comma and space, and could lead too"One Microsoft Way, Redmond, WA, USA"</span></span>

- - -
### <a name="replacechars"></a><span data-ttu-id="b316a-802">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="b316a-802">ReplaceChars</span></span>
<span data-ttu-id="b316a-803">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-803">**Description:**</span></span>  
<span data-ttu-id="b316a-804">Hallo ReplaceChars functie vervangt alle instanties van de tekens uit de Hallo ReplacePattern tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b316a-804">hello ReplaceChars function replaces all occurrences of characters found in hello ReplacePattern string.</span></span>

<span data-ttu-id="b316a-805">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-805">**Syntax:**</span></span>  
`str ReplaceChars(str string, str ReplacePattern)`

* <span data-ttu-id="b316a-806">tekenreeks: een tekenreeks tooreplace tekens in.</span><span class="sxs-lookup"><span data-stu-id="b316a-806">string: A string tooreplace characters in.</span></span>
* <span data-ttu-id="b316a-807">ReplacePattern: een tekenreeks met een woordenlijst met tooreplace tekens.</span><span class="sxs-lookup"><span data-stu-id="b316a-807">ReplacePattern: a string containing a dictionary with characters tooreplace.</span></span>

<span data-ttu-id="b316a-808">Hallo-indeling is {bron1}: {target1}, {bron2}: {target2}, {bronN}, {targetN} waarbij bron Hallo teken toofind en doel Hallo tekenreeks tooreplace met is.</span><span class="sxs-lookup"><span data-stu-id="b316a-808">hello format is {source1}:{target1},{source2}:{target2},{sourceN},{targetN} where source is hello character toofind and target hello string tooreplace with.</span></span>

<span data-ttu-id="b316a-809">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-809">**Remarks:**</span></span>

* <span data-ttu-id="b316a-810">Hallo-functie heeft elk exemplaar van de gedefinieerde bronnen en Hallo doelen vervangen.</span><span class="sxs-lookup"><span data-stu-id="b316a-810">hello function takes each occurrence of defined sources and replaces them with hello targets.</span></span>
* <span data-ttu-id="b316a-811">Hallo-bron moet precies één teken voor (unicode).</span><span class="sxs-lookup"><span data-stu-id="b316a-811">hello source must be exactly one (unicode) character.</span></span>
* <span data-ttu-id="b316a-812">Hallo-bron kan niet leeg zijn of langer is dan één teken (parseerfout).</span><span class="sxs-lookup"><span data-stu-id="b316a-812">hello source cannot be empty or longer than one character (parsing error).</span></span>
* <span data-ttu-id="b316a-813">Hallo doel kan meerdere tekens, bijvoorbeeld ö:oe, β:ss hebben.</span><span class="sxs-lookup"><span data-stu-id="b316a-813">hello target can have multiple characters, for example ö:oe, β:ss.</span></span>
* <span data-ttu-id="b316a-814">Hallo doel mag leeg die aangeeft dat Hallo teken moet worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="b316a-814">hello target can be empty indicating that hello character should be removed.</span></span>
* <span data-ttu-id="b316a-815">Hallo-bron is hoofdlettergevoelig en moet een exacte overeenkomst.</span><span class="sxs-lookup"><span data-stu-id="b316a-815">hello source is case-sensitive and must be an exact match.</span></span>
* <span data-ttu-id="b316a-816">Hallo, (door komma's) en: (dubbele punt) zijn gereserveerde tekens en met deze functie kan niet worden vervangen.</span><span class="sxs-lookup"><span data-stu-id="b316a-816">hello , (comma) and : (colon) are reserved characters and cannot be replaced using this function.</span></span>
* <span data-ttu-id="b316a-817">Spaties en andere witte tekens in Hallo ReplacePattern tekenreeks worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-817">Spaces and other white characters in hello ReplacePattern string are ignored.</span></span>

<span data-ttu-id="b316a-818">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-818">**Example:**</span></span>  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
<span data-ttu-id="b316a-819">Retourneert Raksmorgas</span><span class="sxs-lookup"><span data-stu-id="b316a-819">Returns Raksmorgas</span></span>

`ReplaceChars("O’Neil",%ReplaceString%)`  
<span data-ttu-id="b316a-820">Retourneert 'ONeil', één maatstreepjes Hallo is gedefinieerde toobe verwijderd.</span><span class="sxs-lookup"><span data-stu-id="b316a-820">Returns "ONeil", hello single tick is defined toobe removed.</span></span>

- - -
### <a name="right"></a><span data-ttu-id="b316a-821">Rechts</span><span class="sxs-lookup"><span data-stu-id="b316a-821">Right</span></span>
<span data-ttu-id="b316a-822">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-822">**Description:**</span></span>  
<span data-ttu-id="b316a-823">Hallo juiste functie retourneert een opgegeven aantal tekens van Hallo rechts (end) van een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b316a-823">hello Right function returns a specified number of characters from hello right (end) of a string.</span></span>

<span data-ttu-id="b316a-824">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-824">**Syntax:**</span></span>  
`str Right(str string, num NumChars)`

* <span data-ttu-id="b316a-825">tekenreeks: Hallo tekenreeks tooreturn tekens bevatten uit</span><span class="sxs-lookup"><span data-stu-id="b316a-825">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="b316a-826">NumChars: een getal dat aangeeft Hallo aantal tekens tooreturn van Hallo einde (rechts) van de tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b316a-826">NumChars: a number identifying hello number of characters tooreturn from hello end (right) of string</span></span>

<span data-ttu-id="b316a-827">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-827">**Remarks:**</span></span>  
<span data-ttu-id="b316a-828">NumChars tekens geretourneerd vanaf de laatste positie Hallo van een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b316a-828">NumChars characters are returned from hello last position of string.</span></span>

<span data-ttu-id="b316a-829">Een tekenreeks met Hallo laatste numChars tekens in de tekenreeks:</span><span class="sxs-lookup"><span data-stu-id="b316a-829">A string containing hello last numChars characters in string:</span></span>

* <span data-ttu-id="b316a-830">Als numChars = 0, lege tekenreeks retourneren.</span><span class="sxs-lookup"><span data-stu-id="b316a-830">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="b316a-831">Als numChars < 0, invoerreeks retourneren.</span><span class="sxs-lookup"><span data-stu-id="b316a-831">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="b316a-832">Als de tekenreeks is null, leeg tekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-832">If string is null, return empty string.</span></span>

<span data-ttu-id="b316a-833">Als de tekenreeks bevat minder tekens dan het aantal opgegeven in NumChars hello, wordt een identieke toostring tekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-833">If string contains fewer characters than hello number specified in NumChars, a string identical toostring is returned.</span></span>

<span data-ttu-id="b316a-834">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-834">**Example:**</span></span>  
`Right("John Doe", 3)`  
<span data-ttu-id="b316a-835">Retourneert 'De Vries'.</span><span class="sxs-lookup"><span data-stu-id="b316a-835">Returns "Doe".</span></span>

- - -
### <a name="rtrim"></a><span data-ttu-id="b316a-836">RTrim</span><span class="sxs-lookup"><span data-stu-id="b316a-836">RTrim</span></span>
<span data-ttu-id="b316a-837">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-837">**Description:**</span></span>  
<span data-ttu-id="b316a-838">Hallo functie RTrim verwijdert de afsluitende spaties uit een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b316a-838">hello RTrim function removes trailing white spaces from a string.</span></span>

<span data-ttu-id="b316a-839">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-839">**Syntax:**</span></span>  
`str RTrim(str value)`

<span data-ttu-id="b316a-840">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-840">**Example:**</span></span>  
`RTrim(" Test ")`  
<span data-ttu-id="b316a-841">Retourneert 'Test'.</span><span class="sxs-lookup"><span data-stu-id="b316a-841">Returns " Test".</span></span>

- - -
### <a name="select"></a><span data-ttu-id="b316a-842">Selecteer</span><span class="sxs-lookup"><span data-stu-id="b316a-842">Select</span></span>
<span data-ttu-id="b316a-843">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-843">**Description:**</span></span>  
<span data-ttu-id="b316a-844">Proces alle waarden in een met meerdere waarden kenmerk (of uitvoer van een expressie) op basis van functie die is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="b316a-844">Process all values in a multi-valued attribute (or output of an expression) based on function specified.</span></span>

<span data-ttu-id="b316a-845">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-845">**Syntax:**</span></span>  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* <span data-ttu-id="b316a-846">item: Hiermee geeft u een element in een kenmerk met meerdere waarden Hallo</span><span class="sxs-lookup"><span data-stu-id="b316a-846">item: Represents an element in hello multi-valued attribute</span></span>
* <span data-ttu-id="b316a-847">kenmerk: Hallo een kenmerk met meerdere waarden</span><span class="sxs-lookup"><span data-stu-id="b316a-847">attribute: hello multi-valued attribute</span></span>
* <span data-ttu-id="b316a-848">expressie: een expressie die een verzameling waarden retourneert</span><span class="sxs-lookup"><span data-stu-id="b316a-848">expression: an expression that returns a collection of values</span></span>
* <span data-ttu-id="b316a-849">voorwaarde: de functie waarmee een item in het Hallo-kenmerk kan worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="b316a-849">condition: any function that can process an item in hello attribute</span></span>

<span data-ttu-id="b316a-850">**Voorbeelden:**</span><span class="sxs-lookup"><span data-stu-id="b316a-850">**Examples:**</span></span>  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
<span data-ttu-id="b316a-851">Alle Hallo-waarden in Hallo kenmerk met meerdere waarden otherPhone retourneren nadat afbreekstreepjes (-) zijn verwijderd.</span><span class="sxs-lookup"><span data-stu-id="b316a-851">Return all hello values in hello multi-valued attribute otherPhone after hyphens (-) have been removed.</span></span>

- - -
### <a name="split"></a><span data-ttu-id="b316a-852">Splitsen</span><span class="sxs-lookup"><span data-stu-id="b316a-852">Split</span></span>
<span data-ttu-id="b316a-853">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-853">**Description:**</span></span>  
<span data-ttu-id="b316a-854">Hallo gesplitste functie een tekenreeks die van elkaar gescheiden door een scheidingsteken en maakt het een tekenreeks met meerdere waarden.</span><span class="sxs-lookup"><span data-stu-id="b316a-854">hello Split function takes a string separated with a delimiter and makes it a multi-valued string.</span></span>

<span data-ttu-id="b316a-855">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-855">**Syntax:**</span></span>  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* <span data-ttu-id="b316a-856">waarde: string met een scheidingsteken teken tooseparate Hallo.</span><span class="sxs-lookup"><span data-stu-id="b316a-856">value: hello string with a delimiter character tooseparate.</span></span>
* <span data-ttu-id="b316a-857">scheidingsteken: één teken toobe als scheidingsteken Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b316a-857">delimiter: single character toobe used as hello delimiter.</span></span>
* <span data-ttu-id="b316a-858">limiet: maximum aantal waarden die kunnen worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-858">limit: maximum number of values that can return.</span></span>

<span data-ttu-id="b316a-859">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-859">**Example:**</span></span>  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
<span data-ttu-id="b316a-860">Retourneert een tekenreeks met meerdere waarden met 2 elementen nuttig voor Hallo proxyAddress-kenmerk.</span><span class="sxs-lookup"><span data-stu-id="b316a-860">Returns a multi-valued string with 2 elements useful for hello proxyAddress attribute.</span></span>

- - -
### <a name="stringfromguid"></a><span data-ttu-id="b316a-861">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="b316a-861">StringFromGuid</span></span>
<span data-ttu-id="b316a-862">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-862">**Description:**</span></span>  
<span data-ttu-id="b316a-863">Hallo functie StringFromGuid neemt een binaire GUID en converteert deze tooa</span><span class="sxs-lookup"><span data-stu-id="b316a-863">hello StringFromGuid function takes a binary GUID and converts it tooa string</span></span>

<span data-ttu-id="b316a-864">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-864">**Syntax:**</span></span>  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a><span data-ttu-id="b316a-865">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="b316a-865">StringFromSid</span></span>
<span data-ttu-id="b316a-866">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-866">**Description:**</span></span>  
<span data-ttu-id="b316a-867">Hallo StringFromSid functie converteert een bytematrix die een beveiligings-id tooa tekenreeks bevat.</span><span class="sxs-lookup"><span data-stu-id="b316a-867">hello StringFromSid function converts a byte array containing a security identifier tooa string.</span></span>

<span data-ttu-id="b316a-868">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-868">**Syntax:**</span></span>  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a><span data-ttu-id="b316a-869">Switch</span><span class="sxs-lookup"><span data-stu-id="b316a-869">Switch</span></span>
<span data-ttu-id="b316a-870">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-870">**Description:**</span></span>  
<span data-ttu-id="b316a-871">de functie Switch Hallo is gebruikte tooreturn één waarde op basis van de geëvalueerde voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="b316a-871">hello Switch function is used tooreturn a single value based on evaluated conditions.</span></span>

<span data-ttu-id="b316a-872">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-872">**Syntax:**</span></span>  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* <span data-ttu-id="b316a-873">expr: gewenste tooevaluate Variant-expressie.</span><span class="sxs-lookup"><span data-stu-id="b316a-873">expr: Variant expression you want tooevaluate.</span></span>
* <span data-ttu-id="b316a-874">waarde: waarde toobe geretourneerd als de bijbehorende expressie Hallo waar is.</span><span class="sxs-lookup"><span data-stu-id="b316a-874">value: Value toobe returned if hello corresponding expression is True.</span></span>

<span data-ttu-id="b316a-875">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-875">**Remarks:**</span></span>  
<span data-ttu-id="b316a-876">Hallo Switch functieargument bestaat uit combinaties van expressies en waarden.</span><span class="sxs-lookup"><span data-stu-id="b316a-876">hello Switch function argument list consists of pairs of expressions and values.</span></span> <span data-ttu-id="b316a-877">Hallo-expressies worden van links tooright geëvalueerd en Hallo-waarde die is gekoppeld aan Hallo eerste expressie tooevaluate tooTrue geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-877">hello expressions are evaluated from left tooright, and hello value associated with hello first expression tooevaluate tooTrue is returned.</span></span> <span data-ttu-id="b316a-878">Als het Hallo-onderdelen zijn niet correct is gekoppeld, wordt een runtime fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="b316a-878">If hello parts aren't properly paired, a run-time error occurs.</span></span>

<span data-ttu-id="b316a-879">Als expr1 True is, retourneert Switch value1.</span><span class="sxs-lookup"><span data-stu-id="b316a-879">For example, if expr1 is True, Switch returns value1.</span></span> <span data-ttu-id="b316a-880">Als expr-1 ingesteld op False is, maar expr 2 True is, retourneert Switch waarde 2, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="b316a-880">If expr-1 is False, but expr-2 is True, Switch returns value-2, and so on.</span></span>

<span data-ttu-id="b316a-881">Levert een switch als:</span><span class="sxs-lookup"><span data-stu-id="b316a-881">Switch returns a Nothing if:</span></span>

* <span data-ttu-id="b316a-882">Geen van de expressies Hallo is True.</span><span class="sxs-lookup"><span data-stu-id="b316a-882">None of hello expressions are True.</span></span>
* <span data-ttu-id="b316a-883">Hallo eerste ' True '-expressie heeft een overeenkomende waarde die Null is.</span><span class="sxs-lookup"><span data-stu-id="b316a-883">hello first True expression has a corresponding value that is Null.</span></span>

<span data-ttu-id="b316a-884">Switch evalueert alle expressies, ook al wordt slechts één van beide geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-884">Switch evaluates all expressions, even though it returns only one of them.</span></span> <span data-ttu-id="b316a-885">Daarom moet u neveneffecten gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-885">For this reason, you should watch for undesirable side effects.</span></span> <span data-ttu-id="b316a-886">Als Hallo evaluatie van een expressie in een deling door nul-fout resulteert, wordt bijvoorbeeld een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="b316a-886">For example, if hello evaluation of any expression results in a division by zero error, an error occurs.</span></span>

<span data-ttu-id="b316a-887">Waarde kan ook worden Hallo FOUTFUNCTIE, die een aangepaste tekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-887">Value can also be hello Error function, which would return a custom string.</span></span>

<span data-ttu-id="b316a-888">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-888">**Example:**</span></span>  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
<span data-ttu-id="b316a-889">Hallo taal gesproken in sommige steden retourneert, anders wordt een fout geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-889">Returns hello language spoken in some major cities, otherwise returns an Error.</span></span>

- - -
### <a name="trim"></a><span data-ttu-id="b316a-890">Trim</span><span class="sxs-lookup"><span data-stu-id="b316a-890">Trim</span></span>
<span data-ttu-id="b316a-891">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-891">**Description:**</span></span>  
<span data-ttu-id="b316a-892">Hallo Trim functie verwijdert voorloopspaties en afsluitende spaties uit een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b316a-892">hello Trim function removes leading and trailing white spaces from a string.</span></span>

<span data-ttu-id="b316a-893">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-893">**Syntax:**</span></span>  
`str Trim(str value)`  

<span data-ttu-id="b316a-894">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-894">**Example:**</span></span>  
`Trim(" Test ")`  
<span data-ttu-id="b316a-895">Retourneert 'Test'.</span><span class="sxs-lookup"><span data-stu-id="b316a-895">Returns "Test".</span></span>

`Trim([proxyAddresses])`  
<span data-ttu-id="b316a-896">Verwijdert voorloopspaties en afsluitende spaties voor elke waarde in Hallo proxyAddress-kenmerk.</span><span class="sxs-lookup"><span data-stu-id="b316a-896">Removes leading and trailing spaces for each value in hello proxyAddress attribute.</span></span>

- - -
### <a name="ucase"></a><span data-ttu-id="b316a-897">UCase</span><span class="sxs-lookup"><span data-stu-id="b316a-897">UCase</span></span>
<span data-ttu-id="b316a-898">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-898">**Description:**</span></span>  
<span data-ttu-id="b316a-899">Hallo UCase functie converteert alle tekens in een tekenreeks tooupper geval.</span><span class="sxs-lookup"><span data-stu-id="b316a-899">hello UCase function converts all characters in a string tooupper case.</span></span>

<span data-ttu-id="b316a-900">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-900">**Syntax:**</span></span>  
`str UCase(str string)`

<span data-ttu-id="b316a-901">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-901">**Example:**</span></span>  
`UCase("TeSt")`  
<span data-ttu-id="b316a-902">Retourneert 'TEST'.</span><span class="sxs-lookup"><span data-stu-id="b316a-902">Returns "TEST".</span></span>

- - -
### <a name="where"></a><span data-ttu-id="b316a-903">waar</span><span class="sxs-lookup"><span data-stu-id="b316a-903">Where</span></span>

<span data-ttu-id="b316a-904">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-904">**Description:**</span></span>  
<span data-ttu-id="b316a-905">Retourneert een subset van de waarden van een met meerdere waarden kenmerk (of dezelfde uitvoer van een expressie) op basis van specifieke voorwaarde.</span><span class="sxs-lookup"><span data-stu-id="b316a-905">Returns a subset of values from a multi-valued attribute (or output of an expression) based on specific condition.</span></span>

<span data-ttu-id="b316a-906">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-906">**Syntax:**</span></span>  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* <span data-ttu-id="b316a-907">item: Hiermee geeft u een element in een kenmerk met meerdere waarden Hallo</span><span class="sxs-lookup"><span data-stu-id="b316a-907">item: Represents an element in hello multi-valued attribute</span></span>
* <span data-ttu-id="b316a-908">kenmerk: Hallo een kenmerk met meerdere waarden</span><span class="sxs-lookup"><span data-stu-id="b316a-908">attribute: hello multi-valued attribute</span></span>
* <span data-ttu-id="b316a-909">voorwaarde: een expressie die kan worden geëvalueerd tootrue of ONWAAR</span><span class="sxs-lookup"><span data-stu-id="b316a-909">condition: any expression that can be evaluated tootrue or false</span></span>
* <span data-ttu-id="b316a-910">expressie: een expressie die een verzameling waarden retourneert</span><span class="sxs-lookup"><span data-stu-id="b316a-910">expression: an expression that returns a collection of values</span></span>

<span data-ttu-id="b316a-911">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-911">**Example:**</span></span>  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
<span data-ttu-id="b316a-912">Hallo certificaat waarden retourneren in Hallo kenmerk met meerdere waarden userCertificate die niet zijn verlopen.</span><span class="sxs-lookup"><span data-stu-id="b316a-912">Return hello certificate values in hello multi-valued attribute userCertificate which aren’t expired.</span></span>

- - -
### <a name="with"></a><span data-ttu-id="b316a-913">met</span><span class="sxs-lookup"><span data-stu-id="b316a-913">With</span></span>
<span data-ttu-id="b316a-914">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-914">**Description:**</span></span>  
<span data-ttu-id="b316a-915">Hallo met de functie biedt een manier toosimplify een samengestelde expressie met behulp van een variabele toorepresent een subexpressie die één of meerdere keren in Hallo complexe expressie.</span><span class="sxs-lookup"><span data-stu-id="b316a-915">hello With function provides a way toosimplify a complex expression by using a variable toorepresent a subexpression which appears one or more times in hello complex expression.</span></span>

<span data-ttu-id="b316a-916">**Syntaxis:**
`With(var variable, exp subExpression, exp complexExpression)`</span><span class="sxs-lookup"><span data-stu-id="b316a-916">**Syntax:**
`With(var variable, exp subExpression, exp complexExpression)`</span></span>  
* <span data-ttu-id="b316a-917">variabele: vertegenwoordigt Hallo subexpressie.</span><span class="sxs-lookup"><span data-stu-id="b316a-917">variable: Represents hello subexpression.</span></span>
* <span data-ttu-id="b316a-918">Subexpressie: subexpressie dat wordt vertegenwoordigd door de variabele.</span><span class="sxs-lookup"><span data-stu-id="b316a-918">subExpression: subexpression represented by variable.</span></span>
* <span data-ttu-id="b316a-919">complexExpression: een complexe expressie.</span><span class="sxs-lookup"><span data-stu-id="b316a-919">complexExpression: A complex expression.</span></span>

<span data-ttu-id="b316a-920">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-920">**Example:**</span></span>  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
<span data-ttu-id="b316a-921">Is functioneel equivalent met:</span><span class="sxs-lookup"><span data-stu-id="b316a-921">Is functionally equivalent to:</span></span>  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
<span data-ttu-id="b316a-922">Die alleen niet-verlopen certificaat waarden resulteert in Hallo userCertificate kenmerk.</span><span class="sxs-lookup"><span data-stu-id="b316a-922">Which returns only unexpired certificate values in hello userCertificate attribute.</span></span>


- - -
### <a name="word"></a><span data-ttu-id="b316a-923">Word</span><span class="sxs-lookup"><span data-stu-id="b316a-923">Word</span></span>
<span data-ttu-id="b316a-924">**Beschrijving:**</span><span class="sxs-lookup"><span data-stu-id="b316a-924">**Description:**</span></span>  
<span data-ttu-id="b316a-925">Hallo Word functie retourneert een woord dat voorkomt in een tekenreeks, op basis van parameters Hallo scheidingstekens toouse en Hallo word nummer tooreturn beschrijven.</span><span class="sxs-lookup"><span data-stu-id="b316a-925">hello Word function returns a word contained within a string, based on parameters describing hello delimiters toouse and hello word number tooreturn.</span></span>

<span data-ttu-id="b316a-926">**Syntaxis:**</span><span class="sxs-lookup"><span data-stu-id="b316a-926">**Syntax:**</span></span>  
`str Word(str string, num WordNumber, str delimiters)`

* <span data-ttu-id="b316a-927">tekenreeks: Hallo tekenreeks tooreturn een woord uit.</span><span class="sxs-lookup"><span data-stu-id="b316a-927">string: hello string tooreturn a word from.</span></span>
* <span data-ttu-id="b316a-928">WordNumber: een getal dat aangeeft welke word-nummer moet worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-928">WordNumber: a number identifying which word number should return.</span></span>
* <span data-ttu-id="b316a-929">scheidingstekens: een tekenreeks voor Hallo delimiter(s) die gebruikt tooidentify woorden worden moet</span><span class="sxs-lookup"><span data-stu-id="b316a-929">delimiters: a string representing hello delimiter(s) that should be used tooidentify words</span></span>

<span data-ttu-id="b316a-930">**Opmerkingen:**</span><span class="sxs-lookup"><span data-stu-id="b316a-930">**Remarks:**</span></span>  
<span data-ttu-id="b316a-931">Elke reeks tekens in tekenreeks gescheiden door Hallo een Hallo tekens scheidingstekens worden aangeduid als woorden:</span><span class="sxs-lookup"><span data-stu-id="b316a-931">Each string of characters in string separated by hello one of hello characters in delimiters are identified as words:</span></span>

* <span data-ttu-id="b316a-932">Als < 1 nummer, het resultaat een lege tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b316a-932">If number < 1, returns empty string.</span></span>
* <span data-ttu-id="b316a-933">Als tekenreeks null is, retourneert lege tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b316a-933">If string is null, returns empty string.</span></span>

<span data-ttu-id="b316a-934">Als de tekenreeks bevat minder dan het aantal woorden of tekenreeks bevat geen woorden geïdentificeerd door scheidingstekens, wordt een lege tekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b316a-934">If string contains less than number words, or string does not contain any words identified by delimiters, an empty string is returned.</span></span>

<span data-ttu-id="b316a-935">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="b316a-935">**Example:**</span></span>  
`Word("hello quick brown fox",3," ")`  
<span data-ttu-id="b316a-936">Retourneert 'bruine'</span><span class="sxs-lookup"><span data-stu-id="b316a-936">Returns "brown"</span></span>

`Word("This,string!has&many separators",3,",!&#")`  
<span data-ttu-id="b316a-937">Retourneert 'is'</span><span class="sxs-lookup"><span data-stu-id="b316a-937">Would return "has"</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b316a-938">Aanvullende resources</span><span class="sxs-lookup"><span data-stu-id="b316a-938">Additional Resources</span></span>
* [<span data-ttu-id="b316a-939">Inzicht in expressies declaratieve inrichting</span><span class="sxs-lookup"><span data-stu-id="b316a-939">Understanding Declarative Provisioning Expressions</span></span>](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [<span data-ttu-id="b316a-940">Azure AD Connect-synchronisatie: Synchronisatie-opties voor aanpassen</span><span class="sxs-lookup"><span data-stu-id="b316a-940">Azure AD Connect Sync: Customizing Synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="b316a-941">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b316a-941">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
