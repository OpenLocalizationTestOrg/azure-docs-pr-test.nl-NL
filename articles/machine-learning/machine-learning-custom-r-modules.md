---
title: aaaAuthor aangepaste R-Modules in Azure Machine Learning | Microsoft Docs
description: Snel starten voor het schrijven van aangepaste R-modules in Azure Machine Learning.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6cbc628a-7e60-42ce-9f90-20aaea7ba630
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 03/24/2017
ms.author: bradsev;ankarlof
ms.openlocfilehash: 8007c2abe20a4ab990f38b6d09bc4e6834ad2082
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="author-custom-r-modules-in-azure-machine-learning"></a>Aangepaste R-modules maken in Azure Machine Learning
Dit onderwerp wordt beschreven hoe tooauthor en implementeren van een aangepaste R-module in Azure Machine Learning. Hierin wordt uitgelegd wat aangepaste R-modules zijn en welke bestanden zijn gebruikte toodefine ze. Dit wordt geïllustreerd hoe tooconstruct Hallo voor bestanden die een module te definiëren en hoe tooregister Hallo-module voor implementatie in een Machine Learning-werkruimte. Hallo zijn-elementen en kenmerken die worden gebruikt in Hallo definitie van de aangepaste module Hallo vervolgens uitvoeriger beschreven. Hoe toouse aanvullende functionaliteit, bestanden en meerdere uitgangen wordt ook beschreven. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a>Wat is een aangepaste R-module?
Een **aangepaste module** is een door de gebruiker gedefinieerde module die kan worden geüpload tooyour werkruimte en uitgevoerd als onderdeel van een Azure Machine Learning-experiment. Een **aangepaste R-module** is een aangepaste module die wordt uitgevoerd een R door de gebruiker gedefinieerde functie. **R** is een programmeertaal voor statistische computing en afbeeldingen die veel door statistici en gegevens verzameld gebruikt wordt voor het implementeren van de algoritmen. R is momenteel de enige Hallo-taal ondersteund in aangepaste modules, maar ondersteuning voor extra talen is gepland voor toekomstige releases.

Aangepaste modules hebben **eersteklas status** in Azure Machine Learning in Hallo zin dat ze net als elke andere module kunnen worden gebruikt. Ze kunnen worden uitgevoerd met andere modules, opgenomen in gepubliceerde experimenten of visualisaties. U hebben controle over Hallo algoritme geïmplementeerd door de module hello, Hallo invoer en uitvoer poorten toobe gebruikt, Hallo modellering parameters en andere verschillende runtime-bewerkingen. Een experiment met aangepaste modules kan ook worden gepubliceerd in Hallo Cortana Intelligence Gallery delen.

## <a name="files-in-a-custom-r-module"></a>Bestanden in een aangepaste R-module
Een aangepaste R-module is gedefinieerd door een ZIP-bestand met ten minste twee bestanden:

* Een **bronbestand** die beschikbaar is gemaakt door de module Hallo Hallo R-functie wordt geïmplementeerd
* Een **definitie XML-bestand** die beschrijft Hallo aangepaste module-interface

Aanvullende hulpbestanden kunnen ook worden opgenomen in Hallo ZIP-bestand dat wordt functionaliteit geboden die toegankelijk zijn vanuit Hallo aangepaste module. Deze optie wordt besproken in Hallo **argumenten** deel uit van Hallo verwijzing sectie **elementen in de definitie van Hallo XML-bestand** Hallo Quick Start-voorbeeld te volgen.

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a>Quick Start-voorbeeld: definiëren, verpakken en registreren van een aangepaste R-module
In dit voorbeeld ziet u hoe tooconstruct Hallo voor bestanden die vereist zijn door een aangepaste R-module, verpakken in een zip-bestand en registreren Hallo-module in Machine Learning-werkruimte. Hallo voorbeeld zip-pakket en voorbeeld-bestanden kunnen worden gedownload vanuit [CustomAddRows.zip downloaden bestand](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).

