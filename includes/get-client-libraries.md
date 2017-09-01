### <a name="install-via-composer"></a>Installeren via de Composer
1. [Installeer Git][install-git]. Houd er rekening mee dat in Windows, u ook het Git uitvoerbare bestand aan de omgevingsvariabele PATH toevoegen moet. 
2. Maak een bestand met de naam **composer.json** in de hoofdmap van uw project en voeg de volgende code toe:
   
    ```json
    {
      "require": {
        "microsoft/windowsazure": "^0.4"
      }
    }
    ```
3. Download  **[composer.phar] [ composer-phar]**  in de hoofdmap van uw project.
4. Open een opdrachtprompt en voer de volgende opdracht in de hoofdmap van uw project
   
    ```
    php composer.phar install
    ```

[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[download-SDK-PHP]: ../articles/php-download-sdk.md
[composer-phar]: http://getcomposer.org/composer.phar
