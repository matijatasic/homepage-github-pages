# Persönliche Homepage auf GitHub Pages

**Abschlussdokumentation** · Umsetzung: Matija Tasic · Stand: 16.10.2026

Eigene Homepage unter `matija-tasic.de`: statisch gebaut, bei GitHub Pages gehostet und über die Domain bei Strato erreichbar.

**Live:** [matija-tasic.de](https://matija-tasic.de) · **PDF:** [Abschlussdokumentation_Homepage.pdf](Abschlussdokumentation_Homepage.pdf) · **Quellcode der Seite:** [matijatasic.github.io](https://github.com/matijatasic/matijatasic.github.io)

## 1. Zusammenfassung

Die persönliche Homepage ist als statische Seite mit HTML, CSS und etwas JavaScript umgesetzt und läuft über GitHub Pages unter der eigenen Domain `matija-tasic.de`. Die Gestaltung lehnt sich an Bewerbung und Projektdokumentation an: dunkle Seitenleiste, Petrol als Akzentfarbe und eine durchgehende „Leitung“, die die Kapitel beim Scrollen wie Ports in einem Netzplan verbindet. Die Domain wurde dafür bei Strato aufgeräumt: alte Subdomains und DynDNS entfernt, die Einträge auf GitHub gesetzt und eine Kontaktadresse eingerichtet.

**Ergebnis:**

- Homepage live unter `matija-tasic.de`, veröffentlicht automatisch bei jedem Push auf `main`
- Deutsch und Englisch per Schalter, helle und dunkle Darstellung, für Handy und Desktop
- Verschlüsselt über HTTPS mit Zertifikat von Let’s Encrypt, http wird automatisch umgeleitet
- Keine Cookies, kein Tracking, keine externen Schriften oder Dienste
- DNS bei Strato sauber auf GitHub umgestellt, alte Einträge und DynDNS entfernt
- Kontakt über `kontakt@matija-tasic.de`, Zustellung getestet
- Alle Commits nur mit Matija Tasic als Autor

## 2. Ausgangslage und Ziel

**Ausgangslage**

- Domain `matija-tasic.de` bei Strato in einem einfachen Domain-Paket
- Hauptdomain zeigte per DynDNS auf den Internetanschluss zu Hause
- Drei alte Subdomains aus früheren Heimserver-Projekten, keine davon mehr in Betrieb
- Kein eigener Webauftritt vorhanden

**Ziel**

- Eigene Homepage als Portfolio, gehostet auf GitHub Pages
- Hauptdomain zeigt auf GitHub, Subdomains bleiben für spätere Heimserver-Projekte frei
- Gestaltung angelehnt an Bewerbung und Dokumentation, seriös, mit eigenem Wiedererkennungswert
- Zuerst steht die Seite, die Inhalte folgen später

### 2.1 Umfang

**Im Umfang**

- Aufbau der Seite in HTML und CSS
- Sprach- und Darstellungsschalter
- Repository und Veröffentlichung mit GitHub Pages
- Domain, DNS und HTTPS
- Kontaktadresse bei Strato

**Außerhalb des Umfangs**

- Endgültige Texte und Projektinhalte
- Nextcloud und Reverse Proxy zu Hause (eigenes Projekt)
- Kontaktformular (bewusst entfallen)
- Analyse- oder Tracking-Werkzeuge

## 3. Anforderungen

Die Anforderungen wurden zu Beginn gemeinsam erhoben. Es wurde nichts ergänzt, was nicht ausdrücklich gewünscht war.

| Anforderung | Umsetzung |
|---|---|
| Hauptdomain `matija-tasic.de` auf GitHub | GitHub Pages mit eigener Domain, Einträge bei Strato |
| Subdomains später für den Heimserver | Nur Hauptdomain und `www` belegt, alles andere frei |
| Portfolio im Stil von Bewerbung und Doku | Konzept „Dossier“: Seitenleiste, Petrol, Kapitelköpfe wie im PDF |
| Abheben von üblichen IT-Seiten, seriös, mit Aha-Effekt | Scroll-gesteuerte „Leitung“, die Kapitel wie Netzwerk-Ports verbindet |
| Reines HTML/CSS | Kein Framework, kein Build-Schritt |
| Repository `matijatasic.github.io` | Öffentliches Repository, Veröffentlichung aus `main` |
| Deutsch mit Schalter auf Englisch | Alle Texte doppelt gepflegt, Wahl wird gemerkt |
| Hell/Dunkel-Schalter | Folgt der Systemeinstellung, Wahl wird gemerkt |
| Kontaktmöglichkeit | E-Mail-Adresse und GitHub-Profil im Kapitel Kontakt |

## 4. Architektur

![Abb. 1 · Weg einer Anfrage: Der Besucher fragt das DNS bei Strato, lädt die Seite über HTTPS von GitHub Pages; Mails an die Domain landen im Strato-Postfach.](img/architektur.svg)

| Baustein | Aufgabe |
|---|---|
| Strato | Registrar und DNS der Domain, Postfach für E-Mails |
| GitHub Repository | Quellcode der Seite, jeder Push auf `main` löst die Veröffentlichung aus |
| GitHub Pages | Ausliefern der Seite, TLS-Zertifikat für die eigene Domain |
| Browser | Sprache und Darstellung werden lokal im Browser gemerkt (localStorage) |

## 5. Gestaltung und Aufbau der Seite

### 5.1 Konzept „Dossier“

Die Seite liest sich wie ein technisches Dossier: Links eine dunkle Seitenleiste mit Portrait, Kapitelübersicht und den Schaltern, rechts der Inhalt auf einem feinen Rasterhintergrund. Die Kapitel tragen nummerierte Köpfe wie `01 PROFIL`, genau wie in der Projektdokumentation.

Der Wiedererkennungswert entsteht durch die **Leitung**: Eine Linie läuft beim Scrollen am Inhalt entlang, schaltet die Kapitel nacheinander „online“ und zweigt zu jeder Projekt- und Kompetenzkarte ab. In der Kapitelübersicht leuchten passend dazu kleine LEDs. Unten rechts zeigt ein Seitenzähler wie im PDF das aktuelle Kapitel.

![Abb. 2 · Startseite in heller Darstellung.](img/start-hell.png)

| Element | Umsetzung |
|---|---|
| Schriften | Inter und Inter Display für Text, DejaVu Sans Mono für Kennungen |
| Farben | Petrol `#17a398` als Akzent, dunkle Seitenleiste, eigene Farbwerte für Dunkel |
| Kapitel | 00 Start · 01 Profil · 02 Kompetenzen · 03 Projekte · 04 Kontakt |
| Projekte | Status je Karte: abgeschlossen, in Arbeit, geplant |
| Handy | Seitenleiste wird zum Menü, Leitung und Karten passen sich an |
| Barrierefreiheit | Sprunglink zum Inhalt, Tastaturbedienung, reduzierte Bewegung wird respektiert |

![Abb. 3 · Kontakt in dunkler Darstellung und Startseite auf dem Handy.](img/kontakt-dunkel-handy.png)

### 5.2 Technik

| Datei | Inhalt |
|---|---|
| `index.html` | Startseite mit allen Kapiteln, Texte auf Deutsch und Englisch |
| `404.html` | Eigene Fehlerseite |
| `assets/css/site.css` | Gestaltung, Farbwerte für hell und dunkel, Handy-Ansicht |
| `assets/js/site.js` | Sprach- und Darstellungsschalter, Leitung, Seitenzähler |
| `assets/fonts/` | Schriften als WOFF2 mit Lizenztexten |
| `assets/img/` | Portrait und Favicon |
| `CNAME` | Eigene Domain für GitHub Pages |
| `.nojekyll` | Seite wird unverändert ausgeliefert, ohne Jekyll |

**Sprache:** Jeder Text steht doppelt im HTML, einmal mit `data-l="de"` und einmal mit `data-l="en"`. Der Schalter setzt nur die Sprache der Seite, das CSS blendet die jeweils andere Fassung aus. Ein kurzes Skript im Kopf der Seite stellt die gemerkte Wahl schon vor dem ersten Zeichnen her, damit nichts flackert.

**Darstellung:** Ohne Wahl folgt die Seite der Systemeinstellung. Ein Klick legt hell oder dunkel fest und merkt sich das.

**Datenschutz by Design:** Keine Cookies, kein Tracking, keine Schriften oder Skripte von fremden Servern. Im Browser werden nur Sprache und Darstellung gespeichert.

## 6. Veröffentlichung auf GitHub Pages

| Einstellung | Wert |
|---|---|
| Repository | `matijatasic/matijatasic.github.io`, öffentlich |
| Quelle | Bereitstellung von einem Branch: `main`, Ordner `/` |
| Eigene Domain | `matija-tasic.de` |
| Domain-Verifizierung | TXT-Eintrag im GitHub-Profil bestätigt |
| HTTPS erzwingen | aktiviert, Zertifikat von Let’s Encrypt ausgestellt |

> **Ablauf:** Änderung lokal prüfen, als Matija Tasic committen, auf `main` pushen. GitHub baut und veröffentlicht die Seite danach selbst, in der Regel innerhalb einer Minute.

**Commits:** Alle Commits stehen nur unter dem Namen Matija Tasic und nutzen die private noreply-Adresse von GitHub. So bleibt die echte E-Mail-Adresse verborgen.

## 7. Domain und DNS bei Strato

### 7.1 Vorgehen

Die Reihenfolge folgt der Empfehlung von GitHub, damit niemand anderes die Domain bei GitHub Pages übernehmen kann:

1. Domain im GitHub-Profil verifizieren (TXT-Eintrag)
2. Eigene Domain im Repository eintragen
3. DNS-Einträge bei Strato auf GitHub umstellen
4. Zertifikat abwarten, HTTPS erzwingen

### 7.2 Vorher und nachher

| Eintrag | Vorher | Nachher |
|---|---|---|
| Hauptdomain A | Heimanschluss über DynDNS | `185.199.108.153` (GitHub Pages) |
| Hauptdomain AAAA | keiner | `2606:50c0:8000::153` (GitHub Pages) |
| TXT `_github-pages-challenge-matijatasic` | keiner | Prüfwert von GitHub |
| `www` | Strato-Platzhalter | CNAME auf `matijatasic.github.io` |
| DynDNS | aktiv, aktualisiert von der FRITZ!Box | bei Strato und in der FRITZ!Box abgeschaltet |
| Alte Subdomains (3) | vorhanden, ohne Funktion | gelöscht |
| E-Mail (MX) | Strato | unverändert Strato |

> **Wichtig bei Strato:** Ein CNAME auf der Hauptdomain hätte alle übrigen Einträge abgeschaltet, auch die E-Mail. Der CNAME für `www` wurde deshalb in der Subdomain selbst gesetzt. Neben dem Eingabefeld muss `.www.matija-tasic.de` stehen, nicht `.matija-tasic.de`.

### 7.3 DynDNS abschalten

Strato erlaubt einen eigenen A-Eintrag nur ohne DynDNS. DynDNS wurde deshalb zuerst bei Strato und danach in der FRITZ!Box abgeschaltet (Internet → Freigaben → DynDNS). Sonst hätte die FRITZ!Box den Eintrag für GitHub später wieder mit der Heim-IP überschrieben. Portfreigaben für 80 oder 443 gab es in der FRITZ!Box keine.

Für den Zugriff auf die FRITZ!Box aus dem privaten Netz kam in OPNsense eine eng gefasste Regel dazu: nur die Admin-PCs, nur zur FRITZ!Box, nur HTTPS. Sie steht über der Sperrregel für interne Netze und folgt dem Namensschema aus dem Segmentierungsprojekt.

## 8. HTTPS

GitHub Pages stellt für die eigene Domain automatisch ein Zertifikat von Let’s Encrypt aus. Das gelingt erst, wenn alle zugehörigen Namen korrekt auf GitHub zeigen. Solange `www` noch auf den Strato-Platzhalter zeigte, blieb die Ausstellung hängen.

> **Stand 16.10.2026, 20:19:** Nachdem `www` per CNAME auf GitHub zeigte, hat GitHub das Zertifikat ausgestellt. Die Seite lädt mit Schloss, und „HTTPS erzwingen“ leitet jeden Aufruf über http automatisch auf https um.

## 9. E-Mail

Die Adresse `kontakt@matija-tasic.de` ist bei Strato als Alias auf ein bestehendes Postfach eingerichtet. Mails an die Adresse landen dort und sind per Webmail oder IMAP abrufbar. Eine Testmail von einer externen Adresse ist angekommen.

Ein Kontaktformular gibt es bewusst nicht. Besucher schreiben direkt per E-Mail. Das spart einen externen Formular-Dienst und hält die Seite frei von fremden Diensten.

## 10. Tests

| Test | Ergebnis |
|---|---|
| Veröffentlichung durch GitHub Pages (5 Durchläufe) | ok |
| Domain-Verifizierung per TXT | ok |
| DNS-Prüfung in den Pages-Einstellungen | ok, „DNS-Prüfung erfolgreich“ |
| Aufruf über `matija-tasic.de` | ok |
| Testmail an `kontakt@matija-tasic.de` | ok, im Postfach angekommen |
| Schalter Deutsch / Englisch | ok, alle Texte wechseln, Wahl bleibt nach Neuladen |
| Schalter Hell / Dunkel | ok, Wahl bleibt nach Neuladen |
| Handy-Ansicht 390 px | ok, kein seitliches Scrollen, Menü funktioniert |
| Browser-Konsole | ok, keine Fehler |
| Zertifikat für HTTPS | ok, ausgestellt, http wird auf https umgeleitet |
| Aufruf über `www.matija-tasic.de` | ok, Zertifikat gilt auch für www |

## 11. Entscheidungen

| Datum | Entscheidung | Begründung |
|---|---|---|
| 16.10.2026 | Hauptdomain auf GitHub, Subdomains frei | Homepage zuerst, Heimserver-Dienste später über Subdomains |
| 16.10.2026 | Reines HTML/CSS ohne Framework | Wenig Abhängigkeiten, leicht zu pflegen, schnell |
| 16.10.2026 | Konzept „Dossier“ | Passt zu Bewerbung und Doku, hebt sich von üblichen IT-Seiten ab |
| 16.10.2026 | Schriften lokal statt von Google Fonts | Keine Verbindung zu fremden Servern beim Seitenaufruf |
| 16.10.2026 | Alte Subdomains gelöscht | Ohne Funktion, später bei Bedarf neu anlegen |
| 16.10.2026 | DynDNS abgeschaltet | Nötig für eigenen A-Eintrag, zu Hause läuft derzeit nichts darüber |
| 16.10.2026 | Kein Kontaktformular | Kontakt per E-Mail reicht, kein externer Formular-Dienst nötig |
| 16.10.2026 | Kein Impressum und keine Datenschutzerklärung | Bewusste Entscheidung des Betreibers, Seiten bei Bedarf aus der Git-Historie wiederherstellbar |
| 16.10.2026 | Automatische Browser-Übersetzung abgeschaltet | Die Seite hat einen eigenen Sprachschalter |

## 12. Probleme und Lösungen

**Eigener A-Eintrag bei Strato nicht möglich**

- *Ursache:* DynDNS war für die Hauptdomain aktiv.
- *Lösung:* DynDNS bei Strato abgeschaltet, danach A- und AAAA-Eintrag gesetzt.

**FRITZ!Box aus dem privaten Netz nicht erreichbar**

- *Ursache:* Die Firewall sperrt bewusst alle internen Netze, also auch das Netz der FRITZ!Box.
- *Lösung:* Eng gefasste Regel nur für die Admin-PCs und nur HTTPS, oberhalb der Sperrregel.

**Neue Firewall-Regel griff nicht**

- *Ursache:* Der Alias für die FRITZ!Box war gespeichert, aber noch nicht angewendet und damit leer.
- *Lösung:* Auf der Alias-Seite „Anwenden“ geklickt, Inhalt unter Firewall → Diagnose → Aliase geprüft.

**Englische Fassung erschien auf Deutsch**

- *Ursache:* Der Browser übersetzte die englische Seite automatisch zurück ins Deutsche.
- *Lösung:* Seite als nicht zu übersetzen markiert (`translate="no"`), der eigene Schalter genügt.

**CNAME beinahe auf der Hauptdomain**

- *Ursache:* Das CNAME-Formular der Hauptdomain sieht dem der Subdomain sehr ähnlich.
- *Lösung:* Vor dem Speichern abgebrochen, CNAME in der Subdomain `www` gesetzt. Merkmal ist die Endung neben dem Eingabefeld.

**HTTPS-Zertifikat wurde nicht ausgestellt**

- *Ursache:* `www` zeigte noch auf den Strato-Platzhalter.
- *Lösung:* CNAME für `www` auf `matijatasic.github.io`, danach hat GitHub die Ausstellung neu gestartet.

## 13. Lessons Learned

- Die von GitHub empfohlene Reihenfolge (erst verifizieren, dann umstellen) verhindert, dass jemand anderes die Domain übernimmt.
- Vor einer DNS-Änderung immer den Ist-Stand per Screenshot sichern.
- Bei Strato hängt viel an der richtigen Ebene: Hauptdomain und Subdomain haben eigene DNS-Seiten.
- Eine strenge Firewall wirkt auch gegen den eigenen Router. Ausnahmen so eng wie möglich halten.
- In OPNsense werden Aliase erst mit „Anwenden“ aktiv. Die Diagnose-Seite zeigt den echten Inhalt.
- Zweisprachige Seiten sollten die automatische Browser-Übersetzung abschalten.

## 14. Offene Punkte

1. Optional: die drei weiteren A- und AAAA-Adressen von GitHub Pages ergänzen, für mehr Ausfallsicherheit.
2. Endgültige Texte und Projektinhalte einpflegen.
3. Späteres Heimserver-Projekt: DynDNS auf einer Subdomain statt auf der Hauptdomain.

## 15. Anhang

### 15.1 Chronologie

| Zeit | Meilenstein |
|---|---|
| 16:46 | Projekt in Notion angelegt; Anforderungen erhoben |
| 17:35 | Repository angelegt; erster Entwurf mit Vorschaubildern |
| 17:38 | Entwurf freigegeben; erste Version veröffentlicht |
| 17:52 | Ist-Stand bei Strato gesichert; alte Subdomains gelöscht |
| 18:09 | Domain verifiziert; eigene Domain im Repository eingetragen |
| ca. 18:30 | DynDNS bei Strato aus; A- und AAAA-Eintrag gesetzt; DNS-Prüfung erfolgreich |
| 18:50 | Zugriff auf die FRITZ!Box eingerichtet; DynDNS in der FRITZ!Box aus |
| 19:10 | Kontaktadresse eingerichtet; Testmail angekommen |
| 19:24 | Kontaktformular, Impressum und Datenschutz entfernt |
| 19:29 | Browser-Übersetzung abgeschaltet; Sprachschalter bestätigt |
| 19:53 | `www` per CNAME auf GitHub; Zertifikat neu angefordert |
| 20:19 | Zertifikat ausgestellt; HTTPS aktiv und erzwungen |

### 15.2 Projektverwaltung

Das Projekt wurde wie das Segmentierungsprojekt in Notion geführt: Projektseite, Aufgabendatenbank „Aufgaben Homepage“ mit Phasen von Bedarf bis Abschluss und ein Projektjournal. Jede Änderung an DNS und Firewall wurde vorher mit Risiko und Rückweg benannt und erst nach Freigabe umgesetzt.
