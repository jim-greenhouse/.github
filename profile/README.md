<!--
  GreenSense — GitHub organisation profile README.
  Lives in jim-greenhouse/.github/profile/README.md
  Rendered automatically at https://github.com/jim-greenhouse
-->

<div align="center">
  <a href="https://green-sense.ru">
    <img src="./logo.svg" alt="GreenSense" width="120" height="120" />
  </a>

  <h1>GreenSense</h1>

  <p>
    <b>Локальная IoT-платформа для&nbsp;промышленных теплиц</b><br/>
    <sub>Автономные устройства <code>Sprout</code> на&nbsp;ESP32-C6 + LoRa&nbsp;868&nbsp;МГц · real-time телеметрия · рекомендации агроному · автоматические задачи для&nbsp;работников</sub>
  </p>

  <p>
    <a href="https://demo.green-sense.ru">
      <img alt="Открыть демо" src="https://img.shields.io/badge/demo-green--sense.ru-00b85e?style=for-the-badge&logo=react&logoColor=white" />
    </a>
    <a href="https://green-sense.ru">
      <img alt="Сайт" src="https://img.shields.io/badge/landing-green--sense.ru-0b1116?style=for-the-badge&labelColor=00b85e" />
    </a>
    <a href="mailto:info@green-sense.ru">
      <img alt="Email" src="https://img.shields.io/badge/info@green--sense.ru-0b1116?style=for-the-badge&logo=maildotru&logoColor=00b85e" />
    </a>
    <a href="https://t.me/GreenSense_Manager">
      <img alt="Telegram" src="https://img.shields.io/badge/Telegram-0b1116?style=for-the-badge&logo=telegram&logoColor=00b85e" />
    </a>
  </p>

  <p>
    <img alt="On-premise" src="https://img.shields.io/badge/deployment-on--premise-36ef96?style=flat-square" />
    <img alt="LoRa 868" src="https://img.shields.io/badge/radio-LoRa%20868%20MHz-36ef96?style=flat-square" />
    <img alt="ESP32-C6" src="https://img.shields.io/badge/MCU-ESP32--C6-a78bfa?style=flat-square" />
    <img alt="MQTT" src="https://img.shields.io/badge/bus-MQTT-a78bfa?style=flat-square" />
    <img alt="TimescaleDB" src="https://img.shields.io/badge/DB-PostgreSQL%20%2B%20TimescaleDB-3aa6ff?style=flat-square" />
    <img alt="License" src="https://img.shields.io/badge/license-Proprietary-f5a524?style=flat-square" />
  </p>
</div>

---

## 🌱 О&nbsp;продукте

**GreenSense** — это законченная IoT-платформа для&nbsp;тепличных хозяйств, которая решает три задачи разом:

1. **Видит, что происходит в&nbsp;каждом секторе** — каждые 60 секунд снимает 8 метрик с&nbsp;воздуха, почвы, света и&nbsp;CO₂.
2. **Подсказывает агроному, что делать** — рекомендации с&nbsp;обоснованием, основанные на&nbsp;фазе роста культуры и&nbsp;истории метрик.
3. **Распределяет работу команде** — автоматические задачи для&nbsp;работников с&nbsp;приоритетом и&nbsp;дедлайном.

Главное отличие от&nbsp;«облачных коробок» — **всё работает локально**. Серверная стойка на&nbsp;Raspberry&nbsp;Pi рядом с&nbsp;теплицей хранит данные, обслуживает интерфейс и&nbsp;принимает LoRa-пакеты. Интернет нужен только если вы&nbsp;сами захотите удалённый доступ.

---

## 🛰️ Sprout — наше устройство

<table>
  <tr>
    <td width="50%" valign="top">
      <p>
        <b>Sprout</b> — это автономный аппаратный узел, который мы&nbsp;разработали специально для&nbsp;этой платформы. Один компактный IP65-корпус, который ставится прямо в&nbsp;грядке, содержит:
      </p>
      <ul>
        <li><b>8 сенсоров</b> на&nbsp;борту: <code>BME280</code> (температура&nbsp;/ влажность&nbsp;/ давление), <code>SCD41</code> (CO₂), <code>TSL2591</code> (свет), <code>DS18B20</code> (температура почвы), <code>PH-4502C</code> (pH), <code>EC&nbsp;Gravity</code> (электропроводность), <code>Soil&nbsp;V1.2</code> (влажность почвы).</li>
        <li><b>FireBeetle&nbsp;2 ESP32-C6</b> — RISC-V&nbsp;160&nbsp;МГц с&nbsp;deep-sleep.</li>
        <li><b>LoRa&nbsp;868&nbsp;МГц</b>, дальность до&nbsp;5&nbsp;км в&nbsp;поле.</li>
        <li><b>Li-Po 5000&nbsp;мАч + солнечная панель</b> — автономность до&nbsp;30 дней без&nbsp;зарядки.</li>
        <li><b>OLED-дисплей</b> с&nbsp;живыми показаниями.</li>
      </ul>
      <p>
        В&nbsp;API, базе данных и&nbsp;спецификациях Sprout проходит как <code>MetricCollectorDevice</code> — это его техническое имя. Для&nbsp;пользователей мы&nbsp;везде говорим «Sprout».
      </p>
    </td>
    <td width="50%" valign="top" align="center">
      <pre style="display:inline-block; text-align:left; font-size:11px;">
