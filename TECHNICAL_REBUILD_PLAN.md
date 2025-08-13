# Public Citizen Website Technical Rebuild Plan

**Project Type:** Architecture Rebuild with Design Preservation  
**Hosting Provider:** WP Engine (maintained)  
**Development Approach:** Staging Environment with Phased Migration  
**Target Technology Stack:** Bricks Builder + Core Framework + Advanced Themer + ACF Pro

---

## Executive Summary

This technical plan outlines the complete rebuild of the Public Citizen website to address over-engineered content categorization complexity while preserving the current visual design. The rebuild will simplify the content architecture from 7 custom post types and 6 taxonomies to a streamlined 4 post type system with flexible categorization, significantly improving the content management experience.

**Key Metrics from Live Site Analysis:**
- **Total Content Items:** 21,492 posts across all custom post types
- **Users to Migrate:** 88 users with custom role structure
- **Taxonomies to Consolidate:** 6 current → 2-3 simplified
- **Active Plugins:** 41 total (33 regular + 8 must-use/dropins)

---

## Current Site Analysis (Live Data)

### Content Distribution
Based on WP-CLI analysis of live site (`pcitizen@pcitizen.ssh.wpengine.net`):

| Post Type | Count | Migration Priority | Target Consolidation |
|-----------|-------|-------------------|---------------------|
| **News** | 15,144 | Phase 2 | → Articles (News Category) |
| **Articles** | 4,720 | Phase 1 | → Articles |
| **Litigation** | 1,142 | Phase 4 | → Resources (Legal Category) |
| **Acts** | 190 | Phase 3 | → Articles (Action Category) |
| **People** | 140 | Phase 3 | → People |
| **Topics** | 91 | Phase 4 | → Remove (convert to categories) |
| **Stories** | 47 | Phase 3 | → Articles (Victory Category) |
| **Supertags** | 18 | Phase 4 | → Remove (convert to tags) |

### Current Taxonomy Structure
| Taxonomy | Terms | Applied To | Migration Strategy |
|----------|-------|------------|-------------------|
| **tax_topic** | 79 | article, topic, news, act, litigation, post | → Categories |
| **tax_case_topic** | 34 | article, litigation, topic, news | → Categories (Legal) |
| **tax_supertag** | 18 | supertag, article, act, news | → Tags |
| **tax_type** | 4 | article | → Categories |
| **tax_news** | 5 | news | → Categories |
| **person_type** | 4 | person | → Custom Field |

### User Structure
- **Total Users:** 88
- **Custom Roles Identified:** policy_author, policy_editor, organizer, litigation_editor, comms_intern
- **Migration Required:** All users with role mapping to simplified structure

---

## New Architecture Design

### Simplified Post Type Structure (4 Total)

#### 1. **Articles** (Consolidated from: articles, news, acts, stories)
- **Purpose:** All written content including news, opinion pieces, action items, and victory stories
- **Categorization:** Flexible categories (Policy, News, Actions, Victories, etc.)
- **ACF Fields:** 
  - Content type selector (News, Opinion, Action, Victory)
  - Publication date
  - Related resources (optional)
  - Featured image and media gallery

#### 2. **Resources** (Consolidated from: litigation, documents)
- **Purpose:** Legal cases, policy documents, research reports, downloadable materials
- **Categorization:** Resource type categories (Legal Cases, Policy Documents, Research, etc.)
- **ACF Fields:**
  - Resource type
  - Document attachments
  - Related legal topics
  - Case status (for legal resources)

#### 3. **People** (Maintained)
- **Purpose:** Staff, board members, experts, guest contributors
- **Categorization:** Simple categories (Staff, Board, Experts, Contributors)
- **ACF Fields:**
  - Position/title
  - Bio and photo
  - Contact information
  - Areas of expertise

#### 4. **Pages** (WordPress Default)
- **Purpose:** Static content like About, Contact, Topic landing pages
- **Categorization:** Minimal taxonomy usage
- **ACF Fields:** Flexible content builder for custom layouts

