# agents

[English](../README.md) · **Русский**

> Набор скиллов для агентов под **вайбкодинг** — Cursor, Claude Code, Codex и др. Быстро шипить с агентом и при этом понимать, что именно построили.

Вайбкодинг ломается, когда нужно дебажить, расширять или защищать код, который писал не ты. Эти скиллы закрывают разрыв: автоматизируют рутину работы с агентом, не превращая тебя в пассивного ревьюера.

---

## Скиллы

| Скилл | Команда | Зачем |
|---|---|---|
| [**learn**](../learn/) | `/learn` | Сократический учитель — проверяет, что ты *понимаешь* код (проблема → решение → контекст), а не просто «работает». Чеклисты в `.learning/`, квизы, интервальное повторение. |

Скиллов будет больше. Каждый — в своей папке с `SKILL.md` и документацией.

---

## Установка

Через [skills CLI](https://github.com/vercel-labs/skills):

```bash
npx skills add MegaBadCoder/agent-skills --list
npx skills add MegaBadCoder/agent-skills --skill learn -g -a claude-code -a cursor -a codex -y
```

Вручную:

```bash
for dir in ~/.claude/skills ~/.cursor/skills ~/.codex/skills; do
  mkdir -p "$dir/learn"
  cp skills/learn/SKILL.md "$dir/learn/SKILL.md"
done
```

Перезапустите агента один раз, если папка `skills/` раньше не существовала.

---

## Структура репо

```
agents/
├── README.md
├── i18n/README.ru.md
├── skills/learn/SKILL.md
└── learn/             # документация
```
