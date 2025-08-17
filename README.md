## Login Page UI

A minimal, static login page built with plain HTML and CSS. It includes:
- A centered login box with username and password fields
- A decorative avatar circle
- An optional full-screen file panel that can be toggled into view

This repository ships no JavaScript functionality by default; you can add your own behavior as needed.

### Files
- `Index.html`: Page markup and component structure
- `style.css`: Visual styling for all components and utility classes

### Quick start
- Open `Index.html` directly in a modern browser.
- Ensure `style.css` is in the same directory.
- The page references `main.js`, but no such file is included. Either remove that `<script>` tag or provide your own JavaScript (see examples below).

### Public API: Components and CSS classes
Use these classes in your markup to compose the page. You can rename them, but update your HTML accordingly.

- **Page**
  - `body`: Global background, typography, and box-sizing.

- **Login box**
  - `.box`: Container for the login form. Positioned absolutely, horizontally centered via `transform: translate(-50%)` and vertically positioned at ~30% from top. Rounded with dark theme background.
    - `h1`: Title styled under `.box h1`.
    - `input.txt`: Username field. Equivalent to `input[type="text"]` inside `.box`.
    - `input.psw`: Password field. Equivalent to `input[type="password"]` inside `.box`.
    - `.btn`: Wrapper for the main button and extras.
    - `button`: Primary call-to-action. Rounded button styled globally.
    - `.or`: Separator text between actions.
    - `.sing`: Link-style secondary action.
  - Focus behavior: Inputs expand from 150px to 250px width on focus and change border color/radius.

- **Decorative avatar**
  - `.cercel`: Circular background element placed behind the box. When used inside `.box`, it appears as a decorative avatar circle.
  - `.head`, `.body`: Small rounded shapes positioned to resemble a simplistic avatar; typically placed in a sibling container to `.cercel`.

- **Full-screen file panel**
  - `.page2-file`: Full-viewport panel, initially off-screen (`right: -100%`). Add the `onclick` class to slide it into view (`right: 0`). High `z-index` so it overlays the page.
  - `.page2-file.onclick`: Variant that shows the panel.
  - Contains a child wrapper `div.continer` (sic) which holds an `input[type="file"]`.

### Markup structure (recommended)
Here is a minimal structure that uses the provided classes.

```html
<link rel="stylesheet" href="style.css">

<div class="page2-file" id="filePanel">
  <div class="continer">
    <input type="file" />
  </div>
</div>

<div class="box">
  <form>
    <h1>Login</h1>
    <input type="text" placeholder="Username" class="txt" />
    <input type="password" placeholder="Password" class="psw" />

    <div class="btn">
      <button type="button" id="loginButton">Login</button>
      <p class="or">_____OR_____</p>
      <a class="sing" href="#" id="openFilePanel">Sign in with file</a>
    </div>
  </form>

  <div class="cercel">
    <img src="FB_IMG_1576695994379.jpg" alt="Avatar" />
  </div>

  <div class="none">
    <div class="head"></div>
    <div class="body"></div>
  </div>
</div>
```

### Optional JavaScript behaviors
No JavaScript is bundled. If you want to enable interactions, you can add a small script. Either create `main.js` and include it, or place a `<script>` tag at the end of `Index.html`.

- **Show/hide the file panel** by toggling the `onclick` class on `.page2-file`.
- **Handle the login button** to prevent form submission while you wire up your auth logic.

```js
// Example behavior (attach after DOM is ready)
const filePanel = document.querySelector('.page2-file');
const openFilePanel = document.querySelector('#openFilePanel');
const loginButton = document.querySelector('#loginButton');

if (openFilePanel && filePanel) {
  openFilePanel.addEventListener('click', (event) => {
    event.preventDefault();
    filePanel.classList.add('onclick');
  });

  // Click outside to close
  filePanel.addEventListener('click', (event) => {
    if (event.target === event.currentTarget) {
      filePanel.classList.remove('onclick');
    }
  });
}

if (loginButton) {
  loginButton.addEventListener('click', (event) => {
    event.preventDefault();
    // TODO: Replace with real login logic
    alert('Implement login logic here.');
  });
}
```

### Theming and customization
- **Colors**: Primary palette uses dark grays (`#0b0c10`, `#1f2833`), teal accents (`#45a29e`, `#66fcf1`), and highlight variants (`#fce181`). Update the color values in `style.css` to re-theme.
- **Sizing**: The login inputs expand on focus. Adjust widths in `.box input[type="text"], .box input[type="password"]` and the focus rule.
- **Positioning**: The login box is centered horizontally with `transform: translate(-50%)` and placed at `top: 30%`. If you want true center, change to `transform: translate(-50%, -50%)` and adjust `top: 50%`.

### Accessibility recommendations
- Add `<label for="...">` tags associated with inputs, or use `aria-label` when appropriate.
- Use a proper submit button (`<button type="submit">`) and handle the submit event in JavaScript if you build an auth flow.
- Provide `alt` text for images (as shown above) and ensure sufficient color contrast for text.

### Notes and gotchas
- The HTML in `Index.html` references `main.js` which is not included. Provide your own or remove the script tag.
- Avoid using inline `onclick` attributes on buttons. Prefer adding event listeners in JavaScript (see example above).
- There is an extra closing `</input>` tag in the original markup that is not needed; inputs are self-closing in HTML.
- Class name `continer` is intentional in the source; if you prefer `container`, rename it in your HTML and CSS consistently.

### License
No license specified. Add one if you plan to distribute or open-source beyond Hacktoberfest demos.
