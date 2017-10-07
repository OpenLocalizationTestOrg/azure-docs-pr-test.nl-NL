---
title: aaaCreate maken en terugzetten een back-up in BizTalk Services | Microsoft Docs
description: BizTalk Services omvat back-up en herstel. Meer informatie over hoe toocreate en herstellen van een back-up en bepalen wat opgehaald back-up gemaakt. MABS, WABS
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 59f91173-4683-48df-abd5-41262bfce6df
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 32356ad870678fa5fd5bbbbf13d9377188f770a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-backup-and-restore"></a>BizTalk Services: back-ups maken en herstellen

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Azure BizTalk Services bevat de mogelijkheden van back-up en herstel. Dit onderwerp wordt beschreven hoe toobackup en terugzetten van BizTalk Services met behulp van de klassieke Azure-portal Hallo.

U kunt ook back-up BizTalk Services met behulp van Hallo [REST-API van BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=325584). 

> [!NOTE]
> Hybride verbindingen zijn geen back-up, ongeacht Hallo Edition. U moet uw hybride verbindingen opnieuw maken.


## <a name="before-you-begin"></a>Voordat u begint
* Back-up en herstel mogelijk niet beschikbaar voor alle edities. Zie [BizTalk Services: grafiek van edities](biztalk-editions-feature-chart.md).
* Hallo klassieke Azure-portal gebruikt, kunt u een On Demand back-up maken of een geplande back-up maken. 
* Back-up van inhoud kan worden teruggezet toohello dezelfde BizTalk Service of tooa nieuwe BizTalk Service. toorestore Hallo BizTalk Service met behulp van Hallo Hallo bestaande BizTalk Service met dezelfde naam moet worden verwijderd en Hallo-naam moet beschikbaar zijn. Nadat u een BizTalk Service hebt verwijderd, kunnen duurt langer dan wilden voor Hallo dezelfde naam toobe beschikbaar. Als u niet kunt tot Hallo wachten dezelfde naam toobe beschikbaar en zet vervolgens tooa nieuwe BizTalk Service.
* BizTalk Services kunnen worden hersteld toohello dezelfde versie of een hogere editie. Herstellen van BizTalk Services tooa wordt lagere edition uit wanneer Hallo back-up is gemaakt, niet ondersteund.
  
    Bijvoorbeeld, een back-up met behulp van Hallo die Basic-editie kan worden hersteld toohello Premium Edition. Een back-up met behulp van Hallo die Premium Edition kan niet worden hersteld toohello Standard Edition.
* Hallo EDI-besturingselement cijfers zijn back-up toomaintain continuïteit van Hallo besturingselement getallen. Als berichten worden verwerkt na de laatste back-up hello, herstellen van de inhoud van deze back-up kan leiden tot dubbele besturingselement cijfers.
* Als een batch actieve berichten heeft, Hallo batch verwerkt **voordat** waarop een back-up. Wanneer u een back-up (als de benodigde of geplande) maakt, worden berichten in batches nooit worden opgeslagen. 
  
    **Als u een back-up wordt gemaakt met actieve berichten in een batch, wordt deze berichten worden niet een back-up en zijn daarom verloren.**
* Optioneel: In Hallo BizTalk Services-Portal, stopt alle beheertaken uit te voeren.

## <a name="create-a-backup"></a>Maak een back-up
Een back-up kan worden uitgevoerd op elk gewenst moment en volledig door u worden beheerd. Deze sectie vindt u Hallo stappen toocreate back-ups Hallo klassieke Azure portal, met inbegrip van:

