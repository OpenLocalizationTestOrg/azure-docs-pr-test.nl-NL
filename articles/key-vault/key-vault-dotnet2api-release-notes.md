---
title: Belangrijke opmerkingen bij de Release van de kluis .NET 2.x API | Microsoft Docs
description: .NET-ontwikkelaars wilt deze API code voor Azure Sleutelkluis gebruiken
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
ms.openlocfilehash: c5b5fd7f16faf17d16ecc82269fb1264adf4dd06
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a><span data-ttu-id="4a14b-103">Azure Sleutelkluis .NET 2.0 - Release-opmerkingen en Migratiehandleiding</span><span class="sxs-lookup"><span data-stu-id="4a14b-103">Azure Key Vault .NET 2.0 - Release Notes and Migration Guide</span></span>
<span data-ttu-id="4a14b-104">De volgende opmerkingen en richtlijnen zijn voor ontwikkelaars die werken met Azure Key Vault .NET / C#-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="4a14b-104">The following notes and guidance are for developers working with Azure Key Vault .NET / C# library.</span></span> <span data-ttu-id="4a14b-105">In de overgang van versie 1.0 naar versie 2.0, een aantal updates zijn aangebracht die wordt vereist migratie werk in uw code in om te kunnen profiteren van de functionele verbeteringen en toevoegingen, zoals functies **Sleutelkluis-certificaten**  ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="4a14b-105">In the transition from the 1.0 version to the 2.0 version, a number of updates have been made that will require migration work in your code in order for you to benefit from the functional improvements and feature additions such as **Key Vault certificates** support.</span></span>

## <a name="key-vault-certificates"></a><span data-ttu-id="4a14b-106">Sleutelkluis-certificaten</span><span class="sxs-lookup"><span data-stu-id="4a14b-106">Key Vault certificates</span></span>

<span data-ttu-id="4a14b-107">Sleutelkluis certificaten ondersteuning biedt voor het beheren van uw x509 certificaten en de volgende problemen:</span><span class="sxs-lookup"><span data-stu-id="4a14b-107">Key Vault certificates support provides for management of your x509 certificates and the following behaviors:</span></span>  

* <span data-ttu-id="4a14b-108">Kan de eigenaar van een certificaat om een certificaat via een proces voor het maken van Sleutelkluis of het importeren van een bestaand certificaat te maken.</span><span class="sxs-lookup"><span data-stu-id="4a14b-108">Allows a certificate owner to create a certificate through a Key Vault creation process or through the import of an existing certificate.</span></span> <span data-ttu-id="4a14b-109">Dit omvat zowel zelfondertekend en de certificeringsinstantie die certificaten worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="4a14b-109">This includes both self-signed and Certificate Authority generated certificates.</span></span>
* <span data-ttu-id="4a14b-110">Hiermee kunt u de eigenaar van een Sleutelkluis-certificaat voor het implementeren van veilige opslag en beheer van X509 certificaten zonder interactie met privésleutelmateriaal.</span><span class="sxs-lookup"><span data-stu-id="4a14b-110">Allows a Key Vault certificate owner to implement secure storage and management of X509 certificates without interaction with private key material.</span></span>  
* <span data-ttu-id="4a14b-111">Kan de eigenaar van een certificaat om een beleid waarin wordt verwezen Sleutelkluis voor het beheren van de levenscyclus van een certificaat te maken.</span><span class="sxs-lookup"><span data-stu-id="4a14b-111">Allows a certificate owner to create a policy that directs Key Vault to manage the life-cycle of a certificate.</span></span>  
* <span data-ttu-id="4a14b-112">Kan certificaat eigenaren van contactgegevens voor melding over de levenscyclus van gebeurtenissen van verlopen en verlenging van het certificaat opgeven.</span><span class="sxs-lookup"><span data-stu-id="4a14b-112">Allows certificate owners to provide contact information for notification about life-cycle events of expiration and renewal of certificate.</span></span>  
* <span data-ttu-id="4a14b-113">Ondersteunt automatische vernieuwing met geselecteerde verleners - Sleutelkluis partner X509 providers van het certificaat / certificeringsinstanties.</span><span class="sxs-lookup"><span data-stu-id="4a14b-113">Supports automatic renewal with selected issuers - Key Vault partner X509 certificate providers / certificate authorities.</span></span>
  
  * <span data-ttu-id="4a14b-114">Opmerking: providers/instanties niet in de samenwerking ook zijn toegestaan, maar geen ondersteuning voor de functie voor automatisch vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="4a14b-114">NOTE - Non-partnered providers/authorities are also allowed but, will not support the auto renewal feature.</span></span>

