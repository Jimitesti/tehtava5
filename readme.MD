# H5 Uusi komento

## a) Hei komento! Tee järjestelmään uusi "hei maailma" -komento ja asenna se orjille Saltilla. Liitä raporttiisi 'ls -l /usr/local/bin/' tulosteesta ainakin se rivi, jolla näkyy uuden komentotiedostosi oikeudet. Vinkkejä: tee shell script, joka tulostaa "hei maailma". Kokeile ensin käsin, sitten automatisoi. Luonteva paikka paketinhalllinnan ulkopuolelta asennetuille ohjelmille on /usr/local/bin/. Katso myös 'salt-call --local sys.state_doc file.managed'. Muista (aina ja kaikessa mitä teet tietokoneella) testata lopputulos. Hyvä testi on mahdollisimman lähellä sitä, mitä käyttäjä tekisi.
Aloitin tekemällä salt-kansioon (/srv/salt) uuden kansion nimeltä "heimaailma" ja sinne init.sls state tiedoston. Tein myös samaan kansioon yksinkertaisen shell skriptin nimeltä "heimaailma.sh", jonka ainoa komento on näyttää teksti "Hei maailma!".
Hakemiston rakenne näyttää nyt seuraavalta:

![hakemistorakenne]()

Tämän jälkeen ajoin salt-tilan "heimaailma", joka näytti että oikeudet olisivat 644, joten käyttäjillä ei ollut oikeuksia ajaa ohjelmaa.

		$ sudo salt '*' state.apply heimaailma

![eioikeuksia]()

Joten kävin korjaamassa oikeudet lisäämällä salt-tiedostoon komennon - mode, joka muokkaa kopioidun tiedoston oikeuksia.

![korjatutoikeudet]()

Ja ajoin salt-tilan uudestaan komennolla

		$ sudo salt '*' state.apply heimaailma

![korjatutoikeudet2]()

![ubuntuoikeudet]()
Tämän jälkee homma pelitti niinkuin pitää ja toimi toisella virtuaalikoneella.

![toimivaheimaailma]()

## b) whatsup.sh. Tee järjestelmään uusi komento, joka kertoo ajankohtaisia tietoja; asenna se orjille. Vinkkejä: Voit näyttää valintasi mukaan esimerkiksi päivämäärää, säätä, tietoja koneesta, verkon tilanteesta...

Aloitin tämän vaiheen tekemällä salt-hakemistoon (/srv/salt) uuden hakemiston nimeltä whatsup ja sinne tyypillisen init.sls state-tiedoston. Samaan hakemistoon myös skriptin whatsup.sh, jonka aion kopioida state-tiedoston kautta muille koneille.

Hakemisto siis näyttää seuraavalta:

![whatsuphakemisto]()

Seuraavaksi kirjoitin skriptin, joka näyttää joitain tietokoneen tietoja ja lopuksi ajan ja päivämäärän.

![whatsupskripti]()

Jonka jälkeen kirjoittelin init.sls state-tiedoston joka kopioi skriptin orjan /usr/local/bin/ hakemistoon ja ajaa sen samalla cmd.run komennolla.

![whatsupstate]()

![whatsupecho]()

## c) hello.py. Tee järjestelmään uusi komento Pythonilla ja asenna se orjille. Vinkkejä: Hei maailma riittää, mutta propellihatut saavat toki koodaillakin. Shebang on "#!/usr/bin/python3". Helpoin Python-komento on: print("Hei Tero!")

Aloitin taas samalla tavalla kuin aikasemmat kaksi tehtävää ja tein uuden kansion salt-kansioon (/srv/salt) nimeltä python, sinne init.sls state-tiedosto ja test.py python skriptin.

![pythonstate]()

![pythonskripti]()

Ensiksi state-tiedosto tarkistaa että python3 on asennettu, sitten siirtää skriptin /usr/local/bin hakemistoon nimellä "testiskripti" ja muuttaa oikeudet kaikille ajettavaksi, jonka jälkeen ajaa skriptin.

![pythonoutput]()

![pythonoutput2]()

## d) Laiskaa skriptailua. Tee kansio, josta jokainen skripti kopioituu orjille. Vinkki: 'salt-call --local sys.state_doc file.recurse'. Kun tämä on valmis, on todella helppoa laittaa orjille mikä tahansa yhden tiedoston shell script, Python-ohjelma, Perl-ohjelma, Go-binääri tai muu yhden binäärin ohjelma.

Aloitin tämän tehtävän tekemällä salt-hakemistoon kansion nimeltä scripts (/srv/salt/scripts/) sinne init.sls tiedoston ja kopioin käsin kaikki muut skriptit muista kansioista tähän kansioon.

		$ sudo cp -r /srv/salt/*/*.sh /srv/salt/skriptit | sudo cp -r /srv/salt/*/*.py /srv/salt/skriptit

## e) Intel. Etsi kolme loppuprojektia joltain vanhalta kurssitoteutukselta. Kuvaile projektit tiiviisti ja linkitä alkuperäiseeen raporttin. Vinkkejä: Loppuprojekteja löydät etsimällä opiskelijoiden raportteja vanhoilta kursseilta ja selailemalla sivuja, joilta ne löytyivät. Raportteja löytyy vanhojen kurssitotetusten kommenteista. Ja tietysti kannattaa silmäillä listaa sieltä täältä, niin näet eri projektit kuin muut. Voi hakea myös Googlella ja DuckDuckGolla.

## f) Lukua, ei luottamusta. Kokeile yhtä kohdassa e-Intel löytämääsi modulia koneella. Tämä on infraa koodina, joten luottamusta ei tarvita. Voit lukea koodista, mitä olet ajamassa.