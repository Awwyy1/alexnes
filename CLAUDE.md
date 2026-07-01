# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

Static HTML website for AlexNes (Alexander Nesterenko), a Russian-language addiction therapist based in Germany. Deployed on Vercel. No build system, no npm, no bundler — pure HTML/CSS/JS.

**Live site:** https://alexnes.com  
**Contact:** WhatsApp +49 162 602 7760, Telegram @nesterealex

## No build commands

There is no build step. Edit HTML files directly and push. Vercel deploys automatically on merge to main.

`vercel.json` configures: cleanUrls (no `.html` in URLs), trailingSlash off, legacy redirects from `/blog/article-N` slugs, and security headers.

## File structure

- `/` — root pages: `index.html`, `about.html`, `blog.html`, `reviews.html`, `video.html`, `voprosy.html`, service pages (`terapiya-travmy.html`, `trezvost.html`, etc.)
- `/blog/` — individual article HTML files (~35 articles)
- `/testy/` — psychological test pages
- `/images/` — photos and avatars
- `sitemap.xml` — must be updated manually when adding pages

## Adding a new blog article

Each blog article is a self-contained HTML file in `/blog/`. Copy an existing article (e.g. `blog/prokrastinaciya.html`) and update:

1. **`<head>`**: `<title>`, `<meta name="description">`, `<link rel="canonical">`, OG tags, Twitter Card tags, JSON-LD schema (`headline`, `description`, `url`, `articleSection`, `datePublished`, `dateModified`)
2. **Breadcrumb `<li>`** (last item): article title in `aria-current="page"` span
3. **`article-header`**: `<span class="article-tag">` (category) and `<h1>`
4. **`article-content`**: the article body
5. **Related articles**: 2 `<a class="related-card">` links to thematically related articles

After creating the article file:
- Add a `<article class="blog-card">` entry to **`blog.html`** (prepend to the grid — newest first), with `data-tag` attribute matching the category
- Add a `<url>` entry to **`sitemap.xml`**

## Theming system

Two themes stored in `localStorage` key `theme`: `"neon"` (default, dark purple + violet accent `#8B5CF6`) and `"classic"` (monochrome). CSS uses `[data-theme="neon"]` and `[data-theme="classic"]` attribute selectors on `<html>`. All CSS is inline inside `<style>` tags — there are no external stylesheet files.

Key CSS variables:
```css
--accent-primary  /* white in classic, #8B5CF6 in neon */
--glow-color      /* used for neon box-shadows */
--btn-radius      /* 0 in classic, 50px in neon */
```

## Article categories

`Самооценка`, `Зависимость`, `Отношения`, `Созависимость`, `Психология`, `Реабилитация`, `Родителям`, `Выздоровление`, `Доверие`, `Осознанность`

## Analytics (present in every page)

- Google Analytics: `G-D9MGJNMBVG` + Google Ads `AW-18060459277`
- Microsoft Clarity: `vyoxcpmq95`

---

# Стиль письма — Алекс

## Главное правило
Писать как человек рассказывает другу за кофе. Не как статья из психологического журнала.

## Что нельзя делать никогда

- Никаких длинных тире и никаких тире вообще
- Никаких двоеточий
- Никаких параллельных конструкций для драматического эффекта. То есть вот это запрещено: "Почти получил повышение. Почти запустил проект. Почти построил отношения. Почти." Это самый узнаваемый AI-паттерн
- Никаких коротких ударных предложений через точку для эффекта
- Никаких идеально выстроенных абзацев где каждый делает ровно один чёткий вывод
- Никакой повторяемости слов в риторическом смысле
- Никаких идеальных переходов между мыслями
- Никаких конструкций "это не про X, это про Y". Этот паттерн узнаётся мгновенно
- Никаких заголовков с двоеточием вида "Тема: подзаголовок". Но и не заменять двоеточие всегда одним и тем же словом (например везде "или") — так заголовки статей начинают читаться как один шаблон и выглядят роботизированно. Каждый заголовок переформулировать индивидуально и по-разному, чтобы соседние статьи в ленте не были похожи друг на друга. Годятся точка, запятая с придаточным, заголовок-вопрос, вводное "как" или "почему", или полная переформулировка
- Никакого чётко структурированного идеального текста. Текст не должен выглядеть как отполированная статья где каждый абзац на своём месте и каждая мысль логически вытекает из предыдущей

## Как надо писать

- Длинные предложения которые соединяются через "и", "но", "потому что", "хотя" и гуляют по мысли
- Мысли иногда отвлекаются, меняют направление, возвращаются
- Текст может быть немного сбивчивым, это нормально и даже нужно
- Иногда автор сам не уверен в формулировке и это видно
- Структура с заголовками ок, но внутри каждого раздела живой поток, не список выводов
- Язык простой, иногда разговорный, иногда с небольшими шероховатостями
- Не идеальный текст лучше чем идеально структурированный AI-текст
- Разговорные вкрапления в тексте: "знаете", "ну как бы", "честно говоря", "понимаете", "таким знаете". Не в каждом абзаце, но периодически
- Автор пишет от первого лица, от лица терапевта с личным опытом. "Я часто вижу", "я обычно говорю клиенту", "я замечаю"
- Первый абзац статьи начинается предметно, с конкретной ситуации или наблюдения, а не с общей философской мысли
- Вместо коротких рубленых перечислений через точку использовать перечисление через запятую внутри живого предложения. То есть не "Удобную. Безопасную. Одобряемую." а "Удобную, безопасную, вечно ищущую одобрения, ну вы понимаете о чём я"
- Местами можно слегка дерзить, не бояться быть резким или прямолинейным, писать по-проще без лишней вежливости и обтекаемости

## Пример хорошего фрагмента (одобрен пользователем)

"Я долго не мог понять одну вещь про людей с которыми работаю. Они умные, они явно хотят изменений, они приходят, разбираются, делают выводы, и потом в какой-то момент просто... останавливаются. Причём останавливаются именно тогда когда всё уже почти сложилось."

## Чего избегать в структуре

- Не заканчивать каждый раздел аккуратным выводом или резюме
- Не делать из highlight-блоков красивые цитаты, они должны звучать как живая мысль
- Не подводить читателя за руку от пункта к пункту, пусть переходы будут иногда резкими или неожиданными
