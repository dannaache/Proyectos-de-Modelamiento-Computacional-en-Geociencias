# Modelación Geoquímica de Formaciones – Stage 01

**Formaciones:** La Luna · Mugrosa · Rosablanca · Tablazo  
**Software:** PHREEQC v3 · Database: `phreeqc.dat`  
**Fecha:** Mayo 2026

---

## 1. Introducción

El modelado de interacción agua-roca en formaciones de alta salinidad es fundamental para evaluar la compatibilidad de fluidos de inyección, el riesgo de incrustaciones (scale), y los cambios mineralógicos que alteran la permeabilidad del yacimiento. Este informe presenta la especiación geoquímica inicial de cuatro formaciones del bloque de estudio (La Luna, Mugrosa, Rosablanca y Tablazo) y el estado termodinámico de equilibrio alcanzado tras la reacción agua-roca simulada con PHREEQC, usando el comando `EQUILIBRIUM_PHASES` con masa de agua ajustada a la porosidad del yacimiento.

---

## 2. Escenario Base – Especiación del Agua Cruda

### 2.1 Composición iónica inicial (mg/L)

| Parámetro       | La Luna | Mugrosa | Rosablanca | Tablazo |
|:--------------- |:-------:|:-------:|:----------:|:-------:|
| Temp. (°C)      | 25.0    | 26.1    | 25.0       | 25.0    |
| pH              | 7.90    | 6.60    | 6.10       | 6.10    |
| TDS est. (mg/L) | ~68,644 | ~26,561 | ~94,600    | ~94,600 |
| Na (mg/L)       | 23,845  | 16,399  | 21,840     | 21,840  |
| K (mg/L)        | 2,410   | 71.4    | 3,805      | 3,805   |
| Ca (mg/L)       | 105.0   | 3,402   | 10,685     | 10,685  |
| Mg (mg/L)       | 62.0    | 202.0   | 1,090      | 1,090   |
| Cl (mg/L)       | 38,510  | 20,123  | 56,265     | 56,265  |
| SO₄ (mg/L)      | 185.0   | 19.5    | 233.8      | 233.8   |
| HCO₃ (mg/L)     | 3,357.5 | 127.6   | 747.2      | 747.2   |
| Fe (mg/L)       | 2.8     | 2.8     | 48.8       | 48.8    |

### 2.2 Error de balance de carga eléctrica

| Formación  | Error CBE (%) | Interpretación                                                                             |
|:---------- |:-------------:|:------------------------------------------------------------------------------------------ |
| La Luna    | −1.61         | Aceptable (< ±5%)                                                                          |
| Mugrosa    | **+22.87**    | **Alto** – posible submedición de aniones (HCO₃ o acetatos/ácidos orgánicos no reportados) |
| Rosablanca | +2.08         | Aceptable                                                                                  |
| Tablazo    | +2.08         | Aceptable                                                                                  |

> El alto error de Mugrosa (22.87 %) indica que el análisis de laboratorio tiene deficiencia aniónica significativa. Este valor debe ser considerado en la interpretación de los resultados de Mugrosa.

### 2.3 Índices de saturación (SI) – Escenario Base

Los SI indican la tendencia termodinámica: **SI > 0** → tendencia a precipitar; **SI < 0** → tendencia a disolverse.

| Mineral       | La Luna  | Mugrosa | Rosablanca | Tablazo  |
|:------------- |:--------:|:-------:|:----------:|:--------:|
| Calcita       | **1.22** | 0.05    | **0.65**   | **0.65** |
| Dolomita      | **2.66** | −0.69   | **0.79**   | **0.79** |
| Yeso (Gypsum) | −2.50    | −1.93   | −0.60      | −0.60    |
| Anhidrita     | −2.68    | −2.13   | −0.78      | −0.78    |
| Halita        | −1.90    | −2.33   | −1.75      | −1.75    |
| Siderita      | 0.49     | −0.89   | 0.27       | 0.27     |
| Goethita      | 9.24     | 6.79    | 6.31       | 6.31     |

**Hallazgos clave (agua cruda):**

