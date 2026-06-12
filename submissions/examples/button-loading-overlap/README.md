## Bug: Button Text Overlaps with Loading Spinner on Click State

### Describe the Bug
When the `.ease-btn-loading` class is dynamically appended to a button, the CSS pseudo-element (`::after`) correctly renders the loading spinner in the center. However, the original button text/label remains fully visible directly behind the moving spinner. 

This creates a serious visual overlap anti-pattern, causing the text to bleed through the background of the loader. It looks unpolished and severely compromises readability and accessibility.

### To Reproduce
1. Render a standard `<button class="ease-btn ease-btn-loading">Submit Changes</button>`.
2. Notice that the text string "Submit Changes" is still visible on screen.
3. The loading spinner animates directly on top of the text characters.

### Expected Behavior
When a button transitions into its loading state, the active text label should cleanly disappear from sight, leaving *only* the centered loading spinner visible to indicate a background processing task to the user.

### Proposed Resolution
1. **Wrap Text Content:** Standardize the inner HTML structure by wrapping the raw text string inside a dedicated `.ease-btn-text` span element.
2. **State Transition:** Add a CSS rule that matches `.ease-btn-loading .ease-btn-text` and cleanly transitions both `opacity` and `visibility` parameters to `0` / `hidden`.
3. **Accessibility Safeguard:** Apply `pointer-events: none` on the loading button to block accidental form double-submits while the processing state is active.
