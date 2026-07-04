# 32. VLMs

A vision-language model, or VLM, processes both images and text.

VLMs can answer questions about images, describe screenshots, extract information from documents, or reason over visual content.

## Inputs

A VLM request may include:

- Text instructions
- One or more images
- Conversation history
- Retrieved context

The image is converted into internal representations that the language model can use.

## Use Cases

Common use cases include:

- Document understanding
- Chart explanation
- UI screenshot analysis
- Visual question answering
- Image-based customer support

## Inference Concerns

Images add preprocessing time and memory use. Image resolution, number of images, and model architecture affect cost.

Do not assume image requests cost the same as text-only requests.

## Key Ideas

- VLMs combine vision and language.
- Images are transformed before the model reasons over them.
- Image size and count affect latency and cost.
- VLM outputs still need validation.

## Developer Checklist

- Limit image size and number of images per request.
- Test with real screenshots or documents.
- Validate extracted fields.
- Log modality-specific metrics such as image count and resolution.

