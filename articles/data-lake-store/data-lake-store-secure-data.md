---
title: aaaSecuring opgeslagen gegevens in Azure Data Lake Store | Microsoft Docs
description: Meer informatie over hoe toosecure gegevens in Azure Data Lake Store met behulp van groepen en toegang beheren voor een lijst met
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ca35e65f-3986-4f1b-bf93-9af6066bb716
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 2b4ed7e322e1843ca47d6968ec8801ac19ea6399
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="securing-data-stored-in-azure-data-lake-store"></a>De beveiliging van gegevens die zijn opgeslagen in Azure Data Lake Store
Gegevens beveiligen in Azure Data Lake Store is een benadering drie stappen.

1. Begint met het maken van beveiligingsgroepen in Azure Active Directory (AAD). Deze beveiligingsgroepen worden gebruikt tooimplement op rollen gebaseerde toegangsbeheer (RBAC) in Azure Portal. Zie voor meer informatie [toegangsbeheer op basis van rollen in Microsoft Azure](../active-directory/role-based-access-control-configure.md).
2. Hallo AAD beveiliging groepen toohello Azure Data Lake Store-account toewijzen. Hiermee bepaalt u access toohello Data Lake Store-account van Hallo portal- en beheerbewerkingen van Hallo portal of API's.
3. Hallo AAD-beveiligingsgroepen toewijzen toegangsbeheerlijsten (ACL's) op Hallo Data Lake Store-bestandssysteem.
4. U kunt daarnaast ook een IP-adresbereik voor clients die toegang gegevens in Data Lake Store Hallo tot instellen.

In dit artikel vindt u instructies voor hoe toouse hello Azure portal tooperform Hallo hierboven taken. Zie voor gedetailleerde informatie over hoe Data Lake Store implementeert voor beveiliging op het niveau voor het account en gegevens van Hallo [beveiliging in Azure Data Lake Store](data-lake-store-security-overview.md). Zie voor informatie over hoe ACL's worden geïmplementeerd in Azure Data Lake Store dieper [overzicht van toegangsbeheer in Data Lake Store](data-lake-store-access-control.md).

## <a name="prerequisites"></a>Vereisten
Voordat u deze zelfstudie begint, moet u de volgende Hallo hebben:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).
* **Een Azure Data Lake Store-account**. Voor instructies over het toocreate één, Zie [aan de slag met Azure Data Lake Store](data-lake-store-get-started-portal.md)

## <a name="create-security-groups-in-azure-active-directory"></a>Beveiligingsgroepen maken in Azure Active Directory
Voor instructies over het toocreate AAD-beveiligingsgroepen en hoe tooadd toohello-gebruikersgroep, Zie [beheren in Azure Active Directory-beveiligingsgroepen](../active-directory/active-directory-accessmanagement-manage-groups.md).

> [!NOTE] 
> U kunt zowel gebruikers als andere groepen tooa groep toevoegen in Azure AD dat gebruikmaakt van hello Azure-portal. Echter, in volgorde van de groep van een service-principal tooa voor tooadd, gebruikt u [Azure AD PowerShell-module](../active-directory/active-directory-accessmanagement-groups-settings-v2-cmdlets.md).
> 
> ```powershell
> # Get hello desired group and service principal and identify hello correct object IDs
> Get-AzureADGroup -SearchString "<group name>"
> Get-AzureADServicePrincipal -SearchString "<SPI name>"
> 
> # Add hello service principal toohello group
> Add-AzureADGroupMember -ObjectId <Group object ID> -RefObjectId <SPI object ID>
> ```
 
## <a name="assign-users-or-security-groups-tooazure-data-lake-store-accounts"></a>Toewijzen van gebruikers of beveiligingsgroepen tooAzure Data Lake Store-accounts
Wanneer u toewijzen aan gebruikers of tooAzure Data Lake Store-accounts beveiligingsgroepen, kunt u access toohello beheerbewerkingen op Hallo-account met behulp van hello Azure-portal en Azure Resource Manager-API's beheren. 

1. Open een Azure Data Lake Store-account. Klik in het linkerdeelvenster hello, **Bladeren**, klikt u op **Data Lake Store**, en klik vervolgens op Hallo account naam toowhich die u wilt dat een gebruiker of beveiligingsgroep groep tooassign Hallo Data Lake Store-blade.

