# Dino Run

A small endless runner in the style of Chrome's offline dinosaur game, written in Flutter with the Flame game engine.

I built it for a talk at Flutter Ottawa, "From Code to Play: Developing Dino Run using Flutter and Flame" ([event page](https://www.meetup.com/flutter-meetup-group/events/301410386/?eventOrigin=group_past_events)), held online on June 26, 2024. Over 30 people attended. The session covered how the game was built with Flutter and Flame and ended with a live demo.

## How it plays

- Press the space bar to jump. There is no touch control yet, so you need a keyboard.
- Angry pigs walk along the ground and bats fly in at random heights. A new enemy spawns every 2 seconds.
- You start with 5 lives (shown as hearts). Getting hit costs one life and plays a short hit animation.
- You score a point for every enemy that makes it off the left edge of the screen.
- There is a main menu, a pause menu (Resume, Restart, Exit) and a game over screen. The game pauses itself when the app goes to the background.
- The game runs at a fixed 360x180 resolution, in landscape and full screen, with a six-layer parallax background, background music and jump/hit sound effects.

## Stack

- Flutter, Dart
- [Flame](https://pub.dev/packages/flame) 1.17.0 for the game loop, sprites, parallax and collision detection
- flame_audio 2.10.1 for music and sound effects
- provider 6.1.2 to push score and lives from the game into the Flutter overlay widgets

It was written against Flutter 3.19 (Dart 3.3.4). Flame and the other packages are pinned to the versions above, so a much newer Flutter SDK may need those bumped.

## Running it

```bash
git clone https://github.com/rohanjariwala03/Dino-Run.git
cd Dino-Run
flutter pub get
flutter run
```

The repo includes the standard Android, iOS, web, macOS, Windows and Linux runners. Since jumping is keyboard-only, desktop or web (`flutter run -d chrome`) is the easiest way to play.

## Project structure

```
lib/
  main.dart              App entry, GameWidget setup and overlay registration
  game/
    dino_run.dart        FlameGame: asset loading, parallax, keyboard input, game over check
    dino.dart            Player sprite, gravity, jump and hit handling
    enemy.dart           Enemy movement and scoring
    enemy_manager.dart   Spawns a random enemy on a timer
    audio_manager.dart   Wrapper around flame_audio
  models/                PlayerData (score, lives) and EnemyData
  widgets/               Main menu, HUD, pause menu and game over overlays
assets/                  Sprites, parallax layers, audio and the Audiowide font
```

## Credits

The sprites, background and audio are free assets from itch.io and are not mine. Authors and links are listed in [assets/images/readme.md](assets/images/readme.md) and [assets/audio/readme.md](assets/audio/readme.md). The Audiowide font is under the SIL Open Font License ([OFL.txt](assets/fonts/Audiowide/OFL.txt)).
