# Quick Start Guide - InboxOwl Spec+TDD Workflow

## 🎯 Overview

InboxOwl uses **Specification and Test-Driven Development (Spec+TDD)**. This means:
- Write specs before design
- Write design before tests
- Write tests before code
- **Never skip steps!**

## 📋 The 6-Phase Workflow

```
1. Architecture → 2. Spec → 3. Design → 4. Tests → 5. Code → 6. Integration
```

## 🚀 Starting Your First Component

### Step 1: Architecture (if needed)
**When:** Starting project or adding major subsystems

```bash
# Create system design documents
cd docs/architecture/
# Edit 00-overview.md, 01-system-design.md, etc.
```

**Create an ADR if making architectural decisions:**
```bash
cp docs/templates/adr-template.md docs/design/decisions/001-your-decision.md
# Fill in the ADR
```

### Step 2: Write Specification
**When:** Before every new component

```bash
# Copy the spec template
cp docs/templates/component-spec-template.md \
   docs/specs/components/your-component.spec.md

# Fill in:
# - Purpose and responsibilities
# - Interface (inputs/outputs)
# - Behavior specifications
# - Error handling
# - Test requirements
# - Performance requirements
```

**Template sections:**
- ✅ Purpose
- ✅ Responsibilities
- ✅ Interface (function signatures)
- ✅ Dependencies
- ✅ Error handling
- ✅ Test requirements
- ✅ Performance requirements

**Review checklist:**
- [ ] All inputs and outputs defined?
- [ ] Error conditions specified?
- [ ] Test requirements listed?
- [ ] Dependencies identified?

### Step 3: Write Design
**When:** After spec is approved

```bash
# Copy the design template
cp docs/templates/component-design-template.md \
   docs/design/component-designs/your-component-design.md

# Fill in:
# - Module structure
# - Classes/functions
# - Algorithms
# - Data flow
# - Implementation approach
```

**Template sections:**
- ✅ Module structure
- ✅ Classes/functions with signatures
- ✅ Algorithms (with complexity analysis)
- ✅ Data flow diagrams
- ✅ Error handling strategy
- ✅ Testing strategy

**Review checklist:**
- [ ] Design satisfies spec requirements?
- [ ] Algorithms chosen and justified?
- [ ] Data structures defined?
- [ ] Error handling planned?

### Step 4: Generate Tests
**When:** After design is approved, before implementation

```bash
# Create test file (mirrors src structure)
# If component will be: src/components/email-parser/parser.ts
# Create test at: tests/unit/components/email-parser/parser.test.ts

# Write test cases based on spec requirements
# Tests should FAIL initially (red state)
```

**Test checklist:**
- [ ] Test for each function in spec?
- [ ] Test happy paths?
- [ ] Test error conditions?
- [ ] Test edge cases?
- [ ] All tests currently failing? (red state)

**Run tests:**
```bash
# [TODO: Add test command, e.g., npm test, pytest, etc.]
# Expect: All tests FAIL (red state) ❌
```

### Step 5: Implement Component
**When:** After tests are written and failing

```bash
# Create source file (mirrors test structure)
# If test is: tests/unit/components/email-parser/parser.test.ts
# Create at: src/components/email-parser/parser.ts

# Implement to make tests pass
# Refactor while keeping tests green
```

**Implementation checklist:**
- [ ] All tests now passing? (green state)
- [ ] Code follows design document?
- [ ] Error handling implemented?
- [ ] No over-engineering?
- [ ] Code is readable?

**Run tests:**
```bash
# [TODO: Add test command]
# Expect: All tests PASS (green state) ✅
```

### Step 6: Integration
**When:** After component implementation is complete

```bash
# Create integration tests
cd tests/integration/
# Write tests that verify components work together

# Update documentation
cd docs/
# Update TRACEABILITY.md
# Mark component as complete ✅
```

**Integration checklist:**
- [ ] Integration tests written?
- [ ] Integration tests passing?
- [ ] Traceability matrix updated?
- [ ] Component status marked complete?

