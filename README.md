# El Problema del Juez del Puente
Paradojas Lógicas Aplicadas a la Programación en C

# 🧠 Paradojas Lógicas Aplicadas a la Programación en C

Este repositorio contiene un análisis práctico y teórico sobre cómo las paradojas clásicas de la literatura y la filosofía se reflejan directamente en la informática, la lógica formal y el desarrollo de software en **C**.

El objetivo de este proyecto es demostrar cómo la **autorreferencia** y las **contradicciones lógicas** provocan fallos de ejecución reales (como el *Stack Overflow*) y sirven para explicar teoremas fundamentales de la computación.

---

## 🤥 1. La Paradoja de Pinocho (El Bucle de Autorreferencia)

### El Concepto Filosófico
Ocurre cuando combinamos la regla del universo de Pinocho (su nariz crece si miente) con un enunciado que se evalúa a sí mismo. Pinocho afirma: **"Mi nariz va a crecer ahora mismo"**.
* Si es **verdad**, su nariz no debería crecer. Pero si no crece, la frase se vuelve falsa.
* Si es **mentira**, su nariz debería crecer. Pero si crece, la frase se vuelve verdadera.

### Reflejo en Código (C)
En programación, esto equivale a una función recursiva que altera su propia condición de salida basándose en el resultado de sí misma, generando una oscilación infinita que desborda la pila de memoria (*Stack Overflow*).

```c
#include <stdio.h>
#include <stdbool.h>

// 1 = Crece (Mentira), 0 = No crece (Verdad)
bool evaluar_nariz(bool prediccion_crecera) {
    if (prediccion_crecera == true) {
        // La condición se niega a sí misma infinitamente en la pila de llamadas
        return !evaluar_nariz(prediccion_crecera); 
    }
    return false;
}

int main() {
    printf("Evaluando frase de Pinocho...\n");
    // Provoca un desbordamiento de pila (Stack Overflow)
    evaluar_nariz(true); 
    return 0;
}
```

---

## 🛡️ 2. La Paradoja de Sancho Panza en el Puente (El Problema del Juez del Puente)

### El Concepto Filosófico
Extraída del capítulo 51 de la segunda parte de *Don Quijote de la Mancha*. En la ínsula Barataria, una ley establece que quien cruce un puente debe jurar a dónde va y qué va a hacer:
* Si dice la **verdad**, pasa libre.
* Si **miente**, es ahorcado.

Un viajero llega y jura: **"Vengo a morir en esa horca y a ninguna otra cosa"**. Los jueces entran en una contradicción insalvable: si lo ahorcan violan la ley (porque dijo la verdad y debía pasar libre), y si lo dejan pasar también la violan (porque mintió y debían ahorcarlo).

### Reflejo en Código (C)
Esta paradoja es la representación exacta del **Problema del Paro (Halting Problem)** de Alan Turing (1936). Demuestra que es matemáticamente imposible programar un algoritmo estático perfecto (`juez_del_puente`) capaz de predecir si cualquier otro programa arbitrario terminará o se colgará en un bucle infinito.

```c
#include <stdio.h>
#include <stdbool.h>

// Supongamos que existiera esta función analizadora perfecta de código
bool juez_del_puente(void (*programa)()) {
    // Devuelve true si el programa termina, false si se cuelga
}

// El programa viajero diseñado maliciosamente para contradecir al juez:
void viajero_paradojico() {
    if (juez_del_puente(viajero_paradojico) == true) {
        // Si el juez predice que va a terminar con éxito...
        while(true) {
            // ...el programa entra en un bucle infinito para hacerlo fallar.
        }
    }
    // Si el juez predice que se va a colgar, el programa finaliza inmediatamente.
}
```

---

## 🚀 Conclusiones Computacionales

* **La Autorreferencia es Peligrosa:** Cuando un sistema intenta analizarse estrictamente a sí mismo usando sus propias reglas operativas, se exponen vulnerabilidades lógicas.
* **Soluciones Prácticas en C:** Para evitar que estos escenarios congelen o destruyan sistemas en producción, los ingenieros de software implementan:
  1. **Límites de tiempo (Timeouts)**.
  2. **Contadores de profundidad máxima** en funciones recursivas.
  3. **Análisis estático de código** para detectar ciclos antes de la ejecución.

---

## 📂 Cómo clonar y experimentar
```bash
git clone https://github.com/4trastos/the-bridge-judge-problem.git
cd the-bridge-judge-problem
gcc sancho.c -o sancho
./sancho
```

---
*Desarrollado con fines educativos para conectar los mundos de la literatura clásica y las ciencias de la computación.*
