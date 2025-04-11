# clase-del-2-de-abril
# Sintonización PID en Lazo Cerrado

La sintonización PID en lazo cerrado es una técnica muy utilizada en sistemas de control automático para ajustar los parámetros del controlador PID (proporcional, integral y derivativo) a partir del comportamiento real del sistema. Este método se enfoca en obtener una respuesta deseada sin necesidad de conocer el modelo matemático exacto, lo cual lo hace práctico y aplicable a sistemas reales. En esta clase se abordaron los métodos más utilizados: Ziegler & Nichols y el método del relé, junto con el tratamiento del fenómeno wind-up y sus estrategias de corrección.

## 1. Métodos de Sintonización PID

### 1.1. Método de Ziegler & Nichols
- Llevar Ki y Kd a cero.
- Aumentar Kp hasta obtener oscilación sostenida (estado marginalmente estable).
- Medir:
  - Ku: ganancia última.
  - Pu: periodo de oscilación.
- Aplicar fórmulas empíricas según el tipo de controlador.

### 1.2. Método del Relé
- Emplea un relé con histéresis para inducir oscilaciones.
- Evita sobreexcitar el sistema.
- Medir Pu y Au, calcular Kc con:

$$K_c = \frac{4d}{\pi (A_u^2 - \varepsilon^2)}$$

## 2. Definiciones
>🔑 *Sintonización PID:* Ajuste de los parámetros Kp, Ki y Kd de un controlador para obtener un comportamiento deseado del sistema.

>🔑 *Ganancia última (Ku):* Valor de Kp que genera oscilaciones sostenidas en el sistema.

>🔑 *Periodo último (Pu):* Tiempo que dura un ciclo completo de oscilación en el sistema.

>🔑 *Wind-up:* Fenómeno donde la acción integral del controlador sigue acumulando error aunque el actuador esté saturado.

## 3. Anti Wind-up

### 3.1. Por Saturación de la Integral
Bloquea la acumulación de la acción integral cuando el actuador está saturado.

### 3.2. Integración Condicional
Permite integrar solo cuando no hay saturación. Puede generar pulsos no deseados al cortar la integral abruptamente.

### 3.3. Re-cálculo y Seguimiento
Suspende la acción integral suavemente al predecir la saturación, usando:

$$T_t = T_i \cdot T_d$$

## 4. Ejemplos

💡**Ejemplo 1:** Si se obtiene Ku = 60 y Pu = 1.894 s, para control PID:

$$K_p = 0.6 \, Ku = 36$$  
$$T_i = \frac{Pu}{2} = 0.947$$  
$$T_d = \frac{Pu}{8} = 0.236$$

## 5. Ecuaciones

💡**Ejemplo 2:** Cálculo de Kc en método del relé:

$$K_c = \frac{4d}{\pi (A_u^2 - \varepsilon^2)}$$

## 6. Figuras

![Figura de oscilación sostenida](images/pid/osc_sostenida.png)

Figura 1. Ejemplo de oscilación sostenida en método Ziegler & Nichols

## 7. Tablas

💡**Ejemplo 3:** Fórmulas empíricas de Ziegler & Nichols

| Controlador | Kp       | Ti        | Td       |
|-------------|----------|-----------|----------|
| P           | 0.5 Ku   | —         | —        |
| PI          | 0.45 Ku  | Pu / 1.2  | —        |
| PID         | 0.6 Ku   | Pu / 2    | Pu / 8   |

Tabla 1. Parámetros recomendados por Ziegler & Nichols

## 8. Código



## 9. Ejercicios

# 📚 Ejercicio 1
**Enunciado:** Si un sistema presenta oscilaciones sostenidas con Kp = 50 y Pu = 2.5 s, calcule los parámetros de un controlador PID.

**Solución:**  
$$Ku = 50,\quad Pu = 2.5$$  
$$K_p = 0.6 \, Ku = 30$$  
$$T_i = \frac{2.5}{2} = 1.25$$  
$$T_d = \frac{2.5}{8} = 0.3125$$

# 📚 Ejercicio 2
**Enunciado:** Un sistema en prueba con relé tiene Au = 0.4, d = 0.5 y ε = 0.05. Calcule Kc.

**Solución:**  
$$K_c = \frac{4 \cdot 0.5}{\pi (0.4^2 - 0.05^2)} \approx 10.83$$

## 10. Conclusiones

Los métodos de sintonización en lazo cerrado permiten ajustar controladores PID de forma práctica y directa, sin requerir modelos matemáticos detallados del sistema. Tanto Ziegler & Nichols como el método del relé son herramientas válidas y vigentes. Además, es fundamental considerar el fenómeno wind-up e implementar alguna estrategia de anti wind-up para asegurar un comportamiento adecuado en sistemas reales.

## 11. Referencias

- Presentación "Sintonización de controladores PID en lazo cerrado", Ing. Jorge Eduardo Cote B.
- Aström, K.J. y T. Hägglund – "Benchmark Systems for PID Control", IFAC Workshop, 2000.
- Controladores PID - Ajuste empírico, F. Morilla, UNED, 2006.

