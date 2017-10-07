---
title: aaaManage kosten effectief voor SQL Server op virtuele machines in Azure | Microsoft Docs
description: Bevat de aanbevolen procedures voor het kiezen van Hallo juiste SQL Server virtuele machine model prijzen.
services: virtual-machines-windows
documentationcenter: na
author: luisherring
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/18/2017
ms.author: jroth
ms.openlocfilehash: 6c6a4394e95b5a915ea3e7d5965730000d331036
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="pricing-guidance-for-sql-server-azure-vms"></a>Prijsinformatie voor Azure VM's van SQL Server

In dit onderwerp biedt prijsstelling richtlijnen voor SQL Server virtuele machines in Azure. Er zijn verschillende opties die invloed hebben op de kosten en het is belangrijk toopick Hallo rechts afbeelding die een compromis tussen de kosten op zakelijke vereisten.

## <a name="free-licensed-sql-server-editions"></a>Vrije-gelicentieerde SQL Server-edities

Als u toodevelop wilt, testen, of een POC bouwen en gebruik Hallo gratis licentie **ontwikkelaarsversie van SQL Server**. Deze editie biedt alles wat in SQL Server Enterprise edition, dus u kunt deze toobuild elke gewenste toepassing. Het toorun gewoon niet toegestaan in de productieomgeving. Een virtuele machine van SQL Server Developer wordt alleen kosten in rekening gebracht voor Hallo kosten van het Hallo VM, niet voor SQL Server-licentieverlening.

Als u wilt dat toorun een lichte werkbelasting in productie (< 4 kernen < 1 GB geheugen, < 10 GB/database), gebruikt u Hallo gratis licentie **SQL Server Express edition**. Een SQL Express-VM wordt alleen kosten in rekening gebracht voor de kosten Hallo Hallo VM, niet SQL-licentieverlening.

Voor deze ontwikkeling en testen of lightweight productieworkloads, kunt u ook geld besparen door het kiezen van een kleinere VM-grootte die overeenkomt met deze werkbelastingen. Hallo DS1v2 mogelijk een goede keuze voor deze werkbelastingen.

een SQL Server 2016 Azure virtuele machine met een van deze installatiekopieën toocreate Zie Hallo koppelingen te volgen:

- [SQL Server 2016 Developer Azure VM](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1DeveloperWindowsServer2016-ARM)
- [SQL Server 2016 Express Azure VM](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1ExpressWindowsServer2016-ARM)

## <a name="paid-sql-server-editions"></a>Betaalde edities van SQL Server

Als u een niet-lightweight productie-werkbelasting hebt, een Hallo volgende edities van SQL Server gebruiken:

| SQL Server-editie | Workload |
|-----|-----|
| Web | Kleine websites |
| Standard | Kleine toomedium werkbelastingen |
| Enterprise | Grote of bedrijfskritieke werkbelastingen|

U hebt twee opties toopay voor SQL Server-licentieverlening voor deze edities: *betaalde per gebruik* of *brengt uw eigen licentie*.

### <a name="pay-per-usage"></a>Betalen per gebruik

**Betalende Hallo SQL Server-licentie per gebruik** betekent dat Hallo per minuut kosten van het uitvoeren van hello Azure VM Hallo kosten van Hallo SQL Server-licentie bevat. U ziet Hallo prijzen voor Hallo verschillende edities van SQL Server (Web, Standard, Enterprise) in Hallo [Azure VM pagina met prijzen](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard). Hallo kosten is hello gelijk voor alle versies van SQL Server (too2016 2008 R2). Zoals met SQL Server-licentieverlening in het algemeen Hallo afhankelijk licentiekosten per minuut Hallo aantal VM-kernen.

Betalende Hallo SQL Server wordt-licentieverlening per gebruik aanbevolen voor:

- Tijdelijke of periodieke werkbelastingen. Bijvoorbeeld: een app die behoeften toosupport een gebeurtenis van een aantal maanden elk jaar of business-analyse op maandag.
- Werklasten met onbekende levensduur of schaal. Bijvoorbeeld, een app die mogelijk niet vereist zijn in een paar maanden of waarvoor meer of minder rekencapaciteit, afhankelijk van de aanvraag.

een SQL Server 2016 Azure virtuele machine met een van deze installatiekopieën betalen per gebruik toocreate Zie Hallo koppelingen te volgen:

- [SQL Server 2016 Web Azure VM](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1WebWindowsServer2016)
- [SQL Server 2016 standaard Azure VM](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1StandardWindowsServer2016)
- [SQL Server 2016 Enterprise Azure VM](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1EnterpriseWindowsServer2016)

