---
title: aaaAzure Security Center- en Linux virtuele machines in Azure | Microsoft Docs
description: Meer informatie over de beveiliging van uw Azure Linux virtuele machine met Azure Security Center.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/07/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7aa0de35fb311457e769f152c8575ec43e41c39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a>Beveiliging van de virtuele machine bewaken met behulp van Azure Security Center

Azure Security Center kunt u meer inzicht verkrijgen in uw Azure-resource procedures voor beveiliging. Security Center biedt geïntegreerde beveiligingsbewaking. Bedreigingen die anders onopgemerkt kunnen worden gedetecteerd. In deze zelfstudie hebt u meer informatie over Azure Security Center en hoe:
 
> [!div class="checklist"]
> * Verzamelen van gegevens instellen
> * Een beveiligingsbeleid instellen
> * Weergeven en oplossen van problemen met configuratie-status
> * Bekijk de gedetecteerde bedreigingen  

## <a name="security-center-overview"></a>Security Center-overzicht

Beveiligingscentrum identificeert mogelijke configuratieproblemen van de virtuele machine (VM) en gerichte beveiligingsrisico's. Hierbij kunnen virtuele machines met netwerkbeveiligingsgroepen, niet-versleutelde schijven en beveiligingsaanvallen Remote Desktop Protocol (RDP ontbrekende). Hallo-informatie wordt weergegeven op Hallo Security Center-dashboard in de grafieken gemakkelijk te lezen.

tooaccess Hallo Security Center-dashboard in hello Azure-portal, selecteer Hallo menu **Security Center**. Op Hallo-dashboard kunt u Zie Hallo beveiligingsstatus van uw Azure-omgeving, een telling van de huidige aanbevelingen vinden en Hallo huidige status van de threat waarschuwingen weergeven. U kunt elke toosee op hoog niveau grafiek uitbreiden meer details.

![Security Center-dashboard](./media/tutorial-azure-security/asc-dash.png)

Security Center zich verder uitstrekt dan gegevens detectie tooprovide aanbevelingen voor problemen die worden gedetecteerd. Bijvoorbeeld, als een virtuele machine zonder een gekoppelde netwerkbeveiligingsgroep is geïmplementeerd, Security Center wordt weergegeven een aanbeveling, met herstelstappen die u kunt nemen. Automatisch doorvoeren krijgt u zonder Hallo context van Security Center.  

