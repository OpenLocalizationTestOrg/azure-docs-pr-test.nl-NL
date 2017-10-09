---
title: aaaScale U-SQL lokaal uitvoeren en testen met Azure Data Lake U-SQL-SDK | Microsoft Docs
description: Ontdek hoe lokale toouse Azure Data Lake U-SQL-SDK tooscale U-SQL-taken uitvoeren en testen met de opdrachtregel en API's op uw lokale werkstation.
services: data-lake-analytics
documentationcenter: 
author: 
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: yanacai
ms.openlocfilehash: 2b0a16229789268e333f723ff6fc2c3efdc29905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a>Schaal U-SQL lokaal uitvoeren en testen met Azure Data Lake U-SQL-SDK

Bij het ontwikkelen van U-SQL-script, is het algemene toorun en U-SQL-testscript lokaal vóór het indienen toocloud. Azure Data Lake biedt een Nuget-pakket Azure Data Lake U-SQL-SDK voor dit scenario aangeroepen, via die u kunt gemakkelijk de schaal van U-SQL lokaal uitvoeren en testen. Het is ook mogelijk toointegrate dit U-SQL testen met CI (continue integratie) systeem tooautomate Hallo compileren en testen.

Als u het belangrijkst hoe toomanually lokale uitvoeren en fouten opsporen in U-SQL-script met GUI tooling, kunt u Azure Data Lake Tools voor Visual Studio gebruiken voor die. U kunt meer informatie van [hier](data-lake-analytics-data-lake-tools-local-run.md).

## <a name="install-azure-data-lake-u-sql-sdk"></a>Installeren Azure Data Lake U-SQL-SDK

U krijgt hello Azure Data Lake U-SQL-SDK [hier](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) op Nuget.org. En voordat u deze gebruikt, moet u ervoor dat u als volgt afhankelijkheden hebt toomake.

### <a name="dependencies"></a>Afhankelijkheden

Hallo SDK voor Data Lake U-SQL vereist Hallo afhankelijkheden te volgen:

