---
title: aaaEncryption in Azure Data Lake Store | Microsoft Docs
description: Informatie over de werking van versleuteling en sleutelroulatie in Azure Data Lake Store
services: data-lake-store
documentationcenter: 
author: yagupta
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 4/14/2017
ms.author: yagupta
ms.openlocfilehash: a9f3a2dce8232deba93005594d1e6a21e9c0cbee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="encryption-of-data-in-azure-data-lake-store"></a>Versleuteling van gegevens in Azure Data Lake Store

Versleuteling in Azure Data Lake Store helpt u uw gegevens te beveiligen, beveiligingsbeleid voor uw onderneming te implementeren en te voldoen aan wettelijke vereisten. Dit artikel biedt een overzicht van Hallo ontwerp en worden enkele van de technische aspecten van uitvoering Hallo beschreven.

Data Lake Store biedt ondersteuning voor versleuteling van gegevens in rust en doorvoer. Data Lake Store ondersteunt on-by-default, transparante versleuteling van data-at-rest. Hier wordt iets gedetailleerder uitgelegd wat deze termen betekenen:

* **Op standaard**: wanneer u een nieuw Data Lake Store-account maakt, schakelt u versleuteling Hallo standaardinstelling. Gegevens die zijn opgeslagen in Data Lake Store is daarna altijd versleutelde voorafgaande toostoring op permanente media. Dit is Hallo-gedrag voor alle gegevens en kan niet worden gewijzigd nadat een account is gemaakt.
* **Transparante**: Data Lake Store automatisch voorafgaande toopersisting gegevens versleutelt en ontsleutelt voorafgaande tooretrieval gegevens. Hallo-versleuteling is geconfigureerd en beheerd op Hallo Data Lake Store-niveau door een beheerder. Geen wijzigingen zijn aangebracht toohello gegevens toegang tot API's. Er zijn dus geen wijzigingen vereist in toepassingen en services die interactie hebben met Data Lake Store vanwege versleuteling.

Gegevens tijdens overdracht (ook wel gegevens in beweging genoemd) worden ook altijd versleuteld in Data Lake Store. Bovendien tooencrypting gegevens voorafgaande toostoring toopersistent media Hallo gegevens is ook altijd onderweg via HTTPS beveiligd. HTTPS is alleen Hallo-protocol dat wordt ondersteund voor Hallo die Data Lake Store REST-interfaces. Hallo volgende diagram ziet u hoe de gegevens in Data Lake Store wordt versleuteld:

![Diagram van gegevensversleuteling in Data Lake Store](./media/data-lake-store-encryption/fig1.png)


## <a name="set-up-encryption-with-data-lake-store"></a>Versleuteling instellen met Data Lake Store

Versleuteling voor Data Lake Store wordt ingesteld tijdens het maken van het account en is standaard altijd ingeschakeld. U kunt Hallo sleutels zelf beheren, of toestaan van Data Lake Store toomanage ze voor u (dit is standaard Hallo).

Zie de [Introductie](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal) voor meer informatie.

## <a name="how-encryption-works-in-data-lake-store"></a>De werking van versleuteling in Data Lake Store

Hallo volgende informatie bevat informatie over hoe toomanage master versleutelingssleutels en wordt uitgelegd Hallo drie verschillende typen sleutels die u in gegevensversleuteling voor Data Lake Store gebruiken kunt.

### <a name="master-encryption-keys"></a>Hoofdversleutelingssleutels