![Aanbevelingen](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a>Verzamelen van gegevens instellen

Voordat u VM-beveiligingsconfiguraties zichtbaarheid krijgen kunt, moet u tooset van gegevensverzameling Security Center. Dit omvat het inschakelen van gegevensverzameling en het maken van een Azure storage-account toohold verzamelde gegevens. 

1. Klik op Hallo Security Center-dashboard, **beveiligingsbeleid**, en selecteer vervolgens uw abonnement. 
2. Voor **gegevensverzameling**, selecteer **op**.
3. selecteert u een opslagaccount toocreate **een opslagaccount kiezen**. Selecteer **OK**.
4. Op Hallo **beveiligingsbeleid** blade Selecteer **opslaan**. 

Hallo Beveiligingscentrum data collection agent geïnstalleerd op alle virtuele machines en begint met het verzamelen van gegevens. 

## <a name="set-up-a-security-policy"></a>Een beveiligingsbeleid instellen

Beleidsregels voor veiligheid zijn gebruikte toodefine Hallo items waarvoor Security Center worden gegevens verzameld en worden aanbevelingen gedaan. U kunt verschillende beveiligingsvereisten beleid toodifferent sets van Azure-resources kunt toepassen. Hoewel Azure-resources worden standaard geëvalueerd tegen alle beleidsitems, kunt u afzonderlijke beleidsitems voor alle Azure-resources of voor een resourcegroep uitschakelen. Zie voor gedetailleerde informatie over Security Center-beveiligingsbeleid [beveiligingsbeleid instellen in Azure Security Center](../../security-center/security-center-policies.md). 

tooset van een beveiligingsbeleid voor alle Azure-resources:

1. Selecteer op het Hallo-Security Center-dashboard **beveiligingsbeleid**, en selecteer vervolgens uw abonnement.
2. Selecteer **preventiebeleid**.
3. Inschakelen of uitschakelen van de beleidsitems die u wilt dat tooapply tooall Azure-resources.
4. Wanneer u klaar bent uw instellingen te selecteren, selecteert u **OK**.
5. Op Hallo **beveiligingsbeleid** blade Selecteer **opslaan**. 

tooset om een beleid voor een specifieke resourcegroep:

1. Selecteer op het Hallo-Security Center-dashboard **beveiligingsbeleid**, en selecteer vervolgens een resourcegroep.
2. Selecteer **preventiebeleid**.
3. Inschakelen of uitschakelen beleidsitems gewenste tooapply toohello resourcegroep.
4. Onder **overname**, selecteer **unieke**.
5. Wanneer u klaar bent uw instellingen te selecteren, selecteert u **OK**.
6. Op Hallo **beveiligingsbeleid** blade Selecteer **opslaan**.  

Ook kunt u uitschakelen gegevensverzameling voor een specifieke resourcegroep op deze pagina.

In de Hallo voorbeeld te volgen, een uniek beleid is gemaakt voor een resourcegroep met de naam *myResoureGroup*. Schijf versleutelings- en web application firewall aanbevelingen zijn in dit beleid uitgeschakeld.

![Unieke beleidsnaam](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a>Configuratiestatus van weergave VM

Nadat u hebt ingeschakeld op het verzamelen van gegevens en een beveiligingsbeleid instellen, begint Security Center tooprovide waarschuwingen en aanbevelingen. Als u virtuele machines zijn geïmplementeerd, is Hallo-agent voor het verzamelen van gegevens geïnstalleerd. Security Center wordt vervolgens ingevuld met gegevens voor Hallo nieuwe virtuele machines. Zie voor gedetailleerde informatie over de configuratiestatus VM [beveiligen van uw virtuele machines in Security Center](../../security-center/security-center-virtual-machine-recommendations.md). 

Als gegevens worden verzameld, wordt de resourcestatus Hallo voor elke virtuele machine en de gerelateerde Azure-resource geaggregeerd. Hallo-informatie wordt weergegeven in het diagram van een gemakkelijk te lezen. 

de resourcestatus tooview:

1.  Op Hallo Security Center-dashboard, onder **resourcebeveiligingsstatus**, selecteer **Compute**. 
2.  Op Hallo **Compute** blade Selecteer **virtuele machines**. Deze weergave bevat een samenvatting van status Hallo-configuratie voor alle virtuele machines.

![Status berekenen](./media/tutorial-azure-security/compute-health.png)

toosee alle aanbevelingen voor een VM, selecteer Hallo VM. Aanbevelingen en het doorvoeren worden behandeld in meer detail in de volgende sectie Hallo van deze zelfstudie.

## <a name="remediate-configuration-issues"></a>Problemen met de configuratie herstellen

Nadat het Beveiligingscentrum gestart toopopulate met configuratiegegevens, zijn aanbevelingen gemaakt op basis van Hallo beveiligingsbeleid voor die u ingesteld. Als een virtuele machine zonder een gekoppelde netwerkbeveiligingsgroep is ingesteld, wordt een aanbeveling bijvoorbeeld toocreate een gemaakt. 

een lijst met alle aanbevelingen toosee: 

1. Selecteer op het Hallo-Security Center-dashboard **aanbevelingen**.
2. Selecteer een specifieke aanbeveling. Er verschijnt een lijst van alle resources waarvoor Hallo aanbeveling van toepassing is.
3. tooapply een aanbeveling, selecteer een specifieke bron. 
4. Volg de instructies Hallo voor herstelstappen uit. 

In veel gevallen Security Center biedt bruikbare stappen u kunt tooaddress een aanbeveling uitvoeren zonder Security Center. Security Center detecteert in Hallo voorbeeld te volgen, een netwerkbeveiligingsgroep met een onbeperkte inkomende regel. Op Hallo aanbeveling pagina kunt u Hallo **binnenkomende regels bewerken** knop. Hallo gebruikersinterface die benodigde toomodify Hallo regel wordt weergegeven. 

![Aanbevelingen](./media/tutorial-azure-security/remediation.png)

Als de aanbevelingen zijn hersteld, worden ze gemarkeerd als opgelost. 

## <a name="view-detected-threats"></a>Weergave van gedetecteerde bedreigingen

Tooresource configuratieaanbevelingen, Security Center wordt bovendien dagelijks geconstateerde waarschuwingen weergegeven. Hallo waarschuwingen beveiligingsfunctie aggregeert gegevens verzameld van elke virtuele machine, Azure VPN-logboeken en verbonden partner oplossingen toodetect bedreigingen van Azure-resources. Zie voor gedetailleerde informatie over Security Center threat detectiemogelijkheden [Azure Security Center detectiemogelijkheden](../../security-center/security-center-detection-capabilities.md).

Hallo waarschuwingen beveiligingsfunctie vereist Hallo Security Center prijzen laag toobe verhoogd van *vrije* te*standaard*. Een 30-daagse **gratis proefversie** is beschikbaar wanneer u een hogere prijscategorie toothis verplaatst. 

toochange hello prijscategorie:  

1. Klik op Hallo Security Center-dashboard, **beveiligingsbeleid**, en selecteer vervolgens uw abonnement.
2. Selecteer **prijscategorie**.
3. Selecteer de nieuwe laag hello, en selecteer vervolgens **Selecteer**.
4. Op Hallo **beveiligingsbeleid** blade Selecteer **opslaan**. 

Nadat u Hallo prijscategorie hebt gewijzigd, worden in Hallo beveiliging waarschuwingen grafiek toopopulate begint beveiligingsrisico's worden gedetecteerd.

![Beveiligingswaarschuwingen](./media/tutorial-azure-security/security-alerts.png)

Selecteer een waarschuwing tooview. U kunt bijvoorbeeld een beschrijving van Hallo threat, detectietijd hello, alle threat pogingen en Hallo aanbevolen herstel. Hallo voorbeeld te volgen, zijn een RDP-brute-force-aanvallen aangetroffen, met 294 mislukte pogingen voor RDP. Een aanbevolen oplossing is opgegeven.

![RDP-aanval](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie kunt u instellen in Azure Security Center en vervolgens geëvalueerd VM's in Security Center. U hebt geleerd hoe u:

> [!div class="checklist"]
> * Verzamelen van gegevens instellen
> * Een beveiligingsbeleid instellen
> * Weergeven en oplossen van problemen met configuratie-status
> * Bekijk de gedetecteerde bedreigingen

De volgende zelfstudie toolearn toohello voor vooraf informatie over het maken van een CI/CD-pijplijn met Jenkins, GitHub en Docker.

> [!div class="nextstepaction"]
> [CI/CD-infrastructuur met Jenkins, GitHub en Docker maken](tutorial-jenkins-github-docker-cicd.md)

