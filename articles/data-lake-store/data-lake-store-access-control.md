---
title: aaaOverview van toegangsbeheer in Data Lake Store | Microsoft Docs
description: Begrijpen hoe toegangsbeheer werkt in Azure Data Lake Store
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d16f8c09-c954-40d3-afab-c86ffa8c353d
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 1cc5d578f22ef0a123a1547abebfb4795ea09139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="access-control-in-azure-data-lake-store"></a>Toegangsbeheer in Azure Data Lake Store

Azure Data Lake Store implementeert een model voor toegangsbeheer die is afgeleid van HDFS die op zijn beurt is afgeleid van Hallo POSIX model voor toegangsbeheer. In dit artikel bevat een overzicht van Hallo basisprincipes van Hallo model voor toegangsbeheer voor Data Lake Store. toolearn meer informatie over Hallo HDFS model voor toegangsbeheer, Zie [HDFS machtigingen handleiding](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).

## <a name="access-control-lists-on-files-and-folders"></a>Toegangsbeheerlijsten voor bestanden en mappen

Er zijn twee soorten toegangsbeheerlijsten (ACL's): **Toegangs-ACL's** en **Standaard-ACL's**.

* **Toegang tot de ACL's**: deze control toegang tooan-object. Bestanden en mappen hebben Toegangs-ACL's.

* **ACL's standaard**: een 'sjabloon' van ACL's die zijn gekoppeld aan een map die bepalen Hallo toegang ACL's voor alle onderliggende items die in die map worden gemaakt. Bestanden hebben geen Standaard-ACL's.

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-acls-1.png)

Zowel toegang ACL's en standaard ACL's hebben Hallo dezelfde structuur.

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-acls-2.png)



> [!NOTE]
> Veranderende Hallo ACL standaard op een bovenliggende heeft geen invloed op Hallo ACL Access of standaard ACL van onderliggende items die al bestaan.
>
>

## <a name="users-and-identities"></a>Gebruikers en identiteiten

Alle bestanden en mappen beschikken over verschillende machtigingen voor de volgende identiteiten:

* Hallo die eigenaar is van de gebruiker van Hallo-bestand
* Hallo eigenaar groep
* Benoemde gebruikers
* Benoemde groepen
* Alle andere gebruikers

Hallo-identiteit van gebruikers en groepen zijn identiteiten met Azure Active Directory (Azure AD). Dus tenzij anders vermeld, ', ' in de context van Data Lake Store Hallo kan de gebruiker: een Azure AD-gebruiker of een Azure AD-beveiligingsgroep.

## <a name="permissions"></a>Machtigingen

Hallo-machtigingen voor een bestandssysteemobject zijn **lezen**, **schrijven**, en **Execute**, en ze kunnen worden gebruikt voor bestanden en mappen zoals weergegeven in de volgende tabel Hallo:

|            |    File     |   Map |
|------------|-------------|----------|
| **Lezen (L)** | Hallo-inhoud van een bestand kan worden gelezen | Vereist **lezen** en **Execute** toolist Hallo inhoud van Hallo-map|
| **Schrijven (S)** | Kan schrijven of tooa toevoegen | Vereist **schrijven** en **Execute** toocreate onderliggende items in een map |
| **Uitvoeren (U)** | Betekent niet dat iets in de context Hallo van Data Lake Store | Vereiste tootraverse Hallo onderliggende items van een map |

### <a name="short-forms-for-permissions"></a>Korte formulieren voor machtigingen

**RWX** gebruikte tooindicate is **lezen + schrijven + uitvoeren**. Er bestaat een meer compacte numerieke vorm waarin **lezen = 4**, **schrijven = 2**, en **Execute = 1**, Hallo som waarvan vertegenwoordigt Hallo machtigingen. Hier volgen enkele voorbeelden.

| Numerieke vorm | Verkorte vorm |      Wat het betekent     |
|--------------|------------|------------------------|
| 7            | LSU        | Lezen + Schrijven + Uitvoeren |
| 5            | L-U        | Lezen + Uitvoeren         |
| 4            | L--        | Lezen                   |
| 0            | ---        | Geen machtigingen         |


