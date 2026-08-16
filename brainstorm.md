# Agent X Files – Brainstorm

> Eigenständiges Singleplayer-Detektivspiel im X-Files-Stil.
> Status: Rohfassung, bewusst ausbaufähig.
> Letzter Merge: 2026-08-16 – Charakter-Details und Vertical-Slice-Logik aus dem privaten Repo übernommen.

## Kernidee

Du bist ein FBI-Agent (im Kern Mulder, aber mit eigenem Agentennamen, z. B. „Agent Krieger“).
Scully ist dein Co-Partner – du siehst sie nie persönlich, nur über den Chat / das Klapptelefon.
Sie gibt dir Aufträge, hilft bei der Falllösung und kann Informationen über Personen abfragen (kostet Budget).

Das zentrale Ziel des Spiels: herausfinden, wer du wirklich bist, wie du an den Startpunkt gekommen bist und was die Gegenstände in deiner Tasche bedeuten.

## Startszene (Amnesie)

Du wachst desorientiert in einem Gebüsch auf einem großen Parkplatz neben einer Tankstelle auf.
Dein Anzug ist etwas zerrissen. Absolute Amnesie – du weißt nicht, wer du bist und was vorher passiert ist.

### Fundstücke
- Zwei Theater-Tickets für eine Vorstellung in der Zukunft (zentrale Frage: Wem gehört die zweite Karte?)
- Eine Packung Frauenzigaretten (obwohl du glaubst, nicht zu rauchen)
- Autoschlüssel für einen Camaro (du weißt nicht, ob er dir gehört und wo er steht)
- Kugelschreiber + eine Nummer auf deinem Unterarm (gleiche Farbe wie der Stift → du hast sie selbst geschrieben; später erweist sich die Nummer als Teil des Camaro-Nummernschilds)
- Brieftasche mit ca. 300 Dollar, aber ohne Dokumente oder Ausweis
- Altes Klapptelefon (damals modern) – dein direkter Kontakt zu Scully

### Erster Kontakt
Direkt nach dem Aufwachen klingelt das Klapptelefon. Auf dem Display steht „Scully“.
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

## Charaktere (Vertical Slice – detailliert)

Jeder Charakter hat:
- eigene Visitenkarte
- eigenes Profilbild
- eigenen Steckbrief (inkl. Vorstrafen)
- **eigenes LLM**, das Persönlichkeit, Stimme und Reaktionen steuert
- individuelle Sprachausgabe (TTS, z. B. ElevenLabs Voice Cloning)

### Kassiererin (`GAS_STATION_CLERK`)

Freundlich, aufmerksam, fotografisches Gedächtnis. Beobachtet viel und merkt sich Nummernschilder, Gesichter und Details extrem genau. Hilfsbereit bei höflichem Umgang. Plaudert nicht unnötig.

**Bekannte Fakten (Engine-kontrolliert):**
- Vollständiges Nummernschild des Camaros
- Standort des Camaros auf dem großen Parkplatz hinter der Tankstelle (dritte Reihe, neben weißem Van)

**Unlock-Regel:** Spieler muss die Arm-Nummer erwähnen (Keywords: nummer, arm, unterarm, schild, nummernschild, auto, wagen, camaro). Dann gibt sie Standort + Schild frei.

### Motorradfahrer (`MOTORCYCLE_RIDER`)

Wortkarg, misstrauisch, schnell reizbar. Mitte 40, wettergegerbt, Dreitagebart, abgewetzte Lederjacke, alte Harley. Will in Ruhe rauchen. Mag keine neugierigen Typen (besonders keine, die wie Cops klingen).

**Rolle:** Reiner Risiko-NPC. Keine Story-Clues. Zweck: Gefahr, Konsequenz und Training, auf die innere Stimme zu hören.

