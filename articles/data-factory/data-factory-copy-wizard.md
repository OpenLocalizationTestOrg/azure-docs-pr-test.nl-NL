---
title: "aaaCopy gegevens eenvoudig met de Wizard kopiëren - Azure | Microsoft Docs"
description: "Meer informatie over hoe toouse Data Factory-Wizard kopiëren toocopy gegevens van ondersteunde gegevensbronnen toosinks Hallo."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f904972f-cd33-48db-9755-2b3196ae4168
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 99437ec16facf3b94c8be18487ec89e9f13acc9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-or-move-data-easily-with-azure-data-factory-copy-wizard"></a>Gegevens eenvoudig met Azure Data Factory-Wizard voor kopiëren kopiëren of verplaatsen
Hello Azure Data Factory-Wizard voor kopiëren is tooease Hallo proces van het opnemen van gegevens, die meestal een eerste stap in een end-to-end gegevens integratiescenario is. Bij gebruik van hello Azure Data Factory-Wizard voor kopiëren, hoeft u niet toounderstand een JSON-definities voor de gekoppelde services, gegevenssets en pijplijnen. Echter nadat u alle Hallo stappen in Hallo wizard hebt voltooid, maakt Hallo wizard automatisch een pijplijn toocopy data Hallo geselecteerde gegevensbron toohello het geselecteerde doel. Bovendien Hallo Wizard kopiëren helpt u toovalidate Hallo gegevens wordt ingenomen op Hallo moment van ontwerpen, die wordt opgeslagen veel van de tijd, vooral wanneer u zijn ophalen van gegevens voor Hallo eerst uit Hallo-gegevensbron. toostart hello Wizard kopiëren, klikt u op Hallo **gegevens kopiëren** tegel op Hallo-startpagina van uw gegevensfactory.

