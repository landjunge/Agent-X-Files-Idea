# Tankstelle – Aggressionsmechanismus (Motorradfahrer)

> Vertical Slice – detaillierte, Engine-kontrollierte Definition

## Motorradfahrer (`MOTORCYCLE_RIDER`)

### Persönlichkeit (Basis für LLM System Prompt)
Wortkarg, misstrauisch, schnell reizbar. Mitte vierzig, wettergegerbte Haut, Dreitagebart, abgewetzte Lederjacke. Fährt eine alte Harley. Will in Ruhe seine Zigarette rauchen. Mag keine neugierigen Typen – besonders keine, die wie Cops oder Agenten klingen.

### Rolle
**Reiner Risiko-NPC.** Keine wichtigen Story-Clues. Sein Zweck ist Gefahr, Konsequenz und das Training, auf die innere Stimme zu hören.

---

## Aggressionsmechanismus (vollständig Engine-kontrolliert)

### State-Variablen

```ts
{
  aggression_level: number;      // 0–5
  question_count: number;        // Anzahl der Fragen in dieser Unterhaltung
  has_been_warned: boolean;      // hat er schon einmal klar gedroht?
  is_hostile: boolean;           // true ab Threshold
}
```

### Startwerte
- `aggression_level = 0`
- `question_count = 0`
- `has_been_warned = false`
- `is_hostile = false`

### Wie Aggression steigt (Engine bewertet jede Spieler-Nachricht)

| Auslöser                              | Erhöhung |
|---------------------------------------|----------|
| Neutrale / höfliche Aussage           | +0       |
| Direkte Frage                         | +1       |
| Pushy Keywords (siehe Liste unten)    | +2       |
| Wiederholte Frage / gleiches Thema    | +2       |
| erwähnung von FBI / Agent / Polizei   | +3       |
| Drohender oder fordernder Ton         | +2       |

**Pushy Keywords (Beispiele):**
`wer bist du`, `was weißt du`, `was hast du gesehen`, `erzähl`, `gib mir`, `antwort`, `camaro`, `auto`, `nummernschild`, `fbi`, `agent`, `polizei`, `untersuchen`

Die Engine klassifiziert die Nachricht **vor** dem LLM-Call und erhöht den Wert. Das LLM bekommt nur den aktuellen Level mitgeteilt.

### Aggression Levels und erlaubtes Verhalten

| Level | Zustand          | Erlaubtes LLM-Verhalten                              | Innere Stimme                          |
|-------|------------------|------------------------------------------------------|----------------------------------------|
| 0     | Neutral             | Einsilbig, genervt, aber noch geduldig               | –                                      |
| 1     | Genervt          | Kurze, abweisende Antworten                          | –                                      |
| 2     | Gereizt          | Deutlich genervt, erste Warnung                      | „Der wird unruhig. Sei vorsichtig.“    |
| 3     | Drohend          | Klare Drohung („Hör auf zu fragen…“)                 | „Ey, der meint das ernst. Lass es.“    |
| 4     | Hochaggressiv    | Letzte Warnung, greift gleich an                     | „Hör sofort auf. Der haut gleich zu.“  |
| 5     | Angriff          | Kein Dialog mehr – Engine übernimmt die Konsequenz   | –                                      |

**Threshold = 4** (bei Level 4 droht er das letzte Mal, bei 5 greift er an).

### Konsequenz bei Angriff (Level 5)

```ts
{
  sets_flags: ["beaten_up"],
  budget_change: "set_to_0",           // nimmt das restliche Geld
  is_hostile: true,
  conversation_ends: true,
  message_to_player: "Der Motorradfahrer packt dich am Kragen, schlägt dir mehrmals ins Gesicht und nimmt dir das restliche Geld ab. Dann stößt er dich weg und setzt sich wieder hin.",
  later_consequence: "Ohne Geld muss der Camaro schwarz getankt werden → erhöhtes Polizei-Risiko auf dem Weg nach Bellefleur"
}
```

### Restricted Context für das LLM (wird von der Engine gebaut)

Das LLM bekommt **immer** den aktuellen Aggression-Level mitgeteilt:

```
SYSTEM:
Du bist der Motorradfahrer. Aktueller Aggression-Level: {aggression_level}

Verhaltensregeln für diesen Level:
{level_instructions}

Du darfst KEINE Informationen über den Camaro, Nummernschilder, den Spieler oder die Geschichte erfinden.
Bleibe wortkarg und in Charakter.
```

### Wichtige Design-Entscheidungen

1. **Die Engine entscheidet alles.** Das LLM formuliert nur den Ton, der zum aktuellen Level passt.
2. Aggression steigt **innerhalb einer Unterhaltung** und bleibt bestehen, solange der Spieler am Ort ist.
3. Es gibt **keine echten Clues** von diesem NPC im ersten Vertical Slice.
4. Die innere Stimme wird von der Engine getriggert und erscheint als separate Nachricht (nicht vom Motorradfahrer selbst).

---

*Dieser Mechanismus ist deterministisch, vorhersehbar und leicht implementierbar. Er lehrt den Spieler Risiko und das Zuhören auf die innere Stimme.*
