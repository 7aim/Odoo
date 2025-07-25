# Odoo Development: Sıfırdan Peşəkara

## Mündəricat

1. **Giriş**
   - Odoo nədir?
   - Odoo-nun tarixi və inkişafı
   - Odoo Community və Enterprise versiyaları
   - Odoo-nun arxitektura icmalı

2. **İnkişaf Mühitinin Qurulması**
   - Odoo 18-in quraşdırılması
   - İnkişaf verilənlər bazasının yaradılması
   - Əsas konfiqurasiya
   - İnkişaf alətləri və IDE-nin qurulması

3. **Odoo-nun Əsasları**
   - Modullar haqqında anlayış
   - Modul strukturu
   - Əsas varislik mexanizmləri
   - Əsas XML yazıları

4. **Modellər və Sahələr**
   - Modellərin yaradılması
   - Sahə növləri
   - Əlaqəli sahələr
   - Hesablanmış sahələr və metodlar

5. **Görünüşlər (Views)**
   - Form görünüşləri
   - Siyahı/ağac görünüşləri
   - Axtarış görünüşləri
   - Kanban görünüşləri
   - Təqvim görünüşləri
   - Digər görünüş növləri

6. **Fəaliyyətlər və Menyular**
   - Pəncərə fəaliyyətləri
   - Server fəaliyyətləri
   - URL fəaliyyətləri
   - Menyuların yaradılması
   - Giriş hüquqları və qaydaları

7. **Hesabatlar**
   - QWeb hesabatları
   - PDF hesabatları
   - Hesabat düzəlişləri

8. **Biznes Məntiq**
   - ORM metodları
   - İş axınları və vəziyyətlər
   - Məhdudiyyətlər və validasiyalar
   - Onchange metodları

9. **Sehrbazlar (Wizards)**
   - Sehrbazların yaradılması
   - Çox addımlı sehrbazlar
   - Keçici modellər

10. **Web Kontrolerlər və Marşrutlar**
    - Əsas kontrollerlər
    - Marşrutlar və URL-lər
    - Şablon renderingi

11. **Odoo-da JavaScript Əsasları**
    - Widget yaratma
    - JavaScript varisliyi
    - Odoo-da ümumi JavaScript nümunələri

12. **Ümumi Düzəliş Ssenariləri**
    - Mövcud modulların genişləndirilməsi
    - Yeni funksionallıqların yaradılması
    - Digər modullarla inteqrasiya

13. **Debugging və Problemlərin Həlli**
    - Loqlaşdırma
    - Debugging texnikaları
    - Ümumi problemlər və həlləri

14. **Yerləşdirmə Əsasları**
    - İstehsal üçün konfiqurasiya
    - Əsas təhlükəsizlik mülahizələri
    - Yeniləmələr və texniki xidmət

---

## 1. Giriş

### Odoo nədir?

Odoo, keçmişdə OpenERP kimi tanınan, açıq qaynaq biznes tətbiqləri dəstidir. Bu, şirkətlərə müxtəlif biznes ehtiyaclarını idarə etməyə imkan verən inteqrasiya olunmuş proqram təminatı həllidir. Odoo modulyar quruluşa malikdir və mühasibat, satış, CRM, eCommerce, anbar, istehsal, layihə idarəetməsi və daha çox sahələri əhatə edən 40-dan çox əsas tətbiqi özündə birləşdirir.

Odoo-nun ən güclü cəhətlərindən biri onun çevikliyidir. Müəssisələr öz ehtiyaclarına uyğun olaraq modulları seçə, konfiqurasiya edə və ya özəlləşdirə bilərlər. Bu, kiçik şirkətlərdən tutmuş böyük korporasiyalara qədər müxtəlif ölçülü təşkilatlar üçün Odoo-nu ideal həll edir.

### Odoo-nun tarixi və inkişafı

Odoo-nun tarixi 2005-ci ildə Fabien Pinckaers tərəfindən TinyERP adı ilə başlamışdır. O zaman Fabien sadə və istifadəçi dostu bir ERP sistemi yaratmaq istəyirdi. 2009-cu ildə şirkət OpenERP adını aldı və 2014-cü ildə isə Odoo adı ilə yenidən brendləşdirildi. Bu ad dəyişikliyi şirkətin ERP-dən kənara çıxan genişlənmiş funksionallığını əks etdirirdi.

İllər ərzində Odoo sürətlə inkişaf etdi və beynəlxalq icma tərəfindən dəstəklənən güclü bir platformaya çevrildi. Hər yeni versiya ilə yeni modullar və təkmilləşdirilmiş funksionallıqlar əlavə edildi. Hazırda Odoo 18 versiyası ən son versiya olaraq, daha yaxşı istifadəçi təcrübəsi, yeni funksionallıqlar və artan performans təqdim edir.

### Odoo Community və Enterprise versiyaları

Odoo iki əsas versiyada mövcuddur: Community və Enterprise.

**Odoo Community Edition (CE)**: Bu, tamamilə pulsuz və açıq qaynaqlıdır, GNU LGPL lisenziyası altında yayılır. İcma versiyası əsas funksionallıqları təqdim edir, lakin daha qabaqcıl xüsusiyyətlər və xidmətlər olmadan. Bu versiya kiçik şirkətlər, startaplar və ya Odoo-nu sınaqdan keçirmək istəyənlər üçün idealdır.

**Odoo Enterprise Edition (EE)**: Bu, ödənişli versiya olub, əlavə modullar, funksionallıqlar və xidmətlər təqdim edir. Enterprise versiyası mobil tətbiqlər, hesabat panelləri, daha çox inteqrasiya imkanları, VoIP inteqrasiyası və rəsmi texniki dəstək kimi üstünlüklərə malikdir.

İnkişaf etdirici kimi, hər iki versiya ilə işləməyi öyrənmək vacibdir, çünki fərqlər əsasən funksionallıq səviyyəsindədir, nəinki texniki infrastrukturda.

### Odoo-nun arxitektura icmalı

Odoo, üç təbəqəli arxitektura əsasında qurulmuşdur:

1. **Verilənlər bazası təbəqəsi**: Odoo PostgreSQL verilənlər bazasından istifadə edir. PostgreSQL açıq mənbəli, güclü, obyekt-əlaqəli verilənlər bazası sistemidir və Odoo-nun bütün verilənləri burada saxlanılır.

2. **Server təbəqəsi**: Odoo serveri Python dilində yazılmışdır və biznes məntiqini idarə edir. Server, verilənlər bazası ilə əlaqə saxlayır və istifadəçi interfeysi ilə qarşılıqlı təsir göstərir.

3. **İstifadəçi interfeysi təbəqəsi**: Odoo veb interfeysi HTML, CSS və JavaScript istifadə edərək qurulmuşdur. Son versiyalarda Odoo, daha yaxşı istifadəçi təcrübəsi üçün modern JavaScript framework-lərdən istifadə edir.

Bu arxitektura Odoo-ya miqyaslanma, çeviklik və genişlənmə imkanı verir. Modul sistemi sayəsində, inkişaf etdiricilər mövcud funksionallığı genişləndirə və ya tamamilə yeni funksionallıq əlavə edə bilərlər.

Odoo həmçinin ORM (Object-Relational Mapping) sistemindən istifadə edir, bu da inkişaf etdiricilərə birbaşa SQL əvəzinə Python obyektləri ilə işləməyə imkan verir. Bu, inkişaf prosesini daha sürətli və təhlükəsiz edir.

---

## 2. İnkişaf Mühitinin Qurulması

Odoo ilə işləməyə başlamadan əvvəl, inkişaf mühitimizi düzgün qurmağımız lazımdır. Bu bölümdə Odoo 18-in quraşdırılması, inkişaf verilənlər bazasının yaradılması və lazımi alətlərin quraşdırılması prosesini addım-addım izah edəcəyik.

### Odoo 18-in quraşdırılması

Odoo-nu müxtəlif üsullarla quraşdırmaq mümkündür. Bu bölümdə əsas quraşdırma üsullarını nəzərdən keçirəcəyik. Siz öz ehtiyaclarınıza və inkişaf mühitinizə ən uyğun olanı seçə bilərsiniz.

#### 1. Odoo-nu Git ilə mənbədən quraşdırma

Bu üsul inkişaf etdiricilər üçün ən çevik və məqsədəuyğun üsuldur, çünki kodda birbaşa dəyişikliklər etməyə imkan verir.

**Tələblər:**
- Linux/Mac/Windows işlətmə sistemi (Linux tövsiyə olunur)
- Git
- Python 3.10 və ya daha yuxarı versiya
- PostgreSQL 12 və ya daha yuxarı versiya
- Əlavə Python paketləri

**Addımlar:**

1. İlk öncə, lazımi paketləri quraşdırın (Ubuntu/Debian üçün nümunə):

```bash
sudo apt update
sudo apt install git python3-pip python3-dev python3-venv python3-wheel libxslt-dev libzip-dev libldap2-dev libsasl2-dev python3-setuptools node-less libjpeg-dev libpq-dev
```

2. PostgreSQL-i quraşdırın:

```bash
sudo apt install postgresql postgresql-client
```

3. Git deposunu klonlayın:

```bash
git clone https://github.com/odoo/odoo.git --depth 1 --branch 18.0 --single-branch odoo18
```

4. Virtual mühit yaradın və aktivləşdirin:

```bash
cd odoo18
python3 -m venv venv
source venv/bin/activate
```

5. Tələb olunan Python paketlərini quraşdırın:

```bash
pip install -r requirements.txt
```

6. Odoo istifadəçisi və verilənlər bazası yaradın:

```bash
sudo -u postgres createuser -s $USER
createdb odoo18_dev
```

7. Odoo-nu işə salın:

```bash
python3 odoo-bin -d odoo18_dev -i base --without-demo=all
```

#### 2. Docker ilə quraşdırma

Docker, Odoo-nu sürətli və izolyasiya olunmuş şəkildə quraşdırmağa imkan verir. Bu üsul xüsusilə müxtəlif Odoo versiyaları ilə işləyərkən faydalıdır.

**Tələblər:**
- Docker
- Docker Compose

**Addımlar:**

1. Docker və Docker Compose quraşdırın (əgər hələ quraşdırmamısınızsa).

2. `docker-compose.yml` faylını yaradın:

```yaml
version: '3'
services:
  db:
    image: postgres:14
    environment:
      - POSTGRES_DB=postgres
      - POSTGRES_PASSWORD=odoo
      - POSTGRES_USER=odoo
    volumes:
      - odoo18-db-data:/var/lib/postgresql/data
    networks:
      - odoo18-network

  odoo:
    image: odoo:18.0
    depends_on:
      - db
    ports:
      - "8069:8069"
    volumes:
      - ./addons:/mnt/extra-addons
      - ./etc:/etc/odoo
      - odoo18-web-data:/var/lib/odoo
    environment:
      - POSTGRES_DB=postgres
      - POSTGRES_PASSWORD=odoo
      - POSTGRES_USER=odoo
    networks:
      - odoo18-network

networks:
  odoo18-network:

volumes:
  odoo18-db-data:
  odoo18-web-data:
```

