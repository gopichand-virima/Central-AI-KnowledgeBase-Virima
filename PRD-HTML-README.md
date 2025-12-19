# PRD HTML Viewer - Instructions

## Overview
The `KB-SSOT-PRD.html` file is a standalone HTML page that displays your PRD with professional Virima-branded styling.

## How to Use

### Option 1: Local Web Server (Recommended)
Due to browser security restrictions, you need to serve the files via a web server:

**Using Python:**
```bash
# Python 3
python -m http.server 8000

# Then open: http://localhost:8000/KB-SSOT-PRD.html
```

**Using Node.js:**
```bash
npx http-server -p 8000

# Then open: http://localhost:8000/KB-SSOT-PRD.html
```

**Using VS Code:**
1. Install "Live Server" extension
2. Right-click on `KB-SSOT-PRD.html`
3. Select "Open with Live Server"

### Option 2: Direct File Access
If you open the HTML file directly (double-click), it may not load the markdown file due to CORS restrictions. The page will show an error message with troubleshooting steps.

## Features

- **Virima Brand Styling**: Professional color scheme matching Virima's design system
- **Responsive Design**: Works on desktop, tablet, and mobile devices
- **Interactive Table of Contents**: Auto-generated from headings with smooth scrolling
- **Styled Tables**: Professional table formatting with hover effects
- **Print-Friendly**: Optimized for printing
- **Scroll to Top**: Button appears when scrolling down

## File Structure

```
.
├── KB-SSOT PRD.md          # Source markdown file
├── KB-SSOT-PRD.html        # HTML viewer (this file)
└── PRD-HTML-README.md      # This instructions file
```

## Customization

The HTML file includes embedded CSS with Virima brand colors. You can customize:

- **Colors**: Edit the CSS variables in the `:root` section
- **Typography**: Modify font families and sizes
- **Layout**: Adjust container width and spacing

## Browser Compatibility

- Chrome/Edge (latest)
- Firefox (latest)
- Safari (latest)
- Mobile browsers

## Troubleshooting

**Issue**: "Error Loading PRD" message
- **Solution**: Ensure you're using a web server (not file:// protocol)
- **Solution**: Check that `KB-SSOT PRD.md` is in the same directory

**Issue**: Tables not displaying correctly
- **Solution**: The page uses marked.js which should handle tables automatically
- **Solution**: Check browser console for JavaScript errors

**Issue**: Styling looks broken
- **Solution**: Ensure internet connection for CDN resources (marked.js)
- **Solution**: Check browser console for CSS loading errors

## Notes

- The HTML file uses the `marked.js` library from CDN for markdown parsing
- All styling is embedded in the HTML file (no external CSS needed)
- The page automatically generates a table of contents from headings
- Tables are automatically styled with Virima branding

