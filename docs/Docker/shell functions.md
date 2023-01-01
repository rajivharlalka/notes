### Docker history of layers

```shell
docker history --human --format "{{.CreatedBy}}: {{.Size}}" <container name>
```