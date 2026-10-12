# Simulador: reproducción de Amin, Masada y Womack (1984)

Simulador en línea del controlador auto-sintonizable (STC) multivariable de
Amin, Masada y Womack (1984), aplicado a la caldera de la unidad termoeléctrica
de 600 MW modelada por Usoro (1977). Corre por completo en el navegador: no
necesita MATLAB ni instalar nada.

**Abrir el simulador:** https://marioabdel01-arch.github.io/simulador-amin-usoro/

## Qué simula

- **Planta:** el modelo no lineal de 47 estados de Usoro, con sus lazos PI
  originales, integrado con Runge–Kutta de cuarto orden y paso de 0,1 s.
- **Variables:** se regulan la temperatura del vapor sobrecalentado (TSSO), la
  del recalentado (TRHO) y la presión del vapor (PSSO), manipulando la demanda
  maestra de caldera (CBMD), la inclinación de quemadores (CXGG) y la
  atemperación del sobrecalentador (CWSY).
- **Controladores:**
  - el PI de Usoro;
  - el STC de Amin: ARX 3×3, N = 5, k = 1, T = 20 s, RLS con factor de
    olvido β, y ley de varianza mínima generalizada con ponderación λ;
  - el STC modificado: tabla de parámetros cada 5 % de carga y estimador
    congelado durante el transitorio.
- **Pruebas:** rampas de 90 a 70 % y de 70 a 90 % a 10 %/min, y el 75 %
  constante.
- **Opciones:** λ, β, la ley corregida o la impresa en el artículo (con su
  errata de signo) y la duración.
- **Pestaña «Planta»:** el esquema de la unidad con los valores del modelo en
  el instante actual.

## Verificación

El código es una traducción a JavaScript del simulador en MATLAB de la
reproducción. Las seis corridas del artículo (PI, STC y STC modificado en las
dos rampas) coinciden con las de MATLAB con diferencias menores a 10⁻⁶ en las
salidas, y los índices IAE son idénticos. Para comprobarlo:

```
node verificacion/verifica.js
```

## Estructura

| Archivo | Contenido |
|---|---|
| `index.html`, `css/`, `js/app.js` | interfaz |
| `js/digpte47.js`, `js/funciones.js` | modelo de 47 estados de Usoro (traducido de MATLAB) |
| `js/sim.js` | RLS, ley de control, tabla por carga y lazo de simulación |
| `js/datos.js` | parámetros de la planta, modelo ARX, tabla por carga, covarianza inicial y estados estacionarios |
| `img/esquema_planta.png` | esquema de la planta |
| `verificacion/` | corridas de referencia de MATLAB y el script que las compara |

## Insertarlo en otra página

```html
<iframe src="https://marioabdel01-arch.github.io/simulador-amin-usoro/"
        width="100%" height="1100" style="border:0"></iframe>
```

## Créditos

- Usoro, P. B. (1977). *Modeling and simulation of a drum boiler-turbine power
  plant under emergency state control* [Tesis de maestría, MIT].
- Quintero-Mármol Márquez, E. (2025). *Plantas termoeléctricas: análisis
  dinámico, modelado, simulación y control*. TecNM/CENIDET. (Esquema de la
  planta.)
- Quintero-Mármol Márquez, E. (2026). *Programación asistida por inteligencia
  artificial generativa de modelos de proceso para plantas termoeléctricas: el
  caso del modelo Usoro de 47.º orden* [Documento de trabajo]. TecNM/CENIDET.
  (Conversión del modelo de FORTRAN 77 a MATLAB.)
- Amin, M., Masada, G. Y., y Womack, B. F. (1984). Application of a
  multivariable self-tuning controller to a power plant boiler. *Proceedings of
  the 1984 American Control Conference*, 339–346.

Reproducción y simulador: Ing. Mario Abdel Guerra Pérez y Dr. Enrique
Quintero-Mármol Márquez, TecNM/CENIDET, Departamento de Ingeniería
Electrónica.
