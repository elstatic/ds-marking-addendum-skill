# ds-marking-addendum-skill

Репозиторий с Codex-навыком `ds-marking-addendum`.

## Структура

Навык расположен в подпапке `ds-marking-addendum/`.

Это важно: установка через `skill-installer` должна идти по пути к подпапке навыка, а не по `.`.

## Установка для агентов (рекомендуемый безошибочный способ)

Используйте системный установщик навыков и режим `git`:

```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo elstatic/ds-marking-addendum-skill \
  --path ds-marking-addendum \
  --name ds-marking-addendum \
  --method git
```

Почему так:
- `--path ds-marking-addendum` ставит именно полную папку навыка (включая `scripts/`, `references/`, `agents/`).
- `--method git` обходит частые SSL-ошибки Python (`CERTIFICATE_VERIFY_FAILED`) при download-режиме.

## Переустановка (если навык уже был установлен)

```bash
rm -rf ~/.codex/skills/ds-marking-addendum
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo elstatic/ds-marking-addendum-skill \
  --path ds-marking-addendum \
  --name ds-marking-addendum \
  --method git
```

После установки перезапустите Codex, чтобы навык появился в списке.
