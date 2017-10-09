---
title: access-aaaJust in tijd virtuele machine in Azure Security Center | Microsoft Docs
description: Dit document wordt u begeleid bij hoe NET tijdig VM-toegang in Azure Security Center helpt u toegang tot tooyour Azure virtuele machines.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: terrylan
ms.openlocfilehash: e6b58dd2c686cb227392b294e85914df5a546016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machine-access-using-just-in-time"></a>Virtuele machine toegang met behulp van in de tijd beheren

Alleen in tijd virtuele machine (VM) zijn toegang gebruikte toolock omlaag binnenkomend verkeer tooyour Azure Virtual machines blootstelling tooattacks verminderen terwijl er eenvoudig toegang tooconnect tooVMs wanneer deze nodig.

> [!NOTE]
> Hallo alleen in de functie is in preview en beschikbaar is op Hallo standaardcategorie van Security Center.  Zie [prijzen](security-center-pricing.md) toolearn meer informatie over Security Center de prijscategorie.
>
>

## <a name="attack-scenario"></a>Aanval

Brute force-aanvallen vaak doelpoorten management als een manier toogain toegang tooa VM. Als dit lukt, kan een aanvaller besturen Hallo VM en een voet achter de deur tot stand brengen in uw omgeving.

Eenzijdige tooreduce blootstelling tooa beveiligingsaanval is toolimit Hallo hoeveelheid tijd die een poort geopend is. Poorten voor beheertaken doen niet nodig toobe open te allen tijde. Hoeft alleen toobe openen terwijl u bent verbonden toohello VM, bijvoorbeeld tooperform management en-onderhoud. Wanneer u in de tijd is ingeschakeld, wordt gebruikt door Security Center [Netwerkbeveiligingsgroep](../virtual-network/virtual-networks-nsg.md) (NSG), deze regels toomanagement toegangspoorten beperken zodat ze niet worden gericht door aanvallers.

![Alleen bij tijd scenario][1]

## <a name="how-does-just-in-time-access-work"></a>Hoe werkt alleen bij het toegang in uitvoeringstijd combinatie?

Wanneer in de tijd is ingeschakeld, wordt in Security Center binnenkomend verkeer tooyour Azure Virtual machines vergrendelt door het maken van een NSG-regel. U selecteert Hallo poorten op Hallo VM toowhich binnenkomend verkeer wordt worden vergrendeld. Deze poorten worden beheerd door Hallo NET in tijdoplossing.

