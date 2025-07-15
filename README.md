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

## DSL Sections

### project
Define your project's core identity and setup requirements.

**Directives:**
- `name:` - Project identifier
- `description:` - Brief project summary
- `explore:` - Generate analysis of project approaches and patterns
- `@git` - Initialize git repository
- `@file` - Include context from external files

**Example:**
```
project
	name: my-web-app
	description: Modern web application with user authentication
	explore: authentication patterns
	@git
	@file
		docs/requirements.md
		existing-api.json
```

### environment
Specify platform, runtime, and deployment configuration.

**Directives:**
- `platform:` - Target platform (web, ios, android, cli, desktop)
- `runtime:` - Runtime version (node18+, python3.9+, go1.20+)
- `deploy:` - Deployment target (vercel, aws, heroku, docker)
- `explore:` - Analyze environment and deployment options
- `@file` - Reference environment configuration files

**Example:**
```
environment
	platform: web
	runtime: node18+
	deploy: vercel
	explore: serverless vs container deployment
	@file
		.env.example
		docker-compose.yml
```

### dependencies
Manage package requirements and constraints.

**Directives:**
- `explore:` - Analyze dependency choices (general or specific topic)
- `auto:` - Let the LLM choose optimal dependencies
- `no:` - Exclude specific packages
- `version:` - Specify version constraints
- `@file` - Reference dependency configuration files

**Example:**
```
dependencies
	explore: testing frameworks
	auto: ui components
	no: jquery
	no: lodash
	version: typescript@^5.0.0
	version: react@^18.0.0
	@file
		package.json
		requirements.txt
```

### structure
Define file organization and generation hints.

**Directives:**
- `skip:` - Don't generate specified files/folders
- `stub:` - Create minimal implementations
- `explore:` - Analyze structure patterns and conventions
- `@file` - Reference structure documentation

**Example:**
```
structure
	src/
		components/
			stub: Button.tsx
			stub: Modal.tsx
		utils/
			skip: legacy.js
	skip: old-migrations/
	explore: component organization patterns
	@file
		docs/architecture.md
```

## Usage Patterns

### Exploration-Driven Development
Use `explore:` directives to understand options before making decisions:

```
dependencies
	explore: state management
	explore: testing
	
environment
	explore: deployment options
```

### Incremental Development
Use `stub:` for placeholder implementations:

```
structure
	src/
		auth/
			stub: login.ts
			stub: register.ts
		api/
			stub: client.ts
```

### Legacy Integration
Use `@file` to provide context about existing systems:

```
project
	@file
		legacy-api-docs.md
		current-schema.sql
```
