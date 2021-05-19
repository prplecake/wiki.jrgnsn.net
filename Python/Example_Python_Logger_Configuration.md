---
title: Example Python Logger Configuration
---

```python
project_name = "" # your project, log file is named after this, see line 21
LOGGER_CONFIG = {
    'version': 1,
    'disable_existing_loggers': False,
    'formatters': {
        'default': {
            'format': '[%(asctime)s] - %(name)s - %(levelname)s - %(message)s'
        },
    },
    'handlers': {
        'console': {
            'class':        'logging.StreamHandler',
            'formatter':    'default',
            'level':        'INFO',
        },
        'file': {
            'class':        'logging.handlers.RotatingFileHandler',
            'formatter':    'default',
            'mode':         'a',
            'level':        'INFO',
            'filename':     'log/' + project_name + '.log',
            'maxBytes':     1024,
            'backupCount':  3
        },
    },
    'loggers': {
        '': {
            'level':    'DEBUG',
            'handlers': ['console', 'file'],
            'propagate': True
            },
        }
}
```