---
title: "aaaData Factory-Wizard voor het kopiëren van Azure | Microsoft Docs"
description: "Meer informatie over hoe toouse Data Factory-Wizard voor kopiëren van Azure toocopy gegevens van ondersteunde gegevensbronnen toosinks Hallo."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 0974eb40-db98-4149-a50d-48db46817076
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: 188b3ae15f937b84a58aec1b979347ac8090abf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory-copy-wizard"></a>Azure Data Factory-Wizard kopiëren
Hello Azure Data Factory-Wizard voor kopiëren kan Hallo-proces voor het opnemen van gegevens, die meestal een eerste stap in een end-to-end gegevens integratiescenario is vergemakkelijken. Bij gebruik van hello Azure Data Factory-Wizard voor kopiëren, hoeft u niet toounderstand een JSON-definities voor de gekoppelde services, gegevenssets en pijplijnen. Hallo wizard maakt automatisch een pijplijn toocopy data Hallo geselecteerde gegevensbron toohello het geselecteerde doel. Bovendien Hallo Wizard kopiëren helpt u te toovalidate Hallo gegevens wordt ingenomen op Hallo moment van ontwerpen. Dit bespaart tijd, vooral wanneer u zijn ophalen van gegevens voor Hallo eerst uit Hallo-gegevensbron. toostart hello Wizard kopiëren, klikt u op Hallo **gegevens kopiëren** tegel op Hallo-startpagina van uw gegevensfactory.

