
# Proyecto 2 

Grupo: Ignacio Cruzat, Juan Vicente Celedón, Wille Saarenpaa

Juego en assembly para el Espino Core (RV32E), en la Nandland Go Board.
El `.hex` lo genera nuestro assembler. No usar `riscv64-unknown-elf-as`.

## Jugar (la placa ya está grabada)

Enchufar el micro-USB. No hace falta terminal ni PC con herramientas.

- Se prenden los 4 LED unos segundos.
- Queda uno. Apretar el botón de ese LED (SW1 = D1, SW2 = D2, SW3 = D3, SW4 = D4).
- Bien: décimas en el display (`06` = 0,6 s). Soltar el botón.
- Mal: `EE`. Esa ronda no cuenta.
- A los 10 aciertos el display se queda en el promedio y no hay LED.
- Desenchufar y enchufar = partida nueva.

## ¿Cómo jugar?

Ventana negra (aplicación start del archivo de oss-cad-build), placa ya enchufada. Uno por uno.

La ventana es: Escritorio > Universidad > Arquitectura de computadores > herramientas GitHub oss cad > oss-cad-suite > start

Paso 1.
```bat
set "PATH=C:\Users\wille\OneDrive\Escritorio\Universidad\ARQUITECTURA DE COMPUTADORES\herramientas github oss cad\oss-cad-suite\bin;C:\Users\wille\OneDrive\Escritorio\Universidad\ARQUITECTURA DE COMPUTADORES\herramientas github oss cad\oss-cad-suite\lib;%PATH%"
```
Paso 2.
```bat
cd C:\Users\wille\Proyecto2\pochoco_soc-main
```
Paso 3.
```bat
copy /Y C:\Users\wille\Proyecto2\assembler\game.hex sw\game.hex
```
Tiene que decir 1 archivo(s) copiado(s).

Paso 4.

```bat
yosys -p "read_verilog rtl/game_top.v rtl/pochoco_periph.v rtl/pochoco_ram.v rtl/pochoco_soc.v rtl/pochoco_spi_slave.v rtl/espino_core/espino_alu.v rtl/espino_core/espino_controller.v rtl/espino_core/espino_core.v rtl/espino_core/espino_decoder.v rtl/espino_core/espino_id_stage.v rtl/espino_core/espino_if_stage.v rtl/espino_core/espino_load_store_unit.v rtl/espino_core/espino_register_file.v; synth_ice40 -top game_top -json game_top.json; stat"
nextpnr-ice40 --hx1k --package vq100 --json game_top.json --pcf goboard.pcf --asc game_top.asc
icepack game_top.asc game_top.bin
iceprog game_top.bin
```
Al Bye. se prenden los 4 LED chicos. No desenchufar: la flash no lo guarda.
Si no se prenden, repetir solo el paso 4.








## Regenerar el hex (VS Code)

```bat
cd C:\Users\wille\Proyecto2\assembler
python assemble.py game.s game.hex
copy game.hex C:\Users\wille\Proyecto2\pochoco_soc-main\sw\game.hex
```
Esto regenera game.hex desde game.s si es que en algún momento se cambia el código del juego.

### Subir cambios a github desde VScode
```bat
cd C:\Users\wille\Proyecto2
git pull
git add assembler pochoco_soc-main
git commit -m "mensaje"
git push
```

## Grabar de nuevo

Se ocupa si se cambió una constante del juego, se regeneró `game.hex`, o se tocó un `.v`.
Si la placa ya está grabada y solo se quiere jugar, no hace falta: enchufar el USB.

La ventana negra es la de OSS CAD (`start`), no la de VS Code.
En esta PC `make` no existe. Placa enchufada antes del `iceprog`.

```bat
set "PATH=C:\Users\wille\OneDrive\Escritorio\Universidad\ARQUITECTURA DE COMPUTADORES\herramientas github oss cad\oss-cad-suite\bin;C:\Users\wille\OneDrive\Escritorio\Universidad\ARQUITECTURA DE COMPUTADORES\herramientas github oss cad\oss-cad-suite\lib;%PATH%"
cd C:\Users\wille\Proyecto2\pochoco_soc-main
yosys -p "read_verilog rtl/game_top.v rtl/pochoco_periph.v rtl/pochoco_ram.v rtl/pochoco_soc.v rtl/pochoco_spi_slave.v rtl/espino_core/espino_alu.v rtl/espino_core/espino_controller.v rtl/espino_core/espino_core.v rtl/espino_core/espino_decoder.v rtl/espino_core/espino_id_stage.v rtl/espino_core/espino_if_stage.v rtl/espino_core/espino_load_store_unit.v rtl/espino_core/espino_register_file.v; synth_ice40 -top game_top -json game_top.json; stat"
nextpnr-ice40 --hx1k --package vq100 --json game_top.json --pcf goboard.pcf --asc game_top.asc
icepack game_top.asc game_top.bin
iceprog game_top.bin
```


