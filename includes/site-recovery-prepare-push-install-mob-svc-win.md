### <a name="prepare-for-a-push-installation-on-a-windows-computer"></a>Voorbereiden voor een pushinstallatie op een Windows-computer

1. Zorg ervoor dat er netwerkverbinding tussen Hallo Windows-computer en de processerver Hallo is.
2. Maak een account dat processerver Hallo tooaccess Hallo computer kunt gebruiken. Hallo-account moet administrator-rechten (lokaal of domeinbeheerder) hebben. (Gebruik dit account alleen voor Hallo push-installatie en agentupdates.)

   > [!NOTE]
   > Als u niet een domeinaccount, moet u externe toegang van de gebruiker besturingselement op de lokale computer Hallo uitschakelen. toodisable externe gebruiker toegangsbeheer, onder registersleutel Hallo HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System, Voeg een nieuwe DWORD: **LocalAccountTokenFilterPolicy**. Hallo-waarde te instellen**1**. toodo dit op een opdracht vragen Hallo volgende opdracht uitvoeren:  
   `REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`
   >
   >
2. In Windows Firewall op de computer Hallo gewenste tooprotect, selecteer **toestaan van een app of functie via Firewall**. Schakel **bestands- en printerdeling** en **Windows Management Instrumentation (WMI)**. Voor computers die deel uitmaken van tooa domein, kunt u Hallo firewall-instellingen configureren met behulp van een groepsbeleidsobject (GPO).

   ![Firewallinstellingen](./media/site-recovery-prepare-push-install-mob-svc-win/mobility1.png)

3. Hallo-account die u hebt gemaakt in CSPSConfigtool toevoegen.
    1.  Meld u aan de configuratieserver tooyour.
    2.  Open **cspsconfigtool.exe**. (Dit is beschikbaar als een snelkoppeling op Hallo bureaublad en in Hallo %ProgramData%\home\svsystems\bin map).
    3.  Op Hallo **Accounts beheren** tabblad **Account toevoegen**.
    4.  U hebt gemaakt Hallo-account toevoegen.
    5.  Geef referenties op Hallo die u gebruiken wanneer u replicatie voor een computer inschakelen.
