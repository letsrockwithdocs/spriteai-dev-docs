---
slug: /
sidebar_position: 1
---

# generateSprite Documentation

## Brief Description
`generateSprite` is a function that generates a sprite sheet image based on a given description, using AI-powered image generation and analysis. Additionally, the `generateItemSprites` function is now available for generating item sprite sheets.

## Usage
To use `generateSprite` or `generateItemSprites`, import them from the sprite module and call them with the appropriate description and options.

```javascript
import { sprite } from './path/to/sprite/module';

const characterResult = await sprite.generateSprite(description, options);
const itemResult = await sprite.generateItemSprites(description, options);
```

## Parameters
For `generateSprite`:
- `description` (string, required): A text description of the character to generate.
- `options` (object, optional):
  - `iterations` (number): Number of sprite variations to generate.
  - `size` (string): Size of the generated image (default: "1024x1024").
  - `save` (boolean): Whether to save the generated image to disk.

For `generateItemSprites`:
- `description` (string, required): A text description of the items to generate.
- `options` (object, optional):
  - `itemCount` (number): Number of items to generate (default: 4).
  - `size` (string): Size of the generated image (default: "1024x1024").
  - `style` (string): Style of the items (default: "pixel-art").
  - `padding` (number): Padding between items (default: 1).
  - `itemType` (string): Type of items (default: "equipment").
  - `background` (string): Background color (default: "white").
  - `save` (boolean): Whether to save the generated image to disk.

## Return Value
For `generateSprite`:
Returns an object or array of objects containing:
- `messages`: JSON object with frameHeight and frameWidth information.
- `image`: Base64-encoded image data URL of the generated sprite sheet.

For `generateItemSprites`:
Returns an object containing:
- `original`: URL of the original generated image.
- `itemSheet`: Base64-encoded image data URL of the generated item sheet.
- `metadata`: Object containing information about the generated items, including:
  - `itemCount`: Number of items generated.
  - `itemType`: Type of items generated.
  - `dimensions`: Width and height of the generated image.
  - `itemData`: Information about the layout of items in the sheet.

## Examples

1. Generate a single character sprite sheet:
```javascript
const result = await sprite.generateSprite("A pixelated robot");
console.log(result.messages);
console.log(result.image);
```

2. Generate multiple character variations:
```javascript
const variations = await sprite.generateSprite("A cartoon cat", { iterations: 3 });
variations.forEach((variation, index) => {
  console.log(`Variation ${index + 1}:`, variation.messages);
});
```

3. Generate an item sprite sheet:
```javascript
const itemResult = await sprite.generateItemSprites("Fantasy weapons", {
  itemCount: 6,
  style: "pixel-art",
  itemType: "weapons"
});
console.log(itemResult.metadata);
console.log(itemResult.itemSheet);
```

## Notes or Considerations
- Both functions use AI models (DALL-E 3) to generate images, which may result in varying outputs for the same input.
- Generated character sprites are optimized for walking animations and follow a specific layout (6 frames in a 2x3 grid).
- Generated item sprites are arranged in a grid layout, with the number of items and layout determined by the `itemCount` option.
- When saving images, they are stored in an 'assets' folder with a filename based on the description.
- The functions may take some time to complete due to API calls and image processing.
- The `generateItemSprites` function is particularly useful for creating game inventory icons or collectible item sets.
- Consider using different styles (e.g., "pixel-art", "vector", "3d") to match your game or application's visual theme.