**Aggressionsmechanismus (vollständig Engine-kontrolliert):**
- Level 0–5
- Steigt durch direkte Fragen (+1), Pushy Keywords (+2), FBI/Agent/Polizei-Erwähnung (+3), wiederholte Fragen (+2)
- Ab Level 2 warnt die innere Stimme
- Ab Level 5: Angriff → Spieler wird verprügelt, Geld weg, Flag `beaten_up`

### Innere Stimme

Zweite, intime Stimme des Spielers (Mulder-ähnlich). Kein externer NPC.
Ton: leise, nachdenklich, leicht zynisch, manchmal paranoid, immer in der zweiten Person („du“ / „ey“).

**Trigger-Kategorien (Engine-gesteuert):**
| Trigger | Kategorie | Beispiel |
|---------|-----------|----------|
| Clue / Inventory | Hint | „Ey, die Nummer auf deinem Arm… das könnte ein Nummernschild sein.“ |
| Aggression ≥ 2 | Warning | „Der wird unruhig. Lass das lieber.“ |
| Aggression ≥ 3 | Urgent Warning | „Hör auf. Der haut gleich zu.“ |
| Nach Angriff | Reaction | „Verdammt. Das Geld ist weg. Jetzt wird’s eng.“ |
| Camaro gefunden | Commentary | „Endlich. Wenigstens hast du jetzt ein Auto.“ |
| Idle | Soft Nudge | „Vielleicht solltest du nochmal die Kassiererin fragen.“ |

Max. 1–2 kurze Sätze. Eigene visuelle Darstellung und eigene TTS-Spur (leiser, mit leichtem Hall = „im Kopf“).

### Scully

Klar, professionell, ruhig, präzise. Erscheint ausschließlich über Chat / Klapptelefon.
Auftraggeberin, Informationsquelle (Steckbriefe gegen Budget), Vertrauensperson und Legitimationsinstanz.
Erfindet niemals neue Fakten – nur was die Engine freigegeben hat.

## Tankstellen-Szene (Startort)

Großer, trockener kalifornischer Parkplatz mit vielen 80er/90er-Autos. Der Camaro steht dazwischen (dritte Reihe, neben weißem Van).
Die Tankstelle ist belebt, nicht tot: helle fluoreszierende Lichter, Kassiererin hinter der Theke, Motorradfahrer draußen rauchend, ein bis zwei Leute die tanken und ansprechbar sind.
Klarer Nachthimmel, kein Regen, kein nasser Asphalt, teal-cyan Film-Look, keine lesbaren Marken/Logos.

## Erster Fall (Bellefleur, Kalifornien)

- Tankstelle liegt ca. 20 km von Bellefleur entfernt
- Basiert auf dem X-Files-Pilot: mysteriöse Todesfälle / Verschwinden junger Leute der Highschool-Klasse 1989, pinke Markierungen am Rücken, Zeitverluste, Alien-Implantat
- Beteiligte Charaktere (Beispiele): Billy Miles (Schlafwandler), Theresa Nemman, Peggy O’Dell, Dr. Jay Nemman
- Tatortbilder mit versteckten visuellen Hinweisen, Autopsie-Bilder, Profilbilder

## Zentrales Rätsel (Theater-Tickets)

Die zwei Tickets sind für eine Vorstellung in der Zukunft.
Du willst diese Vorstellung erreichen, weil dort möglicherweise die Person für die zweite Karte erscheint – und dir alles sagen kann, was dir an Informationen fehlt (wer du bist, was passiert ist).

## Bild-Prompts (Vertical Slice – Tankstelle)

Regeln für alle Bilder: klarer kalifornischer Nachthimmel, kein Regen, kein nasser Asphalt, Shop vorhanden, voller Parkplatz, etwas Leben, teal-cyan Film-Look, keine lesbaren Marken/Logos/Schriftzüge.

