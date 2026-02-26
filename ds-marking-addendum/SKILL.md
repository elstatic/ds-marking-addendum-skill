---
name: ds-marking-addendum
description: Generate filled DOCX addenda for mandatory ad-marking services from a provided template and client names (domain or legal entity). Use when the user asks to prepare multiple "ДС на администрирование маркировки рекламных материалов", pull signer/contract data from existing contracts, save outputs in the same folders as the source contracts, and return direct file links.
---

# DS Marking Addendum

Use this skill to produce ready-to-sign DOCX addenda from a user template for one or many clients.

## Workflow

1. Locate template document.
2. Resolve client names to contract folders under `Договоры/Договоры (по клиентам)` in the current workspace.
3. Select active base contract and extract required fields.
4. Generate DS DOCX into the same folder as the selected base contract.
5. Return absolute file paths (one path per output file).

Read detailed field rules in `references/field-checklist.md`.

## Template Handling

- If template is `.gdoc`, open export URL in browser and use downloaded `.docx`.
- If template is already `.docx`, use it directly.

Example export pattern:

```bash
open 'https://docs.google.com/document/d/<DOC_ID>/export?format=docx'
```

## Contract Discovery

Find candidate folders by domain or legal name:

```bash
CONTRACTS_ROOT="$(find . -type d -name 'Договоры (по клиентам)' | head -n 1)"
find "$CONTRACTS_ROOT" -maxdepth 3 -type d | rg -i '<domain|name>'
```

Extract signer/contract details from `.docx` or `.pdf`:

```bash
textutil -convert txt -stdout '<contract.docx>' | sed -n '1,180p'
pdftotext '<contract.pdf>' - | sed -n '1,180p'
```

## Generation Script

Use `scripts/generate_marking_ds.py`.

```bash
python3 "$CODEX_HOME/skills/ds-marking-addendum/scripts/generate_marking_ds.py" \
  --template '<template.docx>' \
  --output '<target-folder>/ДС №<n> к <contract-no> <client>.docx' \
  --ds-no '<n>' \
  --agreement-kind 'agent' \
  --agreement-no '<AG-...>' \
  --agreement-date 'DD.MM.YYYY' \
  --sign-date 'DD.MM.YYYY' \
  --principal-full 'Общество с ограниченной ответственностью «... »' \
  --principal-short 'ООО «... »' \
  --principal-position-intro 'Генерального директора' \
  --principal-position-sign 'Генеральный директор' \
  --principal-signer-full 'Иванова Ивана Ивановича' \
  --principal-signer-short 'Иванов И.И.' \
  --acting-word 'действующего'
```

Use `--agreement-kind contract` for non-agent contracts.

## Output Rules

- Save each generated DS in the same folder as its base contract.
- Keep file names human-readable: `ДС №<n> к <contract-no> <client>.docx`.
- In the final response, list absolute output paths only.
- If a client is ambiguous, report the exact folder candidates and ask for one confirmation before generation.
