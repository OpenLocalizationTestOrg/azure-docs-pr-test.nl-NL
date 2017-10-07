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
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a><span data-ttu-id="b1b7a-103">SSL-verbindingen in Azure voor MySQL-Database</span><span class="sxs-lookup"><span data-stu-id="b1b7a-103">SSL connectivity in Azure Database for MySQL</span></span>
<span data-ttu-id="b1b7a-104">Azure MySQL-Database ondersteunt verbindingen van uw server tooclient databasetoepassingen met Secure Sockets Layer (SSL).</span><span class="sxs-lookup"><span data-stu-id="b1b7a-104">Azure Database for MySQL supports connecting your database server tooclient applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="b1b7a-105">Afdwingen van SSL-verbindingen tussen uw database-server en client-toepassingen beschermt tegen 'man-in Hallo middle'-aanvallen door het versleutelen van de gegevensstroom Hallo tussen Hallo-server en uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="b1b7a-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

## <a name="default-settings"></a><span data-ttu-id="b1b7a-106">Standaard-instellingen</span><span class="sxs-lookup"><span data-stu-id="b1b7a-106">Default settings</span></span>
<span data-ttu-id="b1b7a-107">Standaard moet Hallo databaseservice geconfigureerde toorequire SSL-verbindingen tijdens het verbinden van tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="b1b7a-107">By default, hello database service should be configured toorequire SSL connections when connecting tooMySQL.</span></span>  <span data-ttu-id="b1b7a-108">Het is raadzaam voorkomen Hallo SSL-optie indien mogelijk uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="b1b7a-108">It is recommended avoid disabling hello SSL option whenever possible.</span></span> 

<span data-ttu-id="b1b7a-109">Bij het inrichten van een nieuwe Azure-Database voor de MySQL-server via hello Azure-portal en CLI kan afdwinging van SSL-verbindingen is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="b1b7a-109">When provisioning a new Azure Database for MySQL server through hello Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="b1b7a-110">Evenzo bevatten verbindingsreeksen die vooraf zijn gedefinieerd in Hallo 'Verbindingsreeksen' instellingen onder uw server in Azure-portal Hallo Hallo vereiste parameters voor algemene talen tooconnect tooyour database-server via SSL.</span><span class="sxs-lookup"><span data-stu-id="b1b7a-110">Likewise, connection strings that are pre-defined in hello "Connection Strings" settings under your server in hello Azure portal include hello required parameters for common languages tooconnect tooyour database server using SSL.</span></span> <span data-ttu-id="b1b7a-111">Hallo SSL parameter varieert op basis van Hallo-connector, bijvoorbeeld ' ssl = true ' of ' sslmode = vereisen ' of ' sslmode = vereist ' en andere variaties.</span><span class="sxs-lookup"><span data-stu-id="b1b7a-111">hello SSL parameter varies based on hello connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

<span data-ttu-id="b1b7a-112">hoe SSL tooenable of disable-verbinding bij het ontwikkelen van toepassing, Raadpleeg te toolearn[hoe tooconfigure SSL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="b1b7a-112">toolearn how tooenable or disable SSL connection when developing application, please refer too[How tooconfigure SSL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1b7a-113">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b1b7a-113">Next steps</span></span>
[<span data-ttu-id="b1b7a-114">Verbindingsbibliotheken voor Azure-Database voor MySQL</span><span class="sxs-lookup"><span data-stu-id="b1b7a-114">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)