## <a name="hello-source-file"></a>Hallo-bronbestand
Bekijk Hallo voorbeeld van een **rijen toevoegen van aangepaste** module die u de standaardimplementatie Hallo Hallo wijzigt **rijen toevoegen** module tooconcatenate rijen (opmerkingen) van twee gegevenssets (gegevensframes) gebruikt. Hallo standaard **rijen toevoegen** module voegt Hallo rijen van Hallo tweede invoergegevensset toohello einde van Hallo eerste invoergegevensset met Hallo `rbind` algoritme. Hallo aangepast `CustomAddRows` functie op dezelfde manier accepteert twee gegevenssets, maar ook een parameter Booleaanse wisselen als extra invoer. Als Hallo swap-parameter is ingesteld, te**FALSE**, het retourneert Hallo dezelfde gegevensset zoals Hallo standaardimplementatie. Maar als Hallo wisselen parameter **TRUE**, Hallo functie voegt rijen van de eerste invoergegevensset toohello einde van de tweede gegevensset Hallo in plaats daarvan. Hallo CustomAddRows.R-bestand met de Hallo-implementatie van Hallo R `CustomAddRows` functie die worden weergegeven door Hallo **rijen toevoegen van aangepaste** module heeft Hallo R code te volgen.

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) 
    {
        if (swap)
        {
            return (rbind(dataset2, dataset1));
        }
        else
        {
            return (rbind(dataset1, dataset2));
        } 
    } 

### <a name="hello-xml-definition-file"></a>Hallo definitie XML-bestand
tooexpose dit `CustomAddRows` functie als een Azure Machine Learning-module, een XML-definitie-bestand moet worden gemaakt toospecify hoe Hallo **rijen toevoegen van aangepaste** module dient uiterlijk en gedrag. 

    <!-- Defined a module using an R Script -->
    <Module name="Custom Add Rows">
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother. Dataset 2 is concatenated tooDataset 1 when Swap is FALSE, and vice versa when Swap is TRUE.</Description>

    <!-- Specify hello base language, script file and R function toouse for this module. -->        
        <Language name="R" 
         sourceFile="CustomAddRows.R" 
         entryPoint="CustomAddRows" />  

    <!-- Define module input and output ports -->
    <!-- Note: hello values of hello id attributes in hello Input and Arg elements must match hello parameter names in hello R Function CustomAddRows defined in CustomAddRows.R. -->
        <Ports>
            <Input id="dataset1" name="Dataset 1" type="DataTable">
                <Description>First input dataset</Description>
            </Input>
            <Input id="dataset2" name="Dataset 2" type="DataTable">
                <Description>Second input dataset</Description>
            </Input>
            <Output id="dataset" name="Dataset" type="DataTable">
                <Description>hello combined dataset</Description>
            </Output>
        </Ports>

    <!-- Define module parameters -->
        <Arguments>
            <Arg id="swap" name="Swap" type="bool" >
                <Description>Swap input datasets.</Description>
            </Arg>
        </Arguments>
    </Module>


Het is essentieel toonote die waarde van Hallo Hallo **id** kenmerken van Hallo **invoer** en **Arg** elementen in de XML-bestand Hallo moeten overeenkomen met de Hallo functie parameternamen Hallo R code in Hallo CustomAddRows.R bestand exact: (*dataset1*, *dataset2*, en *wisselen* in Hallo voorbeeld). Op deze manier Hallo waarde Hallo **entryPoint** kenmerk Hallo **taal** element moet exact Hallo-naam van Hallo-functie in Hallo R-script: (*CustomAddRows* in Hallo voorbeeld). 

Daarentegen Hallo **id** kenmerk voor Hallo **uitvoer** element komt niet overeen met tooany variabelen in Hallo R-script. Als meer dan één uitvoer vereist is, gewoon retourneren een lijst van Hallo R-functie met resultaten geplaatst *in Hallo dezelfde volgorde* als **uitvoer** elementen zijn gedeclareerd in Hallo XML-bestand.

