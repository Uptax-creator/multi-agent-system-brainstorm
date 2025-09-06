# Contributing to Multi-Agent System Brainstorm

## Welcome!

We're excited that you're interested in contributing to the Multi-Agent System project!

## How to Contribute

### 1. Fork the Repository

1. Click the "Fork" button on GitHub
2. Clone your fork locally:
```bash
git clone https://github.com/YOUR-USERNAME/multi-agent-system-brainstorm.git
cd multi-agent-system-brainstorm
```

### 2. Create a Branch

```bash
git checkout -b feature/your-feature-name
```

### 3. Make Your Changes

- Follow the existing code structure
- Update documentation as needed
- Add tests for new features
- Validate JSON schemas

### 4. Test Your Changes

```bash
npm test
npm run validate
```

### 5. Commit Your Changes

```bash
git add .
git commit -m "feat: describe your changes"
```

Commit message format:
- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation changes
- `test:` Test additions/changes
- `refactor:` Code refactoring

### 6. Push and Create Pull Request

```bash
git push origin feature/your-feature-name
```

Then create a Pull Request on GitHub.

## Development Guidelines

### JSON Schemas

- Always validate schemas before committing
- Use semantic versioning for schema changes
- Document all properties clearly
- Include examples for complex schemas

### Agent Prompts

- Keep prompts clear and specific
- Include input/output examples
- Test prompts thoroughly
- Version control all changes

### n8n Workflows

- Export workflows in JSON format
- Remove sensitive credentials
- Document node configurations
- Test workflows in isolation

## Code Style

- Use consistent formatting
- Follow ESLint rules
- Comment complex logic
- Keep functions small and focused

## Testing

- Write unit tests for new features
- Ensure all tests pass
- Maintain >80% code coverage
- Test edge cases

## Documentation

- Update README for new features
- Document API changes
- Include usage examples
- Keep schemas documentation current

## Questions?

Open an issue on GitHub or contact the maintainers.

Thank you for contributing! 🚀