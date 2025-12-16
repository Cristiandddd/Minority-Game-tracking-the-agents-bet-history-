# Predicción de Parámetros del Minority Game usando Redes Neuronales Recurrentes

**Autor:** [Tu Nombre]  
**Tutor:** [Nombre del Tutor]  
**Fecha:** [Fecha]  
**Institución:** [Universidad/Instituto]

---

## Resumen Ejecutivo

Este informe presenta el desarrollo de un sistema de predicción basado en redes neuronales recurrentes (GRU) para estimar el parámetro α del Minority Game a partir de secuencias de apuestas históricas. El parámetro α = P/N (donde P = 2^M^) caracteriza la dinámica del juego y determina el régimen de comportamiento del sistema.

**Palabras clave:** Minority Game, Redes Neuronales Recurrentes, GRU, Sistemas Complejos, Predicción de Parámetros

---

## 1. Introducción

### 1.1 El Minority Game

El Minority Game es un modelo de teoría de juegos donde N agentes compiten eligiendo entre dos opciones en cada ronda. Los agentes que pertenecen al grupo minoritario ganan. Cada agente utiliza estrategias basadas en el historial pasado de longitud M para tomar decisiones.

En cada tiempo t:
- Cada agente i elige una acción a~i~(t) ∈ {0, 1}
- Se calcula la asistencia total: A(t) = Σ~i~ a~i~(t)
- Ganan los agentes del lado minoritario: |A(t)| < N/2

### 1.2 Parámetro α (Alpha)

El parámetro α = P/N = 2^M^/N es crucial para caracterizar el comportamiento del sistema:

- **α pequeño (< 0.3):** Sistema frustrado con alta competencia. Los agentes no pueden coordinarse eficientemente y el sistema muestra alta volatilidad.
- **α grande (> 0.5):** Recursos abundantes, baja competencia. El sistema converge a estados predecibles.
- **α crítico (≈ 0.3-0.5):** Transición de fase y comportamiento crítico. El sistema exhibe propiedades complejas y emergentes.

### 1.3 Objetivo

Desarrollar un modelo de aprendizaje profundo capaz de predecir el valor de α observando únicamente el historial de apuestas de los agentes, sin conocimiento explícito de los parámetros del sistema (N, M, P).

**Hipótesis:** Las secuencias de apuestas contienen información suficiente sobre la dinámica del sistema que permite inferir el valor de α.

---

## 2. Metodología

### 2.1 Adquisición de Datos

Los datos fueron generados mediante simulaciones del Minority Game implementado en C++. El sistema exporta el historial de apuestas de cada agente junto con el valor de α correspondiente en archivos JSON con formato `betting_history_{alpha}.json`.

#### Parámetros de Simulación

| Parámetro | Valor |
|-----------|-------|
| Número de agentes (N) | Variable |
| Memoria (M) | Variable |
| Estrategias por agente (S) | 2 |
| Tiempo de equilibración | 10,000 rondas |
| Rondas registradas | 10,000 (post-equilibración) |

La simulación se ejecuta durante `t_eq + 10,000` rondas totales, pero solo se registran las últimas 10,000 rondas para asegurar que el sistema ha alcanzado el estado estacionario.

#### Estructura de los Datos

Cada archivo JSON contiene:
- **game_parameters:** N, M, P, S, alpha, equilibration_time
- **agents:** Array de objetos con el historial de apuestas de cada agente
  - **agent_id:** Identificador único del agente
  - **betting_history:** Array de apuestas [0 o 1] de longitud 10,000
  - **total_bets:** Número total de apuestas registradas

### 2.2 Filtrado de Datos

Se implementó un sistema de filtrado robusto para eliminar secuencias de baja calidad que podrían perjudicar el entrenamiento del modelo.

#### Criterios de Filtrado

**Filtro 1: Secuencias Monótonas**
- Eliminación de secuencias donde todos los valores son idénticos
- Descarte de secuencias con rachas excesivamente largas del mismo valor (> 100 elementos consecutivos)
- **Justificación:** Estas secuencias no contienen información dinámica sobre el sistema

