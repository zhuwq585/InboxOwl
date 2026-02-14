# InboxOwl Project Structure

## Recommended Folder Structure for Spec & Test-Driven Development

```
InboxOwl/
│
├── docs/                           # All documentation and design specs
│   ├── architecture/              # System architecture documentation
│   │   ├── 00-overview.md        # High-level system overview
│   │   ├── 01-system-design.md   # Overall system architecture
│   │   ├── 02-data-flow.md       # Data flow diagrams and descriptions
│   │   ├── 03-tech-stack.md      # Technology choices and rationale
│   │   └── diagrams/             # Architecture diagrams (mermaid, draw.io, etc.)
│   │
│   ├── specs/                     # Component specifications
│   │   ├── components/           # Individual component specs
│   │   │   ├── email-parser.spec.md
│   │   │   ├── notification-service.spec.md
│   │   │   └── ...
│   │   ├── api/                  # API specifications
│   │   │   ├── rest-api.spec.md
│   │   │   └── openapi.yaml
│   │   └── database/             # Database schemas and specs
│   │       ├── schema.sql
│   │       └── migrations/
│   │
│   ├── design/                    # Detailed design documents
│   │   ├── component-designs/    # Per-component design docs
│   │   │   ├── email-parser-design.md
│   │   │   └── ...
│   │   └── decisions/            # Architecture Decision Records (ADRs)
│   │       ├── 001-database-choice.md
│   │       ├── 002-testing-framework.md
│   │       └── template.md
│   │
│   └── PROJECT_STRUCTURE.md      # This file
│
├── src/                           # Source code
│   ├── components/               # Main components/modules
│   │   ├── email-parser/
│   │   │   ├── index.ts
│   │   │   ├── parser.ts
│   │   │   └── types.ts
│   │   ├── notification-service/
│   │   │   └── ...
│   │   └── ...
│   │
│   ├── utils/                    # Shared utilities
│   │   ├── validation/
│   │   └── helpers/
│   │
│   ├── types/                    # Shared type definitions
│   │   └── index.ts
│   │
│   └── config/                   # Configuration files
│       ├── index.ts
│       └── constants.ts
│
├── tests/                         # Test files (mirrors src structure)
│   ├── unit/                     # Unit tests
│   │   ├── components/
│   │   │   ├── email-parser/
│   │   │   │   ├── parser.test.ts
│   │   │   │   └── ...
│   │   │   └── ...
│   │   └── utils/
│   │
│   ├── integration/              # Integration tests
│   │   ├── api/
│   │   └── services/
│   │
│   ├── e2e/                      # End-to-end tests
│   │   └── workflows/
│   │
│   ├── fixtures/                 # Test data and fixtures
│   │   ├── sample-emails/
│   │   └── mock-data/
│   │
│   └── helpers/                  # Test utilities
│       ├── setup.ts
│       └── mocks.ts
│
├── scripts/                       # Build, deploy, and utility scripts
│   ├── generate-tests.sh
│   ├── validate-specs.sh
│   └── ...
│
├── .github/                      # GitHub specific files
│   ├── workflows/                # CI/CD workflows
│   └── ISSUE_TEMPLATE/
│
├── config/                       # Project configuration files
│   ├── jest.config.js           # Test configuration
│   ├── tsconfig.json            # TypeScript config
│   └── ...
│
├── CLAUDE.md                     # AI assistant guidelines
├── README.md                     # Project README
├── LICENSE                       # MIT License
├── package.json                  # Dependencies (if Node.js)
└── .gitignore                    # Git ignore rules

```

## Development Workflow

**IMPORTANT:** Architecture is a PROJECT-LEVEL activity done ONCE. Component development follows a 5-phase workflow repeated for EACH component.

### Phase 0: System Architecture (PROJECT-LEVEL - Done Once)

**Complete this BEFORE starting any component work:**

1. Create system architecture in `docs/architecture/`
   - `00-overview.md` - High-level system overview
   - `01-system-design.md` - Overall system architecture
   - `02-data-flow.md` - Data flow diagrams
   - `03-tech-stack.md` - Technology choices
   - Define all component boundaries and interfaces
   - Identify all components that need to be built

2. Document key architecture decisions in `docs/design/decisions/` as ADRs
   - Database choice
   - Framework/language selection
   - Architectural patterns
   - Major design trade-offs

3. Review and approve architecture

**Output:** Complete list of components to implement

**This answers:** What components exist? How do they interact? What are the component boundaries?

---

