# spriteAI Overview

spriteAI is a powerful project designed to generate character spritesheets, pixel art, animated emojis, and other game-related assets using AI-powered image generation and processing techniques. This overview will introduce you to the main features and components of spriteAI.

## Features

spriteAI offers a range of functions to create various types of game assets:

1. Character Spritesheets
2. Pixel Art Sprites
3. Animated Emojis
4. Isometric Sprites
5. Environment Sprites
6. Item Sprites

Each of these features utilizes AI models (primarily DALL-E 3) to generate high-quality, customizable assets based on text descriptions.

## Main Components

### 1. Character Spritesheet Generation

The `generateCharacterSpritesheet` function allows you to create detailed character spritesheets with multiple animation states.

```javascript
import { generateCharacterSpritesheet } from './index.js';

const description = 'a cute dragon';
const options = {
  states: ['idle', 'walk', 'run'],
  framesPerState: 4,
  size: '512x512',
  style: 'pixel-art',
  padding: 2,
  direction: 'left',
  save: true
};

generateCharacterSpritesheet(description, options)
  .then(result => {
    console.log('Spritesheet generated:', result.spritesheet);
  })
  .catch(error => {
    console.error('Error generating spritesheet:', error);
  });
```

### 2. Pixel Art Generation

The `generatePixelArt` function creates pixel art sprites based on text descriptions.

### 3. Animated Emoji Generation

Use `generateAnimatedEmoji` to create 4-frame animated emojis.

### 4. Isometric Sprite Generation

`generateIsometric` produces isometric-style sprites for objects or characters.

### 5. Environment Sprite Generation

`generateEnvironmentSprites` creates tilesets for game environments.

### 6. Item Sprite Generation

`generateItemSprites` produces sprites for game items or equipment.

## Utility Functions

- `removeBackgroundColor`: Removes a specific background color from an image.
- `fetchAvailableAnimationStates`: Retrieves a list of available animation states.
- `fetchAvailableSpriteStyles`: Provides a list of available sprite styles.

## Getting Started

To use spriteAI, you'll need to install the necessary dependencies:

```bash
npm install
```

Make sure you have the required API credentials set up for using the OpenAI image generation service.

## Usage Notes

- All generation functions use AI models, which may produce varying results for the same input.
- Generated assets are typically returned as Base64-encoded image data URLs.
- Most functions offer an option to save the generated images to disk.
- Processing times may vary due to API calls and image processing.

For detailed information on each function, please refer to their specific documentation pages.

## Contributing

Contributions to spriteAI are welcome. Please refer to the project's GitHub repository for guidelines on how to contribute.

## License

spriteAI is licensed under the MIT License. See the LICENSE file in the project repository for full license text.