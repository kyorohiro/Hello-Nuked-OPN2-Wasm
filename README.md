# Nuked-OPN2
High accuracy Yamaha YM3438(OPN2) emulator.

The YM3438 is a CMOS variant of the YM2612 used in Sega MegaDrive(Genesis) and FM Towns.

Genesis Plus GX fork with this core integrated is available here: https://github.com/nukeykt/Genesis-Plus-GX

# Why this repository exists

This repository was prepared so
[Tetorica FM2612 / hello_ymfm_wasm](https://github.com/kyorohiro/hello_ymfm_wasm)
can try a second YM2612-compatible backend in the browser.

Tetorica FM2612:
- repository: https://github.com/kyorohiro/hello_ymfm_wasm
- site: https://kyorohiro.github.io/hello_ymfm_wasm/

The main goal here is to make it easier to switch or compare:
- `ymfm`
- `nuked-opn2`

under similar WebAssembly and browser conditions.

In particular, this repository is useful when checking whether a sound difference
comes from:
- the FM core itself
- the WebAssembly wrapper
- or the browser-side playback path

# What is included here

- `generated/nuked_opn2_wasm.js`
- `generated/nuked_opn2_wasm.wasm`
- `web/ym2612.js`
- `docs/index.html`
- `docs/demos/nuked_opn2_embeded.html`

The `web/ym2612.js` wrapper intentionally mirrors the shape used in
`hello_ymfm_wasm`, so browser-side tests can stay close to each other.

# Try it in the browser

If you serve the `docs/` directory locally, open:

- `docs/index.html`
- `docs/demos/nuked_opn2_embeded.html`

For example:

```sh
cd docs
python3 -m http.server 8086
```

Then open:

- `http://localhost:8086/`
- `http://localhost:8086/demos/nuked_opn2_embeded.html`

The embedded demo plays one small YM2612-style beep through the
Nuked-OPN2 WebAssembly runtime.

# Features:
- Based on YM3438 die shot reverse engineering and thus provides very high emulation accuracy.

- Cycle-accurate.

- Undocumented registers/features emulation.
- SSG-EG, CSM mode emulation.
- Compatible with the YM2612.

# API documention
```
void OPN2_Reset(ym3438_t *chip) - Reset emulated chip
void OPN2_Clock(ym3438_t *chip, Bit32s *buffer) - Advances emulated chip state by 1 internal clock(6 master clocks). Writes signed 9-bit MOL, MOR pin states to buffer. 
void OPN2_Write(ym3438_t *chip, Bit32u port, Bit8u data) - Write 8-bit data to port.
void OPN2_SetTestPin(ym3438_t *chip, Bit32u value) - Set TEST pin value.
Bit32u OPN2_ReadTestPin(ym3438_t *chip) - Read TEST pin value.
Bit32u OPN2_ReadIRQPin(ym3438_t *chip) - Read IRQ pin value.
Bit8u OPN2_Read(ym3438_t *chip, Bit32u port) - Read chip status.
```

# Samples
Sonic the Hedgehog:
https://youtu.be/ImmKy_-pJ8g

Sega CD BIOS v1.10:
https://youtu.be/s-8ASMbtojQ