> [!IMPORTANT]
> Wanneer u een virtuele machine van SQL Server in hello Azure-portal maakt, Hallo maandelijkse kosten weergegeven op Hallo geschatte **een grootte kiezen** blade niet SQL Server-licentiekosten omvat. Dit zijn de kosten Hallo Hallo alleen VM.
>
> ![Blade voor VM-grootte kiezen](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-choose-size-pricing-estimate.png)
>
>Dit is Hallo totale geschatte kosten voor Hallo gratis licentie Express en ontwikkelaars versies van SQL Server. Maar voor de webserver, Standard en Enterprise, vinden Hallo extra licentiekosten van SQL op Hallo [pagina met prijzen virtuele Windows-Machines](https://azure.microsoft.com/pricing/details/virtual-machines/windows/). Selecteer de doeleditie van SQL Server op Hallo pagina met prijzen.

### <a name="bring-your-own-license-byol"></a>BYOL (Bring your own license)

**U brengt uw eigen SQL Server-licentie via License Mobility**, ook wel aangeduid tooas **BYOL**, betekent het gebruik van een bestaande SQL Server-volumelicentie met Software Assurance in een Azure VM. Een SQL Server-VM die gebruikmaakt van BYOL wordt alleen kosten in rekening gebracht voor Hallo kosten van het uitvoeren van Hallo VM, niet voor SQL Server-licentieverlening, gezien het feit dat u al licenties en Software Assurance hebt aangeschaft via een Volume Licensing-programma.

U brengt uw eigen SQL wordt licenties via License Mobility aanbevolen voor:

- Continue werkbelastingen. Bijvoorbeeld: een app die toosupport bedrijfsactiviteiten 24 x 7 nodig.
- Werklasten met bekende levensduur en schaal. Bijvoorbeeld, een app die vereist zijn voor de hele jaar Hallo en welke vraag is prognose.

toouse BYOL met een virtuele machine van SQL Server, moet u een licentie hebben voor SQL Server Standard of Enterprise en [Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx#tab=1), dit is een vereiste optie door enkele [Volume Licensing](https://www.microsoft.com/en-us/download/details.aspx?id=10585) programma's en een optionele koop met anderen.  Hallo prijzen niveaus opgegeven via volumelicentieprogramma's varieert op basis van overeenkomst en Hallo hoeveelheid en/of streven tooSQL Server Hallo type. Maar als een vuistregel brengen van uw eigen licentie voor continue productieworkloads heeft Hallo volgende voordelen:

| BYOL benefit | Beschrijving |
|-----|-----|
| **Kostenbesparingen** | U brengt uw eigen SQL Server-licentie is rendabeler dan betalen per gebruik, als een werklast continu wordt uitgevoerd, SQL Server Standard of Enterprise voor *meer dan 10 maanden*. |
| **Besparingen op lange termijn** | Gemiddeld is *30% goedkoper per jaar* toobuy of vernieuwen van een SQL Server-licentie voor Hallo eerste drie jaar. Bovendien na drie jaar hoeft u geen toorenew Hallo licentie voordoet, alleen betalen voor Software Assurance. Op dat moment is *200% goedkoper*. |
| **Gratis passieve secundaire replica** | Een ander voordeel van uw eigen licentie meebrengen is Hallo [gratis licentieverlening voor één passieve secundaire replica](https://azure.microsoft.com/pricing/licensing-faq/) per SQL-Server voor maximale beschikbaarheid dient. Deze geknipt in half Hallo licentieverlening kosten van een maximaal beschikbare SQL Server-implementatie (bijvoorbeeld met behulp van AlwaysOn-beschikbaarheidsgroepen). Hallo rechten toorun Hallo passieve secundaire door Hallo failover-Servers Software Assurance-voordeel zijn voorzien. |

een SQL Server 2016 Azure virtuele machine met een van deze installatiekopieën bring-your-eigenaar-licentie toocreate Zie Hallo VMs voorafgegaan door '{BYOL}':

- [SQL Server 2016 Enterprise Azure VM](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1EnterpriseWindowsServer2016)
- [SQL Server 2016 standaard Azure VM](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016)

> [!NOTE]
> Laat ons weten binnen tien dagen hoeveel SQL Server-licenties u in Azure. Hallo koppelingen toohello vorige afbeeldingen hebt instructies over het toodo dit.

## <a name="avoid-unecessary-costs"></a>Vermijd unecessary kosten

Als u van alle werkbelastingen die niet continu uitgevoerd gebruikmaakt, kunt u overwegen Hallo virtuele machine afgesloten tijdens Hallo inactieve perioden. U betaalt alleen voor wat u gebruikt.

Bijvoorbeeld, als u gewoon uit SQL Server op een virtuele machine in Azure probeert, wilt niet tooincur kosten door per ongeluk draait weken. Eén oplossing is toouse hello [automatisch afsluiten functie](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/).

![SQL VM autoshutdown](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-auto-shutdown.png)

Automatisch afsluiten maakt deel uit van een grotere set van soortgelijke functies van [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab).

Voor andere werkstromen, kunt u automatisch afsluiten en opnieuw starten van virtuele Azure-machines met een scripting-oplossing, zoals [Azure Automation](https://azure.microsoft.com/services/automation/).

> [!IMPORTANT]
> Afgesloten en toewijzing van uw virtuele machine is Hallo alleen manier tooavoid de kosten. Gewoon stoppen of met behulp van power opties tooshut omlaag Hallo VM nog steeds leidt ertoe dat gebruikskosten.

## <a name="next-steps"></a>Volgende stappen

Voor algemene Azure prijzen richtlijnen, Zie [te voorkomen dat onverwachte kosten met Azure-facturering en kostenbeheer](../../../billing/billing-getting-started.md).

Hallo nieuwste virtuele Machines prijzen, waaronder SQL Server, Zie voor Hallo [Azure VM pagina met prijzen](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard).

Zie de andere virtuele Machine van SQL Server-onderwerpen op [SQL Server op Azure Virtual Machines Overview](virtual-machines-windows-sql-server-iaas-overview.md).
