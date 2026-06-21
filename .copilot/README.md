# GitHub Copilot Configuration for Mailer

## Instructions
- `copilot-instructions.md` - Global project standards

## Skills
1. `email-validation` - Email address validation
2. `mailer-complete-testing` - Full test design for Mailer

Użycie:
```text
@copilot use email-validation skill
```

## Agents
1. `docs-generator-agent` - Documentation generation
2. [Dodaj więcej w przyszłości]

Użycie:
```text
Generate API documentation for mailer.subscribers module
```

## Workflow
1. Developer pisze kod.
2. Copilot sugeruje pattern z odpowiedniego skill.
3. Dev generuje testy używając skill.
4. Docs generator tworzy dokumentację.
5. Code reviews wspierane instrukcjami.

## Best Practices
- Zawsze patrz na instrukcje przed rozpoczęciem.
- Użyj skill jeśli dostępny.
- Agenci są dla złożonych, wieloetapowych zadań.
