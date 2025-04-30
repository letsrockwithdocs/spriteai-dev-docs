---
slug: /
sidebar_position: 1
---

# generateSprite Documentation

## Brief Description
`generateSprite` is a function that generates a sprite sheet image based on a given description, using AI-powered image generation and analysis.

## Usage
To use `generateSprite`, import it from the sprite module and call it with a description of the character you want to generate.

```javascript
import { sprite } from './path/to/sprite/module';

const result = await sprite.generateSprite(description, options);
```

## Parameters
- `description` (string, required): A text description of the character to generate.
- `options` (object, optional):
  - `iterations` (number): Number of sprite variations to generate.
  - `size` (string): Size of the generated image (default: "1024x1024").
  - `save` (boolean): Whether to save the generated image to disk.

## Return Value
Returns an object or array of objects containing:
- `messages`: JSON object with frameHeight and frameWidth information.
- `image`: Base64-encoded image data URL of the generated sprite sheet.

## Examples

1. Generate a single sprite sheet:
```javascript
const result = await sprite.generateSprite("A pixelated robot");
console.log(result.messages);
console.log(result.image);
```

2. Generate multiple variations:
```javascript
const variations = await sprite.generateSprite("A cartoon cat", { iterations: 3 });
variations.forEach((variation, index) => {
  console.log(`Variation ${index + 1}:`, variation.messages);
});
```

## Notes or Considerations
- The function uses AI models (DALL-E 3 and GPT) to generate and analyze images, which may result in varying outputs for the same input.
- Generated sprites are optimized for walking animations and follow a specific layout (6 frames in a 2x3 grid).
- The function converts images to grayscale, which may affect the final output.
- When saving images, they are stored in an 'assets' folder with a filename based on the description.
- The function may take some time to complete due to API calls and image processing.

## generateItemSprites Function

The `generateItemSprites` function is a new addition to the sprite generation module. It allows you to generate a collection of item sprites for game assets.

### Usage
```javascript
import { sprite } from './path/to/sprite/module';

const result = await sprite.generateItemSprites(description, options);
```

### Parameters
- `description` (string, required): A text description of the items to generate.
- `options` (object, optional):
  - `itemCount` (number): Number of items to generate (default: 4).
  - `size` (string): Size of the generated image (default: "1024x1024").
  - `style` (string): Style of the generated items (default: "pixel-art").
  - `padding` (number): Padding between items (default: 1).
  - `itemType` (string): Type of items to generate (default: "equipment").
  - `background` (string): Background color of the generated image (default: "white").
  - `save` (boolean): Whether to save the generated image to disk.

### Return Value
Returns an object containing:
- `original`: URL of the original generated image.
- `itemSheet`: Base64-encoded image data URL of the generated item sheet.
- `metadata`: Object containing information about the generated items, including:
  - `itemCount`: Number of items generated.
  - `itemType`: Type of items generated.
  - `dimensions`: Width and height of the generated image.
  - `itemData`: Information about the layout of items in the sheet.

### Example
```javascript
const result = await sprite.generateItemSprites("Fantasy RPG weapons", {
  itemCount: 6,
  style: "pixel-art",
  itemType: "weapons"
});
console.log(result.metadata);
console.log(result.itemSheet);
```

### Notes or Considerations
- The function uses AI models (DALL-E 3) to generate item sprites, which may result in varying outputs for the same input.
- Generated items are arranged in a grid layout, with a maximum of 2 columns.
- The function provides options for customizing the style, background, and type of items generated.
- When saving images, they are stored in an 'assets' folder with a filename based on the description.
- The function may take some time to complete due to API calls and image processing.
