# Django REST Framework Serializer 仕様

## 公式ドキュメント

http://www.django-rest-framework.org/api-guide/serializers/

## Serializerの定義

```python
from rest_framework import serializers

class Comment():
    def __init__(self, email, content, created=None):
        self.email = email
        self.content = content
        self.created = created or datetime.now()

class CommentSerializer(serializers.Serializer):
    email = serializers.EmailField()
    content = serializers.CharField(max_length=200)
    created = serializers.DateTimeField()

comment = Comment(...)
serializer = CommentSerializer(comment)
print(serializer.data)
```

## ネストされたオブジェクトの扱い

```python
class UserSerializer(serializers.Serializer):
    email = serializers.EmailField()
    username = serializers.CharField(max_length=100)

class CommentSerializer(serializers.Serializer):
    user = UserSerializer() # <-
    content = serializers.CharField(max_length=200)
    created = serializers.DateTimeField()
```

## ModelSerializer

```python
class AccountSerializer(serializers.ModelSerializer):
    class Meta:
        model = Account
        fields = ('id', 'account_name', 'users', 'created')
```


## serializers

* serializers.CharField(max_length=100)
* serializers.EmailField()
* serializers.DateTimeField()

## parameters

* required=True/False
* many=True/False
*