---
title: aaaSet beveiligingsbeleid in Azure Security Center | Microsoft Docs
description: Dit document helpt u tooconfigure beveiligingsbeleid in Azure Security Center.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 3b9e1c15-3cdb-4820-b678-157e455ceeba
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: yurid
ms.openlocfilehash: 59226dd84a1c66a2d8367417060ab10a1ff73848
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-security-policies-in-azure-security-center"></a>Beveiligingsbeleid instellen in Azure Security Center
Dit document helpt u tooconfigure beveiligingsbeleid in Security Center door leidt u door Hallo nodige tooperform deze taak.

>[!NOTE] 
>Begin juni 2017 vanaf kan Security Center toocollect en store-gegevens van Microsoft Monitoring Agent Hallo gebruikt. Zie [Azure Security Center-Platform migratie](security-center-platform-migration.md) toolearn meer. Hallo-informatie in dit artikel beschrijft Security Center functionaliteit na de overgang toohello Microsoft Monitoring Agent.
>

## <a name="what-are-security-policies"></a>Wat is beveiligingsbeleid?
Een beveiligingsbeleid bepaalt Hallo set besturingselementen wordt aanbevolen voor resources binnen Hallo opgegeven abonnement. In Security Center definieert u beleid voor uw Azure-abonnementen volgens tooyour bedrijf beveiligingsvereisten en Hallo type toepassingen of de vertrouwelijkheid van gegevens in elk abonnement Hallo.

Zo kunnen er voor resources die worden gebruikt voor ontwikkeling of tests, andere beveiligingsvereisten zijn dan voor resources die worden gebruikt voor productietoepassingen. Ook kan voor toepassingen met gereglementeerde gegevens, zoals persoonsgegevens, een hoger beveiligingsniveau vereist zijn. Beleidsregels voor veiligheid zijn ingeschakeld in Azure Security Center station beveiligingsaanbevelingen en bewaking toohelp u mogelijke beveiligingsproblemen identificeren en bedreigingen te verhelpen. Lees [en Bedieningsgids voor het plannen van Azure Security Center](security-center-planning-and-operations-guide.md) voor meer informatie over hoe toodetermine Hallo optie die geschikt is voor u is.

## <a name="set-security-policies"></a>Beveiligingsbeleid instellen
U kunt voor elk abonnement beveiligingsbeleid configureren. toomodify een beveiligingsbeleid, moet u een eigenaar of bijdrager van het abonnement. Meld u aan toohello Azure-portal en volg Hallo slaagt stappen tooconfigure beveiligingsbeleid in Security Center:

1. Klik op Hallo **beleid** -tegel in Hallo Security Center-dashboard.
2. Selecteer in de blade beveiligingsbeleid Hallo die wordt geopend, Hallo abonnement waarop tooenable Hallo beveiligingsbeleid.

    ![Beleid definiëren](./media/security-center-policies/security-center-policies-fig1-ga.png)
3. Hallo **beveiligingsbeleid** blade voor Hallo geselecteerd abonnement wordt geopend met een aantal opties. beschikbare opties in deze blade Hallo zijn:

   * **Preventiebeleid**: Gebruik deze optie tooconfigure beleid per abonnement.  
   * **E-mailmeldingen**: Gebruik deze optie tooconfigure een e-mailbericht dat wordt verzonden op Hallo eerste dagelijkse exemplaar van een waarschuwing en waarschuwingen met hoog dreigingsniveau. E-mailvoorkeuren kunnen alleen worden geconfigureerd voor abonnementsbeleid. Lees [contact op met informatie over de beveiliging in Azure Security Center bieden](security-center-provide-security-contact-details.md) voor meer informatie over het tooconfigure een e-mailbericht.
   * **Prijscategorie**: Gebruik deze optie tooupgrade Hallo laag selectie prijzen. Zie [Security Center prijzen](security-center-pricing.md) toolearn meer informatie over prijzen.
4. Zorg ervoor dat de optie **Gegevens van virtuele machines verzamelen** is ingesteld op **Aan**. Met deze optie kunt automatisch logboekgegevens verzameld voor bestaande en nieuwe resources met behulp van Microsoft Monitoring Agent Hallo – dit Hallo dezelfde agent wordt gebruikt door Hallo Operations Management Suite en Log Analytics-service is. Gegevens die worden verzameld van deze agent wordt opgeslagen in een bestaande logboekanalyse workspace(s) die zijn gekoppeld aan uw Azure-abonnement of een nieuwe workspace(s), waarbij rekening wordt gehouden account Hallo wereld Hallo VM.

5. In Hallo **beveiligingsbeleid** blade, klikt u op **preventiebeleid** toosee Hallo beschikbare opties. Klik op **op** tooenable Hallo aanbevelingen voor beveiliging die relevant voor dit abonnement zijn.

    ![Hallo-beveiligingsbeleid selecteren](./media/security-center-policies/security-center-policies-fig7.png)

Gebruik tabel als een verwijzing toounderstand Hallo elke optie:

