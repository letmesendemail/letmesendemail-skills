# Installation

## Node.js

```bash
npm install @letmesendemail/letmesendemail-node
```

```typescript
import { LetMeSendEmail } from "@letmesendemail/letmesendemail-node";

const client = new LetMeSendEmail(process.env.LETMESENDEMAIL_API_KEY!);
```

## Python

```bash
pip install letmesendemail
```

```python
from letmesendemail import LetMeSendEmail

client = LetMeSendEmail(api_key=os.environ["LETMESENDEMAIL_API_KEY"])
```

Use as a context manager (`with LetMeSendEmail(...) as client:`) so connections close cleanly.

## PHP / Laravel

```bash
composer require letmesendemail/letmesendemail-php
composer require letmesendemail/letmesendemail-laravel  # Laravel integration
```

## API key

Create keys in the dashboard: user menu → API keys. Copy the full value shown once at creation (keys have no fixed prefix). Always load from the `LETMESENDEMAIL_API_KEY` environment variable — never hardcode.

More SDKs (Go, Java, Ruby, Rust, .NET) follow the same pattern: construct a client with the API key, call `client.emails.send(...)`. See each SDK's README for exact signatures.
