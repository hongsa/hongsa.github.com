---
layout: post
title: Django Auth User Customize
category : programming
---

###장고에서 기본적으로 제공하는 Auth.User를 customize해서 사용
- settings에서 선언해줘야 함(이 부분을 잊지말자!)

```python
AUTH_USER_MODEL = 'movement.Client' //(app.modelname)
```

- 상속해서 사용하기

```python
from django.contrib.auth.models import BaseUserManager, AbstractBaseUser

#custom-user model manager
class MyClientManager(BaseUserManager):

    def create_user(self, email, password = None):
        """
        Creates and saves a User with the given email and password
        """
        if not email:
            raise ValueError('User must have an email address')

        client = self.model(
            email=self.normalize_email(email),
        )

        client.set_password(password)
        client.save(using=self._db)

        return client

    def create_superuser(self, email, password):
        """
        Creates and saves a superuser
        """
        client = self.create_user(
            email,
            password=password
        )
        client.is_admin = True
        client.save(using=self._db)
        return client


#custom 사용자 테이블
class Client(AbstractBaseUser):
    email = models.EmailField(
        verbose_name='email address',
        max_length=255,
        unique=True,
    )
    username = models.CharField(
        verbose_name='Username',
        max_length=30,
        unique=True,
        null=False
    )
    is_active = models.BooleanField(default=True)
    is_admin = models.BooleanField(default=False)
    date_joined = models.DateTimeField(auto_now_add=True)

    objects = MyClientManager()

    USERNAME_FIELD = 'email'
    # REQUIRED_FIELDS = ['username','password']

    def get_full_name(self):
        # The user is identified by their email address
        return self.email

    def get_short_name(self):
        # The user is identified by their email address
        return self.email

    def __str__(self):              # __unicode__ on Python 2
        return self.email

    def has_perm(self, perm, obj=None):
        "Does the user have a specific permission?"
        # Simplest possible answer: Yes, always
        return True

    def has_module_perms(self, app_label):
        "Does the user have permissions to view the app `app_label`?"
        # Simplest possible answer: Yes, always
        return True

    @property
    def is_staff(self):
        "Is the user a member of staff?"
        # Simplest possible answer: All admins are staff
        return self.is_admin
```