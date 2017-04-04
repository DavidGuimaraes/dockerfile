### 3. Sobrescrevendo comando

* Criando nova imagem herdando da `img-onbuild`
```bash
$ docker run -t overwrite-cmd .
```

* Rodando container sobrescrevendo comando `CMD`
```bash
$ docker run overwrite-cmd
```