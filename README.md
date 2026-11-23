# Tanque 01 · HMI web del sistema de llenado automático

Interfaz web de operación (HMI) para un sistema de llenado automático de un tanque de 20 L con **ESP32**, dos flotadores y un caudalímetro **YF-S201**. La página se conecta directamente al broker **EMQX Cloud** por **MQTT sobre WebSocket seguro (WSS)**.

**Abrir en línea:** https://fertello29.github.io/tanque-iot-hmi/

## Qué muestra
- Tanque animado con el **nivel virtual**, calculado con los flotadores y la integración del caudal.
- **Caudal** en tiempo real y tendencia de caudal y nivel.
- Estado de la **máquina de estados**: REPOSO, LLENANDO, LLENO y FALLA.
- **Mando:** modo automático o manual, encendido, paro, restablecer falla y calibración del caudalímetro.
- **KPIs** de eficiencia, mantenimiento y seguridad, historial de eventos y alarmas.
- **Modo demostración:** un simulador reproduce la lógica del firmware sin hardware.

## Uso
1. Abrir la página.
2. En la ventana **Conexión**, la dirección del broker y el usuario ya vienen llenos. Solo hay que escribir la **contraseña del usuario `hmi_web`** y presionar **Conectar**.
3. Para probar sin la ESP32, usar **Usar modo demo**.

## Tópicos MQTT
| Tópico | Sentido |
|---|---|
| `iot/tanque01/telemetria` | ESP32 → HMI (cada 1 s) |
| `iot/tanque01/eventos` | ESP32 → HMI |
| `iot/tanque01/estado` | Last Will (`online` / `offline`) |
| `iot/tanque01/config` | Datos del tanque (retenido) |
| `iot/tanque01/cmd` | HMI → ESP32 (`auto`, `manual`, `on`, `off`, `reset`, `calibrar`) |

## Seguridad
La página **no contiene contraseñas**. El usuario `hmi_web` tiene permisos limitados en el broker (ACL): solo puede leer `iot/tanque01/#` y publicar en `iot/tanque01/cmd`.

---
Práctica de IoT Industrial: MQTT, visualización, dashboards y toma de decisiones.
