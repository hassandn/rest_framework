# rest_framework
این برای django rest framework هست 
دونستنش واجبه برای هر کسی که جنگو کار میخواد بشه
api کلا میاد بین سرور و دیتا بیس و بین دیتا بیس و سیستم ها میاد
rest یک نوع معماری هست  که هرچیزی که با معماری اون ساخته شده باشهrestfull هست
ویژگی هایی که REST API باید داشه باشه به این صورته 
1.باید کلاینت سرور باشه
2.اطلاعات به صورت کشیبل باشن
3.معماری ما باید STATELESS
stateless یعنی اینکه مثلا اگه یوزر 10 تا ریکویست بده وقتی این ریکویست ها از هم دیگه خبر نداشته باشن بهشون میگن stateless
اگه از هم خبر داشته باشن میشه stateful

قبل از اون بای و ببینیم json چی هست
java script object notation
json یک نوع داده ای هست برای انتفال داده ها و ذخیزه داده ها و  به جای xml اوممده

متد هایی که در json برا یایتون هست 
# dump
میاد یک فایل پایتونی رو به فایل جیسونی تبدیل میکنه
# dumps 
استرینگ رو تبدیل میکنه به استرینگ
# json.load 
میاد و یک فایل جیسونی رو تبدیل میکنه به یک فایل پایتونی که قابل خوندن باشه
# json.loads
این هم برای استرین هست

json.dump(data,file,indent=2)


# drf session 2
توی این قسمت میاد یاد میده چجوری فاکنشنال میتونیم از رست ای پی ای استفاده کنیم 
برای اینکار میتونیم از دکوریتور ها استفاده کنیم که خوده رست فریم ورک اونها رو اضافه کرده که توی سایت خودش هم هست اگه بری نگاه کنی
```django
from restapiframework.decerators import something

@something()
```
اگه داخل دکریتور چیزی ننویسیم از متد پست استفاده میکنه 
ولی اگه میخوایم هم میتونیم چیزی بنویسی
برای استفاده از ای پی ای 
برای جواب دادن از متد response استفاده میکنیم که تنها پارامتره اجباریش دیتا هست که باید به صورت دیکشنری باشه که اون رو به جی سون بتونه تبدیل کنه
سریالایز کردن یعنی تبدیل کردن اطلاعات در فرمت پایتون به فرمت جی سون برای اینکه مرورگر اونها رو بخونه
برای استفاده کردن اون از class base ها کد تقریبا به این صورت هست
```djagno
from restframework.views import apiviews
class Home(apiviews):
  def get(self,request):
      return response({"name":"ali"})
```

گفت که browseble api رو کنسل کنیم چون خطرناکه 
برای اینکه بخوایم از api تست بگیریم میتونیم از پست من استفاده کنیم
در رست فریم ورک در یو ار ال ها میگن endpoint

و اینسومنیا
#session 3
ما مثل جنگو که داخل متد ها از پارامتر request استفاده میکردیم باید برای رست ای پی ای هم از این استفاده کنیم
حالا ما میتونیم از این ریکوست چند چیز برداریم مثل
.data
که داده های کاربر توی بدنه به ما ارسال میکنم
.query_params
همون یو ار ال ها هستن 
.user
مثلا در جنگو مینوشتیم 
request.user و اینطوری به اطلاعات کاربر دسترسی داشتیم
توی این قسمت درمورد دیتا ها قراره ویدیو ببینیم
خب توی متد گت و متد پست ما میتونیم اطلاعات رو ارسال کنیم ولی شیوه هاشون فرق داره
توی متد گت ما میتونیم دو جور اطلاعات رو ارسال کنیم یکی از طریق آرگومان
یعنی که کاربر بگیم نام کاربریشو توی یو ار ال بزنه
اول از همه باید بری توی فایل یو ار ال ها و بگی قراره که یک متغیر وارد بشه از طریق یو ار ال به نام name که بعدش بتونیم از اون استفاده کنیم طریقه استفاده ازش به این صورت هست
```url
127.0.0.1:8000/ali
```
```django
urls.py
urlspatterns = [
  path('<string:username>/',views.method,name=''>
]
```
بعد از اون توی فایل views باید ریکویست رو اضافه کنیم 
یه چیزیم بگم که اون داره کلاس بیس کاراشو پیش میبره
```django
Class home(api_view):
  def get(self,request,username)
    return Response({"name":username})
```
این بعدش در name مینویسه علی
یا از طریق کویری پارامتر ها
این روش در سرچ ها استفاده میشه
این ها با علامت سوال شروع میشن و حالت کی ولیو دارن 
```
12.0.0.1:8000/?name=ali
```
بعد از اون برای اینکه اطلاعات رو ببینه دیگه نیازی نیست توی یو ار ال ها چیزی بنویسیم و خالی باشه اوکی هست 
و بعد فقط برای اینکه از این روش استفاده کنیمم باید توی ویوز باید اینکار رو انجام بدیم 
```django
Class home(api_view):
  def get(self,request):
    name = request.queryparams['name']
    return Response({"name":name}
```
ما وقتی از متد پست استفاده میکنیم که بخوایم فایلی رو اپلود کنیم یا یا یانکه میخوایم یوزرنیم و پسورد رو بزاریم برای فرستادن به سرور
توی این روش اطلاعات از طریق جی سون ارسال میشن به سرور برای استفاده اون در  رست فریمورک میتونیم این کار ها رو انجام بدیم

