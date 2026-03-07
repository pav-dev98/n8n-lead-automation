# n8n Lead Automation

Workflows for automatic thank-you messages on new Supabase leads (email/WhatsApp).

## Structure
- `workflows/` → All exported n8n workflows as .json
- `docker/`    → Docker Compose for production
- `credentials/` → (optional) anonymized credentials

## Development
1. Run local n8n: `npx n8n`
2. Build workflows in UI
3. Export to `workflows/` folder
4. Commit & push

## Production
Deploy via Docker Compose (Render, Railway, VPS, etc.)