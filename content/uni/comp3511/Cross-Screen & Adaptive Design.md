---
title: Cross-Screen & Adaptive Design
draft: false
tags:
  - ui
  - ux
  - design
---
## What is Cross-Screen Design?

It is imperative to design digital experiences that work seamlessly across multiple devices while maintaining usability, consistency, and task continuity. This involves supporting uses as they switch between devices.

The reason why it's needed is because users switch between devices, and inconsistent interfaces increase cognitive load. Additionally, a brand's trust depends on consistency. Poor adaptation interrupts tasks.

## Responsive vs Adaptive Layout

Frameworks like Bootstap employ a powerful 12-column grid system to structure and organise content. This is a responsive layout. [Here are examples](https://getbootstrap.com/docs/4.0/examples/)

### Responsive:
- Fluid grids
- Flexible images
- CSS breakpoints
- Continuous scaling

### Adaptive:
- Multiple fixed layouts
- Device-specific optimisation
- Context-aware logic

## Types of Adaptation

### Layout adaptation
Rearranging UI components. E.g. sidebar becomes bottom tab bar on mobile.
![[Screenshot 2026-07-11 at 10.50.05.png]]
### Content adaptation
Hiding or summarising information. E.g. Long article preview becomes a short summary card.
![[Screenshot 2026-07-11 at 10.49.57.png]]
### Interaction adaptation
Changing input methods. E.g. Hover tooltip on desktop becomes tap-to-reveal on mobile.
![[Screenshot 2026-07-11 at 10.49.47.png]]
### Functional adaptation
Adding or removing features. E.g. Advanced editing tools available only on desktop.
![[Screenshot 2026-07-11 at 10.49.39.png]]
### Contextual adaptation
Adjusting based on environment. E.g. Navigation app simplifies UI while driving.
![[Screenshot 2026-07-11 at 10.49.29.png]]

## Adaptation Strategies

### Represent density shifts
Adjust how much information is visible at once. E.g. 1-column layout on mobile --> 3-column layout on desktop![[Screenshot 2026-07-11 at 10.49.07.png]]

### Navigation restructuring
Change navigation pattern based on width. E.g. Hamburger menu (mobile) --> Horizontal top menu (desktop).
![[Screenshot 2026-07-11 at 10.51.21.png]]

### Hierarchy changes
Reorganise importance of elements when space increases. E.g. Sidebar filters appear on desktop but collapse on mobile![[Screenshot 2026-07-11 at 10.52.29.png]]

### Design around content, not device
Define breakpoints where layout breaks. E.g. when text becomes cramped at 720px, redesign the layout.

### Progressive Disclosure
Shows users only the information and controls they need at a given moment.

- __Mobile__: Show essentials --> Display only the core features needed for primary tasks to reduce clutter and cognitive load.
- __Desktop__: Reveal efficiency tools --> Provide advanced controls and shortcuts to support productivity and multitasking.

### Information Density

- __Small screens: Lower density__ --> Show fewer elements at once to improve readability and reduce cognitive overload.
- __Large screens: Parallel layouts__ --> Display multiple panels or information areas simultaneously to support multitasking.
- __Density must scale logically__ --> Increase information gradually while preserving hierarchy and clarity.

## Designing Web forms for Mobile Phones vs Desktop

Consider using progressive disclosure (a step-by-step signup flow). Allowing one primary action per screen. Use full-screen navigation menus with the minimum amount of menu levels.![[Screenshot 2026-07-11 at 11.06.47.png]]

## Adaptive Design and Consistency

### Visual Consistency
Maintaining the same colours, typography, icons, and layout style across screens to preserve brand identity and recognition.

#### Consistent colours
Use the same primary, secondary, and accent colours to maintain brand identity and visual recognition across devices.

#### Typography scale
Maintain a structured text hierarchy (heading, subheading, body) that scales proportionally across screen sizes.

#### Iconography
Use the same icon style and meaning to ensure users recognise actions regardless of device.

### Functional Consistency
Ensuring core features and tasks behave similarly across devices, even if the layout changes.

### Internal Constistency
Using the same design rules and patterns within the same application (e.g. buttons behave the same everywhere).

### External consistency
Aligning with platform conventions and standards (e.g. iOS navigation patterns, Android gestures).

## Development Strategies for Adaptive Design

### Reusable components
Predefined UI elements (buttons, cards, modals) reused across screens to ensure consistency and efficiency.

### Unified spacing
Standardised margin and padding rules that maintain visual rhythm across layouts.

### Consistent behaviour
Components respond the same way everywhere.

##### Useful sources: [Material Design Google](https://m3.material.io/), [Human Interface Guidelines Apple](https://developer.apple.com/design/human-interface-guidelines), [Fluent Design Microsoft](https://fluent2.microsoft.design/)

### State Consistency Across Devices
- Cloud sync --> User data is automatically synchronised across devices in real time.
- Saved progress --> Tasks can be paused and resumed on another device without restarting.
- Persistent session state --> User preferences, login status, and settings remain active across sessions and devices.

## Adaptive Design based on Screen Orientation

### Desktop and laptop users
The vast majority use screens in landscape orientation, while portrait mode is mainly used for specialised tasks such as coding or document review.

### Mobile users
About 94% use their smartphones in portrait mode, while only 6% use them in landscape.

- Portrait mode: Best suited for reading, scrolling, and vertically structured content.
- Landscape mode: Better suited for watching videos, gaming, and wide-format content.

#### Categories of Orientation Design

### FLUID
Some applications adjust themselves to the new orientation's size by simply changing the layout.

![[Screenshot 2026-07-11 at 11.22.25.png]]

### EXTENDED
This interface adjusts to the screen's size, adding or subtracting layout components according to the dimensions of the chosen orientation.![[Screenshot 2026-07-11 at 11.23.18.png]]

### COMPLEMENTARY
With this interface, a changed orientation triggers an auxiliary screen with relevant supplementary information

![[Screenshot 2026-07-11 at 11.25.37.png]]

### CONTINUOUS
A continuous design enables the user to access a secondary interface by a simple rotation of the device.![[Screenshot 2026-07-11 at 11.27.27.png]]

## Touch Screen Considerations

Place most important actions in "thumb zone"![[Screenshot 2026-07-11 at 11.29.16.png]]![[Screenshot 2026-07-11 at 11.29.23.png]]