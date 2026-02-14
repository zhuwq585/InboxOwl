# CLAUDE.md

This file provides context and guidelines for AI assistants working with the InboxOwl codebase.

## Project Overview

**Project Name:** InboxOwl
**License:** MIT
**Owner:** zhuwq585

InboxOwl is [TODO: Add project description - what does InboxOwl do?]

## Development Methodology

**InboxOwl follows a Specification and Test-Driven Development (Spec+TDD) approach:**

1. **Architecture First** - Design system architecture before components
2. **Specification Driven** - Write detailed specs before design
3. **Design Before Code** - Create detailed designs before implementation
4. **Test First** - Generate unit tests before writing logic
5. **Implement Last** - Write code to make tests pass

See `docs/PROJECT_STRUCTURE.md` for detailed workflow and structure.

## Project Structure

```
InboxOwl/
├── docs/                      # All documentation and design specs
│   ├── architecture/         # System architecture documentation
│   ├── specs/               # Component specifications
│   │   ├── components/      # Individual component specs
│   │   ├── api/            # API specifications
│   │   └── database/       # Database schemas
│   ├── design/             # Detailed design documents
│   │   ├── component-designs/  # Per-component designs
│   │   └── decisions/      # Architecture Decision Records (ADRs)
│   ├── templates/          # Document templates
│   ├── PROJECT_STRUCTURE.md  # Detailed structure guide
│   └── TRACEABILITY.md     # Spec-Design-Test-Code tracking
│
├── src/                    # Source code
│   ├── components/        # Main components/modules
│   ├── utils/            # Shared utilities
│   ├── types/            # Shared type definitions
│   └── config/           # Configuration
│
├── tests/                 # Test files (mirrors src structure)
│   ├── unit/            # Unit tests
│   ├── integration/     # Integration tests
│   ├── e2e/            # End-to-end tests
│   ├── fixtures/       # Test data
│   └── helpers/        # Test utilities
│
├── scripts/              # Build and utility scripts
├── config/              # Project configuration
├── CLAUDE.md            # This file
├── README.md            # Project README
└── LICENSE              # MIT License
```

**Important Files:**
- `docs/PROJECT_STRUCTURE.md` - Complete structure and workflow guide
- `docs/TRACEABILITY.md` - Component development tracking
- `docs/templates/` - Templates for specs, designs, and ADRs

## Development Guidelines

### Spec+TDD Workflow

**CRITICAL: Architecture is done ONCE at project level, then each component follows a 5-phase workflow.**

#### Phase 0: System Architecture (PROJECT-LEVEL - Done Once)

**Do this FIRST before any component work:**

- Create system design in `docs/architecture/`
  - Overall system architecture
  - Component identification and boundaries
  - Component interfaces and interactions
  - Data flow diagrams
- Document key decisions as ADRs in `docs/design/decisions/`
  - Technology choices (database, framework, language, etc.)
  - Architectural patterns
  - Major design trade-offs
- Review and approve architecture
- **Output:** List of components to build

**This phase answers:** What components exist? How do they interact? What technologies do we use?

#### Per-Component Workflow (Repeat for each component)

**Once architecture identifies components, follow this 5-phase workflow for EACH component:**

1. **Specification Phase**
   - Use template: `docs/templates/component-spec-template.md`
   - Create spec in `docs/specs/components/[component-name].spec.md`
   - Define interfaces, behavior, and test requirements
   - Get spec reviewed and approved

2. **Design Phase**
   - Use template: `docs/templates/component-design-template.md`
   - Create design in `docs/design/component-designs/[component-name]-design.md`
   - Detail implementation approach, algorithms, data structures
   - Get design reviewed and approved

3. **Test Generation Phase**
   - Create test file in `tests/unit/` (mirror src structure)
   - Write test cases based on spec requirements
   - Tests should fail initially (Red state)
   - Review test coverage

4. **Implementation Phase**
   - Create source file in `src/` (mirror test structure)
   - Implement to make tests pass (Green state)
   - Refactor while keeping tests green
   - Code review