### <a name="permissions-do-not-inherit"></a>Machtigingen worden niet overgenomen

Hallo POSIX-stijl-model dat wordt gebruikt door de Data Lake Store, zijn machtigingen voor een item opgeslagen in Hallo item zelf. Met andere woorden, kunnen niet de machtigingen voor een item worden overgenomen van Hallo bovenliggende items.

## <a name="common-scenarios-related-toopermissions"></a>Algemene scenario's gerelateerde toopermissions

Hieronder volgen enkele algemene scenario's toohelp u weten welke machtigingen zijn vereist tooperform bepaalde bewerkingen op een Data Lake Store-account.

### <a name="permissions-needed-tooread-a-file"></a>Machtigingen nodig tooread een bestand

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-acls-3.png)

* Hallo aanroeper behoeften voor Hallo bestand toobe lezen, **lezen** machtigingen.
* Voor alle mappen in de mapstructuur Hallo die Hallo-bestand bevatten hello, Hallo aanroeper behoeften **Execute** machtigingen.

### <a name="permissions-needed-tooappend-tooa-file"></a>Machtigingen nodig tooappend tooa bestand

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-acls-4.png)

* Voor Hallo bestand toobe toegevoegd aan, Hallo aanroeper behoeften **schrijven** machtigingen.
* Voor alle mappen met Hallo bestand hello, Hallo aanroeper behoeften **Execute** machtigingen.

### <a name="permissions-needed-toodelete-a-file"></a>Machtigingen nodig toodelete een bestand

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-acls-5.png)

* Voor de bovenliggende map Hallo Hallo aanroeper behoeften **schrijven + uitvoeren** machtigingen.
* Voor alle andere mappen in Hallo bestandspad hello, Hallo aanroeper behoeften **Execute** machtigingen.



> [!NOTE]
> Schrijven machtigingen op Hallo-bestand zijn niet vereist toodelete deze zolang Hallo van de vorige twee voorwaarden wordt voldaan.
>
>

### <a name="permissions-needed-tooenumerate-a-folder"></a>Machtigingen nodig tooenumerate een map

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-acls-6.png)

* Hallo aanroeper behoeften voor Hallo map tooenumerate, **lezen + Execute** machtigingen.
* Voor alle bovenliggende mappen hello, Hallo aanroeper behoeften **Execute** machtigingen.

## <a name="viewing-permissions-in-hello-azure-portal"></a>Machtigingen weergeven in hello Azure-portal

Van Hallo **Data Explorer** blade Hallo Data Lake Store-account, klikt u op **toegang** toosee Hallo ACL's voor een bestand of map. Klik op **toegang** toosee Hallo ACL's voor Hallo **catalogus** map onder Hallo **mydatastore** account.

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-show-acls-1.png)

Op deze blade geeft de bovenste gedeelte Hallo een overzicht van Hallo machtigingen die u hebt. (In Hallo schermafbeelding is Hallo gebruiker Bob.) Hierna Hallo toegangsmachtigingen worden weergegeven. Daarna van Hallo **toegang** blade, klikt u op **eenvoudige weergave** toosee Hallo eenvoudiger weergave.

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-show-acls-simple-view.png)

Klik op **geavanceerde weergave** toosee Hallo meer geavanceerde weergave, waarbij Hallo concepten van standaard ACL's, masker en supergebruiker worden weergegeven.

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-show-acls-advance-view.png)

## <a name="hello-super-user"></a>Hallo supergebruiker

Een supergebruiker heeft Hallo meeste rechten van gebruikers met alle Hallo in Hallo Data Lake Store. Een supergebruiker:

* RWX machtigingen te heeft**alle** bestanden en mappen.
* Kunt Hallo-machtigingen op een bestand of map wijzigen.
* Kunt Hallo eigendom van gebruiker of groep van een bestand of map eigenaar wijzigen.

In Azure heeft een Data Lake Store-account meerdere Azure-rollen, waaronder:

