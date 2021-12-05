## To reproduce

- `git clone` this repo.
- `dip build`
- try the following two cases:
  - 1: using the normal docker-compose
    - `docker-compose up -d`
    - check the port forwarding via `docker ps`
      - PORTS: `0.0.0.0:3000->3000/tcp, 0.0.0.0:9229->9229/tcp` (works fine)
    - `docker-compose down`

  - 2: using dip
    - `dip sh`
    - check the port forwarding via `docker ps`
      - PORTS: (empty)

As far as I see, the following host/ports configs will not working when using dip.

```yaml

...
    environments:
    ...
      HOST: 0.0.0.0
...
    ports:
      - '3000:3000'
      - '9229:9229'
```

