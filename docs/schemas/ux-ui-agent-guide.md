# UX/UI Agent Schema Documentation

## Overview
The UX/UI Agent is responsible for creating comprehensive design systems, visual identities, and frontend component specifications. This agent leverages modern design tools and libraries to ensure consistent, accessible, and performant user interfaces.

## Key Features

### 1. **Tools and Libraries Integration**
The agent has built-in knowledge of popular UI libraries and frameworks:

#### Component Libraries
- **shadcn/ui**: Modern, customizable React components with Tailwind
- **Radix UI**: Unstyled, accessible component primitives
- **Material UI**: Complete enterprise design system
- **Ant Design**: Data-heavy enterprise applications
- **Chakra UI**: Modular and themeable components
- **Mantine**: Full-featured with built-in hooks
- **NextUI**: Beautiful modern components for Next.js

#### Styling Frameworks
- **Tailwind CSS**: Utility-first CSS framework
- **Styled Components**: CSS-in-JS with component scoping
- **Emotion**: Performance-focused CSS-in-JS
- **CSS Modules**: Local scope with standard CSS
- **Vanilla Extract**: Zero-runtime, type-safe styles

#### Documentation & Testing
- **Context7**: API documentation and patterns
- **Storybook**: Interactive component documentation
- **Docusaurus**: Markdown-based documentation

#### Accessibility Tools
- **axe DevTools**: Automated accessibility testing
- **WAVE**: Web accessibility evaluation
- **React Aria**: Accessible React hooks
- **Reach UI**: Accessible component library

### 2. **Brand Identity Creation**
- Logo design with multiple variations
- Comprehensive color palette (primary, secondary, semantic, neutral)
- Typography system with scale and line heights
- Spacing system for consistent layouts

### 3. **Theme Support**
Complete light and dark theme specifications:
- Background variations (default, paper, elevated)
- Text hierarchy (primary, secondary, disabled)
- Shadow system for depth
- Smooth theme transitions

### 4. **Component Specifications**
Each component includes:
- React code implementation
- Props documentation with TypeScript types
- Multiple variants for different use cases
- Accessibility features (ARIA labels, keyboard navigation)
- Storybook stories for testing
- Library references for best practices

### 5. **Layout Systems**
Pre-defined layouts for common patterns:
- Dashboard
- Forms
- Lists
- Detail views
- Landing pages
- Authentication
- Settings
- Wizards

### 6. **User Flows & Interactions**
- Step-by-step user journey mapping
- Alternative path considerations
- Success criteria definition
- Interaction patterns for navigation, forms, and feedback

### 7. **Implementation Guides**
- Tech stack recommendations
- Setup instructions
- Folder structure suggestions
- Code examples with dependencies
- Integration guides for external services

## Usage Example

```json
{
  "metadata": {
    "agent_type": "ux_ui_agent",
    "version": "1.0.0",
    "timestamp": "2025-09-07T03:00:00Z",
    "task_id": "UPT-14",
    "project_context": "Multi-Agent Research System"
  },
  "input": {
    "requirements": {
      "functional": [
        "User authentication",
        "Dashboard with analytics",
        "Responsive design"
      ],
      "accessibility": {
        "wcag_level": "AA",
        "screen_reader_support": true,
        "keyboard_navigation": true
      }
    },
    "user_persona": [{
      "name": "Developer",
      "tech_level": "advanced",
      "goals": ["Efficient workflow", "Clear documentation"],
      "devices": ["Desktop", "Laptop"]
    }],
    "technical_constraints": {
      "framework": "React",
      "browser_support": ["Chrome", "Firefox", "Safari", "Edge"]
    }
  }
}
```

## Output Structure

The agent will provide:

1. **Selected Tools**: Justified selection of libraries and frameworks
2. **Brand Identity**: Complete visual identity system
3. **Themes**: Light and dark theme specifications
4. **Components**: Fully specified UI components
5. **Layouts**: Page layout templates
6. **User Flows**: Interaction patterns and journeys
7. **Implementation Guide**: Technical setup and integration
8. **Validation Checklist**: Quality assurance criteria

## Integration with Other Agents

### From Research Agent
- User research insights
- Competitor analysis
- Market trends

### To Architect Agent
- Component specifications
- Performance requirements
- Technology stack recommendations

### To Development Agent
- Component code
- Styling system
- Implementation guides

### To Test Agent
- Accessibility criteria
- Performance benchmarks
- User flow test scenarios

## Best Practices

1. **Always consider accessibility first** - WCAG AA compliance minimum
2. **Design for mobile-first** - Progressive enhancement approach
3. **Use established patterns** - Leverage existing UI libraries
4. **Document everything** - Clear props, usage examples, and edge cases
5. **Test across devices** - Responsive design validation
6. **Optimize performance** - Bundle size and loading considerations
7. **Maintain consistency** - Use design tokens throughout

## Validation Criteria

The UX/UI Agent output should be validated against:

- [ ] Accessibility standards (WCAG)
- [ ] Performance metrics (Lighthouse)
- [ ] Responsive design breakpoints
- [ ] Browser compatibility
- [ ] User testing feedback
- [ ] Brand consistency
- [ ] Component reusability
- [ ] Documentation completeness

## Updates and Versioning

This schema follows semantic versioning:
- **Major**: Breaking changes to schema structure
- **Minor**: New features or properties added
- **Patch**: Bug fixes or documentation updates

Current Version: **1.0.0**

## Resources

- [shadcn/ui Documentation](https://ui.shadcn.com)
- [Radix UI Primitives](https://www.radix-ui.com)
- [Tailwind CSS](https://tailwindcss.com)
- [WCAG Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
- [Material Design 3](https://m3.material.io)
- [Storybook](https://storybook.js.org)
