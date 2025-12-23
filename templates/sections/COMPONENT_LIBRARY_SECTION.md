# Component Library Section Template

**Insert these sections into your CLAUDE.md when building reusable component/module libraries**

Use with: CLAUDE_MD_UNIVERSAL.md or CLAUDE_MD_TOKEN_OPTIMIZED.md
For: UI components, service catalogs, design systems, utility libraries

---

## 🚨 Critical Rules - Component Library Management

**Add to your Critical Rules section:**

### Never Modify Components in Consumer Projects

❌ **WRONG:** Modify component in website/consumer folder
✅ **CORRECT:** Customize via custom.css OR create library variant OR use wrapper

### Component Updates Follow Versioning

**Update workflow:**
1. Update in library source (not consumer)
2. Bump version (patch/minor/major)
3. Test in isolation
4. Update COMPONENT_REGISTRY.md
5. Deploy to consumers

### Customizations Use Custom CSS Only

**Consumers customize via:**
- ✅ Custom CSS/variables
- ✅ Wrapper components (rare)

**Never:**
- ❌ Modify component HTML
- ❌ Copy component into project
- ❌ Create parallel versions

---

## 🎨 Component Categories

**Add after Architecture section - customize for your project:**

### [Your Library Name] Components

**[Category 1]** - Brief description
Location: `/path/to/category/`

**[Category 2]** - Brief description
Location: `/path/to/category/`

**See:** `COMPONENT_REGISTRY.md` for searchable list

---

## 🔄 Development Workflow - Component Extraction

**Add to your workflow section:**

### Creating Components

1. **Build in context** - Create while building real project
2. **Test with real data** - Validate actual use case
3. **Extract to library** - Move with versioning
4. **Add to registry** - Update COMPONENT_REGISTRY.md
5. **Refactor** - Replace custom code with library version

### Updating Components

1. **Identify impact** - Which projects use this?
2. **Determine version** - Patch/minor/major?
3. **Update in library** - Never in consumer
4. **Bump version** - Follow semver
5. **Update registry** - Reflect changes
6. **Deploy** - Update consumers

### Extraction Checklist

```
☐ Works in isolation
☐ Clear props/API documented
☐ Follows naming conventions
☐ Versioned (start v1.0.0)
☐ Added to registry
☐ Original refactored
☐ README created
```

---

## 📊 Quick Reference

**File structure:**
```
/components/               # Library source
  /[category]/
    /[component-name]/
      index.html           # Implementation
      metadata.json        # Version, tags
      README.md           # Usage docs
/[consumers]/             # Projects using library
```

**Key files:**
- `.claude/documentation/COMPONENT_REGISTRY.md` - Quick lookup
- `.claude/documentation/Component_Library_System.md` - Architecture
- `VERSIONING_STRATEGY.md` - Version rules (optional)

---

## 💡 Usage Instructions

**When to use this template:**
- Building reusable component library
- Managing design system
- Service catalog or module library
- 15+ reusable abstractions

**How to use:**
1. Start with UNIVERSAL or TOKEN_OPTIMIZED template
2. Insert "Critical Rules - Component Library" into Critical Rules
3. Add "Component Categories" after Architecture
4. Add "Development Workflow" to workflow section
5. Customize categories for your library

**Token impact:** +150-200 lines, prevents costly mistakes, saves 60-70% on discovery

---

**Version:** 1.5.0
**Framework:** claude-brain-framework
**Type:** Section template (not standalone)
