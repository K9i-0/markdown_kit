# markdown_kit

Flutter package that renders Markdown for AI chat: streaming-safe parsing and text selection across blocks. The public API is what `lib/markdown_kit.dart` lists with `show`; everything else under `lib/src/` is internal. `example/` is a three-tab demo (chat, editor, showcase) that also builds for the web and is deployed to GitHub Pages.

Design decisions, compatibility policy, the release procedure and known limits are in [doc/architecture.md](doc/architecture.md) (Japanese). Read it before changing the parser, the selection engine or the public API.

## Setup and verification

Use Flutter 3.50.1 from `.mise.toml`. The published floor is Flutter 3.50.0 / Dart 3.14; lower it only after the tests pass on that version.

```sh
flutter pub get
(cd example && flutter pub get)
flutter analyze --fatal-infos
sh tool/check_format.sh
flutter test
(cd example && flutter test)
```

CI (`.github/workflows/check_pr.yml`) also builds the example for the web, runs `flutter pub publish --dry-run`, and repeats the tests on Flutter 3.50.0.

## Working agreements

- `lib/` imports only `package:flutter/widgets.dart` and friends: no `material.dart`, `cupertino.dart` or `material_ui`. Appearance and actions come in through builders and callbacks.
- Public API changes follow semantic versioning. `public_member_api_docs` is on, so every public member needs a doc comment.
- Users import the barrel only. The package's own tests may import `src/`; the example may not.
- Maintainers commit directly on `main` with Conventional Commits and push without a PR. A `main` push runs checks and does not publish.
- Publish only when a release is requested, by pushing a `markdown_kit-v<version>` tag after bumping `pubspec.yaml` and `CHANGELOG.md`. Do not run a manual publish command.
- `test/commonmark_spec/spec.json` is CC BY-SA 4.0 and stays unmodified; see `NOTICE.md`.
- `tool/promo/` holds the sources of the promo video and is excluded from the pub.dev archive.
