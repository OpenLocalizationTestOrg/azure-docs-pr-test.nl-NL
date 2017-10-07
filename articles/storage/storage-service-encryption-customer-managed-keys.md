---
title: aaaAzure Service versleuteling van opslag met behulp van de klant beheerde sleutels in Azure Sleutelkluis | Microsoft Docs
description: 'Gebruik hello Azure Storage-Service: versleuteling functie tooencrypt uw Azure-blobopslag op Hallo servicezijde bij het opslaan van gegevens Hallo en ontsleutelen wanneer sleutels bij het ophalen van Hallo-gegevens met behulp van de klant beheerd.'
services: storage
documentationcenter: .net
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: lakasa
ms.openlocfilehash: 870cae2f258b356aa234f8bba65a023ac389be10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="storage-service-encryption-using-customer-managed-keys-in-azure-key-vault"></a>Versleuteling van opslag-Service met behulp van de klant beheerde sleutels in Azure Sleutelkluis

Microsoft Azure is sterk doorgevoerd toohelping u beveiligen en uw toomeet gegevens beveiligt uw organisatie beveiliging en naleving verplichtingen.  Een manier die u kunt uw gegevens in rust beveiligen is toouse opslag Service versleuteling (SSE), die automatisch worden uw gegevens worden gecodeerd bij het schrijven van toostorage en uw gegevens ontsleutelt bij het ophalen van het. Hallo versleuteling en ontsleuteling is automatische en volledig transparant en maakt gebruik van 256-bits [AES-versleuteling](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), een van de sterkste blok Hallo coderingen beschikbaar.

U kunt Microsoft beheerde versleutelingssleutels SSE of kunt u uw eigen versleutelingssleutels. In dit artikel wordt Bespreek Hallo laatste. Zie voor meer informatie over het gebruik van door Microsoft beheerde sleutels of over SSE in het algemeen [Service versleuteling van opslag voor gegevens in rust](storage-service-encryption.md).

tooprovide hello mogelijkheid toouse uw eigen versleutelingssleutels SSE voor Blob storage Azure van met Azure Key Vault (Sleutelkluis) is geïntegreerd. U kunt uw eigen versleutelingssleutels maken en op te slaan in Azure Sleutelkluis, of kunt u de Azure Sleutelkluis-API's toogenerate versleutelingssleutels. Niet alleen biedt Azure Sleutelkluis kunt u toomanage en beheren van uw sleutels, ook kunt u tooaudit uw sleutelgebruik. 

Waarom zou u wilt dat toocreate uw eigen sleutels? Dit biedt u meer flexibiliteit, met inbegrip van Hallo mogelijkheid toocreate, draaien, uitschakelen en toegangsbeheer en tooaudit Hallo versleuteling sleutels die worden gebruikt tooprotect uw gegevens definiëren.

## <a name="sse-with-customer-managed-keys-preview"></a>SSE met de klant beheerde sleutels preview

Deze functie is momenteel beschikbaar als preview-product. toouse die deze functie, moet u een nieuw opslagaccount toocreate. U kunt een nieuwe sleutelkluis maken en sleutel of u een bestaande sleutelkluis en sleutel kunt gebruiken. Hallo-opslagaccount en Hallo sleutelkluis moeten zich op Hallo dezelfde regio, maar ze kunnen zich in verschillende abonnementen behoren.

tooparticipate hello Preview neemt contact op met [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com). We bieden een speciale koppeling tooparticipate Hallo Preview-versie.

