# Skill: Text-to-Speech

## Purpose
Convert text content to audio files using TTS APIs.

## Trigger
Use when asked to: convert text to speech, generate audio, narrate, read aloud, TTS.

---

## API Options

| API | Cost | Quality | Limit |
|---|---|---|---|
| OpenAI TTS | $0.015/1K chars | High | 4096 chars/request |
| ElevenLabs | Free tier: 10K chars/mo | Very high | — |
| Edge TTS | Free (Microsoft Edge) | Medium | No limit |

---

## Patterns

### OpenAI TTS
```python
from pathlib import Path
from openai import OpenAI

client = OpenAI()

def text_to_speech(text: str, output_path: str, voice: str = "alloy") -> Path:
    """
    Voices: alloy, echo, fable, onyx, nova, shimmer
    """
    response = client.audio.speech.create(
        model="tts-1",
        voice=voice,
        input=text
    )
    path = Path(output_path)
    response.stream_to_file(path)
    return path
```

### Chunking long text
```python
def chunk_text(text: str, max_chars: int = 4000) -> list[str]:
    """Split at sentence boundaries, not mid-sentence."""
    sentences = text.split(". ")
    chunks = []
    current = ""
    for sentence in sentences:
        if len(current) + len(sentence) > max_chars:
            chunks.append(current.strip())
            current = sentence
        else:
            current += sentence + ". "
    if current:
        chunks.append(current.strip())
    return chunks

def long_text_to_speech(text: str, output_dir: str) -> list[Path]:
    chunks = chunk_text(text)
    paths = []
    for i, chunk in enumerate(chunks):
        path = text_to_speech(chunk, f"{output_dir}/part_{i:03d}.mp3")
        paths.append(path)
    return paths
```

### Free option: Edge TTS
```bash
pip install edge-tts
edge-tts --voice ru-RU-SvetlanaNeural --text "Привет, мир" --write-media output.mp3
```

---

## Rules

- Always chunk text longer than 4000 characters
- Save intermediate chunks — don't regenerate on failure
- Use MP3 format for compatibility
- For Russian text: use `ru-RU-SvetlanaNeural` (Edge TTS) or `nova` (OpenAI)

---

## Output

Audio file(s) in MP3 format, named descriptively: `{title}_{part}.mp3`
