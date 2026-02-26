# Field Checklist

Use this checklist before generating each DS.

## Mandatory Inputs

- Template DOCX path.
- DS number (`№1`, `№2`, ...).
- Agreement type (`agent` or `contract`).
- Base contract number.
- Base contract date (`DD.MM.YYYY`).
- DS signing date (`DD.MM.YYYY`).
- Principal full legal name.
- Principal short legal name for signature block.
- Principal signer full name in genitive case.
- Principal signer short name (`Фамилия И.О.`).
- Position in intro (`Генерального директора`, `Директора`, ...).
- Position in signature block (`Генеральный директор`, `Директор`, ...).
- Correct acting word (`действующего` or `действующей`).

## Selection Rules

1. Prefer the latest active contract in the client folder.
2. For this DS workflow, prefer agent contracts (`AG-*`) when available.
3. If the client has only service contracts (`MR-*`), use `--agreement-kind contract`.
4. DS numbering:
   - inspect existing DS in the same contract folder,
   - pick next sequential number,
   - do not duplicate an existing number.

## Quality Checks

- Confirm there are no placeholders left (`___`, `№_`, `AG-______`).
- Confirm section numbering `1..5` is present.
- Confirm signature block has both sides (`Принципал`, `Агент`).
- Confirm output file is in the same folder as base contract.
