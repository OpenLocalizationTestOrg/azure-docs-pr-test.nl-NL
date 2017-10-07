---
title: Linux-distributies aaaEndorsed | Microsoft Docs
description: Meer informatie over Linux op Azure goedgekeurde distributies, met inbegrip van de richtlijnen voor Ubuntu, CentOS, Oracle en SUSE.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: 2777a526-c260-4cb9-a31a-bdfe1a55fffc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: f006972d4611434c62b72a1d8df60caf753e15f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="linux-on-distributions-endorsed-by-azure"></a>Linux op door Azure goedgekeurde distributies
Partners bieden Linux afbeeldingen in hello Azure Marketplace. We werken met verschillende Linux-community's tooadd nog meer versies toohello goedgekeurde distributielijst. In Hallo tussentijd voor distributies die niet beschikbaar is via Hallo Marketplace, u kunt altijd brengt uw eigen Linux door Hallo richtlijnen op [maken en uploaden van een virtuele harde schijf waarop Hallo Linux-besturingssysteem](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="supported-distributions-and-versions"></a>Ondersteunde distributies en versies
Hallo volgende tabel bevat Hallo Linux-distributies en versies die worden ondersteund in Azure. Raadpleeg te[ondersteuning voor Linux-installatiekopieën in Microsoft Azure](https://support.microsoft.com/en-us/kb/2941892) voor meer informatie gedetailleerde.

Hallo Linux Integration Services (LIS) stuurprogramma's voor Hyper-V en Azure zijn Microsoft bijdraagt rechtstreeks toohello upstream Linux kernel kernelmodules.  Sommige LIS stuurprogramma's zijn ingebouwd in de kernel Hallo distributie van standaard. Oudere distributies die zijn gebaseerd op Red Hat Enterprise (RHEL) / CentOS zijn beschikbaar als een afzonderlijke download op [Linux Integration Services versie 4.1 voor Hyper-V](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409). Zie [Linux kernel vereisten](create-upload-generic.md#linux-kernel-requirements) voor meer informatie over Hallo LIS stuurprogramma's.

Hello Azure Linux Agent al vooraf is geïnstalleerd op Hallo Azure Marketplace-installatiekopieën en bevindt zich normaal gesproken uit Hallo distributie van pakket-opslagplaats. Broncode vindt u op [GitHub](https://github.com/azure/walinuxagent).

| Distributie | Versie | Stuurprogramma's | Agent |
| --- | --- | --- | --- |
| CentOS |CentOS 6.3 + 7.0 + |CentOS 6.3: [LIS downloaden](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409)<p>CentOS 6.4 +: In de kernel |Pakket: In [opslagplaats](http://olcentgbl.trafficmanager.net/openlogic/6/openlogic/x86_64/RPMS/) onder 'WALinuxAgent' <br/>Broncode: [GitHub](https://github.com/Azure/WALinuxAgent) |
| [CoreOS](https://coreos.com/docs/running-coreos/cloud-providers/azure/) |494.4.0+ |In de kernel |Broncode: [GitHub](https://github.com/coreos/coreos-overlay/tree/master/app-emulation/wa-linux-agent) |
| Debian |Debian 7,9 +, 8.2 + |In de kernel |Pakket: In de opslagplaats onder 'waagent' <br/>Broncode: [GitHub](https://github.com/Azure/WALinuxAgent) |
| Oracle Linux |6.4+, 7.0+ |In de kernel |Pakket: In de opslagplaats onder 'WALinuxAgent' <br/>Broncode: [GitHub](http://go.microsoft.com/fwlink/p/?LinkID=250998) |
| Red Hat Enterprise Linux |RHEL 6.7 +, 7.1 + |In de kernel |Pakket: In de opslagplaats onder 'WALinuxAgent' <br/>Broncode: [GitHub](https://github.com/Azure/WALinuxAgent) |
| SUSE Linux Enterprise |SLES/SLES voor SAP<br>11 SP4<br>12 SP1 +|In de kernel |Pakket:<p> voor 11 in [Cloud: extra](https://build.opensuse.org/project/show/Cloud:Tools) opslagplaats<br>voor 12 opgenomen in de Module 'Openbare Cloud' onder 'python-azure-agent'<br/>Broncode: [GitHub](http://go.microsoft.com/fwlink/p/?LinkID=250998) |
| openSUSE |openSUSE Leap 42,1 + |In de kernel |Pakket: In [Cloud: extra](https://build.opensuse.org/project/show/Cloud:Tools) opslagplaats onder 'python-azure-agent' <br/>Broncode: [GitHub](https://github.com/Azure/WALinuxAgent) |
| Ubuntu |Ubuntu 12.04, 14.04, 16.04, 16,10 |In de kernel |Pakket: In de opslagplaats onder 'walinuxagent' <br/>Broncode: [GitHub](https://github.com/Azure/WALinuxAgent) |

## <a name="partners"></a>Partners

### <a name="coreos"></a>CoreOS
[https://coreos.com/Docs/Running-coreos/cloud-providers/Azure/](https://coreos.com/docs/running-coreos/cloud-providers/azure/)

Van Hallo virtuele CoreOS-website:

*Virtuele CoreOS is ontworpen voor beveiliging, consistentie en betrouwbaarheid. In plaats van de installatie van pakketten via yum of apt, virtuele CoreOS maakt gebruik van Linux containers toomanage uw services op een hoger niveau van abstractie. Een enkele service code en alle afhankelijkheden zijn verpakt in een container die kan worden uitgevoerd op een of meer virtuele CoreOS-machines.*

### <a name="credativ"></a>Credativ
[http://www.credativ.co.uk/credativ-blog/debian-images-Microsoft-Azure](http://www.credativ.co.uk/credativ-blog/debian-images-microsoft-azure)

Credativ is een onafhankelijke advies en services-bedrijf dat gespecialiseerd in het Hallo-ontwikkeling en implementatie van oplossingen voor professional met behulp van gratis software. Als de toonaangevende open source-specialisten heeft Credativ internationale herkenning met veel IT-afdelingen die gebruikmaken van hun ondersteuning. In combinatie met Microsoft wordt Credativ momenteel voorbereid bijbehorende Debian installatiekopieën voor Debian 8 (Jessie) en Debian vóór 7 (Wheezy). Beide afbeeldingen zijn speciaal ontworpen toorun op Azure en kunnen eenvoudig worden beheerd via Hallo-platform. Credativ ondersteunen ook Hallo op lange termijn onderhoud en bijwerken van Hallo Debian installatiekopieën voor Azure via de Open Source Support Centers.

### <a name="oracle"></a>Oracle
[http://www.Oracle.com/technetwork/Topics/cloud/FAQ-1963009.HTML](http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html)

De Oracle-strategie is toooffer een breed scala aan oplossingen voor openbare en privéclouds. Hallo-strategie biedt klanten keuze en flexibiliteit in hoe ze Oracle-software in Oracle-clouds en andere clouds implementeren. Van Oracle-samen met Microsoft kan klanten toodeploy Oracle-software in Microsoft openbare en persoonlijke clouds met Hallo vertrouwen van de certificeringsinstantie en ondersteuning van Oracle.  Het streven en de investeringen in Oracle openbare en persoonlijke cloud-oplossingen van Oracle blijft ongewijzigd.

### <a name="red-hat"></a>Red Hat
[http://www.RedHat.com/en/partners/Strategic-Alliance/Microsoft](http://www.redhat.com/en/partners/strategic-alliance/microsoft)

Hallo wereld toonaangevende leverancier van oplossingen voor open-source, Red Hat helpt meer dan 90% van Fortune 500 bedrijven zakelijke problemen oplossen, align hun IT en business-strategieën en bereid voor toekomstige Hallo van technologie. Red Hat doet dit door het bieden van beveiligde oplossingen via een open bedrijfsmodel en een betaalbare, voorspelbare abonnementsmodel.

### <a name="suse"></a>SUSE
[http://www.SUSE.com/SUSE-Linux-Enterprise-Server-on-Azure](http://www.suse.com/suse-linux-enterprise-server-on-azure)

SUSE Linux Enterprise Server in Azure is een beproefde platform waarmee hogere betrouwbaarheid en -beveiliging voor cloudcomputing. SUSE van veelzijdige Linux-platform probleemloos worden geïntegreerd met Azure cloud services toodeliver een eenvoudig beheerbare cloudomgeving. Met meer dan 9,200 gecertificeerde toepassingen van meer dan 1800 onafhankelijke softwareleveranciers voor SUSE Linux Enterprise Server en SUSE zorgt ervoor dat werkbelastingen ondersteunde in Hallo Datacenter probleemloos kunnen worden geïmplementeerd in Azure.

### <a name="canonical"></a>Canonical
[http://www.Ubuntu.com/cloud/Azure](http://www.ubuntu.com/cloud/azure)

Canonieke engineering en open community governance station Ubuntu van succes in client-, server- en cloud computing, waaronder persoonlijke cloudservices voor consumenten. Canonieke de visie van een uniforme, gratis platform in Ubuntu, van telefoon toocloud, biedt een serie van samenhangende interfaces voor het Hallo-telefoon, tablet, tv- en bureaublad. Deze visie kunt Ubuntu Hallo eerste keuze voor diverse instellingen uit een openbare cloud providers toohello besluitvormers van consumer electronics en een favoriet tussen afzonderlijke technologen.

Met ontwikkelaars en engineering centers Hallo wereld is Canonical uniek geplaatste toopartner met hardware besluitvormers, inhoudsproviders en software ontwikkelaars toobring Ubuntu oplossingen toomarket voor pc's, servers en mobiele apparaten.