toolearn meer, Raadpleeg toohello [Veelgestelde vragen over](#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).

> [!IMPORTANT]
> U moet zich registreren voor Hallo preview voorafgaande toofollowing Hallo stappen in dit artikel. Zonder toegang tot het preview, wordt u niet kunt tooenable deze functie in Hallo-portal zijn.

## <a name="getting-started"></a>Aan de slag
## <a name="step-1-create-a-new-storage-accountstorage-create-storage-accountmd"></a>Stap 1: [een nieuw opslagaccount maken](storage-create-storage-account.md)

## <a name="step-2-enable-encryption"></a>Stap 2: Enable-versleuteling
U kunt SSE inschakelen voor Hallo storage-account met behulp van Hallo [Azure-portal](https://portal.azure.com). Hallo blade van de instellingen voor Hallo storage-account, zoekt u naar Hallo Blob-Service sectie zoals weergegeven in onderstaande afbeelding en klik op versleuteling.

![De optie versleuteling Portal schermopname](./media/storage-service-encryption/image1.png)
<br/>*SSE voor Blob-Service inschakelen*

Als u tooprogrammatically inschakelen of Hallo versleuteling van de opslagruimte op een storage-account uitschakelen, kunt u Hallo [REST API van Azure Storage Resource Provider](https://docs.microsoft.com/en-us/rest/api/storagerp/?redirectedfrom=MSDN), Hallo [Storage Resource Provider-clientbibliotheek voor .NET](https://docs.microsoft.com/en-us/dotnet/api/?redirectedfrom=MSDN), [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview?view=azurermps-4.0.0), of Hallo [Azure CLI](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli).

In dit scherm als u niet Hallo 'gebruiken your own key' selectievakje ziet zijn u niet goedgekeurd voor Hallo preview. Verzend een e-mailbericht te[ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) en goedkeuring aanvragen.

![Portal schermafbeelding versleuteling Preview](./media/storage-service-encryption-customer-managed-keys/ssecmk1.png)

Standaard SSE Microsoft beheerd sleutels gebruikt. toouse selectievakje Hallo van uw eigen sleutels. Vervolgens kunt u uw sleutel URI opgeven, of Selecteer een sleutel en de Sleutelkluis in Hallo objectkiezer.

## <a name="step-3-select-your-key"></a>Stap 3: Uw sleutel selecteren

![Schermafbeelding van de portal uw eigen sleutel optie weergegeven versleuteling gebruiken](./media/storage-service-encryption-customer-managed-keys/ssecmk2.png)

![Portal schermafbeelding versleuteling met sleutel uri optie invoeren](./media/storage-service-encryption-customer-managed-keys/ssecmk3.png)

Als Hallo storage-account geen toegang tot toohello Sleutelkluis heeft, kunt u de volgende Hallo uitvoeren met behulp van Azure Powershell toogrant toegang toohello opslagaccounts toohello vereist sleutelkluis opdracht.

![Portal schermafbeelding toegang is geweigerd voor sleutelkluis](./media/storage-service-encryption-customer-managed-keys/ssecmk4.png)

U kunt ook toegang via hello Azure-portal door te gaan toohello Azure Sleutelkluis in hello Azure-portal en het verlenen van toegang toohello storage-account.

## <a name="step-4-copy-data-toostorage-account"></a>Stap 4: Kopieer data toostorage-account
Als u tootransfer gegevens in uw nieuwe opslagaccount wilt zodat ze zijn versleuteld, Raadpleeg te[stap 3 van aan de slag in Service-versleuteling van opslag voor gegevens in rust](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-3-copy-data-to-storage-account).

## <a name="step-5-query-hello-status-of-hello-encrypted-data"></a>Stap 5: De status van de Hallo Hallo versleutelde gegevens
tooquery hello status van de gegevens versleuteld Hallo Raadpleeg te[stap 4 van aan de slag in Service-versleuteling van opslag voor gegevens in rust](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-4-query-the-status-of-the-encrypted-data).

## <a name="frequently-asked-questions-about-storage-service-encryption-for-data-at-rest"></a>Veelgestelde vragen over Service-versleuteling van opslag voor gegevens in rust
**V: ik gebruik Premium-opslag; kan ik SSE gebruiken met sleutels van de klant beheerd?**

A: Ja SSE met door Microsoft beheerd en de klant beheerde sleutels op zowel Standard-opslag- en Premium-opslag wordt ondersteund. 

**V: kan ik nieuwe storage-accounts met SSE met beheer van de klant sleutels ingeschakeld met behulp van Azure PowerShell en Azure CLI maken?**

A: Ja.

**V: hoe veel meer kosten van Azure Storage biedt als SSE met klant beheerde sleutels is ingeschakeld?**

A: Er is een waarde die is gekoppeld voor het gebruik van Azure Sleutelkluis. Voor meer informatie gaat u naar [Sleutelkluis prijzen](https://azure.microsoft.com/en-us/pricing/details/key-vault/). Er is geen extra kosten voor het gebruik van SSE.

**V: kan ik toegang toohello versleutelingssleutels intrekken?**

A: Ja, kunt u de toegang intrekken op elk gewenst moment. Er zijn verschillende manieren toorevoke tooyour toegangssleutels. Raadpleeg het te[Azure Key Vault PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.0.0) en [Azure Key Vault CLI](https://docs.microsoft.com/en-us/cli/azure/keyvault) voor meer informatie. Toegang intrekken wordt toegang tot tooall blobs in de storage-account Hallo effectief geblokkeerd als Hallo versleutelingssleutel Account niet toegankelijk door Azure Storage is.

**V: kan ik een opslagaccount en de sleutel in andere regio maken?**

A: Nee, Hallo Hallo storage-account en sleutel/sleutel van de kluis nodig toobe in dezelfde regio. 

**V: kan ik SSE inschakelen met beheer van de klant sleutels bij het maken van Hallo storage-account?**

A: Nee. Wanneer u SSE inschakelt tijdens het maken van Hallo storage-account, kunt u alleen Microsoft beheerde sleutels. Als u toouse beheer van de klant sleutels dat wilt moet u tooupdate Hallo eigenschappen van het opslagaccount. U kunt REST gebruiken of een van de Hallo opslag client bibliotheken tooprogrammatically uw storage-account bijwerken of bijwerken van Hallo eigenschappen van het opslagaccount hello Azure Portal gebruiken na het Hallo-account maken.

**V: kan ik versleuteling uitschakelen tijdens het gebruik van SSE met de klant beheerde sleutels?**

A: u kunt versleuteling Nee, niet uitschakelen terwijl SSE gebruiken met de klant sleutels beheerde. toodisable versleuteling, moet u tooswitch toousing Microsoft beheerde sleutels. U kunt dit doen met behulp van hello Azure-portal of PowerShell.

**V: is SSE standaard ingeschakeld wanneer ik een nieuw opslagaccount maken?**

A: SSE is niet standaard; hello Azure portal tooenable kunt u deze. U kunt deze functie met Hallo REST-API van Storage Resource Provider ook programmatisch inschakelen. 

**V: ik inschakelen niet codering voor mijn storage-account.**

A: is het een Resource Manager-storage-account? Klassieke opslagaccounts worden niet ondersteund. SSE met sleutels voor beheer van de klant kan ook worden ingeschakeld alleen op de zojuist gemaakte Resource Manager-opslagaccounts.

**V: SSE Is met de klant beheerde sleutels alleen toegestaan in specifieke gebieden?**

A: SSE is beschikbaar in alleen bepaalde regio's voor Blob-opslag voor deze Preview. Stuur een e-mail [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) toocheck voor beschikbaarheid en meer informatie over de preview. 

**V: hoe neem ik iemand als ik problemen hebt of tooprovide feedback wilt?**

A: neemt contact op met [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) van eventuele tooStorage versleuteling van de Service problemen. 

## <a name="next-steps"></a>Volgende stappen

*   Voor meer informatie over een uitgebreide reeks beveiliging Hallo mogelijkheden die ontwikkelaars helpen bij het ontwikkelen van beveiligde toepassingen, raadpleegt u Hallo [opslag beveiligingshandleiding](https://docs.microsoft.com/en-us/azure/storage/storage-security-guide).
*   Zie voor informatie over Azure Sleutelkluis [wat is Azure Sleutelkluis](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)?
*   Zie voor aan de slag op Azure Sleutelkluis, [aan de slag met Azure Key Vault](../key-vault/key-vault-get-started.md).
