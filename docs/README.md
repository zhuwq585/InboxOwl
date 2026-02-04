# InboxOwl Documentation

Welcome to the InboxOwl documentation directory. This folder contains all specifications, designs, and architectural documentation for the project.

## Quick Start

### For New Contributors

1. **Read first:**
   - `/CLAUDE.md` - Project guidelines and AI assistant instructions
   - `/docs/PROJECT_STRUCTURE.md` - Detailed structure and workflow guide
   - `/docs/architecture/` - System architecture documents

2. **Starting a new component:**
   - Copy template from `docs/templates/component-spec-template.md`
   - Follow the Spec+TDD workflow (see below)
   - Update `docs/TRACEABILITY.md` as you progress

3. **Making changes to existing components:**
   - Read the spec in `docs/specs/components/`
   - Review the design in `docs/design/component-designs/`
   - Follow the update workflow (see below)

## Spec+TDD Workflow

```
┌─────────────┐
│ Architecture│ → System design, ADRs
└──────┬──────┘
       ↓
┌─────────────┐
│    Spec     │ → Component specification
└──────┬──────┘
       ↓
┌─────────────┐
│   Design    │ → Detailed design document
└──────┬──────┘
       ↓
┌─────────────┐
│    Tests    │ → Unit tests (failing/red)
└──────┬──────┘
       ↓
┌─────────────┐
│Implementation│ → Code to pass tests (green)
└──────┬──────┘
       ↓
┌─────────────┐
│ Integration │ → Integration tests, docs
└─────────────┘
```

## Directory Structure

```
docs/
├── README.md                    # This file
├── PROJECT_STRUCTURE.md         # Complete project structure guide
├── TRACEABILITY.md              # Component tracking matrix
│
├── architecture/                # System Architecture
│   ├── 00-overview.md          # System overview
│   ├── 01-system-design.md     # Architecture design
│   ├── 02-data-flow.md         # Data flow documentation
│   ├── 03-tech-stack.md        # Technology choices
│   └── diagrams/               # Architecture diagrams
│
├── specs/                       # Specifications
│   ├── components/             # Component specifications
│   ├── api/                    # API specifications
│   └── database/               # Database schemas
│
├── design/                      # Detailed Designs
│   ├── component-designs/      # Component design documents
│   └── decisions/              # Architecture Decision Records
│       └── template.md         # ADR template
│
└── templates/                   # Document Templates
    ├── component-spec-template.md
    ├── component-design-template.md
    └── adr-template.md
```

## Document Types

### Architecture Documents
**Location:** `docs/architecture/`
**Purpose:** High-level system design and architectural decisions

**When to create:**
- Starting the project
- Major architectural changes
- Adding new subsystems

### Specifications
**Location:** `docs/specs/components/`
**Template:** `docs/templates/component-spec-template.md`
**Purpose:** Define what a component should do (interface, behavior, requirements)

**When to create:**
- Before implementing any new component
- Before making significant changes to existing components

### Design Documents
**Location:** `docs/design/component-designs/`
**Template:** `docs/templates/component-design-template.md`
**Purpose:** Define how a component will be implemented (classes, algorithms, data structures)

**When to create:**
- After spec is approved
- Before writing tests

### Architecture Decision Records (ADRs)
**Location:** `docs/design/decisions/`
**Template:** `docs/templates/adr-template.md`
**Purpose:** Document important architectural decisions and their rationale

**When to create:**
- Choosing technologies
- Major design patterns
- Significant trade-offs

## Document Workflow

### Creating a New Component

1. **Check traceability matrix** (`docs/TRACEABILITY.md`)
   - Ensure component doesn't already exist
   - Add entry with "⏳ Pending" status

2. **Write specification**
   - Copy `docs/templates/component-spec-template.md`
   - Save to `docs/specs/components/[component-name].spec.md`
   - Fill in all sections
   - Get reviewed and approved

3. **Write design document**
   - Copy `docs/templates/component-design-template.md`
   - Save to `docs/design/component-designs/[component-name]-design.md`
   - Fill in all sections
   - Get reviewed and approved

4. **Generate tests** (see `/tests/`)
   - Write unit tests based on spec
   - Tests should fail (red state)

5. **Implement component** (see `/src/`)
   - Write code to pass tests
   - Refactor to green state

6. **Update traceability**
   - Mark component as "✅ Complete"
   - Update test coverage metrics
   - Add any follow-up items

### Updating an Existing Component

1. **Read existing docs**
   - Spec: `docs/specs/components/[component-name].spec.md`
   - Design: `docs/design/component-designs/[component-name]-design.md`

2. **Update specification** if needed
   - Document what changes
   - Update version number
   - Get reviewed

3. **Update design** if needed
   - Document how changes
   - Update version number
   - Get reviewed

4. **Update tests first**
   - Add/modify tests for new behavior
   - Ensure tests fail for new features

5. **Update implementation**
   - Make tests pass
   - Refactor as needed

6. **Update traceability**
   - Note changes in `docs/TRACEABILITY.md`
   - Update "Last Modified" dates

## Best Practices

### Writing Specifications
- ✅ Be clear and unambiguous
- ✅ Define all inputs and outputs
- ✅ Specify error conditions
- ✅ Include performance requirements
- ✅ List test requirements
- ❌ Don't include implementation details (that's for design docs)

### Writing Design Documents
- ✅ Explain the "how" not the "what"
- ✅ Include algorithms and data structures
- ✅ Justify design decisions
- ✅ Consider performance implications
- ✅ Document dependencies
- ❌ Don't duplicate spec content

### Writing ADRs
- ✅ Document the context clearly
- ✅ Explain alternatives considered
- ✅ Be honest about trade-offs
- ✅ Update status as decisions evolve
- ✅ Link to related ADRs
- ❌ Don't be overly verbose

## Naming Conventions

### Files
- **Specs:** `[component-name].spec.md`
- **Designs:** `[component-name]-design.md`
- **ADRs:** `NNN-short-title.md` (e.g., `001-database-choice.md`)

### Components
- Use kebab-case for file names
- Use PascalCase for class names (if applicable)
- Be descriptive but concise

## Tools and Automation

### Document Generation
```bash
# [TODO: Add scripts for document generation]
```

### Validation
```bash
# [TODO: Add scripts to validate docs match implementation]
```

### Diagram Tools
- **Mermaid:** Text-based diagrams (works in GitHub)
- **Draw.io:** Visual diagrams
- **PlantUML:** UML diagrams

## Maintenance

### Regular Updates
- Review traceability matrix weekly
- Update architecture docs when system evolves
- Keep ADRs current (mark as deprecated when superseded)
- Archive old versions in git history (don't delete)

### Documentation Debt
Track documentation that needs updating:
- [ ] TODO item 1
- [ ] TODO item 2

## Questions?

- Check `CLAUDE.md` for project guidelines
- Review `PROJECT_STRUCTURE.md` for detailed structure
- See templates in `docs/templates/`
- Refer to `TRACEABILITY.md` for component status

---

*Last Updated: 2026-02-04*
*This README should be updated as documentation practices evolve.*
