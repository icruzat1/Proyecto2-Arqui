# Proyecto-Arqui
# Proyecto 2 — Juego de reflejos

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

## Regenerar el hex (VS Code)

```bat
cd C:\Users\wille\Proyecto2\assembler
python assemble.py game.s game.hex
copy game.hex C:\Users\wille\Proyecto2\pochoco_soc-main\sw\game.hex
´´´

cd C:\Users\wille\Proyecto2
git pull
git add assembler pochoco_soc-main
git commit -m "mensaje"
git push