- **La Luna** presenta la mayor sobresaturación en Calcita (SI = 1.22) y Dolomita (SI = 2.66). Sin la presencia de la roca, el agua tendería a precipitar carbonatos. La alta alcalinidad (3,357 mg/L HCO₃) a pH 7.9 es la responsable.
- **Rosablanca y Tablazo** son idénticas (misma muestra de agua). Moderadamente sobresaturadas en Calcita y Dolomita.
- **Mugrosa** está cercana al equilibrio con Calcita (SI ≈ 0.05), indicando un sistema carbónico casi estabilizado, posiblemente por interacción previa con el yacimiento.
- **Halita, Yeso y Anhidrita** subsaturados en todas las formaciones → no hay riesgo de precipitación de estas fases en el agua cruda.
- **Goethita** fuertemente sobresaturada en todas las formaciones (SI = 6–9), consistente con la presencia de Fe³⁺ oxidado bajo condiciones redox controladas.

---

## 3. Análisis de Interacción Agua-Roca (Equilibrio Termodinámico)

> **Fuente:** `FmSolution_v2.pqi` — archivo de entrada corregido que separa cada formación en una simulación independiente con la directiva `END`, garantizando que PHREEQC ejecute el batch reaction para cada solución + ensamblaje mineral. Se corrigió también la entrada duplicada de Caolinita en Mugrosa. Resultados extraídos de `FmSolution_v2.out`.

### 3.1 Efecto buffer de pH

| Formación  | pH inicial | pH equilibrio | ΔpH   | Proceso dominante                                                     |
|:---------- |:----------:|:-------------:|:-----:|:--------------------------------------------------------------------- |
| La Luna    | 7.90       | **9.34**      | +1.44 | Buffer silicato-carbonato: disolución Illita + precipitación Dolomita |
| Mugrosa    | 6.60       | **9.79**      | +3.19 | Disolución Illita + precipitación K-feldespato; mayor ΔpH de las 4    |
| Rosablanca | 6.10       | **5.67**      | −0.43 | pH baja: precipitación Calcita consume HCO₃⁻; Pirita en equilibrio    |
| Tablazo    | 6.10       | **5.67**      | −0.43 | Ídem Rosablanca (mineralogía y química idénticas)                     |

**La Luna y Mugrosa** presentan un fuerte buffer alcalino impulsado por la disolución de silicatos alumínicos (Illita). **Rosablanca y Tablazo** responden de forma opuesta: la precipitación de Calcita consume alcalinidad, disminuyendo levemente el pH.

### 3.2 Transferencia de masa mineral

Δ Moles = Final − Inicial: **(+) precipitación** | **(−) disolución**. Valores ≈ 0 indican mineral prácticamente inerte bajo las condiciones del ensamblaje.

#### La Luna

| Mineral   | Fórmula                      | Δ Moles       | Proceso       | Implicación geoquímica                                          |
|:--------- |:---------------------------- |:-------------:|:-------------:|:--------------------------------------------------------------- |
| Calcita   | CaCO₃                        | **−6.2×10⁻⁴** | Disolución    | Libera Ca²⁺; consecuencia del pH alto y redistribución de CO₃²⁻ |
| Dolomita  | CaMg(CO₃)₂                   | **+8.4×10⁻⁴** | Precipitación | Elimina Ca²⁺ y Mg²⁺ de la solución                              |
| Illita    | K₀.₆Mg₀.₂₅Al₂.₃Si₃.₅O₁₀(OH)₂ | **−2.5×10⁻³** | Disolución    | Fuente de K⁺, Mg²⁺, Al³⁺ y Si                                   |
| Caolinita | Al₂Si₂O₅(OH)₄                | **+2.9×10⁻³** | Precipitación | Consume Al³⁺ y Si liberado por Illita                           |
| Cuarzo    | SiO₂                         | **+3.0×10⁻³** | Precipitación | Consume exceso de Si                                            |

**Reacciones netas:** Illita → Caolinita + Cuarzo + K⁺ (diagénesis tardía) + dolomitización acoplada.

#### Mugrosa

| Mineral      | Fórmula       | Δ Moles       | Proceso       | Implicación geoquímica                      |
|:------------ |:------------- |:-------------:|:-------------:|:------------------------------------------- |
| Calcita      | CaCO₃         | **+4.0×10⁻⁴** | Precipitación | Ligera incrustación carbonática al subir pH |
| Calcedonia   | SiO₂ (amorfo) | **−7.0×10⁻²** | Disolución    | Gran aporte de Si a la solución             |
| Illita       | K₀.₆…O₁₀(OH)₂ | **−1.5×10⁻³** | Disolución    | Libera K⁺, Al³⁺; eleva pH                   |
| K-Feldespato | KAlSi₃O₈      | **+1.1×10⁻³** | Precipitación | Consume K⁺ y Al³⁺ liberados por Illita      |
| Caolinita    | Al₂Si₂O₅(OH)₄ | **+1.2×10⁻³** | Precipitación | Consume Al³⁺ residual                       |
| Cuarzo       | SiO₂          | **+6.9×10⁻²** | Precipitación | Recristalización de Calcedonia → Cuarzo     |

