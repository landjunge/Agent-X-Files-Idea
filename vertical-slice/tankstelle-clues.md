# Tankstelle – Clues & Unlock Rules (Kassiererin)

> Vertical Slice – erste konkrete Definition

## Kassiererin (`GAS_STATION_CLERK`)

### Persönlichkeit (für LLM System Prompt)
Freundlich, aufmerksam, hat ein fotografisches Gedächtnis. Sie beobachtet viel und merkt sich Nummernschilder, Gesichter und Details extrem genau. Sie ist hilfsbereit, wenn man sie höflich und respektvoll anspricht. Sie plaudert nicht unnötig über Dinge, die sie nicht weiß oder die irrelevant sind.

### Permanent bekannte Fakten (known_clues)
- `CAMARO_LICENSE_PLATE` – sie kennt das vollständige Nummernschild des Camaros
- `CAMARO_LOCATION` – sie weiß, wo der Camaro auf dem großen Parkplatz hinter der Tankstelle steht

### Clues, die der Spieler mitbringt / entdeckt

```ts
{
  id: "ARM_NUMBER",
  title: "Nummer auf dem Unterarm",
  description: "Eine handgeschriebene Nummer auf dem Unterarm des Spielers. Die Tinte hat die gleiche Farbe wie der Kugelschreiber in seiner Tasche.",
  discovered: true,          // Spieler startet damit
  is_red_herring: false
}

{
  id: "CAMARO_LICENSE_PLATE",
  title: "Camaro Nummernschild",
  description: "Vollständiges Nummernschild des Camaros (z.B. CA-4827-X). Die Nummer auf dem Arm des Spielers ist ein Teil davon.",
  discovered: false,
  required_clues: ["ARM_NUMBER"]
}

{
  id: "CAMARO_LOCATION",
  title: "Standort des Camaros",
  description: "Der Camaro steht auf dem großen Parkplatz hinter der Tankstelle, dritte Reihe von links, neben einem weißen Van.",
  discovered: false,
  required_clues: ["ARM_NUMBER"]
}
```

### Unlock Rule (Game Engine kontrolliert)

```ts
{
  npc_id: "GAS_STATION_CLERK",
  required_player_clues: ["ARM_NUMBER"],
  required_keywords: [
    "nummer",
    "arm",
    "unterarm",
    "schild",
    "nummernschild",
    "auto",
    "wagen",
    "camaro"
  ],
  reveals_clue: "CAMARO_LOCATION",
  also_reveals: ["CAMARO_LICENSE_PLATE"],
  cost: 0
}
```

### Verhalten der Engine

1. Spieler spricht mit der Kassiererin und erwähnt eines der Keywords **und** besitzt bereits `ARM_NUMBER`.
2. Engine setzt `CAMARO_LOCATION` und `CAMARO_LICENSE_PLATE` auf `discovered: true`.
3. Dem LLM wird im restricted context mitgeteilt:
   - Die Kassiererin darf jetzt den Standort und das vollständige Schild nennen.
   - Sie soll natürlich und freundlich antworten.
   - Sie darf **keine** weiteren Fakten erfinden (kein Fahrer, keine Uhrzeit, keine Geschichte, es sei denn sie werden später explizit hinzugefügt).

### Beispiel-Dialog (nach Unlock)

Spieler: „Ich habe da eine Nummer auf dem Arm... 4827 oder so.“

Kassiererin: „Moment mal... die Nummer kommt mir bekannt vor. Das ist ein Teil vom Schild von dem schwarzen Camaro. Der steht hinten auf dem großen Parkplatz, dritte Reihe, direkt neben dem weißen Van.“

---

*Nur die Kassiererin. Motorradfahrer und weitere Clues kommen als Nächstes.*
