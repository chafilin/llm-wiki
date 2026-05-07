# User Activation

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Defenses/User_activation

## Overview

User activation is a security mechanism that restricts access to sensitive APIs to prevent malicious scripts from abusing features that could degrade user experience. Some APIs can only be used when the user is in an "active interaction" state—either currently interacting with the page or having interacted with it since page load.

## Activation Triggering Input Events

An **activation triggering input event** is defined as an event that:

- Has the `isTrusted` attribute set to `true`
- Is one of the following types:
  - `keydown` (except Esc, browser shortcuts, and keys like Caps Lock, Num Lock, Print Screen)
  - `mousedown`
  - `pointerdown` (if `pointerType` is "mouse")
  - `pointerup` (if `pointerType` is not "mouse")
  - `touchend`

## Two Types of Activation Windows

### Transient Activation

**Transient activation** indicates a user has recently pressed a button or performed user interaction. It:
- Expires after a timeout if not renewed
- May be consumed (deactivated) by some APIs

**APIs requiring transient activation include:**
- `Clipboard.read()`, `Clipboard.readText()`, `Clipboard.write()`, `Clipboard.writeText()`
- `Element.requestFullScreen()`, `Element.requestPointerLock()`
- `Window.open()`, `Window.showDirectoryPicker()`, `Window.showOpenFilePicker()`, `Window.showSaveFilePicker()`
- `MediaDevices.getDisplayMedia()`
- `PaymentRequest.show()`
- `XRSystem.requestSession()`
- And many more

### Sticky Activation

**Sticky activation** indicates a user has interacted with the page at some point in the session. It:
- Is not reset after being set initially (unlike transient activation)
- Persists until the end of the session

**APIs requiring sticky activation include:**
- `beforeunload` event
- `Navigator.vibrate()`
- Media and Web Audio API autoplay

## UserActivation API

The `UserActivation` API allows programmatic checking of user activation status via `navigator.userActivation`:

- **`UserActivation.hasBeenActive`** — indicates sticky user activation
- **`UserActivation.isActive`** — indicates transient user activation

Example:
```javascript
if (navigator.userActivation.isActive) {
  // Transient activation is available
  window.open('https://example.com');
}

if (navigator.userActivation.hasBeenActive) {
  // Sticky activation is available
  navigator.vibrate(100);
}
```

## Key Difference

**Transient vs Sticky:**
- **Transient**: Short-lived, can be consumed; ensures APIs are directly triggered by user
- **Sticky**: Long-lived, never resets; prevents features from auto-triggering on page load
