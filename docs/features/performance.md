# Performance & Caching

Optimize performance for sites with thousands of files.

## Overview

PraisonPressGit includes intelligent caching and indexing systems to handle sites of any size efficiently.

## Caching System

### WordPress Transients

File content is cached using WordPress transients:

```php
// Configure cache TTL
add_filter('praison_cache_ttl', function($ttl, $post_type) {
    if ($post_type === 'lyrics') {
        return 7200; // 2 hours for lyrics
    }
    return $ttl;
}, 10, 2);
```

### Cache Invalidation

Cache automatically invalidates when:
- Files are modified
- Admin clears cache manually
- TTL expires

### Clear Cache

**Admin Dashboard:**
Click "Clear Cache" in the PraisonPress dashboard

**WP-CLI:**
```bash
wp cache flush
wp transient delete --all
```

## Index System

For large sites (1,000+ files), enable the index system:

### Build Index

```bash
# Generate index file
php wp-content/plugins/praisonpressgit/scripts/build-index.php
```

### Index Benefits

| Site Size | Without Index | With Index |
|-----------|---------------|------------|
| < 1,000 | 0.5s | 0.2s |
| 1,000 - 10,000 | 2-5s | 0.2s |
| 10,000 - 100,000 | 10-30s | 0.5-2s |

## Scaling Guide

### Small Sites (< 1,000 files)

```yaml
Performance: ~0.5s load time
Memory: ~50MB
Cache: WordPress transients
```

### Medium Sites (1,000 - 10,000 files)

```yaml
Performance: ~0.2s load time (5x faster)
Memory: ~80MB
Cache: Transients + Object cache
Index: Recommended
```

### Large Sites (10,000 - 100,000 files)

```yaml
Performance: ~0.5-2s load time (50x faster)
Memory: ~150MB
Cache: Redis/Memcached required
Index: Required
```

## Object Cache

For best performance, use Redis:

```php
// wp-config.php
define('WP_REDIS_HOST', 'redis-service');
define('WP_REDIS_PORT', 6379);
```

Install Redis Object Cache plugin:
```bash
wp plugin install redis-cache --activate
```