```DJANGO
Class home(api_view):
  def post(self,request):
    name = request.data['name']
```
و اینکه  در متد گت یو ار ال ما نمیتونه بیشتر از 2048 باشه
# post 
برای اینکه از متد پست استفاده کنیم در میتونیم از .data استفاده کنیم
کدش به این صورت هست
```django
Class home(api_view):
  def post(self,request):
    name = request.data['name']
    return response({"name":name})
```
این بادی رو درست کردی اون وقت درست میشه
# serializer 3
ما تا الان میومدیم و اطلاعات رو خودمون به طور دستی وارد میکردیم ولی در دنیای واقعی ما باید اطلاعات رو از مدل ها بگیریم
ما باید روشی داشته باشیم که کویری ست هایی که میگیرم خودشون تبدیل بشن ه دیکشنری و تبدیلش میکنیم به دیکنشری که صورت جیسون به کاربر نشون داده بشه برای اینکار باید از serializer ها استفاده بکنیم
serialize
میگه که تبدیل نوع کویری ست و یا دیتا مدل ها به داده هایی هست که پایتون داره 
deserialize 
یعنی تبدیل نوع داده پایتون به داده هایی مثل جیسون یا ایکس ام ال

سریالایز مثل فرم ها هستن باید مثل مدل ها خودمون فییلد ها رو درست کنیم و....
Serializer مثل Form
ModelSerializer مثل ModelForm
خب الان میریم داخل مدل ها و یک مدل درست میکنیم
با اسم سن و ایمیل
```django
form django.db import models
Class persion(models.Model):
  name = blah blah
  age  = blah blah
  email= blah blah
  def __str__(self):
    return self.name
```
بعد برای اینکه اطلاعات در داخل دیتا بیس ذخیزه بشه مینویسیم
makemigrations
migrate
خب حالا توی ادمین پنل هم داریم اونو
خب فرض کن ما میخوایم که یه اند پوینت داشته باشیم که وقتی اونو زدیم کاربر های ما رو نشون بده
داخل سریالازر یه چیزی هست که مشخص میکنه داخل مدل چه خبر هست
برای سریالایز کردن باید یک فایل دیگه درست کینم به نام serrialize 
پیشنهاد میشه برای اسم گزای کلاس های سریالایزر ها اول اسم مدل رو بنویسید و بعد بنویسید سریالایزر 
حالا فیلدی که داخل مدل داریم باید داخل سریالایزر ها بزاریم که توی سایتش هست
```django
from rest_framework import serializers

class PersonSerializer(serializers.Serializer):
    name = serializers.CharField()
    age  = serializers.IntegerField()
    email= serializers.EmailField()
```
این کد برای سریالایزر هست 
بعد از اون باید بریم توی ویو هامون تا از داده های مدلمون رو بتونیم بفرستیم
```django
views.py
form .models import person
from .serializer import Personserializer
@api_view(['GET'])
def say_hello(request):
    persons       = person.objects.all()#for gett all informations from model
    serlizer_data = PersonSerializer(instance=persons,many = True)# this line is for serialize information in models and instance is fot that and this thing just accept one information because of that we should set many=true because we use many informain
    return Response(data=serlizer_data.data)#its must be a .data because its should return data only
```
خب بیا اول توضیح بدم معنی این کد ها رو 
اولین خط که میاد اطلاعات رو از مدل ها میگیره
خط دوم هم برای سریالایزر کردن اطلاعات توی مدل هست و اگه اطلاعات ما از یکی بیشتر بود باید منی رو ترو میزاشتیم
خط سوم هم باید .data بزاریم که فقط دیتا رو نشون بده 
براری زدن ای دی میتونیم از این رو در سریالایز کردن اضافه کنیم
```django
id = serializer.integerfield()
```
متیونیم فیلتر بزاریم و با استفاده از گت از اون استفاده کنیم
```django
form .models import person
from .serializer import Personserializer
@api_view(['GET'])
def say_hello(request):
    persons       = person.objects.get(name="amir")
    serlizer_data = PersonSerializer(instance=persons)
    return Response(data=serlizer_data.data)#its must be a .data because its should return data only
```
ولی باید منی رو برداریم چون فقط داریم یک اطلاعات رو نشون میدیم
# register user 4
توی این قسمت میخوایم یوزر رو ثبت نام کنیم برای اینکار
یک اپ اکانت میسازیم
بعد یک فایل سریالایزر براش درست میکنیم 
برای یوزر 
یوزرنیم داریم پسورد و ایمیل
بعد از اون هر فیلد در سریالایزر یک ارگومانی میگیرن ولی برای استفاده و بعضی از ارگومان ها هستن که برای همه فیلد ها استفاده میشه مثل readonly و....
به اینا میگن core argument البته الان کاری به اینا نداریم 
و الان باید از required رو ترو بزاریم تا کاربر اونها رو وارد کنه
بعد میریم توی ویوزو این کد رو مینویسیم
```django
@api_views(['POST'])
def UserRegister(request):
  serializer_data = UserRegiserserializer(data=request.POST)
````
اگه توجه کرده باشی ما در سریلایزر گفتیم instance ولی اینجا میگیم دیتا چون باید از کاربر اینا رو بگیریم
که بعدا بتونیم روی اطلاعات کاربر بزنیم is_valid()
خب اگه یادت باشه وقتی ما توی جنگو بودیم میزدیم که آیا اطلاعات کاربر درست هست یا نه باید از cleaned_data استفاده میکردیم
ولی الان باید ی روش دیگه بریم
اینا رو ی بار نوشتم دستم خورد کامیت نشده رفت بیرون 
```django
class userregister(api_view):
  def post(self,request):
    serializer_data = UserRegisterSerializer(data=request.POST)
    if serializer_data.is_valid():
      User.objects.create_user(
        username =  serializer.data['username']
        password =  serializer.data['password']
        email    =  serializer.data['email']
        return Response(serializer_data.data)
      )
    return Response(serializer_data.errors)
