---
slug: /
sidebar_position: 1
---

# generateSprite Documentation

## Brief Description
`generateSprite` is a function that generates a sprite sheet image based on a given description, using AI-powered image generation and analysis. Additionally, the `generateItemSprites` function generates a collection of item sprites for game development.

## Usage
To use `generateSprite` or `generateItemSprites`, import them from the sprite module and call them with the appropriate parameters.

```javascript
import { sprite } from './path/to/sprite/module';

const characterResult = await sprite.generateSprite(description, options);
const itemResult = await sprite.generateItemSprites(description, options);
```

## Parameters
### generateSprite
- `description` (string, required): A text description of the character to generate.
- `options` (object, optional):
  - `states` (array): Animation states to generate (default: ['idle', 'walk', 'run', 'attack']).
  - `framesPerState` (number): Number of frames per animation state (default: 6).
  - `size` (string): Size of the generated image (default: "1024x1024").
  - `style` (string): Style of the sprite (default: "pixel-art").
  - `padding` (number): Padding between frames (default: 1).
  - `direction` (string): Direction the character faces (default: "right").
  - `save` (boolean): Whether to save the generated image to disk.

### generateItemSprites
- `description` (string, required): A text description of the items to generate.
- `options` (object, optional):
  - `itemCount` (number): Number of items to generate (default: 4).
  - `size` (string): Size of the generated image (default: "1024x1024").
  - `style` (string): Style of the sprites (default: "pixel-art").
  - `padding` (number): Padding between items (default: 1).
  - `itemType` (string): Type of items to generate (default: "equipment").
  - `background` (string): Background color (default: "white").
  - `save` (boolean): Whether to save the generated image to disk.

## Return Value
### generateSprite
Returns an object containing:
- `original`: URL of the original generated image.
- `spritesheet`: Base64-encoded image data URL of the processed sprite sheet.
- `metadata`: Object with information about the sprite sheet, including states, frames, and dimensions.

### generateItemSprites
Returns an object containing:
- `original`: URL of the original generated image.
- `itemSheet`: Base64-encoded image data URL of the processed item sheet.
- `metadata`: Object with information about the item sheet, including item count, dimensions, and layout.

## Examples

1. Generate a character sprite sheet:
```javascript
const result = await sprite.generateSprite("A pixelated robot", {
  states: ['idle', 'walk', 'attack'],
  framesPerState: 4,
  style: "pixel-art"
});
console.log(result.metadata);
console.log(result.spritesheet);
```

2. Generate item sprites:
```javascript
const itemResult = await sprite.generateItemSprites("Fantasy weapons and armor", {
  itemCount: 6,
  itemType: "equipment",
  style: "pixel-art"
});
console.log(itemResult.metadata);
console.log(itemResult.itemSheet);
```

## Notes or Considerations
- Both functions use AI models (DALL-E 3) to generate images, which may result in varying outputs for the same input.
- The generated sprites are optimized for the specified animation states or item types.
- When saving images, they are stored in an 'assets' folder with a filename based on the description.
- The functions may take some time to complete due to API calls and image processing.
- Consider adjusting the `size` and `itemCount` parameters based on your specific needs and the complexity of the sprites you want to generate.
- The `style` parameter allows you to specify different art styles, such as "pixel-art", "vector", or "hand-drawn".
- For item sprites, you can customize the background color to match your game's UI or to create transparent backgrounds.
