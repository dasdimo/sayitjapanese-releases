# Say It In Japanese

*English below.*

Eine Fabric-Mod für **Minecraft 26.3**: Jedes neue Item, das du bekommst, musst du laut auf Japanisch sagen, bevor der
Countdown abläuft. Ab 80 % ist es für immer freigeschaltet, sonst löscht die Mod es aus deinem Inventar. Über jedem
Kanji steht die Lesung in Hiragana, und statt Japanisch geht auch jede andere Minecraft-Sprache.

## So bekommst du die Mod

Über den **[DasDimo Launcher](https://github.com/dasdimo/dasdimo-launcher-releases)**: Er legt die Mod in dein
Minecraft-Profil (Minecraft Launcher, Modrinth App, NoRisk Client, CurseForge, Prism), hält sie aktuell und zeigt dir,
was noch fehlt.

Wer Mods selbst verwaltet: die `.jar` aus dem
[neuesten Release](https://github.com/dasdimo/sayitjapanese-releases/releases/latest) in den `mods`-Ordner legen, dazu
Fabric API und die Spracherkennung (siehe unten).

## Was du brauchst

- Minecraft **26.3** mit **Fabric Loader 0.20.1** oder neuer (Java 25 bringt Minecraft selbst mit)
- **[Fabric API](https://modrinth.com/mod/fabric-api)** 0.165.0+26.3 oder neuer
- empfohlen: **[Simple Voice Chat](https://modrinth.com/plugin/simple-voice-chat)** (für 26.3 bisher als Beta). Ohne
  Voice Chat nimmt die Mod selbst auf, nur während einer Challenge.
- eine **Spracherkennung**: whisper.cpp auf deinem PC (kostenlos, siehe unten) oder ein OpenAI-Schlüssel (kostet Geld)

Im Multiplayer braucht der Server die Mod und Fabric API, und jeder Spieler die Mod.

## Spracherkennung einrichten (whisper.cpp, Windows)

1. Bei [whisper.cpp → Releases](https://github.com/ggml-org/whisper.cpp/releases) das neueste Release öffnen und die
   Zip laden: mit NVIDIA-Grafikkarte die mit **cuda** im Namen (ca. 700 MB, deutlich schneller), sonst
   `whisper-bin-x64.zip`. Nach `C:\whisper` entpacken. Darin liegt `whisper-server.exe`.
2. Ein Sprachmodell von [Hugging Face](https://huggingface.co/ggerganov/whisper.cpp/tree/main) nach `C:\whisper\models`
   laden:

   | Modell | Größe | Japanisch |
   |---|---|---|
   | `ggml-large-v3-turbo.bin` | ca. 1,6 GB | gut – Empfehlung mit Grafikkarte |
   | `ggml-small.bin` | ca. 0,5 GB | brauchbar – läuft auch nur auf dem Prozessor |

3. Server starten und das Fenster offen lassen, solange du spielst:

   ```
   C:\whisper\whisper-server.exe -m C:\whisper\models\ggml-large-v3-turbo.bin --host 127.0.0.1 --port 8080 -l ja
   ```

   Tipp: Diese Zeile in eine Datei `C:\whisper\start-whisper.bat` schreiben, dann reicht ein Doppelklick.
4. Im Spiel `/sayitclient mictest` eingeben: Die Mod nimmt 4 Sekunden auf und zeigt, was sie verstanden hat.

**Statt whisper.cpp:** In `config/sayitjapanese.json` `"sttBackend": "openai"` und `"openAiApiKey": "sk-…"`
eintragen. Der Schlüssel steht nur in dieser Datei – teile sie nie.

**Hört `mictest` nur Stille?** In den Windows-Einstellungen unter *Datenschutz und Sicherheit → Mikrofon* „Desktop-Apps
Zugriff auf das Mikrofon erlauben“ einschalten. Mit `/sayitclient devices` siehst du deine Mikrofone. Einen Teil des
Namens kannst du in `config/sayitjapanese.json` bei `microphoneDevice` eintragen.

## Einstellungen (`config/sayitjapanese.json`)

| Schlüssel | Standard | Bedeutung |
|---|---|---|
| `timeLimitSeconds` | `10` | Countdown pro Item |
| `successThreshold` | `0.8` | ab diesem Wert ist ein Versuch richtig (0.8 = 80 %) |
| `exemptItems` | `[]` | Items ohne Challenge, z. B. `["minecraft:wooden_sword"]` |
| `targetLanguage` | `"ja_jp"` | Zielsprache als Minecraft-Code: `de_de`, `fr_fr`, `es_es`, `ko_kr`, … |
| `showFurigana` | `true` | Hiragana-Lesung über den Kanji |
| `challengeInCreative` | `false` | Challenges auch im Kreativmodus |

Spielregeln (Zeit, Schwelle, Ausnahmen) kommen vom Server, Sprache und Mikrofon von jedem Spieler selbst. Eine eigene
Lesung für ein Item kannst du in `config/sayitjapanese-overrides.json` eintragen, z. B.
`{ "ja_jp": { "minecraft:stick": "ki no bou" } }`.

## Befehle

| Befehl | Was |
|---|---|
| `/sayit stats` | deine Statistik: gelernte Wörter, gelöschte Items, schwerste Wörter |
| `/sayit stats export` | Statistik als JSON und CSV speichern |
| `/sayit test <item>` | Übungs-Challenge, löscht nichts |
| `/sayit toggle` | Mod für dich an oder aus (Weltbesitzer oder OP) |
| `/sayit unlock <item>` | Item sofort freischalten (Weltbesitzer oder OP) |
| `/sayit reset` | eigene Freischaltungen und Statistik löschen (Weltbesitzer oder OP) |
| `/sayitclient mictest` | 4 Sekunden aufnehmen, Lautstärke und Erkanntes zeigen |
| `/sayitclient devices` | Mikrofone auflisten |
| `/sayitclient demo` | Vorführung der Anzeige, ohne Mikrofon |

## Lizenzen

Die Mod steht unter der MIT-Lizenz. Sie enthält **Kuromoji** 0.9.0 (Apache License 2.0, © Atilika Inc. und
Mitwirkende) mit Daten aus **mecab-ipadic** 2.7.0 (Hinweis von NAIST/ICOT). Die vollständigen Texte liegen in der
`.jar` (`LICENSE_say-it-in-japanese`, `THIRD_PARTY_NOTICES.md`). whisper.cpp und die Sprachmodelle lädst du selbst; sie
stehen unter ihren eigenen Lizenzen.

Fehler und Wünsche bitte direkt an DasDimo schicken.

---

# Say It In Japanese (English)

A Fabric mod for **Minecraft 26.3**: every new item you get must be said out loud in Japanese before the countdown
runs out. At 80 % or better it is unlocked for good, otherwise the mod deletes it from your inventory. The reading in
hiragana sits above every kanji, and instead of Japanese you can pick any other Minecraft language.

## How to get it

Through the **[DasDimo Launcher](https://github.com/dasdimo/dasdimo-launcher-releases)**: it puts the mod into your
Minecraft profile (Minecraft Launcher, Modrinth App, NoRisk Client, CurseForge, Prism), keeps it up to date and shows
what else you need.

If you manage your mods yourself: put the `.jar` from the
[latest release](https://github.com/dasdimo/sayitjapanese-releases/releases/latest) into your `mods` folder, together
with Fabric API and the speech recognition (see below).

## What you need

- Minecraft **26.3** with **Fabric Loader 0.20.1** or newer (Minecraft brings Java 25 itself)
- **[Fabric API](https://modrinth.com/mod/fabric-api)** 0.165.0+26.3 or newer
- recommended: **[Simple Voice Chat](https://modrinth.com/plugin/simple-voice-chat)** (a beta for 26.3 so far). Without
  it the mod records by itself, only during a challenge.
- **speech recognition**: whisper.cpp on your PC (free, see below) or an OpenAI key (costs money)

In multiplayer the server needs the mod and Fabric API, and every player needs the mod.

## Setting up speech recognition (whisper.cpp, Windows)

1. Open the latest release on [whisper.cpp → Releases](https://github.com/ggml-org/whisper.cpp/releases) and get the
   zip: with an NVIDIA graphics card the one with **cuda** in its name (about 700 MB, much faster), otherwise
   `whisper-bin-x64.zip`. Extract it to `C:\whisper`; it contains `whisper-server.exe`.
2. Put a speech model from [Hugging Face](https://huggingface.co/ggerganov/whisper.cpp/tree/main) into
   `C:\whisper\models`:

   | Model | Size | Japanese |
   |---|---|---|
   | `ggml-large-v3-turbo.bin` | about 1.6 GB | good – recommended with a graphics card |
   | `ggml-small.bin` | about 0.5 GB | usable – also runs on the processor alone |

3. Start the server and keep the window open while you play:

   ```
   C:\whisper\whisper-server.exe -m C:\whisper\models\ggml-large-v3-turbo.bin --host 127.0.0.1 --port 8080 -l ja
   ```

   Tip: put this line into a file `C:\whisper\start-whisper.bat`, then a double click is enough.
4. Type `/sayitclient mictest` in game: the mod records 4 seconds and shows what it understood.

**Instead of whisper.cpp:** set `"sttBackend": "openai"` and `"openAiApiKey": "sk-…"` in `config/sayitjapanese.json`.
The key is only in that file – never share it.

**`mictest` hears only silence?** In Windows settings under *Privacy & security → Microphone* turn on “Let desktop apps
access your microphone”. `/sayitclient devices` lists your microphones; put part of the name into `microphoneDevice` in
`config/sayitjapanese.json`.

## Settings (`config/sayitjapanese.json`)

| Key | Default | Meaning |
|---|---|---|
| `timeLimitSeconds` | `10` | countdown per item |
| `successThreshold` | `0.8` | a try is right from this value (0.8 = 80 %) |
| `exemptItems` | `[]` | items without a challenge, e.g. `["minecraft:wooden_sword"]` |
| `targetLanguage` | `"ja_jp"` | target language as a Minecraft code: `de_de`, `fr_fr`, `es_es`, `ko_kr`, … |
| `showFurigana` | `true` | hiragana reading above the kanji |
| `challengeInCreative` | `false` | challenges in creative mode too |

Game rules (time, threshold, exemptions) come from the server, language and microphone from each player. Your own
reading for an item goes into `config/sayitjapanese-overrides.json`, e.g.
`{ "ja_jp": { "minecraft:stick": "ki no bou" } }`.

## Commands

| Command | What |
|---|---|
| `/sayit stats` | your statistics: learned words, deleted items, hardest words |
| `/sayit stats export` | save your statistics as JSON and CSV |
| `/sayit test <item>` | practice challenge, deletes nothing |
| `/sayit toggle` | turn the mod on or off for you (world owner or OP) |
| `/sayit unlock <item>` | unlock an item right away (world owner or OP) |
| `/sayit reset` | delete your unlocks and statistics (world owner or OP) |
| `/sayitclient mictest` | record 4 seconds, show the level and what was understood |
| `/sayitclient devices` | list microphones |
| `/sayitclient demo` | demo of the display, no microphone needed |

## Licenses

The mod is under the MIT license. It contains **Kuromoji** 0.9.0 (Apache License 2.0, © Atilika Inc. and
contributors) with data from **mecab-ipadic** 2.7.0 (NAIST/ICOT notice). The full texts are inside the `.jar`
(`LICENSE_say-it-in-japanese`, `THIRD_PARTY_NOTICES.md`). You download whisper.cpp and the speech models yourself;
they come under their own licenses.

Bugs and wishes: please send them to DasDimo directly.
