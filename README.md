# Vault Tech Logs

A **Markdown-only** daily work log system designed for software engineers to track tasks, learnings, and communications efficiently using VSCode and Copilot Chat.



## User flow:
- Copilot chat what you are working on, prefix with the category for better organization
    - example: "working on: fixed the bug with the login page TKET-1234"
- For images manually paste into the markdown file, the image will be inserted into the assets folder automatically (named by folder and timestamp)



## Updates required:
- find and replace `https://yourcompany.atlassian.net/browse/` with your actual Jira base URL wherever it appears in the files above.



## Pro Tips:
- Pretty rendered markdown by default (Command+Enter toggles between preview and edit modes)
    - follow setup in Vault-Tech-Logs/.vscode/keybindings.json
    - set markdown preview as primary view
        - right click a markdown file
        - Open With...
        - Configure default editor for '*.md'...
        - Select 'Markdown Preview'
- use git for local history to quickly rollback copilot chat changes (backup using your companies computer cloud storage if you are unable to push)







