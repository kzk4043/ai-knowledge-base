# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## System Overview

This is a **技術情報キュレーションシステム** (Technical Information Curation System) - an AI-assisted system for efficiently collecting, organizing, and learning from technical articles and information sources.

### Core Architecture

The system follows a **profile-driven content curation approach**:

1. **User Profile Management** (`00_setting/user_profile.md`) - Central configuration defining:
   - Technical skill levels per domain
   - Interest areas with priority rankings  
   - Learning goals (short/medium/long term)
   - Areas needing improvement
   - Content exclusion criteria

2. **Content Analysis Workflow**:
   - URL input → Article analysis → Candidate prioritization → User confirmation → Summary generation → Profile learning

3. **Structured Knowledge Organization** - Hierarchical categorization:
   - `10_general/` - General technical topics (Git, reviews, management)
   - `20_frontend/` - Frontend technologies
   - `30_backend/` - Backend technologies  
   - `40_devops/` - DevOps and infrastructure

### Article Processing System

**Content Prioritization**: Articles are classified using a 3-tier importance system:
- 🔴 High - Critical and urgent information
- 🟡 Medium - Reference-worthy information  
- 🟢 Low - Future utility information

**Template Structure** for article summaries:
- Standardized metadata (URL, date, importance, tags)
- Structured content (overview, key points, details, code examples, related resources)

### Key Workflows

1. **Information Collection Flow**: Multi-URL processing with user confirmation before summarization
2. **Output Flow**: Category-based Markdown generation with change tracking in CHANGELOG.md  
3. **Continuous Learning Flow**: Profile refinement based on user feedback and interaction patterns

## Working with this Repository

### User Profile Configuration
Always reference `00_setting/user_profile.md` when processing content - this drives all prioritization and relevance decisions. The profile includes importance evaluation criteria such as prioritizing technologies that replace complex/unstable implementations with browser standards.

### URL Processing Workflow
Use `90_prompt/url_processing.md` as the standard template for processing technical articles:

1. **Content Analysis**: Read URLs and extract article information, including linked articles
2. **Profile Matching**: Analyze against user profile criteria and technical priorities
3. **Candidate Presentation**: Present prioritized list with 🔴🟡🟢 importance ratings and reasoning
4. **User Confirmation**: Wait for user selection before proceeding with summarization
5. **Structured Summarization**: Create standardized Markdown summaries with metadata, key points, and code examples
6. **Profile Feedback Loop**: Collect user feedback to refine future prioritization accuracy
7. **Repository Updates**: Update CHANGELOG.md and consider structural improvements

### Content Addition Process
- Read user profile to understand current interests/skill levels (React/TypeScript/Node.js focus)
- Analyze provided URLs against profile criteria including the preference for browser standard replacements
- Present prioritized candidate list to user for confirmation
- Generate summaries only for approved articles using the standard template
- Update appropriate category files within the numbered directory structure
- Log changes in CHANGELOG.md with version increments
- Collect feedback for continuous profile refinement

### File Organization Rules
- Place content in appropriate numbered directories (10_general/, 20_frontend/, 30_backend/, 40_devops/)
- Use descriptive subdirectory names within categories (frameworks/, concepts/, tools/)
- Maintain consistent Markdown formatting per the defined template structure
- Add `.gitkeep` files to empty directories for version control
- Consider structural optimization based on user profile evolution

### Repository Management
The system emphasizes **continuous profile improvement** and **structural optimization** - each interaction should potentially refine both the user's profile and the repository structure for better future content curation and accessibility.