# CommitPulse
Monitor GitHub repositories and get AI-summarized commit notifications via WhatsApp using n8n.

## Overview

This n8n workflow monitors GitHub repositories for new commits and sends notifications via WhatsApp when changes are detected. The automation tracks both your public repositories and starred repositories, comparing commit history to identify new activity.

## Features

- Monitors public and starred repositories every minute
- Tracks commit history in a data table for comparison
- Detects new commits and changes in repositories
- Generates AI-powered summaries of commit changes
- Sends formatted notifications via WhatsApp

## Workflow Components

### Trigger
- **Schedule Trigger**: Runs every minute to check for repository updates

### Data Collection
- **Public Repos**: Fetches list of user's public repositories from GitHub API
- **Starred Repos**: Fetches list of user's starred repositories from GitHub API
- **Public + Starred**: Merges both repository lists for processing

### Data Processing
- **Repo Cleanup**: Extracts owner and repository name from repository data
- **Commit Request**: Fetches the latest commit for each repository
- **Map Commits**: Formats commit data with essential information (SHA, URL, message)

### Change Detection
- **Get Last Saved Commit**: Retrieves previously stored commit data from data table
- **New + Old Commits**: Combines current and historical commit data
- **Check Commits Diffs**: Compares commits to detect new changes and set notification flags
- **Save New Commits**: Updates data table with latest commit information

### Notification Generation
- **Filter**: Filters repositories that require notifications
- **Commit Info Request**: Fetches detailed commit information including file changes
- **Create Prompt**: Generates AI prompt with commit details and file changes
- **Create Message**: Uses Google Gemini AI to create concise commit summaries
- **Send Message**: Delivers notifications via WhatsApp

## Requirements

### Credentials
- GitHub API credentials (for repository and commit access)
- WhatsApp Business API credentials (for message delivery)
- Google Gemini API credentials (for AI summarization)

### Data Storage
- n8n Data Table for tracking commit history across executions

## Configuration

### Schedule
The workflow runs automatically every minute to check for repository updates.

### Repositories Monitored
- All public repositories for the configured GitHub user
- All repositories starred by the configured GitHub user

### Notification Criteria
- New repositories (previously untracked)
- Repositories with new commits (SHA mismatch)
- Commits with file changes

## Output

WhatsApp notifications include:
- Repository owner and name
- Committer information
- Concise summary of changes (AI-generated)
- Commit message and main modifications
- Direct link to the commit

## Data Privacy

Sensitive information including phone numbers and API credentials are stored securely in n8n's credential management system and are not exposed in the workflow configuration.

## Maintenance

The workflow automatically maintains commit history in the data table and only notifies on actual changes, preventing duplicate notifications for the same commits.

# License

This project is licensed under the MIT License. See [LICENSE](LICENSE)