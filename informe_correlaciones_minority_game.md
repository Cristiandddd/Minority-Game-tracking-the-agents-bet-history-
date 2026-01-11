# Correlaciones y Comportamiento Colectivo de Agentes en el Minority Game: Transiciones de Fase y Estructura de Información

---

## Resumen

Este capítulo investiga cómo el parámetro de control α = P/N determina la estructura de correlaciones y el comportamiento colectivo de agentes en el Minority Game. El estudio se centra en tres preguntas fundamentales: (1) ¿cómo varía la predictibilidad de las decisiones individuales a través de los regímenes del sistema?, (2) ¿qué estructura de correlaciones emerge entre agentes y cómo se transforma al cruzar el punto crítico?, y (3) ¿existe flujo de información direccional entre agentes que revele dinámicas de liderazgo-seguimiento? Los resultados muestran que el punto crítico α_c ≈ 0.34 marca una transición cualitativa en la organización del sistema, con implicaciones para la comprensión de mercados financieros y sistemas de decisión colectiva.

---

## 1. Introducción

### 1.1 El Problema Científico

El Minority Game constituye uno de los modelos paradigmáticos para estudiar sistemas de agentes competitivos con información limitada. En este juego, N agentes deben elegir repetidamente entre dos opciones, y aquellos en el lado minoritario obtienen recompensa. Esta simple regla genera dinámicas complejas que dependen críticamente del parámetro α = P/N, donde P = 2^M representa el número de estados de memoria posibles.

La física estadística del Minority Game ha establecido que existe una transición de fase en α_c ≈ 0.34, separando dos regímenes cualitativamente distintos:

**Régimen crowded (α < α_c):** Los agentes compiten por un número limitado de estrategias efectivas. Esta escasez de recursos informacionales induce correlaciones fuertes entre agentes que comparten o usan estrategias similares. El sistema es ineficiente: las fluctuaciones de la asistencia global σ²/N crecen, indicando que los agentes frecuentemente toman decisiones correlacionadas que amplifican los movimientos colectivos.

**Régimen diluted (α > α_c):** Existe abundancia de estrategias disponibles. Los agentes pueden diferenciarse, reduciendo la competencia directa. El sistema se vuelve eficiente: σ²/N alcanza un mínimo cercano al límite aleatorio, indicando que las decisiones de los agentes se cancelan estadísticamente como lo harían variables independientes.

Sin embargo, la mayoría de estudios previos se han enfocado en cantidades agregadas (volatilidad, eficiencia global). Menos explorada está la pregunta de cómo las **correlaciones entre pares de agentes** y la **estructura de información** del sistema se transforman a través de estos regímenes. Esta es precisamente la pregunta central de este capítulo.

### 1.2 Objetivos

Este estudio busca caracterizar, desde la perspectiva de teoría de la información:

1. **La predictibilidad individual:** ¿Qué tan aleatorias son las decisiones de cada agente? ¿Varía esto con α?

2. **La estructura de correlaciones:** ¿Existen grupos de agentes fuertemente correlacionados? ¿Cómo cambia esta estructura al cruzar α_c?

3. **El flujo de información:** ¿Hay agentes que "lideran" las decisiones de otros? ¿La causalidad informacional es simétrica o dirigida?

### 1.3 Estructura del Capítulo

El capítulo se organiza siguiendo la línea lógica del análisis: primero caracterizamos el comportamiento individual de los agentes mediante entropía (Sección 2), luego examinamos las correlaciones entre pares (Sección 3), después analizamos la estructura colectiva mediante clustering y redes (Sección 4), y finalmente estudiamos los flujos de información direccional (Sección 5). La Sección 6 sintetiza los hallazgos en el contexto de la física del Minority Game.

---

## 2. Entropía y Predictibilidad Individual

La primera pregunta es fundamental: ¿qué tan predecibles son las decisiones de un agente? Si un agente siempre elige la misma opción, su comportamiento tiene entropía cero y es completamente predecible. Si elige aleatoriamente con probabilidad 50-50, su entropía es máxima (1 bit) y es completamente impredecible.

### 2.1 Entropía de Shannon: Aleatoriedad Aparente

La entropía de Shannon H = -Σ p(x) log₂ p(x) mide la incertidumbre en las decisiones de un agente. Para decisiones binarias, H alcanza su máximo de 1 bit cuando ambas opciones son igualmente probables.