### Simplified Taxonomy Structure (2-3 Total)

#### 1. **Content Categories** (Replaces: tax_topic, tax_case_topic, tax_type, tax_news)
- **Hierarchical:** Yes
- **Applied To:** Articles, Resources, Pages
- **Structure:**
  ```
  Policy Areas
  ├── Democracy & Voting
  ├── Healthcare
  ├── Consumer Protection
  ├── Climate & Environment
  ├── Justice & Courts
  └── Corporate Accountability
  
  Content Types
  ├── News & Commentary
  ├── Action Items
  ├── Victory Stories
  ├── Research & Reports
  └── Legal Cases
  ```

#### 2. **Content Tags** (Replaces: tax_supertag)
- **Hierarchical:** No
- **Applied To:** Articles, Resources
- **Purpose:** Flexible cross-referencing and content discovery

#### 3. **Person Categories** (Optional - may use ACF field instead)
- **Applied To:** People only
- **Values:** Staff, Board, Experts, Contributors

---

## Technology Stack Implementation

### Core Platform: Bricks Builder + Core Framework + Advanced Themer

#### **Bricks Builder** (Primary Theme)
- **Role:** Visual page builder and theme system
- **Benefits:** 
  - Clean code generation
  - ACF Pro deep integration via Dynamic Data
  - Query Loop Builder for custom post type displays
  - Responsive design with custom breakpoints
  - Template system for consistent layouts

#### **Core Framework** (CSS Architecture)
- **Role:** Unified CSS framework and design system
- **Benefits:**
  - Maintains current visual design through preserved CSS variables
  - Provides utility classes for consistent styling
  - Visual component editor for design modifications
  - Modular CSS approach for maintainability

#### **Advanced Themer** (Development Enhancement)
- **Role:** Productivity and functionality enhancement for Bricks
- **Benefits:**
  - 179 additional features for Bricks Builder
  - Advanced color management and CSS variables
  - AI integration for content generation
  - Strict editor controls for client content management
  - Dynamic data helpers for complex content relationships

#### **ACF Pro** (Content Management)
- **Role:** Custom field management and content structure
- **Benefits:**
  - Simplified field groups (32 current → ~8-10 optimized)
  - Flexible content layouts
  - Conditional logic where truly needed (minimal usage)
  - Local JSON for version control

---

## Design Preservation Strategy

### CSS Migration Approach
The current site uses a sophisticated CSS architecture that must be preserved:

**Current CSS Structure Analysis:**
- **CSS Variables:** Extensive use of custom properties for theming
- **Component-Based Classes:** Modular styling (.nav1, .header1, .footer1)
- **Responsive Breakpoints:** 
  - Large: 1280px+
  - Medium: 720px-1279px
  - Small: <719px
  - Extra Small: <359px

**Migration Strategy:**
1. **Extract Core Framework Variables:** Map existing CSS variables to Core Framework system
2. **Component Recreation:** Rebuild current components in Bricks Builder using preserved styles
3. **Responsive Mapping:** Configure Bricks breakpoints to match current responsive behavior
4. **Visual QA Process:** Side-by-side comparison of each page/component during development

### Design System Documentation
Create comprehensive design system documentation including:
- Color palette mapping
- Typography scale preservation
- Component library in Bricks
- Spacing and layout patterns
- Interactive element behaviors

---

## Development Environment Setup

### WP Engine Staging Strategy

#### **Phase 1: Environment Preparation**
1. **Create Clean Staging Environment**
   ```bash
   # WP Engine staging environment creation
   # New WordPress installation with clean database
   ```

2. **Install Core Technology Stack**
   ```bash
   # Install licensed plugins
   - Bricks Builder (licensed)
   - Core Framework Bricks plugin (€119)
   - Advanced Themer (starting at $59)
   - ACF Pro (existing license)
   ```

3. **Basic Configuration**
   - Configure WP Engine settings
   - Set up SSL and security
   - Install essential development tools