3. Konteyneri başladın:

```bash
docker-compose up -d
```

4. Brauzerdə `http://localhost:8069` ünvanına daxil olun və Odoo quraşdırma sehrbazını tamamlayın.

#### 3. Windows üçün quraşdırma spesifikasiyaları

Windows istifadəçiləri üçün əlavə addımlar tələb oluna bilər:

1. Python-u [python.org](https://www.python.org/) saytından yükləyin və quraşdırın.
2. PostgreSQL-i [postgresql.org](https://www.postgresql.org/) saytından yükləyin və quraşdırın.
3. Git-i [git-scm.com](https://git-scm.com/) saytından yükləyin və quraşdırın.

Windows üçün WSL2 (Windows Subsystem for Linux 2) istifadə etmək tövsiyə olunur, çünki bu, Linux mühitində işləməyə imkan verir və Odoo inkişafı üçün daha uyğundur.

### İnkişaf verilənlər bazasının yaradılması

Odoo-nu quraşdırdıqdan sonra, inkişaf üçün ayrıca verilənlər bazası yaratmaq yaxşı təcrübədir. Bu, istehsal verilənlərinə təsir etmədən təhlükəsiz təcrübələr aparmağa imkan verir.

#### Yeni verilənlər bazası yaratma

**CLI ilə:**

```bash
createdb odoo18_dev
```

**Odoo interfeysi ilə:**

1. Brauzerdə `http://localhost:8069/web/database/manager` ünvanına keçin.
2. "Create Database" seçin.
3. Verilənlər bazası adını, ana istifadəçi adını və şifrəni daxil edin.
4. "Create Database" düyməsini klikləyin.

#### Demo məlumatlarla verilənlər bazası yaratma

Təlim və sınaq məqsədləri üçün demo məlumatlarla verilənlər bazası yaratmaq faydalı ola bilər:

```bash
python3 odoo-bin -d odoo18_demo -i base --demo=all
```

və ya Odoo interfeysi vasitəsilə verilənlər bazası yaradarkən "Load demonstration data" seçimini işarələyin.

### Əsas konfiqurasiya

Odoo-nu effektiv şəkildə inkişaf etdirmək üçün bir neçə əsas konfiqurasiya parametrini tənzimləmək lazımdır.

#### Konfiqurasiya faylı

Odoo serveri üçün konfiqurasiya faylı yaradaq. Bu, serverin necə işləməsini tənzimləyəcək.

`odoo.conf` faylını yaradın:

```ini
[options]
addons_path = /path/to/odoo18/addons,/path/to/custom_addons
admin_passwd = admin_password
db_host = localhost
db_port = 5432
db_user = odoo
db_password = odoo
http_port = 8069
logfile = /path/to/logfile.log
log_level = debug
dev_mode = true
```

Əsas parametrlərin izahı:
- `addons_path`: Odoo-nun əlavələri (modulları) axtaracağı qovluqların siyahısı.
- `admin_passwd`: Verilənlər bazası idarəetmə interfeysi üçün admin şifrəsi.
- `db_host`, `db_port`, `db_user`, `db_password`: PostgreSQL konfiqurasiyası.
- `http_port`: Odoo serverinin dinləyəcəyi port.
- `logfile`: Log faylının yeri.
- `log_level`: Loglama səviyyəsi (debug, info, warning, error, critical).
- `dev_mode`: İnkişaf rejimini aktivləşdirir, bu da assets-lərin yenidən yüklənməsini və digər inkişaf xüsusiyyətlərini təmin edir.

#### İnkişaf rejimi parametrləri

İnkişaf zamanı əlavə parametrlər faydalı ola bilər:

```bash
python3 odoo-bin -d odoo18_dev --dev=all --log-level=debug
```

`--dev=all` parametri:
- Assets-lərin avtomatik yenilənməsi
- Şablonların yenilənməsi
- Xəta izləmə
- Əlavə loqlaşdırma

### İnkişaf alətləri və IDE-nin qurulması

Effektiv Odoo inkişafı üçün düzgün alətlər vacibdir. Bu bölümdə ən populyar və məhsuldar alətləri və IDE-ləri nəzərdən keçirəcəyik.

#### IDE seçimi

**Visual Studio Code (VS Code)**

VS Code, Odoo inkişafı üçün ən populyar və çevik IDE-lərdən biridir. Odoo inkişafını dəstəkləyən bəzi əsas əlavələr:

- Python (Microsoft)
- Pylint
- XML Tools
- Odoo Snippets
- GitLens
- Docker

VS Code-u quraşdırdıqdan sonra aşağıdakı Python əlavə tənzimləmələrini edin:
```json
{
    "python.linting.enabled": true,
    "python.linting.pylintEnabled": true,
    "python.linting.pylintArgs": [
        "--load-plugins=pylint_odoo"
    ]
}
```

Pylint Odoo pluginini quraşdırın:
```bash
pip install pylint-odoo
```

**PyCharm**

PyCharm Professional, xüsusən də böyük Odoo layihələri üçün güclü bir seçimdir. Python, XML və JavaScript dəstəyi ilə bir çox funksiya təqdim edir.

PyCharm'da Odoo inkişafı üçün tənzimləmələr:
1. Python interpretatorunu layihənizin virtual mühitinə yönləndirin.
2. Layihənizdəki Odoo qovluğunu və öz modullarınızı əlavə edin.
3. Run konfiqurasiyasında Odoo-nun başlatma parametrlərini əlavə edin:
   ```
   Parameters: -c /path/to/odoo.conf -d odoo18_dev
   ```

#### Faydalı əlavə alətlər

**Git**

Versiya idarəetmə sistemi kimi Git əvəzolunmazdır. Git CLI ilə yanaşı, GUI əsaslı Git klientləri də mövcuddur:
- GitKraken
- SourceTree
- Github Desktop

**pgAdmin**

PostgreSQL verilənlər bazası idarəetməsi üçün pgAdmin güclü və istifadəçi dostu interfeysdir. Verilənlər bazası strukturunu görüntüləmək və sorğular icra etmək üçün faydalıdır.

**Postman**

Odoo REST API ilə işləyərkən Postman, API sorğularını sınaqdan keçirmək və debug etmək üçün əla bir alətdir.

### İnkişaf Mühitinin Sınaqdan Keçirilməsi

İnkişaf mühitinizi qurduqdan sonra, hər şeyin düzgün işlədiyini yoxlamaq üçün sadə bir sınaq modulunu yaradaq.

1. Öz əlavə modullarınız üçün qovluq yaradın:

```bash
mkdir -p ~/custom_addons/test_module
```

2. `__manifest__.py` faylını yaradın:

```python
{
    'name': 'Test Module',
    'version': '1.0',
    'summary': 'Test module for Odoo 18',
    'description': 'A simple test module for Odoo 18 development',
    'author': 'Your Name',
    'category': 'Uncategorized',
    'depends': ['base'],
    'data': [
        'views/views.xml',
    ],
    'application': True,
    'installable': True,
}
```

3. `__init__.py` faylını yaradın:

```python
from . import models
```

4. `models` qovluğunu və onun içində faylları yaradın:

```bash
mkdir -p ~/custom_addons/test_module/models
```

5. `models/__init__.py` faylını yaradın:

```python
from . import test_model
```

6. `models/test_model.py` faylını yaradın:

```python
from odoo import models, fields, api

class TestModel(models.Model):
    _name = 'test.model'
    _description = 'Test Model'

    name = fields.Char(string='Name', required=True)
    description = fields.Text(string='Description')
    date = fields.Date(string='Date')
```

7. `views` qovluğunu və görünüş faylını yaradın:

```bash
mkdir -p ~/custom_addons/test_module/views
```

8. `views/views.xml` faylını yaradın:

```xml
<?xml version="1.0" encoding="utf-8"?>
<odoo>
    <record id="view_test_model_tree" model="ir.ui.view">
        <field name="name">test.model.tree</field>
        <field name="model">test.model</field>
        <field name="arch" type="xml">
            <tree>
                <field name="name"/>
                <field name="date"/>
            </tree>
        </field>
    </record>

    <record id="view_test_model_form" model="ir.ui.view">
        <field name="name">test.model.form</field>
        <field name="model">test.model</field>
        <field name="arch" type="xml">
            <form>
                <sheet>
                    <group>
                        <field name="name"/>
                        <field name="date"/>
                        <field name="description"/>
                    </group>
                </sheet>
            </form>
        </field>
    </record>

    <record id="action_test_model" model="ir.actions.act_window">
        <field name="name">Test Model</field>
        <field name="res_model">test.model</field>
        <field name="view_mode">tree,form</field>
    </record>

    <menuitem id="menu_test_root" name="Test Module"/>
    <menuitem id="menu_test_model" name="Test Models" parent="menu_test_root" action="action_test_model"/>
</odoo>
```

9. Odoo-ya əlavələr yolunu göstərin:

Odoo konfiqurasiya faylında `addons_path` parametrini düzəltdiyinizdən əmin olun:
```ini
addons_path = /path/to/odoo18/addons,/path/to/custom_addons
```

10. Odoo serveri başladın:

```bash
python3 odoo-bin -c /path/to/odoo.conf -d odoo18_dev
```

11. Brauzerdə Odoo-ya daxil olun və "Apps" menyusuna keçin. "Test Module" axtarın və quraşdırın.

Quraşdırmadan sonra yeni "Test Module" menyusu görünməlidir. Bu modulda verilənlər yarada bilməyiniz inkişaf mühitinizin düzgün qurulduğunu göstərir.

### Nəticə

Bu bölümdə Odoo 18 üçün inkişaf mühitinin qurulması prosesini addım-addım izah etdik. Müxtəlif quraşdırma üsullarını, verilənlər bazasının yaradılmasını, konfiqurasiya parametrlərini və lazımi inkişaf alətlərini nəzərdən keçirdik. Həmçinin sadə bir test modulu yaradaraq, mühitimizin işlək olduğunu sınaqdan keçirdik.

İnkişaf mühitini düzgün qurmaq, Odoo ilə işləməyə başlamaq üçün əsas addımdır. Növbəti bölümdə Odoo-nun əsaslarını və modulların strukturunu daha ətraflı araşdıracağıq.

---

**Praktiki tapşırıq:**

1. Odoo 18-i yuxarıda göstərilən üsullardan birini istifadə edərək quraşdırın.
2. İki ayrı verilənlər bazası yaradın: biri demo məlumatlarla, biri isə boş.
3. Test modulunu yaradın və inkişaf mühitinizin işlədiyini təsdiqləyin.
4. VS Code və ya PyCharm IDE-ni konfiqurasiya edin.
5. Quraşdırma zamanı qarşılaşdığınız çətinlikləri və həll yollarını qeyd edin.

## 3. Odoo-nun Əsasları

Bu bölümdə Odoo-nun fundamental konsepsiyalarını araşdıracağıq. Modulların strukturu, varislik mexanizmləri və əsas XML yazıları kimi mövzular bu bölümdə əhatə olunacaq. Bu əsas bilikləri mənimsəmək, gələcəkdə daha mürəkkəb Odoo inkişaf tapşırıqlarını həyata keçirmək üçün möhkəm təməl yaradacaq.

### Modullar haqqında anlayış

#### Modul nədir?

Odoo-da modul, xüsusi bir biznes ehtiyacını qarşılamaq üçün yaradılmış funksional bölmədir. Texniki baxımdan modul, Python paketinə bənzər şəkildə təşkil edilmiş qovluq strukturudur. Odoo-nun modular quruluşu sayəsində, sistemin əsas funksionallığını dəyişdirmədən yeni xüsusiyyətlər əlavə etmək və mövcud funksionallığı genişləndirmək mümkündür.

Modullar aşağıdakı məqsədlər üçün istifadə olunur:
- Yeni biznes funksionallığı əlavə etmək
- Mövcud biznes funksionallığını genişləndirmək və ya dəyişdirmək
- Xüsusi hesabatlar və görünüşlər yaratmaq
- Üçüncü tərəf sistemlərlə inteqrasiya etmək
- İstifadəçi interfeysi və təcrübəsini təkmilləşdirmək

#### Modulların növləri

Odoo-da modullar əsasən üç növə bölünür:

1. **Əsas modullar**: Odoo-nun özü tərəfindən təqdim edilən modullar (`base`, `web`, `mail` və s.). Bunlar Odoo-nun əsas funksionallığını təmin edir.

2. **Applikasiya modulları**: Müəyyən bir biznes sahəsini əhatə edən modullar (`crm`, `sale`, `purchase`, `mrp` və s.). Bu modullar geniş funksionallıq təqdim edir və adətən, istifadəçi interfeysi menyularında birbaşa görünür.

3. **Texniki modullar**: Bu modullar birbaşa biznes funksionallığı təqdim etmir, lakin digər modullar üçün texniki funksiyalar və genişlənmə nöqtələri təmin edir (məsələn, `base_setup`, `web_editor`).

#### Modulu necə tapmaq olar?

Odoo-da modulu bir neçə üsulla tapmaq olar:

1. **İnterfeysə əsaslanan yanaşma**: "Apps" menyusunda modulların siyahısı və təsvirləri göstərilir.

2. **Qovluq strukturu**: Odoo quraşdırma qovluğunuzda `addons` qovluğunda və ya `addons_path` parametrində göstərilən qovluqlarda modullar yerləşir.

3. **Texniki adına görə**: Modulu texniki adına (məsələn, `sale`, `crm`) görə axtarmaq olar. Bu ad modul qovluğunun adı ilə eynidir.

### Modul strukturu

Odoo modulunun standart strukturu ilə tanış olaq. Modul, müəyyən bir struktura malik qovluqdur və bu struktur Odoo tərəfindən tanına bilməsi üçün vacibdir.

#### Əsas fayl və qovluqlar

Odoo modulunun əsas elementləri:

1. **`__init__.py`**: Python paketi üçün standart inisializasiya faylı. Bu fayl Python modullarını idxal edir.

2. **`__manifest__.py`**: Modulun təsviri və konfiqurasiyası. Bu fayl Odoo-ya modulun necə yüklənəcəyi, başqa hansı modullardan asılı olduğu və hansı məlumat fayllarının daxil ediləcəyi barədə məlumat verir.

3. **`models/`**: Bu qovluqda modelləri təyin edən Python faylları yerləşir. Adətən `models/__init__.py` faylı da olur və bu fayl digər model fayllarını idxal edir.

4. **`views/`**: XML faylları burada saxlanılır və istifadəçi interfeysi elementlərini (formalar, siyahılar, menyular və s.) təyin edir.

5. **`data/`**: Modul quraşdırılarkən yüklənəcək məlumatlar (təriflər, konfiqurasiyalar, demo məlumatları) burada saxlanılır.

6. **`security/`**: Təhlükəsizliklə əlaqəli fayllar, o cümlədən giriş hüquqları qaydaları və qrupları burada təyin edilir.

7. **`static/`**: Statik fayllar (JavaScript, CSS, şəkillər və s.) burada saxlanılır.

8. **`controllers/`**: HTTP sorğularını idarə edən kontrollerlər burada təyin edilir.

9. **`wizards/`**: Sehrbazlar (istifadəçi tərəfindən doldurulması lazım olan çox addımlı formalar) burada təyin edilir.

10. **`report/`**: Hesabatlar və onların dizaynı burada təyin edilir.

11. **`i18n/`**: Tərcümə faylları burada saxlanılır.

#### Nümunə modul strukturu

Sadə bir satış sifarişi genişlənməsi modulu üçün qovluq strukturu belə ola bilər:

```
sale_extension/
│
├── __init__.py
├── __manifest__.py
│
├── models/
│   ├── __init__.py
│   └── sale_order.py
│
├── views/
│   ├── sale_order_views.xml
│   └── menu_views.xml
│
├── data/
│   └── sale_data.xml
│
├── security/
│   ├── ir.model.access.csv
│   └── sale_security.xml
│
└── static/
    ├── description/
    │   └── icon.png
    └── src/
        ├── js/
        │   └── sale_script.js
        └── css/
            └── sale_style.css
```

#### `__manifest__.py` faylının strukturu

`__manifest__.py` faylı, modulunuz haqqında Odoo-ya məlumat verən əsas fayl hesab olunur. Bu faylın düzgün tərtib edilməsi vacibdir. Aşağıda tipik bir `__manifest__.py` faylının strukturu göstərilmişdir:

```python
{
    'name': 'Satış Sifarişi Genişlənməsi',       # Modulun başlığı
    'version': '1.0',                           # Versiya nömrəsi
    'summary': 'Satış sifarişlərini genişləndirir', # Qısa təsvir
    'description': """
        Bu modul satış sifarişlərini genişləndirir:
        - Əlavə sahələr
        - Xüsusi hesabat
        - İnteqrasiya funksiyaları
    """,                                         # Ətraflı təsvir
    'author': 'Sizin Adınız',                   # Müəllif adı
    'website': 'https://www.sizinsayt.com',     # Müəllif veb saytı
    'category': 'Sales',                        # Modul kateqoriyası
    'depends': [                                # Asılılıqlar
        'base',
        'sale',
        'stock',
    ],
    'data': [                                   # Data faylları
        'security/sale_security.xml',
        'security/ir.model.access.csv',
        'views/sale_order_views.xml',
        'views/menu_views.xml',
        'data/sale_data.xml',
    ],
    'demo': [                                   # Demo məlumatlar (optional)
        'demo/sale_demo.xml',
    ],
    'qweb': [                                   # QWeb şablonları (JS üçün)
        'static/src/xml/sale_dashboard.xml',
    ],
    'assets': {                                 # Odoo 15+ üçün asset tərifləri
        'web.assets_backend': [
            'sale_extension/static/src/js/sale_script.js',
            'sale_extension/static/src/css/sale_style.css',
        ],
    },
    'application': False,                       # Applikasiya modu
    'installable': True,                        # Quraşdırıla bilər
    'auto_install': False,                      # Avtomatik quraşdırılma
    'license': 'LGPL-3',                        # Lisenziya
}
```

`__manifest__.py` faylındakı əsas sahələrin izahı:

- **name**: Modulun başlığı, istifadəçiyə göstərilir.
- **version**: Modulun versiyası.
- **summary**: Qısa təsvir, modulun əsas məqsədini göstərir.
- **description**: Modulun ətraflı təsviri.
- **author**: Modulun müəllifi.
- **website**: Müəllifin veb saytı.
- **category**: Modulun aid olduğu kateqoriya.
- **depends**: Bu modul üçün lazım olan digər modullar.
- **data**: Quraşdırma zamanı yüklənəcək fayllar.
- **demo**: Demo məlumatları olan fayllar.
- **qweb**: QWeb şablon faylları.
- **assets**: JavaScript və CSS fayllarının yüklənməsini idarə edir.
- **application**: `True` olduqda, bu modul applikasiya kimi işarələnir.
- **installable**: Modulun quraşdırıla biləcəyini göstərir.
- **auto_install**: `True` olduqda, bu modul asılılıqları quraşdırıldıqda avtomatik quraşdırılır.

### Əsas varislik mexanizmləri

Odoo-nun ən güclü xüsusiyyətlərindən biri onun varislik mexanizmidir. Bu, mövcud kodu təkrarlamadan və əsas kodu dəyişdirmədən funksionallığı genişləndirməyə imkan verir.

#### Model varisliliyi

Odoo-da üç əsas model varislik mexanizmi var:

1. **Klassik varislik**:
   Python-un standart varislik mexanizmindən istifadə edir. Yeni model yaradarkən mövcud modelin bütün xüsusiyyətlərini miras alır.

   ```python
   class SaleOrder(models.Model):
       _name = 'sale.order'
       # sahələr və metodlar...

   class CustomSaleOrder(SaleOrder):
       _name = 'custom.sale.order'
       # əlavə sahələr və metodlar...
   ```

2. **Genişlənmə varisliliyi**:
   Mövcud modeli genişləndirmək üçün istifadə olunur. `_inherit` atributundan istifadə edilir, lakin `_name` təyin edilmir (və ya eyni ad istifadə edilir).

   ```python
   class SaleOrderExtension(models.Model):
       _inherit = 'sale.order'
       
       # Yeni sahələr
       new_field = fields.Char(string='Yeni Sahə')
       
       # Mövcud metodu override etmək
       def action_confirm(self):
           # Öz məntiqimiz
           return super(SaleOrderExtension, self).action_confirm()
   ```

3. **Delegasiya varisliliyi**:
   Bu mexanizm, bir modelin sahə və metodlarını digər modelə delegasiya etməyə imkan verir. `_inherits` atributundan istifadə edilir.

   ```python
   class SaleSubscription(models.Model):
       _name = 'sale.subscription'
       _inherits = {'sale.order': 'sale_order_id'}
       
       sale_order_id = fields.Many2one(
           'sale.order', 
           required=True, 
           ondelete='cascade'
       )
       # Əlavə sahələr...
   ```

#### Görünüşlərdə varislik

Odoo-da görünüşləri də genişləndirmək mümkündür. Bu, mövcud görünüşləri dəyişdirmək və ya genişləndirmək üçün istifadə olunur.

1. **Görünüşün yenidən təyin edilməsi**:

   ```xml
   <record id="view_order_form_inherit" model="ir.ui.view">
       <field name="name">sale.order.form.inherit</field>
       <field name="model">sale.order</field>
       <field name="inherit_id" ref="sale.view_order_form"/>
       <field name="arch" type="xml">
           <!-- XPath istifadə edərək mövcud elementi tapmaq -->
           <xpath expr="//field[@name='partner_id']" position="after">
               <field name="new_field"/>
           </xpath>
           
           <!-- Qısa sintaksis istifadə edərək -->
           <field name="date_order" position="attributes">
               <attribute name="string">Sifariş Tarixi</attribute>
               <attribute name="required">True</attribute>
           </field>
       </field>
   </record>
   ```

2. **Əsas `position` atributları**:
   - `after`: Tapılan elementin sonuna əlavə edir
   - `before`: Tapılan elementin əvvəlinə əlavə edir
   - `inside`: Tapılan elementin içərisinə əlavə edir
   - `replace`: Tapılan elementi əvəz edir
   - `attributes`: Tapılan elementin atributlarını dəyişir

#### Fəaliyyətlərin varisliliyi

Odoo-da fəaliyyətləri (actions) də genişləndirmək mümkündür. Bu, mövcud fəaliyyətləri dəyişdirmək üçün istifadə olunur.

```xml
<record id="sale.action_orders" model="ir.actions.act_window">
    <field name="context">{'search_default_my_sale_orders_filter': 1}</field>
    <field name="domain">[('state', 'not in', ('draft', 'cancel'))]</field>
</record>
```

### Əsas XML yazıları

Odoo-da bir çox konfiqurasiya və tərifləmələr XML faylları vasitəsilə edilir. Bu bölümdə ən çox istifadə olunan XML yazılarını nəzərdən keçirəcəyik.

#### Verilənlər tərifləri

XML, Odoo-da verilənləri təyin etmək üçün istifadə olunur:

```xml
<odoo>
    <data>
        <!-- Yeni qeyd yaratmaq -->
        <record id="custom_product_category" model="product.category">
            <field name="name">Xüsusi Kateqoriya</field>
            <field name="parent_id" ref="product.product_category_all"/>
        </record>
        
        <!-- Mövcud qeydi düzəltmək -->
        <record id="product.product_category_all" model="product.category">
            <field name="name">Bütün Məhsullar (Düzəliş)</field>
        </record>
    </data>
</odoo>
```

#### Görünüşlər

Görünüşlər, istifadəçi interfeysi elementlərini təyin etmək üçün istifadə olunur:

1. **Form görünüşü**:

   ```xml
   <record id="view_partner_form" model="ir.ui.view">
       <field name="name">res.partner.form</field>
       <field name="model">res.partner</field>
       <field name="arch" type="xml">
           <form>
               <sheet>
                   <group>
                       <field name="name"/>
                       <field name="email"/>
                       <field name="phone"/>
                   </group>
               </sheet>
           </form>
       </field>
   </record>
   ```

2. **Siyahı (tree) görünüşü**:

   ```xml
   <record id="view_partner_tree" model="ir.ui.view">
       <field name="name">res.partner.tree</field>
       <field name="model">res.partner</field>
       <field name="arch" type="xml">
           <tree>
               <field name="name"/>
               <field name="email"/>
               <field name="phone"/>
           </tree>
       </field>
   </record>
   ```

3. **Axtarış görünüşü**:

   ```xml
   <record id="view_partner_search" model="ir.ui.view">
       <field name="name">res.partner.search</field>
       <field name="model">res.partner</field>
       <field name="arch" type="xml">
           <search>
               <field name="name"/>
               <field name="email"/>
               <filter string="Müştərilər" name="customers" domain="[('customer_rank', '>', 0)]"/>
               <group expand="0" string="Qruplaşdır">
                   <filter string="Ölkə" name="country" context="{'group_by': 'country_id'}"/>
               </group>
           </search>
       </field>
   </record>
   ```

#### Fəaliyyətlər və Menyular

Fəaliyyətlər və menyular istifadəçi interfeysi naviqasiyasını təyin edir:

1. **Pəncərə fəaliyyəti**:

   ```xml
   <record id="action_partners" model="ir.actions.act_window">
       <field name="name">Tərəfdaşlar</field>
       <field name="res_model">res.partner</field>
       <field name="view_mode">tree,form</field>
       <field name="context">{'search_default_customers': 1}</field>
       <field name="help" type="html">
           <p class="o_view_nocontent_smiling_face">
               Yeni tərəfdaş yaradın
           </p>
       </field>
   </record>
   ```

2. **Menyu elementi**:

   ```xml
   <menuitem id="menu_partner_root" name="Tərəfdaşlar" sequence="10"/>
   
   <menuitem id="menu_partner" name="Tərəfdaşlar" 
             parent="menu_partner_root" 
             action="action_partners" 
             sequence="10"/>
   ```

#### Təhlükəsizlik tərifləri

Təhlükəsizlik tərifləri giriş hüquqlarını və qaydalarını təyin edir:

1. **Giriş hüquqları**:

   `ir.model.access.csv` faylı:
   ```csv
   id,name,model_id:id,group_id:id,perm_read,perm_write,perm_create,perm_unlink
   access_custom_model_user,custom.model.user,model_custom_model,base.group_user,1,1,1,0
   access_custom_model_manager,custom.model.manager,model_custom_model,base.group_system,1,1,1,1
   ```

2. **Qayda-əsaslı təhlükəsizlik**:

   ```xml
   <record id="rule_custom_model_own_documents" model="ir.rule">
       <field name="name">Xüsusi Model: öz sənədləri</field>
       <field name="model_id" ref="model_custom_model"/>
       <field name="domain_force">[('create_uid', '=', user.id)]</field>
       <field name="groups" eval="[(4, ref('base.group_user'))]"/>
   </record>
   ```

#### Server fəaliyyətləri

Server fəaliyyətləri, serverdə icra olunan funksiyaları təyin edir:

```xml
<record id="action_check_stock" model="ir.actions.server">
    <field name="name">Stoku Yoxla</field>
    <field name="model_id" ref="model_product_product"/>
    <field name="binding_model_id" ref="model_product_product"/>
    <field name="state">code</field>
    <field name="code">
        for record in records:
            record.check_stock()
    </field>
</record>
```

### Modul yaratma və quraşdırma

İndi bütün öyrəndiklərimizi tətbiq edərək sadə bir modul yaradaq. Bu nümunə, Odoo-da modul yaratma və quraşdırma prosesini başa düşməyə kömək edəcək.

#### Modul üçün tələblər

Müştəri sifarişlərini izləmək üçün sadə bir modul yaradaq. Modul aşağıdakı funksionallığı təmin etməlidir:

1. Müştəri sifarişlərini saxlamaq üçün yeni model
2. Sifariş elementlərini saxlamaq üçün əlavə model
3. Sifarişləri göstərmək üçün form və siyahı görünüşləri
4. Sifarişlərə giriş üçün menyu

#### Modul strukturunun yaradılması

1. Əvvəlcə modula uyğun qovluq strukturunu yaradaq:

```
customer_orders/
│
├── __init__.py
├── __manifest__.py
│
├── models/
│   ├── __init__.py
│   ├── customer_order.py
│   └── order_line.py
│
├── views/
│   ├── customer_order_views.xml
│   └── menu_views.xml
│
└── security/
    └── ir.model.access.csv
```

2. `__manifest__.py` faylını yaradaq:

```python
{
    'name': 'Müştəri Sifarişləri',
    'version': '1.0',
    'summary': 'Müştəri sifarişlərini idarə etmək üçün modul',
    'description': """
        Bu modul müştəri sifarişlərini idarə etmək üçün istifadə olunur:
        - Sifarişlərin yaradılması və izlənməsi
        - Sifariş elementlərinin idarə edilməsi
    """,
    'author': 'Sizin Adınız',
    'category': 'Sales',
    'depends': ['base', 'product'],
    'data': [
        'security/ir.model.access.csv',
        'views/customer_order_views.xml',
        'views/menu_views.xml',
    ],
    'application': True,
    'installable': True,
}
```

3. Əsas `__init__.py` faylını yaradaq:

```python
from . import models
```

4. `models/__init__.py` faylını yaradaq:

```python
from . import customer_order
from . import order_line
```

#### Model fayllarının yaradılması

1. `models/customer_order.py` faylını yaradaq:

```python
from odoo import models, fields, api
from datetime import datetime

class CustomerOrder(models.Model):
    _name = 'customer.order'
    _description = 'Müştəri Sifarişi'
    
    name = fields.Char(string='Sifariş Referansı', required=True, copy=False, 
                       readonly=True, default=lambda self: 'Yeni')
    partner_id = fields.Many2one('res.partner', string='Müştəri', required=True)
    date_order = fields.Date(string='Sifariş Tarixi', default=fields.Date.today)
    state = fields.Selection([
        ('draft', 'Qaralama'),
        ('confirmed', 'Təsdiqlənmiş'),
        ('done', 'Tamamlanmış'),
        ('cancel', 'Ləğv edilmiş'),
    ], string='Status', default='draft')
    order_line_ids = fields.One2many('customer.order.line', 'order_id', 
                                     string='Sifariş Xətləri')
    amount_total = fields.Float(string='Ümumi Məbləğ', compute='_compute_amount_total',
                               store=True)
    
    @api.depends('order_line_ids.price_subtotal')
    def _compute_amount_total(self):
        for order in self:
            order.amount_total = sum(line.price_subtotal for line in order.order_line_ids)
    
    @api.model
    def create(self, vals):
        if vals.get('name', 'Yeni') == 'Yeni':
            vals['name'] = self.env['ir.sequence'].next_by_code('customer.order') or 'Yeni'
        return super(CustomerOrder, self).create(vals)
    
    def action_confirm(self):
        self.state = 'confirmed'
    
    def action_done(self):
        self.state = 'done'
    
    def action_cancel(self):
        self.state = 'cancel'
    
    def action_draft(self):
        self.state = 'draft'
```

2. `models/order_line.py` faylını yaradaq:

```python
from odoo import models, fields, api

class CustomerOrderLine(models.Model):
    _name = 'customer.order.line'
    _description = 'Müştəri Sifarişi Xətti'
    
    order_id = fields.Many2one('customer.order', string='Sifariş', required=True, 
                              ondelete='cascade')
    product_id = fields.Many2one('product.product', string='Məhsul', required=True)
    name = fields.Text(string='Təsvir')
    quantity = fields.Float(string='Miqdar', default=1.0)
    price_unit = fields.Float(string='Vahid Qiymət')
    price_subtotal = fields.Float(string='Ara Məbləğ', compute='_compute_price_subtotal',
                                 store=True)
    
    @api.depends('quantity', 'price_unit')
    def _compute_price_subtotal(self):
        for line in self:
            line.price_subtotal = line.quantity * line.price_unit
    
    @api.onchange('product_id')
    def _onchange_product_id(self):
        if self.product_id:
            self.name = self.product_id.name
            self.price_unit = self.product_id.list_price
```

#### Görünüş və menyu fayllarının yaradılması

1. `views/customer_order_views.xml` faylını yaradaq:

```xml
<?xml version="1.0" encoding="utf-8"?>
<odoo>
    <!-- Form Görünüşü -->
    <record id="view_customer_order_form" model="ir.ui.view">
        <field name="name">customer.order.form</field>
        <field name="model">customer.order</field>
        <field name="arch" type="xml">
            <form>
                <header>
                    <button name="action_confirm" string="Təsdiqlə" type="object" 
                            states="draft" class="oe_highlight"/>
                    <button name="action_done" string="Tamamla" type="object" 
                            states="confirmed" class="oe_highlight"/>
                    <button name="action_cancel" string="Ləğv et" type="object" 
                            states="draft,confirmed"/>
                    <button name="action_draft" string="Qaralamaya qaytar" type="object" 
                            states="cancel"/>
                    <field name="state" widget="statusbar" 
                           statusbar_visible="draft,confirmed,done"/>
                </header>
                <sheet>
                    <div class="oe_title">
                        <h1>
                            <field name="name"/>
                        </h1>
                    </div>
                    <group>
                        <group>
                            <field name="partner_id"/>
                            <field name="date_order"/>
                        </group>
                        <group>
                            <field name="amount_total"/>
                        </group>
                    </group>
                    <notebook>
                        <page string="Sifariş Xətləri">
                            <field name="order_line_ids">
                                <tree editable="bottom">
                                    <field name="product_id"/>
                                    <field name="name"/>
                                    <field name="quantity"/>
                                    <field name="price_unit"/>
                                    <field name="price_subtotal" sum="Ümumi"/>
                                </tree>
                            </field>
                        </page>
                    </notebook>
                </sheet>
            </form>
        </field>
    </record>
    
    <!-- Siyahı Görünüşü -->
    <record id="view_customer_order_tree" model="ir.ui.view">
        <field name="name">customer.order.tree</field>
        <field name="model">customer.order</field>
        <field name="arch" type="xml">
            <tree decoration-info="state == 'draft'" 
                  decoration-success="state == 'done'" 
                  decoration-muted="state == 'cancel'">
                <field name="name"/>
                <field name="partner_id"/>
                <field name="date_order"/>
                <field name="amount_total" sum="Ümumi"/>
                <field name="state"/>
            </tree>
        </field>
    </record>
    
    <!-- Axtarış Görünüşü -->
    <record id="view_customer_order_search" model="ir.ui.view">
        <field name="name">customer.order.search</field>
        <field name="model">customer.order</field>
        <field name="arch" type="xml">
            <search>
                <field name="name"/>
                <field name="partner_id"/>
                <filter string="Qaralama" name="draft" domain="[('state', '=', 'draft')]"/>
                <filter string="Təsdiqlənmiş" name="confirmed" domain="[('state', '=', 'confirmed')]"/>
                <filter string="Tamamlanmış" name="done" domain="[('state', '=', 'done')]"/>
                <filter string="Ləğv edilmiş" name="cancel" domain="[('state', '=', 'cancel')]"/>
                <group expand="0" string="Qruplaşdır">
                    <filter string="Müştəri" name="partner_id" context="{'group_by': 'partner_id'}"/>
                    <filter string="Status" name="state" context="{'group_by': 'state'}"/>
                    <filter string="Sifariş Tarixi" name="date_order" context="{'group_by': 'date_order'}"/>
                </group>
            </search>
        </field>
    </record>
    
    <!-- Pəncərə Fəaliyyəti -->
    <record id="action_customer_orders" model="ir.actions.act_window">
        <field name="name">Müştəri Sifarişləri</field>
        <field name="res_model">customer.order</field>
        <field name="view_mode">tree,form</field>
        <field name="context">{'search_default_draft': 1}</field>
        <field name="help" type="html">
            <p class="o_view_nocontent_smiling_face">
                Yeni müştəri sifarişi yaradın
            </p>
        </field>
    </record>
</odoo>
```

2. `views/menu_views.xml` faylını yaradaq:

```xml
<?xml version="1.0" encoding="utf-8"?>
<odoo>
    <!-- Əsas Menyu -->
    <menuitem id="menu_customer_order_root" 
              name="Müştəri Sifarişləri" 
              sequence="10"/>
    
    <!-- Alt Menyu -->
    <menuitem id="menu_customer_order" 
              name="Sifarişlər" 
              parent="menu_customer_order_root" 
              action="action_customer_orders" 
              sequence="10"/>
</odoo>
```

#### Təhlükəsizlik faylının yaradılması

`security/ir.model.access.csv` faylını yaradaq:

```csv
id,name,model_id:id,group_id:id,perm_read,perm_write,perm_create,perm_unlink
access_customer_order_user,customer.order.user,model_customer_order,base.group_user,1,1,1,1
access_customer_order_line_user,customer.order.line.user,model_customer_order_line,base.group_user,1,1,1,1
```

#### Modulun quraşdırılması

1. Modulun qovluğunu Odoo əlavələr yoluna (`addons_path`) əlavə edin.
2. Odoo-nu yenidən başladın.
3. Applikasiyalar menyusuna gedin və "Müştəri Sifarişləri" modulunu axtarın.
4. Modulu quraşdırın.

Quraşdırmadan sonra, əsas menyuda "Müştəri Sifarişləri" adlı yeni bir menyu elementi görünəcək. Bu menyuya klik edərək, müştəri sifarişlərini yarada və idarə edə bilərsiniz.

### Nəticə

Bu bölümdə Odoo-nun fundamental konsepsiyalarını araşdırdıq. Modulların strukturu, varislik mexanizmləri və əsas XML yazıları haqqında ətraflı məlumat əldə etdik. Eyni zamanda, sadə bir modul yaradaraq öyrəndiklərimizi praktikada tətbiq etdik.

Bu əsas biliklər, gələcəkdə daha mürəkkəb modullar yaratmaq və mövcud modulları genişləndirmək üçün möhkəm təməl yaradır. Növbəti bölümlərdə daha mürəkkəb mövzulara keçəcəyik və Odoo-nun daha qabaqcıl funksionallıqlarını araşdıracağıq.

---

**Praktiki tapşırıq:**

1. Bu bölümdə yaratdığımız "Müştəri Sifarişləri" modulunu yaradın və quraşdırın.
2. Mövcud modulda aşağıdakı əlavə funksionallıqları əlavə edin:
   - Sifariş tarixçəsini izləmək üçün qeydlər əlavə edin.
   - Sifarişlər üçün sadə bir hesabat yaradın.
   - Kanban görünüşü əlavə edin.
3. Hər hansı bir mövcud Odoo modulunu (məsələn, "crm" və ya "sale") araşdırın və onun strukturunu öyrənin.
4. Öz başınıza sadə bir modul yaradaraq, öyrəndiklərinizi tətbiq edin.

## 4. Modellər və Sahələr

Odoo-da inkişafın ən fundamental aspektlərindən biri modellər və sahələrdir. Bu bölümdə modellərin necə yaradılacağını, müxtəlif sahə tiplərini, əlaqəli sahələri və hesablanmış sahələri ətraflı şəkildə öyrənəcəyik. Bu biliklər, hər hansı bir Odoo tətbiqinin məlumat strukturunu düzgün dizayn etmək üçün əsasdır.

### Modellərin yaradılması

#### Model nədir?

Odoo-da model, verilənlər bazasında cədvəl ilə təmsil olunan bir iş obyektidir. Texniki baxımdan, model Python sinfidir və `models.Model` sinfindən varislik alır. Hər model xüsusi bir biznes konsepsiyasını təmsil edir, məsələn, müştəri, məhsul, satış sifarişi və s.

Modellərin əsas vəzifəsi məlumatların strukturunu təyin etmək, biznes məntiqini icra etmək və istifadəçi interfeysi ilə qarşılıqlı əlaqəni təmin etməkdir.

#### Modelin təyin edilməsi

Yeni bir model yaratmaq üçün `models.Model` sinfindən varislik alan Python sinfi yaratmalısınız:

```python
from odoo import models, fields, api

class CourseModule(models.Model):
    _name = 'course.module'
    _description = 'Kurs Modulu'
    
    name = fields.Char(string='Adı', required=True)
    description = fields.Text(string='Təsvir')
```

Bu nümunədə:
- `_name`: Modelin texniki adıdır və verilənlər bazasında cədvəl adını təyin edir. Odoo, cədvəl adını `_name` dəyərindən yaradır, ancaq nöqtələri altxətlə əvəz edir (məsələn, `course.module` → `course_module`).
- `_description`: Modelin insanlar tərəfindən oxuna bilən təsviridir və istifadəçi interfeysi və qeydlər üçün istifadə olunur.
- `name` və `description`: Modelin sahələridir.

#### Model atributları

Modellər, onların davranışını və xüsusiyyətlərini təyin edən müxtəlif atributlara malikdir:

1. **`_name`**: Modelin unikal texniki adı (məcburidir, yeni model yaradılanda).

2. **`_inherit`**: Varislik üçün istifadə olunur. Mövcud modelin funksionallığını genişləndirmək üçün.
   ```python
   class ExtendedPartner(models.Model):
       _inherit = 'res.partner'
       
       new_field = fields.Char(string='Yeni Sahə')
   ```

3. **`_inherits`**: Delegasiya varisliliyi üçün. Bir modelin xüsusiyyətlərini digərinə delegasiya edir.
   ```python
   class Employee(models.Model):
       _name = 'hr.employee'
       _inherits = {'res.partner': 'partner_id'}
       
       partner_id = fields.Many2one('res.partner', required=True, ondelete='cascade')
   ```

4. **`_description`**: İnsan tərəfindən oxuna bilən təsvir.

5. **`_order`**: Standart sıralama meyarı.
   ```python
   _order = 'name, date desc'
   ```

6. **`_rec_name`**: Qeydin adını təmsil edən sahə (standart `name` sahəsidir).
   ```python
   _rec_name = 'code'  # 'name' əvəzinə 'code' sahəsi istifadə olunacaq
   ```

7. **`_table`**: Verilənlər bazasında cədvəl adı (standart olaraq `_name` əsasında yaradılır).
   ```python
   _table = 'custom_course_module'
   ```

8. **`_log_access`**: Avtomatik audit sahələrinin yaradılması (`create_date`, `write_date` və s.).
   ```python
   _log_access = False  # Audit sahələrini yaratma
   ```

9. **`_auto`**: `True` olduqda, Odoo avtomatik olaraq verilənlər bazasında cədvəl yaradır.
   ```python
   _auto = False  # Verilənlər bazasında cədvəl yaratma
   ```

10. **`_sql_constraints`**: SQL səviyyəsində məhdudiyyətlər.
    ```python
    _sql_constraints = [
        ('name_uniq', 'unique (name)', 'Kurs adı unikal olmalıdır!')
    ]
    ```

11. **`_constraints`**: Python səviyyəsində məhdudiyyətlər (Odoo 13+ versiyalarda `@api.constrains` ilə əvəz olunub).

#### Model təsdiqləri (validasiyalar)

Modellər üçün təsdiqlər, məlumatların doğruluğunu və tamlığını təmin etmək üçün istifadə olunur. İki əsas növ təsdiq var:

1. **SQL məhdudiyyətləri**: Verilənlər bazası səviyyəsində tətbiq olunur və çox effektivdir.
   ```python
   _sql_constraints = [
       ('code_uniq', 'unique (code)', 'Kod unikal olmalıdır!'),
       ('check_price', 'CHECK(price >= 0)', 'Qiymət mənfi ola bilməz!')
   ]
   ```

2. **Python məhdudiyyətləri**: Daha mürəkkəb məntiq üçün istifadə olunur.
   ```python
   @api.constrains('date_start', 'date_end')
   def _check_dates(self):
       for record in self:
           if record.date_start and record.date_end and record.date_start > record.date_end:
               raise models.ValidationError('Başlama tarixi bitmə tarixindən sonra ola bilməz!')
   ```

#### Nümunə: Tam model təyin edilməsi

Bir kurs modulu idarəetmə sistemi üçün tam bir model təyin edək:

```python
from odoo import models, fields, api
from odoo.exceptions import ValidationError
from datetime import timedelta

class Course(models.Model):
    _name = 'training.course'
    _description = 'Təlim Kursu'
    _order = 'sequence, name'
    
    name = fields.Char(string='Kursun Adı', required=True, index=True)
    code = fields.Char(string='Kod', required=True, index=True)
    description = fields.Text(string='Təsvir')
    sequence = fields.Integer(string='Ardıcıllıq', default=10)
    duration = fields.Float(string='Müddət (Saat)', default=1.0)
    price = fields.Float(string='Qiymət', digits=(10, 2))
    max_participants = fields.Integer(string='Maksimum İştirakçı Sayı')
    date_start = fields.Date(string='Başlama Tarixi')
    date_end = fields.Date(string='Bitmə Tarixi')
    active = fields.Boolean(string='Aktiv', default=True)
    state = fields.Selection([
        ('draft', 'Qaralama'),
        ('confirmed', 'Təsdiqlənmiş'),
        ('done', 'Tamamlanmış'),
        ('cancelled', 'Ləğv Edilmiş'),
    ], string='Status', default='draft')
    color = fields.Integer(string='Rəng İndeksi')
    tags_ids = fields.Many2many('training.tag', string='Etiketlər')
    instructor_id = fields.Many2one('res.partner', string='Təlimçi')
    
    _sql_constraints = [
        ('code_uniq', 'unique (code)', 'Kurs kodu unikal olmalıdır!'),
        ('check_price', 'CHECK(price >= 0)', 'Qiymət mənfi ola bilməz!'),
    ]
    
    @api.constrains('date_start', 'date_end')
    def _check_dates(self):
        for course in self:
            if course.date_start and course.date_end and course.date_start > course.date_end:
                raise ValidationError('Başlama tarixi bitmə tarixindən sonra ola bilməz!')
    
    @api.onchange('date_start', 'duration')
    def _onchange_date_start(self):
        if self.date_start and self.duration:
            hours = int(self.duration)
            days = hours // 8
            if days == 0:
                days = 1
            self.date_end = self.date_start + timedelta(days=days)
    
    def action_confirm(self):
        self.state = 'confirmed'
    
    def action_done(self):
        self.state = 'done'
    
    def action_draft(self):
        self.state = 'draft'
    
    def action_cancel(self):
        self.state = 'cancelled'
```

### Sahə növləri

Odoo-da müxtəlif növ sahələr mövcuddur və hər biri müxtəlif məlumat tipləri üçün istifadə olunur. Bu bölümdə, əsas sahə növlərini və onların xüsusiyyətlərini nəzərdən keçirəcəyik.

#### Əsas sahə növləri

1. **Char**: Qısa mətn sahəsi.
   ```python
   name = fields.Char(string='Adı', required=True, size=64, translate=True)
   ```
   - `size`: Maksimum simvol sayı (məhdudiyyət qoymaq istəyirsinizsə).
   - `translate`: `True` olduqda, bu sahə tərcümə edilə bilər.

2. **Text**: Uzun mətn sahəsi.
   ```python
   description = fields.Text(string='Təsvir', translate=True)
   ```

3. **Html**: HTML formatında mətn.
   ```python
   content = fields.Html(string='Məzmun', sanitize=True)
   ```
   - `sanitize`: `True` olduqda, təhlükəsizlik üçün HTML təmizlənir.

4. **Boolean**: Doğru/yanlış dəyəri.
   ```python
   active = fields.Boolean(string='Aktiv', default=True)
   ```

5. **Integer**: Tam ədəd.
   ```python
   sequence = fields.Integer(string='Ardıcıllıq', default=10)
   ```

6. **Float**: Kəsr ədəd.
   ```python
   price = fields.Float(string='Qiymət', digits=(10, 2))
   ```
   - `digits`: Ümumi rəqəm sayı və onluq hissədəki rəqəm sayı.

7. **Monetary**: Pul vahidi.
   ```python
   salary = fields.Monetary(string='Maaş', currency_field='currency_id')
   currency_id = fields.Many2one('res.currency', string='Valyuta')
   ```
   - `currency_field`: Valyuta sahəsinin adı.

8. **Date**: Tarix.
   ```python
   birth_date = fields.Date(string='Doğum Tarixi')
   ```

9. **Datetime**: Tarix və saat.
   ```python
   registration_datetime = fields.Datetime(string='Qeydiyyat Tarixi və Saatı', default=fields.Datetime.now)
   ```

10. **Binary**: İkili məlumat (məsələn, fayl).
    ```python
    attachment = fields.Binary(string='Əlavə')
    ```

11. **Selection**: Seçim siyahısı.
    ```python
    state = fields.Selection([
        ('draft', 'Qaralama'),
        ('confirmed', 'Təsdiqlənmiş'),
        ('done', 'Tamamlanmış'),
        ('cancelled', 'Ləğv Edilmiş'),
    ], string='Status', default='draft')
    ```
    - Birinci element texniki dəyərdir, ikinci element istifadəçiyə göstərilən etiketdir.

12. **Reference**: Fərqli modellərə dinamik əlaqə.
    ```python
    reference = fields.Reference(selection=[
        ('res.partner', 'Partner'),
        ('product.product', 'Məhsul'),
    ], string='İstinad')
    ```

#### Sahə parametrləri

Bütün sahə növləri üçün ümumi parametrlər:

1. **`string`**: İstifadəçi interfeysi üçün etiket.
   ```python
   name = fields.Char(string='Müştərinin Adı')
   ```

2. **`required`**: Sahə məcburidirmi?
   ```python
   name = fields.Char(string='Adı', required=True)
   ```

3. **`readonly`**: Sahə yalnız oxuna bilərmi?
   ```python
   code = fields.Char(string='Kod', readonly=True)
   ```

4. **`default`**: Standart dəyər.
   ```python
   active = fields.Boolean(string='Aktiv', default=True)
   ```
   - Funksiya da istifadə edə bilərsiniz:
   ```python
   date = fields.Date(string='Tarix', default=fields.Date.today)
   ```

5. **`index`**: Verilənlər bazasında indeks yaradılsınmı?
   ```python
   name = fields.Char(string='Adı', index=True)
   ```

6. **`copy`**: Qeyd kopyalandıqda bu sahə də kopyalansınmı?
   ```python
   reference = fields.Char(string='İstinad', copy=False)
   ```

7. **`groups`**: Hansı istifadəçi qrupları bu sahəni görə və/və ya dəyişə bilər.
   ```python
   salary = fields.Float(string='Maaş', groups='hr.group_hr_manager')
   ```

8. **`states`**: Vəziyyətə əsaslanan xüsusiyyətlər (məsələn, `readonly`).
   ```python
   description = fields.Text(string='Təsvir', states={
       'confirmed': [('readonly', True)],
       'done': [('readonly', True)],
   })
   ```

9. **`help`**: Kömək mətni (tooltip).
   ```python
   max_participants = fields.Integer(string='Maksimum İştirakçı Sayı', 
                                   help='Kursa qəbul ediləcək maksimum iştirakçı sayı')
   ```

10. **`company_dependent`**: Şirkətə bağlı dəyər (multi-company mühitində).
    ```python
    property_account_id = fields.Many2one('account.account', string='Hesab', 
                                        company_dependent=True)
    ```

### Əlaqəli sahələr

Odoo-da əlaqəli sahələr, müxtəlif modellər arasında əlaqələri təyin etmək üçün istifadə olunur. Əlaqəli sahələr, verilənlər bazasında əlaqələri (references) təmsil edir və relasiya modelində "foreign key" konsepsiyasına bənzərdir.

#### Many2one sahəsi

`Many2one` sahəsi, cari qeydin başqa bir modelin bir qeydinə əlaqəsini göstərir. Məsələn, bir sifariş bir müştəriyə aid ola bilər.

```python
customer_id = fields.Many2one('res.partner', string='Müştəri', required=True)
```

Bu sahə aşağıdakı parametrləri qəbul edir:
- `comodel_name`: Əlaqəli modelin adı ('res.partner').
- `ondelete`: Əlaqəli qeyd silindikdə nə baş verəcəyini təyin edir ('cascade', 'restrict', 'set null').
- `domain`: Əlaqəli modeldəki qeydləri süzmək üçün domen.
- `context`: Əlaqəli modeli açarkən keçirilən kontekst.
- `auto_join`: SQL sorğularda avtomatik birləşmələr üçün.

Nümunə:
```python
category_id = fields.Many2one('product.category', string='Kateqoriya', 
                           required=True, ondelete='restrict',
                           domain=[('active', '=', True)],
                           context={'default_active': True})
```

#### One2many sahəsi

`One2many` sahəsi, əlaqəli modeldəki qeydlərin siyahısını göstərir, hansı ki cari qeydə `Many2one` sahəsi ilə əlaqəlidir. Məsələn, bir müştərinin bir neçə sifarişi ola bilər.

```python
order_ids = fields.One2many('sale.order', 'customer_id', string='Sifarişlər')
```

Bu sahə aşağıdakı parametrləri qəbul edir:
- `comodel_name`: Əlaqəli modelin adı ('sale.order').
- `inverse_name`: Əlaqəli modeldə cari modelə geri əlaqə yaradan `Many2one` sahəsinin adı ('customer_id').
- `domain`: Əlaqəli qeydləri süzmək üçün domen.
- `context`: Əlaqəli qeydləri yaradarkən və ya redaktə edərkən keçirilən kontekst.

Nümunə:
```python
line_ids = fields.One2many('sale.order.line', 'order_id', string='Sifariş Xətləri',
                        domain=[('state', '!=', 'cancel')],
                        context={'default_state': 'draft'})
```

#### Many2many sahəsi

`Many2many` sahəsi, cari modelin qeydləri ilə başqa bir modelin qeydləri arasında çoxdan-çoxa əlaqəni təmsil edir. Məsələn, bir məhsul bir neçə etiketə aid ola bilər və bir etiket bir neçə məhsula aid ola bilər.

```python
tag_ids = fields.Many2many('product.tag', string='Etiketlər')
```

Bu sahə aşağıdakı parametrləri qəbul edir:
- `comodel_name`: Əlaqəli modelin adı ('product.tag').
- `relation`: Münasibət cədvəlinin adı (standart olaraq yaradılır, lakin dəqiqləşdirilə bilər).
- `column1`: Cari modelin ID-sini saxlayan münasibət cədvəlindəki sütun.
- `column2`: Əlaqəli modelin ID-sini saxlayan münasibət cədvəlindəki sütun.
- `domain`: Əlaqəli qeydləri süzmək üçün domen.
- `context`: Əlaqəli qeydləri yaradarkən və ya redaktə edərkən keçirilən kontekst.

Nümunə:
```python
category_ids = fields.Many2many(
    'product.category',
    'product_category_rel',
    'product_id',
    'category_id',
    string='Kateqoriyalar',
    domain=[('active', '=', True)]
)
```

#### Reference sahəsi

`Reference` sahəsi, fərqli modellərə dinamik əlaqələrə imkan verir. Bu, cari qeydin eyni sahədən müxtəlif modellərə əlaqəli olmasına imkan verir.

```python
resource = fields.Reference(selection=[
    ('res.partner', 'Partner'),
    ('product.product', 'Məhsul'),
], string='Resurs')
```

Bu sahə aşağıdakı parametrləri qəbul edir:
- `selection`: Mümkün modellərin siyahısı.
- `selection_add`: Mövcud seçimə əlavə etmək üçün (varislikdə istifadə olunur).

#### Əlaqəli sahələrlə işləmək

Əlaqəli sahələrdən dəyərləri oxumaq və yazmaq:

```python
# Many2one oxuma
partner_name = record.partner_id.name
# Many2one yazma
record.partner_id = self.env['res.partner'].browse(1)  # ID ilə
record.partner_id = partner_record  # Qeyd obyekti ilə

# One2many oxuma
for line in record.line_ids:
    print(line.name)
# One2many yazma
line_vals = {'name': 'Yeni xətt', 'price': 100.0}
record.line_ids = [(0, 0, line_vals)]  # Yeni xətt əlavə et
record.line_ids = [(1, line_id, {'price': 200.0})]  # Mövcud xətti yenilə
record.line_ids = [(2, line_id, 0)]  # Xətti sil
record.line_ids = [(5, 0, 0)]  # Bütün xətləri sil
record.line_ids = [(6, 0, [1, 2, 3])]  # Xətləri ID-lər ilə əvəz et

# Many2many oxuma
for tag in record.tag_ids:
    print(tag.name)
# Many2many yazma (One2many ilə eyni formada)
record.tag_ids = [(4, tag_id, 0)]  # Tag əlavə et
record.tag_ids = [(3, tag_id, 0)]  # Tag sil
record.tag_ids = [(6, 0, [1, 2, 3])]  # Tag-ları ID-lər ilə əvəz et
```

### Hesablanmış sahələr və metodlar

Hesablanmış sahələr, başqa sahələrə əsasən dinamik şəkildə hesablanan sahələrdir. Bu, məlumatların təkrarlanmasını azaldır və həmişə ən son hesablanmış dəyərlərin olmasını təmin edir.

#### Hesablanmış sahələr

Hesablanmış sahəni təyin etmək üçün `compute` parametrindən istifadə olunur:

```python
total_amount = fields.Float(string='Ümumi Məbləğ', compute='_compute_total_amount')

@api.depends('line_ids.price', 'line_ids.quantity')
def _compute_total_amount(self):
    for record in self:
        record.total_amount = sum(line.price * line.quantity for line in record.line_ids)
```

Burada:
- `compute`: Hesablama metodunun adı.
- `@api.depends`: Hansı sahələrin dəyişməsi ilə hesablamanın yenidən işə salınacağını göstərir.

Hesablanmış sahələr üçün əlavə parametrlər:
- `store`: `True` olduqda, hesablanmış dəyər verilənlər bazasında saxlanılır.
- `readonly`: Standart olaraq `True`-dur, amma `inverse` təyin edildikdə `False` ola bilər.
- `inverse`: Sahə dəyişdirildikdə çağırılacaq metod (oxunulabilən hesablanmış sahələr üçün).
- `search`: Sahə üzrə axtarış edilərkən çağırılacaq metod.

Nümunə:
```python
full_name = fields.Char(string='Tam Ad', compute='_compute_full_name', 
                      store=True, readonly=False, inverse='_inverse_full_name')

@api.depends('first_name', 'last_name')
def _compute_full_name(self):
    for record in self:
        if record.first_name or record.last_name:
            record.full_name = (record.first_name or '') + ' ' + (record.last_name or '')
        else:
            record.full_name = ''

def _inverse_full_name(self):
    for record in self:
        parts = record.full_name.split(' ', 1)
        record.first_name = parts[0] if parts else ''
        record.last_name = parts[1] if len(parts) > 1 else ''
```

#### Əlaqəli hesablanmış sahələr

Odoo, əlaqəli qeydlərdəki sahələrə əsasən hesablanmış sahələri dəstəkləyir:

```python
partner_credit = fields.Float(string='Kredit', related='partner_id.credit', store=True)
```

Burada:
- `related`: Əlaqəli qeydin sahə yolunu göstərir.
- `store`: `True` olduqda, əlaqəli dəyər verilənlər bazasında saxlanılır.

Əlaqəli sahələr daha dərin əlaqələrə də dəstək verir:
```python
country_name = fields.Char(string='Ölkə', related='partner_id.country_id.name')
```

#### Metodlar

Odoo-da modellər üçün müxtəlif növ metodlar mövcuddur:

1. **API metodları**:
   - `@api.model`: Tək qeydə bağlı olmayan metodlar üçün.
   ```python
   @api.model
   def get_default_currency(self):
       return self.env.company.currency_id
   ```
   
   - `@api.multi` (Odoo 13+ versiyalarda default): Bir və ya bir neçə qeyd üçün çağırıla bilən metodlar.
   ```python
   def action_confirm(self):
       for record in self:
           record.state = 'confirmed'
       return True
   ```

2. **CRUD metodları**: Create, Read, Update, Delete funksiyalarını təyin edən metodlar.
   - `create`: Yeni qeydlər yaratmaq üçün.
   ```python
   @api.model
   def create(self, vals):
       if 'code' not in vals:
           vals['code'] = self.env['ir.sequence'].next_by_code('my.model')
       return super(MyModel, self).create(vals)
   ```
   
   - `write`: Mövcud qeydləri yeniləmək üçün.
   ```python
   def write(self, vals):
       if 'state' in vals and vals['state'] == 'done':
           vals['completion_date'] = fields.Date.today()
       return super(MyModel, self).write(vals)
   ```
   
   - `unlink`: Qeydləri silmək üçün.
   ```python
   def unlink(self):
       for record in self:
           if record.state == 'done':
               raise UserError('Tamamlanmış qeydlər silinə bilməz!')
       return super(MyModel, self).unlink()
   ```
   
   - `copy`: Qeydləri kopyalamaq üçün.
   ```python
   def copy(self, default=None):
       default = dict(default or {})
       default.update({'state': 'draft', 'name': _('%s (copy)') % self.name})
       return super(MyModel, self).copy(default)
   ```

3. **Hadisə işləyiciləri**:
   - `@api.onchange`: İstifadəçi interfeysi dəyişikliklərini idarə etmək üçün.
   ```python
   @api.onchange('product_id')
   def _onchange_product_id(self):
       if self.product_id:
           self.price_unit = self.product_id.list_price
           self.name = self.product_id.name
   ```
   
   - `@api.constrains`: Qeydlərin doğruluğunu yoxlamaq üçün.
   ```python
   @api.constrains('date_start', 'date_end')
   def _check_dates(self):
       for record in self:
           if record.date_start and record.date_end and record.date_start > record.date_end:
               raise ValidationError('Başlama tarixi bitmə tarixindən sonra ola bilməz!')
   ```
   
   - `@api.depends`: Hesablanmış sahələrin asılılıqlarını təyin etmək üçün.
   ```python
   @api.depends('line_ids.price_subtotal')
   def _compute_amount(self):
       for order in self:
           order.amount_total = sum(line.price_subtotal for line in order.line_ids)
   ```

4. **ORM metodları**:
   - `search`: Qeydləri axtarmaq üçün.
   ```python
   partners = self.env['res.partner'].search([('customer_rank', '>', 0), ('active', '=', True)])
   ```
   
   - `browse`: ID ilə qeydləri əldə etmək üçün.
   ```python
   partner = self.env['res.partner'].browse(1)
   ```
   
   - `filtered`, `mapped`, `sorted`: Qeyd dəstini manipulyasiya etmək üçün.
   ```python
   active_partners = partners.filtered(lambda p: p.active)
   partner_names = partners.mapped('name')
   sorted_partners = partners.sorted(lambda p: p.name)
   ```

### Praktiki nümunə: Təhsil İdarəetmə Sistemi

İndi öyrəndiyimiz konsepsiyaları tətbiq edərək, sadə bir təhsil idarəetmə sistemi yaradaq. Bu sistem kursları, tələbələri və qeydiyyatları idarə edəcək.

#### Kurs modeli

```python
from odoo import models, fields, api
from odoo.exceptions import ValidationError

class Course(models.Model):
    _name = 'education.course'
    _description = 'Kurs'
    _order = 'sequence, name'
    
    name = fields.Char(string='Kursun Adı', required=True, index=True)
    code = fields.Char(string='Kod', required=True, index=True)
    description = fields.Text(string='Təsvir')
    sequence = fields.Integer(string='Ardıcıllıq', default=10)
    duration = fields.Float(string='Müddət (Saat)', default=1.0)
    price = fields.Float(string='Qiymət', digits=(10, 2))
    max_participants = fields.Integer(string='Maksimum İştirakçı Sayı')
    instructor_id = fields.Many2one('res.partner', string='Təlimçi', 
                                  domain=[('instructor', '=', True)])
    category_id = fields.Many2one('education.course.category', string='Kateqoriya')
    tag_ids = fields.Many2many('education.tag', string='Etiketlər')
    session_ids = fields.One2many('education.session', 'course_id', string='Sessiyalar')
    session_count = fields.Integer(string='Sessiya Sayı', compute='_compute_session_count')
    participant_ids = fields.Many2many('education.student', string='İştirakçılar',
                                    compute='_compute_participants')
    participant_count = fields.Integer(string='İştirakçı Sayı', 
                                     compute='_compute_participant_count')
    active = fields.Boolean(string='Aktiv', default=True)
    state = fields.Selection([
        ('draft', 'Qaralama'),
        ('open', 'Açıq'),
        ('closed', 'Bağlı'),
    ], string='Status', default='draft')
    color = fields.Integer(string='Rəng')
    
    _sql_constraints = [
        ('code_uniq', 'unique (code)', 'Kurs kodu unikal olmalıdır!'),
        ('check_price', 'CHECK(price >= 0)', 'Qiymət mənfi ola bilməz!'),
    ]
    
    @api.depends('session_ids')
    def _compute_session_count(self):
        for course in self:
            course.session_count = len(course.session_ids)
    
    @api.depends('session_ids.registration_ids.student_id')
    def _compute_participants(self):
        for course in self:
            students = course.session_ids.mapped('registration_ids.student_id')
            course.participant_ids = students
    
    @api.depends('participant_ids')
    def _compute_participant_count(self):
        for course in self:
            course.participant_count = len(course.participant_ids)
    
    @api.constrains('max_participants')
    def _check_max_participants(self):
        for course in self:
            if course.max_participants and course.max_participants < 0:
                raise ValidationError('Maksimum iştirakçı sayı mənfi ola bilməz!')
    
    def action_open(self):
        self.state = 'open'
    
    def action_close(self):
        self.state = 'closed'
    
    def action_draft(self):
        self.state = 'draft'
    
    def action_view_sessions(self):
        return {
            'name': 'Sessiyalar',
            'type': 'ir.actions.act_window',
            'res_model': 'education.session',
            'view_mode': 'tree,form',
            'domain': [('course_id', '=', self.id)],
        }
    
    def action_view_participants(self):
        return {
            'name': 'İştirakçılar',
            'type': 'ir.actions.act_window',
            'res_model': 'education.student',
            'view_mode': 'tree,form',
            'domain': [('id', 'in', self.participant_ids.ids)],
        }
```

#### Sessiya modeli

```python
from odoo import models, fields, api
from odoo.exceptions import ValidationError
from datetime import timedelta

class Session(models.Model):
    _name = 'education.session'
    _description = 'Təlim Sessiyası'
    
    name = fields.Char(string='Adı', required=True, compute='_compute_name', store=True)
    course_id = fields.Many2one('education.course', string='Kurs', required=True, 
                              ondelete='cascade')
    start_date = fields.Date(string='Başlama Tarixi', required=True, default=fields.Date.today)
    end_date = fields.Date(string='Bitmə Tarixi', compute='_compute_end_date', store=True)
    duration = fields.Float(string='Müddət (Gün)', default=1.0)
    instructor_id = fields.Many2one('res.partner', string='Təlimçi', 
                                  related='course_id.instructor_id', store=True)
    location = fields.Char(string='Məkan')
    registration_ids = fields.One2many('education.registration', 'session_id', 
                                     string='Qeydiyyatlar')
    attendee_count = fields.Integer(string='İştirakçı Sayı', 
                                  compute='_compute_attendee_count')
    max_participants = fields.Integer(string='Maksimum İştirakçı Sayı', 
                                    related='course_id.max_participants')
    taken_seats_percentage = fields.Float(string='Doluluk Faizi (%)', 
                                        compute='_compute_taken_seats')
    active = fields.Boolean(string='Aktiv', default=True)
    state = fields.Selection([
        ('draft', 'Qaralama'),
        ('confirmed', 'Təsdiqlənmiş'),
        ('done', 'Tamamlanmış'),
        ('cancelled', 'Ləğv Edilmiş'),
    ], string='Status', default='draft')
    color = fields.Integer(string='Rəng')
    
    @api.depends('course_id', 'start_date')
    def _compute_name(self):
        for session in self:
            if session.course_id and session.start_date:
                session.name = f"{session.course_id.name} ({session.start_date})"
            elif session.course_id:
                session.name = session.course_id.name
            else:
                session.name = "Yeni Sessiya"
    
    @api.depends('start_date', 'duration')
    def _compute_end_date(self):
        for session in self:
            if session.start_date and session.duration:
                duration = int(session.duration)
                if duration < 1:
                    duration = 1
                session.end_date = session.start_date + timedelta(days=duration - 1)
            else:
                session.end_date = session.start_date
    
    @api.depends('registration_ids')
    def _compute_attendee_count(self):
        for session in self:
            session.attendee_count = len(session.registration_ids)
    
    @api.depends('registration_ids', 'max_participants')
    def _compute_taken_seats(self):
        for session in self:
            if not session.max_participants:
                session.taken_seats_percentage = 0.0
            else:
                session.taken_seats_percentage = (session.attendee_count / session.max_participants) * 100
    
    @api.onchange('max_participants', 'registration_ids')
    def _verify_valid_seats(self):
        if self.max_participants and self.attendee_count > self.max_participants:
            return {
                'warning': {
                    'title': "Çox iştirakçı",
                    'message': "İştirakçı sayı maksimum iştirakçı sayını aşır!",
                }
            }
    
    @api.constrains('instructor_id', 'registration_ids')
    def _check_instructor_not_in_attendees(self):
        for session in self:
            students = session.registration_ids.mapped('student_id.partner_id')
            if session.instructor_id and session.instructor_id in students:
                raise ValidationError("Təlimçi öz sessiyasında iştirakçı ola bilməz!")
    
    def action_confirm(self):
        self.state = 'confirmed'
    
    def action_done(self):
        self.state = 'done'
    
    def action_cancel(self):
        self.state = 'cancelled'
    
    def action_draft(self):
        self.state = 'draft'
```

#### Tələbə modeli

```python
from odoo import models, fields, api

class Student(models.Model):
    _name = 'education.student'
    _description = 'Tələbə'
    _inherit = ['mail.thread', 'mail.activity.mixin']
    
    name = fields.Char(string='Adı', required=True, tracking=True)
    partner_id = fields.Many2one('res.partner', string='Əlaqəli Partner', 
                              required=True, ondelete='cascade')
    email = fields.Char(string='E-poçt', related='partner_id.email', readonly=False)
    phone = fields.Char(string='Telefon', related='partner_id.phone', readonly=False)
    birth_date = fields.Date(string='Doğum Tarixi')
    registration_ids = fields.One2many('education.registration', 'student_id', 
                                     string='Qeydiyyatlar')
    course_count = fields.Integer(string='Kurs Sayı', compute='_compute_course_count')
    session_ids = fields.Many2many('education.session', string='Sessiyalar',
                                compute='_compute_sessions', store=True)
    active = fields.Boolean(string='Aktiv', default=True)
    image = fields.Binary(string='Şəkil', related='partner_id.image_1920')
    
    @api.depends('registration_ids.session_id.course_id')
    def _compute_course_count(self):
        for student in self:
            courses = student.registration_ids.mapped('session_id.course_id')
            student.course_count = len(courses)
    
    @api.depends('registration_ids.session_id')
    def _compute_sessions(self):
        for student in self:
            student.session_ids = student.registration_ids.mapped('session_id')
    
    @api.model
    def create(self, vals):
        if not vals.get('partner_id'):
            partner = self.env['res.partner'].create({
                'name': vals.get('name'),
                'email': vals.get('email'),
                'phone': vals.get('phone'),
                'company_type': 'person',
            })
            vals['partner_id'] = partner.id
        return super(Student, self).create(vals)
    
    def action_view_courses(self):
        courses = self.registration_ids.mapped('session_id.course_id')
        return {
            'name': 'Kurslar',
            'type': 'ir.actions.act_window',
            'res_model': 'education.course',
            'view_mode': 'tree,form',
            'domain': [('id', 'in', courses.ids)],
        }
```

#### Qeydiyyat modeli

```python
from odoo import models, fields, api
from odoo.exceptions import ValidationError

class Registration(models.Model):
    _name = 'education.registration'
    _description = 'Kurs Qeydiyyatı'
    _rec_name = 'session_id'
    
    session_id = fields.Many2one('education.session', string='Sessiya', required=True,
                               ondelete='cascade')
    course_id = fields.Many2one('education.course', string='Kurs', 
                             related='session_id.course_id', store=True)
    student_id = fields.Many2one('education.student', string='Tələbə', required=True,
                               ondelete='cascade')
    registration_date = fields.Date(string='Qeydiyyat Tarixi', default=fields.Date.today)
    state = fields.Selection([
        ('draft', 'Qaralama'),
        ('confirmed', 'Təsdiqlənmiş'),
        ('attended', 'İştirak Etdi'),
        ('cancelled', 'Ləğv Edilmiş'),
    ], string='Status', default='draft')
    attendance = fields.Float(string='İştirak (%)', default=0.0)
    feedback = fields.Text(string='Rəy')
    
    _sql_constraints = [
        ('unique_registration', 'unique(session_id, student_id)', 
         'Tələbə artıq bu sessiyaya qeydiyyatdan keçib!'),
    ]
    
    @api.constrains('attendance')
    def _check_attendance(self):
        for registration in self:
            if registration.attendance < 0 or registration.attendance > 100:
                raise ValidationError('İştirak faizi 0 ilə 100 arasında olmalıdır!')
    
    @api.onchange('session_id')
    def _onchange_session(self):
        if self.session_id and self.session_id.attendee_count >= self.session_id.max_participants:
            return {
                'warning': {
                    'title': "Sessiya Doludur",
                    'message': "Bu sessiya artıq maksimum iştirakçı sayına çatıb!",
                }
            }
    
    def action_confirm(self):
        self.state = 'confirmed'
    
    def action_attend(self):
        self.state = 'attended'
    
    def action_cancel(self):
        self.state = 'cancelled'
    
    def action_draft(self):
        self.state = 'draft'
```

### Nəticə

Bu bölümdə Odoo-da modellər və sahələr haqqında ətraflı məlumat əldə etdik. Modellərin yaradılması, müxtəlif sahə növləri, əlaqəli sahələr və hesablanmış sahələr haqqında öyrəndik. Eyni zamanda, praktiki bir nümunə vasitəsilə öyrəndiklərimizi tətbiq etdik.

Modellər və sahələr, Odoo inkişafının əsasını təşkil edir və hər bir Odoo tətbiqinin məlumat strukturunu müəyyən edir. Bu konsepsiyaları yaxşı anlamaq, uğurlu Odoo modulları yaratmaq üçün vacibdir.

Növbəti bölümdə, istifadəçi interfeysi elementlərindən olan görünüşləri (views) araşdıracağıq və istifadəçilərin məlumatlarla necə qarşılıqlı əlaqədə olduğunu öyrənəcəyik.

---

**Praktiki tapşırıq:**

1. Bu bölümdə yaratdığımız Təhsil İdarəetmə Sistemi modellərinə əsaslanaraq tam bir modul yaradın.
2. Aşağıdakı əlavə funksionallıqları əlavə edin:
   - Kurs materialları üçün model yaradın (`Binary` sahələrdən istifadə edərək).
   - Tələbə imtahan nəticələrini izləmək üçün model yaradın.
   - Kurslara qiymətləndirmə sistemi əlavə edin.
3. Hesablanmış sahələrdən istifadə edərək, tələbənin ümumi performansını hesablayan funksionallıq əlavə edin.
4. Məhdudiyyətlər əlavə edərək, məlumatların doğruluğunu və tamlığını təmin edin.
