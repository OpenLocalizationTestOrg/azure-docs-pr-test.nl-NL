---
title: 'Azure CLI-Script voorbeeld: een Batch-account maken | Microsoft Docs'
description: 'Azure CLI-Script voorbeeld: een Batch-account maken'
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: 698978fd717091c49a1375e222f46f4325431223
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-batch-account-with-the-azure-cli"></a>Een Batch-account maken met de Azure CLI

Dit script maakt een Azure Batch-account en toont hoe verschillende eigenschappen van het account kunnen worden opgevraagd en bijgewerkt.

## <a name="prerequisites"></a>Vereisten

Installeer de Azure CLI met behulp van de instructies in de [Azure CLI installatiehandleiding](https://docs.microsoft.com/cli/azure/install-azure-cli), als u dit nog niet hebt gedaan.

## <a name="batch-account-sample-script"></a>Voorbeeldscript voor batch-account

Wanneer u een Batch-account maakt, standaard worden de rekenknooppunten toegewezen intern door de Batch-service. Toegewezen rekenknooppunten zijn onderworpen aan een afzonderlijke kerngeheugenquotum en het account kan worden geverifieerd, hetzij via gedeelde sleutel referenties of een Azure Active Dirctory-token.

[!code-azurecli[belangrijkste](../../../cli_scripts/batch/create-account/create-account.sh "-Account maken")]

## <a name="batch-account-using-user-subscription-sample-script"></a>Batch-account met behulp van de gebruiker abonnement voorbeeldscript

U kunt er ook voor kiezen om Batch de rekenknooppunten in uw eigen Azure-abonnement maken.
Accounts die worden toegewezen compute knooppunten in uw abonnement moeten worden geverifieerd via een Azure Active Directory-token en de rekenknooppunten toegewezen meetelt quotum voor uw abonnement. Voor het maken van een account in deze modus, moet een verwijzing naar een Sleutelkluis opgeven bij het maken van het account.

[!code-azurecli[belangrijkste](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Account maken met behulp van gebruikerabonnement")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie

Nadat u een van de bovenstaande voorbeelden van scripts uitvoeren, voer de volgende opdracht om te verwijderen van de resourcegroep en alle gerelateerde resources (met inbegrip van de Batch-accounts, Azure Storage-accounts en Azure sleutelkluizen).

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, Batch-account en alle gerelateerde resources. Elke opdracht in de tabel is gekoppeld aan de opdracht specifieke documentatie bij.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ batch-account maken](https://docs.microsoft.com/cli/azure/batch/account#create) | Maakt de Batch-account.  |
| [AZ batch-account instellen](https://docs.microsoft.com/cli/azure/batch/account#set) | De eigenschappen van de updates van het Batch-account.  |
| [AZ batch-account weergeven](https://docs.microsoft.com/cli/azure/batch/account#show) | Haalt de details van de opgegeven Batch-account.  |
| [lijst van AZ batch-account-sleutels](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | Hiermee haalt u de toegangssleutels van het opgegeven Batch-account.  |
| [aanmeldingsnaam AZ batch-account](https://docs.microsoft.com/cli/azure/batch/account#login) | Wordt geverifieerd op basis van de opgegeven Batch-account voor verdere tussenkomst van de CLI.  |
| [AZ storage-account maken](https://docs.microsoft.com/cli/azure/storage/account#create) | Hiermee maakt u een opslagaccount. |
| [AZ keyvault maken](https://docs.microsoft.com/cli/azure/keyvault#create) | Maakt een sleutelkluis. |
| [AZ keyvault-beleid instellen](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | Het beveiligingsbeleid van de opgegeven sleutelkluis bijwerken. |
| [AZ groep verwijderen](https://docs.microsoft.com/cli/azure/group#delete) | Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Aanvullende Batch CLI scriptvoorbeelden vindt u in de [documentatie van Azure Batch CLI](../batch-cli-samples.md).