### <a name="package-and-register-hello-module"></a>Hallo-module voor pakket- en registreren
Deze twee bestanden opslaan als *CustomAddRows.R* en *CustomAddRows.xml* en vervolgens zip Hallo twee bestanden samen in een *CustomAddRows.zip* bestand.

ze op in uw Machine Learning-werkruimte, Ga tooyour werkruimte in Hallo Machine Learning Studio, klikt u op Hallo tooregister **+ nieuw** knop op Hallo onder en kies **MODULE -> van ZIP-pakket** tooupload Hallo nieuwe **rijen toevoegen van aangepaste** module.

![Zip uploaden](./media/machine-learning-custom-r-modules/upload-from-zip-package.png)

Hallo **rijen toevoegen van aangepaste** -module is nu gereed toobe toegankelijk is voor uw Machine Learning-experimenten.

## <a name="elements-in-hello-xml-definition-file"></a>Elementen in de definitie van Hallo XML-bestand
### <a name="module-elements"></a>Module-elementen
Hallo **Module** element heeft de gebruikte toodefine een aangepaste module in Hallo XML-bestand. Meerdere modules kunnen worden gedefinieerd in een XML-bestand meerdere **module** elementen. Elke module in uw werkruimte moet een unieke naam hebben. Een aangepaste module hebt geregistreerd met dezelfde naam als een bestaande aangepaste module Hallo en vervangt bestaande module Hallo Hello nieuwe. Aangepaste modules kunnen echter worden geregistreerd met dezelfde naam als een bestaande Azure Machine Learning module Hallo. Als u dus ze worden weergegeven in Hallo **aangepaste** categorie van het modulepalet Hallo.

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother...</Description>/> 


Binnen Hallo **Module** element, kunt u twee extra optionele elementen:

* een **eigenaar** element dat is ingesloten in het Hallo-module  
* een **beschrijving** element bevat tekst die wordt weergegeven in de help voor Hallo-module van snelle en wanneer u de muisaanwijzer op Hallo-module in Machine Learning UI Hallo.

Regels voor de limieten van de tekens in Hallo Module elementen:

* waarde van Hallo Hallo **naam** kenmerk in Hallo **Module** element mag niet groter zijn dan 64 tekens lang zijn. 
* inhoud van het Hallo Hallo **beschrijving** element mag niet groter zijn dan 128 tekens.
* inhoud van het Hallo Hallo **eigenaar** element mag niet groter zijn dan 32 tekens lang zijn.

De resultaten van de module kunnen deterministische of nondeterministic.* * standaard, alle modules worden beschouwd als toobe deterministisch. Dat wil zeggen, gezien een onveranderlijke reeks invoerparameters en gegevens, Hallo module moet worden geretourneerd Hallo dezelfde resulteert eacRAND of een functionh terwijl die deze wordt uitgevoerd. Dit gedrag, Azure Machine Learning Studio wordt alleen opnieuw uitgevoerd modules die zijn gemarkeerd als deterministisch als een parameter of de invoergegevens Hallo is gewijzigd. Retourneren van resultaten in de cache opgeslagen Hallo biedt ook veel experimenten sneller wordt uitgevoerd.

Er zijn functies die niet-deterministisch, zoals RNG of een functie die Hallo huidige datum of tijd retourneert. Als uw module heeft een niet-deterministische functie gebruikt, kunt u opgeven dat Hallo-module is niet-deterministische door Hallo instelling optioneel **isDeterministic** te kenmerk**FALSE**. Hierdoor weet u zeker dat Hallo-module is opnieuw uitgevoerd wanneer Hallo experiment wordt uitgevoerd, zelfs als hello module-invoer en parameters zijn niet gewijzigd. 

