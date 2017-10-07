---
title: Starten van de taken in Azure Cloud Services aaaRun | Microsoft Docs
description: Starten van de taken helpen bij het voorbereiden van uw cloud service-omgeving voor uw app. Dit leert u hoe het starten van de taken werken en hoe toomake ze
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 886939be-4b5b-49cc-9a6e-2172e3c133e9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 3391a5d7434164f59972b8e497e5c34e33409543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-and-run-startup-tasks-for-a-cloud-service"></a>Hoe tooconfigure en voer opstarten taken voor een cloudservice
U kunt opstarten taken tooperform operations voordat een rol wordt gestart. Wilt u misschien tooperform bewerkingen bevatten een onderdeel te installeren, het registreren van COM-onderdelen, registersleutels instellen of starten van een langdurige proces.

> [!NOTE]
> Starten van de taken zijn niet van toepassing tooVirtual Machines, alleen tooCloud Service-Web- en werkrollen.
> 
> 

## <a name="how-startup-tasks-work"></a>De werking van de taken starten
Starten van de taken zijn acties die worden uitgevoerd voordat uw rollen beginnen en zijn gedefinieerd in Hallo [ServiceDefinition.csdef] bestand met behulp van Hallo [taak] element in Hallo [opstarten]element. Starten van de taken zijn vaak batch-bestanden, maar ze kunnen ook worden consoletoepassingen of batch-bestanden die PowerShell-scripts starten.

Omgevingsvariabelen informatie doorgeven in een taak starten en lokale opslag kan gegevens uit een taak starten van de gebruikte toopass. Bijvoorbeeld een omgevingsvariabele Hallo pad tooa programma kunt opgeven dat u wilt dat tooinstall en bestanden kunnen worden geschreven toolocal opslag die vervolgens door uw rollen later kan worden gelezen.

Het starten van de taak kan zich aanmelden informatie en fouten toohello map die is opgegeven door Hallo **TEMP** omgevingsvariabele. Hallo tijdens Hallo starten van de taak **TEMP** omgevingsvariabele wordt omgezet toohello *C:\\Resources\\temp\\[guid]. [ rolename]\\RoleTemp* directory wanneer u gebruikmaakt van Hallo cloud.

Starten van de taken kunnen ook worden uitgevoerd meerdere keren opnieuw wordt gestart. Bijvoorbeeld Hallo starten van de taak wordt uitgevoerd telkens Hallo-rol wordt gerecycled en rol recyclet mogelijk opnieuw opstarten geen altijd opgenomen. Starten van de taken worden op een manier die ze toorun meerdere keren zonder problemen kan geschreven.

Starten van de taken moeten eindigen met een **errorlevel** (of afsluitcode) van nul voor Hallo opstarten proces toocomplete. Als een taak starten met een niet-nul eindigt **errorlevel**, Hallo-rol kan niet worden gestart.

## <a name="role-startup-order"></a>De opstartvolgorde rol
Hallo lijsten Hallo rol starten van de procedure in Azure te volgen:

1. Hallo-exemplaar is gemarkeerd als **starten** en ontvangt geen verkeer.
2. Alle starten van de taken worden uitgevoerd op basis van tootheir **taskType** kenmerk.
   
   * Hallo **eenvoudige** taken worden uitgevoerd, synchroon, één voor één.
   * Hallo **achtergrond** en **voorgrond** taken zijn gestart asynchroon, parallelle toohello starten van de taak.  
     
     > [!WARNING]
     > IIS mogelijk niet volledig geconfigureerd tijdens het Hallo starten van de taak in het opstartproces hello, zodat rolspecifieke gegevens mogelijk niet beschikbaar. Starten van de taken waarvoor rolspecifieke gegevens moeten gebruiken [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).
     > 
     > 
