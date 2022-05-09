---
title: "Pen & Paper, Musik und Corona, Pt. 1"
date: 2022-05-08T13:18:59+02:00
draft: false
tags: ["Pen & Paper", "Musik", "Elixir"]
author: "Dominik Visca"

autoCollapseToc: true
---

## Status quo ante

Vor Corona war ich ein strikter Verfechter des "persönlichen" Pen & Paper-Spielens: Man trifft sich, quatscht ein wenig (oder auch ein wenig mehr), isst zusammen, fängt dann an einem großen Tisch mit Kerzenschein, viel Papier und Würfeln an zu spielen und hört auf, wenn alle müde sind. Virtuelles Pen & Paper empfand ich immer als ein unzureichendes Erlebnis, ein wesentliches Element - das Zusammensein - fehlte. Diese Empfindung beruhte allerdings mehr auf meiner Vorstellung von virtuellem Spiel als meiner Erfahrung. Ich hatte bis dahin lediglich an einem Abend einer TeamSpeak-Gruppe mitgemacht und das gefiel mir nicht[^1]. Auch nach der Schul- und Studienzeit blieb das persönliche Spielen vor Ort die absolute Norm, auch wenn durch Umzüge und neue Lebensmittelpunkte mitunter einiges an Wegstrecke anfiel. Wie so vieles veränderte Corona Anfang 2020 aber auch diese "absolute Norm".

## Virtuelles Spiel als Chance