| Beleid | Wanneer de status is ingesteld op aan |
| --- | --- |
| Systeemupdates |Hiermee wordt via Windows Update of Windows Server Update Services een dagelijkse lijst opgehaald van beschikbare beveiligingsupdates en essentiële updates. Hallo opgehaalde lijst is afhankelijk van Hallo-service die geconfigureerd voor die virtuele machine en raadt aan dat Hallo ontbrekende updates worden toegepast. Hallo-beleid gebruikt voor Linux-systemen, Hallo distro geleverde pakket management system toodetermine pakketten met beschikbare updates. Ook wordt bij [virtuele Azure Cloud Services-machines](../cloud-services/cloud-services-how-to-configure.md) gecontroleerd of er beveiligingsupdates en essentiële updates zijn. |
| Beveiligingsproblemen van besturingssystemen |Analyseert configuraties dagelijkse toodetermine problemen met besturingssystemen die Hallo virtuele machine kwetsbaar tooattack kunnen maken. configuratie wijzigingen tooaddress Hallo beleid ook aangeraden deze beveiligingsproblemen. Zie Hallo [lijst met aanbevolen basislijnen](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335) voor meer informatie over Hallo specifieke configuraties die worden bewaakt. (Op dit moment wordt Windows Server 2016 niet volledig ondersteund.) |
| Eindpuntbeveiliging |Raadt endpoint protection toobe ingericht voor alle Windows virtuele machines toohelp identificeren en virussen, spyware en andere schadelijke software verwijderen. |
| Schijfversleuteling |Raadt schijfversleuteling in alle virtuele machines tooenhance gegevensbescherming in rust inschakelen. |
| Netwerkbeveiligingsgroepen |Hiermee wordt de configuratie [netwerkbeveiligingsgroepen](../virtual-network/virtual-networks-nsg.md) worden geconfigureerde toocontrol binnenkomend en uitgaand verkeer tooVMs die openbare eindpunten hebben. Netwerkbeveiligingsgroepen die zijn geconfigureerd voor een subnet, worden overgenomen door alle netwerkinterfaces van virtuele machines, tenzij anders wordt aangegeven. Bovendien toochecking dat er een netwerkbeveiligingsgroep is geconfigureerd, dit beleid beoordeelt de binnenkomende regels tooidentify beveiligingsregels die binnenkomend verkeer toestaan. |
| Web Application Firewall |Beveelt aan dat een web application firewall op virtuele machines worden ingericht als een van de volgende Hallo is ingesteld op true: </br></br>[Openbare IP-adres voor instantieniveau](../virtual-network/virtual-networks-instance-level-public-ip.md) (ILPIP) wordt gebruikt en hello inkomende beveiligingsregels voor de gekoppelde netwerkbeveiligingsgroep Hallo zijn geconfigureerde tooallow toegang tooport 80/443.</br></br>Netwerktaakverdeling IP-adres wordt gebruikt en Hallo gekoppeld taakverdeling en inkomende netwerk address translation (NAT) regels zijn geconfigureerde tooallow toegang tooport 80/443. (Zie [Azure Resource Manager-ondersteuning voor load balancer](../load-balancer/load-balancer-arm.md) voor meer informatie.) |
| Next Generation Firewall |Hiermee wordt meer netwerkbeveiliging toegevoegd dan met de netwerkbeveiligingsgroepen die in Azure zijn ingebouwd. Security Center worden gedetecteerd door implementaties waarvoor next generation firewall wordt aanbevolen en tooprovision een virtueel apparaat inschakelen. |
| Controleren voor SQL en bedreigingen detecteren |Aanbevolen dat de controle van toegang tooAzure Database worden ingeschakeld voor naleving en ook geavanceerde detectie van dreigingen voor onderzoek. |
| SQL-versleuteling |Hiermee wordt aanbevolen dat versleuteling-at-rest wordt ingeschakeld voor uw Azure SQL-databases, gekoppelde back-ups en transactielogboekbestanden. Zelfs bij een inbreuk kunnen uw gegevens niet worden gelezen. |
| Beoordeling van beveiligingslekken |Hiermee wordt aanbevolen dat een oplossing voor de beoordeling van beveiligingslekken wordt geïnstalleerd op de VM. |
| Storage-versleuteling |Deze functie is momenteel beschikbaar voor Azure-blobs en -bestanden. Nadat Storage-serviceversleuteling is ingeschakeld, worden alleen nieuwe gegevens versleuteld. Alle bestaande bestanden in dit opslagaccount zijn nog steeds niet-versleuteld. |
| JIT-netwerktoegang |Wanneer in de tijd is ingeschakeld, wordt in Security Center binnenkomend verkeer tooyour Azure Virtual machines vergrendelt door het maken van een NSG-regel. U selecteert Hallo poorten op Hallo VM toowhich binnenkomend verkeer moet worden vergrendeld. Zie [Manage virtual machine access using just in time](https://docs.microsoft.com/azure/security-center/security-center-just-in-time) (VM-toegang beheren met behulp van JIT) voor meer informatie. |

Nadat u alle opties hebt geconfigureerd, klikt u op **OK** in Hallo **beveiligingsbeleid** -blade waarmee de Hallo aanbevelingen heeft en klik vervolgens op **opslaan** in Hallo **beveiliging Beleid** -blade waarmee de initiële Hallo-instellingen.

> [!NOTE]
> Hallo prijscategorie is nog steeds van toepassing hello niveau van de resourcegroep. Voor meer informatie naar Hallo [prijzen](https://azure.microsoft.com/pricing/details/security-center/) pagina.
>
>

## <a name="see-also"></a>Zie ook
In dit document, u leert hoe tooconfigure beveiligingsbeleid in Azure Security Center. toolearn meer informatie over Azure Security Center Hallo ziet:

* [Plannings- en bedieningsgids voor Azure Security Center](security-center-planning-and-operations-guide.md). Meer informatie over hoe tooplan en Hallo ontwerpoverwegingen tooadopt Azure Security Center begrijpen.
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md). Meer informatie over hoe toomonitor Hallo status van uw Azure-resources.
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md). Meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.
* [Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md). Meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md). Veelgestelde vragen over het gebruik van Hallo service vinden.
* [Azure-beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/). Raadpleeg de blogberichten over beveiliging en naleving in Azure.
