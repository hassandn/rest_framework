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
برای اینکار باید بری و توی داکیومنتا بخونیشون
میتونی روی همه ویو ها اثتنتیکیت بزاری یا اینکه روی بعضی از ویو ها بزاری
توی این دوره رفت داخل ستینگز و اینستالد اپز و برنامه رو اضافه کرد 
و روش های مختلفی وجود داره برای کاربر که توکن رو بهشون بدیم
میتونیم دستی این کار رو انجام بدیم 
میتونیم با سیگنال ها اینکار رو انجام بدیم که وقتی کاربر جدید ساخته شد توکن هم براش ساخته بشه
یا میتونی برای همه کاربر ها این کار رو انجام بدی
ی روش دیگشم اینکه از یک ویو استفاده کنیم که با زدن یک یو ار ال یوزرنیم و پسورد رو برای کاربر ارسال میکنیم و بعد اون میاد و برای کاربر یک توکن میسازه
و یا میتونی کاستومایزش کنی
با منیج . پای هم میشه اینکار رو انجام داد
وقتی که توکن رو مشخص کردیم میتونیم نوع اثتنتیکیشن رو مشخص کنیم

یادت نره ختما توی تنظیمات این رو بنویسی
```django
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        # 'rest_framework.authentication.SessionAuthentication',
        # 'rest_framework.authentication.authtoken'
        'rest_framework.authentication.TokenAuthentication',
    ]
}
```
[link](https://www.django-rest-framework.org/api-guide/authentication/)
# permessions 10
با پرمیشن ها میتونیم محدودیت بزاریم روی ویو هامون
با request.user و request.auth میتونیم مشخص کنیم که کاربر به یک ویو دسترسی داشته باشه یا نه
اگه یک نفر اجازه نداشته باشه یا 
exceptions.PermissionDenied or exceptions.NotAuthenticated
چون لازم نیست روی همه ویو ها اتفاقات خاصی بیوفته به جای اثتنیکیشن ما باید روی بعضی از ویوهامون از پرمیشن هامون استفاده کنیم
اینا رو دیگه خودت برو ببین خسته شدم

# question answer 11
توی این جلسه ای پی ای رو بسازه که کاربر ها بتونن سوال بپرسن و ی سری دیگه از کاربر ها بیان و بهش جواب بدن
اول میاد و یک مدل برای سوال ها و یک مدل برای جواب ها میسازه که من در ادامه اونها رو اضاقه خواهم کرد
خب اول از همه اومد و یک مدل برای سوال ها ایجاد کرد
```django
class Question(models.Model):
  user = models.ForeignKey(User, on_delete=models.CASCADE, related_name='questions')
	title = models.CharField(max_length=200)
	slug = models.SlugField(max_length=200)
	body = models.TextField()
	created = models.DateTimeField(auto_now_add=True)

	def __str__(self):
		return f'{self.user} - {self.title[:20]}'

	def __str__(self):
		return f'{self.user} - {self.question.title[:20]}'
```
خب توی این کد میاد فیلد ها رو مشخص میکنه در خط یوزر اونحا که زده ان دلت منظورش اینکه اگه این پاک شده بقیه جاها هم پاک بشه فکر کنم تا جایی که یادمه 
بعدیش هم یوزر هست که ایدی یوزری که اونو فرستاده داخلش هست
در خط سوال نمیدونم الان چرا سوالو دوباره تو خودش اورده 
و اینها رو به عنوان فارن کی اضافه کرده 
در کریتد هم تاریخ همون لحظه رو خودش به صورت خودکار مینویسه
و بعدشم که تابع اس تی ار هست که در ادمین پنل این ها رو نمایش میده 
که اسم یوزر و 20 تا کاراکتر اول سوالش رو نشون میده برای ادمین
اشتباه کردم
کست کیت هم میگه اگه یوزر اون ور پاک کرد تو بقیه جاها تو هم پاکش کن

```django
class Answer(models.Model):
	user = models.ForeignKey(User, on_delete=models.CASCADE, related_name='answers')
	question = models.ForeignKey(Question, on_delete=models.CASCADE, related_name='answers')
	body = models.TextField()
	created = models.DateTimeField(auto_now_add=True)

	def __str__(self):
		return f'{self.user} - {self.question.title[:20]}'
```
اینجا در خط سوال نوشته شده که به جواب لینک شده
خب بعدش اون ها رو توی سریالایزر اضافه میکنیم
و بعد در ویو ما یک کلاس اضافه میکنیم که متد های مختلفی رو میگیره مثل get post put delete
که گت برای دیدن اطلاعات هست پست برای ارسال اطلاعات و پوت برای اپدیت کردن اطلاعات و دلت برای پاک کردن اطلاعات


```djngao
class QuestionSerializer(serializers.ModelSerializer):
	answers = serializers.SerializerMethodField()
	user = UserEmailNameRelationalField(read_only=True)

	class Meta:
		model = Question
		fields = '__all__'


class AnswerSerializer(serializers.ModelSerializer):
	class Meta:
		model = Answer
		fields = '__all__'
```
عملیات کراد کرید رید اپدیت و دلت
# update-delete 12
برای ساختن که باید از متد پست استفاده کنیم مثل همون کاری که قبلا انجام دادیم
```django
class questions(api_View):
	def post(self,request):
		serializer_data = Questionserializer(request.post)#or request.data
		if serilizer_data.is_valid():
			serializer_data.save()
			return response(serilizer_data.data)
		return response(serilizer_data.errors)
```
دبلیلی که انقد راحت سیو رو زد این بود که ما از مدل فرم ها در دیتا بیسمون استفاده کرده بودیم 
برای همین اینطوری شد وگرنه باید خودمون به صورت دستی این کار رو انجام میدادیم
بهتره که برای هر کار یک کلاس جداگونه درست کنیم 
برای اپدیت کردن ما نیاز به پرایمری کی داریم تا بدونیم کدوم ابجکت رو میخوایم اپدیت کنیم 
```django
def put(self,request,pk):
	
```
پوت برای آپدیت کردن به کار میره 
# method field 13
توی ایت جلسه میخواد متد هایی رو که داریم در کلاس های جداگونه پخش بکنیم
و اینکه زمانی که سوال ها رو نشون دادیم جواب ها رم بتونیم نشون بدیم
برای اینکار میریم در قسمت داکیومنت قسمت فیلد های متفرقه
[link](https://www.django-rest-framework.org/api-guide/fields/#miscellaneous-fields)
این اجازه میده که فیلدی رو به متد خاصی متصل کنیم
برای اینکه بتونیم جواب های سوال ها رو با سوال ها با هم ببینیم باید از متد فیلد ها استفاده کنیم
```django
class QuestionSerializer(serializers.ModelSerializer):
	answers = serializers.SerializerMethodField()

	class Meta:
		model = Question
		fields = '__all__'

	def get_answers(self, obj):
		result = obj.answers.all()
		return AnswerSerializer(instance=result, many=True).data
```
در خط answers ما میام و از سریالایزر متد فیلد ها استفاده میکنیم که بتونیم فیلد ها رو به متد خاصی تخصیص بدیم
get_answers هم  برای اینکه که ابجکت رو نشون بده برای همین یه قانون داره اونم اینکه از گت _ و اسم انسرز استفاده کنیم که حالا میتونه هر اسمی باشه 
بعدش هم ریزالت رو مساوی با ابجکت قرار میدیم که یعنی اون سوال برای ما به نمایش در بیاد و بعد انسرز رو مینویسیم و همشو فراخوانی میکنیم
بعد از اون انسر سریالایزر رو صدا میزنیم و اینستنس رو میزاریم روی ریزالت و منی رو مساوی با ترو قرار میدیم و دیتای اون رو برمیگردونیم
دلیل اینکه اون انسر توی ریزالت همون ریلیتد نیم هست توی مدل هامون
 و دلیل اینکه تونستیم جواب ها رو بگیرم اینکه ما فارن کیه جواب ها رو مساوی قرار داده بودیم با question 
```django
class Answer(models.Model):
	user = models.ForeignKey(User, on_delete=models.CASCADE, related_name='answers')
	question = models.ForeignKey(Question, on_delete=models.CASCADE, related_name='answers')
```

# custom permission 14
بعضی وقت ها ما نیاز داریم به کاستوم پرمیشن ها تا کنترل بیشتری روی پرمشن ها داشته باشیم
برای اینکار ما باید کلاسی بسازیم که از base permission ارث بری کنه
.has_permission(self, request, view) 
این میگه که آیا کاربر میتونه به ویو دسترسی داشته باشه و قبل از اینکه کاربر وارد ویو بشه اون رو بررسی میکنه 
.has_object_permission(self, request, view, obj)
این میگه که آیا کاربر میتونه به آبجکت دسترسی داشته باشه یا نه این بعد از اینکه کاربر وارد ویو شد بررسیش میکنه
خب ما چند تا چالش داریم برای برناممون 
1.هر کسی که میتونه سوالات رو ببینه
2. فقط کاربران اثتنتیکیت کرده میتونن سوالات رو ببینن
3.فقط کاربرانی که اثتنتیکیت کردن میتونن سوالات رو اپدیت و یا که حذف کنند و  اینکه حتما باید سوالات خودشونو حذف باید بتونن بکنن
# serializer relations 15
مشخص میکنه چه رابطه ای رو در نتیجه نشون بدیم
خب تا الان هر وقت میخواستیم اطلاعات رو ببینیم ایدی طرف نمایش داده میشده برای ما
یا مثلا میخوای به جای ایدی اصلا بیاد و ایمیل کاربر رو نشون بده
خب برای این میتونی بری و داکیومنتو بخونی
[link](https://www.django-rest-framework.org/api-guide/relations/)
 هایپر لینک یعنی اینکه به جای ایدی یک لینک میاد که با زدن روش میتونی بری و فقط اون اطلاعات رو بخونی و ببینی
 ما میتونیم حتی custom relational fields استفاده کنیم
 مثلا فرض کن میخوای یوزر اول یوزرنیمش رو نشون بدی و بعد ایمیلشو برای این کار باید این کاررو بکنی

# viewsets 16
ویو ست ها به ما اچازه میدن چند تا عملیات رو داخل یک کلاس قرار بدیم
خب همونطور که یادته توی کارهایی که قبلا انجام دادیم داشتیم که مثلا برای اپدیت کردن یک کلاس داشتیم برای دیدین سوال ها یک کلاس و برای حذف هم یک کلاس داشتیم و برای هرکدوم از اونها یک یو ار ال ساخته بودیم
وقتی که پروژه بزرگتر بشه تعدا یو ار ال های اونم زیادتر میشه برای همین ما نیاز داریم به ویو ست ها 
توی ویو ست ها ما نمیتونیم از از متد ها پست و گت استفاده کنیم 
به جاش مثلا لیست داریم یا کریت که کار های انها رو انجام میده مثل 
لیست که نشون میده ابجکت ها رو 
کریت که میسازه ابجکت هارو
retrieve برای خوندن یک ابجکت هست
Update برای اپدیت کردن یک آبجکت
partial_update برای اپدیت کردن بخش جزیی از یک ابجکت
destroy این هم برای پاک کردن یک آبجکت استفاده میشه
خب الان میریم توی اپ اکانت و میایم از ویو ست ها استفاده میکنیم
ویو ست ها وقتی استفاده میشن که کاری که انجام میدیم ساده هستش 
اگه کاری که انجام میدیم خطوطش زیاد باشه	
از همون ای پی ای ویو باید استفاده بکنی
یو ار ال های معولی نمیتونن با ویو ست ها کار بکنن چون ویو ست ها چندین متد مختلف داخل خودشون دارن برای کار کردن با ویوست ها ما میایم و از روترها استفاده میکنیم
روتر ها میان به صورت اتوماتیک برای ما یو ار ال ایجاد میکنن مناسب ویوست ها هستند
خب توی ویو ست ها بسته به اینکه با چه متدی صدا میزنیم یو ار الو کار های مختلفی انجام میده 
متد patch فکر کنم برای آپدیت کردن هست
ما تو دنیای واقعی اطلاعات کاربر رو حذف نمیکنیم 
ما دیفالت روتر داریم که با سیمپل روتر فرق زیادی نداره
داخل ویو ست ها ما نمیتونیم از کاستوم پرمشن ها استفاده کنیم
و دیگه خودت باید بری و داخل سریالایزر ها خودت بریم بررسی بکنی یا میتونی بری داخل همون ویو و خودت اون رو بررسی کنی
