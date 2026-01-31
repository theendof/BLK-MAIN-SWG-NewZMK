# Бранч zmk-main-update

## Описание
Экспериментальная ветка прошивки ZMK для **Charybdis 4x6** на базе **nice_nano (nRF52840)** с трекболом **PMW3610**.

## Ключевые особенности

### ZMK и Zephyr
- **ZMK**: актуальная **main** ветка (rolling release)
- **Zephyr**: версия **4.1**
- Переход с `nice_nano_v2` на `nice_nano` в связи с изменениями в Zephyr 4.1

### Аппаратная конфигурация
- **Плата**: nice_nano (ProMicro nRF52840)
- **Раскладка**: Charybdis 4x6 (сплит-клавиатура)
- **Трекбол**: PMW3610 (драйвер от badjeff)
- **Интерфейс**: SPI (CS: P0.20, SCK: P0.08, MOSI/MISO: P0.17, IRQ: P0.06)

### Настройки трекбола (PMW3610)
```
CPI: 1000
swap-xy: включен
invert-x: включен
invert-y: включен
force-awake: включен
Режим: INPUT_EV_REL (mouse movement)
```

### Bluetooth оптимизация
- `CONFIG_BT_BUF_EVT_RX_COUNT=40` - увеличенный буфер для стабильной связи

### Архитектура
- Shield-based конфигурация (`charybdis_left`, `charybdis_right`)
- `input-listener` для обработки трекбола
- Упрощенная структура без input-processors (для стабильности)

## Последние изменения
1. Обновление на ZMK main (Zephyr 4.1)
2. Фикс имени платы: `nice_nano_v2` → `nice_nano`
3. Увеличение BT буфера: `CONFIG_BT_BUF_EVT_RX_COUNT=40`
4. Коррекция направления трекбола: добавлен `invert-x`
5. Упрощение конфигурации: удалены input-processors

## Для чего этот бранч
Тестирование актуальной main ветки ZMK с Zephyr 4.1 для:
- Оценки стабильности новых фич
- Проверки совместимости с PMW3610
- Отладки Bluetooth соединения
- Адаптации под изменения в именовании плат

## Важные ссылки
- [ZMK Firmware](https://github.com/zmkfirmware/zmk)
- [PMW3610 Driver by badjeff](https://github.com/badjeff/zmk-pmw3610-driver)
- [Build workflow](.github/workflows/)

## Предупреждение
⚠️ **Экспериментальный бранч!** Main ветка ZMK может содержать нестабильные изменения. Для production используйте фиксированные версии ZMK.
