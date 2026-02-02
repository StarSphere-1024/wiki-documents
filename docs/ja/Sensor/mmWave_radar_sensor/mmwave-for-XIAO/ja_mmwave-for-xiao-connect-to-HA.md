---
description: mmWave センサーが HA に接続する方法の紹介。
title: XIAO 用 mmWave から Home Assistant へ Bluetooth または Wifi 経由で接続
keywords:
- mmwave
- radar
image: https://files.seeedstudio.com/wiki/seeed_logo/logo_2023.png
slug: /ja/mmwave_for_xiao_to_ha_bt
last_update:
  date: 09/14/2024
  author: Allen, Djair
---

# XIAO 用 mmWave から Home Assistant へ Bluetooth 経由で接続

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/mmwave-for-xiao/HA-HiLink/9.png" style={{width:1000, height:'auto'}}/></div>

## はじめに

24GHz mmWave Sensor for XIAO - Human Static Presence は、Seeed Studio XIAO シリーズ用の拡張ボードです。これは FMCW 原理に基づいたアンテナ一体型の高感度 mmwave センサーです。センサー信号処理と正確な人体感知アルゴリズムを組み合わせることで、動いている状態と静止している状態の人体を識別できます。

この章では、主に 24GHz mmWave Sensor for XIAO が Bluetooth 経由で HA に接続する方法を紹介します。24GHz mmWave Sensor for XIAO の詳細な機能については、[こちら](https://wiki.seeedstudio.com/ja/mmwave_for_xiao/)を参照してください。

:::caution
この Wiki のすべての内容は 24GHz mmWave for XIAO にのみ適用され、他のミリ波センサーには使用できない場合があります。
:::

## 入門ガイド

### ハードウェアの準備

この記事では、美観と配線の簡単さのために、mmWave for XIAO を XIAO ESP32C3 と組み合わせて使用し、Home Assistant に接続します。このチュートリアルに正確に従いたい場合は、以下のモジュールを準備する必要があります。

<table align="center">
	<tr>
		<th>Seeed Studio XIAO ESP32C3</th>
        <th>24GHz mmWave for XIAO</th>
	</tr>
	<tr>
		<td><div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/round_display_for_xiao/xiaoesp32c3.jpg" style={{width:200, height:'auto'}}/></div></td>
        <td><div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/mmwave-for-xiao/1.png" style={{width:150, height:'auto'}}/></div></td>
	</tr>
    <tr>
		<td><div class="get_one_now_container" style={{textAlign: 'center'}}>
    		<a class="get_one_now_item" href="https://www.seeedstudio.com/seeed-xiao-esp32c3-p-5431.html" target="_blank">
            <strong><span><font color={'FFFFFF'} size={"4"}> 今すぐ入手 🖱️</font></span></strong>
    		</a>
		</div></td>
        <td><div class="get_one_now_container" style={{textAlign: 'center'}}>
				<a class="get_one_now_item" href="https://www.seeedstudio.com/Seeed-Studio-24GHz-mmWave-for-XIAO-p-5830.html" target="_blank">
				<strong><span><font color={'FFFFFF'} size={"4"}> 今すぐ入手 🖱️</font></span></strong>
				</a>
        </div></td>
	</tr>
</table>

このセンサーは XIAO 互換性のために設計されているため、一般的に、このセンサーを使用したい場合は、XIAO を準備し、センサー用のメスヘッダーピンを取り付ける必要があります。XIAO に接続する際は、センサーの取り付け方向に特に注意してください。逆向きに差し込まないでください。そうしないと、センサーや XIAO を焼損する可能性があります。

:::caution
正しい方向は、センサーのアンテナが外側を向くようにすることです。
:::

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/mmwave-for-xiao/5.png" style={{width:800, height:'auto'}}/></div>

接続方向が正しいことを確認した後、USB-C タイプケーブルをコンピューターまたは 3.3V 電源に接続すると、センサーが動作を開始します。

:::tip
現在 XIAO が手元にない場合は、TTL を 3.3V ピンと GND ピンに接続して mmwave for XIAO に個別に電源を供給することもできます。これもこのチュートリアルの内容を使用して実行できます。このチュートリアルでは、RX と TX ピンを使用する必要はありません。

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/mmwave-for-xiao/HA-HiLink/10.jpg" style={{width:300, height:'auto'}}/></div>
:::


### ソフトウェアの準備

まだ HomeAssistant をインストールしていない場合は、[こちら](https://www.home-assistant.io/installation/)をクリックして公式の HomeAssistant チュートリアルを参照してください。

## 手順

### ステップ 1. デバイスの発見

Home Assistant で、左下の **setting** をクリックし、中央の **Devices&Services** を選択します。

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/mmwave-for-xiao/HA-HiLink/1.png" style={{width:1000, height:'auto'}}/></div>

Discovered ゾーンにセンサーアイコンが表示されるので、**configure** をクリックします。

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/mmwave-for-xiao/HA-HiLink/2.png" style={{width:1000, height:'auto'}}/></div>

ポップアップウィンドウが表示されるので、**submit** をクリックします。

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/mmwave-for-xiao/HA-HiLink/3.png" style={{width:1000, height:'auto'}}/></div>

設定成功のポップアップが表示されるので、**finish** をクリックします。

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/mmwave-for-xiao/HA-HiLink/4.png" style={{width:1000, height:'auto'}}/></div>

### ステップ 2. デバイスの設定

設定済みゾーンで、**ld2410_ble** をクリックします。

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/mmwave-for-xiao/HA-HiLink/5.png" style={{width:1000, height:'auto'}}/></div>

センサー設定ページに入ったら、**1 device** をクリックします。

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/mmwave-for-xiao/HA-HiLink/6.png" style={{width:1000, height:'auto'}}/></div>

センサーの戻り値をダッシュボードに追加します。

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/mmwave-for-xiao/HA-HiLink/7.png" style={{width:1000, height:'auto'}}/></div>

ポップアップウィンドウで **ADD TO DASHBOARD** を選択します。

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/mmwave-for-xiao/HA-HiLink/8.png" style={{width:1000, height:'auto'}}/></div>

最後に、左上の **overview** をクリックすると、mmwave-for-xiao センサーデータがダッシュボードに正常に表示されます。これで mmwave for xiao センサーが Home Assistant に正常に接続されました。

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/mmwave-for-xiao/HA-HiLink/9.png" style={{width:1000, height:'auto'}}/></div>

次に、自動化で創造性を発揮してください！

# ESPHome を使用した Wifi 経由での XIAO 用 mmWave から Home Assistant への接続
以下の yaml ファイルは、ESPHome ファームウェアを使用して、レーダーモジュール付きの Seeed XIAO ESP32-C3 を Home Assistant に接続します：

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

## 技術サポートと製品ディスカッション

弊社製品をお選びいただき、ありがとうございます！弊社製品での体験が可能な限りスムーズになるよう、さまざまなサポートを提供しています。さまざまな好みやニーズに対応するため、複数のコミュニケーションチャネルを提供しています。

<div class="button_tech_support_container">
<a href="https://forum.seeedstudio.com/" class="button_forum"></a>
<a href="https://www.seeedstudio.com/contacts" class="button_email"></a>
</div>

<div class="button_tech_support_container">
<a href="https://discord.gg/eWkprNDMU7" class="button_discord"></a>
<a href="https://github.com/Seeed-Studio/wiki-documents/discussions/69" class="button_discussion"></a>
</div>
