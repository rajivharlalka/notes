- [Learn Docker: Container training](https://container.training/intro-selfpaced.yml.html)

---
### Tools

- [dive](https://github.com/wagoodman/dive)


---

### Docker history of layers

```shell
docker history --human --format "{{.CreatedBy}}: {{.Size}}" <container name>
```