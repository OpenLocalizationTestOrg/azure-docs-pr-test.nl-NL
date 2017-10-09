---
title: aaaPartner integratie in Azure Security Center | Microsoft Docs
description: Meer informatie over hoe Azure Security Center met partners tooenhance integreert algehele beveiliging van uw Azure-resources.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 6af354da-f27a-467a-8b7e-6cbcf70fdbcb
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: yurid
ms.openlocfilehash: 3621335730a076721cb3c23788a47be50aa8fc73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="partner-integration-in-azure-security-center"></a>Partnerintegratie in Azure Security Center

In dit artikel wordt beschreven hoe Azure Security Center integreert met partners toohelp verbetering van de algehele beveiliging. Security Center biedt een geïntegreerde ervaring in Azure en maakt gebruik van hello Azure Marketplace voor partner certificering en facturering.

> [!NOTE] 
> Security Center gebruikt vanaf juni 2017 Hallo Microsoft Monitoring Agent toocollect en store-gegevens. Zie [Migratie van Azure Security Center-platform](security-center-platform-migration.md) voor meer informatie. Hallo-informatie in dit artikel beschrijft Security Center functionaliteit na de overgang toohello Microsoft Monitoring Agent.
>

## <a name="why-deploy-partner-solutions-from-security-center"></a>Waarom partneroplossingen uit Security Center implementeren

Er zijn vier hoofdredenen tooleverage partner integratie in Security Center:

- **Eenvoudige implementatie**. Een partneroplossing implementeren door de volgende Hallo Security Center-aanbeveling is veel eenvoudiger. Hallo-implementatieproces kan volledig worden geautomatiseerd met behulp van een standaardtopologie voor installatie en het netwerk. Klanten kunnen ook kiezen voor een semi-geautomatiseerde optie voor meer flexibiliteit en aanpassing.
- **Geïntegreerde detectie**. Beveiligingsgebeurtenissen van partneroplossingen worden automatisch verzameld, samengevoegd en weergegeven als meldingen en incidenten in Security Center. Deze gebeurtenissen worden ook zekering met detecties van andere bronnen tooprovide geavanceerde mogelijkheden voor detectie van dreigingen.
- **Geïntegreerde status- en beheercontrole**. Klanten kunnen geïntegreerde health gebeurtenissen toomonitor alle partneroplossingen gebruiken in een oogopslag. Basic-management is beschikbaar met eenvoudige toegang tooadvanced setup uit met behulp van de partneroplossing Hallo.
- **Exporteren van tooSIEM**. Klanten alle Security Center kunnen exporteren en partner waarschuwt gemeenschappelijk gebeurtenis-indeling (CEF) tooon-premises Security Information en Event Management SIEM ()-systemen met behulp van Azure-logboekanalyse-integratie (preview).


## <a name="partners-that-integrate-with-security-center"></a>Partners die zijn geïntegreerd met Security Center

Security Center is momenteel geïntegreerd met deze oplossingen:

- Eindpuntbeveiliging ([Trend Micro](https://help.deepsecurity.trendmicro.com/azure-marketplace-getting-started-with-deep-security.html), Symantec en [Microsoft Antimalware for Azure Cloud Services and Virtual Machines](https://docs.microsoft.com/azure/security/azure-security-antimalware)) 
- Firewall voor webtoepassingen ([Barracuda](https://www.barracuda.com/products/webapplicationfirewall), [F5](https://support.f5.com/kb/en-us/products/big-ip_asm/manuals/product/bigip-ve-web-application-firewall-microsoft-azure-12-0-0.html), [Imperva](https://www.imperva.com/Products/WebApplicationFirewall-WAF), [Fortinet](https://www.fortinet.com/resources.html?limit=10&search=&document-type=data-sheets) en [Azure Application Gateway](https://azure.microsoft.com/blog/azure-web-application-firewall-waf-generally-available/)) 
- Firewall van de volgende generatie ([Check Point](https://www.checkpoint.com/products/vsec-microsoft-azure/), [Barracuda](https://campus.barracuda.com/product/nextgenfirewallf/article/NGF/AzureDeployment/), [Fortinet](http://docs.fortinet.com/d/fortigate-fortios-handbook-the-complete-guide-to-fortios-5.2) en [Cisco](http://www.cisco.com/c/en/us/td/docs/security/firepower/quick_start/azure/ftdv-azure-qsg.html)) 
- Evaluatie van beveiligingsproblemen ([Qualys](https://www.qualys.com/public-clouds/microsoft-azure/))  

Security Center wordt gedurende een periode, vouw Hallo aantal partners binnen deze categorieën en nieuwe categorieën toevoegen. 

## <a name="deploy-a-partner-solution"></a>Een partneroplossing implementeren

Op basis van Hallo-instellingen van uw Azure-omgeving en het Hallo-beveiligingsbeleid die u hebt gedefinieerd, aanbevelen Security Center die u een partneroplossing implementeert. Hallo Security Center aanbevelingen begeleidt u bij Hallo proces van selecteren en de installatie van een partneroplossing. Hallo kan algehele implementatie-ervaring afwijken, afhankelijk van Hallo type oplossing en de partner die u gebruikt. Zie voor meer informatie Hallo artikelen te volgen:

- [Eindpuntbeveiliging installeren](security-center-install-endpoint-protection.md)
- [Een firewall voor webtoepassingen toevoegen](security-center-add-web-application-firewall.md)
- [Een firewall van de volgende generatie toevoegen](security-center-add-next-generation-firewall.md)
- [Evaluatie van beveiligingsproblemen is niet geïnstalleerd](security-center-vulnerability-assessment-recommendations.md)

## <a name="manage-partner-solutions"></a>Partneroplossingen beheren

Na de implementatie tooview informatie over status van de oplossing Hallo Hallo en elementaire informatie over beheertaken uitvoeren op Hallo **Security Center** blade, selecteer Hallo **partneroplossingen** optie. Raadpleeg [Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) voor meer informatie over het beheren van partneroplossingen in Security Center.

![Partnerintegratie](./media/security-center-partner-integration/security-center-partner-integration-fig1-new2.png)

> [!NOTE]
> Symantec endpoint protection-ondersteuning is beperkt toodiscovery. Er zijn geen statuswaarschuwingen beschikbaar.
>

## <a name="see-also"></a>Zie ook

In dit artikel hebt u geleerd hoe toointegrate partneroplossingen in Azure Security Center. toolearn meer informatie over Security Center, Zie Hallo artikelen te volgen:

* [Plannings- en bedieningsgids voor Security Center](security-center-planning-and-operations-guide.md)
* [Beheren en hierop reageren toosecurity waarschuwingen in Security Center](security-center-managing-and-responding-alerts.md)
* [Beveiligingswaarschuwingen per type in Security Center](security-center-alerts-type.md)
* [Beveiligingsstatus controleren in Security Center](security-center-monitoring.md). Meer informatie over hoe toomonitor Hallo status van uw Azure-resources.
* [Partneroplossingen controleren met Security Center](security-center-partner-solutions.md). Meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md). Toofrequently van antwoorden op veelgestelde vragen over met behulp van Hallo-service ophalen.
* [Azure-beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/). Raadpleeg de blogberichten over beveiliging en naleving in Azure.