**Reacciones netas:** Transformación polimorfa Calcedonia → Cuarzo (principal por magnitud) + Illita → K-Feldespato + Caolinita. K cae 97% (2.853 → 0.088 mmol/kgw) por captura en K-Feldespato.

#### Rosablanca y Tablazo

| Mineral   | Fórmula       | Δ Moles (Rosablanca) | Δ Moles (Tablazo) | Proceso              |
|:--------- |:------------- |:--------------------:|:-----------------:|:-------------------- |
| Calcita   | CaCO₃         | +6.9×10⁻⁵            | +1.2×10⁻⁴         | Precipitación mínima |
| Caolinita | Al₂Si₂O₅(OH)₄ | ≈ 0                  | ≈ 0               | Inerte               |
| Pirita    | FeS₂          | ≈ 0                  | ≈ 0               | Inerte               |
| Cuarzo    | SiO₂          | ≈ 0                  | ≈ 0               | Inerte               |

**Sistema casi en equilibrio:** el agua de Rosablanca/Tablazo ya está muy próxima al equilibrio con el ensamblaje mineral. La Calcita precipita en trazas (consume HCO₃⁻ → ΔpH = −0.43 unidades). Pirita, Caolinita y Cuarzo son inertes bajo estas condiciones.

### 3.3 Evolución de concentraciones – todas las formaciones (inicial vs. equilibrio)

#### La Luna

| Ion   | Inicial (mg/L) | Equilibrio (mg/L) | Factor cambio                                               |
|:----- |:--------------:|:-----------------:|:-----------------------------------------------------------:|
| Na    | 23,845         | 23,304            | ≈ 1× (conservativo)                                         |
| K     | 2,410          | 3,051             | +1.27× (enriquecimiento — disolución Illita)                |
| Ca    | 105.0          | **0.72**          | **−146×** (empobrecimiento severo — precipitación Dolomita) |
| Mg    | 62.0           | **0.25**          | **−248×** (empobrecimiento severo — precipitación Dolomita) |
| Cl    | 38,510         | 37,617            | ≈ 1× (conservativo)                                         |
| SO₄   | 185.0          | 180.9             | ≈ 1× (conservativo)                                         |
| HCO₃* | 3,357.5        | 3,757             | +1.12× (leve enriquecimiento)                               |

#### Mugrosa

| Ion   | Inicial (mg/L) | Equilibrio (mg/L) | Factor cambio                                            |
|:----- |:--------------:|:-----------------:|:--------------------------------------------------------:|
| Na    | 16,399         | 16,426            | ≈ 1× (conservativo)                                      |
| K     | 71.4           | **21.2**          | **−3.4×** (empobrecimiento — precipitación K-Feldespato) |
| Ca    | 3,402          | 3,313             | ≈ 1× (leve precipitación Calcita)                        |
| Mg    | 202.0          | 258               | +1.28× (enriquecimiento — disolución Illita)             |
| Cl    | 20,123         | 20,162            | ≈ 1× (conservativo)                                      |
| SO₄   | 19.5           | 19.6              | ≈ 1× (conservativo)                                      |
| HCO₃* | 127.6          | **27.6**          | **−4.6×** (consume alcalinidad al subir pH hasta 9.79)   |

#### Rosablanca

| Ion   | Inicial (mg/L) | Equilibrio (mg/L) | Factor cambio                                                 |
|:----- |:--------------:|:-----------------:|:-------------------------------------------------------------:|
| Na    | 21,840         | 21,230            | ≈ 1× (conservativo)                                           |
| K     | 3,805          | 3,694             | ≈ 1× (conservativo)                                           |
| Ca    | 10,685         | **10,286**        | −1.04× (leve precipitación Calcita)                           |
| Mg    | 1,090          | 1,059             | ≈ 1× (conservativo)                                           |
| Cl    | 56,265         | 54,668            | ≈ 1× (conservativo)                                           |
| SO₄   | 233.8          | 227               | ≈ 1× (conservativo)                                           |
| HCO₃* | 747.2          | 432               | −1.7× (consume alcalinidad — precipitación Calcita + baja pH) |