**Pregunta:** ¿Los agentes en el régimen crowded son más o menos predecibles que en el régimen diluted?

**Hallazgo principal:** [Pendiente de resultados experimentales]

La interpretación física es la siguiente: en el régimen crowded, los agentes están "atrapados" usando un conjunto limitado de estrategias, lo que podría hacer sus decisiones más predecibles. En el régimen diluted, la abundancia de estrategias permite mayor diversidad de comportamientos.

### 2.2 Entropía de Bloque: Dependencias Temporales

La entropía de Shannon solo considera la frecuencia marginal de decisiones. Pero las decisiones de los agentes tienen memoria: dependen del historial reciente a través del mecanismo de estrategias. La entropía de bloque H_k examina secuencias de k decisiones consecutivas.

Si las decisiones fueran independientes, esperaríamos H_k = k × H_1. Desviaciones de esta linealidad revelan correlaciones temporales.

**Pregunta:** ¿Qué régimen exhibe mayor estructura temporal en las decisiones?

**Hallazgo principal:** [Pendiente de resultados experimentales]

### 2.3 Densidad de Entropía: La Impredecibilidad Irreducible

La densidad de entropía h = lim(H_k/k) cuando k→∞ representa la impredecibilidad "verdadera" del proceso, una vez descontadas las correlaciones temporales. Es la cantidad de información nueva generada por cada decisión.

Esta medida es crucial porque permite comparar sistemas con diferentes estructuras de memoria. Un proceso con h bajo genera pocas sorpresas; uno con h alto es genuinamente impredecible.

**Pregunta:** ¿Cómo se relaciona h con el régimen de α?

**Hallazgo principal:** [Pendiente de resultados experimentales]

---

## 3. Correlaciones Entre Agentes

Más allá del comportamiento individual, la pregunta central es: ¿cómo se relacionan las decisiones de diferentes agentes?

### 3.1 Correlación de Pearson: Sincronización Lineal

La correlación de Pearson ρ_ij mide el grado en que dos agentes i, j tienden a tomar la misma decisión (ρ > 0) o decisiones opuestas (ρ < 0) simultáneamente.

**Predicción teórica:** En el régimen crowded, donde múltiples agentes usan estrategias idénticas o similares, esperamos correlaciones positivas significativas. En el régimen diluted, las correlaciones deberían aproximarse a cero.

**Hallazgo principal:** [Pendiente de resultados experimentales]

### 3.2 Información Mutua: Dependencias No Lineales

La correlación de Pearson solo captura dependencias lineales. La información mutua I(X;Y) detecta cualquier tipo de dependencia estadística, incluyendo relaciones no lineales.

**Pregunta:** ¿Existen dependencias no lineales entre agentes que la correlación de Pearson no detecta?

**Hallazgo principal:** [Pendiente de resultados experimentales]

### 3.3 Distribución de Correlaciones por Régimen

Para caracterizar la estructura global de correlaciones, examinamos la distribución completa de todos los coeficientes de correlación ρ_ij.

En un sistema sin estructura, esperamos una distribución centrada en cero. Desviaciones sistemáticas indican organización colectiva.

**Hallazgo principal:** [Pendiente de resultados experimentales]

---

## 4. Estructura Colectiva: Redes de Co-Victoria

Si existen correlaciones significativas entre agentes, la siguiente pregunta es: ¿forman estos agentes grupos o comunidades identificables? Pero más allá de la correlación de decisiones, existe una pregunta más fundamental en el contexto del Minority Game: **¿qué agentes tienden a ganar juntos?**

Esta sección introduce una métrica original: la **red de co-victoria**, que captura las relaciones de éxito compartido entre agentes y permite estudiar transiciones topológicas con α.

### 4.1 Definición de la Matriz de Co-Victoria

Para cada ronda t, definimos el conjunto de ganadores G(t) como los agentes que eligieron la acción minoritaria. Construimos la matriz de adyacencia de co-victorias:

$$W_{ij} = \frac{1}{T} \sum_{t=1}^{T} \mathbb{1}[i \in G(t) \land j \in G(t)]$$

donde T es el número total de rondas y $\mathbb{1}[\cdot]$ es la función indicadora.

**Interpretación:** $W_{ij}$ representa la fracción de rondas en las que los agentes i y j ganaron simultáneamente. Si los agentes decidieran independientemente y la probabilidad de ganar fuera p ≈ 0.5, esperaríamos $W_{ij} \approx 0.25$.

