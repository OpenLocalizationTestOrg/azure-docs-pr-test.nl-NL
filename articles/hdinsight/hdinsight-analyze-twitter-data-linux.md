---
title: aaaAnalyze Twitter-gegevens met Apache Hive - Azure HDInsight | Microsoft Docs
description: Informatie over hoe toouse gebruik Hive en Hadoop op HDInsight tootransform onbewerkte TWitter-gegevens in een doorzoekbare Hive-tabel.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1e249ed-5f57-40d6-b3bc-a1b4d9a871d3
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 02c4d027c7bbf390ac1c3724c14f8d549ea5195e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-and-hadoop-on-hdinsight"></a>Twitter-gegevens met Hive en Hadoop op HDInsight analyseren

Meer informatie over hoe toouse Apache Hive tooprocess Twitter-gegevens. Hallo-resultaat is een lijst met Twitter-gebruikers die verzonden hello meeste tweets die een bepaald woord bevatten.

> [!IMPORTANT]
> Hallo stappen in dit document zijn getest op HDInsight 3.6.
>
> Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

## <a name="get-hello-data"></a>Hallo-gegevens ophalen

Twitter, kunt u tooretrieve hello [gegevens voor elke tweet](https://dev.twitter.com/docs/platform-objects/tweets) als een document notatie JSON (JavaScript Object) via een REST-API. [OAuth](http://oauth.net) is vereist voor verificatie toohello API.

### <a name="create-a-twitter-application"></a>Een Twitter-toepassing maken

1. Vanuit een webbrowser, meld u aan te[https://apps.twitter.com/](https://apps.twitter.com/). Klik op Hallo **nu aanmelden** koppelen als u een Twitter-account niet hebt.

2. Klik op **nieuwe App maken**.

3. Voer **naam**, **beschrijving**, **Website**. U kunt een URL voor Hallo gezamenlijk **Website** veld. Hallo volgende tabel ziet u enkele waarden voorbeeld toouse:

   | Veld | Waarde |
   |:--- |:--- |
   | Naam |MyHDInsightApp |
   | Beschrijving |MyHDInsightApp |
   | Website |http://www.myhdinsightapp.com |

4. Controleer **Ja, ik ga akkoord**, en klik vervolgens op **uw Twitter-toepassing maken**.

5. Klik op Hallo **machtigingen** tabblad Hallo standaardmachtiging **alleen-lezen**.

6. Klik op Hallo **sleutels en toegangstokens** tabblad.

7. Klik op **maken van mijn toegangstoken**.

8. Klik op **Test OAuth** in Hallo rechterbovenhoek van Hallo pagina.

9. Noteer **consumentsleutel**, **consumentgeheim**, **toegangstoken**, en **Access token geheim**.

### <a name="download-tweets"></a>Tweets downloaden

Hallo Python code na 10.000 tweets downloads van Twitter en sla ze tooa-bestand met de naam **tweets.txt**.

> [!NOTE]
> Hallo stappen worden uitgevoerd op Hallo van HDInsight-cluster, omdat Python al is geïnstalleerd.

1. Verbinding maken met toohello HDInsight-cluster via SSH:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

3. Gebruik Hallo deze opdrachten tooinstall [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2), en andere vereiste pakketten:

   ```bash
   sudo apt install python-dev libffi-dev libssl-dev
   sudo apt remove python-openssl
   pip install virtualenv
   mkdir gettweets
   cd gettweets
   virtualenv gettweets
   source gettweets/bin/activate
   pip install tweepy progressbar pyOpenSSL requests[security]
   ```

4. Gebruik Hallo volgende opdracht toocreate uit een bestand met de naam **gettweets.py**:

   ```bash
   nano gettweets.py
   ```

5. Gebruik Hallo na de tekst hello inhoud Hallo **gettweets.py** bestand:

   ```python
   #!/usr/bin/python

   from tweepy import Stream, OAuthHandler
   from tweepy.streaming import StreamListener
   from progressbar import ProgressBar, Percentage, Bar
   import json
   import sys

   #Twitter app information
   consumer_secret='Your consumer secret'
   consumer_key='Your consumer key'
   access_token='Your access token'
   access_token_secret='Your access token secret'

   #hello number of tweets we want tooget
   max_tweets=10000

   #Create hello listener class that receives and saves tweets
   class listener(StreamListener):
       #On init, set hello counter toozero and create a progress bar
       def __init__(self, api=None):
           self.num_tweets = 0
           self.pbar = ProgressBar(widgets=[Percentage(), Bar()], maxval=max_tweets).start()

       #When data is received, do this
       def on_data(self, data):
           #Append hello tweet toohello 'tweets.txt' file
           with open('tweets.txt', 'a') as tweet_file:
               tweet_file.write(data)
               #Increment hello number of tweets
               self.num_tweets += 1
               #Check toosee if we have hit max_tweets and exit if so
               if self.num_tweets >= max_tweets:
                   self.pbar.finish()
                   sys.exit(0)
               else:
                   #increment hello progress bar
                   self.pbar.update(self.num_tweets)
           return True

       #Handle any errors that may occur
       def on_error(self, status):
           print status

   #Get hello OAuth token
   auth = OAuthHandler(consumer_key, consumer_secret)
   auth.set_access_token(access_token, access_token_secret)
   #Use hello listener class for stream processing
   twitterStream = Stream(auth, listener())
   #Filter for these topics
   twitterStream.filter(track=["azure","cloud","hdinsight"])
   ```

    > [!IMPORTANT]
    > Vervang Hallo tijdelijke aanduiding voor de volgende items met Hallo-informatie van uw toepassing twitter Hallo:
    >
    > * `consumer_secret`
    > * `consumer_key`
    > * `access_token`
    > * `access_token_secret`

6. Gebruik **Ctrl + X**, klikt u vervolgens **Y** toosave Hallo-bestand.

7. Gebruik Hallo opdrachtbestand toorun hello te volgen en tweets downloaden:

    ```bash
    python gettweets.py
    ```

    Er verschijnt een voortgangsindicator. Deze telt too100% als Hallo tweets worden gedownload.

   > [!NOTE]
   > Als dit Hallo voortgang balk tooadvance lang duurt, wijzigt u Hallo filter tootrack trends onderwerpen. Wanneer er veel tweets over Hallo onderwerp in het filter, kunt u snel ophalen Hallo 10000 tweets nodig.

### <a name="upload-hello-data"></a>Hallo gegevens uploaden

tooupload hello tooHDInsight gegevensopslag, gebruik Hallo volgende opdrachten:

   ```bash
   hdfs dfs -mkdir -p /tutorials/twitter/data
   hdfs dfs -put tweets.txt /tutorials/twitter/data/tweets.txt
```

Hallo-gegevens opslaan deze opdrachten in een locatie die voor alle knooppunten in cluster Hallo toegankelijk.

## <a name="run-hello-hiveql-job"></a>Hallo HiveQL taak uitvoeren

1. Gebruik Hallo opdracht toocreate een bestand met HiveQL-instructies te volgen:

   ```bash
   nano twitter.hql
   ```

    Gebruik Hallo tekst als Hallo inhoud van Hallo-bestand te volgen:

   ```hiveql
   set hive.exec.dynamic.partition = true;
   set hive.exec.dynamic.partition.mode = nonstrict;
   -- Drop table, if it exists
   DROP TABLE tweets_raw;
   -- Create it, pointing toward hello tweets logged from Twitter
   CREATE EXTERNAL TABLE tweets_raw (
       json_response STRING
   )
   STORED AS TEXTFILE LOCATION '/tutorials/twitter/data';
   -- Drop and recreate hello destination table
   DROP TABLE tweets;
   CREATE TABLE tweets
   (
       id BIGINT,
       created_at STRING,
       created_at_date STRING,
       created_at_year STRING,
       created_at_month STRING,
       created_at_day STRING,
       created_at_time STRING,
       in_reply_to_user_id_str STRING,
       text STRING,
       contributors STRING,
       retweeted STRING,
       truncated STRING,
       coordinates STRING,
       source STRING,
       retweet_count INT,
       url STRING,
       hashtags array<STRING>,
       user_mentions array<STRING>,
       first_hashtag STRING,
       first_user_mention STRING,
       screen_name STRING,
       name STRING,
       followers_count INT,
       listed_count INT,
       friends_count INT,
       lang STRING,
       user_location STRING,
       time_zone STRING,
       profile_image_url STRING,
       json_response STRING
   );
   -- Select tweets from hello imported data, parse hello JSON,
   -- and insert into hello tweets table
   FROM tweets_raw
   INSERT OVERWRITE TABLE tweets
   SELECT
       cast(get_json_object(json_response, '$.id_str') as BIGINT),
       get_json_object(json_response, '$.created_at'),
       concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
       substr (get_json_object(json_response, '$.created_at'),27,4)),
       substr (get_json_object(json_response, '$.created_at'),27,4),
       case substr (get_json_object(json_response,    '$.created_at'),5,3)
           when "Jan" then "01"
           when "Feb" then "02"
           when "Mar" then "03"
           when "Apr" then "04"
           when "May" then "05"
           when "Jun" then "06"
           when "Jul" then "07"
           when "Aug" then "08"
           when "Sep" then "09"
           when "Oct" then "10"
           when "Nov" then "11"
           when "Dec" then "12" end,
       substr (get_json_object(json_response, '$.created_at'),9,2),
       substr (get_json_object(json_response, '$.created_at'),12,8),
       get_json_object(json_response, '$.in_reply_to_user_id_str'),
       get_json_object(json_response, '$.text'),
       get_json_object(json_response, '$.contributors'),
       get_json_object(json_response, '$.retweeted'),
       get_json_object(json_response, '$.truncated'),
       get_json_object(json_response, '$.coordinates'),
       get_json_object(json_response, '$.source'),
       cast (get_json_object(json_response, '$.retweet_count') as INT),
       get_json_object(json_response, '$.entities.display_url'),
       array(
           trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[1].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[2].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[3].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[4].text')))),
       array(
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[1].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[2].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[3].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[4].screen_name')))),
       trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
       trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
       get_json_object(json_response, '$.user.screen_name'),
       get_json_object(json_response, '$.user.name'),
       cast (get_json_object(json_response, '$.user.followers_count') as INT),
       cast (get_json_object(json_response, '$.user.listed_count') as INT),
       cast (get_json_object(json_response, '$.user.friends_count') as INT),
       get_json_object(json_response, '$.user.lang'),
       get_json_object(json_response, '$.user.location'),
       get_json_object(json_response, '$.user.time_zone'),
       get_json_object(json_response, '$.user.profile_image_url'),
       json_response
   WHERE (length(json_response) > 500);
   ```

2. Druk op **Ctrl + X**, drukt u vervolgens op **Y** toosave Hallo-bestand.
3. Hallo opdracht toorun hello die hiveql in Hallo-bestand aanwezige volgende gebruiken:

   ```bash
   beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i twitter.hql
   ```

    Met deze opdracht wordt uitgevoerd Hallo Hallo **twitter.hql** bestand. Zodra het Hallo-query is voltooid, ziet u een `jdbc:hive2//localhost:10001/>` prompt.

4. Gebruik vanaf Hallo beeline prompt Hallo na query tooverify dat de gegevens zijn geïmporteerd:

   ```hiveql
   SELECT name, screen_name, count(1) as cc
       FROM tweets
       WHERE text like "%Azure%"
       GROUP BY name,screen_name
       ORDER BY cc DESC LIMIT 10;
   ```

    Deze query retourneert maximaal 10 tweets waarin Hallo woord **Azure** in Hallo berichttekst.

## <a name="next-steps"></a>Volgende stappen

U hebt geleerd hoe tootransform een niet-gestructureerde JSON-gegevensset naar een gestructureerde Hive-tabel. toolearn meer informatie over Hive in HDInsight, Zie Hallo documenten te volgen:

* [Aan de slag met HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Vertraging vluchtgegevens met HDInsight analyseren](hdinsight-analyze-flight-delay-data-linux.md)

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter
