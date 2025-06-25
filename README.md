
# aider + chatGPT
### Copy context
1. open repo in terminal
2. copy file contents with path (make sure you use a [.gitignore!](https://github.com/github/gitignore/blob/main/Node.gitignore))

```
# macOS
git ls-files -z | xargs -0 -I {} sh -c 'echo "=== {} ==="; cat "{}"' | pbcopy 
```

```
# Linux  
git ls-files -z | xargs -0 -I {} sh -c 'echo "=== {} ==="; cat "{}"' | xclip -selection clipboard
```

```
# Windows
git ls-files | % { "=== $_ ==="; gc $_; "" } | scb
```
3. Paste into chatGPT / claude.ai
### Describe needed change / occuring bug
- Actual behaviour  
- Expected behaviour  
- Exact error / stack trace  
- Steps to reproduce

#### Style
- be precise and exhaustive
- more is more
- check spelling if using TTS (especially library names etc.)

### Review understanding / recommendations
- Did the LLM understand what the problem / required change is? 
	- clarify where needed
- Discuss possible solutions
	- "Propose alternatives and help me decide"
	- Adequate solution for scope? (Quick prototype / MVP / prod-ready?)
	- "You suggested X. Given our scope, is there a lighter alternative?"

### Get aider instructions
Make the LLM generate instructions for aider.
You can use the following prompt:

```
Based on our conversation above, prepare the aider context.

  

1. File list  

Return the paths of every *existing* repo file that aider must read, modify, import, or reference.  

Do **not** include files that will be newly created.

  

Output format: plain text — one path per line (no bullets, no comments).
If no existing files are needed, output a single blank line.
  

2. Task prompt (start after one blank line)  

• One-sentence overview of the change.  

• Up to 15 concise bullets with the key requirements.  

Be clear, high-level, and precise.

  

Respond **exactly** in this order:

  

<file-list>

(blank line)

<task prompt>
```

# Aider task preparation

## Gather context
 `/ask`
1. Describe the needed change / bug.
2. Request files list
	>- "For now, only give me a list of files that you need to see / edit, nothing else" 

## Kick-off generation
> - "Go ahead, implement"
