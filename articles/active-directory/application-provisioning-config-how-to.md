---
title: aaaHow tooconfigure gebruikers inrichten tooan Azure AD-galerie toepassing | Microsoft Docs
description: Hoe kunt u snel uitgebreide gebruikersaccount inrichten en tooapplications al wordt vermeld in de galerie van Azure AD-toepassing hello opheffen van inrichting configureren
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 2c28e59a3ac8f221ed93b2f6b0b1221f7604af23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-user-provisioning-tooan-azure-ad-gallery-application"></a>Hoe tooconfigure gebruiker tooan Azure AD-galerie toepassing inrichten

*Het inrichten van het account* wordt Hallo van maken, bijwerken en/of account gebruikersrecords in lokale opgeslagen gebruikersprofiel van de toepassing uit te schakelen. De meeste cloud en SaaS-toepassingen opslaan Hallo gebruikers rollen en machtigingen die in hun eigen lokale opgeslagen gebruikersprofiel en aanwezigheid van dergelijke een gebruikersrecord in hun lokale archief is *vereist* voor eenmalige aanmelding en toegang toowork.

Hallo in hello Azure-portal, **inrichten** tabblad in het linkernavigatievenster Hallo voor een Enterprise-App wordt weergegeven welke inrichting modi voor die app worden ondersteund. Dit kan een van twee waarden zijn:

## <a name="configuring-an-application-for-manual-provisioning"></a>Configureren van een toepassing voor handmatige inrichting

*Handmatige* inrichting betekent dat gebruikersaccounts handmatig met Hallo methoden van de app moeten worden gemaakt. Dit kan betekenen aan te melden bij een portal beheerdersrechten voor die app en het toevoegen van gebruikers met behulp van een webgebaseerde gebruikersinterface. Of het een spreadsheet met account-details met een mechanisme dat is opgegeven door de toepassing kan uploaden. Raadpleeg de documentatie van Hallo opgegeven door het Hallo-app of neem contact op met Hallo app developer toodetermine wat mechanismen beschikbaar zijn.

Handmatige Hallo alleen de modus weergegeven voor een bepaalde toepassing, betekent dit dat er geen automatische Azure AD connector inrichting is gemaakt voor Hallo app nog. Of het Hallo-app biedt geen ondersteuning voor Hallo vereiste gebruiker management-API bij welke toobuild een geautomatiseerde inrichting connector betekent.

Als u ondersteuning voor automatische inrichting voor een bepaalde app toorequest wilt, kunt u een van de aanvraag op invullen <http://aka.ms/aadapprequest>.

## <a name="configuring-an-application-for-automatic-provisioning"></a>Een toepassing configureren voor automatische inrichting

*Automatische* betekent dat een Azure AD connector inrichting is ontwikkeld voor deze toepassing. Zie voor meer informatie over het Hallo Azure AD-service en hoe het werkt, inrichting [gebruikersaanvragen automatiseren en Deprovisioning tooSaaS toepassingen met Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).

Voor meer informatie over hoe tooprovision specifieke gebruikers en groepen tooan toepassing, Zie [het beheren van gebruikers account inrichten voor zakelijke apps](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).

werkelijke stappen vereist tooenable Hallo en configureren van automatische inrichting variëren afhankelijk van de toepassing hello.

>[!NOTE]
>U moet eerst setup zelfstudie specifieke toosetting up inrichting voor uw toepassing hello en na deze stappen tooconfigure zowel Hallo-app en Azure AD toocreate Hallo inrichting verbinding vinden. 
>
>

App-zelfstudies kunnen worden gevonden op [lijst zelfstudies over het SaaS-Apps met Azure Active Directory tooIntegrate](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).

Een tooconsider wat belangrijk is bij het instellen van de inrichting tooreview Hallo kenmerktoewijzingen en werkstromen die welke gebruiker (of groep) eigenschappen stroom van Azure AD-toepassing voor toohello definiëren en configureren. Dit omvat Hallo 'overeenkomende eigenschap' instelt met gebruikte toouniquely worden geïdentificeerd en overeen met gebruikers/groepen tussen Hallo twee systemen. Voor meer informatie over dit belangrijk proces.

## <a name="next-steps"></a>Volgende stappen
[Gebruikers inrichten kenmerktoewijzingen voor SaaS-toepassingen in Azure Active Directory aanpassen](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)

