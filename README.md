django-admin startproject elibrary_backend
cd elibrary_backend
python manage.py startapp books
from django.db import models

class Book(models.Model):
    title = models.CharField(max_length=200)
    author = models.CharField(max_length=100)
    category = models.CharField(max_length=100)
    availability = models.BooleanField(default=True)
    added_on = models.DateField(auto_now_add=True)

    def __str__(self):
        return self.title
        from rest_framework import serializers
from .models import Book

class BookSerializer(serializers.ModelSerializer):
    class Meta:
        model = Book
        fields = '__all__'
        from rest_framework import viewsets
from .models import Book
from .serializers import BookSerializer

class BookViewSet(viewsets.ModelViewSet):
    queryset = Book.objects.all()
    serializer_class = BookSerializer
    from django.contrib import admin
from django.urls import path, include
from rest_framework import routers
from books.views import BookViewSet

router = routers.DefaultRouter()
router.register(r'books', BookViewSet)

urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/', include(router.urls)),
]
npm install -g @vue/cli
vue create elibrary-frontend
cd elibrary-frontend
npm install axios
<template>
  <div>
    <h2>Book List</h2>
    <ul>
      <li v-for="book in books" :key="book.id">
        {{ book.title }} by {{ book.author }}
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      books: []
    }
  },
  mounted() {
    axios.get("http://localhost:8000/api/books/")
      .then(response => {
        this.books = response.data
      })
      .catch(error => {
        console.error("Error fetching books:", error)
      })
  }
}
</script>
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'elibrary_db',
        'USER': 'your_user',
        'PASSWORD': 'your_password',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}