[Op aanvraag back-up](#backupnow)

[Een back-up plannen](#backupschedule)

#### <a name="backupnow"></a>Op aanvraag back-up
1. Selecteer in de klassieke Azure-portal hello, **BizTalk Services**, en vervolgens Selecteer BizTalk services die u wenst toobackup Hallo.
2. In Hallo **Dashboard** tabblad **Back-up** Hallo Hallo pagina onderaan in.
3. Voer de naam van een back-up. Voer bijvoorbeeld *myBizTalkService*door*datum*.
4. Kies een blob storage-account en selecteer Hallo vinkje toostart Hallo back-up.

Zodra Hallo back-up is voltooid, wordt een container met Hallo back-naam die u invoert in Hallo storage-account gemaakt. Deze container bevat uw BizTalk Service back-upconfiguratie.

#### <a name="backupschedule"></a>Een back-up plannen
1. Selecteer in de klassieke Azure-portal hello, **BizTalk Services**, selecteer BizTalk Service-naam tooschedule Hallo back-up en selecteer vervolgens Hallo Hallo **configureren** tabblad.
2. Set Hallo **back-up Status** te**automatische**. 
3. Selecteer Hallo **Opslagaccount** toostore Hallo back-up, Voer Hallo **frequentie** toocreate Hallo back-ups en back-ups van hoe lang tookeep hello (**dagen bewaren**):
   
    ![][AutomaticBU]
   
    **Opmerkingen bij de**     
   
   * In **dagen bewaren**, Hallo bewaarperiode moet groter dan de back-upfrequentie Hallo.
   * Selecteer **altijd ten minste één back-up bewaren**, zelfs als deze uit het verleden Hallo bewaarperiode.
4. Selecteer **Opslaan**.

Wanneer een geplande back-uptaak wordt uitgevoerd, wordt een container (back-upgegevens toostore) in Hallo storage-account hebt gemaakt. Hallo-naam van de container Hallo heet *naam-/-tijd van de BizTalk Service*. 

Als Hallo BizTalk Service dashboard toont een **mislukt** status:

![Status van laatste geplande back-up][BackupStatus] 

Hallo koppeling opent Hallo Management Services-Bewerkingslogboeken toohelp oplossen. Zie [BizTalk Services: problemen oplossen met bewerkingslogboeken](http://go.microsoft.com/fwlink/p/?LinkId=391211).

## <a name="restore"></a>Herstellen
U kunt back-ups herstellen van Hallo klassieke Azure-portal of van Hallo [herstellen BizTalk Service REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582). Deze sectie vindt Hallo stappen toorestore met Hallo klassieke portal.

#### <a name="before-restoring-a-backup"></a>Voordat u een back-up herstellen
* Nieuwe bijhouden, archiveren en te bewaken winkels kunnen worden ingevoerd tijdens het herstellen van een BizTalk Service.
* Hallo dezelfde EDI-Runtime-gegevens is hersteld. Hallo EDI-Runtime back-up slaat Hallo besturingselement getallen. Hallo hersteld besturingselement getallen worden in volgorde van de tijd Hallo Hallo back-up. Als berichten worden verwerkt na de laatste back-up hello, herstellen van de inhoud van deze back-up kan leiden tot dubbele besturingselement cijfers.

#### <a name="restore-a-backup"></a>Een back-up terugzetten
1. Selecteer in de klassieke Azure-portal hello, **nieuw** > **App Services** > **BizTalk Service** > **herstellen** :
   
    ![Een back-up terugzetten][Restore]
2. In **back-URL**, selecteert u het pictogram map Hallo en vouw hello Azure storage-account dat winkels Hallo BizTalk Service configuratieback-up. Hallo Breid en selecteer in het rechterdeelvenster Hallo Hallo overeenkomende back-up txt-bestand. 
   <br/><br/>
   Selecteer **Open**.
3. Op Hallo **herstellen BizTalk Service** pagina, voert u een **BizTalk-servicenaam** en controleer of Hallo **domein-URL**, **Edition**, en **Regio** voor Hallo BizTalk-Service is hersteld. **Maak een nieuw exemplaar van SQL database** voor Hallo bijhouden van database:
   
    ![][RestoreBizTalkService]
   
    Selecteer Hallo pijl Volgende.
4. Controleer de naam van de Hallo van Hallo SQL-database, Hallo fysieke server waar Hallo SQL-database wordt gemaakt en een gebruikersnaam en wachtwoord invoeren voor die server.

    Als u wilt dat tooconfigure Hallo SQL database-editie, grootte en andere eigenschappen, selecteert u **geavanceerde Database-instellingen configureren**. 

    Selecteer Hallo pijl Volgende.

1. Een nieuw opslagaccount maken of voert u een bestaand opslagaccount voor Hallo BizTalk Service.
2. Selecteer Hallo vinkje toostart Hallo terugzetten.

Zodra het Hallo-herstelbewerking is voltooid, wordt een nieuwe BizTalk Service wordt vermeld in een onderbroken status op Hallo BizTalk Services pagina in Hallo klassieke Azure-portal.

### <a name="postrestore"></a>Na het terugzetten van een back-up
Hallo BizTalk Service wordt altijd hersteld een **onderbroken** status. In deze toestand is, kunt u geen configuratiewijzigingen voordat nieuwe Hallo-omgeving functioneel is, met inbegrip van:

* Als u een BizTalk Service-toepassingen met behulp van Azure BizTalk Services SDK Hallo gemaakt, moet u mogelijk tootooupdate Hallo Access Control (ACS)-referenties in die toowork toepassingen met Hallo hersteld-omgeving.
* U herstelt een BizTalk Service tooreplicate een bestaande BizTalk Service-omgeving. In dit geval, als er zijn geconfigureerd in de oorspronkelijke BizTalk Services-portal Hallo overeenkomsten die gebruikmaken van een FTP-bronmap, moet u mogelijk tooupdate Hallo overeenkomsten in de zojuist hersteld Hallo omgeving toouse een andere bron FTP-map. Anders kunnen er twee verschillende overeenkomsten toopull probeert Hallo hetzelfde bericht.
* Als u toohave omgevingen met meerdere BizTalk Service teruggezet, zorg er dan voor dat u richt de juiste omgeving Hallo in Visual Studio-toepassingen hello, PowerShell-cmdlets, REST-API's of Trading Partner Management OM API's.
* Het is een back-ups tooconfigure geautomatiseerde raadzaam op Hallo zojuist hersteld BizTalk Service-omgeving.

toostart hello BizTalk Service in Hallo klassieke Azure-portal, selecteer Hallo hersteld BizTalk Service en selecteer **hervatten** in de taakbalk Hallo. 

## <a name="what-gets-backed-up"></a>Wat wordt een back-up
Wanneer een back-up is gemaakt, hello volgende items zijn back-up gemaakt:

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH>Een back-up items</TH> 
</tr> 
<tr>
<td colspan="2">
 <strong>Azure BizTalk Services-Portal</strong></td>
</tr> 
<tr>
<td>Configuratie- en Runtime</td> 
<td>
<ul>
<li>Details van partners en -profiel</li>
<li>Partner overeenkomsten</li>
<li>Aangepaste assembly's die zijn geïmplementeerd</li>
<li>Bruggen geïmplementeerd</li>
<li>Certificaten</li>
<li>Transformaties geïmplementeerd</li>
<li>Pijplijnen</li>
<li>Sjablonen gemaakt en opgeslagen in Hallo BizTalk Services-Portal</li>
<li>X12 ST01 en GS01 toewijzingen</li>
<li>Besturingselement cijfers (EDI)</li>
<li>AS2-bericht MIC waarden</li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2">
 <strong>Azure BizTalk Service</strong></td>
</tr> 
<tr>
<td>SSL-certificaat</td> 
<td>
<ul>
<li>Gegevens van SSL-certificaat</li>
<li>Wachtwoord voor SSL-certificaat</li>
</ul>
</td>
</tr> 
<tr>
<td>BizTalk Service-instellingen</td> 
<td>
<ul>
<li>Aantal Scale-eenheden</li>
<li>Editie</li>
<li>Versie van het product</li>
<li>Regio/Datacenter</li>
<li>Access Control Service (ACS) naamruimte en -sleutel</li>
<li>Tekenreeks voor databaseverbinding bijhouden</li>
<li>Archiveren van de verbindingsreeks voor opslag-account</li>
<li>Bewaking van de verbindingsreeks voor opslag-account</li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2">
 <strong>Extra Items</strong></td>
</tr> 
<tr>
<td>Traceringsdatabase</td> 
<td>Wanneer u Hallo BizTalk Service maakt, worden Hallo bijhouden databasedetails ingevoerd, inclusief hello Azure SQL Database-Server en de databasenaam van Hallo bijhouden. Hallo bijhouden Database is geen automatisch back-gemaakt.
<br/><br/>
<strong>Belangrijk</strong><br/>
Als Hallo bijhouden Database wordt verwijderd en Hallo van de databasebehoeften is hersteld, moet een eerdere back-up bestaan. Als een back-up niet bestaat, zijn Hallo Database bijhouden en de gegevens niet hersteld. In dit geval maakt u een nieuwe Database voor het bijhouden van Hello dezelfde databasenaam. Geo-replicatie wordt aanbevolen.</td>
</tr> 
</table>

## <a name="next"></a>Volgende
toocreate Azure BizTalk Services in Azure classic portal, ga te Hallo[BizTalk Services: inrichten met behulp van Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280). toostart te maken van toepassingen, ga[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).

## <a name="see-also"></a>Zie ook
* [Back-up van BizTalk-Service](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [BizTalk Service back-up terugzetten](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [BizTalk Services: Developer, Basic, Standard en Premium-edities grafiek](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [BizTalk Services: Inrichten met behulp van Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [BizTalk Services: statusgrafiek voor de inrichting](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [BizTalk Services: de tabbladen Dashboard, Bewaken en Schalen](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [BizTalk Services: beperking](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [BizTalk Services: naam en sleutel van verlener](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [Hoe gaan gebruiken Azure BizTalk Services SDK Hallo](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

