---
title: aaaKey kluis .NET 2.x API Release-opmerkingen | Microsoft Docs
description: .NET-ontwikkelaars wilt deze toocode API voor Azure Sleutelkluis gebruiken
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
editor: bruceper
ms.assetid: 1cccf21b-5be9-4a49-8145-483b695124ba
ms.service: key-vault
ms.devlang: CSharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/02/2017
ms.author: bruceper
ms.openlocfilehash: d95b84cf73c155f117f37e93893f27b02a75855c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a><span data-ttu-id="ed3d4-103">Azure Sleutelkluis .NET 2.0 - Release-opmerkingen en Migratiehandleiding</span><span class="sxs-lookup"><span data-stu-id="ed3d4-103">Azure Key Vault .NET 2.0 - Release Notes and Migration Guide</span></span>
<span data-ttu-id="ed3d4-104">Hallo volgende opmerkingen en richtlijnen zijn voor ontwikkelaars die werken met Azure Key Vault .NET / C#-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="ed3d4-104">hello following notes and guidance are for developers working with Azure Key Vault .NET / C# library.</span></span> <span data-ttu-id="ed3d4-105">In de overgangsfase Hallo van Hallo 1.0 versie 2.0 toohello versie, een aantal updates zijn aangebracht die wordt vereist migratie werk in uw code om toobenefit van Hallo functionele verbeteringen en toevoegingen, zoals functies **Sleutelkluis certificaten** ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="ed3d4-105">In hello transition from hello 1.0 version toohello 2.0 version, a number of updates have been made that will require migration work in your code in order for you toobenefit from hello functional improvements and feature additions such as **Key Vault certificates** support.</span></span>

## <a name="key-vault-certificates"></a><span data-ttu-id="ed3d4-106">Sleutelkluis-certificaten</span><span class="sxs-lookup"><span data-stu-id="ed3d4-106">Key Vault certificates</span></span>

<span data-ttu-id="ed3d4-107">Sleutelkluis certificaten ondersteuning biedt voor het beheren van uw x509 certificaten en Hallo volgende gedrag:</span><span class="sxs-lookup"><span data-stu-id="ed3d4-107">Key Vault certificates support provides for management of your x509 certificates and hello following behaviors:</span></span>  

* <span data-ttu-id="ed3d4-108">Kan een certificaat eigenaar toocreate een certificaat via een proces voor het maken van Sleutelkluis of Hallo importeren van een bestaand certificaat.</span><span class="sxs-lookup"><span data-stu-id="ed3d4-108">Allows a certificate owner toocreate a certificate through a Key Vault creation process or through hello import of an existing certificate.</span></span> <span data-ttu-id="ed3d4-109">Dit omvat zowel zelfondertekend en de certificeringsinstantie die certificaten worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="ed3d4-109">This includes both self-signed and Certificate Authority generated certificates.</span></span>
* <span data-ttu-id="ed3d4-110">Kan de eigenaar van een Sleutelkluis certificaat tooimplement veilige opslag en beheer van X509 certificaten zonder interactie met privésleutelmateriaal.</span><span class="sxs-lookup"><span data-stu-id="ed3d4-110">Allows a Key Vault certificate owner tooimplement secure storage and management of X509 certificates without interaction with private key material.</span></span>  
* <span data-ttu-id="ed3d4-111">Hiermee kunt een certificaat eigenaar toocreate een beleid dat wordt verwezen Sleutelkluis toomanage Hallo levenscyclus van een certificaat.</span><span class="sxs-lookup"><span data-stu-id="ed3d4-111">Allows a certificate owner toocreate a policy that directs Key Vault toomanage hello life-cycle of a certificate.</span></span>  
* <span data-ttu-id="ed3d4-112">Kan certificaat eigenaars tooprovide contactgegevens voor melding over de levenscyclus van gebeurtenissen van verlopen en verlenging van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="ed3d4-112">Allows certificate owners tooprovide contact information for notification about life-cycle events of expiration and renewal of certificate.</span></span>  
* <span data-ttu-id="ed3d4-113">Ondersteunt automatische vernieuwing met geselecteerde verleners - Sleutelkluis partner X509 providers van het certificaat / certificeringsinstanties.</span><span class="sxs-lookup"><span data-stu-id="ed3d4-113">Supports automatic renewal with selected issuers - Key Vault partner X509 certificate providers / certificate authorities.</span></span>
  
  * <span data-ttu-id="ed3d4-114">Opmerking: providers/instanties niet in de samenwerking ook zijn toegestaan, maar biedt geen ondersteuning voor functie voor automatisch vernieuwen Hallo.</span><span class="sxs-lookup"><span data-stu-id="ed3d4-114">NOTE - Non-partnered providers/authorities are also allowed but, will not support hello auto renewal feature.</span></span>