#### **Phase 2: Architecture Implementation**
1. **Register New Post Types and Taxonomies**
2. **Create ACF Field Groups** (simplified structure)
3. **Import Core Framework CSS Variables** (from current site)
4. **Build Base Templates** in Bricks Builder

---

## Content Migration Strategy

### Migration Tools and Scripts

#### **Primary Tool: WP-CLI + Custom Scripts**
```bash
# Base WP-CLI commands for content export/import
wp export --dir=/tmp/migration --skip_comments
wp import /tmp/migration/content.xml --authors=create
```

#### **Custom Migration Scripts Required**
Due to the architectural changes, custom PHP scripts will be needed:

1. **Content Type Mapping Script**
   ```php
   // Map old post types to new structure
   $mapping = [
       'news' => 'article',
       'act' => 'article', 
       'story' => 'article',
       'litigation' => 'resource',
       'topic' => 'delete', // Convert to categories
       'supertag' => 'delete' // Convert to tags
   ];
   ```

2. **Taxonomy Consolidation Script**
   ```php
   // Map old taxonomies to new categories
   $taxonomy_mapping = [
       'tax_topic' => 'content_categories',
       'tax_case_topic' => 'content_categories',
       'tax_type' => 'content_categories',
       'tax_news' => 'content_categories'
   ];
   ```

3. **ACF Field Migration Script**
   ```php
   // Migrate and simplify ACF field data
   // Remove conditional logic dependencies
   // Consolidate related fields
   ```

### Phased Migration Approach

#### **Phase 1: Foundation (Week 1-2)**
**Target:** Core pages and simple articles (no complex taxonomy relationships)

**Content Scope:**
- WordPress pages (About, Contact, etc.)
- ~500 simple articles without complex categorization
- Basic media files

**Migration Process:**
1. Export foundation content with WP-CLI
2. Import to staging environment
3. Map basic categorization
4. Template creation and testing

**Success Criteria:**
- All pages load correctly
- Basic navigation functional
- CSS preservation verified
- Internal UAT passed

#### **Phase 2: News Content (Week 3-4)**
**Target:** News articles with moderate complexity (15,144 items)

**Content Scope:**
- All news posts → Articles with "News" category
- Associated media and attachments
- Author attribution preservation

**Migration Process:**
1. Batch export news content (groups of 1000)
2. Apply content type mapping (news → article)
3. Apply category mapping (tax_news → content_categories)
4. Import with relationship preservation

**Custom Development Required:**
- News archive page template
- Category filtering functionality
- Search integration

**Success Criteria:**
- News content accessible and properly categorized
- Archive pages functional
- Search returns accurate results
- Client UAT approval

#### **Phase 3: People and Action Content (Week 5-6)**
**Target:** People profiles, action items, victory stories

**Content Scope:**
- People (140 items) → People post type
- Acts (190 items) → Articles with "Action" category
- Stories (47 items) → Articles with "Victory" category

**Migration Process:**
1. People: Direct migration with person_type → custom field mapping
2. Acts: Content type conversion with category assignment
3. Stories: Content type conversion with victory category

**Custom Development Required:**
- People directory template
- Action item display components
- Victory story showcase layouts

#### **Phase 4: Complex Content (Week 7-8)**
**Target:** Litigation, topics, and supertags

**Content Scope:**
- Litigation (1,142 items) → Resources with "Legal" category
- Topics (91 items) → Convert to categories/navigation
- Supertags (18 items) → Convert to tags

**Migration Process:**
1. Litigation → Resources with legal case metadata preservation
2. Topics analysis → Create navigation structure and category mapping
3. Supertags → Tag conversion with content association preservation

**Custom Development Required:**
- Legal case display templates
- Advanced filtering for legal resources
- Topic-based navigation system

#### **Phase 5: Finalization and Content Sync (Week 9-10)**
**Target:** Final content validation and delta migration

**Content Scope:**
- Content created during development period
- Final relationship validation
- User account migration
- Search and navigation testing

**Migration Process:**
1. Content freeze date implementation
2. Delta content identification and migration
3. User migration with role mapping
4. Final testing and validation