Data Lake Store biedt twee modi voor het beheer van hoofdversleutelingssleutels (MEK's). Op dit moment wordt ervan uitgegaan dat Hallo master versleutelingssleutel is op het hoogste niveau Hallo-sleutel. Toegangssleutel toohello hoofdversleutelingssleutel is vereist toodecrypt alle gegevens die zijn opgeslagen in Data Lake Store.

Hallo twee modi voor het beheren van Hallo master versleutelingssleutel zijn als volgt:

*   Door service beheerde sleutels
*   Door klant beheerde sleutels

In beide modi, Hallo master versleutelingssleutel is beveiligd door op te slaan in Azure Sleutelkluis. Sleutelkluis is een maximaal beveiligde volledig beheerde service in Azure die gebruikt toosafeguard cryptografische sleutels worden kan. Zie voor meer informatie [Key Vault](https://azure.microsoft.com/services/key-vault).

Hier volgt een korte vergelijking van mogelijkheden van de twee modi Hallo Hallo MEKs beheren.

|  | Door service beheerde sleutels | Door klant beheerde sleutels |
| --- | --- | --- |
|Hoe worden gegevens opgeslagen?|Altijd versleutelde voorafgaande toobeing opgeslagen.|Altijd versleutelde voorafgaande toobeing opgeslagen.|
|Waar wordt Hallo Master versleutelingssleutel opgeslagen?|Key Vault|Key Vault|
|Worden alle sleutels die zijn opgeslagen in Hallo Schakel versleuteling buiten de Sleutelkluis? |Nee|Nee|
|Door Sleutelkluis hello MEK kan worden opgehaald|Nee. Na het Hallo die MEK wordt opgeslagen in de Sleutelkluis, kan alleen worden gebruikt voor versleuteling en ontsleuteling.|Nee. Na het Hallo die MEK wordt opgeslagen in de Sleutelkluis, kan alleen worden gebruikt voor versleuteling en ontsleuteling.|
|Wie is eigenaar van exemplaar van de Sleutelkluis hello en Hallo MEK?|Hallo Data Lake Store-service|Eigenaar van Hallo Sleutelkluis instantie die in uw eigen Azure-abonnement behoort. Hallo MEK in Sleutelkluis kan worden beheerd door software of hardware.|
|Kunt u access toohello MEK voor Hallo Data Lake Store-service intrekken?|Nee|Ja. U kunt toegangsbeheerlijsten in Sleutelkluis beheren en verwijderen van de access control vermeldingen toohello service-identiteit voor Hallo Data Lake Store-service.|
|Kunt u Hallo MEK permanent verwijderen?|Nee|Ja. Als u Hallo MEK uit Sleutelkluis verwijdert, kan Hallo-gegevens in Data Lake Store-account Hallo kunnen niet worden ontsleuteld door iedereen, inclusief Hallo Data Lake Store-service. <br><br> Als u hebt expliciet back-up Hallo MEK voorafgaande toodeleting deze van Sleutelkluis, Hallo MEK kan worden hersteld en Hallo gegevens vervolgens kunnen worden hersteld. Echter, als u hebt geen back-up Hallo MEK voorafgaande toodeleting deze van Sleutelkluis, Hallo-gegevens in Data Lake Store-account Hallo kan nooit worden ontsleuteld daarna.|


Naast dit verschil van die Hallo MEK beheert en Hallo Sleutelkluis-exemplaar waarin de machine zich bevindt, rest Hallo van Hallo ontwerp is dezelfde Hallo voor beide modi.

Als u Hallo-modus voor Hallo master versleutelingssleutels kiest is belangrijk tooremember Hallo volgende:

*   U kunt kiezen of toouse klant sleutels of sleutels van de service die wordt beheerd beheerd wanneer u een Data Lake Store-account inrichten.
*   Nadat een Data Lake Store-account is ingericht, kan niet Hallo-modus worden gewijzigd.

### <a name="encryption-and-decryption-of-data"></a>Versleuteling en ontsleuteling van gegevens

Er zijn drie typen sleutels die worden gebruikt in Hallo ontwerp van de versleuteling van gegevens. Hallo volgende tabel bevat een samenvatting:

| Sleutel                   | Afkorting | Gekoppeld aan | Opslaglocatie                             | Type       | Opmerkingen                                                                                                   |
|-----------------------|--------------|-----------------|----------------------------------------------|------------|---------------------------------------------------------------------------------------------------------|
| Hoofdversleutelingssleutel | MEK          | Een Data Lake Store-account | Key Vault                              | Asymmetrisch | Deze kan worden beheerd door Data Lake Store of door u.                                                              |
| Gegevensversleutelingssleutel   | DEK          | Een Data Lake Store-account | Permanente opslag, beheerd door Data Lake Store-service | Symmetrisch  | Hallo MEK Hallo DEK wordt versleuteld. Hallo die versleutelde DEK is wat wordt opgeslagen op permanente media. |
| Blokversleutelingssleutel  | BEK          | Een gegevensblok | Geen                                         | Symmetrisch  | Hallo BEK is afgeleid van Hallo DEK en Hallo gegevensblok.                                                      |

Hallo volgende diagram ziet u deze begrippen:

![Sleutels bij gegevensversleuteling](./media/data-lake-store-encryption/fig2.png)

#### <a name="pseudo-algorithm-when-a-file-is-toobe-decrypted"></a>Pseudo-algoritme wanneer een bestand ontsleuteld toobe is:
1.  Controleer of Hallo DEK voor Hallo Data Lake Store-account in de cache en gereed voor gebruik is.
    - Als dat niet het geval is, lees Hallo DEK uit de permanente opslag versleuteld en tooKey kluis toobe ontsleuteld om dit te verzenden. Cache Hallo ontsleuteld DEK in het geheugen. Het is nu gereed toouse.
2.  Voor elk blok van gegevens in Hallo-bestand:
    - Hallo versleutelde gegevensblok lezen uit de permanente opslag.
    - Hallo BEK van Hallo DEK en Hallo versleutelde gegevensblok genereren.
    - Hallo BEK toodecrypt gegevens worden gebruikt.


#### <a name="pseudo-algorithm-when-a-block-of-data-is-toobe-encrypted"></a>Pseudo-algoritme wanneer een blok gegevens versleuteld toobe:
1.  Controleer of Hallo DEK voor Hallo Data Lake Store-account in de cache en gereed voor gebruik is.
    - Als dat niet het geval is, lees Hallo DEK uit de permanente opslag versleuteld en tooKey kluis toobe ontsleuteld om dit te verzenden. Cache Hallo ontsleuteld DEK in het geheugen. Het is nu gereed toouse.
2.  Een unieke BEK voor Hallo blok van gegevens van Hallo DEK worden gegenereerd.
3.  Hallo gegevensblok Hello BEK, versleutelen met behulp van AES-256-versleuteling.
4.  Hallo versleutelde gegevensblok van gegevens opslaan op permanente opslag.

> [!NOTE] 
> Voor betere prestaties Hallo DEK in Hallo wissen in de cache is opgeslagen in het geheugen voor een korte periode en daarna onmiddellijk worden gewist. Voor permanente media, wordt altijd opgeslagen door Hallo MEK gecodeerd.

## <a name="key-rotation"></a>Sleutelroulatie

Wanneer u van sleutels door de klant beheerd gebruikmaakt, kunt u Hallo MEK draaien. hoe tooset van een Data Lake Store-account met de klant beheerd sleutels zien toolearn [aan de slag](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal).

### <a name="prerequisites"></a>Vereisten

Wanneer u Hallo Data Lake Store-account hebt ingesteld, hebt u uw eigen sleutels toouse gekozen. Deze optie kan niet worden gewijzigd nadat het Hallo-account is gemaakt. Hallo volgende stappen wordt ervan uitgegaan dat u van sleutels door de klant beheerd gebruikmaakt (dat wil zeggen, u hebt ervoor gekozen uw eigen sleutels van Sleutelkluis).

Houd er rekening mee dat als u de standaardopties Hallo voor versleuteling gebruikt, uw gegevens wordt altijd versleuteld met sleutels die worden beheerd door de Data Lake Store. In deze optie kunt hebt u geen Hallo mogelijkheid toorotate sleutels, zoals ze worden beheerd door de Data Lake Store.

### <a name="how-toorotate-hello-mek-in-data-lake-store"></a>Hoe toorotate Hallo MEK in Data Lake Store

1. Meld u aan toohello [Azure-portal](https://portal.azure.com/).
2. Blader toohello Sleutelkluis-exemplaar dat uw sleutels die zijn gekoppeld aan uw Data Lake Store-account worden opgeslagen. Selecteer **Sleutels**.

    ![Schermafdruk van Key Vault](./media/data-lake-store-encryption/keyvault.png)

3.  Hallo-sleutel die is gekoppeld aan uw Data Lake Store-account selecteren en maak een nieuwe versie van deze sleutel. Houd er rekening mee dat Data Lake Store momenteel alleen belangrijke rotatie tooa nieuwe versie van een sleutel ondersteunt. Deze biedt geen ondersteuning voor draaiende tooa andere sleutel.

   ![Schermafdruk van het venster Sleutels met de nieuwe versie gemarkeerd](./media/data-lake-store-encryption/keynewversion.png)

4.  Blader toohello Data Lake Store-opslagaccount en selecteer **versleuteling**.

    ![Schermafdruk van Data Lake Store-opslagaccountvenster met versleuteling gemarkeerd](./media/data-lake-store-encryption/select-encryption.png)

5.  Een bericht wordt aangegeven dat een nieuwe sleutel versie van Hallo sleutel beschikbaar is. Klik op **draaien sleutel** tooupdate Hallo sleutel toohello nieuwe versie.

    ![Schermafdruk van Data Lake Store-venster met het bericht en Sleutel rouleren gemarkeerd](./media/data-lake-store-encryption/rotatekey.png)

Deze bewerking moet minder dan twee minuten duren en er is geen verwachte uitvaltijd vanwege tookey worden gedraaid. Nadat het Hallo-bewerking is voltooid, is de nieuwe versie van de Hallo van Hallo-sleutel gebruikt.
