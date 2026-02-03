# Figma и пути к файлам

## Скачать и использовать графику

**Правило путей:**
- **При работе с Figma MCP** (get_figma_data, download_figma_images) — всегда **абсолютные пути**:
  - `localPath`: `/Users/olgastepanova/Desktop/mcp_test/images`
- **В коде проекта** (HTML, CSS) — только **относительные пути**:
  - `images/имя-файла.png`, `images/имя-файла.svg`

**Как скачать графику через MCP:**
1. Вызвать `get_figma_data` с `fileKey` и `nodeId` — получить структуру и ID изображений.
2. Вызвать `download_figma_images` с `fileKey`, массивом `nodes` (nodeId, fileName), **`localPath` — абсолютный путь** к папке `images`.
3. В HTML/CSS подставлять только **относительные** пути: `images/имя-файла.png`.

**Если Figma API вернул 429 (Too Many Requests):** подождать и повторить запрос позже либо экспортировать изображения из Figma вручную и положить в папку `images/` с именами, которые ожидает проект (см. список ниже).

**Графика, используемая в проекте (относительные пути в коде):**
- Norton: `images/norton-browsers.png`, `images/norton-before-1.png`, `images/norton-after-1.png`, `images/norton-before-2.png`, `images/norton-after-2.png`, `images/SPC.png`, `images/norton-personalization-before.png`, `images/norton-personalization-after-7ed238.png`, `images/mobile.png`
- Gectaro: `images/gectaro.png`, `images/gectaro-1.png`, `images/role-based_module.png`, `images/gectaro_flows.png`
- **Site (node 2546-5461):** `site.html` — `images/site-hero.png` (и др. по макету).
- **Frame 2546-5382 (About):** `about.html` — `images/about-1.png`, `images/about-gen.png`, `images/about-fantasy.png`, `images/about-gectaro.png`, `images/about-megafon.png`, `images/about-fl.png`.
- **Contact (node 2546-5445):** `contact.html` — `images/Be.svg`, `images/In.svg` (при 429 экспортировать из Figma вручную в `images/`).
- Остальные страницы: см. ссылки в index.html и в соответствующих .html.

---

## BEM naming
В проекте используется методология BEM для классов:
- **Block** — независимый блок (например `project-detail`, `header`)
- **Element** — элемент блока: `block__element` (например `project-detail__nav`, `project-detail__before-after-image-wrapper`)
- **Modifier** — модификатор (при необходимости): `block__element--modifier`

## Пути при работе с Figma MCP
- **При вызове инструментов Figma** (download_figma_images и т.п.) указывайте **абсолютный путь** к папке проекта:
  - Пример: `/Users/olgastepanova/Desktop/mcp_test/images`
  - Параметр `localPath` в MCP должен быть абсолютным.

## Пути в коде проекта
- В HTML и CSS используйте **относительные пути** к изображениям:
  - Пример: `images/norton-browsers.png`, `images/norton-before-1.png`
  - Относительно корня проекта или текущего файла.

## Как скачать графику из макета
1. **Нужна ссылка на файл Figma.** Без неё скачивание через MCP невозможно.
   - Пример: `https://www.figma.com/design/AbCdEf123/...` или `https://www.figma.com/file/AbCdEf123/...`
   - File key = часть после `/design/` или `/file/` (например `AbCdEf123`).
2. Для нужных фреймов/картинок скопируйте **node-id** из URL (параметр `node-id=...`), формат `1234-5678` или `1234:5678`.
3. При вызове MCP `download_figma_images` укажите **абсолютный путь**:
   - `localPath`: `/Users/olgastepanova/Desktop/mcp_test/images`
4. В коде проекта используйте только **относительные** пути: `images/имя-файла.png`.

---

## Ссылки на макеты

**Файл:** Site — **File key:** `FFyS3r0TaIfWTjNtGuD1Os`

| Страница / фрейм | Node ID | Файл в проекте |
|------------------|---------|-----------------|
| Norton | `2546-5641` (MCP: `2546:5641`) | norton.html |
| Site frame | `2546-5461` (MCP: `2546:5461`) | site.html |
| **Frame 2546-5382 (About)** | **`2546-5382`** (MCP: **`2546:5382`**) | **about.html** |
| **Contact** | **`2546-5445`** (MCP: **`2546:5445`**) | **contact.html** |

**Скачивание графики через MCP (абсолютные пути):**
1. `get_figma_data` с `fileKey: "FFyS3r0TaIfWTjNtGuD1Os"`, `nodeId: "2546-5382"` (или `2546:5382`) — получить структуру и ID изображений.
2. `download_figma_images` с `fileKey`, массивом `nodes` (nodeId, fileName), **`localPath`: `/Users/olgastepanova/Desktop/mcp_test/images`** (абсолютный путь).
3. В HTML/CSS использовать только **относительные** пути: `images/имя-файла.png`.

**Contact (2546-5445):** при работе с Figma — `localPath`: `/Users/olgastepanova/Desktop/mcp_test/images`; в коде — `images/contact-*.png` (или имена по экспорту). При 429 экспортировать вручную из макета в папку `images/`.
