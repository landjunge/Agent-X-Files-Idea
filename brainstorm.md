# Agent X Files – Brainstorm

> Eigenständiges Singleplayer-Detektivspiel im X-Files-Stil.
> Status: Rohfassung, bewusst ausbaufähig.

## Kernidee

Du bist ein FBI-Agent (im Kern Mulder, aber mit eigenem Agentennamen, z. B. „Agent Krieger“).
Scully ist dein Co-Partner – du siehst sie nie persönlich, nur über den Chat.
Sie gibt dir Aufträge, hilft bei der Falllösung und kann Informationen über Personen abfragen (kostet Budget).

Das zentrale Ziel des Spiels: herausfinden, wer du wirklich bist, wie du an den Startpunkt gekommen bist und was die Gegenstände in deiner Tasche bedeuten.

## Startszene (Amnesie)

Du wachst desorientiert in einem Gebüsch auf einem Parkplatz neben einer Tankstelle auf.
Dein Anzug ist etwas zerrissen. Absolute Amnesie – du weißt nicht, wer du bist und was vorher passiert ist.

### Fundstücke in deinen Taschen
- Zwei Theater-Tickets für eine Vorstellung in der Zukunft (zentrale Frage: Wem gehört die zweite Karte?)
- Eine Packung Frauenzigaretten (obwohl du glaubst, nicht zu rauchen)
- Autoschlüssel für einen Camaro (du weißt nicht, ob er dir gehört und wo er steht)
- Kugelschreiber + eine Nummer auf deinem Unterarm (gleiche Farbe wie der Stift → du hast sie selbst geschrieben; später erweist sich die Nummer als Teil des Camaro-Nummernschilds)
- Brieftasche mit ein paar Dollars, aber ohne Dokumente

### Erster Kontakt
Direkt nach dem Aufwachen klingelt das Handy: Scully.
Sie fragt: „Hallo, weißt du, wer ich bin?“
- Antwort „Nein“ → „Okay, tut mir leid, dann ruf ich nochmal später an.“
- Du musst dich mit dem Namen „Scully“ legitimieren.
- Danach erkennt sie dich und gibt dir den ersten Auftrag.

### Innere Stimme
Du hast eine zweite, innere Stimme (Mulder-ähnlich), die dich manchmal richtig hinweist und manchmal in die Irre führt.
Beispiel: „Ey, da ist ein Parkplatz. Vielleicht ist die Nummer auf deinem Unterarm ein Nummernschild. Check das doch mal.“

Sobald du den Camaro mit dem passenden Schlüssel öffnest, meldet sich Scully sofort: „Okay, du hast zumindest den Camaro gefunden, also weiß ich, wer du bist.“

## Dialog mit der inneren Stimme

Die innere Stimme ist ein eigenständiger Charakter mit eigenem Eintrag im Log, eigener Farbe und eigener Stimme.
Sie stellt dir gezielte Fragen, um dich weiterzubringen.
Dazu erscheinen direkt unter ihrer Sprachausgabe im Chatfenster Antwort-Buttons (z. B. Ja/Nein oder kontextbezogene Optionen).
Die Engine steuert die verfügbaren Buttons basierend auf dem aktuellen Spielzustand und den festen Fakten.
Das LLM formuliert nur den Text der inneren Stimme.

Ziel: Strukturierte Entscheidungen, die verhindern, dass man stecken bleibt – und gleichzeitig ein persönlicher, dialogischer Austausch mit der inneren Stimme.

## Barrierefreiheit

Das Spiel ist vollständig per TTS (Text-to-Speech) nutzbar.
Für Legastheniker wird parallel zum gesprochenen Text immer auch der lesbare Text im Chatfenster angezeigt.
So können Spieler je nach Stärke besser hören oder lesen.

## Spielwelt

- Interaktive Amerika-Karte mit ca. 30 Punkten/Städten
- Letzter Punkt: Area 51 (basiert auf der Episode „Deep Throat“ – das, was später passiert, ist eigentlich schon vorher vorgefallen)
- Die Punkte sind miteinander verwoben: Manchmal musst du zurückfahren, weil eine spätere Information einen früheren Hinweis erst verständlich macht

## Budget-System