### <a name="language-definition"></a>Definitie van de taal
Hallo **taal** -element in het XML-definitie-bestand is gebruikte toospecify Hallo aangepaste module taal. R is momenteel alleen ondersteund taal Hallo. waarde van Hallo Hallo **bronbestand** kenmerk moet Hallo-naam van Hallo R-bestand met Hallo functie toocall Hallo module wordt uitgevoerd. Dit bestand moet deel uitmaken van Hallo zip-pakket. waarde van Hallo Hallo **entryPoint** kenmerk Hallo-naam van Hallo-functie wordt aangeroepen en moet overeenkomen met een geldige functie gedefinieerd met in Hallo-bronbestand.

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a>Poorten
Hallo invoer en uitvoer poorten voor een aangepaste module worden opgegeven in de onderliggende elementen van Hallo **poorten** sectie van definitie Hallo XML-bestand. Hallo-volgorde van deze elementen bepaalt Hallo layout ervaren (UX) door gebruikers. het eerste onderliggende Hello **invoer** of **uitvoer** die worden vermeld in Hallo **poorten** element van Hallo XML-bestand wordt Hallo meest linkse invoerpoort in Machine Learning UX Hallo
Elk invoer en uitvoerpoort heeft misschien een optionele **beschrijving** onderliggend element waarmee Hallo-tekst die wordt weergegeven wanneer u de muisaanwijzer muisaanwijzer Hallo Hallo-poort in Hallo Machine Learning-gebruikersinterface.

**Regels poorten**:

* Maximum aantal **invoer en uitvoer poorten** is 8 voor elk.

### <a name="input-elements"></a>Invoer-elementen
Ingangspoorten kunnen u toopass gegevens tooyour R-functie en de werkruimte. Hallo **gegevenstypen** die worden ondersteund voor ingangspoorten als volgt zijn: 

**DataTable:** dit type functie tooyour R is doorgegeven als een data.frame. In feite geen typen (bijvoorbeeld CSV-bestanden of bestanden ARFF) die worden ondersteund door Machine Learning en die compatibel zijn met **DataTable** geconverteerde tooa data.frame automatisch zijn. 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

Hallo **id** die zijn gekoppeld aan elk kenmerk **DataTable** invoerpoort moet een unieke waarde hebben en deze waarde moet overeenkomen met de bijbehorende parameter in uw R-functie met de naam.
Optionele **DataTable** poorten die niet worden doorgegeven als invoer in een experiment Hallo waarde hebben **NULL** doorgegeven toohello R-functie en optioneel zip-poorten worden genegeerd als Hallo-invoer is niet verbonden. Hallo **isOptional** kenmerk is optioneel voor beide Hallo **DataTable** en **Zip** en afkomstig is *false* standaard.

**Postcode:** aangepaste modules kunnen een zip-bestand als invoer worden geaccepteerd. Deze invoer is uitgepakt in de werkmap Hallo R van de functie

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files toobe extracted toohello R working directory.</Description>
           </Input>

Voor aangepaste R-modules heeft Hallo-id voor een Zip-poort geen toomatch parameters van functie Hallo R. Dit komt omdat Hallo zip-bestand automatisch uitgepakte toohello R-werkmap.

**Invoer regels:**

* waarde van Hallo Hallo **id** kenmerk Hallo **invoer** element moet een geldige R variabelenaam in.
* waarde van Hallo Hallo **id** kenmerk Hallo **invoer** element mag niet langer zijn dan 64 tekens zijn.
* waarde van Hallo Hallo **naam** kenmerk Hallo **invoer** element mag niet langer zijn dan 64 tekens zijn.
* inhoud van het Hallo Hallo **beschrijving** element mag niet langer zijn dan 128 tekens zijn
* waarde van Hallo Hallo **type** kenmerk Hallo **invoer** element moet *Zip* of *DataTable*.
* waarde van Hallo Hallo **isOptional** kenmerk Hallo **invoer** element is niet vereist (en *false* standaard als niet is opgegeven); maar als deze is opgegeven, moet dit *true* of *false*.

