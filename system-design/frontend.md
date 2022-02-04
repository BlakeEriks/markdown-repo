# Front-End System Design

## What to consider when designing a system

- Clear requirements & specifications
- Architecture
- Data Model Design
- API Design
- Multi-Device Support
- User Experience
- Performance
- Accessibility 
- i18n (internationalization)
- Security

## UI Components

Examples ➡️ Image carousel; selector which loads options over the network

### **Framework**

- Clear requirements + alignment
- Architecture
- Data model
- API design
- Deep dive
1. UX
2. Performance
3. Accessibility (a11y)
4. i18n
5. Multi-device support
6. Security

Considerations when scoping the system + making requirements:

- What devices should it support?
- What's the primary device that users will access the system on?
- What browsers should we support?
- Do we need to support internationalization?
- How much styling customization should we allow?

### **Architecture**

For frontend, this is focused on the client-side architecture, not on server systems.

For components, list the various sub components that will exist within, and indicate how the data will flow between the sub-components. Draw a diagram of the entities and their relationships.

### **Data model**

For components, data model refers to the component state. Factors to consider when deciding what goes into component state:

- State is allowed to change over time during lifecycle of the component, usually as a result of user interactions
- Each component has its own state such that multiple instances of the component can coexist on one page and not interfere. State should be independent for each component.
- Components are easier to understand the less state there is. The amount of state should be minimized. If a component uses a value which could be derived from another piece of state, then that info should likely not be a part of the state. IE length of list does not need to be stored independently of the list itself.
- Consolidate state to parent such that children are pure + stateless

### **API Design**

For components, api design refers to the options that can be passed to the component (props in React). Good api design results in clean and reusable components. 

- What are reasonable defaults? What properties are required?
- Follow open-closed principle; the component should be open for extension but closed for modification.
- Common configuration options, ex *click*, *blur*
- React is big on favoring composition over inheritance. 

```js
function FancyBorder(props) {
  return (
    <div className={'FancyBorder FancyBorder-' + props.color}>
      {props.children}
    </div>
  );
}

function WelcomeDialog() {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        Welcome
      </h1>
      <p className="Dialog-message">
        Thank you for visiting our spacecraft!
      </p>
    </FancyBorder>
  );
}
```

### **Dive Deep**

Choosing where to focus time here depends on the component and the desired functionality.

### UX Best Practices

- Reflect state of the component to the user. Spinners for background requests, display errors instead of failing silently.
- Display an empty state if the list is empty, instead of no content
- Irreversible destructive actions should have a confirmation step
- Disable interactive elements if they trigger an async request to prevent double firing
- For search inputs, each keystroke should not fire a network request
- Think about really long / short strings and how UI will look for either
- If there's many items to display, show a subset to prevent an excessively long or wide page.

### Performance

This usually refers to **loading speed**, **responsiveness**, and **memory space**.

**Loading Speed**

- Less javascript inside the component, the less the browser has to download to load it and the lower the network request time. It's important to modularize components and allow users to download only the necessary js modules needed for their use case

**Responsiveness**

- If a user action results in displaying of data that has to be loaded over the network, then there will be a delay between the interaction and the ui updating. Minimize that delay or remove it entirely to improve responsiveness
- JavaScript in a browser is single-threaded, meaning the browser can only execute one line of code at a time. The less work the component has to do when a user does something on the page, the faster the component can update the UI to respond to the changes.

**Memory Space**

- The more memory being used by a component, the slower the performance and more sluggish it will feel. Consider this when rendering lists in the scale of hundreds / thousands

### Optimization

- Render only what is displayed on the screen. Leverage windowing / virtualization to emulate a list with many elements, while only rendering the currently displayed items.
- Only load necessary data with lazy loading. Ex in a photo gallery component a user could have thousands of photos, but it's not feasible to load all of them eagerly. Load only the ones that the user is likely to view, or those that are within the viewport (this is called *above the fold*). 
- Preloading data ahead of time increases responsiveness by having data ready to be displayed to the user. Ex on a page of images, the next page is already being loaded while they are browsing the current page. 

### Accessibility (a11y)

This is the practice of making websites as usuable by as many people as possible. Considerations:

- Color contrasts (e.g. color blindness)
- Keyboard friendliness (e.g. people with limited fine motor control)
- Visual Impairment (e.g. blind)
- Transcripts for audio

Tips for achieving a11y

- High contrast between foreground and background
- Use correct HTMl tags for semanticness, or the correct aria-role attributes
- Clickable items should have tabindex attribute so that they are focusable, and cursor: pointer styling to indicate clickability.
- Images should have alt text to be read out by screen readers and act as a fallback if it fails to load.
- Aria-labels should be used to give context to elements which are not obvious to non-visual users. Ex an icon button without a text label should have an aria-label so that the intention is clear for thoe who cannot see the icon.

### Internationalization (i18n)

Internationalization is the design and development of a product, application or document content that enables easy localization for target audiences that vary in culture, region, or language. UI Components don't usually have to worry about internationalization unless under a few circumstances:

- Component uses hard-coded strings, like "prev"/"next" in a gallery navigation. The strings can be a prop with the english version as default
- Order of content matters; does the component support RTL (right to left) languages like arabic and hebrew?

### Mobile Device Support

When considering mobile support, one must consider the less powerful hardware available and smaller viewport. 

- It's important to not use too much memory, which decreases the device performance and increases power consumption.
- Increase the hit box of interactive elements - fingers have an easier time tapping on the right element.

### Security

Usually components aren't exposed to security vulnerabilities, but it can still happen.

Possible attacks include
- XSS (Cross site scripting), possible if user input is rendered using `dangerouslySetInnerHTML`
- CSRF (Cross-site request forgery)
- Clickjacking
- `rel=noopener`