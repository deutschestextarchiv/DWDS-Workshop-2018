layout: true
  
<div class="my-header"></div>

<div class="my-footer">
  <table>
    <tr>
      <td>DWDS &ndash; Digitales Wörterbuch der deutschen Sprache</td>
      <td style="text-align:right"><a href="https://www.dwds.de">www.dwds.de</a></td>
    </tr>
  </table>
</div>

---

class: title-slide

# DWDS &ndash; Digitales Wörterbuch der deutschen Sprache  
## Mittels Computerlinguistik zum Wörterbuch der Zukunft

| Frank Wiegand   | Kay-Michael Würzner |
|:---------------:|:-------------------:|
| [wiegand@bbaw.de](mailto:wiegand@bbaw.de) | [wuerzner@bbaw.de](mailto:wuerzner@bbaw.de) |

---

# Überblick


---

# Was ist Computerlinguistik?

- Teildisziplin der **Sprachwissenschaft**
    + Philologie: Beschäftigung mit den sprachlichen Zeugnissen **einer** Sprache/Sprachfamilie
        * *Germanistik*, *Anglistik*, *Romanistik* etc.
    + Linguistik: Beschäftigung mit **sprachübergreifenden** Phänomenen
        * Ebenen: *Phonologie*, *Morphologie*, *Syntax*, *Semantik* etc.
        * Anwendungsfelder: *Sprachverarbeitung*, *Spracherwerb*, *Sprachstörungen* etc.
- <span style="font-variant:small-caps;">Ferdinand de Saussure</span> (1857&ndash;1913)
    + Begründer des **sprachwissenschaftlichen Strukturalismus**
        * *Langage*: das (biologische) Sprachvermögen
        * *Langue*: Sprache als ein abstraktes System von Regeln
        * *Parole*: Sprechen, konkete Sprachverwendung

---

# Was ist Computerlinguistik?

- Zwei **Teildisziplinen**
    + *Natural Language Processing* (NLP, etwa Linguistische Datenverarbeitung)
        * Verfahren zur automatischen **Analyse** und **Generierung** von Sprache auf allen Ebenen
        * wichtiger Bestandteil unseres medialen Umfelds
    + *Computational Linguistics* (CL, etwa berechenbare, rechenbetonte Sprachwissenschaft)
        * theoretische Beschreibungen der formalen Grundlagen von Sprache
        * Berechenbarkeit, Beweisbarkeit, Modellierung
