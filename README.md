# Quark's Outlines

Educational Python articles based on Python 1.4 Reference Manual.

## Fine-tuned Model

```
ft:gpt-4o-mini-2024-07-18:default-organization:quarks-outlines:CodyDJRI
```

## How to Generate New Articles

```python
from openai import OpenAI
client = OpenAI()

system = """You are Quark, a technical writer who transforms Python documentation into educational articles. Given a section from the Python Reference Manual, write a Quark's Outlines article with:
1. Title: 'Quark's Outlines: [Topic]' with subtitle '*Overview, Historical Timeline, Problems & Solutions*'
2. Overview with 4-5 question-based subsections, each with explanation, bold insight, and code example
3. Historical Timeline with dates
4. 5 Problems & Solutions with real-world examples
Use simple language. Germanic/Anglo-Saxon verbs preferred (built, wrote, ran). No flowery language."""

# Paste Python 1.4 docs section as source
source = "YOUR PYTHON DOCS SECTION HERE"

response = client.chat.completions.create(
    model="ft:gpt-4o-mini-2024-07-18:default-organization:quarks-outlines:CodyDJRI",
    messages=[
        {"role": "system", "content": system},
        {"role": "user", "content": source}
    ],
    max_tokens=4000
)

print(response.choices[0].message.content)
```

## Source Documentation

- Python 1.4 Reference Manual: https://docs.python.org/release/1.4/ref/
- Local copy: `python14_docs/ref*.txt`

## Progress

**Completed (102-145):**
- Chapter 3: Data Model (types, special methods, emulation)
- Chapter 4: Execution Model (code blocks, frames, namespaces, exceptions)
- Chapter 5: Expressions intro + Arithmetic Conversions

**Remaining (Chapter 5 continued + 6-8):**
- 5.2 Atoms (Identifiers, Literals, Parenthesized forms, List/Dict displays, String conversions)
- 5.3 Primaries (Attribute refs, Subscriptions, Slicings, Calls)
- 5.4-5.12 Operators (Power, Unary, Binary, Shifting, Bitwise, Comparisons, Boolean, Expression lists)
- Chapter 6: Simple statements (assignment, pass, del, print, return, raise, break, continue, import, global, exec)
- Chapter 7: Compound statements (if, while, for, try, function defs, class defs)
- Chapter 8: Top-level components

## Training Data

- `quarks_training_final.jsonl` - 43 examples, source docs -> article format
- OpenAI file ID: `file-QcFaZNzqGbG9FZmytpJ4pv`
- Job ID: `ftjob-euGZJKE2tPfFHXk1s7f8WVrs`

## Publishing to Dev.to

Articles in `articles/*.md` auto-publish to Dev.to via GitHub Actions on push to main.

### Workflow

1. **Upload cover image to catbox.moe:**
   ```bash
   curl -F "reqtype=fileupload" -F "fileToUpload=@articles/your-image.png" https://catbox.moe/user/api.php
   ```

2. **Create article with frontmatter:**
   ```yaml
   ---
   title: 'Quark''s Outlines: Topic Name'
   description: Short description here.
   tags:
     - python
     - programming
     - beginners
     - tutorial
   series: Quark's Outlines
   cover_image: https://files.catbox.moe/xxxxx.png
   published: true
   ---
   ```

3. **Push to main** - GitHub Action publishes to Dev.to

### Scheduling (Draft)

Set `published: false` to create a draft. Publish manually from Dev.to dashboard or set `published: true` and push.

### Secrets

- `DEVTO_API_KEY` - Dev.to API key (in GitHub repo secrets)

## File Structure

```
*.txt          - Article content (102-145)
*.ad.txt       - Ad copy for each article
*.png          - Article images
articles/      - Published markdown versions
python14_docs/ - Scraped Python 1.4 ref docs
```

## TODO

- [ ] Generate images for new articles (use existing .png style)
- [ ] Continue generating articles for remaining sections
- [ ] Publish to articles/ folder with frontmatter