- Jeder Ort hat ein Budget für Reisen, Ermittlungen und Abfragen
- Kosten: Reisen, Steckbriefabfragen bei Scully, Bestechung, jemanden auf einen Drink einladen
- Einnahmen: Falllösung, Zufallsereignisse (nette Leute, Mitfahrgelegenheit, Anhalter etc.)
- Bestechung und Drinks werden direkt im Chat abgerechnet

## UI-Konzept (Handy-tauglich)

- **Header oben**: Visitenkarten der verfügbaren Personen am aktuellen Ort (1–10, je nach Ort)
- **Linke Sidebar**: Interaktive Karte (zoombar, touch-freundlich). Aufträge und besuchte Orte werden markiert
- **Mitte**: Chat mit der aktuellen Person / Scully / innerer Stimme
- **Rechte Sidebar**: Historie / Log der bisherigen Ermittlungen
- Am Ortseingang erscheinen unten Bilder der Gebäude (Kneipe, Polizeistation, Tankstelle etc.). Klick öffnet den Innenbereich und die dazugehörigen Charaktere

## Charaktere

Jeder Charakter hat:
- eigene Visitenkarte
- eigenes Profilbild
- eigenen Steckbrief (inkl. Vorstrafen)
- **eigenes LLM**, das Persönlichkeit, Stimme und Reaktionen steuert
- individuelle Sprachausgabe (TTS, z. B. ElevenLabs Voice Cloning)

Nebenfiguren (Barkeeper, Penner, Kassiererin etc.) spielen keine zentrale Rolle, können aber wichtige Hinweise geben, wenn man die richtigen Fragen stellt oder ihre Schwächen kennt.

### Beispiel: Tankstelle (Startort)
- **Motorradfahrer** (Mitte 40, wettergegerbt, Dreitagebart, abgewetzte Lederjacke, alte Harley). Wortkarg, misstrauisch, reizbar. Bei zu vielen Fragen droht er mit Prügel und nimmt dir das restliche Geld (300–400 $). Danach musst du den Camaro „schwarz“ tanken → Polizei-Risiko.
- **Kassiererin** mit fotografischem Gedächtnis. Freundlich, beobachtet viel. Erkennt an deinem Unterarm das Nummernschild des Camaro und gibt die entscheidende Auskunft, wenn man sie richtig fragt.
- Weitere mögliche Personen: Tankstellen-Betreiber, Lkw-Fahrer, Penner etc.

## Erster Fall (Bellefleur, Kalifornien)

- Tankstelle liegt ca. 20 km von Bellefleur entfernt
- Basiert auf dem X-Files-Pilot: mysteriöse Todesfälle / Verschwinden junger Leute der Highschool-Klasse 1989, pinke Markierungen am Rücken, Zeitverluste, Alien-Implantat
- Beteiligte Charaktere (Beispiele): Billy Miles (Schlafwandler), Theresa Nemman, Peggy O’Dell, Dr. Jay Nemman
- Tatortbilder mit versteckten visuellen Hinweisen, Autopsie-Bilder, Profilbilder

## Zentrales Rätsel (Theater-Tickets)

Die zwei Tickets sind für eine Vorstellung in der Zukunft.
Du willst diese Vorstellung erreichen, weil dort möglicherweise die Person für die zweite Karte erscheint – und dir alles sagen kann, was dir an Informationen fehlt (wer du bist, was passiert ist).

## Technische Skizze (grob)

- Frontend: Next.js (responsive, Handy-first)
- Backend: FastAPI
- Pro Charakter eigenes LLM (Persönlichkeit + Dialog)
- Voice: ElevenLabs (oder vergleichbar) für individuelle Stimmen (Scully, Mulder, innere Stimme, alle NPCs)
- Bildgenerierung für stimmige Tatort- und Profilbilder
- Datenmodell: Orte, Charaktere, Fälle, Budget, Vertrauen/Scully-Status

## Offene Punkte / nächste Schritte

- Vertrauenssystem mit Scully ausbauen
- Moralische Entscheidungen mit Langzeit-Konsequenzen
- Genauere Definition der 30 Orte und ihrer Verflechtungen
- Voice-Samples und Prompt-Engineering pro Charakter
- Ersten spielbaren Prototyp (Tankstelle + Camaro + erster Fall)

---

*Reine Spielidee – eigenständiges Projekt.*
