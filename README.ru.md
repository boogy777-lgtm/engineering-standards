# Инженерные стандарты разработки

Русский перевод документации проекта [asckye/engineering-standards](https://github.com/asckye/engineering-standards). Оригинал на китайском языке сохранён в [README.md](README.md).

Универсальные правила инженерной разработки представлены в формате [Agent Skills](https://agentskills.io): их могут загружать AI-агенты, а также читать разработчики. Правила имеют идентификаторы и уровни обязательности.

## Установка

Для Claude Code:

```bash
claude plugin marketplace add asckye/engineering-standards
claude plugin install engineering-standards@asckye-standards
```

Для инструментов, поддерживающих `SKILL.md`, скопируйте нужные каталоги из `skills/` в каталог навыков инструмента (для Codex — `.agents/skills/`). Рекомендуется копировать все восемь каталогов одновременно: между ними существуют ссылки. Работа в других инструментах пока не проверена автором.

## Доступные навыки

| Область | Skill | Дополнительные стандарты | Полный текст | Статус |
|---|---|---|---|---|
| Все проекты | [general-engineering-standard](skills/general-engineering-standard/SKILL.md) | — | [Оглавление](skills/general-engineering-standard/references/contents.md) | 3.0 |
| MCP-серверы | [mcp-server-standard](skills/mcp-server-standard/SKILL.md) | Desktop для локальной части | [Обзор](skills/mcp-server-standard/references/overview.md) | Проект 0.2 |
| Промышленные HMI | [hmi-standard](skills/hmi-standard/SKILL.md) | Desktop | [Правила](skills/hmi-standard/references/rules.md) | 3.0 |
| Машинное зрение | [machine-vision-standard](skills/machine-vision-standard/SKILL.md) | Desktop; HMI при работе с PLC или оператором | [Правила](skills/machine-vision-standard/references/rules.md) | Проект 0.2 |
| Информационные панели | [dashboard-standard](skills/dashboard-standard/SKILL.md) | Web или Desktop | [Правила](skills/dashboard-standard/references/rules.md) | Проект 0.2 |
| Настольные приложения | [desktop-app-standard](skills/desktop-app-standard/SKILL.md) | — | [Правила](skills/desktop-app-standard/references/rules.md) | 3.0 |
| Web-приложения | [web-app-standard](skills/web-app-standard/SKILL.md) | — | [Правила](skills/web-app-standard/references/rules.md) | 3.0 |
| Мобильные приложения | [mobile-app-standard](skills/mobile-app-standard/SKILL.md) | — | [Правила](skills/mobile-app-standard/references/rules.md) | 3.0 |

Общий стандарт применяется ко всем проектам. Автор отмечает отсутствие экспериментальных данных об эффективности и внешней экспертизы.

## Принцип действия

При выполнении задачи агент загружает соответствующий навык. `SKILL.md` содержит минимальный контрольный список и указания, какие материалы следует читать для конкретной задачи. Полные правила расположены в `references/`, шаблоны — в `assets/`. Это позволяет не загружать весь текст в контекст без необходимости.

Навык не обеспечивает принудительного исполнения: агент может не загрузить его либо нарушить правило. Автоматизируемые проверки следует закреплять в CI, см. [раздел 24](skills/general-engineering-standard/references/24-enforcement.md).

## Применение в проекте

1. Изучите [минимальный перечень](skills/general-engineering-standard/SKILL.md#minimum), [основной маршрут](skills/general-engineering-standard/references/00b-golden-path.md), [сценарии задач](skills/general-engineering-standard/references/00c-playbooks.md) и [быструю поставку](skills/general-engineering-standard/references/00d-fast-delivery.md).
2. По разделам 0.1 и 0.2 определите класс проекта (S, M, L) и его тип. Укажите их в README проекта в строке «Инженерные стандарты», чтобы агент мог определить применимые правила.
3. По [разделу 25](skills/general-engineering-standard/references/25-adoption.md) создайте структуру проекта, точку входа сборки и механизм контроля соблюдения правил.
4. Для централизованного учёта класса, типа и долговременных исключений используйте [шаблон внедрения](skills/general-engineering-standard/assets/project-adoption.md).

## Версии и изменения

Общий стандарт и специализированные навыки имеют собственные версии и статусы. При выпуске изменяется также `version` в `.claude-plugin/plugin.json`. Правила версионирования приведены в G-07, история — в [CHANGELOG.md](CHANGELOG.md).

После изменения стандартов выполните:

```bash
python build-tools/check_standards.py
python -m unittest discover -s build-tools
```

Проверяются внутренние ссылки, идентификаторы правил, обоснования, раздел 24, версии, контрольные списки, формат навыков и имя плагина. Для опубликованных правил MUST дополнительно контролируется отсутствие снижения обязательности, удаления или сужения области применения.

В `evals/` находятся задания для оценки навыков с помощью Claude Code (требуется вход в учётную запись). Результаты сохраняются в `evals/results/`:

```bash
claude plugin eval . --allow-tools Write --no-publish
```

## План развития

- Общий стандарт: экспериментальные результаты и контрольные списки по масштабу проекта.
- MCP-стандарт: применение в новом проекте перед выпуском 1.0.
- Машинное зрение и информационные панели: испытания в новых проектах, корректировка правил и уровней перед выпуском 1.0.

## Обратная связь

Вопросы и предложения: [GitHub Issues исходного проекта](https://github.com/asckye/engineering-standards/issues).

## Лицензия и атрибуция

Copyright © 2026 asckye. Документация, навыки и тестовые задания распространяются по [CC BY 4.0](LICENSE), сценарии в `build-tools/` — по [MIT](build-tools/LICENSE).

Основание перевода: «工程开发规范», asckye, [исходный репозиторий](https://github.com/asckye/engineering-standards), CC BY 4.0. Изменение: перевод README на русский язык. Перевод не изменяет обязательность правил и не заменяет оригинал.