3. hostproces Hallo-rol is gestart en Hallo site is gemaakt in IIS.
4. Hallo [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) methode wordt aangeroepen.
5. Hallo-exemplaar is gemarkeerd als **gereed** en verkeer wordt gerouteerd toohello exemplaar.
6. Hallo [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode wordt aangeroepen.

## <a name="example-of-a-startup-task"></a>Voorbeeld van een taak starten
Starten van de taken zijn gedefinieerd in Hallo [ServiceDefinition.csdef] bestand in Hallo **taak** element. Hallo **commandLine** kenmerk geeft Hallo naam en parameters van Hallo starten van de batch-bestand of console opdracht hello **executionContext** kenmerk geeft machtigingsniveau Hallo Hallo opstarten taak en Hallo **taskType** kenmerk geeft aan hoe Hallo-taak wordt uitgevoerd.

In dit voorbeeld wordt een omgevingsvariabele **MyVersionNumber**, is gemaakt voor Hallo starten van de taak en stel toohello waarde '**1.0.0.0**'.

**ServiceDefinition.csdef**:

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

Hallo in Hallo voorbeeld te volgen, **Startup.cmd** batchbestand schrijft Hallo regel 'hello huidige versie is 1.0.0.0' toohello StartupLog.txt bestand in de opgegeven door de omgevingsvariabele TEMP Hallo Hallo-map. Hallo `EXIT /B 0` regel zorgt ervoor dat opstarttaak Hallo eindigt met een **errorlevel** gelijk is aan nul.

```cmd
ECHO hello current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> In Visual Studio Hallo **tooOutput Directory kopiëren** eigenschap voor het starten van de batch-bestand te moet worden ingesteld**kopie altijd** toobe of het starten van de batch-bestand is juist geïmplementeerd tooyour project op Azure (**approot\\bin** voor Web-rollen en **approot** voor werkrollen).
> 
> 

## <a name="description-of-task-attributes"></a>Beschrijving van de kenmerken van de taak
Hallo hieronder wordt beschreven Hallo kenmerken van Hallo **taak** -element in Hallo [ServiceDefinition.csdef] bestand:

**commandLine** -Hiermee geeft u de opdrachtregel Hallo voor Hallo starten van de taak:

* Hallo opdracht met optionele opdrachtregelparameters Hallo starten van de taak wordt gestart.
* Dit is vaak Hallo-bestandsnaam van een batchbestand .cmd of .bat.
* Hallo-taak is relatief toohello AppRoot\\Bin-map voor Hallo-implementatie. Omgevingsvariabelen zijn niet bij het bepalen van Hallo pad en de bestandsnaam van de taak Hallo uitgevouwen. Als uitbreiding van de omgeving vereist is, kunt u een kleine CMD-script waarmee het starten van de taak wordt aangeroepen.
* Kan dit een consoletoepassing of een batchbestand dat begint een [PowerShell-script](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).

**executionContext** -Hiermee geeft u op Hallo machtigingsniveau voor Hallo starten van de taak. Hallo machtigingsniveau kan worden beperkt of met verhoogde bevoegdheden:

* **beperkt**  
  Hallo starten van de taak wordt uitgevoerd met dezelfde als Hallo rol toegangsrechten Hallo. Wanneer Hallo **executionContext** kenmerk voor Hallo [Runtime] element is ook **beperkt**, en vervolgens de gebruiker heeft bevoegdheden die worden gebruikt.
* **verhoogde**  
  Hallo starten van de taak wordt uitgevoerd met administrator-bevoegdheden. Zo kunnen opstarttaken tooinstall programma, IIS-configuratiewijzigingen aanbrengen, wijzigingen in het register en andere taken van de administrator-niveau uitvoeren zonder te verhogen machtigingsniveau Hallo van Hallo rol zelf.  

> [!NOTE]
> Hallo machtigingsniveau van een taak starten hoeft niet toobe Hallo dezelfde als Hallo rol zelf.
> 
> 

**taskType** -Hiermee geeft u op Hallo manier een starten van de taak wordt uitgevoerd.

* **eenvoudige**  
  Taken worden uitgevoerd synchroon, één voor één, in volgorde van Hallo opgegeven in Hallo [ServiceDefinition.csdef] bestand. Wanneer een **eenvoudige** opstarttaak eindigt met een **errorlevel** is aan nul, Hallo naast **eenvoudige** starten van de taak wordt uitgevoerd. Als er niet meer **eenvoudige** opstarten tooexecute, taken en vervolgens het Hallo-rol zelf wordt gestart.   
  
  > [!NOTE]
  > Als hello **eenvoudige** taak eindigt met een niet-nul **errorlevel**, Hallo-exemplaar wordt geblokkeerd. Daaropvolgende **eenvoudige** starten van de taken en Hallo rol zelf, kunnen niet worden gestart.
  > 
  > 
  
    tooensure dat uw batchbestand met eindigt een **errorlevel** is aan nul, Hallo-opdracht uitvoeren `EXIT /B 0` aan Hallo einde van uw batch-bestand.
* **achtergrond**  
  Taken worden asynchroon uitgevoerd parallel met Hallo opstarten van Hallo-rol.
* **voorgrond**  
  Taken worden asynchroon uitgevoerd parallel met Hallo opstarten van Hallo-rol. Hallo belangrijkste verschil tussen een **voorgrond** en een **achtergrond** taak is dat een **voorgrond** taak voorkomt dat Hallo-functie uit de recycling of totdat het Hallo-taak is afgesloten beëindigd. Hallo **achtergrond** taken beschikt niet over deze beperking.

## <a name="environment-variables"></a>Omgevingsvariabelen
Omgevingsvariabelen zijn een manier toopass informatie tooa starten van de taak. U kunt bijvoorbeeld Hallo pad tooa blob met een tooinstall programma of poortnummers die door uw rol wordt gebruikt of instellingen toocontrol functies van uw opstarttaak plaatsen.

Er zijn twee soorten van omgevingsvariabelen voor starten van de taken. statische omgevingsvariabelen en omgevingsvariabelen op basis van de leden van Hallo [ RoleEnvironment] klasse. Beide zijn in Hallo [omgeving] sectie Hallo [ServiceDefinition.csdef] bestands- en beide Hallo gebruik [variabele] element en **naam** kenmerk.

Statische omgeving variabelen gebruikt Hallo **waarde** kenmerk Hallo [variabele] element. Hallo in bovenstaand voorbeeld maakt de omgevingsvariabele Hallo **MyVersionNumber** die een vaste waarde heeft van '**1.0.0.0**'. Een ander voorbeeld is toocreate een **StagingOrProduction** omgevingsvariabele die u handmatig toovalues van instellen kunt '**fasering**"of"**productie**' tooperform starten van de verschillende acties die zijn gebaseerd op Hallo-waarde van Hallo **StagingOrProduction** omgevingsvariabele.

Omgevingsvariabelen op basis van de leden van Hallo RoleEnvironment klasse gebruik geen Hallo **waarde** kenmerk Hallo [variabele] element. In plaats daarvan Hallo [RoleInstanceValue] onderliggend element met de juiste Hallo **XPath** kenmerkwaarde, gebruikte toocreate zijn een omgevingsvariabele op basis van een specifiek lid van Hallo [ RoleEnvironment] klasse. Waarden voor Hallo **XPath** tooaccess kenmerk verschillende [ RoleEnvironment] waarden kunt u vinden [hier](cloud-services-role-config-xpath.md).

Toocreate bijvoorbeeld een omgevingsvariabele die is '**true**' wanneer Hallo-exemplaar wordt uitgevoerd in de rekenemulator hello, en "**false**' wanneer uitgevoerd in de cloud hello, gebruikt u de volgende Hallo [variabele] en [RoleInstanceValue] elementen:

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>

            <!-- Create hello environment variable that informs hello startup task whether it is running
                in hello Compute Emulator or in hello cloud. "%ComputeEmulatorRunning%"=="true" when
                running in hello Compute Emulator, "%ComputeEmulatorRunning%"=="false" when running
                in hello cloud. -->

            <Variable name="ComputeEmulatorRunning">
                <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
            </Variable>

        </Environment>
    </Task>
</Startup>
```

## <a name="next-steps"></a>Volgende stappen
Meer informatie over hoe tooperform sommige [algemene beheertaken voor opstarten](cloud-services-startup-tasks-common.md) met de Cloudservice.

[Pakket](cloud-services-model-and-package.md) uw Cloudservice.  

[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef
[taak]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[opstarten]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[omgeving]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[variabele]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[ RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
