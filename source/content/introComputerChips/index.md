# Primer on <i class="fa-solid fa-microchip"></i> Computer

{% if slide %}
<!-- BUILDING THE SLIDES -->
```{toctree}
:maxdepth: 3

./beginnings
./z3
./mark1
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
```{include} ./mark1.md
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


{.smaller}
**Sources:**  
https://en.wikipedia.org/wiki/Computer  
https://en.wikipedia.org/wiki/Universal_Turing_machine  
https://en.wikipedia.org/wiki/Z3_(computer)#Z3_as_a_universal_Turing_machine  
https://en.wikipedia.org/wiki/Manchester_Mark_1  
https://en.wikipedia.org/wiki/Integrated_circuit  
https://en.wikipedia.org/wiki/Mohamed_Atalla  
https://en.wikipedia.org/wiki/F-14_CADC
https://en.wikipedia.org/wiki/Intel_4004
https://en.wikipedia.org/wiki/Central_processing_unit
https://en.wikipedia.org/wiki/Limits_of_computation  
https://en.wikipedia.org/wiki/Moore%27s_law  
https://en.wikipedia.org/wiki/Dennard_scaling  
https://en.wikipedia.org/wiki/Tejas_and_jayhawk  

{% endif %}

