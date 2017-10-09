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
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a>Azure Sleutelkluis .NET 2.0 - Release-opmerkingen en Migratiehandleiding
Hallo volgende opmerkingen en richtlijnen zijn voor ontwikkelaars die werken met Azure Key Vault .NET / C#-bibliotheek. In de overgangsfase Hallo van Hallo 1.0 versie 2.0 toohello versie, een aantal updates zijn aangebracht die wordt vereist migratie werk in uw code om toobenefit van Hallo functionele verbeteringen en toevoegingen, zoals functies **Sleutelkluis certificaten** ondersteunen.

## <a name="key-vault-certificates"></a>Sleutelkluis-certificaten

Sleutelkluis certificaten ondersteuning biedt voor het beheren van uw x509 certificaten en Hallo volgende gedrag:  

* Kan een certificaat eigenaar toocreate een certificaat via een proces voor het maken van Sleutelkluis of Hallo importeren van een bestaand certificaat. Dit omvat zowel zelfondertekend en de certificeringsinstantie die certificaten worden gegenereerd.
* Kan de eigenaar van een Sleutelkluis certificaat tooimplement veilige opslag en beheer van X509 certificaten zonder interactie met privésleutelmateriaal.  
* Hiermee kunt een certificaat eigenaar toocreate een beleid dat wordt verwezen Sleutelkluis toomanage Hallo levenscyclus van een certificaat.  
* Kan certificaat eigenaars tooprovide contactgegevens voor melding over de levenscyclus van gebeurtenissen van verlopen en verlenging van het certificaat.  
* Ondersteunt automatische vernieuwing met geselecteerde verleners - Sleutelkluis partner X509 providers van het certificaat / certificeringsinstanties.
  
  * Opmerking: providers/instanties niet in de samenwerking ook zijn toegestaan, maar biedt geen ondersteuning voor functie voor automatisch vernieuwen Hallo.

## <a name="net-support"></a>Ondersteuning voor .NET

* **.NET 4.0** wordt niet ondersteund door Hallo 2.0-versie van Azure Sleutelkluis .NET Hallo / C#-bibliotheek
* **.NET core** wordt ondersteund door de versie 2.0 Hallo Hallo Azure Key Vault .NET / C#-bibliotheek

## <a name="namespaces"></a>Naamruimten

* naamruimte voor Hallo **modellen** wordt gewijzigd van **Microsoft.Azure.KeyVault** te**Microsoft.Azure.KeyVault.Models**.
* Hallo **Microsoft.Azure.KeyVault.Internal** naamruimte is verwijderd.
* Hello Azure SDK-afhankelijkheden naamruimte zijn gewijzigd van **Hyak.Common** en **Hyak.Common.Internals** te**Microsoft.Rest** en  **Microsoft.Rest.Serialization**

## <a name="type-changes"></a>Wijzigingen van het type

* *Geheim* gewijzigd te*SecretBundle*
* *Woordenlijst* gewijzigd te*IDictionary*
* *Lijst<T>, string []* gewijzigd te*IList<T>*
* *NextList* gewijzigd te *NextPageLink*

## <a name="return-types"></a>Retourtypen

* **KeyList** en **SecretList** retourneert *IPage<T>*  in plaats van *ListKeysResponseMessage*
* Hallo gegenereerd **BackupKeyAsync** retourneert *BackupKeyResult* die bevat *waarde* (back-up van blob). Methode is voordat Hallo verpakte en terugkerende enige Hallo-waarde.

## <a name="exceptions"></a>Uitzonderingen

* *KeyVaultClientException* wordt gewijzigd te*KeyVaultErrorException*
* Hallo-servicefout wordt gewijzigd van *uitzondering. Fout* te*uitzondering. Body.Error.Message*.
* Aanvullende informatie verwijderd uit de foutbericht Hallo voor **[JsonExtensionData]**.

## <a name="constructors"></a>Constructors

* In plaats van het accepteren van een *HttpClient* als constructor-argument accepteert Hallo constructor alleen *HttpClientHandler* of *DelegatingHandler []*.

## <a name="downloaded-packages"></a>Gedownloade pakketten

Wanneer een client wordt verwerkt door een afhankelijkheid op zijn Sleutelkluis Hallo volgende gedownload

### <a name="previous-package-list"></a>Vorige pakketlijst

* versie van het pakket id="Hyak.Common' = '1.0.2' targetFramework ="net45"
* versie van het pakket id="Microsoft.Azure.Common' = '2.0.4' targetFramework ="net45"
* versie van het pakket id="Microsoft.Azure.Common.Dependencies' = '1.0.0' targetFramework ="net45"
* versie van het pakket id="Microsoft.Azure.KeyVault' = '1.0.0' targetFramework ="net45"
* versie van het pakket id="Microsoft.Bcl' = '1.1.9' targetFramework ="net45"
* versie van het pakket id="Microsoft.Bcl.Async' = '1.0.168' targetFramework ="net45"
* versie van het pakket id="Microsoft.Bcl.Build' = '1.0.14' targetFramework ="net45"
* versie van het pakket id="Microsoft.Net.Http' = '2.2.22' targetFramework ="net45"

### <a name="current-package-list"></a>Huidige pakketlijst

* versie van het pakket id="Microsoft.Azure.KeyVault' = '2.0.0-preview' targetFramework ="net45"
* versie van het pakket id="Microsoft.Rest.ClientRuntime' = '2.2.0' targetFramework ="net45"
* versie van het pakket id="Microsoft.Rest.ClientRuntime.Azure' = '3.2.0' targetFramework ="net45"

## <a name="class-changes"></a>Wijzigingen voor klasse

* **UnixEpoch** klasse is verwijderd
* **Base64UrlConverter** klasse te wordt gewijzigd**Base64UrlJsonConverter**

## <a name="other-changes"></a>Andere wijzigingen

* Ondersteuning voor configuratie van beleid voor KV bewerking opnieuw proberen op tijdelijke fouten Hallo is toothis versie Hallo API toegevoegd.

## <a name="microsoftazuremanagementkeyvault-nuget"></a>Microsoft.Azure.Management.KeyVault NuGet

* Voor Hallo-bewerkingen die geretourneerd een *kluis*, Hallo retourtype is een klasse die deel uitmaakt van een eigenschap van de kluis. Hallo retourtype is nu *kluis*.
* *PermissionsToKeys* en *PermissionsToSecrets* zijn nu *Permissions.Keys* en *Permissions.Secrets*
* Aantal Hallo retourneren typen wijzigingen toepassen toohello-besturingselement-ook vlak.

## <a name="microsoftazurekeyvaultextensions-nuget"></a>Microsoft.Azure.KeyVault.Extensions NuGet

* Hallo-pakket te opgedeeld**Microsoft.Azure.KeyVault.Extensions** en **Microsoft.Azure.KeyVault.Cryptography** voor Hallo cryptografische bewerkingen.

