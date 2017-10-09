---
title: aaaSecurity functies toohelp beveiligen hybride back-ups die gebruikmaken van Azure Backup | Microsoft Docs
description: Meer informatie over hoe toouse beveiligingsfuncties in Azure Backup toomake back-ups veiliger
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 47bc8423-0a08-4191-826d-3f52de0b4cb8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: pajosh
ms.openlocfilehash: 17a0f5e877f84af53c15062ec4a8df480383125e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="security-features-toohelp-protect-hybrid-backups-that-use-azure-backup"></a>Beveiliging functies toohelp hybride back-ups die gebruikmaken van Azure back-up beveiligen
Opmerkingen over beveiligingsproblemen, zoals malware, ransomware en inbraakdetectie, meer. Deze beveiligingsproblemen kunnen kostbare in termen van gegevens en geld zijn. tooguard tegen dergelijke aanvallen, nu Azure Backup biedt beveiliging functies toohelp beveiligen hybride back-ups. In dit artikel bevat informatie over hoe tooenable en gebruik deze functies, met behulp van een Azure Recovery Services-agent en de Azure Backup-Server. Deze functies:

- **Preventie**. Een extra verificatielaag wordt toegevoegd wanneer een kritieke bewerking zoals het wijzigen van een wachtwoordzin wordt uitgevoerd. Deze validatie is tooensure die dergelijke bewerkingen kunnen worden alleen uitgevoerd door gebruikers met een geldige Azure-referenties.
- **Waarschuwingen**. Een e-mailmelding wordt verzonden toohello abonnementsbeheerder wanneer een kritieke bewerking zoals het verwijderen van de back-upgegevens wordt uitgevoerd. Dit e-mailadres zorgt ervoor dat die gebruiker Hallo snel wordt geïnformeerd over deze acties.
- **Herstel**. Verwijderde gegevens back-up wordt bewaard voor een extra 14 dagen na de datum van verwijdering Hallo Hallo. Hierdoor Hallo gegevens kunnen worden hersteld binnen een bepaalde periode, zodat er geen gegevensverlies zelfs als een aanval gebeurt. Een groter aantal minimale herstelpunten worden ook tooguard tegen beschadigde gegevens gehandhaafd.

> [!NOTE]
> Beveiligingsfuncties mag niet worden ingeschakeld als u infrastructuur als een dienst (IaaS) VM-back-up. Deze functies nog niet beschikbaar voor IaaS VM back-up, zodat u deze wilt inschakelen geen invloed heeft. Beveiligingsfuncties moeten alleen worden ingeschakeld als u gebruikmaakt van: <br/>
>  * **Azure backup-agent**. Minimale agentversie 2.0.9052. Nadat u deze functies hebt ingeschakeld, moet u een upgrade uitvoeren voor toothis agent versie tooperform kritieke bewerkingen. <br/>
>  * **Azure Backup-Server**. Azure Backup agent minimumversie 2.0.9052 met Azure Backup-Server bijwerken van 1. <br/>
>  * **System Center Data Protection Manager**. Azure Backup agent minimumversie 2.0.9052 met Data Protection Manager 2012 R2 UR12 of Data Protection Manager 2016 UR2. <br/> 


> [!NOTE]
> Deze functies zijn alleen beschikbaar voor Recovery Services-kluis. Alle Hallo Recovery Services-kluizen een nieuw gemaakt zijn deze functies standaard ingeschakeld. Voor bestaande Recovery Services-kluizen inschakelen gebruikers deze functies met behulp van Hallo stappen in de volgende sectie Hallo genoemd. Ze zijn na Hallo functies zijn ingeschakeld, tooall Hallo Recovery Services agentcomputers, Azure Backup-Server-exemplaren en Data Protection Manager-servers geregistreerd bij kluis Hallo. Inschakelen van deze instelling is een eenmalige bewerking en kunt u deze functies niet uitschakelen nadat deze is ingeschakeld.
>