Die Pandemie sorgte natürlich dafür, dass wir uns nicht mal eben für unsere regelmäßigen Sitzungen treffen konnten. Nach einigem Hin und Her[^2] entschieden wir uns, Pen & Paper in die digitale Welt zu verlegen. Schnell war klar, dass das auch eine Chance böte: Zeitlich waren wir nun flexibler, da Anreise und das ganze Socializing vor und nach unserer Spielsitzung wegfielen. Die Terminfindung wurde erheblich leichter[^3] und wir konnten plötzlich wieder Leute ins Boot holen, die dann doch etwas zu weit weg wohnten, um sich regelmäßig persönlich zu treffen. Es wurde reiner Tisch gemacht und eine neue Kampagne gestartet, in der wir auch zur Wurzel unserer Rollenspiel-Erfahrung zurückkehrten: Die [Theaterritter-Kampagne](https://de.wiki-aventurica.de/wiki/Theaterritter-Kampagne) des Rollenspiels [Das Schwarze Auge](https://de.wikipedia.org/wiki/Das_Schwarze_Auge) sollte es werden. Aber wie?

Unsere technischen Anforderungen waren eigentlich gering. Einer unserer Mitspieler hatte bis dahin ganz gute Erfahrungen mit Tools wie [Roll20](https://roll20.net/) gemacht, der allgemeine Tenor war aber, erst einmal schlank zu starten. Wichtig waren uns guter Ton und gutes Bild. Ein wesentliches Element beim Rollenspiel ist die Kommunikation und diese findet zu großen Teilen nicht nur über das gesprochene Wort sondern eben auch über Mimik und Gestik statt. Sämtliche reinen Audio-Lösungen wie TeamSpeak waren damit raus, aber auch viele Lösungen die Video beinhalteten waren für unsere Zwecke nicht ausreichend. Relativ schnell haben wir uns für [Zoom](https://zoom.us) entschieden. Als Freund offener und datenschutzfreundlicher Software nicht meine liebste Wahl, aber sie hat bei allen Beteiligten reibungslos funktioniert, anders als z.B. [Jitsi](https://jitsi.org/)[^4]. Virtuelles Würfeln, Bodenpläne und Ähnliches wird bei uns nicht benötigt. Für gemeinsame Notizen und das ein oder andere Handout hat sich ein Google Doc bewährt, welches einer unserer Mitspieler spontan nebenher gestartet hat. Es fehlte nur ein Ersatz für die musikalische Untermalung.

## Musik: Komplexer als gedacht

Seit Jahren verwenden wir Michas Jingle-Player[^5], um atmosphärische Begleitmusik oder einzelne Soundeffekte passgenau abzuspielen. Das Tool bietet einem 30 Buttons an, die mit beliebigen Audiodateien bestückt werden und dann per Maus oder Shortcut (parallel) abgespielt werden können. Außerdem gibt es die Möglichkeit, für jeden Button Loop zu aktivieren. Eine "neue" Lösung sollte nicht weniger können als das.

### 1. Versuch: Geteilter Bildschirm

Die naheliegendste Lösung war, Michas Jingle-Player weiterhin zu verwenden. Der Spielleiter teilt seinen Bildschirm, wobei dann eben auch der Ton des Jinge-Players geteilt wird. Leider bringt diese Variante zwei Probleme mit sich:

- Der geteilte Bildschirm (der ansonsten keine Verwendung findet) reduziert die Bildschirmfläche für den Videofeed unserer Mitspieler erheblich.
- Die Lautstärke der Musik und des Spielleiters lassen sich nicht unabhängig von einander einstellen, da beide die gleiche Audioquelle (d.h. "Zoom") sind.

Gerade der letzte Punkt ist ein absoluter Dealbreaker. Selbst wenn die Musik relativ leise im Verhältnis zum Spielleiter ist, die Tatsache dass beides aus der gleichen Audioquelle stammt kann die Trennung zwischen Musik und gesprochenem Wort sehr schwer machen. Außerdem möchte man nicht ständig "kannst du die Musik mal leiser/lauter machen?!" hören. 😄

### 2. Versuch: Alternativlösungen des Pen & Paper-Marktes

Wir sind natürlich nicht die Einzigen mit dem Problem. Mittlerweile gibt es einige Lösungen auf dem Markt, die mehr oder weniger gut funktionieren. Zwei möchte ich dabei erwähnen: Das [Soundpad von TabletopAudio.com](https://tabletopaudio.com/soundpad.html) und [Syrinscape Online](https://syrinscape.com/online/).

Die Musik von TabletopAudio findet bei uns immer wieder Verwendung und ich bin ein großer Fan der Arbeit des Komponisten. Das SoundPad gibt es seit einiger Zeit und erlaubt das Streamen von seinen Stücken in einem virtuellen Raum. Das ist grundsätzlich eine starke Lösung, der große Nachteil ist allerdings, dass man keine eigene Musik verwenden kann.

Syrinscape Online erlaubt ebenfalls das Streamen von Musik, sogar von eigenen Dateien. Allerdings habe ich keine Lust, monatlich ca. 10 € dafür auszugeben. Dafür gefällt mir Syrinscape an sich nicht gut genug...

Andere Lösungen haben uns damals noch weniger zugesagt, ggf. gibt es aber mittlerweile auch bessere Alternativen.

### 3. Versuch: Eigener Audio-Stream

Da ich technisch nicht unbedingt unbegabt bin[^6], war eine hausgemachte Lösung schnell im Gespräch. Ein eigener Audiostream á la YouTube Live oder Twitch kam leider nicht in Frage, da ich das Ganze ja nicht öffentlich machen wollte, schon allein aus Copyright-Gründen der verwendeten Musik. Nach kurzer Recherche stieß ich auf die Möglichkeit, den [Nginx-Webserver](https://nginx.org/en/) mit einem [passenden RTMP-Modul](https://nginx-rtmp.blogspot.com/) auszustatten. Damit ist es möglich, mein lokales Audio (z.B. Michas Jingle-Player) mit einer Broadcasting Software wie [OBS](https://obsproject.com/) an den Webserver zu senden, der dann wiederum einen passenden Audiostream daraus macht, der als Link dann z.B. in einem Mediaplayer wie VLC eingebunden werden kann. Im Endeffekt stellt dies die bessere Version von Variante 1 dar: Der unnötige geteilte Bildschirm fällt weg und die Audiolautstärke kann unabhängig von der Lautstärke des Spielers angepasst werden.

![Alt text](/img/2022-05-08_workflow_nginx.png "a title")

Das klang perfekt und war auch für ein paar Spielabende im Einsatz. Leider gibt es mit dieser Lösung eine nicht zu unterschätzende Verzögerung von stellenweise bis zu 30 Sekunden. Ob das an meiner Konfiguration lag, möchte ich nicht ausschließen, klar ist aber, dass eine Verzögerung in irgendeiner Form zu erwarten ist. Da wir immer mal wieder mit zeitlich abgestimmten Soundeffekten und Musikstücken arbeiten, war die Verzögerung nicht optimal und hat in einigen Szenen den für uns gewohnten Effekt kaputt gemacht.

### 4. Versuch: Der Online-Jingle-Player

Bereits in der Vergangenheit habe ich mich mit einem Mitspieler daran gemacht, einen Ersatz für Michas Jingle-Player zu implementieren. Michas Jingle-Player wird seit geraumer Zeit nicht mehr weiterentwickelt, das ein oder andere Wunschfeature hatten wir aber noch. Nach ein paar Tagen Arbeit hatten wir damals einen funktionsfähigen Jingle-Player auf JavaScript-Basis als [Electron-App](https://www.electronjs.org/). Für unseren jetzigen Zweck (online, synchron mit allen Beteiligten) ließ sich das allerdings nicht so ohne Weiteres verwenden.

Wie es der Zufall so will, hatte ich mich seit einiger Zeit mit [Elixir](https://elixir-lang.org/) und dem dazugehörigen Framework [Phoenix](https://www.phoenixframework.org/) beschäftigt. Phoenix ermöglicht es, mit relativ wenig Aufwand Webanwendungen zu erstellen, ähnlich wie es Rails für Ruby und Django für Python ermöglichen. Einige Monate vor der Pandemie erschien mit Phoenix LiveView ein Feature-Paket, welches geradezu gemacht war, um ohne großen Aufwand einen Online-Jingle-Player umzusetzen. LiveView baut zwischen Server und Client eine kontinuierliche Verbindung durch WebSockets auf. Der Hauptentwickler Chris McCord zeigt in [folgendem Video](https://www.youtube.com/watch?v=MZvmYaFkNJI), wie sich innerhalb von 15 Minuten ein Twitter-Livefeed realisieren lässt.

Die Idee war, ein Soundboard mit serverseitig gespeicherten Audiodateien anzubieten und alle Aktionen - z.B. Starten und Stoppen von Musik - über alle verbundenen Clients zu replizieren. Es soll also kein Audio vom Spielleiter zu den Spielern gestreamt werden, sondern die jeweils im Browsercache vorgehaltenen Audiofiles synchron abgespielt, gestoppt und in ihrer Lautstärke verändert werden können.

Mehr dazu aber in Part 2!

[^1]: Das hatte möglicherweise aber auch ganz andere Gründe als das Medium.
[^2]: Man wusste ja nicht, ob das nun eine größere Sache wurde, oder ob wir einfach 3-4 Wochen Pause machen und dann ganz unbeschwert weiterspielen könnten.
[^3]: Interessanterweise hat sich das schon wieder relativiert. 😄
[^4]: Das ist mittlerweile vielleicht anders und steht definitiv auf meiner Todo-Liste!
[^5]: Leider finde ich auf die Schnelle keine seriöse Seite, um dieses kleine Tool runterzuladen. Die offizielle Seite ist meines Wissens nach schon lange offline.
[^6]: Zumindest traue ich mich, irgendwas einfach mal auszuprobieren!
