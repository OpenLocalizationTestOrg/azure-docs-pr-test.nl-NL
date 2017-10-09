<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a>tooinstall onderhoud modus updates via Windows PowerShell voor StorSimple
1. Als u dit nog niet hebt gedaan, toegang tot Hallo apparaat seriële console en selecteer optie 1, **aanmelden met volledige toegang**. 
2. Type Hallo wachtwoord. is het standaardwachtwoord Hallo **Wachtwoord1**.
3. Typ het volgende achter de opdrachtprompt Hallo:
   
     `Get-HcsUpdateAvailability` 
4. U wordt gewaarschuwd als er updates beschikbaar zijn en of de Hallo-updates zijn verstoren of ononderbroken. tooapply verstoren updates, moet u tooput Hallo apparaat in de onderhoudsmodus. Zie [stap 2: Voer onderhoudsmodus](../articles/storsimple/storsimple-update-device.md#step2) voor instructies.
5. Wanneer het apparaat in de onderhoudsmodus is, bij de opdrachtprompt hello, typt u:`Start-HcsUpdate`
6. U wordt gevraagd om bevestiging. Nadat u Hallo updates bevestigt, zullen ze worden geïnstalleerd op Hallo-domeincontroller die u momenteel gebruikmaken van. Nadat het Hallo-updates worden geïnstalleerd, kunnen Hallo-controller wordt opnieuw gestart. 
7. Hallo-status van de updates bewaken. Type:
   
    `Get-HcsUpdateStatus`
   
    Als hello `RunInProgress` is `True`, Hallo wordt nog steeds bijgewerkt. Als `RunInProgress` is `False`, betekent dit dat Hallo-update is voltooid.  
8. Wanneer Hallo-update is geïnstalleerd op de huidige controller Hallo en opnieuw is opgestart, verbinding toohello andere domeincontrollers en stappen 1 tot en met 6 uitvoeren.
9. Nadat beide domeincontrollers zijn bijgewerkt, sluit u de onderhoudsmodus. Zie [stap 4: afsluiten onderhoudsmodus](../articles/storsimple/storsimple-update-device.md#step4) voor instructies.