5. **Integration Phase**
   - Create integration tests in `tests/integration/`
   - Verify components work together
   - Update `docs/TRACEABILITY.md`

**Never skip steps. Never implement before writing tests.**

### Code Style & Conventions

- [TODO: Add language-specific style guides]
- [TODO: Add naming conventions]
- [TODO: Add formatting rules]

### Git Workflow

- **Main Branch:** [TODO: Specify main branch name - main/master]
- **Feature Branches:** Use descriptive names (e.g., `feature/user-authentication`, `fix/email-parsing`)
- **Commit Messages:** Use clear, descriptive commit messages in present tense
  - Good: "Add email validation function"
  - Avoid: "fixed stuff", "wip"

### Testing

- **Framework:** [TODO: Add testing framework - Jest, pytest, etc.]
- **Coverage Requirement:** Minimum [TODO]% unit test coverage
- **Test Location:** Tests mirror `src/` structure in `tests/unit/`
- **Naming:** `[component-name].test.[ext]`
- **Commands:**
  ```bash
  # [TODO: Add test commands]
  ```

### Dependencies & Environment

- [TODO: Add required dependencies]
- [TODO: Add environment setup instructions]
- [TODO: Add required environment variables]

## Architecture

[TODO: Describe the high-level architecture of InboxOwl]

### Key Components

- [TODO: List and describe main components/modules]

### Data Flow

- [TODO: Describe how data flows through the system]

## Common Tasks

### Setup Development Environment

```bash
# [TODO: Add setup commands]
```

### Running the Application

```bash
# [TODO: Add run commands]
```

### Running Tests

```bash
# [TODO: Add test commands]
```

### Building for Production

```bash
# [TODO: Add build commands]
```

## Important Considerations

### Security

- Never commit sensitive data (API keys, passwords, tokens)
- [TODO: Add project-specific security guidelines]

### Performance

- [TODO: Add performance considerations]

### Error Handling

- [TODO: Add error handling patterns]

## External Resources

- Repository: https://github.com/zhuwq585/InboxOwl
- [TODO: Add documentation links]
- [TODO: Add relevant external resources]

## AI Assistant Notes

### CRITICAL RULES for AI Assistants

**This project uses Spec+TDD. You MUST follow this workflow:**

1. **NEVER write implementation code before:**
   - Writing the specification
   - Creating the design document
   - Writing unit tests that fail

2. **For new components, ALWAYS:**
   - Verify system architecture is complete in `docs/architecture/`
   - Check `docs/TRACEABILITY.md` for existing work
   - Use templates from `docs/templates/`
   - Follow the 5-phase per-component workflow (Spec → Design → Test → Impl → Integration)
   - Update traceability matrix after each phase

3. **For new projects (no architecture yet):**
   - Start with Phase 0: System Architecture (project-level)
   - Identify all components before starting any component work
   - Document architecture decisions as ADRs

4. **For changes to existing components:**
   - Read the spec first (`docs/specs/`)
   - Check the design (`docs/design/`)
   - Update tests before updating implementation
   - Update documentation to match changes

5. **Quality Gates:**
   - ✅ Spec reviewed before design
   - ✅ Design reviewed before tests
   - ✅ Tests written (and failing) before implementation
   - ✅ All tests passing before PR
   - ✅ Documentation updated

### When Working on InboxOwl

1. **Always read existing docs** before making changes
2. **Follow the Spec+TDD workflow** - no exceptions
3. **Keep solutions simple** - avoid over-engineering
4. **Update traceability** - keep `docs/TRACEABILITY.md` current
5. **Use templates** - they ensure consistency

### Current Project Status

This is an early-stage project following strict Spec+TDD methodology. When making contributions:

- **Ask first** before implementing major features
- **Propose architecture** using ADR template
- **Start with specs** not with code
- **Document everything** as you build
- **Track all work** in traceability matrix

---

*Last Updated: 2026-02-04*
*This file should be updated as the project evolves to reflect current practices and architecture.*