## <a name="net-support"></a><span data-ttu-id="ed3d4-115">Ondersteuning voor .NET</span><span class="sxs-lookup"><span data-stu-id="ed3d4-115">.NET support</span></span>

* <span data-ttu-id="ed3d4-116">**.NET 4.0** wordt niet ondersteund door Hallo 2.0-versie van Azure Sleutelkluis .NET Hallo / C#-bibliotheek</span><span class="sxs-lookup"><span data-stu-id="ed3d4-116">**.NET 4.0** is not supported by hello 2.0 version of hello Azure Key Vault .NET/C# library</span></span>
* <span data-ttu-id="ed3d4-117">**.NET core** wordt ondersteund door de versie 2.0 Hallo Hallo Azure Key Vault .NET / C#-bibliotheek</span><span class="sxs-lookup"><span data-stu-id="ed3d4-117">**.NET Core** is supported by hello 2.0 version of hello Azure Key Vault .NET/C# library</span></span>

## <a name="namespaces"></a><span data-ttu-id="ed3d4-118">Naamruimten</span><span class="sxs-lookup"><span data-stu-id="ed3d4-118">Namespaces</span></span>

* <span data-ttu-id="ed3d4-119">naamruimte voor Hallo **modellen** wordt gewijzigd van **Microsoft.Azure.KeyVault** te**Microsoft.Azure.KeyVault.Models**.</span><span class="sxs-lookup"><span data-stu-id="ed3d4-119">hello namespace for **models** is changed from **Microsoft.Azure.KeyVault** too**Microsoft.Azure.KeyVault.Models**.</span></span>
* <span data-ttu-id="ed3d4-120">Hallo **Microsoft.Azure.KeyVault.Internal** naamruimte is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="ed3d4-120">hello **Microsoft.Azure.KeyVault.Internal** namespace is dropped.</span></span>
* <span data-ttu-id="ed3d4-121">Hello Azure SDK-afhankelijkheden naamruimte zijn gewijzigd van **Hyak.Common** en **Hyak.Common.Internals** te**Microsoft.Rest** en  **Microsoft.Rest.Serialization**</span><span class="sxs-lookup"><span data-stu-id="ed3d4-121">hello Azure SDK dependencies namespace are changed from **Hyak.Common** and **Hyak.Common.Internals** too**Microsoft.Rest** and **Microsoft.Rest.Serialization**</span></span>

## <a name="type-changes"></a><span data-ttu-id="ed3d4-122">Wijzigingen van het type</span><span class="sxs-lookup"><span data-stu-id="ed3d4-122">Type changes</span></span>

* <span data-ttu-id="ed3d4-123">*Geheim* gewijzigd te*SecretBundle*</span><span class="sxs-lookup"><span data-stu-id="ed3d4-123">*Secret* changed too*SecretBundle*</span></span>
* <span data-ttu-id="ed3d4-124">*Woordenlijst* gewijzigd te*IDictionary*</span><span class="sxs-lookup"><span data-stu-id="ed3d4-124">*Dictionary* changed too*IDictionary*</span></span>
* <span data-ttu-id="ed3d4-125">*Lijst<T>, string []* gewijzigd te*IList<T>*</span><span class="sxs-lookup"><span data-stu-id="ed3d4-125">*List<T>, string []* changed too*IList<T>*</span></span>
* <span data-ttu-id="ed3d4-126">*NextList* gewijzigd te *NextPageLink*</span><span class="sxs-lookup"><span data-stu-id="ed3d4-126">*NextList* changed too *NextPageLink*</span></span>

## <a name="return-types"></a><span data-ttu-id="ed3d4-127">Retourtypen</span><span class="sxs-lookup"><span data-stu-id="ed3d4-127">Return types</span></span>

* <span data-ttu-id="ed3d4-128">**KeyList** en **SecretList** retourneert *IPage<T>*  in plaats van *ListKeysResponseMessage*</span><span class="sxs-lookup"><span data-stu-id="ed3d4-128">**KeyList** and **SecretList** will return *IPage<T>* instead of *ListKeysResponseMessage*</span></span>
* <span data-ttu-id="ed3d4-129">Hallo gegenereerd **BackupKeyAsync** retourneert *BackupKeyResult* die bevat *waarde* (back-up van blob).</span><span class="sxs-lookup"><span data-stu-id="ed3d4-129">hello generated **BackupKeyAsync** will return *BackupKeyResult* which contains *Value* (back-up blob).</span></span> <span data-ttu-id="ed3d4-130">Methode is voordat Hallo verpakte en terugkerende enige Hallo-waarde.</span><span class="sxs-lookup"><span data-stu-id="ed3d4-130">Before hello method was wrapped and returning only hello value.</span></span>