* Eigenaren
* Inzenders
* Lezers

Iedereen in Hallo **eigenaars** rol voor een Data Lake Store-account wordt automatisch een supergebruiker voor dat account. toolearn meer, Zie [toegangsbeheer op basis van rollen](../active-directory/role-based-access-control-configure.md).
Als u wilt dat toocreate een aangepaste rol-gebaseerd-toegangsbeheer (RBAC)-functie die supergebruiker machtigingen heeft, moet deze toohave Hallo volgende machtigingen:
- Microsoft.DataLakeStore/accounts/Superuser/action
- Microsoft.Authorization/roleAssignments/write


## <a name="hello-owning-user"></a>Hallo eigenaar gebruiker

Hallo-gebruiker die Hallo-item gemaakt is automatisch Hallo eigendom van gebruiker Hallo-item. Een gebruiker die eigenaar is kan:

* Hallo-machtigingen van een bestand dat eigendom is gewijzigd.
* Hallo die eigenaar is van de groep van een bestand dat eigendom is zolang Hallo eigenaar gebruiker deel uitmaakt van de doelgroep Hallo wijzigen.

> [!NOTE]
> Hallo eigendom van gebruiker *kan niet* Hallo die eigenaar is van de gebruiker van een ander in eigendom van bestand wijzigen. Alleen absoluut gebruikers kunnen Hallo die eigenaar is van de gebruiker van een bestand of map wijzigen.
>
>

## <a name="hello-owning-group"></a>Hallo eigenaar groep

Hallo POSIX-ACL's, elke gebruiker is gekoppeld aan een "primaire groep'. Gebruiker 'Els' kan bijvoorbeeld toohello 'Financiën' groep behoren. Els mogelijk ook toomultiple groepen behoren, maar één groep altijd is aangewezen als haar primaire groep. In het POSIX, wanneer een bestand, Alice maakt is Hallo die eigenaar is van de groep van het bestand ingesteld tooher primaire groep, die in dit geval 'Financiën'.

Wanneer een nieuw bestandssysteem item is gemaakt, toegewezen Data Lake Store een waarde toohello die eigenaar is van groep.

* **Voorbeeld 1**: hoofdmap Hallo '/'. Deze map wordt gemaakt wanneer een Data Lake Store-account wordt gemaakt. Hallo eigenaar groep ingesteld in dit geval toohello gebruiker Hallo-account hebt gemaakt.
* **Voorbeeld 2** (alle andere gevallen): wanneer een nieuw item is gemaakt, Hallo eigenaar groep wordt gekopieerd van Hallo bovenliggende map.

Hallo eigenaar groep kan worden gewijzigd door:
* Alle supergebruikers.
* Hallo eigendom van gebruiker, als Hallo eigenaar gebruiker deel uitmaakt van de doelgroep Hallo.

## <a name="access-check-algorithm"></a>Algoritme voor toegangscontrole

Hallo volgende illustratie vertegenwoordigt Hallo toegang selectievakje algoritme voor het Data Lake Store-accounts.

![Algoritme voor Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-acls-algorithm.png)


## <a name="hello-mask-and-effective-permissions"></a>Hallo masker en "effectieve machtigingen"

Hallo **masker** is een RWX waarde die is gebruikt toolimit toegang voor **benoemde gebruikers**, Hallo **die eigenaar is van groep**, en **benoemde groepen** wanneer u klaar Hallo toegang selectievakje algoritme uitvoeren. Hier vindt u belangrijke concepten voor Hallo masker Hallo.

* Hallo masker maakt "effectieve machtigingen." Dat wil zeggen, wijzigt de machtigingen Hallo Hallo gelijktijdig met toegangscontrole.
* Hallo masker kan rechtstreeks worden bewerkt met Hallo bestandseigenaar en eventuele absoluut gebruikers.
* Hallo masker kunt machtigingen toocreate Hallo effectieve machtiging te verwijderen. Hallo masker *kan niet* machtigingen toohello effectieve machtiging toevoegen.