┌──────────────────────────────┐
│ ☀  SOLAR 6V · 10W            │
├──────────────────────────────┤
│ ┌────────────┐  ┌──────────┐ │
│ │ OLED       │  │ ESP32-C6 │ │
│ │ SP-1024    │  │ FireBeetle│ │
│ │ T 23.4°C   │  └──────────┘ │
│ │ RH 68%     │  ┌────┬────┐  │
│ │ CO₂ 1024   │  │BME │SCD │  │
│ └────────────┘  │280 │41  │  │
│ ┌──────────┐    └────┴────┘  │
│ │ LoRa     │    ┌──────────┐ │
│ │ 868 MHz  │    │ TSL2591  │ │
│ └──────────┘    └──────────┘ │
│ 🔋 Li-Po 5000 mAh · 3.7V     │
│ ● ● ● ● ●                    │
│ soil  T°  pH  EC  UV         │
└──────────────────────────────┘
      </pre>
    </td>
  </tr>
</table>

---

## 🏗️ Архитектура

Четыре сервиса, развёрнутых локально на&nbsp;одной Raspberry&nbsp;Pi:

```mermaid
flowchart LR
    subgraph T["🌿 Теплица"]
        D1["Sprout&nbsp;#1<br/>ESP32-C6 + 8 сенсоров"]
        D2["Sprout&nbsp;#2<br/>…"]
        DN["Sprout&nbsp;#N"]
    end

    subgraph PI["🍓 Raspberry Pi · on-premise"]
        GW["Gateway<br/>LoRa → MQTT bridge"]
        MQ["MQTT-брокер<br/>Mosquitto :1883"]
        API["GreenSense API<br/>/api/v1 · JWT<br/>PostgreSQL + TimescaleDB"]
        UI["GreenSense UI<br/>React"]
    end

    USR(["👤 Агроном /<br/>работник"])

    D1 -.->|LoRa 868| GW
    D2 -.->|LoRa 868| GW
    DN -.->|LoRa 868| GW
    GW -->|publish| MQ
    MQ -->|subscribe| API
    API <-->|REST| UI
    UI -->|браузер| USR

    classDef device fill:#0b1116,stroke:#36ef96,color:#e2e8f0
    classDef service fill:#0b1116,stroke:#3aa6ff,color:#e2e8f0
    classDef bus fill:#0b1116,stroke:#a78bfa,color:#e2e8f0
    classDef api fill:#0b1116,stroke:#f5a524,color:#e2e8f0
    classDef user fill:#1c2a3a,stroke:#36ef96,color:#e2e8f0

    class D1,D2,DN device
    class GW service
    class MQ bus
    class API api
    class UI service
    class USR user
```

> **MQTT-брокер** в&nbsp;этой архитектуре нужен для&nbsp;развязки приёма пакетов от&nbsp;их&nbsp;хранения — Gateway может работать и&nbsp;при&nbsp;кратковременной недоступности API, накапливая пакеты в&nbsp;брокере.

---

## 🚀 Демо

Откройте интерактивную демо-версию web-app в&nbsp;браузере. Полностью рабочее приложение с&nbsp;mock-данными: создавайте теплицы и&nbsp;секторы, смотрите gauge'и и&nbsp;графики, выполняйте задачи, редактируйте шаблоны культур.

<p align="center">
  <a href="https://demo.green-sense.ru">
    <img alt="Открыть демо" src="https://img.shields.io/badge/▶%20Открыть%20demo.green--sense.ru-00b85e?style=for-the-badge&logoColor=white" height="48" />
  </a>
</p>

---

## 📦 Репозитории