## <a name="enable-security-features"></a>Beveiligingsfuncties inschakelen
Als u een Recovery Services-kluis maakt, kunt u alle Hallo beveiligingsfuncties. Als u met een bestaande kluis werkt, moet u beveiligingsfuncties inschakelen met de volgende stappen:

1. Meld u toohello Azure-portal met behulp van uw Azure-referenties.
2. Selecteer **Bladeren**, en het type **Recovery Services**.

    ![Schermopname van Azure portal optie voor bladeren](./media/backup-azure-security-feature/browse-to-rs-vaults.png) <br/>

    Hallo-lijst met recovery services-kluizen wordt weergegeven. Selecteer een kluis in deze lijst. Hallo geselecteerde kluisdashboard wordt geopend.
3. Uit Hallo lijst met items die wordt weergegeven onder Hallo-kluis onder **instellingen**, klikt u op **eigenschappen**.

    ![Schermopname van Recovery Services-kluis opties](./media/backup-azure-security-feature/vault-list-properties.png)
4. Onder **beveiligingsinstellingen**, klikt u op **Update**.

    ![Schermopname van Recovery Services-kluis eigenschappen](./media/backup-azure-security-feature/security-settings-update.png)

    Hallo update koppeling opent u Hallo **beveiligingsinstellingen** blade die bevat een samenvatting van Hallo functies en kunt u ze inschakelen.
5. Uit de vervolgkeuzelijst Hallo **hebt geconfigureerd Azure multi-factor Authentication?**, selecteert u een waarde tooconfirm als u hebt ingeschakeld [Azure multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication.md). Als deze is ingeschakeld, kunt u tooauthenticate vanaf een ander apparaat (bijvoorbeeld een mobiele telefoon) wordt gevraagd tijdens het aanmelden toohello Azure-portal.

   Wanneer u kritieke bewerkingen in back-up uitvoert, hebt u tooenter een beveiligingsbeleid voor PINCODE, beschikbaar op Hallo Azure-portal. Azure multi-factor Authentication inschakelt, wordt een beveiligingslaag toegevoegd. Alleen gebruikers met een geldige Azure-referenties geautoriseerde en van een tweede apparaat is geverifieerd, toegang tot hello Azure-portal.
6. toosave beveiligingsinstellingen, selecteer **inschakelen** en klik op **opslaan**. U kunt selecteren **inschakelen** pas nadat u een waarde van Hallo selecteren **hebt geconfigureerd Azure multi-factor Authentication?** lijst in de vorige stap Hallo.

    ![Schermopname van beveiligingsinstellingen](./media/backup-azure-security-feature/enable-security-settings-dpm-update.png)

## <a name="recover-deleted-backup-data"></a>Verwijderde back-upgegevens herstellen
Back-up verwijderde back-upgegevens voor een extra 14 dagen behouden en niet wordt verwijderd onmiddellijk als hello **Stop back-up met back-upgegevens verwijderen** bewerking wordt uitgevoerd. toorestore deze gegevens in Hallo 14 dagen, nemen Hallo stappen hebt uitgevoerd, afhankelijk van wat u gebruikt:

Voor **Azure Recovery Services agent** gebruikers:

1. Als het Hallo-computer waarop de back-ups zijn gebeurt er nog steeds beschikbaar is, gebruikt u [herstellen van gegevens toohello dezelfde machine](backup-azure-restore-windows-server.md#use-instant-restore-to-recover-data-to-the-same-machine) in Azure Recovery Services toorecover van alle Hallo oude herstelpunten.
2. Als deze computer niet beschikbaar is, gebruikt u [herstellen tooan alternatieve machine](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine) toouse tooget van de computer een andere Azure Recovery Services deze gegevens.

Voor **Azure Backup-Server** gebruikers:

1. Hallo-server waar de back-ups zijn gebeurt er nog steeds beschikbaar is, opnieuw Hallo verwijderd gegevensbronnen te beveiligen als hello gebruiken **gegevens herstellen** functie toorecover van alle Hallo oude herstelpunten.
2. Als deze server niet beschikbaar is, gebruikt u [gegevens herstellen vanaf een andere back-upserver van Azure](backup-azure-alternate-dpm-server.md) toouse back-upserver van een andere Azure-instantie tooget deze gegevens.

Voor **Data Protection Manager** gebruikers:

1. Hallo-server waar de back-ups zijn gebeurt er nog steeds beschikbaar is, opnieuw Hallo verwijderd gegevensbronnen te beveiligen als hello gebruiken **gegevens herstellen** functie toorecover van alle Hallo oude herstelpunten.
2. Als deze server niet beschikbaar is, gebruikt u [externe DPM toevoegen](backup-azure-alternate-dpm-server.md) toouse tooget van een andere Data Protection Manager-server deze gegevens.

## <a name="prevent-attacks"></a>Aanvallen te voorkomen
Controles zijn toegevoegd toomake ervoor dat alleen geldige gebruikers verschillende bewerkingen kunnen uitvoeren. Het gaat hierbij om een extra verificatielaag toe te voegen en een minimale bewaartermijn voor hersteldoeleinden te bewaren.

### <a name="authentication-tooperform-critical-operations"></a>Verificatie tooperform kritieke bewerkingen
Als onderdeel van het toevoegen van een extra verificatielaag voor kritieke bewerkingen u na vragen aan gebruiker tooenter een beveiligingsbeleid voor PINCODE zijn bij het uitvoeren van **beveiliging stoppen met het verwijderen van gegevens** en **wijziging wachtwoordzin** bewerkingen .

tooreceive deze PINCODE:

1. Meld u aan toohello Azure-portal.
2. Te bladeren**Recovery Services-kluis** > **instellingen** > **eigenschappen**.
3. Onder **BEVEILIGINGSCODE**, klikt u op **genereren**. Hiermee opent u een blade met Hallo PINCODE toobe ingevoerd in de gebruikersinterface van hello Azure Recovery Services agent.
    Deze PINCODE slechts vijf minuten geldig is en deze automatisch wordt gegenereerd na die periode.

### <a name="maintain-a-minimum-retention-range"></a>Een minimale bewaartermijn onderhouden
tooensure zijn altijd een geldig aantal recovery points beschikbaar, Hallo controles zijn toegevoegd:

- Voor het dagelijkse bewaren van een minimum van **zeven** dagen retentieperiode moeten worden gedaan.
- Voor het bewaren van wekelijks, een minimum van **vier** weken retentieperiode moeten worden gedaan.
- Voor het maandelijkse bewaren van een minimum van **drie** retentieperiode van maanden moeten worden gedaan.
- Voor het bewaren van jaarlijkse, een minimum van **één** jaar retentieperiode moet worden gedaan.

## <a name="notifications-for-critical-operations"></a>Meldingen voor kritieke bewerkingen
Wanneer een kritieke bewerking wordt uitgevoerd, is Hallo abonnementsbeheerder normaal gesproken een e-mailbericht met informatie over het Hallo-bewerking verzonden. U kunt extra e-mailontvangers voor deze meldingen configureren met behulp van hello Azure-portal.

Hallo beveiligingsfuncties in dit artikel genoemde bieden verdediging mechanismen tegen gerichte aanvallen. Belangrijker is, als een aanval gebeurt, deze functies kunt u de mogelijkheid toorecover Hallo uw gegevens.

## <a name="troubleshooting-errors"></a>Het oplossen van problemen
| Bewerking | Details van fouten | Oplossing |
| --- | --- | --- |
| Beleid wijzigen |Hallo back-upbeleid kan niet worden gewijzigd. Fout: Hallo huidige bewerking is mislukt vanwege een interne servicefout tooan [0x29834]. Probeer de bewerking hello later opnieuw. Neem contact op met Microsoft ondersteuning als Hallo probleem zich blijft voordoen. |**Oorzaak:**<br/>Deze fout wordt geleverd wanneer beveiligingsinstellingen zijn ingeschakeld, u de bewaartermijn tooreduce hieronder Hallo minimumwaarden die probeert hierboven is opgegeven en u zich op een niet-ondersteunde versie (ondersteunde versies zijn opgegeven in de eerste notitie van dit artikel). <br/>**Aanbevolen actie:**<br/> In dit geval moet u de bewaarperiode hierboven Hallo minimale periode opgegeven bewaarperiode (zeven dagen voor dagelijks, vier weken wekelijks, drie weken voor maandelijks of één jaar voor per jaar) instellen tooproceed met beleid gerelateerde updates. U kunt desgewenst zou gewenste aanpak tooupdate back-upagent, Azure Backup-Server en/of DPM UR tooleverage Hallo de beveiliging van alle updates. |
| Wachtwoordzin wijzigen |Beveiliging opgegeven PINCODE is onjuist. (ID: 100130) Geef het juiste BEVEILIGINGSCODE toocomplete Hallo deze bewerking. |**Oorzaak:**<br/> Deze fout wordt geleverd wanneer u ongeldige of verlopen BEVEILIGINGSCODE invoeren tijdens het uitvoeren van kritieke bewerking (zoals wachtwoordzin wijzigen). <br/>**Aanbevolen actie:**<br/> toocomplete hello bewerking, moet u geldige BEVEILIGINGSCODE invoeren. tooget Hallo PINCODE, meld u bij tooAzure portal en navigeer tooRecovery Services-kluis > Instellingen > Eigenschappen > beveiliging-PINCODE genereren. Gebruik deze PINCODE toochange wachtwoordzin. |
| Wachtwoordzin wijzigen |Bewerking is mislukt. ID: 120002 |**Oorzaak:**<br/>Deze fout wordt geleverd wanneer beveiligingsinstellingen zijn ingeschakeld, u toochange wachtwoordzin en u zich op een niet-ondersteunde versie (geldige versies die zijn opgegeven in de eerste notitie van dit artikel).<br/>**Aanbevolen actie:**<br/> toochange wachtwoordzin, moet u eerst bijwerken back-upagent toominimum versie minimale 2.0.9052, Azure Backup-server toominimum update 1 en/of DPM toominimum UR12 voor DPM 2012 R2 of DPM 2016 UR2 (downloadkoppelingen hieronder), voer een geldige PINCODE voor beveiliging. tooget Hallo PINCODE, meld u bij tooAzure portal en navigeer tooRecovery Services-kluis > Instellingen > Eigenschappen > beveiliging-PINCODE genereren. Gebruik deze PINCODE toochange wachtwoordzin. |

## <a name="next-steps"></a>Volgende stappen
* [Aan de slag met Azure Recovery Services-kluis](backup-azure-vms-first-look-arm.md) tooenable deze functies.
* [Download de nieuwste Azure Recovery Services-agent Hallo](http://aka.ms/azurebackup_agent) toohelp beveiligen van Windows-computers en bescherming van uw back-upgegevens tegen aanvallen.
* [Download de meest recente Azure Backup-Server Hallo](https://aka.ms/latest_azurebackupserver) toohelp werkbelastingen beveiligen en bescherming van uw back-upgegevens tegen aanvallen.
* [UR12 voor System Center 2012 R2 Data Protection Manager downloaden](https://support.microsoft.com/help/3209592/update-rollup-12-for-system-center-2012-r2-data-protection-manager) of [UR2 voor System Center 2016 Data Protection Manager downloaden](https://support.microsoft.com/help/3209593/update-rollup-2-for-system-center-2016-data-protection-manager) toohelp werkbelastingen beveiligen en bescherming van uw back-upgegevens tegen aanvallen.