### <a name="output-elements"></a>Elementen van de uitvoer
**Standaard uitvoer poorten:** uitvoerpoorten zijn toegewezen toohello retourwaarden van uw R-functie, die vervolgens kunnen worden gebruikt door de volgende modules. *DataTable* Hallo alleen standaarduitvoer poort type op dit moment ondersteund. (Ondersteuning voor *overbrengen* en *transformeert* ontbreekt.) Een *DataTable* uitvoer is gedefinieerd als:

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

Voor de uitvoer in aangepaste R-modules Hallo waarde Hallo **id** kenmerk heeft geen toocorrespond met iets in Hallo R-script, maar deze moet uniek zijn. Voor een uitvoer één module Hallo geretourneerde waarde van Hallo R-functie moet een *data.frame*. In volgorde toooutput meer dan een object van een ondersteund gegevenstype, Hallo juiste output poorten moeten toobe opgegeven in de definitie van Hallo XML-bestand en Hallo objecten moeten toobe geretourneerd als een lijst. Hallo uitvoer objecten toegewezen toooutput poorten uit de linker tooright, opgetreden bij het Hallo-volgorde waarin Hallo objecten worden geplaatst in de lijst geretourneerd Hallo weergeven.

Bijvoorbeeld, als u wilt dat toomodify hello **rijen toevoegen van aangepaste** module toooutput Hallo oorspronkelijke twee gegevenssets, *dataset1* en *dataset2*, Daarnaast toohello nieuw lid DataSet *gegevensset*, (in volgorde, van links tooright als: *gegevensset*, *dataset1*, *dataset2*), vervolgens Hallo definiëren poorten in Hallo CustomAddRows.xml bestand als volgt uitvoeren:

    <Ports> 
        <Output id="dataset" name="Dataset Out" type="DataTable"> 
            <Description>New Dataset</Description> 
        </Output> 
        <Output id="dataset1_out" name="Dataset 1 Out" type="DataTable"> 
            <Description>First Dataset</Description> 
        </Output> 
        <Output id="dataset2_out" name="Dataset 2 Out" type="DataTable"> 
            <Description>Second Dataset</Description> 
        </Output> 
        <Input id="dataset1" name="Dataset 1" type="DataTable"> 
            <Description>First Input Table</Description>
        </Input> 
        <Input id="dataset2" name="Dataset 2" type="DataTable"> 
            <Description>Second Input Table</Description> 
        </Input> 
    </Ports> 


En retourneren een lijst Hallo-lijst van objecten in de juiste volgorde Hallo in 'CustomAddRows.R':

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

**Visualisatie uitvoer:** kunt u ook een uitvoerpoort van het type opgeven *visualisatie*, die Hallo-uitvoer van Hallo R grafische apparaat en de console-uitvoer wordt weergegeven. Deze poort maakt geen deel uit van de uitvoer van de functie Hallo R en niet van invloed op volgorde Hallo Hallo andere poorttypen uitvoer. tooadd toevoegen van een visualisatie poort toohello aangepaste modules die een **uitvoer** element met een waarde van *visualisatie* voor de **type** kenmerk:

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View hello R console graphics device output.</Description>
    </Output>

**Regels voor uitvoer:**

* waarde van Hallo Hallo **id** kenmerk Hallo **uitvoer** element moet een geldige R variabelenaam in.
* waarde van Hallo Hallo **id** kenmerk Hallo **uitvoer** element mag niet langer zijn dan 32 tekens lang zijn.
* waarde van Hallo Hallo **naam** kenmerk Hallo **uitvoer** element mag niet langer zijn dan 64 tekens zijn.
* waarde van Hallo Hallo **type** kenmerk Hallo **uitvoer** element moet *visualisatie*.