| Репозиторий | Назначение | Стек |
|---|---|---|
| [`web-app`](https://github.com/jim-greenhouse/web-app) | Веб-интерфейс GreenSense UI — пользовательский фронтенд платформы | React 18 · TypeScript · Vite · Tailwind · TanStack Query · Recharts |
| [`landing`](https://github.com/jim-greenhouse/landing) | Маркетинговый сайт [green-sense.ru](https://green-sense.ru) | Vite · vanilla JS · GSAP |
| [`api`](https://github.com/jim-greenhouse/api) | GreenSense API — REST `/api/v1`, авторизация, бизнес-логика | _(closed-source / Go / PostgreSQL + TimescaleDB)_ |
| [`gateway`](https://github.com/jim-greenhouse/gateway) | Локальный шлюз: LoRa → MQTT-bridge на&nbsp;Raspberry&nbsp;Pi | _(closed-source / Rust)_ |
| [`firmware`](https://github.com/jim-greenhouse/firmware) | Прошивка устройств Sprout (MetricCollectorDevice) | C++ · PlatformIO · ESP-IDF · Arduino-LoRa |
| [`hardware`](https://github.com/jim-greenhouse/hardware) | Схемы и&nbsp;PCB для&nbsp;Sprout, BOM, корпуса | KiCad · STEP |
| [`spec`](https://github.com/jim-greenhouse/spec) | OpenAPI + AsyncAPI спецификации платформы | YAML · OpenAPI 3.1 |

---

## 🧰 Технологический стек

<table>
  <tr>
    <th>Слой</th>
    <th>Технологии</th>
  </tr>
  <tr>
    <td><b>Фронтенд</b></td>
    <td>
      <img src="https://img.shields.io/badge/React%2018-0b1116?logo=react&logoColor=61dafb" />
      <img src="https://img.shields.io/badge/TypeScript-0b1116?logo=typescript&logoColor=3178c6" />
      <img src="https://img.shields.io/badge/Vite-0b1116?logo=vite&logoColor=ffc000" />
      <img src="https://img.shields.io/badge/Tailwind-0b1116?logo=tailwindcss&logoColor=06b6d4" />
      <img src="https://img.shields.io/badge/TanStack%20Query-0b1116?logo=reactquery&logoColor=ff4154" />
      <img src="https://img.shields.io/badge/Recharts-0b1116?logo=chartdotjs&logoColor=00b85e" />
      <img src="https://img.shields.io/badge/Zustand-0b1116?logoColor=fff" />
    </td>
  </tr>
  <tr>
    <td><b>Бэкенд</b></td>
    <td>
      <img src="https://img.shields.io/badge/REST%20API-0b1116?logo=openapiinitiative&logoColor=00b85e" />
      <img src="https://img.shields.io/badge/JWT%20auth-0b1116?logo=jsonwebtokens&logoColor=fff" />
      <img src="https://img.shields.io/badge/MQTT-0b1116?logo=mqtt&logoColor=a78bfa" />
      <img src="https://img.shields.io/badge/Mosquitto-0b1116?logo=eclipsemosquitto&logoColor=3aa6ff" />
    </td>
  </tr>
  <tr>
    <td><b>Хранилище</b></td>
    <td>
      <img src="https://img.shields.io/badge/PostgreSQL-0b1116?logo=postgresql&logoColor=4169e1" />
      <img src="https://img.shields.io/badge/TimescaleDB-0b1116?logo=timescale&logoColor=fdb515" />
    </td>
  </tr>
  <tr>
    <td><b>Железо</b></td>
    <td>
      <img src="https://img.shields.io/badge/FireBeetle%202%20ESP32--C6-0b1116?logo=espressif&logoColor=e7352c" />
      <img src="https://img.shields.io/badge/LoRa%20868%20MHz-0b1116?logo=arm&logoColor=0091bd" />
      <img src="https://img.shields.io/badge/Raspberry%20Pi-0b1116?logo=raspberrypi&logoColor=c51a4a" />
      <img src="https://img.shields.io/badge/PlatformIO-0b1116?logo=platformio&logoColor=f7822c" />
    </td>
  </tr>
  <tr>
    <td><b>Сенсоры</b></td>
    <td>
      <img src="https://img.shields.io/badge/BME280-0b1116?logoColor=fff" />
      <img src="https://img.shields.io/badge/SCD41-0b1116?logoColor=fff" />
      <img src="https://img.shields.io/badge/TSL2591-0b1116?logoColor=fff" />
      <img src="https://img.shields.io/badge/DS18B20-0b1116?logoColor=fff" />
      <img src="https://img.shields.io/badge/PH--4502C-0b1116?logoColor=fff" />
      <img src="https://img.shields.io/badge/EC%20Gravity-0b1116?logoColor=fff" />
    </td>
  </tr>
</table>

---

## 📐 Метрики и&nbsp;единицы измерения

На&nbsp;каждом Sprout мы&nbsp;снимаем **14 типов метрик**, объединённых в&nbsp;четыре группы:

<table>
<tr><th>Группа</th><th>Метрика</th><th>Ед.</th><th>Норма</th><th>Источник</th></tr>
<tr><td rowspan="5"><b>🌬️ Атмосфера</b></td>
  <td><code>AIR_TEMPERATURE</code></td><td>°C</td><td>18–28</td><td>BME280</td></tr>
<tr><td><code>AIR_HUMIDITY</code></td><td>%</td><td>55–85</td><td>BME280</td></tr>
<tr><td><code>ATMOSPHERIC_PRESSURE</code></td><td>hPa</td><td>980–1030</td><td>BME280</td></tr>
<tr><td><code>VPD</code></td><td>kPa</td><td>0.4–1.4</td><td>расчётно</td></tr>
<tr><td><code>CO2_CONCENTRATION</code></td><td>ppm</td><td>400–1500</td><td>SCD41</td></tr>

<tr><td rowspan="2"><b>☀️ Свет</b></td>
  <td><code>LIGHT_LUX</code></td><td>lx</td><td>5k–50k</td><td>TSL2591</td></tr>
<tr><td><code>UV_INDEX</code></td><td>—</td><td>0–10</td><td>SI1145</td></tr>

<tr><td rowspan="4"><b>🌱 Почва</b></td>
  <td><code>SOIL_MOISTURE</code></td><td>%</td><td>30–80</td><td>Soil V1.2</td></tr>
<tr><td><code>SOIL_TEMPERATURE</code></td><td>°C</td><td>16–26</td><td>DS18B20</td></tr>
<tr><td><code>SOIL_PH</code></td><td>pH</td><td>5.5–7.5</td><td>PH-4502C</td></tr>
<tr><td><code>SOIL_EC</code></td><td>mS/cm</td><td>1.2–3.5</td><td>EC Gravity</td></tr>

<tr><td rowspan="3"><b>🔋 Sprout-узел</b></td>
  <td><code>BATTERY_LEVEL_PERCENT</code></td><td>%</td><td>&gt;&nbsp;20</td><td>внутр.</td></tr>
<tr><td><code>LORA_RSSI</code></td><td>dBm</td><td>&gt;&nbsp;−90</td><td>LoRa</td></tr>
<tr><td><code>LORA_SNR</code></td><td>dB</td><td>&gt;&nbsp;0</td><td>LoRa</td></tr>
</table>

---

## 👥 Кто&nbsp;и&nbsp;что видит

GreenSense рассчитан на&nbsp;три рабочих места. Каждая роль видит свой набор экранов и&nbsp;действий — без&nbsp;«перегруза» функциями, которые конкретному человеку не&nbsp;нужны.

| Роль | Что делает в&nbsp;системе |
|---|---|
| 👑 **OWNER** | Полный доступ. Управление организацией, передача владения. |
| ⚙️ **ADMIN** | Создание/удаление теплиц, регистрация Sprout-узлов, пользователи, инфраструктура. |
| 🌿 **AGRONOMIST** | Управление секторами и&nbsp;фазами роста, шаблоны культур, приём рекомендаций, аналитика телеметрии. |
| 🧤 **WORKER** | Канбан задач, выполнение поручений, комментарии. |

---

## 📚 Документация

- **Архитектура и&nbsp;API** — [`jim-greenhouse/spec`](https://github.com/jim-greenhouse/spec): `openapi-webapi.yaml`, `openapi-gateway.yaml`, `asyncapi-mqtt.yaml`
- **Пользовательская документация** — встроена в&nbsp;интерфейс: [demo.green-sense.ru/docs](https://demo.green-sense.ru/docs) (22 раздела: обучение, оборудование, метрики, FAQ)
- **Руководство по&nbsp;развёртыванию** — [`api`](https://github.com/jim-greenhouse/api) → `docs/deployment.md`
- **Прошивка Sprout** — [`firmware`](https://github.com/jim-greenhouse/firmware) → `README.md`

---

## 🤝 Связь

| | |
|---|---|
| 📧 Email | [info@green-sense.ru](mailto:info@green-sense.ru) |
| 📞 Телефон | [+7 (987) 420-58-33](tel:+79874205833) |
| 💬 Telegram | [@GreenSense_Manager](https://t.me/GreenSense_Manager) |
| 🌐 Сайт | [green-sense.ru](https://green-sense.ru) |
| ▶️ Демо | [demo.green-sense.ru](https://demo.green-sense.ru) |

---

<div align="center">

**Сделано в&nbsp;Казани, с любовью&nbsp;к зелени.**

<sub>© 2026 GreenSense. Все права защищены.</sub>

</div>
