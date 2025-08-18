# Test Case: Fast Typing with Home Row Mods

## Overview
This test validates that the home row mods fix prevents accidental modifier activation during fast typing.

## Test Scenario: Typing "fast"

### Before the Fix
When typing "fast" quickly:
1. Press and hold 'f' key (position 30, mapped to `&mt LEFT_CONTROL F`)
2. Press 'a' key (position 27) before fully releasing 'f'
3. **PROBLEM**: Control modifier activates because 'f' is still held
4. Result: Ctrl+A (select all) instead of "fa"

### After the Fix  
When typing "fast" quickly:
1. Press and hold 'f' key (position 30, mapped to `&hml LEFT_CONTROL F`)
2. Press 'a' key (position 27) before fully releasing 'f'
3. **SOLUTION**: No modifier activation because:
   - `require-prior-idle-ms = 150`: Not enough idle time before 'f' press
   - `hold-trigger-key-positions`: 'a' (pos 27) is not in trigger positions for left hand mods
4. Result: "fa" types normally

## Key Position Reference
```
Row 2 (Home Row): 26[CAPS] 27[A] 28[S] 29[D] 30[F] 31[G]    32 33[H] 34[J] 35[K] 36[L] 37[;] 38[']
```

## Home Row Mod Mappings
- Position 27 (A): `&hml LSHIFT A`
- Position 28 (S): `&hml LEFT_WIN S` 
- Position 29 (D): `&hml LEFT_ALT D`
- Position 30 (F): `&hml LEFT_CONTROL F`
- Position 34 (J): `&hmr RIGHT_CONTROL J`
- Position 35 (K): `&hmr RALT K`
- Position 36 (L): `&hmr RIGHT_WIN L`
- Position 37 (;): `&hmr RIGHT_SHIFT SEMI`

## Expected Behavior
✅ Typing "fast" quickly should NOT trigger any modifiers
✅ Intentionally holding F while pressing right-hand keys should trigger Control modifier
✅ Intentionally holding J while pressing left-hand keys should trigger Control modifier
✅ All other home row mod combinations should work as intended when used deliberately