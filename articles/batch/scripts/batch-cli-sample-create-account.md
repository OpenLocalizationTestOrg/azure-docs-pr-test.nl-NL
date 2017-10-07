---
title: aaaAzure voorbeeldscript CLI - Batch-account maken | Microsoft Docs
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
ms.openlocfilehash: 62b640eebbafdd1081822a638fd0720121ef067a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-cli"></a>Een Batch-account maken met hello Azure CLI

Dit script maakt een Azure Batch-account en toont hoe verschillende eigenschappen van Hallo-account kunnen worden opgevraagd en bijgewerkt.

## <a name="prerequisites"></a>Vereisten

Installeer Azure CLI met behulp van de instructies in Hallo HALLO hallo [Azure CLI installatiehandleiding](https://docs.microsoft.com/cli/azure/install-azure-cli), als u dit nog niet hebt gedaan.

## <a name="batch-account-sample-script"></a>Voorbeeldscript voor batch-account

Wanneer u een Batch-account maakt, standaard worden de rekenknooppunten toegewezen intern door Hallo Batch-service. Toegewezen rekenknooppunten zijn onderwerp tooa afzonderlijke kerngeheugenquotum en Hallo-account kan worden geverifieerd, hetzij via gedeelde sleutel referenties of een Azure Active Dirctory-token.

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]

## <a name="batch-account-using-user-subscription-sample-script"></a>Batch-account met behulp van de gebruiker abonnement voorbeeldscript

U kunt ook voor kiezen toohave Batch de rekenknooppunten in uw eigen Azure-abonnement maken.
Accounts die worden toegewezen compute knooppunten in uw abonnement moeten worden geverifieerd via een Azure Active Directory-token en meetelt Hallo rekenknooppunten toegewezen quotum voor uw abonnement. toocreate een account in deze modus, moet een de verwijzing naar een Sleutelkluis opgeven bij het Hallo-account maken.

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie

Nadat u een van de Hallo hierboven voorbeeldscripts uitvoeren, uitvoeren Hallo opdracht tooremove na de resourcegroep en alle gerelateerde resources (met inbegrip van de Batch-accounts, Azure Storage-accounts en Azure sleutelkluizen).

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van Hallo opdrachten toocreate een resourcegroep, Batch-account en alle gerelateerde resources te volgen. Elke opdracht in Hallo tabel koppelingen toocommand-specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ batch-account maken](https://docs.microsoft.com/cli/azure/batch/account#create) | Hallo Batch-account maakt.  |
| [AZ batch-account instellen](https://docs.microsoft.com/cli/azure/batch/account#set) | Eigenschappen van Batch-account Hallo-updates.  |
| [AZ batch-account weergeven](https://docs.microsoft.com/cli/azure/batch/account#show) | Haalt informatie Hallo Batch-account opgegeven.  |
| [lijst van AZ batch-account-sleutels](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | Haalt Hallo toegangstoetsen Hallo Batch-account opgegeven.  |
| [aanmeldingsnaam AZ batch-account](https://docs.microsoft.com/cli/azure/batch/account#login) | Verifieert tegen Hallo opgegeven Batch-account voor verdere tussenkomst van de CLI.  |
| [AZ storage-account maken](https://docs.microsoft.com/cli/azure/storage/account#create) | Hiermee maakt u een opslagaccount. |
| [AZ keyvault maken](https://docs.microsoft.com/cli/azure/keyvault#create) | Maakt een sleutelkluis. |
| [AZ keyvault-beleid instellen](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | Hallo-beveiligingsbeleid van de opgegeven sleutelkluis Hallo bijwerken. |
| [AZ groep verwijderen](https://docs.microsoft.com/cli/azure/group#delete) | Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Aanvullende Batch CLI scriptvoorbeelden kunnen u vinden in Hallo [documentatie van Azure Batch CLI](../batch-cli-samples.md).
