
# Introducción
La  planificación de la actividad presenta el desarrollo de un modelo de optimización que permite enfrentar una problemática de forma sistemática. Dicha problemática se hace presente durante la semana de solemnes en la institución educativa debido a que implica múltiples restricciones logísticas y académicas. Una mala asignación de secciones de cursos a salas y horarios puede generar conflictos entre evaluaciones de cursos con estudiantes en común, sobrecargas en un mismo día y un uso ineficiente del espacio físico disponible. Estos problemas afectan tanto el rendimiento estudiantil como la gestión académica de la institución.

El objetivo principal es asignar secciones de cursos a salas y módulos horarios disponibles durante la semana de evaluaciones, de forma que se maximice el espacio mínimo restante en las salas utilizadas. Esto busca promover una asignación equitativa y eficiente del uso del espacio, evitando simultáneamente la asignación de evaluaciones con estudiantes en común al mismo horario.

Además, se discuten las variables de decisión, los parámetros y las restricciones involucradas en el modulo, junto con una interpretación detallada de su funcionamiento. Con esto se logra determinar la primera sección de la actividad y sienta las bases para una segunda formulación  que abordará la minimización de conflictos entre cursos con estudiantes compartidos, sin prohibirlos completamente.

### Formulación Matemática

**Conjuntos**:
$C$ : Conjunto de cursos.
$S_c$ : Conjunto de secciones del curso c $∈ C$.
$A$ : conjunto de salas disponibles.
$D$ : conjunto de días de la semana {$L$, $M$, $W$, $J$, $V$, $S$}.
$H$ : conjunto de bloques horarios {1,2, ... , 7}.
$M$ : conjunto de módulos horarios, definido como m = (d,h) donde $d ∈ D, h ∈ H$.
$T$ : conjunto de semestres {1,2, ... , 8}.
$C_t ⊆ C$ : conjunto de cursos correspondientes al semestre $t∈ T$.
$R ⊆ C x C$ : conjunto de pares de cursos con estudiantes en común.


- **C** – _Conjunto de cursos_:  
    Representa todos los cursos que deben rendir evaluaciones.  
    → Permite modelar la asignación de evaluaciones para cada curso.
    
- **ScS_cSc​** – _Secciones del curso ccc_:  
    Cada curso puede tener una o más secciones.  
    → Permite asignar evaluaciones por sección, reflejando la estructura real.
    
- **AAA** – _Salas disponibles_:  
    Lista de todas las salas donde se pueden rendir las evaluaciones.  
    → Permite controlar la capacidad y disponibilidad de espacios físicos.
    
- **DDD** – _Días de la semana_:  
    {L,M,W,J,V,S}\{L, M, W, J, V, S\}{L,M,W,J,V,S} representa los días hábiles de evaluación.  
    → Define el marco temporal donde se pueden distribuir los exámenes.
    
- **HHH** – _Bloques horarios_:  
    {1,2,...,7}\{1, 2, ..., 7\}{1,2,...,7}, representan los horarios diarios disponibles.  
    → Aporta la granularidad temporal al modelo.
    
- **MMM** – _Módulos_:  
    Cada módulo es un par ordenado (d,h)(d,h)(d,h) que combina día y bloque horario.  
    → Permite asignar secciones a tiempos específicos durante la semana.
    
- **TTT** – _Semestres académicos_:  
    {1,2,...,8}\{1,2,...,8\}{1,2,...,8}, representa los semestres que estructuran el plan de estudios.  
    → Útil para evitar que cursos del mismo semestre se asignen juntos.
    
- **Ct⊆CC_t \subseteq CCt​⊆C** – _Cursos del semestre ttt_:  
    Subconjunto de cursos que pertenecen a un mismo nivel.  
    → Ayuda a definir restricciones por cohorte o semestre.
    
- **R⊆C×CR \subseteq C \times CR⊆C×C** – _Pares de cursos con estudiantes en común_:  
    Lista de cursos que comparten estudiantes.  
    → Permite evitar (o minimizar) conflictos de horario entre estos cursos.

### **¿Qué logra el uso de estos conjuntos?**

Estos conjuntos permiten **estructurar el dominio del problema**, organizando los datos académicos (cursos, secciones, salas, horarios, etc.) de manera que el modelo pueda:

- Asignar evaluaciones a horarios específicos y salas adecuadas.
    
- Cumplir restricciones académicas como no solapar cursos con estudiantes en común.
    
- Distribuir las evaluaciones de forma eficiente, respetando la capacidad de las salas.
    
- Generar soluciones realistas, escalables y útiles para la planificación real de evaluaciones.
    

En resumen, los conjuntos **definen el universo sobre el que se toman decisiones**, y son fundamentales para crear restricciones bien formadas y alcanzar soluciones óptimas y viables.

---

**Parámetros**:
$U_a$ : capacidad de la sala $a ∈ A$
$e_c$$_s$ : número de estudiantes inscritos en la sección $s ∈ S_c$ del curso $c$.
$M$ : constante suficientemente grande (mayor que cualquier capacidad de sala).

