# npm

## List global packages with details.
```sh
npm ls -gl --depth=0
```

## View details of a npm package
```sh
npm view <package> [versions|author|license]
```

## Set default configuration for package.json
```sh
npm set init.author.name "$NAME"
npm set init.author.email "$EMAIL"
npm set init.author.url "$SITE"
```

## Bump package version
```sh
npm version 2.1.0
```

## Flatten and deduplicate the dependency tree.
```sh
npm dedupe
```

## Remove extraneous packages
```sh
npm prune
```

## Open the bugtracker of a package
```sh
npm bugs <package>

npm bugs # Current project's bugtracker
```

## Basic npm troubleshooting
```sh
npm doctor
```
