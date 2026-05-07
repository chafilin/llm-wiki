# Optimize Interaction to Next Paint

Source: https://web.dev/articles/optimize-inp

## Overview

INP is a stable Core Web Vital that evaluates how well pages respond to user interactions. Websites should aim for **INP of 200 milliseconds or less** at the 75th percentile.

## Understanding Interactions

An interaction consists of three measurable components:

1. **Input Delay**: Time from user action until event callbacks begin executing
2. **Processing Duration**: Time required for event callbacks to complete
3. **Presentation Delay**: Time until the browser presents the next frame

The sum of these three parts equals total interaction latency.

## Optimization Strategy

### 1. Identify Poor INP

**Field Data First**: Use Real User Monitoring (RUM) providers to capture:
- Specific interaction details
- Timing relative to page load
- Interaction type (click, keypress, tap)

**Supplement with CrUX**: Use PageSpeed Insights to review Chrome User Experience Report data.

**Lab Testing**: Once field data identifies issues, reproduce slow interactions using browser DevTools.

### 2. Reduce Input Delay

Input delay primarily stems from main thread blocking during:
- Script parsing, compilation, and evaluation
- Fetch handling
- Timer functions
- Overlapping interactions

**Script Evaluation During Startup**: Large scripts create long tasks that delay responsiveness.

### 3. Optimize Event Callbacks

**Break Up Work**: Use `setTimeout()` to split callback work into separate tasks:

```javascript
textBox.addEventListener('input', (inputEvent) => {
  // Critical: Update UI immediately for next frame
  updateTextBox(inputEvent);

  // Defer non-critical work
  requestAnimationFrame(() => {
    setTimeout(() => {
      const text = textBox.textContent;
      updateWordCount(text);
      checkSpelling(text);
      saveChanges(text);
    }, 0);
  });
});
```

**Yield Strategically**: Only defer work after visual updates, allowing rendering to occur sooner before background tasks execute.

**Avoid Layout Thrashing**: Do not update styles then immediately read layout values in the same task.

### 4. Minimize Presentation Delay

**Reduce DOM Size**: Large DOMs require more rendering work. Consider:
- Flattening DOM structure
- Adding elements during interactions rather than at load
- Using `content-visibility` CSS property for lazy rendering of off-screen content

**Client-Side Rendering Costs**: "When rendering HTML through JavaScript, the browser won't yield until parsing completes." Minimize client-rendered HTML volume during interactions.

## Key Principles

- Every interaction subpart contributes to latency — optimize all three components
- Each iframe maintains its own main thread
- Resource-constrained devices may experience cross-thread impacts
- INP optimization is iterative; fixing one slow interaction often reveals others
