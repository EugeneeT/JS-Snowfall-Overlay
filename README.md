# Snowfall Background

A lightweight JavaScript package that adds a beautiful snowfall animation to your web page with customizable options.

## Installation

Install the package using npm:

```bash
npm install snowfall-background
```

## Usage

### For React Projects

```javascript
import React, { useEffect } from "react";
import startSnowfall from "snowfall-background";
Import SnowflakeImage from "./path/to/snowflake.png";

const SnowfallPage = () => {
  useEffect(() => {
    // Start snowfall with custom options
    const snowfall = startSnowfall({
      snowflakeCount: 200,
      sizeRange: [5, 25],
      animationDurationRange: [30, 60],
      snowflakeImage: SnowflakeImage,
    });

    // Clean up snowfall when the component unmounts
    return () => {
      snowfall.destroy();
    };
  }, []);

  return <div>Your content here</div>;
};

export default SnowfallPage;
```

### For Vanilla HTML/JavaScript

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Snowfall Background</title>
    <script type="module">
      import startSnowfall from "https://unpkg.com/snowfall-background/snowfall.js";

      // Start snowfall when the page loads
      window.addEventListener("load", () => {
        const snowfall = startSnowfall({
          snowflakeCount: 150,
          sizeRange: [8, 16],
          snowflakeImage: "./path/to/snowflake.png",
        });
      });
    </script>
  </head>
  <body>
    <h1>Snowy Page</h1>
  </body>
</html>
```

## Handling Snowflake Positioning

### Accumulation at Top of Page

If you notice snowflakes accumulating at the top of the page before falling, you have several options:

1. **React Component Styling**:

   ```jsx
   const SnowfallPage = () => {
     useEffect(() => {
       const snowfall = startSnowfall({
         // ... other options
       });

       // Optional: Add custom styling
       const style = document.createElement("style");
       style.textContent = `
         .snowflake {
           will-change: transform, opacity;
           opacity: 0;
         }
       `;
       document.head.appendChild(style);

       return () => {
         snowfall.destroy();
         document.head.removeChild(style);
       };
     }, []);

     return <div>Your content here</div>;
   };
   ```

2. **Z-Index Solution**:
   If you have a navigation banner or header, ensure it has a higher z-index:
   ```css
   .snowflake {
     z-index: 1;
   }
   .navigation-banner {
     z-index: 10;
     position: relative;
   }
   ```

## API Options

- **snowflakeCount** (default: 150): Number of snowflakes
- **sizeRange** (default: [8, 16]): Snowflake size range (pixels)
- **animationDurationRange** (default: [25, 50]): Animation duration range (seconds)
- **container** (default: `document.body`): Container for snowflakes
- **snowflakeImage**: Custom snowflake image path

## Snowflake Image

- Include a custom snowflake image by providing its path
- Recommended image type: PNG with transparent background
- Default image is included in the package

## Methods

- `startSnowfall(options)`: Initializes snowfall
- `snowfall.destroy()`: Removes all snowflakes

## License

MIT License

**Created by Eugen Taranowski**