![De wizard Kopiëren](./media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="designed-for-big-data"></a>Ontworpen voor big data
Deze wizard kunt u tooeasily verplaatsen gegevens uit een groot aantal bronnen toodestinations in minuten. Nadat u de wizard Hallo doorloopt, worden een pijplijn met een kopieeractiviteit automatisch voor u, naast de afhankelijke Data Factory-entiteiten (gekoppelde services en gegevenssets) gemaakt. Er zijn geen extra stappen zijn vereist toocreate Hallo pijplijn.   

![Selecteer gegevensbron](./media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> Zie voor stapsgewijze instructies toocreate een voorbeeld pijplijn toocopy gegevens uit een Azure-blobopslag tooan Azure SQL Database-tabel, Hallo [Wizard kopiëren zelfstudie](data-factory-copy-data-wizard-tutorial.md).
>
>

Hallo-wizard is ontworpen met big data in gedachten van Hallo start met ondersteuning voor diverse gegevens en objecttypen. U kunt Data Factory-pijplijnen verplaatsen honderden mappen, bestanden of tabellen schrijven. Hallo wizard ondersteunt voorbeeld van automatische gegevens, schema vastleggen en toewijzing en het filteren van gegevens.

## <a name="automatic-data-preview"></a>Voorbeeld van automatische gegevens
U kunt een deel van gegevens uit de geselecteerde gegevensbron Hallo in volgorde toovalidate Hallo voorbeeld of Hallo gegevens is wat u wilt toocopy. Bovendien als Hallo brongegevens zich in een tekstbestand, parseert Hallo Wizard kopiëren tekst hello toolearn Hallo rij en kolom scheidingstekens en het schema automatisch.

![Bestandsindelingsinstellingen](./media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a>Schema vastleggen en toewijzing
Hallo-schema van invoergegevens mogelijk niet overeen met het Hallo-schema van uitvoergegevens in sommige gevallen. In dit scenario moet u toomap kolommen uit Hallo bron schema toocolumns van Hallo doelschema.

> [!TIP]
> Wanneer ondersteuning voor het kopiëren van gegevens uit SQL Server of Azure SQL Database in Azure SQL Data Warehouse, als Hallo tabel niet in het doelarchief hello, Data Factory bestaat automatisch tabel maken met behulp van het schema van de gegevensbron. Klik hier als u meer wilt weten van [tooand gegevens verplaatsen van Azure SQL Data Warehouse met behulp van Azure Data Factory](./data-factory-azure-sql-data-warehouse-connector.md).
>

Een vervolgkeuzelijst tooselect een kolom uit Hallo schema toomap tooa bronkolom in doelschema hello gebruiken. Hallo Wizard kopiëren probeert toounderstand het patroon voor kolomtoewijzing. Toepassing hello hetzelfde patroon toohello rest van de kolommen hello, zodat u geen tooselect Hallo kolommen afzonderlijk hoeft toocomplete Hallo schematoewijzing. Als u liever, kunt u deze toewijzingen overschrijven door Hallo vervolgkeuzelijsten toomap Hallo kolommen één voor één. Hallo-patroon wordt nauwkeuriger als u meer kolommen toewijzen. Hallo Wizard kopiëren Hallo patroon voortdurend bijgewerkt en uiteindelijk bereikt Hallo rechts patroon voor Hallo toewijzingskolommen u tooachieve wenst.     

![Schematoewijzing](./media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a>Filteren van gegevens
U kunt filteren bron gegevens tooselect alleen Hallo gegevens die moeten worden gekopieerd toobe toohello sink-gegevensarchief. Hallo volume van Hallo gegevens toobe gekopieerde toohello sink gegevens opslaan en daarom verbetert de doorvoer van kopieerbewerking Hallo Hallo filteren worden beperkt. Dit biedt een flexibele manier toofilter gegevens in een relationele database met behulp van de SQL-querytaal Hallo of bestanden in een Azure blob-map met behulp van [Data Factory-functies en variabelen](data-factory-functions-variables.md).   

### <a name="filtering-of-data-in-a-database"></a>Filteren van gegevens in een database
Hallo volgende schermafbeelding ziet u een SQL-query Hallo `Text.Format` functie en `WindowStart` variabele.

![Expressies valideren](./media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a>Filteren van gegevens in een Azure blob-map
U kunt variabelen gebruiken in Hallo map pad toocopy gegevens vanuit een map die wordt bepaald tijdens runtime op basis van [systeemvariabelen](data-factory-functions-variables.md#data-factory-system-variables). Hallo ondersteund variabelen zijn: **{year}**, **{month}**, **{day}**, **{uur}**, **{minuut}**, en **{aangepaste}**. Bijvoorbeeld: inputfolder / {year} / {month} / {day}.

Stel dat u de mappen in de volgende indeling Hallo hebt ingevoerd:

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

Klik op Hallo **Bladeren** knop voor **bestand of map**, tooone van deze mappen bladeren (bijvoorbeeld: 2016 -> 03 -> 01-02 >), en klik op **Kies**. U ziet `2016/03/01/02` in het tekstvak Hallo. Vervang nu, **2016** met **{year}**, **03** met **{month}**, **01** met **{day}** , en **02** met **{uur}**, en druk op Hallo **tabblad** sleutel. Hier ziet u vervolgkeuzelijsten tooselect Hallo indeling voor deze vier variabelen:

![Met behulp van systeemvariabelen](./media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

Zoals u in de volgende schermafbeelding Hallo, u kunt ook een **aangepaste** variabele en eventuele [indeling tekenreeksen ondersteund](https://msdn.microsoft.com/library/8kb3ddd4.aspx). een map met die structuur, gebruik Hallo tooselect **Bladeren** eerst knop. Vervangt een waarde met **{aangepaste}**, en druk op Hallo **tabblad** key toosee Hallo in het tekstvak u Hallo indelingstekenreeks typt.     

![Met behulp van aangepaste variabele](./media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="scheduling-options"></a>Opties voor het plannen
U kunt de kopieerbewerking Hallo uitvoeren nadat de of volgens een schema (elk uur, dagelijks, enzovoort). Beide opties kunnen worden gebruikt voor Hallo breedte van de Hallo-connectors tussen omgevingen, met inbegrip van on-premises, cloud en lokale bureaublad kopie.

Een eenmalige kopieerbewerking kan slechts één keer verplaatsing van gegevens uit een bron tooa doel. Toepassing toodata van elke grootte en elke ondersteunde indeling. Hallo gepland kopiëren kunt u toocopy gegevens op een voorgeschreven terugkeerpatroon. Kunt u geavanceerde instellingen (zoals opnieuw proberen, time-out en waarschuwingen) tooconfigure Hallo gepland kopiëren.

![Eigenschappen plannen](./media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a>Volgende stappen
Zie voor een snel overzicht van het gebruik van Hallo Data Factory-Wizard kopiëren toocreate een pijplijn met de Kopieeractiviteit [zelfstudie: een pijplijn maken met de Wizard kopiëren Hallo](data-factory-copy-data-wizard-tutorial.md).
