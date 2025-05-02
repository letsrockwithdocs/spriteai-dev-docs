# SpriteAI Documentation

## Introduction

SpriteAI is a powerful library for generating game assets using AI. It provides functions to create character spritesheets, environment sprites, and item sprites for game development. This documentation covers the main features and usage of the SpriteAI library.

## Table of Contents

1. [Character Spritesheet Generation](#character-spritesheet-generation)
2. [Environment Sprite Generation](#environment-sprite-generation)
3. [Item Sprite Generation](#item-sprite-generation)
4. [Utility Functions](#utility-functions)

## Character Spritesheet Generation

The `generateCharacterSpritesheet` function allows you to create character spritesheets with various animation states.

### Usage

```javascript
import { generateCharacterSpritesheet } from 'spriteAI';

const result = await generateCharacterSpritesheet('a warrior character', {
  states: ['idle', 'walk', 'run', 'attack'],
  framesPerState: 6,
  size: '1024x1024',
  style: 'pixel-art',
  padding: 1,
  direction: 'right'
});
```

### Parameters

- `description` (string): A description of the character to generate.
- `options` (object): Configuration options for the spritesheet generation.
  - `states` (array): Animation states to include (default: ['idle', 'walk', 'run', 'attack']).
  - `framesPerState` (number): Number of frames per animation state (default: 6).
  - `size` (string): Size of the output image (default: '1024x1024').
  - `style` (string): Art style of the spritesheet (default: 'pixel-art').
  - `padding` (number): Padding between frames (default: 1).
  - `direction` (string): Direction the character faces (default: 'right').

### Return Value

The function returns an object containing:
- `original`: URL of the original generated image.
- `spritesheet`: Base64-encoded PNG data of the processed spritesheet.
- `metadata`: Detailed information about the generated spritesheet.

## Environment Sprite Generation

The `generateEnvironmentSprites` function creates environmental sprites for game backgrounds and tilesets.

### Usage

```javascript
import { generateEnvironmentSprites } from 'spriteAI';

const result = await generateEnvironmentSprites('forest', {
  elements: 4,
  size: '1024x1024',
  style: 'pixel-art',
  padding: 1,
  theme: 'fantasy'
});
```

### Parameters

- `description` (string): A description of the environment to generate.
- `options` (object): Configuration options for the environment sprite generation.
  - `elements` (number): Number of distinct environment pieces to generate (default: 4).
  - `size` (string): Size of the output image (default: '1024x1024').
  - `style` (string): Art style of the sprites (default: 'pixel-art').
  - `padding` (number): Padding between sprites (default: 1).
  - `theme` (string): Theme of the environment (default: 'fantasy').

### Return Value

The function returns an object containing:
- `original`: URL of the original generated image.
- `tileset`: Base64-encoded PNG data of the processed tileset.
- `metadata`: Detailed information about the generated environment sprites.

## Item Sprite Generation

The `generateItemSprites` function creates sprites for game items, such as equipment or collectibles.

### Usage

```javascript
import { generateItemSprites } from 'spriteAI';

const result = await generateItemSprites('medieval weapons', {
  itemCount: 4,
  size: '1024x1024',
  style: 'pixel-art',
  padding: 1,
  itemType: 'equipment',
  background: 'white'
});
```

### Parameters

- `description` (string): A description of the items to generate.
- `options` (object): Configuration options for the item sprite generation.
  - `itemCount` (number): Number of distinct items to generate (default: 4).
  - `size` (string): Size of the output image (default: '1024x1024').
  - `style` (string): Art style of the sprites (default: 'pixel-art').
  - `padding` (number): Padding between sprites (default: 1).
  - `itemType` (string): Type of items to generate (default: 'equipment').
  - `background` (string): Background color of the sprite sheet (default: 'white').

### Return Value

The function returns an object containing:
- `original`: URL of the original generated image.
- `itemSheet`: Base64-encoded PNG data of the processed item sheet.
- `metadata`: Detailed information about the generated item sprites.

## Utility Functions

SpriteAI provides additional utility functions to enhance your sprite generation workflow.

### fetchAvailableAnimationStates

Retrieves a list of available animation states for character spritesheets.

```javascript
import { fetchAvailableAnimationStates } from 'spriteAI';

const states = await fetchAvailableAnimationStates();
console.log(states); // ['idle', 'walk', 'run', 'attack', 'jump', 'fall', 'hurt', 'die']
```

### fetchAvailableSpriteStyles

Retrieves a list of available sprite styles for asset generation.

```javascript
import { fetchAvailableSpriteStyles } from 'spriteAI';

const styles = await fetchAvailableSpriteStyles();
console.log(styles); // ['pixel-art', 'vector', '3d', 'hand-drawn', 'anime']
```

These utility functions can be used to provide options to users or to validate input in your application.

## Conclusion

SpriteAI offers a comprehensive set of tools for generating game assets using AI. By leveraging these functions, game developers can quickly create high-quality sprites for characters, environments, and items, streamlining the asset creation process in game development.