2. Klik in de instellingenblade van Data Lake Store-account op **Access Control (IAM)**. Hallo-blade door standaardlijsten **abonnementsbeheerders** als eigenaar van een groep.
   
    ![Beveiliging groep tooAzure Data Lake Store-account toewijzen](./media/data-lake-store-secure-data/adl.select.user.icon.png "beveiliging groep tooAzure Data Lake Store-account toewijzen")

    Er zijn twee manieren tooadd van een groep en toewijzen relevante rollen.
   
    * Een gebruiker of groep toohello-account toevoegen en vervolgens een rol toewijzen of
    * Een functie toevoegen en vervolgens gebruikers/groepen toorole toewijzen.
     
    In dit gedeelte kijken we de eerste benadering hello, een groep toe te voegen en vervolgens het toewijzen van rollen. U kunt vergelijkbare stappen toofirst Selecteer een rol uitvoeren en vervolgens groepen toothat rol toe te wijzen.
4. In Hallo **gebruikers** blade, klikt u op **toevoegen** tooopen hello **toegang toevoegen** blade. In Hallo **toegang toevoegen** blade, klikt u op **Selecteer een rol**, en selecteer vervolgens een rol voor Hallo gebruiker of groep.
   
    ![Toevoegen van een rol voor de gebruiker Hallo](./media/data-lake-store-secure-data/adl.add.user.1.png "een rol voor Hallo gebruiker toevoegen")
   
    Hallo **eigenaar** en **Inzender** rol bieden toegang tooa diverse functies voor beheer op Hallo data lake-account. Voor gebruikers die met de gegevens in data lake van hello communiceren, kunt u deze toevoegen toohello ** lezer ** rol. Hallo-bereik van deze rollen zijn beperkt toohello management operations gerelateerde toohello Azure Data Lake Store-account.
   
    Voor gegevens definiëren operations afzonderlijke bestandssysteemmachtigingen Hallo gebruikers kunnen uitvoeren. Daarom een gebruiker met een lezersrol kunt alleen beheerdersrechten instellingen weergeven die zijn gekoppeld aan het Hallo-account, maar kan mogelijk lezen en schrijven gegevens op basis van machtigingen voor het bestandssysteem toothem toegewezen. Data Lake Store-bestandssysteemmachtigingen wordt beschreven op [beveiligingsgroep toewijzen als ACL's toohello Azure Data Lake Store-bestandssysteem](#filepermissions).
5. In Hallo **toegang toevoegen** blade, klikt u op **gebruikers toevoegen** tooopen hello **gebruikers toevoegen** blade. Zoek in deze blade Hallo-beveiligingsgroep die u eerder in Azure Active Directory gemaakt. Als u een groot aantal groepen toosearch van hebt, gebruik Hallo bovenste toofilter op Hallo groepsnaam Hallo tekstvak. Klik op **Selecteren**.
   
    ![Een beveiligingsgroep toevoegt](./media/data-lake-store-secure-data/adl.add.user.2.png "beveiligingsgroep toevoegen")
   
    Als u wilt dat tooadd een groep/gebruiker die niet wordt vermeld, kunt u ze met behulp van Hallo uitnodigen **uitnodigen** pictogram en Hallo e-mailadres voor Hallo gebruiker of groep op te geven.
6. Klik op **OK**. U ziet Hallo-beveiligingsgroep die is toegevoegd, zoals hieronder wordt weergegeven.
   
    ![Beveiligingsgroep toegevoegd](./media/data-lake-store-secure-data/adl.add.user.3.png "beveiligingsgroep toegevoegd")

7. De gebruiker/beveiligingsgroep heeft nu toegang toohello Azure Data Lake Store-account. Als u wilt dat gebruikers toospecific tooprovide, kunt u ze toohello beveiligingsgroep toevoegen. Op dezelfde manier als u toorevoke voor een gebruiker toegang wilt, kunt u deze uit de beveiligingsgroep Hallo. U kunt meerdere beveiligingsgroepen ook tooan account toewijzen. 

## <a name="filepermissions"></a>Gebruikers- of beveiligingsgroep toewijzen als ACL's toohello bestandssysteem van Azure Data Lake Store
Gebruiker/beveiligingsgroepen toohello Azure Data Lake-bestandssysteem toewijst, kunt u toegangsbeheer op Hallo opgeslagen gegevens in Azure Data Lake Store instellen.

1. Klik op de blade van het Data Lake Store-account op **Gegevensverkenner**.
   
    ![Mappen maken in Data Lake Store-account](./media/data-lake-store-secure-data/adl.start.data.explorer.png "mappen maken in Data Lake-account")
2. In Hallo **Data Explorer** blade, klikt u op het Hallo-bestand of map waarvoor u wilt dat tooconfigure Hallo ACL en klik vervolgens op **toegang**. tooassign ACL tooa-bestand, klikt u op **toegang** van Hallo **bestandsvoorbeeld** blade.
   
    ![ACL's ingesteld op Data Lake-bestandssysteem](./media/data-lake-store-secure-data/adl.acl.1.png "ACL's ingesteld op Data Lake-bestandssysteem")
3. Hallo **toegang** blade bevat standaard toegang Hallo en aangepaste toegang toohello hoofdmap al toegewezen. Klik op Hallo **toevoegen** pictogram tooadd aangepast-niveau ACL's.
   
    ![Standaard- en aangepaste toegang lijst](./media/data-lake-store-secure-data/adl.acl.2.png "lijst standaard en aangepaste toegang")
   
   * **Standaard toegang** is hello UNIX-stijl toegang, waarin u opgeeft te lezen, schrijven, uitvoeren (rwx) toothree distinct gebruikersklassen: eigenaar, groep en anderen.
   * **Aangepaste toegang** overeenkomt met toohello POSIX-ACL's waarmee u tooset machtigingen voor specifieke benoemde gebruikers of groepen, en niet alleen Hallo-bestand eigenaar of groep. 
     
     Zie voor meer informatie [HDFS-ACL's](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_Access_Control_Lists). Zie voor meer informatie over hoe de ACL's worden geïmplementeerd in Data Lake Store, [toegangsbeheer in Data Lake Store](data-lake-store-access-control.md).
4. Klik op Hallo **toevoegen** pictogram tooopen hello **aangepaste toegang toevoegen** blade. Klik op deze blade **gebruiker of groep selecteren**, en klik vervolgens in **gebruiker of groep selecteren** blade, zoekt u Hallo-beveiligingsgroep die u eerder in Azure Active Directory gemaakt. Als u een groot aantal groepen toosearch van hebt, gebruik Hallo bovenste toofilter op Hallo groepsnaam Hallo tekstvak. Klik op groep Hallo u tooadd wilt en klik vervolgens op **Selecteer**.
   
    ![Een groep toevoegen](./media/data-lake-store-secure-data/adl.acl.3.png "een groep toevoegen")
5. Klik op **Selecteer machtigingen**, selecteer Hallo machtigingen en of u wilt dat tooassign Hallo machtigingen standaard ACL, toegang krijgen tot ACL of beide. Klik op **OK**.
   
    ![Wijs machtigingen toogroup](./media/data-lake-store-secure-data/adl.acl.4.png "toogroup machtigingen toewijzen")
   
    Zie voor meer informatie over de machtigingen in Data Lake Store en/toegang ACL's, [toegangsbeheer in Data Lake Store](data-lake-store-access-control.md).
6. In Hallo **aangepaste toegang toevoegen** blade, klikt u op **OK**. Hallo toegevoegde groep met machtigingen Hallo die zijn gekoppeld, wordt nu weergegeven in Hallo **toegang** blade.
   
    ![Wijs machtigingen toogroup](./media/data-lake-store-secure-data/adl.acl.5.png "toogroup machtigingen toewijzen")
   
   > [!IMPORTANT]
   > In de huidige release hello, kunt u slechts 9 vermeldingen onder hebt **aangepaste toegang**. Als u meer dan 9 gebruikers tooadd wilt, moet u beveiligingsgroepen maken gebruikers toosecurity groepen toevoegen, toevoegen toothose beveiligingsgroepen toegang bieden voor Hallo Data Lake Store-account.
   > 
   > 
7. Indien nodig, kunt u toegangsmachtigingen Hallo ook wijzigen nadat u hebt Hallo groep toegevoegd. Selectievakje wissen of selecteer Hallo voor elke machtiging (lezen, schrijven, uitvoeren) op basis van of u wilt dat tooremove of wijs toe die machtiging toohello-beveiligingsgroep. Klik op **opslaan** toosave Hallo wijzigingen, of **negeren** tooundo Hallo wijzigingen.

## <a name="set-ip-address-range-for-data-access"></a>Instellen van IP-adresbereik voor toegang tot gegevens
Azure Data Lake Store kunt u toegang tot tooyour data store op niveau voor het vergrendelen van toofurther. U kunt firewall inschakelen, Geef een IP-adres of een IP-adresbereik voor de vertrouwde clients te definiëren. Eenmaal is ingeschakeld, kunnen alleen clients waarvoor Hallo IP-adressen binnen het gedefinieerde bereik verbinding toohello store maken.

![Firewall-instellingen en IP-toegang tot](./media/data-lake-store-secure-data/firewall-ip-access.png "Firewall-instellingen en IP-adres")

## <a name="remove-security-groups-for-an-azure-data-lake-store-account"></a>Beveiligingsgroepen voor een Azure Data Lake Store-account verwijderen
Wanneer u beveiligingsgroepen uit Azure Data Lake Store-accounts verwijderen, wijzigt u alleen toegang toohello beheerbewerkingen op Hallo-account met behulp van hello Azure-Portal en Azure Resource Manager-API's.

1. Klik in de blade van het Data Lake Store-account op **instellingen**. Van Hallo **instellingen** blade, klikt u op **gebruikers**.
   
    ![Beveiliging groep tooAzure Data Lake account toewijzen](./media/data-lake-store-secure-data/adl.select.user.icon.png "beveiliging groep tooAzure Data Lake account toewijzen")
2. In Hallo **gebruikers** blade klikt u op het Hallo-beveiligingsgroep die u wilt dat tooremove.
   
    ![Beveiliging groep tooremove](./media/data-lake-store-secure-data/adl.add.user.3.png "beveiliging groep tooremove")
3. Klik op Hallo blade voor de beveiligingsgroep Hallo **verwijderen**.
   
    ![Beveiligingsgroep verwijderd](./media/data-lake-store-secure-data/adl.remove.group.png "beveiligingsgroep verwijderd")

## <a name="remove-security-group-acls-from-azure-data-lake-store-file-system"></a>Verwijderen van beveiligingsgroep ACL's van Azure Data Lake Store-bestandssysteem
Wanneer u beveiligingsgroepen ACL's van Azure Data Lake Store-bestandssysteem verwijdert, kunt u access toohello-gegevens in Data Lake Store Hallo wijzigen.

1. Klik op de blade van het Data Lake Store-account op **Gegevensverkenner**.
   
    ![Mappen maken in Data Lake-account](./media/data-lake-store-secure-data/adl.start.data.explorer.png "mappen maken in Data Lake-account")
2. In Hallo **Data Explorer** blade, klik op Hallo-bestand of map waarvoor u tooremove Hallo ACL wilt en klikt u in de blade van het account Hallo **toegang** pictogram. tooremove ACL voor een bestand, klikt u op **toegang** van Hallo **bestandsvoorbeeld** blade.
   
    ![ACL's ingesteld op Data Lake-bestandssysteem](./media/data-lake-store-secure-data/adl.acl.1.png "ACL's ingesteld op Data Lake-bestandssysteem")
3. In Hallo **toegang** blade van Hallo **aangepaste toegang** sectie, klikt u op Hallo-beveiligingsgroep die u wilt dat tooremove. In Hallo **aangepaste toegang** blade, klikt u op **verwijderen** en klik vervolgens op **OK**.
   
    ![Wijs machtigingen toogroup](./media/data-lake-store-secure-data/adl.remove.acl.png "toogroup machtigingen toewijzen")

## <a name="see-also"></a>Zie ook
* [Overzicht van Azure Data Lake Store](data-lake-store-overview.md)
* [Gegevens kopiëren van Azure Storage Blobs tooData Lake Store](data-lake-store-copy-data-azure-storage-blob.md)
* [Azure Data Lake Analytics gebruiken met Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight gebruiken met Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Aan de slag met Data Lake Store met behulp van PowerShell](data-lake-store-get-started-powershell.md)
* [Aan de slag met Data Lake Store met .NET SDK](data-lake-store-get-started-net-sdk.md)
* [Diagnostische logboeken openen voor Data Lake Store](data-lake-store-diagnostic-logs.md)

