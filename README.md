# Настройка Caddy для работы через Tailscale Serve на Windows 11

## 📌 Что это?

Этот проект позволяет проксировать ваши локальные сервисы (API, WebSocket, админки и т.д.) через Tailscale Serve, используя Caddy в Docker-контейнере.

## ⚙️ Требования

- Windows 11 Pro/Enterprise (с поддержкой виртуализации)
- Включённая виртуализация в BIOS
- Поддержка Hyper-V **или** WSL2
- Установлен [Git](https://git-scm.com/download/win)
- Установлен [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- Установлен [Tailscale](https://tailscale.com/download/windows)

---

## 🚀 Шаги по установке и запуску

### 1. Включить виртуализацию

- Перезагрузите ПК и зайдите в BIOS/UEFI.
- Включите опцию **Intel VT-x / AMD-V** или **Virtualization Technology**.
- Сохраните изменения и перезагрузитесь.

### 2. Установить Git и Docker Desktop

- Скачайте и установите Git с официального сайта.
- Установите Docker Desktop и выберите **режим Hyper-V или WSL2**.

  - Если Hyper-V недоступен, включите WSL2 (инструкция: [официальная от Microsoft](https://learn.microsoft.com/windows/wsl/install)).

> 💡 Убедитесь, что Docker работает.

### 3. Клонировать репозиторий

```bash
git clone https://github.com/JJSGxKD/caddy-for-tailscale.git
```

или скачать репозиторий вручную.

### 4. Настроить `Caddyfile`

Пример `Caddyfile` уже приложен. Замените `DOMAIN` на имя вашего устройства в Tailscale (например: `desktop.tail908.ts.net`), и укажите нужные пути и порты

Читай комментарии в `Caddyfile`!

Вы можете удалить или закомментировать ненужные блоки `handle_path`.

### 5. Запустить контейнер

```bash
docker compose up -d
```

Контейнер запустит Caddy на портах `80`, `443`, `443/udp`.

---

## 🌐 Настройка Tailscale Serve

### 1. Запустить Tailscale

Запустите Tailscale и войдите в свой аккаунт.

### 2. Включить Tailscale Serve

Запускать в Powershell

```bash
tailscale serve 443
```

Или просто настройте домен через Caddy и дайте Tailscale доступ к порту 443 (как указано выше).

> 💡 Можно использовать [MagicDNS](https://tailscale.com/kb/1081/magicdns/) для удобного доступа по домену `https://ваш-хвост.tailXXX.ts.net`.
