---
description: Introducción de cómo el Sensor mmWave se conecta a HA.
title: mmWave para XIAO a Home Assistant vía Bluetooth o Wifi
keywords:
- mmwave
- radar
image: https://files.seeedstudio.com/wiki/seeed_logo/logo_2023.png
slug: /es/mmwave_for_xiao_to_ha_bt
last_update:
  date: 09/14/2024
  author: Allen, Djair
---

# mmWave para XIAO a Home Assistant vía Bluetooth

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/mmwave-for-xiao/HA-HiLink/9.png" style={{width:1000, height:'auto'}}/></div>

## Introducción

El Sensor mmWave de 24GHz para XIAO - Presencia Estática Humana es una placa de expansión para la serie Seeed Studio XIAO. Es un sensor mmwave de alta sensibilidad integrado con antena que se basa en el principio FMCW. Combinado con el procesamiento de señales del sensor y algoritmos precisos de detección del cuerpo humano, puede identificar cuerpos humanos en estados de movimiento y estacionarios.

Este capítulo introduce principalmente cómo el Sensor mmWave de 24GHz para XIAO se conecta al HA vía Bluetooth. Para características funcionales detalladas del Sensor mmWave de 24GHz para XIAO, puedes consultar [aquí](https://wiki.seeedstudio.com/es/mmwave_for_xiao/).

:::caution
Todos los contenidos de esta Wiki se aplican únicamente al mmWave de 24GHz para XIAO y no pueden ser utilizados en otros sensores de ondas milimétricas.
:::

## Primeros Pasos

### Preparaciones de Hardware

En este artículo, utilizaremos mmWave para XIAO en conjunto con el XIAO ESP32C3 para conectarlo a Home Assistant por motivos de estética y facilidad de cableado. Si quieres seguir este tutorial al pie de la letra, entonces necesitarás preparar los siguientes módulos.

<table align="center">
	<tr>
		<th>Seeed Studio XIAO ESP32C3</th>
        <th>mmWave de 24GHz para XIAO</th>
	</tr>
	<tr>
		<td><div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/round_display_for_xiao/xiaoesp32c3.jpg" style={{width:200, height:'auto'}}/></div></td>
        <td><div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/mmwave-for-xiao/1.png" style={{width:150, height:'auto'}}/></div></td>
	</tr>
    <tr>
		<td><div class="get_one_now_container" style={{textAlign: 'center'}}>
    		<a class="get_one_now_item" href="https://www.seeedstudio.com/seeed-xiao-esp32c3-p-5431.html" target="_blank">
            <strong><span><font color={'FFFFFF'} size={"4"}> Obtener Uno Ahora 🖱️</font></span></strong>
    		</a>
		</div></td>
        <td><div class="get_one_now_container" style={{textAlign: 'center'}}>
				<a class="get_one_now_item" href="https://www.seeedstudio.com/Seeed-Studio-24GHz-mmWave-for-XIAO-p-5830.html" target="_blank">
				<strong><span><font color={'FFFFFF'} size={"4"}> Obtener Uno Ahora 🖱️</font></span></strong>
				</a>
        </div></td>
	</tr>
</table>

El sensor está diseñado para compatibilidad con XIAO, por lo que en general, si quieres usar este sensor, necesitas preparar un XIAO e instalar la fila de pines hembra para el sensor. Al conectar al XIAO, por favor presta especial atención a la dirección de instalación del sensor, por favor no lo conectes al revés, de lo contrario es probable que quemes el sensor o el XIAO.

:::caution
La dirección correcta a seguir es que la antena del sensor debe mirar hacia afuera.
:::

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/mmwave-for-xiao/5.png" style={{width:800, height:'auto'}}/></div>

Después de confirmar que la dirección de conexión es correcta, puedes conectar el cable tipo USB-C a la computadora o fuente de alimentación de 3.3V, y el sensor comenzará a funcionar.

:::tip
Si no tienes un XIAO a mano en este momento, entonces tienes la opción de alimentar el mmwave para XIAO por separado conectando TTL a su pin de 3.3V y pin GND, lo cual también se puede hacer usando el contenido de este tutorial. Para este tutorial, no hay necesidad de usar los pines RX y TX.

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/mmwave-for-xiao/HA-HiLink/10.jpg" style={{width:300, height:'auto'}}/></div>
:::


### Preparaciones de Software

Si aún no has instalado HomeAssistant, puedes consultar el tutorial oficial de HomeAssistant haciendo clic [aquí](https://www.home-assistant.io/installation/).

## Procedimientos

### Paso 1. Descubrir Dispositivo

En Home Assistant, haz clic en **setting** en la esquina inferior izquierda, selecciona **Devices&Services** en el centro.

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/mmwave-for-xiao/HA-HiLink/1.png" style={{width:1000, height:'auto'}}/></div>

En la zona Discovered, habrá un ícono de sensor, haz clic en **configure**.

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/mmwave-for-xiao/HA-HiLink/2.png" style={{width:1000, height:'auto'}}/></div>

Aparecerá una ventana emergente, haz clic en **submit**.

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/mmwave-for-xiao/HA-HiLink/3.png" style={{width:1000, height:'auto'}}/></div>

Verás una ventana emergente de configuración exitosa, haz clic en **finish**.

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/mmwave-for-xiao/HA-HiLink/4.png" style={{width:1000, height:'auto'}}/></div>

### Paso 2. Configurar Dispositivo

En la zona configurada, haz clic en **ld2410_ble**.

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/mmwave-for-xiao/HA-HiLink/5.png" style={{width:1000, height:'auto'}}/></div>

Una vez que estés en la página de configuración del sensor, haz clic en **1 device**.

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/mmwave-for-xiao/HA-HiLink/6.png" style={{width:1000, height:'auto'}}/></div>

Agrega el valor de retorno del sensor al panel de control.

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/mmwave-for-xiao/HA-HiLink/7.png" style={{width:1000, height:'auto'}}/></div>

Selecciona **ADD TO DASHBOARD** en la ventana emergente.

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/mmwave-for-xiao/HA-HiLink/8.png" style={{width:1000, height:'auto'}}/></div>

Finalmente, haz clic en **overview** en la esquina superior izquierda, verás los datos del sensor mmwave-for-xiao mostrados exitosamente en el panel de control. Hasta aquí el sensor mmwave para xiao se ha conectado exitosamente al Home Assistant.

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/mmwave-for-xiao/HA-HiLink/9.png" style={{width:1000, height:'auto'}}/></div>

A continuación, ¡puedes ser creativo con tu automatización!

# mmWave para XIAO a Home Assistant vía Wifi usando ESPHome
El siguiente archivo yaml conecta un Seeed XIAO ESP32-C3 con módulo Radar a Home Assistant, usando el firmware ESPHome:

```
# ==== AUTO-SYNC START: xiao_24ghz_mmwave/xiao_24ghz_mmwave.yaml ====

substitutions:
  name: "xiao-24ghz-mmwave"
  friendly_name: "XIAO 24GHz mmwave"

esphome:
  name: "${name}"
  friendly_name: "${friendly_name}"
  name_add_mac_suffix: True
  on_boot:
    then:
      - deep_sleep.prevent: deepSleep
      - switch.turn_off: RF_en_switch
      - switch.turn_on: ADC_switch
      - switch.turn_on: mmwave_en_switch

esp32:
  board: esp32-c6-devkitc-1
  variant: esp32c6
  flash_size: 4MB    
  framework:
    type: esp-idf

# Enable logging
logger:
  level: NONE

# Enable Home Assistant API
api:
  on_client_connected:
    - logger.log: "API client connected!"
    - delay: 30s
    - deep_sleep.allow: deepSleep

  on_client_disconnected:
    - deep_sleep.prevent: deepSleep

ota:
  - platform: esphome

wifi:
  # Enable fallback hotspot (captive portal) in case wifi connection fails
  ap:
    ssid: "${friendly_name}"

captive_portal:

deep_sleep:
  id: deepSleep
  run_duration: 30s
  sleep_duration: 180min
  wakeup_pin: GPIO2 # D2

uart:
  id: mmWave_uart
  tx_pin: GPIO16  # D6
  rx_pin: GPIO17  # D7
  baud_rate: 256000
  parity: NONE
  stop_bits: 1

ld2410:
  id: ld2410_radar
  uart_id: mmWave_uart
  throttle: 1000ms

text_sensor:
  - platform: ld2410
    status:
      id: "mmWave_status"
      name: "mmWave Status"
      deep_sleep_id: deepSleep

external_components:
  - source: github://pr#7942
    components: [ "adc" ]

  - source:
      type: git
      url: https://github.com/Seeed-Studio/xiao-esphome-projects
      ref: main
    components: [ ld2410 ]

sensor:
  - platform: adc
    id: Battery_ADC
    name: "Battery measurement"
    pin: GPIO1
    attenuation: 12db
    filters:
      - lambda: return x * 2;
    unit_of_measurement: "V"
    update_interval: 5s

output:
  - platform: gpio
    id: power_output
    pin: GPIO19 # D8
  - platform: gpio
    id: RF_output
    pin: GPIO3  # C6
  - platform: gpio
    id: ADC_output
    pin: GPIO20 # D9

switch:
  - platform: output
    id: mmwave_en_switch
    output: power_output
  - platform: output
    id: RF_en_switch
    output: RF_output
  - platform: output
    id: ADC_switch
    output: ADC_output
# ==== AUTO-SYNC END ====
```

## Soporte Técnico y Discusión de Productos

¡Gracias por elegir nuestros productos! Estamos aquí para brindarte diferentes tipos de soporte para asegurar que tu experiencia con nuestros productos sea lo más fluida posible. Ofrecemos varios canales de comunicación para atender diferentes preferencias y necesidades.

<div class="button_tech_support_container">
<a href="https://forum.seeedstudio.com/" class="button_forum"></a>
<a href="https://www.seeedstudio.com/contacts" class="button_email"></a>
</div>

<div class="button_tech_support_container">
<a href="https://discord.gg/eWkprNDMU7" class="button_discord"></a>
<a href="https://github.com/Seeed-Studio/wiki-documents/discussions/69" class="button_discussion"></a>
</div>
