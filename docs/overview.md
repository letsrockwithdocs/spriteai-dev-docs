# spriteAI Overview

spriteAI is a powerful tool designed to generate and manipulate character spritesheets and images using OpenAI's DALL-E 3 API and various image processing libraries. This project provides a set of functions for creating pixel art, character animations, environment sprites, and more.

## Key Features

- Generate character spritesheets with customizable animation states
- Create pixel art sprites
- Produce isometric sprite images
- Generate environment and item sprites
- Create animated emojis
- Remove background colors from images
- Split sprite sheets into individual frames
- Analyze unique colors in images

## Core Functions

### generateCharacterSpritesheet

Creates a complete character spritesheet with multiple animation states and frames.

```javascript
const result = await generateCharacterSpritesheet(description, options);
```

### generatePixelArt

Generates a pixel art sprite based on a given description.

```javascript
const result = await sprite.generatePixelArt(description, options);
```

### generateIsometric

Produces an isometric sprite image for objects or characters.

```javascript
const result = await sprite.generateIsometric(description, options);
```

### generateEnvironmentSprites

Creates a tileset of environment sprites for game development.

```javascript
const result = await generateEnvironmentSprites(description, options);
```

### generateItemSprites

Generates a collection of item sprites for game inventories or pickups.

```javascript
const result = await generateItemSprites(description, options);
```

### generateAnimatedEmoji

Creates a 4-frame animated emoji based on a given description.

```javascript
const result = await sprite.generateAnimatedEmoji(description, options);
```

## Utility Functions

- `removeBackgroundColor`: Removes a specific background color from an image
- `splitSpriteSheet`: Splits a sprite sheet into individual frame images
- `getUniqueColors`: Analyzes an image and returns an array of unique colors
- `encodeImage`: Converts an image file to a base64-encoded string

## Getting Started

To use spriteAI, you'll need to have Node.js installed and set up an OpenAI API key. Clone the repository and install the dependencies:

```bash
git clone <repository-url>
cd spriteAI
npm install
```

Make sure to set your OpenAI API key as an environment variable or in a configuration file before using the image generation functions.

## Usage Example

Here's a basic example of generating a character spritesheet:

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

## Contributing

Contributions to spriteAI are welcome! Please feel free to submit issues, feature requests, or pull requests to help improve the project.

## License

This project is licensed under the MIT License. See the LICENSE file in the repository for more details.