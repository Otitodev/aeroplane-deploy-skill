# aeroplane-deploy

[![skills.sh](https://skills.sh/b/Otitodev/aeroplane-deploy-skill)](https://skills.sh/Otitodev/aeroplane-deploy-skill)

An agent skill that teaches a coding agent how to deploy to a self-hosted [Aeroplane](https://github.com/xt42io/aeroplane) server (aeroplane.run), so you don't have to explain it from scratch in every session.

It covers:

- **First-time setup:** installing Aeroplane on a VPS, onboarding, the GitHub App, and creating an API key.
- **Deploying a project:** choosing the service type, making the repo deployable, creating the project and service, deploying, and verifying.
- **Env vars, domains, and TLS:** variables, database references, generated and custom domains, DNS provider records.
- **Databases, logs, and recovery:** Postgres, MySQL, Redis, MongoDB, backups, log streams, and what rollback really means on Aeroplane.
- **Troubleshooting:** symptoms mapped to causes.

It also ships a small `curl`-based helper, `scripts/aeroplane-api.sh`, that sends authenticated API requests without ever printing your key.

## Install

### All agents (skills.sh)

```sh
npx skills add Otitodev/aeroplane-deploy-skill
```

### Claude Code

Copy the `aeroplane-deploy` folder into your skills directory.

```sh
# every project on your machine
cp -r aeroplane-deploy ~/.claude/skills/

# or just one project
cp -r aeroplane-deploy your-project/.claude/skills/
```

On Windows, the personal directory is `%USERPROFILE%\.claude\skills`. Restart your session, then ask for something like "deploy this project to my Aeroplane server".

### Other coding agents

Agents that read `AGENTS.md` (Codex, Cursor, and others) can use the same files. Copy the folder somewhere in your project or home directory, then add the snippet from [`integrations/AGENTS-snippet.md`](integrations/AGENTS-snippet.md) to your `AGENTS.md`, adjusting the path. I have only tested this skill in Claude Code.

## Set up your connection

The skill reads two environment variables. Set them where your coding agent can see them, **not** in a file inside a repo.

```sh
export AEROPLANE_URL="https://pilot.example.com"
export AEROPLANE_API_KEY="ap_..."
```

Create the key in the dashboard under **System Settings -> API Access**. Use a read and write key for deploying. A key limited to specific projects can't create new ones. Sessions started before you set the variables won't see them.

## What it will and won't do

- It never prints or stores your API key, and the helper refuses to send it over plain `http://` (except to localhost, or when you set `AEROPLANE_ALLOW_HTTP=1`).
- It asks before deleting a project or service, restoring a backup, making a database public, or applying a system update.
- Some steps can only be done in the browser: owner account, GitHub App, system settings, DNS provider connections, and creating API keys. The skill tells you what to click.
- It won't SSH into your server or run the installer unless you ask.
- Aeroplane has no API to roll back or deploy a specific commit. The skill explains the supported way to undo a release (`git revert` and push) instead of pretending otherwise.

## Keeping it accurate

The references were written from the Aeroplane docs and source (`website/src/content/docs/docs/` and `src/server/index.ts`). If Aeroplane's behavior changes, update the matching file in `aeroplane-deploy/references/`. Pull requests are welcome.

## License

Apache-2.0, the same as Aeroplane. See [LICENSE](LICENSE).