---

## Plugin Analysis and Recommendations

### Current Plugin Ecosystem (41 Total)

#### **Essential Plugins to Migrate**

| Current Plugin | Status | Migration Recommendation | Notes |
|---------------|--------|--------------------------|-------|
| **advanced-custom-fields-pro** | Keep | ✅ Direct migration | Core functionality |
| **defender-security** | Keep | ✅ Direct migration | WP Engine security |
| **enable-media-replace** | Keep | ✅ Direct migration | Editorial workflow |
| **query-monitor** | Keep | ✅ Development only | Remove before production |
| **redirection** | Keep | ✅ Direct migration | SEO preservation |
| **wordpress-seo** | Keep | ✅ Direct migration | SEO essential |
| **user-role-editor** | Keep | ✅ Direct migration | User management |

#### **Plugins to Replace**

| Current Plugin | Replace With | Reason | Implementation Notes |
|---------------|--------------|--------|---------------------|
| **classic-editor** | Remove | Bricks Builder eliminates need | Full visual editing |
| **tablepress** | **Bricks Table Element** | Better integration | Rebuild existing tables |
| **header-footer-code-manager** | **Bricks Template System** | Native functionality | Migrate custom code |
| **widgetize-pages-light** | **Bricks Dynamic Content** | Modern approach | Rebuild page layouts |

#### **Specialty Plugins Analysis**

| Current Plugin | Keep/Remove | Migration Strategy |
|---------------|-------------|-------------------|
| **acf-code-field** | Remove | Replace with Bricks Code element |
| **acf-table-field** | Remove | Use Bricks table components |
| **acf-theme-code** | Remove | Not needed with Bricks |
| **us-map** (multiple versions) | Consolidate | Keep one version, remove others |
| **mapsvg** | Evaluate | Assess if still needed |
| **interactive-us-map** | Remove | Duplicate functionality |

#### **WP Engine Specific (Must-Use)**
All WP Engine must-use plugins will be preserved:
- slt-force-strong-passwords
- wpe-cache-plugin  
- wpe-wp-sign-on-plugin
- wpengine-security-auditor
- mu-plugin
- wpe-update-source-selector

---

## Custom Development Requirements

### Required Custom Functionality

#### **1. Content Migration Scripts**
**Location:** `/wp-content/themes/rebuild-migration/`
```php
// Required custom scripts:
- content-type-mapper.php
- taxonomy-consolidator.php  
- acf-field-migrator.php
- user-role-mapper.php
- media-attachment-updater.php
```

#### **2. Bricks Template Components**
**Custom elements needed:**
- News article listing with advanced filtering
- People directory with expertise filtering
- Legal case database with search functionality
- Action item showcase with status tracking
- Victory story timeline display

#### **3. Advanced Search Integration**
```php
// Custom search functionality for consolidated content
- Multi-post-type search
- Category and tag filtering
- Date range filtering
- Content type specific results
```

#### **4. Navigation and Menu Systems**
```php
// Dynamic navigation based on new category structure
- Topic-based mega menu
- Breadcrumb system for new hierarchy
- Related content suggestions
- Content cross-referencing
```

#### **5. User Role and Permissions**
```php
// Simplified role structure mapping
$role_mapping = [
    'policy_author' => 'contributor',
    'policy_editor' => 'editor', 
    'organizer' => 'editor',
    'litigation_editor' => 'editor',
    'comms_intern' => 'contributor'
];
```

### Development Timeline

| Week | Focus Area | Deliverables |
|------|------------|--------------|
| **1-2** | Environment + Foundation | Staging site, basic templates, Phase 1 content |
| **3-4** | News Migration | News content migrated, archive templates |
| **5-6** | People + Actions | People directory, action/victory templates |
| **7-8** | Complex Content | Legal resources, topic navigation |
| **9-10** | Finalization | User migration, final testing, go-live prep |

---

## Content Continuity and Freeze Strategy

### Content Management During Development