We bekijken enkele voorbeelden. In Hallo voorbeeld te volgen, Hallo masker te ingesteld**RWX**, wat betekent dat masker Hallo machtigingen niet verwijderen. Hallo effectieve machtigingen van Hallo benoemde gebruiker, groep eigenaar en de naam van de groep niet worden gewijzigd tijdens het Hallo-toegangscontrole.

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-acls-mask-1.png)

In Hallo voorbeeld te volgen, Hallo masker te ingesteld**R X**. Dit betekent dat deze **wordt uitgeschakeld Hallo schrijfmachtigingen** voor **benoemde gebruiker**, **die eigenaar is van groep**, en **groep** gelijktijdig Hallo met toegang Controleer.

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-acls-mask-2.png)

Ter referentie: dit is waar Hallo masker aan voor een bestand of map wordt weergegeven in hello Azure-portal.

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-show-acls-mask-view.png)

> [!NOTE]
> Voor een nieuwe Data Lake Store-account, Hallo masker voor Hallo ACL Access en standaard ACL van hoofd-Hallo standaard map ('/') tooRWX.
>
>

## <a name="permissions-on-new-files-and-folders"></a>Machtigingen voor nieuwe bestanden en mappen

Wanneer een nieuw bestand of map wordt gemaakt onder een bestaande map, bepaalt Hallo standaard ACL op Hallo bovenliggende map:

- De Standaard-ACL en Toegangs-ACL voor een onderliggende map.
- De Toegangs-ACL van een onderliggend bestand (bestanden beschikken niet over een Standaard-ACL).

### <a name="hello-access-acl-of-a-child-file-or-folder"></a>Hallo ACL Access van een onderliggend bestand of map

Wanneer een onderliggend bestand of map wordt gemaakt, wordt als Hallo ACL Access van Hallo onderliggende bestand of map van het bovenliggende Hallo standaard ACL gekopieerd. Ook als **andere** gebruiker RWX machtigingen in van het bovenliggende Hallo standaard ACL heeft, wordt deze verwijderd uit de ACL Access Hallo onderliggend item.

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-acls-child-items-1.png)

In de meeste gevallen is Hallo voorgaande informatie moet alle u tooknow over hoe een onderliggend item toegang ACL wordt bepaald. Echter, als u bekend met POSIX-systemen en gewenste toounderstand diepgaande hoe deze transformatie wordt voldaan bent, raadpleegt u Hallo sectie [Umask van rol bij het maken van Hallo toegang ACL voor nieuwe bestanden en mappen](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) verderop in dit artikel.


### <a name="a-child-folders-default-acl"></a>De Standaard-ACL voor een onderliggende map

Als een onderliggende map onder de bovenliggende map wordt gemaakt, wordt Hallo bovenliggende map standaard ACL wordt gekopieerd via omdat toohello onderliggende map standaard ACL.

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-acls-child-items-2.png)

## <a name="advanced-topics-for-understanding-acls-in-data-lake-store"></a>Geavanceerde onderwerpen om ACL's in de Data Lake Store te begrijpen

Hier volgen enkele geavanceerde onderwerpen toohelp dat u begrijpt hoe de ACL's voor Data Lake Store-bestanden of mappen zijn bepaald.

### <a name="umasks-role-in-creating-hello-access-acl-for-new-files-and-folders"></a>Rol van Umask Hallo toegang ACL voor nieuwe bestanden en mappen maken

In een POSIX-compatibele systeem Hallo algemeen concept is dat umask is een 9-bits waarde op Hallo bovenliggende map die is gebruikt tootransform Hallo machtiging voor **eigendom van gebruiker**, **die eigenaar is van groep**, en  **andere** op Hallo ACL Access van een nieuw onderliggend bestand of map. Hallo bits van een umask identificeren welke tooturn bits uitschakelen in de ACL Access Hallo onderliggend item. Dus Hiermee tooselectively te voorkomen dat Hallo doorgifte van machtigingen voor **eigendom van gebruiker**, **die eigenaar is van groep**, en **andere**.

