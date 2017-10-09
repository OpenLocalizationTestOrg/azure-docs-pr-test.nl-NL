<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-hotfixes-via-windows-powershell-for-storsimple"></a>tooinstall onderhoud modus hotfixes via Windows PowerShell voor StorSimple
> [!IMPORTANT]
> In de onderhoudsmodus, tooapply Hallo hotfix eerst op één domeincontroller moet en klik vervolgens op Hallo andere domeincontroller.
> 
> 

1. Hallo-apparaat in de onderhoudsmodus plaatsen. Zie [stap 2: Voer onderhoudsmodus](../articles/storsimple/storsimple-update-device.md#step2) voor instructies over het tooenter-onderhoudsmodus.
2. tooapply hello hotfix, type:
   
     `Start-HcsHotfix` 
3. Als u wordt gevraagd, geeft u Hallo pad toohello gedeelde netwerkmap waarin Hallo hotfix-bestanden.
4. U wordt gevraagd om bevestiging. Type **Y** tooproceed Hallo hotfix-installatie.
5. Nadat u hebt toegepast Hallo hotfix op een domeincontroller, aanmelden toohello andere domeincontroller. Hallo hotfix toepassen als bij eerdere Hallo-controller.
6. Nadat Hallo hotfixes worden toegepast, sluit u de onderhoudsmodus. Zie [stap 4: afsluiten onderhoudsmodus](../articles/storsimple/storsimple-update-device.md#step4) voor instructies.

