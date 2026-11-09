# Node & NPM

## Package Management

```bash
npm clean-install          # fast reproducible install from package-lock.json
npm outdated               # check for outdated packages
npm audit --omit=dev       # audit production dependencies only
npm cache clean --force    # flush npm cache
```

## Scripts & Runtime

```bash
npx --no-install <tool>    # run locally installed binary without downloading
node --watch index.js      # native file watcher (Node 18+)
node -e "console.log(process.versions)" # inspect engine versions
```
