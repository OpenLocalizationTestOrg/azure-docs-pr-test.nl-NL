---
title: aaaDisaster herstelscenario's voor Azure Virtual machines | Microsoft Docs
description: Meer informatie over welke toodo in Hallo gebeurtenis een onderbreking van de Azure-service heeft impact op virtuele machines in Azure.
services: virtual-machines
documentationcenter: 
author: kmouss
manager: timlt
editor: 
ms.assetid: 65272148-ff06-4bce-91f1-851d706d4d40
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: kmouss;aglick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 839c6f9c51a7f35b48ef3636bc346eef332bb06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-in-hello-event-that-an-azure-service-disruption-impacts-azure-vms"></a>Welke toodo in Hallo gebeurtenis een onderbreking van de Azure-service heeft impact op Azure Virtual machines
Bij Microsoft werken we harde toomake zorgen dat onze services altijd beschikbaar tooyou wanneer u deze nodig. Dwingt buiten ons wil soms invloed hebben op ons op een manier die niet-geplande serviceonderbrekingen veroorzaken.

Microsoft biedt een Service Level Agreement (SLA) voor de services als een toezegging voor bedrijfstijd en connectiviteit. Hallo SLA voor afzonderlijke Azure-services kan worden gevonden op [Azure Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).

Azure heeft al veel ingebouwde platformfuncties die ondersteuning bieden voor maximaal beschikbare toepassingen. Lees voor meer informatie over deze services, [herstel na noodgevallen en hoge beschikbaarheid voor Azure-toepassingen](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

In dit artikel bevat informatie over waar noodherstelscenario wanneer een hele regio optreedt in een storing vervaldatum toomajor natuurramp of wijdverbreid service wordt onderbroken. Dit zeldzame instanties zijn, maar u moet voorbereiden voor Hallo kans dat er een storing van een hele regio is. Als een hele regio optreedt in een service wordt onderbroken, Hallo lokaal redundante exemplaren van uw gegevens tijdelijk niet beschikbaar. Als u geo-replicatie hebt ingeschakeld, worden de drie extra kopieën van uw Azure Storage-blobs en tabellen opgeslagen in een andere regio. In geval van een volledige regionale uitval of een noodsituatie in welke Hallo primaire regio kan niet worden hersteld hello remaps Azure alle Hallo DNS-vermeldingen toohello geogerepliceerde regio.

toohelp verwerken van deze exemplaren zeldzame, bieden we Hallo volgen richtlijnen voor Azure virtuele machines in Hallo geval van een onderbreking van de service van Hallo hele regio waar uw virtuele machine van Azure-toepassing wordt geïmplementeerd.

## <a name="option-1-initiate-a-failover-by-using-azure-site-recovery"></a>Optie 1: Start een failover met behulp van Azure Site Recovery
U kunt Azure Site Recovery voor uw virtuele machines configureren zodat u uw toepassing met één klik in kwestie van minuten kan herstellen. U kunt repliceren tooAzure regio van uw keuze en niet-beperkte toopaired regio's. U kunt aan de slag door [uw virtuele machines repliceren](https://aka.ms/a2a-getting-started). U kunt [een herstelplan maken](../site-recovery/site-recovery-create-recovery-plans.md) zodat u Hallo volledige failover-proces voor uw toepassing automatiseren kunt. U kunt [uw testfailovers](../site-recovery/site-recovery-test-failover-to-azure.md) vooraf zonder enige impact op de productie-toepassing of Hallo lopende replicatie. In geval van een onderbreking van de primaire regio Hallo die u zojuist hebt [initieer een failover](../site-recovery/site-recovery-failover.md) en uw toepassing te brengen in de doelregio.


## <a name="option-2-wait-for-recovery"></a>Optie 2: Wachten op herstel
In dit geval is geen actie ondernemen vereist. Weten dat we naar eer en geweten toorestore beschikbaarheid van de service werken. U kunt de huidige servicestatus Hallo zien op onze [Azure Service Health Dashboard](https://azure.microsoft.com/status/).

Dit is de beste optie Hallo als u geen Azure Site Recovery, geografisch redundante opslag met leestoegang of onderbreking van de voorafgaande toohello geografisch redundante opslag hebt ingesteld. Als u hebt ingesteld geografisch redundante opslag of geografisch redundante opslag met leestoegang voor het opslagaccount Hallo waar uw virtuele machine virtuele harde schijven (VHD's) zijn opgeslagen, kunt u zoeken toorecover Hallo basisinstallatiekopie VHD en probeert tooprovision een nieuwe virtuele machine uit. Dit is geen voorkeur optie omdat er geen garanties van synchronisatie van gegevens. Deze optie is als gevolg daarvan niet gegarandeerd toowork.


> [!NOTE]
> Let erop dat u geen controle over dit proces hebt en alleen voor de regio hele serviceonderbrekingen kunnen ontstaan geldt. Daarom moet u ook zijn afhankelijk van andere back-strategieën toepassingsspecifieke tooachieve Hallo hoogste niveau van beschikbaarheid. Zie voor meer informatie Hallo-sectie op [gegevens strategieën voor herstel na noodgevallen](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications#data-strategies-for-disaster-recovery).
>
>

## <a name="next-steps"></a>Volgende stappen

- Start [beveiligen van uw toepassingen die worden uitgevoerd op virtuele machines in Azure](https://aka.ms/a2a-getting-started) met Azure Site Recovery

- meer informatie over hoe tooimplement een herstel na noodgevallen en de strategie van hoge beschikbaarheid, Zie toolearn [herstel na noodgevallen en hoge beschikbaarheid voor Azure-toepassingen](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

- Zie voor een gedetailleerde technische kennis van de mogelijkheden van een cloudplatform, toodevelop [technische richtlijnen voor Azure tolerantie](../resiliency/resiliency-technical-guidance.md).


- Als het Hallo-instructies zijn niet wissen of als u wilt Microsoft toodo Hallo bewerkingen namens u, neem dan contact op met [Customer Support](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
