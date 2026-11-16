# NoEdge

🌐 **Language:** [English](#english) | [Русский](#русский)

---

<a name="english"></a>
## 🇬🇧 English

A lightweight, native utility for **Windows 10 / 11** that completely removes **Microsoft Edge** while backing up your bookmarks and keeping **WebView2 Runtime** intact so Windows and third-party apps continue working normally.

### Safety Guarantees

- **WebView2 Runtime & `EdgeCore` preserved:** Explicitly avoids deleting `EdgeWebView2`, `EdgeCore`, or blocking WebView2 updates (`Install{F3017226-...} = 1`). Windows Search, Widgets, Microsoft Office, Discord, Steam, WhatsApp, Visual Studio, and other WebView2-dependent apps keep working without issues.
- **Automatic Bookmark Backup:** Before cleanup, `Bookmarks` from all detected Edge profiles (Stable, Beta, Dev, Canary) are atomically backed up to `%USERPROFILE%\Documents\Edge_Backup`.
- **Safe Windows Integration Cleanup:** Removes Edge shell registrations without corrupting user browser `UserChoice` hashes.

### What It Does (5-Stage Pipeline)

1. **Processes & Services:** Terminates Edge browser/updater processes (without touching `msedgewebview2.exe`) and removes `edgeupdate`, `edgeupdatem`, and `MicrosoftEdgeElevationService`.
2. **Profiles & Backup:** Releases file locks via Windows Restart Manager and backs up user `Bookmarks` to `Documents\Edge_Backup`.
3. **Client Removal:** Unlocks Edge uninstall flags in registry (`experiment_control_labels`, `AllowUninstall`, `NoRemove = 0`), runs `setup.exe --uninstall --msedge ... --force-uninstall` and `MicrosoftEdgeUpdate.exe /uninstall`, removes Edge Appx packages (WinRT `PackageManager`), Provisioned packages (`dism.exe`), and MSI entries (`msiexec.exe`).
4. **Shell & Associations:** Cleans `App Paths\msedge.exe`, `StartMenuInternet\Microsoft Edge`, `RegisteredApplications`, `MSEdge*` / `microsoft-edge` ProgIDs, and `OpenWithProgids`.
5. **Anti-Reinstall & Cleanup:** Blocks automatic Edge channel reinstallation via policies (`DoNotUpdateToEdgeWithChromium = 1`, channel-specific `Install{GUID} = 0` while allowing WebView2) and marks Edge Appx as `Deprovisioned`; cleans startup entries (including `Default\NTUSER.DAT`), scheduled tasks, shortcuts (Desktop, Start Menu, Taskbar), dead registry trees, and leftover Edge folders.

### Features

- **Scan-first workflow:** Shows everything found before performing any removal.
- **Pure Win32 / COM / WinRT APIs:** No `cmd.exe` or `powershell.exe` wrappers.
- **Defender Exclusion Toggle:** Built-in button to add/remove the app from Windows Defender exclusions via native WMI.
- **Multi-language UI:** Automatically adapts to English, Russian, and Ukrainian system locales.

### Requirements & Download

- **OS:** Windows 10 / Windows 11 (Administrator privileges required).
- **Download:** Grab the latest `NoEdge.exe` from the [Releases](../../releases) page and run it as Administrator.

---

<a name="русский"></a>
## 🇷🇺 Русский

Лёгкая нативная утилита для **Windows 10 / 11**, которая полностью удаляет браузер **Microsoft Edge**, предварительно сохраняет закладки пользователя и не затрагивает **WebView2 Runtime**, обеспечивая стабильную работу Windows и программ.

### Безопасность для системы и данных

- **WebView2 Runtime и `EdgeCore` сохраняются:** Программа не удаляет `EdgeWebView2`, не трогает общие бинарники `EdgeCore` и явно разрешает установку/обновление WebView2 (`Install{F3017226-...} = 1`). Поиск Windows, Виджеты, Office, Discord, Steam, WhatsApp, установщик Visual Studio и другие программы продолжают работать без сбоев.
- **Резервная копия закладок:** Перед удалением файлы `Bookmarks` из всех найденных профилей Edge (Stable, Beta, Dev, Canary) атомарно сохраняются в `%USERPROFILE%\Documents\Edge_Backup`.
- **Аккуратная очистка оболочки:** Удаляются только регистрации Edge без повреждения хешей `UserChoice` выбранного вами браузера по умолчанию.

### Как работает (5 этапов)

1. **Процессы и службы:** Останавливает процессы браузера и апдейтера (не затрагивая `msedgewebview2.exe`) и удаляет службы `edgeupdate`, `edgeupdatem`, `MicrosoftEdgeElevationService`.
2. **Профили и бэкап:** Снимает блокировки файлов через Windows Restart Manager и сохраняет закладки в `Documents\Edge_Backup`.
3. **Удаление клиента:** Снимает программные ограничения удаления в реестре (`experiment_control_labels`, `AllowUninstall`, `NoRemove = 0`), запускает `setup.exe` и `MicrosoftEdgeUpdate.exe /uninstall`, удаляет Edge Appx-пакеты (через WinRT `PackageManager`), Provisioned-пакеты (`dism.exe`) и MSI-записи (`msiexec.exe`).
4. **Интеграция и ассоциации:** Очищает `App Paths\msedge.exe`, `StartMenuInternet\Microsoft Edge`, `RegisteredApplications`, ProgID (`MSEdge*`, `microsoft-edge`) и `OpenWithProgids`.
5. **Защита от возврата и следы:** Устанавливает политики блокировки только для каналов браузера Edge (`DoNotUpdateToEdgeWithChromium = 1`, `Install{GUID} = 0` с разрешением WebView2), добавляет ключ `Deprovisioned`, удаляет автозапуск (включая `Default\NTUSER.DAT`), задачи планировщика, ярлыки (Рабочий стол, Пуск, Панель задач), ветки реестра и папки Edge, после чего перезапускает `explorer.exe`.

### Особенности

- **Предварительное сканирование:** Детальный отчёт до внесения любых изменений.
- **Прямые Win32 / COM / WinRT вызовы:** Без `cmd.exe` и `powershell.exe`.
- **Исключения Defender:** Встроенная кнопка добавления/удаления программы в исключения Windows Defender через WMI.
- **Локализация:** Автоматическое переключение интерфейса на русский, украинский или английский язык.

### Запуск и скачивание

- **ОС:** Windows 10 / Windows 11 (требуются права администратора).
- **Скачивание:** Загрузите актуальную версию `NoEdge.exe` со страницы [Releases](../../releases) и запустите от имени администратора.