**Pregunta clave:** ¿Cómo se desvía la distribución de $W_{ij}$ del valor esperado para agentes independientes, y cómo depende esta desviación del régimen de α?

### 4.2 Distribución de Pesos de Co-Victoria

La distribución de los elementos $W_{ij}$ revela la estructura de coordinación del sistema:

- **Media > 0.25:** Indica que existen parejas de agentes que ganan juntos más frecuentemente de lo esperado por azar.
- **Varianza alta:** Sugiere heterogeneidad en las relaciones de co-victoria, con algunos pares fuertemente sincronizados y otros no.
- **Asimetría (skewness):** Una distribución asimétrica positiva indica la presencia de "coaliciones ganadoras" con pesos excepcionalmente altos.

**Predicción teórica:**
- En el régimen **crowded** (α < 0.3), donde los agentes compiten por estrategias limitadas, esperamos que grupos de agentes con estrategias similares ganen y pierdan juntos, produciendo una distribución con media elevada y alta varianza.
- En el régimen **diluted** (α > 0.4), la diversidad de estrategias debería producir una distribución más cercana al caso independiente (media ≈ 0.25, varianza baja).
- En el **punto crítico**, esperamos comportamiento intermedio con posibles fluctuaciones máximas.

**Hallazgo principal:** [Pendiente de resultados experimentales - Figura 05]

### 4.3 Análisis de Percolación: Emergencia de Estructura Global

Una vez construida la matriz W, definimos una red binaria aplicando un umbral θ:

$$A_{ij}(\theta) = \begin{cases} 1 & \text{si } W_{ij} > \theta \\ 0 & \text{si } W_{ij} \leq \theta \end{cases}$$

El análisis de percolación estudia cómo cambia la conectividad de la red al variar θ:

- Para θ bajo, la red está densamente conectada (todos los agentes forman una componente gigante).
- Para θ alto, la red se fragmenta en componentes aisladas.
- El **umbral crítico de percolación** $\theta_c$ marca la transición.

**Pregunta:** ¿Cómo depende $\theta_c$ del régimen de α? ¿Las redes del régimen crowded son más robustas a la fragmentación?

**Hallazgo principal:** [Pendiente de resultados experimentales - Figura 07]

### 4.4 Propiedades Topológicas de las Redes

Para un umbral θ fijo, analizamos las siguientes métricas topológicas:

**Densidad de la red:**
$$\rho = \frac{2|E|}{N(N-1)}$$

donde |E| es el número de aristas. Mide qué fracción de todos los pares posibles están conectados.

**Grado medio:**
$$\langle k \rangle = \frac{1}{N} \sum_i k_i$$

donde $k_i$ es el número de vecinos del agente i.

**Coeficiente de clustering:**
$$C = \frac{1}{N} \sum_i C_i, \quad C_i = \frac{2|\text{triángulos en } i|}{k_i(k_i-1)}$$

Mide la tendencia de los vecinos de un nodo a estar también conectados entre sí. Valores altos indican estructura de "camarillas".

**Longitud de camino promedio:**
$$L = \frac{1}{N(N-1)} \sum_{i \neq j} d(i,j)$$

donde d(i,j) es la distancia más corta entre i y j.

**Predicción teórica:**
- Régimen crowded: Alta densidad, alto clustering (grupos de agentes coordinados), caminos cortos.
- Régimen diluted: Baja densidad, bajo clustering, red más dispersa o fragmentada.

**Hallazgo principal:** [Pendiente de resultados experimentales - Figura 08]

### 4.5 Distribución de Grado: ¿Qué Tipo de Red Emerge?

La distribución de grado P(k) es una firma fundamental de la topología de la red:

- **Red aleatoria (Erdős-Rényi):** P(k) sigue una distribución de Poisson centrada en ⟨k⟩.
- **Red scale-free (Barabási-Albert):** P(k) ~ k^{-γ} con γ ≈ 2-3, indicando la presencia de "hubs" altamente conectados.
- **Red regular:** Todos los nodos tienen aproximadamente el mismo grado.

**Pregunta:** ¿Las redes de co-victoria exhiben hubs (agentes que co-ganan con muchos otros)? ¿La distribución cambia con α?

**Hallazgo principal:** [Pendiente de resultados experimentales - Figura 09]

### 4.6 Detección de Comunidades: Coaliciones Emergentes

Aplicamos el algoritmo de Louvain para detectar comunidades (grupos de nodos más conectados entre sí que con el resto). La **modularidad** Q cuantifica qué tan bien definida está la estructura de comunidades:

