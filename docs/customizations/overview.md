# Customization Overview

INGenious Playwright Studio provides two primary ways to extend and customize the framework to meet your specific testing needs:

## 1. Engine Customization

Engine customization offers **full flexibility** by allowing direct access to the INGenious Engine source code. You can:

- Create new actions using existing or new libraries
- Modify existing action implementations
- Add custom functions and utilities
- Leverage the full power of Java and the underlying frameworks

!!! warning "Important Notice"
    **Engine access will be restricted in future releases.** While engine customization currently provides maximum flexibility, this approach is being phased out in favor of the plugin architecture to maintain framework stability and upgrade compatibility.

[Learn more about Engine Customization](index.md){ .md-button }

---

## 2. INGenious Plugins

**INGenious Plugins are the recommended approach** for extending the framework. Plugins provide:

- A structured, maintainable way to add custom functionality
- Better compatibility across framework versions
- Easier distribution and sharing of customizations
- Isolated dependencies that don't conflict with the core framework

!!! info "Current Status"
    While plugins are the recommended path forward, the plugin API currently has **limited capabilities** compared to full engine access. The development team is actively working to expand plugin functionality and capabilities.

!!! tip "Active Development"
    Plugin development is being **continued and enhanced**. Future releases will expand the plugin API to support more use cases and provide greater flexibility.

[Explore INGenious Plugins](../plugins/plugins.md){ .md-button }
[Plugin API Reference](../plugins/pluginApi.md){ .md-button }

---

## Choosing Your Approach

| Aspect | Engine Customization | INGenious Plugins |
|--------|---------------------|-------------------|
| **Flexibility** | Maximum | Limited (expanding) |
| **Future Support** | Being phased out | Recommended |
| **Maintenance** | Higher effort | Lower effort |
| **Upgrade Path** | May break with updates | Version-compatible |
| **Distribution** | Complex | Simplified |

### Recommendations

- **For new customizations**: Use plugins whenever possibles
- **For existing customizations**: Begin evaluating plugin migration paths

---

## Getting Started

Choose the path that best fits your current needs:

<div class="grid cards" markdown>

- :material-engine: **Engine Customization**  
  Full access to modify framework internals  
  [Get Started →](index.md)

- :material-puzzle: **INGenious Plugins**  
  Recommended, structured extensions  
  [Get Started →](../plugins/plugins.md)

</div>