- **ua​** – _Capacidad de la sala a∈Aa \in Aa∈A_  
    → Indica cuántos estudiantes caben en cada sala.  
    ✅ Permite verificar si una sección cabe en una sala determinada.  
    ✅ Se usa en restricciones de capacidad.
    
- **$e_c$$_s$​** – _Número de estudiantes inscritos en la sección s∈Scs \in S_cs∈Sc​ del curso ccc_  
    → Representa la demanda de espacio para esa sección.  
    ✅ Se usa para asegurar que las salas asignadas tengan capacidad suficiente.
    
- **M** – _Constante grande (por ejemplo, mayor que cualquier uau_aua​)_  
    → Se utiliza para activar o desactivar restricciones lógicas mediante multiplicación.  
    ✅ Aparece en restricciones condicionales, como aquellas que definen el espacio mínimo restante solo si una sala es utilizada.

### **¿Qué logra el uso de estos parámetros?**

Los parámetros permiten al modelo **incorporar información del mundo real** (como capacidades y matrículas) en la optimización. Gracias a ellos, el modelo:

- **Evalúa la factibilidad** de asignar una sección a una sala.
    
- **Calcula el uso del espacio**, lo que es clave para maximizar el mínimo espacio restante.
    
- **Activa o desactiva restricciones** en función de decisiones binarias (por ejemplo, si una sala está usada o no).
    
- **Evita soluciones inviables**, como asignar una sección a una sala que no tiene suficiente capacidad.

---
## 2.3 Variables

- `x_mac_s`: Variable binaria. Vale 1 si la sección `s` del curso `c` es asignada a la sala `a` en el módulo `m`; vale 0 en caso contrario.
    
- `EM`: Variable continua. Representa el espacio mínimo restante en las salas utilizadas. Es la variable objetivo del modelo.
    
- `SU_a`: Variable binaria. Vale 1 si la sala `a` está siendo utilizada; 0 en caso contrario.
    
- `y_cc'_m`: Variable binaria. Vale 1 si los cursos `c` y `c'` están asignados al mismo módulo `m`; 0 en caso contrario. Se usa para controlar conflictos.
    

---

## 2.4 Función Objetivo

**Maximizar:**  
`EM`  
(Maximizar el espacio mínimo restante en las salas utilizadas)

---

## 2.5 Restricciones

1. **Cada sección se asigna exactamente una vez**  
    Para todo curso `c` y sección `s` de `c`:
    
    ```
    suma sobre m en M y a en A de x_mac_s = 1
    ```
    
2. **Una sala no puede tener más de una sección por módulo**  
    Para toda sala `a` y módulo `m`:
    
    ```
    suma sobre c en C y s en S_c de x_mac_s <= 1
    ```
    
3. **Todas las secciones de un curso deben rendir al mismo tiempo**  
    Para todo curso `c`, y todas sus secciones `s` y `s'`, y para todo módulo `m`:
    
    ```
    suma sobre a en A de x_mac_s = suma sobre a en A de x_mac_s'
    ```
    
4. **Capacidad de la sala suficiente**  
    Para todo `m`, `a`, `c`, `s`:
    
    ```
    x_mac_s * e_cs <= u_a
    ```
    
5. **Definición del espacio mínimo restante**  
    Para toda sala `a` y módulo `m`:
    
    ```
    suma sobre c en C y s en S_c de (x_mac_s * (u_a - e_cs)) >= EM - (1 - SU_a) * M
    ```
    
6. **Marcado de sala como utilizada**  
    Para toda sala `a` y módulo `m`:
    
    ```
    suma sobre c en C y s en S_c de x_mac_s <= SU_a * M
    ```
    
7. **Evitar solapamiento entre cursos con estudiantes en común**  
    Para cada par de cursos `(c, c')` en R, y para todo módulo `m`:
    
    ```
    suma sobre a en A y s en S_c de x_mac_s + suma sobre a' en A y s' en S_c' de x_mac_s' <= 1
    ```
    

---

## Discusión del modelo

Este modelo tiene como objetivo asignar secciones de cursos a salas y horarios de forma que se maximice el espacio mínimo restante en las salas utilizadas. Esto ayuda a evitar sobrecargas de espacio y mejora el uso de infraestructura.

### Variables clave:

- `x_mac_s`: Representa la asignación específica de cada sección a una sala y módulo.
    
- `SU_a`: Permite identificar qué salas están siendo utilizadas.
    
- `EM`: Variable que refleja el mínimo espacio disponible entre todas las salas usadas. Es el valor que se busca maximizar.
    
- `y_cc'_m`: Controla si cursos con estudiantes en común están en el mismo módulo (usado en el segundo modelo).
    

### Qué logra el modelo:

- Asegura que cada sección tenga un lugar y horario único.
    
- Controla el uso de salas sin sobrepasar su capacidad.
    
- Evita que cursos con estudiantes en común se solapen.
    
- Promueve una distribución más equitativa y eficiente del espacio físico.
    

