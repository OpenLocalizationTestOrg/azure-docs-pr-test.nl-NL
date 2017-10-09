
1. In Visual Studio Solution Explorer met de rechtermuisknop op Hallo Windows Store-app-project en klik op **Store** > **App koppelen Hello Store**.

    ![App aan Windows Store koppelen](./media/app-service-mobile-register-wns/notification-hub-associate-win8-app.png)
2. Klik in de wizard Hallo op **volgende**, en meld u aan met uw Microsoft-account. Typ een naam voor uw app in **een nieuwe appnaam reserveren**, en klik vervolgens op **Reserve**.
3. Klik na registratie van de app Hallo Hallo is gemaakt, selecteer nieuwe app-naam **volgende**, en klik vervolgens op **koppelen**. Hallo vereist Windows Store-registratie informatie toohello toepassingsmanifest wordt toegevoegd.
4. Herhaal stap 1 en 3 voor Hallo Windows Phone Store-app-project met behulp van dezelfde registratie die u eerder hebt gemaakt voor de Windows Store-app Hallo Hallo.  
5. Blader toohello [Windows-ontwikkelaarscentrum](https://dev.windows.com/en-us/overview), en meld u aan met uw Microsoft-account. Klik op de nieuwe app-registratie Hallo in **mijn apps**, en vouw vervolgens **Services** > **Pushmeldingen**.
6. Op Hallo **Pushmeldingen** pagina, klikt u op **Live Services site** onder **Windows Push Notification Services (WNS) en Microsoft Azure Mobile Apps**. Maak een notitie van waarden van Hallo Hallo **pakket-SID** en Hallo *huidige* waarde in **Toepassingsgeheim**. 

    ![App-instelling in Hallo developer center](./media/app-service-mobile-register-wns/mobile-services-win8-app-push-auth.png)

   > [!IMPORTANT]
   > Hallo toepassingsgeheim en pakket-SID zijn belangrijke beveiligingsreferenties. Deel deze waarden met niemand en distribueer ze niet met uw app.
   >
   >
