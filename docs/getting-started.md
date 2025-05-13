# Getting Started with SpriteAI

Welcome to SpriteAI, a powerful tool for generating game assets using AI. This guide will help you get started with the main features of SpriteAI.

## Installation

To use SpriteAI, you need to have Node.js installed on your system. Once you have Node.js, you can install SpriteAI using npm:

```bash
npm install spriteai
```

## Basic Usage

First, import the necessary functions from the SpriteAI package:

```javascript
import { 
  generateCharacterSpritesheet, 
  generateEnvironmentSprites, 
  generateItemSprites,
  fetchAvailableAnimationStates,
  fetchAvailableSpriteStyles
} from 'spriteai';
```

## Generating Character Spritesheets

To create a character spritesheet, use the `generateCharacterSpritesheet` function:

```javascript
const characterSprite = await generateCharacterSpritesheet('a medieval knight', {
  states: ['idle', 'walk', 'run', 'attack'],
  framesPerState: 6,
  size: '1024x1024',
  style: 'pixel-art',
  direction: 'right'
});

console.log(characterSprite.spritesheet); // Base64 encoded spritesheet
console.log(characterSprite.metadata); // Metadata about the spritesheet
```

## Generating Environment Sprites

For environment sprites, use the `generateEnvironmentSprites` function:

```javascript
const environmentSprites = await generateEnvironmentSprites('forest', {
  elements: 4,
  size: '1024x1024',
  style: 'pixel-art',
  theme: 'fantasy'
});

console.log(environmentSprites.tileset); // Base64 encoded tileset
console.log(environmentSprites.metadata); // Metadata about the tileset
```

## Generating Item Sprites

To create item sprites, use the `generateItemSprites` function:

```javascript
const itemSprites = await generateItemSprites('medieval weapons', {
  itemCount: 4,
  size: '1024x1024',
  style: 'pixel-art',
  itemType: 'equipment'
});

console.log(itemSprites.itemSheet); // Base64 encoded item sheet
console.log(itemSprites.metadata); // Metadata about the item sheet
```

## Fetching Available Options

SpriteAI provides functions to fetch available animation states and sprite styles:

```javascript
const availableStates = await fetchAvailableAnimationStates();
console.log(availableStates); // ['idle', 'walk', 'run', 'attack', 'jump', 'fall', 'hurt', 'die']

const availableStyles = await fetchAvailableSpriteStyles();
console.log(availableStyles); // ['pixel-art', 'vector', '3d', 'hand-drawn', 'anime']
```

## Saving Generated Sprites

To save generated assets locally, include the `save: true` option in the function call:

```javascript
const characterSprite = await generateCharacterSpritesheet('a medieval knight', {
  save: true
});
```

This will save the spritesheet in the `assets` folder of your current working directory.

## Conclusion

This guide covers the basic usage of SpriteAI. For more detailed information on each function and its options, please refer to the API documentation.
