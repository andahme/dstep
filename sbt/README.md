```bash
docker run -it --rm --name sbt \
  --volume ivy-home:/repository \
  --volume ${PWD}:/workspace \
  andahme/sbt
```

