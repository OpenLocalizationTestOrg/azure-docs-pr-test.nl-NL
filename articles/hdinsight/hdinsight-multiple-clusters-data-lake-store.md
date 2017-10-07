---
title: meerdere HDInsight-clusters met een Azure Data Lake Store-account - Azure aaaUse | Microsoft Docs
description: "Meer informatie over hoe toouse meer dan één HDInsight-cluster met één Data Lake Store-account"
keywords: hdinsight-opslag, hdfs, gestructureerde gegevens, ongestructureerde gegevens, data lake store
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: nitinme
ms.openlocfilehash: 3a125b91fcc1e436270a1bd349f7a2d8f27e06fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-multiple-hdinsight-clusters-with-an-azure-data-lake-store-account"></a>Meerdere HDInsight-clusters met een Azure Data Lake Store-account gebruiken

Beginnen met HDInsight versie 3.5, kunt u HDInsight-clusters maken met Azure Data Lake Store-accounts als Hallo standaard bestandssysteem.
Data Lake Store biedt onbeperkte opslag die het maakt niet alleen voor het hosten van grote hoeveelheden gegevens; ideaal ondersteuning maar ook voor het hosten van meerdere HDInsight-clusters die share één Data Lake Store-Account. Zie voor instructionson hoe toocreate een HDInsight-cluster met Data Lake Store als Hallo opslag, [HDInsight-clusters maken met Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

Dit artikel bevat aanbevelingen toohello Data Lake store-beheerder voor het instellen van een enkel en gedeelde Data Lake opslaan-Account waarmee u over meerdere **active** HDInsight-clusters. Deze aanbevelingen toepassing toohosting meerdere beveiligde, evenals een niet-beveiligde Hadoop-clusters op een gedeelde Data Lake store-account.


## <a name="data-lake-store-file-and-folder-level-acls"></a>Data Lake Store bestanden en mappen niveau ACL 's

Hallo rest van dit artikel wordt ervan uitgegaan dat u een goede kennis hebben van bestanden en mappen niveau ACL's in Azure Data Lake Store, die wordt beschreven op [toegangsbeheer in Azure Data Lake Store](../data-lake-store/data-lake-store-access-control.md).

## <a name="data-lake-store-setup-for-multiple-hdinsight-clusters"></a>Data Lake Store-installatie voor meerdere HDInsight-clusters
Laat het ons nemen een maphiërarchie met twee niveaus tooexplain Hallo aanbevelingen voor het gebruik van bevat meerdere HDInsight-clusters met een Data Lake Store-account. Houd rekening met het hebben van een Data Lake Store-account met de mapstructuur Hallo **/clusters/financiën**. Met deze structuur alle Hallo clusters vereist door Hallo Financiën organisatie /clusters/finance als opslaglocatie hello gebruiken. In Hallo toekomstige als een andere organisatie spreken Marketing, wil toocreate HDInsight-clusters met Hallo hetzelfde Data Lake Store-account, /clusters/marketing kan worden gemaakt. Nu gaan we gebruiken **/clusters/financiën**.

tooenable deze map structuur toobe effectief door HDInsight-clusters gebruikt, Hallo Data Lake Store-beheerder moet toewijzen gemachtigd, zoals beschreven in de tabel Hallo. Hallo-machtigingen weergegeven in de tabel Hallo overeen tooAccess-ACL's en geen standaard-ACL's. 


|Map  |Machtigingen  |Gebruiker die eigenaar is  |Groep die eigenaar is  | Benoemde gebruiker | Benoemde gebruikersmachtigingen | Benoemde groep | Benoemde groepsmachtigingen |
|---------|---------|---------|---------|---------|---------|---------|---------|
|/ | rwxr-x--x  |Beheerder |Beheerder  |Service-principal |--x  |FINGRP   |r-x         |
|/clusters | rwxr-x--x |Beheerder |Beheerder |Service-principal |--x  |FINGRP |r-x         |
|clusters/Financiën | rwxr-x--t |Beheerder |FINGRP  |Service-principal |rwx  |-  |-     |

In de tabel hello,

- **beheerder** Hallo Maker en de beheerder van Hallo Data Lake Store-account is.
- **Service-principal** hello Azure Active Directory (AAD) service-principal die is gekoppeld aan het Hallo-account is.
- **FINGRP** is een gebruikersgroep gemaakt in AAD die gebruikers van Hallo Financiën organisatie bevat.

Voor instructies over hoe toocreate een AAD-toepassing (die u maakt ook een Service-Principal), Zie [een AAD-toepassing maken](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application). Voor instructies over hoe toocreate een gebruikersgroep in AAD, Zie [groepen beheren in Azure Active Directory](../active-directory/active-directory-accessmanagement-manage-groups.md).

Sommige tooconsider belangrijke punten.

- Hallo twee niveau mapstructuur (**/clusters financiën/**) moet worden gemaakt en ingericht met de juiste machtigingen door Hallo Data Lake Store beheerder **voordat** Hallo storage-account gebruiken voor clusters. Deze structuur wordt niet automatisch gemaakt tijdens het maken van clusters.
- Hallo in bovenstaand voorbeeld raadt instelling Hallo die eigenaar is van de groep van **/clusters/financiën** als **FINGRP** en waardoor **r-x** toegang tot tooFINGRP toohello hele maphiërarchie vanaf Hallo-hoofdmap. Dit zorgt ervoor dat leden van FINGRP Hallo Hallo mapstructuur starten vanuit de hoofdmap kunnen navigeren.
- In geval van Hallo wanneer verschillende AAD-Service-Principals kunt clusters onder maken **clusters/financiën**, een tijdelijke Hallo-bits (wanneer ingesteld op Hallo **financiën** map) zorgt ervoor dat de mappen door een Service gemaakt Principal kan niet worden verwijderd door Hallo andere.
- Zodra het Hallo-mapstructuur en de machtigingen gemaakt zijn, aanmaakproces voor HDInsight-cluster maakt een loaction clusterspecifieke opslag onder **/clustersfinanciën/**. Hallo-opslag voor een cluster met Hallo naam fincluster01 kan bijvoorbeeld **/clusters/finance/fincluster01**. Hallo eigendom en machtigingen voor Hallo-mappen die zijn gemaakt door HDInsight-cluster worden weergegeven in hier Hallo-tabel.

    |Map  |Machtigingen  |Gebruiker die eigenaar is  |Groep die eigenaar is  | Benoemde gebruiker | Benoemde gebruikersmachtigingen | Benoemde groep | Benoemde groepsmachtigingen |
    |---------|---------|---------|---------|---------|---------|---------|---------|
    |/clusters/finanace/fincluster01 | rwxr-x---  |Service-Principal |FINGRP  |- |-  |-   |-  | 
   


## <a name="recommendations-for-job-input-and-output-data"></a>Aanbevelingen voor taak-en uitvoergegevens

We aanbevelen die gegevens tooa taak invoer en uitvoer van een taak Hallo worden opgeslagen in een map buiten **/clusters**. Dit zorgt ervoor dat zelfs als Hallo cluster-specifieke map Verwijderde tooreclaim bepaalde opslagruimte, Hallo taak invoer en uitvoer nog steeds beschikbaar voor toekomstig gebruik zijn. Zorg ervoor dat de mappenhiërarchie Hallo voor het opslaan van taak Hallo en uitgangen passend niveau van toegang voor Hallo Service-Principal toestaat in dat geval.

## <a name="limit-on-clusters-sharing-a-single-storage-account"></a>De limiet voor clusters delen van een enkele storage-account

Hallo-limiet voor Hallo van clusters die één Data Lake Store-account kunt delen, is afhankelijk van Hallo werkbelasting wordt uitgevoerd op deze clusters. Te veel clusters of zeer zware werklasten op Hallo-clusters die delen van een opslagaccount, kunnen er Hallo storage account inkomend en uitgaand tooget beperkt.

## <a name="support-for-default-acls"></a>Ondersteuning voor standaard-ACL 's

Wanneer een Service-Principal maken met de naam van de gebruiker toegang (zoals wordt weergegeven in bovenstaande Hallo tabel), raden we aan **niet** Hallo met de naam-gebruiker met een standaard-ACL toe te voegen. Inrichten met de naam van de gebruiker toegang met behulp van resultaten van de standaard-ACL's in Hallo toewijzing van 770 machtigingen voor die eigenaar is van de gebruiker die eigenaar is van de groep en de andere. Hoewel deze standaardwaarde van 770 worden machtigingen van die eigenaar is van gebruiker (7) of die eigenaar is van-groep (7), heeft de weg alle machtigingen voor andere (0). Dit resulteert in een bekend probleem met een bepaalde use case die wordt uitgebreid beschreven in Hallo [bekende problemen en tijdelijke oplossingen](#known-issues-and-workarounds) sectie.

## <a name="known-issues-and-workarounds"></a>Bekende problemen en oplossingen

Deze sectie vindt bekende problemen voor het gebruik van HDInsight met Data Lake Store en de tijdelijke oplossingen Hallo.

### <a name="publicly-visible-localized-yarn-resources"></a>Openbaar zichtbaar gelokaliseerde YARN-bronnen

Wanneer een nieuw Azure Data Lake store-account is gemaakt, wordt de hoofdmap Hallo automatisch ingericht met ACL Access machtiging bits set too770. Hallo hoofdmap die eigenaar is set toohello gebruiker die het Hallo-account (Hallo Data Lake Store admin) gemaakt en Hallo eigenaar groep primaire groeps-toohello van Hallo-gebruiker die het Hallo-account hebt gemaakt is ingesteld. Geen toegang is opgegeven voor 'anderen'.

Deze instellingen zijn bekende tooaffect één specifieke HDInsight use case vastgelegd in [YARN 247](https://hwxmonarch.atlassian.net/browse/YARN-247). Voorbeelden van de taak kunnen mislukken met een fout bericht vergelijkbaar toothis:

    Resource XXXX is not publicly accessible and as such cannot be part of hello public cache.

Zoals vermeld in de Hallo die YARN JIRA gekoppeld eerder tijdens het lokaliseren van openbare bronnen hello localizer valideert dat alle Hallo zijn door het controleren van hun machtigingen op Hallo externe bestandssysteem aangevraagde resources inderdaad openbaar. Alle LocalResource die voldoet niet aan die voorwaarde is voor lokalisatie geweigerd. Hallo controle voor machtigingen, leestoegang toohello bestand "anderen" bevat. Dit scenario werkt niet out-of-the-box, bij het hosten van HDInsight-clusters op Azure Data Lake omdat Azure Data Lake weigert u alle toegang te 'anderen' op hoofdniveau van de map.

#### <a name="workaround"></a>Tijdelijke oplossing
Set lees-schrijfrechten hebben voor **anderen** via Hallo-hiërarchie, bijvoorbeeld op  **/** , **/clusters** en   **/clusters/Financiën**  zoals weergegeven in de bovenstaande Hallo-tabel.

## <a name="see-also"></a>Zie ook

* [Een HDInsight-cluster maken met Data Lake Store als opslag](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)