### Master – Establishing Shot (`station`)
```text
Cinematic night photograph of a busy 1990s rural California gas station.
DRY asphalt, no rain, no wet reflections, no puddles.
CLEAR cloudless California night sky, deep dark blue-black with a few sharp stars,
NO clouds, NO fog, NO overcast.

RIGHT: a real convenience shop — clapboard, glass door, large windows glowing
cold fluorescent teal-white, checkout counter and shelves visible,
one clerk silhouette inside.

FRONT: canopy over two pumps. A customer in a denim jacket fuels a beige sedan.
A motorcycle parked at the other pump.

BEHIND and BESIDE the shop: a PACKED parking lot, at least three full rows of
1980s/1990s cars, pickups, one white cargo van, many vehicles, lived-in, not empty.

Teal-cyan fluorescent film grade, light grain, X-Files America but alive.
No readable brand names, no logos, no sign lettering.
Wide 16:9 establishing shot.
```

### Kassiererin (`clerk`)
```text
IMAGE_0 is the locked location. IMAGE_1 is the clerk's face.
Photograph her INSIDE this shop behind the checkout, fluorescent teal-white
interior, shelves, register. Head and shoulders.
Same clear night visible through the window behind/beside her if any sky shows —
no clouds. Dry, no rain. Film grain matching IMAGE_0.
No nametag text, no logos.
```

### Motorradfahrer (`rider`)
```text
IMAGE_0 is the locked location. IMAGE_1 is the biker.
Put him at a pump in front of THIS busy shop, packed lot behind,
clear cloudless California night sky, dry asphalt, no rain, no clouds.
Polaroid close portrait, leather jacket, cigarette, weathered.
Same teal film grade. No logos, no text.
```

### Camaro im Parkplatz (`camaro`)
```text
Keep this exact shop, packed lot, clear starry sky, dry asphalt, people, teal lights.
Park one black 1990s Camaro coupe in the lot beside a white van,
third row if possible.
No extra rain, no clouds, no new logos or readable text.
```

### Startbild / OG (`og`) – Tickets + Schlüssel + Arm
```text
Keep this exact busy dry California night gas station with shop, packed lot,
clear starry sky, no clouds, no rain.
Add in the foreground on dry cracked asphalt:
two worn blank theater tickets, a car key and a partially visible handwritten number on a forearm.
No readable words. Same teal film grade.
```

## Technische Skizze (grob)

- Frontend: Next.js (responsive, Handy-first)
- Backend: FastAPI
- Pro Charakter eigenes LLM (Persönlichkeit + Dialog)
- Voice: ElevenLabs (oder vergleichbar) für individuelle Stimmen (Scully, Mulder, innere Stimme, alle NPCs)
- Bildgenerierung für stimmige Tatort- und Profilbilder
- Datenmodell: Orte, Charaktere, Fälle, Budget, Vertrauen/Scully-Status
- Engine entscheidet Timing, Buttons und freigegebene Fakten – LLM formuliert nur

## Offene Punkte / nächste Schritte

- Vertrauenssystem mit Scully ausbauen
- Moralische Entscheidungen mit Langzeit-Konsequenzen
- Genauere Definition der 30 Orte und ihrer Verflechtungen
- Voice-Samples und Prompt-Engineering pro Charakter
- Ersten spielbaren Prototyp (Tankstelle + Camaro + erster Fall)
- Bild-Prompts für weitere Orte analog zur Tankstelle festhalten
- Automatisierung des Merges private → public (siehe unten)

## Merge-Automatisierung (Vorschlag)

Damit künftige Änderungen aus dem privaten Vertical-Slice sauber ins öffentliche Brainstorm fließen:

1. Einfaches Script (lokal oder als GitHub Action):
   - Liest die relevanten Dateien aus `Agent-X-Files/vertical-slice/`
   - Extrahiert die Abschnitte (Charaktere, Trigger, Unlock-Regeln)
   - Merged sie strukturiert in `Agent-X-Files-Idea/brainstorm.md`
2. Optional: GitHub Action, die bei Push auf main des privaten Repos getriggert wird und einen PR im öffentlichen Repo erstellt.

Aktuell manuell gepflegt – Automatisierung kann als nächstes Schritt umgesetzt werden.

---

*Reine Spielidee – eigenständiges Projekt.*
