# Public Citizen Website Analysis & Findings

**Review Date:** August 13, 2025  
**Site:** https://citizen.org

## Executive Summary

Public Citizen's current website architecture suffers from **over-engineered categorization complexity** that creates significant administrative burden while limiting user experience and content discovery. The system shows classic signs of organic growth without strategic information architecture planning, resulting in a technically sophisticated but operationally burdensome content management system.

## Visual Documentation

This analysis includes comprehensive screenshots of the WordPress administrative interface that demonstrate the categorization complexity issues identified below:

- **Admin Dashboard**: `04_dashboard.png` - WordPress admin interface overview
- **Content Management Complexity**: 
  - `06_topic_listing.png` - Shows 91+ topics demonstrating over-categorization
  - `19_new_topic_creation.png` - Complex topic creation form with multiple required fields
  - `20_topic_edit_with_acf.png` - Advanced Custom Fields conditional logic in action
- **Taxonomy Management Burden**:
  - `13_tax_topic.png` - Main topics taxonomy
  - `14_tax_case_topic.png` - Case-specific topics taxonomy
  - `15_tax_supertag.png` - Custom supertag system
  - `16_tax_type.png` - Content type classifications
  - `17_tax_news.png` - News categorization system
- **Technical Complexity**: `18_acf_field_groups.png` - Advanced Custom Fields management

These visual examples provide concrete evidence of the administrative burden and categorization complexity detailed in this analysis.

## Current Technology Stack

### Core Platform
- **WordPress** with custom "Citizen" theme
- **Twig templating engine** for template structure
- **Advanced Custom Fields Pro** for extensive content management
- **WP Engine hosting** configuration with caching optimization

### Development Environment
- Extensive content database with years of historical content
- Extensive plugin ecosystem (20+ active plugins)
- Custom theme with modular PHP structure

## Content Architecture Analysis

### Custom Post Types (7 Total)
1. **Topic** - Main issue areas (e.g., "Protecting Democracy", "Justice & the Courts")
2. **Article** - In-depth content pieces with full editor support
3. **News** - News articles and commentary
4. **Litigation** - Legal cases and court documents  
5. **Person** - Staff and expert profiles (URL: `/about/person/`)
6. **Act** - Action items and campaigns
7. **Story** - Victory stories and case studies (URL: `/victories/story/`)
8. **Supertag** - Custom replacement for WordPress tags system

### Custom Taxonomies (6 Total)
1. **tax_topic** - Applied to: article, topic, news, act, litigation, post
2. **tax_case_topic** - Litigation-specific categorization
3. **tax_supertag** - Tag-like categorization system
4. **tax_type** - Article type classification
5. **tax_news** - News type classification  
6. **person_type** - Staff vs. board vs. experts classification

### URL Structure
- Topics: `/topic/{topic-name}/`
- Articles: `/article/{article-name}/`  
- News: `/news/{article-name}/`
- Litigation: `/litigation/{case-name}/`
- People: `/about/person/{person-name}/`
- Stories: `/victories/story/{story-name}/`
- Tags: `/tags/{tag-name}/`

## Critical Pain Points Identified

### 1. Administrative Complexity
**Issue:** Content creators face overwhelming categorization requirements

*Visual Evidence: See `06_topic_listing.png` showing 91+ topics, and `19_new_topic_creation.png` demonstrating complex creation interface*

- **7 different post types** with varying field requirements
- **Multiple overlapping taxonomies** create confusion about which to use  
- **Required ACF fields with conditional logic** make content creation rigid (see `20_topic_edit_with_acf.png`)
- **91+ topic categories** visible in admin interface create choice paralysis
- No clear content creation guidelines visible in WordPress admin

**Example:** Creating a "Justice and Courts" topic requires:
- Selecting appropriate post type (topic)
- Setting conditional ACF field "Justice and the Courts" = true  
- This automatically switches taxonomy requirements from `tax_topic` to `tax_case_topic`
- Understanding that this "glues" the topic to the correct taxonomy term
- Navigating through 5+ separate taxonomy management screens (see `13-17_tax_*.png`)

### 2. Rigid Content Relationships
**Issue:** Inflexible content associations limit editorial workflow

*Visual Evidence: See `18_acf_field_groups.png` showing complex field group management and `20_topic_edit_with_acf.png` for conditional logic examples*

- **Forced taxonomy relationships** via required ACF fields
- **No many-to-many content relationships** - content can't naturally exist in multiple topic areas
- **Hierarchical complexity** across different content types  
- **Conditional ACF logic** creates brittle dependencies
- **15+ ACF field groups** managing complex content relationships

**Technical Example:**
```json
{
  "conditional_logic": [
    [
      {
        "field": "field_5c8c0f53963b0",
        "operator": "==", 
        "value": "1"
      }
    ]
  ]
}
```

