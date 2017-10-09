<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-regular-hotfixes-via-windows-powershell-for-storsimple"></a>tooinstall reguliere hotfixes via Windows PowerShell voor StorSimple
1. Verbinding met het maken van de seriële console van toohello apparaat. Zie voor meer informatie [stap 1: verbinding maken met de seriële console toohello](../articles/storsimple/storsimple-update-device.md#step1).
2. In het menu van de seriële console hello, optie 1, **aanmelden met volledige toegang**. Type Hallo wachtwoord. is het standaardwachtwoord Hallo **Wachtwoord1**.
3. Typ het volgende achter de opdrachtprompt Hallo:
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > Met deze opdracht worden alleen tooregular hotfixes toegepast. U deze opdracht uitvoert op slechts één domeincontroller, maar beide domeincontrollers wordt bijgewerkt.
    > Merkt u wellicht een failover van de domeincontroller tijdens het updateproces Hallo; echter, Hallo failover niet van invloed op beschikbaarheid van het systeem of de bewerking.

4. Als u wordt gevraagd, geeft u Hallo pad toohello gedeelde netwerkmap waarin Hallo hotfix-bestanden.
5. U wordt gevraagd om bevestiging. Type **Y** tooproceed Hallo hotfix-installatie.

