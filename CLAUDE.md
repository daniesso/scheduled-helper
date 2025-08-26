# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Python-based scheduled helper that uses OpenAI's GPT-5-nano model with web search capabilities to find positive news articles from Norway. It runs automatically every 15 minutes via GitHub Actions and saves results as JSON artifacts.

## Architecture

- **news_search.py**: Main script containing news search logic with OpenAI Responses API integration
- **GitHub Actions workflow**: `.github/workflows/hourly-news-search.yml` handles automated execution
- **Output format**: Results saved as timestamped JSON files with URLs, metadata, and usage statistics

## Key Components

### Main Script (`news_search.py`)
- Uses OpenAI Responses API with `gpt-5-nano` model
- Implements web_search_preview tool with location context for Trondheim, Norway
- Contains retry logic with exponential backoff (3 attempts max)
- URL validation and extraction from response text
- Error handling with structured JSON output

### GitHub Actions Workflow
- Scheduled execution every 15 minutes (`*/15 * * * *` cron)
- Manual dispatch with optional debug mode
- Python 3.12 environment with pip caching
- Artifact upload for results and logs
- Environment validation for API keys

## Dependencies

- `openai>=1.3.0` - OpenAI Python client
- `requests>=2.31.0` - HTTP library

## Development Commands

### Running Locally
```bash
# Install dependencies
pip install -r requirements.txt

# Set environment variable
export OPENAI_API_KEY="your-api-key"

# Run the news search script
python news_search.py
```

### Testing GitHub Actions
- Manual trigger: Use GitHub Actions tab with optional debug mode
- Check workflow logs for execution details
- Download artifacts containing results and logs

## Configuration

The script is configured for:
- Location: Trondheim, Norway
- Search context: Low (for efficiency) 
- Text verbosity: Low
- Reasoning effort: Minimal
- Output: 1 positive Norwegian news URL per run

## Output Files

- `news_results_latest.json` - Latest search results (overwritten each run)
- `news_results_YYYYMMDD_HHMMSS.json` - Timestamped results archive
- GitHub Actions artifacts with 30-day retention

## Environment Requirements

- `OPENAI_API_KEY` - Required GitHub repository secret for API access
- Python 3.12+ runtime environment