# Heroku

## Restore database from a backup on another app

```sh
heroku pg:backups:restore --app <target_app> <source_app>::<id>
```
