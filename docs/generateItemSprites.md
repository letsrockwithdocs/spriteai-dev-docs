---
slug: /generate-item-sprites
sidebar_position: 4
---
# Image Processing Pipeline

This page describes the image processing pipeline used in the SpriteAI project, from initial API request through final sprite generation and optional background removal.

## Overview

The pipeline consists of the following main steps:

1. API Request to DALL-E
2. Image Download 
3. Spritesheet Generation
4. Background Removal (Optional)
5. Image Saving (Optional)

```mermaid
graph TD
    A[Start] --> B[API Request to DALL-E]
    B --> C[Image Download]
    C --> D[Spritesheet Generation]
    D --> E{Background Removal?}
    E -->|Yes| F[Remove Background]
    E -->|No| G{Save Image?}
    F --> G
    G -->|Yes| H[Save Image]
    G -->|No| I[End]
    H --> I
```

## Detailed Pipeline

### 1. API Request to DALL-E

The process begins with constructing a detailed prompt describing the desired character or landscape sprite. This prompt is sent to OpenAI's DALL-E 3 model via API request:

```javascript
const openAiObject = new OpenAI();
const response = await openAiObject.images.generate({
  model: "dall-e-3",
  prompt: prompt,
  size: size,
  n: 1
});
```

### 2. Image Download

Once DALL-E generates the image, it's downloaded using axios:

```javascript
const res = await axios.get(response.data[0].url, { responseType: 'arraybuffer' });
const imgBuffer = Buffer.from(res.data);
```

### 3. Spritesheet Generation 

For character spritesheets, the downloaded image is processed to create an organized spritesheet with proper padding between sprites:

```javascript
const spritesheet = await generateSpritesheet(imgBuffer, {
  rows: states.length,
  framesPerRow: framesPerState,
  padding: padding
});
```

### 4. Background Removal (Optional)

For landscape sprites, there's an option to remove the background:

```javascript
if (options.removeBackground) {
  // Process involves:
  // 1. Writing image to temporary file
  // 2. Removing background color
  // 3. Reading processed image back
  // 4. Cleaning up temporary files
}
```

The background removal uses the Jimp library to replace pixels matching a target color (typically white) with transparency.

### 5. Image Saving (Optional)

If requested, the final processed image can be saved to the local filesystem:

```javascript
if (options.save) {
  const filename = path.join(assetsDir, `${description.replace(/\s+/g, '_')}_landscape.png`);
  await sharp(imgBuffer).toFile(filename);
}
```

## Output

The pipeline returns an object containing:

- URL of the original DALL-E generated image
- Base64 encoded processed image (spritesheet or landscape)
- Metadata about the generated sprite, including dimensions, animation states (for characters), and other relevant details

This processed image data can then be used directly in game development or further asset creation workflows.

```mermaid
classDiagram
    class Output {
        +String originalUrl
        +String processedImageBase64
        +Object metadata
    }
    class Metadata {
        +Object dimensions
        +String[] animationStates
        +Object additionalDetails
    }
    Output *-- Metadata
```

# generateCharacterSpritesheet

Generates a pixel art character spritesheet with multiple animation states.

## Function Signature

```javascript
async function generateCharacterSpritesheet(description, options = {})
```

## Parameters

- `description` (string): A description of the character to generate.
- `options` (object, optional): Configuration options for the spritesheet generation.

## Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| states | string[] | ['idle', 'walk', 'run', 'attack'] | Animation states to generate |
| framesPerState | number | 6 | Number of frames per animation state |
| size | string | '1024x1024' | Output image size |
| style | string | 'pixel-art' | Art style to use |
| padding | number | 1 | Padding between sprites |
| direction | string | 'right' | Base direction the character faces |
| save | boolean | false | Whether to save the generated spritesheet to disk |

## Return Value

The function returns a Promise that resolves to an object with the following properties:

- `original` (string): URL of the original generated image
- `spritesheet` (string): Base64-encoded PNG data URI of the processed spritesheet
- `metadata` (object): Metadata about the generated spritesheet
  - `states` (string[]): List of animation states
  - `framesPerState` (number): Number of frames per state
  - `totalFrames` (number): Total number of frames in the spritesheet
  - `dimensions` (object): Width and height of the spritesheet
  - `frameData` (object): Information about each animation state's frames

```mermaid
sequenceDiagram
    participant User
    participant generateCharacterSpritesheet
    participant DALL-E API
    participant ImageProcessor
    
    User->>generateCharacterSpritesheet: Call with description and options
    generateCharacterSpritesheet->>DALL-E API: Request image generation
    DALL-E API-->>generateCharacterSpritesheet: Return generated image URL
    generateCharacterSpritesheet->>ImageProcessor: Process image into spritesheet
    ImageProcessor-->>generateCharacterSpritesheet: Return processed spritesheet
    generateCharacterSpritesheet-->>User: Return result object
```

## Examples

### Basic Usage

```javascript
import { generateCharacterSpritesheet } from 'spriteAI';

const result = await generateCharacterSpritesheet('a cute robot');
console.log(result.spritesheet); // Base64 encoded spritesheet
console.log(result.metadata); // Metadata about the spritesheet
```

### Custom Animation States

```javascript
const result = await generateCharacterSpritesheet('a fierce dragon', {
  states: ['idle', 'fly', 'breathe-fire', 'roar'],
  framesPerState: 8
});
```

### Saving to Disk

```javascript
await generateCharacterSpritesheet('a ninja warrior', {
  save: true,
  size: '2048x2048'
});
// Saves to ./assets/ninja_warrior_spritesheet.png
```

## Notes

- The function uses DALL-E 3 to generate the initial spritesheet image.
- The generated spritesheet is organized with each row representing a different animation state.
- When `save` is true, the spritesheet is saved in the `assets` folder of the current working directory.
- The function automatically processes the generated image to create a properly formatted spritesheet with the specified number of frames and states.

```mermaid
graph TD
    A[Start] --> B[Parse Options]
    B --> C[Generate DALL-E Prompt]
    C --> D[Call DALL-E API]
    D --> E[Download Generated Image]
    E --> F[Process into Spritesheet]
    F --> G{Save to Disk?}
    G -->|Yes| H[Save Spritesheet]
    G -->|No| I[Prepare Result Object]
    H --> I
    I --> J[Return Result]
    J --> K[End]
```