## <a name="net-support"></a><span data-ttu-id="4a14b-115">Ondersteuning voor .NET</span><span class="sxs-lookup"><span data-stu-id="4a14b-115">.NET support</span></span>

* <span data-ttu-id="4a14b-116">**.NET 4.0** wordt niet ondersteund door de versie 2.0 van .NET Azure Key Vault / C#-bibliotheek</span><span class="sxs-lookup"><span data-stu-id="4a14b-116">**.NET 4.0** is not supported by the 2.0 version of the Azure Key Vault .NET/C# library</span></span>
* <span data-ttu-id="4a14b-117">**.NET core** wordt ondersteund door de versie 2.0 van .NET Azure Key Vault / C#-bibliotheek</span><span class="sxs-lookup"><span data-stu-id="4a14b-117">**.NET Core** is supported by the 2.0 version of the Azure Key Vault .NET/C# library</span></span>

## <a name="namespaces"></a><span data-ttu-id="4a14b-118">Naamruimten</span><span class="sxs-lookup"><span data-stu-id="4a14b-118">Namespaces</span></span>

* <span data-ttu-id="4a14b-119">De naamruimte voor **modellen** wordt gewijzigd van **Microsoft.Azure.KeyVault** naar **Microsoft.Azure.KeyVault.Models**.</span><span class="sxs-lookup"><span data-stu-id="4a14b-119">The namespace for **models** is changed from **Microsoft.Azure.KeyVault** to **Microsoft.Azure.KeyVault.Models**.</span></span>
* <span data-ttu-id="4a14b-120">De **Microsoft.Azure.KeyVault.Internal** naamruimte is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="4a14b-120">The **Microsoft.Azure.KeyVault.Internal** namespace is dropped.</span></span>
* <span data-ttu-id="4a14b-121">De naamruimte Azure SDK-afhankelijkheden zijn gewijzigd van **Hyak.Common** en **Hyak.Common.Internals** naar **Microsoft.Rest** en  **Microsoft.Rest.Serialization**</span><span class="sxs-lookup"><span data-stu-id="4a14b-121">The Azure SDK dependencies namespace are changed from **Hyak.Common** and **Hyak.Common.Internals** to **Microsoft.Rest** and **Microsoft.Rest.Serialization**</span></span>

## <a name="type-changes"></a><span data-ttu-id="4a14b-122">Wijzigingen van het type</span><span class="sxs-lookup"><span data-stu-id="4a14b-122">Type changes</span></span>

* <span data-ttu-id="4a14b-123">*Geheim* gewijzigd in *SecretBundle*</span><span class="sxs-lookup"><span data-stu-id="4a14b-123">*Secret* changed to *SecretBundle*</span></span>
* <span data-ttu-id="4a14b-124">*Woordenlijst* gewijzigd in *IDictionary*</span><span class="sxs-lookup"><span data-stu-id="4a14b-124">*Dictionary* changed to *IDictionary*</span></span>
* <span data-ttu-id="4a14b-125">*Lijst<T>, string []* gewijzigd in *IList<T>*</span><span class="sxs-lookup"><span data-stu-id="4a14b-125">*List<T>, string []* changed to *IList<T>*</span></span>
* <span data-ttu-id="4a14b-126">*NextList* gewijzigd in *NextPageLink*</span><span class="sxs-lookup"><span data-stu-id="4a14b-126">*NextList* changed to  *NextPageLink*</span></span>

## <a name="return-types"></a><span data-ttu-id="4a14b-127">Retourtypen</span><span class="sxs-lookup"><span data-stu-id="4a14b-127">Return types</span></span>

* <span data-ttu-id="4a14b-128">**KeyList** en **SecretList** retourneert *IPage<T>*  in plaats van *ListKeysResponseMessage*</span><span class="sxs-lookup"><span data-stu-id="4a14b-128">**KeyList** and **SecretList** will return *IPage<T>* instead of *ListKeysResponseMessage*</span></span>
* <span data-ttu-id="4a14b-129">De gegenereerde **BackupKeyAsync** retourneert *BackupKeyResult* die bevat *waarde* (back-up van blob).</span><span class="sxs-lookup"><span data-stu-id="4a14b-129">The generated **BackupKeyAsync** will return *BackupKeyResult* which contains *Value* (back-up blob).</span></span> <span data-ttu-id="4a14b-130">Voordat de methode is ingepakt en alleen de waarde te retourneren.</span><span class="sxs-lookup"><span data-stu-id="4a14b-130">Before the method was wrapped and returning only the value.</span></span>

