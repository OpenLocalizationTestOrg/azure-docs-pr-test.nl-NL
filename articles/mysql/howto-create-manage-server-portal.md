---
title: aaaCreate en beheren van Azure-Database voor de MySQL-server met Azure portal | Microsoft Docs
description: Dit artikel wordt beschreven hoe u kunt snel een nieuwe Azure-Database voor de MySQL-server maken en beheren Hallo-server met behulp van hello Azure-Portal.
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: c532df43b3d2124d7bd34875b32d52357f162af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a>Maken en beheren van Azure-Database voor de MySQL-server met Azure portal
Dit artikel wordt beschreven hoe u kunt snel een nieuwe Azure-Database voor de MySQL-server maken en beheren Hallo-server met behulp van hello Azure-Portal. Serverbeheer bevat Serverdetails & databases weer te geven, wachtwoord opnieuw instellen en verwijderen van Hallo-server.

## <a name="log-in-toohello-azure-portal"></a>Meld u bij toohello Azure-portal
Meld u bij toohello [Azure-portal](https://portal.azure.com).

## <a name="create-an-azure-database-for-mysql-server"></a>Een Azure-database voor MySQL-server maken
Volg deze stappen toocreate een Azure-Database voor de MySQL-server met de naam 'mysqlserver4demo'

1 Klik **nieuw** knop gevonden op Hallo linkerbovenhoek Hallo Azure-portal.

2 Selecteer **Databases** van Hallo nieuwe pagina en selecteer **Azure Database voor MySQL** van Hallo Databases pagina.

> Een Azure-Database voor de MySQL-server is gemaakt met een gedefinieerde set [berekenings- en](./concepts-compute-unit-and-storage.md) resources. Hallo-database wordt gemaakt vanuit een Azure-resourcegroep en in een Azure-Database voor de MySQL-server.

![Maak nieuwe-server](./media/howto-create-manage-server-portal/create-new-server.png)

3 - invullen hello Azure Database voor MySQL formulier Hello volgende informatie:

| **Formulierveld** | **Beschrijving van veld** |
|----------------|-----------------------|
| *Servernaam* | Azure-mysql (servernaam is globally unique identifier) |
| *Abonnement* | MySQLaaS (Selecteer in de vervolgkeuzelijst) |
| *Resourcegroep* | MyResource (een nieuwe resourcegroep maken of een bestaande gebruiken) |
| *Aanmeldgegevens van serverbeheerder* | myadmin (stel accountnaam van beheerder in) |
| *Wachtwoord* | beheerderswachtwoord voor account Setup |
| *Wachtwoord bevestigen* | bevestig wachtwoord voor beheerdersaccount |
| *Locatie* | Noord-Europa (Selecteer tussen Noord-Europa en VS-West) |
| *Versie* | 5.6 (Kies Azure Database voor MySQL server-versie) |

4 Klik **prijscategorie** toospecify Hallo prijscategorie en prestatieniveau serviceniveau voor uw nieuwe server. COMPUTE eenheid tussen 50 en 100 in de basisstaffel 100 en 200 in Standard-laag kan worden geconfigureerd en opslag op basis van opgenomen bedrag kan worden toegevoegd. Voor deze handleiding procedure kiezen we 50 Compute-eenheid en 50GB. Klik op **OK** toosave uw selectie.
![Maak-server--prijscategorie](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)

5 Klik **maken** tooprovision Hallo-server. De inrichting duurt een paar minuten.

> Controleer de Hallo **pincode toodashboard** optie tooallow eenvoudig bijhouden van uw implementaties.
> [!NOTE]
> Hoewel too1000GB in basisstaffel en 10000GB in standaard laag wordt ondersteund voor opslag, voor de openbare Preview is Hallo maximale opslagcapaciteit het nog steeds beperkt too1000GB tijdelijk. 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a>Een Azure-Database voor de MySQL-server bijwerken
Nadat de nieuwe server is ingericht, gebruiker heeft van 2 opties tooedit een bestaande server: beheerderswachtwoord of schaal omhoog/omlaag Hallo-server opnieuw instellen door te wijzigen Hallo compute-eenheden.

### <a name="change-hello-administrator-user-password"></a>Wachtwoord wijzigen Hallo beheerder-gebruiker
1 - op Hallo server **overzicht** blade, klikt u op **wachtwoord opnieuw instellen** toopopulate de invoer en de bevestiging venster van een wachtwoord.

2 - nieuw wachtwoord invoeren en Bevestig Hallo-wachtwoord in als hieronder Hallo-venster: ![wachtwoord opnieuw instellen](./media/howto-create-manage-server-portal/reset-password.png)

3 en klik op **OK** toosave Hallo nieuwe wachtwoord.

### <a name="scale-updown-by-changing-compute-units"></a>Omhoog/omlaag schalen door het wijzigen van de Compute-eenheden

1 - op Hallo serverblade onder **instellingen**, klikt u op **prijscategorie** tooopen Hallo prijzen laag blade voor hello Azure Database voor de MySQL-server.

2 volgen stap 4 in **maken van een Azure-Database voor MySQL server** toochange Compute eenheden in dezelfde prijscategorie Hallo.

## <a name="delete-an-azure-database-for-mysql-server"></a>Een Azure-Database voor de MySQL-server verwijderen

1 - op Hallo server **overzicht** blade, klikt u op **verwijderen** opdracht knop tooopen Hallo verwijderen bevestiging blade.

2-type Hallo juiste servernaam in het invoervak van de blade hello om dubbele bevestiging.

3 en klik op **verwijderen** knop opnieuw tooconfirm actie verwijderen en wachten op de pop-up 'Verwijderen geslaagd' op Hallo meldingsbalk.

## <a name="list-hello-azure-database-for-mysql-databases"></a>Lijst hello Azure Database voor de MySQL-databases
Op de server Hallo **overzicht** blade Schuif omlaag totdat u de database Hallo ziet tegel op Hallo onder. Alle Hallo databases worden vermeld in de tabel Hallo. Klik op **verwijderen** opdracht knop tooopen Hallo verwijderen bevestiging blade.

![weergeven-databases](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a>Details weergeven van een Azure-Database voor de MySQL-server
Klik op **eigenschappen** onder **instellingen** op Hallo server blade geopend Hallo **eigenschappen** blade. U kunt vervolgens alle informatie over het Hallo-server weergeven.

## <a name="next-steps"></a>Volgende stappen

[Snelstartgids: Azure-Database maken voor de MySQL-server met Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)