### <a name="arguments"></a>Argumenten
Aanvullende gegevens kan toohello R-functie worden doorgegeven via de moduleparameters die zijn gedefinieerd in Hallo **argumenten** element. Deze parameters worden weergegeven in de meest rechtse eigenschappendeelvenster Hallo Hallo Machine Learning UI wanneer Hallo-module is geselecteerd. Argumenten kunnen worden ondersteund Hallo typen of kunt u een aangepaste opsomming wanneer deze nodig is. Vergelijkbare toohello **poorten** elementen, **argumenten** elementen kunnen hebben een optioneel **beschrijving** element waarmee wordt aangegeven Hallo-tekst die wordt weergegeven wanneer u de Hallo muisaanwijzer via Hallo parameternaam.
Optionele eigenschappen voor een module, zoals defaultValue minValue en maxValue tooany argument zoals tooa kenmerken kunnen worden toegevoegd **eigenschappen** element. Geldige eigenschappen voor Hallo **eigenschappen** element afhankelijk zijn van Hallo argumenttype en met de argumenttypen hello wordt ondersteund in de volgende sectie Hallo worden beschreven. Argumenten Hello **isOptional** eigenschappenset te**'true'** vereisen geen Hallo gebruiker tooenter een waarde. Als een waarde toohello argument niet is opgegeven, is klikt u vervolgens Hallo-argument niet doorgegeven functie vermeldingspunt toohello. Argumenten van de functie vermeldingspunt Hallo die optionele nodig toobe expliciet verwerkt door de functie Hallo toegewezen bijvoorbeeld een standaardwaarde van NULL in Hallo vermelding punt functiedefinitie. Een optioneel argument wordt alleen afgedwongen Hallo andere beperkingen argument, dat wil zeggen min of max, als een waarde is opgegeven door de gebruiker Hallo.
Met in- en uitgangen is het cruciaal dat elk Hallo parameters unieke id-waarden die zijn gekoppeld hebben. In onze snel starten voorbeeld Hallo gekoppeld id-parameter is *wisselen*.

### <a name="arg-element"></a>Arg element
Een module-parameter is gedefinieerd met behulp van Hallo **Arg** onderliggend element van Hallo **argumenten** sectie van definitie Hallo XML-bestand. Net als bij Hallo onderliggende elementen in Hallo **poorten** sectie, Hallo ordening van parameters in Hallo **argumenten** sectie Hallo lay-out aangetroffen in Hallo UX worden gedefinieerd Hallo parameters staan van boven naar beneden in Hallo UI in dezelfde volgorde in die ze gedefinieerd Hallo in Hallo XML-bestand. Hallo die worden ondersteund door Machine Learning voor parameters worden hier weergegeven. 

**int** – een typeparameter van geheel getal (32-bits).

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* *Optionele eigenschappen*: **min**, **max**, **standaard** en **isOptional**

**dubbele** – een double-type-parameter.

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* *Optionele eigenschappen*: **min**, **max**, **standaard** en **isOptional**

**BOOL** – een Boole-parameter die wordt vertegenwoordigd door een selectievakje in UX

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* *Optionele eigenschappen*: **standaard** -false als dat niet is ingesteld

**tekenreeks**: een standaardtekenreeks

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* *Optionele eigenschappen*: **standaard** en **isOptional**

