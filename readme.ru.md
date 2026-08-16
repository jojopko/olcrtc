<div align="center">

<img src="https://github.com/openlibrecommunity/material/blob/master/olcrtc.png" width="250" height="250">

![License](https://img.shields.io/badge/license-WTFPL-0D1117?style=flat-square&logo=open-source-initiative&logoColor=green&labelColor=0D1117)
![Golang](https://img.shields.io/badge/-Golang-0D1117?style=flat-square&logo=go&logoColor=00A7D0)

**RU** / [EN](readme.md)

</div>

# olcRTC

`olcRTC` (OpenLibreCommunity RTC) - зашифрованный TCP-over-WebRTC туннель. Трафик маскируется под обычный видеозвонок на разрешённых сервисах (Jitsi, Yandex Telemost, WbStream). Внутри - шифрование XChaCha20-Poly1305 и мультиплексирование smux поверх WebRTC data/video каналов.

Статус: **Beta**

```text
app -> SOCKS5 -> olcrtc cnc -> WebRTC/SFU сервис -> olcrtc srv -> интернет
```

> **Важно:** проверяйте, что нужный сервис видеозвонков есть в белых списках и работает в вашей сети. Если нет - используйте другой.

## Возможности

- **Провайдеры:** `jitsi`, `telemost`, `wbstream`
- **Транспорты:** `datachannel`, `vp8channel`, `seichannel`, `videochannel`
- **Платформы:** Linux, macOS, Windows, Android (gomobile), встраиваемая Go-библиотека

Рекомендуемый старт: `jitsi + datachannel`.

## Быстрый старт

Нужны Go 1.26+ и mage.

```sh
go install github.com/magefile/mage@latest
git clone https://github.com/openlibrecommunity/olcrtc --recurse-submodules
cd olcrtc
mage build
```

Сгенерируй общий ключ (одинаковый на сервере и клиенте):

```sh
openssl rand -hex 32
```

Запусти сервер и клиент с YAML-конфигами:

```sh
./build/olcrtc-linux-amd64 server.yaml
./build/olcrtc-linux-amd64 client.yaml
```

Клиент поднимает локальный SOCKS5 на `127.0.0.1:8808`. Проверка:

```sh
curl --socks5-hostname 127.0.0.1:8808 https://icanhazip.com
```

Полные инструкции и примеры конфигов - в [docs/fast.md](docs/fast.ru.md) и [docs/configuration.md](docs/configuration.ru.md).

## Документация

| Документ | Содержание |
|---|---|
| [about.md](docs/about.ru.md) | архитектура, провайдеры, транспорты, публичный API |
| [fast.md](docs/fast.ru.md) | быстрый старт для новичков |
| [manual.md](docs/manual.ru.md) | ручная сборка |
| [configuration.md](docs/configuration.ru.md) | настройка YAML |
| [settings.md](docs/settings.ru.md) | матрица совместимости |
| [uri.md](docs/uri.ru.md) | формат URI клиента |
| [sub.md](docs/sub.ru.md) | формат подписки |

## Сборка

```sh
mage build   # текущая платформа
mage cross   # кросс-компиляция
mage test    # тесты
mage lint    # golangci-lint
mage mobile  # gomobile bindings (Android)
```

## Сообщество

- Telegram: [@openlibrecommunity](https://t.me/openlibrecommunity)
- Issues: [github.com/openlibrecommunity/olcrtc/issues](https://github.com/openlibrecommunity/olcrtc/issues)
- UI-клиент сообщества: [alananisimov/olcbox](https://github.com/alananisimov/olcbox)

## Лицензия

WTFPL

<div align="center">

---

Telegram: [zarazaex](https://t.me/zarazaexe)
<br>
Email: [zarazaex@tuta.io](mailto:zarazaex@tuta.io)
<br>
Site: [zarazaex.xyz](https://zarazaex.xyz)

</div>
