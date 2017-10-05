---
title: PaaS-webtoepassingen en mobiele toepassingen met Azure App Services beveiligen | Microsoft Docs
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
ms.openlocfilehash: 0738522250f1863c9584936a2d2b2c7a0a823c8c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="securing-paas-web-and-mobile-applications-using-azure-app-services"></a>PaaS-webtoepassingen en mobiele toepassingen met Azure App Services beveiligen

In dit artikel bespreken we een verzameling van [Azure App Services](https://azure.microsoft.com/services/app-service/) aanbevolen beveiligingsprocedures voor het beveiligen van uw PaaS-webtoepassingen en mobiele toepassingen. Deze aanbevolen procedures zijn afgeleid van onze ervaring met Azure en de ervaringen van klanten zoals zelf.

## <a name="azure-app-services"></a>Azure App Services
[Azure App Services](../app-service/app-service-value-prop-what-is.md) is een PaaS die aanbieding kunt u web- en mobiele apps voor alle platforms en apparaten maken en verbinding maken met gegevens overal en in de cloud of on-premises. App-Services omvat het web en mobiel mogelijkheden die werden eerder afzonderlijk verkrijgbaar Azure Websites en Azure Mobile Services. Deze service bevat ook nieuwe mogelijkheden voor het automatiseren van bedrijfsprocessen en het hosten van cloud-API's. Als een geïntegreerde service brengt App Services een groot aantal mogelijkheden voor web-, mobiele en integratiescenario's.

Zie voor meer informatie, overzichten op [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) en [Web-Apps](../app-service-web/app-service-web-overview.md).

## <a name="best-practices"></a>Aanbevolen procedures

Wanneer u App-Services gebruikt, volgt u deze aanbevolen procedures:

- [Verifiëren via Azure Active Directory (AD)](../app-service-web/web-sites-authentication-authorization.md#authenticate-through-azure-active-directory). App-Services biedt een OAuth 2.0-service voor uw id-provider. OAuth 2.0 richt zich op de client developer eenvoud tijdens het ontwikkelen van specifieke autorisatie stromen voor webtoepassingen, bureaubladtoepassingen en mobiele telefoons. Azure AD maakt gebruik van OAuth 2.0, zodat u toegang tot mobiele en webtoepassingen autoriseren.
- De toegang op basis van de noodzaak om te weten en minimale bevoegdheden beveiligingsprincipes beperken. Beperken van de toegang is van cruciaal belang voor organisaties die willen beveiligingsbeleid instellen voor toegang tot gegevens. Op rollen gebaseerde toegangsbeheer (RBAC) kan worden gebruikt om machtigingen te wijzen aan gebruikers, groepen en toepassingen op een bepaalde scope. Zie voor meer informatie over gebruikers geen toegang verlenen tot toepassingen, [aan de slag met toegangsbeheer](../active-directory/role-based-access-control-what-is.md).
- Beveiligen van uw sleutels. Het maakt niet uit hoe goed is de beveiliging van uw als u uw abonnement sleutels verliest. Met Azure Key Vault kunt u de cryptografische sleutels en geheimen beveiligen die door cloudtoepassingen en -services worden gebruikt. U kunt met Key Vault sleutels en geheimen versleutelen (zoals verificatiesleutels, opslagaccountsleutels, gegevensversleutelingssleutels, PFX-bestanden en wachtwoorden) door gebruik te maken van sleutels die worden beveiligd met HSM's. Voor extra zekerheid kunt u de sleutels importeren of genereren in HSM's. Zie [Azure Key Vault](../key-vault/key-vault-whatis.md) voor meer informatie. U kunt ook Sleutelkluis gebruiken voor het beheren van de TLS-certificaten met automatische verlenging.
- Binnenkomende bron-IP-adressen beperken. [App-serviceomgeving](../app-service-web/app-service-app-service-environment-intro.md) beschikt over een virtueel netwerk integratie-functie waarmee u binnenkomende bron-IP-adressen via netwerkbeveiligingsgroepen (nsg's) beperken. Als u niet bekend bent met Azure Virtual Networks (vnet's), is dit een functie waarmee u veel van uw Azure-resources in een internet-routeerbaar netwerk die u toegang tot te plaatsen. Zie voor meer informatie, [uw app integreren met een Azure Virtual Network](../app-service-web/web-sites-integrate-with-vnet.md).

## <a name="next-steps"></a>Volgende stappen
In dit artikel is geïntroduceerd aan een verzameling van App Services aanbevolen beveiligingsprocedures voor het beveiligen van uw PaaS-webtoepassingen en mobiele toepassingen. Zie voor meer informatie over het beveiligen van uw PaaS-implementaties:

- [PaaS-implementaties beveiligen](security-paas-deployments.md)
- [PaaS-webtoepassingen en mobiele toepassingen met behulp van Azure SQL Database en SQL Data Warehouse beveiligen](security-paas-applications-using-sql.md)