### 3. User Experience Limitations
**Issue:** Poor content discovery and navigation
- **Siloed content types** with limited cross-referencing
- **Basic search functionality** without advanced filtering
- **Topic pages lack sophisticated filtering** options
- **No faceted search** or multiple criteria browsing
- **Limited content cross-linking** between related items

**Front-end Observations:**
- Main topics visible on homepage but not fully exploited
- Content discovery relies heavily on main topic landing pages
- No apparent filtering by content type, date, or multiple topics
- Search results appear basic without advanced categorization options

### 4. Technical Debt & Maintenance Issues
**Issue:** Complex architecture creates ongoing maintenance burden

*Visual Evidence: Admin interface screenshots demonstrate the scope of technical complexity*

- **Over-engineered taxonomy system** with 6 separate taxonomies requiring deep system knowledge
- **Theme heavily dependent** on specific ACF field structures (see `18_acf_field_groups.png`)
- **Conditional logic dependencies** make changes risky (demonstrated in `20_topic_edit_with_acf.png`)
- **91+ topic categories** indicating potential redundancy and maintenance overhead
- **Limited flexibility** for adapting to new organizational needs

## Database Analysis Findings

### Content Volume
- **Extensive historical content** dating back to 2008
- **Heavy reliance on custom fields** for content relationships
- **Complex metadata structures** supporting taxonomy system
- **Large number of taxonomy terms** indicating rich but potentially redundant categorization

### Content Distribution
Based on URL rewrite rules analysis:
- **Topics**: Primary organizational structure
- **Articles**: High-volume content type with editor support
- **News**: Historical content with date-based organization  
- **Litigation**: Specialized content with case-specific categorization
- **People**: Staff/expert profiles with type-based classification

## Live Site User Experience Assessment

### Navigation Strengths
- Clear main topic areas on homepage
- Logical URL structure for SEO
- Topic-based organization aligns with organizational structure

### Navigation Weaknesses  
- **Limited content filtering** on topic pages
- **No cross-topic content surfacing**
- **Basic search without advanced options**
- **Siloed content types** don't interconnect well
- **Topic hierarchies not fully exposed** to users

### Content Discovery Issues
- Difficult to find related content across different post types
- No ability to browse by multiple criteria simultaneously
- Limited cross-referencing between news, articles, and litigation
- Victory stories disconnected from related ongoing work

## Recommendations for Rebuild

### 1. Simplify Information Architecture
- **Reduce to 3-4 core content types**: Articles, News, People, Resources
- **Implement flexible tagging system** vs. rigid taxonomies
- **Create intuitive topic/issue area structure** without forced relationships
- **Enable natural many-to-many relationships** between content and topics

### 2. Improve Content Management Workflow
- **Streamline content creation** with fewer required fields
- **Remove conditional ACF logic** dependencies
- **Implement content templates** for consistent structure
- **Create clear editorial guidelines** and workflows

### 3. Enhance User Experience
- **Implement faceted search and filtering** across all content types
- **Create dynamic topic pages** with multiple content type integration
- **Improve content discovery** with related content suggestions
- **Enable multiple criteria browsing** (topic + content type + date range)

### 4. Technical Architecture Improvements
- **Modern WordPress block editor** integration for flexibility
- **Simplified custom field structure** for maintainability
- **Performance optimization** for large content volumes
- **Mobile-first responsive design** improvements

## Migration Considerations

### Content Preservation
- **Historical content** (2008-present) must be preserved
- **URL structure** should maintain SEO value where possible
- **Taxonomy mapping** strategy needed for existing categorization
- **Media files and documents** require systematic migration

### Technical Migration Path
- **Content audit and cleanup** of redundant/outdated material
- **Taxonomy consolidation** mapping current 6 taxonomies to simplified structure
- **ACF field migration** to block editor or simplified custom fields
- **Template rebuilding** with modern WordPress standards

## Conclusion

The current Public Citizen website represents a classic case of technical sophistication that has grown beyond practical usability. While the system demonstrates deep organizational knowledge and content relationships, it has become a barrier to both content creators and end users.

**Visual evidence from the WordPress administrative interface clearly demonstrates:**
- 91+ topic categories creating choice paralysis for content creators
- Complex, multi-step content creation workflows with conditional field requirements  
- 6 separate taxonomy management systems requiring specialized knowledge
- 15+ ACF field groups managing intricate content relationships

A strategic rebuild focused on **simplified information architecture**, **flexible content relationships**, and **improved user experience** would significantly enhance the organization's digital presence while reducing ongoing maintenance burden.

The foundation is strong - extensive content, clear organizational structure, and sophisticated hosting infrastructure. The challenge is architecting a system that serves the content and users rather than constraining them.

---

*This analysis includes comprehensive visual documentation of the administrative interface to demonstrate the scope and impact of the categorization complexity issues identified.*