$$Q = \frac{1}{2m} \sum_{ij} \left[ A_{ij} - \frac{k_i k_j}{2m} \right] \delta(c_i, c_j)$$

donde m es el número de aristas, y $\delta(c_i, c_j) = 1$ si i y j están en la misma comunidad.

**Interpretación física:** Las comunidades en la red de co-victoria representan "coaliciones" de agentes que tienden a ganar juntos. En el Minority Game, estas coaliciones podrían corresponder a grupos de agentes usando estrategias complementarias o anticorrelacionadas con el resto del sistema.

**Preguntas:**
1. ¿El número de comunidades depende del régimen de α?
2. ¿La modularidad Q es mayor en algún régimen particular?
3. ¿Las comunidades son más fragmentadas (muchas pequeñas) o concentradas (pocas grandes)?

**Hallazgo principal:** [Pendiente de resultados experimentales - Figuras 10-11]

### 4.7 Identificación de Topología: Comparación con Modelos Canónicos

Para caracterizar qué tipo de red emerge en cada régimen, comparamos con tres modelos canónicos:

**Modelo de Erdős-Rényi (ER):**
Red aleatoria donde cada arista existe con probabilidad p independiente. Genera redes con clustering bajo y caminos cortos.

**Modelo de Barabási-Albert (BA):**
Red construida por conexión preferencial, donde nuevos nodos se conectan preferentemente a nodos ya muy conectados. Genera redes scale-free con hubs prominentes.

**Modelo de Watts-Strogatz (WS):**
Interpolación entre red regular y aleatoria. Genera redes "small-world" con alto clustering y caminos cortos.

**Metodología:** Para cada red empírica, generamos redes sintéticas con el mismo número de nodos y aristas (o grado medio), y comparamos las distribuciones de grado y los valores de C y L.

**Hallazgo principal:** [Pendiente de resultados experimentales - Figura 12]

### 4.8 Diagrama de Fase Topológico: C vs L

El diagrama de clustering C versus longitud de camino L permite clasificar redes en un espacio bidimensional:

| Región | C | L | Tipo de Red |
|--------|---|---|-------------|
| Arriba-izquierda | Alto | Bajo | Small-world |
| Abajo-izquierda | Bajo | Bajo | Aleatoria |
| Arriba-derecha | Alto | Alto | Regular/lattice |
| Abajo-derecha | Bajo | Alto | Fragmentada |

**Pregunta central:** ¿Dónde se ubican las redes de co-victoria en este diagrama, y cómo migran al variar α?

Si las redes transicionan de una región a otra al cruzar α_c, esto constituiría una **transición de fase topológica** en el espacio de redes.

**Hallazgo principal:** [Pendiente de resultados experimentales - Figura 13]

### 4.9 Evolución Topológica con α: El Diagrama de Fase

Consolidamos todos los hallazgos topológicos en un diagrama de fase que muestra cómo las propiedades de la red de co-victoria varían continuamente con α:

**Variables a graficar vs α (escala logarítmica):**
- Densidad ρ
- Clustering C
- Grado medio ⟨k⟩
- Modularidad Q
- Número de comunidades
- Tamaño de la componente gigante

**Expectativa:** Si la transición de fase del Minority Game en α_c tiene manifestación topológica, esperamos ver cambios cualitativos o singularidades en estas curvas cerca de α ≈ 0.34.

**Hallazgo principal:** [Pendiente de resultados experimentales - Síntesis de Figuras 05-13]

---

## 5. Flujo de Información y Causalidad

Las correlaciones son simétricas: si A está correlacionado con B, B está correlacionado con A. Pero la causalidad puede ser asimétrica: quizás A "lidera" y B "sigue". La transfer entropy permite detectar estas asimetrías.

### 5.1 Transfer Entropy: Causalidad Informacional

La transfer entropy T_Y→X mide cuánto reduce el conocimiento de Y la incertidumbre sobre el futuro de X, más allá de lo que la historia de X ya predice. Es una medida de causalidad predictiva direccional.

**Pregunta:** ¿Existen agentes "líderes" que influyen en las decisiones de otros?

**Hallazgo principal:** [Pendiente de resultados experimentales]

### 5.2 Asimetría del Flujo de Información

La diferencia ΔT_ij = T_i→j - T_j→i indica la dirección neta del flujo de información entre dos agentes.

