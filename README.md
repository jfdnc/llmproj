# llmproj

Minimal, tab-delimited DSL for scaffolding software projects using LLMs.

## Usage

```bash
./llmproj build project.lp                 # Generate prompt to stdout
./llmproj build project.lp -o prompt.txt   # Save to file
./llmproj build project.lp --clipboard     # Copy to clipboard
./llmproj validate project.lp              # Validate syntax
./llmproj template [name]                   # Create template .lp file
```

## DSL Format

Files use `.lp` extension with tab-delimited sections:

```
project
	name: my-app
	description: Web application
	@git

environment
	platform: web
	runtime: node18+
	
dependencies
	no: react
	version:
		typescript@^5.0.0
		
structure
	src/
		components/
			stub: App.tsx
			skip: unused.ts
```

The CLI generates comprehensive prompts with DSL specifications, project details, and implementation guidelines for any LLM.

## Getting Started

Create a new project template:

```bash
./llmproj template                    # Creates template.lp
./llmproj template my-project         # Creates my-project.lp
```

The template includes all sections with commented examples and usage instructions.
