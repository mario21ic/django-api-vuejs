# django-api-vuejs
Demo project to practice api rest with django and vuejs 

Create App
```
eb init -p python-3.7 django-api
```

Update some configuration
```
eb init -i
```

Create environment
```
eb create django-api-env1
```

Status
```
eb status
```

Make some changes and deploy:
```
eb deploy
```

Check logs
```
eb logs --all
```

Delete environment:
```
eb terminate django-api-env1
```
