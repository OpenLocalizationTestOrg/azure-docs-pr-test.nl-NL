---
title: aaaOperations Management Suite beveiligings- en Audit oplossing basislijn | Microsoft Docs
description: Dit document wordt uitgelegd hoe toouse OMS beveiligings- en Audit oplossing tooperform een basislijn beoordeling van alle bewaakte computers voor naleving en beveiliging doel.
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: ea52408cb9d2598728fe3826a946067e1c99318f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Basislijnevaluatie in de oplossing Beveiliging en controle in Operations Management Suite
Dit document helpt u toouse [Operations Management Suite (OMS) beveiligings- en Audit oplossing](operations-management-suite-overview.md) basislijn assessment mogelijkheden tooaccess Hallo beveiligingsstatus van uw bewaakte resources.

## <a name="what-is-baseline-assessment"></a>Wat is basislijnevaluatie?
Microsoft definieert samen met brancheorganisaties en overheidsinstanties overal ter wereld een Windows-configuratie die garandeert dat maximaal beveiligde serverimplementaties worden gebruikt. Deze configuratie bestaat uit een verzameling registersleutels, controlebeleidsinstellingen en beveiligingsbeleidsinstellingen, gecombineerd met waarden die door Microsoft voor deze instellingen worden aanbevolen. Deze verzameling staat bekend als de beveiligingsbasislijn. Met de functie van Beveiliging en controle in OMS om een basislijnevaluatie uit te voeren, kunt u al uw computers naadloos scannen om te zien of ze aan nalevingsvereisten voldoen. 

Er zijn drie soorten regels:

* **Registerregels**: deze controleren of registersleutels juist zijn ingesteld.
* **Controlebeleidsregels**: regels die betrekking hebben op uw controlebeleid.
* **Beleidsregels voor beveiliging**: regels over Hallo gebruikersmachtigingen op Hallo-machine.