#### **Content Freeze Date Strategy**
1. **Announce Freeze Date:** 2 weeks before migration begins
2. **Content Tracking Period:** All content created after freeze date must be documented
3. **Delta Migration:** Final sync of new content before go-live

#### **Content Tracking Methodology**
```bash
# WP-CLI scripts for tracking new content
wp post list --post_status=publish --after="2025-XX-XX" --format=csv > new_content.csv
wp post list --post_status=publish --modified_after="2025-XX-XX" --format=csv > modified_content.csv
```

#### **Editorial Workflow During Development**
1. **Content Creator Documentation:** Track all new content with post IDs
2. **Editorial Review:** Weekly review of new content for migration priority
3. **Final Sync Process:** Batch migration of tracked content before launch

### User Account Migration

#### **User Export/Import Process**
```bash
# Export users with custom fields and role data
wp user list --format=json > users_backup.json

# Import users to new site with role mapping
wp user import-csv users_migrated.csv --send-email=false
```

#### **Role Simplification Strategy**
```php
// Map current complex roles to simplified structure
$new_roles = [
    'administrator' => 'administrator', // No change
    'policy_author' => 'contributor',   // Content creation only
    'policy_editor' => 'editor',        // Content management
    'organizer' => 'editor',            // Content management  
    'litigation_editor' => 'editor',    // Content management
    'comms_intern' => 'contributor'     // Content creation only
];
```

---

## Testing and Quality Assurance

### UAT Process Structure

#### **Internal UAT (Development Team)**
**Duration:** 1 week per phase
**Focus Areas:**
- Functionality testing
- Performance validation
- Cross-browser compatibility
- Mobile responsiveness
- Content accuracy

**Testing Checklist:**
- [ ] All migrated content displays correctly
- [ ] Search functionality works across content types
- [ ] Navigation and filtering systems functional
- [ ] Forms and interactive elements working
- [ ] SEO metadata preserved
- [ ] Page load performance acceptable (<3 seconds)

#### **Client UAT (Public Citizen Team)**
**Duration:** 1 week per phase
**Focus Areas:**
- Content accuracy and completeness
- Editorial workflow testing
- User role functionality
- Content creation process
- Public-facing experience

**Client Testing Scenarios:**
1. **Content Manager Test:** Create new article with proper categorization
2. **Editor Test:** Review and publish content through workflow
3. **Public User Test:** Browse site and use search functionality
4. **Mobile User Test:** Access content on mobile devices

### Performance and SEO Validation

#### **Performance Targets**
- **Page Load Speed:** <3 seconds for all pages
- **Core Web Vitals:** Green scores across all metrics
- **Mobile Performance:** 90+ PageSpeed score
- **Accessibility:** WCAG 2.1 AA compliance

#### **SEO Preservation**
- **URL Structure:** Maintain existing URLs where possible
- **Meta Data:** Preserve all SEO metadata
- **Internal Linking:** Maintain content relationships
- **Schema Markup:** Implement structured data
- **Sitemap Generation:** Automated XML sitemaps

---

## Risk Mitigation and Rollback Strategy

### Identified Risks and Mitigation

#### **Risk 1: Content Loss During Migration**
**Mitigation:**
- Complete database backups before each phase
- Staged migration with validation checkpoints
- Content verification scripts for accuracy checking

#### **Risk 2: SEO Impact from URL Changes**
**Mitigation:**
- Comprehensive 301 redirect mapping
- URL structure preservation where possible
- Search console monitoring during transition

#### **Risk 3: User Adoption Challenges**
**Mitigation:**
- Comprehensive user training documentation
- Simplified content creation workflows
- Gradual rollout with feedback collection

#### **Risk 4: Performance Degradation**
**Mitigation:**
- Performance testing at each phase
- WP Engine optimization implementation
- Caching strategy optimization

### Rollback Procedures

#### **Phase-Level Rollback**
```bash
# Database rollback for specific migration phase
wp db restore backup_pre_phase_X.sql

# Content rollback to previous state
wp post delete --post_type=article --after="phase_start_date" --force
```