Hallo umask is in een HDFS-systeem, meestal een configuratieoptie op de hele site, die wordt beheerd door beheerders. Data Lake Store gebruikt een **umask voor het hele account** die niet kan worden gewijzigd. Hallo volgende tabel toont Hallo maskeren voor Data Lake Store.

| Gebruikersgroep  | Instelling | Invloed op de Toegangs-ACL van het nieuwe onderliggende item |
|------------ |---------|---------------------------------------|
| Gebruiker die eigenaar is | ---     | Geen effect                             |
| Groep die eigenaar is| ---     | Geen effect                             |
| Overige       | LSU     | Lezen + Schrijven + Uitvoeren verwijderen         |

Hallo volgende afbeelding ziet deze umask in actie. Hallo netto effect is tooremove **lezen + schrijven + uitvoeren** voor **andere** gebruiker. Omdat Hallo umask is niet opgegeven voor bits voor **eigendom van gebruiker** en **die eigenaar is van groep**, deze machtigingen niet worden getransformeerd.

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-acls-umask.png)

### <a name="hello-sticky-bit"></a>een tijdelijke Hallo-bits

een tijdelijke Hallo-bit is een geavanceerde functie van een POSIX-bestandssysteem. In de context van de Hallo van Data Lake Store is het onwaarschijnlijk dat een tijdelijke bits Hallo nodig.

Hallo volgende tabel ziet u de werking van een tijdelijke bits Hallo in Data Lake Store.

| Gebruikersgroep         | File    | Map |
|--------------------|---------|-------------------------|
| Vergrendelde bit **UIT** | Geen effect   | Geen effect.           |
| Vergrendelde bit **AAN**  | Geen effect   | Voorkomen dat iemand behalve **absoluut gebruikers** en Hallo **eigendom van gebruiker** van een onderliggend item van het verwijderen of hernoemen van onderliggende item.               |

een tijdelijke bits Hallo wordt niet weergegeven in hello Azure-portal.

## <a name="common-questions-about-acls-in-data-lake-store"></a>Veelgestelde vragen over ACL's in Data Lake Store

Hier volgen enkele vragen die vaak worden gesteld over ACL's in Data Lake Store.

### <a name="do-i-have-tooenable-support-for-acls"></a>Heb ik tooenable ondersteuning voor de ACL's?

Nee. Toegangsbeheer via de ACL's is altijd ingeschakeld voor een Data Lake Store-account.

### <a name="which-permissions-are-required-toorecursively-delete-a-folder-and-its-contents"></a>Welke machtigingen zijn vereist toorecursively het verwijderen van een map en de inhoud ervan?

* Hallo bovenliggende map moet hebben **schrijven + uitvoeren** machtigingen.
* Hallo map toobe verwijderd en vereist dat elke map erin **lezen + schrijven + uitvoeren** machtigingen.

> [!NOTE]
> U hoeft geen schrijfmachtigingen toodelete bestanden in mappen. Bovendien hoofdmap Hallo ' / ' kunnen **nooit** worden verwijderd.
>
>

### <a name="who-is-hello-owner-of-a-file-or-folder"></a>Wie is eigenaar van een bestand of map Hallo?

Hallo maker van een bestand of map wordt Hallo eigenaar.

### <a name="which-group-is-set-as-hello-owning-group-of-a-file-or-folder-at-creation"></a>Welke groep is ingesteld als Hallo die eigenaar is van een bestand of map bij het maken van groep?

Hallo eigenaar groep wordt gekopieerd van Hallo die eigenaar is van de groep van Hallo bovenliggende map onder welke Hallo nieuw bestand of map wordt gemaakt.

### <a name="i-am-hello-owning-user-of-a-file-but-i-dont-have-hello-rwx-permissions-i-need-what-do-i-do"></a>Ik ben Hallo die eigenaar is van de gebruiker van een bestand, maar ik heb Hallo RWX machtigingen die ik nodig. Wat moet ik doen?

Hallo eigenaar gebruiker kunt Hallo machtigingen wijzigen van Hallo bestand toogive zelf alle RWX machtigingen die ze nodig hebben.

