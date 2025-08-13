# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a WordPress website for Public Citizen running on a Local by Flywheel development environment with WP Engine hosting configuration. The site uses a custom theme called "Citizen" with Twig templating and extensive use of Advanced Custom Fields (ACF) for content management.

## Local Development Environment

This site is set up with Local by Flywheel:
- **Local URL**: Accessible through Local's interface
- **Web root**: `/public/` directory
- **Database**: MySQL via Local (credentials in `wp-config.php`)
- **Server stack**: Nginx + PHP-FPM + MySQL configured through Local's `conf/` directory

## Architecture Overview

### Core Technologies
- **WordPress**: Standard WordPress installation with custom theme
- **Twig Templating**: Custom theme uses Twig templates located in `wp-content/themes/citizen/_html/templates/`
- **Advanced Custom Fields Pro**: Extensive use of ACF for custom fields and flexible content
- **WP Engine**: Hosting-specific configurations and caching
- **Composer**: PHP dependency management for Twig and other packages

### Theme Structure
The main theme is `citizen` located at `wp-content/themes/citizen/`:
- **Templates**: Twig templates in `_html/templates/` with partials in `partials/`
- **PHP Functions**: Modular structure in `inc/` directory:
  - `core.php`: Main theme setup and WordPress functionality
  - `helper.php`: Helper functions
  - `types.php`: Custom post types
  - `acf.php`: ACF configurations
  - `misc.php`: Miscellaneous functions
  - Additional helpers for search, redirections, shortcodes
- **Assets**: CSS/JS in `assets/` directory
- **ACF JSON**: Field definitions stored in `acf-json/`

### Custom Post Types & Taxonomies
The site uses several custom post types managed through ACF and custom functions:
- Custom taxonomies including Justice taxonomy (ID: 118)
- Custom image sizes for responsive design (pc-250, pc-500, pc-1000, etc.)

### Key Plugins
- **Advanced Custom Fields Pro**: Core content management
- **Twig**: Template engine (via Composer)
- **WP Engine plugins**: Caching and hosting optimization
- **Security**: WP Defender, Force Strong Passwords
- **SEO**: Yoast SEO
- **Development**: Query Monitor for debugging
- **Media**: Enable Media Replace
- **Users**: User Role Editor Pro, Members
- **Various utility plugins**: TablePress, Redirection, Stream, etc.

## Development Commands

### Theme Development
- **CSS Version**: Defined as `CSS_VERSION = 'v22'` in core.php
- **Asset compilation**: No build process configured for main theme
- **Twig dependencies**: Managed via Composer in `_html/` directory

### WordPress Standard Operations
```bash
# Access WordPress admin
# Local site URL + /wp-admin/

# Database operations through Local by Flywheel interface
# Or directly via phpMyAdmin/Adminer through Local

# File permissions are managed by Local environment
# File system permissions: directories 775, files 664
```

### Plugin Management
- Most plugins are installed and managed through WordPress admin
- Some premium plugins may require manual updates
- WP Engine specific plugins handle caching and environment configurations

## Content Management

### ACF Integration
- Field groups stored as JSON in `wp-content/themes/citizen/acf-json/`
- Extensive use of flexible content fields
- Custom fields integrated with Twig templates

### Template System
- Twig templates in `_html/templates/`
- Modular partials system for reusable components
- Template inheritance using `core/base.twig`
- Custom macros in `core/macros.twig`

### Media Handling
- Custom image sizes for responsive design
- Media replacement capabilities via Enable Media Replace plugin
- Upload handling through WordPress media library

## Environment Configuration

### WP Engine Specifics
- **Cache**: WP_CACHE enabled with Memcached
- **CDN**: WPE CDN configuration in wp-config.php
- **Security**: SSL forced, file modifications controlled
- **Cron**: WP_CRON disabled (handled by WP Engine)
- **Revisions**: Limited to 5 per post

### Database Configuration
- Local development uses 'local' database
- MySQL configuration handled by Local environment
- UTF-8 charset with unicode collation

### Security Features
- Strong password enforcement via plugin
- WP Defender security monitoring
- File modification controls
- SSL/HTTPS enforcement

## Important File Locations

- **Main theme**: `wp-content/themes/citizen/`
- **Twig templates**: `wp-content/themes/citizen/_html/templates/`
- **ACF field definitions**: `wp-content/themes/citizen/acf-json/`
- **Plugin configurations**: `wp-content/plugins/`
- **Uploads**: `wp-content/uploads/`
- **Configuration**: `wp-config.php`
- **Local environment**: `conf/` directory for server configurations

## Deployment Notes

- Site configured for WP Engine hosting
- WP Engine specific constants and configurations in wp-config.php
- Domain mappings and CDN configurations included
- File permissions and security settings optimized for WP Engine