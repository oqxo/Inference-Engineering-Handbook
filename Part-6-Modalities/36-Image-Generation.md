# 36. Image Generation

Image generation models create images from prompts, reference images, or other conditioning inputs.

They are used for design, marketing, games, education, prototyping, and creative tools.

## Text-To-Image

Text-to-image models generate an image from a written description.

The prompt describes subject, style, composition, lighting, and constraints.

## Image-To-Image

Image-to-image systems use an existing image as input and create a modified or related output.

This is useful for editing, restyling, cleanup, and variation generation.

## Inference Concerns

Image generation is often slower than text classification or embeddings. Resolution, number of steps, model size, and batch size affect latency and cost.

Generated images may also require moderation and storage handling.

## Quality Evaluation

Image quality is subjective. For production systems, evaluate whether images satisfy the user's task, not only whether they look impressive.

## Key Ideas

- Image generation creates visual output from prompts or references.
- Resolution and generation settings affect cost.
- Output may require moderation.
- Task success matters more than artistic novelty.

## Developer Checklist

- Set limits for resolution and batch count.
- Store prompts, settings, and outputs for debugging when policy allows.
- Moderate unsafe or restricted content.
- Test with domain-specific prompts.

