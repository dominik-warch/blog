---
title: "Über das Speichern von Webseiten, Oder: Warum die einfachste Lösung manchmal die beste ist"
date: 2023-03-04T18:19:51+02:00
draft: false
---

Als Kind und Jugendlicher mit sehr beschränktem Internetzugriff (meistens nur an den Bibliotheks-Computern meiner Schule) war es fast schon Routine, interessante Webseiten per "Datei -> Speichern unter..." lokal zu sichern. Ich habe dann ein Lied von meinem tragbaren MP3-Player mit satten 128 MB Speicher gelöscht und konnte so einen ganzen Schwung Internet mit nach Hause nehmen und dort in aller Ruhe begutachten. Quasi Internet ausdrucken der Generation Millenials. Durch die ständige Verfügbarkeit von Internet ist diese Praxis heutzutage fast obsolet. Dutzende offene Tabs die bei Bedarf einfach den Inhalt neu laden, "Read it later"-Erweiterungen für den Browser und dergleichen lassen die Notwendigkeit gar nicht erst aufkommen. Vom rein praktischen Standpunkt aus, sind moderne Single Page Applications (SPA) sowieso auch gar nicht mehr so einfach lokal zu speichern.

Wenn man - wie ich - haufenweise Lesezeichen ansammelt und sie nach einiger Zeit auch noch einmal anschaut, sieht man immer häufiger Folgendes: **404 - Not found**. Das Internet ist ein schnelllebiger Platz und wo es einerseits heißt _"Das Internet vergisst nicht"_, ist es auf der anderen Seite nicht selten, dass die gesuchten Webseiten und damit auch ihre Informationen und Daten verschollen sind. Nicht gezahlte Hostinggebühren oder einfach fehlende Zeit oder fehlendes Interesse an Wartung und Erhalt führen zu verwaisten Links. Wenn man Glück hat, gibt es einen Snapshot im [Internet Archive](https://archive.org/), aber je kleiner und skuriller die Website (sowas wie mein Blog hier) ist, desto unwahrscheinlicher ist das. Und dann gibt es noch eine ganze Kategorie von Inhalten, die sich per Definition immer wieder ändern, aber hochinformativ sind: Offene Kursmaterialien von Universitäten, die (mit wechselnder Qualität) pro Semester oder Jahr aktualisiert oder sogar ganz eingestellt werden. Schöne Beispiele sind [The Missing Semester of Your CS Education](https://missing.csail.mit.edu/) oder die Geoinformatik-Kurse der PennState (z.B. [GEOG 485: GIS Programming and Software Development](https://www.e-education.psu.edu/geog485/syllabus)). Vielleicht werden vorherige Iterationen des Kurses erhalten (wie beim Missing Semester), vielleicht aber auch nicht (wie bei der PennState). Für mich sind das wertvolle Wissensschätze und Referenzmaterialien und erhaltenswert. Aber wie erhalten?

## Speichern unter

Die alte Fast-Routine funktioniert für einfache Seiten noch immer ziemlich gut. Wenn viele Fremdquellen (CSS und JavaScript von einem CDN z.B.) eingebunden sind, ist das lokale Betrachten durch Mixed-Content-Regeln häufig eingeschränkt und am Ende des Tages auch nicht nachhaltig. Der CDN-Anbieter kann die Inhalte offline nehmen, der Link kann sich ändern etc. Dann habe ich vielleich noch einen großen Teil der reinen Textinhalte, aber schön sieht das nicht aus. Das kann einem egal sein, aber... mir ist es das nicht.

Das viel größere Manko: Per "Speichern unter" sichere ich nur die eine Seite, auf der ich aktuell unterwegs bin. Gerade meine beiden angeführten Beispiele haben allerdings einige Unterseiten - häufig pro Kurseinheit oder Semesterwochenstunde. Die händisch durchzuarbeiten... das macht keinen Spaß und im Zweifel vergisst man auch etwas. Da musste eine bessere Lösung her.

## Internet Archive

Ein nachhaltiger und umfänglicher Ansatz ist es, die gewünschten Seiten selbst von der Wayback Machine des Internet Archive archivieren zu lassen. Ich finde das Internet Archive wunderbar und das Vorhaben absolut begrüßenswert - dass ich jederzeit einfach die Archivierung einer Webseite veranlassen kann und das dann innerhalb weniger Sekunden bis Minuten umgesetzt wird: Wahnsinn! Leider habe ich aber keine lokale (und damit schnelle) Kopie auf meinem Rechner. Die Wayback Machine ist leider verhältnismäßig träge. Außerdem bin ich wieder abhängig davon, dass der Anbieter seine Inhalte zur Verfügung stellt und nicht irgendwann einfach alles weg ist. Klar... dass das Internet Archive von heute auf morgen tot ist, ist deutlich weniger wahrscheinlich als dass meine lokale Kopie plötzlich verschwunden ist, aber mehr Redundanz kann ja nicht schaden... oder? Je populärer eine Seite ist, desto mehr Snapshots gibt es allerdings auch und desto komplexer ist es, zwischen Unterseiten verschiedener Zeitpunkte hin und her zu springen. Das ist gerade bei so Kursmaterialien ärgerlich, wenn man bei den Inhalten zwischen Semestern hin- und herspringt.

## ArchiveBox

In der Self-Hosted-Welt gibt es mit [ArchiveBox](https://github.com/ArchiveBox/ArchiveBox) eine (aber bei weitem nicht die einzige) Lösung, lokal oder auf einem eigenen Server eine Art self-hosted Wayback Machine zu haben. Ebenfalls toll und unterstützenswert, leider habe ich bei der ArchiveBox - der bliebtesten Lösung in dem Bereich - das gleiche Problem wie beim "Speichern unter": Lediglich die eine durchgereichte Seite wird gesichert und wenn ich das mit allen Unterseiten mache, haben diese leider keine Verbindung zueinander. Sie wissen gar nicht, dass sie alle jeweils eine Version in der ArchiveBox sind, sondern verlinken fröhlich weiter zu ihrer Originalquelle. Das ist ärgerlich und ich habe beim Sichten und Testen einiger anderer Lösungen auch keine andere gefunden, die mir das ermöglicht.

## wget

Bei StackOverflow (wo sonst) bin ich dann auf die `wget` gestoßen. Nicht im Sinne von, wget entdeckt - ich kannte das schon vorher - aber ich habe nicht daran gedacht, wget in dem Kontext zu verwenden. Wget ist ein GNU-Kommandozeilenprogramm zum Herunterladen von Dateien. So einfach, so simpel. Auf dem ersten Blick könnte man meinen: Stark, die "Speichern unter"-Variante im Terminal, damit könnte man zumindest die ganzen Unterseiten über ein Batch-Script automatisch runterladen und musst nicht per Hand auf jeder Unterseite "Speichern unter" drücken. Ha, genau das dachte ich auch, bis mir der StackOverflow-Beitrag die zahlreichen Flags aufgezeigt hat, die wget zur perfekten Lösung für mein Problem werden lassen!

Für die lokale Sicherung einer Seite und deren Unterseiten (am Beispiel des obigen PennState-Kurses) verwende ich folgenden Befehl im Terminal:

```bash
wget --recursive --no-clobber --page-requisites --html-extension --convert-links https://www.e-education.psu.edu/geog485/syllabus
```

Die zusätzlichen Flags sind `--recursive`, `--no-clobber`, `--page-requisites`, `--html-extension` und `--convert-links`. Was diese Flags bewirken?

- **--recursive** sorgt dafür, dass nicht nur die Seite der durchgegebenen URL heruntergeladen wird, sondern auch "Unter"seiten, die auf der durchgegeben Seite verlinkt sind. Die maximale Tiefe kann mit einer weiteren Flag definiert werden, standardmäßig beträgt sie fünf Stufen, wobei wget lokal dann eine Ordnerstruktur anlegt wie es sie auch auf dem Server vorfindet. Ich bleibe meistens bei der Standardtiefe und schaue mir das Ergebnis an, ggf. verändere ich dann den Wert und führe den Befehl noch einmal neu aus.
- **--no-clobber:** Gerade das rekursive Herunterladen kann dazu führen, dass die gleiche Seite mehrmals heruntergeladen werden würde. `no-clobber` verhindert das, sodass man keine unnötigen Duplikate hat.
- **--page-requisites:** `page-requisites` sorgt dafür, dass auch CSS-Dateien, Bilder, JavaScript, Videos heruntergeladen werden, alles eben, was man braucht, um die Seite lokal zu betrachten!
- **--html-extension:** Manchmal sind die Ursprungsinhalte in Form von .asp-Seiten oder CGI-generiert. Das stupide Herunterladen würde dazu führen, dass sich die Seiten nicht ohne Weiteres lokal im Browser öffnen lassen. Die Flag `html-extension` forciert die "Umwandlung" zu HTML-Dateien und vereinfacht den Umgang mit den heruntergeladenen Inhalten.
- **--convert-links:** Zusammen mit `recursive` und `page-requisites` das absolute Killer-Feature: Nachdem alle Inhalte heruntergeladen wurden, ändert wget alle Links so ab, dass man die Seite lokal auch betrachten kann. Hat wget die Inhalte hinter dem Link heruntergeladen, wird der Link zu einem passenden, relativen Pfad verändert, andernfalls wird z.B. der Hostname ergänzt, um absolute Pfade ins Internet zu bekommen (wenn die Maximaltiefe z.B. nicht ausreichend war).

Das Ergebnis ist dann ein Ordner (hier ein Auszug des Unterordners des eigentlich Kurses 485 - der Befehl hat deutlich mehr heruntergeladen!) mit den statischen Dateien wie Stylesheets und Bildern und eben den dazugehörigen HTML-Dateien mitsamt den Inhalten.

![Screenshot des wget-Downloadergebnisses](/img/wget_ergebnis.jpg)
