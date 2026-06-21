# GitHub Copilot Instructions - Mailer Project

## 1. Python and Dependencies
- Use Python 3.9+.
- Keep dependencies explicit and current in `requirements.txt`.
- Prefer `black`, `flake8`, and `pytest` for formatting, linting, and tests.
- Use type hints for public functions, methods, and module-level helpers.

## 2. Code Style
- Follow PEP 8 in all Python files.
- Keep functions focused and short; split complex logic into helpers.
- Keep modules small and cohesive.
- Use clear, descriptive names for variables, functions, classes, and files.

## 3. Project Structure
- `mailer/` contains business logic and should not depend on Flask templates or static assets.
- `templates/` contains Flask HTML templates only.
- `static/` contains CSS and JavaScript assets only.
- `tests/` contains pytest test modules and fixtures.

## 4. Testing
- Every meaningful change should include or update tests.
- Use `pytest` and `pytest-cov` for the test suite.
- Mock SMTP, external services, and filesystem interactions where appropriate.
- Keep tests deterministic and isolated.
- For detailed test design, use the Mailer Complete Testing Skill.
- Minimum expectation: at least 2 tests per function, edge cases, error handling, and external service mocking.
- Target coverage should stay at 80% or higher.

## 5. Security
- Never hardcode secrets, credentials, or API keys.
- Read sensitive values from environment variables.
- Validate all external input, especially email addresses and form fields.
- Avoid logging sensitive data.

## 6. Error Handling
- Fail fast with clear exceptions when inputs are invalid.
- Return user-friendly error messages in the web layer.
- Handle external service failures gracefully and do not expose internals to users.
- Prefer explicit error checks over silent failures.

## 7. Naming Conventions
- Use `snake_case` for functions, variables, and module names.
- Use `PascalCase` for class names.
- Use lowercase, hyphen-free names for templates and static asset files where possible.

## 8. Git Conventions
- Use conventional commits such as `feat:`, `fix:`, `docs:`, `test:`, and `refactor:`.
- Use branch names like `feature/*`, `bugfix/*`, or `docs/*`.
- Keep pull requests focused and include tests for behavior changes.

## 9. Skill Usage
- Use the `mailer-complete-testing` skill when designing or updating test suites.
- Use the `email-validation` skill when implementing or reviewing email validation logic.