## <a name="exceptions"></a><span data-ttu-id="4a14b-131">Uitzonderingen</span><span class="sxs-lookup"><span data-stu-id="4a14b-131">Exceptions</span></span>

* <span data-ttu-id="4a14b-132">*KeyVaultClientException* wordt gewijzigd naar *KeyVaultErrorException*</span><span class="sxs-lookup"><span data-stu-id="4a14b-132">*KeyVaultClientException* is changed to *KeyVaultErrorException*</span></span>
* <span data-ttu-id="4a14b-133">De servicefout is gewijzigd van *uitzondering. Fout* naar *uitzondering. Body.Error.Message*.</span><span class="sxs-lookup"><span data-stu-id="4a14b-133">The service error is changed from *exception.Error* to *exception.Body.Error.Message*.</span></span>
* <span data-ttu-id="4a14b-134">Aanvullende informatie verwijderd uit het foutbericht voor **[JsonExtensionData]**.</span><span class="sxs-lookup"><span data-stu-id="4a14b-134">Removed additional info from the error message for **[JsonExtensionData]**.</span></span>

## <a name="constructors"></a><span data-ttu-id="4a14b-135">Constructors</span><span class="sxs-lookup"><span data-stu-id="4a14b-135">Constructors</span></span>

* <span data-ttu-id="4a14b-136">In plaats van het accepteren van een *HttpClient* als constructor-argument accepteert de constructor alleen *HttpClientHandler* of *DelegatingHandler []*.</span><span class="sxs-lookup"><span data-stu-id="4a14b-136">Instead of accepting an *HttpClient* as a constructor argument, the constructor only accepts *HttpClientHandler* or *DelegatingHandler[]*.</span></span>

## <a name="downloaded-packages"></a><span data-ttu-id="4a14b-137">Gedownloade pakketten</span><span class="sxs-lookup"><span data-stu-id="4a14b-137">Downloaded packages</span></span>

<span data-ttu-id="4a14b-138">Wanneer een client een afhankelijkheid van Sleutelkluis verwerkt zijn de volgende gedownload</span><span class="sxs-lookup"><span data-stu-id="4a14b-138">When a client is processing a  dependency on Key Vault the following were downloaded</span></span>

### <a name="previous-package-list"></a><span data-ttu-id="4a14b-139">Vorige pakketlijst</span><span class="sxs-lookup"><span data-stu-id="4a14b-139">Previous package list</span></span>

* <span data-ttu-id="4a14b-140">versie van het pakket id="Hyak.Common' = '1.0.2' targetFramework ="net45"</span><span class="sxs-lookup"><span data-stu-id="4a14b-140">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span></span>
* <span data-ttu-id="4a14b-141">versie van het pakket id="Microsoft.Azure.Common' = '2.0.4' targetFramework ="net45"</span><span class="sxs-lookup"><span data-stu-id="4a14b-141">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span></span>
* <span data-ttu-id="4a14b-142">versie van het pakket id="Microsoft.Azure.Common.Dependencies' = '1.0.0' targetFramework ="net45"</span><span class="sxs-lookup"><span data-stu-id="4a14b-142">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="4a14b-143">versie van het pakket id="Microsoft.Azure.KeyVault' = '1.0.0' targetFramework ="net45"</span><span class="sxs-lookup"><span data-stu-id="4a14b-143">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="4a14b-144">versie van het pakket id="Microsoft.Bcl' = '1.1.9' targetFramework ="net45"</span><span class="sxs-lookup"><span data-stu-id="4a14b-144">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span></span>
* <span data-ttu-id="4a14b-145">versie van het pakket id="Microsoft.Bcl.Async' = '1.0.168' targetFramework ="net45"</span><span class="sxs-lookup"><span data-stu-id="4a14b-145">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span></span>
* <span data-ttu-id="4a14b-146">versie van het pakket id="Microsoft.Bcl.Build' = '1.0.14' targetFramework ="net45"</span><span class="sxs-lookup"><span data-stu-id="4a14b-146">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span></span>
* <span data-ttu-id="4a14b-147">versie van het pakket id="Microsoft.Net.Http' = '2.2.22' targetFramework ="net45"</span><span class="sxs-lookup"><span data-stu-id="4a14b-147">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span></span>

