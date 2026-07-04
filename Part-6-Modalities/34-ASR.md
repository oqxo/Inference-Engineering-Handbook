# 34. ASR

ASR means automatic speech recognition. It converts speech audio into text.

ASR is used for transcription, voice assistants, call analysis, subtitles, and meeting notes.

## Input Audio

Audio quality strongly affects ASR output. Background noise, accents, overlapping speakers, poor microphones, and compression can reduce accuracy.

## Streaming ASR

Streaming ASR transcribes audio while it is still being recorded. This is useful for live captions and voice interfaces.

Streaming systems must balance latency and accuracy.

## Batch ASR

Batch ASR processes a complete audio file. It can use more context and may be easier to optimize for accuracy.

## Post-Processing

ASR output may need punctuation, speaker labels, timestamps, formatting, or domain-specific correction.

## Key Ideas

- ASR converts speech to text.
- Audio quality affects accuracy.
- Streaming ASR prioritizes low latency.
- Batch ASR can use more complete context.

## Developer Checklist

- Test with real audio from your users.
- Track word error rate or task-level accuracy.
- Handle silence, noise, and long files.
- Protect sensitive audio and transcripts.