- <span style="font-variant:small-caps;">Noam Chomsky</span> (&#x2A;1928)
    + Begründer der **generativen Linguistik**
        * *Universalgrammatik*: alle Sprachen folgen gemeinsamen, angeborenen Prinzipien
        * *Tiefen- vs. Oberflächenstruktur*: unterschiedliche Realisierungen gleicher Bedeutungen basieren auf einer gemeinsamen abstrakten Struktur

---

# Das DWDS

- Institution: Berlin-Brandenburgische Akademie der Wissenschaften (BBAW)
- Langzeitvorhaben
- ca. 15 Mitarbeiter/innen
- Wörterbücher, Textsammlungen (Korpora), Tools
- ca. 465 000 Wörterbucheinträge
- ca. 13 Milliarden Textbelege aus über vier Jahrhunderten


- (nur!) online: [https://www.dwds.de](https://www.dwds.de) (seit 2004)

---

# Das DWDS
![DWDS-Webseite](figures/dwds.png)

---

# Vogelperspektive

---

# DWDS: Formteil

http://zwei.dwds.de/wb/Leiter

- Zusammenfassung der **formalen Eigenschaften** eines Wortes:
    + Wortart
    + Eck- (Substantive), Stamm- (Verben) und Komparationsformen (Adjektive)
    + Aussprache
    + Worttrennung (Zeilenende)
    + Wortzerlegung, -bildung
- teils manuell, teils automatisch erhoben

---

# NLP: morphologische Analyse

- Aufgabe
    + Bestimmung der **möglichen** Wortarten eines Wortes
      ```
      grünen ↦ {Verb, Adjektiv}
      Kai    ↦ {Substantiv, Eigenname}
      ```
    + Abbildung auf eine kanonische **Grundform**
      ```
      grünen ↦ grün
      Kais   ↦ Kai
      ```
    + Identifikation der beteiligten Wortbildungsprozesse
      ```
      Grünspan ↦ grün<A>#Span<N>
      verirren ↦ ver<p>+irren<V>
      ```

---

# NLP: morphologische Analyse

- Rezept `Finite State Morphology`:
    + Man nehme
        * eine **große** Liste einfacher Wörter
        * deren **morphosyntaktische** Eigenschaften
        * Vor- und Nachsilben,
    + packe dies in einen **endlichen Automaten** und
    + bilde dessen **kleenesche Hülle**
- <span style="font-variant:small-caps;">Stephen Cole Kleene</span> (1909&ndash;1994)
    + Mitbegründer der theoretischen Informatik
        * formale Sprachen
        * **reguläre Ausdrücke**

---

# NLP: morphologische Analyse

- Illustration
    + Lexikon `{schön<A>,Geist<N>}`
    + Vorsilben `{un<p>,ur<p>}`
    + Nachsilben `{heit<N>,lich<A>}`

---

# NLP: morphologische Analyse

- Zahlen
    + *n* Lexikoneinträge
    + *x* Vorsilben
    + *y* Nachsilben
    + *z* Regeln
    + *i* Zustände
- klassischer **regelbasierter** Ansatz,
    + manuell gepflegte **Daten** als Operanden und
    + manuell erstellte **Regeln** zu deren Kombination
- Grundlage bzw. Bestandteil der meisten Sprachverarbeitungssysteme

http://zwei.dwds.de/?q=Dampfschifffahrtsgesellschaftskapit%C3%A4n&from=wb
http://zwei.dwds.de/?q=Dampfschifffahrtsgesellschaftskapit%C3%A4nsm%C3%BCtze&from=wb

---

# NLP: Worttrennung

- Aufgabe
    + Bestimmung aller möglichen Stellen für die Worttrennung **am Zeilenende**
      ```
      Elektrik ↦ Elek·t·rik ↦ {Elek-trik,Elekt-rik}
      ```
    + nicht zu verwechseln mit **Silbentrennung**
      ```
      Elektrik ↦ E·lek·trik ↦ {E-lek-trik}
      ```
    + Herausforderung durch **Lehnwörter**
      ```
      Ale ↦ Ale ↦ {Ale}
      ```

---

# NLP: Worttrennung

- Rezept `Sequenzklassifizierung`
    + Man nehme
        * eine **sehr große** Liste **manuell annotierter** Daten und
        * einen **Trainingsalgorithmus**,
    + induziere ein **statistisches Modell**,
    + und evaluiere dessen Qualität anhand von **Evaluationsdaten**
- <span style="font-variant:small-caps;">Andrei Andrejewitsch Markow</span> (1856&ndash;1922)
    + wesentliche Beiträge zur **Wahrscheinlichkeitstheorie**
    + arbeitete früh (1913) mit Häufigkeitsanalysen in Textsammlungen
    + formulierten die Grundlagen sog. *Hidden Markov Models*

---

# NLP: Wortrennung

- Illustration

---

# NLP: Wortrennung

- Evaluation
    * ...
- klassischer **statistischer Ansatz**,
    + manuell gepflegte **Daten** als Operanden und
    + **Induktionsverfahren** zu deren Modellierung
- Grundlage heute omnipräsenter Verfahren des *Deep Learning*
- Einsatz in allen Domänen der Sprachverarbeitung

---

# Lexikografische Arbeit

> In keiner Sprache kann man sich so schwer verständigen wie in der Sprache.  
*(Karl Kraus, österr. Schriftsteller, 1874&ndash;1936)*

+ (oft mühevolle) Handarbeit
+ viel Recherche:
    - in anderen Wörterbüchern
    - in Bibliotheken
    - im Internet
    - in Textsammlungen
    - ...
+ Teamsitzungen zur Absprache und Nachfrage

---

# Lexikografische Arbeit

+ *Deutsches Wörterbuch* (DWB), 1838&ndash;1961
    - von <span style="font-variant:small-caps;">Jacob</span> und <span style="font-variant:small-caps;">Wilhelm Grimm</span>
        * Gründungsväter der Germanistik
        * Herausgeber der weltberühmten *Kinder- und Hausmärchen*
    - das größte und umfassendste Wörterbuch zur deutschen Sprache
    - Belegwörterbuch zur Herkunft und zum Gebrauch jedes deutschen Wortes
    - 32 Bände, ca. 320&#x202f;000 Stichwörter, ca. 600&#x202f;000 Belege
    - konsequente Kleinschreibung

---

# Deutsches Wörterbuch (DWB)

![¹DWB](http://dwb.bbaw.de/band1.jpg)

---

# Lexikografische Arbeit

![lexikografischer Arbeitsplatz](http://dwb.bbaw.de/arbeitsstelle/archiv/archiv1-m.jpg)

---

# Lexikografische Arbeit

+ Wortschatz der deutschen Sprache im Auge behalten
+ das eigene Wörterbuch kennen


+ neue Wörterbuchartikel schreiben: **Brexit**, **posten**
+ bestehende Artikel ergänzen:
    - neue Bedeutungen: **Maus**, **Ampel**
    - Anpassung an gesellschaftlichen Wandel: **Ehe**, **Eskimo**, **Gutmensch**
    - Artikel erweitern (weil bislang nur minimal)
+ bestehende Artikel überarbeiten:
    - Bedeutungswandel: **klicken**
    - Rechtschreibreform: ~~Ketschup~~, **Co-Trainer**

---

# Formangaben

+ Wortart (Substantiv, Verb, Adjektiv, ...)
+ Schreibungen
    * alles zulässig: **Delfin**, **Delphin**
    * neue Rechtschreibung: **Ablass**, ~~Ablaß~~
    * war schon immer falsch: **E-Mail**, ~~Email~~
+ weitere Informationen
    * **die** E-Mail, **das** E-Mail
.diasys[süddeutsch, österreichisch, schweizerisch]
    * **das** Virus, **der** Virus
.diasys[umgangssprachlich]
    * **Ferien**
.diasys[wird nur im Plural verwendet]


---

# Homographe

- gleich geschriebene Wörter
- verschieden nach: Herkunft, Formen, Genus, Aussprache, Zusammensetzung
- Beispiele:
    + **Bug**: Vorderteil eines Schiffes, (Software)Fehler
    + **Band**: Pl. Bänder/Bande, Bände, Bands
    + **Bank**: Pl. Bänke, Banken
    + **sein**: Pronomen, Verb
    + **Dichtung**: von *dicht*, von *(er)dichten*
    + **Hut**: der, die
    + **Wachstube**: *Wach* + *Stube*, *Wachs* + *Tube*

---

# Lesarten

- (Unter)Bedeutungen eines Wortes:
    + **scharf**: schneidend, spitz, stark reizend, genau, deutlich, streng, ...
    + **Läufer**: jmd. der läuft, Teppich, Schachfigur, ...
    + **Birne**: Frucht, Baum, Glühlampe, Kopf
- Markierungen:
    + 
.diasys[bildlich] den Teufel an die Wand **malen**
    + 
.diasys[salopp, abwertend] jmdn. nicht **riechen** können
    + 
.diasys[vertraulich] altes **Haus**!
    + 
.diasys[gehoben, veraltend] jemanden einer Tat **zeihen** *(= bezichtigen)*
    + 
.diasys[Medizin] **Exazerbation:** Verschlimmerung, zeitweise Steigerung, Wiederaufleben einer Krankheit
    + 
.diasys[Schülersprache, landschaftlich] **Giftzettel:** Schulzeugnis

---

# Lesarten

- (konstruierte) Beispiele:
    + die allgemeinbildende, berufsbildende, zehnklassige **Schule**
- Belege aus Textsammlungen:
    + „Urlaub in der eigenen Stadt ist nicht traurig, sondern **trendy**, und das schon seit einer ganzen Weile.“ *[Welt am Sonntag, 25.09.2016, Nr. 39]*
- Konstruktionsmuster:
    + etwas **gilt**
    + etwas **gelten** lassen
    + etwas **geltend** machen
    + es **gilt** etwas (zu tun)
- Kollokationen (= Stellung, Anordnung):
    + *mit Akkusativobjekt:* **Drogen** beschlagnahmen, sicherstellen
    + *mit vergleichender Wortgruppe:* **Drogen** wie Kokain, Ecstasy, Heroin

---

# Etymologie

- altgriechisch: *ἐτυμολογία (etymología)*
    + *ἔτυμος (étymos):* „wahr, echt, wirklich“
    + *λόγος (lógos):* „Wort“
- Wissenschaft von der Entstehung und geschichtlichen Veränderung einzelner Wörter 
- im DWDS mit ca. 25 000 Einträgen:
    + <span style="font-variant:small-caps;">Wolfgang Pfeiffer</span> (&#x2A;1922) &ndash; *Etymologisches Wörterbuch des Deutschen*

---

# Etymologie &ndash; Beispiele

.smaller[**Fake News:** Übernahme von gleichbedeutend *fake news* (amerik.-engl.)]

.smaller[**Eskimo:** Genaue Herkunft unsicher; wohl über **eskimoda**<sub>en</sub> oder **esquimau**<sub>frz</sub> aus einer indigenen nordostamerikanischen Algonkin-Sprache (Innu-aimun bzw. Montagnais), vermutlich mit einer ursprünglichen Bedeutung ‘Schneeschuh-Knüpfer’. Eine zunächst angenommene ursprüngliche Bedeutung ‘Esser von rohem Fleisch’ gilt als widerlegt, war aber der Grund, die Bezeichnung **Eskimo** als abwertend einzuschätzen.]

.smaller[**Maulwurf:** Der Name hat mehrfach volksetymologische Umdeutungen erfahren. Die älteste Bezeugung ahd. (8. Jh.), mhd. *mūwerf*, ahd. *mūwerfo* (11. Jh.) enthält in ihrem ersten Glied ein zu aengl. *mūga*, *mūha*, *mūwa* ‘Kornhaufen’, engl. *mow* ‘Heu-, Kornhaufen’, anord. *mūgi*, *mūgr* ‘Menge, Haufen’, mhd. *mocke* ‘Klumpen, Brocken’ gehörendes Substantiv, das vielleicht mit griech. *mýkōn* (*μύκων*) ‘(Korn)haufen’ verwandt ist ...]

---

# Thesaurus

- altgriechisch:
  + *θησαυρός (thesaurós)* → „Schatz, Schatzhaus“
  + später lateinisch *thesaurus* → *Tresor*
- Wortnetz: listet systematisch Wörter
    + gleichbedeutend, ähnlich (Synonyme)
    + Oberbegriffe (Hyperonyme)
    + Unterbegriffe (Hyponyme)
    + thematisch verwandt (Assoziationen)
    + Gegenwörter (Antonyme)
- im DWDS:
    + [OpenThesaurus](http://www.openthesaurus.de) mit ca. 160 000 Einträgen
    + GermaNet

---

# Thesaurus

- Synonyme:
    * **Kreuz:**
        + Bürde, Crux, Fron, Joch, Knechtschaft, Krux, Last, Plage
        + Autobahnknoten
        + Rücken, Rückgrat, Wirbelsäule
- Oberbegriffe (Hyperonyme):
    + **Tomate:** Fruchtgemüse, essbare Pflanzen(teile), Grünzeug
- Unterbegriffe (Hyponyme):
    + **Fahrzeug:** Bahn, Bus, Zug
- Assoziationen:
    + **Apfel:** Birne, Apfelsaft
- Gegenworte (Antonyme):
    + **Ernst:** Spaß

---

# Überblick

## Demo

- Typische Verbindungen:
    - Korpora: Annotation, Quellen
    - syntaktische Analyse
    - Kollokationen
    - distributionelle Semantik (Profilardy)
- Verwendungsbeispiele
- Wortverlaufskurven

---

# Überblick

## Aufgabenteil

---

# Typische Verbindungen

![Stress](figures/wp_kaffee.png)

---

# Typische Verbindungen

+ statistisch signifikante und damit typische Wortverbindungen
+ als Schlagwortwolke (Tagcloud) oder als Tabelle

.center[.img-orig[![Stress](figures/wp_kaffee_objekt.png)]]

---

# Wortverlaufskurven

+ Wortvergleiche möglich (Gemeinsamkeiten und Unterschiede)

---

# Wortverlaufskurven

+ nutzen Textsammlungen als Basis:
    - Zeitungen (1945 bis heute)
    - Deutsches Textarchiv und DWDS-Kernkorpus (1600&ndash;2000)
+ Metadaten für jeden Text:
    - *Datum* (Jahr)
    - *Textklasse* (Belletristik, Gebrauchsliteratur, Wissenschaft, Zeitung)
    - und viele weitere ...
+ bilden die Häufigkeit eines Wort über einen zeitlichen Verlauf ab:
    - relativ (Vorkommen pro Million)
        + 
.red[Achtung!] Kurven werden geglättet, da nicht für jedes Jahr ausreichend und gleich viele Daten verfügbar sind
    - in absoluten Zahlen

---

# Wortverlaufskurven

![Stress](figures/stress.svg)

---

# Wortverlaufskurven

![Flugzeug vs. Eisenbahn](figures/flugzeug_vs_eisenbahn.svg)

---

# Wortverlaufskurven

![(Bundes)Kanzler vs. (Bundes)Kanzlerin](figures/kanzler_vs_kanzlerin.svg)
