# Home Row Mods Fix for Fast Typing

## Problem
When typing quickly, home row modifiers were triggering incorrectly. For example, typing "fast" would activate the Control modifier on the 'f' key because the 'f' key was still held when 'a' was pressed.

## Solution
Configured custom home row mod behaviors with the following optimizations:

### Key Settings
- **require-prior-idle-ms = 150**: Requires 150ms of no key activity before a home row mod can activate
- **hold-trigger-key-positions**: Left hand mods only trigger when right hand keys are pressed, and vice versa
- **hold-trigger-on-release**: Only decide between hold/tap when the key is released
- **tapping-term-ms = 280**: Balanced timing for hold detection
- **quick-tap-ms = 175**: Time window for quick repeated taps

### Hand Separation
- Left hand home row mods (A, S, D, F) only activate when pressing right hand keys
- Right hand home row mods (J, K, L, ;) only activate when pressing left hand keys
- This prevents same-hand key combinations from triggering mods

## Test Case
The word "fast" should now type normally without triggering any modifiers, even when typed quickly with overlapping key presses.

## Technical Details
- Uses custom `hml` (homerow_mods_left) and `hmr` (homerow_mods_right) behaviors
- Replaces default `&mt` behaviors in the keymap
- Based on ZMK best practices for fast typing scenarios