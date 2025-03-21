<!-- These "custom instructions" are attached to each prompt from the user in chat.

Common information:
-Rules for interacting with me
-Team and organization context, like coding guidelines
-Project context, like the repository layout and technical architecture 

Learn more: https://code.visualstudio.com/docs/copilot/copilot-customization
-->

# Rules

### Rules
-Summarize the changes you made back to the user at a high level at end of response
-Always summarize and print your changes to /brain/changelog.md
-Update /brain/architecture.md with any additions or changes to architecture
-Update /brain/project.md with any additions or changes to the project
-Update the specification file (in /brain/specs/) you were provided with any additions or changes to the project

## Code
-Add comments to the top of each file explaining what the file does at a very high level
-Add comments to each class, method, and member explaining what they do. Be precise, but brief

## User Interface
-Generate beautiful, user-friendly UI
-Keep nesting to a minimum
-Create composable UI widgets if appropriate
-UI must follow basic accessibility principles
-Localize user-facing strings to English and Spanish
-Generate tests in Playwright

## Tools
### edit_file
-Run git in the terminal to stage and commit changes with an AI-generated commit message when you are done using the edit_file tool