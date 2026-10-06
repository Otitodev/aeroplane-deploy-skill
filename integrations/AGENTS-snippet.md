## Deploying to Aeroplane

This project deploys to a self-hosted Aeroplane server. Before deploying, setting up a server, adding env vars or domains, or debugging a failed deployment, read `PATH/TO/aeroplane-deploy/SKILL.md` and follow it. It points to the reference files it needs.

- Connection details come from the `AEROPLANE_URL` and `AEROPLANE_API_KEY` environment variables. Never print or commit the key.
- Use `PATH/TO/aeroplane-deploy/scripts/aeroplane-api.sh METHOD /api/path [json]` for API calls.
- Ask before deleting projects or services, restoring backups, or making databases public.
