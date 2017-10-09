<!--author=SharS last changed: 11/18/16-->

#### <a name="tooinstall-regular-updates-via-windows-powershell-for-storsimple"></a>tooinstall regelmatig updates via Windows PowerShell voor StorSimple
1. Open Hallo apparaat seriële console en selecteer optie 1, **aanmelden met volledige toegang**. Type Hallo wachtwoord. is het standaardwachtwoord Hallo *Wachtwoord1*. 
2. Typ het volgende achter de opdrachtprompt Hallo:
   
     `Get-HcsUpdateAvailability`
   
    U wordt gewaarschuwd als er updates beschikbaar zijn en of de Hallo-updates zijn verstoren of ononderbroken.
3. Typ het volgende achter de opdrachtprompt Hallo:
   
     `Start-HcsUpdate`
   
    Hallo-updateproces wordt gestart.

> [!IMPORTANT]
> * Met deze opdracht geldt alleen tooregular updates. U deze opdracht uitvoert op slechts één domeincontroller, maar beide domeincontrollers wordt bijgewerkt. 
> * Merkt u wellicht een failover van de domeincontroller tijdens het updateproces Hallo; echter, Hallo failover niet van invloed op beschikbaarheid van het systeem of de bewerking.
> 
> 

