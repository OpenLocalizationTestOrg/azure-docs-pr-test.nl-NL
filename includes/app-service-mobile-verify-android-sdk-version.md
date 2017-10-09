Vanwege de verdere ontwikkeling Hallo Android SDK versie geïnstalleerd in Android Studio mogelijk niet overeenkomt met Hallo in Hallo-code. Hallo Android SDK, waarnaar wordt verwezen in deze zelfstudie is versie 23, Hallo recente op Hallo moment van schrijven. Hallo versienummer kan verhogen als nieuwe versies van Hallo SDK worden weergegeven en kunt het beste Hallo laatst beschikbare versie gebruikt.

Er zijn twee symptomen van versie komt niet overeen:

- Wanneer u bouwen of Hallo-project te bouwen, mogelijk dat u de foutberichten Gradle zoals '**mislukt toofind doel Google Inc.:Google APIs:n**'.
- Standaard Android objecten in de code die moet worden omgezet op basis van `import` instructies foutberichten kunnen genereren.

Als een van beide wordt weergegeven, Hallo-versie van Android SDK geïnstalleerd in Android Studio Hallo mogelijk niet overeen met Hallo SDK doel van project Hallo gedownload. tooverify hello versie, Hallo volgende wijzigingen aanbrengen:

1. Klik in Android Studio **extra** > **Android** > **SDK Manager**. Als u de meest recente versie Hallo Hallo SDK Platform niet hebt geïnstalleerd, klikt u op tooinstall deze. Noteer Hallo versienummer.
2. Op Hallo **Projectverkenner** tabblad onder **Gradle Scripts**Open Hallo bestand **build.gradle (modeule: app)**. Zorg ervoor dat Hallo **compileSdkVersion** en **buildToolsVersion** toohello nieuwste SDK versie geïnstalleerd zijn ingesteld. Hallo labels uitzien als volgt:

             compileSdkVersion 'Google Inc.:Google APIs:23'
            buildToolsVersion "23.0.2"
3. Kies in Android Studio Project Explorer, klik met de rechtermuisknop Hallo projectknooppunt Hallo **eigenschappen**, en kies in de linkerkolom Hallo **Android**. Zorg ervoor dat Hallo **doel van de Projectbuild** toohello is ingesteld dezelfde SDK versie als Hallo **targetSdkVersion**.

In Android Studio Hallo manifestbestand is niet langer gebruikt toospecify Hallo doel SDK en de minimale SDK-versie, in tegenstelling tot Hallo geval met Eclipse.
