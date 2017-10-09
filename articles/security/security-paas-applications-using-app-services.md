---
title: aaaSecuring PaaS webtoepassingen en mobiele toepassingen met Azure App Services | Microsoft Docs
description: " Meer informatie over Azure App Services aanbevolen beveiligingsprocedures voor het beveiligen van uw PaaS-webtoepassingen en mobiele toepassingen. "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: terrylan
ms.openlocfilehash: 68a741c668efe2157cff114b649e0e287ef196f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-web-and-mobile-applications-using-azure-app-services"></a>PaaS-webtoepassingen en mobiele toepassingen met Azure App Services beveiligen

In dit artikel bespreken we een verzameling van [Azure App Services](https://azure.microsoft.com/services/app-service/) aanbevolen beveiligingsprocedures voor het beveiligen van uw PaaS-webtoepassingen en mobiele toepassingen. Deze aanbevolen procedures zijn afgeleid van onze ervaring met Azure en Hallo ervaringen van klanten, zoals zelf.

## <a name="azure-app-services"></a>Azure App Services
[Azure App Services](../app-service/app-service-value-prop-what-is.md) is een aanbieding PaaS waarmee u web- en mobiele apps voor alle platforms en apparaten maken en toodata overal en op Hallo cloud of on-premises verbinding maken. App-Services omvat Hallo web en mobiel mogelijkheden die werden eerder afzonderlijk verkrijgbaar Azure Websites en Azure Mobile Services. Deze service bevat ook nieuwe mogelijkheden voor het automatiseren van bedrijfsprocessen en het hosten van cloud-API's. Als een geïntegreerde service biedt App-Services een uitgebreide reeks mogelijkheden tooweb, mobiele en integratie scenario's.

meer, Zie overzichten op toolearn [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) en [Web-Apps](../app-service-web/app-service-web-overview.md).

## <a name="best-practices"></a>Aanbevolen procedures

Wanneer u App-Services gebruikt, volgt u deze aanbevolen procedures:

- [Verifiëren via Azure Active Directory (AD)](../app-service-web/web-sites-authentication-authorization.md#authenticate-through-azure-active-directory). App-Services biedt een OAuth 2.0-service voor uw id-provider. OAuth 2.0 richt zich op de client developer eenvoud tijdens het ontwikkelen van specifieke autorisatie stromen voor webtoepassingen, bureaubladtoepassingen en mobiele telefoons. Azure AD maakt gebruik van OAuth 2.0 tooenable u tooauthorize toegang toomobile en web-apps.
- Toegang beperken op basis Hallo nodig tooknow en minimale bevoegdheden beveiligingsprincipes. Beperken van de toegang is van cruciaal belang voor organisaties die tooenforce beveiligingsbeleid voor toegang tot gegevens willen. Op rollen gebaseerde toegangsbeheer (RBAC) kan worden gebruikt tooassign machtigingen toousers, groepen en toepassingen op een bepaalde scope. toolearn meer informatie over het verlenen van gebruikers toegang krijgen tot tooapplications, Zie [aan de slag met toegangsbeheer](../active-directory/role-based-access-control-what-is.md).
- Beveiligen van uw sleutels. Het maakt niet uit hoe goed is de beveiliging van uw als u uw abonnement sleutels verliest. Met Azure Key Vault kunt u de cryptografische sleutels en geheimen beveiligen die door cloudtoepassingen en -services worden gebruikt. U kunt met Key Vault sleutels en geheimen versleutelen (zoals verificatiesleutels, opslagaccountsleutels, gegevensversleutelingssleutels, PFX-bestanden en wachtwoorden) door gebruik te maken van sleutels die worden beveiligd met HSM's. Voor extra zekerheid kunt u de sleutels importeren of genereren in HSM's. Zie [Azure Key Vault](../key-vault/key-vault-whatis.md) toolearn meer. U kunt ook Sleutelkluis toomanage TLS-certificaten gebruiken met automatisch verlengen.
- Binnenkomende bron-IP-adressen beperken. [App-serviceomgeving](../app-service-web/app-service-app-service-environment-intro.md) beschikt over een virtueel netwerk integratie-functie waarmee u binnenkomende bron-IP-adressen via netwerkbeveiligingsgroepen (nsg's) beperken. Als u niet bekend bent met Azure Virtual Networks (vnet's), is dit een functie waarmee u veel van uw Azure-resources in een internet-routeerbaar netwerk dat u beheert de toegang tot tooplace. toolearn meer, Zie [uw app integreren met een Azure Virtual Network](../app-service-web/web-sites-integrate-with-vnet.md).

## <a name="next-steps"></a>Volgende stappen
In dit artikel geïntroduceerd tooa verzameling van App Services aanbevolen beveiligingsprocedures voor het beveiligen van uw PaaS-webtoepassingen en mobiele toepassingen. toolearn meer informatie over het beveiligen van uw PaaS-implementaties, Zie:

- [PaaS-implementaties beveiligen](security-paas-deployments.md)
- [PaaS-webtoepassingen en mobiele toepassingen met behulp van Azure SQL Database en SQL Data Warehouse beveiligen](security-paas-applications-using-sql.md)