#### Tablazo

Concentraciones finales idénticas a Rosablanca (misma analítica inicial y mismo ensamblaje mineral). ΔCa = −399 mg/L, ΔHCO₃ = −315 mg/L por precipitación de Calcita (+1.2×10⁻⁴ mol vs +6.9×10⁻⁵ mol de Rosablanca, diferencia proporcional al mayor volumen de agua por porosidad).

*Alcalinidad total expresada como mg/L HCO₃ equivalente (Alk × 61,020 mg/eq × kgw/L).

Na, Cl y SO₄ actúan como **trazadores conservativos** en todas las formaciones, confirmando la integridad de las simulaciones.

---

## 4. Figuras

Las figuras a continuación son generadas por el script `plot_geochem.py`.

---

### Figura 1 – Diagrama de Schoeller

![Diagrama de Schoeller](figures/fig1_schoeller.png)

**Interpretación:** El diagrama semi-logarítmico muestra la "firma química" de cada formación (líneas sólidas) y su estado de equilibrio agua-roca (líneas discontinuas). La Luna y Mugrosa presentan las mayores desviaciones en la dirección alcalina (pH 9.34 y 9.79 respectivamente). El colapso de Ca²⁺ y Mg²⁺ en La Luna hacia valores infra-mg/L es la señal más visible (dolomitización). En Mugrosa, K cae 97% por captura en K-Feldespato. Rosablanca y Tablazo permanecen prácticamente invariantes — confirma que el agua ya está cerca del equilibrio con el ensamblaje Calcita-Caolinita-Cuarzo-Pirita.

---

### Figura 2 – Gráfico de Dispersión 1:1 (La Luna)

![Gráfico 1:1](figures/fig2_scatter_1to1.png)

**Interpretación:** Los puntos sobre la línea 1:1 (verde) indican enriquecimiento por disolución de minerales; los puntos bajo la línea (rojo) indican empobrecimiento por precipitación. Ca y Mg caen drásticamente por debajo de la diagonal — señal inequívoca de precipitación carbonática (dolomitización). K se enriquece por encima de la diagonal, confirmando la disolución de Illita. Na, Cl y SO₄ permanecen en la diagonal, validando su comportamiento conservativo.

---

### Figura 3 – Índice de Saturación de Calcita

![Índice de Saturación Calcita](figures/fig3_si_calcite.png)

**Interpretación:** Las barras azules muestran el SI inicial de la Calcita en el agua cruda (La Luna = 1.2244, Rosablanca = Tablazo = 0.6532, Mugrosa = 0.0542). Las barras verdes muestran el SI final tras la reacción con la roca (SI = 0.00 en todas las formaciones, confirmado por PHREEQC en los Phase assemblage blocks). La mayor corrección ocurre en La Luna; Mugrosa ya estaba casi en equilibrio con la Calcita.

---

## 5. Conclusiones

1. **La Luna** es el agua de formación más reactiva: alta alcalinidad + ensamblaje arcillo-carbonático producen buffer de pH intenso (+1.44 unidades) y dolomitización efectiva que depleta Ca²⁺ (−146×) y Mg²⁺ (−248×).

2. **Mugrosa** muestra el mayor ΔpH (+3.19 unidades, de 6.60 a 9.79) impulsado por la transformación Calcedonia→Cuarzo + disolución de Illita. K cae 97% por precipitación de K-Feldespato. El alto error de balance (22.87%) en el agua cruda debe considerarse al interpretar los índices de saturación iniciales.

3. **Rosablanca y Tablazo** son las salmueras de mayor TDS (~94,600 mg/L) y están casi en equilibrio con el ensamblaje Calcita-Caolinita-Cuarzo-Pirita. Los cambios de equilibrio son mínimos (ΔCa ≈ −400 mg/L, ΔHCO₃ ≈ −315 mg/L) y el pH decrece levemente (−0.43 unidades) por precipitación de Calcita.

4. **Cl⁻, Na⁺ y SO₄²⁻** son trazadores conservativos en todas las formaciones, consistente con la ausencia de fases cloruradas, sulfatadas y sódicas activas en los ensamblajes.

5. La simulación con `FmSolution_v2.pqi` (simulaciones separadas por `END`) confirma que el uso de `EQUILIBRIUM_PHASES` con target SI = 0.00 permite cuantificar la transferencia de masa mineral y predecir la química de yacimiento bajo condiciones in situ para las cuatro formaciones.
