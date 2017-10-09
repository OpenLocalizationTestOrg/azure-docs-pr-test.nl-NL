---
title: aaaManage Azure Data Lake Analytics met behulp van Azure-portal Hallo | Microsoft Docs
description: Meer informatie over hoe Data Lake Analytics acounts, gegevens toomanage, gebruikers bronnen, en taken.
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: a0e045f1-73d6-427f-868d-7b55c10f811b
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: f63ccdfae79772c92e92462194e8cdc636a73dc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-by-using-hello-azure-portal"></a>Azure Data Lake Analytics beheren met behulp van hello Azure-portal
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Meer informatie over hoe Hallo toomanage Azure Data Lake Analytics-accounts, gegevensbronnen account, gebruikers en taken met behulp van Azure-portal. toosee management onderwerpen over het gebruik van andere hulpprogramma's, klikt u op een tabblad bovenaan Hallo Hallo pagina.

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-lake-analytics-accounts"></a>Data Lake Analytics-accounts beheren

### <a name="create-an-account"></a>Een account maken

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op **Nieuw** > **Intelligence + analyse** > **Data Lake Analytics**.
3. Waarden selecteren voor Hallo volgende items: 
   1. **Naam**: naam Hallo Hallo Data Lake Analytics-account.
   2. **Abonnement**: hello Azure-abonnement gebruikt voor het Hallo-account.
   3. **Resourcegroep**: hello Azure resourcegroep in welk toocreate Hallo-account. 
   4. **Locatie**: hello Azure-datacenter voor Hallo Data Lake Analytics-account. 
   5. **Data Lake Store**: Hallo standaard store toobe gebruikt voor Hallo Data Lake Analytics-account. Hello Azure Data Lake Store-account en Hallo Data Lake Analytics-account moet zich in Hallo dezelfde locatie.
4. Klik op **Create**. 

### <a name="delete-a-data-lake-analytics-account"></a>Een Data Lake Analytics-account verwijderen

Voordat u een Data Lake Analytics-account verwijdert, verwijdert u de Data Lake Store-standaardaccount.

1. Ga in de Azure-portal hello, tooyour Data Lake Analytics-account.
2. Klik op **Verwijderen**.
3. Typenaam Hallo-account.
4. Klik op **Verwijderen**.

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-sources"></a>Gegevensbronnen beheren

Data Lake Analytics ondersteunt Hallo gegevensbronnen te volgen:

* Data Lake Store
* Azure Storage

U kunt Data Explorer toobrowse gegevensbronnen gebruiken en basic bestand beheerbewerkingen uitvoeren. 

### <a name="add-a-data-source"></a>Een gegevensbron toevoegen

1. Ga in de Azure-portal hello, tooyour Data Lake Analytics-account.
2. Klik op **gegevensbronnen**.
3. Klik op **gegevensbron toevoegen**.
    
   * tooadd een Data Lake Store-account, moet u Hallo-account en toohello account toobe kunnen tooquery deze.
   * tooadd Azure Blob-opslag, moet u Hallo storage-account en accountsleutel Hallo. toofind ze, gaat u toohello storage-account in Hallo-portal.

## <a name="set-up-firewall-rules"></a>Firewallregels instellen

U kunt Data Lake Analytics toofurther vergrendelen toegang tooyour Data Lake Analytics-account op netwerkniveau hello gebruiken. U kunt een firewall inschakelen, Geef een IP-adres of een IP-adresbereik voor de vertrouwde clients te definiëren. Nadat u deze maatregelen hebt ingeschakeld, kunnen alleen clients waarvoor Hallo IP-adressen binnen het bereik van Hallo gedefinieerd verbinding toohello store maken.

Als andere Azure-services, zoals Azure Data Factory- of virtuele machines, verbinding toohello Data Lake Analytics-account maakt, controleert u of **Azure-Services toestaan** is ingeschakeld **op**. 

### <a name="set-up-a-firewall-rule"></a>Een firewallregel instellen

1. Ga in de Azure-portal hello, tooyour Data Lake Analytics-account.
2. Klik op het menu aan de linkerkant Hallo Hallo **Firewall**.

## <a name="add-a-new-user"></a>Een nieuwe gebruiker toevoegen

U kunt Hallo **Wizard gebruiker toevoegen** tooeasily nieuwe Data Lake gebruikers hebt ingericht.