### <a name="when-i-look-at-acls-in-hello-azure-portal-i-see-user-names-but-through-apis-i-see-guids-why-is-that"></a>Wanneer ik Kijk ACL's in Azure-portal Hallo Zie ik gebruikersnamen, maar via API's, Zie GUID's, waarom is dat?

Vermeldingen in het Hallo-ACL's worden opgeslagen als GUID's die overeenkomen met toousers in Azure AD. Hallo API's retourneren Hallo GUID's is. Hello Azure-portal probeert toomake ACL's eenvoudiger toouse door vertalen Hallo GUID's naar beschrijvende namen indien mogelijk.

### <a name="why-do-i-sometimes-see-guids-in-hello-acls-when-im-using-hello-azure-portal"></a>Waarom kan ik soms zien GUID's in Hallo ACL's bij gebruik van hello Azure-portal?

Een GUID wordt weergegeven wanneer het Hallo-gebruiker in Azure AD meer bestaat niet. Dit gebeurt meestal wanneer de gebruiker Hallo Hallo bedrijf heeft verlaten of als hun account in Azure AD is verwijderd.

### <a name="does-data-lake-store-support-inheritance-of-acls"></a>Biedt Data Lake Store ondersteuning voor overname van ACL's?

Nee.

### <a name="what-is-hello-difference-between-mask-and-umask"></a>Wat is Hallo verschil tussen het masker en umask?

| masker | umask|
|------|------|
| Hallo **masker** -eigenschap is beschikbaar op alle bestanden en mappen. | Hallo **umask** is een eigenschap van Hallo Data Lake Store-account. Er is daarom alleen een enkele umask in Hallo Data Lake Store.    |
| Hallo masker eigenschap op een bestand of map kan worden gewijzigd door Hallo eigendom van gebruiker of groep van een bestand of een absoluut gebruiker die eigenaar is. | Hallo umask eigenschap kan niet worden gewijzigd door een gebruiker, zelfs supergebruiker. Het is een onveranderbare, constante waarde.|
| de eigenschap mask Hello wordt gebruikt tijdens Hallo toegang selectievakje algoritme op runtime toodetermine of de gebruiker de juiste tooperform Hallo op de bewerking op een bestand of map is. Hallo-rol van Hallo masker is toocreate 'effectieve machtigingen' Hallo gelijktijdig met toegangscontrole. | Hallo umask wordt niet gebruikt tijdens toegangscontrole helemaal. Hallo umask is gebruikte toodetermine Hallo toegang ACL van nieuwe onderliggende items van een map. |
| Hallo-masker is een 3-bits RWX-waarde die toonamed gebruiker, benoemde groep en gebruiker die eigenaar is van toepassing op Hallo moment toegangscontrole.| Hallo umask is een 9-bits waarde die van toepassing eigendom van gebruiker is, groep eigenaar toohello en **andere** van een nieuw onderliggend.|

### <a name="where-can-i-learn-more-about-posix-access-control-model"></a>Waar kan ik meer informatie over het POSIX-model voor toegangsbeheer?

* [POSIX met behulp van toegangsbeheerlijsten op Linux](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html)

* [Handleiding voor HDFS-machtigingen](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)

* [Veelgestelde vragen over POSIX](http://www.opengroup.org/austin/papers/posix_faq.html)

* [POSIX 1003.1 2008](http://standards.ieee.org/findstds/standard/1003.1-2008.html)

* [POSIX 1003.1 2013](http://pubs.opengroup.org/onlinepubs/9699919799.2013edition/)

* [POSIX 1003.1 2016](http://pubs.opengroup.org/onlinepubs/9699919799.2016edition/)

* [POSIX ACL in Ubuntu](https://help.ubuntu.com/community/FilePermissionsACLs)

* [ACL met behulp van toegangsbeheerlijsten op Linux](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/)

## <a name="see-also"></a>Zie ook

* [Overzicht van Azure Data Lake Store](data-lake-store-overview.md)
