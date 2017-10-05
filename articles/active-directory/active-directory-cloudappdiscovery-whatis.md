---
title: Zoeken naar niet-beheerde cloud-toepassingen met Cloud App Discovery | Microsoft Docs
description: Bevat informatie over het zoeken en beheren van toepassingen met Cloud App Discovery, wat zijn de voordelen en hoe het werkt.
services: active-directory
keywords: cloud app discovery, het beheren van toepassingen
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: db968bf5-22ae-489f-9c3e-14df6e1fef0a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 6284ff5bac8edbc19561d0916adef153526dfbe3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a>Cloud-toepassingen zoeken die niet worden beheerd met Cloud App Discovery
## <a name="overview"></a>Overzicht
In moderne ondernemingen zijn IT-afdelingen vaak niet op de hoogte van alle cloudtoepassingen die leden van hun organisatie gebruikmaken voor hun werk. Het is gemakkelijk om te zien waarom beheerders zou twijfels hebt over niet-geautoriseerde toegang tot zakelijke gegevens, mogelijk gegevenslekken en andere beveiligingsrisico's. Dit gebrek aan bewustzijn over kunt maken met het maken van een plan voor het afhandelen van deze beveiligingsrisico's afschrikken.

Cloud App Discovery is een functie van Azure Active Directory (AD) Premium waarmee u voor het detecteren van cloud-toepassingen wordt gebruikt door mensen in uw organisatie.

**Met Cloud App Discovery, kunt u het volgende doen:**

* Zoeken naar de cloudtoepassingen die worden gebruikt en dat gebruik meten door het aantal gebruikers, hoeveelheid verkeer of aantal webaanvragen naar de toepassing.
* De gebruikers die van een toepassing gebruikmaken te identificeren.
* Exporteer gegevens voor offline-analyse.
* Zorg ervoor dat deze toepassingen onder het IT-beheer en eenmalige aanmelding inschakelen voor gebruikersbeheer.

## <a name="how-it-works"></a>Hoe werkt het?
1. Toepassing gebruik agents zijn geïnstalleerd op de computers van gebruikers.
2. De gebruiksgegevens van de toepassing wordt vastgelegd door de agents is verzonden via een beveiligde, gecodeerde kanaal naar de cloud app discovery-service.
3. De Cloud App Discovery-service evalueert de gegevens en genereert rapporten.

![Cloud App Discovery-diagram](./media/active-directory-cloudappdiscovery/cad01.png)

Aan de slag met Cloud App Discovery Zie [ophalen van de slag met Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)

## <a name="related-articles"></a>Verwante artikelen:
* [Cloud App Discovery beveiligings- en privacyoverwegingen](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [Cloud App Discovery Group Policy Deployment Guide](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [Implementatiehandleiding voor cloud App Discovery System Center](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [Cloud App Discovery-registerinstellingen voor proxyservers met aangepaste poorten](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [Cloud App Discovery Agent Changelog](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [Veelgestelde vragen over de cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)