````
# custom validator 5
توی این قسمت میخوایم درمورد ولیدیشن صبحت کنیم که قراره درمورد دو نووع از اونها صبحت کنیم
دوتا قسمت داره
Field-level validation
Object-level validation
در فیلد لول ما میایم وقتی میخوایم یک فیلد خاص رو ولیدیت کنیم استفاده میکنیم مثلا میایم میگیم که کاربر عادی باشه و ادمین نباشه
یا اینکه یک فیلد دیگه از پسورد درست میکنیم 
برای اینکار یک سری کار ها باید انجام بدیم
اول باید یک تابع درست کنیم در فایل serializers.py بعدش اسمش اولش باید validata_title باشه که دو ارگومان میگیره
```
  def validate_title(self,value):
    if value == 'amdin':
      raise serializers.validationError("you cant be a admin")
    return vlaue
```
این میگه که اگه اسم رو گذاشت ادمین بهش بگه که تو نمیتونی اسم ادمین رو انتخاب کنی
یک کار دیگه ای که میشه باهاش کرد اینکه بهش پسورد کانفیگ اضافه کنیم
به این کار میگن ابجکت لول چون داریم چند چیز رو باهم مقایسه میکنم فکر کنیم
```django
  def validate(self,data):
    if data['password'] != data['password2']:
      raise serializers.validationError("passwords are not match")
    return data
```