**ColumnPicker**: een parameter van de selectie kolom. Dit type wordt gerenderd in Hallo UX als het kiezen van een kolom. Hallo **eigenschap** element is gebruikte hier toospecify Hallo-id van Hallo-poort van waaruit de kolommen worden geselecteerd, waarop Hallo poort doeltype moet *DataTable*. Hallo-resultaat van Hallo kolomselectie wordt toohello R functie doorgegeven als een lijst met tekenreeksen met de kolomnamen Hallo geselecteerd. 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* *Vereiste eigenschappen*: **portId** -komt overeen met de id van een invoer-element met type Hallo *DataTable*.
* *Optionele eigenschappen*:
  
  * **allowedTypes** -Filters Hallo kolom typen uit die u kunt kiezen. Geldige waarden zijn: 
    
    * numerieke
    * Booleaanse waarde
    * Categorische gegevens
    * Tekenreeks
    * Label
    * Functie
    * Score
    * Alle
  * **standaard** -geldig standaardselecties voor Hallo kolomkiezer omvatten: 
    
    * Geen
    * NumericFeature
    * NumericLabel
    * NumericScore
    * NumericAll
    * BooleanFeature
    * BooleanLabel
    * BooleanScore
    * BooleanAll
    * CategoricalFeature
    * CategoricalLabel
    * CategoricalScore
    * CategoricalAll
    * StringFeature
    * StringLabel
    * StringScore
    * StringAll
    * AllLabel
    * AllFeature
    * AllScore
    * Alle

**Vervolgkeuzelijst**: een gebruiker opgegeven opgesomde (vervolgkeuzelijst) wordt weergegeven. Hallo dropdown artikelen zijn opgegeven in Hallo **eigenschappen** met behulp van element een **Item** element. Hallo **id** voor elk **Item** moeten uniek zijn en een geldige R-variabele. waarde van Hallo Hallo **naam** van een **Item** fungeert als zowel Hallo-tekst die wordt weergegeven als Hallo-waarde die wordt doorgegeven toohello R-functie.

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* *Optionele eigenschappen*:
  * **standaard** - hello waarde voor de standaardeigenschap Hallo met een id-waarde van een Hallo overeenkomen moet **Item** elementen.

### <a name="auxiliary-files"></a>Hulpbestanden
Elk bestand dat wordt geplaatst in uw aangepaste module-ZIP-bestand is momenteel toobe beschikbaar voor gebruik tijdens uitvoeringstijd. Eventuele mapstructuren aanwezig blijven behouden. Dit betekent dat bestand sourcing works dezelfde Hallo lokaal en in Azure Machine Learning worden uitgevoerd. 

> [!NOTE]
> Merk op dat alle bestanden uitgepakt too'src zijn ' directory zodat alle paden moet ' src /' voorvoegsel.
> 
> 

Stel dat u wilt tooremove rijen met NAs uit Hallo gegevensset en ook eventuele dubbele rijen verwijderen voordat deze worden uitgevoerd in CustomAddRows als u al een R functie die in een bestand RemoveDupNARows.R hebt geschreven:

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
U kunt bronbestand Hallo reserve RemoveDupNARows.R in Hallo CustomAddRows functie:

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) {
        source("src/RemoveDupNARows.R")
            if (swap) { 
                dataset <- rbind(dataset2, dataset1))
             } else { 
                  dataset <- rbind(dataset1, dataset2)) 
             } 
        dataset <- removeDupNARows(dataset)
        return (dataset)
    }

Vervolgens uploaden een zip-bestand met 'CustomAddRows.R', 'CustomAddRows.xml' en 'RemoveDupNARows.R' als een aangepaste R-module.

## <a name="execution-environment"></a>Uitvoeringsomgeving
Hallo uitvoeringsomgeving voor Hallo R-script maakt gebruik van dezelfde versie van R als Hallo Hallo **R-Script uitvoeren** module en gebruik kunt Hallo dezelfde standaard pakketten. U kunt ook aanvullende R-pakketten tooyour aangepaste module toevoegen door ze in Hallo aangepaste module-zip-pakket. Zojuist geladen in het R-script zoals u zou in uw eigen omgeving voor R doen. 

**Beperkingen van de uitvoeringsomgeving Hallo** omvatten:

* Niet-permanente bestandssysteem: bestanden die zijn geschreven wanneer Hallo aangepaste module wordt uitgevoerd, blijven niet bestaan voor meerdere uitvoert Hallo dezelfde module.
* Er is geen toegang tot het netwerk

