---
name: generate-video
description: Instruction set to generate animated videos from comic images using the Google Veo / Gemini API.
---
# Generate Video Skill

This skill provides instructions and reusable Python scripts to generate high-quality, animated video clips from static comic panel images using **Google Veo** via the Gemini API (`google-genai` SDK).

## Setup Requirements

Ensure you have the Google GenAI SDK installed:
```bash
pip install google-genai
```

You must have the `GEMINI_API_KEY` set in your environment variables.

## How to Generate Video with Veo

Here is a standard integration script to convert a static image into a 5-second video using the latest Veo model.

### Implementation Script (`scripts/generate_veo.py`)

```python
import os
import time
from google import genai
from google.genai import types

def generate_video_from_image(image_path: str, prompt: str, output_path: str):
    """
    Generates a video clip from a static image using Google Veo.
    """
    if not os.path.exists(image_path):
        raise FileNotFoundError(f"Image not found at {image_path}")

    # Initialize the Gemini GenAI Client
    client = genai.Client()

    # Read the image bytes
    with open(image_path, 'rb') as f:
        image_bytes = f.read()

    print(f"Uploading {image_path} and requesting video generation...")
    
    # Call Veo to generate video
    operation = client.models.generate_videos(
        model='veo-3.1-generate-preview',
        prompt=prompt,
        image={"image_bytes": image_bytes, "mime_type": "image/png"},
        config=types.GenerateVideosConfig(
            aspect_ratio='16:9',
            duration_seconds=5,
            person_generation='allow_adult',
        )
    )

    # Poll for completion
    while not operation.done:
        print("Generation in progress, waiting 10 seconds...")
        time.sleep(10)
        operation = client.operations.get(operation)

    if operation.error:
        raise RuntimeError(f"Video generation failed: {operation.error}")

    # Save the generated video file
    generated_video = operation.result.generated_videos[0]
    with open(output_path, 'wb') as f:
        f.write(generated_video.video.bytes)
        
    print(f"SUCCESS! Animated video saved to {output_path}")

if __name__ == "__main__":
    # Example usage:
    # generate_video_from_image("input.png", "A slow pan right across the futuristic lab", "output.mp4")
    pass
```

## Best Practices for Prompts
* **Camera Movement:** Explicitly state the camera action (e.g., "slow pan right", "gentle zoom in", "rack focus").
* **Maintain Consistency:** Reference elements in the original image (e.g., "Keep the character Dia still while the background lights flicker gently").
* **English Only:** Ensure all prompts are written in English.