## <a name="exceptions"></a><span data-ttu-id="ed3d4-131">Uitzonderingen</span><span class="sxs-lookup"><span data-stu-id="ed3d4-131">Exceptions</span></span>

* <span data-ttu-id="ed3d4-132">*KeyVaultClientException* wordt gewijzigd te*KeyVaultErrorException*</span><span class="sxs-lookup"><span data-stu-id="ed3d4-132">*KeyVaultClientException* is changed too*KeyVaultErrorException*</span></span>
* <span data-ttu-id="ed3d4-133">Hallo-servicefout wordt gewijzigd van *uitzondering. Fout* te*uitzondering. Body.Error.Message*.</span><span class="sxs-lookup"><span data-stu-id="ed3d4-133">hello service error is changed from *exception.Error* too*exception.Body.Error.Message*.</span></span>
* <span data-ttu-id="ed3d4-134">Aanvullende informatie verwijderd uit de foutbericht Hallo voor **[JsonExtensionData]**.</span><span class="sxs-lookup"><span data-stu-id="ed3d4-134">Removed additional info from hello error message for **[JsonExtensionData]**.</span></span>

## <a name="constructors"></a><span data-ttu-id="ed3d4-135">Constructors</span><span class="sxs-lookup"><span data-stu-id="ed3d4-135">Constructors</span></span>

* <span data-ttu-id="ed3d4-136">In plaats van het accepteren van een *HttpClient* als constructor-argument accepteert Hallo constructor alleen *HttpClientHandler* of *DelegatingHandler []*.</span><span class="sxs-lookup"><span data-stu-id="ed3d4-136">Instead of accepting an *HttpClient* as a constructor argument, hello constructor only accepts *HttpClientHandler* or *DelegatingHandler[]*.</span></span>

## <a name="downloaded-packages"></a><span data-ttu-id="ed3d4-137">Gedownloade pakketten</span><span class="sxs-lookup"><span data-stu-id="ed3d4-137">Downloaded packages</span></span>

<span data-ttu-id="ed3d4-138">Wanneer een client wordt verwerkt door een afhankelijkheid op zijn Sleutelkluis Hallo volgende gedownload</span><span class="sxs-lookup"><span data-stu-id="ed3d4-138">When a client is processing a  dependency on Key Vault hello following were downloaded</span></span>

### <a name="previous-package-list"></a><span data-ttu-id="ed3d4-139">Vorige pakketlijst</span><span class="sxs-lookup"><span data-stu-id="ed3d4-139">Previous package list</span></span>

* <span data-ttu-id="ed3d4-140">versie van het pakket id="Hyak.Common' = '1.0.2' targetFramework ="net45"</span><span class="sxs-lookup"><span data-stu-id="ed3d4-140">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span></span>
* <span data-ttu-id="ed3d4-141">versie van het pakket id="Microsoft.Azure.Common' = '2.0.4' targetFramework ="net45"</span><span class="sxs-lookup"><span data-stu-id="ed3d4-141">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span></span>
* <span data-ttu-id="ed3d4-142">versie van het pakket id="Microsoft.Azure.Common.Dependencies' = '1.0.0' targetFramework ="net45"</span><span class="sxs-lookup"><span data-stu-id="ed3d4-142">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="ed3d4-143">versie van het pakket id="Microsoft.Azure.KeyVault' = '1.0.0' targetFramework ="net45"</span><span class="sxs-lookup"><span data-stu-id="ed3d4-143">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="ed3d4-144">versie van het pakket id="Microsoft.Bcl' = '1.1.9' targetFramework ="net45"</span><span class="sxs-lookup"><span data-stu-id="ed3d4-144">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span></span>
* <span data-ttu-id="ed3d4-145">versie van het pakket id="Microsoft.Bcl.Async' = '1.0.168' targetFramework ="net45"</span><span class="sxs-lookup"><span data-stu-id="ed3d4-145">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span></span>
* <span data-ttu-id="ed3d4-146">versie van het pakket id="Microsoft.Bcl.Build' = '1.0.14' targetFramework ="net45"</span><span class="sxs-lookup"><span data-stu-id="ed3d4-146">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span></span>
* <span data-ttu-id="ed3d4-147">versie van het pakket id="Microsoft.Net.Http' = '2.2.22' targetFramework ="net45"</span><span class="sxs-lookup"><span data-stu-id="ed3d4-147">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span></span>

