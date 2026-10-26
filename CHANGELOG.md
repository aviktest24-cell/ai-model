# Changelog

## 2.1.0 — Rate-limit fallback fix

- Added the anonymous-compatible fast model to the live model picker only when it is present in the live catalogue.
- Combined that option with up to four lightweight text models that currently have active community workers.
- Added route-aware generation so each selected model is sent to the API that supports its ID.
- Removed the obsolete GET retry path that could produce 404 errors for unsupported model IDs.
- On a fast-service HTTP 402, the app now tries available community models. If all backups fail, it waits for the reported cooldown (or 30 seconds if none is provided) and retries the supported POST route once.
- Kept the provider's name out of visible application status and error text.
- Updated model-picker descriptions for the fast option and clarified rate-limit behavior in the README.