![De wizard Kopiëren](./media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="an-intuitive-wizard-for-copying-data"></a>Een intuïtieve wizard voor het kopiëren van gegevens
Deze wizard kunt u tooeasily verplaatsen gegevens uit een groot aantal bronnen toodestinations in minuten. Na het doorlopen van de wizard Hallo wordt een pijplijn met een kopieeractiviteit automatisch gemaakt voor u samen met afhankelijke Data Factory-entiteiten (gekoppelde services en gegevenssets). Er zijn geen extra stappen zijn vereist toocreate Hallo pijplijn.   

![Selecteer gegevensbron](./media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> Zie [Wizard kopiëren zelfstudie](data-factory-copy-data-wizard-tutorial.md) artikel voor stapsgewijze instructies toocreate een voorbeeld pijplijn toocopy gegevens uit een Azure-blobopslag tooan Azure SQL Database-tabel. 
> 
> 

Hallo-wizard is ontworpen met big data in gedachten van Hallo starten. Het is eenvoudig en efficiënt tooauthor Data Factory-pijplijnen verplaatsen honderden mappen, bestanden of tabellen met Hallo gegevens kopiëren van de wizard. Hallo wizard ondersteunt de volgende drie functies Hallo: voorbeeld van automatische gegevens, schema vastleggen en toewijzing en het filteren van gegevens. 

## <a name="automatic-data-preview"></a>Voorbeeld van automatische gegevens
de wizard kopiëren Hallo kunt u tooreview deel van de gegevens Hallo van Hallo gegevensbron voor u geselecteerd toovalidate of hello gegevens is Hallo rechtermuisknop gegevens die u wilt toocopy. Bovendien als Hallo brongegevens zich in een tekstbestand, parseert de wizard kopiëren Hallo Hallo tekst bestand toolearn rij en kolom scheidingstekens en schema automatisch. 

![Bestandsindelingsinstellingen](./media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a>Schema vastleggen en toewijzing
Hallo-schema van invoergegevens mogelijk niet overeen met het Hallo-schema van uitvoergegevens in sommige gevallen. In dit scenario moet u toomap kolommen uit Hallo bron schema toocolumns van Hallo doelschema. 

de wizard kopiëren Hallo automatisch kolommen in Hallo bron schema toocolumns in Hallo doelschema toegewezen. U kunt Hallo toewijzingen overschrijven met behulp van de vervolgkeuzelijsten hello (of) opgeven of er een kolom toobe overgeslagen moet tijdens het Hallo-gegevens te kopiëren.   

![Schematoewijzing](./media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a>Filteren van gegevens
Hallo wizard kunt u toofilter bron gegevens tooselect alleen Hallo gegevens die moeten worden gekopieerd toobe toohello bestemming/sink-gegevensarchief. Hallo volume van Hallo gegevens toobe gekopieerde toohello sink gegevens opslaan en daarom verbetert de doorvoer van kopieerbewerking Hallo Hallo filteren worden beperkt. Het biedt een flexibele manier toofilter gegevens in een relationele database met behulp van SQL query language (of)-bestanden in de map van een Azure-blob met behulp van [Data Factory-functies en variabelen](data-factory-functions-variables.md).   

### <a name="filtering-of-data-in-a-database"></a>Filteren van gegevens in een database
In Hallo voorbeeld gebruikt de SQL-query Hallo Hallo `Text.Format` functie en `WindowStart` variabele. 

![Expressies valideren](./media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a>Filteren van gegevens in een Azure blob-map
U kunt variabelen gebruiken in Hallo map pad toocopy gegevens vanuit een map die wordt bepaald tijdens runtime op basis van [systeemvariabelen](data-factory-functions-variables.md#data-factory-system-variables). Hallo ondersteund variabelen zijn: **{year}**, **{month}**, **{day}**, **{uur}**, **{minuut}**, en **{aangepaste}**. Voorbeeld: inputfolder / {year} / {month} / {day}.

Stel dat u de mappen in de volgende indeling Hallo hebt ingevoerd:

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

Klik op Hallo **Bladeren** knop voor **bestand of map**, tooone van deze mappen bladeren (bijvoorbeeld: 2016 -> 03 -> 01-02 >), en klik op **Kies**. U ziet `2016/03/01/02` in het tekstvak Hallo. Vervang nu, **2016** met **{year}**, **03** met **{month}**, **01** met **{day}** , en **02** met **{uur}**, en druk op Tab. Hier ziet u vervolgkeuzelijsten tooselect Hallo indeling voor deze vier variabelen:

![Met behulp van systeemvariabelen](./media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

Zoals u in de volgende schermafbeelding Hallo, u kunt ook een **aangepaste** variabele en eventuele [indeling tekenreeksen ondersteund](https://msdn.microsoft.com/library/8kb3ddd4.aspx). een map met die structuur, gebruik Hallo tooselect **Bladeren** eerst knop. Vervangt een waarde met **{aangepaste}**, en druk op Tab toosee Hallo tekstvak u Hallo indelingstekenreeks typt.     

![Met behulp van aangepaste variabele](./media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="support-for-diverse-data-and-object-types"></a>Ondersteuning voor diverse gegevens en objecttypen
U kunt met behulp van de Wizard kopiëren Hallo efficiënt honderden mappen, bestanden of tabellen verplaatsen.

![Selecteer de tabellen uit welke gegevens toocopy](./media/data-factory-copy-wizard/select-tables-to-copy-data.png)

## <a name="scheduling-options"></a>Opties voor het plannen
U kunt de kopieerbewerking Hallo uitvoeren nadat de of volgens een schema (elk uur, dagelijks, enzovoort). Beide opties kunnen worden gebruikt voor de breedte van connectors Hallo Hallo over on-premises, cloud en lokale bureaublad kopie.

Een eenmalige kopieerbewerking kan slechts één keer verplaatsing van gegevens uit een bron tooa doel. Toepassing toodata van elke grootte en elke ondersteunde indeling. Hallo gepland kopiëren kunt u toocopy gegevens op een voorgeschreven terugkeerpatroon. Kunt u geavanceerde instellingen (zoals opnieuw proberen, time-out en waarschuwingen) tooconfigure Hallo gepland kopiëren.

![Eigenschappen plannen](./media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a>Volgende stappen
Zie voor een snel overzicht van het gebruik van Hallo Data Factory-Wizard kopiëren toocreate een pijplijn met de Kopieeractiviteit [zelfstudie: een pijplijn maken met de Wizard kopiëren Hallo](data-factory-copy-data-wizard-tutorial.md).