### Per-Component Workflow (Repeat for Each Component)

Once architecture is complete and components are identified, follow this 5-phase workflow for EACH component:

#### Phase 1: Component Specification
1. Create spec in `docs/specs/components/[component-name].spec.md`
2. Use template: `docs/templates/component-spec-template.md`
3. Spec should include:
   - Purpose and responsibilities
   - Input/output contracts (public API)
   - Dependencies
   - Error handling requirements
   - Performance requirements
   - Test requirements

#### Phase 2: Component Design
1. Create design doc in `docs/design/component-designs/[component-name]-design.md`
2. Use template: `docs/templates/component-design-template.md`
3. Include:
   - Class/module structure
   - Function signatures (internal + public)
   - Data structures
   - Algorithm choices
   - Implementation approach

#### Phase 3: Test Generation
1. Create test file in `tests/unit/` matching the component path
2. Write test cases based on spec requirements
3. Tests should be runnable but fail (red state)
4. Verify test coverage of all spec requirements

#### Phase 4: Implementation
1. Create source file in `src/` matching the component path
2. Implement to make tests pass (green state)
3. Refactor as needed while keeping tests green
4. Code review

#### Phase 5: Integration
1. Create integration tests in `tests/integration/`
2. Verify components work together
3. Update `docs/TRACEABILITY.md`
4. Update documentation as needed

## Document Templates

### Component Spec Template
```markdown
# Component: [Name]

## Purpose
Brief description of what this component does

## Responsibilities
- Responsibility 1
- Responsibility 2

## Interface
### Inputs
- Parameter 1: type, description
- Parameter 2: type, description

### Outputs
- Return value: type, description

### Errors
- Error condition 1
- Error condition 2

## Dependencies
- Dependency 1
- Dependency 2

## Test Requirements
- Test case 1
- Test case 2

## Performance Requirements
- Requirement 1
- Requirement 2
```

### ADR Template
```markdown
# ADR-XXX: [Title]

## Status
[Proposed | Accepted | Deprecated | Superseded]

## Context
What is the issue that we're seeing that is motivating this decision?

## Decision
What is the change that we're proposing and/or doing?

## Consequences
What becomes easier or more difficult to do because of this change?

## Alternatives Considered
- Alternative 1: pros and cons
- Alternative 2: pros and cons
```

## Traceability Matrix

Maintain a traceability document that links:
- Spec → Design → Tests → Implementation

Example in `docs/TRACEABILITY.md`:
```markdown
| Component | Spec | Design | Tests | Implementation | Status |
|-----------|------|--------|-------|----------------|--------|
| EmailParser | docs/specs/components/email-parser.spec.md | docs/design/component-designs/email-parser-design.md | tests/unit/components/email-parser/ | src/components/email-parser/ | ✅ Complete |
```

## Naming Conventions

### Documentation Files
- Specs: `[component-name].spec.md`
- Design: `[component-name]-design.md`
- ADRs: `NNN-short-title.md` (e.g., `001-database-choice.md`)

### Test Files
- Unit tests: `[file-name].test.[ext]` (e.g., `parser.test.ts`)
- Integration tests: `[feature-name].integration.test.[ext]`
- E2E tests: `[workflow-name].e2e.test.[ext]`

### Source Files
- Follow language-specific conventions
- Use clear, descriptive names
- Match test file names (minus `.test`)

## Benefits of This Structure

1. **Clear Separation**: Docs, specs, tests, and code are clearly separated
2. **Traceability**: Easy to trace from spec → design → test → implementation
3. **Scalability**: Structure supports growth without reorganization
4. **Standard Pattern**: Tests mirror source structure for easy navigation
5. **Documentation-First**: Encourages thinking before coding
6. **Review-Friendly**: Easy for reviewers to find related documents
7. **Tooling-Friendly**: Standard structure works well with IDEs and test runners

## Recommended Tools

- **Documentation**: Markdown files (easy to version control)
- **Diagrams**: Mermaid (text-based, works in GitHub) or Draw.io
- **API Specs**: OpenAPI/Swagger for REST APIs
- **Test Coverage**: Track coverage reports in `tests/coverage/`
- **Traceability**: Consider tools like Sphinx, MkDocs, or custom scripts

## Next Steps

1. Review and approve this structure
2. Create initial folder structure
3. Add templates to `docs/templates/`
4. Start with system architecture documents
5. Define first component spec
6. Generate first unit test
7. Implement first component

---

*Last Updated: 2026-02-04*