### <a name="current-package-list"></a><span data-ttu-id="ed3d4-148">Huidige pakketlijst</span><span class="sxs-lookup"><span data-stu-id="ed3d4-148">Current package list</span></span>

* <span data-ttu-id="ed3d4-149">versie van het pakket id="Microsoft.Azure.KeyVault' = '2.0.0-preview' targetFramework ="net45"</span><span class="sxs-lookup"><span data-stu-id="ed3d4-149">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span></span>
* <span data-ttu-id="ed3d4-150">versie van het pakket id="Microsoft.Rest.ClientRuntime' = '2.2.0' targetFramework ="net45"</span><span class="sxs-lookup"><span data-stu-id="ed3d4-150">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span></span>
* <span data-ttu-id="ed3d4-151">versie van het pakket id="Microsoft.Rest.ClientRuntime.Azure' = '3.2.0' targetFramework ="net45"</span><span class="sxs-lookup"><span data-stu-id="ed3d4-151">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span></span>

## <a name="class-changes"></a><span data-ttu-id="ed3d4-152">Wijzigingen voor klasse</span><span class="sxs-lookup"><span data-stu-id="ed3d4-152">Class changes</span></span>

* <span data-ttu-id="ed3d4-153">**UnixEpoch** klasse is verwijderd</span><span class="sxs-lookup"><span data-stu-id="ed3d4-153">**UnixEpoch** class has been removed</span></span>
* <span data-ttu-id="ed3d4-154">**Base64UrlConverter** klasse te wordt gewijzigd**Base64UrlJsonConverter**</span><span class="sxs-lookup"><span data-stu-id="ed3d4-154">**Base64UrlConverter** class is renamed too**Base64UrlJsonConverter**</span></span>

## <a name="other-changes"></a><span data-ttu-id="ed3d4-155">Andere wijzigingen</span><span class="sxs-lookup"><span data-stu-id="ed3d4-155">Other changes</span></span>

* <span data-ttu-id="ed3d4-156">Ondersteuning voor configuratie van beleid voor KV bewerking opnieuw proberen op tijdelijke fouten Hallo is toothis versie Hallo API toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="ed3d4-156">Support for hello configuration of KV operation retry policy on transient failures has been added toothis version of hello API.</span></span>

## <a name="microsoftazuremanagementkeyvault-nuget"></a><span data-ttu-id="ed3d4-157">Microsoft.Azure.Management.KeyVault NuGet</span><span class="sxs-lookup"><span data-stu-id="ed3d4-157">Microsoft.Azure.Management.KeyVault NuGet</span></span>

* <span data-ttu-id="ed3d4-158">Voor Hallo-bewerkingen die geretourneerd een *kluis*, Hallo retourtype is een klasse die deel uitmaakt van een eigenschap van de kluis.</span><span class="sxs-lookup"><span data-stu-id="ed3d4-158">For hello operations that returned a *vault*, hello return type was a class that contained a Vault property.</span></span> <span data-ttu-id="ed3d4-159">Hallo retourtype is nu *kluis*.</span><span class="sxs-lookup"><span data-stu-id="ed3d4-159">hello return type is now *Vault*.</span></span>
* <span data-ttu-id="ed3d4-160">*PermissionsToKeys* en *PermissionsToSecrets* zijn nu *Permissions.Keys* en *Permissions.Secrets*</span><span class="sxs-lookup"><span data-stu-id="ed3d4-160">*PermissionsToKeys* and *PermissionsToSecrets* are now *Permissions.Keys* and *Permissions.Secrets*</span></span>
* <span data-ttu-id="ed3d4-161">Aantal Hallo retourneren typen wijzigingen toepassen toohello-besturingselement-ook vlak.</span><span class="sxs-lookup"><span data-stu-id="ed3d4-161">Some of hello return types changes apply toohello control-plane as well.</span></span>

## <a name="microsoftazurekeyvaultextensions-nuget"></a><span data-ttu-id="ed3d4-162">Microsoft.Azure.KeyVault.Extensions NuGet</span><span class="sxs-lookup"><span data-stu-id="ed3d4-162">Microsoft.Azure.KeyVault.Extensions NuGet</span></span>

* <span data-ttu-id="ed3d4-163">Hallo-pakket te opgedeeld**Microsoft.Azure.KeyVault.Extensions** en **Microsoft.Azure.KeyVault.Cryptography** voor Hallo cryptografische bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="ed3d4-163">hello package is broken up too**Microsoft.Azure.KeyVault.Extensions** and **Microsoft.Azure.KeyVault.Cryptography** for hello cryptography operations.</span></span>

