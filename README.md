# Confiabilidad y planeación de capacidad de un servicio de inferencia de IA

Proyecto final de **Ciencia Computacional Intermedia** (Universidad Sergio Arboleda, 2026) sobre el caso **AndesVision AI**: análisis de la telemetría de un servicio de clasificación de imágenes para responder tres preguntas de la Dirección Técnica.

- **P1.** ¿Cómo se comportan el tráfico, los fallos y el tiempo de cómputo?
- **P2.** ¿La versión B es mejor que la A?
- **P3.** ¿Cuántas GPU y qué regla de alertas se necesitan si el tráfico se multiplica por 2?

**Integrantes:** Thomas Bacca, María José Pachón, Sara León y Valeria Noreña.
**Profesor:** Ph.D. Ricardo Andrés Fonseca Perdomo.

## Contenido

| Archivo | Descripción |
|---|---|
| `Punto A y B.ipynb` | Limpieza de datos, régimen estable, llegadas (Poisson), reintentos y MLE |
| `Punto_C (1).ipynb` | Tiempo de cómputo en GPU (variable mixta) y tiempo de red |
| `Punto_D.ipynb` | Dependencia tamaño–caché, esperanza condicional y regresión lineal |
| `Punto_E.ipynb` | Monitoreo, reglas de alerta D1/D2 y probabilidad de incidente |
| `Punto_F.ipynb` | Inferencia, bootstrap, comparación de versiones B vs A y validación |
| `Punto_G (2).ipynb` | Simulador de la cola con c GPU y decisión de capacidad |
| `PDF_Manuscrito/` | Deducciones a mano: B3, bloque C, bloque D y bloque F |

## Cómo ejecutarlo

1. Abrir cada notebook en Google Colab.
2. Subir los archivos de datos del grupo (`solicitudes.csv`, `monitoreo.csv` y `solicitudes_validacion.csv`). **No están en el repositorio.**
3. Ejecutar con *Run all*. Toda la aleatoriedad sale de `np.random.default_rng(S)`, así que los resultados se reproducen.

Librerías: `numpy`, `pandas`, `scipy`, `matplotlib`.

## Resultados principales

- El tráfico estable es un proceso de Poisson de unos 21,6 solicitudes/s, con una ráfaga entre 397 s y 577 s.
- La versión B reduce el cómputo medio en la ventana principal, pero la ventaja no se reproduce en la ventana de validación.
- Con el tráfico ×2 bastan **3 GPU** para cumplir el SLO (P(L > 230 ms) ≤ 3 %).
- La regla de alertas recomendada es **«D1 y D2»**.
