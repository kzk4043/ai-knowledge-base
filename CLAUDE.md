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
Always reference `00_setting/user_profile.md` when processing content - this drives all prioritization and relevance decisions.

### Content Addition Process
1. Read user profile to understand current interests/skill levels
2. Analyze provided URLs against profile criteria
3. Present prioritized candidate list to user for confirmation
4. Generate summaries only for approved articles
5. Update appropriate category files
6. Log changes in CHANGELOG.md
7. Optionally update user profile based on feedback

### File Organization Rules
- Place content in appropriate numbered directories (10_, 20_, 30_, 40_)
- Use descriptive subdirectory names within categories
- Maintain consistent Markdown formatting per the defined template
- Add `.gitkeep` files to empty directories for version control

The system emphasizes **continuous profile improvement** - each interaction should potentially refine the user's profile for better future content curation.