1. Ga in de Azure-portal hello, tooyour Data Lake Analytics-account.
2. Op Hallo links, klikt u onder **aan de slag**, klikt u op **Wizard gebruiker toevoegen**.
3. Selecteer een gebruiker en klik vervolgens op **Selecteer**.
4. Selecteer een rol en klik vervolgens op **Selecteer**. tooset van een nieuwe developer toouse Azure Data Lake, selecteer Hallo **Data Lake Analytics Developer** rol.
5. Selecteer Hallo toegangsbeheerlijsten (ACL's) voor Hallo U-SQL-databases. Wanneer u tevreden met uw keuzes bent, klikt u op **Selecteer**.
6. Selecteer Hallo ACL's voor bestanden. Voor het standaardarchief hello, niet te wijzigen Hallo ACL's voor de hoofdmap Hallo '/' en voor Hallo/System-map. Klik op **Selecteren**.
7. Controleer de geselecteerde wijzigingen en klik vervolgens op **uitvoeren**.
8. Wanneer het Hallo-wizard is voltooid, klikt u op **gedaan**.

## <a name="manage-role-based-access-control"></a>Toegangsbeheer op basis van rollen beheren

Net als andere Azure-services, kunt u rollen gebaseerd toegangsbeheer (RBAC) toocontrol hoe gebruikers interacteren met Hallo-service.

Hallo standaard RBAC-rollen hebben Hallo volgende mogelijkheden:
* **Eigenaar**: kunt verzenden van taken, taken controleren, annuleren taken van elke gebruiker en Hallo-account configureren.
* **Inzender**: kunt verzenden van taken, taken controleren, annuleren taken van elke gebruiker en Hallo-account configureren.
* **Lezer**: taken kunt bewaken.

Hallo Data Lake Analytics Developer rol tooenable U-SQL-ontwikkelaars toouse Hallo Data Lake Analytics service gebruiken. U kunt Hallo Data Lake Analytics Developer-rol:
* Verzenden van taken.
* De voortgang taak status en Hallo van taken die worden verzonden door een gebruiker.
* Zie Hallo U-SQL-scripts uit taken die worden aangeboden door een gebruiker.
* Alleen uw eigen taken annuleren.

### <a name="add-users-or-security-groups-tooa-data-lake-analytics-account"></a>Gebruikers- of beveiliging groepen tooa Data Lake Analytics-account toevoegen

1. Ga in de Azure-portal hello, tooyour Data Lake Analytics-account.
2. Klik op **toegangsbeheer (IAM)** > **toevoegen**.
3. Selecteer een rol.
4. Een gebruiker toevoegen.
5. Klik op **OK**.

>[!NOTE]
>Als een gebruiker of een beveiligingsgroep toosubmit taken moet, nodig ze ook machtiging op Hallo store-account. Zie voor meer informatie [beveiliging van gegevens die zijn opgeslagen in Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).
>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-jobs"></a>Taken beheren

### <a name="submit-a-job"></a>Verzenden van een taak

1. Ga in de Azure-portal hello, tooyour Data Lake Analytics-account.

2. Klik op **nieuwe taak**. Voor elke taak configureren:

    1. **Taaknaam**: Hallo-naam van Hallo-taak.
    2. **Prioriteit**: lagere getallen hebben een hogere prioriteit. Als u twee taken in de wachtrij staan, Hallo met lagere prioriteitswaarde eerste wordt uitgevoerd.
    3. **Parallelle uitvoering**: Hallo kunt u het maximum aantal compute tooreserve voor deze taak worden verwerkt.

3. Klik op **Taak verzenden**.

### <a name="monitor-jobs"></a>Taken controleren

1. Ga in de Azure-portal hello, tooyour Data Lake Analytics-account.
2. Klik op **alle taken weergeven**. Een lijst met alle Hallo actief en recent voltooide taken in Hallo-account wordt weergegeven.
3. Klik desgewenst op **Filter** toohelp vindt u de taken op Hallo **tijdsbereik**, **taaknaam**, en **auteur** waarden. 

### <a name="monitoring-pipeline-jobs"></a>Taken van de pijplijn bewaken
Taken die deel van een pijplijn uitmaken werken samen, meestal opeenvolgend tooaccomplish een specifiek scenario. U kunt bijvoorbeeld een pijplijn die schoongemaakt, pakt, transformaties, gebruik voor de klant insights aggregeert hebben. Pipeline-taken worden aangeduid met Hallo "Pipeline" eigenschap bij het Hallo-taak is verzonden. Taken gepland met ADF V2 hebben automatisch deze eigenschap is ingevuld. 

een lijst met U-SQL-taken die deel van pijplijnen uitmaken tooview: 

1. Ga in de Azure-portal hello, tooyour Data Lake Analytics-accounts.
2. Klik op **taak Insights**. Hallo die tabblad 'Alle taken' wordt standaard ingesteld, bevat een overzicht van die wordt uitgevoerd, in de wachtrij en taken beëindigd.
3. Klik op Hallo **pijplijn taken** tabblad. Een lijst met taken van de pijplijn wordt weergegeven samen met de samengevoegde statistieken voor elke pijplijn.

### <a name="monitoring-recurring-jobs"></a>Terugkerende taken bewaken
Een terugkerende taak is een die Hallo heeft dezelfde bedrijfslogica hierbij wordt gebruikgemaakt van verschillende invoergegevens telkens wanneer deze wordt uitgevoerd. In het ideale geval moeten terugkerende taken altijd slagen en hebben relatief stabiel uitvoeringstijd; Deze problemen bewaking helpt ervoor te zorgen Hallo-taak is in orde. Terugkerende taken worden aangeduid met Hallo "Recurrence" eigenschap. Taken gepland met ADF V2 hebben automatisch deze eigenschap is ingevuld.

een lijst met U-SQL-taken die zijn terugkerende tooview: 

1. Ga in de Azure-portal hello, tooyour Data Lake Analytics-accounts.
2. Klik op **taak Insights**. Hallo die tabblad 'Alle taken' wordt standaard ingesteld, bevat een overzicht van die wordt uitgevoerd, in de wachtrij en taken beëindigd.
3. Klik op Hallo **terugkerende taken** tabblad. Een lijst met terugkerende taken wordt samen met de samengevoegde statistieken voor elke terugkerende taak weergegeven.

## <a name="manage-policies"></a>Beleid beheren

### <a name="account-level-policies"></a>Beleid account-niveau

Deze beleidsregels van toepassing tooall taken in een Data Lake Analytics-account.

#### <a name="maximum-number-of-aus-in-a-data-lake-analytics-account"></a>Maximum aantal AUs in een Data Lake Analytics-account
Een beleid regelt Hallo kunt u het totale aantal Analytics-eenheden (AUs) uw Data Lake Analytics-account kunt gebruiken. Hallo-waarde is standaard too250. Als deze waarde is ingesteld too250 AUs, u kunt bijvoorbeeld één taak uitgevoerd met 250 AUs toegewezen tooit of 10 taken uitgevoerd met 25 AUs elke. Aanvullende taken die zijn ingediend in de wachtrij staan totdat Hallo actieve taken zijn voltooid. Wanneer taken zijn voltooid, AUs worden vrijgemaakt voor de Hallo toorun taken in de wachtrij.

toochange hello aantal AUs voor uw Data Lake Analytics-account:

1. Ga in de Azure-portal hello, tooyour Data Lake Analytics-account.
2. Klik op **Eigenschappen**.
3. Onder **maximale AUs**, verplaatsen Hallo schuifregelaar tooselect een waarde of Hallo waarde invoeren in het tekstvak Hallo. 
4. Klik op **Opslaan**.

> [!NOTE]
> Als u moet meer dan standaard (250) Hallo AUs, klik in Hallo portal op **Help + ondersteuning** toosubmit ondersteuning aan te vragen. Hallo aantal AUs beschikbaar in uw Data Lake Analytics-account kan worden verhoogd.
>

#### <a name="maximum-number-of-jobs-that-can-run-simultaneously"></a>Maximum aantal taken dat tegelijkertijd kan worden uitgevoerd
Een beleid bepaalt hoeveel taken kunnen uitvoeren op Hallo hetzelfde moment. Standaard is deze waarde too20 ingesteld. Als uw Data Lake Analytics AUs beschikbaar heeft, worden nieuwe taken geplande toorun onmiddellijk totdat Hallo totaal aantal actieve taken Hallo-waarde van dit beleid heeft bereikt. Wanneer u Hallo kunt u het maximum aantal taken dat tegelijkertijd kan worden uitgevoerd bereikt, latere taken in de wachtrij staan in volgorde van prioriteit als een of meer actieve taken hebt voltooid (afhankelijk van de beschikbaarheid van Australië).

toochange hello aantal taken dat tegelijk kunt uitvoeren:

1. Ga in de Azure-portal hello, tooyour Data Lake Analytics-account.
2. Klik op **Eigenschappen**.
3. Onder **Maximum aantal van een actief taken**, verplaatsen Hallo schuifregelaar tooselect een waarde of Hallo waarde invoeren in het tekstvak Hallo. 
4. Klik op **Opslaan**.

> [!NOTE]
> Als u meer dan Hallo standaard (20) aantal taken in Hallo-portal klikt u op toorun moet **Help + ondersteuning** toosubmit ondersteuning aan te vragen. Hallo aantal taken dat tegelijk in uw Data Lake Analytics-account uitvoeren kunt kan worden verhoogd.
>

#### <a name="how-long-tookeep-job-metadata-and-resources"></a>Hoe lang tookeep taak metagegevens en resources 
Wanneer uw gebruikers U-SQL-taken uitvoeren, behoudt Hallo Data Lake Analytics-service alle bijbehorende bestanden. Verwante bestanden bevatten Hallo U-SQL-script waarnaar wordt verwezen in Hallo U-SQL-script, gecompileerde bronnen en statistieken van Hallo dll-bestanden. Hallo-bestanden zijn in Hallo /system/ map van Hallo standaard Azure Data Lake Storage-account. Dit beleid bepaalt hoe lang deze resources worden opgeslagen voordat ze automatisch worden verwijderd (Hallo standaardwaarde is 30 dagen). U kunt deze bestanden gebruiken voor foutopsporing en voor prestaties afstemmen van taken die u opnieuw in toekomstige Hallo gaat uitvoeren.

toochange hoe lang tookeep taak metagegevens en bronnen:

1. Ga in de Azure-portal hello, tooyour Data Lake Analytics-account.
2. Klik op **Eigenschappen**.
3. Onder **dagen tooRetain taak voert een query**, verplaatsen Hallo schuifregelaar tooselect een waarde of Hallo waarde invoeren in het tekstvak Hallo.  
4. Klik op **Opslaan**.

### <a name="job-level-policies"></a>Beleid Job-niveau
U kunt beheren met beleid voor niveau van de taak Hallo maximale AUs en Hallo maximumprioriteit individuele gebruikers (of leden van bepaalde beveiligingsgroepen) kunnen worden ingesteld voor taken die ze verzenden. Dit kunt u Hallo kosten van gebruikers beheren. U kunt ook besturingselement Hallo effect dat taken worden geplande mogelijk hebt u een hoge prioriteit productietaken die worden uitgevoerd in Hallo dezelfde Data Lake Analytics-account.

Data Lake Analytics heeft twee beleidsregels die u op Hallo taakniveau instellen kunt:

* **Australië limiet is per taak**: gebruikers kunnen alleen taken die u een aantal AUs toothis hebt indienen. Standaard is deze limiet Hallo hetzelfde als Hallo Australië maximumlimiet voor Hallo-account.
* **Prioriteit**: gebruikers kunnen alleen indienen voor taken met een prioriteitswaarde toothis lager is dan of gelijk zijn. Houd er rekening mee dat een hoger getal een lagere prioriteit geeft. Dit is standaard too1, namelijk Hallo hoogst mogelijke prioriteit.

Er is een standaardbeleid instellen voor elke account. Hallo-standaardbeleid is van toepassing tooall gebruikers van Hallo-account. U kunt extra beleidsregels instellen voor specifieke gebruikers en groepen. 

> [!NOTE]
> Beleidsregels voor account-niveau en op jobniveau toepassing tegelijk.
>

#### <a name="add-a-policy-for-a-specific-user-or-group"></a>Een beleid voor een specifieke gebruiker of groep toevoegen

1. Ga in de Azure-portal hello, tooyour Data Lake Analytics-account.
2. Klik op **Eigenschappen**.
3. Onder **taak verzending limieten**, klikt u op Hallo **beleid toevoegen** knop. Vervolgens, selecteer of typ Hallo volgende instellingen:
    1. **Beleidsnaam COMPUTE**: Voer een naam voor beleid tooremind u Hallo doel van Hallo-beleid.
    2. **Gebruiker of groep selecteren**: Selecteer Hallo-gebruiker of groep die dit beleid is van toepassing op.
    3. **Hallo Australië taaklimiet ingesteld**: Hallo Australië limiet die van toepassing toohello is geselecteerde gebruiker of groep.
    4. **Hallo prioriteit limiet ingesteld**: Hallo prioriteit limiet die van toepassing toohello is geselecteerde gebruiker of groep.

4. Klik op **OK**.

5. Hallo nieuwe beleid wordt weergegeven in Hallo **standaard** beleid tabel onder **taak verzending limieten**. 

#### <a name="delete-or-edit-an-existing-policy"></a>Verwijder of een bestaand beleid bewerken

1. Ga in de Azure-portal hello, tooyour Data Lake Analytics-account.
2. Klik op **Eigenschappen**.
3. Onder **taak verzending limieten**, zoeken Hallo beleid gewenste tooedit.
4.  Hallo toosee **verwijderen** en **bewerken** opties in de meest rechtse kolom Hallo van Hallo tabel, klikt u op **...** .

### <a name="additional-resources-for-job-policies"></a>Aanvullende bronnen voor taak-beleid
* [Blogbericht beleid-overzicht](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)
* [Blogbericht beleid account-niveau](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)
* [Blogbericht beleid Job-niveau](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)

## <a name="next-steps"></a>Volgende stappen

* [Overzicht van Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Aan de slag met Data Lake Analytics met behulp van hello Azure-portal](data-lake-analytics-get-started-portal.md)
* [Azure Data Lake Analytics beheren met behulp van Azure PowerShell](data-lake-analytics-manage-use-powershell.md)

