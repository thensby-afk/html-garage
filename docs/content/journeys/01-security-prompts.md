# Journey: Security Prompt Retrieval

## Purpose
Citizen developers need a checklist of security requirements before building or remediating an HTML tool. This journey gives them everything they need to brief an AI coding assistant for a compliant build.

## Actors

| Actor | Role |
|---|---|
| Citizen Developer | Retrieves and uses the prompt |
| HTML Garage | Displays the checklist |
| AI coding assistant (Claude, Copilot, etc.) | Applies the prompt to generate or remediate HTML |

## Steps

1. Developer navigates to the HTML Garage home screen.
2. Developer clicks **Security Prompts**.
3. The app displays a structured security prompt — a set of requirements covering all C1–C9 checks in natural language, formatted for direct use with an AI assistant.
4. Developer copies the prompt.
5. Developer opens their AI coding assistant and pastes the prompt, followed by their tool's code (or their build brief).
6. AI assistant generates or remediates the HTML tool against the requirements.
7. Developer receives the remediated HTML file.
8. Developer proceeds to the **Certify** journey to scan and register the tool.

## Key decision points

- **Tool already built vs. building from scratch.** The prompt works for both. For an existing tool, the developer pastes the current HTML after the prompt. For a new build, they describe the tool's purpose.
- **AI output passes scan immediately.** This is the expected path. Developer proceeds to Certify.
- **AI output fails scan.** Developer returns to the AI with the specific failure details from the scan report and iterates.

## Inputs and outputs

| | Description |
|---|---|
| **Input** | None — the prompt is generated and displayed by the app |
| **Output** | A security-compliant HTML file, ready for the Certify journey |

## Notes

The prompt is versioned with the app. When Tech Services updates the C1–C9 checks (e.g. to address a new threat), they redeploy the app with an updated prompt. Developers who retrieve the prompt after a redeployment automatically get the updated requirements.