#### **Complete Site Rollback**
- **Database Restoration:** Full database restore from pre-migration backup
- **File System Restoration:** WordPress files and uploads restoration
- **DNS Management:** Revert to original site if domain cutover completed

---

## Go-Live and Launch Strategy

### Pre-Launch Checklist

#### **Technical Validation**
- [ ] All content migration phases completed and approved
- [ ] User accounts migrated and tested
- [ ] Search functionality validated
- [ ] Performance targets achieved
- [ ] Security scanning completed
- [ ] Backup systems confirmed

#### **Content Validation**
- [ ] All URLs redirect properly
- [ ] SEO metadata preserved
- [ ] Images and media files accessible
- [ ] Forms and interactive elements functional
- [ ] Cross-content relationships maintained

### Launch Day Process

#### **Step 1: Final Content Sync** (T-2 hours)
```bash
# Final delta migration of content created during development
wp import final_content_delta.xml --authors=skip
```

#### **Step 2: DNS Cutover** (T-1 hour)
- Update DNS records to point to new staging environment
- Monitor for propagation across global DNS

#### **Step 3: Post-Launch Monitoring** (T+0 to T+24 hours)
- Real-time monitoring of site performance
- Error log monitoring
- User feedback collection
- Search console monitoring for SEO impact

### Post-Launch Support Plan

#### **Week 1: Intensive Monitoring**
- Daily performance and error monitoring
- User feedback collection and rapid response
- Content creation workflow support
- Search and navigation behavior analysis

#### **Week 2-4: Optimization Period**
- Performance optimization based on real usage data
- User training and workflow refinement
- Content organization improvements
- SEO monitoring and adjustment

#### **Month 2-3: Stabilization**
- Monthly performance reviews
- Content management workflow optimization
- User satisfaction assessment
- Long-term maintenance planning

---

## Maintenance and Future Considerations

### Ongoing Maintenance Requirements

#### **Technical Maintenance**
- **Plugin Updates:** Quarterly review and testing of Bricks, Core Framework, Advanced Themer updates
- **WordPress Core Updates:** Monthly core updates with staging testing
- **Performance Monitoring:** Continuous monitoring with monthly optimization reviews
- **Security Updates:** Immediate security patches with WP Engine coordination

#### **Content Management**
- **User Training:** Quarterly training sessions for new content creation workflows
- **Content Audit:** Annual content audit and optimization
- **SEO Monitoring:** Monthly SEO performance reviews and optimization
- **User Feedback Integration:** Ongoing workflow improvements based on editor feedback

### Future Enhancement Opportunities

#### **Phase 2 Enhancements (6-12 months post-launch)**
- Advanced content personalization
- Enhanced search with AI-powered recommendations
- Interactive content features
- Advanced analytics and content performance tracking

#### **Integration Possibilities**
- CRM integration for member management
- Email marketing platform integration
- Social media automation
- Advanced form and survey capabilities

---

## Conclusion

This technical rebuild plan provides a comprehensive roadmap for transforming the Public Citizen website from its current over-engineered state to a streamlined, maintainable, and user-friendly content management system. By consolidating 7 post types into 4 and 6 taxonomies into 2-3, while preserving the visual design through Core Framework integration, the rebuild will significantly improve content creator experience while maintaining the site's professional appearance and functionality.

The phased migration approach minimizes risk while ensuring content continuity, and the combination of Bricks Builder, Core Framework, and Advanced Themer provides a robust foundation for future growth and enhancement.

**Key Success Metrics:**
- **Content Management Efficiency:** 50% reduction in time required for content creation and categorization
- **System Maintainability:** 70% reduction in ACF field complexity and conditional logic
- **User Satisfaction:** 90%+ approval rating from content creators during UAT
- **Performance Preservation:** Maintain or improve current site performance metrics
- **SEO Preservation:** Zero negative impact on search rankings during transition

This rebuild positions Public Citizen for more efficient content management, reduced technical debt, and improved scalability for future organizational needs.