> [!NOTE]
> Lees [gebruik OMS beveiliging tooassess Hallo beveiliging Configuratiebasislijn](https://blogs.technet.microsoft.com/msoms/2016/08/12/use-oms-security-to-assess-the-security-configuration-baseline/) voor een kort overzicht van deze functie.
> 
> 

## <a name="security-baseline-assessment"></a>Evaluatie van de beveiligingsbasislijn
U kunt uw huidige beveiligingsevaluatie voor een basislijn voor alle computers die worden bewaakt door OMS beveiligings- en Audit met Hallo dashboard bekijken.  Volgende stappen tooaccess Hallo beveiliging basislijn assessment dashboard Hallo uitvoeren:

1. In Hallo **Microsoft Operations Management Suite** hoofddashboard, klikt u op **beveiligings- en Audit** tegel.
2. In Hallo **beveiligings- en Audit** dashboard, klikt u op **basislijn Assessment** onder **beveiligingsdomeinen**. Hallo **beveiligingsevaluatie basislijn** dashboard wordt weergegeven zoals in Hallo installatiekopie te volgen:
   
    ![Basislijnevaluatie in Beveiliging en controle in OMS](./media/oms-security-baseline/oms-security-baseline-fig1.png)

Dit dashboard is onderverdeeld in drie belangrijke gebieden:

* **Computers vergeleken toobaseline**: in deze sectie geeft een samenvatting van het aantal computers die zijn geopend en het percentage van computers die zijn geslaagd voor beoordeling Hallo HALLO hallo. Dit biedt ook Hallo bovenste 10-computers en Hallo percentage resultaat Hallo-evaluatie.
* **Status van de regels vereist**: in deze sectie heeft Hallo opzet toobring bewust te maken van regels Hallo is mislukt op ernst en regels per type is mislukt. Door het opzoeken van de eerste toohello-grafiek die u snel identificeren kunt als de meeste Hallo is mislukt voor regels zijn kritiek, of niet. Dit biedt ook een lijst met Hallo bovenste 10 mislukte regels en de ernst. Hallo tweede grafiek toont Hallo-type van de regel die is mislukt tijdens het Hallo-evaluatie. 
* **Computers met ontbrekende basislijn assessment**: in deze sectie lijst Hallo-computers die zijn niet toegankelijk vanwege toooperating system incompatibiliteit of storingen. 

### <a name="accessing-computers-compared-toobaseline"></a>Toegang tot computers vergeleken toobaseline
In het ideale geval zijn alle uw computers zijn compatibel met Hallo basislijn beveiligingsevaluatie. In sommige omstandigheden is dat echter niet het geval. Als onderdeel van Hallo management beveiligingsproces is het belangrijk tooinclude Hallo-computers die niet alle security assessment tests zijn geslaagd toopass controleren. Een snelle manier toovisualize die door de optie Hallo **Computers toegankelijk** zich in Hallo **Computers vergeleken toobaseline** sectie. U ziet Hallo logboek weergeeft Hallo lijst met zoekresultaten van computers zoals wordt weergegeven in het volgende scherm Hallo:

![Resultaten van geopende computers](./media/oms-security-baseline/oms-security-baseline-fig2.png)

Hallo zoekresultaat wordt in een tabel, waarbij de eerste kolom Hallo Hallo computernaam heeft en tweede kleur Hallo Hallo aantal regels die niet weergegeven. tooretrieve hello informatie met betrekking tot Hallo-type van de regel die is mislukt, klikt u op in het aantal mislukte regels naast de naam van de computer Hallo Hallo. Hier ziet u een resultaat vergelijkbaar toohello een in Hallo volgende afbeelding wordt weergegeven:

![Details van resultaten van geopende computers](./media/oms-security-baseline/oms-security-baseline-fig3.png)

In dit zoekresultaat u hebt Hallo totaal gebruikte regels, Hallo aantal kritieke regels die niet zijn geslaagd, Hallo waarschuwingsregels en Hallo regels met gegevens is mislukt.

### <a name="accessing-required-rules-status"></a>Status van toegang tot vereiste regels
Nadat u hebt verkregen Hallo informatie met betrekking tot Hallo percentage aantal computers dat Hallo assessment doorgegeven, kunt u tooobtain meer informatie over welke regels volgens toohello kritisch geval mislukken. Deze visualisatie helpt u tooprioritize welke computers moeten worden verholpen eerste tooensure worden deze in de volgende evaluatie Hallo compatibel. Beweeg de muisaanwijzer over Hallo essentieel onderdeel van Hallo grafiek zich in Hallo **regels op ernst kan** tegel onder **regels status vereist** en klik erop. Hier ziet u een resultaat vergelijkbaar toohello scherm te volgen:

![Mislukte regels per gegevens over ernst](./media/oms-security-baseline/oms-security-baseline-fig4.png) 

In dit logboek resultaat ziet u Hallo-type van de basislijn-regel die is mislukt, Hallo beschrijving van deze regel en Hallo Common Configuration Enumeration (CCE)-ID van deze regel. Deze kenmerken moet voldoende tooperform een toofix corrigerende maatregelen dit probleem op de doelcomputer Hallo.

> [!NOTE]
> Toegang tot Hallo voor meer informatie over CCE [National Vulnerability Database](https://nvd.nist.gov/cce/index.cfm).
> 
> 

### <a name="accessing-computers-missing-baseline-assessment"></a>Computers openen waarop de evaluatie van de basislijn ontbreekt
OMS ondersteunt Hallo domeinlid en domeincontroller basislijn profiel op Windows Server 2008 R2 up tooWindows Server 2012 R2. De basislijn voor Windows Server 2016 is nog niet helemaal klaar en wordt toegevoegd zodra deze is gepubliceerd. Alle andere besturingssystemen gescand via OMS beveiligings- en Audit basislijn beoordeling wordt weergegeven onder Hallo **Computers met ontbrekende basislijn assessment** sectie.

## <a name="see-also"></a>Zie ook
In dit document hebt u meer kunnen lezen over het evalueren van de basislijn door Beveiliging- en controle in OMS. toolearn meer informatie over OMS-beveiliging, Zie Hallo artikelen te volgen:

* [Overzicht van Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Bewaking en reageren tooSecurity waarschuwingen in de beveiliging van Operations Management Suite en Audit-oplossing](oms-security-responding-alerts.md)
* [Resources bewaken in de oplossing Beveiliging en controle van Operations Management Suite ](oms-security-monitoring-resources.md)