- [Microsoft .NET Framework 4.6 of nieuwere](https://www.microsoft.com/download/details.aspx?id=17851).
- Microsoft Visual C++-14 en Windows-SDK 10.0.10240.0 of hoger (die wordt CppSDK in dit artikel genoemd). Er zijn twee manieren tooget CppSDK:

    - Installeer [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou). U hebt een \Windows Kits\10 map onder de map Program Files van Hallo--bijvoorbeeld C:\Program Files (x86) \Windows Kits\10\. Ook vindt u Hallo Windows 10 SDK versie onder \Windows Kits\10\Lib. Als u deze mappen niet ziet, installeer Visual Studio en ervoor tooselect Hallo SDK voor Windows 10 worden tijdens de installatie van Hallo. Als u dit geïnstalleerd met Visual Studio hebt, vindt lokale Hallo U-SQL-compiler deze automatisch.

    ![Data Lake Tools voor Visual Studio local-klaar Windows 10-SDK](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - Installeer [Data Lake Tools voor Visual Studio](http://aka.ms/adltoolsvs). U vindt Hallo voorverpakt Visual C++- en Windows SDK-bestanden op C:\Program Files (x86) \Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK. Hallo afhankelijkheden niet in dit geval automatisch door lokale U-SQL-compiler Hallo vinden. Hiervoor moet u toospecify hello CppSDK pad. Hallo bestanden tooanother locatie kopiëren of gebruikt u deze zo is.

## <a name="understand-basic-concepts"></a>Basisconcepten begrijpen

### <a name="data-root"></a>Gegevenshoofdmap

Hallo-gegevens-hoofdmap is een 'lokale store' voor Hallo lokale compute-account. Het is equivalente toohello Azure Data Lake Store-account van een Data Lake Analytics-account. Overschakelen van tooa is verschillende gegevens uit een hoofdmap net als andere store-account tooa overschakelen. Als u gegevens tooaccess vaak gedeeld met andere gegevens hoofdmappen wilt, moet u in uw scripts absolute paden gebruiken. Of het bestand system symbolische koppelingen maken (bijvoorbeeld **mklink** van NTFS) onder het Hallo-gegevenshoofdmap map toopoint toohello gedeelde gegevens.

Hallo data-hoofdmap wordt gebruikt voor:

- Lokale metagegevens, zoals databases, tabellen, tabelfuncties (tvf's) en assembly's opgeslagen.
- Hallo invoer en uitvoerpaden die zijn gedefinieerd als relatieve paden in de U-SQL opzoeken. Gebruik relatieve paden maakt het eenvoudiger toodeploy uw tooAzure U-SQL-projecten.

### <a name="file-path-in-u-sql"></a>Bestandspad in U-SQL

U kunt een relatief pad en een lokaal absoluut pad in U-SQL-scripts gebruiken. Hallo relatief pad is relatief toohello opgegeven gegevenshoofdmap mappad. U wordt aangeraden dat u gebruik ' / ' Hallo als pad scheidingsteken toomake uw scripts die compatibel is met het Hallo-serverzijde. Hier volgen enkele voorbeelden van relatieve paden en hun equivalente absolute paden. In deze voorbeelden is C:\LocalRunDataRoot hello, gegevens-hoofdmap.

|Relatief pad|Het absolute pad|
|-------------|-------------|
|/ABC/DEF/Input.csv |C:\LocalRunDataRoot\abc\def\input.csv|
|ABC/DEF/Input.csv  |C:\LocalRunDataRoot\abc\def\input.csv|
|D:/ABC/DEF/Input.csv |D:\abc\def\input.csv|

### <a name="working-directory"></a>Werkmap

Wanneer Hallo U-SQL-script lokaal wordt uitgevoerd, wordt een werkmap tijdens de compilatie onder de huidige actieve directory gemaakt. Bovendien toohello compilatie levert, hello nodig runtime-bestanden voor lokale uitvoering worden shadow gekopieerde toothis werkmap. Hallo werken directory hoofdmap 'ScopeWorkDir' wordt genoemd en Hallo bestanden onder Hallo werkmap zijn als volgt:

|Map/bestand|Map/bestand|Map/bestand|Definitie|Beschrijving|
|--------------|--------------|--------------|----------|-----------|
|C6A101DDCB470506| | |Hash-tekenreeks van de runtime-versie|Schaduwkopie van de runtimebestanden die nodig zijn voor lokale uitvoering|
| |Script_66AE4909AA0ED06C| |De naam van een script + hash-tekenreeks van scriptpad|Compilatie-uitvoer en uitvoering van stap logboekregistratie|
| | |\_script\_.abr|Compiler-uitvoer|Wiskundige bestand|
| | |\_ScopeCodeGen\_. *|Compiler-uitvoer|Beheerde code gegenereerd|
| | |\_ScopeCodeGenEngine\_. *|Compiler-uitvoer|Gegenereerde systeemeigen code|
| | |assemblies waarnaar wordt verwezen|Assembly-verwijzing|Bestanden van de assembly waarnaar wordt verwezen|
| | |deployed_resources|Resources implementeren|Bronbestanden van de implementatie|
| | |XXXXXXXX.xxx[1..n]\_\*. *|Uitvoeringslogboek|Logboek van de stappen worden uitgevoerd|


## <a name="use-hello-sdk-from-hello-command-line"></a>Hallo SDK vanaf de opdrachtregel hello gebruiken

### <a name="command-line-interface-of-hello-helper-application"></a>Opdrachtregelinterface van Hallo helper-toepassing

Onder de SDK-directory\build\runtime is LocalRunHelper.exe Hallo opdrachtregelprogramma toepassing die voorziet in interfaces toomost Hallo gebruikte lokaal uitvoeren functies. Houd er rekening mee dat zowel opdracht Hallo en Hallo schakelopties hoofdlettergevoelig zijn. tooinvoke het:

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

LocalRunHelper.exe worden uitgevoerd zonder argumenten of met Hallo **help** overschakelen tooshow Hallo help-informatie:

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile hello script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

In Hallo help-informatie:

-  **Opdracht** geeft de naam van de opdracht Hallo.  
-  **Een vereist Argument** een lijst met argumenten die moeten worden opgegeven.  
-  **Optioneel Argument** een lijst met argumenten die optioneel, met standaardwaarden zijn.  Optionele Booleaanse argumenten geen parameters hebben en hun uiterlijk betekenen negatieve tootheir standaardwaarde.

### <a name="return-value-and-logging"></a>Retourwaarde en logboekregistratie

retourneert de helper-toepassing Hello **0** voor succes en **-1** van de fout. Hallo helper verzendt standaard alle berichten toohello huidige console. De meeste opdrachten Hallo ondersteunen echter Hallo **- MessageOut pad_naar_logboekbestand** optioneel argument die enterpriseenrollment.contoso.com Hallo levert tooa logboekbestand.

### <a name="environment-variable-configuring"></a>Omgeving variabele configureren

U-SQL lokaal moet een hoofdmap opgegeven gegevens run as-account met lokale opslag, evenals een opgegeven pad CppSDK voor afhankelijkheden. U kunt beide argument set Hallo in opdrachtregel- of stel omgevingsvariabele voor hen.

- Set Hallo **SCOPE_CPP_SDK** omgevingsvariabele.

    Als u Microsoft Visual C++ en Hallo Windows SDK door het installeren van Data Lake Tools voor Visual Studio, Controleer of u Hallo volgende map:

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    Definieer een nieuwe omgevingsvariabele aangeroepen **SCOPE_CPP_SDK** toopoint toothis directory. Of Hallo map toohello andere locatie kopiëren en geef **SCOPE_CPP_SDK** als die.

    In de omgevingsvariabele voor toevoeging toosetting hello, kunt u Hallo **- CppSDK** argument wanneer u Hallo vanaf de opdrachtregel. Dit argument overschrijft uw standaard CppSDK-omgevingsvariabele.

- Set Hallo **LOCALRUN_DATAROOT** omgevingsvariabele.

    Definieer een nieuwe omgevingsvariabele aangeroepen **LOCALRUN_DATAROOT** die toohello gegevenshoofdmap verwijst.

    In de omgevingsvariabele voor toevoeging toosetting hello, kunt u Hallo **- DataRoot** argument met het Hallo-gegevenshoofdmap pad wanneer u een opdrachtregel. Dit argument wordt overschreven door de omgevingsvariabele van uw standaard-hoofdmap van de gegevens. U moet dit argument tooevery vanaf de opdrachtregel uitvoert zodat u kunt Hallo standaard gegevenshoofdmap omgevingsvariabele voor alle bewerkingen overschrijven tooadd.

### <a name="sdk-command-line-usage-samples"></a>SDK opdrachtregel usage-voorbeelden

#### <a name="compile-and-run"></a>Compileren en uitvoeren

Hallo **uitvoeren** opdracht wordt gebruikt voor toocompile Hallo script en vervolgens de resultaten wordt uitgevoerd. De opdrachtregelargumenten zijn een combinatie van die van **compileren** en **uitvoeren**.

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

Hallo volgen optionele argumenten voor **uitvoeren**:


|Argument|Standaardwaarde|Beschrijving|
|--------|-------------|-----------|
|-CodeBehind|False|Hallo-script heeft .cs code achter|
|-CppSDK| |CppSDK Directory|
|-DataRoot| De omgevingsvariabele DataRoot|DataRoot voor lokale uitvoering te standaard 'LOCALRUN_DATAROOT'-omgevingsvariabele|
|-MessageOut| |Dump berichten op console tooa bestand|
|-Parallel|1|Voer Hallo plan met Hallo opgegeven parallelle uitvoering|
|-Verwijzingen| |Lijst met paden tooextra verwijzings-assembly's of de gegevensbestanden van de code achter, gescheiden door ';'|
|-UdoRedirect|False|Udo assembly omleiding config genereren|
|-UseDatabase|model|Database-toouse voor code achter tijdelijke assembly-registratie|
|-Verbose|False|Gedetailleerde uitvoer van de runtime weergeven|
|-WorkDir|Huidige map|Map voor de compiler gebruiks- en uitvoer|
|-RunScopeCEP|0|ScopeCEP modus toouse|
|-ScopeCEPTempPath|TEMP|Toouse temp-pad voor het streamen van gegevens|
|-OptFlags| |Door komma's gescheiden lijst met optimalisatie van vlaggen|


Hier volgt een voorbeeld:

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

Naast combineren **compileren** en **uitvoeren**, u kunt compileren en uitvoerbare bestanden Hallo gecompileerd afzonderlijk uitvoeren.

#### <a name="compile-a-u-sql-script"></a>Compileren van een U-SQL-script

Hallo **compileren** opdracht gebruikte toocompile een U-SQL-script tooexecutables is.

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

Hallo volgen optionele argumenten voor **compileren**:


|Argument|Beschrijving|
|--------|-----------|
| -CodeBehind [standaardwaarde 'False']|Hallo-script heeft .cs code achter|
| -CppSDK [standaardwaarde '']|CppSDK Directory|
| -DataRoot [standaardwaarde 'Omgevingsvariabele DataRoot']|DataRoot voor lokale uitvoering te standaard 'LOCALRUN_DATAROOT'-omgevingsvariabele|
| -MessageOut [standaardwaarde '']|Dump berichten op console tooa bestand|
| -Verwijst naar [standaardwaarde '']|Lijst met paden tooextra verwijzings-assembly's of de gegevensbestanden van de code achter, gescheiden door ';'|
| -Recente [standaardwaarde 'False']|Recente compileren|
| -UdoRedirect [standaardwaarde 'False']|Udo assembly omleiding config genereren|
| -UseDatabase [standaardwaarde 'master']|Database-toouse voor code achter tijdelijke assembly-registratie|
| -WorkDir [standaardwaarde 'Huidige map']|Map voor de compiler gebruiks- en uitvoer|
| -RunScopeCEP [standaardwaarde '0']|ScopeCEP modus toouse|
| -ScopeCEPTempPath [standaardwaarde 'temp']|Toouse temp-pad voor het streamen van gegevens|
| -OptFlags [standaardwaarde '']|Door komma's gescheiden lijst met optimalisatie van vlaggen|


Hier volgen enkele voorbeelden van het gebruik.

Compileren van een U-SQL-script:

    LocalRunHelper compile -Script d:\test\test1.usql

Compileren van een U-SQL-script en stel Hallo data-hoofdmap. Houd er rekening mee dat dit Hallo set omgevingsvariabele wordt overschreven.

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

Compileren van een U-SQL-script en stel een werkmap, de referentie-assembly en de database:

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a>Gecompileerde resultaten uitvoeren

Hallo **uitvoeren** opdracht is gebruikte tooexecute gecompileerd resultaten.   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

Hallo volgen optionele argumenten voor **uitvoeren**:

|Argument|Beschrijving|
|--------|-----------|
|-DataRoot [standaardwaarde '']|De gegevenshoofdmap voor de uitvoering van de metagegevens. Wordt standaard toohello **LOCALRUN_DATAROOT** omgevingsvariabele.|
|-MessageOut [standaardwaarde '']|Dump berichten op het Hallo-console tooa-bestand.|
|-Parallel standaardwaarde '1'|Indicator toorun Hallo gegenereerd lokaal uitvoeren stappen Hello opgegeven parallelle uitvoering niveau.|
|-Verbose [standaardwaarde 'False']|Indicator tooshow gedetailleerde uitvoer van de runtime.|

Hier volgt een voorbeeld van gebruik:

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-hello-sdk-with-programming-interfaces"></a>Hallo SDK gebruiken met API 's

Hallo-API's bevinden zich in Hallo LocalRunHelper.exe. U kunt ze toointegrate Hallo functionaliteit van Hallo U-SQL-SDK gebruiken en C# test framework tooscale Hallo uw U-SQL-script lokaal testen. In dit artikel ik gebruik Hallo standaard C#-eenheid test project tooshow hoe toouse deze interfaces tootest uw U-SQL-script.

### <a name="step-1-create-c-unit-test-project-and-configuration"></a>Stap 1: C#-eenheid test-project en de configuratie maken

- Maak een C#-eenheid test-project via Bestand > Nieuw > Project > Visual C# > testen > Project eenheid testen.
- LocalRunHelper.exe toevoegen als een verwijzing voor Hallo-project. Hallo LocalRunHelper.exe bevindt zich op \build\runtime\LocalRunHelper.exe in Nuget-pakket.

    ![Azure Data Lake U-SQL-SDK verwijzing toevoegen](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- U-SQL-SDK **alleen** x64 ondersteuningsomgeving, zorg ervoor dat tooset build platform doel als x64. Dat kunt u instellen via projecteigenschap > bouwen > Platform doel.

    ![Azure Data Lake U-SQL-SDK configureren x64 Project](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- Zorg ervoor dat tooset uw testomgeving als x64. In Visual Studio kunt u dit instellen via testen > instellingen testen > processorarchitectuur standaard > x64.

    ![Azure Data Lake U-SQL-SDK configureren x64 testomgeving](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- Zorg ervoor dat toocopy alle afhankelijkheidsbestanden onder NugetPackage\build\runtime\ tooproject werkmap namelijk doorgaans ProjectFolder\bin\x64\Debug.

### <a name="step-2-create-u-sql-script-test-case"></a>Stap 2: Maak Testscenario U-SQL-script

Hieronder vindt u de voorbeeldcode Hallo voor U-SQL-script test. Voor het testen, moet u tooprepare scripts, invoerbestanden en bestanden van de verwachte uitvoer.

    using System;
    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using System.IO;
    using System.Text;
    using System.Security.Cryptography;
    using Microsoft.Analytics.LocalRun;

    namespace UnitTestProject1
    {
        [TestClass]
        public class USQLUnitTest
        {
            [TestMethod]
            public void TestUSQLScript()
            {
                //Specify hello local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure hello DateRoot path, Script Path and CPPSDK path
                localrun.DataRoot = "../../../";
                localrun.ScriptPath = "../../../Script/Script.usql";
                localrun.CppSdkDir = "../../../CppSDK";

                //Run U-SQL script
                localrun.DoRun();

                //Script output 
                string Result = Path.Combine(localrun.DataRoot, "Output/result.csv");

                //Expected script output
                string ExpectedResult = "../../../ExpectedOutput/result.csv";

                Test.Helpers.FileAssert.AreEqual(Result, ExpectedResult);

                //Don't forget tooclose MessageOutput tooget logs into file
                MessageOutput.Close();
            }
        }
    }

    namespace Test.Helpers
    {
        public static class FileAssert
        {
            static string GetFileHash(string filename)
            {
                Assert.IsTrue(File.Exists(filename));

                using (var hash = new SHA1Managed())
                {
                    var clearBytes = File.ReadAllBytes(filename);
                    var hashedBytes = hash.ComputeHash(clearBytes);
                    return ConvertBytesToHex(hashedBytes);
                }
            }

            static string ConvertBytesToHex(byte[] bytes)
            {
                var sb = new StringBuilder();

                for (var i = 0; i < bytes.Length; i++)
                {
                    sb.Append(bytes[i].ToString("x"));
                }
                return sb.ToString();
            }

            public static void AreEqual(string filename1, string filename2)
            {
                string hash1 = GetFileHash(filename1);
                string hash2 = GetFileHash(filename2);

                Assert.AreEqual(hash1, hash2);
            }
        }
    }


### <a name="programming-interfaces-in-localrunhelperexe"></a>Programming interfaces in LocalRunHelper.exe

LocalRunHelper.exe biedt Hallo programming interfaces voor de U-SQL lokaal compileren, uitvoeren, enz. Hallo interfaces als volgt worden vermeld.

**Constructor**

openbare LocalRunHelper ([System.IO.TextWriter messageOutput = null])

|Parameter|Type|Beschrijving|
|---------|----|-----------|
|messageOutput|System.IO.TextWriter|voor Uitvoerberichten, stelt u toonull toouse Console|

**Eigenschappen**

|Eigenschap|Type|Beschrijving|
|--------|----|-----------|
|AlgebraPath|Tekenreeks|Hallo pad tooalgebra bestand (wiskundige-bestand is een van de resultaten van Hallo compilatie)|
|CodeBehindReferences|Tekenreeks|Als Hallo script aanvullende code achter verwijzingen heeft, geeft u Hallo paden van elkaar gescheiden door ';'|
|CppSdkDir|Tekenreeks|CppSDK directory|
|CurrentDir|Tekenreeks|Huidige map|
|DataRoot|Tekenreeks|Pad naar de hoofdmap van gegevens|
|DebuggerMailPath|Tekenreeks|Hallo pad toodebugger mailslot|
|GenerateUdoRedirect|BOOL|Als we willen toogenerate assembly geladen omleiding config overschrijven|
|HasCodeBehind|BOOL|Als Hallo script heeft code achter|
|InputDir|Tekenreeks|Map voor invoergegevens|
|MessagePath|Tekenreeks|Bericht dump bestandspad|
|OutputDir|Tekenreeks|Map voor de uitvoergegevens|
|Parallelle uitvoering|int|Parallelle uitvoering toorun Hallo wiskundige|
|ParentPid|int|PID van Hallo bovenliggende op welke Hallo service tooexit, set too0 of negatieve tooignore bewaakt|
|ResultPath|Tekenreeks|Resultaat dump bestandspad|
|RuntimeDir|Tekenreeks|Runtime-map|
|scriptPath|Tekenreeks|Waar toofind script Hallo|
|Recente|BOOL|Recente compileren of niet|
|TempDir|Tekenreeks|Tijdelijke map|
|UseDataBase|Tekenreeks|Hallo database toouse voor code achter tijdelijke assembly-registratie, master standaard opgeven|
|WorkDir|Tekenreeks|Voorkeur werkmap|


**Methode**

|Methode|Beschrijving|retourneren|Parameter|
|------|-----------|------|---------|
|openbare bool DoCompile()|Hallo U-SQL-script compileren|True indien geslaagd| |
|openbare bool DoExec()|Hallo gecompileerd resultaat uitvoeren|True indien geslaagd| |
|openbare bool DoRun()|Voer Hallo U-SQL-script (compileren + uitvoeren)|True indien geslaagd| |
|openbare bool IsValidRuntimeDir (pad tekenreeks)|Controleer of de Hallo opgegeven pad geldig runtime pad|Geldt voor geldige|Hallo-pad van de runtime-map|


## <a name="faq-about-common-issue"></a>Veelgestelde vragen over veel voorkomende problemen

### <a name="error-1"></a>Fout 1:
E_CSC_SYSTEM_INTERNAL: Interne fout! Kan bestand of assembly 'ScopeEngineManaged.dll' of een afhankelijkheid hiervan niet laden. de opgegeven module Hallo kan niet worden gevonden.

Neem contact op met de volgende Hallo:

- Zorg ervoor dat u hebt x64 omgeving. Hallo build-doelplatform en Hallo testomgeving moet worden x64, raadpleeg dan te**stap 1: eenheid maken C#-project en configuratie testen** hierboven.
- Zorg ervoor dat u alle afhankelijkheidsbestanden onder NugetPackage\build\runtime\ tooproject werkmap hebt gekopieerd.


## <a name="next-steps"></a>Volgende stappen

* toolearn U-SQL, Zie [aan de slag met Azure Data Lake Analytics U-SQL-taal](data-lake-analytics-u-sql-get-started.md).
* toolog diagnostische informatie, Zie [toegang tot logboeken met diagnostische gegevens voor Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).
* Zie voor een complexere query toosee [websitelogboeken analyseren met Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).
* taakdetails tooview, Zie [gebruik taak Browser en weergave van de taak voor Azure Data Lake Analytics-taken](data-lake-analytics-data-lake-tools-view-jobs.md).
* toouse hello hoekpunt uitvoering weergave Zie [gebruik Hallo Vertex Execution View in Data Lake Tools voor Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).