## 📊 Tracking Your Progress

**Update the traceability matrix after each phase:**

```bash
# Edit docs/TRACEABILITY.md
# Update component status:
# ❌ Not Started → ⏳ Pending → 🟡 In Progress → ✅ Complete
```

## 🎓 Example Walkthrough

Let's say you want to create an "Email Parser" component:

### Phase 1: Spec
```bash
cp docs/templates/component-spec-template.md \
   docs/specs/components/email-parser.spec.md
```

Fill in:
```markdown
# Component: Email Parser

## Purpose
Parse raw email strings into structured data

## Interface
parseEmail(rawEmail: string): ParsedEmail
- Input: Raw email string
- Output: ParsedEmail object
- Throws: ParseError if invalid format
```

### Phase 2: Design
```bash
cp docs/templates/component-design-template.md \
   docs/design/component-designs/email-parser-design.md
```

Fill in:
```markdown
# Component Design: Email Parser

## Classes
class EmailParser {
  parse(raw: string): ParsedEmail
  validateFormat(raw: string): boolean
  extractHeaders(raw: string): Headers
  extractBody(raw: string): Body
}
```

### Phase 3: Tests
```bash
# Create: tests/unit/components/email-parser/parser.test.ts
```

```typescript
describe('EmailParser', () => {
  it('should parse valid email', () => {
    const result = parser.parse(validEmail);
    expect(result.subject).toBe('Test');
  });

  it('should throw on invalid format', () => {
    expect(() => parser.parse(invalid)).toThrow(ParseError);
  });
});
```

Run: **Expect FAIL ❌**

### Phase 4: Implement
```bash
# Create: src/components/email-parser/parser.ts
```

```typescript
export class EmailParser {
  parse(raw: string): ParsedEmail {
    // Implementation here
  }
}
```

Run: **Expect PASS ✅**

### Phase 5: Update Tracking
```bash
# Edit: docs/TRACEABILITY.md
# Change status to: ✅ Complete
```

## 🔍 Common Mistakes to Avoid

❌ **DON'T:**
- Skip writing specs
- Start coding before tests
- Skip the design phase
- Forget to update traceability

✅ **DO:**
- Follow all 6 phases in order
- Write tests that fail first
- Keep documentation updated
- Review each phase before proceeding

## 📚 Key Documents

| Document | Purpose | When to Use |
|----------|---------|-------------|
| `CLAUDE.md` | Project guidelines | Read first! |
| `docs/PROJECT_STRUCTURE.md` | Detailed structure | Planning phase |
| `docs/TRACEABILITY.md` | Track progress | Throughout development |
| `docs/README.md` | Documentation guide | Writing docs |
| `docs/templates/*.md` | Document templates | Creating new docs |

## 🎯 Decision Tree

```
Need to add functionality?
│
├─ Is it a new component?
│  ├─ YES → Follow full 6-phase workflow
│  └─ NO → Is it a significant change?
│     ├─ YES → Update spec, design, tests, then code
│     └─ NO → Update tests, then code
│
└─ Is it an architectural decision?
   └─ YES → Create ADR first
```

## 🆘 Getting Help

- **Spec questions:** Review `docs/templates/component-spec-template.md`
- **Design questions:** Review `docs/templates/component-design-template.md`
- **Architecture decisions:** Review `docs/templates/adr-template.md`
- **Process questions:** Review `docs/PROJECT_STRUCTURE.md`
- **Progress tracking:** Check `docs/TRACEABILITY.md`

## ✅ Final Checklist

Before considering a component "done":

- [ ] Spec written and reviewed
- [ ] Design document written and reviewed
- [ ] Unit tests written and passing
- [ ] Integration tests written and passing
- [ ] Code reviewed
- [ ] Documentation updated
- [ ] Traceability matrix updated
- [ ] All quality gates passed

---

**Remember:** The goal of Spec+TDD is quality, not speed. Take time to think through each phase. It's faster to do it right the first time than to refactor later!

*Last Updated: 2026-02-04*