یه روش دیگه هم وجود داره که وقتی مثلا یک فیلد باید چند تا ولیدیشن میخواد خوبه
اسمش هم validators هست
```django
def no_spam(value):
  if 'allah' != in value:
   raise serializers.validationError('fields can not have a word 'allah' in it')
```
این تابع رو قبل از کلاس اضلی بزار
بعدش داخل فیلد ها بنویس
```django
username = serilizers.Charfleid(validators=[no_spam])
```
# model serializers 6
تاجایی که من فهیدم این همون کار قبلی رو انجام میده فقط تمیز تر
مدل سریالایزر مثل همون مدل فرم ها بود 
البته من یادم نمیاد چی بود مدل فرما فقط میدونم کاره راحت تری نسبت به مدل ها باید انجام میدادیم
```django
>>> from django.forms import ModelForm
>>> from myapp.models import Article

# Create the form class.
>>> class ArticleForm(ModelForm):
...     class Meta:
...         model = Article
...         fields = ["pub_date", "headline", "content", "reporter"]
...

# Creating a form to add an article.
>>> form = ArticleForm()

# Creating a form to change an existing article.
>>> article = Article.objects.get(pk=1)
>>> form = ArticleForm(instance=article)
```
یه همچین چیزی بوده
کاربرد های مدل سریالایزر ها از سریالایزر ها بیشتر هست
خب برای اینکه از مدل سریالایزر ها استفاده کنیم باید به این صورت عمل کنیم
```django
from django.contrib.auth.models import User
class UserRegisterSerializer(api_veiw):
  class META:
      model = User
      fields = ['username','password','email']
      # or
      fields = "__all__"
      # its means every thing except this things
      excludes = ['usernema'] # everything but username
```
خب این میاد و مثل قبل کار میکنه 
برای اینکه بریم و رایت انلی کنیم یک فیلد رو میتونیم از دیکشنری extra_kwargs استفاده میکنیم
پس داریم
```django
from django.contrib.auth.models import User
Class UserRegisterSerializer(api_view):
  class Meta:
    model = User
    fields = ['username','password','email']
    extra_kwargs = {'password':{"read_only":true}}
```
حالا ما تو روش قبلی ولیدیتور ها رو میزاشتیم جای پارامترا ولی حالا میزاریم این کار رو انجام میدیم
```django
from django.contrib.auth.models import User
def anti_sapm(value):
    if 'admin'==value:
      serializers.validationError('fields can not have a word 'admin' in it')
     return value
Class UserRegisterSerializer(api_view):
    class Meta:
        model = User
        fields= ['username','password','emial']
        extra_kwargs = {'username':{'read_only':true},
        {"email":{"validators":anti_spam}
        
        }
```
خب حالا فرض کن که میخوایم فیلدی رو اضافه کنیم که داخل ماژول ما نبوده برای اینکار کافیه که قبل از کلاس متا اون رو اضافه کنیم
به این صورت 

```django
Class UserRegisterSerializer(api_view):
  password2 = Serializer.Charfield(required=true,write_only=true)
  class Meta:
    model = User
    fields = ['username','password','email','password']
```
# override clean 7
زمانی که ما یک مدل سریالایزر درست کردیم میتونیم از اون برای ساختن و یا اپدیت کردن یک آبجکت زوی اون مدل استفاده کنیم 
توی فایل سریالایزر مینویسیم
```djngo
from rest_framework import serializers
from django.contrib.auth.models import User


def anti_spam(value):
    if 'allah' in value:
        raise serializers.ValidationError('fields dont have a allowed to use word `allah` in it')


class RegisterUserSerializer(serializers.ModelSerializer):
    password2 = serializers.CharField(write_only=True,required=True)
    class Meta:
        model = User
        fields = ['username','password','password2','email']
    
    def create(self, validated_data):
        del validated_data['password2']
        return User.objects.create_user(**validated_data)
```
و در فایل ویوز باید بنویسیم
```django
from rest_framework.views import APIView
from rest_framework.response import Response
from .models import UserRgister
from .serializers import RegisterUserSerializer
from django.contrib.auth.models import User


class RegisterUser(APIView):
    def post(self,request):
        serializer_data = RegisterUserSerializer(data=request.POST)
        if serializer_data.is_valid():
            serializer_data.create(serializer_data.validated_data)
            return Response(serializer_data.data)
        return Response(serializer_data.errors)


```

# status codes 8
کد هایی که میان میگن ریکویست چه اتفاقی براش افتاد و در چه وضعیتی تموم شد
منظورمون کد های وضعیت http هست که 5 عدد دارن 
مثل 
کد های 
1XX informational 
هستن
2XX successful
3XX redirection
یعنی اون منبعی که در سرور دنبالش بودیم در سرور جابه جا شده
4XX  client error
5XX server error
is_informational()  # 1xx
is_success()        # 2xx
is_redirect()       # 3xx
is_client_error()   # 4xx
is_server_error()   # 5xx

خوانایی کد رو هم میبره بالاتر
از این به بعد هر ریسپانسی که برمیگردونیم باید status code رو هم بهش بدیم
کد ها رو درست بزار
[link](https://www.django-rest-framework.org/api-guide/status-codes/)
# authentication 9
برای شناسایی کاربر هست
برای اینکه مثلا دسترسی های کاربر رو قطع کنیم از پرمیشن ها استفاده میکنیم
