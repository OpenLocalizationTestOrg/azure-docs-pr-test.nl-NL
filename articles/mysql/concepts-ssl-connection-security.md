---
title: aaaSSL connectiviteit voor de Azure-Database voor MySQL | Microsoft Docs
description: Informatie voor het configureren van Azure-Database voor MySQL en de bijbehorende toepassingen tooproperly SSL-verbindingen gebruiken
services: mysql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6fca7c88fc0f1fd6058d68fcff90fd409abd97a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a>SSL-verbindingen in Azure voor MySQL-Database
Azure MySQL-Database ondersteunt verbindingen van uw server tooclient databasetoepassingen met Secure Sockets Layer (SSL). Afdwingen van SSL-verbindingen tussen uw database-server en client-toepassingen beschermt tegen 'man-in Hallo middle'-aanvallen door het versleutelen van de gegevensstroom Hallo tussen Hallo-server en uw toepassing.

## <a name="default-settings"></a>Standaard-instellingen
Standaard moet Hallo databaseservice geconfigureerde toorequire SSL-verbindingen tijdens het verbinden van tooMySQL.  Het is raadzaam voorkomen Hallo SSL-optie indien mogelijk uitschakelen. 

Bij het inrichten van een nieuwe Azure-Database voor de MySQL-server via hello Azure-portal en CLI kan afdwinging van SSL-verbindingen is standaard ingeschakeld. 

Evenzo bevatten verbindingsreeksen die vooraf zijn gedefinieerd in Hallo 'Verbindingsreeksen' instellingen onder uw server in Azure-portal Hallo Hallo vereiste parameters voor algemene talen tooconnect tooyour database-server via SSL. Hallo SSL parameter varieert op basis van Hallo-connector, bijvoorbeeld ' ssl = true ' of ' sslmode = vereisen ' of ' sslmode = vereist ' en andere variaties.

hoe SSL tooenable of disable-verbinding bij het ontwikkelen van toepassing, Raadpleeg te toolearn[hoe tooconfigure SSL](howto-configure-ssl.md).

## <a name="next-steps"></a>Volgende stappen
[Verbindingsbibliotheken voor Azure-Database voor MySQL](concepts-connection-libraries.md)
