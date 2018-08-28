# Django REST Framework Serializer 仕様

## 公式ドキュメント

http://www.django-rest-framework.org/api-guide/serializers/

## Serializerの定義

```python
class Comment():
    def __init__(self, email, content, created=None):
        self.email = email
        self.content = content
        self.created = created or datetime.now()
        
class CommentSerializer(serializers.Serializer):
    email = serializers.EmailField()
    content = serializers.CharField(max_length=200)
    created = serializers.DateTimeField()
```
