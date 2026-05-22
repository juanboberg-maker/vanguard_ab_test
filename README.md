# vanguard_ab_test
# Vanguard A/B Test — Análisis de Resultados

## Contexto del Experimento

Vanguard rediseñó el proceso de onboarding digital que sus clientes siguen para completar una gestión financiera. El experimento comparó el diseño actual (Control) con el nuevo diseño (Test) durante 97 días, del 15 de marzo al 20 de junio de 2017, con ambos grupos corriendo en paralelo. Un total de 50.500 usuarios participaron: 23.532 en Control y 26.968 en Test. El criterio de éxito se definió como una mejora mínima del 5% en la tasa de finalización del proceso.

---

## Hipótesis

- **H1 ✅** ¿El nuevo diseño consigue que más gente termine el proceso?
- **H2 ✅** ¿El nuevo diseño hace el proceso más rápido?
- **H3 ❌** ¿El nuevo diseño reduce los errores y los retrocesos?

---

## Análisis de KPIs

### 1. Completion Rate
Un 3.71% más de usuarios termina el proceso con el nuevo diseño (65.59% → 69.29%). H1 confirmada, aunque la mejora no supera el umbral mínimo del 5%.

### 2. Time per Step
El nuevo diseño es más rápido en general, especialmente en step_3 (-16s). El tiempo en confirm aumenta +311s, pero el tiempo total del proceso es menor en el Test (354s vs 378s). H2 confirmada.

### 3. Error Rate
La tasa de error es prácticamente igual en ambos grupos (53.42% vs 55.10%). Más de la mitad de los usuarios que completan el proceso retroceden en algún momento. H3 no confirmada.

### 4. Momento de Abandono
El abandono en start cae un 10.94pp con el nuevo diseño, pero se redistribuye hacia step_1 (+5.94pp) y step_3 (+3.57pp). El nuevo diseño engancha mejor al principio pero desplaza el problema hacia adelante.

### 5. Drop-off Rate
El nuevo diseño mejora el salto de start a step_1 (-4.83pp) pero el resto de pasos quedan casi igual. El impacto se concentra en la entrada al flujo.

### 6. Tasa de Retorno
En ambos grupos alrededor del 25% de los que abandonan vuelven a intentarlo. El nuevo diseño no cambia este comportamiento.

### 7. Tiempo Total
El Test completa el proceso 24 segundos antes de mediana (354s vs 378s). Pequeño pero consistente con la mejora en step_3.

---

## Test de Hipótesis

Se realizaron dos Z-tests de proporciones con `proportions_ztest` de `statsmodels`.

**Test 1 — Completion Rate**
- Z-statistic: 8.8745 | P-value: 0.0000
- ✅ Estadísticamente significativo
- ❌ No supera el umbral del 5% (diferencia: 3.71pp)

**Test 2 — Abandono en Start**
- Z-statistic: -17.1661 | P-value: 0.0000
- ✅ Estadísticamente significativo
- El nuevo diseño reduce el abandono en start del 13.96% al 9.10% (-4.86pp)

---

## Evaluación del Experimento

### Efectividad del Diseño
El nuevo diseño mejora la completion rate (+3.71pp) de forma significativa pero no alcanza el umbral del 5%. **No se recomienda implementar de forma inmediata.**

**Qué funcionó:**
- Reducción del abandono en start (-4.86pp)
- Mejora del tiempo total (-24s)
- Simplificación de step_3 (-16s)
- Mayor engagement inicial

**Qué no funcionó:**
- Abandono redistribuido a step_1 y step_3
- Error rate sin mejora
- Tiempo muy alto en confirm (+311s)
- Mejora insuficiente en completion rate

### Duración
97 días con ambos grupos en paralelo. Duración adecuada con muestra suficiente. Posibles limitaciones: efecto de novedad y cambios externos durante el periodo.

### Datos Adicionales Necesarios
- Comportamiento dentro de cada paso (clics, scroll depth, campos del formulario)
- Dispositivo y canal de entrada
- Segmentación de usuarios (nuevo vs experimentado)
- Satisfacción y retención post-proceso

---

## Conclusiones y Recomendaciones

El nuevo diseño confirma 2 de las 3 hipótesis: más gente termina el proceso y lo hace más rápido. Sin embargo no resuelve los errores ni la fricción en pasos intermedios. La recomendación es **no implementar de forma inmediata** e iterar sobre step_1, step_3 y confirm antes de lanzar un nuevo test A/B.