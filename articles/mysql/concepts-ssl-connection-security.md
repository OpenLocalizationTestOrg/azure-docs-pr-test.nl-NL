---
title: SSL-verbindingen voor de Azure-Database voor MySQL | Microsoft Docs
description: Informatie voor het configureren van Azure-Database voor MySQL en de bijbehorende toepassingen juist gebruik van SSL-verbindingen
services: mysql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b03b3a2dbfad92cc0cfa84777b38ddff90452cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a><span data-ttu-id="493f3-103">SSL-verbindingen in Azure voor MySQL-Database</span><span class="sxs-lookup"><span data-stu-id="493f3-103">SSL connectivity in Azure Database for MySQL</span></span>
<span data-ttu-id="493f3-104">Azure MySQL-Database ondersteunt verbindingen van uw database-server met clienttoepassingen met Secure Sockets Layer (SSL).</span><span class="sxs-lookup"><span data-stu-id="493f3-104">Azure Database for MySQL supports connecting your database server to client applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="493f3-105">Afdwingen van SSL-verbindingen tussen uw database-server en client-toepassingen beschermt tegen 'man-in het midden'-aanvallen door het versleutelen van de gegevensstroom tussen de server en uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="493f3-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" attacks by encrypting the data stream between the server and your application.</span></span>

## <a name="default-settings"></a><span data-ttu-id="493f3-106">Standaard-instellingen</span><span class="sxs-lookup"><span data-stu-id="493f3-106">Default settings</span></span>
<span data-ttu-id="493f3-107">Standaard wordt de database-service zo dat SSL-verbindingen vereisen bij het verbinden met MySQL.</span><span class="sxs-lookup"><span data-stu-id="493f3-107">By default, the database service should be configured to require SSL connections when connecting to MySQL.</span></span>  <span data-ttu-id="493f3-108">Het verdient aanbeveling te voorkomen dat de SSL-optie indien mogelijk uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="493f3-108">It is recommended avoid disabling the SSL option whenever possible.</span></span> 

<span data-ttu-id="493f3-109">Bij het inrichten van een nieuwe Azure-Database voor de MySQL-server via de Azure portal en CLI kan afdwinging van SSL-verbindingen is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="493f3-109">When provisioning a new Azure Database for MySQL server through the Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="493f3-110">Verbindingsreeksen die vooraf zijn gedefinieerd in de instellingen 'Verbindingsreeksen' onder uw server in de Azure portal omvatten ook de vereiste parameters voor algemene talen verbinding maken met uw database-server met behulp van SSL.</span><span class="sxs-lookup"><span data-stu-id="493f3-110">Likewise, connection strings that are pre-defined in the "Connection Strings" settings under your server in the Azure portal include the required parameters for common languages to connect to your database server using SSL.</span></span> <span data-ttu-id="493f3-111">De parameter SSL varieert op basis van de connector, bijvoorbeeld ' ssl = true ' of ' sslmode = vereisen ' of ' sslmode = vereist ' en andere variaties.</span><span class="sxs-lookup"><span data-stu-id="493f3-111">The SSL parameter varies based on the connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

<span data-ttu-id="493f3-112">Voor informatie over het in- of uitschakelen van SSL-verbinding bij het ontwikkelen van toepassing, raadpleegt u [SSL configureren](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="493f3-112">To learn how to enable or disable SSL connection when developing application, please refer to [How to configure SSL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="493f3-113">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="493f3-113">Next steps</span></span>
[<span data-ttu-id="493f3-114">Verbindingsbibliotheken voor Azure-Database voor MySQL</span><span class="sxs-lookup"><span data-stu-id="493f3-114">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)