### <a name="current-package-list"></a><span data-ttu-id="4a14b-148">Huidige pakketlijst</span><span class="sxs-lookup"><span data-stu-id="4a14b-148">Current package list</span></span>

* <span data-ttu-id="4a14b-149">versie van het pakket id="Microsoft.Azure.KeyVault' = '2.0.0-preview' targetFramework ="net45"</span><span class="sxs-lookup"><span data-stu-id="4a14b-149">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span></span>
* <span data-ttu-id="4a14b-150">versie van het pakket id="Microsoft.Rest.ClientRuntime' = '2.2.0' targetFramework ="net45"</span><span class="sxs-lookup"><span data-stu-id="4a14b-150">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span></span>
* <span data-ttu-id="4a14b-151">versie van het pakket id="Microsoft.Rest.ClientRuntime.Azure' = '3.2.0' targetFramework ="net45"</span><span class="sxs-lookup"><span data-stu-id="4a14b-151">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span></span>

## <a name="class-changes"></a><span data-ttu-id="4a14b-152">Wijzigingen voor klasse</span><span class="sxs-lookup"><span data-stu-id="4a14b-152">Class changes</span></span>

* <span data-ttu-id="4a14b-153">**UnixEpoch** klasse is verwijderd</span><span class="sxs-lookup"><span data-stu-id="4a14b-153">**UnixEpoch** class has been removed</span></span>
* <span data-ttu-id="4a14b-154">**Base64UrlConverter** klasse is gewijzigd in **Base64UrlJsonConverter**</span><span class="sxs-lookup"><span data-stu-id="4a14b-154">**Base64UrlConverter** class is renamed to **Base64UrlJsonConverter**</span></span>

## <a name="other-changes"></a><span data-ttu-id="4a14b-155">Andere wijzigingen</span><span class="sxs-lookup"><span data-stu-id="4a14b-155">Other changes</span></span>

* <span data-ttu-id="4a14b-156">Ondersteuning voor de configuratie van beleid voor KV bewerking opnieuw proberen op tijdelijke fouten is toegevoegd in deze versie van de API.</span><span class="sxs-lookup"><span data-stu-id="4a14b-156">Support for the configuration of KV operation retry policy on transient failures has been added to this version of the API.</span></span>

## <a name="microsoftazuremanagementkeyvault-nuget"></a><span data-ttu-id="4a14b-157">Microsoft.Azure.Management.KeyVault NuGet</span><span class="sxs-lookup"><span data-stu-id="4a14b-157">Microsoft.Azure.Management.KeyVault NuGet</span></span>

* <span data-ttu-id="4a14b-158">Voor de bewerkingen die geretourneerd een *kluis*, het retourtype is een klasse die deel uitmaakt van een eigenschap van de kluis.</span><span class="sxs-lookup"><span data-stu-id="4a14b-158">For the operations that returned a *vault*, the return type was a class that contained a Vault property.</span></span> <span data-ttu-id="4a14b-159">Het retourtype is nu *kluis*.</span><span class="sxs-lookup"><span data-stu-id="4a14b-159">The return type is now *Vault*.</span></span>
* <span data-ttu-id="4a14b-160">*PermissionsToKeys* en *PermissionsToSecrets* zijn nu *Permissions.Keys* en *Permissions.Secrets*</span><span class="sxs-lookup"><span data-stu-id="4a14b-160">*PermissionsToKeys* and *PermissionsToSecrets* are now *Permissions.Keys* and *Permissions.Secrets*</span></span>
* <span data-ttu-id="4a14b-161">Enkele wijzigingen retourtypen aan het besturingselement-ook van toepassing.</span><span class="sxs-lookup"><span data-stu-id="4a14b-161">Some of the return types changes apply to the control-plane as well.</span></span>

## <a name="microsoftazurekeyvaultextensions-nuget"></a><span data-ttu-id="4a14b-162">Microsoft.Azure.KeyVault.Extensions NuGet</span><span class="sxs-lookup"><span data-stu-id="4a14b-162">Microsoft.Azure.KeyVault.Extensions NuGet</span></span>

* <span data-ttu-id="4a14b-163">Het pakket is verbroken tot **Microsoft.Azure.KeyVault.Extensions** en **Microsoft.Azure.KeyVault.Cryptography** voor de cryptografie-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="4a14b-163">The package is broken up to **Microsoft.Azure.KeyVault.Extensions** and **Microsoft.Azure.KeyVault.Cryptography** for the cryptography operations.</span></span>