**Filtro 2: Baja Variación Estadística**
- Descarte de secuencias donde una opción domina excesivamente (> 95% de las apuestas)
- **Justificación:** Falta de diversidad en las decisiones indica comportamiento trivial

**Filtro 3: Entropía de la Secuencia**
- Eliminación de secuencias con entropía muy baja (< 0.1)
- Entropía calculada como: H = -Σ p~i~ log(p~i~)
- **Justificación:** Baja entropía indica predictibilidad extrema y falta de información

---

## 3. Resultados del Filtrado de Datos

### 3.1 Estadísticas Generales

Se procesaron **30 archivos** de historial de apuestas, generando un dataset inicial de **7,976 secuencias** de apuestas individuales.

| Categoría | Cantidad | Porcentaje |
|-----------|----------|------------|
| **Ejemplos Aceptados** | 3,271 | 41.0% |
| **Ejemplos Descartados** | 4,705 | 59.0% |
| **Total Procesados** | 7,976 | 100.0% |

### 3.2 Desglose de Descartes

| Criterio de Descarte | Cantidad | Porcentaje del Total Descartado |
|---------------------|----------|----------------------------------|
| Completamente monótonos | 4,705 | 100.0% |
| Poca variación | 0 | 0.0% |
| Otros criterios | 0 | 0.0% |

### 3.3 Análisis de Resultados

El alto porcentaje de descartes (59%) se debe principalmente a secuencias completamente monótonas, donde los agentes repiten la misma apuesta durante toda la simulación. Este comportamiento puede ocurrir cuando:

1. Un agente encuentra una estrategia dominante que nunca cambia
2. El sistema converge a un estado estable muy rápidamente
3. Parámetros extremos de α generan comportamiento trivial
4. El agente tiene estrategias mal inicializadas

**Implicaciones para el entrenamiento:**

- El dataset filtrado de **3,271 secuencias** representa ejemplos de alta calidad con dinámica rica
- Las secuencias aceptadas muestran variabilidad suficiente para capturar patrones complejos
- La eliminación de casos triviales mejora la capacidad del modelo para generalizar

---

## 4. Análisis Exploratorio de Datos

### 4.1 Distribución del Parámetro Alpha

Se analizaron **3,271 ejemplos** de secuencias filtradas, correspondientes a **17 valores únicos** del parámetro α.

#### Estadísticas de Alpha

| Métrica | Valor |
|---------|-------|
| **Mínimo** | 0.3558 |
| **Máximo** | 102.4000 |
| **Media** | 2.5827 |
| **Desviación estándar** | 7.5115 |

![Distribución de Alpha](/images/01-distribucion-alpha.png)

**Interpretación:** La distribución de α muestra una fuerte concentración en valores bajos (α < 5), con aproximadamente 2,700 ejemplos (~82.5%) en este rango. La distribución exhibe una cola larga hacia valores altos, con algunos casos extremos cercanos a α = 100. Esta distribución sesgada refleja que la mayoría de las simulaciones exploraron el régimen de alta competencia (α pequeño), que es el más interesante desde el punto de vista de sistemas complejos.

### 4.2 Análisis de Proporciones de Apuestas

#### Estadísticas de Variación

| Métrica | Valor |
|---------|-------|
| **Proporción media de 1's** | 0.500 |
| **Proporción media de -1's** | 0.500 |
| **Entropía media** | 0.998 |
| **Máxima racha media** | 10.8 |