**Pregunta:** ¿La estructura de causalidad es diferente en los distintos regímenes?

**Hallazgo principal:** [Pendiente de resultados experimentales]

---

## 6. Síntesis: El Minority Game a Través del Cristal de la Información

### 6.1 El Régimen Crowded (α < 0.3)

[Síntesis de hallazgos para este régimen - pendiente de resultados]

La interpretación física: cuando P/N < α_c, el número de estados de memoria es pequeño comparado con el número de agentes. Muchos agentes terminan usando estrategias idénticas o fuertemente correlacionadas. Esta "congestión estratégica" tiene las siguientes consecuencias informacionales:

- [Consecuencia 1 - pendiente]
- [Consecuencia 2 - pendiente]
- [Consecuencia 3 - pendiente]

### 6.2 El Punto Crítico (0.3 ≤ α ≤ 0.4)

[Síntesis de hallazgos para el punto crítico - pendiente de resultados]

En el punto crítico, el sistema exhibe fluctuaciones máximas y comportamiento de scaling. Desde la perspectiva informacional:

- [Observación 1 - pendiente]
- [Observación 2 - pendiente]

### 6.3 El Régimen Diluted (α > 0.4)

[Síntesis de hallazgos para este régimen - pendiente de resultados]

Cuando P/N > α_c, las estrategias son abundantes y los agentes pueden diferenciarse. Las consecuencias informacionales:

- [Consecuencia 1 - pendiente]
- [Consecuencia 2 - pendiente]
- [Consecuencia 3 - pendiente]

### 6.4 La Transición de Fase Vista desde la Teoría de la Información

[Discusión integradora - pendiente de resultados]

---

## 7. Conclusiones

Este estudio ha caracterizado la estructura de información y correlaciones en el Minority Game a través de los diferentes regímenes del parámetro α. Los principales hallazgos son:

1. [Hallazgo principal 1 - pendiente]
2. [Hallazgo principal 2 - pendiente]
3. [Hallazgo principal 3 - pendiente]

Estos resultados contribuyen a la comprensión de cómo la competencia por recursos informacionales (estrategias) genera estructura colectiva en sistemas de agentes, con posibles implicaciones para el estudio de mercados financieros y otros sistemas de decisión distribuida.

---

## Anexo A: Metodología Técnica

### A.1 Datos Utilizados

Los datos provienen de simulaciones del Minority Game estándar con los siguientes parámetros:
- Número de agentes: N variable según configuración
- Memoria: M variable según configuración  
- Estrategias por agente: S = 2
- Rondas de simulación: 10,000 decisiones por agente (fase estacionaria)
- Valores de α explorados: [lista según datos disponibles]

### A.2 Preprocesamiento

Las secuencias de decisiones {-1, +1} se convirtieron a formato binario {0, 1} para cálculos de entropía. Se verificó la integridad de los datos descartando secuencias monótonas (agentes "congelados").

### A.3 Cálculo de Entropías

**Entropía de Shannon:**
$$H_1 = -p \log_2(p) - (1-p) \log_2(1-p)$$

donde p es la fracción de decisiones positivas.

**Entropía de bloque:**
Se contabilizaron todas las subsecuencias de longitud k y se calculó la entropía de su distribución empírica.

**Densidad de entropía:**
Aproximación: h ≈ H_k - H_{k-1} para k suficientemente grande.

### A.4 Cálculo de Correlaciones

**Correlación de Pearson:** Implementación estándar de NumPy.

**Información mutua:** Discretización de secuencias y cálculo mediante la fórmula estándar.

**Transfer entropy:** Implementación mediante estimación de probabilidades condicionales con k=1 paso de historia.

### A.5 Clustering y Redes

**Clustering jerárquico:** Método de Ward sobre matriz de distancias (1 - |ρ|).

**Redes de correlación:** Umbral de |ρ| > 0.3 para definir aristas. Análisis mediante NetworkX.

---

## Anexo B: Especificaciones del Sistema

**Plataforma:** RunPod  
**GPU:** NVIDIA A40 (48GB VRAM)  
**CPU:** Intel Xeon Gold 6342 @ 2.80GHz  
**RAM:** 50GB  

**Software:**
- Python 3.10
- NumPy 1.24
- SciPy 1.10
- Pandas 2.0
- Matplotlib 3.7
- Seaborn 0.12
- NetworkX 3.1
- scikit-learn 1.3

---

**Fecha:** [Pendiente]
