# Volumes & Bind Mounts

**Anonymous Volume**
- Creates specifically for a single container
- Survives when container shutdown/restart, unless `-rm` is used
- Can NOT be shared across containers
- Since it's anonymous can't be re-used
- Useful to prioritize container-internal paths higher than external paths
```
docker run -v /app/data ...
```

**Named Volume**
- Not bind to any specific container
- Survives when container shutdown/restart - removal via Docker CLI
- Can be shared across containers
- Can be re-used for same container
```
docker run -v data:/app/data ...
```

**Bind Mount**
- Live on local/host machine, not bind to any specific container
- Survives when container shutdown/restart - removal on host
- Can be shared across containers
- Can be re-used for same container
- >Shortcut for path : macOS / Linux: `-v $(pwd):/app`. Windows: `-v "%cd%":/app`
```
docker run -v /path/to/code:/app/code ...
```

**Read Only Volume**
- Using with Bind Mount
- Ensure that Docker will not be able to write anything into specified folder
- Make volume read only by using `ro` flag

```
docker run -v /path/to/code:/app/code:ro ...
```
