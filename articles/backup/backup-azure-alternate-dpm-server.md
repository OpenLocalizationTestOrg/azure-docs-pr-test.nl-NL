---
title: aaaRecover gegevens van een Azure Backup-Server | Microsoft Docs
description: U hebt beveiligd Hallo-gegevens herstellen tooa Recovery Services-kluis uit alle geregistreerde toothat kluis van Azure Backup-Server.
services: backup
documentationcenter: 
author: nkolli1
manager: shreeshd
editor: 
ms.assetid: a55f8c6b-3627-42e1-9d25-ed3e4ab17b1f
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: adigan;giridham;trinadhk;markgal
ms.openlocfilehash: 74847880e646c3c4f198afe318f1db30363d137a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="recover-data-from-azure-backup-server"></a>Gegevens herstellen vanaf Azure Backup Server
U kunt Azure Backup-Server toorecover Hallo-gegevens die u hebt een back-up tooa die Recovery Services-kluis. Hallo-proces voor dit zo is geïntegreerd in de beheerconsole van hello Azure Backup-Server en is vergelijkbaar toohello herstelwerkstroom voor andere Azure Backup-onderdelen.

> [!NOTE]
> In dit artikel is van toepassing op [System Center Data Protection Manager 2012 R2 met UR7 of hoger] (https://support.microsoft.com/en-us/kb/3065246), gecombineerd met Hallo [meest recente Azure backup-agent](http://aka.ms/azurebackup_agent).
>
>

toorecover gegevens uit een Azure Backup-Server:

1. Van Hallo **herstel** tabblad Hallo beheerconsole voor Azure Backup-Server, klikt u op **externe DPM toevoegen** (op Hallo linksboven welkomstscherm).   
    ![Externe DPM toevoegen](./media/backup-azure-alternate-dpm-server/add-external-dpm.png)
2. Download nieuwe **vault referenties** uit Hallo kluis die is gekoppeld aan Hallo **Azure Backup-Server** waar Hallo gegevens worden hersteld, kiest u hello Azure Backup-Server in Hallo lijst met Servers die Azure back-up geregistreerd bij Hallo Recovery Services-kluis en bieden Hallo **wachtwoordzin voor versleuteling** die zijn gekoppeld aan het Hallo-server waarvan gegevens worden hersteld.

    ![Externe DPM-referenties](./media/backup-azure-alternate-dpm-server/external-dpm-credentials.png)

   > [!NOTE]
   > Alleen Azure back-up-Servers die zijn gekoppeld aan Hallo dezelfde registratie kluis elkaars gegevens kunt herstellen.
   >
   >

    Zodra Hallo externe Azure Backup-Server met succes is toegevoegd, kunt u gegevens van de externe server Hallo Hallo bladeren en lokale Azure back-upserver van Hallo Hallo **herstel** tabblad.
3. Bladeren Hallo lijst met beschikbare productieservers beveiligd door Hallo externe Azure Backup-Server en selecteer de geschikte gegevensbron Hallo.

    ![Bladeren door externe DPM-Server](./media/backup-azure-alternate-dpm-server/browse-external-dpm.png)
4. Selecteer **Hallo maand en jaar** van Hallo **herstelpunten** vervolgkeuzelijst, selecteer Hallo vereist **herstel datum** voor wanneer Hallo herstelpunt gemaakt en selecteer Hallo is **Hersteltijd**.

    Er verschijnt een lijst van bestanden en mappen in deelvenster Hallo onderaan die kan worden bekeken en tooany locatie hersteld.

    ![Herstelpunten van externe DPM-Server](./media/backup-azure-alternate-dpm-server/external-dpm-recoverypoint.png)
5. Klik met de rechtermuisknop op Hallo juiste item en klik op **herstellen**.

    ![Externe DPM-herstel](./media/backup-azure-alternate-dpm-server/recover.png)
6. Bekijk Hallo **selectie herstellen**. Controleer of het Hallo-gegevens en tijd van de back-up hello wordt hersteld, evenals Hallo bron waaruit Hallo back-up is gemaakt. Als de selectie van Hallo onjuist is, klikt u op **annuleren** toonavigate back toorecovery tabblad tooselect juiste herstelpunt. Als de selectie van Hallo juist is, klikt u op **volgende**.

    ![Externe DPM recovery samenvatting](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-summary.png)
7. Selecteer **tooan alternatieve locatie herstellen**. **Blader** toohello juiste locatie voor Hallo herstel.

    ![Externe DPM alternatieve herstellocatie](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-alternate-location.png)
8. Hallo optie gerelateerde te**kopie maken**, **overslaan**, of **overschrijven**.

   * **Maak kopie** -maakt een kopie van Hallo-bestand als er een conflicterende namen.
   * **Overslaan** - als er een conflict met de naam is niet binnen de Hallo-bestand dat het oorspronkelijke bestand Hallo verlaat.
   * **Overschrijven** - als er een conflict met de naam van bestaande kopie van de Hallo van Hallo bestand overschreven.

     Kies de gewenste optie hello te**beveiligingsinstellingen voor herstel**. U kunt toepassen Hallo beveiligingsinstellingen van doelcomputer Hallo waar Hallo gegevens worden hersteld of Hallo beveiligingsinstellingen die zijn van toepassing tooproduct gelijktijdig Hallo Hallo herstelpunt is gemaakt.

     Bepalen of een **melding** wordt verzonden zodra Hallo herstel is voltooid.

     ![Externe DPM Recovery meldingen](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-notifications.png)
9. Hallo **samenvatting** scherm toont Hallo-opties tot nu toe is gekozen. Nadat u op **'Herstellen'**, Hallo gegevens zijn herstelde toohello geschikte on-premises locatie.

    ![Externe DPM Recovery opties samenvatting](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-options-summary.png)

   > [!NOTE]
   > de hersteltaak Hallo kan worden bewaakt op Hallo **bewaking** tabblad van hello Azure Backup-Server.
   >
   >

    ![Bewaking van herstel](./media/backup-azure-alternate-dpm-server/monitoring-recovery.png)
10. U kunt klikken op **externe DPM wissen** op Hallo **herstel** tabblad Hallo DPM server tooremove Hallo-weergave van Hallo externe DPM-server.

    ![Externe DPM wissen](./media/backup-azure-alternate-dpm-server/clear-external-dpm.png)

## <a name="troubleshooting-error-messages"></a>Foutberichten
| Nee. | Foutbericht | Stappen voor probleemoplossing |
|:---:|:--- |:--- |
| 1. |Deze server is geen geregistreerde toohello kluis die is opgegeven bij de kluisreferentie Hallo. |**Oorzaak:** deze fout treedt op wanneer Hallo kluisreferentiebestand geselecteerd niet behoort toohello Recovery Services-kluis die is gekoppeld aan Azure Backup-Server op welke Hallo herstel wordt uitgevoerd. <br> **Oplossing:** downloaden Hallo kluisreferentiebestand van Hallo Recovery Services-kluis toowhich hello Azure Backup-Server is geregistreerd. |
| 2. |Hallo herstelbare gegevens zijn niet beschikbaar of de geselecteerde server Hallo is geen DPM-server. |**Oorzaak:** er zijn geen andere Azure-back-up Servers geregistreerde toohello Recovery Services-kluis, of Hallo servers hebt Hallo metagegevens nog niet geüpload of Hallo geselecteerde server is niet een back-upserver van Azure (ook wel Windows-Server of Windows-Client). <br> **Oplossing:** als er andere Azure-back-up Servers geregistreerde toohello Recovery Services-kluis, zorg ervoor dat Hallo meest recente Azure backup-agent is geïnstalleerd. <br>Als er andere Azure-back-up Servers geregistreerde toohello Recovery Services-kluis, wacht u totdat een dag na de installatie toostart Hallo herstelproces. Hallo elke nacht een taak wordt Hallo-metagegevens voor alle beveiligde Hallo back-ups toocloud geüpload. Hallo-gegevens zijn beschikbaar voor herstel. |
| 3. |Er zijn geen andere DPM-server is geregistreerd toothis kluis. |**Oorzaak:** er zijn geen andere Azure back-up Servers die zijn geregistreerd toohello kluis uit welke Hallo herstel wordt wordt uitgevoerd.<br>**Oplossing:** als er andere Azure-back-up Servers geregistreerde toohello Recovery Services-kluis, zorg ervoor dat Hallo meest recente Azure backup-agent is geïnstalleerd.<br>Als er andere Azure-back-up Servers geregistreerde toohello Recovery Services-kluis, wacht u totdat een dag na de installatie toostart Hallo herstelproces. Hallo nachtelijke taak bestandsuploads Hallo-metagegevens voor alle beveiligde back-ups toocloud. Hallo-gegevens zijn beschikbaar voor herstel. |
| 4. |Hallo opgegeven wachtwoordzin voor versleuteling komt niet overeen met de wachtwoordzin die bij Hallo volgende server hoort:**<server name>** |**Oorzaak:** Hallo wachtwoordzin voor versleuteling gebruikt in het Hallo-proces voor het versleutelen van gegevens uit hello Azure back-up van Server-gegevens die wordt hersteld Hallo komt niet overeen met de Hallo opgegeven wachtwoordzin voor versleuteling. Hallo-agent is toodecrypt Hallo gegevens. Daarom mislukt Hallo herstel.<br>**Oplossing:** Geef Hallo exact dezelfde wachtwoordzin voor versleuteling gekoppeld hello Azure Backup-Server waarvan gegevens worden hersteld. |

## <a name="frequently-asked-questions"></a>Veelgestelde vragen

### <a name="why-cant-i-add-an-external-dpm-server-after-installing-ur7-and-latest-azure-backup-agent"></a>Waarom niet kan ik een externe DPM-server toevoegen na de installatie van UR7 en de meest recente Azure backup-agent?

Voor de hello DPM-servers met gegevensbronnen die zijn beveiligd toohello cloud (met behulp van een updatepakket ouder zijn dan updatepakket 7 bijwerken), moet u ten minste één dag na de installatie van Hallo UR7 en de meest recente Azure backup-agent, toostart wachten **toevoegen externe DPM-server** . Hallo één dag is periode benodigde tooupload Hallo metagegevens van Hallo DPM beveiliging groepen tooAzure. Beveiliging groep metagegevens is geüpload Hallo eerst via elke nacht een taak.

### <a name="what-is-hello-minimum-version-of-hello-microsoft-azure-recovery-services-agent-needed"></a>Wat is Hallo minimale versie van Microsoft Azure Recovery Services-agent Hallo nodig?

Hallo minimaal vereiste versie van Microsoft Azure Recovery Services-agent Hallo of Azure backup-agent, vereist tooenable deze functie is 2.0.8719.0.  tooview hello agent-versie: open het Configuratiescherm  **>**  alle Configuratiescherm-items  **>**  programma's en onderdelen  **>**  Microsoft Azure Recovery Services-Agent. Als het Hallo-versie is minder dan 2.0.8719.0, downloaden en installeren van Hallo [meest recente Azure backup-agent](https://go.microsoft.com/fwLink/?LinkID=288905).

![Externe DPM wissen](./media/backup-azure-alternate-dpm-server/external-dpm-azurebackupagentversion.png)

## <a name="next-steps"></a>Volgende stappen:
• [Veelgestelde vragen over azure Backup](backup-azure-backup-faq.md)
