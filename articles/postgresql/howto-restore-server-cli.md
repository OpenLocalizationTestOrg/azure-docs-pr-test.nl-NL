---
title: Hoe tooback ups en het terugzetten van een server in Azure-Database voor PostgreSQL | Microsoft Docs
description: Meer informatie over hoe Hallo tooback up en herstel van een server in Azure-Database voor PostgreSQL met behulp van Azure CLI.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 0b9ed25e3e3a88dd5c7ffe2ae7c27f8eef9be710
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-a-server-in-azure-database-for-postgresql-by-using-hello-azure-cli"></a>Hoe Hallo tooback up en herstel van een server in Azure-Database voor PostgreSQL met behulp van Azure CLI

Azure-Database gebruiken voor PostgreSQL toorestore een server-database tooan eerdere datum die van 7 too35 dagen omvat.

## <a name="prerequisites"></a>Vereisten
toocomplete hoe-tooguide die u nodig:
- Een [Azure Database voor PostgreSQL-server en database](quickstart-create-server-database-azure-cli.md)

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

 

> [!IMPORTANT]
> Als u installeert en lokaal hello Azure CLI gebruiken, wordt deze hoe-tooguide vereist dat u Azure CLI versie 2.0 of hoger. Voer tooconfirm Hallo versie bij hello Azure CLI-opdrachtprompt `az --version`. tooinstall upgraden, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).

## <a name="back-up-happens-automatically"></a>Wordt automatisch een back-up.
Wanneer u Azure-Database voor PostgreSQL, wordt Hallo database-service automatisch een back-up van Hallo-service om de 5 minuten. 

Basic-laag zijn Hallo back-ups beschikbaar voor 7 dagen. Standard-laag zijn Hallo back-ups beschikbaar voor 35 dagen. Zie voor meer informatie [Azure Database voor PostgreSQL Prijscategorieën](concepts-service-tiers.md).

U kunt met deze functie voor automatische back-up herstellen Hallo-server en de databases tooan eerdere datum of tijdstip voor herstel.

## <a name="restore-a-database-tooa-previous-point-in-time-by-using-hello-azure-cli"></a>Een database tooa eerder punt in tijd herstellen met behulp van hello Azure CLI
Azure-Database gebruiken voor PostgreSQL toorestore Hallo server tooa vorige punt in tijd. Hallo hersteld gegevens wordt de nieuwe server gekopieerde tooa en bestaande Hallo-server is ongewijzigd worden gelaten. Als een tabel wordt per ongeluk verwijderd op twaalf uur 's middags vandaag de dag, kunt u bijvoorbeeld toohello tijd net vóór twaalf uur 's middags herstellen. U kunt vervolgens Hallo ontbrekende tabel en gegevens uit de Hallo hersteld kopieën van Hallo server ophalen. 

Gebruik hello Azure CLI-server Hallo toorestore [az postgres server terugzetten](/cli/azure/postgres/server#restore) opdracht.

### <a name="run-hello-restore-command"></a>Hallo restore-opdracht uitvoeren

toorestore hello server op Hallo Azure CLI-opdrachtregel invoeren Hallo volgende opdracht:

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

Hallo `az postgres server restore` opdracht vereist Hallo volgende parameters:
| Instelling | Voorgestelde waarde | Beschrijving  |
| --- | --- | --- |
| resourcegroep |  myResourceGroup |  De resourcegroep waar Hallo bronserver bestaat.  |
| naam | mypgserver hersteld | Hallo-naam van de nieuwe Hallo-server die is gemaakt door de opdracht restore Hallo. |
| herstel punt in tijd | 2017-04-13T13:59:00Z | Selecteer een punt in tijd toorestore aan. Deze datum en tijd moet binnen Hallo van bronserver maakt u een back-up van de bewaarperiode. Gebruik Hallo ISO8601-indeling voor datum en tijd. Bijvoorbeeld, kunt u uw eigen lokale tijdzone, zoals `2017-04-13T05:59:00-08:00`. U kunt ook Hallo Zulu UTC-indeling, bijvoorbeeld `2017-04-13T13:59:00Z`. |
| bron-server | mypgserver 20170401 | Hallo-naam of ID van Hallo bron server toorestore uit. |

Wanneer u een tooan server herstelt eerdere punt in tijd, een nieuwe server is gemaakt. Hallo oorspronkelijke server en de databases van Hallo opgegeven tijdstip zijn gekopieerde toohello nieuwe server.

Hallo locatie en prijzen laag waarden Hallo voor blijven hersteld Hallo server dezelfde als de oorspronkelijke server Hallo. 

Hallo `az postgres server restore` opdracht synchroon is. Nadat het Hallo-server is hersteld, kunt u deze opnieuw toorepeat Hallo proces voor een ander punt in tijd. 

Na het Hallo herstellen proces is voltooid, zoek de nieuwe server Hallo en controleer of dat Hallo gegevens is hersteld, zoals verwacht.

## <a name="next-steps"></a>Volgende stappen
[Verbindingsbibliotheken voor Azure-Database voor PostgreSQL](concepts-connection-libraries.md)