Wanneer een gebruiker toegang tooa VM aanvraagt, Security Center controleert die gebruiker Hallo [op rollen gebaseerde toegangsbeheer (RBAC)](../active-directory/role-based-access-control-configure.md) machtigingen die schrijftoegang voor hello Azure-resource bieden. Als ze schrijftoegang hebben, Hallo-aanvraag is goedgekeurd en Security Center configureert automatisch Hallo Netwerkbeveiligingsgroepen (nsg's) tooallow poorten voor verkeer toohello inkomende hello en de hoeveelheid tijd die u hebt opgegeven. Nadat het Hallo-tijd is verstreken, herstelt Security Center Hallo nsg's tootheir vorige staat.

> [!NOTE]
> Security Center alleen bij het VM-time-toegang ondersteunt momenteel alleen virtuele machines die zijn geïmplementeerd via Azure Resource Manager. Zie informatie over het Hallo-classic en Resource Manager-implementatiemodel toolearn [Azure Resource Manager versus klassieke implementatie](../azure-resource-manager/resource-manager-deployment-model.md).
>
>

## <a name="using-just-in-time-access"></a>Met behulp van alleen bij het time-toegang

Hallo **Just in time VM toegang** tegel op Hallo **Security Center** blade ziet u Hallo aantal VM's zijn geconfigureerd voor alleen bij tijd toegang en Hallo aantal goedgekeurde toegangsaanvragen in Hallo afgelopen week.

Selecteer Hallo **Just in time VM toegang** tegel en Hallo **Just in time VM toegang** blade wordt geopend.

![Alleen in de tijd VM toegang tegel][2]

Hallo **Just in time VM toegang** blade bevat informatie over het Hallo-status van uw virtuele machines:

- **Geconfigureerd** -virtuele machines die geconfigureerd toosupport alleen bij het VM-time-toegang zijn. Hallo-gegevens die worden gepresenteerd Hallo afgelopen week en voor elke VM Hallo aantal goedgekeurde aanvragen, de datum van laatste toegang en de tijd en de laatste gebruiker bevat.
- **Aanbevolen** -VM's die alleen bij het toegang in uitvoeringstijd VM kunnen ondersteunen, maar niet is geconfigureerd voor. Het is raadzaam dat u alleen bij het VM-toegangsbeheer tijd voor deze virtuele machines inschakelt. Zie [tijd VM toegang inschakelen](#enable-just-in-time-vm-access).
- **Geen aanbeveling** -redenen die leiden een virtuele machine niet toobe aanbevolen tot kunnen zijn:
  - Ontbrekende NSG - Hallo NET in tijdoplossing vereist een NSG toobe aanwezig.
  - Klassieke VM - Security Center alleen bij het VM-time-toegang ondersteunt momenteel alleen virtuele machines die zijn geïmplementeerd via Azure Resource Manager. Een klassieke implementatie wordt niet ondersteund door Hallo NET in tijdoplossing.
  - Andere - een virtuele machine is in deze categorie als Hallo NET tijdig oplossing is uitgeschakeld in het beveiligingsbeleid Hallo van Hallo abonnement of resourcegroep hello, of dat Hallo VM een openbaar IP-adres ontbreekt en niet beschikken over een NSG.

## <a name="configuring-a-just-in-time-access-policy"></a>Configureren van een in het toegangsbeleid tijd

tooselect hello virtuele machines die u wilt dat tooenable:

1. Op Hallo **Just in time VM toegang** blade, selecteer Hallo **aanbevolen** tabblad.

  ![Time-toegang inschakelen][3]

2. Onder **VMs**, Hallo virtuele machines die u tooenable wilt selecteren. Hiermee wordt een vinkje volgende tooa VM geplaatst.
3. Selecteer **JIT op virtuele machines inschakelen**.
4. Selecteer **Opslaan**.

### <a name="default-ports"></a>Standaard-poorten

Hallo-standaardpoorten die Security Center aanbeveelt inschakelen in de tijd, kunt u zien.

1. Op Hallo **Just in time VM toegang** blade, selecteer Hallo **aanbevolen** tabblad.

  ![Standaardpoorten weergeven][6]

2. Onder **VMs**, selecteert u een virtuele machine. Hiermee wordt een vinkje volgende toohello virtuele machine en wordt geopend Hallo geplaatst **JIT VM-configuratie** blade. Deze blade geeft Hallo standaardpoorten.

### <a name="add-ports"></a>Poorten toevoegen

Van Hallo **JIT VM-configuratie** blade kunt u ook toevoegen en configureren van een nieuwe poort waarop tooenable Hallo NET in tijdoplossing.

1. Op Hallo **JIT VM-configuratie** blade Selecteer **toevoegen**. Hiermee opent u Hallo **toevoegen poortconfiguratie** blade.

  ![Poortconfiguratie][7]

2. Op **toevoegen poortconfiguratie** blade u identificeren Hallo-poort, protocoltype, bron-IP-adressen en de maximale duur van aanvraag toegestaan.

  Bron-IP-adressen toegestaan zijn Hallo IP-adresbereiken toegestane tooget toegang op een verzoek goedgekeurd.

  Maximale aanvraagtijd is Hallo maximale tijdsduur dat een specifieke poort kan worden geopend.

3. Selecteer **OK**.

## <a name="requesting-access-tooa-vm"></a>Aanvragen van toegang tooa VM

toorequest toegang tooa VM:

1. Op Hallo **Just in time VM toegang** blade, selecteer Hallo **geconfigureerde** tabblad.
2. Onder **VMs**, Hallo virtuele machines die u toegang tooenable wilt selecteren. Hiermee wordt een vinkje volgende tooa VM geplaatst.
3. Selecteer **toegang aanvragen**. Hiermee opent u Hallo **toegang aanvragen** blade.

  ![Aanvraag toegang tooa VM][4]

4. Op Hallo **toegang aanvragen** blade u configureert voor elke VM Hallo poorten tooopen samen met de Hallo bron-IP dat Hallo poort geopend tooand Hallo-tijdvenster voor welke Hallo poort is geopend. U kunt alleen toohello toegangspoorten die zijn geconfigureerd in Hallo NET in tijd beleid aanvragen. Elke poort heeft een maximale toegestane tijd die is afgeleid van Hallo NET in tijd beleid.
5. Selecteer **poorten openen**.

## <a name="editing-a-just-in-time-access-policy"></a>Een bewerking in het toegangsbeleid tijd

U kunt wijzigen van een virtuele machine bestaande net in tijd beleid door toe te voegen en een nieuwe poort tooopen configureren voor die VM of door het wijzigen van de andere parameters gerelateerde tooan al poort beveiligd.

In volgorde tooedit een bestaande alleen bij het beleid van de tijd van een VM hello **geconfigureerde** tabblad wordt gebruikt:

1. Onder **VMs**, selecteer een tooadd VM een poort tooby voor die VM op Hallo drie punten binnen Hallo rij te klikken. Hiermee opent u een menu.
2. Selecteer **bewerken** in Hallo-menu. Hiermee opent u Hallo **JIT VM-configuratie** blade.

  ![Beleid bewerken][8]

3. Op Hallo **JIT VM-configuratie** blade, u kunt de bestaande instellingen Hallo van een poort al beveiligde voor installatie zonder toezicht bewerken door te klikken op de poort of u kunt selecteren **toevoegen**. Hiermee opent u Hallo **toevoegen poortconfiguratie** blade.

  ![Een poort toevoegen][7]

4. Op **toevoegen poortconfiguratie** blade Hallo-poort, protocoltype toegestane bron-IP-adressen en maximale aanvraagtijd identificeren.
5. Selecteer **OK**.
6. Selecteer **Opslaan**.

## <a name="auditing-just-in-time-access-activity"></a>Controleren in activiteit voor het openen

U kunt Verkrijg inzicht in de VM-activiteiten logboek zoekactie. tooview Logboeken:

1. Op Hallo **Just in time VM toegang** blade, selecteer Hallo **geconfigureerde** tabblad.
2. Onder **VMs**, selecteert u een VM tooview informatie over door te klikken op Hallo drie punten binnen Hallo rij voor die VM. Hiermee opent u een menu.
3. Selecteer **activiteitenlogboek** in Hallo-menu. Hiermee opent u Hallo **activiteitenlogboek** blade.

![Activiteitenlogboek selecteren][9]

Hallo **activiteitenlogboek** blade biedt een gefilterde weergave van de vorige bewerkingen voor die VM samen met de tijd, datum en -abonnement.

![Logboek van de activiteit weergeven][5]

U kunt Hallo logboekgegevens downloaden door te selecteren **Klik hier toodownload alle Hallo items als CSV**.

Hallo filters wijzigen en selecteer **toepassen** toocreate Zoek- en logboekbestanden.

## <a name="using-just-in-time-vm-access-via-powershell"></a>Met behulp van alleen in de tijd VM toegang via PowerShell

In de volgorde toouse Hallo NET in tijdoplossing via PowerShell, Controleer of er Hallo [nieuwste](/powershell/azure/install-azurerm-ps) Azure PowerShell-versie.
Nadat u dit doet, moet u tooinstall hello [nieuwste](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Azure Security Center van Hallo PowerShell gallery.

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a>Configureren van een in tijd beleid voor een virtuele machine

een tooconfigure in tijd beleid op een specifieke virtuele machine, moet u toorun met deze opdracht in uw PowerShell-sessie: Set-ASCJITAccessPolicy.
Ga als volgt Hallo cmdlet toolearn meer documentatie.

### <a name="requesting-access-tooa-vm"></a>Aanvragen van toegang tooa VM

een specifieke virtuele machine die wordt beveiligd met tooaccess Hallo NET in tijdoplossing, moet u toorun met deze opdracht in uw PowerShell-sessie: aanroepen ASCJITAccess.
Ga als volgt Hallo cmdlet toolearn meer documentatie.

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd hoe alleen bij het VM-toegang in Security Center helpt tijd beheren van toegang tooyour Azure virtuele machines.

toolearn meer informatie over Security Center Hallo ziet:

- [Beveiligingsbeleid instellen](security-center-policies.md) : meer informatie hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.
- [Aanbevelingen voor beveiliging beheren](security-center-recommendations.md) : Leer hoe aanbevelingen u uw Azure-resources te beveiligen.
- [Beveiligingsstatus bewaken](security-center-monitoring.md) : meer informatie over hoe toomonitor Hallo status van uw Azure-resources.
- [Beheren en erop reageren toosecurity waarschuwingen](security-center-managing-and-responding-alerts.md) : meer informatie hoe toomanage en gereageerd had toosecurity waarschuwingen.
- [Partneroplossingen bewaken](security-center-partner-solutions.md) : meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.
- [Security Center FAQ](security-center-faq.md) : Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
- [Azure-beveiligingsblog](https://blogs.msdn.microsoft.com/azuresecurity/): lees blogberichten over de beveiliging en naleving van Azure.


<!--Image references-->
[1]: ./media/security-center-just-in-time/just-in-time-scenario.png
[2]: ./media/security-center-just-in-time/just-in-time.png
[3]: ./media/security-center-just-in-time/enable-just-in-time-access.png
[4]: ./media/security-center-just-in-time/request-access-to-a-vm.png
[5]: ./media/security-center-just-in-time/activity-log.png
[6]: ./media/security-center-just-in-time/default-ports.png
[7]: ./media/security-center-just-in-time/add-a-port.png
[8]: ./media/security-center-just-in-time/edit-policy.png
[9]: ./media/security-center-just-in-time/select-activity-log.png
