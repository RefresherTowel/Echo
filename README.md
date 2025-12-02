# Echo

![Echo icon](./echo_icon.png)

*Hear what your game is telling you*

Echo is a lightweight debug logger for GameMaker. Your game is already telling you what is happening; Echo helps you actually hear it. Swap scattered `show_debug_message` calls for level based logs with tags, optional stack traces, and a history buffer you can dump to a file when something gets weird.

This repository is for the Echo framework landing page and issue tracker.

## Features at a glance

- Drop in, macro controlled debug logging:
  - `#macro ECHO_DEBUG_ENABLED 1` to enable Echo globally.
- Log levels so you can control noise:
  - `NONE`, `SEVERE_ONLY`, `COMPREHENSIVE`, `COMPLETE`.
- Urgency levels on each message:
  - `INFO`, `WARNING`, `SEVERE`.
- Optional stack trace capture for severe errors or in `COMPLETE` mode.
- Tag support on every log call:
  - Single tag or array of tags.
  - Runtime filtering with `EchoDebugSetTags` so you can focus on one system at a time.
- Rolling log history in memory:
  - Configurable max size.
  - Read, clear, or dump to a timestamped text file.
- Simple API:
  - `EchoDebug`, `EchoDebugInfo`, `EchoDebugWarn`, `EchoDebugSevere`.
  - Helper functions to get and set log level, history size, and tag filters.
- Integrates cleanly with other frameworks:
  - Statement and future RefresherTowel frameworks use Echo for their own debugging hooks.

## Quick start

Enable Echo with a macro, then log messages with different levels and tags.
```js
// In a global script or config
#macro ECHO_DEBUG_ENABLED 1

// Somewhere in your code
EchoDebugInfo("Player spawned", "Player");

EchoDebugWarn("Health is low", ["Player", "Combat"]);

if (hp <= 0) {
    EchoDebugSevere("Player died unexpectedly", ["Player", "Error"]);
}
```
Control how much you see by changing the debug level:
```js
// Only SEVERE messages will print
EchoDebugSetLevel(__ECHO_eDebugLevel.SEVERE_ONLY);

// Show WARNING and SEVERE (default)
EchoDebugSetLevel(__ECHO_eDebugLevel.COMPREHENSIVE);

// Show everything, with stack traces
EchoDebugSetLevel(__ECHO_eDebugLevel.COMPLETE);
```
Filter by tag when you want to focus:
```js
// Only log messages tagged "Combat" or "AI"
EchoDebugSetTags(["Combat", "AI"]);

// Clear the tag filter so all tags are allowed again
EchoDebugClearTags();
```
Dump the entire log history to a text file if you need to inspect a bug after the fact:
```js
EchoDebugDumpLog();
```
If `ECHO_DEBUG_ENABLED` is set to 0, all Echo functions become no ops (apart from a minimal fallback in `EchoDebug`), so you can safely leave calls in your code for release builds.

## Documentation

Full online docs for Echo are available here:

### Echo docs:
https://refreshertowel.github.io/docs/echo/

### Where to buy

Echo is available on itch.io:

Itch page:
itch-url

Echo is also included for free with some RefresherTowel frameworks, such as Statement.

### Bug reports and feature requests

The best place to report bugs or request features is the GitHub Issues page:

Issues:
[https://github.com/RefresherTowel/Echo/issues](https://github.com/RefresherTowel/Echo/issues)

If you are not comfortable using GitHub, you can also post in the [**Echo channel on the RefresherTowel Games Discord**](https://discord.gg/w5NWDBwNta) and I can file an issue for you.

License

Echo is a paid framework. The license terms for using it in your projects are in:

[LICENSE_Echo.txt](LICENSE_Echo.txt)

In short: it is licensed per developer seat, you can use it in unlimited games (free or commercial), but you cannot redistribute the framework source itself.