![Distribución de Proporción de 1's](/images/02-proporcion-1s.png)

**Interpretación:** La distribución de la proporción de apuestas positivas (1's) muestra una distribución aproximadamente normal centrada en 0.5, indicando que las secuencias filtradas mantienen un balance equilibrado entre ambas opciones. Esta simetría es esperada en el Minority Game debido a la naturaleza competitiva del sistema: si un lado se vuelve dominante, los agentes adaptan sus estrategias para explotar el desequilibrio, restaurando el balance. La línea punteada roja marca el 50%, confirmando que la mayoría de los ejemplos exhiben comportamiento balanceado.

### 4.3 Relación entre Proporción de Apuestas y Alpha

![Proporción de 1's vs Alpha](/images/04-proporcion-vs-alpha.png)

**Interpretación:** El gráfico de dispersión revela que la proporción de apuestas positivas se mantiene consistentemente alrededor de 0.5 para todos los valores de α, sin mostrar una correlación clara (correlación = 0.021). Esto indica que el balance entre las dos opciones es una propiedad robusta del Minority Game que se mantiene independiente del régimen de competencia. Sin embargo, se observa mayor dispersión en valores bajos de α (α < 5), sugiriendo que el régimen de alta competencia genera mayor variabilidad en las estrategias individuales, aunque el promedio global permanece balanceado.

### 4.4 Entropía de las Secuencias

![Entropía vs Alpha](/images/03-entropia-vs-alpha.png)

**Interpretación:** La entropía de las secuencias se mantiene consistentemente alta (≈ 0.99-1.0) para todos los valores de α, confirmando que las secuencias filtradas son altamente impredecibles y contienen información rica. La entropía cercana a 1 indica distribución uniforme entre ambas opciones, consistente con el comportamiento caótico esperado en el Minority Game. La correlación prácticamente nula con α (0.00035) sugiere que la impredecibilidad es una característica intrínseca del sistema independientemente del régimen de competencia.

### 4.5 Patrones Temporales en las Secuencias

![Ejemplos de Secuencias Filtradas](/images/05-ejemplos-secuencias.png)

**Interpretación:** Se muestran tres ejemplos representativos de secuencias de apuestas para diferentes valores de α (0.36, 39.38, y 102.40). Las tres secuencias exhiben oscilaciones rápidas entre -1 y 1, sin patrones periódicos obvios, confirmando el comportamiento caótico. Visualmente, no se aprecian diferencias claras entre los regímenes de α bajo, medio y alto, lo que sugiere que las diferencias se encuentran en propiedades estadísticas sutiles de las secuencias que solo pueden ser capturadas por modelos de aprendizaje profundo.

### 4.6 Análisis de Rachas Consecutivas

![Máxima Racha vs Alpha](/images/06-max-racha-vs-alpha.png)

**Interpretación:** La máxima racha consecutiva de la misma apuesta muestra una tendencia débil a disminuir con valores más altos de α (correlación = -0.030). Para α < 5, se observan rachas que van desde 5 hasta 25 timesteps, con mayor concentración en rachas cortas (10-15). Esta variabilidad sugiere que en el régimen de alta competencia, algunos agentes ocasionalmente mantienen la misma estrategia por períodos extendidos. Para α > 20, las rachas máximas son consistentemente más cortas, indicando cambios de estrategia más frecuentes.

### 4.7 Matriz de Correlaciones

![Matriz de Correlaciones](/images/07-matriz-correlaciones.png)

#### Correlaciones con Alpha

| Variable | Correlación con α |
|----------|-------------------|
| **alpha** | 1.000 |
| **prop_positivos** | -0.021 |
| **entropia** | 0.00035 |
| **prop_negativos** | 0.021 |
| **max_racha** | -0.030 |

**Interpretación:** La matriz de correlaciones revela que todas las variables calculadas (proporción de positivos/negativos, entropía, máxima racha) muestran correlaciones extremadamente bajas con α (|r| < 0.03). Esto indica que las características estadísticas simples de primer orden no son suficientes para discriminar entre diferentes valores de α. Las correlaciones perfectamente simétricas entre prop_positivos y prop_negativos (-1.0) confirman la naturaleza binaria balanceada de las apuestas.

**Implicaciones para el modelo GRU:**

1. **Desafío de Predicción:** Las correlaciones bajas sugieren que la información sobre α está codificada en patrones temporales complejos de alto orden, no en estadísticas simples.

2. **Necesidad de Modelos Secuenciales:** Un modelo recurrente como GRU es esencial para capturar dependencias temporales sutiles que no son visibles en análisis estadístico básico.

3. **Justificación del Enfoque:** El hecho de que las secuencias sean visualmente indistinguibles pero correspondan a diferentes α valida la necesidad de utilizar redes neuronales profundas capaces de aprender representaciones latentes complejas.

### 4.8 Conclusiones del Análisis Exploratorio

1. **Dataset de Alta Calidad:** Las 3,271 secuencias filtradas representan ejemplos con alta entropía, balance estadístico, y ausencia de patrones triviales.

2. **Desafío Computacional:** La predicción de α requiere capturar patrones temporales sutiles que no son evidentes en análisis estadístico convencional.

3. **Distribución Sesgada:** El dataset está dominado por valores bajos de α (< 5), lo que puede introducir un sesgo en el modelo hacia este régimen. Esto deberá considerarse en la evaluación.

4. **Robustez del Sistema:** El Minority Game exhibe propiedades universales (balance 50-50, alta entropía) independientes de α, lo que hace que la tarea de predicción sea particularmente desafiante.

---

## 5. Preprocesamiento de Datos

### 5.1 División del Dataset

El dataset filtrado de 3,271 secuencias se dividió en tres conjuntos utilizando una estrategia de división aleatoria estratificada:

| Conjunto | Tamaño | Porcentaje |
|----------|--------|------------|
| **Entrenamiento** | 2,123 | 64.9% |
| **Validación** | 491 | 15.0% |
| **Prueba** | 657 | 20.1% |

**Justificación:** La división 65-15-20 proporciona suficientes datos para entrenamiento mientras mantiene conjuntos de validación y prueba representativos para evaluar la capacidad de generalización del modelo.

### 5.2 Transformación de Secuencias

Las secuencias de apuestas originales en formato {-1, 1} se transformaron al rango {0, 1} para optimizar el entrenamiento de la red neuronal:

$$x_{transformado} = \frac{x_{original} + 1}{2}$$

**Razón:** Las redes neuronales con activaciones sigmoid o tanh convergen más eficientemente con entradas en el rango [0, 1], y esta transformación preserva toda la información temporal de las secuencias.

### 5.3 Formato de Entrada para RNN

Las secuencias fueron reformateadas para cumplir con los requisitos de entrada de redes recurrentes:

**Dimensiones finales:**
- **X_train:** (2,123, 1,000, 1)
- **X_val:** (491, 1,000, 1)
- **X_test:** (657, 1,000, 1)

Donde:
- **Primera dimensión:** Número de ejemplos (muestras)
- **Segunda dimensión:** Longitud de la secuencia temporal (1,000 timesteps)
- **Tercera dimensión:** Número de características por timestep (1 = apuesta binaria)

### 5.4 Normalización del Target (α)

El valor de α fue normalizado usando estandarización Z-score para facilitar el entrenamiento:

$$\alpha_{normalizado} = \frac{\alpha - \mu_{\alpha}}{\sigma_{\alpha}}$$

#### Estadísticas de Normalización

| Métrica | Conjunto Entrenamiento |
|---------|------------------------|
| **Media original (μ)** | 2.5020 |
| **Desviación estándar original (σ)** | 7.1547 |
| **Media escalada** | 0.0000 |
| **Desviación estándar escalada** | 1.0000 |

**Beneficios de la normalización:**

1. **Estabilidad numérica:** Previene problemas de gradientes explosivos o desvanecientes durante el entrenamiento
2. **Convergencia más rápida:** El optimizador puede utilizar tasas de aprendizaje más altas sin inestabilidad
3. **Comparabilidad:** Facilita la interpretación de errores independientemente de la escala original de α
4. **Reversibilidad:** Los valores predichos pueden ser transformados de vuelta a la escala original usando: $$\alpha_{predicho} = \alpha_{normalizado} \times \sigma_{\alpha} + \mu_{\alpha}$$

### 5.5 Verificación de Integridad

Se realizaron verificaciones para asegurar la calidad del preprocesamiento:

- ✓ No hay valores NaN o infinitos en las secuencias
- ✓ Todas las secuencias tienen exactamente 1,000 timesteps
- ✓ Las transformaciones son reversibles
- ✓ Los conjuntos de validación y prueba mantienen la distribución de α del conjunto completo

---

## 6. Arquitectura del Modelo GRU
