# Primer on <i class="fa-solid fa-microchip"></i> Computer

{% if slide %}
<!-- BUILDING THE SLIDES -->
```{toctree}
:maxdepth: 3

./beginnings
./z3
./first
./transistors
./integratedCircuit
./microprocessor.md
./laws
./meltDown
./powerWall
```

{% else %}
<!-- BUILDING THE PAGES -->

```{include} ./beginnings.md
```
```{include} ./z3.md
```
```{include} ./first.md
```
```{include} ./transistors.md
```
```{include} ./integratedCircuit.md
```
```{include} ./microprocessor.md
```
```{include} ./laws.md
```
```{include} ./meltDown.md
```
```{include} ./powerWall.md
```
<!--
```{include} ./someFolde/fileA.md
```
```{include} ./someFolde/fileB.md
```
-->
{% endif %}

